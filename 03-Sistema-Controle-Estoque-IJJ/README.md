# 📦 Projeto: Sistema de Controle de Estoque - IJJ

## 📌 Visão Geral

**Contexto:** Validação da qualidade do Sistema de Controle de Estoque do Instituto Joga Junto. O projeto seguiu rigorosamente normas de engenharia de software (**ISO/IEC 29119** e **ISO/IEC 25010**) para garantir que o produto atenda aos requisitos funcionais (RF) e não funcionais (NF).

**Objetivo:** Assegurar a integridade dos módulos de cadastro de usuários, gestão de produtos, autenticação e atualização de estoque em tempo real via API REST e Interface Web.

**Arquitetura:**
Aplicação Web em nuvem com Backend API REST documentada via Swagger. Integração entre módulos de Vendas, Financeiro e Estoque.

**Ferramentas e Tecnologias:**

- **Planejamento:** ISO/IEC 29119-4 (Técnicas de Teste).
- **API Testing:** Postman (Validação de Status Code, Payload e Segurança).
- **Gestão de Bugs:** Google Sheets / Jira.
- **Tipos de Teste:** Funcional (Manual), Exploratório, API, Usabilidade e Segurança.

---

## 🗺️ Estratégia de Teste

A estratégia foi baseada em riscos e prioridades, utilizando técnicas de **Caixa Preta**, **Particionamento de Equivalência** e **Análise de Valor Limite**.

**Cobertura de Requisitos (Destaques):**

- ✅ **RF002 - Autenticação:** Login, restrições de acesso e segurança de credenciais.
- ✅ **RF004/RF005 - CRUD de Produtos:** Cadastro, edição e validação de campos obrigatórios.
- ✅ **RF010 - Estoque em Tempo Real:** Atualização automática pós-transação.
- ✅ **NF004 - Usabilidade:** Adaptação a temas (Dark Mode) e Responsividade Mobile.

---

## 🧪 Cenários de Teste Executados

Abaixo, uma amostra dos cenários críticos validados:

| ID | Funcionalidade | Cenário | Resultado Esperado | Status |
| :--- | :--- | :--- | :--- | :--- |
| **API-024** | **Segurança** | Deletar produto sem token de autenticação | API deve retornar `401 Unauthorized`. | ❌ Falhou (BUG Crítico) |
| **LOG-003** | **Login** | Autenticar com senha incorreta | Sistema deve exibir mensagem de erro e não logar. | ❌ Falhou (Erro 200 OK) |
| **PRD-006** | **Regra de Negócio** | Cadastro de produto com preço zero | Sistema deve bloquear e exibir erro. | ❌ Falhou |
| **NF-0005** | **Interface** | Alternância de Tema (Dark Mode) | UI deve adaptar cores imediatamente. | ❌ Falhou |

---

## 🐞 Bugs Reportados (Top Defeitos)

Foram identificados **60 bugs** no total, com alta criticidade na camada de API e Segurança.

### 🔴 [CRÍTICO] API: Falha Grave de Segurança (Broken Access Control)

**Bug Relacionado:** API-024 / BUG-046
**Descrição:** O endpoint `DELETE /{produtoId}` permite a exclusão de produtos sem exigir token de autenticação.
**Impacto:** Qualquer usuário anônimo consegue apagar registros do banco de dados.
**Evidência Técnica:**

```json
// Request: DELETE /produtos/999 (Sem Header Authorization)
// Response Recebido:
Status: 200 OK
{ "message": "Produto deletado" }
```

### 🔴 [CRÍTICO] API: Retorno 200 OK para Login Falho

**Bug Relacionado:** LOG-003 / BUG-047
**Descrição:** Ao enviar credenciais inválidas (senha errada), a API retorna status `200 OK` em vez de `401 Unauthorized`, mascarando a falha de autenticação.

### 🟠 [GRAVE] Integração: Falha em Webhooks

**Bug Relacionado:** NF-0008 / BUG-007
**Descrição:** O cadastro de produtos não está disparando as chamadas HTTP obrigatórias para os sistemas de Vendas e Financeiro, quebrando a integridade dos dados entre sistemas.

### 🟡 [MÉDIO] UI: Inconsistência Visual (Dark Mode)

**Bug Relacionado:** NF-0004 / BUG-003
**Descrição:** A aplicação não respeita a configuração de tema do navegador ou o switch manual, mantendo elementos visuais desconfigurados.

---

## 📉 Conclusão e Recomendações (QA Insights)

O ciclo de testes indicou que o sistema **NÃO está apto para produção (No-Go)** devido a falhas de segurança bloqueantes.

**Principais Gaps Identificados:**

1. **Segurança da API:** Implementar validação obrigatória de JWT em todas as rotas de escrita/deleção.
2. **Padrão REST:** Corrigir os Status Codes para refletir erros reais (4xx/5xx).
3. **Validação de Input:** Impedir cadastro de valores negativos ou zerados em regras de negócio críticas.

---

📫 **QA Responsável:** [Danilo Melin](https://github.com/DaniloMelin) | **Squad:** MaQAcos
