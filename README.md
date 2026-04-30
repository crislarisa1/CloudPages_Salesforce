# CloudPages

Repositório com exemplos práticos de CloudPages desenvolvidas no Salesforce Marketing Cloud, organizadas por branches, cada uma representando um caso de uso específico dentro de CRM e marketing automation.

---

## Estrutura

Cada Cloud Page está isolada em uma branch própria, permitindo versionamento independente, organização por contexto de negócio e reutilização de componentes.

---

## Cloud Pages

### 1. Inscrição

Landing page focada em captação de leads.

* Captura email via formulário
* Valida duplicidade com `LookupRows`
* Insere dados com `UpsertDE`
* Gera subscriber key
* Exibe mensagens dinâmicas (novo vs existente)

**Objetivo:** construção de base de dados e entrada de contactos no ecossistema CRM.

---

### 2. Mensagem Personalizada

Landing page interativa para envio de mensagens entre utilizadores.

* Captura dados do remetente e destinatário
* Permite seleção de mensagens pré-definidas
* Valida inputs obrigatórios
* Insere dados com `InsertData`
* Preparada para integração com Journey Builder

**Objetivo:** ativação de campanhas emocionais e triggers de comunicação personalizada.

---

## Tecnologias

* AMPscript
* HTML5
* CSS
* JavaScript
* Salesforce Marketing Cloud

---

## Objetivo do Repositório

* Centralizar implementações de CloudPages
* Servir como portfólio técnico
* Demonstrar boas práticas de CRM e marketing automation
* Facilitar reutilização e escalabilidade de soluções

---
