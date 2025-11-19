# 📊 Painel Financeiro & Previdência - Estilo Banco do Brasil

![Power BI](https://img.shields.io/badge/Power_BI-Desktop-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![Status](https://img.shields.io/badge/Status-Concluído-brightgreen?style=for-the-badge)
![Design](https://img.shields.io/badge/Design-Banco_do_Brasil-003DA5?style=for-the-badge)

> Um dashboard analítico completo desenvolvido no Microsoft Power BI, focado na demonstração de resultados financeiros de planos de previdência, aplicando rigorosamente a identidade visual corporativa do Banco do Brasil.

---

## 🎯 Objetivo do Projeto

Transformar dados brutos de balancetes contábeis (`.xlsx`) em informações gerenciais visuais, permitindo a análise rápida de:
- Saldos iniciais e finais por plano.
- Evolução mensal do fluxo de investimentos.
- Monitoramento do Patrimônio Social.
- Comparativo entre diferentes planos de previdência.

Tudo isso aplicando conceitos de **UX/UI Design** baseados no guia de marca do Banco do Brasil para garantir uma interface profissional e familiar ao usuário corporativo.

---

## 🛠️ Stack Tecnológica

* **Microsoft Power BI Desktop:** Ferramenta principal de desenvolvimento.
* **Power Query (M):** Extração, Transformação e Carregamento (ETL) dos dados.
* **DAX (Data Analysis Expressions):** Criação de medidas complexas e inteligência de tempo.
* **Excel:** Fonte de dados bruta (`Base.xlsx` e `Planos.xlsx`).

---

## ⚙️ Funcionalidades e Desenvolvimento

### 1. Modelagem de Dados (Star Schema)
O projeto utiliza uma arquitetura otimizada em estrela:
* **Tabela Fato:** `Base` (Movimentações financeiras).
* **Tabelas Dimensão:** `Planos` (Cadastro) e `dCalendario` (Inteligência temporal).
* *Tratamento:* Conversão de chaves (`NU_CNPB`, `NUM_CONTA`) para texto no Power Query para garantir a integridade dos relacionamentos.

### 2. Cálculos DAX Principais
Foram desenvolvidas medidas específicas para filtrar contas contábeis sem poluir o modelo de dados:

**Variação do Patrimônio Social:**
```dax
Variação Patrimônio Social = 
CALCULATE(
    SUM('Base'[VL_DEBITO]) - SUM('Base'[VL_CREDITO]),
    'Base'[NM_CONTA] = "PATRIMÔNIO SOCIAL"
)
