---
title: "Good Code Still Matters"
date: 2026-02-26
layout: single
tags:
  - code
  - software
  - vibe-coding
  - engineering
  - AI
  - coding-agents
  - product-management
---

As the desire for faster development and quicker time-to-market continues to grow, the importance of good code remains as crucial as ever. Coding agents are being used to write a significant amount of code without enough context which can lead to bugs, regressions, vulnerabilities, and higher maintenance cost including increased token spend. 

Why should it matter if the machine will just figure it out? Machines can't infer intent and don't handle ambiguity well. There is a very clear desire among software development teams to leverage coding agents to speed up development, but without detailed prompts and useful context your codebase will very quickly become filled to the brim with slop and features will break. Going all-in on coding agents without a strategy built on collaboration, specificity, and a bit of caution _will_ make your software worse, not better. Good code is not just about aesthetics; it's about creating software that is reliable, scalable, and less costly to maintain. In the age of the coding agent it's more important than ever for teams to decide and record what this looks like to them to avoid becoming buried in mountains of buggy, unmaintainable code.

## Good Code in a Group Setting

There is much to be said for the subjectivity of good code, especially when working in diverse teams. Not everyone will agree on all of the same practices and finer details of syntax golf, but it is important that teams develop a mutual vision of how the codebase should be structured and have it written down. It's even more important if you expect coding agents to do everyone's typing for them and produce something passable.

In my experience I have found success in taking some inspiration from Kent Beck's fundamentally excellent book _Extreme Programming Explained_ [^1] by having the team define values, principles, and practices. These are the foundation from which good software arises, and good software starts with good collaboration.

One way to navigate this is by conducting a free-writing exercise where team members take a few minutes to jot down the things that they think represent good coding practices and bad coding practices with no wrong answers. You might end up with something like this, where items on the left and right are not necessarily related:

| Things I Like | Things I Don't Like |
| --- | --- |
| Descriptive variable names | Inconsistent naming conventions |
| Separate modules for features | Large functions with multiple responsibilities |
| Comprehensive unit tests | Lack of documentation |
| Separating state from logic | Deeply nested code |
| Constructive code review | Monolithic classes |
| Robust error handling | Inheritance abuse |

For 10 minutes, a small group of engineers will dig deep into their personal experience to come up with what is essentially a sentiment word cloud that can spark incredibly productive conversations. It helps to stay open minded and ask questions. You may find that there are many shared values to be had, which is exactly the point! From here, you can extrapolate from these preferences into values, principles, and practices. To start, what do we value?

**Values** are axioms that we all agree on, representing high-level ideals from which we can build out the rest of our strategy. From the table above we may realize the following:

```
VALUES
* Documentation
* Understandable code
* Modular structures
* Automated testing
* Separation of concerns
* Feedback from other engineers
* Error handling
```

**Principles** are statements derived from values that help advise behavior for most situations. These are not universal truths and are meant to be adaptable for any given situation or even evolve into something else over time as you learn more or as circumstances demand. It's helpful to think about values as they might apply in a real-world situation and ask yourself: "What should we do **in principle?**":

```
PRINCIPLES
* Documentation should be concise and describe why the code exists
* Variable names should use a standard naming convention and clearly describe the data being held
* Features and services should be kept in separate modules
* Monolithic classes should be broken up into smaller, more purposeful, and testable classes
* Large functions and deeply nested blocks should be broken up into smaller, single-purpose functions
* Unit tests should be written
* State classes should not contain any business logic
* Code review should be thorough, constructive, and encouraging
* Errors should always be handled to promote stability, debuggability, and a helpful user experience
* Inheritance should be used sparingly if needed when defining state models, and not for sharing behavior between classes
```

**Practices** are how you put these values and principles into action. These are concrete steps that can be taken as-needed to ensure what everyone creates is more-or-less aligned with a shared vision. What are your "best practices"?

```
PRACTICES
* Write concise module READMEs that explain why the code exists and how to use it
* Add docstrings that state intent, side effects, and important invariants
* Enforce a consistent naming convention via linters and pre-commit hooks
* Keep state classes as plain data containers; put business logic in service functions/classes
* Prefer composition and explicit interfaces over inheritance for sharing behavior
* Use guard clauses and early returns to avoid deep nesting; refactor nested logic into smaller functions
* Write unit tests for happy paths, edge cases, and failure modes
* Use mocking/fakes for external dependencies and keep unit tests fast and isolated
* Run tests in CI on every PR and require passing status before merging
* Use static typing and linters; fail CI on type or lint regressions
* Handle errors explicitly; attach contextual information and surface actionable messages
* Log errors with structured logs and include correlation/context IDs for debugging
* Require constructive code reviews and a lightweight checklist for common issues
```

Exploring these ideas together in this forum ought to give everyone an opportunity to work out some key differences in opinion and come to a mutually beneficial understanding across many topics.

These ideas also happen to translate very well into instructions for a forgetful text-generating probability machine! Compile them into a shared document such as `CODING_BEST_PRACTICES.md` and commit it to your repository so it can be referenced in your prompts.

## Good Code from an Agent

One of the most effective ways to improve the quality of output from a coding agent is to build a clear system of custom _Skills_ and _Sub-Agents_ [^2]. Coding agents work best when given domain-specific expertise and consistent instructions delivered through structured, reusable documents rather than ad-hoc prompting.

Most of my own experience with coding agents comes from working with _Claude Code_ which has pioneered many of the tools and methods that allow us to improve LLM performance systematically. I can only accurately speak to working with _Claude_, however, Skills and Sub-Agents are fast becoming standards across the board.

### Skills

Skills are markdown files that serve as knowledge repositories for your coding agent and can be used to package your team's values, principles, and practices (among many other things) into reusable instructions. Instead of repeatedly explaining your standards in every conversation, you can create Skills that embody them and can be useful across many different use cases. Here's one that describes standards for constructive code reviews, starting with a prompt that can be used to generate it:

```
Create a Claude Code skill document for code reviews based on our team's standards in CODING_BEST_PRACTICES.md. It should cover evaluation criteria and include a review checklist.
```

{% capture code_review_standards %}
{% include snippets/code-review-standards.md %}
{% endcapture %}
{% include expandable-code-block.html content=code_review_standards lines=10 %}

The metadata at the top is read by the agent at the start of a session, which prevents it from loading the whole thing prematurely into context. Instead, it will be invoked automatically when relevant. This is called **Progressive Disclosure**. The coding agent always knows which skills are available and can use them efficiently.

A couple of things to consider to help you write strong Skills:

* Skills are appropriate for code review standards, reference materials, complex workflows, detailed examples, and even executing scripts. 
* Resist the urge to create Skills for every minor variation of these things and focus on reusable patterns. Creating too many similar Skills increases the maintenance burden and it isn't necessary.

### Sub-agents

Sub-agents are specialized agent instances that have particular Skills loaded and follow a structured workflow to accomplish tasks. They act as domain specialists that can be invoked as needed and load only relevant information as context. The following agent is designed to leverage our `code-review-standards` skill to perform a thorough code review workflow step-by-step and leave constructive feedback. It also contains templates to be used when it comments on a Pull Request!

```
Create a Claude Code sub-agent document for conducting code reviews. It should use the code-review-standards skill, follow a step-by-step workflow (understand the change, review structure, apply standards, detect issues, generate feedback), and include comment templates for both minor improvements and significant issues. Base the standards and feedback patterns on CODING_BEST_PRACTICES.md.
```

{% capture code_review_agent %}
{% include snippets/code-review-agent.md %}
{% endcapture %}
{% include expandable-code-block.html content=code_review_agent lines=10 %}

Beyond the example of a code reviewer, Sub-agents are well-suited for a number of workflow automations such as planning, implementation, testing, deployment, and probably anything else you want to delegate to the agent.

Unlike skills, Sub-agents are invoked through human interaction for which there are three main triggers:
* Direct Task Assignment (i.e: "Perform this task...")
* Context-Triggered Activation (on mention of keywords)
* Workflow Handoffs (triggered by other sub-agents)

### What goes where?

Since we're just working with markdown files here it would be easy to introduce unwanted overlap between Skills and Sub-agents. This might cause some of your intended instructions to be ignored, or could cause the agent to do the wrong thing. For these reasons we should be clear about what kind of instructions belong in a Skill vs a Sub-agent.

A good way to mentally separate the two would be to consider that Skills are for knowledge, and Sub-agents are for executing tasks in specific use cases.

| Skill | Sub-agent |
| --- | --- |
| Standards and criteria | Task orchestration |
| General workflows | Output templates |
| Reference material | Which skills need to be used |
| Evaluation frameworks | Context-specific processes |

## Progress and Caution

This could mark a significant tooling change for your team, and as such I recommend going about it slowly and systematically. Start small by using one or two skills before expanding into new and exciting territory. Validate outcomes and measure impact so you can refine how your skills and agents produce output that align with your team's vision. Ensure team members are on board with this new transition and understand how to use Skills and Sub-agents to their advantage. Open the door to feedback and keep iterating.

Maintaining oversight over agent behavior is incredibly important because agents cannot be safely used as a replacement for human judgement when it comes to critical decisions. Where necessary, establish a pattern of checkpoints with agents to bring a human into the loop. Make sure the agent is instructed to stop and wait for human intervention in places where you don't trust it, regardless of its confidence.

If you plan on running the agent autonomously or with minimal supervision you should consider tailoring its security settings to limit which tools, commands, websites, and files it can access. Many agents have a `settings.json` file that enables you to configure exactly what the agent can and cannot do. You may even want to configure it to run in sandbox mode to isolate it from the computer running it, just in case you're doing something a bit risky. After all, there is a non-zero chance that the agent will delete your entire disk contents without asking.

For the same reason why you should consider limiting which websites the agent can access, it is **not recommended** to leverage publicly available Skills repositories without reviewing the skills documents thoroughly by yourself. Automatically downloading and running Skills poses a very serious risk of malicious prompt injection that could lead to destruction or data theft.

## Conclusion

I think what we have at our disposal with the latest coding agents has the potential to make our everyday lives as software engineers a lot easier, but it needs to be executed with a well-formed strategy and a healthy dose of caution. There is significant risk in allowing numerous contributors to dump thousands of lines of inconsistent slop into your codebase, and a good way to combat that would be to build a series of Skills and Sub-agents that reflect your values, principles, and practices.

Building systems like these collaboratively and with intent feels to me like it could define what the future looks like for the software industry. It has the potential to fundamentally change how we've been doing our jobs for decades now. Perhaps our roles will be hoisted up by another abstraction layer; no longer writing code, but orchestrating and refining layers of automation to meet desired outcomes through markdown files.

These are interesting times, and maybe a little bit scary. At the very least I hope you find some joy in learning how to use these incredible new tools and can use them to make your life a bit easier. As always, do what works and have fun!

## Further Reading

[^1]: Kent Beck and Cynthia Andres, _Extreme Programming Explained: Embrace Change_, 2nd ed. (Boston: Addison-Wesley, 2005)
[^2]: "Agent Skills", Anthropic PBC, https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview