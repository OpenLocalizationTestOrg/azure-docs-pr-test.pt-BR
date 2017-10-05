---
title: "Azure Active Directory Domain Service: ingressar uma VM RHEL em um domínio gerenciado | Microsoft Docs"
description: "Ingresse uma máquina virtual do Red Hat Enterprise Linux nos Serviços de Domínio do Azure AD"
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
ms.openlocfilehash: 69f1850bfed90392e9a4695e2443ffaa6bfc746d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="join-a-red-hat-enterprise-linux-7-virtual-machine-to-a-managed-domain"></a><span data-ttu-id="2f93c-103">Ingressar uma máquina virtual do Red Hat Enterprise Linux 7 em um domínio gerenciado</span><span class="sxs-lookup"><span data-stu-id="2f93c-103">Join a Red Hat Enterprise Linux 7 virtual machine to a managed domain</span></span>
<span data-ttu-id="2f93c-104">Este artigo mostra como ingressar em uma máquina virtual do RHEL (Red Hat Enterprise Linux) 7 em um domínio gerenciado dos Serviços de Domínio do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f93c-104">This article shows you how to join a Red Hat Enterprise Linux (RHEL) 7 virtual machine to an Azure AD Domain Services managed domain.</span></span>

## <a name="provision-a-red-hat-enterprise-linux-virtual-machine"></a><span data-ttu-id="2f93c-105">Provisionar uma máquina virtual do Red Hat Enterprise Linux</span><span class="sxs-lookup"><span data-stu-id="2f93c-105">Provision a Red Hat Enterprise Linux virtual machine</span></span>
<span data-ttu-id="2f93c-106">Execute as seguintes etapas para provisionar uma máquina virtual do RHEL 7 usando o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2f93c-106">Perform the following steps to provision a RHEL 7 virtual machine using the Azure portal.</span></span>

1. <span data-ttu-id="2f93c-107">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2f93c-107">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

    ![Painel do portal do Azure](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-dashboard.png)
2. <span data-ttu-id="2f93c-109">Clique em **Novo** no painel à esquerda e digite **Red Hat** na barra de pesquisa, como mostra a captura de tela abaixo.</span><span class="sxs-lookup"><span data-stu-id="2f93c-109">Click **New** on the left pane and type **Red Hat** into the search bar as shown in the following screenshot.</span></span> <span data-ttu-id="2f93c-110">As entradas para Red Hat Enterprise Linux aparecem nos resultados de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="2f93c-110">Entries for Red Hat Enterprise Linux appear in the search results.</span></span> <span data-ttu-id="2f93c-111">Clique em **Red Hat Enterprise Linux 7.2**.</span><span class="sxs-lookup"><span data-stu-id="2f93c-111">Click **Red Hat Enterprise Linux 7.2**.</span></span>

    ![Selecione RHEL nos resultados](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-find-rhel-image.png)
3. <span data-ttu-id="2f93c-113">Os resultados da pesquisa no painel **Tudo** deve listar a imagem do Red Hat Enterprise Linux 7.2.</span><span class="sxs-lookup"><span data-stu-id="2f93c-113">The search results in the **Everything** pane should list the Red Hat Enterprise Linux 7.2 image.</span></span> <span data-ttu-id="2f93c-114">Clique em **Red Hat Enterprise Linux 7.2** para exibir mais informações sobre a imagem da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2f93c-114">Click **Red Hat Enterprise Linux 7.2** to view more information about the virtual machine image.</span></span>

    ![Selecione RHEL nos resultados](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-rhel-image.png)
4. <span data-ttu-id="2f93c-116">No painel **Red Hat Enterprise Linux 7.2** , você deve ver mais informações sobre a imagem da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2f93c-116">In the **Red Hat Enterprise Linux 7.2** pane, you should see more information about the virtual machine image.</span></span> <span data-ttu-id="2f93c-117">Na lista suspensa **Selecionar um modelo de implantação**, selecione **Clássico**.</span><span class="sxs-lookup"><span data-stu-id="2f93c-117">In the **Select a deployment model** dropdown, select **Classic**.</span></span> <span data-ttu-id="2f93c-118">Em seguida, clique no botão **Criar** .</span><span class="sxs-lookup"><span data-stu-id="2f93c-118">Then click the **Create** button.</span></span>

    ![Exibir detalhes da imagem](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-clicked.png)
5. <span data-ttu-id="2f93c-120">Na página **Noções Básicas** do assistente **Criar máquina virtual**, insira o **Nome do Host** para a nova máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2f93c-120">In the **Basics** page of the **Create virtual machine** wizard, enter the **Host Name** for the new virtual machine.</span></span> <span data-ttu-id="2f93c-121">Também especifique um nome de usuário administrador local no campo **Nome de usuário** e uma **Senha**.</span><span class="sxs-lookup"><span data-stu-id="2f93c-121">Also specify a local administrator user name in the **User name** field and a **Password**.</span></span> <span data-ttu-id="2f93c-122">Você também pode optar por usar uma chave SSH para autenticar o usuário administrador local.</span><span class="sxs-lookup"><span data-stu-id="2f93c-122">You may also choose to use an SSH key to authenticate the local administrator user.</span></span> <span data-ttu-id="2f93c-123">Selecione também um **Tipo de Preço** para a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2f93c-123">Also select a **Pricing Tier** for the virtual machine.</span></span>

    ![Criar VM — página de noções básicas](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-basic-details.png)
6. <span data-ttu-id="2f93c-125">Na página **Tamanho** do assistente **Criar máquina virtual**, escolha o tamanho da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2f93c-125">In the **Size** page of the **Create virtual machine** wizard, select the size for the virtual machine.</span></span>

    ![Criar VM — selecionar tamanho](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-vm-size.png)

7. <span data-ttu-id="2f93c-127">Na página **Configurações** do assistente **Criar máquina virtual**, escolha a conta de armazenamento para a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2f93c-127">In the **Settings** page of the **Create virtual machine** wizard, select the storage account for the virtual machine.</span></span> <span data-ttu-id="2f93c-128">Clique em **Rede Virtual** para escolher a rede virtual na qual a VM do Linux deve ser implantada.</span><span class="sxs-lookup"><span data-stu-id="2f93c-128">Click **Virtual Network** to select the virtual network to which the Linux VM should be deployed.</span></span> <span data-ttu-id="2f93c-129">Na folha **Rede Virtual**, escolha a rede virtual na qual o Azure AD Domain Services está disponível.</span><span class="sxs-lookup"><span data-stu-id="2f93c-129">In the **Virtual Network** blade, select the virtual network in which Azure AD Domain Services is available.</span></span> <span data-ttu-id="2f93c-130">Neste exemplo, vamos escolher a rede virtual 'MyPreviewVNet'.</span><span class="sxs-lookup"><span data-stu-id="2f93c-130">In this example, we pick the 'MyPreviewVNet' virtual network.</span></span>

    ![Criar VM - selecionar rede virtual](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-select-vnet.png)
8. <span data-ttu-id="2f93c-132">Na página **Resumo** do assistente **Criar máquina virtual**, revise e clique no botão **OK**.</span><span class="sxs-lookup"><span data-stu-id="2f93c-132">On the **Summary** page of the **Create virtual machine** wizard, review and click the **OK** button.</span></span>

    ![Criar VM - rede virtual selecionada](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-vnet-selected.png)
9. <span data-ttu-id="2f93c-134">A implantação da nova máquina virtual com base na imagem do RHEL 7.2 deve começar.</span><span class="sxs-lookup"><span data-stu-id="2f93c-134">Deployment of the new virtual machine based on the RHEL 7.2 image should start.</span></span>

    ![Criar VM - implantação iniciada](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployment-started.png)
10. <span data-ttu-id="2f93c-136">Depois de alguns minutos, a máquina virtual deve estar implantada com êxito e pronta para uso.</span><span class="sxs-lookup"><span data-stu-id="2f93c-136">After a few minutes, the virtual machine should be deployed successfully and ready for use.</span></span>

    ![Criar VM - implantada](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployed.png)

## <a name="connect-remotely-to-the-newly-provisioned-linux-virtual-machine"></a><span data-ttu-id="2f93c-138">Conectar-se remotamente à máquina virtual do Linux recém-provisionada</span><span class="sxs-lookup"><span data-stu-id="2f93c-138">Connect remotely to the newly provisioned Linux virtual machine</span></span>
<span data-ttu-id="2f93c-139">A máquina virtual do RHEL 7.2 foi provisionada no Azure.</span><span class="sxs-lookup"><span data-stu-id="2f93c-139">The RHEL 7.2 virtual machine has been provisioned in Azure.</span></span> <span data-ttu-id="2f93c-140">A próxima tarefa é se conectar remotamente à máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2f93c-140">The next task is to connect remotely to the virtual machine.</span></span>

<span data-ttu-id="2f93c-141">**Conectar-se à máquina virtual do RHEL 7.2** siga as instruções no artigo [Como fazer logon em uma máquina virtual que executa o Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2f93c-141">**Connect to the RHEL 7.2 virtual machine** Follow the instructions in the article [How to log on to a virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="2f93c-142">O restante das etapas assume que você usa o cliente SSH PuTTY para se conectar à máquina virtual RHEL.</span><span class="sxs-lookup"><span data-stu-id="2f93c-142">The rest of the steps assume you use the PuTTY SSH client to connect to the RHEL virtual machine.</span></span> <span data-ttu-id="2f93c-143">Para obter mais informações, consulte a [PuTTY Download page](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)(Página de download do PuTTY).</span><span class="sxs-lookup"><span data-stu-id="2f93c-143">For more information, see the [PuTTY Download page](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

1. <span data-ttu-id="2f93c-144">Abra o programa PuTTY.</span><span class="sxs-lookup"><span data-stu-id="2f93c-144">Open the PuTTY program.</span></span>
2. <span data-ttu-id="2f93c-145">Insira o **Nome do Host** da máquina virtual do RHEL recém-criada.</span><span class="sxs-lookup"><span data-stu-id="2f93c-145">Enter the **Host Name** for the newly created RHEL virtual machine.</span></span> <span data-ttu-id="2f93c-146">Neste exemplo, nossa máquina virtual tem o nome de host 'contoso-rhel.cloudapp.net'.</span><span class="sxs-lookup"><span data-stu-id="2f93c-146">In this example, our virtual machine has the host name 'contoso-rhel.cloudapp.net'.</span></span> <span data-ttu-id="2f93c-147">Se você não tiver certeza do nome do host da VM, consulte o painel da VM no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2f93c-147">If you are not sure of the host name of your VM, refer to the VM dashboard on the Azure portal.</span></span>

    ![Conectar no PuTTY](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-connect.png)
3. <span data-ttu-id="2f93c-149">Faça logon na máquina virtual usando as credenciais de administrador local que você especificou quando a máquina virtual foi criada.</span><span class="sxs-lookup"><span data-stu-id="2f93c-149">Log on to the virtual machine using the local administrator credentials you specified when the virtual machine was created.</span></span> <span data-ttu-id="2f93c-150">Neste exemplo, estávamos usando a conta de administrador local “mahesh”.</span><span class="sxs-lookup"><span data-stu-id="2f93c-150">In this example, we used the local administrator account "mahesh".</span></span>

    ![Logon no PuTTY](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-login.png)

## <a name="install-required-packages-on-the-linux-virtual-machine"></a><span data-ttu-id="2f93c-152">Instalar os pacotes necessários na máquina virtual do Linux</span><span class="sxs-lookup"><span data-stu-id="2f93c-152">Install required packages on the Linux virtual machine</span></span>
<span data-ttu-id="2f93c-153">Depois de se conectar à máquina virtual, a próxima tarefa é instalar os pacotes necessários para o ingresso no domínio na máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2f93c-153">After connecting to the virtual machine, the next task is to install packages required for domain join on the virtual machine.</span></span> <span data-ttu-id="2f93c-154">Execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="2f93c-154">Perform the following steps:</span></span>

1. <span data-ttu-id="2f93c-155">**Instalar o realmd:** o pacote realmd é usado para o ingresso no domínio.</span><span class="sxs-lookup"><span data-stu-id="2f93c-155">**Install realmd:** The realmd package is used for domain join.</span></span> <span data-ttu-id="2f93c-156">No terminal do PuTTY, digite o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="2f93c-156">In your PuTTY terminal, type the following command:</span></span>

    <span data-ttu-id="2f93c-157">sudo yum install realmd</span><span class="sxs-lookup"><span data-stu-id="2f93c-157">sudo yum install realmd</span></span>

    ![Instalar o realmd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-realmd.png)

    <span data-ttu-id="2f93c-159">Depois de alguns minutos, o pacote realmd deve ser instalado na máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2f93c-159">After a few minutes, the realmd package should get installed on the virtual machine.</span></span>

    ![realmd instalado](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-installed.png)
2. <span data-ttu-id="2f93c-161">**Instalar o sssd:** o pacote realmd depende do sssd para executar as operações de ingresso no domínio.</span><span class="sxs-lookup"><span data-stu-id="2f93c-161">**Install sssd:** The realmd package depends on sssd to perform domain join operations.</span></span> <span data-ttu-id="2f93c-162">No terminal do PuTTY, digite o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="2f93c-162">In your PuTTY terminal, type the following command:</span></span>

    <span data-ttu-id="2f93c-163">sudo yum install sssd</span><span class="sxs-lookup"><span data-stu-id="2f93c-163">sudo yum install sssd</span></span>

    ![Instalar o sssd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-sssd.png)

    <span data-ttu-id="2f93c-165">Depois de alguns minutos, o pacote sssd deve ser instalado na máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2f93c-165">After a few minutes, the sssd package should get installed on the virtual machine.</span></span>

    ![realmd instalado](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-sssd-installed.png)
3. <span data-ttu-id="2f93c-167">**Instalar o kerberos:** no terminal do PuTTY, digite o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="2f93c-167">**Install kerberos:** In your PuTTY terminal, type the following command:</span></span>

    <span data-ttu-id="2f93c-168">sudo yum install krb5-workstation krb5-libs</span><span class="sxs-lookup"><span data-stu-id="2f93c-168">sudo yum install krb5-workstation krb5-libs</span></span>

    ![Instalar o kerberos](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-kerberos.png)

    <span data-ttu-id="2f93c-170">Depois de alguns minutos, o pacote realmd deve ser instalado na máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2f93c-170">After a few minutes, the realmd package should get installed on the virtual machine.</span></span>

    ![Kerberos instalado](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kerberos-installed.png)

## <a name="join-the-linux-virtual-machine-to-the-managed-domain"></a><span data-ttu-id="2f93c-172">Ingressar a máquina virtual do Linux no domínio gerenciado</span><span class="sxs-lookup"><span data-stu-id="2f93c-172">Join the Linux virtual machine to the managed domain</span></span>
<span data-ttu-id="2f93c-173">Agora que os pacotes necessários são instalados na máquina virtual do Linux, a próxima tarefa é ingressar a máquina virtual no domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="2f93c-173">Now that the required packages are installed on the Linux virtual machine, the next task is to join the virtual machine to the managed domain.</span></span>

1. <span data-ttu-id="2f93c-174">Descubra o domínio gerenciado dos Serviços de Domínio do AAD.</span><span class="sxs-lookup"><span data-stu-id="2f93c-174">Discover the AAD Domain Services managed domain.</span></span> <span data-ttu-id="2f93c-175">No terminal do PuTTY, digite o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="2f93c-175">In your PuTTY terminal, type the following command:</span></span>

    <span data-ttu-id="2f93c-176">sudo realm discover CONTOSO100.COM</span><span class="sxs-lookup"><span data-stu-id="2f93c-176">sudo realm discover CONTOSO100.COM</span></span>

    ![realm discover](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-discover.png)

    <span data-ttu-id="2f93c-178">Se **realm discover** não conseguir localizar seu domínio gerenciado, certifique-se de que o domínio esteja acessível da máquina virtual (tente executar o ping).</span><span class="sxs-lookup"><span data-stu-id="2f93c-178">If **realm discover** is unable to find your managed domain, ensure that the domain is reachable from the virtual machine (try ping).</span></span> <span data-ttu-id="2f93c-179">Além disso, verifique se a máquina virtual, de fato, foi implantada na mesma rede virtual na qual o domínio gerenciado está disponível.</span><span class="sxs-lookup"><span data-stu-id="2f93c-179">Also ensure that the virtual machine has indeed been deployed to the same virtual network in which the managed domain is available.</span></span>
2. <span data-ttu-id="2f93c-180">Inicialize o kerberos.</span><span class="sxs-lookup"><span data-stu-id="2f93c-180">Initialize kerberos.</span></span> <span data-ttu-id="2f93c-181">No terminal do PuTTY, digite o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="2f93c-181">In your PuTTY terminal, type the following command.</span></span> <span data-ttu-id="2f93c-182">Certifique-se de especificar um usuário que pertence ao grupo 'Administradores do DC do AAD’.</span><span class="sxs-lookup"><span data-stu-id="2f93c-182">Ensure that you specify a user who belongs to the 'AAD DC Administrators' group.</span></span> <span data-ttu-id="2f93c-183">Apenas esses usuários podem ingressar computadores ao domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="2f93c-183">Only these users can join computers to the managed domain.</span></span>

    <span data-ttu-id="2f93c-184">kinit bob@CONTOSO100.COM</span><span class="sxs-lookup"><span data-stu-id="2f93c-184">kinit bob@CONTOSO100.COM</span></span>

    ![kinit ](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kinit.png)

    <span data-ttu-id="2f93c-186">Especifique o nome do domínio em letras maiúsculas, caso contrário, o kinit falhará.</span><span class="sxs-lookup"><span data-stu-id="2f93c-186">Ensure that you specify the domain name in capital letters, else kinit fails.</span></span>
3. <span data-ttu-id="2f93c-187">Ingresse a máquina no domínio.</span><span class="sxs-lookup"><span data-stu-id="2f93c-187">Join the machine to the domain.</span></span> <span data-ttu-id="2f93c-188">No terminal do PuTTY, digite o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="2f93c-188">In your PuTTY terminal, type the following command.</span></span> <span data-ttu-id="2f93c-189">Especifique o mesmo usuário que você especificou na etapa anterior ('kinit').</span><span class="sxs-lookup"><span data-stu-id="2f93c-189">Specify the same user you specified in the preceding step ('kinit').</span></span>

    <span data-ttu-id="2f93c-190">sudo realm join --verbose CONTOSO100.COM -U 'bob@CONTOSO100.COM'</span><span class="sxs-lookup"><span data-stu-id="2f93c-190">sudo realm join --verbose CONTOSO100.COM -U 'bob@CONTOSO100.COM'</span></span>

    ![Ingresso no realm](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-join.png)

<span data-ttu-id="2f93c-192">Você deverá receber uma mensagem ("Computador registrado com êxito no realm") quando a máquina for ingressada com êxito no domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="2f93c-192">You should get a message ("Successfully enrolled machine in realm") when the machine is successfully joined to the managed domain.</span></span>

## <a name="verify-domain-join"></a><span data-ttu-id="2f93c-193">Verificar o ingresso no domínio</span><span class="sxs-lookup"><span data-stu-id="2f93c-193">Verify domain join</span></span>
<span data-ttu-id="2f93c-194">Você pode verificar rapidamente se a máquina ingressou com êxito no domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="2f93c-194">You can quickly verify whether the machine has been successfully joined to the managed domain.</span></span> <span data-ttu-id="2f93c-195">Conecte-se ao domínio recém-associado RHEL VM usando SSH e uma conta de usuário de domínio e, em seguida, verifique se a conta de usuário é resolvida corretamente.</span><span class="sxs-lookup"><span data-stu-id="2f93c-195">Connect to the newly domain joined RHEL VM using SSH and a domain user account and then check to see if the user account is resolved correctly.</span></span>

1. <span data-ttu-id="2f93c-196">No terminal do PuTTY, digite o seguinte comando para se conectar à máquina virtual do RHEL recém-ingressada no domínio usando SSH.</span><span class="sxs-lookup"><span data-stu-id="2f93c-196">In your PuTTY terminal, type the following command to connect to the newly domain joined RHEL virtual machine using SSH.</span></span> <span data-ttu-id="2f93c-197">Use uma conta de domínio que pertença ao domínio gerenciado (por exemplo, 'bob@CONTOSO100.COM' neste caso).</span><span class="sxs-lookup"><span data-stu-id="2f93c-197">Use a domain account that belongs to the managed domain (for example, 'bob@CONTOSO100.COM' in this case.)</span></span>

    <span data-ttu-id="2f93c-198">ssh -l bob@CONTOSO100.COM contoso-rhel.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="2f93c-198">ssh -l bob@CONTOSO100.COM contoso-rhel.cloudapp.net</span></span>
2. <span data-ttu-id="2f93c-199">No terminal do PuTTY, digite o seguinte comando para ver se o diretório base foi inicializado corretamente.</span><span class="sxs-lookup"><span data-stu-id="2f93c-199">In your PuTTY terminal, type the following command to see if the home directory was initialized correctly.</span></span>

    <span data-ttu-id="2f93c-200">pwd</span><span class="sxs-lookup"><span data-stu-id="2f93c-200">pwd</span></span>
3. <span data-ttu-id="2f93c-201">No terminal do PuTTY, digite o seguinte comando para ver se as associações de grupo estão sendo resolvidas corretamente.</span><span class="sxs-lookup"><span data-stu-id="2f93c-201">In your PuTTY terminal, type the following command to see if the group memberships are being resolved correctly.</span></span>

    <span data-ttu-id="2f93c-202">ID</span><span class="sxs-lookup"><span data-stu-id="2f93c-202">id</span></span>

<span data-ttu-id="2f93c-203">Abaixo temos uma saída de exemplo desses comandos:</span><span class="sxs-lookup"><span data-stu-id="2f93c-203">A sample output of these commands follows:</span></span>

![Verificar o ingresso no domínio](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-verify-domain-join.png)

## <a name="troubleshooting-domain-join"></a><span data-ttu-id="2f93c-205">Solucionando problemas de ingresso no domínio</span><span class="sxs-lookup"><span data-stu-id="2f93c-205">Troubleshooting domain join</span></span>
<span data-ttu-id="2f93c-206">Consulte o artigo [Troubleshooting domain join](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) (Solucionando problemas de ingresso no domínio).</span><span class="sxs-lookup"><span data-stu-id="2f93c-206">Refer to the [Troubleshooting domain join](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) article.</span></span>

## <a name="related-content"></a><span data-ttu-id="2f93c-207">Conteúdo relacionado</span><span class="sxs-lookup"><span data-stu-id="2f93c-207">Related Content</span></span>
* [<span data-ttu-id="2f93c-208">Serviços de Domínio do Azure AD - Guia de Introdução</span><span class="sxs-lookup"><span data-stu-id="2f93c-208">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="2f93c-209">Ingressar uma máquina virtual do Windows Server em um domínio gerenciado dos Serviços de Domínio do Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f93c-209">Join a Windows Server virtual machine to an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* <span data-ttu-id="2f93c-210">[Como fazer logon em uma máquina virtual executando o Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2f93c-210">[How to log on to a virtual machine running Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* [<span data-ttu-id="2f93c-211">Installing Kerberos (Instalando o Kerberos)</span><span class="sxs-lookup"><span data-stu-id="2f93c-211">Installing Kerberos</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Smart_Cards/installing-kerberos.html)
* [<span data-ttu-id="2f93c-212">Red Hat Enterprise Linux 7 - Windows Integration Guide (Red Hat Enterprise Linux 7: Guia de integração do Windows)</span><span class="sxs-lookup"><span data-stu-id="2f93c-212">Red Hat Enterprise Linux 7 - Windows Integration Guide</span></span>](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/index.html)
