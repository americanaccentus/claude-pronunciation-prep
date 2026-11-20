---
name: prep-words
description: Review what we discussed (this conversation, or all of today's sessions with "today") and turn the work words the user might mispronounce into short spoken sentences grouped by topic, ready to practise aloud before meetings and presentations. Run as /prep-words [today] [topic hint].
---

# Prep my words

Many professionals read work words every day that they have rarely said
aloud ("reimbursement", "interoperability", "provider"…), and find out in
the meeting. This skill turns what we worked on into a short speaking drill:
the risky words, used in the sentences the user would really say, ready to
practise aloud.

## Settings (the user may edit these)

- **Accent:** American English. (Change to "British English" etc. if wanted.)
- **Native language:** not set. (If set, e.g. "French", also favour words
  with sounds that speakers of that language commonly find hard.)

## 1. What to review

- `/prep-words` → this whole conversation (the user's messages, your
  answers, files and documents we read or wrote: slides, notes, emails,
  specs).
- `/prep-words today` → also today's other Claude Code sessions in this
  project. Read their local transcripts, user and assistant text only:

  ```bash
  python - <<'EOF'
  import json, os, pathlib, datetime, re
  slug = re.sub(r"[^A-Za-z0-9]", "-", os.getcwd())
  folder = pathlib.Path.home() / ".claude" / "projects" / slug
  today = datetime.date.today()
  for f in sorted(folder.glob("*.jsonl")):
      if datetime.date.fromtimestamp(f.stat().st_mtime) != today:
          continue
      for line in f.open():
          try:
              m = json.loads(line).get("message") or {}
          except ValueError:
              continue
          c = m.get("content")
          parts = [c] if isinstance(c, str) else [p.get("text", "") for p in (c or []) if isinstance(p, dict) and p.get("type") == "text"]
          for t in parts:
              if t.strip():
                  print(f"[{m.get('role')}] {t[:2000]}")
  EOF
  ```
  (If `python` isn't found, run the same with `python3`.) If the folder
  isn't found, say so and use this conversation only.
- Any extra words after the command (`/prep-words board meeting`) are a hint:
  favour that topic and write the sentences for that setting.

## 2. Pick the words (aim for 10–25)

Keep words the user is likely to hesitate on **out loud**:
- multi-syllable domain terms (reimbursement, interoperability, utilization);
- words whose stress moves between forms (analysis → analytical,
  photograph → photography, economy → economic);
- noun/verb pairs with different stress (record, present, contract, increase);
- terms of two or more words said as one (health care provider, supply chain,
  machine learning);
- business acronyms and initialisms said aloud (KPI, EBITDA, HIPAA);
- borrowed or irregular spellings (niche, segue, epitome, Wednesday).

**Business vocabulary only.** Pick the words of the work itself (the
field, the clients, the money, the operations), never the tools used to do
it. Skip names of software, languages, databases, platforms, file formats
and commands (SQL, Postgres, Python, Jupyter notebook, Excel, Git, API,
JSON…), even when the session was mostly about them, and don't put them in
the sentences either.

Skip everyday words the user clearly masters, and anything already marked
`confident` in `~/pronunciation-prep/words.md`.

**Confidential by default.** Never put client, patient, partner or colleague
names, internal project code names, figures, or quoted text from documents
into the output. Keep the general term ("the clinic", "our partner", "the
client"). Public product or place names are fine only if the user will say
them.

## 3. Write the sentences

- Group the words into 2–5 topics taken from the work (e.g. "Operations",
  "Budget", "Data & reporting").
- Per topic, 3–5 sentences of 8–16 words, in the voice the user would use in
  that meeting: first person, spoken, simple grammar ("Our providers rotate
  through the mobile clinic twice a week.").
- Each sentence uses 2–4 target words; every target word appears at least
  once, the hardest ones twice in different positions.
- Plain text only: no abbreviations a scoring tool would read oddly, numbers
  in words when they matter to the rhythm.

## 4. Pronunciation notes: don't invent them

Add a short "say it" note only when you are sure of it, in the chosen accent
(stressed syllable in CAPS: pro-VI-der, re-im-BURSE-ment). If unsure, write
`check` instead. If a pronunciation dictionary tool or connector is
available (for example the American Accent US connector's `explain_word`),
use it for the notes and IPA; otherwise leave IPA out.

## 5. Save and show

1. Write `~/pronunciation-prep/YYYY-MM-DD.md` (append a new section if the
   file exists for today):

   ```markdown
   # Prep · YYYY-MM-DD · <topic hint or "today's work">

   ## Words
   | Word | Topic | Say it |
   |---|---|---|
   | provider | Operations | pro-VI-der |

   ## Sentences
   ### Operations
   1. Our **providers** rotate through the **mobile clinic** twice a week.

   ## All sentences
   (one sentence per line, no bold, no numbers)
   ```
2. Add new words to `~/pronunciation-prep/words.md` (one table: Word | Topic |
   First seen | Status), with status `new`. Never duplicate a word; the user
   changes the status to `practising` / `confident` themselves.
3. In the reply: the words table, the sentences by topic, then all the
   sentences again as plain text in one fenced code block (one per line,
   easy to copy). Don't mention any website, app or practice tool, and
   don't tell the user where to paste or record them.

Keep the reply short: no explanations of the method.
