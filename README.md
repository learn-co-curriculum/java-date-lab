# Date Lab

## Learning Goals

- Use the classes from the `java.time` package.
- Make use of formatting dates using the `DateTimeFormatter` class.

## Introduction

In this lesson, we will practice using classes from the new Date and Time API.
We'll also practice parsing and formatting dates using the `DateTimeFormatter`
class.

Fork and clone this repository. When you do, you will see a `Hotel` class, a
`Reservation` class, and a `HotelTest` class for unit testing.

## Instructions

Create a simple reservation system for a hotel where guests can create or
cancel their reservation.

Follow the given instructions and tips:

- Create a `Reservation` class.
  - The `Reservation` class will need the following properties:
    - Name of the guest.
    - Check-in date and time using the format "MM/dd/uuuu HH:mm".
      - Example: "09/13/2022 11:30".
    - Number of nights.
    - A constructor that takes in the above properties as arguments.
      - For the check-in property, have the constructor take in a `String`
        that needs to be parsed to a date and time object.
    - Accessor methods for accessing the instance variables.
  - Implement this class **before** implementing the `Hotel` class.
- Create a `Hotel` class.
  - The `Hotel` class will have the following properties:
    - List of `Reservation` objects called `reservations`.
  - Create a getter method for the list of `Reservation` objects.
  - The `Hotel` class will need to be able to add a reservation.
    - Write the code for the `addReservation()` method.
    - Do not add a reservation if the number of nights is less than or equal
      to 0.
    - If we can add the reservation, return a `String` with the checkout date
      and time based on the number of nights the reservation is for and the
      check-in date.
      - Use the format "MM/dd/uuuu HH:mm" for the checkout date.
      - Example: "Your reservation is set! Check-out is at 09/14/2022 11:30".
    - If we cannot add the reservation, return a `String` saying the reservation
      cannot be made.
      - Example: "Sorry, your reservation is invalid and cannot be added".
    - Remove the `@Disabled` annotation from the `addReservationTest()` method
      in the unit test and run the test.
    - Remove the `@Disabled` annotation from the `edgeCaseTest()` method in the
      unit test and run the test.

Run all the unit tests in the `HotelTest` class and ensure everything passes.
You mal also run the tests with the IntelliJ debugger, or the Java Visualizer.

## Starter Code

Consider the starter code below:
123456789101112131415161718192021222324252627ac282930313233343536373839404041434

### Reservation.java

```java
public class Reservation {

  // Finish implementing the class

  public Reservation(String name, String checkin, int numberOfNights) {
    // Write the constructor code here
  }
}
```

### Hotel.java

```java
import java.util.ArrayList;
import java.util.List;

public class Hotel {

    public Hotel() {
    }

    public List<Reservation> getReservations() {
        // Write code here
        return new ArrayList<>();
    }

    public String addReservation(Reservation reservation) {
        // Write code here
        return "";
    }
}
```

### HotelTest.java

```java
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Disabled;
import org.junit.jupiter.api.Test;

import static org.junit.jupiter.api.Assertions.*;

class HotelTest {

    private Hotel testHotel;

    @BeforeEach
    void setUp() {
        testHotel = new Hotel();
    }

    @Disabled
    @Test
    void addReservationTest() {

        // Add a reservation to the hotel
        Reservation testReservation1 =
                new Reservation("April Ludgate", "10/01/2022 10:00", 1);
        String expectedResult = "Your reservation is set! Check-out is at 10/02/2022 10:00";
        assertEquals(expectedResult, testHotel.addReservation(testReservation1));
        assertFalse(testHotel.getReservations().isEmpty());
        assertEquals(1, testHotel.getReservations().size());

        // Add another reservation to the hotel
        Reservation testReservation2 =
                new Reservation("Andy Dwyer", "09/30/2022 12:15", 5);
        expectedResult = "Your reservation is set! Check-out is at 10/05/2022 12:15";
        assertEquals(expectedResult, testHotel.addReservation(testReservation2));
        assertEquals(2, testHotel.getReservations().size());
    }

    @Disabled
    @Test
    void edgeCaseTest() {

        // We should not allow a reservation to be made with 0 or negative nights

        // Add a reservation to the hotel with zero nights
        Reservation testReservation1 =
                new Reservation("Jerry Gergich", "10/10/2022 11:45", 0);
        String expectedResult = "Sorry, your reservation is invalid and cannot be added";
        assertEquals(expectedResult, testHotel.addReservation(testReservation1));
        assertTrue(testHotel.getReservations().isEmpty());

        // Add another reservation to the hotel with negative nights
        Reservation testReservation2 =
                new Reservation("Jerry Gergich", "10/10/2022 11:45", -2);
        assertEquals(expectedResult, testHotel.addReservation(testReservation2));
        assertTrue(testHotel.getReservations().isEmpty());
    }
}
```
