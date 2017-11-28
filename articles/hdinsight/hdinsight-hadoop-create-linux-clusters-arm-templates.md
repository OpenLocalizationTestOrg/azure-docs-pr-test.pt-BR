---
title: "Criar clusters Hadoop usando modelos – Azure HDInsight | Microsoft Docs"
description: Aprenda a criar clusters para o HDInsight usando modelos do Resource Manager
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
ms.openlocfilehash: b2cdc954530daea2a641599c946ce3787149e762
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="create-hadoop-clusters-in-hdinsight-by-using-resource-manager-templates"></a><span data-ttu-id="c6766-103">Criar clusters Hadoop no HDInsight usando modelos do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c6766-103">Create Hadoop clusters in HDInsight by using Resource Manager templates</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="c6766-104">Neste artigo, você aprenderá várias maneiras de criar clusters do Azure HDInsight com modelos do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c6766-104">In this article, you learn several ways to create Azure HDInsight clusters with Azure Resource Manager templates.</span></span> <span data-ttu-id="c6766-105">Para saber mais, confira [Implantar um aplicativo com o modelo do Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="c6766-105">For more information, see [Deploy an application with Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="c6766-106">Para aprender sobre outros recursos e outras ferramentas de criação de cluster, clique no seletor de guia na parte superior dessa página ou consulte [Métodos de criação de cluster](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).</span><span class="sxs-lookup"><span data-stu-id="c6766-106">To learn about other cluster creation tools and features, click the tab selector on the top of this page or see [Cluster creation methods](hdinsight-hadoop-provision-linux-clusters.md#cluster-setup-methods).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c6766-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c6766-107">Prerequisites</span></span>
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="c6766-108">Para seguir as instruções neste artigo, você precisará de:</span><span class="sxs-lookup"><span data-stu-id="c6766-108">To follow the instructions in this article, you'll need:</span></span>

* <span data-ttu-id="c6766-109">Uma [assinatura do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="c6766-109">An [Azure subscription](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="c6766-110">Azure PowerShell e/ou CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6766-110">Azure PowerShell and/or Azure CLI.</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell-and-cli.md)]

### <a name="resource-manager-templates"></a><span data-ttu-id="c6766-111">Modelos do Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="c6766-111">Resource Manager templates</span></span>
<span data-ttu-id="c6766-112">Um modelo do Resource Manager torna mais fácil criar o seguinte para o seu aplicativo, em uma única operação coordenada:</span><span class="sxs-lookup"><span data-stu-id="c6766-112">A Resource Manager template makes it easy to create the following for your application in a single, coordinated operation:</span></span>
* <span data-ttu-id="c6766-113">Clusters HDInsight e seus recursos dependentes (tais como a conta de armazenamento padrão)</span><span class="sxs-lookup"><span data-stu-id="c6766-113">HDInsight clusters and their dependent resources (such as the default storage account)</span></span>
* <span data-ttu-id="c6766-114">Outros recursos (tais como o Banco de Dados SQL do Azure para usar o Apache Sqoop)</span><span class="sxs-lookup"><span data-stu-id="c6766-114">Other resources (such as Azure SQL Database to use Apache Sqoop)</span></span>

<span data-ttu-id="c6766-115">No modelo, você deve definir os recursos que são necessários para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c6766-115">In the template, you define the resources that are needed for the application.</span></span> <span data-ttu-id="c6766-116">Você também pode especificar parâmetros de implantação para inserir valores para ambientes diferentes.</span><span class="sxs-lookup"><span data-stu-id="c6766-116">You also specify deployment parameters to input values for different environments.</span></span> <span data-ttu-id="c6766-117">O modelo consiste em JSON e expressões que você pode usar para criar valores para sua implantação.</span><span class="sxs-lookup"><span data-stu-id="c6766-117">The template consists of JSON and expressions that you use to construct values for your deployment.</span></span>

<span data-ttu-id="c6766-118">É possível encontrar amostras de modelo do HDInsight em [Modelos de início rápido do Azure](https://azure.microsoft.com/resources/templates/?term=hdinsight).</span><span class="sxs-lookup"><span data-stu-id="c6766-118">You can find HDInsight template samples at [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/?term=hdinsight).</span></span> <span data-ttu-id="c6766-119">Use o [Visual Studio Code](https://code.visualstudio.com/#alt-downloads) de plataforma cruzada com a [extensão do Resource Manager](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) ou um editor de texto para salvar o modelo em um arquivo da estação de trabalho.</span><span class="sxs-lookup"><span data-stu-id="c6766-119">Use cross-platform [Visual Studio Code](https://code.visualstudio.com/#alt-downloads) with the [Resource Manager extension](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) or a text editor to save the template into a file on your workstation.</span></span> <span data-ttu-id="c6766-120">Você aprende a chamar o modelo usando diferentes métodos.</span><span class="sxs-lookup"><span data-stu-id="c6766-120">You learn how to call the template by using different methods.</span></span>

<span data-ttu-id="c6766-121">Para obter mais informações sobre modelos do Resource Manager, consulte os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="c6766-121">For more information about Resource Manager templates, see the following articles:</span></span>

* [<span data-ttu-id="c6766-122">Criar modelos do Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="c6766-122">Author Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)
* [<span data-ttu-id="c6766-123">Implantar um aplicativo com o modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c6766-123">Deploy an application with Azure Resource Manager templates</span></span>](../azure-resource-manager/resource-group-template-deploy.md)

## <a name="generate-templates"></a><span data-ttu-id="c6766-124">Gerar modelos</span><span class="sxs-lookup"><span data-stu-id="c6766-124">Generate templates</span></span>

<span data-ttu-id="c6766-125">Usando o portal do Azure, é possível configurar todas as propriedades de um cluster e, em seguida, salvar o modelo antes de implantá-lo.</span><span class="sxs-lookup"><span data-stu-id="c6766-125">By using the Azure portal, you can configure all the properties of a cluster and then save the template before deploying it.</span></span> <span data-ttu-id="c6766-126">Você pode então reutilizar o modelo.</span><span class="sxs-lookup"><span data-stu-id="c6766-126">You can then reuse the template.</span></span>

<span data-ttu-id="c6766-127">**Para gerar um modelo usando o portal do Azure**</span><span class="sxs-lookup"><span data-stu-id="c6766-127">**To generate a template by using the Azure portal**</span></span>

1. <span data-ttu-id="c6766-128">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c6766-128">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c6766-129">Clique em **Novo** no menu à esquerda, clique em **Inteligência + análise** e em **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="c6766-129">Click **New** on the left menu, click **Intelligence + analytics**, and then click **HDInsight**.</span></span>
3. <span data-ttu-id="c6766-130">Siga as instruções para inserir propriedades.</span><span class="sxs-lookup"><span data-stu-id="c6766-130">Follow the instructions to enter properties.</span></span> <span data-ttu-id="c6766-131">É possível usar tanto a opção **Criação rápida** ou **Personalizado**.</span><span class="sxs-lookup"><span data-stu-id="c6766-131">You can use either the **Quick create** or the **Custom** option.</span></span>
4. <span data-ttu-id="c6766-132">Na guia **Resumo**, clique em **Baixar modelo e parâmetros**:</span><span class="sxs-lookup"><span data-stu-id="c6766-132">On the **Summary** tab, click **Download template and parameters**:</span></span>

    ![Criação de cluster de Download do modelo do Resource Manager pelo Hadoop HDInsight](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download.png)

    <span data-ttu-id="c6766-134">Você vê uma lista o arquivo de modelo, o arquivo de parâmetros e os exemplos de código para implantar o modelo:</span><span class="sxs-lookup"><span data-stu-id="c6766-134">You see a list of the template file, parameters file, and code samples used to deploy the template:</span></span>

    ![Criação de cluster de Opções de download do modelo do Resource Manager pelo Hadoop HDInsight](./media/hdinsight-hadoop-create-linux-clusters-arm-templates/hdinsight-create-cluster-resource-manager-template-download-options.png)

    <span data-ttu-id="c6766-136">Aqui, é possível baixar o modelo, salvá-lo na biblioteca de modelos ou implantá-lo.</span><span class="sxs-lookup"><span data-stu-id="c6766-136">From here, you can download the template, save it to your template library, or deploy the template.</span></span>

    <span data-ttu-id="c6766-137">Para acessar um modelo na biblioteca, clique em **Mais serviços** no menu à esquerda e clique em **Modelos** (na categoria **Outros**).</span><span class="sxs-lookup"><span data-stu-id="c6766-137">To access a template in your library, click **More services** from the left menu, and then click **Templates** (under the **Other** category).</span></span>

    > [!Note]
    > <span data-ttu-id="c6766-138">O arquivo de parâmetros e o modelo devem ser usados juntos.</span><span class="sxs-lookup"><span data-stu-id="c6766-138">The template and parameters file must be used together.</span></span> <span data-ttu-id="c6766-139">Caso contrário, você poderá obter resultados inesperados.</span><span class="sxs-lookup"><span data-stu-id="c6766-139">Otherwise, you might get unexpected results.</span></span> <span data-ttu-id="c6766-140">Por exemplo, o valor da propriedade **clusterKind** padrão é sempre **hadoop**, independentemente do que foi especificado antes de o modelo ser baixado.</span><span class="sxs-lookup"><span data-stu-id="c6766-140">For example, the default **clusterKind** property value is always **hadoop**, despite what you specify before you download the template.</span></span>



## <a name="deploy-with-powershell"></a><span data-ttu-id="c6766-141">Implantação com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="c6766-141">Deploy with PowerShell</span></span>

<span data-ttu-id="c6766-142">Esse procedimento cria um cluster Hadoop no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c6766-142">This procedure creates a Hadoop cluster in HDInsight.</span></span>

1. <span data-ttu-id="c6766-143">Salve o arquivo JSON encontrado no [Apêndice](#appx-a-arm-template) em sua estação de trabalho.</span><span class="sxs-lookup"><span data-stu-id="c6766-143">Save the JSON file in the [Appendix](#appx-a-arm-template) to your workstation.</span></span> <span data-ttu-id="c6766-144">No script do PowerShell, o nome do arquivo é `C:\HDITutorials-ARM\hdinsight-arm-template.json`.</span><span class="sxs-lookup"><span data-stu-id="c6766-144">In the PowerShell script, the file name is `C:\HDITutorials-ARM\hdinsight-arm-template.json`.</span></span>
2. <span data-ttu-id="c6766-145">Defina as variáveis e os parâmetros, se necessário.</span><span class="sxs-lookup"><span data-stu-id="c6766-145">Set the parameters and variables if needed.</span></span>
3. <span data-ttu-id="c6766-146">Execute o modelo usando o seguinte script do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c6766-146">Run the template by using the following PowerShell script:</span></span>

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
        # Connect to Azure
        ####################################
        #region - Connect to Azure subscription
        Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
        try{Get-AzureRmContext}
        catch{Login-AzureRmAccount}
        #endregion

        # Create a resource group
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $Location

        # Create cluster and the dependent storage account
        $parameters = @{clusterName="$hdinsightClusterName"}

        New-AzureRmResourceGroupDeployment `
            -Name $armDeploymentName `
            -ResourceGroupName $resourceGroupName `
            -TemplateFile $templateFile `
            -TemplateParameterObject $parameters

        # List cluster
        Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName

    <span data-ttu-id="c6766-147">O script do PowerShell configura apenas o nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="c6766-147">The PowerShell script configures only the cluster name.</span></span> <span data-ttu-id="c6766-148">O nome da conta de armazenamento está embutido em código no modelo.</span><span class="sxs-lookup"><span data-stu-id="c6766-148">The storage account name is hard-coded in the template.</span></span> <span data-ttu-id="c6766-149">Será solicitado que você insira a senha de usuário do cluster.</span><span class="sxs-lookup"><span data-stu-id="c6766-149">You are prompted to enter the cluster user password.</span></span> <span data-ttu-id="c6766-150">(O nome de usuário padrão é **admin**.) Também será solicitado que você insira a senha de usuário SSH.</span><span class="sxs-lookup"><span data-stu-id="c6766-150">(The default username is **admin**.) You are also prompted to enter the SSH user password.</span></span> <span data-ttu-id="c6766-151">(O nome de usuário SSH padrão é **sshuser**.)</span><span class="sxs-lookup"><span data-stu-id="c6766-151">(The default SSH username is **sshuser**.)</span></span>  

<span data-ttu-id="c6766-152">Para obter mais informações, veja [Implantar com o PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span><span class="sxs-lookup"><span data-stu-id="c6766-152">For more information, see  [Deploy with PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy-local-template).</span></span>

## <a name="deploy-with-cli"></a><span data-ttu-id="c6766-153">Implantar com a CLI</span><span class="sxs-lookup"><span data-stu-id="c6766-153">Deploy with CLI</span></span>
<span data-ttu-id="c6766-154">O exemplo a seguir usa a CLI (interface de linha de comando) do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6766-154">The following sample uses Azure command-line interface (CLI).</span></span> <span data-ttu-id="c6766-155">Ele cria um cluster e os respectivos contêiner e conta de armazenamento dependente chamando um modelo do Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="c6766-155">It creates a cluster and its dependent storage account and container by calling a Resource Manager template:</span></span>

    azure login
    azure config mode arm
    azure group create -n hdi1229rg -l "East US"
    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "C:\HDITutorials-ARM\hdinsight-arm-template.json"

<span data-ttu-id="c6766-156">Será solicitado que você insira:</span><span class="sxs-lookup"><span data-stu-id="c6766-156">You are prompted to enter:</span></span>
* <span data-ttu-id="c6766-157">O nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="c6766-157">The cluster name.</span></span>
* <span data-ttu-id="c6766-158">A senha de usuário do cluster.</span><span class="sxs-lookup"><span data-stu-id="c6766-158">The cluster user password.</span></span> <span data-ttu-id="c6766-159">(O nome de usuário padrão é **admin**.)</span><span class="sxs-lookup"><span data-stu-id="c6766-159">(The default username is **admin**.)</span></span>
* <span data-ttu-id="c6766-160">A senha de usuário do SSH.</span><span class="sxs-lookup"><span data-stu-id="c6766-160">The SSH user password.</span></span> <span data-ttu-id="c6766-161">(O nome de usuário SSH padrão é **sshuser**.)</span><span class="sxs-lookup"><span data-stu-id="c6766-161">(The default SSH username is **sshuser**.)</span></span>

<span data-ttu-id="c6766-162">O código a seguir fornece parâmetros embutidos:</span><span class="sxs-lookup"><span data-stu-id="c6766-162">The following code provides inline parameters:</span></span>

    azure group deployment create --resource-group "hdi1229rg" --name "hdi1229" --template-file "c:\Tutorials\HDInsightARM\create-linux-based-hadoop-cluster-in-hdinsight.json" --parameters '{\"clusterName\":{\"value\":\"hdi1229\"},\"clusterLoginPassword\":{\"value\":\"Pass@word1\"},\"sshPassword\":{\"value\":\"Pass@word1\"}}'

## <a name="deploy-with-the-rest-api"></a><span data-ttu-id="c6766-163">Implantar com a API REST</span><span class="sxs-lookup"><span data-stu-id="c6766-163">Deploy with the REST API</span></span>
<span data-ttu-id="c6766-164">Veja [Implantar com a API REST](../azure-resource-manager/resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="c6766-164">See [Deploy with the REST API](../azure-resource-manager/resource-group-template-deploy-rest.md).</span></span>

## <a name="deploy-with-visual-studio"></a><span data-ttu-id="c6766-165">Implantação com o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c6766-165">Deploy with Visual Studio</span></span>
 <span data-ttu-id="c6766-166">Use o Visual Studio para criar um projeto do grupo de recursos e implantá-lo ao Azure por meio da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="c6766-166">Use Visual Studio to create a resource group project and deploy it to Azure through the user interface.</span></span> <span data-ttu-id="c6766-167">Selecione o tipo de recursos a serem incluídos em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="c6766-167">You select the type of resources to include in your project.</span></span> <span data-ttu-id="c6766-168">Esses recursos são adicionados automaticamente ao modelo do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c6766-168">Those resources are automatically added to the Resource Manager template.</span></span> <span data-ttu-id="c6766-169">O projeto também fornece um script do PowerShell para implantar o modelo.</span><span class="sxs-lookup"><span data-stu-id="c6766-169">The project also provides a PowerShell script to deploy the template.</span></span>

<span data-ttu-id="c6766-170">Para obter uma introdução ao uso do Visual Studio com grupos de recursos, veja [Criando e implantando grupos de recursos do Azure por meio do Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="c6766-170">For an introduction to using Visual Studio with resource groups, see [Creating and deploying Azure resource groups through Visual Studio](../azure-resource-manager/vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="c6766-171">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="c6766-171">Troubleshoot</span></span>

<span data-ttu-id="c6766-172">Se você tiver problemas com a criação de clusters HDInsight, confira os [requisitos de controle de acesso](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="c6766-172">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6766-173">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c6766-173">Next steps</span></span>
<span data-ttu-id="c6766-174">Neste artigo, você aprendeu várias maneiras de criar um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c6766-174">In this article, you have learned several ways to create an HDInsight cluster.</span></span> <span data-ttu-id="c6766-175">Para saber mais, consulte os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="c6766-175">To learn more, see the following articles:</span></span>

* <span data-ttu-id="c6766-176">Para obter um exemplo de como implantar recursos por meio da biblioteca de cliente do .NET, veja [Implantar recursos usando bibliotecas do .NET e um modelo](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c6766-176">For an example of deploying resources through the .NET client library, see [Deploy resources by using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="c6766-177">Para obter um exemplo detalhado de implantação de um aplicativo, confira [Provisionar e implantar microsserviços de forma previsível no Azure](../app-service-web/app-service-deploy-complex-application-predictably.md).</span><span class="sxs-lookup"><span data-stu-id="c6766-177">For an in-depth example of deploying an application, see [Provision and deploy microservices predictably in Azure](../app-service-web/app-service-deploy-complex-application-predictably.md).</span></span>
* <span data-ttu-id="c6766-178">Para obter orientação sobre como implantar a solução em ambientes diferentes, confira [Ambientes de desenvolvimento e de teste no Microsoft Azure](../solution-dev-test-environments.md).</span><span class="sxs-lookup"><span data-stu-id="c6766-178">For guidance on deploying your solution to different environments, see [Development and test environments in Microsoft Azure](../solution-dev-test-environments.md).</span></span>
* <span data-ttu-id="c6766-179">Para saber mais sobre as seções do modelo do Azure Resource Manager, veja [Criando modelos](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="c6766-179">To learn about the sections of the Azure Resource Manager template, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="c6766-180">Para obter uma lista das funções que podem ser usadas em um modelo do Azure Resource Manager, veja [Funções do modelo](../azure-resource-manager/resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="c6766-180">For a list of the functions you can use in an Azure Resource Manager template, see [Template functions](../azure-resource-manager/resource-group-template-functions.md).</span></span>

## <a name="appendix-resource-manager-template-to-create-a-hadoop-cluster"></a><span data-ttu-id="c6766-181">Apêndice: modelo do Resource Manager para criar um cluster Hadoop</span><span class="sxs-lookup"><span data-stu-id="c6766-181">Appendix: Resource Manager template to create a Hadoop cluster</span></span>
<span data-ttu-id="c6766-182">O modelo a seguir do Azure Resource Manager cria um cluster Hadoop baseado em Linux com a conta de armazenamento do Azure dependente.</span><span class="sxs-lookup"><span data-stu-id="c6766-182">The following Azure Resource Manager template creates a Linux-based Hadoop cluster with the dependent Azure storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="c6766-183">Este exemplo inclui informações de configuração para o metastore do Hive e o metastore do Oozie.</span><span class="sxs-lookup"><span data-stu-id="c6766-183">This sample includes configuration information for Hive metastore and Oozie metastore.</span></span> <span data-ttu-id="c6766-184">Remova a seção ou configure a seção antes de usar o modelo.</span><span class="sxs-lookup"><span data-stu-id="c6766-184">Remove the section or configure the section before using the template.</span></span>
>
>

    {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "clusterName": {
        "type": "string",
        "metadata": {
            "description": "The name of the HDInsight cluster to create."
        }
        },
        "clusterLoginUserName": {
        "type": "string",
        "defaultValue": "admin",
        "metadata": {
            "description": "These credentials can be used to submit jobs to the cluster and to log into cluster dashboards."
        }
        },
        "clusterLoginPassword": {
        "type": "securestring",
        "metadata": {
            "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
        }
        },
        "sshUserName": {
        "type": "string",
        "defaultValue": "sshuser",
        "metadata": {
            "description": "These credentials can be used to remotely access the cluster."
        }
        },
        "sshPassword": {
        "type": "securestring",
        "metadata": {
            "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
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
            "description": "The location where all azure resources will be deployed."
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
            "description": "The type of the HDInsight cluster to create."
        }
        },
        "clusterWorkerNodeCount": {
        "type": "int",
        "defaultValue": 2,
        "metadata": {
            "description": "The number of nodes in the HDInsight cluster."
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

## <a name="appendix-resource-manager-template-to-create-a-spark-cluster"></a><span data-ttu-id="c6766-185">Apêndice: modelo do Resource Manager para criar um cluster Spark</span><span class="sxs-lookup"><span data-stu-id="c6766-185">Appendix: Resource Manager template to create a Spark cluster</span></span>

<span data-ttu-id="c6766-186">Esta seção fornece um modelo do Azure Resource Manager que você pode usar para criar um cluster Spark do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c6766-186">This section provides a Resource Manager template that you can use to create an HDInsight Spark cluster.</span></span> <span data-ttu-id="c6766-187">Esse modelo inclui configurações para `spark-defaults` e `spark-thrift-sparkconf` (para clusters Spark 1.6) e `spark2-defaults` e `spark2-thrift-sparkconf` (para clusters Spark 2).</span><span class="sxs-lookup"><span data-stu-id="c6766-187">This template includes configurations for `spark-defaults` and `spark-thrift-sparkconf` (for Spark 1.6 clusters) and `spark2-defaults` and `spark2-thrift-sparkconf` (for Spark 2 clusters).</span></span> <span data-ttu-id="c6766-188">Além disso, o HDInsight calcula e define as configurações como `spark.executor.instances`, `spark.executor.memory` e `spark.executor.cores` com base no tamanho do cluster.</span><span class="sxs-lookup"><span data-stu-id="c6766-188">In addition to this, HDInsight calculates and sets configurations such as `spark.executor.instances`, `spark.executor.memory`, and `spark.executor.cores` based on the cluster size.</span></span> 

<span data-ttu-id="c6766-189">Se você definir qualquer parâmetro individual em uma seção como parte do modelo, HDInsight não calculará e definirá os outros parâmetros da mesma seção.</span><span class="sxs-lookup"><span data-stu-id="c6766-189">If you set any one parameter in a section as part of the template itself, HDInsight does not calculate and set the other parameters of the same section.</span></span> <span data-ttu-id="c6766-190">Por exemplo, o parâmetro `spark.executor.instances` está na configuração `spark-defaults`.</span><span class="sxs-lookup"><span data-stu-id="c6766-190">For example, parameter `spark.executor.instances` is in the  `spark-defaults` configuration.</span></span> <span data-ttu-id="c6766-191">Se você definir outro parâmetro (por exemplo, `spark.yarn.exector.memoryOverhead`) na configuração `spark-defaults`, o HDInsight não calculará nem definirá o parâmetro `spark.executor.instances` também.</span><span class="sxs-lookup"><span data-stu-id="c6766-191">If you set another parameter (for example, `spark.yarn.exector.memoryOverhead`) in the `spark-defaults` configuration, HDInsight does not calculate and set the `spark.executor.instances` parameter as well.</span></span>

    {
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "0.9.0.0",
    "parameters": {
        "clusterName": {
            "type": "string",
            "metadata": {
                "description": "The name of the HDInsight cluster to create."
            }
        },
        "clusterLoginUserName": {
            "type": "string",
            "defaultValue": "admin",
            "metadata": {
                "description": "These credentials can be used to submit jobs to the cluster and to log into cluster dashboards."
            }
        },
        "clusterLoginPassword": {
            "type": "securestring",
            "metadata": {
                "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
            }
        },
        "location": {
            "type": "string",
            "defaultValue": "southcentralus",
            "metadata": {
                "description": "The location where all azure resources will be deployed."
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
                "description": "The number of nodes in the HDInsight cluster."
            }
        },
        "clusterKind": {
            "type": "string",
            "defaultValue": "SPARK",
            "metadata": {
                "description": "The type of the HDInsight cluster to create."
            }
        },
        "sshUserName": {
            "type": "string",
            "defaultValue": "sshuser",
            "metadata": {
                "description": "These credentials can be used to remotely access the cluster."
            }
        },
        "sshPassword": {
            "type": "securestring",
            "metadata": {
                "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
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
