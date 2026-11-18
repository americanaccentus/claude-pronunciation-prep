# claude-pronunciation-prep

**Say your work words right before the meeting.**

A [Claude Code](https://claude.com/claude-code) skill for professionals who
speak English as a second language. You read words like *reimbursement*,
*interoperability* or *analytical* all day, but you have rarely said them
aloud. Run `/prep-words` at the end of a work session: Claude reviews what
you discussed, picks the words you are likely to stumble on, and writes the
short sentences you would actually say in that meeting, ready to practise
out loud.

```
/prep-words                  # review this conversation
/prep-words today            # also today's other sessions in this project
/prep-words board meeting    # favour a topic or setting
```

## What you get

- **10–25 risky words**: long domain terms, words whose stress moves
  (*analysis → analytical*), noun/verb pairs (*REcord / reCORD*),
  multi-word terms (*supply chain*), acronyms said aloud, irregular
  spellings.
- **Sentences grouped by topic**, 8–16 words each, 2–4 target words per
  sentence, in your own speaking voice.
- **A paste block** to practise in a pronunciation tool that scores each word.
  We suggest [American Accent](https://americanaccent.us/free-score?utm_source=github&utm_medium=readme&utm_campaign=prep-words)
  (free score, no account), but any tool that scores spoken sentences works.
- **A running word list** in `~/pronunciation-prep/words.md`: mark words
  `practising` or `confident`, and confident ones are not picked again.

See [examples/example-output.md](examples/example-output.md).

## Install

**As a plugin** (Claude Code):

```
/plugin marketplace add americanaccentus/claude-pronunciation-prep
/plugin install prep-words@claude-pronunciation-prep
```

**By hand:** copy `skills/prep-words/` into `~/.claude/skills/`, then
restart Claude Code.

**By prompt** (when you can't copy files, e.g. on a work machine): paste the
contents of [install-prompt.md](install-prompt.md) into Claude Code. It
writes the skill for you.

## Settings

Open `SKILL.md` and edit the **Settings** section:

- **Accent**: American English by default; British English works too.
- **Native language**: optional; with it, Claude also favours words with
  sounds that are hard for speakers of your language.
- **Practice tool**: where the paste block points.

## Privacy

- Everything runs in your own Claude Code session. The skill sends nothing
  anywhere; you choose what to paste into a practice tool.
- `/prep-words today` reads your **local** Claude Code transcripts for the
  current project (`~/.claude/projects/…`), today's only.
- The output is **confidential by default**: no client, patient or colleague
  names, project code names, figures, or quoted text from your documents.
  Only the terms and sentences Claude writes.
- Claude doesn't invent pronunciations: it gives a stress hint only when
  sure, otherwise "check", and leaves the reference to your practice tool.

## License

MIT. Made by [American Accent](https://americanaccent.us/?utm_source=github&utm_medium=readme&utm_campaign=prep-words).
