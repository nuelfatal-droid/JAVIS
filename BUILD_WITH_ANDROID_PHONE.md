# Build JARVIS APK using only an Android phone

1. Create/sign in to a GitHub account at https://github.com.
2. In your browser, create a new repository named `jarvis-android`. For a private repo, select Private; either visibility works for this source.
3. Upload the contents of this `JARVIS_Android` folder to the repository root (not the outer folder). Make sure `.github/workflows/android-apk.yml` is included. GitHub's web upload supports folder/file upload; if hidden files are not shown by your file picker, upload `.github/workflows/android-apk.yml` separately using Add file > Create new file and paste its contents.
4. Open the repository's Actions tab. Select `Build JARVIS Android APK`, then `Run workflow` if it has not started automatically after the first push.
5. Wait for the workflow to finish. Open the successful run and download the `JARVIS-debug-APK` artifact.
6. Extract the downloaded artifact ZIP using your phone's Files app. Tap `app-debug.apk` to install. If Android asks, allow your browser or Files app to install unknown apps, then install.

Notes:
- This creates a debug APK for testing, not a Play Store release.
- Do not put Groq, Picovoice, or other API secrets in source files or commit them to a public repository.
- Wake-word operation and AI features still need their required provider configuration and Android microphone permissions. Android may limit background microphone use; start the listening service from inside the app and keep its foreground notification visible.
- If the build fails, open the failed Actions run and share the error log (not any API keys) for troubleshooting.
