# Análise de Risco de Crédito

![Excel](https://img.shields.io/badge/Ferramenta-Microsoft%20Excel-217346?style=flat&logo=microsoft-excel&logoColor=white)
![Status](https://img.shields.io/badge/Status-Concluído-brightgreen)

Projeto de Análise de Dados focado na avaliação de risco de crédito, com o objetivo de identificar padrões de inadimplência e apoiar a tomada de decisão na concessão de crédito.

---

## Problema do Negócio

Uma instituição bancária necessitava de compreender melhor o perfil de risco dos seus clientes de crédito, a fim de tomar decisões mais rigorosas na aprovação de empréstimos, identificar os segmentos mais vulneráveis à inadimplência e reduzir as perdas de capital.

O Gestor levantou as seguintes questões para serem respondidas:

1. Quais tipos de empréstimo têm o maior percentual de "Mau Pagadores"?
2. Empréstimos de longo prazo e valores altos apresentam maior risco?
3. Clientes com conta crítica falham mais?
4. Existe um padrão de risco ligado à idade ou ao tipo de moradia?
5. Como o nível de comprometimento (1 a 4) afeta a classificação do Target (Status de Risco)?

---

## Contexto

A base de dados utilizada contém informações de clientes de crédito de uma instituição bancária, com variáveis que cobrem o perfil financeiro, demográfico e comportamental de cada cliente. A análise foi realizada com o objectivo de identificar padrões de risco e gerar recomendações accionáveis para a política de concessão de crédito.

>  **Fonte dos dados:** [Kaggle](https://www.kaggle.com/datasets/raulconstanski/risco-de-credito-alemao-portugues)

---

## Premissas da Análise

- Os dados foram tratados e analisados no **Microsoft Excel**.
- Antes de carregar os dados para análise, foram realizadas as seguintes transformações no **Power Query**:

| Transformação | Descrição |
|---------------|-----------|
| **Encoding UTF-8** | Alterado para reconhecer caracteres especiais com acentos |
| **Coluna "Status Risco"** | Coluna condicional criada a partir da coluna `Target`: valor 1 → *Baixo Risco*, valor 2 → *Alto Risco* |
| **Separação "Estado Civil - Sexo"** | A coluna original foi dividida em duas colunas independentes: `Estado Civil` e `Sexo` |
| **Substituição de "n/há"** | Os valores sem informação foram substituídos por frases mais claras e descritivas |
| **Coluna "Status Emprego"** | Coluna condicional criada a partir de `Emprego actual desde`, para identificar melhor a experiência de trabalho de cada cliente |
| **Coluna "Faixa Etária"** | Coluna condicional criada a partir de `Idade em anos`, para segmentar os clientes por faixa etária |
| **Coluna "Status Conta Corrente"** | Coluna condicional criada para dar mais clareza aos movimentos da conta corrente |
| **Limpeza final** | Remoção de espaços nos caracteres e eliminação de valores nulos |

- Todas as transacções foram consideradas válidas para a análise.
- A coluna `Target` é a variável central da análise, onde **1 = Bom Pagador** e **2 = Mau Pagador**.

---

## Estratégia da Solução

### Passo 1 — Resumo do Contexto em Pergunta Aberta
> *Qual é o perfil de risco dos clientes de crédito desta instituição bancária?*

### Passo 2 — Transformação em Perguntas Fechadas
> - Quais finalidades de crédito concentram mais maus pagadores?
> - Contratos mais longos e de maior valor geram mais inadimplência?
> - Clientes com histórico de conta crítica são mais propensos ao incumprimento?
> - A idade e o tipo de moradia influenciam o nível de risco do cliente?
> - Um maior comprometimento da renda aumenta a probabilidade de inadimplência?

### Passo 3 — Definição da Coluna Facto
A coluna facto principal é **Target** (rebaptizada como `Status de Risco`), pois é a variável que classifica cada cliente como Bom ou Mau Pagador e serve de base para todas as análises de risco.

### Passo 4 — Identificação das Dimensões

| Dimensão | Coluna |
|----------|--------|
| Perfil Financeiro | `Valor do crédito`, `Duração em meses`, `Comprometimento de Renda` |
| Comportamento Bancário | `Movimentação na conta`, `Status Conta Corrente`, `Histórico de pagamentos` |
| Finalidade | `Finalidade do crédito` |
| Perfil Demográfico | `Idade em anos`, `Faixa Etária`, `Sexo`, `Estado Civil`, `Forma de Moradia` |
| Situação Laboral | `Emprego actual desde`, `Status Emprego`, `Trabalhador estrangeiro` |
| Classificação de Risco | `Target`, `Status de Risco` |

### Passo 5 — Hipóteses Analíticas

- H1: Determinadas finalidades de crédito concentram uma proporção maior de maus pagadores.
- H2: Empréstimos de maior valor e longa duração apresentam maior risco de inadimplência.
- H3: Clientes com conta crítica têm maior probabilidade de falhar nos pagamentos.
- H4: A faixa etária e o tipo de moradia influenciam directamente o perfil de risco do cliente.
- H5: Clientes com maior comprometimento da renda têm maior probabilidade de inadimplência.

### Passo 6 — Critérios de Priorização

As hipóteses foram priorizadas com base em dois critérios:

- **Impacto Financeiro** — quanto a hipótese afecta directamente as perdas de capital da instituição.
- **Relevância Estratégica** — quanto o insight pode influenciar a política de concessão de crédito.

### Passo 7 — Priorização das Hipóteses Analíticas

| Prioridade | Hipótese | Justificativa |
|------------|----------|---------------|
| Alta | H2 — Risco em contratos longos e de alto valor | Maior exposição financeira da instituição |
| Alta | H5 — Comprometimento da renda vs. inadimplência | Impacto directo na capacidade de pagamento |
| Média | H1 — Finalidade do crédito vs. inadimplência | Orienta critérios de aprovação por produto |
| Média | H4 — Idade e moradia vs. risco | Permite segmentar melhor o perfil de risco |
| Baixa | H3 — Conta crítica vs. inadimplência | Reavaliação da política para novos clientes |

---

## Insights da Análise

### 1 — Tipos de Empréstimo com Maior Percentual de Mau Pagadores
O elevado índice de inadimplência em **Educação** sugere que investimentos de longo prazo sem retorno imediato aumentam a vulnerabilidade financeira do cliente. A categoria **"Outros"** apresenta risco elevado devido à incerteza sobre o destino do capital, enquanto o risco em **Carros Novos** (superior ao de Carros Usados) indica que parcelas mais altas combinadas com a depreciação do bem impactam directamente a capacidade de pagamento — exigindo critérios de aprovação mais rigorosos para estas finalidades.

<img width="660" height="314" alt="Analise1" src="https://github.com/user-attachments/assets/4989f4dc-7255-4011-8ded-f9945e9f4560" />


### 2 — Risco em Empréstimos de Longo Prazo e Alto Valor
Os dados revelam uma correlação directa entre o tempo de contrato e o prejuízo potencial: quanto maior a duração do empréstimo, maior é o valor médio em risco. Em todas as faixas de tempo, o valor médio dos **maus pagadores ($3.938)** é significativamente superior ao dos **bons pagadores ($2.985)**. O ponto de maior vulnerabilidade está nos contratos **acima de 40 meses**, onde o ticket médio ultrapassa os **$7.000**, sugerindo que empréstimos de alto valor e longa duração devem exigir critérios de aprovação muito mais rigorosos para evitar grandes perdas de capital.

<img width="661" height="217" alt="Analise2" src="https://github.com/user-attachments/assets/e2a74ea9-77e5-483a-b3cb-b5b536d7ee71" />


### 3 — Clientes com Conta Crítica vs. Novos Clientes
Os dados revelam um padrão contra-intuitivo: clientes com **Conta Crítica** (16,4% de risco) são mais fiéis aos pagamentos do que aqueles **sem histórico anterior** (63,2% de alto risco). Isso indica que a ausência de histórico representa um perigo maior para o banco do que um passado conturbado, possivelmente porque clientes "críticos" são tomadores recorrentes que o banco já conhece e monitoriza de perto. O maior risco da instituição não está nos devedores conhecidos, mas nos **novos clientes sem histórico documentado**, exigindo uma política de entrada muito mais rigorosa para este perfil.

<img width="662" height="194" alt="Analise3" src="https://github.com/user-attachments/assets/f593a2a6-69cd-4812-a665-0695bcc47228" />



### 4 — Padrão de Risco por Idade e Tipo de Moradia
Os dados revelam um padrão de risco surpreendente: **a posse de imóvel não é garantia de pagamento**. O grupo de **Adultos (26–40 anos) com casa própria** é o que mais traz prejuízo ao banco, representando sozinho **37% de todos os casos de alto risco** (112 de 300). Isso indica que existe uma "falsa sensação de segurança" ao emprestar para este perfil, levando à libertação de valores acima da capacidade real de pagamento dos clientes. Recomenda-se que o banco seja mais rigoroso e reduza os limites de crédito para o público adulto, mesmo que possuam casa própria.

<img width="751" height="224" alt="Analise4" src="https://github.com/user-attachments/assets/07fe9f3e-574d-4764-b6a6-cfd901498534" />

### 5 — Comprometimento da Renda vs. Status de Risco
Existe uma relação directa: **quanto maior o comprometimento da renda, maior a chance de inadimplência**. No **Nível 1** (menor peso no salário), o risco é de **25%**, subindo para **33% no Nível 4**. Isso indica que clientes com o orçamento mais "apertado" têm menos margem para imprevistos, tornando-se mais arriscados para a instituição. Recomenda-se que o banco priorize a aprovação de clientes nos **níveis 1 e 2**, sendo muito mais rigoroso nos **níveis 3 e 4**, onde 1 em cada 3 clientes acaba por falhar no pagamento.

<img width="662" height="170" alt="Analise5" src="https://github.com/user-attachments/assets/1b924241-9927-40d0-8bf8-9725da740afa" />


---

## Resultados

<img width="1870" height="894" alt="Analise de Risco Dashboard" src="https://github.com/user-attachments/assets/2be675cd-9425-4036-a033-f3eed36226cc" />


Com base na análise, é possível concluir que:

- Finalidades como **Educação, "Outros" e Carros Novos** exigem critérios de aprovação mais rigorosos devido ao elevado índice de inadimplência.
- Contratos **acima de 40 meses** com tickets elevados representam o maior risco de perda de capital para a instituição.
- O maior perigo não está nos clientes com histórico negativo conhecido, mas nos **novos clientes sem qualquer histórico de crédito** — que devem passar por um processo de entrada mais criterioso.
- **Adultos com casa própria** representam um perfil de risco subestimado — a posse de imóvel não deve ser usada como critério suficiente para aprovação de crédito elevado.
- A instituição deve **limitar ou condicionar** a aprovação de crédito para clientes nos **níveis 3 e 4** de comprometimento de renda, onde o risco de inadimplência é significativamente mais alto.

---

## Estrutura do Projecto

```
 analise-risco-credito
│
├──  dados
│   └── risco-de-credito-alemao-traduzido-ptgues.csv           # Base de dados original do Kaggle
├──  analise
│   └── Análise de Risco de credito Macro.xlsx                 # Base de dados tratada, análises e dashboard
└──  README.md                                                 # Documentação do projecto
```

---

## Ferramentas Utilizadas

- **Microsoft Excel** — Para o tratamento e transformação dos dados via Power Query, colunas calculadas e condicionais, Tabelas Dinâmicas, Gráficos, Macro e Dashboard

---

## Autor

**Santiago Casseca**  
[LinkedIn](www.linkedin.com/in/santiago-casseca-496b84195)
