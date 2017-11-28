---
title: "aaaHow toouse SendGrid nas funções do Azure | Microsoft Docs"
description: "Mostra como toouse SendGrid em funções do Azure"
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 01/31/2017
ms.author: rachelap
ms.openlocfilehash: a0ffdae04e5924c773d2d26427626fc1f570f7ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-sendgrid-in-azure-functions"></a><span data-ttu-id="1e53f-103">Como toouse SendGrid em funções do Azure</span><span class="sxs-lookup"><span data-stu-id="1e53f-103">How toouse SendGrid in Azure Functions</span></span>

## <a name="sendgrid-overview"></a><span data-ttu-id="1e53f-104">Visão geral do SendGrid</span><span class="sxs-lookup"><span data-stu-id="1e53f-104">SendGrid Overview</span></span>

<span data-ttu-id="1e53f-105">Suporte de funções do Azure SendGrid saída associações tooenable suas mensagens de email de toosend funções com algumas linhas de código e uma conta do SendGrid.</span><span class="sxs-lookup"><span data-stu-id="1e53f-105">Azure Functions supports SendGrid output bindings tooenable your functions toosend email messages with a few lines of code and a SendGrid account.</span></span>

<span data-ttu-id="1e53f-106">API do SendGrid toouse Olá em uma função do Azure, você deve ter uma [conta do SendGrid](http://SendGrid.com).</span><span class="sxs-lookup"><span data-stu-id="1e53f-106">toouse hello SendGrid API in an Azure Function, you must have a [SendGrid account](http://SendGrid.com).</span></span> <span data-ttu-id="1e53f-107">Além disso, você deve ter uma chave de API do SendGrid.</span><span class="sxs-lookup"><span data-stu-id="1e53f-107">Additionally, you must have a SendGrid API Key.</span></span> <span data-ttu-id="1e53f-108">Faça logon na conta do SendGrid de tooyour e clique **configurações** , em seguida, **chave API** chave toogenerate uma API.</span><span class="sxs-lookup"><span data-stu-id="1e53f-108">Log in tooyour SendGrid account and click **Settings** then **API Key** toogenerate an API key.</span></span> <span data-ttu-id="1e53f-109">Mantenha essa chave disponível, pois você a usará em uma etapa futura.</span><span class="sxs-lookup"><span data-stu-id="1e53f-109">Keep this key available as you use it in an upcoming step.</span></span>

<span data-ttu-id="1e53f-110">Agora você está pronto toocreate um aplicativo de função do Azure.</span><span class="sxs-lookup"><span data-stu-id="1e53f-110">You are now ready toocreate an Azure Function app.</span></span>

## <a name="create-an-azure-function-app"></a><span data-ttu-id="1e53f-111">Criar um Aplicativo de funções do Azure</span><span class="sxs-lookup"><span data-stu-id="1e53f-111">Create an Azure Function app</span></span> 

<span data-ttu-id="1e53f-112">Aplicativos do Azure Function são contêineres para uma ou mais Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="1e53f-112">Azure Function Apps are containers for one or more Azure functions.</span></span> <span data-ttu-id="1e53f-113">Azure Functions são exatamente isso, uma função.</span><span class="sxs-lookup"><span data-stu-id="1e53f-113">Azure functions are just that - a function.</span></span> <span data-ttu-id="1e53f-114">Cada função do Azure é gatilho tooone associado, que é um evento que faz com que o hello função toorun.</span><span class="sxs-lookup"><span data-stu-id="1e53f-114">Each Azure function is tied tooone trigger, which is an event that causes hello function toorun.</span></span>
<span data-ttu-id="1e53f-115">Cada função pode conter qualquer número de associações de entrada ou saída.</span><span class="sxs-lookup"><span data-stu-id="1e53f-115">Each function can contain any number of input or output bindings.</span></span> <span data-ttu-id="1e53f-116">Associações são serviços que podem ser usados em uma função.</span><span class="sxs-lookup"><span data-stu-id="1e53f-116">Bindings are services that you can use in a function.</span></span> <span data-ttu-id="1e53f-117">SendGrid é uma saída de associação que você pode usar o email toosend.</span><span class="sxs-lookup"><span data-stu-id="1e53f-117">SendGrid is an output binding you can use toosend email.</span></span> 

1. <span data-ttu-id="1e53f-118">Faça logon no portal do Azure de toohello e [criar um aplicativo de função do Azure](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) ou abrir um aplicativo de função existente.</span><span class="sxs-lookup"><span data-stu-id="1e53f-118">Log in toohello Azure portal and [create an Azure Function App](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) or open an existing Function app.</span></span> 
2. <span data-ttu-id="1e53f-119">Crie uma função do Azure.</span><span class="sxs-lookup"><span data-stu-id="1e53f-119">Create an Azure function.</span></span> <span data-ttu-id="1e53f-120">tookeep-o simples, escolha um gatilho manual e c#.</span><span class="sxs-lookup"><span data-stu-id="1e53f-120">tookeep it simple, choose a manual trigger and C#.</span></span> 

 ![Criar uma função do Azure](./media/functions-how-to-use-sendgrid/functions-new-function-manual-trigger-page.png)

## <a name="configure-sendgrid-for-use-in-an-azure-function-app"></a><span data-ttu-id="1e53f-122">Configure o SendGrid para uso em um aplicativo de funções do Azure</span><span class="sxs-lookup"><span data-stu-id="1e53f-122">Configure SendGrid for use in an Azure Function app</span></span>

<span data-ttu-id="1e53f-123">Você deve armazenar sua chave de API do SendGrid como um toouse de configuração do aplicativo em uma função.</span><span class="sxs-lookup"><span data-stu-id="1e53f-123">You must store your SendGrid API Key as an app setting toouse it in a function.</span></span> <span data-ttu-id="1e53f-124">campo de ApiKey Olá não é sua chave de API do SendGrid real, mas um configuração de aplicativo definir que representa a sua chave de API real.</span><span class="sxs-lookup"><span data-stu-id="1e53f-124">hello ApiKey field is not your actual SendGrid API key, but an app setting you define that represents your actual API key.</span></span> <span data-ttu-id="1e53f-125">Armazenar a chave dessa maneira é para segurança, pois ela é separada de qualquer código ou arquivos que possam ser verificados no controle do código-fonte.</span><span class="sxs-lookup"><span data-stu-id="1e53f-125">Storing your key this way is for security, since it is separate from any code or files that might be checked into source code control.</span></span>

- <span data-ttu-id="1e53f-126">Crie uma chave **AppSettings** nas **Configurações de Aplicativo** de seu aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="1e53f-126">Create an **AppSettings** key in your function app's **Application Settings**.</span></span>

 ![Criar uma função do Azure](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-api-key-app-settings.png)

## <a name="configure-sendgrid-output-bindings"></a><span data-ttu-id="1e53f-128">Configurar associações de saída do SendGrid</span><span class="sxs-lookup"><span data-stu-id="1e53f-128">Configure SendGrid output bindings</span></span>

<span data-ttu-id="1e53f-129">O SendGrid está disponível como uma associação de saída da função do Azure.</span><span class="sxs-lookup"><span data-stu-id="1e53f-129">SendGrid is available as an Azure function output binding.</span></span> <span data-ttu-id="1e53f-130">associação de saída toocreate um SendGrid:</span><span class="sxs-lookup"><span data-stu-id="1e53f-130">toocreate a SendGrid output binding:</span></span>

1. <span data-ttu-id="1e53f-131">Vá toohello **integrar** guia da função Olá Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1e53f-131">Go toohello **Integrate** tab of hello function in hello Azure portal.</span></span>
2. <span data-ttu-id="1e53f-132">Clique em **nova saída** toocreate um SendGrid associação de saída.</span><span class="sxs-lookup"><span data-stu-id="1e53f-132">Click **New Output** toocreate a SendGrid output binding.</span></span>
3. <span data-ttu-id="1e53f-133">Preencha Olá **chave API** e **nome de parâmetro de mensagem** propriedades.</span><span class="sxs-lookup"><span data-stu-id="1e53f-133">Fill in hello **API Key** and **Message parameter name** properties.</span></span> <span data-ttu-id="1e53f-134">Se desejar, você pode inserir Olá outras propriedades agora ou codificá-los em vez disso.</span><span class="sxs-lookup"><span data-stu-id="1e53f-134">If you want, you can enter hello other properties now, or code them instead.</span></span> <span data-ttu-id="1e53f-135">Essas configurações podem ser usadas como padrões.</span><span class="sxs-lookup"><span data-stu-id="1e53f-135">These settings can be used as defaults.</span></span>

 ![Configurar associações de saída do SendGrid](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-output-bindings.png)

<span data-ttu-id="1e53f-137">Adicionar uma função de tooa associação cria um arquivo chamado **function.json** na pasta da função.</span><span class="sxs-lookup"><span data-stu-id="1e53f-137">Adding a binding tooa function creates a file called **function.json** in your function's folder.</span></span> <span data-ttu-id="1e53f-138">Esse arquivo contém todos os Olá as mesmas informações que você vê no hello da função do Azure **integrar** guia, mas o formato Json.</span><span class="sxs-lookup"><span data-stu-id="1e53f-138">This file contains all hello same information that you see in hello Azure function's **Integrate** tab, but in Json format.</span></span> <span data-ttu-id="1e53f-139">Saudação de configuração **ApiKey**, **mensagem**, e **de** campos criaram Olá Olá entradas a seguir **function.json** arquivo:</span><span class="sxs-lookup"><span data-stu-id="1e53f-139">Setting hello **ApiKey**, **message**, and **from** fields create hello following entries in hello **function.json** file:</span></span> 

```json
{
  "bindings": [    
    {
      "type": "sendGrid",
      "name": "message",
      "apiKey": "SendGridKey",
      "direction": "out",
      "from": "azure@contoso.com"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="1e53f-140">Se preferir, você poderá modificar esse arquivo diretamente, por conta própria.</span><span class="sxs-lookup"><span data-stu-id="1e53f-140">If you prefer, you may modify this file yourself directly.</span></span>

<span data-ttu-id="1e53f-141">Agora que você criou e configurou hello função de aplicativo e função, você pode escrever Olá código toosend um email.</span><span class="sxs-lookup"><span data-stu-id="1e53f-141">Now that you have created and configured hello Function App and function, you can write hello code toosend an email.</span></span>

## <a name="write-code-that-creates-and-sends-email"></a><span data-ttu-id="1e53f-142">Escrever um código que cria e envia um email</span><span class="sxs-lookup"><span data-stu-id="1e53f-142">Write code that creates and sends email</span></span>

<span data-ttu-id="1e53f-143">Olá API do SendGrid contém todos os Olá comandos necessário toocreate e enviar um email.</span><span class="sxs-lookup"><span data-stu-id="1e53f-143">hello SendGrid API contains all hello commands you need toocreate and send an email.</span></span>  

- <span data-ttu-id="1e53f-144">Substitua o código de saudação em função hello com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="1e53f-144">Replace hello code in hello function with hello following code:</span></span>

```cs
#r "SendGrid"
using System;
using SendGrid.Helpers.Mail;

public static void Run(TraceWriter log, string input, out Mail message)
{
    message = new Mail
    {        
        Subject = "Azure news"          
    };

    var personalization = new Personalization();
    // change tooemail of recipient
    personalization.AddTo(new Email("MoreEmailPlease@contoso.com"));   

    Content content = new Content
    {
        Type = "text/plain",
        Value = input
    };
    message.AddContent(content);
    message.AddPersonalization(personalization);
}
```

<span data-ttu-id="1e53f-145">Aviso Olá primeira linha contém Olá ```#r``` diretiva que faz referência ao assembly do SendGrid hello.</span><span class="sxs-lookup"><span data-stu-id="1e53f-145">Notice hello first line contains hello ```#r``` directive that references hello SendGrid assembly.</span></span> <span data-ttu-id="1e53f-146">Depois disso, você pode usar um ```using``` instrução toomore acessar facilmente os objetos de saudação naquele namespace.</span><span class="sxs-lookup"><span data-stu-id="1e53f-146">After that, you can use a ```using``` statement toomore easily access hello objects in that namespace.</span></span> <span data-ttu-id="1e53f-147">No código hello, criar instâncias de ```Mail```, ```Personalization```, e ```Content``` objetos de saudação API do SendGrid que compõem o email de saudação.</span><span class="sxs-lookup"><span data-stu-id="1e53f-147">In hello code, create instances of ```Mail```, ```Personalization```, and ```Content``` objects from hello SendGrid API that compose hello email.</span></span> <span data-ttu-id="1e53f-148">Quando você retorna a mensagem de saudação, SendGrid a entrega.</span><span class="sxs-lookup"><span data-stu-id="1e53f-148">When you return hello message, SendGrid delivers it.</span></span> 

<span data-ttu-id="1e53f-149">Olá assinatura da função também contém um extra de parâmetro de tipo out ```Mail``` chamado ```message```.</span><span class="sxs-lookup"><span data-stu-id="1e53f-149">hello function's signature also contains an extra out parameter of type ```Mail``` named ```message```.</span></span> <span data-ttu-id="1e53f-150">Ambas as associações de entrada e saída expressam a si mesmas como parâmetros de função no código.</span><span class="sxs-lookup"><span data-stu-id="1e53f-150">Both input and output bindings express themselves as function parameters in code.</span></span> 

2. <span data-ttu-id="1e53f-151">Teste seu código clicando **teste** e inserindo uma mensagem no hello **corpo da solicitação** campo, em seguida, clicando em Olá **executar** botão.</span><span class="sxs-lookup"><span data-stu-id="1e53f-151">Test your code by clicking **Test** and entering a message into hello **Request body** field, then clicking hello **Run** button.</span></span>

 ![Testar seu código](./media/functions-how-to-use-sendgrid/functions-develop-test-sendgrid.png)

3. <span data-ttu-id="1e53f-153">Verificar email tooverify SendGrid enviado email hello.</span><span class="sxs-lookup"><span data-stu-id="1e53f-153">Check email tooverify that SendGrid sent hello email.</span></span> <span data-ttu-id="1e53f-154">Ele deve ir endereço toohello no código de saudação da etapa 1 e contém a mensagem de saudação do hello **corpo da solicitação**.</span><span class="sxs-lookup"><span data-stu-id="1e53f-154">It should go toohello address in hello code from step 1, and contain hello message from hello **Request body**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e53f-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1e53f-155">Next steps</span></span>
<span data-ttu-id="1e53f-156">Este artigo demonstrou como toouse Olá SendGrid toocreate de serviço e enviar email.</span><span class="sxs-lookup"><span data-stu-id="1e53f-156">This article has demonstrated how toouse hello SendGrid service toocreate and send email.</span></span> <span data-ttu-id="1e53f-157">toolearn mais sobre como usar funções do Azure em seus aplicativos, consulte Olá seguintes tópicos:</span><span class="sxs-lookup"><span data-stu-id="1e53f-157">toolearn more about using Azure Functions in your apps, see hello following topics:</span></span> 

- <span data-ttu-id="1e53f-158">[Práticas recomendadas para funções do Azure](functions-best-practices.md) lista alguns toouse práticas recomendada durante a criação de funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="1e53f-158">[Best practices for Azure Functions](functions-best-practices.md) Lists some best practices toouse when creating Azure Functions.</span></span>

- <span data-ttu-id="1e53f-159">[Referência do desenvolvedor do Azure Functions](functions-reference.md) Referência do programador para a codificação de funções e a definição de gatilhos e de associações.</span><span class="sxs-lookup"><span data-stu-id="1e53f-159">[Azure Functions developer reference](functions-reference.md) Programmer reference for coding functions and defining triggers and bindings.</span></span>

- <span data-ttu-id="1e53f-160">[Testando o Azure Functions](functions-test-a-function.md) Descreve várias ferramentas e técnicas para testar suas funções.</span><span class="sxs-lookup"><span data-stu-id="1e53f-160">[Testing Azure Functions](functions-test-a-function.md) Describes various tools and techniques for testing your functions.</span></span>