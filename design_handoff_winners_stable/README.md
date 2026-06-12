# Handoff: The Winner's Stable — Barn Management App

## Overview

A full-featured barn management dashboard for **The Winner's Stable** (Georgetown, TX), owned by Chris & Eileen Sikes. The app is used daily by the stable manager (Laine), stable hand (Stoney), and boarding clients to track horses, feeding schedules, daily tasks, arena bookings, and boarder info.

---

## About the Design Files

The files in this bundle are **design references built in HTML** — high-fidelity prototypes showing intended look, layout, data, and behavior. They are not production code to copy directly.

The task for the developer is to **recreate these HTML designs in the target codebase** (React, Next.js, or similar) using its established patterns, libraries, and database layer. All data currently lives in `localStorage` — the production version should persist to a real backend (Supabase, Firebase, or similar).

---

## Fidelity

**High-fidelity.** Pixel-accurate colors, typography, spacing, icons, and interactions are all finalized in the prototype. Recreate them precisely, using the design tokens listed below.

---

## Screens / Views

### 1. Dashboard

**Purpose:** At-a-glance overview for the barn manager or staff when they arrive each morning.

**Layout:** Full-height sidebar (220px wide, dark green `#1C3A2E`) + main content area. Top header bar (70px, frosted `rgba(247,242,231,.86)`). Content: greeting + 5 stat cards in a CSS grid (5 cols), then a 2-col grid (ratio 1.55:1) for arena schedule + tasks (left) and feed board + health alerts (right).

**Components:**
- **Stat cards** — white, `border-radius: 15px`, border `#E8DFCC`, padding `16px 17px`. Label in `Hanken Grotesk 600 12px #8A8170`, value in `Spectral 600 31px #23201C`, delta in `600 11.5px` colored per tone.
- **Section cards** — white, `border-radius: 16px`, border `#E8DFCC`, `box-shadow: 0 1px 2px rgba(40,30,15,.04)`.
- **Arena schedule** — list of events with a 4px color bar, time (right-aligned 62px column), title + who, arena badge (pill `#F1EADA` border `#E4D9C0`).
- **Daily tasks** — progress bar (`#EDE5D2` track, `#3C7A57` fill), task rows with checkbox (`border-radius: 7px`, green fill `#3C7A57` when done), strikethrough title when done.
- **PM Feed board** — horse rows with coat color dot, name, ration text, and a tap-to-check Done button.
- **Health alerts** — colored alert pills (overdue = `#B4502E` bg, due = `#9c7026` bg).

---

### 2. Horses

**Purpose:** Browse all horses at the stable. Click to open a full profile.

**Layout:** Responsive grid of horse cards (min 260px). Each card: coat-gradient header with horse name and photo drop zone, then details below.

**Horse profile panel (right side):**
- Left card: photo slot, name, breed/sex/age/height/stall/board/arrived in a 2-col grid, **Edit info & feeding** button.
- Right tabs: Feeding (AM/PM/supplements), Health (vaccinations + care list), Notes.
- Edit mode: inline form with inputs for all fields + AM/PM/supplements textareas. Save persists to `localStorage` key `ws-horse-edits`.

**Coat colors (gradient map):**
```
Bay       → linear-gradient(160deg,#6B3A2A,#3D1F10)
Chestnut  → linear-gradient(160deg,#8B4513,#5C2D0A)
Sorrel    → linear-gradient(160deg,#A0522D,#7A3B1E)
Palomino  → linear-gradient(160deg,#C8A448,#9A7320)
Grey      → linear-gradient(160deg,#9E9E9E,#6B6B6B)
Black     → linear-gradient(160deg,#2C2C2C,#111)
Buckskin  → linear-gradient(160deg,#C4A35A,#8B6914)
Paint     → linear-gradient(160deg,#8B6914,#4A3010)
```

**Current horse roster:**

| ID  | Name    | Coat      | Location      | Owner        |
|-----|---------|-----------|---------------|--------------|
| h1  | Georgia | Bay       | Paddock W1    | Emily        |
| h2  | Sophie  | Chestnut  | Paddock W3    | Christy      |
| h3  | Alvin   | Sorrel    | Paddock W3    | Christy      |
| h4  | Foxy    | Palomino  | Paddock W4    | Stephanie    |
| h5  | Rio     | Bay       | Paddock W6    | Laine        |
| h6  | Pretzel | Grey      | Paddock W7    | Laurel       |
| h7  | Amali   | Black     | Paddock W7    | Laurel       |
| h8  | Journey | Buckskin  | Paddock W8    | Maddie       |
| h9  | Santana | Chestnut  | Paddock W9    | Mani         |
| h10 | Malibu  | Palomino  | Paddock W10   | Bri          |
| h11 | Lena    | Bay       | Paddock W12   | Chris/Eileen |
| h12 | Whiskey | Sorrel    | Paddock W12   | Chris/Eileen |
| h13 | Jig     | Bay       | Stall 1       | Chris/Eileen |
| h14 | Diamond | Chestnut  | Stall 3       | Charlie      |
| h15 | Rohze   | Bay       | Stall 4       | Chris/Eileen |
| h16 | Tess    | Sorrel    | Stall 5       | Chris/Eileen |
| h17 | Remy    | Grey      | Stall 7       | —            |
| h18 | Ruby    | Palomino  | Stall 8       | Charlie      |

---

### 3. Boarders

**Purpose:** Manage boarding clients — contact info, horses, billing.

**Layout:** Left list of boarder cards (avatar initials with person-color, name, phone, horses). Right: selected boarder profile with photo slot, name, since date, contact info, horse list.

**Edit mode:** Clicking "Edit info" replaces contact block with inputs for Name, Phone, Email, Boarding since. Save persists to `localStorage` key `ws-boarder-edits`.

**Current boarders:**

| ID  | Name           | Phone        | Horses            |
|-----|----------------|--------------|-------------------|
| b1  | Emily          | —            | Georgia           |
| b2  | Christy        | 512-767-8019 | Sophie, Alvin     |
| b3  | Stephanie      | 512-468-3002 | Foxy              |
| b4  | Laine          | 512-567-3022 | Rio               |
| b5  | Laurel         | 214-901-8764 | Pretzel, Amali    |
| b6  | Maddie         | 971-228-9916 | Journey           |
| b7  | Mani           | 254-624-0966 | Santana           |
| b8  | Bri            | 512-796-1931 | Malibu            |
| b9  | Chris & Eileen | 512-585-4092 | Lena, Whiskey, Jig, Rohze, Tess |
| b10 | Charlie        | 512-549-0051 | Diamond, Ruby     |

---

### 4. Daily Tasks

**Purpose:** Checklist of daily barn chores, assigned to staff members.

**Layout:** List in a white card. Each row: checkbox (green when done), task title + area badge + time + assignee avatar. Edit/delete icons on hover. "Add task" button at top.

**Task edit modal:** Centered overlay (`rgba(0,0,0,.45)` backdrop). Fields: Title (text input), Area (select: Barn / Paddocks / All areas / Covered Arena / Hay room / Other), Time (text), Assignee (select: Laine / Stoney / Chris & Eileen / Other). Save + Delete buttons.

**Persistence:** `localStorage` key `ws-tasks`.

---

### 5. Arena Calendar

**Purpose:** Book and manage arena time slots across Arena, Covered Arena, Round Pen 1, and Round Pen 2.

**Layout:** Time-grid calendar (7am–7pm, 15-min increments). Columns per arena. Events are colored blocks spanning their duration. 

**Add/edit booking modal:** Fields: Title, Who, Arena (select), Type (Lesson / Open ride / Groundwork / Training / Blocked), Start time, End time, color auto-assigned by type. Drag to reposition (optional for v1). × button on each event to delete.

**Persistence:** `localStorage` key `ws-cal-events`.

**Event type colors:**
```
Lesson     → #3C7A57
Open ride  → #9c7026
Groundwork → #7A4A2B
Training   → #3C7A57
Blocked    → #B4502E
```

---

### 6. Facilities Map

**Purpose:** Visual map of all paddocks and stalls showing which are occupied.

**Layout:** Grid of paddock cells (W1–W15 + E1–E3 + Stalls 1–8 + Round Pens + Arenas). Each cell: coat-color dot if occupied, horse name, boarder name. Vacant cells show "Vacant" label.

---

### 7. Messages

**Purpose:** Simple inbox for barn manager to communicate with boarders and staff.

**Layout:** Left thread list (avatar, name, role, snippet, time, unread dot). Right: message thread with bubbles (outgoing right `#1C3A2E` bg, incoming left `#F1EADA`). Text input at bottom.

---

### 8. Staff

**Purpose:** Staff directory with contact info and role.

**Layout:** Cards with name, role, phone. Edit button opens inline form.

**Current staff:**
| Name   | Role                              | Phone        |
|--------|-----------------------------------|--------------|
| Laine  | Stable Manager                    | 512-567-3022 |
| Stoney | Stable Hand (PM) / Web Developer  | 512-736-7588 |

**Owners:** Chris & Eileen Sikes

---

## Role-Based Views

The app has three roles switchable from the sidebar:

| Role    | Access |
|---------|--------|
| Manager | All screens, full edit |
| Staff   | All screens, edit tasks/feeding/calendar |
| Boarder | Dashboard, own horses only, messages |

---

## Interactions & Behavior

- **Sidebar navigation** — active nav item highlighted `rgba(255,255,255,.12)` bg, left `3px` accent bar `#C99A4A`.
- **Mobile sidebar** — collapses off-screen at `< 768px`. Hamburger button in header opens it with overlay. Close via × button or overlay tap.
- **Checkbox tasks** — toggle done state, progress bar updates in real-time.
- **Feed board** — tap horse row to mark PM feed done (green checkmark).
- **Photo slots** — drag-and-drop image onto any horse/boarder avatar. Persists via `image-slot.js` web component using `localStorage`.
- **Edit forms** — appear inline (replace read view), Save writes to `localStorage`, Cancel restores previous state.
- **Calendar events** — click event to edit, × to delete, "Book arena" to add new.
- **Animations** — `fadeUp` keyframe (opacity 0→1, translateY 8px→0) on page transitions.

---

## State Management

All state currently lives in `localStorage`. Production should migrate each key to a backend collection:

| localStorage key     | Description                        | Suggested DB table |
|----------------------|------------------------------------|--------------------|
| `ws-horse-edits`     | Horse profile overrides (JSON obj) | `horses`           |
| `ws-boarder-edits`   | Boarder contact overrides          | `boarders`         |
| `ws-cal-events`      | Arena calendar bookings            | `arena_bookings`   |
| `ws-tasks`           | Daily task list                    | `daily_tasks`      |

---

## Design Tokens

### Colors
```
Background (warm sand)   #EBE2CF
Sidebar (dark green)     #1C3A2E
Sidebar accent           #234738
Nav highlight            rgba(255,255,255,.12)
Active nav bar           #C99A4A
Gold/amber               #C99A4A, #9c7026
Green accent             #3C7A57
Alert red                #B4502E
Card background          #FFFFFF
Card border              #E8DFCC
Light field bg           #FBF6EC, #FFFDF7
Field border             #E4D9C0
Body text                #2f2a23
Secondary text           #5a5345
Muted text               #8A8170, #9a9081
Sidebar text             #E9E2D0
Sidebar muted            #9DBCA8
```

### Typography
```
Serif headings   Spectral (Google Fonts) — weights 400, 500, 600, 700
Body / UI        Hanken Grotesk (Google Fonts) — weights 400, 500, 600, 700, 800
```

### Spacing & Radius
```
Card radius      15–16px
Button radius    9–11px
Input radius     7–9px
Badge radius     20px (pill)
Content padding  26px 28px
Section gap      18px
Card padding     16–20px
```

### Shadows
```
Card      0 1px 2px rgba(40,30,15,.04)
Button    0 4px 12px rgba(28,58,46,.25)
Modal     0 24px 60px rgba(0,0,0,.3)
```

---

## Assets

- **Fonts:** Spectral + Hanken Grotesk via Google Fonts CDN
- **Icons:** Inline SVG throughout (no icon library — all hand-coded feather-style, `stroke-width: 2`, `stroke-linecap: round`)
- **Photos:** Drag-and-drop placeholders via `image-slot.js` web component (included in bundle)
- **No external image assets** — all visuals are CSS/SVG

---

## Files in This Bundle

| File | Description |
|------|-------------|
| `The Winners Stable.dc.html` | Full application prototype — open directly in any browser |
| `image-slot.js` | Drag-and-drop photo slot web component |
| `README.md` | This document |

---

## Notes for Developer

1. **Data layer first** — set up the DB schema (horses, boarders, tasks, bookings, staff) before wiring UI. The data shapes in `horsesData()` and `boardersData()` in the prototype are the exact schema to replicate.
2. **Auth** — implement role-based auth (Manager / Staff / Boarder) gating views as described above.
3. **Real-time** — tasks and calendar would benefit from real-time sync (Supabase Realtime or similar) so staff on different devices stay in sync.
4. **Mobile** — the sidebar collapse at 768px is already designed; extend the grid layouts to stack on small screens.
5. **Feeding board** — the PM feed "done" state resets each day; implement a daily reset via a scheduled job or date-key in the DB.
