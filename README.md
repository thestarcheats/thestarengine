
<img width="545" height="110" alt="Screenshot 2026-02-17 214328" src="https://github.com/user-attachments/assets/d3ad6485-86f8-41f2-836b-468e1aed6a6a" />

# THESTAR.ENGINE

**TSE** — A next-gen memory editing toolkit built because Cheat Engine 7.5/7.6 was getting on my nerves. This is the private beta (v1.0.4), closed source, and honestly? It's just better.

---

## what it actually does

- **Memory Scanner** — First scan, next scan, exact value, changed/unchanged, value between... the usual stuff but faster and less jank
- **Address Table** — Bookmark your findings, freeze values (locks them every frame), edit on the fly
- **Hex Viewer** — Raw memory inspection with ASCII side panel, navigate by address
- **Memory Map** — Visual breakdown of process memory regions with protection flags
- **Pointer Scanner** — Find multi-level pointer chains automatically (depth up to 4)
- **PRS (Process Hacker vibes)** — Full process browser with threads, modules, handles, memory regions, CPU usage, and the ability to suspend/resume/terminate processes
- **DLL Injector** — LoadLibrary injection with x86/x64 architecture detection (won't let you shoot yourself in the foot with mismatched DLLs)

---

## tech stack

| Thing | What |
|-------|------|
| Language | C++17 |
| UI | Dear ImGui (shoutout Omar Cornut) |
| Platform | Windows (Win32 API, TLHelp32, PSAPI, NTDLL hacks) |
| Injection | Classic remote thread + LoadLibrary (with WoW64 awareness) |

---

## why this exists

Cheat Engine is powerful but:
- The UI feels like it's from 2005 (because it is)
- Random crashes when scanning certain processes
- Pointer scanning is slow af
- The process list doesn't show enough useful info

TSE fixes all that and adds PRS so you don't need Process Hacker open in the background anymore.

---

## usage (if you somehow got this)

1. Run as Administrator (required for most operations)
2. Click "Open Process" and attach to your target
3. Use the Memory Scanner tab to find values
4. Double-click results to add to Address Table
5. Freeze values or edit them live
6. Use PRS tab if you need to inspect threads/modules or suspend processes
7. Injector tab for DLL injection (auto-detects architecture mismatches)

**Hotkey:** `INSERT` to toggle the UI (if running as DLL)

---

## architecture detection (the boring but important part)

The injector specifically handles WoW64 (32-bit processes on 64-bit Windows) by:
- Loading `SysWOW64\kernel32.dll` as a data file to get correct export offsets
- Finding the actual base address of kernel32 in the target process
- Calculating the real `LoadLibraryW` address for the target's architecture

This prevents the classic "64-bit DLL into 32-bit process" crash that most injectors don't bother checking for.

---

## credits

- **Omar Cornut** — Dear ImGui (the UI framework that makes this not look like garbage)
- **thestarcheats** — Everything else (scanner engine, PRS, injector, hex viewer, pointer chain logic, styling, suffering)

---

## legal blah blah

This tool is for educational purposes and legitimate game modding/reverse engineering only. Don't use it to cheat in multiplayer games or whatever. Not responsible if you get banned, arrested, or haunted by the ghost of Dennis Ritchie.

---

*Built with the power of STAR* 

**Current build:** 1.0.4 PRIV BETA
