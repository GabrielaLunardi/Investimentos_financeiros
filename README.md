# 💰 Investimentos Financeiros — Planilha de Planejamento e Simulação

![Investimentos Financeiros](investimentos_financeiros_banner.png)

Planilha em Excel para planejamento financeiro pessoal com foco em **investimentos mensais recorrentes** e **Fundos de Investimento Imobiliário (FIIs)**. A ferramenta simula o crescimento do patrimônio ao longo do tempo, projeta dividendos mensais e sugere uma alocação de carteira de acordo com o perfil de risco do investidor.

---

Esta planilha foi criada para ajudar a responder, de forma rápida e visual, perguntas como:

- Se eu investir **R$ X por mês**, quanto vou acumular em **2, 5, 10, 20 ou 30 anos**?
- Quanto de **dividendo mensal** esse patrimônio pode gerar no futuro?
- Com base no meu **perfil de investidor**, como devo distribuir meus aportes entre os diferentes tipos de FIIs?

Todos os cálculos são feitos automaticamente a partir de fórmulas nativas do Excel e de intervalos nomeados, o que torna a planilha fácil de entender, auditar e adaptar.

---

##  Estrutura do arquivo

O arquivo `Projeto_-_Investimentos_financeiros.xlsx` contém **2 abas**:

### 1. `Tabela_financeira`
Aba principal, onde ficam as configurações, os cálculos e os resultados.

### 2. `Tabela_de_apoio`
Tabela auxiliar (banco de dados) com os percentuais de alocação sugeridos para cada perfil de investidor. Serve como base para as fórmulas de `PROCV` da aba principal, não precisa ser editada no uso comum da planilha.

---

##  Como a aba `Tabela_financeira` é organizada

###  Configurações
| Campo | Descrição | Exemplo |
|---|---|---|
| **Salário** | Renda mensal usada como referência | R$ 2.000,00 |
| **Rendimento da carteira** | Rendimento médio mensal esperado da carteira | 0,60% |
| **Sugestão de investimento (30%)** | Calcula automaticamente 30% do salário como valor sugerido de aporte mensal | `=30%*Salario` |

###  Investimento mensal
| Campo | Descrição |
|---|---|
| **Quanto investir por mês?** | Valor de aporte mensal definido pelo usuário |
| **Por quantos anos?** | Prazo do investimento, em anos |
| **Taxa de rendimento mensal?** | Taxa de juros/rendimento mensal usada na projeção |
| **Patrimônio acumulado?** | Valor futuro do patrimônio, calculado com a função `VF` (Valor Futuro) |
| **Dividendos mensais?** | Estimativa de dividendos mensais gerados pelo patrimônio acumulado (`patrimônio × rendimento da carteira`) |

### Cenários
Projeção automática do patrimônio acumulado e do dividendo mensal correspondente para cinco cenários diferentes: 2, 5, 10, 20 e 30 anos, permitindo que o comparare o efeito dos juros compostos no longo prazo sem precisar alterar o campo "Por quantos anos?".

### Perfil e alocação sugerida
| Campo | Descrição |
|---|---|
| **Perfil** | Selecione entre `CONSERVADOR`, `MODERADO` ou `AGRESSIVO` |
| **Valor a ser investido por mês** | Puxado automaticamente do campo de aporte mensal |
| **Tabela de tipos de FII** | Mostra o percentual sugerido e o valor em R$ a ser alocado em cada tipo de fundo, de acordo com o perfil escolhido |

Tipos de FII contemplados: **Papel, Tijolo, Híbridos, FOFs, Desenvolvimento e Hotelárias.**

---

## Perfis de investidor e alocação sugerida

| Tipo de FII | Conservador | Moderado | Agressivo |
|---|---|---|---|
| Papel | 30% | 32% | 50% |
| Tijolo | 50% | 35% | 10% |
| Híbridos | 10% | 8% | 5% |
| FOFs | 10% | 5% | 5% |
| Desenvolvimento | 0% | 10% | 20% |
| Hotelárias | 0% | 10% | 10% |

> Esses percentuais ficam armazenados na aba `Tabela_de_apoio` e são buscados automaticamente via `PROCV`, combinando o perfil selecionado com o tipo de FII (`PERFIL & "-" & TIPO DE FII`).

---

## Fórmulas e lógica utilizadas

| Elemento | Uso |
|---|---|
| `VF()` (Valor Futuro) | Calcula o patrimônio acumulado ao final do período, com base em aportes mensais constantes e uma taxa de rendimento fixa |
| `PROCV()` | Busca, na tabela de apoio, o percentual de alocação sugerido para a combinação perfil + tipo de FII |
| Concatenação de chave (`&`) | Cria uma chave única (`PERFIL-TIPO`) na tabela de apoio para permitir a busca com `PROCV` |
| **Intervalos nomeados** | Os principais campos possuem nomes definidos, o que torna as fórmulas mais legíveis (ex: `=VF(Taxa_mensal;Qntd_anos*12;Aporte*-1)` em vez de referências de célula soltas) |

### Intervalos nomeados definidos
| Nome | Célula | Significado |
|---|---|---|
| `Salario` | `Tabela_financeira!D13` | Renda mensal |
| `Rendimento_carteira` | `Tabela_financeira!D14` | Rendimento mensal médio da carteira |
| `Sugestao_investimento` | `Tabela_financeira!D15` | 30% do salário |
| `Aporte` | `Tabela_financeira!D18` | Valor investido por mês |
| `Qntd_anos` | `Tabela_financeira!D19` | Prazo em anos |
| `Taxa_mensal` | `Tabela_financeira!D20` | Taxa de rendimento mensal |
| `patrimonio` | `Tabela_financeira!D21` | Patrimônio acumulado projetado |

---

##  Como usar:

1. Baixe o arquivo `Projeto_-_Investimentos_financeiros.xlsx` e abra no **Microsoft Excel** (ou em alternativas compatíveis, como Google Sheets ou LibreOffice Calc).
2. Na seção **CONFIGURAÇÕES**, informe seu **salário** e o **rendimento médio esperado da carteira**.
3. Na seção **INVESTIMENTO MENSAL**, defina:
   - Quanto pretende investir por mês;
   - Por quantos anos pretende manter os aportes;
   - A taxa de rendimento mensal esperada.
4. Veja automaticamente o **patrimônio acumulado** e os **dividendos mensais estimados**.
5. Confira a seção **CENÁRIOS** para comparar a evolução do patrimônio em 2, 5, 10, 20 e 30 anos.
6. Em **PERFIL**, escolha seu perfil de investidor (`CONSERVADOR`, `MODERADO` ou `AGRESSIVO`) e veja a sugestão de distribuição do seu aporte mensal entre os tipos de FII.

---

##  Exemplo de simulação incluído no arquivo

Com os valores de exemplo já preenchidos na planilha:

- **Aporte mensal:** R$ 600,00
- **Prazo:** 5 anos
- **Taxa de rendimento mensal:** 1,079%
- **Patrimônio acumulado:** ≈ R$ 50.266,15
- **Dividendo mensal estimado:** ≈ R$ 301,60
- **Perfil selecionado:** Agressivo → maior concentração em FIIs de Papel (50%) e Desenvolvimento (20%)

| Prazo | Patrimônio acumulado | Dividendo mensal |
|---|---|---|
| 2 anos | R$ 16.336,58 | R$ 98,02 |
| 5 anos | R$ 50.266,15 | R$ 301,60 |
| 10 anos | R$ 145.970,53 | R$ 875,82 |
| 20 anos | R$ 675.119,04 | R$ 4.050,71 |
| 30 anos | R$ 2.593.301,79 | R$ 15.559,81 |

---

##  Tecnologias

- Microsoft Excel (`.xlsx`)
- Funções nativas: `VF`, `PROCV`, concatenação, formatação condicional de moeda (R$) e percentual
- Intervalos nomeados para legibilidade das fórmulas

---

## ⚠️ Aviso importante

Esta planilha tem **finalidade educacional e de simulação**. Os percentuais de alocação, taxas de rendimento e projeções são estimativas baseadas em premissas definidas pelo usuário e **não constituem recomendação de investimento**. Rendimentos passados ou projetados não garantem resultados futuros. Antes de investir, consulte um profissional certificado.

---

## Licença

Este projeto pode ser usado livremente para fins de estudo e planejamento pessoal. Sinta-se à vontade para adaptar os percentuais, prazos e taxas de acordo com a sua realidade.

📥 [Baixar a planilha (.xlsx)](Projeto_-_Investimentos_financeiros.xlsx)

---
