---
title: "Backup Automatizado para máquinas virtuais do Azure do SQL Server 2014 | Microsoft Docs"
description: "Explica o recurso de Backup Automatizado para VMs do SQL Server 2014 em execução no Azure. Este artigo é específico para VMs que usam o Resource Manager."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: bdc63fd1-db49-4e76-87d5-b5c6a890e53c
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 91aab896dd5f06c950ee0ed8f36cc6a953d91611
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="automated-backup-for-sql-server-2014-virtual-machines-resource-manager"></a><span data-ttu-id="bafe5-104">Backup Automatizado para em máquinas virtuais do SQL Server 2014 (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="bafe5-104">Automated Backup for SQL Server 2014 Virtual Machines (Resource Manager)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="bafe5-105">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="bafe5-105">SQL Server 2014</span></span>](virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="bafe5-106">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="bafe5-106">SQL Server 2016</span></span>](virtual-machines-windows-sql-automated-backup-v2.md)

<span data-ttu-id="bafe5-107">O backup automatizado configura automaticamente o [Backup Gerenciado do Microsoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) para todos os bancos de dados novos e existentes em uma VM do Azure executando o SQL Server 2014 Standard ou Enterprise.</span><span class="sxs-lookup"><span data-stu-id="bafe5-107">Automated Backup automatically configures [Managed Backup to Microsoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> <span data-ttu-id="bafe5-108">Isso permite que você configure backups regulares do banco de dados que utilizam o durável armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="bafe5-108">This enables you to configure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="bafe5-109">O Backup Automatizado depende da [Extensão do agente IaaS do SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="bafe5-109">Automated Backup depends on the [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="bafe5-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="bafe5-110">Prerequisites</span></span>
<span data-ttu-id="bafe5-111">Para usar o Backup Automatizado, considere os seguintes pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="bafe5-111">To use Automated Backup, consider the following prerequisites:</span></span>

<span data-ttu-id="bafe5-112">**Sistema operacional**:</span><span class="sxs-lookup"><span data-stu-id="bafe5-112">**Operating System**:</span></span>

- <span data-ttu-id="bafe5-113">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="bafe5-113">Windows Server 2012</span></span>
- <span data-ttu-id="bafe5-114">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="bafe5-114">Windows Server 2012 R2</span></span>
- <span data-ttu-id="bafe5-115">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="bafe5-115">Windows Server 2016</span></span>

<span data-ttu-id="bafe5-116">**Versão/edição do SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="bafe5-116">**SQL Server version/edition**:</span></span>

- <span data-ttu-id="bafe5-117">SQL Server 2014 Standard</span><span class="sxs-lookup"><span data-stu-id="bafe5-117">SQL Server 2014 Standard</span></span>
- <span data-ttu-id="bafe5-118">SQL Server 2014 Enterprise</span><span class="sxs-lookup"><span data-stu-id="bafe5-118">SQL Server 2014 Enterprise</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bafe5-119">O Backup Automatizado funciona com o SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="bafe5-119">Automated Backup works with SQL Server 2014.</span></span> <span data-ttu-id="bafe5-120">Se você estiver usando o SQL Server 2016, pode usar o Backup Automatizado v2 para fazer backup de seus bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="bafe5-120">If you are using SQL Server 2016, you can use Automated Backup v2 to back up your databases.</span></span> <span data-ttu-id="bafe5-121">Para saber mais, confira [Backup Automatizado v2 para máquinas virtuais do Azure no SQL Server 2016](virtual-machines-windows-sql-automated-backup-v2.md).</span><span class="sxs-lookup"><span data-stu-id="bafe5-121">For more information, see [Automated Backup v2 for SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).</span></span>

<span data-ttu-id="bafe5-122">**Configuração do banco de dados**:</span><span class="sxs-lookup"><span data-stu-id="bafe5-122">**Database configuration**:</span></span>

- <span data-ttu-id="bafe5-123">Os bancos de dados de destino devem usar o modelo de recuperação completa.</span><span class="sxs-lookup"><span data-stu-id="bafe5-123">Target databases must use the full recovery model.</span></span> <span data-ttu-id="bafe5-124">Para obter mais informações sobre o impacto do modelo de recuperação completa em backups, consulte [Backup com o modelo de recuperação completa](https://technet.microsoft.com/library/ms190217.aspx).</span><span class="sxs-lookup"><span data-stu-id="bafe5-124">For more information about the impact of the full recovery model on backups, see [Backup Under the Full Recovery Model](https://technet.microsoft.com/library/ms190217.aspx).</span></span>
- <span data-ttu-id="bafe5-125">Os bancos de dados de destino devem estar na instância padrão do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="bafe5-125">Target databases must be on the default SQL Server instance.</span></span> <span data-ttu-id="bafe5-126">A extensão de IaaS do SQL Server não oferece suporte a instâncias nomeadas.</span><span class="sxs-lookup"><span data-stu-id="bafe5-126">The SQL Server IaaS Extension does not support named instances.</span></span>

<span data-ttu-id="bafe5-127">**Modelo de implantação do Azure**:</span><span class="sxs-lookup"><span data-stu-id="bafe5-127">**Azure deployment model**:</span></span>

- <span data-ttu-id="bafe5-128">Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="bafe5-128">Resource Manager</span></span>

<span data-ttu-id="bafe5-129">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="bafe5-129">**Azure PowerShell**:</span></span>

- <span data-ttu-id="bafe5-130">[Instalar os comandos mais recentes do Azure PowerShell](/powershell/azure/overview) se você planeja configurar o Backup Automatizado com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bafe5-130">[Install the latest Azure PowerShell commands](/powershell/azure/overview) if you plan to configure Automated Backup with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="bafe5-131">O Backup Automatizado conta com a Extensão do agente IaaS do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="bafe5-131">Automated Backup relies on the SQL Server IaaS Agent Extension.</span></span> <span data-ttu-id="bafe5-132">As imagens atuais da galeria da máquina virtual do SQL adicionam essa extensão por padrão.</span><span class="sxs-lookup"><span data-stu-id="bafe5-132">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="bafe5-133">Para obter mais informações, consulte [Extensão do agente IaaS do SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="bafe5-133">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="bafe5-134">Configurações</span><span class="sxs-lookup"><span data-stu-id="bafe5-134">Settings</span></span>

<span data-ttu-id="bafe5-135">A tabela a seguir descreve as opções que podem ser configuradas para Backup Automatizado.</span><span class="sxs-lookup"><span data-stu-id="bafe5-135">The following table describes the options that can be configured for Automated Backup.</span></span> <span data-ttu-id="bafe5-136">As etapas de configuração reais variam dependendo de se você usar os comandos do Portal do Azure ou do Azure Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bafe5-136">The actual configuration steps vary depending on whether you use the Azure portal or Azure Windows PowerShell commands.</span></span>

| <span data-ttu-id="bafe5-137">Configuração</span><span class="sxs-lookup"><span data-stu-id="bafe5-137">Setting</span></span> | <span data-ttu-id="bafe5-138">Intervalo (Padrão)</span><span class="sxs-lookup"><span data-stu-id="bafe5-138">Range (Default)</span></span> | <span data-ttu-id="bafe5-139">Descrição</span><span class="sxs-lookup"><span data-stu-id="bafe5-139">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bafe5-140">**Backup Automatizado**</span><span class="sxs-lookup"><span data-stu-id="bafe5-140">**Automated Backup**</span></span> | <span data-ttu-id="bafe5-141">Habilitar/desabilitar (Desabilitado)</span><span class="sxs-lookup"><span data-stu-id="bafe5-141">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="bafe5-142">Habilita ou desabilita o Backup Automatizado de uma VM do Azure que executa o SQL Server 2014 Standard ou Enterprise.</span><span class="sxs-lookup"><span data-stu-id="bafe5-142">Enables or disables Automated Backup for an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> |
| <span data-ttu-id="bafe5-143">**Período de retenção**</span><span class="sxs-lookup"><span data-stu-id="bafe5-143">**Retention Period**</span></span> | <span data-ttu-id="bafe5-144">Um a 30 dias (30 dias)</span><span class="sxs-lookup"><span data-stu-id="bafe5-144">1-30 days (30 days)</span></span> | <span data-ttu-id="bafe5-145">O número de dias para manter um backup.</span><span class="sxs-lookup"><span data-stu-id="bafe5-145">The number of days to retain a backup.</span></span> |
| <span data-ttu-id="bafe5-146">**Conta de armazenamento**</span><span class="sxs-lookup"><span data-stu-id="bafe5-146">**Storage Account**</span></span> | <span data-ttu-id="bafe5-147">Conta de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="bafe5-147">Azure storage account</span></span> | <span data-ttu-id="bafe5-148">Uma conta de armazenamento do Azure a ser usada para armazenar arquivos de Backup Automatizado no armazenamento de blobs.</span><span class="sxs-lookup"><span data-stu-id="bafe5-148">An Azure storage account to use for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="bafe5-149">Um contêiner é criado neste local para armazenar todos os arquivos de backup.</span><span class="sxs-lookup"><span data-stu-id="bafe5-149">A container is created at this location to store all backup files.</span></span> <span data-ttu-id="bafe5-150">A convenção de nomenclatura do arquivo de backup inclui a data, hora e nome do computador.</span><span class="sxs-lookup"><span data-stu-id="bafe5-150">The backup file naming convention includes the date, time, and machine name.</span></span> |
| <span data-ttu-id="bafe5-151">**Criptografia**</span><span class="sxs-lookup"><span data-stu-id="bafe5-151">**Encryption**</span></span> | <span data-ttu-id="bafe5-152">Habilitar/desabilitar (Desabilitado)</span><span class="sxs-lookup"><span data-stu-id="bafe5-152">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="bafe5-153">Habilita ou desabilita a criptografia.</span><span class="sxs-lookup"><span data-stu-id="bafe5-153">Enables or disables encryption.</span></span> <span data-ttu-id="bafe5-154">Quando a criptografia está habilitada, os certificados usados para restaurar o backup estão localizados na conta de armazenamento especificado no mesmo contêiner `automaticbackup` usando a mesma convenção de nomenclatura.</span><span class="sxs-lookup"><span data-stu-id="bafe5-154">When encryption is enabled, the certificates used to restore the backup are located in the specified storage account in the same `automaticbackup` container using the same naming convention.</span></span> <span data-ttu-id="bafe5-155">Se a senha for alterada, um novo certificado será gerado com essa senha, mas o certificado antigo permanece para restaurar backups anteriores.</span><span class="sxs-lookup"><span data-stu-id="bafe5-155">If the password changes, a new certificate is generated with that password, but the old certificate remains to restore prior backups.</span></span> |
| <span data-ttu-id="bafe5-156">**Senha**</span><span class="sxs-lookup"><span data-stu-id="bafe5-156">**Password**</span></span> | <span data-ttu-id="bafe5-157">Texto da senha</span><span class="sxs-lookup"><span data-stu-id="bafe5-157">Password text</span></span> | <span data-ttu-id="bafe5-158">Uma senha para as chaves de criptografia.</span><span class="sxs-lookup"><span data-stu-id="bafe5-158">A password for encryption keys.</span></span> <span data-ttu-id="bafe5-159">Isso só é necessário se a criptografia estiver habilitada.</span><span class="sxs-lookup"><span data-stu-id="bafe5-159">This is only required if encryption is enabled.</span></span> <span data-ttu-id="bafe5-160">Para restaurar um backup criptografado, você deverá ter a senha correta e o certificado relacionado que foi usado no momento em que o backup foi feito.</span><span class="sxs-lookup"><span data-stu-id="bafe5-160">In order to restore an encrypted backup, you must have the correct password and related certificate that was used at the time the backup was taken.</span></span> |

## <a name="configuration-in-the-portal"></a><span data-ttu-id="bafe5-161">Configuração no Portal</span><span class="sxs-lookup"><span data-stu-id="bafe5-161">Configuration in the Portal</span></span>

<span data-ttu-id="bafe5-162">Você pode usar o Portal do Azure para configurar o Backup Automatizado durante o provisionamento ou para as VMs do SQL Server 2014 existentes.</span><span class="sxs-lookup"><span data-stu-id="bafe5-162">You can use the Azure portal to configure Automated Backup during provisioning or for existing SQL Server 2014 VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="bafe5-163">Novas VMs</span><span class="sxs-lookup"><span data-stu-id="bafe5-163">New VMs</span></span>

<span data-ttu-id="bafe5-164">Use o Portal do Azure para configurar o Backup Automatizado quando criar uma nova Máquina Virtual do SQL Server 2014 no modelo de implantação do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bafe5-164">Use the Azure portal to configure Automated Backup when you create a new SQL Server 2014 Virtual Machine in the Resource Manager deployment model.</span></span>

<span data-ttu-id="bafe5-165">Na folha **Configurações do SQL Server**, selecione **Backup Automatizado**.</span><span class="sxs-lookup"><span data-stu-id="bafe5-165">In the **SQL Server settings** blade, select **Automated backup**.</span></span> <span data-ttu-id="bafe5-166">A captura de tela do portal do Azure a seguir mostra a folha **Backup Automatizado do SQL** .</span><span class="sxs-lookup"><span data-stu-id="bafe5-166">The following Azure portal screenshot shows the **SQL Automated Backup** blade.</span></span>

![Configuração de Backup Automatizado do SQL no portal do Azure](./media/virtual-machines-windows-sql-automated-backup/azure-sql-arm-autobackup.png)

<span data-ttu-id="bafe5-168">Para ter contexto, consulte o tópico completo sobre [provisionamento de uma máquina virtual do SQL Server no Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="bafe5-168">For context, see the complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="bafe5-169">VMs existentes</span><span class="sxs-lookup"><span data-stu-id="bafe5-169">Existing VMs</span></span>

<span data-ttu-id="bafe5-170">Para máquinas virtuais existentes do SQL Server, selecione sua máquina virtual do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="bafe5-170">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="bafe5-171">Selecione a seção **Configuração do SQL Server** da folha **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="bafe5-171">Then select the **SQL Server configuration** section of the **Settings** blade.</span></span>

![Backup Automatizado do SQL para VMs existentes](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-existing-vms.png)

<span data-ttu-id="bafe5-173">Na folha **Configuração do SQL Server**, clique no botão **Editar** na seção de Backup Automatizado.</span><span class="sxs-lookup"><span data-stu-id="bafe5-173">In the **SQL Server configuration** blade, click the **Edit** button in the Automated backup section.</span></span>

![Configurar o Backup Automatizado do SQL para VMs existentes](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-configuration.png)

<span data-ttu-id="bafe5-175">Quando terminar, clique no botão **OK** na parte inferior da folha **Configuração do SQL Server** para salvar suas alterações.</span><span class="sxs-lookup"><span data-stu-id="bafe5-175">When finished, click the **OK** button on the bottom of the **SQL Server configuration** blade to save your changes.</span></span>

<span data-ttu-id="bafe5-176">Se você for habilitar o Backup Automatizado pela primeira vez, o Azure configurará o Agente IaaS do SQL Server em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="bafe5-176">If you are enabling Automated Backup for the first time, Azure configures the SQL Server IaaS Agent in the background.</span></span> <span data-ttu-id="bafe5-177">Durante esse tempo, o portal do Azure pode não mostrar que o Backup Automatizado está configurado.</span><span class="sxs-lookup"><span data-stu-id="bafe5-177">During this time, the Azure portal might not show that Automated Backup is configured.</span></span> <span data-ttu-id="bafe5-178">Aguarde alguns minutos para que o agente seja instalado e configurado.</span><span class="sxs-lookup"><span data-stu-id="bafe5-178">Wait several minutes for the agent to be installed, configured.</span></span> <span data-ttu-id="bafe5-179">Depois disso, o portal do Azure refletirá as novas configurações.</span><span class="sxs-lookup"><span data-stu-id="bafe5-179">After that the Azure portal will reflect the new settings.</span></span>

> [!NOTE]
> <span data-ttu-id="bafe5-180">Você também pode configurar o Backup Automatizado usando um modelo.</span><span class="sxs-lookup"><span data-stu-id="bafe5-180">You can also configure Automated Backup using a template.</span></span> <span data-ttu-id="bafe5-181">Para obter mais informações, consulte o [Modelo de início rápido do Azure para o Backup Automatizado](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update).</span><span class="sxs-lookup"><span data-stu-id="bafe5-181">For more information, see [Azure quickstart template for Automated Backup](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update).</span></span>

## <a name="configuration-with-powershell"></a><span data-ttu-id="bafe5-182">Configuração com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="bafe5-182">Configuration with PowerShell</span></span>

<span data-ttu-id="bafe5-183">Você pode usar o PowerShell para configurar o Backup Automatizado.</span><span class="sxs-lookup"><span data-stu-id="bafe5-183">You can use PowerShell to configure Automated Backup.</span></span> <span data-ttu-id="bafe5-184">Antes de começar, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="bafe5-184">Before you begin, you must:</span></span>

- <span data-ttu-id="bafe5-185">[Baixe e instale o Azure PowerShell mais recente](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="bafe5-185">[Download and install the latest Azure PowerShell](http://aka.ms/webpi-azps).</span></span>
- <span data-ttu-id="bafe5-186">Abra o Windows PowerShell e associe-o à sua conta.</span><span class="sxs-lookup"><span data-stu-id="bafe5-186">Open Windows PowerShell and associate it with your account.</span></span> <span data-ttu-id="bafe5-187">Você pode fazer isso seguindo as etapas na seção [Configurar sua assinatura](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) do tópico de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="bafe5-187">You can do this by following the steps in the [Configure your subscription](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) section of the provisioning topic.</span></span>

### <a name="install-the-sql-iaas-extension"></a><span data-ttu-id="bafe5-188">Instalar a Extensão IaaS do SQL Server</span><span class="sxs-lookup"><span data-stu-id="bafe5-188">Install the SQL IaaS Extension</span></span>
<span data-ttu-id="bafe5-189">Se você tiver provisionado uma máquina virtual do SQL Server no Portal do Azure, a Extensão IaaS do SQL Server já deverá estar instalada.</span><span class="sxs-lookup"><span data-stu-id="bafe5-189">If you provisioned a SQL Server virtual machine from the Azure portal, the SQL Server IaaS Extension should already be installed.</span></span> <span data-ttu-id="bafe5-190">Você pode determinar se ele está instalado para a sua VM chamando o comando **Get-AzureRmVM** e examinando a propriedade **Extensions**.</span><span class="sxs-lookup"><span data-stu-id="bafe5-190">You can determine if it is installed for your VM by calling **Get-AzureRmVM** command and examining the **Extensions** property.</span></span>

```powershell
$vmname = "vmname"
$resourcegroupname = "resourcegroupname"

(Get-AzureRmVM -Name $vmname -ResourceGroupName $resourcegroupname).Extensions
```

<span data-ttu-id="bafe5-191">Se a extensão do agente IaaS do SQL Server estiver instalada, você deverá vê-lo listado como “SqlIaaSAgent” ou “SQLIaaSExtension”.</span><span class="sxs-lookup"><span data-stu-id="bafe5-191">If the SQL Server IaaS Agent extension is installed, you should see it listed as “SqlIaaSAgent” or “SQLIaaSExtension”.</span></span> <span data-ttu-id="bafe5-192">**ProvisioningState** para a extensão também deve mostrar "Êxito".</span><span class="sxs-lookup"><span data-stu-id="bafe5-192">**ProvisioningState** for the extension should also show “Succeeded”.</span></span>

<span data-ttu-id="bafe5-193">Se ele não estiver instalado ou o provisionamento tiver falhado, você poderá instalá-lo com o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="bafe5-193">If it is not installed or failed to be provisioned, you can install it with the following command.</span></span> <span data-ttu-id="bafe5-194">Além do grupo de recursos e do nome da VM, você também deve especificar a região (**$region**) em que a VM está localizada.</span><span class="sxs-lookup"><span data-stu-id="bafe5-194">In addition to the VM name and resource group, you must also specify the region (**$region**) that your VM is located in.</span></span>

```powershell
$region = “EASTUS2”
Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region
```

### <span data-ttu-id="bafe5-195"><a id="verifysettings"></a> Verificar as configurações atuais</span><span class="sxs-lookup"><span data-stu-id="bafe5-195"><a id="verifysettings"></a> Verify current settings</span></span>

<span data-ttu-id="bafe5-196">Se você habilitou o backup automatizado durante o provisionamento, poderá usar o PowerShell para verificar a configuração atual.</span><span class="sxs-lookup"><span data-stu-id="bafe5-196">If you enabled automated backup during provisioning, you can use PowerShell to check your current configuration.</span></span> <span data-ttu-id="bafe5-197">Execute o comando **Get-AzureRmVMSqlServerExtension** e examine a propriedade **AutoBackupSettings**:</span><span class="sxs-lookup"><span data-stu-id="bafe5-197">Run the **Get-AzureRmVMSqlServerExtension** command and examine the **AutoBackupSettings** property:</span></span>

```powershell
(Get-AzureRmVMSqlServerExtension -VMName $vmname -ResourceGroupName $resourcegroupname).AutoBackupSettings
```

<span data-ttu-id="bafe5-198">Você deve ver um resultado semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="bafe5-198">You should get output similar to the following:</span></span>

```
Enable                      : False
EnableEncryption            : False
RetentionPeriod             : -1
StorageUrl                  : NOTSET
StorageAccessKey            : 
Password                    : 
BackupSystemDbs             : False
BackupScheduleType          : 
FullBackupFrequency         : 
FullBackupStartTime         : 
FullBackupWindowHours       : 
LogBackupFrequency          : 
```

<span data-ttu-id="bafe5-199">Se a saída mostrar que **Enable** está definido como **False**, você precisará habilitar o backup automatizado.</span><span class="sxs-lookup"><span data-stu-id="bafe5-199">If your output shows that **Enable** is set to **False**, then you have to enable automated backup.</span></span> <span data-ttu-id="bafe5-200">A boa notícia é que você habilita e configura o Backup Automatizado da mesma maneira.</span><span class="sxs-lookup"><span data-stu-id="bafe5-200">The good news is that you enable and configure Automated Backup in the same way.</span></span> <span data-ttu-id="bafe5-201">Confira a próxima seção para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="bafe5-201">See the next section for this information.</span></span>

> [!NOTE] 
> <span data-ttu-id="bafe5-202">Se você verificar as configurações imediatamente depois de fazer uma alteração, será possível que você obtenha os valores de configuração antigos.</span><span class="sxs-lookup"><span data-stu-id="bafe5-202">If you check the settings immediately after making a change, it is possible that you will get back the old configuration values.</span></span> <span data-ttu-id="bafe5-203">Aguarde alguns minutos e verifique as configurações novamente para se certificar de que as alterações foram aplicadas.</span><span class="sxs-lookup"><span data-stu-id="bafe5-203">Wait a few minutes and check the settings again to make sure that your changes were applied.</span></span>

### <a name="configure-automated-backup"></a><span data-ttu-id="bafe5-204">Configurar o Backup Automatizado</span><span class="sxs-lookup"><span data-stu-id="bafe5-204">Configure Automated Backup</span></span>
<span data-ttu-id="bafe5-205">Você pode usar o PowerShell para habilitar o Backup Automatizado, bem como para modificar sua configuração e comportamento a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="bafe5-205">You can use PowerShell to enable Automated Backup as well as to modify its configuration and behavior at any time.</span></span>

<span data-ttu-id="bafe5-206">Primeiro, selecione ou crie uma conta de armazenamento para os arquivos de backup.</span><span class="sxs-lookup"><span data-stu-id="bafe5-206">First, select or create a storage account for the backup files.</span></span> <span data-ttu-id="bafe5-207">O script a seguir seleciona uma conta de armazenamento ou a cria se ela não existir.</span><span class="sxs-lookup"><span data-stu-id="bafe5-207">The following script selects a storage account or creates it if it does not exist.</span></span>

```powershell
$storage_accountname = “yourstorageaccount”
$storage_resourcegroupname = $resourcegroupname

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }
```

> [!NOTE]
> <span data-ttu-id="bafe5-208">O Backup Automatizado não dá suporte ao armazenamento de backups no Armazenamento Premium, mas ele pode fazer backups de discos de VM que usam o Armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="bafe5-208">Automated Backup does not support storing backups in premium storage, but it can take backups from VM disks which use Premium Storage.</span></span>

<span data-ttu-id="bafe5-209">Em seguida, use o comando **New-AzureRmVMSqlServerAutoBackupConfig** para habilitar e definir as configurações do Backup Automatizado para armazenar backups na conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="bafe5-209">Then use the **New-AzureRmVMSqlServerAutoBackupConfig** command to enable and configure the Automated Backup settings to store backups in the Azure storage account.</span></span> <span data-ttu-id="bafe5-210">Neste exemplo, os backups são definidos para ser mantidos por 10 dias.</span><span class="sxs-lookup"><span data-stu-id="bafe5-210">In this example, the backups are set to be retained for 10 days.</span></span> <span data-ttu-id="bafe5-211">O segundo comando, **Set-AzureRmVMSqlServerExtension**, atualiza a VM do Azure especificada com essas configurações.</span><span class="sxs-lookup"><span data-stu-id="bafe5-211">The second command, **Set-AzureRmVMSqlServerExtension**, updates the specified Azure VM with these settings.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

<span data-ttu-id="bafe5-212">Pode demorar vários minutos para instalar e configurar o Agente IaaS do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="bafe5-212">It could take several minutes to install and configure the SQL Server IaaS Agent.</span></span>

> [!NOTE]
> <span data-ttu-id="bafe5-213">Há outras configurações para **New-AzureRmVMSqlServerAutoBackupConfig** que se aplicam somente ao SQL Server 2016 e ao Backup automatizado v2.</span><span class="sxs-lookup"><span data-stu-id="bafe5-213">There are other settings for **New-AzureRmVMSqlServerAutoBackupConfig** that apply only to SQL Server 2016 and Automated Backup v2.</span></span> <span data-ttu-id="bafe5-214">O SQL Server 2014 não suporta as seguintes configurações: **BackupSystemDbs**, **BackupScheduleType**, **FullBackupFrequency**, **FullBackupStartHour**, **FullBackupWindowInHours** e **LogBackupFrequencyInMinutes**.</span><span class="sxs-lookup"><span data-stu-id="bafe5-214">SQL Server 2014 does not support the following settings: **BackupSystemDbs**, **BackupScheduleType**, **FullBackupFrequency**, **FullBackupStartHour**, **FullBackupWindowInHours**, and **LogBackupFrequencyInMinutes**.</span></span> <span data-ttu-id="bafe5-215">Se você tentar definir essas configurações em uma máquina virtual do SQL Server 2014, não haverá erro, mas as configurações não serão aplicadas.</span><span class="sxs-lookup"><span data-stu-id="bafe5-215">If you attempt to configure these settings on a SQL Server 2014 virtual machine, there is no error, but the settings do not get applied.</span></span> <span data-ttu-id="bafe5-216">Se você quiser usar essas configurações em uma máquina virtual do SQL Server 2016, veja [Backup automatizado v2 para máquinas virtuais do Azure no SQL Server 2016](virtual-machines-windows-sql-automated-backup-v2.md).</span><span class="sxs-lookup"><span data-stu-id="bafe5-216">If you want to use these settings on a SQL Server 2016 virtual machine, see [Automated Backup v2 for SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).</span></span>

<span data-ttu-id="bafe5-217">Para habilitar a criptografia, modifique o script anterior para passar o parâmetro **EnableEncryption** e uma senha (cadeia de caracteres segura) para o parâmetro **CertificatePassword**.</span><span class="sxs-lookup"><span data-stu-id="bafe5-217">To enable encryption, modify the previous script to pass the **EnableEncryption** parameter along with a password (secure string) for the **CertificatePassword** parameter.</span></span> <span data-ttu-id="bafe5-218">O script a seguir habilita as configurações de Backup Automatizado no exemplo anterior e adiciona a criptografia.</span><span class="sxs-lookup"><span data-stu-id="bafe5-218">The following script enables the Automated Backup settings in the previous example and adds encryption.</span></span>

```powershell
$password = "P@ssw0rd"
$encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -EnableEncryption -CertificatePassword $encryptionpassword `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

<span data-ttu-id="bafe5-219">Para confirmar que as configurações estão aplicadas, [verifique a configuração do Backup Automatizado](#verifysettings).</span><span class="sxs-lookup"><span data-stu-id="bafe5-219">To confirm your settings are applied, [verify the Automated Backup configuration](#verifysettings).</span></span>

### <a name="disable-automated-backup"></a><span data-ttu-id="bafe5-220">Desabilitar o Backup automatizado</span><span class="sxs-lookup"><span data-stu-id="bafe5-220">Disable Automated Backup</span></span>

<span data-ttu-id="bafe5-221">Para desabilitar o Backup Automatizado, execute o mesmo script sem o parâmetro **-Enable** para o comando **New-AzureRmVMSqlServerAutoBackupConfig**.</span><span class="sxs-lookup"><span data-stu-id="bafe5-221">To disable Automated Backup, run the same script without the **-Enable** parameter to the **New-AzureRmVMSqlServerAutoBackupConfig** command.</span></span> <span data-ttu-id="bafe5-222">A ausência do parâmetro **-Enable** sinaliza o comando para desabilitar o recurso.</span><span class="sxs-lookup"><span data-stu-id="bafe5-222">The absence of the **-Enable** parameter signals the command to disable the feature.</span></span> <span data-ttu-id="bafe5-223">Assim como acontece com a instalação, pode demorar vários minutos para desabilitar o Backup Automatizado.</span><span class="sxs-lookup"><span data-stu-id="bafe5-223">As with installation, it can take several minutes to disable Automated Backup.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

### <a name="example-script"></a><span data-ttu-id="bafe5-224">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="bafe5-224">Example script</span></span>

<span data-ttu-id="bafe5-225">O script a seguir fornece um conjunto de variáveis que você pode personalizar para habilitar e configurar o Backup Automatizado para sua VM.</span><span class="sxs-lookup"><span data-stu-id="bafe5-225">The following script provides a set of variables that you can customize to enable and configure Automated Backup for your VM.</span></span> <span data-ttu-id="bafe5-226">No seu caso, convém personalizar o script de acordo com seus requisitos.</span><span class="sxs-lookup"><span data-stu-id="bafe5-226">In your case, you might need to customize the script based on your requirements.</span></span> <span data-ttu-id="bafe5-227">Por exemplo, você teria que fazer alterações desejasse desabilitar o backup de bancos de dados do sistema ou habilitar a criptografia.</span><span class="sxs-lookup"><span data-stu-id="bafe5-227">For example, you would have to make changes if you wanted to disable the backup of system databases or enable encryption.</span></span>

```powershell
$vmname = "yourvmname"
$resourcegroupname = "vmresourcegroupname"
$region = “Azure region name such as EASTUS2”
$storage_accountname = “storageaccountname”
$storage_resourcegroupname = $resourcegroupname
$retentionperiod = 10

# ResourceGroupName is the resource group which is hosting the VM where you are deploying the SQL IaaS Extension

Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region

# Creates/use a storage account to store the backups

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }

# Configure Automated Backup settings

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays $retentionperiod -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

# Apply the Automated Backup settings to the VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="bafe5-228">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bafe5-228">Next steps</span></span>

<span data-ttu-id="bafe5-229">O Backup Automatizado configura o Backup Gerenciado em VMs do Azure.</span><span class="sxs-lookup"><span data-stu-id="bafe5-229">Automated Backup configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="bafe5-230">Portanto, é importante [ler a documentação do Backup Gerenciado](https://msdn.microsoft.com/library/dn449496.aspx) para entender o comportamento e suas implicações.</span><span class="sxs-lookup"><span data-stu-id="bafe5-230">So it is important to [review the documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) to understand the behavior and implications.</span></span>

<span data-ttu-id="bafe5-231">Você pode encontrar outras orientações de backup e de restauração para o SQL Server em VMs do Azure no seguinte tópico: [Backup e restauração do SQL Server em Máquinas Virtuais do Azure](virtual-machines-windows-sql-backup-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="bafe5-231">You can find additional backup and restore guidance for SQL Server on Azure VMs in the following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span></span>

<span data-ttu-id="bafe5-232">Para obter informações sobre outras tarefas de automação disponíveis, consulte [Extensão do agente IaaS do SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="bafe5-232">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="bafe5-233">Para obter mais informações sobre como executar o SQL Server em VMs do Azure, consulte [Visão geral do SQL Server em Máquinas Virtuais do Azure](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bafe5-233">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

