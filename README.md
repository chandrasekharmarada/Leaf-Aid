# 🌿 Leaf Aid

**An Explainable AI-Based Web Platform for Instant Plant Leaf Disease Diagnosis**

Leaf Aid is an installable, mobile-first Progressive Web App. A grower photographs a leaf and receives an immediate diagnosis that explains its reasoning. No laboratory, specialist visit or native app installation is required.

---

## ✨ Features

- **Instant diagnosis:** capture or upload a leaf photo and get a result within seconds, with a local preview that needs no network call.
- **Explainability layer:** each result shows a confidence score, a colour-coded severity tag (low / medium / high), a ranked list of plain-language visual reasons, and a toggleable Grad-CAM-style saliency overlay.
- **Secure scan history:** every diagnosis is saved to a private, per-user record. Users can add notes and mark results helpful or not helpful.
- **Context-aware assistant:** a Gemini-powered chat grounded in the user's latest diagnosis answers follow-up questions on treatment, dosage and prevention.
- **Installable and offline-ready:** a PWA with a web manifest and a service worker for offline caching.

---

## 🏗️ Architecture

Leaf Aid follows a three-tier design:

| Tier | Technology | Responsibility |
|------|-----------|----------------|
| Presentation | HTML5, CSS3, ES6 JavaScript (framework-free PWA) | Capture, preview, diagnosis card, history |
| Service | Supabase (Auth, Postgres, Storage) | Authentication, `scans` table with Row-Level Security, photo and avatar storage |
| AI | Netlify serverless function + Google Gemini API | Diagnosis-grounded chat, with the API key kept server-side |

### Workflow

`Capture → Preview → Diagnosis → Saliency overlay → Persisted history → Grounded chat`

---

## 🧪 Current Status

The classification step is currently a **curated, rule-based engine covering four disease–crop profiles**, not a trained model. This was a deliberate scoping choice. It let the full explainable-diagnosis pipeline, the secure data layer and the conversational assistant be built and validated end to end first.

The diagnosis engine is designed as a **drop-in replacement point**. A trained CNN with Grad-CAM can be substituted without changing the UI, the database schema or the explanation layer.

---

## 🗺️ Roadmap

- [ ] Train a CNN classifier on a public leaf-image dataset such as PlantVillage
- [ ] Generate real Grad-CAM heat-maps from the trained model
- [ ] Derive severity from lesion-area estimation
- [ ] Evaluate on field-quality (phone-camera) images
- [ ] Expand disease and crop coverage

---

## 🚀 Getting Started

### Prerequisites

- A [Supabase](https://supabase.com) project (Auth, a `scans` table, and storage buckets for leaf photos and avatars)
- A [Google Gemini API](https://ai.google.dev) key
- [Netlify CLI](https://docs.netlify.com/cli/get-started/)

### Installation

```bash
git clone https://github.com/<your-username>/leaf-aid.git
cd leaf-aid
```

### Configuration

1. Add your Supabase project URL and anon key to the client configuration.
2. Set the Gemini key as a Netlify environment variable:

```bash
netlify env:set GEMINI_API_KEY your_key_here
```

### Run locally

```bash
netlify dev
```

> ⚠️ Never commit API keys or secrets. Use environment variables.

---

## 📁 Project Structure

```
leaf-aid/
├── index.html
├── dashboard.html
├── login / signup pages
├── script.js
├── dashboard.js
├── auth.js
├── manifest.json
├── service-worker.js
└── netlify/
    └── functions/
        └── chat.js
```

---

## 🛠️ Tech Stack

HTML5 · CSS3 · JavaScript (ES6) · Supabase · PostgreSQL · Netlify Functions · Google Gemini API · Service Workers

---

## 🔒 Privacy and Security

- Row-Level Security keeps every user's photos, diagnoses, notes and feedback private by construction.
- The Gemini API key stays on the server and is never exposed to the client.

---

## 📚 References

- Selvaraju et al. (2017). *Grad-CAM: Visual Explanations from Deep Networks via Gradient-Based Localization.*
- Mohanty, Hughes & Salathé (2016). *Using Deep Learning for Image-Based Plant Disease Detection.*
- Adadi & Berrada (2018). *Peeking Inside the Black-Box: A Survey on Explainable AI.*

---

## 📄 License

This project is licensed under the MIT License.
