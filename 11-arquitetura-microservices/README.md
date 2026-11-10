# 11 — Arquitetura Microservices

Microsserviços são o estilo distribuído mais discutido da última década. Esta aula separa o conceito dos modismos: o que é um microsserviço, o que ele exige e quando ele não vale a pena.

## Objetivos de aprendizagem

- Definir microsserviços e seus princípios.
- Avaliar granularidade e fronteiras de serviço.
- Entender comunicação, dados e operação em um sistema distribuído.
- Reconhecer os antipadrões e os custos reais do estilo.

## O que são microsserviços

Um microsserviço é um **serviço pequeno, autônomo e implantável de forma independente**, organizado em torno de uma capacidade de negócio e com seu próprio modelo de dados.

Princípios comuns:

- **Autonomia:** cada serviço decide como implementar sua responsabilidade.
- **Deploy independente:** uma mudança em um serviço não exige reimplantar os demais.
- **Organização por domínio:** fronteiras baseadas em bounded contexts, não em camadas técnicas.
- **Descentralização de dados:** cada serviço é dono do seu estado.
- **Comunicação por contratos:** APIs ou mensagens bem definidas.
- **Tolerância a falhas:** falhas parciais não devem derrubar o sistema inteiro.

## Granularidade: o problema central

Não existe "tamanho certo" universal. A granularidade deve ser definida por:

- **coesão de negócio:** o serviço resolve uma capacidade completa;
- **autonomia de mudança:** o serviço pode evoluir sem coordenar com outros;
- **fronteira de dados:** o serviço é dono dos dados que precisa;
- **tamanho da equipe:** um serviço por time, não um time por serviço;
- **custo de comunicação:** chamadas remotas são caras; dividir demais gera latência e complexidade.

Sintomas de granularidade errada:

- **nanoservices:** serviços minúsculos que só fazem CRUD e exigem orquestração constante;
- **distributed monolith:** serviços que precisam ser implantados juntos e compartilham banco;
- **serviço "faz-tudo":** um serviço gigante que concentra o domínio.

## Comunicação

### Síncrona

- **REST/HTTP:** simples, amplamente suportado, bom para APIs públicas.
- **gRPC:** contratos fortes, binário e eficiente, bom para comunicação interna.

Riscos: acoplamento temporal, cascata de falhas, latência acumulada.

### Assíncrona

- **Mensageria/eventos:** desacoplamento, bufferização, resiliência.

Riscos: consistência eventual, duplicidade, complexidade de rastreamento.

### Padrões de infraestrutura

- **API gateway:** ponto de entrada único, roteamento, autenticação e rate limiting.
- **BFF (Backend for Frontend):** API dedicada a um tipo de cliente.
- **Service discovery:** localização dinâmica das instâncias.
- **Service mesh:** comunicação, retries, mTLS e telemetria entre serviços.

## Dados

- **Database per service:** cada serviço é dono do seu esquema; outros acessam apenas via API.
- **Saga:** coordena transações distribuídas com compensações.
- **Outbox:** publica eventos de forma confiável junto com a transação local.
- **CQRS:** separa leitura e escrita quando os modelos divergem.
- **Consistência eventual:** o sistema converge, mas não instantaneamente.

Compartilhar banco entre serviços é o atalho mais comum para criar um **distributed monolith**.

## Operação

Microsserviços transferem complexidade do código para a operação. Sem estes itens, o estilo tende a falhar:

- **CI/CD** por serviço;
- **observabilidade:** logs estruturados, métricas e tracing distribuído;
- **correlation IDs** para seguir requisições;
- **containers e orquestração** (Docker, Kubernetes);
- **health checks, circuit breakers, retries e timeouts**;
- **cultura de ownership:** o time que constrói também opera.

## Quando usar

- domínios complexos com múltiplas capacidades de negócio;
- organização com vários times que precisam de autonomia;
- necessidade real de escalar partes diferentes em ritmos diferentes;
- maturidade em automação, observabilidade e operação distribuída.

## Quando evitar

- domínio simples ou ainda em descoberta;
- equipe pequena sem estrutura de operação;
- prazos curtos com baixa tolerância a complexidade;
- ausência de CI/CD e observabilidade;
- quando um monólito modular atende ao requisito.

## Antipadrões

| Antipadrão | Sintoma |
|---|---|
| Distributed monolith | Deploy acoplado e banco compartilhado |
| Nanoservices | Serviços triviais e muitas chamadas remotas |
| Shared database | Serviços leem tabelas uns dos outros |
| Chatty services | Dezenas de chamadas para montar uma tela |
| Hardcoded endpoints | Configuração espalhada e frágil |
| Sem tracing | Impossível diagnosticar falhas |

## Trade-offs e armadilhas

- **Complexidade distribuída:** rede não é confiável; falhas parciais são a regra.
- **Consistência:** transações distribuídas exigem sagas e compensações.
- **Custo operacional:** múltiplos pipelines, monitoramento e ambientes.
- **Curva de aprendizado:** a equipe precisa dominar sistemas distribuídos.
- **Moda:** adotar microsserviços sem os problemas que eles resolvem.

## Perguntas para revisão

1. O que torna um serviço "microsserviço" e não apenas um serviço?
2. Como definir a granularidade de um serviço?
3. Por que o banco compartilhado é um antipadrão nesse estilo?
4. O que é um distributed monolith?
5. Que capacidades operacionais são pré-requisito para microsserviços?

## Para ir além

- RICHARDS, Mark; FORD, Neal. *Fundamentos de Arquitetura de Software*. Cap. 17 — Microservices Architecture.
- NEWMAN, Sam. *Building Microservices*. 2. ed.
- RICHARDSON, Chris. *Microservices Patterns*.
- FOWLER, Martin; LEWIS, James. "Microservices". martinfowler.com.
- The Twelve-Factor App — 12factor.net.
