---
layout: post
title: "Pathways: Branching AI Conversations"
subtitle: "An Experiment in Non-Linear AI Interaction for Learning and Decision-Making"
date: 2025-11-01 10:00:00 -0800
categories: [projects, ai]
tags: [ai, branching-conversations, open-source, ux-design]
excerpt: "An experimental project exploring branching, non-linear conversations with AI: enabling parallel exploration without losing context."
author: Arunabh Ghosh
toc: true
toc_sticky: true
feature_type: project
featured: true
---

Ever had a great conversation with an AI, maybe learning a new topic, and an interesting tangent pops up? You want to explore it, but it's different from your main goal. Do you follow the tangent, which can derail the primary conversation and fill the context with unrelated details? Or do you ignore the new idea and just stick to your original task? This practical trade-off is a built-in limitation of the linear, single-threaded chat interface.

## The Problem with a Single Thread

Standard chat models force you to pick one path, often forcing a choice between **focus and exploration**.

For example, imagine you're planning a vacation. You start a chat with all your context: budget, dates, and preferences. The AI suggests three options: Colorado, Savannah, or Atlanta with a Blue Ridge Mountains side trip. You want to explore all three and compare full itineraries.

You face a dilemma:

1. **Explore in one thread:** You develop a Colorado itinerary, then ask about Savannah, then Atlanta. The chat history quickly becomes a cluttered mix of information, making side-by-side comparison difficult and risking the AI conflating details from different destinations.
2. **Start separate chats:** You create three different conversations, one per destination. This keeps things clean, but you're forced to re-establish all your original context (budget, dates, etc.) every single time.

This isn't just for trip planning. Take learning, for instance. If you're learning about recommendation systems and are deep into understanding [Singular Value Decomposition](https://en.wikipedia.org/wiki/Singular_value_decomposition){:target="_blank"} (SVD) when the ["cold start problem"](https://en.wikipedia.org/wiki/Cold_start_(recommender_systems)){:target="_blank"} is mentioned - something you're also curious about - you face the same choice: either dilute your SVD context by pivoting, or start a new chat and lose your original thread.

The **linear chat interface** is fundamentally at odds with **comparative, exploratory thinking**.

## The Solution: Pathways

This frustration is what led me to build **[Pathways](https://github.com/arunabh98/pathways-ai){:target="_blank"}**, an experimental personal project for non-linear AI conversations.

Instead of a single, scrolling chat log, Pathways visualizes the entire conversation as a branching tree. You can pursue one line of inquiry, then jump back to an earlier message and click a "branch" button (⤴) to start a new, parallel conversation. Your original thread is saved, and you can instantly switch between these different contexts.

It's easier to see than to explain. I've recorded two short demos showing exactly how it works:

### Demo 1: Learning Use Case

<div class="video-container">
  <iframe title="Pathways: Learn Complex Topics with Branching AI Conversations" src="https://www.youtube-nocookie.com/embed/AoZIyKOP-ps" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
<p class="video-caption">Exploring recommendation systems by creating separate branches for "Matrix Factorization" and the "Cold Start Problem"</p>

### Demo 2: Trip Planning Use Case

<div class="video-container">
  <iframe title="Pathways: Compare Travel Plans Side-by-Side with Branching AI" src="https://www.youtube-nocookie.com/embed/h7RiUqW2bLM" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>
<p class="video-caption">Planning a vacation by comparing three different destinations (Colorado, Atlanta + Blue Ridge, Savannah) in parallel</p>

The goal isn't to replace linear chat, but to offer a new tool for specific tasks: deep learning, complex planning, and comparing fully-developed options side-by-side.

## How It Works

Pathways runs on a [React](https://react.dev/){:target="_blank"} frontend, an [Express](https://expressjs.com/){:target="_blank"} server, and the [Anthropic Claude API](https://docs.anthropic.com/){:target="_blank"}.

Instead of storing messages in a linear array, conversations are saved as a **graph structure**. Each message is a **node** that holds references to its **`parent`** (the message before it) and its **`children`** (any replies). The `currentBranch` is just an array of message IDs that defines the path you're currently viewing.

When you create a new branch, no data is duplicated. You're simply starting a new path from an existing node, which makes the entire operation instant.

For cost optimization, every message triggers two API calls simultaneously:

* **Claude 4.5 Sonnet** generates the main, high-quality response.
* **Claude 3.5 Haiku**, a much faster and cheaper model, generates a short label (max 20 tokens) for the tree visualization.

This keeps the main conversation quality high while keeping API costs reasonable.

## The Development Journey: AI-Assisted Development

This project was built almost entirely with [AI-assisted development](https://en.wikipedia.org/wiki/Vibe_coding){:target="_blank"}. The AI assistant handled most of the implementation details while I focused on the high-level plans and ensuring the overall direction was correct.

Two practices made this process effective:

1. **Detailed planning upfront:** Before writing any code, I brainstormed the overall architecture and broke it down into concrete implementation steps. Having this detailed plan meant I always knew exactly what to ask the AI to do next. Rather than rushing, I gave the AI one step at a time: implement, test, verify, then proceed. Breaking the work into smaller and smaller steps kept the AI focused and prevented it from drifting from the original plan.

2. **Writing tests first:** By creating unit tests and end-to-end tests *before* implementation, the AI could run these tests as it worked. When a test failed, it immediately knew it had gone off track and could self-correct. This drastically reduced debugging time and kept the codebase stable throughout development.

## Limitations & The Open-Source Future

It's important to be honest about what Pathways is: an experiment. It's not a production-ready tool.

All conversations are stored in-memory on the server (meaning they vanish on restart), there's no user authentication, and error handling is minimal. This simplicity is intentional: as a prototype, the goal is to clearly demonstrate the *concept* of branching interaction, without the overhead of a production-ready system.

Because this is an open-source project released under the [MIT License](https://opensource.org/licenses/MIT){:target="_blank"}, I'm excited to see if others find the idea useful. The **[GitHub repository](https://github.com/arunabh98/pathways-ai){:target="_blank"}** has all the code, and the README includes setup instructions to get it running locally quickly. Future extensions could include database persistence, side-by-side branch comparison views, collaborative features for teams exploring ideas together, or AI-powered suggestions for interesting branch points.

## The Bottom Line

Pathways demonstrates that AI conversations don't have to be linear. For complex learning and decision-making, branching is an incredibly valuable interaction pattern. What might have taken months to build was prototyped and polished in weeks (more like weekends), thanks to AI-assisted development.

The result is experimental but functional: a new way to explore, plan, and think with AI. The code is open source. I invite you to clone it, experiment with it, and see if branching conversations change the way you interact with AI.
