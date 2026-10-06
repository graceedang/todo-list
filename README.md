# Lab 4: From Specifications to Design

In this lab, you will explore a small todo list application and think about
how we get from a description of what a program should do to a design that
can actually support that behaviour.

You will:

- explore an existing (and not particularly well-designed!) todo list application;
- identify entities and responsibilities from a specification;
- draw a UML class diagram;
- use a **scenario walk-through** to check your proposed design; and
- try to implement a user story and see what questions the story leaves unanswered.

---

## Getting Started

Each team member should clone the lab repo and make sure they can run the program in IntelliJ.

If you have technical problems, ask your teammates for help first, and ask a TA
if the problem persists.

You should each see something like this when running the program, but with no initial todo items:

![Todo List App Screenshot](images/todo-app.png)

To interact with the program:

- Type a name for a task and press Enter/Return to add it to the list.
- Select a task and press the spacebar to toggle whether it is completed.
- Try selecting an existing task. What happens?

Spend a few minutes experimenting with the program, but don't look at the code yet.

---

## Part 1: What Can the Program Do?

A **user story** describes a feature from the perspective of a user:

> As a [kind of user], I want to [accomplish a goal] so that
> [I receive some benefit].

Consider the following user stories for a todo list application.

As a user ...

1. I want to add a todo item so that I can keep track of tasks.
2. I want to view my todo list so that I can choose what to do next.
3. I want to mark a todo item as done so that I can track my progress.
4. I want to unmark a todo item as done so that I can revisit tasks.
5. I want to remove a todo item so that I can manage my tasks.
6. I want to edit a todo item so that I can update task details.
7. I want to filter my todo list by completed or incomplete items so that I can
   focus on what needs to be done.
8. I want to sort my todo list by priority or due date so that I can prioritize
   my tasks.
9. I want to save my todo list so that I can keep my changes when I quit.
10. When I open the app, I want to see my existing todo list so that I can
    continue working on my tasks.

Still without looking at the code, as a team:

1. Which stories does the current program support?
- Supports: 1, 2, 3, 4, 5, 9 10
3. Which stories does it only *partially* support?
- Supports: 7

Now find the code that implements the **Mark a todo item as done** user story.

While investigating that code, answer:

- What Java type represents a todo item?
- How is a todo item's completion status represented?
- How can the program tell whether a todo item is completed when it saves the data?
- What do you think of this current representation?

> You do not need to understand every line in `TodoListPanel`. Focus on tracing
how this one piece of functionality works.

---

## Part 2: From a Specification to a Design

In Part 1, you saw how the existing program represents todo items and their
completion status. That representation works, but it was part of the user
interface rather than a truly object-oriented solution.

Let's step back from the existing code and start again from a slightly more formal
specification of the expected behaviour of our todo list application. We will use this
specification to identify classes and responsibilities for an object-oriented design.

Here is a specification for the todo list application:

> A todo list application lets a user create a list of tasks to be completed.
> Each task has a title, description, due date, and priority level.
> The user can add, edit, delete, and mark tasks as completed.
> The application should allow the user to filter tasks to see only the ones
> not yet completed, and sort the list of tasks by name, due date, or priority.
> The application should automatically save the list of tasks to persistent
> storage so that the todo list persists when they quit and reopen the app.

### Noun–verb analysis

To get started, perform a **noun–verb analysis** of the specification as a team.

1. Identify the important **nouns**.
   - Which are candidate classes?
   - Which are better represented as attributes (instance variables) of another class?

2. Identify the important **verb phrases**.
   - What responsibilities do they suggest?
   - Which of your candidate classes should be responsible for each one?

> Remember, not *every* noun and verb should necessarily become a class or method
> in our design.

### Draw your UML

Use your analysis to draw a UML class diagram for the **entities** needed to
represent the todo list domain.

Include:

- class names;
- important instance variables;
- important responsibilities/methods; and
- relationships between your classes.

Focus on the data and operations that would exist regardless of what the user
interface looks like.

> You can either draw by hand or use PlantUML for this step.

---

## Part 3: Check Your Design with a Scenario Walk-Through

A UML class diagram can look reasonable without actually containing everything
needed to carry out the program's behaviour.

Let's check your team's design!

Consider this scenario:

> **A user marks an incomplete todo item as completed.**

Put your UML diagram where everyone on your team can see it. Manually trace
through how the objects in your proposed design would carry out this scenario.

For each step, ask:

1. Which class has the responsibility for this step?
2. What other objects would an instance of that class need to collaborate with?
3. What information would it need?
4. Does your UML class diagram provide the responsibilities and relationships needed
   for this to happen?

If you reach a step that no class can perform, or an object needs information
that it cannot obtain, **revise your UML diagram and start the scenario again**.

Continue until you can complete the entire scenario without changing your
design.

<details>
<summary>Hint if you are not sure how to do the walk-through</summary>

**Use only the information, relationships, and responsibilities currently shown
on your UML diagram.**

If you find yourself saying "then the task marks itself completed," but your
diagram gives `Task` (or whatever your equivalent class is) no way to do that, you have found a gap.

Add the missing responsibility to your diagram and start the scenario again.

</details>

### Discuss

When your scenario has stabilized:

- Did your UML change during the walk-through?
- If so, what responsibility, information, or relationship was missing?
- If it did not change, what part of your original design made the scenario
  straightforward?

**Be prepared to explain one design decision to your TA.**

---

## Part 4: Compare with One Possible Design

Once you have completed the scenario walk-through, switch to the
`entity-refactor` branch:

```bash
git switch entity-refactor
```

This branch contains **one possible design** that introduces entity objects for
the todo list application.

Run the program again. From the user's perspective, its basic behaviour should
be familiar even though its internal representation has changed.

As a team:

1. Find the entity classes introduced on this branch.
2. Compare them with your UML diagram.
3. Identify one similarity and one difference between your design and this one.
4. Find where the GUI now interacts with these entities.

---

## Part 5: From a User Story to Code

Now consider a feature that the original application does not fully support:

> **As a user, I want to edit a todo item so that I can correct or update a task.**

This sounds like a fairly simple feature.

Let's try to implement it.

### Before you start

Run the application and select an existing task.

Notice what the program already does when a task is selected. Look at the
relevant code and discuss how you could build on it.

Before you start coding, do a quick **scenario walk-through** for editing an
item using the entity design on this branch.
Does the current design provide the responsibilities, information,
and relationships needed to carry out the scenario? If not, identify what needs
to change before you begin implementing the story.

### Try implementing the user story

Choose one team member who will do the coding for your team during this part,
and one team member to take notes.

As a team, begin modifying the program to support editing a todo item.

**Spend at most 10 minutes on this. You are not expected to finish implementing
the feature.**

> **Whenever your team needs to decide what the program should do and the user
> story does not give you the answer, stop and write down the question.**

As a team, decide on a reasonable answer to your question and continue working.

> **For extra practice:** Try making the same change on the `main` branch.
> Is the feature easier or harder to implement with the original representation
> of todo items? Why?

### Stop and Reflect

After about 10 minutes, stop coding, even if you have not finished.

Review the questions your team wrote down.

Discuss:

1. Did your scenario walk-through reveal anything that needed to change in the
   class design?
2. What decisions did you have to make that were **not specified by the user
   story**?
3. Which of those decisions describe what the **user should observe**?
4. Which are decisions about the internal **design or implementation**?

Write down **two questions about the expected behaviour that would need
to be answered before you could confidently implement this feature.**

A user story deliberately gives us a concise statement of a user's goal and
the value of that goal. As you have just seen, that does not necessarily give
developers enough behavioural detail to implement and test the feature without
further discussion.

Soon in the course, we will introduce the concept of **use cases** to make some
of that behavioural detail explicit.

---

# Extra Practice (Optional)

If your team has extra time, choose **any other user story** from Part 1 that
the program does not currently support and try to implement it.

Before you start coding, use the idea of a **scenario walk-through** with the
entity design on the `entity-refactor` branch:

1. Walk through what needs to happen to accomplish the user story.
2. Identify which class is responsible for each step.
3. Check whether the current classes have the information, relationships, and
   responsibilities needed to carry out the scenario.
4. If you discover a gap, modify the class design before continuing with your
   implementation.

As you work, keep track of two different kinds of changes you encounter:

- **Behavioural decisions:** Did the user story leave anything unclear about
  what the program should do?
- **Design changes:** Did supporting the story require adding or changing a
  responsibility, relationship, or class?

If you finish implementing the story, try another one!

---

# Next: Your Project

You have now seen several stages of moving from requirements toward working
software:

- a written **specification** helped identify candidate entities and
  responsibilities;
- a **UML class diagram** recorded a proposed design;
- a **scenario walk-through** helped test a design and identify changes needed
  to support a concrete scenario;
- a **user story** captured a user's goal, but left questions to resolve before
  implementation.

Now you will start to apply these ideas to your team's own project!
