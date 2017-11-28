---
title: "Instalar pacotes de aplicativos em nós de computação - Azure Batch | Microsoft Docs"
description: "Use o recurso de pacotes de aplicativos do Lote do Azure para gerenciar facilmente vários aplicativos e versões para instalação nos nós de computação do Lote."
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
ms.openlocfilehash: afcc04c80ec15872a22de5d5969a7ef6a583562f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-applications-to-compute-nodes-with-batch-application-packages"></a><span data-ttu-id="43c6a-103">Implantar aplicativos em nós de computação com pacotes de aplicativos do Lote</span><span class="sxs-lookup"><span data-stu-id="43c6a-103">Deploy applications to compute nodes with Batch application packages</span></span>

<span data-ttu-id="43c6a-104">O recurso de pacotes de aplicativos do Lote do Azure fornece um fácil gerenciamento dos aplicativos de tarefa e sua implantação para os nós de computação em seu pool.</span><span class="sxs-lookup"><span data-stu-id="43c6a-104">The application packages feature of Azure Batch provides easy management of task applications and their deployment to the compute nodes in your pool.</span></span> <span data-ttu-id="43c6a-105">Com os pacotes de aplicativos, você pode carregar e gerenciar diversas versões dos aplicativos que suas tarefas executam, incluindo seus arquivos de suporte.</span><span class="sxs-lookup"><span data-stu-id="43c6a-105">With application packages, you can upload and manage multiple versions of the applications your tasks run, including their supporting files.</span></span> <span data-ttu-id="43c6a-106">Você pode implantar automaticamente um ou mais desses aplicativos nos nós de computação em seu pool.</span><span class="sxs-lookup"><span data-stu-id="43c6a-106">You can then automatically deploy one or more of these applications to the compute nodes in your pool.</span></span>

<span data-ttu-id="43c6a-107">Neste artigo, você aprenderá como carregar e gerenciar os pacotes de aplicativos usando o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="43c6a-107">In this article, you will learn how to upload and manage application packages in the Azure portal.</span></span> <span data-ttu-id="43c6a-108">Em seguida, aprenderá como instalá-los nos nós de computação de um pool com a biblioteca [.NET do Lote][api_net].</span><span class="sxs-lookup"><span data-stu-id="43c6a-108">You will then learn how to install them on a pool's compute nodes with the [Batch .NET][api_net] library.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="43c6a-109">Os pacotes de aplicativos têm suporte em todos os pools do Lote criados após 5 de julho de 2017.</span><span class="sxs-lookup"><span data-stu-id="43c6a-109">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="43c6a-110">Elas só terão suporte em pools do Lote criados entre 10 de março de 2016 e 5 de julho de 2017 se o pool tiver sido criado usando uma configuração de Serviço de Nuvem.</span><span class="sxs-lookup"><span data-stu-id="43c6a-110">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if the pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="43c6a-111">Os pools do Lote criados antes de 10 de março de 2016 não dão suporte a pacotes de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="43c6a-111">Batch pools created prior to 10 March 2016 do not support application packages.</span></span>
>
> <span data-ttu-id="43c6a-112">As APIs para criar e gerenciar pacotes de aplicativos fazem parte da biblioteca [Batch Management .NET][[api_net_mgmt]].</span><span class="sxs-lookup"><span data-stu-id="43c6a-112">The APIs for creating and managing application packages are part of the [Batch Management .NET][[api_net_mgmt]] library.</span></span> <span data-ttu-id="43c6a-113">As APIs para instalar pacotes de aplicativos em um nó de computação fazem parte da biblioteca [Batch .NET][api_net].</span><span class="sxs-lookup"><span data-stu-id="43c6a-113">The APIs for installing application packages on a compute node are part of the [Batch .NET][api_net] library.</span></span>  
>
> <span data-ttu-id="43c6a-114">O recurso de pacotes de aplicativos descrito aqui substitui o recurso Aplicativos do Lote, disponível nas versões anteriores do serviço.</span><span class="sxs-lookup"><span data-stu-id="43c6a-114">The application packages feature described here supersedes the Batch Apps feature available in previous versions of the service.</span></span>
> 
> 

## <a name="application-package-requirements"></a><span data-ttu-id="43c6a-115">Requisitos do pacote de aplicativos</span><span class="sxs-lookup"><span data-stu-id="43c6a-115">Application package requirements</span></span>
<span data-ttu-id="43c6a-116">Para usar pacotes de aplicativos, você deve [vincular uma conta de Armazenamento do Azure](#link-a-storage-account) à sua conta do Lote.</span><span class="sxs-lookup"><span data-stu-id="43c6a-116">To use application packages, you need to [link an Azure Storage account](#link-a-storage-account) to your Batch account.</span></span>

<span data-ttu-id="43c6a-117">Esse recurso foi introduzido na [API REST do Lote][api_rest] versão 2015-12-01.2.2 e na biblioteca [.NET do Lote][api_net] correspondente, versão 3.1.0.</span><span class="sxs-lookup"><span data-stu-id="43c6a-117">This feature was introduced in [Batch REST API][api_rest] version 2015-12-01.2.2 and the corresponding [Batch .NET][api_net] library version 3.1.0.</span></span> <span data-ttu-id="43c6a-118">É recomendável sempre usar a versão da API mais recente ao trabalhar com o Lote.</span><span class="sxs-lookup"><span data-stu-id="43c6a-118">We recommend that you always use the latest API version when working with Batch.</span></span>

> [!NOTE]
> <span data-ttu-id="43c6a-119">Os pacotes de aplicativos têm suporte em todos os pools do Lote criados após 5 de julho de 2017.</span><span class="sxs-lookup"><span data-stu-id="43c6a-119">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="43c6a-120">Elas só terão suporte em pools do Lote criados entre 10 de março de 2016 e 5 de julho de 2017 se o pool tiver sido criado usando uma configuração de Serviço de Nuvem.</span><span class="sxs-lookup"><span data-stu-id="43c6a-120">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if the pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="43c6a-121">Os pools do Lote criados antes de 10 de março de 2016 não dão suporte a pacotes de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="43c6a-121">Batch pools created prior to 10 March 2016 do not support application packages.</span></span>
>
>

## <a name="about-applications-and-application-packages"></a><span data-ttu-id="43c6a-122">Sobre aplicativos e pacotes de aplicativos</span><span class="sxs-lookup"><span data-stu-id="43c6a-122">About applications and application packages</span></span>
<span data-ttu-id="43c6a-123">No Lote do Azure, um *aplicativo* refere-se a um conjunto de binários com versão que podem ser baixados automaticamente para os nós de computação no pool.</span><span class="sxs-lookup"><span data-stu-id="43c6a-123">Within Azure Batch, an *application* refers to a set of versioned binaries that can be automatically downloaded to the compute nodes in your pool.</span></span> <span data-ttu-id="43c6a-124">Um *pacote de aplicativos* refere-se a um *conjunto específico* desses binários e representa uma determinada *versão* do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="43c6a-124">An *application package* refers to a *specific set* of those binaries and represents a given *version* of the application.</span></span>

<span data-ttu-id="43c6a-125">![Diagrama de alto nível de aplicativos e pacotes de aplicativos][1]</span><span class="sxs-lookup"><span data-stu-id="43c6a-125">![High-level diagram of applications and application packages][1]</span></span>

### <a name="applications"></a><span data-ttu-id="43c6a-126">Aplicativos</span><span class="sxs-lookup"><span data-stu-id="43c6a-126">Applications</span></span>
<span data-ttu-id="43c6a-127">Um aplicativo no Lote contém um ou mais pacotes de aplicativos e especifica as opções de configuração para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="43c6a-127">An application in Batch contains one or more application packages and specifies configuration options for the application.</span></span> <span data-ttu-id="43c6a-128">Por exemplo, um aplicativo pode especificar a versão do pacote de aplicativos padrão para instalar nos nós de computação e se seus pacotes podem ser atualizados ou excluídos.</span><span class="sxs-lookup"><span data-stu-id="43c6a-128">For example, an application can specify the default application package version to install on compute nodes and whether its packages can be updated or deleted.</span></span>

### <a name="application-packages"></a><span data-ttu-id="43c6a-129">pacotes de aplicativos</span><span class="sxs-lookup"><span data-stu-id="43c6a-129">Application packages</span></span>
<span data-ttu-id="43c6a-130">Um pacote de aplicativos é um arquivo .zip contendo os binários de aplicativo e arquivos de suporte exigidos para que suas tarefas executem o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="43c6a-130">An application package is a .zip file that contains the application binaries and supporting files that are required for your tasks to run the application.</span></span> <span data-ttu-id="43c6a-131">Cada pacote de aplicativos representa uma versão específica do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="43c6a-131">Each application package represents a specific version of the application.</span></span>

<span data-ttu-id="43c6a-132">Você pode especificar os pacotes de aplicativos no nível do pool e no de tarefa.</span><span class="sxs-lookup"><span data-stu-id="43c6a-132">You can specify application packages at the pool and task levels.</span></span> <span data-ttu-id="43c6a-133">Você pode especificar um ou mais desses pacotes e (opcionalmente) uma versão quando você cria uma tarefa ou um pool.</span><span class="sxs-lookup"><span data-stu-id="43c6a-133">You can specify one or more of these packages and (optionally) a version when you create a pool or task.</span></span>

* <span data-ttu-id="43c6a-134">**Pacotes de aplicativos do pool** são implantados em *cada* nó no pool.</span><span class="sxs-lookup"><span data-stu-id="43c6a-134">**Pool application packages** are deployed to *every* node in the pool.</span></span> <span data-ttu-id="43c6a-135">Os aplicativos são implantados quando um nó ingressa em um pool e quando ele é reinicializado ou tem a imagem recriada.</span><span class="sxs-lookup"><span data-stu-id="43c6a-135">Applications are deployed when a node joins a pool, and when it is rebooted or reimaged.</span></span>
  
    <span data-ttu-id="43c6a-136">Os pacotes de aplicativos do pool são adequados quando todos os nós em um pool executam as tarefas de um trabalho.</span><span class="sxs-lookup"><span data-stu-id="43c6a-136">Pool application packages are appropriate when all nodes in a pool execute a job's tasks.</span></span> <span data-ttu-id="43c6a-137">Você pode especificar um ou mais pacotes de aplicativos quando cria um pool e pode adicionar ou atualizar os pacotes de um pool existente.</span><span class="sxs-lookup"><span data-stu-id="43c6a-137">You can specify one or more application packages when you create a pool, and you can add or update an existing pool's packages.</span></span> <span data-ttu-id="43c6a-138">Se você atualizar os pacotes de aplicativos de um pool existente, deverá reiniciar os nós para instalar o novo pacote.</span><span class="sxs-lookup"><span data-stu-id="43c6a-138">If you update an existing pool's application packages, you must restart its nodes to install the new package.</span></span>
* <span data-ttu-id="43c6a-139">**pacotes de aplicativos de tarefa** são implantados somente em um nó de computação programado para executar uma tarefa, logo antes de executar a linha de comando da tarefa.</span><span class="sxs-lookup"><span data-stu-id="43c6a-139">**Task application packages** are deployed only to a compute node scheduled to run a task, just before running the task's command line.</span></span> <span data-ttu-id="43c6a-140">Se o pacote de aplicativos especificado e a versão já estiverem no nó, ele não será reimplantado e o pacote existente será usado.</span><span class="sxs-lookup"><span data-stu-id="43c6a-140">If the specified application package and version is already on the node, it is not redeployed and the existing package is used.</span></span>
  
    <span data-ttu-id="43c6a-141">Os pacotes de aplicativos de tarefa são úteis nos ambientes de pool compartilhado, onde diferentes trabalhos são executados em um pool, e o pool não é excluído quando um trabalho é concluído.</span><span class="sxs-lookup"><span data-stu-id="43c6a-141">Task application packages are useful in shared-pool environments, where different jobs are run on one pool, and the pool is not deleted when a job is completed.</span></span> <span data-ttu-id="43c6a-142">Se o trabalho tiver menos tarefas do que os nós no pool, pacotes de aplicativos de tarefa poderão minimizar a transferência de dados, pois o aplicativo é implantado apenas para os nós que executam tarefas.</span><span class="sxs-lookup"><span data-stu-id="43c6a-142">If your job has fewer tasks than nodes in the pool, task application packages can minimize data transfer since your application is deployed only to the nodes that run tasks.</span></span>
  
    <span data-ttu-id="43c6a-143">Outros cenários que podem aproveitar os pacotes de aplicativos de tarefa são os trabalhos que executam um aplicativo grande, mas para um pequeno número de tarefas.</span><span class="sxs-lookup"><span data-stu-id="43c6a-143">Other scenarios that can benefit from task application packages are jobs that run a large application, but for only a few tasks.</span></span> <span data-ttu-id="43c6a-144">Por exemplo, uma fase de pré-processamento ou uma tarefa de mesclagem na qual o aplicativo pré-processamento ou mesclagem é pesado pode beneficiar-se do uso de pacotes de aplicativos de tarefa.</span><span class="sxs-lookup"><span data-stu-id="43c6a-144">For example, a pre-processing stage or a merge task, where the pre-processing or merge application is heavyweight, may benefit from using task application packages.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="43c6a-145">Há restrições ao número de aplicativos e pacotes de aplicativos em uma conta do Lote, bem como ao tamanho máximo do pacote de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="43c6a-145">There are restrictions on the number of applications and application packages within a Batch account and on the maximum application package size.</span></span> <span data-ttu-id="43c6a-146">Consulte [Cotas e limites para o serviço do Lote do Azure](batch-quota-limit.md) para obter detalhes sobre esses limites.</span><span class="sxs-lookup"><span data-stu-id="43c6a-146">See [Quotas and limits for the Azure Batch service](batch-quota-limit.md) for details about these limits.</span></span>
> 
> 

### <a name="benefits-of-application-packages"></a><span data-ttu-id="43c6a-147">Benefícios dos pacotes de aplicativos</span><span class="sxs-lookup"><span data-stu-id="43c6a-147">Benefits of application packages</span></span>
<span data-ttu-id="43c6a-148">Os pacotes de aplicativos podem simplificar o código em sua solução de Lote e reduzir a sobrecarga exigida para gerenciar os aplicativos que suas tarefas executam.</span><span class="sxs-lookup"><span data-stu-id="43c6a-148">Application packages can simplify the code in your Batch solution and lower the overhead required to manage the applications that your tasks run.</span></span>

<span data-ttu-id="43c6a-149">Com pacotes de aplicativos, a tarefa de inicialização do pool não precisa especificar uma longa lista de arquivos de recursos individuais para instalar nos nós.</span><span class="sxs-lookup"><span data-stu-id="43c6a-149">With application packages, your pool's start task doesn't have to specify a long list of individual resource files to install on the nodes.</span></span> <span data-ttu-id="43c6a-150">Não é preciso gerenciar manualmente diversas versões dos arquivos do aplicativo no Armazenamento do Azure nem em seus nós.</span><span class="sxs-lookup"><span data-stu-id="43c6a-150">You don't have to manually manage multiple versions of your application files in Azure Storage, or on your nodes.</span></span> <span data-ttu-id="43c6a-151">E você não precisa preocupar-se com a geração de [URLs SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md) para fornecer acesso aos arquivos em sua conta de Armazenamento.</span><span class="sxs-lookup"><span data-stu-id="43c6a-151">And, you don't need to worry about generating [SAS URLs](../storage/common/storage-dotnet-shared-access-signature-part-1.md) to provide access to the files in your Storage account.</span></span> <span data-ttu-id="43c6a-152">O Lote funciona em segundo plano com o Armazenamento do Azure para armazenar os pacotes de aplicativos e implantá-los nos nós de computação.</span><span class="sxs-lookup"><span data-stu-id="43c6a-152">Batch works in the background with Azure Storage to store application packages and deploy them to compute nodes.</span></span>

> [!NOTE] 
> <span data-ttu-id="43c6a-153">O tamanho total de uma tarefa de início deve ser menor ou igual a 32768 caracteres, incluindo arquivos de recurso e variáveis de ambiente.</span><span class="sxs-lookup"><span data-stu-id="43c6a-153">The total size of a start task must be less than or equal to 32768 characters, including resource files and environment variables.</span></span> <span data-ttu-id="43c6a-154">Se a tarefa de inicialização exceder esse limite, usar pacotes de aplicativos é outra opção.</span><span class="sxs-lookup"><span data-stu-id="43c6a-154">If your start task exceeds this limit, then using application packages is another option.</span></span> <span data-ttu-id="43c6a-155">Você pode também criar um arquivo compactado contendo os arquivos de recurso, carregá-lo como um blob no armazenamento do Azure e descompactá-lo na linha de comando da tarefa inicial.</span><span class="sxs-lookup"><span data-stu-id="43c6a-155">You can also create a zipped archive containing your resource files, upload it as a blob to Azure Storage, and then unzip it from the command line of your start task.</span></span> 
>
>

## <a name="upload-and-manage-applications"></a><span data-ttu-id="43c6a-156">Carregar e gerenciar aplicativos</span><span class="sxs-lookup"><span data-stu-id="43c6a-156">Upload and manage applications</span></span>
<span data-ttu-id="43c6a-157">Você pode usar o [Portal do Azure][portal] ou a biblioteca [.NET de Gerenciamento do Lote](batch-management-dotnet.md) para gerenciar os pacotes de aplicativos em sua conta do Lote.</span><span class="sxs-lookup"><span data-stu-id="43c6a-157">You can use the [Azure portal][portal] or the [Batch Management .NET](batch-management-dotnet.md) library to manage the application packages in your Batch account.</span></span> <span data-ttu-id="43c6a-158">Nas próximas seções, primeiro vincularemos uma conta de Armazenamento e analisaremos como adicionar aplicativos e pacotes e como gerenciá-los com o portal.</span><span class="sxs-lookup"><span data-stu-id="43c6a-158">In the next few sections, we first show how to link a Storage account, then discuss adding applications and packages and managing them with the portal.</span></span>

### <a name="link-a-storage-account"></a><span data-ttu-id="43c6a-159">Vincular uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="43c6a-159">Link a Storage account</span></span>
<span data-ttu-id="43c6a-160">Para usar pacotes de aplicativos, em primeiro lugar, você deve vincular uma conta de armazenamento do Azure à sua conta do Lote.</span><span class="sxs-lookup"><span data-stu-id="43c6a-160">To use application packages, you must first link an Azure Storage account to your Batch account.</span></span> <span data-ttu-id="43c6a-161">Se você ainda não configurou uma conta de Armazenamento, o portal do Azure exibe um aviso na primeira vez em que clicar no bloco **Aplicativos** na folha **Conta do Lote**.</span><span class="sxs-lookup"><span data-stu-id="43c6a-161">If you have not yet configured a Storage account, the Azure portal displays a warning the first time you click the **Applications** tile in the **Batch account** blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="43c6a-162">No momento, o Lote dá suporte *somente* ao tipo de conta de armazenamento de **Uso geral**, conforme descrito na etapa 5 [Criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account) em [Sobre as contas de armazenamento do Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="43c6a-162">Batch currently supports *only* the **General-purpose** storage account type as described in step 5, [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account), in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="43c6a-163">Ao vincular uma conta de Armazenamento do Azure à sua conta do Lote, você vincula *somente* uma conta de armazenamento de **Finalidade geral**.</span><span class="sxs-lookup"><span data-stu-id="43c6a-163">When you link an Azure Storage account to your Batch account, link *only* a **General-purpose** storage account.</span></span>
> 
> 

<span data-ttu-id="43c6a-164">![Aviso de 'Nenhuma conta de armazenamento configurada' no portal do Azure][9]</span><span class="sxs-lookup"><span data-stu-id="43c6a-164">!['No storage account configured' warning in Azure portal][9]</span></span>

<span data-ttu-id="43c6a-165">O serviço de Lote usa a conta de Armazenamento associada para armazenar os pacotes de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="43c6a-165">The Batch service uses the associated Storage account to store your application packages.</span></span> <span data-ttu-id="43c6a-166">Depois que você tiver vinculado as duas contas, o Lote poderá implantar automaticamente os pacotes armazenados na conta de armazenamento vinculada nos nós de computação.</span><span class="sxs-lookup"><span data-stu-id="43c6a-166">After you've linked the two accounts, Batch can automatically deploy the packages stored in the linked Storage account to your compute nodes.</span></span> <span data-ttu-id="43c6a-167">Para vincular uma conta de armazenamento à sua conta do Lote, clique em **Configurações da conta de armazenamento** na folha **Aviso** e clique em **Conta de Armazenamento** na folha **Conta de Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="43c6a-167">To link a Storage account to your Batch account, click **Storage account settings** on the **Warning** blade, and then click **Storage Account** on the **Storage Account** blade.</span></span>

<span data-ttu-id="43c6a-168">![Folha Escolher conta de armazenamento no portal do Azure][10]</span><span class="sxs-lookup"><span data-stu-id="43c6a-168">![Choose storage account blade in Azure portal][10]</span></span>

<span data-ttu-id="43c6a-169">Recomendamos que você crie uma conta de armazenamento para usar *especificamente* com sua conta do Lote e que a selecione aqui.</span><span class="sxs-lookup"><span data-stu-id="43c6a-169">We recommend that you create a Storage account *specifically* for use with your Batch account, and select it here.</span></span> <span data-ttu-id="43c6a-170">Para obter detalhes sobre como criar uma conta de armazenamento, consulte "Criar uma Conta de Armazenamento" em [Sobre contas de Armazenamento do Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="43c6a-170">For details about how to create a storage account, see "Create a Storage account" in [About Azure Storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="43c6a-171">Depois de ter criado uma conta de Armazenamento, você poderá vinculá-la à sua conta do Lote usando a folha **Conta de Armazenamento** .</span><span class="sxs-lookup"><span data-stu-id="43c6a-171">After you've created a Storage account, you can then link it to your Batch account by using the **Storage Account** blade.</span></span>

> [!WARNING]
> <span data-ttu-id="43c6a-172">O serviço de Lote usa o Armazenamento do Azure para armazenar os pacotes de aplicativos como blobs de blocos.</span><span class="sxs-lookup"><span data-stu-id="43c6a-172">The Batch service uses Azure Storage to store your application packages as block blobs.</span></span> <span data-ttu-id="43c6a-173">Você é [cobrado normalmente][storage_pricing] pelos dados de blob de blocos.</span><span class="sxs-lookup"><span data-stu-id="43c6a-173">You are [charged as normal][storage_pricing] for the block blob data.</span></span> <span data-ttu-id="43c6a-174">Não se esqueça de considerar o tamanho e o número de pacotes de aplicativos e, periodicamente, remova pacotes preteridos para minimizar o custo.</span><span class="sxs-lookup"><span data-stu-id="43c6a-174">Be sure to consider the size and number of your application packages, and periodically remove deprecated packages to minimize costs.</span></span>
> 
> 

### <a name="view-current-applications"></a><span data-ttu-id="43c6a-175">Exibir aplicativos atuais</span><span class="sxs-lookup"><span data-stu-id="43c6a-175">View current applications</span></span>
<span data-ttu-id="43c6a-176">Para exibir os aplicativos em sua conta do Lote, clique no item de menu **Aplicativos** no menu à esquerda enquanto exibe a folha **Conta do Lote**.</span><span class="sxs-lookup"><span data-stu-id="43c6a-176">To view the applications in your Batch account, click the **Applications** menu item in the left menu while viewing the **Batch account** blade.</span></span>

<span data-ttu-id="43c6a-177">![Bloco Aplicativos][2]</span><span class="sxs-lookup"><span data-stu-id="43c6a-177">![Applications tile][2]</span></span>

<span data-ttu-id="43c6a-178">Selecionar essa opção de menu abre a folha **Aplicativos**:</span><span class="sxs-lookup"><span data-stu-id="43c6a-178">Selecting this menu option opens the **Applications** blade:</span></span>

<span data-ttu-id="43c6a-179">![Listar aplicativos][3]</span><span class="sxs-lookup"><span data-stu-id="43c6a-179">![List applications][3]</span></span>

<span data-ttu-id="43c6a-180">A folha **Aplicativos** exibe a ID de cada aplicativo em sua conta e as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="43c6a-180">The **Applications** blade displays the ID of each application in your account and the following properties:</span></span>

* <span data-ttu-id="43c6a-181">**Pacotes**: o número de versões associadas a este aplicativo.</span><span class="sxs-lookup"><span data-stu-id="43c6a-181">**Packages**: The number of versions associated with this application.</span></span>
* <span data-ttu-id="43c6a-182">**Versão padrão**: a versão do aplicativo que será instalada se você não indicar uma versão ao especificar o aplicativo para um pool.</span><span class="sxs-lookup"><span data-stu-id="43c6a-182">**Default version**: The application version installed if you do not indicate a version when you specify the application for a pool.</span></span> <span data-ttu-id="43c6a-183">Essa configuração é opcional.</span><span class="sxs-lookup"><span data-stu-id="43c6a-183">This setting is optional.</span></span>
* <span data-ttu-id="43c6a-184">**Permitir atualizações**: o valor que especifica se são permitidas as atualizações, exclusões e adições do pacote.</span><span class="sxs-lookup"><span data-stu-id="43c6a-184">**Allow updates**: The value that specifies whether package updates, deletions, and additions are allowed.</span></span> <span data-ttu-id="43c6a-185">Se isso estiver definido para **Não**, as exclusões e atualizações do pacote ficarão desabilitadas para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="43c6a-185">If this is set to **No**, package updates and deletions are disabled for the application.</span></span> <span data-ttu-id="43c6a-186">Apenas novas versões do pacote de aplicativos poderão ser adicionadas.</span><span class="sxs-lookup"><span data-stu-id="43c6a-186">Only new application package versions can be added.</span></span> <span data-ttu-id="43c6a-187">O padrão é **Sim**.</span><span class="sxs-lookup"><span data-stu-id="43c6a-187">The default is **Yes**.</span></span>

### <a name="view-application-details"></a><span data-ttu-id="43c6a-188">Exibir detalhes do aplicativo</span><span class="sxs-lookup"><span data-stu-id="43c6a-188">View application details</span></span>
<span data-ttu-id="43c6a-189">Clique em um aplicativo na folha **Aplicativos** para abrir a folha que inclui os detalhes desse aplicativo.</span><span class="sxs-lookup"><span data-stu-id="43c6a-189">To open the blade that includes the details for an application, select the application in the **Applications** blade.</span></span>

<span data-ttu-id="43c6a-190">![Detalhes do aplicativo][4]</span><span class="sxs-lookup"><span data-stu-id="43c6a-190">![Application details][4]</span></span>

<span data-ttu-id="43c6a-191">Na folha de detalhes do aplicativo, você pode configurar as definições a seguir para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="43c6a-191">In the application details blade, you can configure the following settings for your application.</span></span>

* <span data-ttu-id="43c6a-192">**Permitir atualizações**: especifique se seus pacotes de aplicativos podem ser atualizados ou excluídos.</span><span class="sxs-lookup"><span data-stu-id="43c6a-192">**Allow updates**: Specify whether its application packages can be updated or deleted.</span></span> <span data-ttu-id="43c6a-193">Consulte "Atualizar ou excluir um pacote de aplicativos" mais adiante neste artigo.</span><span class="sxs-lookup"><span data-stu-id="43c6a-193">See "Update or Delete an application package" later in this article.</span></span>
* <span data-ttu-id="43c6a-194">**Versão padrão**: especifique um pacote de aplicativos padrão para implantar nos nós de computação.</span><span class="sxs-lookup"><span data-stu-id="43c6a-194">**Default version**: Specify a default application package to deploy to compute nodes.</span></span>
* <span data-ttu-id="43c6a-195">**Nome de exibição**: especifique um nome amigável que sua solução de Lote pode usar ao exibir informações sobre o aplicativo, como na interface do usuário de um serviço que você fornece aos clientes por meio do Lote.</span><span class="sxs-lookup"><span data-stu-id="43c6a-195">**Display name**: Specify a friendly name that your Batch solution can use when it displays information about the application, for example, in the UI of a service that you provide to your customers through Batch.</span></span>

### <a name="add-a-new-application"></a><span data-ttu-id="43c6a-196">Adicionar um novo aplicativo</span><span class="sxs-lookup"><span data-stu-id="43c6a-196">Add a new application</span></span>
<span data-ttu-id="43c6a-197">Para criar um novo aplicativo, adicione um pacote de aplicativos e especifique uma ID de aplicativo nova e exclusiva.</span><span class="sxs-lookup"><span data-stu-id="43c6a-197">To create a new application, add an application package and specify a new, unique application ID.</span></span> <span data-ttu-id="43c6a-198">O primeiro pacote de aplicativos que você adiciona com a nova ID de aplicativo também cria o novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="43c6a-198">The first application package that you add with the new application ID also creates the new application.</span></span>

<span data-ttu-id="43c6a-199">Clique em **Adicionar** na folha **Aplicativos** para abrir a folha **Novo aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="43c6a-199">Click **Add** on the **Applications** blade to open the **New application** blade.</span></span>

<span data-ttu-id="43c6a-200">![Folha Novo aplicativo no portal do Azure][5]</span><span class="sxs-lookup"><span data-stu-id="43c6a-200">![New application blade in Azure portal][5]</span></span>

<span data-ttu-id="43c6a-201">A folha **Novo aplicativo** fornece os campos a seguir para especificar as configurações do seu novo aplicativo e do pacote de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="43c6a-201">The **New application** blade provides the following fields to specify the settings of your new application and application package.</span></span>

<span data-ttu-id="43c6a-202">**ID do aplicativo**</span><span class="sxs-lookup"><span data-stu-id="43c6a-202">**Application id**</span></span>

<span data-ttu-id="43c6a-203">Este campo especifica a ID do novo aplicativo, que está sujeita às regras de validação padrão de ID do Lote do Azure.</span><span class="sxs-lookup"><span data-stu-id="43c6a-203">This field specifies the ID of your new application, which is subject to the standard Azure Batch ID validation rules.</span></span> <span data-ttu-id="43c6a-204">As regras para fornecer uma ID de aplicativo são conforme descrito a seguir:</span><span class="sxs-lookup"><span data-stu-id="43c6a-204">The rules for providing an application ID are as follows:</span></span>

* <span data-ttu-id="43c6a-205">Em nós do Windows, a ID pode conter qualquer combinação de caracteres alfanuméricos, hifens e sublinhados.</span><span class="sxs-lookup"><span data-stu-id="43c6a-205">On Windows nodes, the ID can contain any combination of alphanumeric characters, hyphens, and underscores.</span></span> <span data-ttu-id="43c6a-206">Em nós do Linux, são permitidos somente caracteres alfanuméricos e sublinhados.</span><span class="sxs-lookup"><span data-stu-id="43c6a-206">On Linux nodes, only alphanumeric characters and underscores are permitted.</span></span>
* <span data-ttu-id="43c6a-207">Não pode conter mais de 64 caracteres.</span><span class="sxs-lookup"><span data-stu-id="43c6a-207">Cannot contain more than 64 characters.</span></span>
* <span data-ttu-id="43c6a-208">Deve ser exclusiva na conta do Lote.</span><span class="sxs-lookup"><span data-stu-id="43c6a-208">Must be unique within the Batch account.</span></span>
* <span data-ttu-id="43c6a-209">Não diferencia maiúsculas de minúsculas e preserva maiúsculas e minúsculas.</span><span class="sxs-lookup"><span data-stu-id="43c6a-209">Is case-preserving and case-insensitive.</span></span>

<span data-ttu-id="43c6a-210">**Versão**</span><span class="sxs-lookup"><span data-stu-id="43c6a-210">**Version**</span></span>

<span data-ttu-id="43c6a-211">Este campo especifica a versão do pacote de aplicativos que você está carregando.</span><span class="sxs-lookup"><span data-stu-id="43c6a-211">This field specifies the version of the application package you are uploading.</span></span> <span data-ttu-id="43c6a-212">As cadeias de caracteres da versão estão sujeitas às seguintes regras de validação:</span><span class="sxs-lookup"><span data-stu-id="43c6a-212">Version strings are subject to the following validation rules:</span></span>

* <span data-ttu-id="43c6a-213">Em nós do Windows, a cadeia de caracteres de versão pode conter qualquer combinação de caracteres alfanuméricos, hifens, sublinhados e pontos.</span><span class="sxs-lookup"><span data-stu-id="43c6a-213">On Windows nodes, the version string can contain any combination of alphanumeric characters, hyphens, underscores, and periods.</span></span> <span data-ttu-id="43c6a-214">Em nós do Linux, a cadeia de caracteres de versão pode conter somente caracteres alfanuméricos e sublinhados.</span><span class="sxs-lookup"><span data-stu-id="43c6a-214">On Linux nodes, the version string can contain only alphanumeric characters and underscores.</span></span>
* <span data-ttu-id="43c6a-215">Não pode conter mais de 64 caracteres.</span><span class="sxs-lookup"><span data-stu-id="43c6a-215">Cannot contain more than 64 characters.</span></span>
* <span data-ttu-id="43c6a-216">Devem ser exclusivas no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="43c6a-216">Must be unique within the application.</span></span>
* <span data-ttu-id="43c6a-217">Não diferenciam maiúsculas de minúsculas e preservam maiúsculas e minúsculas.</span><span class="sxs-lookup"><span data-stu-id="43c6a-217">Are case-preserving and case-insensitive.</span></span>

<span data-ttu-id="43c6a-218">**Pacote de aplicativos**</span><span class="sxs-lookup"><span data-stu-id="43c6a-218">**Application package**</span></span>

<span data-ttu-id="43c6a-219">Esse campo especifica o arquivo .zip que contém os binários do aplicativo e os arquivos de suporte que necessários à execução do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="43c6a-219">This field specifies the .zip file that contains the application binaries and supporting files that are required to execute the application.</span></span> <span data-ttu-id="43c6a-220">Clique na caixa **Selecionar um arquivo** ou no ícone de pasta para procurar e selecionar um arquivo .zip que contém os arquivos do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="43c6a-220">Click the **Select a file** box or the folder icon to browse to and select a .zip file that contains your application's files.</span></span>

<span data-ttu-id="43c6a-221">Depois de ter selecionado um arquivo, clique em **OK** para começar a carregar no Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="43c6a-221">After you've selected a file, click **OK** to begin the upload to Azure Storage.</span></span> <span data-ttu-id="43c6a-222">Quando a operação de upload for concluída, o portal exibirá uma notificação e fechará a folha.</span><span class="sxs-lookup"><span data-stu-id="43c6a-222">When the upload operation is complete, the portal displays a notification and closes the blade.</span></span> <span data-ttu-id="43c6a-223">Dependendo do tamanho do arquivo que você estiver carregando e da velocidade da conexão de rede, essa operação pode demorar um pouco.</span><span class="sxs-lookup"><span data-stu-id="43c6a-223">Depending on the size of the file that you are uploading and the speed of your network connection, this operation may take some time.</span></span>

> [!WARNING]
> <span data-ttu-id="43c6a-224">Não feche a folha **Novo aplicativo** antes de a operação de carregamento estar concluída.</span><span class="sxs-lookup"><span data-stu-id="43c6a-224">Do not close the **New application** blade before the upload operation is complete.</span></span> <span data-ttu-id="43c6a-225">Isso interromperá o processo de carregamento.</span><span class="sxs-lookup"><span data-stu-id="43c6a-225">Doing so will stop the upload process.</span></span>
> 
> 

### <a name="add-a-new-application-package"></a><span data-ttu-id="43c6a-226">Adicionar um novo pacote de aplicativos</span><span class="sxs-lookup"><span data-stu-id="43c6a-226">Add a new application package</span></span>
<span data-ttu-id="43c6a-227">Para adicionar uma nova versão do pacote de aplicativos a um aplicativo existente, selecione um aplicativo na folha **Aplicativos**, clique em **Pacotes** e **Adicionar** para abrir a folha **Adicionar pacote**.</span><span class="sxs-lookup"><span data-stu-id="43c6a-227">To add a new application package version for an existing application, select an application in the **Applications** blade, click **Packages**, then click **Add** to open the **Add package** blade.</span></span>

<span data-ttu-id="43c6a-228">![Folha Adicionar pacote de aplicativos no portal do Azure][8]</span><span class="sxs-lookup"><span data-stu-id="43c6a-228">![Add application package blade in Azure portal][8]</span></span>

<span data-ttu-id="43c6a-229">Como você pode ver, os campos correspondem aos da folha **Novo aplicativo**, mas a caixa **ID do Aplicativo** fica desabilitada.</span><span class="sxs-lookup"><span data-stu-id="43c6a-229">As you can see, the fields match those of the **New application** blade, but the **Application id** box is disabled.</span></span> <span data-ttu-id="43c6a-230">Assim como para o novo aplicativo, especifique a **Versão** do novo pacote, procure o arquivo .zip do **Pacote de aplicativos** e clique em **OK** para carregar o pacote.</span><span class="sxs-lookup"><span data-stu-id="43c6a-230">As you did for the new application, specify the **Version** for your new package, browse to your **Application package** .zip file, then click **OK** to upload the package.</span></span>

### <a name="update-or-delete-an-application-package"></a><span data-ttu-id="43c6a-231">Atualizar ou excluir um pacote de aplicativos</span><span class="sxs-lookup"><span data-stu-id="43c6a-231">Update or delete an application package</span></span>
<span data-ttu-id="43c6a-232">Para atualizar ou excluir um pacote de aplicativos existente, abra a folha de detalhes do aplicativo, clique em **Pacotes** para abrir a folha **Pacotes**, clique nas **reticências** na linha do pacote de aplicativos que você deseja modificar e selecione a ação que deseja executar.</span><span class="sxs-lookup"><span data-stu-id="43c6a-232">To update or delete an existing application package, open the details blade for the application, click **Packages** to open the **Packages** blade, click the **ellipsis** in the row of the application package that you want to modify, and select the action that you want to perform.</span></span>

<span data-ttu-id="43c6a-233">![Atualizar ou excluir pacote no portal do Azure][7]</span><span class="sxs-lookup"><span data-stu-id="43c6a-233">![Update or delete package in Azure portal][7]</span></span>

<span data-ttu-id="43c6a-234">**Atualizar**</span><span class="sxs-lookup"><span data-stu-id="43c6a-234">**Update**</span></span>

<span data-ttu-id="43c6a-235">Quando você clica em **Atualizar**, a folha *Atualizar pacote* é exibida.</span><span class="sxs-lookup"><span data-stu-id="43c6a-235">When you click **Update**, the *Update package* blade is displayed.</span></span> <span data-ttu-id="43c6a-236">Essa folha é semelhante à folha *Novo pacote de aplicativos*. No entanto, somente o campo de seleção de pacotes está habilitado, permitindo que você especifique um novo arquivo ZIP a carregar.</span><span class="sxs-lookup"><span data-stu-id="43c6a-236">This blade is similar to the *New application package* blade, however only the package selection field is enabled, allowing you to specify a new ZIP file to upload.</span></span>

<span data-ttu-id="43c6a-237">![Folha do pacote de atualização no portal do Azure][11]</span><span class="sxs-lookup"><span data-stu-id="43c6a-237">![Update package blade in Azure portal][11]</span></span>

<span data-ttu-id="43c6a-238">**Excluir**</span><span class="sxs-lookup"><span data-stu-id="43c6a-238">**Delete**</span></span>

<span data-ttu-id="43c6a-239">Quando você clica em **Excluir**, é preciso confirmar a exclusão da versão do pacote e o Lote exclui o pacote do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="43c6a-239">When you click **Delete**, you are asked to confirm the deletion of the package version, and Batch deletes the package from Azure Storage.</span></span> <span data-ttu-id="43c6a-240">Se você excluir a versão padrão de um aplicativo, a configuração da **Versão padrão** será removida para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="43c6a-240">If you delete the default version of an application, the **Default version** setting is removed for the application.</span></span>

<span data-ttu-id="43c6a-241">![Excluir aplicativo ][12]</span><span class="sxs-lookup"><span data-stu-id="43c6a-241">![Delete application ][12]</span></span>

## <a name="install-applications-on-compute-nodes"></a><span data-ttu-id="43c6a-242">Instalar aplicativos em nós de computação</span><span class="sxs-lookup"><span data-stu-id="43c6a-242">Install applications on compute nodes</span></span>
<span data-ttu-id="43c6a-243">Agora que você aprendeu como gerenciar os pacotes de aplicativos com o portal do Azure, podemos analisar como implantá-los para os nós de computação e executá-los com tarefas em Lote.</span><span class="sxs-lookup"><span data-stu-id="43c6a-243">Now that you've learned how to manage application packages with the Azure portal, we can discuss how to deploy them to compute nodes and run them with Batch tasks.</span></span>

### <a name="install-pool-application-packages"></a><span data-ttu-id="43c6a-244">Instalar pacotes de aplicativos do pool</span><span class="sxs-lookup"><span data-stu-id="43c6a-244">Install pool application packages</span></span>
<span data-ttu-id="43c6a-245">Para instalar um pacote de aplicativos em todos os nós de computação em um pool, especifique uma ou mais *referências* do pacote de aplicativos para o pool.</span><span class="sxs-lookup"><span data-stu-id="43c6a-245">To install an application package on all compute nodes in a pool, specify one or more application package *references* for the pool.</span></span> <span data-ttu-id="43c6a-246">Os pacotes de aplicativo que você especifica para um pool são instalados em cada nó de computação quando esse nó se une ao pool, e quando o nó é reinicializado ou tem sua imagem refeita.</span><span class="sxs-lookup"><span data-stu-id="43c6a-246">The application packages that you specify for a pool are installed on each compute node when that node joins the pool, and when the node is rebooted or reimaged.</span></span>

<span data-ttu-id="43c6a-247">No .NET do Lote, especifique um ou mais [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref] quando você criar um novo pool ou para um pool existente.</span><span class="sxs-lookup"><span data-stu-id="43c6a-247">In Batch .NET, specify one or more [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref] when you create a new pool, or for an existing pool.</span></span> <span data-ttu-id="43c6a-248">A classe [ApplicationPackageReference][net_pkgref] especifica uma ID e versão do aplicativo para instalar nos nós de computação de um pool.</span><span class="sxs-lookup"><span data-stu-id="43c6a-248">The [ApplicationPackageReference][net_pkgref] class specifies an application ID and version to install on a pool's compute nodes.</span></span>

```csharp
// Create the unbound CloudPool
CloudPool myCloudPool =
    batchClient.PoolOperations.CreatePool(
        poolId: "myPool",
        targetDedicatedComputeNodes: 1,
        virtualMachineSize: "small",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

// Specify the application and version to install on the compute nodes
myCloudPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "litware",
        Version = "1.1001.2b" }
};

// Commit the pool so that it's created in the Batch service. As the nodes join
// the pool, the specified application package is installed on each.
await myCloudPool.CommitAsync();
```

> [!IMPORTANT]
> <span data-ttu-id="43c6a-249">Se uma implantação do pacote de aplicativos falhar por algum motivo, o serviço do Lote marcará o nó como [inutilizável][net_nodestate] e nenhuma tarefa será agendada para a execução nesse nó.</span><span class="sxs-lookup"><span data-stu-id="43c6a-249">If an application package deployment fails for any reason, the Batch service marks the node [unusable][net_nodestate], and no tasks are scheduled for execution on that node.</span></span> <span data-ttu-id="43c6a-250">Nesse caso, você deve **reiniciar** o nó para reiniciar a implantação do pacote.</span><span class="sxs-lookup"><span data-stu-id="43c6a-250">In this case, you should **restart** the node to reinitiate the package deployment.</span></span> <span data-ttu-id="43c6a-251">A reinicialização do nó também habilita novamente nele o agendamento de tarefas.</span><span class="sxs-lookup"><span data-stu-id="43c6a-251">Restarting the node also enables task scheduling again on the node.</span></span>
> 
> 

### <a name="install-task-application-packages"></a><span data-ttu-id="43c6a-252">Instalar pacotes de aplicativos de tarefa</span><span class="sxs-lookup"><span data-stu-id="43c6a-252">Install task application packages</span></span>
<span data-ttu-id="43c6a-253">Semelhante a um pool, você especifica as *referências* do pacote de aplicativos para uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="43c6a-253">Similar to a pool, you specify application package *references* for a task.</span></span> <span data-ttu-id="43c6a-254">Quando uma tarefa está agendada para ser executada em um nó, o pacote é baixado e extraído um pouco antes da linha de comando da tarefa ser executada.</span><span class="sxs-lookup"><span data-stu-id="43c6a-254">When a task is scheduled to run on a node, the package is downloaded and extracted just before the task's command line is executed.</span></span> <span data-ttu-id="43c6a-255">Se o pacote especificado e a versão já estiverem instalados no nó, o pacote não será baixado e o pacote existente será usado.</span><span class="sxs-lookup"><span data-stu-id="43c6a-255">If a specified package and version is already installed on the node, the package is not downloaded and the existing package is used.</span></span>

<span data-ttu-id="43c6a-256">Para instalar um pacote de aplicativos de tarefa, configure a propriedade [CloudTask][net_cloudtask].[ApplicationPackageReferences][net_cloudtask_pkgref] da tarefa:</span><span class="sxs-lookup"><span data-stu-id="43c6a-256">To install a task application package, configure the task's [CloudTask][net_cloudtask].[ApplicationPackageReferences][net_cloudtask_pkgref] property:</span></span>

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

## <a name="execute-the-installed-applications"></a><span data-ttu-id="43c6a-257">Executar os aplicativos instalados</span><span class="sxs-lookup"><span data-stu-id="43c6a-257">Execute the installed applications</span></span>
<span data-ttu-id="43c6a-258">Os pacotes que você especificou para uma tarefa ou um pool são baixados e extraídos para um diretório nomeado dentro do `AZ_BATCH_ROOT_DIR` do nó.</span><span class="sxs-lookup"><span data-stu-id="43c6a-258">The packages that you've specified for a pool or task are downloaded and extracted to a named directory within the `AZ_BATCH_ROOT_DIR` of the node.</span></span> <span data-ttu-id="43c6a-259">O Lote também cria uma variável de ambiente que contém o caminho para o diretório nomeado.</span><span class="sxs-lookup"><span data-stu-id="43c6a-259">Batch also creates an environment variable that contains the path to the named directory.</span></span> <span data-ttu-id="43c6a-260">As linhas de comando da tarefa usam essa variável de ambiente ao referenciar o aplicativo no nó.</span><span class="sxs-lookup"><span data-stu-id="43c6a-260">Your task command lines use this environment variable when referencing the application on the node.</span></span> 

<span data-ttu-id="43c6a-261">Em nós do Windows, a variável está no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="43c6a-261">On Windows nodes, the variable is in the following format:</span></span>

```
Windows:
AZ_BATCH_APP_PACKAGE_APPLICATIONID#version
```

<span data-ttu-id="43c6a-262">Em nós do Linux, o formato é ligeiramente diferente.</span><span class="sxs-lookup"><span data-stu-id="43c6a-262">On Linux nodes, the format is slightly different.</span></span> <span data-ttu-id="43c6a-263">Pontos (.), hifens (-) e teclas jogo da velha (#) são transformados em sublinhados na variável de ambiente.</span><span class="sxs-lookup"><span data-stu-id="43c6a-263">Periods (.), hypens (-) and number signs (#) are flattened to underscores in the environment variable.</span></span> <span data-ttu-id="43c6a-264">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="43c6a-264">For example:</span></span>

```
Linux:
AZ_BATCH_APP_PACKAGE_APPLICATIONID_version
```

<span data-ttu-id="43c6a-265">`APPLICATIONID` e `version` são os valores que correspondem à versão do aplicativo e do pacote que você especificou para a implantação.</span><span class="sxs-lookup"><span data-stu-id="43c6a-265">`APPLICATIONID` and `version` are values that correspond to the application and package version you've specified for deployment.</span></span> <span data-ttu-id="43c6a-266">Por exemplo, se você especificou que a versão 2.7 do *blender* de aplicativos deve ser instalada em nós do Windows, as linhas de comando da tarefa usarão essa variável de ambiente para acessar seus arquivos:</span><span class="sxs-lookup"><span data-stu-id="43c6a-266">For example, if you specified that version 2.7 of application *blender* should be installed on Windows nodes, your task command lines would use this environment variable to access its files:</span></span>

```
Windows:
AZ_BATCH_APP_PACKAGE_BLENDER#2.7
```

<span data-ttu-id="43c6a-267">Em nós do Linux, especifique a variável de ambiente neste formato:</span><span class="sxs-lookup"><span data-stu-id="43c6a-267">On Linux nodes, specify the environment variable in this format:</span></span>

```
Linux:
AZ_BATCH_APP_PACKAGE_BLENDER_2_7
``` 

<span data-ttu-id="43c6a-268">Quando você carrega um pacote de aplicativos, você pode especificar uma versão padrão para implantar em seus nós de computação.</span><span class="sxs-lookup"><span data-stu-id="43c6a-268">When you upload an application package, you can specify a default version to deploy to your compute nodes.</span></span> <span data-ttu-id="43c6a-269">Se você tiver especificado uma versão padrão para um aplicativo, poderá omitir o sufixo da versão ao referenciar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="43c6a-269">If you have specified a default version for an application, you can omit the version suffix when you reference the application.</span></span> <span data-ttu-id="43c6a-270">Você pode especificar a versão padrão do aplicativo no portal do Azure, na folha de Aplicativos, como mostrado em [Carregue e gerencie aplicativos](#upload-and-manage-applications).</span><span class="sxs-lookup"><span data-stu-id="43c6a-270">You can specify the default application version in the Azure portal, on the Applications blade, as shown in [Upload and manage applications](#upload-and-manage-applications).</span></span>

<span data-ttu-id="43c6a-271">Por exemplo, se você definiu "2.7" como a versão padrão do *blender* de aplicativos e suas tarefas referenciam a variável de ambiente a seguir, seus nós do Windows executarão a versão 2.7:</span><span class="sxs-lookup"><span data-stu-id="43c6a-271">For example, if you set "2.7" as the default version for application *blender*, and your tasks reference the following environment variable, then your Windows nodes will execute version 2.7:</span></span>

`AZ_BATCH_APP_PACKAGE_BLENDER`

<span data-ttu-id="43c6a-272">O trecho de código a seguir mostra uma linha de comando da tarefa de exemplo que inicializa a versão padrão do *blender* de aplicativos:</span><span class="sxs-lookup"><span data-stu-id="43c6a-272">The following code snippet shows an example task command line that launches the default version of the *blender* application:</span></span>

```csharp
string taskId = "blendertask01";
string commandLine =
    @"cmd /c %AZ_BATCH_APP_PACKAGE_BLENDER%\blender.exe -args -here";
CloudTask blenderTask = new CloudTask(taskId, commandLine);
```

> [!TIP]
> <span data-ttu-id="43c6a-273">Consulte [Configurações do ambiente para tarefas](batch-api-basics.md#environment-settings-for-tasks) na [Visão geral do recurso de Lote](batch-api-basics.md) para saber mais sobre as configurações do ambiente do nó de computação.</span><span class="sxs-lookup"><span data-stu-id="43c6a-273">See [Environment settings for tasks](batch-api-basics.md#environment-settings-for-tasks) in the [Batch feature overview](batch-api-basics.md) for more information about compute node environment settings.</span></span>
> 
> 

## <a name="update-a-pools-application-packages"></a><span data-ttu-id="43c6a-274">Atualizar pacotes de aplicativos de um pool</span><span class="sxs-lookup"><span data-stu-id="43c6a-274">Update a pool's application packages</span></span>
<span data-ttu-id="43c6a-275">Se um pool existente já tiver sido configurado com um pacote de aplicativos, você poderá especificar um novo pacote para o pool.</span><span class="sxs-lookup"><span data-stu-id="43c6a-275">If an existing pool has already been configured with an application package, you can specify a new package for the pool.</span></span> <span data-ttu-id="43c6a-276">Se você especificar uma nova referência de pacote para um pool, o seguinte se aplicará:</span><span class="sxs-lookup"><span data-stu-id="43c6a-276">If you specify a new package reference for a pool, the following apply:</span></span>

* <span data-ttu-id="43c6a-277">O serviço de Lote instala o pacote recém-especificado em todos os novos nós que ingressam no pool e em qualquer nó existente que seja reinicializado ou cuja imagem seja refeita.</span><span class="sxs-lookup"><span data-stu-id="43c6a-277">The Batch service installs the newly specified package on all new nodes that join the pool and on any existing node that is rebooted or reimaged.</span></span>
* <span data-ttu-id="43c6a-278">Os nós de computação que já estão no pool quando você atualiza as referências do pacote não instalam automaticamente o novo pacote de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="43c6a-278">Compute nodes that are already in the pool when you update the package references do not automatically install the new application package.</span></span> <span data-ttu-id="43c6a-279">Esses nós de computação devem ser reinicializados ou ter sua imagem recriada para receber o novo pacote.</span><span class="sxs-lookup"><span data-stu-id="43c6a-279">These compute nodes must be rebooted or reimaged to receive the new package.</span></span>
* <span data-ttu-id="43c6a-280">Quando um novo pacote é implantado, as variáveis de ambiente criadas refletem as novas referências do pacote de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="43c6a-280">When a new package is deployed, the created environment variables reflect the new application package references.</span></span>

<span data-ttu-id="43c6a-281">Neste exemplo, o pool existente tem a versão 2.7 do aplicativo *blender* configurada como um de seus [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref].</span><span class="sxs-lookup"><span data-stu-id="43c6a-281">In this example, the existing pool has version 2.7 of the *blender* application configured as one of its [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref].</span></span> <span data-ttu-id="43c6a-282">Para atualizar os nós do pool com a versão 2.76b, especifique um novo [ApplicationPackageReference][net_pkgref] com a nova versão e confirme a mudança.</span><span class="sxs-lookup"><span data-stu-id="43c6a-282">To update the pool's nodes with version 2.76b, specify a new [ApplicationPackageReference][net_pkgref] with the new version, and commit the change.</span></span>

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

<span data-ttu-id="43c6a-283">Agora que a nova versão foi configurada, o serviço de Lote instala a versão 2.76b em qualquer nó *novo* que ingresse no pool.</span><span class="sxs-lookup"><span data-stu-id="43c6a-283">Now that the new version has been configured, the Batch service installs version 2.76b to any *new* node that joins the pool.</span></span> <span data-ttu-id="43c6a-284">Para instalar a versão 2.76b nos nós que já *estão* no pool, reinicialize-os ou refaça a imagem deles.</span><span class="sxs-lookup"><span data-stu-id="43c6a-284">To install 2.76b on the nodes that are *already* in the pool, reboot or reimage them.</span></span> <span data-ttu-id="43c6a-285">Observe que os nós reinicializados retém os arquivos das implantações anteriores do pacote.</span><span class="sxs-lookup"><span data-stu-id="43c6a-285">Note that rebooted nodes retain the files from previous package deployments.</span></span>

## <a name="list-the-applications-in-a-batch-account"></a><span data-ttu-id="43c6a-286">Listar os aplicativos em uma conta do Lote</span><span class="sxs-lookup"><span data-stu-id="43c6a-286">List the applications in a Batch account</span></span>
<span data-ttu-id="43c6a-287">Você pode listar os aplicativos e seus pacotes em uma conta do Lote usando o método [ApplicationOperations][net_appops].[ListApplicationSummaries][net_appops_listappsummaries].</span><span class="sxs-lookup"><span data-stu-id="43c6a-287">You can list the applications and their packages in a Batch account by using the [ApplicationOperations][net_appops].[ListApplicationSummaries][net_appops_listappsummaries] method.</span></span>

```csharp
// List the applications and their application packages in the Batch account.
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

## <a name="wrap-up"></a><span data-ttu-id="43c6a-288">Conclusão</span><span class="sxs-lookup"><span data-stu-id="43c6a-288">Wrap up</span></span>
<span data-ttu-id="43c6a-289">Com os pacotes de aplicativos, você pode fornecer ajudar seus clientes a escolher os aplicativos para seus trabalhos e especificar a versão exata a ser usada ao processar trabalhos com o serviço habilitado para o Lote.</span><span class="sxs-lookup"><span data-stu-id="43c6a-289">With application packages, you can help your customers select the applications for their jobs and specify the exact version to use when processing jobs with your Batch-enabled service.</span></span> <span data-ttu-id="43c6a-290">Você também pode fornecer aos clientes a capacidade de carregar e rastrear os próprios aplicativos no serviço.</span><span class="sxs-lookup"><span data-stu-id="43c6a-290">You might also provide the ability for your customers to upload and track their own applications in your service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="43c6a-291">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="43c6a-291">Next steps</span></span>
* <span data-ttu-id="43c6a-292">A [API REST do Lote][api_rest] também dá suporte ao trabalho com pacotes de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="43c6a-292">The [Batch REST API][api_rest] also provides support to work with application packages.</span></span> <span data-ttu-id="43c6a-293">Por exemplo, consulte o elemento [applicationPackageReferences][rest_add_pool_with_packages] em [Adicionar um pool a uma conta][rest_add_pool] para obter informações sobre como especificar os pacotes a instalar usando a API REST.</span><span class="sxs-lookup"><span data-stu-id="43c6a-293">For example, see the [applicationPackageReferences][rest_add_pool_with_packages] element in [Add a pool to an account][rest_add_pool] for information about how to specify packages to install by using the REST API.</span></span> <span data-ttu-id="43c6a-294">Consulte [Aplicativos][rest_applications] para obter detalhes sobre como obter informações do aplicativo usando a API REST do Lote.</span><span class="sxs-lookup"><span data-stu-id="43c6a-294">See [Applications][rest_applications] for details about how to obtain application information by using the Batch REST API.</span></span>
* <span data-ttu-id="43c6a-295">Aprenda a [gerenciar de modo programático as contas e as cotas do Lote do Azure com o .NET de Gerenciamento do Lote](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="43c6a-295">Learn how to programmatically [manage Azure Batch accounts and quotas with Batch Management .NET](batch-management-dotnet.md).</span></span> <span data-ttu-id="43c6a-296">A biblioteca [.NET de Gerenciamento do Lote][api_net_mgmt] pode permitir os recursos de criação e exclusão de conta para seu aplicativo ou serviço do Lote.</span><span class="sxs-lookup"><span data-stu-id="43c6a-296">The [Batch Management .NET][api_net_mgmt] library can enable account creation and deletion features for your Batch application or service.</span></span>

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
