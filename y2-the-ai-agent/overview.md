---
description: Y2's differentiator with cutting edge RLM techniques.
icon: satellite-dish
---

# Overview

## Y2 Recursive Research: Overview

### The Problem with Traditional AI Research

Most AI-powered research tools operate in a single pass: you ask a question, the AI searches, and returns an answer. This approach has fundamental limitations:

#### Surface-Level Coverage

Single-pass systems can only explore topics at one depth. They're like reading the first page of Google results—you get an overview, but miss the nuanced details buried in specialized sources.

#### No Follow-up Questions

Human researchers naturally ask follow-up questions. When you discover something interesting, you dig deeper. Traditional AI tools don't have this capability—they can't pursue promising leads or explore subtopics that emerge during research.

#### Source Quantity vs Quality Trade-off

You're forced to choose: either retrieve many shallow sources, or a few deep sources. You can't do both efficiently in a single pass.

#### Fixed Context Window

Every search happens in isolation. There's no memory of what was already discovered, leading to redundant searches and wasted API costs.

### Introducing Recursive Language Models (RLM)

Y2's recursive research system is inspired by **Recursive Language Models**, an emerging AI research paradigm that mirrors how humans actually conduct research:

1. **Start Broad** - Get the lay of the land
2. **Identify Gaps** - Notice what's missing or needs clarification
3. **Dive Deep** - Explore specific subtopics with targeted searches
4. **Synthesize** - Combine findings from all layers into coherent insights

#### The Key Insight

Just as recursion in programming solves complex problems by breaking them into smaller subproblems, recursive research breaks down complex topics into manageable subtopics, each investigated independently and then synthesized.

### Why Y2's Approach is Superior

#### 1. Multi-Layer Intelligence Gathering

**Layer 0: Reconnaissance**

* Broad scan of the topic landscape (10 sources)
* Identifies key themes, recent developments, and knowledge gaps
* Purpose: "What's out there?"

**Layer 1: Deep Dive**

* Focused exploration of 3-5 subtopics (5 sources each)
* Targeted searches for specific aspects discovered in Layer 0
* Purpose: "What are the details?"

**Layer 2: Verification** (optional)

* Cross-reference findings and check for recent updates (3 sources per subtopic)
* Validate facts across multiple sources
* Purpose: "Is this accurate and current?"

#### 2. Intelligent Subtopic Decomposition

After each layer, GLM-4.5 analyzes the findings and generates specific subtopics for deeper investigation. This is fundamentally different from pre-defined queries:

**Traditional Approach:**

```
Query: "Bitcoin market analysis"
→ Search once
→ Get 10 generic results
→ Done
```

**Recursive Approach:**

```
Layer 0 Query: "Bitcoin market analysis"
→ Search (10 results)
→ Discover: price volatility, institutional adoption, regulatory concerns

Layer 1 Subtopics (generated dynamically):
  → "Bitcoin institutional investment Q1 2025" (5 results)
  → "Bitcoin ETF regulatory developments" (5 results)
  → "Bitcoin technical support levels analysis" (5 results)

Layer 2 Verification (if enabled):
  → Cross-check each subtopic with recent sources
```

The system **discovers what to research** based on **what it finds**, not what you pre-program.

#### 3. Source Freshness Validation

Not all sources are created equal. Y2 implements sophisticated freshness scoring:

**Age-Based Scoring**

* Exponential decay formula: newer sources score higher
* Topic-specific thresholds:
  * Crypto prices: 24 hours
  * Security threats: 30 days
  * General topics: 90 days

**Content-Based Staleness Detection**

* Scans for outdated year references (2020, 2021, etc.)
* Detects phrases like "last year" or "archived"
* Flags deprecated information

**Aggregate Metrics**

* Average source age across all layers
* Freshness score (0-1, higher = better)
* Stale source count and warnings

#### 4. Link Health Checking

Sources are useless if they're dead. Y2 validates every link:

**HTTP Status Validation**

* Asynchronous HEAD requests (doesn't block report delivery)
* 5-second timeout per link with parallel execution
* Circuit breaker for repeatedly failing domains

**Web Archive Fallback**

* If a link is dead, automatically fetch Wayback Machine snapshot
* Preserves historical sources that would otherwise be lost
* Metadata includes archive URL and timestamp

#### 5. Parallel Execution Strategy

Y2 implements a hybrid execution strategy:

**Breadth-First (Parallel)**

* All subtopics at a layer execute simultaneously
* 3x faster than sequential execution
* Optimal for time-sensitive reports

**Depth-First (Sequential)**

* Each subtopic completes fully before next starts
* Lower peak memory usage
* Better for extremely deep research (depth 3+)

**Hybrid (Default)**

* Parallel at Layer 0 and Layer 1
* Sequential at Layer 2 for verification
* Best balance of speed and resource efficiency

{% hint style="info" %}
We currently only breadth and hybrid execution strategies. Due to to the long function cycles depth first requires, our serverless architecture currently timeout for anything running >600 seconds.&#x20;
{% endhint %}

### Real-World Impact

#### Traditional Single-Pass Report

```
Topic: "Cybersecurity threats to financial institutions 2025"
Time: 45 seconds
Sources: 5
Depth: Surface overview
Quality: Generic, misses emerging threats
Cost: $0.15
```

#### Y2 Recursive Research (Depth 1)

```
Topic: "Cybersecurity threats to financial institutions 2025"
Time: 2 minutes
Sources: 25 (Layer 0: 10, Layer 1: 15)

Discovered Subtopics:
  - API security vulnerabilities in banking apps
  - AI-powered phishing attacks targeting executives
  - Supply chain compromises in payment processors

Quality: Specific, actionable intelligence on emerging threats
Cost: $0.15 (same cost, 5x more sources, 10x better insights)
```

### When to Use Each Depth

#### Depth 0: Quick Intelligence

**Use Cases:**

* Daily market briefs
* Price updates
* News summaries
* Quick fact-checking

**Characteristics:**

* 30 seconds
* 3-5 sources
* Broad overview

#### Depth 1: Standard Research

**Use Cases:**

* Weekly intelligence reports
* Competitive analysis
* Industry trend reports
* Investment research

**Characteristics:**

* 90 seconds
* 12-20 sources
* Balanced depth and breadth

#### Depth 2: Deep Investigation

**Use Cases:**

* Strategic planning documents
* Due diligence reports
* Comprehensive threat assessments
* Academic-quality research

**Characteristics:**

* 4 minutes
* 40-60 sources
* Maximum depth and verification

### The Recursive Advantage

Y2's recursive research system doesn't just search more—it **searches smarter**:

1. **Adaptive**: Discovers what to research based on findings
2. **Thorough**: Multiple layers ensure nothing is missed
3. **Fresh**: Validates source recency and accessibility
4. **Efficient**: Parallel execution maximizes speed
5. **Cost-Effective**: GLM-4.5 delivers quality at 10% the cost
6. **Verifiable**: Cross-references findings across layers

_**This isn't just an incremental improvement over single-pass systems. It's a fundamental rethinking of how AI conducts research—modeled after human intelligence gathering, not simple keyword**_
