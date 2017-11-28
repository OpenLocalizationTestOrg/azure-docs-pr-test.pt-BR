---
title: "Personalizar os clusters HDInsight usando ações de script – Azure | Microsoft Docs"
description: "Adicione componentes personalizados ao clusters HDInsight baseados em Linux usando Ações de Script. As Ações de Script são scripts Bash que podem ser usadas para personalizar a configuração do cluster ou adicionar outros serviços e utilitários, como Hue, Solr ou R."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 48e85f53-87c1-474f-b767-ca772238cc13
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: 0c5d00b6cb9f68a1a0e474f81c969eb1b5654c67
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="customize-linux-based-hdinsight-clusters-using-script-action"></a><span data-ttu-id="41211-104">Personalizar clusters HDInsight baseados em Linux usando a Ação de Script</span><span class="sxs-lookup"><span data-stu-id="41211-104">Customize Linux-based HDInsight clusters using Script Action</span></span>

<span data-ttu-id="41211-105">O HDInsight fornece uma opção de configuração chamada **Ação de Script** que chama os scripts personalizados que personalizam o cluster.</span><span class="sxs-lookup"><span data-stu-id="41211-105">HDInsight provides a configuration option called **Script Action** that invokes custom scripts that customize the cluster.</span></span> <span data-ttu-id="41211-106">Esses scripts são usados para instalar componentes adicionais e alterar definições de configuração.</span><span class="sxs-lookup"><span data-stu-id="41211-106">These scripts are used to install additional components and change configuration settings.</span></span> <span data-ttu-id="41211-107">Ações de script podem ser usadas durante ou após a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="41211-107">Script actions can be used during or after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="41211-108">A capacidade de usar as ações de script em um cluster já em execução só está disponível para os clusters HDInsight baseados em Linux.</span><span class="sxs-lookup"><span data-stu-id="41211-108">The ability to use script actions on an already running cluster is only available for Linux-based HDInsight clusters.</span></span>
>
> <span data-ttu-id="41211-109">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="41211-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="41211-110">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="41211-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="41211-111">Ações de script também podem ser publicadas no Azure Marketplace como um aplicativo do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="41211-111">Script actions can also be published to the Azure Marketplace as an HDInsight application.</span></span> <span data-ttu-id="41211-112">Alguns dos exemplos neste documento mostram como você pode instalar um aplicativo do HDInsight usando comandos de ação de script do PowerShell e o SDK do .NET.</span><span class="sxs-lookup"><span data-stu-id="41211-112">Some of the examples in this document show how you can install an HDInsight application using script action commands from PowerShell and the .NET SDK.</span></span> <span data-ttu-id="41211-113">Para obter mais informações sobre aplicativos do HDInsight, consulte [Publicar aplicativos do HDInsight no Azure Marketplace](hdinsight-apps-publish-applications.md).</span><span class="sxs-lookup"><span data-stu-id="41211-113">For more information on HDInsight applications, see [Publish HDInsight applications into the Azure Marketplace](hdinsight-apps-publish-applications.md).</span></span>

## <a name="permissions"></a><span data-ttu-id="41211-114">Permissões</span><span class="sxs-lookup"><span data-stu-id="41211-114">Permissions</span></span>

<span data-ttu-id="41211-115">Se você estiver usando um cluster de HDInsight do domínio, há duas permissões Ambari necessárias ao usar ações de script com o cluster:</span><span class="sxs-lookup"><span data-stu-id="41211-115">If you are using a domain-joined HDInsight cluster, there are two Ambari permissions that are required when using script actions with the cluster:</span></span>

* <span data-ttu-id="41211-116">**AMBARI. EXECUTAR\_PERSONALIZADO\_COMANDO**: função de administrador de Ambari tem essa permissão por padrão.</span><span class="sxs-lookup"><span data-stu-id="41211-116">**AMBARI.RUN\_CUSTOM\_COMMAND**: The Ambari Administrator role has this permission by default.</span></span>
* <span data-ttu-id="41211-117">**CLUSTER. EXECUTAR\_PERSONALIZADO\_COMANDO**: administrador de Cluster HDInsight e administrador de Ambari têm essa permissão por padrão.</span><span class="sxs-lookup"><span data-stu-id="41211-117">**CLUSTER.RUN\_CUSTOM\_COMMAND**: Both the HDInsight Cluster Administrator and Ambari Administrator have this permission by default.</span></span>

<span data-ttu-id="41211-118">Para obter mais informações sobre como trabalhar com permissões com o HDInsight de domínio, consulte [gerenciar clusters de HDInsight de domínio](hdinsight-domain-joined-manage.md).</span><span class="sxs-lookup"><span data-stu-id="41211-118">For more information on working with permissions with domain-joined HDInsight, see [Manage domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span></span>

## <a name="access-control"></a><span data-ttu-id="41211-119">Controle de acesso</span><span class="sxs-lookup"><span data-stu-id="41211-119">Access control</span></span>

<span data-ttu-id="41211-120">Se você não for o proprietário/administrador da sua assinatura do Azure, sua conta deverá ter pelo menos acesso de **Colaborador** ao grupo de recursos que contém o cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="41211-120">If you are not the administrator/owner of your Azure subscription, your account must have at least **Contributor** access to the resource group that contains the HDInsight cluster.</span></span>

<span data-ttu-id="41211-121">Além disso, se você está criando um cluster HDInsight, alguém com no mínimo acesso de **Colaborador** à assinatura do Azure deve ter registrado anteriormente o provedor para HDInsight.</span><span class="sxs-lookup"><span data-stu-id="41211-121">Additionally, if you are creating an HDInsight cluster, someone with at least **Contributor** access to the Azure subscription must have previously registered the provider for HDInsight.</span></span> <span data-ttu-id="41211-122">O registro do provedor acontece quando um usuário com acesso de Colaborador à assinatura cria um recurso nela pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="41211-122">Provider registration happens when a user with Contributor access to the subscription creates a resource for the first time on the subscription.</span></span> <span data-ttu-id="41211-123">Isso também pode ser feito sem criar um recurso, [registrando um provedor com o uso de REST](https://msdn.microsoft.com/library/azure/dn790548.aspx).</span><span class="sxs-lookup"><span data-stu-id="41211-123">It can also be accomplished without creating a resource by [registering a provider using REST](https://msdn.microsoft.com/library/azure/dn790548.aspx).</span></span>

<span data-ttu-id="41211-124">Para saber mais sobre como trabalhar com o gerenciamento de acesso, confira os seguintes documentos:</span><span class="sxs-lookup"><span data-stu-id="41211-124">For more information on working with access management, see the following documents:</span></span>

* [<span data-ttu-id="41211-125">Introdução ao gerenciamento de acesso no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="41211-125">Get started with access management in the Azure portal</span></span>](../active-directory/role-based-access-control-what-is.md)
* [<span data-ttu-id="41211-126">Usar as atribuições de função para gerenciar o acesso aos recursos de assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="41211-126">Use role assignments to manage access to your Azure subscription resources</span></span>](../active-directory/role-based-access-control-configure.md)

## <a name="understanding-script-actions"></a><span data-ttu-id="41211-127">Noções básicas sobre Ações de Script</span><span class="sxs-lookup"><span data-stu-id="41211-127">Understanding Script Actions</span></span>

<span data-ttu-id="41211-128">Uma Ação de Script é simplesmente um script Bash para o qual você fornecer um URI e parâmetros.</span><span class="sxs-lookup"><span data-stu-id="41211-128">A Script Action is simply a Bash script that you provide a URI to, and parameters for.</span></span> <span data-ttu-id="41211-129">O script é executado em nós no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="41211-129">The script runs on nodes in the HDInsight cluster.</span></span> <span data-ttu-id="41211-130">A seguir, as características e os recursos das ações de script.</span><span class="sxs-lookup"><span data-stu-id="41211-130">The following are characteristics and features of script actions.</span></span>

* <span data-ttu-id="41211-131">Deve estar armazenado em um URI que pode ser acessado do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="41211-131">Must be stored on a URI that is accessible from the HDInsight cluster.</span></span> <span data-ttu-id="41211-132">Estes são os possíveis locais de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="41211-132">The following are possible storage locations:</span></span>

    * <span data-ttu-id="41211-133">Uma conta de **Azure Data Lake Store** acessível pelo cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="41211-133">An **Azure Data Lake Store** account that is accessible by the HDInsight cluster.</span></span> <span data-ttu-id="41211-134">Para obter mais informações sobre o uso do Azure Data Lake Store com o HDInsight, veja [Criar um cluster HDInsight com o Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="41211-134">For information on using Azure Data Lake Store with HDInsight, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

        <span data-ttu-id="41211-135">Ao usar um script armazenado no Data Lake Store, o formato de URI é `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.</span><span class="sxs-lookup"><span data-stu-id="41211-135">When using a script stored in Data Lake Store, the URI format is `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.</span></span>

        > [!NOTE]
        > <span data-ttu-id="41211-136">A entidade de serviço que HDInsight usa para acessar o Data Lake Store deve ter acesso de leitura para o script.</span><span class="sxs-lookup"><span data-stu-id="41211-136">The service principal HDInsight uses to access Data Lake Store must have read access to the script.</span></span>

    * <span data-ttu-id="41211-137">Um blob em uma **conta do Armazenamento do Azure** que é a conta de armazenamento principal ou adicional para o cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="41211-137">A blob in an **Azure Storage account** that is either the primary or additional storage account for the HDInsight cluster.</span></span> <span data-ttu-id="41211-138">O HDInsight recebe acesso a ambos esses tipos de contas de armazenamento durante a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="41211-138">HDInsight is granted access to both of these types of storage accounts during cluster creation.</span></span>

    * <span data-ttu-id="41211-139">Um serviço de compartilhamento de arquivos público como o Blob do Azure, o GitHub, o OneDrive, o Dropbox, etc.</span><span class="sxs-lookup"><span data-stu-id="41211-139">A public file sharing service such as Azure Blob, GitHub, OneDrive, Dropbox, etc.</span></span>

        <span data-ttu-id="41211-140">Para URIs de exemplo, consulte a seção [Scripts de exemplo de Ação de Script](#example-script-action-scripts).</span><span class="sxs-lookup"><span data-stu-id="41211-140">For example URIs, see the [Example script action scripts](#example-script-action-scripts) section.</span></span>

        > [!WARNING]
        > <span data-ttu-id="41211-141">O HDInsight suporta apenas contas do Azure Storage de __Uso geral__.</span><span class="sxs-lookup"><span data-stu-id="41211-141">HDInsight only supports __General-purpose__ Azure Storage accounts.</span></span> <span data-ttu-id="41211-142">Atualmente ele não dá suporte ao tipo de conta __Armazenamento de blobs__.</span><span class="sxs-lookup"><span data-stu-id="41211-142">It does not currently support the __Blob storage__ account type.</span></span>

* <span data-ttu-id="41211-143">Podem ser restritos à **execução somente em determinados tipos de nó**, por exemplo, nos nós de cabeçalho ou nos nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="41211-143">Can be restricted to **run on only certain node types**, for example head nodes or worker nodes.</span></span>

  > [!NOTE]
  > <span data-ttu-id="41211-144">Quando usado com HDInsight Premium, você pode especificar que o script deve ser usado no nó de borda.</span><span class="sxs-lookup"><span data-stu-id="41211-144">When used with HDInsight Premium, you can specify that the script should be used on the edge node.</span></span>

* <span data-ttu-id="41211-145">Pode ser **persistente** ou **ad hoc**.</span><span class="sxs-lookup"><span data-stu-id="41211-145">Can be **persisted** or **ad hoc**.</span></span>

    <span data-ttu-id="41211-146">Os scripts **persistentes** são aplicados aos nós de trabalho adicionados ao cluster depois que o script é executado.</span><span class="sxs-lookup"><span data-stu-id="41211-146">**Persisted** scripts are applied to worker nodes added to the cluster after the script runs.</span></span> <span data-ttu-id="41211-147">Por exemplo, ao escalar verticalmente o cluster.</span><span class="sxs-lookup"><span data-stu-id="41211-147">For example, when scaling up the cluster.</span></span>

    <span data-ttu-id="41211-148">Um script persistente também pode aplicar alterações a outro tipo de nó, como um nó de cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="41211-148">A persisted script might also apply changes to another node type, such as a head node.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="41211-149">As ações de script persistentes devem ter um nome exclusivo.</span><span class="sxs-lookup"><span data-stu-id="41211-149">Persisted script actions must have a unique name.</span></span>

    <span data-ttu-id="41211-150">Scripts **Ad hoc** não são persistentes.</span><span class="sxs-lookup"><span data-stu-id="41211-150">**Ad hoc** scripts are not persisted.</span></span> <span data-ttu-id="41211-151">Eles não são aplicados a nós de trabalho adicionados ao cluster após o script ter sido executado.</span><span class="sxs-lookup"><span data-stu-id="41211-151">They are not applied to worker nodes added to the cluster after the script has ran.</span></span> <span data-ttu-id="41211-152">Você pode promover posteriormente um script ad hoc a um script persistente ou rebaixar um script persistente a um script ad hoc.</span><span class="sxs-lookup"><span data-stu-id="41211-152">You can subsequently promote an ad hoc script to a persisted script, or demote a persisted script to an ad hoc script.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="41211-153">As ações de script usadas durante a criação do cluster são mantidas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="41211-153">Script actions used during cluster creation are automatically persisted.</span></span>
  >
  > <span data-ttu-id="41211-154">Os scripts que falham não são persistentes, mesmo que você indique especificamente que eles devem ser.</span><span class="sxs-lookup"><span data-stu-id="41211-154">Scripts that fail are not persisted, even if you specifically indicate that they should be.</span></span>

* <span data-ttu-id="41211-155">Podem aceitar **parâmetros** usados pelo script durante a execução.</span><span class="sxs-lookup"><span data-stu-id="41211-155">Can accept **parameters** that are used by the script during execution.</span></span>
* <span data-ttu-id="41211-156">São executados com os **privilégios no nível da raiz** nos nós do cluster.</span><span class="sxs-lookup"><span data-stu-id="41211-156">Run with **root level privileges** on the cluster nodes.</span></span>
* <span data-ttu-id="41211-157">Podem ser usados por meio do **Portal do Azure**, do **Azure PowerShell**, da **CLI do Azure** ou do **SDK do .NET do HDInsight**</span><span class="sxs-lookup"><span data-stu-id="41211-157">Can be used through the **Azure portal**, **Azure PowerShell**, **Azure CLI**, or **HDInsight .NET SDK**</span></span>

<span data-ttu-id="41211-158">O cluster mantém um histórico de todos os scripts que foram executados.</span><span class="sxs-lookup"><span data-stu-id="41211-158">The cluster keeps a history of all scripts that have been ran.</span></span> <span data-ttu-id="41211-159">O histórico é útil quando você precisa localizar a ID de um script para operações de promoção ou rebaixamento.</span><span class="sxs-lookup"><span data-stu-id="41211-159">The history is useful when you need to find the ID of a script for promotion or demotion operations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="41211-160">Não há nenhuma forma automática de desfazer as alterações feitas por uma ação de script.</span><span class="sxs-lookup"><span data-stu-id="41211-160">There is no automatic way to undo the changes made by a script action.</span></span> <span data-ttu-id="41211-161">Reverta manualmente as alterações ou forneça um script que as reverta.</span><span class="sxs-lookup"><span data-stu-id="41211-161">Either manually reverse the changes or provide a script that reverses them.</span></span>


### <a name="script-action-in-the-cluster-creation-process"></a><span data-ttu-id="41211-162">Ação de Script no processo de criação do cluster</span><span class="sxs-lookup"><span data-stu-id="41211-162">Script Action in the cluster creation process</span></span>

<span data-ttu-id="41211-163">As ações de script usadas durante a criação do cluster são ligeiramente diferentes das ações de script executadas em um cluster existente:</span><span class="sxs-lookup"><span data-stu-id="41211-163">Script Actions used during cluster creation are slightly different from script actions ran on an existing cluster:</span></span>

* <span data-ttu-id="41211-164">O script é **automaticamente persistente**.</span><span class="sxs-lookup"><span data-stu-id="41211-164">The script is **automatically persisted**.</span></span>
* <span data-ttu-id="41211-165">Uma **falha** no script pode fazer com que o processo de criação do cluster falhe.</span><span class="sxs-lookup"><span data-stu-id="41211-165">A **failure** in the script can cause the cluster creation process to fail.</span></span>

<span data-ttu-id="41211-166">O diagrama a seguir ilustra quando a Ação de Script é executada durante o processo de criação:</span><span class="sxs-lookup"><span data-stu-id="41211-166">The following diagram illustrates when Script Action is executed during the creation process:</span></span>

<span data-ttu-id="41211-167">![Personalização do cluster HDInsight e estágios durante a criação de cluster][img-hdi-cluster-states]</span><span class="sxs-lookup"><span data-stu-id="41211-167">![HDInsight cluster customization and stages during cluster creation][img-hdi-cluster-states]</span></span>

<span data-ttu-id="41211-168">O script é executado enquanto o HDInsight está sendo configurado.</span><span class="sxs-lookup"><span data-stu-id="41211-168">The script runs while HDInsight is being configured.</span></span> <span data-ttu-id="41211-169">Nesse estágio, o script é executado em paralelo com todos os nós especificados no cluster e é executado com os privilégios de raiz nos nós.</span><span class="sxs-lookup"><span data-stu-id="41211-169">At this stage, the script runs in parallel on all the specified nodes in the cluster, and runs with root privileges on the nodes.</span></span>

> [!NOTE]
> <span data-ttu-id="41211-170">Como o script é executado com o privilégio de nível raiz nos nós do cluster, você pode executar operações como parar e iniciar serviços, incluindo os serviços relacionados ao Hadoop.</span><span class="sxs-lookup"><span data-stu-id="41211-170">Because the script runs with root level privilege on the cluster nodes, you can perform operations like stopping and starting services, including Hadoop-related services.</span></span> <span data-ttu-id="41211-171">Se você parar quaisquer serviços, você deve garantir que os serviços Ambari e outros serviços relacionados ao Hadoop estejam funcionando antes do script terminar a execução.</span><span class="sxs-lookup"><span data-stu-id="41211-171">If you stop services, you must ensure that the Ambari service and other Hadoop-related services are up and running before the script finishes running.</span></span> <span data-ttu-id="41211-172">Esses serviços são necessários para determinar com êxito a integridade e o estado do cluster enquanto ele está sendo criado.</span><span class="sxs-lookup"><span data-stu-id="41211-172">These services are required to successfully determine the health and state of the cluster while it is being created.</span></span>


<span data-ttu-id="41211-173">Durante a criação do cluster, você pode usar várias ações de script simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="41211-173">During cluster creation, you can use multiple script actions at once.</span></span> <span data-ttu-id="41211-174">Esses scripts são invocados na ordem em que eles foram especificados.</span><span class="sxs-lookup"><span data-stu-id="41211-174">These scripts are invoked in the order in which they were specified.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="41211-175">Ações de script devem ser concluídas em 60 minutos ou atingirão o tempo limite.</span><span class="sxs-lookup"><span data-stu-id="41211-175">Script actions must complete within 60 minutes, or timeout.</span></span> <span data-ttu-id="41211-176">Durante o provisionamento do cluster, o script é executado simultaneamente com outros processos de instalação e configuração.</span><span class="sxs-lookup"><span data-stu-id="41211-176">During cluster provisioning, the script runs concurrently with other setup and configuration processes.</span></span> <span data-ttu-id="41211-177">A competição por recursos, como tempo de CPU ou largura de banda rede, pode fazer com que o script leve mais tempo para ser concluído comparado ao seu tempo de conclusão no ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="41211-177">Competition for resources such as CPU time or network bandwidth may cause the script to take longer to finish than it does in your development environment.</span></span>
>
> <span data-ttu-id="41211-178">Para minimizar o tempo necessário para executar o script, evite tarefas como baixar e compilar aplicativos da origem.</span><span class="sxs-lookup"><span data-stu-id="41211-178">To minimize the time it takes to run the script, avoid tasks such as downloading and compiling applications from source.</span></span> <span data-ttu-id="41211-179">Pré-compile aplicativos e armazene o binário no Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="41211-179">Pre-compile applications and store the binary in Azure Storage.</span></span>


### <a name="script-action-on-a-running-cluster"></a><span data-ttu-id="41211-180">Ação de script em um cluster em execução</span><span class="sxs-lookup"><span data-stu-id="41211-180">Script action on a running cluster</span></span>

<span data-ttu-id="41211-181">Ao contrário das ações de script usadas durante a criação do cluster, uma falha em um script executado em um cluster já em execução não faz com o cluster mude automaticamente para um estado de falha.</span><span class="sxs-lookup"><span data-stu-id="41211-181">Unlike script actions used during cluster creation, a failure in a script ran on an already running cluster does not automatically cause the cluster to change to a failed state.</span></span> <span data-ttu-id="41211-182">Quando um script é concluído, o cluster deve retornar a um estado "em execução".</span><span class="sxs-lookup"><span data-stu-id="41211-182">Once a script completes, the cluster should return to a "running" state.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="41211-183">Mesmo que o cluster apresente um estado "em execução", o script com falha pode ter partes desfeitas.</span><span class="sxs-lookup"><span data-stu-id="41211-183">Even if the cluster has a 'running' state, the failed script may have broken things.</span></span> <span data-ttu-id="41211-184">Por exemplo, um script poderia excluir arquivos necessários para o cluster.</span><span class="sxs-lookup"><span data-stu-id="41211-184">For example, a script could delete files needed by the cluster.</span></span>
>
> <span data-ttu-id="41211-185">As ações de script são executadas com privilégios de raiz, portanto, você deve assegurar que entendeu o que faz um script antes de aplicá-lo ao seu cluster.</span><span class="sxs-lookup"><span data-stu-id="41211-185">Scripts actions run with root privileges, so you should make sure that you understand what a script does before applying it to your cluster.</span></span>

<span data-ttu-id="41211-186">Ao aplicar um script a um cluster, o estado do cluster muda de **Em execução** para **Aceito**, depois para **Configuração do HDInsight** e, por fim, de volta para **Executando** para os scripts bem-sucedidos.</span><span class="sxs-lookup"><span data-stu-id="41211-186">When applying a script to a cluster, the cluster state changes to from **Running** to **Accepted**, then **HDInsight configuration**, and finally back to **Running** for successful scripts.</span></span> <span data-ttu-id="41211-187">O status do script é registrado no histórico de ações do script e você pode usar essas informações para determinar se o script teve êxito ou falhou.</span><span class="sxs-lookup"><span data-stu-id="41211-187">The script status is logged in the script action history, and you can use this information to determine whether the script succeeded or failed.</span></span> <span data-ttu-id="41211-188">Por exemplo, o cmdlet `Get-AzureRmHDInsightScriptActionHistory` do PowerShell pode ser usado para exibir o status de um script.</span><span class="sxs-lookup"><span data-stu-id="41211-188">For example, the `Get-AzureRmHDInsightScriptActionHistory` PowerShell cmdlet can be used to view the status of a script.</span></span> <span data-ttu-id="41211-189">Isso retorna informações semelhantes ao seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="41211-189">It returns information similar to the following text:</span></span>

    ScriptExecutionId : 635918532516474303
    StartTime         : 8/14/2017 7:40:55 PM
    EndTime           : 8/14/2017 7:41:05 PM
    Status            : Succeeded

> [!NOTE]
> <span data-ttu-id="41211-190">Se você alterou a senha de usuário (admin) do cluster depois que o cluster foi criado, ações de script executadas em relação a esse cluster podem falhar.</span><span class="sxs-lookup"><span data-stu-id="41211-190">If you have changed the cluster user (admin) password after the cluster was created, script actions ran against this cluster may fail.</span></span> <span data-ttu-id="41211-191">Se você tiver ações de script persistente direcionadas para nós de trabalho, esses scripts poderão falhar quando você dimensionar o cluster.</span><span class="sxs-lookup"><span data-stu-id="41211-191">If you have any persisted script actions that target worker nodes, these scripts may fail when you scale the cluster.</span></span>

## <a name="example-script-action-scripts"></a><span data-ttu-id="41211-192">Scripts de exemplo de Ação de Script</span><span class="sxs-lookup"><span data-stu-id="41211-192">Example Script Action scripts</span></span>

<span data-ttu-id="41211-193">Scripts de ação de script podem ser usados por meio dos utilitários a seguir:</span><span class="sxs-lookup"><span data-stu-id="41211-193">Script Action scripts can be used through the following utilities:</span></span>

* <span data-ttu-id="41211-194">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="41211-194">Azure portal</span></span>
* <span data-ttu-id="41211-195">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="41211-195">Azure PowerShell</span></span>
* <span data-ttu-id="41211-196">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="41211-196">Azure CLI</span></span>
* <span data-ttu-id="41211-197">SDK do .NET do HDInsight</span><span class="sxs-lookup"><span data-stu-id="41211-197">HDInsight .NET SDK</span></span>

<span data-ttu-id="41211-198">O HDInsight fornece scripts para instalar os seguintes componentes nos clusters do HDInsight:</span><span class="sxs-lookup"><span data-stu-id="41211-198">HDInsight provides scripts to install the following components on HDInsight clusters:</span></span>

| <span data-ttu-id="41211-199">Nome</span><span class="sxs-lookup"><span data-stu-id="41211-199">Name</span></span> | <span data-ttu-id="41211-200">Script</span><span class="sxs-lookup"><span data-stu-id="41211-200">Script</span></span> |
| --- | --- |
| <span data-ttu-id="41211-201">**Adicionar uma conta de armazenamento do Azure**</span><span class="sxs-lookup"><span data-stu-id="41211-201">**Add an Azure Storage account**</span></span> |<span data-ttu-id="41211-202">https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh. Veja [Adicionar armazenamento adicional a um cluster HDInsight](hdinsight-hadoop-add-storage.md).</span><span class="sxs-lookup"><span data-stu-id="41211-202">https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh. See [Add additional storage to an HDInsight cluster](hdinsight-hadoop-add-storage.md).</span></span> |
| <span data-ttu-id="41211-203">**Instalar o Hue**</span><span class="sxs-lookup"><span data-stu-id="41211-203">**Install Hue**</span></span> |<span data-ttu-id="41211-204">https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. Veja [Instalar e usar o Hue em clusters HDInsight](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="41211-204">https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. See [Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> |
| <span data-ttu-id="41211-205">**Instalar o Presto**</span><span class="sxs-lookup"><span data-stu-id="41211-205">**Install Presto**</span></span> |<span data-ttu-id="41211-206">https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh. Veja [Instalar e usar o Presto em clusters HDInsight](hdinsight-hadoop-install-presto.md).</span><span class="sxs-lookup"><span data-stu-id="41211-206">https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh. See [Install and use Presto on HDInsight clusters](hdinsight-hadoop-install-presto.md).</span></span> |
| <span data-ttu-id="41211-207">**Instalar Solr**</span><span class="sxs-lookup"><span data-stu-id="41211-207">**Install Solr**</span></span> |<span data-ttu-id="41211-208">https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh. Consulte [Instalar e usar o Solr em clusters HDInsight](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="41211-208">https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh. See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span> |
| <span data-ttu-id="41211-209">**Instalar o Giraph**</span><span class="sxs-lookup"><span data-stu-id="41211-209">**Install Giraph**</span></span> |<span data-ttu-id="41211-210">https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh. Consulte [Instalar e usar o Giraph em clusters HDInsight](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="41211-210">https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh. See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> |
| <span data-ttu-id="41211-211">**Pré-carregar bibliotecas Hive**</span><span class="sxs-lookup"><span data-stu-id="41211-211">**Pre-load Hive libraries**</span></span> |<span data-ttu-id="41211-212">https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh. Veja [Adicionar bibliotecas do Hive em clusters HDInsight](hdinsight-hadoop-add-hive-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="41211-212">https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh. See [Add Hive libraries on HDInsight clusters](hdinsight-hadoop-add-hive-libraries.md).</span></span> |
| <span data-ttu-id="41211-213">**Instalar ou atualizar Mono**</span><span class="sxs-lookup"><span data-stu-id="41211-213">**Install or update Mono**</span></span> | <span data-ttu-id="41211-214">https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash.</span><span class="sxs-lookup"><span data-stu-id="41211-214">https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash.</span></span> <span data-ttu-id="41211-215">Veja [Instalar ou atualizar o Mono no HDInsight](hdinsight-hadoop-install-mono.md).</span><span class="sxs-lookup"><span data-stu-id="41211-215">See [Install or update Mono on HDInsight](hdinsight-hadoop-install-mono.md).</span></span> |

## <a name="use-a-script-action-during-cluster-creation"></a><span data-ttu-id="41211-216">Usar uma Ação de Script durante a criação do cluster</span><span class="sxs-lookup"><span data-stu-id="41211-216">Use a Script Action during cluster creation</span></span>

<span data-ttu-id="41211-217">Esta seção fornece exemplos sobre as diferentes maneiras em que você pode usar ações de script ao criar um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="41211-217">This section provides examples on the different ways you can use script actions when creating an HDInsight cluster.</span></span>

### <a name="use-a-script-action-during-cluster-creation-from-the-azure-portal"></a><span data-ttu-id="41211-218">Usar uma Ação de Script durante a criação do cluster no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="41211-218">Use a Script Action during cluster creation from the Azure portal</span></span>

1. <span data-ttu-id="41211-219">Comece criando um cluster como descrito em [Criar clusters Hadoop no HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="41211-219">Start creating a cluster as described at [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="41211-220">Pare quando atingir a seção __Resumo do cluster__.</span><span class="sxs-lookup"><span data-stu-id="41211-220">Stop when you reach the __Cluster summary__ section.</span></span>

2. <span data-ttu-id="41211-221">Na seção __Resumo do cluster__, selecione o link __editar__ para __Configurações avançadas__.</span><span class="sxs-lookup"><span data-stu-id="41211-221">From the __Cluster summary__ section, select the __edit__ link for __Advanced settings__.</span></span>

    ![Link Configurações avançadas](./media/hdinsight-hadoop-customize-cluster-linux/advanced-settings-link.png)

3. <span data-ttu-id="41211-223">Na seção __Configurações avançadas__, selecione __Ações de script__.</span><span class="sxs-lookup"><span data-stu-id="41211-223">From the __Advanced settings__ section, select __Script actions__.</span></span> <span data-ttu-id="41211-224">Na seção __Ações de script__, selecione __+ Enviar novo__</span><span class="sxs-lookup"><span data-stu-id="41211-224">From the __Script actions__ section, select __+ Submit new__</span></span>

    ![Enviar uma nova ação de script](./media/hdinsight-hadoop-customize-cluster-linux/add-script-action.png)

4. <span data-ttu-id="41211-226">Use a entrada __Selecionar um script__ para selecionar um script pré-criado.</span><span class="sxs-lookup"><span data-stu-id="41211-226">Use the __Select a script__ entry to select a pre-made script.</span></span> <span data-ttu-id="41211-227">Para usar um script personalizado, selecione __Personalizado__ e, em seguida, forneça o __Nome__ e o __URI do script Bash__ para o seu script.</span><span class="sxs-lookup"><span data-stu-id="41211-227">To use a custom script, select __Custom__ and then provide the __Name__ and __Bash script URI__ for your script.</span></span>

    ![Adicionar um script no formulário selecionar script](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    <span data-ttu-id="41211-229">A tabela a seguir descreve os elementos no formulário:</span><span class="sxs-lookup"><span data-stu-id="41211-229">The following table describes the elements on the form:</span></span>

    | <span data-ttu-id="41211-230">Propriedade</span><span class="sxs-lookup"><span data-stu-id="41211-230">Property</span></span> | <span data-ttu-id="41211-231">Valor</span><span class="sxs-lookup"><span data-stu-id="41211-231">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="41211-232">Selecionar um script</span><span class="sxs-lookup"><span data-stu-id="41211-232">Select a script</span></span> | <span data-ttu-id="41211-233">Para usar seu próprio script, selecione __Personalizado__.</span><span class="sxs-lookup"><span data-stu-id="41211-233">To use your own script, select __Custom__.</span></span> <span data-ttu-id="41211-234">Caso contrário, selecione um dos scripts fornecidos.</span><span class="sxs-lookup"><span data-stu-id="41211-234">Otherwise, select one of the provided scripts.</span></span> |
    | <span data-ttu-id="41211-235">Nome</span><span class="sxs-lookup"><span data-stu-id="41211-235">Name</span></span> |<span data-ttu-id="41211-236">Especifique um nome para a ação de script.</span><span class="sxs-lookup"><span data-stu-id="41211-236">Specify a name for the script action.</span></span> |
    | <span data-ttu-id="41211-237">URI do script Bash</span><span class="sxs-lookup"><span data-stu-id="41211-237">Bash script URI</span></span> |<span data-ttu-id="41211-238">Especifique o URI para o script que é chamado para personalizar o cluster.</span><span class="sxs-lookup"><span data-stu-id="41211-238">Specify the URI to the script that is invoked to customize the cluster.</span></span> |
    | <span data-ttu-id="41211-239">Cabeçalho/Trabalho/Zookeeper</span><span class="sxs-lookup"><span data-stu-id="41211-239">Head/Worker/Zookeeper</span></span> |<span data-ttu-id="41211-240">Especifique os nós (**Cabeçalho**, de **Trabalho** ou **ZooKeeper**) nos quais o script de personalização é executado.</span><span class="sxs-lookup"><span data-stu-id="41211-240">Specify the nodes (**Head**, **Worker**, or **ZooKeeper**) on which the customization script is run.</span></span> |
    | <span data-ttu-id="41211-241">parâmetros</span><span class="sxs-lookup"><span data-stu-id="41211-241">Parameters</span></span> |<span data-ttu-id="41211-242">Especifique os parâmetros, se exigido pelo script.</span><span class="sxs-lookup"><span data-stu-id="41211-242">Specify the parameters, if required by the script.</span></span> |

    <span data-ttu-id="41211-243">Use a entrada __Persistir essa ação de script__ para garantir que o script seja aplicado durante operações de colocação em escala.</span><span class="sxs-lookup"><span data-stu-id="41211-243">Use the __Persist this script action__ entry to ensure that the script is applied during scaling operations.</span></span>

5. <span data-ttu-id="41211-244">Selecione __Criar__ para salvar o script.</span><span class="sxs-lookup"><span data-stu-id="41211-244">Select __Create__ to save the script.</span></span> <span data-ttu-id="41211-245">Em seguida, você pode usar __+ Enviar novo__ para adicionar outro script.</span><span class="sxs-lookup"><span data-stu-id="41211-245">You can then use __+ Submit new__ to add another script.</span></span>

    ![Várias ações de script](./media/hdinsight-hadoop-customize-cluster-linux/multiple-scripts.png)

    <span data-ttu-id="41211-247">Quando você terminar de adicionar scripts, use o botão __Selecionar__ e, em seguida, o botão __Avançar__ para retornar à seção __Resumo do cluster__.</span><span class="sxs-lookup"><span data-stu-id="41211-247">When you are done adding scripts, use the __Select__ button, and then the __Next__ button to return to the __Cluster summary__ section.</span></span>

3. <span data-ttu-id="41211-248">Para criar o cluster, selecione __Criar__ na seleção __Resumo do cluster__.</span><span class="sxs-lookup"><span data-stu-id="41211-248">To create the cluster, select __Create__ from the __Cluster summary__ selection.</span></span>

### <a name="use-a-script-action-from-azure-resource-manager-templates"></a><span data-ttu-id="41211-249">Usar uma Ação de Script em modelos do Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="41211-249">Use a Script Action from Azure Resource Manager templates</span></span>

<span data-ttu-id="41211-250">Os exemplos nesta seção demonstram como usar ações de script com modelos do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="41211-250">The examples in this section demonstrate how to use script actions with Azure Resource Manager templates.</span></span>

#### <a name="before-you-begin"></a><span data-ttu-id="41211-251">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="41211-251">Before you begin</span></span>

* <span data-ttu-id="41211-252">Para obter informações sobre como configurar uma estação de trabalho para executar os cmdlets do PowerShell do HDInsight, consulte [Instalar e configurar o PowerShell do Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="41211-252">For information about configuring a workstation to run HDInsight Powershell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="41211-253">Para obter instruções sobre como criar modelos, confira [Criando modelos do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="41211-253">For instructions on how to create templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="41211-254">Se você ainda não utilizou o PowerShell do Azure com o Gerenciador de recursos, consulte [Uso do PowerShell do Azure com o Gerenciador de recursos do Azure](../azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="41211-254">If you have not previously used Azure PowerShell with Resource Manager, see [Using Azure PowerShell with Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

#### <a name="create-clusters-using-script-action"></a><span data-ttu-id="41211-255">Criar clusters usando a Ação de Script</span><span class="sxs-lookup"><span data-stu-id="41211-255">Create clusters using Script Action</span></span>

1. <span data-ttu-id="41211-256">Copie o modelo a seguir para um local no computador.</span><span class="sxs-lookup"><span data-stu-id="41211-256">Copy the following template to a location on your computer.</span></span> <span data-ttu-id="41211-257">Esse modelo instala o Giraph nos nós de cabeçalho e em nós de trabalho no cluster.</span><span class="sxs-lookup"><span data-stu-id="41211-257">This template installs Giraph on the headnodes and worker nodes in the cluster.</span></span> <span data-ttu-id="41211-258">Você também pode verificar se o modelo JSON é válido.</span><span class="sxs-lookup"><span data-stu-id="41211-258">You can also verify if the JSON template is valid.</span></span> <span data-ttu-id="41211-259">Cole o conteúdo do modelo no [JSONLint](http://jsonlint.com/), uma ferramenta online para validação de JSON.</span><span class="sxs-lookup"><span data-stu-id="41211-259">Paste your template content into [JSONLint](http://jsonlint.com/), an online JSON validation tool.</span></span>

            {
            "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
            "contentVersion": "1.0.0.0",
            "parameters": {
                "clusterLocation": {
                    "type": "string",
                    "defaultValue": "West US",
                    "allowedValues": [ "West US" ]
                },
                "clusterName": {
                    "type": "string"
                },
                "clusterUserName": {
                    "type": "string",
                    "defaultValue": "admin"
                },
                "clusterUserPassword": {
                    "type": "securestring"
                },
                "sshUserName": {
                    "type": "string",
                    "defaultValue": "username"
                },
                "sshPassword": {
                    "type": "securestring"
                },
                "clusterStorageAccountName": {
                    "type": "string"
                },
                "clusterStorageAccountResourceGroup": {
                    "type": "string"
                },
                "clusterStorageType": {
                    "type": "string",
                    "defaultValue": "Standard_LRS",
                    "allowedValues": [
                        "Standard_LRS",
                        "Standard_GRS",
                        "Standard_ZRS"
                    ]
                },
                "clusterStorageAccountContainer": {
                    "type": "string"
                },
                "clusterHeadNodeCount": {
                    "type": "int",
                    "defaultValue": 1
                },
                "clusterWorkerNodeCount": {
                    "type": "int",
                    "defaultValue": 2
                }
            },
            "variables": {
            },
            "resources": [
                {
                    "name": "[parameters('clusterStorageAccountName')]",
                    "type": "Microsoft.Storage/storageAccounts",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-05-01-preview",
                    "dependsOn": [ ],
                    "tags": { },
                    "properties": {
                        "accountType": "[parameters('clusterStorageType')]"
                    }
                },
                {
                    "name": "[parameters('clusterName')]",
                    "type": "Microsoft.HDInsight/clusters",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-03-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Storage/storageAccounts/', parameters('clusterStorageAccountName'))]"
                    ],
                    "tags": { },
                    "properties": {
                        "clusterVersion": "3.2",
                        "osType": "Linux",
                        "clusterDefinition": {
                            "kind": "hadoop",
                            "configurations": {
                                "gateway": {
                                    "restAuthCredential.isEnabled": true,
                                    "restAuthCredential.username": "[parameters('clusterUserName')]",
                                    "restAuthCredential.password": "[parameters('clusterUserPassword')]"
                                }
                            }
                        },
                        "storageProfile": {
                            "storageaccounts": [
                                {
                                    "name": "[concat(parameters('clusterStorageAccountName'),'.blob.core.windows.net')]",
                                    "isDefault": true,
                                    "container": "[parameters('clusterStorageAccountContainer')]",
                                    "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('clusterStorageAccountName')), '2015-05-01-preview').key1]"
                                }
                            ]
                        },
                        "computeProfile": {
                            "roles": [
                                {
                                    "name": "headnode",
                                    "targetInstanceCount": "[parameters('clusterHeadNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installGiraph",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                },
                                {
                                    "name": "workernode",
                                    "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installR",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                }
                            ]
                        }
                    }
                }
            ],
            "outputs": {
                "cluster":{
                    "type" : "object",
                    "value" : "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
                }
            }
        }
2. <span data-ttu-id="41211-260">Inicie o Azure PowerShell e faça logon em sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="41211-260">Start Azure PowerShell and Log in to your Azure account.</span></span> <span data-ttu-id="41211-261">Depois de fornecer suas credenciais, o comando retornará informações sobre sua conta.</span><span class="sxs-lookup"><span data-stu-id="41211-261">After providing your credentials, the command returns information about your account.</span></span>

        Add-AzureRmAccount

        Id                             Type       ...
        --                             ----
        someone@example.com            User       ...
3. <span data-ttu-id="41211-262">Se você tiver várias assinaturas, forneça a ID da assinatura que deseja usar para implantação.</span><span class="sxs-lookup"><span data-stu-id="41211-262">If you have multiple subscriptions, provide the subscription ID you wish to use for deployment.</span></span>

        Select-AzureRmSubscription -SubscriptionID <YourSubscriptionId>

    > [!NOTE]
    > <span data-ttu-id="41211-263">Você pode usar `Get-AzureRmSubscription` para obter uma lista de todas as assinaturas associadas à sua conta, o que inclui a ID de assinatura de cada uma delas.</span><span class="sxs-lookup"><span data-stu-id="41211-263">You can use `Get-AzureRmSubscription` to get a list of all subscriptions associated with your account, which includes the subscription ID for each one.</span></span>

4. <span data-ttu-id="41211-264">Se você não tiver um grupo de recursos existente, crie um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="41211-264">If you do not have an existing resource group, create a resource group.</span></span> <span data-ttu-id="41211-265">Forneça o nome do grupo de recursos e o local necessários para sua solução.</span><span class="sxs-lookup"><span data-stu-id="41211-265">Provide the name of the resource group and location that you need for your solution.</span></span> <span data-ttu-id="41211-266">Um resumo do novo grupo de recursos é retornado.</span><span class="sxs-lookup"><span data-stu-id="41211-266">A summary of the new resource group is returned.</span></span>

        New-AzureRmResourceGroup -Name myresourcegroup -Location "West US"

        ResourceGroupName : myresourcegroup
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/######/resourceGroups/ExampleResourceGroup

5. <span data-ttu-id="41211-267">Para criar uma implantação para seu grupo de recursos, execute o comando **New-AzureRmResourceGroupDeployment** e forneça os parâmetros necessários.</span><span class="sxs-lookup"><span data-stu-id="41211-267">To create a deployment for your resource group, run the **New-AzureRmResourceGroupDeployment** command and provide the necessary parameters.</span></span> <span data-ttu-id="41211-268">Os parâmetros incluem os seguintes dados:</span><span class="sxs-lookup"><span data-stu-id="41211-268">The parameters include the following data:</span></span>

    * <span data-ttu-id="41211-269">Um nome para sua implantação</span><span class="sxs-lookup"><span data-stu-id="41211-269">A name for your deployment</span></span>
    * <span data-ttu-id="41211-270">O nome do seu grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="41211-270">The name of your resource group</span></span>
    * <span data-ttu-id="41211-271">O caminho ou a URL para o modelo que você criou.</span><span class="sxs-lookup"><span data-stu-id="41211-271">The path or URL to the template you created.</span></span>

  <span data-ttu-id="41211-272">Se seu modelo exige quaisquer parâmetros, você deve passar esses parâmetros também.</span><span class="sxs-lookup"><span data-stu-id="41211-272">If your template requires any parameters, you must pass those parameters as well.</span></span> <span data-ttu-id="41211-273">Nesse caso, a ação de script para instalar o R no cluster não exige nenhum parâmetro.</span><span class="sxs-lookup"><span data-stu-id="41211-273">In this case, the script action to install R on the cluster does not require any parameters.</span></span>

        New-AzureRmResourceGroupDeployment -Name mydeployment -ResourceGroupName myresourcegroup -TemplateFile <PathOrLinkToTemplate>

    <span data-ttu-id="41211-274">Você será solicitado a fornecer valores para os parâmetros definidos no modelo.</span><span class="sxs-lookup"><span data-stu-id="41211-274">You are prompted to provide values for the parameters defined in the template.</span></span>

1. <span data-ttu-id="41211-275">Quando o grupo de recursos tiver sido implantado, você verá um resumo da implantação.</span><span class="sxs-lookup"><span data-stu-id="41211-275">When the resource group has been deployed, a summary of the deployment is displayed.</span></span>

          DeploymentName    : mydeployment
          ResourceGroupName : myresourcegroup
          ProvisioningState : Succeeded
          Timestamp         : 8/14/2017 7:00:27 PM
          Mode              : Incremental
          ...

2. <span data-ttu-id="41211-276">Se sua implantação falhar, você poderá usar os cmdlets a seguir para obter informações sobre as falhas.</span><span class="sxs-lookup"><span data-stu-id="41211-276">If your deployment fails, you can use the following cmdlets to get information about the failures.</span></span>

        Get-AzureRmResourceGroupDeployment -ResourceGroupName myresourcegroup -ProvisioningState Failed

### <a name="use-a-script-action-during-cluster-creation-from-azure-powershell"></a><span data-ttu-id="41211-277">Usar uma Ação de Script durante a criação do cluster no Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="41211-277">Use a Script Action during cluster creation from Azure PowerShell</span></span>

<span data-ttu-id="41211-278">Nesta seção, usamos o cmdlet [Add-AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) para invocar scripts usando a Ação de Script para personalizar um cluster.</span><span class="sxs-lookup"><span data-stu-id="41211-278">In this section, we use the [Add-AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) cmdlet to invoke scripts by using Script Action to customize a cluster.</span></span> <span data-ttu-id="41211-279">Antes de prosseguir, verifique se você instalou e configurou o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="41211-279">Before proceeding, make sure you have installed and configured Azure PowerShell.</span></span> <span data-ttu-id="41211-280">Para obter informações sobre como configurar uma estação de trabalho para executar os cmdlets do PowerShell do HDInsight, confira [Instalar e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="41211-280">For information about configuring a workstation to run HDInsight PowerShell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="41211-281">O script a seguir demonstra como aplicar uma ação de script ao criar um cluster usando o PowerShell:</span><span class="sxs-lookup"><span data-stu-id="41211-281">The following script demonstrates how to apply a script action when creating a cluster using PowerShell:</span></span>

<span data-ttu-id="41211-282">[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=5-90)]</span><span class="sxs-lookup"><span data-stu-id="41211-282">[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=5-90)]</span></span>

<span data-ttu-id="41211-283">Pode levar alguns minutos até que o cluster seja criado.</span><span class="sxs-lookup"><span data-stu-id="41211-283">It can take several minutes before the cluster is created.</span></span>

### <a name="use-a-script-action-during-cluster-creation-from-the-hdinsight-net-sdk"></a><span data-ttu-id="41211-284">Usar uma Ação de Script durante a criação do cluster no SDK do .NET do HDInsight</span><span class="sxs-lookup"><span data-stu-id="41211-284">Use a Script Action during cluster creation from the HDInsight .NET SDK</span></span>

<span data-ttu-id="41211-285">O SDK do .NET do HDInsight fornece bibliotecas de cliente que facilitam o trabalho com o HDInsight por meio de um aplicativo .NET.</span><span class="sxs-lookup"><span data-stu-id="41211-285">The HDInsight .NET SDK provides client libraries that makes it easier to work with HDInsight from a .NET application.</span></span> <span data-ttu-id="41211-286">Para ver um exemplo de código, consulte [Criar clusters baseados em Linux no HDInsight usando o SDK do .NET](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).</span><span class="sxs-lookup"><span data-stu-id="41211-286">For a code sample, see [Create Linux-based clusters in HDInsight using the .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).</span></span>

## <a name="apply-a-script-action-to-a-running-cluster"></a><span data-ttu-id="41211-287">Aplicar uma Ação de Script em um cluster em execução</span><span class="sxs-lookup"><span data-stu-id="41211-287">Apply a Script Action to a running cluster</span></span>

<span data-ttu-id="41211-288">Nesta seção, aprenda como aplicar ações de script a um cluster em execução.</span><span class="sxs-lookup"><span data-stu-id="41211-288">In this section, learn how to apply script actions to a running cluster.</span></span>

### <a name="apply-a-script-action-to-a-running-cluster-from-the-azure-portal"></a><span data-ttu-id="41211-289">Aplicar uma Ação de Script em um cluster em execução no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="41211-289">Apply a Script Action to a running cluster from the Azure portal</span></span>

1. <span data-ttu-id="41211-290">No [Portal do Azure](https://portal.azure.com), escolha o cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="41211-290">From the [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="41211-291">Na visão geral do cluster HDInsight, selecione o bloco **Ações de Script**.</span><span class="sxs-lookup"><span data-stu-id="41211-291">From the HDInsight cluster overview, select the **Script Actions** tile.</span></span>

    ![Bloco Ações de script](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > <span data-ttu-id="41211-293">Você também pode selecionar **Todas as configurações** e **Ações de Script** na seção Configurações.</span><span class="sxs-lookup"><span data-stu-id="41211-293">You can also select **All settings** and then select **Script Actions** from the Settings section.</span></span>

3. <span data-ttu-id="41211-294">Na parte superior da seção Ações de Script, selecione **Enviar novo**.</span><span class="sxs-lookup"><span data-stu-id="41211-294">From the top of the Script Actions section, select **Submit new**.</span></span>

    ![Adicionar um script a um cluster em execução](./media/hdinsight-hadoop-customize-cluster-linux/add-script-running-cluster.png)

4. <span data-ttu-id="41211-296">Use a entrada __Selecionar um script__ para selecionar um script pré-criado.</span><span class="sxs-lookup"><span data-stu-id="41211-296">Use the __Select a script__ entry to select a pre-made script.</span></span> <span data-ttu-id="41211-297">Para usar um script personalizado, selecione __Personalizado__ e, em seguida, forneça o __Nome__ e o __URI do script Bash__ para o seu script.</span><span class="sxs-lookup"><span data-stu-id="41211-297">To use a custom script, select __Custom__ and then provide the __Name__ and __Bash script URI__ for your script.</span></span>

    ![Adicionar um script no formulário selecionar script](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    <span data-ttu-id="41211-299">A tabela a seguir descreve os elementos no formulário:</span><span class="sxs-lookup"><span data-stu-id="41211-299">The following table describes the elements on the form:</span></span>

    | <span data-ttu-id="41211-300">Propriedade</span><span class="sxs-lookup"><span data-stu-id="41211-300">Property</span></span> | <span data-ttu-id="41211-301">Valor</span><span class="sxs-lookup"><span data-stu-id="41211-301">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="41211-302">Selecionar um script</span><span class="sxs-lookup"><span data-stu-id="41211-302">Select a script</span></span> | <span data-ttu-id="41211-303">Para usar seu próprio script, selecione __personalizado__.</span><span class="sxs-lookup"><span data-stu-id="41211-303">To use your own script, select __custom__.</span></span> <span data-ttu-id="41211-304">Caso contrário, selecione um script fornecido.</span><span class="sxs-lookup"><span data-stu-id="41211-304">Otherwise, select a provided script.</span></span> |
    | <span data-ttu-id="41211-305">Nome</span><span class="sxs-lookup"><span data-stu-id="41211-305">Name</span></span> |<span data-ttu-id="41211-306">Especifique um nome para a ação de script.</span><span class="sxs-lookup"><span data-stu-id="41211-306">Specify a name for the script action.</span></span> |
    | <span data-ttu-id="41211-307">URI do script Bash</span><span class="sxs-lookup"><span data-stu-id="41211-307">Bash script URI</span></span> |<span data-ttu-id="41211-308">Especifique o URI para o script que é chamado para personalizar o cluster.</span><span class="sxs-lookup"><span data-stu-id="41211-308">Specify the URI to the script that is invoked to customize the cluster.</span></span> |
    | <span data-ttu-id="41211-309">Cabeçalho/Trabalho/Zookeeper</span><span class="sxs-lookup"><span data-stu-id="41211-309">Head/Worker/Zookeeper</span></span> |<span data-ttu-id="41211-310">Especifique os nós (**Cabeçalho**, de **Trabalho** ou **ZooKeeper**) nos quais o script de personalização é executado.</span><span class="sxs-lookup"><span data-stu-id="41211-310">Specify the nodes (**Head**, **Worker**, or **ZooKeeper**) on which the customization script is run.</span></span> |
    | <span data-ttu-id="41211-311">parâmetros</span><span class="sxs-lookup"><span data-stu-id="41211-311">Parameters</span></span> |<span data-ttu-id="41211-312">Especifique os parâmetros, se exigido pelo script.</span><span class="sxs-lookup"><span data-stu-id="41211-312">Specify the parameters, if required by the script.</span></span> |

    <span data-ttu-id="41211-313">Use a entrada __Persistir essa ação de script__ para garantir que o script seja aplicado durante operações de colocação em escala.</span><span class="sxs-lookup"><span data-stu-id="41211-313">Use the __Persist this script action__ entry to make sure the script is applied during scaling operations.</span></span>

5. <span data-ttu-id="41211-314">Por fim, use o botão **Criar** para aplicar o script ao cluster.</span><span class="sxs-lookup"><span data-stu-id="41211-314">Finally, use the **Create** button to apply the script to the cluster.</span></span>

### <a name="apply-a-script-action-to-a-running-cluster-from-azure-powershell"></a><span data-ttu-id="41211-315">Aplicar uma Ação de Script em um cluster em execução no Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="41211-315">Apply a Script Action to a running cluster from Azure PowerShell</span></span>

<span data-ttu-id="41211-316">Antes de prosseguir, verifique se você instalou e configurou o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="41211-316">Before proceeding, make sure you have installed and configured Azure PowerShell.</span></span> <span data-ttu-id="41211-317">Para obter informações sobre como configurar uma estação de trabalho para executar os cmdlets do PowerShell do HDInsight, confira [Instalar e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="41211-317">For information about configuring a workstation to run HDInsight PowerShell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="41211-318">O exemplo a seguir demonstra como aplicar uma ação de script a um cluster em execução:</span><span class="sxs-lookup"><span data-stu-id="41211-318">The following example demonstrates how to apply a script action to a running cluster:</span></span>

<span data-ttu-id="41211-319">[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=105-117)]</span><span class="sxs-lookup"><span data-stu-id="41211-319">[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=105-117)]</span></span>

<span data-ttu-id="41211-320">Quando a operação for concluída, você receberá informações semelhantes ao seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="41211-320">Once the operation completes, you receive information similar to the following text:</span></span>

    OperationState  : Succeeded
    ErrorMessage    :
    Name            : Giraph
    Uri             : https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh
    Parameters      :
    NodeTypes       : {HeadNode, WorkerNode}

### <a name="apply-a-script-action-to-a-running-cluster-from-the-azure-cli"></a><span data-ttu-id="41211-321">Aplicar uma Ação de Script em um cluster em execução da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="41211-321">Apply a Script Action to a running cluster from the Azure CLI</span></span>

<span data-ttu-id="41211-322">Antes de prosseguir, certifique-se de ter instalado e configurado a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="41211-322">Before proceeding, make sure you have installed and configured the Azure CLI.</span></span> <span data-ttu-id="41211-323">Para obter mais informações, consulte [Instalar a CLI do Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="41211-323">For more information, see [Install the Azure CLI](../cli-install-nodejs.md).</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. <span data-ttu-id="41211-324">Para alternar para o modo Azure Resource Manager, use o seguinte comando na linha de comando:</span><span class="sxs-lookup"><span data-stu-id="41211-324">To switch to Azure Resource Manager mode, use the following command at the command line:</span></span>

        azure config mode arm

2. <span data-ttu-id="41211-325">Use o comando a seguir para fazer logon em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="41211-325">Use the following to authenticate to your Azure subscription.</span></span>

        azure login

3. <span data-ttu-id="41211-326">Use o comando a seguir para aplicar uma ação de script a um cluster em execução</span><span class="sxs-lookup"><span data-stu-id="41211-326">Use the following command to apply a script action to a running cluster</span></span>

        azure hdinsight script-action create <clustername> -g <resourcegroupname> -n <scriptname> -u <scriptURI> -t <nodetypes>

    <span data-ttu-id="41211-327">Se você omitir parâmetros para esse comando, você será solicitado a fornecê-los.</span><span class="sxs-lookup"><span data-stu-id="41211-327">If you omit parameters for this command, you are prompted for them.</span></span> <span data-ttu-id="41211-328">Caso o script especificado com `-u` aceite parâmetros, você poderá especificá-los usando o parâmetro `-p`.</span><span class="sxs-lookup"><span data-stu-id="41211-328">If the script you specify with `-u` accepts parameters, you can specify them using the `-p` parameter.</span></span>

    <span data-ttu-id="41211-329">Os tipos de nós válidos são `headnode`, `workernode` e `zookeeper`.</span><span class="sxs-lookup"><span data-stu-id="41211-329">Valid node types are `headnode`, `workernode`, and `zookeeper`.</span></span> <span data-ttu-id="41211-330">Caso o script deva ser aplicado a vários tipos de nós, especifique os tipos separados por um ';'.</span><span class="sxs-lookup"><span data-stu-id="41211-330">If the script should be applied to multiple node types, specify the types separated by a ';'.</span></span> <span data-ttu-id="41211-331">Por exemplo: `-n headnode;workernode`.</span><span class="sxs-lookup"><span data-stu-id="41211-331">For example, `-n headnode;workernode`.</span></span>

    <span data-ttu-id="41211-332">Para persistir o script, adicione `--persistOnSuccess`.</span><span class="sxs-lookup"><span data-stu-id="41211-332">To persist the script, add the `--persistOnSuccess`.</span></span> <span data-ttu-id="41211-333">Também é possível persistir o script posteriormente usando `azure hdinsight script-action persisted set`.</span><span class="sxs-lookup"><span data-stu-id="41211-333">You can also persist the script later by using `azure hdinsight script-action persisted set`.</span></span>

    <span data-ttu-id="41211-334">Quando o trabalho for concluído, você receberá uma saída semelhante ao seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="41211-334">Once the job completes, you receive output similar to the following text:</span></span>

        info:    Executing command hdinsight script-action create
        + Executing Script Action on HDInsight cluster
        data:    Operation Info
        data:    ---------------
        data:    Operation status:
        data:    Operation ID:  b707b10e-e633-45c0-baa9-8aed3d348c13
        info:    hdinsight script-action create command OK

### <a name="apply-a-script-action-to-a-running-cluster-using-rest-api"></a><span data-ttu-id="41211-335">Aplicar uma Ação de Script em um cluster em execução usando a API REST</span><span class="sxs-lookup"><span data-stu-id="41211-335">Apply a Script Action to a running cluster using REST API</span></span>

<span data-ttu-id="41211-336">Consulte [Executar Ações de Script em um cluster em execução](https://msdn.microsoft.com/library/azure/mt668441.aspx).</span><span class="sxs-lookup"><span data-stu-id="41211-336">See [Run Script Actions on a running cluster](https://msdn.microsoft.com/library/azure/mt668441.aspx).</span></span>

### <a name="apply-a-script-action-to-a-running-cluster-from-the-hdinsight-net-sdk"></a><span data-ttu-id="41211-337">Aplicar uma Ação de Script em um cluster em execução no SDK do .NET do HDInsight</span><span class="sxs-lookup"><span data-stu-id="41211-337">Apply a Script Action to a running cluster from the HDInsight .NET SDK</span></span>

<span data-ttu-id="41211-338">Para obter um exemplo de como usar o SDK do .NET para aplicar scripts a um cluster, consulte [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span><span class="sxs-lookup"><span data-stu-id="41211-338">For an example of using the .NET SDK to apply scripts to a cluster, see [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span></span>

## <a name="view-history-promote-and-demote-script-actions"></a><span data-ttu-id="41211-339">Exibir o histórico, promover e rebaixar Ações de Script</span><span class="sxs-lookup"><span data-stu-id="41211-339">View history, promote, and demote Script Actions</span></span>

### <a name="using-the-azure-portal"></a><span data-ttu-id="41211-340">Usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="41211-340">Using the Azure portal</span></span>

1. <span data-ttu-id="41211-341">No [Portal do Azure](https://portal.azure.com), escolha o cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="41211-341">From the [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="41211-342">Na visão geral do cluster HDInsight, selecione o bloco **Ações de Script**.</span><span class="sxs-lookup"><span data-stu-id="41211-342">From the HDInsight cluster overview, select the **Script Actions** tile.</span></span>

    ![Bloco Ações de script](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > <span data-ttu-id="41211-344">Você também pode selecionar **Todas as configurações** e **Ações de Script** na seção Configurações.</span><span class="sxs-lookup"><span data-stu-id="41211-344">You can also select **All settings** and then select **Script Actions** from the Settings section.</span></span>

4. <span data-ttu-id="41211-345">Um histórico de scripts para esse cluster é exibido na seção Ações de Script.</span><span class="sxs-lookup"><span data-stu-id="41211-345">A history of scripts for this cluster is displayed on the Script Actions section.</span></span> <span data-ttu-id="41211-346">Essas informações incluem uma lista de scripts persistentes.</span><span class="sxs-lookup"><span data-stu-id="41211-346">This information includes a list of persisted scripts.</span></span> <span data-ttu-id="41211-347">Na captura de tela abaixo, você pode ver que o script Solr foi executado nesse cluster.</span><span class="sxs-lookup"><span data-stu-id="41211-347">In the screenshot below, you can see that the Solr script has been ran on this cluster.</span></span> <span data-ttu-id="41211-348">A captura de tela não mostra nenhum os scripts persistente.</span><span class="sxs-lookup"><span data-stu-id="41211-348">The screenshot does not show any persisted scripts.</span></span>

    ![Seção Ações de Script](./media/hdinsight-hadoop-customize-cluster-linux/script-action-history.png)

5. <span data-ttu-id="41211-350">A seleção de um script no histórico exibe a seção Propriedades desse script.</span><span class="sxs-lookup"><span data-stu-id="41211-350">Selecting a script from the history displays the Properties section for this script.</span></span> <span data-ttu-id="41211-351">Na parte superior da tela, é possível executar novamente o script ou promovê-lo.</span><span class="sxs-lookup"><span data-stu-id="41211-351">From the top of the screen, you can rerun the script or promote it.</span></span>

    ![Propriedades de Ações de script](./media/hdinsight-hadoop-customize-cluster-linux/promote-script-actions.png)

6. <span data-ttu-id="41211-353">Também é possível usar **...** à direita das entradas na seção Ações de Script para executar ações.</span><span class="sxs-lookup"><span data-stu-id="41211-353">You can also use the **...** to the right of entries on the Script Actions section to perform actions.</span></span>

    ![Ações de script... uso](./media/hdinsight-hadoop-customize-cluster-linux/deletepromoted.png)

### <a name="using-azure-powershell"></a><span data-ttu-id="41211-355">Usando o PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="41211-355">Using Azure PowerShell</span></span>

| <span data-ttu-id="41211-356">Usar o seguinte...</span><span class="sxs-lookup"><span data-stu-id="41211-356">Use the following...</span></span> | <span data-ttu-id="41211-357">Para...</span><span class="sxs-lookup"><span data-stu-id="41211-357">To ...</span></span> |
| --- | --- |
| <span data-ttu-id="41211-358">Get-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="41211-358">Get-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="41211-359">Recuperar informações sobre as ações de script persistentes</span><span class="sxs-lookup"><span data-stu-id="41211-359">Retrieve information on persisted script actions</span></span> |
| <span data-ttu-id="41211-360">Get-AzureRmHDInsightScriptActionHistory</span><span class="sxs-lookup"><span data-stu-id="41211-360">Get-AzureRmHDInsightScriptActionHistory</span></span> |<span data-ttu-id="41211-361">Recuperar um histórico das ações de script aplicadas no cluster ou detalhes de um script específico</span><span class="sxs-lookup"><span data-stu-id="41211-361">Retrieve a history of script actions applied to the cluster, or details for a specific script</span></span> |
| <span data-ttu-id="41211-362">Set-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="41211-362">Set-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="41211-363">Promove uma ação de script ad hoc para uma ação de script persistente</span><span class="sxs-lookup"><span data-stu-id="41211-363">Promotes an ad hoc script action to a persisted script action</span></span> |
| <span data-ttu-id="41211-364">Remove-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="41211-364">Remove-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="41211-365">Rebaixa uma ação de script persistente a uma ação ad hoc</span><span class="sxs-lookup"><span data-stu-id="41211-365">Demotes a persisted script action to an ad hoc action</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="41211-366">Usar `Remove-AzureRmHDInsightPersistedScriptAction` não desfaz as ações realizadas por um script.</span><span class="sxs-lookup"><span data-stu-id="41211-366">Using `Remove-AzureRmHDInsightPersistedScriptAction` does not undo the actions performed by a script.</span></span> <span data-ttu-id="41211-367">Esse cmdlet remove apenas o sinalizador persistente.</span><span class="sxs-lookup"><span data-stu-id="41211-367">This cmdlet only removes the persisted flag.</span></span>

<span data-ttu-id="41211-368">O script de exemplo a seguir demonstra como usar os cmdlets para promover e depois rebaixar um script.</span><span class="sxs-lookup"><span data-stu-id="41211-368">The following example script demonstrates using the cmdlets to promote, then demote a script.</span></span>

<span data-ttu-id="41211-369">[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=123-140)]</span><span class="sxs-lookup"><span data-stu-id="41211-369">[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=123-140)]</span></span>

### <a name="using-the-azure-cli"></a><span data-ttu-id="41211-370">Usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="41211-370">Using the Azure CLI</span></span>

| <span data-ttu-id="41211-371">Usar o seguinte...</span><span class="sxs-lookup"><span data-stu-id="41211-371">Use the following...</span></span> | <span data-ttu-id="41211-372">Para...</span><span class="sxs-lookup"><span data-stu-id="41211-372">To ...</span></span> |
| --- | --- |
| `azure hdinsight script-action persisted list <clustername>` |<span data-ttu-id="41211-373">Recuperar uma lista de ações de script persistente</span><span class="sxs-lookup"><span data-stu-id="41211-373">Retrieve a list of persisted script actions</span></span> |
| `azure hdinsight script-action persisted show <clustername> <scriptname>` |<span data-ttu-id="41211-374">Recuperar informações sobre uma ação de script persistente específica</span><span class="sxs-lookup"><span data-stu-id="41211-374">Retrieve information on a specific persisted script action</span></span> |
| `azure hdinsight script-action history list <clustername>` |<span data-ttu-id="41211-375">Recuperar um histórico das ações de script aplicadas ao cluster</span><span class="sxs-lookup"><span data-stu-id="41211-375">Retrieve a history of script actions applied to the cluster</span></span> |
| `azure hdinsight script-action history show <clustername> <scriptname>` |<span data-ttu-id="41211-376">Recuperar informações sobre uma ação de script específica</span><span class="sxs-lookup"><span data-stu-id="41211-376">Retrieve information on a specific script action</span></span> |
| `azure hdinsight script action persisted set <clustername> <scriptexecutionid>` |<span data-ttu-id="41211-377">Promove uma ação de script ad hoc para uma ação de script persistente</span><span class="sxs-lookup"><span data-stu-id="41211-377">Promotes an ad hoc script action to a persisted script action</span></span> |
| `azure hdinsight script-action persisted delete <clustername> <scriptname>` |<span data-ttu-id="41211-378">Rebaixa uma ação de script persistente a uma ação ad hoc</span><span class="sxs-lookup"><span data-stu-id="41211-378">Demotes a persisted script action to an ad hoc action</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="41211-379">Usar `azure hdinsight script-action persisted delete` não desfaz as ações realizadas por um script.</span><span class="sxs-lookup"><span data-stu-id="41211-379">Using `azure hdinsight script-action persisted delete` does not undo the actions performed by a script.</span></span> <span data-ttu-id="41211-380">Esse cmdlet remove apenas o sinalizador persistente.</span><span class="sxs-lookup"><span data-stu-id="41211-380">This cmdlet only removes the persisted flag.</span></span>

### <a name="using-the-hdinsight-net-sdk"></a><span data-ttu-id="41211-381">Usando o SDK do .NET do HDInsight</span><span class="sxs-lookup"><span data-stu-id="41211-381">Using the HDInsight .NET SDK</span></span>

<span data-ttu-id="41211-382">Para obter um exemplo de como usar o SDK do .NET para recuperar o histórico de scripts de um cluster, promover ou rebaixar scripts, consulte [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span><span class="sxs-lookup"><span data-stu-id="41211-382">For an example of using the .NET SDK to retrieve script history from a cluster, promote or demote scripts, see [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span></span>

> [!NOTE]
> <span data-ttu-id="41211-383">Este exemplo também demonstra como instalar um aplicativo do HDInsight usando o SDK do .NET.</span><span class="sxs-lookup"><span data-stu-id="41211-383">This example also demonstrates how to install an HDInsight application using the .NET SDK.</span></span>

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a><span data-ttu-id="41211-384">Suporte para software livre utilizado em clusters do HDInsight</span><span class="sxs-lookup"><span data-stu-id="41211-384">Support for open-source software used on HDInsight clusters</span></span>

<span data-ttu-id="41211-385">O serviço do Microsoft Azure HDInsight usa um ecossistema de tecnologias de software livre formado em torno do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="41211-385">The Microsoft Azure HDInsight service uses an ecosystem of open-source technologies formed around Hadoop.</span></span> <span data-ttu-id="41211-386">O Microsoft Azure fornece um nível geral de suporte para tecnologias de software livre.</span><span class="sxs-lookup"><span data-stu-id="41211-386">Microsoft Azure provides a general level of support for open-source technologies.</span></span> <span data-ttu-id="41211-387">Para obter mais informações, consulte a seção **Escopo do Suporte** do [site de perguntas frequentes sobre o Suporte do Azure](https://azure.microsoft.com/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="41211-387">For more information, see the **Support Scope** section of the [Azure Support FAQ website](https://azure.microsoft.com/support/faq/).</span></span> <span data-ttu-id="41211-388">O serviço HDInsight fornece um nível adicional de suporte a componentes internos.</span><span class="sxs-lookup"><span data-stu-id="41211-388">The HDInsight service provides an additional level of support for built-in components.</span></span>

<span data-ttu-id="41211-389">Há dois tipos de componentes de software livre disponíveis no serviço HDInsight:</span><span class="sxs-lookup"><span data-stu-id="41211-389">There are two types of open-source components that are available in the HDInsight service:</span></span>

* <span data-ttu-id="41211-390">**Componentes internos** : estes componentes estão pré-instalado em clusters HDInsight e fornecem a funcionalidade básica do cluster.</span><span class="sxs-lookup"><span data-stu-id="41211-390">**Built-in components** - These components are pre-installed on HDInsight clusters and provide core functionality of the cluster.</span></span> <span data-ttu-id="41211-391">Por exemplo, o gerenciador de recursos YARN RM, o HiveQL (linguagem de consulta do Hive) e a biblioteca Mahout pertencem a esta categoria.</span><span class="sxs-lookup"><span data-stu-id="41211-391">For example, YARN ResourceManager, the Hive query language (HiveQL), and the Mahout library belong to this category.</span></span> <span data-ttu-id="41211-392">Uma lista completa dos componentes de cluster está disponível em [Novidades nas versões do cluster Hadoop fornecidas pelo HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="41211-392">A full list of cluster components is available in [What's new in the Hadoop cluster versions provided by HDInsight](hdinsight-component-versioning.md).</span></span>
* <span data-ttu-id="41211-393">**Componentes personalizados** : como usuário do cluster, você pode instalar ou usar em sua carga de trabalho qualquer componente disponível na comunidade ou criado por você.</span><span class="sxs-lookup"><span data-stu-id="41211-393">**Custom components** - You, as a user of the cluster, can install or use in your workload any component available in the community or created by you.</span></span>

> [!WARNING]
> <span data-ttu-id="41211-394">Componentes fornecidos com o cluster HDInsight contam com suporte total.</span><span class="sxs-lookup"><span data-stu-id="41211-394">Components provided with the HDInsight cluster are fully supported.</span></span> <span data-ttu-id="41211-395">O Suporte da Microsoft ajuda a isolar e resolver problemas relacionados a esses componentes.</span><span class="sxs-lookup"><span data-stu-id="41211-395">Microsoft Support helps to isolate and resolve issues related to these components.</span></span>
>
> <span data-ttu-id="41211-396">Componentes personalizados recebem suporte comercialmente razoável para ajudá-lo a solucionar o problema.</span><span class="sxs-lookup"><span data-stu-id="41211-396">Custom components receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="41211-397">O suporte da Microsoft pode estar apto a resolver o problema OU pode solicitar que você contate canais disponíveis para as tecnologias de software livre em que é encontrado conhecimento profundo sobre essa tecnologia.</span><span class="sxs-lookup"><span data-stu-id="41211-397">Microsoft support may be able to resolve the issue OR they may ask you to engage available channels for the open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="41211-398">Por exemplo, há muitos sites de comunidades que podem ser usados, como o [Fórum do MSDN para o HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Além disso, os projetos do Apache têm sites do projeto em [http://apache.org](http://apache.org), por exemplo: [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="41211-398">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>

<span data-ttu-id="41211-399">O serviço HDInsight possibilita o uso de componentes personalizados de várias formas.</span><span class="sxs-lookup"><span data-stu-id="41211-399">The HDInsight service provides several ways to use custom components.</span></span> <span data-ttu-id="41211-400">O mesmo nível de suporte se aplica, independentemente de como um componente é usado ou instalado no cluster.</span><span class="sxs-lookup"><span data-stu-id="41211-400">The same level of support applies, regardless of how a component is used or installed on the cluster.</span></span> <span data-ttu-id="41211-401">A lista a seguir descreve as formas mais comuns de usar os componentes personalizados em clusters HDInsight:</span><span class="sxs-lookup"><span data-stu-id="41211-401">The following list describes the most common ways that custom components can be used on HDInsight clusters:</span></span>

1. <span data-ttu-id="41211-402">Envio de trabalhos: trabalhos do Hadoop ou de outros tipos que executam ou usam componentes personalizados podem ser enviados para o cluster.</span><span class="sxs-lookup"><span data-stu-id="41211-402">Job submission - Hadoop or other types of jobs that execute or use custom components can be submitted to the cluster.</span></span>

2. <span data-ttu-id="41211-403">Personalização de clusters: durante a criação de clusters, você pode especificar configurações adicionais e componentes personalizados para instalação nos nós de cluster.</span><span class="sxs-lookup"><span data-stu-id="41211-403">Cluster customization - During cluster creation, you can specify additional settings and custom components that are installed on the cluster nodes.</span></span>

3. <span data-ttu-id="41211-404">Exemplos: para componentes personalizados populares, a Microsoft e outras empresas podem fornecer exemplos de uso desses componentes em clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="41211-404">Samples - For popular custom components, Microsoft and others may provide samples of how these components can be used on the HDInsight clusters.</span></span> <span data-ttu-id="41211-405">Esses exemplos são fornecidos sem suporte.</span><span class="sxs-lookup"><span data-stu-id="41211-405">These samples are provided without support.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="41211-406">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="41211-406">Troubleshooting</span></span>

<span data-ttu-id="41211-407">Você pode usar a interface do usuário da Web Ambari para exibir as informações registradas pelas ações de script.</span><span class="sxs-lookup"><span data-stu-id="41211-407">You can use Ambari web UI to view information logged by script actions.</span></span> <span data-ttu-id="41211-408">Se o script falhar durante a criação do cluster, os logs também estarão disponíveis na conta de armazenamento padrão associada ao cluster.</span><span class="sxs-lookup"><span data-stu-id="41211-408">If the script fails during cluster creation, the logs are also available in the default storage account associated with the cluster.</span></span> <span data-ttu-id="41211-409">Esta seção fornece informações sobre como recuperar logs usando ambas as opções.</span><span class="sxs-lookup"><span data-stu-id="41211-409">This section provides information on how to retrieve the logs using both these options.</span></span>

### <a name="using-the-ambari-web-ui"></a><span data-ttu-id="41211-410">Usando a interface do usuário da Web do Ambari</span><span class="sxs-lookup"><span data-stu-id="41211-410">Using the Ambari Web UI</span></span>

1. <span data-ttu-id="41211-411">No seu navegador, navegue até https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="41211-411">In your browser, navigate to https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="41211-412">Substitua CLUSTERNAME com o nome do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="41211-412">Replace CLUSTERNAME with the name of your HDInsight cluster.</span></span>

    <span data-ttu-id="41211-413">Quando solicitado, insira o nome de conta de administrador (admin) e a senha correspondente para o cluster.</span><span class="sxs-lookup"><span data-stu-id="41211-413">When prompted, enter the admin account name (admin) and password for the cluster.</span></span> <span data-ttu-id="41211-414">Você precisará reinserir as credenciais de administrador em um formulário da Web.</span><span class="sxs-lookup"><span data-stu-id="41211-414">You may have to reenter the admin credentials in a web form.</span></span>

2. <span data-ttu-id="41211-415">Na barra na parte superior da página, selecione a entrada **ops**.</span><span class="sxs-lookup"><span data-stu-id="41211-415">From the bar at the top of the page, select the **ops** entry.</span></span> <span data-ttu-id="41211-416">Uma lista das operações atuais e anteriores realizadas no cluster por meio do Ambari é exibida.</span><span class="sxs-lookup"><span data-stu-id="41211-416">A list of current and previous operations performed on the cluster through Ambari is displayed.</span></span>

    ![Barra de interface do usuário da Web do Ambari com o item "ops" selecionado](./media/hdinsight-hadoop-customize-cluster-linux/ambari-nav.png)

3. <span data-ttu-id="41211-418">Localize as entradas com **run\_customscriptaction** na coluna **Operações**.</span><span class="sxs-lookup"><span data-stu-id="41211-418">Find the entries that have **run\_customscriptaction** in the **Operations** column.</span></span> <span data-ttu-id="41211-419">Essas entradas são criadas quando as Ações de Script são executadas.</span><span class="sxs-lookup"><span data-stu-id="41211-419">These entries are created when the Script Actions run.</span></span>

    ![Captura de tela de operações](./media/hdinsight-hadoop-customize-cluster-linux/ambariscriptaction.png)

    <span data-ttu-id="41211-421">Para exibir a saída STDOUT e STDERR, selecione a entrada run\customscriptaction e faça uma busca detalhada pelos links.</span><span class="sxs-lookup"><span data-stu-id="41211-421">To view the STDOUT and STDERR output, select the run\customscriptaction entry and drill down through the links.</span></span> <span data-ttu-id="41211-422">Essa saída é gerada quando o script é executado e pode conter informações úteis.</span><span class="sxs-lookup"><span data-stu-id="41211-422">This output is generated when the script runs, and may contain useful information.</span></span>

### <a name="access-logs-from-the-default-storage-account"></a><span data-ttu-id="41211-423">Acessar logs na conta de armazenamento padrão</span><span class="sxs-lookup"><span data-stu-id="41211-423">Access logs from the default storage account</span></span>

<span data-ttu-id="41211-424">Se a criação do cluster falhar devido a um erro de ação de script, os logs poderão ser acessados da conta de armazenamento de cluster.</span><span class="sxs-lookup"><span data-stu-id="41211-424">If the cluster creation fails due to a script action error, the logs can be accessed from the cluster storage account.</span></span>

* <span data-ttu-id="41211-425">Os logs de armazenamento estão disponíveis em `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.</span><span class="sxs-lookup"><span data-stu-id="41211-425">The storage logs are available at `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.</span></span>

    ![Captura de tela de operações](./media/hdinsight-hadoop-customize-cluster-linux/script_action_logs_in_storage.png)

    <span data-ttu-id="41211-427">Nesse diretório, os logs são organizados separadamente em nó de cabeçalho, nó de trabalho e nós do zookeeper.</span><span class="sxs-lookup"><span data-stu-id="41211-427">Under this directory, the logs are organized separately for headnode, workernode, and zookeeper nodes.</span></span> <span data-ttu-id="41211-428">Alguns exemplos incluem:</span><span class="sxs-lookup"><span data-stu-id="41211-428">Some examples are:</span></span>

    * <span data-ttu-id="41211-429">**Nó de cabeçalho** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="41211-429">**Headnode** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`</span></span>

    * <span data-ttu-id="41211-430">**Nó de trabalho** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="41211-430">**Worker node** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`</span></span>

    * <span data-ttu-id="41211-431">**Nó zookeeper** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="41211-431">**Zookeeper node** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`</span></span>

* <span data-ttu-id="41211-432">Todos os stdout e stderr do host correspondentes são carregados para a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="41211-432">All stdout and stderr of the corresponding host is uploaded to the storage account.</span></span> <span data-ttu-id="41211-433">Há um **output-\*.txt** e um **errors-\*.txt** para cada ação de script.</span><span class="sxs-lookup"><span data-stu-id="41211-433">There is one **output-\*.txt** and **errors-\*.txt** for each script action.</span></span> <span data-ttu-id="41211-434">O arquivo *.txt de saída contém informações sobre o URI do script que foi executado no host.</span><span class="sxs-lookup"><span data-stu-id="41211-434">The output-*.txt file contains information about the URI of the script that got run on the host.</span></span> <span data-ttu-id="41211-435">Por exemplo,</span><span class="sxs-lookup"><span data-stu-id="41211-435">For example</span></span>

        'Start downloading script locally: ', u'https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh'

* <span data-ttu-id="41211-436">É possível criar repetidamente um cluster de ação de script com o mesmo nome.</span><span class="sxs-lookup"><span data-stu-id="41211-436">It's possible that you repeatedly create a script action cluster with the same name.</span></span> <span data-ttu-id="41211-437">Nesse caso, você pode distinguir os logs relevantes com base no nome da pasta DATE.</span><span class="sxs-lookup"><span data-stu-id="41211-437">In such case, you can distinguish the relevant logs based on the DATE folder name.</span></span> <span data-ttu-id="41211-438">Por exemplo, a estrutura de pastas de um cluster (mycluster) criado em datas diferentes será semelhante às seguintes entradas de log:</span><span class="sxs-lookup"><span data-stu-id="41211-438">For example, the folder structure for a cluster (mycluster) created on different dates appears similar to the following log entries:</span></span>

    <span data-ttu-id="41211-439">`\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`</span><span class="sxs-lookup"><span data-stu-id="41211-439">`\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`</span></span>

* <span data-ttu-id="41211-440">Se você criar um cluster de ação de script com o mesmo nome no mesmo dia, você poderá usar o prefixo exclusivo para identificar os arquivos de log relevantes.</span><span class="sxs-lookup"><span data-stu-id="41211-440">If you create a script action cluster with the same name on the same day, you can use the unique prefix to identify the relevant log files.</span></span>

* <span data-ttu-id="41211-441">Se você criar um cluster perto de 12:00 (meia-noite), é possível que os arquivos de log incluam dois dias.</span><span class="sxs-lookup"><span data-stu-id="41211-441">If you create a cluster near 12:00AM (midnight), it's possible that the log files span across two days.</span></span> <span data-ttu-id="41211-442">Nesses casos, você verá duas pastas com datas diferentes para o mesmo cluster.</span><span class="sxs-lookup"><span data-stu-id="41211-442">In such cases, you see two different date folders for the same cluster.</span></span>

* <span data-ttu-id="41211-443">Carregar arquivos de log no contêiner padrão pode levar até 5 minutos, especialmente para clusters grandes.</span><span class="sxs-lookup"><span data-stu-id="41211-443">Uploading log files to the default container can take up to 5 mins, especially for large clusters.</span></span> <span data-ttu-id="41211-444">Portanto, se desejar acessar os logs, você não deverá imediatamente excluir o cluster se uma ação de script falhar.</span><span class="sxs-lookup"><span data-stu-id="41211-444">So, if you want to access the logs, you should not immediately delete the cluster if a script action fails.</span></span>

### <a name="ambari-watchdog"></a><span data-ttu-id="41211-445">Ambari Watchdog</span><span class="sxs-lookup"><span data-stu-id="41211-445">Ambari watchdog</span></span>

> [!WARNING]
> <span data-ttu-id="41211-446">Não altere a senha do Ambari Watchdog (hdinsightwatchdog) no seu cluster HDInsight baseado em Linux.</span><span class="sxs-lookup"><span data-stu-id="41211-446">Do not change the password for the Ambari Watchdog (hdinsightwatchdog) on your Linux-based HDInsight cluster.</span></span> <span data-ttu-id="41211-447">A alteração da senha para essa conta interrompe a capacidade de executar novas ações de script no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="41211-447">Changing the password for this account breaks the ability to run new script actions on the HDInsight cluster.</span></span>

### <a name="cant-import-name-blobservice"></a><span data-ttu-id="41211-448">Não é possível importar o BlobService de nome</span><span class="sxs-lookup"><span data-stu-id="41211-448">Can't import name BlobService</span></span>

<span data-ttu-id="41211-449">__Sintomas__: falha na ação de script.</span><span class="sxs-lookup"><span data-stu-id="41211-449">__Symptoms__: The script action fails.</span></span> <span data-ttu-id="41211-450">Texto semelhante ao seguinte erro é exibido quando você exibe a operação no Ambari:</span><span class="sxs-lookup"><span data-stu-id="41211-450">Text similar to the following error is displayed when you view the operation in Ambari:</span></span>

```
Traceback (most recent call list):
  File "/var/lib/ambari-agent/cache/custom_actions/scripts/run_customscriptaction.py", line 21, in <module>
    from azure.storage.blob import BlobService
ImportError: cannot import name BlobService
```

<span data-ttu-id="41211-451">__Causa__: esse erro ocorre se você atualizar o cliente de Armazenamento do Azure Python incluído com o cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="41211-451">__Cause__: This error occurs if you upgrade the Python Azure Storage client that is included with the HDInsight cluster.</span></span> <span data-ttu-id="41211-452">O HDInsight espera o cliente de Armazenamento do Azure 0.20.0.</span><span class="sxs-lookup"><span data-stu-id="41211-452">HDInsight expects Azure Storage client 0.20.0.</span></span>

<span data-ttu-id="41211-453">__Resolução__: para resolver esse erro, conecte-se manualmente a cada nó de cluster usando `ssh`, e use o comando a seguir para reinstalar a versão do cliente de armazenamento correta:</span><span class="sxs-lookup"><span data-stu-id="41211-453">__Resolution__: To resolve this error, manually connect to each cluster node using `ssh` and use the following command to reinstall the correct storage client version:</span></span>

```
sudo pip install azure-storage==0.20.0
```

<span data-ttu-id="41211-454">Para saber mais sobre como se conectar ao cluster com o SSH, veja [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="41211-454">For information on connecting to the cluster with SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

### <a name="history-doesnt-show-scripts-used-during-cluster-creation"></a><span data-ttu-id="41211-455">O histórico de não mostra os scripts usados durante a criação do cluster</span><span class="sxs-lookup"><span data-stu-id="41211-455">History doesn't show scripts used during cluster creation</span></span>

<span data-ttu-id="41211-456">Se o cluster tiver sido criado antes de 15 de março de 2016, talvez você não veja uma entrada no histórico de Ação de Script.</span><span class="sxs-lookup"><span data-stu-id="41211-456">If your cluster was created before March 15, 2016, you may not see an entry in Script Action history.</span></span> <span data-ttu-id="41211-457">Se você redimensionar o cluster após 15 de março de 2016, os scripts usados durante a criação do cluster aparecerão no histórico, pois eles são aplicados aos novos nós no cluster como parte da operação de redimensionamento.</span><span class="sxs-lookup"><span data-stu-id="41211-457">If you resize the cluster after March 15, 2016, the scripts using during cluster creation appear in history as they are applied to new nodes in the cluster as part of the resize operation.</span></span>

<span data-ttu-id="41211-458">Há duas exceções:</span><span class="sxs-lookup"><span data-stu-id="41211-458">There are two exceptions:</span></span>

* <span data-ttu-id="41211-459">Se o cluster tiver sido criado antes de 1º de setembro de 2015.</span><span class="sxs-lookup"><span data-stu-id="41211-459">If your cluster was created before September 1, 2015.</span></span> <span data-ttu-id="41211-460">Esta data é quando as Ações de Script foram introduzidas.</span><span class="sxs-lookup"><span data-stu-id="41211-460">This date is when Script Actions were introduced.</span></span> <span data-ttu-id="41211-461">Qualquer cluster criado antes dessa data não poderia ter usado as Ações de Script para a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="41211-461">Any cluster created before this date could not have used Script Actions for cluster creation.</span></span>

* <span data-ttu-id="41211-462">Se você tiver usado várias Ações de Script durante a criação do cluster e se tiver usado o mesmo nome para vários scripts ou o mesmo nome, o mesmo URI, mas diferentes parâmetros para vários scripts.</span><span class="sxs-lookup"><span data-stu-id="41211-462">If you used multiple Script Actions during cluster creation, and used the same name for multiple scripts, or the same name, same URI, but different parameters for multiple scripts.</span></span> <span data-ttu-id="41211-463">Nesses casos, você recebe o erro a seguir:</span><span class="sxs-lookup"><span data-stu-id="41211-463">In these cases, you receive the following error:</span></span>

    <span data-ttu-id="41211-464">Nenhuma nova ação de script pode ser executada nesse cluster devido aos nomes de script conflitantes nos scripts existentes.</span><span class="sxs-lookup"><span data-stu-id="41211-464">No new script actions can be ran on this cluster due to conflicting script names in existing scripts.</span></span> <span data-ttu-id="41211-465">Os nomes de script fornecidos na criação do cluster devem ser exclusivos.</span><span class="sxs-lookup"><span data-stu-id="41211-465">Script names provided at cluster create must be all unique.</span></span> <span data-ttu-id="41211-466">Os scripts existentes são executados no redimensionamento.</span><span class="sxs-lookup"><span data-stu-id="41211-466">Existing scripts are ran on resize.</span></span>

## <a name="next-steps"></a><span data-ttu-id="41211-467">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="41211-467">Next steps</span></span>

* [<span data-ttu-id="41211-468">Desenvolver scripts de Ação de Script para o HDInsight</span><span class="sxs-lookup"><span data-stu-id="41211-468">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions-linux.md)
* [<span data-ttu-id="41211-469">Instalar e usar o Solr em clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="41211-469">Install and use Solr on HDInsight clusters</span></span>](hdinsight-hadoop-solr-install-linux.md)
* [<span data-ttu-id="41211-470">Instalar e usar o Giraph em clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="41211-470">Install and use Giraph on HDInsight clusters</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* [<span data-ttu-id="41211-471">Acrescentar armazenamento adicional a um cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="41211-471">Add additional storage to an HDInsight cluster</span></span>](hdinsight-hadoop-add-storage.md)

<span data-ttu-id="41211-472">[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster-linux/HDI-Cluster-state.png "Estágios durante a criação de cluster"</span><span class="sxs-lookup"><span data-stu-id="41211-472">[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster-linux/HDI-Cluster-state.png "Stages during cluster creation"</span></span>
