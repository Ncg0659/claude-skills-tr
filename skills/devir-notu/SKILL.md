---
name: devir-notu
description: Use at the end of a work session, when switching between AI assistants (Claude, Codex, ChatGPT, Cursor, Gemini), or when a note from another assistant is pasted. Writes or verifies a short, honest Turkish handoff note.
---

# Devir Notu (Handoff Note)

Many people build the same project with several AI assistants. Work done in one tool is invisible to the others, and assistants happily report work that never happened. This skill turns every switch into a short, honest, copy-pasteable note — and treats incoming notes as claims to verify, not facts.

## Core rules (always)
- Record only what actually happened in this session. Plans, guesses and another assistant's claims are never "done".
- Mark anything not verified with **(doğrulanmadı)**.
- Never put API keys, tokens, passwords or private personal data into a note.
- Do not save the note into the project unless the user asks. If they keep a `HANDOFF.md`, offer to append to it.
- Write the note in Turkish. Keep code identifiers, file names and commands as they are.

## Mode 1 — Writing a note
**Triggers:** "not çıkar", "devir notu yaz", "Codex'e / ChatGPT'ye geçiyorum", the session is ending, or a substantial coding task just finished.

Use today's date (from a clock tool if available). Output one Markdown code block, under ~40 lines:

```
# Devir Notu — <Proje> — <YYYY-AA-GG>
Yazan: <asistan adı>

## Hedef
<bu oturumun hedefi, tek cümle>

## Yapılanlar
- <dosya>: <ne değişti, tek satır>

## Doğrulananlar / Test sonuçları
- <ne, nerede kontrol edildi, sonuç>

## Yarım kalanlar
- <maddeler veya "Yok">

## Yeni kararlar ve kurallar
- <kullanıcının bu oturumda verdiği kararlar veya "Yok">

## Bilinen sorunlar
- <açık hatalar / riskler veya "Yok">

## Sıradaki en küçük adım
<tek eylem>

## Diğer asistana not
<dokunulmaması gereken dosyalar, korunması gereken davranışlar>
```

## Mode 2 — Reading a note from another assistant
**Triggers:** the user pastes a note, summary or log written by another assistant or chat.

1. Treat every line as a **claim**.
2. If project files are available, check the important claims against them (does the function exist, did the file actually change, does the test pass).
3. Reply with three short lists:
   - **Doğrulandı** — confirmed in files
   - **Doğrulanamadı** — no way to check here
   - **Çelişki** — note says X, files show Y
4. Ask which conflicts to resolve before starting new work.

## Finish
After writing a note, add one line saying where to paste it (the other assistant's chat, or `HANDOFF.md`).
