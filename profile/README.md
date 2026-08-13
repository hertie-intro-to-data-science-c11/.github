# Introduction to Data Science

**Introduction to Data Science** - the persistent **course org** for this course, managed by the Hertie Data
Science Lab. It is the control panel: version-controlled materials + assignment templates, plus
every faculty & instructors action button. Each year's students live in a separate **cohort org** that
receives releases from here.

> **Faculty & instructors - start here:** run everything from the
> **[`.github` Actions tab](https://github.com/intro-to-data-science-c11/.github/actions)**. New to the platform?
> Follow the step-by-step
> **[workflow runbooks](https://github.com/hertie-data-science-lab/dsl-teaching-toolkit/blob/main/docs/README.md)**.
> The sections below are a live index of this org's cohorts, repositories, and actions.

_This page is auto-generated; edits will be overwritten on the next refresh._

## Cohorts

List of cohort orgs registered to receive releases from this course org. _Auto-discovered from the
`cohort-courses-pages.yml` registry_:

- [intro-to-data-science-f26](https://github.com/intro-to-data-science-f26)

## Repositories

List of all repositories associated with the course org; a centralised registry and historical
record of course-related content. _Add new course-related content here, then push to the relevant
cohort org using the GitHub Actions below_.

| Repo | Visibility | Description |
| --- | --- | --- |
| [course-materials-f2026](https://github.com/intro-to-data-science-c11/course-materials-f2026) | private | Course materials (lectures/readings by session) |

## Available actions for faculty, instructors & admin

All actions live in the [`.github` repo's Actions tab](https://github.com/intro-to-data-science-c11/.github/actions)
_(automatically bootstrapped from the central
[dsl-teaching-toolkit repo](https://github.com/hertie-data-science-lab/dsl-teaching-toolkit))_:

### One-time setup actions:
- [**Bootstrap cohort**](https://github.com/intro-to-data-science-c11/.github/actions/workflows/bootstrap-cohort.yml) - configure a freshly-created cohort org (sets up scaffold repos), register it with the course org, refresh dropdowns.
- [**Send enrolment codes**](https://github.com/intro-to-data-science-c11/.github/actions/workflows/send-codes.yml) - generate a random non-PII enrolment code per student and email each their code (to their university inbox). Students paste the code into the welcome Join issue - no personal data in the public repo. `dry_run` previews codes + emails. Needs the `GRAPH_*` (or `SMTP_*`) secrets.
- [**Sync membership**](https://github.com/intro-to-data-science-c11/.github/actions/workflows/sync-membership.yml) - one consolidated, fully-automatic reconcile of org + `students`-team access (from `students.csv`), project teams (from `teams.csv`), `course_admins` (from this org's declared `people:` block, mirrored into every cohort's own `course-admin` team), and each cohort's own `instructors`/`teaching_assistants` (from its `classroom-config/people.yml`, reconciled into that cohort's `instructors` team AND a course-org `instructors-<tag>` team). Triggers on push (editing any of those files takes effect immediately, including removals - there's no prune toggle, the file is the live truth) and on a daily cron (catches a faculty entry's `start`/`end` rotation with no edit that day); `workflow_dispatch` is a manual escape hatch.
- [**New materials repo**](https://github.com/intro-to-data-science-c11/.github/actions/workflows/new-materials.yml) - scaffold a correctly-structured `course-materials-<year>` repo (session folders + the Release buttons).
- [**New assignment**](https://github.com/intro-to-data-science-c11/.github/actions/workflows/new-assignment.yml) - scaffold an `assignment-N-<year>` template repo (starter on `main`; the `solution` branch carries the model solution, `grading.yml`, and the hidden tests).
- [**Refresh actions**](https://github.com/intro-to-data-science-c11/.github/actions/workflows/refresh-actions.yml) - repopulate the cohort/session/assignment dropdowns, re-equip content repos, and rebuild this index. Runs itself nightly, so this org stays in step with the central toolkit on its own.
- [**Check cohort setup**](https://github.com/intro-to-data-science-c11/.github/actions/workflows/check-cohort-setup.yml) - a per-cohort checklist of everything configured (identity, people, schedule + release plan, roster, teams, grades) with direct edit links for anything missing. Read-only.

### Optional: public course website (open courseware)
- [**Publish course website**](https://github.com/intro-to-data-science-c11/.github/actions/workflows/publish-site.yml) - build/refresh a PUBLIC site `intro-to-data-science-c11.github.io` that shares this course's lecture materials and readings with the world. Opt-in (the first run scaffolds the site); afterwards a daily cron re-syncs it from the settings that run chose, so later materials edits appear without another click. Pick a materials repo and choose for readings: `reading-list` (citations only) or `actual-readings` (also host the files). Because the materials repos are private, the site **hosts** the shared files itself. This is separate from each cohort's student-facing site.

### Session cadence actions:
- [**Release materials**](https://github.com/intro-to-data-science-c11/.github/actions/workflows/release-materials.yml) - copy path(s) from a course repo into a cohort repo: any folder or file (a session folder, a whole section, a subpackage of a growing importable package), one or several at a time.
- [**Release assignment**](https://github.com/intro-to-data-science-c11/.github/actions/workflows/release-assignment.yml) - generate one private repo per student from a chosen `assignment-*` template repo.

NB: alternatively each materials repo *also* carries its own **Release** buttons (run from inside the
repo; there `course_source_repo` is pre-filled with that repo instead of being a dropdown).

### Grades (private, previewable):
- [**Grade assignment**](https://github.com/intro-to-data-science-c11/.github/actions/workflows/grade-assignment.yml) - faculty-side autograder: after the deadline, run the HIDDEN tests (from the template's `solution` branch) against each submission and record the machine score into `classroom-config/grades/<assignment>.csv`. Nothing is written to student repos; faculty & instructors then add manual marks. Optional per assignment (skipped if `grading.yml` sets `autograde: false`).
- [**Sync gradebooks**](https://github.com/intro-to-data-science-c11/.github/actions/workflows/sync-gradebooks.yml) - ensure every onboarded student has a PRIVATE `grades-<handle>` repo (the single home for all their grades). Idempotent.
- [**Render grades (preview)**](https://github.com/intro-to-data-science-c11/.github/actions/workflows/render-grades.yml) - build per-student `gradebook/<handle>.yml` from `classroom-config/grades/<assignment>.csv` and open ONE pull request. **That PR is the preview** - review every student's grades in the diff before sending.
- [**Distribute grades**](https://github.com/intro-to-data-science-c11/.github/actions/workflows/distribute-grades.yml) - after merging the preview PR, copy each student's gradebook into their private repo and (unless silenced) email each student a notification to their university inbox (needs the `GRAPH_*` or `SMTP_*` secrets).

- [**Scheduled release**](https://github.com/intro-to-data-science-c11/.github/actions/workflows/scheduled-release.yml) - hourly cron that auto-releases whatever each cohort's `classroom-config/schedule.yml` `releases:` plan says is now due (honouring each release's `when` time to the hour). Manual runs default to a dry-run preview ("what opens when"). Manual buttons above still work for early/ad-hoc release.

- _[**Sync site**](https://github.com/intro-to-data-science-c11/.github/actions/workflows/sync-site.yml) - regenerate a cohort's website from the org structure (releases do this automatically; standard workflow has no need for manual sync)._

## How the actions behave

**Release materials** - run it from the materials repo (`course_source_repo` pre-filled with
that repo) or from the course org's central `.github` control panel (`course_source_repo` is
a dropdown). **Both** take the same five fields, which are exactly a `schedule.yml` `deploy:`
entry: `cohort_org`, `course_source_repo`, `course_source_path`, `cohort_dest_repo`,
`cohort_dest_path` - so the manual button and the scheduled release plan share one
vocabulary. `course_source_path` is any folder or file (`lectures/03_regression`,
`mlpkg/simulation`, `SYLLABUS.md`); a folder is copied whole, **every file** in it.
`course_source_path` and `cohort_dest_path` accept comma-separated lists paired in order, so
one click can release several paths at once; a blank `cohort_dest_path` mirrors each source
path. `cohort_dest_repo` (default `materials`) is created on demand, private, with
`students` **and** `auditors` read. Copies are additive and idempotent: only what you have
released appears, and re-releasing changes nothing.

**Release assignment** - two stages: (1) it freezes a cohort-level template repo
`<assignment>` from your `assignment-*-<year>` template; (2) it generates one private
`<assignment>-<handle>` repo per onboarded student **from that cohort template**, adding
each as collaborator. After the assignment deadline, rerun with **include_solution** to push the
template's `solution` branch into every student repo. Solutions stay on the `solution`
branch so a normal release never leaks them.

**The cohort website** - every cohort has an auto-deployed site `<org>.github.io`. It is regenerated
on every release (and via **Sync site**). Its lecture links point at the cohort's private repos, so
they only resolve for enrolled members (deliberate).

**The public course website** (optional) - `Publish course website` builds `intro-to-data-science-c11.github.io`, a public
open-courseware site for the course as a whole. Unlike the cohort sites it **hosts** the shared lecture
files (the source repos are private, so links would 404); readings are published either as a text-only
reading list or as hosted files. It is opt-in - releases and refresh never touch it, so a public site
only exists once you run the action - but after that first run a daily cron re-syncs it from the
settings you chose, so later materials edits reach it on their own.

## Repository structure (required)

```
intro-to-data-science-c11/                            <- this COURSE org (persistent)
|-- .github/                      profile + faculty & instructors action buttons + cohort registry
|-- course-materials-<year>/      lectures/01_.../   readings/01_.../   (+ syllabus, README)
`-- assignment-<n>-<year>/        is_template repo:
                                    main      -> starter + autograder   (students get this)
                                    solution  -> solution/   (pushed to students on demand)

<Course>-f<year>/                 <- one COHORT org per year (Bootstrap cohort sets it up)
|-- welcome/                      Join issue -> onboard (enrol)
|-- classroom-config/             students.csv  (private roster)
|-- materials/                    released lectures/readings  (students-team read)
|-- <org>.github.io/              auto-deployed website (synced from this structure)
`-- <assignment>-<handle>/        one private repo per student
```

This whole structure is bootstrapped from the central
[`dsl-teaching-toolkit`](https://github.com/hertie-data-science-lab/dsl-teaching-toolkit)
repo (via its **Bootstrap Course Org** action), and the actions above run that same central code.

The course-level actions assume this layout - use **New materials repo** / **New assignment** above to scaffold correctly.

**Materials repo** (`course-materials-<year>`) - the source for Release materials. Any path
in it can be released; the convention below is what the cohort **website** reads, since it
lists whatever sits in an ordinal-prefixed (`01_`, `02_`, `03_`, ...) folder:
- `lectures/01_.../` - one folder per session's lecture files;
- `readings/01_.../` - one folder per session's readings;
- add more sections freely (e.g. `labs/01_.../`) - nothing declares them;
- root files (`SYLLABUS.md`, `README.md`) release like any other path - name the file as the
  `course_source_path`.

**Assignment repo** (`assignment-N-<year>`, an `is_template` repo) - the source for Release assignment:
- **`main` branch** - the starter code only (no tests, no autograder). This is exactly what students receive (native template-generate copies `main` only).
- **`solution` branch** - the model solution (`solution/`), plus **`grading.yml`** and the **hidden tests** that the Grade assignment button runs faculty-side. **All of this MUST live on this branch, never on `main`** - that is what guarantees it is never copied into student repos on generate. Only the `solution/` folder reaches students, and only when you run Release assignment with **include_solution** ticked (a separate, later commit); the hidden tests and `grading.yml` never do.

---
Maintained by the [Hertie Data Science Lab](https://github.com/hertie-data-science-lab).
