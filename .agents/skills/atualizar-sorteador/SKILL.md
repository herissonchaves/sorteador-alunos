---
name: atualizar-sorteador
description: >
  Modifica, corrige ou adiciona funcionalidades ao arquivo HTML do Sorteador de Turmas.
  Use esta skill quando o usuário quiser: adicionar uma nova página ou função ao app,
  corrigir um bug visual ou de comportamento, alterar o design ou cores, melhorar a
  acessibilidade, otimizar o código JavaScript, adicionar exportação de dados, refatorar
  trechos do código, ou qualquer outra modificação no arquivo "sorteador de alunos.html".
  Também ative quando o usuário disser "muda o app", "adiciona uma funcionalidade",
  "corrige o sorteador", "quero que o app faça X", "tá com bug na roleta/equipes/CSV",
  "melhora o visual", "refatora o código", "adiciona animação" ou similar.
---

# Skill: atualizar-sorteador

## Objetivo

Modificar o arquivo `sorteador de alunos.html` de forma segura, preservando o funcionamento
offline, o padrão visual e a estrutura SPA do app.

## Entradas esperadas

- Descrição da modificação desejada (texto livre do usuário)
- Opcionalmente: screenshot, descrição do bug a corrigir, ou trecho de código de referência

## Saída esperada

- O arquivo `sorteador de alunos.html` atualizado, na raiz do projeto
- Breve resumo das mudanças feitas (o que foi alterado e por quê)

## Passo a passo

1. **Ler o arquivo** `sorteador de alunos.html` completo para entender a estrutura atual
2. **Mapear o impacto** da mudança solicitada:
   - Quais seções do HTML/CSS/JS são afetadas?
   - A mudança interfere na navegação SPA (`navigate()`)?
   - Alguma variável ou função existente precisa ser alterada?
3. **Planejar a edição** antes de escrever qualquer código:
   - Identificar exatamente onde inserir ou modificar o trecho
   - Garantir que não há colisão de IDs, nomes de função ou variáveis CSS
4. **Aplicar a modificação** no arquivo, respeitando todas as regras globais do `AGENT.md`
5. **Verificar consistência:**
   - O arquivo ainda é auto-contido (sem dependências externas além de Google Fonts)?
   - Todos os `id` referenciados no JS existem no HTML?
   - A navegação entre páginas continua funcionando?
   - Nenhuma funcionalidade existente foi removida sem intenção?
6. **Resumir as alterações** feitas para o usuário de forma clara e objetiva

## Árvore de decisão para novos recursos

```
O recurso precisa de uma nova "página" no SPA?
├── SIM → Criar div#page-<nome> + botão no menu home + case no navigate()
└── NÃO → Adicionar dentro da página mais adequada existente

O recurso lê/grava dados persistentes?
├── SIM → Usar as funções loadData() e saveData() existentes via localStorage
└── NÃO → Usar variáveis em memória (let/const no escopo adequado)

O recurso tem animação ou transição?
└── Usar a variável CSS --transition ou @keyframes fadeIn já existente no arquivo
```

## Regras e restrições

- **Não separar em múltiplos arquivos.** CSS, JS e HTML devem permanecer no mesmo `.html`.
- **Não remover funcionalidades existentes** sem confirmação explícita do usuário.
- **Manter a paleta de cores** (`--primary: #6C5CE7`, `--secondary: #00CEC9`, etc.) salvo pedido contrário.
- **Manter a fonte Nunito** (já carregada via Google Fonts no `<head>`).
- **Preservar o padrão de navegação SPA:** novas páginas devem ter `id="page-<nome>"` e usar `navigate('<nome>')`.
- **Não usar `localStorage` para dados sensíveis** — apenas turmas, alunos e configurações do app.
- **Comentar blocos novos** com `// --- <DESCRIÇÃO> ---` para facilitar manutenção futura.
- **Responsividade:** qualquer elemento novo deve ter breakpoint para mobile (`max-width: 600px`).

## Checklist pré-entrega

- [ ] O arquivo abre corretamente no navegador sem servidor?
- [ ] Todas as páginas do menu estão acessíveis via navegação?
- [ ] O app funciona em mobile (testado mentalmente em 375px de largura)?
- [ ] Nenhuma função ou ID existente foi removido sem intenção?
- [ ] O código novo está comentado com `// --- <DESCRIÇÃO> ---`?
- [ ] O arquivo permanece auto-contido (sem novas dependências externas desnecessárias)?
