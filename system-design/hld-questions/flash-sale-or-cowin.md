# Flash Sale | CoWin

### Resources

* Src: [amazing Shopify Video](https://www.youtube.com/watch?v=-I4tIudkArY\&ab\_channel=ShopifyEngineering)

## About the system?

* **Limited availability system:** both in terms of
  1. **quantity**: Number of ordering request is much larger than inventory size. (1 million users competing for 10,000 items/slots)
  2. **time**: Large number of users come to the system at the same time, causing a spike in traffic. (sales starts at 6am and finishs at 6:30am)
* System is checkout-driven; ==> so its **write-heavy**
  * so we **cant** simply just push a **Cache** in front of everything & call it a day
* social-media bashing when/if you fail => **Reputation**

## Challenges&#x20;

#### => What are the challenges we're dealing with?

1. **Handle load on read**. Users will constantly **refresh** the page\*\* to check available inventory\*\*. It’s also likely that all users will **request for other similar resource at the same time**, such as account, item description, etc.
2. **Provide high throughput**. There will be many **concurrent read and write** to the limited inventory records, so the **database lock** may result in timeout for some of the requests.
3. **Avoid** inventory from being **oversold or undersold.** how to handle the available inventory number?
   * An item may be oversold if multiple requests reserved the same inventory. A
   * n item may be undersold if the inventory is hold but the process failed and inventory is not released.
   * This happened to some e-commerce website, and usually they will call the customers to **refund**.
4. **Prevent cheating with script**. user could write a script to fire request in a **loop**. so this user may generate many repeated requests



## 3. APIs&#x20;

* /catalogue/:item\_id
* /checkout

## 4. HLD

![basic HLD](../../.gitbook/assets/screenshot-2021-09-04-at-12.13.31-pm.png)

![Detailed HLD](../../.gitbook/assets/screenshot-2021-09-04-at-12.13.39-pm.png)

## How to scale-up for FlashSales

* \*\*@client side: \*\*
  * **@UI:** Disable submit button once clicked
  * **@server side**: dont allow mulitple reqs with same `item_id `& `user_id`
* \*\*@DB(sql): \*\*
  * have a `serialisable` \*\*isolation level \*\*for the transaction which affects performance.
    * If we do not apply this isolation level, we may end up with phantom read and thought that we still have enough inventory this request, and then we sell more than what we have.
    * To handle this, we can use a **counter with atomicity**. **Redis** will be a good choice for atomic decrement when a request need to be processed.
  * read replicas
  * sharding
* Use Application LB (such as **NGNIX)**, it can be used for:
  * Reverse Proxy
  * Edge LB
  * Request throttling
  * SSL
* **Back Pressure/ Leaky Bucket: ---> to improve UX**
  * Even if you've optimized every query; you cant server all the requests
  * Make the platform handle back-pressure: "Hey wait, I'm at full capacity. Come back later"
  * This\*\* Back Pressure\*\* can be implemented using **Leaky Bucket**.
  * **LOGIC:================================**
    * \*\*Algorithms to Rate Limit the reqs (\*\*taken from #12. API **)**
    *   **Token Bucket❌**

        * For every user; store his last API hit time & number of tokens left
        * **e.g: ProductHunt API**
        * `user_id -> {last_hit_time, tokens_left}`
        * store this in **key-val DB (Redis)**
        * for each new request; update the values in DB
        * Deny request when tokens\_left = 0
        * \*\*Con: \*\*not useful here, as every req is from a new user

        **2. Leaky Bucket ✅**

        * maintain a **fixed-size-queue**
        * All the incoming req(from all users) are processed via this queue(in \*\*FIFO \*\*order)
        * when the queue size is full; deny the incoming requests

        **3. Fixed Window Counter❌**
    * only **N** requests can be processed in a time \*\*T \*\*
    * so for every window of **`|t .... t+T| `**; count the incoming reqs;
      * when the **counter reached N**; deny the further reqs in this **time duration**
      * **Con:** bad UX & data loss
  * **HOW TO IMPLEMENT =============================================**
    * when you cant handle new checkout requests, serve a **Throttle page**, saying-"Hey, we got your checkout; we'll process it soon.Pleas be patient"
    * **STEPS**:
    * user sends a` /checkout` req to LB
    * LB is out of capacity; so it asks for a **throttle page** from server
    * LB caches this throttle page for future requests & serve it to the user
    * this Throttle page has **Javascript** & some sort of **refresh tags**; that constantly **polls the LB in background**-"hey, do you have capacity now?"
    * when the LB has capacity; it would pass the req to App server
    * And the LB places a **cookie** on **user session**, that "hey, dont throttle this req anymore"
    * So to user; it looks like there wasn't any throttle at all.
  * **CON:**
    * if a user comes at min=0; he has to wait for 30 mins
    * if a user comes at min=29; he might get lucky & have to wait just 1 min
    * So overall; it wouldn't improve the user-chaos
    * **How to solve:**
      * add the timestamp(of when user entered into queue) with the cookie
      * each LB will process these reqs in FIFO
      * but since there are multiple LB's; the system won't be fully stateless; but decent enough

![](../../.gitbook/assets/screenshot-2021-09-04-at-11.36.14-am.png)

fa
