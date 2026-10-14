# Debugging Report – Overlapping Bookings

## 1. Which error did I investigate?

I investigated a bug where the booking system did not detect all overlapping bookings. This could allow a user to book a room when it was already reserved during part of the requested time.

## 2. How did I reproduce the error?

I used an existing booking in the room Aspen from 09:00 to 11:00 on 2026-10-15. I then attempted to create another booking in Aspen from 10:00 to 12:00 on the same date.

## 3. What result did I get?

The original validation logic could miss overlaps when the new booking started before the existing booking or when the time intervals overlapped in other ways.

## 4. What result should I have got?

The application should reject any new booking that overlaps an active booking in the same room on the same date. It should display:

`The room is already booked during the selected time.`

A booking from 11:00 to 12:00 should be allowed because it starts exactly when the existing booking ends.

## 5. Which part of the code caused the error?

The error was in the overlap validation inside the `Validate()` method in `BookingService.cs`.

## 6. Why did the code produce an incorrect result?

The original condition only checked whether the new booking's start time was within the existing booking's time interval. It did not check whether the new booking started earlier and ended while the existing booking was still active. Therefore, some overlapping time intervals were not detected.

## 7. What did I change?

I changed the overlap condition to:

```csharp
booking.StartTime < existing.EndTime &&
booking.EndTime > existing.StartTime
```

The validation also checks that the existing booking is not cancelled and that the room and date match.

## 8. How did I verify the fix?

I built the solution and tested a booking in Aspen from 10:00 to 12:00 when an existing booking occupied 09:00 to 11:00. The application rejected the new booking and displayed the expected error message. I also ran the automated test suite, and all 14 tests passed.

## 9. Which automated test protects against regression?

The test `Create_WhenBookingOverlapsExistingBooking_ReturnsFailure` in `BookingServiceTests.cs` verifies that a new booking is rejected when it overlaps an existing booking. This test helps prevent the same bug from returning in future changes.