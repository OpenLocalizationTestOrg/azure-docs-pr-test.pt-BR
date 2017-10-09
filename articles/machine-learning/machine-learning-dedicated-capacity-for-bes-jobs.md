---
title: "aaaDedicated capacidade para trabalhos de serviço de execução do máquina aprendizado em lotes | Microsoft Docs"
description: "Visão geral dos serviços do Lote do Azure para trabalhos do Machine Learning."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.service: machine-learning
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: bba7970bb31c50e5b0b9d5f4ff4f0d2dacf942e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-batch-service-for-machine-learning-jobs"></a><span data-ttu-id="73a63-103">Serviço do Lote do Azure para trabalhos do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="73a63-103">Azure Batch service for Machine Learning jobs</span></span>

<span data-ttu-id="73a63-104">Processamento de Pool de lote do aprendizado de máquina fornece escala gerenciada pelo cliente para hello Azure Machine Learning lote execução serviço.</span><span class="sxs-lookup"><span data-stu-id="73a63-104">Machine Learning Batch Pool processing provides customer-managed scale for hello Azure Machine Learning Batch Execution Service.</span></span> <span data-ttu-id="73a63-105">Clássico processamento em lotes para aprendizado de máquina ocorre em um ambiente multilocatário, o número da saudação limites de trabalhos simultâneos, você pode enviar e trabalhos é enfileirado em uma base de primeiro a entrar, primeiro a sair.</span><span class="sxs-lookup"><span data-stu-id="73a63-105">Classic batch processing for machine learning takes place in a multi-tenant environment, which limits hello number of concurrent jobs you can submit, and jobs are queued on a first-in-first-out basis.</span></span> <span data-ttu-id="73a63-106">Essa incerteza significa que você não pode prever com exatidão quando seu trabalho será executado.</span><span class="sxs-lookup"><span data-stu-id="73a63-106">This uncertainty means that you can't accurately predict when your job will run.</span></span>

<span data-ttu-id="73a63-107">Processamento em lote do Pool permite pools toocreate no qual você pode enviar trabalhos de lote.</span><span class="sxs-lookup"><span data-stu-id="73a63-107">Batch Pool processing allows you toocreate pools on which you can submit batch jobs.</span></span> <span data-ttu-id="73a63-108">Controlar o tamanho de saudação do pool de saudação e toowhich pool Olá trabalho é enviado.</span><span class="sxs-lookup"><span data-stu-id="73a63-108">You control hello size of hello pool, and toowhich pool hello job is submitted.</span></span> <span data-ttu-id="73a63-109">Seu trabalho BES é executado em seu próprio processamento fornecendo espaço desempenho previsível e Olá capacidade toocreate pools de recursos que correspondem a carga de processamento de toohello que você enviar.</span><span class="sxs-lookup"><span data-stu-id="73a63-109">Your BES job runs in its own processing space providing predictable processing performance and hello ability toocreate resource pools that correspond toohello processing load that you submit.</span></span>

## <a name="how-toouse-batch-pool-processing"></a><span data-ttu-id="73a63-110">Como o processamento em lotes Pool toouse</span><span class="sxs-lookup"><span data-stu-id="73a63-110">How toouse Batch Pool processing</span></span>

<span data-ttu-id="73a63-111">Configuração de lote Pool de processamento não está disponível atualmente por meio de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="73a63-111">Configuration of Batch Pool Processing is not currently available through hello Azure portal.</span></span> <span data-ttu-id="73a63-112">toouse Pool do lote de processamento, você deve:</span><span class="sxs-lookup"><span data-stu-id="73a63-112">toouse Batch Pool processing, you must:</span></span>

-   <span data-ttu-id="73a63-113">Chamar CSS toocreate uma conta de Pool de lote e obter uma URL de serviço de Pool e uma chave de autorização</span><span class="sxs-lookup"><span data-stu-id="73a63-113">Call CSS toocreate a Batch Pool Account and obtain a Pool Service URL and an authorization key</span></span>
-   <span data-ttu-id="73a63-114">Criar um serviço Web baseado no novo Resource Manager e um plano de cobrança</span><span class="sxs-lookup"><span data-stu-id="73a63-114">Create a New Resource Manager based web service and billing plan</span></span>

<span data-ttu-id="73a63-115">toocreate sua conta, chame o atendimento ao cliente Microsoft e suporte (CSS) e fornecer sua ID de assinatura.</span><span class="sxs-lookup"><span data-stu-id="73a63-115">toocreate your account, call Microsoft Customer Service and Support (CSS) and provide your Subscription ID.</span></span> <span data-ttu-id="73a63-116">CSS funcionará com você toodetermine Olá capacidade apropriada para seu cenário.</span><span class="sxs-lookup"><span data-stu-id="73a63-116">CSS will work with you toodetermine hello appropriate capacity for your scenario.</span></span> <span data-ttu-id="73a63-117">CSS, em seguida, configura sua conta com número de máximo de saudação de pools, você pode criar e Olá número máximo de máquinas virtuais (VMs) que você pode colocar em cada pool.</span><span class="sxs-lookup"><span data-stu-id="73a63-117">CSS then configures your account with hello maximum number of pools you can create and hello maximum number of virtual machines (VMs) that you can place in each pool.</span></span> <span data-ttu-id="73a63-118">Assim que sua conta estiver configurada, você receberá a URL de Serviço do Pool e uma chave de autorização.</span><span class="sxs-lookup"><span data-stu-id="73a63-118">Once your account is configured, you are provided your Pool Service URL and an authorization key.</span></span>

<span data-ttu-id="73a63-119">Depois que a conta é criada, você pode usar Olá URL do serviço de Pool e autorização tooperform chave pool operações de gerenciamento em seu Pool de lote.</span><span class="sxs-lookup"><span data-stu-id="73a63-119">After your account is created, you use hello Pool Service URL and authorization key tooperform pool management operations on your Batch Pool.</span></span>

![Arquitetura do serviço do pool do lote.](media/machine-learning-dedicated-capacity-for-bes-jobs/pool-architecture.png)

<span data-ttu-id="73a63-121">Você pode criar pools chamando a operação de criar Pool de saudação na URL do serviço de pool de saudação que tooyou CSS fornecido.</span><span class="sxs-lookup"><span data-stu-id="73a63-121">You create pools by calling hello Create Pool operation on hello pool service URL that CSS provided tooyou.</span></span> <span data-ttu-id="73a63-122">Quando você cria um pool, especifique número Olá de VMs e URL de saudação do hello swagger. JSON de um novo Gerenciador de recursos com base em serviço web de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="73a63-122">When you create a pool, specify hello number of VMs and hello URL of hello swagger.json of a New Resource Manager based Machine Learning web service.</span></span> <span data-ttu-id="73a63-123">Esse serviço da web é fornecido a associação de cobrança de saudação do tooestablish.</span><span class="sxs-lookup"><span data-stu-id="73a63-123">This web service is provided tooestablish hello billing association.</span></span> <span data-ttu-id="73a63-124">Olá serviço de Pool do lote usa pool de Olá Olá swagger. JSON tooassociate com um plano de cobrança.</span><span class="sxs-lookup"><span data-stu-id="73a63-124">hello Batch Pool service uses hello swagger.json tooassociate hello pool with a billing plan.</span></span> <span data-ttu-id="73a63-125">Você pode executar qualquer BES serviço da web, ambos os novo Gerenciador de recursos com base e clássico, escolha no pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="73a63-125">You can run any BES web service, both New Resource Manager based and classic, you choose on hello pool.</span></span>

<span data-ttu-id="73a63-126">Você pode usar qualquer serviço do novo Gerenciador de recursos com base na web, mas lembre-se de que a cobrança Olá para trabalhos de saudação é cobrado em relação ao plano de cobrança Olá associado ao serviço.</span><span class="sxs-lookup"><span data-stu-id="73a63-126">You can use any New Resource Manager based web service, but be aware that hello billing for hello jobs are charged against hello billing plan associated with that service.</span></span> <span data-ttu-id="73a63-127">Talvez você queira toocreate um serviço web e cobrança novo plano especificamente para executar trabalhos do Pool do lote.</span><span class="sxs-lookup"><span data-stu-id="73a63-127">You may want toocreate a web service and new billing plan specifically for running Batch Pool jobs.</span></span>

<span data-ttu-id="73a63-128">Para saber mais sobre como criar serviços Web, confira [Implantar um serviço Web do Machine Learning do Azure](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="73a63-128">For more information on creating web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="73a63-129">Depois de criar um pool, enviar Olá BES trabalho usando hello URL de solicitações em lote para o serviço da web de saudação.</span><span class="sxs-lookup"><span data-stu-id="73a63-129">Once you have created a pool, you submit hello BES job using hello Batch Requests URL for hello web service.</span></span> <span data-ttu-id="73a63-130">Você pode escolher toosubmit-tooa tooclassic ou pool de processamento de lote.</span><span class="sxs-lookup"><span data-stu-id="73a63-130">You can choose toosubmit it tooa pool or tooclassic batch processing.</span></span> <span data-ttu-id="73a63-131">toosubmit um processamento de Pool de tooBatch de trabalho, você adiciona Olá corpo de solicitação de envio do parâmetro toohello trabalho a seguir:</span><span class="sxs-lookup"><span data-stu-id="73a63-131">toosubmit a job tooBatch Pool processing, you add hello following parameter toohello job submission request body:</span></span>

<span data-ttu-id="73a63-132">"AzureBatchPoolId":"&lt;pool ID&gt;"</span><span class="sxs-lookup"><span data-stu-id="73a63-132">"AzureBatchPoolId":"&lt;pool ID&gt;"</span></span>

<span data-ttu-id="73a63-133">Se você não adicionar o parâmetro hello, o trabalho de saudação é executado no ambiente de processo de lote clássico hello.</span><span class="sxs-lookup"><span data-stu-id="73a63-133">If you do not add hello parameter, hello job is run in hello classic batch process environment.</span></span> <span data-ttu-id="73a63-134">Se o pool de saudação tiver recursos disponíveis, o trabalho de saudação começa a ser executado imediatamente.</span><span class="sxs-lookup"><span data-stu-id="73a63-134">If hello pool has available resources, hello job starts running immediately.</span></span> <span data-ttu-id="73a63-135">Se o pool Olá não tem recursos gratuitos, seu trabalho está na fila até que um recurso está disponível.</span><span class="sxs-lookup"><span data-stu-id="73a63-135">If hello pool does not have free resources, your job is queued until a resource is available.</span></span>

<span data-ttu-id="73a63-136">Se você descobrir que você regularmente alcançar a capacidade de saudação de seus pools, e você precisar de maior capacidade, pode chamar CSS e trabalhar com um representante tooincrease suas cotas.</span><span class="sxs-lookup"><span data-stu-id="73a63-136">If you find that you regularly reach hello capacity of your pools, and you need increased capacity, you can call CSS and work with a representative tooincrease your quotas.</span></span>

<span data-ttu-id="73a63-137">Solicitação de exemplo:</span><span class="sxs-lookup"><span data-stu-id="73a63-137">Example Request:</span></span>

<span data-ttu-id="73a63-138">https://ussouthcentral.services.azureml.net/subscriptions/80c77c7674ba4c8c82294c3b2957990c/services/9fe659022c9747e3b9b7b923c3830623/jobs?api-version=2.0</span><span class="sxs-lookup"><span data-stu-id="73a63-138">https://ussouthcentral.services.azureml.net/subscriptions/80c77c7674ba4c8c82294c3b2957990c/services/9fe659022c9747e3b9b7b923c3830623/jobs?api-version=2.0</span></span>

```json
{

    "Input":{
    
        "ConnectionString":"DefaultEndpointsProtocol=https;BlobEndpoint=https://sampleaccount.blob.core.windows.net/;TableEndpoint
        =https://sampleaccount.table.core.windows.net/;QueueEndpoint=https://sampleaccount.queue.core.windows.net/;FileEndpoint=https://zhguim
        l.file.core.windows.net/;AccountName=sampleaccount;AccountKey=&lt;Key&gt;;",
        
        "BaseLocation":null,
        
        "RelativeLocation":"testint/AdultCensusIncomeBinaryClassificationDataset.csv",
        
        "SasBlobToken":null
    
    },
    
    "GlobalParameters":{ },
    
    "Outputs":{
    
        "output1":{
        
            "ConnectionString":"DefaultEndpointsProtocol=https;BlobEndpoint=https://sampleaccount.blob.core.windows.net/;TableEndpo
            int=https://sampleaccount.table.core.windows.net/;QueueEndpoint=https://sampleaccount.queue.core.windows.net/;FileEndpoint=https://sampleaccount.file.core.windows.net/;AccountName=sampleaccount;AccountKey=&lt;Key&gt;",
            "BaseLocation":null,
            "RelativeLocation":"testintoutput/testint\_results.csv",
            
            "SasBlobToken":null
        
        }
    
    },
    
    "AzureBatchPoolId":"8dfc151b0d3e446497b845f3b29ef53b"

}
```

## <a name="considerations-when-using-batch-pool-processing"></a><span data-ttu-id="73a63-139">Considerações ao usar o processamento Pool do Lote</span><span class="sxs-lookup"><span data-stu-id="73a63-139">Considerations when using Batch Pool processing</span></span>

<span data-ttu-id="73a63-140">Processamento de Pool do lote é um serviço de faturável sempre ativa e que exige que você tooassociate-lo com um Gerenciador de recursos com base em plano de cobrança.</span><span class="sxs-lookup"><span data-stu-id="73a63-140">Batch Pool Processing is an always-on billable service and that requires you tooassociate it with a Resource Manager based billing plan.</span></span> <span data-ttu-id="73a63-141">Você só será cobrado por número de saudação de horas de computação pool hello está sendo executado. independentemente do número de saudação de trabalhos executados durante esse pool de tempo.</span><span class="sxs-lookup"><span data-stu-id="73a63-141">You are only billed for hello number of compute hours hello pool is running; regardless of hello number of jobs run during that time pool.</span></span> <span data-ttu-id="73a63-142">Se você criar um pool, você será cobrado por horas de computação de saudação de cada máquina virtual no pool de saudação até que o pool de saudação é excluído, mesmo que nenhum trabalho em lotes está em execução no pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="73a63-142">If you create a pool, you are billed for hello compute hours of each virtual machine in hello pool until hello pool is deleted, even if no batch jobs are running in hello pool.</span></span> <span data-ttu-id="73a63-143">Cobrança para máquinas virtuais de saudação inicia quando terminarem de provisionamento e interrompida quando eles foram excluídos.</span><span class="sxs-lookup"><span data-stu-id="73a63-143">Billing for hello virtual machines starts when they have finished provisioning and stops when they have been deleted.</span></span> <span data-ttu-id="73a63-144">Você pode usar qualquer um dos planos de saudação encontrados no hello [página de preços de aprendizado de máquina](https://azure.microsoft.com/pricing/details/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="73a63-144">You can use any of hello plans found on hello [Machine Learning Pricing page](https://azure.microsoft.com/pricing/details/machine-learning/).</span></span>

<span data-ttu-id="73a63-145">Exemplo de cobrança:</span><span class="sxs-lookup"><span data-stu-id="73a63-145">Billing example:</span></span>

<span data-ttu-id="73a63-146">Caso você crie um Pool do Lote com 2 máquinas virtuais e o exclua após 24 horas, serão debitadas 48 horas de computação do seu plano de cobrança, independentemente de quantos trabalhos foram executados durante esse período.</span><span class="sxs-lookup"><span data-stu-id="73a63-146">If you create a Batch Pool with 2 virtual machines and delete it after 24 hours your billing plan is debited 48 compute hours; regardless of how many jobs were run during that period.</span></span>

<span data-ttu-id="73a63-147">Caso você crie um Pool do Lote com 4 máquinas virtuais e o exclua após 12 horas, também serão debitadas 48 horas de computação do seu plano de cobrança.</span><span class="sxs-lookup"><span data-stu-id="73a63-147">If you create a Batch Pool with 4 virtual machines and delete it after 12 hours, your billing plan is also debited 48 compute hours.</span></span>

<span data-ttu-id="73a63-148">É recomendável que você sondar Olá toodetermine de status de trabalho quando os trabalhos são concluídos.</span><span class="sxs-lookup"><span data-stu-id="73a63-148">We recommend that you poll hello job status toodetermine when jobs complete.</span></span> <span data-ttu-id="73a63-149">Quando todos os trabalhos de terminar de executar, chamada hello redimensionar Pool operação tooset Olá número de máquinas virtuais em Olá pool toozero.</span><span class="sxs-lookup"><span data-stu-id="73a63-149">When all your jobs have finished running, call hello Resize Pool operation tooset hello number of virtual machines in hello pool toozero.</span></span> <span data-ttu-id="73a63-150">Se você for curto em recursos do pool e é necessário toocreate um novo pool, por exemplo toobill em relação a um plano de cobrança diferente, é possível excluir o pool de saudação em vez disso, quando tem terminado de todos os trabalhos em execução.</span><span class="sxs-lookup"><span data-stu-id="73a63-150">If you are short on pool resources and you need toocreate a new pool, for example toobill against a different billing plan, you can delete hello pool instead when all your jobs have finished running.</span></span>


| <span data-ttu-id="73a63-151">**Use o Processamento Pool do Lote quando**</span><span class="sxs-lookup"><span data-stu-id="73a63-151">**Use Batch Pool Processing when**</span></span>    | <span data-ttu-id="73a63-152">**Use o processamento em lotes clássico quando**</span><span class="sxs-lookup"><span data-stu-id="73a63-152">**Use classic batch processing when**</span></span>  |
|---|---|
|<span data-ttu-id="73a63-153">Você precisa toorun um grande número de trabalhos</span><span class="sxs-lookup"><span data-stu-id="73a63-153">You need toorun a large number of jobs</span></span><br><span data-ttu-id="73a63-154">Ou</span><span class="sxs-lookup"><span data-stu-id="73a63-154">Or</span></span><br/><span data-ttu-id="73a63-155">Você precisa tooknow os trabalhos serão executados imediatamente</span><span class="sxs-lookup"><span data-stu-id="73a63-155">You need tooknow that your jobs will run immediately</span></span><br/><span data-ttu-id="73a63-156">Ou</span><span class="sxs-lookup"><span data-stu-id="73a63-156">Or</span></span><br/><span data-ttu-id="73a63-157">Você precisar de taxa de transferência garantida.</span><span class="sxs-lookup"><span data-stu-id="73a63-157">You need guaranteed throughput.</span></span> <span data-ttu-id="73a63-158">Por exemplo, você precisa toorun um número de trabalhos em um determinado período de tempo e deseja tooscale out seu toomeet de recursos de computação às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="73a63-158">For example, you need toorun a number of jobs in a given time frame, and want tooscale out your compute resources toomeet your needs.</span></span>    | <span data-ttu-id="73a63-159">Você estiver executando apenas alguns trabalhos</span><span class="sxs-lookup"><span data-stu-id="73a63-159">You are running just a few jobs</span></span><br/><span data-ttu-id="73a63-160">e</span><span class="sxs-lookup"><span data-stu-id="73a63-160">And</span></span><br/> <span data-ttu-id="73a63-161">Você não precisa Olá trabalhos toorun imediatamente</span><span class="sxs-lookup"><span data-stu-id="73a63-161">You don’t need hello jobs toorun immediately</span></span> |
