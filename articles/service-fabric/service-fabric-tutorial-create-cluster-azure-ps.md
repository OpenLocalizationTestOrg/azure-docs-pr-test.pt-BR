---
title: Criar um cluster do Service Fabric no Azure | Microsoft Docs
description: Saiba como criar um cluster do Windows ou Linux do Service Fabric no Azure usando o PowerShell.
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
ms.openlocfilehash: f62249417552b9cf840bfac3b94c27f63bd7064e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-secure-cluster-on-azure-using-powershell"></a><span data-ttu-id="a3886-103">Criar um cluster seguro no Azure usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="a3886-103">Create a secure cluster on Azure using PowerShell</span></span>
<span data-ttu-id="a3886-104">Este tutorial mostra como criar um cluster do Service Fabric (do Windows ou Linux) em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="a3886-104">This tutorial shows you how to create a Service Fabric cluster (Windows or Linux) running in Azure.</span></span> <span data-ttu-id="a3886-105">Ao terminar, você terá um cluster em execução na nuvem no qual você poderá implantar aplicativos.</span><span class="sxs-lookup"><span data-stu-id="a3886-105">When you're finished, you have a cluster running in the cloud that you can deploy applications to.</span></span>

<span data-ttu-id="a3886-106">Neste tutorial, você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="a3886-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a3886-107">Criar um cluster do Service Fabric seguro no Azure usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="a3886-107">Create a secure Service Fabric cluster in Azure using PowerShell</span></span>
> * <span data-ttu-id="a3886-108">Proteger o cluster com um certificado X.509</span><span class="sxs-lookup"><span data-stu-id="a3886-108">Secure the cluster with an X.509 certificate</span></span>
> * <span data-ttu-id="a3886-109">Conectar o cluster usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="a3886-109">Connect to the cluster using PowerShell</span></span>
> * <span data-ttu-id="a3886-110">Remover um cluster</span><span class="sxs-lookup"><span data-stu-id="a3886-110">Remove a cluster</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a3886-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a3886-111">Prerequisites</span></span>
<span data-ttu-id="a3886-112">Antes de começar este tutorial:</span><span class="sxs-lookup"><span data-stu-id="a3886-112">Before you begin this tutorial:</span></span>
- <span data-ttu-id="a3886-113">Se você não tem uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span><span class="sxs-lookup"><span data-stu-id="a3886-113">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="a3886-114">Instale o [SDK do Service Fabric e o módulo do PowerShell](service-fabric-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="a3886-114">Install the [Service Fabric SDK and PowerShell module](service-fabric-get-started.md)</span></span>
- <span data-ttu-id="a3886-115">Instale o [módulo do Azure PowerShell versão 4.1 ou superior](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)</span><span class="sxs-lookup"><span data-stu-id="a3886-115">Install the [Azure Powershell module version 4.1 or higher](https://docs.microsoft.com/powershell/azure/install-azurerm-ps)</span></span>

<span data-ttu-id="a3886-116">O procedimento a seguir cria uma versão prévia (única máquina virtual) de nó único cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a3886-116">The following procedure creates a single-node (single virtual machine) preview Service Fabric cluster.</span></span> <span data-ttu-id="a3886-117">O cluster é protegido por um certificado autoassinado que obtém criado juntamente com o cluster e, em seguida, é colocado em um cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="a3886-117">The cluster is secured by a self-signed certificate that gets created along with the cluster and then placed in a key vault.</span></span> <span data-ttu-id="a3886-118">Os clusters de nó único não podem ser dimensionados além de uma máquina virtual e clusters de versão prévia não podem ser atualizados para versões mais recentes.</span><span class="sxs-lookup"><span data-stu-id="a3886-118">Single-node clusters cannot be scaled beyond one virtual machine and preview clusters cannot be upgraded to newer versions.</span></span>

<span data-ttu-id="a3886-119">Para calcular o custo incorrido ao executar um cluster do Service Fabric no Azure, use a [Calculadora de Preços do Azure](https://azure.microsoft.com/pricing/calculator/).</span><span class="sxs-lookup"><span data-stu-id="a3886-119">To calculate cost incurred by running a Service Fabric cluster in Azure use the [Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/).</span></span>
<span data-ttu-id="a3886-120">Para obter mais informações sobre a criação de clusters do Service Fabric, confira [Criar um cluster do Service Fabric usando o Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="a3886-120">For more information on creating Service Fabric clusters, see [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span>

## <a name="create-the-cluster-using-azure-powershell"></a><span data-ttu-id="a3886-121">Criar o cluster usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a3886-121">Create the cluster using Azure PowerShell</span></span>
1. <span data-ttu-id="a3886-122">Baixe uma cópia local do modelo do Azure Resource Manager e o arquivo de parâmetro do repositório [modelo do Azure Resource Manager para o Service Fabric](https://aka.ms/securepreviewonelineclustertemplate) do GitHub.</span><span class="sxs-lookup"><span data-stu-id="a3886-122">Download a local copy of the Azure Resource Manager template and the parameter file from the [Azure Resource Manager template for Service Fabric](https://aka.ms/securepreviewonelineclustertemplate) GitHub repository.</span></span>  <span data-ttu-id="a3886-123">O *azuredeploy.json* é o modelo do Azure Resource Manager que define um cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a3886-123">*azuredeploy.json* is the Azure Resource Manager template that defines a Service Fabric cluster.</span></span> <span data-ttu-id="a3886-124">O *azuredeploy.parameters.json* é um arquivo de parâmetros para personalizar a implantação do cluster.</span><span class="sxs-lookup"><span data-stu-id="a3886-124">*azuredeploy.parameters.json* is a parameters file for you to customize the cluster deployment.</span></span>

2. <span data-ttu-id="a3886-125">Personalize os seguintes parâmetros no arquivo de parâmetros *azuredeploy.parameters.json*:</span><span class="sxs-lookup"><span data-stu-id="a3886-125">Customize the following parameters in the *azuredeploy.parameters.json* parameters file:</span></span>

   | <span data-ttu-id="a3886-126">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="a3886-126">Parameter</span></span>       | <span data-ttu-id="a3886-127">Descrição</span><span class="sxs-lookup"><span data-stu-id="a3886-127">Description</span></span> | <span data-ttu-id="a3886-128">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="a3886-128">Suggested Value</span></span> |
   | --------------- | ----------- | --------------- |
   | <span data-ttu-id="a3886-129">clusterLocation</span><span class="sxs-lookup"><span data-stu-id="a3886-129">clusterLocation</span></span> | <span data-ttu-id="a3886-130">A região do Azure na qual o cluster será implantado.</span><span class="sxs-lookup"><span data-stu-id="a3886-130">The Azure region to which to deploy the cluster.</span></span> | <span data-ttu-id="a3886-131">*Por exemplo, westeurope, eastasia, eastus*</span><span class="sxs-lookup"><span data-stu-id="a3886-131">*for example, westeurope, eastasia, eastus*</span></span> |
   | <span data-ttu-id="a3886-132">clusterName</span><span class="sxs-lookup"><span data-stu-id="a3886-132">clusterName</span></span>     | <span data-ttu-id="a3886-133">Nome do cluster que você deseja criar.</span><span class="sxs-lookup"><span data-stu-id="a3886-133">Name of the cluster you want to create.</span></span> | <span data-ttu-id="a3886-134">*Por exemplo, bobs-sfpreviewcluster*</span><span class="sxs-lookup"><span data-stu-id="a3886-134">*for example, bobs-sfpreviewcluster*</span></span> |
   | <span data-ttu-id="a3886-135">adminUserName</span><span class="sxs-lookup"><span data-stu-id="a3886-135">adminUserName</span></span>   | <span data-ttu-id="a3886-136">A conta do administrador local nas máquinas virtuais do cluster.</span><span class="sxs-lookup"><span data-stu-id="a3886-136">The local admin account on the cluster virtual machines.</span></span> | <span data-ttu-id="a3886-137">*Qualquer nome de usuário válido do Windows Server*</span><span class="sxs-lookup"><span data-stu-id="a3886-137">*Any valid Windows Server username*</span></span> |
   | <span data-ttu-id="a3886-138">adminPassword</span><span class="sxs-lookup"><span data-stu-id="a3886-138">adminPassword</span></span>   | <span data-ttu-id="a3886-139">Senha da conta do administrador local nas máquinas virtuais do cluster.</span><span class="sxs-lookup"><span data-stu-id="a3886-139">Password of the local admin account on the cluster virtual machines.</span></span> | <span data-ttu-id="a3886-140">*Qualquer senha válida do Windows Server*</span><span class="sxs-lookup"><span data-stu-id="a3886-140">*Any valid Windows Server password*</span></span> |
   | <span data-ttu-id="a3886-141">clusterCodeVersion</span><span class="sxs-lookup"><span data-stu-id="a3886-141">clusterCodeVersion</span></span> | <span data-ttu-id="a3886-142">A versão do Service Fabric a ser executada.</span><span class="sxs-lookup"><span data-stu-id="a3886-142">The Service Fabric version to run.</span></span> <span data-ttu-id="a3886-143">(255.255.X.255 são versões de visualização).</span><span class="sxs-lookup"><span data-stu-id="a3886-143">(255.255.X.255 are preview versions).</span></span> | <span data-ttu-id="a3886-144">**255.255.5718.255**</span><span class="sxs-lookup"><span data-stu-id="a3886-144">**255.255.5718.255**</span></span> |
   | <span data-ttu-id="a3886-145">vmInstanceCount</span><span class="sxs-lookup"><span data-stu-id="a3886-145">vmInstanceCount</span></span> | <span data-ttu-id="a3886-146">O número de máquinas virtuais no cluster (pode ser 1 ou 3-99).</span><span class="sxs-lookup"><span data-stu-id="a3886-146">The number of virtual machines in your cluster (can be 1 or 3-99).</span></span> | <span data-ttu-id="a3886-147">**1**</span><span class="sxs-lookup"><span data-stu-id="a3886-147">**1**</span></span> | <span data-ttu-id="a3886-148">*Para um cluster de visualização, especifique apenas uma máquina virtual*</span><span class="sxs-lookup"><span data-stu-id="a3886-148">*For a preview cluster specify only one virtual machine*</span></span> |

3. <span data-ttu-id="a3886-149">Abra um console do PowerShell, faça logon no Azure e selecione a assinatura na qual você deseja implantar o cluster:</span><span class="sxs-lookup"><span data-stu-id="a3886-149">Open a PowerShell console, login to Azure, and select the subscription you want to deploy the cluster in:</span></span>

   ```powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription -SubscriptionId <subscription-id>
   ```
4. <span data-ttu-id="a3886-150">Crie e criptografe uma senha para o certificado a ser usado pelo Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a3886-150">Create and encrypt a password for the certificate to be used by Service Fabric.</span></span>

   ```powershell
   $pwd = "<your password>" | ConvertTo-SecureString -AsPlainText -Force
   ```
5. <span data-ttu-id="a3886-151">Crie o cluster e seu certificado executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="a3886-151">Create the cluster and its certificate by running the following command:</span></span>

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
   ><span data-ttu-id="a3886-152">O parâmetro `-CertificateSubjectName` deve ser alinhado com o parâmetro clusterName, especificado no arquivo de parâmetros, bem como ao domínio vinculado à região do Azure escolhida, como `clustername.eastus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="a3886-152">The `-CertificateSubjectName` parameter should align with the clusterName parameter specified in the parameters file, as well as the domain tied to the Azure region you chose, such as: `clustername.eastus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="a3886-153">Depois que a configuração for concluído, ele produz informações sobre o cluster criado no Azure.</span><span class="sxs-lookup"><span data-stu-id="a3886-153">Once the configuration finishes, it outputs information about the cluster created in Azure.</span></span> <span data-ttu-id="a3886-154">Ele também copia o certificado de cluster para o diretório - CertificateOutputFolder no caminho especificado para esse parâmetro.</span><span class="sxs-lookup"><span data-stu-id="a3886-154">It also copies the cluster certificate to the -CertificateOutputFolder directory on the path you specified for this parameter.</span></span> <span data-ttu-id="a3886-155">Você precisará deste certificado para acessar o Service Fabric Explorer e exibir a integridade do cluster.</span><span class="sxs-lookup"><span data-stu-id="a3886-155">You need this certificate to access Service Fabric Explorer and view the health of your cluster.</span></span>

<span data-ttu-id="a3886-156">Anote a URL para o cluster, o que pode ser semelhante a seguinte URL: *https://mycluster.westeurope.cloudapp.azure.com:19080*</span><span class="sxs-lookup"><span data-stu-id="a3886-156">Take note of the URL for your cluster, which may be similar to the following URL: *https://mycluster.westeurope.cloudapp.azure.com:19080*</span></span>

## <a name="modify-the-certificate--access-service-fabric-explorer"></a><span data-ttu-id="a3886-157">Modificar o certificado e acessar o Gerenciador do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a3886-157">Modify the certificate & access Service Fabric Explorer</span></span> ##

1. <span data-ttu-id="a3886-158">Clique duas vezes no certificado para abrir o Assistente para Importação de Certificados.</span><span class="sxs-lookup"><span data-stu-id="a3886-158">Double-click the certificate to open the Certificate Import Wizard.</span></span>

2. <span data-ttu-id="a3886-159">Use as configurações padrão, mas marque a caixa de seleção **Marcar esta chave como exportável.**</span><span class="sxs-lookup"><span data-stu-id="a3886-159">Use default settings, but make sure to check the **Mark this key as exportable.**</span></span> <span data-ttu-id="a3886-160">, na etapa **proteção de chave privada**.</span><span class="sxs-lookup"><span data-stu-id="a3886-160">check box, in the **private key protection** step.</span></span> <span data-ttu-id="a3886-161">O Visual Studio precisa exportar o certificado ao configurar o Registro de Contêiner do Azure para autenticação do Cluster do Service Fabric, mais adiante neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="a3886-161">Visual Studio needs to export the certificate when configuring Azure Container Registry to Service Fabric Cluster authentication later in this tutorial.</span></span>

3. <span data-ttu-id="a3886-162">Agora você pode abrir o Service Fabric Explorer em um navegador.</span><span class="sxs-lookup"><span data-stu-id="a3886-162">You can now open Service Fabric Explorer in a browser.</span></span> <span data-ttu-id="a3886-163">Para fazer isso, navegue até o **ManagementEndpoint** URL para o cluster usando um navegador da web e selecione o certificado que foi salvo no seu computador.</span><span class="sxs-lookup"><span data-stu-id="a3886-163">To do so, navigate to the **ManagementEndpoint** URL for your cluster using a web browser, and select the certificate that was saved on your machine.</span></span>

>[!NOTE]
><span data-ttu-id="a3886-164">Ao abrir o Service Fabric Explorer, você verá um erro de certificado, pois está usando um certificado autoassinado.</span><span class="sxs-lookup"><span data-stu-id="a3886-164">When opening Service Fabric Explorer, you see a certificate error, as you are using a self-signed certificate.</span></span> <span data-ttu-id="a3886-165">No Edge, você precisa clicar em *Detalhes* e no link *Ir para a página da Web*.</span><span class="sxs-lookup"><span data-stu-id="a3886-165">In Edge, you have to click *Details* and then the *Go on to the webpage* link.</span></span> <span data-ttu-id="a3886-166">No Chrome, você precisa clicar em *Avançado* e no link *Continuar*.</span><span class="sxs-lookup"><span data-stu-id="a3886-166">In Chrome, you have to click *Advanced* and then the *proceed* link.</span></span>

>[!NOTE]
><span data-ttu-id="a3886-167">Se a criação do cluster falhar, você sempre poderá executar novamente o comando, o que atualiza os recursos já implantados.</span><span class="sxs-lookup"><span data-stu-id="a3886-167">If the cluster creation fails, you can always rerun the command, which updates the resources already deployed.</span></span> <span data-ttu-id="a3886-168">Se um certificado tiver sido criado como parte da implantação com falha, um novo será gerado.</span><span class="sxs-lookup"><span data-stu-id="a3886-168">If a certificate was created as part of the failed deployment, a new one is generated.</span></span> <span data-ttu-id="a3886-169">Para solucionar problemas de criação do cluster, consulte [Criar um cluster do Service Fabric usando o Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="a3886-169">To troubleshoot cluster creation, see [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span>

## <a name="connect-to-the-secure-cluster"></a><span data-ttu-id="a3886-170">Conectar-se ao cluster seguro</span><span class="sxs-lookup"><span data-stu-id="a3886-170">Connect to the secure cluster</span></span>
<span data-ttu-id="a3886-171">Conecte-se ao cluster usando o módulo do PowerShell do Service Fabric instalado com o SDK do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a3886-171">Connect to the cluster using the Service Fabric PowerShell module installed with the Service Fabric SDK.</span></span>  <span data-ttu-id="a3886-172">Primeiro, instale o certificado no repositório pessoal (Meu) do usuário atual no seu computador.</span><span class="sxs-lookup"><span data-stu-id="a3886-172">First, install the certificate into the Personal (My) store of the current user on your computer.</span></span>  <span data-ttu-id="a3886-173">Execute o seguinte comando do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="a3886-173">Run the following PowerShell command:</span></span>

```powershell
$certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\mysfcluster20170531104310.pfx `
        -Password $certpwd
```

<span data-ttu-id="a3886-174">Agora você está pronto para se conectar ao seu cluster seguro.</span><span class="sxs-lookup"><span data-stu-id="a3886-174">You are now ready to connect to your secure cluster.</span></span>

<span data-ttu-id="a3886-175">O módulo do PowerShell do **Service Fabric** fornece vários cmdlets para gerenciar clusters, aplicativos e serviços do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a3886-175">The **Service Fabric** PowerShell module provides many cmdlets for managing Service Fabric clusters, applications, and services.</span></span>  <span data-ttu-id="a3886-176">Use o cmdlet [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster) para se conectar ao cluster seguro.</span><span class="sxs-lookup"><span data-stu-id="a3886-176">Use the [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster) cmdlet to connect to the secure cluster.</span></span> <span data-ttu-id="a3886-177">Os detalhes de ponto de extremidade de conexão e de impressão digital do certificado podem ser encontrados na saída da etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="a3886-177">The certificate thumbprint and connection endpoint details are found in the output from a previous step.</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mysfcluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="a3886-178">Verifique se você está conectado e se o cluster está íntegro, usando o cmdlet [Get-ServiceFabricClusterHealth](/powershell/module/servicefabric/get-servicefabricclusterhealth).</span><span class="sxs-lookup"><span data-stu-id="a3886-178">Check that you are connected and the cluster is healthy using the [Get-ServiceFabricClusterHealth](/powershell/module/servicefabric/get-servicefabricclusterhealth) cmdlet.</span></span>

```powershell
Get-ServiceFabricClusterHealth
```

## <a name="clean-up-resources"></a><span data-ttu-id="a3886-179">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="a3886-179">Clean up resources</span></span>

<span data-ttu-id="a3886-180">Um cluster é composto por outros recursos do Azure, além do próprio recurso do cluster.</span><span class="sxs-lookup"><span data-stu-id="a3886-180">A cluster is made up of other Azure resources in addition to the cluster resource itself.</span></span> <span data-ttu-id="a3886-181">A maneira mais simples de excluir o cluster e todos os recursos que ele consume é excluir o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a3886-181">The simplest way to delete the cluster and all the resources it consumes is to delete the resource group.</span></span>

<span data-ttu-id="a3886-182">Faça logon no Azure e selecione a ID de assinatura com a qual você deseja remover o cluster.</span><span class="sxs-lookup"><span data-stu-id="a3886-182">Log in to Azure and select the subscription ID with which you want to remove the cluster.</span></span>  <span data-ttu-id="a3886-183">Você pode encontrar sua ID de assinatura fazendo logon no [Portal do Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a3886-183">You can find your subscription ID by logging in to the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="a3886-184">Exclua o grupo de recursos e todos os recursos de cluster usando o [cmdlet Remove-AzureRMResourceGroup](/en-us/powershell/module/azurerm.resources/remove-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="a3886-184">Delete the resource group and all the cluster resources using the [Remove-AzureRMResourceGroup cmdlet](/en-us/powershell/module/azurerm.resources/remove-azurermresourcegroup).</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId "Subcription ID"

$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="next-steps"></a><span data-ttu-id="a3886-185">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a3886-185">Next steps</span></span>
<span data-ttu-id="a3886-186">Neste tutorial, você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="a3886-186">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a3886-187">Criar um cluster do Service Fabric no Azure</span><span class="sxs-lookup"><span data-stu-id="a3886-187">Create a Service Fabric cluster in Azure</span></span>
> * <span data-ttu-id="a3886-188">Proteger o cluster com um certificado X.509</span><span class="sxs-lookup"><span data-stu-id="a3886-188">Secure the cluster with an X.509 certificate</span></span>
> * <span data-ttu-id="a3886-189">Conectar o cluster usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="a3886-189">Connect to the cluster using PowerShell</span></span>
> * <span data-ttu-id="a3886-190">Remover um cluster</span><span class="sxs-lookup"><span data-stu-id="a3886-190">Remove a cluster</span></span>

<span data-ttu-id="a3886-191">Em seguida, avance para o próximo tutorial para saber como implantar um aplicativo existente.</span><span class="sxs-lookup"><span data-stu-id="a3886-191">Next, advance to the following tutorial to learn how to deploy an existing application.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="a3886-192">Implantar um aplicativo existente do .NET com o Docker Compose</span><span class="sxs-lookup"><span data-stu-id="a3886-192">Deploy an existing .NET application with Docker Compose</span></span>](service-fabric-host-app-in-a-container.md)
