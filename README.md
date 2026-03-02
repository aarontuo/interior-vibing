# Interior Vibing 🏠

AI-powered interior design renderings that solve real problems. Upload a room photo, get a professional redesign with a click-through presentation deck.

**Not generic "modern living room" output.** Every recommendation is specific to your room's architecture, your goal, and real purchasable items with prices.

## What It Does

1. You upload a room photo
2. AI analyzes the space (dimensions, materials, light, fixed elements)
3. You say what you need (Airbnb staging, rental appeal, home sale, personal refresh)
4. Gemini generates a photorealistic redesign rendering
5. You get a polished presentation deck with before/after, analysis, shopping list, and ROI estimates

## Demo

```
You: [uploads bedroom.jpg] "Stage this for Airbnb, warm Scandinavian style, $1,500 budget"

Interior Vibing:
  → Analyzes room: 12×14, north-facing, oak floors, bare walls
  → Writes specific prompt (not "nice modern bedroom")
  → Generates 2K redesign rendering via Gemini
  → Produces 8-slide presentation deck:
    Slide 1: Title (room photo as background)
    Slide 2: Before photo
    Slide 3: Room analysis (stats + best asset / biggest problem)
    Slide 4: Design concept (style + color palette)
    Slide 5: After rendering
    Slide 6: Before → After comparison
    Slide 7: Shopping list (items ranked by ROI)
    Slide 8: Investment summary (budget tiers + payback)
```

## Install

### Claude Code

```bash
# Option 1: Clone directly into your skills directory
git clone https://github.com/yourusername/interior-vibing.git ~/.claude/skills/interior-vibing

# Option 2: Clone into a project
git clone https://github.com/yourusername/interior-vibing.git
cp -r interior-vibing my-project/.claude/skills/interior-vibing

# Option 3: agent-skills-cli (works with Cursor, VS Code, etc.)
npx agent-skills-cli add yourusername/interior-vibing
```

### Claude.ai (Projects)

1. Open a Project → Project Knowledge
2. Upload `SKILL.md` and `scripts/render.py`
3. Upload room photos and start designing

### Any LLM

The `SKILL.md` is model-agnostic. Paste it into system instructions for any LLM that supports code execution. The `render.py` script calls Gemini's API regardless of which LLM orchestrates the workflow.

## Setup

### 1. Get a Gemini API Key (free tier available)

Go to [https://aistudio.google.com/apikey](https://aistudio.google.com/apikey) and create a key.

### 2. Set Your Key

**Option A:** Copy `.env.example` to `.env` and paste your key:

```bash
cp .env.example .env
# Edit .env and replace paste_your_key_here with your actual key
```

**Option B:** Set as environment variable:

```bash
export GEMINI_API_KEY=your_key_here
```

### 3. Install Dependencies

```bash
pip install google-genai Pillow
```

That's it. Upload a room photo and go.

## Models Used

| Task | Model | Why |
|------|-------|-----|
| Room analysis | `gemini-2.5-flash` | Fast, great vision understanding, cost-efficient |
| Image generation | `gemini-3-pro-image-preview` | Nano Banana Pro — reasoning-enhanced, up to 4K, best image quality |

## File Structure

```
interior-vibing/
├── SKILL.md           ← Instructions for Claude (the brain)
├── scripts/
│   └── render.py      ← Gemini API bridge (the hands)
├── .env.example       ← API key template
└── README.md          ← You are here
```

## Manual Usage (without Claude)

The script works standalone:

```bash
# Analyze a room
python scripts/render.py analyze --image room.jpg

# Generate a redesign
python scripts/render.py render \
  --image room.jpg \
  --prompt "King bed with white linen bedding, oak nightstands, brass lamps, 9x12 ivory wool rug, large abstract art in earth tones above headboard" \
  --purpose "airbnb listing" \
  --style "warm scandinavian" \
  --resolution 2K \
  --aspect-ratio 4:3

# Edit specific areas
python scripts/render.py edit \
  --image room.jpg \
  --prompt "Replace the dated brass light fixture with a matte black pendant. Add white linen curtains." \
  --resolution 2K
```

All outputs go to `.stilo-output/` in your current directory.

## Philosophy

> Every recommendation must answer: "Why THIS item, in THIS room, for THIS purpose, at THIS price."

- ❌ "Add a pop of color" → ✅ "Terracotta (#C65D3E) through a linen lumbar pillow and ceramic vase"
- ❌ "Statement piece" → ✅ "40×30 abstract art in earth tones, centered 57 inches from floor"
- ❌ "Modern bedroom" → ✅ 100+ word prompt referencing the room's actual floors, light, and architecture

## License

MIT
