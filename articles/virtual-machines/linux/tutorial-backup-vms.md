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
ms.openlocfilehash: d0cbf7883a8737bcb10e9dd251c9792a12993f77
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="back-up-linux--virtual-machines-in-azure"></a><span data-ttu-id="0c14a-103">Fazer backup de máquinas virtuais do Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="0c14a-103">Back up Linux  virtual machines in Azure</span></span>

<span data-ttu-id="0c14a-104">Você pode proteger seus dados fazendo backups em intervalos regulares.</span><span class="sxs-lookup"><span data-stu-id="0c14a-104">You can protect your data by taking backups at regular intervals.</span></span> <span data-ttu-id="0c14a-105">O Backup do Azure cria pontos de recuperação que são armazenados em cofres de recuperação com redundância geográfica.</span><span class="sxs-lookup"><span data-stu-id="0c14a-105">Azure Backup creates recovery points that are stored in geo-redundant recovery vaults.</span></span> <span data-ttu-id="0c14a-106">Ao restaurar de um ponto de recuperação, você pode restaurar a VM inteira ou apenas arquivos específicos.</span><span class="sxs-lookup"><span data-stu-id="0c14a-106">When you restore from a recovery point, you can restore the whole VM or just specific files.</span></span> <span data-ttu-id="0c14a-107">Este artigo explica como restaurar um único arquivo em uma VM do Linux que executa o nginx.</span><span class="sxs-lookup"><span data-stu-id="0c14a-107">This article explains how to restore a single file to a Linux VM running nginx.</span></span> <span data-ttu-id="0c14a-108">Se você ainda não tem uma VM para usar, você pode criar uma usando o [Início rápido do Linux](quick-create-cli.md).</span><span class="sxs-lookup"><span data-stu-id="0c14a-108">If you don't already have a VM to use, you can create one using the [Linux quickstart](quick-create-cli.md).</span></span> <span data-ttu-id="0c14a-109">Neste tutorial, você aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="0c14a-109">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0c14a-110">Criar um backup de uma VM</span><span class="sxs-lookup"><span data-stu-id="0c14a-110">Create a backup of a VM</span></span>
> * <span data-ttu-id="0c14a-111">Agendar um backup diário</span><span class="sxs-lookup"><span data-stu-id="0c14a-111">Schedule a daily backup</span></span>
> * <span data-ttu-id="0c14a-112">Restaurar um arquivo de um backup</span><span class="sxs-lookup"><span data-stu-id="0c14a-112">Restore a file from a backup</span></span>



## <a name="backup-overview"></a><span data-ttu-id="0c14a-113">Visão geral do backup</span><span class="sxs-lookup"><span data-stu-id="0c14a-113">Backup overview</span></span>

<span data-ttu-id="0c14a-114">Quando o serviço de Backup do Azure inicia um backup, ele dispara a extensão de backup para obter um instantâneo pontual.</span><span class="sxs-lookup"><span data-stu-id="0c14a-114">When the Azure Backup service initiates a backup, it triggers the backup extension to take a point-in-time snapshot.</span></span> <span data-ttu-id="0c14a-115">O serviço de Backup do Azure usa a extensão _VMSnapshotLinux_ no Linux.</span><span class="sxs-lookup"><span data-stu-id="0c14a-115">The Azure Backup service uses the _VMSnapshotLinux_ extension in Linux.</span></span> <span data-ttu-id="0c14a-116">A extensão é instalada durante o primeiro backup de VM se a VM está em execução.</span><span class="sxs-lookup"><span data-stu-id="0c14a-116">The extension is installed during the first VM backup if the VM is running.</span></span> <span data-ttu-id="0c14a-117">Se a VM não estiver em execução, o serviço de Backup criará um instantâneo do armazenamento subjacente (já que nenhuma gravação de aplicativo ocorre enquanto a VM está parada).</span><span class="sxs-lookup"><span data-stu-id="0c14a-117">If the VM is not running, the Backup service takes a snapshot of the underlying storage (since no application writes occur while the VM is stopped).</span></span>

<span data-ttu-id="0c14a-118">Por padrão, o Backup do Azure usa um backup consistente de sistema de arquivos para a VM do Linux, mas ele pode ser configurado para fazer um [backup consistente de aplicativos usando a estrutura de pré e pós-script](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent).</span><span class="sxs-lookup"><span data-stu-id="0c14a-118">By default, Azure Backup takes a file system consistent backup for Linux VM but it can be configured to take [application consistent backup using pre-script and post-script framework](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent).</span></span> <span data-ttu-id="0c14a-119">Depois que o serviço de Backup do Azure gera o instantâneo, os dados são transferidos para o cofre.</span><span class="sxs-lookup"><span data-stu-id="0c14a-119">Once the Azure Backup service takes the snapshot, the data is transferred to the vault.</span></span> <span data-ttu-id="0c14a-120">Para maximizar a eficiência, o serviço identifica e transfere apenas os blocos de dados que foram alterados desde o backup anterior.</span><span class="sxs-lookup"><span data-stu-id="0c14a-120">To maximize efficiency, the service identifies and transfers only the blocks of data that have changed since the previous backup.</span></span>

<span data-ttu-id="0c14a-121">Quando a transferência de dados é concluída, o instantâneo é removido e um ponto de recuperação é criado.</span><span class="sxs-lookup"><span data-stu-id="0c14a-121">When the data transfer is complete, the snapshot is removed and a recovery point is created.</span></span>


## <a name="create-a-backup"></a><span data-ttu-id="0c14a-122">Criar um backup</span><span class="sxs-lookup"><span data-stu-id="0c14a-122">Create a backup</span></span>
<span data-ttu-id="0c14a-123">Crie um backup diário agendado simples em um Cofre de Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="0c14a-123">Create a simple scheduled daily backup to a Recovery Services Vault.</span></span> 

1. <span data-ttu-id="0c14a-124">Entre no [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0c14a-124">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="0c14a-125">No menu à esquerda, selecione **Máquinas virtuais**.</span><span class="sxs-lookup"><span data-stu-id="0c14a-125">In the menu on the left, select **Virtual machines**.</span></span> 
3. <span data-ttu-id="0c14a-126">Na lista, selecione uma VM da qual fazer backup.</span><span class="sxs-lookup"><span data-stu-id="0c14a-126">From the list, select a VM to back up.</span></span>
4. <span data-ttu-id="0c14a-127">Na folha da VM, na seção **Configurações**, clique em **Backup**.</span><span class="sxs-lookup"><span data-stu-id="0c14a-127">On the VM blade, in the **Settings** section, click **Backup**.</span></span> <span data-ttu-id="0c14a-128">A folha **Habilitar backup** é aberta.</span><span class="sxs-lookup"><span data-stu-id="0c14a-128">The **Enable backup** blade opens.</span></span>
5. <span data-ttu-id="0c14a-129">Em **Cofre de Serviços de Recuperação**, clique em **Criar novo** e forneça o nome para o novo cofre.</span><span class="sxs-lookup"><span data-stu-id="0c14a-129">In **Recovery Services vault**, click **Create new** and provide the name for the new vault.</span></span> <span data-ttu-id="0c14a-130">Um novo cofre é criado no mesmo Grupo de Recursos e na mesma localização que a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0c14a-130">A new vault is created in the same Resource Group and location as the virtual machine.</span></span>
6. <span data-ttu-id="0c14a-131">Clique em **Política de backup**.</span><span class="sxs-lookup"><span data-stu-id="0c14a-131">Click **Backup policy**.</span></span> <span data-ttu-id="0c14a-132">Para este exemplo, mantenha os padrões e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="0c14a-132">For this example, keep the defaults and click **OK**.</span></span>
7. <span data-ttu-id="0c14a-133">Na folha **Habilitar backup**, clique em **Habilitar Backup**.</span><span class="sxs-lookup"><span data-stu-id="0c14a-133">On the **Enable backup** blade, click **Enable Backup**.</span></span> <span data-ttu-id="0c14a-134">Isso cria um backup diário com base no agendamento padrão.</span><span class="sxs-lookup"><span data-stu-id="0c14a-134">This creates a daily backup based on the default schedule.</span></span>
10. <span data-ttu-id="0c14a-135">Para criar um ponto de recuperação inicial, na folha **Backup**, clique em **Fazer backup agora**.</span><span class="sxs-lookup"><span data-stu-id="0c14a-135">To create an initial recovery point, on the **Backup** blade click **Backup now**.</span></span>
11. <span data-ttu-id="0c14a-136">Na folha **Fazer Backup Agora**, clique no ícone de calendário, use o controle de calendário para selecionar o último dia de retenção desse ponto de recuperação e clique em **Fazer Backup**.</span><span class="sxs-lookup"><span data-stu-id="0c14a-136">On the **Backup Now** blade, click the calendar icon, use the calendar control to select the last day this recovery point is retained, and click **Backup**.</span></span>
12. <span data-ttu-id="0c14a-137">Na folha **Backup** de sua VM, você verá o número de pontos de recuperação completos.</span><span class="sxs-lookup"><span data-stu-id="0c14a-137">In the **Backup** blade for your VM, you will see the number of recovery points that are complete.</span></span>

    ![Pontos de Recuperação](./media/tutorial-backup-vms/backup-complete.png)

<span data-ttu-id="0c14a-139">O primeiro backup leva aproximadamente 20 minutos.</span><span class="sxs-lookup"><span data-stu-id="0c14a-139">The first backup takes about 20 minutes.</span></span> <span data-ttu-id="0c14a-140">Prossiga para a próxima parte deste tutorial depois que o backup for concluído.</span><span class="sxs-lookup"><span data-stu-id="0c14a-140">Proceed to the next part of this tutorial after your backup is finished.</span></span>

## <a name="restore-a-file"></a><span data-ttu-id="0c14a-141">Restaurar um arquivo</span><span class="sxs-lookup"><span data-stu-id="0c14a-141">Restore a file</span></span>

<span data-ttu-id="0c14a-142">Se você acidentalmente excluir ou fizer alterações em um arquivo, você poderá usar a recuperação de arquivo para recuperar o arquivo de seu cofre de backup.</span><span class="sxs-lookup"><span data-stu-id="0c14a-142">If you accidentally delete or make changes to a file, you can use File Recovery to recover the file from your backup vault.</span></span> <span data-ttu-id="0c14a-143">A Recuperação de Arquivo utiliza um script que é executado na VM para montar o ponto de recuperação como uma unidade local.</span><span class="sxs-lookup"><span data-stu-id="0c14a-143">File Recovery uses a script that runs on the VM, to mount the recovery point as local drive.</span></span> <span data-ttu-id="0c14a-144">Essas unidades permanecerão montadas por 12 horas para que você possa copiar arquivos do ponto de recuperação e restaurá-los para a VM.</span><span class="sxs-lookup"><span data-stu-id="0c14a-144">These drives will remain mounted for 12 hours so that you can copy files from the recovery point and restore them to the VM.</span></span>  

<span data-ttu-id="0c14a-145">Neste exemplo, mostramos como recuperar a página Web do nginx padrão /var/www/html/index.nginx-debian.html.</span><span class="sxs-lookup"><span data-stu-id="0c14a-145">In this example, we show how to recover the default nginx web page /var/www/html/index.nginx-debian.html.</span></span> <span data-ttu-id="0c14a-146">O endereço IP público de nossa VM neste exemplo é *13.69.75.209*.</span><span class="sxs-lookup"><span data-stu-id="0c14a-146">The public IP address of our VM in this example is *13.69.75.209*.</span></span> <span data-ttu-id="0c14a-147">Encontre o endereço IP da sua vm usando:</span><span class="sxs-lookup"><span data-stu-id="0c14a-147">You can find the IP address of your vm using:</span></span>

 ```bash 
 az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
 ```

 
1. <span data-ttu-id="0c14a-148">No computador local, abra um navegador e digite o endereço IP público de sua VM para ver a página Web do nginx padrão.</span><span class="sxs-lookup"><span data-stu-id="0c14a-148">On your local computer, open a browser and type in the public IP address of your VM to see the default nginx web page.</span></span>

    ![Página Web do nginx padrão](./media/tutorial-backup-vms/nginx-working.png)

1. <span data-ttu-id="0c14a-150">SSH em sua VM.</span><span class="sxs-lookup"><span data-stu-id="0c14a-150">SSH into your VM.</span></span>

    ```bash
    ssh 13.69.75.209
    ```
2. <span data-ttu-id="0c14a-151">Exclua /var/www/html/index.nginx-debian.html.</span><span class="sxs-lookup"><span data-stu-id="0c14a-151">Delete /var/www/html/index.nginx-debian.html.</span></span>

    ```bash
    sudo rm /var/www/html/index.nginx-debian.html
    ```
    
4. <span data-ttu-id="0c14a-152">No computador local, atualize o navegador teclando em CTRL + F5 para ver se a página padrão do nginx foi removida.</span><span class="sxs-lookup"><span data-stu-id="0c14a-152">On your local computer, refresh the browser by hitting CTRL + F5 to see that default nginx page is gone.</span></span>

    ![Página Web do nginx padrão](./media/tutorial-backup-vms/nginx-broken.png)
    
1. <span data-ttu-id="0c14a-154">No computador local, entre no [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0c14a-154">On your local computer, sign in to the [Azure portal](https://portal.azure.com/).</span></span>
6. <span data-ttu-id="0c14a-155">No menu à esquerda, selecione **Máquinas virtuais**.</span><span class="sxs-lookup"><span data-stu-id="0c14a-155">In the menu on the left, select **Virtual machines**.</span></span> 
7. <span data-ttu-id="0c14a-156">Selecione a VM na lista.</span><span class="sxs-lookup"><span data-stu-id="0c14a-156">From the list, select the VM.</span></span>
8. <span data-ttu-id="0c14a-157">Na folha da VM, na seção **Configurações**, clique em **Backup**.</span><span class="sxs-lookup"><span data-stu-id="0c14a-157">On the VM blade, in the **Settings** section, click **Backup**.</span></span> <span data-ttu-id="0c14a-158">A folha **Backup** é aberta.</span><span class="sxs-lookup"><span data-stu-id="0c14a-158">The **Backup** blade opens.</span></span> 
9. <span data-ttu-id="0c14a-159">No menu na parte superior da folha, selecione **Recuperação de Arquivo**.</span><span class="sxs-lookup"><span data-stu-id="0c14a-159">In the menu at the top of the blade, select **File Recovery**.</span></span> <span data-ttu-id="0c14a-160">A folha **Recuperação de arquivo** será aberta.</span><span class="sxs-lookup"><span data-stu-id="0c14a-160">The **File Recovery** blade opens.</span></span>
10. <span data-ttu-id="0c14a-161">Em **Etapa 1: selecionar um ponto de recuperação**, selecione um ponto de recuperação do menu suspenso.</span><span class="sxs-lookup"><span data-stu-id="0c14a-161">In **Step 1: Select recovery point**, select a recovery point from the drop-down.</span></span>
11. <span data-ttu-id="0c14a-162">Em **Etapa 2: baixar o script para procurar e recuperar arquivos**, clique no botão **Baixar Executável**.</span><span class="sxs-lookup"><span data-stu-id="0c14a-162">In **Step 2: Download script to browse and recover files**, click the **Download Executable** button.</span></span> <span data-ttu-id="0c14a-163">Salve o arquivo baixado em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="0c14a-163">Save the downloaded file to your local computer.</span></span>
7. <span data-ttu-id="0c14a-164">Clique em **Baixar script** para baixar o arquivo de script localmente.</span><span class="sxs-lookup"><span data-stu-id="0c14a-164">Click **Download script** to download the script file locally.</span></span>
8. <span data-ttu-id="0c14a-165">Abra um prompt Bash e digite o seguinte, substituindo *Linux_myVM_05-05-2017.sh* pelo caminho e o nome de arquivo do script que você baixou, *azureuser* pelo nome de usuário da VM e *13.69.75.209* pelo endereço IP público de sua VM.</span><span class="sxs-lookup"><span data-stu-id="0c14a-165">Open a Bash prompt and type the following, replacing *Linux_myVM_05-05-2017.sh* with the correct path and filename for the script that you downloaded, *azureuser* with the username for the VM and *13.69.75.209* with the public IP address for your VM.</span></span>
    
    ```bash
    scp Linux_myVM_05-05-2017.sh azureuser@13.69.75.209:
    ```
    
9. <span data-ttu-id="0c14a-166">No computador local, abra uma conexão SSH para a VM.</span><span class="sxs-lookup"><span data-stu-id="0c14a-166">On your local computer, open an SSH connection to the VM.</span></span>

    ```bash
    ssh 13.69.75.209
    ```
    
10. <span data-ttu-id="0c14a-167">Em sua VM, adicione permissões de execução ao arquivo de script.</span><span class="sxs-lookup"><span data-stu-id="0c14a-167">On your VM, add execute permissions to the script file.</span></span>

    ```bash
    chmod +x Linux_myVM_05-05-2017.sh
    ```
    
11. <span data-ttu-id="0c14a-168">Em sua VM, execute o script para montar o ponto de recuperação como um sistema de arquivos.</span><span class="sxs-lookup"><span data-stu-id="0c14a-168">On your VM, run the script to mount the recovery point as a filesystem.</span></span>

    ```bash
    ./Linux_myVM_05-05-2017.sh
    ```
    
12. <span data-ttu-id="0c14a-169">A saída do script fornece o caminho para o ponto de montagem.</span><span class="sxs-lookup"><span data-stu-id="0c14a-169">The output from the script gives you the path for the mount point.</span></span> <span data-ttu-id="0c14a-170">A saída deve ser semelhante a esta:</span><span class="sxs-lookup"><span data-stu-id="0c14a-170">The output looks similar to this:</span></span>

    ```bash
    Microsoft Azure VM Backup - File Recovery
    ______________________________________________
                          
    Connecting to recovery point using ISCSI service...
    
    Connection succeeded!
    
    Please wait while we attach volumes of the recovery point to this machine...
                         
    ************ Volumes of the recovery point and their mount paths on this machine ************

    Sr.No.  |  Disk  |  Volume  |  MountPath 

    1)  | /dev/sdc  |  /dev/sdc1  |  /home/azureuser/myVM-20170505191055/Volume1

    ************ Open File Explorer to browse for files. ************

    After recovery, to remove the disks and close the connection to the recovery point, please click 'Unmount Disks' in step 3 of the portal.

    Please enter 'q/Q' to exit...
    ```

12. <span data-ttu-id="0c14a-171">Em sua VM, copie a página Web nginx padrão do ponto de montagem para o local onde você excluiu o arquivo.</span><span class="sxs-lookup"><span data-stu-id="0c14a-171">On your VM, copy the nginx default web page from the mount point back to where you deleted the file.</span></span>

    ```bash
    sudo cp ~/myVM-20170505191055/Volume1/var/www/html/index.nginx-debian.html /var/www/html/
    ```
    
17. <span data-ttu-id="0c14a-172">No computador local, abra a guia do navegador em que você está conectado ao endereço IP da VM mostrando a página padrão do nginx.</span><span class="sxs-lookup"><span data-stu-id="0c14a-172">On your local computer, open the browser tab where you are connected to the IP address of the VM showing the nginx default page.</span></span> <span data-ttu-id="0c14a-173">Pressione CTRL + F5 para atualizar a página do navegador.</span><span class="sxs-lookup"><span data-stu-id="0c14a-173">Press CTRL + F5 to refresh the browser page.</span></span> <span data-ttu-id="0c14a-174">Agora você verá que a página padrão está funcionando novamente.</span><span class="sxs-lookup"><span data-stu-id="0c14a-174">You should now see that the default page is working again.</span></span>

    ![Página Web do nginx padrão](./media/tutorial-backup-vms/nginx-working.png)

18. <span data-ttu-id="0c14a-176">No computador local, volte para a guia do navegador para o Portal do Azure e, na **Etapa 3: desmontar discos após a recuperação**, clique no botão **Desmontar Discos**.</span><span class="sxs-lookup"><span data-stu-id="0c14a-176">On your local computer, go back to the browser tab for the Azure portal and in **Step 3: Unmount the disks after recovery** click the **Unmount Disks** button.</span></span> <span data-ttu-id="0c14a-177">Se você esquecer de fazer isso, a conexão para o ponto de montagem será fechada automaticamente após 12 horas.</span><span class="sxs-lookup"><span data-stu-id="0c14a-177">If you forget to do this step, the connection to the mountpoint is automatically close after 12 hours.</span></span> <span data-ttu-id="0c14a-178">Após essas 12 horas, você precisa baixar um novo script para criar um novo ponto de montagem.</span><span class="sxs-lookup"><span data-stu-id="0c14a-178">After those 12 hours, you need to download a new script to create a new mountpoint.</span></span>


## <a name="next-steps"></a><span data-ttu-id="0c14a-179">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0c14a-179">Next steps</span></span>

<span data-ttu-id="0c14a-180">Neste tutorial, você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="0c14a-180">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0c14a-181">Criar um backup de uma VM</span><span class="sxs-lookup"><span data-stu-id="0c14a-181">Create a backup of a VM</span></span>
> * <span data-ttu-id="0c14a-182">Agendar um backup diário</span><span class="sxs-lookup"><span data-stu-id="0c14a-182">Schedule a daily backup</span></span>
> * <span data-ttu-id="0c14a-183">Restaurar um arquivo de um backup</span><span class="sxs-lookup"><span data-stu-id="0c14a-183">Restore a file from a backup</span></span>

<span data-ttu-id="0c14a-184">Avance para o próximo tutorial para saber mais sobre o monitoramento de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="0c14a-184">Advance to the next tutorial to learn about monitoring virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0c14a-185">Monitorar máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="0c14a-185">Monitor virtual machines</span></span>](tutorial-monitoring.md)

