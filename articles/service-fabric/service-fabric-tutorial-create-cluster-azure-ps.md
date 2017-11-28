---
title: "aaaCreate uma malha do serviço de cluster no Azure | Microsoft Docs"
description: Saiba como toocreate um Windows ou Linux Service Fabric do cluster no Azure usando o PowerShell.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/13/2017
ms.author: ryanwi
ms.openlocfilehash: e697e2a2e99f67cb02422efdb368c664c9fd5a97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-secure-cluster-on-azure-using-powershell"></a><span data-ttu-id="b2358-103">Criar um cluster seguro no Azure usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="b2358-103">Create a secure cluster on Azure using PowerShell</span></span>
<span data-ttu-id="b2358-104">Este tutorial mostra como toocreate uma malha do serviço de cluster (Windows ou Linux) em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="b2358-104">This tutorial shows you how toocreate a Service Fabric cluster (Windows or Linux) running in Azure.</span></span> <span data-ttu-id="b2358-105">Quando você terminar, você tem um cluster em execução na nuvem Olá que você pode implantar aplicativos.</span><span class="sxs-lookup"><span data-stu-id="b2358-105">When you're finished, you have a cluster running in hello cloud that you can deploy applications to.</span></span>

<span data-ttu-id="b2358-106">Neste tutorial, você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="b2358-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b2358-107">Criar um cluster do Service Fabric seguro no Azure usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="b2358-107">Create a secure Service Fabric cluster in Azure using PowerShell</span></span>
> * <span data-ttu-id="b2358-108">Cluster Olá seguro com um certificado x. 509</span><span class="sxs-lookup"><span data-stu-id="b2358-108">Secure hello cluster with an X.509 certificate</span></span>
> * <span data-ttu-id="b2358-109">Conecte-se o cluster toohello usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="b2358-109">Connect toohello cluster using PowerShell</span></span>
> * <span data-ttu-id="b2358-110">Remover um cluster</span><span class="sxs-lookup"><span data-stu-id="b2358-110">Remove a cluster</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b2358-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b2358-111">Prerequisites</span></span>
<span data-ttu-id="b2358-112">Antes de começar este tutorial:</span><span class="sxs-lookup"><span data-stu-id="b2358-112">Before you begin this tutorial:</span></span>
- <span data-ttu-id="b2358-113">Se você não tem uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span><span class="sxs-lookup"><span data-stu-id="b2358-113">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="b2358-114">Instalar Olá [módulo SDK do Service Fabric e do PowerShell](service-fabric-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="b2358-114">Install hello [Service Fabric SDK and PowerShell module](service-fabric-get-started.md)</span></span>
- <span data-ttu-id="b2358-115">Instalar Olá [Azure Powershell versão 4.1 ou superior do módulo](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)</span><span class="sxs-lookup"><span data-stu-id="b2358-115">Install hello [Azure Powershell module version 4.1 or higher](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)</span></span>

<span data-ttu-id="b2358-116">Olá procedimento a seguir cria uma visualização (única máquina virtual) de nó único cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b2358-116">hello following procedure creates a single-node (single virtual machine) preview Service Fabric cluster.</span></span> <span data-ttu-id="b2358-117">cluster de saudação é protegida por um certificado autoassinado que obtém criado juntamente com cluster hello e, em seguida, é colocado em um cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="b2358-117">hello cluster is secured by a self-signed certificate that gets created along with hello cluster and then placed in a key vault.</span></span> <span data-ttu-id="b2358-118">Clusters de nó único não podem ser escaladas além de uma máquina virtual e clusters de visualização não podem ser atualizado toonewer versões.</span><span class="sxs-lookup"><span data-stu-id="b2358-118">Single-node clusters cannot be scaled beyond one virtual machine and preview clusters cannot be upgraded toonewer versions.</span></span>

<span data-ttu-id="b2358-119">custo toocalculate executando em um cluster do Service Fabric no uso do Azure Olá [Calculadora de preços do Azure](https://azure.microsoft.com/pricing/calculator/).</span><span class="sxs-lookup"><span data-stu-id="b2358-119">toocalculate cost incurred by running a Service Fabric cluster in Azure use hello [Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/).</span></span>
<span data-ttu-id="b2358-120">Para obter mais informações sobre a criação de clusters do Service Fabric, confira [Criar um cluster do Service Fabric usando o Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="b2358-120">For more information on creating Service Fabric clusters, see [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span>

## <a name="create-hello-cluster-using-azure-powershell"></a><span data-ttu-id="b2358-121">Criar cluster hello usando o PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="b2358-121">Create hello cluster using Azure PowerShell</span></span>
1. <span data-ttu-id="b2358-122">Baixar uma cópia local do modelo do Azure Resource Manager hello e arquivo de parâmetro de saudação do hello [modelo do Gerenciador de recursos do Azure para Service Fabric](https://aka.ms/securepreviewonelineclustertemplate) repositório GitHub.</span><span class="sxs-lookup"><span data-stu-id="b2358-122">Download a local copy of hello Azure Resource Manager template and hello parameter file from hello [Azure Resource Manager template for Service Fabric](https://aka.ms/securepreviewonelineclustertemplate) GitHub repository.</span></span>  <span data-ttu-id="b2358-123">*azuredeploy.JSON* é hello Azure Resource Manager modelo que define um cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b2358-123">*azuredeploy.json* is hello Azure Resource Manager template that defines a Service Fabric cluster.</span></span> <span data-ttu-id="b2358-124">*azuredeploy.Parameters.JSON* é um arquivo de parâmetros para a implantação de cluster toocustomize hello.</span><span class="sxs-lookup"><span data-stu-id="b2358-124">*azuredeploy.parameters.json* is a parameters file for you toocustomize hello cluster deployment.</span></span>

2. <span data-ttu-id="b2358-125">Personalizar Olá Olá parâmetros a seguir *azuredeploy.parameters.json* arquivo de parâmetros:</span><span class="sxs-lookup"><span data-stu-id="b2358-125">Customize hello following parameters in hello *azuredeploy.parameters.json* parameters file:</span></span>

   | <span data-ttu-id="b2358-126">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="b2358-126">Parameter</span></span>       | <span data-ttu-id="b2358-127">Descrição</span><span class="sxs-lookup"><span data-stu-id="b2358-127">Description</span></span> | <span data-ttu-id="b2358-128">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="b2358-128">Suggested Value</span></span> |
   | --------------- | ----------- | --------------- |
   | <span data-ttu-id="b2358-129">clusterLocation</span><span class="sxs-lookup"><span data-stu-id="b2358-129">clusterLocation</span></span> | <span data-ttu-id="b2358-130">cluster do Hello região do Azure toowhich toodeploy hello.</span><span class="sxs-lookup"><span data-stu-id="b2358-130">hello Azure region toowhich toodeploy hello cluster.</span></span> | <span data-ttu-id="b2358-131">*Por exemplo, westeurope, eastasia, eastus*</span><span class="sxs-lookup"><span data-stu-id="b2358-131">*for example, westeurope, eastasia, eastus*</span></span> |
   | <span data-ttu-id="b2358-132">clusterName</span><span class="sxs-lookup"><span data-stu-id="b2358-132">clusterName</span></span>     | <span data-ttu-id="b2358-133">Nome do cluster Olá deseja toocreate.</span><span class="sxs-lookup"><span data-stu-id="b2358-133">Name of hello cluster you want toocreate.</span></span> | <span data-ttu-id="b2358-134">*Por exemplo, bobs-sfpreviewcluster*</span><span class="sxs-lookup"><span data-stu-id="b2358-134">*for example, bobs-sfpreviewcluster*</span></span> |
   | <span data-ttu-id="b2358-135">adminUserName</span><span class="sxs-lookup"><span data-stu-id="b2358-135">adminUserName</span></span>   | <span data-ttu-id="b2358-136">conta de administrador local Olá em Olá cluster das máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="b2358-136">hello local admin account on hello cluster virtual machines.</span></span> | <span data-ttu-id="b2358-137">*Qualquer nome de usuário válido do Windows Server*</span><span class="sxs-lookup"><span data-stu-id="b2358-137">*Any valid Windows Server username*</span></span> |
   | <span data-ttu-id="b2358-138">adminPassword</span><span class="sxs-lookup"><span data-stu-id="b2358-138">adminPassword</span></span>   | <span data-ttu-id="b2358-139">Senha da conta de administrador local Olá em Olá cluster das máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="b2358-139">Password of hello local admin account on hello cluster virtual machines.</span></span> | <span data-ttu-id="b2358-140">*Qualquer senha válida do Windows Server*</span><span class="sxs-lookup"><span data-stu-id="b2358-140">*Any valid Windows Server password*</span></span> |
   | <span data-ttu-id="b2358-141">clusterCodeVersion</span><span class="sxs-lookup"><span data-stu-id="b2358-141">clusterCodeVersion</span></span> | <span data-ttu-id="b2358-142">Olá toorun de versão do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b2358-142">hello Service Fabric version toorun.</span></span> <span data-ttu-id="b2358-143">(255.255.X.255 são versões de visualização).</span><span class="sxs-lookup"><span data-stu-id="b2358-143">(255.255.X.255 are preview versions).</span></span> | <span data-ttu-id="b2358-144">**255.255.5718.255**</span><span class="sxs-lookup"><span data-stu-id="b2358-144">**255.255.5718.255**</span></span> |
   | <span data-ttu-id="b2358-145">vmInstanceCount</span><span class="sxs-lookup"><span data-stu-id="b2358-145">vmInstanceCount</span></span> | <span data-ttu-id="b2358-146">número de saudação de máquinas virtuais no cluster (pode ser 1 ou 3-99).</span><span class="sxs-lookup"><span data-stu-id="b2358-146">hello number of virtual machines in your cluster (can be 1 or 3-99).</span></span> | <span data-ttu-id="b2358-147">**1**</span><span class="sxs-lookup"><span data-stu-id="b2358-147">**1**</span></span> | <span data-ttu-id="b2358-148">*Para um cluster de visualização, especifique apenas uma máquina virtual*</span><span class="sxs-lookup"><span data-stu-id="b2358-148">*For a preview cluster specify only one virtual machine*</span></span> |

3. <span data-ttu-id="b2358-149">Abra um console do PowerShell, tooAzure de logon e selecione assinatura Olá desejada toodeploy Olá cluster em:</span><span class="sxs-lookup"><span data-stu-id="b2358-149">Open a PowerShell console, login tooAzure, and select hello subscription you want toodeploy hello cluster in:</span></span>

   ```powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription -SubscriptionId <subscription-id>
   ```
4. <span data-ttu-id="b2358-150">Criar e criptografar uma senha para Olá toobe de certificado usado pelo serviço de malha.</span><span class="sxs-lookup"><span data-stu-id="b2358-150">Create and encrypt a password for hello certificate toobe used by Service Fabric.</span></span>

   ```powershell
   $pwd = "<your password>" | ConvertTo-SecureString -AsPlainText -Force
   ```
5. <span data-ttu-id="b2358-151">Crie cluster hello e seu certificado executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="b2358-151">Create hello cluster and its certificate by running hello following command:</span></span>

   ```powershell
      New-AzureRmServiceFabricCluster
          -TemplateFile C:\Users\me\Desktop\azuredeploy.json `
          -ParameterFile C:\Users\me\Desktop\azuredeploy.parameters.json `
          -CertificateOutputFolder C:\Users\me\Desktop\ `
          -CertificatePassword $pwd `
          -CertificateSubjectName "mycluster.westeurope.cloudapp.azure.com" `
          -ResourceGroupName myclusterRG
   ```

   >[!NOTE]
   ><span data-ttu-id="b2358-152">Olá `-CertificateSubjectName` parâmetro deve ser alinhadas com o parâmetro hello clusterName especificado no arquivo de parâmetros de hello, bem como Olá domínio vinculado toohello região do Azure você escolher, como: `clustername.eastus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="b2358-152">hello `-CertificateSubjectName` parameter should align with hello clusterName parameter specified in hello parameters file, as well as hello domain tied toohello Azure region you chose, such as: `clustername.eastus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="b2358-153">Quando termina a configuração hello, ele produz informações sobre cluster Olá criado no Azure.</span><span class="sxs-lookup"><span data-stu-id="b2358-153">Once hello configuration finishes, it outputs information about hello cluster created in Azure.</span></span> <span data-ttu-id="b2358-154">Ele também copia Olá cluster certificado toohello - CertificateOutputFolder directory no caminho de saudação especificado para esse parâmetro.</span><span class="sxs-lookup"><span data-stu-id="b2358-154">It also copies hello cluster certificate toohello -CertificateOutputFolder directory on hello path you specified for this parameter.</span></span> <span data-ttu-id="b2358-155">É necessário tooaccess esse certificado Service Fabric Explorer e exibir a integridade de saudação do cluster.</span><span class="sxs-lookup"><span data-stu-id="b2358-155">You need this certificate tooaccess Service Fabric Explorer and view hello health of your cluster.</span></span>

<span data-ttu-id="b2358-156">Anote a URL Olá para o cluster, o que pode ser semelhante toohello URL a seguir: *https://mycluster.westeurope.cloudapp.azure.com:19080*</span><span class="sxs-lookup"><span data-stu-id="b2358-156">Take note of hello URL for your cluster, which may be similar toohello following URL: *https://mycluster.westeurope.cloudapp.azure.com:19080*</span></span>

## <a name="modify-hello-certificate--access-service-fabric-explorer"></a><span data-ttu-id="b2358-157">& Modificar certificado Olá acessar Gerenciador do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b2358-157">Modify hello certificate & access Service Fabric Explorer</span></span> ##

1. <span data-ttu-id="b2358-158">Clique duas vezes em Olá tooopen de certificado Olá Assistente de importação de certificado.</span><span class="sxs-lookup"><span data-stu-id="b2358-158">Double-click hello certificate tooopen hello Certificate Import Wizard.</span></span>

2. <span data-ttu-id="b2358-159">Usar as configurações padrão, mas verifique se Olá de toocheck **marcar esta chave como exportável.**</span><span class="sxs-lookup"><span data-stu-id="b2358-159">Use default settings, but make sure toocheck hello **Mark this key as exportable.**</span></span> <span data-ttu-id="b2358-160">caixa de seleção, Olá **proteção de chave privada** etapa.</span><span class="sxs-lookup"><span data-stu-id="b2358-160">check box, in hello **private key protection** step.</span></span> <span data-ttu-id="b2358-161">O Visual Studio precisa certificado de saudação tooexport ao configurar a autenticação de Cluster de malha do registro de contêiner do Azure tooService posteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="b2358-161">Visual Studio needs tooexport hello certificate when configuring Azure Container Registry tooService Fabric Cluster authentication later in this tutorial.</span></span>

3. <span data-ttu-id="b2358-162">Agora você pode abrir o Service Fabric Explorer em um navegador.</span><span class="sxs-lookup"><span data-stu-id="b2358-162">You can now open Service Fabric Explorer in a browser.</span></span> <span data-ttu-id="b2358-163">toodo assim, navegar toohello **ManagementEndpoint** URL para o cluster usando um navegador da web e um certificado de saudação select que foi salvo no seu computador.</span><span class="sxs-lookup"><span data-stu-id="b2358-163">toodo so, navigate toohello **ManagementEndpoint** URL for your cluster using a web browser, and select hello certificate that was saved on your machine.</span></span>

>[!NOTE]
><span data-ttu-id="b2358-164">Ao abrir o Service Fabric Explorer, você verá um erro de certificado, pois está usando um certificado autoassinado.</span><span class="sxs-lookup"><span data-stu-id="b2358-164">When opening Service Fabric Explorer, you see a certificate error, as you are using a self-signed certificate.</span></span> <span data-ttu-id="b2358-165">Na borda, você tem tooclick *detalhes* e, em seguida, Olá *ir na página da Web de toohello* link.</span><span class="sxs-lookup"><span data-stu-id="b2358-165">In Edge, you have tooclick *Details* and then hello *Go on toohello webpage* link.</span></span> <span data-ttu-id="b2358-166">No Chrome, você tem tooclick *avançado* e, em seguida, Olá *continuar* link.</span><span class="sxs-lookup"><span data-stu-id="b2358-166">In Chrome, you have tooclick *Advanced* and then hello *proceed* link.</span></span>

>[!NOTE]
><span data-ttu-id="b2358-167">Se a criação do cluster Olá falhar, sempre pode ser executada comando hello, que atualiza os recursos de saudação já implantados.</span><span class="sxs-lookup"><span data-stu-id="b2358-167">If hello cluster creation fails, you can always rerun hello command, which updates hello resources already deployed.</span></span> <span data-ttu-id="b2358-168">Se um certificado foi criado como parte da implantação de saudação falhada, um novo será gerado.</span><span class="sxs-lookup"><span data-stu-id="b2358-168">If a certificate was created as part of hello failed deployment, a new one is generated.</span></span> <span data-ttu-id="b2358-169">tootroubleshoot criação do cluster, consulte [criar um cluster do Service Fabric usando o Gerenciador de recursos do Azure](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="b2358-169">tootroubleshoot cluster creation, see [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span>

## <a name="connect-toohello-secure-cluster"></a><span data-ttu-id="b2358-170">Conecte-se o cluster seguro toohello</span><span class="sxs-lookup"><span data-stu-id="b2358-170">Connect toohello secure cluster</span></span>
<span data-ttu-id="b2358-171">Conecte o cluster toohello usando Olá Service Fabric PowerShell module instalada com hello SDK do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b2358-171">Connect toohello cluster using hello Service Fabric PowerShell module installed with hello Service Fabric SDK.</span></span>  <span data-ttu-id="b2358-172">Primeiro, instale o certificado de saudação no repositório de pessoal (Meu) de saudação do usuário atual de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="b2358-172">First, install hello certificate into hello Personal (My) store of hello current user on your computer.</span></span>  <span data-ttu-id="b2358-173">Execute Olá comando PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="b2358-173">Run hello following PowerShell command:</span></span>

```powershell
$certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\mysfcluster20170531104310.pfx `
        -Password $certpwd
```

<span data-ttu-id="b2358-174">Agora você está pronto tooconnect tooyour segura cluster.</span><span class="sxs-lookup"><span data-stu-id="b2358-174">You are now ready tooconnect tooyour secure cluster.</span></span>

<span data-ttu-id="b2358-175">Olá **Service Fabric** módulo do PowerShell fornece vários cmdlets para gerenciar clusters, aplicativos e serviços do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b2358-175">hello **Service Fabric** PowerShell module provides many cmdlets for managing Service Fabric clusters, applications, and services.</span></span>  <span data-ttu-id="b2358-176">Saudação de uso [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster) tooconnect de cmdlet toohello cluster seguro.</span><span class="sxs-lookup"><span data-stu-id="b2358-176">Use hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet tooconnect toohello secure cluster.</span></span> <span data-ttu-id="b2358-177">Olá a impressão digital do certificado e detalhes de ponto de extremidade de conexão são encontrados na saída de saudação de uma etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="b2358-177">hello certificate thumbprint and connection endpoint details are found in hello output from a previous step.</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mysfcluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="b2358-178">Verifique se você está conectado e cluster hello está íntegro usando Olá [ServiceFabricClusterHealth Get](/powershell/module/servicefabric/get-servicefabricclusterhealth) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b2358-178">Check that you are connected and hello cluster is healthy using hello [Get-ServiceFabricClusterHealth](/powershell/module/servicefabric/get-servicefabricclusterhealth) cmdlet.</span></span>

```powershell
Get-ServiceFabricClusterHealth
```

## <a name="clean-up-resources"></a><span data-ttu-id="b2358-179">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="b2358-179">Clean up resources</span></span>

<span data-ttu-id="b2358-180">Um cluster é composto por outros recursos do Azure além de recurso de cluster toohello propriamente dito.</span><span class="sxs-lookup"><span data-stu-id="b2358-180">A cluster is made up of other Azure resources in addition toohello cluster resource itself.</span></span> <span data-ttu-id="b2358-181">cluster do Hello mais simples maneira toodelete hello e todos os recursos de saudação consome é o grupo de recursos de saudação do toodelete.</span><span class="sxs-lookup"><span data-stu-id="b2358-181">hello simplest way toodelete hello cluster and all hello resources it consumes is toodelete hello resource group.</span></span>

<span data-ttu-id="b2358-182">Faça logon no tooAzure e selecione Olá ID da assinatura com a qual você deseja que o cluster de saudação tooremove.</span><span class="sxs-lookup"><span data-stu-id="b2358-182">Log in tooAzure and select hello subscription ID with which you want tooremove hello cluster.</span></span>  <span data-ttu-id="b2358-183">Você pode encontrar sua ID de assinatura fazendo logon em toohello [portal do Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b2358-183">You can find your subscription ID by logging in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="b2358-184">Excluir grupo de recursos de saudação e todos os recursos de cluster de saudação usando Olá [cmdlet Remove-AzureRMResourceGroup](/en-us/powershell/module/azurerm.resources/remove-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="b2358-184">Delete hello resource group and all hello cluster resources using hello [Remove-AzureRMResourceGroup cmdlet](/en-us/powershell/module/azurerm.resources/remove-azurermresourcegroup).</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId "Subcription ID"

$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="next-steps"></a><span data-ttu-id="b2358-185">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b2358-185">Next steps</span></span>
<span data-ttu-id="b2358-186">Neste tutorial, você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="b2358-186">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b2358-187">Criar um cluster do Service Fabric no Azure</span><span class="sxs-lookup"><span data-stu-id="b2358-187">Create a Service Fabric cluster in Azure</span></span>
> * <span data-ttu-id="b2358-188">Cluster Olá seguro com um certificado x. 509</span><span class="sxs-lookup"><span data-stu-id="b2358-188">Secure hello cluster with an X.509 certificate</span></span>
> * <span data-ttu-id="b2358-189">Conecte-se o cluster toohello usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="b2358-189">Connect toohello cluster using PowerShell</span></span>
> * <span data-ttu-id="b2358-190">Remover um cluster</span><span class="sxs-lookup"><span data-stu-id="b2358-190">Remove a cluster</span></span>

<span data-ttu-id="b2358-191">Em seguida, Avançar toohello toolearn tutorial a seguir como toodeploy um aplicativo existente.</span><span class="sxs-lookup"><span data-stu-id="b2358-191">Next, advance toohello following tutorial toolearn how toodeploy an existing application.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="b2358-192">Implantar um aplicativo existente do .NET com o Docker Compose</span><span class="sxs-lookup"><span data-stu-id="b2358-192">Deploy an existing .NET application with Docker Compose</span></span>](service-fabric-host-app-in-a-container.md)
