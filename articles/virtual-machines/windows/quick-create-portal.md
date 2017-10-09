---
title: "aaaAzure início rápido - criar Portal de VM do Windows | Microsoft Docs"
description: "Início Rápido do Azure – Portal Criar VM do Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5646ad51244db6d214c0121d1f7cc45c59f9a78b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-hello-azure-portal"></a><span data-ttu-id="8063e-103">Criar uma máquina virtual do Windows com hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8063e-103">Create a Windows virtual machine with hello Azure portal</span></span>

<span data-ttu-id="8063e-104">Máquinas virtuais do Azure podem ser criadas por meio de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8063e-104">Azure virtual machines can be created through hello Azure portal.</span></span> <span data-ttu-id="8063e-105">Esse método fornece uma interface do usuário baseada em navegador para a criação e configuração de máquinas virtuais e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="8063e-105">This method provides a browser-based user interface for creating and configuring virtual machines and all related resources.</span></span> <span data-ttu-id="8063e-106">Este guia de início rápido percorre criando uma máquina virtual e instalar um servidor Web no hello VM.</span><span class="sxs-lookup"><span data-stu-id="8063e-106">This Quickstart steps through creating a virtual machine and installing a webserver on hello VM.</span></span>

<span data-ttu-id="8063e-107">Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="8063e-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="8063e-108">Faça logon no tooAzure</span><span class="sxs-lookup"><span data-stu-id="8063e-108">Log in tooAzure</span></span>

<span data-ttu-id="8063e-109">Faça logon em toohello portal do Azure em http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="8063e-109">Log in toohello Azure portal at http://portal.azure.com.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="8063e-110">Criar máquina virtual</span><span class="sxs-lookup"><span data-stu-id="8063e-110">Create virtual machine</span></span>

1. <span data-ttu-id="8063e-111">Clique em Olá **novo** botão localizado no canto superior esquerdo de saudação do hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8063e-111">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="8063e-112">Selecione **Computação** e, em seguida, selecione **Windows Server 2016 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="8063e-112">Select **Compute**, and then select **Windows Server 2016 Datacenter**.</span></span> 

3. <span data-ttu-id="8063e-113">Insira informações da máquina virtual hello.</span><span class="sxs-lookup"><span data-stu-id="8063e-113">Enter hello virtual machine information.</span></span> <span data-ttu-id="8063e-114">nome de usuário de saudação e a senha digitada aqui é toolog usada na máquina virtual de toohello.</span><span class="sxs-lookup"><span data-stu-id="8063e-114">hello user name and password entered here is used toolog in toohello virtual machine.</span></span> <span data-ttu-id="8063e-115">Ao concluir, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="8063e-115">When complete, click **OK**.</span></span>

    ![Insira as informações básicas sobre sua VM na folha portal Olá](./media/quick-create-portal/create-windows-vm-portal-basic-blade.png)  

4. <span data-ttu-id="8063e-117">Selecione um tamanho para Olá VM.</span><span class="sxs-lookup"><span data-stu-id="8063e-117">Select a size for hello VM.</span></span> <span data-ttu-id="8063e-118">toosee mais tamanhos, selecione **exibir todos os** ou alterar Olá **suporte para o tipo de disco** filtro.</span><span class="sxs-lookup"><span data-stu-id="8063e-118">toosee more sizes, select **View all** or change hello **Supported disk type** filter.</span></span> 

    ![A captura de tela que mostra os tamanhos da VM](./media/quick-create-portal/create-windows-vm-portal-sizes.png)  

5. <span data-ttu-id="8063e-120">Na folha de configurações hello, lembre-Olá padrões e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="8063e-120">On hello settings blade, keep hello defaults and click **OK**.</span></span>

6. <span data-ttu-id="8063e-121">Na página de resumo de saudação, clique em **Okey** toostart implantação da máquina virtual hello.</span><span class="sxs-lookup"><span data-stu-id="8063e-121">On hello summary page, click **Ok** toostart hello virtual machine deployment.</span></span>

7. <span data-ttu-id="8063e-122">Olá VM será fixado toohello painel do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8063e-122">hello VM will be pinned toohello Azure portal dashboard.</span></span> <span data-ttu-id="8063e-123">Após a conclusão da implantação hello, folha de resumo de VM Olá é aberto automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8063e-123">Once hello deployment has completed, hello VM summary blade automatically opens.</span></span>


## <a name="connect-toovirtual-machine"></a><span data-ttu-id="8063e-124">Conectar máquina toovirtual</span><span class="sxs-lookup"><span data-stu-id="8063e-124">Connect toovirtual machine</span></span>

<span data-ttu-id="8063e-125">Crie uma máquina de virtual de toohello de conexão de área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="8063e-125">Create a remote desktop connection toohello virtual machine.</span></span>

1. <span data-ttu-id="8063e-126">Clique em Olá **conectar** botão nas propriedades de máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="8063e-126">Click hello **Connect** button on hello virtual machine properties.</span></span> <span data-ttu-id="8063e-127">Um arquivo do protocolo RDP (.rdp) é criado e baixado.</span><span class="sxs-lookup"><span data-stu-id="8063e-127">A Remote Desktop Protocol file (.rdp file) is created and downloaded.</span></span>

    ![Portal 9](./media/quick-create-portal/quick-create-portal/portal-quick-start-9.png) 

2. <span data-ttu-id="8063e-129">tooconnect tooyour VM, abra Olá baixado o arquivo RDP.</span><span class="sxs-lookup"><span data-stu-id="8063e-129">tooconnect tooyour VM, open hello downloaded RDP file.</span></span> <span data-ttu-id="8063e-130">Se solicitado, clique em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="8063e-130">If prompted, click **Connect**.</span></span> <span data-ttu-id="8063e-131">Em um Mac, você precisa de um cliente RDP como esta [área de trabalho remota](https://itunes.apple.com/us/app/microsoft-remote-desktop/id715768417?mt=12) de saudação Mac App Store.</span><span class="sxs-lookup"><span data-stu-id="8063e-131">On a Mac, you need an RDP client such as this [Remote Desktop Client](https://itunes.apple.com/us/app/microsoft-remote-desktop/id715768417?mt=12) from hello Mac App Store.</span></span>

3. <span data-ttu-id="8063e-132">Insira o nome de usuário de saudação e senha que você especificou ao criar a máquina virtual de saudação, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="8063e-132">Enter hello user name and password you specified when creating hello virtual machine, then click **Ok**.</span></span>

4. <span data-ttu-id="8063e-133">Você receberá um aviso de certificado durante o processo de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="8063e-133">You may receive a certificate warning during hello sign-in process.</span></span> <span data-ttu-id="8063e-134">Clique em **Sim** ou **continuar** tooproceed com conexão hello.</span><span class="sxs-lookup"><span data-stu-id="8063e-134">Click **Yes** or **Continue** tooproceed with hello connection.</span></span>


## <a name="install-iis-using-powershell"></a><span data-ttu-id="8063e-135">Instalar o IIS usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="8063e-135">Install IIS using PowerShell</span></span>

<span data-ttu-id="8063e-136">Na máquina virtual de hello, iniciar uma sessão do PowerShell e execute Olá tooinstall comando IIS a seguir.</span><span class="sxs-lookup"><span data-stu-id="8063e-136">On hello virtual machine, start a PowerShell session and run hello following command tooinstall IIS.</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

<span data-ttu-id="8063e-137">Quando terminar, sair da sessão RDP hello e retornam propriedades da VM Olá em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8063e-137">When done, exit hello RDP session and return hello VM properties in hello Azure portal.</span></span>

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="8063e-138">Abra a porta 80 para tráfego da Web</span><span class="sxs-lookup"><span data-stu-id="8063e-138">Open port 80 for web traffic</span></span> 

<span data-ttu-id="8063e-139">Um Grupo de Segurança de Rede (NSG) protege o tráfego de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="8063e-139">A Network security group (NSG) secures inbound and outbound traffic.</span></span> <span data-ttu-id="8063e-140">Quando uma máquina virtual é criada a partir Olá portal do Azure, uma regra de entrada é criada na porta 3389 para conexões RDP.</span><span class="sxs-lookup"><span data-stu-id="8063e-140">When a VM is created from hello Azure portal, an inbound rule is created on port 3389 for RDP connections.</span></span> <span data-ttu-id="8063e-141">Como essa VM hospeda um servidor Web, uma regra NSG necessita toobe criado para a porta 80.</span><span class="sxs-lookup"><span data-stu-id="8063e-141">Because this VM hosts a webserver, an NSG rule needs toobe created for port 80.</span></span>

1. <span data-ttu-id="8063e-142">Na máquina virtual de Olá, clique em nome de saudação do hello **grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="8063e-142">On hello virtual machine, click hello name of hello **Resource group**.</span></span>
2. <span data-ttu-id="8063e-143">Selecione Olá **grupo de segurança de rede**.</span><span class="sxs-lookup"><span data-stu-id="8063e-143">Select hello **network security group**.</span></span> <span data-ttu-id="8063e-144">Olá NSG pode ser identificado usando Olá **tipo** coluna.</span><span class="sxs-lookup"><span data-stu-id="8063e-144">hello NSG can be identified using hello **Type** column.</span></span> 
3. <span data-ttu-id="8063e-145">No menu esquerdo hello, em configurações, clique em **regras de segurança de entrada**.</span><span class="sxs-lookup"><span data-stu-id="8063e-145">On hello left-hand menu, under settings, click **Inbound security rules**.</span></span>
4. <span data-ttu-id="8063e-146">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="8063e-146">Click on **Add**.</span></span>
5. <span data-ttu-id="8063e-147">Em **Nome**, digite **http**.</span><span class="sxs-lookup"><span data-stu-id="8063e-147">In **Name**, type **http**.</span></span> <span data-ttu-id="8063e-148">Certifique-se de **intervalo de portas** é definir too80 e **ação** está definido muito**permitir**.</span><span class="sxs-lookup"><span data-stu-id="8063e-148">Make sure **Port range** is set too80 and **Action** is set too**Allow**.</span></span> 
6. <span data-ttu-id="8063e-149">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="8063e-149">Click **OK**.</span></span>


## <a name="view-hello-iis-welcome-page"></a><span data-ttu-id="8063e-150">Olá exibir página de boas-vindas do IIS</span><span class="sxs-lookup"><span data-stu-id="8063e-150">View hello IIS welcome page</span></span>

<span data-ttu-id="8063e-151">Com o IIS instalado e a porta 80 abra tooyour VM, Olá servidorweb agora pode ser acessado de saudação à internet.</span><span class="sxs-lookup"><span data-stu-id="8063e-151">With IIS installed, and port 80 open tooyour VM, hello webserver can now be accessed from hello internet.</span></span> <span data-ttu-id="8063e-152">Abra um navegador da web e digite o endereço IP público de saudação do hello VM.</span><span class="sxs-lookup"><span data-stu-id="8063e-152">Open a web browser, and enter hello public IP address of hello VM.</span></span> <span data-ttu-id="8063e-153">endereço IP público de saudação pode ser encontrado na folha VM Olá no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8063e-153">hello public IP address can be found on hello VM blade in hello Azure portal.</span></span>

![Site do IIS padrão](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="8063e-155">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="8063e-155">Clean up resources</span></span>

<span data-ttu-id="8063e-156">Quando não é mais necessário, exclua o grupo de recursos de saudação, máquina virtual e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="8063e-156">When no longer needed, delete hello resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="8063e-157">toodo, portanto, selecione o grupo de recursos de saudação da folha de máquina virtual hello e clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="8063e-157">toodo so, select hello resource group from hello virtual machine blade and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8063e-158">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8063e-158">Next steps</span></span>

<span data-ttu-id="8063e-159">Neste início rápido, você implantou uma máquina virtual simples, uma regra de grupo de segurança de rede e instalou um servidor Web.</span><span class="sxs-lookup"><span data-stu-id="8063e-159">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="8063e-160">toolearn mais sobre máquinas virtuais do Azure, continuar toohello tutorial para VMs do Windows.</span><span class="sxs-lookup"><span data-stu-id="8063e-160">toolearn more about Azure virtual machines, continue toohello tutorial for Windows VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8063e-161">Tutoriais de máquina virtual do Windows Azure</span><span class="sxs-lookup"><span data-stu-id="8063e-161">Azure Windows virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
