---
title: aaaView atividades do Azure registra recursos toomonitor | Microsoft Docs
description: "Use hello atividade registra erros e tooreview ações do usuário. Mostra o Portal do Azure, PowerShell, CLI do Azure e REST."
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
ms.openlocfilehash: 8430ed2a9c1dfe5f13423a55d358e590b0facb22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="view-activity-logs-tooaudit-actions-on-resources"></a><span data-ttu-id="0d067-104">Exibir atividade registra ações de tooaudit em recursos</span><span class="sxs-lookup"><span data-stu-id="0d067-104">View activity logs tooaudit actions on resources</span></span>
<span data-ttu-id="0d067-105">Com os logs de atividade, você pode determinar:</span><span class="sxs-lookup"><span data-stu-id="0d067-105">Through activity logs, you can determine:</span></span>

* <span data-ttu-id="0d067-106">as operações que foram feitas em recursos de saudação em sua assinatura</span><span class="sxs-lookup"><span data-stu-id="0d067-106">what operations were taken on hello resources in your subscription</span></span>
* <span data-ttu-id="0d067-107">Quem iniciou a operação de saudação (embora operações iniciadas por um serviço de back-end não retornam um usuário como chamador Olá)</span><span class="sxs-lookup"><span data-stu-id="0d067-107">who initiated hello operation (although operations initiated by a backend service do not return a user as hello caller)</span></span>
* <span data-ttu-id="0d067-108">Quando a operação de saudação ocorreu</span><span class="sxs-lookup"><span data-stu-id="0d067-108">when hello operation occurred</span></span>
* <span data-ttu-id="0d067-109">status de saudação da operação de saudação</span><span class="sxs-lookup"><span data-stu-id="0d067-109">hello status of hello operation</span></span>
* <span data-ttu-id="0d067-110">valores de saudação de outras propriedades que podem ajudá-lo a pesquisar operação Olá</span><span class="sxs-lookup"><span data-stu-id="0d067-110">hello values of other properties that might help you research hello operation</span></span>

[!INCLUDE [resource-manager-audit-limitations](../../includes/resource-manager-audit-limitations.md)]

<span data-ttu-id="0d067-111">Você pode recuperar informações dos logs de atividade Olá por meio do portal hello, PowerShell, CLI do Azure, Insights API de REST, ou [Insights .NET biblioteca](https://www.nuget.org/packages/Microsoft.Azure.Insights/).</span><span class="sxs-lookup"><span data-stu-id="0d067-111">You can retrieve information from hello activity logs through hello portal, PowerShell, Azure CLI, Insights REST API, or [Insights .NET Library](https://www.nuget.org/packages/Microsoft.Azure.Insights/).</span></span>

## <a name="portal"></a><span data-ttu-id="0d067-112">Portal</span><span class="sxs-lookup"><span data-stu-id="0d067-112">Portal</span></span>
1. <span data-ttu-id="0d067-113">logs de atividade de saudação tooview por meio do portal hello, selecione **Monitor**.</span><span class="sxs-lookup"><span data-stu-id="0d067-113">tooview hello activity logs through hello portal, select **Monitor**.</span></span>
   
    ![selecionar logs de atividade](./media/resource-group-audit/select-monitor.png)

   <span data-ttu-id="0d067-115">Ou então, log de atividades de saudação tooautomatically filtro para um determinado recurso ou grupo de recursos, selecione **log de atividades** da folha de recursos.</span><span class="sxs-lookup"><span data-stu-id="0d067-115">Or, tooautomatically filter hello activity log for a particular resource or resource group, select **Activity log** from that resource blade.</span></span> <span data-ttu-id="0d067-116">Observe que esse log de atividades de saudação é automaticamente filtrado pelo recurso de saudação selecionado.</span><span class="sxs-lookup"><span data-stu-id="0d067-116">Notice that hello activity log is automatically filtered by hello selected resource.</span></span>
   
    ![filtrar por recurso](./media/resource-group-audit/filtered-by-resource.png)
2. <span data-ttu-id="0d067-118">Em Olá **Log de atividades** folha, você ver um resumo das operações recentes.</span><span class="sxs-lookup"><span data-stu-id="0d067-118">In hello **Activity Log** blade, you see a summary of recent operations.</span></span>
   
    ![mostrar ações](./media/resource-group-audit/audit-summary.png)
3. <span data-ttu-id="0d067-120">número de saudação toorestrict de operações, exibido, selecione condições diferentes.</span><span class="sxs-lookup"><span data-stu-id="0d067-120">toorestrict hello number of operations displayed, select different conditions.</span></span> <span data-ttu-id="0d067-121">Por exemplo, hello imagem a seguir mostra Olá **Timespan** e **evento iniciado por** campos alterados tooview Olá ações de um determinado usuário ou aplicativo para Olá mês passado.</span><span class="sxs-lookup"><span data-stu-id="0d067-121">For example, hello following image shows hello **Timespan** and **Event initiated by** fields changed tooview hello actions taken by a particular user or application for hello past month.</span></span> <span data-ttu-id="0d067-122">Selecione **aplicar** tooview resultados de saudação da consulta.</span><span class="sxs-lookup"><span data-stu-id="0d067-122">Select **Apply** tooview hello results of your query.</span></span>
   
    ![definir opções de filtragem](./media/resource-group-audit/set-filter.png)

4. <span data-ttu-id="0d067-124">Se você precisar de consulta de saudação toorun novamente mais tarde, selecione **salvar** e dê um nome de consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="0d067-124">If you need toorun hello query again later, select **Save** and give hello query a name.</span></span>
   
    ![salvar consulta](./media/resource-group-audit/save-query.png)
5. <span data-ttu-id="0d067-126">tooquickly executar uma consulta, você pode selecionar uma das consultas internas hello, como implantações com falha.</span><span class="sxs-lookup"><span data-stu-id="0d067-126">tooquickly run a query, you can select one of hello built-in queries, such as failed deployments.</span></span>

    ![selecionar consulta](./media/resource-group-audit/select-quick-query.png)

   <span data-ttu-id="0d067-128">consulta selecionada Olá automaticamente define valores de filtro Olá necessário.</span><span class="sxs-lookup"><span data-stu-id="0d067-128">hello selected query automatically sets hello required filter values.</span></span>

    ![exibir erros de implantação](./media/resource-group-audit/view-failed-deployment.png)   

6. <span data-ttu-id="0d067-130">Selecione uma saudação operações toosee um resumo do evento hello.</span><span class="sxs-lookup"><span data-stu-id="0d067-130">Select one of hello operations toosee a summary of hello event.</span></span>

    ![exibir operação](./media/resource-group-audit/view-operation.png)  

## <a name="powershell"></a><span data-ttu-id="0d067-132">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0d067-132">PowerShell</span></span>
1. <span data-ttu-id="0d067-133">entradas de log tooretrieve, executadas Olá **AzureRmLog Get** comando.</span><span class="sxs-lookup"><span data-stu-id="0d067-133">tooretrieve log entries, run hello **Get-AzureRmLog** command.</span></span> <span data-ttu-id="0d067-134">Você fornecer a lista de saudação toofilter parâmetros adicionais de entradas.</span><span class="sxs-lookup"><span data-stu-id="0d067-134">You provide additional parameters toofilter hello list of entries.</span></span> <span data-ttu-id="0d067-135">Se você não especificar uma hora de início e término, as entradas para a última hora de saudação são retornadas.</span><span class="sxs-lookup"><span data-stu-id="0d067-135">If you do not specify a start and end time, entries for hello last hour are returned.</span></span> <span data-ttu-id="0d067-136">Por exemplo, executar operações de saudação tooretrieve para um grupo de recursos durante a saudação hora anterior:</span><span class="sxs-lookup"><span data-stu-id="0d067-136">For example, tooretrieve hello operations for a resource group during hello past hour run:</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup
  ```
   
    <span data-ttu-id="0d067-137">saudação de exemplo a seguir mostra como a atividade de saudação toouse log tooresearch operações executadas durante um período especificado.</span><span class="sxs-lookup"><span data-stu-id="0d067-137">hello following example shows how toouse hello activity log tooresearch operations taken during a specified time.</span></span> <span data-ttu-id="0d067-138">Olá datas de início e término são especificadas em um formato de data.</span><span class="sxs-lookup"><span data-stu-id="0d067-138">hello start and end dates are specified in a date format.</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime 2015-08-28T06:00 -EndTime 2015-09-10T06:00
  ```

    <span data-ttu-id="0d067-139">Ou, você pode usar funções toospecify Olá data intervalo de datas, como Olá últimos 14 dias.</span><span class="sxs-lookup"><span data-stu-id="0d067-139">Or, you can use date functions toospecify hello date range, such as hello last 14 days.</span></span>
   
  ```powershell 
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14)
  ```

2. <span data-ttu-id="0d067-140">Dependendo da hora de início de saudação especificado, os comandos anteriores Olá podem retornar uma longa lista de operações para o grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="0d067-140">Depending on hello start time you specify, hello previous commands can return a long list of operations for hello resource group.</span></span> <span data-ttu-id="0d067-141">Você pode filtrar os resultados de saudação para o que você está procurando, fornecendo os critérios de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="0d067-141">You can filter hello results for what you are looking for by providing search criteria.</span></span> <span data-ttu-id="0d067-142">Por exemplo, se você estiver tentando tooresearch como um aplicativo web foi interrompido, você pode executar Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="0d067-142">For example, if you are trying tooresearch how a web app was stopped, you could run hello following command:</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14) | Where-Object OperationName -eq Microsoft.Web/sites/stop/action
  ```

    <span data-ttu-id="0d067-143">Que, para este exemplo, mostra que a ação de parada foi executada por someone@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="0d067-143">Which for this example shows that a stop action was performed by someone@contoso.com.</span></span> 

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

3. <span data-ttu-id="0d067-144">Você pode procurar as ações de saudação realizadas por um determinado usuário, mesmo para um grupo de recursos que não existe mais.</span><span class="sxs-lookup"><span data-stu-id="0d067-144">You can look up hello actions taken by a particular user, even for a resource group that no longer exists.</span></span>

  ```powershell 
  Get-AzureRmLog -ResourceGroup deletedgroup -StartTime (Get-Date).AddDays(-14) -Caller someone@contoso.com
  ```

4. <span data-ttu-id="0d067-145">Você pode filtrar para mostrar operações com falha.</span><span class="sxs-lookup"><span data-stu-id="0d067-145">You can filter for failed operations.</span></span>

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -Status Failed
  ```

5. <span data-ttu-id="0d067-146">Você pode focalizar um erro ao examinar a mensagem de saudação do status para a entrada.</span><span class="sxs-lookup"><span data-stu-id="0d067-146">You can focus on one error by looking at hello status message for that entry.</span></span>
   
        ((Get-AzureRmLog -Status Failed -ResourceGroup ExampleGroup -DetailedOutput).Properties[1].Content["statusMessage"] | ConvertFrom-Json).error
   
    <span data-ttu-id="0d067-147">Que retorna:</span><span class="sxs-lookup"><span data-stu-id="0d067-147">Which returns:</span></span>
   
        code           message                                                                        
        ----           -------                                                                        
        DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. 


## <a name="azure-cli"></a><span data-ttu-id="0d067-148">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="0d067-148">Azure CLI</span></span>
* <span data-ttu-id="0d067-149">entradas de log tooretrieve, executar Olá **grupo do azure log mostrar** comando.</span><span class="sxs-lookup"><span data-stu-id="0d067-149">tooretrieve log entries, you run hello **azure group log show** command.</span></span>

  ```azurecli
  azure group log show ExampleGroup --json
  ```


## <a name="rest-api"></a><span data-ttu-id="0d067-150">API REST</span><span class="sxs-lookup"><span data-stu-id="0d067-150">REST API</span></span>
<span data-ttu-id="0d067-151">operações de REST Olá para trabalhar com o log de atividades de saudação fazem parte da saudação [Insights REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="0d067-151">hello REST operations for working with hello activity log are part of hello [Insights REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span> <span data-ttu-id="0d067-152">eventos de log de atividade de tooretrieve, consulte [liste Olá eventos de gerenciamento em uma assinatura](https://msdn.microsoft.com/library/azure/dn931934.aspx).</span><span class="sxs-lookup"><span data-stu-id="0d067-152">tooretrieve activity log events, see [List hello management events in a subscription](https://msdn.microsoft.com/library/azure/dn931934.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d067-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0d067-153">Next steps</span></span>
* <span data-ttu-id="0d067-154">Logs de atividade do Azure podem ser usados com ideias do Power BI toogain maiores sobre ações de saudação em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="0d067-154">Azure Activity logs can be used with Power BI toogain greater insights about hello actions in your subscription.</span></span> <span data-ttu-id="0d067-155">Confira [View and analyze Azure Activity Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/)(Exibir e analisar logs de atividade do Azure no Power BI e muito mais).</span><span class="sxs-lookup"><span data-stu-id="0d067-155">See [View and analyze Azure Activity Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/).</span></span>
* <span data-ttu-id="0d067-156">toolearn sobre a configuração de políticas de segurança, consulte [controle de acesso baseado em função do Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="0d067-156">toolearn about setting security policies, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>
* <span data-ttu-id="0d067-157">toolearn sobre comandos Olá para exibir as operações de implantação, consulte [Exibir operações de implantação](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="0d067-157">toolearn about hello commands for viewing deployment operations, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="0d067-158">toolearn como tooprevent exclusões em um recurso para todos os usuários, consulte [bloquear recursos do Azure Resource Manager](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="0d067-158">toolearn how tooprevent deletions on a resource for all users, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

