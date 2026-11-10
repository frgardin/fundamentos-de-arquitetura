# AGENTS.md — Regras do repositório

Repositório de anotações do curso de **Arquitetura de Sistemas** (Anhanguera). Cada `aula` é uma pasta numerada com dois arquivos: `README.md` (conteúdo de referência) e `anotacoes.md` (notas pessoais do estudante).

## Idioma

- Escreva em **português do Brasil**, com acentuação correta.
- Mantenha termos técnicos consagrados em inglês (ex.: *trade-off*, *fitness function*, *bounded context*, *pipeline*), sem traduções forçadas.
- Use a mesma grafia dos títulos das aulas em todo o repositório.

## Estrutura

- Pastas de aula seguem o padrão `NN-nome-em-kebab-case`, com dois dígitos (`01` a `13`).
- A ordem numérica é o cronograma do curso: **nunca renumere nem reordene** pastas existentes.
- Cada aula contém exatamente `README.md` e `anotacoes.md`.
- Arquivos e links internos usam caminhos relativos e kebab-case.

## Conteúdo dos READMEs de aula

Todo README de aula deve ter, nesta ordem:

1. título `NN — Nome da aula`;
2. um parágrafo de abertura explicando o tema;
3. `## Objetivos de aprendizagem` em lista;
4. seções de conteúdo com os conceitos da aula;
5. `## Trade-offs e armadilhas` (ou seção equivalente, quando fizer sentido);
6. `## Perguntas para revisão`;
7. `## Para ir além` com referências e capítulos.

O README explica o tema; ele não é um resumo pessoal. Exemplos e opiniões do estudante vão para `anotacoes.md`.

## Anotações

- `anotacoes.md` pertence ao estudante: **preserve o conteúdo existente** ao editar.
- Prefira acrescentar seções ou preencher lacunas a reescrever anotações.
- Não mova anotações de uma aula para outra sem pedido explícito.

## Ao adicionar ou alterar uma aula

1. Crie a pasta com o próximo número disponível.
2. Crie `README.md` e `anotacoes.md` seguindo o padrão acima.
3. Atualize a tabela **Estrutura das aulas** e a lista de progresso no `README.md` raiz.
4. Verifique se os links relativos funcionam.

## Commits

- Mensagens em português, no padrão Conventional Commits: `docs: adiciona aula 07`, `fix: corrige link da aula 03`.
- Um commit por mudança coerente; não misture conteúdo de aulas diferentes.

## Estilo de escrita

- Prefira frases curtas e voz ativa.
- Explique o conceito antes de citar ferramentas.
- Apresente estilos e decisões como trade-offs, não como recomendações absolutas.
- Use tabelas para comparações e listas para critérios.
