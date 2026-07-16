# Hill Climb Racing — 1.67.0

**Package:** `com.fingersoft.hillclimb`  
**Verdict:** ⚠️ Runs with issues  
**Source:** APKPure — (uploaded directly, no link)  
**APK SHA-256:** `542c25e56ac80768d4a9f74bd77ef463deb4517623df886ee0602315107b150a`  
**APK integrity check:** ❓ Not available (submitted before this check existed, or the engine build predates it)  
**Play Store category check:** GAME  
**Submitted by:** aaronateataco  
**Test environment:** Android Horizon build `0.1.124`, Switch firmware `22.1.0`, Atmosphere `1.11.2`  
**Supersedes:** submission by aaronateataco on 2026-07-10T11:07:39Z  

## Analysis

Runs, but with issues (51 severe stall(s), worst 5149ms; at least one error/crash marker logged).

- Frame stalls logged: **178** (severe: **51**)
- Worst stall: **5149ms**, average: **139.2ms**
- First error/crash line found: `[  4s] game stdio[tid=0x2f466a4a0]: failed to load external entity ""`

## Raw logs

See `launcher_log.txt`, `compat_log.txt`, `core_log.txt` in this folder.
