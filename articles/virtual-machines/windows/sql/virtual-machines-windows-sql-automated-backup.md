---
title: "aaaAutomated Backup para máquinas de virtuais do SQL Server 2014 do Azure | Microsoft Docs"
description: "Explica o recurso de Backup automatizado Olá para VMs do SQL Server 2014 em execução no Azure. Este artigo é específico tooVMs usando Olá Gerenciador de recursos."
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
ms.openlocfilehash: c6803d8ef9f80e44a2f87918d87e099f1b562483
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-for-sql-server-2014-virtual-machines-resource-manager"></a><span data-ttu-id="026fc-104">Backup Automatizado para em máquinas virtuais do SQL Server 2014 (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="026fc-104">Automated Backup for SQL Server 2014 Virtual Machines (Resource Manager)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="026fc-105">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="026fc-105">SQL Server 2014</span></span>](virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="026fc-106">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="026fc-106">SQL Server 2016</span></span>](virtual-machines-windows-sql-automated-backup-v2.md)

<span data-ttu-id="026fc-107">Backup automatizado configura automaticamente [tooMicrosoft de Backup gerenciado do Azure](https://msdn.microsoft.com/library/dn449496.aspx) para todos os novos e existentes bancos de dados em uma VM do Azure executando o SQL Server 2014 Standard ou Enterprise.</span><span class="sxs-lookup"><span data-stu-id="026fc-107">Automated Backup automatically configures [Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> <span data-ttu-id="026fc-108">Isso permite que os backups de banco de dados regular tooconfigure que utilizam o armazenamento de BLOBs do Azure durável.</span><span class="sxs-lookup"><span data-stu-id="026fc-108">This enables you tooconfigure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="026fc-109">Backup automatizado depende Olá [extensão do SQL Server IaaS Agent](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="026fc-109">Automated Backup depends on hello [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="026fc-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="026fc-110">Prerequisites</span></span>
<span data-ttu-id="026fc-111">toouse Backup automatizado, considere Olá pré-requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="026fc-111">toouse Automated Backup, consider hello following prerequisites:</span></span>

<span data-ttu-id="026fc-112">**Sistema operacional**:</span><span class="sxs-lookup"><span data-stu-id="026fc-112">**Operating System**:</span></span>

- <span data-ttu-id="026fc-113">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="026fc-113">Windows Server 2012</span></span>
- <span data-ttu-id="026fc-114">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="026fc-114">Windows Server 2012 R2</span></span>
- <span data-ttu-id="026fc-115">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="026fc-115">Windows Server 2016</span></span>

<span data-ttu-id="026fc-116">**Versão/edição do SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="026fc-116">**SQL Server version/edition**:</span></span>

- <span data-ttu-id="026fc-117">SQL Server 2014 Standard</span><span class="sxs-lookup"><span data-stu-id="026fc-117">SQL Server 2014 Standard</span></span>
- <span data-ttu-id="026fc-118">SQL Server 2014 Enterprise</span><span class="sxs-lookup"><span data-stu-id="026fc-118">SQL Server 2014 Enterprise</span></span>

> [!IMPORTANT]
> <span data-ttu-id="026fc-119">O Backup Automatizado funciona com o SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="026fc-119">Automated Backup works with SQL Server 2014.</span></span> <span data-ttu-id="026fc-120">Se você estiver usando o SQL Server 2016, você pode usar o Backup automatizado v2 tooback backup de seus bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="026fc-120">If you are using SQL Server 2016, you can use Automated Backup v2 tooback up your databases.</span></span> <span data-ttu-id="026fc-121">Para saber mais, confira [Backup Automatizado v2 para máquinas virtuais do Azure no SQL Server 2016](virtual-machines-windows-sql-automated-backup-v2.md).</span><span class="sxs-lookup"><span data-stu-id="026fc-121">For more information, see [Automated Backup v2 for SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).</span></span>

<span data-ttu-id="026fc-122">**Configuração do banco de dados**:</span><span class="sxs-lookup"><span data-stu-id="026fc-122">**Database configuration**:</span></span>

- <span data-ttu-id="026fc-123">Bancos de dados de destino devem usar o modelo de recuperação completa de saudação.</span><span class="sxs-lookup"><span data-stu-id="026fc-123">Target databases must use hello full recovery model.</span></span> <span data-ttu-id="026fc-124">Para obter mais informações sobre o impacto de saudação do modelo de recuperação completa de saudação em backups, consulte [Olá Backup no modelo de recuperação completa](https://technet.microsoft.com/library/ms190217.aspx).</span><span class="sxs-lookup"><span data-stu-id="026fc-124">For more information about hello impact of hello full recovery model on backups, see [Backup Under hello Full Recovery Model](https://technet.microsoft.com/library/ms190217.aspx).</span></span>
- <span data-ttu-id="026fc-125">Bancos de dados de destino devem estar na instância do SQL Server padrão hello.</span><span class="sxs-lookup"><span data-stu-id="026fc-125">Target databases must be on hello default SQL Server instance.</span></span> <span data-ttu-id="026fc-126">Olá extensão de IaaS do SQL Server não oferece suporte a instâncias nomeadas.</span><span class="sxs-lookup"><span data-stu-id="026fc-126">hello SQL Server IaaS Extension does not support named instances.</span></span>

<span data-ttu-id="026fc-127">**Modelo de implantação do Azure**:</span><span class="sxs-lookup"><span data-stu-id="026fc-127">**Azure deployment model**:</span></span>

- <span data-ttu-id="026fc-128">Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="026fc-128">Resource Manager</span></span>

<span data-ttu-id="026fc-129">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="026fc-129">**Azure PowerShell**:</span></span>

- <span data-ttu-id="026fc-130">[Olá mais recente do Azure PowerShell comandos de instalação](/powershell/azure/overview) se você planejar tooconfigure Backup automatizado com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="026fc-130">[Install hello latest Azure PowerShell commands](/powershell/azure/overview) if you plan tooconfigure Automated Backup with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="026fc-131">Backup automatizado depende Olá extensão do SQL Server IaaS Agent.</span><span class="sxs-lookup"><span data-stu-id="026fc-131">Automated Backup relies on hello SQL Server IaaS Agent Extension.</span></span> <span data-ttu-id="026fc-132">As imagens atuais da galeria da máquina virtual do SQL adicionam essa extensão por padrão.</span><span class="sxs-lookup"><span data-stu-id="026fc-132">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="026fc-133">Para obter mais informações, consulte [Extensão do agente IaaS do SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="026fc-133">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="026fc-134">Configurações</span><span class="sxs-lookup"><span data-stu-id="026fc-134">Settings</span></span>

<span data-ttu-id="026fc-135">Olá, tabela a seguir descreve as opções de saudação que podem ser configuradas para Backup automatizado.</span><span class="sxs-lookup"><span data-stu-id="026fc-135">hello following table describes hello options that can be configured for Automated Backup.</span></span> <span data-ttu-id="026fc-136">etapas de configuração real de saudação variam dependendo se você usar Olá portal do Azure ou comandos do PowerShell do Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="026fc-136">hello actual configuration steps vary depending on whether you use hello Azure portal or Azure Windows PowerShell commands.</span></span>

| <span data-ttu-id="026fc-137">Configuração</span><span class="sxs-lookup"><span data-stu-id="026fc-137">Setting</span></span> | <span data-ttu-id="026fc-138">Intervalo (Padrão)</span><span class="sxs-lookup"><span data-stu-id="026fc-138">Range (Default)</span></span> | <span data-ttu-id="026fc-139">Descrição</span><span class="sxs-lookup"><span data-stu-id="026fc-139">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="026fc-140">**Backup Automatizado**</span><span class="sxs-lookup"><span data-stu-id="026fc-140">**Automated Backup**</span></span> | <span data-ttu-id="026fc-141">Habilitar/desabilitar (Desabilitado)</span><span class="sxs-lookup"><span data-stu-id="026fc-141">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="026fc-142">Habilita ou desabilita o Backup Automatizado de uma VM do Azure que executa o SQL Server 2014 Standard ou Enterprise.</span><span class="sxs-lookup"><span data-stu-id="026fc-142">Enables or disables Automated Backup for an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> |
| <span data-ttu-id="026fc-143">**Período de retenção**</span><span class="sxs-lookup"><span data-stu-id="026fc-143">**Retention Period**</span></span> | <span data-ttu-id="026fc-144">Um a 30 dias (30 dias)</span><span class="sxs-lookup"><span data-stu-id="026fc-144">1-30 days (30 days)</span></span> | <span data-ttu-id="026fc-145">número de saudação de dias tooretain um backup.</span><span class="sxs-lookup"><span data-stu-id="026fc-145">hello number of days tooretain a backup.</span></span> |
| <span data-ttu-id="026fc-146">**Conta de armazenamento**</span><span class="sxs-lookup"><span data-stu-id="026fc-146">**Storage Account**</span></span> | <span data-ttu-id="026fc-147">Conta de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="026fc-147">Azure storage account</span></span> | <span data-ttu-id="026fc-148">Um toouse de conta de armazenamento do Azure para armazenar arquivos de Backup automatizado no armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="026fc-148">An Azure storage account toouse for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="026fc-149">Um contêiner é criado neste local toostore todos os arquivos de backup.</span><span class="sxs-lookup"><span data-stu-id="026fc-149">A container is created at this location toostore all backup files.</span></span> <span data-ttu-id="026fc-150">o arquivo de backup Olá convenção de nomenclatura inclui Olá data, hora e nome do computador.</span><span class="sxs-lookup"><span data-stu-id="026fc-150">hello backup file naming convention includes hello date, time, and machine name.</span></span> |
| <span data-ttu-id="026fc-151">**Criptografia**</span><span class="sxs-lookup"><span data-stu-id="026fc-151">**Encryption**</span></span> | <span data-ttu-id="026fc-152">Habilitar/desabilitar (Desabilitado)</span><span class="sxs-lookup"><span data-stu-id="026fc-152">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="026fc-153">Habilita ou desabilita a criptografia.</span><span class="sxs-lookup"><span data-stu-id="026fc-153">Enables or disables encryption.</span></span> <span data-ttu-id="026fc-154">Quando a criptografia está habilitada, Olá certificados usados toorestore Olá backup estão localizados em Olá especificado conta de armazenamento em Olá mesmo `automaticbackup` Olá contêiner usando a mesma convenção de nomenclatura.</span><span class="sxs-lookup"><span data-stu-id="026fc-154">When encryption is enabled, hello certificates used toorestore hello backup are located in hello specified storage account in hello same `automaticbackup` container using hello same naming convention.</span></span> <span data-ttu-id="026fc-155">Se Olá senha for alterada, um novo certificado será gerado com essa senha, mas o certificado antigo Olá permanece backups anteriores toorestore.</span><span class="sxs-lookup"><span data-stu-id="026fc-155">If hello password changes, a new certificate is generated with that password, but hello old certificate remains toorestore prior backups.</span></span> |
| <span data-ttu-id="026fc-156">**Senha**</span><span class="sxs-lookup"><span data-stu-id="026fc-156">**Password**</span></span> | <span data-ttu-id="026fc-157">Texto da senha</span><span class="sxs-lookup"><span data-stu-id="026fc-157">Password text</span></span> | <span data-ttu-id="026fc-158">Uma senha para as chaves de criptografia.</span><span class="sxs-lookup"><span data-stu-id="026fc-158">A password for encryption keys.</span></span> <span data-ttu-id="026fc-159">Isso só é necessário se a criptografia estiver habilitada.</span><span class="sxs-lookup"><span data-stu-id="026fc-159">This is only required if encryption is enabled.</span></span> <span data-ttu-id="026fc-160">Ordem toorestore um backup criptografado, você deve ter senha correta hello e o certificado relacionado que foi usado em tempo de Olá Olá backup foi feito.</span><span class="sxs-lookup"><span data-stu-id="026fc-160">In order toorestore an encrypted backup, you must have hello correct password and related certificate that was used at hello time hello backup was taken.</span></span> |

## <a name="configuration-in-hello-portal"></a><span data-ttu-id="026fc-161">Configuração no Portal de saudação</span><span class="sxs-lookup"><span data-stu-id="026fc-161">Configuration in hello Portal</span></span>

<span data-ttu-id="026fc-162">Você pode usar o hello tooconfigure portal do Azure Backup automatizado durante o provisionamento ou para VMs existentes do SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="026fc-162">You can use hello Azure portal tooconfigure Automated Backup during provisioning or for existing SQL Server 2014 VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="026fc-163">Novas VMs</span><span class="sxs-lookup"><span data-stu-id="026fc-163">New VMs</span></span>

<span data-ttu-id="026fc-164">Use Olá tooconfigure portal do Azure Backup automatizado quando você cria uma nova máquina SQL Server 2014 Virtual no modelo de implantação do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="026fc-164">Use hello Azure portal tooconfigure Automated Backup when you create a new SQL Server 2014 Virtual Machine in hello Resource Manager deployment model.</span></span>

<span data-ttu-id="026fc-165">Em Olá **configurações do SQL Server** folha, selecione **backup automatizado**.</span><span class="sxs-lookup"><span data-stu-id="026fc-165">In hello **SQL Server settings** blade, select **Automated backup**.</span></span> <span data-ttu-id="026fc-166">Olá, seguinte captura de tela de portal do Azure mostra Olá **Backup automatizado do SQL** folha.</span><span class="sxs-lookup"><span data-stu-id="026fc-166">hello following Azure portal screenshot shows hello **SQL Automated Backup** blade.</span></span>

![Configuração de Backup Automatizado do SQL no portal do Azure](./media/virtual-machines-windows-sql-automated-backup/azure-sql-arm-autobackup.png)

<span data-ttu-id="026fc-168">Para o contexto, consulte o tópico completo do hello sobre [Provisionando uma máquina virtual do SQL Server no Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="026fc-168">For context, see hello complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="026fc-169">VMs existentes</span><span class="sxs-lookup"><span data-stu-id="026fc-169">Existing VMs</span></span>

<span data-ttu-id="026fc-170">Para máquinas virtuais existentes do SQL Server, selecione sua máquina virtual do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="026fc-170">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="026fc-171">Em seguida, selecione Olá **configuração do SQL Server** seção Olá **configurações** folha.</span><span class="sxs-lookup"><span data-stu-id="026fc-171">Then select hello **SQL Server configuration** section of hello **Settings** blade.</span></span>

![Backup Automatizado do SQL para VMs existentes](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-existing-vms.png)

<span data-ttu-id="026fc-173">Em hello **configuração do SQL Server** folha, clique em hello **editar** botão Olá automatizada seção de backup.</span><span class="sxs-lookup"><span data-stu-id="026fc-173">In hello **SQL Server configuration** blade, click hello **Edit** button in hello Automated backup section.</span></span>

![Configurar o Backup Automatizado do SQL para VMs existentes](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-configuration.png)

<span data-ttu-id="026fc-175">Quando terminar, clique em Olá **Okey** botão na parte inferior de saudação da saudação **configuração do SQL Server** folha toosave suas alterações.</span><span class="sxs-lookup"><span data-stu-id="026fc-175">When finished, click hello **OK** button on hello bottom of hello **SQL Server configuration** blade toosave your changes.</span></span>

<span data-ttu-id="026fc-176">Se você estiver habilitando o Backup automatizado para Olá primeira vez, o Azure configura Olá IaaS do SQL Server Agent no plano de fundo de saudação.</span><span class="sxs-lookup"><span data-stu-id="026fc-176">If you are enabling Automated Backup for hello first time, Azure configures hello SQL Server IaaS Agent in hello background.</span></span> <span data-ttu-id="026fc-177">Durante esse tempo, Olá portal do Azure não pode mostrar que o Backup automatizado é configurado.</span><span class="sxs-lookup"><span data-stu-id="026fc-177">During this time, hello Azure portal might not show that Automated Backup is configured.</span></span> <span data-ttu-id="026fc-178">Aguarde alguns minutos para Olá agente toobe instalado, configurado.</span><span class="sxs-lookup"><span data-stu-id="026fc-178">Wait several minutes for hello agent toobe installed, configured.</span></span> <span data-ttu-id="026fc-179">Depois que hello Azure portal refletirá novas configurações de saudação.</span><span class="sxs-lookup"><span data-stu-id="026fc-179">After that hello Azure portal will reflect hello new settings.</span></span>

> [!NOTE]
> <span data-ttu-id="026fc-180">Você também pode configurar o Backup Automatizado usando um modelo.</span><span class="sxs-lookup"><span data-stu-id="026fc-180">You can also configure Automated Backup using a template.</span></span> <span data-ttu-id="026fc-181">Para obter mais informações, consulte o [Modelo de início rápido do Azure para o Backup Automatizado](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update).</span><span class="sxs-lookup"><span data-stu-id="026fc-181">For more information, see [Azure quickstart template for Automated Backup](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update).</span></span>

## <a name="configuration-with-powershell"></a><span data-ttu-id="026fc-182">Configuração com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="026fc-182">Configuration with PowerShell</span></span>

<span data-ttu-id="026fc-183">Você pode usar o PowerShell tooconfigure Backup automatizado.</span><span class="sxs-lookup"><span data-stu-id="026fc-183">You can use PowerShell tooconfigure Automated Backup.</span></span> <span data-ttu-id="026fc-184">Antes de começar, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="026fc-184">Before you begin, you must:</span></span>

- <span data-ttu-id="026fc-185">[Baixe e instale o hello Azure PowerShell mais recente](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="026fc-185">[Download and install hello latest Azure PowerShell](http://aka.ms/webpi-azps).</span></span>
- <span data-ttu-id="026fc-186">Abra o Windows PowerShell e associe-o à sua conta.</span><span class="sxs-lookup"><span data-stu-id="026fc-186">Open Windows PowerShell and associate it with your account.</span></span> <span data-ttu-id="026fc-187">Você pode fazer isso, seguindo as etapas de Olá Olá [configurar sua assinatura](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) seção Olá provisionamento tópico.</span><span class="sxs-lookup"><span data-stu-id="026fc-187">You can do this by following hello steps in hello [Configure your subscription](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) section of hello provisioning topic.</span></span>

### <a name="install-hello-sql-iaas-extension"></a><span data-ttu-id="026fc-188">Instalar Olá extensão SQL IaaS</span><span class="sxs-lookup"><span data-stu-id="026fc-188">Install hello SQL IaaS Extension</span></span>
<span data-ttu-id="026fc-189">Se você provisionar uma máquina de virtual do SQL Server do hello portal do Azure, Olá extensão de IaaS do SQL Server já deve ser instalado.</span><span class="sxs-lookup"><span data-stu-id="026fc-189">If you provisioned a SQL Server virtual machine from hello Azure portal, hello SQL Server IaaS Extension should already be installed.</span></span> <span data-ttu-id="026fc-190">Você pode determinar se ele é instalado em sua VM chamando **Get-AzureRmVM** comando e examinando Olá **extensões** propriedade.</span><span class="sxs-lookup"><span data-stu-id="026fc-190">You can determine if it is installed for your VM by calling **Get-AzureRmVM** command and examining hello **Extensions** property.</span></span>

```powershell
$vmname = "vmname"
$resourcegroupname = "resourcegroupname"

(Get-AzureRmVM -Name $vmname -ResourceGroupName $resourcegroupname).Extensions
```

<span data-ttu-id="026fc-191">Se Olá extensão do SQL Server IaaS Agent estiver instalado, você verá que ele listado como "SqlIaaSAgent" ou "SQLIaaSExtension".</span><span class="sxs-lookup"><span data-stu-id="026fc-191">If hello SQL Server IaaS Agent extension is installed, you should see it listed as “SqlIaaSAgent” or “SQLIaaSExtension”.</span></span> <span data-ttu-id="026fc-192">**ProvisioningState** para extensão Olá também deve mostrar "Êxito".</span><span class="sxs-lookup"><span data-stu-id="026fc-192">**ProvisioningState** for hello extension should also show “Succeeded”.</span></span>

<span data-ttu-id="026fc-193">Se ele não está instalado ou com falha toobe provisionado, você pode instalá-lo com hello comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="026fc-193">If it is not installed or failed toobe provisioned, you can install it with hello following command.</span></span> <span data-ttu-id="026fc-194">Adição toohello VM nome e grupo de recursos, você deve também especificar região hello (**$region**) localizado na sua VM.</span><span class="sxs-lookup"><span data-stu-id="026fc-194">In addition toohello VM name and resource group, you must also specify hello region (**$region**) that your VM is located in.</span></span>

```powershell
$region = “EASTUS2”
Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region
```

### <span data-ttu-id="026fc-195"><a id="verifysettings"></a> Verificar as configurações atuais</span><span class="sxs-lookup"><span data-stu-id="026fc-195"><a id="verifysettings"></a> Verify current settings</span></span>

<span data-ttu-id="026fc-196">Se você habilitou o backup automatizado durante o provisionamento, você pode usar PowerShell toocheck sua configuração atual.</span><span class="sxs-lookup"><span data-stu-id="026fc-196">If you enabled automated backup during provisioning, you can use PowerShell toocheck your current configuration.</span></span> <span data-ttu-id="026fc-197">Executar Olá **Get-AzureRmVMSqlServerExtension** de comando e examine Olá **AutoBackupSettings** propriedade:</span><span class="sxs-lookup"><span data-stu-id="026fc-197">Run hello **Get-AzureRmVMSqlServerExtension** command and examine hello **AutoBackupSettings** property:</span></span>

```powershell
(Get-AzureRmVMSqlServerExtension -VMName $vmname -ResourceGroupName $resourcegroupname).AutoBackupSettings
```

<span data-ttu-id="026fc-198">Você deve obter a seguir toohello semelhante saída:</span><span class="sxs-lookup"><span data-stu-id="026fc-198">You should get output similar toohello following:</span></span>

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

<span data-ttu-id="026fc-199">Se a saída mostra que **habilitar** está definido muito**False**, em seguida, você tem o backup automatizado tooenable.</span><span class="sxs-lookup"><span data-stu-id="026fc-199">If your output shows that **Enable** is set too**False**, then you have tooenable automated backup.</span></span> <span data-ttu-id="026fc-200">Olá boa notícia é que você habilita e configurar o Backup automatizado no hello mesma maneira.</span><span class="sxs-lookup"><span data-stu-id="026fc-200">hello good news is that you enable and configure Automated Backup in hello same way.</span></span> <span data-ttu-id="026fc-201">Consulte a próxima seção Olá para obter essas informações.</span><span class="sxs-lookup"><span data-stu-id="026fc-201">See hello next section for this information.</span></span>

> [!NOTE] 
> <span data-ttu-id="026fc-202">Se você verificar as configurações de saudação imediatamente depois de fazer uma alteração, é possível que você receberá novamente os valores de configuração antigo hello.</span><span class="sxs-lookup"><span data-stu-id="026fc-202">If you check hello settings immediately after making a change, it is possible that you will get back hello old configuration values.</span></span> <span data-ttu-id="026fc-203">Aguarde alguns minutos e verificar as configurações de saudação novamente toomake-se de que as alterações foram aplicadas.</span><span class="sxs-lookup"><span data-stu-id="026fc-203">Wait a few minutes and check hello settings again toomake sure that your changes were applied.</span></span>

### <a name="configure-automated-backup"></a><span data-ttu-id="026fc-204">Configurar o Backup Automatizado</span><span class="sxs-lookup"><span data-stu-id="026fc-204">Configure Automated Backup</span></span>
<span data-ttu-id="026fc-205">Você pode usar PowerShell tooenable Backup automatizado, bem como toomodify sua configuração e o comportamento a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="026fc-205">You can use PowerShell tooenable Automated Backup as well as toomodify its configuration and behavior at any time.</span></span>

<span data-ttu-id="026fc-206">Primeiro, selecione ou crie uma conta de armazenamento para Olá arquivos de backup.</span><span class="sxs-lookup"><span data-stu-id="026fc-206">First, select or create a storage account for hello backup files.</span></span> <span data-ttu-id="026fc-207">Olá script a seguir seleciona uma conta de armazenamento ou cria se ele não existe.</span><span class="sxs-lookup"><span data-stu-id="026fc-207">hello following script selects a storage account or creates it if it does not exist.</span></span>

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
> <span data-ttu-id="026fc-208">O Backup Automatizado não dá suporte ao armazenamento de backups no Armazenamento Premium, mas ele pode fazer backups de discos de VM que usam o Armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="026fc-208">Automated Backup does not support storing backups in premium storage, but it can take backups from VM disks which use Premium Storage.</span></span>

<span data-ttu-id="026fc-209">Em seguida, usar Olá **New-AzureRmVMSqlServerAutoBackupConfig** tooenable de comando e configurar backups de toostore de configurações de Backup automatizado de saudação em Olá conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="026fc-209">Then use hello **New-AzureRmVMSqlServerAutoBackupConfig** command tooenable and configure hello Automated Backup settings toostore backups in hello Azure storage account.</span></span> <span data-ttu-id="026fc-210">Neste exemplo, os backups de saudação são definidos toobe mantido por 10 dias.</span><span class="sxs-lookup"><span data-stu-id="026fc-210">In this example, hello backups are set toobe retained for 10 days.</span></span> <span data-ttu-id="026fc-211">Olá o segundo comando, **AzureRmVMSqlServerExtension conjunto**, Olá atualizações especificado VM do Azure com essas configurações.</span><span class="sxs-lookup"><span data-stu-id="026fc-211">hello second command, **Set-AzureRmVMSqlServerExtension**, updates hello specified Azure VM with these settings.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

<span data-ttu-id="026fc-212">Ele pode levar vários tooinstall de minutos e configure Olá SQL Server IaaS Agent.</span><span class="sxs-lookup"><span data-stu-id="026fc-212">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span>

> [!NOTE]
> <span data-ttu-id="026fc-213">Existem outras configurações para **AzureRmVMSqlServerAutoBackupConfig novo** que se aplicam somente tooSQL Server 2016 e Backup automatizado v2.</span><span class="sxs-lookup"><span data-stu-id="026fc-213">There are other settings for **New-AzureRmVMSqlServerAutoBackupConfig** that apply only tooSQL Server 2016 and Automated Backup v2.</span></span> <span data-ttu-id="026fc-214">SQL Server 2014 não oferece suporte a saudação configurações a seguir: **BackupSystemDbs**, **BackupScheduleType**, **FullBackupFrequency**,  **FullBackupStartHour**, **FullBackupWindowInHours**, e **LogBackupFrequencyInMinutes**.</span><span class="sxs-lookup"><span data-stu-id="026fc-214">SQL Server 2014 does not support hello following settings: **BackupSystemDbs**, **BackupScheduleType**, **FullBackupFrequency**, **FullBackupStartHour**, **FullBackupWindowInHours**, and **LogBackupFrequencyInMinutes**.</span></span> <span data-ttu-id="026fc-215">Se você tentar tooconfigure essas configurações em uma máquina de virtual do SQL Server 2014, nenhum erro, mas as configurações de saudação não serão aplicadas.</span><span class="sxs-lookup"><span data-stu-id="026fc-215">If you attempt tooconfigure these settings on a SQL Server 2014 virtual machine, there is no error, but hello settings do not get applied.</span></span> <span data-ttu-id="026fc-216">Se você quiser que essas configurações em uma máquina de virtual do SQL Server 2016 toouse, consulte [v2 de Backup automatizado para máquinas de virtuais do SQL Server 2016 Azure](virtual-machines-windows-sql-automated-backup-v2.md).</span><span class="sxs-lookup"><span data-stu-id="026fc-216">If you want toouse these settings on a SQL Server 2016 virtual machine, see [Automated Backup v2 for SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).</span></span>

<span data-ttu-id="026fc-217">criptografia de tooenable modificar Olá Olá de toopass script anterior **EnableEncryption** parâmetro junto com uma senha (cadeia de caracteres segura) para Olá **CertificatePassword** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="026fc-217">tooenable encryption, modify hello previous script toopass hello **EnableEncryption** parameter along with a password (secure string) for hello **CertificatePassword** parameter.</span></span> <span data-ttu-id="026fc-218">Olá script a seguir permite que as configurações de Backup automatizado Olá no exemplo anterior hello e adiciona a criptografia.</span><span class="sxs-lookup"><span data-stu-id="026fc-218">hello following script enables hello Automated Backup settings in hello previous example and adds encryption.</span></span>

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

<span data-ttu-id="026fc-219">tooconfirm suas configurações são aplicadas, [verificar a configuração de Backup automatizado Olá](#verifysettings).</span><span class="sxs-lookup"><span data-stu-id="026fc-219">tooconfirm your settings are applied, [verify hello Automated Backup configuration](#verifysettings).</span></span>

### <a name="disable-automated-backup"></a><span data-ttu-id="026fc-220">Desabilitar o Backup automatizado</span><span class="sxs-lookup"><span data-stu-id="026fc-220">Disable Automated Backup</span></span>

<span data-ttu-id="026fc-221">toodisable Backup automatizado, Olá execução mesmo script sem Olá **-habilitar** parâmetro toohello **AzureRmVMSqlServerAutoBackupConfig novo** comando.</span><span class="sxs-lookup"><span data-stu-id="026fc-221">toodisable Automated Backup, run hello same script without hello **-Enable** parameter toohello **New-AzureRmVMSqlServerAutoBackupConfig** command.</span></span> <span data-ttu-id="026fc-222">Olá ausência de saudação **-habilitar** recurso de saudação do parâmetro sinais Olá comando toodisable.</span><span class="sxs-lookup"><span data-stu-id="026fc-222">hello absence of hello **-Enable** parameter signals hello command toodisable hello feature.</span></span> <span data-ttu-id="026fc-223">Como com a instalação, pode levar vários minutos toodisable Backup automatizado.</span><span class="sxs-lookup"><span data-stu-id="026fc-223">As with installation, it can take several minutes toodisable Automated Backup.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

### <a name="example-script"></a><span data-ttu-id="026fc-224">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="026fc-224">Example script</span></span>

<span data-ttu-id="026fc-225">Olá script a seguir fornece um conjunto de variáveis que você pode personalizar tooenable e configurar o Backup automatizado para sua VM.</span><span class="sxs-lookup"><span data-stu-id="026fc-225">hello following script provides a set of variables that you can customize tooenable and configure Automated Backup for your VM.</span></span> <span data-ttu-id="026fc-226">No seu caso, talvez seja necessário toocustomize script de saudação com base nos seus requisitos.</span><span class="sxs-lookup"><span data-stu-id="026fc-226">In your case, you might need toocustomize hello script based on your requirements.</span></span> <span data-ttu-id="026fc-227">Por exemplo, você deve ter toomake alterações se desejar que o backup de saudação toodisable de bancos de dados do sistema ou habilitar a criptografia.</span><span class="sxs-lookup"><span data-stu-id="026fc-227">For example, you would have toomake changes if you wanted toodisable hello backup of system databases or enable encryption.</span></span>

```powershell
$vmname = "yourvmname"
$resourcegroupname = "vmresourcegroupname"
$region = “Azure region name such as EASTUS2”
$storage_accountname = “storageaccountname”
$storage_resourcegroupname = $resourcegroupname
$retentionperiod = 10

# ResourceGroupName is hello resource group which is hosting hello VM where you are deploying hello SQL IaaS Extension

Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region

# Creates/use a storage account toostore hello backups

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }

# Configure Automated Backup settings

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays $retentionperiod -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

# Apply hello Automated Backup settings toohello VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="026fc-228">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="026fc-228">Next steps</span></span>

<span data-ttu-id="026fc-229">O Backup Automatizado configura o Backup Gerenciado em VMs do Azure.</span><span class="sxs-lookup"><span data-stu-id="026fc-229">Automated Backup configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="026fc-230">Portanto, é muito importante[documentação Olá Backup gerenciado](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand Olá comportamento e as implicações.</span><span class="sxs-lookup"><span data-stu-id="026fc-230">So it is important too[review hello documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello behavior and implications.</span></span>

<span data-ttu-id="026fc-231">Você pode encontrar backup adicional e restaurar a orientação do SQL Server em VMs do Azure no hello tópico a seguir: [de Backup e restauração do SQL Server em máquinas virtuais Azure](virtual-machines-windows-sql-backup-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="026fc-231">You can find additional backup and restore guidance for SQL Server on Azure VMs in hello following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span></span>

<span data-ttu-id="026fc-232">Para obter informações sobre outras tarefas de automação disponíveis, consulte [Extensão do agente IaaS do SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="026fc-232">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="026fc-233">Para obter mais informações sobre como executar o SQL Server em VMs do Azure, consulte [Visão geral do SQL Server em Máquinas Virtuais do Azure](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="026fc-233">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

