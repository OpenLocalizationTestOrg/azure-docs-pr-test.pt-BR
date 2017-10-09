---
title: aaaInstall v2 do servidor de Backup do Azure | Microsoft Docs
description: "O Servidor de Backup do Azure v2 oferece recursos aprimorados de backup para proteção de VMs, arquivos e pastas, cargas de trabalho e muito mais. Saiba como tooinstall ou atualização tooAzure v2 do servidor de Backup."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: masaran;markgal
ms.openlocfilehash: 5b1699dadd3a173f1c0ef91a1a600bc5e12f20ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-azure-backup-server-v2"></a><span data-ttu-id="07988-104">Instalar o Servidor de Backup do Azure v2</span><span class="sxs-lookup"><span data-stu-id="07988-104">Install Azure Backup Server v2</span></span>

<span data-ttu-id="07988-105">Servidor de Backup do Azure ajuda a proteger suas máquinas virtuais (VMs), cargas de trabalho, arquivos e pastas e muito mais.</span><span class="sxs-lookup"><span data-stu-id="07988-105">Azure Backup Server helps protect your virtual machines (VMs), workloads, files and folders, and more.</span></span> <span data-ttu-id="07988-106">O Servidor de Backup do Azure v2 se baseia no Servidor de Backup do Azure v1 e oferece novos recursos que não estão disponíveis em v1.</span><span class="sxs-lookup"><span data-stu-id="07988-106">Azure Backup Server v2 builds on Azure Backup Server v1, and gives you new features that are not available in v1.</span></span> <span data-ttu-id="07988-107">Para obter uma comparação de recursos entre v1 e v2, consulte [Matriz de proteção do Servidor de Backup do Azure](backup-mabs-protection-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="07988-107">For a comparison of features between v1 and v2, see [Azure Backup Server protection matrix](backup-mabs-protection-matrix.md).</span></span> 

<span data-ttu-id="07988-108">recursos adicionais de saudação no servidor de Backup v2 são uma atualização do servidor de Backup v1.</span><span class="sxs-lookup"><span data-stu-id="07988-108">hello additional features in Backup Server v2 are an upgrade from Backup Server v1.</span></span> <span data-ttu-id="07988-109">No entanto, o Servidor de Backup v1 não é um pré-requisito para instalar o Servidor de Backup v2.</span><span class="sxs-lookup"><span data-stu-id="07988-109">However, Backup Server v1 is not a prerequisite for installing Backup Server v2.</span></span> <span data-ttu-id="07988-110">Se você quiser tooupgrade do servidor de Backup v1 tooBackup v2 do servidor, instale v2 do servidor de Backup no servidor de proteção do servidor de Backup de saudação.</span><span class="sxs-lookup"><span data-stu-id="07988-110">If you want tooupgrade from Backup Server v1 tooBackup Server v2, install Backup Server v2 on hello Backup Server protection server.</span></span> <span data-ttu-id="07988-111">As suas configurações do Servidor de Backup existentes permanecem intactas.</span><span class="sxs-lookup"><span data-stu-id="07988-111">Your existing Backup Server settings remain intact.</span></span>

<span data-ttu-id="07988-112">Você pode instalar o Servidor de Backup v2 no Windows Server 2012 R2 ou Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="07988-112">You can install Backup Server v2 on Windows Server 2012 R2 or Windows Server 2016.</span></span> <span data-ttu-id="07988-113">tootake proveito dos novos recursos, como System Center 2016 Data Protection Manager moderno Backup armazenamento, você deve instalar o servidor de Backup v2 no Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="07988-113">tootake advantage of new features like System Center 2016 Data Protection Manager Modern Backup Storage, you must install Backup Server v2 on Windows Server 2016.</span></span> <span data-ttu-id="07988-114">Antes de você atualizar a instalação de tooor v2 do servidor de Backup, leia sobre Olá [os pré-requisitos de instalação](https://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites).</span><span class="sxs-lookup"><span data-stu-id="07988-114">Before you upgrade tooor install Backup Server v2, read about hello [installation prerequisites](https://docs.microsoft.com/system-center/dpm/install-dpm#setup-prerequisites).</span></span>

> [!NOTE]
> <span data-ttu-id="07988-115">Servidor de Backup do Azure tem Olá mesmo código de base como o System Center Data Protection Manager.</span><span class="sxs-lookup"><span data-stu-id="07988-115">Azure Backup Server has hello same code base as System Center Data Protection Manager.</span></span> <span data-ttu-id="07988-116">Backup v1 do servidor é o equivalente tooData Protection Manager 2012 R2 e v2 do servidor de Backup é equivalente tooData Protection Manager 2016.</span><span class="sxs-lookup"><span data-stu-id="07988-116">Backup Server v1 is equivalent tooData Protection Manager 2012 R2, and Backup Server v2 is equivalent tooData Protection Manager 2016.</span></span> <span data-ttu-id="07988-117">Este artigo ocasionalmente faz referência a documentação do Data Protection Manager hello.</span><span class="sxs-lookup"><span data-stu-id="07988-117">This article occasionally references hello Data Protection Manager documentation.</span></span>
>
>

## <a name="upgrade-backup-server-toov2"></a><span data-ttu-id="07988-118">Atualizar o servidor de Backup toov2</span><span class="sxs-lookup"><span data-stu-id="07988-118">Upgrade Backup Server toov2</span></span>
<span data-ttu-id="07988-119">tooupgrade do servidor de Backup v1 tooBackup v2 do servidor, verifique se a instalação tem atualizações Olá necessários:</span><span class="sxs-lookup"><span data-stu-id="07988-119">tooupgrade from Backup Server v1 tooBackup Server v2, make sure your installation has hello required updates:</span></span>

- <span data-ttu-id="07988-120">[Atualizar os agentes de proteção Olá](backup-mabs-upgrade-to-v2.md#update-the-dpm-protection-agent) em Olá servidores protegidos.</span><span class="sxs-lookup"><span data-stu-id="07988-120">[Update hello protection agents](backup-mabs-upgrade-to-v2.md#update-the-dpm-protection-agent) on hello protected servers.</span></span>
- <span data-ttu-id="07988-121">Atualize o Windows Server 2012 R2 tooWindows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="07988-121">Upgrade Windows Server 2012 R2 tooWindows Server 2016.</span></span>
- <span data-ttu-id="07988-122">Atualização do administrador remoto do Servidor de Backup do Azure em todos os servidores de produção.</span><span class="sxs-lookup"><span data-stu-id="07988-122">Upgrade Azure Backup Server Remote Administrator on all production servers.</span></span>
- <span data-ttu-id="07988-123">Certifique-se de que os backups são definidos toocontinue sem reiniciar o servidor de produção.</span><span class="sxs-lookup"><span data-stu-id="07988-123">Ensure that backups are set toocontinue without restarting your production server.</span></span>


### <a name="upgrade-steps-for-backup-server-v2"></a><span data-ttu-id="07988-124">Etapas de atualização para o Servidor de Backup v2</span><span class="sxs-lookup"><span data-stu-id="07988-124">Upgrade steps for Backup Server v2</span></span>

1. <span data-ttu-id="07988-125">Em Olá Centro de Download, [baixar o instalador de atualização Olá](https://go.microsoft.com/fwlink/?LinkId=626082).</span><span class="sxs-lookup"><span data-stu-id="07988-125">In hello Download Center, [download hello upgrade installer](https://go.microsoft.com/fwlink/?LinkId=626082).</span></span>

2. <span data-ttu-id="07988-126">Depois de extrair o Assistente de instalação de saudação, certifique-se de que **executar setup.exe** está selecionado e, em seguida, selecione **concluir**.</span><span class="sxs-lookup"><span data-stu-id="07988-126">After you extract hello setup wizard, make sure that **Execute setup.exe** is selected, and then select **Finish**.</span></span>

  ![Instalador de instalação - Execute a instalação](./media/backup-mabs-upgrade-to-v2/run-setup.png)

3. <span data-ttu-id="07988-128">No Assistente do servidor de Backup do Microsoft Azure hello, em **instalar**, selecione **Microsoft Azure Backup Server**.</span><span class="sxs-lookup"><span data-stu-id="07988-128">In hello Microsoft Azure Backup Server wizard, under **Install**, select **Microsoft Azure Backup Server**.</span></span>

  ![Instalador de instalação - Selecione instalação](./media/backup-mabs-upgrade-to-v2/mabs-installer-s1.png)

4. <span data-ttu-id="07988-130">Em Olá **bem-vindo** página, examine os avisos de saudação e, em seguida, selecione **próximo**.</span><span class="sxs-lookup"><span data-stu-id="07988-130">On hello **Welcome** page, review hello warnings, and then select **Next**.</span></span>

  ![Instalador de instalação - Página Inicial](./media/backup-mabs-upgrade-to-v2/mabs-installer-s2.png)

5. <span data-ttu-id="07988-132">Assistente de instalação Olá executa verificações de pré-requisitos toomake-se de que atualiza seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="07988-132">hello setup wizard performs prerequisite checks toomake sure your environment can upgrade.</span></span> <span data-ttu-id="07988-133">Em Olá **Prerequisite Checks** página, selecione **verificar**.</span><span class="sxs-lookup"><span data-stu-id="07988-133">On hello **Prerequisite Checks** page, select **Check**.</span></span>

  ![Instalador de instalação - página Verificações de Pré-requisitos](./media/backup-mabs-upgrade-to-v2/mabs-installer-s3-perform-checks.png)

6. <span data-ttu-id="07988-135">Verificações de pré-requisitos de saudação deve passar em seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="07988-135">Your environment must pass hello prerequisite checks.</span></span> <span data-ttu-id="07988-136">Se seu ambiente não passarem na verificação de hello, observe Olá problemas e corrigi-los.</span><span class="sxs-lookup"><span data-stu-id="07988-136">If your environment doesn't pass hello checks, note hello issues and fix them.</span></span> <span data-ttu-id="07988-137">Em seguida, selecione **Verificar Novamente**.</span><span class="sxs-lookup"><span data-stu-id="07988-137">Then, select **Check Again**.</span></span> <span data-ttu-id="07988-138">Depois de passar verificações de pré-requisitos hello, selecione **próximo**.</span><span class="sxs-lookup"><span data-stu-id="07988-138">After you pass hello prerequisite checks, select **Next**.</span></span>

  ![Instalador de instalação - Botão Verificar Novamente](./media/backup-mabs-upgrade-to-v2/mabs-installer-s4-pass-checks.png)

7. <span data-ttu-id="07988-140">Em Olá **configurações do SQL** página, selecione a opção de saudação relevantes para sua instalação do SQL e, em seguida, selecione **verificar e instalar**.</span><span class="sxs-lookup"><span data-stu-id="07988-140">On hello **SQL Settings** page, select hello relevant option for your SQL installation, and then select **Check and Install**.</span></span>

  ![Instalador de instalação - Página Configurações do SQL](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5-sql-settings.png)

  <span data-ttu-id="07988-142">verificações de saudação podem levar alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="07988-142">hello checks might take a few minutes.</span></span> <span data-ttu-id="07988-143">Quando as verificações de saudação são terminar, selecione **próximo**.</span><span class="sxs-lookup"><span data-stu-id="07988-143">When hello checks are finished, select **Next**.</span></span>

  ![Instalador de instalação - botão de Instalação e Verificação de Configurações do SQL](./media/backup-mabs-upgrade-to-v2/mabs-installer-s5a-check-and fix-settings.png)

8. <span data-ttu-id="07988-145">Em Olá **configurações de instalação** página, que qualquer local de toohello alterações em que o servidor de Backup está instalado, ou toohello local de rascunho.</span><span class="sxs-lookup"><span data-stu-id="07988-145">On hello **Installation Settings** page, make any changes toohello location where Backup Server is installed, or toohello Scratch Location.</span></span> <span data-ttu-id="07988-146">Selecione **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="07988-146">Select **Next**.</span></span>

  ![Instalador de instalação - página de Configurações de Instalação](./media/backup-mabs-upgrade-to-v2/mabs-installer-s6-installation-settings.png)

9. <span data-ttu-id="07988-148">Assistente de instalação Olá toofinish, selecione **concluir**.</span><span class="sxs-lookup"><span data-stu-id="07988-148">toofinish hello setup wizard, select **Finish**.</span></span>

  ![Instalador de instalação - Concluir](./media/backup-mabs-upgrade-to-v2/run-setup.png)



## <a name="add-storage-for-modern-backup-storage"></a><span data-ttu-id="07988-150">Adicionar armazenamento para Armazenamento de Backup moderno</span><span class="sxs-lookup"><span data-stu-id="07988-150">Add storage for Modern Backup Storage</span></span>

<span data-ttu-id="07988-151">eficiência de armazenamento de backup tooimprove, v2 do servidor de Backup adiciona suporte para volumes.</span><span class="sxs-lookup"><span data-stu-id="07988-151">tooimprove backup storage efficiency, Backup Server v2 adds support for volumes.</span></span> <span data-ttu-id="07988-152">Como o Servidor de Backup v1, o Servidor de Backup v2 oferece suporte a discos.</span><span class="sxs-lookup"><span data-stu-id="07988-152">Like Backup Server v1, Backup Server v2 supports disks.</span></span>

### <a name="add-volumes-and-disks"></a><span data-ttu-id="07988-153">Adicionar discos e volumes</span><span class="sxs-lookup"><span data-stu-id="07988-153">Add volumes and disks</span></span>
<span data-ttu-id="07988-154">Se você executar v2 do servidor de Backup no Windows Server 2016, você pode usar dados de backup de toostore de volumes.</span><span class="sxs-lookup"><span data-stu-id="07988-154">If you run Backup Server v2 on Windows Server 2016, you can use volumes toostore backup data.</span></span> <span data-ttu-id="07988-155">Os volumes oferecem economia de armazenamento e backups mais rápidos.</span><span class="sxs-lookup"><span data-stu-id="07988-155">Volumes offer storage savings and faster backups.</span></span> <span data-ttu-id="07988-156">Como os volumes são tooBackup novo servidor, você deve adicioná-los.</span><span class="sxs-lookup"><span data-stu-id="07988-156">Because volumes are new tooBackup Server, you must add them.</span></span> 

<span data-ttu-id="07988-157">Quando você adiciona um servidor de tooBackup de volume, você pode dar volume Olá um nome amigável.</span><span class="sxs-lookup"><span data-stu-id="07988-157">When you add a volume tooBackup Server, you can give hello volume a friendly name.</span></span> <span data-ttu-id="07988-158">Clique em Olá **nome amigável** coluna de volume Olá você deseja tooname.</span><span class="sxs-lookup"><span data-stu-id="07988-158">Click hello **Friendly Name** column of hello volume you want tooname.</span></span> <span data-ttu-id="07988-159">Você pode alterar o nome hello mais tarde, se necessário.</span><span class="sxs-lookup"><span data-stu-id="07988-159">You can change hello name later, if necessary.</span></span> <span data-ttu-id="07988-160">Você também pode usar o PowerShell tooadd ou alterar nomes amigáveis para volumes.</span><span class="sxs-lookup"><span data-stu-id="07988-160">You also can use PowerShell tooadd or change friendly names for volumes.</span></span>

<span data-ttu-id="07988-161">tooadd um volume no hello Console do administrador:</span><span class="sxs-lookup"><span data-stu-id="07988-161">tooadd a volume in hello Administrator Console:</span></span>

1. <span data-ttu-id="07988-162">No hello Console de administrador do servidor de Backup do Azure, selecione **gerenciamento** > **armazenamento em disco** > **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="07988-162">In hello Azure Backup Server Administrator Console, select **Management** > **Disk Storage** > **Add**.</span></span>

    ![Assistente de adicionar o armazenamento de disco Olá aberto](./media//backup-mabs-upgrade-to-v2/open-add-disk-storage-wizard.png)

    <span data-ttu-id="07988-164">Isso abre o Assistente de adicionar o armazenamento de disco de saudação.</span><span class="sxs-lookup"><span data-stu-id="07988-164">This opens hello Add Disk Storage wizard.</span></span>

2. <span data-ttu-id="07988-165">Em Olá **adicionar armazenamento em disco** página Olá **volumes disponíveis** caixa, selecione um volume e, em seguida, selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="07988-165">On hello **Add Disk Storage** page, in hello **Available volumes** box, select a volume, and then select **Add**.</span></span>
3. <span data-ttu-id="07988-166">Em Olá **selecionado volumes** caixa, digite um nome amigável para o volume de saudação e, em seguida, selecione **Okey**.</span><span class="sxs-lookup"><span data-stu-id="07988-166">In hello **Selected volumes** box, enter a friendly name for hello volume, and then select **OK**.</span></span>

      ![Assistente para Adicionar Armazenamento em Disco - Adicionar volume](./media/backup-mabs-upgrade-to-v2/add-volume.png)

  <span data-ttu-id="07988-168">Se você quiser tooadd um disco, disco Olá deve pertencer tooa grupo de proteção que tem armazenamento legado.</span><span class="sxs-lookup"><span data-stu-id="07988-168">If you want tooadd a disk, hello disk must belong tooa protection group that has legacy storage.</span></span> <span data-ttu-id="07988-169">Esses discos podem ser usados apenas para esses grupos de proteção.</span><span class="sxs-lookup"><span data-stu-id="07988-169">These disks can only be used for these protection groups.</span></span> <span data-ttu-id="07988-170">Se o servidor de Backup não tem fontes que têm proteção herdada, disco Olá não está listado.</span><span class="sxs-lookup"><span data-stu-id="07988-170">If Backup Server doesn't have sources that have legacy protection, hello disk isn't listed.</span></span>

  <span data-ttu-id="07988-171">Para obter mais informações sobre como adicionar discos, consulte [adicionando discos tooincrease herdados armazenamento](http://docs.microsoft.com/system-center/dpm/upgrade-to-dpm-2016#adding-disks-to-increase-legacy-storage).</span><span class="sxs-lookup"><span data-stu-id="07988-171">For more information about adding disks, see [Adding disks tooincrease legacy storage](http://docs.microsoft.com/system-center/dpm/upgrade-to-dpm-2016#adding-disks-to-increase-legacy-storage).</span></span> <span data-ttu-id="07988-172">Você não pode dar um nome amigável para um disco.</span><span class="sxs-lookup"><span data-stu-id="07988-172">You can't give a disk a friendly name.</span></span>


### <a name="assign-workloads-toovolumes"></a><span data-ttu-id="07988-173">Atribuir toovolumes de cargas de trabalho</span><span class="sxs-lookup"><span data-stu-id="07988-173">Assign workloads toovolumes</span></span>

<span data-ttu-id="07988-174">No servidor de Backup, você especificar que cargas de trabalho recebem toowhich volumes.</span><span class="sxs-lookup"><span data-stu-id="07988-174">In Backup Server, you specify which workloads are assigned toowhich volumes.</span></span> <span data-ttu-id="07988-175">Por exemplo, você pode definir volumes caros que dão suporte a um grande número de operações de entrada/saída por segundo (IOPS) toostore somente as cargas de trabalho que exigem backups frequentes, de alto volume.</span><span class="sxs-lookup"><span data-stu-id="07988-175">For example, you can set expensive volumes that support a high number of input/output operations per second (IOPS) toostore only workloads that require frequent, high-volume backups.</span></span> <span data-ttu-id="07988-176">Um exemplo é o SQL Server com logs de transação.</span><span class="sxs-lookup"><span data-stu-id="07988-176">An example is SQL Server with transaction logs.</span></span>

#### <a name="update-dpmdiskstorage"></a><span data-ttu-id="07988-177">Update-DPMDiskStorage</span><span class="sxs-lookup"><span data-stu-id="07988-177">Update-DPMDiskStorage</span></span>

<span data-ttu-id="07988-178">Propriedades de saudação tooupdate de um volume no pool de armazenamento Olá no servidor de Backup, use o cmdlet do PowerShell de saudação DPMDiskStorage de atualização.</span><span class="sxs-lookup"><span data-stu-id="07988-178">tooupdate hello properties of a volume in hello storage pool in Backup Server, use hello PowerShell cmdlet Update-DPMDiskStorage.</span></span>

<span data-ttu-id="07988-179">Sintaxe:</span><span class="sxs-lookup"><span data-stu-id="07988-179">Syntax:</span></span>

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

<span data-ttu-id="07988-180">Todas as alterações feitas por meio do PowerShell são refletidas na saudação da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="07988-180">All changes that you make by using PowerShell are reflected in hello UI.</span></span>


## <a name="protect-data-sources"></a><span data-ttu-id="07988-181">Proteger fontes de dados</span><span class="sxs-lookup"><span data-stu-id="07988-181">Protect data sources</span></span>
<span data-ttu-id="07988-182">toobegin proteção fontes de dados, crie um grupo de proteção.</span><span class="sxs-lookup"><span data-stu-id="07988-182">toobegin protecting data sources, create a protection group.</span></span> <span data-ttu-id="07988-183">Olá seguindo as etapas realce as alterações ou adições toohello assistente New Protection Group.</span><span class="sxs-lookup"><span data-stu-id="07988-183">hello following steps highlight changes or additions toohello New Protection Group wizard.</span></span>

<span data-ttu-id="07988-184">toocreate um grupo de proteção:</span><span class="sxs-lookup"><span data-stu-id="07988-184">toocreate a protection group:</span></span>

1. <span data-ttu-id="07988-185">No hello Console do administrador do servidor de Backup, selecione **proteção**.</span><span class="sxs-lookup"><span data-stu-id="07988-185">In hello Backup Server Administrator Console, select **Protection**.</span></span>

2. <span data-ttu-id="07988-186">Na faixa de opções de ferramenta hello, selecione **novo**.</span><span class="sxs-lookup"><span data-stu-id="07988-186">On hello tool ribbon, select **New**.</span></span>

    <span data-ttu-id="07988-187">Isso abre o Assistente para criar novo grupo de proteção de saudação.</span><span class="sxs-lookup"><span data-stu-id="07988-187">This opens hello Create New Protection Group wizard.</span></span>

  ![Assistente para Criar Novo Grupo de Proteção](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-1.png)

3. <span data-ttu-id="07988-189">Em Olá **bem-vindo** página, selecione **próximo**.</span><span class="sxs-lookup"><span data-stu-id="07988-189">On hello **Welcome** page, select **Next**.</span></span>
4. <span data-ttu-id="07988-190">Em Olá **Selecionar tipo de grupo de proteção** , selecione o tipo de saudação do grupo de proteção, você deseja toocreate e, em seguida, selecione **próximo**.</span><span class="sxs-lookup"><span data-stu-id="07988-190">On hello **Select Protection Group Type** page, select hello type of protection group you want toocreate, and then select **Next**.</span></span>

  ![Selecionar a página do Tipo de Grupo de Proteção](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-2.png)

5. <span data-ttu-id="07988-192">Em Olá **selecionar membros do grupo** página Olá **membros disponíveis** painel, membros de saudação com proteção agentes estão listados.</span><span class="sxs-lookup"><span data-stu-id="07988-192">On hello **Select Group Members** page, in hello **Available members** pane, hello members with protection agents are listed.</span></span> <span data-ttu-id="07988-193">Neste exemplo, selecione o volume D:\ e E:\ e adicioná-las toohello **membros selecionados** painel.</span><span class="sxs-lookup"><span data-stu-id="07988-193">For this example, select volume D:\ and E:\ and add them toohello **Selected members** pane.</span></span> <span data-ttu-id="07988-194">Selecione **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="07988-194">Select **Next**.</span></span>

  ![Selecionar a página Membros do Grupo](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-3.png)

6. <span data-ttu-id="07988-196">Em Olá **Selecionar método de proteção de dados** , insira um **nome do grupo de proteção**, selecione o método de proteção hello e, em seguida, selecione **próximo**.</span><span class="sxs-lookup"><span data-stu-id="07988-196">On hello **Select Data Protection Method** page, enter a **Protection group name**, select hello protection method, and then select **Next**.</span></span> <span data-ttu-id="07988-197">Se desejar que a proteção de curto prazo, você deve selecionar Olá **disco** método de backup.</span><span class="sxs-lookup"><span data-stu-id="07988-197">If you want short-term protection, you must select hello **Disk** backup method.</span></span>

  ![Selecionar a página Método de Proteção de Dados](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-4.png)

7. <span data-ttu-id="07988-199">Em Olá **especificar objetivos de curto prazo** página Detalhes Olá selecione **período de retenção** e **frequência de sincronização**.</span><span class="sxs-lookup"><span data-stu-id="07988-199">On hello **Specify Short-Term Goals** page, select hello details for **Retention range** and **Synchronization frequency**.</span></span> <span data-ttu-id="07988-200">Em seguida, selecione **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="07988-200">Then, select **Next**.</span></span> <span data-ttu-id="07988-201">Opcionalmente, o agendamento de saudação toochange para quando os pontos de recuperação são feitos, selecione **modificar**.</span><span class="sxs-lookup"><span data-stu-id="07988-201">Optionally, toochange hello schedule for when recovery points are taken, select **Modify**.</span></span>

  ![Especificar a página Objetivos de Curto Prazo](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-5.png)

8. <span data-ttu-id="07988-203">Em Olá **rever alocação do disco armazenamento** página, examine os detalhes sobre as fontes de dados de saudação selecionado, tamanho e valores para Olá espaço toobe provisionado e Olá volume de armazenamento de destino.</span><span class="sxs-lookup"><span data-stu-id="07988-203">On hello **Review Disk Storage Allocation** page, review details about hello data sources you selected, their size, and  values for hello space toobe provisioned and hello target storage volume.</span></span>

  ![Página Examinar Alocação de Armazenamento de Disco](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-6.png)

  <span data-ttu-id="07988-205">Volumes de armazenamento são baseados na alocação de volume de carga de trabalho de saudação (definida usando o PowerShell) e Olá armazenamento disponível.</span><span class="sxs-lookup"><span data-stu-id="07988-205">Storage volumes are based on hello workload volume allocation (set by using PowerShell) and hello available storage.</span></span> <span data-ttu-id="07988-206">Você pode alterar os volumes de armazenamento Olá selecionando outros volumes no menu suspenso de saudação.</span><span class="sxs-lookup"><span data-stu-id="07988-206">You can change hello storage volumes by selecting other volumes in hello drop-down menu.</span></span> <span data-ttu-id="07988-207">Se você alterar o valor Olá **armazenamento de destino**, Olá valor para **armazenamento em disco disponível** alterado dinamicamente valores de tooreflect em **espaço livre** e **Pela espaço**.</span><span class="sxs-lookup"><span data-stu-id="07988-207">If you change hello value for **Target Storage**, hello value for **Available disk storage** dynamically changes tooreflect values under **Free Space** and **Underprovisioned Space**.</span></span>

  <span data-ttu-id="07988-208">Se as fontes de dados de saudação o crescimento como planejado, Olá valor Olá **espaço pela** coluna em **armazenamento em disco disponível** reflete a quantidade de saudação de armazenamento adicional é necessário.</span><span class="sxs-lookup"><span data-stu-id="07988-208">If hello data sources grow as planned, hello value for hello **Underprovisioned Space** column in **Available disk storage** reflects hello amount of additional storage that's needed.</span></span> <span data-ttu-id="07988-209">Use este plano de toohelp valor suas necessidades de armazenamento de backups suaves.</span><span class="sxs-lookup"><span data-stu-id="07988-209">Use this value toohelp plan your storage needs for smooth backups.</span></span> <span data-ttu-id="07988-210">Não se o valor de saudação for zero, há nenhum problema potencial com o armazenamento em um futuro próximo Olá.</span><span class="sxs-lookup"><span data-stu-id="07988-210">If hello value is zero, there are no potential problems with storage in hello foreseeable future.</span></span> <span data-ttu-id="07988-211">Se o valor de saudação é um número diferente de zero, você não tem armazenamento suficiente alocado (com base em sua proteção hello e política de tamanho dos dados de seus membros protegidos).</span><span class="sxs-lookup"><span data-stu-id="07988-211">If hello value is a number other than zero, you do not have sufficient storage allocated  (based on your protection policy and hello data size of your protected members).</span></span>

  ![Armazenamento em disco subalocado](./media/backup-mabs-upgrade-to-v2/create-a-protection-group-7.png)

   <span data-ttu-id="07988-213">toofinish criar Assistente de saudação completa, grupo de proteção.</span><span class="sxs-lookup"><span data-stu-id="07988-213">toofinish creating your protection group, complete hello wizard.</span></span>

## <a name="migrate-legacy-storage-toomodern-backup-storage"></a><span data-ttu-id="07988-214">Migrar armazenamento legado tooModern o armazenamento de Backup</span><span class="sxs-lookup"><span data-stu-id="07988-214">Migrate legacy storage tooModern Backup Storage</span></span>
<span data-ttu-id="07988-215">Depois de atualizar instalação tooor v2 do servidor de Backup e atualização Olá tooWindows de sistema operacional Server 2016, atualize seu grupos de proteção toouse modernos o armazenamento de Backup.</span><span class="sxs-lookup"><span data-stu-id="07988-215">After you upgrade tooor install Backup Server v2 and upgrade hello operating system tooWindows Server 2016, update your protection groups toouse Modern Backup Storage.</span></span> <span data-ttu-id="07988-216">Por padrão, os grupos de proteção não são alterados.</span><span class="sxs-lookup"><span data-stu-id="07988-216">By default, protection groups are not changed.</span></span> <span data-ttu-id="07988-217">Eles continuam toofunction como eles foram configurados inicialmente.</span><span class="sxs-lookup"><span data-stu-id="07988-217">They continue toofunction as they were initially set up.</span></span> 

<span data-ttu-id="07988-218">Atualizar grupos de proteção toouse modernos o armazenamento de Backup é opcional.</span><span class="sxs-lookup"><span data-stu-id="07988-218">Updating protection groups toouse Modern Backup Storage is optional.</span></span> <span data-ttu-id="07988-219">grupo de proteção do tooupdate Olá, interrompa a proteção de todas as fontes de dados usando Olá manter opção dados.</span><span class="sxs-lookup"><span data-stu-id="07988-219">tooupdate hello protection group, stop protection of all data sources by using hello retain data option.</span></span> <span data-ttu-id="07988-220">Em seguida, adicione Olá dados fontes tooa novo grupo de proteção.</span><span class="sxs-lookup"><span data-stu-id="07988-220">Then, add hello data sources tooa new protection group.</span></span>

1. <span data-ttu-id="07988-221">No Console do administrador do hello, selecione Olá **proteção** recurso.</span><span class="sxs-lookup"><span data-stu-id="07988-221">In hello Administrator Console, select hello **Protection** feature.</span></span> <span data-ttu-id="07988-222">Em Olá **membro do grupo de proteção** lista, membro hello e, em seguida, selecione **parar proteção do membro**.</span><span class="sxs-lookup"><span data-stu-id="07988-222">In hello **Protection Group Member** list, right-click hello member, and then select **Stop protection of member**.</span></span>

  ![Interromper a proteção de membro](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-stop-protection1.png)

2. <span data-ttu-id="07988-224">Em Olá **remover do grupo** caixa de diálogo, examine Olá usado espaço em disco e Olá espaço livre para o pool de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="07988-224">In hello **Remove from Group** dialog box, review hello used disk space and hello available free space for hello storage pool.</span></span> <span data-ttu-id="07988-225">padrão de saudação é tooleave pontos de recuperação Olá no disco hello e permitir que eles tooexpire por sua política de retenção associado.</span><span class="sxs-lookup"><span data-stu-id="07988-225">hello default is tooleave hello recovery points on hello disk and allow them tooexpire per their associated retention policy.</span></span> <span data-ttu-id="07988-226">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="07988-226">Click **OK**.</span></span>

  <span data-ttu-id="07988-227">Se quiser que o pool do tooimmediately Olá retorno usado em disco espaço toohello livre de armazenamento, selecione Olá **excluir réplica no disco** dados backup da caixa de seleção toodelete saudação (e pontos de recuperação) associado a esse membro.</span><span class="sxs-lookup"><span data-stu-id="07988-227">If you want tooimmediately return hello used disk space toohello free storage pool, select hello **Delete replica on disk** check box toodelete hello backup data (and recovery points) associated with that member.</span></span>

  ![Remover da caixa de diálogo Grupo](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-retain-data.png)

3. <span data-ttu-id="07988-229">Crie um grupo de proteção que usa o Armazenamento de Backup Moderno.</span><span class="sxs-lookup"><span data-stu-id="07988-229">Create a protection group that uses Modern Backup Storage.</span></span> <span data-ttu-id="07988-230">Inclua fontes de dados de Saudação desprotegida.</span><span class="sxs-lookup"><span data-stu-id="07988-230">Include hello unprotected data sources.</span></span>


## <a name="add-disks-tooincrease-legacy-storage"></a><span data-ttu-id="07988-231">Adicionar discos tooincrease herdados armazenamento</span><span class="sxs-lookup"><span data-stu-id="07988-231">Add disks tooincrease legacy storage</span></span>

<span data-ttu-id="07988-232">Se você deseja que o armazenamento de toouse herdados com o servidor de Backup, talvez seja necessário armazenamento herdados do tooincrease tooadd discos.</span><span class="sxs-lookup"><span data-stu-id="07988-232">If you want toouse legacy storage with Backup Server, you might need tooadd disks tooincrease legacy storage.</span></span> 

<span data-ttu-id="07988-233">armazenamento em disco tooadd:</span><span class="sxs-lookup"><span data-stu-id="07988-233">tooadd disk storage:</span></span>

1. <span data-ttu-id="07988-234">No Console do administrador do hello, selecione **gerenciamento** > **armazenamento em disco** > **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="07988-234">In hello Administrator Console, select **Management** > **Disk Storage** > **Add**.</span></span>

    ![Adicionar caixa de diálogo de Armazenamento em Disco](http://docs.microsoft.com/system-center/dpm/media/upgrade-to-dpm-2016/dpm-2016-add-disk-storage.png)

4. <span data-ttu-id="07988-236">Em Olá **adicionar armazenamento em disco** caixa de diálogo, selecione **adicionar discos**.</span><span class="sxs-lookup"><span data-stu-id="07988-236">In hello **Add Disk Storage** dialog, select **Add disks**.</span></span>

5. <span data-ttu-id="07988-237">Na lista de saudação de discos disponíveis, selecione discos Olá deseja tooadd, selecione **adicionar**e, em seguida, selecione **Okey**.</span><span class="sxs-lookup"><span data-stu-id="07988-237">In hello list of available disks, select hello disks you want tooadd, select **Add**, and then select **OK**.</span></span>

## <a name="update-hello-data-protection-manager-protection-agent"></a><span data-ttu-id="07988-238">Atualizar o agente de proteção Olá Data Protection Manager</span><span class="sxs-lookup"><span data-stu-id="07988-238">Update hello Data Protection Manager protection agent</span></span>

<span data-ttu-id="07988-239">Servidor de backup usa o agente de proteção do System Center Data Protection Manager Olá para atualizações.</span><span class="sxs-lookup"><span data-stu-id="07988-239">Backup Server uses hello System Center Data Protection Manager protection agent for updates.</span></span> <span data-ttu-id="07988-240">Se você estiver atualizando um agente de proteção não está conectado toohello rede, você não pode usar o hello Data Protection Manager Administrator Console toocomplete uma atualização de agente conectado.</span><span class="sxs-lookup"><span data-stu-id="07988-240">If you are upgrading a protection agent that is not connected toohello network, you cannot use hello Data Protection Manager Administrator Console toocomplete a connected agent upgrade.</span></span> <span data-ttu-id="07988-241">Você deve atualizar o agente de proteção de saudação em um ambiente de domínio não ativo.</span><span class="sxs-lookup"><span data-stu-id="07988-241">You must upgrade hello protection agent in a nonactive domain environment.</span></span> <span data-ttu-id="07988-242">Até que o computador do cliente de saudação é rede toohello conectado, Olá que Data Protection Manager Administrator Console mostra essa atualização de agente de proteção hello está pendente.</span><span class="sxs-lookup"><span data-stu-id="07988-242">Until hello client computer is connected toohello network, hello Data Protection Manager Administrator Console shows that hello protection agent update is pending.</span></span>

<span data-ttu-id="07988-243">Olá seções a seguir descrevem como tooupdate agentes de proteção para computadores cliente que estão conectados e os computadores cliente que não estão conectados.</span><span class="sxs-lookup"><span data-stu-id="07988-243">hello following sections describe how tooupdate protection agents for client computers that are connected and client computers that are not connected.</span></span>

### <a name="update-a-protection-agent-for-a-connected-client-computer"></a><span data-ttu-id="07988-244">Atualizar um agente de proteção de um computador cliente conectado</span><span class="sxs-lookup"><span data-stu-id="07988-244">Update a protection agent for a connected client computer</span></span>

1. <span data-ttu-id="07988-245">No hello Console do administrador do servidor de Backup, selecione **gerenciamento** > **agentes**.</span><span class="sxs-lookup"><span data-stu-id="07988-245">In hello Backup Server Administrator Console, select **Management** > **Agents**.</span></span>

2. <span data-ttu-id="07988-246">No painel de exibição de hello, selecione os computadores cliente Olá para o qual você deseja que o agente de proteção de saudação tooupdate.</span><span class="sxs-lookup"><span data-stu-id="07988-246">In hello display pane, select hello client computers for which you want tooupdate hello protection agent.</span></span>

  > [!NOTE]
  > <span data-ttu-id="07988-247">Olá **atualizações de agente** coluna indica quando uma atualização do agente de proteção está disponível para cada computador protegido.</span><span class="sxs-lookup"><span data-stu-id="07988-247">hello **Agent Updates** column indicates when a protection agent update is available for each protected computer.</span></span> <span data-ttu-id="07988-248">Em Olá **ações** painel, Olá **atualização** ação está disponível somente quando um computador protegido está selecionado e as atualizações estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="07988-248">In hello **Actions** pane, hello **Update** action is available only when a protected computer is selected and updates are available.</span></span>
  >
  >

3. <span data-ttu-id="07988-249">tooinstall atualizado agentes de proteção em computadores Olá selecionado, Olá **ações** painel, selecione **atualização**.</span><span class="sxs-lookup"><span data-stu-id="07988-249">tooinstall updated protection agents on hello selected computers, in hello **Actions** pane, select **Update**.</span></span>

### <a name="update-a-protection-agent-on-a-client-computer-that-is-not-connected"></a><span data-ttu-id="07988-250">Atualizar um agente de proteção em um computador cliente que não está conectado</span><span class="sxs-lookup"><span data-stu-id="07988-250">Update a protection agent on a client computer that is not connected</span></span>

1. <span data-ttu-id="07988-251">No hello Console do administrador do servidor de Backup, selecione **gerenciamento** > **agentes**.</span><span class="sxs-lookup"><span data-stu-id="07988-251">In hello Backup Server Administrator Console, select **Management** > **Agents**.</span></span>

2. <span data-ttu-id="07988-252">No painel de exibição de hello, selecione os computadores cliente Olá para o qual você deseja que o agente de proteção de saudação tooupdate.</span><span class="sxs-lookup"><span data-stu-id="07988-252">In hello display pane, select hello client computers for which you want tooupdate hello protection agent.</span></span>

  > [!NOTE]
   > <span data-ttu-id="07988-253">Olá **atualizações de agente** coluna indica quando uma atualização do agente de proteção está disponível para cada computador protegido.</span><span class="sxs-lookup"><span data-stu-id="07988-253">hello **Agent Updates** column indicates when a protection agent update is available for each protected computer.</span></span> <span data-ttu-id="07988-254">Em Olá **ações** painel, Olá **atualização** ação não está disponível quando um computador protegido está selecionado, a menos que as atualizações estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="07988-254">In hello **Actions** pane, hello **Update** action is not available when a protected computer is selected unless updates are available.</span></span>
  >
  >

3. <span data-ttu-id="07988-255">tooinstall atualizado agentes de proteção nos computadores de saudação selecionada, selecionados **atualização**.</span><span class="sxs-lookup"><span data-stu-id="07988-255">tooinstall updated protection agents on hello selected computers, select **Update**.</span></span>

4. <span data-ttu-id="07988-256">Para um computador cliente que não está conectado rede toohello, até que o computador Olá é rede toohello conectado, Olá **Status do agente** coluna mostra um status de **atualização pendente**.</span><span class="sxs-lookup"><span data-stu-id="07988-256">For a client computer that is not connected toohello network, until hello computer is connected toohello network, hello **Agent Status** column shows a status of **Update Pending**.</span></span>

  <span data-ttu-id="07988-257">Depois que um computador cliente estiver conectado toohello rede, Olá **atualizações de agente** coluna para o computador de cliente Olá mostra um status de **atualização**.</span><span class="sxs-lookup"><span data-stu-id="07988-257">After a client computer is connected toohello network, hello **Agent Updates** column for hello client computer shows a status of **Updating**.</span></span>
  
### <a name="move-legacy-protection-groups-from-old-version-and-sync-hello-new-version-with-azure"></a><span data-ttu-id="07988-258">Mover herdado de grupos de proteção de uma versão antiga e sincronização Olá nova versão com o Azure</span><span class="sxs-lookup"><span data-stu-id="07988-258">Move legacy Protection groups from old version and sync hello new version with Azure</span></span>

<span data-ttu-id="07988-259">Depois que o servidor de Backup do Azure e hello SO são atualizadas, você está pronto tooprotect novas fontes de dados usando o armazenamento de Backup modernos.</span><span class="sxs-lookup"><span data-stu-id="07988-259">Once Azure Backup Server and hello OS are both updated, you are ready tooprotect new data sources using Modern Backup Storage.</span></span> <span data-ttu-id="07988-260">No entanto já protegido fontes de dados continuará toobe protegido na Olá herdado de maneira que estavam no servidor de Backup do Azure, mas todas as novas proteções usará o armazenamento de Backup modernos.</span><span class="sxs-lookup"><span data-stu-id="07988-260">However already protected data sources will continue toobe protected in hello legacy way as they were in Azure Backup Server but all new protection will use Modern Backup Storage.</span></span>

<span data-ttu-id="07988-261">Etapas a seguir são toomigrate fontes de dados do modo herdado proteção tooModern de armazenamento de backup.</span><span class="sxs-lookup"><span data-stu-id="07988-261">Below steps are toomigrate data sources from legacy  mode of protection tooModern backup storage.</span></span>

<span data-ttu-id="07988-262">• Adicione Olá novo volume toohello DPM pool de armazenamento e atribuir marcas de fonte de dados e nomes amigáveis, se desejado.</span><span class="sxs-lookup"><span data-stu-id="07988-262">• Add hello new volume(s) toohello DPM storage pool and assign friendly names and data source tags if desired.</span></span>
<span data-ttu-id="07988-263">• Para cada fonte de dados que está no modo herdado, interrompa a proteção de fontes de dados hello e "Reter dados protegidos".</span><span class="sxs-lookup"><span data-stu-id="07988-263">• For each data source that is in legacy mode, stop protection of hello data sources and “Retain Protected Data”.</span></span>  <span data-ttu-id="07988-264">Isso permitirá a recuperação de pontos de recuperação antigos após a migração.</span><span class="sxs-lookup"><span data-stu-id="07988-264">This will allow recovery of old recovery points after migration.</span></span>

<span data-ttu-id="07988-265">• Criar um novo grupo de proteção e selecione Olá fontes de dados que são armazenado usando o novo formato de toobe.</span><span class="sxs-lookup"><span data-stu-id="07988-265">• Create a new PG and select hello data sources that are toobe stored using new format.</span></span>
<span data-ttu-id="07988-266">• O DPM fará uma cópia da réplica Olá herdados do armazenamento de backup em Olá volume de armazenamento de Backup modernos localmente.</span><span class="sxs-lookup"><span data-stu-id="07988-266">• DPM will do a replica copy from hello legacy backup storage into hello Modern Backup Storage volume locally.</span></span>
<span data-ttu-id="07988-267">Observação: Isso será visto como um trabalho de operação pós-recuperação • Todos os novos pontos de sincronização e de recuperação serão então armazenados no armazenamento de backup moderno.</span><span class="sxs-lookup"><span data-stu-id="07988-267">Note: This will be seen as a post-recovery operation job • All new sync and recovery points will then be stored in Modern Backup Storage.</span></span>
<span data-ttu-id="07988-268">• Pontos de recuperação antigos serão removidos de limite expirar e, eventualmente, libere espaço em disco hello.</span><span class="sxs-lookup"><span data-stu-id="07988-268">• Old recovery points will be pruned out as they expire and eventually free up hello disk space.</span></span>
<span data-ttu-id="07988-269">• Depois que todos os volumes de saudação herdados são excluídos do armazenamento antigo hello, disco Olá pode ser removido do sistema de backup e hello do Azure.</span><span class="sxs-lookup"><span data-stu-id="07988-269">• Once all hello legacy volumes are deleted from hello old storage, hello disk can be removed from Azure backup and hello system.</span></span>
<span data-ttu-id="07988-270">• Fazer um backup de hello Azure DPMDB.</span><span class="sxs-lookup"><span data-stu-id="07988-270">• Take a backup of hello  Azure DPMDB.</span></span>

<span data-ttu-id="07988-271">Parte 2:-itens importantes > novo servidor de saudação precisará toobe mesmo nome como servidor de Backup do Azure original hello.</span><span class="sxs-lookup"><span data-stu-id="07988-271">Part 2: -Important items> hello new server will need toobe named same as hello original Azure Backup server.</span></span> <span data-ttu-id="07988-272">Não é possível alterar o nome de saudação do servidor de backup do Azure nova Olá se você deseja que o pool de armazenamento antigo toouse e pontos de recuperação de tooretain DPMDB - deve ter backup do DPMDB, pois ele será necessário toobe restaurado</span><span class="sxs-lookup"><span data-stu-id="07988-272">You cannot change hello name of hello new Azure backup server if you want toouse old storage pool and DPMDB tooretain recovery points -Must have backup of DPMDB  as it will need toobe restored</span></span>

1) <span data-ttu-id="07988-273">Desligamento Olá servidor de backup do Azure original ou tirá-lo durante a transmissão hello.</span><span class="sxs-lookup"><span data-stu-id="07988-273">Shutdown hello original Azure backup server or take it off hello wire.</span></span>
2) <span data-ttu-id="07988-274">Redefina conta da máquina Olá no active directory.</span><span class="sxs-lookup"><span data-stu-id="07988-274">Reset hello machine account in active directory.</span></span>
3) <span data-ttu-id="07988-275">Instale o Server 2016 no novo computador e nome-Olá o mesmo nome de máquina de servidor de Backup do Azure original hello.</span><span class="sxs-lookup"><span data-stu-id="07988-275">Install Server 2016 on new machine and name it hello same machine name as hello original Azure Backup server.</span></span>
4) <span data-ttu-id="07988-276">Unir Olá domínio</span><span class="sxs-lookup"><span data-stu-id="07988-276">Join hello Domain</span></span>
5) <span data-ttu-id="07988-277">Instalar o servidor de Backup do Azure V2 (mover discos do pool de armazenamento do DPM do servidor antigo e importar)</span><span class="sxs-lookup"><span data-stu-id="07988-277">Install Azure Backup server V2 (Move DPM Storage pool disks from old server and import)</span></span>
6) <span data-ttu-id="07988-278">Restaurar Olá DPMDB retirado do final da parte 2</span><span class="sxs-lookup"><span data-stu-id="07988-278">Restore hello DPMDB taken from end of part 2</span></span>
7) <span data-ttu-id="07988-279">Anexe armazenamento Olá da saudação original backup toohello novo servidor.</span><span class="sxs-lookup"><span data-stu-id="07988-279">Attach hello storage from hello original backup server toohello new server.</span></span>
8) <span data-ttu-id="07988-280">Na restauração do SQL Olá DPMDB</span><span class="sxs-lookup"><span data-stu-id="07988-280">From SQL Restore hello DPMDB</span></span>
9) <span data-ttu-id="07988-281">Na linha de comando de administrador no novo tooMicrosoft de cd do servidor do Azure Backup instalar local e a pasta bin</span><span class="sxs-lookup"><span data-stu-id="07988-281">From admin command line on new server cd tooMicrosoft Azure Backup install location and bin folder</span></span>

<span data-ttu-id="07988-282">Exemplo de caminho: C:\windows\system32>cd "c:\Program Files\Microsoft Azure Backup\DPM\DPM\bin\\</span><span class="sxs-lookup"><span data-stu-id="07988-282">Path example: C:\windows\system32>cd "c:\Program Files\Microsoft Azure Backup\DPM\DPM\bin\\</span></span>
<span data-ttu-id="07988-283">backup tooAzure execute DPMSYNC-SYNC</span><span class="sxs-lookup"><span data-stu-id="07988-283">tooAzure backup Run DPMSYNC -SYNC</span></span>

10) <span data-ttu-id="07988-284">Execute o DPMSYNC-SYNC Observação Se você tiver adicionado um novo pool de armazenamento do DPM toohello discos em vez de mover Olá antigas, execute DPMSYNC - Reallocatereplica</span><span class="sxs-lookup"><span data-stu-id="07988-284">Run DPMSYNC -SYNC Note If you have added NEW disks toohello DPM Storage pool instead of moving hello old ones, then run DPMSYNC -Reallocatereplica</span></span>

## <a name="new-powershell-cmdlets-in-v2"></a><span data-ttu-id="07988-285">Novo cmdlets do PowerShell em v2</span><span class="sxs-lookup"><span data-stu-id="07988-285">New PowerShell cmdlets in v2</span></span>

<span data-ttu-id="07988-286">Quando você instala o Servidor de Backup do Azure v2, dois novos cmdlets estão disponíveis:</span><span class="sxs-lookup"><span data-stu-id="07988-286">When you install Azure Backup Server v2, two new cmdlets are available:</span></span> 
* [<span data-ttu-id="07988-287">Mount-DPMRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="07988-287">Mount-DPMRecoveryPoint</span></span>](https://technet.microsoft.com/library/mt787159.aspx)
* [<span data-ttu-id="07988-288">Dismount-DPMRecoveryPoint</span><span class="sxs-lookup"><span data-stu-id="07988-288">Dismount-DPMRecoveryPoint</span></span>](https://technet.microsoft.com/library/mt787158.aspx)

## <a name="next-steps"></a><span data-ttu-id="07988-289">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="07988-289">Next steps</span></span>

<span data-ttu-id="07988-290">Saiba como tooprepare seu servidor ou começar a proteger uma carga de trabalho:</span><span class="sxs-lookup"><span data-stu-id="07988-290">Learn how tooprepare your server or begin protecting a workload:</span></span>
- [<span data-ttu-id="07988-291">Preparar as cargas de trabalho do Servidor de Backup</span><span class="sxs-lookup"><span data-stu-id="07988-291">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="07988-292">Usar o servidor de Backup tooback um servidor VMware</span><span class="sxs-lookup"><span data-stu-id="07988-292">Use Backup Server tooback up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="07988-293">Usar o servidor de Backup tooback o SQL Server</span><span class="sxs-lookup"><span data-stu-id="07988-293">Use Backup Server tooback up SQL Server</span></span>](backup-azure-sql-mabs.md)
- [<span data-ttu-id="07988-294">Usar o Armazenamento de Backup Moderno com o Servidor de Backup</span><span class="sxs-lookup"><span data-stu-id="07988-294">Use Modern Backup Storage with Backup Server</span></span>](backup-mabs-add-storage.md)

