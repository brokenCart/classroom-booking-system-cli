# Classroom Booking System CLI

Classroom Booking System CLI is a lightweight command-line application designed for managing classroom availability and booking schedules across campus buildings.

## Description

The Classroom Booking System CLI provides a simple and efficient way to handle classroom allocations without external database dependencies or complex user interfaces. Built entirely using Python's standard library, the application maintains room metadata—such as building names, seating capacities, and hourly booking states (0–23 hours)—with automatic persistence to a local CSV file. Users can register new rooms, search for available spaces based on custom criteria, reserve hourly slots with double-booking prevention, and review schedule details directly from the terminal.

## Key Features

- **Room Management**: Add classrooms with custom room numbers, building names, and seating capacities.
- **Search and Filtering**: Locate available classrooms filtered by building, minimum capacity, specific free hours, or a combination of all three.
- **Reservation System**: Book specific hour slots (0–23) with built-in validation to prevent double-booking.
- **Schedule Inspection**: View comprehensive details and booked time slots for any registered room.
- **CSV Data Persistence**: Store and load classroom schedules automatically using `bookings_final_state.csv`.
- **Zero External Dependencies**: Works out-of-the-box on standard Python installations without requiring third-party libraries.

## Installation

### Prerequisites

- Python 3.6 or higher installed on your system.

### Setup Instructions

1. Clone the repository:

   ```bash
   git clone https://github.com/brokenCart/classroom-booking-system-cli.git
   cd classroom-booking-system-cli
   ```

2. Run the application:

   ```bash
   python main.py
   ```

No virtual environment or dependency installation via `pip` is needed.

## Usage

Launch the CLI application by running `python main.py` to display the interactive menu:

```
Welcome to the Classroom Booking System!
-----------------------------------------

What would you like to do?
1. Create a new Room
2. Find Available Rooms
3. Book a Room
4. View a Room's Schedule
5. Exit
Enter your choice:
```

### Command Options

- **Option 1 (Create a new Room)**: Prompts for room number, building name, and capacity.
- **Option 2 (Find Available Rooms)**: Filters rooms by building, minimum capacity, and/or free hour slot.
- **Option 3 (Book a Room)**: Reserves a specified room for a target hour slot.
- **Option 4 (View a Room's Schedule)**: Displays room details and all currently booked hours.
- **Option 5 (Exit)**: Saves all updates to `bookings_final_state.csv` and exits.

## Project Structure

```
classroom-booking-system-cli/
├── main.py                     # Entry point and interactive CLI menu loop
├── classroom.py                # Core domain models and booking system logic
├── errors.py                   # Custom error definitions
├── bookings_final_state.csv    # CSV data storage file
├── .gitignore
└── README.md
```

## Data Format

Data is stored in `bookings_final_state.csv` with the following schema:

| Column | Type | Description |
|---|---|---|
| `room_no` | string | Unique identifier for the room |
| `building` | string | Building name or code |
| `capacity` | integer | Maximum seating capacity |
| `booked_hours` | string | Semicolon-separated list of booked hours (0-23) |

Example:

```csv
room_no,building,capacity,booked_hours
NAB101,NAB,60,
5105,LTC,300,4
1223,FD-I,60,
```
