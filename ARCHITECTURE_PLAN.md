# Roger's Guide — Architecture & Build Plan

**Project**: A personal, interactive web guide for Roger King (77) to learn AI, social media, and modern technology.
**Built by**: Philip King (his son) via Claude
**Deployment**: Vercel static site — Roger bookmarks the URL or adds it to his home screen
**Context Document**: See `Roger_King_Tech_Guide_Handoff.md` for all business context (Commission Army, Bay Angels, Chief People, Philip's Claude portfolio, Roger's background). Do NOT duplicate that content here — reference it and weave it into the guide naturally.

---

## 1. DESIGN DIRECTION

### Aesthetic: "Warm Editorial"
Think: a beautifully typeset personal magazine made just for one person. Not corporate. Not techy. Not a SaaS dashboard. This should feel like opening a handcrafted book that happens to live on a screen.

**Tone**: Warm, inviting, patient, personal. This is a gift from a son to his father.

**Key design principles**:
- **Generous whitespace** — nothing should feel crowded or rushed
- **Large, readable typography** — Roger is 77. Body text minimum 18px, headings should be bold and clear
- **Warm color palette** — think deep navy (#1a2744), warm cream/ivory (#faf8f5), gold/amber accents (#c8956c or similar), with a soft sage or muted teal as a secondary accent. NO harsh whites, NO neon, NO purple gradients.
- **Subtle texture** — light paper-like grain on backgrounds, soft shadows, nothing flat and sterile
- **Photography-inspired** — Roger is a photographer. The aesthetic should subtly honor that. Think: gallery-like spacing, careful framing of content blocks, perhaps subtle film-grain overlays or darkroom-inspired color shifts in section headers
- **Motion with restraint** — smooth page transitions, gentle fade-ins on scroll, subtle hover states on cards. Nothing jarring. Nothing that moves when you don't expect it to.

### Typography
- **Display/Headings**: Something with character — a refined serif like `Playfair Display`, `DM Serif Display`, or `Lora`. Should feel classic and warm, not cold and geometric.
- **Body**: A highly readable humanist sans like `Source Sans 3`, `Nunito`, or `DM Sans`. Round, friendly, easy on the eyes at large sizes.
- **Monospace (for prompts/code blocks)**: `JetBrains Mono` or `Fira Code` — clean and distinct from body text.
- Load via Google Fonts CDN.

### Layout
- **Mobile-first** (iPhone/iPad primary) but beautiful on Mac too
- Single-page app with smooth route transitions (no full page reloads)
- Persistent navigation: bottom tab bar on mobile (iOS-style), sidebar on desktop/iPad landscape
- Each section is its own "page" within the SPA
- Content within sections uses expandable accordions so Roger isn't overwhelmed by wall-of-text
- Prompt blocks are visually distinct (dark background, monospace, with a big "Copy" button)

---

## 2. TECHNICAL ARCHITECTURE

### Stack
- **Single HTML file** with embedded CSS and JS
- **React 18** via CDN (unpkg or cdnjs)
- **No build step** — this ships as one file
- CSS via `<style>` tags (or CSS-in-JS via React if cleaner)
- Google Fonts loaded via `<link>`
- Deployed to Vercel as a static site

### Routing
- Use React state to manage "pages" (no React Router needed for a single-file app)
- URL hash routing optional (`#getting-started`, `#ai-personal`, etc.) — nice for bookmarking sections
- Smooth transitions between pages (CSS transitions or simple opacity/transform animations)

### Responsive Breakpoints
- **Mobile** (< 768px): Single column, bottom tab navigation, full-width cards
- **Tablet** (768px - 1024px): Two-column card grid on landing, sidebar nav option
- **Desktop** (> 1024px): Sidebar navigation, wider content area, more generous spacing

### Key Components to Build
1. **App Shell** — nav, routing, page container with transitions
2. **Landing Page** — hero greeting + section cards grid
3. **Section Page Template** — reusable layout for all 6 sections (header, intro, accordion content)
4. **Accordion Component** — expandable/collapsible content blocks
5. **Prompt Block Component** — styled code block with copy-to-clipboard button + success feedback
6. **Step-by-Step Component** — numbered steps with icons/illustrations for walkthroughs
7. **Comparison Table Component** — for platform breakdowns, model comparisons
8. **Card Component** — for landing page navigation and project showcases
9. **Back to Top / Home button** — persistent, always accessible

---

## 3. CONTENT STRUCTURE & SECTIONS

### Landing Page

**Hero area**:
- Large greeting: "Hey Roger — welcome to your personal guide to AI, social media, and technology."
- Subtitle: "Built for you by Philip. Take it at your own pace."
- Maybe a subtle animation on load — the text fades in gently, cards stagger in below

**Section Cards** (6 cards, 2x3 grid on tablet/desktop, stacked on mobile):

| Card | Icon/Emoji | Color Accent | Label |
|------|-----------|-------------|-------|
| Getting Started | 🚀 | Gold | "Start Here" |
| AI for Everyday Life | 💬 | Warm blue | "AI — Personal" |
| AI for Business | 📊 | Deep navy | "AI — Professional" |
| Social Media (Personal) | 📸 | Sage/teal | "Social — Personal" |
| Social Media (Professional) | 💼 | Amber | "Social — Professional" |
| Cool Stuff & Tips | ✨ | Accent gold | "Explore" |

Each card: title, 1-line description, subtle hover effect (lift + shadow).

---

### Section 1: Getting Started

**Purpose**: Roger's absolute first steps. Do this before anything else.

**Intro** (2-3 paragraphs):
Welcome Roger. Explain that this section gets him set up with Claude — the AI tool Philip uses every day to build documents, spreadsheets, business plans, and more. Frame it as: "This is the single most useful tool I've found, and I want you to have it too." Tell him it'll take about 10 minutes.

**Content blocks (as numbered steps)**:

**Step 1: Download Claude**
- iPhone/iPad: App Store link (or instructions to search "Claude by Anthropic")
- Mac: Download from claude.ai/download or App Store
- Also available at claude.ai in any web browser
- Include visual callout: "Look for the orange/brown Claude logo"

**Step 2: Sign In**
- Use your Chief People email: roger@chiefpeople.com
- Google sign-in is the easiest method — tap "Continue with Google"
- If he doesn't have a Google account tied to that email, walk through email+password signup

**Step 3: Subscribe to Claude Pro ($20/month)**
- Why: Free tier has message limits that'll frustrate you when you're exploring. Pro removes those limits, gives you access to the best models, and unlocks features like extended thinking.
- How: Settings → Subscription → Upgrade to Pro
- Philip's recommendation: "Just do it. When you're learning, the last thing you want is to hit a wall mid-conversation."

**Step 4: Your First Conversation**
- Include a copy-pasteable "icebreaker" prompt. Something like:

```
Hi Claude — my name is Roger King. I'm 77 years old, I'm the founder of Bay Angels (one of Silicon Valley's oldest angel investment networks), and I'm learning to use AI tools for the first time. My son Philip set me up with you.

Can you introduce yourself, tell me what you're capable of, and suggest three things I could ask you about right now that would show me what you can do? Keep it simple and conversational — I'm just getting started.
```

- Explain what will happen: Claude will respond conversationally, suggest things, and Roger can just... keep talking.

---

### Section 2: AI for Everyday Life (Personal)

**Purpose**: Make Claude feel approachable and useful for non-business, everyday things.

**Intro**: "Claude isn't just for work. Think of it as a patient, knowledgeable friend who's available 24/7, never judges your questions, and never gets tired of explaining things."

**Sub-sections (accordions)**:

**What is Claude?**
- Not a search engine — it's a conversation
- It doesn't browse the internet by default (unless you ask it to search) — it knows things from its training
- It can read documents, analyze spreadsheets, write content, help you think through problems
- Simple analogy: "Imagine you could call someone who's read every book, every manual, every article — and they're infinitely patient. That's Claude."

**Chat vs. Cowork vs. Voice Mode**
- Build a clean comparison table:

| Feature | Chat | Cowork | Voice |
|---------|------|--------|-------|
| What it is | Text conversation | Claude works with your files | Talk to Claude like a phone call |
| Best for | Questions, writing, thinking through ideas | Building documents, spreadsheets, multi-step projects | Quick questions, brainstorming, hands-free use |
| Capacity | Full power | Full power + file access | More limited — conversational only |
| Where to find it | Main Claude interface | Claude desktop app | Microphone icon in Claude app |

- Philip's take: "Start with Chat. Try Voice when you're comfortable — it's fun and engaging. Graduate to Cowork when you want Claude to actually build things for you."

**Voice Mode Deep Dive**
- How to use it: tap the microphone icon
- What it's great for: asking questions while doing other things, having a brainstorming conversation, getting explanations read aloud to you
- What it can't do: it doesn't have the same depth as Chat. It can't read your files, build documents, or do multi-step complex work.
- Roger will probably love this — it's the most natural way to interact. Frame it as: "Think of Voice as chatting with Claude. Think of Chat as emailing Claude. Both useful, different purposes."

**Basic Prompting Guide — "Better Questions, Better Answers"**
Frame this as 6 simple rules:

1. **Be specific** — "Help me plan a trip" → "Help me plan a 5-day photography trip to Cuba in March, budget $3,000, focused on street photography in Havana"
2. **Give context** — Tell Claude who you are, what you're working on, and why. It doesn't know you unless you tell it.
3. **Tell Claude what you want** — A list? A paragraph? A step-by-step guide? A spreadsheet? Say so.
4. **Ask follow-ups** — The first answer isn't always the best. Say "Can you go deeper on point 3?" or "Make it simpler" or "Give me an example."
5. **Start new conversations for new topics** — Don't try to cram everything into one chat. Fresh conversations get cleaner results.
6. **Don't be afraid to experiment** — You can't break anything. The worst that happens is you get an answer you don't love, and you try again.

Include a before/after example:
- Bad: "Tell me about angel investing"
- Good: "I'm the founder of Bay Angels, an angel investment network in Silicon Valley that's been operating since 1998. I want to write a LinkedIn post explaining what angel investing is to people who've never heard of it. Keep it under 200 words and make it conversational, not academic."

**The House Manual Prompt**
This is Roger's "aha moment" — a real, detailed prompt he can paste into Claude that will produce something genuinely useful.

```
I need you to create a comprehensive house manual for guests who are renting or staying at my home. This should be warm and welcoming but thorough.

Please include the following sections:

1. **Welcome & Overview** — A warm greeting, brief description of the home, and what makes it special
2. **Arrival & Access** — How to get in (lockbox code, key location, parking instructions, gate code if applicable)
3. **Wi-Fi & Technology** — Network name, password, how to use the TV/streaming setup, smart home devices if any
4. **Kitchen & Appliances** — How to use the coffee maker, dishwasher, oven, any quirky appliances. Where to find dishes, utensils, trash bags, etc.
5. **Heating & Cooling** — How to operate the thermostat, ceiling fans, fireplace if applicable
6. **Outdoor Spaces** — Pool/hot tub instructions, grill, patio furniture, garden
7. **House Rules** — Quiet hours, smoking policy, pet policy, maximum occupancy, shoes on/off
8. **Local Recommendations** — Nearby restaurants, grocery stores, pharmacies, gas stations, beaches/parks, hidden gems
9. **Emergency Information** — Emergency contacts, nearest hospital, fire extinguisher location, first aid kit, circuit breaker
10. **Checkout Procedures** — What to do before leaving (trash, dishes, linens, lockup, thermostat settings)

Format this as a clean, professional Word document with clear headings and a friendly but informative tone. Leave placeholder brackets [like this] anywhere I need to fill in specific details like addresses, codes, or names. Make it feel like a high-end Airbnb experience.
```

- Include a note: "Paste this into Claude Chat (or Cowork if you want it to create an actual Word document file). Fill in the [brackets] with your specific details. You'll have a professional guest manual in about 60 seconds."

**More Things to Try**
Quick list with one-line descriptions:
- Plan a road trip ("Plan a 7-day driving trip from San Francisco to...)
- Get a recipe ("I have salmon, asparagus, and lemons. What should I make for dinner?")
- Write a letter or email ("Help me write a thank-you note to...")
- Research a topic ("Explain blockchain to me like I'm completely new to it")
- Organize your thoughts ("I'm trying to decide between X and Y. Help me think through the pros and cons")

---

### Section 3: AI for Business (Professional)

**Purpose**: Show Roger how Claude becomes a business partner. This is where the real power is.

**Intro**: "This is where Claude goes from helpful to transformative. Philip has used Claude to build entire business plans, financial models, pitch coaching strategies, and marketing campaigns. Here's how — and here are the exact prompts you can use to do the same."

**Sub-sections (accordions)**:

**Understanding the Models — Sonnet vs. Opus**

Plain English explanation:
- **Sonnet 4.5** — Fast, smart, great for 90% of things. Think of it as a very talented analyst who works quickly.
- **Opus 4.5** — The heavy hitter. Slower, more expensive (uses more of your message quota), but significantly more powerful for complex reasoning, nuanced writing, and strategic thinking. Think of it as a senior partner who takes their time but delivers exceptional work.
- **Extended Thinking** — A mode you can turn on for either model. It lets Claude "think before speaking" — working through the problem step by step before giving you an answer. Makes both models significantly better.

**Philip's recommendation**: "Use Sonnet 4.5 with Extended Thinking for 9 out of 10 things. It's fast, it's smart, and it handles almost everything you'll throw at it. Switch to Opus 4.5 with Extended Thinking when you're working on something really important — a pitch deck, a business plan, a critical email, a strategic decision. That's your heavy artillery."

Include a simple decision guide:
- Writing an email? → Sonnet
- Planning a trip? → Sonnet
- Building a business plan? → Opus
- Drafting a pitch deck? → Opus
- Quick questions? → Sonnet
- Complex financial analysis? → Opus
- Not sure? → Start with Sonnet. If the answer isn't deep enough, switch to Opus.

How to switch: explain where the model selector is in the Claude interface.

**Chat vs. Cowork — The Deep Dive**

Explain what Cowork can do that Chat can't:
- Create actual files (Word docs, Excel spreadsheets, PDFs, presentations)
- Work with files you upload
- Execute multi-step tasks (research → analyze → build document → refine)
- Access your computer's file system (with permission)
- Build things that live on your desktop, not just in the chat

Philip's quote: Cowork is "perhaps the most impactful thing that's happened in AI in the past six months... knocked dozens of startups completely out of the water."

Frame it as: Chat is for conversations. Cowork is for getting work done.

**Advanced Prompting Guide**

Building on the basics from Section 2, add:

1. **Give Claude a role** — "You are a financial analyst with 20 years of experience in SaaS metrics..." This focuses the response.
2. **Use structured requests** — Break complex asks into numbered sections. "I need you to: 1) Analyze X, 2) Compare Y, 3) Recommend Z"
3. **Provide examples** — "Here's an example of what I'm looking for: [example]. Now do something similar for my situation."
4. **Iterate, don't restart** — If the first draft is 70% right, say "This is good, but change the tone to be more conversational" or "Expand section 3 and shorten section 1." Build on what Claude gives you.
5. **Set constraints** — "Keep it under 500 words." "Use bullet points." "Write it at an 8th-grade reading level." "No jargon."
6. **Ask Claude to think step by step** — "Walk me through your reasoning before giving me a recommendation." This produces much better answers for complex questions.
7. **Chain conversations** — Start with research ("What are the best practices for X?"), then move to application ("Now, using those best practices, build me a Y"), then refinement ("Great, now make it more Z").

**The Commission Army Financial Model Prompt**

The crown jewel. A comprehensive prompt that builds a full Excel financial model. Reference the handoff doc for all the business details — the prompt should incorporate Commission Army's actual numbers.

```
I need you to build a comprehensive Excel financial model for Commission Army, a two-sided referral marketplace platform. This should be a professional, investor-ready spreadsheet with the following tabs:

**Tab 1: Revenue Model**
- Monthly projections for 24 months
- Two revenue streams: subscription fees ($10/month individual referrers after first 1,000 free; $49.95/month businesses after first 100 free) and transaction fees (20% take rate on all referral commissions flowing through the platform)
- Inputs at the top for: monthly new referrer signups, monthly new business signups, average transaction value per successful referral, referral conversion rate (leads submitted → deals closed), monthly churn rate for each segment
- Monthly Recurring Revenue (MRR) calculation
- Annual Recurring Revenue (ARR) projection
- Show free tier users vs. paid tier separately

**Tab 2: Customer Acquisition Cost (CAC) Model**
- Marketing spend by channel (content marketing, paid social, events/partnerships, referral incentives)
- CAC calculation by segment (referrers vs. businesses)
- CAC trend graph showing how CAC changes as marketing spend increases
- LTV:CAC ratio tracking (target: 3:1 minimum)
- CAC payback period in months
- Show diminishing returns curve — as you spend more per channel, cost per acquisition rises

**Tab 3: Subscriber Growth Dashboard**
- Cumulative referrers and businesses over 24 months
- Growth curves (S-curve modeling for marketplace network effects)
- Monthly active users vs. total registered
- Net revenue retention
- Churn waterfall: new adds, churned, reactivated, net

**Tab 4: Hiring Plan & Operational Costs**
- Monthly headcount plan for 24 months
- Roles: Founder(s) (unpaid initially), CTO/Lead Engineer (Month 3-4 post-funding), Marketing hire (Month 4-6), Ops/Support hire (Month 6-8), first salesperson (when?), customer service (when?)
- Trigger thresholds for each hire: "Hire a support person when monthly tickets exceed X" / "Hire a salesperson when inbound leads exceed Y"
- Fully loaded cost per employee (salary + benefits + overhead at 1.3x multiplier)
- Contractor vs. full-time decision framework
- Total monthly burn rate

**Tab 5: Fundraising & Runway**
- Seed round: $500,000
- Use of funds breakdown: Product Development 40%, Go-to-Market 30%, Operations 20%, Reserve 10%
- Monthly cash flow (revenue minus expenses)
- Runway calculation: months until cash runs out at current burn
- Breakeven analysis: what month does revenue cover expenses?
- Key insight section: "Why raising $100K today is different from 3 years ago or 10 years ago" — include a comparison showing how AI tools (vibe coding, Claude for ops) mean you can build an MVP with $0 in engineering spend, making seed money about growth, not about building the initial product

**Tab 6: Summary Dashboard**
- Key metrics at a glance: MRR, ARR, total users, burn rate, runway, LTV:CAC
- Month 18 targets: 1,500 businesses, 25,000 referrers, $375K monthly transaction volume, $75K monthly platform revenue
- Traffic light indicators: green/yellow/red for each KPI vs. target
- Path to Series A readiness: $200K+ monthly revenue, LTV:CAC > 3:1

**Formatting requirements:**
- Professional formatting with consistent colors, borders, and number formatting
- Currency formatted as $X,XXX
- Percentages formatted consistently
- Input cells highlighted in light yellow so Roger knows what to change
- Charts embedded in each tab where relevant (line charts for growth, bar charts for comparisons, waterfall for churn)
- Print-friendly layout
- Freeze panes on headers

Make all assumptions explicit and adjustable. Use the input cells approach so Roger can change assumptions and watch the model update automatically. Include a small "Assumptions" box at the top of each tab listing the key inputs and their default values.
```

**What Philip Has Built with Claude — Showcase**

Display as a gallery of cards. Each card has:
- Project name
- 1-line description
- What Claude feature was used (Chat, Cowork, etc.)
- A subtle visual indicator of the type (document, spreadsheet, presentation, research)

Projects to include (pull details from the handoff doc):
- Commission Army Business Plan (full 12-section business plan)
- Roger King Pitch Coaching Credentials Research
- Guiding Angels / Pitch to an Angel Launch Strategy
- Roger King Judging Dossier (for pitch competition prep)
- Bay Angels Pitch Scoring Rubric (10-criterion weighted system)
- Client Social Media Reach Spreadsheet (55 international clients, 17 regions)
- Bay Angels Submission Spreadsheet Redesign
- Linda and Bob Cord-Cutting Guide (elderly clients, cable → streaming)
- Roger's Photography Retrospective Presentation

Closing message for this section: "Roger — all of this was built with Claude. Every single item. Philip's been using this tool every day for months, and this is what's possible. You won't get here overnight, and you don't need to. Start with the basics, try the prompts in this guide, and build from there. The point isn't to match what Philip does — it's to see what's possible and find the parts that are useful to YOU."

---

### Section 4: Social Media — Personal

**Purpose**: Get Roger comfortable with social platforms for sharing his personal interests (photography, Cuba trips, cars).

**Intro**: "Social media isn't about becoming an influencer. For you, it's about sharing the things you love — your photography, your trips to Cuba, your car projects — with the people who care about them."

**Sub-sections (accordions)**:

**Platform Breakdown**

Build as visual cards, one per platform:

**Facebook**
- Purpose for Roger: Sharing memories with friends and family
- Audience potential: Not a growth platform anymore — your audience is people you already know
- What to post: Trip photos, family updates, life milestones, car project updates
- Bottom line: Keep using it casually. It's a digital photo album for your existing circle.

**Instagram**
- Purpose for Roger: THE platform for his photography and visual storytelling
- Audience potential: Strong — especially for photography and travel content. Everyone's on it.
- What to post: Photos from Cuba trips, car projects, fine art photography, behind-the-scenes of Bay Angels events
- Key features: Posts (permanent), Stories (disappear after 24 hours), Reels (short videos — this is where growth happens)
- Bottom line: This should be Roger's primary personal platform. His photography deserves to be seen.

**TikTok**
- Purpose for Roger: Short-form video, the most viral platform
- Audience potential: Massive, but skews younger. That said, older creators with authentic content often do extremely well (the contrast is part of the appeal)
- Key feature: **AutoCut** — TikTok can automatically edit your long videos into short clips. You film something, and TikTok chops it up for you.
- The big insight: **Authentic posting beats professional posting every time.** Posting a real, unpolished clip of yourself working on a car or walking through Havana will outperform a professionally produced video. The algorithm rewards consistency and authenticity. Post daily or 3-4x/week and your audience WILL grow.
- Bottom line: Worth exploring, especially for video content. The built-in editor makes it surprisingly easy.

**LinkedIn** (brief — full treatment in Professional section)
- Purpose for Roger: Professional audience growth, pitch coaching credibility
- More detail in the Professional Social Media section

**Getting Started on Instagram — Step by Step**

Walk through every step:
1. Download Instagram from the App Store (include what the icon looks like)
2. Open it and tap "Log in" (not "Create new account")
3. Tap "Continue with Facebook" — this will connect to your existing account
4. Your handle is something with "Havana" in it — [PLACEHOLDER: confirm exact handle]. If you can't find it, that's okay — we can recover it.
5. You're in! Here's what you're looking at — explain the home feed, the search/explore page, the + button for posting, your profile

**Post Your First Photo**
1. Tap the + button at the bottom center
2. Select "Post"
3. Choose a photo from your camera roll — pick one of your Cuba shots
4. Optional: apply a filter (subtle ones like "Clarendon" or "Juno" look great for photography)
5. Write a caption — keep it simple. "Havana, 2023. One of my favorite streets to photograph." Add a few hashtags: #Cuba #Havana #StreetPhotography #Travel
6. Tap "Share"
7. You just posted! It's now visible to anyone who follows you and anyone who searches those hashtags.

**Post Your First Reel (Short Video)**
1. Tap the + button, select "Reel"
2. You can record a new video OR select an existing video from your camera roll
3. The editor lets you: trim the clip, add text overlay, add music from Instagram's library
4. Keep it under 30 seconds for your first one
5. Add a caption and share
6. Reels get shown to people who DON'T follow you — this is how you grow

**The Built-In Editors**
- Both Instagram and TikTok have editing tools built right in. You don't need Premiere Pro or Final Cut.
- Instagram editor: trim, filters, text, music, stickers
- TikTok editor: trim, text, effects, music, **AutoCut** (automatically edits long videos into short clips)
- Frame it as: "If you can use a smartphone camera, you can use these editors. They're designed for everyone."

---

### Section 5: Social Media — Professional

**Purpose**: Connect LinkedIn to Roger's professional goals (pitch coaching, Bay Angels credibility, Commission Army).

**Intro**: "Here's where social media becomes a business tool. You've spent 30 years building an incredible network and reputation in Silicon Valley. LinkedIn lets you turn that reputation into an audience — and an audience into clients."

**Sub-sections (accordions)**:

**LinkedIn: Your Professional Platform**

Why LinkedIn matters for Roger:
- He founded one of Silicon Valley's oldest angel groups
- He's judged startups on three continents (Beijing, Seoul, Tokyo, Prague, Athens, Havana)
- He's been published in Forbes and Fortune, appeared on CNN
- He has a testimonial from a founder he helped raise funds
- All of this is GOLD on LinkedIn — but only if people see it

How consistent posting works:
- The LinkedIn algorithm rewards frequency. Posting 3-5x/week dramatically increases visibility.
- Every post is seen by your connections AND by people in their network
- Over time, followers compound. 100 becomes 500 becomes 2,000. Each new follower is a potential coaching client.

What to post:
- Pitch coaching insights: "I've reviewed 5,000+ pitch decks. Here are the 3 mistakes I see in 90% of them."
- Bay Angels stories: "We first invested in OpenTable when it was little more than an idea on a napkin."
- Founder advice: "I can tell in 90 seconds if a founder knows their business. Here's what I'm looking for."
- Event recaps: Photos and takeaways from Bay Angels events
- Personal reflections: "I started Bay Angels in 1998 in Sausalito. Here's what I've learned in 27 years."

The key insight: Every post is a micro-pitch for the Guiding Angels / Pitch to an Angel coaching services. You're not selling — you're demonstrating credibility. People will come to you.

**Authentic vs. Professional Posting**

The counterintuitive truth:
- Spending money on professional content (produced videos, designed graphics, paid campaigns) often produces zero results on LinkedIn
- Authentic, text-based posts with real stories and real opinions consistently outperform polished content
- The algorithm rewards engagement (comments, shares), and people engage with authentic voices, not marketing material
- Roger's real stories (angel investing since 1995, building ChiefPeople to 135 employees, judging in Havana and Seoul) are infinitely more compelling than any designed graphic

**Audience = Opportunity**

Simple framework:
- Followers → Credibility → Inbound leads → Paying clients
- For Roger: LinkedIn followers who see his pitch coaching content → some of them are founders → some need coaching → they reach out → paying clients at $250/hour
- This is the pipeline for Guiding Angels / Pitch to an Angel
- It's also the pipeline for Commission Army awareness ("I'm building a referral marketplace — here's why")

**Platform Purpose Summary**

Clean reference table:

| Platform | Personal Use | Professional Use |
|----------|-------------|-----------------|
| Facebook | Share memories with friends/family | Not useful professionally |
| Instagram | Photography, travel, car projects | Bay Angels event promotion |
| TikTok | Fun video content, virality | Possible thought leadership clips |
| LinkedIn | Not primary for personal | Pitch coaching pipeline, Bay Angels credibility, Commission Army awareness |

---

### Section 6: Cool Stuff & Tips

**Purpose**: Keep Roger coming back. Show him the edges of what's possible. Make it fun.

**Intro**: "This section is just for fun. These are things that might surprise you, delight you, or make you say 'wait, it can do THAT?'"

**Content ideas (as cards or tiles he can click)**:

**Voice Mode Tricks**
- Ask Claude to explain something complex while you're driving or cooking
- Have Claude quiz you on a topic ("Quiz me on angel investing terminology")
- Use it for brainstorming — just talk through an idea out loud
- Practice a pitch with Claude playing the role of a skeptical investor

**Things You Didn't Know Claude Could Do**
- Read and analyze a PDF you upload ("Here's a pitch deck — what are the strengths and weaknesses?")
- Analyze a spreadsheet ("Here's my expenses spreadsheet — where am I overspending?")
- Write code (this is how Philip built the Commission Army MVP)
- Create professional presentations, Word documents, and spreadsheets
- Help you write emails in a specific tone
- Translate between languages
- Explain your medical test results in plain English

**Fun Prompts to Try**
Include copy-pasteable prompts:
- "I'm a photographer who leads trips to Cuba. Write me a 60-second elevator pitch for my photography workshops that I could give at a networking event."
- "I founded one of Silicon Valley's oldest angel investment groups. Write me a short bio for LinkedIn that sounds credible but not stuffy."
- "Explain cryptocurrency to me like I'm a smart person who just hasn't been paying attention to it."
- "I'm 77 and I want to start posting on Instagram. Give me 10 post ideas based on my interests: photography, classic cars, Cuba travel, and angel investing."

**The "Wow Moment" Prompt**
One single prompt designed to genuinely impress:

```
I want you to analyze my professional background and tell me what business opportunities I'm missing.

Here's my background: I'm Roger King, 77 years old. I founded Bay Angels in 1998 — one of Silicon Valley's oldest angel investment networks. I've personally reviewed thousands of pitch decks over 30 years. I've judged startup competitions on three continents (Beijing, Seoul, Tokyo, Prague, Athens, Havana). I've been published in Forbes and Fortune and appeared on CNN multiple times discussing startup culture. I built a recruiting company (ChiefPeople) to 135 employees before the dotcom crash. I'm currently developing a startup called Commission Army (a referral marketplace) and I offer pitch coaching through a venture called Pitch to an Angel.

Based on this background, what are the top 5 business opportunities I should be pursuing that I might not have considered? Think creatively — consider speaking, publishing, consulting, digital products, partnerships, and anything else that leverages my unique background. For each opportunity, estimate the potential revenue and explain why it's a good fit.
```

---

## 4. GLOBAL FEATURES

### Copy-to-Clipboard Prompt Blocks
Every prompt in the guide should be in a visually distinct block (dark background, monospace font, clear border) with a prominent "Copy" button. When clicked:
- Copy text to clipboard
- Button briefly changes to "Copied! ✓" with a green flash
- Returns to normal after 2 seconds

### Search / Quick Find (Nice to Have v1)
A search bar at the top that filters across all sections. Type "Instagram" and it highlights/navigates to Instagram-related content.

### Progress Tracking (Nice to Have v1)
Light checkboxes on each section/sub-section. Roger can mark things as "done" as he works through the guide. State persisted in localStorage.

### Print-Friendly Prompt Pages (Nice to Have v2)
A "Print this prompt" button that opens a clean, print-formatted version of just the prompt block.

### Dark Mode Toggle (Nice to Have v2)
For late-night reading. Toggle in the nav.

---

## 5. DEPLOYMENT

### Vercel
- Deploy as a static site (single index.html)
- Custom subdomain if available (rogers-guide.vercel.app or similar)
- Roger accesses via URL → adds to iPhone/iPad home screen via Safari "Add to Home Screen"
- Include a note in the Getting Started section about how to add a home screen shortcut

### PWA-Ready (Nice to Have v1)
Add a basic manifest.json and service worker so it behaves like a native app when added to home screen:
- Custom icon
- Full-screen mode (no browser chrome)
- Offline capability for cached content

---

## 6. NICE-TO-HAVES (FUTURE VERSIONS)

### v1.1
- Search/filter across all sections
- Progress tracking (checkboxes with localStorage)
- PWA support (home screen icon, full-screen mode)
- Smooth scroll-to-section from landing page cards

### v1.2
- Dark mode toggle
- Print-friendly prompt pages
- "Share this prompt" button (generates a link or copies formatted text)
- Expandable "Roger's FAQ" section with common questions he'll have

### v2.0
- Interactive prompt builder — Roger fills in fields (topic, tone, length) and the guide assembles a prompt for him
- Video walkthroughs embedded (screen recordings of how to do things in Claude)
- Integration with Roger's actual accounts (show his Instagram feed, LinkedIn post count, etc.)
- AI-powered "Ask the guide" — a Claude-powered chat widget embedded in the site that can answer questions about the guide content
- Commission Army dashboard — live data from the platform once it's built

---

## 7. BUILD INSTRUCTIONS FOR CODING AGENT

### What to build
A single `index.html` file containing all React components, CSS, and content. This file will be deployed to Vercel as a static site.

### Key requirements
1. **Mobile-first responsive design** optimized for iPhone, iPad, and Mac
2. **Warm editorial aesthetic** — see Section 1 for full design direction
3. **All 6 sections fully built** with all content from Section 3
4. **All prompts** included as copy-pasteable blocks with copy buttons
5. **Smooth navigation** — SPA with page transitions, persistent nav
6. **Accordion components** for sub-sections to prevent content overwhelm
7. **Big, readable text** — 18px minimum body, generous line-height and spacing

### What NOT to do
- Don't make it look like a SaaS dashboard
- Don't use purple gradients, neon colors, or dark mode by default
- Don't use generic fonts (Inter, Roboto, Arial)
- Don't make the navigation confusing — Roger should always know where he is and how to get home
- Don't use technical jargon in the content — write for a 77-year-old who is smart but not tech-native
- Don't skimp on content — every section should have real, substantive, useful content

### What to optimize for
- Readability above all else
- Touch targets for iPad/iPhone (minimum 44px)
- Fast load time (everything in one file, minimal external dependencies)
- The feeling of receiving a personal gift, not reading a manual

### Creative freedom
The coding agent should feel free to:
- Choose the exact color values within the warm palette described
- Add subtle animations, hover effects, and micro-interactions that feel delightful
- Make creative typography choices within the serif heading + humanist sans body framework
- Add visual flourishes (subtle grain, paper texture, photography-inspired elements)
- Improve the layout beyond what's described here if a better approach exists
- Add small delightful touches (a personal message from Philip somewhere, a subtle camera icon motif honoring Roger's photography, etc.)

---

*This plan references the `Roger_King_Tech_Guide_Handoff.md` document for all business context (Commission Army, Bay Angels, Chief People, Roger's background, Philip's Claude portfolio). The coding agent should read that document before building.*
