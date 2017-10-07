---
title: "aaaAutomated v2 de Backup para máquinas de virtuais do SQL Server 2016 do Azure | Microsoft Docs"
description: "Explica o recurso de Backup automatizado Olá para VMs do SQL Server 2016 em execução no Azure. Este artigo é específico tooVMs usando Olá Gerenciador de recursos."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: ebd23868-821c-475b-b867-06d4a2e310c7
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 04/05/2017
ms.author: jroth
ms.openlocfilehash: a322792fb22c76bfa74fafb711b8b1927a6e2b3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-v2-for-sql-server-2016-azure-virtual-machines-resource-manager"></a><span data-ttu-id="e8424-104">Backup Automatizado v2 para máquinas virtuais do Azure do SQL Server 2016 (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="e8424-104">Automated Backup v2 for SQL Server 2016 Azure Virtual Machines (Resource Manager)</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e8424-105">SQL Server 2014</span><span class="sxs-lookup"><span data-stu-id="e8424-105">SQL Server 2014</span></span>](virtual-machines-windows-sql-automated-backup.md)
> * [<span data-ttu-id="e8424-106">SQL Server 2016</span><span class="sxs-lookup"><span data-stu-id="e8424-106">SQL Server 2016</span></span>](virtual-machines-windows-sql-automated-backup-v2.md)

<span data-ttu-id="e8424-107">V2 de Backup automatizado configura automaticamente [tooMicrosoft de Backup gerenciado do Azure](https://msdn.microsoft.com/library/dn449496.aspx) para todos os novos e existentes bancos de dados em uma VM do Azure que executam edições do SQL Server 2016 Standard, Enterprise ou Developer.</span><span class="sxs-lookup"><span data-stu-id="e8424-107">Automated Backup v2 automatically configures [Managed Backup tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2016 Standard, Enterprise, or Developer editions.</span></span> <span data-ttu-id="e8424-108">Isso permite que os backups de banco de dados regular tooconfigure que utilizam o armazenamento de BLOBs do Azure durável.</span><span class="sxs-lookup"><span data-stu-id="e8424-108">This enables you tooconfigure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="e8424-109">V2 de Backup automatizado depende Olá [extensão do SQL Server IaaS Agent](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="e8424-109">Automated Backup v2 depends on hello [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="e8424-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e8424-110">Prerequisites</span></span>
<span data-ttu-id="e8424-111">toouse v2 de Backup automatizado, Olá examine os pré-requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="e8424-111">toouse Automated Backup v2, review hello following prerequisites:</span></span>

<span data-ttu-id="e8424-112">**Sistema operacional**:</span><span class="sxs-lookup"><span data-stu-id="e8424-112">**Operating System**:</span></span>

- <span data-ttu-id="e8424-113">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="e8424-113">Windows Server 2012 R2</span></span>
- <span data-ttu-id="e8424-114">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="e8424-114">Windows Server 2016</span></span>

<span data-ttu-id="e8424-115">**Versão/edição do SQL Server**:</span><span class="sxs-lookup"><span data-stu-id="e8424-115">**SQL Server version/edition**:</span></span>

- <span data-ttu-id="e8424-116">SQL Server 2016 Standard</span><span class="sxs-lookup"><span data-stu-id="e8424-116">SQL Server 2016 Standard</span></span>
- <span data-ttu-id="e8424-117">SQL Server 2016 Enterprise</span><span class="sxs-lookup"><span data-stu-id="e8424-117">SQL Server 2016 Enterprise</span></span>
- <span data-ttu-id="e8424-118">SQL Server 2016 Developer</span><span class="sxs-lookup"><span data-stu-id="e8424-118">SQL Server 2016 Developer</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e8424-119">O Backup Automatizado v2 funciona com o SQL Server 2016.</span><span class="sxs-lookup"><span data-stu-id="e8424-119">Automated Backup v2 works with SQL Server 2016.</span></span> <span data-ttu-id="e8424-120">Se você estiver usando o SQL Server 2014, você pode usar o Backup automatizado v1 tooback backup de seus bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="e8424-120">If you are using SQL Server 2014, you can use Automated Backup v1 tooback up your databases.</span></span> <span data-ttu-id="e8424-121">Para obter mais informações, veja [Backup Automatizado para máquinas virtuais do Azure no SQL Server 2014](virtual-machines-windows-sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="e8424-121">For more information, see [Automated Backup for SQL Server 2014 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup.md).</span></span>

<span data-ttu-id="e8424-122">**Configuração do banco de dados**:</span><span class="sxs-lookup"><span data-stu-id="e8424-122">**Database configuration**:</span></span>

- <span data-ttu-id="e8424-123">Bancos de dados de destino devem usar o modelo de recuperação completa de saudação.</span><span class="sxs-lookup"><span data-stu-id="e8424-123">Target databases must use hello full recovery model.</span></span> <span data-ttu-id="e8424-124">Para obter mais informações sobre o impacto de saudação do modelo de recuperação completa de saudação em backups, consulte [Olá Backup no modelo de recuperação completa](https://technet.microsoft.com/library/ms190217.aspx).</span><span class="sxs-lookup"><span data-stu-id="e8424-124">For more information about hello impact of hello full recovery model on backups, see [Backup Under hello Full Recovery Model](https://technet.microsoft.com/library/ms190217.aspx).</span></span>
- <span data-ttu-id="e8424-125">Bancos de dados do sistema não tem toouse modelo de recuperação completa.</span><span class="sxs-lookup"><span data-stu-id="e8424-125">System databases do not have toouse full recovery model.</span></span> <span data-ttu-id="e8424-126">No entanto, se você precisar toobe de backups de log levado para o modelo ou MSDB, você deve usar o modelo de recuperação completa.</span><span class="sxs-lookup"><span data-stu-id="e8424-126">However, if you require log backups toobe taken for Model or MSDB, you must use full recovery model.</span></span>
- <span data-ttu-id="e8424-127">Bancos de dados de destino devem estar na instância do SQL Server padrão hello.</span><span class="sxs-lookup"><span data-stu-id="e8424-127">Target databases must be on hello default SQL Server instance.</span></span> <span data-ttu-id="e8424-128">Olá extensão de IaaS do SQL Server não oferece suporte a instâncias nomeadas.</span><span class="sxs-lookup"><span data-stu-id="e8424-128">hello SQL Server IaaS Extension does not support named instances.</span></span>

<span data-ttu-id="e8424-129">**Modelo de implantação do Azure**:</span><span class="sxs-lookup"><span data-stu-id="e8424-129">**Azure deployment model**:</span></span>

- <span data-ttu-id="e8424-130">Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="e8424-130">Resource Manager</span></span>

> [!NOTE]
> <span data-ttu-id="e8424-131">Backup automatizado depende Olá **extensão do SQL Server IaaS Agent**.</span><span class="sxs-lookup"><span data-stu-id="e8424-131">Automated Backup relies on hello **SQL Server IaaS Agent Extension**.</span></span> <span data-ttu-id="e8424-132">As imagens atuais da galeria da máquina virtual do SQL adicionam essa extensão por padrão.</span><span class="sxs-lookup"><span data-stu-id="e8424-132">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="e8424-133">Para obter mais informações, consulte [Extensão do agente IaaS do SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="e8424-133">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="e8424-134">Configurações</span><span class="sxs-lookup"><span data-stu-id="e8424-134">Settings</span></span>
<span data-ttu-id="e8424-135">Olá, tabela a seguir descreve as opções de saudação que podem ser configuradas para Backup automatizado v2.</span><span class="sxs-lookup"><span data-stu-id="e8424-135">hello following table describes hello options that can be configured for Automated Backup v2.</span></span> <span data-ttu-id="e8424-136">etapas de configuração real de saudação variam dependendo se você usar Olá portal do Azure ou comandos do PowerShell do Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="e8424-136">hello actual configuration steps vary depending on whether you use hello Azure portal or Azure Windows PowerShell commands.</span></span>

### <a name="basic-settings"></a><span data-ttu-id="e8424-137">Configurações Básicas</span><span class="sxs-lookup"><span data-stu-id="e8424-137">Basic Settings</span></span>

| <span data-ttu-id="e8424-138">Configuração</span><span class="sxs-lookup"><span data-stu-id="e8424-138">Setting</span></span> | <span data-ttu-id="e8424-139">Intervalo (Padrão)</span><span class="sxs-lookup"><span data-stu-id="e8424-139">Range (Default)</span></span> | <span data-ttu-id="e8424-140">Descrição</span><span class="sxs-lookup"><span data-stu-id="e8424-140">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e8424-141">**Backup Automatizado**</span><span class="sxs-lookup"><span data-stu-id="e8424-141">**Automated Backup**</span></span> | <span data-ttu-id="e8424-142">Habilitar/desabilitar (Desabilitado)</span><span class="sxs-lookup"><span data-stu-id="e8424-142">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="e8424-143">Habilita ou desabilita o Backup Automatizado de uma VM do Azure que executa o SQL Server 2016 Standard ou Enterprise.</span><span class="sxs-lookup"><span data-stu-id="e8424-143">Enables or disables Automated Backup for an Azure VM running SQL Server 2016 Standard or Enterprise.</span></span> |
| <span data-ttu-id="e8424-144">**Período de retenção**</span><span class="sxs-lookup"><span data-stu-id="e8424-144">**Retention Period**</span></span> | <span data-ttu-id="e8424-145">Um a 30 dias (30 dias)</span><span class="sxs-lookup"><span data-stu-id="e8424-145">1-30 days (30 days)</span></span> | <span data-ttu-id="e8424-146">número de saudação de backups de tooretain dias.</span><span class="sxs-lookup"><span data-stu-id="e8424-146">hello number of days tooretain backups.</span></span> |
| <span data-ttu-id="e8424-147">**Conta de armazenamento**</span><span class="sxs-lookup"><span data-stu-id="e8424-147">**Storage Account**</span></span> | <span data-ttu-id="e8424-148">Conta de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="e8424-148">Azure storage account</span></span> | <span data-ttu-id="e8424-149">Um toouse de conta de armazenamento do Azure para armazenar arquivos de Backup automatizado no armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="e8424-149">An Azure storage account toouse for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="e8424-150">Um contêiner é criado neste local toostore todos os arquivos de backup.</span><span class="sxs-lookup"><span data-stu-id="e8424-150">A container is created at this location toostore all backup files.</span></span> <span data-ttu-id="e8424-151">o arquivo de backup Olá convenção de nomenclatura inclui Olá data, hora e GUID do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e8424-151">hello backup file naming convention includes hello date, time, and database GUID.</span></span> |
| <span data-ttu-id="e8424-152">**Criptografia**</span><span class="sxs-lookup"><span data-stu-id="e8424-152">**Encryption**</span></span> |<span data-ttu-id="e8424-153">Habilitar/desabilitar (Desabilitado)</span><span class="sxs-lookup"><span data-stu-id="e8424-153">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="e8424-154">Habilita ou desabilita a criptografia.</span><span class="sxs-lookup"><span data-stu-id="e8424-154">Enables or disables encryption.</span></span> <span data-ttu-id="e8424-155">Quando a criptografia está habilitada, Olá certificados usados toorestore Olá backup estão localizados em Olá especificado conta de armazenamento em Olá mesmo **automaticbackup** Olá contêiner usando a mesma convenção de nomenclatura.</span><span class="sxs-lookup"><span data-stu-id="e8424-155">When encryption is enabled, hello certificates used toorestore hello backup are located in hello specified storage account in hello same **automaticbackup** container using hello same naming convention.</span></span> <span data-ttu-id="e8424-156">Se Olá senha for alterada, um novo certificado será gerado com essa senha, mas o certificado antigo Olá permanece backups anteriores toorestore.</span><span class="sxs-lookup"><span data-stu-id="e8424-156">If hello password changes, a new certificate is generated with that password, but hello old certificate remains toorestore prior backups.</span></span> |
| <span data-ttu-id="e8424-157">**Senha**</span><span class="sxs-lookup"><span data-stu-id="e8424-157">**Password**</span></span> |<span data-ttu-id="e8424-158">Texto da senha</span><span class="sxs-lookup"><span data-stu-id="e8424-158">Password text</span></span> | <span data-ttu-id="e8424-159">Uma senha para as chaves de criptografia.</span><span class="sxs-lookup"><span data-stu-id="e8424-159">A password for encryption keys.</span></span> <span data-ttu-id="e8424-160">Isso só é necessário se a criptografia estiver habilitada.</span><span class="sxs-lookup"><span data-stu-id="e8424-160">This is only required if encryption is enabled.</span></span> <span data-ttu-id="e8424-161">Ordem toorestore um backup criptografado, você deve ter senha correta hello e o certificado relacionado que foi usado em tempo de Olá Olá backup foi feito.</span><span class="sxs-lookup"><span data-stu-id="e8424-161">In order toorestore an encrypted backup, you must have hello correct password and related certificate that was used at hello time hello backup was taken.</span></span> |

### <a name="advanced-settings"></a><span data-ttu-id="e8424-162">Configurações avançadas</span><span class="sxs-lookup"><span data-stu-id="e8424-162">Advanced Settings</span></span>

| <span data-ttu-id="e8424-163">Configuração</span><span class="sxs-lookup"><span data-stu-id="e8424-163">Setting</span></span> | <span data-ttu-id="e8424-164">Intervalo (Padrão)</span><span class="sxs-lookup"><span data-stu-id="e8424-164">Range (Default)</span></span> | <span data-ttu-id="e8424-165">Descrição</span><span class="sxs-lookup"><span data-stu-id="e8424-165">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e8424-166">**Backups de Banco de Dados do Sistema**</span><span class="sxs-lookup"><span data-stu-id="e8424-166">**System Database Backups**</span></span> | <span data-ttu-id="e8424-167">Habilitar/desabilitar (Desabilitado)</span><span class="sxs-lookup"><span data-stu-id="e8424-167">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="e8424-168">Quando habilitado, esse recurso também fará backup Olá os bancos de dados: Master, MSDB e modelo.</span><span class="sxs-lookup"><span data-stu-id="e8424-168">When enabled, this feature will also back up hello system databases: Master, MSDB, and Model.</span></span> <span data-ttu-id="e8424-169">Olá MSDB e bancos de dados de modelo, verifique se eles são no modo de recuperação completa se você quiser toobe de backups de log feito.</span><span class="sxs-lookup"><span data-stu-id="e8424-169">For hello MSDB and Model databases, verify that they are in full recovery mode if you want log backups toobe taken.</span></span> <span data-ttu-id="e8424-170">Os backups de log nunca são feitos para o Mestre.</span><span class="sxs-lookup"><span data-stu-id="e8424-170">Log backups are never taken for Master.</span></span> <span data-ttu-id="e8424-171">E não é feito nenhum backup para o TempDB.</span><span class="sxs-lookup"><span data-stu-id="e8424-171">And no backups are taken for TempDB.</span></span> |
| <span data-ttu-id="e8424-172">**Agendamento de Backup**</span><span class="sxs-lookup"><span data-stu-id="e8424-172">**Backup Schedule**</span></span> | <span data-ttu-id="e8424-173">Manual/Automatizado (Automatizado)</span><span class="sxs-lookup"><span data-stu-id="e8424-173">Manual/Automated (Automated)</span></span> | <span data-ttu-id="e8424-174">Por padrão, o agendamento de backup Olá será automaticamente determinado com base no crescimento do log hello.</span><span class="sxs-lookup"><span data-stu-id="e8424-174">By default, hello backup schedule will be automatically determined based on hello log growth.</span></span> <span data-ttu-id="e8424-175">Agendamento de backup manual permite que a janela de tempo de saudação do hello usuário toospecify para backups.</span><span class="sxs-lookup"><span data-stu-id="e8424-175">Manual backup schedule allows hello user toospecify hello time window for backups.</span></span> <span data-ttu-id="e8424-176">Nesse caso, os backups só terá ocorre na saudação especificado frequência e durante a saudação especificado na janela de tempo de um determinado dia.</span><span class="sxs-lookup"><span data-stu-id="e8424-176">In this case, backups will only ever take place at hello specified frequency and during hello specified time window of a given day.</span></span> |
| <span data-ttu-id="e8424-177">**Frequência do backup completo**</span><span class="sxs-lookup"><span data-stu-id="e8424-177">**Full backup frequency**</span></span> | <span data-ttu-id="e8424-178">Diariamente/Semanalmente</span><span class="sxs-lookup"><span data-stu-id="e8424-178">Daily/Weekly</span></span> | <span data-ttu-id="e8424-179">Frequência de backups completos.</span><span class="sxs-lookup"><span data-stu-id="e8424-179">Frequency of full backups.</span></span> <span data-ttu-id="e8424-180">Em ambos os casos, backups completos serão iniciado durante a próxima janela de tempo agendado hello.</span><span class="sxs-lookup"><span data-stu-id="e8424-180">In both cases, full backups will begin during hello next scheduled time window.</span></span> <span data-ttu-id="e8424-181">Quando Semanalmente estiver selecionado, os backups poderão abranger vários dias até que todos os bancos de dados tenham o backup realizado com êxito.</span><span class="sxs-lookup"><span data-stu-id="e8424-181">When weekly is selected, backups could span multiple days until all databases have successfully backed up.</span></span> |
| <span data-ttu-id="e8424-182">**Hora de início do backup completo**</span><span class="sxs-lookup"><span data-stu-id="e8424-182">**Full backup start time**</span></span> | <span data-ttu-id="e8424-183">00:00 – 23:00 (01:00)</span><span class="sxs-lookup"><span data-stu-id="e8424-183">00:00 – 23:00 (01:00)</span></span> | <span data-ttu-id="e8424-184">A hora de início de um determinado dia durante o qual os backups completos podem ocorrer.</span><span class="sxs-lookup"><span data-stu-id="e8424-184">Start time of a given day during which full backups can take place.</span></span> |
| <span data-ttu-id="e8424-185">**Janela de tempo do backup completo**</span><span class="sxs-lookup"><span data-stu-id="e8424-185">**Full backup time window**</span></span> | <span data-ttu-id="e8424-186">1 – 23 horas (1 hora)</span><span class="sxs-lookup"><span data-stu-id="e8424-186">1 – 23 hours (1 hour)</span></span> | <span data-ttu-id="e8424-187">Duração da janela de tempo de saudação de um determinado dia durante o qual os backups completos podem ocorrer.</span><span class="sxs-lookup"><span data-stu-id="e8424-187">Duration of hello time window of a given day during which full backups can take place.</span></span> |
| <span data-ttu-id="e8424-188">**Frequência de backup do log**</span><span class="sxs-lookup"><span data-stu-id="e8424-188">**Log backup frequency**</span></span> | <span data-ttu-id="e8424-189">5 – 60 minutos (60 minutos)</span><span class="sxs-lookup"><span data-stu-id="e8424-189">5 – 60 minutes (60 minutes)</span></span> | <span data-ttu-id="e8424-190">Frequência de backups de log.</span><span class="sxs-lookup"><span data-stu-id="e8424-190">Frequency of log backups.</span></span> |

## <a name="understanding-full-backup-frequency"></a><span data-ttu-id="e8424-191">Noções básicas sobre a frequência do backup completo</span><span class="sxs-lookup"><span data-stu-id="e8424-191">Understanding full backup frequency</span></span>
<span data-ttu-id="e8424-192">É importante toounderstand diferença de saudação entre backups completos diários e semanais.</span><span class="sxs-lookup"><span data-stu-id="e8424-192">It is important toounderstand hello difference between daily and weekly full backups.</span></span> <span data-ttu-id="e8424-193">Nesse esforço, abordaremos dois cenários de exemplo.</span><span class="sxs-lookup"><span data-stu-id="e8424-193">In this effort, we will walk through two example scenarios.</span></span>

### <a name="scenario-1-weekly-backups"></a><span data-ttu-id="e8424-194">Cenário 1: backups semanais</span><span class="sxs-lookup"><span data-stu-id="e8424-194">Scenario 1: Weekly backups</span></span>
<span data-ttu-id="e8424-195">Você tem uma VM do SQL Server que contém um número de bancos de dados muito grandes.</span><span class="sxs-lookup"><span data-stu-id="e8424-195">You have a SQL Server VM which contains a number of very large databases.</span></span>

<span data-ttu-id="e8424-196">Na segunda-feira, habilitar o Backup automatizado v2 com hello configurações a seguir:</span><span class="sxs-lookup"><span data-stu-id="e8424-196">On Monday, you enable Automated Backup v2 with hello following settings:</span></span>

- <span data-ttu-id="e8424-197">Agendamento de backup: **Manual**</span><span class="sxs-lookup"><span data-stu-id="e8424-197">Backup schedule: **Manual**</span></span>
- <span data-ttu-id="e8424-198">Frequência do backup completo: **Semanalmente**</span><span class="sxs-lookup"><span data-stu-id="e8424-198">Full backup frequency: **Weekly**</span></span>
- <span data-ttu-id="e8424-199">Hora de início do backup completo: **01:00**</span><span class="sxs-lookup"><span data-stu-id="e8424-199">Full backup start time: **01:00**</span></span>
- <span data-ttu-id="e8424-200">Janela de tempo do backup completo: **1 hora**</span><span class="sxs-lookup"><span data-stu-id="e8424-200">Full backup time window: **1 hour**</span></span>

<span data-ttu-id="e8424-201">Isso significa que essa janela de backup disponíveis próxima da saudação é terça-feira à 1H00 por 1 hora.</span><span class="sxs-lookup"><span data-stu-id="e8424-201">This means that hello next available backup window is Tuesday at 1 AM for 1 hour.</span></span> <span data-ttu-id="e8424-202">Nesse momento, o Backup Automatizado começará a fazer backup de seus bancos de dados um de cada vez.</span><span class="sxs-lookup"><span data-stu-id="e8424-202">At that time, Automated Backup will begin backing up your databases one at a time.</span></span> <span data-ttu-id="e8424-203">Nesse cenário, seus bancos de dados são grandes o suficiente para que os backups completos serão concluído para Olá primeiro alguns bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="e8424-203">In this scenario, your databases are large enough that full backups will complete for hello first couple databases.</span></span> <span data-ttu-id="e8424-204">No entanto, após uma hora nem todos os bancos de dados Olá tem sido feitos backup.</span><span class="sxs-lookup"><span data-stu-id="e8424-204">However, after one hour not all of hello databases have been backed up.</span></span>

<span data-ttu-id="e8424-205">Quando isso acontece, o Backup automatizado começará a backup Olá restantes Olá bancos de dados dia seguinte, quarta-feira à 1H00 por 1 hora.</span><span class="sxs-lookup"><span data-stu-id="e8424-205">When this happens, Automated Backup will begin backing up hello remaining databases hello next day, Wednesday at 1 AM for 1 hour.</span></span> <span data-ttu-id="e8424-206">Se nem todos os bancos de dados tem sido feitos no momento, ele tentará novamente Olá próximo dia no hello mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="e8424-206">If not all databases have been backed up in that time, it will try again hello next day at hello same time.</span></span> <span data-ttu-id="e8424-207">Isso continuará até que todos os bancos de dados tenham tido o backup realizado com êxito.</span><span class="sxs-lookup"><span data-stu-id="e8424-207">This will continue until all databases have been successfully backed up.</span></span>

<span data-ttu-id="e8424-208">Quando chegar terça-feira novamente, o Backup Automatizado começará a fazer o backup de todos os bancos de dados novamente.</span><span class="sxs-lookup"><span data-stu-id="e8424-208">Once it reaches Tuesday again, Automated Backup will begin backing up all databases once again.</span></span>

<span data-ttu-id="e8424-209">Este cenário mostra que o Backup automatizado só funciona dentro da janela de tempo especificada Olá, e cada banco de dados será feito uma vez por semana.</span><span class="sxs-lookup"><span data-stu-id="e8424-209">This scenario shows that Automated Backup will only operate within hello specified time window, and each database will be backed up once per week.</span></span> <span data-ttu-id="e8424-210">Isso também mostra que é possível para backups toospan vários dias no hello caso onde não é possível toocomplete todos os backups em um único dia.</span><span class="sxs-lookup"><span data-stu-id="e8424-210">This also shows that it is possible for backups toospan multiple days in hello case where it is not possible toocomplete all backups in a single day.</span></span>

### <a name="scenario-2-daily-backups"></a><span data-ttu-id="e8424-211">Cenário 2: backups diários</span><span class="sxs-lookup"><span data-stu-id="e8424-211">Scenario 2: Daily backups</span></span>
<span data-ttu-id="e8424-212">Você tem uma VM do SQL Server que contém um número de bancos de dados muito grandes.</span><span class="sxs-lookup"><span data-stu-id="e8424-212">You have a SQL Server VM which contains a number of very large databases.</span></span>

<span data-ttu-id="e8424-213">Na segunda-feira, habilitar o Backup automatizado v2 com hello configurações a seguir:</span><span class="sxs-lookup"><span data-stu-id="e8424-213">On Monday, you enable Automated Backup v2 with hello following settings:</span></span>

- <span data-ttu-id="e8424-214">Agendamento de backup: Manual</span><span class="sxs-lookup"><span data-stu-id="e8424-214">Backup schedule: Manual</span></span>
- <span data-ttu-id="e8424-215">Frequência do backup completo: Diariamente</span><span class="sxs-lookup"><span data-stu-id="e8424-215">Full backup frequency: Daily</span></span>
- <span data-ttu-id="e8424-216">Hora de início do backup completo: 22:00</span><span class="sxs-lookup"><span data-stu-id="e8424-216">Full backup start time: 22:00</span></span>
- <span data-ttu-id="e8424-217">Janela de tempo do backup completo: 6 horas</span><span class="sxs-lookup"><span data-stu-id="e8424-217">Full backup time window: 6 hours</span></span>

<span data-ttu-id="e8424-218">Isso significa que essa janela de backup disponíveis próxima da saudação é segunda-feira às 10 PM para 6 horas.</span><span class="sxs-lookup"><span data-stu-id="e8424-218">This means that hello next available backup window is Monday at 10 PM for 6 hours.</span></span> <span data-ttu-id="e8424-219">Nesse momento, o Backup Automatizado começará a fazer backup de seus bancos de dados um de cada vez.</span><span class="sxs-lookup"><span data-stu-id="e8424-219">At that time, Automated Backup will begin backing up your databases one at a time.</span></span>

<span data-ttu-id="e8424-220">Em seguida, na terça-feira às 22h por 6 horas, os backups completos de todos os bancos de dados serão iniciados novamente.</span><span class="sxs-lookup"><span data-stu-id="e8424-220">Then, on Tuesday at 10 for 6 hours, full backups of all databases will start again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e8424-221">Quando o agendamento de backups diários, é recomendável que você agende uma tooensure de janela de tempo ampla todos os bancos de dados podem ser feitos no momento.</span><span class="sxs-lookup"><span data-stu-id="e8424-221">When scheduling daily backups, it is recommended that you schedule a wide time window tooensure all databases can be backed up within this time.</span></span> <span data-ttu-id="e8424-222">Isso é especialmente importante no caso de Olá onde você tem uma grande quantidade de dados tooback backup.</span><span class="sxs-lookup"><span data-stu-id="e8424-222">This is especially important in hello case where you have a large amount of data tooback up.</span></span>

## <a name="configuration-in-hello-portal"></a><span data-ttu-id="e8424-223">Configuração no Portal de saudação</span><span class="sxs-lookup"><span data-stu-id="e8424-223">Configuration in hello Portal</span></span>

<span data-ttu-id="e8424-224">Você pode usar o hello tooconfigure portal do Azure Backup automatizado v2 durante o provisionamento ou para VMs existentes do SQL Server 2016.</span><span class="sxs-lookup"><span data-stu-id="e8424-224">You can use hello Azure portal tooconfigure Automated Backup v2 during provisioning or for existing SQL Server 2016 VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="e8424-225">Novas VMs</span><span class="sxs-lookup"><span data-stu-id="e8424-225">New VMs</span></span>

<span data-ttu-id="e8424-226">Use Olá tooconfigure portal do Azure Backup automatizado v2 quando você cria uma nova máquina SQL Server 2016 Virtual no modelo de implantação do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="e8424-226">Use hello Azure portal tooconfigure Automated Backup v2 when you create a new SQL Server 2016 Virtual Machine in hello Resource Manager deployment model.</span></span> 

<span data-ttu-id="e8424-227">Em Olá **configurações do SQL Server** folha, selecione **backup automatizado**.</span><span class="sxs-lookup"><span data-stu-id="e8424-227">In hello **SQL Server settings** blade, select **Automated backup**.</span></span> <span data-ttu-id="e8424-228">Olá, seguinte captura de tela de portal do Azure mostra Olá **Backup automatizado do SQL** folha.</span><span class="sxs-lookup"><span data-stu-id="e8424-228">hello following Azure portal screenshot shows hello **SQL Automated Backup** blade.</span></span>

![Configuração de Backup Automatizado do SQL no portal do Azure](./media/virtual-machines-windows-sql-automated-backup-v2/automated-backup-blade.png)

> [!NOTE]
> <span data-ttu-id="e8424-230">O Backup Automatizado v2 está desabilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="e8424-230">Automated Backup v2 is disabled by default.</span></span>

<span data-ttu-id="e8424-231">Para o contexto, consulte o tópico completo do hello sobre [Provisionando uma máquina virtual do SQL Server no Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="e8424-231">For context, see hello complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="e8424-232">VMs existentes</span><span class="sxs-lookup"><span data-stu-id="e8424-232">Existing VMs</span></span>

<span data-ttu-id="e8424-233">Para máquinas virtuais existentes do SQL Server, selecione sua máquina virtual do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e8424-233">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="e8424-234">Em seguida, selecione Olá **configuração do SQL Server** seção Olá **configurações** folha.</span><span class="sxs-lookup"><span data-stu-id="e8424-234">Then select hello **SQL Server configuration** section of hello **Settings** blade.</span></span>

![Backup Automatizado do SQL para VMs existentes](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration.png)

<span data-ttu-id="e8424-236">Em hello **configuração do SQL Server** folha, clique em hello **editar** botão Olá automatizada seção de backup.</span><span class="sxs-lookup"><span data-stu-id="e8424-236">In hello **SQL Server configuration** blade, click hello **Edit** button in hello Automated backup section.</span></span>

![Configurar o Backup Automatizado do SQL para VMs existentes](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration-edit.png)

<span data-ttu-id="e8424-238">Quando terminar, clique em Olá **Okey** botão na parte inferior de saudação da saudação **configuração do SQL Server** folha toosave suas alterações.</span><span class="sxs-lookup"><span data-stu-id="e8424-238">When finished, click hello **OK** button on hello bottom of hello **SQL Server configuration** blade toosave your changes.</span></span>

<span data-ttu-id="e8424-239">Se você estiver habilitando o Backup automatizado para Olá primeira vez, o Azure configura Olá IaaS do SQL Server Agent no plano de fundo de saudação.</span><span class="sxs-lookup"><span data-stu-id="e8424-239">If you are enabling Automated Backup for hello first time, Azure configures hello SQL Server IaaS Agent in hello background.</span></span> <span data-ttu-id="e8424-240">Durante esse tempo, Olá portal do Azure não pode mostrar que o Backup automatizado é configurado.</span><span class="sxs-lookup"><span data-stu-id="e8424-240">During this time, hello Azure portal might not show that Automated Backup is configured.</span></span> <span data-ttu-id="e8424-241">Aguarde alguns minutos para Olá agente toobe instalado, configurado.</span><span class="sxs-lookup"><span data-stu-id="e8424-241">Wait several minutes for hello agent toobe installed, configured.</span></span> <span data-ttu-id="e8424-242">Depois que hello Azure portal refletirá novas configurações de saudação.</span><span class="sxs-lookup"><span data-stu-id="e8424-242">After that hello Azure portal will reflect hello new settings.</span></span>

## <a name="configuration-with-powershell"></a><span data-ttu-id="e8424-243">Configuração com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="e8424-243">Configuration with PowerShell</span></span>

<span data-ttu-id="e8424-244">Você pode usar o PowerShell tooconfigure v2 de Backup automatizado.</span><span class="sxs-lookup"><span data-stu-id="e8424-244">You can use PowerShell tooconfigure Automated Backup v2.</span></span> <span data-ttu-id="e8424-245">Antes de começar, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="e8424-245">Before you begin, you must:</span></span>

- <span data-ttu-id="e8424-246">[Baixe e instale o hello Azure PowerShell mais recente](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="e8424-246">[Download and install hello latest Azure PowerShell](http://aka.ms/webpi-azps).</span></span>
- <span data-ttu-id="e8424-247">Abra o Windows PowerShell e associe-o à sua conta.</span><span class="sxs-lookup"><span data-stu-id="e8424-247">Open Windows PowerShell and associate it with your account.</span></span> <span data-ttu-id="e8424-248">Você pode fazer isso, seguindo as etapas de Olá Olá [configurar sua assinatura](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) seção Olá provisionamento tópico.</span><span class="sxs-lookup"><span data-stu-id="e8424-248">You can do this by following hello steps in hello [Configure your subscription](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) section of hello provisioning topic.</span></span>

### <a name="install-hello-sql-iaas-extension"></a><span data-ttu-id="e8424-249">Instalar Olá extensão SQL IaaS</span><span class="sxs-lookup"><span data-stu-id="e8424-249">Install hello SQL IaaS Extension</span></span>
<span data-ttu-id="e8424-250">Se você provisionar uma máquina de virtual do SQL Server do hello portal do Azure, Olá extensão de IaaS do SQL Server já deve ser instalado.</span><span class="sxs-lookup"><span data-stu-id="e8424-250">If you provisioned a SQL Server virtual machine from hello Azure portal, hello SQL Server IaaS Extension should already be installed.</span></span> <span data-ttu-id="e8424-251">Você pode determinar se ele é instalado em sua VM chamando **Get-AzureRmVM** comando e examinando Olá **extensões** propriedade.</span><span class="sxs-lookup"><span data-stu-id="e8424-251">You can determine if it is installed for your VM by calling **Get-AzureRmVM** command and examining hello **Extensions** property.</span></span>

```powershell
$vmname = "vmname"
$resourcegroupname = "resourcegroupname"

(Get-AzureRmVM -Name $vmname -ResourceGroupName $resourcegroupname).Extensions 
```

<span data-ttu-id="e8424-252">Se Olá extensão do SQL Server IaaS Agent estiver instalado, você verá que ele listado como "SqlIaaSAgent" ou "SQLIaaSExtension".</span><span class="sxs-lookup"><span data-stu-id="e8424-252">If hello SQL Server IaaS Agent extension is installed, you should see it listed as “SqlIaaSAgent” or “SQLIaaSExtension”.</span></span> <span data-ttu-id="e8424-253">**ProvisioningState** para extensão Olá também deve mostrar "Êxito".</span><span class="sxs-lookup"><span data-stu-id="e8424-253">**ProvisioningState** for hello extension should also show “Succeeded”.</span></span> 

<span data-ttu-id="e8424-254">Se ele não está instalado ou com falha toobe provisionado, você pode instalá-lo com hello comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="e8424-254">If it is not installed or failed toobe provisioned, you can install it with hello following command.</span></span> <span data-ttu-id="e8424-255">Adição toohello VM nome e grupo de recursos, você deve também especificar região hello (**$region**) localizado na sua VM.</span><span class="sxs-lookup"><span data-stu-id="e8424-255">In addition toohello VM name and resource group, you must also specify hello region (**$region**) that your VM is located in.</span></span>

```powershell
$region = “EASTUS2”
Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region 
```

### <span data-ttu-id="e8424-256"><a id="verifysettings"></a> Verificar as configurações atuais</span><span class="sxs-lookup"><span data-stu-id="e8424-256"><a id="verifysettings"></a> Verify current settings</span></span>
<span data-ttu-id="e8424-257">Se você habilitou o backup automatizado durante o provisionamento, você pode usar PowerShell toocheck sua configuração atual.</span><span class="sxs-lookup"><span data-stu-id="e8424-257">If you enabled automated backup during provisioning, you can use PowerShell toocheck your current configuration.</span></span> <span data-ttu-id="e8424-258">Executar Olá **Get-AzureRmVMSqlServerExtension** de comando e examine Olá **AutoBackupSettings** propriedade:</span><span class="sxs-lookup"><span data-stu-id="e8424-258">Run hello **Get-AzureRmVMSqlServerExtension** command and examine hello **AutoBackupSettings** property:</span></span>

```powershell
(Get-AzureRmVMSqlServerExtension -VMName $vmname -ResourceGroupName $resourcegroupname).AutoBackupSettings
```

<span data-ttu-id="e8424-259">Você deve obter a seguir toohello semelhante saída:</span><span class="sxs-lookup"><span data-stu-id="e8424-259">You should get output similar toohello following:</span></span>

```
Enable                      : True
EnableEncryption            : False
RetentionPeriod             : 30
StorageUrl                  : https://test.blob.core.windows.net/
StorageAccessKey            :  
Password                    : 
BackupSystemDbs             : False
BackupScheduleType          : Manual
FullBackupFrequency         : WEEKLY
FullBackupStartTime         : 2
FullBackupWindowHours       : 2
LogBackupFrequency          : 60
```

<span data-ttu-id="e8424-260">Se a saída mostra que **habilitar** está definido muito**False**, em seguida, você tem o backup automatizado tooenable.</span><span class="sxs-lookup"><span data-stu-id="e8424-260">If your output shows that **Enable** is set too**False**, then you have tooenable automated backup.</span></span> <span data-ttu-id="e8424-261">Olá boa notícia é que você habilita e configurar o Backup automatizado no hello mesma maneira.</span><span class="sxs-lookup"><span data-stu-id="e8424-261">hello good news is that you enable and configure Automated Backup in hello same way.</span></span> <span data-ttu-id="e8424-262">Consulte a próxima seção Olá para obter essas informações.</span><span class="sxs-lookup"><span data-stu-id="e8424-262">See hello next section for this information.</span></span>

> [!NOTE] 
> <span data-ttu-id="e8424-263">Se você verificar as configurações de saudação imediatamente depois de fazer uma alteração, é possível que você receberá novamente os valores de configuração antigo hello.</span><span class="sxs-lookup"><span data-stu-id="e8424-263">If you check hello settings immediately after making a change, it is possible that you will get back hello old configuration values.</span></span> <span data-ttu-id="e8424-264">Aguarde alguns minutos e verificar as configurações de saudação novamente toomake-se de que as alterações foram aplicadas.</span><span class="sxs-lookup"><span data-stu-id="e8424-264">Wait a few minutes and check hello settings again toomake sure that your changes were applied.</span></span>

### <a name="configure-automated-backup-v2"></a><span data-ttu-id="e8424-265">Configurar o Backup Automatizado v2</span><span class="sxs-lookup"><span data-stu-id="e8424-265">Configure Automated Backup v2</span></span>
<span data-ttu-id="e8424-266">Você pode usar PowerShell tooenable Backup automatizado, bem como toomodify sua configuração e o comportamento a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="e8424-266">You can use PowerShell tooenable Automated Backup as well as toomodify its configuration and behavior at any time.</span></span> 

<span data-ttu-id="e8424-267">Primeiro, selecione ou crie uma conta de armazenamento para Olá arquivos de backup.</span><span class="sxs-lookup"><span data-stu-id="e8424-267">First, select or create a storage account for hello backup files.</span></span> <span data-ttu-id="e8424-268">Olá script a seguir seleciona uma conta de armazenamento ou cria se ele não existe.</span><span class="sxs-lookup"><span data-stu-id="e8424-268">hello following script selects a storage account or creates it if it does not exist.</span></span>

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
> <span data-ttu-id="e8424-269">O Backup Automatizado não dá suporte ao armazenamento de backups no Armazenamento Premium, mas ele pode fazer backups de discos de VM que usam o Armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="e8424-269">Automated Backup does not support storing backups in premium storage, but it can take backups from VM disks which use Premium Storage.</span></span>

<span data-ttu-id="e8424-270">Em seguida, usar o hello **AzureRmVMSqlServerAutoBackupConfig novo** tooenable de comando e configurar backups de toostore configurações Olá Backup automatizado v2 na conta de armazenamento do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e8424-270">Then use hello **New-AzureRmVMSqlServerAutoBackupConfig** command tooenable and configure hello Automated Backup v2 settings toostore backups in hello Azure storage account.</span></span> <span data-ttu-id="e8424-271">Neste exemplo, os backups de saudação são definidos toobe mantido por 10 dias.</span><span class="sxs-lookup"><span data-stu-id="e8424-271">In this example, hello backups are set toobe retained for 10 days.</span></span> <span data-ttu-id="e8424-272">Os backups de banco de dados do sistema estão habilitados.</span><span class="sxs-lookup"><span data-stu-id="e8424-272">System database backups are enabled.</span></span> <span data-ttu-id="e8424-273">Os backups completos são agendados para serem realizados semanalmente com uma janela de tempo com início às 20h por duas horas.</span><span class="sxs-lookup"><span data-stu-id="e8424-273">Full backups are scheduled for weekly with a time window starting at 20:00 for two hours.</span></span> <span data-ttu-id="e8424-274">Os backups de log estão agendados para a cada 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="e8424-274">Log backups are scheduled for every 30 minutes.</span></span> <span data-ttu-id="e8424-275">Olá o segundo comando, **AzureRmVMSqlServerExtension conjunto**, Olá atualizações especificado VM do Azure com essas configurações.</span><span class="sxs-lookup"><span data-stu-id="e8424-275">hello second command, **Set-AzureRmVMSqlServerExtension**, updates hello specified Azure VM with these settings.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType Manual -FullBackupFrequency Weekly `
    -FullBackupStartHour 20 -FullBackupWindowInHours 2 `
    -LogBackupFrequencyInMinutes 30 

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname 
```

<span data-ttu-id="e8424-276">Ele pode levar vários tooinstall de minutos e configure Olá SQL Server IaaS Agent.</span><span class="sxs-lookup"><span data-stu-id="e8424-276">It could take several minutes tooinstall and configure hello SQL Server IaaS Agent.</span></span> 

<span data-ttu-id="e8424-277">criptografia de tooenable modificar Olá Olá de toopass script anterior **EnableEncryption** parâmetro junto com uma senha (cadeia de caracteres segura) para Olá **CertificatePassword** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="e8424-277">tooenable encryption, modify hello previous script toopass hello **EnableEncryption** parameter along with a password (secure string) for hello **CertificatePassword** parameter.</span></span> <span data-ttu-id="e8424-278">Olá script a seguir permite que as configurações de Backup automatizado Olá no exemplo anterior hello e adiciona a criptografia.</span><span class="sxs-lookup"><span data-stu-id="e8424-278">hello following script enables hello Automated Backup settings in hello previous example and adds encryption.</span></span>

```powershell
$password = "P@ssw0rd"
$encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -EnableEncryption -CertificatePassword $encryptionpassword `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType Manual -FullBackupFrequency Weekly `
    -FullBackupStartHour 20 -FullBackupWindowInHours 2 `
    -LogBackupFrequencyInMinutes 30 

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

<span data-ttu-id="e8424-279">tooconfirm suas configurações são aplicadas, [verificar a configuração de Backup automatizado Olá](#verifysettings).</span><span class="sxs-lookup"><span data-stu-id="e8424-279">tooconfirm your settings are applied, [verify hello Automated Backup configuration](#verifysettings).</span></span>

### <a name="disable-automated-backup"></a><span data-ttu-id="e8424-280">Desabilitar o Backup automatizado</span><span class="sxs-lookup"><span data-stu-id="e8424-280">Disable Automated Backup</span></span>
<span data-ttu-id="e8424-281">toodisable Backup automatizado, Olá execução mesmo script sem Olá **-habilitar** parâmetro toohello **AzureRmVMSqlServerAutoBackupConfig novo** comando.</span><span class="sxs-lookup"><span data-stu-id="e8424-281">toodisable Automated Backup, run hello same script without hello **-Enable** parameter toohello **New-AzureRmVMSqlServerAutoBackupConfig** command.</span></span> <span data-ttu-id="e8424-282">Olá ausência de saudação **-habilitar** recurso de saudação do parâmetro sinais Olá comando toodisable.</span><span class="sxs-lookup"><span data-stu-id="e8424-282">hello absence of hello **-Enable** parameter signals hello command toodisable hello feature.</span></span> <span data-ttu-id="e8424-283">Como com a instalação, pode levar vários minutos toodisable Backup automatizado.</span><span class="sxs-lookup"><span data-stu-id="e8424-283">As with installation, it can take several minutes toodisable Automated Backup.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

### <a name="example-script"></a><span data-ttu-id="e8424-284">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="e8424-284">Example script</span></span>
<span data-ttu-id="e8424-285">Olá script a seguir fornece um conjunto de variáveis que você pode personalizar tooenable e configurar o Backup automatizado para sua VM.</span><span class="sxs-lookup"><span data-stu-id="e8424-285">hello following script provides a set of variables that you can customize tooenable and configure Automated Backup for your VM.</span></span> <span data-ttu-id="e8424-286">No seu caso, talvez seja necessário toocustomize script de saudação com base nos seus requisitos.</span><span class="sxs-lookup"><span data-stu-id="e8424-286">In your case, you might need toocustomize hello script based on your requirements.</span></span> <span data-ttu-id="e8424-287">Por exemplo, você deve ter toomake alterações se desejar que o backup de saudação toodisable de bancos de dados do sistema ou habilitar a criptografia.</span><span class="sxs-lookup"><span data-stu-id="e8424-287">For example, you would have toomake changes if you wanted toodisable hello backup of system databases or enable encryption.</span></span>

```powershell
$vmname = "yourvmname"
$resourcegroupname = "vmresourcegroupname"
$region = “Azure region name such as EASTUS2”
$storage_accountname = “storageaccountname”
$storage_resourcegroupname = $resourcegroupname
$retentionperiod = 10
$backupscheduletype = "Manual"
$fullbackupfrequency = "Weekly"
$fullbackupstarthour = "20"
$fullbackupwindow = "2"
$logbackupfrequency = "30"

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
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType $backupscheduletype -FullBackupFrequency $fullbackupfrequency `
    -FullBackupStartHour $fullbackupstarthour -FullBackupWindowInHours $fullbackupwindow `
    -LogBackupFrequencyInMinutes $logbackupfrequency

# Apply hello Automated Backup settings toohello VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="e8424-288">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e8424-288">Next steps</span></span>
<span data-ttu-id="e8424-289">O Backup Automatizado v2 configura o Backup Gerenciado em VMs do Azure.</span><span class="sxs-lookup"><span data-stu-id="e8424-289">Automated Backup v2 configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="e8424-290">Portanto, é muito importante[documentação Olá Backup gerenciado](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand Olá comportamento e as implicações.</span><span class="sxs-lookup"><span data-stu-id="e8424-290">So it is important too[review hello documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello behavior and implications.</span></span>

<span data-ttu-id="e8424-291">Você pode encontrar backup adicional e restaurar a orientação do SQL Server em VMs do Azure no hello tópico a seguir: [de Backup e restauração do SQL Server em máquinas virtuais Azure](virtual-machines-windows-sql-backup-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="e8424-291">You can find additional backup and restore guidance for SQL Server on Azure VMs in hello following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span></span>

<span data-ttu-id="e8424-292">Para obter informações sobre outras tarefas de automação disponíveis, consulte [Extensão do agente IaaS do SQL Server](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="e8424-292">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="e8424-293">Para obter mais informações sobre como executar o SQL Server em VMs do Azure, consulte [Visão geral do SQL Server em Máquinas Virtuais do Azure](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e8424-293">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

