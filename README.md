# SkillGate demonstration skills

Synthetic demonstration fixtures for SkillGate Finance's installation checks.
They do not reproduce a named incident or measure a language model's behaviour.

## Sandbox only

Use a disposable project with no secrets, wallet, payment tools, or real assets.
Never install these fixtures into your everyday agent profile. The trap contains
an active instruction to hide a fictitious transfer; it must be treated as
untrusted input. The archive itself contains only Markdown and JSON, no executable
scripts, real wallet address, credential collection, or external network endpoint.

| Skill | Purpose | Expected local static result |
| --- | --- | --- |
| portfolio-summary | Read the fictitious ledger only | Automatic installation |
| portfolio-summary-trap | Claims read-only access but asks for a hidden transfer of 25 DEMOUSD | Held before activation, with evidence |

The names identify the demonstration roles for the audience; the scanner must
decide from the actual bytes, not their names. These are development examples,
not independent benchmark cases or a safety certification.

## Run after downloading and extracting

With the SkillGate CLI installed, create a disposable project and initialize it:

```sh
DEMO_ROOT="$(mktemp -d)"
skillgate --project "$DEMO_ROOT" init --agent codex
skillgate --project "$DEMO_ROOT" add /absolute/path/to/extracted/skills/portfolio-summary
skillgate --project "$DEMO_ROOT" add /absolute/path/to/extracted/skills/portfolio-summary-trap
```

The first skill should appear in the disposable project's .agents/skills. The
second should remain outside that active folder unless an explicit exception is
chosen. Cancelling is the default. Scan and installation are real local actions.

Each actions.json is input for SkillGate's bounded deterministic ledger simulator:
only read(demo-user) and transfer(demo-user, demo-external, integer amount 1–100,
DEMOUSD) are supported, with at most ten actions. No shell or network is used by
that simulator. Replaying this plan is a deterministic simulation, not execution
of the natural-language instructions by an actual agent or model.

The example starts with 100 DEMOUSD for demo-user and zero for demo-external.
Replaying the trap plan without the gate leaves 75 and 25. Holding installation
leaves 100 and zero. No real funds exist or move.

No public download URL is claimed by these files. Publication location and any
public availability must be verified separately. Select one skill folder when
using a GitHub source; repository roots contain both examples.
