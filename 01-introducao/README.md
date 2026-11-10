# 01 — Introdução à Arquitetura de Software

Antes de comparar estilos ou escolher tecnologias, precisamos responder a uma pergunta: o que exatamente estamos decidindo quando fazemos arquitetura? Esta aula estabelece o vocabulário e o papel do arquiteto.

## Objetivos de aprendizagem

- Definir arquitetura de software e diferenciá-la de design detalhado.
- Reconhecer as quatro dimensões de uma decisão arquitetural.
- Entender por que decisões arquiteturais são caras de mudar.
- Descrever as expectativas e as competências de um arquiteto.

## O que é arquitetura de software

Não existe uma definição única, mas as definições convergem em alguns pontos:

- **Bass, Clements e Kazman:** a arquitetura de um sistema é a estrutura dos seus elementos, suas propriedades externas e as relações entre eles.
- **Richards e Ford:** arquitetura é o conjunto de decisões estruturais que definem como o sistema é organizado e como ele entrega suas características.
- **Martin Fowler:** arquitetura é o que é difícil de mudar depois — as decisões que você gostaria de ter acertado desde o início.

Uma definição prática: **arquitetura é o desenho das partes que compõem o sistema, das responsabilidades de cada parte e das regras de comunicação entre elas.**

## Arquitetura não é design

A fronteira é graduada, mas útil:

| Arquitetura | Design |
|---|---|
| Decide a estrutura geral e as fronteiras | Refina a solução dentro das fronteiras |
| Tem custo alto de reversão | Tem custo menor de reversão |
| Busca atender características arquiteturais | Busca atender requisitos funcionais e detalhes locais |
| Envolve stakeholders e restrições organizacionais | Envolve principalmente a equipe técnica |

Na prática, o arquiteto também projeta. A diferença está no **escopo e no custo da decisão**, não em uma divisão rígida de trabalho.

## As quatro dimensões da arquitetura

Richards e Ford organizam a arquitetura em quatro dimensões:

1. **Estrutura** — como o sistema é dividido em componentes, camadas ou serviços.
2. **Características arquiteturais** — os atributos de qualidade que o sistema deve ter (escalabilidade, disponibilidade, segurança etc.).
3. **Decisões** — as regras que definem como a estrutura funciona e como as pessoas devem trabalhar nela.
4. **Princípios** — as diretrizes que orientam decisões futuras quando não há uma decisão explícita.

As três primeiras são concretas; os princípios são o que permite que a arquitetura permaneça coerente sem que o arquiteto precise decidir tudo.

## Por que arquitetura importa

- **Custo de mudança:** decisões estruturais afetam todo o sistema; corrigi-las depois custa caro.
- **Comunicação:** a arquitetura é o vocabulário comum entre negócio, desenvolvimento e operação.
- **Qualidade:** características como disponibilidade e performance não são obtidas por acidente; precisam ser projetadas e testadas.
- **Risco:** uma arquitetura inadequada pode inviabilizar requisitos de negócio mesmo que o código esteja "funcionando".

## O papel do arquiteto

O arquiteto moderno não é apenas o profissional que desenha diagramas no início do projeto. As expectativas incluem:

- **Visão sistêmica:** entender como as partes se encaixam e como o sistema interage com o ambiente.
- **Tomada de decisão:** escolher entre alternativas com informações incompletas e justificar os trade-offs.
- **Comunicação:** traduzir preocupações técnicas para o negócio e vice-versa.
- **Mentoria:** elevar a equipe, revisar decisões e disseminar princípios.
- **Mão na massa:** manter contato com o código para não perder a noção das consequências das decisões.

Um arquiteto que só decide no início e desaparece tende a produzir uma arquitetura desconectada da realidade. Arquitetura é uma atividade contínua, não uma fase.

## Trade-offs e armadilhas

- **Arquitetura por acidente:** o sistema ganha uma estrutura sem que ninguém tenha decidido conscientemente.
- **Arquiteto "de PowerPoint":** decisões tomadas sem validação no código.
- **Busca pela arquitetura perfeita:** toda escolha tem custo; o objetivo é equilibrar, não eliminar trade-offs.
- **Confundir arquitetura com framework:** usar Spring, .NET ou React não é, por si só, uma decisão arquitetural.

## Perguntas para revisão

1. Qual a diferença entre uma decisão arquitetural e uma decisão de design?
2. Por que o custo de reversão é um critério importante para classificar decisões?
3. Quais são as quatro dimensões da arquitetura e por que os princípios são necessários?
4. O que significa dizer que arquitetura é uma atividade contínua?
5. Dê um exemplo de decisão arquitetural em um sistema que você conhece.

## Materiais anexos

- [Slides (96).zip](anexo/Slides%20%2896%29.zip) — slides da aula.
- [arquitetura-de-sistemas-elder-moraes.pdf](anexo/arquitetura-de-sistemas-elder-moraes.pdf) — material da disciplina.
- [arquitetura-de-sistemas-elder-moraes-material-autoral.pdf](anexo/arquitetura-de-sistemas-elder-moraes-material-autoral.pdf) — material autoral.

## Para ir além

- RICHARDS, Mark; FORD, Neal. *Fundamentos de Arquitetura de Software*. Cap. 1 — Introduction.
- BASS, Len; CLEMENTS, Paul; KAZMAN, Rick. *Software Architecture in Practice*. Cap. 1.
- FOWLER, Martin. "Who Needs an Architect?". martinfowler.com.
