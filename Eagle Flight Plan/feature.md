# Eagle Flight Plan — Features

## Parent user story

> As a student, when I want to do some activities to prepare me to get a job when I graduate, I want to have a checklist of tasks and events that I can do each semester I am in school so that I am prepared to successfully apply for a job.

## System overview

Eagle Flight Plan helps students prepare for job applications throughout college. Career-readiness work is broken into a **semester-by-semester checklist** of **tasks** (for example, write a résumé) and **events** (for example, attend a career fair). **The checklist is not one campus-wide list:** each **college / major** has its own plan, then filtered by the student’s class year and semester.

**Students** follow and complete their plan. If a student **changes major**, they move onto that major’s plan: completed items that also exist on the new plan stay complete; items that do not apply are dropped. Most items are **self-reported**. A smaller set of high-impact items (for example, attending a career fair or finishing a mock interview) also ask for a short **what happened / results** note. Completing that note is enough for the item to count; staff feedback is optional coaching, not a grade. **Career Services / admins** define and maintain the tasks and events, including which items need that extra note. **Faculty / advisors** and Career Services can **read** those notes and **comment** with feedback.

## Roles

| Role | Purpose in this system |
| --- | --- |
| Student | View and complete the plan; set college, major, and class year; write notes; read staff feedback |
| Faculty / advisor | View advisees’ checklists and notes; leave optional comments to coach the student |
| Career Services / admin | Create, edit, and publish plans **by college and major**; manage tasks, events, and access |

---

## Feature 1: Semester checklist

Students see a checklist of career-prep items for a given semester instead of a single unstructured list. Advisors can open the same checklist for a student they advise.

### User stories

1. As a student, I want to view a checklist of tasks and events for the **current** semester (determined by the system, not picked by me as “now”) so that I know what to work on this term.
2. As a student, I want to switch the view to other semesters (for example, last Spring or next Fall) so that I can plan ahead and review past checklists without changing what “current” is.
3. As a student, I want checklist items grouped by type (task vs. event) so that I can tell which items I complete on my own and which require attending something.
4. As a student, I want each checklist item to show a short title and completion status so that I can scan what is done and what is still open.
5. As a faculty member / advisor, I want to view a student’s semester checklist so that I can see what they are supposed to be doing this term.

---

## Feature 2: Academic standing, major, and relevant plan

The checklist should match the student’s **college/major** and **class year**. A freshman in Computer Science and a senior in Business should not see the same plan.

**The student sets college, major, and class year** in their profile. **The system determines the real current semester** from the academic calendar (for example, Fall 2026 vs. Spring 2027). Students do not pick “what term it is now.”

### User stories

1. As a student, I want to choose my college and major from a list so that I am placed on the correct flight plan.
2. As a student, I want to set my class year (freshman, sophomore, junior, senior) in my profile so that I see a plan that fits my year.
3. As a student, I want my default view to open on the checklist for the real current semester so that I do not have to pick the term myself.
4. As a student, I want to see recommended items for later semesters in **my** major’s plan so that I understand the full path to being job-ready by graduation.
5. As a student, I want my checklist to show my major, college, class year, and the current semester so that I can tell I am on the correct plan.
6. As a Career Services admin, I want to assign checklist items to a college, major, class year, and semester so that the right students see the right work.
7. As a Career Services admin, I want to maintain the academic calendar (when Fall, Spring, and other terms start and end) so that the system always knows which semester is current.
8. As a faculty member / advisor, I want to see a student’s major, college, class year, and the current semester next to their plan so that I know which flight plan they are on.

---

## Feature 2b: Change of major

When a student **updates their major in their profile**, their checklist switches to the new program’s plan. Progress is not wiped: items that exist on both plans keep their completion (and any notes/comments). Items that belong only to the old major no longer appear as required work.

This version does not define a separate path for undeclared students or double majors. Advisors and admins do not change the student’s major for them.

### User stories

1. As a student, I want to change my major in my profile so that I can move to the correct plan without asking staff to edit it.
2. As a student, I want to confirm the change before it applies so that I do not switch plans by accident.
3. As a student, I want my checklist to switch to my new major’s plan after I confirm so that I am not following the old program’s tasks.
4. As a student, I want items I already completed that also exist on the new plan to stay marked complete so that I do not redo work (for example, a résumé or a career fair I already attended).
5. As a student, I want old-major-only items to drop off my active checklist so that I am not asked to finish work that no longer applies.
6. As a student, I want notes and staff comments on kept items to still be there after the switch so that my history is not lost.
7. As a student, I want to see a short summary of the new major and which items carried over so that I understand what changed.
8. As a faculty member / advisor, I want to see that an advisee changed majors and is now on the new plan so that I advise against the right checklist.
9. As a Career Services admin, I want a student’s plan to rebuild from the new major automatically when they update it so that I do not rebuild their list by hand.

---

## Feature 3: Task and event details

Users need enough information to complete or explain an item correctly, not only a title.

### User stories

1. As a student, I want to open a checklist item and read a description of what to do so that I know how to complete it.
2. As a student, I want to see suggested timing or due dates for an item so that I can finish it during the right part of the semester.
3. As a student, I want event items to show date, time, and location (or virtual link) so that I can attend them.
4. As a student, I want to see why an item matters for job applications so that I am motivated to complete it.
5. As a student, I want links or next steps (for example, Career Services, résumé upload, or event signup) so that I can act without leaving the plan.
6. As a Career Services admin, I want to enter and update an item’s description, timing, location, and links so that students get accurate instructions.
7. As a faculty member / advisor, I want to read the same item details a student sees so that I can explain next steps in an advising meeting.

---

## Feature 4: Completion tracking

Most checklist items are completed on the honor system: the student marks them done and they count immediately. Staff can still see status. Completing an item does **not** require staff approval.

### User stories

1. As a student, I want to mark most tasks as complete without extra paperwork so that routine items stay quick to update.
2. As a student, I want to mark an event as attended so that my checklist reflects that I went.
3. As a student, I want to undo a completion if I marked the wrong item so that my record stays accurate.
4. As a student, I want completed items to stay visible but clearly marked done so that I can see what I have already accomplished.
5. As a student, I want incomplete items to stay easy to find so that I know what still needs to be done this semester.
6. As a faculty member / advisor, I want to see which items a student has completed so that I can focus advising on what is still open.
7. As a Career Services admin, I want to see completion status for students so that I know who is using the plan and who may need outreach.

---

## Feature 4b: Reflection / results on selected items

Some items need more than a checkmark. When Career Services marks an item as needing a follow-up note, the student must add a short description before it counts as complete. Examples:

- Career fair: what happened (who they talked to, what they learned, next steps)
- Mock interview: results afterward (feedback received, strengths, what to practice)

These notes are still student-written. They are not a staff sign-off. Staff may **read** the note and **leave a comment**. A comment is optional coaching; the item is complete once the student submits the note.

### User stories

1. As a student, I want to know which items need a short description or results note so that I am not surprised at check-off time.
2. As a student, I want to write a brief “what happened” note when I attend a career fair so that I remember the outcome and my advisor can see it.
3. As a student, I want to record mock-interview results (feedback and what I will work on) so that the item reflects practice, not only attendance.
4. As a student, I want the item to stay incomplete until I add the required note so that I finish the reflection, not only the checkmark.
5. As a student, I want to edit my note later so that I can add a follow-up (for example, a recruiter emailed me after the fair).
6. As a faculty member / advisor, I want to read a student’s career-fair description and mock-interview results so that I can coach them on next steps.
7. As a Career Services admin, I want to mark an item as “checkmark only” or “requires a student note” so that only the right items ask for extra writing.
8. As a Career Services admin, I want to set a short prompt for those items (for example, “What happened at the fair?” or “What were your mock-interview results?”) so that students know what to write.

---

## Feature 4c: Optional staff comments on notes

Advisors and Career Services can reply to a student’s reflection or results note. Comments do not approve or reject the item. Students can see the feedback on that checklist item.

### User stories

1. As a faculty member / advisor, I want to comment on a student’s note so that I can give specific coaching without waiting for a meeting.
2. As a Career Services admin, I want to comment on a student’s note (for example, mock-interview results) so that I can reinforce what they should do next.
3. As a student, I want to read comments from my advisor or Career Services on my note so that I know how to improve.
4. As a student, I want my item to stay marked complete even if no one has commented yet so that I am not blocked waiting for staff.
5. As a student, I want to be able to add a follow-up on my note after I get a comment so that I can show I acted on the feedback.
6. As a faculty member / advisor, I want to see whether I have already commented on an item so that I do not leave duplicate feedback.

---

## Feature 5: Progress toward job readiness

Students, advisors, and Career Services should see how far a student has come and what is left before they apply.

### User stories

1. As a student, I want to see how many checklist items I have completed this semester so that I can measure this term’s effort.
2. As a student, I want to see overall progress across all semesters so that I know whether I am on track for graduation.
3. As a student, I want to see which high-priority items (for example, résumé, internship search, mock interview) are still incomplete so that I focus on what employers care about most.
4. As a student, I want a simple “ready to apply” summary when core items are done so that I know I am prepared to start job applications.
5. As a faculty member / advisor, I want a progress summary for each advisee so that I can tell who is on track and who is behind.
6. As a Career Services admin, I want aggregate progress (for example, by class year) so that I can see how prepared students are as a group.

---

## Feature 6: Filter, search, and organize the checklist

Long plans are easier to use when users can narrow the list.

### User stories

1. As a student, I want to filter the checklist by category (résumé, networking, internships, interviews, professional skills) so that I can work on one area at a time.
2. As a student, I want to filter by status (not started, in progress, complete) so that I can focus on unfinished work.
3. As a student, I want to search for a task or event by name so that I can find it quickly.
4. As a student, I want optional items distinguished from required items so that I know the minimum I should complete each semester.
5. As a faculty member / advisor, I want to filter an advisee’s list by incomplete or required items so that advising time stays focused.
6. As a Career Services admin, I want to mark items as required or optional so that the plan has a clear minimum path.

---

## Feature 7: Reminders for upcoming work

Students should not miss time-sensitive events or semester deadlines. Staff may need to know when students are falling behind.

### User stories

1. As a student, I want to see upcoming events on my checklist ordered by date so that I do not miss them.
2. As a student, I want a reminder before an event so that I remember to attend.
3. As a student, I want a reminder for incomplete semester tasks before the term ends so that I can finish them in time.
4. As a faculty member / advisor, I want to see which advisees have incomplete required items late in the semester so that I can follow up.
5. As a Career Services admin, I want to set or update event dates used for reminders so that students are notified from current information.

---

## Feature 8: Accounts and role-based access

Each person signs in as a student, faculty/advisor, or Career Services admin and only sees what their role allows.

### User stories

1. As a student, I want to sign in so that I see my own checklist and progress, not someone else’s.
2. As a student, I want my completions to be saved so that they are still there when I come back next session.
3. As a student, I want my checklist to persist from semester to semester so that my four-year plan is one continuous record.
4. As a faculty member / advisor, I want to sign in so that I only see students I advise (or am allowed to view).
5. As a Career Services admin, I want to sign in with admin access so that I can manage plans without using a student account.
6. As a Career Services admin, I want to assign roles (student, faculty/advisor, admin) so that the right people can view or edit the right things.
7. As a student, I want a profile where I can set my college, major, and class year so that my checklist is personalized.

---

## Feature 9: Plan authoring (Career Services / admin)

Career Services owns the content of each flight plan. Plans are authored **per college and major**, then by class year and semester, so students and advisors work from the list that matches that program.

### User stories

1. As a Career Services admin, I want to create a separate plan for each college and major so that, for example, engineering and business are not forced onto the same checklist.
2. As a Career Services admin, I want to create a task for a given college, major, semester, and class year so that it appears only on the right student checklists.
3. As a Career Services admin, I want to create an event with date, time, and location and attach it to one or more majors so that a campus-wide fair can appear on several plans without duplicating it by hand if we choose to share it.
4. As a Career Services admin, I want to edit or retire an item so that outdated tasks and events do not stay on active plans.
5. As a Career Services admin, I want to publish a semester’s checklist for a major so that students and advisors see a finished plan, not a draft.
6. As a Career Services admin, I want to copy last year’s items for a major into a new semester so that I do not recreate that major’s whole plan from scratch.
7. As a Career Services admin, I want to choose whether a new item is self-check or requires a reflection/results note so that completion rules match the activity.
8. As a Career Services admin, I want a list of majors and colleges I can assign plans to so that I am not typing program names inconsistently.

---

## Feature 10: Advisee roster and student lookup

Faculty/advisors and Career Services need a way to find students, not only a single checklist screen.

### User stories

1. As a faculty member / advisor, I want a list of my advisees so that I can open each student’s plan from one place.
2. As a faculty member / advisor, I want to search for a student I am allowed to view so that I can prepare for a meeting quickly.
3. As a Career Services admin, I want to look up any student by name or ID so that I can help them with their plan.
4. As a student, I want advisors and Career Services to see my plan only when they are authorized so that my progress stays reasonably private.
5. As a faculty member / advisor, I want to filter my advisee list by major or college so that I can review one program at a time.

---

## Traceability to the parent story

| Parent need | Features that address it |
| --- | --- |
| Do activities that prepare me for a job after graduation | Features 1, 3, 5, 9 |
| Checklist of **tasks** and **events** | Features 1, 3, 4, 4b, 9 |
| Organized **each semester** I am in school | Features 1, 2, 8, 9 |
| Plan matches the student’s field of study | Features 2, 2b, 9, 10 |
| Be prepared to **successfully apply** for a job | Features 4, 4b, 4c, 5, 6, 7, 10 |
| Staff support the student (advisors + Career Services) | Features 4c, 8, 9, 10, plus staff stories in 1–7 |
