---
title: "Introdução ao FreeBSD no Azure | Microsoft Docs"
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
ms.openlocfilehash: 7ada9fddd7ffccc3dcbfe3eac05d99b710b67cbc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="introduction-to-freebsd-on-azure"></a><span data-ttu-id="70827-103">Introdução ao FreeBSD no Azure</span><span class="sxs-lookup"><span data-stu-id="70827-103">Introduction to FreeBSD on Azure</span></span>
<span data-ttu-id="70827-104">Este tópico fornece uma visão geral da execução da máquina virtual FreeBSD no Azure.</span><span class="sxs-lookup"><span data-stu-id="70827-104">This topic provides an overview of running a FreeBSD virtual machine in Azure.</span></span>

## <a name="overview"></a><span data-ttu-id="70827-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="70827-105">Overview</span></span>
<span data-ttu-id="70827-106">O FreeBSD para Microsoft Azure é um sistema operacional avançado usado para capacitar servidores modernos, desktops e plataformas incorporadas.</span><span class="sxs-lookup"><span data-stu-id="70827-106">FreeBSD for Microsoft Azure is an advanced computer operating system used to power modern servers, desktops, and embedded platforms.</span></span>

<span data-ttu-id="70827-107">A Microsoft Corporation está disponibilizando imagens do FreeBSD no Azure com o [Agente convidado da VM Azure](https://github.com/Azure/WALinuxAgent/) pré-configurado.</span><span class="sxs-lookup"><span data-stu-id="70827-107">Microsoft Corporation is making images of FreeBSD available on Azure with the [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) pre-configured.</span></span> <span data-ttu-id="70827-108">No momento, as seguintes versões do FreeBSD são oferecidas como imagens pela Microsoft:</span><span class="sxs-lookup"><span data-stu-id="70827-108">Currently, the following FreeBSD versions are offered as images by Microsoft:</span></span>

- <span data-ttu-id="70827-109">FreeBSD 10.3-RELEASE</span><span class="sxs-lookup"><span data-stu-id="70827-109">FreeBSD 10.3-RELEASE</span></span>
- <span data-ttu-id="70827-110">FreeBSD 11.0-RELEASE</span><span class="sxs-lookup"><span data-stu-id="70827-110">FreeBSD 11.0-RELEASE</span></span>

<span data-ttu-id="70827-111">O agente é responsável pela comunicação entre a VM do FreeBSD e a malha do Azure para operações como provisionamento da VM no primeiro uso (nome de usuário, senha, chave SSH, nome do host, etc.) e habilitação da funcionalidade para extensões de VM seletivas.</span><span class="sxs-lookup"><span data-stu-id="70827-111">The agent is responsible for communication between the FreeBSD VM and the Azure fabric for operations such as provisioning the VM on first use (user name, password or SSH key, host name, etc.) and enabling functionality for selective VM extensions.</span></span>

<span data-ttu-id="70827-112">Para versões futuras do FreeBSD, a estratégia é manter-se atualizado e disponibilizar as versões mais recentes logo após a publicação pela equipe de engenharia de versão do FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="70827-112">As for future versions of FreeBSD, the strategy is to stay current and make the latest releases available shortly after they are published by the FreeBSD release engineering team.</span></span>

## <a name="deploying-a-freebsd-virtual-machine"></a><span data-ttu-id="70827-113">Implantando uma máquina virtual FreeBSD</span><span class="sxs-lookup"><span data-stu-id="70827-113">Deploying a FreeBSD virtual machine</span></span>
<span data-ttu-id="70827-114">A implantação de uma máquina virtual do FreeBSD é um processo simples que usa uma imagem do Azure Marketplace do Portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="70827-114">Deploying a FreeBSD virtual machine is a straightforward process using an image from the Azure Marketplace from the Azure portal:</span></span>

- [<span data-ttu-id="70827-115">FreeBSD 10.3 no Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="70827-115">FreeBSD 10.3 on the Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd103/)
- [<span data-ttu-id="70827-116">FreeBSD 11.0 no Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="70827-116">FreeBSD 11.0 on the Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/)

### <a name="create-a-freebsd-vm-through-azure-cli-20-on-freebsd"></a><span data-ttu-id="70827-117">Criar uma VM do FreeBSD por meio da CLI do Azure 2.0 no FreeBSD</span><span class="sxs-lookup"><span data-stu-id="70827-117">Create a FreeBSD VM through Azure CLI 2.0 on FreeBSD</span></span>
<span data-ttu-id="70827-118">Primeiro, você precisa instalar a [CLI do Azure 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) seguindo os comandos em um computador FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="70827-118">First you need to install [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) though following command on a FreeBSD machine.</span></span>

```bash 
curl -L https://aka.ms/InstallAzureCli | bash
```

<span data-ttu-id="70827-119">Se o bash não estiver instalado no seu computador FreeBSD, execute o comando a seguir antes da instalação.</span><span class="sxs-lookup"><span data-stu-id="70827-119">If bash is not installed on your FreeBSD machine, run following command before the installation.</span></span> 

```bash
sudo pkg install bash
```

<span data-ttu-id="70827-120">Se o Python não estiver instalado no seu computador FreeBSD, execute o comando a seguir antes da instalação.</span><span class="sxs-lookup"><span data-stu-id="70827-120">If python is not installed on your FreeBSD machine, run following commands before the installation.</span></span> 

```bash
sudo pkg install python35
cd /usr/local/bin 
sudo rm /usr/local/bin/python 
sudo ln -s /usr/local/bin/python3.5 /usr/local/bin/python
```

<span data-ttu-id="70827-121">Durante a instalação, `Modify profile to update your $PATH and enable shell/tab completion now? (Y/n)` será solicitado.</span><span class="sxs-lookup"><span data-stu-id="70827-121">During the installation, you are asked `Modify profile to update your $PATH and enable shell/tab completion now? (Y/n)`.</span></span> <span data-ttu-id="70827-122">Se responder `y` e inserir `/etc/rc.conf` como `a path to an rc file to update`, você poderá encontrar o problema `ERROR: [Errno 13] Permission denied`.</span><span class="sxs-lookup"><span data-stu-id="70827-122">If you answer `y` and enter `/etc/rc.conf` as `a path to an rc file to update`, you may meet the problem `ERROR: [Errno 13] Permission denied`.</span></span> <span data-ttu-id="70827-123">Para resolvê-lo, você deve conceder o direito de gravação ao usuário atual sobre o arquivo `etc/rc.conf`.</span><span class="sxs-lookup"><span data-stu-id="70827-123">To resolve this problem, you should grant the write right to current user against the file `etc/rc.conf`.</span></span>

<span data-ttu-id="70827-124">Agora você pode fazer logon no Azure e criar sua VM do FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="70827-124">Now you can log in Azure and create your FreeBSD VM.</span></span> <span data-ttu-id="70827-125">Abaixo está um exemplo de como criar uma VM do FreeBSD 11.0.</span><span class="sxs-lookup"><span data-stu-id="70827-125">Below is an example to create a FreeBSD 11.0 VM.</span></span> <span data-ttu-id="70827-126">Você também pode adicionar o parâmetro `--public-ip-address-dns-name` com um nome DNS exclusivo para um IP público recém-criado.</span><span class="sxs-lookup"><span data-stu-id="70827-126">You can also add the parameter `--public-ip-address-dns-name` with a globally unique DNS name for a newly created Public IP.</span></span> 

```azurecli
az login 
az group create --name myResourceGroup --location eastus
az vm create --name myFreeBSD11 \
    --resource-group myResourceGroup \
    --image MicrosoftOSTC:FreeBSD:11.0:latest \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="70827-127">Em seguida, você pode fazer logon em sua VM do FreeBSD pelo endereço IP impresso na saída acima da implantação.</span><span class="sxs-lookup"><span data-stu-id="70827-127">Then you can log in to your FreeBSD VM through the ip address that printed in the output of above deployment.</span></span> 

```bash
ssh azureuser@xx.xx.xx.xx -i /etc/ssh/ssh_host_rsa_key
```   

## <a name="vm-extensions-for-freebsd"></a><span data-ttu-id="70827-128">Extensões de VM para FreeBSD</span><span class="sxs-lookup"><span data-stu-id="70827-128">VM extensions for FreeBSD</span></span>
<span data-ttu-id="70827-129">Os itens a seguir têm suporte de extensões de VM no FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="70827-129">Following are supported VM extensions in FreeBSD.</span></span>

### <a name="vmaccess"></a><span data-ttu-id="70827-130">VMAccess</span><span class="sxs-lookup"><span data-stu-id="70827-130">VMAccess</span></span>
<span data-ttu-id="70827-131">A extensão [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) pode:</span><span class="sxs-lookup"><span data-stu-id="70827-131">The [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) extension can:</span></span>

* <span data-ttu-id="70827-132">Redefinir a senha do usuário sudo original.</span><span class="sxs-lookup"><span data-stu-id="70827-132">Reset the password of the original sudo user.</span></span>
* <span data-ttu-id="70827-133">Criar um novo usuário sudo com a senha especificada.</span><span class="sxs-lookup"><span data-stu-id="70827-133">Create a new sudo user with the password specified.</span></span>
* <span data-ttu-id="70827-134">Definir a chave pública do host com a chave fornecida.</span><span class="sxs-lookup"><span data-stu-id="70827-134">Set the public host key with the key given.</span></span>
* <span data-ttu-id="70827-135">Redefinir a chave pública do host fornecida durante o provisionamento da VM se a chave do host não for fornecida.</span><span class="sxs-lookup"><span data-stu-id="70827-135">Reset the public host key provided during VM provisioning if the host key is not provided.</span></span>
* <span data-ttu-id="70827-136">Abrir a porta (22) SSH e restaurar o sshd_config se reset_ssh estiver definido como true.</span><span class="sxs-lookup"><span data-stu-id="70827-136">Open the SSH port (22) and restore the sshd_config if reset_ssh is set to true.</span></span>
* <span data-ttu-id="70827-137">Remover o usuário existente.</span><span class="sxs-lookup"><span data-stu-id="70827-137">Remove the existing user.</span></span>
* <span data-ttu-id="70827-138">Verificar os discos.</span><span class="sxs-lookup"><span data-stu-id="70827-138">Check disks.</span></span>
* <span data-ttu-id="70827-139">Reparar o disco adicionado.</span><span class="sxs-lookup"><span data-stu-id="70827-139">Repair an added disk.</span></span>

### <a name="customscript"></a><span data-ttu-id="70827-140">CustomScript</span><span class="sxs-lookup"><span data-stu-id="70827-140">CustomScript</span></span>
<span data-ttu-id="70827-141">A extensão [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) pode:</span><span class="sxs-lookup"><span data-stu-id="70827-141">The [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) extension can:</span></span>

* <span data-ttu-id="70827-142">Se for fornecida, baixar os scripts personalizados do Armazenamento do Azure ou do armazenamento público externo (por exemplo, GitHub).</span><span class="sxs-lookup"><span data-stu-id="70827-142">If provided, download the customized scripts from Azure Storage or external public storage (for example, GitHub).</span></span>
* <span data-ttu-id="70827-143">Executar o script de ponto de entrada.</span><span class="sxs-lookup"><span data-stu-id="70827-143">Run the entry point script.</span></span>
* <span data-ttu-id="70827-144">Oferecer suporte ao comando embutido.</span><span class="sxs-lookup"><span data-stu-id="70827-144">Support inline commands.</span></span>
* <span data-ttu-id="70827-145">Converter automaticamente o estilo newline do Windows em scripts de Shell e Python.</span><span class="sxs-lookup"><span data-stu-id="70827-145">Convert Windows-style newline in shell and Python scripts automatically.</span></span>
* <span data-ttu-id="70827-146">Remover automaticamente BOM em scripts de Shell e Python.</span><span class="sxs-lookup"><span data-stu-id="70827-146">Remove BOM in shell and Python scripts automatically.</span></span>
* <span data-ttu-id="70827-147">Proteger dados confidenciais em CommandToExecute.</span><span class="sxs-lookup"><span data-stu-id="70827-147">Protect sensitive data in CommandToExecute.</span></span>

> [!NOTE]
> <span data-ttu-id="70827-148">A VM do FreeBSD só oferece suporte ao CustomScript versão 1. x até o momento.</span><span class="sxs-lookup"><span data-stu-id="70827-148">FreeBSD VM only supports CustomScript version 1.x by now.</span></span>  

## <a name="authentication-user-names-passwords-and-ssh-keys"></a><span data-ttu-id="70827-149">Autenticação: nomes de usuário, senhas e chaves SSH</span><span class="sxs-lookup"><span data-stu-id="70827-149">Authentication: user names, passwords, and SSH keys</span></span>
<span data-ttu-id="70827-150">Ao criar uma máquina virtual FreeBSD usando o Portal do Azure, você deve fornecer um nome de usuário, uma senha ou uma chave pública SSH.</span><span class="sxs-lookup"><span data-stu-id="70827-150">When you're creating a FreeBSD virtual machine by using the Azure portal, you must provide a user name, password, or SSH public key.</span></span>
<span data-ttu-id="70827-151">Os nomes de usuário para implantação de uma máquina virtual do FreeBSD no Azure não devem corresponder aos nomes de contas do sistema (UID <100) já presentes na máquina virtual (“root”, por exemplo).</span><span class="sxs-lookup"><span data-stu-id="70827-151">User names for deploying a FreeBSD virtual machine on Azure must not match names of system accounts (UID <100) already present in the virtual machine ("root", for example).</span></span>
<span data-ttu-id="70827-152">Atualmente, há suporte apenas para a chave RSA SSH.</span><span class="sxs-lookup"><span data-stu-id="70827-152">Currently, only the RSA SSH key is supported.</span></span> <span data-ttu-id="70827-153">Uma chave SSH multilinha deve começar com `---- BEGIN SSH2 PUBLIC KEY ----` e terminar com `---- END SSH2 PUBLIC KEY ----`.</span><span class="sxs-lookup"><span data-stu-id="70827-153">A multiline SSH key must begin with `---- BEGIN SSH2 PUBLIC KEY ----` and end with `---- END SSH2 PUBLIC KEY ----`.</span></span>

## <a name="obtaining-superuser-privileges"></a><span data-ttu-id="70827-154">Obtendo privilégios de superusuário</span><span class="sxs-lookup"><span data-stu-id="70827-154">Obtaining superuser privileges</span></span>
<span data-ttu-id="70827-155">A conta de usuário especificada durante a implantação da instância de máquina virtual no Azure é uma conta privilegiada.</span><span class="sxs-lookup"><span data-stu-id="70827-155">The user account that is specified during virtual machine instance deployment on Azure is a privileged account.</span></span> <span data-ttu-id="70827-156">O pacote do sudo foi instalado na imagem de FreeBSD publicada.</span><span class="sxs-lookup"><span data-stu-id="70827-156">The package of sudo was installed in the published FreeBSD image.</span></span>
<span data-ttu-id="70827-157">Depois de fazer logon usando essa conta de usuário, você poderá executar comandos como raiz usando a sintaxe de comando.</span><span class="sxs-lookup"><span data-stu-id="70827-157">After you're logged in through this user account, you can run commands as root by using the command syntax.</span></span>

```
$ sudo <COMMAND>
```

<span data-ttu-id="70827-158">Opcionalmente, é possível obter um shell root usando `sudo -s`.</span><span class="sxs-lookup"><span data-stu-id="70827-158">You can optionally obtain a root shell by using `sudo -s`.</span></span>

## <a name="known-issues"></a><span data-ttu-id="70827-159">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="70827-159">Known issues</span></span>
<span data-ttu-id="70827-160">O [Agente convidado da VM Azure](https://github.com/Azure/WALinuxAgent/) versão 2.2.2 tem um [problema conhecido] (https://github.com/Azure/WALinuxAgent/pull/517) que causa a falha de provisionamento da VM do FreeBSD no Azure.</span><span class="sxs-lookup"><span data-stu-id="70827-160">The [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.2 has a [known issue] (https://github.com/Azure/WALinuxAgent/pull/517) that causes the provision failure for FreeBSD VM on Azure.</span></span> <span data-ttu-id="70827-161">A correção foi capturada pelo [Agente Convidado da VM do Azure](https://github.com/Azure/WALinuxAgent/) versão 2.2.3 e versões posteriores.</span><span class="sxs-lookup"><span data-stu-id="70827-161">The fix was captured by [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.3 and later releases.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="70827-162">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="70827-162">Next steps</span></span>
* <span data-ttu-id="70827-163">Acesse o [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) para criar uma VM FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="70827-163">Go to [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) to create a FreeBSD VM.</span></span>
* <span data-ttu-id="70827-164">Se você quiser levar seu próprio FreeBSD para o Azure, veja [Criar e carregar um VHD FreeBSD no Azure](classic/freebsd-create-upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="70827-164">If you want to bring your own FreeBSD to Azure, refer to [Create and upload a FreeBSD VHD to Azure](classic/freebsd-create-upload-vhd.md).</span></span>
