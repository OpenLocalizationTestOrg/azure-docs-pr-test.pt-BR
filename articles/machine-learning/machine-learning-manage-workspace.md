---
title: "um espaço de trabalho do aprendizado de máquina do aaaManage | Microsoft Docs"
description: "Gerenciar espaços de trabalho do access tooAzure aprendizado de máquina, implantar e gerenciar os serviços da web de API ML"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: daf3d413-7a77-4beb-9a7a-6b4bdf717719
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: garye
ms.openlocfilehash: 7bd378d82aa46f4340ca974c7dc5a612c089cdca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-machine-learning-workspace"></a><span data-ttu-id="43ec3-103">Gerenciar um espaço de trabalho do Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="43ec3-103">Manage an Azure Machine Learning workspace</span></span>

> [!NOTE]
> <span data-ttu-id="43ec3-104">Para obter informações sobre como gerenciar serviços Web no portal de serviços de Web do aprendizado de máquina hello, consulte [gerenciar um serviço Web usando o portal de serviços de Web de aprendizado de máquina do Azure Olá](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="43ec3-104">For information on managing Web services in hello Machine Learning Web Services portal, see [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span>
> 
> 

<span data-ttu-id="43ec3-105">Você pode gerenciar espaços de trabalho do aprendizado de máquina em qualquer Olá portal do Azure ou Olá portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="43ec3-105">You can manage Machine Learning workspaces in either hello Azure portal or hello Azure classic portal.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="use-hello-azure-portal"></a><span data-ttu-id="43ec3-106">Use Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="43ec3-106">Use hello Azure portal</span></span>

<span data-ttu-id="43ec3-107">toomanage um espaço de trabalho Olá portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="43ec3-107">toomanage a workspace in hello Azure portal:</span></span>

1. <span data-ttu-id="43ec3-108">Entrar toohello [portal do Azure](https://portal.azure.com/) usando uma conta de administrador de assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="43ec3-108">Sign in toohello [Azure portal](https://portal.azure.com/) using an Azure subscription administrator account.</span></span>
2. <span data-ttu-id="43ec3-109">Na caixa de pesquisa de saudação na parte superior de saudação da página Olá, insira "espaços de trabalho do aprendizado de máquina" e, em seguida, selecione **espaços de trabalho aprendizado de máquina**.</span><span class="sxs-lookup"><span data-stu-id="43ec3-109">In hello search box at hello top of hello page, enter "machine learning workspaces" and then select **Machine Learning Workspaces**.</span></span>
3. <span data-ttu-id="43ec3-110">Clique em espaço de trabalho de saudação deseja toomanage.</span><span class="sxs-lookup"><span data-stu-id="43ec3-110">Click hello workspace you want toomanage.</span></span>

<span data-ttu-id="43ec3-111">Além de informações de gerenciamento de recursos padrão toohello e opções disponíveis, você pode:</span><span class="sxs-lookup"><span data-stu-id="43ec3-111">In addition toohello standard resource management information and options available, you can:</span></span>

- <span data-ttu-id="43ec3-112">Exibição **propriedades** - essa página exibe informações de espaço de trabalho e recursos de Olá, e você pode alterar a assinatura de saudação e o grupo de recursos que esse espaço de trabalho está conectado com.</span><span class="sxs-lookup"><span data-stu-id="43ec3-112">View **Properties** - This page displays hello workspace and resource information, and you can change hello subscription and resource group that this workspace is connected with.</span></span>
- <span data-ttu-id="43ec3-113">**Ressincronizar as chaves de armazenamento** -espaço de trabalho Olá mantém a conta de armazenamento toohello de chaves.</span><span class="sxs-lookup"><span data-stu-id="43ec3-113">**Resync Storage Keys** - hello workspace maintains keys toohello storage account.</span></span> <span data-ttu-id="43ec3-114">Se a conta de armazenamento Olá altera as chaves, então você pode clicar em **Resync chaves** toosynchronize chaves de saudação com espaço de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="43ec3-114">If hello storage account changes keys, then you can click **Resync keys** toosynchronize hello keys with hello workspace.</span></span>

<span data-ttu-id="43ec3-115">Serviços de web hello toomanage associados a este espaço de trabalho, usar o portal de serviços de Web do aprendizado de máquina hello.</span><span class="sxs-lookup"><span data-stu-id="43ec3-115">toomanage hello web services associated with this workspace, use hello Machine Learning Web Services portal.</span></span> <span data-ttu-id="43ec3-116">Consulte [gerenciar um serviço Web usando o portal de serviços de Web de aprendizado de máquina do Azure Olá](machine-learning-manage-new-webservice.md) para obter informações completas.</span><span class="sxs-lookup"><span data-stu-id="43ec3-116">See [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md) for complete information.</span></span>

> [!NOTE]
> <span data-ttu-id="43ec3-117">toodeploy ou gerenciar novos serviços da web, você deve ser atribuído um colaborador ou função de administrador no serviço web do hello assinatura toowhich Olá é implantada.</span><span class="sxs-lookup"><span data-stu-id="43ec3-117">toodeploy or manage New web services you must be assigned a contributor or administrator role on hello subscription toowhich hello web service is deployed.</span></span> <span data-ttu-id="43ec3-118">Se você convidar outro espaço de trabalho de aprendizado de máquina usuário tooa, você deve atribui-los tooa a função Colaborador ou o administrador de assinatura de saudação antes de implantar ou gerenciar os serviços web.</span><span class="sxs-lookup"><span data-stu-id="43ec3-118">If you invite another user tooa machine learning workspace, you must assign them tooa contributor or administrator role on hello subscription before they can deploy or manage web services.</span></span> 
> 
><span data-ttu-id="43ec3-119">Para obter mais informações sobre como definir permissões de acesso, consulte [exibir as atribuições de acesso para usuários e grupos no portal do Azure – visualização pública do hello](../active-directory/role-based-access-control-manage-assignments.md).</span><span class="sxs-lookup"><span data-stu-id="43ec3-119">For more information on setting access permissions, see [View access assignments for users and groups in hello Azure portal - Public preview](../active-directory/role-based-access-control-manage-assignments.md).</span></span>

## <a name="use-hello-azure-classic-portal"></a><span data-ttu-id="43ec3-120">Use Olá portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="43ec3-120">Use hello Azure classic portal</span></span>

<span data-ttu-id="43ec3-121">Usando Olá portal clássico do Azure, você pode gerenciar seus espaços de trabalho do aprendizado de máquina para:</span><span class="sxs-lookup"><span data-stu-id="43ec3-121">Using hello Azure classic portal, you can manage your Machine Learning workspaces to:</span></span>

* <span data-ttu-id="43ec3-122">Monitorar como o espaço de trabalho hello está sendo usado</span><span class="sxs-lookup"><span data-stu-id="43ec3-122">Monitor how hello workspace is being used</span></span>
* <span data-ttu-id="43ec3-123">Configurar Olá tooallow de espaço de trabalho ou negar acesso</span><span class="sxs-lookup"><span data-stu-id="43ec3-123">Configure hello workspace tooallow or deny access</span></span>
* <span data-ttu-id="43ec3-124">Gerenciar serviços Web criados no espaço de trabalho de saudação</span><span class="sxs-lookup"><span data-stu-id="43ec3-124">Manage Web services created in hello workspace</span></span>
* <span data-ttu-id="43ec3-125">Excluir espaço de trabalho de saudação</span><span class="sxs-lookup"><span data-stu-id="43ec3-125">Delete hello workspace</span></span>

<span data-ttu-id="43ec3-126">Além disso, a guia Painel Olá fornece uma visão geral do uso do espaço de trabalho e uma visão geral rápida das suas informações de espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="43ec3-126">In addition, hello dashboard tab provides an overview of your workspace usage and a quick glance of your workspace information.</span></span>  

> [!TIP]
> <span data-ttu-id="43ec3-127">No estúdio de aprendizado de máquina do Azure, em Olá **serviços WEB** guia, você pode adicionar, atualizar ou excluir um serviço Web de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="43ec3-127">In Azure Machine Learning Studio, on hello **WEB SERVICES** tab, you can add, update, or delete a Machine Learning Web service.</span></span>
> 
> 

<span data-ttu-id="43ec3-128">toomanage um espaço de trabalho Olá portal clássico do Azure:</span><span class="sxs-lookup"><span data-stu-id="43ec3-128">toomanage a workspace in hello Azure classic portal:</span></span>

1. <span data-ttu-id="43ec3-129">Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com/) usando o Microsoft Azure conta - use conta Olá associado Olá assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="43ec3-129">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) using your Microsoft Azure account - use hello account that's associated with hello Azure subscription.</span></span>
2. <span data-ttu-id="43ec3-130">No painel de serviços do Microsoft Azure hello, clique em **APRENDIZADO de máquina**.</span><span class="sxs-lookup"><span data-stu-id="43ec3-130">In hello Microsoft Azure services panel, click **MACHINE LEARNING**.</span></span>
3. <span data-ttu-id="43ec3-131">Clique em espaço de trabalho de saudação deseja toomanage.</span><span class="sxs-lookup"><span data-stu-id="43ec3-131">Click hello workspace you want toomanage.</span></span>

<span data-ttu-id="43ec3-132">página de espaço de trabalho Olá tem três guias:</span><span class="sxs-lookup"><span data-stu-id="43ec3-132">hello workspace page has three tabs:</span></span>

* <span data-ttu-id="43ec3-133">**PAINEL** -permite que você tooview uso de espaço de trabalho e informações</span><span class="sxs-lookup"><span data-stu-id="43ec3-133">**DASHBOARD** - Allows you tooview workspace usage and information</span></span>
* <span data-ttu-id="43ec3-134">**CONFIGURAR** -permite que o espaço de trabalho de toohello de acesso toomanage</span><span class="sxs-lookup"><span data-stu-id="43ec3-134">**CONFIGURE** - Allows you toomanage access toohello workspace</span></span>
* <span data-ttu-id="43ec3-135">**SERVIÇOS WEB** -permite que serviços Web toomanage que foram publicados deste espaço de trabalho</span><span class="sxs-lookup"><span data-stu-id="43ec3-135">**WEB SERVICES** - Allows you toomanage Web services that have been published from this workspace</span></span>

### <a name="toomonitor-how-hello-workspace-is-being-used"></a><span data-ttu-id="43ec3-136">toomonitor como o espaço de trabalho hello está sendo usado</span><span class="sxs-lookup"><span data-stu-id="43ec3-136">toomonitor how hello workspace is being used</span></span>
<span data-ttu-id="43ec3-137">Clique em Olá **painel** guia.</span><span class="sxs-lookup"><span data-stu-id="43ec3-137">Click hello **DASHBOARD** tab.</span></span>

<span data-ttu-id="43ec3-138">No painel de saudação, você pode exibir o uso geral do seu espaço de trabalho e obter uma visão geral rápida das informações de espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="43ec3-138">From hello dashboard, you can view overall usage of your workspace and get a quick glance of workspace information.</span></span>

* <span data-ttu-id="43ec3-139">Olá **de computação** gráfico mostra os recursos de computação hello está sendo usados pelo espaço de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="43ec3-139">hello **COMPUTE** chart shows hello compute resources being used by hello workspace.</span></span> <span data-ttu-id="43ec3-140">Você pode alterar Olá exibição toodisplay relativo ou absolutos e você pode alterar o período de tempo de saudação exibido no gráfico de saudação.</span><span class="sxs-lookup"><span data-stu-id="43ec3-140">You can change hello view toodisplay relative or absolute values, and you can change hello timeframe displayed in hello chart.</span></span>
* <span data-ttu-id="43ec3-141">**Visão geral de uso** exibe o armazenamento do Azure que está sendo usado pelo espaço de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="43ec3-141">**Usage overview** displays Azure storage being used by hello workspace.</span></span>
* <span data-ttu-id="43ec3-142">**Visão rápida** fornece um resumo das informações do espaço de trabalho e links úteis.</span><span class="sxs-lookup"><span data-stu-id="43ec3-142">**Quick glance** provides a summary of workspace information and useful links.</span></span>

> [!NOTE]
> <span data-ttu-id="43ec3-143">Olá **tooML entrar Studio** link abre o estúdio de aprendizado de máquina usando Olá Account da Microsoft você está conectado.</span><span class="sxs-lookup"><span data-stu-id="43ec3-143">hello **Sign-in tooML Studio** link opens Machine Learning Studio using hello Microsoft Account you are currently signed into.</span></span> <span data-ttu-id="43ec3-144">Olá Account da Microsoft usada toosign no toohello toocreate portal clássico do Azure um espaço de trabalho não tem automaticamente permissão tooopen esse espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="43ec3-144">hello Microsoft Account you used toosign in toohello Azure classic portal toocreate a workspace does not automatically have permission tooopen that workspace.</span></span> <span data-ttu-id="43ec3-145">tooopen um espaço de trabalho, você deve estar conectado toohello Account da Microsoft que foi definido como proprietário de saudação do espaço de trabalho de saudação ou se precisar de tooreceive um convite de espaço de trabalho da saudação toojoin Olá proprietário.</span><span class="sxs-lookup"><span data-stu-id="43ec3-145">tooopen a workspace, you must be signed in toohello Microsoft Account that was defined as hello owner of hello workspace, or you need tooreceive an invitation from hello owner toojoin hello workspace.</span></span>
> 
> 

### <a name="toogrant-or-suspend-access-for-users"></a><span data-ttu-id="43ec3-146">toogrant ou suspender acesso aos usuários</span><span class="sxs-lookup"><span data-stu-id="43ec3-146">toogrant or suspend access for users</span></span>
<span data-ttu-id="43ec3-147">Clique em Olá **configurar** guia.</span><span class="sxs-lookup"><span data-stu-id="43ec3-147">Click hello **CONFIGURE** tab.</span></span>

<span data-ttu-id="43ec3-148">Na guia de configuração de saudação, você pode:</span><span class="sxs-lookup"><span data-stu-id="43ec3-148">From hello configuration tab you can:</span></span>

* <span data-ttu-id="43ec3-149">Suspenda o espaço de trabalho do aprendizado de máquina do acesso toohello clicando em Negar.</span><span class="sxs-lookup"><span data-stu-id="43ec3-149">Suspend access toohello Machine Learning workspace by clicking DENY.</span></span> <span data-ttu-id="43ec3-150">Os usuários não será capaz de tooopen o espaço de trabalho de saudação no estúdio de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="43ec3-150">Users will no longer be able tooopen hello workspace in Machine Learning Studio.</span></span> <span data-ttu-id="43ec3-151">toorestore acessar, clique em permitir.</span><span class="sxs-lookup"><span data-stu-id="43ec3-151">toorestore access, click ALLOW.</span></span>

<span data-ttu-id="43ec3-152">toomanage outras contas que têm acesso toohello espaço de trabalho no estúdio de aprendizado de máquina, clique em **tooML entrar Studio** em hello **painel** guia (consulte a Observação do hello anterior sobre  **Sign-in tooML Studio**).</span><span class="sxs-lookup"><span data-stu-id="43ec3-152">toomanage additional accounts who have access toohello workspace in Machine Learning Studio, click **Sign-in tooML Studio** in hello **DASHBOARD** tab (see hello preceeding note regarding **Sign-in tooML Studio**).</span></span> <span data-ttu-id="43ec3-153">Isso abre o espaço de trabalho Olá no estúdio de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="43ec3-153">This opens hello workspace in Machine Learning Studio.</span></span> <span data-ttu-id="43ec3-154">Aqui, clique em Olá **configurações** guia e, em seguida, **usuários**.</span><span class="sxs-lookup"><span data-stu-id="43ec3-154">From here, click hello **SETTINGS** tab and then **USERS**.</span></span> <span data-ttu-id="43ec3-155">Você pode clicar em **CONVIDAR usuários mais** toogive usuários acessar toohello de espaço de trabalho, ou selecione um usuário e clique em **remover**.</span><span class="sxs-lookup"><span data-stu-id="43ec3-155">You can click **INVITE MORE USERS** toogive users access toohello workspace, or select a user and click **REMOVE**.</span></span>

### <a name="toomanage-web-services-in-this-workspace"></a><span data-ttu-id="43ec3-156">Serviços de web toomanage neste espaço de trabalho</span><span class="sxs-lookup"><span data-stu-id="43ec3-156">toomanage web services in this workspace</span></span>
<span data-ttu-id="43ec3-157">Clique em Olá **serviços WEB** guia.</span><span class="sxs-lookup"><span data-stu-id="43ec3-157">Click hello **WEB SERVICES** tab.</span></span>

<span data-ttu-id="43ec3-158">Isso exibe uma lista de serviços Web publicados desse espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="43ec3-158">This displays a list of web services published from this workspace.</span></span>
<span data-ttu-id="43ec3-159">toomanage um serviço web, clique em nome de saudação na página de serviço Olá lista tooopen Olá Web.</span><span class="sxs-lookup"><span data-stu-id="43ec3-159">toomanage a web service, click hello name in hello list tooopen hello Web service page.</span></span>

<span data-ttu-id="43ec3-160">Um serviço Web pode ter um ou mais pontos de extremidade definidos.</span><span class="sxs-lookup"><span data-stu-id="43ec3-160">A Web service may have one or more endpoints defined.</span></span>

* <span data-ttu-id="43ec3-161">Você pode definir mais pontos de extremidade no ponto de extremidade de adição toohello "Padrão".</span><span class="sxs-lookup"><span data-stu-id="43ec3-161">You can define more endpoints in addition toohello "Default" endpoint.</span></span> <span data-ttu-id="43ec3-162">tooadd Olá ponto de extremidade, clique em **gerenciar pontos de extremidade** na parte inferior de saudação do portal de serviços de Web de aprendizado de máquina do Azure Olá painel tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="43ec3-162">tooadd hello endpoint, click **Manage Endpoints** at hello bottom of hello dashboard tooopen hello Azure Machine Learning Web Services portal.</span></span>
* <span data-ttu-id="43ec3-163">toodelete um ponto de extremidade (você não pode excluir o ponto de extremidade hello "Padrão"), clique Olá a caixa de seleção no início de saudação da linha do ponto de extremidade hello e clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="43ec3-163">toodelete an endpoint (you cannot delete hello "Default" endpoint), click hello check box at hello beginning of hello endpoint row, and click **DELETE**.</span></span> <span data-ttu-id="43ec3-164">Isso remove o ponto de extremidade Olá Olá serviço Web.</span><span class="sxs-lookup"><span data-stu-id="43ec3-164">This removes hello endpoint from hello Web service.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="43ec3-165">Se um aplicativo estiver usando o ponto de extremidade de serviço de web hello quando o ponto de extremidade de saudação é excluído, o aplicativo hello receberá Olá um erro próxima vez que ele tenta tooaccess serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="43ec3-165">If an application is using hello web service endpoint when hello endpoint is deleted, hello application will receive an error hello next time it tries tooaccess hello service.</span></span>
  > 
  > 

<span data-ttu-id="43ec3-166">Clique em nome de saudação de um tooopen de ponto de extremidade de serviço Web-lo.</span><span class="sxs-lookup"><span data-stu-id="43ec3-166">Click hello name of a Web service endpoint tooopen it.</span></span> 

<span data-ttu-id="43ec3-167">No painel de Olá, você pode exibir o uso geral do serviço Web durante um período de tempo.</span><span class="sxs-lookup"><span data-stu-id="43ec3-167">From hello dashboard, you can view overall usage of your Web service over a period of time.</span></span> <span data-ttu-id="43ec3-168">Você pode selecionar tooview período Olá menu Olá período suspensa no canto superior direito de saudação de gráficos do uso de saudação.</span><span class="sxs-lookup"><span data-stu-id="43ec3-168">You can select hello period tooview from hello Period dropdown menu in hello upper right of hello usage charts.</span></span> <span data-ttu-id="43ec3-169">painel Olá mostra Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="43ec3-169">hello dashboard shows hello following information:</span></span>

* <span data-ttu-id="43ec3-170">**Solicitações ao longo do tempo** exibe um gráfico de etapa do número de saudação de solicitações nos Olá período de tempo selecionado.</span><span class="sxs-lookup"><span data-stu-id="43ec3-170">**Requests Over Time** displays a step graph of hello number of requests over hello selected time period.</span></span> <span data-ttu-id="43ec3-171">Ele pode ajudar a identificar se houver picos de uso.</span><span class="sxs-lookup"><span data-stu-id="43ec3-171">It can help identify if you are experiencing spikes in usage.</span></span>
* <span data-ttu-id="43ec3-172">**Solicitações de solicitação-resposta** exibe Olá o número total de chamadas de solicitação-resposta serviço Olá recebeu via hello período de tempo selecionado e quantos deles falha.</span><span class="sxs-lookup"><span data-stu-id="43ec3-172">**Request-Response Requests** displays hello total number of Request-Response calls hello service has received over hello selected time period and how many of them failed.</span></span>
* <span data-ttu-id="43ec3-173">**Tempo médio de solicitação-resposta de computação** exibe uma média de tempo de saudação necessário tooexecute Olá recebeu solicitações.</span><span class="sxs-lookup"><span data-stu-id="43ec3-173">**Average Request-Response Compute Time** displays an average of hello time needed tooexecute hello received requests.</span></span>
* <span data-ttu-id="43ec3-174">**Solicitações em lote** exibe o número total saudação do serviço de saudação de solicitações em lote recebeu via Olá período de tempo selecionado e quantos deles falha.</span><span class="sxs-lookup"><span data-stu-id="43ec3-174">**Batch Requests** displays hello total number of Batch Requests hello service has received over hello selected time period and how many of them failed.</span></span>
* <span data-ttu-id="43ec3-175">**Média de latência do trabalho** exibe uma média de tempo de saudação necessário tooexecute Olá recebeu solicitações.</span><span class="sxs-lookup"><span data-stu-id="43ec3-175">**Average Job Latency** displays an average of hello time needed tooexecute hello received requests.</span></span>
* <span data-ttu-id="43ec3-176">**Erros** exibe a agregação do número de erros que ocorreram Olá no serviço de web toohello chamadas.</span><span class="sxs-lookup"><span data-stu-id="43ec3-176">**Errors** displays hello aggregate number of errors that have occurred on calls toohello web service.</span></span>
* <span data-ttu-id="43ec3-177">**Custos de serviços** exibe encargos Olá para o plano de cobrança Olá associadas ao serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="43ec3-177">**Services Costs** displays hello charges for hello billing plan associated with hello service.</span></span>

<span data-ttu-id="43ec3-178">Página Configurar de saudação, você pode atualizar Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="43ec3-178">From hello Configure page, you can update hello following properties:</span></span>

* <span data-ttu-id="43ec3-179">**Descrição** permite que você tooenter uma descrição para Olá serviço da Web.</span><span class="sxs-lookup"><span data-stu-id="43ec3-179">**Description** allows you tooenter a description for hello Web service.</span></span> <span data-ttu-id="43ec3-180">Descrição é um campo obrigatório.</span><span class="sxs-lookup"><span data-stu-id="43ec3-180">Description is a required field.</span></span>
* <span data-ttu-id="43ec3-181">**Registro em log** permite erro tooenable ou Desabilitar log no ponto de extremidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="43ec3-181">**Logging** allows you tooenable or disable error logging on hello endpoint.</span></span> <span data-ttu-id="43ec3-182">Para obter mais informações sobre Registrar em Log, veja Habilitar [registro em log de serviços Web do Machine Learning](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="43ec3-182">For more information on Logging, see Enable [logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>
* <span data-ttu-id="43ec3-183">**Habilitar dados de exemplo** permite que você tooprovide dados de exemplo que você pode usar o serviço do tootest Olá solicitação-resposta.</span><span class="sxs-lookup"><span data-stu-id="43ec3-183">**Enable Sample data** allows you tooprovide sample data that you can use tootest hello Request-Response service.</span></span> <span data-ttu-id="43ec3-184">Se você criou o serviço web de saudação no estúdio de aprendizado de máquina, dados de exemplo hello são obtidos da dados saudação seu tootrain usado seu modelo.</span><span class="sxs-lookup"><span data-stu-id="43ec3-184">If you created hello web service in Machine Learning Studio, hello sample data is taken from hello data your used tootrain your model.</span></span> <span data-ttu-id="43ec3-185">Se você criou o serviço Olá programaticamente, dados saudação provém de dados de exemplo hello fornecido como parte do pacote JSON de saudação.</span><span class="sxs-lookup"><span data-stu-id="43ec3-185">If you created hello service programmatically, hello data is taken from hello example data you provided as part of hello JSON package.</span></span>

