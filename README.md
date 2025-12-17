# Blog Content Repository

Repositório dedicado para armazenar o conteúdo do blog [ranimontagna.com](https://ranimontagna.com).

## 📁 Estrutura

```
ranimontagna-blog-content/
└── posts/
    ├── pt/          # Posts em Português
    ├── en/          # Posts em Inglês
    └── es/          # Posts em Espanhol
```

## 📝 Formato dos Posts

Os posts são arquivos MDX (Markdown + JSX) com frontmatter:

```mdx
---
title: "Título do Post"
date: "2024-01-15"
description: "Breve descrição do post"
tags: ["tag1", "tag2"]
published: true
---

# Conteúdo do post

Seu conteúdo em Markdown aqui...
```

## 🔧 Gerenciamento

Os posts são criados e gerenciados através do **Admin Panel**:
- **Repositório Admin:** [admin.ranimontagna.com](https://github.com/RanielliMontagna/admin.ranimontagna.com)
- **CRUD:** Create, Read, Update, Delete via GitHub API
- **Deploy:** Automático via Vercel (webhook)

## 📋 Convenções de Nomenclatura

Os arquivos devem seguir o padrão:
```
YYYY-MM-DD-slug-do-post.mdx
```

Exemplos:
- `2024-01-15-introducao-nextjs.mdx`
- `2024-02-20-typescript-best-practices.mdx`

## 🌍 Multi-idioma

- **Português (pt):** Idioma principal
- **Inglês (en):** Traduções
- **Espanhol (es):** Traduções

Cada idioma tem sua própria pasta para manter a organização.

### ⚠️ Importante: Slugs Consistentes

**O slug DEVE ser o mesmo em todos os idiomas** para permitir que o blog faça a ligação entre traduções.

**✅ Correto:**
```
posts/pt/2024-01-15-introducao-nextjs.mdx
posts/en/2024-01-15-introducao-nextjs.mdx
posts/es/2024-01-15-introducao-nextjs.mdx
```

**❌ Errado:**
```
posts/pt/2024-01-15-introducao-nextjs.mdx
posts/en/2024-01-15-introduction-nextjs.mdx  ← Slug diferente!
posts/es/2024-01-15-introduccion-nextjs.mdx  ← Slug diferente!
```

O admin garantirá automaticamente que o slug seja o mesmo ao criar traduções.

## 🔐 Acesso

Este repositório é privado e gerenciado via GitHub API pelo painel administrativo.

## 🚀 Como Funciona

1. **Admin cria post** → Commit neste repo
2. **GitHub Webhook** → Notifica Vercel
3. **Vercel rebuild** → Blog atualizado automaticamente
