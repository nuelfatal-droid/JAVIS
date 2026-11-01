# JARVIS AI for Android — Version 3.0

A native Android Studio starter project continuing the JARVIS v2 prototype.

## Version 3 features

- On-device Porcupine wake-word detection (starter keyword: **Bumblebee**).
- User-started microphone foreground service with persistent Stop notification.
- Android speech recognition after wake-word activation.
- Groq-powered conversational answers and Android Text-to-Speech replies.
- Local phone commands that do not need an AI API call:
  - `Open WhatsApp`, `Open YouTube`, `Open Chrome`, `Open Maps`, `Open Settings`, `Open Phone`.
  - `Set an alarm for 6:30 AM` (opens the system alarm confirmation UI).
  - `Remind me to call the supplier` (opens Calendar's event editor; choose date/time and save).
  - `WhatsApp I will call you back` (opens WhatsApp with prefilled text; choose a recipient and tap Send yourself).
- Futuristic dark/cyan interface with example voice commands.

## Build and install

1. Install Android Studio and JDK 17.
2. Open this folder (`JARVIS_Android`) in Android Studio and allow Gradle sync.
3. Connect your Android phone with USB debugging enabled, or use Android Studio wireless debugging.
4. Press Run to build and install. This archive contains source code, not a prebuilt APK.
5. Create a Picovoice Console account at https://console.picovoice.ai/ and copy your AccessKey.
6. Create a Groq API key at https://console.groq.com/keys.
7. Enter both keys in JARVIS and save. Tap Start Wake-Word Listening and grant microphone and notification permissions.
8. Say **Bumblebee**, then speak a request.

## Custom “Hey Jarvis” wake word

The included wake word is Porcupine's built-in `BUMBLEBEE`. To use a custom phrase, create/download an Android `.ppn` model for “Hey Jarvis” in Picovoice Console, put it at `app/src/main/assets/hey-jarvis.ppn`, then replace the built-in keyword configuration in `WakeWordService.kt` with:

```kotlin
.setKeywordPaths(arrayOf("hey-jarvis.ppn"))
```

Update the notification text accordingly and rebuild. A custom model is not included because it must be generated for the user's Picovoice account/device target.

## Android restrictions and privacy

- Android requires microphone access to be explicitly granted and the microphone foreground service to be started while the app is visible. The ongoing notification remains visible while listening. The app cannot silently activate the microphone or guarantee listening after force-stop/reboot; manufacturer battery management may stop it.
- Wake-word detection runs locally. Speech recognition may use Google's/device speech provider; the spoken request is sent to Groq for AI answers.
- Phone actions are limited to launching common apps, opening the alarm UI, opening the calendar event editor, and preparing a WhatsApp message. JARVIS does not silently send messages, place calls, or change device settings.
- Groq and Picovoice keys are stored in app-private preferences for this development prototype. This is not a hardened secret vault. A production release should proxy Groq requests through an authenticated backend, add rate limits, and protect local credentials with Android Keystore.
- Never enter passwords, banking credentials, crypto seed phrases, or wallet recovery phrases into JARVIS.

## Requirements

- Android 8.0 (API 26) or newer.
- Android Studio, JDK 17, internet for Gradle sync and AI responses.
- Picovoice AccessKey and Groq API key.

## Project structure

- `app/src/main/java/com/naftal/jarvis/MainActivity.kt` — UI actions, speech recognition, local commands, Groq and TTS.
- `app/src/main/java/com/naftal/jarvis/WakeWordService.kt` — foreground wake-word service.
- `app/src/main/res/layout/activity_main.xml` — JARVIS interface.
- `app/src/main/assets/prototype-v1.html` — original web prototype reference.
