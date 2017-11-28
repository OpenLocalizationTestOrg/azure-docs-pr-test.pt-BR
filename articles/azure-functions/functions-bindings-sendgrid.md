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
# <a name="azure-functions-sendgrid-bindings"></a><span data-ttu-id="f9f7c-103">Associações do SendGrid no Azure Functions</span><span class="sxs-lookup"><span data-stu-id="f9f7c-103">Azure Functions SendGrid bindings</span></span>

<span data-ttu-id="f9f7c-104">Este artigo explica como tooconfigure e trabalhar com associações do SendGrid em funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="f9f7c-104">This article explains how tooconfigure and work with SendGrid bindings in Azure Functions.</span></span> <span data-ttu-id="f9f7c-105">Com SendGrid, você pode usar funções do Azure toosend personalizado email programaticamente.</span><span class="sxs-lookup"><span data-stu-id="f9f7c-105">With SendGrid, you can use Azure Functions toosend customized email programmatically.</span></span>

<span data-ttu-id="f9f7c-106">Este artigo traz informações de referência para desenvolvedores do Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="f9f7c-106">This article is reference information for Azure Functions developers.</span></span> <span data-ttu-id="f9f7c-107">Se você estiver novas funções tooAzure, inicie com hello recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="f9f7c-107">If you're new tooAzure Functions, start with hello following resources:</span></span>

<span data-ttu-id="f9f7c-108">[Crie seu primeiro Azure Function](functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="f9f7c-108">[Create your first Azure Function](functions-create-first-azure-function.md).</span></span> 
<span data-ttu-id="f9f7c-109">Referências do desenvolvedor do [C#](functions-reference-csharp.md), [F#](functions-reference-fsharp.md) ou [Node](functions-reference-node.md).</span><span class="sxs-lookup"><span data-stu-id="f9f7c-109">[C#](functions-reference-csharp.md), [F#](functions-reference-fsharp.md), or [Node](functions-reference-node.md) developer references.</span></span>

## <a name="functionjson-for-sendgrid-bindings"></a><span data-ttu-id="f9f7c-110">function.json para associações do SendGrid</span><span class="sxs-lookup"><span data-stu-id="f9f7c-110">function.json for SendGrid bindings</span></span>

<span data-ttu-id="f9f7c-111">O Azure Functions fornece uma associação de saída para o SendGrid.</span><span class="sxs-lookup"><span data-stu-id="f9f7c-111">Azure Functions provides an output binding for SendGrid.</span></span> <span data-ttu-id="f9f7c-112">Olá SendGrid saída associação permite que você toocreate e enviar emails por meio de programação.</span><span class="sxs-lookup"><span data-stu-id="f9f7c-112">hello SendGrid output binding enables you toocreate and send email programmatically.</span></span> 

<span data-ttu-id="f9f7c-113">associação de SendGrid Olá dá suporte a saudação propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="f9f7c-113">hello SendGrid binding supports hello following properties:</span></span>

- <span data-ttu-id="f9f7c-114">`name`: Necessária – o nome de variável Olá usado no código de função para solicitação de saudação ou o corpo da solicitação.</span><span class="sxs-lookup"><span data-stu-id="f9f7c-114">`name` : Required - hello variable name used in function code for hello request or request body.</span></span> <span data-ttu-id="f9f7c-115">Esse valor é ```$return``` quando há apenas um valor retornado.</span><span class="sxs-lookup"><span data-stu-id="f9f7c-115">This value is ```$return``` when there is only one return value.</span></span> 
- <span data-ttu-id="f9f7c-116">`type`: Necessária - deve ser definido muito "sendGrid".</span><span class="sxs-lookup"><span data-stu-id="f9f7c-116">`type` : Required - must be set too"sendGrid."</span></span>
- <span data-ttu-id="f9f7c-117">`direction`: Necessária - deve ser definido muito "out".</span><span class="sxs-lookup"><span data-stu-id="f9f7c-117">`direction` : Required - must be set too"out."</span></span>
- <span data-ttu-id="f9f7c-118">`apiKey`: Necessária - deve ser o nome de toohello de conjunto de sua chave de API armazenada nas configurações do aplicativo do aplicativo de função hello.</span><span class="sxs-lookup"><span data-stu-id="f9f7c-118">`apiKey` : Required - must be set toohello name of your API key stored in hello Function App's app settings.</span></span>
- <span data-ttu-id="f9f7c-119">`to`: Olá endereço de email do destinatário.</span><span class="sxs-lookup"><span data-stu-id="f9f7c-119">`to` : hello recipient's email address.</span></span>
- <span data-ttu-id="f9f7c-120">`from`: Olá endereço de email do remetente.</span><span class="sxs-lookup"><span data-stu-id="f9f7c-120">`from` : hello sender's email address.</span></span>
- <span data-ttu-id="f9f7c-121">`subject`: assunto de saudação do email hello.</span><span class="sxs-lookup"><span data-stu-id="f9f7c-121">`subject` : hello subject of hello email.</span></span>
- <span data-ttu-id="f9f7c-122">`text`: Olá conteúdo de email.</span><span class="sxs-lookup"><span data-stu-id="f9f7c-122">`text` : hello email content.</span></span>

<span data-ttu-id="f9f7c-123">Exemplo de **function.json**:</span><span class="sxs-lookup"><span data-stu-id="f9f7c-123">Example of **function.json**:</span></span>

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
> <span data-ttu-id="f9f7c-124">O Azure Functions armazena suas informações de conexão e as chaves de API como configurações de aplicativo, para que elas não sejam inseridas no repositório de controle do código-fonte.</span><span class="sxs-lookup"><span data-stu-id="f9f7c-124">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="f9f7c-125">Essa ação protege as informações confidenciais.</span><span class="sxs-lookup"><span data-stu-id="f9f7c-125">This action safeguards your sensitive information.</span></span>
>
>

## <a name="c-example-of-hello-sendgrid-output-binding"></a><span data-ttu-id="f9f7c-126">Associação de saída de exemplo em c# de saudação SendGrid</span><span class="sxs-lookup"><span data-stu-id="f9f7c-126">C# example of hello SendGrid output binding</span></span>

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

## <a name="node-example-of-hello-sendgrid-output-binding"></a><span data-ttu-id="f9f7c-127">Exemplo de nó de saudação SendGrid saída de associação</span><span class="sxs-lookup"><span data-stu-id="f9f7c-127">Node example of hello SendGrid output binding</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="f9f7c-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f9f7c-128">Next steps</span></span>
<span data-ttu-id="f9f7c-129">Para obter informações sobre outras associações e outros gatilhos do Azure Functions, consulte</span><span class="sxs-lookup"><span data-stu-id="f9f7c-129">For information about other bindings and triggers for Azure Functions, see</span></span> 
- [<span data-ttu-id="f9f7c-130">Referências do desenvolvedor de gatilhos e associações do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="f9f7c-130">Azure Functions triggers and bindings developer reference</span></span>](functions-triggers-bindings.md)

- <span data-ttu-id="f9f7c-131">[Práticas recomendadas para funções do Azure](functions-best-practices.md) lista alguns toouse práticas recomendada durante a criação de funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="f9f7c-131">[Best practices for Azure Functions](functions-best-practices.md) Lists some best practices toouse when creating Azure Functions.</span></span>

- <span data-ttu-id="f9f7c-132">[Referência do desenvolvedor do Azure Functions](functions-reference.md) Referência do programador para a codificação de funções e a definição de gatilhos e de associações.</span><span class="sxs-lookup"><span data-stu-id="f9f7c-132">[Azure Functions developer reference](functions-reference.md) Programmer reference for coding functions and defining triggers and bindings.</span></span>
