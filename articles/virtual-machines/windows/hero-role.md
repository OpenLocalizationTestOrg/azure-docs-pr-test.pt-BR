---
title: Instalar o IIS em sua primeira VM do Windows | Microsoft Docs
description: "Teste sua primeira máquina virtual do Windows instalando o IIS e abrindo a porta 80 usando o Portal do Azure."
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
ms.openlocfilehash: b11ce1eab0c26a802c31bc418cdf725cbc4fba30
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="experiment-with-installing-a-role-on-your-windows-vm"></a><span data-ttu-id="61000-103">Experimentar a instalação de uma função em sua VM do Windows</span><span class="sxs-lookup"><span data-stu-id="61000-103">Experiment with installing a role on your Windows VM</span></span>
<span data-ttu-id="61000-104">Quando você tiver sua primeira VM (máquina virtual) em funcionamento, passe para a instalação de software e serviços.</span><span class="sxs-lookup"><span data-stu-id="61000-104">Once you have your first virtual machine (VM) up and running, you can move on to installing software and services.</span></span> <span data-ttu-id="61000-105">Para este tutorial, vamos usar o Gerenciador de Servidores na VM do Windows Server para instalar o IIS.</span><span class="sxs-lookup"><span data-stu-id="61000-105">For this tutorial, we are going to use Server Manager on the Windows Server VM to install IIS.</span></span> <span data-ttu-id="61000-106">Em seguida, criaremos um NSG (Grupo de Segurança de Rede) usando o Portal do Azure para abrir a porta 80 para tráfego IIS.</span><span class="sxs-lookup"><span data-stu-id="61000-106">Then, we will create a Network Security Group (NSG) using the Azure portal to open port 80 to IIS traffic.</span></span> 

<span data-ttu-id="61000-107">Se você ainda não criou sua primeira VM, volte para [Criar sua primeira máquina virtual do Windows no portal do Azure](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) antes de continuar com este tutorial.</span><span class="sxs-lookup"><span data-stu-id="61000-107">If you haven't already created your first VM, you should go back to [Create your first Windows virtual machine in the Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before continuing with this tutorial.</span></span>

## <a name="make-sure-the-vm-is-running"></a><span data-ttu-id="61000-108">Verificar se a VM está em execução</span><span class="sxs-lookup"><span data-stu-id="61000-108">Make sure the VM is running</span></span>
1. <span data-ttu-id="61000-109">Abra o [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="61000-109">Open the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="61000-110">No menu hub, clique em **Máquinas Virtuais**.</span><span class="sxs-lookup"><span data-stu-id="61000-110">On the hub menu, click **Virtual Machines**.</span></span> <span data-ttu-id="61000-111">Selecione a máquina virtual na lista.</span><span class="sxs-lookup"><span data-stu-id="61000-111">Select the virtual machine from the list.</span></span>
3. <span data-ttu-id="61000-112">Se o status for **Parado (Desalocado)**, clique no botão **Iniciar** na folha **Essentials** da VM.</span><span class="sxs-lookup"><span data-stu-id="61000-112">If the status is **Stopped (Deallocated)**, click the **Start** button on the **Essentials** blade of the VM.</span></span> <span data-ttu-id="61000-113">Se o status indicar **Em Execução**, passe para a próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="61000-113">If the status is **Running**, you can move on to the next step.</span></span>

## <a name="connect-to-the-virtual-machine-and-sign-in"></a><span data-ttu-id="61000-114">Conectar-se à máquina virtual e entrar</span><span class="sxs-lookup"><span data-stu-id="61000-114">Connect to the virtual machine and sign in</span></span>
1. <span data-ttu-id="61000-115">No menu hub, clique em **Máquinas Virtuais**.</span><span class="sxs-lookup"><span data-stu-id="61000-115">On the hub menu, click **Virtual Machines**.</span></span> <span data-ttu-id="61000-116">Selecione a máquina virtual na lista.</span><span class="sxs-lookup"><span data-stu-id="61000-116">Select the virtual machine from the list.</span></span>
2. <span data-ttu-id="61000-117">Na folha da máquina virtual, clique em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="61000-117">On the blade for the virtual machine, click **Connect**.</span></span> <span data-ttu-id="61000-118">Isso cria e baixa um arquivo .rdp (Protocolo de Área de Trabalho Remota) que é como um atalho para se conectar ao seu computador.</span><span class="sxs-lookup"><span data-stu-id="61000-118">This creates and downloads a Remote Desktop Protocol file (.rdp file) that is like a shortcut to connect to your machine.</span></span> <span data-ttu-id="61000-119">Convém salvar o arquivo em sua área de trabalho para facilitar o acesso.</span><span class="sxs-lookup"><span data-stu-id="61000-119">You might want to save the file to your desktop for easy access.</span></span> <span data-ttu-id="61000-120">**Abra** esse arquivo para conectar sua VM.</span><span class="sxs-lookup"><span data-stu-id="61000-120">**Open** this file to connect to your VM.</span></span>
   
    ![Captura de tela do portal do Azure mostrando como conectar sua VM](./media/hero-role/connect.png)
3. <span data-ttu-id="61000-122">Você receberá um aviso de que o .rdp é proveniente de um editor desconhecido.</span><span class="sxs-lookup"><span data-stu-id="61000-122">You get a warning that the .rdp is from an unknown publisher.</span></span> <span data-ttu-id="61000-123">Isso é normal.</span><span class="sxs-lookup"><span data-stu-id="61000-123">This is normal.</span></span> <span data-ttu-id="61000-124">Na janela de Área de Trabalho Remota, clique em **Conectar** para continuar.</span><span class="sxs-lookup"><span data-stu-id="61000-124">In the Remote Desktop window, click **Connect** to continue.</span></span>
   
    ![Captura de tela de um aviso sobre um editor desconhecido](./media/hero-role/rdp-warn.png)
4. <span data-ttu-id="61000-126">Na janela de Segurança do Windows, digite o nome de usuário e a senha para a conta local que você criou durante a criação da VM.</span><span class="sxs-lookup"><span data-stu-id="61000-126">In the Windows Security window, type the username and password for the local account that you created when you created the VM.</span></span> <span data-ttu-id="61000-127">O nome de usuário é inserido como *vmname*&#92;*nome de usuário*, depois, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="61000-127">The username is entered as *vmname*&#92;*username*, then click **OK**.</span></span>
   
    ![Captura de tela da inserção do nome da VM, do nome de usuário e da senha](./media/hero-role/credentials.png)
5. <span data-ttu-id="61000-129">Você receberá um aviso de que o certificado não pode ser verificado.</span><span class="sxs-lookup"><span data-stu-id="61000-129">You get a warning that the certificate cannot be verified.</span></span> <span data-ttu-id="61000-130">Isso é normal.</span><span class="sxs-lookup"><span data-stu-id="61000-130">This is normal.</span></span> <span data-ttu-id="61000-131">Clique em **Sim** para verificar a identidade da máquina virtual e concluir o logon.</span><span class="sxs-lookup"><span data-stu-id="61000-131">Click **Yes** to verify the identity of the virtual machine and finish logging on.</span></span>
   
   ![Captura de tela mostrando uma mensagem sobre como verificar a identidade da VM](./media/hero-role/cert-warning.png)

<span data-ttu-id="61000-133">Se você tiver problemas ao tentar conectar, consulte [Solucionar problemas de conexões da Área de Trabalho Remota com uma Máquina Virtual do Azure baseada no Windows](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="61000-133">If you run in to trouble when you try to connect, see [Troubleshoot Remote Desktop connections to a Windows-based Azure Virtual Machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="install-iis-on-your-vm"></a><span data-ttu-id="61000-134">Instalar o IIS em sua VM</span><span class="sxs-lookup"><span data-stu-id="61000-134">Install IIS on your VM</span></span>
<span data-ttu-id="61000-135">Agora que você está conectado à VM, iremos instalar uma função de servidor para que possa experimentar mais.</span><span class="sxs-lookup"><span data-stu-id="61000-135">Now that you are logged in to the VM, we will install a server role so that you can experiment more.</span></span>

1. <span data-ttu-id="61000-136">Abra o **Gerenciador de Servidores** se ainda não estiver aberto.</span><span class="sxs-lookup"><span data-stu-id="61000-136">Open **Server Manager** if it isn't already open.</span></span> <span data-ttu-id="61000-137">Clique no menu **Iniciar** e em **Gerenciador de Servidores**.</span><span class="sxs-lookup"><span data-stu-id="61000-137">Click the **Start** menu, and then click **Server Manager**.</span></span>
2. <span data-ttu-id="61000-138">No **Gerenciador de Servidores**, selecione **Servidor Local** no painel à esquerda.</span><span class="sxs-lookup"><span data-stu-id="61000-138">In **Server Manager**, select **Local Server** from the left pane.</span></span> 
3. <span data-ttu-id="61000-139">No menu, selecione **Gerenciar** > **Adicionar Funções e Recursos**.</span><span class="sxs-lookup"><span data-stu-id="61000-139">In the menu, select **Manage** > **Add Roles and Features**.</span></span>
4. <span data-ttu-id="61000-140">No Assistente para Adicionar Funções e Recursos, na página **Tipo de Instalação**, escolha **Instalação baseada em função ou recurso**, em seguida, clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="61000-140">In the Add Roles and Features Wizard, on the **Installation Type** page, choose **Role-based or feature-based installation**, and then click **Next**.</span></span>
   
    ![Captura de tela mostrando a guia Assistente para Adicionar Funções e Recursos para o Tipo de Instalação](./media/hero-role/role-wizard.png)
5. <span data-ttu-id="61000-142">Selecione a VM no pool de servidores e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="61000-142">Select the VM from the server pool and click **Next**.</span></span>
6. <span data-ttu-id="61000-143">Na página **Funções do Servidor**, selecione **Servidor Web (IIS)**.</span><span class="sxs-lookup"><span data-stu-id="61000-143">On the **Server Roles** page, select **Web Server (IIS)**.</span></span>
   
    ![Captura de tela mostrando a guia Assistente para Adicionar Funções e Recursos para as Funções do Servidor](./media/hero-role/add-iis.png)
7. <span data-ttu-id="61000-145">No menu pop-up para adicionar recursos necessários para o IIS, verifique se a opção **Incluir ferramentas de gerenciamento** está selecionada, em seguida, clique em **Adicionar Recursos**.</span><span class="sxs-lookup"><span data-stu-id="61000-145">In the pop-up about adding features needed for IIS, make sure that **Include management tools** is selected and then click **Add Features**.</span></span> <span data-ttu-id="61000-146">Quando o pop-up fechar, clique em **Próximo** no assistente.</span><span class="sxs-lookup"><span data-stu-id="61000-146">When the pop-up closes, click **Next** in the wizard.</span></span>
   
    ![Captura de tela mostrando o menu pop-up para confirmar a adição da função do IIS](./media/hero-role/confirm-add-feature.png)
8. <span data-ttu-id="61000-148">Na página de recursos, clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="61000-148">On the features page, click **Next**.</span></span>
9. <span data-ttu-id="61000-149">Na página **Função do Servidor Web (IIS)**, clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="61000-149">On the **Web Server Role (IIS)** page, click **Next**.</span></span> 
10. <span data-ttu-id="61000-150">Na página **Serviços da Função**,clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="61000-150">On the **Role Services** page, click **Next**.</span></span> 
11. <span data-ttu-id="61000-151">Na página **Confirmação**, clique em **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="61000-151">On the **Confirmation** page, click **Install**.</span></span> 
12. <span data-ttu-id="61000-152">Quando a instalação for concluída, clique em **Fechar** no assistente.</span><span class="sxs-lookup"><span data-stu-id="61000-152">When the installation is complete, click **Close** on the wizard.</span></span>

## <a name="open-port-80"></a><span data-ttu-id="61000-153">Abrir a porta 80</span><span class="sxs-lookup"><span data-stu-id="61000-153">Open port 80</span></span>
<span data-ttu-id="61000-154">Para sua VM aceitar o tráfego de entrada na porta 80, você precisa adicionar uma regra de entrada ao grupo de segurança da rede.</span><span class="sxs-lookup"><span data-stu-id="61000-154">In order for your VM to accept inbound traffic over port 80, you need to add an inbound rule to the network security group.</span></span> 

1. <span data-ttu-id="61000-155">Abra o [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="61000-155">Open the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="61000-156">Em **Máquinas virtuais** , selecione a VM criada.</span><span class="sxs-lookup"><span data-stu-id="61000-156">In **Virtual machines** select the VM that you created.</span></span>
3. <span data-ttu-id="61000-157">Nas configurações das máquinas virtuais, selecione **Interfaces de rede** e, em seguida, selecione a interface de rede existente.</span><span class="sxs-lookup"><span data-stu-id="61000-157">In the virtual machines settings, select **Network interfaces** and then select the existing network interface.</span></span>
   
    ![Captura de tela mostrando a configuração da máquina virtual para as interfaces de rede](./media/hero-role/network-interface.png)
4. <span data-ttu-id="61000-159">Em **Essentials** para a interface de rede, clique no **Grupo de Segurança da Rede**.</span><span class="sxs-lookup"><span data-stu-id="61000-159">In **Essentials** for the network interface, click the **Network security group**.</span></span>
   
    ![Captura de tela mostrando a seção Essentials para a interface de rede](./media/hero-role/select-nsg.png)
5. <span data-ttu-id="61000-161">Na folha **Essentials** do NSG, você deve ter uma regra de entrada padrão existente para **default-allow-rdp**, que permite fazer logon na VM.</span><span class="sxs-lookup"><span data-stu-id="61000-161">In the **Essentials** blade for the NSG, you should have one existing default inbound rule for **default-allow-rdp** which allows you to log in to the VM.</span></span> <span data-ttu-id="61000-162">Você adicionará outra regra de entrada para permitir o tráfego do IIS.</span><span class="sxs-lookup"><span data-stu-id="61000-162">You will add another inbound rule to allow IIS traffic.</span></span> <span data-ttu-id="61000-163">Clique em **Regra de segurança de entrada**.</span><span class="sxs-lookup"><span data-stu-id="61000-163">Click **Inbound security rule**.</span></span>
   
    ![Captura de tela mostrando a seção Essentials para o NSG](./media/hero-role/inbound.png)
6. <span data-ttu-id="61000-165">Nas **Regras de segurança de entrada**, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="61000-165">In **Inbound security rules**, click **Add**.</span></span>
   
    ![Captura de tela mostrando o botão para adicionar uma regra de segurança](./media/hero-role/add-rule.png)
7. <span data-ttu-id="61000-167">Nas **Regras de segurança de entrada**, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="61000-167">In **Inbound security rules**, click **Add**.</span></span> <span data-ttu-id="61000-168">Digite **80** no intervalo de portas e verifique se **Permitir** está selecionado.</span><span class="sxs-lookup"><span data-stu-id="61000-168">Type **80** in the port range and make sure **Allow** is selected.</span></span> <span data-ttu-id="61000-169">Quando terminar, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="61000-169">When you are done, click **OK**.</span></span>
   
    ![Captura de tela mostrando o botão para adicionar uma regra de segurança](./media/hero-role/port-80.png)

<span data-ttu-id="61000-171">Para obter mais informações sobre os NSGs, regras de entrada e saída, consulte [Permitir o acesso externo à sua VM usando o portal do Azure](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="61000-171">For more information about NSGs, inbound and outbound rules, see [Allow external access to your VM using the Azure portal](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

## <a name="connect-to-the-default-iis-website"></a><span data-ttu-id="61000-172">Conectar ao site do IIS padrão</span><span class="sxs-lookup"><span data-stu-id="61000-172">Connect to the default IIS website</span></span>
1. <span data-ttu-id="61000-173">No portal do Azure, clique em **Máquinas virtuais** , em seguida, selecione sua VM.</span><span class="sxs-lookup"><span data-stu-id="61000-173">In the Azure portal, click **Virtual machines** and then select your VM.</span></span>
2. <span data-ttu-id="61000-174">Na folha **Essentials**, copie seu **Endereço IP público**.</span><span class="sxs-lookup"><span data-stu-id="61000-174">In the **Essentials** blade, copy your **Public IP address**.</span></span>
   
    ![Captura de tela mostrando onde encontrar o endereço IP público da VM](./media/hero-role/ipaddress.png)
3. <span data-ttu-id="61000-176">Abra um navegador e na barra de endereços, digite seu endereço IP público assim: http://<publicIPaddress> e clique em **Enter** para ir para esse endereço.</span><span class="sxs-lookup"><span data-stu-id="61000-176">Open a browser and in the address bar, type in your public IP address like this: http://<publicIPaddress> and click **Enter** to go to that address.</span></span>
4. <span data-ttu-id="61000-177">Seu navegador deve abrir a página Web padrão do IIS.</span><span class="sxs-lookup"><span data-stu-id="61000-177">Your browser should open the default IIS web page.</span></span> <span data-ttu-id="61000-178">É algo semelhante a isto:</span><span class="sxs-lookup"><span data-stu-id="61000-178">It looks something like this:</span></span>
   
    ![Captura de tela mostrando a aparência da página padrão do IIS em um navegador](./media/hero-role/iis-default.png)

## <a name="next-steps"></a><span data-ttu-id="61000-180">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="61000-180">Next steps</span></span>
* <span data-ttu-id="61000-181">Você também pode experimentar [anexar um disco de dados](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) à sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="61000-181">You can also experiment with [attaching a data disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to your virtual machine.</span></span> <span data-ttu-id="61000-182">Os discos de dados oferecem mais armazenamento para sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="61000-182">Data disks provide more storage for your virtual machine.</span></span>

