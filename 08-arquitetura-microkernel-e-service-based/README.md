# 08 — Arquitetura Microkernel e Arquitetura Service-Based

Dois estilos que ocupam posições opostas no espectro de distribuição: o **microkernel** é um monolito extensível; o **service-based** é uma arquitetura distribuída "pé no chão", com serviços maiores e menor complexidade operacional.

## Objetivos de aprendizagem

- Explicar a estrutura core + plug-ins do microkernel.
- Avaliar quando a extensibilidade justifica a complexidade do microkernel.
- Descrever a arquitetura service-based e suas variações.
- Comparar service-based com microsserviços.

## Arquitetura microkernel (plug-in architecture)

### Estrutura

```
┌─────────────────────────────────────┐
│           Sistema Núcleo            │
│  (regras comuns, fluxo principal)   │
│                                     │
│   ┌──────────┐   ┌──────────┐       │
│   │ Plug-in A│   │ Plug-in B│  ...  │
│   └──────────┘   └──────────┘       │
└─────────────────────────────────────┘
```

- **Core system:** contém o fluxo principal, as regras comuns e os pontos de extensão.
- **Plug-ins:** componentes independentes que adicionam comportamento específico.
- **Contrato do plug-in:** interface que o núcleo conhece e os plug-ins implementam.
- **Registry:** mecanismo que descobre e carrega os plug-ins disponíveis.

O núcleo **não conhece** os plug-ins concretos; conhece apenas o contrato. Isso permite adicionar, remover ou trocar extensões sem recompilar o núcleo.

### Exemplos

- IDEs com extensões (VS Code, Eclipse, IntelliJ);
- navegadores com add-ons;
- plataformas de e-commerce com módulos de pagamento e frete;
- ERPs com customizações por cliente;
- sistemas de automação com regras configuráveis.

### Vantagens e desvantagens

| Vantagens | Desvantagens |
|---|---|
| Extensibilidade sem alterar o núcleo | Complexidade de design do contrato |
| Isolamento de customizações | Performance: chamadas indiretas |
| Evolução independente de plug-ins | Versionamento e compatibilidade |
| Bom para produtos com variações por cliente | Risco de núcleo genérico demais |
| Manutenção do núcleo pequena | Testes de integração mais complexos |

### Quando usar

Produtos com **variações por cliente, mercado ou configuração**, nos quais o fluxo principal é estável e as extensões mudam com frequência.

## Arquitetura service-based

### Estrutura

A **service-based architecture (SBA)** organiza o sistema em **serviços de granulação grossa** (macroserviços), normalmente de 4 a 12, cada um responsável por um domínio amplo.

```
┌──────────────────────────────────────┐
│              UI / BFF                │
└──────────────┬───────────────────────┘
               │
┌──────────────▼───────────────────────┐
│           API Facade                 │
└──────┬──────────┬──────────┬─────────┘
       │          │          │
┌──────▼───┐ ┌────▼─────┐ ┌──▼───────┐
│Serviço A │ │Serviço B │ │Serviço C │
└──────┬───┘ └────┬─────┘ └──┬───────┘
       │          │          │
       └──────────┴──────────┘
          Banco compartilhado
```

Características:

- serviços maiores, com menos fronteiras e menos overhead de rede;
- **API facade** centraliza o acesso e simplifica a comunicação com a UI;
- **banco compartilhado** é comum, embora traga acoplamento;
- transações podem ser coordenadas com mais facilidade do que em microsserviços;
- deploy pode ser independente, mas muitas vezes é coordenado.

### Vantagens e desvantagens

| Vantagens | Desvantagens |
|---|---|
| Menor complexidade que microservices | Banco compartilhado acopla os serviços |
| Boa separação de domínios | Escala independente limitada |
| Transações mais simples | Deploy nem sempre é independente |
| Boa performance de rede | Menor isolamento de falhas |
| Equipe menor consegue operar | Pode virar monólito distribuído |

### Quando usar

- sistemas de negócio de complexidade média;
- organizações com equipes pequenas ou média maturidade em operação distribuída;
- quando se quer algum grau de autonomia sem o custo total de microsserviços;
- migração gradual de um monólito para serviços.

## Service-based versus microsserviços

| Aspecto | Service-based | Microsserviços |
|---|---|---|
| Granularidade | Macroserviços | Serviços pequenos |
| Banco | Frequentemente compartilhado | Um por serviço |
| Transações | Coordenação mais simples | Sagas e consistência eventual |
| Deploy | Pode ser coordenado | Independente |
| Complexidade operacional | Média | Alta |
| Escala | Por serviço, limitada | Granular |
| Equipe | Pequena/média | Múltiplos times autônomos |

A SBA é frequentemente a escolha mais sensata quando a organização ainda não tem maturidade para microsserviços.

## Trade-offs e armadilhas

- **Microkernel genérico demais:** o núcleo tenta prever todas as extensões e vira complexo.
- **Contrato de plug-in instável:** cada mudança quebra extensões existentes.
- **SBA com banco compartilhado:** se todos acessam todas as tabelas, é um monólito distribuído.
- **Confundir tamanho com autonomia:** um serviço grande não é automaticamente autônomo.
- **Escolher microsserviços "porque é o padrão":** a SBA costuma entregar mais valor com menos custo em contextos menores.

## Perguntas para revisão

1. Quais são os elementos de um microkernel e qual o papel do registro?
2. Por que o núcleo não deve conhecer os plug-ins concretos?
3. O que caracteriza a arquitetura service-based?
4. Qual o risco do banco compartilhado na SBA?
5. Em que cenário você escolheria SBA em vez de microsserviços?

## Para ir além

- RICHARDS, Mark; FORD, Neal. *Fundamentos de Arquitetura de Software*. Cap. 12 — Microkernel Architecture e Cap. 13 — Service-Based Architecture.
- FOWLER, Martin. "Microservice Premium". martinfowler.com.
- RICHARDS, Mark. "Service-Based Architecture: The Middle Ground". developerToArchitect.com.
