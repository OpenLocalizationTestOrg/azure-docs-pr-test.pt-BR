---
title: tarefas de gerenciamento de aaaAutomate em VMs do SQL (Gerenciador de recursos) | Microsoft Docs
description: "Este tópico descreve como toomanage Olá extensão do agente do SQL Server, que automatiza tarefas de administração do SQL Server específicas. Entre elas estão o Backup Automatizado, a Aplicação de Patch Automatizada e a Integração do Cofre de Chaves do Azure. Este tópico usa o modo de implantação do Gerenciador de recursos de saudação."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: effe4e2f-35b5-490a-b5ef-b06746083da4
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ae917612c4af59f12c0b083440673bdc555e9d56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-management-tasks-on-azure-virtual-machines-with-hello-sql-server-agent-extension-resource-manager"></a><span data-ttu-id="2dcf8-105">Automatizar tarefas de gerenciamento em máquinas virtuais do Azure com hello extensão do SQL Server Agent (Gerenciador de recursos)</span><span class="sxs-lookup"><span data-stu-id="2dcf8-105">Automate management tasks on Azure Virtual Machines with hello SQL Server Agent Extension (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2dcf8-106">Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="2dcf8-106">Resource Manager</span></span>](virtual-machines-windows-sql-server-agent-extension.md)
> * [<span data-ttu-id="2dcf8-107">Clássico</span><span class="sxs-lookup"><span data-stu-id="2dcf8-107">Classic</span></span>](../classic/sql-server-agent-extension.md)
> 
> 

<span data-ttu-id="2dcf8-108">Olá extensão do agente IaaS do SQL Server (SQLIaaSExtension) é executado em máquinas virtuais do Azure tooautomate as tarefas de administração.</span><span class="sxs-lookup"><span data-stu-id="2dcf8-108">hello SQL Server IaaS Agent Extension (SQLIaaSExtension) runs on Azure virtual machines tooautomate administration tasks.</span></span> <span data-ttu-id="2dcf8-109">Este tópico fornece uma visão geral dos serviços de saudação suportados pela extensão de hello, bem como instruções de instalação, status e remoção.</span><span class="sxs-lookup"><span data-stu-id="2dcf8-109">This topic provides an overview of hello services supported by hello extension as well as instructions for installation, status, and removal.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="2dcf8-110">tooview Olá clássico versão deste artigo, consulte [extensão do agente do SQL Server para SQL Server VMs clássico](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="2dcf8-110">tooview hello classic version of this article, see [SQL Server Agent Extension for SQL Server VMs Classic](../classic/sql-server-agent-extension.md).</span></span>

## <a name="supported-services"></a><span data-ttu-id="2dcf8-111">Serviços com suporte</span><span class="sxs-lookup"><span data-stu-id="2dcf8-111">Supported services</span></span>
<span data-ttu-id="2dcf8-112">Olá extensão do SQL Server IaaS Agent dá suporte a saudação tarefas de administração a seguir:</span><span class="sxs-lookup"><span data-stu-id="2dcf8-112">hello SQL Server IaaS Agent Extension supports hello following administration tasks:</span></span>

| <span data-ttu-id="2dcf8-113">Recurso de administração</span><span class="sxs-lookup"><span data-stu-id="2dcf8-113">Administration feature</span></span> | <span data-ttu-id="2dcf8-114">Descrição</span><span class="sxs-lookup"><span data-stu-id="2dcf8-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2dcf8-115">**Backup Automatizado do SQL**</span><span class="sxs-lookup"><span data-stu-id="2dcf8-115">**SQL Automated Backup**</span></span> |<span data-ttu-id="2dcf8-116">Automatiza Olá agendamento de backups para todos os bancos de dados para instância padrão de saudação do SQL Server na VM de saudação.</span><span class="sxs-lookup"><span data-stu-id="2dcf8-116">Automates hello scheduling of backups for all databases for hello default instance of SQL Server in hello VM.</span></span> <span data-ttu-id="2dcf8-117">Para saber mais, veja [Backup automatizado para SQL Server em máquinas virtuais do Azure (Resource Manager)](virtual-machines-windows-sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="2dcf8-117">For more information, see [Automated backup for SQL Server in Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-backup.md).</span></span> |
| <span data-ttu-id="2dcf8-118">**Aplicação de patch automatizada do SQL**</span><span class="sxs-lookup"><span data-stu-id="2dcf8-118">**SQL Automated Patching**</span></span> |<span data-ttu-id="2dcf8-119">Configura uma janela de manutenção durante as atualizações tooyour VM pode levar coloca, para que você possa evitar atualizações durante horários de pico para sua carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="2dcf8-119">Configures a maintenance window during which updates tooyour VM can take place, so  you can avoid updates during peak times for your workload.</span></span> <span data-ttu-id="2dcf8-120">Para saber mais, veja [Aplicação de patch automatizada para o SQL Server em Máquinas Virtuais do Azure (Resource Manager)](virtual-machines-windows-sql-automated-patching.md).</span><span class="sxs-lookup"><span data-stu-id="2dcf8-120">For more information, see [Automated patching for SQL Server in Azure Virtual Machines (Resource Manager)](virtual-machines-windows-sql-automated-patching.md).</span></span> |
| <span data-ttu-id="2dcf8-121">**Integração do Cofre da Chave do Azure**</span><span class="sxs-lookup"><span data-stu-id="2dcf8-121">**Azure Key Vault Integration**</span></span> |<span data-ttu-id="2dcf8-122">Permite que você tooautomatically instalar e configurar o Cofre de chaves do Azure na VM do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2dcf8-122">Enables you tooautomatically install and configure Azure Key Vault on your SQL Server VM.</span></span> <span data-ttu-id="2dcf8-123">Para saber mais, confira [Configurar a integração do Cofre de Chaves do Azure para SQL Server em VMs do Azure (Resource Manager)](virtual-machines-windows-ps-sql-keyvault.md).</span><span class="sxs-lookup"><span data-stu-id="2dcf8-123">For more information, see [Configure Azure Key Vault Integration for SQL Server on Azure VMs (Resource Manager)](virtual-machines-windows-ps-sql-keyvault.md).</span></span> |

<span data-ttu-id="2dcf8-124">Depois de instalado e em execução, Olá extensão do SQL Server IaaS Agent disponibiliza esses recursos de administração no painel de SQL Server de saudação do hello máquina virtual no hello Portal do Azure e por meio do PowerShell do Azure para imagens do marketplace do SQL Server e por meio de Azure PowerShell para instalações manuais de extensão de saudação.</span><span class="sxs-lookup"><span data-stu-id="2dcf8-124">Once installed and running, hello SQL Server IaaS Agent Extension makes these administration features available on hello SQL Server panel of hello virtual machine in hello Azure Portal and through Azure PowerShell for SQL Server marketplace images, and through Azure PowerShell for manual installations of hello extension.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="2dcf8-125">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2dcf8-125">Prerequisites</span></span>
<span data-ttu-id="2dcf8-126">Requisitos toouse Olá extensão do SQL Server IaaS Agent na sua VM:</span><span class="sxs-lookup"><span data-stu-id="2dcf8-126">Requirements toouse hello SQL Server IaaS Agent Extension on your VM:</span></span>

<span data-ttu-id="2dcf8-127">**Sistema operacional**:</span><span class="sxs-lookup"><span data-stu-id="2dcf8-127">**Operating System**:</span></span>

* <span data-ttu-id="2dcf8-128">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="2dcf8-128">Windows Server 2012</span></span>
* <span data-ttu-id="2dcf8-129">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="2dcf8-129">Windows Server 2012 R2</span></span>
* <span data-ttu-id="2dcf8-130">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="2dcf8-130">Windows Server 2016</span></span>

<span data-ttu-id="2dcf8-131">**Versões do SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="2dcf8-131">**SQL Server versions**:</span></span>

* <span data-ttu-id="2dcf8-132">SQL Server 2012</span><span class="sxs-lookup"><span data-stu-id="2dcf8-132">SQL Server 2012</span></span>
* <span data-ttu-id="2dcf8-133">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="2dcf8-133">SQL Server 2014</span></span>
* <span data-ttu-id="2dcf8-134">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="2dcf8-134">SQL Server 2016</span></span>

<span data-ttu-id="2dcf8-135">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="2dcf8-135">**Azure PowerShell**:</span></span>

* [<span data-ttu-id="2dcf8-136">Baixar e configurar os comandos do PowerShell do Azure mais recentes Olá</span><span class="sxs-lookup"><span data-stu-id="2dcf8-136">Download and configure hello latest Azure PowerShell commands</span></span>](/powershell/azure/overview)

## <a name="installation"></a><span data-ttu-id="2dcf8-137">Instalação</span><span class="sxs-lookup"><span data-stu-id="2dcf8-137">Installation</span></span>
<span data-ttu-id="2dcf8-138">Olá extensão do SQL Server IaaS Agent é instalado automaticamente quando você provisiona uma das imagens de galeria de máquina virtual saudação do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2dcf8-138">hello SQL Server IaaS Agent Extension is automatically installed when you provision one of hello SQL Server virtual machine gallery images.</span></span> <span data-ttu-id="2dcf8-139">Se você precisar de extensão de saudação tooreinstall manualmente em um dessas VMs do SQL Server, use Olá comando PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="2dcf8-139">If you need tooreinstall hello extension manually on one of these SQL Server VMs, use hello following PowerShell command:</span></span>

```powershell
Set-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension" -Version "1.2" -Location "East US 2"
```

<span data-ttu-id="2dcf8-140">Também é possível tooinstall Olá extensão do SQL Server IaaS Agent em uma máquina virtual de somente do sistema operacional Windows Server.</span><span class="sxs-lookup"><span data-stu-id="2dcf8-140">It is also possible tooinstall hello SQL Server IaaS Agent Extension on an OS-only Windows Server virtual machine.</span></span> <span data-ttu-id="2dcf8-141">Isso será suportado apenas se você tiver instalado manualmente o SQL Server nesta máquina.</span><span class="sxs-lookup"><span data-stu-id="2dcf8-141">This is only supported if you have also manually installed SQL Server on that machine.</span></span> <span data-ttu-id="2dcf8-142">Em seguida, instalar Olá extensão manualmente usando Olá mesmo **AzureVMSqlServerExtension conjunto** cmdlet do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2dcf8-142">Then install hello extension manually by using hello same **Set-AzureVMSqlServerExtension** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="2dcf8-143">Se você instalar manualmente o hello extensão do SQL Server IaaS Agent em uma VM somente do sistema operacional Windows Server, você não pode gerenciar as definições de configuração do SQL Server Olá por meio de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2dcf8-143">If you manually install hello SQL Server IaaS Agent Extension on an OS-only Windows Server VM, you can not manage hello SQL Server configuration settings through hello Azure portal.</span></span> <span data-ttu-id="2dcf8-144">Nesse cenário, você deverá fazer todas as alterações com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2dcf8-144">In this scenario, you must make all changes with PowerShell.</span></span>

## <a name="status"></a><span data-ttu-id="2dcf8-145">Status</span><span class="sxs-lookup"><span data-stu-id="2dcf8-145">Status</span></span>
<span data-ttu-id="2dcf8-146">Tooverify unidirecional que extensão hello está instalado é o status do agente de saudação tooview no hello Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2dcf8-146">One way tooverify that hello extension is installed is tooview hello agent status in hello Azure Portal.</span></span> <span data-ttu-id="2dcf8-147">Selecione **todas as configurações** Olá folha da máquina virtual e, em seguida, clique em **extensões**.</span><span class="sxs-lookup"><span data-stu-id="2dcf8-147">Select **All settings** in hello virtual machine blade, and then click on **Extensions**.</span></span> <span data-ttu-id="2dcf8-148">Você deve ver Olá **SQLIaaSExtension** extensão listado.</span><span class="sxs-lookup"><span data-stu-id="2dcf8-148">You should see hello **SQLIaaSExtension** extension listed.</span></span>

![Extensão do Agente IaaS do SQL Server no Portal do Azure](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-portal.png)

<span data-ttu-id="2dcf8-150">Você também pode usar o hello **AzureVMSqlServerExtension Get** cmdlet do Powershell do Azure.</span><span class="sxs-lookup"><span data-stu-id="2dcf8-150">You can also use hello **Get-AzureVMSqlServerExtension** Azure Powershell cmdlet.</span></span>

    Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"

<span data-ttu-id="2dcf8-151">comando anterior Olá confirma agente hello está instalado e fornece informações de status geral.</span><span class="sxs-lookup"><span data-stu-id="2dcf8-151">hello previous command confirms hello agent is installed and provides general status information.</span></span> <span data-ttu-id="2dcf8-152">Você também pode obter informações de status específicas sobre o Backup automatizado e aplicação de patch com hello comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="2dcf8-152">You can also get specific status information about Automated Backup and Patching with hello following commands.</span></span>

    $sqlext = Get-AzureRmVMSqlServerExtension -VMName "vmname" -ResourceGroupName "resourcegroupname"
    $sqlext.AutoPatchingSettings
    $sqlext.AutoBackupSettings

## <a name="removal"></a><span data-ttu-id="2dcf8-153">Remoção</span><span class="sxs-lookup"><span data-stu-id="2dcf8-153">Removal</span></span>
<span data-ttu-id="2dcf8-154">Olá Portal do Azure, você pode desinstalar extensão Olá clicando reticências Olá em Olá **extensões** folha de propriedades de sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2dcf8-154">In hello Azure Portal, you can uninstall hello extension by clicking hello ellipsis on hello **Extensions** blade of your virtual machine properties.</span></span> <span data-ttu-id="2dcf8-155">Em seguida, clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="2dcf8-155">Then click **Delete**.</span></span>

![Desinstalar Olá extensão do agente IaaS do SQL Server no Portal do Azure](./media/virtual-machines-windows-sql-server-agent-extension/azure-rm-sql-server-iaas-agent-uninstall.png)

<span data-ttu-id="2dcf8-157">Você também pode usar o hello **AzureRmVMSqlServerExtension remover** cmdlet do Powershell.</span><span class="sxs-lookup"><span data-stu-id="2dcf8-157">You can also use hello **Remove-AzureRmVMSqlServerExtension** Powershell cmdlet.</span></span>

    Remove-AzureRmVMSqlServerExtension -ResourceGroupName "resourcegroupname" -VMName "vmname" -Name "SQLIaasExtension"

## <a name="next-steps"></a><span data-ttu-id="2dcf8-158">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2dcf8-158">Next Steps</span></span>
<span data-ttu-id="2dcf8-159">Começar a usar um dos serviços de Olá Olá extensão oferece suportados.</span><span class="sxs-lookup"><span data-stu-id="2dcf8-159">Begin using one of hello services supported by hello extension.</span></span> <span data-ttu-id="2dcf8-160">Para obter mais detalhes, consulte os tópicos de saudação referenciados no hello [suporte para serviços](#supported-services) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="2dcf8-160">For more details, see hello topics referenced in hello [Supported services](#supported-services) section of this article.</span></span>

<span data-ttu-id="2dcf8-161">Para obter mais informações sobre como executar o SQL Server em Máquinas Virtuais do Azure, veja [Visão geral do SQL Server em Máquinas Virtuais do Azure](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2dcf8-161">For more information about running SQL Server on Azure Virtual Machines, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

