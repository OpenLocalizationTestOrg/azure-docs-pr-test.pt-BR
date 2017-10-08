---
title: modelo do Gerenciador de recursos do Azure aaaExport | Microsoft Docs
description: Use o gerenciamento de recursos do Azure tooexport um modelo de um grupo de recursos existente.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 5f5ca940-eef8-4125-b6a0-f44ba04ab5ab
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/06/2017
ms.author: tomfitz
ms.openlocfilehash: 94daa4812da2fec705044ca31c8e74e6d59bd53f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="export-an-azure-resource-manager-template-from-existing-resources"></a><span data-ttu-id="b98d1-103">Exportar um modelo do Azure Resource Manager a partir dos recursos existentes</span><span class="sxs-lookup"><span data-stu-id="b98d1-103">Export an Azure Resource Manager template from existing resources</span></span>
<span data-ttu-id="b98d1-104">Neste artigo, você aprenderá como tooexport um modelo do Gerenciador de recursos de recursos existentes em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="b98d1-104">In this article, you learn how tooexport a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="b98d1-105">Você pode usar esse toogain modelo gerado uma melhor compreensão da sintaxe de modelo.</span><span class="sxs-lookup"><span data-stu-id="b98d1-105">You can use that generated template toogain a better understanding of template syntax.</span></span>

<span data-ttu-id="b98d1-106">Há dois tooexport de maneiras de um modelo:</span><span class="sxs-lookup"><span data-stu-id="b98d1-106">There are two ways tooexport a template:</span></span>

* <span data-ttu-id="b98d1-107">Você pode exportar Olá **real usado para implantação do modelo**.</span><span class="sxs-lookup"><span data-stu-id="b98d1-107">You can export hello **actual template used for deployment**.</span></span> <span data-ttu-id="b98d1-108">modelo exportado Olá inclui todas as variáveis e parâmetros de saudação exatamente como eles eram exibidos no modelo original hello.</span><span class="sxs-lookup"><span data-stu-id="b98d1-108">hello exported template includes all hello parameters and variables exactly as they appeared in hello original template.</span></span> <span data-ttu-id="b98d1-109">Essa abordagem é útil quando você implantou recursos por meio do portal hello e deseja toosee Olá modelo toocreate esses recursos.</span><span class="sxs-lookup"><span data-stu-id="b98d1-109">This approach is helpful when you deployed resources through hello portal, and want toosee hello template toocreate those resources.</span></span> <span data-ttu-id="b98d1-110">Este modelo é facilmente utilizável.</span><span class="sxs-lookup"><span data-stu-id="b98d1-110">This template is readily usable.</span></span> 
* <span data-ttu-id="b98d1-111">Você pode exportar um **gerado do modelo que representa o estado atual de saudação do grupo de recursos de saudação**.</span><span class="sxs-lookup"><span data-stu-id="b98d1-111">You can export a **generated template that represents hello current state of hello resource group**.</span></span> <span data-ttu-id="b98d1-112">modelo exportado Olá não é baseado em qualquer modelo que você usou para a implantação.</span><span class="sxs-lookup"><span data-stu-id="b98d1-112">hello exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="b98d1-113">Em vez disso, ele cria um modelo que é um instantâneo de saudação do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b98d1-113">Instead, it creates a template that is a snapshot of hello resource group.</span></span> <span data-ttu-id="b98d1-114">modelo exportado Olá tem muitos valores embutidos e provavelmente não tantos parâmetros quantos você definiria normalmente.</span><span class="sxs-lookup"><span data-stu-id="b98d1-114">hello exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="b98d1-115">Essa abordagem é útil quando você modificou o grupo de recursos de saudação após a implantação.</span><span class="sxs-lookup"><span data-stu-id="b98d1-115">This approach is useful when you have modified hello resource group after deployment.</span></span> <span data-ttu-id="b98d1-116">Este modelo geralmente requer modificações antes de ser usado.</span><span class="sxs-lookup"><span data-stu-id="b98d1-116">This template usually requires modifications before it is usable.</span></span>

<span data-ttu-id="b98d1-117">Este tópico mostra ambas as abordagens por meio do portal hello.</span><span class="sxs-lookup"><span data-stu-id="b98d1-117">This topic shows both approaches through hello portal.</span></span>

## <a name="deploy-resources"></a><span data-ttu-id="b98d1-118">Implantação de recursos</span><span class="sxs-lookup"><span data-stu-id="b98d1-118">Deploy resources</span></span>
<span data-ttu-id="b98d1-119">Vamos começar tooAzure de recursos que você pode usar para exportar como um modelo de implantação.</span><span class="sxs-lookup"><span data-stu-id="b98d1-119">Let's start by deploying resources tooAzure that you can use for exporting as a template.</span></span> <span data-ttu-id="b98d1-120">Se você já tiver um grupo de recursos em sua assinatura que você deseja tooexport tooa modelo, você poderá ignorar esta seção.</span><span class="sxs-lookup"><span data-stu-id="b98d1-120">If you already have a resource group in your subscription that you want tooexport tooa template, you can skip this section.</span></span> <span data-ttu-id="b98d1-121">Olá restante deste artigo presume que você implantou Olá web app e solução de banco de dados SQL mostrados nesta seção.</span><span class="sxs-lookup"><span data-stu-id="b98d1-121">hello remainder of this article assumes you have deployed hello web app and SQL database solution shown in this section.</span></span> <span data-ttu-id="b98d1-122">Se você usar uma solução diferente, sua experiência pode ser um pouco diferente, mas etapas Olá tooexport um modelo são Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="b98d1-122">If you use a different solution, your experience might be a little different, but hello steps tooexport a template are hello same.</span></span> 

1. <span data-ttu-id="b98d1-123">Em Olá [portal do Azure](https://portal.azure.com), selecione **novo**.</span><span class="sxs-lookup"><span data-stu-id="b98d1-123">In hello [Azure portal](https://portal.azure.com), select **New**.</span></span>
   
      ![Selecione Novo](./media/resource-manager-export-template/new.png)
2. <span data-ttu-id="b98d1-125">Procurar **web app + SQL** e selecioná-lo entre as opções disponíveis de saudação.</span><span class="sxs-lookup"><span data-stu-id="b98d1-125">Search for **web app + SQL** and select it from hello available options.</span></span>
   
      ![Pesquise aplicativo Web e SQL](./media/resource-manager-export-template/webapp-sql.png)

3. <span data-ttu-id="b98d1-127">Selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="b98d1-127">Select **Create**.</span></span>

      ![Selecione Criar](./media/resource-manager-export-template/create.png)

4. <span data-ttu-id="b98d1-129">Forneça valores de saudação necessária para Olá web app e o banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="b98d1-129">Provide hello required values for hello web app and SQL database.</span></span> <span data-ttu-id="b98d1-130">Selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="b98d1-130">Select **Create**.</span></span>

      ![Forneça a web e o valor SQL](./media/resource-manager-export-template/provide-web-values.png)

<span data-ttu-id="b98d1-132">implantação de saudação pode levar um minuto.</span><span class="sxs-lookup"><span data-stu-id="b98d1-132">hello deployment may take a minute.</span></span> <span data-ttu-id="b98d1-133">Após a conclusão da implantação hello, sua assinatura contém solução hello.</span><span class="sxs-lookup"><span data-stu-id="b98d1-133">After hello deployment finishes, your subscription contains hello solution.</span></span>

## <a name="view-template-from-deployment-history"></a><span data-ttu-id="b98d1-134">Visualização de modelo do histórico de implantações</span><span class="sxs-lookup"><span data-stu-id="b98d1-134">View template from deployment history</span></span>
1. <span data-ttu-id="b98d1-135">Vá toohello folha de grupo de recursos para seu novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b98d1-135">Go toohello resource group blade for your new resource group.</span></span> <span data-ttu-id="b98d1-136">Observe a que folha Olá mostra o resultado de saudação da última implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="b98d1-136">Notice that hello blade shows hello result of hello last deployment.</span></span> <span data-ttu-id="b98d1-137">Selecione este link.</span><span class="sxs-lookup"><span data-stu-id="b98d1-137">Select this link.</span></span>
   
      ![folha do grupo de recursos](./media/resource-manager-export-template/select-deployment.png)
2. <span data-ttu-id="b98d1-139">Você ver um histórico de implantações de grupo hello.</span><span class="sxs-lookup"><span data-stu-id="b98d1-139">You see a history of deployments for hello group.</span></span> <span data-ttu-id="b98d1-140">No seu caso, a folha Olá provavelmente lista apenas uma implantação.</span><span class="sxs-lookup"><span data-stu-id="b98d1-140">In your case, hello blade probably lists only one deployment.</span></span> <span data-ttu-id="b98d1-141">Selecione essa implantação.</span><span class="sxs-lookup"><span data-stu-id="b98d1-141">Select this deployment.</span></span>
   
     ![última implantação](./media/resource-manager-export-template/select-history.png)
3. <span data-ttu-id="b98d1-143">folha de saudação exibe um resumo de implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="b98d1-143">hello blade displays a summary of hello deployment.</span></span> <span data-ttu-id="b98d1-144">Olá resumo inclui o status de saudação da implantação de saudação e suas operações e valores hello fornecido para os parâmetros.</span><span class="sxs-lookup"><span data-stu-id="b98d1-144">hello summary includes hello status of hello deployment and its operations and hello values that you provided for parameters.</span></span> <span data-ttu-id="b98d1-145">modelo de saudação toosee que você usou para a implantação de saudação, selecione **exibir modelo**.</span><span class="sxs-lookup"><span data-stu-id="b98d1-145">toosee hello template that you used for hello deployment, select **View template**.</span></span>
   
     ![exibir resumo da implantação](./media/resource-manager-export-template/view-template.png)
4. <span data-ttu-id="b98d1-147">Gerenciador de recursos recupera Olá sete arquivos a seguir para você:</span><span class="sxs-lookup"><span data-stu-id="b98d1-147">Resource Manager retrieves hello following seven files for you:</span></span>
   
   1. <span data-ttu-id="b98d1-148">**Modelo** -modelo Olá que define a infraestrutura de saudação para sua solução.</span><span class="sxs-lookup"><span data-stu-id="b98d1-148">**Template** - hello template that defines hello infrastructure for your solution.</span></span> <span data-ttu-id="b98d1-149">Quando você criou a conta de armazenamento Olá por meio do portal Olá, Gerenciador de recursos usado um modelo toodeploy-lo e salva esse modelo para referência futura.</span><span class="sxs-lookup"><span data-stu-id="b98d1-149">When you created hello storage account through hello portal, Resource Manager used a template toodeploy it and saved that template for future reference.</span></span>
   2. <span data-ttu-id="b98d1-150">**Parâmetros** -um arquivo de parâmetro que você pode usar toopass em valores de durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="b98d1-150">**Parameters** - A parameter file that you can use toopass in values during deployment.</span></span> <span data-ttu-id="b98d1-151">Contém valores hello que você forneceu durante a implantação de saudação primeiro.</span><span class="sxs-lookup"><span data-stu-id="b98d1-151">It contains hello values that you provided during hello first deployment.</span></span> <span data-ttu-id="b98d1-152">Você pode alterar qualquer um desses valores ao reimplantar o modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="b98d1-152">You can change any of these values when you redeploy hello template.</span></span>
   3. <span data-ttu-id="b98d1-153">**CLI** -arquivo de script do Azure de uma interface de linha comando (CLI) que você pode usar o modelo de saudação toodeploy.</span><span class="sxs-lookup"><span data-stu-id="b98d1-153">**CLI** - An Azure command-line-interface (CLI) script file that you can use toodeploy hello template.</span></span>
   3. <span data-ttu-id="b98d1-154">**2.0 do CLI** -arquivo de script do Azure de uma interface de linha comando (CLI) que você pode usar o modelo de saudação toodeploy.</span><span class="sxs-lookup"><span data-stu-id="b98d1-154">**CLI 2.0** - An Azure command-line-interface (CLI) script file that you can use toodeploy hello template.</span></span>
   4. <span data-ttu-id="b98d1-155">**PowerShell** -arquivo de script de um Azure PowerShell que você pode usar o modelo de saudação toodeploy.</span><span class="sxs-lookup"><span data-stu-id="b98d1-155">**PowerShell** - An Azure PowerShell script file that you can use toodeploy hello template.</span></span>
   5. <span data-ttu-id="b98d1-156">**.NET** -classe .NET A que você pode usar o modelo de saudação toodeploy.</span><span class="sxs-lookup"><span data-stu-id="b98d1-156">**.NET** - A .NET class that you can use toodeploy hello template.</span></span>
   6. <span data-ttu-id="b98d1-157">**Ruby** -classe Ruby A que você pode usar o modelo de saudação toodeploy.</span><span class="sxs-lookup"><span data-stu-id="b98d1-157">**Ruby** - A Ruby class that you can use toodeploy hello template.</span></span>
      
      <span data-ttu-id="b98d1-158">arquivos de saudação estão disponíveis por meio de links em folha hello.</span><span class="sxs-lookup"><span data-stu-id="b98d1-158">hello files are available through links across hello blade.</span></span> <span data-ttu-id="b98d1-159">Por padrão, a folha de saudação exibe modelo hello.</span><span class="sxs-lookup"><span data-stu-id="b98d1-159">By default, hello blade displays hello template.</span></span>
      
       ![Exibir modelo](./media/resource-manager-export-template/see-template.png)
      
<span data-ttu-id="b98d1-161">Este modelo é modelo real Olá usado toocreate seu aplicativo web e o banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="b98d1-161">This template is hello actual template used toocreate your web app and SQL database.</span></span> <span data-ttu-id="b98d1-162">Observe que ele contém parâmetros que permitem valores diferentes de tooprovide durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="b98d1-162">Notice it contains parameters that enable you tooprovide different values during deployment.</span></span> <span data-ttu-id="b98d1-163">toolearn mais sobre a estrutura de saudação de um modelo, consulte [modelos de autoria do Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="b98d1-163">toolearn more about hello structure of a template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

## <a name="export-hello-template-from-resource-group"></a><span data-ttu-id="b98d1-164">Exportar modelo de saudação do grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="b98d1-164">Export hello template from resource group</span></span>
<span data-ttu-id="b98d1-165">Se você tiver manualmente seus recursos alterados ou adicionados recursos em várias implantações, recuperando um modelo de histórico de implantação Olá refletem não o estado atual de Olá Olá do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b98d1-165">If you have manually changed your resources or added resources in multiple deployments, retrieving a template from hello deployment history does not reflect hello current state of hello resource group.</span></span> <span data-ttu-id="b98d1-166">Esta seção mostra como tooexport um modelo que reflete Olá o estado atual do grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="b98d1-166">This section shows you how tooexport a template that reflects hello current state of hello resource group.</span></span> 

> [!NOTE]
> <span data-ttu-id="b98d1-167">Você não pode exportar um modelo para um grupo de recursos que tenha mais de 200 recursos.</span><span class="sxs-lookup"><span data-stu-id="b98d1-167">You cannot export a template for a resource group that has more than 200 resources.</span></span>
> 
> 

1. <span data-ttu-id="b98d1-168">modelo de saudação tooview para um grupo de recursos, selecione **script de automação**.</span><span class="sxs-lookup"><span data-stu-id="b98d1-168">tooview hello template for a resource group, select **Automation script**.</span></span>
   
      ![exportar grupo de recursos](./media/resource-manager-export-template/select-automation.png)
   
     <span data-ttu-id="b98d1-170">Gerenciador de recursos avalia Olá recursos no grupo de recursos de saudação e gera um modelo para esses recursos.</span><span class="sxs-lookup"><span data-stu-id="b98d1-170">Resource Manager evaluates hello resources in hello resource group, and generates a template for those resources.</span></span> <span data-ttu-id="b98d1-171">Nem todos os tipos de recurso suportam Olá exportar modelo de função.</span><span class="sxs-lookup"><span data-stu-id="b98d1-171">Not all resource types support hello export template function.</span></span> <span data-ttu-id="b98d1-172">Você verá um erro indicando que há um problema com a exportação de saudação.</span><span class="sxs-lookup"><span data-stu-id="b98d1-172">You may see an error stating that there is a problem with hello export.</span></span> <span data-ttu-id="b98d1-173">Você aprenderá como toohandle os problemas no hello [correção de problemas de exportação](#fix-export-issues) seção.</span><span class="sxs-lookup"><span data-stu-id="b98d1-173">You learn how toohandle those issues in hello [Fix export issues](#fix-export-issues) section.</span></span>
2. <span data-ttu-id="b98d1-174">Novamente, verá que você pode usar a solução de saudação tooredeploy seis arquivos de saudação.</span><span class="sxs-lookup"><span data-stu-id="b98d1-174">You again see hello six files that you can use tooredeploy hello solution.</span></span> <span data-ttu-id="b98d1-175">No entanto, esse modelo de saudação do tempo é um pouco diferente.</span><span class="sxs-lookup"><span data-stu-id="b98d1-175">However, this time hello template is a little different.</span></span> <span data-ttu-id="b98d1-176">Observe que Olá modelo gerado contém menos parâmetros do modelo de saudação na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="b98d1-176">Notice that hello generated template contains fewer parameters than hello template in previous section.</span></span> <span data-ttu-id="b98d1-177">Além disso, muitos dos valores da saudação (como o local e valores SKU) são codificados por este modelo em vez de aceitar um valor de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="b98d1-177">Also, many of hello values (like location and SKU values) are hard-coded in this template rather than accepting a parameter value.</span></span> <span data-ttu-id="b98d1-178">Antes de reutilizar esse modelo, talvez você queira tooedit Olá modelo toomake melhor uso de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="b98d1-178">Before reusing this template, you might want tooedit hello template toomake better use of parameters.</span></span> 
   
3. <span data-ttu-id="b98d1-179">Você tem duas opções para continuar toowork com esse modelo.</span><span class="sxs-lookup"><span data-stu-id="b98d1-179">You have a couple of options for continuing toowork with this template.</span></span> <span data-ttu-id="b98d1-180">Você pode baixar o modelo hello e executá-la localmente com um editor de JSON.</span><span class="sxs-lookup"><span data-stu-id="b98d1-180">You can either download hello template and work on it locally with a JSON editor.</span></span> <span data-ttu-id="b98d1-181">Ou, você pode salvar a biblioteca de tooyour modelo hello e trabalhar por meio do portal hello.</span><span class="sxs-lookup"><span data-stu-id="b98d1-181">Or, you can save hello template tooyour library and work on it through hello portal.</span></span>
   
     <span data-ttu-id="b98d1-182">Se você estiver familiarizado com o uso de um editor de JSON como [código VS](https://code.visualstudio.com/) ou [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md), talvez você prefira baixar modelo de saudação localmente e usar esse editor.</span><span class="sxs-lookup"><span data-stu-id="b98d1-182">If you are comfortable using a JSON editor like [VS Code](https://code.visualstudio.com/) or [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md), you might prefer downloading hello template locally and using that editor.</span></span> <span data-ttu-id="b98d1-183">toowork localmente, selecione **baixar**.</span><span class="sxs-lookup"><span data-stu-id="b98d1-183">toowork locally, select **Download**.</span></span>
   
      ![baixar modelo](./media/resource-manager-export-template/download-template.png)
   
     <span data-ttu-id="b98d1-185">Se você não estiver configurado com um editor de JSON, talvez você prefira editando Olá modelo por meio do portal hello.</span><span class="sxs-lookup"><span data-stu-id="b98d1-185">If you are not set up with a JSON editor, you might prefer editing hello template through hello portal.</span></span> <span data-ttu-id="b98d1-186">Olá restante este tópico presume que você salvou biblioteca de tooyour Olá modelos no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="b98d1-186">hello remainder of this topic assumes you have saved hello template tooyour library in hello portal.</span></span> <span data-ttu-id="b98d1-187">No entanto, você fazer Olá mesmo modelo toohello alterações de sintaxe se trabalhando localmente com um editor de JSON ou por meio do portal hello.</span><span class="sxs-lookup"><span data-stu-id="b98d1-187">However, you make hello same syntax changes toohello template whether working locally with a JSON editor or through hello portal.</span></span> <span data-ttu-id="b98d1-188">Selecione toowork por meio do portal hello, **adicionar toolibrary**.</span><span class="sxs-lookup"><span data-stu-id="b98d1-188">toowork through hello portal, select **Add toolibrary**.</span></span>
   
      ![Adicionar toolibrary](./media/resource-manager-export-template/add-to-library.png)
   
     <span data-ttu-id="b98d1-190">Ao adicionar uma biblioteca de toohello de modelo, atribua o modelo de saudação um nome e uma descrição.</span><span class="sxs-lookup"><span data-stu-id="b98d1-190">When adding a template toohello library, give hello template a name and description.</span></span> <span data-ttu-id="b98d1-191">Em seguida, selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="b98d1-191">Then, select **Save**.</span></span>
   
     ![definir valores de modelo](./media/resource-manager-export-template/save-library-template.png)
4. <span data-ttu-id="b98d1-193">tooview um modelo de salvo em sua biblioteca, selecione **mais serviços**, tipo **modelos** toofilter resultados, selecionados **modelos**.</span><span class="sxs-lookup"><span data-stu-id="b98d1-193">tooview a template saved in your library, select **More services**, type **Templates** toofilter results, select **Templates**.</span></span>
   
      ![localizar modelos](./media/resource-manager-export-template/find-templates.png)
5. <span data-ttu-id="b98d1-195">Selecione o modelo de saudação com nome hello que você salvou.</span><span class="sxs-lookup"><span data-stu-id="b98d1-195">Select hello template with hello name you saved.</span></span>
   
      ![selecionar modelo](./media/resource-manager-export-template/select-saved-template.png)

## <a name="customize-hello-template"></a><span data-ttu-id="b98d1-197">Personalizar o modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="b98d1-197">Customize hello template</span></span>
<span data-ttu-id="b98d1-198">trabalha de modelo Hello exportada bem que se você quiser toocreate Olá mesmo web app e o banco de dados SQL para cada implantação.</span><span class="sxs-lookup"><span data-stu-id="b98d1-198">hello exported template works fine if you want toocreate hello same web app and SQL database for every deployment.</span></span> <span data-ttu-id="b98d1-199">No entanto, o Resource Manager fornece opções para que você possa implantar modelos com muito mais flexibilidade.</span><span class="sxs-lookup"><span data-stu-id="b98d1-199">However, Resource Manager provides options so that you can deploy templates with a lot more flexibility.</span></span> <span data-ttu-id="b98d1-200">Este artigo mostra como parâmetros de tooadd para Olá banco de dados nome do administrador e senha.</span><span class="sxs-lookup"><span data-stu-id="b98d1-200">This article shows you how tooadd parameters for hello database administrator name and password.</span></span> <span data-ttu-id="b98d1-201">Você pode usar esse mesmo tooadd de abordagem mais flexibilidade para outros valores no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="b98d1-201">You can use this same approach tooadd more flexibility for other values in hello template.</span></span>

1. <span data-ttu-id="b98d1-202">modelo de saudação toocustomize, selecione **editar**.</span><span class="sxs-lookup"><span data-stu-id="b98d1-202">toocustomize hello template, select **Edit**.</span></span>
   
     ![mostrar modelo](./media/resource-manager-export-template/select-edit.png)
2. <span data-ttu-id="b98d1-204">Selecione o modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="b98d1-204">Select hello template.</span></span>
   
     ![editar modelo](./media/resource-manager-export-template/select-added-template.png)
3. <span data-ttu-id="b98d1-206">valores de saudação do toobe toopass capaz de que talvez você queira toospecify durante a implantação, adicione Olá toohello de dois parâmetros a seguir **parâmetros** seção modelo hello:</span><span class="sxs-lookup"><span data-stu-id="b98d1-206">toobe able toopass hello values that you might want toospecify during deployment, add hello following two parameters toohello **parameters** section in hello template:</span></span>

   ```json
   "administratorLogin": {
       "type": "String"
   },
   "administratorLoginPassword": {
       "type": "SecureString"
   },
   ```

4. <span data-ttu-id="b98d1-207">toouse Olá novos parâmetros, substituir definição Olá SQL server no hello **recursos** seção.</span><span class="sxs-lookup"><span data-stu-id="b98d1-207">toouse hello new parameters, replace hello SQL server definition in hello **resources** section.</span></span> <span data-ttu-id="b98d1-208">Observe que o **administratorLogin** e o **administratorLoginPassword** passaram a usar os valores de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="b98d1-208">Notice that **administratorLogin** and **administratorLoginPassword** now use parameter values.</span></span>

   ```json
   {
       "comments": "Generalized from resource: '/subscriptions/{subscription-id}/resourceGroups/exportsite/providers/Microsoft.Sql/servers/tfserverexport'.",
       "type": "Microsoft.Sql/servers",
       "kind": "v12.0",
       "name": "[parameters('servers_tfserverexport_name')]",
       "apiVersion": "2014-04-01-preview",
       "location": "South Central US",
       "scale": null,
       "properties": {
           "administratorLogin": "[parameters('administratorLogin')]",
           "administratorLoginPassword": "[parameters('administratorLoginPassword')]",
           "version": "12.0"
       },
       "dependsOn": []
   },
   ```

6. <span data-ttu-id="b98d1-209">Selecione **Okey** quando tiver terminado a edição de modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="b98d1-209">Select **OK** when you are done editing hello template.</span></span>
7. <span data-ttu-id="b98d1-210">Selecione **salvar** modelo de toohello toosave Olá alterações.</span><span class="sxs-lookup"><span data-stu-id="b98d1-210">Select **Save** toosave hello changes toohello template.</span></span>
   
     ![salvar modelo](./media/resource-manager-export-template/save-template.png)
8. <span data-ttu-id="b98d1-212">modelo de saudação atualizado tooredeploy, selecione **implantar**.</span><span class="sxs-lookup"><span data-stu-id="b98d1-212">tooredeploy hello updated template, select **Deploy**.</span></span>
   
     ![implantar modelo](./media/resource-manager-export-template/redeploy-template.png)
9. <span data-ttu-id="b98d1-214">Fornecer valores de parâmetro e selecione um recurso de saudação do recurso grupo toodeploy para.</span><span class="sxs-lookup"><span data-stu-id="b98d1-214">Provide parameter values, and select a resource group toodeploy hello resources to.</span></span>


## <a name="fix-export-issues"></a><span data-ttu-id="b98d1-215">Corrigir os problemas da exportação</span><span class="sxs-lookup"><span data-stu-id="b98d1-215">Fix export issues</span></span>
<span data-ttu-id="b98d1-216">Nem todos os tipos de recurso suportam Olá exportar modelo de função.</span><span class="sxs-lookup"><span data-stu-id="b98d1-216">Not all resource types support hello export template function.</span></span> <span data-ttu-id="b98d1-217">tooresolve manualmente esse problema, adicione recursos ausentes Olá volta para o modelo.</span><span class="sxs-lookup"><span data-stu-id="b98d1-217">tooresolve this issue, manually add hello missing resources back into your template.</span></span> <span data-ttu-id="b98d1-218">mensagem de erro de saudação inclui tipos de recurso de saudação não podem ser exportados.</span><span class="sxs-lookup"><span data-stu-id="b98d1-218">hello error message includes hello resource types that cannot be exported.</span></span> <span data-ttu-id="b98d1-219">Encontre o tipo de recurso em [referência de modelo](/azure/templates/).</span><span class="sxs-lookup"><span data-stu-id="b98d1-219">Find that resource type in [Template reference](/azure/templates/).</span></span> <span data-ttu-id="b98d1-220">Por exemplo, toomanually adicionar um gateway de rede virtual, consulte [referência de modelo Microsoft.Network/virtualNetworkGateways](/azure/templates/microsoft.network/virtualnetworkgateways).</span><span class="sxs-lookup"><span data-stu-id="b98d1-220">For example, toomanually add a virtual network gateway, see [Microsoft.Network/virtualNetworkGateways template reference](/azure/templates/microsoft.network/virtualnetworkgateways).</span></span>

> [!NOTE]
> <span data-ttu-id="b98d1-221">Você só encontra problemas de exportação quando exporta de um grupo de recursos em vez de seu histórico de implantações.</span><span class="sxs-lookup"><span data-stu-id="b98d1-221">You only encounter export issues when exporting from a resource group rather than from your deployment history.</span></span> <span data-ttu-id="b98d1-222">Se sua última implantação representa com precisão o estado atual de Olá Olá do grupo de recursos, você deve exportar modelo de saudação do histórico de implantação de saudação em vez de saudação do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b98d1-222">If your last deployment accurately represents hello current state of hello resource group, you should export hello template from hello deployment history rather than from hello resource group.</span></span> <span data-ttu-id="b98d1-223">Exporte somente de um grupo de recursos quando você tiver feito alterações toohello grupo de recursos não estão definidas em um único modelo.</span><span class="sxs-lookup"><span data-stu-id="b98d1-223">Only export from a resource group when you have made changes toohello resource group that are not defined in a single template.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="b98d1-224">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b98d1-224">Next steps</span></span>
<span data-ttu-id="b98d1-225">Você aprendeu como tooexport um modelo de recursos que você criou no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="b98d1-225">You have learned how tooexport a template from resources that you created in hello portal.</span></span>

* <span data-ttu-id="b98d1-226">Você pode implantar um modelo por meio do [PowerShell](resource-group-template-deploy.md), da [CLI do Azure](resource-group-template-deploy-cli.md) ou da [API REST](resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="b98d1-226">You can deploy a template through [PowerShell](resource-group-template-deploy.md), [Azure CLI](resource-group-template-deploy-cli.md), or [REST API](resource-group-template-deploy-rest.md).</span></span>
* <span data-ttu-id="b98d1-227">toosee como tooexport um modelo por meio do PowerShell, consulte [usando o PowerShell do Azure com o Azure Resource Manager](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="b98d1-227">toosee how tooexport a template through PowerShell, see [Using Azure PowerShell with Azure Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="b98d1-228">toosee como tooexport um modelo por meio da CLI do Azure, consulte [Olá Use CLI do Azure para Mac, Linux e Windows com o Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="b98d1-228">toosee how tooexport a template through Azure CLI, see [Use hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>

