# Fundamentos de Arquitetura de Sistemas

Repositório de estudos do curso de **Arquitetura de Sistemas** da **Anhanguera**.

Cada aula tem uma pasta própria com:

- `README.md` — conteúdo de referência, com objetivos, conceitos, trade-offs e perguntas de revisão;
- `anotacoes.md` — espaço pessoal para resumos, dúvidas e conexões feitas durante a aula;
- `anexo/` — materiais da aula, como slides, PDFs e planilhas.

> A ideia é que este repositório funcione como um caderno técnico vivo: o README explica, as anotações registram o que você entendeu.

## Sobre o curso

O curso percorre a arquitetura de software do fundamento à prática: o que é arquitetura, como pensar em trade-offs, como modularizar um sistema, como identificar características arquiteturais e como escolher (e documentar) um estilo arquitetural.

O fio condutor é uma ideia simples: **arquitetura é o conjunto de decisões estruturais que são caras de mudar depois**. Por isso, o curso trata estilos arquiteturais não como receitas, mas como conjuntos de trade-offs que precisam ser avaliados contra as características que o sistema precisa entregar.

### Objetivos de aprendizagem

Ao final do curso, você deve ser capaz de:

- explicar o que é arquitetura de software e qual o papel do arquiteto;
- analisar decisões arquiteturais em termos de trade-offs;
- avaliar coesão, acoplamento e limites de módulos;
- identificar e priorizar características arquiteturais;
- comparar estilos arquiteturais (camadas, pipeline, microkernel, service-based, event-driven, space-based e microservices);
- documentar decisões e riscos arquiteturais;
- aplicar os princípios da Clean Architecture na organização de dependências.

## Estrutura das aulas

| # | Aula | Tema central | Pasta |
|---|------|--------------|-------|
| 01 | Introdução | O que é arquitetura, por que importa e o papel do arquiteto | [`01-introducao`](01-introducao/) |
| 02 | Pensamento arquitetural | Trade-offs, pensamento sistêmico e amplitude técnica | [`02-pensamento-arquitetural`](02-pensamento-arquitetural/) |
| 03 | Modularização | Coesão, acoplamento, fronteiras e métricas de módulo | [`03-modularizacao`](03-modularizacao/) |
| 04 | Características arquiteturais | Atributos de qualidade, fitness functions e priorização | [`04-caracteristicas-arquiteturais`](04-caracteristicas-arquiteturais/) |
| 05 | Pensamento component-based | Componentes, contratos, granularidade e reuso | [`05-pensamento-component-based`](05-pensamento-component-based/) |
| 06 | Fundamentos de estilos arquiteturais | Estrutura, categorias de estilo e critérios de escolha | [`06-fundamentos-de-estilos-arquiteturais`](06-fundamentos-de-estilos-arquiteturais/) |
| 07 | Camadas e Pipeline | Layered architecture e pipes & filters | [`07-arquitetura-em-camadas-e-pipeline`](07-arquitetura-em-camadas-e-pipeline/) |
| 08 | Microkernel e Service-based | Núcleo extensível e serviços macro | [`08-arquitetura-microkernel-e-service-based`](08-arquitetura-microkernel-e-service-based/) |
| 09 | Event-driven | Eventos, broker, mediator, CQRS e sagas | [`09-arquitetura-event-driven`](09-arquitetura-event-driven/) |
| 10 | Space-based | Processamento em memória, data grids e elasticidade | [`10-arquitetura-space-based`](10-arquitetura-space-based/) |
| 11 | Microservices | Autonomia, granularidade, dados e operação distribuída | [`11-arquitetura-microservices`](11-arquitetura-microservices/) |
| 12 | Escolhas, decisões e riscos | ADRs, matrizes de decisão, riscos e dívida técnica | [`12-escolhas-decisoes-e-riscos`](12-escolhas-decisoes-e-riscos/) |
| 13 | Clean Architecture | Regra da dependência, fronteiras e casos de uso | [`13-clean-architecture`](13-clean-architecture/) |

## Como usar este repositório

### 1. Clone o repositório

```bash
git clone https://github.com/frgardin/fundamentos-de-arquitetura.git
cd fundamentos-de-arquitetura
```

### 2. Estude pela pasta da aula

Leia o `README.md` da aula antes ou depois da exposição do professor. Ele funciona como um mapa: não substitui a aula, mas organiza o que foi visto. Os slides e demais materiais fornecidos ficam em `anexo/`, na pasta da aula.

### 3. Registre suas anotações

Use o `anotacoes.md` de cada pasta para:

- resumir a aula com as **suas** palavras;
- listar conceitos que ainda não ficaram claros;
- registrar exemplos reais (sistemas que você conhece, projetos, notícias);
- conectar a aula com as anteriores e com a próxima.

Dica: escrever o resumo sem consultar o material é uma das formas mais eficientes de descobrir o que você realmente aprendeu.

### 4. Acompanhe o progresso

Marque as aulas concluídas:

- [ ] 01 — Introdução
- [ ] 02 — Pensamento arquitetural
- [ ] 03 — Modularização
- [ ] 04 — Características arquiteturais
- [ ] 05 — Pensamento component-based
- [ ] 06 — Fundamentos de estilos arquiteturais
- [ ] 07 — Arquitetura em camadas e arquitetura pipeline
- [ ] 08 — Arquitetura microkernel e arquitetura service-based
- [ ] 09 — Arquitetura event-driven
- [ ] 10 — Arquitetura space-based
- [ ] 11 — Arquitetura microservices
- [ ] 12 — Escolhas, decisões e riscos
- [ ] 13 — Clean Architecture

## Referências principais

- RICHARDS, Mark; FORD, Neal. **Fundamentos de Arquitetura de Software**: uma abordagem moderna para o design de sistemas distribuídos. 2. ed. São Paulo: Alta Books.
- MARTIN, Robert C. **Clean Architecture**: a arte da robustez e da resiliência do software. São Paulo: Alta Books.
- BASS, Len; CLEMENTS, Paul; KAZMAN, Rick. **Software Architecture in Practice**. 4. ed. Addison-Wesley.
- EVANS, Eric. **Domain-Driven Design**: atacando as complexidades da modelagem de software. Rio de Janeiro: Alta Books.
- NYGARD, Michael. **Release It!**: design and deploy production-ready software. 2. ed. Pragmatic Bookshelf.
- FOWLER, Martin. **martinfowler.com** — artigos sobre estilos, padrões e arquitetura evolutiva.

## Licença e uso

Material de estudo produzido a partir das aulas da Anhanguera. O conteúdo dos READMEs é um resumo autoral para fins educacionais; as obras citadas pertencem aos seus respectivos autores e editoras.
