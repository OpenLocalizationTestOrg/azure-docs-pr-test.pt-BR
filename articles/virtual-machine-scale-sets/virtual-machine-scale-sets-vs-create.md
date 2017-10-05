---
title: "Implantar um conjunto de dimensionamento de máquinas virtuais usando o Visual Studio | Microsoft Docs"
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
ms.openlocfilehash: 78a4b0c8d305f57f495402cecb92d18425ff6bff
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-create-a-virtual-machine-scale-set-with-visual-studio"></a><span data-ttu-id="1025f-103">Como criar um Conjunto de Dimensionamento de Máquinas Virtuais com o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1025f-103">How to create a Virtual Machine Scale Set with Visual Studio</span></span>
<span data-ttu-id="1025f-104">Este artigo mostra como implantar um Conjunto de Escala de Máquina Virtual do Azure usando uma Implantação de Grupo de Recursos do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1025f-104">This article shows you how to deploy an Azure Virtual Machine Scale Set using a Visual Studio Resource Group Deployment.</span></span>

<span data-ttu-id="1025f-105">Os [Conjuntos de Dimensionamento de Máquinas Virtuais do Azure](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) são um recurso de Computação do Azure para implantar e gerenciar uma coleção de máquinas virtuais semelhantes com escala automática e balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="1025f-105">[Azure Virtual Machine Scale Sets](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) is an Azure Compute resource to deploy and manage a collection of similar virtual machines with auto-scale and load balancing.</span></span> <span data-ttu-id="1025f-106">É possível provisionar e implantar os Conjuntos de Dimensionamento de Máquinas Virtuais usando os [Modelos do Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="1025f-106">You can provision and deploy Virtual Machine Scale Sets using [Azure Resource Manager Templates](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="1025f-107">Os Modelos do Azure Resource Manager podem ser implantados usando a CLI do Azure, o PowerShell, a REST e também diretamente por meio do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1025f-107">Azure Resource Manager Templates can be deployed using Azure CLI, PowerShell, REST and also directly from Visual Studio.</span></span> <span data-ttu-id="1025f-108">O Visual Studio fornece um conjunto de modelos de exemplo, que podem ser implantados como parte de um projeto de Implantação de Grupo de Recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="1025f-108">Visual Studio provides a set of example templates, which can be deployed as part of an Azure Resource Group Deployment project.</span></span>

<span data-ttu-id="1025f-109">As implantações de Grupo de Recursos do Azure são uma maneira de agrupar e publicar um conjunto de recursos relacionados do Azure em uma única operação de implantação.</span><span class="sxs-lookup"><span data-stu-id="1025f-109">Azure Resource Group deployments are a way to group and publish a set of related Azure resources in a single deployment operation.</span></span> <span data-ttu-id="1025f-110">Saiba mais sobre eles aqui: [Criando e implantando grupos de recursos do Azure por meio do Visual Studio](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="1025f-110">You can learn more about them here: [Creating and deploying Azure resource groups through Visual Studio](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="1025f-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1025f-111">Pre-requisites</span></span>
<span data-ttu-id="1025f-112">Para começar a implantar Conjuntos de Dimensionamento de Máquinas Virtuais no Visual Studio, você precisa do seguinte:</span><span class="sxs-lookup"><span data-stu-id="1025f-112">To get started deploying Virtual Machine Scale Sets in Visual Studio, you need the following:</span></span>

* <span data-ttu-id="1025f-113">Visual Studio 2013 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="1025f-113">Visual Studio 2013 or later</span></span>
* <span data-ttu-id="1025f-114">SDK do Azure 2.7, 2.8 ou 2.9</span><span class="sxs-lookup"><span data-stu-id="1025f-114">Azure SDK 2.7, 2.8 or 2.9</span></span>

>[!NOTE]
><span data-ttu-id="1025f-115">Essas instruções pressupõem que você esteja usando o Visual Studio com o [SDK do Azure 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).</span><span class="sxs-lookup"><span data-stu-id="1025f-115">These instructions assume you are using Visual Studio with [Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).</span></span>

## <a name="creating-a-project"></a><span data-ttu-id="1025f-116">Criando um projeto</span><span class="sxs-lookup"><span data-stu-id="1025f-116">Creating a Project</span></span>
1. <span data-ttu-id="1025f-117">Crie um novo projeto no Visual Studio escolhendo **Arquivo | Novo | Projeto**.</span><span class="sxs-lookup"><span data-stu-id="1025f-117">Create a new project in Visual Studio by choosing **File | New | Project**.</span></span>
   
    ![Arquivo novo][file_new]

2. <span data-ttu-id="1025f-119">Em **Visual C# | Nuvem**, escolha **Azure Resource Manager** para criar um projeto para implantar um Modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1025f-119">Under **Visual C# | Cloud**, choose **Azure Resource Manager** to create a project for deploying an Azure Resource Manager Template.</span></span>
   
    ![Criar projeto][create_project]

3. <span data-ttu-id="1025f-121">Na lista de Modelos, selecione o Modelo de Conjunto de Escala de Máquina Virtual do Windows ou do Linux.</span><span class="sxs-lookup"><span data-stu-id="1025f-121">From the list of Templates, select either the Linux or Windows Virtual Machine Scale Set Template.</span></span>
   
   ![Selecionar modelo][select_Template]

4. <span data-ttu-id="1025f-123">Depois de criar o projeto, você verá scripts de implantação do PowerShell, um Modelo do Azure Resource Manager e um arquivo de parâmetros para o Conjunto de Dimensionamento de Máquinas Virtuais.</span><span class="sxs-lookup"><span data-stu-id="1025f-123">Once your project is created you see PowerShell deployment scripts, an Azure Resource Manager Template, and a parameter file for the Virtual Machine Scale Set.</span></span>
   
    ![Gerenciador de Soluções][solution_explorer]

## <a name="customize-your-project"></a><span data-ttu-id="1025f-125">Personalizar seu projeto</span><span class="sxs-lookup"><span data-stu-id="1025f-125">Customize your project</span></span>
<span data-ttu-id="1025f-126">Agora você pode editar o Modelo para personalizá-lo de acordo com as necessidades de seu aplicativo, como adicionar propriedades de extensão de VM ou editar regras de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="1025f-126">Now you can edit the Template to customize it for your application's needs, such as adding VM extension properties or editing load balancing rules.</span></span> <span data-ttu-id="1025f-127">Por padrão, os Modelos do Conjunto de Dimensionamento de Máquinas Virtuais são configurados para implantar a extensão AzureDiagnostics, que facilita a adição de regras de escala automática.</span><span class="sxs-lookup"><span data-stu-id="1025f-127">By default the Virtual Machine Scale Set Templates are configured to deploy the AzureDiagnostics extension, which makes it easy to add autoscale rules.</span></span> <span data-ttu-id="1025f-128">Ela também implanta um balanceador de carga com um endereço IP público, configurado com regras NAT de entrada.</span><span class="sxs-lookup"><span data-stu-id="1025f-128">It also deploys a load balancer with a public IP address, configured with inbound NAT rules.</span></span> 

<span data-ttu-id="1025f-129">O balanceador de carga permite que você se conecte às instâncias da VM com o SSH (Linux) ou o RDP (Windows).</span><span class="sxs-lookup"><span data-stu-id="1025f-129">The load balancer lets you connect to the VM instances with SSH (Linux) or RDP (Windows).</span></span> <span data-ttu-id="1025f-130">O intervalo de portas de front-end começa em 50000.</span><span class="sxs-lookup"><span data-stu-id="1025f-130">The front-end port range starts at 50000.</span></span> <span data-ttu-id="1025f-131">Para o Linux, isso significa que, se você usar o SSH para a porta 50000, será roteado para a porta 22 da primeira VM no Conjunto de Dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="1025f-131">For linux this means that if you SSH to port 50000, you are routed to port 22 of the first VM in the Scale Set.</span></span> <span data-ttu-id="1025f-132">A conexão à porta 50001 é roteada para a porta 22 da segunda VM e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="1025f-132">Connecting to port 50001 is routed to port 22 of the second VM and so on.</span></span>

 <span data-ttu-id="1025f-133">Uma boa maneira de editar os Modelos com o Visual Studio é usar a Estrutura de Tópicos JSON para organizar os parâmetros, as variáveis e os recursos.</span><span class="sxs-lookup"><span data-stu-id="1025f-133">A good way to edit your Templates with Visual Studio is to use the JSON Outline to organize the parameters, variables, and resources.</span></span> <span data-ttu-id="1025f-134">Com uma compreensão do esquema do Visual Studio, é possível detectar erros em seu Modelo antes de implantá-lo.</span><span class="sxs-lookup"><span data-stu-id="1025f-134">With an understanding of the schema Visual Studio can point out errors in your Template before you deploy it.</span></span>

![Gerenciador JSON][json_explorer]

## <a name="deploy-the-project"></a><span data-ttu-id="1025f-136">Implantar o projeto</span><span class="sxs-lookup"><span data-stu-id="1025f-136">Deploy the project</span></span>
1. <span data-ttu-id="1025f-137">Implante o Modelo do Azure Resource Manager para criar o recurso Conjunto de Dimensionamento de Máquinas Virtuais.</span><span class="sxs-lookup"><span data-stu-id="1025f-137">Deploy the Azure Resource Manager Template to create the Virtual Machine Scale Set resource.</span></span> <span data-ttu-id="1025f-138">Clique com o botão direito do mouse no nó do projeto e escolha **Implantar | Nova Implantação**.</span><span class="sxs-lookup"><span data-stu-id="1025f-138">Right-click on the project node and choose **Deploy | New Deployment**.</span></span>
   
    ![Implantar o modelo][5deploy_Template]
    
2. <span data-ttu-id="1025f-140">Selecione sua assinatura no diálogo “Implantar no Grupo de Recursos”.</span><span class="sxs-lookup"><span data-stu-id="1025f-140">Select your subscription in the “Deploy to Resource Group” dialog.</span></span>
   
    ![Implantar o modelo][6deploy_Template]

3. <span data-ttu-id="1025f-142">Aqui, é possível criar um Grupo de Recursos do Azure no qual o Modelo será implantado.</span><span class="sxs-lookup"><span data-stu-id="1025f-142">From here, you can create an Azure Resource Group to deploy your Template to.</span></span>
   
    ![Novo grupo de recursos][new_resource]

4. <span data-ttu-id="1025f-144">Em seguida, clique em **Editar Parâmetros** para inserir parâmetros que são passados para o Modelo.</span><span class="sxs-lookup"><span data-stu-id="1025f-144">Next, click **Edit Parameters** to enter parameters that are passed to your Template.</span></span> <span data-ttu-id="1025f-145">Forneça o nome de usuário e a senha do sistema operacional, que é necessária para criar a implantação.</span><span class="sxs-lookup"><span data-stu-id="1025f-145">Provide the username and password for the OS, which is required to create the deployment.</span></span> <span data-ttu-id="1025f-146">Se não tiver as Ferramentas PowerShell para Visual Studio instaladas, será recomendável marcar **Salvar senhas** para evitar um prompt oculto de linha de comando do PowerShell ou usar o [suporte do keyvault](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/).</span><span class="sxs-lookup"><span data-stu-id="1025f-146">If you don't have PowerShell Tools for Visual Studio installed, it is recommended to check **Save passwords** to avoid a hidden PowerShell command-line prompt, or use [keyvault support](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/).</span></span>
   
    ![Editar Parâmetros][edit_parameters]

5. <span data-ttu-id="1025f-148">Agora clique em **Implantar**.</span><span class="sxs-lookup"><span data-stu-id="1025f-148">Now click **Deploy**.</span></span> <span data-ttu-id="1025f-149">A janela **Saída** mostra o progresso da implantação.</span><span class="sxs-lookup"><span data-stu-id="1025f-149">The **Output** window shows the deployment progress.</span></span> <span data-ttu-id="1025f-150">Observe que a ação executa o script **Deploy-AzureResourceGroup.ps1**.</span><span class="sxs-lookup"><span data-stu-id="1025f-150">Note that the action is executing the **Deploy-AzureResourceGroup.ps1** script.</span></span>
   
   ![Janela de saída][output_window]

## <a name="exploring-your-virtual-machine-scale-set"></a><span data-ttu-id="1025f-152">Explorando o Conjunto de Dimensionamento de Máquinas Virtuais</span><span class="sxs-lookup"><span data-stu-id="1025f-152">Exploring your Virtual Machine Scale Set</span></span>
<span data-ttu-id="1025f-153">Depois que a implantação for concluída, é possível exibir o novo Conjunto de Dimensionamento de Máquinas Virtuais no **Cloud Explorer** do Visual Studio (basta atualizar a lista).</span><span class="sxs-lookup"><span data-stu-id="1025f-153">Once the deployment completes, you can view the new Virtual Machine Scale Set in the Visual Studio **Cloud Explorer** (refresh the list).</span></span> <span data-ttu-id="1025f-154">O Gerenciador de Nuvem permite que você gerencie recursos do Azure no Visual Studio ao mesmo tempo que desenvolve aplicativos.</span><span class="sxs-lookup"><span data-stu-id="1025f-154">Cloud Explorer lets you manage Azure resources in Visual Studio while developing applications.</span></span> <span data-ttu-id="1025f-155">Você também pode exibir o Conjunto de Dimensionamento de Máquinas Virtuais no [portal do Azure](https://portal.azure.com) e no [Gerenciador de Recursos do Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1025f-155">You can also view your Virtual Machine Scale Set in the [Azure portal](https://portal.azure.com) and [Azure Resource Explorer](https://resources.azure.com/).</span></span>

![Gerenciador de Nuvem][cloud_explorer]

 <span data-ttu-id="1025f-157">O portal fornece a melhor maneira de gerenciar visualmente sua infraestrutura do Azure com um navegador da Web, enquanto o Gerenciador de Recursos do Azure oferece uma maneira fácil de explorar e depurar recursos do Azure, proporcionando uma janela para a “exibição de instância”, além de mostrar comandos do PowerShell para os recursos que você está examinando.</span><span class="sxs-lookup"><span data-stu-id="1025f-157">The portal provides the best way to visually manage your Azure infrastructure with a web browser, while Azure Resource Explorer provides an easy way to explore and debug Azure resources, giving a window into the "instance view" and also showing PowerShell commands for the resources you are looking at.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1025f-158">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1025f-158">Next steps</span></span>
<span data-ttu-id="1025f-159">Depois de implantar os Conjuntos de Dimensionamento de Máquinas Virtuais com êxito por meio do Visual Studio, é possível personalizar o projeto ainda mais para atender às necessidades do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1025f-159">Once you’ve successfully deployed Virtual Machine Scale Sets through Visual Studio, you can further customize your project to suit your application requirements.</span></span> <span data-ttu-id="1025f-160">Por exemplo, configurar a escala automática adicionando um recurso do **Insights**, adicionar a infraestrutura ao Modelo (como VMs independentes) ou implantar aplicativos usando a extensão de script personalizado.</span><span class="sxs-lookup"><span data-stu-id="1025f-160">For example, configure auto-scale by adding an **Insights** resource, adding infrastructure to your Template (like standalone VMs), or deploying applications using the custom script extension.</span></span> <span data-ttu-id="1025f-161">Encontre bons modelos de exemplo no repositório GitHub de [Modelos de Início Rápido do Azure](https://github.com/Azure/azure-quickstart-templates) (pesquise “vmss”).</span><span class="sxs-lookup"><span data-stu-id="1025f-161">Good example templates can be found in the [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates) GitHub repository (search for "vmss").</span></span>

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
