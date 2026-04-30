# CloudPages

# Cloud Page 1: Inscrição

## Descrição

Landing page desenvolvida no Salesforce Marketing Cloud para captação de emails, armazenamento em Data Extension e exibição de mensagens dinâmicas conforme o estado do utilizador.

---

## Funcionamento

* Captura o email via formulário
* Verifica se já existe na base (`LookupRows`)
* Se novo:

  * Insere com `UpsertDE`
  * Gera subscriber key
  * Regista data/hora
  * Exibe mensagem de sucesso
* Se já existir:

  * Não insere novamente
  * Exibe mensagem alternativa
* Controla exibição do formulário via variável (`@exibir_form`)

---

## AMPscript (Resumo)

```ampscript
SET @email = RequestParameter('email')
SET @jaExiste = LookupRows("DEX_LP_INSCRICAO","email",@email)

IF NOT EMPTY(@email) AND RowCount(@jaExiste) == 0 THEN
  UpsertDE(...)
  SET @exibir_form = "false"

ELSEIF RowCount(@jaExiste) > 0 THEN
  SET @exibir_form = "false"
ENDIF
```

---

## HTML

* Formulário submete para a própria página
* Conteúdo é renderizado dinamicamente com AMPscript

```ampscript
%%[ IF @exibir_form == "false" THEN ]%%
  %%=v(@mensagem)=%%
%%[ ELSE ]%%
  <!-- formulário -->
%%[ ENDIF ]%%
```

---

## Data Extension

**Nome:** `DEX_LP_INSCRICAO`

| Campo               | Tipo |
| ------------------- | ---- |
| email               | Text |
| nova_subscriber_key | Text |
| data_resp           | Date |

---

## Notas

* Evita duplicidade de leads
* Estrutura simples e reutilizável
* Preparada para integração com jornadas e CRM
