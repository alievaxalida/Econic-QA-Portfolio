# 📝 Test Cases - Econic Mini App

This document contains manual test cases executed for the **Econic** Telegram Mini App. The testing process focuses on core gameplay loops (Spawn, Merge, Grow), the in-game economy, and edge cases utilizing Boundary Value Analysis.

### 📌 TC-001: First Launch & Onboarding Experience (FTUE)
**Module:** Onboarding / Launch  
**Pre-conditions:** The user is launching the Econic app for the very first time.

| Step | Action | Expected Result | Pass/Fail |
| :--- | :--- | :--- | :--- |
| 1 | Open the Econic bot in Telegram and send `/start`. | The bot welcomes the user with an introductory message and a "Play" button. | ✅ Pass |
| 2 | Click the "Play" button. | The Mini App loads smoothly without opening an external browser. | ✅ Pass |
| 3 | Verify the initial onboarding screen. | A top banner correctly displays "WELCOME! YOU RECEIVED 1000 ECTY & 5 ENERGY!". The tutorial modal ("SPAWN → MERGE → GROW") appears with a functional "NEXT STEP" button. | ✅ Pass |

---

### 📌 TC-002: Core Mechanics - Spawn & Merge Logic
**Module:** Gameplay / Grid System  
**Pre-conditions:** User has at least 1 Energy. The grid has empty tiles, one Level 1 building, and one Level 2 building.

| Step | Action | Expected Result | Pass/Fail |
| :--- | :--- | :--- | :--- |
| 1 | Tap the "Spawn" button. | 1 Energy is deducted. A new Level 1 building appears on an empty grid tile. | ✅ Pass |
| 2 | Drag and drop a Level 1 building onto another Level 1 building. | The buildings merge successfully into a single Level 2 building. Visual/audio merge feedback triggers. | ✅ Pass |
| 3 | Drag a Level 1 building onto a Level 2 building (Negative Test). | The merge fails. The building snaps back to its original position without any level change. | ✅ Pass |
| 4 | Fill the entire grid with buildings and tap "Spawn". | Action is blocked. A "Grid Full" message is displayed, and no Energy is consumed. | ✅ Pass |

---

### 📌 TC-003: Economy & Energy System Boundaries
**Module:** Economy System / Edge Cases  
**Pre-conditions:** User's Energy balance is exactly 0. 

| Step | Action | Expected Result | Pass/Fail |
| :--- | :--- | :--- | :--- |
| 1 | Attempt to tap the "Spawn" button with 0 Energy. | Action is blocked. "Insufficient Energy" notification appears. | ✅ Pass |
| 2 | Wait for exactly 5 minutes while keeping the app open. | Energy automatically refills by 1 unit. | ✅ Pass |
| 3 | Allow the Energy to refill to the maximum limit (20) and wait another 5 minutes. | Energy balance strictly remains at 20 (Boundary limit check). Does not exceed the maximum cap. | ✅ Pass |

---

### 📌 TC-004: Offline Earnings Calculation (Time-based)
**Module:** Persistence / Offline Logic  
**Pre-conditions:** User has active income-generating buildings.

| Step | Action | Expected Result | Pass/Fail |
| :--- | :--- | :--- | :--- |
| 1 | Note the current "ECTY" balance and total "ECTYPerSecond" income. | Data is accurately recorded before exiting. | ✅ Pass |
| 2 | Close the Mini App entirely (simulate offline state). | The `last_exit` timestamp is saved to the database/localStorage. | ✅ Pass |
| 3 | Wait for 10 minutes, then relaunch the app. | An "Offline Earnings" modal appears showing the correct calculation `(NicPerSecond * time elapsed)`. The exact amount is added to the total ECTY balance. | ✅ Pass |

### 📌 TC-005: Daily Bonus System (Exploit Prevention)
**Module:** Economy / Rewards
**Pre-conditions:** The user is on their first session of the day.

| Step | Action | Expected Result | Pass/Fail |
| :--- | :--- | :--- | :--- |
| 1 | Open the game. | Bonus modal appears and reward (ECTY/Energy) is added. | ✅ Pass |
| 2 | Claim the bonus. | Bonus is credited; "daily_bonus_claimed" event is tracked. | ✅ Pass |
| 3 | Refresh the page. | Bonus modal does not appear again; balance does not increase. | ✅ Pass |

### 📌 TC-006: Weather Timer Persistence
**Module:** Game Logic / Timers
**Pre-conditions:** The weather timer is active (e.g., 25:00 remaining).

| Step | Action | Expected Result | Pass/Fail |
| :--- | :--- | :--- | :--- |
| 1 | Open the game and observe the timer. | Timer correctly displays the remaining time from local storage. | ✅ Pass |
| 2 | Wait for 10 seconds. | Timer updates correctly (e.g., to 24:50). | ✅ Pass |
| 3 | Refresh the page. | Timer continues from 24:50 (or current time); it does not reset to 30:00. | ✅ Pass |

### 📌 TC-007: Offline Earnings Calculation
**Module:** Persistence / Economy
**Pre-conditions:** User is logged in and has buildings generating income.

| Step | Action | Expected Result | Pass/Fail |
| :--- | :--- | :--- | :--- |
| 1 | Exit the game. | last_exit timestamp is captured. | ✅ Pass |
| 2 | Wait for a specific duration (e.g., 5 minutes). | Income accumulates correctly based on nicPerSecond. | ✅ Pass |
| 3 | Re-enter the game. | The "Offline Earnings" modal appears showing the correct accumulated amount. | ✅ Pass |
| 4 | Claim the earnings. | Balance updates correctly; offline modal closes. | ✅ Pass |

