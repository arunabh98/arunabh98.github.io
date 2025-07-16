---
layout: post
title: "Network Endpoint Entity Resolution Patent"
subtitle: "Automated Device Identity Resolution for Large-Scale Networks"
date: 2023-10-24 10:00:00 -0800
categories: [projects, patents]
tags: [patents, networking, security, entity-resolution, arista-networks]
excerpt: "A patented system that automatically resolves device identity ambiguity at scale, enabling precise security policies without manual configuration."
author: Arunabh Ghosh
toc: true
toc_sticky: true
feature_type: patent
featured: true
---

## The Problem

Modern networks face a fundamental challenge: the same device appears under different names to different systems. When a smartphone connects to a network, one fingerprint parser might identify it as "android os," another as "sony android," and a third as "xperia E6653." 

This creates serious problems for network security and management. How do you write security policies or detect threats when you can't even agree on what to call a device? Today, this requires manual effort to map these different labels together—a process that doesn't scale to enterprise networks with thousands of devices.

## Our Solution

This patent presents an automated system that solves entity resolution for network endpoints. Here's how it works:

1. **Multi-Parser Collection**: When a device connects, we extract its network fingerprint from packet headers and send it to multiple fingerprint parsers. Each parser returns its own set of labels for the device.

2. **Entity Resolution**: We identify which labels from different parsers refer to the same entity using:
   - String similarity metrics (cosine similarity, Jaro-Winkler distance)
   - Substring detection (recognizing "linux" is less specific than "debian-linux")
   - External validation via web search engines and online encyclopedias

3. **Voting Algorithm**: The system scores each candidate label based on:
   - Agreement across multiple parsers
   - Specificity (more detailed labels score higher)
   - Similarity of associated web search results
   - Whether different labels resolve to the same encyclopedia article

The highest-scoring label becomes the unified identity for that device.

## Key Innovation

The system combines deterministic string algorithms with external knowledge sources to achieve accurate entity resolution. By querying web search engines and encyclopedias, it understands relationships between labels that simple string matching would miss—for example, that "xperia" and "sony android" are related because Xperia is a Sony product line.

The architecture uses a master database with publish-subscribe updates to leaf switches, ensuring consistent device identification across the entire network. This enables precise security policies and threat detection tailored to specific device types.

## Patent Details

- **Patent Number**: US 11,799,882 B1
- **Filed**: May 26, 2022
- **Granted**: October 24, 2023
- **Inventors**: Arunabh Ghosh, Debabrata Dash
- **Assignee**: Arista Networks Inc.
- **View Patent**: [Google Patents](https://patents.google.com/patent/US11799882B1/)

This technology transforms device identification from a manual, error-prone process into an automated system essential for modern network security and management.
