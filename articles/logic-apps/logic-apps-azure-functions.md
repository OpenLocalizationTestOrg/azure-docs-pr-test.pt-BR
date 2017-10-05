---
title: "Código personalizado para Aplicativo Lógico do Azure com o Azure Functions | Microsoft Docs"
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
ms.openlocfilehash: 18442c87b049200fac5ed41cc7034ba7a848b8d3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="add-and-run-custom-code-for-logic-apps-through-azure-functions"></a><span data-ttu-id="c3550-103">Adicionar e executar código personalizado para aplicativos lógicos por meio do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="c3550-103">Add and run custom code for logic apps through Azure Functions</span></span>

<span data-ttu-id="c3550-104">Para executar trechos personalizados do C# ou Node.js em aplicativos lógicos, é possível criar funções personalizadas por meio do Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="c3550-104">To run custom snippets of C# or node.js in logic apps, you can create custom functions through Azure Functions.</span></span> 
<span data-ttu-id="c3550-105">O [Azure Functions](../azure-functions/functions-overview.md) oferece uma computação sem servidor no Microsoft Azure e é útil para realizar estas tarefas:</span><span class="sxs-lookup"><span data-stu-id="c3550-105">[Azure Functions](../azure-functions/functions-overview.md) offers server-free computing in Microsoft Azure and are useful for performing these tasks:</span></span>

* <span data-ttu-id="c3550-106">Formatação avançada ou computação de campos em um aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="c3550-106">Advanced formatting or compute of fields in logic apps</span></span>
* <span data-ttu-id="c3550-107">Execute cálculos em um fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="c3550-107">Perform calculations in a workflow.</span></span>
* <span data-ttu-id="c3550-108">Estender a funcionalidade do aplicativo lógico com funções com suporte no C# ou no node.js</span><span class="sxs-lookup"><span data-stu-id="c3550-108">Extend the logic app functionality with functions that are supported in C# or node.js</span></span>

## <a name="create-custom-functions-for-your-logic-apps"></a><span data-ttu-id="c3550-109">Criar funções personalizadas para aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="c3550-109">Create custom functions for your logic apps</span></span>

<span data-ttu-id="c3550-110">É recomendável que você crie uma função no portal das Azure Functions usando os modelos **Webhook Genérico – Nó** ou **Webhook Genérico – C#**.</span><span class="sxs-lookup"><span data-stu-id="c3550-110">We recommend that you create a function in the Azure Functions portal, from the **Generic Webhook - Node** or **Generic Webhook - C#** templates.</span></span> <span data-ttu-id="c3550-111">O resultado cria um modelo populado automaticamente que aceita `application/json` de um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="c3550-111">The result creates an auto-populated a template that accepts `application/json` from a logic app.</span></span> <span data-ttu-id="c3550-112">As funções que você cria desses modelos são automaticamente detectadas e listadas no Designer de Aplicativos Lógicos em **Azure Functions em minha região.**</span><span class="sxs-lookup"><span data-stu-id="c3550-112">Functions that you create from these templates are automatically detected and appear in the Logic App Designer under **Azure Functions in my region.**</span></span>

<span data-ttu-id="c3550-113">No Portal do Azure, no painel **Integrar** de sua função, o modelo deve mostrar que **Modo** está definido como **Webhook** e o **Tipo do Webhook** está definido como **JSON Genérico**.</span><span class="sxs-lookup"><span data-stu-id="c3550-113">In the Azure portal, on the **Integrate** pane for your function, your template should show that **Mode** set to **Webhook** and **Webhook type** is set to **Generic JSON**.</span></span> 

<span data-ttu-id="c3550-114">As funções do Webhook aceitam uma solicitação e passam-na para o método por meio de uma variável `data` .</span><span class="sxs-lookup"><span data-stu-id="c3550-114">Webhook functions accept a request and pass it into the method via a `data` variable.</span></span> <span data-ttu-id="c3550-115">Você pode acessar as propriedades do conteúdo usando uma notação de ponto como `data.function-name`.</span><span class="sxs-lookup"><span data-stu-id="c3550-115">You can access the properties of your payload by using dot notation like `data.function-name`.</span></span> <span data-ttu-id="c3550-116">Por exemplo, uma função Javascript simples, que converte um valor DateTime em uma cadeia de caracteres de data, terá a seguinte aparência:</span><span class="sxs-lookup"><span data-stu-id="c3550-116">For example, a simple JavaScript function that converts a DateTime value into a date string looks like the following example:</span></span>

```
function start(req, res){
    var data = req.body;
    res = {
        body: data.date.ToDateString();
    }
}
```

## <a name="call-azure-functions-from-logic-apps"></a><span data-ttu-id="c3550-117">Chamar o Azure Functions de aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="c3550-117">Call Azure Functions from logic apps</span></span>

<span data-ttu-id="c3550-118">Para listar os contêineres em sua assinatura e selecionar a função que você deseja chamar, no Designer de Aplicativos Lógicos, clique no menu **Ações** e selecione **Azure Functions na minha Região**.</span><span class="sxs-lookup"><span data-stu-id="c3550-118">To list the containers in your subscription and select the function that you want to call, in Logic App Designer, click the **Actions** menu, and select from **Azure Functions in my Region**.</span></span>

<span data-ttu-id="c3550-119">Depois de escolher a função, será solicitado que você especifique um objeto de conteúdo de entrada.</span><span class="sxs-lookup"><span data-stu-id="c3550-119">After you select the function, you are asked to specify an input payload object.</span></span> <span data-ttu-id="c3550-120">Esse objeto é a mensagem que o aplicativo lógico envia para a função e deve ser um objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="c3550-120">This object is the message that the logic app sends to the function and must be a JSON object.</span></span> <span data-ttu-id="c3550-121">Por exemplo, se você quiser passar a data da **Última Modificação** de um gatilho Salesforce, o conteúdo da função poderá ser como neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="c3550-121">For example, if you want to pass in the **Last Modified** date from a Salesforce trigger, the function payload might look like this example:</span></span>

![Data da última modificação][1]

## <a name="trigger-logic-apps-from-a-function"></a><span data-ttu-id="c3550-123">Disparar aplicativos lógicos a partir de uma função</span><span class="sxs-lookup"><span data-stu-id="c3550-123">Trigger logic apps from a function</span></span>

<span data-ttu-id="c3550-124">Você pode disparar um aplicativo lógico de dentro de uma função.</span><span class="sxs-lookup"><span data-stu-id="c3550-124">You can trigger a logic app from inside a function.</span></span> <span data-ttu-id="c3550-125">Constule [Aplicativos lógicos como pontos de extremidade escaláveis](logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="c3550-125">See [Logic apps as callable endpoints](logic-apps-http-endpoint.md).</span></span> <span data-ttu-id="c3550-126">Crie um aplicativo lógico que tenha um gatilho manual, em seguida, de dentro de sua função, gere um POST HTTP para a URL do gatilho manual com o conteúdo que você deseja enviar para o aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="c3550-126">Create a logic app that has a manual trigger, then from inside your function, generate an HTTP POST to the manual trigger URL with the payload that you want sent to the logic app.</span></span>

### <a name="create-a-function-from-logic-app-designer"></a><span data-ttu-id="c3550-127">Criar uma função do Designer de Aplicativos Lógicos</span><span class="sxs-lookup"><span data-stu-id="c3550-127">Create a function from Logic App Designer</span></span>

<span data-ttu-id="c3550-128">Você também pode criar uma função de webhook do node.js de dentro do designer.</span><span class="sxs-lookup"><span data-stu-id="c3550-128">You can also create a node.js webhook function from the designer.</span></span> <span data-ttu-id="c3550-129">Primeiro, selecione **Azure Functions em minha região** , em seguida, escolha um contêiner de sua função.</span><span class="sxs-lookup"><span data-stu-id="c3550-129">First, select **Azure Functions in my Region,** and then choose a container for your function.</span></span> <span data-ttu-id="c3550-130">Se você ainda não tiver um contêiner, precisará criar um a partir do [portal das Azure Functions](https://functions.azure.com/signin).</span><span class="sxs-lookup"><span data-stu-id="c3550-130">If you don't yet have a container, you need to create one from the [Azure Functions portal](https://functions.azure.com/signin).</span></span> <span data-ttu-id="c3550-131">Em seguida, selecione **Criar Novo**.</span><span class="sxs-lookup"><span data-stu-id="c3550-131">Then select **Create New**.</span></span>  

<span data-ttu-id="c3550-132">Para gerar um modelo com base nos dados que você deseja calcular, especifique o objeto de contexto que planeja passar para uma função.</span><span class="sxs-lookup"><span data-stu-id="c3550-132">To generate a template based on the data that you want to compute, specify the context object that you plan to pass into a function.</span></span> <span data-ttu-id="c3550-133">Esse objeto deve ser um objeto JSON.</span><span class="sxs-lookup"><span data-stu-id="c3550-133">This object must be a JSON object.</span></span> <span data-ttu-id="c3550-134">Por exemplo, se você passar o conteúdo do arquivo por meio de uma ação FTP, o conteúdo do contexto ficará como neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="c3550-134">For example, if you pass in the file content from an FTP action, the context payload looks like this example:</span></span>

![Conteúdo do contexto][2]

> [!NOTE]
> <span data-ttu-id="c3550-136">Como esse objeto não foi convertido em uma cadeia de caracteres, o conteúdo é adicionado diretamente ao conteúdo JSON.</span><span class="sxs-lookup"><span data-stu-id="c3550-136">Because this object wasn't cast as a string, the content is added directly to the JSON payload.</span></span> <span data-ttu-id="c3550-137">No entanto, um erro ocorrerá se o objeto não for um token JSON (ou seja, uma cadeia de caracteres ou um objeto/matriz JSON).</span><span class="sxs-lookup"><span data-stu-id="c3550-137">However, an error occurs if the object is not a JSON token (that is, a string or a JSON object/array).</span></span> <span data-ttu-id="c3550-138">Para converter o objeto em uma cadeia de caracteres, adicione aspas conforme mostrado na primeira ilustração neste artigo.</span><span class="sxs-lookup"><span data-stu-id="c3550-138">To cast the object as a string, add quotes as shown in the first illustration in this article.</span></span>
> 

<span data-ttu-id="c3550-139">Então, o designer irá gerar um modelo de função que você poderá criar embutido.</span><span class="sxs-lookup"><span data-stu-id="c3550-139">The designer then generates a function template that you can create inline.</span></span> <span data-ttu-id="c3550-140">As variáveis são previamente criadas com base no contexto que você planeja passar para a função.</span><span class="sxs-lookup"><span data-stu-id="c3550-140">Variables are pre-created based on the context that you plan to pass into the function.</span></span>

<!--Image references-->
[1]: ./media/logic-apps-azure-functions/callfunction.png
[2]: ./media/logic-apps-azure-functions/createfunction.png
