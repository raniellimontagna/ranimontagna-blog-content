# Lemon Energia Career Announcement Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Publish a sourced, personal career announcement about joining Lemon Energia in Portuguese, English, and Spanish, dated July 14, 2026.

**Architecture:** The Portuguese MDX article is the canonical editorial source. English and Spanish are natural editorial translations that preserve its facts, dates, links, distinctions, and narrative arc under the same basename. Validation is repository-local: YAML frontmatter parsing, content guardrails, word counts, URL checks, and a final cross-language review.

**Tech Stack:** MDX, Markdown, YAML frontmatter, Ruby 4 standard library, ripgrep, curl, Git

## Global Constraints

- Follow `docs/superpowers/specs/2026-07-13-lemon-novo-capitulo-design.md` exactly.
- Publication date is `2026-07-14`; the first workday was `2026-07-13`.
- Use the same basename in `posts/pt`, `posts/en`, and `posts/es`: `2026-07-14-eu-nao-conhecia-a-lemon.mdx`.
- Portuguese is canonical; English and Spanish must read naturally rather than literally.
- Set `published: true` and `coverImage: 'https://energialemon.com.br/social-media-thumb.png'` in all languages.
- Do not present “Engenheiro de Software” or “Software Engineer” as the confirmed official title.
- Describe the role as software-engineering work connecting the Center of Excellence (COE) and business teams.
- Do not name the former employer, the layoff, or the dismissal circumstances.
- Preserve the approved subtle contrast without hostility.
- Separate public facts about Lemon's current AI use from the author's personal view of applied AI.
- Attribute company metrics to Lemon and identify the G1 article as sponsored content produced by Lemon.
- Do not claim savings of 20%; do not foreground any savings percentage.
- Do not claim completed internal work, results, or knowledge the author does not yet have.
- Keep source links next to relevant claims and avoid a standalone bibliography section.
- Target 1,200–1,600 body words in Portuguese; allow 1,000–1,700 in each translation.
- Commit locally after each language; do not push.

---

## File Map

- Create `posts/pt/2026-07-14-eu-nao-conhecia-a-lemon.mdx`: canonical Portuguese announcement and factual source of truth.
- Create `posts/en/2026-07-14-eu-nao-conhecia-a-lemon.mdx`: natural English adaptation with equivalent claims and links.
- Create `posts/es/2026-07-14-eu-nao-conhecia-a-lemon.mdx`: natural Spanish adaptation with equivalent claims and links.
- Read `docs/superpowers/specs/2026-07-13-lemon-novo-capitulo-design.md`: approved requirements and factual guardrails; do not modify during implementation.

### Task 1: Write the canonical Portuguese article

**Files:**
- Create: `posts/pt/2026-07-14-eu-nao-conhecia-a-lemon.mdx`
- Reference: `docs/superpowers/specs/2026-07-13-lemon-novo-capitulo-design.md`

**Interfaces:**
- Consumes: the approved narrative, source hierarchy, exact dates, role wording, and disclosure rules from the design specification.
- Produces: the canonical section order, facts, links, and personal framing that Tasks 2 and 3 must preserve.

- [ ] **Step 1: Create the exact Portuguese frontmatter**

Use `apply_patch` to create the file with this frontmatter:

```mdx
---
title: Eu não conhecia a Lemon. Hoje começo a construir com ela
date: '2026-07-14'
description: >-
  Ontem comecei um novo capítulo na Lemon Energia. O que descobri sobre
  geração distribuída, tecnologia e IA — e por que esse mercado me surpreendeu.
tags:
  - carreira
  - lemon-energia
  - energytech
  - energia-renovavel
  - geracao-distribuida
  - tecnologia
  - inteligencia-artificial
published: true
coverImage: 'https://energialemon.com.br/social-media-thumb.png'
---
```

- [ ] **Step 2: Write the opening and personal discovery**

Add the sections `## Ontem comecei na Lemon` and `## Eu realmente não conhecia a Lemon`.

The first sentence must establish the durable date explicitly: “Ontem, 13 de julho, comecei um novo capítulo profissional na Lemon Energia.” Include the approved contrast once, unchanged in meaning: “Depois de um encerramento abrupto, ficou ainda mais claro para mim que o próximo passo precisava ser em um lugar onde tecnologia, propósito e pessoas fossem partes da mesma construção.”

Explain that the author did not know Lemon or the energytech market before the selection process. Avoid implying that Lemon was obscure; frame the gap as evidence that energy still feels distant to many software professionals.

- [ ] **Step 3: Explain shared distributed generation and the three-part appeal**

Add `## Energia solar sem placas no telhado?` and `## O que me surpreendeu nesse modelo`.

Link the first technical explanation to [ANEEL](https://www.gov.br/aneel/pt-br/assuntos/geracao-distribuida). State that shared generation lets multiple participants use electricity produced by one or more distributed-generation plants to compensate consumption through the distribution system. Clarify that the grid and credits connect generation to consumption; do not claim a dedicated physical stream from a named plant reaches each customer.

Explain the three-part appeal in prose: access without rooftop installation, potential savings and lower bureaucracy for small businesses, and sustainability enabled by operational technology. Link current scale to the [official Lemon site](https://energialemon.com.br/) and attribute “mais de 100 usinas solares parceiras” and “15 mil negócios” to Lemon.

Use the [G1 comparison](https://g1.globo.com/sp/campinas-regiao/especial-publicitario/lemon-energia-a-nova-era-da-energia-solar/noticia/2025/09/12/placa-solar-ou-geracao-distribuida-de-energia-entenda-qual-faz-mais-sentido.ghtml) only after labeling it “especial publicitário produzido pela Lemon”. Do not treat its market statistics as independent verification.

- [ ] **Step 4: Explain the technology behind the customer experience**

Add `## A tecnologia por trás da simplicidade`.

Describe the operational chain in concrete terms: online signup, consumption analysis, credit allocation, distributor coordination, billing, app-based history, and support. Present software, data, and product as the layer that makes this chain feel simple to the customer.

Link the historical context to [Exame](https://exame.com/negocios/lemon-energia-startup-da-energia-verde-para-pmes-capta-r-60-milhoes-com-kaszek/). State that Lemon was founded in 2019 and that Exame reported a R$ 60 million Series A. Make the historical framing explicit; do not imply the round is recent.

- [ ] **Step 5: Separate Lemon's public AI use from the author's AI perspective**

Add `## IA quando ela resolve um problema real`.

In one paragraph linked to the [public recruiting FAQ](https://lemonenergy.notion.site/FAQ-Processo-Seletivo-df36ec30b9a7493783fff7b3a3eed476), state that Lemon publicly mentions NotebookLM and proprietary solutions applying AI to its knowledge base.

Start a separate paragraph with the author's position: useful AI reduces repetitive work, organizes context, supports decisions, and improves operational efficiency. Avoid product-roadmap claims and avoid saying that the author has already implemented any AI initiative at Lemon.

- [ ] **Step 6: State the initial scope and close with humility**

Add `## O que começo a construir agora` and `## Primeiro dia, primeiro registro`.

Use the approved role wording: “atuando com engenharia de software na conexão entre o Centro de Excelência (COE) e as áreas de negócio”. Explain that the initial scope involves understanding needs and contributing improvements, automations, and digital solutions. Do not use an official job title.

Close by saying that this is an opening record rather than a verdict about a company on day one. Emphasize the public signals that motivated the move—transparency, purpose, builder mentality, and pragmatic technology—and end with a short italic invitation for readers in energy, energytech, or applied AI to exchange notes.

- [ ] **Step 7: Run Portuguese content guardrails**

Run:

```bash
ruby -e 'text = File.read(ARGV[0]).sub(/\A---\n.*?\n---\n/m, ""); count = text.scan(/\S+/).size; abort("Portuguese body has #{count} words") unless (1200..1600).cover?(count); puts "Portuguese body: #{count} words"' posts/pt/2026-07-14-eu-nao-conhecia-a-lemon.mdx
```

Expected: `Portuguese body: N words`, where `N` is between 1200 and 1600.

Run:

```bash
if rg -n 'Luizalabs|layoff|20%|Engenheiro de Software' posts/pt/2026-07-14-eu-nao-conhecia-a-lemon.mdx; then exit 1; else echo 'Portuguese forbidden claims absent'; fi
for pattern in '13 de julho' 'ANEEL' 'especial publicitário' 'R\$ 60 milhões' 'NotebookLM' 'Centro de Excelência'; do rg -n "$pattern" posts/pt/2026-07-14-eu-nao-conhecia-a-lemon.mdx || exit 1; done
git diff --check -- posts/pt/2026-07-14-eu-nao-conhecia-a-lemon.mdx
```

Expected: the forbidden-claims message, matches for all six required concepts, and no `git diff --check` output.

- [ ] **Step 8: Commit the Portuguese article**

```bash
git add posts/pt/2026-07-14-eu-nao-conhecia-a-lemon.mdx
git commit -m "feat(blog): draft Lemon announcement in Portuguese"
```

Expected: one new committed Portuguese MDX file and a clean working tree.

### Task 2: Create the English editorial translation

**Files:**
- Create: `posts/en/2026-07-14-eu-nao-conhecia-a-lemon.mdx`
- Read: `posts/pt/2026-07-14-eu-nao-conhecia-a-lemon.mdx`

**Interfaces:**
- Consumes: the completed Portuguese article's facts, dates, narrative order, source URLs, and distinction between public facts and personal expectations.
- Produces: a fluent English article with equivalent factual meaning and the shared basename required by the blog.

- [ ] **Step 1: Create the exact English frontmatter**

```mdx
---
title: I Had Never Heard of Lemon. Now I Get to Help Build It
date: '2026-07-14'
description: >-
  Yesterday I started a new chapter at Lemon Energia. What I learned about
  distributed generation, technology, and AI — and why this market surprised me.
tags:
  - career
  - lemon-energia
  - energytech
  - renewable-energy
  - distributed-generation
  - technology
  - artificial-intelligence
published: true
coverImage: 'https://energialemon.com.br/social-media-thumb.png'
---
```

- [ ] **Step 2: Translate the complete narrative editorially**

Translate every Portuguese section into natural English using these headings in order:

```md
## Yesterday, I Started at Lemon
## I Genuinely Had Never Heard of Lemon
## Solar Energy Without Panels on Your Roof?
## What Surprised Me About This Model
## The Technology Behind the Simplicity
## AI When It Solves a Real Problem
## What I’m Starting to Build
## A First-Day Note
```

Use “July 13” for the first day, “Center of Excellence (COE)” for the organizational term, “shared distributed generation” for the energy model, and “sponsored content produced by Lemon” for the G1 disclosure. Preserve all five source URLs exactly. Keep the subtle contrast reflective, not accusatory.

- [ ] **Step 3: Verify English facts and language guardrails**

Run:

```bash
ruby -e 'text = File.read(ARGV[0]).sub(/\A---\n.*?\n---\n/m, ""); count = text.scan(/\S+/).size; abort("English body has #{count} words") unless (1000..1700).cover?(count); puts "English body: #{count} words"' posts/en/2026-07-14-eu-nao-conhecia-a-lemon.mdx
if rg -n 'Luizalabs|layoff|20%|Software Engineer @|my title is Software Engineer' posts/en/2026-07-14-eu-nao-conhecia-a-lemon.mdx; then exit 1; else echo 'English forbidden claims absent'; fi
for pattern in 'July 13' 'ANEEL' 'sponsored content' 'R\$ 60 million' 'NotebookLM' 'Center of Excellence'; do rg -n "$pattern" posts/en/2026-07-14-eu-nao-conhecia-a-lemon.mdx || exit 1; done
git diff --check -- posts/en/2026-07-14-eu-nao-conhecia-a-lemon.mdx
```

Expected: a body word count from 1000 to 1700, the forbidden-claims message, matches for all six required concepts, and no whitespace errors.

- [ ] **Step 4: Commit the English translation**

```bash
git add posts/en/2026-07-14-eu-nao-conhecia-a-lemon.mdx
git commit -m "feat(blog): translate Lemon announcement to English"
```

Expected: the English MDX file committed separately and a clean working tree.

### Task 3: Create the Spanish editorial translation

**Files:**
- Create: `posts/es/2026-07-14-eu-nao-conhecia-a-lemon.mdx`
- Read: `posts/pt/2026-07-14-eu-nao-conhecia-a-lemon.mdx`

**Interfaces:**
- Consumes: the completed Portuguese article's facts, dates, narrative order, source URLs, and distinction between public facts and personal expectations.
- Produces: a fluent Spanish article with equivalent factual meaning and the shared basename required by the blog.

- [ ] **Step 1: Create the exact Spanish frontmatter**

```mdx
---
title: No conocía Lemon. Hoy empiezo a construir junto a ella
date: '2026-07-14'
description: >-
  Ayer empecé un nuevo capítulo en Lemon Energia. Lo que descubrí sobre
  generación distribuida, tecnología e IA, y por qué este mercado me sorprendió.
tags:
  - carrera
  - lemon-energia
  - energytech
  - energia-renovable
  - generacion-distribuida
  - tecnologia
  - inteligencia-artificial
published: true
coverImage: 'https://energialemon.com.br/social-media-thumb.png'
---
```

- [ ] **Step 2: Translate the complete narrative editorially**

Translate every Portuguese section into natural Spanish using these headings in order:

```md
## Ayer empecé en Lemon
## Realmente no conocía Lemon
## ¿Energía solar sin paneles en el tejado?
## Lo que me sorprendió de este modelo
## La tecnología detrás de la simplicidad
## IA cuando resuelve un problema real
## Lo que empiezo a construir ahora
## Primer día, primer registro
```

Use “13 de julio” for the first day, “Centro de Excelencia (COE)” for the organizational term, “generación distribuida compartida” for the energy model, and “contenido publicitario producido por Lemon” for the G1 disclosure. Preserve all five source URLs exactly. Maintain Latin American Spanish and avoid literal Portuguese syntax.

- [ ] **Step 3: Verify Spanish facts and language guardrails**

Run:

```bash
ruby -e 'text = File.read(ARGV[0]).sub(/\A---\n.*?\n---\n/m, ""); count = text.scan(/\S+/).size; abort("Spanish body has #{count} words") unless (1000..1700).cover?(count); puts "Spanish body: #{count} words"' posts/es/2026-07-14-eu-nao-conhecia-a-lemon.mdx
if rg -n 'Luizalabs|layoff|20%|Ingeniero de Software @|mi cargo es Ingeniero de Software' posts/es/2026-07-14-eu-nao-conhecia-a-lemon.mdx; then exit 1; else echo 'Spanish forbidden claims absent'; fi
for pattern in '13 de julio' 'ANEEL' 'contenido publicitario' 'R\$ 60 millones' 'NotebookLM' 'Centro de Excelencia'; do rg -n "$pattern" posts/es/2026-07-14-eu-nao-conhecia-a-lemon.mdx || exit 1; done
git diff --check -- posts/es/2026-07-14-eu-nao-conhecia-a-lemon.mdx
```

Expected: a body word count from 1000 to 1700, the forbidden-claims message, matches for all six required concepts, and no whitespace errors.

- [ ] **Step 4: Commit the Spanish translation**

```bash
git add posts/es/2026-07-14-eu-nao-conhecia-a-lemon.mdx
git commit -m "feat(blog): translate Lemon announcement to Spanish"
```

Expected: the Spanish MDX file committed separately and a clean working tree.

### Task 4: Validate the trilingual publication package

**Files:**
- Verify: `posts/pt/2026-07-14-eu-nao-conhecia-a-lemon.mdx`
- Verify: `posts/en/2026-07-14-eu-nao-conhecia-a-lemon.mdx`
- Verify: `posts/es/2026-07-14-eu-nao-conhecia-a-lemon.mdx`
- Reference: `docs/superpowers/specs/2026-07-13-lemon-novo-capitulo-design.md`

**Interfaces:**
- Consumes: the three independently committed language files.
- Produces: a validated local publication package whose metadata, links, facts, and editorial intent agree across languages.

- [ ] **Step 1: Parse and compare frontmatter**

Run:

```bash
ruby -ryaml -rdate -e '
expected_name = "2026-07-14-eu-nao-conhecia-a-lemon.mdx"
expected_cover = "https://energialemon.com.br/social-media-thumb.png"
ARGV.each do |path|
  abort("wrong basename: #{path}") unless File.basename(path) == expected_name
  match = File.read(path).match(/\A---\n(.*?)\n---\n/m) or abort("missing frontmatter: #{path}")
  data = YAML.safe_load(match[1], permitted_classes: [Date], aliases: false)
  required = %w[title date description tags published coverImage]
  missing = required.reject { |key| data.key?(key) }
  abort("missing #{missing.join(", ")} in #{path}") unless missing.empty?
  abort("wrong date in #{path}") unless data["date"].to_s == "2026-07-14"
  abort("not published: #{path}") unless data["published"] == true
  abort("wrong cover in #{path}") unless data["coverImage"] == expected_cover
  abort("expected seven tags in #{path}") unless data["tags"].is_a?(Array) && data["tags"].length == 7
  puts "frontmatter valid: #{path}"
end
' posts/pt/2026-07-14-eu-nao-conhecia-a-lemon.mdx posts/en/2026-07-14-eu-nao-conhecia-a-lemon.mdx posts/es/2026-07-14-eu-nao-conhecia-a-lemon.mdx
```

Expected: three `frontmatter valid` lines.

- [ ] **Step 2: Verify all external sources and the cover**

Run:

```bash
for url in \
  https://energialemon.com.br/ \
  https://energialemon.com.br/social-media-thumb.png \
  https://www.gov.br/aneel/pt-br/assuntos/geracao-distribuida \
  https://lemonenergy.notion.site/FAQ-Processo-Seletivo-df36ec30b9a7493783fff7b3a3eed476 \
  https://exame.com/negocios/lemon-energia-startup-da-energia-verde-para-pmes-capta-r-60-milhoes-com-kaszek/ \
  https://g1.globo.com/sp/campinas-regiao/especial-publicitario/lemon-energia-a-nova-era-da-energia-solar/noticia/2025/09/12/placa-solar-ou-geracao-distribuida-de-energia-entenda-qual-faz-mais-sentido.ghtml
do
  curl -L --fail --silent --show-error --max-time 20 -o /dev/null -w '%{http_code} %{url_effective}\n' "$url"
done
```

Expected: six lines with HTTP `200`.

- [ ] **Step 3: Review cross-language factual parity**

Read the three articles side by side and confirm each contains:

- first day `2026-07-13` and publication perspective from `2026-07-14`;
- the same five source links: the official Lemon home page, ANEEL, the recruiting FAQ, Exame, and G1;
- the attributed current metrics of more than 100 partner solar plants and 15,000 businesses;
- the historical 2019 founding and R$ 60 million Series A context;
- the G1 sponsored-content disclosure;
- separate paragraphs for Lemon's public AI use and the author's AI perspective;
- the provisional-role wording without an official title;
- the subtle transition contrast and no former-employer reference.

Correct any translation that changes a fact, source status, degree of certainty, or personal tone.

- [ ] **Step 4: Run the final repository checks**

Run:

```bash
git diff c4e3908..HEAD --check
git status --short --branch
git log -5 --oneline --decorate
```

Expected: no whitespace errors, a clean working tree, and separate commits for the plan plus the three article languages. If Step 3 required edits, commit only those corrections with:

```bash
git add posts/pt/2026-07-14-eu-nao-conhecia-a-lemon.mdx posts/en/2026-07-14-eu-nao-conhecia-a-lemon.mdx posts/es/2026-07-14-eu-nao-conhecia-a-lemon.mdx
git commit -m "chore(blog): polish Lemon announcement translations"
```

Do not create an empty polish commit when Step 3 requires no changes.
