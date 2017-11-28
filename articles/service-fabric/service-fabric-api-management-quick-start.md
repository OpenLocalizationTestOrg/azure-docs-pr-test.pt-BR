---
title: "aaaAzure Service Fabric com início rápido do gerenciamento de API | Microsoft Docs"
description: "Este guia mostra como tooquickly Introdução ao gerenciamento de API do Azure e do Service Fabric."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: vturecek
ms.openlocfilehash: f76f3f39a92f89892d6a02ecaab1ec3d343fe2a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-with-azure-api-management-quick-start"></a><span data-ttu-id="fbda6-103">Service Fabric com início rápido de Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="fbda6-103">Service Fabric with Azure API Management Quick Start</span></span>

<span data-ttu-id="fbda6-104">Este guia mostra como tooset até gerenciamento de API do Azure com o Service Fabric e configurar sua primeira API operação toosend tráfego tooback ponta os serviços no Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="fbda6-104">This guide shows you how tooset up Azure API Management with Service Fabric and configure your first API operation toosend traffic tooback-end services in Service Fabric.</span></span> <span data-ttu-id="fbda6-105">toolearn mais informações sobre cenários de gerenciamento de API do Azure com o Service Fabric, consulte Olá [visão geral](service-fabric-api-management-overview.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="fbda6-105">toolearn more about Azure API Management scenarios with Service Fabric, see hello [overview](service-fabric-api-management-overview.md) article.</span></span> 

## <a name="deploy-api-management-and-service-fabric-tooazure"></a><span data-ttu-id="fbda6-106">Implantar o gerenciamento de API e do Service Fabric tooAzure</span><span class="sxs-lookup"><span data-stu-id="fbda6-106">Deploy API Management and Service Fabric tooAzure</span></span>

<span data-ttu-id="fbda6-107">Olá primeira etapa é toodeploy gerenciamento de API e um tooAzure de cluster do Service Fabric em uma rede Virtual compartilhada.</span><span class="sxs-lookup"><span data-stu-id="fbda6-107">hello first step is toodeploy API Management and a Service Fabric cluster tooAzure in a shared Virtual Network.</span></span> <span data-ttu-id="fbda6-108">Isso permite que toocommunicate de gerenciamento de API diretamente com o Service Fabric para executar descoberta de serviço, resolução de partição de serviço e encaminhar o tráfego diretamente tooany back-end do serviço na malha do serviço.</span><span class="sxs-lookup"><span data-stu-id="fbda6-108">This allows API Management toocommunicate directly with Service Fabric so it can perform service discovery, service partition resolution, and forward traffic directly tooany backend service in Service Fabric.</span></span>

### <a name="topology"></a><span data-ttu-id="fbda6-109">Topologia</span><span class="sxs-lookup"><span data-stu-id="fbda6-109">Topology</span></span>

<span data-ttu-id="fbda6-110">Este guia implanta seguinte Olá tooAzure de topologia em que o gerenciamento de API e do Service Fabric estejam em sub-redes de Olá mesma rede Virtual:</span><span class="sxs-lookup"><span data-stu-id="fbda6-110">This guide deploys hello following topology tooAzure in which API Management and Service Fabric are in subnets of hello same Virtual Network:</span></span>

 ![Legenda de imagem][sf-apim-topology-overview]

<span data-ttu-id="fbda6-112">modelos do Gerenciador de recursos tooget início rápido, são fornecidos para cada etapa de implantação:</span><span class="sxs-lookup"><span data-stu-id="fbda6-112">tooget started quickly, Resource Manager templates are provided for each deployment step:</span></span>

 - <span data-ttu-id="fbda6-113">Topologia de rede:</span><span class="sxs-lookup"><span data-stu-id="fbda6-113">Network topology:</span></span>
    - <span data-ttu-id="fbda6-114">[network.json][network-arm]</span><span class="sxs-lookup"><span data-stu-id="fbda6-114">[network.json][network-arm]</span></span>
    - <span data-ttu-id="fbda6-115">[network.parameters.json][network-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="fbda6-115">[network.parameters.json][network-parameters-arm]</span></span>
 - <span data-ttu-id="fbda6-116">Cluster do Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="fbda6-116">Service Fabric cluster:</span></span>
    - <span data-ttu-id="fbda6-117">[cluster.json][cluster-arm]</span><span class="sxs-lookup"><span data-stu-id="fbda6-117">[cluster.json][cluster-arm]</span></span>
    - <span data-ttu-id="fbda6-118">[cluster.parameters.json][cluster-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="fbda6-118">[cluster.parameters.json][cluster-parameters-arm]</span></span>
 - <span data-ttu-id="fbda6-119">Gerenciamento de API:</span><span class="sxs-lookup"><span data-stu-id="fbda6-119">API Management:</span></span>
    - <span data-ttu-id="fbda6-120">[apim.json][apim-arm]</span><span class="sxs-lookup"><span data-stu-id="fbda6-120">[apim.json][apim-arm]</span></span>
    - <span data-ttu-id="fbda6-121">[apim.parameters.json][apim-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="fbda6-121">[apim.parameters.json][apim-parameters-arm]</span></span>

### <a name="sign-in-tooazure-and-select-your-subscription"></a><span data-ttu-id="fbda6-122">Entre no tooAzure e selecione sua assinatura</span><span class="sxs-lookup"><span data-stu-id="fbda6-122">Sign in tooAzure and select your subscription</span></span>

<span data-ttu-id="fbda6-123">Este guia usa o [Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="fbda6-123">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="fbda6-124">Quando você inicia uma nova sessão do PowerShell, entre no tooyour conta do Azure e selecione sua assinatura antes de executar comandos do Azure.</span><span class="sxs-lookup"><span data-stu-id="fbda6-124">When you start a new PowerShell session, sign in tooyour Azure account and select your subscription before you execute Azure commands.</span></span>
 
<span data-ttu-id="fbda6-125">Entre tooyour conta do Azure:</span><span class="sxs-lookup"><span data-stu-id="fbda6-125">Sign in tooyour Azure account:</span></span>

```powershell
PS > Login-AzureRmAccount
```

<span data-ttu-id="fbda6-126">Selecione sua assinatura:</span><span class="sxs-lookup"><span data-stu-id="fbda6-126">Select your subscription:</span></span>

```powershell
PS > Get-AzureRmSubscription
PS > Set-AzureRmContext -SubscriptionId <guid>
```

### <a name="create-a-resource-group"></a><span data-ttu-id="fbda6-127">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="fbda6-127">Create a resource group</span></span>

<span data-ttu-id="fbda6-128">Crie um novo grupo de recursos para sua implantação.</span><span class="sxs-lookup"><span data-stu-id="fbda6-128">Create a new resource group for your deployment.</span></span> <span data-ttu-id="fbda6-129">Dê um nome e um local.</span><span class="sxs-lookup"><span data-stu-id="fbda6-129">Give it a name and a location.</span></span>

```powershell
PS > New-AzureRmResourceGroup -Name <my-resource-group> -Location westus
```

### <a name="deploy-hello-network-topology"></a><span data-ttu-id="fbda6-130">Implantar a topologia de rede Olá</span><span class="sxs-lookup"><span data-stu-id="fbda6-130">Deploy hello network topology</span></span>

<span data-ttu-id="fbda6-131">Olá primeira etapa é tooset backup toowhich de topologia de rede Olá API de gerenciamento e cluster do Service Fabric Olá será implantado.</span><span class="sxs-lookup"><span data-stu-id="fbda6-131">hello first step is tooset up hello network topology toowhich API Management and hello Service Fabric cluster will be deployed.</span></span> <span data-ttu-id="fbda6-132">Olá [network.json] [ network-arm] modelo do Gerenciador de recursos é toocreate configurado uma rede Virtual (VNET) com duas sub-redes e dois grupos de segurança de rede (NSG).</span><span class="sxs-lookup"><span data-stu-id="fbda6-132">hello [network.json][network-arm] Resource Manager template is configured toocreate a Virtual Network (VNET) with two subnets and two Network Security Groups (NSG).</span></span> 

<span data-ttu-id="fbda6-133">Olá [network.parameters.json] [ network-parameters-arm] arquivo de parâmetros contém nomes de saudação de sub-redes hello e NSGs gerenciamento de API e a malha do serviço serão implantado.</span><span class="sxs-lookup"><span data-stu-id="fbda6-133">hello [network.parameters.json][network-parameters-arm] parameters file contains hello names of hello subnets and NSGs that API Management and Service Fabric will be deployed to.</span></span> <span data-ttu-id="fbda6-134">Para este guia, os valores de parâmetro hello não é necessário toobe alterado.</span><span class="sxs-lookup"><span data-stu-id="fbda6-134">For this guide, hello parameter values do not need toobe changed.</span></span> <span data-ttu-id="fbda6-135">modelos de gerenciamento de API e o Gerenciador de recursos de malha do serviço Olá usam esses valores, para que se eles são modificados, você deve modificar no hello outros modelos do Gerenciador de recursos adequadamente.</span><span class="sxs-lookup"><span data-stu-id="fbda6-135">hello API Management and Service Fabric Resource Manager templates use these values, so if they are modified here, you must modify them in hello other Resource Manager templates accordingly.</span></span> 

 1. <span data-ttu-id="fbda6-136">Baixe Olá arquivo de modelo e os parâmetros do Gerenciador de recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="fbda6-136">Download hello following Resource Manager template and parameters file:</span></span>

    - <span data-ttu-id="fbda6-137">[network.json][network-arm]</span><span class="sxs-lookup"><span data-stu-id="fbda6-137">[network.json][network-arm]</span></span>
    - <span data-ttu-id="fbda6-138">[network.parameters.json][network-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="fbda6-138">[network.parameters.json][network-parameters-arm]</span></span>

 2. <span data-ttu-id="fbda6-139">Use Olá PowerShell toodeploy Olá Gerenciador de recursos modelo e o parâmetro de arquivos de comando para configurar uma rede Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="fbda6-139">Use hello following PowerShell command toodeploy hello Resource Manager template and parameter files for hello network setup:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\network.json -TemplateParameterFile .\network.parameters.json -Verbose
    ```

### <a name="deploy-hello-service-fabric-cluster"></a><span data-ttu-id="fbda6-140">Implantar um cluster do Service Fabric Olá</span><span class="sxs-lookup"><span data-stu-id="fbda6-140">Deploy hello Service Fabric cluster</span></span>

<span data-ttu-id="fbda6-141">Depois de terminarem de recursos de rede Olá implantando, Olá próxima etapa é toodeploy um toohello de cluster do Service Fabric rede virtual na sub-rede hello e NSG designado para o cluster do Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="fbda6-141">Once hello network resources have finished deploying, hello next step is toodeploy a Service Fabric cluster toohello VNET in hello subnet and NSG designated for hello Service Fabric cluster.</span></span> <span data-ttu-id="fbda6-142">Para este tutorial, o modelo de serviço Gerenciador de recursos de malha de Olá é toouse pré-configurado Olá nomes Olá rede virtual, sub-rede e NSG que você configurou na etapa anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="fbda6-142">For this tutorial, hello Service Fabric Resource Manager template is pre-configured toouse hello names of hello VNET, subnet, and NSG that you set up in hello previous step.</span></span> 

<span data-ttu-id="fbda6-143">modelo de Gerenciador de recursos de cluster Olá Service Fabric é configurado toocreate um cluster seguro com segurança de certificado.</span><span class="sxs-lookup"><span data-stu-id="fbda6-143">hello Service Fabric cluster Resource Manager template is configured toocreate a secure cluster with certificate security.</span></span> <span data-ttu-id="fbda6-144">certificado de saudação é comunicação de nó para nó toosecure usado para o cluster e o cluster do Service Fabric do toomanage usuário acesso tooyour.</span><span class="sxs-lookup"><span data-stu-id="fbda6-144">hello certificate is used toosecure node-to-node communication for your cluster and toomanage user access tooyour Service Fabric cluster.</span></span> <span data-ttu-id="fbda6-145">Gerenciamento de API usa saudação de tooaccess este certificado o serviço de nomes de malha de serviço para descoberta de serviço.</span><span class="sxs-lookup"><span data-stu-id="fbda6-145">API Management uses this certificate tooaccess  hello Service Fabric Naming Service for service discovery.</span></span>

<span data-ttu-id="fbda6-146">Esta etapa exige ter um certificado no Key Vault para segurança de cluster.</span><span class="sxs-lookup"><span data-stu-id="fbda6-146">This step requires having a certificate in Key Vault for cluster security.</span></span> <span data-ttu-id="fbda6-147">Para obter mais informações sobre como configurar um cluster seguro com o Key Vault, consulte [este guia em criar um cluster no Azure usando o Resource Manager](service-fabric-cluster-creation-via-arm.md)</span><span class="sxs-lookup"><span data-stu-id="fbda6-147">For more information on setting up a secure cluster with Key Vault, see [this guide on creating a cluster in Azure using Resource Manager](service-fabric-cluster-creation-via-arm.md)</span></span>

> [!NOTE]
> <span data-ttu-id="fbda6-148">Você pode adicionar a autenticação do Active Directory do Azure em adição toohello certificado usado para acesso ao cluster.</span><span class="sxs-lookup"><span data-stu-id="fbda6-148">You may add Azure Active Directory authentication in addition toohello certificate used for cluster access.</span></span> <span data-ttu-id="fbda6-149">Active Directory do Azure é hello recomendado cluster do Service Fabric tooyour de acesso do modo toomanage usuário, mas é toocomplete não é necessário neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="fbda6-149">Azure Active Directory is hello recommended way toomanage user access tooyour Service Fabric cluster, but is not necessary toocomplete this tutorial.</span></span> <span data-ttu-id="fbda6-150">Um certificado é exigido de qualquer forma para a segurança de nó para nó de cluster e para autenticação de Gerenciamento de API do Azure, que atualmente não oferece suporte para autenticação com Azure Active Directory para back-end do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="fbda6-150">A certificate is required either way for cluster node-to-node security and for Azure API Management authentication, which currently does not support authenticating with Azure Active Directory for a Service Fabric backend.</span></span>

 1. <span data-ttu-id="fbda6-151">Baixe Olá arquivo de modelo e os parâmetros do Gerenciador de recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="fbda6-151">Download hello following Resource Manager template and parameters file:</span></span>
 
    - <span data-ttu-id="fbda6-152">[cluster.json][cluster-arm]</span><span class="sxs-lookup"><span data-stu-id="fbda6-152">[cluster.json][cluster-arm]</span></span>
    - <span data-ttu-id="fbda6-153">[cluster.parameters.json][cluster-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="fbda6-153">[cluster.parameters.json][cluster-parameters-arm]</span></span>

 2. <span data-ttu-id="fbda6-154">Preenchimento nos parâmetros vazio Olá Olá `cluster.parameters.json` arquivo para sua implantação, incluindo Olá [informações de Cofre de chaves](service-fabric-cluster-creation-via-arm.md#set-up-a-key-vault) para o seu certificado de cluster.</span><span class="sxs-lookup"><span data-stu-id="fbda6-154">Fill in hello empty parameters in hello `cluster.parameters.json` file for your deployment, including hello [Key Vault information](service-fabric-cluster-creation-via-arm.md#set-up-a-key-vault) for your cluster certificate.</span></span>

 3. <span data-ttu-id="fbda6-155">Use Olá PowerShell comando toodeploy Olá Gerenciador de recursos modelo e o parâmetro arquivos toocreate Olá cluster do Service Fabric a seguir:</span><span class="sxs-lookup"><span data-stu-id="fbda6-155">Use hello following PowerShell command toodeploy hello Resource Manager template and parameter files toocreate hello Service Fabric cluster:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\cluster.json -TemplateParameterFile .\cluster.parameters.json -Verbose
    ```

### <a name="deploy-api-management"></a><span data-ttu-id="fbda6-156">Implantar o Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="fbda6-156">Deploy API Management</span></span>

<span data-ttu-id="fbda6-157">Por fim, implantar o gerenciamento de API toohello rede virtual na sub-rede hello e NSG designado para gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="fbda6-157">Finally, deploy API Management toohello VNET in hello subnet and NSG designated for API Management.</span></span> <span data-ttu-id="fbda6-158">Você não precisa toowait para Olá toofinish de implantação de cluster de malha do serviço antes de implantar o gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="fbda6-158">You do not need toowait for hello Service Fabric cluster deployment toofinish before deploying API Management.</span></span> 

<span data-ttu-id="fbda6-159">Para este tutorial, modelo do Gerenciador de recursos de gerenciamento de API de saudação é pré-configurado toouse Olá nomes Olá rede virtual, sub-rede e NSG que você configurou na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="fbda6-159">For this tutorial, hello API Management Resource Manager template is pre-configured toouse hello names of hello VNET, subnet, and NSG that you set up in hello previous step.</span></span> 

 1. <span data-ttu-id="fbda6-160">Baixe Olá arquivo de modelo e os parâmetros do Gerenciador de recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="fbda6-160">Download hello following Resource Manager template and parameters file:</span></span>
 
    - <span data-ttu-id="fbda6-161">[apim.json][apim-arm]</span><span class="sxs-lookup"><span data-stu-id="fbda6-161">[apim.json][apim-arm]</span></span>
    - <span data-ttu-id="fbda6-162">[apim.parameters.json][apim-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="fbda6-162">[apim.parameters.json][apim-parameters-arm]</span></span>

 2. <span data-ttu-id="fbda6-163">Preenchimento nos parâmetros vazio Olá Olá `apim.parameters.json` para sua implantação.</span><span class="sxs-lookup"><span data-stu-id="fbda6-163">Fill in hello empty parameters in hello `apim.parameters.json` for your deployment.</span></span>

 3. <span data-ttu-id="fbda6-164">Use Olá seguintes PowerShell comando toodeploy Olá Gerenciador de recursos modelo e o parâmetro de arquivos para o gerenciamento de API:</span><span class="sxs-lookup"><span data-stu-id="fbda6-164">Use hello following PowerShell command toodeploy hello Resource Manager template and parameter files for API Management:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\apim.json -TemplateParameterFile .\apim.parameters.json -Verbose
    ```

## <a name="configure-api-management"></a><span data-ttu-id="fbda6-165">Configurar o Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="fbda6-165">Configure API Management</span></span>

<span data-ttu-id="fbda6-166">Uma vez que o cluster do Service Fabric e o Gerenciamento de API tenha sido implantado será possível configurar um back-end do Service Fabric no Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="fbda6-166">Once your API Management and Service Fabric cluster are deployed, you can configure a Service Fabric backend in API Management.</span></span> <span data-ttu-id="fbda6-167">Isso permite que você toocreate uma política de serviço de back-end que envia o cluster do tráfego tooyour do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="fbda6-167">This allows you toocreate a backend service policy that sends traffic tooyour Service Fabric cluster.</span></span>

### <a name="api-management-security"></a><span data-ttu-id="fbda6-168">Segurança de Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="fbda6-168">API Management Security</span></span>

<span data-ttu-id="fbda6-169">back-end do Service Fabric de saudação tooconfigure, é necessário primeiro tooconfigure as configurações de segurança do gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="fbda6-169">tooconfigure hello Service Fabric backend, you first need tooconfigure API Management security settings.</span></span> <span data-ttu-id="fbda6-170">configurações de segurança tooconfigure, vá tooyour API do serviço de gerenciamento em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="fbda6-170">tooconfigure security settings, go tooyour API Management service in hello Azure portal.</span></span>

#### <a name="enable-hello-api-management-rest-api"></a><span data-ttu-id="fbda6-171">Habilitar Olá API de REST de gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="fbda6-171">Enable hello API Management REST API</span></span>

<span data-ttu-id="fbda6-172">Olá API REST de API de gerenciamento está atualmente Olá tooconfigure somente da forma um serviço de back-end.</span><span class="sxs-lookup"><span data-stu-id="fbda6-172">hello API Management REST API is currently hello only way tooconfigure a backend service.</span></span> <span data-ttu-id="fbda6-173">Olá primeira etapa é tooenable hello API de REST de gerenciamento de API e protegê-lo.</span><span class="sxs-lookup"><span data-stu-id="fbda6-173">hello first step is tooenable hello API Management REST API and secure it.</span></span>

 1. <span data-ttu-id="fbda6-174">No serviço de gerenciamento de API de Olá, selecione **API de gerenciamento - visualização** em **segurança**.</span><span class="sxs-lookup"><span data-stu-id="fbda6-174">In hello API Management service, select **Management API - PREVIEW** under **Security**.</span></span>
 2. <span data-ttu-id="fbda6-175">Verificar Olá **Habilitar API REST de gerenciamento de API** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="fbda6-175">Check hello **Enable API Management REST API** checkbox.</span></span>
 3. <span data-ttu-id="fbda6-176">Observação: Olá URL da API de gerenciamento - esta é a URL Olá usaremos posterior tooset o back-end do Service Fabric de saudação</span><span class="sxs-lookup"><span data-stu-id="fbda6-176">Note hello Management API URL - this is hello URL we'll use later tooset up hello Service Fabric backend</span></span>
 4. <span data-ttu-id="fbda6-177">Gerar um **Token de acesso** selecionando uma data de expiração e uma chave, em seguida, clique em Olá **gerar** botão em direção à parte inferior de saudação da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="fbda6-177">Generate an **access Token** by selecting an expiry date and a key, then click hello **Generate** button toward hello bottom of hello page.</span></span>
 5. <span data-ttu-id="fbda6-178">Saudação de cópia **token de acesso** e salvá-lo - usaremos isso Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="fbda6-178">Copy hello **access token** and save it - we'll use this in hello following steps.</span></span> <span data-ttu-id="fbda6-179">Observe que isso é diferente da chave de saudação primária e secundária.</span><span class="sxs-lookup"><span data-stu-id="fbda6-179">Note this is different from hello primary key and secondary key.</span></span>

#### <a name="upload-a-service-fabric-client-certificate"></a><span data-ttu-id="fbda6-180">Upload de um certificado do cliente do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="fbda6-180">Upload a Service Fabric client certificate</span></span>

<span data-ttu-id="fbda6-181">Gerenciamento de API deve ser autenticado com o cluster do Service Fabric para descoberta de serviço usando um certificado de cliente que tem acesso tooyour cluster.</span><span class="sxs-lookup"><span data-stu-id="fbda6-181">API Management must authenticate with your Service Fabric cluster for service discovery using a client certificate that has access tooyour cluster.</span></span> <span data-ttu-id="fbda6-182">Para simplificar, este tutorial usa Olá mesmo certificado especificado durante a criação de cluster do Service Fabric hello, o que, por padrão, pode ser usado tooaccess seu cluster.</span><span class="sxs-lookup"><span data-stu-id="fbda6-182">For simplicity, this tutorial uses hello same certificate specified when creating hello Service Fabric cluster, which by default can be used tooaccess your cluster.</span></span>

 1. <span data-ttu-id="fbda6-183">No serviço de gerenciamento de API de Olá, selecione **certificados de cliente - visualização** em **segurança**.</span><span class="sxs-lookup"><span data-stu-id="fbda6-183">In hello API Management service, select **Client certificates - PREVIEW** under **Security**.</span></span>
 2. <span data-ttu-id="fbda6-184">Clique em Olá **+ adicionar** botão</span><span class="sxs-lookup"><span data-stu-id="fbda6-184">Click hello **+ Add** button</span></span>
 2. <span data-ttu-id="fbda6-185">Selecione Olá arquivo de chave privada (. pfx) do certificado de cluster Olá que você especificou ao criar o cluster do Service Fabric, dê a ele um nome e fornecer a senha da chave privada hello.</span><span class="sxs-lookup"><span data-stu-id="fbda6-185">Select hello private key file (.pfx) of hello cluster certificate that you specified when creating your Service Fabric cluster, give it a name, and provide hello private key password.</span></span>

> [!NOTE]
> <span data-ttu-id="fbda6-186">Este tutorial usa Olá mesmo certificado de segurança do cliente autenticação e o cluster de nó para nó.</span><span class="sxs-lookup"><span data-stu-id="fbda6-186">This tutorial uses hello same certificate for client authentication and cluster node-to-node security.</span></span> <span data-ttu-id="fbda6-187">Você pode usar um certificado de cliente separados se você tiver um tooaccess configurado o cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="fbda6-187">You may use a separate client certificate if you have one configured tooaccess your Service Fabric cluster.</span></span>

### <a name="configure-hello-backend"></a><span data-ttu-id="fbda6-188">Configurar Olá back-end</span><span class="sxs-lookup"><span data-stu-id="fbda6-188">Configure hello backend</span></span>

<span data-ttu-id="fbda6-189">Agora que a configuração de segurança do gerenciamento de API, você pode configurar o back-end do hello Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="fbda6-189">Now that API Management security is configured, you can configure hello Service Fabric backend.</span></span> <span data-ttu-id="fbda6-190">Para a malha do serviço back-ends, cluster do Service Fabric Olá é Olá back-end, em vez de um serviço de malha do serviço específico.</span><span class="sxs-lookup"><span data-stu-id="fbda6-190">For Service Fabric backends, hello Service Fabric cluster is hello backend, rather than a specific Service Fabric service.</span></span> <span data-ttu-id="fbda6-191">Isso permite que toomore de tooroute uma única política de um serviço em cluster hello.</span><span class="sxs-lookup"><span data-stu-id="fbda6-191">This allows a single policy tooroute toomore than one service in hello cluster.</span></span>

<span data-ttu-id="fbda6-192">Esta etapa requer um token de acesso de saudação gerada anteriormente e Olá a impressão digital do seu certificado de cluster que você carregou tooAPI gerenciamento na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="fbda6-192">This step requires hello access token you generated earlier and hello thumbprint for your cluster certificate you uploaded tooAPI Management in hello previous step.</span></span>

> [!NOTE]
> <span data-ttu-id="fbda6-193">Se você usou um certificado de cliente separado na etapa anterior Olá para gerenciamento de API, você precisa de impressão digital de Olá Olá certificado de cliente em adição toohello cluster impressão digital de certificado nesta etapa.</span><span class="sxs-lookup"><span data-stu-id="fbda6-193">If you used a separate client certificate in hello previous step for API Management, you need hello thumbprint for hello client certificate in addition toohello cluster certificate thumbprint in this step.</span></span>

<span data-ttu-id="fbda6-194">Envie Olá toohello de solicitação HTTP PUT URL de API de gerenciamento de API observado anteriormente ao habilitar o serviço de back-end do hello API de REST de gerenciamento de API tooconfigure Olá malha do serviço a seguir.</span><span class="sxs-lookup"><span data-stu-id="fbda6-194">Send hello following HTTP PUT request toohello API Management API URL you noted earlier when enabling hello API Management REST API tooconfigure hello Service Fabric backend service.</span></span> <span data-ttu-id="fbda6-195">Você deve ver uma `HTTP 201 Created` resposta ao comando Olá terá êxito.</span><span class="sxs-lookup"><span data-stu-id="fbda6-195">You should see an `HTTP 201 Created` response when hello command succeeds.</span></span> <span data-ttu-id="fbda6-196">Para obter mais informações sobre cada campo, consulte Olá gerenciamento de API [documentação de referência de API de back-end](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend).</span><span class="sxs-lookup"><span data-stu-id="fbda6-196">For more information on each field, see hello API Management [backend API reference documentation](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend).</span></span>

<span data-ttu-id="fbda6-197">Comando HTTP e URL:</span><span class="sxs-lookup"><span data-stu-id="fbda6-197">HTTP command and URL:</span></span>
```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
```

<span data-ttu-id="fbda6-198">Cabeçalhos de solicitação:</span><span class="sxs-lookup"><span data-stu-id="fbda6-198">Request headers:</span></span>
```http
Authorization: SharedAccessSignature <your access token>
Content-Type: application/json
```

<span data-ttu-id="fbda6-199">Corpo da solicitação:</span><span class="sxs-lookup"><span data-stu-id="fbda6-199">Request body:</span></span>
```http
{
    "description": "<description>",
    "url": "<fallback service name>",
    "protocol": "http",
    "resourceId": "<cluster HTTP management endpoint>",
    "properties": {
        "serviceFabricCluster": {
            "managementEndpoints": [ "<cluster HTTP management endpoint>" ],
            "clientCertificateThumbprint": "<client cert thumbprint>",
            "serverCertificateThumbprints": [ "<cluster cert thumbprint>" ],
            "maxPartitionResolutionRetries" : 5
        }
    }
}
```

<span data-ttu-id="fbda6-200">Olá **url** parâmetro aqui é um nome de serviço totalmente qualificado de um serviço em cluster que todas as solicitações são roteadas tooby padrão se nenhum nome de serviço é especificado em uma política de back-end.</span><span class="sxs-lookup"><span data-stu-id="fbda6-200">hello **url** parameter here is a fully-qualified service name of a service in your cluster that all requests are routed tooby default if no service name is specified in a backend policy.</span></span> <span data-ttu-id="fbda6-201">Você pode usar um nome de serviço falsos, como "fabric: / falso/serviço" Se você não pretende toohave um serviço de fallback.</span><span class="sxs-lookup"><span data-stu-id="fbda6-201">You may use a fake service name, such as "fabric:/fake/service" if you do not intend toohave a fallback service.</span></span>

<span data-ttu-id="fbda6-202">Consulte toohello gerenciamento de API [documentação de referência de API de back-end](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend) para obter mais detalhes sobre cada campo.</span><span class="sxs-lookup"><span data-stu-id="fbda6-202">Refer toohello API Management [backend API reference documentation](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend) for more details on each field.</span></span>

#### <a name="example"></a><span data-ttu-id="fbda6-203">Exemplo</span><span class="sxs-lookup"><span data-stu-id="fbda6-203">Example</span></span>

```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
Authorization: SharedAccessSignature 230948023984&Ld93cRGcNU6KZ4uVz7JlfTec4eX43Q9Nu8ndatOgBzs6+f559Pkf3iHX2cSge+r42pn35qGY3TitjrIl13hwcQ==
Content-Type: application/json

{
    "description": "My Service Fabric backend",
    "url": "fabric:/myapp/myservice",
    "protocol": "http",
    "resourceId": "https://your-cluster.westus.cloudapp.azure.com:19080",
    "properties": {
        "serviceFabricCluster": {
            "managementEndpoints": ["https://your-cluster.westus.cloudapp.azure.com:19080"],
            "clientCertificateThumbprint": "57bc463aba3aea3a12a18f36f44154f819f0fe32",
            "serverCertificateThumbprints": ["57bc463aba3aea3a12a18f36f44154f819f0fe32"],
            "maxPartitionResolutionRetries" : 5
        }
    }
}
```

## <a name="deploy-a-service-fabric-back-end-service"></a><span data-ttu-id="fbda6-204">Implantar um serviço de back-end do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="fbda6-204">Deploy a Service Fabric back-end service</span></span>

<span data-ttu-id="fbda6-205">Agora que você tem Olá que Service Fabric configurado como um gerenciamento de tooAPI de back-end, você pode criar políticas de back-end para suas APIs que enviam tráfego tooyour os serviços do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="fbda6-205">Now that you have hello Service Fabric configured as a backend tooAPI Management, you can author backend policies for your APIs that send traffic tooyour Service Fabric services.</span></span> <span data-ttu-id="fbda6-206">Mas primeiro você precisa de um serviço em execução no Service Fabric tooaccept solicitações.</span><span class="sxs-lookup"><span data-stu-id="fbda6-206">But first you need a service running in Service Fabric tooaccept requests.</span></span>

### <a name="create-a-service-fabric-service-with-an-http-endpoint"></a><span data-ttu-id="fbda6-207">Criar um serviço do Service Fabric com um ponto de extremidade HTTP</span><span class="sxs-lookup"><span data-stu-id="fbda6-207">Create a Service Fabric service with an HTTP endpoint</span></span>

<span data-ttu-id="fbda6-208">Para este tutorial, criaremos um básica sem monitoração de estado ASP.NET Core serviço confiável usando o modelo de projeto de API da Web saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="fbda6-208">For this tutorial, we'll create a basic stateless ASP.NET Core Reliable Service using hello default Web API project template.</span></span> <span data-ttu-id="fbda6-209">Isso cria um ponto de extremidade HTTP para o seu serviço que será exposto através do Gerenciamento de API do Azure:</span><span class="sxs-lookup"><span data-stu-id="fbda6-209">This creates an HTTP endpoint for your service, which you'll expose through Azure API Management:</span></span>

```
/api/values
```

<span data-ttu-id="fbda6-210">Inicie [configurando seu ambiente de desenvolvimento para o desenvolvimento de ASP.NET Core](service-fabric-add-a-web-frontend.md#set-up-your-environment-for-aspnet-core).</span><span class="sxs-lookup"><span data-stu-id="fbda6-210">Start by [setting up your development environment for ASP.NET Core development](service-fabric-add-a-web-frontend.md#set-up-your-environment-for-aspnet-core).</span></span>

<span data-ttu-id="fbda6-211">Após configurar seu ambiente de desenvolvimento, inicie o Visual Studio como Administrador e crie um serviço ASP.NET Core:</span><span class="sxs-lookup"><span data-stu-id="fbda6-211">Once your development environment is set up, start Visual Studio as Administrator and create an ASP.NET Core service:</span></span>

 1. <span data-ttu-id="fbda6-212">No Visual Studio, selecione Arquivo -> Novo projeto.</span><span class="sxs-lookup"><span data-stu-id="fbda6-212">In Visual Studio, select File -> New Project.</span></span>
 2. <span data-ttu-id="fbda6-213">Selecione o modelo de aplicativo do Service Fabric Olá em nuvem e nomeie- **"ApiApplication"**.</span><span class="sxs-lookup"><span data-stu-id="fbda6-213">Select hello Service Fabric Application template under Cloud and name it **"ApiApplication"**.</span></span>
 3. <span data-ttu-id="fbda6-214">Selecione hello modelo de serviço do ASP.NET Core e o projeto de saudação do nome **"WebApiService"**.</span><span class="sxs-lookup"><span data-stu-id="fbda6-214">Select hello ASP.NET Core service template and name hello project **"WebApiService"**.</span></span>
 4. <span data-ttu-id="fbda6-215">Selecione o modelo de projeto Olá Web API ASP.NET Core 1.1.</span><span class="sxs-lookup"><span data-stu-id="fbda6-215">Select hello Web API ASP.NET Core 1.1 project template.</span></span>
 5. <span data-ttu-id="fbda6-216">Depois de criar o projeto hello, abra `PackageRoot\ServiceManifest.xml` e remover Olá `Port` atributo da configuração de recurso de ponto de extremidade de saudação:</span><span class="sxs-lookup"><span data-stu-id="fbda6-216">Once hello project is created, open `PackageRoot\ServiceManifest.xml` and remove hello `Port` attribute from hello endpoint resource configuration:</span></span>
 
    ```xml
    <Resources>
      <Endpoints>
        <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" />
      </Endpoints>
    </Resources>
    ```

    <span data-ttu-id="fbda6-217">Isso permite Service Fabric toospecify uma porta dinamicamente a partir do intervalo de portas do aplicativo hello, que são abertas pelo Olá grupo de segurança de rede no modelo de Gerenciador de recursos de cluster Olá, permitindo que o tráfego tooflow tooit do gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="fbda6-217">This allows Service Fabric toospecify a port dynamically from hello application port range, which we opened through hello Network Security Group in hello cluster Resource Manager template, allowing traffic tooflow tooit from API Management.</span></span>
 
 6. <span data-ttu-id="fbda6-218">Pressione F5 na API da web do hello Visual Studio tooverify está disponível localmente.</span><span class="sxs-lookup"><span data-stu-id="fbda6-218">Press F5 in Visual Studio tooverify hello web API is available locally.</span></span> 

    <span data-ttu-id="fbda6-219">Abra o Gerenciador do Service Fabric e Detalhar tooa a instância específica de saudação ASP.NET Core toosee Olá endereço base Olá serviço está escutando.</span><span class="sxs-lookup"><span data-stu-id="fbda6-219">Open Service Fabric Explorer and drill down tooa specific instance of hello ASP.NET Core service toosee hello base address hello service is listening on.</span></span> <span data-ttu-id="fbda6-220">Adicionar `/api/values` toohello endereço base e abri-lo em um navegador.</span><span class="sxs-lookup"><span data-stu-id="fbda6-220">Add `/api/values` toohello base address and open it in a browser.</span></span> <span data-ttu-id="fbda6-221">Isso chama Olá método Get em Olá ValuesController no modelo de API da Web hello.</span><span class="sxs-lookup"><span data-stu-id="fbda6-221">This invokes hello Get method on hello ValuesController in hello Web API template.</span></span> <span data-ttu-id="fbda6-222">Ele retorna a resposta padrão Olá fornecida pelo modelo hello, uma matriz JSON que contém duas cadeias de caracteres:</span><span class="sxs-lookup"><span data-stu-id="fbda6-222">It returns hello default response that is provided by hello template, a JSON array that contains two strings:</span></span>

    ```json
    ["value1", "value2"]`
    ```

    <span data-ttu-id="fbda6-223">Este é o ponto de extremidade de saudação que irá expor por meio do gerenciamento de API no Azure.</span><span class="sxs-lookup"><span data-stu-id="fbda6-223">This is hello endpoint that you'll expose through API Management in Azure.</span></span>

 7. <span data-ttu-id="fbda6-224">Por fim, implante o cluster de tooyour Olá aplicativo no Azure.</span><span class="sxs-lookup"><span data-stu-id="fbda6-224">Finally, deploy hello application tooyour cluster in Azure.</span></span> <span data-ttu-id="fbda6-225">[Usando o Visual Studio](service-fabric-publish-app-remote-cluster.md#to-publish-an-application-using-the-publish-service-fabric-application-dialog-box), projeto de aplicativo hello e selecione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="fbda6-225">[Using Visual Studio](service-fabric-publish-app-remote-cluster.md#to-publish-an-application-using-the-publish-service-fabric-application-dialog-box), right-click hello Application project and select **Publish**.</span></span> <span data-ttu-id="fbda6-226">Forneça seu ponto de extremidade do cluster (por exemplo, `mycluster.westus.cloudapp.azure.com:19000`) toodeploy Olá aplicativo tooyour malha do serviço de cluster no Azure.</span><span class="sxs-lookup"><span data-stu-id="fbda6-226">Provide your cluster endpoint (for example, `mycluster.westus.cloudapp.azure.com:19000`) toodeploy hello application tooyour Service Fabric cluster in Azure.</span></span>

<span data-ttu-id="fbda6-227">Um serviço sem estado ASP.NET Core nomeado `fabric:/ApiApplication/WebApiService` agora deve estar em execução no seu cluster do Service Fabric no Azure.</span><span class="sxs-lookup"><span data-stu-id="fbda6-227">An ASP.NET Core stateless service named `fabric:/ApiApplication/WebApiService` should now be running in your Service Fabric cluster in Azure.</span></span>

## <a name="create-an-api-operation"></a><span data-ttu-id="fbda6-228">Criar uma operação de API</span><span class="sxs-lookup"><span data-stu-id="fbda6-228">Create an API operation</span></span>

<span data-ttu-id="fbda6-229">Agora estamos pronto toocreate uma operação no gerenciamento de API que toocommunicate de uso de clientes externos com hello serviço sem monitoração de estado do ASP.NET Core em execução no cluster do Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="fbda6-229">Now we're ready toocreate an operation in API Management that external clients use toocommunicate with hello ASP.NET Core stateless service running in hello Service Fabric cluster.</span></span>

 1. <span data-ttu-id="fbda6-230">Faça logon no portal do Azure de toohello e navegue tooyour implantação do serviço de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="fbda6-230">Log in toohello Azure portal and navigate tooyour API Management service deployment.</span></span>
 2. <span data-ttu-id="fbda6-231">Na folha de serviço de gerenciamento de API hello, selecione **APIs - visualização**</span><span class="sxs-lookup"><span data-stu-id="fbda6-231">In hello API Management service blade, select **APIs - Preview**</span></span>
 3. <span data-ttu-id="fbda6-232">Adicionar uma nova API clicando Olá **API em branco** caixa e preenchendo a caixa de diálogo hello:</span><span class="sxs-lookup"><span data-stu-id="fbda6-232">Add a new API by clicking hello **Blank API** box and filling out hello dialog box:</span></span>

     - <span data-ttu-id="fbda6-233">**URL do serviço Web**: para back-ends do Service Fabric esse valor de URL não é utilizado.</span><span class="sxs-lookup"><span data-stu-id="fbda6-233">**Web service URL**: For Service Fabric backends, this URL value is not used.</span></span> <span data-ttu-id="fbda6-234">Aqui, você pode colocar qualquer valor.</span><span class="sxs-lookup"><span data-stu-id="fbda6-234">You can put any value here.</span></span> <span data-ttu-id="fbda6-235">Neste tutorial, utilize: `http://servicefabric`.</span><span class="sxs-lookup"><span data-stu-id="fbda6-235">For this tutorial, use: `http://servicefabric`.</span></span>
     - <span data-ttu-id="fbda6-236">**Nome**: forneça qualquer nome para sua API.</span><span class="sxs-lookup"><span data-stu-id="fbda6-236">**Name**: Provide any name for your API.</span></span> <span data-ttu-id="fbda6-237">Neste tutorial, utilize `Service Fabric App`.</span><span class="sxs-lookup"><span data-stu-id="fbda6-237">For this tutorial, use `Service Fabric App`.</span></span>
     - <span data-ttu-id="fbda6-238">**Esquema de URL**: selecione HTTP, HTTPS ou ambos.</span><span class="sxs-lookup"><span data-stu-id="fbda6-238">**URL scheme**: Select either HTTP, HTTPS, or both.</span></span> <span data-ttu-id="fbda6-239">Neste tutorial, utilize `both`.</span><span class="sxs-lookup"><span data-stu-id="fbda6-239">For this tutorial, use `both`.</span></span>
     - <span data-ttu-id="fbda6-240">**Sufixo de URL da API**: forneça um sufixo para a API.</span><span class="sxs-lookup"><span data-stu-id="fbda6-240">**API URL Suffix**: Provide a suffix for our API.</span></span> <span data-ttu-id="fbda6-241">Neste tutorial, utilize `myapp`.</span><span class="sxs-lookup"><span data-stu-id="fbda6-241">For this tutorial, use `myapp`.</span></span>
 
 4. <span data-ttu-id="fbda6-242">Depois de criar hello API, clique em **+ Adicionar operação** operação tooadd uma API de front-end.</span><span class="sxs-lookup"><span data-stu-id="fbda6-242">Once hello API is created, click **+ Add operation** tooadd a front-end API operation.</span></span> <span data-ttu-id="fbda6-243">Preencha valores hello:</span><span class="sxs-lookup"><span data-stu-id="fbda6-243">Fill out hello values:</span></span>
    
     - <span data-ttu-id="fbda6-244">**URL**: selecione `GET` e fornecer um caminho de URL para Olá API.</span><span class="sxs-lookup"><span data-stu-id="fbda6-244">**URL**: Select `GET` and provide a URL path for hello API.</span></span> <span data-ttu-id="fbda6-245">Neste tutorial, utilize `/api/values`.</span><span class="sxs-lookup"><span data-stu-id="fbda6-245">For this tutorial, use `/api/values`.</span></span>
     
       <span data-ttu-id="fbda6-246">Por padrão, o caminho de URL Olá especificado aqui é o caminho da URL Olá enviado toohello serviço de malha do serviço de back-end.</span><span class="sxs-lookup"><span data-stu-id="fbda6-246">By default, hello URL path specified here is hello URL path sent toohello backend Service Fabric service.</span></span> <span data-ttu-id="fbda6-247">Se você usar o hello mesmo caminho URL aqui que o serviço usa, nesse caso `/api/values`, em seguida, a operação de saudação funciona sem modificações adicionais.</span><span class="sxs-lookup"><span data-stu-id="fbda6-247">If you use hello same URL path here that your service uses, in this case `/api/values`, then hello operation works without further modification.</span></span> <span data-ttu-id="fbda6-248">Você também pode especificar um caminho de URL aqui o que é diferente do caminho da URL Olá usado pelo seu back-end, o serviço de malha do serviço, caso em que você vai também toospecify necessidade de reconfiguração de um caminho em sua política de operação mais tarde.</span><span class="sxs-lookup"><span data-stu-id="fbda6-248">You may also specify a URL path here that is different from hello URL path used by your backend Service Fabric service, in which case you will also need toospecify a path rewrite in your operation policy later.</span></span>
     - <span data-ttu-id="fbda6-249">**Nome de exibição**: forneça qualquer nome para Olá API.</span><span class="sxs-lookup"><span data-stu-id="fbda6-249">**Display name**: Provide any name for hello API.</span></span> <span data-ttu-id="fbda6-250">Neste tutorial, utilize `Values`.</span><span class="sxs-lookup"><span data-stu-id="fbda6-250">For this tutorial, use `Values`.</span></span>

## <a name="configure-a-backend-policy"></a><span data-ttu-id="fbda6-251">Configure uma política de back-end</span><span class="sxs-lookup"><span data-stu-id="fbda6-251">Configure a backend policy</span></span>

<span data-ttu-id="fbda6-252">política de back-end Olá reúne tudo.</span><span class="sxs-lookup"><span data-stu-id="fbda6-252">hello backend policy ties everything together.</span></span> <span data-ttu-id="fbda6-253">Isso é onde você configura o back-end Olá Service Fabric toowhich solicitações são roteadas.</span><span class="sxs-lookup"><span data-stu-id="fbda6-253">This is where you configure hello backend Service Fabric service toowhich requests are routed.</span></span> <span data-ttu-id="fbda6-254">Você pode aplicar essa operação da API tooany política.</span><span class="sxs-lookup"><span data-stu-id="fbda6-254">You can apply this policy tooany API operation.</span></span> <span data-ttu-id="fbda6-255">Olá [configuração de back-end para a malha do serviço](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService) fornece controles de roteamentos de solicitação a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="fbda6-255">hello [backend configuration for Service Fabric](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService) provides hello following request routing controls:</span></span> 
 - <span data-ttu-id="fbda6-256">Seleção de instância de serviço especificando um nome de instância de serviço do Service Fabric, ou codificados (por exemplo, `"fabric:/myapp/myservice"`) ou gerado a partir da solicitação HTTP de saudação (por exemplo, `"fabric:/myapp/users/" + context.Request.MatchedParameters["name"]`).</span><span class="sxs-lookup"><span data-stu-id="fbda6-256">Service instance selection by specifying a Service Fabric service instance name, either hardcoded (for example, `"fabric:/myapp/myservice"`) or generated from hello HTTP request (for example, `"fabric:/myapp/users/" + context.Request.MatchedParameters["name"]`).</span></span>
 - <span data-ttu-id="fbda6-257">Resolução de partição gerando uma chave de partição utilizando qualquer esquema de particionamento do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="fbda6-257">Partition resolution by generating a partition key using any Service Fabric partitioning scheme.</span></span>
 - <span data-ttu-id="fbda6-258">Seleção de réplica para serviços com estado.</span><span class="sxs-lookup"><span data-stu-id="fbda6-258">Replica selection for stateful services.</span></span>
 - <span data-ttu-id="fbda6-259">Resolução Repita condições que permitem que você toospecify condições de saudação para resolver novamente um local de serviço e reenviar uma solicitação.</span><span class="sxs-lookup"><span data-stu-id="fbda6-259">Resolution retry conditions that allow you toospecify hello conditions for re-resolving a service location and resending a request.</span></span>

<span data-ttu-id="fbda6-260">Para este tutorial, crie uma política de back-end que rotas diretamente solicitações toohello serviço sem monitoração de estado do ASP.NET Core implantado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="fbda6-260">For this tutorial, create a backend policy that routes requests directly toohello ASP.NET Core stateless service deployed earlier:</span></span>

 1. <span data-ttu-id="fbda6-261">Selecionar e editar Olá **políticas de entrada** para Olá `Values` operação clicando em Editar hello e, em seguida, selecionando **visualização de código**.</span><span class="sxs-lookup"><span data-stu-id="fbda6-261">Select and edit hello **inbound policies** for hello `Values` operation by clicking hello edit icon, and then selecting **Code View**.</span></span>
 2. <span data-ttu-id="fbda6-262">No editor de código de diretiva hello, adicione um `set-backend-service` política em políticas de entrada, conforme mostrado a seguir e clique em Olá **salvar** botão:</span><span class="sxs-lookup"><span data-stu-id="fbda6-262">In hello policy code editor, add a `set-backend-service` policy under inbound policies as shown here and click hello **Save** button:</span></span>
    
    ```xml
    <policies>
      <inbound>
        <base/>
        <set-backend-service 
           backend-id="servicefabric"
           sf-service-instance-name="fabric:/ApiApplication/WebApiService"
           sf-resolve-condition="@((int)context.Response.StatusCode != 200)" />
      </inbound>
      <backend>
        <base/>
      </backend>
      <outbound>
        <base/>
      </outbound>
    </policies>
    ```

<span data-ttu-id="fbda6-263">Para um conjunto completo de atributos de política de back-end do Service Fabric, consulte toohello [documentação de back-end do gerenciamento de API](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService)</span><span class="sxs-lookup"><span data-stu-id="fbda6-263">For a full set of Service Fabric back-end policy attributes, refer toohello [API Management back-end documentation](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService)</span></span>

### <a name="add-hello-api-tooa-product"></a><span data-ttu-id="fbda6-264">Adicione Olá API tooa produto.</span><span class="sxs-lookup"><span data-stu-id="fbda6-264">Add hello API tooa product.</span></span> 

<span data-ttu-id="fbda6-265">Antes de chamar a API de hello, ele deve ser adicionado tooa produto onde você pode conceder acesso toousers.</span><span class="sxs-lookup"><span data-stu-id="fbda6-265">Before you can call hello API, it must be added tooa product where you can grant access toousers.</span></span> 

 1. <span data-ttu-id="fbda6-266">No serviço de gerenciamento de API de Olá, selecione **produtos - visualização**.</span><span class="sxs-lookup"><span data-stu-id="fbda6-266">In hello API Management service, select **Products - PREVIEW**.</span></span>
 2. <span data-ttu-id="fbda6-267">Por padrão, o Gerenciamento de API oferece dois produtos: Starter e Ilimitado.</span><span class="sxs-lookup"><span data-stu-id="fbda6-267">By default, API Management providers two products: Starter and Unlimited.</span></span> <span data-ttu-id="fbda6-268">Selecione produto ilimitados hello.</span><span class="sxs-lookup"><span data-stu-id="fbda6-268">Select hello Unlimited product.</span></span>
 3. <span data-ttu-id="fbda6-269">Selecione APIs.</span><span class="sxs-lookup"><span data-stu-id="fbda6-269">Select APIs.</span></span>
 4. <span data-ttu-id="fbda6-270">Clique em Olá **+ adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="fbda6-270">Click hello **+ Add** button.</span></span>
 5. <span data-ttu-id="fbda6-271">Selecione Olá `Service Fabric App` API que você criou nas etapas anteriores hello e clique em Olá **selecione** botão.</span><span class="sxs-lookup"><span data-stu-id="fbda6-271">Select hello `Service Fabric App` API you created in hello previous steps and click hello **Select** button.</span></span>

### <a name="test-it"></a><span data-ttu-id="fbda6-272">Testá-lo</span><span class="sxs-lookup"><span data-stu-id="fbda6-272">Test it</span></span>

<span data-ttu-id="fbda6-273">Agora você pode tentar enviar uma solicitação de serviço de back-end de tooyour na malha do serviço por meio do gerenciamento de API diretamente da saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="fbda6-273">You can now try sending a request tooyour back-end service in Service Fabric through API Management directly from hello Azure portal.</span></span>

 1. <span data-ttu-id="fbda6-274">No serviço de gerenciamento de API de Olá, selecione **API - visualização**.</span><span class="sxs-lookup"><span data-stu-id="fbda6-274">In hello API Management service, select **API - PREVIEW**.</span></span>
 2. <span data-ttu-id="fbda6-275">Em Olá `Service Fabric App` API que você criou nas etapas anteriores do hello, selecione Olá **teste** guia.</span><span class="sxs-lookup"><span data-stu-id="fbda6-275">In hello `Service Fabric App` API you created in hello previous steps, select hello **Test** tab.</span></span>
 3. <span data-ttu-id="fbda6-276">Clique em Olá **enviar** botão toosend um serviço de back-end de toohello de solicitação de teste.</span><span class="sxs-lookup"><span data-stu-id="fbda6-276">Click hello **Send** button toosend a test request toohello backend service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fbda6-277">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fbda6-277">Next steps</span></span>

<span data-ttu-id="fbda6-278">Neste ponto, é possível ter uma configuração básica com o Service Fabric e o Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="fbda6-278">At this point, you should have a basic setup with Service Fabric and API Management.</span></span>

<span data-ttu-id="fbda6-279">Este tutorial usa a autenticação do usuário básica baseada em certificado para sua tooget de cluster do Service Fabric que configurar rapidamente.</span><span class="sxs-lookup"><span data-stu-id="fbda6-279">This tutorial uses basic certificate-based user authentication for your Service Fabric cluster tooget you set up quickly.</span></span> <span data-ttu-id="fbda6-280">A autenticação de usuário mais avançada para o cluster do Service Fabric é preferível com a [autenticação Azure Active Directory](service-fabric-cluster-creation-via-arm.md#set-up-azure-active-directory-for-client-authentication).</span><span class="sxs-lookup"><span data-stu-id="fbda6-280">More advanced user authentication for your Service Fabric cluster is preferable with [Azure Active Directory authentication](service-fabric-cluster-creation-via-arm.md#set-up-azure-active-directory-for-client-authentication).</span></span> 

<span data-ttu-id="fbda6-281">Em seguida, [criar e configurar as configurações avançadas de produto no gerenciamento de API do Azure](https://docs.microsoft.com/azure/api-management/api-management-howto-product-with-rules) tooprepare seu aplicativo para o tráfego do mundo real.</span><span class="sxs-lookup"><span data-stu-id="fbda6-281">Next, [create and configure advanced product settings in Azure API Management](https://docs.microsoft.com/azure/api-management/api-management-howto-product-with-rules) tooprepare your application for real world traffic.</span></span>

<!-- links -->
[azure-powershell]:https://azure.microsoft.com/documentation/articles/powershell-install-configure/

[network-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/network.json
[network-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/network.parameters.json

[apim-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/apim.json
[apim-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/apim.parameters.json

[cluster-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/cluster.json
[cluster-parameters-arm]:https://github.com/Azure-Samples/service-fabric-api-management/blob/master/cluster.parameters.json


<!-- pics -->
[sf-apim-topology-overview]: ./media/service-fabric-api-management-quickstart/sf-apim-topology-overview.png
