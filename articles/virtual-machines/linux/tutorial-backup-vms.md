---
title: Fazer backup de VMs do Linux do Azure | Microsoft Docs
description: Proteja as VMs do Linux fazendo backup delas com o Backup do Azure.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/27/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 7c00392d5185a2f067f2ee2717529dcbde1e71f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-linux--virtual-machines-in-azure"></a><span data-ttu-id="fbacf-103">Fazer backup de máquinas virtuais do Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="fbacf-103">Back up Linux  virtual machines in Azure</span></span>

<span data-ttu-id="fbacf-104">Você pode proteger seus dados fazendo backups em intervalos regulares.</span><span class="sxs-lookup"><span data-stu-id="fbacf-104">You can protect your data by taking backups at regular intervals.</span></span> <span data-ttu-id="fbacf-105">O Backup do Azure cria pontos de recuperação que são armazenados em cofres de recuperação com redundância geográfica.</span><span class="sxs-lookup"><span data-stu-id="fbacf-105">Azure Backup creates recovery points that are stored in geo-redundant recovery vaults.</span></span> <span data-ttu-id="fbacf-106">Quando você restaurar de um ponto de recuperação, você poderá restaurar Olá VM inteira ou apenas determinados arquivos.</span><span class="sxs-lookup"><span data-stu-id="fbacf-106">When you restore from a recovery point, you can restore hello whole VM or just specific files.</span></span> <span data-ttu-id="fbacf-107">Este artigo explica como toorestore um único arquivo tooa nginx de VM do Linux em execução.</span><span class="sxs-lookup"><span data-stu-id="fbacf-107">This article explains how toorestore a single file tooa Linux VM running nginx.</span></span> <span data-ttu-id="fbacf-108">Se você ainda não tiver um toouse VM, você pode criar um usando Olá [Linux quickstart](quick-create-cli.md).</span><span class="sxs-lookup"><span data-stu-id="fbacf-108">If you don't already have a VM toouse, you can create one using hello [Linux quickstart](quick-create-cli.md).</span></span> <span data-ttu-id="fbacf-109">Neste tutorial, você aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="fbacf-109">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fbacf-110">Criar um backup de uma VM</span><span class="sxs-lookup"><span data-stu-id="fbacf-110">Create a backup of a VM</span></span>
> * <span data-ttu-id="fbacf-111">Agendar um backup diário</span><span class="sxs-lookup"><span data-stu-id="fbacf-111">Schedule a daily backup</span></span>
> * <span data-ttu-id="fbacf-112">Restaurar um arquivo de um backup</span><span class="sxs-lookup"><span data-stu-id="fbacf-112">Restore a file from a backup</span></span>



## <a name="backup-overview"></a><span data-ttu-id="fbacf-113">Visão geral do backup</span><span class="sxs-lookup"><span data-stu-id="fbacf-113">Backup overview</span></span>

<span data-ttu-id="fbacf-114">Quando Olá serviço Backup do Azure inicia um backup, ela aciona Olá extensão backup tootake um instantâneo point-in-time.</span><span class="sxs-lookup"><span data-stu-id="fbacf-114">When hello Azure Backup service initiates a backup, it triggers hello backup extension tootake a point-in-time snapshot.</span></span> <span data-ttu-id="fbacf-115">saudação de serviço de Backup do Azure usa Olá _VMSnapshotLinux_ extensão no Linux.</span><span class="sxs-lookup"><span data-stu-id="fbacf-115">hello Azure Backup service uses hello _VMSnapshotLinux_ extension in Linux.</span></span> <span data-ttu-id="fbacf-116">extensão de saudação é instalado durante o primeiro backup VM Olá se Olá VM está em execução.</span><span class="sxs-lookup"><span data-stu-id="fbacf-116">hello extension is installed during hello first VM backup if hello VM is running.</span></span> <span data-ttu-id="fbacf-117">Se hello VM não está em execução, Olá serviço de Backup tira um instantâneo de saudação armazenamento subjacente (já que nenhum aplicativo grava ocorre durante a saudação que VM estiver parada).</span><span class="sxs-lookup"><span data-stu-id="fbacf-117">If hello VM is not running, hello Backup service takes a snapshot of hello underlying storage (since no application writes occur while hello VM is stopped).</span></span>

<span data-ttu-id="fbacf-118">Por padrão, Backup do Azure usa um backup consistente de sistema de arquivos para a VM do Linux, mas pode ser configurado tootake [backup consistente de aplicativo usando o script de pré e pós-framework](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent).</span><span class="sxs-lookup"><span data-stu-id="fbacf-118">By default, Azure Backup takes a file system consistent backup for Linux VM but it can be configured tootake [application consistent backup using pre-script and post-script framework](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent).</span></span> <span data-ttu-id="fbacf-119">Depois de saudação serviço Backup do Azure usa instantâneo hello, dados saudação são toohello transferidos cofre.</span><span class="sxs-lookup"><span data-stu-id="fbacf-119">Once hello Azure Backup service takes hello snapshot, hello data is transferred toohello vault.</span></span> <span data-ttu-id="fbacf-120">toomaximize eficiência, o serviço de saudação identifica e transfere apenas os blocos de dados que foram alterados desde o backup anterior de saudação hello.</span><span class="sxs-lookup"><span data-stu-id="fbacf-120">toomaximize efficiency, hello service identifies and transfers only hello blocks of data that have changed since hello previous backup.</span></span>

<span data-ttu-id="fbacf-121">Quando a transferência de dados de saudação for concluída, Olá é removido e um ponto de recuperação é criado.</span><span class="sxs-lookup"><span data-stu-id="fbacf-121">When hello data transfer is complete, hello snapshot is removed and a recovery point is created.</span></span>


## <a name="create-a-backup"></a><span data-ttu-id="fbacf-122">Criar um backup</span><span class="sxs-lookup"><span data-stu-id="fbacf-122">Create a backup</span></span>
<span data-ttu-id="fbacf-123">Crie um simple agendado diariamente backup tooa Cofre de serviços de recuperação.</span><span class="sxs-lookup"><span data-stu-id="fbacf-123">Create a simple scheduled daily backup tooa Recovery Services Vault.</span></span> 

1. <span data-ttu-id="fbacf-124">Entrar toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="fbacf-124">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="fbacf-125">No menu Olá Olá esquerda, selecione **máquinas virtuais**.</span><span class="sxs-lookup"><span data-stu-id="fbacf-125">In hello menu on hello left, select **Virtual machines**.</span></span> 
3. <span data-ttu-id="fbacf-126">Olá, selecione lista tooback uma VM para cima.</span><span class="sxs-lookup"><span data-stu-id="fbacf-126">From hello list, select a VM tooback up.</span></span>
4. <span data-ttu-id="fbacf-127">Na folha VM hello, em Olá **configurações** seção, clique em **Backup**.</span><span class="sxs-lookup"><span data-stu-id="fbacf-127">On hello VM blade, in hello **Settings** section, click **Backup**.</span></span> <span data-ttu-id="fbacf-128">Olá **habilitar backup** folha é aberta.</span><span class="sxs-lookup"><span data-stu-id="fbacf-128">hello **Enable backup** blade opens.</span></span>
5. <span data-ttu-id="fbacf-129">Em **Cofre de serviços de recuperação**, clique em **criar novo** e fornecer nome hello novo cofre de saudação.</span><span class="sxs-lookup"><span data-stu-id="fbacf-129">In **Recovery Services vault**, click **Create new** and provide hello name for hello new vault.</span></span> <span data-ttu-id="fbacf-130">Um novo cofre é criado no hello mesmo grupo de recursos e o local da máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="fbacf-130">A new vault is created in hello same Resource Group and location as hello virtual machine.</span></span>
6. <span data-ttu-id="fbacf-131">Clique em **Política de backup**.</span><span class="sxs-lookup"><span data-stu-id="fbacf-131">Click **Backup policy**.</span></span> <span data-ttu-id="fbacf-132">Neste exemplo, lembre-Olá padrões e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="fbacf-132">For this example, keep hello defaults and click **OK**.</span></span>
7. <span data-ttu-id="fbacf-133">Em Olá **habilitar backup** folha, clique em **habilitar Backup**.</span><span class="sxs-lookup"><span data-stu-id="fbacf-133">On hello **Enable backup** blade, click **Enable Backup**.</span></span> <span data-ttu-id="fbacf-134">Isso cria um backup diário com base no agendamento de padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="fbacf-134">This creates a daily backup based on hello default schedule.</span></span>
10. <span data-ttu-id="fbacf-135">toocreate um ponto de recuperação inicial, em Olá **Backup** folha clique **Backup agora**.</span><span class="sxs-lookup"><span data-stu-id="fbacf-135">toocreate an initial recovery point, on hello **Backup** blade click **Backup now**.</span></span>
11. <span data-ttu-id="fbacf-136">Em Olá **Backup agora** folha, clique no ícone de calendário hello, use Olá calendário controle tooselect Olá último dia deste ponto de recuperação é mantido e clique em **Backup**.</span><span class="sxs-lookup"><span data-stu-id="fbacf-136">On hello **Backup Now** blade, click hello calendar icon, use hello calendar control tooselect hello last day this recovery point is retained, and click **Backup**.</span></span>
12. <span data-ttu-id="fbacf-137">Em Olá **Backup** folha para sua VM, você verá Olá número de pontos de recuperação completa.</span><span class="sxs-lookup"><span data-stu-id="fbacf-137">In hello **Backup** blade for your VM, you will see hello number of recovery points that are complete.</span></span>

    ![Pontos de Recuperação](./media/tutorial-backup-vms/backup-complete.png)

<span data-ttu-id="fbacf-139">primeiro backup de saudação leva cerca de 20 minutos.</span><span class="sxs-lookup"><span data-stu-id="fbacf-139">hello first backup takes about 20 minutes.</span></span> <span data-ttu-id="fbacf-140">Depois que o backup for concluído, vá toohello próxima parte deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="fbacf-140">Proceed toohello next part of this tutorial after your backup is finished.</span></span>

## <a name="restore-a-file"></a><span data-ttu-id="fbacf-141">Restaurar um arquivo</span><span class="sxs-lookup"><span data-stu-id="fbacf-141">Restore a file</span></span>

<span data-ttu-id="fbacf-142">Se você excluir ou fazer alterações tooa arquivo acidentalmente, você pode usar o arquivo de saudação do toorecover de recuperação de arquivos do seu Cofre de backup.</span><span class="sxs-lookup"><span data-stu-id="fbacf-142">If you accidentally delete or make changes tooa file, you can use File Recovery toorecover hello file from your backup vault.</span></span> <span data-ttu-id="fbacf-143">Recuperação de arquivos usa um script que é executado em Olá VM, ponto de recuperação toomount hello como unidade local.</span><span class="sxs-lookup"><span data-stu-id="fbacf-143">File Recovery uses a script that runs on hello VM, toomount hello recovery point as local drive.</span></span> <span data-ttu-id="fbacf-144">Essas unidades permanecerá montadas por 12 horas para que você possa copiar arquivos de ponto de recuperação de saudação e restaurá-los toohello VM.</span><span class="sxs-lookup"><span data-stu-id="fbacf-144">These drives will remain mounted for 12 hours so that you can copy files from hello recovery point and restore them toohello VM.</span></span>  

<span data-ttu-id="fbacf-145">Neste exemplo, mostramos como toorecover Olá padrão nginx página da web /var/www/html/index.nginx-debian.html.</span><span class="sxs-lookup"><span data-stu-id="fbacf-145">In this example, we show how toorecover hello default nginx web page /var/www/html/index.nginx-debian.html.</span></span> <span data-ttu-id="fbacf-146">endereço IP público de saudação do nosso VM neste exemplo é *13.69.75.209*.</span><span class="sxs-lookup"><span data-stu-id="fbacf-146">hello public IP address of our VM in this example is *13.69.75.209*.</span></span> <span data-ttu-id="fbacf-147">Você pode encontrar o endereço IP de saudação do vm usando:</span><span class="sxs-lookup"><span data-stu-id="fbacf-147">You can find hello IP address of your vm using:</span></span>

 ```bash 
 az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
 ```

 
1. <span data-ttu-id="fbacf-148">No computador local, abra um navegador e digite no endereço IP público de saudação VM toosee saudação padrão nginx da página da web.</span><span class="sxs-lookup"><span data-stu-id="fbacf-148">On your local computer, open a browser and type in hello public IP address of your VM toosee hello default nginx web page.</span></span>

    ![Página Web do nginx padrão](./media/tutorial-backup-vms/nginx-working.png)

1. <span data-ttu-id="fbacf-150">SSH em sua VM.</span><span class="sxs-lookup"><span data-stu-id="fbacf-150">SSH into your VM.</span></span>

    ```bash
    ssh 13.69.75.209
    ```
2. <span data-ttu-id="fbacf-151">Exclua /var/www/html/index.nginx-debian.html.</span><span class="sxs-lookup"><span data-stu-id="fbacf-151">Delete /var/www/html/index.nginx-debian.html.</span></span>

    ```bash
    sudo rm /var/www/html/index.nginx-debian.html
    ```
    
4. <span data-ttu-id="fbacf-152">No computador local, atualize o navegador de saudação pressionando CTRL + F5 toosee que nginx página padrão não existe mais.</span><span class="sxs-lookup"><span data-stu-id="fbacf-152">On your local computer, refresh hello browser by hitting CTRL + F5 toosee that default nginx page is gone.</span></span>

    ![Página Web do nginx padrão](./media/tutorial-backup-vms/nginx-broken.png)
    
1. <span data-ttu-id="fbacf-154">Em seu computador local, faça logon no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="fbacf-154">On your local computer, sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
6. <span data-ttu-id="fbacf-155">No menu Olá Olá esquerda, selecione **máquinas virtuais**.</span><span class="sxs-lookup"><span data-stu-id="fbacf-155">In hello menu on hello left, select **Virtual machines**.</span></span> 
7. <span data-ttu-id="fbacf-156">Olá, selecione lista Olá VM.</span><span class="sxs-lookup"><span data-stu-id="fbacf-156">From hello list, select hello VM.</span></span>
8. <span data-ttu-id="fbacf-157">Na folha VM hello, em Olá **configurações** seção, clique em **Backup**.</span><span class="sxs-lookup"><span data-stu-id="fbacf-157">On hello VM blade, in hello **Settings** section, click **Backup**.</span></span> <span data-ttu-id="fbacf-158">Olá **Backup** folha é aberta.</span><span class="sxs-lookup"><span data-stu-id="fbacf-158">hello **Backup** blade opens.</span></span> 
9. <span data-ttu-id="fbacf-159">No menu de saudação na parte superior de saudação da folha de saudação, selecione **recuperação de arquivo**.</span><span class="sxs-lookup"><span data-stu-id="fbacf-159">In hello menu at hello top of hello blade, select **File Recovery**.</span></span> <span data-ttu-id="fbacf-160">Olá **recuperação de arquivo** folha é aberta.</span><span class="sxs-lookup"><span data-stu-id="fbacf-160">hello **File Recovery** blade opens.</span></span>
10. <span data-ttu-id="fbacf-161">Em **etapa 1: selecione o ponto de recuperação**, selecione um ponto de recuperação na lista suspensa hello.</span><span class="sxs-lookup"><span data-stu-id="fbacf-161">In **Step 1: Select recovery point**, select a recovery point from hello drop-down.</span></span>
11. <span data-ttu-id="fbacf-162">No **etapa 2: baixar o script toobrowse e recuperar arquivos**, clique em hello **executável baixar** botão.</span><span class="sxs-lookup"><span data-stu-id="fbacf-162">In **Step 2: Download script toobrowse and recover files**, click hello **Download Executable** button.</span></span> <span data-ttu-id="fbacf-163">Salve o computador local do tooyour Olá arquivo baixado.</span><span class="sxs-lookup"><span data-stu-id="fbacf-163">Save hello downloaded file tooyour local computer.</span></span>
7. <span data-ttu-id="fbacf-164">Clique em **baixar script** arquivo de script de saudação toodownload localmente.</span><span class="sxs-lookup"><span data-stu-id="fbacf-164">Click **Download script** toodownload hello script file locally.</span></span>
8. <span data-ttu-id="fbacf-165">Abra um Bash prompt e digite Olá a seguir, substituindo *Linux_myVM_05-05-2017.sh* com hello corrija o caminho e nome de arquivo para o script hello baixado, *azureuser* com nome de usuário Olá para Olá VM e *13.69.75.209* com endereço IP público de saudação para sua VM.</span><span class="sxs-lookup"><span data-stu-id="fbacf-165">Open a Bash prompt and type hello following, replacing *Linux_myVM_05-05-2017.sh* with hello correct path and filename for hello script that you downloaded, *azureuser* with hello username for hello VM and *13.69.75.209* with hello public IP address for your VM.</span></span>
    
    ```bash
    scp Linux_myVM_05-05-2017.sh azureuser@13.69.75.209:
    ```
    
9. <span data-ttu-id="fbacf-166">No computador local, abra uma conexão de SSH toohello VM.</span><span class="sxs-lookup"><span data-stu-id="fbacf-166">On your local computer, open an SSH connection toohello VM.</span></span>

    ```bash
    ssh 13.69.75.209
    ```
    
10. <span data-ttu-id="fbacf-167">Na sua VM, adicionar executar o arquivo de script de toohello de permissões.</span><span class="sxs-lookup"><span data-stu-id="fbacf-167">On your VM, add execute permissions toohello script file.</span></span>

    ```bash
    chmod +x Linux_myVM_05-05-2017.sh
    ```
    
11. <span data-ttu-id="fbacf-168">Na sua VM, execute o ponto de recuperação de saudação do hello script toomount como um sistema de arquivos.</span><span class="sxs-lookup"><span data-stu-id="fbacf-168">On your VM, run hello script toomount hello recovery point as a filesystem.</span></span>

    ```bash
    ./Linux_myVM_05-05-2017.sh
    ```
    
12. <span data-ttu-id="fbacf-169">Olá saída de hello script fornece que Olá o caminho para o ponto de montagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="fbacf-169">hello output from hello script gives you hello path for hello mount point.</span></span> <span data-ttu-id="fbacf-170">saída de Hello parece semelhante toothis:</span><span class="sxs-lookup"><span data-stu-id="fbacf-170">hello output looks similar toothis:</span></span>

    ```bash
    Microsoft Azure VM Backup - File Recovery
    ______________________________________________
                          
    Connecting toorecovery point using ISCSI service...
    
    Connection succeeded!
    
    Please wait while we attach volumes of hello recovery point toothis machine...
                         
    ************ Volumes of hello recovery point and their mount paths on this machine ************

    Sr.No.  |  Disk  |  Volume  |  MountPath 

    1)  | /dev/sdc  |  /dev/sdc1  |  /home/azureuser/myVM-20170505191055/Volume1

    ************ Open File Explorer toobrowse for files. ************

    After recovery, tooremove hello disks and close hello connection toohello recovery point, please click 'Unmount Disks' in step 3 of hello portal.

    Please enter 'q/Q' tooexit...
    ```

12. <span data-ttu-id="fbacf-171">Na sua VM, copie a página da web do hello nginx padrão do hello montagem ponto back toowhere você excluir o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="fbacf-171">On your VM, copy hello nginx default web page from hello mount point back toowhere you deleted hello file.</span></span>

    ```bash
    sudo cp ~/myVM-20170505191055/Volume1/var/www/html/index.nginx-debian.html /var/www/html/
    ```
    
17. <span data-ttu-id="fbacf-172">No computador local, abra a guia do navegador de saudação em que você está conectado toohello endereço IP de saudação VM mostrando Olá nginx padrão a página.</span><span class="sxs-lookup"><span data-stu-id="fbacf-172">On your local computer, open hello browser tab where you are connected toohello IP address of hello VM showing hello nginx default page.</span></span> <span data-ttu-id="fbacf-173">Pressione CTRL + F5 página do navegador Olá toorefresh.</span><span class="sxs-lookup"><span data-stu-id="fbacf-173">Press CTRL + F5 toorefresh hello browser page.</span></span> <span data-ttu-id="fbacf-174">Agora, você verá que Olá página padrão está funcionando novamente.</span><span class="sxs-lookup"><span data-stu-id="fbacf-174">You should now see that hello default page is working again.</span></span>

    ![Página Web do nginx padrão](./media/tutorial-backup-vms/nginx-working.png)

18. <span data-ttu-id="fbacf-176">No computador local, volte toohello guia do navegador para Olá portal do Azure e na **etapa 3: desmontar discos Olá após a recuperação** clique Olá **desmontar discos** botão.</span><span class="sxs-lookup"><span data-stu-id="fbacf-176">On your local computer, go back toohello browser tab for hello Azure portal and in **Step 3: Unmount hello disks after recovery** click hello **Unmount Disks** button.</span></span> <span data-ttu-id="fbacf-177">Se você esquecer toodo nesta etapa, ponto de montagem do hello conexão toohello é fechar automaticamente após 12 horas.</span><span class="sxs-lookup"><span data-stu-id="fbacf-177">If you forget toodo this step, hello connection toohello mountpoint is automatically close after 12 hours.</span></span> <span data-ttu-id="fbacf-178">Após as 12 horas, é necessário toodownload um novo toocreate de script um novo ponto de montagem.</span><span class="sxs-lookup"><span data-stu-id="fbacf-178">After those 12 hours, you need toodownload a new script toocreate a new mountpoint.</span></span>


## <a name="next-steps"></a><span data-ttu-id="fbacf-179">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fbacf-179">Next steps</span></span>

<span data-ttu-id="fbacf-180">Neste tutorial, você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="fbacf-180">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fbacf-181">Criar um backup de uma VM</span><span class="sxs-lookup"><span data-stu-id="fbacf-181">Create a backup of a VM</span></span>
> * <span data-ttu-id="fbacf-182">Agendar um backup diário</span><span class="sxs-lookup"><span data-stu-id="fbacf-182">Schedule a daily backup</span></span>
> * <span data-ttu-id="fbacf-183">Restaurar um arquivo de um backup</span><span class="sxs-lookup"><span data-stu-id="fbacf-183">Restore a file from a backup</span></span>

<span data-ttu-id="fbacf-184">Avançar toohello toolearn próximo de tutorial sobre o monitoramento de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="fbacf-184">Advance toohello next tutorial toolearn about monitoring virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fbacf-185">Monitorar máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="fbacf-185">Monitor virtual machines</span></span>](tutorial-monitoring.md)

