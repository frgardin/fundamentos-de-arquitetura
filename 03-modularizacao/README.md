# 03 — Modularização

Sistemas grandes só são compreensíveis quando divididos em partes com fronteiras claras. Modularização é a arte de decidir onde essas fronteiras ficam — e o que pode atravessá-las.

## Objetivos de aprendizagem

- Explicar coesão, acoplamento, abstração e encapsulamento.
- Avaliar a qualidade de um módulo usando métricas.
- Reconhecer dependências cíclicas e outros problemas estruturais.
- Relacionar módulos, bounded contexts e a estrutura da organização.

## O que é modularidade

**Modularidade** é a propriedade de um sistema ser composto por partes relativamente independentes, cada uma com uma responsabilidade bem definida. Um módulo pode ser um pacote, um namespace, um conjunto de classes ou um serviço — o conceito independe da tecnologia.

A modularidade importa porque permite:

- **compreensão:** estudar uma parte sem carregar o sistema inteiro na cabeça;
- **paralelismo:** times trabalharem em partes diferentes;
- **evolução:** mudar uma parte com impacto controlado;
- **testabilidade:** testar unidades isoladas.

## Coesão

Coesão mede o quanto as responsabilidades de um módulo estão relacionadas. Quanto maior a coesão, melhor — desde que o módulo não fique pequeno demais.

Tipos de coesão, do pior para o melhor:

1. **Coincidental:** partes agrupadas sem relação (ex.: pacote `utils`).
2. **Lógica:** partes do mesmo tipo, mas com propósitos diferentes (ex.: todas as validações).
3. **Temporal:** partes executadas no mesmo momento (ex.: inicialização).
4. **Procedural:** partes que seguem uma sequência de execução.
5. **Comunicacional:** partes que operam sobre os mesmos dados.
6. **Sequencial:** a saída de uma parte é a entrada da outra.
7. **Funcional:** todas as partes contribuem para uma única tarefa bem definida.

## Acoplamento

Acoplamento mede o grau de dependência entre módulos. Quanto menor, melhor — mas acoplamento zero significa que os módulos não colaboram.

Formas de acoplamento, da mais forte para a mais fraca:

- **Conteúdo:** um módulo acessa diretamente os dados internos de outro.
- **Comum:** módulos compartilham estado global.
- **Externo:** dependência de um formato ou protocolo externo.
- **Controle:** um módulo passa flags que alteram o fluxo interno de outro.
- **Dados:** módulos trocam apenas dados por parâmetros.
- **Mensagem:** comunicação por eventos ou mensagens bem definidas.

## Abstração e encapsulamento

- **Abstração** é expor o essencial e esconder o detalhe. Uma boa abstração permite trocar a implementação sem afetar os consumidores.
- **Encapsulamento** é impedir o acesso ao estado interno. Ele protege as regras de negócio e reduz o acoplamento.

A combinação dos dois define o **contrato** do módulo: o que ele promete fazer, não como faz.

## Métricas de módulo

Robert C. Martin propõe três métricas úteis para avaliar pacotes:

| Métrica | Fórmula | Interpretação |
|---|---|---|
| **Instabilidade (I)** | `I = Ce / (Ca + Ce)` | 0 = estável, 1 = instável |
| **Abstração (A)** | `A = classes abstratas / total de classes` | 0 = concreto, 1 = abstrato |
| **Distância da sequência principal (D)** | `D = \|A + I - 1\|` | 0 = equilibrado, 1 = zona de dor |

Onde `Ca` é o número de módulos que dependem deste e `Ce` é o número de módulos dos quais este depende.

A ideia central: **módulos estáveis devem ser abstratos** (para poderem ser estendidos sem mudança) e **módulos instáveis devem ser concretos** (para absorverem mudanças). Um módulo concreto e muito estável é difícil de mudar; um módulo abstrato e muito instável é inútil.

## Fronteiras e dependências

- **Dependências cíclicas** são um sinal de fronteiras mal definidas: A depende de B, que depende de C, que depende de A. Elas dificultam testes, build e evolução.
- **Dependência estável** aponta na direção das abstrações, não das implementações.
- **Bounded context** (DDD) é uma fronteira de significado: dentro dele, um termo tem um modelo único. Dois contextos podem usar a mesma palavra com sentidos diferentes.
- **Lei de Conway:** a estrutura do sistema tende a espelhar a estrutura de comunicação da organização. Se a arquitetura precisa de outra divisão, a organização também precisa mudar.

## Modular monolith

Um **monólito modular** organiza o sistema em módulos bem delimitados, mas executa tudo em um único processo. É uma alternativa intermediária: mantém a simplicidade operacional do monólito e preserva a possibilidade de extrair módulos no futuro, se as fronteiras estiverem limpas.

## Trade-offs e armadilhas

- **Granularidade excessiva:** muitos módulos minúsculos aumentam a navegação e a coordenação.
- **Granularidade insuficiente:** um módulo faz tudo e vira um mini-monólito.
- **Pacote `utils`:** coesão coincidente disfarçada de reuso.
- **Fronteira só no nome:** pastas separadas, mas acesso livre ao estado interno umas das outras.
- **Otimizar métricas:** a métrica orienta a conversa; ela não substitui o julgamento arquitetural.

## Perguntas para revisão

1. Qual a diferença entre coesão e acoplamento?
2. Por que módulos estáveis devem ser abstratos?
3. O que é uma dependência cíclica e por que ela é problemática?
4. Como a Lei de Conway influencia a modularização?
5. Quando um monólito modular é preferível a microsserviços?

## Para ir além

- RICHARDS, Mark; FORD, Neal. *Fundamentos de Arquitetura de Software*. Cap. 3 — Modularity.
- MARTIN, Robert C. *Clean Architecture*. Parte III — Design de componentes.
- EVANS, Eric. *Domain-Driven Design*. Cap. 14 — Maintained Model Integrity.
- FOWLER, Martin. "BoundedContext". martinfowler.com.
