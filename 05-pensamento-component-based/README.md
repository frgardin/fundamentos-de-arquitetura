# 05 — Pensamento Component-Based

Antes de escolher entre camadas, serviços ou eventos, é preciso identificar **quais são os blocos** do sistema. O pensamento component-based trata da descoberta, do contrato e da granularidade desses blocos.

## Objetivos de aprendizagem

- Definir componente e diferenciá-lo de classe, módulo e serviço.
- Identificar componentes de domínio, técnicos e de infraestrutura.
- Projetar contratos claros e versionáveis.
- Avaliar granularidade e reuso sem cair em generalização prematura.

## O que é um componente

Um **componente** é uma unidade de software com uma responsabilidade bem definida, um contrato explícito e a capacidade de ser substituído ou reutilizado sem que os consumidores conheçam seus detalhes internos.

Um componente pode ser implementado como:

- um conjunto de classes em um pacote;
- uma biblioteca;
- um módulo de um monólito;
- um serviço independente;
- uma função serverless.

O que o define não é o mecanismo de deploy, mas o **contrato e a fronteira**.

## Componentes de domínio, técnicos e de infraestrutura

| Tipo | Responsabilidade | Exemplo |
|---|---|---|
| **Domínio** | Regras de negócio e conceitos do problema | Pedido, Pagamento, Estoque |
| **Técnico** | Capacidades genéricas reutilizáveis | Autenticação, auditoria, cache |
| **Infraestrutura** | Integração com o mundo externo | Banco, fila, gateway de pagamento |

Uma confusão comum é misturar regra de negócio com detalhe de infraestrutura. Um componente de domínio que importa o driver do banco perde testabilidade e acopla a regra a uma tecnologia.

## Contratos

O contrato é o que o componente promete ao mundo. Ele inclui:

- **operações:** o que pode ser chamado;
- **entradas e saídas:** formatos e significados;
- **pré-condições e pós-condições:** o que deve ser verdade antes e depois;
- **erros:** o que pode falhar e como;
- **garantias:** idempotência, ordenação, consistência.

Um bom contrato é **estável** e **expressivo**: muda pouco e comunica intenção. Contratos que expõem detalhes internos (entidades de banco, estruturas de framework) criam acoplamento desnecessário.

## Descoberta de componentes

Componentes não caem do céu. Algumas técnicas para encontrá-los:

- **Event storming:** mapear eventos de negócio, comandos e agregados para revelar fronteiras.
- **Domain-Driven Design:** identificar bounded contexts, agregados e linguagem ubíqua.
- **Análise de fluxo de valor:** seguir o caminho de uma requisição de negócio e agrupar responsabilidades coesas.
- **Workflow analysis:** observar as etapas de um processo e verificar quais compartilham dados e regras.

O resultado deve ser um conjunto de componentes com nomes do domínio, não uma divisão por camadas técnicas (`controllers`, `services`, `repositories`) que esconde as regras.

## Granularidade

Granularidade é o tamanho e o escopo de um componente. Ela envolve trade-offs:

| Componente menor | Componente maior |
|---|---|
| Mais reuso e composição | Mais coesão e menos coordenação |
| Mais contratos e integrações | Menos chamadas e latência |
| Mais overhead de governança | Mais dificuldade de reuso |
| Mais fácil de substituir | Mais difícil de extrair depois |

Não existe granularidade certa universal. O critério é a **coesão de responsabilidade** e a **estabilidade da fronteira**: se duas partes mudam juntas com frequência, talvez sejam um único componente.

## Reuso e acoplamento por contrato

Reuso é consequência de bons contratos, não de generalização antecipada. Um componente reutilizável:

- resolve um problema bem delimitado;
- tem contrato estável e documentado;
- não vaza detalhes de implementação;
- é versionado de forma compatível.

Criar abstrações para "casos futuros" costuma gerar complexidade sem retorno. Prefira extrair o componente quando o segundo consumidor aparecer.

## Componentes e estilos arquiteturais

O mesmo conjunto de componentes pode ser organizado em diferentes estilos:

- em **camadas**, componentes de domínio ficam isolados da interface e da persistência;
- em **microsserviços**, cada componente de domínio pode virar um serviço;
- em **event-driven**, componentes se comunicam por eventos;
- em **microkernel**, componentes de domínio podem ser plug-ins do núcleo.

Por isso, pensar em componentes vem **antes** de escolher o estilo.

## Trade-offs e armadilhas

- **Componente "faz-tudo":** baixa coesão e contrato gigante.
- **Contrato baseado em banco:** consumidores dependem de tabelas, não de comportamento.
- **Reuso forçado:** generalizar antes de ter consumidores reais.
- **Fronteiras por camada técnica:** organização que dificulta encontrar a regra de negócio.
- **Versionamento informal:** mudanças que quebram consumidores sem aviso.

## Perguntas para revisão

1. O que diferencia um componente de uma classe?
2. Por que componentes de domínio não devem depender de infraestrutura?
3. Como o event storming ajuda a descobrir componentes?
4. Que critérios usar para decidir a granularidade?
5. Por que o pensamento component-based antecede a escolha do estilo?

## Para ir além

- RICHARDS, Mark; FORD, Neal. *Fundamentos de Arquitetura de Software*. Cap. 8 — Component-Based Thinking.
- EVANS, Eric. *Domain-Driven Design*. Parte II — Model-Driven Design.
- BRANDOLINI, Alberto; et al. *Introducing EventStorming*.
