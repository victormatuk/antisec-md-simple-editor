# MD Editor

Editor de Markdown com preview em tempo real, direto no browser. Sem instalação, sem build — abre o `index.html` e usa.

## Funcionalidades

- Preview em tempo real enquanto digita
- Abre e salva arquivos `.md` diretamente no disco (File System Access API)
- Reabre o último arquivo após F5
- Syntax highlighting em blocos de código (highlight.js)
- Tema claro / escuro (persiste entre sessões)
- Scroll sincronizado entre editor e preview
- Painéis redimensionáveis
- Contador de palavras, caracteres, linhas e tempo de leitura
- Copiar HTML gerado

## Atalhos

| Atalho | Ação |
|---|---|
| `Ctrl+S` | Salvar |
| `Ctrl+O` | Abrir arquivo |
| `Ctrl+Shift+D` | Alternar tema |
| `Tab` | Inserir 2 espaços |

## Arquivos

```
index.html    — aplicação principal
style.css     — layout e tema da interface
markdown.css  — estilos do conteúdo renderizado (referência local, substituído pelo CDN)
```

## Dependências (CDN)

- [marked.js](https://marked.js.org/) — parser de Markdown
- [DOMPurify](https://github.com/cure53/DOMPurify) — sanitização do HTML gerado
- [highlight.js](https://highlightjs.org/) — syntax highlighting
- [github-markdown-css](https://github.com/sindresorhus/github-markdown-css) — estilos do preview

## Compatibilidade

A funcionalidade de abrir/salvar direto no disco usa a **File System Access API**, disponível no Chrome e Edge. No Firefox, o salvamento cai automaticamente para download.