# VideoCall – Android Application Security Research Project

Android video calling application built using the **StreamVideo SDK**, created primarily as an **Application Security learning and analysis project**.  
The goal of this project is to understand how real-time communication apps work internally, what their **attack surface looks like**, and how to **secure video, audio, and signaling flows** in production environments.

---

## 🎯 Security Research Goals

- Analyze real-time video communication flows
- Understand trust boundaries in RTC (Real-Time Communication) apps
- Study SDK-based abstractions from a security perspective
- Identify common weaknesses in video calling applications
- Learn how to design safer media and signaling layers

---

## 🔍 Attack Surface Explored

- Camera and microphone access control
- SDK token usage and lifecycle
- Client-side permission enforcement
- Signaling channel trust assumptions
- UI-triggered state changes (mute, camera on/off)
- Error handling and information disclosure
- Lifecycle misuse leading to resource leaks

---

## 🧠 Technologies Analyzed

- **StreamVideo SDK**
  - Real-time audio/video streaming
  - Client-side SDK security assumptions
- **Jetpack Compose**
  - UI-driven state transitions
  - Interaction-triggered privilege usage
- **Kotlin Coroutines**
  - Async execution and race condition analysis
- **Android Lifecycle**
  - Resource cleanup and state desynchronization risks

---

## 🛡️ Security Perspective

This project helps understand:

- Why media permissions are a critical attack vector
- How SDK misuse can lead to:
  - Unauthorized media access
  - Session hijacking
  - State desynchronization
- The importance of:
  - Server-side authorization
  - Short-lived tokens
  - Explicit permission handling
- Why UI state ≠ actual security state

---

## 🧪 Defensive Takeaways

- Do not trust client-side mute/camera flags
- Validate session state server-side
- Properly scope SDK tokens
- Handle lifecycle events defensively
- Minimize information leakage in error messages

---

## 📱 Functionality (for Analysis)

- Video calling
- Camera on/off control
- Microphone mute/unmute
- Compose-based UI
- Graceful error handling

---

## 📸 Demo

![VideoCall Demo](https://github.com/nikolaivetrik24062010/VideoCall/assets/98304653/a9d16702-0cd0-4026-ab3e-d1c4bc4157a5)

---

## 👤 Author

**Nikolay Vetrik**  
Application Security / Mobile Security Engineer

---

## ⚠️ Disclaimer

This project is intended **strictly for educational, defensive application security research and hiring evaluation purposes**.  
No malicious use is encouraged or supported.
