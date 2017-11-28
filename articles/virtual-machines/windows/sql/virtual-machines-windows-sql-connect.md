---
title: "aaaConnect tooa Máquina Virtual do SQL Server (Gerenciador de recursos) | Microsoft Docs"
description: "Saiba como tooconnect tooSQL Server em execução em uma máquina Virtual no Azure. Este tópico usa o modelo de implantação clássico hello. cenários de saudação diferem dependendo da configuração de rede hello e local de saudação do cliente de saudação."
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
ms.openlocfilehash: 7b127c14c37b9a72c19ed17f8b1dad61c7bc2d38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-sql-server-virtual-machine-on-azure-resource-manager"></a><span data-ttu-id="e5572-105">Conecte-se tooa Máquina Virtual do SQL Server no Azure (Gerenciador de recursos)</span><span class="sxs-lookup"><span data-stu-id="e5572-105">Connect tooa SQL Server Virtual Machine on Azure (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e5572-106">Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="e5572-106">Resource Manager</span></span>](virtual-machines-windows-sql-connect.md)
> * [<span data-ttu-id="e5572-107">Clássico</span><span class="sxs-lookup"><span data-stu-id="e5572-107">Classic</span></span>](../classic/sql-connect.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="e5572-108">Visão geral</span><span class="sxs-lookup"><span data-stu-id="e5572-108">Overview</span></span>

<span data-ttu-id="e5572-109">Este tópico descreve como tooconnect tooyour do SQL Server da instância em execução em uma máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="e5572-109">This topic describes how tooconnect tooyour SQL Server instance running on an Azure virtual machine.</span></span> <span data-ttu-id="e5572-110">Ele aborda alguns [cenários gerais de conectividade](#connection-scenarios) e descreve [etapas detalhadas para configurar a conectividade com o SQL Server em uma VM do Azure](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="e5572-110">It covers some [general connectivity scenarios](#connection-scenarios) and then provides [detailed steps for configuring SQL Server connectivity in an Azure VM](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="e5572-111">Para ver uma apresentação completa sobre provisionamento e conectividade, veja [Provisionando uma Máquina Virtual do SQL Server no Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="e5572-111">If you would rather have a full walk-through of both provisioning and connectivity, see [Provisioning a SQL Server Virtual Machine on Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

## <a name="connection-scenarios"></a><span data-ttu-id="e5572-112">Cenários de conexão</span><span class="sxs-lookup"><span data-stu-id="e5572-112">Connection scenarios</span></span>

<span data-ttu-id="e5572-113">forma de saudação um cliente se conecta tooSQL Server em execução em uma máquina Virtual é diferente dependendo do local de saudação do cliente hello e configuração de rede de saudação.</span><span class="sxs-lookup"><span data-stu-id="e5572-113">hello way a client connects tooSQL Server running on a Virtual Machine differs depending on hello location of hello client and hello networking configuration.</span></span>

<span data-ttu-id="e5572-114">Se você provisionar uma VM no portal do Azure de saudação do SQL Server, você tem a opção de saudação da especificação de tipo de saudação do **conectividade SQL**.</span><span class="sxs-lookup"><span data-stu-id="e5572-114">If you provision a SQL Server VM in hello Azure portal, you have hello option of specifying hello type of **SQL connectivity**.</span></span>

![Opção de conectividade SQL pública durante o provisionamento](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity.png)

<span data-ttu-id="e5572-116">As opções de conectividade incluem:</span><span class="sxs-lookup"><span data-stu-id="e5572-116">Your options for connectivity include:</span></span>

| <span data-ttu-id="e5572-117">Opção</span><span class="sxs-lookup"><span data-stu-id="e5572-117">Option</span></span> | <span data-ttu-id="e5572-118">Descrição</span><span class="sxs-lookup"><span data-stu-id="e5572-118">Description</span></span> |
|---|---|
| <span data-ttu-id="e5572-119">**Pública**</span><span class="sxs-lookup"><span data-stu-id="e5572-119">**Public**</span></span> | <span data-ttu-id="e5572-120">Conectar tooSQL Server sobre Olá internet</span><span class="sxs-lookup"><span data-stu-id="e5572-120">Connect tooSQL Server over hello internet</span></span> |
| <span data-ttu-id="e5572-121">**Privada**</span><span class="sxs-lookup"><span data-stu-id="e5572-121">**Private**</span></span> | <span data-ttu-id="e5572-122">Conectar tooSQL Server no hello mesma rede virtual</span><span class="sxs-lookup"><span data-stu-id="e5572-122">Connect tooSQL Server in hello same virtual network</span></span> |
| <span data-ttu-id="e5572-123">**Local**</span><span class="sxs-lookup"><span data-stu-id="e5572-123">**Local**</span></span> | <span data-ttu-id="e5572-124">Conecte-se tooSQL Server localmente no hello mesma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="e5572-124">Connect tooSQL Server locally on hello same virtual machine</span></span> | 

<span data-ttu-id="e5572-125">Olá, seções a seguir explicam Olá **pública** e **privada** opções em mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="e5572-125">hello following sections explain hello **Public** and **Private** options in more detail.</span></span>

## <a name="connect-toosql-server-over-hello-internet"></a><span data-ttu-id="e5572-126">Conecte-se tooSQL Server pela Internet da saudação</span><span class="sxs-lookup"><span data-stu-id="e5572-126">Connect tooSQL Server over hello Internet</span></span>

<span data-ttu-id="e5572-127">Se você desejar tooconnect tooyour mecanismo de banco de dados do SQL Server de saudação da Internet, selecione **pública** para Olá **conectividade SQL** tipo no portal de saudação durante o provisionamento.</span><span class="sxs-lookup"><span data-stu-id="e5572-127">If you want tooconnect tooyour SQL Server database engine from hello Internet, select **Public** for hello **SQL connectivity** type in hello portal during provisioning.</span></span> <span data-ttu-id="e5572-128">portal Olá Olá automaticamente as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="e5572-128">hello portal automatically does hello following steps:</span></span>

* <span data-ttu-id="e5572-129">Habilita o protocolo TCP/IP de saudação do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e5572-129">Enables hello TCP/IP protocol for SQL Server.</span></span>
* <span data-ttu-id="e5572-130">Configura uma saudação de tooopen de regra de firewall porta TCP do SQL Server (padrão: 1433).</span><span class="sxs-lookup"><span data-stu-id="e5572-130">Configures a firewall rule tooopen hello SQL Server TCP port (default 1433).</span></span>
* <span data-ttu-id="e5572-131">Habilita a Autenticação do SQL Server, necessária para acesso público.</span><span class="sxs-lookup"><span data-stu-id="e5572-131">Enables SQL Server Authentication, required for public access.</span></span>
* <span data-ttu-id="e5572-132">Configura o grupo de segurança de rede Olá no Olá VM tooall TCP no tráfego da saudação porta do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e5572-132">Configures hello network security group on hello VM tooall TCP traffic on hello SQL Server port.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e5572-133">imagens de máquina virtual de saudação para Olá SQL Server Developer e edições Express automaticamente não habilite o protocolo de saudação TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="e5572-133">hello virtual machine images for hello SQL Server Developer and Express editions do not automatically enable hello TCP/IP protocol.</span></span> <span data-ttu-id="e5572-134">Para edições Express e de desenvolvedor, você deve usar SQL Server Configuration Manager muito[habilitar manualmente o protocolo TCP/IP de saudação](#manualtcp) depois de criar hello VM.</span><span class="sxs-lookup"><span data-stu-id="e5572-134">For Developer and Express editions, you must use SQL Server Configuration Manager too[manually enable hello TCP/IP protocol](#manualtcp) after creating hello VM.</span></span>

<span data-ttu-id="e5572-135">Qualquer cliente com acesso à internet pode se conectar a instância do SQL Server toohello especificando o endereço IP público de saudação da máquina virtual de saudação ou qualquer rótulo DNS atribuído toothat endereço IP.</span><span class="sxs-lookup"><span data-stu-id="e5572-135">Any client with internet access can connect toohello SQL Server instance by specifying either hello public IP address of hello virtual machine or any DNS label assigned toothat IP address.</span></span> <span data-ttu-id="e5572-136">Se Olá porta do SQL Server é 1433, não é necessário toospecify na cadeia de caracteres de conexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="e5572-136">If hello SQL Server port is 1433, you do not need toospecify it in hello connection string.</span></span> <span data-ttu-id="e5572-137">saudação de cadeia de caracteres de conexão a seguir conecta tooa VM do SQL com um rótulo DNS de `sqlvmlabel.eastus.cloudapp.azure.com` usando a autenticação do SQL (você também pode usar endereço IP público de saudação).</span><span class="sxs-lookup"><span data-stu-id="e5572-137">hello following connection string connects tooa SQL VM with a DNS label of `sqlvmlabel.eastus.cloudapp.azure.com` using SQL Authentication (you could also use hello public IP address).</span></span>

```
Server=sqlvmlabel.eastus.cloudapp.azure.com;Integrated Security=false;User ID=<login_name>;Password=<your_password>
```

<span data-ttu-id="e5572-138">Embora isso habilita a conectividade de clientes sobre Olá da internet, isso não significa que qualquer pessoa pode se conectar a tooyour do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e5572-138">Although this enables connectivity for clients over hello internet, this does not imply that anyone can connect tooyour SQL Server.</span></span> <span data-ttu-id="e5572-139">Clientes fora tem correto toohello de nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="e5572-139">Outside clients have toohello correct username and password.</span></span> <span data-ttu-id="e5572-140">No entanto, para segurança adicional, você pode evitar a porta conhecida Olá 1433.</span><span class="sxs-lookup"><span data-stu-id="e5572-140">However, for additional security, you can avoid hello well-known port 1433.</span></span> <span data-ttu-id="e5572-141">Por exemplo, se você configurou toolisten do SQL Server na porta 1500 e estabelecida apropriadas do firewall e regras de grupo de segurança de rede, você pôde se conectar por meio do acréscimo Olá porta número toohello nome do servidor.</span><span class="sxs-lookup"><span data-stu-id="e5572-141">For example, if you configured SQL Server toolisten on port 1500 and established proper firewall and network security group rules, you could connect by appending hello port number toohello Server name.</span></span> <span data-ttu-id="e5572-142">Olá exemplo a seguir altera a saudação anterior, adicionando um número de porta personalizada, **1500**, toohello o nome do servidor:</span><span class="sxs-lookup"><span data-stu-id="e5572-142">hello following example alters hello previous one by adding a custom port number, **1500**, toohello server name:</span></span>

```
Server=sqlvmlabel.eastus.cloudapp.azure.com,1500;Integrated Security=false;User ID=<login_name>;Password=<your_password>"
```

> [!NOTE]
> <span data-ttu-id="e5572-143">Quando você consulta do SQL Server em uma VM em Olá internet, todos os dados de saída de hello Azure datacenter é o assunto toonormal [de preço em transferências de dados de saída](https://azure.microsoft.com/pricing/details/data-transfers/).</span><span class="sxs-lookup"><span data-stu-id="e5572-143">When you query SQL Server in a VM over hello internet, all outgoing data from hello Azure datacenter is subject toonormal [pricing on outbound data transfers](https://azure.microsoft.com/pricing/details/data-transfers/).</span></span>

## <a name="connect-toosql-server-within-a-virtual-network"></a><span data-ttu-id="e5572-144">Conecte-se tooSQL Server em uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="e5572-144">Connect tooSQL Server within a virtual network</span></span>

<span data-ttu-id="e5572-145">Quando você escolhe **privada** para Olá **conectividade SQL** tipo no portal hello, o Azure configura a maioria das configurações de saudação idênticas muito**público**.</span><span class="sxs-lookup"><span data-stu-id="e5572-145">When you choose **Private** for hello **SQL connectivity** type in hello portal, Azure configures most of hello settings identical too**Public**.</span></span> <span data-ttu-id="e5572-146">Olá uma diferença é que não há nenhuma regra tooallow do rede segurança grupo fora do tráfego na porta do SQL Server de saudação (padrão 1433).</span><span class="sxs-lookup"><span data-stu-id="e5572-146">hello one difference is that there is no network security group rule tooallow outside traffic on hello SQL Server port (default 1433).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e5572-147">imagens de máquina virtual de saudação para Olá SQL Server Developer e edições Express automaticamente não habilite o protocolo de saudação TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="e5572-147">hello virtual machine images for hello SQL Server Developer and Express editions do not automatically enable hello TCP/IP protocol.</span></span> <span data-ttu-id="e5572-148">Para edições Express e de desenvolvedor, você deve usar SQL Server Configuration Manager muito[habilitar manualmente o protocolo TCP/IP de saudação](#manualtcp) depois de criar hello VM.</span><span class="sxs-lookup"><span data-stu-id="e5572-148">For Developer and Express editions, you must use SQL Server Configuration Manager too[manually enable hello TCP/IP protocol](#manualtcp) after creating hello VM.</span></span>

<span data-ttu-id="e5572-149">Normalmente, a conectividade privada é usada em conjunto com [Rede Virtual](../../../virtual-network/virtual-networks-overview.md), o que permite vários cenários.</span><span class="sxs-lookup"><span data-stu-id="e5572-149">Private connectivity is often used in conjunction with [Virtual Network](../../../virtual-network/virtual-networks-overview.md), which enables several scenarios.</span></span> <span data-ttu-id="e5572-150">Você pode se conectar a máquinas virtuais na mesma rede virtual, mesmo se essas VMs existe em grupos de recursos diferentes de saudação.</span><span class="sxs-lookup"><span data-stu-id="e5572-150">You can connect VMs in hello same virtual network, even if those VMs exist in different resource groups.</span></span> <span data-ttu-id="e5572-151">E com um [VPN site a site](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), você pode criar uma arquitetura híbrida que conecta as VMs a computadores e redes locais.</span><span class="sxs-lookup"><span data-stu-id="e5572-151">And with a [site-to-site VPN](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), you can create a hybrid architecture that connects VMs with on-premises networks and machines.</span></span>

<span data-ttu-id="e5572-152">Redes virtuais também permitem que você toojoin seu domínio de tooa VMs do Azure.</span><span class="sxs-lookup"><span data-stu-id="e5572-152">Virtual networks also enable     you toojoin your Azure VMs tooa domain.</span></span> <span data-ttu-id="e5572-153">Isso é Olá somente o modo toouse a autenticação do Windows tooSQL Server.</span><span class="sxs-lookup"><span data-stu-id="e5572-153">This is hello only way toouse Windows Authentication tooSQL Server.</span></span> <span data-ttu-id="e5572-154">Olá outros cenários de conexão requerem autenticação do SQL com nomes de usuário e senhas.</span><span class="sxs-lookup"><span data-stu-id="e5572-154">hello other connection scenarios require SQL Authentication with user names and passwords.</span></span>

<span data-ttu-id="e5572-155">Supondo que você configurou o DNS em sua rede virtual, você pode se conectar a instância do SQL Server tooyour especificando o nome do computador Olá VM do SQL Server na cadeia de caracteres de conexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="e5572-155">Assuming that you have configured DNS in your virtual network, you can connect tooyour SQL Server instance by specifying hello SQL Server VM computer name in hello connection string.</span></span> <span data-ttu-id="e5572-156">saudação de exemplo a seguir também pressupõe que a autenticação do Windows também foi configurada e usuário Olá foi concedido a instância do SQL Server toohello acesso.</span><span class="sxs-lookup"><span data-stu-id="e5572-156">hello following example also assumes that Windows Authentication has also been configured and that hello user has been granted access toohello SQL Server instance.</span></span>

```
Server=mysqlvm;Integrated Security=true
```

## <span data-ttu-id="e5572-157"><a id="change"></a> Alterar as configurações de conectividade do SQL</span><span class="sxs-lookup"><span data-stu-id="e5572-157"><a id="change"></a> Change SQL connectivity settings</span></span>

<span data-ttu-id="e5572-158">Você pode alterar as configurações de conectividade Olá para sua máquina de virtual do SQL Server no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e5572-158">You can change hello connectivity settings for your SQL Server virtual machine in hello Azure portal.</span></span>

1. <span data-ttu-id="e5572-159">No portal do Azure de Olá, selecione **máquinas virtuais**.</span><span class="sxs-lookup"><span data-stu-id="e5572-159">In hello Azure portal, select **Virtual Machines**.</span></span>

2. <span data-ttu-id="e5572-160">Selecione sua VM do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e5572-160">Select your SQL Server VM.</span></span>

3. <span data-ttu-id="e5572-161">Em **Configurações**, clique em **Configuração do SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="e5572-161">Under **Settings**, click **SQL Server configuration**.</span></span>

4. <span data-ttu-id="e5572-162">Saudação de alteração **o nível de conectividade do SQL** tooyour configuração necessária.</span><span class="sxs-lookup"><span data-stu-id="e5572-162">Change hello **SQL connectivity level** tooyour required setting.</span></span> <span data-ttu-id="e5572-163">Opcionalmente, você pode usar este Olá toochange de área porta do SQL Server ou as configurações de autenticação do SQL hello.</span><span class="sxs-lookup"><span data-stu-id="e5572-163">You can optionally use this area toochange hello SQL Server port or hello SQL Authentication settings.</span></span>

   ![Alterar a conectividade do SQL](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity-change.png)

5. <span data-ttu-id="e5572-165">Aguarde alguns minutos para Olá toocomplete de atualização.</span><span class="sxs-lookup"><span data-stu-id="e5572-165">Wait several minutes for hello update toocomplete.</span></span>

   ![Notificação de atualização da VM do SQL](./media/virtual-machines-windows-sql-connect/sql-vm-updating-notification.png)

## <span data-ttu-id="e5572-167"><a id="manualtcp"></a> Habilitar TCP/IP para as edições Developer e Express</span><span class="sxs-lookup"><span data-stu-id="e5572-167"><a id="manualtcp"></a> Enable TCP/IP for Developer and Express editions</span></span>

<span data-ttu-id="e5572-168">Ao alterar as configurações de conectividade do SQL Server, o Azure não habilita automaticamente protocolo hello TCP/IP para edições Express e o SQL Server Developer.</span><span class="sxs-lookup"><span data-stu-id="e5572-168">When changing SQL Server connectivity settings, Azure does not automatically enable hello TCP/IP protocol for SQL Server Developer and Express editions.</span></span> <span data-ttu-id="e5572-169">Olá estas etapas explicam como toomanually habilitar TCP/IP para que você pode se conectar remotamente pelo endereço IP.</span><span class="sxs-lookup"><span data-stu-id="e5572-169">hello steps below explain how toomanually enable TCP/IP so that you can connect remotely by IP address.</span></span>

<span data-ttu-id="e5572-170">Primeiro, conecte-se a máquina do SQL Server toohello com área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="e5572-170">First, connect toohello SQL Server machine with remote desktop.</span></span>

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-remote-desktop-connect.md)]

<span data-ttu-id="e5572-171">Em seguida, habilite o protocolo TCP/IP de saudação com **SQL Server Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="e5572-171">Next, enable hello TCP/IP protocol with **SQL Server Configuration Manager**.</span></span>

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-connection-tcp-protocol.md)]

## <a name="connect-with-ssms"></a><span data-ttu-id="e5572-172">Conectar com SSMS</span><span class="sxs-lookup"><span data-stu-id="e5572-172">Connect with SSMS</span></span>

<span data-ttu-id="e5572-173">Olá etapas a seguir mostram como toocreate um opcional DNS de rótulo para VMs do Azure e, em seguida, conecte-se com o SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="e5572-173">hello following steps show how toocreate an optional DNS Label for your Azure VM and then connect with SQL Server Management Studio (SSMS).</span></span>

[!INCLUDE [Connect tooSQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]

## <a name="next-steps"></a><span data-ttu-id="e5572-174">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e5572-174">Next Steps</span></span>

<span data-ttu-id="e5572-175">instruções de provisionamento toosee junto com essas etapas de conectividade, consulte [provisionar uma máquina Virtual do SQL Server no Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="e5572-175">toosee provisioning instructions along with these connectivity steps, see [Provisioning a SQL Server Virtual Machine on Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

<span data-ttu-id="e5572-176">Para outros tópicos relacionados toorunning do SQL Server em VMs do Azure, consulte [do SQL Server em máquinas virtuais Azure](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e5572-176">For other topics related toorunning SQL Server in Azure VMs, see [SQL Server on Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
