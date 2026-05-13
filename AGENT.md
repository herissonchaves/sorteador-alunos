# Sorteador de Alunos

## Papel do agente

Agente especializado na manutenção e evolução do **Sorteador de Turmas** — uma aplicação web 100% offline
para professores sortearem equipes e realizarem roletas com seus alunos.

## Contexto do projeto

O Sorteador de Turmas é um único arquivo HTML auto-contido (`sorteador de alunos.html`) que roda
diretamente no navegador, sem servidor, sem instalação. Professores importam listas de alunos via CSV,
gerenciam turmas, sorteiam equipes aleatórias e usam uma roleta animada para escolher alunos
individualmente. Os dados ficam salvos no `localStorage` do navegador.

## Regras globais

- **Nunca quebrar o funcionamento offline** — o app não pode depender de APIs externas ou servidores.
- **Preservar o padrão visual** — paleta de cores (`--primary: #6C5CE7`), fonte Nunito, estilo SPA com navegação por `navigate()`.
- **Manter tudo em arquivo único** — CSS, JS e HTML devem permanecer no mesmo `.html`; não criar arquivos separados.
- **Em caso de erro no código:** avisar o usuário com descrição clara do problema e onde ele ocorre.
- **Idioma:** sempre responder e comentar em português (pt-BR).

## Estrutura de pastas

```
Sorteador-alunos/
├── AGENT.md                          ← instrução principal do agente
├── sorteador de alunos.html          ← aplicação web principal (único arquivo do app)
└── .agents/
    └── skills/
        ├── atualizar-sorteador/      ← modifica/evolui o HTML
        │   └── SKILL.md
        └── gerar-csv-alunos/         ← cria CSVs no formato correto para importação
            └── SKILL.md
```

## Formato do CSV de entrada

Cada linha do CSV deve seguir o padrão:

```
nome, sexo, turma
```

Exemplo:

```csv
Ana Souza, F, 1A
Bruno Lima, M, 1A
Carla Mendes, F, 2B
```

- **nome**: nome completo do aluno
- **sexo**: `M` (masculino) ou `F` (feminino)
- **turma**: código da turma (ex: `1A`, `2B`, `3C`)

## Skills disponíveis

| Skill | Quando usar |
|-------|-------------|
| `atualizar-sorteador` | Modificar, corrigir ou adicionar funcionalidades ao HTML do app |
| `gerar-csv-alunos` | Criar arquivos CSV de alunos prontos para importação no app |
