---
title: "Conectar-se a uma Máquina Virtual do SQL Server (Resource Manager) | Microsoft Docs"
description: "Saiba como se conectar ao SQL Server em execução em uma Máquina Virtual no Azure. Este tópico usa o modelo de implantação clássica. Os cenários diferem dependendo da configuração da rede e do local do cliente."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-resource-manager
ms.assetid: aa5bf144-37a3-4781-892d-e0e300913d03
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/14/2017
ms.author: jroth
ms.openlocfilehash: 67ba43f9456bbeffbf602067586143c4c68af672
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="connect-to-a-sql-server-virtual-machine-on-azure-resource-manager"></a><span data-ttu-id="ccf3a-105">Conectar-se a uma Máquina Virtual do SQL Server no Azure (Gerenciador de Recursos)</span><span class="sxs-lookup"><span data-stu-id="ccf3a-105">Connect to a SQL Server Virtual Machine on Azure (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ccf3a-106">Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="ccf3a-106">Resource Manager</span></span>](virtual-machines-windows-sql-connect.md)
> * [<span data-ttu-id="ccf3a-107">Clássico</span><span class="sxs-lookup"><span data-stu-id="ccf3a-107">Classic</span></span>](../classic/sql-connect.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="ccf3a-108">Visão geral</span><span class="sxs-lookup"><span data-stu-id="ccf3a-108">Overview</span></span>

<span data-ttu-id="ccf3a-109">Este tópico descreve como se conectar à instância do SQL Server em execução em uma máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="ccf3a-109">This topic describes how to connect to your SQL Server instance running on an Azure virtual machine.</span></span> <span data-ttu-id="ccf3a-110">Ele aborda alguns [cenários gerais de conectividade](#connection-scenarios) e descreve [etapas detalhadas para configurar a conectividade com o SQL Server em uma VM do Azure](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="ccf3a-110">It covers some [general connectivity scenarios](#connection-scenarios) and then provides [detailed steps for configuring SQL Server connectivity in an Azure VM](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="ccf3a-111">Para ver uma apresentação completa sobre provisionamento e conectividade, veja [Provisionando uma Máquina Virtual do SQL Server no Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="ccf3a-111">If you would rather have a full walk-through of both provisioning and connectivity, see [Provisioning a SQL Server Virtual Machine on Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

## <a name="connection-scenarios"></a><span data-ttu-id="ccf3a-112">Cenários de conexão</span><span class="sxs-lookup"><span data-stu-id="ccf3a-112">Connection scenarios</span></span>

<span data-ttu-id="ccf3a-113">A maneira como um cliente se conecta ao SQL Server em execução em uma máquina virtual varia dependendo do local do cliente e da configuração de rede.</span><span class="sxs-lookup"><span data-stu-id="ccf3a-113">The way a client connects to SQL Server running on a Virtual Machine differs depending on the location of the client and the networking configuration.</span></span>

<span data-ttu-id="ccf3a-114">Se você provisionar uma VM do SQL Server no Portal do Azure, terá a opção de especificar o tipo de **Conectividade SQL**.</span><span class="sxs-lookup"><span data-stu-id="ccf3a-114">If you provision a SQL Server VM in the Azure portal, you have the option of specifying the type of **SQL connectivity**.</span></span>

![Opção de conectividade SQL pública durante o provisionamento](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity.png)

<span data-ttu-id="ccf3a-116">As opções de conectividade incluem:</span><span class="sxs-lookup"><span data-stu-id="ccf3a-116">Your options for connectivity include:</span></span>

| <span data-ttu-id="ccf3a-117">Opção</span><span class="sxs-lookup"><span data-stu-id="ccf3a-117">Option</span></span> | <span data-ttu-id="ccf3a-118">Descrição</span><span class="sxs-lookup"><span data-stu-id="ccf3a-118">Description</span></span> |
|---|---|
| <span data-ttu-id="ccf3a-119">**Pública**</span><span class="sxs-lookup"><span data-stu-id="ccf3a-119">**Public**</span></span> | <span data-ttu-id="ccf3a-120">Conectar-se ao SQL Server pela Internet</span><span class="sxs-lookup"><span data-stu-id="ccf3a-120">Connect to SQL Server over the internet</span></span> |
| <span data-ttu-id="ccf3a-121">**Privada**</span><span class="sxs-lookup"><span data-stu-id="ccf3a-121">**Private**</span></span> | <span data-ttu-id="ccf3a-122">Conectar-se ao SQL Server na mesma rede virtual</span><span class="sxs-lookup"><span data-stu-id="ccf3a-122">Connect to SQL Server in the same virtual network</span></span> |
| <span data-ttu-id="ccf3a-123">**Local**</span><span class="sxs-lookup"><span data-stu-id="ccf3a-123">**Local**</span></span> | <span data-ttu-id="ccf3a-124">Conectar-se ao SQL Server localmente, na mesma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="ccf3a-124">Connect to SQL Server locally on the same virtual machine</span></span> | 

<span data-ttu-id="ccf3a-125">As seções a seguir explicam as opções **Pública** e **Privada** com mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="ccf3a-125">The following sections explain the **Public** and **Private** options in more detail.</span></span>

## <a name="connect-to-sql-server-over-the-internet"></a><span data-ttu-id="ccf3a-126">Conectar-se ao SQL Server pela Internet</span><span class="sxs-lookup"><span data-stu-id="ccf3a-126">Connect to SQL Server over the Internet</span></span>

<span data-ttu-id="ccf3a-127">Se você quiser se conectar ao seu mecanismo de banco de dados do SQL Server a partir da Internet, selecione **Pública** para o tipo **Conectividade SQL** no portal durante o provisionamento.</span><span class="sxs-lookup"><span data-stu-id="ccf3a-127">If you want to connect to your SQL Server database engine from the Internet, select **Public** for the **SQL connectivity** type in the portal during provisioning.</span></span> <span data-ttu-id="ccf3a-128">O portal execute automaticamente estas etapas:</span><span class="sxs-lookup"><span data-stu-id="ccf3a-128">The portal automatically does the following steps:</span></span>

* <span data-ttu-id="ccf3a-129">Habilita o protocolo TCP/IP para o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ccf3a-129">Enables the TCP/IP protocol for SQL Server.</span></span>
* <span data-ttu-id="ccf3a-130">Configura uma regra de firewall para abrir a porta TCP do SQL Server (padrão 1433).</span><span class="sxs-lookup"><span data-stu-id="ccf3a-130">Configures a firewall rule to open the SQL Server TCP port (default 1433).</span></span>
* <span data-ttu-id="ccf3a-131">Habilita a Autenticação do SQL Server, necessária para acesso público.</span><span class="sxs-lookup"><span data-stu-id="ccf3a-131">Enables SQL Server Authentication, required for public access.</span></span>
* <span data-ttu-id="ccf3a-132">Configura o grupo de segurança de rede na VM para todo o tráfego TCP na porta do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ccf3a-132">Configures the network security group on the VM to all TCP traffic on the SQL Server port.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ccf3a-133">As imagens de máquina virtual para as edições Developer e Express do SQL Server não habilitam automaticamente o protocolo TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="ccf3a-133">The virtual machine images for the SQL Server Developer and Express editions do not automatically enable the TCP/IP protocol.</span></span> <span data-ttu-id="ccf3a-134">Para as edições Developer e Express, você deve usar o SQL Server Configuration Manager para [habilitar manualmente o protocolo TCP/IP](#manualtcp) após a criação da VM.</span><span class="sxs-lookup"><span data-stu-id="ccf3a-134">For Developer and Express editions, you must use SQL Server Configuration Manager to [manually enable the TCP/IP protocol](#manualtcp) after creating the VM.</span></span>

<span data-ttu-id="ccf3a-135">Qualquer cliente com acesso à Internet pode se conectar à instância do SQL Server especificando o endereço IP público da máquina virtual ou o rótulo de DNS atribuído a esse endereço IP.</span><span class="sxs-lookup"><span data-stu-id="ccf3a-135">Any client with internet access can connect to the SQL Server instance by specifying either the public IP address of the virtual machine or any DNS label assigned to that IP address.</span></span> <span data-ttu-id="ccf3a-136">Se a porta do SQL Server for 1433, você não precisará especificá-la na cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="ccf3a-136">If the SQL Server port is 1433, you do not need to specify it in the connection string.</span></span> <span data-ttu-id="ccf3a-137">A cadeia de conexão a seguir se conecta a uma VM do SQL com um rótulo de DNS `sqlvmlabel.eastus.cloudapp.azure.com` usando a Autenticação SQL (você também pode usar o endereço IP público).</span><span class="sxs-lookup"><span data-stu-id="ccf3a-137">The following connection string connects to a SQL VM with a DNS label of `sqlvmlabel.eastus.cloudapp.azure.com` using SQL Authentication (you could also use the public IP address).</span></span>

```
Server=sqlvmlabel.eastus.cloudapp.azure.com;Integrated Security=false;User ID=<login_name>;Password=<your_password>
```

<span data-ttu-id="ccf3a-138">Embora isso habilite a conectividade para clientes pela Internet, não significa que qualquer pessoa possa se conectar ao seu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ccf3a-138">Although this enables connectivity for clients over the internet, this does not imply that anyone can connect to your SQL Server.</span></span> <span data-ttu-id="ccf3a-139">Clientes externos precisam ter o nome de usuário e a senha corretos.</span><span class="sxs-lookup"><span data-stu-id="ccf3a-139">Outside clients have to the correct username and password.</span></span> <span data-ttu-id="ccf3a-140">No entanto, para obter mais segurança, você pode evitar a porta 1433 conhecida.</span><span class="sxs-lookup"><span data-stu-id="ccf3a-140">However, for additional security, you can avoid the well-known port 1433.</span></span> <span data-ttu-id="ccf3a-141">Por exemplo, se você configurou o SQL Server para escutar na porta 1500 e estabeleceu regras do grupo de segurança de rede e de firewall apropriadas, poderá se conectar acrescentando o número da porta ao nome do servidor.</span><span class="sxs-lookup"><span data-stu-id="ccf3a-141">For example, if you configured SQL Server to listen on port 1500 and established proper firewall and network security group rules, you could connect by appending the port number to the Server name.</span></span> <span data-ttu-id="ccf3a-142">O exemplo a seguir altera o anterior adicionando um número de porta personalizada, **1500**, ao nome do servidor:</span><span class="sxs-lookup"><span data-stu-id="ccf3a-142">The following example alters the previous one by adding a custom port number, **1500**, to the server name:</span></span>

```
Server=sqlvmlabel.eastus.cloudapp.azure.com,1500;Integrated Security=false;User ID=<login_name>;Password=<your_password>"
```

> [!NOTE]
> <span data-ttu-id="ccf3a-143">Quando você consulta o SQL Server em uma VM na internet, todos os dados de saída do data center do Azure estão sujeitos a [preços de transferências de dados de saída](https://azure.microsoft.com/pricing/details/data-transfers/) normais.</span><span class="sxs-lookup"><span data-stu-id="ccf3a-143">When you query SQL Server in a VM over the internet, all outgoing data from the Azure datacenter is subject to normal [pricing on outbound data transfers](https://azure.microsoft.com/pricing/details/data-transfers/).</span></span>

## <a name="connect-to-sql-server-within-a-virtual-network"></a><span data-ttu-id="ccf3a-144">Conectar-se ao SQL Server dentro de uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="ccf3a-144">Connect to SQL Server within a virtual network</span></span>

<span data-ttu-id="ccf3a-145">Quando você escolhe **Privada** como o tipo de **Conectividade SQL** no portal, o Azure define a maioria das configurações de forma idêntica a **Pública**.</span><span class="sxs-lookup"><span data-stu-id="ccf3a-145">When you choose **Private** for the **SQL connectivity** type in the portal, Azure configures most of the settings identical to **Public**.</span></span> <span data-ttu-id="ccf3a-146">A única diferença é que não há uma regra de grupo de segurança de rede para permitir o tráfego externo na porta do SQL Server (padrão 1433).</span><span class="sxs-lookup"><span data-stu-id="ccf3a-146">The one difference is that there is no network security group rule to allow outside traffic on the SQL Server port (default 1433).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ccf3a-147">As imagens de máquina virtual para as edições Developer e Express do SQL Server não habilitam automaticamente o protocolo TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="ccf3a-147">The virtual machine images for the SQL Server Developer and Express editions do not automatically enable the TCP/IP protocol.</span></span> <span data-ttu-id="ccf3a-148">Para as edições Developer e Express, você deve usar o SQL Server Configuration Manager para [habilitar manualmente o protocolo TCP/IP](#manualtcp) após a criação da VM.</span><span class="sxs-lookup"><span data-stu-id="ccf3a-148">For Developer and Express editions, you must use SQL Server Configuration Manager to [manually enable the TCP/IP protocol](#manualtcp) after creating the VM.</span></span>

<span data-ttu-id="ccf3a-149">Normalmente, a conectividade privada é usada em conjunto com [Rede Virtual](../../../virtual-network/virtual-networks-overview.md), o que permite vários cenários.</span><span class="sxs-lookup"><span data-stu-id="ccf3a-149">Private connectivity is often used in conjunction with [Virtual Network](../../../virtual-network/virtual-networks-overview.md), which enables several scenarios.</span></span> <span data-ttu-id="ccf3a-150">Você pode conectar VMS na mesma rede virtual, ainda que essas VMs existam em grupos de recursos diferentes.</span><span class="sxs-lookup"><span data-stu-id="ccf3a-150">You can connect VMs in the same virtual network, even if those VMs exist in different resource groups.</span></span> <span data-ttu-id="ccf3a-151">E com um [VPN site a site](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), você pode criar uma arquitetura híbrida que conecta as VMs a computadores e redes locais.</span><span class="sxs-lookup"><span data-stu-id="ccf3a-151">And with a [site-to-site VPN](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), you can create a hybrid architecture that connects VMs with on-premises networks and machines.</span></span>

<span data-ttu-id="ccf3a-152">As redes virtuais também permitem que você ingresse suas VMs do Azure a um domínio.</span><span class="sxs-lookup"><span data-stu-id="ccf3a-152">Virtual networks also enable     you to join your Azure VMs to a domain.</span></span> <span data-ttu-id="ccf3a-153">Essa é a única maneira de usar a autenticação do Windows para o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ccf3a-153">This is the only way to use Windows Authentication to SQL Server.</span></span> <span data-ttu-id="ccf3a-154">Outros cenários de conexão requerem autenticação SQL com nomes de usuário e senhas.</span><span class="sxs-lookup"><span data-stu-id="ccf3a-154">The other connection scenarios require SQL Authentication with user names and passwords.</span></span>

<span data-ttu-id="ccf3a-155">Supondo que tenha configurado o DNS na sua rede virtual, você pode se conectar à instância do SQL Server especificando o nome do computador da VM do SQL Server na cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="ccf3a-155">Assuming that you have configured DNS in your virtual network, you can connect to your SQL Server instance by specifying the SQL Server VM computer name in the connection string.</span></span> <span data-ttu-id="ccf3a-156">O exemplo a seguir também pressupõe que a autenticação do Windows foi configurada e que o usuário recebeu acesso à instância do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ccf3a-156">The following example also assumes that Windows Authentication has also been configured and that the user has been granted access to the SQL Server instance.</span></span>

```
Server=mysqlvm;Integrated Security=true
```

## <span data-ttu-id="ccf3a-157"><a id="change"></a> Alterar as configurações de conectividade do SQL</span><span class="sxs-lookup"><span data-stu-id="ccf3a-157"><a id="change"></a> Change SQL connectivity settings</span></span>

<span data-ttu-id="ccf3a-158">Você pode alterar as configurações de conectividade de sua máquina de virtual do SQL Server no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ccf3a-158">You can change the connectivity settings for your SQL Server virtual machine in the Azure portal.</span></span>

1. <span data-ttu-id="ccf3a-159">No Portal do Azure, selecione **Máquinas Virtuais**.</span><span class="sxs-lookup"><span data-stu-id="ccf3a-159">In the Azure portal, select **Virtual Machines**.</span></span>

2. <span data-ttu-id="ccf3a-160">Selecione sua VM do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ccf3a-160">Select your SQL Server VM.</span></span>

3. <span data-ttu-id="ccf3a-161">Em **Configurações**, clique em **Configuração do SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="ccf3a-161">Under **Settings**, click **SQL Server configuration**.</span></span>

4. <span data-ttu-id="ccf3a-162">Altere o **Nível de conectividade do SQL** para sua configuração exigida.</span><span class="sxs-lookup"><span data-stu-id="ccf3a-162">Change the **SQL connectivity level** to your required setting.</span></span> <span data-ttu-id="ccf3a-163">Como opção, você pode usar essa área para alterar a porta do SQL Server ou as configurações da Autenticação SQL.</span><span class="sxs-lookup"><span data-stu-id="ccf3a-163">You can optionally use this area to change the SQL Server port or the SQL Authentication settings.</span></span>

   ![Alterar a conectividade do SQL](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity-change.png)

5. <span data-ttu-id="ccf3a-165">Aguarde alguns minutos até a conclusão da atualização.</span><span class="sxs-lookup"><span data-stu-id="ccf3a-165">Wait several minutes for the update to complete.</span></span>

   ![Notificação de atualização da VM do SQL](./media/virtual-machines-windows-sql-connect/sql-vm-updating-notification.png)

## <span data-ttu-id="ccf3a-167"><a id="manualtcp"></a> Habilitar TCP/IP para as edições Developer e Express</span><span class="sxs-lookup"><span data-stu-id="ccf3a-167"><a id="manualtcp"></a> Enable TCP/IP for Developer and Express editions</span></span>

<span data-ttu-id="ccf3a-168">Ao alterar as configurações de conectividade do SQL Server, o Azure não habilita automaticamente o protocolo TCP/IP para as edições Developer e Express do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ccf3a-168">When changing SQL Server connectivity settings, Azure does not automatically enable the TCP/IP protocol for SQL Server Developer and Express editions.</span></span> <span data-ttu-id="ccf3a-169">As etapas abaixo explicam como habilitar manualmente o TCP/IP para que você possa conectar remotamente pelo endereço IP.</span><span class="sxs-lookup"><span data-stu-id="ccf3a-169">The steps below explain how to manually enable TCP/IP so that you can connect remotely by IP address.</span></span>

<span data-ttu-id="ccf3a-170">Primeiro, conecte-se à máquina do SQL Server com a área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="ccf3a-170">First, connect to the SQL Server machine with remote desktop.</span></span>

> [!INCLUDE [Connect to SQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-remote-desktop-connect.md)]

<span data-ttu-id="ccf3a-171">Em seguida, habilite o protocolo TCP/IP com o **SQL Server Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="ccf3a-171">Next, enable the TCP/IP protocol with **SQL Server Configuration Manager**.</span></span>

> [!INCLUDE [Connect to SQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-connection-tcp-protocol.md)]

## <a name="connect-with-ssms"></a><span data-ttu-id="ccf3a-172">Conectar com SSMS</span><span class="sxs-lookup"><span data-stu-id="ccf3a-172">Connect with SSMS</span></span>

<span data-ttu-id="ccf3a-173">As etapas a seguir mostram como criar um Rótulo DNS opcional para sua VM do Azure e, em seguida, conectar-se com o SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="ccf3a-173">The following steps show how to create an optional DNS Label for your Azure VM and then connect with SQL Server Management Studio (SSMS).</span></span>

[!INCLUDE [Connect to SQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]

## <a name="next-steps"></a><span data-ttu-id="ccf3a-174">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ccf3a-174">Next Steps</span></span>

<span data-ttu-id="ccf3a-175">Para ver instruções de provisionamento com estas etapas de conectividade, consulte [Provisionando uma Máquina Virtual do SQL Server no Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="ccf3a-175">To see provisioning instructions along with these connectivity steps, see [Provisioning a SQL Server Virtual Machine on Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

<span data-ttu-id="ccf3a-176">Para outros tópicos relacionados à execução do SQL Server em VMs do Azure, consulte [SQL Server em Máquinas Virtuais do Azure](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ccf3a-176">For other topics related to running SQL Server in Azure VMs, see [SQL Server on Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>