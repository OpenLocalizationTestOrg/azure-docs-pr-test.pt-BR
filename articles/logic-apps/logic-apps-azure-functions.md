---
title: "código de aaaCustom para aplicativos do Azure lógica com funções do Azure | Microsoft Docs"
description: "Criar e executar código personalizado para Aplicativo Lógico do Azure com o Azure Functions"
services: logic-apps,functions
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 9fab1050-cfbc-4a8b-b1b3-5531bee92856
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 18b3821ed7e434feb568b9b96e9a5a2189dba3bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-and-run-custom-code-for-logic-apps-through-azure-functions"></a><span data-ttu-id="f39b9-103">Adicionar e executar código personalizado para aplicativos lógicos por meio do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="f39b9-103">Add and run custom code for logic apps through Azure Functions</span></span>

<span data-ttu-id="f39b9-104">toorun personalizado trechos de código do c# ou Node. js em aplicativos lógicos, você pode criar funções personalizadas por meio das funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="f39b9-104">toorun custom snippets of C# or node.js in logic apps, you can create custom functions through Azure Functions.</span></span> 
<span data-ttu-id="f39b9-105">O [Azure Functions](../azure-functions/functions-overview.md) oferece uma computação sem servidor no Microsoft Azure e é útil para realizar estas tarefas:</span><span class="sxs-lookup"><span data-stu-id="f39b9-105">[Azure Functions](../azure-functions/functions-overview.md) offers server-free computing in Microsoft Azure and are useful for performing these tasks:</span></span>

* <span data-ttu-id="f39b9-106">Formatação avançada ou computação de campos em um aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="f39b9-106">Advanced formatting or compute of fields in logic apps</span></span>
* <span data-ttu-id="f39b9-107">Execute cálculos em um fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="f39b9-107">Perform calculations in a workflow.</span></span>
* <span data-ttu-id="f39b9-108">Estender a funcionalidade do aplicativo hello lógica com funções que têm suporte em c# ou Node. js</span><span class="sxs-lookup"><span data-stu-id="f39b9-108">Extend hello logic app functionality with functions that are supported in C# or node.js</span></span>

## <a name="create-custom-functions-for-your-logic-apps"></a><span data-ttu-id="f39b9-109">Criar funções personalizadas para aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="f39b9-109">Create custom functions for your logic apps</span></span>

<span data-ttu-id="f39b9-110">É recomendável que você crie uma função no portal do Azure funções hello, de saudação **Webhook genérico - nó** ou **Webhook genérico - C#** modelos.</span><span class="sxs-lookup"><span data-stu-id="f39b9-110">We recommend that you create a function in hello Azure Functions portal, from hello **Generic Webhook - Node** or **Generic Webhook - C#** templates.</span></span> <span data-ttu-id="f39b9-111">resultado de saudação cria um preenchido automaticamente de um modelo que aceita `application/json` de um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="f39b9-111">hello result creates an auto-populated a template that accepts `application/json` from a logic app.</span></span> <span data-ttu-id="f39b9-112">Funções que você cria com esses modelos são detectadas automaticamente e aparecer em Olá lógica Designer do aplicativo em **funções do Azure em minha região.**</span><span class="sxs-lookup"><span data-stu-id="f39b9-112">Functions that you create from these templates are automatically detected and appear in hello Logic App Designer under **Azure Functions in my region.**</span></span>

<span data-ttu-id="f39b9-113">Em Olá portal do Azure, Olá **integrar** painel para sua função, o modelo deve mostrar que **modo** definido muito**Webhook** e **Webhook tipo** está definido muito**JSON genérico**.</span><span class="sxs-lookup"><span data-stu-id="f39b9-113">In hello Azure portal, on hello **Integrate** pane for your function, your template should show that **Mode** set too**Webhook** and **Webhook type** is set too**Generic JSON**.</span></span> 

<span data-ttu-id="f39b9-114">Funções de Webhook aceitar uma solicitação e passá-lo no método hello por meio de um `data` variável.</span><span class="sxs-lookup"><span data-stu-id="f39b9-114">Webhook functions accept a request and pass it into hello method via a `data` variable.</span></span> <span data-ttu-id="f39b9-115">Você pode acessar as propriedades de saudação da carga usando a notação como `data.function-name`.</span><span class="sxs-lookup"><span data-stu-id="f39b9-115">You can access hello properties of your payload by using dot notation like `data.function-name`.</span></span> <span data-ttu-id="f39b9-116">Por exemplo, uma função JavaScript simples que converte um valor DateTime em uma cadeia de caracteres de data aparência Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="f39b9-116">For example, a simple JavaScript function that converts a DateTime value into a date string looks like hello following example:</span></span>

```
function start(req, res){
    var data = req.body;
    res = {
        body: data.date.ToDateString();
    }
}
```

## <a name="call-azure-functions-from-logic-apps"></a><span data-ttu-id="f39b9-117">Chamar o Azure Functions de aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="f39b9-117">Call Azure Functions from logic apps</span></span>

<span data-ttu-id="f39b9-118">contêineres de saudação toolist em sua assinatura e a função hello selecione que você deseja toocall, no Designer de lógica de aplicativo, clique em Olá **ações** menu e selecione uma das **funções do Azure em minha região**.</span><span class="sxs-lookup"><span data-stu-id="f39b9-118">toolist hello containers in your subscription and select hello function that you want toocall, in Logic App Designer, click hello **Actions** menu, and select from **Azure Functions in my Region**.</span></span>

<span data-ttu-id="f39b9-119">Depois de selecionar a função hello, será solicitado toospecify um objeto de carga de entrada.</span><span class="sxs-lookup"><span data-stu-id="f39b9-119">After you select hello function, you are asked toospecify an input payload object.</span></span> <span data-ttu-id="f39b9-120">Este objeto é uma mensagem de saudação Olá lógica aplicativo envia toohello função e deve ser um objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="f39b9-120">This object is hello message that hello logic app sends toohello function and must be a JSON object.</span></span> <span data-ttu-id="f39b9-121">Por exemplo, se você quiser toopass em Olá **última modificação** data de um disparador da equipe de vendas, carga de função hello pode parecer semelhante a este exemplo:</span><span class="sxs-lookup"><span data-stu-id="f39b9-121">For example, if you want toopass in hello **Last Modified** date from a Salesforce trigger, hello function payload might look like this example:</span></span>

![Data da última modificação][1]

## <a name="trigger-logic-apps-from-a-function"></a><span data-ttu-id="f39b9-123">Disparar aplicativos lógicos a partir de uma função</span><span class="sxs-lookup"><span data-stu-id="f39b9-123">Trigger logic apps from a function</span></span>

<span data-ttu-id="f39b9-124">Você pode disparar um aplicativo lógico de dentro de uma função.</span><span class="sxs-lookup"><span data-stu-id="f39b9-124">You can trigger a logic app from inside a function.</span></span> <span data-ttu-id="f39b9-125">Constule [Aplicativos lógicos como pontos de extremidade escaláveis](logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="f39b9-125">See [Logic apps as callable endpoints](logic-apps-http-endpoint.md).</span></span> <span data-ttu-id="f39b9-126">Criar um aplicativo de lógica que tem um gatilho manual, em seguida, de dentro de sua função, gerar uma URL de gatilho manual toohello HTTP POST com carga Olá que quer enviar toohello lógica aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f39b9-126">Create a logic app that has a manual trigger, then from inside your function, generate an HTTP POST toohello manual trigger URL with hello payload that you want sent toohello logic app.</span></span>

### <a name="create-a-function-from-logic-app-designer"></a><span data-ttu-id="f39b9-127">Criar uma função do Designer de Aplicativos Lógicos</span><span class="sxs-lookup"><span data-stu-id="f39b9-127">Create a function from Logic App Designer</span></span>

<span data-ttu-id="f39b9-128">Você também pode criar uma função de webhook Node. js do designer de saudação.</span><span class="sxs-lookup"><span data-stu-id="f39b9-128">You can also create a node.js webhook function from hello designer.</span></span> <span data-ttu-id="f39b9-129">Primeiro, selecione **Azure Functions em minha região** , em seguida, escolha um contêiner de sua função.</span><span class="sxs-lookup"><span data-stu-id="f39b9-129">First, select **Azure Functions in my Region,** and then choose a container for your function.</span></span> <span data-ttu-id="f39b9-130">Se você ainda não tiver um contêiner, você precisa toocreate de saudação [portal do Azure funções](https://functions.azure.com/signin).</span><span class="sxs-lookup"><span data-stu-id="f39b9-130">If you don't yet have a container, you need toocreate one from hello [Azure Functions portal](https://functions.azure.com/signin).</span></span> <span data-ttu-id="f39b9-131">Em seguida, selecione **Criar Novo**.</span><span class="sxs-lookup"><span data-stu-id="f39b9-131">Then select **Create New**.</span></span>  

<span data-ttu-id="f39b9-132">toogenerate um modelo com base em dados de saudação que você deseja toocompute, especifique o objeto de contexto de saudação que você planeje toopass em uma função.</span><span class="sxs-lookup"><span data-stu-id="f39b9-132">toogenerate a template based on hello data that you want toocompute, specify hello context object that you plan toopass into a function.</span></span> <span data-ttu-id="f39b9-133">Esse objeto deve ser um objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="f39b9-133">This object must be a JSON object.</span></span> <span data-ttu-id="f39b9-134">Por exemplo, se você passar no conteúdo do arquivo hello de uma ação de FTP, carga de contexto de saudação é semelhante a este exemplo:</span><span class="sxs-lookup"><span data-stu-id="f39b9-134">For example, if you pass in hello file content from an FTP action, hello context payload looks like this example:</span></span>

![Conteúdo do contexto][2]

> [!NOTE]
> <span data-ttu-id="f39b9-136">Porque esse objeto não foi convertido como uma cadeia de caracteres, o conteúdo de saudação é adicionado diretamente toohello carga JSON.</span><span class="sxs-lookup"><span data-stu-id="f39b9-136">Because this object wasn't cast as a string, hello content is added directly toohello JSON payload.</span></span> <span data-ttu-id="f39b9-137">No entanto, ocorrerá um erro se o objeto de saudação não é um token JSON (ou seja, uma cadeia de caracteres ou JSON/matriz object).</span><span class="sxs-lookup"><span data-stu-id="f39b9-137">However, an error occurs if hello object is not a JSON token (that is, a string or a JSON object/array).</span></span> <span data-ttu-id="f39b9-138">objeto de saudação toocast como uma cadeia de caracteres, adicionar aspas, conforme mostrado na primeira ilustração Olá neste artigo.</span><span class="sxs-lookup"><span data-stu-id="f39b9-138">toocast hello object as a string, add quotes as shown in hello first illustration in this article.</span></span>
> 

<span data-ttu-id="f39b9-139">designer de Hello, em seguida, gera um modelo de função que você pode criar embutido.</span><span class="sxs-lookup"><span data-stu-id="f39b9-139">hello designer then generates a function template that you can create inline.</span></span> <span data-ttu-id="f39b9-140">Variáveis são previamente criadas com base no contexto de saudação que você planeje toopass em função hello.</span><span class="sxs-lookup"><span data-stu-id="f39b9-140">Variables are pre-created based on hello context that you plan toopass into hello function.</span></span>

<!--Image references-->
[1]: ./media/logic-apps-azure-functions/callfunction.png
[2]: ./media/logic-apps-azure-functions/createfunction.png
