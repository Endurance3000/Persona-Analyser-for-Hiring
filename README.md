# 🎯 Persona Analyser for Hiring

A C++ console application that evaluates candidate personality traits using the **Big Five (OCEAN) model** and generates structured psychometric reports to support data-driven hiring decisions.

Originally designed with a defense/recruitment use case in mind (see the "Character Assessment Report" format), the system is fully generic and can be adapted for HR screening, academic assessment, or any structured personality-based evaluation workflow.

---

## 📖 Overview

**Persona Analyser for Hiring (PAH)** is a dual-role console system built around two panels:

- **Admin Panel** — create, view, sort, and delete assessment questions; calculate and review candidate scores; visualize trait profiles as bar graphs.
- **Candidate Panel** — take a timed personality assessment by ranking answer options, with responses automatically scored against the Big Five traits.

All data is persisted to disk using flat text files, making the system lightweight, portable, and dependency-free (aside from the Windows graphics stack used for visualization).

---

## ✨ Key Features

- 🧠 **Big Five Personality Scoring** — Neuroticism, Openness, Extraversion, Agreeableness, and Conscientiousness, each scored out of 20 and banded as `LOW`, `MODERATE`, or `HIGH`.
- 🔐 **Secure Admin Access** — password-protected login with XOR-based obfuscation, attempt limiting, and a timed lockout after repeated failures.
- 📝 **Dynamic Question Bank** — add, view, sort, and delete assessment questions, each auto-assigned a trait-based ID (e.g. `2.5`).
- ⏱️ **Timed Candidate Assessment** — each question is answered by ranking four options (`A`–`D`) in priority order, converted into weighted points (4/3/2/1).
- 📊 **Automated Report Generation** — produces a formatted trait-by-trait breakdown, overall score, and identification of each candidate's strongest and weakest traits.
- 📈 **Bar Graph Visualization** — renders a candidate's trait profile graphically for quick visual comparison.
- 🗂️ **Persistent File-Based Storage** — candidate registry, individual response files, and consolidated score reports are all stored as human-readable `.txt` files.
- 🖥️ **Cross-Platform-Aware Design** — Windows-specific input handling (`conio.h`, `windows.h`) with POSIX fallbacks for non-Windows terminals.

---

## 🧩 How It Works

1. **Admin** defines a bank of personality-assessment questions, each mapped to one of the five traits and scored via priority ranking.
2. **Candidate** completes the assessment; each answer is timed and converted into trait points based on ranking priority.
3. Responses are saved to a dedicated candidate file and registered in a central registry.
4. **Admin** triggers score calculation, which parses every registered candidate's responses and generates a full character assessment report — including trait bands, interpretations, and a strongest/weakest trait summary.
5. Reports can be viewed on-screen, saved to file, and optionally visualized as a bar graph.

---

## 🗂️ Project Structure

```
Persona-Analyser-for-Hiring/
├── main.cpp                     # Application entry point, admin panel logic, report generation
├── candidate.h / candidate.cpp  # Candidate assessment class and logic
├── shared.h                     # Shared utilities, Question struct, User base class
├── drawBarGraph.h                # Bar graph visualization for trait scores
├── questions.txt                 # Persisted question bank
├── candidate_registry.txt        # Index of all registered candidates
├── candidate_scores.txt          # Consolidated candidate score reports
├── candidate_counter.txt         # Auto-incrementing candidate ID tracker
├── Documentation/                 # Supporting project documentation
├── PAH_Final_Defense.pdf          # Project defense/presentation document
└── PAH.exe                        # Prebuilt Windows executable
```

---

## 🛠️ Tech Stack

- **Language:** C++ (Standard Library — STL containers, streams, `<chrono>`, `<random>`)
- **Design Principles:** Object-Oriented Programming — inheritance, runtime polymorphism, operator/function overloading, static members, encapsulation
- **Graphics:** Windows graphics API (via `drawBarGraph.h`) for trait visualization
- **Storage:** Flat-file persistence (no external database required)
- **Platform:** Windows (primary), with partial POSIX compatibility for terminal I/O

---

## 🚀 Getting Started

### Prerequisites

- A C++ compiler supporting C++11 or later (e.g. **MinGW-w64 / g++**)
- Windows OS recommended (for full graphics and password-masking support)

### Build from Source

```bash
g++ main.cpp candidate.cpp -o PAH.exe -lgdi32
```

> The included `libgcc_s_dw2-1.dll`, `libstdc++-6.dll`, and `libwinpthread-1.dll` are MinGW runtime dependencies required to run the compiled executable on machines without MinGW installed.

### Run

```bash
./PAH.exe
```

On launch, choose between:

```
[1] ADMIN PANEL      → Manage questions, candidates & results
[2] CANDIDATE PANEL  → Take the personality assessment
[3] EXIT
```

**Default Admin Password:** `admin123`
> ⚠️ Change this credential in `main.cpp` before deploying in any real hiring context.

---

## 📊 Sample Report Output

```
================================================
 CHARACTER ASSESSMENT REPORT
================================================
CandidateID : C001
Name        : Sanish Thapa Shrestha
Age         : 24
Phone       : XXXXXXXXXX
------------------------------------------------
TRAIT SCORES & PROFILE
------------------------------------------------
1. Neuroticism      : 8/20  [LOW]
   -> Emotionally stable, calm under pressure, resilient in stressful situations.

2. Openness         : 14/20 [MODERATE]
   -> Adaptable when needed, balances tradition with flexibility.
...
------------------------------------------------
OVERALL SCORE : 78/100
------------------------------------------------
TRAIT SUMMARY
  Strongest Trait : Conscientiousness (18/20)
  Weakest Trait   : Neuroticism (8/20)
================================================
```

---

## 📄 Documentation

Additional project documentation, including the formal defense/presentation deck, is available in:

- [`PAH_Final_Defense.pdf`](./PAH_Final_Defense.pdf)
- [`Documentation/`](./Documentation)

---

## 🤝 Contributing

Contributions, issues, and feature requests are welcome. Feel free to fork the repository and submit a pull request.

---

## 📜 License

This project is currently unlicensed. Consider adding an open-source license (e.g. MIT) if you intend for others to reuse this code.

---

## 👤 Author

**Endurance3000**
[GitHub Profile](https://github.com/Endurance3000)
