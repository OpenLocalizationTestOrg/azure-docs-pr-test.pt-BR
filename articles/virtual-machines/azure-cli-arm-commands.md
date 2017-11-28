---
title: aaaAzure CLI comandos no modo do Gerenciador de recursos | Microsoft Docs
description: "Recursos toomanage no modelo de implantação do Gerenciador de recursos de saudação de comandos de interface de linha de comando (CLI) do Azure"
services: virtual-machines-linux,virtual-machines-windows,virtual-network,mobile-services,cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: be37da5b-72fe-41a1-9fa0-8937b69464ec
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: command-line-interface
ms.devlang: na
ms.topic: article
ms.date: 04/18/2017
ms.author: danlep
ms.openlocfilehash: 49539655f7b24511e219f982819bcb59c9305d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-commands-in-resource-manager-mode"></a><span data-ttu-id="d5fce-103">Comandos da CLI do Azure no modo do Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="d5fce-103">Azure CLI commands in Resource Manager mode</span></span>
<span data-ttu-id="d5fce-104">Este artigo fornece sintaxe e opções para comandos de interface de linha de comando (CLI) do Azure que faria normalmente para usam toocreate e gerenciar recursos do Azure no modelo de implantação do Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="d5fce-104">This article provides syntax and options for Azure command-line interface (CLI) commands you'd commonly use toocreate and manage Azure resources in hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="d5fce-105">Você pode acessar esses comandos executando Olá CLI no modo do Gerenciador de recursos (arm).</span><span class="sxs-lookup"><span data-stu-id="d5fce-105">You access these commands by running hello CLI in Resource Manager (arm) mode.</span></span> <span data-ttu-id="d5fce-106">Essa não é uma referência completa, e sua versão da CLI poderá mostrar comandos ou parâmetros um pouco diferentes.</span><span class="sxs-lookup"><span data-stu-id="d5fce-106">This is not a complete reference, and your CLI version may show slightly different commands or parameters.</span></span> <span data-ttu-id="d5fce-107">Para obter uma visão geral dos recursos e dos grupos de recursos do Azure, confira [Visão geral do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d5fce-107">For a general overview of Azure resources and resource groups, see [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>  

> [!NOTE]
> <span data-ttu-id="d5fce-108">Este artigo mostra Gerenciador de recursos de comandos de modo Olá CLI do Azure, às vezes chamado 1.0 da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="d5fce-108">This article shows Resource Manager mode commands in hello Azure CLI, sometimes called Azure CLI 1.0.</span></span> <span data-ttu-id="d5fce-109">toowork no modelo do Gerenciador de recursos de saudação, você também pode tentar Olá [2.0 do CLI do Azure](/cli/azure/install-az-cli2), nossa próxima multiplataforma de geração CLI.</span><span class="sxs-lookup"><span data-stu-id="d5fce-109">toowork in hello Resource Manager model, you can also try hello [Azure CLI 2.0](/cli/azure/install-az-cli2), our next generation multi-platform CLI.</span></span>
><span data-ttu-id="d5fce-110">Saiba mais sobre Olá [antigo e novo CLIs do Azure](/cli/azure/old-and-new-clis).</span><span class="sxs-lookup"><span data-stu-id="d5fce-110">Find out more about hello [old and new Azure CLIs](/cli/azure/old-and-new-clis).</span></span>
>

<span data-ttu-id="d5fce-111">tooget iniciada, primeiro [instalar Olá CLI do Azure](../cli-install-nodejs.md) e [conectar tooyour assinatura do Azure](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="d5fce-111">tooget started, first [install hello Azure CLI](../cli-install-nodejs.md) and [connect tooyour Azure subscription](../xplat-cli-connect.md).</span></span>

<span data-ttu-id="d5fce-112">Para sintaxe de comando atual e as opções na linha de comando Olá no modo do Gerenciador de recursos, digite `azure help` ou toodisplay ajuda para um comando específico, `azure help [command]`.</span><span class="sxs-lookup"><span data-stu-id="d5fce-112">For current command syntax and options at hello command line in Resource Manager mode, type `azure help` or, toodisplay help for a specific command, `azure help [command]`.</span></span> <span data-ttu-id="d5fce-113">Também encontre exemplos CLI na documentação de saudação para criar e gerenciar os serviços do Azure específicos.</span><span class="sxs-lookup"><span data-stu-id="d5fce-113">Also find CLI examples in hello documentation for creating and managing specific Azure services.</span></span>

<span data-ttu-id="d5fce-114">Parâmetros opcionais são mostrados entre colchetes (por exemplo, `[parameter]`).</span><span class="sxs-lookup"><span data-stu-id="d5fce-114">Optional parameters are shown in square brackets (for example, `[parameter]`).</span></span> <span data-ttu-id="d5fce-115">Todos os outros parâmetros são obrigatórios.</span><span class="sxs-lookup"><span data-stu-id="d5fce-115">All other parameters are required.</span></span>

<span data-ttu-id="d5fce-116">Parâmetros opcionais são específicas de toocommand adição documentados aqui, há três parâmetros opcionais que podem ser usado toodisplay detalhadas de saída, como opções de solicitação e códigos de status.</span><span class="sxs-lookup"><span data-stu-id="d5fce-116">In addition toocommand-specific optional parameters documented here, there are three optional parameters that can be used toodisplay detailed output such as request options and status codes.</span></span> <span data-ttu-id="d5fce-117">Olá `-v` parâmetro fornece a saída detalhada e hello `-vv` parâmetro fornece ainda mais detalhado de saída detalhada.</span><span class="sxs-lookup"><span data-stu-id="d5fce-117">hello `-v` parameter provides verbose output, and hello `-vv` parameter provides even more detailed verbose output.</span></span> <span data-ttu-id="d5fce-118">Olá `--json` opção produz resultados Olá no formato json bruto.</span><span class="sxs-lookup"><span data-stu-id="d5fce-118">hello `--json` option outputs hello result in raw json format.</span></span>

## <a name="setting-hello-resource-manager-mode"></a><span data-ttu-id="d5fce-119">Configuração do modo de saudação Gerenciador de recursos</span><span class="sxs-lookup"><span data-stu-id="d5fce-119">Setting hello Resource Manager mode</span></span>
<span data-ttu-id="d5fce-120">Use Olá tooenable comandos de CLI do Azure Resource Manager comandos de modo a seguir.</span><span class="sxs-lookup"><span data-stu-id="d5fce-120">Use hello following command tooenable Azure CLI Resource Manager mode commands.</span></span>

    azure config mode arm

> [!NOTE]
> <span data-ttu-id="d5fce-121">modos de Gerenciador de recursos do Azure e gerenciamento de serviços do Azure do Hello CLI são mutuamente exclusivos.</span><span class="sxs-lookup"><span data-stu-id="d5fce-121">hello CLI's Azure Resource Manager mode and Azure Service Management mode are mutually exclusive.</span></span> <span data-ttu-id="d5fce-122">Ou seja, os recursos criados no modo não podem ser gerenciados de saudação outro modo.</span><span class="sxs-lookup"><span data-stu-id="d5fce-122">That is, resources created in one mode cannot be managed from hello other mode.</span></span>
> 
> 

## <a name="azure-account-manage-your-account-information"></a><span data-ttu-id="d5fce-123">conta do Azure: gerenciar as informações da sua conta</span><span class="sxs-lookup"><span data-stu-id="d5fce-123">azure account: Manage your account information</span></span>
<span data-ttu-id="d5fce-124">As informações de assinatura do Azure são usadas pela conta do hello ferramenta tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="d5fce-124">Your Azure subscription information is used by hello tool tooconnect tooyour account.</span></span>

<span data-ttu-id="d5fce-125">**Listar assinaturas Olá importado**</span><span class="sxs-lookup"><span data-stu-id="d5fce-125">**List hello imported subscriptions**</span></span>

    account list [options]

<span data-ttu-id="d5fce-126">**Mostra detalhes sobre uma assinatura**</span><span class="sxs-lookup"><span data-stu-id="d5fce-126">**Show details about a subscription**</span></span>  

    account show [options] [subscriptionNameOrId]

<span data-ttu-id="d5fce-127">**Definir a assinatura atual Olá**</span><span class="sxs-lookup"><span data-stu-id="d5fce-127">**Set hello current subscription**</span></span>

    account set [options] <subscriptionNameOrId>

<span data-ttu-id="d5fce-128">**Remover uma assinatura ou o ambiente ou limpar todas as informações de conta e ambiente Olá armazenado**</span><span class="sxs-lookup"><span data-stu-id="d5fce-128">**Remove a subscription or environment, or clear all of hello stored account and environment info**</span></span>  

    account clear [options]

<span data-ttu-id="d5fce-129">**Comandos toomanage seu ambiente de conta**</span><span class="sxs-lookup"><span data-stu-id="d5fce-129">**Commands toomanage your account environment**</span></span>  

    account env list [options]
    account env show [options] [environment]
    account env add [options] [environment]
    account env set [options] [environment]
    account env delete [options] [environment]

## <a name="azure-ad-commands-toodisplay-active-directory-objects"></a><span data-ttu-id="d5fce-130">o ad do Azure: comandos toodisplay objetos do Active Directory</span><span class="sxs-lookup"><span data-stu-id="d5fce-130">azure ad: Commands toodisplay Active Directory objects</span></span>
<span data-ttu-id="d5fce-131">**Comandos toodisplay do active directory aplicativos**</span><span class="sxs-lookup"><span data-stu-id="d5fce-131">**Commands toodisplay active directory applications**</span></span>

    ad app create [options]
    ad app delete [options] <object-id>

<span data-ttu-id="d5fce-132">**Grupos do comandos toodisplay do active directory**</span><span class="sxs-lookup"><span data-stu-id="d5fce-132">**Commands toodisplay active directory groups**</span></span>

    ad group list [options]
    ad group show [options]

<span data-ttu-id="d5fce-133">**Comandos tooprovide uma informação de grupo ou um membro da sub do active directory**</span><span class="sxs-lookup"><span data-stu-id="d5fce-133">**Commands tooprovide an active directory sub group or member info**</span></span>

    ad group member list [options] [objectId]

<span data-ttu-id="d5fce-134">**Entidades de serviço comandos toodisplay do active directory**</span><span class="sxs-lookup"><span data-stu-id="d5fce-134">**Commands toodisplay active directory service principals**</span></span>

    ad sp list [options]
    ad sp show [options]
    ad sp create [options] <application-id>
    ad sp delete [options] <object-id>

<span data-ttu-id="d5fce-135">**Usuários do active directory de toodisplay de comandos**</span><span class="sxs-lookup"><span data-stu-id="d5fce-135">**Commands toodisplay active directory users**</span></span>

    ad user list [options]
    ad user show [options]

## <a name="azure-availset-commands-toomanage-your-availability-sets"></a><span data-ttu-id="d5fce-136">Azure availset: toomanage comandos sua disponibilidade define</span><span class="sxs-lookup"><span data-stu-id="d5fce-136">azure availset: commands toomanage your availability sets</span></span>
<span data-ttu-id="d5fce-137">**Cria um conjunto de disponibilidade dentro de um grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="d5fce-137">**Creates an availability set within a resource group**</span></span>

    availset create [options] <resource-group> <name> <location> [tags]

<span data-ttu-id="d5fce-138">**Listas Olá conjuntos de disponibilidade dentro de um grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="d5fce-138">**Lists hello availability sets within a resource group**</span></span>

    availset list [options] <resource-group>

<span data-ttu-id="d5fce-139">**Obtém um conjunto de disponibilidade dentro de um grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="d5fce-139">**Gets one availability set within a resource group**</span></span>

    availset show [options] <resource-group> <name>

<span data-ttu-id="d5fce-140">**Exclui um conjunto de disponibilidade dentro de um grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="d5fce-140">**Deletes one availability set within a resource group**</span></span>

    availset delete [options] <resource-group> <name>

## <a name="azure-config-commands-toomanage-your-local-settings"></a><span data-ttu-id="d5fce-141">configuração do Azure: comandos toomanage as configurações locais</span><span class="sxs-lookup"><span data-stu-id="d5fce-141">azure config: commands toomanage your local settings</span></span>
<span data-ttu-id="d5fce-142">**Lista definições de configuração de CLI do Azure**</span><span class="sxs-lookup"><span data-stu-id="d5fce-142">**List Azure CLI configuration settings**</span></span>

    config list [options]

<span data-ttu-id="d5fce-143">**Exclui uma definição de configuração**</span><span class="sxs-lookup"><span data-stu-id="d5fce-143">**Delete a config setting**</span></span>

    config delete [options] <name>

<span data-ttu-id="d5fce-144">**Atualiza uma definição de configuração**</span><span class="sxs-lookup"><span data-stu-id="d5fce-144">**Update a config setting**</span></span>

    config set <name> <value>

<span data-ttu-id="d5fce-145">**Conjuntos Olá CLI do Azure trabalhar de modo tooeither `arm` ou`asm`**</span><span class="sxs-lookup"><span data-stu-id="d5fce-145">**Sets hello Azure CLI working mode tooeither `arm` or `asm`**</span></span>

    config mode [options] <modename>


## <a name="azure-feature-commands-toomanage-account-features"></a><span data-ttu-id="d5fce-146">o recurso do Azure: recursos de conta toomanage de comandos</span><span class="sxs-lookup"><span data-stu-id="d5fce-146">azure feature: commands toomanage account features</span></span>
<span data-ttu-id="d5fce-147">**Lista todos os recursos disponíveis para sua assinatura**</span><span class="sxs-lookup"><span data-stu-id="d5fce-147">**List all features available for your subscription**</span></span>

    feature list [options]

<span data-ttu-id="d5fce-148">**Mostra um recurso**</span><span class="sxs-lookup"><span data-stu-id="d5fce-148">**Shows a feature**</span></span>

    feature show [options] <providerName> <featureName>

<span data-ttu-id="d5fce-149">**Registra um recurso visualizado de um provedor de recursos**</span><span class="sxs-lookup"><span data-stu-id="d5fce-149">**Registers a previewed feature of a resource provider**</span></span>

    feature register [options] <providerName> <featureName>

## <a name="azure-group-commands-toomanage-your-resource-groups"></a><span data-ttu-id="d5fce-150">grupo do Azure: comandos toomanage os grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="d5fce-150">azure group: Commands toomanage your resource groups</span></span>
<span data-ttu-id="d5fce-151">**Crie um grupos de recursos**</span><span class="sxs-lookup"><span data-stu-id="d5fce-151">**Creates a resource group**</span></span>

    group create [options] <name> <location>

<span data-ttu-id="d5fce-152">**Grupo de recursos do conjunto de marcas tooa**</span><span class="sxs-lookup"><span data-stu-id="d5fce-152">**Set tags tooa resource group**</span></span>

    group set [options] <name> <tags>

<span data-ttu-id="d5fce-153">**Exclui um grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="d5fce-153">**Deletes a resource group**</span></span>

    group delete [options] <name>

<span data-ttu-id="d5fce-154">**Lista os grupos de recursos Olá para sua assinatura**</span><span class="sxs-lookup"><span data-stu-id="d5fce-154">**Lists hello resource groups for your subscription**</span></span>

    group list [options]

<span data-ttu-id="d5fce-155">**Mostra um grupo de recursos para sua assinatura**</span><span class="sxs-lookup"><span data-stu-id="d5fce-155">**Shows a resource group for your subscription**</span></span>

    group show [options] <name>

<span data-ttu-id="d5fce-156">**Logs de grupo de recursos de toomanage de comandos**</span><span class="sxs-lookup"><span data-stu-id="d5fce-156">**Commands toomanage resource group logs**</span></span>

    group log show [options] [name]

<span data-ttu-id="d5fce-157">**Comandos toomanage sua implantação em um grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="d5fce-157">**Commands toomanage your deployment in a resource group**</span></span>

    group deployment create [options] [resource-group] [name]
    group deployment list [options] <resource-group> [state]
    group deployment show [options] <resource-group> [deployment-name]
    group deployment stop [options] <resource-group> [deployment-name]

<span data-ttu-id="d5fce-158">**Comandos toomanage o modelo de grupo de recursos de galeria ou local**</span><span class="sxs-lookup"><span data-stu-id="d5fce-158">**Commands toomanage your local or gallery resource group template**</span></span>

    group template list [options]
    group template show [options] <name>
    group template download [options] [name] [file]
    group template validate [options] <resource-group>

## <a name="azure-hdinsight-commands-toomanage-your-hdinsight-clusters"></a><span data-ttu-id="d5fce-159">hdinsight do Azure: comandos toomanage seus clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="d5fce-159">azure hdinsight: Commands toomanage your HDInsight clusters</span></span>
<span data-ttu-id="d5fce-160">**Comandos toocreate ou adicionar o arquivo de configuração de cluster tooa**</span><span class="sxs-lookup"><span data-stu-id="d5fce-160">**Commands toocreate or add tooa cluster configuration file**</span></span>

    hdinsight config create [options] <configFilePath> <overwrite>
    hdinsight config add-config-values [options] <configFilePath>
    hdinsight config add-script-action [options] <configFilePath>

<span data-ttu-id="d5fce-161">Exemplo: Crie um arquivo de configuração que contém um toorun de ação de script ao criar um cluster.</span><span class="sxs-lookup"><span data-stu-id="d5fce-161">Example: Create a configuration file that contains a script action toorun when creating a cluster.</span></span>

    hdinsight config create "C:\myFiles\configFile.config"
    hdinsight config add-script-action --configFilePath "C:\myFiles\configFile.config" --nodeType HeadNode --uri <scriptActionURI> --name myScriptAction --parameters "-param value"

<span data-ttu-id="d5fce-162">**Comando toocreate um cluster em um grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="d5fce-162">**Command toocreate a cluster in a resource group**</span></span>

    hdinsight cluster create [options] <clusterName>

<span data-ttu-id="d5fce-163">Exemplo: criar um Storm no cluster do Linux</span><span class="sxs-lookup"><span data-stu-id="d5fce-163">Example: Create a Storm on Linux cluster</span></span>

    azure hdinsight cluster create -g myarmgroup -l westus -y Linux --clusterType Storm --version 3.2 --defaultStorageAccountName mystorageaccount --defaultStorageAccountKey <defaultStorageAccountKey> --defaultStorageContainer mycontainer --userName admin --password <clusterPassword> --sshUserName sshuser --sshPassword <sshPassword> --workerNodeCount 1 myNewCluster01

    info:    Executing command hdinsight cluster create
    + Submitting hello request toocreate cluster...
    info:    hdinsight cluster create command OK

<span data-ttu-id="d5fce-164">Exemplo: criar um cluster com uma ação de script</span><span class="sxs-lookup"><span data-stu-id="d5fce-164">Example: Create a cluster with a script action</span></span>

    azure hdinsight cluster create -g myarmgroup -l westus -y Linux --clusterType Hadoop --version 3.2 --defaultStorageAccountName mystorageaccount --defaultStorageAccountKey <defaultStorageAccountKey> --defaultStorageContainer mycontainer --userName admin --password <clusterPassword> --sshUserName sshuser --sshPassword <sshPassword> --workerNodeCount 1 –configurationPath "C:\myFiles\configFile.config" myNewCluster01

    info:    Executing command hdinsight cluster create
    + Submitting hello request toocreate cluster...
    info:    hdinsight cluster create command OK

<span data-ttu-id="d5fce-165">Opções de parâmetro:</span><span class="sxs-lookup"><span data-stu-id="d5fce-165">Parameter options:</span></span>

    -h, --help                                                 output usage information
    -v, --verbose                                              use verbose output
    -vv                                                        more verbose with debug output
    --json                                                     use json output
    -g --resource-group <resource-group>                       hello name of hello resource group
    -c, --clusterName <clusterName>                            HDInsight cluster name
    -l, --location <location>                                  Data center location for hello cluster
    -y, --osType <osType>                                      HDInsight cluster operating system
    'Windows' or 'Linux'
    --version <version>                                        HDInsight cluster version
    --clusterType <clusterType>                                HDInsight cluster type.
    Hadoop | HBase | Spark | Storm
    --defaultStorageAccountName <storageAccountName>           Storage account url toouse for default HDInsight storage
    --defaultStorageAccountKey <storageAccountKey>             Key toohello storage account toouse for default HDInsight storage
    --defaultStorageContainer <storageContainer>               Container in hello storage account toouse for HDInsight default storage
    --headNodeSize <headNodeSize>                              (Optional) Head node size for hello cluster
    --workerNodeCount <workerNodeCount>                        Number of worker nodes toouse for hello cluster
    --workerNodeSize <workerNodeSize>                          (Optional) Worker node size for hello cluster)
    --zookeeperNodeSize <zookeeperNodeSize>                    (Optional) Zookeeper node size for hello cluster
    --userName <userName>                                      Cluster username
    --password <password>                                      Cluster password
    --sshUserName <sshUserName>                                SSH username (only for Linux clusters)
    --sshPassword <sshPassword>                                SSH password (only for Linux clusters)
    --sshPublicKey <sshPublicKey>                              SSH public key (only for Linux clusters)
    --rdpUserName <rdpUserName>                                RDP username (only for Windows clusters)
    --rdpPassword <rdpPassword>                                RDP password (only for Windows clusters)
    --rdpAccessExpiry <rdpAccessExpiry>                        RDP access expiry.
    For example 12/12/2015 (only for Windows clusters)
    --virtualNetworkId <virtualNetworkId>                      (Optional) Virtual network ID for hello cluster.
    Value is a GUID for Windows cluster and ARM resource ID for Linux cluster)
    --subnetName <subnetName>                                  (Optional) Subnet for hello cluster
    --additionalStorageAccounts <additionalStorageAccounts>    (Optional) Additional storage accounts.
    Can be multiple.
    In hello format of 'accountName#accountKey'.
    For example, --additionalStorageAccounts "acc1#key1;acc2#key2"
    --hiveMetastoreServerName <hiveMetastoreServerName>        (Optional) SQL Server name for hello external metastore for Hive
    --hiveMetastoreDatabaseName <hiveMetastoreDatabaseName>    (Optional) Database name for hello external metastore for Hive
    --hiveMetastoreUserName <hiveMetastoreUserName>            (Optional) Database username for hello external metastore for Hive
    --hiveMetastorePassword <hiveMetastorePassword>            (Optional) Database password for hello external metastore for Hive
    --oozieMetastoreServerName <oozieMetastoreServerName>      (Optional) SQL Server name for hello external metastore for Oozie
    --oozieMetastoreDatabaseName <oozieMetastoreDatabaseName>  (Optional) Database name for hello external metastore for Oozie
    --oozieMetastoreUserName <oozieMetastoreUserName>          (Optional) Database username for hello external metastore for Oozie
    --oozieMetastorePassword <oozieMetastorePassword>          (Optional) Database password for hello external metastore for Oozie
    --configurationPath <configurationPath>                    (Optional) HDInsight cluster configuration file path
    -s, --subscription <id>                                    hello subscription id
    --tags <tags>                                              Tags tooset toohello cluster.
    Can be multiple.
    In hello format of 'name=value'.
    Name is required and value is optional.
    For example, --tags tag1=value1;tag2


<span data-ttu-id="d5fce-166">**Comando toodelete um cluster**</span><span class="sxs-lookup"><span data-stu-id="d5fce-166">**Command toodelete a cluster**</span></span>

    hdinsight cluster delete [options] <clusterName>

<span data-ttu-id="d5fce-167">**Detalhes do comando tooshow cluster**</span><span class="sxs-lookup"><span data-stu-id="d5fce-167">**Command tooshow cluster details**</span></span>

    hdinsight cluster show [options] <clusterName>

<span data-ttu-id="d5fce-168">**Toolist de comando todos os clusters (em um grupo de recursos específico, se fornecida)**</span><span class="sxs-lookup"><span data-stu-id="d5fce-168">**Command toolist all clusters (in a specific resource group, if provided)**</span></span>

    hdinsight cluster list [options]

<span data-ttu-id="d5fce-169">**Comando tooresize um cluster**</span><span class="sxs-lookup"><span data-stu-id="d5fce-169">**Command tooresize a cluster**</span></span>

    hdinsight cluster resize [options] <clusterName> <targetInstanceCount>

<span data-ttu-id="d5fce-170">**Acesso de tooenable HTTP para um cluster de comando**</span><span class="sxs-lookup"><span data-stu-id="d5fce-170">**Command tooenable HTTP access for a cluster**</span></span>

    hdinsight cluster enable-http-access [options] <clusterName> <userName> <password>

<span data-ttu-id="d5fce-171">**Acesso de toodisable HTTP para um cluster de comando**</span><span class="sxs-lookup"><span data-stu-id="d5fce-171">**Command toodisable HTTP access for a cluster**</span></span>

    hdinsight cluster disable-http-access [options] <clusterName>

<span data-ttu-id="d5fce-172">**Comando tooenable acesso RDP para um cluster**</span><span class="sxs-lookup"><span data-stu-id="d5fce-172">**Command tooenable RDP access for a cluster**</span></span>

    hdinsight cluster enable-rdp-access [options] <clusterName> <rdpUserName> <rdpPassword> <rdpExpiryDate>

<span data-ttu-id="d5fce-173">**Acesso de toodisable HTTP para um cluster de comando**</span><span class="sxs-lookup"><span data-stu-id="d5fce-173">**Command toodisable HTTP access for a cluster**</span></span>

    hdinsight cluster disable-rdp-access [options] <clusterName>

## <a name="azure-insights-commands-related-toomonitoring-insights-events-alert-rules-autoscale-settings-metrics"></a><span data-ttu-id="d5fce-174">o Azure insights: comandos relacionados toomonitoring Insights (eventos, regras de alerta, configurações de dimensionamento automático, as métricas)</span><span class="sxs-lookup"><span data-stu-id="d5fce-174">azure insights: Commands related toomonitoring Insights (events, alert rules, autoscale settings, metrics)</span></span>
<span data-ttu-id="d5fce-175">**Recupera os logs de operação para uma assinatura, uma correlationId, um grupo de recursos, o recurso ou o provedor de recursos**</span><span class="sxs-lookup"><span data-stu-id="d5fce-175">**Retrieve operation logs for a subscription, a correlationId, a resource group, resource, or resource provider**</span></span>

    insights logs list [options]

## <a name="azure-location-commands-tooget-hello-available-locations-for-all-resource-types"></a><span data-ttu-id="d5fce-176">local do Azure: comandos locais disponíveis do tooget Olá para todos os tipos de recurso</span><span class="sxs-lookup"><span data-stu-id="d5fce-176">azure location: Commands tooget hello available locations for all resource types</span></span>
<span data-ttu-id="d5fce-177">**Lista os locais disponíveis Olá**</span><span class="sxs-lookup"><span data-stu-id="d5fce-177">**List hello available locations**</span></span>

    location list [options]

## <a name="azure-network-commands-toomanage-network-resources"></a><span data-ttu-id="d5fce-178">rede do Azure: comandos toomanage recursos de rede</span><span class="sxs-lookup"><span data-stu-id="d5fce-178">azure network: Commands toomanage network resources</span></span>
<span data-ttu-id="d5fce-179">**Comandos toomanage as redes virtuais**</span><span class="sxs-lookup"><span data-stu-id="d5fce-179">**Commands toomanage virtual networks**</span></span>

    network vnet create [options] <resource-group> <name> <location>
<span data-ttu-id="d5fce-180">Cria uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="d5fce-180">Creates a virtual network.</span></span> <span data-ttu-id="d5fce-181">Olá exemplo a seguir é criar uma rede virtual denominado newvnet para myresourcegroup do grupo de recursos na região Oeste dos EUA de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5fce-181">In hello following example we create a virtual network named newvnet for resource group myresourcegroup in hello West US region.</span></span>

    azure network vnet create myresourcegroup newvnet "west us"
    info:    Executing command network vnet create
    + Looking up virtual network "newvnet"
    + Creating virtual network "newvnet"
     Loading virtual network state
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet
    data:    Name:                 newvnet
    data:    Type:                 Microsoft.Network/virtualNetworks
    data:    Location:             westus
    data:    Tags:
    data:    Provisioning state:   Succeeded
    data:    Address prefixes:
    data:     10.0.0.0/8
    data:    DNS servers:
    data:    Subnets:
    data:
    info:    network vnet create command OK


<span data-ttu-id="d5fce-182">Opções de parâmetro:</span><span class="sxs-lookup"><span data-stu-id="d5fce-182">Parameter options:</span></span>

     -h, --help                                 output usage information
     -v, --verbose                              use verbose output
    --json                                     use json output
     -g, --resource-group <resource-group>      hello name of hello resource group
     -n, --name <name>                          hello name of hello virtual network
     -l, --location <location>                  hello location
     -a, --address-prefixes <address-prefixes>  hello comma separated list of address prefixes for this virtual network
      For example -a 10.0.0.0/24,10.0.1.0/24.
      Default value is 10.0.0.0/8

    -d, --dns-servers <dns-servers>            hello comma separated list of DNS servers IP addresses
     -t, --tags <tags>                          hello tags set on this virtual network.
      Can be multiple. In hello format of "name=value".
      Name is required and value is optional.
      For example, -t tag1=value1;tag2
     -s, --subscription <subscription>          hello subscription identifier
<BR>

    network vnet set [options] <resource-group> <name>

<span data-ttu-id="d5fce-183">Atualiza uma configuração de rede virtual dentro de um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d5fce-183">Updates a virtual network configuration within a resource group.</span></span>

    azure network vnet set myresourcegroup newvnet

    info:    Executing command network vnet set
    + Looking up virtual network "newvnet"
    + Updating virtual network "newvnet"
    + Loading virtual network state
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet
    data:    Name:                 newvnet
    data:    Type:                 Microsoft.Network/virtualNetworks
    data:    Location:             westus
    data:    Tags:
    data:    Provisioning state:   Succeeded
    data:    Address prefixes:
    data:     10.0.0.0/8
    data:    DNS servers:
    data:    Subnets:
    data:
    info:    network vnet set command OK

<span data-ttu-id="d5fce-184">Opções de parâmetro:</span><span class="sxs-lookup"><span data-stu-id="d5fce-184">Parameter options:</span></span>

       -h, --help                                 output usage information
       -v, --verbose                              use verbose output
       --json                                     use json output
       -g, --resource-group <resource-group>      hello name of hello resource group
       -n, --name <name>                          hello name of hello virtual network
       -a, --address-prefixes <address-prefixes>  hello comma separated list of address prefixes for this virtual network.
        For example -a 10.0.0.0/24,10.0.1.0/24.
        This list will be appended toohello current list of address prefixes.
        hello address prefixes in this list should not overlap between them.
        hello address prefixes in this list should not overlap with existing address prefixes in hello vnet.

       -d, --dns-servers [dns-servers]            hello comma separated list of DNS servers IP addresses.
        This list will be appended toohello current list of DNS server IP addresses.

       -t, --tags <tags>                          hello tags set on this virtual network.
        Can be multiple. In hello format of "name=value".
        Name is required and value is optional. For example, -t tag1=value1;tag2.
        This list will be appended toohello current list of tags

       --no-tags                                  remove all existing tags
       -s, --subscription <subscription>          hello subscription identifier
<BR>

    network vnet list [options] <resource-group>

<span data-ttu-id="d5fce-185">comando Olá lista todas as redes virtuais em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d5fce-185">hello command lists all virtual networks in a resource group.</span></span>

    C:\>azure network vnet list myresourcegroup

    info:    Executing command network vnet list
    + Listing virtual networks
        data:    ID
       Name      Location  Address prefixes  DNS servers
    data:    -------------------------------------------------------------------
    ------  --------  --------  ----------------  -----------
    data:    /subscriptions/###############################/resourceGroups/
    wvnet   newvnet   westus    10.0.0.0/8
    info:    network vnet list command OK

<span data-ttu-id="d5fce-186">Opções de parâmetro:</span><span class="sxs-lookup"><span data-stu-id="d5fce-186">Parameter options:</span></span>

      -h, --help                             output usage information
      -v, --verbose                          use verbose output
      --json                                 use json output
      -g, --resource-group <resource-group>  hello name of hello resource group
      -s, --subscription <subscription>      hello subscription identifier

<BR>

    network vnet show [options] <resource-group> <name>
<span data-ttu-id="d5fce-187">comando de saudação mostra as propriedades de rede virtual de saudação em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d5fce-187">hello command shows hello virtual network properties in a resource group.</span></span>

    azure network vnet show -g myresourcegroup -n newvnet

    info:    Executing command network vnet show
    + Looking up virtual network "newvnet"
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet
    data:    Name:                 newvnet
    data:    Type:                 Microsoft.Network/virtualNetworks
    data:    Location:             westus
    data:    Tags:
    data:    Provisioning state:   Succeeded
    data:    Address prefixes:
    data:     10.0.0.0/8
    data:    DNS servers:
    data:    Subnets:
    data:
    info:    network vnet show command OK
<BR>

    network vnet delete [options] <resource-group> <name>
<span data-ttu-id="d5fce-188">comando Olá remove uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="d5fce-188">hello command removes a virtual network.</span></span>

    azure network vnet delete myresourcegroup newvnetX

    info:    Executing command network vnet delete
    + Looking up virtual network "newvnetX"
    Delete virtual network newvnetX? [y/n] y
    + Deleting virtual network "newvnetX"
    info:    network vnet delete command OK

<span data-ttu-id="d5fce-189">Opções de parâmetro:</span><span class="sxs-lookup"><span data-stu-id="d5fce-189">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  hello name of hello resource group
     -n, --name <name>                      hello name of hello virtual network
     -q, --quiet                            quiet mode, do not ask for delete confirmation
     -s, --subscription <subscription>      hello subscription identifier


<span data-ttu-id="d5fce-190">**Sub-redes de rede virtual toomanage comandos**</span><span class="sxs-lookup"><span data-stu-id="d5fce-190">**Commands toomanage virtual network subnets**</span></span>

    network vnet subnet create [options] <resource-group> <vnet-name> <name>

<span data-ttu-id="d5fce-191">Adiciona outro subrede tooan rede virtual existente.</span><span class="sxs-lookup"><span data-stu-id="d5fce-191">Adds another subnet tooan existing virtual network.</span></span>

    azure network vnet subnet create -g myresourcegroup --vnet-name newvnet -n subnet --address-prefix 10.0.1.0/24

    info:    Executing command network vnet subnet create
    + Looking up hello subnet "subnet"
    + Creating subnet "subnet"
    + Looking up hello subnet "subnet"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet
    data:    Name:                      subnet
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet create command OK

<span data-ttu-id="d5fce-192">Opções de parâmetro:</span><span class="sxs-lookup"><span data-stu-id="d5fce-192">Parameter options:</span></span>

     -h, --help                                                       output usage information
     -v, --verbose                                                    use verbose output
         --json                                                           use json output
     -g, --resource-group <resource-group>                            hello name of hello resource group
     -e, --vnet-name <vnet-name>                                      hello name of hello virtual network
     -n, --name <name>                                                hello name of hello subnet
     -a, --address-prefix <address-prefix>                            hello address prefix
     -w, --network-security-group-id <network-security-group-id>      hello network security group identifier.
           e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/networkSecurityGroups/<nsg-name>
     -o, --network-security-group-name <network-security-group-name>  hello network security group name
     -s, --subscription <subscription>                                hello subscription identifier

<BR>

    network vnet subnet set [options] <resource-group> <vnet-name> <name>

<span data-ttu-id="d5fce-193">Define uma sub-rede de rede virtual específica dentro de um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d5fce-193">Sets a specific virtual network subnet within a resource group.</span></span>

    C:\>azure network vnet subnet set -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet set
    + Looking up hello subnet "subnet1"
    + Setting subnet "subnet1"
    + Looking up hello subnet "subnet1"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet1
    data:    Name:                      subnet1
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet set command OK
<BR>

    network vnet subnet list [options] <resource-group> <vnet-name>

<span data-ttu-id="d5fce-194">Lista todas as sub-redes de rede virtual Olá para uma rede virtual específica dentro de um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d5fce-194">Lists all hello virtual network subnets for a specific virtual network within a resource group.</span></span>

    azure network vnet subnet set -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet set
    + Looking up hello subnet "subnet1"
    + Setting subnet "subnet1"
    + Looking up hello subnet "subnet1"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet1
    data:    Name:                      subnet1
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet set command OK
<BR>

    network vnet subnet show [options] <resource-group> <vnet-name> <name>
<span data-ttu-id="d5fce-195">Exibe as propriedades de sub-rede da rede virtual</span><span class="sxs-lookup"><span data-stu-id="d5fce-195">Displays virtual network subnet properties</span></span>

    azure network vnet subnet show -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet show
    + Looking up hello subnet "subnet1"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft
    .Network/virtualNetworks/newvnet/subnets/subnet1
    data:    Name:                      subnet1
    data:    Type:                      Microsoft.Network/virtualNetworks/subnets
    data:    Provisioning state:        Succeeded
    data:    Address prefix:            10.0.1.0/24
    info:    network vnet subnet show command OK

<span data-ttu-id="d5fce-196">Opções de parâmetro:</span><span class="sxs-lookup"><span data-stu-id="d5fce-196">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -e, --vnet-name <vnet-name>            hello name of hello virtual network
    -n, --name <name>                      hello name of hello subnet
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network vnet subnet delete [options] <resource-group> <vnet-name> <subnet-name>
<span data-ttu-id="d5fce-197">Remove uma sub-rede de uma rede virtual existente.</span><span class="sxs-lookup"><span data-stu-id="d5fce-197">Removes a subnet from an existing virtual network.</span></span>

    azure network vnet subnet delete -g myresourcegroup --vnet-name newvnet -n subnet1

    info:    Executing command network vnet subnet delete
    + Looking up hello subnet "subnet1"
    Delete subnet "subnet1"? [y/n] y
    + Deleting subnet "subnet1"
    info:    network vnet subnet delete command OK

<span data-ttu-id="d5fce-198">Opções de parâmetro:</span><span class="sxs-lookup"><span data-stu-id="d5fce-198">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  hello name of hello resource group
     -e, --vnet-name <vnet-name>            hello name of hello virtual network
     -n, --name <name>                      hello subnet name
     -s, --subscription <subscription>      hello subscription identifier
     -q, --quiet                            quiet mode, do not ask for delete confirmation

<span data-ttu-id="d5fce-199">**Balanceadores de carga toomanage comandos**</span><span class="sxs-lookup"><span data-stu-id="d5fce-199">**Commands toomanage load balancers**</span></span>

    network lb create [options] <resource-group> <name> <location>
<span data-ttu-id="d5fce-200">Cria um conjunto de balanceadores de carga.</span><span class="sxs-lookup"><span data-stu-id="d5fce-200">Creates a load balancer set.</span></span>

    azure network lb create -g myresourcegroup -n mylb -l westus

    info:    Executing command network lb create
    + Looking up hello load balancer "mylb"
    + Creating load balancer "mylb"
    + Looking up hello load balancer "mylb"
    data:    Id:                           /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb
    data:    Name:                         mylb
    data:    Type:                         Microsoft.Network/loadBalancers
    data:    Location:                     westus
    data:    Provisioning state:           Succeeded
    info:    network lb create command OK

<span data-ttu-id="d5fce-201">Opções de parâmetro:</span><span class="sxs-lookup"><span data-stu-id="d5fce-201">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -n, --name <name>                      hello name of hello load balancer
    -l, --location <location>              hello location
    -t, --tags <tags>                      hello list of tags.
     Can be multiple. In hello format of "name=value".
     Name is required and value is optional. For example, -t tag1=value1;tag2
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb list [options] <resource-group>
<span data-ttu-id="d5fce-202">Lista os recursos do balanceador de carga dentro de um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d5fce-202">Lists Load balancer resources within a resource group.</span></span>

    azure network lb list myresourcegroup

    info:    Executing command network lb list
    + Getting hello load balancers
    data:    Name  Location
    data:    ----  --------
    data:    mylb  westus
    info:    network lb list command OK

<span data-ttu-id="d5fce-203">Opções de parâmetro:</span><span class="sxs-lookup"><span data-stu-id="d5fce-203">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb show [options] <resource-group> <name>

<span data-ttu-id="d5fce-204">Exibe informações do balanceador de carga de um balanceador de carga específico dentro de um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="d5fce-204">Displays load balancer information of a specific load balancer within a resource group</span></span>

    azure network lb show myresourcegroup mylb -v

    info:    Executing command network lb show
    verbose: Looking up hello load balancer "mylb"
    data:    Id:                           /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb
    data:    Name:                         mylb
    data:    Type:                         Microsoft.Network/loadBalancers
    data:    Location:                     westus
    data:    Provisioning state:           Succeeded
    info:    network lb show command OK

<span data-ttu-id="d5fce-205">Opções de parâmetro:</span><span class="sxs-lookup"><span data-stu-id="d5fce-205">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -n, --name <name>                      hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier

<BR>

    network lb delete [options] <resource-group> <name>

<span data-ttu-id="d5fce-206">Exclui recursos do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="d5fce-206">Delete load balancer resources.</span></span>

    azure network lb delete  myresourcegroup mylb

    info:    Executing command network lb delete
    + Looking up hello load balancer "mylb"
    Delete load balancer "mylb"? [y/n] y
    + Deleting load balancer "mylb"
    info:    network lb delete command OK

<span data-ttu-id="d5fce-207">Opções de parâmetro:</span><span class="sxs-lookup"><span data-stu-id="d5fce-207">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  hello name of hello resource group
     -n, --name <name>                      hello name of hello load balancer
     -q, --quiet                            quiet mode, do not ask for delete confirmation
     -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="d5fce-208">**Testes de toomanage de comandos de um balanceador de carga**</span><span class="sxs-lookup"><span data-stu-id="d5fce-208">**Commands toomanage probes of a load balancer**</span></span>

    network lb probe create [options] <resource-group> <lb-name> <name>

<span data-ttu-id="d5fce-209">Crie a configuração de investigação de saudação para status de integridade no balanceador de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5fce-209">Create hello probe configuration for health status in hello load balancer.</span></span> <span data-ttu-id="d5fce-210">Tenha em mente toorun esse comando, o balanceador de carga requer um recurso de ip de front-end (Check-out tooassign do comando "azure rede front-end-ip" um balanceador de tooload de endereço ip).</span><span class="sxs-lookup"><span data-stu-id="d5fce-210">Keep in mind toorun this command, your load balancer requires a frontend-ip resource (Check out command "azure network frontend-ip" tooassign an ip address tooload balancer).</span></span>

    azure network lb probe create -g myresourcegroup --lb-name mylb -n mylbprobe --protocol tcp --port 80 -i 300

    info:    Executing command network lb probe create
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    info:    network lb probe create command OK

<span data-ttu-id="d5fce-211">Opções de parâmetro:</span><span class="sxs-lookup"><span data-stu-id="d5fce-211">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello probe
    -p, --protocol <protocol>              hello probe protocol
    -o, --port <port>                      hello probe port
    -f, --path <path>                      hello probe path
    -i, --interval <interval>              hello probe interval in seconds
    -c, --count <count>                    hello number of probes
    -s, --subscription <subscription>      hello subscription identifier

<BR>

    network lb probe set [options] <resource-group> <lb-name> <name>

<span data-ttu-id="d5fce-212">Atualiza uma investigação do balanceador de carga existente com novos valores para o mesmo.</span><span class="sxs-lookup"><span data-stu-id="d5fce-212">Updates an existing load balancer probe with new values for it.</span></span>

    azure network lb probe set -g myresourcegroup -l mylb -n mylbprobe -p mylbprobe1 -p TCP -o 443 -i 300

    info:    Executing command network lb probe set
        + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    info:    network lb probe set command OK

<span data-ttu-id="d5fce-213">Opções de parâmetro</span><span class="sxs-lookup"><span data-stu-id="d5fce-213">Parameter options</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello probe
    -e, --new-probe-name <new-probe-name>  hello new name of hello probe
    -p, --protocol <protocol>              hello new value for probe protocol
    -o, --port <port>                      hello new value for probe port
    -f, --path <path>                      hello new value for probe path
    -i, --interval <interval>              hello new value for probe interval in seconds
    -c, --count <count>                    hello new value for number of probes
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb probe list [options] <resource-group> <lb-name>

<span data-ttu-id="d5fce-214">Propriedades de investigação de saudação da lista para um conjunto de Balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="d5fce-214">List hello probe properties for a load balancer set.</span></span>

    C:\>azure network lb probe list -g myresourcegroup -l mylb

    info:    Executing command network lb probe list
    + Looking up hello load balancer "mylb"
    data:    Name       Protocol  Port  Path  Interval  Count
    data:    ---------  --------  ----  ----  --------  -----
    data:    mylbprobe  Tcp       443         300       2
    info:    network lb probe list command OK

<span data-ttu-id="d5fce-215">Opções de parâmetro:</span><span class="sxs-lookup"><span data-stu-id="d5fce-215">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier


    network lb probe delete [options] <resource-group> <lb-name> <name>
<span data-ttu-id="d5fce-216">Remove a investigação Olá criada Olá balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="d5fce-216">Removes hello probe created for hello load balancer.</span></span>

    azure network lb probe delete -g myresourcegroup -l mylb -n mylbprobe

    info:    Executing command network lb probe delete
    + Looking up hello load balancer "mylb"
    Delete a probe "mylbprobe?" [y/n] y
    + Updating load balancer "mylb"
    info:    network lb probe delete command OK

<span data-ttu-id="d5fce-217">**Configurações de ip de front-end de toomanage de comandos de um balanceador de carga**</span><span class="sxs-lookup"><span data-stu-id="d5fce-217">**Commands toomanage frontend ip configurations of a load balancer**</span></span>

    network lb frontend-ip create [options] <resource-group> <lb-name> <name>
<span data-ttu-id="d5fce-218">Cria um tooan de configuração de IP de front-end existente conjunto do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="d5fce-218">Creates a frontend IP configuration tooan existing load balancer set.</span></span>

    azure network lb frontend-ip create -g myresourcegroup --lb-name mylb -n myfrontendip -o Dynamic -e subnet -m newvnet

    info:    Executing command network lb frontend-ip create
    + Looking up hello load balancer "mylb"
    + Looking up hello subnet "subnet"
    + Creating frontend IP configuration "myfrontendip"
    + Looking up hello load balancer "mylb"
    data:    Id:                           /subscriptions/###############################/resourceGroups/Myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb
    /frontendIPConfigurations/myfrontendip
    data:    Name:                         myfrontendip
    data:    Type:                         Microsoft.Network/loadBalancers/frontendIPConfigurations
    data:    Provisioning state:           Succeeded
    data:    Private IP allocation method: Dynamic
    data:    Private IP address:           10.0.1.4
    data:    Subnet:                       id=/subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/virtualNetworks/newvnet/subnets/subnet
    data:    Public IP address:
    data:    Inbound NAT rules
    data:    Outbound NAT rules
    data:    Load balancing rules
    data:
    info:    network lb frontend-ip create command OK

<BR>

    network lb frontend-ip set [options] <resource-group> <lb-name> <name>

<span data-ttu-id="d5fce-219">Atualizações de uma configuração existente de um front-end IP.hello comando a seguir adiciona um IP público chamado mypubip5 tooan existente carga balanceador IP front-end denominado myfrontendip.</span><span class="sxs-lookup"><span data-stu-id="d5fce-219">Updates an existing configuration of a frontend IP.hello command below adds a public IP called mypubip5 tooan existing load balancer frontend IP named myfrontendip.</span></span>

    azure network lb frontend-ip set -g myresourcegroup --lb-name mylb -n myfrontendip -i mypubip5

    info:    Executing command network lb frontend-ip set
    + Looking up hello load balancer "mylb"
    + Looking up hello public ip "mypubip5"
    + Updating load balancer "mylb"
    + Looking up hello load balancer "mylb"
    data:    Id:                           /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Name:                         myfrontendip
    data:    Type:                         Microsoft.Network/loadBalancers/frontendIPConfigurations
    data:    Provisioning state:           Succeeded
    data:    Private IP allocation method: Dynamic
    data:    Private IP address:
    data:    Subnet:
    data:    Public IP address:            id=/subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/publicIPAddresses/mypubip5
    data:    Inbound NAT rules
    data:    Outbound NAT rules
    data:    Load balancing rules
    data:
    info:    network lb frontend-ip set command OK

<span data-ttu-id="d5fce-220">Opções de parâmetro:</span><span class="sxs-lookup"><span data-stu-id="d5fce-220">Parameter options:</span></span>

    -h, --help                                                         output usage information
    -v, --verbose                                                      use verbose output
    --json                                                             use json output
    -g, --resource-group <resource-group>                              hello name of hello resource group
    -l, --lb-name <lb-name>                                            hello name of hello load balancer
    -n, --name <name>                                                  hello name of hello frontend ip configuration
    -a, --private-ip-address <private-ip-address>                      hello private ip address
    -o, --private-ip-allocation-method <private-ip-allocation-method>  hello private ip allocation method [Static, Dynamic]
    -u, --public-ip-id <public-ip-id>                                  hello public ip identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/publicIPAddresses/<public-ip-name>
    -i, --public-ip-name <public-ip-name>                              hello public ip name.
    This public ip must exist in hello same resource group as hello lb.
    Please use public-ip-id if that is not hello case.
    -b, --subnet-id <subnet-id>                                        hello subnet id.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/VirtualNetworks/<vnet-name>/subnets/<subnet-name>
    -e, --subnet-name <subnet-name>                                    hello subnet name
    -m, --vnet-name <vnet-name>                                        hello virtual network name.
    This virtual network must exist in hello same resource group as hello lb.
    Please use subnet-id if that is not hello case.
    -s, --subscription <subscription>                                  hello subscription identifier

<BR>

    network lb frontend-ip list [options] <resource-group> <lb-name>

<span data-ttu-id="d5fce-221">Lista todos os recursos IP de front-end de saudação configurados Olá balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="d5fce-221">Lists all hello frontend IP resources configured for hello load balancer.</span></span>

    azure network lb frontend-ip list -g myresourcegroup -l mylb

    info:    Executing command network lb frontend-ip list
    + Looking up hello load balancer "mylb"
    data:    Name         Provisioning state  Private IP allocation method  Subnet
    data:    -----------  ------------------  ----------------------------  ------
    data:    myprivateip  Succeeded           Dynamic
    info:    network lb frontend-ip list command OK

<span data-ttu-id="d5fce-222">Opções de parâmetro:</span><span class="sxs-lookup"><span data-stu-id="d5fce-222">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb frontend-ip delete [options] <resource-group> <lb-name> <name>
<span data-ttu-id="d5fce-223">Exclui Olá front-end IP objeto associado tooload balanceador</span><span class="sxs-lookup"><span data-stu-id="d5fce-223">Deletes hello frontend IP object associated tooload balancer</span></span>

    network lb frontend-ip delete -g myresourcegroup -l mylb -n myfrontendip
    info:    Executing command network lb frontend-ip delete
    + Looking up hello load balancer "mylb"
    Delete frontend ip configuration "myfrontendip"? [y/n] y
    + Updating load balancer "mylb"

<span data-ttu-id="d5fce-224">Opções de parâmetro:</span><span class="sxs-lookup"><span data-stu-id="d5fce-224">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello frontend ip configuration
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="d5fce-225">**Comandos toomanage pools de endereços de back-end de um balanceador de carga**</span><span class="sxs-lookup"><span data-stu-id="d5fce-225">**Commands toomanage backend address pools of a load balancer**</span></span>

    network lb address-pool create [options] <resource-group> <lb-name> <name>

<span data-ttu-id="d5fce-226">Cria um pool de endereços de back-end para um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="d5fce-226">Create a backend address pool for a load balancer.</span></span>

    azure network lb address-pool create -g myresourcegroup --lb-name mylb -n myaddresspool

    info:    Executing command network lb address-pool create
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    + Looking up hello load balancer "mylb"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourgroup/providers/Microso.Network/loadBalancers/mylb/backendAddressPools/myaddresspool
    data:    Name:                      myaddresspool
    data:    Type:                      Microsoft.Network/loadBalancers/backendAddressPools
    data:    Provisioning state:        Succeeded
    data:    Backend IP configurations:
    data:    Load balancing rules:
    data:
    info:    network lb address-pool create command OK

<span data-ttu-id="d5fce-227">Opções de parâmetro:</span><span class="sxs-lookup"><span data-stu-id="d5fce-227">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello backend address pool
    -s, --subscription <subscription>      hello subscription identifier

<BR>

    network lb address-pool list [options] <resource-group> <lb-name>

<span data-ttu-id="d5fce-228">Lista o intervalo de pool de endereços IP de back-end para um grupo de recursos específicos</span><span class="sxs-lookup"><span data-stu-id="d5fce-228">List backend IP address pool range for a specific resource group</span></span>

    azure network lb address-pool list -g myresourcegroup -l mylb

    info:    Executing command network lb address-pool list
    + Looking up hello load balancer "mylb"
    data:    Name           Provisioning state
    data:    -------------  ------------------
    data:    mybackendpool  Succeeded
    info:    network lb address-pool list command OK

<span data-ttu-id="d5fce-229">Opções de parâmetro:</span><span class="sxs-lookup"><span data-stu-id="d5fce-229">Parameter options:</span></span>

     -h, --help                             output usage information
     -v, --verbose                          use verbose output
     --json                                 use json output
     -g, --resource-group <resource-group>  hello name of hello resource group
     -l, --lb-name <lb-name>                hello name of hello load balancer
     -s, --subscription <subscription>      hello subscription identifier

<BR>
    <span data-ttu-id="d5fce-230">excluir o pool de endereços de balanceamento de carga de rede [Opções] < resource-group >< lb-name ><name></span><span class="sxs-lookup"><span data-stu-id="d5fce-230">network lb address-pool delete [options] <resource-group> <lb-name> <name></span></span>

<span data-ttu-id="d5fce-231">Remove o recurso de intervalo de pool IP do hello back-end do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="d5fce-231">Removes hello backend IP pool range resource from load balancer.</span></span>

    azure network lb address-pool delete -g myresourcegroup -l mylb -n mybackendpool

    info:    Executing command network lb address-pool delete
    + Looking up hello load balancer "mylb"
    Delete backend address pool "mybackendpool"? [y/n] y
    + Updating load balancer "mylb"
    info:    network lb address-pool delete command OK

<span data-ttu-id="d5fce-232">Opções de parâmetro:</span><span class="sxs-lookup"><span data-stu-id="d5fce-232">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello backend address pool
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="d5fce-233">**Comandos toomanage regras de Balanceador de carga**</span><span class="sxs-lookup"><span data-stu-id="d5fce-233">**Commands toomanage load balancer rules**</span></span>

    network lb rule create [options] <resource-group> <lb-name> <name>
<span data-ttu-id="d5fce-234">Crie regras para o balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="d5fce-234">Create load balancer rules.</span></span>

<span data-ttu-id="d5fce-235">Você pode criar uma regra de Balanceador de carga Configurando o ponto de extremidade do hello front-end do balanceador de carga de saudação e Olá back-end endereço pool intervalo tooreceive Olá tráfego de rede.</span><span class="sxs-lookup"><span data-stu-id="d5fce-235">You can create a load balancer rule configuring hello frontend endpoint for hello load balancer and hello backend address pool range tooreceive hello incoming network traffic.</span></span> <span data-ttu-id="d5fce-236">As configurações também incluem portas Olá para o ponto de extremidade IP de front-end e portas para o intervalo de pool de endereços de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5fce-236">Settings also include hello ports for frontend IP endpoint and ports for hello backend address pool range.</span></span>

<span data-ttu-id="d5fce-237">Olá exemplo a seguir mostra como regra toocreate um balanceador de carga, ponto de extremidade de front-end de saudação escutando tooport 80 tooport 8080 para o intervalo de pool de endereços de back-end de saudação de envio de tráfego de rede de TCP e o balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="d5fce-237">hello following example shows how toocreate a load balancer rule,  hello frontend endpoint listening tooport 80 TCP and load balancing network traffic sending tooport 8080 for hello backend address pool range.</span></span>

    azure network lb rule create -g myresourcegroup -l mylb -n mylbrule -p tcp -f 80 -b 8080 -i 10


    info:    Executing command network lb rule create
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    + Loading rule state
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/loadBalancingRules/mylbrule
    data:    Name:                      mylbrule
    data:    Type:                      Microsoft.Network/loadBalancers/loadBalancingRules
    data:    Provisioning state:        Succeeded
    data:    Frontend IP configuration: /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Backend address pool:      id=/subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/mybackendpool
    data:    Protocol:                  Tcp
    data:    Frontend port:             80
    data:    Backend port:              8080
    data:    Enable floating IP:        false
    data:    Idle timeout in minutes:   10
    data:    Probes
    data:
    info:    network lb rule create command OK

<BR>

    network lb rule set [options] <resource-group> <lb-name> <name>

<span data-ttu-id="d5fce-238">Atualiza uma regra de balanceador de carga existente definida em um grupo de recursos específico.</span><span class="sxs-lookup"><span data-stu-id="d5fce-238">Updates an existing load balancer rule set in a specific resource group.</span></span> <span data-ttu-id="d5fce-239">Olá exemplo a seguir, alteramos o nome da regra de saudação do mylbrule toomynewlbrule.</span><span class="sxs-lookup"><span data-stu-id="d5fce-239">In hello following example, we changed hello rule name from mylbrule toomynewlbrule.</span></span>

    azure network lb rule set -g myresourcegroup -l mylb -n mylbrule -r mynewlbrule -p tcp -f 80 -b 8080 -i 10 -t myfrontendip -o mybackendpool

    info:    Executing command network lb rule set
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    + Loading rule state
    data:    Id:                        /subscriptions/###############################/resourceGroups/yresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/loadBalancingRules/mynewlbrule
    data:    Name:                      mynewlbrule
    data:    Type:                      Microsoft.Network/loadBalancers/loadBalancingRules
    data:    Provisioning state:        Succeeded
    data:    Frontend IP configuration: /subscriptions/###############################/resourceGroups/yresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Backend address pool:      id=/subscriptions/###############################/resourceGroups/yresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/mybackendpool
    data:    Protocol:                  Tcp
    data:    Frontend port:             80
    data:    Backend port:              8080
    data:    Enable floating IP:        false
    data:    Idle timeout in minutes:   10
    data:    Probes
    data:
    info:    network lb rule set command OK

<span data-ttu-id="d5fce-240">Opções de parâmetro:</span><span class="sxs-lookup"><span data-stu-id="d5fce-240">Parameter options:</span></span>

    -h, --help                                         output usage information
    -v, --verbose                                      use verbose output
    --json                                             use json output
    -g, --resource-group <resource-group>              hello name of hello resource group
    -l, --lb-name <lb-name>                            hello name of hello load balancer
    -n, --name <name>                                  hello name of hello rule
    -r, --new-rule-name <new-rule-name>                new rule name
    -p, --protocol <protocol>                          hello rule protocol
    -f, --frontend-port <frontend-port>                hello frontend port
    -b, --backend-port <backend-port>                  hello backend port
    -e, --enable-floating-ip <enable-floating-ip>      enable floating point ip
    -i, --idle-timeout <idle-timeout>                  hello idle timeout in minutes
    -a, --probe-name [probe-name]                      hello name of hello probe defined in hello same load balancer
    -t, --frontend-ip-name <frontend-ip-name>          hello name of hello frontend ip configuration in hello same load balancer
    -o, --backend-address-pool <backend-address-pool>  name of hello backend address pool defined in hello same load balancer
    -s, --subscription <subscription>                  hello subscription identifier


    network lb rule list [options] <resource-group> <lb-name>

<span data-ttu-id="d5fce-241">Lista todas as regras do balanceador de carga configuradas para um balanceador de carga em um grupo de recursos específico.</span><span class="sxs-lookup"><span data-stu-id="d5fce-241">Lists all load balancer rules configured for a load balancer in a specific resource group.</span></span>

    azure network lb rule list -g myresourcegroup -l mylb

    info:    Executing command network lb rule list
    + Looking up hello load balancer "mylb"
    data:    Name         Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes  Backend address pool  Probe data

    data:    mynewlbrule  Succeeded           Tcp       80             8080          false               10                       /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/backendAddressPools/mybackendpool
    info:    network lb rule list command OK

<span data-ttu-id="d5fce-242">Opções de parâmetro:</span><span class="sxs-lookup"><span data-stu-id="d5fce-242">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier

    network lb rule delete [options] <resource-group> <lb-name> <name>

<span data-ttu-id="d5fce-243">Exclui uma regra de balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="d5fce-243">Deletes a load balancer rule.</span></span>

    azure network lb rule delete -g myresourcegroup -l mylb -n mynewlbrule

    info:    Executing command network lb rule delete
    + Looking up hello load balancer "mylb"
    Delete load balancing rule mynewlbrule? [y/n] y
    + Updating load balancer "mylb"
    info:    network lb rule delete command OK

<span data-ttu-id="d5fce-244">Opções de parâmetro:</span><span class="sxs-lookup"><span data-stu-id="d5fce-244">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello rule
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="d5fce-245">**Regras NAT de entrada do balanceador de carga toomanage comandos**</span><span class="sxs-lookup"><span data-stu-id="d5fce-245">**Commands toomanage load balancer inbound NAT rules**</span></span>

    network lb inbound-nat-rule create [options] <resource-group> <lb-name> <name>
<span data-ttu-id="d5fce-246">Cria uma regra de NAT de entrada para o balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="d5fce-246">Creates an inbound NAT rule for load balancer.</span></span>

<span data-ttu-id="d5fce-247">Em Olá o exemplo a seguir criamos uma regra NAT de IP de front-end (que foi anteriormente definida usando o comando hello "ip de front-end de rede do azure") com uma porta de escuta de entrada e a porta de saída que balanceador de carga Olá usa tráfego de rede toosend hello.</span><span class="sxs-lookup"><span data-stu-id="d5fce-247">In hello following example  we created a NAT rule from frontend IP (which was previously defined using hello "azure network frontend-ip" command) with an inbound listening port and outbound port that hello load balancer uses toosend hello network traffic.</span></span>

    azure network lb inbound-nat-rule create -g myresourcegroup -l mylb -n myinboundnat -p tcp -f 80 -b 8080 -i myfrontendip

    info:    Executing command network lb inbound-nat-rule create
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    + Looking up hello load balancer "mylb"
    data:    Id:                        /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/inboundNatRules/myinboundnat
    data:    Name:                      myinboundnat
    data:    Type:                      Microsoft.Network/loadBalancers/inboundNatRules
    data:    Provisioning state:        Succeeded
    data:    Frontend IP Configuration: id=/subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Backend IP configuration
    data:    Protocol                   Tcp
    data:    Frontend port              80
    data:    Backend port               8080
    data:    Enable floating IP         false
    info:    network lb inbound-nat-rule create command OK

<span data-ttu-id="d5fce-248">Opções de parâmetro:</span><span class="sxs-lookup"><span data-stu-id="d5fce-248">Parameter options:</span></span>

    -h, --help                                     output usage information
    -v, --verbose                                  use verbose output
    --json                                         use json output
    -g, --resource-group <resource-group>          hello name of hello resource group
    -l, --lb-name <lb-name>                        hello name of hello load balancer
    -n, --name <name>                              hello name of hello inbound NAT rule
    -p, --protocol <protocol>                      hello rule protocol [tcp,udp]
    -f, --frontend-port <frontend-port>            hello frontend port [0-65535]
    -b, --backend-port <backend-port>              hello backend port [0-65535]
    -e, --enable-floating-ip <enable-floating-ip>  enable floating point ip [true,false]
    -i, --frontend-ip <frontend-ip>                hello name of hello frontend ip configuration
    -m, --vm-id <vm-id>                            hello VM id.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Compute/virtualMachines/<vm-name>
    -a, --vm-name <vm-name>                        hello VM name.This VM must exist in hello same resource group as hello lb.
    Please use vm-id if that is not hello case.
    this parameter will be ignored if --vm-id is specified
    -s, --subscription <subscription>              hello subscription identifier
<BR>

    network lb inbound-nat-rule set [options] <resource-group> <lb-name> <name>
<span data-ttu-id="d5fce-249">Atualiza uma regra de nat de entrada existente.</span><span class="sxs-lookup"><span data-stu-id="d5fce-249">Updates an existing inbound nat rule.</span></span> <span data-ttu-id="d5fce-250">Em Olá exemplo a seguir, alteramos Olá porta de escuta de 80 too81 de entrada.</span><span class="sxs-lookup"><span data-stu-id="d5fce-250">In hello following example, we changed hello inbound listening port from 80 too81.</span></span>

    azure network lb inbound-nat-rule set -g group-1 -l mylb -n myinboundnat -p tcp -f 81 -b 8080 -i myfrontendip

    info:    Executing command network lb inbound-nat-rule set
    + Looking up hello load balancer "mylb"
    + Updating load balancer "mylb"
    + Looking up hello load balancer "mylb"
    data:    Id:                        /subscriptions/###############################/resourceGroups/group-1/providers/Microsoft.Network/loadBalancers/mylb/inboundNatRules/myinboundnat
    data:    Name:                      myinboundnat
    data:    Type:                      Microsoft.Network/loadBalancers/inboundNatRules
    data:    Provisioning state:        Succeeded
    data:    Frontend IP Configuration: id=/subscriptions/###############################/resourceGroups/group-1/providers/Microsoft.Network/loadBalancers/mylb/frontendIPConfigurations/myfrontendip
    data:    Backend IP configuration
    data:    Protocol                   Tcp
    data:    Frontend port              81
    data:    Backend port               8080
    data:    Enable floating IP         false
    info:    network lb inbound-nat-rule set command OK

<span data-ttu-id="d5fce-251">Opções de parâmetro:</span><span class="sxs-lookup"><span data-stu-id="d5fce-251">Parameter options:</span></span>

    -h, --help                                     output usage information
    -v, --verbose                                  use verbose output
    --json                                         use json output
    -g, --resource-group <resource-group>          hello name of hello resource group
    -l, --lb-name <lb-name>                        hello name of hello load balancer
    -n, --name <name>                              hello name of hello inbound NAT rule
    -p, --protocol <protocol>                      hello rule protocol [tcp,udp]
    -f, --frontend-port <frontend-port>            hello frontend port [0-65535]
    -b, --backend-port <backend-port>              hello backend port [0-65535]
    -e, --enable-floating-ip <enable-floating-ip>  enable floating point ip [true,false]
    -i, --frontend-ip <frontend-ip>                hello name of hello frontend ip configuration
    -m, --vm-id [vm-id]                            hello VM id.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Compute/virtualMachines/<vm-name>
    -a, --vm-name <vm-name>                        hello VM name.
    This virtual machine must exist in hello same resource group as hello lb.
    Please use vm-id if that is not hello case
    -s, --subscription <subscription>              hello subscription identifier
<BR>

    network lb inbound-nat-rule list [options] <resource-group> <lb-name>

<span data-ttu-id="d5fce-252">Lista todas as regras de nat de entrada para o balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="d5fce-252">Lists all inbound nat rules for load balancer.</span></span>

    azure network lb inbound-nat-rule list -g myresourcegroup -l mylb

    info:    Executing command network lb inbound-nat-rule list
    + Looking up hello load balancer "mylb"
    data:    Name          Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes  Backend IP configuration
    data:    ------------  ------------------  --------  -------------  ------------  ------------------  -----------------------  ---
    ---------------------
    data:    myinboundnat  Succeeded           Tcp       81             8080          false               4

    info:    network lb inbound-nat-rule list command OK

<span data-ttu-id="d5fce-253">Opções de parâmetro:</span><span class="sxs-lookup"><span data-stu-id="d5fce-253">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -s, --subscription <subscription>      hello subscription identifier
<BR>

    network lb inbound-nat-rule delete [options] <resource-group> <lb-name> <name>

<span data-ttu-id="d5fce-254">Exclui a regra NAT Olá balanceador de carga em um grupo de recursos específicos.</span><span class="sxs-lookup"><span data-stu-id="d5fce-254">Deletes NAT rule for hello load balancer in a specific resource group.</span></span>

    azure network lb inbound-nat-rule delete -g myresourcegroup -l mylb -n myinboundnat

    info:    Executing command network lb inbound-nat-rule delete
    + Looking up hello load balancer "mylb"
    Delete inbound NAT rule "myinboundnat?" [y/n] y
    + Updating load balancer "mylb"
    info:    network lb inbound-nat-rule delete command OK

<span data-ttu-id="d5fce-255">Opções de parâmetro:</span><span class="sxs-lookup"><span data-stu-id="d5fce-255">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -l, --lb-name <lb-name>                hello name of hello load balancer
    -n, --name <name>                      hello name of hello inbound NAT rule
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier

<span data-ttu-id="d5fce-256">**Endereços de ip público toomanage comandos**</span><span class="sxs-lookup"><span data-stu-id="d5fce-256">**Commands toomanage public ip addresses**</span></span>

    network public-ip create [options] <resource-group> <name> <location>
<span data-ttu-id="d5fce-257">Cria um recurso de ip público.</span><span class="sxs-lookup"><span data-stu-id="d5fce-257">Creates a public ip resource.</span></span> <span data-ttu-id="d5fce-258">Você criará o recurso de ip público de saudação e associar o nome de domínio tooa.</span><span class="sxs-lookup"><span data-stu-id="d5fce-258">You will create hello public ip resource and associate tooa domain name.</span></span>

    azure network public-ip create -g myresourcegroup -n mytestpublicip1 -l eastus -d azureclitest -a "Dynamic"
    info:    Executing command network public-ip create
    + Looking up hello public ip "mytestpublicip1"
    + Creating public ip address "mytestpublicip1"
    + Looking up hello public ip "mytestpublicip1"
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/publicIPAddresses/mytestpublicip1
    data:    Name:                 mytestpublicip1
    data:    Type:                 Microsoft.Network/publicIPAddresses
    data:    Location:             eastus
    data:    Provisioning state:   Succeeded
    data:    Allocation method:    Dynamic
    data:    Idle timeout:         4
    data:    Domain name label:    azureclitest
    data:    FQDN:                 azureclitest.eastus.cloudapp.azure.com
    info:    network public-ip create command OK


<span data-ttu-id="d5fce-259">Opções de parâmetro:</span><span class="sxs-lookup"><span data-stu-id="d5fce-259">Parameter options:</span></span>

    -h, --help                                   output usage information
    -v, --verbose                                use verbose output
    --json                                       use json output
    -g, --resource-group <resource-group>        hello name of hello resource group
    -n, --name <name>                            hello name of hello public ip
    -l, --location <location>                    hello location
    -d, --domain-name-label <domain-name-label>  hello domain name label.
    This set DNS too<domain-name-label>.<location>.cloudapp.azure.com
    -a, --allocation-method <allocation-method>  hello allocation method [Static][Dynamic]
    -i, --idletimeout <idletimeout>              hello idle timeout in minutes
    -f, --reverse-fqdn <reverse-fqdn>            hello reverse fqdn
    -t, --tags <tags>                            hello list of tags.
    Can be multiple. In hello format of "name=value".
    Name is required and value is optional.
    For example, -t tag1=value1;tag2
    -s, --subscription <subscription>            hello subscription identifier
<br>

    network public-ip set [options] <resource-group> <name>
<span data-ttu-id="d5fce-260">Atualiza as propriedades de saudação de um recurso de ip público existente.</span><span class="sxs-lookup"><span data-stu-id="d5fce-260">Updates hello properties of an existing public ip resource.</span></span> <span data-ttu-id="d5fce-261">Saudação de exemplo a seguir alteramos o endereço IP público de saudação do tooStatic dinâmico.</span><span class="sxs-lookup"><span data-stu-id="d5fce-261">In hello following example we changed hello public IP address from Dynamic tooStatic.</span></span>

    azure network public-ip set -g group-1 -n mytestpublicip1 -d azureclitest -a "Static"
    info:    Executing command network public-ip set
    + Looking up hello public ip "mytestpublicip1"
    + Updating public ip address "mytestpublicip1"
    + Looking up hello public ip "mytestpublicip1"
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/publicIPAddresses/mytestpublicip1
    data:    Name:                 mytestpublicip1
    data:    Type:                 Microsoft.Network/publicIPAddresses
    data:    Location:             eastus
    data:    Provisioning state:   Succeeded
    data:    Allocation method:    Static
    data:    Idle timeout:         4
    data:    IP Address:           (static IP address)
    data:    Domain name label:    azureclitest
    data:    FQDN:                 azureclitest.eastus.cloudapp.azure.com
    info:    network public-ip set command OK

<span data-ttu-id="d5fce-262">Opções de parâmetro:</span><span class="sxs-lookup"><span data-stu-id="d5fce-262">Parameter options:</span></span>

    -h, --help                                   output usage information
    -v, --verbose                                use verbose output
    --json                                       use json output
    -g, --resource-group <resource-group>        hello name of hello resource group
    -n, --name <name>                            hello name of hello public ip
    -d, --domain-name-label [domain-name-label]  hello domain name label.
    This set DNS too<domain-name-label>.<location>.cloudapp.azure.com
    -a, --allocation-method <allocation-method>  hello allocation method [Static][Dynamic]
    -i, --idletimeout <idletimeout>              hello idle timeout in minutes
    -f, --reverse-fqdn [reverse-fqdn]            hello reverse fqdn
    -t, --tags <tags>                            hello list of tags.
    Can be multiple. In hello format of "name=value".
    Name is required and value is optional.
    For example, -t tag1=value1;tag2
    --no-tags                                    remove all existing tags
    -s, --subscription <subscription>            hello subscription identifier

<br>
    <span data-ttu-id="d5fce-263">network public-ip list [options] &lt;resource-group&gt; Lista todos os recursos de IP público em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d5fce-263">network public-ip list [options] <resource-group> Lists all public IP resources within a resource group.</span></span>

    azure network public-ip list -g myresourcegroup

    info:    Executing command network public-ip list
    + Getting hello public ip addresses
    data:    Name             Location  Allocation  IP Address    Idle timeout  DNS Name
    data:    ---------------  --------  ----------  ------------  ------------  -------------------------------------------
    data:    mypubip5         westus    Dynamic                   4             "domain name".westus.cloudapp.azure.com
    data:    myPublicIP       eastus    Dynamic                   4             "domain name".eastus.cloudapp.azure.com
    data:    mytestpublicip   eastus    Dynamic                   4             "domain name".eastus.cloudapp.azure.com
    data:    mytestpublicip1  eastus   Static (Static IP address) 4             azureclitest.eastus.cloudapp.azure.com

<span data-ttu-id="d5fce-264">Opções de parâmetro:</span><span class="sxs-lookup"><span data-stu-id="d5fce-264">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -s, --subscription <subscription>      hello subscription identifier
<BR>
    <span data-ttu-id="d5fce-265">rede ip público Mostrar [Opções] < grupo de recursos ><name></span><span class="sxs-lookup"><span data-stu-id="d5fce-265">network public-ip show [options] <resource-group> <name></span></span>

<span data-ttu-id="d5fce-266">Exibe as propriedades de ip público de um recurso de ip público dentro de um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d5fce-266">Displays public ip properties for a public ip resource within a resource group.</span></span>

    azure network public-ip show -g myresourcegroup -n mytestpublicip

    info:    Executing command network public-ip show
    + Looking up hello public ip "mytestpublicip1"
    data:    Id:                   /subscriptions/###############################/resourceGroups/myresourcegroup/providers/Microsoft.Network/publicIPAddresses/mytestpublicip
    data:    Name:                 mytestpublicip
    data:    Type:                 Microsoft.Network/publicIPAddresses
    data:    Location:             eastus
    data:    Provisioning state:   Succeeded
    data:    Allocation method:    Static
    data:    Idle timeout:         4
    data:    IP Address:           (static IP address)
    data:    Domain name label:    azureclitest
    data:    FQDN:                 azureclitest.eastus.cloudapp.azure.com
    info:    network public-ip show command OK

<span data-ttu-id="d5fce-267">Opções de parâmetro:</span><span class="sxs-lookup"><span data-stu-id="d5fce-267">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -n, --name <name>                      hello name of hello public IP
    -s, --subscription <subscription>      hello subscription identifier


    network public-ip delete [options] <resource-group> <name>

<span data-ttu-id="d5fce-268">Exclui um recurso de ip público.</span><span class="sxs-lookup"><span data-stu-id="d5fce-268">Deletes public ip resource.</span></span>

    azure network public-ip delete -g group-1 -n mypublicipname
    info:    Executing command network public-ip delete
    + Looking up hello public ip "mypublicipname"
    Delete public ip address "mypublicipname"? [y/n] y
    + Deleting public ip address "mypublicipname"
    info:    network public-ip delete command OK

<span data-ttu-id="d5fce-269">Opções de parâmetro:</span><span class="sxs-lookup"><span data-stu-id="d5fce-269">Parameter options:</span></span>

    -h, --help                             output usage information
    -v, --verbose                          use verbose output
    --json                                 use json output
    -g, --resource-group <resource-group>  hello name of hello resource group
    -n, --name <name>                      hello name of hello public IP
    -q, --quiet                            quiet mode, do not ask for delete confirmation
    -s, --subscription <subscription>      hello subscription identifier


<span data-ttu-id="d5fce-270">**Interfaces de rede toomanage comandos**</span><span class="sxs-lookup"><span data-stu-id="d5fce-270">**Commands toomanage network interfaces**</span></span>

    network nic create [options] <resource-group> <name> <location>
<span data-ttu-id="d5fce-271">Cria um recurso chamado de interface de rede (NIC) que pode ser usada para balanceadores de carga ou associar tooa Máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="d5fce-271">Creates a resource called network interface (NIC) which can be used for load balancers or associate tooa Virtual Machine.</span></span>

    azure network nic create -g myresourcegroup -l eastus -n testnic1 --subnet-name subnet-1 --subnet-vnet-name myvnet

    info:    Executing command network nic create
    + Looking up hello network interface "testnic1"
    + Looking up hello subnet "subnet-1"
    + Creating network interface "testnic1"
    + Looking up hello network interface "testnic1"
    data:    Id:                     /subscriptions/c4a17ddf-aa84-491c-b6f9-b90d882299f7/resourceGroups/group-1/providers/Microsoft.Network/networkInterfaces/testnic1
    data:    Name:                   testnic1
    data:    Type:                   Microsoft.Network/networkInterfaces
    data:    Location:               eastus
    data:    Provisioning state:     Succeeded
    data:    IP configurations:
    data:       Name:                         NIC-config
    data:       Provisioning state:           Succeeded
    data:       Private IP address:           10.0.0.5
    data:       Private IP Allocation Method: Dynamic
    data:       Subnet:                       /subscriptions/c4a17ddf-aa84-491c-b6f9-b90d882299f7/resourceGroups/group-1/providers/Microsoft.Network/virtualNetworks/myVNET/subnets/Subnet-1

<span data-ttu-id="d5fce-272">Opções de parâmetro:</span><span class="sxs-lookup"><span data-stu-id="d5fce-272">Parameter options:</span></span>

    -h, --help                                                       output usage information
    -v, --verbose                                                    use verbose output
    --json                                                           use json output
    -g, --resource-group <resource-group>                            hello name of hello resource group
    -n, --name <name>                                                hello name of hello network interface
    -l, --location <location>                                        hello location
    -w, --network-security-group-id <network-security-group-id>      hello network security group identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/networkSecurityGroups/<nsg-name>
    -o, --network-security-group-name <network-security-group-name>  hello network security group name.
    This network security group must exist in hello same resource group as hello nic.
    Please use network-security-group-id if that is not hello case.
    -i, --public-ip-id <public-ip-id>                                hello public IP identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/publicIPAddresses/<public-ip-name>
    -p, --public-ip-name <public-ip-name>                            hello public IP name.
    This public ip must exist in hello same resource group as hello nic.
    Please use public-ip-id if that is not hello case.
    -a, --private-ip-address <private-ip-address>                    hello private IP address
    -u, --subnet-id <subnet-id>                                      hello subnet identifier.
    e.g. /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>/providers/Microsoft.Network/virtualNetworks/<vnet-name>/subnets/<subnet-name>
    --subnet-name <subnet-name>                                  hello subnet name
    -m, --subnet-vnet-name <subnet-vnet-name>                        hello vnet name under which subnet-name exists
    -t, --tags <tags>                                                hello comma seperated list of tags.
    Can be multiple. In hello format of "name=value".
    Name is required and value is optional.
    For example, -t tag1=value1;tag2
    -s, --subscription <subscription>                                hello subscription identifier
    data:
    info:    network nic create command OK

<BR>

    network nic set [options] <resource-group> <name>

    network nic list [options] <resource-group>
    network nic show [options] <resource-group> <name>
    network nic delete [options] <resource-group> <name>

<span data-ttu-id="d5fce-273">**Grupos de segurança de rede de toomanage de comandos**</span><span class="sxs-lookup"><span data-stu-id="d5fce-273">**Commands toomanage network security groups**</span></span>

    network nsg create [options] <resource-group> <name> <location>
    network nsg set [options] <resource-group> <name>
    network nsg list [options] <resource-group>
    network nsg show [options] <resource-group> <name>
    network nsg delete [options] <resource-group> <name>

<span data-ttu-id="d5fce-274">**Comandos toomanage regras de grupo de segurança de rede**</span><span class="sxs-lookup"><span data-stu-id="d5fce-274">**Commands toomanage network security group rules**</span></span>

    network nsg rule create [options] <resource-group> <nsg-name> <name>
    network nsg rule set [options] <resource-group> <nsg-name> <name>
    network nsg rule list [options] <resource-group> <nsg-name>
    network nsg rule show [options] <resource-group> <nsg-name> <name>
    network nsg rule delete [options] <resource-group> <nsg-name> <name>

<span data-ttu-id="d5fce-275">**Perfil do Gerenciador de tráfego de toomanage de comandos**</span><span class="sxs-lookup"><span data-stu-id="d5fce-275">**Commands toomanage traffic manager profile**</span></span>

    network traffic-manager profile create [options] <resource-group> <name>
    network traffic-manager profile set [options] <resource-group> <name>
    network traffic-manager profile list [options] <resource-group>
    network traffic-manager profile show [options] <resource-group> <name>
    network traffic-manager profile delete [options] <resource-group> <name>
    network traffic-manager profile is-dns-available [options] <resource-group> <relative-dns-name>

<span data-ttu-id="d5fce-276">**Pontos de extremidade de comandos toomanage traffic manager**</span><span class="sxs-lookup"><span data-stu-id="d5fce-276">**Commands toomanage traffic manager endpoints**</span></span>

    network traffic-manager profile endpoint create [options] <resource-group> <profile-name> <name> <endpoint-location>
    network traffic-manager profile endpoint set [options] <resource-group> <profile-name> <name>
    network traffic-manager profile endpoint delete [options] <resource-group> <profile-name> <name>

<span data-ttu-id="d5fce-277">**Gateways de rede virtual toomanage comandos**</span><span class="sxs-lookup"><span data-stu-id="d5fce-277">**Commands toomanage virtual network gateways**</span></span>

    network gateway list [options] <resource-group>

## <a name="azure-provider-commands-toomanage-resource-provider-registrations"></a><span data-ttu-id="d5fce-278">o provedor do Azure: comandos toomanage registros de provedor de recursos</span><span class="sxs-lookup"><span data-stu-id="d5fce-278">azure provider: Commands toomanage resource provider registrations</span></span>
<span data-ttu-id="d5fce-279">**Liste os provedores registrados atualmente no Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="d5fce-279">**List currently registered providers in Resource Manager**</span></span>

    provider list [options]

<span data-ttu-id="d5fce-280">**Mostrar detalhes sobre Olá solicitado namespace do provedor**</span><span class="sxs-lookup"><span data-stu-id="d5fce-280">**Show details about hello requested provider namespace**</span></span>

    provider show [options] <namespace>

<span data-ttu-id="d5fce-281">**Registre o provedor com assinatura de saudação**</span><span class="sxs-lookup"><span data-stu-id="d5fce-281">**Register provider with hello subscription**</span></span>

    provider register [options] <namespace>

<span data-ttu-id="d5fce-282">**Cancelar o registro do provedor com assinatura Olá**</span><span class="sxs-lookup"><span data-stu-id="d5fce-282">**Unregister provider with hello subscription**</span></span>

    provider unregister [options] <namespace>

## <a name="azure-resource-commands-toomanage-your-resources"></a><span data-ttu-id="d5fce-283">recursos do Azure: comandos toomanage seus recursos</span><span class="sxs-lookup"><span data-stu-id="d5fce-283">azure resource: Commands toomanage your resources</span></span>
<span data-ttu-id="d5fce-284">**Cria um recurso em um grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="d5fce-284">**Creates a resource in a resource group**</span></span>

    resource create [options] <resource-group> <name> <resource-type> <location> <api-version>

<span data-ttu-id="d5fce-285">**Atualiza um recurso em um grupo de recursos sem parâmetros ou modelos**</span><span class="sxs-lookup"><span data-stu-id="d5fce-285">**Updates a resource in a resource group without any templates or parameters**</span></span>

    resource set [options] <resource-group> <name> <resource-type> <properties> <api-version>

<span data-ttu-id="d5fce-286">**Recursos de saudação listas**</span><span class="sxs-lookup"><span data-stu-id="d5fce-286">**Lists hello resources**</span></span>

    resource list [options] [resource-group]

<span data-ttu-id="d5fce-287">**Obtém um recurso dentro de um grupo de recursos ou assinatura**</span><span class="sxs-lookup"><span data-stu-id="d5fce-287">**Gets one resource within a resource group or subscription**</span></span>

    resource show [options] <resource-group> <name> <resource-type> <api-version>

<span data-ttu-id="d5fce-288">**Exclui um recurso em um grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="d5fce-288">**Deletes a resource in a resource group**</span></span>

    resource delete [options] <resource-group> <name> <resource-type> <api-version>

## <a name="azure-role-commands-toomanage-your-azure-roles"></a><span data-ttu-id="d5fce-289">função do Azure: comandos toomanage as funções do Azure</span><span class="sxs-lookup"><span data-stu-id="d5fce-289">azure role: Commands toomanage your Azure roles</span></span>
<span data-ttu-id="d5fce-290">**Obtenha todas as definições de função disponíveis**</span><span class="sxs-lookup"><span data-stu-id="d5fce-290">**Get all available role definitions**</span></span>

    role list [options]

<span data-ttu-id="d5fce-291">**Obtenha uma definição de função disponível**</span><span class="sxs-lookup"><span data-stu-id="d5fce-291">**Get an available role definition**</span></span>

    role show [options] [name]

<span data-ttu-id="d5fce-292">**Comandos toomanage sua atribuição de função**</span><span class="sxs-lookup"><span data-stu-id="d5fce-292">**Commands toomanage your role assignment**</span></span>

    role assignment create [options] [objectId] [upn] [mail] [spn] [role] [scope] [resource-group] [resource-type] [resource-name]
    role assignment list [options] [objectId] [upn] [mail] [spn] [role] [scope] [resource-group] [resource-type] [resource-name]
    role assignment delete [options] [objectId] [upn] [mail] [spn] [role] [scope] [resource-group] [resource-type] [resource-name]

## <a name="azure-storage-commands-toomanage-your-storage-objects"></a><span data-ttu-id="d5fce-293">armazenamento do Azure: comandos toomanage seus objetos de armazenamento</span><span class="sxs-lookup"><span data-stu-id="d5fce-293">azure storage: Commands toomanage your Storage objects</span></span>
<span data-ttu-id="d5fce-294">**Comandos toomanage suas contas de armazenamento**</span><span class="sxs-lookup"><span data-stu-id="d5fce-294">**Commands toomanage your Storage accounts**</span></span>

    storage account list [options]
    storage account show [options] <name>
    storage account create [options] <name>
    storage account set [options] <name>
    storage account delete [options] <name>

<span data-ttu-id="d5fce-295">**Comandos toomanage suas chaves de conta de armazenamento**</span><span class="sxs-lookup"><span data-stu-id="d5fce-295">**Commands toomanage your Storage account keys**</span></span>

    storage account keys list [options] <name>
    storage account keys renew [options] <name>

<span data-ttu-id="d5fce-296">**Comandos tooshow sua cadeia de caracteres de conexão de armazenamento**</span><span class="sxs-lookup"><span data-stu-id="d5fce-296">**Commands tooshow your Storage connection string**</span></span>

    storage account connectionstring show [options] <name>

<span data-ttu-id="d5fce-297">**Comandos toomanage seus contêineres de armazenamento**</span><span class="sxs-lookup"><span data-stu-id="d5fce-297">**Commands toomanage your Storage containers**</span></span>

    storage container list [options] [prefix]
    storage container show [options] [container]
    storage container create [options] [container]
    storage container delete [options] [container]
    storage container set [options] [container]

<span data-ttu-id="d5fce-298">**Assinaturas de acesso compartilhado de toomanage comandos do seu contêiner de armazenamento**</span><span class="sxs-lookup"><span data-stu-id="d5fce-298">**Commands toomanage shared access signatures of your Storage container**</span></span>

    storage container sas create [options] [container] [permissions] [expiry]

<span data-ttu-id="d5fce-299">**Comandos toomanage armazenado políticas de acesso do seu contêiner de armazenamento**</span><span class="sxs-lookup"><span data-stu-id="d5fce-299">**Commands toomanage stored access policies of your Storage container**</span></span>

    storage container policy create [options] [container] [name]
    storage container policy show [options] [container] [name]
    storage container policy list [options] [container]
    storage container policy set [options] [container] [name]
    storage container policy delete [options] [container] [name]

<span data-ttu-id="d5fce-300">**Comandos toomanage seus blobs de armazenamento**</span><span class="sxs-lookup"><span data-stu-id="d5fce-300">**Commands toomanage your Storage blobs**</span></span>

    storage blob list [options] [container] [prefix]
    storage blob show [options] [container] [blob]
    storage blob delete [options] [container] [blob]
    storage blob upload [options] [file] [container] [blob]
    storage blob download [options] [container] [blob] [destination]

<span data-ttu-id="d5fce-301">**Comandos toomanage suas operações de cópia de blob**</span><span class="sxs-lookup"><span data-stu-id="d5fce-301">**Commands toomanage your blob copy operations**</span></span>

    storage blob copy start [options] [sourceUri] [destContainer]
    storage blob copy show [options] [container] [blob]
    storage blob copy stop [options] [container] [blob] [copyid]

<span data-ttu-id="d5fce-302">**Assinatura de acesso compartilhado toomanage comandos do seu blob de armazenamento**</span><span class="sxs-lookup"><span data-stu-id="d5fce-302">**Commands toomanage shared access signature of your Storage blob**</span></span>

    storage blob sas create [options] [container] [blob] [permissions] [expiry]

<span data-ttu-id="d5fce-303">**Comandos toomanage seus compartilhamentos de arquivos de armazenamento**</span><span class="sxs-lookup"><span data-stu-id="d5fce-303">**Commands toomanage your Storage file shares**</span></span>

    storage share create [options] [share]
    storage share show [options] [share]
    storage share delete [options] [share]
    storage share list [options] [prefix]

<span data-ttu-id="d5fce-304">**Comandos toomanage seus arquivos de armazenamento**</span><span class="sxs-lookup"><span data-stu-id="d5fce-304">**Commands toomanage your Storage files**</span></span>

    storage file list [options] [share] [path]
    storage file delete [options] [share] [path]
    storage file upload [options] [source] [share] [path]
    storage file download [options] [share] [path] [destination]

<span data-ttu-id="d5fce-305">**Comandos toomanage seu diretório do arquivo de armazenamento**</span><span class="sxs-lookup"><span data-stu-id="d5fce-305">**Commands toomanage your Storage file directory**</span></span>

    storage directory create [options] [share] [path]
    storage directory delete [options] [share] [path]

<span data-ttu-id="d5fce-306">**Comandos toomanage suas filas de armazenamento**</span><span class="sxs-lookup"><span data-stu-id="d5fce-306">**Commands toomanage your Storage queues**</span></span>

    storage queue create [options] [queue]
    storage queue list [options] [prefix]
    storage queue show [options] [queue]
    storage queue delete [options] [queue]

<span data-ttu-id="d5fce-307">**Assinaturas de acesso comandos toomanage compartilhado de sua fila de armazenamento**</span><span class="sxs-lookup"><span data-stu-id="d5fce-307">**Commands toomanage shared access signatures of your Storage queue**</span></span>

    storage queue sas create [options] [queue] [permissions] [expiry]

<span data-ttu-id="d5fce-308">**Comandos toomanage armazenado políticas de acesso de sua fila de armazenamento**</span><span class="sxs-lookup"><span data-stu-id="d5fce-308">**Commands toomanage stored access policies of your Storage queue**</span></span>

    storage queue policy create [options] [queue] [name]
    storage queue policy show [options] [queue] [name]
    storage queue policy list [options] [queue]
    storage queue policy set [options] [queue] [name]
    storage queue policy delete [options] [queue] [name]

<span data-ttu-id="d5fce-309">**Comandos toomanage suas propriedades de log de armazenamento**</span><span class="sxs-lookup"><span data-stu-id="d5fce-309">**Commands toomanage your Storage logging properties**</span></span>

    storage logging show [options]
    storage logging set [options]

<span data-ttu-id="d5fce-310">**Comandos toomanage suas propriedades de métricas de armazenamento**</span><span class="sxs-lookup"><span data-stu-id="d5fce-310">**Commands toomanage your Storage metrics properties**</span></span>

    storage metrics show [options]
    storage metrics set [options]

<span data-ttu-id="d5fce-311">**Comandos toomanage suas tabelas de armazenamento**</span><span class="sxs-lookup"><span data-stu-id="d5fce-311">**Commands toomanage your Storage tables**</span></span>

    storage table create [options] [table]
    storage table list [options] [prefix]
    storage table show [options] [table]
    storage table delete [options] [table]

<span data-ttu-id="d5fce-312">**Assinaturas de acesso compartilhado de toomanage comandos de sua tabela de armazenamento**</span><span class="sxs-lookup"><span data-stu-id="d5fce-312">**Commands toomanage shared access signatures of your Storage table**</span></span>

    storage table sas create [options] [table] [permissions] [expiry]

<span data-ttu-id="d5fce-313">**Comandos toomanage armazenado políticas de acesso de sua tabela de armazenamento**</span><span class="sxs-lookup"><span data-stu-id="d5fce-313">**Commands toomanage stored access policies of your Storage table**</span></span>

    storage table policy create [options] [table] [name]
    storage table policy show [options] [table] [name]
    storage table policy list [options] [table]
    storage table policy set [options] [table] [name]
    storage table policy delete [options] [table] [name]

## <a name="azure-tag-commands-toomanage-your-resource-manager-tag"></a><span data-ttu-id="d5fce-314">marca do Azure: comandos toomanage sua marca de Gerenciador de recursos</span><span class="sxs-lookup"><span data-stu-id="d5fce-314">azure tag: Commands toomanage your resource manager tag</span></span>
<span data-ttu-id="d5fce-315">**Adicione uma marca**</span><span class="sxs-lookup"><span data-stu-id="d5fce-315">**Add a tag**</span></span>

    tag create [options] <name> <value>

<span data-ttu-id="d5fce-316">**Remova uma marca inteira ou um valor de marca**</span><span class="sxs-lookup"><span data-stu-id="d5fce-316">**Remove an entire tag or a tag value**</span></span>

    tag delete [options] <name> <value>

<span data-ttu-id="d5fce-317">**Lista informações de marca Olá**</span><span class="sxs-lookup"><span data-stu-id="d5fce-317">**Lists hello tag information**</span></span>

    tag list [options]

<span data-ttu-id="d5fce-318">**Obtém uma marca**</span><span class="sxs-lookup"><span data-stu-id="d5fce-318">**Get a tag**</span></span>

    tag show [options] [name]

## <a name="azure-vm-commands-toomanage-your-azure-virtual-machines"></a><span data-ttu-id="d5fce-319">vm do Azure: comandos toomanage máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="d5fce-319">azure vm: Commands toomanage your Azure Virtual Machines</span></span>
<span data-ttu-id="d5fce-320">**Cria uma máquina virtual**</span><span class="sxs-lookup"><span data-stu-id="d5fce-320">**Create a VM**</span></span>

    vm create [options] <resource-group> <name> <location> <os-type>

<span data-ttu-id="d5fce-321">**Cria uma máquina virtual com recursos padrões**</span><span class="sxs-lookup"><span data-stu-id="d5fce-321">**Create a VM with default resources**</span></span>

    vm quick-create [options] <resource-group> <name> <location> <os-type> <image-urn> <admin-username> <admin-password

> [!TIP]
> <span data-ttu-id="d5fce-322">A partir do CLI versão 0,10, você pode fornecer um alias curto, como "UbuntuLTS" ou "Win2012R2Datacenter" como Olá `image-urn` para algumas imagens do Marketplace populares.</span><span class="sxs-lookup"><span data-stu-id="d5fce-322">Starting with CLI version 0.10, you can provide a short alias such as "UbuntuLTS" or "Win2012R2Datacenter" as hello `image-urn` for some popular Marketplace images.</span></span> <span data-ttu-id="d5fce-323">Execute `azure help vm quick-create` para opções.</span><span class="sxs-lookup"><span data-stu-id="d5fce-323">Run `azure help vm quick-create` for options.</span></span> <span data-ttu-id="d5fce-324">Além disso, começando com a versão 0,10, `azure vm quick-create` usa o armazenamento premium por padrão, se ele está disponível na região selecionada da saudação.</span><span class="sxs-lookup"><span data-stu-id="d5fce-324">Additionally, starting with version 0.10, `azure vm quick-create` uses premium storage by default if it's available in hello selected region.</span></span>
> 
> 

<span data-ttu-id="d5fce-325">**Listar máquinas virtuais de saudação em uma conta**</span><span class="sxs-lookup"><span data-stu-id="d5fce-325">**List hello virtual machines within an account**</span></span>

    vm list [options]

<span data-ttu-id="d5fce-326">**Obtém uma máquina virtual dentro de um grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="d5fce-326">**Get one virtual machine within a resource group**</span></span>

    vm show [options] <resource-group> <name>

<span data-ttu-id="d5fce-327">**Exclui uma máquina virtual dentro de um grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="d5fce-327">**Delete one virtual machine within a resource group**</span></span>

    vm delete [options] <resource-group> <name>

<span data-ttu-id="d5fce-328">**Desliga uma máquina virtual dentro de um grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="d5fce-328">**Shutdown one virtual machine within a resource group**</span></span>

    vm stop [options] <resource-group> <name>

<span data-ttu-id="d5fce-329">**Reinicia uma máquina virtual dentro de um grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="d5fce-329">**Restart one virtual machine within a resource group**</span></span>

    vm restart [options] <resource-group> <name>

<span data-ttu-id="d5fce-330">**Inicia uma máquina virtual dentro de um grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="d5fce-330">**Start one virtual machine within a resource group**</span></span>

    vm start [options] <resource-group> <name>

<span data-ttu-id="d5fce-331">**Desligar uma máquina virtual em uma saudação de grupo e as versões do recurso de recursos de computação**</span><span class="sxs-lookup"><span data-stu-id="d5fce-331">**Shutdown one virtual machine within a resource group and releases hello compute resources**</span></span>

    vm deallocate [options] <resource-group> <name>

<span data-ttu-id="d5fce-332">**Lista os tamanhos de máquina virtual disponíveis**</span><span class="sxs-lookup"><span data-stu-id="d5fce-332">**List available virtual machine sizes**</span></span>

    vm sizes [options]

<span data-ttu-id="d5fce-333">**Capturar Olá VM como imagem do sistema operacional ou imagem de VM**</span><span class="sxs-lookup"><span data-stu-id="d5fce-333">**Capture hello VM as OS Image or VM Image**</span></span>

    vm capture [options] <resource-group> <name> <vhd-name-prefix>

<span data-ttu-id="d5fce-334">**Definir estado de saudação do hello VM tooGeneralized**</span><span class="sxs-lookup"><span data-stu-id="d5fce-334">**Set hello state of hello VM tooGeneralized**</span></span>

    vm generalize [options] <resource-group> <name>

<span data-ttu-id="d5fce-335">**Obter exibição de instância de saudação VM**</span><span class="sxs-lookup"><span data-stu-id="d5fce-335">**Get instance view of hello VM**</span></span>

    vm get-instance-view [options] <resource-group> <name>

<span data-ttu-id="d5fce-336">**Habilitar o acesso de área de trabalho remota ou SSH configurações em uma máquina Virtual e tooreset Olá senha para conta Olá com o administrador ou sudo autoridade tooreset**</span><span class="sxs-lookup"><span data-stu-id="d5fce-336">**Enable you tooreset Remote Desktop Access or SSH settings on a Virtual Machine and tooreset hello password for hello account that has administrator or sudo authority**</span></span>

    vm reset-access [options] <resource-group> <name>

<span data-ttu-id="d5fce-337">**Atualiza a VM com novos dados**</span><span class="sxs-lookup"><span data-stu-id="d5fce-337">**Update VM with new data**</span></span>

    vm set [options] <resource-group> <name>

<span data-ttu-id="d5fce-338">**Comandos toomanage os discos de dados de máquina Virtual**</span><span class="sxs-lookup"><span data-stu-id="d5fce-338">**Commands toomanage your Virtual Machine data disks**</span></span>

    vm disk attach-new [options] <resource-group> <vm-name> <size-in-gb> [vhd-name]
    vm disk detach [options] <resource-group> <vm-name> <lun>
    vm disk attach [options] <resource-group> <vm-name> [vhd-url]

<span data-ttu-id="d5fce-339">**Extensões de recurso VM comandos toomanage**</span><span class="sxs-lookup"><span data-stu-id="d5fce-339">**Commands toomanage VM resource extensions**</span></span>

    vm extension set [options] <resource-group> <vm-name> <name> <publisher-name> <version>
    vm extension get [options] <resource-group> <vm-name>

<span data-ttu-id="d5fce-340">**Comandos toomanage sua máquina Virtual do Docker**</span><span class="sxs-lookup"><span data-stu-id="d5fce-340">**Commands toomanage your Docker Virtual Machine**</span></span>

    vm docker create [options] <resource-group> <name> <location> <os-type>

<span data-ttu-id="d5fce-341">**Comandos toomanage imagens da VM**</span><span class="sxs-lookup"><span data-stu-id="d5fce-341">**Commands toomanage VM images**</span></span>

    vm image list-publishers [options] <location>
    vm image list-offers [options] <location> <publisher>
    vm image list-skus [options] <location> <publisher> <offer>
    vm image list [options] <location> <publisher> [offer] [sku]
