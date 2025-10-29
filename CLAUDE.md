# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is Guttyo's blog and knowledge base repository containing articles primarily about:
- Medical technology and healthcare IT
- AI applications in medicine and pharmacy
- iOS development for healthcare apps
- Technical knowledge for pharmacists

The repository owner is a hospital pharmacist who develops medical iOS apps and writes technical blog posts.

## Content Structure

```
articles/
├── medical/     # Healthcare and pharmaceutical articles
├── ai/          # AI-related articles (medical AI, ChatGPT, etc.)
├── misc/        # Other topics
├── BLOG_RULES.md         # Comprehensive writing rules (primary reference)
├── WRITING_GUIDELINES.md # Additional writing guidelines
└── TEMPLATE.md           # Article template
```

## Article Writing Workflow

### 1. Competitor Analysis Phase

When given a new article topic with keywords:

1. **Search for top 10 competitors** using the main keyword
2. **Extract heading structures** from top-ranking articles
3. **Identify common patterns** across competitors
4. **Design article structure** that:
   - Incorporates common competitor patterns
   - Covers all suggest keywords naturally
   - Addresses user search intent comprehensively

### 2. Writing Phase

**File naming**: `YYYY-MM-DD-article-title.md`

**Critical writing rules** (from `BLOG_RULES.md`):
- **No emojis** (✅❌⭕⚠️📊📋🎯💾🤖 etc.) - AI detection avoidance
- **No half-width spaces** around bold text or elsewhere
- Use proper punctuation (。、)
- JLPT N1 level Japanese
- Minimum 8,000 characters (detailed guides can be 20,000-60,000 characters)
- **Conclusion-first**: Answer the search query at the beginning
- Use headings (##, ###) for structure
- Balance bullet points and prose

**Content quality standards**:
- Cite sources when available
- Mark speculation explicitly ("おそらく", "〜かと思います")
- State "現時点で不明" when information is unavailable
- For medical information: emphasize evidence, avoid diagnosis/treatment instructions
- For technical information: include version info, environment dependencies

**Article structure**:
1. はじめに (Conclusion-first answer to search query)
2. Chapter 1: Background/current situation
3. Chapter 2: Main topic detailed explanation
4. Chapter 3: Concrete examples/practical methods
5. Chapter 4+: Further deep dives
6. まとめ (Summary)
7. さらに学ぶためのリソース (Resources)
8. 参考文献・リソース (References)
9. よくある質問 (FAQ)

### 3. Quality Assurance Phase

**Self-Refine and ReAct Grounding** (CRITICAL):
- Verify all statistics and factual claims via web searches
- Check AI model versions, tool availability, journal policies
- Add verified sources to references section
- Correct any inaccuracies found

**AI Detection Avoidance Checks**:
- Remove all emojis (use Python script if needed)
- Remove half-width spaces
- Vary sentence structure and length
- Avoid AI-typical patterns
- Ensure natural Japanese flow

### 4. Affiliate Integration

**Approved affiliate links**:

**Perplexity AI** (primary promotion):
```
https://plex.it/referrals/860HKTSY
```
- Include 1-3 times per article
- Position as recommended tool, not pushy

**Amazon** (secondary):
- Kindle Unlimited: `https://www.amazon.co.jp/kindle-dbs/hz/signup?tag=yakuzaishi.app-22`
- Audible: `https://www.amazon.co.jp/hz/audible/mlp?tag=yakuzaishi.app-22`
- Place in "さらに学ぶためのリソース" section
- Use suggested phrasing from BLOG_RULES.md

## Git Workflow

### Branch Naming Convention

Development branches **MUST** follow this pattern:
```
claude/<descriptive-name>-<session-id>
```

Example: `claude/add-ai-article-011CUR4uFAt6jmDRXk3Z9NNX`

**CRITICAL**: The branch name must:
- Start with `claude/`
- End with the matching session ID (visible in system context)
- Otherwise, `git push` will fail with 403 error

### Commit Guidelines

**Commit message format**:
```
Title: Brief description

Detailed explanation of changes.

Key features:
- Feature 1
- Feature 2
- Feature 3

🤖 Generated with [Claude Code](https://claude.com/claude-code)

Co-Authored-By: Claude <noreply@anthropic.com>
```

**Push with retry logic**:
- Always use: `git push -u origin <branch-name>`
- On network failures, retry up to 4 times with exponential backoff (2s, 4s, 8s, 16s)

### Pre-Commit Hooks

The repository uses stop hooks. If blocked:
1. Check if untracked files exist
2. Commit and push changes before stopping
3. Ensure branch name matches session ID

## Common Tasks

### Writing a New Article

```bash
# 1. Start on development branch (already created)
git status  # Verify correct branch

# 2. Create article file
# articles/{category}/YYYY-MM-DD-title.md

# 3. Write following workflow:
#    - Competitor analysis
#    - Writing phase
#    - Self-Refine & ReAct grounding
#    - AI detection avoidance

# 4. Commit and push
git add articles/{category}/{file}.md
git commit -m "Add {topic} article with {features}"
git push -u origin claude/{branch-name}
```

### Verifying Article Quality

**Check emoji removal**:
```python
python3 << 'EOF'
with open('articles/{category}/{file}.md', 'r', encoding='utf-8') as f:
    content = f.read()
emojis = ['✅', '❌', '⭕', '⚠️', '📊', '📋', '🎯', '💾', '🤖']
found = {e: content.count(e) for e in emojis if content.count(e) > 0}
if found:
    print("Found emojis:", found)
else:
    print("✓ No emojis found!")
EOF
```

**Verify statistics with web search**:
- Use `WebSearch` tool to verify all numerical claims
- Check tool versions, release dates, accuracy rates
- Update references section with verified sources

## Key Principles

1. **User Intent First**: Design articles to fully answer search queries
2. **Evidence-Based**: Verify all factual claims, especially for medical content
3. **Natural Japanese**: Avoid AI-typical patterns for detection avoidance
4. **Comprehensive Coverage**: Target 8,000+ characters with thorough explanations
5. **Practical Value**: Include actionable prompts, examples, and resources
6. **Transparent Sourcing**: Cite references, mark speculation clearly

## Reference Files

- `articles/BLOG_RULES.md` - Complete writing rules (primary reference)
- `articles/WRITING_GUIDELINES.md` - Additional guidelines
- `articles/TEMPLATE.md` - Article template
- `articles/README.md` - Repository overview
