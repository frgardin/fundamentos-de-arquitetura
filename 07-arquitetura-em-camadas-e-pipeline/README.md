# 07 — Arquitetura em Camadas e Arquitetura Pipeline

Dois estilos monolíticos clássicos, com lógicas opostas: um organiza o sistema por **responsabilidade** (camadas); o outro organiza por **fluxo de processamento** (pipeline).

## Objetivos de aprendizagem

- Explicar a estrutura e o funcionamento da arquitetura em camadas.
- Reconhecer o antipadrão *architecture sinkhole*.
- Explicar pipes & filters e suas propriedades.
- Comparar os dois estilos e identificar contextos de uso.

## Arquitetura em camadas (Layered Architecture)

### Estrutura

O sistema é dividido em camadas horizontais, cada uma com uma responsabilidade:

```
┌─────────────────────────────┐
│ Apresentação                │
├─────────────────────────────┤
│ Negócio                     │
├─────────────────────────────┤
│ Persistência                │
├─────────────────────────────┤
│ Banco de dados              │
└─────────────────────────────┘
```

Uma requisição atravessa as camadas de cima para baixo. Cada camada só pode chamar a camada imediatamente abaixo (camadas **fechadas**) ou pode ser acessada por qualquer camada superior (camadas **abertas**).

### Variações

- **Camadas fechadas:** isolamento maior, mas uma simples consulta pode atravessar todas as camadas sem agregar valor.
- **Camadas abertas:** permitem que a apresentação chame diretamente a persistência, o que reduz código cerimonial e aumenta o acoplamento.
- **Camadas de domínio isoladas:** a camada de negócio não conhece detalhes de persistência nem de apresentação — um passo em direção à Clean Architecture.

### Architecture sinkhole

O **sinkhole** ocorre quando uma requisição passa por várias camadas sem que nenhuma execute lógica relevante — apenas repassa a chamada. É um sintoma de camadas cerimoniais e de regras de negócio pobres ( anemia de domínio).

Mitigações:

- permitir que camadas abertas pulem camadas sem valor;
- enriquecer o domínio com comportamento;
- repensar se a separação está gerando valor real.

### Vantagens e desvantagens

| Vantagens | Desvantagens |
|---|---|
| Fácil de entender e ensinar | Pode criar acoplamento entre camadas |
| Boa separação de responsabilidades | Sinkhole e código cerimonial |
| Simples de testar por camada | Escalabilidade limitada |
| Baixa complexidade operacional | Deploy único |
| Boa para começar | Pode esconder o domínio |

### Quando usar

Sistemas de complexidade baixa a média, equipes iniciantes, aplicações internas e como ponto de partida para um monólito modular.

## Arquitetura pipeline (Pipes & Filters)

### Estrutura

O processamento é organizado como uma sequência de **filtros** conectados por **pipes**:

```
[Filtro A] ──pipe──▶ [Filtro B] ──pipe──▶ [Filtro C] ──▶ saída
```

- **Filtro:** componente que transforma, valida ou enriquece os dados.
- **Pipe:** canal que transporta os dados entre filtros.

O fluxo é normalmente **unidirecional**: cada filtro recebe dados, processa e envia o resultado adiante. Filtros podem ser reutilizados em pipelines diferentes.

### Propriedades

- **Composição:** novos comportamentos surgem da combinação de filtros.
- **Reuso:** um filtro bem definido serve a vários fluxos.
- **Testabilidade:** cada filtro pode ser testado isoladamente.
- **Paralelismo:** filtros independentes podem executar em paralelo quando o fluxo permite.
- **Acoplamento fraco:** filtros não conhecem uns aos outros, apenas o formato dos dados.

### Desvantagens

- **Latência acumulada:** cada etapa adiciona overhead.
- **Transações:** difícil manter atomicidade em um fluxo longo.
- **Interatividade:** o modelo é pouco adequado para interação síncrona com o usuário.
- **Tratamento de erros:** uma falha no meio do fluxo exige estratégia clara (retry, dead letter, compensação).
- **Formato comum:** todos os filtros precisam concordar sobre o formato dos dados.

### Quando usar

- processamento em lote (ETL, importação de arquivos);
- processamento de streams e eventos;
- compiladores e interpretadores (lexer → parser → analyzer);
- validação e transformação de documentos;
- pipelines de CI/CD.

## Comparação

| Aspecto | Camadas | Pipeline |
|---|---|---|
| Organização | Por responsabilidade | Por etapa de processamento |
| Fluxo | Requisição atravessa camadas | Dados fluem por filtros |
| Reuso | Limitado | Alto |
| Interatividade | Boa | Fraca |
| Transações | Mais simples | Difíceis |
| Complexidade | Baixa | Média |

## Trade-offs e armadilhas

- **Camadas por camada:** criar uma camada para cada tipo de classe sem necessidade.
- **Sinkhole:** camadas que só repassam chamadas.
- **Domínio anêmico:** regras espalhadas em serviços de aplicação.
- **Pipeline para tudo:** usar filtros em fluxos que exigem resposta síncrona e transacional.
- **Filtros oniscientes:** um filtro que faz validação, transformação e persistência ao mesmo tempo.

## Perguntas para revisão

1. Qual a diferença entre camadas abertas e fechadas?
2. O que é o architecture sinkhole e como evitá-lo?
3. Quais são os elementos de um pipeline?
4. Por que pipelines têm dificuldade com transações?
5. Em que situação você escolheria camadas em vez de pipeline?

## Para ir além

- RICHARDS, Mark; FORD, Neal. *Fundamentos de Arquitetura de Software*. Cap. 10 — Layered Architecture e Cap. 11 — Pipeline Architecture.
- FOWLER, Martin. "Pipes and Filters". martinfowler.com.
- BUSCHMANN, Frank; et al. *Pattern-Oriented Software Architecture*. Vol. 1.
