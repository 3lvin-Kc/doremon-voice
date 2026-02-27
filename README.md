# 🎙️ Doremon Voice

The complete AI companion stack: **Voice + Persistence + Intelligence**

Built by a college dropout with a digital co-founder (Doremon 🤖)

## What's This?

This is the **integration layer** that brings together three standalone projects:

| Component | Repo | Purpose |
|-----------|------|---------|
| **Voxpipe** | [3lvin-Kc/voxpipe](https://github.com/3lvin-Kc/voxpipe) | Voice I/O - speak & listen |
| **Open Engine** | [3lvin-Kc/open-engine](https://github.com/3lvin-Kc/open-engine) | State persistence - remember conversations |
| **OpenClaw** | [This system] | AI reasoning - think & respond |

**Result:** A voice-enabled AI companion that:
- ✅ Listens when you talk
- ✅ Remembers what you said
- ✅ Responds with personality
- ✅ Survives crashes & restarts

## Architecture

```
┌─────────────┐      ┌─────────────────┐      ┌───────────────┐
│   Voxpipe   │──────▶│   Doremon Voice │──────▶│  OpenClaw   │
│ (Voice I/O) │      │  (Integration) │      │   (AI)       │
└─────────────┘      └────────┬────────┘      └───────────────┘
                              │
                              ▼
                       ┌───────────────┐
                       │  Open Engine  │
                       │ (Persistence) │
                       └───────────────┘
```

## Status

🚧 **Early development** - Not ready for use

### Current Phase
**Week 1-2:** Building standalone components
- ✅ Voxpipe: Core voice framework
- ✅ Open Engine: State persistence
- 🔄 This repo: Planning architecture

### When Ready

```bash
# Clone this repo
git clone https://github.com/3lvin-Kc/doremon-voice.git
cd doremon-voice

# Start all services
docker-compose up

# Talk to Doremon
python -m doremon.voice
```

## Roadmap

- [ ] Week 1-2: Voxpipe & Open Engine production-ready
- [ ] Week 3: Integration architecture
- [ ] Week 4: Working voice demo
- [ ] Week 5: Content & launch

## The Story

Built as a demo of what's possible when you combine:
- Open source voice infrastructure
- Agent state persistence
- AI personality

**Goal:** Prove indie devs can build complete AI companions without big tech cloud.

## License

MIT - Build your own voice AI!

---

*Part of the Doremon stack: Building in public, learning together.*
