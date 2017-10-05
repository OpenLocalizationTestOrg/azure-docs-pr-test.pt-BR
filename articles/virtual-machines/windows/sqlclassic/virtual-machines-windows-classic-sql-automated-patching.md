---
title: "Aplicação de patch automatizada para VMs do SQL Server (Clássico) | Microsoft Docs"
description: "Explica o recurso de Aplicação de Patch Automatizada para Máquinas Virtuais do SQL Server em execução no Azure e usando o modo de implantação clássico."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 737b2f65-08b9-4f54-b867-e987730265a8
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 1959871141f196ba80ffd7b37e62e5ea5b42dba3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-classic"></a><span data-ttu-id="a3669-103">Aplicação de patch automatizada para o SQL Server em Máquinas Virtuais do Azure (Clássico)</span><span class="sxs-lookup"><span data-stu-id="a3669-103">Automated Patching for SQL Server in Azure Virtual Machines (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a3669-104">Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="a3669-104">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-automated-patching.md)
> * [<span data-ttu-id="a3669-105">Clássico</span><span class="sxs-lookup"><span data-stu-id="a3669-105">Classic</span></span>](../classic/sql-automated-patching.md)
> 
> 

<span data-ttu-id="a3669-106">A aplicação de patch automatizada estabelece uma janela de manutenção para uma Máquina Virtual do Azure que executa o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a3669-106">Automated Patching establishes a maintenance window for an Azure Virtual Machine running SQL Server.</span></span> <span data-ttu-id="a3669-107">Atualizações automáticas só podem ser instaladas durante esta janela de manutenção.</span><span class="sxs-lookup"><span data-stu-id="a3669-107">Automated Updates can only be installed during this maintenance window.</span></span> <span data-ttu-id="a3669-108">Para o SQL Server, isso garante que as atualizações do sistema e qualquer reinicialização associada ocorrerão no melhor momento possível para o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="a3669-108">For SQL Server, this ensures that system updates and any associated restarts occur at the best possible time for the database.</span></span> <span data-ttu-id="a3669-109">A aplicação de patch automatizada depende da [Extensão do Agente IaaS do SQL Server](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="a3669-109">Automated Patching depends on the [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="a3669-110">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="a3669-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="a3669-111">Este artigo aborda o uso do modelo de implantação Clássica.</span><span class="sxs-lookup"><span data-stu-id="a3669-111">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="a3669-112">A Microsoft recomenda que a maioria das implantações novas use o modelo do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="a3669-112">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="a3669-113">Para exibir a versão do Resource Manager deste artigo, consulte [Aplicação de Patch Automatizada para o SQL Server em Máquinas Virtuais do Azure do Resource Manager](../sql/virtual-machines-windows-sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="a3669-113">To view the Resource Manager version of this article, see [Automated Patching for SQL Server in Azure Virtual Machines Resource Manager](../sql/virtual-machines-windows-sql-automated-patching.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a3669-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a3669-114">Prerequisites</span></span>
<span data-ttu-id="a3669-115">Para usar a Aplicação de Patch Automatizada, considere os seguintes pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="a3669-115">To use Automated Patching, consider the following prerequisites:</span></span>

<span data-ttu-id="a3669-116">**Sistema operacional**:</span><span class="sxs-lookup"><span data-stu-id="a3669-116">**Operating System**:</span></span>

* <span data-ttu-id="a3669-117">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="a3669-117">Windows Server 2012</span></span>
* <span data-ttu-id="a3669-118">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="a3669-118">Windows Server 2012 R2</span></span>
* <span data-ttu-id="a3669-119">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="a3669-119">Windows Server 2016</span></span>

<span data-ttu-id="a3669-120">**Versão do SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="a3669-120">**SQL Server version**:</span></span>

* <span data-ttu-id="a3669-121">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="a3669-121">SQL Server 2012</span></span>
* <span data-ttu-id="a3669-122">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="a3669-122">SQL Server 2014</span></span>
* <span data-ttu-id="a3669-123">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="a3669-123">SQL Server 2016</span></span>

<span data-ttu-id="a3669-124">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="a3669-124">**Azure PowerShell**:</span></span>

* <span data-ttu-id="a3669-125">[Instale os comandos mais recentes do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a3669-125">[Install the latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="a3669-126">**Extensão IaaS do SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="a3669-126">**SQL Server IaaS Extension**:</span></span>

* <span data-ttu-id="a3669-127">[Instale a Extensão IaaS do SQL Server](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="a3669-127">[Install the SQL Server IaaS Extension](../classic/sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="a3669-128">Configurações</span><span class="sxs-lookup"><span data-stu-id="a3669-128">Settings</span></span>
<span data-ttu-id="a3669-129">A tabela a seguir descreve as opções que podem ser configuradas para Aplicação de Patch Automatizada.</span><span class="sxs-lookup"><span data-stu-id="a3669-129">The following table describes the options that can be configured for Automated Patching.</span></span> <span data-ttu-id="a3669-130">Para VMs clássicas, você deve usar o PowerShell para definir essas configurações.</span><span class="sxs-lookup"><span data-stu-id="a3669-130">For classic VMs, you must use PowerShell to configure these settings.</span></span>

| <span data-ttu-id="a3669-131">Configuração</span><span class="sxs-lookup"><span data-stu-id="a3669-131">Setting</span></span> | <span data-ttu-id="a3669-132">Valores possíveis</span><span class="sxs-lookup"><span data-stu-id="a3669-132">Possible values</span></span> | <span data-ttu-id="a3669-133">Descrição</span><span class="sxs-lookup"><span data-stu-id="a3669-133">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a3669-134">**Aplicação de patch automatizada**</span><span class="sxs-lookup"><span data-stu-id="a3669-134">**Automated Patching**</span></span> |<span data-ttu-id="a3669-135">Habilitar/desabilitar (Desabilitado)</span><span class="sxs-lookup"><span data-stu-id="a3669-135">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="a3669-136">Habilita ou desabilita a Aplicação de Patch Automatizada para uma máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="a3669-136">Enables or disables Automated Patching for an Azure virtual machine.</span></span> |
| <span data-ttu-id="a3669-137">**Agenda de manutenção**</span><span class="sxs-lookup"><span data-stu-id="a3669-137">**Maintenance schedule**</span></span> |<span data-ttu-id="a3669-138">Todos os dias, segunda-feira, terça-feira, quarta-feira, quinta-feira, sexta-feira, sábado e domingo</span><span class="sxs-lookup"><span data-stu-id="a3669-138">Everyday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday</span></span> |<span data-ttu-id="a3669-139">A agenda para baixar e instalar atualizações do Windows, do SQL Server e do Microsoft para sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a3669-139">The schedule for downloading and installing Windows, SQL Server, and Microsoft updates for your virtual machine.</span></span> |
| <span data-ttu-id="a3669-140">**Hora de início da manutenção**</span><span class="sxs-lookup"><span data-stu-id="a3669-140">**Maintenance start hour**</span></span> |<span data-ttu-id="a3669-141">0h a 24h</span><span class="sxs-lookup"><span data-stu-id="a3669-141">0-24</span></span> |<span data-ttu-id="a3669-142">A hora de início local para atualizar a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a3669-142">The local start time to update the virtual machine.</span></span> |
| <span data-ttu-id="a3669-143">**Duração da janela de manutenção**</span><span class="sxs-lookup"><span data-stu-id="a3669-143">**Maintenance window duration**</span></span> |<span data-ttu-id="a3669-144">30-180</span><span class="sxs-lookup"><span data-stu-id="a3669-144">30-180</span></span> |<span data-ttu-id="a3669-145">O número de minutos permitidos para concluir o download e a instalação de atualizações.</span><span class="sxs-lookup"><span data-stu-id="a3669-145">The number of minutes permitted to complete the download and installation of updates.</span></span> |
| <span data-ttu-id="a3669-146">**Categoria de patch**</span><span class="sxs-lookup"><span data-stu-id="a3669-146">**Patch Category**</span></span> |<span data-ttu-id="a3669-147">Importante</span><span class="sxs-lookup"><span data-stu-id="a3669-147">Important</span></span> |<span data-ttu-id="a3669-148">A categoria de atualizações para baixar e instalar.</span><span class="sxs-lookup"><span data-stu-id="a3669-148">The category of updates to download and install.</span></span> |

## <a name="configuration-with-powershell"></a><span data-ttu-id="a3669-149">Configuração com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="a3669-149">Configuration with PowerShell</span></span>
<span data-ttu-id="a3669-150">No exemplo a seguir, o PowerShell é usado para configurar a Aplicação de Patch Automatizada em uma VM existente do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a3669-150">In the following example, PowerShell is used to configure Automated Patching on an existing SQL Server VM.</span></span> <span data-ttu-id="a3669-151">O comando **New-AzureVMSqlServerAutoPatchingConfig** configura uma nova janela de manutenção para atualizações automáticas.</span><span class="sxs-lookup"><span data-stu-id="a3669-151">The **New-AzureVMSqlServerAutoPatchingConfig** command configures a new maintenance window for automatic updates.</span></span>

    $aps = New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoPatchingSettings $aps | Update-AzureVM

<span data-ttu-id="a3669-152">Com base neste exemplo, a tabela a seguir descreve o efeito prático sobre a VM do Azure de destino:</span><span class="sxs-lookup"><span data-stu-id="a3669-152">Based on this example, the following table describes the practical effect on the target Azure VM:</span></span>

| <span data-ttu-id="a3669-153">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="a3669-153">Parameter</span></span> | <span data-ttu-id="a3669-154">Efeito</span><span class="sxs-lookup"><span data-stu-id="a3669-154">Effect</span></span> |
| --- | --- |
| <span data-ttu-id="a3669-155">**DayOfWeek**</span><span class="sxs-lookup"><span data-stu-id="a3669-155">**DayOfWeek**</span></span> |<span data-ttu-id="a3669-156">Patches instalados toda quinta-feira.</span><span class="sxs-lookup"><span data-stu-id="a3669-156">Patches installed every Thursday.</span></span> |
| <span data-ttu-id="a3669-157">**MaintenanceWindowStartingHour**</span><span class="sxs-lookup"><span data-stu-id="a3669-157">**MaintenanceWindowStartingHour**</span></span> |<span data-ttu-id="a3669-158">Inicia as atualizações às 11h.</span><span class="sxs-lookup"><span data-stu-id="a3669-158">Begin updates at 11:00am.</span></span> |
| <span data-ttu-id="a3669-159">**MaintenanceWindowsDuration**</span><span class="sxs-lookup"><span data-stu-id="a3669-159">**MaintenanceWindowsDuration**</span></span> |<span data-ttu-id="a3669-160">Os patches devem ser instalados dentro de 120 minutos.</span><span class="sxs-lookup"><span data-stu-id="a3669-160">Patches must be installed within 120 minutes.</span></span> <span data-ttu-id="a3669-161">Com base na hora de início, eles devem estar concluídos até 13h.</span><span class="sxs-lookup"><span data-stu-id="a3669-161">Based on the start time, they must complete by 1:00pm.</span></span> |
| <span data-ttu-id="a3669-162">**PatchCategory**</span><span class="sxs-lookup"><span data-stu-id="a3669-162">**PatchCategory**</span></span> |<span data-ttu-id="a3669-163">A única configuração possível para esse parâmetro é "Important".</span><span class="sxs-lookup"><span data-stu-id="a3669-163">The only possible setting for this parameter is “Important”.</span></span> |

<span data-ttu-id="a3669-164">Pode demorar vários minutos para instalar e configurar o Agente IaaS do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a3669-164">It could take several minutes to install and configure the SQL Server IaaS Agent.</span></span>

<span data-ttu-id="a3669-165">Para desabilitar a Aplicação de Patch Automatizada, execute o mesmo script sem o parâmetro -Enable para New-AzureVMSqlServerAutoPatchingConfig.</span><span class="sxs-lookup"><span data-stu-id="a3669-165">To disable Automated Patching, run the same script without the -Enable parameter to the New-AzureVMSqlServerAutoPatchingConfig.</span></span> <span data-ttu-id="a3669-166">Assim como acontece com a instalação, pode demorar vários minutos para desabilitar a Aplicação de Patch Automatizada.</span><span class="sxs-lookup"><span data-stu-id="a3669-166">As with installation, it can take several minutes to disable Automated Patching.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3669-167">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a3669-167">Next steps</span></span>
<span data-ttu-id="a3669-168">Para obter informações sobre outras tarefas de automação disponíveis, consulte [Extensão do agente IaaS do SQL Server](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="a3669-168">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

<span data-ttu-id="a3669-169">Para obter mais informações sobre como executar o SQL Server em VMs do Azure, consulte [Visão geral do SQL Server em Máquinas Virtuais do Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a3669-169">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

