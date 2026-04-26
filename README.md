# Book Editor Agent Team

Um time de 5 agentes especializados que transforma manuscritos brutos em versões organizadas, humanizadas e aprofundadas — preservando a voz do autor.

## Como funciona

O orquestrador (Claude Code) executa os agentes em sequência, passando o trabalho de um para o próximo:

```
Leitor → Organizador → Humanizador → Expansor → Revisor → Output
```

Cada agente tem uma responsabilidade clara e não ultrapassa sua fronteira:

| # | Agente | Responsabilidade | Modelo |
|---|--------|-----------------|--------|
| 1 | **Leitor** | Diagnostica o manuscrito, extrai voz do autor, identifica lacunas | Haiku 4.5 |
| 2 | **Organizador** | Reorganiza estrutura e sequência lógica — sem gerar conteúdo novo | Sonnet 4.6 |
| 3 | **Humanizador** | Reescreve forma (ritmo, clareza, voz) — sem alterar conteúdo | Opus 4.7 |
| 4 | **Expansor** | Aprofunda lacunas com exemplos, contexto e perspectivas | Opus 4.7 |
| 5 | **Revisor** | Audita qualidade, corrige falhas, lista itens para o autor | Sonnet 4.6 |

## Pré-requisitos

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) instalado e autenticado

## Início rápido

**1. Clone o repositório**

```bash
git clone <repo-url>
cd book-editor-team
```

**2. Adicione o manuscrito**

```bash
cp meu-livro.md ./input/
```

Formatos suportados: `.txt`, `.md`, `.pdf`, `.docx`

**3. (Opcional) Configure as referências de qualidade**

Edite `./inspirations.md` adicionando os autores, livros e editoras que definem o padrão que o livro deve atingir. Quanto mais específico, melhor o resultado.

**4. Execute**

```bash
claude "Edite o livro em ./input/ e gere os outputs em ./output/"
```

Os resultados são salvos automaticamente em `./output/`.

## Estrutura do projeto

```
book-editor-team/
├── agents/
│   ├── 01-leitor.md        ← diagnóstica o manuscrito
│   ├── 02-organizador.md   ← reorganiza estrutura
│   ├── 03-humanizador.md   ← melhora voz e ritmo
│   ├── 04-expansor.md      ← aprofunda o conteúdo
│   └── 05-revisor.md       ← garante qualidade final
├── input/                  ← coloque o manuscrito aqui (não versionado)
├── output/                 ← outputs gerados (não versionados)
│   ├── analise.md
│   └── livro-editado.md
├── inspirations.md         ← referências de qualidade alvo
├── CLAUDE.md               ← instruções do orquestrador
└── README.md
```

## Personalizando o padrão de qualidade

O arquivo `./inspirations.md` calibra o nível de qualidade do time. Sem ele os agentes funcionam, mas sem régua de referência externa.

Exemplo de preenchimento:

```markdown
## Autores de referência
### Estilo de escrita / voz
- Richard Feynman — explica o complexo com analogias cotidianas, nunca perde o leitor

### Narrativa e ritmo
- Malcolm Gladwell — abre capítulos com histórias concretas antes de chegar à tese

## Livros de referência
### Profundidade e exemplos
- "The Pragmatic Programmer" — cada princípio tem um exemplo concreto aplicável

## Editoras de referência
- O'Reilly — clareza técnica, exemplos práticos, estrutura de capítulo consistente
```

## Outputs gerados

### `./output/analise.md`

Diagnóstico completo com:
- Pontos fortes, fracos e lacunas (Agente 1)
- Lista de mudanças estruturais aplicadas (Agente 2)
- Principais intervenções de voz e ritmo (Agente 3)
- Lista de expansões com justificativas (Agente 4)
- Notas para o autor com itens que requerem decisão humana (Agente 5)

### `./output/livro-editado.md`

Texto completo editado. Trechos adicionados pelo Expansor são marcados para fácil revisão:

```html
<!-- Expansão: exemplo -->
Aqui vai o trecho adicionado pelo time.
<!-- /Expansão -->
```

Tipos de marcador: `exemplo`, `contexto`, `contraponto`, `implicação`, `mini-história`, `lacuna`.

Revise esses trechos antes de publicar — o time sinalizou, a decisão final é sua.

## Modelos utilizados

| Agente | Modelo | Motivo |
|--------|--------|--------|
| Leitor | `claude-haiku-4-5` | Rápido e econômico para leitura e diagnóstico |
| Organizador | `claude-sonnet-4-6` | Bom raciocínio estrutural, custo equilibrado |
| Humanizador | `claude-opus-4-7` | Maior sensibilidade para voz, ritmo e nuance |
| Expansor | `claude-opus-4-7` | Melhor capacidade de geração de conteúdo coeso |
| Revisor | `claude-sonnet-4-6` | Bom para auditoria e crítica sem excesso de geração |
