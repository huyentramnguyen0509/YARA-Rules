# LockBit 3.0 Ransomware Detection Rules (YARA)

## Overview
This repository contains a collection of custom **YARA rules** developed during a comprehensive reverse engineering research project on **LockBit 3.0 (LockBit Black)**.

These rules are designed to identify specific **Evasion Techniques** and **Anti-Analysis** mechanisms used by the ransomware to bypass security controls and hinder debugging efforts.

## Research Context
* **Target:** LockBit 3.0 (Windows PE Variant)
* **Sample Hash (SHA-256):** `e6ad076db5e1fbbe14d35992f5282676c56e5bda6568d63fab937cf2e7a29dd2`
* **Focus:** Advanced Static Analysis & Anti-Reverse Engineering techniques.

## Rule Coverage
The ruleset (`lockbit3_detection.yar`) specifically targets the following behaviors:

1.  **Anti-Debugging Checks:**
    * Detection of API calls like `IsDebuggerPresent`, `CheckRemoteDebuggerPresent`.
    * PEB (Process Environment Block) manipulation.
2.  **Timing Attacks:**
    * Identification of `RDTSC` (Time Stamp Counter) and `QueryPerformanceCounter` usage to detect virtualization latency.
3.  **Exception Handling Traps:**
    * Detection of custom SEH (Structured Exception Handling) manipulation used to confuse debuggers (e.g., `SetUnhandledExceptionFilter`).
4.  **Thread & Process Hiding:**
    * Techniques involving `SetInformationThread` and `NtQueryInformationProcess`.
5.  **LockBit Specific Patterns:**
    * Signature opcodes found in the unpacking loader.

## Usage
To test these rules against a suspect file, use the standard YARA command line tool:

```bash
yara -r lockbit3_detection.yar /path/to/suspicious/files
