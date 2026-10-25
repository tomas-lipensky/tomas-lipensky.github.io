# copilot

### Odkazy

https://copilot.microsoft.com/

### CLI

[copilot](https://github.com/features/copilot/cli) --allow-all-paths --allow-all-tools --enable-all-github-mcp-tools --model "gpt-5-mini" ... spustí copilot CLI  

### Obecně

Copilot repo init

### Soubory

.github/copilot-instructions.md ... instrukce, co se přidají k jakémukoli promptu  
.github/instructions/*.instructions.md ... použijí se, když prompt obsahuje nějakou informaci, co vypadá, že souvisí s instrukcí  
.github/skills/<skill-name>/SKILL.md ... popis dovednosti - perfektně popsané, co umí, co dělat, například "release preparation". Umí spouštět is skripty  
.github/agents/<agent_name>.md, nebo .github/agents/<agent_name>.agent.md ... agent, nebo subagent  
.github/prompts/<název>.prompt.md  

### Tipy

používání flowchartu:

```
flowchart LR
A(["Start"])
A --> B{"Decision"}
B --> C{"Option A"}
B --> D{"Option B"}
```

Pokud vstup je např. pdf., je dobré si jej převést na text sám, jinak Copilot udělá automaticky a spotřebuje víc kreditů

Používat templaty místo detailních popisů

Nepoužívat mnoho nástrojů, pluginů, skillů

Používat implementační plány v lepším modelu, implementace v levnějším modelu

### Nástroje

https://github.com/obra/superpowers ... sada skillů  
https://github.com/github/spec-kit ... sada skillů jak superpowers  
https://github.com/JuliusBrussee/caveman ... skily, aby mluvil velmi narovinu a jednoduše  
https://github.com/github/awesome-copilot ... Předpřipravené skilly pro konkrétní jazyky a tasky  

### Agenti a subagenti

Omezení kontextu, ať se šetří  
Pro konkrétní úkoly pouštět subagenty, s omezeným kontextem a akcí, vrací výstupy agentovi  

např. Agent - orchestrátor, subagent - zjistit počasí pro danou oblase, další subagent načte akce a udělá přehled, další subagent - zmixuje počasí a akce a udělá doporučení.

```
---
description:
tools: [read, write, search, execute]
model: "GPT-5 mini (copilot)"
user-invocable: false
---
# Constrains
```
