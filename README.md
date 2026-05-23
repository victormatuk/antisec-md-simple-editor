# MD Editor

Editor de Markdown com preview em tempo real, direto no browser. Sem instalação, sem build — abre o `index.html` e usa.

## Funcionalidades

- Preview em tempo real enquanto digita
- Abre e salva arquivos `.md` diretamente no disco (File System Access API)
- Reabre o último arquivo após F5
- Barra de formatação completa: cabeçalhos H1–H6, negrito, itálico, tachado, código inline, citação, listas (com e sem ordem, tarefas), link, imagem, menção, referência (issue/PR), tabela, linha horizontal, sub/sobrescrito, destaque (`<mark>`), sublinhado (`<ins>`), tecla (`<kbd>`), abreviação (`<abbr>`) e bloco recolhível (`<details>`)
- Bloco de código com seletor de linguagem
- Syntax highlighting em blocos de código (highlight.js)
- Tema claro / escuro (persiste entre sessões)
- Scroll sincronizado entre editor e preview
- Painéis redimensionáveis
- Contador de palavras, caracteres, linhas e tempo de leitura
- Copiar HTML gerado
- Notificações agendadas via `@notify(...)` (lembretes nativos do Chrome)

## Notificações `@notify(...)`

Você pode incluir lembretes diretamente no markdown. Ao salvar o arquivo (Ctrl+S), o editor agenda uma notificação nativa do navegador para cada `@notify(...)` válido. Os agendamentos sobrevivem a recarregar a página (são persistidos no IndexedDB).

Sintaxe: `@notify(QUANDO, TEXTO)`

`QUANDO` aceita duas formas:

**Duração relativa** — combinação de tokens com as unidades curtas `s` (segundos), `m` (minutos), `h` (horas):

| Exemplo | Significado |
|---|---|
| `@notify(30s, Verificar o forno)` | 30 segundos |
| `@notify(30m, Tomar água)` | 30 minutos |
| `@notify(2h, Almoço)` | 2 horas |
| `@notify(1h30, Voltar para a reunião)` | 1h30min (número solto depois de `h` = minutos) |
| `@notify(2h30m, Reunião)` | 2h e 30min |
| `@notify(2h30m40s, Reunião curta)` | 2h, 30min e 40s |

**Timestamp absoluto** — `YYYYMMDD HH:MM` (segundos opcionais):

| Exemplo | Significado |
|---|---|
| `@notify(20260522 21:07, Sair)` | dispara em 22/05/2026 às 21:07 |
| `@notify(20260522 21:07:20, Sair)` | precisão em segundos |

Formas longas como `30min`, `30sec` ou `1hour` **não** são aceitas — aparecem em vermelho no preview e não são agendadas. Timestamps no passado também são ignorados.

Quando salvo, o badge no preview ganha cor de destaque (`⏰ spec · texto`) e aparece um aviso curto `✓ N lembrete(s) agendado(s)`. Notificações idênticas (mesmo `QUANDO` + mesmo `TEXTO`) só agendam uma vez; basta variar o texto para criar várias.

Requisitos: a Notification API precisa de contexto seguro — funciona via `localhost` (use `python3 serve.py`) ou HTTPS. O navegador pedirá permissão na primeira vez.

## Atalhos

| Atalho | Ação |
|---|---|
| `Ctrl+S` | Salvar |
| `Ctrl+O` | Abrir arquivo |
| `Ctrl+B` | Negrito |
| `Ctrl+I` | Itálico |
| `Ctrl+E` | Código inline |
| `Ctrl+K` | Link |
| `Ctrl+Shift+D` | Alternar tema |
| `Tab` | Inserir 2 espaços |

## Arquivos

```
index.html    — aplicação principal
style.css     — layout e tema da interface
```

## Dependências (CDN)

- [marked.js](https://marked.js.org/) — parser de Markdown
- [DOMPurify](https://github.com/cure53/DOMPurify) — sanitização do HTML gerado
- [highlight.js](https://highlightjs.org/) — syntax highlighting
- [github-markdown-css](https://github.com/sindresorhus/github-markdown-css) — estilos do preview

## Compatibilidade

A funcionalidade de abrir/salvar direto no disco usa a **File System Access API**, disponível no Chrome e Edge. No Firefox, o salvamento cai automaticamente para download.