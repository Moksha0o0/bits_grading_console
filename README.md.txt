# BITS Digital CodeForge V1.0 - Grading Console

## 🚀 Live Demo
You can access the deployed application here: [https://college-submission.web.app/](https://college-submission.web.app/)

---

## 📌 Project Overview
This application is a web-based Grading Console prototype built for instructors to upload Excel mark sheets, configure grade ranges, analyze student performance, and export final grade distributions as CSV files.

---

## 🐛 Stage 1: Bug Fix Log

| # | Bug / Issue Identified | How You Reproduced It | Root Cause | Fix Implemented | How You Tested the Fix |
|---|-----------------------|-----------------------|------------|-----------------|------------------------|
| 1 | Course list duplicates after uploading another file | Uploaded two Excel files sequentially | Existing course options were not cleared | Cleared existing options before adding new courses | Uploaded 2 files and verified unique course list |
| 2 | Average shows an incorrect value when no students are present | Selected a course with no records | Average calculation was performed on an empty dataset | Added empty-data handling | Tested with an empty course |
| 3 | [Your bug description] | [Your test steps] | [Your diagnosis] | [Your solution] | [Your verification] |

---

## ✨ Stage 2: Enhancements Made

1. **Enhancement 1 (e.g., UI / UX Redesign):** Brief explanation of what you improved and why it helps the instructor.
2. **Enhancement 2 (e.g., Visual Analytics & Charts):** Brief explanation of the feature added.
3. **Enhancement 3 (e.g., Input Validation & Error Handling):** Brief explanation of how it prevents bad inputs or improves security.

---

## 🛠️ How to Run Locally

1. Clone the repository:
   ```bash
   git clone [https://github.com/YOUR-USERNAME/YOUR-REPOSITORY-NAME.git](https://github.com/YOUR-USERNAME/YOUR-REPOSITORY-NAME.git)