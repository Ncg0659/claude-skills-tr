---
name: hata-avcisi
description: Use when something is broken in an app, game or script — a bug report, error message, crash, wrong value, or "çalışmıyor". Finds the cause with evidence before changing code, then makes the smallest fix and reports in Turkish.
---

# Hata Avcısı (Bug Hunter)

Guessed fixes burn usage limits and break things that worked. This skill forces the order that experienced developers use: **reproduce → prove the cause → smallest fix → re-test → honest report.**

## Core rules (always)
- Work only from files and messages in this session. Never assume a fix discussed in another chat or tool was applied. Label every claim: **gözlenen / kodda doğrulanan / kullanıcı söyledi / varsayım**.
- Smallest reversible change. No unrelated refactors, new features, new dependencies, deployments or accounts without approval. Keep the existing look, language and working features.
- Never paste the user's code, keys or private files into web searches; search with generic, anonymized terms.
- Say exactly which checks ran. Never claim a real device or browser was tested unless it was.

## Method
1. **Write down the symptom.** Expected vs. actual, where (screen / function), device and browser, since when. If something essential is missing, ask once (console message, screenshot, steps).
2. **Reproduce.** Find the shortest steps that trigger it. If you can run it, run it and read the console/output. If you cannot reproduce, say so — do not fix blind.
3. **Read only the relevant code.** Follow the data from the trigger to the wrong output.
4. **List 1–3 hypotheses**, ranked. For each, name the single check that confirms or rules it out.
5. **Test the cheapest hypothesis first.** One change at a time; never stack speculative fixes.
6. **Fix the root cause, not the symptom.** No empty `try/catch` to silence errors, no hard-coded values to pass one case, no hiding the broken element.
7. **Re-run the reproduction**, then check one neighbouring feature that shares the code.

**Stop rule:** after two ruled-out hypotheses, stop. Report what is known and ask for the specific data that would decide it, instead of guessing a third time.

## Usual suspects in small web apps
- Old version still loaded: browser cache or a service worker serving stale files.
- Sensors or microphone silent: page not on HTTPS, permission not requested from a user tap (iOS), denied with no fallback.
- Saved data in `localStorage` from an older version with a different shape.
- Timers or listeners started twice (`setInterval` never cleared, duplicate event listeners).
- Time zone / date boundary errors (local time vs UTC).
- A free API returned empty, late or rate-limited data and the UI treated it as real.
- Layout breaking only at narrow widths (320–375 px) or under the phone notch.

## Required report (Turkish, short)
1. **Belirti:** what was wrong, one sentence.
2. **Kök neden:** the cause and the evidence (or "kanıtlanamadı").
3. **Değişen dosyalar:** exact files and changes, or "Yok".
4. **Test sonuçları:** what was re-run, where, result; what was *not* tested.
5. **Riskler / bilinmeyenler.**
6. **Sonraki adım:** the smallest safe next action.
