# What Needs To Be Done
A front-end-only web app/page

Replace real crawling and backend logic with a **static mock dataset** and client-side JavaScript. The app only needs to let a user select course codes, load mock workload data, sort/compare courses side-by-side, show course available timeslots, and highlight the highest workload.

## 1. Scope

A front-end-only prototype must:

- Run entirely in the browser.
- Use **mock course data** stored in a local JSON/JS file.
- Simulate the “crawl/aggregate” step by loading from that mock dataset.
- Perform selection, sorting, normalisation, and comparison on the client.
- Require **no backend, no database, no API, no real web crawling, no login**.
- Be deployable as a static site or runnable locally.

## 2. Data Needed

You need a mock dataset of courses. Minimum fields:

```json
{
  "courseCode": "EE1001",
  "courseSession": "C01",
  "crn": "12345",
  "courseName": "Introduction to Electrical Engineering",
  "instructor": "Dr. CHAN Tai Man",
  "term": "Semester A 2025/26",
  "expectedStudyHours": 120,
  "assessmentLoad": "High",
  "difficulty": 4,
  "gradingComponents": {
    "assignments": 30,
    "midterm": 20,
    "final": 50
  },
  "scheduledMeetingTimes": [{
    "type": "Class",
    "time": "12:00 pm - 2:50 pm",
    "days": "W",
    "where": "Li Dak Sum Yip Yio Chin A Bldg 4307",
    "scheduleType": "Second room",
    "instructors": "Dr. CHAN Tai Man"
    },
    {
    "type": "Class",
    "time": "12:00 pm - 2:50 pm",
    "days": "T",
    "where": "Yeung Kin Man Acad Building P4701",
    "scheduleType": "First room",
    "instructors": "Dr. CHAN Tai Man"
    },
  ]
  "prerequisites": [],
  "description": "Basic circuits, signals, and engineering practice."
}
```

Recommended:

- 4–6 mock courses minimum.
- A simple workload score rule, e.g. sort by `expectedStudyHours`, or a weighted score:
  `workloadScore = expectedStudyHours + difficulty*10 + assessmentLoadWeight`.
- A mapping from course code to record.

## 3. UI Components Needed

### Course Selection
- Multi-select list, checkboxes, or searchable dropdown.
- Optional: paste course codes into a textarea.
- Optional: “import timetable” mock button that fills selected codes.
- Validation for unknown course codes.

### Comparison Table
- Side-by-side columns for each selected course.
- Rows for:
  - Course code
  - Course name
  - Instructor
  - Term
  - Expected study hours
  - Assessment load
  - Difficulty
  - Grading components
  - Workload score
- Sortable by workload, difficulty, assessment load, or course code.

### Highlighting
- Clearly mark the course with the **highest expected workload**.
- Use a badge, colour, bold text, or icon.

### States
- Empty state: “Select at least two courses to compare.”
- Loading state: optional, even for mock data.
- Error state: “Course code not found.”
- Reset/clear selection.

## 4. Client-Side Logic Needed

- Load mock JSON into memory.
- Track selected course codes.
- Filter/select records by course code.
- Normalise or quantise workload indicators.
- Sort selected courses by chosen key.
- Render comparison table dynamically.
- Re-render when selection or sort order changes.
- Highlight highest workload.
- Optional: save selected courses in `localStorage`.

## 5. Minimal Tech Stack

### Simplest
- HTML
- CSS
- Vanilla JavaScript
- Static JSON file

### More structured
- React, Vue, or Svelte
- Vite for local development/build
- Tailwind, Bootstrap, or Material UI for styling
- Static JSON or JS module for mock data

### No need for
- Node/Express backend
- Database
- Authentication
- API keys
- Web crawler
- Server-side rendering

## 6. Non-Functional Requirements

- Responsive on desktop and mobile.
- Fast load, since data is local.
- Accessible: labels, keyboard navigation, readable contrast.
- Easy to swap mock data for a real API later.
- Clear separation between data layer and UI layer.

## 7. Out of Scope for Front-End-Only

- Real CityU portal crawling.
- Live course data.
- User accounts.
- Persistent reviews.
- Moderation.
- Anonymous posting.
- Critical mass of real reviews.
- Legal/ethical crawling decisions.

## 8. Acceptance Criteria

The prototype is successful when:

1. John can select or import at least two course codes.
2. The app loads mock workload data for those courses.
3. The app displays a side-by-side comparison table.
4. The table can be sorted by workload indicators.
5. The course with the highest expected workload is clearly indicated.
6. No backend or live crawling is required.
7. The app works as a static front-end site.

## 9. Minimum Deliverable

- One page.
- A mock course dataset.
- A multi-select or paste-course-codes input.
- A comparison table.
- A what-if timetable tool
- A sort dropdown.
- A “highest workload” badge.
- Static hosting or local `index.html`.
