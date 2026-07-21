## 📋 Matriz Detalhada de Casos de Teste

### 1. `POST /api/v1/courier` — Criação de Entregador

| ID | Caso de Teste | Dados de Entrada (Payload JSON) | Resultado Esperado | Resultado Real | Status | Bug Jira |
| :---: | :--- | :--- | :--- | :--- | :---: | :---: |
| **1** | Login com 2 caracteres | `{"login": "LS", "password": "1234", "firstName": "saske"}` | `201 Created` | `201 Created` | ✅ **Aprovado** | - |
| **2** | Login com 1 caractere | `{"login": "L", "password": "1234", "firstName": "saske"}` | `409 Login inválido` | `201 Created` | ❌ **Failed** | `RB9ST3-9` |
| **3** | Login vazio ou ausente | `{"login": "", "password": "1234", "firstName": "saske"}` | `400 Sem dados suficientes` | `400 Sem dados suficientes` | ✅ **Aprovado** | - |
| **4** | Login com 10 caracteres | `{"login": "Rodrigomon", "password": "1234", "firstName": "Rodrigo"}` | `201 Created` | `201 Created` | ✅ **Aprovado** | - |
| **5** | Login com 11 caracteres | `{"login": "Rodrigomon0", "password": "1234", "firstName": "Rodrigo"}` | `409 Login inválido` | `201 Created` | ❌ **Failed** | `RB9ST3-10` |
| **6** | Login com símbolos | `{"login": "R()dr|go", "password": "1234", "firstName": "Rodrigo"}` | `409 Login inválido` | `201 Created` | ❌ **Failed** | `RB9ST3-11` |
| **7** | Login já existente | `{"login": "ninja", "password": "1235", "firstName": "naruto"}` | `409 Login indisponível` | `409 Login indisponível` | ✅ **Aprovado** | - |
| **8** | `firstName` com 2 caracteres | `{"login": "ninjaa", "password": "1239", "firstName": "SU"}` | `201 Created` | `201 Created` | ✅ **Aprovado** | - |
| **9** | `firstName` com 1 caractere | `{"login": "ninjaa", "password": "1239", "firstName": "S"}` | `409 Nome inválido` | `201 Created` | ❌ **Failed** | `RB9ST3-12` |
| **10** | `firstName` com 10 caracteres | `{"login": "ninjaaa", "password": "1239", "firstName": "Saske Uchi"}` | `201 Created` | `201 Created` | ✅ **Aprovado** | - |
| **11** | `firstName` com 11 caracteres | `{"login": "ninjaaa", "password": "1239", "firstName": "Saske Uchih"}` | `409 Nome inválido` | `201 Created` | ❌ **Failed** | `RB9ST3-13` |
| **12** | `firstName` já existente | `{"login": "nindja", "password": "1235", "firstName": "saske"}` | `201 Created` | `201 Created` | ✅ **Aprovado** | - |
| **13** | Sem campo `firstName` | `{"login": "hunter1", "password": "1234"}` | `201 Created` | `201 Created` | ✅ **Aprovado** | - |
| **14** | `password` com letras | `{"login": "hunter", "password": "abcd", "firstName": "Gon"}` | `409 Senha inválida` | `201 Created` | ❌ **Failed** | `RB9ST3-7` |
| **15** | `password` com 3 caracteres | `{"login": "hunter1", "password": "321", "firstName": "Killua"}` | `409 Senha inválida` | `201 Created` | ❌ **Failed** | `RB9ST3-8` |
| **16** | `password` com 5 caracteres | `{"login": "Ininja", "password": "12354", "firstName": "Saske"}` | `409 Senha inválida` | `201 Created` | ❌ **Failed** | `RB9ST3-14` |
| **17** | `password` vazio | `{"login": "hunter", "password": "", "firstName": "Rodrigo"}` | `400 Sem dados suficientes` | `400 Sem dados suficientes` | ✅ **Aprovado** | - |

---

### 2. `DELETE /api/v1/courier/:id` — Exclusão de Entregador

| ID | Caso de Teste | Corpo da Solicitação / Parâmetros | Resultado Esperado | Resultado Real | Status | Bug Jira |
| :---: | :--- | :--- | :--- | :--- | :---: | :---: |
| **1** | Excluir entregador existente | `{"id": "1"}` | `200 Ok` | `200 Ok` | ✅ **Aprovado** | - |
| **2** | Excluir entregador inexistente | `{"id": "9"}` | `404 Nenhum Entregador com este ID` | `404 Nenhum Entregador com este ID` | ✅ **Aprovado** | - |
| **3** | Excluir com ID inválido (string) | `{"id": "a"}` | `500 Inserção inválida` | `500 Inserção inválida` | ✅ **Aprovado** | - |
| **4** | Excluir sem ID no corpo | *Ausente / Nulo* | `400 Requisição inválida` | `200 Ok` | ❌ **Failed** | `RB9ST3-15` |

---

## 🐛 Mapeamento de Bugs (Jira)

Abaixo estão os defeitos identificados durante a execução da suíte de testes e cadastrados no Jira:

| Ticket Jira | Módulo / Rota | Problema Encontrado | Gravidade / Impacto |
| :--- | :--- | :--- | :--- |
| **`RB9ST3-7`** | `POST /courier` | API aceita senhas compostas apenas por letras (`"abcd"`). | Alta (Validação de Senha) |
| **`RB9ST3-8`** | `POST /courier` | API aceita senhas de 3 caracteres (abaixo do limite mínimo). | Média |
| **`RB9ST3-9`** | `POST /courier` | API aceita login com apenas 1 caractere (`"L"`). | Média |
| **`RB9ST3-10`** | `POST /courier` | API aceita login acima do limite de 10 caracteres (`"Rodrigomon0"`). | Média |
| **`RB9ST3-11`** | `POST /courier` | API aceita login contendo caracteres especiais/símbolos (`"R()dr\|go"`). | Média |
| **`RB9ST3-12`** | `POST /courier` | API aceita `firstName` com apenas 1 caractere (`"S"`). | Baixa |
| **`RB9ST3-13`** | `POST /courier` | API aceita `firstName` acima de 10 caracteres (`"Saske Uchih"`). | Baixa |
| **`RB9ST3-14`** | `POST /courier` | API aceita senhas fora da regra de formato esperado (5 caracteres numericos sem validação). | Média |
| **`RB9ST3-15`** | `DELETE /courier` | Requisição DELETE sem ID no corpo retorna status `200 OK` em vez de `400 Bad Request`. | Alta (Segurança / Consistência) |

---

## 📁 Estrutura do Arquivo de Dados

O arquivo Excel `Quality Assurance for API PT-BR.xlsx` é composto por duas abas (sheets):

1. **`Project info`**:
   - Informações gerais sobre a versão do projeto (`Project Version: 1.2`).
2. **`Caso de Teste - API`**:
   - Tabela principal contendo as colunas:
     - `ID`: Identificador do caso de teste dentro da rota.
     - `Caso de teste`: Descrição resumida da regra a ser testada.
     - `Pré-condição`: Estado necessário da aplicação (ex: *Iniciar o Servidor*).
     - `Etapas do teste`: Rota/Método HTTP executado.
     - `Dados de teste (corpo da solicitação)`: Body JSON enviado no request.
     - `Resultado esperado`: Resposta e status code HTTP definidos na especificação.
     - `Resultado real`: Resposta e status code HTTP obtidos durante a execução.
     - `Status`: Resultado final (`Aprovado` / `Failed`).
     - `Link de bug do Jira`: Código do ticket cadastrado na ferramenta de gerenciamento.

---

## 🚀 Como Executar e Validar os Testes

1. **Pré-requisitos:**
   - Servidor da API em execução (`http://localhost:8080` ou URL equivalente de Staging/QA).
   - Cliente HTTP (Postman, Insomnia) ou script de testes automatizados (Jest, Supertest, PyTest, Newman).

2. **Exemplo de Execução via cURL:**

   *Criar Entregador:*
   ```bash
   curl -X POST http://localhost:8080/api/v1/courier \\
     -H "Content-Type: application/json" \\
     -d '{
           "login": "LS",
           "password": "1234",
           "firstName": "saske"
         }'
