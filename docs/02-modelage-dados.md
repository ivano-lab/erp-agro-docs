# 📊 Modelagem de Dados — ERP Agro

Este documento descreve a modelagem atual do banco de dados do ERP Agro, com foco nas entidades centrais que compõem os módulos de gestão agrícola. A modelagem segue princípios de normalização, integridade referencial e modularidade, visando uma base sólida e escalável.

---

## 🧱 Entidades

As entidades estão organizadas por domínio funcional.

---

### 🌾 Domínio Agrícola

#### 🏡 FAZENDA

| Campo               | Tipo     | Obrigatório  | Descrição                                               |
|---------------------|----------|--------------|---------------------------------------------------------|
| `id`                | int      | ✅           | Identificador único da fazenda                          |
| `nome`              | string   | ✅           | Nome da fazenda                                         |
| `localizacao`       | string   | ✅           | Cidade, estado ou coordenadas                           |
| `hectares`          | float    | ✅           | Tamanho total em hectares                               |
| `tipo_pessoa`       | string   | ✅           | Tipo de pessoa: 'Física' ou 'Jurídica'                  |
| `cpf`               | string   | condicional  | CPF do proprietário, obrigatório se tipo_pessoa='Física'|
| `cnpj`              | string   | condicional  | CNPJ da fazenda, obrigatório se tipo_pessoa='Jurídica'  |
| `proprietario`      | string   | ❌           | Nome do responsável                                     |
| `inscricao_estadual`| string   | ❌           | Inscrição estadual, se aplicável                        |
| `razao_social`      | string   | ❌           | Razão social, se pessoa jurídica                        |
| `data_abertura`     | string   | ❌           | Data de abertura da empresa, se pessoa jurídica         |

---

#### 🧱 ÁREA

| Campo               | Tipo     | Obrigatório | Descrição                                                |
|---------------------|----------|-------------|----------------------------------------------------------|
| `id`                | int      | ✅          | Identificador único da área                              |
| `nome`              | string   | ✅          | Nome ou código interno                                   |
| `tipo_solo`         | string   | ❌          | Classificação do solo                                    |
| `hectares`          | float    | ✅          | Tamanho da área                                          |
| `fazenda_id`        | int (FK) | ✅          | Ref. à fazenda proprietária                              |

---

### 🌱 CULTURA (refatorada)

Representa o tipo de cultivo implantado em uma determinada área agrícola.

| Campo        | Tipo     | Obrigatório | Descrição                                 |
|--------------|----------|-------------|--------------------------------------------|
| `id`         | int      | ✅           | Identificador único da cultura             |
| `tipo`       | string   | ✅           | Nome do cultivo (milho, soja, arroz...)    |
| `area_id`    | int (FK) | ✅           | Referência à área onde esse cultivo ocorre |

> 🔁 A cultura pode ter várias safras ao longo do tempo.

---

### 🌾 SAFRA

Representa uma instância específica de plantio e colheita de uma determinada cultura em uma área, dentro de um período agrícola.

| Campo           | Tipo     | Obrigatório | Descrição                                 |
|------------------|----------|-------------|--------------------------------------------|
| `id`             | int      | ✅           | Identificador único da safra              |
| `cultura_id`     | int (FK) | ✅           | Referência à cultura associada            |
| `data_plantio`   | date     | ✅           | Data do plantio                           |
| `data_colheita`  | date     | ❌           | Data da colheita (real ou prevista)       |
| `observacoes`    | string   | ❌           | Anotações adicionais sobre a safra        |

---

### 🛠️ Domínio Operacional

#### 🧪 INSUMO

| Campo               | Tipo     | Obrigatório | Descrição                                                |
|---------------------|----------|-------------|----------------------------------------------------------|
| `id`                | int      | ✅          | Identificador único                                      |
| `nome`              | string   | ✅          | Nome do insumo                                           |
| `tipo`              | string   | ✅          | Categoria (fertilizante, semente, etc.)                  |
| `quantidade`        | float    | ✅          | Quantidade atual em estoque                              |
| `unidade`           | string   | ✅          | Unidade de medida (kg, L, sacas, etc.)                   |
| `descricao`         | string   | ❌          | Informações adicionais                                   |

---

#### 🛠️ ATIVIDADE

| Campo               | Tipo     | Obrigatório | Descrição                                                |
|---------------------|----------|-------------|----------------------------------------------------------|
| `id`                | int      | ✅          | Identificador único                                      |
| `tipo`              | string   | ✅          | Tipo (plantio, irrigação, colheita, etc.)                |
| `descricao`         | string   | ❌          | Detalhes da operação                                     |
| `data_execucao`     | date     | ✅          | Data de execução                                         |
| `area_id`           | int (FK) | ✅          | Ref. à área onde ocorreu                                 |
| `usuario_id`        | int (FK) | ❌          | Ref. ao usuário que registrou                            |

> 🧩 Extensível: poderá se relacionar com insumos utilizados em cada tarefa.

---

### 👤 Domínio de Acesso

#### 👤 USUÁRIO

| Campo                | Tipo     | Obrigatório | Descrição                                               |
|----------------------|----------|-------------|---------------------------------------------------------|
| `id`                 | int      | ✅          | Identificador único                                     |
| `nome`               | string   | ✅          | Nome completo                                           |
| `email`              | string   | ✅          | E-mail único                                            |
| `senha_hash`         | string   | ✅          | Hash da senha                                           |
| `perfil`             | string   | ✅          | Papel (`admin`, `produtor`, `func`)                     |

---

## 🔁 Relacionamentos

| Entidade origem      | Entidade destino | Tipo        | Descrição                                        |
|----------------------|------------------|-------------|--------------------------------------------------|
| Fazenda              | Área             | 1 : N       | Uma fazenda possui várias áreas                  |
| Área                 | Cultura          | 1 : N       | Uma área pode conter várias culturas             |
| Área                 | Atividade        | 1 : N       | Uma área pode ter várias atividades operacionais |
| Usuário              | Atividade        | 1 : N       | (opcional) Um usuário pode registrar atividades  |
| Atividade            | Insumo           | N : N (futuro) | Uma atividade pode consumir vários insumos    |
| Cultura              | Safra            | 1:N         | Uma cultura pode gerar várias safras             |



> 🔧 O relacionamento entre `ATIVIDADE` e `INSUMO` será implementado por meio de uma tabela associativa `atividade_insumo` no futuro.

---

## 🧭 Normalização e Consistência

- Todos os campos `*_id` são chaves primárias ou estrangeiras com restrições explícitas.
- A modelagem segue 3FN (Terceira Forma Normal), evitando redundância.
- Tipos de dados são genéricos para facilitar migração entre SGBDs (ex: SQLite → MySQL).
- Toda entidade pode ser estendida sem impacto nas dependentes (baixo acoplamento).

---

## 📐 Diagrama ER Visual

O diagrama visual desta modelagem está disponível em:

👉 [`diagrams/der.md`](../diagrams/der.md)

---

## 📌 Próximos passos

- Adicionar controle de estoque por safra
- Associar `ATIVIDADE` a múltiplos insumos com quantidades
- Adicionar `LOG` para rastreabilidade (auditoria leve)
- Evoluir para múltiplos usuários por fazenda com permissão por perfil

---

