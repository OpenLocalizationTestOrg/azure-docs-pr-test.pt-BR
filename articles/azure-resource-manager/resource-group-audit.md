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
# <a name="view-activity-logs-tooaudit-actions-on-resources"></a>Exibir atividade registra ações de tooaudit em recursos
Com os logs de atividade, você pode determinar:

* as operações que foram feitas em recursos de saudação em sua assinatura
* Quem iniciou a operação de saudação (embora operações iniciadas por um serviço de back-end não retornam um usuário como chamador Olá)
* Quando a operação de saudação ocorreu
* status de saudação da operação de saudação
* valores de saudação de outras propriedades que podem ajudá-lo a pesquisar operação Olá

[!INCLUDE [resource-manager-audit-limitations](../../includes/resource-manager-audit-limitations.md)]

Você pode recuperar informações dos logs de atividade Olá por meio do portal hello, PowerShell, CLI do Azure, Insights API de REST, ou [Insights .NET biblioteca](https://www.nuget.org/packages/Microsoft.Azure.Insights/).

## <a name="portal"></a>Portal
1. logs de atividade de saudação tooview por meio do portal hello, selecione **Monitor**.
   
    ![selecionar logs de atividade](./media/resource-group-audit/select-monitor.png)

   Ou então, log de atividades de saudação tooautomatically filtro para um determinado recurso ou grupo de recursos, selecione **log de atividades** da folha de recursos. Observe que esse log de atividades de saudação é automaticamente filtrado pelo recurso de saudação selecionado.
   
    ![filtrar por recurso](./media/resource-group-audit/filtered-by-resource.png)
2. Em Olá **Log de atividades** folha, você ver um resumo das operações recentes.
   
    ![mostrar ações](./media/resource-group-audit/audit-summary.png)
3. número de saudação toorestrict de operações, exibido, selecione condições diferentes. Por exemplo, hello imagem a seguir mostra Olá **Timespan** e **evento iniciado por** campos alterados tooview Olá ações de um determinado usuário ou aplicativo para Olá mês passado. Selecione **aplicar** tooview resultados de saudação da consulta.
   
    ![definir opções de filtragem](./media/resource-group-audit/set-filter.png)

4. Se você precisar de consulta de saudação toorun novamente mais tarde, selecione **salvar** e dê um nome de consulta de saudação.
   
    ![salvar consulta](./media/resource-group-audit/save-query.png)
5. tooquickly executar uma consulta, você pode selecionar uma das consultas internas hello, como implantações com falha.

    ![selecionar consulta](./media/resource-group-audit/select-quick-query.png)

   consulta selecionada Olá automaticamente define valores de filtro Olá necessário.

    ![exibir erros de implantação](./media/resource-group-audit/view-failed-deployment.png)   

6. Selecione uma saudação operações toosee um resumo do evento hello.

    ![exibir operação](./media/resource-group-audit/view-operation.png)  

## <a name="powershell"></a>PowerShell
1. entradas de log tooretrieve, executadas Olá **AzureRmLog Get** comando. Você fornecer a lista de saudação toofilter parâmetros adicionais de entradas. Se você não especificar uma hora de início e término, as entradas para a última hora de saudação são retornadas. Por exemplo, executar operações de saudação tooretrieve para um grupo de recursos durante a saudação hora anterior:

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup
  ```
   
    saudação de exemplo a seguir mostra como a atividade de saudação toouse log tooresearch operações executadas durante um período especificado. Olá datas de início e término são especificadas em um formato de data.

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime 2015-08-28T06:00 -EndTime 2015-09-10T06:00
  ```

    Ou, você pode usar funções toospecify Olá data intervalo de datas, como Olá últimos 14 dias.
   
  ```powershell 
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14)
  ```

2. Dependendo da hora de início de saudação especificado, os comandos anteriores Olá podem retornar uma longa lista de operações para o grupo de recursos de saudação. Você pode filtrar os resultados de saudação para o que você está procurando, fornecendo os critérios de pesquisa. Por exemplo, se você estiver tentando tooresearch como um aplicativo web foi interrompido, você pode executar Olá comando a seguir:

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -StartTime (Get-Date).AddDays(-14) | Where-Object OperationName -eq Microsoft.Web/sites/stop/action
  ```

    Que, para este exemplo, mostra que a ação de parada foi executada por someone@contoso.com. 

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

3. Você pode procurar as ações de saudação realizadas por um determinado usuário, mesmo para um grupo de recursos que não existe mais.

  ```powershell 
  Get-AzureRmLog -ResourceGroup deletedgroup -StartTime (Get-Date).AddDays(-14) -Caller someone@contoso.com
  ```

4. Você pode filtrar para mostrar operações com falha.

  ```powershell
  Get-AzureRmLog -ResourceGroup ExampleGroup -Status Failed
  ```

5. Você pode focalizar um erro ao examinar a mensagem de saudação do status para a entrada.
   
        ((Get-AzureRmLog -Status Failed -ResourceGroup ExampleGroup -DetailedOutput).Properties[1].Content["statusMessage"] | ConvertFrom-Json).error
   
    Que retorna:
   
        code           message                                                                        
        ----           -------                                                                        
        DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. 


## <a name="azure-cli"></a>CLI do Azure
* entradas de log tooretrieve, executar Olá **grupo do azure log mostrar** comando.

  ```azurecli
  azure group log show ExampleGroup --json
  ```


## <a name="rest-api"></a>API REST
operações de REST Olá para trabalhar com o log de atividades de saudação fazem parte da saudação [Insights REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx). eventos de log de atividade de tooretrieve, consulte [liste Olá eventos de gerenciamento em uma assinatura](https://msdn.microsoft.com/library/azure/dn931934.aspx).

## <a name="next-steps"></a>Próximas etapas
* Logs de atividade do Azure podem ser usados com ideias do Power BI toogain maiores sobre ações de saudação em sua assinatura. Confira [View and analyze Azure Activity Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/)(Exibir e analisar logs de atividade do Azure no Power BI e muito mais).
* toolearn sobre a configuração de políticas de segurança, consulte [controle de acesso baseado em função do Azure](../active-directory/role-based-access-control-configure.md).
* toolearn sobre comandos Olá para exibir as operações de implantação, consulte [Exibir operações de implantação](resource-manager-deployment-operations.md).
* toolearn como tooprevent exclusões em um recurso para todos os usuários, consulte [bloquear recursos do Azure Resource Manager](resource-group-lock-resources.md).

