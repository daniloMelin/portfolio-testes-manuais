# 🛒 Projeto: E-commerce Automation Practice (Bugou? O QA tá On!)

## 📌 Visão Geral

**Contexto:** Projeto prático realizado durante o curso "Bugou? O QA tá On!" do Instituto Joga Junto. O objetivo foi validar os fluxos críticos de um e-commerce simulado, aplicando metodologias ágeis e gestão de testes profissional.

**Objetivo:** Garantir a funcionalidade, usabilidade e acessibilidade dos módulos de **Cadastro, Login, Carrinho e Checkout** no ambiente `automationpractice.pl`.

**Ferramentas Utilizadas:**

- **Gestão de Projeto:** Jira Software (Scrum/Kanban)
- **Gestão de Testes:** Zephyr Scale / Qase
- **Execução:** Manual (Exploratório e Scriptado)
- **Tipos de Teste:** Funcional, Usabilidade, Acessibilidade e Regressivo.

---

## 🗺️ Estratégia de Teste

A execução abrangeu uma varredura completa (End-to-End), identificando falhas não apenas funcionais, mas também de lógica de negócio e inclusão digital.

**Escopo Validado:**

- ✅ **Acessibilidade:** Navegação por teclado e leitores de tela.
- ✅ **Autenticação:** Cadastro, Login e Recuperação de Senha.
- ✅ **Financeiro:** Cálculos de subtotal, total e métodos de pagamento.
- ✅ **Navegação:** Links, Menus e Responsividade (Mobile).

---

## 🧪 Casos de Teste (Principais Cenários)

Abaixo, os cenários críticos executados e seus resultados:

| ID        | Funcionalidade     | Cenário                                        | Status   | Bug Relacionado                      |
| :-------- | :----------------- | :--------------------------------------------- | :------- | :----------------------------------- |
| **CT-01** | **Cadastro**       | Validar criação de conta ("Create an Account") | ❌ Falhou | **BUG-0075** (Erro 404)              |
| **CT-02** | **Login**          | Realizar login com credenciais válidas         | ❌ Falhou | **BUG-0080** (Erro 405)              |
| **CT-03** | **Carrinho**       | Adicionar produto ao carrinho                  | ❌ Falhou | **BUG-0028** (Redireciona p/ Google) |
| **CT-04** | **Pagamento**      | Finalizar compra com Cartão/Boleto             | ❌ Falhou | **BUG-0066** (Não processa)          |
| **CT-05** | **Acessibilidade** | Navegar usando apenas teclado (Tab/Enter)      | ❌ Falhou | **BUG-0022** (Sem foco/títulos)      |

---

## 🐞 Bugs Reportados (Destaques)

Foram identificados **93 bugs** no total. Abaixo, detalho os mais críticos que inviabilizam o negócio.

### 🔴 [CRÍTICO] BUG-0066 - Pagamento não processado

**Impacto:** Perda total de receita. Nenhuma forma de pagamento (Cartão, Boleto, PIX) finaliza a compra.
**Cenário:** Tela de Checkout > Seleção de Pagamento.
**Resultado Atual:** O sistema não processa a transação e não gera o pedido.

### 🔴 [CRÍTICO] BUG-0075 a BUG-0080 - Bloqueio de Acesso (Auth)

**Impacto:** Novos usuários não conseguem se cadastrar e usuários antigos não conseguem logar.
**Descrição:** - Ao clicar em "Create an Account", o sistema retorna **Erro 404**.

- Ao tentar logar, o sistema retorna **Erro 405 (Method Not Allowed)**.

### 🔴 [CRÍTICO] BUG-0028 - Botão "Adicionar ao Carrinho" redireciona para o Google

**Impacto:** Quebra grave de fluxo de navegação.
**Descrição:** Ao tentar comprar o produto "Casaco Longo", o botão de ação redireciona o usuário para a página externa do Google, impedindo a compra.

### 🟠 [GRAVE] BUG-0057 - Erro de Cálculo Financeiro

**Impacto:** Prejuízo financeiro ou cobrança indevida.
**Descrição:** O subtotal do carrinho não corresponde à soma dos valores unitários multiplicados pela quantidade. 
> *Ex: R$ 360,00 x 2 está gerando um valor divergente.*

### 🟡 [ACESSIBILIDADE] BUG-0022 - Navegação Inviável com Leitor de Tela

**Impacto:** Exclusão de usuários com deficiência visual.
**Descrição:** Não é possível navegar utilizando teclas de atalho (Tab/Enter) e o leitor de tela não identifica títulos de links e botões.

---

## 📉 Métricas Finais do Ciclo

O ambiente apresenta instabilidade severa em todas as camadas críticas.

| Classificação          | Quantidade  | % do Total |
| :--------------------- | :---------- | :--------- |
| **Critical / Blocker** | 30+         | ~35%       |
| **Grave**              | 30+         | ~35%       |
| **Moderada / Leve**    | 30          | ~30%       |
| **TOTAL**              | **93 Bugs** | **100%**   |

**Conclusão:** 🛑 **NO-GO**. O produto não possui condições mínimas de ir para produção devido ao bloqueio de cadastro, login e pagamentos, além de falhas graves de cálculo.

---
📫 **QA Responsável:** [Danilo Melin](https://github.com/DaniloMelin)