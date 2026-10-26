# AI Compatibility

Compatible with any instruction-following text model:
- ChatGPT (4, 4o, o1)
- Claude
- Gemini
- Grok
- DeepSeek
- Mistral
- Local models (Llama, Qwen)

## How It Works
1. User downloads `CUSTOM_PROMPT.md` from website
2. Pastes into AI chat as system prompt
3. AI asks: "What kind of video would you like to create?"
4. User describes idea
5. AI produces `coordinate-motion-v1` JSON per protocol
6. User imports JSON into studio

## AI Requirements
- Must follow CUSTOM_PROMPT.md's 28 sections
- Must not invent effect IDs outside catalog
- Must produce valid JSON
- Must respect chosen preset (vertical vs YouTube)

## Fallback
If model cannot attach files, it returns JSON code block. User copies and pastes into Import panel.
