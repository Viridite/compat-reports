# TempleRun — 1.10.0

**Package:** `com.imangi.templerun`  
**Verdict:** ❌ Fails to launch  
**Source:** APKPure — (uploaded directly, no link)  
**APK SHA-256:** `d23d69a29f30a35fa9c23a1a0a267e5da2f6aa5de748cf7540e61a3c0ac87ea1`  
**APK integrity check:** ❓ Not available (submitted before this check existed, or the engine build predates it)  
**Play Store category check:** GAME  
**Submitted by:** aaronateataco  
**Test environment:** Android Horizon build `Unknown (submitted before build/firmware logging existed)`, Switch firmware `Unknown`, Atmosphere `Unknown`  

## Analysis

Fails to launch / crashes before ever rendering a frame.

- Frame stalls logged: **0** (severe: **0**)
- Worst stall: **0ms**, average: **0ms**
- First error/crash line found: `[  1s] ELF: 69 total unresolved symbols across all libs`

## Submitter notes

Straight-up crashes and goes to an Atmosphère error screen on installation and does the same when launching the broken installation.

## Raw logs

See `launcher_log.txt`, `compat_log.txt`, `core_log.txt` in this folder.
