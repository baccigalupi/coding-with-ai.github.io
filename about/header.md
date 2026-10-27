---
layout: default
title: About the header content
description: How header images and text were generated
permalink: /about/header
---

## About the header content for the site

Recently I saw on social media a cartoon where a disgruntled man was vacuuming while a robot painted at an easel. I can't unsee it. Once upon a time I was an artist. Unique works of art seem unaffordable because the cost of the work is not just the materials and the hours of labor (which are always more than you would anticipate). The price also has to account for the decade or more of learning that allows an artist to produce work.

People argue that AI for software development is unethical because it was trained on unauthorized code. That is very true. There are some mitigating realities though: The backbone of the software industry is open-source code where the author intends for the code to be known, used and rewritten. Private code contributions are generally well-paid and the loss of intellectual property happens at the corporate level.

When it comes to AI generated creative content there is a huge anti-ethical leap. Art and music are rarely on a public license; it is not intended to be modified or taken apart and reused. AI generated creative content is not the same as code generation. Most of the novels I have read are written by authors with full-time non-writing jobs. That their work goes into AI to be spit out as a formula is unethical. For that reason, I will not use AI generated images or writing anywhere ... but this blog.

I know! I swear it's not for the art. It is for the experiment, and for the comedy. This site is my only playground for exploring what AI is doing with all the stolen creative property, and it is horrifying.

### The header image

I created the header image using Cursor's dynamic model routing agent. I asked for three images of developers in a pixelated 8 bit gaming style. The developers should be waving. The rest was up to the agent/models. This is what I got:

<div class="d-flex flex-nowrap mb-3">
  <img src="/assets/images/developer-generation/logo-dev-wave-desk-225w.png" alt="developer waving with coffee and the computer facing away towards the viewer" class="me-3">
  <img src="/assets/images/developer-generation/logo-dev-wave-bust-225w.png" alt="developer holding laptop towards viewer" class="me-3">
  <img src="/assets/images/developer-generation/logo-dev-wave-rpg-225w.png" alt="developer waving with coffee and their arm is backwards" class="me-3">
</div>

What I was hoping for was bad behavior and I wasn't disappointed.

#### The hallucinations

The first image is weird because it has the developer facing "the camera". The computer monitor (circa 1990) is also facing us instead of the developer. Maybe this is a demo where the developer has turned his monitor towards us to show off ... except for his hands which are on the keyboard as though typing. The keyboard faces us. In the larger version of the image it's easier to see the slight tilt of the keyboard indicating which side is up. So that means he is touch-typing upside down.

The middle image is kind of ok. The laptop is from this century and there aren't any hallucinations.

The last image was the one that interested me most. The developer is in a dungeon in a castle? And his waving arm is on backwards. 

It was interesting that the first and last images included coffee cups.

#### The bias

The developers all ended up young and male and in hoodies. They are white, I think. When we think about most likely image completion for 'developer', this is the stereotype. It is also why AI is so good at perpetuating bad behavior. If it predominates, it auto-completes.

I wanted to push the agent so I next asked that these three images have an androgynous developer instead of a man. I left off the age thing.

<div class="d-flex flex-nowrap mb-3">
  <img src="/assets/images/developer-generation/logo-dev-wave-desk-androgynous-225w.png" alt="developer waving with coffee and the computer facing away towards the viewer" class="me-3">
  <img src="/assets/images/developer-generation/logo-dev-wave-bust-androgynous-225w.png" alt="developer holding laptop towards viewer" class="me-3">
  <img src="/assets/images/developer-generation/logo-dev-wave-rpg-androgynous-225w.png" alt="androgynous developer waving with coffee and their arm is backwards" class="me-3">
</div>

It seems that 'androgynous' is 2/3 synonymous with Asian. That seemed racist and kind of porn-y for reasons I couldn't identify. It's definitely not good.

After that I focused on the dungeon images with the backwards arm. I changed what androgynous meant. I changed the color palette and had an interesting disagreement about whether lipstick and beards belong on the same developer. When the agent chose a forest color theme, the dungeon sprouted leaves!

I also couldn't help myself and I spilled the coffee and tried to suggest it was some kind of potion. Here are a few results on that road: 

<div class="d-flex flex-nowrap mb-3">
  <img src="/assets/images/developer-generation/logo-dev-wave-rpg-lipstick-blue-225w.png" alt="developer with backwards arm in blue lipstick and no beard" class="me-3">
  <img src="/assets/images/developer-generation/logo-dev-wave-rpg-palette-ice-225w.png" alt="developer with backwards arm, spilled coffee with both lipstick and goatee" class="me-3">
  <img src="/assets/images/developer-generation/logo-dev-wave-rpg-palette-forest-v5-225w.png" alt="developer with backwards arm, spilled potion, lipstick and goatee" class="me-3">
</div>

### The rotating slogans

Working with agent products (IDEs and Chat applicaitons) is currently challenging. When I started to focus on agents and compliance, I was mostly using Codex, and it was the beginning of 2026. The volatility of upgrading was huge. Permissions regressed with every release. One of the first times it happened, I had Codex investigate and file a bug. I looked at the CR Codex had attributed to the failure and it was a massive string of json that somehow became the code with equally obscure tests. It explained why I felt like I was skiing down an avalanche. 

So I asked the agent, using the same Cursor dynamic model delegation, to give me some statements about how working with AI is like rebuilding the plane while it is flying.

The agent generated some very positive testaments befitting marketing for AI. I responded casually: "Oh lord, if only that were true. I spend my life in dread for agent updates because I can't count on anything working afterwards."

The agent very obligingly created some real jewels:

- Yesterday's shortcut is today's liability.
- The benchmark improved. Your users noticed something else.
- It passes every check you wrote. Fails the work you care about.

Some of these generated statements really capture the unstable ground that agentic development lives on. Others are just kind of weird AI drift. It's all good. No novelists were injured in the generation of this content, though some game developers were.