# 📱 POS Device Operations Tracker

A robust, offline-first operational solution designed to streamline field inspections, multi-device tracking, and photo documentation for POS equipment with zero data loss.

---

## 🎯 Overview & Problem Statement
Field engineers and operations teams often struggle with data loss and inefficient workflows when registering multiple POS devices per site visit. Standard flat-form entries fail to efficiently handle multi-image capture and individual condition notes under unstable network environments.

To address this, I engineered a relational system that allows tracking multiple devices under a single operational session with dedicated photo captures, itemized notes, and seamless offline synchronization.

---

## 🏗 Architecture & Database Design

The system is built on a **Master-Detail (Parent-Child)** database architecture using Google Sheets as the relational backend:

* **`Operations`** *(Parent Table - Session Metadata)*
  * └── **`Devices_Photos`** *(Child Table via `Ref` + `IsPartOf`)*
    * ├── **Terminal ID** `(Text)`
    * ├── **Image Capture** `(Image)`
    * └── **Condition Notes** `(LongText)`

### Key Technical Decisions:
1. **Relational Data Modeling:**
  * Separated operational session metadata (Client Name, Date, Contact) from item-level logs. Utilized `Ref` columns with `IsPartOf` enabled to allow adding unlimited devices under one master log.
2. **Offline-Resilient Sync Strategy:** 
   * **`Delayed Sync = ON`**: Enables full offline usability, allowing field workers to log multiple devices and capture images without waiting for a server response.
   * **`Automatic Updates = ON`**: Automatically pushes cached records to Google Sheets once a network connection is detected.

---

## 📸 Key Features

* 🚀 **Multi-Device Registration:**
*  Track multiple POS devices within a single session without repeating client metadata.
* 📷 **Direct Camera Stream:**
*  Instant camera trigger per device entry for fast inspection workflow.
* 📝 **Itemized Inspection Notes:**
*  Attach unique condition notes (e.g., screen damage, missing cable) directly to each photo.
* 📶 **Offline Readiness:**
*  Full functionality in zero-connectivity environments with local device caching.

---

## 🛠 Tech Stack & Tools

* **Frontend / Application Platform:** AppSheet
* **Backend Database:**
* Google Sheets (Relational Architecture)
* **Data Pattern:**
*  Master-Detail (Parent-Child) Schema
