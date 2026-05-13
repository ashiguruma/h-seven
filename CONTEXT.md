# Domain context: h-seven

h-seven is a personal productivity app grounded in Stephen Covey's _The 7 Habits of Highly Effective People_. The domain centres on intentional weekly living: defining the roles you inhabit, setting goals within each role for the week, focusing energy on what matters rather than what shouts loudest, and renewing yourself across all four dimensions of life.

---

## Glossary

Use the **Preferred term** column when naming types, variables, components, issue titles, and test descriptions. The **Avoid** column lists synonyms that sound similar but carry different connotations or create ambiguity.

| Preferred term | Definition | Avoid |
|----------------|-----------|-------|
| **Mission** | A personal mission statement — a short declaration of purpose and values that acts as the north star for all planning. One per user; long-lived. | Vision, goal, objective |
| **Role** | A life role the user defines for themselves (e.g. "Parent", "Builder", "Learner", "Friend"). Roles are the lenses through which goals are set each week. A person typically has 5–7 roles. | Category, area, hat |
| **WeeklyPlan** | The container for one week's planning session. Anchored to a specific calendar week (identified by its Monday date in ISO format). A new WeeklyPlan is created each week; previous ones are read-only history. | Week, journal, log |
| **RoleGoal** | One goal scoped to a specific Role within a WeeklyPlan. Has a title and a done/not-done status. A Role may have zero or more RoleGoals per week. | Task, action item, to-do |
| **Task** | A discrete action that can be scheduled, prioritised, and completed. Has a title, optional Role association, a Quadrant, and a status (open or done). Unlike a RoleGoal, a Task lives outside any specific WeeklyPlan and can carry over across weeks. | To-do, item, action |
| **Quadrant** | One of four priority zones from the Eisenhower matrix, as mapped to Covey's framework. Q1 = Urgent + Important (crises); Q2 = Not Urgent + Important (planning, prevention, growth — the target zone); Q3 = Urgent + Not Important (interruptions); Q4 = Not Urgent + Not Important (trivia). The app defaults to showing Q2. | Priority level, urgency tier |
| **Big Rock** | A Task or RoleGoal that represents high-leverage, Q2 work — the kind of thing that gets squeezed out by urgency if not scheduled deliberately. Not a separate data type; it's a descriptor applied to Q2 Tasks and RoleGoals. | Key result, OKR |
| **SharpenEntry** | A weekly log of renewal activity, one per WeeklyPlan. Records activity or reflection across all four Dimensions. Named for Habit 7, "Sharpen the Saw". | Reflection, log, journal entry |
| **Dimension** | One of four renewal categories: Physical (body, exercise, nutrition), Mental (learning, reading, planning), Social/Emotional (relationships, empathy, service), Spiritual (values, meditation, nature). Each Dimension has a free-text notes field and an optional effort rating (1–5). | Pillar, area, category |

---

## Key invariants

- A **WeeklyPlan** is created at most once per calendar week. The week key is the Monday date in `YYYY-MM-DD` format.
- A **RoleGoal** belongs to exactly one Role and one WeeklyPlan.
- A **Task** is not bound to a WeeklyPlan; it persists until marked done or deleted.
- A **SharpenEntry** is always 1:1 with a WeeklyPlan — created automatically when the weekly plan is opened.
- The **Mission** is a singleton — there is only one, and it is replaced (not versioned) when updated.

---

## What this app is not

- It is not a general task manager (no projects, no tags, no recurring tasks in v1).
- It is not a habit tracker (daily streaks, chains) — that's a different paradigm.
- It is not a calendar — Tasks have no due dates in v1.
