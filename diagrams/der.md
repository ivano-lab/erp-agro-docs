# 📐 Diagrama ER — ERP Agro 

Este diagrama representa a modelagem de dados do ERP Agro, com foco nas entidades principais: **Fazenda**, **Área**, **Cultura**, **Insumo** e **Atividade**.

> Renderizado automaticamente via Mermaid no GitHub.  
> Última atualização: 2025-07-08

---

```mermaid
erDiagram
    FAZENDA   ||--o{ AREA : possui
    AREA      ||--o{ CULTURA : contem
    AREA      ||--o{ ATIVIDADE : executa
    CULTURA   ||--o{ SAFRA : gera
    USUARIO   ||--o{ ATIVIDADE : registra
    ATIVIDADE ||--o{ ATIVIDADE_INSUMO : possui
    INSUMO    ||--o{ ATIVIDADE_INSUMO : utilizado_em
    
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
        int area_id
    }

    SAFRA {
        int id
        int cultura_id
        date data_plantio
        date data_colheita
        string observacoes
    }

    INSUMO {
        int id
        string nome
        string tipo
        float quantidade
        string unidade
        string descricao
        string fornecedor
        date validade
        float custo_unitario            
    }

    ATIVIDADE {
        int id
        string tipo
        string descricao
        date data_execucao
        datetime data_criacao
        datetime ultima_atualizacao
        string status
        int area_id
        int usuario_id
    }

    USUARIO {
        int id
        string nome
        string email
        string senha_hash
        string perfil    
    }
