# \# BITS Digital CodeForge V1.0 - Advanced Grading Console

# 

# \## Live Demo

# Check out the deployed application here: \[https://college-submission.web.app/](https://college-submission.web.app/)

# 

# \---

# 

# \## Project Overview

# This project is a web-based \*\*Grading Console\*\* designed for instructors to upload student mark sheets, configure dynamic grade cutoffs, analyze class performance statistics, visualize score distributions, and export final grades into standardized reports.

# 

# Starting from the initial prototype, several critical functional and UI bugs were identified and resolved. Following the bug fixes, multiple feature enhancements were implemented to deliver a faster, safer, and more intuitive grading experience.

# 

# \---

# 

# \## Stage 1: Bug Fix Log

# 

# | # | Bug / Issue Identified | How You Reproduced It | Root Cause | Fix Implemented | How You Tested the Fix |

# |---|------------------------|-----------------------|------------|-----------------|------------------------|

# | \*\*1\*\* | Course dropdown keeps showing duplicate/old entries after uploading a second Excel file | Uploaded one file, then uploaded another file with different courses | The file upload handler kept appending new `<option>` tags to the dropdown without clearing out the old list first | Cleared out `courseSelect.innerHTML` back to the default option before loading new courses | Uploaded two different files back-to-back and verified the dropdown only showed courses from the current file |

# | \*\*2\*\* | Grade ranges reset to default every time you switch courses | Uploaded a file with 2+ courses, changed grade ranges for Course A, switched to Course B and back | `buildGradeUI()` (which resets input fields to default values) was running inside the course-change handler on every switch | Moved `buildGradeUI()` so it executes once on page initialization. Course switches now only update stats/roster without overwriting custom ranges | Set custom ranges for Course A, switched to Course B, returned to Course A, and confirmed custom ranges were retained |

# | \*\*3\*\* | Min, Max, Average, and Median showed `NaN` or broke when a course had no valid marks | Uploaded a file and selected a course where all marks were blank or invalid | Stats calculations attempted division by `marks.length` and array indexing without checking if the dataset was empty | Added empty-dataset safety handling in `computeStats()` to display `-` across all metrics when no valid marks exist | Selected a course with 0 valid records and verified the statistics panel displayed `-` without throwing JavaScript errors |

# | \*\*4\*\* | Students with blank, text, or "AB"/"Absent" marks were dropped from exported CSV | Included a row with text (e.g., "AB") in the Total Marks column and exported CSV | Grading logic only processed numeric ranges. Non-numeric inputs were omitted from counts and CSV generation | Implemented `sanitizeMark()` to map blank, non-numeric, or "AB"/"Absent" entries to `NC`, and updated `getGradeForMark()` to handle non-numeric cases | Uploaded a file containing valid marks and "AB" entries; confirmed "AB" rows appeared in the roster and exported CSV as `NC` |

# | \*\*5\*\* | Excel file picker blocked `.xlsx` files depending on browser configuration | Tried selecting a standard `.xlsx` file using the native file picker | The file input tag was restricted to `accept=".xls"`, blocking modern Excel files despite `xlsx.js` support | Updated the file input attribute to `accept=".xlsx, .xls"` | Selected a `.xlsx` file using the file picker and verified successful upload and parsing |

# | \*\*6\*\* | "Reset Range" button triggered two consecutive confirmation pop-ups | Clicked "Reset Range" button | The click event listener called `confirm()` twice in succession | Removed the redundant `confirm()` call so only a single prompt is shown | Clicked "Reset Default" and confirmed only one modal prompt appeared |

# | \*\*7\*\* | Timer clock displayed `00:00` for the first second during startup | Observed timer clock immediately upon page load | `startTimer()` updated the timer display inside `setInterval`, causing a 1-second delay before the first tick | Executed an immediate `tick()` invocation prior to launching `setInterval` | Refreshed the page and verified the clock rendered and updated timestamp formatting immediately |

# 

# \---

# 

# \## Stage 2: Enhancements Made

# 

# \* \*\*Grading Policy Presets\*\*: Added quick preset options (\*Standard BITS\*, \*Rigorous\*, and \*Generous Pass\*) next to the manual range editor. Instructors can instantly preview alternative grade curves without manually retyping range cutoffs.

# \* \*\*Live Roster with Search and Filters\*\*: Implemented a scrollable roster table that updates dynamically as grade cutoffs change. Includes real-time search (by BITS ID or grade) and interactive grade summary chips that filter the roster view.

# \* \*\*Automated NC Handling\*\*: Built a `sanitizeMark()` / `getGradeForMark()` data pipeline that automatically identifies blank, non-numeric, or absent ("AB") entries and maps them to `NC` across the roster, stats summary, and CSV export.

# \* \*\*Comprehensive CSV Exporting\*\*: Exported CSV documents output both raw original input values and sanitized numeric values alongside final calculated grades for complete auditability.

# \* \*\*Flexible Column Matching\*\*: Implemented column header pattern matching (e.g., matching \*Course\*, \*Program\*, \*Total Marks\*, \*Score\*) rather than relying on strict column indices. Includes support for detecting imported reference grade columns.

# \* \*\*Enhanced Visual Analytics\*\*: Upgraded the distribution panel with an animated canvas histogram alongside a smooth fitted Gaussian normal curve overlay, statistical summary cards, and grade distribution badges.

# 

# \---

# 

# \## How to Run Locally

# 

# 1\. \*\*Clone the repository:\*\*

# &#x20;  ```bash

# &#x20;  git clone \[https://github.com/Moksha0o0/bits\_grading\_console.git](https://github.com/Moksha0o0/bits\_grading\_console.git)

&#x20;  cd bits\_grading\_console\\\\\_grading\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\_console.git)





