---
title: clusters de aaaCreate Hadoop usando modelos - HDInsight do Azure | Microsoft Docs
description: Saiba como toocreate clusters de HDInsight usando modelos do Gerenciador de recursos
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00a80dea-011f-44f0-92a4-25d09db9d996
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/30/2017
ms.author: jgao
ms.openlocfilehash: 92a6c1d888e401a11537dba34f188245ac17f448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-clusters-in-hdinsight-by-using-resource-manager-templates"></a><span data-ttu-id="2c645-103">Criar clusters Hadoop no HDInsight usando modelos do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2c645-103">Create Hadoop clusters in HDInsight by using Resource Manager templates</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="2c645-104">Neste artigo, você aprenderá várias maneiras toocreate HDInsight do Azure clusters com modelos do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="2c645-104">In this article, you learn several ways toocreate Azure HDInsight clusters with Azure Resource Manager templates.</span></span> <span data-ttu-id="2c645-105">Para saber mais, confira [Implantar um aplicativo com o modelo do Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="2c645-105">For more information, see [Deploy an application with Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="2c645-106">toolearn sobre outras ferramentas de criação de cluster e recursos, clique no seletor de guia Olá na parte superior da saudação dessa página ou consulte [métodos de criação de Cluster](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).</span><span class="sxs-lookup"><span data-stu-id="2c645-106">toolearn about other cluster creation tools and features, click hello tab selector on hello top of this page or see [Cluster creation methods](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2c645-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2c645-107">Prerequisites</span></span>
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="2c645-108">instruções de saudação toofollow neste artigo, você precisará:</span><span class="sxs-lookup"><span data-stu-id="2c645-108">toofollow hello instructions in this article, you'll need:</span></span>

* <span data-ttu-id="2c645-109">Uma [assinatura do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="2c645-109">An [Azure subscription](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="2c645-110">Azure PowerShell e/ou CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="2c645-110">Azure PowerShell and/or Azure CLI.</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell-and-cli.md)]

### <a name="resource-manager-templates"></a><span data-ttu-id="2c645-111">Modelos do Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="2c645-111">Resource Manager templates</span></span>
<span data-ttu-id="2c645-112">Um modelo do Gerenciador de recursos torna fácil toocreate Olá a seguir para seu aplicativo em uma única operação coordenado:</span><span class="sxs-lookup"><span data-stu-id="2c645-112">A Resource Manager template makes it easy toocreate hello following for your application in a single, coordinated operation:</span></span>
* <span data-ttu-id="2c645-113">Clusters HDInsight e seus recursos dependentes (como a conta de armazenamento padrão Olá)</span><span class="sxs-lookup"><span data-stu-id="2c645-113">HDInsight clusters and their dependent resources (such as hello default storage account)</span></span>
* <span data-ttu-id="2c645-114">Outros recursos (como o banco de dados do Azure SQL toouse Apache Sqoop)</span><span class="sxs-lookup"><span data-stu-id="2c645-114">Other resources (such as Azure SQL Database toouse Apache Sqoop)</span></span>

<span data-ttu-id="2c645-115">No modelo de hello, você define os recursos de saudação que são necessários para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="2c645-115">In hello template, you define hello resources that are needed for hello application.</span></span> <span data-ttu-id="2c645-116">Você também pode especificar valores de tooinput de parâmetros de implantação para ambientes diferentes.</span><span class="sxs-lookup"><span data-stu-id="2c645-116">You also specify deployment parameters tooinput values for different environments.</span></span> <span data-ttu-id="2c645-117">Olá modelo consiste em JSON e expressões que você use tooconstruct valores para sua implantação.</span><span class="sxs-lookup"><span data-stu-id="2c645-117">hello template consists of JSON and expressions that you use tooconstruct values for your deployment.</span></span>

<span data-ttu-id="2c645-118">É possível encontrar amostras de modelo do HDInsight em [Modelos de início rápido do Azure](https://azure.microsoft.com/resources/templates/?term=hdinsight).</span><span class="sxs-lookup"><span data-stu-id="2c645-118">You can find HDInsight template samples at [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/?term=hdinsight).</span></span> <span data-ttu-id="2c645-119">Usar da plataforma cruzada [código do Visual Studio](https://code.visualstudio.com/#alt-downloads) com hello [extensão do Gerenciador de recursos](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) ou um modelo do hello de toosave do editor de texto em um arquivo na estação de trabalho.</span><span class="sxs-lookup"><span data-stu-id="2c645-119">Use cross-platform [Visual Studio Code](https://code.visualstudio.com/#alt-downloads) with hello [Resource Manager extension](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) or a text editor toosave hello template into a file on your workstation.</span></span> <span data-ttu-id="2c645-120">Você aprenderá como toocall Olá modelo usando métodos diferentes.</span><span class="sxs-lookup"><span data-stu-id="2c645-120">You learn how toocall hello template by using different methods.</span></span>

<span data-ttu-id="2c645-121">Para obter mais informações sobre modelos do Gerenciador de recursos, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="2c645-121">For more information about Resource Manager templates, see hello following articles:</span></span>

* [<span data-ttu-id="2c645-122">Criar modelos do Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="2c645-122">Author Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)
* [<span data-ttu-id="2c645-123">Implantar um aplicativo com o modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2c645-123">Deploy an application with Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-template-deploy.md)

## <a name="generate-templates"></a><span data-ttu-id="2c645-124">Gerar modelos</span><span class="sxs-lookup"><span data-stu-id="2c645-124">Generate templates</span></span>

<span data-ttu-id="2c645-125">Usando Olá portal do Azure, você pode configurar todas as propriedades de saudação de um cluster e, em seguida, salve o modelo de saudação antes de implantá-lo.</span><span class="sxs-lookup"><span data-stu-id="2c645-125">By using hello Azure portal, you can configure all hello properties of a cluster and then save hello template before deploying it.</span></span> <span data-ttu-id="2c645-126">Em seguida, você pode reutilizar o modelo hello.</span><span class="sxs-lookup"><span data-stu-id="2c645-126">You can then reuse hello template.</span></span>

<span data-ttu-id="2c645-127">**toogenerate um modelo usando Olá portal do Azure**</span><span class="sxs-lookup"><span data-stu-id="2c645-127">**toogenerate a template by using hello Azure portal**</span></span>

1. <span data-ttu-id="2c645-128">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2c645-128">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="2c645-129">Clique em **novo** no menu esquerdo Olá **Intelligence + análise**e, em seguida, clique em **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="2c645-129">Click **New** on hello left menu, click **Intelligence + analytics**, and then click **HDInsight**.</span></span>
3. <span data-ttu-id="2c645-130">Seguem Olá instruções tooenter propriedades.</span><span class="sxs-lookup"><span data-stu-id="2c645-130">Follow hello instructions tooenter properties.</span></span> <span data-ttu-id="2c645-131">Você pode usar o hello **criação rápida** ou hello **personalizado** opção.</span><span class="sxs-lookup"><span data-stu-id="2c645-131">You can use either hello **Quick create** or hello **Custom** option.</span></span>
4. <span data-ttu-id="2c645-132">Em Olá **resumo** , clique em **baixar modelo e parâmetros de**:</span><span class="sxs-lookup"><span data-stu-id="2c645-132">On hello **Summary** tab, click **Download template and parameters**:</span></span>

    ![Criação de cluster de Download do modelo do Resource Manager pelo Hadoop HDInsight](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download.png)

    <span data-ttu-id="2c645-134">Você verá uma lista de arquivo de modelo hello, arquivo de parâmetros e código amostras usadas toodeploy Olá modelo:</span><span class="sxs-lookup"><span data-stu-id="2c645-134">You see a list of hello template file, parameters file, and code samples used toodeploy hello template:</span></span>

    ![Criação de cluster de Opções de download do modelo do Resource Manager pelo Hadoop HDInsight](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download-options.png)

    <span data-ttu-id="2c645-136">A partir daqui, baixar modelo hello, salvá-lo tooyour biblioteca de modelos ou implantar o modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="2c645-136">From here, you can download hello template, save it tooyour template library, or deploy hello template.</span></span>

    <span data-ttu-id="2c645-137">tooaccess um modelo de biblioteca, clique em **mais serviços** no menu esquerdo hello e clique **modelos** (em Olá **outros** categoria).</span><span class="sxs-lookup"><span data-stu-id="2c645-137">tooaccess a template in your library, click **More services** from hello left menu, and then click **Templates** (under hello **Other** category).</span></span>

    > [!Note]
    > <span data-ttu-id="2c645-138">arquivo de modelo e parâmetros de saudação deve ser usado juntas.</span><span class="sxs-lookup"><span data-stu-id="2c645-138">hello template and parameters file must be used together.</span></span> <span data-ttu-id="2c645-139">Caso contrário, você poderá obter resultados inesperados.</span><span class="sxs-lookup"><span data-stu-id="2c645-139">Otherwise, you might get unexpected results.</span></span> <span data-ttu-id="2c645-140">Por exemplo, Olá padrão **clusterKind** o valor da propriedade é sempre **hadoop**, apesar do que você especificar antes de baixar o modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="2c645-140">For example, hello default **clusterKind** property value is always **hadoop**, despite what you specify before you download hello template.</span></span>



## <a name="deploy-with-powershell"></a><span data-ttu-id="2c645-141">Implantação com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="2c645-141">Deploy with PowerShell</span></span>

<span data-ttu-id="2c645-142">Esse procedimento cria um cluster Hadoop no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2c645-142">This procedure creates a Hadoop cluster in HDInsight.</span></span>

1. <span data-ttu-id="2c645-143">Salve o arquivo JSON de saudação em Olá [apêndice](#appx-a-arm-template) tooyour estação de trabalho.</span><span class="sxs-lookup"><span data-stu-id="2c645-143">Save hello JSON file in hello [Appendix](#appx-a-arm-template) tooyour workstation.</span></span> <span data-ttu-id="2c645-144">Olá script do PowerShell, nome de arquivo hello é `C:\HDITutorials-ARM\hdinsight-arm-template.json`.</span><span class="sxs-lookup"><span data-stu-id="2c645-144">In hello PowerShell script, hello file name is `C:\HDITutorials-ARM\hdinsight-arm-template.json`.</span></span>
2. <span data-ttu-id="2c645-145">Defina as variáveis e parâmetros de saudação se necessário.</span><span class="sxs-lookup"><span data-stu-id="2c645-145">Set hello parameters and variables if needed.</span></span>
3. <span data-ttu-id="2c645-146">Execute o modelo hello usando Olá script do PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="2c645-146">Run hello template by using hello following PowerShell script:</span></span>

        ####################################
        # Set these variables
        ####################################
        #region - used for creating Azure service names
        $nameToken = "<Enter an Alias>"
        $templateFile = "C:\HDITutorials-ARM\hdinsight-arm-template.json"
        #endregion

        ####################################
        # Service names and variables
        ####################################
        #region - service names
        $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

        $resourceGroupName = $namePrefix + "rg"
        $hdinsightClusterName = $namePrefix + "hdi"
        $defaultStorageAccountName = $namePrefix + "store"
        $defaultBlobContainerName = $hdinsightClusterName

        $location = "East US 2"

        $armDeploymentName = $namePrefix
        #endregion

        ####################################
        # Connect tooAzure
        ####################################
        #region - Connect tooAzure subscription
        Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
        try{Get-AzureRmContext}
        catch{Login-AzureRmAccount}
        #endregion

        # Create a resource group
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $Location

        # Create cluster and hello dependent storage account
        $parameters = @{clusterName="$hdinsightClusterName"}

        New-AzureRmResourceGroupDeployment `
            -Name $armDeploymentName `
            -ResourceGroupName $resourceGroupName `
            -TemplateFile $templateFile `
            -TemplateParameterObject $parameters

        # List cluster
        Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName

    <span data-ttu-id="2c645-147">saudação de script do PowerShell configura apenas o nome de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="2c645-147">hello PowerShell script configures only hello cluster name.</span></span> <span data-ttu-id="2c645-148">o nome de conta de armazenamento Olá é embutido no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="2c645-148">hello storage account name is hard-coded in hello template.</span></span> <span data-ttu-id="2c645-149">Você está senha de usuário de cluster de saudação tooenter solicitada.</span><span class="sxs-lookup"><span data-stu-id="2c645-149">You are prompted tooenter hello cluster user password.</span></span> <span data-ttu-id="2c645-150">(nome de usuário saudação padrão é **admin**.) Você também é senha de usuário solicitada tooenter Olá SSH.</span><span class="sxs-lookup"><span data-stu-id="2c645-150">(hello default username is **admin**.) You are also prompted tooenter hello SSH user password.</span></span> <span data-ttu-id="2c645-151">(nome de usuário do SSH saudação padrão é **sshuser**.)</span><span class="sxs-lookup"><span data-stu-id="2c645-151">(hello default SSH username is **sshuser**.)</span></span>  

<span data-ttu-id="2c645-152">Para obter mais informações, veja [Implantar com o PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span><span class="sxs-lookup"><span data-stu-id="2c645-152">For more information, see  [Deploy with PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span></span>

## <a name="deploy-with-cli"></a><span data-ttu-id="2c645-153">Implantar com a CLI</span><span class="sxs-lookup"><span data-stu-id="2c645-153">Deploy with CLI</span></span>
<span data-ttu-id="2c645-154">saudação de exemplo a seguir usa a interface de linha de comando (CLI) do Azure.</span><span class="sxs-lookup"><span data-stu-id="2c645-154">hello following sample uses Azure command-line interface (CLI).</span></span> <span data-ttu-id="2c645-155">Ele cria um cluster e os respectivos contêiner e conta de armazenamento dependente chamando um modelo do Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="2c645-155">It creates a cluster and its dependent storage account and container by calling a Resource Manager template:</span></span>

    azure login
    azure config mode arm
    azure group create -n hdi1229rg -l "East US"
    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "C:\HDITutorials-ARM\hdinsight-arm-template.json"

<span data-ttu-id="2c645-156">Você está tooenter solicitada:</span><span class="sxs-lookup"><span data-stu-id="2c645-156">You are prompted tooenter:</span></span>
* <span data-ttu-id="2c645-157">nome do cluster Hello.</span><span class="sxs-lookup"><span data-stu-id="2c645-157">hello cluster name.</span></span>
* <span data-ttu-id="2c645-158">senha de usuário de cluster Hello.</span><span class="sxs-lookup"><span data-stu-id="2c645-158">hello cluster user password.</span></span> <span data-ttu-id="2c645-159">(nome de usuário saudação padrão é **admin**.)</span><span class="sxs-lookup"><span data-stu-id="2c645-159">(hello default username is **admin**.)</span></span>
* <span data-ttu-id="2c645-160">senha de usuário SSH Hello.</span><span class="sxs-lookup"><span data-stu-id="2c645-160">hello SSH user password.</span></span> <span data-ttu-id="2c645-161">(nome de usuário do SSH saudação padrão é **sshuser**.)</span><span class="sxs-lookup"><span data-stu-id="2c645-161">(hello default SSH username is **sshuser**.)</span></span>

<span data-ttu-id="2c645-162">saudação de código a seguir fornece parâmetros embutido:</span><span class="sxs-lookup"><span data-stu-id="2c645-162">hello following code provides inline parameters:</span></span>

    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "c:\Tutorials\HDInsightARM\create-linux-based-hadoop-cluster-in-hdinsight.json" --parameters '{\"clusterName\":{\"value\":\"hdi1229\"},\"clusterLoginPassword\":{\"value\":\"Pass@word1\"},\"sshPassword\":{\"value\":\"Pass@word1\"}}'

## <a name="deploy-with-hello-rest-api"></a><span data-ttu-id="2c645-163">Implantar com hello API REST</span><span class="sxs-lookup"><span data-stu-id="2c645-163">Deploy with hello REST API</span></span>
<span data-ttu-id="2c645-164">Consulte [implantar com a API REST de saudação](../azure-resource-manager/resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="2c645-164">See [Deploy with hello REST API](../azure-resource-manager/resource-group-template-deploy-rest.md).</span></span>

## <a name="deploy-with-visual-studio"></a><span data-ttu-id="2c645-165">Implantação com o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2c645-165">Deploy with Visual Studio</span></span>
 <span data-ttu-id="2c645-166">Use o Visual Studio toocreate um projeto do grupo de recursos e implantá-lo tooAzure por meio da interface do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="2c645-166">Use Visual Studio toocreate a resource group project and deploy it tooAzure through hello user interface.</span></span> <span data-ttu-id="2c645-167">Selecione o tipo de saudação de tooinclude de recursos em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="2c645-167">You select hello type of resources tooinclude in your project.</span></span> <span data-ttu-id="2c645-168">Esses recursos são adicionados automaticamente o modelo do Gerenciador de recursos de toohello.</span><span class="sxs-lookup"><span data-stu-id="2c645-168">Those resources are automatically added toohello Resource Manager template.</span></span> <span data-ttu-id="2c645-169">projeto Olá também fornece um modelo de saudação do toodeploy de script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2c645-169">hello project also provides a PowerShell script toodeploy hello template.</span></span>

<span data-ttu-id="2c645-170">Para uma introdução toousing Visual Studio com grupos de recursos, consulte [criando e implantando grupos de recursos do Azure com o Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="2c645-170">For an introduction toousing Visual Studio with resource groups, see [Creating and deploying Azure resource groups through Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="2c645-171">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="2c645-171">Troubleshoot</span></span>

<span data-ttu-id="2c645-172">Se você tiver problemas com a criação de clusters HDInsight, confira os [requisitos de controle de acesso](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="2c645-172">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c645-173">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2c645-173">Next steps</span></span>
<span data-ttu-id="2c645-174">Neste artigo, você aprendeu um cluster HDInsight toocreate de várias maneiras.</span><span class="sxs-lookup"><span data-stu-id="2c645-174">In this article, you have learned several ways toocreate an HDInsight cluster.</span></span> <span data-ttu-id="2c645-175">toolearn mais, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="2c645-175">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="2c645-176">Para obter um exemplo de implantação de recursos por meio da biblioteca de cliente .NET hello, consulte [implantar recursos usando as bibliotecas .NET e um modelo](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2c645-176">For an example of deploying resources through hello .NET client library, see [Deploy resources by using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="2c645-177">Para obter um exemplo detalhado de implantação de um aplicativo, confira [Provisionar e implantar microsserviços de forma previsível no Azure](../app-service-web/app-service-deploy-complex-application-predictably.md).</span><span class="sxs-lookup"><span data-stu-id="2c645-177">For an in-depth example of deploying an application, see [Provision and deploy microservices predictably in Azure](../app-service-web/app-service-deploy-complex-application-predictably.md).</span></span>
* <span data-ttu-id="2c645-178">Para obter orientação sobre a implantação de ambientes de toodifferent sua solução, consulte [ambientes de desenvolvimento e teste no Microsoft Azure](../solution-dev-test-environments.md).</span><span class="sxs-lookup"><span data-stu-id="2c645-178">For guidance on deploying your solution toodifferent environments, see [Development and test environments in Microsoft Azure](../solution-dev-test-environments.md).</span></span>
* <span data-ttu-id="2c645-179">toolearn sobre seções de saudação do modelo do Azure Resource Manager hello, consulte [criar modelos](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="2c645-179">toolearn about hello sections of hello Azure Resource Manager template, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="2c645-180">Para obter uma lista de funções de saudação, você pode usar em um modelo do Gerenciador de recursos do Azure, consulte [funções de modelo](../azure-resource-manager/resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="2c645-180">For a list of hello functions you can use in an Azure Resource Manager template, see [Template functions](../azure-resource-manager/resource-group-template-functions.md).</span></span>

## <a name="appendix-resource-manager-template-toocreate-a-hadoop-cluster"></a><span data-ttu-id="2c645-181">Apêndice: Gerenciador de recursos modelo toocreate um cluster Hadoop</span><span class="sxs-lookup"><span data-stu-id="2c645-181">Appendix: Resource Manager template toocreate a Hadoop cluster</span></span>
<span data-ttu-id="2c645-182">Hello seguinte modelo do Azure Resource Manager cria um cluster Hadoop baseado em Linux com conta de armazenamento do Azure dependentes hello.</span><span class="sxs-lookup"><span data-stu-id="2c645-182">hello following Azure Resource Manager template creates a Linux-based Hadoop cluster with hello dependent Azure storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="2c645-183">Este exemplo inclui informações de configuração para o metastore do Hive e o metastore do Oozie.</span><span class="sxs-lookup"><span data-stu-id="2c645-183">This sample includes configuration information for Hive metastore and Oozie metastore.</span></span> <span data-ttu-id="2c645-184">Remover seção hello ou configurar a seção Olá antes de usar o modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="2c645-184">Remove hello section or configure hello section before using hello template.</span></span>
>
>

    {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "clusterName": {
        "type": "string",
        "metadata": {
            "description": "hello name of hello HDInsight cluster toocreate."
        }
        },
        "clusterLoginUserName": {
        "type": "string",
        "defaultValue": "admin",
        "metadata": {
            "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
        }
        },
        "clusterLoginPassword": {
        "type": "securestring",
        "metadata": {
            "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "sshUserName": {
        "type": "string",
        "defaultValue": "sshuser",
        "metadata": {
            "description": "These credentials can be used tooremotely access hello cluster."
        }
        },
        "sshPassword": {
        "type": "securestring",
        "metadata": {
            "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "location": {
        "type": "string",
        "defaultValue": "East US",
        "allowedValues": [
            "East US",
            "East US 2",
            "North Central US",
            "South Central US",
            "West US",
            "North Europe",
            "West Europe",
            "East Asia",
            "Southeast Asia",
            "Japan East",
            "Japan West",
            "Australia East",
            "Australia Southeast"
        ],
        "metadata": {
            "description": "hello location where all azure resources will be deployed."
        }
        },
        "clusterType": {
        "type": "string",
        "defaultValue": "hadoop",
        "allowedValues": [
            "hadoop",
            "hbase",
            "storm",
            "spark"
        ],
        "metadata": {
            "description": "hello type of hello HDInsight cluster toocreate."
        }
        },
        "clusterWorkerNodeCount": {
        "type": "int",
        "defaultValue": 2,
        "metadata": {
            "description": "hello number of nodes in hello HDInsight cluster."
        }
        }
    },
    "variables": {
        "defaultApiVersion": "2015-05-01-preview",
        "clusterApiVersion": "2015-03-01-preview",
        "clusterStorageAccountName": "[concat(parameters('clusterName'),'store')]"
    },
    "resources": [
        {
        "name": "[variables('clusterStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": { },
        "properties": {
            "accountType": "Standard_LRS"
        }
        },
        {
        "name": "[parameters('clusterName')]",
        "type": "Microsoft.HDInsight/clusters",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('clusterApiVersion')]",
        "dependsOn": [ "[concat('Microsoft.Storage/storageAccounts/',variables('clusterStorageAccountName'))]" ],
        "tags": {

        },
        "properties": {
            "clusterVersion": "3.4",
            "osType": "Linux",
            "tier": "standard",
            "clusterDefinition": {
            "kind": "[parameters('clusterType')]",
            "configurations": {
                "gateway": {
                "restAuthCredential.isEnabled": true,
                "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                },
                "hive-site": {
                    "javax.jdo.option.ConnectionDriverName": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
                    "javax.jdo.option.ConnectionURL": "jdbc:sqlserver://myadla0901dbserver.database.windows.net;database=myhive20160901;encrypt=true;trustServerCertificate=true;create=false;loginTimeout=300",
                    "javax.jdo.option.ConnectionUserName": "johndole",
                    "javax.jdo.option.ConnectionPassword": "myPassword$"
                },
                "hive-env": {
                    "hive_database": "Existing MSSQL Server database with SQL authentication",
                    "hive_database_name": "myhive20160901",
                    "hive_database_type": "mssql",
                    "hive_existing_mssql_server_database": "myhive20160901",
                    "hive_existing_mssql_server_host": "myadla0901dbserver.database.windows.net",
                    "hive_hostname": "myadla0901dbserver.database.windows.net"
                },
                "oozie-site": {
                    "oozie.service.JPAService.jdbc.driver": "com.microsoft.sqlserver.jdbc.SQLServerDriver",
                    "oozie.service.JPAService.jdbc.url": "jdbc:sqlserver://myadla0901dbserver.database.windows.net;database=myhive20160901;encrypt=true;trustServerCertificate=true;create=false;loginTimeout=300",
                    "oozie.service.JPAService.jdbc.username": "johndole",
                    "oozie.service.JPAService.jdbc.password": "myPassword$",
                    "oozie.db.schema.name": "oozie"
                },
                "oozie-env": {
                    "oozie_database": "Existing MSSQL Server database with SQL authentication",
                    "oozie_database_name": "myhive20160901",
                    "oozie_database_type": "mssql",
                    "oozie_existing_mssql_server_database": "myhive20160901",
                    "oozie_existing_mssql_server_host": "myadla0901dbserver.database.windows.net",
                    "oozie_hostname": "myadla0901dbserver.database.windows.net"
                }            
            }
            },
            "storageProfile": {
            "storageaccounts": [
                {
                "name": "[concat(variables('clusterStorageAccountName'),'.blob.core.windows.net')]",
                "isDefault": true,
                "container": "[parameters('clusterName')]",
                "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('clusterStorageAccountName')), variables('defaultApiVersion')).keys[0].value]"
                }
            ]
            },
            "computeProfile": {
            "roles": [
                {
                "name": "headnode",
                "targetInstanceCount": "2",
                "hardwareProfile": {
                    "vmSize": "Standard_D3"
                },
                "osProfile": {
                    "linuxOperatingSystemProfile": {
                    "username": "[parameters('sshUserName')]",
                    "password": "[parameters('sshPassword')]"
                    }
                }
                },
                {
                "name": "workernode",
                "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                "hardwareProfile": {
                    "vmSize": "Standard_D3"
                },
                "osProfile": {
                    "linuxOperatingSystemProfile": {
                    "username": "[parameters('sshUserName')]",
                    "password": "[parameters('sshPassword')]"
                    }
                }
                }
            ]
            }
        }
        }
    ],
    "outputs": {
        "cluster": {
        "type": "object",
        "value": "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
        }
    }
    }

## <a name="appendix-resource-manager-template-toocreate-a-spark-cluster"></a><span data-ttu-id="2c645-185">Apêndice: Gerenciador de recursos modelo toocreate um cluster Spark</span><span class="sxs-lookup"><span data-stu-id="2c645-185">Appendix: Resource Manager template toocreate a Spark cluster</span></span>

<span data-ttu-id="2c645-186">Esta seção fornece um modelo do Gerenciador de recursos que você pode usar toocreate um cluster HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="2c645-186">This section provides a Resource Manager template that you can use toocreate an HDInsight Spark cluster.</span></span> <span data-ttu-id="2c645-187">Esse modelo inclui configurações para `spark-defaults` e `spark-thrift-sparkconf` (para clusters Spark 1.6) e `spark2-defaults` e `spark2-thrift-sparkconf` (para clusters Spark 2).</span><span class="sxs-lookup"><span data-stu-id="2c645-187">This template includes configurations for `spark-defaults` and `spark-thrift-sparkconf` (for Spark 1.6 clusters) and `spark2-defaults` and `spark2-thrift-sparkconf` (for Spark 2 clusters).</span></span> <span data-ttu-id="2c645-188">Além disso, toothis, HDInsight calcula e define as configurações como `spark.executor.instances`, `spark.executor.memory`, e `spark.executor.cores` com base no tamanho do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="2c645-188">In addition toothis, HDInsight calculates and sets configurations such as `spark.executor.instances`, `spark.executor.memory`, and `spark.executor.cores` based on hello cluster size.</span></span> 

<span data-ttu-id="2c645-189">Se você definir qualquer um parâmetro em uma seção como parte do próprio modelo hello, HDInsight não calcular e definir Olá outros parâmetros de saudação mesma seção.</span><span class="sxs-lookup"><span data-stu-id="2c645-189">If you set any one parameter in a section as part of hello template itself, HDInsight does not calculate and set hello other parameters of hello same section.</span></span> <span data-ttu-id="2c645-190">Por exemplo, o parâmetro `spark.executor.instances` está em Olá `spark-defaults` configuração.</span><span class="sxs-lookup"><span data-stu-id="2c645-190">For example, parameter `spark.executor.instances` is in hello  `spark-defaults` configuration.</span></span> <span data-ttu-id="2c645-191">Se você definir outro parâmetro (por exemplo, `spark.yarn.exector.memoryOverhead`) no hello `spark-defaults` configuração HDInsight não calcular e definir Olá `spark.executor.instances` parâmetro também.</span><span class="sxs-lookup"><span data-stu-id="2c645-191">If you set another parameter (for example, `spark.yarn.exector.memoryOverhead`) in hello `spark-defaults` configuration, HDInsight does not calculate and set hello `spark.executor.instances` parameter as well.</span></span>

    {
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "0.9.0.0",
    "parameters": {
        "clusterName": {
            "type": "string",
            "metadata": {
                "description": "hello name of hello HDInsight cluster toocreate."
            }
        },
        "clusterLoginUserName": {
            "type": "string",
            "defaultValue": "admin",
            "metadata": {
                "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
            }
        },
        "clusterLoginPassword": {
            "type": "securestring",
            "metadata": {
                "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        },
        "location": {
            "type": "string",
            "defaultValue": "southcentralus",
            "metadata": {
                "description": "hello location where all azure resources will be deployed."
            }
        },
        "clusterVersion": {
            "type": "string",
            "defaultValue": "3.5",
            "metadata": {
                "description": "HDInsight cluster version."
            }
        },
        "clusterWorkerNodeCount": {
            "type": "int",
            "defaultValue": 4,
            "metadata": {
                "description": "hello number of nodes in hello HDInsight cluster."
            }
        },
        "clusterKind": {
            "type": "string",
            "defaultValue": "SPARK",
            "metadata": {
                "description": "hello type of hello HDInsight cluster toocreate."
            }
        },
        "sshUserName": {
            "type": "string",
            "defaultValue": "sshuser",
            "metadata": {
                "description": "These credentials can be used tooremotely access hello cluster."
            }
        },
        "sshPassword": {
            "type": "securestring",
            "metadata": {
                "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        }
    },
    "variables": {
        "defaultApiVersion": "2017-06-01",
        "clusterStorageAccountName": "[concat(parameters('clusterName'),'store')]"
    },
    "resources": [
        {
        "name": "[variables('clusterStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": { },
        "properties": {
            "accountType": "Standard_LRS"
        }
        },
    {
            "apiVersion": "2015-03-01-preview",
            "name": "[parameters('clusterName')]",
            "type": "Microsoft.HDInsight/clusters",
            "location": "[parameters('location')]",
            "dependsOn": [],
            "properties": {
                "clusterVersion": "[parameters('clusterVersion')]",
                "osType": "Linux",
                "tier": "standard",
                "clusterDefinition": {
                    "kind": "[parameters('clusterKind')]",
                    "configurations": {
                        "gateway": {
                            "restAuthCredential.isEnabled": true,
                            "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                            "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                        },
                        "spark-defaults": {
                            "spark.executor.cores": "2"
                        },
                        "spark-thrift-sparkconf": {
                            "spark.yarn.executor.memoryOverhead": "896"
                        }
                    }
                },
                "storageProfile": {
                    "storageaccounts": [
                        {
                            "name": "[concat(variables('clusterStorageAccountName'),'.blob.core.windows.net')]",
                            "isDefault": true,
                            "container": "[parameters('clusterName')]",
                            "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('clusterStorageAccountName')), variables('defaultApiVersion')).keys[0].value]"
                        }
                    ]
                },
                "computeProfile": {
                    "roles": [
                        {
                            "name": "headnode",
                            "minInstanceCount": 1,
                            "targetInstanceCount": 2,
                            "hardwareProfile": {
                                "vmSize": "Standard_D12"
                            },
                            "osProfile": {
                                "linuxOperatingSystemProfile": {
                                    "username": "[parameters('sshUserName')]",
                                    "password": "[parameters('sshPassword')]"
                                }
                            },
                            "virtualNetworkProfile": null,
                            "scriptActions": []
                        },
                        {
                            "name": "workernode",
                            "minInstanceCount": 1,
                            "targetInstanceCount": 4,
                            "hardwareProfile": {
                                "vmSize": "Standard_D4"
                            },
                            "osProfile": {
                                "linuxOperatingSystemProfile": {
                                    "username": "[parameters('sshUserName')]",
                                    "password": "[parameters('sshPassword')]"
                                    }
                                },
                                "virtualNetworkProfile": null,
                                "scriptActions": []
                            }
                        ]
                    }
                }
            }
        ]
    }
