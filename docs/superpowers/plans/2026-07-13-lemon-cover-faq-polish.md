# Lemon Cover and FAQ Polish Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Remover o hyperlink do FAQ no pacote trilíngue e gerar uma capa 16:9 própria para revisão, sem publicar o artigo.

**Architecture:** As duas tarefas são independentes e podem ser executadas em paralelo. A tarefa editorial altera apenas três linhas Markdown e cria um commit; a tarefa visual usa a referência oficial da Lemon para gerar uma prévia local, sem alterar o frontmatter dos posts.

**Tech Stack:** MDX/YAML frontmatter, Ruby para guardrails, ripgrep, Git e a ferramenta built-in `image_gen`.

## Global Constraints

- Os três posts devem permanecer com `published: false`.
- Não alterar datas, títulos, tags, fatos, ressalvas, estrutura ou traduções fora da remoção dos três hyperlinks.
- Não atualizar `coverImage` antes da revisão visual e do upload da capa para o CDN.
- A capa não pode conter título, slogan, pessoas identificáveis, texto adicional ou watermark.
- Usar `/tmp/ranimontagna-cover-reference/lemon-brand.png` como referência oficial do símbolo da Lemon.
- Não fazer push, merge ou publicação nesta etapa.

---

### Task 1: Remover o link do FAQ nas três versões

**Files:**
- Modify: `posts/pt/2026-07-14-eu-nao-conhecia-a-lemon.mdx:79`
- Modify: `posts/en/2026-07-14-eu-nao-conhecia-a-lemon.mdx:79`
- Modify: `posts/es/2026-07-14-eu-nao-conhecia-a-lemon.mdx:79`

**Interfaces:**
- Consumes: os três artigos em estado de rascunho e a URL `https://lemonenergy.notion.site/FAQ-Processo-Seletivo-df36ec30b9a7493783fff7b3a3eed476`.
- Produces: os mesmos parágrafos e fatos sem hyperlink, com os outros quatro links preservados.

- [ ] **Step 1: Demonstrar que o guardrail de ausência ainda falha**

```bash
if rg -q 'https://lemonenergy\.notion\.site/FAQ-Processo-Seletivo-df36ec30b9a7493783fff7b3a3eed476' \
  posts/pt/2026-07-14-eu-nao-conhecia-a-lemon.mdx \
  posts/en/2026-07-14-eu-nao-conhecia-a-lemon.mdx \
  posts/es/2026-07-14-eu-nao-conhecia-a-lemon.mdx
then
  printf '%s\n' 'expected pre-change failure: FAQ URL still present'
  exit 1
fi
```

Expected: exit `1` and the explicit pre-change message.

- [ ] **Step 2: Remover somente a sintaxe Markdown dos três links**

Use `apply_patch` para transformar:

```md
No [FAQ público do processo seletivo](URL),
In its [public interview-process FAQ](URL),
En el [FAQ público del proceso de selección](URL),
```

em:

```md
No FAQ público do processo seletivo,
In its public interview-process FAQ,
En el FAQ público del proceso de selección,
```

Mantenha todo o restante de cada parágrafo byte a byte.

- [ ] **Step 3: Validar ausência da URL, conteúdo preservado e estado de draft**

```bash
ruby -ryaml -rdate -e '
url = "https://lemonenergy.notion.site/FAQ-Processo-Seletivo-df36ec30b9a7493783fff7b3a3eed476"
ARGV.each do |path|
  text = File.read(path)
  abort("FAQ URL remains: #{path}") if text.include?(url)
  abort("NotebookLM missing: #{path}") unless text.include?("NotebookLM")
  match = text.match(/\A---\n(.*?)\n---\n/m) or abort("frontmatter missing: #{path}")
  data = YAML.safe_load(match[1], permitted_classes: [Date], aliases: false)
  abort("not draft: #{path}") unless data["published"] == false
  links = text.sub(/\A---\n.*?\n---\n/m, "").scan(/\]\((https:\/\/[^)]+)\)/).flatten
  abort("expected four source links: #{path}") unless links.length == 4
  puts "FAQ unlinked and draft preserved: #{path}"
end
' posts/pt/2026-07-14-eu-nao-conhecia-a-lemon.mdx posts/en/2026-07-14-eu-nao-conhecia-a-lemon.mdx posts/es/2026-07-14-eu-nao-conhecia-a-lemon.mdx
git diff --check
```

Expected: três confirmações, quatro links por idioma e nenhum erro de whitespace.

- [ ] **Step 4: Confirmar que o diff contém só três substituições e commitar**

```bash
git diff --stat
git diff -- posts/pt/2026-07-14-eu-nao-conhecia-a-lemon.mdx posts/en/2026-07-14-eu-nao-conhecia-a-lemon.mdx posts/es/2026-07-14-eu-nao-conhecia-a-lemon.mdx
git add posts/pt/2026-07-14-eu-nao-conhecia-a-lemon.mdx posts/en/2026-07-14-eu-nao-conhecia-a-lemon.mdx posts/es/2026-07-14-eu-nao-conhecia-a-lemon.mdx
git commit -m "fix(blog): remove FAQ links from Lemon announcement"
```

Expected: um commit com três inserções e três remoções, sem outras mudanças rastreadas.

### Task 2: Gerar a capa editorial para revisão

**Files:**
- Read: `/tmp/ranimontagna-cover-reference/lemon-brand.png`
- Create: `.superpowers/imagegen/2026-07-14-eu-nao-conhecia-a-lemon-cover.png`
- Verify only: `posts/pt/2026-07-14-eu-nao-conhecia-a-lemon.mdx`
- Verify only: `posts/en/2026-07-14-eu-nao-conhecia-a-lemon.mdx`
- Verify only: `posts/es/2026-07-14-eu-nao-conhecia-a-lemon.mdx`

**Interfaces:**
- Consumes: a referência oficial da Lemon e o design em `docs/superpowers/specs/2026-07-13-lemon-cover-faq-polish-design.md`.
- Produces: uma prévia bitmap horizontal para aprovação, sem URL pública e sem mutação dos artigos.

- [ ] **Step 1: Validar a referência e registrar o estado dos posts**

```bash
test -f /tmp/ranimontagna-cover-reference/lemon-brand.png
file /tmp/ranimontagna-cover-reference/lemon-brand.png
git diff -- posts/pt/2026-07-14-eu-nao-conhecia-a-lemon.mdx posts/en/2026-07-14-eu-nao-conhecia-a-lemon.mdx posts/es/2026-07-14-eu-nao-conhecia-a-lemon.mdx
```

Expected: PNG oficial disponível e nenhuma alteração de `coverImage`.

- [ ] **Step 2: Gerar a imagem com a ferramenta built-in `image_gen`**

Use a imagem oficial como referência e este prompt de produção:

```text
Use case: ads-marketing
Asset type: horizontal 16:9 editorial blog cover, final framing designed for 1376x768 display
Primary request: create a premium cinematic cover for a personal career article about beginning a new chapter at Lemon Energia, connecting renewable solar energy, software, data, and practical AI
Input images: Image 1 is the official Lemon brand reference; preserve the white symbol geometry accurately and use it only as a small brand mark
Scene/backdrop: a broad solar farm at sunrise, deep emerald foreground, luminous horizon, subtle atmosphere and natural depth
Subject: solar panels leading toward the horizon; extremely subtle thin green data connections moving across a few panels, suggesting operational software without becoming a literal interface
Style/medium: photorealistic editorial photography with restrained conceptual finishing, premium and human, not corporate stock photography
Composition/framing: wide 16:9 landscape; strong leading lines from lower left toward the sunrise; uncluttered negative space in the upper-right corner; small official white Lemon symbol in that upper-right safe area with generous margins; resilient to center cropping
Lighting/mood: hopeful sunrise, calm confidence, soft golden light balanced with Lemon green
Color palette: Lemon emerald green, deep forest green, white, restrained warm gold
Text (verbatim): no text
Constraints: no title, no slogan, no letters, no numbers, no identifiable people, no robot, no AI brain, no source code, no dashboard, no rooftop house, no exaggerated neon; keep the official brand symbol crisp, small, white, and geometrically faithful
Avoid: generic corporate advertising, greenwashing clichés, sci-fi spectacle, distorted solar panels, fake UI, extra logos, watermark
```

Use `referenced_image_paths` com `/tmp/ranimontagna-cover-reference/lemon-brand.png`. Salve ou copie a saída final para `.superpowers/imagegen/2026-07-14-eu-nao-conhecia-a-lemon-cover.png` antes de encerrar.

- [ ] **Step 3: Inspecionar e validar a prévia**

Abra a saída com `view_image` e confirme:

- orientação horizontal próxima de 16:9;
- painéis solares coerentes e horizonte legível;
- linhas digitais discretas;
- ausência de textos, pessoas identificáveis, watermark e elementos proibidos;
- símbolo branco pequeno no canto superior direito, sem deformação perceptível;
- área segura suficiente para recortes do blog.

Use `file` e `sips -g pixelWidth -g pixelHeight` para registrar formato e dimensões. Se houver um único desvio claro, faça uma segunda geração corrigindo apenas esse desvio e substitua a prévia local.

- [ ] **Step 4: Preservar o estado de rascunho**

```bash
rg -n '^published: false$|^coverImage:' posts/{pt,en,es}/2026-07-14-eu-nao-conhecia-a-lemon.mdx
git status --short --branch
```

Expected: os três posts continuam como draft, `coverImage` não mudou e a imagem fica somente na área local ignorada `.superpowers/` para revisão.

Não crie commit vazio para a imagem local e não faça upload ou publicação.
