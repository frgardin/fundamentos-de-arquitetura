# 02 — Pensamento Arquitetural

Arquitetura é menos sobre saber a resposta certa e mais sobre formular boas perguntas, comparar alternativas e assumir as consequências. Esta aula trata do modo de pensar que sustenta todas as decisões seguintes.

## Objetivos de aprendizagem

- Aplicar pensamento sistêmico a problemas de software.
- Analisar decisões em termos de trade-offs.
- Diferenciar amplitude e profundidade de conhecimento técnico.
- Reconhecer vieses e armadilhas comuns na escolha de tecnologias.

## Pensamento sistêmico

Um sistema não é a soma das partes: é o produto das interações entre elas. Pensar sistemicamente significa olhar para:

- **fronteiras:** o que está dentro e fora do sistema analisado;
- **fluxos:** dados, eventos, dinheiro e responsabilidades que atravessam as partes;
- **feedback:** como uma mudança em uma parte afeta as demais;
- **ambiente:** usuários, integrações, regulação e a organização que constrói o sistema.

A consequência prática: uma decisão local ótima pode ser ruim para o sistema. Cachear tudo pode melhorar a latência de uma tela e criar inconsistências em outra.

## Tudo é trade-off

Não existe decisão arquitetural sem custo. Toda escolha favorece algumas características e prejudica outras:

- microsserviços aumentam a autonomia de times e a complexidade operacional;
- um banco relacional forte simplifica transações e dificulta escalabilidade horizontal;
- consistência forte reduz anomalias de dados e aumenta a latência;
- uma arquitetura em camadas facilita o entendimento e pode criar acoplamento excessivo.

O trabalho do arquiteto é **explicitar o que se ganha, o que se perde e por que a troca faz sentido** para aquele contexto.

### Perguntas que ajudam a analisar um trade-off

1. Qual característica arquitetural esta decisão melhora?
2. Qual característica ela degrada?
3. Quão difícil é reverter a decisão depois?
4. Que evidência temos de que o problema existe?
5. Qual é a alternativa mais simples que atende ao requisito?

## Amplitude versus profundidade

O arquiteto precisa de **amplitude técnica**: conhecer o suficiente sobre muitas tecnologias para saber quando cada uma se aplica. Profundidade extrema em uma única stack pode levar a soluções enviesadas.

Duas práticas ajudam:

- **Regra dos 20 minutos:** dedicar um tempo curto por dia para estudar um tema fora da zona de conforto.
- **Technology radar:** classificar tecnologias em adotar, testar, avaliar e evitar, revisando periodicamente.

Amplitude não significa superficialidade. Significa saber fazer as perguntas certas e reconhecer quando chamar um especialista.

## Vieses e armadilhas

- **Arquitetura guiada pelo currículo:** escolher a tecnologia da moda para valorizar o currículo, não o sistema.
- **Bala de prata:** acreditar que uma ferramenta resolve problemas estruturais.
- **Viés de confirmação:** buscar apenas evidências que sustentam a escolha já feita.
- **Overengineering:** antecipar problemas que talvez nunca ocorram.
- **Paralisia por análise:** adiar decisões indefinidamente enquanto o custo de não decidir cresce.

## Documentar o raciocínio

Uma decisão sem contexto vira dogma. Registre:

- o problema e as restrições do momento;
- as alternativas consideradas;
- os critérios usados na comparação;
- a decisão e suas consequências esperadas;
- as condições que fariam a decisão ser revista.

Esse registro é a base dos **Architecture Decision Records (ADRs)**, aprofundados na aula 12.

## Perguntas para revisão

1. O que significa dizer que uma decisão local pode ser globalmente ruim?
2. Como explicar um trade-off para alguém não técnico?
3. Qual a diferença entre amplitude e profundidade técnica?
4. Por que a decisão mais simples costuma ser um bom ponto de partida?
5. Que sinais indicam que uma escolha foi guiada por moda em vez de contexto?

## Para ir além

- RICHARDS, Mark; FORD, Neal. *Fundamentos de Arquitetura de Software*. Cap. 2 — Architectural Thinking.
- THINKING, Fast and Slow — Daniel Kahneman (vieses de decisão).
- ThoughtWorks Technology Radar — thoughtworks.com/radar.
