---
title: "aaaAutomated aplicação de patches para VMs do SQL Server (Gerenciador de recursos) | Microsoft Docs"
description: "Explica o recurso de aplicação de patch automatizada hello para SQL Server máquinas virtuais em execução no Azure usando o Gerenciador de recursos."
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
ms.openlocfilehash: 8bb8d0fb265e69d7bbf1fa047f5ceef02e7c56fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="automated-patching-for-sql-server-in-azure-virtual-machines-resource-manager"></a><span data-ttu-id="0cb09-103">Aplicação de patch automatizada para o SQL Server em Máquinas Virtuais do Azure (Gerenciador de Recursos)</span><span class="sxs-lookup"><span data-stu-id="0cb09-103">Automated Patching for SQL Server in Azure Virtual Machines (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0cb09-104">Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="0cb09-104">Resource Manager</span></span>](virtual-machines-windows-sql-automated-patching.md)
> * [<span data-ttu-id="0cb09-105">Clássico</span><span class="sxs-lookup"><span data-stu-id="0cb09-105">Classic</span></span>](../classic/sql-automated-patching.md)
> 
> 

<span data-ttu-id="0cb09-106">A aplicação de patch automatizada estabelece uma janela de manutenção para uma Máquina Virtual do Azure que executa o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0cb09-106">Automated Patching establishes a maintenance window for an Azure Virtual Machine running SQL Server.</span></span> <span data-ttu-id="0cb09-107">Atualizações automáticas só podem ser instaladas durante esta janela de manutenção.</span><span class="sxs-lookup"><span data-stu-id="0cb09-107">Automated Updates can only be installed during this maintenance window.</span></span> <span data-ttu-id="0cb09-108">Para o SQL Server, esse rescriction garante que as atualizações do sistema e qualquer reinicialização associada ocorre no melhor tempo possível Olá para o banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="0cb09-108">For SQL Server, this rescriction ensures that system updates and any associated restarts occur at hello best possible time for hello database.</span></span> <span data-ttu-id="0cb09-109">Aplicação de patch automatizada depende Olá [extensão do SQL Server IaaS Agent](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="0cb09-109">Automated Patching depends on hello [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="0cb09-110">tooview Olá clássico versão deste artigo, consulte [aplicação de patch automatizada para SQL Server no Azure máquinas virtuais clássicas](../classic/sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="0cb09-110">tooview hello classic version of this article, see [Automated Patching for SQL Server in Azure Virtual Machines Classic](../classic/sql-automated-patching.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0cb09-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0cb09-111">Prerequisites</span></span>
<span data-ttu-id="0cb09-112">toouse aplicação de patch automatizada, considere Olá pré-requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="0cb09-112">toouse Automated Patching, consider hello following prerequisites:</span></span>

<span data-ttu-id="0cb09-113">**Sistema operacional**:</span><span class="sxs-lookup"><span data-stu-id="0cb09-113">**Operating System**:</span></span>

* <span data-ttu-id="0cb09-114">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="0cb09-114">Windows Server 2012</span></span>
* <span data-ttu-id="0cb09-115">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="0cb09-115">Windows Server 2012 R2</span></span>
* <span data-ttu-id="0cb09-116">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="0cb09-116">Windows Server 2016</span></span>

<span data-ttu-id="0cb09-117">**Versão do SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="0cb09-117">**SQL Server version**:</span></span>

* <span data-ttu-id="0cb09-118">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="0cb09-118">SQL Server 2012</span></span>
* <span data-ttu-id="0cb09-119">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="0cb09-119">SQL Server 2014</span></span>
* <span data-ttu-id="0cb09-120">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="0cb09-120">SQL Server 2016</span></span>

<span data-ttu-id="0cb09-121">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="0cb09-121">**Azure PowerShell**:</span></span>

* <span data-ttu-id="0cb09-122">[Olá mais recente do Azure PowerShell comandos de instalação](/powershell/azure/overview) se você planejar tooconfigure aplicação de patch automatizada com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0cb09-122">[Install hello latest Azure PowerShell commands](/powershell/azure/overview) if you plan tooconfigure Automated Patching with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="0cb09-123">Aplicação de patch automatizada depende Olá extensão do SQL Server IaaS Agent.</span><span class="sxs-lookup"><span data-stu-id="0cb09-123">Automated Patching relies on hello SQL Server IaaS Agent Extension.</span></span> <span data-ttu-id="0cb09-124">As imagens atuais da galeria da máquina virtual do SQL adicionam essa extensão por padrão.</span><span class="sxs-lookup"><span data-stu-id="0cb09-124">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="0cb09-125">Para obter mais informações, consulte [Extensão do agente IaaS do SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="0cb09-125">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>
> 
> 

## <a name="settings"></a><span data-ttu-id="0cb09-126">Configurações</span><span class="sxs-lookup"><span data-stu-id="0cb09-126">Settings</span></span>
<span data-ttu-id="0cb09-127">Olá, tabela a seguir descreve as opções de saudação que podem ser configuradas para aplicação de patch automatizada.</span><span class="sxs-lookup"><span data-stu-id="0cb09-127">hello following table describes hello options that can be configured for Automated Patching.</span></span> <span data-ttu-id="0cb09-128">etapas de configuração real de saudação variam dependendo se você usar Olá portal do Azure ou comandos do PowerShell do Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="0cb09-128">hello actual configuration steps vary depending on whether you use hello Azure portal or Azure Windows PowerShell commands.</span></span>

| <span data-ttu-id="0cb09-129">Configuração</span><span class="sxs-lookup"><span data-stu-id="0cb09-129">Setting</span></span> | <span data-ttu-id="0cb09-130">Valores possíveis</span><span class="sxs-lookup"><span data-stu-id="0cb09-130">Possible values</span></span> | <span data-ttu-id="0cb09-131">Descrição</span><span class="sxs-lookup"><span data-stu-id="0cb09-131">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0cb09-132">**Aplicação de patch automatizada**</span><span class="sxs-lookup"><span data-stu-id="0cb09-132">**Automated Patching**</span></span> |<span data-ttu-id="0cb09-133">Habilitar/desabilitar (Desabilitado)</span><span class="sxs-lookup"><span data-stu-id="0cb09-133">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="0cb09-134">Habilita ou desabilita a Aplicação de Patch Automatizada para uma máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="0cb09-134">Enables or disables Automated Patching for an Azure virtual machine.</span></span> |
| <span data-ttu-id="0cb09-135">**Agenda de manutenção**</span><span class="sxs-lookup"><span data-stu-id="0cb09-135">**Maintenance schedule**</span></span> |<span data-ttu-id="0cb09-136">Todos os dias, segunda-feira, terça-feira, quarta-feira, quinta-feira, sexta-feira, sábado e domingo</span><span class="sxs-lookup"><span data-stu-id="0cb09-136">Everyday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday</span></span> |<span data-ttu-id="0cb09-137">agenda de saudação para baixar e instalar atualizações do Windows, SQL Server e Microsoft para sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0cb09-137">hello schedule for downloading and installing Windows, SQL Server, and Microsoft updates for your virtual machine.</span></span> |
| <span data-ttu-id="0cb09-138">**Hora de início da manutenção**</span><span class="sxs-lookup"><span data-stu-id="0cb09-138">**Maintenance start hour**</span></span> |<span data-ttu-id="0cb09-139">0h a 24h</span><span class="sxs-lookup"><span data-stu-id="0cb09-139">0-24</span></span> |<span data-ttu-id="0cb09-140">Olá início local tempo tooupdate Olá VM.</span><span class="sxs-lookup"><span data-stu-id="0cb09-140">hello local start time tooupdate hello virtual machine.</span></span> |
| <span data-ttu-id="0cb09-141">**Duração da janela de manutenção**</span><span class="sxs-lookup"><span data-stu-id="0cb09-141">**Maintenance window duration**</span></span> |<span data-ttu-id="0cb09-142">30-180</span><span class="sxs-lookup"><span data-stu-id="0cb09-142">30-180</span></span> |<span data-ttu-id="0cb09-143">número de saudação de minutos permitidos download de saudação toocomplete e instalação de atualizações.</span><span class="sxs-lookup"><span data-stu-id="0cb09-143">hello number of minutes permitted toocomplete hello download and installation of updates.</span></span> |
| <span data-ttu-id="0cb09-144">**Categoria de patch**</span><span class="sxs-lookup"><span data-stu-id="0cb09-144">**Patch Category**</span></span> |<span data-ttu-id="0cb09-145">Importante</span><span class="sxs-lookup"><span data-stu-id="0cb09-145">Important</span></span> |<span data-ttu-id="0cb09-146">categoria de saudação do toodownload atualizações e instalar.</span><span class="sxs-lookup"><span data-stu-id="0cb09-146">hello category of updates toodownload and install.</span></span> |

## <a name="configuration-in-hello-portal"></a><span data-ttu-id="0cb09-147">Configuração no Portal de saudação</span><span class="sxs-lookup"><span data-stu-id="0cb09-147">Configuration in hello Portal</span></span>
<span data-ttu-id="0cb09-148">Você pode usar o hello tooconfigure portal do Azure aplicação de patch automatizada durante o provisionamento ou para máquinas virtuais existentes.</span><span class="sxs-lookup"><span data-stu-id="0cb09-148">You can use hello Azure portal tooconfigure Automated Patching during provisioning or for existing VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="0cb09-149">Novas VMs</span><span class="sxs-lookup"><span data-stu-id="0cb09-149">New VMs</span></span>
<span data-ttu-id="0cb09-150">Saudação de uso do Azure tooconfigure portal aplicação de patch automatizada quando você cria uma nova máquina Virtual do SQL Server no modelo de implantação do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="0cb09-150">Use hello Azure portal tooconfigure Automated Patching when you create a new SQL Server Virtual Machine in hello Resource Manager deployment model.</span></span>

<span data-ttu-id="0cb09-151">Em Olá **configurações do SQL Server** folha, selecione **aplicação de patches automatizada**.</span><span class="sxs-lookup"><span data-stu-id="0cb09-151">In hello **SQL Server settings** blade, select **Automated patching**.</span></span> <span data-ttu-id="0cb09-152">Olá, seguinte captura de tela de portal do Azure mostra Olá **SQL Automated Patching** folha.</span><span class="sxs-lookup"><span data-stu-id="0cb09-152">hello following Azure portal screenshot shows hello **SQL Automated Patching** blade.</span></span>

![Aplicação de Patch Automática do SQL no Portal do Azure](./media/virtual-machines-windows-sql-automated-patching/azure-sql-arm-patching.png)

<span data-ttu-id="0cb09-154">Para o contexto, consulte o tópico completo do hello sobre [Provisionando uma máquina virtual do SQL Server no Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="0cb09-154">For context, see hello complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="0cb09-155">VMs existentes</span><span class="sxs-lookup"><span data-stu-id="0cb09-155">Existing VMs</span></span>
<span data-ttu-id="0cb09-156">Para máquinas virtuais existentes do SQL Server, selecione sua máquina virtual do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0cb09-156">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="0cb09-157">Em seguida, selecione Olá **configuração do SQL Server** seção Olá **configurações** folha.</span><span class="sxs-lookup"><span data-stu-id="0cb09-157">Then select hello **SQL Server configuration** section of hello **Settings** blade.</span></span>

![Aplicação de Patch Automática do SQL para VMs existentes](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-existing-vms.png)

<span data-ttu-id="0cb09-159">Em Olá **configuração do SQL Server** folha, clique em Olá **editar** botão Olá automatizada seção aplicação de patch.</span><span class="sxs-lookup"><span data-stu-id="0cb09-159">In hello **SQL Server configuration** blade, click hello **Edit** button in hello Automated patching section.</span></span>

![Configurar a Aplicação de Patch Automática do SQL para VMs existentes](./media/virtual-machines-windows-sql-automated-patching/azure-sql-rm-patching-configuration.png)

<span data-ttu-id="0cb09-161">Quando terminar, clique em Olá **Okey** botão na parte inferior de saudação da saudação **configuração do SQL Server** folha toosave suas alterações.</span><span class="sxs-lookup"><span data-stu-id="0cb09-161">When finished, click hello **OK** button on hello bottom of hello **SQL Server configuration** blade toosave your changes.</span></span>

<span data-ttu-id="0cb09-162">Se você estiver habilitando aplicação de patch automatizada para Olá primeira vez, o Azure configura Olá IaaS do SQL Server Agent no plano de fundo de saudação.</span><span class="sxs-lookup"><span data-stu-id="0cb09-162">If you are enabling Automated Patching for hello first time, Azure configures hello SQL Server IaaS Agent in hello background.</span></span> <span data-ttu-id="0cb09-163">Durante esse tempo, Olá portal do Azure não pode mostrar que a aplicação de patch automatizada está configurada.</span><span class="sxs-lookup"><span data-stu-id="0cb09-163">During this time, hello Azure portal might not show that Automated Patching is configured.</span></span> <span data-ttu-id="0cb09-164">Aguarde alguns minutos para Olá agente toobe instalado, configurado.</span><span class="sxs-lookup"><span data-stu-id="0cb09-164">Wait several minutes for hello agent toobe installed, configured.</span></span> <span data-ttu-id="0cb09-165">Depois que hello Azure portal reflete novas configurações de saudação.</span><span class="sxs-lookup"><span data-stu-id="0cb09-165">After that hello Azure portal reflects hello new settings.</span></span>

> [!NOTE]
> <span data-ttu-id="0cb09-166">Você também pode configurar a Aplicação de Patch Automatizada usando um modelo.</span><span class="sxs-lookup"><span data-stu-id="0cb09-166">You can also configure Automated Patching using a template.</span></span> <span data-ttu-id="0cb09-167">Para obter mais informações, consulte o [Modelo de início rápido do Azure para a Aplicação de Patch Automatizada](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autopatching-update).</span><span class="sxs-lookup"><span data-stu-id="0cb09-167">For more information, see [Azure quickstart template for Automated Patching](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autopatching-update).</span></span>
> 
> 

## <a name="configuration-with-powershell"></a><span data-ttu-id="0cb09-168">Configuração com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="0cb09-168">Configuration with PowerShell</span></span>
<span data-ttu-id="0cb09-169">Depois de provisionar a VM do SQL, use PowerShell tooconfigure aplicação de patch automatizada.</span><span class="sxs-lookup"><span data-stu-id="0cb09-169">After provisioning your SQL VM, use PowerShell tooconfigure Automated Patching.</span></span>

<span data-ttu-id="0cb09-170">Olá exemplo a seguir, PowerShell é usado tooconfigure aplicação de patch automatizada em uma VM existente do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0cb09-170">In hello following example, PowerShell is used tooconfigure Automated Patching on an existing SQL Server VM.</span></span> <span data-ttu-id="0cb09-171">Olá **AzureRM.Compute\New AzureVMSqlServerAutoPatchingConfig** comando configura uma nova janela de manutenção para atualizações automáticas.</span><span class="sxs-lookup"><span data-stu-id="0cb09-171">hello **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig** command configures a new maintenance window for automatic updates.</span></span>

    $vmname = "vmname"
    $resourcegroupname = "resourcegroupname"
    $aps = AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig -Enable -DayOfWeek "Thursday" -MaintenanceWindowStartingHour 11 -MaintenanceWindowDuration 120  -PatchCategory "Important"

    Set-AzureRmVMSqlServerExtension -AutoPatchingSettings $aps -VMName $vmname -ResourceGroupName $resourcegroupname

<span data-ttu-id="0cb09-172">Com base neste exemplo, hello tabela a seguir descreve a efeito prático Olá no destino Olá VM do Azure:</span><span class="sxs-lookup"><span data-stu-id="0cb09-172">Based on this example, hello following table describes hello practical effect on hello target Azure VM:</span></span>

| <span data-ttu-id="0cb09-173">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="0cb09-173">Parameter</span></span> | <span data-ttu-id="0cb09-174">Efeito</span><span class="sxs-lookup"><span data-stu-id="0cb09-174">Effect</span></span> |
| --- | --- |
| <span data-ttu-id="0cb09-175">**DayOfWeek**</span><span class="sxs-lookup"><span data-stu-id="0cb09-175">**DayOfWeek**</span></span> |<span data-ttu-id="0cb09-176">Patches instalados toda quinta-feira.</span><span class="sxs-lookup"><span data-stu-id="0cb09-176">Patches installed every Thursday.</span></span> |
| <span data-ttu-id="0cb09-177">**MaintenanceWindowStartingHour**</span><span class="sxs-lookup"><span data-stu-id="0cb09-177">**MaintenanceWindowStartingHour**</span></span> |<span data-ttu-id="0cb09-178">Inicia as atualizações às 11h.</span><span class="sxs-lookup"><span data-stu-id="0cb09-178">Begin updates at 11:00am.</span></span> |
| <span data-ttu-id="0cb09-179">**MaintenanceWindowsDuration**</span><span class="sxs-lookup"><span data-stu-id="0cb09-179">**MaintenanceWindowsDuration**</span></span> |<span data-ttu-id="0cb09-180">Os patches devem ser instalados dentro de 120 minutos.</span><span class="sxs-lookup"><span data-stu-id="0cb09-180">Patches must be installed within 120 minutes.</span></span> <span data-ttu-id="0cb09-181">Com base na hora de início do hello, elas devem concluir até 1:00 pm.</span><span class="sxs-lookup"><span data-stu-id="0cb09-181">Based on hello start time, they must complete by 1:00pm.</span></span> |
| <span data-ttu-id="0cb09-182">**PatchCategory**</span><span class="sxs-lookup"><span data-stu-id="0cb09-182">**PatchCategory**</span></span> |<span data-ttu-id="0cb09-183">Olá única configuração possível para esse parâmetro é **importante**.</span><span class="sxs-lookup"><span data-stu-id="0cb09-183">hello only possible setting for this parameter is **Important**.</span></span> |

<span data-ttu-id="0cb09-184">Ele pode levar vários tooinstall de minutos e configure Olá SQL Server IaaS Agent.</span><span class="sxs-lookup"><span data-stu-id="0cb09-184">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span>

<span data-ttu-id="0cb09-185">toodisable aplicação de patch automatizada, Olá execução mesmo script sem Olá **-habilitar** parâmetro toohello **AzureRM.Compute\New AzureVMSqlServerAutoPatchingConfig**.</span><span class="sxs-lookup"><span data-stu-id="0cb09-185">toodisable Automated Patching, run hello same script without hello **-Enable** parameter toohello **AzureRM.Compute\New-AzureVMSqlServerAutoPatchingConfig**.</span></span> <span data-ttu-id="0cb09-186">Olá ausência de saudação **-habilitar** recurso de saudação do parâmetro sinais Olá comando toodisable.</span><span class="sxs-lookup"><span data-stu-id="0cb09-186">hello absence of hello **-Enable** parameter signals hello command toodisable hello feature.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0cb09-187">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0cb09-187">Next steps</span></span>
<span data-ttu-id="0cb09-188">Para obter informações sobre outras tarefas de automação disponíveis, consulte [Extensão do agente IaaS do SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="0cb09-188">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="0cb09-189">Para obter mais informações sobre como executar o SQL Server em VMs do Azure, consulte [Visão geral do SQL Server em Máquinas Virtuais do Azure](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0cb09-189">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

