---
layout: post
title: "Building the Oppia Learner Dashboard"
subtitle: "A Personalized Hub for Long-Term Learner Engagement"
date: 2017-09-07 10:00:00 -0800
categories: [projects, open-source]
tags: [full-stack, open-source, education, gsoc]
excerpt: "A foundational project for the Oppia Foundation during Google Summer of Code 2017 to build a centralized dashboard, enhancing user retention and creating a personalized learning journey."
author: Arunabh Ghosh
toc: true
toc_sticky: true
feature_type: project
featured: true
---

## The Problem: A Disjointed Learning Experience

Online learning platforms often excel at delivering content but struggle with a more subtle challenge: **long-term user engagement**. Before 2017, the [Oppia Foundation](https://www.oppia.org/){:target="_blank"} faced a similar issue. While learners could consume individual lessons ("explorations"), there was no central, personalized space for them to manage their journey.

This created a disjointed experience. Progress was difficult to track, valuable feedback from creators was easily lost, and there was no simple way to bookmark interesting lessons for later. Without a personal "home base," learners were less likely to build a lasting relationship with the platform, hindering Oppia's mission to make learning effective and enjoyable.

## Our Solution: A Centralized Learner Dashboard

As part of [Google Summer of Code](https://summerofcode.withgoogle.com/){:target="_blank"} 2017 (selected with a 7% acceptance rate), I designed and built the Learner Dashboard from the ground up. This project introduced a personal space that consolidated all learning activities into one intuitive interface, built around four core features:

### 1. Unified Progress Tracking

We implemented a robust backend system to automatically track every learner's progress. The dashboard visualizes completed and in-progress explorations, allowing users to seamlessly resume exactly where they left off.

![Learner Dashboard Progress Tracking](/assets/images/posts/2017-oppia-learner-dashboard/learner_dashboard_progress.png)
*The dashboard displays learners' ongoing and completed explorations in an organized list*

### 2. Creator Subscription & Updates

To foster a community, we built a subscription system. Learners can follow their favorite content creators and receive notifications directly on their dashboard when new explorations are published, bridging the gap between creators and their audience.

### 3. Integrated Feedback Management

Previously, feedback threads were scattered across the platform. We centralized them in the dashboard with:
- Clear visual indicators for unread messages
- Direct response capabilities from the dashboard
- Thread organization by exploration

This ensures learners never miss valuable advice and can "close the loop" on their questions efficiently.

### 4. "Play Later" Bookmarking

To help learners plan their educational journey, we added a "Play Later" feature with:
- One-click bookmarking of explorations and collections
- Personal learning queue management
- Drag-and-drop reordering functionality

![Play Later Feature](/assets/images/posts/2017-oppia-learner-dashboard/learner_dashboard_play_later.png)
*Learners can bookmark explorations to create a personalized learning queue*

## Key Innovation

The dashboard's architecture combined several technical innovations:

1. **Scalable Backend Design**: Built with Python and [Google App Engine](https://cloud.google.com/appengine){:target="_blank"}, utilizing Map-Reduce for parallel processing to support millions of learners
2. **Real-time Synchronization**: Using [AngularJS](https://angularjs.org/){:target="_blank"} for dynamic updates without page refreshes
3. **Modular Component System**: Reusable components that could be extended for future features
4. **User-Centered Design Process**: Extensive user interviews and iterative design refinements

## Impact & Results

The Learner Dashboard delivered both immediate and long-term benefits:

**Enhanced User Experience**: By centralizing all activities, the dashboard dramatically reduced friction and made managing one's learning journey effortless.

**Improved Learner Retention**: Providing a personalized and persistent space significantly boosted learner motivation and retention through features like progress tracking and contextual prompts.

**Foundation for Future Innovation**: The scalable infrastructure established robust patterns for:
- Personalized recommendation systems
- Advanced learning analytics
- Adaptive educational experiences
- Community features and social learning

## Project Details

- **Program**: Google Summer of Code 2017
- **Organization**: [Oppia Foundation](https://www.oppia.org/){:target="_blank"}
- **Project Title**: Learner Dashboard
- **Mentors**: Sean Lip, Jared Silver, Rachel Chen
- **Status**: Successfully completed and passed all evaluations
- **Official Link**: [GSoC Project Page](https://summerofcode.withgoogle.com/projects/6713336413552640){:target="_blank"}
- **Repository**: [Oppia GitHub](https://github.com/oppia/oppia){:target="_blank"}

This project remains one of my most impactful open-source contributions, directly improving the learning experience for thousands of students worldwide while establishing critical infrastructure for the platform's continued growth.
