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
# <a name="uninstall-elastic-database-jobs-components"></a><span data-ttu-id="d8474-103">Desinstalar componentes de trabalhos de banco de dados elástico</span><span class="sxs-lookup"><span data-stu-id="d8474-103">Uninstall Elastic Database jobs components</span></span>
<span data-ttu-id="d8474-104">**Trabalhos do banco de dados Elásticos** componentes podem ser desinstalados usando Olá Portal ou o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d8474-104">**Elastic Database jobs** components can be uninstalled using either hello Portal or PowerShell.</span></span>

## <a name="uninstall-elastic-database-jobs-components-using-hello-azure-portal"></a><span data-ttu-id="d8474-105">Desinstalar os componentes do banco de dados Elástico trabalhos usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d8474-105">Uninstall Elastic Database jobs components using hello Azure portal</span></span>
1. <span data-ttu-id="d8474-106">Olá abrir [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d8474-106">Open hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d8474-107">Navegue toohello assinatura que contém **trabalhos do banco de dados Elástico** componentes, ou seja, Olá assinatura na qual banco de dados Elástico componentes de trabalhos foram instaladas.</span><span class="sxs-lookup"><span data-stu-id="d8474-107">Navigate toohello subscription that contains **Elastic Database jobs** components, namely hello subscription in which Elastic Database jobs components were installed.</span></span>
3. <span data-ttu-id="d8474-108">Clique em **Procurar** e clique em **Grupos de recursos**.</span><span class="sxs-lookup"><span data-stu-id="d8474-108">Click **Browse** and click **Resource groups**.</span></span>
4. <span data-ttu-id="d8474-109">Grupo de recursos de saudação selecione chamado "__ElasticDatabaseJob".</span><span class="sxs-lookup"><span data-stu-id="d8474-109">Select hello resource group named "__ElasticDatabaseJob".</span></span>
5. <span data-ttu-id="d8474-110">Exclua grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="d8474-110">Delete hello resource group.</span></span>

## <a name="uninstall--elastic-database-jobs-components-using-powershell"></a><span data-ttu-id="d8474-111">Desinstalar componentes de trabalhos de banco de dados elástico usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="d8474-111">Uninstall  Elastic Database jobs components using PowerShell</span></span>
1. <span data-ttu-id="d8474-112">Inicie uma janela de comando do Microsoft Azure PowerShell e navegue toohello ferramentas subdiretório na pasta de Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x Olá: tipo **cd ferramentas**.</span><span class="sxs-lookup"><span data-stu-id="d8474-112">Launch a Microsoft Azure PowerShell command window and navigate toohello tools sub-directory under hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x folder: Type **cd tools**.</span></span>
   
     <span data-ttu-id="d8474-113">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools</span><span class="sxs-lookup"><span data-stu-id="d8474-113">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools</span></span>
2. <span data-ttu-id="d8474-114">Execute o script do PowerShell.\UninstallElasticDatabaseJobs.ps1 hello.</span><span class="sxs-lookup"><span data-stu-id="d8474-114">Execute hello .\UninstallElasticDatabaseJobs.ps1 PowerShell script.</span></span>
   
     <span data-ttu-id="d8474-115">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\UninstallElasticDatabaseJobs.ps1   PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\UninstallElasticDatabaseJobs.ps1</span><span class="sxs-lookup"><span data-stu-id="d8474-115">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\UninstallElasticDatabaseJobs.ps1   PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\UninstallElasticDatabaseJobs.ps1</span></span>

<span data-ttu-id="d8474-116">Ou simplesmente, execute Olá script a seguir, supondo que o padrão valores em usada na instalação de componentes de saudação:</span><span class="sxs-lookup"><span data-stu-id="d8474-116">Or simply, execute hello following script, assuming default values where used on installation of hello components:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="d8474-117">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d8474-117">Next steps</span></span>
<span data-ttu-id="d8474-118">trabalhos do banco de dados Elástico toore-instalar, consulte [instalar o serviço de trabalho de banco de dados Elástico Olá](sql-database-elastic-jobs-service-installation.md)</span><span class="sxs-lookup"><span data-stu-id="d8474-118">toore-install Elastic Database jobs, see [Installing hello Elastic Database job service](sql-database-elastic-jobs-service-installation.md)</span></span>

<span data-ttu-id="d8474-119">Para uma visão geral de trabalhos de banco de dados elástico, consulte [Visão geral de trabalhos de banco de dados elástico](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d8474-119">For an overview of Elastic Database jobs, see [Elastic Database jobs overview](sql-database-elastic-jobs-overview.md).</span></span>

<!--Image references-->


