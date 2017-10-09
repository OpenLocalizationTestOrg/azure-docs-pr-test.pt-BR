---
title: "aaaBackup máquinas virtuais do Windows Azure | Microsoft Docs"
description: Proteja as VMs do Windows fazendo backup delas com o Backup do Azure.
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/27/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 1cd3e1940a83aacd160cba3c8613b63b6f3c11d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-windows-virtual-machines-in-azure"></a><span data-ttu-id="dd2fb-103">Fazer backup de máquinas virtuais do Windows no Azure</span><span class="sxs-lookup"><span data-stu-id="dd2fb-103">Back up Windows virtual machines in Azure</span></span>

<span data-ttu-id="dd2fb-104">Você pode proteger seus dados fazendo backups em intervalos regulares.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-104">You can protect your data by taking backups at regular intervals.</span></span> <span data-ttu-id="dd2fb-105">O Backup do Azure cria pontos de recuperação que são armazenados em cofres de recuperação com redundância geográfica.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-105">Azure Backup creates recovery points that are stored in geo-redundant recovery vaults.</span></span> <span data-ttu-id="dd2fb-106">Quando você restaurar de um ponto de recuperação, você poderá restaurar Olá VM inteira ou apenas determinados arquivos.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-106">When you restore from a recovery point, you can restore hello whole VM or just specific files.</span></span> <span data-ttu-id="dd2fb-107">Este artigo explica como toorestore um único arquivo tooa VM que executa o Windows Server e o IIS.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-107">This article explains how toorestore a single file tooa VM running Windows Server and IIS.</span></span> <span data-ttu-id="dd2fb-108">Se você ainda não tiver um toouse VM, você pode criar um usando Olá [início rápido do Windows](quick-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="dd2fb-108">If you don't already have a VM toouse, you can create one using hello [Windows quickstart](quick-create-portal.md).</span></span> <span data-ttu-id="dd2fb-109">Neste tutorial, você aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="dd2fb-109">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="dd2fb-110">Criar um backup de uma VM</span><span class="sxs-lookup"><span data-stu-id="dd2fb-110">Create a backup of a VM</span></span>
> * <span data-ttu-id="dd2fb-111">Agendar um backup diário</span><span class="sxs-lookup"><span data-stu-id="dd2fb-111">Schedule a daily backup</span></span>
> * <span data-ttu-id="dd2fb-112">Restaurar um arquivo de um backup</span><span class="sxs-lookup"><span data-stu-id="dd2fb-112">Restore a file from a backup</span></span>




## <a name="backup-overview"></a><span data-ttu-id="dd2fb-113">Visão geral do backup</span><span class="sxs-lookup"><span data-stu-id="dd2fb-113">Backup overview</span></span>

<span data-ttu-id="dd2fb-114">Quando Olá serviço Backup do Azure inicia um trabalho de backup, ela aciona Olá extensão backup tootake um instantâneo point-in-time.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-114">When hello Azure Backup service initiates a backup job, it triggers hello backup extension tootake a point-in-time snapshot.</span></span> <span data-ttu-id="dd2fb-115">saudação de serviço de Backup do Azure usa Olá _VMSnapshot_ extensão.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-115">hello Azure Backup service uses hello _VMSnapshot_ extension.</span></span> <span data-ttu-id="dd2fb-116">extensão de saudação é instalado durante o primeiro backup VM Olá se Olá VM está em execução.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-116">hello extension is installed during hello first VM backup if hello VM is running.</span></span> <span data-ttu-id="dd2fb-117">Se hello VM não está em execução, Olá serviço de Backup tira um instantâneo de saudação armazenamento subjacente (já que nenhum aplicativo grava ocorre durante a saudação que VM estiver parada).</span><span class="sxs-lookup"><span data-stu-id="dd2fb-117">If hello VM is not running, hello Backup service takes a snapshot of hello underlying storage (since no application writes occur while hello VM is stopped).</span></span>

<span data-ttu-id="dd2fb-118">Ao tirar um instantâneo de máquinas virtuais do Windows, o serviço de Backup Olá coordena com hello Volume Shadow Copy Service (VSS) tooget um instantâneo consistente dos discos da máquina de virtual hello.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-118">When taking a snapshot of Windows VMs, hello Backup service coordinates with hello Volume Shadow Copy Service (VSS) tooget a consistent snapshot of hello virtual machine's disks.</span></span> <span data-ttu-id="dd2fb-119">Depois de saudação serviço Backup do Azure usa instantâneo hello, dados saudação são toohello transferidos cofre.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-119">Once hello Azure Backup service takes hello snapshot, hello data is transferred toohello vault.</span></span> <span data-ttu-id="dd2fb-120">toomaximize eficiência, o serviço de saudação identifica e transfere apenas os blocos de dados que foram alterados desde o backup anterior de saudação hello.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-120">toomaximize efficiency, hello service identifies and transfers only hello blocks of data that have changed since hello previous backup.</span></span>

<span data-ttu-id="dd2fb-121">Quando a transferência de dados de saudação for concluída, Olá é removido e um ponto de recuperação é criado.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-121">When hello data transfer is complete, hello snapshot is removed and a recovery point is created.</span></span>


## <a name="create-a-backup"></a><span data-ttu-id="dd2fb-122">Criar um backup</span><span class="sxs-lookup"><span data-stu-id="dd2fb-122">Create a backup</span></span>
<span data-ttu-id="dd2fb-123">Crie um simple agendado diariamente backup tooa Cofre de serviços de recuperação.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-123">Create a simple scheduled daily backup tooa Recovery Services Vault.</span></span> 

1. <span data-ttu-id="dd2fb-124">Entrar toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="dd2fb-124">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="dd2fb-125">No menu Olá Olá esquerda, selecione **máquinas virtuais**.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-125">In hello menu on hello left, select **Virtual machines**.</span></span> 
3. <span data-ttu-id="dd2fb-126">Olá, selecione lista tooback uma VM para cima.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-126">From hello list, select a VM tooback up.</span></span>
4. <span data-ttu-id="dd2fb-127">Na folha VM hello, em Olá **configurações** seção, clique em **Backup**.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-127">On hello VM blade, in hello **Settings** section, click **Backup**.</span></span> <span data-ttu-id="dd2fb-128">Olá **habilitar backup** folha é aberta.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-128">hello **Enable backup** blade opens.</span></span>
5. <span data-ttu-id="dd2fb-129">Em **Cofre de serviços de recuperação**, clique em **criar novo** e fornecer nome hello novo cofre de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-129">In **Recovery Services vault**, click **Create new** and provide hello name for hello new vault.</span></span> <span data-ttu-id="dd2fb-130">Um novo cofre é criado no hello mesmo grupo de recursos e o local da máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-130">A new vault is created in hello same Resource Group and location as hello virtual machine.</span></span>
6. <span data-ttu-id="dd2fb-131">Clique em **Política de backup**.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-131">Click **Backup policy**.</span></span> <span data-ttu-id="dd2fb-132">Neste exemplo, lembre-Olá padrões e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-132">For this example, keep hello defaults and click **OK**.</span></span>
7. <span data-ttu-id="dd2fb-133">Em Olá **habilitar backup** folha, clique em **habilitar Backup**.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-133">On hello **Enable backup** blade, click **Enable Backup**.</span></span> <span data-ttu-id="dd2fb-134">Isso cria um backup diário com base no agendamento de padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-134">This creates a daily backup based on hello default schedule.</span></span>
10. <span data-ttu-id="dd2fb-135">toocreate um ponto de recuperação inicial, em Olá **Backup** folha clique **Backup agora**.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-135">toocreate an initial recovery point, on hello **Backup** blade click **Backup now**.</span></span>
11. <span data-ttu-id="dd2fb-136">Em Olá **Backup agora** folha, clique no ícone de calendário hello, use Olá calendário controle tooselect Olá último dia deste ponto de recuperação é mantido e clique em **Backup**.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-136">On hello **Backup Now** blade, click hello calendar icon, use hello calendar control tooselect hello last day this recovery point is retained, and click **Backup**.</span></span>
12. <span data-ttu-id="dd2fb-137">Em Olá **Backup** folha para sua VM, você verá Olá número de pontos de recuperação completa.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-137">In hello **Backup** blade for your VM, you will see hello number of recovery points that are complete.</span></span>

    ![Pontos de Recuperação](./media/tutorial-backup-vms/backup-complete.png)
    
<span data-ttu-id="dd2fb-139">primeiro backup de saudação leva cerca de 20 minutos.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-139">hello first backup takes about 20 minutes.</span></span> <span data-ttu-id="dd2fb-140">Depois que o backup for concluído, vá toohello próxima parte deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-140">Proceed toohello next part of this tutorial after your backup is finished.</span></span>

## <a name="recover-a-file"></a><span data-ttu-id="dd2fb-141">Recuperar um arquivo</span><span class="sxs-lookup"><span data-stu-id="dd2fb-141">Recover a file</span></span>

<span data-ttu-id="dd2fb-142">Se você excluir ou fazer alterações tooa arquivo acidentalmente, você pode usar o arquivo de saudação do toorecover de recuperação de arquivos do seu Cofre de backup.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-142">If you accidentally delete or make changes tooa file, you can use File Recovery toorecover hello file from your backup vault.</span></span> <span data-ttu-id="dd2fb-143">Recuperação de arquivos usa um script que é executado em Olá VM, ponto de recuperação toomount hello como unidade local.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-143">File Recovery uses a script that runs on hello VM, toomount hello recovery point as local drive.</span></span> <span data-ttu-id="dd2fb-144">Essas unidades permanecerá montadas por 12 horas para que você possa copiar arquivos de ponto de recuperação de saudação e restaurá-los toohello VM.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-144">These drives will remain mounted for 12 hours so that you can copy files from hello recovery point and restore them toohello VM.</span></span>  

<span data-ttu-id="dd2fb-145">Neste exemplo, mostramos como toorecover Olá arquivo de imagem que é usado na página saudação padrão da web para o IIS.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-145">In this example, we show how toorecover hello image file that is used in hello default web page for IIS.</span></span> 

1. <span data-ttu-id="dd2fb-146">Abra um navegador e conecte-se o endereço IP toohello da página IIS Olá VM tooshow saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-146">Open a browser and connect toohello IP address of hello VM tooshow hello default IIS page.</span></span>

    ![Página da Web padrão do IIS](./media/tutorial-backup-vms/iis-working.png)

2. <span data-ttu-id="dd2fb-148">Conecte-se toohello VM.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-148">Connect toohello VM.</span></span>
3. <span data-ttu-id="dd2fb-149">No hello VM, abra **Explorador de arquivos** e navegue too\inetpub\wwwroot e exclua o arquivo hello **iisstart.png**.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-149">On hello VM, open **File Explorer** and navigate too\inetpub\wwwroot and delete hello file **iisstart.png**.</span></span>
4. <span data-ttu-id="dd2fb-150">No computador local, a atualização Olá navegador toosee que Olá imagem na página IIS padrão Olá será excluída.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-150">On your local computer, refresh hello browser toosee that hello image on hello default IIS page is gone.</span></span>

    ![Página da Web padrão do IIS](./media/tutorial-backup-vms/iis-broken.png)

5. <span data-ttu-id="dd2fb-152">No computador local, abra uma nova guia e vá Olá Olá [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="dd2fb-152">On your local computer, open a new tab and go hello hello [Azure portal](https://portal.azure.com).</span></span>
6. <span data-ttu-id="dd2fb-153">No menu Olá Olá esquerda, selecione **máquinas virtuais** e selecione Olá VM formulário Olá lista.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-153">In hello menu on hello left, select **Virtual machines** and select hello VM form hello list.</span></span>
8. <span data-ttu-id="dd2fb-154">Na folha VM hello, em Olá **configurações** seção, clique em **Backup**.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-154">On hello VM blade, in hello **Settings** section, click **Backup**.</span></span> <span data-ttu-id="dd2fb-155">Olá **Backup** folha é aberta.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-155">hello **Backup** blade opens.</span></span> 
9. <span data-ttu-id="dd2fb-156">No menu de saudação na parte superior de saudação da folha de saudação, selecione **recuperação de arquivo**.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-156">In hello menu at hello top of hello blade, select **File Recovery**.</span></span> <span data-ttu-id="dd2fb-157">Olá **recuperação de arquivo** folha é aberta.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-157">hello **File Recovery** blade opens.</span></span>
10. <span data-ttu-id="dd2fb-158">Em **etapa 1: selecione o ponto de recuperação**, selecione um ponto de recuperação na lista suspensa hello.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-158">In **Step 1: Select recovery point**, select a recovery point from hello drop-down.</span></span>
11. <span data-ttu-id="dd2fb-159">No **etapa 2: baixar o script toobrowse e recuperar arquivos**, clique em hello **executável baixar** botão.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-159">In **Step 2: Download script toobrowse and recover files**, click hello **Download Executable** button.</span></span> <span data-ttu-id="dd2fb-160">Salvar Olá arquivo tooyour **Downloads** pasta.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-160">Save hello file tooyour **Downloads** folder.</span></span>
12. <span data-ttu-id="dd2fb-161">No computador local, abra **Explorador de arquivos** e navegue tooyour **Downloads** Olá pasta e copie o arquivo de .exe baixado.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-161">On your local computer, open **File Explorer** and navigate tooyour **Downloads** folder and copy hello downloaded .exe file.</span></span> <span data-ttu-id="dd2fb-162">nome de arquivo Hello será prefixado pelo nome da sua VM.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-162">hello filename will be prefixed by your VM name.</span></span> 
13. <span data-ttu-id="dd2fb-163">Na sua VM (sobre Olá conexão RDP) cole Olá .exe arquivo toohello área de trabalho da VM.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-163">On your VM (over hello RDP connection) paste hello .exe file toohello Desktop of your VM.</span></span> 
14. <span data-ttu-id="dd2fb-164">Navegue até toohello a área de trabalho da VM e clique duas vezes em .exe hello.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-164">Navigate toohello desktop of your VM and double-click on hello .exe.</span></span> <span data-ttu-id="dd2fb-165">Isso iniciará um prompt de comando e em seguida, monte o ponto de recuperação hello como um compartilhamento de arquivos que você pode acessar.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-165">This will launch a command prompt and then mount hello recovery point as a file share that you can access.</span></span> <span data-ttu-id="dd2fb-166">Quando ele for concluído criar compartilhamento de hello, digite **p** tooclose prompt de comando de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-166">When it is finished creating hello share, type **q** tooclose hello command prompt.</span></span>
15. <span data-ttu-id="dd2fb-167">Em sua VM, abra **Explorador de arquivos** e navegue toohello letra da unidade que foi usada para o compartilhamento de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-167">On your VM, open **File Explorer** and navigate toohello drive letter that was used for hello file share.</span></span>
16. <span data-ttu-id="dd2fb-168">Navegue too\inetpub\wwwroot e cópia **iisstart.png** do arquivo hello compartilhar e cole-o em \Inetpub\Wwwroot..</span><span class="sxs-lookup"><span data-stu-id="dd2fb-168">Navigate too\inetpub\wwwroot and copy **iisstart.png** from hello file share and paste it into \inetpub\wwwroot.</span></span> <span data-ttu-id="dd2fb-169">Por exemplo, copie F:\inetpub\wwwroot\iisstart.png e cole-o em um arquivo de saudação do c:\inetpub\wwwroot toorecover.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-169">For example, copy F:\inetpub\wwwroot\iisstart.png and paste it into c:\inetpub\wwwroot toorecover hello file.</span></span>
17. <span data-ttu-id="dd2fb-170">No computador local, abra a guia do navegador de saudação em que você está conectado toohello endereço IP de saudação VM mostrando Olá IIS padrão a página.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-170">On your local computer, open hello browser tab where you are connected toohello IP address of hello VM showing hello IIS default page.</span></span> <span data-ttu-id="dd2fb-171">Pressione CTRL + F5 página do navegador Olá toorefresh.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-171">Press CTRL + F5 toorefresh hello browser page.</span></span> <span data-ttu-id="dd2fb-172">Agora, você verá que Olá imagem foi restaurada.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-172">You should now see that hello image has been restored.</span></span>
18. <span data-ttu-id="dd2fb-173">No computador local, volte toohello guia do navegador para Olá portal do Azure e na **etapa 3: desmontar discos Olá após a recuperação** clique Olá **desmontar discos** botão.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-173">On your local computer, go back toohello browser tab for hello Azure portal and in **Step 3: Unmount hello disks after recovery** click hello **Unmount Disks** button.</span></span> <span data-ttu-id="dd2fb-174">Se você esquecer toodo nesta etapa, ponto de montagem do hello conexão toohello é fechar automaticamente após 12 horas.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-174">If you forget toodo this step, hello connection toohello mountpoint is automatically close after 12 hours.</span></span> <span data-ttu-id="dd2fb-175">Após as 12 horas, é necessário toodownload um novo toocreate de script um novo ponto de montagem.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-175">After those 12 hours, you need toodownload a new script toocreate a new mountpoint.</span></span>


## <a name="next-steps"></a><span data-ttu-id="dd2fb-176">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dd2fb-176">Next steps</span></span>

<span data-ttu-id="dd2fb-177">Neste tutorial, você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="dd2fb-177">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="dd2fb-178">Criar um backup de uma VM</span><span class="sxs-lookup"><span data-stu-id="dd2fb-178">Create a backup of a VM</span></span>
> * <span data-ttu-id="dd2fb-179">Agendar um backup diário</span><span class="sxs-lookup"><span data-stu-id="dd2fb-179">Schedule a daily backup</span></span>
> * <span data-ttu-id="dd2fb-180">Restaurar um arquivo de um backup</span><span class="sxs-lookup"><span data-stu-id="dd2fb-180">Restore a file from a backup</span></span>

<span data-ttu-id="dd2fb-181">Avançar toohello toolearn próximo de tutorial sobre o monitoramento de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="dd2fb-181">Advance toohello next tutorial toolearn about monitoring virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="dd2fb-182">Monitorar máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="dd2fb-182">Monitor virtual machines</span></span>](tutorial-monitoring.md)









