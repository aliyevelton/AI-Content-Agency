# Content Agency — CrewAI Masterclass Project

Multi-agent **Content Agency**: researches emerging trends, analyzes data, writes reports, and uses a Manager LLM to review and refine output. Built for the **CrewAI Masterclass: The Future of Agentic Workflows (2026)**.

## What This Repo Matches (Tutorial Parts)

| Part | Topic | In This Repo |
|------|--------|---------------|
| **2** | Mental model: Agents, Tasks, Tools, Process | `config/agents.yaml`, `config/tasks.yaml`, `crew.py` |
| **4** | YAML config: identity vs execution, `{topic}` variable | `agents.yaml` (Researcher, Writer), `tasks.yaml` |
| **5** | Tools + expected_output | Researcher has `SerperDevTool`; tasks define format/length/structure |
| **6** | Hierarchical process, Manager LLM | `crew.py`: `Process.hierarchical`, `manager_llm='gpt-4o'` |
| **7** | Run and train | `crewai run`, `crewai train -n 5` (see below) |

## Installation (Part 3 — UV)

- Python **3.10–3.12** (avoid 3.13 for now).
- Install [UV](https://docs.astral.sh/uv/), then:

```bash
uv tool install crewai
uv tool update-shell
```

From this repo (or after `crewai create crew my_agency` and copying in this code):

```bash
cd content_agency
crewai install
```

## Environment

Copy or create a `.env` in the project root:

- **OPENAI_API_KEY** — required for agents and Manager LLM.
- **SERPER_API_KEY** — required for the Researcher’s live search ([get one](https://serper.dev)).
- **MODEL** (optional) — default worker model (e.g. `gpt-4o-mini`). Manager is set in code to `gpt-4o`.

## Running (Part 7)

From the `content_agency` directory:

```bash
crewai run
```

- Uses `main.py` inputs: `topic: 'AI LLMs'`, `current_year`.
- Output: `report.md` in the project root.
- Change topic by editing `main.py` `inputs` (e.g. `'topic': 'Crypto'` or `'Healthcare'`).

## Training (Part 7)

```bash
crewai train -n 5
```

Provide feedback when prompted; the system stores improvements so the crew adapts to your standards.

## Architecture (Parts 2 & 6)

- **Agents**: Researcher (Senior Tech Analyst + SerperDevTool), Writer (Content Strategist).
- **Tasks**: Research → 10-bullet outline; Reporting → full markdown report with clear `expected_output`.
- **Process**: **Hierarchical** — Manager LLM (`gpt-4o`) reviews outputs, approves or sends back for refinement; workers use your `MODEL` from `.env`.

## Project layout

- `src/content_agency/config/agents.yaml` — agent roles, goals, backstories.
- `src/content_agency/config/tasks.yaml` — task descriptions and expected outputs.
- `src/content_agency/crew.py` — crew definition, tools, hierarchical Crew + `manager_llm`.
- `src/content_agency/main.py` — `run` / `train` entrypoints and inputs.

## Support

- [CrewAI docs](https://docs.crewai.com)
- [Hierarchical process](https://docs.crewai.com/how-to/Hierarchical/)
- [CrewAI GitHub](https://github.com/joaomdmoura/crewai)
