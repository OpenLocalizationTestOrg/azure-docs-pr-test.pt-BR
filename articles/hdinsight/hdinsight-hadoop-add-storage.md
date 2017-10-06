---
title: contas de armazenamento do Azure adicionais aaaAdd tooHDInsight | Microsoft Docs
description: Saiba como tooadd adicionais de armazenamento do Azure contas tooan cluster de HDInsight existente.
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
ms.openlocfilehash: ce5acfa4b61bf7e83b1fb374d64a1eaa3182fbec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-additional-storage-accounts-toohdinsight"></a><span data-ttu-id="dc64a-103">Adicionar tooHDInsight de contas de armazenamento adicional</span><span class="sxs-lookup"><span data-stu-id="dc64a-103">Add additional storage accounts tooHDInsight</span></span>

<span data-ttu-id="dc64a-104">Saiba como toouse script ações tooadd mais armazenamento do Azure contas tooHDInsight.</span><span class="sxs-lookup"><span data-stu-id="dc64a-104">Learn how toouse script actions tooadd additional Azure storage accounts tooHDInsight.</span></span> <span data-ttu-id="dc64a-105">Olá, as etapas neste documento adicionam um cluster de HDInsight baseados em Linux existente do armazenamento conta tooan.</span><span class="sxs-lookup"><span data-stu-id="dc64a-105">hello steps in this document add a storage account tooan existing Linux-based HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dc64a-106">informações de saudação neste documento são sobre como adicionar armazenamento adicional tooa cluster após ele ter sido criado.</span><span class="sxs-lookup"><span data-stu-id="dc64a-106">hello information in this document is about adding additional storage tooa cluster after it has been created.</span></span> <span data-ttu-id="dc64a-107">Para saber mais sobre como adicionar contas de armazenamento durante a criação do cluster, veja [Configurar clusters no HDInsight com Hadoop, Spark, Kafka e muito mais](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="dc64a-107">For information on adding storage accounts during cluster creation, see [Set up clusters in HDInsight with Hadoop, Spark, Kafka, and more](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="how-it-works"></a><span data-ttu-id="dc64a-108">Como ele funciona</span><span class="sxs-lookup"><span data-stu-id="dc64a-108">How it works</span></span>

<span data-ttu-id="dc64a-109">Esse script usa Olá parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="dc64a-109">This script takes hello following parameters:</span></span>

* <span data-ttu-id="dc64a-110">__Nome da conta de armazenamento do Azure__: nome Olá Olá conta tooadd toohello HDInsight do cluster de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="dc64a-110">__Azure storage account name__: hello name of hello storage account tooadd toohello HDInsight cluster.</span></span> <span data-ttu-id="dc64a-111">Depois de executar o script hello, HDInsight pode ler e gravar dados armazenados nesta conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="dc64a-111">After running hello script, HDInsight can read and write data stored in this storage account.</span></span>

* <span data-ttu-id="dc64a-112">__Chave de conta de armazenamento do Azure__: uma chave que concede a conta de armazenamento de toohello de acesso.</span><span class="sxs-lookup"><span data-stu-id="dc64a-112">__Azure storage account key__: A key that grants access toohello storage account.</span></span>

* <span data-ttu-id="dc64a-113">__-p__ (opcional): se for especificado, a chave de Olá não é criptografado e é armazenado no arquivo de Core-site.XML hello como texto sem formatação.</span><span class="sxs-lookup"><span data-stu-id="dc64a-113">__-p__ (optional): If specified, hello key is not encrypted and is stored in hello core-site.xml file as plain text.</span></span>

<span data-ttu-id="dc64a-114">Durante o processamento, o script hello executa Olá ações a seguir:</span><span class="sxs-lookup"><span data-stu-id="dc64a-114">During processing, hello script performs hello following actions:</span></span>

* <span data-ttu-id="dc64a-115">Se hello conta de armazenamento já existe na configuração de Core-site.XML Olá para cluster hello, Olá script será encerrado e nenhuma ação adicional é executadas.</span><span class="sxs-lookup"><span data-stu-id="dc64a-115">If hello storage account already exists in hello core-site.xml configuration for hello cluster, hello script exits and no further actions are performed.</span></span>

* <span data-ttu-id="dc64a-116">Verifica se a conta de armazenamento Olá existe e pode ser acessada usando a chave de saudação.</span><span class="sxs-lookup"><span data-stu-id="dc64a-116">Verifies that hello storage account exists and can be accessed using hello key.</span></span>

* <span data-ttu-id="dc64a-117">Criptografa a chave de saudação usando credenciais de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="dc64a-117">Encrypts hello key using hello cluster credential.</span></span>

* <span data-ttu-id="dc64a-118">Adiciona Olá armazenamento conta toohello Core-site.XML arquivo.</span><span class="sxs-lookup"><span data-stu-id="dc64a-118">Adds hello storage account toohello core-site.xml file.</span></span>

* <span data-ttu-id="dc64a-119">Para e reinicia os serviços de saudação Oozie, YARN, MapReduce2 e HDFS.</span><span class="sxs-lookup"><span data-stu-id="dc64a-119">Stops and restarts hello Oozie, YARN, MapReduce2, and HDFS services.</span></span> <span data-ttu-id="dc64a-120">Parar e iniciar esses serviços permitem toouse Olá nova conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="dc64a-120">Stopping and starting these services allows them toouse hello new storage account.</span></span>

> [!WARNING]
> <span data-ttu-id="dc64a-121">Não há suporte para usar uma conta de armazenamento no cluster do HDInsight Olá um local diferente.</span><span class="sxs-lookup"><span data-stu-id="dc64a-121">Using a storage account in a different location than hello HDInsight cluster is not supported.</span></span>

## <a name="hello-script"></a><span data-ttu-id="dc64a-122">script Hello</span><span class="sxs-lookup"><span data-stu-id="dc64a-122">hello script</span></span>

<span data-ttu-id="dc64a-123">__Local do script__: [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)</span><span class="sxs-lookup"><span data-stu-id="dc64a-123">__Script location__: [https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh)</span></span>

<span data-ttu-id="dc64a-124">__Requisitos__:</span><span class="sxs-lookup"><span data-stu-id="dc64a-124">__Requirements__:</span></span>

* <span data-ttu-id="dc64a-125">script Hello deve ser aplicada em Olá __nós de cabeçalho__.</span><span class="sxs-lookup"><span data-stu-id="dc64a-125">hello script must be applied on hello __Head nodes__.</span></span>

## <a name="toouse-hello-script"></a><span data-ttu-id="dc64a-126">script de saudação toouse</span><span class="sxs-lookup"><span data-stu-id="dc64a-126">toouse hello script</span></span>

<span data-ttu-id="dc64a-127">Esse script pode ser usado em Olá portal do Azure, Azure PowerShell, ou Olá 1.0 da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="dc64a-127">This script can be used from hello Azure portal, Azure PowerShell, or hello Azure CLI 1.0.</span></span> <span data-ttu-id="dc64a-128">Para obter mais informações, consulte Olá [usando a ação de script de clusters HDInsight baseados em Linux personalizar](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) documento.</span><span class="sxs-lookup"><span data-stu-id="dc64a-128">For more information, see hello [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dc64a-129">Ao usar etapas Olá fornecidas no documento de personalização hello, use Olá tooapply informações a seguir este script:</span><span class="sxs-lookup"><span data-stu-id="dc64a-129">When using hello steps provided in hello customization document, use hello following information tooapply this script:</span></span>
>
> * <span data-ttu-id="dc64a-130">Substitua qualquer ação de script de exemplo URI hello URI para esse script (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh).</span><span class="sxs-lookup"><span data-stu-id="dc64a-130">Replace any example script action URI with hello URI for this script (https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh).</span></span>
> * <span data-ttu-id="dc64a-131">Substitua quaisquer parâmetros de exemplo com o nome de conta de armazenamento do Azure hello e chave Olá conta toobe toohello adicionado do cluster de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="dc64a-131">Replace any example parameters with hello Azure storage account name and key of hello storage account toobe added toohello cluster.</span></span> <span data-ttu-id="dc64a-132">Se usar hello portal do Azure, esses parâmetros devem ser separados por um espaço.</span><span class="sxs-lookup"><span data-stu-id="dc64a-132">If using hello Azure portal, these parameters must be separated by a space.</span></span>
> * <span data-ttu-id="dc64a-133">Você não precisa toomark esse script como __Persisted__, como ele atualizações de configuração do Ambari Olá para cluster Olá diretamente.</span><span class="sxs-lookup"><span data-stu-id="dc64a-133">You do not need toomark this script as __Persisted__, as it directly updates hello Ambari configuration for hello cluster.</span></span>

## <a name="known-issues"></a><span data-ttu-id="dc64a-134">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="dc64a-134">Known issues</span></span>

### <a name="storage-accounts-not-displayed-in-azure-portal-or-tools"></a><span data-ttu-id="dc64a-135">Contas de armazenamento não exibidas no Portal do Azure ou nas ferramentas</span><span class="sxs-lookup"><span data-stu-id="dc64a-135">Storage accounts not displayed in Azure portal or tools</span></span>

<span data-ttu-id="dc64a-136">Ao exibir hello HDInsight cluster no hello portal do Azure, selecionando Olá __contas de armazenamento__ entrada em __propriedades__ não mostra as contas de armazenamento adicionadas por esta ação de script.</span><span class="sxs-lookup"><span data-stu-id="dc64a-136">When viewing hello HDInsight cluster in hello Azure portal, selecting hello __Storage Accounts__ entry under __Properties__ does not display storage accounts added through this script action.</span></span> <span data-ttu-id="dc64a-137">Azure PowerShell e a CLI do Azure não exibem conta de armazenamento adicional da saudação ou.</span><span class="sxs-lookup"><span data-stu-id="dc64a-137">Azure PowerShell and Azure CLI do not display hello additional storage account either.</span></span>

<span data-ttu-id="dc64a-138">informações de armazenamento de saudação não são exibidas porque o script hello apenas modifica a configuração de Core-site.XML de saudação para cluster hello.</span><span class="sxs-lookup"><span data-stu-id="dc64a-138">hello storage information isn't displayed because hello script only modifies hello core-site.xml configuration for hello cluster.</span></span> <span data-ttu-id="dc64a-139">Essas informações não são usadas ao recuperar informações de cluster hello usando APIs de gerenciamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="dc64a-139">This information is not used when retrieving hello cluster information using Azure management APIs.</span></span>

<span data-ttu-id="dc64a-140">informações de conta de armazenamento tooview adicionado cluster toohello usando esse script, use Olá API REST do Ambari.</span><span class="sxs-lookup"><span data-stu-id="dc64a-140">tooview storage account information added toohello cluster using this script, use hello Ambari REST API.</span></span> <span data-ttu-id="dc64a-141">Olá tooretrieve comandos a seguir ao Use essas informações para seu cluster:</span><span class="sxs-lookup"><span data-stu-id="dc64a-141">Use hello following commands tooretrieve this information for your cluster:</span></span>

```PowerShell
$creds = Get-Credential -UserName "admin" -Message "Enter hello cluster login credentials"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties."fs.azure.account.key.$storageAccountName.blob.core.windows.net"
```

> [!NOTE]
> <span data-ttu-id="dc64a-142">Definir `$clusterName` toohello nome do cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="dc64a-142">Set `$clusterName` toohello name of hello HDInsight cluster.</span></span> <span data-ttu-id="dc64a-143">Definir `$storageAccountName` toohello nome hello da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="dc64a-143">Set `$storageAccountName` toohello name of hello storage account.</span></span> <span data-ttu-id="dc64a-144">Quando solicitado, insira o logon de cluster da saudação (administrador) e a senha.</span><span class="sxs-lookup"><span data-stu-id="dc64a-144">When prompted, enter hello cluster login (admin) and password.</span></span>

```Bash
curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.azure.account.key.$STORAGEACCOUNTNAME.blob.core.windows.net"] | select(. != null)'
```

> [!NOTE]
> <span data-ttu-id="dc64a-145">Definir `$PASSWORD` toohello senha da conta de logon (admin) de cluster.</span><span class="sxs-lookup"><span data-stu-id="dc64a-145">Set `$PASSWORD` toohello cluster login (admin) account password.</span></span> <span data-ttu-id="dc64a-146">Definir `$CLUSTERNAME` toohello nome do cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="dc64a-146">Set `$CLUSTERNAME` toohello name of hello HDInsight cluster.</span></span> <span data-ttu-id="dc64a-147">Definir `$STORAGEACCOUNTNAME` toohello nome hello da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="dc64a-147">Set `$STORAGEACCOUNTNAME` toohello name of hello storage account.</span></span>
>
> <span data-ttu-id="dc64a-148">Este exemplo usa [ondulação (http://curl.haxx.se/)](http://curl.haxx.se/) e [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) tooretrieve e análise de dados JSON.</span><span class="sxs-lookup"><span data-stu-id="dc64a-148">This example uses [curl (http://curl.haxx.se/)](http://curl.haxx.se/) and [jq (https://stedolan.github.io/jq/)](https://stedolan.github.io/jq/) tooretrieve and parse JSON data.</span></span>

<span data-ttu-id="dc64a-149">Ao usar esse comando, substitua __CLUSTERNAME__ com o nome de saudação do cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="dc64a-149">When using this command, replace __CLUSTERNAME__ with hello name of hello HDInsight cluster.</span></span> <span data-ttu-id="dc64a-150">Substituir __senha__ com a senha de logon de saudação HTTP para o cluster hello.</span><span class="sxs-lookup"><span data-stu-id="dc64a-150">Replace __PASSWORD__ with hello HTTP login password for hello cluster.</span></span> <span data-ttu-id="dc64a-151">Substituir __STORAGEACCOUNT__ com nome Olá Olá da conta de armazenamento adicionada usando a ação de script.</span><span class="sxs-lookup"><span data-stu-id="dc64a-151">Replace __STORAGEACCOUNT__ with hello name of hello storage account added using script action.</span></span> <span data-ttu-id="dc64a-152">Informações retornadas deste comando será exibida semelhante toohello texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="dc64a-152">Information returned from this command appears similar toohello following text:</span></span>

    "MIIB+gYJKoZIhvcNAQcDoIIB6zCCAecCAQAxggFaMIIBVgIBADA+MCoxKDAmBgNVBAMTH2RiZW5jcnlwdGlvbi5henVyZWhkaW5zaWdodC5uZXQCEA6GDZMW1oiESKFHFOOEgjcwDQYJKoZIhvcNAQEBBQAEggEATIuO8MJ45KEQAYBQld7WaRkJOWqaCLwFub9zNpscrquA2f3o0emy9Vr6vu5cD3GTt7PmaAF0pvssbKVMf/Z8yRpHmeezSco2y7e9Qd7xJKRLYtRHm80fsjiBHSW9CYkQwxHaOqdR7DBhZyhnj+DHhODsIO2FGM8MxWk4fgBRVO6CZ5eTmZ6KVR8wYbFLi8YZXb7GkUEeSn2PsjrKGiQjtpXw1RAyanCagr5vlg8CicZg1HuhCHWf/RYFWM3EBbVz+uFZPR3BqTgbvBhWYXRJaISwssvxotppe0ikevnEgaBYrflB2P+PVrwPTZ7f36HQcn4ifY1WRJQ4qRaUxdYEfzCBgwYJKoZIhvcNAQcBMBQGCCqGSIb3DQMHBAhRdscgRV3wmYBg3j/T1aEnO3wLWCRpgZa16MWqmfQPuansKHjLwbZjTpeirqUAQpZVyXdK/w4gKlK+t1heNsNo1Wwqu+Y47bSAX1k9Ud7+Ed2oETDI7724IJ213YeGxvu4Ngcf2eHW+FRK"

<span data-ttu-id="dc64a-153">Esse texto é um exemplo de uma chave criptografada, que é usada tooaccess Olá conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="dc64a-153">This text is an example of an encrypted key, which is used tooaccess hello storage account.</span></span>

### <a name="unable-tooaccess-storage-after-changing-key"></a><span data-ttu-id="dc64a-154">Não é possível tooaccess armazenamento depois de alterar a chave</span><span class="sxs-lookup"><span data-stu-id="dc64a-154">Unable tooaccess storage after changing key</span></span>

<span data-ttu-id="dc64a-155">Se você alterar a chave de saudação para uma conta de armazenamento, HDInsight não pode acessar a conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="dc64a-155">If you change hello key for a storage account, HDInsight can no longer access hello storage account.</span></span> <span data-ttu-id="dc64a-156">HDInsight usa uma cópia armazenada em cache de chave em Olá Core-site.XML para cluster hello.</span><span class="sxs-lookup"><span data-stu-id="dc64a-156">HDInsight uses a cached copy of key in hello core-site.xml for hello cluster.</span></span> <span data-ttu-id="dc64a-157">Essa cópia armazenada em cache deve ser a nova chave de saudação toomatch atualizado.</span><span class="sxs-lookup"><span data-stu-id="dc64a-157">This cached copy must be updated toomatch hello new key.</span></span>

<span data-ttu-id="dc64a-158">Executado novamente ação de script hello __não__ atualizar chave hello, conforme o script hello verifica toosee se já existe uma entrada para a conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="dc64a-158">Running hello script action again does __not__ update hello key, as hello script checks toosee if an entry for hello storage account already exists.</span></span> <span data-ttu-id="dc64a-159">Se já houver uma entrada, ele não fará alterações.</span><span class="sxs-lookup"><span data-stu-id="dc64a-159">If an entry already exists, it does not make any changes.</span></span>

<span data-ttu-id="dc64a-160">toowork alternativa para esse problema, você deve remover a entrada existente Olá Olá conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="dc64a-160">toowork around this problem, you must remove hello existing entry for hello storage account.</span></span> <span data-ttu-id="dc64a-161">Use Olá entrada existente de saudação de tooremove de etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="dc64a-161">Use hello following steps tooremove hello existing entry:</span></span>

1. <span data-ttu-id="dc64a-162">Em um navegador da web, abra a saudação da interface do usuário do Ambari Web para seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dc64a-162">In a web browser, open hello Ambari Web UI for your HDInsight cluster.</span></span> <span data-ttu-id="dc64a-163">Olá URI é https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="dc64a-163">hello URI is https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="dc64a-164">Substituir __CLUSTERNAME__ com nome de saudação do cluster.</span><span class="sxs-lookup"><span data-stu-id="dc64a-164">Replace __CLUSTERNAME__ with hello name of your cluster.</span></span>

    <span data-ttu-id="dc64a-165">Quando solicitado, insira o usuário de logon do hello HTTP e a senha para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="dc64a-165">When prompted, enter hello HTTP login user and password for your cluster.</span></span>

2. <span data-ttu-id="dc64a-166">Na lista de saudação de serviços esquerda Olá da página hello, selecione __HDFS__.</span><span class="sxs-lookup"><span data-stu-id="dc64a-166">From hello list of services on hello left of hello page, select __HDFS__.</span></span> <span data-ttu-id="dc64a-167">Em seguida, selecione Olá __configurações__ guia no Centro de saudação da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="dc64a-167">Then select hello __Configs__ tab in hello center of hello page.</span></span>

3. <span data-ttu-id="dc64a-168">Em Olá __filtro...__  campo, digite um valor de __fs.azure.account__.</span><span class="sxs-lookup"><span data-stu-id="dc64a-168">In hello __Filter...__ field, enter a value of __fs.azure.account__.</span></span> <span data-ttu-id="dc64a-169">Isso retorna as entradas para as contas de armazenamento adicional que foram adicionadas toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="dc64a-169">This returns entries for any additional storage accounts that have been added toohello cluster.</span></span> <span data-ttu-id="dc64a-170">Há dois tipos de entradas; __keyprovider__ e __key__.</span><span class="sxs-lookup"><span data-stu-id="dc64a-170">There are two types of entries; __keyprovider__ and __key__.</span></span> <span data-ttu-id="dc64a-171">Conter nome Olá Olá da conta de armazenamento como parte do nome da chave hello.</span><span class="sxs-lookup"><span data-stu-id="dc64a-171">Both contain hello name of hello storage account as part of hello key name.</span></span>

    <span data-ttu-id="dc64a-172">Olá, a seguir está exemplos de entradas para uma conta de armazenamento denominada __mystorage__:</span><span class="sxs-lookup"><span data-stu-id="dc64a-172">hello following are example entries for a storage account named __mystorage__:</span></span>

        fs.azure.account.keyprovider.mystorage.blob.core.windows.net
        fs.azure.account.key.mystorage.blob.core.windows.net

4. <span data-ttu-id="dc64a-173">Depois de ter identificado chaves Olá Olá conta de armazenamento é necessário tooremove, use Olá vermelho '-' toohello ícone à direita da saudação entrada toodelete-lo.</span><span class="sxs-lookup"><span data-stu-id="dc64a-173">After you have identified hello keys for hello storage account you need tooremove, use hello red '-' icon toohello right of hello entry toodelete it.</span></span> <span data-ttu-id="dc64a-174">Em seguida, usar Olá __salvar__ botão toosave suas alterações.</span><span class="sxs-lookup"><span data-stu-id="dc64a-174">Then use hello __Save__ button toosave your changes.</span></span>

5. <span data-ttu-id="dc64a-175">Depois que as alterações foram salvas, use conta de armazenamento de Olá Olá script ação tooadd e o novo cluster de toohello do valor de chave.</span><span class="sxs-lookup"><span data-stu-id="dc64a-175">After changes have been saved, use hello script action tooadd hello storage account and new key value toohello cluster.</span></span>

### <a name="poor-performance"></a><span data-ttu-id="dc64a-176">Desempenho ruim</span><span class="sxs-lookup"><span data-stu-id="dc64a-176">Poor performance</span></span>

<span data-ttu-id="dc64a-177">Se a conta de armazenamento Olá estiver em uma região diferente cluster do HDInsight hello, você pode enfrentar desempenho insatisfatório.</span><span class="sxs-lookup"><span data-stu-id="dc64a-177">If hello storage account is in a different region than hello HDInsight cluster, you may experience poor performance.</span></span> <span data-ttu-id="dc64a-178">Acessar os dados de um região diferente envia tráfego de rede fora hello Azure data center regional e em Olá internet pública, que pode apresentar latência.</span><span class="sxs-lookup"><span data-stu-id="dc64a-178">Accessing data in a different region sends network traffic outside hello regional Azure data center and across hello public internet, which can introduce latency.</span></span>

> [!WARNING]
> <span data-ttu-id="dc64a-179">Não há suporte para usar uma conta de armazenamento no cluster do HDInsight Olá uma região diferente.</span><span class="sxs-lookup"><span data-stu-id="dc64a-179">Using a storage account in a different region than hello HDInsight cluster is not supported.</span></span>

### <a name="additional-charges"></a><span data-ttu-id="dc64a-180">Custos adicionais</span><span class="sxs-lookup"><span data-stu-id="dc64a-180">Additional charges</span></span>

<span data-ttu-id="dc64a-181">Se a conta de armazenamento Olá é em uma região diferente de Olá cluster HDInsight, você pode perceber encargo adicional na sua cobrança do Azure.</span><span class="sxs-lookup"><span data-stu-id="dc64a-181">If hello storage account is in a different region than hello HDInsight cluster, you may notice additional egress charges on your Azure billing.</span></span> <span data-ttu-id="dc64a-182">Um encargo de saída é aplicado quando os dados saem de um data center regional.</span><span class="sxs-lookup"><span data-stu-id="dc64a-182">An egress charge is applied when data leaves a regional data center.</span></span> <span data-ttu-id="dc64a-183">Essa taxa será aplicada mesmo que o tráfego de saudação é destinado para outro data center do Azure em uma região diferente.</span><span class="sxs-lookup"><span data-stu-id="dc64a-183">This charge is applied even if hello traffic is destined for another Azure data center in a different region.</span></span>

> [!WARNING]
> <span data-ttu-id="dc64a-184">Não há suporte para usar uma conta de armazenamento no cluster do HDInsight Olá uma região diferente.</span><span class="sxs-lookup"><span data-stu-id="dc64a-184">Using a storage account in a different region than hello HDInsight cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc64a-185">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dc64a-185">Next steps</span></span>

<span data-ttu-id="dc64a-186">Você aprendeu como contas de armazenamento adicional tooadd tooan cluster de HDInsight existente.</span><span class="sxs-lookup"><span data-stu-id="dc64a-186">You have learned how tooadd additional storage accounts tooan existing HDInsight cluster.</span></span> <span data-ttu-id="dc64a-187">Para saber mais sobre as ações de script, confira [Personalizar clusters HDInsight com base em Linux usando a ação de script](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="dc64a-187">For more information on script actions, see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>
