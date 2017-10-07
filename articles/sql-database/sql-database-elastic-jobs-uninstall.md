---
title: "ferramenta de trabalhos de banco de dados Elástico aaaHow toouninstall"
description: "Como toouninstall Olá ferramenta de trabalhos do banco de dados Elástico"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: bfc9d820-edbd-4fca-bfbf-1f339cfcc448
ms.service: sql-database
ms.workload: sql-database
ms.custom: scale out apps
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 3bc1e889d5042bc3eaa9fd9da89816737e0b8df8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="uninstall-elastic-database-jobs-components"></a>Desinstalar componentes de trabalhos de banco de dados elástico
**Trabalhos do banco de dados Elásticos** componentes podem ser desinstalados usando Olá Portal ou o PowerShell.

## <a name="uninstall-elastic-database-jobs-components-using-hello-azure-portal"></a>Desinstalar os componentes do banco de dados Elástico trabalhos usando Olá portal do Azure
1. Olá abrir [portal do Azure](https://portal.azure.com/).
2. Navegue toohello assinatura que contém **trabalhos do banco de dados Elástico** componentes, ou seja, Olá assinatura na qual banco de dados Elástico componentes de trabalhos foram instaladas.
3. Clique em **Procurar** e clique em **Grupos de recursos**.
4. Grupo de recursos de saudação selecione chamado "__ElasticDatabaseJob".
5. Exclua grupo de recursos de saudação.

## <a name="uninstall--elastic-database-jobs-components-using-powershell"></a>Desinstalar componentes de trabalhos de banco de dados elástico usando o PowerShell
1. Inicie uma janela de comando do Microsoft Azure PowerShell e navegue toohello ferramentas subdiretório na pasta de Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x Olá: tipo **cd ferramentas**.
   
     PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools
2. Execute o script do PowerShell.\UninstallElasticDatabaseJobs.ps1 hello.
   
     PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\UninstallElasticDatabaseJobs.ps1   PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\UninstallElasticDatabaseJobs.ps1

Ou simplesmente, execute Olá script a seguir, supondo que o padrão valores em usada na instalação de componentes de saudação:

        $ResourceGroupName = "__ElasticDatabaseJob"
        Switch-AzureMode AzureResourceManager

        $resourceGroup = Get-AzureResourceGroup -Name $ResourceGroupName
        if(!$resourceGroup)
        {
            Write-Host "hello Azure Resource Group: $ResourceGroupName has already been deleted.  Elastic database job components are uninstalled."
            return
        }

        Write-Host "Removing hello Azure Resource Group: $ResourceGroupName.  This may take a few minutes.”
        Remove-AzureResourceGroup -Name $ResourceGroupName -Force
        Write-Host "Completed removing hello Azure Resource Group: $ResourceGroupName.  Elastic database job compoennts are now uninstalled."

## <a name="next-steps"></a>Próximas etapas
trabalhos do banco de dados Elástico toore-instalar, consulte [instalar o serviço de trabalho de banco de dados Elástico Olá](sql-database-elastic-jobs-service-installation.md)

Para uma visão geral de trabalhos de banco de dados elástico, consulte [Visão geral de trabalhos de banco de dados elástico](sql-database-elastic-jobs-overview.md).

<!--Image references-->


