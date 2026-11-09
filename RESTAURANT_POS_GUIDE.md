# Rasa Nusantara POS - Full-Stack Restaurant & Kitchen System

A modern full-stack multi-station restaurant Point of Sale (POS) system built with **Node.js, Express, SQLite/JSON persistence**, and **Server-Sent Events (SSE)** for real-time multi-device synchronization.

---

## 🌟 Stations & Device Architecture

The application connects all restaurant operational areas over a central local server (`http://localhost:3000/`):

```
                                  ┌─────────────────────────────────┐
                                  │   Central Node.js POS Server    │
                                  │      (Port 3000 / SQLite)       │
                                  └───────────────┬─────────────────┘
                                                  │
            ┌──────────────────────┬──────────────┴───────────────┬──────────────────────┐
            ▼                      ▼                              ▼                      ▼
  📱 Waitstaff Mobile     🖥️ Kitchen (KDS)               🛒 Cashier Station     📊 Sales Recap & Z-Report
   • Tableside ordering    • Live ticket queue            • Bill settlements     • Shift cash drawer audit
   • Instant kitchen push  • "Cooking / Ready" buttons    • Dynamic QRIS engine  • Variance (Over/Short)
   • Stock-checked items   • Elapsed timer ticker         • 80mm Thermal Receipt • Hourly sales chart
```

---

## 🚀 Key Features

### 1. Cashier POS Station (`/`)
* **Menu Catalog & Pricing**: Categorized dishes (*Main Courses, Appetizers & Sides, Beverages, Desserts*) with authentic Indonesian dishes in IDR (`Rp XX.XXX`).
* **Service Flows**:
  * **Pay Later (Dine-In)**: Send orders to the kitchen first; the table stays seated while guests dine, and the bill is settled at the cashier counter when leaving.
  * **Pay Now (Take Away / Counter Order)**: Immediate upfront checkout with receipt printing.
* **Live Portion Stock Badges**: Real-time indicators (*Healthy Stock*, *Low Stock $\le 5$*, *Sold Out*). Prevents over-ordering.
* **Discounts & Taxes**: Happy Hour 10%, VIP 15%, Weekend 20%, PB1 Restaurant Tax 10% toggle, Service Charge 5% toggle.
* **Supervisor PIN**: PIN protection (`8888`) required for transaction voiding and cash drawer audits.

### 2. Waitstaff Mobile Station (`📱 Waitstaff Mobile`)
* Mobile-responsive interface designed for servers walking between tables.
* **Table Selector (Table 01 - 20)**: Real-time visual status (*Open* vs *Seated*).
* **Tableside Order Entry**: Tap items to add, specify custom kitchen notes (*"less spicy", "gravy on side", "no onions"*), and tap **"Send Order to Kitchen KDS"**.

### 3. Kitchen Display System (`🖥️ Kitchen (KDS)`)
* Real-time ticket queue for kitchen chefs.
* **Live Urgency Timers**: Shows elapsed ticket time (e.g., `⏱️ 4m elapsed`), turning red when exceeding 15 minutes.
* **Interactive State Transitions**:
  * **[🍳 Start Cooking]**: Marks ticket in-progress.
  * **[🔔 Mark as Ready to Serve]**: Triggers acoustic bell chime to alert food runners and waitstaff.

### 4. Dynamic QRIS Payment Engine
* **National Standard UI**: Compliant national QRIS red-and-white header with **GPN** and **ASPI** standard badges.
* **Dynamic QR Generation**: Offline pure SVG generator embedding exact transaction amounts, NMID `ID10202611089901`, and unique invoice references.
* **5-Minute Countdown**: Automatic expiration countdown ticker.
* **Interactive Testing**: **[⚡ Simulate Customer Scan & Pay]** simulates instant customer scan from banking apps (*GoPay, BCA Mobile, OVO, ShopeePay, Dana*) with digital cash register chimes.
* **Alternative Payments**: Cash tender with quick presets and change calculation, plus EDC Card terminal reference recording.

### 5. 80mm Thermal Receipt Printing
* Formatted specifically for standard 80mm POS receipt printers via CSS `@media print`.
* Includes restaurant details, tax registration, invoice number, guest name, table, itemized lines, subtotal, discount, taxes, QRIS reference code, and status **PAID IN FULL**.
* Quick **"Copy Receipt Text"** button for sending digital receipts via WhatsApp or SMS.

### 6. Stock & Inventory Management (`📦 Stock & Inventory`)
* **KPI Metrics**: Total Menu Items, Safe Stock, Low Stock Warnings, Out of Stock Items, and Total Inventory Asset Valuation in `Rp`.
* **Inventory Table**: Item name, category, cost price (HPP), selling price, profit margin %, current stock.
* **Quick Restock**: Instant batch restock buttons (`+5`, `+10`), spoilage adjustments (`-1`), and exact numerical edits.
* **Add Menu Item**: Form to register new dishes directly into the database.

### 7. Sales Recap & Shift Z-Report (`📊 Sales Recap & Z-Report`)
* **Financial KPIs**: Gross Sales Revenue, Net Sales, Total Orders, Average Order Value (AOV), Total Portions Sold, and PB1 Tax Collected.
* **Payment Method Breakdown**: Visual progress bars and metrics for QRIS, Cash, and EDC Card.
* **Top 5 Best Sellers**: Ranked table with portion counts, revenue, and revenue share.
* **Hourly Peak Distribution Chart**: Pure SVG bar chart displaying sales volume across operational hours (09:00 - 21:00) highlighting lunch and dinner rush hours.
* **Shift Z-Report & Cash Drawer Audit**:
  * Opening cash float reconciliation.
  * Expected vs. actual cash counted with automatic **Variance calculation (Cash Over / Short)**.
  * Supervisor PIN verification (`8888`) and printable thermal Z-report slip.
  * **CSV Data Export** button.

---

## ⌨️ Cashier Keyboard Shortcuts

| Shortcut | Action |
|---|---|
| <kbd>/</kbd> | Instant focus to menu search |
| <kbd>F2</kbd> | Open checkout & payment modal |
| <kbd>Esc</kbd> | Close active modal |

---

## 🔗 Live Application Access
* **Central Server**: [http://localhost:3000/](http://localhost:3000/)
* **Server Script**: [server.js](file:///home/antigravity/server.js)
* **Frontend Web App**: [public/index.html](file:///home/antigravity/public/index.html)
* **Database Storage**: [database.json](file:///home/antigravity/database.json)
