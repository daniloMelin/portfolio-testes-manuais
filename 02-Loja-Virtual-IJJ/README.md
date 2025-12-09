# 🛒 Projeto: Loja Virtual - Instituto Joga Junto (v1.0)

## 📌 Visão Geral

**Contexto:** Validação da versão 1.0 da Loja Virtual do Instituto Joga Junto. O foco deste projeto foi além do funcional, garantindo a qualidade técnica de uma aplicação monolítica hospedada na **AWS**, com ênfase em **Performance (Google Lighthouse)** e **Experiência Mobile**.

**Objetivo:** Validar fluxos críticos de negócio (Navegação, Cadastro, Compra) e assegurar que a aplicação seja rápida e acessível em diferentes dispositivos.

**Arquitetura e Ambiente:**

- **Stack:** Python (Monólito), HTML, CSS, JS.
- **Infraestrutura:** AWS (Cloud Computing).
- **Ambiente de Teste:** `https://lojaqa.jogajuntoinstituto.com/`

**Ferramentas Utilizadas:**

- **Gestão de Testes:** BDD (Gherkin).
- **Performance:** Google Lighthouse (Mobile & Desktop).
- **Compatibilidade:** Cross-browser (Chrome, Edge, Firefox) e Mobile (Android 10+).
- **Inspeção:** Chrome DevTools.

---

## 🗺️ Estratégia de Teste

A estratégia combinou **Testes Funcionais** (jornada do usuário) com uma auditoria de **Testes Não-Funcionais** (métricas de qualidade técnica).

**Cobertura:**

- ✅ **Usabilidade:** Navegação responsiva e acessibilidade.
- ✅ **Funcional:** Ciclo de vida do pedido (Cadastro -> Carrinho -> Pagamento).
- ✅ **Performance:** Análise de tempo de carregamento e boas práticas Web.

---

## 🧪 Cenários de Teste (Destaques)

Os testes utilizaram a sintaxe Gherkin para alinhar requisitos.

| ID          | Funcionalidade     | Cenário Resumido             | Resultado Esperado                            |
| :---------- | :----------------- | :--------------------------- | :-------------------------------------------- |
| **NAV-008** | **Responsividade** | Acessar via Mobile (Android) | Menu e layout devem se adaptar sem quebra.    |
| **CRC-001** | **Carrinho**       | Adicionar/Remover itens      | Subtotal deve ser recalculado em tempo real.  |
| **PG-002**  | **Pagamento**      | Cartão Inválido              | Sistema deve rejeitar e exibir erro amigável. |
| **CC-004**  | **Cadastro**       | E-mail Duplicado             | Bloquear criação de conta duplicada.          |

---

## 📊 Relatório de Performance (Google Lighthouse)

Foi realizada uma auditoria técnica completa. Os resultados apontam uma **discrepância crítica** entre Desktop e Mobile.

### 🖥️ Desktop (Resultados)

| Métrica            | Pontuação | Status  |
| :----------------- | :-------- | :------ |
| **SEO**            | **82**    | 🟢 Bom   |
| **Acessibilidade** | **77**    | 🟡 Médio |
| **Performance**    | **76**    | 🟡 Médio |

### 📱 Mobile (Resultados Críticos)

| Métrica            | Pontuação | Status        |
| :----------------- | :-------- | :------------ |
| **SEO**            | **82**    | 🟢 Bom         |
| **Acessibilidade** | **79**    | 🟡 Médio       |
| **Performance**    | **44**    | 🔴 **Crítico** |

---

## 📉 Recomendações Técnicas (QA Insights)

Com base na auditoria, foram sugeridas as seguintes melhorias para a equipe de engenharia:

1. **Otimização Mobile (Performance):**
   * O tempo de carregamento (LCP) é de 14.4s no mobile.
   * **Ação:** Implementar *Lazy Loading* para imagens e ativar compressão de texto (Gzip).

2. **Segurança (HTTPS):**
   * Detectadas 51 requisições não seguras (HTTP).
   * **Ação:** Forçar redirecionamento HTTPS no servidor AWS.

3. **Acessibilidade:**
   * Imagens sem texto alternativo (`alt`) e baixo contraste.
   * **Ação:** Revisão de tags HTML para conformidade WCAG.

---
📫 **QA Responsável:** [Danilo Melin](https://github.com/DaniloMelin) | **Squad:** 7 - QAvengers
