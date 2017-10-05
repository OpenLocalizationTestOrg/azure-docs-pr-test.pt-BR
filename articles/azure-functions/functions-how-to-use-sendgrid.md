---
title: Como usar o SendGrid no Azure Functions | Microsoft Docs
description: Mostra como usar o SendGrid no Azure Functions
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
ms.openlocfilehash: 05c9f4e4a4351219da68af8b702c25f21d7d4d02
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-sendgrid-in-azure-functions"></a><span data-ttu-id="c8342-103">Como usar o SendGrid no Azure Functions</span><span class="sxs-lookup"><span data-stu-id="c8342-103">How to use SendGrid in Azure Functions</span></span>

## <a name="sendgrid-overview"></a><span data-ttu-id="c8342-104">Visão geral do SendGrid</span><span class="sxs-lookup"><span data-stu-id="c8342-104">SendGrid Overview</span></span>

<span data-ttu-id="c8342-105">O Azure Functions dá suporte às saídas de associações do SendGrid para habilitar funções para envio de mensagens de email com algumas linhas de código e uma conta do SendGrid.</span><span class="sxs-lookup"><span data-stu-id="c8342-105">Azure Functions supports SendGrid output bindings to enable your functions to send email messages with a few lines of code and a SendGrid account.</span></span>

<span data-ttu-id="c8342-106">Para usar a API do SendGrid em um Azure Function, você deve ter uma [conta do SendGrid](http://SendGrid.com).</span><span class="sxs-lookup"><span data-stu-id="c8342-106">To use the SendGrid API in an Azure Function, you must have a [SendGrid account](http://SendGrid.com).</span></span> <span data-ttu-id="c8342-107">Além disso, você deve ter uma chave de API do SendGrid.</span><span class="sxs-lookup"><span data-stu-id="c8342-107">Additionally, you must have a SendGrid API Key.</span></span> <span data-ttu-id="c8342-108">Faça logon em sua conta do SendGrid e clique em **Configurações** e depois em **Chave de API** para gerar uma chave de API.</span><span class="sxs-lookup"><span data-stu-id="c8342-108">Log in to your SendGrid account and click **Settings** then **API Key** to generate an API key.</span></span> <span data-ttu-id="c8342-109">Mantenha essa chave disponível, pois você a usará em uma etapa futura.</span><span class="sxs-lookup"><span data-stu-id="c8342-109">Keep this key available as you use it in an upcoming step.</span></span>

<span data-ttu-id="c8342-110">Agora você está pronto para criar um aplicativo de funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="c8342-110">You are now ready to create an Azure Function app.</span></span>

## <a name="create-an-azure-function-app"></a><span data-ttu-id="c8342-111">Criar um Aplicativo de funções do Azure</span><span class="sxs-lookup"><span data-stu-id="c8342-111">Create an Azure Function app</span></span> 

<span data-ttu-id="c8342-112">Aplicativos do Azure Function são contêineres para uma ou mais Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="c8342-112">Azure Function Apps are containers for one or more Azure functions.</span></span> <span data-ttu-id="c8342-113">Azure Functions são exatamente isso, uma função.</span><span class="sxs-lookup"><span data-stu-id="c8342-113">Azure functions are just that - a function.</span></span> <span data-ttu-id="c8342-114">Cada função do Azure está ligada a um gatilho, que é um evento que faz com que a função seja executada.</span><span class="sxs-lookup"><span data-stu-id="c8342-114">Each Azure function is tied to one trigger, which is an event that causes the function to run.</span></span>
<span data-ttu-id="c8342-115">Cada função pode conter qualquer número de associações de entrada ou saída.</span><span class="sxs-lookup"><span data-stu-id="c8342-115">Each function can contain any number of input or output bindings.</span></span> <span data-ttu-id="c8342-116">Associações são serviços que podem ser usados em uma função.</span><span class="sxs-lookup"><span data-stu-id="c8342-116">Bindings are services that you can use in a function.</span></span> <span data-ttu-id="c8342-117">O SendGrid é uma associação de saída que você pode usar para enviar email.</span><span class="sxs-lookup"><span data-stu-id="c8342-117">SendGrid is an output binding you can use to send email.</span></span> 

1. <span data-ttu-id="c8342-118">Faça logon no portal do Azure e [crie um Aplicativo de Funções do Azure](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) ou abra um Aplicativo de funções existente.</span><span class="sxs-lookup"><span data-stu-id="c8342-118">Log in to the Azure portal and [create an Azure Function App](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) or open an existing Function app.</span></span> 
2. <span data-ttu-id="c8342-119">Crie uma função do Azure.</span><span class="sxs-lookup"><span data-stu-id="c8342-119">Create an Azure function.</span></span> <span data-ttu-id="c8342-120">Para mantê-la simples, escolha um gatilho manual e C#.</span><span class="sxs-lookup"><span data-stu-id="c8342-120">To keep it simple, choose a manual trigger and C#.</span></span> 

 ![Criar uma função do Azure](./media/functions-how-to-use-sendgrid/functions-new-function-manual-trigger-page.png)

## <a name="configure-sendgrid-for-use-in-an-azure-function-app"></a><span data-ttu-id="c8342-122">Configure o SendGrid para uso em um aplicativo de funções do Azure</span><span class="sxs-lookup"><span data-stu-id="c8342-122">Configure SendGrid for use in an Azure Function app</span></span>

<span data-ttu-id="c8342-123">Você deve armazenar sua chave de API do SendGrid como uma configuração de aplicativo para usá-la em uma função.</span><span class="sxs-lookup"><span data-stu-id="c8342-123">You must store your SendGrid API Key as an app setting to use it in a function.</span></span> <span data-ttu-id="c8342-124">O campo ApiKey não é sua chave de API do SendGrid real, mas uma configuração de aplicativo que você define e que representa sua chave de API real.</span><span class="sxs-lookup"><span data-stu-id="c8342-124">The ApiKey field is not your actual SendGrid API key, but an app setting you define that represents your actual API key.</span></span> <span data-ttu-id="c8342-125">Armazenar a chave dessa maneira é para segurança, pois ela é separada de qualquer código ou arquivos que possam ser verificados no controle do código-fonte.</span><span class="sxs-lookup"><span data-stu-id="c8342-125">Storing your key this way is for security, since it is separate from any code or files that might be checked into source code control.</span></span>

- <span data-ttu-id="c8342-126">Crie uma chave **AppSettings** nas **Configurações de Aplicativo** de seu aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="c8342-126">Create an **AppSettings** key in your function app's **Application Settings**.</span></span>

 ![Criar uma função do Azure](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-api-key-app-settings.png)

## <a name="configure-sendgrid-output-bindings"></a><span data-ttu-id="c8342-128">Configurar associações de saída do SendGrid</span><span class="sxs-lookup"><span data-stu-id="c8342-128">Configure SendGrid output bindings</span></span>

<span data-ttu-id="c8342-129">O SendGrid está disponível como uma associação de saída da função do Azure.</span><span class="sxs-lookup"><span data-stu-id="c8342-129">SendGrid is available as an Azure function output binding.</span></span> <span data-ttu-id="c8342-130">Para criar uma associação de saída do SendGrid:</span><span class="sxs-lookup"><span data-stu-id="c8342-130">To create a SendGrid output binding:</span></span>

1. <span data-ttu-id="c8342-131">Vá para a guia **Integrar** da função no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c8342-131">Go to the **Integrate** tab of the function in the Azure portal.</span></span>
2. <span data-ttu-id="c8342-132">Clique em **Nova Saída** para criar uma associação de saída do SendGrid.</span><span class="sxs-lookup"><span data-stu-id="c8342-132">Click **New Output** to create a SendGrid output binding.</span></span>
3. <span data-ttu-id="c8342-133">Preencha as propriedades **Chave de API** e **Nome do parâmetro de mensagem**.</span><span class="sxs-lookup"><span data-stu-id="c8342-133">Fill in the **API Key** and **Message parameter name** properties.</span></span> <span data-ttu-id="c8342-134">Se desejar, você poderá inserir as outras propriedades agora ou então codificá-las.</span><span class="sxs-lookup"><span data-stu-id="c8342-134">If you want, you can enter the other properties now, or code them instead.</span></span> <span data-ttu-id="c8342-135">Essas configurações podem ser usadas como padrões.</span><span class="sxs-lookup"><span data-stu-id="c8342-135">These settings can be used as defaults.</span></span>

 ![Configurar associações de saída do SendGrid](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-output-bindings.png)

<span data-ttu-id="c8342-137">Adicionar uma associação a uma função cria um arquivo chamado **function.json** na pasta da função.</span><span class="sxs-lookup"><span data-stu-id="c8342-137">Adding a binding to a function creates a file called **function.json** in your function's folder.</span></span> <span data-ttu-id="c8342-138">Esse arquivo contém as mesmas informações que você vê na guia **Integrar** da função do Azure, mas no formato Json.</span><span class="sxs-lookup"><span data-stu-id="c8342-138">This file contains all the same information that you see in the Azure function's **Integrate** tab, but in Json format.</span></span> <span data-ttu-id="c8342-139">Configurar os campos **ApiKey**, **message** e **from** criará as seguintes entradas no arquivo **function.json**:</span><span class="sxs-lookup"><span data-stu-id="c8342-139">Setting the **ApiKey**, **message**, and **from** fields create the following entries in the **function.json** file:</span></span> 

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

<span data-ttu-id="c8342-140">Se preferir, você poderá modificar esse arquivo diretamente, por conta própria.</span><span class="sxs-lookup"><span data-stu-id="c8342-140">If you prefer, you may modify this file yourself directly.</span></span>

<span data-ttu-id="c8342-141">Agora que você criou e configurou a função e o Aplicativo de funções, você pode escrever o código para enviar um email.</span><span class="sxs-lookup"><span data-stu-id="c8342-141">Now that you have created and configured the Function App and function, you can write the code to send an email.</span></span>

## <a name="write-code-that-creates-and-sends-email"></a><span data-ttu-id="c8342-142">Escrever um código que cria e envia um email</span><span class="sxs-lookup"><span data-stu-id="c8342-142">Write code that creates and sends email</span></span>

<span data-ttu-id="c8342-143">A API do SendGrid contém todos os comandos de que você precisa para criar e enviar um email.</span><span class="sxs-lookup"><span data-stu-id="c8342-143">The SendGrid API contains all the commands you need to create and send an email.</span></span>  

- <span data-ttu-id="c8342-144">Substitua o código na função pelo código a seguir:</span><span class="sxs-lookup"><span data-stu-id="c8342-144">Replace the code in the function with the following code:</span></span>

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
    // change to email of recipient
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

<span data-ttu-id="c8342-145">Observe que a primeira linha contém a diretiva ```#r``` que faz referência ao assembly SendGrid.</span><span class="sxs-lookup"><span data-stu-id="c8342-145">Notice the first line contains the ```#r``` directive that references the SendGrid assembly.</span></span> <span data-ttu-id="c8342-146">Depois disso, você pode usar uma instrução ```using``` para acessar mais facilmente os objetos nesse namespace.</span><span class="sxs-lookup"><span data-stu-id="c8342-146">After that, you can use a ```using``` statement to more easily access the objects in that namespace.</span></span> <span data-ttu-id="c8342-147">No código, crie instâncias de ```Mail```, ```Personalization``` e ```Content``` objetos da API do SendGrid que compõem o email.</span><span class="sxs-lookup"><span data-stu-id="c8342-147">In the code, create instances of ```Mail```, ```Personalization```, and ```Content``` objects from the SendGrid API that compose the email.</span></span> <span data-ttu-id="c8342-148">Quando você retorna a mensagem, o SendGrid a entrega.</span><span class="sxs-lookup"><span data-stu-id="c8342-148">When you return the message, SendGrid delivers it.</span></span> 

<span data-ttu-id="c8342-149">A assinatura da função também contém um parâmetro de saída adicional do tipo ```Mail``` chamado ```message```.</span><span class="sxs-lookup"><span data-stu-id="c8342-149">The function's signature also contains an extra out parameter of type ```Mail``` named ```message```.</span></span> <span data-ttu-id="c8342-150">Ambas as associações de entrada e saída expressam a si mesmas como parâmetros de função no código.</span><span class="sxs-lookup"><span data-stu-id="c8342-150">Both input and output bindings express themselves as function parameters in code.</span></span> 

2. <span data-ttu-id="c8342-151">Teste seu código clicando em **Testar** e insira uma mensagem no campo **Corpo da solicitação**, então clique no botão **Executar**.</span><span class="sxs-lookup"><span data-stu-id="c8342-151">Test your code by clicking **Test** and entering a message into the **Request body** field, then clicking the **Run** button.</span></span>

 ![Testar seu código](./media/functions-how-to-use-sendgrid/functions-develop-test-sendgrid.png)

3. <span data-ttu-id="c8342-153">Verifique o email para confirmar se o SendGrid enviou o email.</span><span class="sxs-lookup"><span data-stu-id="c8342-153">Check email to verify that SendGrid sent the email.</span></span> <span data-ttu-id="c8342-154">Ele deve ir para o endereço no código da etapa 1 e conter a mensagem do **Corpo da solicitação**.</span><span class="sxs-lookup"><span data-stu-id="c8342-154">It should go to the address in the code from step 1, and contain the message from the **Request body**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c8342-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c8342-155">Next steps</span></span>
<span data-ttu-id="c8342-156">Este artigo demonstrou como usar o serviço SendGrid para criar e enviar email.</span><span class="sxs-lookup"><span data-stu-id="c8342-156">This article has demonstrated how to use the SendGrid service to create and send email.</span></span> <span data-ttu-id="c8342-157">Para saber mais sobre como usar o Azure Functions em seus aplicativos, consulte os tópicos a seguir:</span><span class="sxs-lookup"><span data-stu-id="c8342-157">To learn more about using Azure Functions in your apps, see the following topics:</span></span> 

- <span data-ttu-id="c8342-158">[Melhores Práticas para o Azure Functions](functions-best-practices.md) lista algumas melhores práticas para usar ao criar Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="c8342-158">[Best practices for Azure Functions](functions-best-practices.md) Lists some best practices to use when creating Azure Functions.</span></span>

- <span data-ttu-id="c8342-159">[Referência do desenvolvedor do Azure Functions](functions-reference.md) Referência do programador para a codificação de funções e a definição de gatilhos e de associações.</span><span class="sxs-lookup"><span data-stu-id="c8342-159">[Azure Functions developer reference](functions-reference.md) Programmer reference for coding functions and defining triggers and bindings.</span></span>

- <span data-ttu-id="c8342-160">[Testando o Azure Functions](functions-test-a-function.md) Descreve várias ferramentas e técnicas para testar suas funções.</span><span class="sxs-lookup"><span data-stu-id="c8342-160">[Testing Azure Functions](functions-test-a-function.md) Describes various tools and techniques for testing your functions.</span></span>