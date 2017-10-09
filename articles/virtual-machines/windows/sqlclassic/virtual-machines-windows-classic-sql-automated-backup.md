---
title: "aaaAutomated Backup para máquinas de virtuais de servidor do SQL (clássico) | Microsoft Docs"
description: "Explica o recurso de Backup automatizado Olá para SQL Server em execução em máquinas virtuais do Azure usando o Gerenciador de recursos. "
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 3333e830-8a60-42f5-9f44-8e02e9868d7b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: 5d8f0412578c2d86edc6e54093a5da4891d3847e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-for-sql-server-in-azure-virtual-machines-classic"></a><span data-ttu-id="4c3f8-103">Backup automatizado para SQL Server em Máquinas Virtuais do Azure (Clássico)</span><span class="sxs-lookup"><span data-stu-id="4c3f8-103">Automated Backup for SQL Server in Azure Virtual Machines (Classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4c3f8-104">Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="4c3f8-104">Resource Manager</span></span>](../sql/virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="4c3f8-105">Clássico</span><span class="sxs-lookup"><span data-stu-id="4c3f8-105">Classic</span></span>](../classic/sql-automated-backup.md)
> 
> 

<span data-ttu-id="4c3f8-106">Backup automatizado configura automaticamente [tooMicrosoft de Backup gerenciado do Azure](https://msdn.microsoft.com/library/dn449496.aspx) para todos os novos e existentes bancos de dados em uma VM do Azure executando o SQL Server 2014 Standard ou Enterprise.</span><span class="sxs-lookup"><span data-stu-id="4c3f8-106">Automated Backup automatically configures [Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> <span data-ttu-id="4c3f8-107">Isso permite que os backups de banco de dados regular tooconfigure que utilizam o armazenamento de BLOBs do Azure durável.</span><span class="sxs-lookup"><span data-stu-id="4c3f8-107">This enables you tooconfigure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="4c3f8-108">Backup automatizado depende Olá [extensão do SQL Server IaaS Agent](../classic/sql-server-agent-extension.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4c3f8-108">Automated Backup depends on hello [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="4c3f8-109">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="4c3f8-109">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="4c3f8-110">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="4c3f8-110">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="4c3f8-111">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="4c3f8-111">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="4c3f8-112">versão do Gerenciador de recursos de saudação tooview deste artigo, consulte [Backup automatizado para SQL Server no Gerenciador de recursos de máquinas virtuais do Azure](../sql/virtual-machines-windows-sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="4c3f8-112">tooview hello Resource Manager version of this article, see [Automated Backup for SQL Server in Azure Virtual Machines Resource Manager](../sql/virtual-machines-windows-sql-automated-backup.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4c3f8-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4c3f8-113">Prerequisites</span></span>
<span data-ttu-id="4c3f8-114">toouse Backup automatizado, considere Olá pré-requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="4c3f8-114">toouse Automated Backup, consider hello following prerequisites:</span></span>

<span data-ttu-id="4c3f8-115">**Sistema operacional**:</span><span class="sxs-lookup"><span data-stu-id="4c3f8-115">**Operating System**:</span></span>

* <span data-ttu-id="4c3f8-116">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="4c3f8-116">Windows Server 2012</span></span>
* <span data-ttu-id="4c3f8-117">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="4c3f8-117">Windows Server 2012 R2</span></span>
* <span data-ttu-id="4c3f8-118">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="4c3f8-118">Windows Server 2016</span></span>

<span data-ttu-id="4c3f8-119">**Versão/edição do SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="4c3f8-119">**SQL Server version/edition**:</span></span>

* <span data-ttu-id="4c3f8-120">SQL Server 2014 Standard</span><span class="sxs-lookup"><span data-stu-id="4c3f8-120">SQL Server 2014 Standard</span></span>
* <span data-ttu-id="4c3f8-121">SQL Server 2014 Enterprise</span><span class="sxs-lookup"><span data-stu-id="4c3f8-121">SQL Server 2014 Enterprise</span></span>

> [!NOTE]
> <span data-ttu-id="4c3f8-122">No Backup Automatizado, ainda não há suporte para o SQL Server 2016.</span><span class="sxs-lookup"><span data-stu-id="4c3f8-122">SQL Server 2016 is not yet supported for Automated Backup.</span></span>
> 
> 

<span data-ttu-id="4c3f8-123">**Configuração do banco de dados**:</span><span class="sxs-lookup"><span data-stu-id="4c3f8-123">**Database configuration**:</span></span>

* <span data-ttu-id="4c3f8-124">Bancos de dados de destino devem usar o modelo de recuperação completa de saudação.</span><span class="sxs-lookup"><span data-stu-id="4c3f8-124">Target databases must use hello full recovery model.</span></span>

<span data-ttu-id="4c3f8-125">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="4c3f8-125">**Azure PowerShell**:</span></span>

* <span data-ttu-id="4c3f8-126">[Olá mais recente do Azure PowerShell comandos de instalação](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4c3f8-126">[Install hello latest Azure PowerShell commands](/powershell/azure/overview).</span></span>

<span data-ttu-id="4c3f8-127">**Extensão IaaS do SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="4c3f8-127">**SQL Server IaaS Extension**:</span></span>

* <span data-ttu-id="4c3f8-128">[Instalar Olá extensão do SQL Server IaaS](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="4c3f8-128">[Install hello SQL Server IaaS Extension](../classic/sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="4c3f8-129">Configurações</span><span class="sxs-lookup"><span data-stu-id="4c3f8-129">Settings</span></span>
<span data-ttu-id="4c3f8-130">Olá, tabela a seguir descreve as opções de saudação que podem ser configuradas para Backup automatizado.</span><span class="sxs-lookup"><span data-stu-id="4c3f8-130">hello following table describes hello options that can be configured for Automated Backup.</span></span> <span data-ttu-id="4c3f8-131">Para VMs clássicas, você deve usar PowerShell tooconfigure essas configurações.</span><span class="sxs-lookup"><span data-stu-id="4c3f8-131">For classic VMs, you must use PowerShell tooconfigure these settings.</span></span>

| <span data-ttu-id="4c3f8-132">Configuração</span><span class="sxs-lookup"><span data-stu-id="4c3f8-132">Setting</span></span> | <span data-ttu-id="4c3f8-133">Intervalo (Padrão)</span><span class="sxs-lookup"><span data-stu-id="4c3f8-133">Range (Default)</span></span> | <span data-ttu-id="4c3f8-134">Descrição</span><span class="sxs-lookup"><span data-stu-id="4c3f8-134">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4c3f8-135">**Backup Automatizado**</span><span class="sxs-lookup"><span data-stu-id="4c3f8-135">**Automated Backup**</span></span> |<span data-ttu-id="4c3f8-136">Habilitar/desabilitar (Desabilitado)</span><span class="sxs-lookup"><span data-stu-id="4c3f8-136">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="4c3f8-137">Habilita ou desabilita o Backup Automatizado de uma VM do Azure que executa o SQL Server 2014 Standard ou Enterprise.</span><span class="sxs-lookup"><span data-stu-id="4c3f8-137">Enables or disables Automated Backup for an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> |
| <span data-ttu-id="4c3f8-138">**Período de retenção**</span><span class="sxs-lookup"><span data-stu-id="4c3f8-138">**Retention Period**</span></span> |<span data-ttu-id="4c3f8-139">Um a 30 dias (30 dias)</span><span class="sxs-lookup"><span data-stu-id="4c3f8-139">1-30 days (30 days)</span></span> |<span data-ttu-id="4c3f8-140">número de saudação de dias tooretain um backup.</span><span class="sxs-lookup"><span data-stu-id="4c3f8-140">hello number of days tooretain a backup.</span></span> |
| <span data-ttu-id="4c3f8-141">**Conta de armazenamento**</span><span class="sxs-lookup"><span data-stu-id="4c3f8-141">**Storage Account**</span></span> |<span data-ttu-id="4c3f8-142">Conta de armazenamento do Azure (conta de armazenamento Olá criada para Olá especificado VM)</span><span class="sxs-lookup"><span data-stu-id="4c3f8-142">Azure storage account (hello storage account created for hello specified VM)</span></span> |<span data-ttu-id="4c3f8-143">Um toouse de conta de armazenamento do Azure para armazenar arquivos de Backup automatizado no armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="4c3f8-143">An Azure storage account toouse for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="4c3f8-144">Um contêiner é criado neste local toostore todos os arquivos de backup.</span><span class="sxs-lookup"><span data-stu-id="4c3f8-144">A container is created at this location toostore all backup files.</span></span> <span data-ttu-id="4c3f8-145">o arquivo de backup Olá convenção de nomenclatura inclui Olá data, hora e nome do computador.</span><span class="sxs-lookup"><span data-stu-id="4c3f8-145">hello backup file naming convention includes hello date, time, and machine name.</span></span> |
| <span data-ttu-id="4c3f8-146">**Criptografia**</span><span class="sxs-lookup"><span data-stu-id="4c3f8-146">**Encryption**</span></span> |<span data-ttu-id="4c3f8-147">Habilitar/desabilitar (Desabilitado)</span><span class="sxs-lookup"><span data-stu-id="4c3f8-147">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="4c3f8-148">Habilita ou desabilita a criptografia.</span><span class="sxs-lookup"><span data-stu-id="4c3f8-148">Enables or disables encryption.</span></span> <span data-ttu-id="4c3f8-149">Quando a criptografia está habilitada, certificados Olá backup de saudação toorestore usados estão localizados em Olá especificado conta de armazenamento no hello automaticbackup mesmo contêiner usando Olá a mesma convenção de nomenclatura.</span><span class="sxs-lookup"><span data-stu-id="4c3f8-149">When encryption is enabled, hello certificates used toorestore hello backup are located in hello specified storage account in hello same automaticbackup container using hello same naming convention.</span></span> <span data-ttu-id="4c3f8-150">Se Olá senha for alterada, um novo certificado será gerado com essa senha, mas o certificado antigo Olá permanece backups anteriores toorestore.</span><span class="sxs-lookup"><span data-stu-id="4c3f8-150">If hello password changes, a new certificate is generated with that password, but hello old certificate remains toorestore prior backups.</span></span> |
| <span data-ttu-id="4c3f8-151">**Senha**</span><span class="sxs-lookup"><span data-stu-id="4c3f8-151">**Password**</span></span> |<span data-ttu-id="4c3f8-152">Texto da senha (nenhum)</span><span class="sxs-lookup"><span data-stu-id="4c3f8-152">Password text (None)</span></span> |<span data-ttu-id="4c3f8-153">Uma senha para as chaves de criptografia.</span><span class="sxs-lookup"><span data-stu-id="4c3f8-153">A password for encryption keys.</span></span> <span data-ttu-id="4c3f8-154">Isso só é necessário se a criptografia estiver habilitada.</span><span class="sxs-lookup"><span data-stu-id="4c3f8-154">This is only required if encryption is enabled.</span></span> <span data-ttu-id="4c3f8-155">Ordem toorestore um backup criptografado, você deve ter senha correta hello e o certificado relacionado que foi usado em tempo de Olá Olá backup foi feito.</span><span class="sxs-lookup"><span data-stu-id="4c3f8-155">In order toorestore an encrypted backup, you must have hello correct password and related certificate that was used at hello time hello backup was taken.</span></span> | <span data-ttu-id="4c3f8-156">**Bancos de dados do sistema de backup**</span><span class="sxs-lookup"><span data-stu-id="4c3f8-156">**Backup system databases**</span></span> | <span data-ttu-id="4c3f8-157">Habilitar/desabilitar (Desabilitado)</span><span class="sxs-lookup"><span data-stu-id="4c3f8-157">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="4c3f8-158">Fazer backups completos do Mestre, Modelo e MSDB</span><span class="sxs-lookup"><span data-stu-id="4c3f8-158">Take full backups of Master, Model, and MSDB</span></span> |
| <span data-ttu-id="4c3f8-159">**Configurar agendamento de backup**</span><span class="sxs-lookup"><span data-stu-id="4c3f8-159">**Configure backup schedule**</span></span> | <span data-ttu-id="4c3f8-160">Manual/Automatizado (Automatizado)</span><span class="sxs-lookup"><span data-stu-id="4c3f8-160">Manual/Automated (Automated)</span></span> | <span data-ttu-id="4c3f8-161">Selecione **automatizada** tooautomatically levar completa e com base no crescimento do log de backups de log.</span><span class="sxs-lookup"><span data-stu-id="4c3f8-161">Select **Automated** tooautomatically take full and log backups based on log growth.</span></span> <span data-ttu-id="4c3f8-162">Selecione **Manual** toospecify agenda de saudação para completo e backups de log.</span><span class="sxs-lookup"><span data-stu-id="4c3f8-162">Select **Manual** toospecify hello schedule for full and log backups.</span></span> |

## <a name="configuration-with-powershell"></a><span data-ttu-id="4c3f8-163">Configuração com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="4c3f8-163">Configuration with PowerShell</span></span>
<span data-ttu-id="4c3f8-164">Olá PowerShell de exemplo a seguir, o Backup automatizado é configurado para uma VM existente do SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="4c3f8-164">In hello following PowerShell example, Automated Backup is configured for an existing SQL Server 2014 VM.</span></span> <span data-ttu-id="4c3f8-165">Olá **AzureVMSqlServerAutoBackupConfig novo** comando configura os backups de toostore de configurações de Backup automatizado Olá na conta de armazenamento do Azure Olá especificada pela variável Olá $storageaccount.</span><span class="sxs-lookup"><span data-stu-id="4c3f8-165">hello **New-AzureVMSqlServerAutoBackupConfig** command configures hello Automated Backup settings toostore backups in hello Azure storage account specified by hello $storageaccount variable.</span></span> <span data-ttu-id="4c3f8-166">Esses backups serão mantidos por 10 dias.</span><span class="sxs-lookup"><span data-stu-id="4c3f8-166">These backups will be retained for 10 days.</span></span> <span data-ttu-id="4c3f8-167">Olá **AzureVMSqlServerExtension conjunto** comando Olá atualizações especificado VM do Azure com essas configurações.</span><span class="sxs-lookup"><span data-stu-id="4c3f8-167">hello **Set-AzureVMSqlServerExtension** command updates hello specified Azure VM with these settings.</span></span>

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

<span data-ttu-id="4c3f8-168">Ele pode levar vários tooinstall de minutos e configure Olá SQL Server IaaS Agent.</span><span class="sxs-lookup"><span data-stu-id="4c3f8-168">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span>

<span data-ttu-id="4c3f8-169">criptografia de tooenable modificar Olá anterior script toopass Olá parâmetro EnableEncryption junto com uma senha (cadeia de caracteres segura) para o parâmetro CertificatePassword de saudação.</span><span class="sxs-lookup"><span data-stu-id="4c3f8-169">tooenable encryption, modify hello previous script toopass hello EnableEncryption parameter along with a password (secure string) for hello CertificatePassword parameter.</span></span> <span data-ttu-id="4c3f8-170">Olá script a seguir permite que as configurações de Backup automatizado Olá no exemplo anterior hello e adiciona a criptografia.</span><span class="sxs-lookup"><span data-stu-id="4c3f8-170">hello following script enables hello Automated Backup settings in hello previous example and adds encryption.</span></span>

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $password = "P@ssw0rd"
    $encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10 -EnableEncryption -CertificatePassword $encryptionpassword

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

<span data-ttu-id="4c3f8-171">toodisable o backup automático, Olá execução mesmo script sem Olá **-habilitar** parâmetro toohello **AzureVMSqlServerAutoBackupConfig novo**.</span><span class="sxs-lookup"><span data-stu-id="4c3f8-171">toodisable automatic backup, run hello same script without hello **-Enable** parameter toohello **New-AzureVMSqlServerAutoBackupConfig**.</span></span> <span data-ttu-id="4c3f8-172">Como com a instalação, pode levar vários minutos toodisable Backup automatizado.</span><span class="sxs-lookup"><span data-stu-id="4c3f8-172">As with installation, it can take several minutes toodisable Automated Backup.</span></span>

> [!NOTE]
> <span data-ttu-id="4c3f8-173">Desabilitar e desinstalar Olá IaaS do SQL Server Agent não remove as configurações de Backup gerenciado Olá configurado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="4c3f8-173">Disabling and uninstalling hello SQL Server IaaS Agent does not remove hello previously configured Managed Backup settings.</span></span> <span data-ttu-id="4c3f8-174">Você deve desabilitar o Backup automatizado antes de desabilitar ou desinstalar Olá SQL Server IaaS Agent.</span><span class="sxs-lookup"><span data-stu-id="4c3f8-174">You should disable Automated Backup before disabling or uninstalling hello SQL Server IaaS Agent.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="4c3f8-175">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4c3f8-175">Next steps</span></span>
<span data-ttu-id="4c3f8-176">O Backup Automatizado configura o Backup Gerenciado em VMs do Azure.</span><span class="sxs-lookup"><span data-stu-id="4c3f8-176">Automated Backup configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="4c3f8-177">Portanto, é muito importante[documentação Olá Backup gerenciado](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand Olá comportamento e as implicações.</span><span class="sxs-lookup"><span data-stu-id="4c3f8-177">So it is important too[review hello documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello behavior and implications.</span></span>

<span data-ttu-id="4c3f8-178">Você pode encontrar backup adicional e restaurar a orientação do SQL Server em VMs do Azure no hello tópico a seguir: [de Backup e restauração do SQL Server em máquinas virtuais Azure](../sql/virtual-machines-windows-sql-backup-recovery.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4c3f8-178">You can find additional backup and restore guidance for SQL Server on Azure VMs in hello following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-backup-recovery.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>

<span data-ttu-id="4c3f8-179">Para obter informações sobre outras tarefas de automação disponíveis, consulte [Extensão do agente IaaS do SQL Server](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="4c3f8-179">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

<span data-ttu-id="4c3f8-180">Para obter mais informações sobre como executar o SQL Server em VMs do Azure, consulte [Visão geral do SQL Server em Máquinas Virtuais do Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4c3f8-180">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

