# Tier-System

## Overview
This document explains the three tiers of memory utilized in the system, detailing their characteristics and functionalities.

### T1: Ephemeral In-Memory with Optional Snapshots
- **Description:** This tier holds data temporarily in-memory. It is designed for speed and efficiency in processing immediate tasks.
- **Snapshots:** Users have the option to create snapshots of the data, which can be helpful for recovery or analysis purposes.

### T2: Episodic Candidates with 7-Day Decay
- **Description:** Data in T2 exists for a week and represents candidates that may be relevant in episodic contexts. After 7 days, this data begins to decay and is purged promptly.
- **Usage:** This tier is useful for short-term memory needs where data relevance is time-sensitive. 

### T3: Consensus Memory with 90-Day Decay and Promotion Lineage Tracking
- **Description:** T3 is designed for long-term memory, maintaining data for up to 90 days. It ensures that data is agreed upon through a consensus mechanism, making it reliable for significant decisions.
- **Promotion Lineage Tracking:** This feature allows users to track the history and changes of data within this tier, enhancing accountability and clarity on data evolution.

## Conclusion
Understanding these tiers is crucial for effectively utilizing the memory system, ensuring optimal data management for various use cases.