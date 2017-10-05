---
title: Exibir logs de atividades do Azure para monitorar recursos | Microsoft Docs
description: "Use o log de atividade para examinar erros e ações do usuário. Mostra o Portal do Azure, PowerShell, CLI do Azure e REST."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: fcdb3125-13ce-4c3b-9087-f514c5e41e73
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: tomfitz
ms.openlocfilehash: 9f90bc80c146c6c2da04aacbc110f7d389c0baa2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="view-activity-logs-to-audit-actions-on-resources"></a><span data-ttu-id="80d4e-104">Exibir logs de atividade para auditar ações em recursos</span><span class="sxs-lookup"><span data-stu-id="80d4e-104">View activity logs to audit actions on resources</span></span>
<span data-ttu-id="80d4e-105">Com os logs de atividade, você pode determinar:</span><span class="sxs-lookup"><span data-stu-id="80d4e-105">Through activity logs, you can determine:</span></span>

* <span data-ttu-id="80d4e-106">quais operações foram executadas nos recursos em sua assinatura</span><span class="sxs-lookup"><span data-stu-id="80d4e-106">what operations were taken on the resources in your subscription</span></span>
* <span data-ttu-id="80d4e-107">quem iniciou a operação (embora as operações iniciadas por um serviço de back-end não retornem um usuário como o chamador)</span><span class="sxs-lookup"><span data-stu-id="80d4e-107">who initiated the operation (although operations initiated by a backend service do not return a user as the caller)</span></span>
* <span data-ttu-id="80d4e-108">quando a operação ocorreu</span><span class="sxs-lookup"><span data-stu-id="80d4e-108">when the operation occurred</span></span>
* <span data-ttu-id="80d4e-109">o status da operação</span><span class="sxs-lookup"><span data-stu-id="80d4e-109">the status of the operation</span></span>
* <span data-ttu-id="80d4e-110">os valores de outras propriedades que podem ajudar você a pesquisar a operação</span><span class="sxs-lookup"><span data-stu-id="80d4e-110">the values of other properties that might help you research the operation</span></span>

[!INCLUDE [resource-manager-audit-limitations](../../includes/resource-manager-audit-limitations.md)]

<span data-ttu-id="80d4e-111">Você pode recuperar informações dos logs de atividade por meio do Portal, do PowerShell, da CLI do Azure, da API REST do Insights ou da [Biblioteca .NET do Insights](https://www.nuget.org/packages/Microsoft.Azure.Insights/).</span><span class="sxs-lookup"><span data-stu-id="80d4e-111">You can retrieve information from the activity logs through the portal, PowerShell, Azure CLI, Insights REST API, or [Insights .NET Library](https://www.nuget.org/packages/Microsoft.Azure.Insights/).</span></span>

## <a name="portal"></a><span data-ttu-id="80d4e-112">Portal</span><span class="sxs-lookup"><span data-stu-id="80d4e-112">Portal</span></span>
1. <span data-ttu-id="80d4e-113">Para exibir os logs de atividade no portal, escolha **Monitorar**.</span><span class="sxs-lookup"><span data-stu-id="80d4e-113">To view the activity logs through the portal, select **Monitor**.</span></span>
   
    ![selecionar logs de atividade](./media/resource-group-audit/select-monitor.png)

   <span data-ttu-id="80d4e-115">Ou, para filtrar automaticamente o log de atividades para um determinado recurso ou grupo de recursos, selecione **Log de atividades** na folha desse recurso.</span><span class="sxs-lookup"><span data-stu-id="80d4e-115">Or, to automatically filter the activity log for a particular resource or resource group, select **Activity log** from that resource blade.</span></span> <span data-ttu-id="80d4e-116">Observe que o log de atividades é automaticamente filtrado pelo recurso selecionado.</span><span class="sxs-lookup"><span data-stu-id="80d4e-116">Notice that the activity log is automatically filtered by the selected resource.</span></span>
   
    ![filtrar por recurso](./media/resource-group-audit/filtered-by-resource.png)
2. <span data-ttu-id="80d4e-118">Na folha **Log de Atividades**, você vê um resumo das operações recentes.</span><span class="sxs-lookup"><span data-stu-id="80d4e-118">In the **Activity Log** blade, you see a summary of recent operations.</span></span>
   
    ![mostrar ações](./media/resource-group-audit/audit-summary.png)
3. <span data-ttu-id="80d4e-120">Para restringir o número de operações exibidas, selecione condições diferentes.</span><span class="sxs-lookup"><span data-stu-id="80d4e-120">To restrict the number of operations displayed, select different conditions.</span></span> <span data-ttu-id="80d4e-121">Por exemplo, a imagem a seguir mostra os campos **Intervalo de tempo** e **Evento iniciado por** alterados para exibir as ações realizadas por um determinado usuário ou aplicativo no mês passado.</span><span class="sxs-lookup"><span data-stu-id="80d4e-121">For example, the following image shows the **Timespan** and **Event initiated by** fields changed to view the actions taken by a particular user or application for the past month.</span></span> <span data-ttu-id="80d4e-122">Selecione **Aplicar** para exibir os resultados da consulta.</span><span class="sxs-lookup"><span data-stu-id="80d4e-122">Select **Apply** to view the results of your query.</span></span>
   
    ![definir opções de filtragem](./media/resource-group-audit/set-filter.png)

4. <span data-ttu-id="80d4e-124">Se você precisar executar a consulta novamente mais tarde, selecione **Salvar** e nomeie a consulta.</span><span class="sxs-lookup"><span data-stu-id="80d4e-124">If you need to run the query again later, select **Save** and give the query a name.</span></span>
   
    ![salvar consulta](./media/resource-group-audit/save-query.png)
5. <span data-ttu-id="80d4e-126">Para executar rapidamente uma consulta, selecione uma das consultas internas, como falhas de implantação.</span><span class="sxs-lookup"><span data-stu-id="80d4e-126">To quickly run a query, you can select one of the built-in queries, such as failed deployments.</span></span>

    ![selecionar consulta](./media/resource-group-audit/select-quick-query.png)

   <span data-ttu-id="80d4e-128">A consulta selecionada define automaticamente os valores de filtro obrigatórios.</span><span class="sxs-lookup"><span data-stu-id="80d4e-128">The selected query automatically sets the required filter values.</span></span>

    ![exibir erros de implantação](./media/resource-group-audit/view-failed-deployment.png)   

6. <span data-ttu-id="80d4e-130">Selecione uma das operações para ver um resumo do evento.</span><span class="sxs-lookup"><span data-stu-id="80d4e-130">Select one of the operations to see a summary of the event.</span></span>

    ![exibir operação](./media/resource-group-audit/view-operation.png)  

## <a name="powershell"></a><span data-ttu-id="80d4e-132">PowerShell</span><span class="sxs-lookup"><span data-stu-id="80d4e-132">PowerShell</span></span>
1. <span data-ttu-id="80d4e-133">Para recuperar as entradas de log, execute o comando **Get-AzureRmLog** .</span><span class="sxs-lookup"><span data-stu-id="80d4e-133">To retrieve log entries, run the **Get-AzureRmLog** command.</span></span> <span data-ttu-id="80d4e-134">Forneça parâmetros adicionais para filtrar a lista de entradas.</span><span class="sxs-lookup"><span data-stu-id="80d4e-134">You provide additional parameters to filter the list of entries.</span></span> <span data-ttu-id="80d4e-135">Se você não especificar uma hora de início e de término, as entradas da última hora retornarão.</span><span class="sxs-lookup"><span data-stu-id="80d4e-135">If you do not specify a start and end time, entries for the last hour are returned.</span></span> <span data-ttu-id="80d4e-136">Por exemplo, para recuperar as operações de um grupo de recursos durante a execução na última hora:</span><span class="sxs-lookup"><span data-stu-id="80d4e-136">For example, to retrieve the operations for a resource group during the past hour run:</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup
  ```
   
    <span data-ttu-id="80d4e-137">O exemplo a seguir mostra como usar o log de atividades para operações de pesquisa executadas durante um período especificado.</span><span class="sxs-lookup"><span data-stu-id="80d4e-137">The following example shows how to use the activity log to research operations taken during a specified time.</span></span> <span data-ttu-id="80d4e-138">As datas de início e de término são especificadas em um formato de data.</span><span class="sxs-lookup"><span data-stu-id="80d4e-138">The start and end dates are specified in a date format.</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime 2015-08-28T06:00 -EndTime 2015-09-10T06:00
  ```

    <span data-ttu-id="80d4e-139">Outra opção é usar funções de data para especificar o intervalo de datas, como os últimos 14 dias.</span><span class="sxs-lookup"><span data-stu-id="80d4e-139">Or, you can use date functions to specify the date range, such as the last 14 days.</span></span>
   
  ```powershell 
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14)
  ```

2. <span data-ttu-id="80d4e-140">Dependendo da hora de início que você especificar, os comandos anteriores poderão retornar uma longa lista de operações para o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="80d4e-140">Depending on the start time you specify, the previous commands can return a long list of operations for the resource group.</span></span> <span data-ttu-id="80d4e-141">Você pode, pelo fornecimento de critérios de pesquisa, filtrar os resultados para o que você está procurando.</span><span class="sxs-lookup"><span data-stu-id="80d4e-141">You can filter the results for what you are looking for by providing search criteria.</span></span> <span data-ttu-id="80d4e-142">Por exemplo, se estiver tentando pesquisar como um aplicativo Web foi interrompido, você poderá executar o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="80d4e-142">For example, if you are trying to research how a web app was stopped, you could run the following command:</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14) | Where-Object OperationName -eq Microsoft.Web/sites/stop/action
  ```

    <span data-ttu-id="80d4e-143">Que, para este exemplo, mostra que a ação de parada foi executada por someone@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="80d4e-143">Which for this example shows that a stop action was performed by someone@contoso.com.</span></span> 

  ```powershell 
  Authorization     :
  Scope     : /subscriptions/xxxxx/resourcegroups/ExampleGroup/providers/Microsoft.Web/sites/ExampleSite
  Action    : Microsoft.Web/sites/stop/action
  Role      : Subscription Admin
  Condition :
  Caller            : someone@contoso.com
  CorrelationId     : 84beae59-92aa-4662-a6fc-b6fecc0ff8da
  EventSource       : Administrative
  EventTimestamp    : 8/28/2015 4:08:18 PM
  OperationName     : Microsoft.Web/sites/stop/action
  ResourceGroupName : ExampleGroup
  ResourceId        : /subscriptions/xxxxx/resourcegroups/ExampleGroup/providers/Microsoft.Web/sites/ExampleSite
  Status            : Succeeded
  SubscriptionId    : xxxxx
  SubStatus         : OK
  ```

3. <span data-ttu-id="80d4e-144">Você pode procurar as ações realizadas por um determinado usuário, mesmo para um grupo de recursos que não existe mais.</span><span class="sxs-lookup"><span data-stu-id="80d4e-144">You can look up the actions taken by a particular user, even for a resource group that no longer exists.</span></span>

  ```powershell 
  Get-AzureRmLog -ResourceGroup deletedgroup -StartTime (Get-Date).AddDays(-14) -Caller someone@contoso.com
  ```

4. <span data-ttu-id="80d4e-145">Você pode filtrar para mostrar operações com falha.</span><span class="sxs-lookup"><span data-stu-id="80d4e-145">You can filter for failed operations.</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -Status Failed
  ```

5. <span data-ttu-id="80d4e-146">Você pode focar em um erro examinando a mensagem de status dessa entrada.</span><span class="sxs-lookup"><span data-stu-id="80d4e-146">You can focus on one error by looking at the status message for that entry.</span></span>
   
        ((Get-AzureRmLog -Status Failed -ResourceGroup ExampleGroup -DetailedOutput).Properties[1].Content["statusMessage"] | ConvertFrom-Json).error
   
    <span data-ttu-id="80d4e-147">Que retorna:</span><span class="sxs-lookup"><span data-stu-id="80d4e-147">Which returns:</span></span>
   
        code           message                                                                        
        ----           -------                                                                        
        DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. 


## <a name="azure-cli"></a><span data-ttu-id="80d4e-148">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="80d4e-148">Azure CLI</span></span>
* <span data-ttu-id="80d4e-149">Para recuperar as entradas de log, execute o comando **azure group log show** .</span><span class="sxs-lookup"><span data-stu-id="80d4e-149">To retrieve log entries, you run the **azure group log show** command.</span></span>

  ```azurecli
  azure group log show ExampleGroup --json
  ```


## <a name="rest-api"></a><span data-ttu-id="80d4e-150">API REST</span><span class="sxs-lookup"><span data-stu-id="80d4e-150">REST API</span></span>
<span data-ttu-id="80d4e-151">As operações de REST para trabalhar com o log de atividade fazem parte da [API REST do Insights](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="80d4e-151">The REST operations for working with the activity log are part of the [Insights REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span> <span data-ttu-id="80d4e-152">Para recuperar os eventos de log de atividade, confira [Listar os eventos de gerenciamento em uma assinatura](https://msdn.microsoft.com/library/azure/dn931934.aspx).</span><span class="sxs-lookup"><span data-stu-id="80d4e-152">To retrieve activity log events, see [List the management events in a subscription](https://msdn.microsoft.com/library/azure/dn931934.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="80d4e-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="80d4e-153">Next steps</span></span>
* <span data-ttu-id="80d4e-154">Os logs de atividade do Azure podem ser usados com o Power BI para obter mais informações sobre as ações em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="80d4e-154">Azure Activity logs can be used with Power BI to gain greater insights about the actions in your subscription.</span></span> <span data-ttu-id="80d4e-155">Confira [View and analyze Azure Activity Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/)(Exibir e analisar logs de atividade do Azure no Power BI e muito mais).</span><span class="sxs-lookup"><span data-stu-id="80d4e-155">See [View and analyze Azure Activity Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/).</span></span>
* <span data-ttu-id="80d4e-156">Para aprender sobre como definir políticas de segurança, confira [Controle de acesso baseado em função do Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="80d4e-156">To learn about setting security policies, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>
* <span data-ttu-id="80d4e-157">Para saber mais sobre os comandos para exibir as operações de implantação, consulte [Exibir operações de implantação](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="80d4e-157">To learn about the commands for viewing deployment operations, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="80d4e-158">Para saber como impedir exclusões em um recurso para todos os usuários, confira [Bloquear recursos com o Azure Resource Manager](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="80d4e-158">To learn how to prevent deletions on a resource for all users, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

