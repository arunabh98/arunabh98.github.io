---
layout: post
title: "Simmer: Cooking From What You Have"
subtitle: "A Quick Weekend Project That Uses AI to Find a Recipe Built Around the Ingredients in Your Kitchen"
date: 2026-09-07 07:00:00 -0800
categories: [projects, ai]
tags: [ai, recipes, search, open-source]
excerpt: "An experiment in starting from the ingredients rather than the dish: describe what you have, and Simmer searches the web, judges what it finds, and returns a dish that fits with a link to the recipe."
author: Arunabh Ghosh
toc: true
toc_sticky: true
feature_type: project
featured: true
---

Figuring out what to cook from what is already in the fridge is harder than it should be. One weekend I had some broccoli, a bunch of cashews, and a lot of mint sitting around, and I wanted to know whether there was a good dish I could make out of them.

Search isn't much help here, because it works best when you already know the name of the dish you want. Typing in the ingredients instead returns pages that mention them somewhere, not pages built around them. The constraints don't survive either: "thirty minutes", "no onions or garlic", "I don't own an oven" are the things that actually decide what gets cooked, and a keyword query drops all of them. And plenty of what does come back is written with search rankings in mind, so you scroll past a long preamble to reach the recipe, and it takes a few pages before you can tell which one is worth cooking from.

So I built **[Simmer](https://github.com/arunabh98/recipe-search){:target="_blank"}**.

## What It Does

You describe what's in your kitchen in your own words, for example *"Broccoli, some cashews, and a bunch of mint. Some Indian dish?"*. Simmer plans a set of searches, pulls in candidate pages, and judges the content of each one: whether there is a real recipe on the page and whether it looks like a good one, or whether it is mostly written for search rankings. What comes back is the dish that stands out, why it fits, what you're still missing, and a link to the recipe. If nothing usable turns up, it says so.

![Simmer's recommendation for broccoli, cashews, and mint: Malai Broccoli, with the reasoning, the missing ingredients, and a link to the original recipe](/assets/images/posts/2026-simmer-recipe-search/simmer-recommendation.jpg)
*Simmer answering a real request: the dish, why it fits, what is missing, and a link to the original recipe*

If typing all of it out is tedious, there is a camera button instead: point it at your fridge, up to five photos, and Claude turns them into ingredients you can edit and remove before searching. The images are analyzed in memory and never stored.

## How It Works

Simmer is a small [FastAPI](https://fastapi.tiangolo.com/){:target="_blank"} service backed by two external APIs: [Exa](https://exa.ai){:target="_blank"} for neural web search and the [Anthropic Claude API](https://docs.anthropic.com/){:target="_blank"} for evaluating what comes back. The flow is **plan, search, judge, adapt, recommend**.

**1. Plan.** A fast Claude call reads your request and first decides whether it is about food at all, so homework questions and random keyboard mashing get turned away before anything is spent on a search. Then it writes one to three search queries in plain language, turning what you typed into the kind of phrase that would sit next to a good recipe: "broccoli, cashews, mint, Indian?" becomes something like *"Here is a great Indian recipe that uses broccoli, cashews, and mint:"*. Exa matches meaning rather than keywords, so that phrasing finds better pages than the raw ingredient list does.

One detail took a while to get right: **negations never go into the search query**. Embeddings can't represent "not onions", so a query mentioning onions retrieves onion-heavy pages however you phrase it. Exclusions get dropped from retrieval and enforced later, during ranking.

**2. Search.** The planned queries run against Exa at the same time, and each comes back with its own list of results. Instead of stacking those lists end to end, Simmer takes the top result from each list, then the second from each, and so on, so a strong hit from the second query doesn't get pushed out by eleven mediocre ones from the first. The combined pool is deduplicated by URL and capped at twelve.

**3. Judge.** One Claude call sees all twelve at once, each with a relevant excerpt from the page, and evaluates them against your *original* words rather than the rewritten queries. For each one it decides whether the page has an actual cookable recipe on it (a list of links to other recipes, a video with no written steps, or a forum thread doesn't count), what the dish is, which of your ingredients it genuinely uses, what you would still need to buy, and how spammy it looks. Because it's one comparative call rather than twelve independent ones, it can rank rather than just score.

**4. Adapt.** If nothing usable comes back, Simmer retries once, feeding the judge's own rejection reasons to the planner so it takes a different angle instead of rephrasing the same miss. If that fails too, it returns the first honest ranking.

**5. Recommend.** A final call turns the usable candidates into what you actually read: the dish, why it fits, missing items marked *essential* or *nice to have* with a substitution where one exists, which page to follow, and a few alternatives with a line each on when you would prefer them.

One precaution worth mentioning: the links never come from the model. It refers to recipes by number, and Simmer attaches the real titles and URLs afterwards from the search results, so it cannot send you to a recipe that doesn't exist.

## Knowing Whether It Works

I added tests early, mostly so I would know when something broke. There are over a hundred now, all running offline against fakes, and they cover the mechanical things: a rate limit returns a 429, a malformed response doesn't crash the server. None of them say anything about whether a recommendation was actually any good.

For that I created an evaluation set, a script that runs a fixed list of queries through the real pipeline against live Exa and Claude, covering a range of scenarios the app should handle. Every run also writes out a detailed log: the searches it planned, whether it had to retry, and every candidate with its judgment, so I can see how it arrived at a particular recommendation.

## The Bottom Line

Simmer is a weekend project. The **[GitHub repository](https://github.com/arunabh98/recipe-search){:target="_blank"}** has the code and the setup instructions to run it locally, along with a README and an architecture doc covering every route, prompt, and failure path, so it should be easy enough to pick up, change, or contribute to.

If you do run it, throw the weird combinations at it. That is where it gets most interesting, and I would love to know what else it can cook up.
