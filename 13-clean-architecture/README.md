# 13 — Clean Architecture

A Clean Architecture, proposta por Robert C. Martin, organiza o código para que as **regras de negócio não dependam de detalhes** como frameworks, banco de dados ou interface. O princípio central é simples: as dependências apontam para dentro.

## Objetivos de aprendizagem

- Explicar a regra da dependência.
- Identificar as camadas e suas responsabilidades.
- Diferenciar entidades, casos de uso e adaptadores.
- Comparar Clean Architecture com arquitetura hexagonal e onion.
- Reconhecer os custos e as críticas do estilo.

## A regra da dependência

> As dependências de código-fonte devem apontar apenas para dentro, na direção das regras de negócio.

Nada em uma camada interna pode conhecer algo de uma camada externa. As camadas externas podem depender das internas; o contrário nunca.

Consequências:

- o domínio não importa o framework web;
- os casos de uso não conhecem o banco de dados;
- a interface e a persistência são substituíveis;
- os testes de regra de negócio rodam sem infraestrutura.

## As camadas

```
┌─────────────────────────────────────────────┐
│ Frameworks & Drivers                        │
│  ┌───────────────────────────────────────┐  │
│  │ Interface Adapters                    │  │
│  │  ┌─────────────────────────────────┐  │  │
│  │  │ Use Cases                       │  │  │
│  │  │  ┌───────────────────────────┐  │  │  │
│  │  │  │ Entities                  │  │  │  │
│  │  │  └───────────────────────────┘  │  │  │
│  │  └─────────────────────────────────┘  │  │
│  └───────────────────────────────────────┘  │
└─────────────────────────────────────────────┘
        dependências apontam para dentro
```

### Entidades

Objetos de negócio que encapsulam as regras mais gerais e estáveis da empresa. Não devem depender de nada além da linguagem e das bibliotecas padrão.

Exemplo: `Pedido` com regras de cálculo de desconto e validação de itens.

### Casos de uso

Orquestram o fluxo de uma operação de negócio. Coordenam entidades e definem os contratos (interfaces) que as camadas externas precisam implementar.

Exemplo: `CriarPedido`, `CancelarAssinatura`, `ProcessarPagamento`.

Os casos de uso não sabem se o resultado será salvo em PostgreSQL, MongoDB ou em memória; eles dependem de uma interface (ex.: `PedidoRepository`).

### Adaptadores de interface

Convertem dados entre o formato do domínio e o formato das ferramentas externas:

- controllers e presenters (web);
- gateways e repositórios (banco);
- adaptadores de mensageria;
- mapeadores entre DTOs e entidades.

### Frameworks e drivers

A camada mais externa: banco de dados, framework web, biblioteca de UI, fila, serviços externos. É onde os detalhes vivem. Deve conter o mínimo possível de código de negócio.

## Inversão de dependência na prática

O caso de uso define uma interface:

```typescript
interface PedidoRepository {
  salvar(pedido: Pedido): Promise<void>;
  buscarPorId(id: string): Promise<Pedido | null>;
}
```

A implementação concreta fica na camada externa:

```typescript
class PostgresPedidoRepository implements PedidoRepository {
  async salvar(pedido: Pedido): Promise<void> {
    // detalhes de SQL
  }
  async buscarPorId(id: string): Promise<Pedido | null> {
    // detalhes de SQL
  }
}
```

O fluxo de controle vai do caso de uso para o repositório; a dependência de código-fonte vai na direção oposta, graças à interface. Isso é o **Princípio da Inversão de Dependência (DIP)**.

## Comparação com outros estilos

| Estilo | Ênfase | Fronteira principal |
|---|---|---|
| **Clean Architecture** | Casos de uso no centro | Regra da dependência |
| **Hexagonal (ports & adapters)** | Portas e adaptadores | Entrada/saída substituíveis |
| **Onion** | Camadas concêntricas | Domínio no centro |
| **Camadas tradicional** | Separação por responsabilidade | Camada superior chama a inferior |

Os três primeiros compartilham a mesma ideia: **o domínio no centro, a infraestrutura na periferia**. A diferença está principalmente no vocabulário e na ênfase.

## Benefícios

- **Testabilidade:** regras de negócio testadas sem banco, sem web, sem mocks pesados.
- **Independência de frameworks:** trocar a biblioteca web não afeta o domínio.
- **Independência de banco:** persistência é detalhe substituível.
- **Independência de UI:** a mesma regra serve a web, mobile ou CLI.
- **Manutenibilidade:** fronteiras claras reduzem o impacto de mudanças.

## Custos e críticas

- **Mais código e mapeamentos:** DTOs, interfaces e adaptadores adicionam camadas.
- **Overengineering em sistemas simples:** CRUDs podem não justificar a estrutura.
- **Curva de aprendizado:** exige disciplina para não vazar dependências.
- **Risco de "camadas de cerimônia":** muitos arquivos para pouca regra de negócio.
- **Não resolve granularidade de serviços:** é um estilo de organização interna, não de distribuição.

## Aplicação prática

1. Modele as entidades e as regras de negócio primeiro.
2. Defina os casos de uso com seus contratos de entrada e saída.
3. Crie interfaces para as dependências externas (repositórios, gateways).
4. Implemente os adaptadores na periferia.
5. Mantenha as dependências apontando para dentro — use testes ou análise estática para garantir.
6. Aplique o estilo onde houver regra de negócio relevante; em CRUDs simples, avalie o custo.

## Trade-offs e armadilhas

- **Vazar o framework:** entidade importando anotações de ORM.
- **Caso de uso anêmico:** apenas repassa dados para o repositório.
- **Interface para tudo:** criar abstração sem necessidade real de substituição.
- **Confundir Clean Architecture com pastas:** a estrutura de diretórios não garante a regra da dependência.
- **Aplicar em todo lugar:** o estilo é uma ferramenta, não um dogma.

## Perguntas para revisão

1. O que diz a regra da dependência?
2. Qual a diferença entre entidade e caso de uso?
3. Como o DIP permite que o domínio não dependa do banco?
4. Quais os custos de adotar Clean Architecture?
5. Em que aspectos Clean, hexagonal e onion se parecem?

## Para ir além

- MARTIN, Robert C. *Clean Architecture: a arte da robustez e da resiliência do software*. Parte III e IV.
- COCKBURN, Alistair. *Hexagonal Architecture*. alistair.cockburn.us.
- PALERMO, Jeffrey. *Clean Architecture in .NET* (exemplo prático).
- MARTIN, Robert C. "The Clean Architecture". blog.cleancoder.com.
