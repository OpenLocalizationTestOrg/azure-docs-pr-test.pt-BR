---
title: "Azure Service Fabric com início rápido de Gerenciamento de API | Microsoft Docs"
description: Este guia mostra como iniciar rapidamente com o Gerenciamento de API e o Service Fabric.
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
ms.openlocfilehash: e9f44d8a43d274768f43261fea68f0da9c681ae1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="service-fabric-with-azure-api-management-quick-start"></a><span data-ttu-id="c4be0-103">Service Fabric com início rápido de Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="c4be0-103">Service Fabric with Azure API Management Quick Start</span></span>

<span data-ttu-id="c4be0-104">Este guia mostra como configurar o Gerenciamento de API do Azure com o Service Fabric e configurar sua primeira operação de API para enviar tráfego para serviços de back-end no Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c4be0-104">This guide shows you how to set up Azure API Management with Service Fabric and configure your first API operation to send traffic to back-end services in Service Fabric.</span></span> <span data-ttu-id="c4be0-105">Para saber mais sobre os cenários do Gerenciamento de API do Azure com Service Fabric, consulte o artigo [visão geral](service-fabric-api-management-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c4be0-105">To learn more about Azure API Management scenarios with Service Fabric, see the [overview](service-fabric-api-management-overview.md) article.</span></span> 

## <a name="deploy-api-management-and-service-fabric-to-azure"></a><span data-ttu-id="c4be0-106">Implantar o Gerenciamento de API e o Service Fabric ao Azure</span><span class="sxs-lookup"><span data-stu-id="c4be0-106">Deploy API Management and Service Fabric to Azure</span></span>

<span data-ttu-id="c4be0-107">A primeira etapa é implantar o Gerenciamento de API e um cluster do Service Fabric no Azure em uma Rede Virtual compartilhada.</span><span class="sxs-lookup"><span data-stu-id="c4be0-107">The first step is to deploy API Management and a Service Fabric cluster to Azure in a shared Virtual Network.</span></span> <span data-ttu-id="c4be0-108">Isso permite que o Gerenciamento de API se comunique diretamente com o Service Fabric para que ele possa executar a descoberta do serviço, a resolução da partição de serviço e encaminhar o tráfego diretamente para qualquer serviço de back-end no Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c4be0-108">This allows API Management to communicate directly with Service Fabric so it can perform service discovery, service partition resolution, and forward traffic directly to any backend service in Service Fabric.</span></span>

### <a name="topology"></a><span data-ttu-id="c4be0-109">Topologia</span><span class="sxs-lookup"><span data-stu-id="c4be0-109">Topology</span></span>

<span data-ttu-id="c4be0-110">Este guia implanta a seguinte topologia para o Azure, na qual o Gerenciamento de API e o Service Fabric estão em sub-redes da mesma Rede Virtual:</span><span class="sxs-lookup"><span data-stu-id="c4be0-110">This guide deploys the following topology to Azure in which API Management and Service Fabric are in subnets of the same Virtual Network:</span></span>

 ![Legenda de imagem][sf-apim-topology-overview]

<span data-ttu-id="c4be0-112">Para iniciar rapidamente, os modelos do Resource Manager são fornecidos para cada etapa de implantação:</span><span class="sxs-lookup"><span data-stu-id="c4be0-112">To get started quickly, Resource Manager templates are provided for each deployment step:</span></span>

 - <span data-ttu-id="c4be0-113">Topologia de rede:</span><span class="sxs-lookup"><span data-stu-id="c4be0-113">Network topology:</span></span>
    - <span data-ttu-id="c4be0-114">[network.json][network-arm]</span><span class="sxs-lookup"><span data-stu-id="c4be0-114">[network.json][network-arm]</span></span>
    - <span data-ttu-id="c4be0-115">[network.parameters.json][network-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="c4be0-115">[network.parameters.json][network-parameters-arm]</span></span>
 - <span data-ttu-id="c4be0-116">Cluster do Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="c4be0-116">Service Fabric cluster:</span></span>
    - <span data-ttu-id="c4be0-117">[cluster.json][cluster-arm]</span><span class="sxs-lookup"><span data-stu-id="c4be0-117">[cluster.json][cluster-arm]</span></span>
    - <span data-ttu-id="c4be0-118">[cluster.parameters.json][cluster-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="c4be0-118">[cluster.parameters.json][cluster-parameters-arm]</span></span>
 - <span data-ttu-id="c4be0-119">Gerenciamento de API:</span><span class="sxs-lookup"><span data-stu-id="c4be0-119">API Management:</span></span>
    - <span data-ttu-id="c4be0-120">[apim.json][apim-arm]</span><span class="sxs-lookup"><span data-stu-id="c4be0-120">[apim.json][apim-arm]</span></span>
    - <span data-ttu-id="c4be0-121">[apim.parameters.json][apim-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="c4be0-121">[apim.parameters.json][apim-parameters-arm]</span></span>

### <a name="sign-in-to-azure-and-select-your-subscription"></a><span data-ttu-id="c4be0-122">Entre no Azure e selecione sua assinatura</span><span class="sxs-lookup"><span data-stu-id="c4be0-122">Sign in to Azure and select your subscription</span></span>

<span data-ttu-id="c4be0-123">Este guia usa o [Azure PowerShell][azure-powershell].</span><span class="sxs-lookup"><span data-stu-id="c4be0-123">This guide uses [Azure PowerShell][azure-powershell].</span></span> <span data-ttu-id="c4be0-124">Ao iniciar uma nova sessão do PowerShell, entre em sua conta do Azure e selecione sua assinatura antes de executar comandos do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4be0-124">When you start a new PowerShell session, sign in to your Azure account and select your subscription before you execute Azure commands.</span></span>
 
<span data-ttu-id="c4be0-125">Entre na sua conta do Azure:</span><span class="sxs-lookup"><span data-stu-id="c4be0-125">Sign in to your Azure account:</span></span>

```powershell
PS > Login-AzureRmAccount
```

<span data-ttu-id="c4be0-126">Selecione sua assinatura:</span><span class="sxs-lookup"><span data-stu-id="c4be0-126">Select your subscription:</span></span>

```powershell
PS > Get-AzureRmSubscription
PS > Set-AzureRmContext -SubscriptionId <guid>
```

### <a name="create-a-resource-group"></a><span data-ttu-id="c4be0-127">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="c4be0-127">Create a resource group</span></span>

<span data-ttu-id="c4be0-128">Crie um novo grupo de recursos para sua implantação.</span><span class="sxs-lookup"><span data-stu-id="c4be0-128">Create a new resource group for your deployment.</span></span> <span data-ttu-id="c4be0-129">Dê um nome e um local.</span><span class="sxs-lookup"><span data-stu-id="c4be0-129">Give it a name and a location.</span></span>

```powershell
PS > New-AzureRmResourceGroup -Name <my-resource-group> -Location westus
```

### <a name="deploy-the-network-topology"></a><span data-ttu-id="c4be0-130">Implante a topologia da rede</span><span class="sxs-lookup"><span data-stu-id="c4be0-130">Deploy the network topology</span></span>

<span data-ttu-id="c4be0-131">O primeiro passo é configurar a topologia de rede para a qual o Gerenciamento de API e o cluster do Service Fabric serão implantados.</span><span class="sxs-lookup"><span data-stu-id="c4be0-131">The first step is to set up the network topology to which API Management and the Service Fabric cluster will be deployed.</span></span> <span data-ttu-id="c4be0-132">O modelo [network.json][network-arm] do Resource Manager é configurado para criar uma VNET (Rede Virtual) com duas sub-redes e dois NSG (Grupos de Segurança de Rede).</span><span class="sxs-lookup"><span data-stu-id="c4be0-132">The [network.json][network-arm] Resource Manager template is configured to create a Virtual Network (VNET) with two subnets and two Network Security Groups (NSG).</span></span> 

<span data-ttu-id="c4be0-133">O arquivo de parâmetros [network.parameters.json][network-parameters-arm] contém os nomes das sub-redes e NSGs em que o Gerenciamento de API e o Service Fabric serão implantados.</span><span class="sxs-lookup"><span data-stu-id="c4be0-133">The [network.parameters.json][network-parameters-arm] parameters file contains the names of the subnets and NSGs that API Management and Service Fabric will be deployed to.</span></span> <span data-ttu-id="c4be0-134">Para este guia, os valores de parâmetros não precisam ser alterados.</span><span class="sxs-lookup"><span data-stu-id="c4be0-134">For this guide, the parameter values do not need to be changed.</span></span> <span data-ttu-id="c4be0-135">Os modelos do Resource Manager do Service Fabric e Gerenciamento de API utilizam esses valores, portanto, se forem aqui modificados, então, será necessário modificá-los nos outros modelos do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c4be0-135">The API Management and Service Fabric Resource Manager templates use these values, so if they are modified here, you must modify them in the other Resource Manager templates accordingly.</span></span> 

 1. <span data-ttu-id="c4be0-136">Baixe o seguinte modelo do Resource Manager e arquivo de parâmetros:</span><span class="sxs-lookup"><span data-stu-id="c4be0-136">Download the following Resource Manager template and parameters file:</span></span>

    - <span data-ttu-id="c4be0-137">[network.json][network-arm]</span><span class="sxs-lookup"><span data-stu-id="c4be0-137">[network.json][network-arm]</span></span>
    - <span data-ttu-id="c4be0-138">[network.parameters.json][network-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="c4be0-138">[network.parameters.json][network-parameters-arm]</span></span>

 2. <span data-ttu-id="c4be0-139">Use o seguinte comando do PowerShell para implantar o modelo do Resource Manager e os arquivos de parâmetros para a configuração de rede:</span><span class="sxs-lookup"><span data-stu-id="c4be0-139">Use the following PowerShell command to deploy the Resource Manager template and parameter files for the network setup:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\network.json -TemplateParameterFile .\network.parameters.json -Verbose
    ```

### <a name="deploy-the-service-fabric-cluster"></a><span data-ttu-id="c4be0-140">Implantar o cluster do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c4be0-140">Deploy the Service Fabric cluster</span></span>

<span data-ttu-id="c4be0-141">Uma vez que os recursos de rede concluíram a implantação, a próxima etapa é implantar um cluster do Service Fabric na VNET na sub-rede e o NSG designado para o cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c4be0-141">Once the network resources have finished deploying, the next step is to deploy a Service Fabric cluster to the VNET in the subnet and NSG designated for the Service Fabric cluster.</span></span> <span data-ttu-id="c4be0-142">Para este tutorial, o modelo do Resource Manager do Service Fabric é pré-configurado para usar os nomes da VNET, sub-rede e do NSG que você configurou na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="c4be0-142">For this tutorial, the Service Fabric Resource Manager template is pre-configured to use the names of the VNET, subnet, and NSG that you set up in the previous step.</span></span> 

<span data-ttu-id="c4be0-143">O modelo do Resource Manager do cluster do Service Fabric é configurado para criar um cluster seguro com segurança de certificado.</span><span class="sxs-lookup"><span data-stu-id="c4be0-143">The Service Fabric cluster Resource Manager template is configured to create a secure cluster with certificate security.</span></span> <span data-ttu-id="c4be0-144">O certificado é utilizado para proteger a comunicação do nó para nó para o seu cluster e gerenciar o acesso do usuário ao seu cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c4be0-144">The certificate is used to secure node-to-node communication for your cluster and to manage user access to your Service Fabric cluster.</span></span> <span data-ttu-id="c4be0-145">O Gerenciamento de API utiliza esse certificado para acessar o Serviço de Cadastramento do Service Fabric para descoberta de serviço.</span><span class="sxs-lookup"><span data-stu-id="c4be0-145">API Management uses this certificate to access  the Service Fabric Naming Service for service discovery.</span></span>

<span data-ttu-id="c4be0-146">Esta etapa exige ter um certificado no Key Vault para segurança de cluster.</span><span class="sxs-lookup"><span data-stu-id="c4be0-146">This step requires having a certificate in Key Vault for cluster security.</span></span> <span data-ttu-id="c4be0-147">Para obter mais informações sobre como configurar um cluster seguro com o Key Vault, consulte [este guia em criar um cluster no Azure usando o Resource Manager](service-fabric-cluster-creation-via-arm.md)</span><span class="sxs-lookup"><span data-stu-id="c4be0-147">For more information on setting up a secure cluster with Key Vault, see [this guide on creating a cluster in Azure using Resource Manager](service-fabric-cluster-creation-via-arm.md)</span></span>

> [!NOTE]
> <span data-ttu-id="c4be0-148">É possível adicionar a autenticação do Azure Active Directory, além do certificado utilizado para acesso ao cluster.</span><span class="sxs-lookup"><span data-stu-id="c4be0-148">You may add Azure Active Directory authentication in addition to the certificate used for cluster access.</span></span> <span data-ttu-id="c4be0-149">O Azure Active Directory é a maneira recomendada para gerenciar o acesso do usuário ao cluster do Service Fabric, mas não é necessário concluir este tutorial.</span><span class="sxs-lookup"><span data-stu-id="c4be0-149">Azure Active Directory is the recommended way to manage user access to your Service Fabric cluster, but is not necessary to complete this tutorial.</span></span> <span data-ttu-id="c4be0-150">Um certificado é exigido de qualquer forma para a segurança de nó para nó de cluster e para autenticação de Gerenciamento de API do Azure, que atualmente não oferece suporte para autenticação com Azure Active Directory para back-end do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c4be0-150">A certificate is required either way for cluster node-to-node security and for Azure API Management authentication, which currently does not support authenticating with Azure Active Directory for a Service Fabric backend.</span></span>

 1. <span data-ttu-id="c4be0-151">Baixe o seguinte modelo do Resource Manager e arquivo de parâmetros:</span><span class="sxs-lookup"><span data-stu-id="c4be0-151">Download the following Resource Manager template and parameters file:</span></span>
 
    - <span data-ttu-id="c4be0-152">[cluster.json][cluster-arm]</span><span class="sxs-lookup"><span data-stu-id="c4be0-152">[cluster.json][cluster-arm]</span></span>
    - <span data-ttu-id="c4be0-153">[cluster.parameters.json][cluster-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="c4be0-153">[cluster.parameters.json][cluster-parameters-arm]</span></span>

 2. <span data-ttu-id="c4be0-154">Preencha os parâmetros vazios no arquivo `cluster.parameters.json` para sua implantação, incluindo as [informações do Key Vault](service-fabric-cluster-creation-via-arm.md#set-up-a-key-vault) para o certificado de cluster.</span><span class="sxs-lookup"><span data-stu-id="c4be0-154">Fill in the empty parameters in the `cluster.parameters.json` file for your deployment, including the [Key Vault information](service-fabric-cluster-creation-via-arm.md#set-up-a-key-vault) for your cluster certificate.</span></span>

 3. <span data-ttu-id="c4be0-155">Utilize o seguinte comando do PowerShell para implantar o modelo do Resource Manager e arquivos de parâmetros para criar o cluster do Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="c4be0-155">Use the following PowerShell command to deploy the Resource Manager template and parameter files to create the Service Fabric cluster:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\cluster.json -TemplateParameterFile .\cluster.parameters.json -Verbose
    ```

### <a name="deploy-api-management"></a><span data-ttu-id="c4be0-156">Implantar o Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="c4be0-156">Deploy API Management</span></span>

<span data-ttu-id="c4be0-157">Finalmente, implante o Gerenciamento de API na VNET na sub-rede e no NSG designado para o Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="c4be0-157">Finally, deploy API Management to the VNET in the subnet and NSG designated for API Management.</span></span> <span data-ttu-id="c4be0-158">Não é necessário aguardar a implantação do cluster do Service Fabric terminar, antes de implantar o gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="c4be0-158">You do not need to wait for the Service Fabric cluster deployment to finish before deploying API Management.</span></span> 

<span data-ttu-id="c4be0-159">Para este tutorial, o modelo do Resource Manager do Gerenciamento de API é pré-configurado para usar os nomes da VNET, sub-rede e do NSG que você configurou na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="c4be0-159">For this tutorial, the API Management Resource Manager template is pre-configured to use the names of the VNET, subnet, and NSG that you set up in the previous step.</span></span> 

 1. <span data-ttu-id="c4be0-160">Baixe o seguinte modelo do Resource Manager e arquivo de parâmetros:</span><span class="sxs-lookup"><span data-stu-id="c4be0-160">Download the following Resource Manager template and parameters file:</span></span>
 
    - <span data-ttu-id="c4be0-161">[apim.json][apim-arm]</span><span class="sxs-lookup"><span data-stu-id="c4be0-161">[apim.json][apim-arm]</span></span>
    - <span data-ttu-id="c4be0-162">[apim.parameters.json][apim-parameters-arm]</span><span class="sxs-lookup"><span data-stu-id="c4be0-162">[apim.parameters.json][apim-parameters-arm]</span></span>

 2. <span data-ttu-id="c4be0-163">Preencha os parâmetros vazios em `apim.parameters.json` para sua implantação.</span><span class="sxs-lookup"><span data-stu-id="c4be0-163">Fill in the empty parameters in the `apim.parameters.json` for your deployment.</span></span>

 3. <span data-ttu-id="c4be0-164">Utilize o seguinte comando do PowerShell para implantar o modelo do Resource Manager e os arquivos de parâmetros para o Gerenciamento de API:</span><span class="sxs-lookup"><span data-stu-id="c4be0-164">Use the following PowerShell command to deploy the Resource Manager template and parameter files for API Management:</span></span>

    ```powershell
    PS > New-AzureRmResourceGroupDeployment -ResourceGroupName <my-resource-group> -TemplateFile .\apim.json -TemplateParameterFile .\apim.parameters.json -Verbose
    ```

## <a name="configure-api-management"></a><span data-ttu-id="c4be0-165">Configurar o Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="c4be0-165">Configure API Management</span></span>

<span data-ttu-id="c4be0-166">Uma vez que o cluster do Service Fabric e o Gerenciamento de API tenha sido implantado será possível configurar um back-end do Service Fabric no Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="c4be0-166">Once your API Management and Service Fabric cluster are deployed, you can configure a Service Fabric backend in API Management.</span></span> <span data-ttu-id="c4be0-167">Isso permite que você crie uma política de serviço de back-end que envia tráfego para o cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c4be0-167">This allows you to create a backend service policy that sends traffic to your Service Fabric cluster.</span></span>

### <a name="api-management-security"></a><span data-ttu-id="c4be0-168">Segurança de Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="c4be0-168">API Management Security</span></span>

<span data-ttu-id="c4be0-169">Para configurar o back-end do Service Fabric, primeiro você precisa definir as configurações de segurança do Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="c4be0-169">To configure the Service Fabric backend, you first need to configure API Management security settings.</span></span> <span data-ttu-id="c4be0-170">Para definir as configurações de segurança, acesse o serviço de Gerenciamento de API no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4be0-170">To configure security settings, go to your API Management service in the Azure portal.</span></span>

#### <a name="enable-the-api-management-rest-api"></a><span data-ttu-id="c4be0-171">Habilite a API REST do Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="c4be0-171">Enable the API Management REST API</span></span>

<span data-ttu-id="c4be0-172">Atualmente, a API REST do Gerenciamento de API é a única maneira de configurar um serviço de back-end.</span><span class="sxs-lookup"><span data-stu-id="c4be0-172">The API Management REST API is currently the only way to configure a backend service.</span></span> <span data-ttu-id="c4be0-173">A primeira etapa é habilitar a API REST do Gerenciamento de API e protegê-la.</span><span class="sxs-lookup"><span data-stu-id="c4be0-173">The first step is to enable the API Management REST API and secure it.</span></span>

 1. <span data-ttu-id="c4be0-174">No serviço de Gerenciamento de API, selecione **API de Gerenciamento - VISUALIZAÇÃO** em **Segurança**.</span><span class="sxs-lookup"><span data-stu-id="c4be0-174">In the API Management service, select **Management API - PREVIEW** under **Security**.</span></span>
 2. <span data-ttu-id="c4be0-175">Marque a caixa de seleção **Habilitar REST API do Gerenciamento de API**.</span><span class="sxs-lookup"><span data-stu-id="c4be0-175">Check the **Enable API Management REST API** checkbox.</span></span>
 3. <span data-ttu-id="c4be0-176">Observe a URL de API de Gerenciamento - essa é a URL que usaremos mais tarde para configurar o back-end do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c4be0-176">Note the Management API URL - this is the URL we'll use later to set up the Service Fabric backend</span></span>
 4. <span data-ttu-id="c4be0-177">Gere um **Token de acesso** selecionando uma data de validade e uma chave e, em seguida, clique no botão **Gerar** no final da página.</span><span class="sxs-lookup"><span data-stu-id="c4be0-177">Generate an **access Token** by selecting an expiry date and a key, then click the **Generate** button toward the bottom of the page.</span></span>
 5. <span data-ttu-id="c4be0-178">Copie o **token de acesso** e salve-o - utilizaremos isso nas seguintes etapas.</span><span class="sxs-lookup"><span data-stu-id="c4be0-178">Copy the **access token** and save it - we'll use this in the following steps.</span></span> <span data-ttu-id="c4be0-179">Observe que isso é diferente da chave primária e da chave secundária.</span><span class="sxs-lookup"><span data-stu-id="c4be0-179">Note this is different from the primary key and secondary key.</span></span>

#### <a name="upload-a-service-fabric-client-certificate"></a><span data-ttu-id="c4be0-180">Upload de um certificado do cliente do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c4be0-180">Upload a Service Fabric client certificate</span></span>

<span data-ttu-id="c4be0-181">O Gerenciamento de API deve autenticar com seu cluster do Service Fabric para descoberta de serviço utilizando um certificado do cliente que tenha acesso ao seu cluster.</span><span class="sxs-lookup"><span data-stu-id="c4be0-181">API Management must authenticate with your Service Fabric cluster for service discovery using a client certificate that has access to your cluster.</span></span> <span data-ttu-id="c4be0-182">Por simplicidade, esse tutorial utiliza o mesmo certificado especificado ao criar o cluster do Service Fabric que, por padrão, pode ser utilizado para acessar seu cluster.</span><span class="sxs-lookup"><span data-stu-id="c4be0-182">For simplicity, this tutorial uses the same certificate specified when creating the Service Fabric cluster, which by default can be used to access your cluster.</span></span>

 1. <span data-ttu-id="c4be0-183">No serviço de gerenciamento de API, selecione **Certificados do cliente - VISUALIZAÇÃO** em **Segurança**.</span><span class="sxs-lookup"><span data-stu-id="c4be0-183">In the API Management service, select **Client certificates - PREVIEW** under **Security**.</span></span>
 2. <span data-ttu-id="c4be0-184">Clique no botão **+ Adicionar**</span><span class="sxs-lookup"><span data-stu-id="c4be0-184">Click the **+ Add** button</span></span>
 2. <span data-ttu-id="c4be0-185">Selecione o arquivo de chave privada (.pfx) do certificado de cluster que você especificou ao criar seu cluster do Service Fabric, atribua um nome e forneça a senha de chave privada.</span><span class="sxs-lookup"><span data-stu-id="c4be0-185">Select the private key file (.pfx) of the cluster certificate that you specified when creating your Service Fabric cluster, give it a name, and provide the private key password.</span></span>

> [!NOTE]
> <span data-ttu-id="c4be0-186">Este tutorial usa o mesmo certificado para autenticação de cliente e segurança de nó a nó de cluster.</span><span class="sxs-lookup"><span data-stu-id="c4be0-186">This tutorial uses the same certificate for client authentication and cluster node-to-node security.</span></span> <span data-ttu-id="c4be0-187">É possível utilizar um certificado do cliente separado se você tiver um configurado para acessar seu cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c4be0-187">You may use a separate client certificate if you have one configured to access your Service Fabric cluster.</span></span>

### <a name="configure-the-backend"></a><span data-ttu-id="c4be0-188">Configure o back-end</span><span class="sxs-lookup"><span data-stu-id="c4be0-188">Configure the backend</span></span>

<span data-ttu-id="c4be0-189">Agora que a segurança do Gerenciamento de API está configurada, é possível configurar o back-end do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c4be0-189">Now that API Management security is configured, you can configure the Service Fabric backend.</span></span> <span data-ttu-id="c4be0-190">Para back-ends do Service Fabric, o cluster do Service Fabric é o back-end, em vez de um serviço do Service Fabric específico.</span><span class="sxs-lookup"><span data-stu-id="c4be0-190">For Service Fabric backends, the Service Fabric cluster is the backend, rather than a specific Service Fabric service.</span></span> <span data-ttu-id="c4be0-191">Isso permite que uma única política encaminhe para mais de um serviço no cluster.</span><span class="sxs-lookup"><span data-stu-id="c4be0-191">This allows a single policy to route to more than one service in the cluster.</span></span>

<span data-ttu-id="c4be0-192">Essa etapa requer o token de acesso gerado anteriormente e a impressão digital do certificado de cluster que você enviou para o Gerenciamento de API na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="c4be0-192">This step requires the access token you generated earlier and the thumbprint for your cluster certificate you uploaded to API Management in the previous step.</span></span>

> [!NOTE]
> <span data-ttu-id="c4be0-193">Se você utilizou um certificado do cliente separado na etapa anterior para o Gerenciamento de API, nessa etapa será necessária a impressão digital para o certificado do cliente, além da impressão digital do certificado de cluster.</span><span class="sxs-lookup"><span data-stu-id="c4be0-193">If you used a separate client certificate in the previous step for API Management, you need the thumbprint for the client certificate in addition to the cluster certificate thumbprint in this step.</span></span>

<span data-ttu-id="c4be0-194">Envie a seguinte solicitação HTTP PUT para a URL da API de Gerenciamento de API que você observou anteriormente ao habilitar a API REST do Gerenciamento de API para configurar o serviço back-end do Serviço Fabric.</span><span class="sxs-lookup"><span data-stu-id="c4be0-194">Send the following HTTP PUT request to the API Management API URL you noted earlier when enabling the API Management REST API to configure the Service Fabric backend service.</span></span> <span data-ttu-id="c4be0-195">Uma resposta `HTTP 201 Created` deverá ser exibida quando o comando for bem-sucedido.</span><span class="sxs-lookup"><span data-stu-id="c4be0-195">You should see an `HTTP 201 Created` response when the command succeeds.</span></span> <span data-ttu-id="c4be0-196">Para obter mais informações sobre cada campo, consulte a [documentação de referência de API do back-end](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend) do Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="c4be0-196">For more information on each field, see the API Management [backend API reference documentation](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend).</span></span>

<span data-ttu-id="c4be0-197">Comando HTTP e URL:</span><span class="sxs-lookup"><span data-stu-id="c4be0-197">HTTP command and URL:</span></span>
```http
PUT https://your-apim.management.azure-api.net/backends/servicefabric?api-version=2016-10-10
```

<span data-ttu-id="c4be0-198">Cabeçalhos de solicitação:</span><span class="sxs-lookup"><span data-stu-id="c4be0-198">Request headers:</span></span>
```http
Authorization: SharedAccessSignature <your access token>
Content-Type: application/json
```

<span data-ttu-id="c4be0-199">Corpo da solicitação:</span><span class="sxs-lookup"><span data-stu-id="c4be0-199">Request body:</span></span>
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

<span data-ttu-id="c4be0-200">O parâmetro **url** nesse exemplo é um nome de serviço totalmente qualificado de um serviço em seu cluster onde todos os pedidos são roteados por padrão se nenhum nome de serviço for especificado em uma política de back-end.</span><span class="sxs-lookup"><span data-stu-id="c4be0-200">The **url** parameter here is a fully-qualified service name of a service in your cluster that all requests are routed to by default if no service name is specified in a backend policy.</span></span> <span data-ttu-id="c4be0-201">É possível utilizar um nome de serviço falso, como "fabric:/serviço/falso" se você não pretende ter um serviço de fallback.</span><span class="sxs-lookup"><span data-stu-id="c4be0-201">You may use a fake service name, such as "fabric:/fake/service" if you do not intend to have a fallback service.</span></span>

<span data-ttu-id="c4be0-202">Consulte a [documentação de referência da API do back-end](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend) do Gerenciamento de API para obter mais detalhes em cada campo.</span><span class="sxs-lookup"><span data-stu-id="c4be0-202">Refer to the API Management [backend API reference documentation](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#a-namebackenda-backend) for more details on each field.</span></span>

#### <a name="example"></a><span data-ttu-id="c4be0-203">Exemplo</span><span class="sxs-lookup"><span data-stu-id="c4be0-203">Example</span></span>

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

## <a name="deploy-a-service-fabric-back-end-service"></a><span data-ttu-id="c4be0-204">Implantar um serviço de back-end do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c4be0-204">Deploy a Service Fabric back-end service</span></span>

<span data-ttu-id="c4be0-205">Agora que você tem o Service Fabric configurado como um back-end para Gerenciamento de API, é possível criar políticas de back-end para suas APIs que enviam tráfego para serviços do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c4be0-205">Now that you have the Service Fabric configured as a backend to API Management, you can author backend policies for your APIs that send traffic to your Service Fabric services.</span></span> <span data-ttu-id="c4be0-206">Mas, primeiro, é necessário um serviço executando no Service Fabric para aceitar solicitações.</span><span class="sxs-lookup"><span data-stu-id="c4be0-206">But first you need a service running in Service Fabric to accept requests.</span></span>

### <a name="create-a-service-fabric-service-with-an-http-endpoint"></a><span data-ttu-id="c4be0-207">Criar um serviço do Service Fabric com um ponto de extremidade HTTP</span><span class="sxs-lookup"><span data-stu-id="c4be0-207">Create a Service Fabric service with an HTTP endpoint</span></span>

<span data-ttu-id="c4be0-208">Para este tutorial, criaremos um serviço confiável do Núcleo de ASP.NET sem estado básico utilizando o modelo de projeto de API Web padrão.</span><span class="sxs-lookup"><span data-stu-id="c4be0-208">For this tutorial, we'll create a basic stateless ASP.NET Core Reliable Service using the default Web API project template.</span></span> <span data-ttu-id="c4be0-209">Isso cria um ponto de extremidade HTTP para o seu serviço que será exposto através do Gerenciamento de API do Azure:</span><span class="sxs-lookup"><span data-stu-id="c4be0-209">This creates an HTTP endpoint for your service, which you'll expose through Azure API Management:</span></span>

```
/api/values
```

<span data-ttu-id="c4be0-210">Inicie [configurando seu ambiente de desenvolvimento para o desenvolvimento de ASP.NET Core](service-fabric-add-a-web-frontend.md#set-up-your-environment-for-aspnet-core).</span><span class="sxs-lookup"><span data-stu-id="c4be0-210">Start by [setting up your development environment for ASP.NET Core development](service-fabric-add-a-web-frontend.md#set-up-your-environment-for-aspnet-core).</span></span>

<span data-ttu-id="c4be0-211">Após configurar seu ambiente de desenvolvimento, inicie o Visual Studio como Administrador e crie um serviço ASP.NET Core:</span><span class="sxs-lookup"><span data-stu-id="c4be0-211">Once your development environment is set up, start Visual Studio as Administrator and create an ASP.NET Core service:</span></span>

 1. <span data-ttu-id="c4be0-212">No Visual Studio, selecione Arquivo -> Novo projeto.</span><span class="sxs-lookup"><span data-stu-id="c4be0-212">In Visual Studio, select File -> New Project.</span></span>
 2. <span data-ttu-id="c4be0-213">Selecione o modelo de Aplicativo do Service Fabric em Nuvem e nomeie-o **"ApiApplication"**.</span><span class="sxs-lookup"><span data-stu-id="c4be0-213">Select the Service Fabric Application template under Cloud and name it **"ApiApplication"**.</span></span>
 3. <span data-ttu-id="c4be0-214">Selecione o modelo de serviço do ASP.NET Core e nomeie o projeto **"WebApiService"**.</span><span class="sxs-lookup"><span data-stu-id="c4be0-214">Select the ASP.NET Core service template and name the project **"WebApiService"**.</span></span>
 4. <span data-ttu-id="c4be0-215">Selecione o modelo de projeto ASP.NET Core 1.1 da API Web.</span><span class="sxs-lookup"><span data-stu-id="c4be0-215">Select the Web API ASP.NET Core 1.1 project template.</span></span>
 5. <span data-ttu-id="c4be0-216">Uma vez que o projeto é criado, abra `PackageRoot\ServiceManifest.xml` e remova o atributo `Port` da configuração do recurso do ponto de extremidade:</span><span class="sxs-lookup"><span data-stu-id="c4be0-216">Once the project is created, open `PackageRoot\ServiceManifest.xml` and remove the `Port` attribute from the endpoint resource configuration:</span></span>
 
    ```xml
    <Resources>
      <Endpoints>
        <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" />
      </Endpoints>
    </Resources>
    ```

    <span data-ttu-id="c4be0-217">Isso permite que o Service Fabric especifique uma porta dinamicamente do intervalo de portas do aplicativo, que abrimos através do Grupo de Segurança de Rede no modelo do Resource Manager do cluster, permitindo que o tráfego flua para o Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="c4be0-217">This allows Service Fabric to specify a port dynamically from the application port range, which we opened through the Network Security Group in the cluster Resource Manager template, allowing traffic to flow to it from API Management.</span></span>
 
 6. <span data-ttu-id="c4be0-218">Pressione F5 no Visual Studio para verificar se a API Web está disponível localmente.</span><span class="sxs-lookup"><span data-stu-id="c4be0-218">Press F5 in Visual Studio to verify the web API is available locally.</span></span> 

    <span data-ttu-id="c4be0-219">Abra o Service Fabric Explorer e faça busca detalhada de uma instância específica do serviço ASP.NET Core para visualizar o endereço básico no qual o serviço está ouvindo.</span><span class="sxs-lookup"><span data-stu-id="c4be0-219">Open Service Fabric Explorer and drill down to a specific instance of the ASP.NET Core service to see the base address the service is listening on.</span></span> <span data-ttu-id="c4be0-220">Adicione `/api/values` ao endereço básico e abra-o em um navegador.</span><span class="sxs-lookup"><span data-stu-id="c4be0-220">Add `/api/values` to the base address and open it in a browser.</span></span> <span data-ttu-id="c4be0-221">Isso invoca o método Get no ValuesController no modelo da API Web.</span><span class="sxs-lookup"><span data-stu-id="c4be0-221">This invokes the Get method on the ValuesController in the Web API template.</span></span> <span data-ttu-id="c4be0-222">Ele retorna a resposta padrão fornecida pelo modelo, uma matriz JSON que contém duas cadeias de caracteres:</span><span class="sxs-lookup"><span data-stu-id="c4be0-222">It returns the default response that is provided by the template, a JSON array that contains two strings:</span></span>

    ```json
    ["value1", "value2"]`
    ```

    <span data-ttu-id="c4be0-223">Este é o ponto de extremidade que você irá expor através do Gerenciamento de API no Azure.</span><span class="sxs-lookup"><span data-stu-id="c4be0-223">This is the endpoint that you'll expose through API Management in Azure.</span></span>

 7. <span data-ttu-id="c4be0-224">Finalmente, implante o aplicativo em seu cluster no Azure.</span><span class="sxs-lookup"><span data-stu-id="c4be0-224">Finally, deploy the application to your cluster in Azure.</span></span> <span data-ttu-id="c4be0-225">[Utilizando o Visual Studio](service-fabric-publish-app-remote-cluster.md#to-publish-an-application-using-the-publish-service-fabric-application-dialog-box), clique com o botão direito do mouse no projeto de Aplicativo e selecione **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="c4be0-225">[Using Visual Studio](service-fabric-publish-app-remote-cluster.md#to-publish-an-application-using-the-publish-service-fabric-application-dialog-box), right-click the Application project and select **Publish**.</span></span> <span data-ttu-id="c4be0-226">Forneça o seu ponto de extremidade de cluster (por exemplo, `mycluster.westus.cloudapp.azure.com:19000`) para implantar o aplicativo em seu cluster do Service Fabric no Azure.</span><span class="sxs-lookup"><span data-stu-id="c4be0-226">Provide your cluster endpoint (for example, `mycluster.westus.cloudapp.azure.com:19000`) to deploy the application to your Service Fabric cluster in Azure.</span></span>

<span data-ttu-id="c4be0-227">Um serviço sem estado ASP.NET Core nomeado `fabric:/ApiApplication/WebApiService` agora deve estar em execução no seu cluster do Service Fabric no Azure.</span><span class="sxs-lookup"><span data-stu-id="c4be0-227">An ASP.NET Core stateless service named `fabric:/ApiApplication/WebApiService` should now be running in your Service Fabric cluster in Azure.</span></span>

## <a name="create-an-api-operation"></a><span data-ttu-id="c4be0-228">Criar uma operação de API</span><span class="sxs-lookup"><span data-stu-id="c4be0-228">Create an API operation</span></span>

<span data-ttu-id="c4be0-229">Agora, estamos prontos para criar uma operação no Gerenciamento de API que os clientes externos utilizam para se comunicar com o serviço sem estado ASP.NET Core que está executando no cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c4be0-229">Now we're ready to create an operation in API Management that external clients use to communicate with the ASP.NET Core stateless service running in the Service Fabric cluster.</span></span>

 1. <span data-ttu-id="c4be0-230">Entren no portal do Azure e navegue até a implantação do serviço de Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="c4be0-230">Log in to the Azure portal and navigate to your API Management service deployment.</span></span>
 2. <span data-ttu-id="c4be0-231">Na folha do serviço de Gerenciamento de API, selecione **APIs - Visualização**</span><span class="sxs-lookup"><span data-stu-id="c4be0-231">In the API Management service blade, select **APIs - Preview**</span></span>
 3. <span data-ttu-id="c4be0-232">Adicione uma nova API clicando na caixa **API em Branco** e preenchendo a caixa de diálogo:</span><span class="sxs-lookup"><span data-stu-id="c4be0-232">Add a new API by clicking the **Blank API** box and filling out the dialog box:</span></span>

     - <span data-ttu-id="c4be0-233">**URL do serviço Web**: para back-ends do Service Fabric esse valor de URL não é utilizado.</span><span class="sxs-lookup"><span data-stu-id="c4be0-233">**Web service URL**: For Service Fabric backends, this URL value is not used.</span></span> <span data-ttu-id="c4be0-234">Aqui, você pode colocar qualquer valor.</span><span class="sxs-lookup"><span data-stu-id="c4be0-234">You can put any value here.</span></span> <span data-ttu-id="c4be0-235">Neste tutorial, utilize: `http://servicefabric`.</span><span class="sxs-lookup"><span data-stu-id="c4be0-235">For this tutorial, use: `http://servicefabric`.</span></span>
     - <span data-ttu-id="c4be0-236">**Nome**: forneça qualquer nome para sua API.</span><span class="sxs-lookup"><span data-stu-id="c4be0-236">**Name**: Provide any name for your API.</span></span> <span data-ttu-id="c4be0-237">Neste tutorial, utilize `Service Fabric App`.</span><span class="sxs-lookup"><span data-stu-id="c4be0-237">For this tutorial, use `Service Fabric App`.</span></span>
     - <span data-ttu-id="c4be0-238">**Esquema de URL**: selecione HTTP, HTTPS ou ambos.</span><span class="sxs-lookup"><span data-stu-id="c4be0-238">**URL scheme**: Select either HTTP, HTTPS, or both.</span></span> <span data-ttu-id="c4be0-239">Neste tutorial, utilize `both`.</span><span class="sxs-lookup"><span data-stu-id="c4be0-239">For this tutorial, use `both`.</span></span>
     - <span data-ttu-id="c4be0-240">**Sufixo de URL da API**: forneça um sufixo para a API.</span><span class="sxs-lookup"><span data-stu-id="c4be0-240">**API URL Suffix**: Provide a suffix for our API.</span></span> <span data-ttu-id="c4be0-241">Neste tutorial, utilize `myapp`.</span><span class="sxs-lookup"><span data-stu-id="c4be0-241">For this tutorial, use `myapp`.</span></span>
 
 4. <span data-ttu-id="c4be0-242">Uma vez que a API é criada, clique em **+ Adicionar operação** para adicionar uma operação de API de front-end.</span><span class="sxs-lookup"><span data-stu-id="c4be0-242">Once the API is created, click **+ Add operation** to add a front-end API operation.</span></span> <span data-ttu-id="c4be0-243">Preencha os valores:</span><span class="sxs-lookup"><span data-stu-id="c4be0-243">Fill out the values:</span></span>
    
     - <span data-ttu-id="c4be0-244">**URL**: selecione `GET` forneça um caminho URL para a API.</span><span class="sxs-lookup"><span data-stu-id="c4be0-244">**URL**: Select `GET` and provide a URL path for the API.</span></span> <span data-ttu-id="c4be0-245">Neste tutorial, utilize `/api/values`.</span><span class="sxs-lookup"><span data-stu-id="c4be0-245">For this tutorial, use `/api/values`.</span></span>
     
       <span data-ttu-id="c4be0-246">Por padrão, o caminho URL especificado aqui é o caminho URL enviado ao serviço do Service Fabric de back-end.</span><span class="sxs-lookup"><span data-stu-id="c4be0-246">By default, the URL path specified here is the URL path sent to the backend Service Fabric service.</span></span> <span data-ttu-id="c4be0-247">Se você utiliza o mesmo caminho URL que aquele do serviço, nesse caso `/api/values`, a operação funciona sem modificações adicionais.</span><span class="sxs-lookup"><span data-stu-id="c4be0-247">If you use the same URL path here that your service uses, in this case `/api/values`, then the operation works without further modification.</span></span> <span data-ttu-id="c4be0-248">Além disso, é possível especificar um caminho URL que seja diferente do caminho URL utilizado pelo serviço do Service Fabric de beck-end, caso em que também será necessário especificar posteriormente uma reescrita do caminho na sua política de operação.</span><span class="sxs-lookup"><span data-stu-id="c4be0-248">You may also specify a URL path here that is different from the URL path used by your backend Service Fabric service, in which case you will also need to specify a path rewrite in your operation policy later.</span></span>
     - <span data-ttu-id="c4be0-249">**Nome de exibição**: forneça um nome para a API.</span><span class="sxs-lookup"><span data-stu-id="c4be0-249">**Display name**: Provide any name for the API.</span></span> <span data-ttu-id="c4be0-250">Neste tutorial, utilize `Values`.</span><span class="sxs-lookup"><span data-stu-id="c4be0-250">For this tutorial, use `Values`.</span></span>

## <a name="configure-a-backend-policy"></a><span data-ttu-id="c4be0-251">Configure uma política de back-end</span><span class="sxs-lookup"><span data-stu-id="c4be0-251">Configure a backend policy</span></span>

<span data-ttu-id="c4be0-252">A política de back-end vincula tudo em conjunto.</span><span class="sxs-lookup"><span data-stu-id="c4be0-252">The backend policy ties everything together.</span></span> <span data-ttu-id="c4be0-253">Dessa forma, o serviço do Service Fabric de back-end é configurado de acordo com as solicitações roteadas.</span><span class="sxs-lookup"><span data-stu-id="c4be0-253">This is where you configure the backend Service Fabric service to which requests are routed.</span></span> <span data-ttu-id="c4be0-254">É possível aplicar essa política a qualquer operação de API.</span><span class="sxs-lookup"><span data-stu-id="c4be0-254">You can apply this policy to any API operation.</span></span> <span data-ttu-id="c4be0-255">A [configuração de back-end para o Service Fabric](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService) fornece os seguintes controles de roteamento de solicitação:</span><span class="sxs-lookup"><span data-stu-id="c4be0-255">The [backend configuration for Service Fabric](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService) provides the following request routing controls:</span></span> 
 - <span data-ttu-id="c4be0-256">Seleção de instância de serviço, especificando um nome de instância de serviço do Service Fabric, codificado (por exemplo, `"fabric:/myapp/myservice"`) ou gerado a partir da solicitação HTTP (por exemplo, `"fabric:/myapp/users/" + context.Request.MatchedParameters["name"]`).</span><span class="sxs-lookup"><span data-stu-id="c4be0-256">Service instance selection by specifying a Service Fabric service instance name, either hardcoded (for example, `"fabric:/myapp/myservice"`) or generated from the HTTP request (for example, `"fabric:/myapp/users/" + context.Request.MatchedParameters["name"]`).</span></span>
 - <span data-ttu-id="c4be0-257">Resolução de partição gerando uma chave de partição utilizando qualquer esquema de particionamento do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c4be0-257">Partition resolution by generating a partition key using any Service Fabric partitioning scheme.</span></span>
 - <span data-ttu-id="c4be0-258">Seleção de réplica para serviços com estado.</span><span class="sxs-lookup"><span data-stu-id="c4be0-258">Replica selection for stateful services.</span></span>
 - <span data-ttu-id="c4be0-259">Condições de repetição de resolução que permitem especificar as condições para resolver novamente um local de serviço e reenviar uma solicitação.</span><span class="sxs-lookup"><span data-stu-id="c4be0-259">Resolution retry conditions that allow you to specify the conditions for re-resolving a service location and resending a request.</span></span>

<span data-ttu-id="c4be0-260">Para este tutorial, crie uma política de back-end que roteie as solicitações diretamente para o serviço sem estado no ASP.NET Core implantado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="c4be0-260">For this tutorial, create a backend policy that routes requests directly to the ASP.NET Core stateless service deployed earlier:</span></span>

 1. <span data-ttu-id="c4be0-261">Selecione e edite as **políticas de entrada** para a `Values` operação clicando no ícone de edição e, em seguida, selecionando **Modo de Exibição de Código**.</span><span class="sxs-lookup"><span data-stu-id="c4be0-261">Select and edit the **inbound policies** for the `Values` operation by clicking the edit icon, and then selecting **Code View**.</span></span>
 2. <span data-ttu-id="c4be0-262">No editor de código de política, adicione uma política `set-backend-service` em políticas de entrada, conforme mostrado e clique no botão **Salvar** :</span><span class="sxs-lookup"><span data-stu-id="c4be0-262">In the policy code editor, add a `set-backend-service` policy under inbound policies as shown here and click the **Save** button:</span></span>
    
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

<span data-ttu-id="c4be0-263">Para obter um conjunto completo de atributos de política de back-end do Service Fabric, consulte a [documentação de back-end do Gerenciamento de API](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService)</span><span class="sxs-lookup"><span data-stu-id="c4be0-263">For a full set of Service Fabric back-end policy attributes, refer to the [API Management back-end documentation](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies#SetBackendService)</span></span>

### <a name="add-the-api-to-a-product"></a><span data-ttu-id="c4be0-264">Adicione a API a um produto.</span><span class="sxs-lookup"><span data-stu-id="c4be0-264">Add the API to a product.</span></span> 

<span data-ttu-id="c4be0-265">Antes de poder chamar a API, ela deve ser adicionada a um produto onde você pode conceder acesso a usuários.</span><span class="sxs-lookup"><span data-stu-id="c4be0-265">Before you can call the API, it must be added to a product where you can grant access to users.</span></span> 

 1. <span data-ttu-id="c4be0-266">No serviço de gerenciamento de API, selecione **Produtos - VISUALIZAÇÃO**.</span><span class="sxs-lookup"><span data-stu-id="c4be0-266">In the API Management service, select **Products - PREVIEW**.</span></span>
 2. <span data-ttu-id="c4be0-267">Por padrão, o Gerenciamento de API oferece dois produtos: Starter e Ilimitado.</span><span class="sxs-lookup"><span data-stu-id="c4be0-267">By default, API Management providers two products: Starter and Unlimited.</span></span> <span data-ttu-id="c4be0-268">Selecione o produto Ilimitado.</span><span class="sxs-lookup"><span data-stu-id="c4be0-268">Select the Unlimited product.</span></span>
 3. <span data-ttu-id="c4be0-269">Selecione APIs.</span><span class="sxs-lookup"><span data-stu-id="c4be0-269">Select APIs.</span></span>
 4. <span data-ttu-id="c4be0-270">Clique no botão **+ Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c4be0-270">Click the **+ Add** button.</span></span>
 5. <span data-ttu-id="c4be0-271">Selecione a `Service Fabric App` API criada nas etapas anteriores e clique no botão **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="c4be0-271">Select the `Service Fabric App` API you created in the previous steps and click the **Select** button.</span></span>

### <a name="test-it"></a><span data-ttu-id="c4be0-272">Testá-lo</span><span class="sxs-lookup"><span data-stu-id="c4be0-272">Test it</span></span>

<span data-ttu-id="c4be0-273">Agora é possível tentar enviar uma solicitação para seu serviço de back-end no Service Fabric através do Gerenciamento de API diretamente do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4be0-273">You can now try sending a request to your back-end service in Service Fabric through API Management directly from the Azure portal.</span></span>

 1. <span data-ttu-id="c4be0-274">No serviço de Gerenciamento de API, selecione **API - VISUALIZAÇÃO**.</span><span class="sxs-lookup"><span data-stu-id="c4be0-274">In the API Management service, select **API - PREVIEW**.</span></span>
 2. <span data-ttu-id="c4be0-275">Na `Service Fabric App` API criada nas etapas anteriores, selecione a guia **Teste**.</span><span class="sxs-lookup"><span data-stu-id="c4be0-275">In the `Service Fabric App` API you created in the previous steps, select the **Test** tab.</span></span>
 3. <span data-ttu-id="c4be0-276">Clique no botão **Enviar** para enviar uma solicitação de teste para o serviço de back-end.</span><span class="sxs-lookup"><span data-stu-id="c4be0-276">Click the **Send** button to send a test request to the backend service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4be0-277">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c4be0-277">Next steps</span></span>

<span data-ttu-id="c4be0-278">Neste ponto, é possível ter uma configuração básica com o Service Fabric e o Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="c4be0-278">At this point, you should have a basic setup with Service Fabric and API Management.</span></span>

<span data-ttu-id="c4be0-279">Este tutorial utiliza a autenticação de usuário básica baseada em certificado para o cluster do Service Fabric para ajudá-lo a configurar rapidamente.</span><span class="sxs-lookup"><span data-stu-id="c4be0-279">This tutorial uses basic certificate-based user authentication for your Service Fabric cluster to get you set up quickly.</span></span> <span data-ttu-id="c4be0-280">A autenticação de usuário mais avançada para o cluster do Service Fabric é preferível com a [autenticação Azure Active Directory](service-fabric-cluster-creation-via-arm.md#set-up-azure-active-directory-for-client-authentication).</span><span class="sxs-lookup"><span data-stu-id="c4be0-280">More advanced user authentication for your Service Fabric cluster is preferable with [Azure Active Directory authentication](service-fabric-cluster-creation-via-arm.md#set-up-azure-active-directory-for-client-authentication).</span></span> 

<span data-ttu-id="c4be0-281">Em seguida, [crie e defina as configurações avançadas do produto no Gerenciamento de API do Azure](https://docs.microsoft.com/azure/api-management/api-management-howto-product-with-rules) de modo a preparar seu aplicativo para o tráfego do mundo real.</span><span class="sxs-lookup"><span data-stu-id="c4be0-281">Next, [create and configure advanced product settings in Azure API Management](https://docs.microsoft.com/azure/api-management/api-management-howto-product-with-rules) to prepare your application for real world traffic.</span></span>

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
