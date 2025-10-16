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

Ever wonder why IT departments struggle to secure enterprise devices? The answer might surprise you: different systems can't agree on what to call them. Here's how one invention solves this fundamental challenge.

## The Problem

Modern networks face a fundamental challenge: the same device appears under different names to different systems. When a smartphone connects to a network, one [fingerprint parser](https://www.recordedfuture.com/threat-intelligence-101/vulnerability-management-threat-hunting/fingerprinting-in-cybersecurity){:target="_blank"} might call it "android os," another "sony android," and a third "xperia E6653": three names for the same phone. 

This creates serious problems for network security and management. How do you write security policies or detect threats when you can't even agree on what to call a device? Today, this requires manual effort to map these different labels together: a process that doesn't scale to enterprise networks with thousands of devices.

## Our Solution

This patent presents an automated system that solves [entity resolution](https://senzing.com/what-is-entity-resolution/){:target="_blank"} for network endpoints. Here's how it works:

1. **Multi-Parser Collection**: When a device connects, we extract its network fingerprint from [packet headers](https://www.cloudflare.com/learning/network-layer/what-is-a-packet/){:target="_blank"} and send it to multiple fingerprint parsers. Each parser returns its own set of labels for the device.

2. **Entity Resolution**: We identify which labels from different parsers refer to the same entity using:
   - String similarity metrics ([cosine similarity](https://en.wikipedia.org/wiki/Cosine_similarity){:target="_blank"}, [Jaro-Winkler distance](https://en.wikipedia.org/wiki/Jaro–Winkler_distance){:target="_blank"})
   - Substring detection (recognizing "linux" is less specific than "debian-linux")
   - External validation via web search engines and online encyclopedias

3. **Voting Algorithm**: The system scores each candidate label based on:
   - Agreement across multiple parsers
   - Specificity (more detailed labels score higher)
   - Similarity of associated web search results
   - Whether different labels resolve to the same encyclopedia article

The highest-scoring label becomes the unified identity for that device.

**Why This Matters**: Security threats are often tailored to specific device types. Without unified device identification, security teams cannot enforce consistent policies. A device labeled "Xperia Z5" by one system and "sony android" by another would be treated as two different devices, creating gaps in threat detection and policy enforcement.

## Example: Resolving a Sony Xperia Z5

To illustrate how the system works in practice, consider what happens when a Sony Xperia Z5 smartphone connects to the network. This example is drawn from the patent's technical specifications.

### Conflicting Parser Outputs

When the device's network fingerprint is submitted to three different fingerprint parsers, each returns a different set of labels:

![Conflicting labels from three different fingerprint parsers](/assets/images/posts/2023-network-endpoint-entity-resolution/fingerprint-parser-conflicting-labels.png)

*Each fingerprint parser sees the device differently, like three witnesses describing the same person. Parser A identifies: "linux os", "xperia android", and "lge android". Parser B returns: "sony android", "xperia z5", and "debian-based linux". Parser C outputs: "xperia E6653", "htc android", and "android os". This label diversity, with conflicting manufacturer attributions (Sony vs. LG vs. HTC) and varying specificity levels, illustrates the core identification challenge the system solves.*

### Resolution Pipeline

The system processes these nine conflicting labels through an automated pipeline:

![Entity resolution pipeline showing transformation from conflicting labels to unified output](/assets/images/posts/2023-network-endpoint-entity-resolution/entity-resolution-voting-pipeline.png)

*The resolution pipeline processes the nine input labels through three stages: (1) Entity Resolution & Heuristics applies string similarity metrics and external knowledge sources to identify semantically equivalent labels, reducing the set to two candidates: "sony xperia z5" and "android". (2) The Voting Algorithm scores these candidates based on parser agreement, label specificity, web search result similarity, and encyclopedia article convergence. (3) The highest-scoring label, "sony xperia z5", becomes the Unified Network Endpoint Label, accurately identifying the device without manual intervention.*

This automated resolution replaces what previously required manual classification across potentially thousands of device types, enabling scalable and accurate network security policies.

## Key Innovation

The system combines deterministic string algorithms with external knowledge sources to achieve accurate entity resolution. By querying web search engines and encyclopedias, it understands relationships between labels that simple string matching would miss. For example, it recognizes that "xperia" and "sony android" are related because Xperia is a Sony product line.

The architecture uses a master database with [publish-subscribe](https://en.wikipedia.org/wiki/Publish–subscribe_pattern){:target="_blank"} updates to [leaf switches](https://www.techtarget.com/searchdatacenter/definition/Leaf-spine){:target="_blank"}, ensuring consistent device identification across the entire network. This enables precise security policies and threat detection tailored to specific device types.

## Patent Details

- **Patent Number**: US 11,799,882 B1
- **Filed**: May 26, 2022
- **Granted**: October 24, 2023
- **Inventors**: Arunabh Ghosh, Debabrata Dash
- **Assignee**: Arista Networks Inc.
- **View Patent**: [Google Patents](https://patents.google.com/patent/US11799882B1/){:target="_blank"}

## The Bottom Line

This automated system eliminates the manual device classification process, making enterprise networks both more secure and easier to manage. What once required security teams to manually map device relationships across thousands of devices now happens automatically, enabling scalable network security policies tailored to specific device types.
