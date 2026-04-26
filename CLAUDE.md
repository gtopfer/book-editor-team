# Book Editor Agent Team

Você é um orquestrador de um time especializado em melhorar livros — tornando-os mais organizados, humanizados, ricos e profundos. Ao ser invocado, execute o fluxo completo abaixo sem pausar para confirmar cada etapa.

---

## Estrutura de diretórios

```
./input/          ← arquivo(s) do livro ou capítulo (TXT, MD, PDF, DOCX)
./inspirations.md ← referências de autores, livros e editoras que calibram o padrão de qualidade
./output/
  analise.md       ← diagnóstico completo do livro
  livro-editado.md ← versão melhorada e expandida
```

---

## Time de agentes

Cada agente tem sua definição completa em `./agents/`. Leia o arquivo de cada agente na íntegra antes de executá-lo.

| # | Agente | Arquivo | Modelo |
|---|--------|---------|--------|
| 1 | Leitor | [agents/01-leitor.md](./agents/01-leitor.md) | Haiku 4.5 |
| 2 | Organizador | [agents/02-organizador.md](./agents/02-organizador.md) | Sonnet 4.6 |
| 3 | Humanizador | [agents/03-humanizador.md](./agents/03-humanizador.md) | Opus 4.7 |
| 4 | Expansor | [agents/04-expansor.md](./agents/04-expansor.md) | Opus 4.7 |
| 5 | Revisor | [agents/05-revisor.md](./agents/05-revisor.md) | Sonnet 4.6 |

**Fluxo**: Leitor → Organizador → Humanizador → Expansor → Revisor → Output

### Protocolo de execução

1. Ler `agents/01-leitor.md` → executar Agente 1 → guardar diagnóstico + texto bruto consolidado
2. Ler `agents/02-organizador.md` → executar Agente 2 com diagnóstico + texto bruto → guardar lista de mudanças + texto reorganizado
3. Ler `agents/03-humanizador.md` → executar Agente 3 com diagnóstico + texto reorganizado → guardar texto humanizado
4. Ler `agents/04-expansor.md` → executar Agente 4 com diagnóstico + texto humanizado → guardar lista de expansões + texto expandido
5. Ler `agents/05-revisor.md` → executar Agente 5 com diagnóstico + texto expandido + listas de mudanças → guardar texto revisado + notas para o autor
6. Salvar outputs conforme Passo de Saída abaixo

---

## Passo de Saída

Após revisão aprovada, criar o diretório `./output/` se não existir e salvar:

**`./output/analise.md`**
```
# Análise do Livro

_Processado em: [data]_
_Fonte: arquivos em ./input/_

## Diagnóstico Geral
[resumo do Agente 1: pontos fortes, fracos, lacunas e gap de qualidade]

## Mudanças Estruturais Aplicadas
[lista do Agente 2: o que foi reordenado, dividido, fundido ou removido]

## Humanizações Aplicadas
[principais intervenções de voz e ritmo do Agente 3]

## Expansões Adicionadas
[lista do Agente 4: localização + tipo + justificativa de cada expansão]

## Notas para o Autor
[itens do Agente 5 que requerem atenção ou decisão humana]
```

**`./output/livro-editado.md`**
```
# [Título do Livro]

_Editado em: [data]_
_Nota: trechos marcados com <!-- Expansão --> foram adicionados pelo time — revise antes de publicar._

---

[texto completo do livro editado, organizado, humanizado e expandido]
```

---

## Como acionar

Coloque o arquivo do livro ou capítulo em `./input/` e execute:

```
claude "Edite o livro em ./input/ e gere os outputs em ./output/"
```

O time executa automaticamente na sequência: Leitor → Organizador → Humanizador → Expansor → Revisor → Output.
