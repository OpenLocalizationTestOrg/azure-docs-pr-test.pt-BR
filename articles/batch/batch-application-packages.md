---
title: "pacotes de aplicativos aaaInstall em nós de computação - lote do Azure | Microsoft Docs"
description: "Recurso de pacotes de aplicativos Use saudação do lote do Azure tooeasily gerenciar vários aplicativos e nós de computação de versões para instalação em lote."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 3b6044b7-5f65-4a27-9d43-71e1863d16cf
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 683be7b7f1bd5db7835332016f6dccb72f45c3b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-applications-toocompute-nodes-with-batch-application-packages"></a><span data-ttu-id="3d9d0-103">Implantar aplicativos toocompute nós com pacotes de aplicativos de lote</span><span class="sxs-lookup"><span data-stu-id="3d9d0-103">Deploy applications toocompute nodes with Batch application packages</span></span>

<span data-ttu-id="3d9d0-104">recurso de pacotes de aplicativos de saudação do lote do Azure fornece fácil gerenciamento de aplicativos de tarefa e sua implantação toohello nós de computação em seu pool.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-104">hello application packages feature of Azure Batch provides easy management of task applications and their deployment toohello compute nodes in your pool.</span></span> <span data-ttu-id="3d9d0-105">Com pacotes de aplicativos, você pode carregar e gerenciar várias versões de aplicativos Olá que executar suas tarefas, incluindo seus arquivos de suporte.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-105">With application packages, you can upload and manage multiple versions of hello applications your tasks run, including their supporting files.</span></span> <span data-ttu-id="3d9d0-106">Automaticamente, em seguida, pode implantar um ou mais desses aplicativos toohello nós de computação em seu pool.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-106">You can then automatically deploy one or more of these applications toohello compute nodes in your pool.</span></span>

<span data-ttu-id="3d9d0-107">Neste artigo, você aprenderá como tooupload e gerenciar pacotes de aplicativos no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-107">In this article, you will learn how tooupload and manage application packages in hello Azure portal.</span></span> <span data-ttu-id="3d9d0-108">Em seguida, você aprenderá como tooinstall-los em um pool nós de computação com hello [Batch .NET] [ api_net] biblioteca.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-108">You will then learn how tooinstall them on a pool's compute nodes with hello [Batch .NET][api_net] library.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="3d9d0-109">Os pacotes de aplicativos têm suporte em todos os pools do Lote criados após 5 de julho de 2017.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-109">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="3d9d0-110">Eles têm suporte em pools de lote criados entre 10 de março de 2016 e 5 de julho de 2017 somente se o pool de saudação foi criado usando uma configuração de serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-110">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if hello pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="3d9d0-111">Pools de lote criados too10 anterior de março de 2016 não dão suporte a pacotes de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-111">Batch pools created prior too10 March 2016 do not support application packages.</span></span>
>
> <span data-ttu-id="3d9d0-112">Olá, APIs para criar e gerenciar pacotes de aplicativos fazem parte da saudação [Batch Management .NET] [[api_net_mgmt]] biblioteca.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-112">hello APIs for creating and managing application packages are part of hello [Batch Management .NET][[api_net_mgmt]] library.</span></span> <span data-ttu-id="3d9d0-113">APIs para instalar os pacotes de aplicativo em um nó de computação Hello fazem parte da saudação [Batch .NET] [ api_net] biblioteca.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-113">hello APIs for installing application packages on a compute node are part of hello [Batch .NET][api_net] library.</span></span>  
>
> <span data-ttu-id="3d9d0-114">recurso de pacotes de aplicativo Hello descrito aqui substitui o recurso de aplicativos em lotes Olá disponível em versões anteriores do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-114">hello application packages feature described here supersedes hello Batch Apps feature available in previous versions of hello service.</span></span>
> 
> 

## <a name="application-package-requirements"></a><span data-ttu-id="3d9d0-115">Requisitos do pacote de aplicativos</span><span class="sxs-lookup"><span data-stu-id="3d9d0-115">Application package requirements</span></span>
<span data-ttu-id="3d9d0-116">pacotes de aplicativos toouse, é necessário muito[vincular uma conta de armazenamento do Azure](#link-a-storage-account) tooyour conta do lote.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-116">toouse application packages, you need too[link an Azure Storage account](#link-a-storage-account) tooyour Batch account.</span></span>

<span data-ttu-id="3d9d0-117">Este recurso foi introduzido no [API REST do lote] [ api_rest] versão 2015-12-01.2.2 e Olá correspondente [Batch .NET] [ api_net] versão da biblioteca 3.1.0.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-117">This feature was introduced in [Batch REST API][api_rest] version 2015-12-01.2.2 and hello corresponding [Batch .NET][api_net] library version 3.1.0.</span></span> <span data-ttu-id="3d9d0-118">É recomendável que você sempre use mais recente versão da API Olá ao trabalhar com o lote.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-118">We recommend that you always use hello latest API version when working with Batch.</span></span>

> [!NOTE]
> <span data-ttu-id="3d9d0-119">Os pacotes de aplicativos têm suporte em todos os pools do Lote criados após 5 de julho de 2017.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-119">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="3d9d0-120">Eles têm suporte em pools de lote criados entre 10 de março de 2016 e 5 de julho de 2017 somente se o pool de saudação foi criado usando uma configuração de serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-120">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if hello pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="3d9d0-121">Pools de lote criados too10 anterior de março de 2016 não dão suporte a pacotes de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-121">Batch pools created prior too10 March 2016 do not support application packages.</span></span>
>
>

## <a name="about-applications-and-application-packages"></a><span data-ttu-id="3d9d0-122">Sobre aplicativos e pacotes de aplicativos</span><span class="sxs-lookup"><span data-stu-id="3d9d0-122">About applications and application packages</span></span>
<span data-ttu-id="3d9d0-123">Em lote do Azure, uma *aplicativo* refere-se o conjunto de tooa de binários com controle de versão que podem ser baixados automaticamente toohello nós de computação no pool de.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-123">Within Azure Batch, an *application* refers tooa set of versioned binaries that can be automatically downloaded toohello compute nodes in your pool.</span></span> <span data-ttu-id="3d9d0-124">Um *pacote de aplicativo* refere-se tooa *conjunto específico* desses binários e representa um determinado *versão* do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-124">An *application package* refers tooa *specific set* of those binaries and represents a given *version* of hello application.</span></span>

<span data-ttu-id="3d9d0-125">![Diagrama de alto nível de aplicativos e pacotes de aplicativos][1]</span><span class="sxs-lookup"><span data-stu-id="3d9d0-125">![High-level diagram of applications and application packages][1]</span></span>

### <a name="applications"></a><span data-ttu-id="3d9d0-126">Aplicativos</span><span class="sxs-lookup"><span data-stu-id="3d9d0-126">Applications</span></span>
<span data-ttu-id="3d9d0-127">Um aplicativo em lote contém uma ou mais aplicativos, pacotes e especifica opções de configuração para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-127">An application in Batch contains one or more application packages and specifies configuration options for hello application.</span></span> <span data-ttu-id="3d9d0-128">Por exemplo, um aplicativo pode especificar o saudação padrão aplicativo pacote versão tooinstall em nós de computação e se seus pacotes podem ser atualizados ou excluídos.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-128">For example, an application can specify hello default application package version tooinstall on compute nodes and whether its packages can be updated or deleted.</span></span>

### <a name="application-packages"></a><span data-ttu-id="3d9d0-129">pacotes de aplicativos</span><span class="sxs-lookup"><span data-stu-id="3d9d0-129">Application packages</span></span>
<span data-ttu-id="3d9d0-130">Um pacote de aplicativo é um arquivo. zip que contém os binários do aplicativo hello e arquivos de suporte que são necessários para seu aplicativo de saudação do toorun de tarefas.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-130">An application package is a .zip file that contains hello application binaries and supporting files that are required for your tasks toorun hello application.</span></span> <span data-ttu-id="3d9d0-131">Cada pacote de aplicativo representa uma versão específica do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-131">Each application package represents a specific version of hello application.</span></span>

<span data-ttu-id="3d9d0-132">Você pode especificar os pacotes de aplicativos em níveis de pool e tarefa hello.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-132">You can specify application packages at hello pool and task levels.</span></span> <span data-ttu-id="3d9d0-133">Você pode especificar um ou mais desses pacotes e (opcionalmente) uma versão quando você cria uma tarefa ou um pool.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-133">You can specify one or more of these packages and (optionally) a version when you create a pool or task.</span></span>

* <span data-ttu-id="3d9d0-134">**Pacotes de aplicativos do pool** são implantados muito*cada* nó no pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-134">**Pool application packages** are deployed too*every* node in hello pool.</span></span> <span data-ttu-id="3d9d0-135">Os aplicativos são implantados quando um nó ingressa em um pool e quando ele é reinicializado ou tem a imagem recriada.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-135">Applications are deployed when a node joins a pool, and when it is rebooted or reimaged.</span></span>
  
    <span data-ttu-id="3d9d0-136">Os pacotes de aplicativos do pool são adequados quando todos os nós em um pool executam as tarefas de um trabalho.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-136">Pool application packages are appropriate when all nodes in a pool execute a job's tasks.</span></span> <span data-ttu-id="3d9d0-137">Você pode especificar um ou mais pacotes de aplicativos quando cria um pool e pode adicionar ou atualizar os pacotes de um pool existente.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-137">You can specify one or more application packages when you create a pool, and you can add or update an existing pool's packages.</span></span> <span data-ttu-id="3d9d0-138">Se você atualizar os pacotes de aplicativos de um pool existente, você deve reiniciar o novo pacote seus nós tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-138">If you update an existing pool's application packages, you must restart its nodes tooinstall hello new package.</span></span>
* <span data-ttu-id="3d9d0-139">**Pacotes de aplicativos de tarefas** são implantados somente do nó de computação tooa toorun um tarefa agendada, apenas antes de executar a linha de comando da tarefa de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-139">**Task application packages** are deployed only tooa compute node scheduled toorun a task, just before running hello task's command line.</span></span> <span data-ttu-id="3d9d0-140">Se especificado de saudação versão e o pacote de aplicativo já está no nó de saudação, ele não for reimplantado e pacote existente de saudação é usado.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-140">If hello specified application package and version is already on hello node, it is not redeployed and hello existing package is used.</span></span>
  
    <span data-ttu-id="3d9d0-141">Pacotes de aplicativos de tarefas são úteis em ambientes de pool compartilhado, onde diferentes trabalhos são executados em um pool e pool de saudação não será excluído quando um trabalho é concluído.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-141">Task application packages are useful in shared-pool environments, where different jobs are run on one pool, and hello pool is not deleted when a job is completed.</span></span> <span data-ttu-id="3d9d0-142">Se o trabalho tiver menos tarefas que os nós no pool hello, pacotes de aplicativos de tarefa podem minimizar transferência de dados desde que o aplicativo é implantado toohello apenas nós que executam tarefas.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-142">If your job has fewer tasks than nodes in hello pool, task application packages can minimize data transfer since your application is deployed only toohello nodes that run tasks.</span></span>
  
    <span data-ttu-id="3d9d0-143">Outros cenários que podem aproveitar os pacotes de aplicativos de tarefa são os trabalhos que executam um aplicativo grande, mas para um pequeno número de tarefas.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-143">Other scenarios that can benefit from task application packages are jobs that run a large application, but for only a few tasks.</span></span> <span data-ttu-id="3d9d0-144">Por exemplo, uma fase de pré-processamento ou uma tarefa de mesclagem, onde o aplicativo hello de pré-processamento ou de mesclagem é pesado, pode se beneficiar do uso pacotes de aplicativos de tarefa.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-144">For example, a pre-processing stage or a merge task, where hello pre-processing or merge application is heavyweight, may benefit from using task application packages.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3d9d0-145">Há restrições no número de saudação de aplicativos e pacotes de aplicativos dentro de uma conta de lote e no tamanho de pacote de aplicativo máximo hello.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-145">There are restrictions on hello number of applications and application packages within a Batch account and on hello maximum application package size.</span></span> <span data-ttu-id="3d9d0-146">Consulte [cotas e limites de saudação do serviço Azure Batch](batch-quota-limit.md) para obter detalhes sobre esses limites.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-146">See [Quotas and limits for hello Azure Batch service](batch-quota-limit.md) for details about these limits.</span></span>
> 
> 

### <a name="benefits-of-application-packages"></a><span data-ttu-id="3d9d0-147">Benefícios dos pacotes de aplicativos</span><span class="sxs-lookup"><span data-stu-id="3d9d0-147">Benefits of application packages</span></span>
<span data-ttu-id="3d9d0-148">Pacotes de aplicativos podem simplificar o código de saudação em sua solução de lote e aplicativos do hello de sobrecarga toomanage necessário Olá inferiores executar suas tarefas.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-148">Application packages can simplify hello code in your Batch solution and lower hello overhead required toomanage hello applications that your tasks run.</span></span>

<span data-ttu-id="3d9d0-149">Com pacotes de aplicativos, tarefas do início do pool não tem toospecify uma longa lista de recursos individuais arquivos tooinstall em nós de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-149">With application packages, your pool's start task doesn't have toospecify a long list of individual resource files tooinstall on hello nodes.</span></span> <span data-ttu-id="3d9d0-150">Você não tem toomanually gerenciar várias versões dos seus arquivos de aplicativo no armazenamento do Azure ou em seus nós.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-150">You don't have toomanually manage multiple versions of your application files in Azure Storage, or on your nodes.</span></span> <span data-ttu-id="3d9d0-151">E, você não precisa tooworry sobre como gerar [URLs da SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md) tooprovide acessar toohello arquivos em sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-151">And, you don't need tooworry about generating [SAS URLs](../storage/common/storage-dotnet-shared-access-signature-part-1.md) tooprovide access toohello files in your Storage account.</span></span> <span data-ttu-id="3d9d0-152">Lote funciona no plano de fundo de saudação com pacotes de aplicativos de toostore de armazenamento do Azure e implantá-las toocompute nós.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-152">Batch works in hello background with Azure Storage toostore application packages and deploy them toocompute nodes.</span></span>

> [!NOTE] 
> <span data-ttu-id="3d9d0-153">Olá tamanho total de uma tarefa de início deve ser menor ou igual too32768 caracteres, incluindo arquivos de recurso e variáveis de ambiente.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-153">hello total size of a start task must be less than or equal too32768 characters, including resource files and environment variables.</span></span> <span data-ttu-id="3d9d0-154">Se a tarefa de inicialização exceder esse limite, usar pacotes de aplicativos é outra opção.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-154">If your start task exceeds this limit, then using application packages is another option.</span></span> <span data-ttu-id="3d9d0-155">Você pode também criar um arquivo compactado que contém os arquivos de recurso, carregá-lo como um blob de tooAzure armazenamento e descompacte-o na linha de comando de saudação da tarefa inicial.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-155">You can also create a zipped archive containing your resource files, upload it as a blob tooAzure Storage, and then unzip it from hello command line of your start task.</span></span> 
>
>

## <a name="upload-and-manage-applications"></a><span data-ttu-id="3d9d0-156">Carregar e gerenciar aplicativos</span><span class="sxs-lookup"><span data-stu-id="3d9d0-156">Upload and manage applications</span></span>
<span data-ttu-id="3d9d0-157">Você pode usar o hello [portal do Azure] [ portal] ou hello [Batch Management .NET](batch-management-dotnet.md) pacotes de aplicativos de biblioteca toomanage Olá em sua conta do lote.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-157">You can use hello [Azure portal][portal] or hello [Batch Management .NET](batch-management-dotnet.md) library toomanage hello application packages in your Batch account.</span></span> <span data-ttu-id="3d9d0-158">Em seguida Olá seções, primeiro, mostramos como toolink uma conta de armazenamento, em seguida, discuta adicionar aplicativos e pacotes e gerenciá-las com hello portal.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-158">In hello next few sections, we first show how toolink a Storage account, then discuss adding applications and packages and managing them with hello portal.</span></span>

### <a name="link-a-storage-account"></a><span data-ttu-id="3d9d0-159">Vincular uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="3d9d0-159">Link a Storage account</span></span>
<span data-ttu-id="3d9d0-160">toouse pacotes de aplicativos, primeiro você deve vincular uma conta de armazenamento do Azure tooyour conta do lote.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-160">toouse application packages, you must first link an Azure Storage account tooyour Batch account.</span></span> <span data-ttu-id="3d9d0-161">Se você ainda não tiver configurado uma conta de armazenamento, hello portal do Azure exibe uma saudação aviso primeira vez que você clicar em Olá **aplicativos** lado a lado no hello **conta de lote** folha.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-161">If you have not yet configured a Storage account, hello Azure portal displays a warning hello first time you click hello **Applications** tile in hello **Batch account** blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3d9d0-162">Lote atualmente oferece suporte a *somente* Olá **geral** tipo de conta de armazenamento, conforme descrito na etapa 5, [criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account), na [sobre o Azure contas de armazenamento](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="3d9d0-162">Batch currently supports *only* hello **General-purpose** storage account type as described in step 5, [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account), in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="3d9d0-163">Vincular ao vincular uma conta de armazenamento do Azure tooyour conta em lotes, *somente* um **geral** conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-163">When you link an Azure Storage account tooyour Batch account, link *only* a **General-purpose** storage account.</span></span>
> 
> 

<span data-ttu-id="3d9d0-164">![Aviso de 'Nenhuma conta de armazenamento configurada' no portal do Azure][9]</span><span class="sxs-lookup"><span data-stu-id="3d9d0-164">!['No storage account configured' warning in Azure portal][9]</span></span>

<span data-ttu-id="3d9d0-165">Olá lote serviço usa Olá associados toostore da conta de armazenamento seus pacotes de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-165">hello Batch service uses hello associated Storage account toostore your application packages.</span></span> <span data-ttu-id="3d9d0-166">Depois de vincular duas contas de hello, lote pode implantar automaticamente pacotes de saudação armazenados em nós de computação tooyour do conta de armazenamento Olá vinculado.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-166">After you've linked hello two accounts, Batch can automatically deploy hello packages stored in hello linked Storage account tooyour compute nodes.</span></span> <span data-ttu-id="3d9d0-167">toolink uma conta de armazenamento tooyour conta do lote, clique em **configurações de conta de armazenamento** em Olá **aviso** folha e depois clique em **conta de armazenamento** em Olá **Conta de armazenamento** folha.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-167">toolink a Storage account tooyour Batch account, click **Storage account settings** on hello **Warning** blade, and then click **Storage Account** on hello **Storage Account** blade.</span></span>

<span data-ttu-id="3d9d0-168">![Folha Escolher conta de armazenamento no portal do Azure][10]</span><span class="sxs-lookup"><span data-stu-id="3d9d0-168">![Choose storage account blade in Azure portal][10]</span></span>

<span data-ttu-id="3d9d0-169">Recomendamos que você crie uma conta de armazenamento para usar *especificamente* com sua conta do Lote e que a selecione aqui.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-169">We recommend that you create a Storage account *specifically* for use with your Batch account, and select it here.</span></span> <span data-ttu-id="3d9d0-170">Para obter detalhes sobre como toocreate uma conta de armazenamento, consulte "Criar uma conta de armazenamento" [contas de armazenamento do Azure sobre](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="3d9d0-170">For details about how toocreate a storage account, see "Create a Storage account" in [About Azure Storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="3d9d0-171">Depois de criar uma conta de armazenamento, você pode, em seguida, vinculá-lo tooyour conta do lote usando Olá **conta de armazenamento** folha.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-171">After you've created a Storage account, you can then link it tooyour Batch account by using hello **Storage Account** blade.</span></span>

> [!WARNING]
> <span data-ttu-id="3d9d0-172">Olá serviço de lote usa toostore de armazenamento do Azure seus pacotes de aplicativos como blobs de bloco.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-172">hello Batch service uses Azure Storage toostore your application packages as block blobs.</span></span> <span data-ttu-id="3d9d0-173">Você está [cobrada como normal] [ storage_pricing] para dados de blob de bloco hello.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-173">You are [charged as normal][storage_pricing] for hello block blob data.</span></span> <span data-ttu-id="3d9d0-174">Ter certeza de que tamanho de saudação de tooconsider e número de seus pacotes de aplicativos e remover periodicamente os custos de toominimize pacotes substituídos.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-174">Be sure tooconsider hello size and number of your application packages, and periodically remove deprecated packages toominimize costs.</span></span>
> 
> 

### <a name="view-current-applications"></a><span data-ttu-id="3d9d0-175">Exibir aplicativos atuais</span><span class="sxs-lookup"><span data-stu-id="3d9d0-175">View current applications</span></span>
<span data-ttu-id="3d9d0-176">aplicativos de saudação tooview em sua conta de lote, clique em Olá **aplicativos** item de menu no menu esquerdo de saudação ao exibir hello **conta de lote** folha.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-176">tooview hello applications in your Batch account, click hello **Applications** menu item in hello left menu while viewing hello **Batch account** blade.</span></span>

<span data-ttu-id="3d9d0-177">![Bloco Aplicativos][2]</span><span class="sxs-lookup"><span data-stu-id="3d9d0-177">![Applications tile][2]</span></span>

<span data-ttu-id="3d9d0-178">Selecionar essa opção de menu abre Olá **aplicativos** folha:</span><span class="sxs-lookup"><span data-stu-id="3d9d0-178">Selecting this menu option opens hello **Applications** blade:</span></span>

<span data-ttu-id="3d9d0-179">![Listar aplicativos][3]</span><span class="sxs-lookup"><span data-stu-id="3d9d0-179">![List applications][3]</span></span>

<span data-ttu-id="3d9d0-180">Olá **aplicativos** folha exibe Olá ID de cada aplicativo em sua conta e Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="3d9d0-180">hello **Applications** blade displays hello ID of each application in your account and hello following properties:</span></span>

* <span data-ttu-id="3d9d0-181">**Pacotes**: Olá número de versões associadas a este aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-181">**Packages**: hello number of versions associated with this application.</span></span>
* <span data-ttu-id="3d9d0-182">**Versão padrão**: versão do aplicativo hello instalado se você não indica uma versão quando você especificar o aplicativo hello para um pool.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-182">**Default version**: hello application version installed if you do not indicate a version when you specify hello application for a pool.</span></span> <span data-ttu-id="3d9d0-183">Essa configuração é opcional.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-183">This setting is optional.</span></span>
* <span data-ttu-id="3d9d0-184">**Permitir atualizações**: valor de saudação que especifica se o pacote de atualizações, exclusões e adições são permitidos.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-184">**Allow updates**: hello value that specifies whether package updates, deletions, and additions are allowed.</span></span> <span data-ttu-id="3d9d0-185">Se isso for definido muito**não**, exclusões e atualizações de pacote estão desabilitadas para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-185">If this is set too**No**, package updates and deletions are disabled for hello application.</span></span> <span data-ttu-id="3d9d0-186">Apenas novas versões do pacote de aplicativos poderão ser adicionadas.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-186">Only new application package versions can be added.</span></span> <span data-ttu-id="3d9d0-187">saudação padrão é **Sim**.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-187">hello default is **Yes**.</span></span>

### <a name="view-application-details"></a><span data-ttu-id="3d9d0-188">Exibir detalhes do aplicativo</span><span class="sxs-lookup"><span data-stu-id="3d9d0-188">View application details</span></span>
<span data-ttu-id="3d9d0-189">folha de saudação tooopen que inclui detalhes de saudação para um aplicativo hello de aplicativo, selecione em Olá **aplicativos** folha.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-189">tooopen hello blade that includes hello details for an application, select hello application in hello **Applications** blade.</span></span>

<span data-ttu-id="3d9d0-190">![Detalhes do aplicativo][4]</span><span class="sxs-lookup"><span data-stu-id="3d9d0-190">![Application details][4]</span></span>

<span data-ttu-id="3d9d0-191">Na folha de detalhes do aplicativo hello, você pode configurar Olá seguindo as configurações para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-191">In hello application details blade, you can configure hello following settings for your application.</span></span>

* <span data-ttu-id="3d9d0-192">**Permitir atualizações**: especifique se seus pacotes de aplicativos podem ser atualizados ou excluídos.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-192">**Allow updates**: Specify whether its application packages can be updated or deleted.</span></span> <span data-ttu-id="3d9d0-193">Consulte "Atualizar ou excluir um pacote de aplicativos" mais adiante neste artigo.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-193">See "Update or Delete an application package" later in this article.</span></span>
* <span data-ttu-id="3d9d0-194">**Versão padrão**: especificar um padrão aplicativo pacote toodeploy toocompute nós.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-194">**Default version**: Specify a default application package toodeploy toocompute nodes.</span></span>
* <span data-ttu-id="3d9d0-195">**Nome de exibição**: especificar amigável para um nome que sua solução pode usar quando ele exibe informações sobre o aplicativo hello, por exemplo, no hello da interface do usuário de um serviço que você fornecer tooyour clientes por meio de lote de lote.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-195">**Display name**: Specify a friendly name that your Batch solution can use when it displays information about hello application, for example, in hello UI of a service that you provide tooyour customers through Batch.</span></span>

### <a name="add-a-new-application"></a><span data-ttu-id="3d9d0-196">Adicionar um novo aplicativo</span><span class="sxs-lookup"><span data-stu-id="3d9d0-196">Add a new application</span></span>
<span data-ttu-id="3d9d0-197">toocreate um novo aplicativo, adicione um pacote de aplicativos e especifique uma ID de aplicativo nova e exclusiva.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-197">toocreate a new application, add an application package and specify a new, unique application ID.</span></span> <span data-ttu-id="3d9d0-198">Olá primeiro pacote de aplicativos que você adicionar a nova ID de aplicativo hello também cria Olá novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-198">hello first application package that you add with hello new application ID also creates hello new application.</span></span>

<span data-ttu-id="3d9d0-199">Clique em **adicionar** em Olá **aplicativos** saudação do folha tooopen **novo aplicativo** folha.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-199">Click **Add** on hello **Applications** blade tooopen hello **New application** blade.</span></span>

<span data-ttu-id="3d9d0-200">![Folha Novo aplicativo no portal do Azure][5]</span><span class="sxs-lookup"><span data-stu-id="3d9d0-200">![New application blade in Azure portal][5]</span></span>

<span data-ttu-id="3d9d0-201">Olá **novo aplicativo** folha fornece a seguinte Olá campos toospecify configurações de saudação do seu pacote de aplicativos e o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-201">hello **New application** blade provides hello following fields toospecify hello settings of your new application and application package.</span></span>

<span data-ttu-id="3d9d0-202">**ID do aplicativo**</span><span class="sxs-lookup"><span data-stu-id="3d9d0-202">**Application id**</span></span>

<span data-ttu-id="3d9d0-203">Este campo especifica a ID de saudação do seu novo aplicativo, que é o assunto toohello padrão ID de lote do Azure as regras de validação.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-203">This field specifies hello ID of your new application, which is subject toohello standard Azure Batch ID validation rules.</span></span> <span data-ttu-id="3d9d0-204">regras de saudação para fornecer uma ID de aplicativo são da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="3d9d0-204">hello rules for providing an application ID are as follows:</span></span>

* <span data-ttu-id="3d9d0-205">Em nós do Windows, Olá ID pode conter qualquer combinação de caracteres alfanuméricos, hifens e sublinhados.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-205">On Windows nodes, hello ID can contain any combination of alphanumeric characters, hyphens, and underscores.</span></span> <span data-ttu-id="3d9d0-206">Em nós do Linux, são permitidos somente caracteres alfanuméricos e sublinhados.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-206">On Linux nodes, only alphanumeric characters and underscores are permitted.</span></span>
* <span data-ttu-id="3d9d0-207">Não pode conter mais de 64 caracteres.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-207">Cannot contain more than 64 characters.</span></span>
* <span data-ttu-id="3d9d0-208">Deve ser exclusivo dentro de saudação conta do lote.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-208">Must be unique within hello Batch account.</span></span>
* <span data-ttu-id="3d9d0-209">Não diferencia maiúsculas de minúsculas e preserva maiúsculas e minúsculas.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-209">Is case-preserving and case-insensitive.</span></span>

<span data-ttu-id="3d9d0-210">**Versão**</span><span class="sxs-lookup"><span data-stu-id="3d9d0-210">**Version**</span></span>

<span data-ttu-id="3d9d0-211">Este campo especifica a versão de Olá Olá do pacote de aplicativo que está carregando.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-211">This field specifies hello version of hello application package you are uploading.</span></span> <span data-ttu-id="3d9d0-212">Cadeias de caracteres de versão são toohello assunto regras de validação a seguir:</span><span class="sxs-lookup"><span data-stu-id="3d9d0-212">Version strings are subject toohello following validation rules:</span></span>

* <span data-ttu-id="3d9d0-213">Em nós do Windows, a cadeia de caracteres de versão Olá pode conter qualquer combinação de caracteres alfanuméricos, hifens, sublinhados e pontos.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-213">On Windows nodes, hello version string can contain any combination of alphanumeric characters, hyphens, underscores, and periods.</span></span> <span data-ttu-id="3d9d0-214">Em nós do Linux, a cadeia de caracteres de versão Olá pode conter apenas caracteres alfanuméricos e sublinhados.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-214">On Linux nodes, hello version string can contain only alphanumeric characters and underscores.</span></span>
* <span data-ttu-id="3d9d0-215">Não pode conter mais de 64 caracteres.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-215">Cannot contain more than 64 characters.</span></span>
* <span data-ttu-id="3d9d0-216">Deve ser exclusivo dentro do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-216">Must be unique within hello application.</span></span>
* <span data-ttu-id="3d9d0-217">Não diferenciam maiúsculas de minúsculas e preservam maiúsculas e minúsculas.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-217">Are case-preserving and case-insensitive.</span></span>

<span data-ttu-id="3d9d0-218">**Pacote de aplicativos**</span><span class="sxs-lookup"><span data-stu-id="3d9d0-218">**Application package**</span></span>

<span data-ttu-id="3d9d0-219">Este campo especifica um arquivo. zip Olá que contém os binários do aplicativo hello e arquivos de suporte que são necessários tooexecute Olá aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-219">This field specifies hello .zip file that contains hello application binaries and supporting files that are required tooexecute hello application.</span></span> <span data-ttu-id="3d9d0-220">Clique em Olá **selecionar um arquivo** caixa ou hello pasta ícone toobrowse tooand selecionar um arquivo. zip que contém os arquivos do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-220">Click hello **Select a file** box or hello folder icon toobrowse tooand select a .zip file that contains your application's files.</span></span>

<span data-ttu-id="3d9d0-221">Depois de selecionar um arquivo, clique em **Okey** toobegin Olá carregamento tooAzure armazenamento.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-221">After you've selected a file, click **OK** toobegin hello upload tooAzure Storage.</span></span> <span data-ttu-id="3d9d0-222">Quando a operação de carregamento de saudação for concluída, o portal de saudação exibe uma notificação e fecha a folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-222">When hello upload operation is complete, hello portal displays a notification and closes hello blade.</span></span> <span data-ttu-id="3d9d0-223">Dependendo do tamanho de saudação do arquivo hello que você está carregando e Olá a velocidade de sua conexão de rede, essa operação pode levar algum tempo.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-223">Depending on hello size of hello file that you are uploading and hello speed of your network connection, this operation may take some time.</span></span>

> [!WARNING]
> <span data-ttu-id="3d9d0-224">Não feche Olá **novo aplicativo** folha antes da operação de carregamento de saudação conclusão.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-224">Do not close hello **New application** blade before hello upload operation is complete.</span></span> <span data-ttu-id="3d9d0-225">Isso irá parar o processo de carregamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-225">Doing so will stop hello upload process.</span></span>
> 
> 

### <a name="add-a-new-application-package"></a><span data-ttu-id="3d9d0-226">Adicionar um novo pacote de aplicativos</span><span class="sxs-lookup"><span data-stu-id="3d9d0-226">Add a new application package</span></span>
<span data-ttu-id="3d9d0-227">tooadd uma nova versão do pacote de aplicativo para um aplicativo existente, selecione um aplicativo no hello **aplicativos** folha, clique em **pacotes**, em seguida, clique em **adicionar** tooopen Olá **Adicionar pacote** folha.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-227">tooadd a new application package version for an existing application, select an application in hello **Applications** blade, click **Packages**, then click **Add** tooopen hello **Add package** blade.</span></span>

<span data-ttu-id="3d9d0-228">![Folha Adicionar pacote de aplicativos no portal do Azure][8]</span><span class="sxs-lookup"><span data-stu-id="3d9d0-228">![Add application package blade in Azure portal][8]</span></span>

<span data-ttu-id="3d9d0-229">Como você pode ver, campos de saudação correspondem da saudação **novo aplicativo** folha, mas Olá **id do aplicativo** caixa está desabilitada.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-229">As you can see, hello fields match those of hello **New application** blade, but hello **Application id** box is disabled.</span></span> <span data-ttu-id="3d9d0-230">Como você fez para o novo aplicativo de hello, especifique Olá **versão** para o novo pacote, procurar tooyour **pacote de aplicativo** . zip do arquivo, em seguida, clique em **Okey** Olá tooupload pacote.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-230">As you did for hello new application, specify hello **Version** for your new package, browse tooyour **Application package** .zip file, then click **OK** tooupload hello package.</span></span>

### <a name="update-or-delete-an-application-package"></a><span data-ttu-id="3d9d0-231">Atualizar ou excluir um pacote de aplicativos</span><span class="sxs-lookup"><span data-stu-id="3d9d0-231">Update or delete an application package</span></span>
<span data-ttu-id="3d9d0-232">tooupdate ou excluir um pacote de aplicativo existente, folha de detalhes aberta Olá para o aplicativo hello, clique em **pacotes** tooopen Olá **pacotes** folha, clique em Olá **reticências**na linha de saudação saudação do pacote de aplicativo que você deseja toomodify e selecione Olá ação que você deseja tooperform.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-232">tooupdate or delete an existing application package, open hello details blade for hello application, click **Packages** tooopen hello **Packages** blade, click hello **ellipsis** in hello row of hello application package that you want toomodify, and select hello action that you want tooperform.</span></span>

<span data-ttu-id="3d9d0-233">![Atualizar ou excluir pacote no portal do Azure][7]</span><span class="sxs-lookup"><span data-stu-id="3d9d0-233">![Update or delete package in Azure portal][7]</span></span>

<span data-ttu-id="3d9d0-234">**Atualizar**</span><span class="sxs-lookup"><span data-stu-id="3d9d0-234">**Update**</span></span>

<span data-ttu-id="3d9d0-235">Quando você clica em **atualização**, Olá *pacote de atualização* folha é exibida.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-235">When you click **Update**, hello *Update package* blade is displayed.</span></span> <span data-ttu-id="3d9d0-236">Esta folha é semelhante toohello *novo pacote de aplicativo* folha, no entanto, somente o campo seleção do pacote hello estiver habilitado, permitindo que você toospecify um novo tooupload de arquivo ZIP.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-236">This blade is similar toohello *New application package* blade, however only hello package selection field is enabled, allowing you toospecify a new ZIP file tooupload.</span></span>

<span data-ttu-id="3d9d0-237">![Folha do pacote de atualização no portal do Azure][11]</span><span class="sxs-lookup"><span data-stu-id="3d9d0-237">![Update package blade in Azure portal][11]</span></span>

<span data-ttu-id="3d9d0-238">**Excluir**</span><span class="sxs-lookup"><span data-stu-id="3d9d0-238">**Delete**</span></span>

<span data-ttu-id="3d9d0-239">Quando você clica em **excluir**, você será solicitado a exclusão da versão do pacote de saudação Olá tooconfirm e lote exclui o pacote de saudação do armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-239">When you click **Delete**, you are asked tooconfirm hello deletion of hello package version, and Batch deletes hello package from Azure Storage.</span></span> <span data-ttu-id="3d9d0-240">Se você excluir a versão padrão de saudação de um aplicativo, Olá **versão padrão** configuração é removida para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-240">If you delete hello default version of an application, hello **Default version** setting is removed for hello application.</span></span>

<span data-ttu-id="3d9d0-241">![Excluir aplicativo ][12]</span><span class="sxs-lookup"><span data-stu-id="3d9d0-241">![Delete application ][12]</span></span>

## <a name="install-applications-on-compute-nodes"></a><span data-ttu-id="3d9d0-242">Instalar aplicativos em nós de computação</span><span class="sxs-lookup"><span data-stu-id="3d9d0-242">Install applications on compute nodes</span></span>
<span data-ttu-id="3d9d0-243">Agora que você aprendeu como o aplicativo toomanage pacotes com hello portal do Azure, podemos discutir como toodeploy-los toocompute nós e executá-los com as tarefas em lote.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-243">Now that you've learned how toomanage application packages with hello Azure portal, we can discuss how toodeploy them toocompute nodes and run them with Batch tasks.</span></span>

### <a name="install-pool-application-packages"></a><span data-ttu-id="3d9d0-244">Instalar pacotes de aplicativos do pool</span><span class="sxs-lookup"><span data-stu-id="3d9d0-244">Install pool application packages</span></span>
<span data-ttu-id="3d9d0-245">tooinstall um pacote de aplicativo em todos os nós de computação em um pool, especifique um ou mais pacotes de aplicativo *referências* para pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-245">tooinstall an application package on all compute nodes in a pool, specify one or more application package *references* for hello pool.</span></span> <span data-ttu-id="3d9d0-246">pacotes de aplicativos de saudação que você especificar para um pool são instalados em cada nó de computação ao nó une pool hello e ao nó de saudação é reinicializado ou recriar a imagem.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-246">hello application packages that you specify for a pool are installed on each compute node when that node joins hello pool, and when hello node is rebooted or reimaged.</span></span>

<span data-ttu-id="3d9d0-247">No .NET do Lote, especifique um ou mais [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref] quando você criar um novo pool ou para um pool existente.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-247">In Batch .NET, specify one or more [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref] when you create a new pool, or for an existing pool.</span></span> <span data-ttu-id="3d9d0-248">Olá [ApplicationPackageReference] [ net_pkgref] classe especifica uma ID de aplicativo e a versão tooinstall em um pool de nós de computação.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-248">hello [ApplicationPackageReference][net_pkgref] class specifies an application ID and version tooinstall on a pool's compute nodes.</span></span>

```csharp
// Create hello unbound CloudPool
CloudPool myCloudPool =
    batchClient.PoolOperations.CreatePool(
        poolId: "myPool",
        targetDedicatedComputeNodes: 1,
        virtualMachineSize: "small",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

// Specify hello application and version tooinstall on hello compute nodes
myCloudPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "litware",
        Version = "1.1001.2b" }
};

// Commit hello pool so that it's created in hello Batch service. As hello nodes join
// hello pool, hello specified application package is installed on each.
await myCloudPool.CommitAsync();
```

> [!IMPORTANT]
> <span data-ttu-id="3d9d0-249">Se uma implantação de pacote do aplicativo falhar por algum motivo, marcas de serviço de lote Olá Olá nó [inutilizável][net_nodestate], e nenhum tarefas estão agendadas para execução nesse nó.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-249">If an application package deployment fails for any reason, hello Batch service marks hello node [unusable][net_nodestate], and no tasks are scheduled for execution on that node.</span></span> <span data-ttu-id="3d9d0-250">Nesse caso, você deve **reiniciar** Olá implantação de pacote de saudação do nó tooreinitiate.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-250">In this case, you should **restart** hello node tooreinitiate hello package deployment.</span></span> <span data-ttu-id="3d9d0-251">Nó de saudação reiniciar também permite que agendamento de tarefas no nó Olá novamente.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-251">Restarting hello node also enables task scheduling again on hello node.</span></span>
> 
> 

### <a name="install-task-application-packages"></a><span data-ttu-id="3d9d0-252">Instalar pacotes de aplicativos de tarefa</span><span class="sxs-lookup"><span data-stu-id="3d9d0-252">Install task application packages</span></span>
<span data-ttu-id="3d9d0-253">Pool tooa semelhante, que você especifique o pacote de aplicativos *referências* para uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-253">Similar tooa pool, you specify application package *references* for a task.</span></span> <span data-ttu-id="3d9d0-254">Quando uma tarefa está agendada toorun em um nó, pacote de saudação é baixado e extraído antes de linha de comando da tarefa Olá é executada.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-254">When a task is scheduled toorun on a node, hello package is downloaded and extracted just before hello task's command line is executed.</span></span> <span data-ttu-id="3d9d0-255">Se um pacote especificado e a versão já estiver instalado no nó hello, pacote de saudação não é baixado e pacote existente Olá é usado.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-255">If a specified package and version is already installed on hello node, hello package is not downloaded and hello existing package is used.</span></span>

<span data-ttu-id="3d9d0-256">tooinstall um pacote de aplicativo de tarefas, configurar da tarefa Olá [CloudTask][net_cloudtask].[ ApplicationPackageReferences] [ net_cloudtask_pkgref] propriedade:</span><span class="sxs-lookup"><span data-stu-id="3d9d0-256">tooinstall a task application package, configure hello task's [CloudTask][net_cloudtask].[ApplicationPackageReferences][net_cloudtask_pkgref] property:</span></span>

```csharp
CloudTask task =
    new CloudTask(
        "litwaretask001",
        "cmd /c %AZ_BATCH_APP_PACKAGE_LITWARE%\\litware.exe -args -here");

task.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference
    {
        ApplicationId = "litware",
        Version = "1.1001.2b"
    }
};
```

## <a name="execute-hello-installed-applications"></a><span data-ttu-id="3d9d0-257">Executar aplicativos Olá instalado</span><span class="sxs-lookup"><span data-stu-id="3d9d0-257">Execute hello installed applications</span></span>
<span data-ttu-id="3d9d0-258">Hello pacotes que você especificou para uma tarefa ou um pool são baixados e extraídos tooa chamado diretório dentro de saudação `AZ_BATCH_ROOT_DIR` do nó de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-258">hello packages that you've specified for a pool or task are downloaded and extracted tooa named directory within hello `AZ_BATCH_ROOT_DIR` of hello node.</span></span> <span data-ttu-id="3d9d0-259">Lote também cria uma variável de ambiente que contém a saudação caminho toohello chamado de diretório.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-259">Batch also creates an environment variable that contains hello path toohello named directory.</span></span> <span data-ttu-id="3d9d0-260">As linhas de comando da tarefa use essa variável de ambiente ao referenciar o aplicativo hello no nó de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-260">Your task command lines use this environment variable when referencing hello application on hello node.</span></span> 

<span data-ttu-id="3d9d0-261">Em nós do Windows, a variável de saudação está no hello formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="3d9d0-261">On Windows nodes, hello variable is in hello following format:</span></span>

```
Windows:
AZ_BATCH_APP_PACKAGE_APPLICATIONID#version
```

<span data-ttu-id="3d9d0-262">Em nós do Linux, o formato de saudação é ligeiramente diferente.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-262">On Linux nodes, hello format is slightly different.</span></span> <span data-ttu-id="3d9d0-263">Pontos (.), hifens (-) e sinais numéricos (#) são toounderscores bidimensional na variável de ambiente hello.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-263">Periods (.), hypens (-) and number signs (#) are flattened toounderscores in hello environment variable.</span></span> <span data-ttu-id="3d9d0-264">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3d9d0-264">For example:</span></span>

```
Linux:
AZ_BATCH_APP_PACKAGE_APPLICATIONID_version
```

<span data-ttu-id="3d9d0-265">`APPLICATIONID`e `version` são valores que correspondem a toohello aplicativo e a versão do pacote que você especificou para implantação.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-265">`APPLICATIONID` and `version` are values that correspond toohello application and package version you've specified for deployment.</span></span> <span data-ttu-id="3d9d0-266">Por exemplo, se você tiver especificado que a versão 2.7 do aplicativo *blender* devem ser instalados em nós do Windows, as linhas de comando da tarefa usaria essa tooaccess de variável de ambiente seus arquivos:</span><span class="sxs-lookup"><span data-stu-id="3d9d0-266">For example, if you specified that version 2.7 of application *blender* should be installed on Windows nodes, your task command lines would use this environment variable tooaccess its files:</span></span>

```
Windows:
AZ_BATCH_APP_PACKAGE_BLENDER#2.7
```

<span data-ttu-id="3d9d0-267">Em nós do Linux, especifique a variável de ambiente Olá neste formato:</span><span class="sxs-lookup"><span data-stu-id="3d9d0-267">On Linux nodes, specify hello environment variable in this format:</span></span>

```
Linux:
AZ_BATCH_APP_PACKAGE_BLENDER_2_7
``` 

<span data-ttu-id="3d9d0-268">Quando você carrega um pacote de aplicativo, você pode especificar um tooyour de toodeploy de versão do padrão de nós de computação.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-268">When you upload an application package, you can specify a default version toodeploy tooyour compute nodes.</span></span> <span data-ttu-id="3d9d0-269">Se você tiver especificado uma versão padrão para um aplicativo, você pode omitir o sufixo da versão de hello quando você referenciar o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-269">If you have specified a default version for an application, you can omit hello version suffix when you reference hello application.</span></span> <span data-ttu-id="3d9d0-270">Você pode especificar versão do aplicativo saudação padrão em Olá portal do Azure, na folha de aplicativos hello, conforme mostrado no [carregar e gerenciar aplicativos](#upload-and-manage-applications).</span><span class="sxs-lookup"><span data-stu-id="3d9d0-270">You can specify hello default application version in hello Azure portal, on hello Applications blade, as shown in [Upload and manage applications](#upload-and-manage-applications).</span></span>

<span data-ttu-id="3d9d0-271">Por exemplo, se você definir "2.7" como versão padrão de saudação para o aplicativo *blender*e suas tarefas de referenciam Olá variável de ambiente a seguir, os nós do Windows executará a versão 2.7:</span><span class="sxs-lookup"><span data-stu-id="3d9d0-271">For example, if you set "2.7" as hello default version for application *blender*, and your tasks reference hello following environment variable, then your Windows nodes will execute version 2.7:</span></span>

`AZ_BATCH_APP_PACKAGE_BLENDER`

<span data-ttu-id="3d9d0-272">Olá, trecho de código a seguir mostra uma linha de comando do exemplo tarefa que inicia a versão padrão Olá Olá *blender* aplicativo:</span><span class="sxs-lookup"><span data-stu-id="3d9d0-272">hello following code snippet shows an example task command line that launches hello default version of hello *blender* application:</span></span>

```csharp
string taskId = "blendertask01";
string commandLine =
    @"cmd /c %AZ_BATCH_APP_PACKAGE_BLENDER%\blender.exe -args -here";
CloudTask blenderTask = new CloudTask(taskId, commandLine);
```

> [!TIP]
> <span data-ttu-id="3d9d0-273">Consulte [configurações de ambiente para tarefas](batch-api-basics.md#environment-settings-for-tasks) em Olá [visão geral do recurso de lote](batch-api-basics.md) para obter mais informações sobre configurações de ambiente do nó de computação.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-273">See [Environment settings for tasks](batch-api-basics.md#environment-settings-for-tasks) in hello [Batch feature overview](batch-api-basics.md) for more information about compute node environment settings.</span></span>
> 
> 

## <a name="update-a-pools-application-packages"></a><span data-ttu-id="3d9d0-274">Atualizar pacotes de aplicativos de um pool</span><span class="sxs-lookup"><span data-stu-id="3d9d0-274">Update a pool's application packages</span></span>
<span data-ttu-id="3d9d0-275">Se um pool existente já tiver sido configurado com um pacote de aplicativo, você pode especificar um novo pacote para o pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-275">If an existing pool has already been configured with an application package, you can specify a new package for hello pool.</span></span> <span data-ttu-id="3d9d0-276">Se você especificar uma nova referência de pacote para um pool, Olá aplicar a seguir:</span><span class="sxs-lookup"><span data-stu-id="3d9d0-276">If you specify a new package reference for a pool, hello following apply:</span></span>

* <span data-ttu-id="3d9d0-277">Olá serviço de lote instala o pacote de especificado mais recentemente de saudação em todos os nós que unem pool hello e em qualquer nó existente que é reinicializado ou recriar a imagem.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-277">hello Batch service installs hello newly specified package on all new nodes that join hello pool and on any existing node that is rebooted or reimaged.</span></span>
* <span data-ttu-id="3d9d0-278">Computação nós que já estão no pool hello quando você atualizar referências de pacote de saudação não instalam automaticamente o novo pacote de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-278">Compute nodes that are already in hello pool when you update hello package references do not automatically install hello new application package.</span></span> <span data-ttu-id="3d9d0-279">Esses computação nós devem ser reinicializados ou imagem recriada tooreceive Olá novo pacote.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-279">These compute nodes must be rebooted or reimaged tooreceive hello new package.</span></span>
* <span data-ttu-id="3d9d0-280">Quando um novo pacote é implantado, Olá criar variáveis de ambiente refletem novas referências de pacote de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-280">When a new package is deployed, hello created environment variables reflect hello new application package references.</span></span>

<span data-ttu-id="3d9d0-281">Neste exemplo, pool existente Olá tem versão 2.7 do hello *blender* aplicativo configurado como um de seus [CloudPool][net_cloudpool].[ ApplicationPackageReferences][net_cloudpool_pkgref].</span><span class="sxs-lookup"><span data-stu-id="3d9d0-281">In this example, hello existing pool has version 2.7 of hello *blender* application configured as one of its [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref].</span></span> <span data-ttu-id="3d9d0-282">nós do pool de saudação tooupdate com a versão 2.76b, especifique um novo [ApplicationPackageReference] [ net_pkgref] com hello nova versão e alterações de saudação de confirmação.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-282">tooupdate hello pool's nodes with version 2.76b, specify a new [ApplicationPackageReference][net_pkgref] with hello new version, and commit hello change.</span></span>

```csharp
string newVersion = "2.76b";
CloudPool boundPool = await batchClient.PoolOperations.GetPoolAsync("myPool");
boundPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "blender",
        Version = newVersion }
};
await boundPool.CommitAsync();
```

<span data-ttu-id="3d9d0-283">Agora que hello nova versão tiver sido configurado, Olá serviço de lote instala a versão 2.76b tooany *novo* nó que une Olá pool.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-283">Now that hello new version has been configured, hello Batch service installs version 2.76b tooany *new* node that joins hello pool.</span></span> <span data-ttu-id="3d9d0-284">tooinstall 2.76b em nós Olá *já* no pool de hello, reinicializar ou refazer imagem-los.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-284">tooinstall 2.76b on hello nodes that are *already* in hello pool, reboot or reimage them.</span></span> <span data-ttu-id="3d9d0-285">Observe que nós reinicializada mantenham arquivos Olá de implantações de pacote anterior.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-285">Note that rebooted nodes retain hello files from previous package deployments.</span></span>

## <a name="list-hello-applications-in-a-batch-account"></a><span data-ttu-id="3d9d0-286">Lista de aplicativos de saudação em uma conta de lote</span><span class="sxs-lookup"><span data-stu-id="3d9d0-286">List hello applications in a Batch account</span></span>
<span data-ttu-id="3d9d0-287">Você pode listar aplicativos hello e seus pacotes em uma conta de lote usando Olá [ApplicationOperations][net_appops].[ ListApplicationSummaries] [ net_appops_listappsummaries] método.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-287">You can list hello applications and their packages in a Batch account by using hello [ApplicationOperations][net_appops].[ListApplicationSummaries][net_appops_listappsummaries] method.</span></span>

```csharp
// List hello applications and their application packages in hello Batch account.
List<ApplicationSummary> applications = await batchClient.ApplicationOperations.ListApplicationSummaries().ToListAsync();
foreach (ApplicationSummary app in applications)
{
    Console.WriteLine("ID: {0} | Display Name: {1}", app.Id, app.DisplayName);

    foreach (string version in app.Versions)
    {
        Console.WriteLine("  {0}", version);
    }
}
```

## <a name="wrap-up"></a><span data-ttu-id="3d9d0-288">Conclusão</span><span class="sxs-lookup"><span data-stu-id="3d9d0-288">Wrap up</span></span>
<span data-ttu-id="3d9d0-289">Com pacotes de aplicativos, você pode ajudar seus clientes selecione Olá aplicativos para seus trabalhos e especifique Olá versão exata toouse durante o processamento de trabalhos com o serviço de lote habilitado.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-289">With application packages, you can help your customers select hello applications for their jobs and specify hello exact version toouse when processing jobs with your Batch-enabled service.</span></span> <span data-ttu-id="3d9d0-290">Você também pode fornecer capacidade Olá para tooupload seus clientes e controlar seus próprios aplicativos em seu serviço.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-290">You might also provide hello ability for your customers tooupload and track their own applications in your service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d9d0-291">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3d9d0-291">Next steps</span></span>
* <span data-ttu-id="3d9d0-292">Olá [API REST do lote] [ api_rest] também fornece suporte toowork com pacotes de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-292">hello [Batch REST API][api_rest] also provides support toowork with application packages.</span></span> <span data-ttu-id="3d9d0-293">Por exemplo, consulte Olá [applicationPackageReferences] [ rest_add_pool_with_packages] elemento [adicionar uma conta do pool de tooan] [ rest_add_pool] para obter informações sobre como toospecify tooinstall de pacotes usando Olá API REST.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-293">For example, see hello [applicationPackageReferences][rest_add_pool_with_packages] element in [Add a pool tooan account][rest_add_pool] for information about how toospecify packages tooinstall by using hello REST API.</span></span> <span data-ttu-id="3d9d0-294">Consulte [aplicativos] [ rest_applications] para obter detalhes sobre como informações do aplicativo tooobtain usando Olá API REST do lote.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-294">See [Applications][rest_applications] for details about how tooobtain application information by using hello Batch REST API.</span></span>
* <span data-ttu-id="3d9d0-295">Saiba como tooprogrammatically [gerenciar contas de lote do Azure e cotas com o Batch Management .NET](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="3d9d0-295">Learn how tooprogrammatically [manage Azure Batch accounts and quotas with Batch Management .NET](batch-management-dotnet.md).</span></span> <span data-ttu-id="3d9d0-296">Olá [Batch Management .NET][api_net_mgmt] biblioteca pode habilitar os recursos de criação e exclusão de conta para o lote de aplicativo ou serviço.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-296">hello [Batch Management .NET][api_net_mgmt] library can enable account creation and deletion features for your Batch application or service.</span></span>

[api_net]: https://docs.microsoft.com/dotnet/api/overview/azure/batch/client?view=azure-dotnet
[api_net_mgmt]: https://docs.microsoft.com/dotnet/api/overview/azure/batch/management?view=azure-dotnet
[api_rest]: https://docs.microsoft.com/en-us/rest/api/batchservice/
[batch_mgmt_nuget]: https://www.nuget.org/packages/Microsoft.Azure.Management.Batch/
[github_samples]: https://github.com/Azure/azure-batch-samples
[storage_pricing]: https://azure.microsoft.com/pricing/details/storage/
[net_appops]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationoperations.aspx
[net_appops_listappsummaries]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationoperations.listapplicationsummaries.aspx
[net_cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_cloudpool_pkgref]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.applicationpackagereferences.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudtask.aspx
[net_cloudtask_pkgref]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudtask.applicationpackagereferences.aspx
[net_nodestate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.state.aspx
[net_pkgref]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationpackagereference.aspx
[portal]: https://portal.azure.com
[rest_applications]: https://msdn.microsoft.com/library/azure/mt643945.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[rest_add_pool_with_packages]: https://msdn.microsoft.com/library/azure/dn820174.aspx#bk_apkgreference

[1]: ./media/batch-application-packages/app_pkg_01.png "Diagrama de alto nível de pacotes de aplicativos"
[2]: ./media/batch-application-packages/app_pkg_02.png "Bloco Aplicativos no portal do Azure"
[3]: ./media/batch-application-packages/app_pkg_03.png "Folha Aplicativos no portal do Azure"
[4]: ./media/batch-application-packages/app_pkg_04.png "Folha Detalhes do aplicativo no portal do Azure"
[5]: ./media/batch-application-packages/app_pkg_05.png "Folha Novo aplicativo no portal do Azure"
[7]: ./media/batch-application-packages/app_pkg_07.png "Menu suspenso Atualizar ou excluir pacotes no portal do Azure"
[8]: ./media/batch-application-packages/app_pkg_08.png "Folha Novo pacote de aplicativos no portal do Azure"
[9]: ./media/batch-application-packages/app_pkg_09.png "Alerta Nenhuma conta de armazenamento vinculada"
[10]: ./media/batch-application-packages/app_pkg_10.png "Folha Escolher conta de armazenamento no portal do Azure"
[11]: ./media/batch-application-packages/app_pkg_11.png "Folha do pacote de atualização no portal do Azure"
[12]: ./media/batch-application-packages/app_pkg_12.png "Caixa de diálogo de confirmação Excluir pacote no portal do Azure"
