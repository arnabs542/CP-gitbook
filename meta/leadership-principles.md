# LeaderShip Principles

## S.T.A.R. Format

\======> Situation -> Task -> Action -> Result

## Things To Talk About:

* **@BITS**
  * DTN project
  * Apriori project
* **@BARC**
  * Office Management System
  * Telephone Directory
* **@Nestaway**
  * Linguini
* **@Rzp**
  * Mozart: integration + test\_coverage
  * Capital: instant loans, instant refunds, KYC integration
  * OTP-elf
* **@Flipkart**
  * Keyword Targeting
  * Sampling
    * computation reduced by 80%
    * real impact during BBD sale 21
  * Bidding Price Recommendation System
  * Ads Merch Separation
  * Pricing Service Feedback
  * Jarvis
  * RCAs
  * NFRs

\====================================================================

#### <mark style="color:yellow;">🤨 -> Tell me about a time when you challenged the status quo.</mark>

\==> 1. Implemented Jarvis platfor for helping out oncall's redundant tasks ==> 2. Sampling

#### <mark style="color:yellow;">🤨 -> Time when you were 75% through a project and realized you had the wrong goal.\</mark></mark>

\==> ?

#### <mark style="color:yellow;">🤨 -> Time when you pushed back a decision from your management for better long term benefits.\</mark></mark>

\==> brand & category enrichment in BSS:

* new platform | first time occurence during the Independence Day Sale
* typecast mismatch from Java's List to Sark's Wrapped Array
  * WrappedArray wraps an Array to give it extra functionality. It also have a bunch of types while array extends only serializable and cloneable, This allows an array to be wrapped so it can be used in places where some generic collection type like Seq is required.
* CORRECTIVE MEASURES:
  * fixed the bug in one night(during sale oncall) collaborating with the ingestion team & serving team
  * (post fix)published Detailed RCA in tech-session withdebugging steps &
  * increased learning of spark & how spark's typecasting work
* Implemented the same type-safety in pipeline's code & added UTs for the same
* IMPACT:Even though we missed the SLA for the first night of sale(Early Access); we fixed the issue on time for the smoother sale

#### <mark style="color:yellow;">🤨 -> Tell me about a time you faced an obstacle and how you overcame it.</mark>

\==> ?

#### <mark style="color:yellow;">🤨 -> Tell me a time you took some on some risk</mark>

\==> ?

#### <mark style="color:yellow;">🤨 -> Have you ever gone out of your way to help a peer? (ownership)\</mark></mark>

\==> 1. yes, several nights up till 2 AM/weekends helping out new joinees/ oncall issues

#### <mark style="color:yellow;">🤨 -> Tell me about a time when you learned new technologies\</mark></mark>

\==> 1. Learning about big data tech upon entering Flipkart

#### <mark style="color:yellow;">🤨 -> Tell me about a time you had multiple solutions and you had to select an optimal one</mark>

\==> 1. Keyword Targeting algos&#x20;

\==> 2. Sampling&#x20;

\==> 3. Linguini

#### <mark style="color:yellow;">🤨 -> Tell me about a time when you innovated and exceeded the expectation</mark>

\==> 1. Sampling : 80% computation time&#x20;

\==> 2. Keyword targeting

#### <mark style="color:yellow;">🤨 -> Handling a tight deadline\</mark></mark>

\==> Sampling

#### <mark style="color:yellow;">🤨 -> How would you help a new employee who is facing technical difficulties?</mark>

\==>

#### <mark style="color:yellow;">🤨 -> disagree and commit and ownership LPs.</mark>

#### <mark style="color:yellow;">🤨 -> Tell me about a time when you had conflicting ideas with your teammates and how did you resolve them</mark>

\==> 1. Linguini&#x20;

\==> 2. KeywordTargeting: algo selection

#### <mark style="color:yellow;">🤨 -> Tell me about time when you faced a difficult challenge.\</mark></mark>

\==> 1. Sampling&#x20;

\==>

#### <mark style="color:yellow;">🤨 -> Tell me about a time when you needed help from someone during a project.</mark>

\==> 1. Onboardings - everywhere&#x20;

\==> 2. Bidding Price Recommendation System : from data-science team

#### <mark style="color:yellow;">🤨 -> Tell me about a time when you thought of an unpopular idea.</mark>

\==> 1. Keyword targeting: not using standard Edit Dist. but researched-> N-Gram&#x20;

\==> 2. Mozart- test coverage => build Tree & BFS ==> 3. Linguini

#### <mark style="color:yellow;">🤨 -> Tell me about a time when you had to decide upon something without consulting your superior.</mark>

\===> 1. Ads Merch separation

* SITUATION/TASK:
  * (cant disclose much internal details)
  * our deployment was impacted due to a recent(same day) deployment; which was not writing Unserved's data to correct sql tables => hence impacting their reporting
  * By the time I figured this out, it was 2AM & the (senior) person who had done the other deployment was slept(had to catc a flight next day)
* ACTION:
  * I got access to that project's config (by awaking some other team member at 2:30 AM)
  * first thing; I stopped the flow to wrong tables => to avoid false positives & dedups
  * Fixed the issue by morning, got PR approved @8AM
  * Triggered reruns for the lost buckets with the help of oncall person

#### <mark style="color:yellow;">🤨 -> Tell me about a time when you did not meet your deadlines for a project | Tell me about a time when you had to face tight time constraints during a project.</mark>

\==> 1. Never(maybe in college lol)&#x20;

\==> 2. tight timeline for Sampling before BBD'21. but stretched over 3 weekends to go live on time

<mark style="color:yellow;">🤨 -></mark> <mark style="color:yellow;">**a project you're proud of**</mark>

\==> Sampling@Rzp | Capital@Rzp

#### <mark style="color:yellow;">🤨 -> a time when you faced a setback initially but still achieved the goal.</mark>\ <mark style="color:yellow;">a time when you had to cut corners to meet a deadline</mark>

\==> Pricing Service Feedback @FK

* SITUATION/TASK:
  * It was a 2-sprint project, was working with 1 (senior) teammate
  * Nearly at the end of 1st sprint, he had to leave immediately due to a medical emeregency at his home(2nd wave)
  * All the responsibility fell onto my shoulders, I was new to that pipeline as well
* ACTION:
  * first thing I did for next 2 days was collected all the info about his tasks (over phone calls, syncing with other team's resp. people)
  * I documented everything & shared it with all the stakeholders for cross-verification
    * thanks for him, that we were able to have a phone call in around every 2 days; for doubt clarification
* RESULT:
  * We completed the project on time
  * It even got me a letter of praise by the multiple-teams & a gift voucher

#### <mark style="color:yellow;">🤨 -> Tell me about a time where you had to make a decision based on limited information and how it impacted the outcome</mark>

<mark style="color:yellow;">**🤨 -> Tell me about a time when you felt under pressure that you wouldn't be able to get something done or had to take a pivot at the last minute**</mark>

\==> Linguini@Nestaway

* 6 months internship; got project in the last 1.5 months
* change of 3 mentors caused too much skeweness in POC (spent enough time with image processing, comparing GCP/AWS/Azure, pricing) \\
* last 3 weeks remaind; panicked as mentor@college was asking for pre-demo & ppt
* improvised & went ahead with speech-to-text + targetted-keywords matching

#### <mark style="color:yellow;">🤨 -> Time when your team members were not supporting something but you pushed and went for a more optimal solution.\</mark></mark>

#### <mark style="color:yellow;">🤨 -> Tell me about a situation where you had a conflict with someone on your team. What was it about? What did you do? How did they react? What was the outcome?</mark>

\==>

#### <mark style="color:yellow;">🤨 -> Give an example of when you saw a peer struggling and decided to step in and help. What was the situation and what actions did you take? What was the outcome?\\</mark>

\==>

#### <mark style="color:yellow;">🤨 -> Tell me about a time you committed a mistake?</mark>

\==>

#### <mark style="color:yellow;">🤨 -> Tell me about a time when your earned your teammate's trust?</mark>

\==>

#### <mark style="color:yellow;">🤨 -> Tell me about a time when you couldn't meet your deadline?</mark>

\==>

#### <mark style="color:yellow;">🤨 -> Tell me about a time when your teammate didn't agree with you? What did you do?</mark>

\==>

#### <mark style="color:yellow;">🤨 -> Tell me about a time when you invented something?</mark>

\==>

#### <mark style="color:yellow;">🤨 -> Tell me about a time when you took important decision without any data?</mark>

\==>

#### <mark style="color:yellow;">🤨 -> Tell me about a time when you helped one of your teammates?</mark>

\==>

#### <mark style="color:yellow;">🤨 -> Have you ever been in a situation where you had to make a choice among a few options, but did not have a lot of time to explore each option</mark>

\==>

#### <mark style="color:yellow;">🤨 -> Have you ever failed at something? What did you learn from it?</mark>

\==>

#### <mark style="color:yellow;">🤨 -> name time when you went out of your way to help someone?</mark>

\==>

#### <mark style="color:yellow;">🤨 -> Time when you came up with novel solution.\</mark></mark>

\==>

#### <mark style="color:yellow;">🤨 -> Received negative feedback from manager and how you responded.\</mark></mark>

\==>

#### <mark style="color:yellow;">🤨 -> Time when you went above and beyond your job responsibilities.\</mark></mark>

\==>

#### <mark style="color:yellow;">🤨 -> Time when you did not have enough data and had to use judgement to make decision.\</mark></mark>

\==>

#### <mark style="color:yellow;">🤨 -> Time when you helped someone in their work.\</mark></mark>

\==>

#### <mark style="color:yellow;">🤨 -> Time when you helped someone grow in career and it benefited them.\</mark></mark>

\==>

#### <mark style="color:yellow;">🤨 -> Time when you helped someone grow but did not benefit them.\</mark></mark>

\==>

\==================================================================

**1. Why do you want to quit your current job ?**

* The job is becoming more data-engineering intensive; as things are progressing in the ecosystem.But I dont want to switch the domain from Software Developer to completely DE. -> this was the key factor I decided to start looking out.
* and unable to switch teams due to internal policies.
* <mark style="color:green;">not learning anything new as product is in a saturated state,</mark>
* <mark style="color:green;">NEVER EVER talk about bad boss, politics etc - it will backfire bigtime.</mark>

**2.What has been the biggest failure of your career till now ? OR What is the most critical feedback received from your boss in your entire career ?**

* \*\*WHAT: \*\*brand & category enrichment in BSS
  * new platform | first time occurence during the Independence Day Sale
  * typecast mismatch from Java's **`List`** to Sark's **`Wrapped Array`**
    * `WrappedArray` wraps an `Array` to give it extra functionality. It also have a bunch of types while array extends only serializable and cloneable, This allows an array to be wrapped so it can be used in places where some generic collection type like `Seq` is required.
* **CORRECTIVE MEASURES:**
  * fixed the bug in one night(during sale oncall) collaborating with the ingestion team & serving team
  * (post fix)
  * published Detailed RCA in tech-session with
    * debugging steps &
    * increased learning of spark & how spark's typecasting work
  * Implemented the same type-safety in pipeline's code & added UTs for the same
* **IMPACT:**
  * Even though we missed the SLA for the first night of sale(Early Access); we fixed the issue on time for the smoother sale.

***

**3. What would you like to improve at your current workplace ? OR What do you dislike/hate at your current job/workplace ?**

* <mark style="color:green;">a trap - if you badmouth your current employer or use any words like</mark> <mark style="color:green;">**hate**</mark> <mark style="color:green;">or</mark> <mark style="color:green;">**dislike**</mark><mark style="color:green;">, it is guaranteed to go against you.</mark>
* Talk about generic things like -
  * sometimes code reviews take a long time due to senior developers being busy
    * probably that can be streamlined.
  * Or say - we should invest more in enhancing the\*\* test automation infrastructure\*\*, which often takes a backseat due to various constraints
  * (!) too many senior people leaving - has resulted in a knowledge bottleneck
* <mark style="color:green;">Basically, try to stay around technical things, and avoid talking about poor cafeteria or no free cab pickup-drop services etc.</mark>
* <mark style="color:green;">The motive is to show your passion towards work related things and not focus on secondary things like cafeteria or cabs or playgrounds etc.</mark>

**4. Are you happy at your current job ?**

* <mark style="color:green;">This is also a big trap.</mark>\ <mark style="color:green;">If you talk only about goody-goody positive things, then this question will be immediately followed by -</mark> <mark style="color:green;">**if you like your job, then why are you looking around for another job**</mark><mark style="color:green;">?</mark>
* <mark style="color:green;">So, answer it diplomatically around point 1 of this post. Talk about good things like - I have gotten to learn a lot.</mark>
  * Got to explore data side
  * Worked on such big scale
* <mark style="color:green;">Then talk about negatives - again in polished way</mark>
  * Domain shift

**5. What would you do if you find your senior or boss doing something unethical or violating a company policy ?**

Always talk about that you would gently point out to that person directly, and request that person to follow the correct process. In case the violations continue, then I would like to know about the violation reporting policy of your company.

Here, you can turnaround the interview by **cross-questioning** your interviewer - "**by the way, can you give a brief insight into policy violation reporting mechanism which exists in this company ?**"

**6. What is your greatest weakness ?**

* <mark style="color:green;">No, NO, NO - please do not talk about</mark> <mark style="color:green;">**being impatient or pushing your team hard etc etc**</mark><mark style="color:green;">. These are all very very well-known answers.</mark>
* <mark style="color:green;">Talk about something more genuine and possibly not related to work -</mark> I am not so good at remembering names of people I interact with for first few times.
* <mark style="color:green;">But be prepared to answer -</mark> **what are you doing to overcome this weakness** ?
* <mark style="color:green;">Possible answers to above examples may be -</mark> **Hi X**, I am using this technique to use the name of the person I am interacting with first time in conversation