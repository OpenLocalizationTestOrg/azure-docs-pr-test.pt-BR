---
title: "Veja como desinstalar a ferramenta de trabalho de banco de dados elástico"
description: "Como desinstalar a ferramenta de trabalho de banco de dados elástico"
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
ms.openlocfilehash: ae7f0bce452a0a86f6f1e4d9b0c93a0fa1727f21
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="uninstall-elastic-database-jobs-components"></a><span data-ttu-id="77faa-103">Desinstalar componentes de trabalhos de banco de dados elástico</span><span class="sxs-lookup"><span data-stu-id="77faa-103">Uninstall Elastic Database jobs components</span></span>
<span data-ttu-id="77faa-104">**trabalhos do banco de dados elástico** podem ser desinstalados usando o Portal ou o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="77faa-104">**Elastic Database jobs** components can be uninstalled using either the Portal or PowerShell.</span></span>

## <a name="uninstall-elastic-database-jobs-components-using-the-azure-portal"></a><span data-ttu-id="77faa-105">Desinstalar componentes de trabalhos de banco de dados elástico usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="77faa-105">Uninstall Elastic Database jobs components using the Azure portal</span></span>
1. <span data-ttu-id="77faa-106">Abra o [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="77faa-106">Open the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="77faa-107">Navegue até a assinatura que contém os componentes de **trabalhos do banco de dados elástico** , ou seja, a assinatura na qual os componentes do banco de dados elástico foram instalados.</span><span class="sxs-lookup"><span data-stu-id="77faa-107">Navigate to the subscription that contains **Elastic Database jobs** components, namely the subscription in which Elastic Database jobs components were installed.</span></span>
3. <span data-ttu-id="77faa-108">Clique em **Procurar** e clique em **Grupos de recursos**.</span><span class="sxs-lookup"><span data-stu-id="77faa-108">Click **Browse** and click **Resource groups**.</span></span>
4. <span data-ttu-id="77faa-109">Selecione o grupo de recursos chamado "__ElasticDatabaseJob".</span><span class="sxs-lookup"><span data-stu-id="77faa-109">Select the resource group named "__ElasticDatabaseJob".</span></span>
5. <span data-ttu-id="77faa-110">Exclua o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="77faa-110">Delete the resource group.</span></span>

## <a name="uninstall--elastic-database-jobs-components-using-powershell"></a><span data-ttu-id="77faa-111">Desinstalar componentes de trabalhos de banco de dados elástico usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="77faa-111">Uninstall  Elastic Database jobs components using PowerShell</span></span>
1. <span data-ttu-id="77faa-112">Inicie uma janela de comando do Microsoft Azure PowerShell e navegue até o subdiretório ferramentas na pasta Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x: digite **cd tools**.</span><span class="sxs-lookup"><span data-stu-id="77faa-112">Launch a Microsoft Azure PowerShell command window and navigate to the tools sub-directory under the Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x folder: Type **cd tools**.</span></span>
   
     <span data-ttu-id="77faa-113">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools</span><span class="sxs-lookup"><span data-stu-id="77faa-113">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools</span></span>
2. <span data-ttu-id="77faa-114">Execute o script do PowerShell .\UninstallElasticDatabaseJobs.ps1.</span><span class="sxs-lookup"><span data-stu-id="77faa-114">Execute the .\UninstallElasticDatabaseJobs.ps1 PowerShell script.</span></span>
   
     <span data-ttu-id="77faa-115">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\UninstallElasticDatabaseJobs.ps1   PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\UninstallElasticDatabaseJobs.ps1</span><span class="sxs-lookup"><span data-stu-id="77faa-115">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\UninstallElasticDatabaseJobs.ps1   PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\UninstallElasticDatabaseJobs.ps1</span></span>

<span data-ttu-id="77faa-116">Ou simplesmente execute o script a seguir, presumindo valores padrão em que os valores são usados na instalação dos componentes:</span><span class="sxs-lookup"><span data-stu-id="77faa-116">Or simply, execute the following script, assuming default values where used on installation of the components:</span></span>

        $ResourceGroupName = "__ElasticDatabaseJob"
        Switch-AzureMode AzureResourceManager

        $resourceGroup = Get-AzureResourceGroup -Name $ResourceGroupName
        if(!$resourceGroup)
        {
            Write-Host "The Azure Resource Group: $ResourceGroupName has already been deleted.  Elastic database job components are uninstalled."
            return
        }

        Write-Host "Removing the Azure Resource Group: $ResourceGroupName.  This may take a few minutes.”
        Remove-AzureResourceGroup -Name $ResourceGroupName -Force
        Write-Host "Completed removing the Azure Resource Group: $ResourceGroupName.  Elastic database job compoennts are now uninstalled."

## <a name="next-steps"></a><span data-ttu-id="77faa-117">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="77faa-117">Next steps</span></span>
<span data-ttu-id="77faa-118">Para reinstalar trabalhos de banco de dados elástico, confira [Instalando o serviço de trabalho de banco de dados elástico](sql-database-elastic-jobs-service-installation.md)</span><span class="sxs-lookup"><span data-stu-id="77faa-118">To re-install Elastic Database jobs, see [Installing the Elastic Database job service](sql-database-elastic-jobs-service-installation.md)</span></span>

<span data-ttu-id="77faa-119">Para uma visão geral de trabalhos de banco de dados elástico, consulte [Visão geral de trabalhos de banco de dados elástico](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="77faa-119">For an overview of Elastic Database jobs, see [Elastic Database jobs overview](sql-database-elastic-jobs-overview.md).</span></span>

<!--Image references-->


