# Homies

An Android app that helps roommates coordinate and manage everything related to living together. Create homes, track reminders, and manage roommate info — all in one place.

**Demo:** https://www.youtube.com/watch?v=JN6Vcm-0h_s&ab_channel=Andrew

---

## Tech Stack

- **Language:** Kotlin
- **Platform:** Android (minSdk 21, targetSdk 33)
- **Architecture:** MVVM (ViewModel + LiveData + Repository)
- **Database:** Room (SQLite)
- **Navigation:** AndroidX Navigation with Safe Args
- **UI:** Material Design (CardView, ChipGroup, RecyclerView)
- **Testing:** Espresso (UI), JUnit (unit)
- **Build:** Gradle

---

## Features

- **Multiple homes** — create separate entries for a dorm, apartment, or any living space
- **Roommate tracking** — list roommates displayed as Material Design chips
- **Reminders** — attach notes and reminders to each home
- **Favorites** — mark homes as favorites and filter the list
- **Swipe to delete** — remove homes with a swipe gesture
- **Persistent storage** — all data saved locally via Room database

---

## Project Structure

```
Code/app/src/main/java/edu/bu/homies/
├── HomiesApplication.kt          # App init, database setup, demo data seeding
├── activities/
│   ├── MainActivity.kt           # Main container activity
│   └── AddHome.kt                # Create new home screen
├── fragments/
│   ├── HomeListRecycleViewFragment.kt  # Home list with filter + swipe-to-delete
│   ├── DetailFragment.kt         # View home details
│   └── EditFragment.kt           # Edit home info
├── viewmodel/
│   ├── HomeListViewModel.kt      # List state and CRUD operations
│   └── CurHomeViewModel.kt       # Currently selected home state
├── adapter/
│   └── MyHomeListRecyclerViewAdapter.kt
└── data/
    ├── Home.kt                   # Room entity
    ├── HomeDao.kt                # Database queries
    ├── HomiesDatabase.kt         # Room database instance
    ├── HomiesRepository.kt       # Data layer abstraction
    └── Converters.kt             # Type converters (Array<String>)
```

---

## Getting Started

### Prerequisites
- Android Studio (Hedgehog or later recommended)
- Android device or emulator running API 21+

### Run the App

1. Open the `Code/` directory in Android Studio
2. Let Gradle sync complete
3. Click **Run** or use:

```bash
./gradlew installDebug
```

### Run Tests

```bash
./gradlew connectedAndroidTest   # Espresso UI tests
./gradlew test                   # Unit tests
```

---

## Data Model

Each **Home** stores:

| Field | Type | Description |
|-------|------|-------------|
| `id` | Int | Auto-generated primary key |
| `title` | String | Home name |
| `description` | String | Home description |
| `links` | Array\<String\> | Home type tags (Home, Dorm, Apartment) |
| `keywords` | Array\<String\> | Roommate names |
| `reminders` | Array\<String\> | Reminders / tasks |
| `isFavorite` | Boolean | Favorite flag |

---

## Architecture

The app follows **MVVM** with a clean separation of concerns:

- **Fragments** handle UI and user interaction only
- **ViewModels** hold and manage UI state, survive configuration changes
- **Repository** abstracts all database access from ViewModels
- **Room DAO** handles all SQL queries
- **LiveData** keeps the UI reactive to data changes automatically
