# VideoCall – RTC Security & Media Privacy Research

A high-performance Android video calling application built with **StreamVideo SDK** and **Jetpack Compose**. This project serves as a dedicated **Application Security (AppSec) research sandbox** to analyze real-time communication (RTC) vulnerabilities and media stream protection.

---

## 🎯 Security Research Objectives

The primary goal of this project is to deconstruct the **RTC Attack Surface** and implement defensive guardrails for video, audio, and signaling flows.

* **RTC Flow Analysis:** Auditing the signaling handshake and media negotiation (WebRTC-based) for potential interception.
* **Trust Boundary Mapping:** Identifying where the SDK ends and the application's responsibility for security begins.
* **Permission Scoping:** Implementing strict lifecycle-aware access to `CAMERA` and `RECORD_AUDIO` to prevent unauthorized background access.
* **Token Lifecycle:** Analyzing JWT-based session authorization and short-lived token enforcement.



---

## 🔍 Attack Surface & Threat Modeling

During development, the following vectors were analyzed and mitigated:

- **Media Hijacking:** Studying how race conditions in Coroutines could lead to accidental camera activation.
- **Unauthorized Session Access:** Testing SDK token scope to ensure a user cannot join unintended calls (Call ID spoofing).
- **UI vs. Logic Desync:** Ensuring that "Mute" in the UI translates to an actual stream termination at the hardware/SDK level, not just a visual overlay.
- **Information Disclosure:** Hardening error handlers to prevent leaking backend infrastructure details or SDK versions via Logcat.

---

## 🛡️ Defensive Implementations & Takeaways

### 1. Media Stream Protection
- **Hardware Lifecycle Binding:** Camera and Mic streams are explicitly bound to the Android Lifecycle. Streams are forcefully terminated on `onStop()` to prevent persistent background eavesdropping.
- **Explicit Permission Guardrails:** Implemented a "Pre-flight" check system ensuring that permissions are validated not just at launch, but before every single session initiation.

### 2. SDK Hardening (StreamVideo)
- **Server-Side Trust:** Architecture assumes the client is untrusted. All session authorizations must be validated via server-side logic before the SDK initializes the call.
- **Token Management:** Implemented secure handling of SDK tokens, ensuring they are never stored in plaintext or persisted in insecure logs.

### 3. UI/UX Security (Clickjacking Defense)
- **State Transparency:** Clear, hardware-synced indicators for active recording/streaming to maintain user trust and transparency.
- **Overlay Protection:** (Planned) Implementing `filterTouchesWhenObscured` to prevent UI redressing attacks that could trick users into enabling media.

---

## 🧠 Technical Stack
- **Language:** Kotlin & Coroutines (for thread-safe signaling)
- **UI:** Jetpack Compose (Modern, declarative UI state)
- **RTC Engine:** StreamVideo SDK
- **Security Validation:** Audited via **MobSF**, **Burp Suite** (for signaling analysis), and **Frida** (to test stream-state manipulation).



---

## 🚀 Research Functionality
- **Secure RTC Signaling:** Encrypted call initiation.
- **Granular Media Control:** Real-time hardware-level mute/unmute.
- **Defensive Error States:** User-friendly alerts without technical leakage.
- **Compose-based UI:** Fully reactive and lifecycle-aware.

---

## 👤 Author
**Nikolay Vetrik** – *Senior Security Engineer & Mobile Developer* 📧 [devnikolaivetrik@gmail.com](mailto:devnikolaivetrik@gmail.com) | 🔗 [LinkedIn](https://www.linkedin.com/in/nikolayvetrik24062010/)

---

## ⚠️ Disclaimer
This project is intended **strictly for educational research, defensive security analysis, and hiring evaluation purposes**. No malicious use is supported.
