---
title: aaaReset uma senha local do Windows sem agente do Azure | Microsoft Docs
description: "Como tooreset Olá a senha de uma conta de usuário do Windows local quando o agente de convidado do Azure Olá não está instalado ou funcionando em uma máquina virtual"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: cf353dd3-89c9-47f6-a449-f874f0957013
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 04/07/2017
ms.author: iainfou
ms.openlocfilehash: c559c31ea142f9cf50d2c5b6182c5355fec9bac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-local-windows-password-for-azure-vm"></a><span data-ttu-id="8dd6d-103">Como tooreset senha do Windows local para a máquina virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="8dd6d-103">How tooreset local Windows password for Azure VM</span></span>
<span data-ttu-id="8dd6d-104">Você pode redefinir senha do Windows local saudação de uma VM no Azure usando Olá [portal do Azure ou o Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) desde que o agente de convidado do Azure hello está instalado.</span><span class="sxs-lookup"><span data-stu-id="8dd6d-104">You can reset hello local Windows password of a VM in Azure using hello [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) provided hello Azure guest agent is installed.</span></span> <span data-ttu-id="8dd6d-105">Esse método é Olá principal maneira tooreset uma senha para uma VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="8dd6d-105">This method is hello primary way tooreset a password for an Azure VM.</span></span> <span data-ttu-id="8dd6d-106">Se você tiver problemas com o agente de convidado do Azure Olá não está respondendo ou falhando tooinstall depois de carregar uma imagem personalizada, você pode redefinir manualmente uma senha do Windows.</span><span class="sxs-lookup"><span data-stu-id="8dd6d-106">If you encounter issues with hello Azure guest agent not responding, or failing tooinstall after uploading a custom image, you can manually reset a Windows password.</span></span> <span data-ttu-id="8dd6d-107">Este artigo fornece detalhes sobre como tooreset uma senha de conta local, anexando Olá tooanother de disco virtual de origem SO VM.</span><span class="sxs-lookup"><span data-stu-id="8dd6d-107">This article details how tooreset a local account password by attaching hello source OS virtual disk tooanother VM.</span></span> 

> [!WARNING]
> <span data-ttu-id="8dd6d-108">Use esse processo apenas como último recurso.</span><span class="sxs-lookup"><span data-stu-id="8dd6d-108">Only use this process as a last resort.</span></span> <span data-ttu-id="8dd6d-109">Tente tooreset sempre uma senha usando Olá [portal do Azure ou o Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) primeiro.</span><span class="sxs-lookup"><span data-stu-id="8dd6d-109">Always try tooreset a password using hello [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) first.</span></span>
> 
> 

## <a name="overview-of-hello-process"></a><span data-ttu-id="8dd6d-110">Visão geral do processo de saudação</span><span class="sxs-lookup"><span data-stu-id="8dd6d-110">Overview of hello process</span></span>
<span data-ttu-id="8dd6d-111">etapas de núcleo Olá para executar uma redefinição para uma VM do Windows Azure quando não há nenhum agente de convidado do Azure toohello acesso de senha local é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="8dd6d-111">hello core steps for performing a local password reset for a Windows VM in Azure when there is no access toohello Azure guest agent is as follows:</span></span>

* <span data-ttu-id="8dd6d-112">Exclua VM de origem hello.</span><span class="sxs-lookup"><span data-stu-id="8dd6d-112">Delete hello source VM.</span></span> <span data-ttu-id="8dd6d-113">discos virtuais Olá são mantidos.</span><span class="sxs-lookup"><span data-stu-id="8dd6d-113">hello virtual disks are retained.</span></span>
* <span data-ttu-id="8dd6d-114">Anexar tooanother disco de sistema operacional da VM de origem Olá VM em Olá mesmo local dentro de sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="8dd6d-114">Attach hello source VM's OS disk tooanother VM on hello same location within your Azure subscription.</span></span> <span data-ttu-id="8dd6d-115">Essa VM é chamado tooas Olá VM de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="8dd6d-115">This VM is referred tooas hello troubleshooting VM.</span></span>
* <span data-ttu-id="8dd6d-116">Usando Olá VM de solução de problemas, crie alguns arquivos de configuração no disco do sistema operacional da VM de origem hello.</span><span class="sxs-lookup"><span data-stu-id="8dd6d-116">Using hello troubleshooting VM, create some config files on hello source VM's OS disk.</span></span>
* <span data-ttu-id="8dd6d-117">Desanexe o disco do sistema operacional da VM de saudação do hello VM de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="8dd6d-117">Detach hello VM's OS disk from hello troubleshooting VM.</span></span>
* <span data-ttu-id="8dd6d-118">Use um modelo de Gerenciador de recursos toocreate uma VM, usando o disco virtual original de saudação.</span><span class="sxs-lookup"><span data-stu-id="8dd6d-118">Use a Resource Manager template toocreate a VM, using hello original virtual disk.</span></span>
* <span data-ttu-id="8dd6d-119">Quando a nova VM é inicializado, Olá Olá arquivos de configuração cria Olá de atualização de senha do usuário Olá necessário.</span><span class="sxs-lookup"><span data-stu-id="8dd6d-119">When hello new VM boots, hello config files you create update hello password of hello required user.</span></span>

## <a name="detailed-steps"></a><span data-ttu-id="8dd6d-120">Etapas detalhadas</span><span class="sxs-lookup"><span data-stu-id="8dd6d-120">Detailed steps</span></span>
<span data-ttu-id="8dd6d-121">Tente tooreset sempre uma senha usando Olá [portal do Azure ou o Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) antes de tentar Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="8dd6d-121">Always try tooreset a password using hello [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before trying hello following steps.</span></span> <span data-ttu-id="8dd6d-122">Verifique se você tem um backup da VM antes de iniciar.</span><span class="sxs-lookup"><span data-stu-id="8dd6d-122">Make sure you have a backup of your VM before you start.</span></span> 

1. <span data-ttu-id="8dd6d-123">Excluir Olá afetados VM no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8dd6d-123">Delete hello affected VM in Azure portal.</span></span> <span data-ttu-id="8dd6d-124">Excluindo Olá VM exclui somente metadados hello, referência de saudação do hello VM no Azure.</span><span class="sxs-lookup"><span data-stu-id="8dd6d-124">Deleting hello VM only deletes hello metadata, hello reference of hello VM within Azure.</span></span> <span data-ttu-id="8dd6d-125">discos virtuais Olá são mantidos quando Olá VM é excluída:</span><span class="sxs-lookup"><span data-stu-id="8dd6d-125">hello virtual disks are retained when hello VM is deleted:</span></span>
   
   * <span data-ttu-id="8dd6d-126">Selecione Olá VM em Olá portal do Azure, clique em *excluir*:</span><span class="sxs-lookup"><span data-stu-id="8dd6d-126">Select hello VM in hello Azure portal, click *Delete*:</span></span>
     
     ![Excluir VM existente](./media/reset-local-password-without-agent/delete_vm.png)
2. <span data-ttu-id="8dd6d-128">Anexe toohello de disco do sistema operacional da VM de origem Olá VM de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="8dd6d-128">Attach hello source VM’s OS disk toohello troubleshooting VM.</span></span> <span data-ttu-id="8dd6d-129">Olá Solucionando problemas de VM deve estar no hello mesma região que o disco do sistema operacional da VM de origem hello (como `West US`):</span><span class="sxs-lookup"><span data-stu-id="8dd6d-129">hello troubleshooting VM must be in hello same region as hello source VM's OS disk (such as `West US`):</span></span>
   
   * <span data-ttu-id="8dd6d-130">Selecione Olá VM de solução de problemas no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8dd6d-130">Select hello troubleshooting VM in hello Azure portal.</span></span> <span data-ttu-id="8dd6d-131">Clique em *Discos* | *Anexar existente*:</span><span class="sxs-lookup"><span data-stu-id="8dd6d-131">Click *Disks* | *Attach existing*:</span></span>
     
     ![Anexar disco existente](./media/reset-local-password-without-agent/disks_attach_existing.png)
     
     <span data-ttu-id="8dd6d-133">Selecione *arquivo VHD* e, em seguida, selecione conta de armazenamento de saudação que contém seu VM de origem:</span><span class="sxs-lookup"><span data-stu-id="8dd6d-133">Select *VHD File* and then select hello storage account that contains your source VM:</span></span>
     
     ![Escolher conta de armazenamento](./media/reset-local-password-without-agent/disks_select_storageaccount.PNG)
     
     <span data-ttu-id="8dd6d-135">Selecione o recipiente de origem hello.</span><span class="sxs-lookup"><span data-stu-id="8dd6d-135">Select hello source container.</span></span> <span data-ttu-id="8dd6d-136">contêiner de origem Olá normalmente é *vhds*:</span><span class="sxs-lookup"><span data-stu-id="8dd6d-136">hello source container is typically *vhds*:</span></span>
     
     ![Escolher contêiner de armazenamento](./media/reset-local-password-without-agent/disks_select_container.png)
     
     <span data-ttu-id="8dd6d-138">Selecione Olá tooattach de vhd de sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="8dd6d-138">Select hello OS vhd tooattach.</span></span> <span data-ttu-id="8dd6d-139">Clique em *selecione* toocomplete processo de saudação:</span><span class="sxs-lookup"><span data-stu-id="8dd6d-139">Click *Select* toocomplete hello process:</span></span>
     
     ![Escolher o disco virtual de origem](./media/reset-local-password-without-agent/disks_select_source_vhd.png)
3. <span data-ttu-id="8dd6d-141">Conecte-se toohello VM usando a área de trabalho remota de solução de problemas e certifique-se de disco do sistema operacional da VM de origem Olá é visível:</span><span class="sxs-lookup"><span data-stu-id="8dd6d-141">Connect toohello troubleshooting VM using Remote Desktop and ensure hello source VM's OS disk is visible:</span></span>
   
   * <span data-ttu-id="8dd6d-142">Selecione Olá VM de solução de problemas no hello portal do Azure e clique em *conectar*.</span><span class="sxs-lookup"><span data-stu-id="8dd6d-142">Select hello troubleshooting VM in hello Azure portal and click *Connect*.</span></span>
   * <span data-ttu-id="8dd6d-143">Abrir arquivo RDP Olá que baixa.</span><span class="sxs-lookup"><span data-stu-id="8dd6d-143">Open hello RDP file that downloads.</span></span> <span data-ttu-id="8dd6d-144">Insira a saudação de nome de usuário e a senha da saudação VM de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="8dd6d-144">Enter hello username and password of hello troubleshooting VM.</span></span>
   * <span data-ttu-id="8dd6d-145">No Explorador de arquivos, procure o disco de dados Olá anexado.</span><span class="sxs-lookup"><span data-stu-id="8dd6d-145">In File Explorer, look for hello data disk you attached.</span></span> <span data-ttu-id="8dd6d-146">Se hello fonte que VHD da VM é hello somente os dados em disco anexado toohello VM de solução de problemas, ele deverá ser unidade f: de saudação:</span><span class="sxs-lookup"><span data-stu-id="8dd6d-146">If hello source VM’s VHD is hello only data disk attached toohello troubleshooting VM, it should be hello F: drive:</span></span>
     
     ![Exibir o disco de dados anexado](./media/reset-local-password-without-agent/troubleshooting_vm_fileexplorer.png)
4. <span data-ttu-id="8dd6d-148">Criar `gpt.ini` em `\Windows\System32\GroupPolicy` na unidade da VM de origem hello (se existir gpt.ini, renomeie toogpt.ini.bak):</span><span class="sxs-lookup"><span data-stu-id="8dd6d-148">Create `gpt.ini` in `\Windows\System32\GroupPolicy` on hello source VM’s drive (if gpt.ini exists, rename toogpt.ini.bak):</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="8dd6d-149">Certifique-se de não acidentalmente criar hello seguintes arquivos em C:\Windows, Olá unidade do sistema operacional para Olá VM de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="8dd6d-149">Make sure that you do not accidentally create hello following files in C:\Windows, hello OS drive for hello troubleshooting VM.</span></span> <span data-ttu-id="8dd6d-150">Crie hello seguintes arquivos na unidade de saudação SO para sua VM que está anexado como um disco de dados de origem.</span><span class="sxs-lookup"><span data-stu-id="8dd6d-150">Create hello following files in hello OS drive for your source VM that is attached as a data disk.</span></span>
   > 
   > 
   
   * <span data-ttu-id="8dd6d-151">Adicionar Olá linhas seguintes no hello `gpt.ini` arquivo criado:</span><span class="sxs-lookup"><span data-stu-id="8dd6d-151">Add hello following lines into hello `gpt.ini` file you created:</span></span>
     
     ```
     [General]
     gPCFunctionalityVersion=2
     gPCMachineExtensionNames=[{42B5FAAE-6536-11D2-AE5A-0000F87571E3}{40B6664F-4972-11D1-A7CA-0000F87571E3}]
     Version=1
     ```
     
     ![Criar gpt.ini](./media/reset-local-password-without-agent/create_gpt_ini.png)
5. <span data-ttu-id="8dd6d-153">Crie `scripts.ini` em `\Windows\System32\GroupPolicy\Machine\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="8dd6d-153">Create `scripts.ini` in `\Windows\System32\GroupPolicy\Machine\Scripts`.</span></span> <span data-ttu-id="8dd6d-154">Verifique se as pastas ocultas são mostradas.</span><span class="sxs-lookup"><span data-stu-id="8dd6d-154">Make sure hidden folders are shown.</span></span> <span data-ttu-id="8dd6d-155">Se necessário, crie Olá `Machine` ou `Scripts` pastas.</span><span class="sxs-lookup"><span data-stu-id="8dd6d-155">If needed, create hello `Machine` or `Scripts` folders.</span></span>
   
   * <span data-ttu-id="8dd6d-156">Adicionar Olá Olá linhas a seguir `scripts.ini` arquivo criado:</span><span class="sxs-lookup"><span data-stu-id="8dd6d-156">Add hello following lines hello `scripts.ini` file you created:</span></span>
     
     ```
     [Startup]
     0CmdLine=C:\Windows\System32\FixAzureVM.cmd
     0Parameters=
     ```
     
     ![Criar scripts.ini](./media/reset-local-password-without-agent/create_scripts_ini.png)
6. <span data-ttu-id="8dd6d-158">Criar `FixAzureVM.cmd` na `\Windows\System32` com hello conteúdo a seguir, substituindo `<username>` e `<newpassword>` com seus próprios valores:</span><span class="sxs-lookup"><span data-stu-id="8dd6d-158">Create `FixAzureVM.cmd` in `\Windows\System32` with hello following contents, replacing `<username>` and `<newpassword>` with your own values:</span></span>
   
    ```
    net user <username> <newpassword> /add
    net localgroup administrators <username> /add
    net localgroup "remote desktop users" <username> /add

    ```

    ![Criar FixAzureVM.cmd](./media/reset-local-password-without-agent/create_fixazure_cmd.png)
   
    <span data-ttu-id="8dd6d-160">Você deve atender aos requisitos de complexidade de senha Olá configurado para sua VM ao definir a nova senha de saudação.</span><span class="sxs-lookup"><span data-stu-id="8dd6d-160">You must meet hello configured password complexity requirements for your VM when defining hello new password.</span></span>
7. <span data-ttu-id="8dd6d-161">No portal do Azure, Desanexe o disco de saudação do hello VM de solução de problemas:</span><span class="sxs-lookup"><span data-stu-id="8dd6d-161">In Azure portal, detach hello disk from hello troubleshooting VM:</span></span>
   
   * <span data-ttu-id="8dd6d-162">Selecione Olá VM de solução de problemas no hello portal do Azure, clique em *discos*.</span><span class="sxs-lookup"><span data-stu-id="8dd6d-162">Select hello troubleshooting VM in hello Azure portal, click *Disks*.</span></span>
   * <span data-ttu-id="8dd6d-163">Disco de dados selecione Olá anexado na etapa 2, clique em *desanexar*:</span><span class="sxs-lookup"><span data-stu-id="8dd6d-163">Select hello data disk attached in step 2, click *Detach*:</span></span>
     
     ![Desanexar disco](./media/reset-local-password-without-agent/detach_disk.png)
8. <span data-ttu-id="8dd6d-165">Antes de criar uma máquina virtual, obtenha o disco do sistema operacional de origem do hello URI tooyour:</span><span class="sxs-lookup"><span data-stu-id="8dd6d-165">Before you create a VM, obtain hello URI tooyour source OS disk:</span></span>
   
   * <span data-ttu-id="8dd6d-166">Conta de armazenamento selecione Olá Olá portal do Azure, clique em *Blobs*.</span><span class="sxs-lookup"><span data-stu-id="8dd6d-166">Select hello storage account in hello Azure portal, click *Blobs*.</span></span>
   * <span data-ttu-id="8dd6d-167">Selecione o contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="8dd6d-167">Select hello container.</span></span> <span data-ttu-id="8dd6d-168">contêiner de origem Olá normalmente é *vhds*:</span><span class="sxs-lookup"><span data-stu-id="8dd6d-168">hello source container is typically *vhds*:</span></span>
     
     ![Selecionar o blob da conta de armazenamento](./media/reset-local-password-without-agent/select_storage_details.png)
     
     <span data-ttu-id="8dd6d-170">Selecione a fonte de VHD de sistema operacional da máquina virtual e clique em Olá *cópia* toohello próximo botão *URL* nome:</span><span class="sxs-lookup"><span data-stu-id="8dd6d-170">Select your source VM OS VHD and click hello *Copy* button next toohello *URL* name:</span></span>
     
     ![Copiar URI do disco](./media/reset-local-password-without-agent/copy_source_vhd_uri.png)
9. <span data-ttu-id="8dd6d-172">Crie uma máquina virtual do disco do sistema operacional da VM de origem hello:</span><span class="sxs-lookup"><span data-stu-id="8dd6d-172">Create a VM from hello source VM’s OS disk:</span></span>
   
   * <span data-ttu-id="8dd6d-173">Use [este modelo do Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) toocreate uma VM em um VHD especializada.</span><span class="sxs-lookup"><span data-stu-id="8dd6d-173">Use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) toocreate a VM from a specialized VHD.</span></span> <span data-ttu-id="8dd6d-174">Clique em Olá `Deploy tooAzure` saudação do botão tooopen portal do Azure com os detalhes do modelo Olá preenchido para você.</span><span class="sxs-lookup"><span data-stu-id="8dd6d-174">Click hello `Deploy tooAzure` button tooopen hello Azure portal with hello templated details populated for you.</span></span>
   * <span data-ttu-id="8dd6d-175">Se você desejar tooretain todas as configurações anteriores de saudação para Olá VM, selecione *Editar modelo* tooprovide sua rede virtual existente, sub-rede, adaptador de rede ou IP público.</span><span class="sxs-lookup"><span data-stu-id="8dd6d-175">If you want tooretain all hello previous settings for hello VM, select *Edit template* tooprovide your existing VNet, subnet, network adapter, or public IP.</span></span>
   * <span data-ttu-id="8dd6d-176">Em Olá `OSDISKVHDURI` caixa de texto de parâmetro, Olá colar URI de sua fonte de VHD obter Olá anterior etapa:</span><span class="sxs-lookup"><span data-stu-id="8dd6d-176">In hello `OSDISKVHDURI` parameter text box, paste hello URI of your source VHD obtain in hello preceding step:</span></span>
     
     ![Criar uma VM usando o modelo](./media/reset-local-password-without-agent/create_new_vm_from_template.png)
10. <span data-ttu-id="8dd6d-178">Após Olá nova máquina virtual está em execução, conecte-se toohello VM usando a área de trabalho remota com hello a nova senha especificada no hello `FixAzureVM.cmd` script.</span><span class="sxs-lookup"><span data-stu-id="8dd6d-178">After hello new VM is running, connect toohello VM using Remote Desktop with hello new password you specified in hello `FixAzureVM.cmd` script.</span></span>
11. <span data-ttu-id="8dd6d-179">Na sua sessão remota toohello nova VM, Olá remove a seguir arquivos tooclean ambiente hello:</span><span class="sxs-lookup"><span data-stu-id="8dd6d-179">From your remote session toohello new VM, remove hello following files tooclean up hello environment:</span></span>
    
    * <span data-ttu-id="8dd6d-180">De %windir%\System32</span><span class="sxs-lookup"><span data-stu-id="8dd6d-180">From %windir%\System32</span></span>
      * <span data-ttu-id="8dd6d-181">remova FixAzureVM.cmd</span><span class="sxs-lookup"><span data-stu-id="8dd6d-181">remove FixAzureVM.cmd</span></span>
    * <span data-ttu-id="8dd6d-182">De %windir%\System32\GroupPolicy\Machine\\</span><span class="sxs-lookup"><span data-stu-id="8dd6d-182">From %windir%\System32\GroupPolicy\Machine\\</span></span>
      * <span data-ttu-id="8dd6d-183">remova scripts.ini</span><span class="sxs-lookup"><span data-stu-id="8dd6d-183">remove scripts.ini</span></span>
    * <span data-ttu-id="8dd6d-184">De %windir%\System32\GroupPolicy</span><span class="sxs-lookup"><span data-stu-id="8dd6d-184">From %windir%\System32\GroupPolicy</span></span>
      * <span data-ttu-id="8dd6d-185">Remover gpt.ini (se gpt.ini existia antes, e você renomeou toogpt.ini.bak, renomeação hello. bak arquivo back toogpt.ini)</span><span class="sxs-lookup"><span data-stu-id="8dd6d-185">remove gpt.ini (if gpt.ini existed before, and you renamed it toogpt.ini.bak, rename hello .bak file back toogpt.ini)</span></span>

## <a name="next-steps"></a><span data-ttu-id="8dd6d-186">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8dd6d-186">Next steps</span></span>
<span data-ttu-id="8dd6d-187">Se você ainda não é possível se conectar usando a área de trabalho remota, consulte Olá [guia de solução de problemas de RDP](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8dd6d-187">If you still cannot connect using Remote Desktop, see hello [RDP troubleshooting guide](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="8dd6d-188">Olá [detalhadas RDP guia de solução de problemas](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) examina métodos em vez de etapas específicas de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="8dd6d-188">hello [detailed RDP troubleshooting guide](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) looks at troubleshooting methods rather than specific steps.</span></span> <span data-ttu-id="8dd6d-189">Você também pode [abrir uma solicitação de suporte do Azure](https://azure.microsoft.com/support/options/) para obter assistência prática.</span><span class="sxs-lookup"><span data-stu-id="8dd6d-189">You can also [open an Azure support request](https://azure.microsoft.com/support/options/) for hands-on assistance.</span></span>

