# 📊 Modelagem de Dados — ERP Agro

Este documento descreve a modelagem inicial do banco de dados do ERP Agro, com foco nas três entidades principais que compõem o núcleo da aplicação: **Fazenda**, **Área** e **Cultura**.

---

## 🧱 Entidades e Atributos

### 🏡 FAZENDA

Representa uma propriedade rural gerenciada pelo sistema.

| Campo          | Tipo     | Obrigatório | Descrição                                 |
|----------------|----------|-------------|--------------------------------------------|
| `id`           | int      | ✅           | Identificador único da fazenda             |
| `nome`         | string   | ✅           | Nome da fazenda                            |
| `localizacao`  | string   | ✅           | Cidade, estado ou coordenadas aproximadas  |
| `hectares`     | float    | ✅           | Tamanho total em hectares                  |
| `proprietario` | string   | ❌           | Nome do responsável                        |

---

### 🌾 ÁREA

Refere-se a uma subdivisão física de uma fazenda, utilizada para fins de plantio ou manejo diferenciado.

| Campo         | Tipo     | Obrigatório | Descrição                                  |
|---------------|----------|-------------|---------------------------------------------|
| `id`          | int      | ✅           | Identificador único da área                |
| `nome`        | string   | ✅           | Nome ou código interno da área             |
| `tipo_solo`   | string   | ❌           | Classificação ou tipo predominante do solo |
| `hectares`    | float    | ✅           | Tamanho da área em hectares                |
| `fazenda_id`  | int (FK) | ✅           | Referência à fazenda à qual pertence       |

---

### 🌱 CULTURA

Corresponde ao tipo de cultivo realizado em uma área durante um período específico.

| Campo           | Tipo     | Obrigatório | Descrição                                   |
|-----------------|----------|-------------|----------------------------------------------|
| `id`            | int      | ✅           | Identificador único da cultura              |
| `tipo`          | string   | ✅           | Tipo de cultivo (milho, soja, etc.)         |
| `data_plantio`  | date     | ✅           | Data prevista ou real de plantio            |
| `data_colheita` | date     | ❌           | Data prevista ou real de colheita           |
| `area_id`       | int (FK) | ✅           | Referência à área onde está sendo cultivada |

---

## 🔁 Relacionamentos entre entidades

| Entidade origem | Entidade destino | Tipo de relação    | Descrição                                                |
|------------------|------------------|---------------------|-----------------------------------------------------------|
| Fazenda          | Área             | 1:N (um para muitos) | Uma fazenda pode conter várias áreas                     |
| Área             | Cultura          | 1:N (um para muitos) | Uma área pode abrigar várias culturas (em safras distintas) |

---

## 🧭 Normalização e Consistência

- As tabelas estão normalizadas até a 3FN.
- Os campos `*_id` são chaves estrangeiras que garantem integridade referencial.
- Cada entidade é projetada para ser independente e reutilizável em diferentes contextos de operação.

---

## 🖼️ Diagrama ER

O diagrama visual dessa modelagem está disponível no diretório `diagrams/`:

👉 [Visualizar Diagrama ER (Mermaid)](../diagrams/der.md)

---

## 📝 Próximas entidades planejadas

As próximas entidades a serem modeladas são:

- **INSUMO**: controle de recursos utilizados no plantio e manejo
- **ATIVIDADE**: tarefas operacionais realizadas nas áreas (ex: plantio, irrigação, colheita)
- **USUÁRIO**: sistema de autenticação e controle de acesso

Essas entidades serão incorporadas ao modelo à medida que os módulos forem implementados.

---
