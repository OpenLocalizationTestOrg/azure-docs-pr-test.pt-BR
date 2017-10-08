---
title: aaaManage Azure Analysis Services com o PowerShell | Microsoft Docs
description: O gerenciamento do Azure Analysis Services com o PowerShell.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: owend
ms.openlocfilehash: bc4250bf77b5a0d86c1049ee57493bcf2a1f0c1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-analysis-services-with-powershell"></a>Gerenciar o Azure Analysis Services com PowerShell

Este artigo descreve PowerShell cmdlets usados tooperform Azure Analysis Services server e banco de dados de tarefas de gerenciamento. 

Tarefas de gerenciamento de servidor, como criação ou exclusão de um servidor, suspender ou retomar as operações do servidor ou alterando o nível de serviço da saudação (camada) usam cmdlets do Gerenciador de recursos do Azure (AzureRM). Outras tarefas de gerenciamento de bancos de dados, como adicionar ou remover membros da função, processamento ou particionamento use cmdlets incluídos no hello mesmo módulo SqlServer, como SQL Server Analysis Services.

## <a name="permissions"></a>Permissões
A maioria das tarefas do PowerShell exigem que você tem privilégios de administrador no servidor do Analysis Services Olá que você está gerenciando. As tarefas agendadas do PowerShell são operações autônomas. conta de saudação executando Agendador Olá deve ter privilégios de administrador no servidor do Analysis Services hello. 

Para operações de servidor usando os cmdlets AzureRm, a conta ou Olá executando Agendador também deve pertencer toohello a função de proprietário para o recurso de saudação em [o Access RBAC (controle)](../active-directory/role-based-access-control-what-is.md). 

## <a name="server-operations"></a>Operações do servidor 
Cmdlets do Azure do Analysis Services são incluídos no hello [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices) módulo de componente. módulos do cmdlet AzureRM tooinstall, consulte [cmdlets do Azure Resource Manager](/powershell/azure/overview) em Olá Galeria do PowerShell.

|Cmdlet|Descrição| 
|------------|-----------------| 
|[Export-AzureAnalysisServicesInstance](/powershell/module/azurerm.analysisservices/export-azureanalysisservicesinstancelog)|Exportações de log toofile.| 
|[Get-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/get-azurermanalysisservicesserver)|Obtém detalhes de uma instância do servidor.|  
|[New-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver)|Cria uma instância de servidor.|
|[Remove-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/remove-azurermanalysisservicesserver)|Remove uma instância do servidor.|  
|[Suspend-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/suspend-azurermanalysisservicesserver)|Suspende uma instância do servidor.| 
|[Resume-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/resume-azurermanalysisservicesserver)|Retoma uma instância do servidor.|  
|[Set-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/set-azurermanalysisservicesserver)|Modifica uma instância do servidor.|   
|[Test-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/test-azurermanalysisservicesserver)|Testes Olá a existência de uma instância de servidor.| 

## <a name="database-operations"></a>Operações de banco de dados

Azure Analysis Services, as operações de banco de dados usam Olá mesmo [SqlServer](https://www.powershellgallery.com/packages/SqlServer) módulo como SQL Server Analysis Services. No entanto, nem todos os cmdlets têm suporte para o Azure Analysis Services. 

módulo do SqlServer Olá fornece cmdlets de gerenciamento de banco de dados de tarefas específicas, bem como o cmdlet Invoke-ASCmd de finalidade geral de Olá que aceita um modelo de script TMSL (linguagem tabela) de consulta ou script. Olá seguintes cmdlets no módulo do SqlServer Olá têm suporte para serviços de análise do Azure.

  
|Cmdlet|Descrição|
|------------|-----------------| 
|[Add-RoleMember](https://msdn.microsoft.com/library/hh510167.aspx)|Adicione um membro da função de banco de dados tooa.| 
|[Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet)|Fazer backup de um banco de dados do Analysis Services.|  
|[Remove-RoleMember](https://msdn.microsoft.com/library/hh510173.aspx)|Remover um membro de uma função de banco de dados.|   
|[Invoke-ASCmd](https://msdn.microsoft.com/library/hh479579.aspx)|Executar um script TMSL.|
|[Invoke-ProcessASDatabase](https://msdn.microsoft.com/library/mt651773.aspx)|Processar um banco de dados.|  
|[Invoke-ProcessPartition](https://msdn.microsoft.com/library/hh510164.aspx)|Processar uma partição.| 
|[Invoke-ProcessTable](https://msdn.microsoft.com/library/mt651774.aspx)|Processar uma tabela.|  
|[Merge-Partition](https://msdn.microsoft.com/library/hh479576.aspx)|Mesclar uma partição.|  
|[Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet)|Restaurar um banco de dados do Analysis Services.| 
  

## <a name="related-information"></a>Informações relacionadas

* [Baixar o módulo do PowerShell do SQL Server](https://docs.microsoft.com/sql/ssms/download-sql-server-ps-module)   
* [Baixar o SSMS](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)   
* [Módulo SqlServer na Galeria do PowerShell](https://www.powershellgallery.com/packages/SqlServer)    
* [Tabular Model Programming for Compatibility Level 1200 and higher](https://msdn.microsoft.com/library/mt712541.aspx) (Programação de Modelo Tabular para o Nível de Compatibilidade 1200 e superior)
