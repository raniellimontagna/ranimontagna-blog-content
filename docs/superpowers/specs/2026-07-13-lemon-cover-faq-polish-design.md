# Design: capa e ajuste do FAQ no artigo da Lemon

## Contexto

O pacote trilíngue `2026-07-14-eu-nao-conhecia-a-lemon.mdx` já está em `main` como rascunho (`published: false`). Este refinamento remove um link editorialmente desnecessário do trecho sobre o FAQ público da Lemon e cria uma capa própria para revisão antes de qualquer publicação.

## Decisões aprovadas

### Menção ao FAQ

- Manter, nos três idiomas, a informação de que o FAQ público do processo seletivo menciona NotebookLM e soluções de IA aplicadas à base de conhecimento.
- Remover somente o hyperlink de `FAQ público do processo seletivo`, `public interview-process FAQ` e `FAQ público del proceso de selección`.
- Não remover as ressalvas que separam fatos públicos, opinião pessoal e iniciativas ainda não implementadas.
- Preservar todos os outros links, fatos, traduções e o estado `published: false`.

### Capa

- Formato horizontal 16:9 para capa de blog.
- Cena editorial cinematográfica e realista de um campo de painéis solares ao amanhecer.
- Horizonte iluminado como metáfora visual do novo capítulo profissional.
- Linhas digitais verdes muito sutis conectando os painéis, sugerindo software, dados e IA sem mostrar cérebro, robô, código ou dashboard.
- Paleta de verde Lemon, verde profundo, branco e luz dourada suave.
- Símbolo oficial branco da Lemon, pequeno no canto superior direito, com ampla margem e geometria preservada a partir da referência oficial.
- Sem título, slogan, pessoas identificáveis, texto adicional ou watermark.
- Evitar estética de banco de imagens, excesso de efeitos futuristas, neon dominante e aparência de anúncio corporativo.

## Referências e entregáveis

- Referência oficial da marca: `/tmp/ranimontagna-cover-reference/lemon-brand.png`.
- Prévia final: `.superpowers/imagegen/2026-07-14-eu-nao-conhecia-a-lemon-cover.png`.
- O arquivo gerado permanece local para revisão visual. O `coverImage` dos posts não será trocado até a aprovação da capa e sua disponibilização em uma URL do CDN usada pelo blog.

## Validação

- Os três artigos continuam com o mesmo basename, data e `published: false`.
- A URL do FAQ fica ausente nos três corpos, enquanto `NotebookLM` e as ressalvas continuam presentes.
- Os outros quatro links permanecem intactos e na mesma ordem.
- A capa é horizontal, legível em recorte de card, não contém texto inventado e segue a direção visual aprovada.
- O símbolo da Lemon deve ser reconhecível, pequeno e sem deformações perceptíveis.

## Fora de escopo

- Publicar o artigo.
- Alterar fatos, cargo, datas, traduções ou a estrutura narrativa.
- Fazer upload no CDN ou trocar `coverImage` antes da revisão da imagem.
