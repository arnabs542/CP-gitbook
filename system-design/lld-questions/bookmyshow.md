# BookMyShow



#### System Requirements:

* **Search movies:** To search movies by title, genre, language, release date, and city name.
* **Create/Modify/View booking:** To book a movie show ticket, cancel it or view details about the show.
* **Make payment for booking:** To pay for the booking.
* **Add a coupon to the payment:** To add a discount coupon to the payment.
* **Assign Seat:** Customers will be shown a seat map to let them select seats for their booking.
* **Refund payment:** Upon cancellation, customers will be refunded the payment amount as long as the cancellation occurs within the allowed time frame.

#### **Classes**

**1.Constants ===============================================================**

* **BookingStatus**: PENDING, CONFIRMED, CHECKED\_IN, CANCELED
* **SeatType**:REGULAR, PREMIUM
* **PaymentStatus**: UNPAID, PENDING, COMPLETED, DECLINED, CANCELLED, REFUNDED

**2.Acc\_Types ===============================================================**

* **Account** - interface
  * password
  * name
  * email
  * reset\_password(self)
* **Customer(Account)**
  * make\_booking(self, booking)
  * get\_bookings()
* **Admin(Account)**
  * add\_movie(self, movie)
  * add\_show(self, show)
* **Guest(Account)**
  * register()

**3.Shows ===============================================================**

* **Show**
  * show\_id
  * created\_on
  * start\_time
  * end\_time
  * played\_at
  * movie
* **Movie**
  * title
  * description
  * duration
  * language
  * release\_date
  * country
  * genre
  * shows = \[]
  * get\_shows()

**4.Cinema ===============================================================**

* **Search** : parent
  * search\_products\_by\_name(self, name)
  * search\_products\_by\_category(self, category)
* **Catalog(Search)**
  * product\_names
  * product\_categories
  * search\_products\_by\_name(self, name)
  * search\_products\_by\_category(self, category)

**5.Search ===============================================================**

* \*\*Search : \*\*interface
  * search\_by\_title(self, title)
  * search\_by\_language(self, language)
  * search\_by\_genre(self, genre)
  * search\_by\_city(self, city\_name)
* **Catalog**
  * movie\_titles = {}
  * movie\_languages = {}
  * movie\_genres = {}
  * movie\_release\_dates = {}
  * movie\_cities = {}
  * search\_by\_title(self, title)
  * search\_by\_language(self, language)
  * search\_by\_city(self, city\_name)

**6.Booking ===============================================================**

* **Booking**
  * booking\_number
  * number\_of\_seats
  * created\_on
  * status
  * show
  * seats
  * payment
  * make\_payment(self, payment)
  * cancel(self)
  * assign\_seats(self, seats)
* **Payment**
  * amount
  * created\_on
  * transaction\_id
  * status

{% tabs %}
{% tab title="constants.py" %}
```python
from enum import Enum

class BookingStatus(Enum):
    PENDING, CONFIRMED, CHECKED_IN, CANCELED = 1, 2, 3, 4

class SeatType(Enum):
    REGULAR, PREMIUM = 1, 2

class PaymentStatus(Enum):
    UNPAID, PENDING, COMPLETED, DECLINED, CANCELLED, REFUNDED = 1, 2, 3, 4, 5, 6
```
{% endtab %}

{% tab title="account_types.py" %}
```python
from abc import ABC
from .constants import AccountStatus


# For simplicity, we are not defining getter and setter functions. The reader can
# assume that all class attributes are private and accessed through their respective
# public getter methods and modified only through their public methods function.


class Account:
    def __init__(self, id, password, status=AccountStatus.Active):
        self.__id = id
        self.__password = password
        self.__status = status

    def reset_password(self):
        None


# from abc import ABC, abstractmethod
class Person(ABC):
    def __init__(self, name, address, email, phone, account):
        self.__name = name
        self.__address = address
        self.__email = email
        self.__phone = phone
        self.__account = account


class Customer(Person):
    def make_booking(self, booking):
        None

    def get_bookings(self):
        None


class Admin(Person):
    def add_movie(self, movie):
        None

    def add_show(self, show):
        None


class Guest:
    def register_account(self):
        None
```
{% endtab %}

{% tab title="show.py" %}
```python
from datetime import datetime

class Show:
    def __init__(self, id, played_at, movie, start_time, end_time):
        self.__show_id = id
        self.__created_on = datetime.date.today()
        self.__start_time = start_time
        self.__end_time = end_time
        self.__played_at = played_at
        self.__movie = movie


class Movie:
    def __init__(self, title, description, duration_in_mins, language, release_date, country, genre, added_by):
        self.__title = title
        self.__description = description
        self.__duration_in_mins = duration_in_mins
        self.__language = language
        self.__release_date = release_date
        self.__country = country
        self.__genre = genre

        self.__shows = []

    def get_shows(self):
        None
```
{% endtab %}

{% tab title="cinema.py" %}
```python
class City:
    def __init__(self, name, state, zip_code):
        self.__name = name
        self.__state = state
        self.__zip_code = zip_code

class Cinema:
    def __init__(self, name, total_cinema_halls, address, halls):
        self.__name = name
        self.__location = address

        self.__halls = halls


class CinemaHall:
    def __init__(self, name, total_seats, seats, shows):
        self.__name = name
        self.__total_seats = total_seats

        self.__seats = seats
        self.__shows = shows


class CinemaHallSeat:
    def __init__(self, id, seat_type):
        self.__hall_seat_id = id
        self.__seat_type = seat_type
```
{% endtab %}

{% tab title="search.py" %}
```python
from abc import ABC

class Search(ABC):
    def search_by_title(self, title):
        None

    def search_by_language(self, language):
        None

    def search_by_genre(self, genre):
        None

    def search_by_city(self, city_name):
        None


class Catalog(Search):
    def __init__(self):
        self.__movie_titles = {}
        self.__movie_languages = {}
        self.__movie_genres = {}
        self.__movie_release_dates = {}
        self.__movie_cities = {}

        def search_by_title(self, title):
            return self.__movie_titles.get(title)

        def search_by_language(self, language):
            return self.__movie_languages.get(language)

        def search_by_city(self, city_name):
            return self.__movie_cities.get(city_name)
```
{% endtab %}

{% tab title="booking.py" %}
```python
from datetime import datetime
from .cinema import CinemaHallSeat


class Booking:
    def __init__(self, booking_number, number_of_seats, status, show, show_seats, payment):
        self.__booking_number = booking_number
        self.__number_of_seats = number_of_seats
        self.__created_on = datetime.date.today()
        self.__status = status
        self.__show = show
        self.__seats = show_seats
        self.__payment = payment

    def make_payment(self, payment):
        None

    def cancel(self):
        None

    def assign_seats(self, seats):
        None


class Payment:
    def __init__(self, amount, transaction_id, payment_status):
        self.__amount = amount
        self.__created_on = datetime.date.today()
        self.__transaction_id = transaction_id
        self.__status = payment_status
```
{% endtab %}
{% endtabs %}

##
