---
title: "Serviços do Azure Active Directory domínio: Ingressar em um domínio gerenciado do RHEL VM tooa | Microsoft Docs"
description: "Adicione uma máquina virtual de Red Hat Enterprise Linux tooAzure AD os serviços de domínio"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 87291c47-1280-43f8-8fb2-da1bd61a4942
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 41ca2aaf2eefbf9c403d2b834d61a1aa0943d950
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-red-hat-enterprise-linux-7-virtual-machine-tooa-managed-domain"></a><span data-ttu-id="95b7e-103">Ingressar em um domínio gerenciado do Red Hat Enterprise Linux 7 máquina virtual tooa</span><span class="sxs-lookup"><span data-stu-id="95b7e-103">Join a Red Hat Enterprise Linux 7 virtual machine tooa managed domain</span></span>
<span data-ttu-id="95b7e-104">Este artigo mostra como toojoin uma tooan de máquina virtual do Red Hat Enterprise Linux (RHEL) 7 serviços de domínio do AD do Azure gerenciados domínio.</span><span class="sxs-lookup"><span data-stu-id="95b7e-104">This article shows you how toojoin a Red Hat Enterprise Linux (RHEL) 7 virtual machine tooan Azure AD Domain Services managed domain.</span></span>

## <a name="provision-a-red-hat-enterprise-linux-virtual-machine"></a><span data-ttu-id="95b7e-105">Provisionar uma máquina virtual do Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="95b7e-105">Provision a Red Hat Enterprise Linux virtual machine</span></span>
<span data-ttu-id="95b7e-106">Execute Olá seguindo as etapas tooprovision RHEL 7 VM usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="95b7e-106">Perform hello following steps tooprovision a RHEL 7 virtual machine using hello Azure portal.</span></span>

1. <span data-ttu-id="95b7e-107">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="95b7e-107">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

    ![Painel do portal do Azure](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-dashboard.png)
2. <span data-ttu-id="95b7e-109">Clique em **novo** em Olá esquerda painel e digite **Red Hat** na barra de pesquisa Olá conforme Olá captura de tela a seguir.</span><span class="sxs-lookup"><span data-stu-id="95b7e-109">Click **New** on hello left pane and type **Red Hat** into hello search bar as shown in hello following screenshot.</span></span> <span data-ttu-id="95b7e-110">Entradas para Red Hat Enterprise Linux são exibidas nos resultados da pesquisa hello.</span><span class="sxs-lookup"><span data-stu-id="95b7e-110">Entries for Red Hat Enterprise Linux appear in hello search results.</span></span> <span data-ttu-id="95b7e-111">Clique em **Red Hat Enterprise Linux 7.2**.</span><span class="sxs-lookup"><span data-stu-id="95b7e-111">Click **Red Hat Enterprise Linux 7.2**.</span></span>

    ![Selecione RHEL nos resultados](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-find-rhel-image.png)
3. <span data-ttu-id="95b7e-113">resultados da pesquisa de saudação em Olá **tudo** painel deve listar imagem Olá Red Hat Enterprise Linux 7.2.</span><span class="sxs-lookup"><span data-stu-id="95b7e-113">hello search results in hello **Everything** pane should list hello Red Hat Enterprise Linux 7.2 image.</span></span> <span data-ttu-id="95b7e-114">Clique em **Red Hat Enterprise Linux 7.2** tooview obter mais informações sobre a imagem de máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="95b7e-114">Click **Red Hat Enterprise Linux 7.2** tooview more information about hello virtual machine image.</span></span>

    ![Selecione RHEL nos resultados](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-rhel-image.png)
4. <span data-ttu-id="95b7e-116">Em Olá **Red Hat Enterprise Linux 7.2** painel, você deve ver mais informações sobre a imagem de máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="95b7e-116">In hello **Red Hat Enterprise Linux 7.2** pane, you should see more information about hello virtual machine image.</span></span> <span data-ttu-id="95b7e-117">Em Olá **selecionar um modelo de implantação** lista suspensa, selecione **clássico**.</span><span class="sxs-lookup"><span data-stu-id="95b7e-117">In hello **Select a deployment model** dropdown, select **Classic**.</span></span> <span data-ttu-id="95b7e-118">Em seguida, clique em Olá **criar** botão.</span><span class="sxs-lookup"><span data-stu-id="95b7e-118">Then click hello **Create** button.</span></span>

    ![Exibir detalhes da imagem](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-clicked.png)
5. <span data-ttu-id="95b7e-120">Em hello **Noções básicas de** página de saudação **criar máquina virtual** assistente, digite Olá **nome de Host** para a máquina virtual da nova hello.</span><span class="sxs-lookup"><span data-stu-id="95b7e-120">In hello **Basics** page of hello **Create virtual machine** wizard, enter hello **Host Name** for hello new virtual machine.</span></span> <span data-ttu-id="95b7e-121">Também especifique um nome de usuário de administrador local no hello **nome de usuário** campo e um **senha**.</span><span class="sxs-lookup"><span data-stu-id="95b7e-121">Also specify a local administrator user name in hello **User name** field and a **Password**.</span></span> <span data-ttu-id="95b7e-122">Você também pode escolher toouse um usuário de administrador local do SSH tooauthenticate chave hello.</span><span class="sxs-lookup"><span data-stu-id="95b7e-122">You may also choose toouse an SSH key tooauthenticate hello local administrator user.</span></span> <span data-ttu-id="95b7e-123">Selecione também um **preço** para a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="95b7e-123">Also select a **Pricing Tier** for hello virtual machine.</span></span>

    ![Criar VM — página de noções básicas](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-basic-details.png)
6. <span data-ttu-id="95b7e-125">Em Olá **tamanho** página de saudação **criar a máquina virtual** tamanho de saudação do assistente, selecione para a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="95b7e-125">In hello **Size** page of hello **Create virtual machine** wizard, select hello size for hello virtual machine.</span></span>

    ![Criar VM — selecionar tamanho](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-vm-size.png)

7. <span data-ttu-id="95b7e-127">Em Olá **configurações** página de saudação **criar a máquina virtual** conta de armazenamento de saudação do assistente, selecione para a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="95b7e-127">In hello **Settings** page of hello **Create virtual machine** wizard, select hello storage account for hello virtual machine.</span></span> <span data-ttu-id="95b7e-128">Clique em **rede Virtual** tooselect Olá rede virtual toowhich Olá VM do Linux deve ser implantado.</span><span class="sxs-lookup"><span data-stu-id="95b7e-128">Click **Virtual Network** tooselect hello virtual network toowhich hello Linux VM should be deployed.</span></span> <span data-ttu-id="95b7e-129">Em Olá **rede Virtual** folha, a rede virtual Olá selecione, no qual os serviços de domínio do AD do Azure está disponível.</span><span class="sxs-lookup"><span data-stu-id="95b7e-129">In hello **Virtual Network** blade, select hello virtual network in which Azure AD Domain Services is available.</span></span> <span data-ttu-id="95b7e-130">Neste exemplo, podemos escolher rede virtual do 'MyPreviewVNet' hello.</span><span class="sxs-lookup"><span data-stu-id="95b7e-130">In this example, we pick hello 'MyPreviewVNet' virtual network.</span></span>

    ![Criar VM - selecionar rede virtual](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-select-vnet.png)
8. <span data-ttu-id="95b7e-132">Em Olá **resumo** página de saudação **criar a máquina virtual** saudação do assistente, examine e clique em **Okey** botão.</span><span class="sxs-lookup"><span data-stu-id="95b7e-132">On hello **Summary** page of hello **Create virtual machine** wizard, review and click hello **OK** button.</span></span>

    ![Criar VM - rede virtual selecionada](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-vnet-selected.png)
9. <span data-ttu-id="95b7e-134">Implantação de máquina virtual nova Olá baseada em imagem Olá RHEL 7.2 deve começar.</span><span class="sxs-lookup"><span data-stu-id="95b7e-134">Deployment of hello new virtual machine based on hello RHEL 7.2 image should start.</span></span>

    ![Criar VM - implantação iniciada](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployment-started.png)
10. <span data-ttu-id="95b7e-136">Após alguns minutos, a máquina virtual de saudação deve ser implantado com êxito e está pronto para uso.</span><span class="sxs-lookup"><span data-stu-id="95b7e-136">After a few minutes, hello virtual machine should be deployed successfully and ready for use.</span></span>

    ![Criar VM - implantada](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployed.png)

## <a name="connect-remotely-toohello-newly-provisioned-linux-virtual-machine"></a><span data-ttu-id="95b7e-138">Conectar-se remotamente toohello recentemente provisionado máquina de virtual do Linux</span><span class="sxs-lookup"><span data-stu-id="95b7e-138">Connect remotely toohello newly provisioned Linux virtual machine</span></span>
<span data-ttu-id="95b7e-139">máquina virtual de saudação RHEL 7.2 tiver sido configurada no Azure.</span><span class="sxs-lookup"><span data-stu-id="95b7e-139">hello RHEL 7.2 virtual machine has been provisioned in Azure.</span></span> <span data-ttu-id="95b7e-140">Olá próxima tarefa é tooconnect remotamente toohello VM.</span><span class="sxs-lookup"><span data-stu-id="95b7e-140">hello next task is tooconnect remotely toohello virtual machine.</span></span>

<span data-ttu-id="95b7e-141">**Conecte-se a máquina virtual de toohello RHEL 7.2** siga as instruções de saudação artigo Olá [como toolog na máquina virtual de tooa executando o Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="95b7e-141">**Connect toohello RHEL 7.2 virtual machine** Follow hello instructions in hello article [How toolog on tooa virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="95b7e-142">rest Olá das etapas de saudação suponha usar Olá PuTTY SSH cliente tooconnect toohello RHEL máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="95b7e-142">hello rest of hello steps assume you use hello PuTTY SSH client tooconnect toohello RHEL virtual machine.</span></span> <span data-ttu-id="95b7e-143">Para obter mais informações, consulte Olá [página de Download do PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="95b7e-143">For more information, see hello [PuTTY Download page](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

1. <span data-ttu-id="95b7e-144">Olá abra PuTTY programa.</span><span class="sxs-lookup"><span data-stu-id="95b7e-144">Open hello PuTTY program.</span></span>
2. <span data-ttu-id="95b7e-145">Digite hello **nome de Host** para Olá recém-criado RHEL VM.</span><span class="sxs-lookup"><span data-stu-id="95b7e-145">Enter hello **Host Name** for hello newly created RHEL virtual machine.</span></span> <span data-ttu-id="95b7e-146">Neste exemplo, a nossa máquina virtual tem o nome de host de saudação 'contoso-rhel.cloudapp .net'.</span><span class="sxs-lookup"><span data-stu-id="95b7e-146">In this example, our virtual machine has hello host name 'contoso-rhel.cloudapp.net'.</span></span> <span data-ttu-id="95b7e-147">Se você não tiver certeza do nome de host de saudação da VM, consulte toohello painel da máquina virtual em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="95b7e-147">If you are not sure of hello host name of your VM, refer toohello VM dashboard on hello Azure portal.</span></span>

    ![Conectar no PuTTY](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-connect.png)
3. <span data-ttu-id="95b7e-149">Faça logon na máquina virtual de toohello usando credenciais de administrador local Olá especificado quando a máquina virtual de saudação foi criada.</span><span class="sxs-lookup"><span data-stu-id="95b7e-149">Log on toohello virtual machine using hello local administrator credentials you specified when hello virtual machine was created.</span></span> <span data-ttu-id="95b7e-150">Neste exemplo, usamos a conta de administrador local hello "mahesh".</span><span class="sxs-lookup"><span data-stu-id="95b7e-150">In this example, we used hello local administrator account "mahesh".</span></span>

    ![Logon no PuTTY](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-login.png)

## <a name="install-required-packages-on-hello-linux-virtual-machine"></a><span data-ttu-id="95b7e-152">Instalar pacotes necessários na máquina de virtual do Linux Olá</span><span class="sxs-lookup"><span data-stu-id="95b7e-152">Install required packages on hello Linux virtual machine</span></span>
<span data-ttu-id="95b7e-153">Depois de conectar máquina de virtual toohello, Olá próxima tarefa é tooinstall pacotes necessários para o ingresso no domínio na máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="95b7e-153">After connecting toohello virtual machine, hello next task is tooinstall packages required for domain join on hello virtual machine.</span></span> <span data-ttu-id="95b7e-154">Execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="95b7e-154">Perform hello following steps:</span></span>

1. <span data-ttu-id="95b7e-155">**Instalar realmd:** pacote de realmd Olá é usado para o ingresso no domínio.</span><span class="sxs-lookup"><span data-stu-id="95b7e-155">**Install realmd:** hello realmd package is used for domain join.</span></span> <span data-ttu-id="95b7e-156">Em seu terminal PuTTY, digite Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="95b7e-156">In your PuTTY terminal, type hello following command:</span></span>

    <span data-ttu-id="95b7e-157">sudo yum install realmd</span><span class="sxs-lookup"><span data-stu-id="95b7e-157">sudo yum install realmd</span></span>

    ![Instalar o realmd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-realmd.png)

    <span data-ttu-id="95b7e-159">Depois de alguns minutos, o pacote de realmd de saudação deve obter instalado na máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="95b7e-159">After a few minutes, hello realmd package should get installed on hello virtual machine.</span></span>

    ![realmd instalado](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-installed.png)
2. <span data-ttu-id="95b7e-161">**Instalar sssd:** pacote de realmd Olá depende de operações de junção de domínio sssd tooperform.</span><span class="sxs-lookup"><span data-stu-id="95b7e-161">**Install sssd:** hello realmd package depends on sssd tooperform domain join operations.</span></span> <span data-ttu-id="95b7e-162">Em seu terminal PuTTY, digite Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="95b7e-162">In your PuTTY terminal, type hello following command:</span></span>

    <span data-ttu-id="95b7e-163">sudo yum install sssd</span><span class="sxs-lookup"><span data-stu-id="95b7e-163">sudo yum install sssd</span></span>

    ![Instalar o sssd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-sssd.png)

    <span data-ttu-id="95b7e-165">Depois de alguns minutos, o pacote de sssd de saudação deve obter instalado na máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="95b7e-165">After a few minutes, hello sssd package should get installed on hello virtual machine.</span></span>

    ![realmd instalado](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-sssd-installed.png)
3. <span data-ttu-id="95b7e-167">**Instalar o kerberos:** em seu terminal PuTTY, digite hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="95b7e-167">**Install kerberos:** In your PuTTY terminal, type hello following command:</span></span>

    <span data-ttu-id="95b7e-168">sudo yum install krb5-workstation krb5-libs</span><span class="sxs-lookup"><span data-stu-id="95b7e-168">sudo yum install krb5-workstation krb5-libs</span></span>

    ![Instalar o kerberos](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-kerberos.png)

    <span data-ttu-id="95b7e-170">Depois de alguns minutos, o pacote de realmd de saudação deve obter instalado na máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="95b7e-170">After a few minutes, hello realmd package should get installed on hello virtual machine.</span></span>

    ![Kerberos instalado](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kerberos-installed.png)

## <a name="join-hello-linux-virtual-machine-toohello-managed-domain"></a><span data-ttu-id="95b7e-172">Ingressar em domínio gerenciado de toohello Olá de máquina virtual Linux</span><span class="sxs-lookup"><span data-stu-id="95b7e-172">Join hello Linux virtual machine toohello managed domain</span></span>
<span data-ttu-id="95b7e-173">Agora que pacotes Olá necessários estão instalados na máquina de virtual do Linux hello, Olá próxima tarefa é domínio gerenciado do toohello toojoin Olá máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="95b7e-173">Now that hello required packages are installed on hello Linux virtual machine, hello next task is toojoin hello virtual machine toohello managed domain.</span></span>

1. <span data-ttu-id="95b7e-174">Descobrir o domínio gerenciado do hello dos serviços de domínio do AAD.</span><span class="sxs-lookup"><span data-stu-id="95b7e-174">Discover hello AAD Domain Services managed domain.</span></span> <span data-ttu-id="95b7e-175">Em seu terminal PuTTY, digite Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="95b7e-175">In your PuTTY terminal, type hello following command:</span></span>

    <span data-ttu-id="95b7e-176">sudo realm discover CONTOSO100.COM</span><span class="sxs-lookup"><span data-stu-id="95b7e-176">sudo realm discover CONTOSO100.COM</span></span>

    ![realm discover](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-discover.png)

    <span data-ttu-id="95b7e-178">Se **realm descobrir** é toofind não é possível o domínio gerenciado, certifique-se de que esse domínio hello está acessível na máquina virtual de saudação (tente ping).</span><span class="sxs-lookup"><span data-stu-id="95b7e-178">If **realm discover** is unable toofind your managed domain, ensure that hello domain is reachable from hello virtual machine (try ping).</span></span> <span data-ttu-id="95b7e-179">Também, certifique-se de que a máquina virtual Olá foi realmente implantado toohello mesma rede virtual no qual Olá domínio gerenciado está disponível.</span><span class="sxs-lookup"><span data-stu-id="95b7e-179">Also ensure that hello virtual machine has indeed been deployed toohello same virtual network in which hello managed domain is available.</span></span>
2. <span data-ttu-id="95b7e-180">Inicialize o kerberos.</span><span class="sxs-lookup"><span data-stu-id="95b7e-180">Initialize kerberos.</span></span> <span data-ttu-id="95b7e-181">Em seu terminal PuTTY, digite Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="95b7e-181">In your PuTTY terminal, type hello following command.</span></span> <span data-ttu-id="95b7e-182">Certifique-se de que você especifique um usuário que pertence a toohello ' AAD controlador de domínio do grupo 'Administradores.</span><span class="sxs-lookup"><span data-stu-id="95b7e-182">Ensure that you specify a user who belongs toohello 'AAD DC Administrators' group.</span></span> <span data-ttu-id="95b7e-183">Apenas esses usuários podem ingressar em domínio gerenciado toohello dos computadores.</span><span class="sxs-lookup"><span data-stu-id="95b7e-183">Only these users can join computers toohello managed domain.</span></span>

    <span data-ttu-id="95b7e-184">kinit bob@CONTOSO100.COM</span><span class="sxs-lookup"><span data-stu-id="95b7e-184">kinit bob@CONTOSO100.COM</span></span>

    ![kinit ](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kinit.png)

    <span data-ttu-id="95b7e-186">Certifique-se de que você especificar o nome de domínio de saudação em letras maiusculas, kinit else falha.</span><span class="sxs-lookup"><span data-stu-id="95b7e-186">Ensure that you specify hello domain name in capital letters, else kinit fails.</span></span>
3. <span data-ttu-id="95b7e-187">Ingresse Olá máquina toohello domínio.</span><span class="sxs-lookup"><span data-stu-id="95b7e-187">Join hello machine toohello domain.</span></span> <span data-ttu-id="95b7e-188">Em seu terminal PuTTY, digite Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="95b7e-188">In your PuTTY terminal, type hello following command.</span></span> <span data-ttu-id="95b7e-189">Especifique a saudação mesmo usuário que você especificou na saudação anterior etapa ('kinit').</span><span class="sxs-lookup"><span data-stu-id="95b7e-189">Specify hello same user you specified in hello preceding step ('kinit').</span></span>

    <span data-ttu-id="95b7e-190">sudo realm join --verbose CONTOSO100.COM -U 'bob@CONTOSO100.COM'</span><span class="sxs-lookup"><span data-stu-id="95b7e-190">sudo realm join --verbose CONTOSO100.COM -U 'bob@CONTOSO100.COM'</span></span>

    ![Ingresso no realm](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-join.png)

<span data-ttu-id="95b7e-192">Você deve receber uma mensagem ("registrado com êxito máquina no realm") quando a máquina de saudação é domínio gerenciado toohello unida com êxito.</span><span class="sxs-lookup"><span data-stu-id="95b7e-192">You should get a message ("Successfully enrolled machine in realm") when hello machine is successfully joined toohello managed domain.</span></span>

## <a name="verify-domain-join"></a><span data-ttu-id="95b7e-193">Verificar o ingresso no domínio</span><span class="sxs-lookup"><span data-stu-id="95b7e-193">Verify domain join</span></span>
<span data-ttu-id="95b7e-194">Rapidamente, você pode verificar se a máquina de saudação foi domínio gerenciado toohello unida com êxito.</span><span class="sxs-lookup"><span data-stu-id="95b7e-194">You can quickly verify whether hello machine has been successfully joined toohello managed domain.</span></span> <span data-ttu-id="95b7e-195">Conecte-se toohello domínio recém-associados RHEL VM usando o SSH e uma conta de usuário de domínio e, em seguida, toosee de seleção se a conta de usuário Olá seja resolvida corretamente.</span><span class="sxs-lookup"><span data-stu-id="95b7e-195">Connect toohello newly domain joined RHEL VM using SSH and a domain user account and then check toosee if hello user account is resolved correctly.</span></span>

1. <span data-ttu-id="95b7e-196">Em seu PuTTY terminal, Olá tipo após o comando tooconnect toohello recentemente ingressado no domínio RHEL virtual máquina usando o SSH.</span><span class="sxs-lookup"><span data-stu-id="95b7e-196">In your PuTTY terminal, type hello following command tooconnect toohello newly domain joined RHEL virtual machine using SSH.</span></span> <span data-ttu-id="95b7e-197">Usar uma conta de domínio que pertence o domínio gerenciado toohello (por exemplo, 'bob@CONTOSO100.COM' nesse caso.)</span><span class="sxs-lookup"><span data-stu-id="95b7e-197">Use a domain account that belongs toohello managed domain (for example, 'bob@CONTOSO100.COM' in this case.)</span></span>

    <span data-ttu-id="95b7e-198">ssh -l bob@CONTOSO100.COM contoso-rhel.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="95b7e-198">ssh -l bob@CONTOSO100.COM contoso-rhel.cloudapp.net</span></span>
2. <span data-ttu-id="95b7e-199">Em seu terminal PuTTY, digite Olá após o comando toosee se o diretório base Olá foi inicializado corretamente.</span><span class="sxs-lookup"><span data-stu-id="95b7e-199">In your PuTTY terminal, type hello following command toosee if hello home directory was initialized correctly.</span></span>

    <span data-ttu-id="95b7e-200">pwd</span><span class="sxs-lookup"><span data-stu-id="95b7e-200">pwd</span></span>
3. <span data-ttu-id="95b7e-201">Em seu terminal PuTTY, digite Olá toosee de comando a seguir se membros do grupo Olá estão sendo resolvidos corretamente.</span><span class="sxs-lookup"><span data-stu-id="95b7e-201">In your PuTTY terminal, type hello following command toosee if hello group memberships are being resolved correctly.</span></span>

    <span data-ttu-id="95b7e-202">ID</span><span class="sxs-lookup"><span data-stu-id="95b7e-202">id</span></span>

<span data-ttu-id="95b7e-203">Abaixo temos uma saída de exemplo desses comandos:</span><span class="sxs-lookup"><span data-stu-id="95b7e-203">A sample output of these commands follows:</span></span>

![Verificar o ingresso no domínio](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-verify-domain-join.png)

## <a name="troubleshooting-domain-join"></a><span data-ttu-id="95b7e-205">Solucionando problemas de ingresso no domínio</span><span class="sxs-lookup"><span data-stu-id="95b7e-205">Troubleshooting domain join</span></span>
<span data-ttu-id="95b7e-206">Consulte toohello [junção de domínio de solução de problemas](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) artigo.</span><span class="sxs-lookup"><span data-stu-id="95b7e-206">Refer toohello [Troubleshooting domain join](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) article.</span></span>

## <a name="related-content"></a><span data-ttu-id="95b7e-207">Conteúdo relacionado</span><span class="sxs-lookup"><span data-stu-id="95b7e-207">Related Content</span></span>
* [<span data-ttu-id="95b7e-208">Serviços de Domínio do Azure AD - guia de Introdução</span><span class="sxs-lookup"><span data-stu-id="95b7e-208">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="95b7e-209">Ingressar em um domínio gerenciado do Windows Server máquina virtual tooan serviços de domínio do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="95b7e-209">Join a Windows Server virtual machine tooan Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* <span data-ttu-id="95b7e-210">[Como toolog na máquina virtual de tooa executando o Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="95b7e-210">[How toolog on tooa virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* [<span data-ttu-id="95b7e-211">Installing Kerberos (Instalando o Kerberos)</span><span class="sxs-lookup"><span data-stu-id="95b7e-211">Installing Kerberos</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Smart_Cards/installing-kerberos.html)
* [<span data-ttu-id="95b7e-212">Red Hat Enterprise Linux 7 - Windows Integration Guide (Red Hat Enterprise Linux 7: Guia de integração do Windows)</span><span class="sxs-lookup"><span data-stu-id="95b7e-212">Red Hat Enterprise Linux 7 - Windows Integration Guide</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/index.html)
