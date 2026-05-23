# Supermercados VidAtiva — Landing Page

Landing page de supermercado com foco em delivery, desenvolvida como projeto prático da pós-graduação em Desenvolvimento Web. A página apresenta seções de hero com carrossel CSS, departamentos, serviços, timeline de entrega, depoimentos e FAQ, com atenção a semântica, acessibilidade, performance e experiência do usuário — tudo em HTML e CSS puros, sem JavaScript e sem dependência de frameworks externos.

---

## Identidade Visual

### Personalidade de Marca

O VidAtiva é posicionado como um supermercado **premium e acessível**, com personalidade visual enraizada no conceito *"Fresh and Healthy"*. O estilo é **minimalista com influências orgânicas**: sem poluição visual, espaço negativo generoso e uma interface tátil que remete à experiência de um mercado limpo e bem organizado.

A narrativa visual foca em **praticidade ágil** — o usuário sente a velocidade de uma experiência digital moderna, confortado pela elegância editorial de uma marca de qualidade.

### Cores

A paleta é inspirada na natureza e implementada como variáveis CSS no `:root` de `style.css`:

| Token | Valor | Papel |
|---|---|---|
| `--color-primary` | `#0d631b` | Verde musgo — identidade da marca, ações primárias |
| `--color-secondary-container` | `#fe851f` | Âmbar quente — urgência, promoções, CTAs de conversão |
| `--color-background` | `#f7fbf0` | Creme off-white — fundo geral, reduz fadiga visual |
| `--color-card` | `#ffffff` | Branco puro — superfície elevada de cards, cria camadas |
| `--color-on-surface` | `#181d17` | Quase preto — textos principais, máximo contraste |
| `--color-on-surface-variant` | `#40493d` | Cinza médio — textos de suporte e legendas |

As sombras usam uma abordagem **tintada com verde** (opacidade 8–16% sobre a cor primária) em vez de preto puro, reforçando sutilmente a identidade da marca mesmo na elevação.

### Tipografia

O sistema usa **contraste intencional entre duas famílias**:

- **Noto Serif** (`--font-display`) — face editorial para títulos. Transmite autoridade, herança e confiança. Usado com `letter-spacing: -0.02em` para aparência compacta e "logo-like".
- **Plus Jakarta Sans** (`--font-body`) — face funcional para corpo e UI. Arredondada, legível e amigável em telas pequenas. `line-height: 1.6` mantém a promessa de "fresh and airy" na experiência de leitura.

### Espaçamento

Baseado em uma unidade de **8px**, com escala definida pelas variáveis `--space-xs` (4px) a `--space-xl` (40px). Espaçamentos generosos entre seções (`--space-xl`) garantem que o conteúdo respire — reflexo direto da personalidade "fresh".

### Elevação e Camadas

Hierarquia visual em três níveis, sem sombras agressivas:

1. **Nível 0 — Fundo:** `--color-background` (creme off-white `#f7fbf0`)
2. **Nível 1 — Cards:** `--color-card` (branco `#ffffff`) com sombra verde difusa
3. **Nível 2 — Sobreposições:** branco com sombra de média difusão e `backdrop-filter: blur`

### Formas

Linguagem de formas **orgânica e suave**. Componentes padrão usam `--radius-sm` (8px); containers maiores usam `--radius-lg` (16px) e `--radius-xl` (24px). Botões e badges adotam `--radius-full` (pill-shaped) — reforça a personalidade ágil e amigável. Cantos retos de 90° são evitados em toda a interface.

---

## Como cada requisito foi resolvido

### 1. Estrutura Semântica Rigorosa

Substituídas todas as `<div>` genéricas por tags HTML5 com significado próprio:

- `<aside aria-label="Promoção">` para a barra de anúncio do topo
- `<nav aria-label="Departamentos">` com `<ul>/<li>` para os links de categoria
- `<main id="main-content">` para delimitar o conteúdo principal
- `<article>` para cada card de serviço e depoimento
- `<ol>/<li>` para a timeline numerada de passos de entrega
- `<blockquote>` para as citações dos clientes e `<cite>` para seus nomes
- `<address>` para as informações de endereço no rodapé
- `<details>/<summary>` para o accordion de FAQ sem JavaScript
- `aria-hidden="true"` nos elementos decorativos (carrossel, números da timeline, ícones nos botões)

---

### 2. Sistema de Design com Variáveis CSS

Bloco `:root` no topo do `style.css` centraliza toda a identidade visual. Para trocar o tema basta editar esses valores — nenhum outro arquivo precisa ser alterado:

- **Cores:** `--color-primary`, `--color-secondary`, `--color-background`, `--color-surface`, `--color-card` e demais tokens semânticos de UI (`--color-header-bg`, `--color-nav-text`, `--color-footer-link` etc.)
- **Tipografia:** `--font-display`, `--font-body`, escala de tamanhos (`--text-sm` a `--text-3xl`) e pesos (`--weight-regular` a `--weight-bold`)
- **Espaçamento:** `--space-xs` a `--space-xl`
- **Bordas:** `--radius-sm` a `--radius-full`
- **Sombras:** `--shadow-sm`, `--shadow-md`, `--shadow-lg`
- **Transições:** `--t-fast`, `--t-normal`, `--t-slow`

---

### 3. Layout Híbrido (Flex & Grid)

Classes CSS puras definidas em `style.css`, sem dependência de framework:

- **Flexbox** (`.layout-flex`, `.site-nav`, `.hero-actions`, `.header-inner`): alinhamento de menus, botões e grupos de elementos inline, com `gap` via variável CSS
- **Grid** (`.layout-grid`, `.layout-grid-3`, `.bento`, `.rates-grid`, `.slots-grid`): grade principal de conteúdo com `grid-template-columns` responsivo definido por breakpoints, incluindo o bento grid da seção de delivery (`2fr 1fr` em telas grandes)

---

### 4. Interface Responsiva (mobile-first)

100% CSS puro, sem framework. As regras base definem o layout mobile; media queries expandem progressivamente:

- `@media (min-width: 640px)` — botões do hero em linha, grid de 2 colunas para taxas de entrega
- `@media (min-width: 768px)` — nav desktop visível, grids de 3 colunas, timeline horizontal, footer em 3 colunas, departamentos em grid de 5 colunas
- `@media (min-width: 1024px)` — bento grid em `2fr 1fr`
- `@media (max-width: 639px)` — carrossel com `background-position: 65% center` para evitar cortes em mobile
- **Tipografia fluida (`clamp()`)** em todos os níveis de heading — `h1`, `h2` (section-title, dept), `h3` (serviços, delivery, FAQ) — transições suaves de tamanho entre breakpoints sem saltos abruptos

---

### 5. Microinterações de Feedback

Todas as animações são CSS puro, sem JavaScript:

- **Hero:** quatro elementos (badge, título, subtítulo e botões) entram com `@keyframes fadeInUp` em cascata, com `animation-delay` escalonado de 0,1 s a 0,55 s
- **Cards:** `.card-hover` aplica `transform: translateY(-5px)` e `box-shadow` no hover
- **Botões:** `.btn-press` aplica `transform: scale(0.95)` e `opacity: 0.88` no `:active`
- **Scroll-reveal:** `.reveal` usa CSS Scroll-Driven Animations (`animation-timeline: view()`) — a animação dispara pela posição de rolagem, sem JavaScript; `@supports not` garante fallback para navegadores sem suporte
- **FAQ:** abertura do `<details>` animada com `fadeInUp` via `details > div`; seta rotacionada com `.faq-item[open] .faq-expand-icon { transform: rotate(180deg); }`

---

### 6. Curadoria de Código com IA

O componente de FAQ (accordion com `<details>/<summary>`) foi gerado e refinado com auxílio de IA. O processo está documentado em um bloco de comentário HTML diretamente antes da seção no `index.html`, contendo:

- O prompt usado para gerar o componente
- O trecho de código original devolvido pela IA
- Os 5 ajustes realizados durante a validação: adequação do espaçamento interno, rotação da seta animada com CSS puro via seletor `[open]`, confirmação do suporte nativo de ARIA no `<details>`, manutenção do atributo `open` na primeira entrada e delegação da animação de abertura ao CSS

---

### 7. Dark Mode Nativo (`prefers-color-scheme`)

Implementado inteiramente em CSS, sem JavaScript e sem classes utilitárias:

- Bloco `@media (prefers-color-scheme: dark)` em `style.css` sobrescreve as variáveis do `:root` — cores de fundo, superfícies, textos, bordas e sombras se adaptam automaticamente à preferência do sistema
- O elemento `<picture>` na logomarca serve `logomarca-dark.svg` (verde claro) em modo escuro e `logomarca-light.svg` (verde escuro) em modo claro, via `<source media="(prefers-color-scheme: dark)">`
- Nenhuma classe ou atributo no HTML precisa ser alterado para a troca de tema ocorrer

---

### 8. Sticky Header e Scroll Snap

- **Sticky header:** `.site-header { position: sticky; top: 0; z-index: 50; }` definido em `style.css`, mantendo a navegação sempre visível durante a rolagem
- **Scroll suave:** `scroll-behavior: smooth` no seletor `html` anima a navegação por âncoras
- **Scroll snap:** `scroll-snap-type: y proximity` no `html` e `scroll-snap-align: start` em cada `<section>` — o modo `proximity` encaixa suavemente as seções sem travar a rolagem em seções longas

---

### 9. Otimização de Performance e Assets

- **Imagens do carrossel:** reduzidas de 10 para **3 slides**, convertidas para **WebP** e hospedadas localmente na pasta `imagens/` (~87 KB total) — elimina todas as requisições externas ao CDN do Unsplash e reduz o payload de ~11,6 MB em 99%; `fetchpriority="high"` no `<img class="hero-lcp">` garante que o LCP (primeiro frame visível) carregue com prioridade máxima; caminhos relativos (`imagens/slide-01.webp`) garantem funcionamento em localhost e GitHub Pages
- **Logomarca:** dois arquivos SVG vetoriais locais (`logomarca-light.svg` / `logomarca-dark.svg`) substituem imagens externas; SVG não perde qualidade em nenhuma resolução
- **Meta description** adicionada para SEO e pré-visualização em mecanismos de busca
- **Imagem hero** (elemento LCP): `fetchpriority="high"` no `<img class="hero-lcp">` sinaliza prioridade máxima ao browser
- **Logo do cabeçalho:** `decoding="async"` para decodificação assíncrona sem bloquear a thread principal
- **Logo do rodapé:** `loading="lazy"` adia o carregamento até a aproximação do elemento
- **Fontes hospedadas localmente:** Noto Serif (v33) e Plus Jakarta Sans (v12) servidas da pasta `fontes/` via `@font-face` com `font-display: swap` — elimina as requisições render-blocking ao Google Fonts e reduz o FCP em ~7 s; `<link rel="preload">` para os dois arquivos críticos (Noto Serif 700 e Plus Jakarta Sans 400) garante que as fontes acima do fold estejam prontas antes do primeiro paint
- **Ícones SVG inline:** os 11 ícones do Material Symbols Outlined foram substituídos por SVG inline diretamente no HTML — elimina a última dependência de CDN externo em runtime. A substituição foi motivada por desempenho: a fonte de ícones do Google era render-blocking (~7 s no 4G simulado do Lighthouse), impedindo o primeiro paint; com SVG inline, zero requisições extras são feitas e as cores herdam automaticamente via `fill: currentColor`, mantendo visual idêntico ao original
- **Favicon SVG:** `<link rel="icon" href="logomarca-light.svg" type="image/svg+xml">` — sem arquivo extra, reaproveitando o SVG da logomarca; escalável em qualquer resolução
- **`<meta name="theme-color">`** com `media` para light/dark — colore a barra de endereço no Android Chrome com a cor correta do tema ativo
- **Open Graph** — `og:title`, `og:description`, `og:image`, `og:locale` e `og:site_name` para preview rico em redes sociais, WhatsApp e apps de mensagem
- **`color-scheme: light dark`** no `:root` — sinaliza ao browser suporte nativo a ambos os temas; scrollbars, inputs e elementos nativos usam automaticamente o esquema correto
- **`content-visibility: auto`** nas seções abaixo do fold (serviços, delivery, depoimentos, FAQ) — browser pula cálculo de layout e paint até o usuário rolar até elas, reduzindo o trabalho da thread principal

---

### 10. Acessibilidade Avançada com Teclado

- **Skip link:** `<a class="skip-link" href="#main-content">` com `position: fixed; top: -100%` — aparece visualmente apenas ao receber foco via Tab, permitindo pular a navegação diretamente ao conteúdo
- **`:focus-visible`:** contorno verde de 3 px com halo semitransparente, visível na navegação por teclado e invisível em cliques com mouse (`:focus:not(:focus-visible) { outline: none }`)
- **`aria-current="page"`** no link ativo da navegação principal
- **`aria-label`** nos botões sem texto visível (carrinho de compras e menu hambúrguer)
- **`aria-hidden="true"`** nos ícones decorativos dentro desses botões
- **Contraste corrigido** após auditoria Lighthouse: botão "Agendar minha entrega" (2,4:1 → 4,6:1) e links do rodapé (4,3:1 → 10:1)
- **Hierarquia de títulos corrigida:** `<h4>` do rodapé alterados para `<h3>`, mantendo a sequência `h1 → h2 → h3` sem saltos
- **`@media (prefers-reduced-motion: reduce)`** — quando o usuário ativa "Reduzir movimento" no SO, todas as animações decorativas são desativadas (carrossel, fadeInUp, scroll-reveal); apenas transições funcionais são preservadas

---

## Estrutura de arquivos

```
Projeto com HTML e CSS/
├── index.html               # Estrutura, conteúdo e ícones SVG inline (zero CDN em runtime)
├── style.css                # Design system, layout, animações e acessibilidade
├── logomarca-light.svg      # Logo modo claro (verde escuro #2E7D32)
├── logomarca-dark.svg       # Logo modo escuro (verde claro #81C784)
├── fontes/                  # Fontes locais (woff2) — Noto Serif v33 + Plus Jakarta Sans v12
│   ├── noto-serif-v33-latin-400.woff2
│   ├── noto-serif-v33-latin-600.woff2
│   ├── noto-serif-v33-latin-700.woff2
│   ├── plus-jakarta-sans-v12-latin-400.woff2
│   ├── plus-jakarta-sans-v12-latin-500.woff2
│   ├── plus-jakarta-sans-v12-latin-600.woff2
│   └── plus-jakarta-sans-v12-latin-700.woff2
├── imagens/                 # 3 imagens do carrossel em WebP (~87 KB total)
│   ├── slide-01.webp        # (preloaded — elemento LCP)
│   ├── slide-02.webp
│   └── slide-03.webp
└── README.md                # Este arquivo
```

> **Zero dependências externas em runtime.** Todos os recursos (fontes, ícones, imagens, logomarca) são servidos localmente. O projeto funciona completamente offline e sem nenhuma requisição a CDN externo após a carga inicial.
