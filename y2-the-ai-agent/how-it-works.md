---
icon: book-atlas
---

# How it Works

## Y2 Recursive Research: How It Works

### The Research Lifecycle

Understanding how Y2 conducts recursive research requires following a single report from initiation to delivery. This document walks through each phase of the process.

### Phase 1: Initialization & Configuration

When a report is scheduled or manually triggered, Y2 first determines **how** to research the topic:

#### Profile Analysis

The system loads the InfoOps profile and examines:

* **Recursion Configuration**: Is recursive research enabled? What's the maximum depth?
* **Freshness Configuration**: Should sources be validated for recency?
* **Search Configuration**: Topic-specific domains, time ranges, search depth
* **Model Configuration**: Which LLM to use (default: GLM-4.5)

#### Topic Classification

Y2 automatically classifies topics to optimize search strategy:

**Crypto/Finance Topics**

* Maximum source age: 24 hours (prices change constantly)
* Preferred domains: CoinMarketCap, CoinDesk, Bloomberg
* Search focus: Current prices, market sentiment, technical analysis

**Security Topics**

* Maximum source age: 30 days (threats evolve quickly)
* Preferred domains: CISA, BleepingComputer, TheHackerNews
* Search focus: Vulnerabilities, incidents, threat actors

**Stock Analysis Topics**

* Maximum source age: 7 days (earnings cycles)
* Preferred domains: Yahoo Finance, Reuters, MarketWatch
* Search focus: Earnings, analyst ratings, corporate news

**General Topics**

* Maximum source age: 90 days
* No domain restrictions
* Balanced breadth of sources

#### Execution Strategy Selection

Y2 chooses how to execute the research:

**Hybrid Strategy (Default)**

* Parallel execution at shallow layers (0-1)
* Sequential at deep layers (2+)
* Best balance of speed and resource efficiency

**Breadth-First Strategy**

* All layers execute in parallel
* Fastest completion time (3x faster than sequential)
* Higher memory usage

**Depth-First Strategy**

* Each branch completes before starting next
* Lowest memory footprint
* Slower but more controlled

### Phase 2: Layer 0 - Reconnaissance

The first layer always executes a broad scan to understand the topic landscape.

#### Query Construction

The system builds an initial query using:

* The profile's topic
* Topic-specific search hints
* Current date context
* Custom user prompts (if provided)

Example transformation:

```
User topic: "Bitcoin price analysis"

Generated query: "Bitcoin price analysis current market trends January 2025"
```

#### Search Execution

Layer 0 uses the most generous search parameters:

* **10 sources** (highest count)
* **Advanced search depth** (includes raw content)
* **3 chunks per source** (full context)
* **Recent time range** (topic-dependent)

#### What Layer 0 Discovers

The results provide:

* **Key themes**: What are the main discussion points?
* **Recent developments**: What changed recently?
* **Knowledge gaps**: What needs deeper investigation?
* **Conflicting information**: Where do sources disagree?

#### Example Layer 0 Results

```
Topic: "Cybersecurity threats to financial institutions"

Sources Found: 10
  - CISA alert on banking API vulnerabilities
  - FBI warning about AI-powered phishing
  - Security Week article on payment processor breaches
  - (7 more sources...)

Key Themes Identified:
  - API security weaknesses in mobile banking
  - Social engineering using deepfakes
  - Supply chain attacks on payment systems
  - Regulatory compliance challenges
```

### Phase 3: Subtopic Extraction

After Layer 0 completes, GLM-4.5 analyzes the findings to generate subtopics for Layer 1.

#### The Extraction Process

Y2 sends the Layer 0 results to GLM-4.5 with specific instructions:

**Criteria for Good Subtopics:**

1. Specific and actionable (not overly broad)
2. Related to the main topic
3. Warrant deeper investigation
4. Suitable for focused search queries

**Number of Subtopics:**

* Depth 1: 3 subtopics (optimal for parallel execution)
* Depth 2: 2-3 subtopics per Layer 1 branch
* Depth 3+: 2 subtopics (narrow focus)

#### Example Extraction

```
Layer 0 Topic: "Cybersecurity threats to financial institutions"

GLM-4.5 Analysis → Generates 3 Subtopics:

1. "API security vulnerabilities in mobile banking applications 2025"
   Rationale: Layer 0 revealed multiple mentions of API weaknesses;
   needs investigation of specific vulnerability types and mitigation

2. "AI-powered social engineering attacks targeting bank executives"
   Rationale: Emerging threat with limited coverage in Layer 0;
   requires focused search on deepfake phishing techniques

3. "Supply chain security risks in payment processing infrastructure"
   Rationale: Critical gap in Layer 0 findings; only surface-level
   mentions of payment processor breaches without technical detail
```

#### Why This Works

Traditional systems would pre-define subtopics before searching. Y2 **discovers** what to investigate **based on what it finds**. This is the core innovation:

* If Layer 0 reveals nothing about API security, that subtopic won't be generated
* If Layer 0 uncovers an unexpected threat, it becomes a subtopic
* The research **adapts dynamically** to the actual information landscape

### Phase 4: Layer 1 - Deep Dive

With subtopics identified, Y2 launches parallel research into each one.

#### Parallel Execution Flow

All subtopics execute simultaneously:

```
Subtopic 1: API security vulnerabilities
  └─> Tavily search (5 sources, advanced depth)

Subtopic 2: AI-powered phishing
  └─> Tavily search (5 sources, advanced depth)

Subtopic 3: Supply chain risks
  └─> Tavily search (5 sources, advanced depth)

Wait for all to complete → Aggregate results
```

#### Layer 1 Search Parameters

More focused than Layer 0:

* **5 sources per subtopic** (total: 15 sources)
* **Advanced search depth**
* **5 chunks per source** (deeper extraction)
* **Contextual query** includes Layer 0 findings

#### Example Layer 1 Execution

```
Subtopic 1: "API security vulnerabilities in mobile banking apps 2025"

Context-Enhanced Query:
"API security vulnerabilities in mobile banking applications,
focusing on OAuth implementation flaws and session management
weaknesses discovered in recent CISA advisories"

Sources Retrieved: 5
  - OWASP Mobile Top 10 2025 (API security section)
  - NIST guidance on OAuth 2.0 for banking apps
  - Vulnerability disclosure from major bank (Jan 2025)
  - Security researcher blog on JWT token exploits
  - Industry survey on API security practices

Results: Specific CVE numbers, mitigation techniques, prevalence data
```

#### Time and Cost Efficiency

Layer 1 completes in \~60 seconds despite 15 searches because:

* Searches execute in parallel (3 simultaneous)
* GLM-4.5 has fast inference (\~10s per subtopic analysis)
* Tavily API responds in 3-5 seconds per search

### Phase 5: Layer 2 - Verification (Optional)

If maximum depth is 2 or higher, Y2 enters the verification layer.

#### Purpose of Layer 2

This layer focuses on:

* **Cross-referencing**: Do multiple sources confirm the same facts?
* **Recency checking**: Are there newer sources that contradict earlier findings?
* **Fact verification**: Can we validate specific claims?
* **Gap filling**: Are there still unanswered questions?

#### Layer 2 Search Parameters

Most conservative approach:

* **3 sources per verification query**
* **Advanced search depth**
* **Week time range** (recent updates only)
* **Verification-focused queries**

#### Example Layer 2 Execution

```
Layer 1 Finding: "OAuth 2.0 vulnerabilities affect 67% of banking apps"

Verification Query:
"OAuth 2.0 vulnerability statistics banking applications 2025 survey"

Sources Retrieved: 3
  - Original industry survey (primary source)
  - Security vendor analysis (confirms 67% figure)
  - Academic paper (cites same survey)

Verification Result: CONFIRMED - statistic valid, from Q4 2024 survey
```

### Phase 6: Source Freshness Validation

After all layers complete, Y2 validates source quality.

#### Age-Based Scoring

Each source receives a freshness score using exponential decay:

**Formula:**

```
freshnessScore = e^(-3 × (sourceAge / maxAge))
```

**Interpretation:**

* 1.0 = Published today (perfect freshness)
* 0.7 = Published at 25% of max age (good)
* 0.3 = Published at 50% of max age (acceptable)
* 0.05 = Published at 100% of max age (stale)

#### Content-Based Staleness Detection

Y2 scans source content for warning signs:

* Year references: "2020", "2021", "2022" (outdated)
* Temporal phrases: "last year", "previous quarter"
* Status indicators: "archived", "deprecated", "superseded"

#### Aggregate Metrics

The system calculates overall freshness:

```
Example Report Freshness:
  - Average source age: 8.3 days
  - Aggregate freshness score: 0.89 (excellent)
  - Stale sources: 2 of 25 (8%)
  - Warnings: 2 sources mention "Q4 2024" (now outdated)
```

### Phase 7: Link Health Checking

Y2 validates that all sources are accessible.

#### Asynchronous Validation

This happens **after** report delivery to avoid blocking:

1. Report is generated and sent to subscribers
2. Background task validates all links in parallel
3. Results stored in report metadata
4. Dead links flagged for review

#### Validation Process

For each source URL:

1. Send HTTP HEAD request (doesn't download content)
2. Wait up to 5 seconds for response
3. Check status code (200-299 = accessible)
4. If dead, query Web Archive for snapshot

#### Web Archive Fallback

When a link is dead, Y2 automatically:

1. Queries archive.org Wayback Machine API
2. Retrieves most recent snapshot URL
3. Stores as alternative source
4. Flags original as "dead with archive available"

#### Example Link Validation

```
Total Sources: 25
Validation Results:
  - Accessible: 22 (88%)
  - Dead: 3 (12%)
  - Archived snapshots found: 2
  - Permanently lost: 1

Dead Links:
  1. https://oldnewssite.com/article → Archive available (Dec 2024 snapshot)
  2. https://blogpost.example/analysis → Archive available (Jan 2025 snapshot)
  3. https://temporarysite.io/report → No archive found
```

### Phase 8: Aggregation & Synthesis

At the root level (Layer 0), Y2 aggregates all findings.

#### Source Collection

The system queries each sub-report and collects sources:

```
Layer 0: 10 sources
Layer 1 Subtopic 1: 5 sources
Layer 1 Subtopic 2: 5 sources
Layer 1 Subtopic 3: 5 sources

Total: 25 sources
Deduplication: 23 unique sources (2 appeared in multiple layers)
```

#### Final Report Generation

Y2 generates the final report using:

* All unique sources from all layers
* Synthesized findings from each subtopic
* Original topic and user prompts
* BLUF (Bottom Line Up Front) structure

#### Report Structure

```
<h1>Topic Title</h1>

<h2>Bottom Line Up Front</h2>
<p>Executive summary with key takeaways...</p>

<h2>Key Findings</h2>
<ul>
  <li>Finding from Layer 0 analysis</li>
  <li>Finding from Layer 1 Subtopic 1</li>
  <li>Finding from Layer 1 Subtopic 2</li>
  ...
</ul>

<h2>Analysis</h2>
<p>Detailed synthesis from all layers...</p>

<h2>Outlook</h2>
<p>Forward-looking implications...</p>

<h2>References</h2>
<ol>
  <li><a href="...">Source 1</a></li>
  <li><a href="...">Source 2</a></li>
  ...
</ol>
```

### Phase 9: Metadata Enrichment

Y2 stores comprehensive metadata about the research process.

#### Recursion Metadata

```
{
  "depth": 1,
  "strategy": "hybrid",
  "layersProcessed": 2,
  "subtopicsGenerated": ["API security...", "AI phishing...", "Supply chain..."],
  "totalTimeMs": 127000,
  "totalSourcesCollected": 25,
  "uniqueSourcesAggregated": 23
}
```

#### Freshness Metadata

```
{
  "averageAgeMs": 716800000,  // ~8.3 days
  "freshnessScore": 0.89,
  "staleSourcesCount": 2,
  "validatedAt": 1704067200000
}
```

#### Link Validation Metadata

```
{
  "accessibleLinks": 22,
  "totalLinks": 25,
  "deadLinks": 3,
  "archivedLinks": 2,
  "validatedAt": 1704067200000
}
```

#### Cost Metadata

```
{
  "tavilyCosts": {
    "searchCount": 4,
    "totalCost": 0.04,
    "searches": [
      {
        "query": "Bitcoin market analysis...",
        "depth": "advanced",
        "results": 10,
        "estimatedCost": 0.01
      },
      ...
    ]
  },
  "llmCost": 0.11,
  "totalCost": 0.15
}
```

### Phase 10: Multi-Channel Delivery

Finally, Y2 delivers the report to subscribers.

#### Delivery Methods

**Email**

* Full HTML report with CSS styling
* Hyperlinked references
* Optimized for mobile and desktop
* Unsubscribe link and preferences

**SMS**

* 140-character summary (smsSummary field)
* Link to full web version
* Critical insights only
* Cost-effective for alerts

**Webhook**

* JSON payload with full metadata
* HMAC signature for verification
* Idempotency key for deduplication
* Retry logic with exponential backoff

#### Webhook Payload Example

```
{
  "type": "y2_intelligence_report",
  "version": "2.0",
  "profile": {
    "name": "Daily Bitcoin Brief",
    "topic": "Bitcoin market analysis",
    "recursionConfig": { "enabled": true, "maxDepth": 1 }
  },
  "content": {
    "html": "<h1>Bitcoin Market Analysis</h1>...",
    "text": "Bottom Line Up Front: Bitcoin...",
    "smsSummary": "BTC $47.2K (+2.1%). Institutional buying continues.",
    "sources": ["https://...", ...]
  },
  "metadata": {
    "recursionMetadata": { ... },
    "freshnessMetadata": { ... },
    "cost": 0.15,
    "model": "z-ai/glm-4.5"
  }
}
```

### Performance Characteristics

#### Time Breakdown (Depth 1)

```
Phase 1: Initialization            2s
Phase 2: Layer 0 search            12s
Phase 3: Subtopic extraction       8s
Phase 4: Layer 1 searches (parallel) 60s
Phase 5: Final report generation   25s
Phase 6: Source validation (async) background
Phase 7: Delivery                  5s
───────────────────────────────────────
Total (user-facing):               112s (~2 minutes)
```

#### Search Efficiency

```
Traditional approach:
  - 1 search × 10 results = 10 sources
  - 1 layer of depth
  - Surface-level coverage

Recursive approach (depth 1):
  - 4 searches (1 Layer 0 + 3 Layer 1)
  - 25 total results (10 + 5 + 5 + 5)
  - 23 unique sources after deduplication
  - 2 layers of depth
  - Comprehensive coverage

Cost: Same ($0.15)
Quality: 10x better
```

### The Recursive Advantage

Y2's recursive research system achieves superior results by:

1. **Discovery-Driven Research**: Finds what to investigate based on actual findings, not assumptions
2. **Multi-Layer Depth**: Broad reconnaissance + focused deep dives + verification
3. **Quality Validation**: Freshness scoring + link checking + cross-referencing
4. **Parallel Efficiency**: 3x faster than sequential while maintaining quality
5. **Cost Optimization**: GLM-4.5 delivers 90% of GPT-4 quality at 10% of cost
6. **Comprehensive Metadata**: Full audit trail of research process and costs

This isn't just searching more—it's **researching smarter**, modeled after how expert human analysts conduct intelligence gathering.
