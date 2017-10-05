---
title: "Associações do SendGrid no Azure Functions | Microsoft Docs"
description: "Referência de associações do SendGrid no Azure Functions"
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/16/2017
ms.author: rachelap
ms.openlocfilehash: 445a40a884e648cdb2a57f8ef43bed4f8a3efcf2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-sendgrid-bindings"></a>Associações do SendGrid no Azure Functions

Este artigo explica como configurar e trabalhar com associações do SendGrid no Azure Functions. Com o SendGrid, é possível usar o Azure Functions para enviar um email personalizado de forma programática.

Este artigo traz informações de referência para desenvolvedores do Azure Functions. Se for novo no Azure Functions, comece com os seguintes recursos:

[Crie seu primeiro Azure Function](functions-create-first-azure-function.md). 
Referências do desenvolvedor do [C#](functions-reference-csharp.md), [F#](functions-reference-fsharp.md) ou [Node](functions-reference-node.md).

## <a name="functionjson-for-sendgrid-bindings"></a>function.json para associações do SendGrid

O Azure Functions fornece uma associação de saída para o SendGrid. A associação de saída do SendGrid permite criar e enviar email de forma programática. 

A associação do SendGrid dá suporte às seguintes propriedades:

- `name`: obrigatório – o nome da variável usado no código da função da solicitação ou do corpo da solicitação. Esse valor é ```$return``` quando há apenas um valor retornado. 
- `type`: obrigatório – deve ser definido como “sendGrid”.
- `direction`: obrigatório – deve ser definido como “out”.
- `apiKey`: obrigatório – deve ser definido com o nome da chave de API armazenado nas configurações de aplicativo do Aplicativo de Funções.
- `to`: o endereço de email do destinatário.
- `from`: o endereço de email do remetente.
- `subject`: o assunto do email.
- `text`: o conteúdo do email.

Exemplo de **function.json**:

```json 
{
    "bindings": [
        {
            "name": "$return",
            "type": "sendGrid",
            "direction": "out",
            "apiKey" : "MySendGridKey",
            "to": "{ToEmail}",
            "from": "{FromEmail}",
            "subject": "SendGrid output bindings"
        }
    ]
}
```

> [!NOTE]
> O Azure Functions armazena suas informações de conexão e as chaves de API como configurações de aplicativo, para que elas não sejam inseridas no repositório de controle do código-fonte. Essa ação protege as informações confidenciais.
>
>

## <a name="c-example-of-the-sendgrid-output-binding"></a>Exemplo do C# da associação de saída do SendGrid

```csharp
#r "SendGrid"
using System;
using SendGrid.Helpers.Mail;

public static Mail Run(TraceWriter log, string input, out Mail message)
{
     message = new Mail
    {        
        Subject = "Azure news"          
    };

    var personalization = new Personalization();
    personalization.AddTo(new Email("recipient@contoso.com"));   

    Content content = new Content
    {
        Type = "text/plain",
        Value = input
    };
    message.AddContent(content);
    message.AddPersonalization(personalization);
}
```

## <a name="node-example-of-the-sendgrid-output-binding"></a>Exemplo de nó da associação de saída do SendGrid

```javascript
module.exports = function (context, input) {    
    var message = {
         "personalizations": [ { "to": [ { "email": "sample@sample.com" } ] } ],
        from: "sender@contoso.com",        
        subject: "Azure news",
        content: [{
            type: 'text/plain',
            value: input
        }]
    };

    context.done(null, message);
};

```

## <a name="next-steps"></a>Próximas etapas
Para obter informações sobre outras associações e outros gatilhos do Azure Functions, consulte 
- [Referências do desenvolvedor de gatilhos e associações do Azure Functions](functions-triggers-bindings.md)

- [Melhores Práticas para o Azure Functions](functions-best-practices.md) lista algumas melhores práticas para usar ao criar Azure Functions.

- [Referência do desenvolvedor do Azure Functions](functions-reference.md) Referência do programador para a codificação de funções e a definição de gatilhos e de associações.
