# 📱 Post Studio

An autonomous agent that researches, drafts, gets roasted by its critic, and iteratively revises until your LinkedIn post is perfect.

## Overview

Post Studio is a lightweight agent for generating high-engagement LinkedIn posts through rapid iteration and real-time feedback loops. The agent researches your topic, writes concise posts optimized for LinkedIn's format, sends drafts to an independent critic, and refines based on feedback until reaching your quality threshold.

## Features

- **Fast Iteration**: Optimized for quick draft-to-critique-to-revision cycles
- **Web Research**: Performs targeted searches to back up claims with real data
- **Independent Critic**: Separate LLM (gpt-4o-mini) scores and critiques each draft
- **Quality Gates**: Won't publish until reaching your minimum score (0-10)
- **LinkedIn Optimization**: 
  - First two lines work as truncated preview (LinkedIn cuts off after ~200 chars)
  - Short paragraphs with generous line breaks
  - Scannable format
  - 900-1800 character sweet spot
- **Alternative Hooks**: Agent generates 3-5 hook variations to test different angles
- **Export Options**: Copy to clipboard or save as Markdown
- **No Emojis by Default**: Clean, professional tone (configurable)

## How It Works

```
1. [Agent] Search → Research the topic
2. [Agent] Write Draft → Compose initial post
3. [Agent] Get Critique → Send to independent critic
4. [Critic] Score & Feedback → Rate 0-10, provide specific feedback
5. [Agent] Revise → Rewrite based on feedback
6. [Repeat] Steps 3-5 until score ≥ min threshold
7. [Agent] Deliver → Finalize with alternative hooks
```

## Getting Started

### Requirements

- OpenAI API key
- Modern web browser
- Internet connection

### Usage

1. **Load the HTML** in your browser
2. **Paste your OpenAI API key** (not stored, cleared on refresh)
3. **Brief the agent**:
   - **What is the post about?** (e.g., "Why RAG breaks in production and how to fix it")
   - **Tone**: Pick from Professional, Casual, Thought Leadership, Humorous
   - **Audience**: (optional) Who should get this? Defaults to general professionals
   - **Hashtags**: Include 3-5 hashtags? (Yes/No)
   - **Min score**: Set quality threshold (6-8 recommended)
4. **Optional**:
   - Enable/disable web search
   - Choose model (gpt-4o recommended; gpt-4o-mini is cheaper)
   - Set step budget
5. **Click "Generate Post"** to start

### Configuration

| Option | Default | Purpose |
|--------|---------|---------|
| Tone | Professional | Writing style and voice |
| Audience | General professionals | Target demographic |
| Include hashtags | Yes | 3-5 hashtags at end |
| Min quality score | 6 | Threshold before delivery (0-10) |
| Model | gpt-4o | LLM for writing and critiquing |
| Step budget | 20 | Max reasoning steps |
| Web search | Enabled | Agent can search for data |

## Understanding the Output

**LinkedIn Preview Card**:
- Realistic LinkedIn post layout
- Name, headline, and timestamp
- Engagement buttons (Like, Comment, Repost, Send)
- Character count displayed

**Alternative Hooks Section**:
- 3-5 different opening lines tested by the agent
- Useful for A/B testing on social media
- Copy any hook to test different angles

## Best Practices

### Topic Selection
- ✅ **Good**: "3 lessons from my failed AI startup"
- ✅ **Good**: "Why most RAG demos fall apart in production"
- ❌ **Avoid**: "AI is cool" (too vague)

### Tone Guidance
- **Professional**: Expert insights, industry data, career advice
- **Casual**: Personal stories, conversational, friendly
- **Thought Leadership**: Contrarian takes, bold predictions
- **Humorous**: Witty observations, self-deprecating stories

### Quality Scores
- **0-3**: Rough, needs major work
- **4-5**: Decent foundation, needs polish
- **6-7**: Good, ready to post
- **8+**: Excellent, highly shareable

## Advanced Tips

1. **Specific Claims**: Agent won't cite made-up statistics; set "Use web search" to ON
2. **Hook Variants**: Agent explores different angles automatically; check the alternative hooks
3. **Audience Mismatch**: If posting for CTO audience, explicitly state it
4. **Testing Tone**: Try 2-3 different tones with the same topic to see what resonates
5. **Step Budget**: Set higher (25-30) if you want more revision cycles; lower (12-15) for speed

## Cost

Approximate costs per post:
- **Quick post** (gpt-4o-mini, 12 steps): ~$0.10–0.25
- **Standard post** (gpt-4o, 15-20 steps): ~$0.30–0.80
- **Polished post** (gpt-4o, 25+ steps): ~$1.00–2.00

*Costs include research, drafting, critiques, and revisions.*

## Architecture

**Frontend**: Single-file HTML/CSS/JavaScript (no dependencies beyond browser APIs)

**Integrations**:
- OpenAI Chat API (gpt-4o, gpt-4o-mini)
- Web search via Perplexity API
- No backend required

**Agent Toolset**:
- `web_search(query)` - Research topic
- `save_note(note)` - Interim note-taking
- `write_draft(draft)` - Create post
- `get_critique(draft)` - Send to critic for scoring
- `deliver_post(post, alt_hooks)` - Finalize with alternatives

## Common Scenarios

### Scenario 1: Controversial Take
```
Brief: "Hot take on why we don't need another ML framework"
Tone: Thought Leadership
Min score: 7
```
The critic will challenge bold claims; agent will refine to be defensible.

### Scenario 2: Personal Story
```
Brief: "Why I left my FAANG job"
Tone: Casual
Min score: 6
```
Agent balances relatability with professionalism; won't bash ex-employer.

### Scenario 3: Product Launch
```
Brief: "We're launching our new bootcamp module for AI engineers"
Tone: Professional
Min score: 7
Include hashtags: Yes
```
Agent creates newsworthy angle, minimal hype language, includes CTAs.

## Error Handling

| Error | What Happens | Recovery |
|-------|-------------|----------|
| API key invalid | Clear error message | Re-enter key, try again |
| Search fails | Agent notes it, proceeds from knowledge | Re-run or disable search |
| Critic unavailable | Agent uses own judgment | Continue iterating |
| Step budget exhausted | Delivers best draft so far | Increase budget and retry |

## Privacy

- **No storage**: API keys sent only to OpenAI; not logged or persisted
- **Browser-only**: All computation happens client-side
- **Session-scoped**: Content cleared on page refresh
- **HTTPS recommended**: Ensure secure connection before pasting API key

## Limitations

- Posts are optimized for LinkedIn, not all platforms
- Agent won't cite statistics it didn't find in search results
- No image insertion (post text only)
- Character limit enforced (~1800 max)
- No direct LinkedIn API integration (copy/paste to LinkedIn.com)

## Future Ideas

- [ ] Direct LinkedIn API integration for one-click posting
- [ ] Platform-specific variants (Twitter, Bluesky, Threads)
- [ ] Performance metrics from previous posts
- [ ] Team collaboration mode (critique from colleagues)
- [ ] Scheduling integration

## License

MIT

## Contributing

Found a bug or have a feature idea? Open an issue or PR.
