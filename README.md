# 🧠 Quiz Mobile Application — Multi-Category Android Quiz Game

> A feature-rich, multi-screen Android quiz game with three distinct game categories, user login, SQLite score persistence, and game-completion gating — built entirely in Java.

🎬 **Watch the Demo Video — Quiz Mobile Application:** *(add your YouTube link here)*

[![Android](https://img.shields.io/badge/Android-API_24%2B-3DDC84.svg?style=flat-square&logo=android)](https://developer.android.com/)
[![Java](https://img.shields.io/badge/Java-8-ED8B00.svg?style=flat-square&logo=openjdk)](https://www.java.com/)
[![SQLite](https://img.shields.io/badge/SQLite-3-003B57.svg?style=flat-square&logo=sqlite)](https://www.sqlite.org/)
[![Android Studio](https://img.shields.io/badge/Android_Studio-Hedgehog-3DDC84.svg?style=flat-square&logo=android-studio)](https://developer.android.com/studio)
[![Compile SDK](https://img.shields.io/badge/Compile_SDK-34-blue.svg?style=flat-square)](https://developer.android.com/about/versions/14)

---

## 🌟 Overview

The **Quiz Mobile Application** is a native Android educational quiz game featuring three unique interactive game categories — Color Recognition, Alphabet Identification, and Object Recognition. Players log in, choose a game from a central dashboard, answer multiple-choice questions, and are taken to a results screen showing their score. A completion-gating mechanism prevents the player from quitting until all three games have been finished.

This project was developed as part of coursework at **TechNet Cloud** to demonstrate multi-activity Android architecture, SQLite database integration using `SQLiteOpenHelper`, `SharedPreferences`-based state persistence, and `Intent`-driven navigation.

---

## ✨ Features

- **🚀 Animated Splash Screen**: A 3-second branded splash screen that automatically transitions to the Login screen using a `Handler.postDelayed` timer.
- **🔐 User Login**: A simple login form with username and password validation. The username is passed via `Intent` extras to the Dashboard.
- **🎮 Three Unique Quiz Games**:
  - **🎨 Game 1 — Color Quiz**: Displays a colored view and asks the player to identify the correct color name from four radio button options (Red, Green, Blue, Yellow).
  - **🔤 Game 2 — Alphabet Quiz**: Shows a letter on-screen and challenges the player to match it from four choices (A, B, C, D).
  - **🖼️ Game 3 — Object Recognition Quiz**: Shows an image (Apple, Car, House, Tree) and prompts the player to select the correct object name.
- **📊 Score Screen**: At the end of each game, the player's total score is displayed with options to return to the Dashboard or quit the app.
- **🔒 Completion Gating**: The "Quit" button only works if all three games have been completed, enforced via `SharedPreferences` flags (`GameOneCompleted`, `GameTwoCompleted`, `GameThreeCompleted`).
- **🗄️ SQLite Database**: A `DatabaseHelper` class manages a `GameScores.db` SQLite database to persist scores with columns for `username`, `game`, `score`, and `date`.
- **🌙 Light/Dark Mode Support**: Full day/night theme support using `values/` and `values-night/` resource directories.

---

## 🛠️ Tech Stack & Architecture

| Layer | Technology |
| :--- | :--- |
| **Language** | Java 8 |
| **UI Framework** | Android XML Layouts |
| **Navigation** | `Intent`-based Activity transitions |
| **Local Storage** | SQLite (`SQLiteOpenHelper` — `GameScores.db`) |
| **State Persistence** | `SharedPreferences` (game completion flags) |
| **Timing** | `Handler.postDelayed` (Splash timer) |
| **Image Assets** | Android `drawable` resources (apple, car, house, tree) |
| **Build System** | Gradle (Kotlin DSL — `.kts`) |
| **IDE** | Android Studio |

### Core Libraries
- `androidx.appcompat` — AppCompat backward compatibility
- `com.google.android.material` — Material Design components
- `androidx.activity` — Activity result contracts
- `androidx.constraintlayout` — Flexible constraint-based layouts

---

## 📁 Project Structure

```
MyApp/
│
├── app/
│   ├── src/
│   │   └── main/
│   │       ├── java/com/example/myapp/
│   │       │   ├── SplashActivity.java       # 3-second splash → navigates to Login
│   │       │   ├── LoginActivity.java        # Username/password form → Dashboard
│   │       │   ├── DashboardActivity.java    # Game selection hub (3 buttons)
│   │       │   ├── GameOneActivity.java      # Color recognition quiz (4 questions)
│   │       │   ├── GameTwoActivity.java      # Alphabet identification quiz (4 questions)
│   │       │   ├── GameThreeActivity.java    # Object recognition quiz (4 image questions)
│   │       │   ├── ScoreActivity.java        # Score display + completion-gated quit
│   │       │   └── DatabaseHelper.java       # SQLiteOpenHelper for GameScores.db
│   │       │
│   │       ├── res/
│   │       │   ├── layout/
│   │       │   │   ├── activity_splash.xml
│   │       │   │   ├── activity_login.xml
│   │       │   │   ├── activity_dashboard.xml
│   │       │   │   ├── activity_game_one.xml
│   │       │   │   ├── activity_game_two.xml
│   │       │   │   ├── activity_game_three.xml
│   │       │   │   └── activity_score.xml
│   │       │   ├── drawable/
│   │       │   │   ├── apple.png             # Game 3 asset
│   │       │   │   ├── car.png               # Game 3 asset
│   │       │   │   ├── house.png             # Game 3 asset
│   │       │   │   └── tree.png              # Game 3 asset
│   │       │   ├── mipmap-*/                 # Launcher icon at all DPI densities
│   │       │   ├── values/                   # Colors, strings, themes (Light)
│   │       │   ├── values-night/             # Dark mode overrides
│   │       │   └── xml/
│   │       │       ├── backup_rules.xml
│   │       │       └── data_extraction_rules.xml
│   │       │
│   │       └── AndroidManifest.xml           # All 7 activities declared
│   │
│   └── build.gradle.kts                      # SDK 24–34, Java 8
│
├── build.gradle.kts
├── settings.gradle.kts
├── gradle.properties
└── README.md
```

---

## 🗺️ App Flow

```
App Launch
    ↓
SplashActivity (3s delay)
    ↓
LoginActivity → enter username + password
    ↓
DashboardActivity → choose a game
    ↓
┌──────────────────────────────────────┐
│  GameOneActivity   → Color Quiz      │
│  GameTwoActivity   → Alphabet Quiz   │
│  GameThreeActivity → Object Quiz     │
└──────────────────────────────────────┘
    ↓
ScoreActivity → view score
    ├── "Go to Dashboard" → back to game selection
    └── "Quit" → only works if ALL 3 games completed
```

---

## 🗄️ Database Schema

**Database:** `GameScores.db`

| Column | Type | Description |
| :--- | :--- | :--- |
| `_id` | INTEGER (PK, AUTOINCREMENT) | Unique row identifier |
| `username` | TEXT | The logged-in player's username |
| `game` | TEXT | Name/identifier of the game played |
| `score` | INTEGER | Player's score for that game session |
| `date` | TEXT | Date/time the game was played |

---

## 🚀 Getting Started

### Prerequisites
- **Android Studio** (Hedgehog or newer)
- **Android SDK** (API Level 24+)
- A **physical Android device** or **AVD Emulator**

### Setup Instructions

**1. Clone the Repository:**
```bash
git clone https://github.com/AnasQ2003/Quiz_Mobile_Application.git
cd Quiz_Mobile_Application
```

**2. Open in Android Studio:**
- Launch Android Studio → click **"Open"** → select the `MyApp` folder.
- Wait for Gradle sync to complete.

**3. Run the App:**
- Connect an Android device (enable USB Debugging) or start an AVD.
- Press **▶ Run** or `Shift+F10`.

---

## ⚙️ Build Configuration

| Property | Value |
| :--- | :--- |
| Minimum SDK | API 24 (Android 7.0 Nougat) |
| Target SDK | API 34 (Android 14) |
| Compile SDK | 34 |
| Java Compatibility | Java 8 |
| Application ID | `com.example.myapp` |
| Version Name | 1.0 |

---

## 📄 License

© 2024 **Anas Ahmed Qureshi**. All Rights Reserved.

---

## 👨‍💻 Author

**Anas Ahmed Qureshi** — [@AnasQ2003](https://github.com/AnasQ2003)
*TechNet Cloud — Android Development Coursework*

---

<div align="center">
  <p>Built with ❤️ using <strong>Java & Android Studio</strong></p>

  **⭐ If you found this project helpful, please star the repository!**
</div>
