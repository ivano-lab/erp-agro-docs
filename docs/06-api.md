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

### 🧪 Insumos
GET /insumos

Lista todos os insumos disponíveis no estoque.

POST /insumos

Adiciona um novo insumo ao sistema.

```

{
  "nome": "NPK 4-14-8",
  "tipo": "Fertilizante",
  "quantidade": 200,
  "unidade": "kg",
  "descricao": "Uso em pré-plantio de milho"
}

```

### 🛠️ Atividades

GET /areas/:areaId/atividades

Lista atividades realizadas em uma área.

POST /areas/:areaId/atividades

Cadastra uma nova atividade operacional.

```

{
  "tipo": "Plantio",
  "descricao": "Plantio da safra 2025 de milho",
  "data_execucao": "2025-02-15",
  "usuario_id": 1
}

```

### 👤 Usuários

GET /usuarios

Lista os usuários (admin).

POST /usuarios

Cadastra um novo usuário.

```

{
  "nome": "Maria Oliveira",
  "email": "maria@exemplo.com",
  "senha": "senhaSegura123",
  "perfil": "produtor"
}

```

### 📌 Considerações

Todos os endpoints que alteram dados (POST, PUT, DELETE) exigem token JWT válido.

Os dados devem ser enviados em application/json.

As respostas seguem padrão HTTP com status 200, 201, 400, 401, 403, 404 e 500 conforme o caso.

### 🔜 Próximos contratos (futuro)

Relacionamento entre atividades e insumos (atividade_insumo)

Rotas de relatórios e exportações

API para consultas temporais e comparações históricas

