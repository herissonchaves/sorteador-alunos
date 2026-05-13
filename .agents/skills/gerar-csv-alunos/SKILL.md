---
name: gerar-csv-alunos
description: >
  Gera arquivos CSV de alunos no formato correto para importação no Sorteador de Turmas.
  Use esta skill quando o usuário quiser: criar uma lista de alunos para uma turma,
  gerar um CSV de exemplo, converter uma lista colada no chat para arquivo CSV,
  ou preparar dados de alunos para importar no app. Ative também quando o usuário disser
  "cria um CSV da turma X", "faz a lista dos alunos", "quero importar essa lista no sorteador",
  "converte essa lista para CSV", "gera o arquivo de alunos", ou similar.
---

# Skill: gerar-csv-alunos

## Objetivo

Criar arquivos `.csv` de alunos no formato aceito pelo Sorteador de Turmas, prontos para
upload direto na tela de "Cadastrar Turmas" do app.

## Formato obrigatório do CSV

Cada linha deve seguir exatamente:

```
nome completo, sexo, turma
```

- **nome**: nome completo do aluno (sem abreviações)
- **sexo**: `M` para masculino ou `F` para feminino (maiúsculas)
- **turma**: código da turma (ex: `1A`, `2B`, `3C`, `EF9A`)
- **Sem cabeçalho** — o app lê a partir da primeira linha
- **Separador**: vírgula seguida de espaço (`, `)

Exemplo válido:
```csv
Ana Souza, F, 1A
Bruno Lima, M, 1A
Carla Mendes, F, 2B
Daniel Rocha, M, 2B
```

## Entradas esperadas

- Lista de nomes colada no chat (formato livre), **ou**
- Descrição da turma (ex: "cria 30 alunos fictícios para a turma 3B"), **ou**
- Arquivo de texto/planilha com dados já existentes

## Saída esperada

- Arquivo `.csv` salvo na **raiz do projeto** com nome no padrão `<turma>-alunos.csv`
- Exemplo: `1A-alunos.csv`, `3B-alunos.csv`
- Se houver múltiplas turmas, gerar um arquivo por turma

## Passo a passo

1. **Identificar a fonte dos dados:**
   - Lista colada no chat → processar e formatar
   - Descrição ("cria 30 alunos fictícios") → gerar nomes realistas em pt-BR
   - Arquivo enviado → ler e converter para o formato correto
2. **Normalizar os dados:**
   - Capitalizar nomes corretamente (ex: `ANA SOUZA` → `Ana Souza`)
   - Verificar se o campo sexo é `M` ou `F`; se ambíguo, perguntar ao usuário
   - Verificar se o código da turma segue o padrão alfanumérico simples
3. **Montar o CSV** sem cabeçalho, separado por `, `
4. **Salvar na raiz do projeto** com o nome `<turma>-alunos.csv`
5. **Confirmar para o usuário:** número de alunos gerados, nome do arquivo e localização

## Regras e restrições

- **Nunca incluir linha de cabeçalho** — o app não suporta e vai cadastrar "Nome, Sexo, Turma" como aluno.
- **Nomes em pt-BR** quando gerados ficticiamente — usar nomes brasileiros comuns.
- **Sexo apenas M ou F** — não usar "Masculino", "Feminino", "X", etc.
- **Uma turma por arquivo** — não misturar turmas diferentes no mesmo CSV (o app aceita, mas dificulta gestão).
- **Encoding UTF-8** — garantir que caracteres acentuados (ã, ç, é) sejam preservados.
- **Sem linhas em branco** no meio do arquivo — o app pode interpretar como erro.

## Checklist pré-entrega

- [ ] Nenhum cabeçalho na primeira linha?
- [ ] Todos os campos `sexo` são `M` ou `F`?
- [ ] Nomes estão capitalizados corretamente?
- [ ] Arquivo salvo na raiz do projeto com nome no padrão `<turma>-alunos.csv`?
- [ ] Encoding é UTF-8?
- [ ] Sem linhas em branco no meio do arquivo?
