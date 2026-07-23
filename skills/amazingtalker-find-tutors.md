---
name: Find AmazingTalker tutors
description: Search AmazingTalker for tutors in a subject and surface bookable profiles with pricing and ratings.
api: openapi/amazingtalker-find-tutors-openapi.yml
operations:
- findTeachers
---

# Find AmazingTalker tutors

Use this skill to find tutors on AmazingTalker for a given subject and present bookable options to a learner.

## Authentication
None. The API is public — `findTeachers` requires no API key or token.

## Steps

1. Call `findTeachers` (`GET https://en.amazingtalker.com/v1/pages/teachers`).
   - Required: `teach_subject` — English letters only, e.g. `english`, `math`.
   - Optional filters:
     - `price_preference` — one of `super_low_price`, `low_price`, `intermediate`, `middle`, `high_price`, `super_high_price` (roughly 0–10, 11–15, 16–20, 21–25, 26–30, 30+ dollars).
     - `tag_url_name` — learning need, English letters only, e.g. `certification`, `conversation`.
     - `auxiliary_language` — a language to also use in class, English letters only, e.g. `english`, `chinese`, `japanese`.
     - `teacher_location` — ISO 3166-1 alpha-2 country code, e.g. `TW`, `US`.
     - `other` — free-text fallback for anything the named filters don't cover.

2. Read the returned array of teacher objects. Each has `teacher_name`, `short_description`, `image_url`, `introduction_video_url`, `course_url`, `avg_rating`, `trial_dollar`, and `private_dollar`.

3. Present matches ranked by `avg_rating` and price fit. Link the learner to `course_url` (the sales/booking page) to reserve a trial or lesson.

## Notes
- Filter parameters that accept only English letters will reject other characters — normalize input before calling.
- `trial_dollar` is the trial-class price; `private_dollar` is the formal-course price.
- The call is a read-only GET and safe to retry.
