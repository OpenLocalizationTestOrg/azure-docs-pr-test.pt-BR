---
title: "tarefas de gerenciamento de aaaAutomate em VMs do SQL (clássico) | Microsoft Docs"
description: "Este tópico descreve como toomanage Olá extensão do agente do SQL Server, que automatiza tarefas de administração do SQL Server específicas. Entre elas estão o Backup Automatizado, a Aplicação de Patch Automatizada e a Integração do Cofre de Chaves do Azure. Este tópico usa o modo de implantação clássico hello."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a9bda2e7-cdba-427c-bc30-77cde4376f3a
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a1dc011e0526845701eaf0c365007938f9ee32ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-hello-sql-server-agent-extension-classic"></a><span data-ttu-id="ccc55-105">Automatizar tarefas de gerenciamento em máquinas virtuais do Azure com hello extensão do SQL Server Agent (clássico)</span><span class="sxs-lookup"><span data-stu-id="ccc55-105">Automate management tasks on Azure Virtual Machines with hello SQL Server Agent Extension (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ccc55-106">Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="ccc55-106">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-server-agent-extension.md)
> * [<span data-ttu-id="ccc55-107">Clássico</span><span class="sxs-lookup"><span data-stu-id="ccc55-107">Classic</span></span>](../classic/sql-server-agent-extension.md)
> 
>
 
<span data-ttu-id="ccc55-108">Olá extensão do agente IaaS do SQL Server (SQLIaaSAgent) é executado em máquinas virtuais do Azure tooautomate as tarefas de administração.</span><span class="sxs-lookup"><span data-stu-id="ccc55-108">hello SQL Server IaaS Agent Extension (SQLIaaSAgent) runs on Azure virtual machines tooautomate administration tasks.</span></span> <span data-ttu-id="ccc55-109">Este tópico fornece uma visão geral dos serviços de saudação suportados pela extensão de hello, bem como instruções de instalação, status e remoção.</span><span class="sxs-lookup"><span data-stu-id="ccc55-109">This topic provides an overview of hello services supported by hello extension as well as instructions for installation, status, and removal.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="ccc55-110">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ccc55-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ccc55-111">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="ccc55-111">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="ccc55-112">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="ccc55-112">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="ccc55-113">versão do Gerenciador de recursos de saudação tooview deste artigo, consulte [extensão do SQL Server Agent para o SQL Server VMs Resource Manager](../sql/virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="ccc55-113">tooview hello Resource Manager version of this article, see [SQL Server Agent Extension for SQL Server VMs Resource Manager](../sql/virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="supported-services"></a><span data-ttu-id="ccc55-114">Serviços com suporte</span><span class="sxs-lookup"><span data-stu-id="ccc55-114">Supported services</span></span>
<span data-ttu-id="ccc55-115">Olá extensão do SQL Server IaaS Agent dá suporte a saudação tarefas de administração a seguir:</span><span class="sxs-lookup"><span data-stu-id="ccc55-115">hello SQL Server IaaS Agent Extension supports hello following administration tasks:</span></span>

| <span data-ttu-id="ccc55-116">Recurso de administração</span><span class="sxs-lookup"><span data-stu-id="ccc55-116">Administration feature</span></span> | <span data-ttu-id="ccc55-117">Descrição</span><span class="sxs-lookup"><span data-stu-id="ccc55-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ccc55-118">**Backup Automatizado do SQL**</span><span class="sxs-lookup"><span data-stu-id="ccc55-118">**SQL Automated Backup**</span></span> |<span data-ttu-id="ccc55-119">Automatiza Olá agendamento de backups para todos os bancos de dados para instância padrão de saudação do SQL Server na VM de saudação.</span><span class="sxs-lookup"><span data-stu-id="ccc55-119">Automates hello scheduling of backups for all databases for hello default instance of SQL Server in hello VM.</span></span> <span data-ttu-id="ccc55-120">Para saber mais, veja [Backup automatizado para o SQL Server em Máquinas Virtuais do Azure (Clássico)](../classic/sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="ccc55-120">For more information, see [Automated backup for SQL Server in Azure Virtual Machines (Classic)](../classic/sql-automated-backup.md).</span></span> |
| <span data-ttu-id="ccc55-121">**Aplicação de patch automatizada do SQL**</span><span class="sxs-lookup"><span data-stu-id="ccc55-121">**SQL Automated Patching**</span></span> |<span data-ttu-id="ccc55-122">Configura uma janela de manutenção durante as atualizações tooyour VM pode levar coloca, para que você possa evitar atualizações durante horários de pico para sua carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="ccc55-122">Configures a maintenance window during which updates tooyour VM can take place, so  you can avoid updates during peak times for your workload.</span></span> <span data-ttu-id="ccc55-123">Para obter mais informações, confira [Aplicação de patch automatizada para SQL Server em máquinas virtuais do Azure (Clássico)](../classic/sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="ccc55-123">For more information, see [Automated patching for SQL Server in Azure Virtual Machines (Classic)](../classic/sql-automated-patching.md).</span></span> |
| <span data-ttu-id="ccc55-124">**Integração do Cofre da Chave do Azure**</span><span class="sxs-lookup"><span data-stu-id="ccc55-124">**Azure Key Vault Integration**</span></span> |<span data-ttu-id="ccc55-125">Permite que você tooautomatically instalar e configurar o Cofre de chaves do Azure na VM do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ccc55-125">Enables you tooautomatically install and configure Azure Key Vault on your SQL Server VM.</span></span> <span data-ttu-id="ccc55-126">Para saber mais, confira [Configurar a Integração do Cofre de Chaves do Azure para o SQL Server em VMs do Azure (Clássico)](../classic/ps-sql-keyvault.md).</span><span class="sxs-lookup"><span data-stu-id="ccc55-126">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs (Classic)](../classic/ps-sql-keyvault.md).</span></span> |

## <a name="prerequisites"></a><span data-ttu-id="ccc55-127">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ccc55-127">Prerequisites</span></span>
<span data-ttu-id="ccc55-128">Requisitos toouse Olá extensão do SQL Server IaaS Agent na sua VM:</span><span class="sxs-lookup"><span data-stu-id="ccc55-128">Requirements toouse hello SQL Server IaaS Agent Extension on your VM:</span></span>

### <a name="operating-system"></a><span data-ttu-id="ccc55-129">Sistema operacional:</span><span class="sxs-lookup"><span data-stu-id="ccc55-129">Operating System:</span></span>
* <span data-ttu-id="ccc55-130">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="ccc55-130">Windows Server 2012</span></span>
* <span data-ttu-id="ccc55-131">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="ccc55-131">Windows Server 2012 R2</span></span>
* <span data-ttu-id="ccc55-132">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="ccc55-132">Windows Server 2016</span></span>

### <a name="sql-server-versions"></a><span data-ttu-id="ccc55-133">Versões do SQL Server:</span><span class="sxs-lookup"><span data-stu-id="ccc55-133">SQL Server versions:</span></span>
* <span data-ttu-id="ccc55-134">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="ccc55-134">SQL Server 2012</span></span>
* <span data-ttu-id="ccc55-135">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="ccc55-135">SQL Server 2014</span></span>
* <span data-ttu-id="ccc55-136">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="ccc55-136">SQL Server 2016</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="ccc55-137">PowerShell do Azure:</span><span class="sxs-lookup"><span data-stu-id="ccc55-137">Azure PowerShell:</span></span>
<span data-ttu-id="ccc55-138">[Baixar e configurar os comandos do PowerShell do Azure mais recentes Olá](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ccc55-138">[Download and configure hello latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="ccc55-139">Inicie o Windows PowerShell e conectá-lo tooyour assinatura do Azure com hello **Add-AzureAccount** comando.</span><span class="sxs-lookup"><span data-stu-id="ccc55-139">Start Windows PowerShell, and connect it tooyour Azure subscription with hello **Add-AzureAccount** command.</span></span>

    Add-AzureAccount

<span data-ttu-id="ccc55-140">Se você tiver várias assinaturas, use **Select-AzureSubscription** tooselect assinatura de saudação que contém o VM clássico.</span><span class="sxs-lookup"><span data-stu-id="ccc55-140">If you have multiple subscriptions, use **Select-AzureSubscription** tooselect hello subscription that contains your target classic VM.</span></span>

    Select-AzureSubscription -SubscriptionName <subscriptionname>

<span data-ttu-id="ccc55-141">Neste ponto, você pode obter uma lista de máquinas virtuais clássicas de saudação e seus nomes de serviço associado com hello **Get-AzureVM** comando.</span><span class="sxs-lookup"><span data-stu-id="ccc55-141">At this point, you can get a list of hello classic virtual machines and their associated service names with hello **Get-AzureVM** command.</span></span>

    Get-AzureVM

## <a name="installation"></a><span data-ttu-id="ccc55-142">Instalação</span><span class="sxs-lookup"><span data-stu-id="ccc55-142">Installation</span></span>
<span data-ttu-id="ccc55-143">Para VMs clássicas, você deve usar o PowerShell tooinstall Olá extensão do SQL Server IaaS Agent e configurar seus serviços associados.</span><span class="sxs-lookup"><span data-stu-id="ccc55-143">For classic VMs, you must use PowerShell tooinstall hello SQL Server IaaS Agent Extension and configure its associated services.</span></span> <span data-ttu-id="ccc55-144">Saudação de uso **AzureVMSqlServerExtension conjunto** extensão de saudação de tooinstall de cmdlet do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ccc55-144">Use hello **Set-AzureVMSqlServerExtension** PowerShell cmdlet tooinstall hello extension.</span></span> <span data-ttu-id="ccc55-145">Por exemplo, hello comando a seguir instala a extensão de saudação em uma VM do Windows Server (clássico) e nomeia "SQLIaaSExtension".</span><span class="sxs-lookup"><span data-stu-id="ccc55-145">For example, hello following command installs hello extension on a Windows Server VM (classic) and names it "SQLIaaSExtension".</span></span>

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -ReferenceName "SQLIaasExtension" -Version "1.2" | Update-AzureVM

<span data-ttu-id="ccc55-146">Se você atualizar a versão mais recente toohello de saudação extensão do agente SQL IaaS, você deve reiniciar a máquina virtual após a atualização da extensão Olá.</span><span class="sxs-lookup"><span data-stu-id="ccc55-146">If you update toohello latest version of hello SQL IaaS Agent Extension, you must restart your virtual machine after updating hello extension.</span></span>

> [!NOTE]
> <span data-ttu-id="ccc55-147">Máquinas virtuais clássicas não têm uma opção tooinstall e configurar Olá extensão do agente SQL IaaS por meio do portal hello.</span><span class="sxs-lookup"><span data-stu-id="ccc55-147">Classic virtual machines do not have an option tooinstall and configure hello SQL IaaS Agent Extension through hello portal.</span></span>
> 
> 

## <a name="status"></a><span data-ttu-id="ccc55-148">Status</span><span class="sxs-lookup"><span data-stu-id="ccc55-148">Status</span></span>
<span data-ttu-id="ccc55-149">Tooverify unidirecional que extensão hello está instalado é o status do agente de saudação tooview no hello Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ccc55-149">One way tooverify that hello extension is installed is tooview hello agent status in hello Azure Portal.</span></span> <span data-ttu-id="ccc55-150">Selecione uma máquina virtual listada na folha da máquina virtual hello e, em seguida, clique em **extensões**.</span><span class="sxs-lookup"><span data-stu-id="ccc55-150">Select a virtual machine listed in hello virtual machine blade, and then click on **Extensions**.</span></span> <span data-ttu-id="ccc55-151">Você deve ver Olá **SQLIaaSAgent** extensão listado.</span><span class="sxs-lookup"><span data-stu-id="ccc55-151">You should see hello **SQLIaaSAgent** extension listed.</span></span>

![Extensão do Agente IaaS do SQL Server no Portal do Azure](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-portal.png)

<span data-ttu-id="ccc55-153">Você também pode usar o hello **AzureVMSqlServerExtension Get** cmdlet do Powershell do Azure.</span><span class="sxs-lookup"><span data-stu-id="ccc55-153">You can also use hello **Get-AzureVMSqlServerExtension** Azure Powershell cmdlet.</span></span>

    Get-AzureVM –ServiceName "service" –Name "vmname" | Get-AzureVMSqlServerExtension

## <a name="removal"></a><span data-ttu-id="ccc55-154">Remoção</span><span class="sxs-lookup"><span data-stu-id="ccc55-154">Removal</span></span>
<span data-ttu-id="ccc55-155">Olá Portal do Azure, você pode desinstalar extensão Olá clicando reticências Olá em Olá **extensões** folha de propriedades de sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ccc55-155">In hello Azure Portal, you can uninstall hello extension by clicking hello ellipsis on hello **Extensions** blade of your virtual machine properties.</span></span> <span data-ttu-id="ccc55-156">Em seguida, clique em **Desinstalar**.</span><span class="sxs-lookup"><span data-stu-id="ccc55-156">Then click **Uninstall**.</span></span>

![Desinstalar Olá extensão do agente IaaS do SQL Server no Portal do Azure](./media/virtual-machines-windows-classic-sql-server-agent-extension/azure-sql-server-iaas-agent-uninstall.png)

<span data-ttu-id="ccc55-158">Você também pode usar o hello **AzureVMSqlServerExtension remover** cmdlet do Powershell.</span><span class="sxs-lookup"><span data-stu-id="ccc55-158">You can also use hello **Remove-AzureVMSqlServerExtension** Powershell cmdlet.</span></span>

    Get-AzureVM –ServiceName "service" –Name "vmname" | Remove-AzureVMSqlServerExtension | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="ccc55-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ccc55-159">Next Steps</span></span>
<span data-ttu-id="ccc55-160">Começar a usar um dos serviços de Olá Olá extensão oferece suportados.</span><span class="sxs-lookup"><span data-stu-id="ccc55-160">Begin using one of hello services supported by hello extension.</span></span> <span data-ttu-id="ccc55-161">Para obter mais detalhes, consulte os tópicos de saudação referenciados no hello [suporte para serviços](#supported-services) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="ccc55-161">For more details, see hello topics referenced in hello [Supported services](#supported-services) section of this article.</span></span>

<span data-ttu-id="ccc55-162">Para obter mais informações sobre como executar o SQL Server em Máquinas Virtuais do Azure, veja [Visão geral do SQL Server em Máquinas Virtuais do Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ccc55-162">For more information about running SQL Server on Azure Virtual Machines, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

