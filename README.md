# BITS Digital CodeForge V1.0 - Grading Console

## 🚀 Live Demo

Check out the deployed app here: [https://college-submission.web.app/](https://college-submission.web.app/)

## 🚀 Project Overview

This is a web-based Grading Console prototype made for instructors to upload Excel mark sheets, set up grade ranges, look at student performance stats, and download the final grades as a CSV file.

Starting from the initial prototype given for this assignment, I found and fixed several functional bugs. After that, I added a few extra features to make grading faster, safer, and easier to use for an instructor.

## 🚀 Stage 1: Bug Fix Log

| # | Bug / Issue Identified | How You Reproduced It | Root Cause | Fix Implemented | How You Tested the Fix |
|---|---|---|---|---|---|
| 1 | Course dropdown keeps showing duplicate/old entries after uploading a second Excel file | Uploaded one file, then uploaded another file with different courses | The file upload handler kept appending new `<option>` tags to the dropdown without clearing out the old list first | Cleared out `courseSelect.innerHTML` back to the default option before loading the new courses | Uploaded two different files back-to-back and checked that the dropdown only showed courses from the current file |
| 2 | Grade ranges reset to default every time you switch courses | Uploaded a file with 2+ courses, changed the grade ranges for the first course, then switched to the second course and back | `buildGradeUI()` (which resets the range inputs to default values) was running inside the course-change handler, so it triggered on every course switch instead of just page load | Moved `buildGradeUI()` so it only runs once when the page loads. Now switching courses only updates stats/roster without touching custom ranges | Set custom ranges for Course A, switched to Course B, went back to Course A, and confirmed the custom ranges were still saved |
| 3 | Min, Max, Average, and Median showed `NaN` or broke when a course had no valid marks | Uploaded a file and selected a course where all marks were blank/invalid | The stats calculation divided by `marks.length` and checked array positions without verifying if the array was empty first | Added an empty-data check in `computeStats()` that shows `-` for all stats when there are no valid marks | Selected a course with 0 valid records and verified the stats panel displayed `-` instead of `NaN` or throwing a JS error |
| 4 | Students with blank, text, or "AB"/"Absent" marks were completely dropped from the exported CSV | Included a row with text (like "AB") in the Total Marks column and exported the CSV | The grading logic only checked numeric ranges. If a mark didn't fit into a numeric band, it skipped the student entirely from both the counts and the CSV export | Added a `sanitizeMark()` function to tag blank/"AB"/"Absent"/non-numeric marks as `NC`, and updated `getGradeForMark()` to return `"NC"`. Now every student shows up on screen and in the CSV | Uploaded a file with a mix of valid marks and an "AB" entry, and made sure the AB row showed up in the roster and CSV as `NC` |
| 5 | Excel file picker blocked `.xlsx` files depending on the browser | Tried picking a normal `.xlsx` file from the file picker | `<input type="file" accept=".xls">` only allowed older `.xls` files, even though the project uses the `xlsx` library and accepts `.xlsx` | Changed the file input attribute to `accept=".xlsx, .xls"` | Selected a `.xlsx` sample file using the file picker and made sure it uploaded and parsed fine |
| 6 | "Reset Range" button opened two confirmation pop-ups in a row | Clicked "Reset Range" once | The click handler was calling `confirm()` twice back-to-back | Removed the extra `confirm()` call so only one pop-up shows | Clicked "Reset Default" and confirmed only a single prompt appeared |

**Note:** I wanted to mention one bug that I left unfixed instead of taking credit for it: the grading timer displays `00:00` for the first second when the page loads. This happens because `startTimer()` updates the text inside `setInterval` instead of running it immediately when starting. Since it's just a minor UI issue and doesn't affect grading calculations, I prioritized the functional bugs above. It can be easily fixed later by calling the update function once before starting the interval.

## 🚀 Stage 2: Enhancements Made

1. **Grading Policy Presets:** Added quick preset options ("Standard BITS", "Rigorous (Higher A)", and "Generous Pass") next to the manual range editor. Instructors don't have to manually type in eight ranges every time they want to try a different curve—they can compare curves instantly and tweak them manually if needed.
2. **Live Roster with Search and Filters:** Built a scrollable roster table that updates automatically as ranges change. It includes a search bar (to search by BITS ID or grade) and clickable grade-count chips to filter students, making it easy to see *who* got what grade instead of just seeing the total count.
3. **Better Handling for Missing/Invalid Marks (NC):** Set up a `sanitizeMark()` / `getGradeForMark()` pipeline that automatically detects blank, non-numeric, or "AB"/"Absent" entries and marks them as `NC` across the whole app (and in the CSV). This keeps students from accidentally disappearing from the grade sheet.
4. **Detailed CSV Export:** The exported CSV now shows both the raw mark and the sanitized mark alongside the final grade. This makes it easy for an instructor or reviewer to see how raw Excel inputs were read, which helps when dealing with typos or weird text values.
5. **Flexible Column Matching:** The app now looks for Course/Program and Total Marks headers by pattern matching column names instead of assuming a fixed column order. It can also detect an optional 4th "imported grade" column to compare existing grades with newly calculated ones.
6. **UI Polish:** Redesigned the layout with clearer analytics and grading panels, a proper histogram with a fitted normal curve, grade status badges, and a live timer, giving it a much cleaner overall look.

## How to Run Locally

1. Clone the repository:
   ```bash
   git clone [https://github.com/Moksha0o0/bits_grading_console.git](https://github.com/Moksha0o0/bits_grading_console.git)