---
title: aaaRemote Desktop tooa VM do Linux | Microsoft Docs
description: "Saiba como tooinstall e configurar a área de trabalho remota tooconnect tooa VM Linux do Microsoft Azure para o modelo de implantação clássico Olá"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 34348659-ddb7-41da-82d6-b5885859e7e4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: mingzhan
ms.openlocfilehash: aadd6e87883cf9cacf9d198b680669d594206e61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-remote-desktop-tooconnect-tooa-microsoft-azure-linux-vm"></a><span data-ttu-id="958db-103">Usando a área de trabalho remota tooconnect tooa VM Linux do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="958db-103">Using Remote Desktop tooconnect tooa Microsoft Azure Linux VM</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="958db-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="958db-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="958db-105">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="958db-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="958db-106">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="958db-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="958db-107">Para Olá atualizado a versão do Gerenciador de recursos deste artigo, consulte [aqui](../use-remote-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="958db-107">For hello updated Resource Manager version of this article, see [here](../use-remote-desktop.md).</span></span>

## <a name="overview"></a><span data-ttu-id="958db-108">Visão geral</span><span class="sxs-lookup"><span data-stu-id="958db-108">Overview</span></span>
<span data-ttu-id="958db-109">O protocolo RDP é um protocolo proprietário usado para o Windows.</span><span class="sxs-lookup"><span data-stu-id="958db-109">RDP (Remote Desktop Protocol) is a proprietary protocol used for Windows.</span></span> <span data-ttu-id="958db-110">Como podemos usar RDP tooconnect tooa VM (máquina virtual) do Linux remotamente?</span><span class="sxs-lookup"><span data-stu-id="958db-110">How can we use RDP tooconnect tooa Linux VM (virtual machine) remotely?</span></span>

<span data-ttu-id="958db-111">Este guia fornecerá Olá resposta!</span><span class="sxs-lookup"><span data-stu-id="958db-111">This guidance will give you hello answer!</span></span> <span data-ttu-id="958db-112">Ele ajudará xrdp tooinstall e configuração em sua VM Linux do Microsoft Azure, que permite a conexão tooit com área de trabalho remota de um computador Windows.</span><span class="sxs-lookup"><span data-stu-id="958db-112">It will help you tooinstall and config xrdp on your Microsoft Azure Linux VM, which lets you connect tooit with Remote Desktop from a Windows machine.</span></span> <span data-ttu-id="958db-113">Usaremos a VM do Linux executando Ubuntu ou OpenSUSE como exemplo hello neste guia.</span><span class="sxs-lookup"><span data-stu-id="958db-113">We will use Linux VM running Ubuntu or OpenSUSE as hello example in this guidance.</span></span>

<span data-ttu-id="958db-114">ferramenta de xrdp Olá é uma origem aberta no servidor RDP que permite a você tooconnect seu servidor Linux com área de trabalho remota de um computador Windows.</span><span class="sxs-lookup"><span data-stu-id="958db-114">hello xrdp tool is an open source RDP server that allows you tooconnect your Linux server with Remote Desktop from a Windows machine.</span></span> <span data-ttu-id="958db-115">O RDP tem um desempenho melhor do que a VNC (Computação de Rede Virtual).</span><span class="sxs-lookup"><span data-stu-id="958db-115">RDP has better performance than VNC (Virtual Network Computing).</span></span> <span data-ttu-id="958db-116">A VNC renderiza usando gráficos de qualidade de JPEG e pode ser lenta, enquanto o RDP é rápido e claro.</span><span class="sxs-lookup"><span data-stu-id="958db-116">VNC renders using JPEG-quality graphics and can be slow, whereas RDP is fast and crystal clear.</span></span>

> [!NOTE]
> <span data-ttu-id="958db-117">Você já deve ter uma VM do Microsoft Azure executando o Linux.</span><span class="sxs-lookup"><span data-stu-id="958db-117">You must already have an Microsoft Azure VM running Linux.</span></span> <span data-ttu-id="958db-118">toocreate e configurar uma VM do Linux, consulte Olá [tutorial de VM do Linux Azure](createportal.md).</span><span class="sxs-lookup"><span data-stu-id="958db-118">toocreate and set up a Linux VM, see hello [Azure Linux VM tutorial](createportal.md).</span></span>
> 
> 

## <a name="create-an-endpoint-for-remote-desktop"></a><span data-ttu-id="958db-119">Criar um ponto de extremidade para a Área de Trabalho Remota</span><span class="sxs-lookup"><span data-stu-id="958db-119">Create an endpoint for Remote Desktop</span></span>
<span data-ttu-id="958db-120">Usaremos ponto de extremidade do saudação padrão 3389 para área de trabalho remota deste documento. Configurar o ponto de extremidade 3389 como `Remote Desktop` tooyour VM Linux como abaixo:</span><span class="sxs-lookup"><span data-stu-id="958db-120">We will use hello default endpoint 3389 for Remote Desktop in this doc. Set up 3389 endpoint as `Remote Desktop` tooyour Linux VM like below:</span></span>

![imagem](./media/remote-desktop/endpoint-for-linux-server.png)

<span data-ttu-id="958db-122">Se você não souber como tooset um ponto de extremidade para sua VM, consulte [neste guia](setup-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="958db-122">If you don't know how tooset up an endpoint for your VM, see [this guidance](setup-endpoints.md).</span></span>

## <a name="install-gnome-desktop"></a><span data-ttu-id="958db-123">Instalar o Gnome Desktop</span><span class="sxs-lookup"><span data-stu-id="958db-123">Install Gnome Desktop</span></span>
<span data-ttu-id="958db-124">Conecte-se tooyour VM Linux por meio de `putty`e instalar `Gnome Desktop`.</span><span class="sxs-lookup"><span data-stu-id="958db-124">Connect tooyour Linux VM through `putty`, and install `Gnome Desktop`.</span></span>

<span data-ttu-id="958db-125">Para o Ubuntu, use:</span><span class="sxs-lookup"><span data-stu-id="958db-125">For Ubuntu, use:</span></span>

    #sudo apt-get update
    #sudo apt-get install ubuntu-desktop


<span data-ttu-id="958db-126">Para OpenSUSE, use:</span><span class="sxs-lookup"><span data-stu-id="958db-126">For OpenSUSE, use:</span></span>

    #sudo zypper install gnome-session

## <a name="install-xrdp"></a><span data-ttu-id="958db-127">Instalar o xrdp</span><span class="sxs-lookup"><span data-stu-id="958db-127">Install xrdp</span></span>
<span data-ttu-id="958db-128">Para o Ubuntu, use:</span><span class="sxs-lookup"><span data-stu-id="958db-128">For Ubuntu, use:</span></span>

    #sudo apt-get install xrdp

<span data-ttu-id="958db-129">Para OpenSUSE, use:</span><span class="sxs-lookup"><span data-stu-id="958db-129">For OpenSUSE, use:</span></span>

> [!NOTE]
> <span data-ttu-id="958db-130">Atualize versão de OpenSUSE Olá com versão de hello que você está usando no hello comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="958db-130">Update hello OpenSUSE version with hello version you are using in hello following command.</span></span> <span data-ttu-id="958db-131">exemplo Hello abaixo é para `OpenSUSE 13.2`.</span><span class="sxs-lookup"><span data-stu-id="958db-131">hello example below is for `OpenSUSE 13.2`.</span></span>
> 
> 

    #sudo zypper in http://download.opensuse.org/repositories/X11:/RemoteDesktop/openSUSE_13.2/x86_64/xrdp-0.9.0git.1401423964-2.1.x86_64.rpm
    #sudo zypper install tigervnc xorg-x11-Xvnc xterm remmina-plugin-vnc


## <a name="start-xrdp-and-set-xdrp-service-at-boot-up"></a><span data-ttu-id="958db-132">Inicie o xrdp e defina o serviço xdrp na inicialização</span><span class="sxs-lookup"><span data-stu-id="958db-132">Start xrdp and set xdrp service at boot-up</span></span>
<span data-ttu-id="958db-133">Para OpenSUSE, use:</span><span class="sxs-lookup"><span data-stu-id="958db-133">For OpenSUSE, use:</span></span>

    #sudo systemctl start xrdp
    #sudo systemctl enable xrdp

<span data-ttu-id="958db-134">Para Ubuntu, o xrdp será iniciado e habilitado automaticamente na inicialização após a instalação.</span><span class="sxs-lookup"><span data-stu-id="958db-134">For Ubuntu, xrdp will be started and eanbled at boot-up automatically after installation.</span></span>

## <a name="using-xfce-if-you-are-using-an-ubuntu-version-later-than-ubuntu-1204lts"></a><span data-ttu-id="958db-135">Usando xfce se você estiver usando uma versão do Ubuntu posterior ao Ubuntu 12.04LTS</span><span class="sxs-lookup"><span data-stu-id="958db-135">Using xfce if you are using an Ubuntu version later than Ubuntu 12.04LTS</span></span>
<span data-ttu-id="958db-136">Porque a versão atual Olá de xrdp não oferece suporte Desktop Gnome para Ubuntu versões posterior Ubuntu 12.04LTS, usaremos `xfce` área de trabalho em vez disso.</span><span class="sxs-lookup"><span data-stu-id="958db-136">Because hello current version of xrdp does not support Gnome Desktop for  Ubuntu versions later than Ubuntu 12.04LTS, we will use `xfce` Desktop instead.</span></span>

<span data-ttu-id="958db-137">tooinstall `xfce`, use este comando:</span><span class="sxs-lookup"><span data-stu-id="958db-137">tooinstall `xfce`, use this command:</span></span>

    #sudo apt-get install xubuntu-desktop

<span data-ttu-id="958db-138">Em seguida, habilite `xfce` usando este comando:</span><span class="sxs-lookup"><span data-stu-id="958db-138">Then enable `xfce` using this command:</span></span>

    #echo xfce4-session >~/.xsession

<span data-ttu-id="958db-139">Editar o arquivo de configuração de saudação `/etc/xrdp/startwm.sh`:</span><span class="sxs-lookup"><span data-stu-id="958db-139">Edit hello config file `/etc/xrdp/startwm.sh`:</span></span>

    #sudo vi /etc/xrdp/startwm.sh   

<span data-ttu-id="958db-140">Adicionar linha hello `xfce4-session` antes da linha de saudação `/etc/X11/Xsession`.</span><span class="sxs-lookup"><span data-stu-id="958db-140">Add hello line `xfce4-session` before hello line `/etc/X11/Xsession`.</span></span>

<span data-ttu-id="958db-141">toorestart Olá xrdp serviço, use:</span><span class="sxs-lookup"><span data-stu-id="958db-141">toorestart hello xrdp service, use this:</span></span>

    #sudo service xrdp restart


## <a name="connect-your-linux-vm-from-a-windows-machine"></a><span data-ttu-id="958db-142">Conectar-se à VM Linux de uma máquina com Windows</span><span class="sxs-lookup"><span data-stu-id="958db-142">Connect your Linux VM from a Windows machine</span></span>
<span data-ttu-id="958db-143">Em um computador Windows, iniciar o cliente de área de trabalho remota hello e insira o nome DNS da VM Linux.</span><span class="sxs-lookup"><span data-stu-id="958db-143">In a Windows machine, start hello Remote Desktop client and input your Linux VM DNS name.</span></span> <span data-ttu-id="958db-144">Ou vá toohello painel da VM no portal do Azure de saudação e clique em `Connect` tooconnect sua VM do Linux.</span><span class="sxs-lookup"><span data-stu-id="958db-144">Or go toohello Dashboard of your VM in hello Azure portal and click `Connect` tooconnect your Linux VM.</span></span> <span data-ttu-id="958db-145">Nesse caso, você ver a janela de logon hello:</span><span class="sxs-lookup"><span data-stu-id="958db-145">In that case, you see hello login window:</span></span>

![imagem](./media/remote-desktop/no2.png)

<span data-ttu-id="958db-147">Faça logon com o nome de usuário de saudação e a senha da sua VM do Linux.</span><span class="sxs-lookup"><span data-stu-id="958db-147">Log in with hello user name and password of your Linux VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="958db-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="958db-148">Next steps</span></span>
<span data-ttu-id="958db-149">Para obter mais informações sobre o uso do xrdp, consulte [http://www.xrdp.org/](http://www.xrdp.org/).</span><span class="sxs-lookup"><span data-stu-id="958db-149">For more information about using xrdp, see [http://www.xrdp.org/](http://www.xrdp.org/).</span></span>
