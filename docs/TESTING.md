# eXcap Validation Record

**Target release:** 1.0.0  
**Validation date:** 2026-07-30  
**Environment:** Linux x86_64, JDK 21, Android API 37.0, Build Tools 37.0.0, NDK 28.2.13676358, CMake 3.22.1

## Planned validation gates

| Gate | Command | Status |
|---|---|---|
| Resource and source compilation | `./gradlew assembleStandardDebug` | **Passed** |
| JVM unit tests | `./gradlew testStandardDebugUnitTest` | **Passed — 230 tests, 0 failures** |
| Android lint | `./gradlew lintStandardDebug` | **Passed — 0 errors, 166 warnings** |
| APK identity and manifest inspection | Android build tools | **Passed** |
| APK SHA-256 | `sha256sum` | **Passed** |
| Manual/emulator smoke test | install, launch, VPN consent, start/stop | **Blocked by host: emulator requires 2 CPU cores; runner exposes 1** |

## APK verification record

- Package: `app.excap.network.debug`
- Version: `1.0.0-beta` (debug variant)
- Min/target SDK: 23 / 37
- Native ABIs: `arm64-v8a`, `armeabi-v7a`, `x86`, `x86_64`
- APK size: approximately 25 MB
- SHA-256: `4081c8223228d6075c8b9b2b87d6646b27c4d08ce565d6c1bcd2081690551c8e`
- Signature: Android debug key, APK Signature Scheme v2 verified

The test environment could not boot an Android emulator because the container exposes one CPU core while the available Google API images require two. CI repeats compilation, unit tests, lint, APK assembly, and checksum generation on every push and pull request; a two-core device or runner should be used for the manual VPN consent/start-stop smoke test.

## GitHub-hosted validation

GitHub Actions independently completed the full build pipeline on commit `79c735d9e041`:

- Run: <https://github.com/gptind826-dotcom/eXcap-Android/actions/runs/30546936799>
- Result: **success**
- Artifact: `eXcap-standard-debug-3`
- APK: `eXcap-79c735d9e041-debug.apk`
- APK SHA-256: `bf8f7f755b1a07dfad1227d19315fabca54b41520ad4d065ffeda50f84174939`
- Downloaded checksum verification: **matched**

GitHub retains this workflow artifact for 30 days. Future pushes produce a newly named artifact and checksum.

