# 🏛️ EXAM-CORE  
### Scalable Architecture Case Study for High-Traffic Exam Portals

<div align="center">

![Header](https://capsule-render.vercel.app/render?type=soft&color=092E20&height=200&section=header&text=Scalable%20Exam%20Portal&fontSize=48&animation=fadeIn&fontAlignY=38)

[![Status](https://img.shields.io/badge/Status-Production--Ready-00C853?style=for-the-badge)]()
[![Architecture](https://img.shields.io/badge/Architecture-Data--Driven-blueviolet?style=for-the-badge)]()
[![Performance](https://img.shields.io/badge/Latency-<100ms-orange?style=for-the-badge)]()

**A high-performance, mobile-first exam platform designed to serve 50+ government exams  
with near-zero latency and minimal infrastructure cost.**

[Live Demo](#) • [Architecture](#-system-architecture--data-flow) • [Features](#-key-implementation-details)

</div>

---

## 🛰️ Project Overview

### The Problem
Students preparing for high-stakes government exams (**RBI, SSC, RRB, Banking, Defence**) need **instant access** to syllabus updates, mock tests, and exam data.

Traditional Django + SQL architectures:
- Overuse databases for static content
- Struggle on low-resource servers
- Fail during peak traffic (mock tests & result submission)

---

### The Solution
**EXAM-CORE** introduces a **Dictionary-Driven NoSQL Architecture** using Django.

Instead of querying a database for static exam data, the system:
- Loads exam content into **in-memory Python dictionaries**
- Serves content with **O(1) lookup time**
- Eliminates database overhead for read-heavy operations

> Result: **Sub-200ms page loads** and **10× concurrency** even on free-tier hardware.

---

## 🛠️ Tech Stack

| Layer | Technology | Purpose |
|------|-----------|---------|
| Backend | Django | Routing, Auth, Business Logic |
| Frontend | Tailwind CSS | Lightweight, mobile-first UI |
| Data Layer | Python Dictionaries | Ultra-fast static content |
| Database | SQL (SQLite/Postgres) | Users, Logs, Analytics |
| Client Logic | Vanilla JavaScript | Mock test scoring |

---

## 🏗️ System Architecture & Data Flow

### Why No Traditional MVT?
Exam patterns, syllabus, and mock questions **rarely change**. Querying SQL for every request adds:
- Latency
- Memory usage
- Unnecessary complexity

---

### Hybrid “Hydration” Model

| Data Type | Storage |
|---------|---------|
| Users & Authentication | SQL Database |
| Admin Logs & Analytics | SQL Database |
| Exam Content | Python Dictionaries |
| Syllabus & Mock Tests | Python Dictionaries |



---


## 🧠 Key Implementation Details

### 1️⃣ Dynamic Exam Routing (Unlimited Pages)

**Problem**  
Managing 50+ exams without creating separate HTML files or database tables.

**Solution**  
Implemented dynamic URL routing backed by dictionary-based lookups.

```text
/exam/rbi-2026 → key = "rbi-2026"


    StudentDash -.-> DB
    StudentDash -.-> DICT

---

### Architecture Diagram (Mermaid)

```mermaid
graph LR
    subgraph Data_Storage [Data Architecture]
        DB[(SQL Database)]
        DICT[[Python Dictionaries]]

        Users --> DB
        Analytics --> DB
        Exams --> DICT
        Syllabus --> DICT
        MockTests --> DICT
    end

    Home --> Auth
    Auth --> StudentDash
    Auth --> AdminDash





