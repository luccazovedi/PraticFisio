# Pratic Fisio

Landing page one-page para a Pratic Fisio, clínica de fisioterapia da Dra. Cristiane Moura (São Paulo). Site institucional focado em geração de contato via WhatsApp, apresentando serviços, o programa "Antes da Queda", metodologia de atendimento e FAQ.

**Site em produção:** https://www.praticfisio.com/

## Stack

Arquivo único (`index.html`) sem build, framework ou dependências de runtime:

- **HTML5** semântico
- **CSS** puro, inline em `<style>`, com custom properties (variáveis) e media queries para responsividade
- **JavaScript** vanilla inline em `<script>`, sem bibliotecas externas
- **Google Fonts**: `Fraunces` (títulos/serifada) e `Outfit` (corpo/sans-serif), carregadas via `<link>`
- **Schema.org JSON-LD** para SEO (tipo `Physiotherapy`)

Não há `package.json`, bundler ou processo de build — basta abrir/servir o `index.html` diretamente.

## Como rodar localmente

Como é um HTML estático, qualquer servidor simples funciona:

```bash
# Opção 1: abrir direto no navegador
start index.html          # Windows
open index.html           # macOS

# Opção 2: servidor local (recomendado para testar SW/fetch/etc.)
python -m http.server 8000
# depois acesse http://localhost:8000
```

## Estrutura do arquivo

Tudo vive em [index.html](index.html), organizado em três blocos:

1. **`<head>`** (linhas 1–362) — meta tags, Open Graph, JSON-LD (dados estruturados do negócio), fontes e todo o CSS em `<style>`
2. **`<body>`** (linhas 363–743) — header, seções da página, footer, barra fixa mobile e o `<script>` de comportamento

### Seções da página (`<main>`)

| Seção | ID | Conteúdo |
|---|---|---|
| Hero | `#top` | Título principal, CTA para WhatsApp, painel lateral "Primeira conversa sem custo" |
| Por onde começar | `#para-quem` | Grid de 4 "dores de entrada" (dor crônica, medo de cair, sedentarismo, lesão) que linkam para outras seções |
| Serviços | `#servicos` | Grid com os 6 tipos de atendimento (domiciliar, clínica, teleconsulta, Pilates clínico, grupos, consultoria online) |
| Antes da Queda | `#antes-da-queda` | Programa preventivo em grupo para condomínios (prevenção de quedas em idosos) |
| Como funciona | `#metodo` | 4 passos do atendimento, do contato inicial à alta |
| Sobre | `#sobre` | Bio da Dra. Cristiane Moura, missão e valores da clínica |
| Dúvidas | `#duvidas` | FAQ em `<details>/<summary>` (acordeão nativo, sem JS de abertura) |
| CTA final | `#contato` | Chamada final + telefone/e-mail/Instagram |

Depois do `<main>`: `<footer>` com links de navegação e nota legal, e uma `.dock` (barra fixa no rodapé, mobile-only) com botões "Ligar" e "WhatsApp".

## Sistema de design (CSS)

Variáveis definidas em `:root` (linha 45+):

```css
--ink:    #0F3B36   /* verde escuro — texto principal, fundos escuros */
--ink-2:  #1C5F55   /* verde escuro, hover */
--paper:  #FBF8F3   /* bege claro — fundo padrão */
--paper-2:#F2ECE1   /* bege, fundo de seções alternadas */
--clay:   #C4623F   /* terracota — cor de destaque/CTA */
--sand:   #D9C9A8   /* areia — acentos secundários */
```

- Tipografia: `Fraunces` (`--display`) para títulos, `Outfit` (`--body`) para texto corrido
- Layout: `.wrap` centraliza o conteúdo (`max-width: 1120px`), `.sec` controla o padding vertical das seções
- Breakpoints: mobile-first, com ajustes em `≥600px` e `≥900px`
- Animação de entrada: classe `.rv` (reveal) + `IntersectionObserver` no JS revela elementos ao rolar a página
- Respeita `prefers-reduced-motion: reduce` (desativa animações)

## Comportamento (JavaScript)

No final do `<body>` (linha 714+):

1. Atualiza o ano no rodapé (`#yr`) automaticamente
2. Adiciona borda no header quando a página é rolada (`.stuck`) e revela a barra fixa mobile (`.dock`) após 480px de scroll
3. `IntersectionObserver` para animar elementos `.rv` conforme entram na viewport
4. Fecha automaticamente outros itens do FAQ quando um `<details>` é aberto (acordeão exclusivo)

## Pontos de contato editáveis

Se precisar atualizar informações de contato, ajuste nos seguintes locais (todos usam o mesmo número):

- WhatsApp: `https://wa.me/5511993986807` (aparece em vários CTAs)
- Telefone: `tel:+5511993986807`
- E-mail: `crismourah@praticfisio.com`
- Instagram: `https://www.instagram.com/praticfisio/`

Esses dados também aparecem duplicados no JSON-LD (linhas 21–42), que deve ser mantido em sincronia para SEO.

## SEO

- Meta description e Open Graph configurados no `<head>`
- `rel="canonical"` apontando para `https://www.praticfisio.com/`
- Dados estruturados (`schema.org/Physiotherapy`) descrevendo serviços, área de atuação e fundadora
- Título da página inclui marca, especialidade e nome da profissional

## Acessibilidade

- Link "Ir para o conteúdo" (skip link) no topo, visível apenas ao focar via teclado
- `:focus-visible` com contorno customizado em toda a página
- Ícones decorativos marcados com `aria-hidden="true"`
- Navegação com `aria-label` (`Navegação principal`, `Rodapé`)
- Animações desativadas para usuários com `prefers-reduced-motion`
