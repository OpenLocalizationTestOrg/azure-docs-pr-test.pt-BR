---
title: "banco de dados do Analysis Services aaaAzure de backup e restauração | Microsoft Docs"
description: "Descreve como toobackup e restauração de um Azure Analysis Services banco de dados."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: cf0a782d237a95fdfa5ef628f998bd053aac0d9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="backup-and-restore"></a><span data-ttu-id="05863-103">Backup e restauração</span><span class="sxs-lookup"><span data-stu-id="05863-103">Backup and restore</span></span>

<span data-ttu-id="05863-104">Fazendo backup de bancos de dados de modelo de tabela no Azure Analysis Services é muito Olá mesmo que o Analysis Services no local.</span><span class="sxs-lookup"><span data-stu-id="05863-104">Backing up tabular model databases in Azure Analysis Services is much hello same as for on-premises Analysis Services.</span></span> <span data-ttu-id="05863-105">Olá principal diferença é onde você armazena seus arquivos de backup.</span><span class="sxs-lookup"><span data-stu-id="05863-105">hello primary difference is where you store your backup files.</span></span> <span data-ttu-id="05863-106">Arquivos de backup devem ser salvo tooa contêiner em uma [conta de armazenamento do Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="05863-106">Backup files must be saved tooa container in an [Azure storage account](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="05863-107">Você pode usar uma conta de armazenamento e um contêiner que já existam ou eles podem ser criados ao definir as configurações de armazenamento para o seu servidor.</span><span class="sxs-lookup"><span data-stu-id="05863-107">You can use a storage account and container you already have, or they can be created when configuring storage settings for your server.</span></span>

> [!NOTE]
> <span data-ttu-id="05863-108">A criação de uma conta de armazenamento pode resultar em um novo serviço faturável.</span><span class="sxs-lookup"><span data-stu-id="05863-108">Creating a storage account can result in a new billable service.</span></span> <span data-ttu-id="05863-109">mais, consulte toolearn [preços de armazenamento do Azure](https://azure.microsoft.com/pricing/details/storage/blobs/).</span><span class="sxs-lookup"><span data-stu-id="05863-109">toolearn more, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/blobs/).</span></span>
> 
> 

<span data-ttu-id="05863-110">Os backups são salvos com uma extensão abf.</span><span class="sxs-lookup"><span data-stu-id="05863-110">Backups are saved with an abf extension.</span></span> <span data-ttu-id="05863-111">Para modelos tabular na memória, ambos os dados de modelo e metadados são armazenados.</span><span class="sxs-lookup"><span data-stu-id="05863-111">For in-memory tabular models, both model data and metadata are stored.</span></span> <span data-ttu-id="05863-112">Para modelos tabulares do DirectQuery, somente os metadados do modelo são armazenados.</span><span class="sxs-lookup"><span data-stu-id="05863-112">For DirectQuery tabular models, only model metadata is stored.</span></span> <span data-ttu-id="05863-113">Os backups podem ser compactados e criptografados, dependendo das opções Olá selecionadas.</span><span class="sxs-lookup"><span data-stu-id="05863-113">Backups can be compressed and encrypted, depending on hello options you choose.</span></span> 



## <a name="configure-storage-settings"></a><span data-ttu-id="05863-114">Definir as configurações de armazenamento</span><span class="sxs-lookup"><span data-stu-id="05863-114">Configure storage settings</span></span>
<span data-ttu-id="05863-115">Antes de fazer backup, você precisa tooconfigure configurações de armazenamento para o servidor.</span><span class="sxs-lookup"><span data-stu-id="05863-115">Before backing up, you need tooconfigure storage settings for your server.</span></span>


### <a name="tooconfigure-storage-settings"></a><span data-ttu-id="05863-116">configurações de armazenamento tooconfigure</span><span class="sxs-lookup"><span data-stu-id="05863-116">tooconfigure storage settings</span></span>
1.  <span data-ttu-id="05863-117">No portal do n Azure > **Configurações**, clique em **Backup**.</span><span class="sxs-lookup"><span data-stu-id="05863-117">In Azure portal > **Settings**, click **Backup**.</span></span>

    ![Backups em Configurações](./media/analysis-services-backup/aas-backup-backups.png)

2.  <span data-ttu-id="05863-119">Clique em **Habilitado** e, em seguida, clique em **Configurações de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="05863-119">Click **Enabled**, then click **Storage Settings**.</span></span>

    ![Habilitar](./media/analysis-services-backup/aas-backup-enable.png)

3. <span data-ttu-id="05863-121">Selecione uma conta de armazenamento ou crie uma nova.</span><span class="sxs-lookup"><span data-stu-id="05863-121">Select your storage account or create a new one.</span></span>

4. <span data-ttu-id="05863-122">Selecione um contêiner ou crie um novo.</span><span class="sxs-lookup"><span data-stu-id="05863-122">Select a container or create a new one.</span></span>

    ![Selecione o contêiner](./media/analysis-services-backup/aas-backup-container.png)

5. <span data-ttu-id="05863-124">Salve as configurações de backup.</span><span class="sxs-lookup"><span data-stu-id="05863-124">Save your backup settings.</span></span>

    ![Salvar as configurações de backup](./media/analysis-services-backup/aas-backup-save.png)

## <a name="backup"></a><span data-ttu-id="05863-126">Backup</span><span class="sxs-lookup"><span data-stu-id="05863-126">Backup</span></span>

### <a name="toobackup-by-using-ssms"></a><span data-ttu-id="05863-127">toobackup usando o SSMS</span><span class="sxs-lookup"><span data-stu-id="05863-127">toobackup by using SSMS</span></span>

1. <span data-ttu-id="05863-128">No SSMS, clique com o botão direito do mouse em um banco de dados > **Backup**.</span><span class="sxs-lookup"><span data-stu-id="05863-128">In SSMS, right-click a database > **Back Up**.</span></span>

2. <span data-ttu-id="05863-129">Em **Banco de Dados de Backup** > **Arquivo de Backup**, clique em **Navegar**.</span><span class="sxs-lookup"><span data-stu-id="05863-129">In **Backup Database** > **Backup file**, click **Browse**.</span></span>

3. <span data-ttu-id="05863-130">Em Olá **salvar arquivo como** caixa de diálogo, verifique se o caminho da pasta hello e, em seguida, digite um nome para o arquivo de backup hello.</span><span class="sxs-lookup"><span data-stu-id="05863-130">In hello **Save file as** dialog, verify hello folder path, and then type a name for hello backup file.</span></span> 

4. <span data-ttu-id="05863-131">Em Olá **banco de dados de Backup** caixa de diálogo, selecione as opções.</span><span class="sxs-lookup"><span data-stu-id="05863-131">In hello **Backup Database** dialog, select options.</span></span>

    <span data-ttu-id="05863-132">**Permitir que o arquivo substituir** -Selecione esta opção toooverwrite arquivos de backup Olá mesmo nome.</span><span class="sxs-lookup"><span data-stu-id="05863-132">**Allow file overwrite** - Select this option toooverwrite backup files of hello same name.</span></span> <span data-ttu-id="05863-133">Se essa opção não estiver selecionada, arquivo hello você está salvando não pode ter Olá mesmo nome como um arquivo que já existe no hello mesmo local.</span><span class="sxs-lookup"><span data-stu-id="05863-133">If this option is not selected, hello file you are saving cannot have hello same name as a file that already exists in hello same location.</span></span>

    <span data-ttu-id="05863-134">**Aplicar compactação** -Selecione esta opção toocompress Olá backup de arquivo.</span><span class="sxs-lookup"><span data-stu-id="05863-134">**Apply compression** - Select this option toocompress hello backup file.</span></span> <span data-ttu-id="05863-135">Arquivos de backup compactados economizam espaço em disco mas exigem uma utilização de CPU ligeiramente maior.</span><span class="sxs-lookup"><span data-stu-id="05863-135">Compressed backup files save disk space, but require slightly higher CPU utilization.</span></span> 

    <span data-ttu-id="05863-136">**Criptografar arquivo de backup** -Selecione esta opção tooencrypt Olá backup de arquivo.</span><span class="sxs-lookup"><span data-stu-id="05863-136">**Encrypt backup file** - Select this option tooencrypt hello backup file.</span></span> <span data-ttu-id="05863-137">Essa opção requer um arquivo de backup de saudação do toosecure senha fornecida pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="05863-137">This option requires a user-supplied password toosecure hello backup file.</span></span> <span data-ttu-id="05863-138">senha Olá impede a leitura dos dados de backup Olá qualquer outro meio de uma operação de restauração.</span><span class="sxs-lookup"><span data-stu-id="05863-138">hello password prevents reading of hello backup data any other means than a restore operation.</span></span> <span data-ttu-id="05863-139">Se você escolher tooencrypt backups, armazene a senha de saudação em um local seguro.</span><span class="sxs-lookup"><span data-stu-id="05863-139">If you choose tooencrypt backups, store hello password in a safe location.</span></span>

5. <span data-ttu-id="05863-140">Clique em **Okey** toocreate e salve o arquivo de backup hello.</span><span class="sxs-lookup"><span data-stu-id="05863-140">Click **OK** toocreate and save hello backup file.</span></span>


### <a name="powershell"></a><span data-ttu-id="05863-141">PowerShell</span><span class="sxs-lookup"><span data-stu-id="05863-141">PowerShell</span></span>
<span data-ttu-id="05863-142">Use o cmdlet [Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet).</span><span class="sxs-lookup"><span data-stu-id="05863-142">Use [Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet) cmdlet.</span></span>

## <a name="restore"></a><span data-ttu-id="05863-143">Restaurar</span><span class="sxs-lookup"><span data-stu-id="05863-143">Restore</span></span>
<span data-ttu-id="05863-144">Ao restaurar, o arquivo de backup deve ser na conta de armazenamento Olá que você configurou para seu servidor.</span><span class="sxs-lookup"><span data-stu-id="05863-144">When restoring, your backup file must be in hello storage account you've configured for your server.</span></span> <span data-ttu-id="05863-145">Se você precisar toomove um arquivo de backup de uma conta de armazenamento local local tooyour, use [Microsoft Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) ou hello [AzCopy](../storage/common/storage-use-azcopy.md) utilitário de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="05863-145">If you need toomove a backup file from an on-premises location tooyour storage account, use [Microsoft Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) or hello [AzCopy](../storage/common/storage-use-azcopy.md) command-line utility.</span></span> 



> [!NOTE]
> <span data-ttu-id="05863-146">Se você estiver restaurando a partir de um servidor local, você deve remover todos os usuários de domínio de saudação de funções de saudação do modelo e adicioná-los fazer toohello funções como usuários do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="05863-146">If you're restoring from an on-premises server, you must remove all hello domain users from hello model's roles and add them back toohello roles as Azure Active Directory users.</span></span>
> 
> 

### <a name="toorestore-by-using-ssms"></a><span data-ttu-id="05863-147">toorestore usando o SSMS</span><span class="sxs-lookup"><span data-stu-id="05863-147">toorestore by using SSMS</span></span>

1. <span data-ttu-id="05863-148">No SSMS, clique com o botão direito do mouse em um banco de dados > **Restaurar**.</span><span class="sxs-lookup"><span data-stu-id="05863-148">In SSMS, right-click a database > **Restore**.</span></span>

2. <span data-ttu-id="05863-149">Em Olá **banco de dados de Backup** caixa de diálogo, na **arquivo de Backup**, clique em **procurar**.</span><span class="sxs-lookup"><span data-stu-id="05863-149">In hello **Backup Database** dialog, in **Backup file**, click **Browse**.</span></span>

3. <span data-ttu-id="05863-150">Em Olá **localizar arquivos de banco de dados** caixa de diálogo, o arquivo hello selecione desejado toorestore.</span><span class="sxs-lookup"><span data-stu-id="05863-150">In hello **Locate Database Files** dialog, select hello file you want toorestore.</span></span>

4. <span data-ttu-id="05863-151">Em **restaurar banco de dados**, selecione o banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="05863-151">In **Restore database**, select hello database.</span></span>

5. <span data-ttu-id="05863-152">Especifique as opções.</span><span class="sxs-lookup"><span data-stu-id="05863-152">Specify options.</span></span> <span data-ttu-id="05863-153">Opções de segurança devem coincidir com as opções de backup Olá usado durante o backup.</span><span class="sxs-lookup"><span data-stu-id="05863-153">Security options must match hello backup options you used when backing up.</span></span>


### <a name="powershell"></a><span data-ttu-id="05863-154">PowerShell</span><span class="sxs-lookup"><span data-stu-id="05863-154">PowerShell</span></span>

<span data-ttu-id="05863-155">Use o cmdlet [Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet).</span><span class="sxs-lookup"><span data-stu-id="05863-155">Use [Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet) cmdlet.</span></span>


## <a name="related-information"></a><span data-ttu-id="05863-156">Informações relacionadas</span><span class="sxs-lookup"><span data-stu-id="05863-156">Related information</span></span>

[<span data-ttu-id="05863-157">Contas de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="05863-157">Azure storage accounts</span></span>](../storage/common/storage-create-storage-account.md)  
<span data-ttu-id="05863-158">[Alta disponibilidade](analysis-services-bcdr.md)   </span><span class="sxs-lookup"><span data-stu-id="05863-158">[High availability](analysis-services-bcdr.md)   </span></span>  
[<span data-ttu-id="05863-159">Gerenciar Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="05863-159">Manage Azure Analysis Services</span></span>](analysis-services-manage.md)
