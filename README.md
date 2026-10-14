# Meeting Room Booking System

A console application for managing meeting room bookings. The project was provided as a starter project for an individual coding exam and has been extended with booking management functionality and bug fixes.

## Features

- **View active bookings:** Display active bookings sorted by date and start time.
- **Search bookings:** Search for customers by full or partial name, regardless of letter case.
- **Create bookings:** Register bookings with customer details, meeting room, date, time, and number of participants.
- **Cancel bookings:** Cancel an existing booking using its booking number.
- **Booking validation:** Validate customer names, room capacity, booking times, and overlapping bookings.
- **File storage:** Store bookings in a JSON file so that changes persist after restarting the application.

## Meeting Rooms

| Room | Capacity |
|---|---:|
| Aspen | 4 participants |
| Birken | 8 participants |
| Eken | 12 participants |

## Requirements

- .NET 10 SDK

## Run the Application

From the repository root, run:

```bash
dotnet run --project src/BookingSystem
```

Follow the console menu to view, search, create, or cancel bookings.

## Run the Tests

Run the automated tests from the repository root:

```bash
dotnet test
```

The tests use xUnit and cover booking service functionality, including validation, searching, and cancellation.

## Project Structure

```text
BookingSystemExam-Student/
├── src/
│   └── BookingSystem/
├── tests/
├── docs/
│   └── DEBUGGING.md
└── README.md
```

## Debugging Report

The report describing the investigation and correction of the overlapping booking validation bug is available in [`docs/DEBUGGING.md`](docs/DEBUGGING.md).