---
title: "aaaDeploy conjunto de escala de máquinas virtuais usando o Visual Studio | Microsoft Docs"
description: "Implantar um conjunto de escala de máquina virtual usando o Visual Studio e um modelo do Resource Manager"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ed0786b8-34b2-49a8-85b5-2a628128ead6
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: guybo
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c89a9f2478ccc3d22989aea604a4273bcc46df82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-virtual-machine-scale-set-with-visual-studio"></a><span data-ttu-id="bb0f6-103">Como toocreate uma escala de máquina Virtual definido com o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bb0f6-103">How toocreate a Virtual Machine Scale Set with Visual Studio</span></span>
<span data-ttu-id="bb0f6-104">Este artigo mostra como toodeploy uma escala de máquina Virtual do Azure definido usando uma implantação de grupo do Visual Studio recursos.</span><span class="sxs-lookup"><span data-stu-id="bb0f6-104">This article shows you how toodeploy an Azure Virtual Machine Scale Set using a Visual Studio Resource Group Deployment.</span></span>

<span data-ttu-id="bb0f6-105">[Conjuntos de escala de máquinas virtuais do Azure](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) é um toodeploy de recursos de computação do Azure e gerenciar uma coleção de máquinas virtuais semelhantes com o dimensionamento automático e o balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="bb0f6-105">[Azure Virtual Machine Scale Sets](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) is an Azure Compute resource toodeploy and manage a collection of similar virtual machines with auto-scale and load balancing.</span></span> <span data-ttu-id="bb0f6-106">É possível provisionar e implantar os Conjuntos de Dimensionamento de Máquinas Virtuais usando os [Modelos do Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="bb0f6-106">You can provision and deploy Virtual Machine Scale Sets using [Azure Resource Manager Templates](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="bb0f6-107">Os Modelos do Azure Resource Manager podem ser implantados usando a CLI do Azure, o PowerShell, a REST e também diretamente por meio do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bb0f6-107">Azure Resource Manager Templates can be deployed using Azure CLI, PowerShell, REST and also directly from Visual Studio.</span></span> <span data-ttu-id="bb0f6-108">O Visual Studio fornece um conjunto de modelos de exemplo, que podem ser implantados como parte de um projeto de Implantação de Grupo de Recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="bb0f6-108">Visual Studio provides a set of example templates, which can be deployed as part of an Azure Resource Group Deployment project.</span></span>

<span data-ttu-id="bb0f6-109">Implantações de grupo de recursos do Azure são uma maneira toogroup e publicam um conjunto de recursos do Azure relacionados em uma única operação de implantação.</span><span class="sxs-lookup"><span data-stu-id="bb0f6-109">Azure Resource Group deployments are a way toogroup and publish a set of related Azure resources in a single deployment operation.</span></span> <span data-ttu-id="bb0f6-110">Saiba mais sobre eles aqui: [Criando e implantando grupos de recursos do Azure por meio do Visual Studio](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="bb0f6-110">You can learn more about them here: [Creating and deploying Azure resource groups through Visual Studio](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="bb0f6-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="bb0f6-111">Pre-requisites</span></span>
<span data-ttu-id="bb0f6-112">tooget iniciar a implantação de conjuntos de escala de máquina Virtual no Visual Studio, você precisa seguir hello:</span><span class="sxs-lookup"><span data-stu-id="bb0f6-112">tooget started deploying Virtual Machine Scale Sets in Visual Studio, you need hello following:</span></span>

* <span data-ttu-id="bb0f6-113">Visual Studio 2013 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="bb0f6-113">Visual Studio 2013 or later</span></span>
* <span data-ttu-id="bb0f6-114">SDK do Azure 2.7, 2.8 ou 2.9</span><span class="sxs-lookup"><span data-stu-id="bb0f6-114">Azure SDK 2.7, 2.8 or 2.9</span></span>

>[!NOTE]
><span data-ttu-id="bb0f6-115">Essas instruções pressupõem que você esteja usando o Visual Studio com o [SDK do Azure 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).</span><span class="sxs-lookup"><span data-stu-id="bb0f6-115">These instructions assume you are using Visual Studio with [Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).</span></span>

## <a name="creating-a-project"></a><span data-ttu-id="bb0f6-116">Criando um projeto</span><span class="sxs-lookup"><span data-stu-id="bb0f6-116">Creating a Project</span></span>
1. <span data-ttu-id="bb0f6-117">Crie um novo projeto no Visual Studio escolhendo **Arquivo | Novo | Projeto**.</span><span class="sxs-lookup"><span data-stu-id="bb0f6-117">Create a new project in Visual Studio by choosing **File | New | Project**.</span></span>
   
    ![Arquivo novo][file_new]

2. <span data-ttu-id="bb0f6-119">Em **Visual c# | Nuvem**, escolha **do Azure Resource Manager** toocreate um projeto para implantar um modelo do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="bb0f6-119">Under **Visual C# | Cloud**, choose **Azure Resource Manager** toocreate a project for deploying an Azure Resource Manager Template.</span></span>
   
    ![Criar projeto][create_project]

3. <span data-ttu-id="bb0f6-121">Saudação de modelos, selecione lista Olá Linux ou definir modelo de escala de máquina Virtual Windows.</span><span class="sxs-lookup"><span data-stu-id="bb0f6-121">From hello list of Templates, select either hello Linux or Windows Virtual Machine Scale Set Template.</span></span>
   
   ![Selecionar modelo][select_Template]

4. <span data-ttu-id="bb0f6-123">Depois de criar seu projeto Consulte scripts de implantação do PowerShell, um modelo do Gerenciador de recursos do Azure e um arquivo de parâmetro hello conjunto de escala de máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="bb0f6-123">Once your project is created you see PowerShell deployment scripts, an Azure Resource Manager Template, and a parameter file for hello Virtual Machine Scale Set.</span></span>
   
    ![Gerenciador de Soluções][solution_explorer]

## <a name="customize-your-project"></a><span data-ttu-id="bb0f6-125">Personalizar seu projeto</span><span class="sxs-lookup"><span data-stu-id="bb0f6-125">Customize your project</span></span>
<span data-ttu-id="bb0f6-126">Agora você pode editar Olá modelo toocustomize-lo para as necessidades do seu aplicativo, como adicionar propriedades de extensão VM ou edição carregar regras de balanceamento.</span><span class="sxs-lookup"><span data-stu-id="bb0f6-126">Now you can edit hello Template toocustomize it for your application's needs, such as adding VM extension properties or editing load balancing rules.</span></span> <span data-ttu-id="bb0f6-127">Por padrão ao definir modelos de escala de máquina Virtual Olá são toodeploy configurado Olá AzureDiagnostics extensão que torna fácil tooadd regras de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="bb0f6-127">By default hello Virtual Machine Scale Set Templates are configured toodeploy hello AzureDiagnostics extension, which makes it easy tooadd autoscale rules.</span></span> <span data-ttu-id="bb0f6-128">Ela também implanta um balanceador de carga com um endereço IP público, configurado com regras NAT de entrada.</span><span class="sxs-lookup"><span data-stu-id="bb0f6-128">It also deploys a load balancer with a public IP address, configured with inbound NAT rules.</span></span> 

<span data-ttu-id="bb0f6-129">o balanceador de carga Olá permite que você se conectar a instâncias de VM toohello com SSH (Linux) ou RDP (Windows).</span><span class="sxs-lookup"><span data-stu-id="bb0f6-129">hello load balancer lets you connect toohello VM instances with SSH (Linux) or RDP (Windows).</span></span> <span data-ttu-id="bb0f6-130">intervalo de portas de front-end de saudação inicia em 50000.</span><span class="sxs-lookup"><span data-stu-id="bb0f6-130">hello front-end port range starts at 50000.</span></span> <span data-ttu-id="bb0f6-131">Para linux, isso significa que, se você SSH tooport 50000, é roteada tooport 22 de Olá primeira VM no hello conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="bb0f6-131">For linux this means that if you SSH tooport 50000, you are routed tooport 22 of hello first VM in hello Scale Set.</span></span> <span data-ttu-id="bb0f6-132">Conectar-se tooport 50001 é roteado tooport 22 de saudação segundo VM e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="bb0f6-132">Connecting tooport 50001 is routed tooport 22 of hello second VM and so on.</span></span>

 <span data-ttu-id="bb0f6-133">Uma boa maneira tooedit seus modelos com o Visual Studio é parâmetros de saudação toouse Olá JSON tópicos tooorganize, variáveis e recursos.</span><span class="sxs-lookup"><span data-stu-id="bb0f6-133">A good way tooedit your Templates with Visual Studio is toouse hello JSON Outline tooorganize hello parameters, variables, and resources.</span></span> <span data-ttu-id="bb0f6-134">Uma compreensão de saudação esquema Visual Studio pode apontar erros em seu modelo antes de implantá-lo.</span><span class="sxs-lookup"><span data-stu-id="bb0f6-134">With an understanding of hello schema Visual Studio can point out errors in your Template before you deploy it.</span></span>

![Gerenciador JSON][json_explorer]

## <a name="deploy-hello-project"></a><span data-ttu-id="bb0f6-136">Implantar projeto Olá</span><span class="sxs-lookup"><span data-stu-id="bb0f6-136">Deploy hello project</span></span>
1. <span data-ttu-id="bb0f6-137">Implante o recurso de conjunto de escala de máquina Virtual Olá toocreate modelo do Gerenciador de recursos do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="bb0f6-137">Deploy hello Azure Resource Manager Template toocreate hello Virtual Machine Scale Set resource.</span></span> <span data-ttu-id="bb0f6-138">Clique com botão direito no nó do projeto hello e escolha **implantar | Nova implantação**.</span><span class="sxs-lookup"><span data-stu-id="bb0f6-138">Right-click on hello project node and choose **Deploy | New Deployment**.</span></span>
   
    ![Implantar o modelo][5deploy_Template]
    
2. <span data-ttu-id="bb0f6-140">Selecione sua assinatura na caixa de diálogo hello "Implantar tooResource grupo".</span><span class="sxs-lookup"><span data-stu-id="bb0f6-140">Select your subscription in hello “Deploy tooResource Group” dialog.</span></span>
   
    ![Implantar o modelo][6deploy_Template]

3. <span data-ttu-id="bb0f6-142">A partir daqui, você pode criar seu modelo para toodeploy um grupo de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="bb0f6-142">From here, you can create an Azure Resource Group toodeploy your Template to.</span></span>
   
    ![Novo grupo de recursos][new_resource]

4. <span data-ttu-id="bb0f6-144">Em seguida, clique em **Editar parâmetros** tooenter parâmetros que são passados tooyour modelo.</span><span class="sxs-lookup"><span data-stu-id="bb0f6-144">Next, click **Edit Parameters** tooenter parameters that are passed tooyour Template.</span></span> <span data-ttu-id="bb0f6-145">Forneça Olá username e password para Olá sistema operacional, é necessário toocreate Olá implantação.</span><span class="sxs-lookup"><span data-stu-id="bb0f6-145">Provide hello username and password for hello OS, which is required toocreate hello deployment.</span></span> <span data-ttu-id="bb0f6-146">Se você não tiver as ferramentas do PowerShell para Visual Studio instaladas, é recomendável toocheck **salvar senhas** tooavoid um oculto de linha de comando do PowerShell prompt ou use [keyvault suporte](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/).</span><span class="sxs-lookup"><span data-stu-id="bb0f6-146">If you don't have PowerShell Tools for Visual Studio installed, it is recommended toocheck **Save passwords** tooavoid a hidden PowerShell command-line prompt, or use [keyvault support](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/).</span></span>
   
    ![Editar Parâmetros][edit_parameters]

5. <span data-ttu-id="bb0f6-148">Agora clique em **Implantar**.</span><span class="sxs-lookup"><span data-stu-id="bb0f6-148">Now click **Deploy**.</span></span> <span data-ttu-id="bb0f6-149">Olá **saída** janela mostra o progresso da implantação hello.</span><span class="sxs-lookup"><span data-stu-id="bb0f6-149">hello **Output** window shows hello deployment progress.</span></span> <span data-ttu-id="bb0f6-150">Observe que a ação de saudação está executando Olá **implantar AzureResourceGroup.ps1** script.</span><span class="sxs-lookup"><span data-stu-id="bb0f6-150">Note that hello action is executing hello **Deploy-AzureResourceGroup.ps1** script.</span></span>
   
   ![Janela de saída][output_window]

## <a name="exploring-your-virtual-machine-scale-set"></a><span data-ttu-id="bb0f6-152">Explorando o Conjunto de Dimensionamento de Máquinas Virtuais</span><span class="sxs-lookup"><span data-stu-id="bb0f6-152">Exploring your Virtual Machine Scale Set</span></span>
<span data-ttu-id="bb0f6-153">Após a conclusão da implantação Olá, é possível exibir hello nova máquina Virtual conjunto de escala no Visual Studio de saudação **Cloud Explorer** (atualização Olá lista).</span><span class="sxs-lookup"><span data-stu-id="bb0f6-153">Once hello deployment completes, you can view hello new Virtual Machine Scale Set in hello Visual Studio **Cloud Explorer** (refresh hello list).</span></span> <span data-ttu-id="bb0f6-154">O Gerenciador de Nuvem permite que você gerencie recursos do Azure no Visual Studio ao mesmo tempo que desenvolve aplicativos.</span><span class="sxs-lookup"><span data-stu-id="bb0f6-154">Cloud Explorer lets you manage Azure resources in Visual Studio while developing applications.</span></span> <span data-ttu-id="bb0f6-155">Você também pode exibir o conjunto de escala de máquinas virtuais em Olá [portal do Azure](https://portal.azure.com) e [Gerenciador de recursos do Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="bb0f6-155">You can also view your Virtual Machine Scale Set in hello [Azure portal](https://portal.azure.com) and [Azure Resource Explorer](https://resources.azure.com/).</span></span>

![Gerenciador de Nuvem][cloud_explorer]

 <span data-ttu-id="bb0f6-157">Olá portal fornece a melhor maneira de saudação toovisually gerenciar sua infraestrutura do Azure com um navegador da web, enquanto o Gerenciador de recursos do Azure fornece uma maneira fácil de tooexplore e depurar recursos do Azure, fornecendo uma janela em hello "instância exibir" e também mostrando PowerShell comandos para recursos de saudação que você está observando.</span><span class="sxs-lookup"><span data-stu-id="bb0f6-157">hello portal provides hello best way toovisually manage your Azure infrastructure with a web browser, while Azure Resource Explorer provides an easy way tooexplore and debug Azure resources, giving a window into hello "instance view" and also showing PowerShell commands for hello resources you are looking at.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bb0f6-158">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bb0f6-158">Next steps</span></span>
<span data-ttu-id="bb0f6-159">Depois que você implantou com êxito os conjuntos de escala de máquina Virtual por meio do Visual Studio, você pode personalizar seu projeto toosuit seus requisitos de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bb0f6-159">Once you’ve successfully deployed Virtual Machine Scale Sets through Visual Studio, you can further customize your project toosuit your application requirements.</span></span> <span data-ttu-id="bb0f6-160">Por exemplo, configurar o dimensionamento automático, adicionando um **Insights** recursos, adicionando infraestrutura tooyour modelo (como as máquinas virtuais autônomas) ou implantação de aplicativos usando a extensão do script personalizado hello.</span><span class="sxs-lookup"><span data-stu-id="bb0f6-160">For example, configure auto-scale by adding an **Insights** resource, adding infrastructure tooyour Template (like standalone VMs), or deploying applications using hello custom script extension.</span></span> <span data-ttu-id="bb0f6-161">Modelos de bom exemplo podem ser encontrados na Olá [modelos de início rápido do Azure](https://github.com/Azure/azure-quickstart-templates) repositório GitHub (procure "vmss").</span><span class="sxs-lookup"><span data-stu-id="bb0f6-161">Good example templates can be found in hello [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates) GitHub repository (search for "vmss").</span></span>

[file_new]: ./media/virtual-machine-scale-sets-vs-create/1-FileNew.png
[create_project]: ./media/virtual-machine-scale-sets-vs-create/2-CreateProject.png
[select_Template]: ./media/virtual-machine-scale-sets-vs-create/3b-SelectTemplateLin.png
[solution_explorer]: ./media/virtual-machine-scale-sets-vs-create/4-SolutionExplorer.png
[json_explorer]: ./media/virtual-machine-scale-sets-vs-create/10-JsonExplorer.png
[5deploy_Template]: ./media/virtual-machine-scale-sets-vs-create/5-DeployTemplate.png
[6deploy_Template]: ./media/virtual-machine-scale-sets-vs-create/6-DeployTemplate.png
[new_resource]: ./media/virtual-machine-scale-sets-vs-create/7-NewResourceGroup.png
[edit_parameters]: ./media/virtual-machine-scale-sets-vs-create/8-EditParameter.png
[output_window]: ./media/virtual-machine-scale-sets-vs-create/9-Output.png
[cloud_explorer]: ./media/virtual-machine-scale-sets-vs-create/12-CloudExplorer.png
