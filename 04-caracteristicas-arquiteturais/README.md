# 04 — Características Arquiteturais

Requisitos funcionais dizem o que o sistema faz; características arquiteturais dizem **quão bem** ele precisa fazer. Esta aula ensina a identificar, priorizar e medir esses atributos de qualidade.

## Objetivos de aprendizagem

- Definir características arquiteturais e diferenciá-las de requisitos funcionais.
- Classificar características em operacionais, estruturais e transversais.
- Identificar características a partir de requisitos e stakeholders.
- Usar fitness functions para governar características ao longo do tempo.

## O que são características arquiteturais

São **critérios de sucesso independentes do domínio** que definem como o sistema deve se comportar. Elas não dizem "o sistema deve cadastrar clientes"; dizem "o sistema deve responder em menos de 200 ms" ou "deve continuar disponível se um data center falhar".

Características arquiteturais também são chamadas de **atributos de qualidade**, **requisitos não funcionais** ou, informalmente, *ilities*.

## Classificação

### Operacionais

Relacionadas à execução em produção:

- disponibilidade, confiabilidade, resiliência;
- escalabilidade, elasticidade, performance;
- recuperação de desastres, tolerância a falhas;
- segurança, monitoramento, observabilidade.

### Estruturais

Relacionadas à organização interna do código:

- modularidade, manutenibilidade, testabilidade;
- reusabilidade, extensibilidade, portabilidade;
- facilidade de deploy, facilidade de configuração.

### Transversais

Atravessam domínio e operação:

- acessibilidade, usabilidade, internacionalização;
- autenticação e autorização;
- privacidade, conformidade legal, auditabilidade.

## Identificando características

Características raramente vêm prontas no documento de requisitos. Elas precisam ser extraídas de:

- **requisitos de negócio:** "precisamos lançar promoções em minutos" sugere extensibilidade e deploy independente;
- **stakeholders:** jurídico pede auditabilidade; operação pede observabilidade;
- **domínio:** um sistema de apostas precisa de baixa latência e consistência; um catálogo precisa de disponibilidade e cache;
- **restrições:** orçamento, equipe, prazo e regulação limitam o que é viável.

Evite a lista infinita de qualidades. Priorize de **3 a 5 características** que realmente diferenciam o sistema. Se tudo é importante, nada é.

## Características explícitas e implícitas

- **Explícitas:** aparecem em requisitos ou decisões documentadas.
- **Implícitas:** são esperadas sem serem ditas (ex.: um sistema web deve ser razoavelmente usável).

O risco está nas implícitas: se ninguém as declarou, ninguém as projetou nem as testou.

## Fitness functions

Uma **fitness function** é um teste ou métrica automatizada que verifica se a arquitetura continua atendendo a uma característica. Exemplos:

- teste de tempo de resposta que falha o build acima de 200 ms;
- análise de dependências que falha se um módulo de domínio importar um framework;
- teste de caos que derruba uma instância e verifica a disponibilidade;
- verificação de cobertura de logs estruturados.

Sem fitness functions, características degradam silenciosamente. Com elas, a arquitetura se torna verificável e evolutiva.

## Características e trade-offs

Características competem entre si:

| Ganho | Custo típico |
|---|---|
| Escalabilidade | Complexidade operacional e de dados |
| Segurança forte | Latência e fricção de uso |
| Consistência | Disponibilidade e desempenho |
| Reusabilidade | Acoplamento e generalização prematura |
| Alta performance | Custo de infraestrutura e complexidade de código |

O arquiteto precisa declarar quais características são prioritárias e quais sacrifícios são aceitáveis. Essa priorização guia a escolha do estilo arquitetural.

## Trade-offs e armadilhas

- **Lista de desejos:** tentar atender a todas as características ao mesmo tempo.
- **Métrica sem contexto:** "99,99% de disponibilidade" sem discutir custo e impacto de negócio.
- **Característica sem teste:** declarar resiliência e nunca exercitá-la.
- **Confundir performance com escalabilidade:** performance é o tempo de uma operação; escalabilidade é a capacidade de crescer com carga.
- **Ignorar características do domínio:** algumas qualidades vêm do negócio, não da infraestrutura.

## Perguntas para revisão

1. Qual a diferença entre requisito funcional e característica arquitetural?
2. Dê exemplos de características operacionais, estruturais e transversais.
3. Como priorizar características quando todas parecem importantes?
4. O que é uma fitness function e por que ela é útil?
5. Que características você priorizaria em um sistema de pagamentos? E em um blog?

## Para ir além

- RICHARDS, Mark; FORD, Neal. *Fundamentos de Arquitetura de Software*. Cap. 4 a 7.
- BASS, Len; CLEMENTS, Paul; KAZMAN, Rick. *Software Architecture in Practice*. Parte II.
- FOWLER, Martin. "FitnessFunction". martinfowler.com.
- ISO/IEC 25010 — modelo de qualidade de produto de software.
