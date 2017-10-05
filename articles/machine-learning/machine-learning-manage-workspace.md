---
title: "Gerenciar um espaço de trabalho do Machine Learning | Microsoft Docs"
description: "Gerencie o acesso aos espaços de trabalho de Azure Machine Learning e implante e gerencie serviços Web da API ML"
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
ms.openlocfilehash: 94800f51baf83311c33490cada5f991ff2101da9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-an-azure-machine-learning-workspace"></a><span data-ttu-id="c8c70-103">Gerenciar um espaço de trabalho do Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="c8c70-103">Manage an Azure Machine Learning workspace</span></span>

> [!NOTE]
> <span data-ttu-id="c8c70-104">Para obter informações sobre como gerenciar serviços Web no portal de serviços Web do Machine Learning, veja [Gerenciar um serviço Web usando o portal de serviços Web do Azure Machine Learning](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="c8c70-104">For information on managing Web services in the Machine Learning Web Services portal, see [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span>
> 
> 

<span data-ttu-id="c8c70-105">Você pode gerenciar seus espaços de trabalho do Machine Learning no portal do Azure ou no portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="c8c70-105">You can manage Machine Learning workspaces in either the Azure portal or the Azure classic portal.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="use-the-azure-portal"></a><span data-ttu-id="c8c70-106">Use o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c8c70-106">Use the Azure portal</span></span>

<span data-ttu-id="c8c70-107">Para gerenciar um espaço de trabalho no portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="c8c70-107">To manage a workspace in the Azure portal:</span></span>

1. <span data-ttu-id="c8c70-108">Entre no [Portal do Azure](https://portal.azure.com/) usando uma conta de administrador de assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="c8c70-108">Sign in to the [Azure portal](https://portal.azure.com/) using an Azure subscription administrator account.</span></span>
2. <span data-ttu-id="c8c70-109">Na caixa de pesquisa na parte superior da página, insira "espaços de trabalho do machine learning" e, em seguida, escolha **Espaço de Trabalho do Machine Learning**.</span><span class="sxs-lookup"><span data-stu-id="c8c70-109">In the search box at the top of the page, enter "machine learning workspaces" and then select **Machine Learning Workspaces**.</span></span>
3. <span data-ttu-id="c8c70-110">Clique no espaço de trabalho que você deseja gerenciar.</span><span class="sxs-lookup"><span data-stu-id="c8c70-110">Click the workspace you want to manage.</span></span>

<span data-ttu-id="c8c70-111">Além das informações de gerenciamento de recursos padrão e das opções disponíveis, você pode:</span><span class="sxs-lookup"><span data-stu-id="c8c70-111">In addition to the standard resource management information and options available, you can:</span></span>

- <span data-ttu-id="c8c70-112">Exibir **Propriedades** - essa página exibe as informações do espaço de trabalho e dos recursos e você pode alterar o assinatura e o grupo de recursos aos quais esse espaço de trabalho está conectado.</span><span class="sxs-lookup"><span data-stu-id="c8c70-112">View **Properties** - This page displays the workspace and resource information, and you can change the subscription and resource group that this workspace is connected with.</span></span>
- <span data-ttu-id="c8c70-113">**Ressincronizar as Chaves de Armazenamento** - o espaço de trabalho mantém chaves para a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c8c70-113">**Resync Storage Keys** - The workspace maintains keys to the storage account.</span></span> <span data-ttu-id="c8c70-114">Se a conta de armazenamento alterar as chaves, clique em **Ressincronizar chaves** para sincronizar as chaves com o espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="c8c70-114">If the storage account changes keys, then you can click **Resync keys** to synchronize the keys with the workspace.</span></span>

<span data-ttu-id="c8c70-115">Para gerenciar os serviços Web associados a esse espaço de trabalho, use o Portal de Serviços Web do Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="c8c70-115">To manage the web services associated with this workspace, use the Machine Learning Web Services portal.</span></span> <span data-ttu-id="c8c70-116">Consulte [Gerenciar um serviço Web usando o portal de Serviços Web do Azure Machine Learning](machine-learning-manage-new-webservice.md) para obter informações completas.</span><span class="sxs-lookup"><span data-stu-id="c8c70-116">See [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md) for complete information.</span></span>

> [!NOTE]
> <span data-ttu-id="c8c70-117">Para implantar ou gerenciar Novos serviços Web, você deverá ser atribuído a uma função de colaborador ou de administrador na assinatura na qual o serviço Web é implantado.</span><span class="sxs-lookup"><span data-stu-id="c8c70-117">To deploy or manage New web services you must be assigned a contributor or administrator role on the subscription to which the web service is deployed.</span></span> <span data-ttu-id="c8c70-118">Se você convidar outro usuário para um espaço de trabalho do Machine Learning, deverá atribuí-lo a uma função de colaborador ou de administrador na assinatura antes de implantar ou gerenciar os serviços Web.</span><span class="sxs-lookup"><span data-stu-id="c8c70-118">If you invite another user to a machine learning workspace, you must assign them to a contributor or administrator role on the subscription before they can deploy or manage web services.</span></span> 
> 
><span data-ttu-id="c8c70-119">Para obter mais informações sobre como configurar permissões de acesso, consulte [Exibir atribuições de acesso para usuários e grupos no portal do Azure – Visualização pública](../active-directory/role-based-access-control-manage-assignments.md).</span><span class="sxs-lookup"><span data-stu-id="c8c70-119">For more information on setting access permissions, see [View access assignments for users and groups in the Azure portal - Public preview](../active-directory/role-based-access-control-manage-assignments.md).</span></span>

## <a name="use-the-azure-classic-portal"></a><span data-ttu-id="c8c70-120">Use o portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="c8c70-120">Use the Azure classic portal</span></span>

<span data-ttu-id="c8c70-121">Com o Portal Clássico do Azure, você pode gerenciar seus espaços de trabalho do Machine Learning para:</span><span class="sxs-lookup"><span data-stu-id="c8c70-121">Using the Azure classic portal, you can manage your Machine Learning workspaces to:</span></span>

* <span data-ttu-id="c8c70-122">Monitorar como o espaço de trabalho está sendo usado</span><span class="sxs-lookup"><span data-stu-id="c8c70-122">Monitor how the workspace is being used</span></span>
* <span data-ttu-id="c8c70-123">Configurar o espaço de trabalho para permitir ou negar acesso</span><span class="sxs-lookup"><span data-stu-id="c8c70-123">Configure the workspace to allow or deny access</span></span>
* <span data-ttu-id="c8c70-124">Gerenciar serviços Web criados no espaço de trabalho</span><span class="sxs-lookup"><span data-stu-id="c8c70-124">Manage Web services created in the workspace</span></span>
* <span data-ttu-id="c8c70-125">Excluir o espaço de trabalho</span><span class="sxs-lookup"><span data-stu-id="c8c70-125">Delete the workspace</span></span>

<span data-ttu-id="c8c70-126">Além disso, a guia do painel fornece uma visão geral do uso do espaço de trabalho e uma breve explicação das informações do espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="c8c70-126">In addition, the dashboard tab provides an overview of your workspace usage and a quick glance of your workspace information.</span></span>  

> [!TIP]
> <span data-ttu-id="c8c70-127">No Azure Machine Learning Studio, na guia **SERVIÇOS WEB**, você pode adicionar, atualizar ou excluir um serviço Web do Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="c8c70-127">In Azure Machine Learning Studio, on the **WEB SERVICES** tab, you can add, update, or delete a Machine Learning Web service.</span></span>
> 
> 

<span data-ttu-id="c8c70-128">Para gerenciar um espaço de trabalho no portal clássico do Azure:</span><span class="sxs-lookup"><span data-stu-id="c8c70-128">To manage a workspace in the Azure classic portal:</span></span>

1. <span data-ttu-id="c8c70-129">Entre no [Portal Clássico do Azure](https://manage.windowsazure.com/) usando sua conta do Microsoft Azure – use a conta que está associada à assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="c8c70-129">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) using your Microsoft Azure account - use the account that's associated with the Azure subscription.</span></span>
2. <span data-ttu-id="c8c70-130">No painel de serviços do Microsoft Azure, clique em **APRENDIZADO DE MÁQUINA**.</span><span class="sxs-lookup"><span data-stu-id="c8c70-130">In the Microsoft Azure services panel, click **MACHINE LEARNING**.</span></span>
3. <span data-ttu-id="c8c70-131">Clique no espaço de trabalho que você deseja gerenciar.</span><span class="sxs-lookup"><span data-stu-id="c8c70-131">Click the workspace you want to manage.</span></span>

<span data-ttu-id="c8c70-132">A página do espaço de trabalho tem três guias:</span><span class="sxs-lookup"><span data-stu-id="c8c70-132">The workspace page has three tabs:</span></span>

* <span data-ttu-id="c8c70-133">**PAINEL** - permite que você exiba o uso e as informações do espaço de trabalho</span><span class="sxs-lookup"><span data-stu-id="c8c70-133">**DASHBOARD** - Allows you to view workspace usage and information</span></span>
* <span data-ttu-id="c8c70-134">**CONFIGURAR** - permite que você gerencie o acesso ao espaço de trabalho</span><span class="sxs-lookup"><span data-stu-id="c8c70-134">**CONFIGURE** - Allows you to manage access to the workspace</span></span>
* <span data-ttu-id="c8c70-135">**SERVIÇOS WEB** - permite que você gerencie serviços Web que foram publicados deste espaço de trabalho</span><span class="sxs-lookup"><span data-stu-id="c8c70-135">**WEB SERVICES** - Allows you to manage Web services that have been published from this workspace</span></span>

### <a name="to-monitor-how-the-workspace-is-being-used"></a><span data-ttu-id="c8c70-136">Para monitorar como o espaço de trabalho está sendo usado</span><span class="sxs-lookup"><span data-stu-id="c8c70-136">To monitor how the workspace is being used</span></span>
<span data-ttu-id="c8c70-137">Clique na guia **PAINEL** .</span><span class="sxs-lookup"><span data-stu-id="c8c70-137">Click the **DASHBOARD** tab.</span></span>

<span data-ttu-id="c8c70-138">No painel, você pode exibir o uso geral do espaço de trabalho e ter uma visão rápida das informações do espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="c8c70-138">From the dashboard, you can view overall usage of your workspace and get a quick glance of workspace information.</span></span>

* <span data-ttu-id="c8c70-139">O gráfico **COMPUTAR** mostra os recursos de computação que estão sendo usados pelo espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="c8c70-139">The **COMPUTE** chart shows the compute resources being used by the workspace.</span></span> <span data-ttu-id="c8c70-140">Você pode alterar o modo de exibição para exibir valores relativos ou absolutos e pode alterar o período de tempo exibido no gráfico.</span><span class="sxs-lookup"><span data-stu-id="c8c70-140">You can change the view to display relative or absolute values, and you can change the timeframe displayed in the chart.</span></span>
* <span data-ttu-id="c8c70-141">**Visão geral de uso** exibe o armazenamento do Azure que está sendo usado pelo espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="c8c70-141">**Usage overview** displays Azure storage being used by the workspace.</span></span>
* <span data-ttu-id="c8c70-142">**Visão rápida** fornece um resumo das informações do espaço de trabalho e links úteis.</span><span class="sxs-lookup"><span data-stu-id="c8c70-142">**Quick glance** provides a summary of workspace information and useful links.</span></span>

> [!NOTE]
> <span data-ttu-id="c8c70-143">O link **Entrar no Estúdio AM** abre o Machine Learning Studio usando a conta da Microsoft com a qual você está conectado no momento.</span><span class="sxs-lookup"><span data-stu-id="c8c70-143">The **Sign-in to ML Studio** link opens Machine Learning Studio using the Microsoft Account you are currently signed into.</span></span> <span data-ttu-id="c8c70-144">A Conta da Microsoft que você usou para entrar no Portal Clássico do Azure para criar um espaço de trabalho não tem automaticamente permissão para abrir esse espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="c8c70-144">The Microsoft Account you used to sign in to the Azure classic portal to create a workspace does not automatically have permission to open that workspace.</span></span> <span data-ttu-id="c8c70-145">Para abrir um espaço de trabalho, você deve estar conectado à Conta da Microsoft que foi definido como proprietária do espaço de trabalho ou você precisa receber um convite do proprietário para ingressar no espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="c8c70-145">To open a workspace, you must be signed in to the Microsoft Account that was defined as the owner of the workspace, or you need to receive an invitation from the owner to join the workspace.</span></span>
> 
> 

### <a name="to-grant-or-suspend-access-for-users"></a><span data-ttu-id="c8c70-146">Para conceder ou suspender acesso para usuários</span><span class="sxs-lookup"><span data-stu-id="c8c70-146">To grant or suspend access for users</span></span>
<span data-ttu-id="c8c70-147">Clique na guia **CONFIGURAR** .</span><span class="sxs-lookup"><span data-stu-id="c8c70-147">Click the **CONFIGURE** tab.</span></span>

<span data-ttu-id="c8c70-148">Na guia de configuração, você pode:</span><span class="sxs-lookup"><span data-stu-id="c8c70-148">From the configuration tab you can:</span></span>

* <span data-ttu-id="c8c70-149">Suspender o acesso ao espaço de trabalho do Machine Learning clicando em NEGAR.</span><span class="sxs-lookup"><span data-stu-id="c8c70-149">Suspend access to the Machine Learning workspace by clicking DENY.</span></span> <span data-ttu-id="c8c70-150">Os usuários não poderão mais abrir o espaço de trabalho no Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="c8c70-150">Users will no longer be able to open the workspace in Machine Learning Studio.</span></span> <span data-ttu-id="c8c70-151">Para restaurar o acesso, clique em PERMITIR.</span><span class="sxs-lookup"><span data-stu-id="c8c70-151">To restore access, click ALLOW.</span></span>

<span data-ttu-id="c8c70-152">Para gerenciar as contas adicionais quem têm acesso ao espaço de trabalho no Machine Learning Studio, clique em **Entrar no Estúdio AM** na guia **PAINEL** (consulte a observação acima sobre **Entrar no Estúdio AM**).</span><span class="sxs-lookup"><span data-stu-id="c8c70-152">To manage additional accounts who have access to the workspace in Machine Learning Studio, click **Sign-in to ML Studio** in the **DASHBOARD** tab (see the preceeding note regarding **Sign-in to ML Studio**).</span></span> <span data-ttu-id="c8c70-153">Isso abre o espaço de trabalho no Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="c8c70-153">This opens the workspace in Machine Learning Studio.</span></span> <span data-ttu-id="c8c70-154">Daqui, clique na guia **CONFIGURAÇÕES** e, em seguida, em **USUÁRIOS**.</span><span class="sxs-lookup"><span data-stu-id="c8c70-154">From here, click the **SETTINGS** tab and then **USERS**.</span></span> <span data-ttu-id="c8c70-155">Você pode clicar em **CONVIDAR MAIS USUÁRIOS** para dar acesso aos usuários ao espaço de trabalho, ou selecionar um usuário e clicar em **REMOVER**.</span><span class="sxs-lookup"><span data-stu-id="c8c70-155">You can click **INVITE MORE USERS** to give users access to the workspace, or select a user and click **REMOVE**.</span></span>

### <a name="to-manage-web-services-in-this-workspace"></a><span data-ttu-id="c8c70-156">Para gerenciar os serviços Web neste espaço de trabalho</span><span class="sxs-lookup"><span data-stu-id="c8c70-156">To manage web services in this workspace</span></span>
<span data-ttu-id="c8c70-157">Clique na  guia **SERVIÇOS WEB** .</span><span class="sxs-lookup"><span data-stu-id="c8c70-157">Click the **WEB SERVICES** tab.</span></span>

<span data-ttu-id="c8c70-158">Isso exibe uma lista de serviços Web publicados desse espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="c8c70-158">This displays a list of web services published from this workspace.</span></span>
<span data-ttu-id="c8c70-159">Para gerenciar um serviço Web, clique no nome na lista para abrir a página do serviço Web.</span><span class="sxs-lookup"><span data-stu-id="c8c70-159">To manage a web service, click the name in the list to open the Web service page.</span></span>

<span data-ttu-id="c8c70-160">Um serviço Web pode ter um ou mais pontos de extremidade definidos.</span><span class="sxs-lookup"><span data-stu-id="c8c70-160">A Web service may have one or more endpoints defined.</span></span>

* <span data-ttu-id="c8c70-161">Você pode definir mais pontos de extremidade além do ponto de extremidade "Padrão".</span><span class="sxs-lookup"><span data-stu-id="c8c70-161">You can define more endpoints in addition to the "Default" endpoint.</span></span> <span data-ttu-id="c8c70-162">Para adicionar o ponto de extremidade, clique em **Gerenciar Pontos de Extremidade** na parte inferior do painel para abrir o portal de serviços Web do Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="c8c70-162">To add the endpoint, click **Manage Endpoints** at the bottom of the dashboard to open the Azure Machine Learning Web Services portal.</span></span>
* <span data-ttu-id="c8c70-163">Para excluir um ponto de extremidade (você não pode excluir o ponto de extremidade "Padrão"), clique na caixa de seleção no início da linha do ponto de extremidade e clique em **EXCLUIR**.</span><span class="sxs-lookup"><span data-stu-id="c8c70-163">To delete an endpoint (you cannot delete the "Default" endpoint), click the check box at the beginning of the endpoint row, and click **DELETE**.</span></span> <span data-ttu-id="c8c70-164">Isso remove o ponto de extremidade do serviço Web.</span><span class="sxs-lookup"><span data-stu-id="c8c70-164">This removes the endpoint from the Web service.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="c8c70-165">Se um aplicativo estiver usando o ponto de extremidade do serviço Web quando o ponto de extremidade for excluído, o aplicativo receberá um erro na próxima vez que tentar acessar o serviço.</span><span class="sxs-lookup"><span data-stu-id="c8c70-165">If an application is using the web service endpoint when the endpoint is deleted, the application will receive an error the next time it tries to access the service.</span></span>
  > 
  > 

<span data-ttu-id="c8c70-166">Clique no nome de um ponto de extremidade de serviço Web para abri-lo.</span><span class="sxs-lookup"><span data-stu-id="c8c70-166">Click the name of a Web service endpoint to open it.</span></span> 

<span data-ttu-id="c8c70-167">No painel, você pode exibir o uso geral do serviço Web em um período de tempo.</span><span class="sxs-lookup"><span data-stu-id="c8c70-167">From the dashboard, you can view overall usage of your Web service over a period of time.</span></span> <span data-ttu-id="c8c70-168">Você pode selecionar o período para exibir no menu suspenso Período no canto superior direito dos gráficos de uso.</span><span class="sxs-lookup"><span data-stu-id="c8c70-168">You can select the period to view from the Period dropdown menu in the upper right of the usage charts.</span></span> <span data-ttu-id="c8c70-169">O painel mostra as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="c8c70-169">The dashboard shows the following information:</span></span>

* <span data-ttu-id="c8c70-170">**Solicitações ao longo do tempo** exibe um gráfico de etapa do número de solicitações ao longo do período selecionado.</span><span class="sxs-lookup"><span data-stu-id="c8c70-170">**Requests Over Time** displays a step graph of the number of requests over the selected time period.</span></span> <span data-ttu-id="c8c70-171">Ele pode ajudar a identificar se houver picos de uso.</span><span class="sxs-lookup"><span data-stu-id="c8c70-171">It can help identify if you are experiencing spikes in usage.</span></span>
* <span data-ttu-id="c8c70-172">**Solicitações de solicitação-resposta** exibe o número total de chamadas de solicitação-resposta que o serviço recebeu no período de tempo selecionado e quantos deles falharam.</span><span class="sxs-lookup"><span data-stu-id="c8c70-172">**Request-Response Requests** displays the total number of Request-Response calls the service has received over the selected time period and how many of them failed.</span></span>
* <span data-ttu-id="c8c70-173">**Tempo médio de computação de solicitação-resposta** exibe uma média do tempo necessário para executar as solicitações recebidas.</span><span class="sxs-lookup"><span data-stu-id="c8c70-173">**Average Request-Response Compute Time** displays an average of the time needed to execute the received requests.</span></span>
* <span data-ttu-id="c8c70-174">**Solicitações de lote** exibe o número total de chamadas de lote que o serviço recebeu no período de tempo selecionado e quantos deles falharam.</span><span class="sxs-lookup"><span data-stu-id="c8c70-174">**Batch Requests** displays the total number of Batch Requests the service has received over the selected time period and how many of them failed.</span></span>
* <span data-ttu-id="c8c70-175">**Latência média de trabalho** exibe uma média do tempo necessário para executar as solicitações recebidas.</span><span class="sxs-lookup"><span data-stu-id="c8c70-175">**Average Job Latency** displays an average of the time needed to execute the received requests.</span></span>
* <span data-ttu-id="c8c70-176">**Erros** exibe o número total de erros que ocorreram em chamadas para o serviço Web.</span><span class="sxs-lookup"><span data-stu-id="c8c70-176">**Errors** displays the aggregate number of errors that have occurred on calls to the web service.</span></span>
* <span data-ttu-id="c8c70-177">**Custos de serviços** exibe os encargos para o plano de faturamento associado ao serviço.</span><span class="sxs-lookup"><span data-stu-id="c8c70-177">**Services Costs** displays the charges for the billing plan associated with the service.</span></span>

<span data-ttu-id="c8c70-178">Na página Configurar, você pode atualizar as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="c8c70-178">From the Configure page, you can update the following properties:</span></span>

* <span data-ttu-id="c8c70-179">**Descrição** permite inserir uma descrição para o serviço Web.</span><span class="sxs-lookup"><span data-stu-id="c8c70-179">**Description** allows you to enter a description for the Web service.</span></span> <span data-ttu-id="c8c70-180">Descrição é um campo obrigatório.</span><span class="sxs-lookup"><span data-stu-id="c8c70-180">Description is a required field.</span></span>
* <span data-ttu-id="c8c70-181">**Registrar em log** permite habilitar ou desabilitar o registro de erros em log no ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="c8c70-181">**Logging** allows you to enable or disable error logging on the endpoint.</span></span> <span data-ttu-id="c8c70-182">Para obter mais informações sobre Registrar em Log, veja Habilitar [registro em log de serviços Web do Machine Learning](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="c8c70-182">For more information on Logging, see Enable [logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>
* <span data-ttu-id="c8c70-183">**Habilitar dados de Exemplo** permite que você forneça dados de exemplo que podem ser usados para testar o seu serviço de Solicitação-Resposta.</span><span class="sxs-lookup"><span data-stu-id="c8c70-183">**Enable Sample data** allows you to provide sample data that you can use to test the Request-Response service.</span></span> <span data-ttu-id="c8c70-184">Se você criou o serviço Web no Machine Learning Studio, os dados de exemplo são retirados dos dados usados para treinar seu modelo.</span><span class="sxs-lookup"><span data-stu-id="c8c70-184">If you created the web service in Machine Learning Studio, the sample data is taken from the data your used to train your model.</span></span> <span data-ttu-id="c8c70-185">Se você criou o serviço programaticamente, os dados foram extraídos dos dados de exemplo fornecidos como parte do pacote JSON.</span><span class="sxs-lookup"><span data-stu-id="c8c70-185">If you created the service programmatically, the data is taken from the example data you provided as part of the JSON package.</span></span>

