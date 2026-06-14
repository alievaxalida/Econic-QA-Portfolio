# 🐛 Bug Reports - Econic Mini App

This document contains sample bug reports identified during the manual testing phase of the **Econic** Telegram Mini App. Defects are documented with precise reproduction steps, expected outcomes, and severity levels to assist the development team in debugging.

---

### 🚨 BUG-001: Weather cycle timer resets to 30 minutes upon app refresh/exit

**Status:** Open  
**Reporter:** Khalida Aliyeva  
**Environment:** Telegram Mobile (iOS)  
**Severity:** Major  
**Priority:** High  
**Module:** Gameplay / Persistence Logic  

#### 📝 Description:
The game features a 30-minute weather cycle timer. When the timer reaches 00:00, the in-game weather is supposed to change dynamically. However, if the user refreshes the page or exits the Mini App before the timer finishes, the countdown does not save its current state. Upon relaunching, the timer completely resets back to 30:00. As a result, the weather permanently remains "Sunny" for users who play in short sessions.

#### 👣 Steps to Reproduce:
1. Launch the **Econic** Telegram Mini App.
2. Observe the weather timer on the screen (e.g., currently showing `30:00`).
3. Wait for a few minutes until the timer decreases (e.g., let it reach `25:30`).
4. Close the Mini App entirely or trigger a page refresh.
5. Relaunch the application.
6. Observe the weather timer again.

#### ✅ Expected Result:
The timer should persist and calculate the elapsed time in the background. Upon relaunch, it should subtract the offline time and resume correctly (e.g., if 2 minutes passed while offline, the timer should show `23:30`). The weather should change when the background time completes.

#### ❌ Actual Result:
The state is not saved in the database or local storage. The timer instantly resets back to `30:00`, and the weather remains stuck on "Sunny" indefinitely. 

#### 📎 Attachments / Evidence:

https://github.com/user-attachments/assets/4eeed688-2eb4-49d4-8941-74061bcb7f41

<br><br>

---

<br>

### 🚨 BUG-002: Settings modal renders behind main dashboard UI (Z-index issue)

**Status:** Closed / Resolved  
**Reporter:** Khalida Aliyeva  
**Environment:** Telegram Web App / Mobile (iOS/Android)  
**Severity:** Major (Blocks UI interaction)  
**Priority:** High  
**Module:** UI / Settings  

#### 📝 Description:
When a user taps the Settings (gear) icon in the top right corner, the settings dropdown menu opens. However, the modal's z-index is lower than the main dashboard elements (such as the total ECTY balance and energy bar). Consequently, the settings menu gets visually overlapped by these elements, making the Sound and Vibration toggles completely unclickable for the user.

#### 👣 Steps to Reproduce:
1. Launch the **Econic** Telegram Mini App.
2. Ensure the main dashboard is fully loaded.
3. Tap the Settings (gear) icon located at the top right of the screen.
4. Attempt to interact with the settings toggles.

#### ✅ Expected Result:
The Settings modal should appear on the absolute foreground (highest z-index layer), dimming or overlaying all other background elements, allowing seamless interaction.

#### ❌ Actual Result:
The settings modal falls behind the sticky header (balance, energy, weather UI). The toggles are obscured and unclickable.

#### 🛠️ Resolution Notes:
*Status updated to CLOSED. The z-index of the settings modal component was increased in the CSS structure. Post-fix regression testing confirms the modal now stays consistently on top across all device sizes.*

#### 📎 Attachments / Evidence:
*Screenshot attached: <img width="828" height="1792" alt="photo_2026-06-14_17-33-12" src="https://github.com/user-attachments/assets/2c3ad3e2-6314-44db-994d-8bd09c5e257c" />
 *

