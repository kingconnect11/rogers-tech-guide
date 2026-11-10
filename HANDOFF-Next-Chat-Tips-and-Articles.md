# Handoff: Adding Tips, Tricks, and Articles to Roger's Tech Guide

## Context for the Next Chat

You're working on **Roger's Tech Guide** — a single-page React app (`index.html`) that Philip King built for his father Roger King (77). It teaches Roger how to use AI (Claude), social media, and technology.

**Read CLAUDE.md first** — it has the complete architecture, design system, and instructions for how to add content.

The site is a single `index.html` file with inline CSS and React components transpiled via Babel Standalone. There's no build step.

## Your Task

Add more specific tips, tricks, and articles across all sections of the guide. The goal is to make each section richer with practical, actionable content Roger can use immediately.

## Deliverable Format

All content goes into `index.html` as new `<Acc>` (accordion) components within the existing section functions (S1 through S7, plus SGuide and SPhilipAI). Here's the pattern:

```jsx
<Acc title="Your Tip Title" id="unique-id" prog={prog} toggle={toggle}>
  <p>Explanation text.</p>

  {/* Optional: a prompt Roger can copy-paste into Claude */}
  <Setup model="Sonnet 4.6" mode="Chat" features={['Extended Thinking']}/>
  <PB text={`The prompt text here. Use \n for line breaks.`}/>

  {/* Optional: a callout box */}
  <div className="co"><div className="co-l">Philip's take</div><p>Personal note from Philip.</p></div>

  {/* Optional: step-by-step instructions */}
  <Steps steps={[
    {title:'Step name', content:<p>Step description.</p>},
  ]}/>
</Acc>
```

### Key Rules
- Every `<Acc>` `id` must be unique across the entire app
- Use `Sonnet 4.6` (not 4.5) for fast/standard model references
- Use `Opus 4.6` for complex/important model references
- Write in Philip's voice — warm, encouraging, never condescending
- Roger is 77, founder of Bay Angels, photographer — he's accomplished, just new to tech
- Include the `prog` and `toggle` props if the accordion should have a progress checkbox

## Content Ideas by Section

### Getting Started (S1)
- Keyboard shortcuts and voice dictation tips for typing prompts
- How to organize conversations (naming, starring)
- How to share a Claude conversation with someone

### AI for Everyday Life (S2)
- Medical appointment prep: "I have a doctor's appointment about X, help me prepare questions"
- Gift ideas prompt: "Help me find a gift for [person] who likes [interests], budget $X"
- Recipe scaling and meal planning
- Explaining financial statements or tax documents
- Writing condolence notes, congratulations, difficult emails

### AI for Business (S3)
- Competitive analysis prompt
- Meeting prep: "I'm meeting with [person/company], brief me"
- Contract review basics
- Investor update email template
- Board meeting agenda builder

### Social Media Personal (S4)
- How to use Instagram Stories
- TikTok video tips for beginners
- Photo editing basics on iPhone
- Hashtag strategy explained simply

### Social Media Pro (S5)
- LinkedIn post formula that works
- How to respond to comments professionally
- Building a content calendar
- Turning one piece of content into 5 platform posts

### Travel (S6)
- Restaurant reservation assistant prompt
- Packing list generator by destination/weather
- Flight delay/cancellation response prompt
- Currency and tipping guide generator
- "I'm here right now" — real-time trip assistance prompt

### How Philip Uses AI (SPhilipAI)
- More specific project examples
- Before/after comparisons (old way vs. AI way)
- Time and cost savings breakdowns

### Cool Stuff (S7)
- Use Claude to write a family history or memoir outline
- Photo caption writer for a specific photography style
- "Explain this like I'm smart but new to it" — a universal prompt pattern
- Investment analysis prompt
- Health and wellness research prompts

## Link Previews — Smart External Article Links

If you want to link to external articles (e.g., tutorials, news stories, helpful guides), here are the options:

### Option A: Simple Inline Links (Easiest)
Just use standard `<a>` tags within accordion content:
```jsx
<p>For more on this, see <a href="https://example.com" target="_blank" rel="noopener">this guide from Anthropic</a>.</p>
```

### Option B: Styled Link Cards (Recommended)
Create a simple link card component for richer presentation:
```jsx
function LinkCard({href, title, source, description}) {
  return (
    <a href={href} target="_blank" rel="noopener" style={{
      display:'block', padding:'16px 20px', margin:'12px 0',
      background:'#fff', border:'1px solid var(--border)', borderRadius:'var(--radius)',
      textDecoration:'none', transition:'all var(--transition)',
      borderLeft:'3px solid var(--warm-blue)'
    }} onMouseOver={e=>e.currentTarget.style.boxShadow='var(--shadow-lg)'}
       onMouseOut={e=>e.currentTarget.style.boxShadow='none'}>
      <div style={{fontSize:'11px', fontWeight:700, textTransform:'uppercase',
        letterSpacing:'0.08em', color:'var(--warm-blue)', marginBottom:'4px'}}>{source}</div>
      <div style={{fontFamily:"'Playfair Display',serif", fontWeight:600,
        fontSize:'1rem', color:'var(--navy)', marginBottom:'4px'}}>{title}</div>
      <div style={{fontSize:'14px', color:'var(--text-light)', margin:0}}>{description}</div>
    </a>
  );
}
```

Usage:
```jsx
<LinkCard
  href="https://support.anthropic.com/en/articles/..."
  title="Getting Started with Claude"
  source="Anthropic"
  description="Official guide to setting up and using Claude effectively."
/>
```

### Option C: Open Graph Previews (Advanced — Not Recommended for This Project)
True link previews (like social media cards with thumbnails) require either:
1. A server-side proxy to fetch OG metadata from URLs
2. A third-party service like Iframely or Microlink

Since this is a static single-file app with no backend, this adds significant complexity. **Stick with Option A or B.**

## Deployment

After making changes:
```bash
cd "/Users/iamtheking/Documents/Projects/Roger's Tech Guide"
vercel deploy --prod --yes
```

## Important Notes

- The `images/` directory MUST stay lowercase (see CLAUDE.md for why)
- All images are in `images/` — reference them as `images/filename.jpg`
- Test locally by opening `index.html` in a browser or running `npx serve .`
- The site is hosted on Vercel — it's a static deploy, no build step
