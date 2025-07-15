# 🌐 Contratos de API — ERP Agro

Este documento descreve os principais endpoints RESTful da API do ERP Agro. A estrutura segue boas práticas REST, com métodos claros, recursos bem definidos e uso de status HTTP adequados.

> 🔒 Algumas rotas exigem autenticação e autorização baseada no perfil do usuário (`admin`, `produtor`, `func`).

---

## 🔐 Autenticação

### `POST /auth/login`

Autentica o usuário e retorna um token JWT.

#### 🔸 Request (JSON)

```json
{
  "email": "usuario@exemplo.com",
  "senha": "senha123"
}

