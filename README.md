---

# 🎟️ Ticket Analytics Dashboard – Power BI Report

This repository contains a fully interactive, 2-page Power BI dashboard that analyzes support tickets using advanced DAX, dynamic parameters, and ZoomCharts Drill Down Visuals. It provides performance monitoring, resolution time trends, geographic distribution, and a flexible tag-based deep dive.

## 📌 Project Overview

This report was designed to uncover insights from ticket data collected between **Jan 2024 and May 2025**. It allows users to explore key support KPIs like:

* Total Tickets
* Tickets Per Day
* Average Resolution Time (Days)

The visuals are fully interactive and optimized for **drill-down**, **dynamic metrics selection**, and **toggle-based visual switching** using bookmarks.

---

## 📊 Report Pages Breakdown

### 🟦 **Page 1 – Time & Type Analysis**

**Visuals:**

1. **ZoomCharts Timeline Series**

   * Tracks selected `[Parameter]` (Total Tickets, Tickets Per Day, Avg Resolution Days) by Month
   * Features MoM% calculation for the active parameter
   * Fully responsive to slicers and filters

2. **ZoomCharts Drill Down Bar Chart**

   * Breaks `[Parameter]` by Ticket Type → Queue → Priority
   * Use ZoomCharts smart drill-down feature for easy hierarchy navigation

3. **ZoomCharts Map Chart**

   * Displays `[Parameter]` by ticket location (Longitude/Latitude)
   * Useful for regional performance or trend identification

**Dynamic Title:**
Visual titles update based on the selected parameter using DAX measures.

---

### 🟩 **Page 2 – Resolution Time & Tag Deep Dive**

**Visuals:**

1. **ZoomCharts Combo Column + Line Chart**

   * Columns: Total Tickets by Priority
   * Line: Avg Resolution Time (Days)
   * Helps identify which priority levels are contributing most to resolution delay

2. **ZoomCharts Scatter Plot**

   * X-axis: Average Resolution Days
   * Y-axis: Ticket Count
   * Legend: Queue → Priority
   * Drill-down enabled

3. **Word Cloud**

   * Extracted from ticket subject lines
   * Helps spot trending issues/keywords

4. **Matrix Table**

   * Columns: Ticket ID, Subject, Body, Answer, Avg Resolution Days
   * Detailed view for support team case reviews

---

### 🧩 **Toggle Feature: Matrix vs Tag-Based Visuals**

Using **Power BI bookmarks**, users can switch between the **Matrix View** and **Tag-Based Visuals** showing the **Top 15** by:

* Primary Tag
* Secondary Tag
* Status Tag
* Resolution Tag
* Category Tag

Each tag chart uses a **dynamic measure + ranking filter** to return the top 15 items for Total Tickets.

---

## 📐 Key Measures

### Metrics Used:

* `[Total Tickets]`
* `[Tickets per Day]`
* `[Avg Resolution(Days)]`

### Time Intelligence:

* `YoY %`, `YoY Diff`, `MoM %`, and PY logic using `SAMEPERIODLASTYEAR`, `DATEADD`, and custom logic to prevent future-looking comparisons

```dax
-- MoM % Example
MoM% =
VAR __PrevMonth =
    CALCULATE([Selected Metric], DATEADD('DimCalendar'[Date], -1, MONTH))
RETURN
    DIVIDE([Selected Metric] - __PrevMonth, __PrevMonth)
```

### Parameter Switching:

```dax
Parameter = {
    ("", NAMEOF('Measures Table'[Total Tickets]), 0),
    ("", NAMEOF('Measures Table'[Tickets per Day]), 1),
    ("", NAMEOF('Measures Table'[Avg Resolution(Days)]), 2)
}
```

### Dynamic Titles:

```dax
Title Timeline =
"Trend of " & SELECTEDVALUE('Parameter Table'[Parameter Label]) & " Over Time"
```

### Conditional Formatting (Ref Card):

```dax
Total Ticket Ref =
"PY: " & py & " | " & py_dif & py_diff_sign & " | " & yoy & yoy_sign
```

Where `py_diff_sign` and `yoy_sign` use icons and colors to visually communicate direction (🔻🔴 or ▲🟢)

---

## 🛠️ Tools & Features Used

| Feature                    | Description                                       |
| -------------------------- | ------------------------------------------------- |
| Power BI Desktop           | Data modeling and dashboard building              |
| DAX Measures               | Used for dynamic calculations & time intelligence |
| ZoomCharts Custom Visuals  | Timeline, drill-down bar, combo, scatter, map     |
| Bookmarks + Buttons        | Toggle between Matrix and Tag Bar Charts          |
| Dynamic Parameter Switch   | Users choose KPI to view in all visuals           |
| Conditional Icons & Colors | Up/down arrows colored based on metric direction  |
| Responsive Design          | Layout optimized for clear cross-filtering        |

---

## 📎 Possible Extensions

* Add drill-through page for detailed ticket exploration
* Include resolution SLA comparison
* Incorporate sentiment analysis using ticket body

---

## 📷 Screenshots

> *Add screenshots or animated GIFs of the report pages with toggles, timeline trends, and tag charts in action.*

---

## 📁 File Structure

```
📦Ticket-Analytics-Dashboard
 ┣ 📊 Ticket_Analytics_Report.pbix
 ┣ 📁 Assets/
 ┃ ┗ 📷 Screenshots and logos
 ┣ 📄 README.md
 ┗ 📄 LICENSE
```

---

## 📩 Let's Connect

Built by **[Emmanuel Idowu](https://www.linkedin.com/in/emmanuel-idowu-analyst/)** — I specialize in building **insightful Power BI reports** that drive decision-making across organizations.

If you find this helpful or would like to collaborate on data projects, feel free to connect or reach out!

---

## 🏷️ Tags

`Power BI` `ZoomCharts` `Customer Support Analytics` `DAX` `Bookmarks` `Tag Analysis` `Parameter Driven` `Dynamic Visuals` `Interactive Dashboard` `Business Intelligence`

---
