---
title: "aaaAutomated aplicação de patches para VMs do SQL Server (clássico) | Microsoft Docs"
description: "Explica o recurso de aplicação de patch automatizada hello para SQL Server máquinas virtuais em execução no Azure usando o modo de implantação clássico hello."
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
ms.openlocfilehash: 2ef06b95705fc457605d6eb2fbc0afd490321843
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-classic"></a><span data-ttu-id="a4104-103">Aplicação de patch automatizada para o SQL Server em Máquinas Virtuais do Azure (Clássico)</span><span class="sxs-lookup"><span data-stu-id="a4104-103">Automated Patching for SQL Server in Azure Virtual Machines (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a4104-104">Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="a4104-104">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-automated-patching.md)
> * [<span data-ttu-id="a4104-105">Clássico</span><span class="sxs-lookup"><span data-stu-id="a4104-105">Classic</span></span>](../classic/sql-automated-patching.md)
> 
> 

<span data-ttu-id="a4104-106">A aplicação de patch automatizada estabelece uma janela de manutenção para uma Máquina Virtual do Azure que executa o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a4104-106">Automated Patching establishes a maintenance window for an Azure Virtual Machine running SQL Server.</span></span> <span data-ttu-id="a4104-107">Atualizações automáticas só podem ser instaladas durante esta janela de manutenção.</span><span class="sxs-lookup"><span data-stu-id="a4104-107">Automated Updates can only be installed during this maintenance window.</span></span> <span data-ttu-id="a4104-108">Para o SQL Server, isso garante que as atualizações do sistema e qualquer reinicialização associada ocorre no melhor tempo possível Olá para o banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="a4104-108">For SQL Server, this ensures that system updates and any associated restarts occur at hello best possible time for hello database.</span></span> <span data-ttu-id="a4104-109">Aplicação de patch automatizada depende Olá [extensão do SQL Server IaaS Agent](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="a4104-109">Automated Patching depends on hello [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="a4104-110">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="a4104-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="a4104-111">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="a4104-111">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="a4104-112">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="a4104-112">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="a4104-113">versão do Gerenciador de recursos de saudação tooview deste artigo, consulte [aplicação de patch automatizada para o SQL Server no Gerenciador de recursos de máquinas virtuais do Azure](../sql/virtual-machines-windows-sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="a4104-113">tooview hello Resource Manager version of this article, see [Automated Patching for SQL Server in Azure Virtual Machines Resource Manager](../sql/virtual-machines-windows-sql-automated-patching.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a4104-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a4104-114">Prerequisites</span></span>
<span data-ttu-id="a4104-115">toouse aplicação de patch automatizada, considere Olá pré-requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="a4104-115">toouse Automated Patching, consider hello following prerequisites:</span></span>

<span data-ttu-id="a4104-116">**Sistema operacional**:</span><span class="sxs-lookup"><span data-stu-id="a4104-116">**Operating System**:</span></span>

* <span data-ttu-id="a4104-117">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="a4104-117">Windows Server 2012</span></span>
* <span data-ttu-id="a4104-118">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="a4104-118">Windows Server 2012 R2</span></span>
* <span data-ttu-id="a4104-119">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="a4104-119">Windows Server 2016</span></span>

<span data-ttu-id="a4104-120">**Versão do SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="a4104-120">**SQL Server version**:</span></span>

* <span data-ttu-id="a4104-121">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="a4104-121">SQL Server 2012</span></span>
* <span data-ttu-id="a4104-122">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="a4104-122">SQL Server 2014</span></span>
* <span data-ttu-id="a4104-123">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="a4104-123">SQL Server 2016</span></span>

<span data-ttu-id="a4104-124">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="a4104-124">**Azure PowerShell**:</span></span>

* <span data-ttu-id="a4104-125">[Olá mais recente do Azure PowerShell comandos de instalação](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a4104-125">[Install hello latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="a4104-126">**Extensão IaaS do SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="a4104-126">**SQL Server IaaS Extension**:</span></span>

* <span data-ttu-id="a4104-127">[Instalar Olá extensão do SQL Server IaaS](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="a4104-127">[Install hello SQL Server IaaS Extension](../classic/sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="a4104-128">Configurações</span><span class="sxs-lookup"><span data-stu-id="a4104-128">Settings</span></span>
<span data-ttu-id="a4104-129">Olá, tabela a seguir descreve as opções de saudação que podem ser configuradas para aplicação de patch automatizada.</span><span class="sxs-lookup"><span data-stu-id="a4104-129">hello following table describes hello options that can be configured for Automated Patching.</span></span> <span data-ttu-id="a4104-130">Para VMs clássicas, você deve usar PowerShell tooconfigure essas configurações.</span><span class="sxs-lookup"><span data-stu-id="a4104-130">For classic VMs, you must use PowerShell tooconfigure these settings.</span></span>

| <span data-ttu-id="a4104-131">Configuração</span><span class="sxs-lookup"><span data-stu-id="a4104-131">Setting</span></span> | <span data-ttu-id="a4104-132">Valores possíveis</span><span class="sxs-lookup"><span data-stu-id="a4104-132">Possible values</span></span> | <span data-ttu-id="a4104-133">Descrição</span><span class="sxs-lookup"><span data-stu-id="a4104-133">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a4104-134">**Aplicação de patch automatizada**</span><span class="sxs-lookup"><span data-stu-id="a4104-134">**Automated Patching**</span></span> |<span data-ttu-id="a4104-135">Habilitar/desabilitar (Desabilitado)</span><span class="sxs-lookup"><span data-stu-id="a4104-135">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="a4104-136">Habilita ou desabilita a Aplicação de Patch Automatizada para uma máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="a4104-136">Enables or disables Automated Patching for an Azure virtual machine.</span></span> |
| <span data-ttu-id="a4104-137">**Agenda de manutenção**</span><span class="sxs-lookup"><span data-stu-id="a4104-137">**Maintenance schedule**</span></span> |<span data-ttu-id="a4104-138">Todos os dias, segunda-feira, terça-feira, quarta-feira, quinta-feira, sexta-feira, sábado e domingo</span><span class="sxs-lookup"><span data-stu-id="a4104-138">Everyday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday</span></span> |<span data-ttu-id="a4104-139">agenda de saudação para baixar e instalar atualizações do Windows, SQL Server e Microsoft para sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a4104-139">hello schedule for downloading and installing Windows, SQL Server, and Microsoft updates for your virtual machine.</span></span> |
| <span data-ttu-id="a4104-140">**Hora de início da manutenção**</span><span class="sxs-lookup"><span data-stu-id="a4104-140">**Maintenance start hour**</span></span> |<span data-ttu-id="a4104-141">0h a 24h</span><span class="sxs-lookup"><span data-stu-id="a4104-141">0-24</span></span> |<span data-ttu-id="a4104-142">Olá início local tempo tooupdate Olá VM.</span><span class="sxs-lookup"><span data-stu-id="a4104-142">hello local start time tooupdate hello virtual machine.</span></span> |
| <span data-ttu-id="a4104-143">**Duração da janela de manutenção**</span><span class="sxs-lookup"><span data-stu-id="a4104-143">**Maintenance window duration**</span></span> |<span data-ttu-id="a4104-144">30-180</span><span class="sxs-lookup"><span data-stu-id="a4104-144">30-180</span></span> |<span data-ttu-id="a4104-145">número de saudação de minutos permitidos download de saudação toocomplete e instalação de atualizações.</span><span class="sxs-lookup"><span data-stu-id="a4104-145">hello number of minutes permitted toocomplete hello download and installation of updates.</span></span> |
| <span data-ttu-id="a4104-146">**Categoria de patch**</span><span class="sxs-lookup"><span data-stu-id="a4104-146">**Patch Category**</span></span> |<span data-ttu-id="a4104-147">Importante</span><span class="sxs-lookup"><span data-stu-id="a4104-147">Important</span></span> |<span data-ttu-id="a4104-148">categoria de saudação do toodownload atualizações e instalar.</span><span class="sxs-lookup"><span data-stu-id="a4104-148">hello category of updates toodownload and install.</span></span> |

## <a name="configuration-with-powershell"></a><span data-ttu-id="a4104-149">Configuração com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4104-149">Configuration with PowerShell</span></span>
<span data-ttu-id="a4104-150">Olá exemplo a seguir, PowerShell é usado tooconfigure aplicação de patch automatizada em uma VM existente do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a4104-150">In hello following example, PowerShell is used tooconfigure Automated Patching on an existing SQL Server VM.</span></span> <span data-ttu-id="a4104-151">Olá **New-AzureVMSqlServerAutoPatchingConfig** comando configura uma nova janela de manutenção para atualizações automáticas.</span><span class="sxs-lookup"><span data-stu-id="a4104-151">hello **New-AzureVMSqlServerAutoPatchingConfig** command configures a new maintenance window for automatic updates.</span></span>

    $aps = New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoPatchingSettings $aps | Update-AzureVM

<span data-ttu-id="a4104-152">Com base neste exemplo, hello tabela a seguir descreve a efeito prático Olá no destino Olá VM do Azure:</span><span class="sxs-lookup"><span data-stu-id="a4104-152">Based on this example, hello following table describes hello practical effect on hello target Azure VM:</span></span>

| <span data-ttu-id="a4104-153">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="a4104-153">Parameter</span></span> | <span data-ttu-id="a4104-154">Efeito</span><span class="sxs-lookup"><span data-stu-id="a4104-154">Effect</span></span> |
| --- | --- |
| <span data-ttu-id="a4104-155">**DayOfWeek**</span><span class="sxs-lookup"><span data-stu-id="a4104-155">**DayOfWeek**</span></span> |<span data-ttu-id="a4104-156">Patches instalados toda quinta-feira.</span><span class="sxs-lookup"><span data-stu-id="a4104-156">Patches installed every Thursday.</span></span> |
| <span data-ttu-id="a4104-157">**MaintenanceWindowStartingHour**</span><span class="sxs-lookup"><span data-stu-id="a4104-157">**MaintenanceWindowStartingHour**</span></span> |<span data-ttu-id="a4104-158">Inicia as atualizações às 11h.</span><span class="sxs-lookup"><span data-stu-id="a4104-158">Begin updates at 11:00am.</span></span> |
| <span data-ttu-id="a4104-159">**MaintenanceWindowsDuration**</span><span class="sxs-lookup"><span data-stu-id="a4104-159">**MaintenanceWindowsDuration**</span></span> |<span data-ttu-id="a4104-160">Os patches devem ser instalados dentro de 120 minutos.</span><span class="sxs-lookup"><span data-stu-id="a4104-160">Patches must be installed within 120 minutes.</span></span> <span data-ttu-id="a4104-161">Com base na hora de início do hello, elas devem concluir até 1:00 pm.</span><span class="sxs-lookup"><span data-stu-id="a4104-161">Based on hello start time, they must complete by 1:00pm.</span></span> |
| <span data-ttu-id="a4104-162">**PatchCategory**</span><span class="sxs-lookup"><span data-stu-id="a4104-162">**PatchCategory**</span></span> |<span data-ttu-id="a4104-163">Olá, somente a configuração possíveis para esse parâmetro é "Importante".</span><span class="sxs-lookup"><span data-stu-id="a4104-163">hello only possible setting for this parameter is “Important”.</span></span> |

<span data-ttu-id="a4104-164">Ele pode levar vários tooinstall de minutos e configure Olá SQL Server IaaS Agent.</span><span class="sxs-lookup"><span data-stu-id="a4104-164">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span>

<span data-ttu-id="a4104-165">toodisable aplicação de patch automatizada, Olá execução mesmo script sem Olá - Enable parâmetro toohello New-AzureVMSqlServerAutoPatchingConfig.</span><span class="sxs-lookup"><span data-stu-id="a4104-165">toodisable Automated Patching, run hello same script without hello -Enable parameter toohello New-AzureVMSqlServerAutoPatchingConfig.</span></span> <span data-ttu-id="a4104-166">Como com a instalação, pode levar várias toodisable de minutos aplicação de patch automatizada.</span><span class="sxs-lookup"><span data-stu-id="a4104-166">As with installation, it can take several minutes toodisable Automated Patching.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4104-167">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a4104-167">Next steps</span></span>
<span data-ttu-id="a4104-168">Para obter informações sobre outras tarefas de automação disponíveis, consulte [Extensão do agente IaaS do SQL Server](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="a4104-168">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

<span data-ttu-id="a4104-169">Para obter mais informações sobre como executar o SQL Server em VMs do Azure, consulte [Visão geral do SQL Server em Máquinas Virtuais do Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a4104-169">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

