# ElevenLabs v4 Script & Voice Guide

## Official Eleven v4 Expressive Audio Tags
Insert these square-bracket tags `[...]` immediately before any sentence or phrase requiring an emotional shift:
- `[curious]` — questioning, intriguing tone (ideal for the opening Hook).
- `[serious]` / `[dramatic]` — authoritative, epic storytelling delivery.
- `[tense]` / `[ominous]` — suspenseful, eerie, or threatening mood.
- `[angry]` — explosive anger, fierce confrontation, or sharp shout.
- `[sighs]` / `[somber]` — heavy exhale, sorrow, regret, or quiet grief.
- `[whispers]` — tense whisper for secrets, dread, or horror beats.
- `[confident]` — decisive, grounded tone for closing lines or cliffhangers.

## Script Writing Rules
1. **Ideal Length:** 95–125 words (~45–55 seconds of voiceover at a steady pace, leaving room for a *Chapter Card*, 2 *Hard Silence Beats*, and a 4-second closing *Title Card* within a 50–65 second final film).
2. **Dramatic Pauses & Paragraphs (Mandatory Blank Line):** In the *Copy-Ready Script*, separate every scene segment with **1 blank line (`Enter` twice)** so ElevenLabs v4 adds natural breathing pauses and FFmpeg `silencedetect` can map scene boundaries cleanly.
3. **Phonetic Pronunciation for Foreign or Invented Terms:** Split unfamiliar syllables with hyphens (e.g., `Val-ha-lla`, `Ex-ca-li-bur`, `A-ra-shi`, `Hi-ka-ri`) so `Language: Auto` in Eleven v4 reads vowels accurately.
4. **Zero AI-Slop Copywriting (Mandatory):**
   - Write like a grounded human storyteller describing concrete visual actions.
   - **FORBIDDEN:** Never use cliché AI filler such as *"unleashing endless terror"*, *"lest the universe perish"*, *"imagine if..."*, cheap rhetorical questions (*"what could possibly happen next?"* / *"how will they survive?"*), or bloated adjectives (*"incredibly dramatic"*, *"truly extraordinary"*).

## Eleven v4 Voice Recommendations
Always recommend voices tailored to the story's tone:
1. **Epic & Authoritative Male Narrator:** `Callum`, `George`, or `Raunak M` (deep register, crisp articulation, responsive to `[dramatic]` → `[angry]` shifts).
2. **Warm Documentary Male Narrator:** `Brian` or `Daniel` (ideal for history, philosophy, science explainers, or calm mythology).
3. **Mysterious & Expressive Female Narrator:** `Aria` or `Charlotte` (great for dark folklore, tragic heroines, or intimate character perspectives).
4. **Custom Voice Design v4:** If the user wants a unique timbre, provide an English voice character prompt for **Try Voice Design for v4**.
