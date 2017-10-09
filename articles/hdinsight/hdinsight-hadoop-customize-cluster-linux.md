---
title: "clusters de HDInsight aaaCustomize usando as ações de script - Azure | Microsoft Docs"
description: "Adicione componentes personalizados, que clusters de HDInsight com base em tooLinux usando ações de Script. Ações de script são scripts de Bash que podem ser toocustomize usado Olá cluster configuração ou adicionar mais serviços e utilitários, como o matiz, Solr ou R."
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
ms.openlocfilehash: ff22680a8a50b21985f6941f1edaf1dcf863d13f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-linux-based-hdinsight-clusters-using-script-action"></a><span data-ttu-id="d213c-104">Personalizar clusters HDInsight baseados em Linux usando a Ação de Script</span><span class="sxs-lookup"><span data-stu-id="d213c-104">Customize Linux-based HDInsight clusters using Script Action</span></span>

<span data-ttu-id="d213c-105">HDInsight fornece uma opção de configuração chamada **ação de Script** que chama scripts personalizados que personalizar Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="d213c-105">HDInsight provides a configuration option called **Script Action** that invokes custom scripts that customize hello cluster.</span></span> <span data-ttu-id="d213c-106">Esses scripts são usado tooinstall componentes adicionais e alterar as definições de configuração.</span><span class="sxs-lookup"><span data-stu-id="d213c-106">These scripts are used tooinstall additional components and change configuration settings.</span></span> <span data-ttu-id="d213c-107">Ações de script podem ser usadas durante ou após a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="d213c-107">Script actions can be used during or after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d213c-108">ações de script Hello capacidade toouse em um cluster já em execução está disponível somente para clusters HDInsight baseados em Linux.</span><span class="sxs-lookup"><span data-stu-id="d213c-108">hello ability toouse script actions on an already running cluster is only available for Linux-based HDInsight clusters.</span></span>
>
> <span data-ttu-id="d213c-109">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="d213c-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d213c-110">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="d213c-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="d213c-111">Ações de script também podem ser publicado toohello Marketplace do Azure como um aplicativo de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d213c-111">Script actions can also be published toohello Azure Marketplace as an HDInsight application.</span></span> <span data-ttu-id="d213c-112">Alguns exemplos de saudação neste documento mostram como você pode instalar um aplicativo de HDInsight usando comandos de ação de script do PowerShell e hello .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="d213c-112">Some of hello examples in this document show how you can install an HDInsight application using script action commands from PowerShell and hello .NET SDK.</span></span> <span data-ttu-id="d213c-113">Para obter mais informações sobre aplicativos de HDInsight, consulte [HDInsight publicar aplicativos em hello Azure Marketplace](hdinsight-apps-publish-applications.md).</span><span class="sxs-lookup"><span data-stu-id="d213c-113">For more information on HDInsight applications, see [Publish HDInsight applications into hello Azure Marketplace](hdinsight-apps-publish-applications.md).</span></span>

## <a name="permissions"></a><span data-ttu-id="d213c-114">Permissões</span><span class="sxs-lookup"><span data-stu-id="d213c-114">Permissions</span></span>

<span data-ttu-id="d213c-115">Se você estiver usando um cluster de HDInsight ingressado no domínio, há duas permissões Ambari que são necessárias para usar ações de script com cluster hello:</span><span class="sxs-lookup"><span data-stu-id="d213c-115">If you are using a domain-joined HDInsight cluster, there are two Ambari permissions that are required when using script actions with hello cluster:</span></span>

* <span data-ttu-id="d213c-116">**AMBARI. EXECUTAR\_personalizado\_comando**: função de administrador do Ambari Olá tem essa permissão por padrão.</span><span class="sxs-lookup"><span data-stu-id="d213c-116">**AMBARI.RUN\_CUSTOM\_COMMAND**: hello Ambari Administrator role has this permission by default.</span></span>
* <span data-ttu-id="d213c-117">**CLUSTER. EXECUTAR\_personalizado\_comando**: ambos Olá administrador de Cluster HDInsight e Ambari administrador têm essa permissão por padrão.</span><span class="sxs-lookup"><span data-stu-id="d213c-117">**CLUSTER.RUN\_CUSTOM\_COMMAND**: Both hello HDInsight Cluster Administrator and Ambari Administrator have this permission by default.</span></span>

<span data-ttu-id="d213c-118">Para obter mais informações sobre como trabalhar com permissões com o HDInsight de domínio, consulte [gerenciar clusters de HDInsight de domínio](hdinsight-domain-joined-manage.md).</span><span class="sxs-lookup"><span data-stu-id="d213c-118">For more information on working with permissions with domain-joined HDInsight, see [Manage domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span></span>

## <a name="access-control"></a><span data-ttu-id="d213c-119">Controle de acesso</span><span class="sxs-lookup"><span data-stu-id="d213c-119">Access control</span></span>

<span data-ttu-id="d213c-120">Se você não estiver Olá administrador/proprietário da assinatura do Azure, sua conta deve ter pelo menos **Colaborador** grupo de recursos do acesso toohello que contém o cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="d213c-120">If you are not hello administrator/owner of your Azure subscription, your account must have at least **Contributor** access toohello resource group that contains hello HDInsight cluster.</span></span>

<span data-ttu-id="d213c-121">Além disso, se você estiver criando um cluster HDInsight, alguém com pelo menos **Colaborador** acesso toohello assinatura do Azure deve ter registrado anteriormente provedor Olá para HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d213c-121">Additionally, if you are creating an HDInsight cluster, someone with at least **Contributor** access toohello Azure subscription must have previously registered hello provider for HDInsight.</span></span> <span data-ttu-id="d213c-122">Registro de provedor ocorre quando um usuário com a assinatura do Colaborador acesso toohello cria um recurso de saudação primeira vez na assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="d213c-122">Provider registration happens when a user with Contributor access toohello subscription creates a resource for hello first time on hello subscription.</span></span> <span data-ttu-id="d213c-123">Isso também pode ser feito sem criar um recurso, [registrando um provedor com o uso de REST](https://msdn.microsoft.com/library/azure/dn790548.aspx).</span><span class="sxs-lookup"><span data-stu-id="d213c-123">It can also be accomplished without creating a resource by [registering a provider using REST](https://msdn.microsoft.com/library/azure/dn790548.aspx).</span></span>

<span data-ttu-id="d213c-124">Para obter mais informações sobre como trabalhar com o gerenciamento de acesso, consulte Olá documentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="d213c-124">For more information on working with access management, see hello following documents:</span></span>

* [<span data-ttu-id="d213c-125">Introdução ao gerenciamento de acesso no hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d213c-125">Get started with access management in hello Azure portal</span></span>](../active-directory/role-based-access-control-what-is.md)
* [<span data-ttu-id="d213c-126">Usar os recursos de assinatura do Azure função atribuições toomanage acesso tooyour</span><span class="sxs-lookup"><span data-stu-id="d213c-126">Use role assignments toomanage access tooyour Azure subscription resources</span></span>](../active-directory/role-based-access-control-configure.md)

## <a name="understanding-script-actions"></a><span data-ttu-id="d213c-127">Noções básicas sobre Ações de Script</span><span class="sxs-lookup"><span data-stu-id="d213c-127">Understanding Script Actions</span></span>

<span data-ttu-id="d213c-128">Uma Ação de Script é simplesmente um script Bash para o qual você fornecer um URI e parâmetros.</span><span class="sxs-lookup"><span data-stu-id="d213c-128">A Script Action is simply a Bash script that you provide a URI to, and parameters for.</span></span> <span data-ttu-id="d213c-129">script de saudação é executado em nós de cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="d213c-129">hello script runs on nodes in hello HDInsight cluster.</span></span> <span data-ttu-id="d213c-130">Olá seguem características e recursos de ações de script.</span><span class="sxs-lookup"><span data-stu-id="d213c-130">hello following are characteristics and features of script actions.</span></span>

* <span data-ttu-id="d213c-131">Deve ser armazenado em um URI que é acessível pelo cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="d213c-131">Must be stored on a URI that is accessible from hello HDInsight cluster.</span></span> <span data-ttu-id="d213c-132">Olá seguem possíveis locais de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="d213c-132">hello following are possible storage locations:</span></span>

    * <span data-ttu-id="d213c-133">Um **repositório Azure Data Lake** conta que seja acessível pelo cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="d213c-133">An **Azure Data Lake Store** account that is accessible by hello HDInsight cluster.</span></span> <span data-ttu-id="d213c-134">Para obter mais informações sobre o uso do Azure Data Lake Store com o HDInsight, veja [Criar um cluster HDInsight com o Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d213c-134">For information on using Azure Data Lake Store with HDInsight, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

        <span data-ttu-id="d213c-135">Ao usar um script armazenado no repositório Data Lake, formato URI de saudação é `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.</span><span class="sxs-lookup"><span data-stu-id="d213c-135">When using a script stored in Data Lake Store, hello URI format is `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.</span></span>

        > [!NOTE]
        > <span data-ttu-id="d213c-136">Olá serviço principal HDInsight usa tooaccess repositório Data Lake deve ter acesso de leitura toohello script.</span><span class="sxs-lookup"><span data-stu-id="d213c-136">hello service principal HDInsight uses tooaccess Data Lake Store must have read access toohello script.</span></span>

    * <span data-ttu-id="d213c-137">Um blob em um **conta de armazenamento do Azure** é qualquer uma das contas de armazenamento principal ou adicionais Olá para o cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="d213c-137">A blob in an **Azure Storage account** that is either hello primary or additional storage account for hello HDInsight cluster.</span></span> <span data-ttu-id="d213c-138">HDInsight é concedido acesso tooboth desses tipos de contas de armazenamento durante a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="d213c-138">HDInsight is granted access tooboth of these types of storage accounts during cluster creation.</span></span>

    * <span data-ttu-id="d213c-139">Um serviço de compartilhamento de arquivos público como o Blob do Azure, o GitHub, o OneDrive, o Dropbox, etc.</span><span class="sxs-lookup"><span data-stu-id="d213c-139">A public file sharing service such as Azure Blob, GitHub, OneDrive, Dropbox, etc.</span></span>

        <span data-ttu-id="d213c-140">Por exemplo, URIs, consulte Olá [scripts de ação de script de exemplo](#example-script-action-scripts) seção.</span><span class="sxs-lookup"><span data-stu-id="d213c-140">For example URIs, see hello [Example script action scripts](#example-script-action-scripts) section.</span></span>

        > [!WARNING]
        > <span data-ttu-id="d213c-141">O HDInsight suporta apenas contas do Azure Storage de __Uso geral__.</span><span class="sxs-lookup"><span data-stu-id="d213c-141">HDInsight only supports __General-purpose__ Azure Storage accounts.</span></span> <span data-ttu-id="d213c-142">Ele não oferece suporte a saudação __armazenamento de Blob__ tipo de conta.</span><span class="sxs-lookup"><span data-stu-id="d213c-142">It does not currently support hello __Blob storage__ account type.</span></span>

* <span data-ttu-id="d213c-143">Pode ser restringido muito**executado em apenas alguns tipos de nó**, para nós de cabeçalho de exemplo ou nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="d213c-143">Can be restricted too**run on only certain node types**, for example head nodes or worker nodes.</span></span>

  > [!NOTE]
  > <span data-ttu-id="d213c-144">Quando usado com o HDInsight Premium, você pode especificar que o script hello deve ser usado no nó de borda hello.</span><span class="sxs-lookup"><span data-stu-id="d213c-144">When used with HDInsight Premium, you can specify that hello script should be used on hello edge node.</span></span>

* <span data-ttu-id="d213c-145">Pode ser **persistente** ou **ad hoc**.</span><span class="sxs-lookup"><span data-stu-id="d213c-145">Can be **persisted** or **ad hoc**.</span></span>

    <span data-ttu-id="d213c-146">**Persistente** scripts são cluster de toohello adicionado nós tooworker aplicado após a execução do script hello.</span><span class="sxs-lookup"><span data-stu-id="d213c-146">**Persisted** scripts are applied tooworker nodes added toohello cluster after hello script runs.</span></span> <span data-ttu-id="d213c-147">Por exemplo, ao dimensionar o cluster hello.</span><span class="sxs-lookup"><span data-stu-id="d213c-147">For example, when scaling up hello cluster.</span></span>

    <span data-ttu-id="d213c-148">Um script persistido também pode ser aplicadas alterações o tipo de nó tooanother, como um nó principal.</span><span class="sxs-lookup"><span data-stu-id="d213c-148">A persisted script might also apply changes tooanother node type, such as a head node.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="d213c-149">As ações de script persistentes devem ter um nome exclusivo.</span><span class="sxs-lookup"><span data-stu-id="d213c-149">Persisted script actions must have a unique name.</span></span>

    <span data-ttu-id="d213c-150">Scripts **Ad hoc** não são persistentes.</span><span class="sxs-lookup"><span data-stu-id="d213c-150">**Ad hoc** scripts are not persisted.</span></span> <span data-ttu-id="d213c-151">Eles não são cluster de toohello adicionado nós tooworker aplicado após a execução da script hello.</span><span class="sxs-lookup"><span data-stu-id="d213c-151">They are not applied tooworker nodes added toohello cluster after hello script has ran.</span></span> <span data-ttu-id="d213c-152">Posteriormente, você pode promover um tooa do script ad-hoc persistentes script ou rebaixar um script ad hoc de tooan script persistentes.</span><span class="sxs-lookup"><span data-stu-id="d213c-152">You can subsequently promote an ad hoc script tooa persisted script, or demote a persisted script tooan ad hoc script.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="d213c-153">As ações de script usadas durante a criação do cluster são mantidas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="d213c-153">Script actions used during cluster creation are automatically persisted.</span></span>
  >
  > <span data-ttu-id="d213c-154">Os scripts que falham não são persistentes, mesmo que você indique especificamente que eles devem ser.</span><span class="sxs-lookup"><span data-stu-id="d213c-154">Scripts that fail are not persisted, even if you specifically indicate that they should be.</span></span>

* <span data-ttu-id="d213c-155">Pode aceitar **parâmetros** que são usados pelo script hello durante a execução.</span><span class="sxs-lookup"><span data-stu-id="d213c-155">Can accept **parameters** that are used by hello script during execution.</span></span>
* <span data-ttu-id="d213c-156">Executar com **privilégios em nível de raiz** em nós de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="d213c-156">Run with **root level privileges** on hello cluster nodes.</span></span>
* <span data-ttu-id="d213c-157">Pode ser usada por meio de saudação **portal do Azure**, **Azure PowerShell**, **CLI do Azure**, ou **HDInsight .NET SDK**</span><span class="sxs-lookup"><span data-stu-id="d213c-157">Can be used through hello **Azure portal**, **Azure PowerShell**, **Azure CLI**, or **HDInsight .NET SDK**</span></span>

<span data-ttu-id="d213c-158">cluster Olá mantém um histórico de todos os scripts que tenha sido executado.</span><span class="sxs-lookup"><span data-stu-id="d213c-158">hello cluster keeps a history of all scripts that have been ran.</span></span> <span data-ttu-id="d213c-159">histórico de saudação é útil quando você precisa toofind Olá ID de um script para operações de promoção ou rebaixamento.</span><span class="sxs-lookup"><span data-stu-id="d213c-159">hello history is useful when you need toofind hello ID of a script for promotion or demotion operations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d213c-160">Não há nenhuma forma automática tooundo Olá alterações feitas por uma ação de script.</span><span class="sxs-lookup"><span data-stu-id="d213c-160">There is no automatic way tooundo hello changes made by a script action.</span></span> <span data-ttu-id="d213c-161">Ou manualmente, reverter alterações de saudação ou fornecer um script que reverte-los.</span><span class="sxs-lookup"><span data-stu-id="d213c-161">Either manually reverse hello changes or provide a script that reverses them.</span></span>


### <a name="script-action-in-hello-cluster-creation-process"></a><span data-ttu-id="d213c-162">Ação de script no processo de criação de cluster Olá</span><span class="sxs-lookup"><span data-stu-id="d213c-162">Script Action in hello cluster creation process</span></span>

<span data-ttu-id="d213c-163">As ações de script usadas durante a criação do cluster são ligeiramente diferentes das ações de script executadas em um cluster existente:</span><span class="sxs-lookup"><span data-stu-id="d213c-163">Script Actions used during cluster creation are slightly different from script actions ran on an existing cluster:</span></span>

* <span data-ttu-id="d213c-164">script Hello é **automaticamente persistente**.</span><span class="sxs-lookup"><span data-stu-id="d213c-164">hello script is **automatically persisted**.</span></span>
* <span data-ttu-id="d213c-165">Um **falha** em Olá script pode causar Olá toofail de processo de criação de cluster.</span><span class="sxs-lookup"><span data-stu-id="d213c-165">A **failure** in hello script can cause hello cluster creation process toofail.</span></span>

<span data-ttu-id="d213c-166">Olá seguinte diagrama ilustra quando a ação de Script é executada durante o processo de criação de saudação:</span><span class="sxs-lookup"><span data-stu-id="d213c-166">hello following diagram illustrates when Script Action is executed during hello creation process:</span></span>

<span data-ttu-id="d213c-167">![Personalização do cluster HDInsight e estágios durante a criação de cluster][img-hdi-cluster-states]</span><span class="sxs-lookup"><span data-stu-id="d213c-167">![HDInsight cluster customization and stages during cluster creation][img-hdi-cluster-states]</span></span>

<span data-ttu-id="d213c-168">script Hello executa enquanto o HDInsight está sendo configurado.</span><span class="sxs-lookup"><span data-stu-id="d213c-168">hello script runs while HDInsight is being configured.</span></span> <span data-ttu-id="d213c-169">Neste estágio, Olá script será executado em paralelo em todos os Olá nós especificados no cluster hello e é executado com privilégios de raiz em nós de saudação.</span><span class="sxs-lookup"><span data-stu-id="d213c-169">At this stage, hello script runs in parallel on all hello specified nodes in hello cluster, and runs with root privileges on hello nodes.</span></span>

> [!NOTE]
> <span data-ttu-id="d213c-170">Porque o script hello é executado com privilégios de nível raiz em nós de cluster hello, você pode executar operações como parar e iniciar serviços, incluindo serviços relacionados ao Hadoop.</span><span class="sxs-lookup"><span data-stu-id="d213c-170">Because hello script runs with root level privilege on hello cluster nodes, you can perform operations like stopping and starting services, including Hadoop-related services.</span></span> <span data-ttu-id="d213c-171">Se você parar serviços, certifique-se de que serviço do Ambari hello e outros serviços relacionados ao Hadoop estão funcionando antes que o script hello terminar a execução.</span><span class="sxs-lookup"><span data-stu-id="d213c-171">If you stop services, you must ensure that hello Ambari service and other Hadoop-related services are up and running before hello script finishes running.</span></span> <span data-ttu-id="d213c-172">Esses serviços são necessários toosuccessfully determinar Olá integridade e o estado do cluster Olá enquanto ele está sendo criado.</span><span class="sxs-lookup"><span data-stu-id="d213c-172">These services are required toosuccessfully determine hello health and state of hello cluster while it is being created.</span></span>


<span data-ttu-id="d213c-173">Durante a criação do cluster, você pode usar várias ações de script simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="d213c-173">During cluster creation, you can use multiple script actions at once.</span></span> <span data-ttu-id="d213c-174">Esses scripts são invocados em ordem de saudação na qual eles foram especificados.</span><span class="sxs-lookup"><span data-stu-id="d213c-174">These scripts are invoked in hello order in which they were specified.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d213c-175">Ações de script devem ser concluídas em 60 minutos ou atingirão o tempo limite.</span><span class="sxs-lookup"><span data-stu-id="d213c-175">Script actions must complete within 60 minutes, or timeout.</span></span> <span data-ttu-id="d213c-176">Durante o provisionamento de cluster, o script hello é executado simultaneamente com outros processos de instalação e configuração.</span><span class="sxs-lookup"><span data-stu-id="d213c-176">During cluster provisioning, hello script runs concurrently with other setup and configuration processes.</span></span> <span data-ttu-id="d213c-177">Competição por recursos, como largura de banda rede ou tempo de CPU pode provocar Olá script tootake mais toofinish do que no ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="d213c-177">Competition for resources such as CPU time or network bandwidth may cause hello script tootake longer toofinish than it does in your development environment.</span></span>
>
> <span data-ttu-id="d213c-178">Olá toominimize tempo que demora toorun Olá script, evite tarefas como baixar e compilar aplicativos de origem.</span><span class="sxs-lookup"><span data-stu-id="d213c-178">toominimize hello time it takes toorun hello script, avoid tasks such as downloading and compiling applications from source.</span></span> <span data-ttu-id="d213c-179">Pré-compile aplicativos e armazenar binário Olá no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="d213c-179">Pre-compile applications and store hello binary in Azure Storage.</span></span>


### <a name="script-action-on-a-running-cluster"></a><span data-ttu-id="d213c-180">Ação de script em um cluster em execução</span><span class="sxs-lookup"><span data-stu-id="d213c-180">Script action on a running cluster</span></span>

<span data-ttu-id="d213c-181">Ao contrário de ações usadas durante a criação do cluster, uma falha em um script foi executadas em um cluster já em execução do script não automaticamente causa Olá cluster toochange tooa falhado estado.</span><span class="sxs-lookup"><span data-stu-id="d213c-181">Unlike script actions used during cluster creation, a failure in a script ran on an already running cluster does not automatically cause hello cluster toochange tooa failed state.</span></span> <span data-ttu-id="d213c-182">Após a conclusão de um script, o cluster Olá deve retornar tooa estado "em execução".</span><span class="sxs-lookup"><span data-stu-id="d213c-182">Once a script completes, hello cluster should return tooa "running" state.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d213c-183">Mesmo que o cluster de saudação tem um estado 'em execução', hello script com falha pode desfeito coisas.</span><span class="sxs-lookup"><span data-stu-id="d213c-183">Even if hello cluster has a 'running' state, hello failed script may have broken things.</span></span> <span data-ttu-id="d213c-184">Por exemplo, um script pode excluir arquivos necessários ao cluster hello.</span><span class="sxs-lookup"><span data-stu-id="d213c-184">For example, a script could delete files needed by hello cluster.</span></span>
>
> <span data-ttu-id="d213c-185">Ações de scripts executados com privilégios de raiz, portanto, assegure-se de que você entenda o que faz um script antes de aplicá-la tooyour cluster.</span><span class="sxs-lookup"><span data-stu-id="d213c-185">Scripts actions run with root privileges, so you should make sure that you understand what a script does before applying it tooyour cluster.</span></span>

<span data-ttu-id="d213c-186">Ao aplicar um cluster de tooa do script, estado do cluster Olá altera toofrom **executando** muito**aceito**, em seguida, **configuração do HDInsight**e finalmente fazer muito**Executando** para scripts com êxito.</span><span class="sxs-lookup"><span data-stu-id="d213c-186">When applying a script tooa cluster, hello cluster state changes toofrom **Running** too**Accepted**, then **HDInsight configuration**, and finally back too**Running** for successful scripts.</span></span> <span data-ttu-id="d213c-187">status do script Hello é registrado no histórico de ação de script hello, e você pode usar este toodetermine informações se o script hello teve êxito ou falhou.</span><span class="sxs-lookup"><span data-stu-id="d213c-187">hello script status is logged in hello script action history, and you can use this information toodetermine whether hello script succeeded or failed.</span></span> <span data-ttu-id="d213c-188">Por exemplo, Olá `Get-AzureRmHDInsightScriptActionHistory` cmdlet do PowerShell pode ser usado tooview Olá status de um script.</span><span class="sxs-lookup"><span data-stu-id="d213c-188">For example, hello `Get-AzureRmHDInsightScriptActionHistory` PowerShell cmdlet can be used tooview hello status of a script.</span></span> <span data-ttu-id="d213c-189">Ele retorna informações toohello semelhante texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="d213c-189">It returns information similar toohello following text:</span></span>

    ScriptExecutionId : 635918532516474303
    StartTime         : 8/14/2017 7:40:55 PM
    EndTime           : 8/14/2017 7:41:05 PM
    Status            : Succeeded

> [!NOTE]
> <span data-ttu-id="d213c-190">Se você alterou a senha de usuário (admin) do cluster Olá depois Olá cluster foi criado, script ações executadas em relação a esse cluster poderá falhar.</span><span class="sxs-lookup"><span data-stu-id="d213c-190">If you have changed hello cluster user (admin) password after hello cluster was created, script actions ran against this cluster may fail.</span></span> <span data-ttu-id="d213c-191">Se você tiver quaisquer ações de script persistentes que nós de trabalho de destino, esses scripts podem falhar quando você dimensionar o cluster hello.</span><span class="sxs-lookup"><span data-stu-id="d213c-191">If you have any persisted script actions that target worker nodes, these scripts may fail when you scale hello cluster.</span></span>

## <a name="example-script-action-scripts"></a><span data-ttu-id="d213c-192">Scripts de exemplo de Ação de Script</span><span class="sxs-lookup"><span data-stu-id="d213c-192">Example Script Action scripts</span></span>

<span data-ttu-id="d213c-193">Scripts de ação de script podem ser usados por meio de saudação utilitários a seguir:</span><span class="sxs-lookup"><span data-stu-id="d213c-193">Script Action scripts can be used through hello following utilities:</span></span>

* <span data-ttu-id="d213c-194">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d213c-194">Azure portal</span></span>
* <span data-ttu-id="d213c-195">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d213c-195">Azure PowerShell</span></span>
* <span data-ttu-id="d213c-196">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="d213c-196">Azure CLI</span></span>
* <span data-ttu-id="d213c-197">SDK do .NET do HDInsight</span><span class="sxs-lookup"><span data-stu-id="d213c-197">HDInsight .NET SDK</span></span>

<span data-ttu-id="d213c-198">HDInsight fornece Olá tooinstall de scripts a seguir de componentes em clusters de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="d213c-198">HDInsight provides scripts tooinstall hello following components on HDInsight clusters:</span></span>

| <span data-ttu-id="d213c-199">Nome</span><span class="sxs-lookup"><span data-stu-id="d213c-199">Name</span></span> | <span data-ttu-id="d213c-200">Script</span><span class="sxs-lookup"><span data-stu-id="d213c-200">Script</span></span> |
| --- | --- |
| <span data-ttu-id="d213c-201">**Adicionar uma conta de armazenamento do Azure**</span><span class="sxs-lookup"><span data-stu-id="d213c-201">**Add an Azure Storage account**</span></span> |<span data-ttu-id="d213c-202">https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh. Consulte [cluster do HDInsight adicionar armazenamento adicional tooan](hdinsight-hadoop-add-storage.md).</span><span class="sxs-lookup"><span data-stu-id="d213c-202">https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh. See [Add additional storage tooan HDInsight cluster](hdinsight-hadoop-add-storage.md).</span></span> |
| <span data-ttu-id="d213c-203">**Instalar o Hue**</span><span class="sxs-lookup"><span data-stu-id="d213c-203">**Install Hue**</span></span> |<span data-ttu-id="d213c-204">https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. Veja [Instalar e usar o Hue em clusters HDInsight](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="d213c-204">https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. See [Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> |
| <span data-ttu-id="d213c-205">**Instalar o Presto**</span><span class="sxs-lookup"><span data-stu-id="d213c-205">**Install Presto**</span></span> |<span data-ttu-id="d213c-206">https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh. Veja [Instalar e usar o Presto em clusters HDInsight](hdinsight-hadoop-install-presto.md).</span><span class="sxs-lookup"><span data-stu-id="d213c-206">https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh. See [Install and use Presto on HDInsight clusters](hdinsight-hadoop-install-presto.md).</span></span> |
| <span data-ttu-id="d213c-207">**Instalar Solr**</span><span class="sxs-lookup"><span data-stu-id="d213c-207">**Install Solr**</span></span> |<span data-ttu-id="d213c-208">https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh. Consulte [Instalar e usar o Solr em clusters HDInsight](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="d213c-208">https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh. See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span> |
| <span data-ttu-id="d213c-209">**Instalar o Giraph**</span><span class="sxs-lookup"><span data-stu-id="d213c-209">**Install Giraph**</span></span> |<span data-ttu-id="d213c-210">https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh. Consulte [Instalar e usar o Giraph em clusters HDInsight](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="d213c-210">https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh. See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> |
| <span data-ttu-id="d213c-211">**Pré-carregar bibliotecas Hive**</span><span class="sxs-lookup"><span data-stu-id="d213c-211">**Pre-load Hive libraries**</span></span> |<span data-ttu-id="d213c-212">https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh. Veja [Adicionar bibliotecas do Hive em clusters HDInsight](hdinsight-hadoop-add-hive-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="d213c-212">https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh. See [Add Hive libraries on HDInsight clusters](hdinsight-hadoop-add-hive-libraries.md).</span></span> |
| <span data-ttu-id="d213c-213">**Instalar ou atualizar Mono**</span><span class="sxs-lookup"><span data-stu-id="d213c-213">**Install or update Mono**</span></span> | <span data-ttu-id="d213c-214">https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash.</span><span class="sxs-lookup"><span data-stu-id="d213c-214">https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash.</span></span> <span data-ttu-id="d213c-215">Veja [Instalar ou atualizar o Mono no HDInsight](hdinsight-hadoop-install-mono.md).</span><span class="sxs-lookup"><span data-stu-id="d213c-215">See [Install or update Mono on HDInsight](hdinsight-hadoop-install-mono.md).</span></span> |

## <a name="use-a-script-action-during-cluster-creation"></a><span data-ttu-id="d213c-216">Usar uma Ação de Script durante a criação do cluster</span><span class="sxs-lookup"><span data-stu-id="d213c-216">Use a Script Action during cluster creation</span></span>

<span data-ttu-id="d213c-217">Esta seção fornece exemplos sobre maneiras diferentes hello, que você pode usar ações de script ao criar um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d213c-217">This section provides examples on hello different ways you can use script actions when creating an HDInsight cluster.</span></span>

### <a name="use-a-script-action-during-cluster-creation-from-hello-azure-portal"></a><span data-ttu-id="d213c-218">Usar uma ação de Script durante a criação do cluster de saudação portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d213c-218">Use a Script Action during cluster creation from hello Azure portal</span></span>

1. <span data-ttu-id="d213c-219">Comece criando um cluster como descrito em [Criar clusters Hadoop no HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="d213c-219">Start creating a cluster as described at [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="d213c-220">Pare quando chegar Olá __resumo do Cluster__ seção.</span><span class="sxs-lookup"><span data-stu-id="d213c-220">Stop when you reach hello __Cluster summary__ section.</span></span>

2. <span data-ttu-id="d213c-221">De saudação __resumo do Cluster__ seção, selecione Olá __editar__ link para __configurações avançadas__.</span><span class="sxs-lookup"><span data-stu-id="d213c-221">From hello __Cluster summary__ section, select hello __edit__ link for __Advanced settings__.</span></span>

    ![Link Configurações avançadas](./media/hdinsight-hadoop-customize-cluster-linux/advanced-settings-link.png)

3. <span data-ttu-id="d213c-223">De saudação __configurações avançadas__ seção, selecione __ações de Script__.</span><span class="sxs-lookup"><span data-stu-id="d213c-223">From hello __Advanced settings__ section, select __Script actions__.</span></span> <span data-ttu-id="d213c-224">De saudação __ações de Script__ seção, selecione __+ novo envio__</span><span class="sxs-lookup"><span data-stu-id="d213c-224">From hello __Script actions__ section, select __+ Submit new__</span></span>

    ![Enviar uma nova ação de script](./media/hdinsight-hadoop-customize-cluster-linux/add-script-action.png)

4. <span data-ttu-id="d213c-226">Saudação de uso __selecionar um script__ entrada tooselect um script predefinido.</span><span class="sxs-lookup"><span data-stu-id="d213c-226">Use hello __Select a script__ entry tooselect a pre-made script.</span></span> <span data-ttu-id="d213c-227">toouse um script personalizado, selecione __personalizado__ e, em seguida, fornecer Olá __nome__ e __Bash script URI__ para o seu script.</span><span class="sxs-lookup"><span data-stu-id="d213c-227">toouse a custom script, select __Custom__ and then provide hello __Name__ and __Bash script URI__ for your script.</span></span>

    ![Adicionar um script na forma de selecione script hello](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    <span data-ttu-id="d213c-229">Olá a tabela a seguir descreve elementos Olá Olá formulário:</span><span class="sxs-lookup"><span data-stu-id="d213c-229">hello following table describes hello elements on hello form:</span></span>

    | <span data-ttu-id="d213c-230">Propriedade</span><span class="sxs-lookup"><span data-stu-id="d213c-230">Property</span></span> | <span data-ttu-id="d213c-231">Valor</span><span class="sxs-lookup"><span data-stu-id="d213c-231">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="d213c-232">Selecionar um script</span><span class="sxs-lookup"><span data-stu-id="d213c-232">Select a script</span></span> | <span data-ttu-id="d213c-233">toouse seu próprio script, selecione __personalizado__.</span><span class="sxs-lookup"><span data-stu-id="d213c-233">toouse your own script, select __Custom__.</span></span> <span data-ttu-id="d213c-234">Caso contrário, selecione um dos scripts de saudação fornecida.</span><span class="sxs-lookup"><span data-stu-id="d213c-234">Otherwise, select one of hello provided scripts.</span></span> |
    | <span data-ttu-id="d213c-235">Nome</span><span class="sxs-lookup"><span data-stu-id="d213c-235">Name</span></span> |<span data-ttu-id="d213c-236">Especifique um nome para a ação de script hello.</span><span class="sxs-lookup"><span data-stu-id="d213c-236">Specify a name for hello script action.</span></span> |
    | <span data-ttu-id="d213c-237">URI do script Bash</span><span class="sxs-lookup"><span data-stu-id="d213c-237">Bash script URI</span></span> |<span data-ttu-id="d213c-238">Especifique Olá URI toohello script que é invocado toocustomize Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="d213c-238">Specify hello URI toohello script that is invoked toocustomize hello cluster.</span></span> |
    | <span data-ttu-id="d213c-239">Cabeçalho/Trabalho/Zookeeper</span><span class="sxs-lookup"><span data-stu-id="d213c-239">Head/Worker/Zookeeper</span></span> |<span data-ttu-id="d213c-240">Especificar nós de saudação (**Head**, **trabalho**, ou **ZooKeeper**) no qual personalização Olá script é executado.</span><span class="sxs-lookup"><span data-stu-id="d213c-240">Specify hello nodes (**Head**, **Worker**, or **ZooKeeper**) on which hello customization script is run.</span></span> |
    | <span data-ttu-id="d213c-241">parâmetros</span><span class="sxs-lookup"><span data-stu-id="d213c-241">Parameters</span></span> |<span data-ttu-id="d213c-242">Especifica parâmetros de hello, se exigido pelo script hello.</span><span class="sxs-lookup"><span data-stu-id="d213c-242">Specify hello parameters, if required by hello script.</span></span> |

    <span data-ttu-id="d213c-243">Saudação de uso __manter essa ação de script__ tooensure de entrada que Olá script é aplicada durante operações de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="d213c-243">Use hello __Persist this script action__ entry tooensure that hello script is applied during scaling operations.</span></span>

5. <span data-ttu-id="d213c-244">Selecione __criar__ toosave script de saudação.</span><span class="sxs-lookup"><span data-stu-id="d213c-244">Select __Create__ toosave hello script.</span></span> <span data-ttu-id="d213c-245">Você pode usar __+ Enviar nova__ tooadd outro script.</span><span class="sxs-lookup"><span data-stu-id="d213c-245">You can then use __+ Submit new__ tooadd another script.</span></span>

    ![Várias ações de script](./media/hdinsight-hadoop-customize-cluster-linux/multiple-scripts.png)

    <span data-ttu-id="d213c-247">Quando você terminar de adicionar scripts, use Olá __selecione__ botão e, em seguida, Olá __próximo__ botão tooreturn toohello __resumo do Cluster__ seção.</span><span class="sxs-lookup"><span data-stu-id="d213c-247">When you are done adding scripts, use hello __Select__ button, and then hello __Next__ button tooreturn toohello __Cluster summary__ section.</span></span>

3. <span data-ttu-id="d213c-248">cluster de saudação toocreate, selecione __criar__ de saudação __resumo do Cluster__ seleção.</span><span class="sxs-lookup"><span data-stu-id="d213c-248">toocreate hello cluster, select __Create__ from hello __Cluster summary__ selection.</span></span>

### <a name="use-a-script-action-from-azure-resource-manager-templates"></a><span data-ttu-id="d213c-249">Usar uma Ação de Script em modelos do Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="d213c-249">Use a Script Action from Azure Resource Manager templates</span></span>

<span data-ttu-id="d213c-250">Olá exemplos nesta seção demonstram como toouse scripts ações com modelos do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="d213c-250">hello examples in this section demonstrate how toouse script actions with Azure Resource Manager templates.</span></span>

#### <a name="before-you-begin"></a><span data-ttu-id="d213c-251">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="d213c-251">Before you begin</span></span>

* <span data-ttu-id="d213c-252">Para obter informações sobre como configurar uma estação de trabalho toorun HDInsight Powershell cmdlets, consulte [instalar e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d213c-252">For information about configuring a workstation toorun HDInsight Powershell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="d213c-253">Para obter instruções sobre como toocreate modelos, consulte [modelos de autoria do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="d213c-253">For instructions on how toocreate templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="d213c-254">Se você ainda não utilizou o PowerShell do Azure com o Gerenciador de recursos, consulte [Uso do PowerShell do Azure com o Gerenciador de recursos do Azure](../azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="d213c-254">If you have not previously used Azure PowerShell with Resource Manager, see [Using Azure PowerShell with Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

#### <a name="create-clusters-using-script-action"></a><span data-ttu-id="d213c-255">Criar clusters usando a Ação de Script</span><span class="sxs-lookup"><span data-stu-id="d213c-255">Create clusters using Script Action</span></span>

1. <span data-ttu-id="d213c-256">Saudação de cópia local do modelo tooa a seguir em seu computador.</span><span class="sxs-lookup"><span data-stu-id="d213c-256">Copy hello following template tooa location on your computer.</span></span> <span data-ttu-id="d213c-257">Este modelo instala Giraph em nós headnodes e de trabalho Olá Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="d213c-257">This template installs Giraph on hello headnodes and worker nodes in hello cluster.</span></span> <span data-ttu-id="d213c-258">Você também pode verificar se o modelo JSON Olá é válido.</span><span class="sxs-lookup"><span data-stu-id="d213c-258">You can also verify if hello JSON template is valid.</span></span> <span data-ttu-id="d213c-259">Cole o conteúdo do modelo no [JSONLint](http://jsonlint.com/), uma ferramenta online para validação de JSON.</span><span class="sxs-lookup"><span data-stu-id="d213c-259">Paste your template content into [JSONLint](http://jsonlint.com/), an online JSON validation tool.</span></span>

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
2. <span data-ttu-id="d213c-260">Inicie o PowerShell do Azure e faça logon tooyour conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="d213c-260">Start Azure PowerShell and Log in tooyour Azure account.</span></span> <span data-ttu-id="d213c-261">Depois de fornecer suas credenciais, o comando Olá retorna informações sobre sua conta.</span><span class="sxs-lookup"><span data-stu-id="d213c-261">After providing your credentials, hello command returns information about your account.</span></span>

        Add-AzureRmAccount

        Id                             Type       ...
        --                             ----
        someone@example.com            User       ...
3. <span data-ttu-id="d213c-262">Se você tiver várias assinaturas, forneça a ID da assinatura Olá desejar toouse para implantação.</span><span class="sxs-lookup"><span data-stu-id="d213c-262">If you have multiple subscriptions, provide hello subscription ID you wish toouse for deployment.</span></span>

        Select-AzureRmSubscription -SubscriptionID <YourSubscriptionId>

    > [!NOTE]
    > <span data-ttu-id="d213c-263">Você pode usar `Get-AzureRmSubscription` tooget uma lista de todas as assinaturas associadas à sua conta, o que inclui a saudação ID da assinatura para cada um.</span><span class="sxs-lookup"><span data-stu-id="d213c-263">You can use `Get-AzureRmSubscription` tooget a list of all subscriptions associated with your account, which includes hello subscription ID for each one.</span></span>

4. <span data-ttu-id="d213c-264">Se você não tiver um grupo de recursos existente, crie um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d213c-264">If you do not have an existing resource group, create a resource group.</span></span> <span data-ttu-id="d213c-265">Forneça o nome de saudação do grupo de recursos de saudação e local que você precisa para sua solução.</span><span class="sxs-lookup"><span data-stu-id="d213c-265">Provide hello name of hello resource group and location that you need for your solution.</span></span> <span data-ttu-id="d213c-266">Um resumo do novo grupo de recursos Olá é retornado.</span><span class="sxs-lookup"><span data-stu-id="d213c-266">A summary of hello new resource group is returned.</span></span>

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

5. <span data-ttu-id="d213c-267">toocreate uma implantação para seu grupo de recursos, execute Olá **AzureRmResourceGroupDeployment novo** de comando e forneça os parâmetros necessários hello.</span><span class="sxs-lookup"><span data-stu-id="d213c-267">toocreate a deployment for your resource group, run hello **New-AzureRmResourceGroupDeployment** command and provide hello necessary parameters.</span></span> <span data-ttu-id="d213c-268">os parâmetros de saudação incluem hello seguintes dados:</span><span class="sxs-lookup"><span data-stu-id="d213c-268">hello parameters include hello following data:</span></span>

    * <span data-ttu-id="d213c-269">Um nome para sua implantação</span><span class="sxs-lookup"><span data-stu-id="d213c-269">A name for your deployment</span></span>
    * <span data-ttu-id="d213c-270">nome de saudação do seu grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="d213c-270">hello name of your resource group</span></span>
    * <span data-ttu-id="d213c-271">caminho de saudação ou modelo toohello URL que você criou.</span><span class="sxs-lookup"><span data-stu-id="d213c-271">hello path or URL toohello template you created.</span></span>

  <span data-ttu-id="d213c-272">Se seu modelo exige quaisquer parâmetros, você deve passar esses parâmetros também.</span><span class="sxs-lookup"><span data-stu-id="d213c-272">If your template requires any parameters, you must pass those parameters as well.</span></span> <span data-ttu-id="d213c-273">Nesse caso, tooinstall de ação de script hello R no cluster Olá não requer parâmetros.</span><span class="sxs-lookup"><span data-stu-id="d213c-273">In this case, hello script action tooinstall R on hello cluster does not require any parameters.</span></span>

        New-AzureRmResourceGroupDeployment -Name mydeployment -ResourceGroupName myresourcegroup -TemplateFile <PathOrLinkToTemplate>

    <span data-ttu-id="d213c-274">Você é valores de tooprovide solicitadas para parâmetros de saudação definidos no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="d213c-274">You are prompted tooprovide values for hello parameters defined in hello template.</span></span>

1. <span data-ttu-id="d213c-275">Quando o grupo de recursos Olá tiver sido implantado, é exibido um resumo de implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="d213c-275">When hello resource group has been deployed, a summary of hello deployment is displayed.</span></span>

          DeploymentName    : mydeployment
          ResourceGroupName : myresourcegroup
          ProvisioningState : Succeeded
          Timestamp         : 8/14/2017 7:00:27 PM
          Mode              : Incremental
          ...

2. <span data-ttu-id="d213c-276">Se sua implantação falhar, você pode usar o hello cmdlets tooget informações sobre falhas de saudação a seguir.</span><span class="sxs-lookup"><span data-stu-id="d213c-276">If your deployment fails, you can use hello following cmdlets tooget information about hello failures.</span></span>

        Get-AzureRmResourceGroupDeployment -ResourceGroupName myresourcegroup -ProvisioningState Failed

### <a name="use-a-script-action-during-cluster-creation-from-azure-powershell"></a><span data-ttu-id="d213c-277">Usar uma Ação de Script durante a criação do cluster no Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d213c-277">Use a Script Action during cluster creation from Azure PowerShell</span></span>

<span data-ttu-id="d213c-278">Nesta seção, usamos Olá [AzureRmHDInsightScriptAction adicionar](https://msdn.microsoft.com/library/mt603527.aspx) cmdlet tooinvoke scripts usando a ação de Script toocustomize um cluster.</span><span class="sxs-lookup"><span data-stu-id="d213c-278">In this section, we use hello [Add-AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) cmdlet tooinvoke scripts by using Script Action toocustomize a cluster.</span></span> <span data-ttu-id="d213c-279">Antes de prosseguir, verifique se você instalou e configurou o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="d213c-279">Before proceeding, make sure you have installed and configured Azure PowerShell.</span></span> <span data-ttu-id="d213c-280">Para obter informações sobre como configurar uma estação de trabalho toorun HDInsight PowerShell cmdlets, consulte [instalar e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d213c-280">For information about configuring a workstation toorun HDInsight PowerShell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="d213c-281">Olá script a seguir demonstra como tooapply uma ação de script ao criar um cluster usando o PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d213c-281">hello following script demonstrates how tooapply a script action when creating a cluster using PowerShell:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=5-90)]

<span data-ttu-id="d213c-282">Pode levar vários minutos antes de saudação cluster é criado.</span><span class="sxs-lookup"><span data-stu-id="d213c-282">It can take several minutes before hello cluster is created.</span></span>

### <a name="use-a-script-action-during-cluster-creation-from-hello-hdinsight-net-sdk"></a><span data-ttu-id="d213c-283">Usar uma ação de Script durante a criação do cluster de saudação HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="d213c-283">Use a Script Action during cluster creation from hello HDInsight .NET SDK</span></span>

<span data-ttu-id="d213c-284">Olá HDInsight .NET SDK fornece bibliotecas de cliente que torna mais fácil toowork com HDInsight de um aplicativo .NET.</span><span class="sxs-lookup"><span data-stu-id="d213c-284">hello HDInsight .NET SDK provides client libraries that makes it easier toowork with HDInsight from a .NET application.</span></span> <span data-ttu-id="d213c-285">Para obter um exemplo de código, consulte [baseados em Linux criar clusters HDInsight usando Olá .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).</span><span class="sxs-lookup"><span data-stu-id="d213c-285">For a code sample, see [Create Linux-based clusters in HDInsight using hello .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).</span></span>

## <a name="apply-a-script-action-tooa-running-cluster"></a><span data-ttu-id="d213c-286">Aplicar um tooa de ação de Script executando cluster</span><span class="sxs-lookup"><span data-stu-id="d213c-286">Apply a Script Action tooa running cluster</span></span>

<span data-ttu-id="d213c-287">Nesta seção, Aprenda como tooapply script tooa ações executando o cluster.</span><span class="sxs-lookup"><span data-stu-id="d213c-287">In this section, learn how tooapply script actions tooa running cluster.</span></span>

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-azure-portal"></a><span data-ttu-id="d213c-288">Aplicar um tooa de ação de Script executando o cluster de saudação portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d213c-288">Apply a Script Action tooa running cluster from hello Azure portal</span></span>

1. <span data-ttu-id="d213c-289">De saudação [portal do Azure](https://portal.azure.com), selecione o cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d213c-289">From hello [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="d213c-290">Visão geral sobre cluster de HDInsight hello, selecione Olá **ações de Script** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="d213c-290">From hello HDInsight cluster overview, select hello **Script Actions** tile.</span></span>

    ![Bloco Ações de script](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > <span data-ttu-id="d213c-292">Você também pode selecionar **todas as configurações** e, em seguida, selecione **ações de Script** da seção configurações da saudação.</span><span class="sxs-lookup"><span data-stu-id="d213c-292">You can also select **All settings** and then select **Script Actions** from hello Settings section.</span></span>

3. <span data-ttu-id="d213c-293">Na parte superior de saudação da saudação seção ações de Script, selecione **enviar novo**.</span><span class="sxs-lookup"><span data-stu-id="d213c-293">From hello top of hello Script Actions section, select **Submit new**.</span></span>

    ![Adicionar um tooa de script executando cluster](./media/hdinsight-hadoop-customize-cluster-linux/add-script-running-cluster.png)

4. <span data-ttu-id="d213c-295">Saudação de uso __selecionar um script__ entrada tooselect um script predefinido.</span><span class="sxs-lookup"><span data-stu-id="d213c-295">Use hello __Select a script__ entry tooselect a pre-made script.</span></span> <span data-ttu-id="d213c-296">toouse um script personalizado, selecione __personalizado__ e, em seguida, fornecer Olá __nome__ e __Bash script URI__ para o seu script.</span><span class="sxs-lookup"><span data-stu-id="d213c-296">toouse a custom script, select __Custom__ and then provide hello __Name__ and __Bash script URI__ for your script.</span></span>

    ![Adicionar um script na forma de selecione script hello](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    <span data-ttu-id="d213c-298">Olá a tabela a seguir descreve elementos Olá Olá formulário:</span><span class="sxs-lookup"><span data-stu-id="d213c-298">hello following table describes hello elements on hello form:</span></span>

    | <span data-ttu-id="d213c-299">Propriedade</span><span class="sxs-lookup"><span data-stu-id="d213c-299">Property</span></span> | <span data-ttu-id="d213c-300">Valor</span><span class="sxs-lookup"><span data-stu-id="d213c-300">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="d213c-301">Selecionar um script</span><span class="sxs-lookup"><span data-stu-id="d213c-301">Select a script</span></span> | <span data-ttu-id="d213c-302">toouse seu próprio script, selecione __personalizado__.</span><span class="sxs-lookup"><span data-stu-id="d213c-302">toouse your own script, select __custom__.</span></span> <span data-ttu-id="d213c-303">Caso contrário, selecione um script fornecido.</span><span class="sxs-lookup"><span data-stu-id="d213c-303">Otherwise, select a provided script.</span></span> |
    | <span data-ttu-id="d213c-304">Nome</span><span class="sxs-lookup"><span data-stu-id="d213c-304">Name</span></span> |<span data-ttu-id="d213c-305">Especifique um nome para a ação de script hello.</span><span class="sxs-lookup"><span data-stu-id="d213c-305">Specify a name for hello script action.</span></span> |
    | <span data-ttu-id="d213c-306">URI do script Bash</span><span class="sxs-lookup"><span data-stu-id="d213c-306">Bash script URI</span></span> |<span data-ttu-id="d213c-307">Especifique Olá URI toohello script que é invocado toocustomize Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="d213c-307">Specify hello URI toohello script that is invoked toocustomize hello cluster.</span></span> |
    | <span data-ttu-id="d213c-308">Cabeçalho/Trabalho/Zookeeper</span><span class="sxs-lookup"><span data-stu-id="d213c-308">Head/Worker/Zookeeper</span></span> |<span data-ttu-id="d213c-309">Especificar nós de saudação (**Head**, **trabalho**, ou **ZooKeeper**) no qual personalização Olá script é executado.</span><span class="sxs-lookup"><span data-stu-id="d213c-309">Specify hello nodes (**Head**, **Worker**, or **ZooKeeper**) on which hello customization script is run.</span></span> |
    | <span data-ttu-id="d213c-310">parâmetros</span><span class="sxs-lookup"><span data-stu-id="d213c-310">Parameters</span></span> |<span data-ttu-id="d213c-311">Especifica parâmetros de hello, se exigido pelo script hello.</span><span class="sxs-lookup"><span data-stu-id="d213c-311">Specify hello parameters, if required by hello script.</span></span> |

    <span data-ttu-id="d213c-312">Saudação de uso __manter essa ação de script__ script de saudação entrada toomake-se de que é aplicada durante operações de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="d213c-312">Use hello __Persist this script action__ entry toomake sure hello script is applied during scaling operations.</span></span>

5. <span data-ttu-id="d213c-313">Por fim, use Olá **criar** cluster toohello do botão tooapply Olá script.</span><span class="sxs-lookup"><span data-stu-id="d213c-313">Finally, use hello **Create** button tooapply hello script toohello cluster.</span></span>

### <a name="apply-a-script-action-tooa-running-cluster-from-azure-powershell"></a><span data-ttu-id="d213c-314">Aplicar um tooa de ação de Script que executa o cluster do Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d213c-314">Apply a Script Action tooa running cluster from Azure PowerShell</span></span>

<span data-ttu-id="d213c-315">Antes de prosseguir, verifique se você instalou e configurou o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="d213c-315">Before proceeding, make sure you have installed and configured Azure PowerShell.</span></span> <span data-ttu-id="d213c-316">Para obter informações sobre como configurar uma estação de trabalho toorun HDInsight PowerShell cmdlets, consulte [instalar e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d213c-316">For information about configuring a workstation toorun HDInsight PowerShell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="d213c-317">Olá exemplo a seguir demonstra como tooapply um cluster em execução do script ação tooa:</span><span class="sxs-lookup"><span data-stu-id="d213c-317">hello following example demonstrates how tooapply a script action tooa running cluster:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=105-117)]

<span data-ttu-id="d213c-318">Após a conclusão da operação de saudação, você receberá informações toohello semelhante texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="d213c-318">Once hello operation completes, you receive information similar toohello following text:</span></span>

    OperationState  : Succeeded
    ErrorMessage    :
    Name            : Giraph
    Uri             : https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh
    Parameters      :
    NodeTypes       : {HeadNode, WorkerNode}

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-azure-cli"></a><span data-ttu-id="d213c-319">Aplicar um tooa de ação de Script executando o cluster de saudação CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="d213c-319">Apply a Script Action tooa running cluster from hello Azure CLI</span></span>

<span data-ttu-id="d213c-320">Antes de prosseguir, certifique-se de ter instalado e configurado Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="d213c-320">Before proceeding, make sure you have installed and configured hello Azure CLI.</span></span> <span data-ttu-id="d213c-321">Para obter mais informações, consulte [instalação Olá CLI do Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="d213c-321">For more information, see [Install hello Azure CLI](../cli-install-nodejs.md).</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. <span data-ttu-id="d213c-322">tooswitch tooAzure modo do Gerenciador de recursos, use Olá na linha de comando Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="d213c-322">tooswitch tooAzure Resource Manager mode, use hello following command at hello command line:</span></span>

        azure config mode arm

2. <span data-ttu-id="d213c-323">Use Olá tooauthenticate tooyour assinatura do Azure a seguir.</span><span class="sxs-lookup"><span data-stu-id="d213c-323">Use hello following tooauthenticate tooyour Azure subscription.</span></span>

        azure login

3. <span data-ttu-id="d213c-324">Use Olá tooapply de comando a seguir um tooa de ação de script executando cluster</span><span class="sxs-lookup"><span data-stu-id="d213c-324">Use hello following command tooapply a script action tooa running cluster</span></span>

        azure hdinsight script-action create <clustername> -g <resourcegroupname> -n <scriptname> -u <scriptURI> -t <nodetypes>

    <span data-ttu-id="d213c-325">Se você omitir parâmetros para esse comando, você será solicitado a fornecê-los.</span><span class="sxs-lookup"><span data-stu-id="d213c-325">If you omit parameters for this command, you are prompted for them.</span></span> <span data-ttu-id="d213c-326">Se Olá script que você especificar com `-u` aceita parâmetros, você pode especificá-los usando Olá `-p` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="d213c-326">If hello script you specify with `-u` accepts parameters, you can specify them using hello `-p` parameter.</span></span>

    <span data-ttu-id="d213c-327">Os tipos de nós válidos são `headnode`, `workernode` e `zookeeper`.</span><span class="sxs-lookup"><span data-stu-id="d213c-327">Valid node types are `headnode`, `workernode`, and `zookeeper`.</span></span> <span data-ttu-id="d213c-328">Se o script hello deve ser aplicada toomultiple tipos de nós, especificar os tipos de saudação separados por um ';'.</span><span class="sxs-lookup"><span data-stu-id="d213c-328">If hello script should be applied toomultiple node types, specify hello types separated by a ';'.</span></span> <span data-ttu-id="d213c-329">Por exemplo: `-n headnode;workernode`.</span><span class="sxs-lookup"><span data-stu-id="d213c-329">For example, `-n headnode;workernode`.</span></span>

    <span data-ttu-id="d213c-330">toopersist Olá script, adicione Olá `--persistOnSuccess`.</span><span class="sxs-lookup"><span data-stu-id="d213c-330">toopersist hello script, add hello `--persistOnSuccess`.</span></span> <span data-ttu-id="d213c-331">Você também pode persistir script hello mais tarde usando `azure hdinsight script-action persisted set`.</span><span class="sxs-lookup"><span data-stu-id="d213c-331">You can also persist hello script later by using `azure hdinsight script-action persisted set`.</span></span>

    <span data-ttu-id="d213c-332">Após a conclusão do trabalho hello, você recebe saída toohello semelhante texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="d213c-332">Once hello job completes, you receive output similar toohello following text:</span></span>

        info:    Executing command hdinsight script-action create
        + Executing Script Action on HDInsight cluster
        data:    Operation Info
        data:    ---------------
        data:    Operation status:
        data:    Operation ID:  b707b10e-e633-45c0-baa9-8aed3d348c13
        info:    hdinsight script-action create command OK

### <a name="apply-a-script-action-tooa-running-cluster-using-rest-api"></a><span data-ttu-id="d213c-333">Aplicar um tooa de ação do Script em execução usando a API REST do cluster</span><span class="sxs-lookup"><span data-stu-id="d213c-333">Apply a Script Action tooa running cluster using REST API</span></span>

<span data-ttu-id="d213c-334">Consulte [Executar Ações de Script em um cluster em execução](https://msdn.microsoft.com/library/azure/mt668441.aspx).</span><span class="sxs-lookup"><span data-stu-id="d213c-334">See [Run Script Actions on a running cluster](https://msdn.microsoft.com/library/azure/mt668441.aspx).</span></span>

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-hdinsight-net-sdk"></a><span data-ttu-id="d213c-335">Aplicar um tooa de ação de Script executando o cluster de saudação HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="d213c-335">Apply a Script Action tooa running cluster from hello HDInsight .NET SDK</span></span>

<span data-ttu-id="d213c-336">Para obter um exemplo do uso de cluster de tooa Olá .NET SDK tooapply scripts, consulte [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span><span class="sxs-lookup"><span data-stu-id="d213c-336">For an example of using hello .NET SDK tooapply scripts tooa cluster, see [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span></span>

## <a name="view-history-promote-and-demote-script-actions"></a><span data-ttu-id="d213c-337">Exibir o histórico, promover e rebaixar Ações de Script</span><span class="sxs-lookup"><span data-stu-id="d213c-337">View history, promote, and demote Script Actions</span></span>

### <a name="using-hello-azure-portal"></a><span data-ttu-id="d213c-338">Usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d213c-338">Using hello Azure portal</span></span>

1. <span data-ttu-id="d213c-339">De saudação [portal do Azure](https://portal.azure.com), selecione o cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d213c-339">From hello [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="d213c-340">Visão geral sobre cluster de HDInsight hello, selecione Olá **ações de Script** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="d213c-340">From hello HDInsight cluster overview, select hello **Script Actions** tile.</span></span>

    ![Bloco Ações de script](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > <span data-ttu-id="d213c-342">Você também pode selecionar **todas as configurações** e, em seguida, selecione **ações de Script** da seção configurações da saudação.</span><span class="sxs-lookup"><span data-stu-id="d213c-342">You can also select **All settings** and then select **Script Actions** from hello Settings section.</span></span>

4. <span data-ttu-id="d213c-343">Um histórico de scripts para este cluster é exibido na seção ações de Script de saudação.</span><span class="sxs-lookup"><span data-stu-id="d213c-343">A history of scripts for this cluster is displayed on hello Script Actions section.</span></span> <span data-ttu-id="d213c-344">Essas informações incluem uma lista de scripts persistentes.</span><span class="sxs-lookup"><span data-stu-id="d213c-344">This information includes a list of persisted scripts.</span></span> <span data-ttu-id="d213c-345">Olá captura de tela abaixo, você verá que Olá Solr script foi executado nesse cluster.</span><span class="sxs-lookup"><span data-stu-id="d213c-345">In hello screenshot below, you can see that hello Solr script has been ran on this cluster.</span></span> <span data-ttu-id="d213c-346">captura de tela de saudação não mostra todos os scripts persistentes.</span><span class="sxs-lookup"><span data-stu-id="d213c-346">hello screenshot does not show any persisted scripts.</span></span>

    ![Seção Ações de Script](./media/hdinsight-hadoop-customize-cluster-linux/script-action-history.png)

5. <span data-ttu-id="d213c-348">A seleção de um script do histórico de saudação exibe a seção de propriedades de saudação para esse script.</span><span class="sxs-lookup"><span data-stu-id="d213c-348">Selecting a script from hello history displays hello Properties section for this script.</span></span> <span data-ttu-id="d213c-349">Da parte superior de saudação da tela hello, você pode executar novamente o script hello ou promovê-la.</span><span class="sxs-lookup"><span data-stu-id="d213c-349">From hello top of hello screen, you can rerun hello script or promote it.</span></span>

    ![Propriedades de Ações de script](./media/hdinsight-hadoop-customize-cluster-linux/promote-script-actions.png)

6. <span data-ttu-id="d213c-351">Você também pode usar o hello **...**  toohello à direita de entradas em ações de tooperform de seção Olá ações de Script.</span><span class="sxs-lookup"><span data-stu-id="d213c-351">You can also use hello **...** toohello right of entries on hello Script Actions section tooperform actions.</span></span>

    ![Ações de script... uso](./media/hdinsight-hadoop-customize-cluster-linux/deletepromoted.png)

### <a name="using-azure-powershell"></a><span data-ttu-id="d213c-353">Usando o PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="d213c-353">Using Azure PowerShell</span></span>

| <span data-ttu-id="d213c-354">Use a seguinte hello...</span><span class="sxs-lookup"><span data-stu-id="d213c-354">Use hello following...</span></span> | <span data-ttu-id="d213c-355">muito...</span><span class="sxs-lookup"><span data-stu-id="d213c-355">too...</span></span> |
| --- | --- |
| <span data-ttu-id="d213c-356">Get-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="d213c-356">Get-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="d213c-357">Recuperar informações sobre as ações de script persistentes</span><span class="sxs-lookup"><span data-stu-id="d213c-357">Retrieve information on persisted script actions</span></span> |
| <span data-ttu-id="d213c-358">Get-AzureRmHDInsightScriptActionHistory</span><span class="sxs-lookup"><span data-stu-id="d213c-358">Get-AzureRmHDInsightScriptActionHistory</span></span> |<span data-ttu-id="d213c-359">Recuperar um histórico de script ações aplicadas toohello cluster ou detalhes de um script específico</span><span class="sxs-lookup"><span data-stu-id="d213c-359">Retrieve a history of script actions applied toohello cluster, or details for a specific script</span></span> |
| <span data-ttu-id="d213c-360">Set-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="d213c-360">Set-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="d213c-361">Promova um ad hoc tooa de ação de script persistentes ação de script</span><span class="sxs-lookup"><span data-stu-id="d213c-361">Promotes an ad hoc script action tooa persisted script action</span></span> |
| <span data-ttu-id="d213c-362">Remove-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="d213c-362">Remove-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="d213c-363">Rebaixa uma ação do script persistidas ação tooan ad hoc</span><span class="sxs-lookup"><span data-stu-id="d213c-363">Demotes a persisted script action tooan ad hoc action</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="d213c-364">Usando `Remove-AzureRmHDInsightPersistedScriptAction` não desfaz ações Olá executadas por um script.</span><span class="sxs-lookup"><span data-stu-id="d213c-364">Using `Remove-AzureRmHDInsightPersistedScriptAction` does not undo hello actions performed by a script.</span></span> <span data-ttu-id="d213c-365">Esse cmdlet remove apenas o sinalizador persistente hello.</span><span class="sxs-lookup"><span data-stu-id="d213c-365">This cmdlet only removes hello persisted flag.</span></span>

<span data-ttu-id="d213c-366">Olá, script de exemplo a seguir demonstra como usar o hello cmdlets toopromote e rebaixar um script.</span><span class="sxs-lookup"><span data-stu-id="d213c-366">hello following example script demonstrates using hello cmdlets toopromote, then demote a script.</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=123-140)]

### <a name="using-hello-azure-cli"></a><span data-ttu-id="d213c-367">Usando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="d213c-367">Using hello Azure CLI</span></span>

| <span data-ttu-id="d213c-368">Use a seguinte hello...</span><span class="sxs-lookup"><span data-stu-id="d213c-368">Use hello following...</span></span> | <span data-ttu-id="d213c-369">muito...</span><span class="sxs-lookup"><span data-stu-id="d213c-369">too...</span></span> |
| --- | --- |
| `azure hdinsight script-action persisted list <clustername>` |<span data-ttu-id="d213c-370">Recuperar uma lista de ações de script persistente</span><span class="sxs-lookup"><span data-stu-id="d213c-370">Retrieve a list of persisted script actions</span></span> |
| `azure hdinsight script-action persisted show <clustername> <scriptname>` |<span data-ttu-id="d213c-371">Recuperar informações sobre uma ação de script persistente específica</span><span class="sxs-lookup"><span data-stu-id="d213c-371">Retrieve information on a specific persisted script action</span></span> |
| `azure hdinsight script-action history list <clustername>` |<span data-ttu-id="d213c-372">Recuperar um histórico de script ações aplicadas toohello cluster</span><span class="sxs-lookup"><span data-stu-id="d213c-372">Retrieve a history of script actions applied toohello cluster</span></span> |
| `azure hdinsight script-action history show <clustername> <scriptname>` |<span data-ttu-id="d213c-373">Recuperar informações sobre uma ação de script específica</span><span class="sxs-lookup"><span data-stu-id="d213c-373">Retrieve information on a specific script action</span></span> |
| `azure hdinsight script action persisted set <clustername> <scriptexecutionid>` |<span data-ttu-id="d213c-374">Promova um ad hoc tooa de ação de script persistentes ação de script</span><span class="sxs-lookup"><span data-stu-id="d213c-374">Promotes an ad hoc script action tooa persisted script action</span></span> |
| `azure hdinsight script-action persisted delete <clustername> <scriptname>` |<span data-ttu-id="d213c-375">Rebaixa uma ação do script persistidas ação tooan ad hoc</span><span class="sxs-lookup"><span data-stu-id="d213c-375">Demotes a persisted script action tooan ad hoc action</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="d213c-376">Usando `azure hdinsight script-action persisted delete` não desfaz ações Olá executadas por um script.</span><span class="sxs-lookup"><span data-stu-id="d213c-376">Using `azure hdinsight script-action persisted delete` does not undo hello actions performed by a script.</span></span> <span data-ttu-id="d213c-377">Esse cmdlet remove apenas o sinalizador persistente hello.</span><span class="sxs-lookup"><span data-stu-id="d213c-377">This cmdlet only removes hello persisted flag.</span></span>

### <a name="using-hello-hdinsight-net-sdk"></a><span data-ttu-id="d213c-378">Usando Olá HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="d213c-378">Using hello HDInsight .NET SDK</span></span>

<span data-ttu-id="d213c-379">Para obter um exemplo de como usar o histórico do script tooretrieve Olá SDK .NET de um cluster, promover ou rebaixar scripts, consulte [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span><span class="sxs-lookup"><span data-stu-id="d213c-379">For an example of using hello .NET SDK tooretrieve script history from a cluster, promote or demote scripts, see [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span></span>

> [!NOTE]
> <span data-ttu-id="d213c-380">Este exemplo também demonstra como tooinstall um aplicativo de HDInsight usando Olá .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="d213c-380">This example also demonstrates how tooinstall an HDInsight application using hello .NET SDK.</span></span>

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a><span data-ttu-id="d213c-381">Suporte para software livre utilizado em clusters do HDInsight</span><span class="sxs-lookup"><span data-stu-id="d213c-381">Support for open-source software used on HDInsight clusters</span></span>

<span data-ttu-id="d213c-382">saudação de serviço do Microsoft Azure HDInsight usa um ecossistema de tecnologias de código-fonte aberto formado em torno do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="d213c-382">hello Microsoft Azure HDInsight service uses an ecosystem of open-source technologies formed around Hadoop.</span></span> <span data-ttu-id="d213c-383">O Microsoft Azure fornece um nível geral de suporte para tecnologias de software livre.</span><span class="sxs-lookup"><span data-stu-id="d213c-383">Microsoft Azure provides a general level of support for open-source technologies.</span></span> <span data-ttu-id="d213c-384">Para obter mais informações, consulte Olá **suporte escopo** seção Olá [site de perguntas frequentes sobre o suporte do Azure](https://azure.microsoft.com/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="d213c-384">For more information, see hello **Support Scope** section of hello [Azure Support FAQ website](https://azure.microsoft.com/support/faq/).</span></span> <span data-ttu-id="d213c-385">Olá serviço HDInsight fornece um nível adicional de suporte para componentes internos.</span><span class="sxs-lookup"><span data-stu-id="d213c-385">hello HDInsight service provides an additional level of support for built-in components.</span></span>

<span data-ttu-id="d213c-386">Há dois tipos de componentes de código-fonte aberto que estão disponíveis no hello serviço HDInsight:</span><span class="sxs-lookup"><span data-stu-id="d213c-386">There are two types of open-source components that are available in hello HDInsight service:</span></span>

* <span data-ttu-id="d213c-387">**Componentes internos** -esses componentes são pré-instaladas em clusters de HDInsight e fornecem funcionalidade principal do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="d213c-387">**Built-in components** - These components are pre-installed on HDInsight clusters and provide core functionality of hello cluster.</span></span> <span data-ttu-id="d213c-388">Por exemplo, o ResourceManager YARN, linguagem de consulta de Hive hello (HiveQL) e biblioteca de Mahout Olá pertencem toothis categoria.</span><span class="sxs-lookup"><span data-stu-id="d213c-388">For example, YARN ResourceManager, hello Hive query language (HiveQL), and hello Mahout library belong toothis category.</span></span> <span data-ttu-id="d213c-389">Uma lista completa dos componentes do cluster está disponível em [Novidades nas versões de cluster de Hadoop Olá fornecidas pelo HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="d213c-389">A full list of cluster components is available in [What's new in hello Hadoop cluster versions provided by HDInsight](hdinsight-component-versioning.md).</span></span>
* <span data-ttu-id="d213c-390">**Componentes personalizados** -você, como um usuário de cluster hello, instalar ou usar em sua carga de trabalho qualquer componente criado por você ou disponível na comunidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="d213c-390">**Custom components** - You, as a user of hello cluster, can install or use in your workload any component available in hello community or created by you.</span></span>

> [!WARNING]
> <span data-ttu-id="d213c-391">Componentes fornecidos com o cluster do HDInsight Olá são totalmente suportados.</span><span class="sxs-lookup"><span data-stu-id="d213c-391">Components provided with hello HDInsight cluster are fully supported.</span></span> <span data-ttu-id="d213c-392">Microsoft Support ajuda tooisolate e resolver problemas relacionados toothese componentes.</span><span class="sxs-lookup"><span data-stu-id="d213c-392">Microsoft Support helps tooisolate and resolve issues related toothese components.</span></span>
>
> <span data-ttu-id="d213c-393">Componentes personalizados recebem suporte comercialmente razoável toohelp toofurther você solucionar o problema de saudação.</span><span class="sxs-lookup"><span data-stu-id="d213c-393">Custom components receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="d213c-394">O suporte da Microsoft pode ser capaz de tooresolve problema de saudação ou eles podem solicitar que você canais disponíveis tooengage para tecnologias do código-fonte aberto Olá onde profundo conhecimento para que a tecnologia é encontrado.</span><span class="sxs-lookup"><span data-stu-id="d213c-394">Microsoft support may be able tooresolve hello issue OR they may ask you tooengage available channels for hello open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="d213c-395">Por exemplo, há muitos sites de comunidades que podem ser usados, como o [Fórum do MSDN para o HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Além disso, os projetos do Apache têm sites do projeto em [http://apache.org](http://apache.org), por exemplo: [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="d213c-395">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>

<span data-ttu-id="d213c-396">Olá serviço HDInsight fornece várias maneiras de componentes personalizados toouse.</span><span class="sxs-lookup"><span data-stu-id="d213c-396">hello HDInsight service provides several ways toouse custom components.</span></span> <span data-ttu-id="d213c-397">Olá se aplica mesmo nível de suporte, independentemente de como um componente é usado ou instalado em um cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="d213c-397">hello same level of support applies, regardless of how a component is used or installed on hello cluster.</span></span> <span data-ttu-id="d213c-398">Olá, lista a seguir descreve formas mais comuns de saudação que componentes personalizados podem ser usados em clusters de HDInsight:</span><span class="sxs-lookup"><span data-stu-id="d213c-398">hello following list describes hello most common ways that custom components can be used on HDInsight clusters:</span></span>

1. <span data-ttu-id="d213c-399">Envio de trabalho - Hadoop ou outros tipos de trabalhos em execução ou usam componentes personalizados pode ser enviado toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="d213c-399">Job submission - Hadoop or other types of jobs that execute or use custom components can be submitted toohello cluster.</span></span>

2. <span data-ttu-id="d213c-400">Personalização de cluster - durante a criação do cluster, você pode especificar configurações adicionais e componentes personalizados que são instalados em nós de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="d213c-400">Cluster customization - During cluster creation, you can specify additional settings and custom components that are installed on hello cluster nodes.</span></span>

3. <span data-ttu-id="d213c-401">Exemplos - para os componentes personalizados, Microsoft e outros podem fornecer exemplos de como esses componentes podem ser usados em clusters de HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="d213c-401">Samples - For popular custom components, Microsoft and others may provide samples of how these components can be used on hello HDInsight clusters.</span></span> <span data-ttu-id="d213c-402">Esses exemplos são fornecidos sem suporte.</span><span class="sxs-lookup"><span data-stu-id="d213c-402">These samples are provided without support.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="d213c-403">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="d213c-403">Troubleshooting</span></span>

<span data-ttu-id="d213c-404">Você pode usar informações de tooview Ambari web da interface do usuário conectadas por ações de script.</span><span class="sxs-lookup"><span data-stu-id="d213c-404">You can use Ambari web UI tooview information logged by script actions.</span></span> <span data-ttu-id="d213c-405">Se o script hello falhar durante a criação do cluster, Olá logs também estão disponíveis na conta de armazenamento padrão de saudação associada Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="d213c-405">If hello script fails during cluster creation, hello logs are also available in hello default storage account associated with hello cluster.</span></span> <span data-ttu-id="d213c-406">Esta seção fornece informações sobre como tooretrieve Olá registra usando ambas as opções.</span><span class="sxs-lookup"><span data-stu-id="d213c-406">This section provides information on how tooretrieve hello logs using both these options.</span></span>

### <a name="using-hello-ambari-web-ui"></a><span data-ttu-id="d213c-407">Usando Olá Ambari Web UI</span><span class="sxs-lookup"><span data-stu-id="d213c-407">Using hello Ambari Web UI</span></span>

1. <span data-ttu-id="d213c-408">No seu navegador, navegue toohttps://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="d213c-408">In your browser, navigate toohttps://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="d213c-409">Substitua CLUSTERNAME pelo nome de saudação do seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d213c-409">Replace CLUSTERNAME with hello name of your HDInsight cluster.</span></span>

    <span data-ttu-id="d213c-410">Quando solicitado, insira o nome de conta de administrador de saudação (administrador) e a senha para o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="d213c-410">When prompted, enter hello admin account name (admin) and password for hello cluster.</span></span> <span data-ttu-id="d213c-411">Você pode ter credenciais de administrador Olá tooreenter em um formulário da web.</span><span class="sxs-lookup"><span data-stu-id="d213c-411">You may have tooreenter hello admin credentials in a web form.</span></span>

2. <span data-ttu-id="d213c-412">Na barra de saudação na parte superior de saudação da página hello, selecione Olá **ops** entrada.</span><span class="sxs-lookup"><span data-stu-id="d213c-412">From hello bar at hello top of hello page, select hello **ops** entry.</span></span> <span data-ttu-id="d213c-413">É exibida uma lista das operações atuais e anteriores executada no cluster Olá por meio do Ambari.</span><span class="sxs-lookup"><span data-stu-id="d213c-413">A list of current and previous operations performed on hello cluster through Ambari is displayed.</span></span>

    ![Barra de interface do usuário da Web do Ambari com o item "ops" selecionado](./media/hdinsight-hadoop-customize-cluster-linux/ambari-nav.png)

3. <span data-ttu-id="d213c-415">Localizar entradas Olá com **executar\_customscriptaction** em Olá **operações** coluna.</span><span class="sxs-lookup"><span data-stu-id="d213c-415">Find hello entries that have **run\_customscriptaction** in hello **Operations** column.</span></span> <span data-ttu-id="d213c-416">Essas entradas são criadas ao executar ações de Script hello.</span><span class="sxs-lookup"><span data-stu-id="d213c-416">These entries are created when hello Script Actions run.</span></span>

    ![Captura de tela de operações](./media/hdinsight-hadoop-customize-cluster-linux/ambariscriptaction.png)

    <span data-ttu-id="d213c-418">Olá tooview STDOUT e STDERR saída selecione Olá run\customscriptaction e fazer drill down em links de saudação.</span><span class="sxs-lookup"><span data-stu-id="d213c-418">tooview hello STDOUT and STDERR output, select hello run\customscriptaction entry and drill down through hello links.</span></span> <span data-ttu-id="d213c-419">Esta saída é gerada quando a execução do script hello e pode conter informações úteis.</span><span class="sxs-lookup"><span data-stu-id="d213c-419">This output is generated when hello script runs, and may contain useful information.</span></span>

### <a name="access-logs-from-hello-default-storage-account"></a><span data-ttu-id="d213c-420">Logs de acesso da conta de armazenamento saudação padrão</span><span class="sxs-lookup"><span data-stu-id="d213c-420">Access logs from hello default storage account</span></span>

<span data-ttu-id="d213c-421">Se a criação do cluster Olá falhar devido a erro de ação de script tooa, Olá logs podem ser acessados de conta de armazenamento de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="d213c-421">If hello cluster creation fails due tooa script action error, hello logs can be accessed from hello cluster storage account.</span></span>

* <span data-ttu-id="d213c-422">Olá logs de armazenamento estão disponíveis em `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.</span><span class="sxs-lookup"><span data-stu-id="d213c-422">hello storage logs are available at `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.</span></span>

    ![Captura de tela de operações](./media/hdinsight-hadoop-customize-cluster-linux/script_action_logs_in_storage.png)

    <span data-ttu-id="d213c-424">Nesse diretório, Olá logs são organizados separadamente para o nó principal, workernode e zookeeper nós.</span><span class="sxs-lookup"><span data-stu-id="d213c-424">Under this directory, hello logs are organized separately for headnode, workernode, and zookeeper nodes.</span></span> <span data-ttu-id="d213c-425">Alguns exemplos incluem:</span><span class="sxs-lookup"><span data-stu-id="d213c-425">Some examples are:</span></span>

    * <span data-ttu-id="d213c-426">**Nó de cabeçalho** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="d213c-426">**Headnode** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`</span></span>

    * <span data-ttu-id="d213c-427">**Nó de trabalho** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="d213c-427">**Worker node** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`</span></span>

    * <span data-ttu-id="d213c-428">**Nó zookeeper** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="d213c-428">**Zookeeper node** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`</span></span>

* <span data-ttu-id="d213c-429">Todos os stdout e stderr de host correspondente Olá é carregado toohello conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d213c-429">All stdout and stderr of hello corresponding host is uploaded toohello storage account.</span></span> <span data-ttu-id="d213c-430">Há um **output-\*.txt** e um **errors-\*.txt** para cada ação de script.</span><span class="sxs-lookup"><span data-stu-id="d213c-430">There is one **output-\*.txt** and **errors-\*.txt** for each script action.</span></span> <span data-ttu-id="d213c-431">arquivo de saída-*. txt Olá contém informações sobre Olá URI do script de saudação que foi executado no host de saudação.</span><span class="sxs-lookup"><span data-stu-id="d213c-431">hello output-*.txt file contains information about hello URI of hello script that got run on hello host.</span></span> <span data-ttu-id="d213c-432">Por exemplo,</span><span class="sxs-lookup"><span data-stu-id="d213c-432">For example</span></span>

        'Start downloading script locally: ', u'https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh'

* <span data-ttu-id="d213c-433">É possível criar repetidamente um cluster de ação de script hello com o mesmo nome.</span><span class="sxs-lookup"><span data-stu-id="d213c-433">It's possible that you repeatedly create a script action cluster with hello same name.</span></span> <span data-ttu-id="d213c-434">Nesse caso, você pode distinguir logs relevantes de saudação com base no nome da pasta Data hello.</span><span class="sxs-lookup"><span data-stu-id="d213c-434">In such case, you can distinguish hello relevant logs based on hello DATE folder name.</span></span> <span data-ttu-id="d213c-435">Por exemplo, a estrutura de pasta de saudação para um cluster (mycluster) criado em datas diferentes aparece semelhante toohello entradas de log a seguir:</span><span class="sxs-lookup"><span data-stu-id="d213c-435">For example, hello folder structure for a cluster (mycluster) created on different dates appears similar toohello following log entries:</span></span>

    <span data-ttu-id="d213c-436">`\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`</span><span class="sxs-lookup"><span data-stu-id="d213c-436">`\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`</span></span>

* <span data-ttu-id="d213c-437">Se você criar um cluster de ação de script com hello mesmo nome no hello mesmo dia, você pode usar arquivos de log relevantes Olá exclusivo do prefixo tooidentify hello.</span><span class="sxs-lookup"><span data-stu-id="d213c-437">If you create a script action cluster with hello same name on hello same day, you can use hello unique prefix tooidentify hello relevant log files.</span></span>

* <span data-ttu-id="d213c-438">Se você criar um cluster próximo 12:00 AM (meia-noite), é possível que os arquivos de log Olá abrangem em dois dias.</span><span class="sxs-lookup"><span data-stu-id="d213c-438">If you create a cluster near 12:00AM (midnight), it's possible that hello log files span across two days.</span></span> <span data-ttu-id="d213c-439">Nesses casos, você ver duas pastas de datas diferentes para Olá mesmo cluster.</span><span class="sxs-lookup"><span data-stu-id="d213c-439">In such cases, you see two different date folders for hello same cluster.</span></span>

* <span data-ttu-id="d213c-440">Carregando contêiner padrão arquivos toohello de log pode demorar até minutos too5, especialmente para grandes clusters.</span><span class="sxs-lookup"><span data-stu-id="d213c-440">Uploading log files toohello default container can take up too5 mins, especially for large clusters.</span></span> <span data-ttu-id="d213c-441">Portanto, se desejar que os logs de saudação tooaccess, você não deve imediatamente Excluir cluster Olá se uma ação de script falhar.</span><span class="sxs-lookup"><span data-stu-id="d213c-441">So, if you want tooaccess hello logs, you should not immediately delete hello cluster if a script action fails.</span></span>

### <a name="ambari-watchdog"></a><span data-ttu-id="d213c-442">Ambari Watchdog</span><span class="sxs-lookup"><span data-stu-id="d213c-442">Ambari watchdog</span></span>

> [!WARNING]
> <span data-ttu-id="d213c-443">Não altere a senha de saudação do hello Ambari Watchdog (hdinsightwatchdog) no seu cluster HDInsight baseados em Linux.</span><span class="sxs-lookup"><span data-stu-id="d213c-443">Do not change hello password for hello Ambari Watchdog (hdinsightwatchdog) on your Linux-based HDInsight cluster.</span></span> <span data-ttu-id="d213c-444">A alteração de senha Olá para esta conta quebra Olá capacidade toorun novo script de ações no cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="d213c-444">Changing hello password for this account breaks hello ability toorun new script actions on hello HDInsight cluster.</span></span>

### <a name="cant-import-name-blobservice"></a><span data-ttu-id="d213c-445">Não é possível importar o BlobService de nome</span><span class="sxs-lookup"><span data-stu-id="d213c-445">Can't import name BlobService</span></span>

<span data-ttu-id="d213c-446">__Sintomas__: Olá falha da ação de script.</span><span class="sxs-lookup"><span data-stu-id="d213c-446">__Symptoms__: hello script action fails.</span></span> <span data-ttu-id="d213c-447">Texto toohello semelhante erro a seguir é exibida quando você exibir operação Olá no Ambari:</span><span class="sxs-lookup"><span data-stu-id="d213c-447">Text similar toohello following error is displayed when you view hello operation in Ambari:</span></span>

```
Traceback (most recent call list):
  File "/var/lib/ambari-agent/cache/custom_actions/scripts/run_customscriptaction.py", line 21, in <module>
    from azure.storage.blob import BlobService
ImportError: cannot import name BlobService
```

<span data-ttu-id="d213c-448">__Causa__: este erro ocorre se você atualizar o cliente de armazenamento do Azure Python Olá que está incluído no cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="d213c-448">__Cause__: This error occurs if you upgrade hello Python Azure Storage client that is included with hello HDInsight cluster.</span></span> <span data-ttu-id="d213c-449">O HDInsight espera o cliente de Armazenamento do Azure 0.20.0.</span><span class="sxs-lookup"><span data-stu-id="d213c-449">HDInsight expects Azure Storage client 0.20.0.</span></span>

<span data-ttu-id="d213c-450">__Resolução__: tooresolve esse erro, conectar-se manualmente usando de nó de cluster tooeach `ssh` e use Olá seguindo a versão do cliente de armazenamento correta do comando tooreinstall hello:</span><span class="sxs-lookup"><span data-stu-id="d213c-450">__Resolution__: tooresolve this error, manually connect tooeach cluster node using `ssh` and use hello following command tooreinstall hello correct storage client version:</span></span>

```
sudo pip install azure-storage==0.20.0
```

<span data-ttu-id="d213c-451">Para obter informações sobre conexão cluster toohello com SSH, consulte [usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="d213c-451">For information on connecting toohello cluster with SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

### <a name="history-doesnt-show-scripts-used-during-cluster-creation"></a><span data-ttu-id="d213c-452">O histórico de não mostra os scripts usados durante a criação do cluster</span><span class="sxs-lookup"><span data-stu-id="d213c-452">History doesn't show scripts used during cluster creation</span></span>

<span data-ttu-id="d213c-453">Se o cluster tiver sido criado antes de 15 de março de 2016, talvez você não veja uma entrada no histórico de Ação de Script.</span><span class="sxs-lookup"><span data-stu-id="d213c-453">If your cluster was created before March 15, 2016, you may not see an entry in Script Action history.</span></span> <span data-ttu-id="d213c-454">Se você redimensionar cluster Olá após 15 de março de 2016, Olá scripts usando durante a criação de cluster são exibidos no histórico conforme elas são aplicadas toonew nós no cluster hello como parte da saudação de operação de redimensionamento.</span><span class="sxs-lookup"><span data-stu-id="d213c-454">If you resize hello cluster after March 15, 2016, hello scripts using during cluster creation appear in history as they are applied toonew nodes in hello cluster as part of hello resize operation.</span></span>

<span data-ttu-id="d213c-455">Há duas exceções:</span><span class="sxs-lookup"><span data-stu-id="d213c-455">There are two exceptions:</span></span>

* <span data-ttu-id="d213c-456">Se o cluster tiver sido criado antes de 1º de setembro de 2015.</span><span class="sxs-lookup"><span data-stu-id="d213c-456">If your cluster was created before September 1, 2015.</span></span> <span data-ttu-id="d213c-457">Esta data é quando as Ações de Script foram introduzidas.</span><span class="sxs-lookup"><span data-stu-id="d213c-457">This date is when Script Actions were introduced.</span></span> <span data-ttu-id="d213c-458">Qualquer cluster criado antes dessa data não poderia ter usado as Ações de Script para a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="d213c-458">Any cluster created before this date could not have used Script Actions for cluster creation.</span></span>

* <span data-ttu-id="d213c-459">Se você usou várias ações de Script durante a criação do cluster e usado Olá mesmo nome para vários scripts ou Olá mesmo nome, mesmo URI, mas diferentes parâmetros para vários scripts.</span><span class="sxs-lookup"><span data-stu-id="d213c-459">If you used multiple Script Actions during cluster creation, and used hello same name for multiple scripts, or hello same name, same URI, but different parameters for multiple scripts.</span></span> <span data-ttu-id="d213c-460">Nesses casos, você receberá Olá erro a seguir:</span><span class="sxs-lookup"><span data-stu-id="d213c-460">In these cases, you receive hello following error:</span></span>

    <span data-ttu-id="d213c-461">Nenhum script de novas ações podem ser executado nesse cluster devido a nomes de script tooconflicting nos scripts existentes.</span><span class="sxs-lookup"><span data-stu-id="d213c-461">No new script actions can be ran on this cluster due tooconflicting script names in existing scripts.</span></span> <span data-ttu-id="d213c-462">Os nomes de script fornecidos na criação do cluster devem ser exclusivos.</span><span class="sxs-lookup"><span data-stu-id="d213c-462">Script names provided at cluster create must be all unique.</span></span> <span data-ttu-id="d213c-463">Os scripts existentes são executados no redimensionamento.</span><span class="sxs-lookup"><span data-stu-id="d213c-463">Existing scripts are ran on resize.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d213c-464">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d213c-464">Next steps</span></span>

* [<span data-ttu-id="d213c-465">Desenvolver scripts de Ação de Script para o HDInsight</span><span class="sxs-lookup"><span data-stu-id="d213c-465">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions-linux.md)
* [<span data-ttu-id="d213c-466">Instalar e usar o Solr em clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="d213c-466">Install and use Solr on HDInsight clusters</span></span>](hdinsight-hadoop-solr-install-linux.md)
* [<span data-ttu-id="d213c-467">Instalar e usar o Giraph em clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="d213c-467">Install and use Giraph on HDInsight clusters</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* [<span data-ttu-id="d213c-468">Adicionar o cluster do HDInsight tooan armazenamento adicional</span><span class="sxs-lookup"><span data-stu-id="d213c-468">Add additional storage tooan HDInsight cluster</span></span>](hdinsight-hadoop-add-storage.md)

[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster-linux/HDI-Cluster-state.png "Estágios durante a criação de cluster"
