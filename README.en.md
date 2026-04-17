# feedback-master

> A Claude Code skill that helps you prepare difficult feedback, coaching, or conflict conversations — through a deep-interview flow that integrates five evidence-based communication frameworks: **NVC (Nonviolent Communication), I-Message, DBT DEAR MAN, SBI-I, and Radical Candor**.
>
> [한국어 README](./README.md)

## What is this?

Most of us don't struggle with *what* to say in a hard conversation — we struggle with the tangled mix of feelings, unclear wants, guilt, and fear of hurting someone that happens *before* we say anything. Formulas like "use I-statements" don't help, because they skip the untangling.

**feedback-master** is a skill for Claude Code that does the untangling with you, *then* assembles a concrete, personalized script you can actually use.

The flow:

1. **Deep interview** — Claude asks you 6 focused questions (observation → feeling → need → other's perspective → goal → constraints), one at a time. You end up understanding your own situation better than when you started.
2. **Framework selection** — Based on what you shared, Claude picks the best fit among five frameworks (or a combination), and explains *why* in one sentence.
3. **Script generation** — Claude drafts what you'll actually say, in your voice (pulling from your `user-preferences.md`), with alternative phrasings and anticipated responses.
4. **Review loop** — You tell Claude what feels off, and Claude rewrites.
5. **Meta-feedback & personalization** — Claude asks whether you'll actually be able to say it, then logs your feedback to `user-preferences.md` so next time starts from a smarter baseline.

## Why this exists

- Workplaces default to **Ruinous Empathy** (saying nothing to avoid short-term discomfort) or **Obnoxious Aggression** (blunt delivery without care). Frameworks like NVC and DEAR MAN solve this, but learning them takes months.
- Individual frameworks have blind spots. I-Message is weak on negative emotions ([Bippus & Young 2005](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=601983)). NVC is deep but slow. DEAR MAN is structured but can feel cold. **A selection-based, situation-aware combination is more effective than any single framework.**
- English-language frameworks often sound harsh when translated literally into Korean. This skill includes a dedicated **Korean workplace adaptation layer** (honorifics, buffer vocabulary, we/I distinction).

## Quick start

### Install (Claude Code)

Clone this repo into your Claude Code skills directory, or symlink it:

```bash
git clone https://github.com/yourusername/feedback-master.git ~/Documents/feedback-master
ln -s ~/Documents/feedback-master ~/.claude/skills/feedback-master
```

Or, if installed via the skills CLI (when published):

```bash
npx skills add yourusername/feedback-master@feedback-master -g -y
```

### Initialize your preferences file (optional but recommended)

```bash
cp ~/Documents/feedback-master/user-preferences.md.template \
   ~/Documents/feedback-master/user-preferences.md
```

Open the file and fill in your tone preferences, typical phrases, and people you interact with. The skill will update this file over time based on your meta-feedback.

> **Privacy note:** `user-preferences.md` is in `.gitignore` and never committed. It's your personal working notebook.

### Use it

In Claude Code, just describe your situation naturally. The skill triggers on phrases like:

- *"I have to give feedback to my teammate, but…"*
- *"I need to say no to my boss about this, and I don't know how…"*
- *"We keep having the same argument, how do I break the cycle?"*
- *"I want to have a difficult conversation with my parent…"*

Claude will enter the deep-interview flow and take you from tangled mind → usable script.

## Usage example

```
User: 팀원에게 납기 지연 피드백을 해야 하는데 상처 주기 싫어서 망설이고 있어.

Claude (feedback-master):
개인화 메모를 읽었어요. "아쉽다" 대신 "답답하다"를 쓰시는 톤 반영할게요.

상황을 조금 더 이해하고 싶어서 몇 가지 여쭤볼게요.

먼저 최근에 정확히 어떤 일이 있었는지, 영상으로 찍었다면 거기에 
무엇이 담겨 있을까요? 언제, 몇 번 정도였나요?

User: 지난 3주에 두 번 있었어. A프로젝트랑 B프로젝트 납기...

(Claude goes through 6-step interview, then selects SBI-I + Radical Candor,
 generates a concrete Korean script with the user's tone, offers 3 alternative
 phrasings, and suggests re-responses to likely reactions.)

(At the end:)
오늘 만든 스크립트가 실제로 쓸 수 있을 것 같나요?
다음 번에 제가 다르게 해야 할 점이 있을까요?

User: 두 번째 문장이 너무 딱딱해. 좀 부드럽게 풀어줘.
      그리고 "답답했어요"보다 "당황스러웠어요"가 내 말투에 가까워.

Claude: 반영했습니다. "당황스러웠어요" 선호를 user-preferences.md에 
기록했어요. 다음 번에 기본값으로 쓸게요. (재작성된 스크립트 제시)
```

## File structure

```
feedback-master/
├── SKILL.md                       # Entry point for Claude
├── README.md                      # Korean (default)
├── README.en.md                   # You are here
├── LICENSE                        # MIT
├── .gitignore                     # Excludes user-preferences.md
├── .claude-plugin/
│   └── plugin.json                # Plugin metadata
├── references/
│   ├── interview-flow.md          # 6-step interview questions
│   ├── i-message.md               # Thomas Gordon
│   ├── nvc.md                     # Marshall Rosenberg
│   ├── dear-man.md                # Marsha Linehan (DBT)
│   ├── sbi.md                     # Center for Creative Leadership
│   ├── radical-candor.md          # Kim Scott
│   ├── framework-selection.md     # Decision tree + matrix
│   ├── korean-workplace.md        # Korean-language adaptation
│   └── examples.md                # 8 worked scenarios
├── user-preferences.md.template   # Starter template
└── user-preferences.md            # (git-ignored) your personal notes
```

## How personalization works

1. On every invocation, Claude reads `user-preferences.md` first.
2. It respects your preferred phrasings, avoids phrases you dislike, and references past feedback entries.
3. At the end of every session, Claude asks: *"Will you actually be able to use this? What should I do differently next time?"*
4. Your response is appended (never overwritten) to the "past feedback log" section of `user-preferences.md`.
5. Over time, the skill converges on your voice.

This is a **skill-level memory**, scoped to feedback preparation. It does not touch your general Claude memory.

## Framework credits

This skill stands on the shoulders of five communication traditions. Full citations are in each reference file.

| Framework | Origin | Year | Primary use |
|---|---|---|---|
| I-Message | Thomas Gordon | 1970 | Quick 1-sentence feedback |
| NVC (OFNR) | Marshall Rosenberg | 1960s–70s | Deep relational dialogue |
| DEAR MAN / GIVE / FAST | Marsha Linehan (DBT) | 1980s | Structured requests & boundaries |
| SBI / SBI-I | Center for Creative Leadership | 1990s–2000s | Workplace feedback |
| Radical Candor | Kim Scott | 2017 | Managerial attitude framing |

**feedback-master** is a *meta-skill*: it integrates these frameworks under a selection logic and a deep-interview elicitation. It does not replace studying the originals — if any framework resonates, read the source books listed at the bottom of each reference file.

## Design principles

- **Self-empathy before formula.** Frameworks without self-understanding become hollow performance. We interview first.
- **Selection, not dogma.** No framework is universally right. We match situation to frame.
- **Personalization over time.** The skill gets better as you use it. Your voice shapes the output.
- **Korean workplace awareness.** Built-in adaptation layer for honorifics, buffer vocabulary, and we/I distinction.
- **Safety first.** For crises (self-harm, violence, severe psychological distress), the skill explicitly directs users to professional resources (Korea: 1393, 1577-0199).

## Limitations

- Not a substitute for therapy or professional coaching in clinical contexts.
- Does not solve structural power imbalances (workplace harassment, abuse) — directs to HR/legal channels.
- Empirical evidence varies by framework (strong for DBT, moderate for I-Message, emerging for NVC). See individual reference files.
- Korean adaptation is based on common patterns, not formal sociolinguistic research. Users with specific cultural contexts may need to adjust.

## Contributing

Contributions welcome. Especially:

- Additional example scenarios in `references/examples.md`
- Non-Korean cultural adaptation layers
- Empirical research updates in reference files
- Edge cases where the framework selection logic fails

Please open a discussion before large changes. This skill tries to stay focused and lean.

## License

MIT. See [LICENSE](./LICENSE).

The communication frameworks themselves remain the intellectual work of their original authors. This skill reconstructs and operationalizes them for practical conversational use; it is not an official product of Gordon Training, the Center for Nonviolent Communication, Behavioral Tech (DBT), CCL, or Radical Candor.

## Acknowledgments

Built on research into feedback, conflict resolution, and workplace communication across clinical psychology, management studies, and organizational behavior. Special thanks to:

- Thomas Gordon (1918–2002)
- Marshall Rosenberg (1934–2015)
- Marsha Linehan
- Kim Scott
- The researchers and practitioners cited in each reference file

---

If this skill helps one difficult conversation go better, it's done its job.
