# 📋 Requisitos do Sistema — ERP Agro

Este documento apresenta os **requisitos funcionais e não funcionais** do ERP Agro, organizados por módulo, com base na modelagem de dados e nos objetivos do sistema.

---

## ✅ Requisitos Funcionais

Requisitos divididos por entidade e fluxo principal.

---

### 🏡 Módulo Fazenda

- RF001: O sistema deve permitir o cadastro de uma nova fazenda com nome, localização, tamanho e proprietário.
- RF002: O sistema deve listar todas as fazendas cadastradas.
- RF003: O sistema deve permitir a edição dos dados de uma fazenda existente.
- RF004: O sistema deve permitir a exclusão de uma fazenda.

---

### 🧱 Módulo Área

- RF005: O sistema deve permitir o cadastro de áreas vinculadas a uma fazenda.
- RF006: O sistema deve listar todas as áreas de uma fazenda.
- RF007: O sistema deve permitir a edição dos dados de uma área.
- RF008: O sistema deve permitir a exclusão de uma área, desde que não esteja vinculada a culturas ou atividades.

---

### 🌱 Módulo Cultura

- RF009: O sistema deve permitir o registro de culturas vinculadas a uma área.
- RF010: O sistema deve listar todas as culturas de uma área.
- RF011: O sistema deve permitir a edição de uma cultura (tipo, etc.).
- RF012: O sistema deve permitir a exclusão de uma cultura, desde que não esteja vinculada a safras.

---

### 🌾 Módulo Safra

- RF013: O sistema deve permitir o cadastro de uma nova safra vinculada a uma cultura.
- RF014: O sistema deve armazenar a data de plantio, data prevista ou real de colheita e observações da safra.
- RF015: O sistema deve listar todas as safras de uma cultura específica.
- RF016: O sistema deve permitir editar e excluir uma safra.

---

### 🧪 Módulo Insumo

- RF017: O sistema deve permitir o cadastro de insumos com nome, tipo, quantidade e unidade.
- RF018: O sistema deve listar todos os insumos disponíveis.
- RF019: O sistema deve permitir atualizar a quantidade em estoque.
- RF020: O sistema deve permitir excluir um insumo, desde que não esteja vinculado a atividades.

---

### 🛠️ Módulo Atividade

- RF021: O sistema deve permitir o registro de uma atividade agrícola (plantio, colheita, irrigação, etc.) vinculada a uma área.
- RF022: O sistema deve armazenar data, tipo e descrição da atividade.
- RF023: O sistema deve permitir listar atividades por área e por período.
- RF024: O sistema deve permitir vincular um usuário à atividade.
- RF025: (futuro) O sistema deve permitir vincular múltiplos insumos usados em uma atividade, com suas quantidades.

---

### 👤 Módulo Usuário

- RF026: O sistema deve permitir o cadastro de usuários com nome, e-mail, senha e perfil.
- RF027: O sistema deve autenticar o usuário por e-mail e senha.
- RF028: O sistema deve proteger rotas e recursos com base no perfil do usuário.
- RF029: O sistema deve permitir listar e editar usuários (admin).
- RF030: O sistema deve registrar qual usuário executou cada atividade (quando aplicável).

---

## 🔒 Requisitos Não Funcionais

| ID    | Descrição |
|-------|-----------|
| RNF001 | O sistema deve responder às requisições com tempo inferior a 2 segundos em 90% dos casos. |
| RNF002 | As senhas dos usuários devem ser armazenadas de forma criptografada. |
| RNF003 | O sistema deve seguir boas práticas REST na organização das rotas. |
| RNF004 | As operações de banco de dados devem respeitar integridade referencial. |
| RNF005 | O sistema deve ser capaz de migrar do SQLite para PostgreSQL sem perda de dados. |
| RNF006 | O frontend deve estar desacoplado da lógica de negócio (arquitetura MVC ou API). |
| RNF007 | O sistema deve estar preparado para multiusuário e autenticação por token (JWT ou similar). |

---

## ⚠️ Restrições e Regras de Negócio

- Uma área só pode ser excluída se **não tiver culturas nem atividades vinculadas**.
- Uma cultura só pode ser excluída se **não tiver nenhuma safra registrada**.
- Um insumo não pode ser excluído se estiver **vinculado a atividades** (futuro).
- Cada usuário terá um **perfil** com permissões diferentes (`admin`, `produtor`, `func`).
- O sistema **não deve permitir edições em atividades ou safras retroativas** após determinado período (regra configurável no futuro).

---

## 📌 Observações

- A versão inicial do sistema se concentra em **registro e visualização** de dados.
- Funcionalidades como **dashboard, relatórios, análises históricas e integração com sensores** podem ser incorporadas nas próximas fases.

---
