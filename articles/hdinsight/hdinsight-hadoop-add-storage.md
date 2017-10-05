---
title: Adicionar outras contas de armazenamento do Azure ao HDInsight | Microsoft Docs
description: Saiba como adicionar outras contas de armazenamento do Azure a um cluster existente do HDInsight.
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/04/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 0853e8605e07c28867676e9c13b89263ade67c88
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="add-additional-storage-accounts-to-hdinsight"></a><span data-ttu-id="cf01f-103">Adicionar outras contas de armazenamento ao HDInsight</span><span class="sxs-lookup"><span data-stu-id="cf01f-103">Add additional storage accounts to HDInsight</span></span>

<span data-ttu-id="cf01f-104">Saiba como usar ações de script para adicionar outras contas de armazenamento do Azure para o HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cf01f-104">Learn how to use script actions to add additional Azure storage accounts to HDInsight.</span></span> <span data-ttu-id="cf01f-105">As etapas neste documento adicionam uma conta de armazenamento a um cluster HDInsight baseado em Linux existente.</span><span class="sxs-lookup"><span data-stu-id="cf01f-105">The steps in this document add a storage account to an existing Linux-based HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cf01f-106">As informações neste documento mostram como adicionar mais armazenamento a um cluster após sua criação.</span><span class="sxs-lookup"><span data-stu-id="cf01f-106">The information in this document is about adding additional storage to a cluster after it has been created.</span></span> <span data-ttu-id="cf01f-107">Para saber mais sobre como adicionar contas de armazenamento durante a criação do cluster, veja [Configurar clusters no HDInsight com Hadoop, Spark, Kafka e muito mais](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="cf01f-107">For information on adding storage accounts during cluster creation, see [Set up clusters in HDInsight with Hadoop, Spark, Kafka, and more](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="how-it-works"></a><span data-ttu-id="cf01f-108">Como ele funciona</span><span class="sxs-lookup"><span data-stu-id="cf01f-108">How it works</span></span>

<span data-ttu-id="cf01f-109">Este script usa os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="cf01f-109">This script takes the following parameters:</span></span>

* <span data-ttu-id="cf01f-110">__Nome da conta de armazenamento do Azure__: o nome da conta de armazenamento a ser adicionada ao cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cf01f-110">__Azure storage account name__: The name of the storage account to add to the HDInsight cluster.</span></span> <span data-ttu-id="cf01f-111">Após a execução do script, o HDInsight pode ler e gravar dados armazenados nessa conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="cf01f-111">After running the script, HDInsight can read and write data stored in this storage account.</span></span>

* <span data-ttu-id="cf01f-112">__Chave da conta de armazenamento do Azure__: uma chave que concede acesso à conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="cf01f-112">__Azure storage account key__: A key that grants access to the storage account.</span></span>

* <span data-ttu-id="cf01f-113">__-p__ (opcional): se for especificado, a chave não será criptografada e armazenada no arquivo core-site.xml como texto sem formatação.</span><span class="sxs-lookup"><span data-stu-id="cf01f-113">__-p__ (optional): If specified, the key is not encrypted and is stored in the core-site.xml file as plain text.</span></span>

<span data-ttu-id="cf01f-114">Durante o processamento, o script executa as ações a seguir:</span><span class="sxs-lookup"><span data-stu-id="cf01f-114">During processing, the script performs the following actions:</span></span>

* <span data-ttu-id="cf01f-115">Se a conta de armazenamento já existir na configuração de core-site.xml do cluster, o script será encerrado e nenhuma ação será executada.</span><span class="sxs-lookup"><span data-stu-id="cf01f-115">If the storage account already exists in the core-site.xml configuration for the cluster, the script exits and no further actions are performed.</span></span>

* <span data-ttu-id="cf01f-116">Verifica se a conta de armazenamento existe e se pode ser acessada usando a chave.</span><span class="sxs-lookup"><span data-stu-id="cf01f-116">Verifies that the storage account exists and can be accessed using the key.</span></span>

* <span data-ttu-id="cf01f-117">Criptografa a chave usando a credencial do cluster.</span><span class="sxs-lookup"><span data-stu-id="cf01f-117">Encrypts the key using the cluster credential.</span></span>

* <span data-ttu-id="cf01f-118">Adiciona a conta de armazenamento ao arquivo core-site.xml.</span><span class="sxs-lookup"><span data-stu-id="cf01f-118">Adds the storage account to the core-site.xml file.</span></span>

* <span data-ttu-id="cf01f-119">Interrompe e reinicia os serviços do Oozie, YARN, MapReduce2 e HDFS.</span><span class="sxs-lookup"><span data-stu-id="cf01f-119">Stops and restarts the Oozie, YARN, MapReduce2, and HDFS services.</span></span> <span data-ttu-id="cf01f-120">Interromper e iniciar esses serviços permite que eles usem a nova conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="cf01f-120">Stopping and starting these services allows them to use the new storage account.</span></span>

> [!WARNING]
> <span data-ttu-id="cf01f-121">Não há suporte para o uso de uma conta de armazenamento em um local diferente do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cf01f-121">Using a storage account in a different location than the HDInsight cluster is not supported.</span></span>

## <a name="the-script"></a><span data-ttu-id="cf01f-122">O script</span><span class="sxs-lookup"><span data-stu-id="cf01f-122">The script</span></span>

<span data-ttu-id="cf01f-123">__Local do script__: [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)</span><span class="sxs-lookup"><span data-stu-id="cf01f-123">__Script location__: [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)</span></span>

<span data-ttu-id="cf01f-124">__Requisitos__:</span><span class="sxs-lookup"><span data-stu-id="cf01f-124">__Requirements__:</span></span>

* <span data-ttu-id="cf01f-125">O script deve ser aplicado sobre os __Nós de cabeça__.</span><span class="sxs-lookup"><span data-stu-id="cf01f-125">The script must be applied on the __Head nodes__.</span></span>

## <a name="to-use-the-script"></a><span data-ttu-id="cf01f-126">Para usar o script</span><span class="sxs-lookup"><span data-stu-id="cf01f-126">To use the script</span></span>

<span data-ttu-id="cf01f-127">Você pode usar o script por meio do Portal do Azure, do Azure PowerShell ou da CLI do Azure 1.0.</span><span class="sxs-lookup"><span data-stu-id="cf01f-127">This script can be used from the Azure portal, Azure PowerShell, or the Azure CLI 1.0.</span></span> <span data-ttu-id="cf01f-128">Para obter informações, veja o documento [Personalizar clusters HDInsight baseados em Linux usando a ação de script](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster).</span><span class="sxs-lookup"><span data-stu-id="cf01f-128">For more information, see the [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cf01f-129">Ao usar as etapas fornecidas no documento de personalização, use as informações a seguir para aplicar esse script:</span><span class="sxs-lookup"><span data-stu-id="cf01f-129">When using the steps provided in the customization document, use the following information to apply this script:</span></span>
>
> * <span data-ttu-id="cf01f-130">Substitua qualquer exemplo de URI de ação de script pelo URI desse script (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh).</span><span class="sxs-lookup"><span data-stu-id="cf01f-130">Replace any example script action URI with the URI for this script (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh).</span></span>
> * <span data-ttu-id="cf01f-131">Substitua quaisquer parâmetros de exemplo pelo nome da conta de armazenamento do Azure e pela chave da conta de armazenamento a ser adicionada ao cluster.</span><span class="sxs-lookup"><span data-stu-id="cf01f-131">Replace any example parameters with the Azure storage account name and key of the storage account to be added to the cluster.</span></span> <span data-ttu-id="cf01f-132">Se você usar o Portal do Azure, esses parâmetros deverão ser separados por um espaço.</span><span class="sxs-lookup"><span data-stu-id="cf01f-132">If using the Azure portal, these parameters must be separated by a space.</span></span>
> * <span data-ttu-id="cf01f-133">Não é necessário marcar esse script como __Persistido__, pois ele atualiza diretamente a configuração do Ambari para o cluster.</span><span class="sxs-lookup"><span data-stu-id="cf01f-133">You do not need to mark this script as __Persisted__, as it directly updates the Ambari configuration for the cluster.</span></span>

## <a name="known-issues"></a><span data-ttu-id="cf01f-134">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="cf01f-134">Known issues</span></span>

### <a name="storage-accounts-not-displayed-in-azure-portal-or-tools"></a><span data-ttu-id="cf01f-135">Contas de armazenamento não exibidas no Portal do Azure ou nas ferramentas</span><span class="sxs-lookup"><span data-stu-id="cf01f-135">Storage accounts not displayed in Azure portal or tools</span></span>

<span data-ttu-id="cf01f-136">Ao exibir o cluster HDInsight no portal do Azure, a seleção da entrada __Contas de Armazenamento__ em __Propriedades__ não exibe as contas de armazenamento adicionadas por meio dessa ação de script.</span><span class="sxs-lookup"><span data-stu-id="cf01f-136">When viewing the HDInsight cluster in the Azure portal, selecting the __Storage Accounts__ entry under __Properties__ does not display storage accounts added through this script action.</span></span> <span data-ttu-id="cf01f-137">O Azure PowerShell e a CLI do Azure também não exibem a conta de armazenamento adicional.</span><span class="sxs-lookup"><span data-stu-id="cf01f-137">Azure PowerShell and Azure CLI do not display the additional storage account either.</span></span>

<span data-ttu-id="cf01f-138">As informações de armazenamento não são exibidas porque o script modifica apenas a configuração core-site.xml para o cluster.</span><span class="sxs-lookup"><span data-stu-id="cf01f-138">The storage information isn't displayed because the script only modifies the core-site.xml configuration for the cluster.</span></span> <span data-ttu-id="cf01f-139">Essas informações não são usadas na recuperação das informações de cluster usando as APIs de gerenciamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="cf01f-139">This information is not used when retrieving the cluster information using Azure management APIs.</span></span>

<span data-ttu-id="cf01f-140">Para exibir informações da conta de armazenamento adicionadas ao cluster usando esse script, use a API REST do Ambari.</span><span class="sxs-lookup"><span data-stu-id="cf01f-140">To view storage account information added to the cluster using this script, use the Ambari REST API.</span></span> <span data-ttu-id="cf01f-141">Use os seguintes comandos para recuperar essas informações para seu cluster:</span><span class="sxs-lookup"><span data-stu-id="cf01f-141">Use the following commands to retrieve this information for your cluster:</span></span>

```PowerShell
$creds = Get-Credential -UserName "admin" -Message "Enter the cluster login credentials"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties."fs.azure.account.key.$storageAccountName.blob.core.windows.net"
```

> [!NOTE]
> <span data-ttu-id="cf01f-142">Defina `$clusterName` como o nome do cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cf01f-142">Set `$clusterName` to the name of the HDInsight cluster.</span></span> <span data-ttu-id="cf01f-143">Defina `$storageAccountName` como o nome da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="cf01f-143">Set `$storageAccountName` to the name of the storage account.</span></span> <span data-ttu-id="cf01f-144">Quando solicitado, insira a senha e o logon do cluster (admin).</span><span class="sxs-lookup"><span data-stu-id="cf01f-144">When prompted, enter the cluster login (admin) and password.</span></span>

```Bash
curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.azure.account.key.$STORAGEACCOUNTNAME.blob.core.windows.net"] | select(. != null)'
```

> [!NOTE]
> <span data-ttu-id="cf01f-145">Defina `$PASSWORD` como a senha de conta de logon do cluster (admin).</span><span class="sxs-lookup"><span data-stu-id="cf01f-145">Set `$PASSWORD` to the cluster login (admin) account password.</span></span> <span data-ttu-id="cf01f-146">Defina `$CLUSTERNAME` como o nome do cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cf01f-146">Set `$CLUSTERNAME` to the name of the HDInsight cluster.</span></span> <span data-ttu-id="cf01f-147">Defina `$STORAGEACCOUNTNAME` como o nome da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="cf01f-147">Set `$STORAGEACCOUNTNAME` to the name of the storage account.</span></span>
>
> <span data-ttu-id="cf01f-148">Esse exemplo usa [curl (http://curl.haxx.se/)](http://curl.haxx.se/) e [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) para recuperar e analisar dados de JSON.</span><span class="sxs-lookup"><span data-stu-id="cf01f-148">This example uses [curl (http://curl.haxx.se/)](http://curl.haxx.se/) and [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) to retrieve and parse JSON data.</span></span>

<span data-ttu-id="cf01f-149">Ao usar esse comando, substitua __NOMEDOCLUSTER__ pelo nome do cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cf01f-149">When using this command, replace __CLUSTERNAME__ with the name of the HDInsight cluster.</span></span> <span data-ttu-id="cf01f-150">Substitua __SENHA__ pela senha de logon HTTP do cluster.</span><span class="sxs-lookup"><span data-stu-id="cf01f-150">Replace __PASSWORD__ with the HTTP login password for the cluster.</span></span> <span data-ttu-id="cf01f-151">Substitua __STORAGEACCOUNT__ pelo nome da conta de armazenamento adicionada usando a ação de script.</span><span class="sxs-lookup"><span data-stu-id="cf01f-151">Replace __STORAGEACCOUNT__ with the name of the storage account added using script action.</span></span> <span data-ttu-id="cf01f-152">As informações que retornam desse comando são semelhantes ao texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="cf01f-152">Information returned from this command appears similar to the following text:</span></span>

    "MIIB+gYJKoZIhvcNAQcDoIIB6zCCAecCAQAxggFaMIIBVgIBADA+MCoxKDAmBgNVBAMTH2RiZW5jcnlwdGlvbi5henVyZWhkaW5zaWdodC5uZXQCEA6GDZMW1oiESKFHFOOEgjcwDQYJKoZIhvcNAQEBBQAEggEATIuO8MJ45KEQAYBQld7WaRkJOWqaCLwFub9zNpscrquA2f3o0emy9Vr6vu5cD3GTt7PmaAF0pvssbKVMf/Z8yRpHmeezSco2y7e9Qd7xJKRLYtRHm80fsjiBHSW9CYkQwxHaOqdR7DBhZyhnj+DHhODsIO2FGM8MxWk4fgBRVO6CZ5eTmZ6KVR8wYbFLi8YZXb7GkUEeSn2PsjrKGiQjtpXw1RAyanCagr5vlg8CicZg1HuhCHWf/RYFWM3EBbVz+uFZPR3BqTgbvBhWYXRJaISwssvxotppe0ikevnEgaBYrflB2P+PVrwPTZ7f36HQcn4ifY1WRJQ4qRaUxdYEfzCBgwYJKoZIhvcNAQcBMBQGCCqGSIb3DQMHBAhRdscgRV3wmYBg3j/T1aEnO3wLWCRpgZa16MWqmfQPuansKHjLwbZjTpeirqUAQpZVyXdK/w4gKlK+t1heNsNo1Wwqu+Y47bSAX1k9Ud7+Ed2oETDI7724IJ213YeGxvu4Ngcf2eHW+FRK"

<span data-ttu-id="cf01f-153">Esse texto é um exemplo de uma chave criptografada, que é usada para acessar a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="cf01f-153">This text is an example of an encrypted key, which is used to access the storage account.</span></span>

### <a name="unable-to-access-storage-after-changing-key"></a><span data-ttu-id="cf01f-154">Não é possível acessar o armazenamento após a alteração da chave</span><span class="sxs-lookup"><span data-stu-id="cf01f-154">Unable to access storage after changing key</span></span>

<span data-ttu-id="cf01f-155">Se você alterar a chave de uma conta de armazenamento, o HDInsight não poderá mais acessar a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="cf01f-155">If you change the key for a storage account, HDInsight can no longer access the storage account.</span></span> <span data-ttu-id="cf01f-156">O HDInsight usa uma cópia em cache da chave no core-site.xml do cluster.</span><span class="sxs-lookup"><span data-stu-id="cf01f-156">HDInsight uses a cached copy of key in the core-site.xml for the cluster.</span></span> <span data-ttu-id="cf01f-157">Essa cópia armazenada em cache deve ser atualizada para corresponder à nova chave.</span><span class="sxs-lookup"><span data-stu-id="cf01f-157">This cached copy must be updated to match the new key.</span></span>

<span data-ttu-id="cf01f-158">Executar a ação de script novamente __não__ atualiza a chave, pois o script verifica se já existe alguma entrada para a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="cf01f-158">Running the script action again does __not__ update the key, as the script checks to see if an entry for the storage account already exists.</span></span> <span data-ttu-id="cf01f-159">Se já houver uma entrada, ele não fará alterações.</span><span class="sxs-lookup"><span data-stu-id="cf01f-159">If an entry already exists, it does not make any changes.</span></span>

<span data-ttu-id="cf01f-160">Para contornar esse problema, remova a entrada existente da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="cf01f-160">To work around this problem, you must remove the existing entry for the storage account.</span></span> <span data-ttu-id="cf01f-161">Use as seguintes etapas para remover a entrada existente:</span><span class="sxs-lookup"><span data-stu-id="cf01f-161">Use the following steps to remove the existing entry:</span></span>

1. <span data-ttu-id="cf01f-162">Em um navegador da Web, abra a interface de usuário na Web do Ambari para seu cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cf01f-162">In a web browser, open the Ambari Web UI for your HDInsight cluster.</span></span> <span data-ttu-id="cf01f-163">O URI é https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="cf01f-163">The URI is https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="cf01f-164">Substitua __CLUSTERNAME__ pelo nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="cf01f-164">Replace __CLUSTERNAME__ with the name of your cluster.</span></span>

    <span data-ttu-id="cf01f-165">Quando receber a solicitação, insira o usuário e a senha de logon HTTP para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="cf01f-165">When prompted, enter the HTTP login user and password for your cluster.</span></span>

2. <span data-ttu-id="cf01f-166">Na lista de serviços à esquerda da página, selecione __HDFS__.</span><span class="sxs-lookup"><span data-stu-id="cf01f-166">From the list of services on the left of the page, select __HDFS__.</span></span> <span data-ttu-id="cf01f-167">Em seguida, selecione a guia __Configurações__ no centro da página.</span><span class="sxs-lookup"><span data-stu-id="cf01f-167">Then select the __Configs__ tab in the center of the page.</span></span>

3. <span data-ttu-id="cf01f-168">No campo __Filtrar...__, insira um valor de __fs.azure.account__.</span><span class="sxs-lookup"><span data-stu-id="cf01f-168">In the __Filter...__ field, enter a value of __fs.azure.account__.</span></span> <span data-ttu-id="cf01f-169">Isso retorna entradas para quaisquer outras contas de armazenamento que foram adicionadas ao cluster.</span><span class="sxs-lookup"><span data-stu-id="cf01f-169">This returns entries for any additional storage accounts that have been added to the cluster.</span></span> <span data-ttu-id="cf01f-170">Há dois tipos de entradas; __keyprovider__ e __key__.</span><span class="sxs-lookup"><span data-stu-id="cf01f-170">There are two types of entries; __keyprovider__ and __key__.</span></span> <span data-ttu-id="cf01f-171">Ambas contêm o nome da conta de armazenamento como parte do nome da chave.</span><span class="sxs-lookup"><span data-stu-id="cf01f-171">Both contain the name of the storage account as part of the key name.</span></span>

    <span data-ttu-id="cf01f-172">Veja a seguir exemplos de entradas para uma conta de armazenamento chamada __mystorage__:</span><span class="sxs-lookup"><span data-stu-id="cf01f-172">The following are example entries for a storage account named __mystorage__:</span></span>

        fs.azure.account.keyprovider.mystorage.blob.core.windows.net
        fs.azure.account.key.mystorage.blob.core.windows.net

4. <span data-ttu-id="cf01f-173">Depois de identificar as chaves da conta de armazenamento que você precisa remover, use o ícone vermelho '-' à direita da entrada para excluí-las.</span><span class="sxs-lookup"><span data-stu-id="cf01f-173">After you have identified the keys for the storage account you need to remove, use the red '-' icon to the right of the entry to delete it.</span></span> <span data-ttu-id="cf01f-174">Depois, use o botão __Salvar__ para salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="cf01f-174">Then use the __Save__ button to save your changes.</span></span>

5. <span data-ttu-id="cf01f-175">Depois que as alterações forem salvas, use a ação de script para adicionar a conta de armazenamento e o novo valor de chaves ao cluster.</span><span class="sxs-lookup"><span data-stu-id="cf01f-175">After changes have been saved, use the script action to add the storage account and new key value to the cluster.</span></span>

### <a name="poor-performance"></a><span data-ttu-id="cf01f-176">Desempenho ruim</span><span class="sxs-lookup"><span data-stu-id="cf01f-176">Poor performance</span></span>

<span data-ttu-id="cf01f-177">Se a conta de armazenamento estiver em uma região diferente do cluster do HDInsight, você poderá enfrentar um desempenho ruim.</span><span class="sxs-lookup"><span data-stu-id="cf01f-177">If the storage account is in a different region than the HDInsight cluster, you may experience poor performance.</span></span> <span data-ttu-id="cf01f-178">O acesso a dados em uma região diferente envia o tráfego de rede para fora do data center regional do Azure e para a internet pública, o que pode introduzir latência.</span><span class="sxs-lookup"><span data-stu-id="cf01f-178">Accessing data in a different region sends network traffic outside the regional Azure data center and across the public internet, which can introduce latency.</span></span>

> [!WARNING]
> <span data-ttu-id="cf01f-179">Não há suporte para o uso de uma conta de armazenamento em uma região diferente do cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cf01f-179">Using a storage account in a different region than the HDInsight cluster is not supported.</span></span>

### <a name="additional-charges"></a><span data-ttu-id="cf01f-180">Custos adicionais</span><span class="sxs-lookup"><span data-stu-id="cf01f-180">Additional charges</span></span>

<span data-ttu-id="cf01f-181">Se a conta de armazenamento estiver em uma região diferente do cluster do HDInsight, você poderá observar encargos adicionais em sua cobrança do Azure.</span><span class="sxs-lookup"><span data-stu-id="cf01f-181">If the storage account is in a different region than the HDInsight cluster, you may notice additional egress charges on your Azure billing.</span></span> <span data-ttu-id="cf01f-182">Um encargo de saída é aplicado quando os dados saem de um data center regional.</span><span class="sxs-lookup"><span data-stu-id="cf01f-182">An egress charge is applied when data leaves a regional data center.</span></span> <span data-ttu-id="cf01f-183">Esse encargo se aplica mesmo se o tráfego for destinado a outro data center do Azure em uma região diferente.</span><span class="sxs-lookup"><span data-stu-id="cf01f-183">This charge is applied even if the traffic is destined for another Azure data center in a different region.</span></span>

> [!WARNING]
> <span data-ttu-id="cf01f-184">Não há suporte para o uso de uma conta de armazenamento em uma região diferente do cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cf01f-184">Using a storage account in a different region than the HDInsight cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf01f-185">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cf01f-185">Next steps</span></span>

<span data-ttu-id="cf01f-186">Você aprendeu a adicionar outras contas de armazenamento a um cluster HDInsight existente.</span><span class="sxs-lookup"><span data-stu-id="cf01f-186">You have learned how to add additional storage accounts to an existing HDInsight cluster.</span></span> <span data-ttu-id="cf01f-187">Para saber mais sobre as ações de script, confira [Personalizar clusters HDInsight com base em Linux usando a ação de script](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="cf01f-187">For more information on script actions, see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>
