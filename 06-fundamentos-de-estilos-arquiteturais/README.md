# 06 — Fundamentos de Estilos Arquiteturais

Estilos arquiteturais são padrões recorrentes de organização de componentes e conectores. Conhecê-los permite comparar alternativas com critérios, em vez de escolher por moda ou familiaridade.

## Objetivos de aprendizagem

- Definir estilo arquitetural e seus elementos.
- Classificar estilos em monolíticos e distribuídos.
- Comparar estilos por características e trade-offs.
- Usar uma matriz de decisão como apoio à escolha.

## O que é um estilo arquitetural

Um **estilo arquitetural** descreve a estrutura de um sistema em termos de:

- **componentes:** as partes que executam a lógica;
- **conectores:** como as partes se comunicam (chamadas, mensagens, pipes);
- **restrições:** regras sobre como componentes e conectores podem ser combinados;
- **propriedades:** as características que o estilo tende a favorecer.

Um estilo é um ponto de partida, não uma camisa de força. Sistemas reais frequentemente combinam estilos (por exemplo, microsserviços com componentes internos em camadas).

## Monolíticos versus distribuídos

### Monolíticos

Tudo executa em um único processo de deploy.

- **Vantagens:** simplicidade operacional, transações locais, baixa latência entre componentes, fácil depuração.
- **Desvantagens:** acoplamento de deploy, escala vertical, um único ponto de falha, risco de "big ball of mud".

Exemplos: camadas, pipeline, microkernel, monólito modular.

### Distribuídos

Componentes executam em processos ou máquinas separadas.

- **Vantagens:** escala independente, isolamento de falhas, autonomia de times, deploy independente.
- **Desvantagens:** latência de rede, consistência eventual, complexidade operacional, depuração difícil, falhas parciais.

Exemplos: service-based, event-driven, space-based, microsserviços.

> A primeira lei da arquitetura distribuída: se você não precisa, não distribua. Distribuir troca complexidade de código por complexidade operacional.

## O antipadrão "big ball of mud"

O **big ball of mud** é o estilo que emerge quando não há decisões conscientes: componentes sem fronteiras, dependências cruzadas e mudanças que afetam tudo. Ele não é escolhido; é o resultado da ausência de arquitetura.

Sinais de alerta:

- dependências cíclicas generalizadas;
- código duplicado com pequenas variações;
- qualquer mudança exige tocar em muitos lugares;
- ninguém consegue explicar a estrutura do sistema.

## Panorama dos estilos do curso

| Estilo | Categoria | Favorece | Dificulta |
|---|---|---|---|
| **Camadas** | Monolítico | Simplicidade, organização por responsabilidade | Escalabilidade, isolamento de deploy |
| **Pipeline** | Monolítico | Composição, reuso de filtros, processamento em etapas | Interatividade, transações, baixa latência |
| **Microkernel** | Monolítico | Extensibilidade, customização, evolução de plug-ins | Performance, complexidade do núcleo |
| **Service-based** | Distribuído | Equilíbrio entre autonomia e simplicidade | Escala extrema, independência total de deploy |
| **Event-driven** | Distribuído | Desacoplamento, reatividade, extensibilidade | Consistência, rastreabilidade, depuração |
| **Space-based** | Distribuído | Elasticidade, picos de carga, baixa latência | Consistência forte, custo de memória |
| **Microservices** | Distribuído | Autonomia, deploy independente, escala por serviço | Complexidade operacional e de dados |

## Como escolher um estilo

A escolha deve partir das **características arquiteturais prioritárias** e das restrições do contexto:

1. Liste as características prioritárias (aula 04).
2. Avalie quais estilos favorecem cada uma.
3. Considere restrições: equipe, orçamento, prazo, maturidade operacional.
4. Identifique os trade-offs que a organização aceita pagar.
5. Documente a decisão e revise-a quando o contexto mudar.

### Matriz de decisão

| Critério (peso) | Estilo A | Estilo B | Estilo C |
|---|---|---|---|
| Escalabilidade (3) | 2 | 3 | 3 |
| Simplicidade operacional (3) | 3 | 1 | 2 |
| Time-to-market (2) | 3 | 1 | 2 |
| **Total ponderado** | **15** | **12** | **15** |

A matriz não decide sozinha: ela torna os critérios explícitos e as notas discutíveis. O valor está na conversa, não no número.

## Trade-offs e armadilhas

- **Escolher o estilo mais moderno:** moda não é critério arquitetural.
- **Copiar a arquitetura de outra empresa:** contexto, escala e equipe são diferentes.
- **Misturar estilos sem critério:** híbridos podem funcionar, mas exigem fronteiras claras.
- **Ignorar o custo operacional:** um estilo distribuído demanda observabilidade, CI/CD e cultura de operação.
- **Achar que o estilo resolve tudo:** o estilo define a estrutura; a qualidade depende da execução.

## Perguntas para revisão

1. Quais elementos definem um estilo arquitetural?
2. Compare vantagens e desvantagens de sistemas monolíticos e distribuídos.
3. O que caracteriza o antipadrão big ball of mud?
4. Como uma matriz de decisão ajuda na escolha de um estilo?
5. Por que a escolha do estilo deve vir depois da identificação das características?

## Para ir além

- RICHARDS, Mark; FORD, Neal. *Fundamentos de Arquitetura de Software*. Cap. 9 — Foundations.
- BASS, Len; CLEMENTS, Paul; KAZMAN, Rick. *Software Architecture in Practice*. Cap. 4.
- FOWLER, Martin. "Patterns of Enterprise Application Architecture" — catálogo de estilos.
