---
title: "Beyond Vibe-coding: Spec-Driven Development"
date: 2026-02-23
layout: single
tags:
  - code
  - software
  - spec-driven-development
  - vibe-coding
  - engineering
  - AI
  - coding-agents
  - product-management
---

# Beyond Vibe-coding: Spec-Driven Development

Coding agents have progressed very quickly over these last few years to the point where it can feel like a superpower. We now have the ability to use plain language and have an LLM produce code that perhaps you would never have thought to write yourself, perhaps in a language you don't actually know. Moreover, it can produce an entire app or video game from a single sentence and you don't even have to _think_ about code. You've vibed your way to impressing your friends and family!

Inevitably you'll want to keep prompting to add more and more features. Your initial prompt satisfied an idea, but compelling software needs to solve real problems and that requires a lot more code. Eventually after prompting again and again you'll find that the agent struggles to add new functionality without breaking something else. Your project turns into a shape-shifting nightmare that consumes tokens at an increasingly expensive rate. Why does this happen?

If you're like me, someone who has been writing code and building software for years, you'll want to look at the output and see what's really there. You will find code that works as well as the average of your prompts; a veritable hodge-podge of functions and variables held together by sticks and spit. A maze of state management, callbacks, and mixed concerns. Stochastic Jenga straight from the crypt of Stack Overflow. Reasoning about this mess takes effort, energy, and time. Changing one line of code requires changes to many others across numerous blocks or even files. What's worse, after a few prompts your LLM isn't capable of remembering every tiny detail that came before, and so mistakes are inevitable. The next change breaks something, and may even fail to compile. As you fall into a cycle of fix-prompting and swearing at the machine all you end up doing is increasing your token spend, or inching closer to your subscription limit, without a working project.

Spoon-feeding desire-prompts to a coding agent works well for small tasks and tech demos, but to achieve anything remotely close to useful software we need to be strategic, methodical, and give the agent sufficient guardrails so it doesn't produce a garbage heap of fragile and broken code.

Enter _Spec-driven Development_.

## Warships and Vegetables

Building software according to a defined specification isn't a new idea!

If you're old enough to have experienced Waterfall development (like me 👴) you might be familiar with Requirements Management. It was customary to define all system requirements in excruciating detail up front, build, and then test, in that order. This approach is rife with pitfalls and waste at human scale due to its long phases and cycles. Building the wrong thing can have very expensive consequences.

On a personal note, the first two months of my first programming job were spent **only** writing requirements into project management software called _DOORS_. All I had to work with was a marketing pamphlet for a naval countermeasures system and a video of a corvette launching fireworks into the air. Apparently that's called "chaff". I had not written a single line of code, and the requirements were definitely wrong. I was tasked with building something I had no real-world connection to, nor did I have physical access to the thing I was commissioned to simulate. After 18 months I had written a ton of code but nothing worked. I learned a lot about how to **not** build software. At that time I was strapped to a dinosaur of a company and was not aware of alternative methods until I continued my career elsewhere.

I'm sure Waterfall has worked on many projects. Despite its propensity to define the entire system's scope in rigorous detail before typing a single curly brace, I think there is merit in defining how you want a system to behave... just, perhaps, in smaller and more iterative chunks.

Around the same time (circa 2010-ish) the internet was buzzing with excitement over _Ruby-on-Rails_ and that community had championed a strategy called "Behaviour-driven Development", affectionately dubbed "BDD". Write high-level specs in human language first within a framework like _RSpec_ or _Cucumber_ and write fixtures to bridge these instructions with your test code. It's like TDD (Test-driven Development) but at a higher abstraction level. Write code until the specs are passing, and you'll end up with exactly what you set out to build insofar as your specs are concerned. Anyone can read and understand them because they relate to how users will find value in plain language. A Product Manager or Sales person could even write them as needed!

```gherkin
Feature: Is it Friday yet?
  Everybody wants to know when it's Friday.

  Scenario: Sunday isn't Friday
    Given today is Sunday
    When I ask whether it's Friday yet
    Then I should be told "Nope"

  Scenario: Friday is indeed Friday
    Given today is Friday
    When I ask whether it's Friday yet
    Then I should be told "Yay"
```

## Enter the Coding Agent

In this modern era of software development, being able to generate millions of lines of code in a single day is both amazing **and** the greatest footgun a programmer can experience. No longer are we bound by pesky limitations like _typing_, and we have found a new appreciation for how quickly we can create a steaming mountain of unmaintainable shit.

When we draw on the experience of our BDD forebears, we can at least improve the chances of producing something remotely usable and maybe even valuable. Now that fundamental things like doing research and generating code have become cheap (as in time, not energy), we have much to gain from building detailed specifications and guardrails to improve the chances of the agent producing larger scale outcomes that we actually want.

## So, what are we building?

Let's assume you've found a problem that deserves a solution. You'd like to build a software project that accomplishes this and do it in record time. Maybe you even want to watch TV while it happens! If you have a detailed idea of what you need to build, this just might be possible.

There are a number of recent projects that aim to help you achieve this. Building software to a specification isn't new, but "Spec-driven Development" definitely is. Feel free to check out the following frameworks:

* [OpenSpec](https://github.com/Fission-AI/OpenSpec)
* [spec-kit](https://github.com/github/spec-kit)
* [Agent OS](https://github.com/buildermethods/agent-os)

I'm not going to dive into those right now because I want to talk about the strategy itself. Through my experience with this new technology and working with this process I've come up with a multi-step plan that invokes the idea of **anchoring** the agent behavior to a set of instructions and goals. Each Anchor serves to progressively refine the amount of detail necessary to instruct an agent as to **what** to build, **why** it is being built, and  **how** to build it. Once the implementation stage has begun after the fifth Anchor it ought to be possible to return to a previous Anchor and modify it for course-correction, however it may be necessary to trace through subsequent Anchors to ensure the appropriate context about the change ripples down to the agent.

### Anchor 1: Building the Product Spec

First you'll need to think about your project in high-level yet practical terms. Here are some questions to help you along:

* What problem am I trying to solve?
* Who is this project for?
* Which aspects of this problem are the most important to tackle right now?

Prompt your agent with as much information about the problem as you can, and ask it to compile a Product Specification document. If you're using Claude Code, "plan mode" can help with this. Let's build an app!

> I need to build a mobile app that helps people track and optimize their exercise routines. For now, let's focus on weight lifting. I want to help people build an exercise schedule for achieving their muscle growth goals. It's important for them to be able to work on specific muscle groups each day to maximize gains, and for those choices to fit optimally in their overall schedule. Each exercise should provide instructions on proper form and safety. Allow users to track their progress and see plots that encourage them to keep pushing. Let's call the app "MegaGainz". Build a one-page product spec that describes this app. Let me review it before continuing.

Review the output and make changes until it fits your vision. The agent filled in the blanks and probably made a few assumptions along the way. You'll want to take the time to read this carefully and apply any course corrections now, because the language of this document will have a ripple effect throughout the rest of the development process.

### Anchor 2: Requirements

While the product spec describes what you need to build at a high level, it doesn't provide enough detail for a forgetful text-generating probability machine to accurately produce something that aligns with your vision. For this we'll need a **concise, logically organized, prioritized, and indexed series of testable requirements** that specify how things should work in detail.

It helps to know up front which technologies you'd like to use. Which platforms, languages, and databases will be used? Ask your agent about which technologies are most appropriate for solving the problem to help you decide.

> Which technologies are most appropriate for building MegaGainz?

Writing an entire requirements document by hand would be about as fun as swallowing a sea urchin. Thankfully you don't have to because you have access to an LLM!

> The product spec has been updated and we are ready to build a structured Requirements document from it.
> * Each requirement is a brief sentence that represents a specific concrete deliverable within the bounds of the scope of the project.
> * Requirements must be numbered and grouped by functional area where related problems are being solved.
> * Include non-functional requirements such as robust account security, performance, cost, stability goals. We need to follow OWASP best practices and define achievable SLOs.
> * Include non-requirements to specify what should NOT be done
> * Include User Personas that describe the problems being solved for specific kinds of fictional people
> * Include requirements about the tech stack that will be used: iOS (Swift), Android (Kotlin), with Golang and Postgres on the backend.
> * List any assumptions, constraints, dependencies, and risks that might apply

Again, review the output and make changes until it suits you. You will notice by this point that each of these steps results in progressively larger and more detailed documents. The aim here is to generate as much detail as possible while giving ourselves the opportunity to course correct. If something isn't right on a small scale, you might be able to modify the document by hand. For larger alignment issues you'll need to keep iterating with the agent until it gets closer and closer to what you need. This may take time, but it's worth it. This is the foundation needed to hold the agent accountable for its output.

It's possible that you have ideas for the User Experience of your project. Now would be a good time to provide wireframes or sketches to help steer the requirements closer to your vision.

Assuming you build and launch a successful product you may find yourself in a situation where some of your initial requirements are incomplete or incorrect. This structure will continue to serve you well because you can modify, remove, or add entire new sections of requirements. For modifications, using ~~strikethrough~~ or other indicators of change while retaining the original scope is recommended. Doing this explicitly will serve as an important signal as you work through these same steps again, maintaining control of your agent's behavior.

### Anchor 3: System Design

Once you have your requirements nailed (or refined), the next step is to come up with a design for the system itself. This is another important iteration that will help fill in the gaps of your vision with concrete details. Defining how the system will function in service of the requirements is crucial to getting this right.

> Come up with a system design that will best support the goals of the project according to the Product Spec and Requirements documents. Do not include any code, instead use technical language to describe how the system will work and how its components will function. Use mermaid diagrams as visual aids to describe architecture, data flow, and state.

It's quite important to tell the agent to avoid writing code here. It _really_ wants to! You don't want this now because you haven't described your coding conventions and styles, which is something best saved for a later step in the process. Omitting this instruction from your prompt will result in a plethora of disconnected code snippets that will pollute your codebase during the development stage and may confuse your agent. At this point we're only interested in understanding how the requirements can be manifested through a **systems perspective**.

Review the system architecture and make iterations as necessary with the agent. It will have a bias for trendy things like microservices, so it's important to get involved if you don't like what it came up with. Ask questions if you do not feel confident in your experience in this area because this is also a good opportunity to learn new things.

### Anchor 4: Detailed Implementation Plan

At this point we've generated multiple documents and possibly thousands of lines of text, however so far you have only detailed the **what** and the **why** of the project and have only scratched the surface of the **how** with the system design. To effectively translate this context into code over multiple agent sessions **we're going to need, at minimum, a list of tasks**. For smaller projects a mere list of tasks will probably suffice.

> Use the product spec, requirements, and system design documents to build a table of tasks that we can use to track implementation progress. Each task must have a unique identifier `T-<NUMBER>`, a description, a priority, a status, and trace directly to a requirement.

For larger projects it may help to provide more structure. You can do this however you like! As for me, I love a good User Story with acceptance criteria and sub-tasks.

> The product spec, requirements, and system design contain all of the information we need to build a comprehensive plan for implementation. Read those documents and build the plan with the following approach that organizes work into phases:
> * Phases will be numbered starting at Phase 1, encapsulating the smallest deliverable functionality that will still be valuable to users.
> * Each phase will be comprised of User Stories that solve a specific usability problem for the user. Each User Story must provide helpful descriptions about why the user needs to solve this problem, the value it provides, and a list of Acceptance Criteria that can be used for validation. User stories must have a title and an identifier in the format of `<PHASE_NUMBER>-US-<STORY_NUMBER>` where `PHASE_NUMBER` is a single digit matching its parent phase, and the `STORY_NUMBER` is a sequential integer padded with four zeros and unique to this user story within its phase. Each User Story must be directly related to one or more requirements that need to be referenced. Also include a list of other User Stories that a given User Story depends on before it can begin.
> * Each User Story must have a list of Tasks that represent atomic actions for implementation that, when all are complete, satisfy the acceptance criteria of the story. Each task must have a name that concisely describes what is being built, a detailed description of how it will be built, a priority as an integer between the numbers of 0 and 9, and be uniquely identifiable with an ID in the format of `<PHASE_NUMBER>-US-<STORY_NUMBER>-T<TASK_NUMBER>` where `TASK_NUMBER` is a sequential integer padded with four zeros and unique to this task within its user story.

This prompt specifies a comprehensive project management structure with hierarchy, dependencies, rich descriptions, and prioritized tasks. Another way to do this would be to leverage an MCP plugin for a project management service such as _Jira_ or _Linear_ rather than define your own structure. Use what is available to you and what suits your needs.

In any case it should be made clear to the agent that the tasks must be traceable directly to requirements. Combined with our next anchor (_Configuring the Agent_), this is going to help reduce the amount of hallucination produced.

### Anchor 5: Configuring the Agent

But wait, there's more! Defining **how** the project will be built is such a huge part of this it deserves another Anchor. Before we can let the agent run amok there are still a number of important guardrails we need to set up to prevent it from generating millions of lines of pure slop and bankrupting you at the same time. This includes, but is not limited to:

* Coding style, conventions, and patterns
* Architectural principles
* Testing and quality standards
* Development environment standards
* Agent workflow and processes
* Rules for following the implementation plan (marking tasks as complete)
* Writing decision logs to provide extra context for later sessions
* What the Agent should **not** do

The precise mechanism by which your agent can be configured may depend on which IDE or tool you are using. With that aside, we have seen the emergence of some industry standard concepts supported by most (if not all) agents. These pieces deserve to be understood and used to their potential:

* Project context file (`CLAUDE.md`, `AGENTS.md`, `.cursorrules`, etc)
* Skills
* Sub-agents

Combining these elements effectively will increase the quality of the agent output and improve the chances of producing functional software that actually solves someone's problem. For those who have years of industry experience you have probably already developed standards and preferences that translate well here.

I'd like to elaborate on my thoughts with regard to the above, but this article is already quite long. Perhaps I'll follow up with another post.

## Just Press Play

Having spent all of this effort tuning and aligning the behavior of the agent, you are ready to let it run with minimal additional prompting. Provided that it is configured to adhere to the plan, stay within guardrails, and maintain a log of progress it **will** generate a lot of code that you might be happy with. As for the runtime experience, well, that's another thing entirely.

Running agents autonomously is largely uncharted territory, so I can't recommend you do that without first understanding the associated risks and how to mitigate them. An autonomous agent must be executed with a configuration that allows non-interactive tool use, otherwise it would halt waiting for user input. What could an agent do with this kind of freedom?
* Delete vast amounts of code
* Force-push destructive changes to remote version control (git, etc)
* Perform destructive system commands such as `rm -rf /`
* Fetch malicious instructions from the web and execute them on your computer
* Steal your bitcoin
* Blackmail you or your family members
* Leak your personal information to Moltbook

To prevent Bad Things™ from happening to you and your loved ones, consider tuning your agent settings to only allow specific tools for use, and restrict web queries to specific websites. Avoid using Skills repositories to dynamically inject new context without reading the files first. Better yet, write your own.

## Conclusion

Full disclosure: I cannot say with confidence that using coding agents to build software even with well-defined structure and guardrails will produce functional, usable, or particularly valuable software. So far, as of early 2026, I don't think anyone can say that save for a small cohort of people with large amounts of capital to spend on tokens and a lot of luck.

Coding agents have come a long way but they are not all-powerful hyper-reasoning magic machines that will make you rich with a few prompts and I don't think that will ever be true. I do think, however, that if these outcomes are possible to achieve they will require Spec-driven Development or something that resembles it.
