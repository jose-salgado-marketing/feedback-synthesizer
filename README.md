# Feedback Synthesizer

A small tool that turns messy, raw performance feedback — peer comments, 360 notes, self-assessments, manager observations — into a concise, natural-sounding performance review: a rating plus a short narrative grounded in specific, named examples.

This is an independent, personal project. It is not affiliated with, and contains no proprietary material from, any employer. Everything here — the prompt design, the example, the code — was built from general people-management best practice (the Situation-Behavior-Impact model), not from any internal company system.

## Why this exists

Most performance-review drafting either goes too generic ("great team player," "needs to improve communication") or takes a manager an hour of staring at a blank page trying to remember specifics. This tool forces the opposite: it will only write a claim if it can point to a concrete example in your notes, which keeps the output honest and useful instead of templated filler.

## What it does

- Takes raw, unstructured notes as input (a text file or piped stdin)
- Produces a one-line rating with justification, plus a ~120–220 word narrative
- Grounds every statement in the Situation → Behavior → Impact model
- Refuses to invent a weakness just to "seem balanced" if the notes don't support one
- Matches the language of your notes (English or Spanish) automatically, or can be forced either way
- Ships two ways to use it: a Python CLI (for repeat/batch use) and a plain prompt template (for anyone who just wants to paste into a chat AI with no setup)

## Quick start (CLI)

```bash
git clone https://github.com/<your-username>/feedback-synthesizer.git
cd feedback-synthesizer
pip install -r requirements.txt
export ANTHROPIC_API_KEY="sk-ant-..."

python feedback_synthesizer.py --input example_input.txt --employee "Alex Rivera"
```

Compare your output against `example_output.md` to see the expected shape.

### Options

| Flag | Description |
|---|---|
| `--input` / `-i` | Path to a text file of raw notes. Omit to read from stdin (`cat notes.txt \| python feedback_synthesizer.py -e "Name"`). |
| `--employee` / `-e` | **Required.** Name of the person being reviewed. |
| `--language` / `-l` | Force `en` or `es`. Default: matches the input notes. |
| `--model` / `-m` | Anthropic model to use. Default: `claude-sonnet-4-5`. |
| `--output` / `-o` | Write to a file instead of printing to stdout. |

## Quick start (no API key)

If you don't want to install anything, open [`prompt_template.md`](./prompt_template.md), copy the prompt block into any chat AI, fill in the brackets, and paste in your notes.

## A note on privacy

This tool processes real feedback about real people. Treat it accordingly:

- **Never commit real employee notes, names, or output to this repo or any public repo.** The `example_input.txt` / `example_output.md` here use a fictional person at a fictional company for exactly this reason.
- Run it locally with your own notes and your own API key; nothing is retained by this tool itself.
- Always read and edit the output before using it — this drafts a starting point, it doesn't replace your own judgment about the person.

## Tech stack

Python 3.8+, the official `anthropic` SDK. No other dependencies.

## License

MIT.
