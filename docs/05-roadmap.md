# 🗺️ Roadmap de Desenvolvimento — ERP Agro

Este documento descreve a trajetória planejada para o desenvolvimento do ERP Agro, dividida em fases progressivas e com foco em entregas incrementais de valor.

---

## 🎯 Objetivo do Projeto

Criar um sistema modular, robusto e acessível para o gerenciamento de propriedades rurais de pequeno e médio porte, priorizando funcionalidades essenciais na primeira fase e mantendo arquitetura escalável para evoluções futuras.

---

## 🚀 Fase 1 — MVP (Produto Mínimo Viável)

### 🧩 Escopo
- Cadastro e listagem de fazendas
- Cadastro e listagem de áreas por fazenda
- Cadastro de culturas e safras
- Registro de atividades operacionais
- Autenticação básica de usuários

### 🛠️ Funcionalidades
- [ ] CRUD completo de Fazenda
- [ ] CRUD completo de Área
- [ ] CRUD de Cultura + Safra normalizada
- [ ] Registro de Atividade (sem insumos ainda)
- [ ] CRUD de Usuário (com login e hash de senha)
- [ ] API REST documentada e funcional
- [ ] Banco de dados em SQLite (modo dev)
- [ ] Frontend HTML/CSS/JS básico (public/)

---

## ⚙️ Fase 2 — Funcionalidades intermediárias

### 🔄 Funcionalidades planejadas
- [ ] Estoque de insumos
- [ ] Relacionamento N:N entre Atividades e Insumos
- [ ] Relatórios por fazenda, área, safra e usuário
- [ ] Dashboard básico (produtividade, insumos, atividades)
- [ ] Exportação de dados (CSV, PDF)

---

## 🌐 Fase 3 — Escalabilidade e Integrações

### 📈 Evoluções estratégicas
- [ ] Migração para PostgreSQL
- [ ] Autenticação por token (JWT)
- [ ] Controle de permissões por perfil de usuário
- [ ] API externa (ex: integração com sensores ou clima)
- [ ] Integração com frontend SPA (React ou Vue)
- [ ] Containerização com Docker
- [ ] Testes automatizados (Jest ou similar)
- [ ] CI/CD (GitHub Actions)

---

## 📝 Histórico de Marcos

| Data       | Evento                            |
|------------|------------------------------------|
| 2025-07-08 | Início da fase de documentação    |
| 2025-07-09 | Finalizada modelagem de dados     |
| 2025-07-10 | Definida estrutura modular de API |
| (em aberto)| Início da codificação do módulo Fazenda |

---

## 📌 Observações

- As fases podem se sobrepor ou ter ajustes conforme necessidades identificadas durante o desenvolvimento.
- Este roadmap será mantido atualizado com o avanço real do projeto.

---
