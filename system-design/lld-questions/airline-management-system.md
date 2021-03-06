# Airline Management System

##

#### System Requirements:

* **Search Flights:** To search the flight schedule to find flights for a suitable date and time.
* **Create/Modify/View reservation:** To reserve a ticket, cancel it, or view details about the flight or ticket.
* **Assign seats to passengers:** To assign seats to passengers for a flight instance with their reservation.
* **Make payment for a reservation:** To pay for the reservation.
* **Update flight schedule:** To make changes in the flight schedule, and to add or remove any flight.
* **Assign pilots and crew:** To assign pilots and crews to flights.

#### **Classes**

**1.Constants ===============================================================**

* **FlightStatus**: PENDING, CONFIRMED, CHECKED\_IN, CANCELED
* \*\*PaymentStatus \*\*:REGULAR, PREMIUM
* \*\*ReservationStatus \*\*: UNPAID, PENDING, COMPLETED, DECLINED, CANCELLED, REFUNDED
* **SeatClass** :
* **SeatType** :

**2.Accounts ===============================================================**

* **Account** - interface
  * password
  * name
  * status
  * reset\_password(self)
* **Customer**
  * name
  * address
  * email
  * phone
  * account
* **Admin(Account)**
  * add\_movie(self, movie)
  * add\_show(self, show)
* **Passenger(Customer)**
  * passport\_number
  * get\_passport\_number()

**3.Airport ===============================================================**

* **Airport**
  * name
  * address
  * code
  * get\_flights()
* **Aircraft**
  * name
  * model
  * manufacturing\_year
  * seats = \[]
  * get\_flights()
* **Seat**
  * seat\_number
  * type
  * seat\_class
* **FlightSeat**
  * fare

**4.Airline Manager==============================================================**

* **Flight** :
  * flight\_number
  * departure
  * arrival
  * schedule = \[]
* **FlightReservation**
  * reservation\_number
  * flight
  * seat\_map
  * creation\_date
  * status
  * fetch\_reservation\_details(self, reservation\_number)
  * get\_passengers(self)
* **Itinerary**
  * customer\_id
  * starting\_airport
  * final\_airport
  * creation\_date
  * reservations = \[]
  * get\_reservations(self)
  * make\_reservation(self)
  * make\_payment(self)

{% tabs %}
{% tab title="constants.py" %}
```python
from enum import Enum

class FlightStatus(Enum):
    ACTIVE, SCHEDULED, DELAYED, DEPARTED, LANDED, IN_AIR = 1, 2, 3, 4, 5, 6, 7


class PaymentStatus(Enum):
    UNPAID, PENDING, COMPLETED, CANCELLED, SETTLING, REFUNDED = 1, 2, 3, 4, 5, 6


class ReservationStatus(Enum):
    PENDING, CONFIRMED, CHECKED_IN, CANCELLED = 1, 2, 3, 4

class SeatClass(Enum):
    ECONOMY BUSINESS = 1, 2


class SeatType(Enum):
    REGULAR, EMERGENCY_EXIT, EXTRA_LEG_ROOM = 1, 2, 3
```
{% endtab %}

{% tab title="account.py" %}
```python
from abc import ABC
from .constants import *


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


class Customer(ABC):
    def __init__(self, name, address, email, phone, account):
        self.__name = name
        self.__address = address
        self.__email = email
        self.__phone = phone
        self.__account = account

class Passenger(Customer):
    def __init__(self, name, passport_number):
        self.__passport_number = passport_number

    def get_passport_number(self):
        return self.__passport_number
```
{% endtab %}

{% tab title="airport.py" %}
```python
class Airport:
    def __init__(self, name, address, code):
        self.__name = name
        self.__address = address
        self.__code = code

    def get_flights(self):
        None


class Aircraft:
    def __init__(self, name, model, manufacturing_year):
        self.__name = name
        self.__model = model
        self.__manufacturing_year = manufacturing_year
        self.__seats = []

    def get_flights(self):
        None


class Seat:
    def __init__(self, seat_number, type, seat_class):
        self.__seat_number = seat_number
        self.__type = type
        self.__seat_class = seat_class


class FlightSeat(Seat):
    def __init__(self, fare):
        self.__fare = fare

    def get_fare(self):
        return self.__fare
```
{% endtab %}

{% tab title="airline_manager.py" %}
```python
class Flight:
    def __init__(self, flight_number, departure, arrival, duration_in_minutes):
        self.__flight_number = flight_number
        self.__departure = departure
        self.__arrival = arrival

        self.__schedule = []

class FlightReservation:
    def __init__(self, reservation_number, flight, aircraft, creation_date, status):
        self.__reservation_number = reservation_number
        self.__flight = flight
        self.__seat_map = {}
        self.__creation_date = creation_date
        self.__status = status

    def fetch_reservation_details(self, reservation_number):
        None

    def get_passengers(self):
        None


class Itinerary:
    def __init__(self, customer_id, starting_airport, final_airport, creation_date):
        self.__customer_id = customer_id
        self.__starting_airport = starting_airport
        self.__final_airport = final_airport
        self.__creation_date = creation_date
        self.__reservations = []

    def get_reservations(self):
        None

    def make_reservation(self):
        None

    def make_payment(self):
        None
```
{% endtab %}
{% endtabs %}

##
