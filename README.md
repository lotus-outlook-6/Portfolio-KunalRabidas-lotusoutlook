<div align="center">

# 🌸 Lotus Outlook

### AI-Powered Interactive Portfolio

[![Live Demo](https://img.shields.io/badge/Live_Site-GitHub_Pages-2ea44f?style=for-the-badge&logo=github)](https://lotus-outlook-6.github.io/Portfolio-KunalRabidas-lotusoutlook/)
[![Google Gemini](https://img.shields.io/badge/Google_Gemini-AI_Engine-886CE4?style=for-the-badge&logo=googlegemini&logoColor=white)](https://aistudio.google.com/)
[![Cloudflare Workers](https://img.shields.io/badge/Backend-Cloudflare_Workers-F38020?style=for-the-badge&logo=cloudflare)](https://workers.cloudflare.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)](LICENSE)

<br/>

> *A modern, fluid, intelligent personal engineering portfolio built for Kunal Rabidas*  
> *Electronics & Communication Engineering (ECE) Student @ Assam University, Silchar*

<br/>

</div>

---

## 📸 Homepage Overview

<div align="center">
  <img src="Screenshot 2026-11-24 at 2.21.26 PM.png" alt="Lotus Outlook Portfolio Homepage" width="100%" style="border-radius: 12px; box-shadow: 0 10px 30px rgba(0,0,0,0.12);" />
</div>

<br/>

### 🔍 Description of the Interface

The homepage of **Lotus Outlook** presents an elegant, calm, and distraction-free interface designed around conversational exploration:

1. **Header & Profile Identity**:
   - Clear introduction: *"Hey, I'm Kunal 👋"* alongside the central headline: *"An ECE student @Assam University Silchar"*.
   - Centered Memoji 3D avatar resting over a dynamic, silky WebGL gradient canvas.
   - Info toggle `(ⓘ)` at the top right for quick onboarding.

2. **Omnibar Natural Language Search ("Ask me anything...")**:
   - The central interaction hub where visitors can ask any question in plain English.
   - Powered by a hybrid natural-language routing engine: questions matching curated portfolio topics trigger curated rich views instantly, while novel inquiries stream live from Google Gemini AI.

3. **Core Category Quick Tabs**:
   - Five interactive pill buttons giving one-click access to Kunal's core qualifications:
     - 👤 **Me**: Personal story, tech philosophy, and animated photo simulation.
     - 💼 **Projects**: Interactive horizontal carousel featuring 6 showcased engineering projects.
     - 🥞 **Skills**: Comprehensive breakdown across ML, embedded hardware, EDA tools, and software languages.
     - 📬 **Contact**: Verified contact points, official university email, and social profiles.
     - 📄 **Resume**: Direct CV preview and one-click PDF download.

4. **Background Fluid Marble Shader**:
   - A custom WebGL shader simulating organic, liquid silk ribbons that smoothly swirl and react to user focus.

---

## 🧠 System Architecture & How Everything Works

Lotus Outlook pairs static client-side hosting with serverless edge compute for maximum performance, zero latency for common questions, and 100% credential security:

```mermaid
flowchart TD
    User([Visitor Query]) --> Input[Search Bar Input / Quick Tabs]
    Input --> Matcher{75% Similarity Matcher}

    Matcher -->|Score >= 75%| Preset[Curated Preset Route]
    Preset --> ActionType{Topic Type?}
    ActionType -->|5 Core Tabs| TabView[Render Rich Tab View]
    ActionType -->|15 Curated Answers| CuratedStream[Stream Curated Answer]

    Matcher -->|Score < 75%| AIProxy[Cloudflare Worker Proxy]
    AIProxy --> SecretKey[(Encrypted GEMINI_API_KEY)]
    SecretKey --> GeminiAPI[Google Gemini API]
    GeminiAPI --> Resilience{Status?}
    Resilience -->|200 OK| Sanitizer[Privacy Sanitizer]
    Resilience -->|503/404 Spike| ModelFallback[Model Fallback Cascade]
    ModelFallback --> Sanitizer
    Sanitizer --> StreamResponse[Typewriter Markdown Stream]
```

### 1. Hybrid 75% Similarity Matching Engine
When a visitor types a question into the search bar, the client evaluates the query against an index of curated preset topics using a dual-metric mathematical similarity algorithm:
- **Token Dice Coefficient (60% weight)**: Compares normalized, stop-word-filtered keywords between the query and known presets.
- **Character 3-Gram Dice Coefficient (40% weight)**: Accounts for typographical errors, minor spelling variations, and suffix differences.
- **$\ge 75\%$ Match**: Bypasses the AI API entirely. It immediately renders the matching curated interactive view or streams pre-written verified content. This ensures **zero API costs, zero quota consumption, and sub-10ms response times** for the most common questions.
- **$< 75\%$ Match**: Recognized as a unique, open-ended question and dynamically forwarded to the Gemini AI backend.

### 2. Zero-Leak Cloudflare Edge Proxy
Rather than exposing API credentials in public frontend JavaScript, Lotus Outlook employs a serverless edge architecture:
- The website communicates with a dedicated **Cloudflare Worker** (`portfolio-gemini.kunalrabidas2004.workers.dev`).
- The worker securely reads `GEMINI_API_KEY` from encrypted environment variables.
- CORS protection ensures requests are only processed according to security policy.
- Visitors and web scrapers inspect only clean JSON payload requests (`{ query: "..." }`) — **the Google Gemini API key is never visible in source code, network tabs, or git history**.

### 3. Model Resilience & Fallback Hierarchy
To defend against temporary high-demand spikes on AI endpoints (such as HTTP 503 errors), the backend implements an automatic fallback cascade:
1. `gemini-3.5-flash-lite` (Ultra-low latency, lightning fast response)
2. `gemini-3.5-flash`
3. `gemini-3.8-flash`
4. `gemini-flash-latest`

If any model experiences a capacity spike, the worker seamlessly retries with the next candidate without the user ever seeing an error.

### 4. Strict Privacy & Anti-Disclosure Defense
Kunal's personal contact number is guarded by a two-stage security firewall:
- **Stage 1 (System Prompt Enforcement)**: The Gemini AI system prompt contains a strict instruction forbidding the disclosure or confirmation of any phone number under any circumstance, redirecting requests to his verified academic email (`kunal.rabidas@aus.ac.in`) and LinkedIn.
- **Stage 2 (Defensive Client Sanitizer)**: A client-side regular expression filter inspects all incoming responses before they render to the DOM, automatically scrubbing any 10-digit or international telephone pattern and replacing it with safe email contact guidance.

---

## 🛠️ Technology Stack

<div align="center">

| Domain | Technologies Used |
| :--- | :--- |
| **Frontend Core** | ![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white) ![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white) ![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black) |
| **Generative AI** | ![Google Gemini](https://img.shields.io/badge/Google_Gemini-886CE4?style=flat-square&logo=googlegemini&logoColor=white) ![Gemini 3.5 Flash](https://img.shields.io/badge/Gemini_3.5_Flash-4285F4?style=flat-square&logo=googlegemini&logoColor=white) |
| **Edge Compute** | ![Cloudflare Workers](https://img.shields.io/badge/Cloudflare_Workers-F38020?style=flat-square&logo=cloudflare&logoColor=white) ![Edge Network](https://img.shields.io/badge/Edge_Network-F38020?style=flat-square&logo=cloudflare&logoColor=white) |
| **Graphics & Shaders** | ![WebGL](https://img.shields.io/badge/WebGL-990000?style=flat-square&logo=webgl&logoColor=white) ![GLSL Shaders](https://img.shields.io/badge/GLSL_Shaders-555555?style=flat-square&logo=opengl&logoColor=white) |
| **Hosting & CI/CD** | ![GitHub Pages](https://img.shields.io/badge/GitHub_Pages-222222?style=flat-square&logo=githubpages&logoColor=white) ![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=flat-square&logo=githubactions&logoColor=white) |
| **Engineering Stack** | ![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white) ![TensorFlow](https://img.shields.io/badge/TensorFlow-FF6F00?style=flat-square&logo=tensorflow&logoColor=white) ![OpenCV](https://img.shields.io/badge/OpenCV-5C3EE8?style=flat-square&logo=opencv&logoColor=white) ![ESP32](https://img.shields.io/badge/ESP32-E7352C?style=flat-square&logo=espressif&logoColor=white) ![Astro](https://img.shields.io/badge/Astro-BC52EE?style=flat-square&logo=astro&logoColor=white) ![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-06B6D4?style=flat-square&logo=tailwindcss&logoColor=white) |

</div>

---

## 🚀 Key Features

- **Adaptive Dark / Light Themes**: Automatically detects system preferences and allows instant toggling with smooth transitions, persisting user choices via `localStorage`.
- **Dynamic GitHub Pages Base Resolution**: Custom header injection automatically calculates whether the page is running under a root domain (`localhost:3000`) or a GitHub Pages subfolder (`/Portfolio-KunalRabidas-lotusoutlook/`), ensuring stylesheets, favicons, and assets load without 404s.
- **Fluid WebGL Physics Simulation**: Organic background shader mimicking flowing liquid silk with soft pastel dynamics and zero layout shifting.
- **Options Bottom Sheet (`•••`)**: A slide-up drawer containing 15 deep-dive questions about Kunal's background, including:
  - AMTRON networking & drone technology internship
  - ProteoPredict Pro protein secondary structure prediction
  - PulseML IoT biometric heart rate monitor
  - Dark Channel Prior (DCP) single-image dehazing
  - VLSI circuit design tools (Cadence Virtuoso, Silvaco TCAD, LTspice)
  - Career vision, education, and open engineering roles

---

## 💻 How to Use the Portfolio

1. **Ask Custom Questions**:
   Type anything into the search bar:
   - *"Tell me about Kunal's background in deep learning."*
   - *"What microcontrollers has Kunal worked with?"*
   - *"Can you summarize his AMTRON internship?"*
   - *"What programming languages does he write?"*
2. **Navigate Core Sections**:
   Click on any of the five pill tabs:
   - **Me**: Read his personal intro and view the animated profile shader.
   - **Projects**: Scroll through live interactive project cards with GitHub and demo links.
   - **Skills**: Explore grouped skill badges across languages, machine learning, and electronics.
   - **Contact**: Access his direct email, location, and social media handles.
   - **Resume**: Preview his resume and download the latest copy.
3. **Explore Deep-Dive Topics**:
   Click the **`•••`** button in the search bar to reveal pre-configured topics categorized into *Me*, *Professional*, *Projects*, and *Skills*.

---

<div align="center">
  <sub>Powered by <b>Google Gemini AI</b> • Secured by <b>Cloudflare Workers</b> • Hosted on <b>GitHub Pages</b></sub>
</div>
