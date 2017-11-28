---
title: aaaInstall IIS em sua primeira VM do Windows | Microsoft Docs
description: "Testar sua primeira máquina virtual do Windows instalando o IIS e abrindo a porta 80 usando Olá portal do Azure."
keywords: 
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6334ea45-db6b-4e08-abb5-1f98927ebc34
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: cynthn
ms.openlocfilehash: 7cfed6197df058c4569d111ee88961da7c6fe0b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="experiment-with-installing-a-role-on-your-windows-vm"></a><span data-ttu-id="6d473-103">Experimentar a instalação de uma função em sua VM do Windows</span><span class="sxs-lookup"><span data-stu-id="6d473-103">Experiment with installing a role on your Windows VM</span></span>
<span data-ttu-id="6d473-104">Uma vez que a sua primeira máquina virtual (VM) para cima e em execução, você pode mover tooinstalling softwares e serviços.</span><span class="sxs-lookup"><span data-stu-id="6d473-104">Once you have your first virtual machine (VM) up and running, you can move on tooinstalling software and services.</span></span> <span data-ttu-id="6d473-105">Para este tutorial, vamos toouse Gerenciador do servidor em Olá tooinstall de VM do Windows Server IIS.</span><span class="sxs-lookup"><span data-stu-id="6d473-105">For this tutorial, we are going toouse Server Manager on hello Windows Server VM tooinstall IIS.</span></span> <span data-ttu-id="6d473-106">Em seguida, vamos criar um grupo de segurança de rede (NSG) usando o tráfego do hello tooopen portal do Azure na porta 80 tooIIS.</span><span class="sxs-lookup"><span data-stu-id="6d473-106">Then, we will create a Network Security Group (NSG) using hello Azure portal tooopen port 80 tooIIS traffic.</span></span> 

<span data-ttu-id="6d473-107">Se você ainda não criou sua primeira VM, você deverá voltar muito[criar sua primeira máquina virtual do Windows no portal do Azure de saudação](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) antes de continuar com este tutorial.</span><span class="sxs-lookup"><span data-stu-id="6d473-107">If you haven't already created your first VM, you should go back too[Create your first Windows virtual machine in hello Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before continuing with this tutorial.</span></span>

## <a name="make-sure-hello-vm-is-running"></a><span data-ttu-id="6d473-108">Verifique se Olá que VM está em execução</span><span class="sxs-lookup"><span data-stu-id="6d473-108">Make sure hello VM is running</span></span>
1. <span data-ttu-id="6d473-109">Olá abrir [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6d473-109">Open hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6d473-110">No menu de hub hello, clique em **máquinas virtuais**.</span><span class="sxs-lookup"><span data-stu-id="6d473-110">On hello hub menu, click **Virtual Machines**.</span></span> <span data-ttu-id="6d473-111">Selecione máquina virtual de Olá Olá lista.</span><span class="sxs-lookup"><span data-stu-id="6d473-111">Select hello virtual machine from hello list.</span></span>
3. <span data-ttu-id="6d473-112">Se o status de saudação é **parado (desalocado)**, clique Olá **iniciar** botão Olá **Essentials** folha de saudação VM.</span><span class="sxs-lookup"><span data-stu-id="6d473-112">If hello status is **Stopped (Deallocated)**, click hello **Start** button on hello **Essentials** blade of hello VM.</span></span> <span data-ttu-id="6d473-113">Se o status de saudação é **executando**, você pode mover toohello próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="6d473-113">If hello status is **Running**, you can move on toohello next step.</span></span>

## <a name="connect-toohello-virtual-machine-and-sign-in"></a><span data-ttu-id="6d473-114">Conecte-se a máquina virtual de toohello e entrar</span><span class="sxs-lookup"><span data-stu-id="6d473-114">Connect toohello virtual machine and sign in</span></span>
1. <span data-ttu-id="6d473-115">No menu de hub hello, clique em **máquinas virtuais**.</span><span class="sxs-lookup"><span data-stu-id="6d473-115">On hello hub menu, click **Virtual Machines**.</span></span> <span data-ttu-id="6d473-116">Selecione máquina virtual de Olá Olá lista.</span><span class="sxs-lookup"><span data-stu-id="6d473-116">Select hello virtual machine from hello list.</span></span>
2. <span data-ttu-id="6d473-117">Na folha de saudação para a máquina virtual de saudação, clique em **conectar**.</span><span class="sxs-lookup"><span data-stu-id="6d473-117">On hello blade for hello virtual machine, click **Connect**.</span></span> <span data-ttu-id="6d473-118">Isso cria e baixa um arquivo de protocolo de área de trabalho remota (arquivo. rdp) que é como uma máquina de tooyour de tooconnect de atalho.</span><span class="sxs-lookup"><span data-stu-id="6d473-118">This creates and downloads a Remote Desktop Protocol file (.rdp file) that is like a shortcut tooconnect tooyour machine.</span></span> <span data-ttu-id="6d473-119">Talvez você queira área de trabalho do toosave Olá arquivo tooyour para facilitar o acesso.</span><span class="sxs-lookup"><span data-stu-id="6d473-119">You might want toosave hello file tooyour desktop for easy access.</span></span> <span data-ttu-id="6d473-120">**Abra** tooyour de tooconnect este arquivo VM.</span><span class="sxs-lookup"><span data-stu-id="6d473-120">**Open** this file tooconnect tooyour VM.</span></span>
   
    ![Captura de tela da saudação mostrando portal do Azure como tooconnect tooyour VM](./media/hero-role/connect.png)
3. <span data-ttu-id="6d473-122">Você receberá um aviso que. rdp de saudação for de um editor desconhecido.</span><span class="sxs-lookup"><span data-stu-id="6d473-122">You get a warning that hello .rdp is from an unknown publisher.</span></span> <span data-ttu-id="6d473-123">Isso é normal.</span><span class="sxs-lookup"><span data-stu-id="6d473-123">This is normal.</span></span> <span data-ttu-id="6d473-124">Na janela de área de trabalho remota hello, clique em **conectar** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="6d473-124">In hello Remote Desktop window, click **Connect** toocontinue.</span></span>
   
    ![Captura de tela de um aviso sobre um editor desconhecido](./media/hero-role/rdp-warn.png)
4. <span data-ttu-id="6d473-126">Na janela de segurança do Windows hello, nome de usuário do tipo hello e a senha da conta de local de saudação que é criada quando você criou Olá VM.</span><span class="sxs-lookup"><span data-stu-id="6d473-126">In hello Windows Security window, type hello username and password for hello local account that you created when you created hello VM.</span></span> <span data-ttu-id="6d473-127">nome de usuário de saudação é inserido como *vmname*&#92; *nome de usuário*, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="6d473-127">hello username is entered as *vmname*&#92;*username*, then click **OK**.</span></span>
   
    ![Captura de tela de inserir o nome da VM Olá, nome de usuário e senha](./media/hero-role/credentials.png)
5. <span data-ttu-id="6d473-129">Receber um aviso de certificado Olá não pode ser verificado.</span><span class="sxs-lookup"><span data-stu-id="6d473-129">You get a warning that hello certificate cannot be verified.</span></span> <span data-ttu-id="6d473-130">Isso é normal.</span><span class="sxs-lookup"><span data-stu-id="6d473-130">This is normal.</span></span> <span data-ttu-id="6d473-131">Clique em **Sim** tooverify Olá identidade da máquina virtual de saudação e concluir o registro em log.</span><span class="sxs-lookup"><span data-stu-id="6d473-131">Click **Yes** tooverify hello identity of hello virtual machine and finish logging on.</span></span>
   
   ![Captura de tela mostrando uma mensagem limitam a verificar a identidade de saudação do hello VM](./media/hero-role/cert-warning.png)

<span data-ttu-id="6d473-133">Se você executar tootrouble quando você tentar tooconnect, consulte [tooa conexões de solucionar problemas de área de trabalho remota baseado no Windows Azure Virtual Machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6d473-133">If you run in tootrouble when you try tooconnect, see [Troubleshoot Remote Desktop connections tooa Windows-based Azure Virtual Machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="install-iis-on-your-vm"></a><span data-ttu-id="6d473-134">Instalar o IIS em sua VM</span><span class="sxs-lookup"><span data-stu-id="6d473-134">Install IIS on your VM</span></span>
<span data-ttu-id="6d473-135">Agora que você está logado toohello VM, vamos instalar uma função de servidor para que você possa testar mais.</span><span class="sxs-lookup"><span data-stu-id="6d473-135">Now that you are logged in toohello VM, we will install a server role so that you can experiment more.</span></span>

1. <span data-ttu-id="6d473-136">Abra o **Gerenciador de Servidores** se ainda não estiver aberto.</span><span class="sxs-lookup"><span data-stu-id="6d473-136">Open **Server Manager** if it isn't already open.</span></span> <span data-ttu-id="6d473-137">Clique em Olá **iniciar** menu e clique **Gerenciador do servidor**.</span><span class="sxs-lookup"><span data-stu-id="6d473-137">Click hello **Start** menu, and then click **Server Manager**.</span></span>
2. <span data-ttu-id="6d473-138">Em **Gerenciador do servidor**, selecione **servidor Local** no painel esquerdo do hello.</span><span class="sxs-lookup"><span data-stu-id="6d473-138">In **Server Manager**, select **Local Server** from hello left pane.</span></span> 
3. <span data-ttu-id="6d473-139">No menu de saudação, selecione **gerenciar** > **adicionar funções e recursos**.</span><span class="sxs-lookup"><span data-stu-id="6d473-139">In hello menu, select **Manage** > **Add Roles and Features**.</span></span>
4. <span data-ttu-id="6d473-140">Em Olá assistente Adicionar funções e recursos, em Olá **tipo de instalação** escolha **instalação baseada em função ou recurso**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="6d473-140">In hello Add Roles and Features Wizard, on hello **Installation Type** page, choose **Role-based or feature-based installation**, and then click **Next**.</span></span>
   
    ![Captura de tela mostrando Olá assistente Adicionar funções e recursos de guia para o tipo de instalação](./media/hero-role/role-wizard.png)
5. <span data-ttu-id="6d473-142">Selecione Olá VM do pool de saudação do servidor e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="6d473-142">Select hello VM from hello server pool and click **Next**.</span></span>
6. <span data-ttu-id="6d473-143">Em Olá **funções de servidor** página, selecione **servidor Web (IIS)**.</span><span class="sxs-lookup"><span data-stu-id="6d473-143">On hello **Server Roles** page, select **Web Server (IIS)**.</span></span>
   
    ![Captura de tela mostrando Olá assistente Adicionar funções e recursos do guia de funções de servidor](./media/hero-role/add-iis.png)
7. <span data-ttu-id="6d473-145">No hello pop-up sobre como adicionar recursos necessários para o IIS, verifique se **incluir ferramentas de gerenciamento** está selecionado e, em seguida, clique em **adicionar recursos**.</span><span class="sxs-lookup"><span data-stu-id="6d473-145">In hello pop-up about adding features needed for IIS, make sure that **Include management tools** is selected and then click **Add Features**.</span></span> <span data-ttu-id="6d473-146">Quando fecha Olá pop-up, clique em **próximo** no Assistente de saudação.</span><span class="sxs-lookup"><span data-stu-id="6d473-146">When hello pop-up closes, click **Next** in hello wizard.</span></span>
   
    ![Captura de tela mostrando tooconfirm pop-up, adicionando a função do IIS Olá](./media/hero-role/confirm-add-feature.png)
8. <span data-ttu-id="6d473-148">Na página de recursos de saudação, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="6d473-148">On hello features page, click **Next**.</span></span>
9. <span data-ttu-id="6d473-149">Em Olá **função de servidor Web (IIS)** , clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="6d473-149">On hello **Web Server Role (IIS)** page, click **Next**.</span></span> 
10. <span data-ttu-id="6d473-150">Em Olá **serviços de função** , clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="6d473-150">On hello **Role Services** page, click **Next**.</span></span> 
11. <span data-ttu-id="6d473-151">Em Olá **confirmação** , clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="6d473-151">On hello **Confirmation** page, click **Install**.</span></span> 
12. <span data-ttu-id="6d473-152">Quando a saudação instalação for concluída, clique em **fechar** no Assistente de saudação.</span><span class="sxs-lookup"><span data-stu-id="6d473-152">When hello installation is complete, click **Close** on hello wizard.</span></span>

## <a name="open-port-80"></a><span data-ttu-id="6d473-153">Abrir a porta 80</span><span class="sxs-lookup"><span data-stu-id="6d473-153">Open port 80</span></span>
<span data-ttu-id="6d473-154">Para que sua VM tooaccept o tráfego de entrada pela porta 80, é necessário tooadd um grupo de segurança de rede de toohello regra de entrada.</span><span class="sxs-lookup"><span data-stu-id="6d473-154">In order for your VM tooaccept inbound traffic over port 80, you need tooadd an inbound rule toohello network security group.</span></span> 

1. <span data-ttu-id="6d473-155">Olá abrir [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6d473-155">Open hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6d473-156">Em **máquinas virtuais** selecione Olá VM que você criou.</span><span class="sxs-lookup"><span data-stu-id="6d473-156">In **Virtual machines** select hello VM that you created.</span></span>
3. <span data-ttu-id="6d473-157">Em configurações de máquinas virtuais hello, selecione **interfaces de rede** e, em seguida, selecione Olá interface de rede existente.</span><span class="sxs-lookup"><span data-stu-id="6d473-157">In hello virtual machines settings, select **Network interfaces** and then select hello existing network interface.</span></span>
   
    ![Captura de tela mostrando a configuração de máquina virtual de saudação para Olá interfaces de rede](./media/hero-role/network-interface.png)
4. <span data-ttu-id="6d473-159">Em **Essentials** Olá interface de rede, clique em Olá **grupo de segurança de rede**.</span><span class="sxs-lookup"><span data-stu-id="6d473-159">In **Essentials** for hello network interface, click hello **Network security group**.</span></span>
   
    ![Captura de tela mostrando a seção do Essentials Olá Olá interface de rede](./media/hero-role/select-nsg.png)
5. <span data-ttu-id="6d473-161">Em Olá **Essentials** folha para Olá NSG, você deve ter um padrão existente regra de entrada de **rdp permitir padrão** que permite que você toolog em toohello VM.</span><span class="sxs-lookup"><span data-stu-id="6d473-161">In hello **Essentials** blade for hello NSG, you should have one existing default inbound rule for **default-allow-rdp** which allows you toolog in toohello VM.</span></span> <span data-ttu-id="6d473-162">Adicione outro tráfego IIS tooallow de regra de entrada.</span><span class="sxs-lookup"><span data-stu-id="6d473-162">You will add another inbound rule tooallow IIS traffic.</span></span> <span data-ttu-id="6d473-163">Clique em **Regra de segurança de entrada**.</span><span class="sxs-lookup"><span data-stu-id="6d473-163">Click **Inbound security rule**.</span></span>
   
    ![Captura de tela mostrando a seção Essentials Olá Olá NSG](./media/hero-role/inbound.png)
6. <span data-ttu-id="6d473-165">Nas **Regras de segurança de entrada**, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6d473-165">In **Inbound security rules**, click **Add**.</span></span>
   
    ![Captura de tela mostrando Olá botão tooadd uma regra de segurança](./media/hero-role/add-rule.png)
7. <span data-ttu-id="6d473-167">Nas **Regras de segurança de entrada**, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6d473-167">In **Inbound security rules**, click **Add**.</span></span> <span data-ttu-id="6d473-168">Tipo **80** em Olá intervalo de portas e certifique-se de **permitir** está selecionado.</span><span class="sxs-lookup"><span data-stu-id="6d473-168">Type **80** in hello port range and make sure **Allow** is selected.</span></span> <span data-ttu-id="6d473-169">Quando terminar, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="6d473-169">When you are done, click **OK**.</span></span>
   
    ![Captura de tela mostrando Olá botão tooadd uma regra de segurança](./media/hero-role/port-80.png)

<span data-ttu-id="6d473-171">Para obter mais informações sobre os NSGs, regras de entrada e saída, consulte [permitir acesso externo tooyour VM usando Olá portal do Azure](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="6d473-171">For more information about NSGs, inbound and outbound rules, see [Allow external access tooyour VM using hello Azure portal](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

## <a name="connect-toohello-default-iis-website"></a><span data-ttu-id="6d473-172">Conecte-se o site do IIS padrão toohello</span><span class="sxs-lookup"><span data-stu-id="6d473-172">Connect toohello default IIS website</span></span>
1. <span data-ttu-id="6d473-173">No portal do Azure de Olá, clique em **máquinas virtuais** e, em seguida, selecione a VM.</span><span class="sxs-lookup"><span data-stu-id="6d473-173">In hello Azure portal, click **Virtual machines** and then select your VM.</span></span>
2. <span data-ttu-id="6d473-174">Em Olá **Essentials** folha, copie o **endereço IP público**.</span><span class="sxs-lookup"><span data-stu-id="6d473-174">In hello **Essentials** blade, copy your **Public IP address**.</span></span>
   
    ![Captura de tela mostrando onde toofind Olá endereço IP público da VM](./media/hero-role/ipaddress.png)
3. <span data-ttu-id="6d473-176">Abra um navegador e na barra de endereços do hello, digite em seu endereço IP público como este: http://<publicIPaddress> e clique em **Enter** toogo toothat endereço.</span><span class="sxs-lookup"><span data-stu-id="6d473-176">Open a browser and in hello address bar, type in your public IP address like this: http://<publicIPaddress> and click **Enter** toogo toothat address.</span></span>
4. <span data-ttu-id="6d473-177">Seu navegador deve abrir a página de web IIS saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="6d473-177">Your browser should open hello default IIS web page.</span></span> <span data-ttu-id="6d473-178">É algo semelhante a isto:</span><span class="sxs-lookup"><span data-stu-id="6d473-178">It looks something like this:</span></span>
   
    ![Captura de tela mostrando qual página IIS padrão Olá aparência em um navegador](./media/hero-role/iis-default.png)

## <a name="next-steps"></a><span data-ttu-id="6d473-180">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6d473-180">Next steps</span></span>
* <span data-ttu-id="6d473-181">Você também pode fazer experiências com [anexar um disco de dados](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="6d473-181">You can also experiment with [attaching a data disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooyour virtual machine.</span></span> <span data-ttu-id="6d473-182">Os discos de dados oferecem mais armazenamento para sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="6d473-182">Data disks provide more storage for your virtual machine.</span></span>

