---
title: tooFreeBSD aaaIntroduction no Azure | Microsoft Docs
description: "Saiba como usar máquinas virtuais FreeBSD no Azure"
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 32b87a5f-d024-4da0-8bf0-77e233d1422b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: kyliel
ms.openlocfilehash: 43ba7a70ed21e7fb8b331f4a26db0426e098c4aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toofreebsd-on-azure"></a><span data-ttu-id="cc409-103">Introdução tooFreeBSD no Azure</span><span class="sxs-lookup"><span data-stu-id="cc409-103">Introduction tooFreeBSD on Azure</span></span>
<span data-ttu-id="cc409-104">Este tópico fornece uma visão geral da execução da máquina virtual FreeBSD no Azure.</span><span class="sxs-lookup"><span data-stu-id="cc409-104">This topic provides an overview of running a FreeBSD virtual machine in Azure.</span></span>

## <a name="overview"></a><span data-ttu-id="cc409-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="cc409-105">Overview</span></span>
<span data-ttu-id="cc409-106">FreeBSD do Microsoft Azure é que um sistema operacional de computador avançado usado plataformas incorporadas, áreas de trabalho e servidores modernos toopower.</span><span class="sxs-lookup"><span data-stu-id="cc409-106">FreeBSD for Microsoft Azure is an advanced computer operating system used toopower modern servers, desktops, and embedded platforms.</span></span>

<span data-ttu-id="cc409-107">Microsoft Corporation está disponibilizando imagens de FreeBSD no Azure com hello [agente convidado da VM do Azure](https://github.com/Azure/WALinuxAgent/) pré-configurado.</span><span class="sxs-lookup"><span data-stu-id="cc409-107">Microsoft Corporation is making images of FreeBSD available on Azure with hello [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) pre-configured.</span></span> <span data-ttu-id="cc409-108">Atualmente, hello FreeBSD versões a seguir são oferecidas como imagens pela Microsoft:</span><span class="sxs-lookup"><span data-stu-id="cc409-108">Currently, hello following FreeBSD versions are offered as images by Microsoft:</span></span>

- <span data-ttu-id="cc409-109">FreeBSD 10.3-RELEASE</span><span class="sxs-lookup"><span data-stu-id="cc409-109">FreeBSD 10.3-RELEASE</span></span>
- <span data-ttu-id="cc409-110">FreeBSD 11.0-RELEASE</span><span class="sxs-lookup"><span data-stu-id="cc409-110">FreeBSD 11.0-RELEASE</span></span>

<span data-ttu-id="cc409-111">agente Olá é responsável pela comunicação entre hello FreeBSD VM e Olá malha do Azure para operações como provisionamento Olá VM no primeiro uso (nome de usuário, senha ou chave SSH, nome de host, etc.) e a funcionalidade de habilitação para extensões VM seletivas.</span><span class="sxs-lookup"><span data-stu-id="cc409-111">hello agent is responsible for communication between hello FreeBSD VM and hello Azure fabric for operations such as provisioning hello VM on first use (user name, password or SSH key, host name, etc.) and enabling functionality for selective VM extensions.</span></span>

<span data-ttu-id="cc409-112">Para versões futuras do FreeBSD, estratégia Olá é toostay atual e disponibilize Olá versões mais recentes logo depois que forem publicados pela equipe de engenharia Olá FreeBSD versão.</span><span class="sxs-lookup"><span data-stu-id="cc409-112">As for future versions of FreeBSD, hello strategy is toostay current and make hello latest releases available shortly after they are published by hello FreeBSD release engineering team.</span></span>

## <a name="deploying-a-freebsd-virtual-machine"></a><span data-ttu-id="cc409-113">Implantando uma máquina virtual FreeBSD</span><span class="sxs-lookup"><span data-stu-id="cc409-113">Deploying a FreeBSD virtual machine</span></span>
<span data-ttu-id="cc409-114">Implantar uma máquina virtual de FreeBSD é um processo simples usando uma imagem de saudação do Azure Marketplace de saudação portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="cc409-114">Deploying a FreeBSD virtual machine is a straightforward process using an image from hello Azure Marketplace from hello Azure portal:</span></span>

- [<span data-ttu-id="cc409-115">10.3 FreeBSD em hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="cc409-115">FreeBSD 10.3 on hello Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd103/)
- [<span data-ttu-id="cc409-116">11.0 FreeBSD em hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="cc409-116">FreeBSD 11.0 on hello Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/)

### <a name="create-a-freebsd-vm-through-azure-cli-20-on-freebsd"></a><span data-ttu-id="cc409-117">Criar uma VM do FreeBSD por meio da CLI do Azure 2.0 no FreeBSD</span><span class="sxs-lookup"><span data-stu-id="cc409-117">Create a FreeBSD VM through Azure CLI 2.0 on FreeBSD</span></span>
<span data-ttu-id="cc409-118">Primeiro é necessário tooinstall [2.0 do CLI do Azure](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) Embora o comando a seguir em um computador FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="cc409-118">First you need tooinstall [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) though following command on a FreeBSD machine.</span></span>

```bash 
curl -L https://aka.ms/InstallAzureCli | bash
```

<span data-ttu-id="cc409-119">Se bash não estiver instalado no seu computador FreeBSD, execute o seguinte comando antes da instalação de saudação.</span><span class="sxs-lookup"><span data-stu-id="cc409-119">If bash is not installed on your FreeBSD machine, run following command before hello installation.</span></span> 

```bash
sudo pkg install bash
```

<span data-ttu-id="cc409-120">Se o python não estiver instalado no seu computador FreeBSD, execute o seguinte comandos antes da instalação de saudação.</span><span class="sxs-lookup"><span data-stu-id="cc409-120">If python is not installed on your FreeBSD machine, run following commands before hello installation.</span></span> 

```bash
sudo pkg install python35
cd /usr/local/bin 
sudo rm /usr/local/bin/python 
sudo ln -s /usr/local/bin/python3.5 /usr/local/bin/python
```

<span data-ttu-id="cc409-121">Durante a instalação do hello, você será solicitado `Modify profile tooupdate your $PATH and enable shell/tab completion now? (Y/n)`.</span><span class="sxs-lookup"><span data-stu-id="cc409-121">During hello installation, you are asked `Modify profile tooupdate your $PATH and enable shell/tab completion now? (Y/n)`.</span></span> <span data-ttu-id="cc409-122">Se você responder `y` e digite `/etc/rc.conf` como `a path tooan rc file tooupdate`, você poderá atender problema Olá `ERROR: [Errno 13] Permission denied`.</span><span class="sxs-lookup"><span data-stu-id="cc409-122">If you answer `y` and enter `/etc/rc.conf` as `a path tooan rc file tooupdate`, you may meet hello problem `ERROR: [Errno 13] Permission denied`.</span></span> <span data-ttu-id="cc409-123">tooresolve esse problema, você deve conceder o direito toocurrent usuário gravação Olá arquivo hello `etc/rc.conf`.</span><span class="sxs-lookup"><span data-stu-id="cc409-123">tooresolve this problem, you should grant hello write right toocurrent user against hello file `etc/rc.conf`.</span></span>

<span data-ttu-id="cc409-124">Agora você pode fazer logon no Azure e criar sua VM do FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="cc409-124">Now you can log in Azure and create your FreeBSD VM.</span></span> <span data-ttu-id="cc409-125">Abaixo está um exemplo toocreate uma VM do FreeBSD 11.0.</span><span class="sxs-lookup"><span data-stu-id="cc409-125">Below is an example toocreate a FreeBSD 11.0 VM.</span></span> <span data-ttu-id="cc409-126">Você também pode adicionar o parâmetro hello `--public-ip-address-dns-name` com o nome DNS exclusivo para um IP público recém-criado.</span><span class="sxs-lookup"><span data-stu-id="cc409-126">You can also add hello parameter `--public-ip-address-dns-name` with a globally unique DNS name for a newly created Public IP.</span></span> 

```azurecli
az login 
az group create --name myResourceGroup --location eastus
az vm create --name myFreeBSD11 \
    --resource-group myResourceGroup \
    --image MicrosoftOSTC:FreeBSD:11.0:latest \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="cc409-127">Em seguida, você pode fazer logon no tooyour FreeBSD VM pelo endereço de ip de saudação impresso na saída de saudação do acima de implantação.</span><span class="sxs-lookup"><span data-stu-id="cc409-127">Then you can log in tooyour FreeBSD VM through hello ip address that printed in hello output of above deployment.</span></span> 

```bash
ssh azureuser@xx.xx.xx.xx -i /etc/ssh/ssh_host_rsa_key
```   

## <a name="vm-extensions-for-freebsd"></a><span data-ttu-id="cc409-128">Extensões de VM para FreeBSD</span><span class="sxs-lookup"><span data-stu-id="cc409-128">VM extensions for FreeBSD</span></span>
<span data-ttu-id="cc409-129">Os itens a seguir têm suporte de extensões de VM no FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="cc409-129">Following are supported VM extensions in FreeBSD.</span></span>

### <a name="vmaccess"></a><span data-ttu-id="cc409-130">VMAccess</span><span class="sxs-lookup"><span data-stu-id="cc409-130">VMAccess</span></span>
<span data-ttu-id="cc409-131">Olá [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) extensão pode:</span><span class="sxs-lookup"><span data-stu-id="cc409-131">hello [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) extension can:</span></span>

* <span data-ttu-id="cc409-132">Redefina a senha de saudação do usuário original de sudo hello.</span><span class="sxs-lookup"><span data-stu-id="cc409-132">Reset hello password of hello original sudo user.</span></span>
* <span data-ttu-id="cc409-133">Crie um novo usuário sudo com senha Olá especificada.</span><span class="sxs-lookup"><span data-stu-id="cc409-133">Create a new sudo user with hello password specified.</span></span>
* <span data-ttu-id="cc409-134">Defina a chave de host público Olá com chave Olá fornecido.</span><span class="sxs-lookup"><span data-stu-id="cc409-134">Set hello public host key with hello key given.</span></span>
* <span data-ttu-id="cc409-135">Redefina a chave de host público de saudação fornecido durante o provisionamento se não for fornecido a chave de saudação do host de VM.</span><span class="sxs-lookup"><span data-stu-id="cc409-135">Reset hello public host key provided during VM provisioning if hello host key is not provided.</span></span>
* <span data-ttu-id="cc409-136">Abra a porta SSH de saudação (22) e restauração Olá sshd_config se reset_ssh for definido tootrue.</span><span class="sxs-lookup"><span data-stu-id="cc409-136">Open hello SSH port (22) and restore hello sshd_config if reset_ssh is set tootrue.</span></span>
* <span data-ttu-id="cc409-137">Remova usuário existente hello.</span><span class="sxs-lookup"><span data-stu-id="cc409-137">Remove hello existing user.</span></span>
* <span data-ttu-id="cc409-138">Verificar os discos.</span><span class="sxs-lookup"><span data-stu-id="cc409-138">Check disks.</span></span>
* <span data-ttu-id="cc409-139">Reparar o disco adicionado.</span><span class="sxs-lookup"><span data-stu-id="cc409-139">Repair an added disk.</span></span>

### <a name="customscript"></a><span data-ttu-id="cc409-140">CustomScript</span><span class="sxs-lookup"><span data-stu-id="cc409-140">CustomScript</span></span>
<span data-ttu-id="cc409-141">Olá [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) extensão pode:</span><span class="sxs-lookup"><span data-stu-id="cc409-141">hello [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) extension can:</span></span>

* <span data-ttu-id="cc409-142">Se fornecido, baixe scripts personalizada de saudação do armazenamento do Azure ou armazenamento público externo (por exemplo, GitHub).</span><span class="sxs-lookup"><span data-stu-id="cc409-142">If provided, download hello customized scripts from Azure Storage or external public storage (for example, GitHub).</span></span>
* <span data-ttu-id="cc409-143">Execute o script de ponto de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="cc409-143">Run hello entry point script.</span></span>
* <span data-ttu-id="cc409-144">Oferecer suporte ao comando embutido.</span><span class="sxs-lookup"><span data-stu-id="cc409-144">Support inline commands.</span></span>
* <span data-ttu-id="cc409-145">Converter automaticamente o estilo newline do Windows em scripts de Shell e Python.</span><span class="sxs-lookup"><span data-stu-id="cc409-145">Convert Windows-style newline in shell and Python scripts automatically.</span></span>
* <span data-ttu-id="cc409-146">Remover automaticamente BOM em scripts de Shell e Python.</span><span class="sxs-lookup"><span data-stu-id="cc409-146">Remove BOM in shell and Python scripts automatically.</span></span>
* <span data-ttu-id="cc409-147">Proteger dados confidenciais em CommandToExecute.</span><span class="sxs-lookup"><span data-stu-id="cc409-147">Protect sensitive data in CommandToExecute.</span></span>

> [!NOTE]
> <span data-ttu-id="cc409-148">A VM do FreeBSD só oferece suporte ao CustomScript versão 1. x até o momento.</span><span class="sxs-lookup"><span data-stu-id="cc409-148">FreeBSD VM only supports CustomScript version 1.x by now.</span></span>  

## <a name="authentication-user-names-passwords-and-ssh-keys"></a><span data-ttu-id="cc409-149">Autenticação: nomes de usuário, senhas e chaves SSH</span><span class="sxs-lookup"><span data-stu-id="cc409-149">Authentication: user names, passwords, and SSH keys</span></span>
<span data-ttu-id="cc409-150">Quando você estiver criando uma máquina virtual de FreeBSD usando Olá portal do Azure, você deve fornecer um nome de usuário, senha ou chave pública SSH.</span><span class="sxs-lookup"><span data-stu-id="cc409-150">When you're creating a FreeBSD virtual machine by using hello Azure portal, you must provide a user name, password, or SSH public key.</span></span>
<span data-ttu-id="cc409-151">Nomes de usuário para implantar uma máquina virtual de FreeBSD no Azure não devem corresponder aos nomes das contas do sistema (UID < 100) já está presente na máquina virtual de saudação ("raiz", por exemplo).</span><span class="sxs-lookup"><span data-stu-id="cc409-151">User names for deploying a FreeBSD virtual machine on Azure must not match names of system accounts (UID <100) already present in hello virtual machine ("root", for example).</span></span>
<span data-ttu-id="cc409-152">Atualmente, há suporte para apenas Olá RSA chave SSH.</span><span class="sxs-lookup"><span data-stu-id="cc409-152">Currently, only hello RSA SSH key is supported.</span></span> <span data-ttu-id="cc409-153">Uma chave SSH multilinha deve começar com `---- BEGIN SSH2 PUBLIC KEY ----` e terminar com `---- END SSH2 PUBLIC KEY ----`.</span><span class="sxs-lookup"><span data-stu-id="cc409-153">A multiline SSH key must begin with `---- BEGIN SSH2 PUBLIC KEY ----` and end with `---- END SSH2 PUBLIC KEY ----`.</span></span>

## <a name="obtaining-superuser-privileges"></a><span data-ttu-id="cc409-154">Obtendo privilégios de superusuário</span><span class="sxs-lookup"><span data-stu-id="cc409-154">Obtaining superuser privileges</span></span>
<span data-ttu-id="cc409-155">conta de usuário de saudação que é especificada durante a implantação de instância de máquina virtual no Azure é uma conta privilegiada.</span><span class="sxs-lookup"><span data-stu-id="cc409-155">hello user account that is specified during virtual machine instance deployment on Azure is a privileged account.</span></span> <span data-ttu-id="cc409-156">Olá pacote do sudo foi instalado no hello publicado FreeBSD imagem.</span><span class="sxs-lookup"><span data-stu-id="cc409-156">hello package of sudo was installed in hello published FreeBSD image.</span></span>
<span data-ttu-id="cc409-157">Depois que você está conectado a esta conta de usuário, você pode executar comandos como raiz usando a sintaxe do comando hello.</span><span class="sxs-lookup"><span data-stu-id="cc409-157">After you're logged in through this user account, you can run commands as root by using hello command syntax.</span></span>

```
$ sudo <COMMAND>
```

<span data-ttu-id="cc409-158">Opcionalmente, é possível obter um shell root usando `sudo -s`.</span><span class="sxs-lookup"><span data-stu-id="cc409-158">You can optionally obtain a root shell by using `sudo -s`.</span></span>

## <a name="known-issues"></a><span data-ttu-id="cc409-159">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="cc409-159">Known issues</span></span>
<span data-ttu-id="cc409-160">Olá [agente convidado da VM do Azure](https://github.com/Azure/WALinuxAgent/) versão 2.2.2 tem um [problema conhecido] (https://github.com/Azure/WALinuxAgent/pull/517) que causa falha de provisionamento de saudação para FreeBSD VM no Azure.</span><span class="sxs-lookup"><span data-stu-id="cc409-160">hello [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.2 has a [known issue] (https://github.com/Azure/WALinuxAgent/pull/517) that causes hello provision failure for FreeBSD VM on Azure.</span></span> <span data-ttu-id="cc409-161">Olá correção foi capturada por [agente convidado da VM do Azure](https://github.com/Azure/WALinuxAgent/) versão 2.2.3 e versões posteriores.</span><span class="sxs-lookup"><span data-stu-id="cc409-161">hello fix was captured by [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.3 and later releases.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="cc409-162">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cc409-162">Next steps</span></span>
* <span data-ttu-id="cc409-163">Vá muito[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) toocreate uma VM FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="cc409-163">Go too[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) toocreate a FreeBSD VM.</span></span>
* <span data-ttu-id="cc409-164">Se você quiser toobring seu próprios tooAzure FreeBSD, consulte muito[criar e carregar um VHD FreeBSD tooAzure](classic/freebsd-create-upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="cc409-164">If you want toobring your own FreeBSD tooAzure, refer too[Create and upload a FreeBSD VHD tooAzure](classic/freebsd-create-upload-vhd.md).</span></span>
