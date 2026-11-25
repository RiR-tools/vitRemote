# vitRemote — Global Cloud Remote Control, Virtual Display, Messenger & AI Voice Suite

> **Developer:** Rubaeat Islam Raja (Arup Raja)  
> **Official Support Telegram:** `@BDrubaeat22` (`https://t.me/BDrubaeat22`)  
> **Platform:** Android 8.0+ (API 26 – API 36) · Kotlin · Jetpack Compose · Material Design 3 · Firebase Cloud Firestore

---

## Overview

**vitRemote** is a modern Android application engineered by **Rubaeat Islam Raja (Arup Raja)** for secure, real-time remote device assistance, live screen sharing, background virtual app execution, device telemetry utilities, participant-scoped messaging, live audio/video calling, and voice-driven AI automation.

Every Android device enrolled in vitRemote receives a **permanent 9-digit connection code** (`XXX-XXX-XXX`) bound cleanly to its signed-in Google account via Jetpack Credential Manager and Firebase Authentication. Devices connect seamlessly across any Wi-Fi, 4G, or 5G network worldwide without needing local IP addresses or router configuration.

---

## Core Features

### 1. Permanent 9-Digit Cloud Connection
- Each device maintains a permanent 9-digit numeric identifier (`XXX-XXX-XXX`) bound to a single Google account inside `deviceBindings`.
- Reinstalling the app on the same device automatically restores the bound account's permanent 9-digit code.
- Supports one-tap Copy, Android Sharesheet sharing, custom device nicknames/aliases, saved remote device bookmarks, and instant viewer disconnection.

### 2. Live Remote Screen & Interactive Touch Control
- Uses `MediaProjection` (`ProjectionActivity` + `CaptureService`) for real-time display streaming with selectable quality presets (`360p`, `480p`, `720p`) and sequence-ordered frames.
- Powered by `RemoteService` (`AccessibilityService`) for remote taps, long-presses, directional swipes, scrolling, soft keyboard input, Enter/Backspace actions, and Android system navigation (`Back`, `Home`, `Recents`, `Notifications`, `Quick Settings`, `Power Dialog`).

### 3. Virtual Screen Mode (Isolated App Execution)
- Scans installed launchable packages on the host phone (`A:list`) and presents searchable app lists inside the remote controller.
- Lets controllers launch apps either on the host phone's **Real Screen** or inside an isolated **Virtual Screen** display (`A:vlaunch:<package>`) without disturbing what the host user sees.

### 4. Hardware Utilities, Telemetry & Notification Mirroring
- **Live Telemetry:** Real-time battery percentage, charging status, battery temperature, RAM utilization, internal storage stats, screen resolution, and active foreground app tracking.
- **Notification Inbox:** Mirrors active host notifications via `RemoteNotificationListenerService` (`N:list`).
- **Find-Phone Ring Alert:** Triggers or stops full-volume alarm alerts (`r:start` / `r:stop`) and volume boost (`X:volmax`) remotely.
- **Camera Flashlight & Brightness:** Toggles the rear camera LED (`f:on` / `f:off` / `f:toggle`) and adjusts screen brightness (`0–255`).
- **Two-Way Clipboard Sync:** Pulls target clipboard contents (`K:pull`) or pushes controller text (`k:<text>`).

### 5. In-App Messenger Chat & Live Audio/Video Calling
- Participant-scoped messaging threads (`chats/{chatId}`) with real-time delivery, zero-permission Android Photo Picker image attachments (`PickVisualMedia`), and automatic call log entries.
- Full-duplex **Audio & Video Calling** powered by `CallMediaEngine` (`AudioRecord`, `AudioTrack`, and live camera streaming) with `IncomingCallDialog` and `ActiveCallScreen`.

### 6. 6-Button AI Voice, Screen Automation & Chat System
1. **Master AI System Switch:** Enables AI modules using the user's optional Google AI Studio key (`AIza...` / `AQ...`).
2. **Virtual Screen AI Mode:** Spoken commands tailored to virtual screen workflows.
3. **Remote Screen AI Mode:** Voice commands targeting connected remote device interactions.
4. **Own Device Voice AI:** Speech recognition (`SpeechRecognizer`), accessibility UI tree reading, `GeminiAssistantClient` (`gemini-flash-latest`), `DeviceActionExecutor`, and `TextToSpeech` voice feedback.
5. **AI Chat Workspace (`AiChatScreen`):** Conversational Gemini assistant with copyable code cards.
6. **Floating AI Overlay (`AiOverlayService`):** System-wide floating assistant badge across apps.

### 7. Bilingual UI, Adaptive Themes & Encrypted Server Vault
- Switch instantly between **Bengali** and **English** and toggle **Light / Dark Material 3 Themes** from the top quick-action bar.
- Includes a built-in 6-step interactive **How-To-Use Guide**, password-locked SHA-256/AES **Server Vault (`SecureServerVault`)**, and direct **Telegram Support (`@BDrubaeat22`)**.

---

## Project Architecture

```text
app/src/main/java/com/example/
├── MainActivity.kt                      # Auth, onboarding, navigation & dialog orchestration
├── MainScreen.kt                        # Host Home dashboard, device code card, switches & AI controls
├── Prefs.kt                             # Preferences, theme/language state & 9-digit permanent code
├── DeviceInfo.kt                        # Battery, RAM, storage & display hardware telemetry
├── CaptureService.kt                    # Foreground MediaProjection display capture service
├── ProjectionActivity.kt                # System MediaProjection consent helper
├── RemoteService.kt                     # AccessibilityService gesture, text & global key engine
├── RemoteNotificationListenerService.kt # Live notification mirroring listener
├── AdminReceiver.kt                     # Optional device lock receiver
├── ai/                                  # AiOverlayService, DeviceActionExecutor, GeminiAssistantClient, VoiceAssistantController
├── call/                                # CallMediaEngine (AudioRecord/AudioTrack & camera streaming)
├── cloud/                               # CloudRelayManager foreground sync & command processor
├── data/                                # CloudModels, CloudRepository & FirestoreErrorHandler
├── security/                            # SecureServerVault (SHA-256 + AES encrypted asset loader)
└── ui/                                  # AuthScreen, OnboardingFlow, RemoteControllerScreen, ChatScreen, AiChatScreen, Theme & Localization
