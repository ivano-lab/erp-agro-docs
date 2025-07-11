# 📐 Diagrama ER — ERP Agro 

Este diagrama representa a modelagem de dados inicial do ERP Agro, com foco nas entidades principais: **Fazenda**, **Área** e **Cultura**.

> Renderizado automaticamente via Mermaid no GitHub.  
> Última atualização: 2025-07-08

---

```mermaid
erDiagram
    FAZENDA ||--o{ AREA : possui
    AREA ||--o{ CULTURA : contem

    FAZENDA {
        int id
        string nome
        string localizacao
        float hectares
        string proprietario
    }

    AREA {
        int id
        string nome
        string tipo_solo
        float hectares
        int fazenda_id
    }

    CULTURA {
        int id
        string tipo
        date data_plantio
        date data_colheita
        int area_id
    }

    INSUMO {
        int id
        string nome
        string tipo
        float quantidade
        string unidade
        string descricao
    }

    ATIVIDADE {
        int id
        string tipo
        string descricao
        date data_execucao
        int (FK) area_id
        int (FK) usuario_id
    }
