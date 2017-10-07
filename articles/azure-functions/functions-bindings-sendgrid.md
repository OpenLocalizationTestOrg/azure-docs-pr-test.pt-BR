---
title: "associações de funções SendGrid aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: 10a3837875eb6ae18e6c789bcf64cc401cf5f26a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-sendgrid-bindings"></a>Associações do SendGrid no Azure Functions

Este artigo explica como tooconfigure e trabalhar com associações do SendGrid em funções do Azure. Com SendGrid, você pode usar funções do Azure toosend personalizado email programaticamente.

Este artigo traz informações de referência para desenvolvedores do Azure Functions. Se você estiver novas funções tooAzure, inicie com hello recursos a seguir:

[Crie seu primeiro Azure Function](functions-create-first-azure-function.md). 
Referências do desenvolvedor do [C#](functions-reference-csharp.md), [F#](functions-reference-fsharp.md) ou [Node](functions-reference-node.md).

## <a name="functionjson-for-sendgrid-bindings"></a>function.json para associações do SendGrid

O Azure Functions fornece uma associação de saída para o SendGrid. Olá SendGrid saída associação permite que você toocreate e enviar emails por meio de programação. 

associação de SendGrid Olá dá suporte a saudação propriedades a seguir:

- `name`: Necessária – o nome de variável Olá usado no código de função para solicitação de saudação ou o corpo da solicitação. Esse valor é ```$return``` quando há apenas um valor retornado. 
- `type`: Necessária - deve ser definido muito "sendGrid".
- `direction`: Necessária - deve ser definido muito "out".
- `apiKey`: Necessária - deve ser o nome de toohello de conjunto de sua chave de API armazenada nas configurações do aplicativo do aplicativo de função hello.
- `to`: Olá endereço de email do destinatário.
- `from`: Olá endereço de email do remetente.
- `subject`: assunto de saudação do email hello.
- `text`: Olá conteúdo de email.

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

## <a name="c-example-of-hello-sendgrid-output-binding"></a>Associação de saída de exemplo em c# de saudação SendGrid

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

## <a name="node-example-of-hello-sendgrid-output-binding"></a>Exemplo de nó de saudação SendGrid saída de associação

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

- [Práticas recomendadas para funções do Azure](functions-best-practices.md) lista alguns toouse práticas recomendada durante a criação de funções do Azure.

- [Referência do desenvolvedor do Azure Functions](functions-reference.md) Referência do programador para a codificação de funções e a definição de gatilhos e de associações.
