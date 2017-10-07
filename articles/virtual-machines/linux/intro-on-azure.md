---
title: tooLinux aaaIntroduction no Azure | Microsoft Docs
description: "Saiba como usar máquinas virtuais Linux no Azure."
services: virtual-machines-linux
documentationcenter: python
author: szarkos
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: b13bf305-87bf-4df3-815e-e8f6337aa6ea
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: szark
ms.openlocfilehash: 3a931447ee23ce7000174ca314c3e10abc6b8e74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toolinux-on-azure"></a><span data-ttu-id="bc5d3-103">Introdução tooLinux no Azure</span><span class="sxs-lookup"><span data-stu-id="bc5d3-103">Introduction tooLinux on Azure</span></span>
<span data-ttu-id="bc5d3-104">Este tópico fornece uma visão geral de alguns aspectos do uso de máquinas virtuais Linux em Olá nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="bc5d3-104">This topic provides an overview of some aspects of using Linux virtual machines in hello Azure cloud.</span></span> <span data-ttu-id="bc5d3-105">Implantar uma máquina virtual Linux é um processo simples usando uma imagem da Galeria de saudação.</span><span class="sxs-lookup"><span data-stu-id="bc5d3-105">Deploying a Linux virtual machine is a straightforward process using an image from hello gallery.</span></span>

## <a name="authentication-usernames-passwords-and-ssh-keys"></a><span data-ttu-id="bc5d3-106">Autenticação: nomes de usuário, senhas e chaves SSH.</span><span class="sxs-lookup"><span data-stu-id="bc5d3-106">Authentication: Usernames, Passwords and SSH Keys</span></span>
<span data-ttu-id="bc5d3-107">Ao criar uma máquina virtual do Linux usando Olá portal do Azure, você será solicitado tooprovide qualquer nome de usuário e senha ou uma chave pública SSH.</span><span class="sxs-lookup"><span data-stu-id="bc5d3-107">When creating a Linux virtual machine using hello Azure portal, you are asked tooprovide a either username and password or an SSH public key.</span></span> <span data-ttu-id="bc5d3-108">Olá, escolha um nome de usuário para implantar uma máquina virtual do Linux no Azure é toohello assunto seguinte restrição: nomes de contas do sistema (UID < 100) já está presente no hello máquina virtual não são permitidos, 'root' por exemplo.</span><span class="sxs-lookup"><span data-stu-id="bc5d3-108">hello choice of a username for deploying a Linux virtual machine on Azure is subject toohello following constraint: names of system accounts (UID <100) already present in hello virtual machine are not allowed, 'root' for example.</span></span>

* <span data-ttu-id="bc5d3-109">Veja [Criar uma máquina virtual que executa Linux](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="bc5d3-109">See [Create a Virtual Machine Running Linux](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* <span data-ttu-id="bc5d3-110">Consulte [como tooUse SSH com Linux no Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="bc5d3-110">See [How tooUse SSH with Linux on Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="obtaining-superuser-privileges-using-sudo"></a><span data-ttu-id="bc5d3-111">Obtendo privilégios de superusuário usando o `sudo`</span><span class="sxs-lookup"><span data-stu-id="bc5d3-111">Obtaining Superuser Privileges Using `sudo`</span></span>
<span data-ttu-id="bc5d3-112">conta de usuário de saudação que é especificada durante a implantação de instância de máquina virtual no Azure é uma conta privilegiada.</span><span class="sxs-lookup"><span data-stu-id="bc5d3-112">hello user account that is specified during virtual machine instance deployment on Azure is a privileged account.</span></span> <span data-ttu-id="bc5d3-113">Essa conta é configurada por hello Azure Linux Agent toobe tooelevate capaz de privilégios tooroot (conta de superusuário) usando Olá `sudo` utilitário.</span><span class="sxs-lookup"><span data-stu-id="bc5d3-113">This account is configured by hello Azure Linux Agent toobe able tooelevate privileges tooroot (superuser account) using hello `sudo` utility.</span></span> <span data-ttu-id="bc5d3-114">Depois de conectado usando essa conta de usuário, você será toorun capaz de comandos como raiz usando sintaxe de comando hello:</span><span class="sxs-lookup"><span data-stu-id="bc5d3-114">Once logged in using this user account, you will be able toorun commands as root using hello command syntax:</span></span>

    # sudo <COMMAND>

<span data-ttu-id="bc5d3-115">Opcionalmente, você pode obter um shell de root usando **sudo -s**.</span><span class="sxs-lookup"><span data-stu-id="bc5d3-115">You can optionally obtain a root shell using **sudo -s**.</span></span>

* <span data-ttu-id="bc5d3-116">Veja [Usando privilégios de raiz em máquinas virtuais Linux do Azure](use-root-privileges.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="bc5d3-116">See [Using root privileges on Linux virtual machines in Azure](use-root-privileges.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="firewall-configuration"></a><span data-ttu-id="bc5d3-117">Configuração do firewall</span><span class="sxs-lookup"><span data-stu-id="bc5d3-117">Firewall Configuration</span></span>
<span data-ttu-id="bc5d3-118">O Azure fornece um filtro de pacote de entrada que restringe a conectividade tooports especificado no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="bc5d3-118">Azure provides an inbound packet filter that restricts connectivity tooports specified in hello Azure portal.</span></span> <span data-ttu-id="bc5d3-119">Por padrão, hello apenas porta permitido é SSH.</span><span class="sxs-lookup"><span data-stu-id="bc5d3-119">By default, hello only allowed port is SSH.</span></span> <span data-ttu-id="bc5d3-120">Você pode abrir as portas do acesso tooadditional na máquina virtual Linux Configurando pontos de extremidade no hello portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="bc5d3-120">You may open up access tooadditional ports on your Linux virtual machine by configuring endpoints in hello Azure portal:</span></span>

* <span data-ttu-id="bc5d3-121">Consulte: [como pontos de extremidade de tooSet tooa Máquina Virtual](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="bc5d3-121">See: [How tooSet Up Endpoints tooa Virtual Machine](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="bc5d3-122">imagens Linux Olá Olá Galeria do Azure não habilitam Olá *iptables* firewall por padrão.</span><span class="sxs-lookup"><span data-stu-id="bc5d3-122">hello Linux images in hello Azure Gallery do not enable hello *iptables* firewall by default.</span></span> <span data-ttu-id="bc5d3-123">Se desejar, pode ser configurado firewall Olá tooprovide de filtragem adicionais.</span><span class="sxs-lookup"><span data-stu-id="bc5d3-123">If desired, hello firewall may be configured tooprovide additional filtering.</span></span>

## <a name="hostname-changes"></a><span data-ttu-id="bc5d3-124">Alterações de nome do host</span><span class="sxs-lookup"><span data-stu-id="bc5d3-124">Hostname Changes</span></span>
<span data-ttu-id="bc5d3-125">Quando você implanta inicialmente uma instância de uma imagem do Linux, será necessário tooprovide um nome de host para a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="bc5d3-125">When you initially deploy an instance of a Linux image, you are required tooprovide a host name for hello virtual machine.</span></span> <span data-ttu-id="bc5d3-126">Depois de máquina virtual de saudação estiver em execução, o nome do host é publicado toohello servidores DNS de plataforma para que vários tooeach máquinas virtuais conectadas outros possa executar pesquisas de endereço IP usando nomes de host.</span><span class="sxs-lookup"><span data-stu-id="bc5d3-126">Once hello virtual machine is running, this hostname is published toohello platform DNS servers so that multiple virtual machines connected tooeach other can perform IP address lookups using hostnames.</span></span>

<span data-ttu-id="bc5d3-127">Se as alterações de nome de host são desejadas após a implantação de uma máquina virtual, use o comando de saudação</span><span class="sxs-lookup"><span data-stu-id="bc5d3-127">If hostname changes are desired after a virtual machine has been deployed, please use hello command</span></span>

    # sudo hostname <newname>

<span data-ttu-id="bc5d3-128">Olá agente Linux do Azure inclui a funcionalidade de tooautomatically detectar essa alteração de nome adequadamente configurar Olá máquina virtual toopersist essa alteração e publicar essa alteração os servidores DNS toohello plataforma.</span><span class="sxs-lookup"><span data-stu-id="bc5d3-128">hello Azure Linux Agent includes functionality tooautomatically detect this name change and appropriately configure hello virtual machine toopersist this change and publish this change toohello platform DNS servers.</span></span>

* [<span data-ttu-id="bc5d3-129">Guia do usuário do agente Linux para o Azure</span><span class="sxs-lookup"><span data-stu-id="bc5d3-129">Azure Linux Agent User Guide</span></span>](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="cloud-init"></a><span data-ttu-id="bc5d3-130">Inicialização de nuvem</span><span class="sxs-lookup"><span data-stu-id="bc5d3-130">Cloud-Init</span></span>
<span data-ttu-id="bc5d3-131">As imagens do **Ubuntu** e **CoreOS** utilizam inicialização de nuvem no Azure, que fornece recursos adicionais para inicializar uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bc5d3-131">**Ubuntu** and **CoreOS** images utilize cloud-init on Azure, which provides additional capabilities for bootstrapping a virtual machine.</span></span>

* [<span data-ttu-id="bc5d3-132">Como tooInject de dados personalizado</span><span class="sxs-lookup"><span data-stu-id="bc5d3-132">How tooInject Custom Data</span></span>](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="bc5d3-133">Dados personalizados e inicialização de nuvem no Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="bc5d3-133">Custom Data and Cloud-Init on Microsoft Azure</span></span>](https://azure.microsoft.com/blog/2014/04/21/custom-data-and-cloud-init-on-windows-azure/)
* [<span data-ttu-id="bc5d3-134">Criar partições de troca do Azure usando a nuvem Init</span><span class="sxs-lookup"><span data-stu-id="bc5d3-134">Create Azure Swap Partitions Using Cloud-Init</span></span>](https://wiki.ubuntu.com/AzureSwapPartitions)
* [<span data-ttu-id="bc5d3-135">Como tooUse CoreOS no Azure</span><span class="sxs-lookup"><span data-stu-id="bc5d3-135">How tooUse CoreOS on Azure</span></span>](https://coreos.com/os/docs/latest/booting-on-azure.html)

## <a name="virtual-machine-image-capture"></a><span data-ttu-id="bc5d3-136">Captura de imagem da máquina virtual</span><span class="sxs-lookup"><span data-stu-id="bc5d3-136">Virtual Machine Image Capture</span></span>
<span data-ttu-id="bc5d3-137">O Azure fornece o estado de saudação do hello capacidade toocapture de uma máquina virtual existente em uma imagem que posteriormente pode ser usado toodeploy instâncias de máquina virtual adicional.</span><span class="sxs-lookup"><span data-stu-id="bc5d3-137">Azure provides hello ability toocapture hello state of an existing virtual machine into an image that can subsequently be used toodeploy additional virtual machine instances.</span></span> <span data-ttu-id="bc5d3-138">Olá agente Linux do Azure pode ser usado toorollback alguns Olá personalização que foi executada durante o processo de provisionamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="bc5d3-138">hello Azure Linux Agent may be used toorollback some of hello customization that was performed during hello provisioning process.</span></span> <span data-ttu-id="bc5d3-139">Você pode seguir as próximas etapas, Olá toocapture uma máquina virtual como uma imagem:</span><span class="sxs-lookup"><span data-stu-id="bc5d3-139">You may follow hello steps below toocapture a virtual machine as an image:</span></span>

1. <span data-ttu-id="bc5d3-140">Executar **waagent-deprovision** tooundo provisionamento personalização.</span><span class="sxs-lookup"><span data-stu-id="bc5d3-140">Run **waagent -deprovision** tooundo provisioning customization.</span></span> <span data-ttu-id="bc5d3-141">Ou **waagent-deprovision + user** toooptionally excluir conta de usuário de saudação especificada durante o provisionamento e todos os respectivos dados.</span><span class="sxs-lookup"><span data-stu-id="bc5d3-141">Or **waagent -deprovision+user** toooptionally delete hello user account specified during provisioning and all associated data.</span></span>
2. <span data-ttu-id="bc5d3-142">Desligado para baixo/desligar a máquina de virtual hello.</span><span class="sxs-lookup"><span data-stu-id="bc5d3-142">Shut down/power off hello virtual machine.</span></span>
3. <span data-ttu-id="bc5d3-143">Clique em **capturar** em hello Azure Olá portal ou use PowerShell ou CLI ferramentas toocapture Olá VM como uma imagem.</span><span class="sxs-lookup"><span data-stu-id="bc5d3-143">Click **Capture** in hello Azure portal or use hello PowerShell or CLI tools toocapture hello virtual machine as an image.</span></span>
   
   * <span data-ttu-id="bc5d3-144">Consulte: [como tooCapture tooUse uma máquina Virtual Linux como um modelo](classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="bc5d3-144">See: [How tooCapture a Linux Virtual Machine tooUse as a Template](classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

## <a name="attaching-disks"></a><span data-ttu-id="bc5d3-145">Anexando discos</span><span class="sxs-lookup"><span data-stu-id="bc5d3-145">Attaching Disks</span></span>
<span data-ttu-id="bc5d3-146">Cada máquina virtual tem um *disco de recursos* anexado.</span><span class="sxs-lookup"><span data-stu-id="bc5d3-146">Each virtual machine has a temporary, local *resource disk* attached.</span></span> <span data-ttu-id="bc5d3-147">Porque os dados em um disco de recurso não podem ser duráveis entre as reinicializações, geralmente é usado por aplicativos e processos em execução na máquina virtual Olá transitório e **temporário** armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="bc5d3-147">Because data on a resource disk may not be durable across reboots, it is often used by applications and processes running in hello virtual machine for transient and **temporary** storage of data.</span></span> <span data-ttu-id="bc5d3-148">Também é usado toostore Olá página ou permuta arquivos Olá sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="bc5d3-148">It is also used toostore hello page or swap files for hello operating system.</span></span>

<span data-ttu-id="bc5d3-149">No Linux, disco de recurso de saudação é normalmente gerenciado pelo Olá agente Linux do Azure e montado automaticamente muito**/mnt/Retention/ recurso** (ou **/mnt** no Ubuntu imagens).</span><span class="sxs-lookup"><span data-stu-id="bc5d3-149">On Linux, hello resource disk is typically managed by hello Azure Linux Agent and automatically mounted too**/mnt/resource** (or **/mnt** on Ubuntu images).</span></span>

> [!NOTE]
> <span data-ttu-id="bc5d3-150">Observe que esse disco de recurso Olá é um **temporário** disco e pode ser excluído e reformatado quando hello VM é reiniciada.</span><span class="sxs-lookup"><span data-stu-id="bc5d3-150">Note that hello resource disk is a **temporary** disk, and might be deleted and reformatted when hello VM is rebooted.</span></span>
> 
> 

<span data-ttu-id="bc5d3-151">Disco de dados Olá no Linux pode ser chamado pelo kernel hello como `/dev/sdc`, e os usuários precisarão toopartition, formatar e montar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="bc5d3-151">On Linux hello data disk might be named by hello kernel as `/dev/sdc`, and users will need toopartition, format and mount that resource.</span></span> <span data-ttu-id="bc5d3-152">Isso é abordado passo a passo no tutorial Olá: [como tooAttach uma máquina Virtual de tooa do disco de dados](../windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bc5d3-152">This is covered step-by-step in hello tutorial: [How tooAttach a Data Disk tooa Virtual Machine](../windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

* <span data-ttu-id="bc5d3-153">**Veja também:** [Configurar o Software RAID no Linux](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) & [Configurar LVM em uma VM do Linux no Azure](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="bc5d3-153">**See also:** [Configure Software RAID on Linux](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) & [Configure LVM on a Linux VM in Azure](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

