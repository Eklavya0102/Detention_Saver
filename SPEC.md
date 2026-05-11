# Detention Saver - Specification Document

## Project Overview
- **Project Name:** Detention Saver
- **Type:** Web Dashboard (Next.js/React)
- **Core Functionality:** Attendance tracker that calculates safe skip limits for students based on timetable and attendance requirements
- **Target Users:** College/University students

## Subject Mapping

| Code | Subject Name |
|------|--------------|
| A | Advanced Calculus and Complex Analysis |
| B | Philosophy of Engineering |
| C | Electronic System and PCB Design |
| D | Communicative English |
| E | Chemistry |
| F | Programming for Problem Solving |
| G | Biology |
| Workshop | Basic Civil and Mechanical Workshop |
| CDC | General Aptitude |
| NSS | National Service Scheme |

## Timetable Grid (Weekly)

### Monday
| Period | Subject |
|--------|---------|
| 1 | A |
| 2 | F |
| 3 | C |
| 4 | E |
| 6 | C |
| 8 | F |

### Tuesday
| Period | Subject |
|--------|---------|
| 1 | B |
| 2 | A |
| 3 | E |
| 4 | F |
| 6 | E |
| 9 | CDC |

### Wednesday
| Period | Subject |
|--------|---------|
| 1 | F |
| 2 | E |
| 3 | D |
| 7 | G |
| 8 | NSS |

### Thursday
| Period | Subject |
|--------|---------|
| 1 | C |
| 2 | D |
| 3 | B |
| 4 | A |
| 6-9 | Workshop |

### Friday
| Period | Subject |
|--------|---------|
| 1 | D |
| 2 | B |
| 3 | A |
| 4 | E |
| 6 | CDC |
| 7 | G |

### Saturday & Sunday
- No classes

## Class Count Per Subject Per Week

| Subject | Classes/Week |
|---------|-------------|
| A | 4 (Mon:1, Tue:2, Thu:4, Fri:3) |
| B | 3 (Tue:1, Thu:3, Fri:2) |
| C | 3 (Mon:3, Mon:6, Thu:1) |
| D | 4 (Wed:3, Thu:2, Fri:1) |
| E | 5 (Mon:4, Tue:3, Tue:6, Fri:4) |
| F | 4 (Mon:2, Mon:8, Tue:4, Wed:1) |
| G | 3 (Wed:7, Fri:7) |
| Workshop | 4 (Thu:6,7,8,9) |
| CDC | 2 (Tue:9, Fri:6) |
| NSS | 1 (Wed:8) |

## UI/UX Specification

### Layout Structure
- **Container:** Centered dashboard, max-width 1000px
- **Header:** Title "Detention Saver" with icon
- **Input Section:** Three inputs in a row (subject, attendance %, date)
- **Main Display:** Large "Safe to Bunk" counter as hero element
- **Stats Grid:** 4-column grid showing key metrics
- **What-If Simulator:** Toggle switch with preview

### Visual Design

#### Color Palette
- **Background:** #0f0f1a (deep navy-black)
- **Card Background:** #1a1a2e (dark purple-navy)
- **Primary Accent:** #00d4aa (cyan-teal)
- **Secondary Accent:** #7c3aed (violet)
- **Warning Red:** #ef4444
- **Warning Yellow:** #f59e0b
- **Success Green:** #10b981
- **Text Primary:** #f8fafc
- **Text Secondary:** #94a3b8
- **Border:** #2d2d44

#### Typography
- **Font Family:** "Outfit" (Google Fonts) - modern geometric sans
- **Title:** 2.5rem, bold, gradient text
- **Counter:** 6rem, bold, monospace feel
- **Labels:** 0.875rem, uppercase, letter-spacing
- **Body:** 1rem

#### Spacing
- **Card Padding:** 24px
- **Section Gap:** 24px
- **Input Gap:** 16px

### Components

#### Subject Selector
- Dropdown with all subjects
- Shows code + full name
- Default: Select a subject

#### Attendance Input
- Number input, 0-100 range
- Slider alternative
- Shows percentage symbol

#### Date Picker
- Native date input
- Defaults to today
- Highlights selected date

#### Safe to Bunk Counter (Hero)
- Large circular or rectangular display
- Number in center, "Safe to Bunk" label below
- Green background if positive
- Red pulsing background if negative (<0)
- Animated number transitions

#### Stats Cards (4 cards)
1. Classes Remaining This Semester
2. Must Attend (to reach 75%)
3. Need for 90%
4. Current Status indicator

#### Warning Indicators
- Red badge: Below 75% threshold
- Yellow badge: 90% unreachable
- Green badge: Above 90%

#### What-If Simulator
- Toggle switch "What-if Mode"
- When ON: "Skip tomorrow's class" checkbox
- Instant update of all metrics
- Shows projected attendance

### Animations
- Counter number animation on change
- Smooth color transitions
- Card hover effects
- Warning pulse animation when negative

## Functionality Specification

### Core Algorithm

```
Input: subject, currentAttendance%, todayDate

1. Get subject's classes per week (from timetable)
2. Calculate semester start (assume 1st week of semester)
3. Calculate total weeks elapsed until today
4. Calculate total classes held so far
5. Calculate classes attended = (currentAttendance/100) * classesHeld
6. Calculate classes remaining in semester (from today until end)
7. For 75% threshold:
   - requiredAttended = 0.75 * totalClassesInSemester
   - neededToAttend = requiredAttended - classesAttended
   - safeToBunk = classesRemaining - neededToAttend
8. For 90% target:
   - targetAttended = 0.90 * totalClassesInSemester
   - neededFor90 = targetAttended - classesAttended

Output: safeToBunk, classesRemaining, neededToAttend75, neededFor90
```

### Semester Assumptions
- Semester duration: 15 weeks (approximate)
- Semester start: First day of current month (simplified)
- Or configurable semester start date

### Edge Cases
- If attendance already below 75%: Show negative safe to bunk with warning
- If no subject selected: Show placeholder
- If date in future: Show error
- If 90% is mathematically impossible: Show yellow warning

## Acceptance Criteria

1. ✅ Subject dropdown shows all 10 subjects with full names
2. ✅ Timetable is stored as structured JSON
3. ✅ Class counts are calculated dynamically from timetable
4. ✅ Safe to Bunk counter updates in real-time
5. ✅ Red warning appears when safe to bunk is negative
6. ✅ Yellow warning appears when 90% is unreachable
7. ✅ What-if simulator shows projected attendance
8. ✅ All stats update instantly on any input change
9. ✅ Responsive design works on mobile
10. ✅ Modern dark theme with accent colors

license : MIT
