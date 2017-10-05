---
title: "Aplicação de Patch automatizada VMs do SQL Server (Resource Manager) | Microsoft Docs"
description: "Explica o recurso de Aplicação de Patch Automatizada para Máquinas Virtuais do SQL Server em execução no Azure usando o Gerenciador de Recursos."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 58232e92-318f-456b-8f0a-2201a541e08d
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 7d501ab45a85010a8dbfd6135d77f18f1743354e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-resource-manager"></a><span data-ttu-id="a554a-103">Aplicação de patch automatizada para o SQL Server em Máquinas Virtuais do Azure (Gerenciador de Recursos)</span><span class="sxs-lookup"><span data-stu-id="a554a-103">Automated Patching for SQL Server in Azure Virtual Machines (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a554a-104">Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="a554a-104">Resource Manager</span></span>](virtual-machines-windows-sql-automated-patching.md)
> * [<span data-ttu-id="a554a-105">Clássico</span><span class="sxs-lookup"><span data-stu-id="a554a-105">Classic</span></span>](../classic/sql-automated-patching.md)
> 
> 

<span data-ttu-id="a554a-106">A aplicação de patch automatizada estabelece uma janela de manutenção para uma Máquina Virtual do Azure que executa o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a554a-106">Automated Patching establishes a maintenance window for an Azure Virtual Machine running SQL Server.</span></span> <span data-ttu-id="a554a-107">Atualizações automáticas só podem ser instaladas durante esta janela de manutenção.</span><span class="sxs-lookup"><span data-stu-id="a554a-107">Automated Updates can only be installed during this maintenance window.</span></span> <span data-ttu-id="a554a-108">Para o SQL Server, essa restrição garante que as atualizações do sistema e qualquer reinicialização associada ocorram no melhor momento possível para o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="a554a-108">For SQL Server, this rescriction ensures that system updates and any associated restarts occur at the best possible time for the database.</span></span> <span data-ttu-id="a554a-109">A aplicação de patch automatizada depende da [Extensão do Agente IaaS do SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="a554a-109">Automated Patching depends on the [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="a554a-110">Para exibir a versão clássica deste artigo, consulte [Aplicação de Patch Automatizada para o SQL Server em Máquinas Virtuais do Azure Clássico](../classic/sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="a554a-110">To view the classic version of this article, see [Automated Patching for SQL Server in Azure Virtual Machines Classic](../classic/sql-automated-patching.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a554a-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a554a-111">Prerequisites</span></span>
<span data-ttu-id="a554a-112">Para usar a Aplicação de Patch Automatizada, considere os seguintes pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="a554a-112">To use Automated Patching, consider the following prerequisites:</span></span>

<span data-ttu-id="a554a-113">**Sistema operacional**:</span><span class="sxs-lookup"><span data-stu-id="a554a-113">**Operating System**:</span></span>

* <span data-ttu-id="a554a-114">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="a554a-114">Windows Server 2012</span></span>
* <span data-ttu-id="a554a-115">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="a554a-115">Windows Server 2012 R2</span></span>
* <span data-ttu-id="a554a-116">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="a554a-116">Windows Server 2016</span></span>

<span data-ttu-id="a554a-117">**Versão do SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="a554a-117">**SQL Server version**:</span></span>

* <span data-ttu-id="a554a-118">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="a554a-118">SQL Server 2012</span></span>
* <span data-ttu-id="a554a-119">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="a554a-119">SQL Server 2014</span></span>
* <span data-ttu-id="a554a-120">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="a554a-120">SQL Server 2016</span></span>

<span data-ttu-id="a554a-121">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="a554a-121">**Azure PowerShell**:</span></span>

* <span data-ttu-id="a554a-122">[Instalar os comandos mais recentes do Azure PowerShell](/powershell/azure/overview) se você planeja configurar a Aplicação de Patch Automatizada com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a554a-122">[Install the latest Azure PowerShell commands](/powershell/azure/overview) if you plan to configure Automated Patching with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="a554a-123">A aplicação de Patch automatizada depende da Extensão do Agente IaaS do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a554a-123">Automated Patching relies on the SQL Server IaaS Agent Extension.</span></span> <span data-ttu-id="a554a-124">As imagens atuais da galeria da máquina virtual do SQL adicionam essa extensão por padrão.</span><span class="sxs-lookup"><span data-stu-id="a554a-124">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="a554a-125">Para obter mais informações, consulte [Extensão do agente IaaS do SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="a554a-125">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>
> 
> 

## <a name="settings"></a><span data-ttu-id="a554a-126">Configurações</span><span class="sxs-lookup"><span data-stu-id="a554a-126">Settings</span></span>
<span data-ttu-id="a554a-127">A tabela a seguir descreve as opções que podem ser configuradas para Aplicação de Patch Automatizada.</span><span class="sxs-lookup"><span data-stu-id="a554a-127">The following table describes the options that can be configured for Automated Patching.</span></span> <span data-ttu-id="a554a-128">As etapas de configuração reais variam dependendo de se você usar os comandos do Portal do Azure ou do Azure Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a554a-128">The actual configuration steps vary depending on whether you use the Azure portal or Azure Windows PowerShell commands.</span></span>

| <span data-ttu-id="a554a-129">Configuração</span><span class="sxs-lookup"><span data-stu-id="a554a-129">Setting</span></span> | <span data-ttu-id="a554a-130">Valores possíveis</span><span class="sxs-lookup"><span data-stu-id="a554a-130">Possible values</span></span> | <span data-ttu-id="a554a-131">Descrição</span><span class="sxs-lookup"><span data-stu-id="a554a-131">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a554a-132">**Aplicação de patch automatizada**</span><span class="sxs-lookup"><span data-stu-id="a554a-132">**Automated Patching**</span></span> |<span data-ttu-id="a554a-133">Habilitar/desabilitar (Desabilitado)</span><span class="sxs-lookup"><span data-stu-id="a554a-133">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="a554a-134">Habilita ou desabilita a Aplicação de Patch Automatizada para uma máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="a554a-134">Enables or disables Automated Patching for an Azure virtual machine.</span></span> |
| <span data-ttu-id="a554a-135">**Agenda de manutenção**</span><span class="sxs-lookup"><span data-stu-id="a554a-135">**Maintenance schedule**</span></span> |<span data-ttu-id="a554a-136">Todos os dias, segunda-feira, terça-feira, quarta-feira, quinta-feira, sexta-feira, sábado e domingo</span><span class="sxs-lookup"><span data-stu-id="a554a-136">Everyday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday</span></span> |<span data-ttu-id="a554a-137">A agenda para baixar e instalar atualizações do Windows, do SQL Server e do Microsoft para sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a554a-137">The schedule for downloading and installing Windows, SQL Server, and Microsoft updates for your virtual machine.</span></span> |
| <span data-ttu-id="a554a-138">**Hora de início da manutenção**</span><span class="sxs-lookup"><span data-stu-id="a554a-138">**Maintenance start hour**</span></span> |<span data-ttu-id="a554a-139">0h a 24h</span><span class="sxs-lookup"><span data-stu-id="a554a-139">0-24</span></span> |<span data-ttu-id="a554a-140">A hora de início local para atualizar a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a554a-140">The local start time to update the virtual machine.</span></span> |
| <span data-ttu-id="a554a-141">**Duração da janela de manutenção**</span><span class="sxs-lookup"><span data-stu-id="a554a-141">**Maintenance window duration**</span></span> |<span data-ttu-id="a554a-142">30-180</span><span class="sxs-lookup"><span data-stu-id="a554a-142">30-180</span></span> |<span data-ttu-id="a554a-143">O número de minutos permitidos para concluir o download e a instalação de atualizações.</span><span class="sxs-lookup"><span data-stu-id="a554a-143">The number of minutes permitted to complete the download and installation of updates.</span></span> |
| <span data-ttu-id="a554a-144">**Categoria de patch**</span><span class="sxs-lookup"><span data-stu-id="a554a-144">**Patch Category**</span></span> |<span data-ttu-id="a554a-145">Importante</span><span class="sxs-lookup"><span data-stu-id="a554a-145">Important</span></span> |<span data-ttu-id="a554a-146">A categoria de atualizações para baixar e instalar.</span><span class="sxs-lookup"><span data-stu-id="a554a-146">The category of updates to download and install.</span></span> |

## <a name="configuration-in-the-portal"></a><span data-ttu-id="a554a-147">Configuração no Portal</span><span class="sxs-lookup"><span data-stu-id="a554a-147">Configuration in the Portal</span></span>
<span data-ttu-id="a554a-148">Você pode usar o portal do Azure para configurar a aplicação de Patch automatizada durante o provisionamento ou para VMs existentes.</span><span class="sxs-lookup"><span data-stu-id="a554a-148">You can use the Azure portal to configure Automated Patching during provisioning or for existing VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="a554a-149">Novas VMs</span><span class="sxs-lookup"><span data-stu-id="a554a-149">New VMs</span></span>
<span data-ttu-id="a554a-150">Use o portal do Azure para configurar a aplicação de Patch automatizada quando criar uma nova máquina virtual do SQL Server no modelo de implantação do gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="a554a-150">Use the Azure portal to configure Automated Patching when you create a new SQL Server Virtual Machine in the Resource Manager deployment model.</span></span>

<span data-ttu-id="a554a-151">Na folha **Configurações do SQL Server**, selecione **Aplicação de patch automatizada**.</span><span class="sxs-lookup"><span data-stu-id="a554a-151">In the **SQL Server settings** blade, select **Automated patching**.</span></span> <span data-ttu-id="a554a-152">As capturas de tela do portal do Azure a seguir mostram a folha **Aplicação de Patch Automatizada** .</span><span class="sxs-lookup"><span data-stu-id="a554a-152">The following Azure portal screenshot shows the **SQL Automated Patching** blade.</span></span>

![Aplicação de Patch Automática do SQL no Portal do Azure](./media/virtual-machines-windows-sql-automated-patching/azure-sql-arm-patching.png)

<span data-ttu-id="a554a-154">Para ter contexto, consulte o tópico completo sobre [provisionamento de uma máquina virtual do SQL Server no Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="a554a-154">For context, see the complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="a554a-155">VMs existentes</span><span class="sxs-lookup"><span data-stu-id="a554a-155">Existing VMs</span></span>
<span data-ttu-id="a554a-156">Para máquinas virtuais existentes do SQL Server, selecione sua máquina virtual do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a554a-156">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="a554a-157">Selecione a seção **Configuração do SQL Server** da folha **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="a554a-157">Then select the **SQL Server configuration** section of the **Settings** blade.</span></span>

![Aplicação de Patch Automática do SQL para VMs existentes](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-existing-vms.png)

<span data-ttu-id="a554a-159">Na folha **Configuração do SQL Server**, clique no botão **Editar** na seção de Aplicação de Patch Automatizada.</span><span class="sxs-lookup"><span data-stu-id="a554a-159">In the **SQL Server configuration** blade, click the **Edit** button in the Automated patching section.</span></span>

![Configurar a Aplicação de Patch Automática do SQL para VMs existentes](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-configuration.png)

<span data-ttu-id="a554a-161">Quando terminar, clique no botão **OK** na parte inferior da folha **Configuração do SQL Server** para salvar suas alterações.</span><span class="sxs-lookup"><span data-stu-id="a554a-161">When finished, click the **OK** button on the bottom of the **SQL Server configuration** blade to save your changes.</span></span>

<span data-ttu-id="a554a-162">Se você for habilitar a Aplicação de Patch Automatizada pela primeira vez, o Azure configurará o Agente IaaS do SQL Server em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="a554a-162">If you are enabling Automated Patching for the first time, Azure configures the SQL Server IaaS Agent in the background.</span></span> <span data-ttu-id="a554a-163">Durante esse tempo, o portal do Azure não mostrará que a Aplicação de Patch Automatizada está configurada.</span><span class="sxs-lookup"><span data-stu-id="a554a-163">During this time, the Azure portal might not show that Automated Patching is configured.</span></span> <span data-ttu-id="a554a-164">Aguarde alguns minutos para que o agente seja instalado e configurado.</span><span class="sxs-lookup"><span data-stu-id="a554a-164">Wait several minutes for the agent to be installed, configured.</span></span> <span data-ttu-id="a554a-165">Depois disso, o portal do Azure reflete as novas configurações.</span><span class="sxs-lookup"><span data-stu-id="a554a-165">After that the Azure portal reflects the new settings.</span></span>

> [!NOTE]
> <span data-ttu-id="a554a-166">Você também pode configurar a Aplicação de Patch Automatizada usando um modelo.</span><span class="sxs-lookup"><span data-stu-id="a554a-166">You can also configure Automated Patching using a template.</span></span> <span data-ttu-id="a554a-167">Para obter mais informações, consulte o [Modelo de início rápido do Azure para a Aplicação de Patch Automatizada](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autopatching-update).</span><span class="sxs-lookup"><span data-stu-id="a554a-167">For more information, see [Azure quickstart template for Automated Patching](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autopatching-update).</span></span>
> 
> 

## <a name="configuration-with-powershell"></a><span data-ttu-id="a554a-168">Configuração com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="a554a-168">Configuration with PowerShell</span></span>
<span data-ttu-id="a554a-169">Depois de provisionar sua VM do SQL, use o PowerShell para configurar a Aplicação de Patch Automatizada.</span><span class="sxs-lookup"><span data-stu-id="a554a-169">After provisioning your SQL VM, use PowerShell to configure Automated Patching.</span></span>

<span data-ttu-id="a554a-170">No exemplo a seguir, o PowerShell é usado para configurar a Aplicação de Patch Automatizada em uma VM existente do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a554a-170">In the following example, PowerShell is used to configure Automated Patching on an existing SQL Server VM.</span></span> <span data-ttu-id="a554a-171">O comando **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig** configura uma nova janela de manutenção para atualizações automáticas.</span><span class="sxs-lookup"><span data-stu-id="a554a-171">The **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig** command configures a new maintenance window for automatic updates.</span></span>

    $vmname = "vmname"
    $resourcegroupname = "resourcegroupname"
    $aps = AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Set-AzureRmVMSqlServerExtension -AutoPatchingSettings $aps -VMName $vmname -ResourceGroupName $resourcegroupname

<span data-ttu-id="a554a-172">Com base neste exemplo, a tabela a seguir descreve o efeito prático sobre a VM do Azure de destino:</span><span class="sxs-lookup"><span data-stu-id="a554a-172">Based on this example, the following table describes the practical effect on the target Azure VM:</span></span>

| <span data-ttu-id="a554a-173">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="a554a-173">Parameter</span></span> | <span data-ttu-id="a554a-174">Efeito</span><span class="sxs-lookup"><span data-stu-id="a554a-174">Effect</span></span> |
| --- | --- |
| <span data-ttu-id="a554a-175">**DayOfWeek**</span><span class="sxs-lookup"><span data-stu-id="a554a-175">**DayOfWeek**</span></span> |<span data-ttu-id="a554a-176">Patches instalados toda quinta-feira.</span><span class="sxs-lookup"><span data-stu-id="a554a-176">Patches installed every Thursday.</span></span> |
| <span data-ttu-id="a554a-177">**MaintenanceWindowStartingHour**</span><span class="sxs-lookup"><span data-stu-id="a554a-177">**MaintenanceWindowStartingHour**</span></span> |<span data-ttu-id="a554a-178">Inicia as atualizações às 11h.</span><span class="sxs-lookup"><span data-stu-id="a554a-178">Begin updates at 11:00am.</span></span> |
| <span data-ttu-id="a554a-179">**MaintenanceWindowsDuration**</span><span class="sxs-lookup"><span data-stu-id="a554a-179">**MaintenanceWindowsDuration**</span></span> |<span data-ttu-id="a554a-180">Os patches devem ser instalados dentro de 120 minutos.</span><span class="sxs-lookup"><span data-stu-id="a554a-180">Patches must be installed within 120 minutes.</span></span> <span data-ttu-id="a554a-181">Com base na hora de início, eles devem estar concluídos até 13h.</span><span class="sxs-lookup"><span data-stu-id="a554a-181">Based on the start time, they must complete by 1:00pm.</span></span> |
| <span data-ttu-id="a554a-182">**PatchCategory**</span><span class="sxs-lookup"><span data-stu-id="a554a-182">**PatchCategory**</span></span> |<span data-ttu-id="a554a-183">A única configuração possível para esse parâmetro é **Important**.</span><span class="sxs-lookup"><span data-stu-id="a554a-183">The only possible setting for this parameter is **Important**.</span></span> |

<span data-ttu-id="a554a-184">Pode demorar vários minutos para instalar e configurar o Agente IaaS do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a554a-184">It could take several minutes to install and configure the SQL Server IaaS Agent.</span></span>

<span data-ttu-id="a554a-185">Para desabilitar a aplicação de Patch automatizada, execute o mesmo script sem o parâmetro **-Enable** para **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig**.</span><span class="sxs-lookup"><span data-stu-id="a554a-185">To disable Automated Patching, run the same script without the **-Enable** parameter to the **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig**.</span></span> <span data-ttu-id="a554a-186">A ausência do parâmetro **-Enable** sinaliza o comando para desabilitar o recurso.</span><span class="sxs-lookup"><span data-stu-id="a554a-186">The absence of the **-Enable** parameter signals the command to disable the feature.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a554a-187">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a554a-187">Next steps</span></span>
<span data-ttu-id="a554a-188">Para obter informações sobre outras tarefas de automação disponíveis, consulte [Extensão do agente IaaS do SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="a554a-188">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="a554a-189">Para obter mais informações sobre como executar o SQL Server em VMs do Azure, consulte [Visão geral do SQL Server em Máquinas Virtuais do Azure](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a554a-189">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

