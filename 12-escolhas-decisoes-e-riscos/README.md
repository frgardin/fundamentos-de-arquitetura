# 12 — Escolhas, Decisões e Riscos

Arquitetura é uma sequência de decisões tomadas sob incerteza. Esta aula trata de como decidir com critério, registrar o raciocínio e administrar os riscos que ficam no caminho.

## Objetivos de aprendizagem

- Estruturar decisões arquiteturais com critérios explícitos.
- Documentar decisões usando ADRs.
- Identificar, analisar e mitigar riscos arquiteturais.
- Reconhecer o momento adequado de decidir e de revisar.

## Decisão arquitetural

Uma **decisão arquitetural** é uma escolha estrutural que restringe o espaço de soluções futuras. Exemplos:

- adotar um banco relacional único ou um banco por serviço;
- usar comunicação síncrona ou assíncrona;
- organizar o sistema em um monólito modular ou em serviços;
- permitir que o frontend acesse o banco diretamente.

Nem toda decisão precisa de registro formal. O critério é o **impacto**: decisões caras de reverter, que afetam muitas equipes ou características importantes, merecem documentação.

## Como decidir

### 1. Enquadrar o problema

Descreva o problema, as restrições e as características prioritárias. Decisões sem contexto viram preferência pessoal.

### 2. Levantar alternativas

Inclua sempre a opção **"não fazer nada"** ou **"manter o que existe"**. Duas alternativas é o mínimo; três permitem comparar trade-offs.

### 3. Definir critérios

Critérios devem ser explícitos e, quando possível, mensuráveis:

- atende às características prioritárias?
- qual o custo de implementação e operação?
- qual o impacto na equipe?
- qual o custo de reversão?
- qual o risco associado?

### 4. Comparar

Use uma **matriz de decisão ponderada**:

| Critério | Peso | Alternativa A | Alternativa B | Alternativa C |
|---|---|---|---|---|
| Escalabilidade | 3 | 2 | 3 | 3 |
| Simplicidade | 2 | 3 | 1 | 2 |
| Custo de operação | 2 | 3 | 1 | 2 |
| **Total** | | **17** | **14** | **17** |

A matriz organiza a discussão. O número final é menos importante do que as notas atribuídas e as premissas por trás delas.

### 5. Decidir e registrar

Registre a decisão, as alternativas descartadas e as consequências esperadas.

## ADR — Architecture Decision Record

Um ADR é um documento curto que captura uma decisão e seu contexto. Um formato comum:

```markdown
# ADR 001 — Adotar monólito modular no MVP

## Status
Aceito

## Contexto
O produto está em descoberta, a equipe tem cinco pessoas e o domínio
ainda muda com frequência. A operação não possui cultura de
observabilidade distribuída.

## Decisão
Vamos construir um monólito modular, com fronteiras de domínio
explícitas e um único pipeline de deploy.

## Consequências
- Positivas: menor custo operacional, transações simples, deploy rápido.
- Negativas: escala acoplada; extração futura de serviços exigirá
  investimento nas fronteiras.
- Revisão: reavaliar quando houver necessidade comprovada de escala
  independente ou times autônomos.
```

ADRs ficam versionados junto com o código, normalmente em `docs/adr/`. Eles formam um histórico das decisões e evitam que o conhecimento se perca.

## Análise de riscos

Risco é a possibilidade de um evento indesejado afetar objetivos. Em arquitetura, os riscos mais comuns são:

- **técnicos:** desempenho insuficiente, integração instável, dívida técnica;
- **de negócio:** requisitos que mudam, regulação, concorrência;
- **de projeto:** prazo, orçamento, equipe, dependências externas;
- **operacionais:** falhas de infraestrutura, segurança, capacidade.

### Risk storming

Técnica colaborativa para identificar riscos:

1. Reúna a equipe e especialistas.
2. Identifique os riscos individualmente (sem influência do grupo).
3. Compartilhe e agrupe os riscos.
4. Avalie **probabilidade** e **impacto**.
5. Defina mitigações e responsáveis.

### Matriz de risco

| Probabilidade \ Impacto | Baixo | Médio | Alto |
|---|---|---|---|
| **Alta** | Monitorar | Mitigar | Evitar |
| **Média** | Aceitar | Mitigar | Mitigar |
| **Baixa** | Aceitar | Monitorar | Transferir/planejar |

### Mitigação

- **protótipos e spikes:** validar hipóteses técnicas antes de comprometer a arquitetura;
- **fitness functions:** detectar degradação cedo;
- **testes de carga e caos:** exercitar cenários adversos;
- **planos de contingência:** definir o que fazer se o risco se materializar;
- **decisões reversíveis:** preferir opções que possam ser desfeitas.

## Reversibilidade e timing

- **Decisões reversíveis** (two-way doors) podem ser tomadas rápido e corrigidas depois.
- **Decisões irreversíveis** (one-way doors) exigem mais análise e documentação.
- **Last responsible moment:** adie a decisão até o ponto em que não decidir passe a custar mais do que decidir. Adiar não é procrastinar; é preservar opções enquanto se coleta informação.

## Dívida técnica

Dívida técnica é o custo futuro de uma solução rápida escolhida hoje. Nem toda dívida é ruim: às vezes é racional sacrificar qualidade para validar um mercado. O problema é a dívida **inconsciente**, não registrada e sem plano de pagamento.

Boas práticas:

- registrar a dívida e o motivo;
- estimar o impacto;
- reservar tempo para pagá-la;
- evitar que ela se acumule em áreas críticas.

## Trade-offs e armadilhas

- **Decisão sem contexto:** "vamos usar Kafka porque é escalável".
- **Análise infinita:** buscar certeza absoluta antes de decidir.
- **ADR como burocracia:** documentos longos que ninguém lê.
- **Risco ignorado:** não registrar o que pode dar errado.
- **Dívida invisível:** atalhos que ninguém sabe que existem.
- **Decidir cedo demais:** comprometer a arquitetura antes de entender o problema.

## Perguntas para revisão

1. O que torna uma decisão "arquitetural"?
2. Quais são as partes de um ADR?
3. Como uma matriz de decisão ajuda a comparar alternativas?
4. O que é o last responsible moment?
5. Como diferenciar dívida técnica saudável de dívida perigosa?

## Para ir além

- RICHARDS, Mark; FORD, Neal. *Fundamentos de Arquitetura de Software*. Cap. 18 a 20.
- NYGARD, Michael. *Release It!* — riscos de produção e padrões de estabilidade.
- ADR GitHub org — adr.github.io.
- FOWLER, Martin. "TechnicalDebt" e "ArchitectureDecisionRecord". martinfowler.com.
