# 10 — Arquitetura Space-Based

Quando o banco de dados se torna o gargalo e a carga varia de forma imprevisível, a arquitetura space-based propõe eliminar o banco central do caminho crítico, mantendo os dados em memória distribuída.

## Objetivos de aprendizagem

- Explicar o problema que a arquitetura space-based resolve.
- Descrever seus componentes principais.
- Entender o papel dos data grids e do cache replicado.
- Avaliar os trade-offs de elasticidade, custo e consistência.

## O problema

Em arquiteturas tradicionais, o banco de dados relacional centraliza o estado e limita a escalabilidade:

- todas as instâncias da aplicação leem e escrevem no mesmo banco;
- picos de carga geram contenção e latência;
- escalar a aplicação não resolve o gargalo do banco;
- a disponibilidade do banco vira um ponto único de falha.

A arquitetura **space-based** (também chamada de **cloud architecture** ou **in-memory distributed architecture**) resolve isso replicando o estado em memória entre as instâncias de processamento.

## Componentes

```
┌──────────────────────────────────────────────────┐
│              Unidades de Processamento           │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐        │
│  │ PU 1     │  │ PU 2     │  │ PU 3     │        │
│  └────┬─────┘  └────┬─────┘  └────┬─────┘        │
│       └─────────────┴─────────────┘              │
│              Data Grid (memória)                 │
└──────────────────────┬───────────────────────────┘
                       │
              ┌────────▼────────┐
              │  Data Pump      │
              └────────┬────────┘
                       │
              ┌────────▼────────┐
              │  Banco / Fonte  │
              └─────────────────┘
```

- **Processing unit (PU):** instância da aplicação que contém a lógica de negócio e os dados em memória.
- **Virtualized middleware:** abstrai a comunicação, o balanceamento e a replicação entre as PUs.
- **Data grid / replicated cache:** armazena os dados em memória, replicados entre as PUs (ex.: Hazelcast, Apache Ignite, Redis).
- **Data pump:** sincroniza os dados entre o grid e a fonte de dados (banco, mensageria).
- **Data writer / data reader:** componentes que movem dados do grid para a persistência e vice-versa.

## Como funciona

1. A requisição chega a qualquer instância de processamento.
2. A PU lê e escreve no **data grid** em memória.
3. Os dados são replicados entre as PUs de forma síncrona ou assíncrona.
4. O **data pump** persiste as mudanças no banco de dados de forma assíncrona.
5. Novas PUs podem ser adicionadas sem reconfigurar o banco.

O banco deixa de estar no caminho crítico: ele vira um repositório de persistência e não a fonte de leitura em tempo real.

## Características favorecidas

- **Elasticidade:** adicionar ou remover PUs conforme a carga.
- **Performance:** acesso a dados em memória, sem round-trip ao banco.
- **Disponibilidade:** se uma PU falhar, outra assume com os dados replicados.
- **Escalabilidade horizontal:** o estado acompanha a aplicação.
- **Tolerância a picos:** bom para cargas imprevisíveis.

## Trade-offs e desafios

| Ganho | Custo |
|---|---|
| Baixa latência | Consumo de memória elevado |
| Elasticidade | Complexidade de replicação |
| Alta disponibilidade | Consistência eventual |
| Picos de carga | Custo de infraestrutura |
| Escala horizontal | Sincronização e conflitos de escrita |

### Consistência

A replicação pode ser:

- **síncrona:** menor latência de consistência, maior custo de coordenação;
- **assíncrona:** melhor desempenho, risco de leitura desatualizada.

Em cenários de escrita concorrente na mesma chave, é preciso definir estratégias de **versionamento, locks ou resolução de conflitos**.

### Persistência

O data pump precisa lidar com:

- falhas durante a gravação;
- eventos duplicados;
- ordem de atualização;
- recuperação após queda de uma PU.

## Quando usar

- picos de acesso imprevisíveis (Black Friday, campanhas, eventos esportivos);
- sistemas com alta concorrência de leitura e escrita;
- aplicações que exigem baixa latência;
- processamento em memória de grandes volumes de dados.

Não é uma boa escolha quando o domínio exige **consistência forte** e transações complexas, ou quando o volume de dados não cabe em memória de forma econômica.

## Trade-offs e armadilhas

- **Tratar o grid como banco durável:** memória não é persistência.
- **Ignorar conflitos de escrita:** replicação sem estratégia de resolução gera perda de dados.
- **Subestimar custo de memória:** data grids são caros em escala.
- **Consistência eventual sem aviso:** usuários podem ver dados desatualizados.
- **Complexidade operacional:** monitorar, particionar e recuperar um grid distribuído não é trivial.

## Perguntas para revisão

1. Qual problema do banco de dados central a arquitetura space-based resolve?
2. Qual o papel do data pump?
3. Por que a consistência eventual é uma consequência natural desse estilo?
4. Em que situações space-based não é adequada?
5. Como o estilo se compara a simplesmente adicionar um cache na frente do banco?

## Para ir além

- RICHARDS, Mark; FORD, Neal. *Fundamentos de Arquitetura de Software*. Cap. 15 — Space-Based Architecture.
- FOWLER, Martin. "Cache". martinfowler.com.
- Documentação do Hazelcast e do Apache Ignite.
- KLEPPMANN, Martin. *Designing Data-Intensive Applications*. Cap. 5 e 6.
