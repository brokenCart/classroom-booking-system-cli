# 🏫 Classroom Booking System — CLI

A command-line application for managing classroom bookings across campus buildings. Built as a recruitment task for the **Students' Union Technical Team (SUTT)** at **BITS Pilani**.

---

## ✨ Features

- **Create Rooms** — Add new classrooms with a room number, building name, and seating capacity.
- **Search & Filter** — Find available rooms by building, minimum capacity, or a specific free hour. Filters can be combined for precise results.
- **Book Rooms** — Reserve a room for a specific hour slot (0–23).
- **View Schedules** — Inspect any room's details and see which hours are already booked.
- **Persistent Storage** — All data is saved to and loaded from a CSV file (`bookings_final_state.csv`), so bookings survive between sessions.

---

## 🛠️ Tech Stack

| Component | Details |
|-----------|---------|
| Language  | Python 3 |
| Storage   | CSV (via Python's built-in `csv` module) |
| External Dependencies | **None** — uses only the standard library |

---

## 🚀 Getting Started

### Prerequisites

- Python 3.6 or higher

### Installation

```bash
git clone https://github.com/brokenCart/classroom-booking-system-cli.git
cd classroom-booking-system-cli
```

### Run

```bash
python main.py
```

> No virtual environment or `pip install` step is required — the project has zero external dependencies.

---

## 📖 Usage

On launch, the system loads existing room data from `bookings_final_state.csv` and presents an interactive menu:

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

### 1 · Create a New Room

Add a classroom by providing its room number (e.g., `NAB101`), building name, and capacity.

### 2 · Find Available Rooms

Search with optional filters — all three can be combined:

| Filter | Description |
|--------|-------------|
| Building Name | Show only rooms in a specific building |
| Minimum Capacity | Show rooms that seat at least *n* people |
| Free Hour (0–23) | Show rooms that are unbooked during that hour |

### 3 · Book a Room

Reserve a room by entering its Room ID and the desired hour slot. The system prevents double-booking with a clear error message.

### 4 · View a Room's Schedule

Displays a room's building, capacity, and a list of all currently booked hours.

### 5 · Exit

Saves all data to the CSV file and exits gracefully.

---

## 📁 Project Structure

```
classroom-booking-system-cli/
├── main.py                     # Entry point — interactive CLI menu loop
├── classroom.py                # Core logic — BookingSystem & Room classes
├── errors.py                   # Custom exception classes
├── bookings_final_state.csv    # Persistent data store (CSV)
├── .gitignore
└── README.md
```

### Module Breakdown

| File | Purpose |
|------|---------|
| `main.py` | Runs the interactive menu, handles user I/O, and orchestrates calls to the booking system |
| `classroom.py` | Contains `BookingSystem` (room CRUD, filtering, CSV I/O) and `Room` (data model with hourly booking slots) |
| `errors.py` | Defines `RoomAlreadyExistsError`, `RoomNotFoundError`, and `TimeslotAlreadyBookedError` for clean error handling |

---

## 📐 Architecture

```
┌──────────┐       ┌──────────────┐       ┌──────┐
│  main.py │──────▶│ BookingSystem │──────▶│ Room │
│  (CLI)   │       │  (Manager)   │       │(Model)│
└──────────┘       └──────┬───────┘       └──────┘
                          │
                   ┌──────▼───────┐
                   │  errors.py   │
                   │ (Exceptions) │
                   └──────────────┘
                          │
                   ┌──────▼───────────────┐
                   │ bookings_final_state  │
                   │       (.csv)          │
                   └──────────────────────-┘
```

- **`main.py`** acts as the controller — it captures user input and delegates to `BookingSystem`.
- **`BookingSystem`** manages a dictionary of `Room` objects and handles all business logic (creation, booking, filtering, persistence).
- **`Room`** is a simple data model holding the room number, building, capacity, and a boolean array of 24 hourly booking slots.
- **`errors.py`** provides descriptive custom exceptions so users get clear, actionable error messages.

---

## 📊 Data Format

Room data is persisted in `bookings_final_state.csv` with the following schema:

| Column | Type | Description |
|--------|------|-------------|
| `room_no` | `str` | Unique room identifier (e.g., `NAB101`, `5101`) |
| `building` | `str` | Building name (e.g., `NAB`, `LTC`, `FD-I`) |
| `capacity` | `int` | Maximum seating capacity |
| `booked_hours` | `str` | Semicolon-separated list of booked hour slots (e.g., `4;10;15`) |

**Example:**

```csv
room_no,building,capacity,booked_hours
NAB101,NAB,60,
5105,LTC,300,4
1223,FD-I,60,
```

---

## 🤝 Contributing

This project was developed as a SUTT recruitment task. Feel free to fork and extend it — ideas include:

- Adding date-based bookings (not just hours)
- User authentication and role-based access
- Migrating from CSV to a proper database (SQLite / PostgreSQL)
- A web-based or TUI front-end
