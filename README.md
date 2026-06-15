# Luma Finance 💸

**Luma Finance** is an Android personal finance management app built for the South African market. The name "Luma" comes from the Zulu word for "bite" or "sting" — referencing the app's goal of helping users take a *bite* out of debt while avoiding the *sting* of unexpected expenses.

Luma Finance was designed to close the gap between independent budgeting aggregators (like Vault22) and bank-native tools (like FNB Smart Budgeting and the Nedbank Money App), while addressing realities specific to South African users — multiple bank accounts, Stokvel savings, load-shedding, and "Black Tax" / family support spending.

> 🎥 **Demo video:** [Watch on YouTube (unlisted)](PASTE_YOUTUBE_LINK_HERE)

---

## 📱 Features

| Feature | Description |
|---|---|
| **Daily Survival Gauge** | Home screen widget that calculates how much the user can safely spend today, based on remaining monthly budget and upcoming debit orders. |
| **Multi-Bank Aggregation** | Links multiple South African bank accounts (FNB, Capitec, Standard Bank, etc.) for a single, holistic view of finances. |
| **Automated Categorisation** | Sorts transactions into local categories such as Groceries, Transport, Data/Airtime, and Black Tax/Family Support. |
| **Stokvel Integration** | A manual-entry collaborative ledger for tracking contributions and payouts from communal savings schemes. |
| **Load-Shedding Offline Mode** | Caches transactions entered offline (e.g. during power outages) and syncs automatically once connectivity returns. |
| **Real-Time Notifications** | Alerts when a user reaches 80% of a category limit, and 48 hours before a scheduled debit order. |
| **Gamification (Luma Credits)** | Users earn credits for staying under budget, redeemable for premium themes and financial education content. |
| **SARS-Ready Export** | Generates a PDF expense report formatted for tax season. |
| **Multilingual Support** | Interface available in English, isiZulu, and Afrikaans. |

> ℹ️ *Note: tick/update this table to reflect which features are fully implemented vs. planned/stubbed in the current build, so your lecturer can see scope clearly.*

---

## 🏗️ Design & Architecture

Luma Finance follows the **MVVM (Model-View-ViewModel)** architecture recommended by Android Developers, structured as follows:

- **UI Layer** – Activities/Fragments and Jetpack Compose/XML layouts, following the navigation flow: `Home → Transactions → Savings → Profile` (Bottom Navigation).
- **ViewModel Layer** – Exposes UI state and handles business logic (e.g. Daily Gauge calculation, budget tracking).
- **Repository Layer** – Mediates between local storage and remote bank data.
- **Data Layer** – **Room** database for local persistence (transactions, budgets, Stokvel ledger), with **WorkManager** handling background sync for offline mode.

### Key non-functional requirements
- **POPIA Compliance** – Data encrypted at rest using AES-256; no banking credentials stored on-device.
- **Performance** – Target launch time under 2 seconds on mid-range devices (e.g. Samsung Galaxy A30).
- **Accessibility** – English, isiZulu, and Afrikaans language support.

Full research and design rationale is available in the [`/docs`](./docs) folder (see below).

---

## 📂 Repository Structure

```
LumaFinance/
├── app/                    # Kotlin source code (Android Studio project)
│   ├── src/main/java/...   # Activities, ViewModels, Repositories
│   ├── src/main/res/...    # Layouts, drawables, strings (en/zu/af)
├── docs/                   # Part 1 research & design documents
│   ├── OPSC_project_plan.docx
│   └── OPSCODING_research.docx
├── .github/workflows/      # GitHub Actions CI configuration
│   └── android-build.yml
└── README.md
```

---

## ⚙️ GitHub & GitHub Actions

This repository is connected to **GitHub Actions** for continuous integration. On every push or pull request to `main`, the workflow:

1. Checks out the repository.
2. Sets up JDK 17.
3. Runs `./gradlew assembleDebug` to confirm the project builds successfully.
4. Runs `./gradlew lint` to catch code quality issues.

This ensures the codebase stays in a buildable state throughout development, and gives a visible build history showing iterative progress on the project.

[![Android CI](../../actions/workflows/android-build.yml/badge.svg)](../../actions/workflows/android-build.yml)

---

## 📦 Built APK

A debug/release APK is available under [Releases](../../releases) (or in the `/apk` folder of this repository).

To install:
1. Download `LumaFinance.apk` from the link above.
2. Enable "Install from unknown sources" on your Android device.
3. Open the APK file to install.

---

## 📑 Research & Design Documents (Part 1)

Copies of the original Part 1 submission are included in this repository for reference:

- **Project Plan & System Design** – app concept, branding, feature specification, UI mockups, navigation flow, and project Gantt chart.
- **Competitor Research** – analysis of Vault22, FNB Smart Budgeting, and the Nedbank Money App, used to inform Luma Finance's feature set.

---

## 🛠️ Tech Stack

- **Language:** Kotlin
- **IDE:** Android Studio
- **Architecture:** MVVM
- **Local Storage:** Room
- **Background Tasks:** WorkManager
- **CI/CD:** GitHub Actions

---

## 📚 References

- Digital Humanity (2025). *Best 4 Budgeting Apps in South Africa.*
- Android Developers (2024). *App Architecture Guide: MVVM Pattern.*
- Stitch API Documentation (2024). *Financial Data Aggregation in South Africa.*
- South African Government (2013). *Protection of Personal Information Act (POPIA).*
