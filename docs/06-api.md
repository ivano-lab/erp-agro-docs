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

{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

### 🏡 Fazendas
GET /fazendas

Retorna a lista de fazendas cadastradas.

🔸 Response

```

[
  {
    "id": 1,
    "nome": "Fazenda Boa Terra",
    "localizacao": "Palmas - TO",
    "hectares": 45.0,
    "proprietario": "José da Silva"
  }
]

```

POST /fazendas

Cadastra uma nova fazenda.

```

{
  "nome": "Fazenda Boa Terra",
  "localizacao": "Palmas - TO",
  "hectares": 45.0,
  "proprietario": "José da Silva"
}

```

PUT /fazendas/:id

Atualiza os dados de uma fazenda existente.

DELETE /fazendas/:id

Exclui uma fazenda (desde que não tenha áreas vinculadas).

### 🧱 Áreas
GET /fazendas/:fazendaId/areas

Lista as áreas de uma fazenda específica.

POST /fazendas/:fazendaId/areas

Cria uma nova área dentro de uma fazenda.

```
{
  "nome": "Área A1",
  "tipo_solo": "Arenoso",
  "hectares": 10.5
}

```

### 🌱 Culturas

GET /areas/:areaId/culturas

Retorna as culturas cadastradas em uma área.

POST /areas/:areaId/culturas

Cria uma cultura vinculada à área.

```

{
  "tipo": "Milho"
}

```

### 🌾 Safras

GET /culturas/:culturaId/safras

Lista todas as safras associadas à cultura.

POST /culturas/:culturaId/safras

Registra uma nova safra.

```

{
  "data_plantio": "2025-02-15",
  "data_colheita": "2025-06-20",
  "observacoes": "Plantio com atraso devido à seca."
}

```
