# Color Switch — 2.40

**Package:** `com.colorswitch.switch2`  
**Verdict:** ❌ Fails to launch  
**Source:** APKMirror — (uploaded directly, no link)  
**APK SHA-256:** `66873f593f7d1cdcd8250ab85cc7a3a3cd37fe80a23d14f2060e2bf7f1353688`  
**APK integrity check:** ❓ Not available (submitted before this check existed, or the engine build predates it)  
**Play Store category check:** GAME  
**Submitted by:** aaronateataco  
**Test environment:** Android Horizon build `Unknown (submitted before build/firmware logging existed)`, Switch firmware `Unknown`, Atmosphere `Unknown`  

## Analysis

Fails to launch / crashes before ever rendering a frame.

- Frame stalls logged: **0** (severe: **0**)
- Worst stall: **0ms**, average: **0ms**
- First error/crash line found: `[  0s] ELF: unresolved: _ZN8firebase11crashlytics11Crashlytics19LogExceptionAsFatalEPKcS3_NSt6__ndk16vectorINS0_5FrameENS4_9allocatorIS6_EEEE`

## Raw logs

See `launcher_log.txt`, `compat_log.txt`, `core_log.txt` in this folder.
