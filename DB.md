# Database Schema Documentation

## 📌 Tables Structure

### User & Auth Tables

```sql
Table User {
  userId        integer       [primary key]
  fullName      varchar(100)
  email         varchar(100)  [unique]
  phone         varchar(20)   [unique]
  password      varchar(255)
  isActive      boolean       [default: true]
  createdAt     timestamp
  updatedAt     timestamp
}
Role Management
sql
Table Role {
  roleId     integer       [primary key]
  name       varchar(50)   [unique] // Admin, Customer, Support
  createdAt  timestamp
}

Table UserRole {
  userRoleId  integer     [primary key]
  userId      integer
  roleId      integer
  createdAt   timestamp

  indexes {
    (userId, roleId) [unique]
  }
}
Airport & City Lookup
sql
Table City {
  cityId     integer       [primary key]
  name       varchar(100)
  country    varchar(100)
}

Table Airport {
  airportId     integer     [primary key]
  name          varchar(255)
  code          varchar(10) [unique]
  cityId        integer
}
Flights
sql
Table Flight {
  flightId        integer     [primary key]
  airline         varchar(100)
  fromAirportId   integer
  toAirportId     integer
  departureTime   timestamp
  arrivalTime     timestamp
  price           decimal(10,2)
  seatsAvailable  integer
  createdAt       timestamp

  indexes {
    (fromAirportId, toAirportId)
  }
}
Hotels & Rooms
sql
Table Hotel {
  hotelId     integer        [primary key]
  name        varchar(255)
  location    varchar(255)
  rating      decimal(2,1)
  logoUrl     varchar(512)
}

Table Room {
  roomId       integer        [primary key]
  hotelId      integer
  type         varchar(100)   // "Single", "Double", "Suite"
  price        decimal(10,2)
  capacity     integer
  isAvailable  boolean
}
Booking Core
sql
Table Booking {
  bookingId    integer        [primary key]
  userId       integer
  type         varchar(20)    // "flight", "hotel"
  status       varchar(20)    // "confirmed", "cancelled", "pending"
  totalAmount  decimal(10,2)
  createdAt    timestamp
}

Table BookingItem {
  bookingItemId   integer     [primary key]
  bookingId       integer
  referenceId     integer      // links to flightId or roomId
  itemType        varchar(10)  // "flight", "hotel"
  quantity        integer
  price           decimal(10,2)
}
Payment & Checkout
sql
Table Payment {
  paymentId     integer        [primary key]
  bookingId     integer
  method        varchar(50)    // "Card", "Wallet", "PayPal"
  status        varchar(20)    // "paid", "failed"
  transactionId varchar(255)
  amount        decimal(10,2)
  paidAt        timestamp
}
Favorites & Trips
sql
Table Favorite {
  favoriteId   integer       [primary key]
  userId       integer
  itemType     varchar(10)   // "flight", "hotel"
  referenceId  integer
  createdAt    timestamp

  indexes {
    (userId, itemType, referenceId) [unique]
  }
}

Table SavedTrip {
  tripId       integer       [primary key]
  userId       integer
  name         varchar(100)
  flightId     integer
  hotelId      integer
  createdAt    timestamp
}
🔗 Foreign Key Relationships
User & Role Management
UserRole.userId → User.userId

UserRole.roleId → Role.roleId

Geographic Data
Airport.cityId → City.cityId

Flights
Flight.fromAirportId → Airport.airportId

Flight.toAirportId → Airport.airportId

Hotels
Room.hotelId → Hotel.hotelId

Booking System
Booking.userId → User.userId

BookingItem.bookingId → Booking.bookingId

Payment.bookingId → Booking.bookingId

Polymorphic References (BookingItem)
BookingItem.referenceId → Flight.flightId (when itemType = 'flight')

BookingItem.referenceId → Room.roomId (when itemType = 'hotel')

Favorites
Favorite.userId → User.userId

Favorite.referenceId → Flight.flightId (when itemType = 'flight')

Favorite.referenceId → Room.roomId (when itemType = 'hotel')

Saved Trips
SavedTrip.userId → User.userId

SavedTrip.flightId → Flight.flightId

SavedTrip.hotelId → Hotel.hotelId
