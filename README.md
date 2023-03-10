# Report for assignment 4

This is a template for your report. You are free to modify it as needed.
It is not required to use markdown for your report either, but the report
has to be delivered in a standard, cross-platform format.

## Project

Name: Teammates

URL: https://github.com/TEAMMATES/teammates

TEAMMATES is a free online tool for managing peer evaluations and other feedback paths of your students. It is provided as a cloud-based service for educators/students and is currently used by hundreds of universities across the world.

## Onboarding experience

We decided to continue on the same project hence the onboarding experience remains the same as the last time. Our onboarding [Onboarding expeirence TEAMMATES](https://github.com/soffan-group-20/teammates/issues/1)

## Effort spent

| Time spent                            | Didrik | Erik   | Hampus | Adam   |
| ------------------------------------- | ------ | ------ | ------ | ------ |
| discussions/meetings                  | 5      | 5      | 5      | 5      |
| discussions within parts of the group | 4      | 2      | 2      | 1      |
| reading documentation                 | 1      | 1      | 1      | 1      |
| configuration and setup               | 1      | 2      | 2      | 2      |
| analyzing code/output                 | 2      | 4      | 2      | 2      |
| writing documentation                 | 2      | 2      | 1      | 1      |
| writing code                          | 7      | 2      | 3      | 5      |
| running code                          | 5      | 4      | 3      | 2      |

## Overview of issue(s) and work done.

For P requirement 5: Code changes are displayed in the following GitHub PRs.

For P requirement 6: Their CI server automatically run tests when a commit is pushed to the repo.

##### PR 1: Add 'course -> copy' option to the instructor home page

URL: https://github.com/TEAMMATES/teammates/pull/12177

Requirements:

1 *Copy button presentation*

> There should be a button "Copy" for each course on the home page. These should be visible when clicking on a course chevron button.

2 *Copy button logic*

> These buttons should copy the course. They should send the same kind of data as in other pages.

Summary & scope:

The copy course functionality was heavily tangled with presentational logic for the courses page. This functionality had to be moved out to their own service, in order to be used from multiple components.

35 files changed, with ~1500 LOC changes (most LOC changes are from test snapshots).

Tests:

Requirement 1 is simply a presentational requirement, which writing a test for would clutter the code base, since we would essentially be testing whether or not the Angular framework can render HTML elements.

This test is made to make sure requirement 2 works: https://github.com/TEAMMATES/teammates/blob/a75f084d37361f835fb600c730df5d1a5a2f722e/src/web/app/components/course-copy/course-copy.component.spec.ts

### UML class diagram and architecture

In Angular 2 there are things called components, having responsibility for presentation, and service, having responsibility for business logic. The course copy logic was now extracted (refactoring pattern) to the `course` service, allowing the logic to be used from any component. The instructor home page and the courses page have a lot in common, which is why this service pattern is good for these kinds of projects. Angular uses a pattern called dependency injection, to allow for components and other services to dynamically tell the execution environment what services they are dependent on. Angular will then, during runtime, inject these services into components and services. Services are by default global, but components can demand that they be given a new scope of a service, which will create a new root service for themselves and all their child components, or services which their child component uses.

Angular is a standard MVC (model, view, controller) framework, meaning separation of these concerns are emphasized. This is implemented by having the view in HTML files, and controllers in Javascript/Typescript files. Models can be supplied either through an API on the web, or be in data structures on the client.

Another commonly used pattern in this project is the Observer pattern, used by the `rxjs` library. The `rxjs` library usually exposes observables on a service level, allowing components to listen to global data changes. `rxjs` also allows for filtering, mapping, and other operators on an observable stream.

Before:

![Blank_UML](https://user-images.githubusercontent.com/5240046/223676185-93346e94-ae8a-4fab-b1f6-ce9f09a219e9.png)

After:

![Blank_UML-2](https://user-images.githubusercontent.com/5240046/223676206-9ee5a639-8cc9-4516-be2c-988786117619.png)

P+ items:

- Optional (point 1): architecture is discussed.
- Optional (point 2): software architecture is discussed.
- Optional (point 3): tests are traced to requirements.
- Optional (point 4): the patch is clean.
- Optional (point 5): considered for acceptance (passes all automated checks), at least the front end checks. Their E2E tests seem to fail for all PRs, but since these have nothing to do with our implementation we consider this PR to pass all automated checks.

##### PR 2: Instructor viewing results of rubric questions: missing space after checkbox

URL: https://github.com/TEAMMATES/teammates/pull/12151 (Merged)

Requirements:

1 *Gap between checkbox and text*

> There should be a space between a checkbox and a text

2 *No dots in gap*

> There should be no dots in the gap.

Summary & scope:

A class `form-check` was added to the parent container, which automatically created the gap. This will not impact functionality but is a visual improvement and affects the file `rubric-question-statistics.component.html`.

1 file changed, 1 LOC.

- Optional (point 3): no tests are required.
- Optional (point 4): the patch is clean.
- Optional (point 5): considered for acceptance (passes all automated checks).

##### PR 3: Instructor home page: redundant padding

URL: https://github.com/TEAMMATES/teammates/pull/12181

Requirements:

1 *No extra padding*

> There should be no extra padding between the inner border and the outer border.

Summary & scope:

The class `col-12` was removed from an element in `sessions-table.component.html` which
fixed the padding issue. The majority of the time was spent trying to understand the
bootstrap tool used by the project and navigating around different files trying
to find the relevant element to modify.

1 file changed, 1 LOC.

- Optional (point 3): no tests are required, but some pre-existing component tests had to be modified.
- Optional (point 4): the patch is clean.

## Code changes

Check the linked pull requests.

## Test results

Check the linked pull requests.

## Overall experience

#### What are your main take-aways from this project? What did you learn?
Didrik: I have practiced using jest to test front end Angular code. I've honed my skills of refactoring large code bases.

Erik: I have increased my knowledge of Git and Github, worked with front-end for the first time (Angular, TypeScript) and improved in testing code. I also feel I have gotten a better understanding of how projects and working together with a team in software development work.

Hampus: During this project I feel like I've practiced analyzing and rewriting code that might not be the most structured and understanding machinery in an entire system.

Adam: I have now had a taste of modern web development. I learned about some Javascript toolkits/libraries/frameworks but I hope to never have to touch them again. A more valuable thing I've learned is how to work with Git and Github on a more advanced level.

#### How did you grow as a team, using the Essence standard to evaluate yourself?

Going through the Essence team checklist we established that we are currently in the Performing state. We have been able to successfully implement a way of working and have trust in each other as a team to take responsibility and do the work needed in a cohesive manner. We are at a stage where we are now performing tasks and identifying, addressing, and eliminating potential problems within the team and as we are now close to finishing the course and the assignments, we place ourselves in the Performing state. What hinders us from reaching the last state Adjourned is being fully complete with the assignment. When this last assignment has been submitted and graded we can fulfil the requirements for the last state and see ourselves as done.

As the group has gotten to know each other better I think we have improved, both individually and as a team. For example, we have realized our strengths and weaknesses, allowing us to work more efficient and find tools and techniques which benefits our working process. We have also been able to improve communication and collaboration within the team. Despite making great progress throughout the course there is always more ways to improve. We are certain we could, if we were to continue working together for a longer period of time, optimize our way of working further and ultimately develop a more efficient process within the team. One of the things we believe can be improved even more is assessing ourselves and our work. For example, by making it a habit in our way of working to continuously pause and assess ourselves and our tools and techniques. In the same way we believe communication within the team could be improved further by making it a habit to have regular team meetings and keeping each other up to date on everyone???s status.
