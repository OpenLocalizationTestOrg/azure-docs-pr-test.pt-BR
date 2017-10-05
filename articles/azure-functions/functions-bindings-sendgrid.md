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
# <a name="azure-functions-sendgrid-bindings"></a><span data-ttu-id="1fb6b-103">Associações do SendGrid no Azure Functions</span><span class="sxs-lookup"><span data-stu-id="1fb6b-103">Azure Functions SendGrid bindings</span></span>

<span data-ttu-id="1fb6b-104">Este artigo explica como configurar e trabalhar com associações do SendGrid no Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="1fb6b-104">This article explains how to configure and work with SendGrid bindings in Azure Functions.</span></span> <span data-ttu-id="1fb6b-105">Com o SendGrid, é possível usar o Azure Functions para enviar um email personalizado de forma programática.</span><span class="sxs-lookup"><span data-stu-id="1fb6b-105">With SendGrid, you can use Azure Functions to send customized email programmatically.</span></span>

<span data-ttu-id="1fb6b-106">Este artigo traz informações de referência para desenvolvedores do Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="1fb6b-106">This article is reference information for Azure Functions developers.</span></span> <span data-ttu-id="1fb6b-107">Se for novo no Azure Functions, comece com os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="1fb6b-107">If you're new to Azure Functions, start with the following resources:</span></span>

<span data-ttu-id="1fb6b-108">[Crie seu primeiro Azure Function](functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="1fb6b-108">[Create your first Azure Function](functions-create-first-azure-function.md).</span></span> 
<span data-ttu-id="1fb6b-109">Referências do desenvolvedor do [C#](functions-reference-csharp.md), [F#](functions-reference-fsharp.md) ou [Node](functions-reference-node.md).</span><span class="sxs-lookup"><span data-stu-id="1fb6b-109">[C#](functions-reference-csharp.md), [F#](functions-reference-fsharp.md), or [Node](functions-reference-node.md) developer references.</span></span>

## <a name="functionjson-for-sendgrid-bindings"></a><span data-ttu-id="1fb6b-110">function.json para associações do SendGrid</span><span class="sxs-lookup"><span data-stu-id="1fb6b-110">function.json for SendGrid bindings</span></span>

<span data-ttu-id="1fb6b-111">O Azure Functions fornece uma associação de saída para o SendGrid.</span><span class="sxs-lookup"><span data-stu-id="1fb6b-111">Azure Functions provides an output binding for SendGrid.</span></span> <span data-ttu-id="1fb6b-112">A associação de saída do SendGrid permite criar e enviar email de forma programática.</span><span class="sxs-lookup"><span data-stu-id="1fb6b-112">The SendGrid output binding enables you to create and send email programmatically.</span></span> 

<span data-ttu-id="1fb6b-113">A associação do SendGrid dá suporte às seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="1fb6b-113">The SendGrid binding supports the following properties:</span></span>

- <span data-ttu-id="1fb6b-114">`name`: obrigatório – o nome da variável usado no código da função da solicitação ou do corpo da solicitação.</span><span class="sxs-lookup"><span data-stu-id="1fb6b-114">`name` : Required - the variable name used in function code for the request or request body.</span></span> <span data-ttu-id="1fb6b-115">Esse valor é ```$return``` quando há apenas um valor retornado.</span><span class="sxs-lookup"><span data-stu-id="1fb6b-115">This value is ```$return``` when there is only one return value.</span></span> 
- <span data-ttu-id="1fb6b-116">`type`: obrigatório – deve ser definido como “sendGrid”.</span><span class="sxs-lookup"><span data-stu-id="1fb6b-116">`type` : Required - must be set to "sendGrid."</span></span>
- <span data-ttu-id="1fb6b-117">`direction`: obrigatório – deve ser definido como “out”.</span><span class="sxs-lookup"><span data-stu-id="1fb6b-117">`direction` : Required - must be set to "out."</span></span>
- <span data-ttu-id="1fb6b-118">`apiKey`: obrigatório – deve ser definido com o nome da chave de API armazenado nas configurações de aplicativo do Aplicativo de Funções.</span><span class="sxs-lookup"><span data-stu-id="1fb6b-118">`apiKey` : Required - must be set to the name of your API key stored in the Function App's app settings.</span></span>
- <span data-ttu-id="1fb6b-119">`to`: o endereço de email do destinatário.</span><span class="sxs-lookup"><span data-stu-id="1fb6b-119">`to` : the recipient's email address.</span></span>
- <span data-ttu-id="1fb6b-120">`from`: o endereço de email do remetente.</span><span class="sxs-lookup"><span data-stu-id="1fb6b-120">`from` : the sender's email address.</span></span>
- <span data-ttu-id="1fb6b-121">`subject`: o assunto do email.</span><span class="sxs-lookup"><span data-stu-id="1fb6b-121">`subject` : the subject of the email.</span></span>
- <span data-ttu-id="1fb6b-122">`text`: o conteúdo do email.</span><span class="sxs-lookup"><span data-stu-id="1fb6b-122">`text` : the email content.</span></span>

<span data-ttu-id="1fb6b-123">Exemplo de **function.json**:</span><span class="sxs-lookup"><span data-stu-id="1fb6b-123">Example of **function.json**:</span></span>

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
> <span data-ttu-id="1fb6b-124">O Azure Functions armazena suas informações de conexão e as chaves de API como configurações de aplicativo, para que elas não sejam inseridas no repositório de controle do código-fonte.</span><span class="sxs-lookup"><span data-stu-id="1fb6b-124">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="1fb6b-125">Essa ação protege as informações confidenciais.</span><span class="sxs-lookup"><span data-stu-id="1fb6b-125">This action safeguards your sensitive information.</span></span>
>
>

## <a name="c-example-of-the-sendgrid-output-binding"></a><span data-ttu-id="1fb6b-126">Exemplo do C# da associação de saída do SendGrid</span><span class="sxs-lookup"><span data-stu-id="1fb6b-126">C# example of the SendGrid output binding</span></span>

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

## <a name="node-example-of-the-sendgrid-output-binding"></a><span data-ttu-id="1fb6b-127">Exemplo de nó da associação de saída do SendGrid</span><span class="sxs-lookup"><span data-stu-id="1fb6b-127">Node example of the SendGrid output binding</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="1fb6b-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1fb6b-128">Next steps</span></span>
<span data-ttu-id="1fb6b-129">Para obter informações sobre outras associações e outros gatilhos do Azure Functions, consulte</span><span class="sxs-lookup"><span data-stu-id="1fb6b-129">For information about other bindings and triggers for Azure Functions, see</span></span> 
- [<span data-ttu-id="1fb6b-130">Referências do desenvolvedor de gatilhos e associações do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="1fb6b-130">Azure Functions triggers and bindings developer reference</span></span>](functions-triggers-bindings.md)

- <span data-ttu-id="1fb6b-131">[Melhores Práticas para o Azure Functions](functions-best-practices.md) lista algumas melhores práticas para usar ao criar Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="1fb6b-131">[Best practices for Azure Functions](functions-best-practices.md) Lists some best practices to use when creating Azure Functions.</span></span>

- <span data-ttu-id="1fb6b-132">[Referência do desenvolvedor do Azure Functions](functions-reference.md) Referência do programador para a codificação de funções e a definição de gatilhos e de associações.</span><span class="sxs-lookup"><span data-stu-id="1fb6b-132">[Azure Functions developer reference](functions-reference.md) Programmer reference for coding functions and defining triggers and bindings.</span></span>
