---
description: How the Y2 News Terminal Works
icon: newspaper
---

# News Terminal

The Signal Feed Terminal is Y2's real-time intelligence monitoring system, providing live news signals and AI-generated recaps across multiple topics.

### Overview

The News Terminal transforms raw signal data from Gloria AI into actionable intelligence, offering two distinct modes:

* **Live Feed Mode**: Real-time signal stream with instant updates
* **AI Recap Mode**: Synthesized intelligence summaries over configurable timeframes

Unlike traditional RSS readers or news aggregators, the Signal Feed uses AI-powered analysis to filter noise and surface meaningful signals across crypto, AI, macro, and technology topics.

### Key Features

#### Multi-Topic Monitoring

Track 15 specialized intelligence feeds simultaneously:

* **Crypto**: Bitcoin, Ethereum, Solana, Ripple, Aptos, Hyperliquid
* **AI/Tech**: AI Agents, Machine Learning, Tech Industry
* **Finance**: Macro Economics, Real World Assets (RWA), Ondo Finance
* **Emerging**: Virtuals Protocol

#### Dual-Mode Intelligence

**Live Feed Mode**

* Stream of individual signals as they occur
* Sub-minute latency from source to display
* Chronological ordering (newest first)
* Direct from Gloria AI's signal detection engine

**AI Recap Mode**

* Synthesized summaries across multiple timeframes (12h, 24h, 3d, 7d)
* Generated on-demand using LLM analysis
* Topic clustering and pattern detection
* Executive-style intelligence briefs

#### Persistent Preferences

Your feed selections, view mode, and timeframe preferences sync across devices:

* Automatic save on every change
* Instant restoration on page load
* No manual "save settings" required

### How It Works

#### Signal Collection Architecture

```
Gloria AI Signal Engine
         ↓
   API Endpoint
   (itsgloria.ai)
         ↓
    Y2 Backend
  (Convex Actions)
         ↓
   Signal Database
         ↓
  News Terminal UI
```

#### Live Feed Pipeline

**1. Signal Detection** (Gloria AI)

* Monitors social media, news outlets, on-chain data
* Pattern recognition for market-moving events
* Sentiment analysis and anomaly detection
* Real-time filtering for relevance

**2. Categorization** (Gloria AI)

* Each signal tagged with feed category
* Timestamp precision to the second
* Metadata preservation (source, confidence, etc.)

**3. Delivery** (Y2 Backend)

* Fetch signals for selected topics
* Limit: 50 most recent per request
* Deduplication across feeds
* Sorted by timestamp (descending)

**4. Display** (Terminal)

* Real-time rendering with React state
* Automatic time-ago formatting
* Color-coded topic badges
* Infinite scroll for history

#### AI Recap Pipeline

**1. Signal Aggregation**

* Collect all signals for topic within timeframe
* Group by semantic similarity
* Remove duplicates and low-quality signals

**2. LLM Analysis**

* Send aggregated signals to language model
* Extract key themes and trends
* Identify market-moving events
* Generate executive summary

**3. Structured Output**

* BLUF (Bottom Line Up Front) format
* Key developments section
* Market implications
* Forward-looking analysis

**4. Caching**

* Recaps cached for 1-hour TTL
* Regenerate on refresh after expiration
* Per-topic, per-timeframe cache keys

### Using the Terminal

#### Selecting Feeds

<figure><img src="../.gitbook/assets/Screenshot 2025-10-18 at 1.12.34 PM.png" alt=""><figcaption></figcaption></figure>

**Multiple Selection Strategy:**

**Focused Monitoring** (1-3 feeds)

* Deep attention on specific topics
* Easier to follow all signals
* Best for active traders or specialists
* Example: Bitcoin + Ethereum + Macro

**Broad Coverage** (4-8 feeds)

* Balanced intelligence gathering
* Spot cross-topic correlations
* Good for portfolio managers
* Example: All crypto + AI + Tech

**Full Spectrum** (9+ feeds)

* Complete market awareness
* Pattern detection across sectors
* Best for researchers and analysts
* Use AI Recap mode to synthesize

**Feed Selection Tips:**

* Click any feed to toggle on/off
* Selected feeds show gradient backgrounds
* At least one feed required to load data
* Changes auto-save and trigger refresh

#### Live Feed Mode

&#x20;_Screenshot placeholder: Terminal showing live signal stream_

**What You See:**

```
[Gradient Badge: Bitcoin]  42m ago
"Bitcoin dominance rises to 58.3% as altcoin market
cools. BTC.D up 1.2% in last 24 hours."
```

**Understanding Signals:**

**Time Precision**

* "Just now": < 1 minute old
* "42m ago": 42 minutes old
* "3h ago": 3 hours old
* "2d ago": 2 days old

**Signal Quality** Gloria AI pre-filters signals, so everything in the feed meets minimum quality thresholds:

* Verifiable source (not rumors)
* Market relevance (impact on prices/sentiment)
* Timeliness (recent developments)
* Clarity (understandable, actionable)

**Volume Expectations:**

* High-activity feeds (Bitcoin, AI): 20-50 signals/day
* Medium-activity feeds (Aptos, RWA): 10-20 signals/day
* Low-activity feeds (Virtuals, Ondo): 5-10 signals/day

**Refresh Behavior:**

* Manual refresh: Click refresh button
* Fetches latest 50 signals per selected feed
* Merges and deduplicates across feeds
* Updates "Last updated" timestamp

#### AI Recap Mode

&#x20;_Screenshot placeholder: Recap cards with gradient headers_

**Timeframe Selection:**

**12 Hours**

* Best for: Day trading, active monitoring
* Coverage: Half-day market cycles
* Signal count: 10-25 per topic
* Refresh: Every 12 hours recommended

**24 Hours**

* Best for: Daily briefs, overnight catch-up
* Coverage: Full trading day
* Signal count: 20-50 per topic
* Refresh: Every morning

**3 Days**

* Best for: Weekly check-ins, trend identification
* Coverage: Short-term trends
* Signal count: 60-150 per topic
* Refresh: Every 2-3 days

**7 Days**

* Best for: Weekly summaries, strategic planning
* Coverage: Full week of developments
* Signal count: 140-350 per topic
* Refresh: Every Monday

**Recap Structure:**

```
[Gradient Header]
Bitcoin
12h intelligence recap                   Jan 18, 3:42 PM

[Content Section]

BOTTOM LINE UP FRONT
Bitcoin maintains $47K support with institutional
buying pressure continuing. ETF inflows reached
$230M this week, largest since December.

KEY DEVELOPMENTS
• Price action: $47.2K (+2.1% 24h)
• ETF flows: $230M net inflows across 11 funds
• On-chain: 15K BTC moved off exchanges
• Sentiment: Fear & Greed index at 62 (Greed)

MARKET IMPLICATIONS
Sustained institutional demand suggests strong
support levels. Low exchange reserves indicate
supply crunch potential if momentum continues.

OUTLOOK
Watch $48.5K resistance. Break above likely
triggers momentum trading toward $50K psychological
level. Support at $46K remains strong.
```

**Generating Recaps:**

1. Select feeds you want recaps for
2. Switch to "AI Recap" view mode
3. Choose timeframe (12h, 24h, 3d, 7d)
4. Click "Refresh" to generate
5. Generation takes 10-30 seconds per topic

**Recap Caching:**

* First request generates new recap
* Subsequent requests serve cached version
* Cache expires after 1 hour
* Refresh button always regenerates

### Understanding Signal Quality

#### What Makes a Good Signal?

**High-Quality Signal Example:**

```
[Bitcoin] 15m ago
"MicroStrategy purchases additional 2,500 BTC for
$117.5M at average price of $47K. Total holdings
now exceed 190,000 BTC. Announcement via 8-K filing."

✓ Specific (exact numbers)
✓ Verifiable (SEC filing reference)
✓ Timely (15 minutes old)
✓ Material (market-moving size)
✓ Actionable (price impact likely)
```

**Low-Quality Signal (Filtered Out):**

```
[Bitcoin] 2h ago
"Someone thinks Bitcoin might go up or down.
Popular trader shares vague opinion on social media."

✗ Vague (no specifics)
✗ Unverifiable (anonymous source)
✗ Not material (opinion, not fact)
✗ Not actionable (no clear implication)
```

#### Signal vs Noise

Gloria AI's filtering removes:

* Duplicate reports of same event
* Unverified rumors and speculation
* Low-engagement social media posts
* Sponsored content and advertisements
* Historical news (>7 days old unless significant)

This filtering means **fewer signals, higher quality**—you see 50 meaningful signals instead of 500 irrelevant posts.

### Advanced Usage Patterns

#### Cross-Topic Correlation

Monitor related feeds to spot patterns:

**Crypto Correlation**

```
Feeds: Bitcoin + Ethereum + Solana
Pattern: When BTC dominance drops, alt-L1s (ETH, SOL) often rally
Use case: Rotation detection, portfolio rebalancing
```

**AI/Crypto Convergence**

```
Feeds: AI Agents + Virtuals + AI
Pattern: AI protocol tokens react to AI research breakthroughs
Use case: Narrative trading, technology adoption
```

**Macro/Crypto Relationship**

```
Feeds: Macro + Bitcoin + Ethereum
Pattern: DXY strength often inversely correlates with crypto
Use case: Risk-on/risk-off positioning
```

#### Event-Driven Monitoring

**Breaking News Response:**

1. Select relevant feed (e.g., Bitcoin)
2. Switch to Live Feed mode
3. Refresh every 2-5 minutes
4. Watch for signal clusters (multiple signals on same event)

**Post-Event Analysis:**

1. Switch to AI Recap mode
2. Select 24h timeframe
3. Generate recap for affected topics
4. Review synthesized impact assessment

#### Research Workflow

**Daily Intelligence Routine:**

```
Morning (9 AM):
1. Open terminal
2. View 24h AI Recaps for all selected feeds
3. Scan for overnight developments
4. Note any surprises or trend changes

Midday Check (12 PM):
5. Switch to Live Feed
6. Refresh to catch intraday signals
7. Assess momentum and sentiment shifts

Evening Review (6 PM):
8. Generate 12h recaps for active topics
9. Compare morning outlook vs actual developments
10. Adjust positions/watchlist accordingly
```

**Weekly Research:**

```
Monday Morning:
1. Generate 7d recaps for all feeds
2. Identify key themes and trends
3. Cross-reference with price action
4. Set weekly monitoring priorities

Throughout Week:
5. Use Live Feed for daily monitoring
6. Flag significant signals for weekly report

Friday Evening:
7. Review week's signals and recaps
8. Document lessons learned
9. Prepare outlook for next week
```

### Integration with Y2 Intelligence

#### Complementary Systems

**Signal Feed** (Reactive)

* Monitors real-time developments
* Responds to market events
* Short-term tactical intelligence
* User-initiated refresh

**Y2 Reports** (Proactive)

* Scheduled automated research
* Deep analysis with recursive search
* Long-term strategic intelligence
* Automatic delivery

#### Using Both Together

**Example Workflow:**

**Step 1: Discover Topic (Signal Feed)**

```
Live Feed shows:
"Aptos announces partnership with major bank for
RWA tokenization. Technical details at AptosCon."

Signal detected → Potential research topic identified
```

**Step 2: Configure Deep Research (Y2 Profile)**

```
Create profile:
  Name: "Aptos RWA Banking Partnership Analysis"
  Topic: "Aptos blockchain RWA tokenization banking partnerships"
  Recursion: Depth 1 (standard research)
  Schedule: One-time manual generation
```

**Step 3: Generate Intelligence Report**

```
Y2 recursive research:
  Layer 0: Broad scan (10 sources on Aptos RWA)
  Layer 1: Deep dives into:
    • Technical implementation details
    • Banking partner background
    • Regulatory implications
    • Competitive landscape

Result: 12,000-word comprehensive analysis
```

**Step 4: Monitor Developments (Signal Feed)**

```
Add "Aptos" feed to terminal
Track ongoing developments
Generate 7d recaps weekly
Update research if material changes occur
```

### Performance & Reliability

#### Response Times

**Live Feed Refresh:**

* API request: 1-2 seconds
* Data processing: <1 second
* UI rendering: <500ms
* Total: 2-4 seconds for 50 signals

**AI Recap Generation:**

* Signal aggregation: 1-2 seconds
* LLM analysis: 8-20 seconds (depends on signal count)
* Formatting: <1 second
* Total: 10-30 seconds per topic

**Parallel Recap Generation:**

```
1 topic:  ~15 seconds
3 topics: ~20 seconds (parallel processing)
5 topics: ~30 seconds
10 topics: ~45 seconds
```

#### Data Freshness

**Signal Latency:**

```
Event occurs (e.g., tweet, news article)
        ↓ 10-30 seconds
Gloria AI detects signal
        ↓ 5-15 seconds
Signal available via API
        ↓ Manual refresh
Displayed in Y2 terminal
```

Total latency: 15-60 seconds from event to display (when refreshing actively)

**Refresh Recommendations:**

* Breaking news: Every 2-5 minutes
* Active monitoring: Every 15-30 minutes
* Passive monitoring: Every 1-2 hours
* Background awareness: 2-3 times per day

#### Rate Limits & Quotas

**API Limits:**

* 50 signals per feed per request
* Unlimited refreshes (no rate limit on Y2 side)
* Gloria AI may throttle excessive requests (>1 req/second)

**Best Practice:**

* Don't refresh more than once per minute
* Use AI Recap mode for historical signals
* Live Feed mode for real-time only

### Troubleshooting

#### No Signals Appearing

**Problem:** Terminal shows "No signals detected"

**Solutions:**

1. **Check feed selection**: At least one feed must be selected
2. **Verify API connectivity**: Gloria AI endpoint may be down
3. **Expand timeframe**: Some feeds have low activity
4. **Try different feeds**: Start with high-volume feeds (Bitcoin, AI)

#### Recaps Not Generating

**Problem:** "Generating AI recaps..." spins indefinitely

**Solutions:**

1. **Check feed selection**: No feeds selected = no recaps
2. **Verify timeframe**: Try 24h first (most reliable)
3. **Reduce feed count**: Generate 1-2 recaps first, then scale
4. **Check quota**: LLM API limits may be reached

#### Preferences Not Saving

**Problem:** Feed selections reset on page reload

**Solutions:**

1. **Wait for save**: Changes save after 1-2 second delay
2. **Check authentication**: Preferences require logged-in user
3. **Clear cache**: Browser cache may be stale
4. **Check console**: Database write errors may appear

#### Slow Performance

**Problem:** Terminal feels sluggish or unresponsive

**Solutions:**

1. **Reduce selected feeds**: 10+ feeds = more data to process
2. **Use AI Recap mode**: Fewer DOM elements than Live Feed
3. **Limit Live Feed history**: Only shows 50 most recent
4. **Clear browser cache**: Accumulated data may slow down

### Mobile Experience

#### Responsive Design

The Signal Feed Terminal is fully optimized for mobile:

**Feed Selection:**

* Horizontally scrollable feed pills
* Larger touch targets (44px minimum)
* Gradient indicators remain visible

**Live Feed:**

* Single column layout
* Condensed timestamps (e.g., "42m ago")
* Full signal text (no truncation)

**AI Recaps:**

* Full-width cards
* Collapsed headers on small screens
* Readable typography (16px base)

#### Mobile Workflow

**Quick Check (2 minutes):**

1. Open terminal on mobile
2. View pre-loaded data (from last session)
3. Scan recent signals
4. Refresh if needed

**Deep Dive (10 minutes):**

1. Switch to AI Recap mode
2. Select 24h timeframe
3. Generate recaps for key feeds
4. Read synthesized intelligence

### Best Practices

#### For Active Traders

**Setup:**

* Select 2-4 core feeds (e.g., Bitcoin, Ethereum, Macro)
* Use Live Feed mode during trading hours
* Keep terminal open in browser tab

**Routine:**

* Refresh every 15 minutes during market hours
* Watch for signal clusters (multiple signals on same event)
* Cross-reference with price charts
* Generate 12h recap at market close

#### For Researchers

**Setup:**

* Select 6-10 feeds across domains
* Primarily use AI Recap mode
* Generate weekly recaps on Monday mornings

**Routine:**

* Morning: 24h recaps for overnight catch-up
* Midday: Live Feed spot check for breaking news
* Evening: Note significant signals for weekly report
* Weekly: 7d recaps for trend analysis

#### For Portfolio Managers

**Setup:**

* Select feeds matching portfolio holdings
* Use both modes (Live Feed + AI Recap)
* Integrate with Y2 scheduled reports

**Routine:**

* Pre-market: 24h recaps for all holdings
* Intraday: Live Feed for breaking developments
* Post-market: Generate 12h recap for daily summary
* Weekly: 7d recaps for strategic review

### Privacy & Data

#### What's Stored

**User Preferences:**

* Selected feeds (array of strings)
* View mode (news or recap)
* Timeframe (12h, 24h, 3d, 7d)

**Not Stored:**

* Signal content (ephemeral, from API)
* Recap content (cached temporarily, not persisted)
* User interaction logs (no analytics tracking)

#### Data Source

All signals originate from **Gloria AI** (itsgloria.ai):

* Independent third-party intelligence provider
* No Y2-specific customization
* Same data available to all Gloria AI users

Y2 adds:

* Multi-topic aggregation
* AI-powered recap generation
* Persistent preferences
* Integration with Y2 intelligence reports
