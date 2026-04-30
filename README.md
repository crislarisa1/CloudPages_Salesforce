# CloudPages

# Cloud Page 2: Mensagem Personalizada

## Descrição

Cloud Page desenvolvida no Salesforce Marketing Cloud para envio de mensagens personalizadas entre utilizadores, com armazenamento em Data Extension e integração com Journey Builder.

---

## Funcionamento

* Captura dados do formulário:

  * Email remetente
  * Email destinatário
  * Nome de quem envia
  * Nome de quem recebe
  * Mensagem selecionada

* Valida se os campos obrigatórios estão preenchidos

* Se inválido:

  * Exibe mensagem de erro

* Se válido:

  * Insere registo na Data Extension (`InsertData`)
  * Gera Subscriber Key
  * Regista data/hora
  * Prepara envio via Journey Builder
  * Exibe mensagem de sucesso

---

## AMPscript

```ampscript
SET @submitted = RequestParameter('submitted')

IF @submitted == "true" THEN

  IF EMPTY(@emailDestinatario) OR EMPTY(@emailRemetente) OR EMPTY(@mensagemCard) THEN
    SET @mensagemErro = "Erro"
  ELSE

    SET @insertStatus = InsertData(...)

    IF @insertStatus > 0 THEN
      SET @mensagemSucesso = "Sucesso"
    ELSE
      SET @mensagemErro = "Erro"
    ENDIF

  ENDIF

ENDIF
```

---

## HTML

* Formulário com envio para a própria página
* Campo hidden para controlo de submissão
* Campo hidden para armazenar mensagem selecionada

```html
<form action="%%=RequestParameter('PAGEURL')=%%" method="post">
```

---

## Interação (Frontend)

* Seleção de mensagens via cards
* Ao clicar:

  * Aplica estilo visual (seleção)
  * Preenche campo hidden (`mensagemCard`)
  * Ativa botão de envio

```javascript
function selectCard(element) {
  const text = element.querySelector('.card-text').innerText;
  document.getElementById('selectedMessage').value = text;
  document.getElementById('submitBtn').disabled = false;
}
```

---

## Renderização Condicional

```ampscript
%%[ IF NOT EMPTY(@mensagemSucesso) THEN ]%%
  <!-- sucesso -->
%%[ ELSE ]%%
  <!-- formulário -->
%%[ ENDIF ]%%
```

* Exibe sucesso após envio
* Caso contrário, mantém formulário

---

## Data Extension

**Nome:** `DEX_LP_MENSAGEMPERSONALIZADA`

Campos esperados:

| Campo               | Tipo  |
| ------------------- | ----- |
| SubscriberKey       | Text  |
| EmailAddress        | Email |
| nomeDe              | Text  |
| nomePara            | Text  |
| mensagem            | Text  |
| nova_subscriber_key | Text  |
| data_resp           | Date  |
| emailRemetente      | Email |

---

## Notas

* Permite múltiplos envios (sem primary key)
* Preparada para ativação via Journey Builder
* UX orientada à seleção guiada de conteúdo
* Validação básica de formulário
* Uso de Tailwind + GSAP para UI e animações
