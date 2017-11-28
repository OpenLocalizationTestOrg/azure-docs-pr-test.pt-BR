---
title: "Usar nós de borda vazios em clusters Hadoop no HDInsight – Azure | Microsoft Docs"
description: "Como adicionar um nó de borda vazio a um cluster HDInsight que pode ser usado como um cliente e então testar/hospedar seus aplicativos de HDInsight."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: mumian
tags: azure-portal
documentationcenter: 
ms.assetid: cdc7d1b4-15d7-4d4d-a13f-c7d3a694b4fb
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jgao
ms.openlocfilehash: e21dabcc6999b1f1047d334e782f723d0c03c2cb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="use-empty-edge-nodes-on-hadoop-clusters-in-hdinsight"></a><span data-ttu-id="b9fb1-103">Usar nós de borda vazios em clusters Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="b9fb1-103">Use empty edge nodes on Hadoop clusters in HDInsight</span></span>

<span data-ttu-id="b9fb1-104">Saiba como adicionar um nó de borda vazio a um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-104">Learn how to add an empty edge node to an HDInsight cluster.</span></span> <span data-ttu-id="b9fb1-105">Um nó de borda vazio é uma máquina virtual do Linux com as mesmas ferramentas de cliente instaladas e configuradas como nos nós de cabeçalho, mas sem serviços do Hadoop em execução.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-105">An empty edge node is a Linux virtual machine with the same client tools installed and configured as in the headnodes, but with no Hadoop services running.</span></span> <span data-ttu-id="b9fb1-106">Você pode usar o nó de borda para acessar o cluster, testar e hospedar seus aplicativos clientes.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-106">You can use the edge node for accessing the cluster, testing your client applications, and hosting your client applications.</span></span> 

<span data-ttu-id="b9fb1-107">Você pode adicionar um nó de borda vazio a um cluster HDInsight existente ou a um novo cluster quando ele é criado.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-107">You can add an empty edge node to an existing HDInsight cluster, to a new cluster when you create the cluster.</span></span> <span data-ttu-id="b9fb1-108">A adição de um nó de borda vazio é feita usando o modelo Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-108">Adding an empty edge node is done using Azure Resource Manager template.</span></span>  <span data-ttu-id="b9fb1-109">O exemplo abaixo demonstra como isso é feito usando um modelo:</span><span class="sxs-lookup"><span data-stu-id="b9fb1-109">The following sample demonstrates how it is done using a template:</span></span>

    "resources": [
        {
            "name": "[concat(parameters('clusterName'),'/', variables('applicationName'))]",
            "type": "Microsoft.HDInsight/clusters/applications",
            "apiVersion": "2015-03-01-preview",
            "dependsOn": [ "[concat('Microsoft.HDInsight/clusters/',parameters('clusterName'))]" ],
            "properties": {
                "marketPlaceIdentifier": "EmptyNode",
                "computeProfile": {
                    "roles": [{
                        "name": "edgenode",
                        "targetInstanceCount": 1,
                        "hardwareProfile": {
                            "vmSize": "Standard_D3"
                        }
                    }]
                },
                "installScriptActions": [{
                    "name": "[concat('emptynode','-' ,uniquestring(variables('applicationName')))]",
                    "uri": "[parameters('installScriptAction')]",
                    "roles": ["edgenode"]
                }],
                "uninstallScriptActions": [],
                "httpsEndpoints": [],
                "applicationType": "CustomApplication"
            }
        }
    ],

<span data-ttu-id="b9fb1-110">Conforme mostrado no exemplo, você pode, opcionalmente, chamar uma [ação do script](hdinsight-hadoop-customize-cluster-linux.md) para executar configurações adicionais, como a instalação do [Apache Hue](hdinsight-hadoop-hue-linux.md) no nó de borda.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-110">As shown in the sample, you can optionally call a [script action](hdinsight-hadoop-customize-cluster-linux.md) to perform additional configuration, such as installing [Apache Hue](hdinsight-hadoop-hue-linux.md) in the edge node.</span></span> <span data-ttu-id="b9fb1-111">O script de ação de script deve ser publicamente acessível na Web.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-111">The script action script must be publicly accessible on the web.</span></span>  <span data-ttu-id="b9fb1-112">Por exemplo, se o script for armazenado no armazenamento do Azure, use contêineres públicos ou blobs públicos.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-112">For example, if the script is stored in Azure storage, use either public containers or public blobs.</span></span>

<span data-ttu-id="b9fb1-113">O tamanho de máquina virtual do nó de borda deve atender aos requisitos de tamanho de VM do nó de trabalho do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-113">The edge node virtual machine size must meet the HDInsight cluster worker node vm size requirements.</span></span> <span data-ttu-id="b9fb1-114">Para obter os tamanhos recomendados de VM do nó de trabalho, consulte [Criar clusters Hadoop no HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span><span class="sxs-lookup"><span data-stu-id="b9fb1-114">For the recommended worker node vm sizes, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span></span>

<span data-ttu-id="b9fb1-115">Depois de criar um nó de borda, você pode conectar-se a ele usando SSH e executar as ferramentas de cliente para acessar o cluster Hadoop no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-115">After you have created an edge node, you can connect to the edge node using SSH, and run client tools to access the Hadoop cluster in HDInsight.</span></span>

> [!WARNING] 
> <span data-ttu-id="b9fb1-116">O uso de um nó de borda vazio com HDInsight está atualmente em versão prévia.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-116">Using an empty edge node with HDInsight is currently in preview.</span></span> <span data-ttu-id="b9fb1-117">Componentes personalizados que são instalados no nó de borda recebem suporte comercialmente cabível da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-117">Custom components that are installed on the edge node receive commercially reasonable support from Microsoft.</span></span> <span data-ttu-id="b9fb1-118">Isso pode resultar na resolução de problemas encontrados.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-118">This might result in resolving problems you encounter.</span></span> <span data-ttu-id="b9fb1-119">Ou você pode receber referências de recursos da comunidade para obter assistência adicional.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-119">Or you may be referred to community resources for further assistance.</span></span> <span data-ttu-id="b9fb1-120">A seguir estão alguns dos sites mais ativos para obter ajuda da comunidade:</span><span class="sxs-lookup"><span data-stu-id="b9fb1-120">The following are some of the most active sites for getting help from the community:</span></span>
>
> * [<span data-ttu-id="b9fb1-121">Fórum do MSDN para HDInsight</span><span class="sxs-lookup"><span data-stu-id="b9fb1-121">MSDN forum for HDInsight</span></span>](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight)
> * <span data-ttu-id="b9fb1-122">[http://stackoverflow.com](http://stackoverflow.com).</span><span class="sxs-lookup"><span data-stu-id="b9fb1-122">[http://stackoverflow.com](http://stackoverflow.com).</span></span>
>
> <span data-ttu-id="b9fb1-123">Se você estiver usando uma tecnologia do Apache, você poderá encontrar sites de projetos de assistência por meio do Apache em [http://apache.org](http://apache.org), tais como o site do [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="b9fb1-123">If you are using an Apache technology, you may be able to find assistance through the Apache project sites on [http://apache.org](http://apache.org), such as the [Hadoop](http://hadoop.apache.org/) site.</span></span>

## <a name="add-an-edge-node-to-an-existing-cluster"></a><span data-ttu-id="b9fb1-124">Adicionar um nó de borda a um cluster existente</span><span class="sxs-lookup"><span data-stu-id="b9fb1-124">Add an edge node to an existing cluster</span></span>
<span data-ttu-id="b9fb1-125">Nesta seção, você pode usar um modelo do Resource Manager para adicionar um nó de borda a um cluster HDInsight existente.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-125">In this section, you use a Resource Manager template to add an edge node to an existing HDInsight cluster.</span></span>  <span data-ttu-id="b9fb1-126">O modelo do Resource Manager pode ser encontrado no [GitHub](https://azure.microsoft.com/en-us/resources/templates/101-hdinsight-linux-add-edge-node/).</span><span class="sxs-lookup"><span data-stu-id="b9fb1-126">The Resource Manager template can be found in [GitHub](https://azure.microsoft.com/en-us/resources/templates/101-hdinsight-linux-add-edge-node/).</span></span> <span data-ttu-id="b9fb1-127">O modelo do Resource Manager chama uma ação de script localizada em https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-add-edge-node/scripts/EmptyNodeSetup.sh. O script não realiza nenhuma ação.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-127">The Resource Manager template calls a script action located at https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-add-edge-node/scripts/EmptyNodeSetup.sh. The script doesn't perform any actions.</span></span>  <span data-ttu-id="b9fb1-128">Isso serve para demonstrar a chamada da ação de script de um modelo do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-128">It is to demonstrate calling script action from a Resource Manager template.</span></span>

<span data-ttu-id="b9fb1-129">**Para adicionar um nó de borda vazio a um cluster existente**</span><span class="sxs-lookup"><span data-stu-id="b9fb1-129">**To add an empty edge node to an existing cluster**</span></span>

1. <span data-ttu-id="b9fb1-130">Se você ainda não tem um, crie um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-130">Create an HDInsight cluster if you don't have one yet.</span></span>  <span data-ttu-id="b9fb1-131">Veja [Tutorial do Hadoop: Introdução ao uso do Hadoop no HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b9fb1-131">See [Hadoop tutorial: Get started using Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
2. <span data-ttu-id="b9fb1-132">Clique na imagem a seguir para entrar no Azure e abra o modelo do Azure Resource Manager no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-132">Click the following image to sign in to Azure and open the Azure Resource Manager template in the Azure portal.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-add-edge-node%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-use-edge-node/deploy-to-azure.png" alt="Deploy to Azure"></a>
3. <span data-ttu-id="b9fb1-133">Configure as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="b9fb1-133">Configure the following properties:</span></span>
   
   * <span data-ttu-id="b9fb1-134">**Assinatura**: selecione uma assinatura do Azure usada para criar esse cluster.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-134">**Subscription**: Select an Azure subscription used for creating the cluster.</span></span>
   * <span data-ttu-id="b9fb1-135">**Grupo de Recursos**: selecione o grupo de recursos usado para o cluster HDInsight existente.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-135">**Resource group**: Select the resource group used for the existing HDInsight cluster.</span></span>
   * <span data-ttu-id="b9fb1-136">**Localização**: Selecione a localização do cluster HDInsight existente.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-136">**Location**: Select the location of the existing HDInsight cluster.</span></span>
   * <span data-ttu-id="b9fb1-137">**Nome do Cluster**: insira o nome de um cluster HDInsight existente.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-137">**Cluster Name**: Enter the name of an existing HDInsight cluster.</span></span>
   * <span data-ttu-id="b9fb1-138">**Tamanho do Nó de Borda**: Selecione um dos tamanhos de VM.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-138">**Edge Node Size**: Select one of the VM sizes.</span></span> <span data-ttu-id="b9fb1-139">O tamanho de VM deve atender aos requisitos de tamanho de VM do nó de trabalho.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-139">The vm size must meet the worker node vm size requirements.</span></span> <span data-ttu-id="b9fb1-140">Para obter os tamanhos recomendados de VM do nó de trabalho, consulte [Criar clusters Hadoop no HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span><span class="sxs-lookup"><span data-stu-id="b9fb1-140">For the recommended worker node vm sizes, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span></span>
   * <span data-ttu-id="b9fb1-141">**Prefixo do Nó de Borda**: O valor padrão é **novo**.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-141">**Edge Node Prefix**: The default value is **new**.</span></span>  <span data-ttu-id="b9fb1-142">Usando o valor padrão, o nome do nó de borda é **new-edgenode**.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-142">Using the default value, the edge node name is **new-edgenode**.</span></span>  <span data-ttu-id="b9fb1-143">Você pode personalizar o prefixo no portal.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-143">You can customize the prefix from the portal.</span></span> <span data-ttu-id="b9fb1-144">Você também pode personalizar o nome completo no modelo.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-144">You can also customize the full name from the template.</span></span>

4. <span data-ttu-id="b9fb1-145">Selecione **Concordo com os termos e condições declarados acima** e clique em **Comprar** para criar um nó de borda.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-145">Check **I agree to the terms and conditions stated above**, and then click  **Purchase** to create the edge node.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="b9fb1-146">Certifique-se de selecionar o grupo de recursos do Azure para o cluster HDInsight existente.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-146">Make sure to select the Azure resource group for the existing HDInsight cluster.</span></span>  <span data-ttu-id="b9fb1-147">Caso contrário, você receberá a mensagem de erro "Não é possível executar a operação solicitada no recurso aninhado.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-147">Otherwise, you get the error message "Can not perform requested operation on nested resource.</span></span> <span data-ttu-id="b9fb1-148">Recurso pai '&lt;NomeDoCluster>' não encontrado".</span><span class="sxs-lookup"><span data-stu-id="b9fb1-148">Parent resource '&lt;ClusterName>' not found."</span></span>

## <a name="add-an-edge-node-when-creating-a-cluster"></a><span data-ttu-id="b9fb1-149">Adicionar um nó de borda ao criar um cluster</span><span class="sxs-lookup"><span data-stu-id="b9fb1-149">Add an edge node when creating a cluster</span></span>
<span data-ttu-id="b9fb1-150">Nesta seção, você pode usar um modelo do Resource Manager para criar um cluster HDInsight com um nó de borda.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-150">In this section, you use a Resource Manager template to create HDInsight cluster with an edge node.</span></span>  <span data-ttu-id="b9fb1-151">O modelo do Resource Manager pode ser encontrado em [Galeria de Modelos de Início Rápido do Azure](https://azure.microsoft.com/documentation/templates/101-hdinsight-linux-with-edge-node/).</span><span class="sxs-lookup"><span data-stu-id="b9fb1-151">The Resource Manager template can be found in the [Azure QuickStart Templates gallery](https://azure.microsoft.com/documentation/templates/101-hdinsight-linux-with-edge-node/).</span></span> <span data-ttu-id="b9fb1-152">O modelo do Resource Manager chama um script de ação localizado em https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-with-edge-node/scripts/EmptyNodeSetup.sh. O script não realiza nenhuma ação.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-152">The Resource Manager template calls a script action located at https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-with-edge-node/scripts/EmptyNodeSetup.sh. The script doesn't perform any actions.</span></span>  <span data-ttu-id="b9fb1-153">Isso serve para demonstrar a chamada da ação de script de um modelo do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-153">It is to demonstrate calling script action from a Resource Manager template.</span></span>

<span data-ttu-id="b9fb1-154">**Para adicionar um nó de borda vazio a um cluster existente**</span><span class="sxs-lookup"><span data-stu-id="b9fb1-154">**To add an empty edge node to an existing cluster**</span></span>

1. <span data-ttu-id="b9fb1-155">Se você ainda não tem um, crie um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-155">Create an HDInsight cluster if you don't have one yet.</span></span>  <span data-ttu-id="b9fb1-156">Veja [Introdução ao uso do Hadoop no HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b9fb1-156">See [Get started using Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
2. <span data-ttu-id="b9fb1-157">Clique na imagem a seguir para entrar no Azure e abra o modelo do Azure Resource Manager no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-157">Click the following image to sign in to Azure and open the Azure Resource Manager template in the Azure portal.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-edge-node%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-use-edge-node/deploy-to-azure.png" alt="Deploy to Azure"></a>
3. <span data-ttu-id="b9fb1-158">Configure as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="b9fb1-158">Configure the following properties:</span></span>
   
   * <span data-ttu-id="b9fb1-159">**Assinatura**: selecione uma assinatura do Azure usada para criar esse cluster.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-159">**Subscription**: Select an Azure subscription used for creating the cluster.</span></span>
   * <span data-ttu-id="b9fb1-160">**Grupo de Recursos**: Criar um novo grupo de recursos usado para o cluster.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-160">**Resource group**: Create a new resource group used for the cluster.</span></span>
   * <span data-ttu-id="b9fb1-161">**Local**: selecione um local para o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-161">**Location**: Select a location for the resource group.</span></span>
   * <span data-ttu-id="b9fb1-162">**Nome do Cluster**: insira um nome para o novo cluster a ser criado.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-162">**Cluster Name**: Enter a name for the new cluster to create.</span></span>
   * <span data-ttu-id="b9fb1-163">**Nome de Usuário de Logon do Cluster** : insira o nome de usuário HTTP do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-163">**Cluster Login User Name**: Enter the Hadoop HTTP user name.</span></span>  <span data-ttu-id="b9fb1-164">O nome padrão é **admin**.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-164">The default name is **admin**.</span></span>
   * <span data-ttu-id="b9fb1-165">**Senha de Logon do Cluster**: digite a senha do usuário HTTP do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-165">**Cluster Login Password**: Enter the Hadoop HTTP user password.</span></span>
   * <span data-ttu-id="b9fb1-166">**Nome de Usuário Ssh**: digite o nome de usuário SSH.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-166">**Ssh User Name**: Enter the SSH user name.</span></span> <span data-ttu-id="b9fb1-167">O nome padrão é **sshuser**.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-167">The default name is **sshuser**.</span></span>
   * <span data-ttu-id="b9fb1-168">**Senha do Ssh**: digite a senha de usuário do SSH.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-168">**Ssh Password**: Enter the SSH user password.</span></span>
   * <span data-ttu-id="b9fb1-169">**Instalar ação do script**: manter o valor padrão para percorrer este tutorial.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-169">**Install Script Action**: Keep the default value for going through this tutorial.</span></span>
     
     <span data-ttu-id="b9fb1-170">Algumas propriedades foram embutidas no código do modelo: tipo de Cluster, contagem de nós de trabalho do Cluster, tamanho do nó de borda e nome do nó de borda.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-170">Some properties have been hardcoded in the template: Cluster type, Cluster worker node count, Edge node size, and Edge node name.</span></span>
4. <span data-ttu-id="b9fb1-171">Selecione **Concordo com os termos e condições declarados acima** e clique em **Comprar** para criar um cluster com nó de borda.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-171">Check **I agree to the terms and conditions stated above**, and then click  **Purchase** to create the cluster with the edge node.</span></span>

## <a name="access-an-edge-node"></a><span data-ttu-id="b9fb1-172">Acessar um nó de borda</span><span class="sxs-lookup"><span data-stu-id="b9fb1-172">Access an edge node</span></span>
<span data-ttu-id="b9fb1-173">O ponto de extremidade SSH do nó de borda é &lt;EdgeNodeName>.&lt;ClusterName>-ssh.azurehdinsight.net:22.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-173">The edge node ssh endpoint is &lt;EdgeNodeName>.&lt;ClusterName>-ssh.azurehdinsight.net:22.</span></span>  <span data-ttu-id="b9fb1-174">Por exemplo, new-edgenode.myedgenode0914-ssh.azurehdinsight.net:22.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-174">For example, new-edgenode.myedgenode0914-ssh.azurehdinsight.net:22.</span></span>

<span data-ttu-id="b9fb1-175">O nó de borda aparece como um aplicativo no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-175">The edge node appears as an application on the Azure portal.</span></span>  <span data-ttu-id="b9fb1-176">O portal fornece as informações para acessar o nó de borda usando o SSH.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-176">The portal gives you the information to access the edge node using SSH.</span></span>

<span data-ttu-id="b9fb1-177">**Para verificar o ponto de extremidade SSH do nó de borda**</span><span class="sxs-lookup"><span data-stu-id="b9fb1-177">**To verify the edge node SSH endpoint**</span></span>

1. <span data-ttu-id="b9fb1-178">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b9fb1-178">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b9fb1-179">Abra o cluster HDInsight com um nó de borda.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-179">Open the HDInsight cluster with an edge node.</span></span>
3. <span data-ttu-id="b9fb1-180">Clique em **Aplicativos** na folha do cluster.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-180">Click **Applications** from the cluster blade.</span></span> <span data-ttu-id="b9fb1-181">Você verá o nó de borda.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-181">You shall see the edge node.</span></span>  <span data-ttu-id="b9fb1-182">O nome padrão é **new-edgenode**.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-182">The default name is **new-edgenode**.</span></span>
4. <span data-ttu-id="b9fb1-183">Clique no nó de borda.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-183">Click the edge node.</span></span> <span data-ttu-id="b9fb1-184">Você deverá ver o ponto de extremidade SSH.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-184">You shall see the SSH endpoint.</span></span>

<span data-ttu-id="b9fb1-185">**Para usar o Hive no nó de borda**</span><span class="sxs-lookup"><span data-stu-id="b9fb1-185">**To use Hive on the edge node**</span></span>

1. <span data-ttu-id="b9fb1-186">Use SSH para conectar-se ao nó de borda.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-186">Use SSH to connect to the edge node.</span></span> <span data-ttu-id="b9fb1-187">Para saber mais, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="b9fb1-187">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="b9fb1-188">Depois que você tiver se conectado ao nó de borda usando o SSH, use o seguinte comando para abrir o console do Hive:</span><span class="sxs-lookup"><span data-stu-id="b9fb1-188">After you have connected to the edge node using SSH, use the following command to open the Hive console:</span></span>
   
        hive
3. <span data-ttu-id="b9fb1-189">Execute o seguinte comando para mostrar as tabelas de Hive no cluster:</span><span class="sxs-lookup"><span data-stu-id="b9fb1-189">Run the following command to show Hive tables in the cluster:</span></span>
   
        show tables;

## <a name="delete-an-edge-node"></a><span data-ttu-id="b9fb1-190">Excluir um nó de borda</span><span class="sxs-lookup"><span data-stu-id="b9fb1-190">Delete an edge node</span></span>
<span data-ttu-id="b9fb1-191">Você pode excluir um nó de borda no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-191">You can delete an edge node from the Azure portal.</span></span>

<span data-ttu-id="b9fb1-192">**Para acessar um nó de borda**</span><span class="sxs-lookup"><span data-stu-id="b9fb1-192">**To access an edge node**</span></span>

1. <span data-ttu-id="b9fb1-193">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b9fb1-193">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b9fb1-194">Abra o cluster HDInsight com um nó de borda.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-194">Open the HDInsight cluster with an edge node.</span></span>
3. <span data-ttu-id="b9fb1-195">Clique em **Aplicativos** na folha do cluster.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-195">Click **Applications** from the cluster blade.</span></span> <span data-ttu-id="b9fb1-196">Você verá uma lista de nós de borda.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-196">You shall see a list of edge nodes.</span></span>  
4. <span data-ttu-id="b9fb1-197">Clique no nó de borda que deseja excluir e clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-197">Right-click the edge node you want to delete, and then click **Delete**.</span></span>
5. <span data-ttu-id="b9fb1-198">Clique em **Sim** para confirmar.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-198">Click **Yes** to confirm.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b9fb1-199">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b9fb1-199">Next steps</span></span>
<span data-ttu-id="b9fb1-200">Neste artigo, você aprendeu como adicionar um nó de borda e como acessar o nó de borda.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-200">In this article, you have learned how to add an edge node and how to access the edge node.</span></span> <span data-ttu-id="b9fb1-201">Para saber mais, consulte os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="b9fb1-201">To learn more, see the following articles:</span></span>

* <span data-ttu-id="b9fb1-202">[Instalar aplicativos do HDInsight](hdinsight-apps-install-applications.md): saiba como instalar um aplicativo do HDInsight em seus clusters.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-202">[Install HDInsight applications](hdinsight-apps-install-applications.md): Learn how to install an HDInsight application to your clusters.</span></span>
* <span data-ttu-id="b9fb1-203">[Instalar aplicativos personalizados do HDInsight](hdinsight-apps-install-custom-applications.md): saiba como implantar um aplicativo do HDInsight não publicado no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-203">[Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md): learn how to deploy an unpublished HDInsight application to HDInsight.</span></span>
* <span data-ttu-id="b9fb1-204">[Publicar aplicativos do HDInsight](hdinsight-apps-publish-applications.md): saiba como publicar seus aplicativos personalizados do HDInsight no Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-204">[Publish HDInsight applications](hdinsight-apps-publish-applications.md): Learn how to publish your custom HDInsight applications to Azure Marketplace.</span></span>
* <span data-ttu-id="b9fb1-205">[MSDN: instalar um aplicativo do HDInsight](https://msdn.microsoft.com/library/mt706515.aspx): saiba como definir aplicativos do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-205">[MSDN: Install an HDInsight application](https://msdn.microsoft.com/library/mt706515.aspx): Learn how to define HDInsight applications.</span></span>
* <span data-ttu-id="b9fb1-206">[Personalizar clusters HDInsight baseados em Linux usando a Ação de Script](hdinsight-hadoop-customize-cluster-linux.md): saiba como usar a Ação de Script para instalar aplicativos adicionais.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-206">[Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md): learn how to use Script Action to install additional applications.</span></span>
* <span data-ttu-id="b9fb1-207">[Personalizar clusters Hadoop baseados em Linux no HDInsight usando modelos do Resource Manager](hdinsight-hadoop-create-linux-clusters-arm-templates.md): saiba como chamar modelos do Resource Manager para criar clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b9fb1-207">[Create Linux-based Hadoop clusters in HDInsight using Resource Manager templates](hdinsight-hadoop-create-linux-clusters-arm-templates.md): learn how to call Resource Manager templates to create HDInsight clusters.</span></span>

