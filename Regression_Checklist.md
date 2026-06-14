# 🔄 Regression Checklist - Econic Mini App

This checklist is executed before any new release or update to ensure that recent code changes have not broken existing, stable functionalities. It includes checks for core game loops and previously resolved defects.

### ⚙️ 1. UI & Settings (Post-Fix Validations)
| ID | Check Item / Test Scenario | Status | Notes |
| :--- | :--- | :--- | :--- |
| REG-001 | **Settings Menu Z-Index:** Tap the Settings icon (top-right). Verify the modal opens strictly on the top layer (foreground) and is not overlapped by game grid elements. | [✅ Pass] | *Verified on the latest build. The previous z-index overlap bug is fully resolved; the modal stays on top.* |
| REG-002 | **Sound & Vibration Toggles:** Verify that Sound and Vibration functions can be successfully activated and deactivated within the Settings menu. | [✅ Pass] | *Both toggles function flawlessly. The selected state is successfully saved even after closing the menu.* |

### 🎮 2. Core Gameplay Loop
| ID | Check Item / Test Scenario | Status | Notes |
| :--- | :--- | :--- | :--- |
| REG-003 | **Spawn Building:** Verify tapping "Spawn" successfully deducts 1 Energy and generates a Level 1 building. | [✅ Pass] | *1 Energy is accurately deducted from the balance. Level 1 building spawns instantly without network lag.* |
| REG-004 | **Merge Logic:** Verify two buildings of the exact same level merge successfully into the next level without visual glitches. | [✅ Pass] | *Merging identical levels works perfectly with correct visual/audio feedback. Attempting to merge different levels fails as expected.* |
| REG-005 | **Grid Constraints:** Verify that the "Spawn" function is properly disabled when the grid is 100% full. | [✅ Pass] | *Spawn functionality is properly blocked. "Grid Full" warning is displayed and no Energy is consumed.* |

### 💰 3. Economy & State Persistence
| ID | Check Item / Test Scenario | Status | Notes |
| :--- | :--- | :--- | :--- |
| REG-006 | **Energy Timer:** Verify Energy reliably refills over time while the app is active and offline. | [✅ Pass] | *Timer functions correctly in both active and background states. The maximum cap limit (20) is strictly respected.* |
| REG-007 | **Income Generation:** Verify that the total balance dynamically updates based on the current buildings on the grid. | [✅ Pass] | *Total ECTY balance dynamically increases in real-time based on the combined NicPerSecond rate of active buildings.* |
