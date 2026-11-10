# 09 — Arquitetura Event-Driven

Na arquitetura orientada a eventos, componentes reagem a **eventos** em vez de chamar uns aos outros diretamente. Isso produz alto desacoplamento — e uma série de desafios novos de consistência, rastreabilidade e depuração.

## Objetivos de aprendizagem

- Diferenciar eventos, comandos e mensagens.
- Comparar as topologias broker e mediator.
- Explicar padrões como event sourcing, CQRS e saga.
- Reconhecer os desafios de consistência e idempotência.

## Eventos, comandos e mensagens

| Conceito | Definição | Exemplo |
|---|---|---|
| **Evento** | Fato ocorrido no passado, imutável | `PedidoCriado`, `PagamentoAprovado` |
| **Comando** | Intenção de que algo aconteça | `CriarPedido`, `CancelarAssinatura` |
| **Mensagem** | Envelope transportado por um canal | O evento ou comando serializado |

Eventos descrevem **o que aconteceu**; comandos descrevem **o que deve acontecer**. Confundir os dois leva a acoplamento disfarçado: um "evento" que exige uma reação específica é, na prática, um comando.

## Topologias

### Broker (coreografia)

Os componentes publicam eventos em um broker e os consumidores se inscrevem nos eventos que lhes interessam.

```
Produtor ──▶ [Broker] ──▶ Consumidor A
                    └───▶ Consumidor B
```

- **Vantagens:** alto desacoplamento, fácil adicionar consumidores, escalabilidade.
- **Desvantagens:** fluxo difícil de visualizar, sem controle central, risco de loops e de eventos duplicados.

### Mediator (orquestração)

Um componente mediador recebe eventos e coordena os próximos passos, emitindo comandos para os participantes.

```
Produtor ──▶ [Mediator] ──▶ Serviço A
                       ──▶ Serviço B
                       ──▶ Serviço C
```

- **Vantagens:** fluxo explícito, controle central, tratamento de erros e compensações centralizado.
- **Desvantagens:** o mediador pode virar gargalo e ponto de acoplamento; risco de centralizar demais a lógica.

## Componentes comuns

- **Event channel:** canal por onde os eventos trafegam.
- **Event processor:** componente que consome e reage a eventos.
- **Event queue:** fila que bufferiza eventos para processamento.
- **Broker:** infraestrutura de publicação e assinatura (Kafka, RabbitMQ, SNS/SQS).
- **Mediator:** coordenador de fluxos.

## Padrões relacionados

### Event sourcing

Em vez de armazenar apenas o estado atual, o sistema armazena a **sequência de eventos** que levou a esse estado. O estado é reconstruído pela reprodução dos eventos.

- **Vantagens:** auditoria completa, histórico, possibilidade de reconstruir projeções.
- **Desvantagens:** complexidade, evolução de esquemas de eventos, crescimento do log.

### CQRS (Command Query Responsibility Segregation)

Separa o modelo de escrita (comandos) do modelo de leitura (consultas). Cada lado pode ter seu próprio modelo e armazenamento.

- **Vantagens:** otimização independente, leitura escalável.
- **Desvantagens:** consistência eventual entre os modelos, complexidade adicional.

### Saga

Coordena transações distribuídas por meio de uma sequência de transações locais com **ações compensatórias** em caso de falha.

- **Coreografia:** cada serviço reage e dispara o próximo evento.
- **Orquestração:** um coordenador central decide os próximos passos.

### Outbox

Garante que a publicação de eventos e a gravação no banco ocorram de forma atômica, gravando o evento na mesma transação e publicando-o depois.

## Desafios

- **Consistência eventual:** os dados ficam temporariamente inconsistentes entre componentes.
- **Idempotência:** consumidores precisam tolerar eventos repetidos.
- **Ordenação:** eventos podem chegar fora de ordem; use chaves de partição quando necessário.
- **Duplicidade:** entrega "pelo menos uma vez" exige deduplicação.
- **Rastreabilidade:** sem correlation IDs, fica difícil seguir um fluxo entre serviços.
- **Depuração:** o fluxo é assíncrono e distribuído; logs e tracing são essenciais.
- **Evolução de contratos:** eventos antigos precisam continuar sendo consumidos.

## Trade-offs e armadilhas

- **Evento como comando disfarçado:** acoplamento escondido.
- **Eventos sem schema:** consumidores quebram com mudanças.
- **Broker como banco de dados:** usar o log de eventos para consultas operacionais sem projeção adequada.
- **Saga sem compensação:** falhas deixam o sistema em estado inconsistente.
- **Assíncrono para tudo:** fluxos simples ficam mais difíceis sem ganho real.

## Perguntas para revisão

1. Qual a diferença entre evento e comando?
2. Compare as topologias broker e mediator.
3. O que é event sourcing e que problema ele resolve?
4. Por que idempotência é obrigatória em consumidores de eventos?
5. Quando a consistência eventual é aceitável?

## Para ir além

- RICHARDS, Mark; FORD, Neal. *Fundamentos de Arquitetura de Software*. Cap. 14 — Event-Driven Architecture.
- FOWLER, Martin. "Event Sourcing" e "CQRS". martinfowler.com.
- KLEPPMANN, Martin. *Designing Data-Intensive Applications*. Cap. 11.
- RICHARDSON, Chris. *Microservices Patterns* — Saga e Outbox.
