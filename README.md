# 🏛️ EXAM-CORE: Scalable Architecture Case Study

<div align="center">

![Header](https://capsule-render.vercel.app/render?type=soft&color=092E20&height=200&section=header&text=Scalable%20Exam%20Portal&fontSize=50&animation=fadeIn&fontAlignY=38)

[![Status](https://img.shields.io/badge/Status-Production--Ready-00FF00?style=for-the-badge&logo=statuspage&logoColor=white)]()
[![Tech](https://img.shields.io/badge/Architecture-Data--Driven-blueviolet?style=for-the-badge)]()
[![Speed](https://img.shields.io/badge/Latency-%3C100ms-orange?style=for-the-badge)]()

**A high-performance, mobile-first LMS designed to serve dynamic content for 50+ government exams with zero database overhead.**

[Explore Live Demo](#) • [View Architecture](#system-architecture) • [Key Features](#-key-implementation-details)

</div>

---

## 🛰️ Project Overview

**The Challenge:** Students preparing for high-stakes exams (**RBI, RRB, SSC**) require instant access to updates. Traditional SQL-heavy architectures often suffer from latency and "clunky" mobile experiences during high-traffic mock tests.

**The Solution:** I architected a **Dictionary-Based NoSQL Pattern** using Django. By treating Python dictionaries as a primary data layer for static datasets, I achieved sub-100ms load times and a "Zero-Latency" mock test engine.

---

## 🛠️ The Engine Room (Tech Stack)

| Backend | Frontend | Data Strategy |
| :--- | :--- | :--- |
| ![Django](https://img.shields.io/badge/Django-092E20?style=for-the-badge&logo=django&logoColor=white) | ![Tailwind](https://img.shields.io/badge/Tailwind_CSS-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white) | **In-Memory Python Dicts** |
| Robust Routing & Logic | Mobile-First UI | Ultra-Fast Read Speeds |

---

## 🏗️ System Architecture

I moved away from the traditional `Model-View-Template` (MVT) database dependency. Since exam patterns are static until an official update, fetching them from SQL was unnecessary.

### The "Data-Hydration" Workflow



```mermaid
graph TD
    User((👤 Student)) -->|Request: /exam/rbi-2026| Router[🔀 Django URL Dispatcher]
    Router -->|ID: rbi-2026| View[⚙️ Exam View Logic]
    
    subgraph "Data Layer (In-Memory)"
        SyllabusDB[(📚 Syllabus_Data.py)]
        MockDB[(📝 Mock_Test_DB.py)]
    end
    
    View -->|Fetch Metadata| SyllabusDB
    View -->|Fetch Questions| MockDB
    
    View -->|Inject Context| Template[📄 Master Template]
    Template -->|Render HTML| User
    
    style SyllabusDB fill:#092E20,stroke:#38B2AC,stroke-width:2px,color:#fff
    style MockDB fill:#092E20,stroke:#38B2AC,stroke-width:2px,color:#fff
    style View fill:#1a1a1a,stroke:#fff,color:#fff
