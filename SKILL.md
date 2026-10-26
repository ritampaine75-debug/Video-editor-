# SKILL.md — Coordinate Motion Studio Skill

## Name
coordinate-motion-studio

## Description
Generates deterministic motion graphics projects as `coordinate-motion-v1` JSON for browser-based rendering. Turns scripts into editable timelines with keyframes, transitions, and effects.

## Compatible Models
Any instruction-following LLM: ChatGPT, Claude, Gemini, Grok, DeepSeek, Mistral, Llama, Qwen.

## Activation
User shares CUSTOM_PROMPT.md or says: "Activate Coordinate Motion Studio skill."

Agent response: Ask what video they want, per CUSTOM_PROMPT.md initialization.

## Inputs Accepted
- Script / storyboard / concept
- Duration, aspect (vertical 9:16 or YouTube 16:9)
- Brand colors, fonts, logos
- Effect preferences
- Voiceover timing

## Outputs
- `coordinate-motion-v1` JSON (download or code block)
- Validation notes
- Editing suggestions

## Workflow
1. Parse user concept -> storyboard
2. Choose composition from preset
3. Partition scenes, assign tracks
4. Create objects with base props + keyframes + easings
5. Assign transitions + effects from catalog (implemented only)
6. Validate, emit JSON
7. Offer iteration: "Want adjustments?"

## Constraints
- No API required, no training, no video model needed
- Use only documented protocol fields
- Respect performance limits
- Provide fallback if mime not supported

## Example Invocation
User: "Make a 10s YouTube intro: 'WELCOME TO THE SHOW' with cinematic sweep."
Agent: Generates JSON with 1920x1080, 10s, dramatic text reveal, light sweep, fade transition, exports webm.

## Integration
- Index.html import: Paste JSON -> Validate -> Render
- File sharing: via Web Share API or download
- Version: 1.0.0, protocol coordinate-motion-v1
