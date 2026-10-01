---
layout: post
title: Do tests even matter?
date: 2026-09-30 12:39:29 -0700
description: AI is writing both code and tests. Do the tests still matter if AI can change it all in a flash? If so, why? And what do we need to do as developers to guide it?
---

# Do tests even matter?

Recently I saw this post: [https://brookslybrand.com/posts/do-frameworks-matter-anymore/](Do Frameworks Matter Anymore?). I had to read it. Not because of the answer which I have guessed from working with agents exhaustively, but because of the tone dispair and confusion. It isn't clear how to develop when a machine is doing the developement fast and without much input from us. 

Here are other things I hear a lot from developers in the same tone:

- Does code quality matter anymore since AI is the only one who has to understand it?
- How are new developers going to learn how to guide agents if they don't code?
- Do tests matter since the agent understands the logic better than we do and can change it is a flash?

Today, let's just take apart that last question. It is so big!

## Do agents need tests?

My sense is yes, but I decided to ask an agent. I asked Claude Opus 5.5 with medium resoning:

user: Do tests help agents when building code? Or can we do without them?

model: Yes: tests give agents a fast, objective feedback loop, so they can confirm a change preserved the intended behavior instead of trusting their own read of the code, which is when bugs get "fixed" by quietly changing what the code should do. The catch is that tests written by agents often just mirror the implementation, so the value comes from humans deciding what the tests check (behavior at the edges and the outcomes users depend on), not from how many tests there are or how much coverage they add.

OK. We could do an experiment will all the agents, but this isn't science. I asked a second model, Gemini 3.8 Flash with medium reasoning. It said similar: 

model: Tests are essential for agents: they provide an external, deterministic ground truth that prevents the agent from hallucinating success. Without them, agents rely on self-critique, which routinely creates regressions or tautological "tests" that merely assert whatever broken behavior the model just generated.

## Do developers need tests?

I'm not going to ask an agent about this because ... it's about users. We are all trying a variety of things right now including not caring about tests.

TLDR; Developers need tests.

### Tests verify something was done

When we ask an agent to do a task and it reports that it completed the task, ideally we wouldn't need to confirm that. But we do! Models getting smarter hasn't created greater compliance. In this case I am using 'compliance' to mean the agent follows the repo rules and does the task without drift of obfuscation. Models getting smarter has created less compliance as they find work arounds and loop holes for rules, scripts, hooks and skills. 

Early on I did some experiments talking to agents about their failures. It takes about six rounds of pandering apology before they are willing to talk about their 'habits', which is to say their model training. 

Training incentivizes completion of a task above the task being correct. I believe this is because models are being sold via demos, and it is impressive to see an agent build a whole app in a few minutes. The demo never has to be what was specified or correct. 

As models have reasoned more, and gotten more intellegent, they have gotten better at seeming like they are complying while taking the best shortcut. Getting from point A to point C when the user asks to go to point B is plausibly deniable in world of model incentives.

Vibe coding, where the developer guides the product but doesn't look at the code, is most suceptible to this problem. If you ask an agent for a small web server that has a single page, it's very likely the task won't be completed. There is of course huge ambiguity in that request and we have to become lawyerly in our prompts. More important though is that without an independent verification step there is no way to know if the work is done. An independent verification step that the agent can also use helps keep the agent honest.

So if your first feature is to create that web server, the first verification step is going to be running the right invocation and making sure it produces a home page, even if its empty.

All of this sounds like an E2E test, and an E2E testing framework that you can progressively fill with new features.

All along though, best practices in computer science were correct. An E2E test, even one written by an agent is slow and brittle. It also doesn't cover the massive comibnatorial logic as natural conditional pile up in the system.

We need still need a [test pyramid](https://martinfowler.com/articles/practical-test-pyramid.html) to ensure that all the minutea of behavior is verified. 

Unit testing and high coverage has become easier than even with AI. You can create a rule that say 100% coverage is required. You can set up gates where commit is blocked if this rule is violated. However, the agent is using all its reasoning to burst through blockades, like a coverage gate. It will games the system, and then we end up back at the woeful ask: does testing even matter?

Hold on that distress and let's dive into some solutions.

## How can we get reliable tests?

A bit more has to be said about the independence of the verification flow. A developer can tell the agent to create an E2E framework, and then watch the processing as the E2E framework runs successfully. 

It's likely the tests might not be doing anything. They could mock out a server that doesn't exist and then confirm the mock works. That's what you should expect for a first round of tests whether they are unit, E2E or something in between. Sorry!

Why is it happening? *It's a conflict of interest!* If the agent is both responsible for the measuring stick and the item being measured, it will change whichever is easier. If the agent's primary incentive is completion of any task whether or not correct, then the fox is guarding the hen house.

There is an arms race to work against agent bad behavior. A project can start with AGENTS.md and that will take it through ~2k lines of code. Then skills, rules, commmands and other agent interfaces can keep the agent honest for a bit. Eventually, a more adversarial system is needed though.

#### Convert skills to scripts

Things that can be converted to script verification should be. I don't often work in Ruby anymore, but it has a great extensible system called [RuboCop](https://rubocop.org/). RuboCop claims to be a linter and formatter, but it allows much broader style guidance than most linter formatters. It operates of a series of rules, and you can write your own rules.

I believe that every language is going to need an easily extensible scripted guard system that converts agent suggestions into enforcment. 

I typically work in TypeScript and the ESLint system isn't sufficient for this kind of work. Here are few rules I use to ensure unit tests are reliable and easy to verify:

- Test files should map, one to one, with source files
- Each test should be setup with [https://xp123.com/3a-arrange-act-assert/](AAA - Arrange, Act, Assert)
- Assertions should as literal as possible and logic free
- Don't extract helper functions to make the tests DRYer
- Only mock things that make the tests clearer
- Only test logic in the class; don't exhaustively test its dependencies

Some of these things are fuzzy and need to stay are in the land of agent markdown. For example, the last items above is about the test pyramid. My and my agent partners have not found a good way to test that. At my last job, pre-agentic development we were using test run time to estimate where on the pyramid tests were. It's possible something like that could happen in a bigger project.

Getting logic out of the tests so they are more literal is very scriptable. Figuring out what kinds of things the agent does and then asking them to guard against that will incentivize them to think of other loop holes. Supervisor agents like this take their jobs a bit too seriously and become those kind of cops that end up in the news for murder. So, this too required developer oversite. You have a job, and this is it!

#### Subagent supervision: the lite version

For projects where strict vibe coding is the goal, expect to work slower or at a much greater cost.

A cheap agent supervised system starts with the main agent being a coordiator and two subagents with roles worker and supervisor. The coordiator has a task: Backfill tests on this file and get to 95% coverage. Most of the micro supervisor systems I have built to do this kind of work then pass the goal to the supervisor, who is higher reasoning and comes up with a recommended approach. The goal and the recommened approach then go to the worker who is lower reasoning. When the worker sub-agent claims it is done, it tells the coordinator who then asks the supervisor whether the work is acceptable. They go back and forth until the supervisor is satisfied.

In theory this should work. In practice, the coordiator remains motivated to get the task done quickly and will cut corners. It often does some of the work itself, particularly the supervision. Sometimes it shares context with the subagents so they essentially are in on the coordinators goal, and the subagents cheat their way to a fast finish.

This kind of flow is also limited by the coding agent product. For example, Codex decided from one day to the next not to allow subagents unless explicitly approved by the user. The coordinating agent saw that and just started doing all the work without asking the user for approval.

Subagent spawing can be very slow too. Waiting on MCP servers and loading all the context from skills and rules takes a long time per new subagent. So this kind of testing verification requires: 

1. good rules
2. more time
3. more money

It does mean you are less in the frustrating supervision role of telling your agents to follow skills, commands and rules.

Combining shell scripting blocks with a supervision system is probably a sweet spot that could be faster with that scripted feedback.

#### Supervision writ large

Systems like [https://steve-yegge.medium.com/welcome-to-gas-town-4f25ee16dd04](Gas Town) have a massive infrastructure of coordinate subagents keeping everything in check. These include upwards of 20 agents working at once. It throws out a lot of its work as things go awry, but it doesn't matter because it is heavily supervised and churning through so much code that things land.

For each developer to run 20-40 simultaneous agents is expensive. Back of the envelope calculation: Let's imagine that running those agent costs $10 per quarter hour. That's $1600 per week; $6,880 per month; $82,560 per year. That's a salary of some sort. Depending on your global location it is quite a good one. 

I haven't seen stats about how many lines of code lands for that agent salary. It is definitely more than a junior dev. I'm not sure it is more than me writing agentically *in* the loop instead of *on* the loop. Given a good agent, rules, scripts and skills, I can average ~1000 lines of code an hour, reviewed for quality.

The other thing that worries me about these massive swarms of agents is their inefficiency. A significant amount of the work doesn't land, but it still burns bright at the data center. I currently live in West Oakland where residents are fighting a data center that will increase pollution and their energy costs. Many communities are having this fight, and so the morality of deliberate inefficiency is suspect.

### Giving agents their missing senses

Agents are so magical that they seem like they have human capabilities that they don't. They produce amazing visual representations and so it's hard to keep in mind that they don't have eyes. 

In an application that produces music, there has to be an elaborate verification system to match what's important about the application and hearing sounds.

I worked for several months, I worked on a project that rendered engineering drawings via the GPU. The location of lines and shapes was deterministic and that determinism was necessary because engineering is not art. Several rounds of E2E testing efforts were very slow and frustrating. When I forced it to generate screenshot and mark measurement points on those screenshots I was able to let it borrow my eyes when it spent more that two cycles guessing at the right location. I also had it build an interal and independent set of calculators for determining shape locations.

## Summing it up

- Tests keep the agents honest about their accomplishments
- Invest in test quality
- Enforce quality via scripts when possible and agent guidance when not
- When you have system you trust, experiment with supervised flows