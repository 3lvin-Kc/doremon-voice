# Integration Architecture

## How The Three Projects Connect

### Voxpipe (Voice Layer)
- **Provides:** Audio capture, TTS output, state management
- **Needs:** Text input to speak, receives audio to transcribe
- **Protocol:** Python function calls

### Open Engine (Persistence Layer)
- **Provides:** Session state, idempotency, crash recovery
- **Needs:** API calls to record actions
- **Protocol:** JSON-RPC over HTTP

### OpenClaw (Intelligence Layer)
- **Provides:** AI reasoning, personality, tool use
- **Needs:** Text input, returns text response
- **Protocol:** Session-based messaging

## Integration Flow

```
┌─────────────────────────────────────────────────────────────┐
│                        Voice Loop                           │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  1. Voxpipe captures audio                                  │
│     ↓                                                       │
│  2. Speech -> Text (STT)                                    │
│     ↓                                                       │
│  3. Send text to OpenClaw                                   │
│     ↓                                                       │
│  4. OpenClaw thinks, responds                               │
│     ↓                                                       │
│  5. Persist in Open Engine                                  │
│     ↓                                                       │
│  6. Text -> Speech (TTS)                                    │
│     ↓                                                       │
│  7. Voxpipe speaks response                                 │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

## State Management

### Conversation State (Open Engine)
```
Session:
  - id: unique session ID
  - start_time: when conversation started
  - status: active | paused | ended
  
Messages:
  - timestamp
  - speaker: user | doremon
  - text: content
  - audio_ref: path to audio file
```

### Audio State (Voxpipe)
```
States:
  - IDLE: Waiting for user
  - LISTENING: Capturing audio
  - PROCESSING: Converting STT
  - THINKING: AI responding
  - SPEAKING: TTS output
```

## API Design

### Voxpipe Interface
```python
class VoiceInterface:
    def listen(self) -> str:
        """Block until audio captured, return transcript"""
        pass
        
    def speak(self, text: str):
        """Speak text, block until done"""
        pass
        
    def interrupt(self):
        """Stop speaking, start listening"""
        pass
```

### Open Engine Interface
```python
class PersistenceInterface:
    def record_message(self, session_id: str, speaker: str, text: str):
        """Persist conversation"""
        pass
        
    def get_context(self, session_id: str, limit: int = 10) -> str:
        """Get conversation history for AI context"""
        pass
```

### OpenClaw Interface
```python
class AIInterface:
    def respond(self, user_input: str, context: str) -> str:
        """Generate AI response"""
        pass
```

## Integration Package

```
doremon-voice/
├── src/
│   ├── voice/           # Voxpipe wrapper
│   ├── persistence/     # Open Engine client
│   ├── ai/             # OpenClaw interface
│   └── coordinator.py  # Orchestrates the flow
├── tests/
│   ├── test_voice.py
│   ├── test_persistence.py
│   └── test_integration.py
├── examples/
│   └── simple_demo.py
└── docker-compose.yml
```

## Next Steps (Blocked)

Waiting for:
1. ✅ Voxpipe standalone tested
2. ✅ Open Engine standalone tested
3. 🔄 Integration implementation

**Target:** Week 3 start integration

---

*This document will be updated as we build.*
