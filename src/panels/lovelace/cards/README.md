# Home Assistant Todoist Priority Extension

This repository contains an enhancement to the existing \*\*Home Assistant Todoist integration\*\*, adding support for displaying \*\*task priorities\*\* in both the backend entity attributes and the frontend Todo list UI.

\### The goal of this extension is to improve task visibility and user awareness by mapping Todoist’s internal priority values to clear, human-readable labels.

\## ✨ Feature Overview

\### ✔ Added Priority Display for Todoist Tasks

Todoist represents task priority using numeric values (`1–4`).

Home Assistant previously did not expose or display this information.

This extension introduces:

\- Priority mapping from numeric → human-readable labels

&nbsp; - `1 → Low`

&nbsp; - `2 → Medium`

&nbsp; - `3 → High`

&nbsp; - `4 → Urgent`

\- Frontend rendering of the priority field in the Todo list card

\- Backend attribute `priority` added to each Todo entity

\- Safe handling of invalid, missing, or unexpected priority values

&nbsp; - Mapped to `"Unknown"` instead of causing errors

This makes Todoist tasks more informative in the Home Assistant UI.

---

\## 🧠 Design Summary

\### Backend Changes (Core Integration)

\- Added a helper function `define\_priority\_level()` to translate Todoist priorities.

\- Updated task attribute construction to include the new mapped priority label.

\- Implemented defensive checks for invalid API data.

\- Ensured compatibility with the generic Home Assistant `todo` platform.

\### Frontend Changes (Lovelace UI)

\- Updated the Todo list UI card to display the new `priority` attribute.

\- Ensured rendering logic gracefully handles missing fields.

---

\## 🧪 Testing

\### Unit Tests

Added new parametrized test coverage for:

\- Valid priority values (1–4)

\- Invalid/edge cases:

&nbsp; - `0`, `5`, negative numbers, `None`, floats, strings

&nbsp; - All map to `"Unknown"`

Tests are located in:tests/components/todoist/test_todo.py

File structure\[Modified]:

homeassistant/components/todoist/

&nbsp; \_\_init\_\_.py

&nbsp; todoist.py

&nbsp; other updated backend files

tests/components/todoist/test_todo.py

frontend/src/panels/lovelace/cards/

&nbsp; hui-todo-list-card.ts (modified for priority display)

---

# Home Assistant Todoist Summary of Tasks Extension

This repository contains an enhancement to the existing the Home Assistant frontend **Todo panel** by introducing a virtual **Summary of Tasks** view.
The Summary dashboard aggregates all todo lists into a unified visualization that displays:

- **Total number of tasks**
- **Number of pending tasks**
- **Number of completed items**

A modern dashboard-style UI with large circular KPI widgets provides an at-a-glance overview of your tasks across all lists.

### 🚀 Features

### ✔ Summary Item in Sidebar

A new static menu item named `Summary of Tasks` appears below all real todo lists.

### ✔ Dashboard View

When Summary is selected, a dashboard displays:

- Total tasks
- Needs Action tasks
- Completed tasks

The UI uses circular KPI-style widgets styled with standard Home Assistant theme variables.

### ✔ Live, Real-Time Updates

The dashboard subscribes to **all todo lists** via the Home Assistant WebSocket API.
Any changes in any list automatically update the summary view.

### ✔ Non-Intrusive Enhancement

No backend or core changes were required.
All logic is entirely frontend-based.

---
