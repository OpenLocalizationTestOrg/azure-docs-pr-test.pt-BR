---
title: "aaaCreate, criar e implantar aplicativos lógicos no Visual Studio - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Crie projetos do Visual Studio para projetar, compilar e implantar Aplicativo Lógico do Azure."
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: e484e5ce-77e9-4fa9-bcbe-f851b4eb42a6
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 2/14/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 5154cb05f9a48e9f0f2381a6953947217f7bb114
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="design-build-and-deploy-azure-logic-apps-in-visual-studio"></a><span data-ttu-id="cedcd-103">Criar, compilar e implantar Aplicativo Lógico do Azure no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cedcd-103">Design, build, and deploy Azure Logic Apps in Visual Studio</span></span>

<span data-ttu-id="cedcd-104">Embora hello [portal do Azure](https://portal.azure.com/) oferece uma ótima maneira de você toocreate e gerenciar os aplicativos lógicos do Azure, você pode usar o Visual Studio para projetar, desenvolver e implantar seus aplicativos lógicos.</span><span class="sxs-lookup"><span data-stu-id="cedcd-104">Although hello [Azure portal](https://portal.azure.com/) offers a great way for you toocreate and manage Azure Logic Apps, you can use Visual Studio for designing, building, and deploying your logic apps.</span></span> <span data-ttu-id="cedcd-105">Visual Studio fornece ferramentas avançadas como Olá Designer de lógica do aplicativo para você toocreate os aplicativos lógicos, configurar modelos de implantação e a automação e implantar o ambiente tooany.</span><span class="sxs-lookup"><span data-stu-id="cedcd-105">Visual Studio provides rich tools like hello Logic App Designer for you toocreate logic apps, configure deployment and automation templates, and deploy tooany environment.</span></span> 

<span data-ttu-id="cedcd-106">Saiba tooget iniciada com os aplicativos lógicos do Azure, [como toocreate seu primeiro aplicativo lógica no portal do Azure de saudação](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="cedcd-106">tooget started with Azure Logic Apps, learn [how toocreate your first logic app in hello Azure portal](logic-apps-create-a-logic-app.md).</span></span>

## <a name="installation-steps"></a><span data-ttu-id="cedcd-107">Etapas de instalação</span><span class="sxs-lookup"><span data-stu-id="cedcd-107">Installation steps</span></span>

<span data-ttu-id="cedcd-108">tooinstall e configurar as ferramentas do Visual Studio para aplicativos do Azure lógica, siga estas etapas.</span><span class="sxs-lookup"><span data-stu-id="cedcd-108">tooinstall and configure Visual Studio tools for Azure Logic Apps, follow these steps.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="cedcd-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="cedcd-109">Prerequisites</span></span>

* <span data-ttu-id="cedcd-110">[Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) ou Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="cedcd-110">[Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) or Visual Studio 2015</span></span>
* <span data-ttu-id="cedcd-111">[SDK mais recente do Azure](https://azure.microsoft.com/downloads/) (2.9.1 ou superior)</span><span class="sxs-lookup"><span data-stu-id="cedcd-111">[Latest Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 or greater)</span></span>
* [<span data-ttu-id="cedcd-112">PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="cedcd-112">Azure PowerShell</span></span>](https://github.com/Azure/azure-powershell#installation)
* <span data-ttu-id="cedcd-113">Web toohello de acesso ao usar o designer incorporado Olá</span><span class="sxs-lookup"><span data-stu-id="cedcd-113">Access toohello web when using hello embedded designer</span></span>

### <a name="install-visual-studio-tools-for-azure-logic-apps"></a><span data-ttu-id="cedcd-114">Instalar ferramentas do Visual Studio para Aplicativos Lógicos do Azure</span><span class="sxs-lookup"><span data-stu-id="cedcd-114">Install Visual Studio tools for Azure Logic Apps</span></span>

<span data-ttu-id="cedcd-115">Depois de instalar os pré-requisitos de saudação:</span><span class="sxs-lookup"><span data-stu-id="cedcd-115">After you install hello prerequisites:</span></span>

1. <span data-ttu-id="cedcd-116">Abra o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cedcd-116">Open Visual Studio.</span></span> <span data-ttu-id="cedcd-117">Em Olá **ferramentas** menu, selecione **extensões e atualizações**.</span><span class="sxs-lookup"><span data-stu-id="cedcd-117">On hello **Tools** menu, select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="cedcd-118">Expanda Olá **Online** categoria para que você pode pesquisar online.</span><span class="sxs-lookup"><span data-stu-id="cedcd-118">Expand hello **Online** category so you can search online.</span></span>
3. <span data-ttu-id="cedcd-119">Procure por **Aplicativos Lógicos** até encontrar as **Ferramentas de Aplicativos Lógicos do Azure para Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="cedcd-119">Browse or search for **Logic Apps** until you find **Azure Logic Apps Tools for Visual Studio**.</span></span>
4. <span data-ttu-id="cedcd-120">toodownload e extensão de saudação de instalação, clique em **baixar**.</span><span class="sxs-lookup"><span data-stu-id="cedcd-120">toodownload and install hello extension, click **Download**.</span></span>
5. <span data-ttu-id="cedcd-121">Reinicie o Visual Studio após a instalação.</span><span class="sxs-lookup"><span data-stu-id="cedcd-121">Restart Visual Studio after installation.</span></span>

> [!NOTE]
> <span data-ttu-id="cedcd-122">Você também pode baixar [ferramentas de aplicativos de lógica do Azure para Visual Studio de 2017](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551) e hello [ferramentas de aplicativos de lógica do Azure para Visual Studio 2015](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio) diretamente do Visual Studio Marketplace de saudação.</span><span class="sxs-lookup"><span data-stu-id="cedcd-122">You can also download [Azure Logic Apps Tools for Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551) and hello [Azure Logic Apps Tools for Visual Studio 2015](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio) directly from hello Visual Studio Marketplace.</span></span>

<span data-ttu-id="cedcd-123">Depois de concluir a instalação, você pode usar o projeto do grupo de recursos do Azure Olá com o Designer de lógica do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cedcd-123">After you finish installation, you can use hello Azure Resource Group project with Logic App Designer.</span></span>

## <a name="create-your-project"></a><span data-ttu-id="cedcd-124">Criar seu projeto</span><span class="sxs-lookup"><span data-stu-id="cedcd-124">Create your project</span></span>

1. <span data-ttu-id="cedcd-125">Em Olá **arquivo** menu Ir muito**novo**e selecione **projeto**.</span><span class="sxs-lookup"><span data-stu-id="cedcd-125">On hello **File** menu, go too**New**, and select **Project**.</span></span> <span data-ttu-id="cedcd-126">Ou tooadd seu tooan projeto existente a solução, ir muito**adicionar**e selecione **novo projeto**.</span><span class="sxs-lookup"><span data-stu-id="cedcd-126">Or tooadd your project tooan existing solution, go too**Add**, and select **New Project**.</span></span>

    ![Menu Arquivo](./media/logic-apps-deploy-from-vs/filemenu.png)

2. <span data-ttu-id="cedcd-128">Em Olá **novo projeto** janela, localizar **nuvem**e selecione **o grupo de recursos do Azure**.</span><span class="sxs-lookup"><span data-stu-id="cedcd-128">In hello **New Project** window, find **Cloud**, and select **Azure Resource Group**.</span></span> <span data-ttu-id="cedcd-129">Nomeie seu projeto e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="cedcd-129">Name your project, and click **OK**.</span></span>

    ![Adicionar novo projeto](./media/logic-apps-deploy-from-vs/addnewproject.png)

3. <span data-ttu-id="cedcd-131">Selecione Olá **aplicativo lógico** modelo, que cria um modelo de implantação de aplicativo em branco lógica de toouse.</span><span class="sxs-lookup"><span data-stu-id="cedcd-131">Select hello **Logic App** template, which creates a blank logic app deployment template for you toouse.</span></span> <span data-ttu-id="cedcd-132">Após selecionar o modelo, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="cedcd-132">After you select your template, click **OK**.</span></span>

    ![Selecione o modelo Aplicativo Lógico](./media/logic-apps-deploy-from-vs/selectazuretemplate1.png)

    <span data-ttu-id="cedcd-134">Você adicionou agora sua solução de tooyour de projeto de aplicativo de lógica.</span><span class="sxs-lookup"><span data-stu-id="cedcd-134">You've now added your logic app project tooyour solution.</span></span> 
    <span data-ttu-id="cedcd-135">No Gerenciador de soluções do hello, o arquivo de implantação deve aparecer.</span><span class="sxs-lookup"><span data-stu-id="cedcd-135">In hello Solution Explorer, your deployment file should appear.</span></span>

    ![Arquivo de implantação](./media/logic-apps-deploy-from-vs/deployment.png)

## <a name="create-your-logic-app-with-logic-app-designer"></a><span data-ttu-id="cedcd-137">Criar seu aplicativo lógico com o Designer de Aplicativos Lógicos</span><span class="sxs-lookup"><span data-stu-id="cedcd-137">Create your logic app with Logic App Designer</span></span>

<span data-ttu-id="cedcd-138">Quando você tiver um projeto de grupo de recursos do Azure que contém um aplicativo lógico, você pode abrir Olá lógica de aplicativo Designer no Visual Studio toocreate o fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="cedcd-138">When you have an Azure Resource Group project that contains a logic app, you can open hello Logic App Designer in Visual Studio toocreate your workflow.</span></span> 

> [!NOTE]
> <span data-ttu-id="cedcd-139">designer de saudação requer uma conexão de internet de consulta muito conectores para dados e propriedades disponíveis.</span><span class="sxs-lookup"><span data-stu-id="cedcd-139">hello designer requires an internet connection too query connectors for available properties and data.</span></span> <span data-ttu-id="cedcd-140">Por exemplo, se você usar o conector do Dynamics CRM Online hello, designer de saudação consulta o CRM instância tooshow disponíveis e personalizados propriedades padrão.</span><span class="sxs-lookup"><span data-stu-id="cedcd-140">For example, if you use hello Dynamics CRM Online connector, hello designer queries your CRM instance tooshow available custom and default properties.</span></span>

1. <span data-ttu-id="cedcd-141">Clique com o botão direito do mouse no arquivo `<template>.json` e selecione **Abrir com o Designer de Aplicativo Lógico**.</span><span class="sxs-lookup"><span data-stu-id="cedcd-141">Right-click your `<template>.json` file, and select **Open with Logic App Designer**.</span></span> <span data-ttu-id="cedcd-142">(`Ctrl+L`)</span><span class="sxs-lookup"><span data-stu-id="cedcd-142">(`Ctrl+L`)</span></span>

2. <span data-ttu-id="cedcd-143">Escolha a assinatura do Azure, grupo de recursos e local para seu modelo de implantação.</span><span class="sxs-lookup"><span data-stu-id="cedcd-143">Choose your Azure subscription, resource group, and location for your deployment template.</span></span>

    > [!NOTE]
    > <span data-ttu-id="cedcd-144">A criação de um aplicativo lógico cria recursos de Conexão da API que consultam propriedades durante o design.</span><span class="sxs-lookup"><span data-stu-id="cedcd-144">Designing a logic app creates API Connection resources that query for properties during design.</span></span> <span data-ttu-id="cedcd-145">O Visual Studio usa essas conexões seu toocreate do grupo de recursos selecionado durante o tempo de design.</span><span class="sxs-lookup"><span data-stu-id="cedcd-145">Visual Studio uses your selected resource group toocreate those connections during design time.</span></span> <span data-ttu-id="cedcd-146">tooview ou alterar quaisquer conexões de API, vá toohello portal do Azure e procurar **API conexões**.</span><span class="sxs-lookup"><span data-stu-id="cedcd-146">tooview or change any API Connections, go toohello Azure portal, and browse for **API Connections**.</span></span>

    ![Seletor de assinatura](./media/logic-apps-deploy-from-vs/designer_picker.png)

    <span data-ttu-id="cedcd-148">designer Olá usa definição Olá em Olá `<template>.json` arquivo para renderização.</span><span class="sxs-lookup"><span data-stu-id="cedcd-148">hello designer uses hello definition in hello `<template>.json` file for rendering.</span></span>

4. <span data-ttu-id="cedcd-149">Crie e projete seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="cedcd-149">Create and design your logic app.</span></span> <span data-ttu-id="cedcd-150">Seu modelo de implantação é atualizado com suas alterações.</span><span class="sxs-lookup"><span data-stu-id="cedcd-150">Your deployment template is updated with your changes.</span></span>

    ![Designer de Aplicativo Lógico no Visual Studio](./media/logic-apps-deploy-from-vs/designer_in_vs.png)

<span data-ttu-id="cedcd-152">O Visual Studio adiciona `Microsoft.Web/connections` muito o recurso de arquivo de recursos para todas as conexões toofunction precisa de seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="cedcd-152">Visual Studio adds `Microsoft.Web/connections` resources too your resource file for any connections your logic app needs toofunction.</span></span> <span data-ttu-id="cedcd-153">Essas propriedades de conexão podem ser definidas quando você implanta e gerenciadas depois de implantar no **API conexões** em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="cedcd-153">These connection properties can be set when you deploy, and managed after you deploy in **API Connections** in hello Azure portal.</span></span>

### <a name="switch-toojson-code-view"></a><span data-ttu-id="cedcd-154">Alternar o modo de exibição de código tooJSON</span><span class="sxs-lookup"><span data-stu-id="cedcd-154">Switch tooJSON code view</span></span>

<span data-ttu-id="cedcd-155">Olá tooshow representação JSON para seu aplicativo lógico, selecione Olá **visualização de código** guia na parte inferior de saudação do designer de saudação.</span><span class="sxs-lookup"><span data-stu-id="cedcd-155">tooshow hello JSON representation for your logic app, select hello **Code View** tab at hello bottom of hello designer.</span></span>

<span data-ttu-id="cedcd-156">tooswitch novamente toohello completo de recursos JSON, clique com botão direito Olá `<template>.json` de arquivo e selecione **abrir**.</span><span class="sxs-lookup"><span data-stu-id="cedcd-156">tooswitch back toohello full resource JSON, right-click hello `<template>.json` file, and select **Open**.</span></span>

### <a name="add-references-for-dependent-resources-toovisual-studio-deployment-templates"></a><span data-ttu-id="cedcd-157">Adicionar referências para modelos de implantação recursos dependentes tooVisual Studio</span><span class="sxs-lookup"><span data-stu-id="cedcd-157">Add references for dependent resources tooVisual Studio deployment templates</span></span>

<span data-ttu-id="cedcd-158">Quando você deseja que sua lógica aplicativo tooreference os recursos dependentes, você pode usar [funções de modelo do Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions) no seu modelo de implantação do aplicativo de lógica.</span><span class="sxs-lookup"><span data-stu-id="cedcd-158">When you want your logic app tooreference dependent resources, you can use [Azure Resource Manager template functions](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions) in your logic app deployment template.</span></span> <span data-ttu-id="cedcd-159">Por exemplo, convém seu aplicativo de lógica tooreference uma conta de função do Azure ou de integração que você deseja toodeploy juntamente com seu aplicativo lógica.</span><span class="sxs-lookup"><span data-stu-id="cedcd-159">For example, you might want your logic app tooreference an Azure Function or integration account that you want toodeploy alongside your logic app.</span></span> <span data-ttu-id="cedcd-160">Siga estas diretrizes sobre como os parâmetros de toouse em seu modelo de implantação para que Olá lógica de aplicativo Designer renderiza corretamente.</span><span class="sxs-lookup"><span data-stu-id="cedcd-160">Follow these guidelines about how toouse parameters in your deployment template so that hello Logic App Designer renders correctly.</span></span> 

<span data-ttu-id="cedcd-161">Você pode usar parâmetros do aplicativo lógico nesses tipos de gatilhos e ações:</span><span class="sxs-lookup"><span data-stu-id="cedcd-161">You can use logic app parameters in these kinds of triggers and actions:</span></span>

*   <span data-ttu-id="cedcd-162">Fluxo de trabalho filho</span><span class="sxs-lookup"><span data-stu-id="cedcd-162">Child workflow</span></span>
*   <span data-ttu-id="cedcd-163">Aplicativo de funções</span><span class="sxs-lookup"><span data-stu-id="cedcd-163">Function app</span></span>
*   <span data-ttu-id="cedcd-164">Chamada APIM</span><span class="sxs-lookup"><span data-stu-id="cedcd-164">APIM call</span></span>
*   <span data-ttu-id="cedcd-165">URL do tempo de execução da conexão de API</span><span class="sxs-lookup"><span data-stu-id="cedcd-165">API connection runtime URL</span></span>
*   <span data-ttu-id="cedcd-166">Caminho de conexão da API</span><span class="sxs-lookup"><span data-stu-id="cedcd-166">API connection path</span></span>

<span data-ttu-id="cedcd-167">E você pode utilizar funções de modelo, como parâmetros, variáveis, resourceId, concat, etc. Por exemplo, aqui está como você pode substituir Olá ID de recurso de função do Azure:</span><span class="sxs-lookup"><span data-stu-id="cedcd-167">And you can use template functions such as parameters, variables, resourceId, concat, etc. For example, here's how you can replace hello Azure Function resource ID:</span></span>

```
"parameters":{
    "functionName": {
        "type":"string",
        "minLength":1,
        "defaultValue":"<FunctionName>"
    }
},
```

<span data-ttu-id="cedcd-168">E onde os parâmetros seriam utilizados:</span><span class="sxs-lookup"><span data-stu-id="cedcd-168">And where you would use parameters:</span></span>

```
"MyFunction": {
    "type": "Function",
    "inputs": {
        "body":{},
        "function":{
            "id":"[resourceid('Microsoft.Web/sites/functions','functionApp',parameters('functionName'))]"
        }
    },
    "runAfter":{}
}
```
<span data-ttu-id="cedcd-169">Como outro exemplo, você pode parametrizar Olá operação de mensagem de envio do barramento de serviço:</span><span class="sxs-lookup"><span data-stu-id="cedcd-169">As another example you can parameterize hello Service Bus send message operation:</span></span>

```
"Send_message": {
    "type": "ApiConnection",
        "inputs": {
            "host": {
                "connection": {
                    "name": "@parameters('$connections')['servicebus']['connectionId']"
                }
            },
            "method": "post",
            "path": "[concat('/@{encodeURIComponent(''', parameters('queueuname'), ''')}/messages')]",
            "body": {
                "ContentData": "@{base64(triggerBody())}"
            },
            "queries": {
                "systemProperties": "None"
            }
        },
        "runAfter": {}
    }
```
> [!NOTE] 
> <span data-ttu-id="cedcd-170">host.runtimeUrl é opcional e pode ser removido do seu modelo, se houver.</span><span class="sxs-lookup"><span data-stu-id="cedcd-170">host.runtimeUrl is optional and can be removed from your template if present.</span></span>
> 


> [!NOTE] 
> <span data-ttu-id="cedcd-171">Para toowork do Designer de lógica do aplicativo hello quando você usar parâmetros, você deve fornecer valores padrão, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="cedcd-171">For hello Logic App Designer toowork when you use parameters, you must provide default values, for example:</span></span>
> 
> ```
> "parameters": {
>     "IntegrationAccount": {
>     "type":"string",
>     "minLength":1,
>     "defaultValue":"/subscriptions/<subscriptionID>/resourceGroups/<resourceGroupName>/providers/Microsoft.Logic/integrationAccounts/<integrationAccountName>"
>     }
> },
> ```

### <a name="save-your-logic-app"></a><span data-ttu-id="cedcd-172">Salve seu aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="cedcd-172">Save your logic app</span></span>

<span data-ttu-id="cedcd-173">toosave seu aplicativo lógico a qualquer momento, vá muito**arquivo** > **salvar**.</span><span class="sxs-lookup"><span data-stu-id="cedcd-173">toosave your logic app at anytime, go too**File** > **Save**.</span></span> <span data-ttu-id="cedcd-174">(`Ctrl+S`)</span><span class="sxs-lookup"><span data-stu-id="cedcd-174">(`Ctrl+S`)</span></span> 

<span data-ttu-id="cedcd-175">Se seu aplicativo lógico tem erros quando você salvar seu aplicativo, eles aparecem no hello Visual Studio **saídas** janela.</span><span class="sxs-lookup"><span data-stu-id="cedcd-175">If your logic app has any errors when you save your app, they appear in hello Visual Studio **Outputs** window.</span></span>

## <a name="deploy-your-logic-app-from-visual-studio"></a><span data-ttu-id="cedcd-176">Implantar seu aplicativo lógico por meio do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cedcd-176">Deploy your logic app from Visual Studio</span></span>

<span data-ttu-id="cedcd-177">Após configurar seu aplicativo, você pode implantar diretamente do Visual Studio em apenas algumas etapas.</span><span class="sxs-lookup"><span data-stu-id="cedcd-177">After configuring your app, you can deploy directly from Visual Studio in just a couple steps.</span></span> 

1. <span data-ttu-id="cedcd-178">No Gerenciador de soluções, clique com o botão direito e vá muito**implantar** > **nova implantação...**</span><span class="sxs-lookup"><span data-stu-id="cedcd-178">In Solution Explorer, right-click your project, and go too**Deploy** > **New Deployment...**</span></span>

    ![Nova implantação](./media/logic-apps-deploy-from-vs/newdeployment.png)

2. <span data-ttu-id="cedcd-180">Quando você for solicitado, entre tooyour assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="cedcd-180">When you're prompted, sign in tooyour Azure subscription.</span></span> 

3. <span data-ttu-id="cedcd-181">Agora você deve selecionar detalhes de Olá Olá para grupo de recursos onde você deseja toodeploy seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="cedcd-181">Now you must select hello details for hello resource group where you want toodeploy your logic app.</span></span> <span data-ttu-id="cedcd-182">Quando terminar, selecione **Implantar**.</span><span class="sxs-lookup"><span data-stu-id="cedcd-182">When you're done, select **Deploy**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="cedcd-183">Certifique-se de que você selecione o modelo correto hello e arquivo de parâmetros para o grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="cedcd-183">Make sure that you select hello correct template and parameters file for hello resource group.</span></span> <span data-ttu-id="cedcd-184">Por exemplo, se desejar que o ambiente de produção tooa toodeploy, escolha o arquivo de parâmetros de produção de hello.</span><span class="sxs-lookup"><span data-stu-id="cedcd-184">For example, if you want toodeploy tooa production environment, choose hello production parameters file.</span></span>

    ![Implantar grupo tooresource](./media/logic-apps-deploy-from-vs/deploytoresourcegroup.png)

    <span data-ttu-id="cedcd-186">status da implantação Olá aparece no hello **saída** janela.</span><span class="sxs-lookup"><span data-stu-id="cedcd-186">hello deployment status appears in hello **Output** window.</span></span> 
    <span data-ttu-id="cedcd-187">Você pode ter tooselect **Azure provisionamento** em Olá **Mostrar saída de** lista.</span><span class="sxs-lookup"><span data-stu-id="cedcd-187">You might have tooselect **Azure Provisioning** in hello **Show output from** list.</span></span>

    ![Saída Status da implantação](./media/logic-apps-deploy-from-vs/output.png)

<span data-ttu-id="cedcd-189">Olá futura, você pode editar o aplicativo lógico no controle de origem e usar as novas versões do Visual Studio toodeploy.</span><span class="sxs-lookup"><span data-stu-id="cedcd-189">In hello future, you can edit your logic app in source control, and use Visual Studio toodeploy new versions.</span></span>

> [!NOTE]
> <span data-ttu-id="cedcd-190">Se você alterar a definição de saudação em Olá portal do Azure diretamente, essas alterações serão substituídas quando você implanta no Visual Studio próxima vez.</span><span class="sxs-lookup"><span data-stu-id="cedcd-190">If you change hello definition in hello Azure portal directly, those changes are overwritten when you deploy from Visual Studio next time.</span></span> 

## <a name="add-your-logic-app-tooan-existing-resource-group-project"></a><span data-ttu-id="cedcd-191">Adicionar projeto de grupo de recursos existente sua lógica aplicativo tooan</span><span class="sxs-lookup"><span data-stu-id="cedcd-191">Add your logic app tooan existing Resource Group project</span></span>

<span data-ttu-id="cedcd-192">Se você tiver um projeto existente do grupo de recursos, você pode adicionar seu projeto de toothat aplicativo lógica na janela de estrutura de tópicos do JSON hello.</span><span class="sxs-lookup"><span data-stu-id="cedcd-192">If you have an existing Resource Group project, you can add your logic app toothat project in hello JSON Outline window.</span></span> <span data-ttu-id="cedcd-193">Você também pode adicionar outro aplicativo lógico juntamente com o aplicativo hello criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="cedcd-193">You can also add another logic app alongside hello app you previously created.</span></span>

1. <span data-ttu-id="cedcd-194">Olá abrir `<template>.json` arquivo.</span><span class="sxs-lookup"><span data-stu-id="cedcd-194">Open hello `<template>.json` file.</span></span>

2. <span data-ttu-id="cedcd-195">Olá tooopen janela estrutura de tópicos de JSON, ir muito**exibição** > **outras janelas** > **JSON tópicos**.</span><span class="sxs-lookup"><span data-stu-id="cedcd-195">tooopen hello JSON Outline window, go too**View** > **Other Windows** > **JSON Outline**.</span></span>

3. <span data-ttu-id="cedcd-196">tooadd um arquivo de modelo de toohello de recursos, clique em **adicionar recurso** na parte superior de saudação da janela de estrutura de JSON de saudação.</span><span class="sxs-lookup"><span data-stu-id="cedcd-196">tooadd a resource toohello template file, click **Add Resource** at hello top of hello JSON Outline window.</span></span> <span data-ttu-id="cedcd-197">Ou na janela de estrutura de tópicos do JSON hello, clique com botão direito **recursos**e selecione **adicionar novo recurso**.</span><span class="sxs-lookup"><span data-stu-id="cedcd-197">Or in hello JSON Outline window, right-click **resources**, and select **Add New Resource**.</span></span>

    ![Janela Estrutura de tópicos JSON](./media/logic-apps-deploy-from-vs/jsonoutline.png)
    
4. <span data-ttu-id="cedcd-199">Em Olá **adicionar recurso** caixa de diálogo, encontre e selecione **aplicativo lógico**.</span><span class="sxs-lookup"><span data-stu-id="cedcd-199">In hello **Add Resource** dialog box, find and select **Logic App**.</span></span> <span data-ttu-id="cedcd-200">Nomeie seu aplicativo lógico e escolha **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="cedcd-200">Name your logic app, and choose **Add**.</span></span>

    ![Adicionar recurso](./media/logic-apps-deploy-from-vs/addresource.png)

## <a name="next-steps"></a><span data-ttu-id="cedcd-202">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cedcd-202">Next Steps</span></span>

* [<span data-ttu-id="cedcd-203">Gerenciar aplicativos lógicos com o Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="cedcd-203">Manage logic apps with Visual Studio Cloud Explorer</span></span>](logic-apps-manage-from-vs.md)
* [<span data-ttu-id="cedcd-204">Veja exemplos e cenários comuns</span><span class="sxs-lookup"><span data-stu-id="cedcd-204">View common examples and scenarios</span></span>](logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="cedcd-205">Saiba como os processos de negócios de tooautomate com os aplicativos lógicos do Azure</span><span class="sxs-lookup"><span data-stu-id="cedcd-205">Learn how tooautomate business processes with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/T694)
* [<span data-ttu-id="cedcd-206">Saiba como toointegrate seus sistemas com os aplicativos lógicos do Azure</span><span class="sxs-lookup"><span data-stu-id="cedcd-206">Learn how toointegrate your systems with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/P462)
