---
name: RumBee
description: Sistema de design da RumBee — grafite e âmbar, Archivo, densidade confortável, dark e light
colors:
  grafite: "#0E1013"
  chrome: "#0B0D10"
  superficie: "#1B2028"
  borda: "#262B33"
  osso: "#ECE9E2"
  nevoa: "#8A9099"
  ambar: "#E8A020"
  ambar-ink: "#8A5A05"
  paper: "#F7F6F2"
  tinta: "#17181B"
typography:
  h1: { fontFamily: "Archivo, system-ui, sans-serif", fontSize: "24px", fontWeight: 700, lineHeight: 1.2, letterSpacing: "-0.02em" }
  h2: { fontFamily: "Archivo, system-ui, sans-serif", fontSize: "20px", fontWeight: 700, lineHeight: 1.3 }
  h3: { fontFamily: "Archivo, system-ui, sans-serif", fontSize: "16px", fontWeight: 600, lineHeight: 1.4 }
  body: { fontFamily: "Archivo, system-ui, sans-serif", fontSize: "13.5px", fontWeight: 400, lineHeight: 1.55 }
  label: { fontFamily: "Archivo, system-ui, sans-serif", fontSize: "11px", fontWeight: 600, letterSpacing: "0.05em" }
  caption: { fontFamily: "Archivo, system-ui, sans-serif", fontSize: "11.5px", fontWeight: 400 }
rounded: { sm: "6px", md: "8px", lg: "12px", xl: "16px", pill: "9999px" }
spacing: { 1: "4px", 2: "8px", 3: "12px", 4: "16px", 5: "20px", 6: "24px", 8: "32px" }
components:
  button-primary: { backgroundColor: "#E8A020", textColor: "#17130A", rounded: "8px", height: "38px", padding: "0 18px" }
  button-secondary: { backgroundColor: "#1B2028", textColor: "#ECE9E2", rounded: "8px", height: "38px", padding: "0 16px" }
  input-default: { backgroundColor: "#1B2028", textColor: "#ECE9E2", rounded: "8px", height: "44px", padding: "0 14px" }
  card-default: { backgroundColor: "#1B2028", rounded: "12px", padding: "20px" }
---

# RumBee — Sistema de Design

Versão 1.2 · Outubro 2026 · **genérico, para qualquer produto RumBee**

Este documento define **como uma coisa é**: token, anatomia, medida, contraste.
**Como uma coisa se comporta** — onde fica o CTA, o que o clique na linha faz, onde vive o
excluir, o que a confirmação pergunta — está em `INTERACTIONS.md`, e as duas leituras são
necessárias antes de construir uma tela.

A marca (conceito, símbolo, voz) mora em `BRAND.md`. O que é específico de um produto
(domínio, telas, vocabulário) mora em `DESIGN-<produto>.md`. Os valores implementados
moram em `tokens.css`; aqui está o **porquê** e o **como usar**.

---

## 1. Fundamentos

### 1.1 Postura

Produto de trabalho, para quem passa o dia dentro dele. Isso define tudo:

- **Densidade confortável, não apertada.** Linha de 44px. O operador vê muita informação
  sem ler apertado.
- **A ação fica onde a mão já está.** Ação de linha na linha, ação de tela no topo da
  tela, ação de registro no rodapé do modal.
- **Neutro carrega a informação; âmbar carrega a decisão.**
- **Nada decorativo.** Sem glassmorphism, sem gradiente de wallpaper, sem ilustração
  genérica, sem card repetido só para preencher a grade.

### 1.2 As dez regras que mais quebram

1. **Uma família tipográfica:** Archivo. Hierarquia por tamanho e peso — nunca por
   troca de família. **Zero mono**, inclusive em valor monetário e ID.
2. **Âmbar ≤ 8% da tela.** Um primário por viewport.
3. **Fill âmbar é igual nos dois temas** (`#E8A020` + texto `#17130A`). O que muda entre
   temas é **texto/link âmbar**: `--accent-ink` escurece para `#8A5A05` no claro.
4. **A sidebar nunca clareia.** Grafite `#0B0D10` nos dois temas — é a âncora da marca.
5. **Ícone e logo nunca lado a lado.** Expandido → logo; recolhido → ícone.
6. **Sem rolagem lateral em tabela** sem necessidade: `table-layout:fixed` +
   `<colgroup>` + `text-overflow:ellipsis`. `min-width` só quando a tabela realmente
   não cabe, e aí o menor possível.
7. **Verde é estado terminal confirmado.** Valor apenas previsto é neutro.
8. **Todo texto ≥ 4.5:1**, incluindo rótulo 11px e texto de badge.
9. **Toda tabela tem seus quatro estados**: vazio, carregando, erro, sem permissão.
10. **`white-space:nowrap` em todo rótulo de botão, badge e cabeçalho de coluna.**

---

## 2. Tokens

A implementação canônica é `tokens.css`. Consuma por alias semântico (`var(--surface)`,
`var(--text-muted)`), não pela escala crua — assim o componente funciona nos dois temas
sem `if`.

### 2.1 Neutros

| Alias | Dark | Light | Uso |
|---|---|---|---|
| `--chrome` | `#0B0D10` | `#0B0D10` | sidebar — **não muda com o tema** |
| `--bg` | `#0E1013` | `#F7F6F2` | fundo da área de trabalho |
| `--surface` | `#1B2028` | `#FFFFFF` | card, tabela, modal |
| `--surface-raised` | `#171B21` | `#F3F1EB` | header de tabela, busca, menu |
| `--row-hover` | `#20262F` | `#F7F6F2` | hover de linha |
| `--border` | `#262B33` | `#E4E1D8` | toda borda e divisor |
| `--text` | `#ECE9E2` | `#17181B` | texto principal |
| `--text-muted` | `#8A9099` | `#5F6266` | texto secundário |
| `--text-faint` | `#9AA0A8` | `#6B6E72` | rótulo, timestamp — **é o piso AA, não vá além** |

> **Por que `--text-faint` não é mais claro:** o terciário existe para hierarquia, mas
> rótulo de coluna e legenda são conteúdo. `#5A616C` sobre `#0E1013` dá 3.6:1 e reprova.
> `#9AA0A8` dá 6.4:1 e ainda lê como terciário.

### 2.2 Âmbar

| Alias | Valor | Uso |
|---|---|---|
| `--accent` | `#E8A020` | fill de primário, barra do item ativo, anel de foco, barra de gráfico "previsto" |
| `--accent-on` | `#17130A` | texto sobre fill âmbar (12.6:1) |
| `--accent-ink` | dark `#E8A020` · light `#8A5A05` | **texto ou link** em âmbar |
| `--accent-tint` | dark `rgba(232,160,32,0.10)` · light `#FDF3E2` | fundo de linha selecionada, etapa ativa |

> **A armadilha:** `#E8A020` com texto branco dá 2.1:1 — reprova. A solução não é clarear
> o âmbar, é **usar texto escuro sobre o âmbar**. E âmbar como *texto* sobre paper dá
> 2.4:1 — daí o `--accent-ink` escuro no tema claro. O fill é constante; a tinta muda.
>
> **O mesmo erro de categoria, com o vermelho:** `--err-text` (`#F87171` no dark) é uma cor
> de **texto sobre fundo neutro**. Usada como **fundo** de botão com texto branco dá
> **2.77:1** e reprova. Por isso existe `--err-fill` (`#B3261E`, constante nos dois temas,
> 6.5:1 com branco). **Regra geral: cor de texto não vira cor de fundo.** Se um papel
> precisa de fill, ele tem um token `-fill` próprio.

### 2.3 Semânticas — pares bg/texto por tema

| Papel | Dark bg | Dark texto | Light bg | Light texto |
|---|---|---|---|---|
| ok | `rgba(16,185,129,0.15)` | `#34D399` | `#D6F5E6` | `#046B4D` |
| warn | `rgba(245,158,11,0.15)` | `#FBBF24` | `#FDF0CF` | `#8A5A05` |
| err | `rgba(220,38,38,0.15)` | `#F87171` | `#FBE3E1` | `#B3261E` |
| err · **fill** | `#B3261E` | branco | `#B3261E` | branco |
| info | `rgba(8,145,178,0.18)` | `#22D3EE` | `#D9F1F7` | `#0E5C70` |
| neutral | `rgba(138,144,153,0.18)` | `#B9BEC5` | `#EFEDE6` | `#5F6266` |

Valores: positivo `--positive`, negativo `--negative` (resolvem por tema).

> **Tint de mesma matiz não fecha AA.** O par neutro nasceu com texto `#8A9099` sobre
> tint `rgba(138,144,153,0.18)` — mesma cor em alfa baixo: 3.89:1, teto matemático abaixo
> do mínimo. Regra: **o texto de um badge é pelo menos 3 passos mais claro (dark) ou mais
> escuro (light) que a matiz do próprio tint.** E texto de corpo sobre superfície tingida
> usa `--text`, não `--text-muted`.
>
> **O tema claro não é o escuro invertido.** As semânticas do claro são tints opacos
> (`#D6F5E6`) com tinta profunda, não `rgba()` sobre paper — `#10B981`/`#DC2626` sobre
> fundo claro ficam ilegíveis.

### 2.4 Tipografia aplicada

| Uso | Tamanho | Peso |
|---|---|---|
| Título de página (`line-height:1.2`, `-0.02em`) | 24px | 700 |
| Subtítulo de página | 13px | 400 |
| Título de seção | 20px | 700 |
| Título de card | 16px | 600 |
| Título de modal | 16px | 700 |
| Corpo | 13.5px | 400 |
| Corpo secundário | 12.5px | 400 |
| Rótulo de campo de formulário (`--rb-size-label-field`) | 13px | 600 |
| Rótulo / overline (uppercase, 0.05em) | 11px | 600 |
| Legenda / metadado | 11.5px | 400 |
| Número grande de card | 23px | 600 |
| Valor em tabela | 13.5px | 500–600 |
| Texto de badge | 11–11.5px | 600 |
| Busca global | 15px | 400 |

**Overline de página é opcional.** O produto já aparece no logo da sidebar e no `<title>`.
Se um produto quiser `RUMBEE <PRODUTO>` acima do título, ele fica 4px antes do `<h1>` e os
28px do topo do conteúdo contam até o overline (§4.10). O estilo de rótulo continua o
mesmo para cabeçalho de coluna, rótulo de seção e rótulo de campo no detalhe.

### 2.5 Raio, controle, sombra, foco

```css
--rb-radius-sm: 6px;     /* badge, ícone de entidade */
--rb-radius-md: 8px;     /* input, botão, select */
--rb-radius-lg: 12px;    /* card, tabela */
--rb-radius-xl: 16px;    /* modal */
--rb-radius-pill: 9999px;/* chip, avatar, busca */

--rb-control-sm: 30px;   /* ação dentro de linha */
--rb-control-md: 38px;   /* padrão de toolbar */
--rb-control-lg: 44px;   /* formulário, autenticação */
--rb-search-h: 50px;
--rb-row-h: 44px;
```

Sombra só em coisa que flutua de verdade: menu (`--shadow-md`), modal (`--shadow-lg`).
Card **não** tem sombra — tem borda. Botão primário pode ter `--glow` âmbar.

Foco: `outline: 2px solid var(--accent); outline-offset: 2px`. Em input, borda âmbar +
`box-shadow: var(--focus-ring)` (anel de 3px, âmbar a 18%). **Nunca** o anel azul do
browser.

Movimento: 150ms para hover/estado, 220ms para entrada, 180ms para largura de sidebar.
Easing `cubic-bezier(0.16,1,0.3,1)`. **Sem bounce, sem elástico.**

---

## 3. O shell

Três regiões, iguais em todo produto RumBee. **É o shell que faz dois produtos
diferentes parecerem a mesma empresa** — não mude por produto.

### 3.1 Sidebar (`--chrome`, nunca clareia)

- **216px expandida / 68px recolhida**, `transition: width .18s ease`, estado em
  `localStorage`.
- **Topo (60px):** expandida → logo de texto claro (15px) + botão circular `‹`
  (24px, borda `#262B33`) para recolher. Recolhida → o ícone RumBee **é** o botão de
  expandir. Nunca os dois juntos.
- **Navegação:** item de 10px/12px, raio 8px, ícone 18px + rótulo 13.5px. Ativo = ícone
  âmbar + rótulo `--text` peso 600 + **barra vertical âmbar de 3px à esquerda**. Jamais
  fundo âmbar preenchido.
- **Recolhida, todo item tem tooltip** no hover: pílula `--surface-raised` a 54px da
  esquerda, centrada na vertical, `z-index:40`. Sem isso o menu recolhido é adivinhação.
- **Rodapé, o menu do usuário:** avatar 28px âmbar + nome + e-mail (recolhida, só o
  avatar, com tooltip do e-mail). Abre um menu para cima (224px), nesta ordem:
  1. e-mail da conta, como rótulo;
  2. **Alternar tema.** O toggle mora aqui, não no topbar. Persistido em
     `localStorage`; sem valor salvo, segue `prefers-color-scheme`;
  3. **Idioma**, quando o produto tem mais de um;
  4. **Gerenciar conta**, que abre o painel de conta do RumBee ID (§3.4), e as
     configurações de perfil próprias do produto, se houver;
  5. separador, **Termos de uso** e **Política de privacidade** (§3.4, nova aba);
  6. separador e **Encerrar sessão** (vermelho).

  **O usuário vive no rodapé da sidebar, não no topbar.**

**Grupo:** item que agrupa outros e não tem endereço próprio. Clicar só abre ou fecha;
nunca navega.

- **Marcação:** `<button aria-expanded aria-controls>`, com ícone de 18px e rótulo de
  13.5px como um item. Chevron de 14px à direita: `›` fechado, `⌄` aberto.
- **Abertura:** abre sozinho na página de um filho; fora disso começa fechado. O estado
  não é salvo.
- **Filhos:**
  - lista com recuo de 21px, para a linha guia ficar no centro do ícone do grupo;
  - linha guia de 1px em `--chrome-border` à esquerda, com 8px de padding até os itens;
  - cada filho com ícone (18px) e rótulo (13.5px).
- **Filho ativo:** a barra âmbar de 3px encosta na linha guia; ícone âmbar e peso 600.
- **Grupo fechado com filho ativo:** o grupo leva a barra âmbar e o peso 600, para o
  "onde estou" nunca sumir.
- **Separador:** antes do grupo vai uma linha de 1px em `--chrome-border`, com 8px de
  margem.
- **Sidebar recolhida:**
  - sem chevron; grupo e filhos com tooltip;
  - quando a sidebar pode expandir (tela larga), clicar no grupo expande a sidebar e abre
    o grupo, nunca fecha; a preferência salva passa a ser "expandida";
  - quando ela não pode expandir (produto que usa trilho fixo em tela estreita, em vez do
    drawer de §5), o grupo abre e fecha ali mesmo e os filhos viram ícones em sequência,
    sem recuo e sem linha guia, com a barra ativa na borda.
- **Rota do grupo:** redireciona pro primeiro filho. Cada filho é uma página, sem abas.
- **Fonte:** os filhos são `children` do item na constante única de navegação.

| Parte | Valor |
|---|---|
| Ícone (grupo e filho) | 18px, `stroke-width` 2 |
| Chevron | 14px |
| Recuo dos filhos | 21px |
| Linha guia | 1px `--chrome-border`, padding-left 8px |
| Barra ativa | 3px âmbar, cantos `--rb-radius-sm` do lado do conteúdo |
| Separador | 1px `--chrome-border`, margem vertical 8px |

### 3.2 Topbar (80px)

No máximo duas coisas: a **busca global**, quando o produto tem, e o **launcher de apps**
do RumBee ID.

- **Barra:** 80px, `position:sticky; top:0`, fundo `--bg`, `border-bottom: 1px solid
  var(--border)`, `padding: 0 32px` (16px abaixo de 768px). Existe mesmo sem busca: as
  medidas do conteúdo (§3.3) contam a partir dela.
- **Busca:** só em produto que tem busca global. Pílula de 50px, `max-width:760px`,
  `flex:1`, fundo `--search-bg`, ícone de lupa 20px a 20px da esquerda, texto 15px,
  padding-left 54px. No foco, borda âmbar + anel `rgba(232,160,32,0.15)` de 4px e fundo
  sobe para `--surface`. Onde existe, é a ferramenta mais usada do produto — tratar como
  campo principal, não como acessório. Sem busca, o topbar fica só com o launcher,
  alinhado à direita (`justify-content:flex-end`).
- **Launcher:** à direita, num slot do próprio topbar, montado pelo script do ID:

  ```html
  <div id="rumbee-launcher-slot"></div>
  <!-- no fim do <body> -->
  <script src="https://id.rumbee.ai/launcher.js" data-container="#rumbee-launcher-slot"
          data-theme="auto" data-lang="pt" defer></script>
  ```

  O botão (40px) e o painel são do RumBee ID: não reestilize, não copie, não
  reimplemente. `data-theme="auto"` acompanha o `data-theme` do `<html>`. O launcher
  autentica com a sessão Clerk da página (§3.4); o contrato do token está no
  `packages/satellite-sdk` do repo `docsales/rumbee-ID`. Sem o slot, ele flutua no canto
  da tela, e isso é fallback, não layout.
- **Nada mais.** Sem toggle de tema (está no menu do usuário), sem avatar, sem
  notificação, sem breadcrumb: tudo isso tem outro lugar.

### 3.3 Conteúdo

`padding: 28px 32px 40px`, coluna única, `gap:16px`. Ordem canônica:

1. **Cabeçalho de página** (§4.10): `<h1>` + subtítulo de uma linha à esquerda, ações de
   tela à direita. Nada acima dele.
2. **Barra de contexto** — card `--surface`, raio 12px: seletor de entidade, navegador de
   período, segmented, ações de escopo.
3. **Cards de resumo** — `repeat(auto-fit, minmax(180px, 1fr))`, gap 14px.
4. **Filtros da lista** — card raso com selects e busca local.
5. **A tabela.**
6. **Nota de proveniência** quando a tela é proposta e não recriação (ver §6).

- O cabeçalho é o primeiro elemento do conteúdo: fica a **28px do topbar** (20px abaixo
  de 768px). Nenhum `margin-top` no primeiro filho; a distância é o padding. As únicas
  coisas que podem vir antes dele são o overline opcional (§2.4) e a faixa de offline
  (§4.9), que só aparece enquanto dura.
- **Tela logada não tem hero.** Sem headline de marketing centrada. A ação principal da
  tela é a barra de contexto, um card abaixo do cabeçalho.
- O conteúdo começa na borda esquerda, alinhado ao título. Texto corrido pode limitar a
  própria largura (`max-width`), mas nunca fica centralizado numa coluna estreita.
  Tabelas ocupam a largura toda.
- Celular (<768px): `padding: 20px 16px 32px`.
- **App logado não tem rodapé de página.** O conteúdo termina no último bloco; Termos e
  Privacidade ficam no menu do usuário (§3.1).

### 3.4 Login, conta e termos

- **Login, cadastro e conta são do RumBee ID** (`id.rumbee.ai`). O produto não tem tela
  de login, cadastro nem recuperação de senha: quem chega sem sessão vai pro login do ID
  com a URL de volta, e a sessão é a do Clerk compartilhado pelos `*.rumbee.ai`. Um
  `/login` legado só redireciona. Integração: `packages/satellite-sdk` do repo
  `docsales/rumbee-ID` (comece pelo `AI-AGENT.md` de lá).
- **Gerenciar conta**, no menu do usuário, abre o painel de conta do RumBee ID. Nunca
  uma tela de perfil reimplementada para nome, e-mail, senha ou login social.
- **Termos e privacidade** moram no site institucional, numa URL só para a família toda:

  | Documento | URL canônica |
  |---|---|
  | Termos de uso | `https://www.rumbee.ai/pt-br/termos-de-uso` |
  | Política de privacidade | `https://www.rumbee.ai/pt-br/politica-de-privacidade` |

  O produto guarda as duas numa constante única e não hospeda cópia do texto. Se precisa
  de rota própria (`/termos`), ela redireciona pra URL canônica. Os links abrem em nova
  aba, com `rel="noopener noreferrer"`.
- **Tela pública tem rodapé legal:** erro, 404, página aberta por link-token e página
  pública do produto. Uma linha centralizada: `Termos de uso · Política de privacidade ·
  © <ano> RumBee`, 12.5px, `--text-muted`, links na mesma cor com sublinhado no hover,
  separador `·` (nunca `|`), `border-top: 1px solid var(--border)`, `padding: 16px`. Item
  próprio do produto (ex.: "Denunciar abuso") entra depois dos dois legais, antes do ©.

---

## 4. Componentes

### 4.1 Botões

| Variante | Fill | Texto | Uso |
|---|---|---|---|
| primário | `--accent` | `--accent-on` | uma ação por tela, com `--glow` |
| secundário | `--surface` + borda | `--text` | ação paralela |
| fantasma | transparente | `--text-muted` | cancelar, limpar |
| destrutivo | `--err-fill` (`#B3261E`, igual nos dois temas) | `--err-on-fill` (branco) | excluir — **fill vermelho profundo, nunca outline** |

38px em toolbar, 44px em formulário, 30px dentro de linha. Peso 700 no primário, 600 nos
outros. Ícone 15px, gap 8px. **`white-space:nowrap` sempre** — sem isso rótulos de duas
palavras quebram e desalinham a fileira.

Ordem no rodapé de modal de detalhe/edição: destrutiva à esquerda em fill vermelho; à
direita Fechar → secundárias → primária âmbar (a primária é sempre a última, mais à
direita). **Em diálogo de confirmação a ordem inverte** — destrutiva à esquerda,
`Cancelar` à direita. Rótulos, foco e comportamento completos em `INTERACTIONS.md` §1 e §4.

### 4.2 Seletor de entidade

O componente mais reaproveitado do sistema (conta bancária, cliente, projeto, carteira —
qualquer coisa com identidade visual e agrupamento). Botão de 42px com:

1. **Marca da entidade** em quadrado 22px, raio 6px, `background:#FFFFFF` com
   `box-shadow: 0 0 0 1px rgba(0,0,0,0.12)` e a imagem 16px em `object-fit:contain`.
   O fundo branco vale nos dois temas — logo de terceiro não se adapta a tema.
2. **Nome** com ellipsis, 3. **qualificador** curto (moeda, tipo, código) em 11px/600
   `--text-faint`, 4. chevron duplo 14px.

Dropdown `--surface`, raio 10px, `--shadow-lg`, `max-height:320px`, com **grupos**
(rótulo 11px/600/uppercase/`--text-faint`, `cursor:default`, sem marca). Sem marca
disponível: quadrado `--surface-raised` com a inicial. **Nunca** a marca de outra
entidade como fallback.

### 4.3 Navegador de período

Grupo com borda, 38–42px, `‹ rótulo ›`, **largura mínima fixa no rótulo** para o grupo
não pular de tamanho ao mudar de mês:

- Mês: `min-width:170px` — "Setembro 2026"
- Ano: `min-width:72px` — "2026"
- Ciclo de fatura: `min-width:170px` — "Fatura · Set/26" + linha auxiliar com vencimento

Mês **e** ano são obrigatórios em qualquer visão temporal: só o mês é ambíguo em produto
que guarda anos de histórico. Quando o período é navegável, ofereça também um atalho
textual "hoje".

### 4.4 Badges de status

Pílula 11–11.5px/600, `padding:3px 10px`, par bg/texto de §2.3, **`nowrap`**.

| Papel | Quando |
|---|---|
| ok | estado terminal confirmado (concluído, pago, conciliado) |
| warn | requer ação humana (parcial, aguardando aprovação, divergência) |
| err | falha ou vencimento (erro, bloqueado, vencido) |
| info | vínculo, regra aplicada, referência |
| neutral | previsto, agendado, rascunho, não iniciado |

O mapa é único no produto: o mesmo estado tem o mesmo par de cor e o mesmo rótulo em toda
tela. **Nunca** exibir enum cru (`REALIZADO`, `PENDING`) — sempre pelo mapa de rótulos
em português.

### 4.5 Tabelas

- Card `--surface`, raio 12px, `overflow:hidden`; `<table>` dentro de
  `<div style="overflow-x:auto">`.
- **`table-layout:fixed` + `<colgroup>` com porcentagens.** Toda célula de texto:
  `overflow:hidden; text-overflow:ellipsis; white-space:nowrap`. `min-width` só quando
  inevitável — 520–560px é o normal; acima de 900px, corte coluna ou empilhe.
- Cabeçalho `--surface-raised`, rótulo 11px/600/uppercase/0.04em/`--text-faint`.
- Linha: `border-top: 1px solid --border`, `padding: 12px 16px`, hover `--row-hover`.
  **Sem zebra** — a borda já separa.
- Valor à direita, 13.5px/500–600, `--positive`/`--negative`/`--text`.
- Seleção de linha: `--accent-tint` + barra âmbar de 3px. Nunca pinta a linha inteira.
- Rodapé de tabela: contagem à esquerda, paginação à direita, ambos 12.5px.
- Sticky header obrigatório acima de 20 linhas.

### 4.6 Modal / lightbox — anatomia única

Todo registro clicado abre modal read-only; clicar em linha **nunca** navega para outra
tela. Uma anatomia só, em todo o produto:

1. **Overlay** `--overlay` + `backdrop-filter: blur(4px)`.
2. **Painel** `--surface`, raio 16px, `max-width` por tamanho (`sm` 420 · `md` 580 ·
   `lg` 780 · `xl` 1000), `max-height:86vh`, `overflow-y:auto`.
3. **Header sticky:** ícone 34px + título 16px/700 + subtítulo de tipo/contexto + badge
   de status; botão fechar 32px à direita.
4. **Corpo:** grade `repeat(auto-fit, minmax(200px,1fr))` de pares rótulo/valor
   (rótulo 11px/600/uppercase/`--text-faint`, valor 13.5px/500).
5. **Vínculos** como chips clicáveis em seção própria.
6. **`<details>` colapsados** para campos técnicos e para o **JSON bruto** da origem —
   `<pre>` em `--bg`, 11.5px, `max-height:280px`. Toda tela que consome dado de terceiro
   expõe o payload original: é o que torna o produto auditável.
7. **Rodapé sticky** com a ordem de botões de §4.1.
8. **Editar é in-place**, trocando o modo do próprio modal — nunca um segundo modal em
   cima do primeiro.

### 4.7 Chips, filtros e etapas

- **Chip de filtro:** pílula 34px, 12.5px/500. Selecionado = fundo `--surface`/`--bg` +
  **borda âmbar**; não selecionado = borda `--border` e opacidade 0.5–0.75.
  **Fundo âmbar preenchido nunca indica seleção.**
- **Segmented:** trilha `--bg` com borda, opção ativa em `--surface` peso 600.
- **Filtros de lista:** card raso com selects de 38px e uma busca local — distinta da
  busca global do topbar, e rotulada como "Buscar nesta lista".
- **Etapas (stepper):** pílulas com número em círculo 20px; concluída = `ok`, ativa =
  fill âmbar + borda âmbar + `--accent-tint`, futura = `neutral`; chevron entre elas.

### 4.8 Gráficos

Barras em `div` com `border-radius: 3–4px 3–4px 0 0`. Semântica de cor fixa:
**`--bar` neutro = contexto**, **verde = realizado/confirmado**, **âmbar = previsto/meta**.
Legenda sempre presente, 12px, com quadrado de 8px. Eixo com duas âncoras (início e fim),
11px `--text-faint`. Sem grade de fundo, sem eixo desenhado, sem biblioteca de chart para
barra simples.

### 4.9 Estados obrigatórios

Toda lista, tabela e card de dado tem os quatro, e eles fazem parte da entrega — não são
refinamento posterior:

- **Vazio:** ícone 44px em quadrado `--surface-raised`, título 14px/600, uma linha
  explicando **o próximo passo** e, quando existir, o botão que o executa.
- **Carregando:** skeleton — blocos `--surface-raised` com as alturas reais do conteúdo
  (não spinner, não "Carregando…").
- **Erro:** faixa `err` com o que falhou, quando, e um botão "Tentar novamente".
- **Sem permissão:** faixa `neutral` dizendo o que falta e quem concede.

E ainda: **offline** (faixa fixa no topo do conteúdo) e **toast** (canto inferior direito,
`--surface` + borda da semântica, título 13px/600 e corpo 12px em `--text`).

### 4.10 Cabeçalho de página

Primeiro elemento de toda tela logada, a 28px do topbar.

- **Esquerda:** `<h1>` (`--rb-size-h1`/700, `line-height: 1.2`, `letter-spacing:
  var(--rb-tracking-h1)`, margem 0). Subtítulo 4px abaixo, uma frase dizendo o que a
  tela resolve, 13px, `--text-muted`.
- **Direita:** ações de tela, com a primária por último e `nowrap`.
- **Linha:** `display:flex; flex-wrap:wrap; justify-content:space-between;
  align-items:flex-start; gap:12px`. No celular as ações descem pra linha de baixo.
- **Variante compacta:** quando a barra de contexto cabe numa linha, os controles dela
  (segmentado, período, seletor) entram na linha do título, sem subtítulo
  (`align-items:center; gap:8px 12px`). O FIN faz isso no Balancete e na DRE.
- **Variante com abas:** abas sublinhadas na linha do título, com `border-bottom` na
  linha toda. O FIN faz isso em Pendentes.
- Até o primeiro bloco: 16px (o `gap` do conteúdo).
- Não é um `<header>` (`<header>` é landmark; use `<div>`).

---

## 5. Padrões de produto

- **Formato brasileiro:** `R$ 1.234,56`, `US$ 1,234.56`, `DD/MM/AAAA`,
  CNPJ `XX.XXX.XXX/XXXX-XX`, CPF `XXX.XXX.XXX-XX`. Negativo com menos tipográfico (`−`).
- **Duas moedas, quando houver:** valor na moeda de origem + conversão em parênteses ou
  coluna adjacente, sempre com a taxa e a fonte visíveis no detalhe.
- **Combo nunca mostra enum cru.** Mapa de rótulos PT no código.
- **Popup do sistema, nunca `alert()`/`confirm()` nativo.**
- **Confirmação destrutiva** repete o nome do que será apagado.
- **Mobile (<768px):** sidebar → drawer; modal → bottom sheet; tabela → lista de cards com
  rótulo acima do valor. Alvo de toque mínimo 44px.

---

## 6. Proveniência (específico para trabalho com IA)

Quando uma tela é **proposta de design** e não recriação fiel de algo que já existe no
código, ela declara isso na própria tela: faixa `warn` discreta no fim do conteúdo, com
badge "proposta nova" e uma frase dizendo **o que veio do código real** (arquivo, tabela,
migration) e **o que é proposta**.

Parece excesso de zelo e não é: sem isso, protótipo gerado por IA é indistinguível de
documentação do que existe, e alguém constrói em cima de uma invenção.

---

## 7. Acessibilidade

- WCAG 2.1 AA é o piso, não a meta. **Todo** texto ≥ 4.5:1 — incluindo rótulo 11px,
  texto de badge e legenda de gráfico.
- Contraste já validado nos tokens. Se você precisar inventar uma cor, meça antes.
- Cor nunca é o único portador de significado: badge tem rótulo, gráfico tem legenda,
  status tem texto.
- `:focus-visible` âmbar em tudo que recebe teclado; `aria-label` em todo botão só-ícone;
  `<table>` real com `<thead>`/`<th>`.
- Nenhuma animação acima de 320ms; respeite `prefers-reduced-motion`.

---

## 8. Proibições

- Segunda família tipográfica — inclusive mono para valores.
- Peso acima de 700 ou abaixo de 400.
- Âmbar como fundo de página, card grande ou sidebar.
- Texto branco sobre fill âmbar.
- Sidebar clara no tema claro.
- Ícone + logo na mesma barra.
- Zebra em tabela, sombra em card, gradiente decorativo, glassmorphism.
- Bounce, elástico, animação acima de 320ms.
- Emoji em interface.
- Rolagem lateral em tabela que cabe.
- Enum cru na interface.
- Cor nova fora de `tokens.css`.

---

## 9. Checklist de entrega

Antes de abrir PR, passe a tela por isto:

- [ ] Dark **e** light conferidos na tela real, não só no token.
- [ ] Um único botão primário âmbar; âmbar visivelmente abaixo de 8% da área.
- [ ] Sidebar grafite nos dois temas; tooltip funcionando recolhida.
- [ ] Topbar só com a busca (se o produto tem) e o launcher do RumBee ID; tema, idioma,
      conta, Termos e Privacidade no menu do usuário.
- [ ] Sem tela de login própria; app logado sem rodapé; tela pública com rodapé legal.
- [ ] Nenhuma rolagem lateral em tabela que cabe na largura.
- [ ] Todo botão, badge e cabeçalho com `nowrap`.
- [ ] Os quatro estados da lista existem.
- [ ] Nenhum hex fora de `tokens.css`.
- [ ] Rótulo 11px lido confortavelmente nos dois temas.
- [ ] Título a 28px do topbar (20px no celular), à esquerda, com subtítulo; ações à
      direita; nada acima; sem hero.
- [ ] Nota de proveniência, se a tela é proposta.

---

## 10. Assets

```
rumbee-brand/
├── README.md      índice e regra de herança
├── BRAND.md       marca: conceito, símbolo, cor, voz
├── DESIGN.md      este arquivo — como uma coisa é
├── INTERACTIONS.md regras de interação — como uma coisa se comporta
├── META.md        head, títulos, description, favicons, manifest
├── AI-AGENT.md    instruções para agentes de IA
├── tokens.css     tokens em CSS custom properties (dark + light)
└── assets/
    ├── rumbee-logo-horizontal-light-text.png   fundo escuro
    ├── rumbee-logo-horizontal-dark-text.png    fundo claro
    ├── rumbee-icon-transparent.png             ícone isolado
    ├── rumbee-beeline-target.png               beeline até o alvo
    ├── rumbee-beeline-stripe.png               faixa listrada
    ├── favicon-32/48/192/512.png               favicons
    ├── apple-touch-icon.png                    180px, fundo grafite
    └── og-image.png                            1200×630 para compartilhamento
```

---

## 11. Changelog

- **1.2 · 2026-10-12** — Topbar passa a ter a busca global só quando o produto tem e
  ganha o launcher de apps do RumBee ID (§3.2); o toggle de tema sai do topbar e fica no
  menu do usuário, que ganha ordem fixa com idioma, Gerenciar conta, Termos e Privacidade
  (§3.1). Nova §3.4: login e conta pelo RumBee ID, URLs canônicas de termos e
  privacidade, app logado sem rodapé, rodapé legal nas telas públicas. O shell segue o
  do RumBee Link.
- **1.1 · 2026-10-12** — Cabeçalho de página vira componente (§4.10); overline opcional
  (§2.4); densidade vertical explícita (§3.3), com padding de celular. Grupo de navegação
  na sidebar (§3.1). `--rb-size-h1` cai de 26px para 24px, como no FIN; ritmo entre
  blocos continua 16px. Título de modal fica em 16px/700 (§2.4 dizia 600, §4.6 dizia 700).
  Tokens novos: `--focus-ring`, `--rb-size-label-field`, `--rb-tracking-h1` e
  `--chrome-border`. Contribuições do RumBee Link.
- **1.0 · 2026-09-16** — Primeira versão genérica, extraída do sistema do RumBee Fin
  (`DESIGN.md` v3.0 do projeto DocSales-Fin) e generalizada: o seletor de conta bancária
  virou seletor de entidade, o vocabulário financeiro saiu, e as decisões de contraste que
  custaram várias rodadas de revisão viraram regra escrita (`--text-faint` no piso AA,
  tint de mesma matiz, fill âmbar constante com tinta variável, tema claro não invertido).
