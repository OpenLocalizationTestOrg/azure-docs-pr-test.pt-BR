---
title: Mover arquivos de e para VMs Linux do Azure com o SCP | Microsoft Docs
description: "Mova arquivos de e para uma VM Linux no Azure com segurança usando o SCP e um par de chaves SSH."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: danlep
ms.openlocfilehash: 736f7c11ec3de04f1ad52ee29d0a4c952c9b0545
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="move-files-to-and-from-a-linux-vm-using-scp"></a><span data-ttu-id="2b5b7-103">Mover arquivos de e para uma VM Linux usando o SCP</span><span class="sxs-lookup"><span data-stu-id="2b5b7-103">Move files to and from a Linux VM using SCP</span></span>

<span data-ttu-id="2b5b7-104">Este artigo mostra como mover arquivos da estação de trabalho para uma VM Linux do Azure ou de uma VM Linux do Azure para a estação de trabalho, usando o SCP (Cópia Segura).</span><span class="sxs-lookup"><span data-stu-id="2b5b7-104">This article shows how to move files from your workstation up to an Azure Linux VM, or from an Azure Linux VM down to your workstation, using Secure Copy (SCP).</span></span> <span data-ttu-id="2b5b7-105">Mover arquivos entre a estação de trabalho e uma VM Linux, de forma rápida e segura, é uma parte crítica do gerenciamento da infraestrutura do Azure.</span><span class="sxs-lookup"><span data-stu-id="2b5b7-105">Moving files between your workstation and a Linux VM, quickly and securely, is critical for managing your Azure infrastructure.</span></span> 

<span data-ttu-id="2b5b7-106">Para este artigo, você precisa de uma VM Linux implantada no Azure usando [arquivos de chave SSH pública e privada](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2b5b7-106">For this article, you need a Linux VM deployed in Azure using [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="2b5b7-107">Você também precisa de um cliente SCP para o computador local.</span><span class="sxs-lookup"><span data-stu-id="2b5b7-107">You also need an SCP client for your local computer.</span></span> <span data-ttu-id="2b5b7-108">Ele é criado com base em SSH e incluído no shell de Bash padrão da maioria dos computadores Linux e Mac e alguns shells do Windows.</span><span class="sxs-lookup"><span data-stu-id="2b5b7-108">It is built on top of SSH and included in the default Bash shell of most Linux and Mac computers and some Windows shells.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="2b5b7-109">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="2b5b7-109">Quick commands</span></span>

<span data-ttu-id="2b5b7-110">Copiar um arquivo para a VM Linux</span><span class="sxs-lookup"><span data-stu-id="2b5b7-110">Copy a file up to the Linux VM</span></span>

```bash
scp file azureuser@azurehost:directory/targetfile
```

<span data-ttu-id="2b5b7-111">Copiar um arquivo da VM Linux</span><span class="sxs-lookup"><span data-stu-id="2b5b7-111">Copy a file down from the Linux VM</span></span>

```bash
scp azureuser@azurehost:directory/file targetfile
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="2b5b7-112">Passo a passo detalhado</span><span class="sxs-lookup"><span data-stu-id="2b5b7-112">Detailed walkthrough</span></span>

<span data-ttu-id="2b5b7-113">Como exemplo, movemos um arquivo de configuração do Azure para uma VM Linux e efetuamos pull de um diretório de arquivos de log, ambos usando o SCP e chaves SSH.</span><span class="sxs-lookup"><span data-stu-id="2b5b7-113">As examples, we move an Azure configuration file up to a Linux VM and pull down a log file directory, both using SCP and SSH keys.</span></span>   

## <a name="ssh-key-pair-authentication"></a><span data-ttu-id="2b5b7-114">Autenticação de par de chaves SSH</span><span class="sxs-lookup"><span data-stu-id="2b5b7-114">SSH key pair authentication</span></span>

<span data-ttu-id="2b5b7-115">O SCP usa o SSH para a camada de transporte.</span><span class="sxs-lookup"><span data-stu-id="2b5b7-115">SCP uses SSH for the transport layer.</span></span> <span data-ttu-id="2b5b7-116">O SSH manipula a autenticação no host de destino e também move o arquivo em um túnel criptografado fornecido por padrão com o SSH.</span><span class="sxs-lookup"><span data-stu-id="2b5b7-116">SSH handles the authentication on the destination host, and it moves the file in an encrypted tunnel provided by default with SSH.</span></span> <span data-ttu-id="2b5b7-117">Para autenticação de SSH, nomes de usuário e senhas podem ser usados.</span><span class="sxs-lookup"><span data-stu-id="2b5b7-117">For SSH authentication, usernames and passwords can be used.</span></span> <span data-ttu-id="2b5b7-118">No entanto, a autenticação de chaves SSH públicas e privadas é recomendada como uma melhor prática de segurança.</span><span class="sxs-lookup"><span data-stu-id="2b5b7-118">However, SSH public and private key authentication are recommended as a security best practice.</span></span> <span data-ttu-id="2b5b7-119">Depois de o SSH autenticar a conexão, o SCP inicia a cópia do arquivo.</span><span class="sxs-lookup"><span data-stu-id="2b5b7-119">Once SSH has authenticated the connection, SCP then begins copying the file.</span></span> <span data-ttu-id="2b5b7-120">Usando um `~/.ssh/config` configurado corretamente e chaves SSH pública e privada, a conexão do SCP pode ser estabelecida sem o uso de um nome de usuário, com apenas um nome do servidor (ou endereço IP).</span><span class="sxs-lookup"><span data-stu-id="2b5b7-120">Using a properly configured `~/.ssh/config` and SSH public and private keys, the SCP connection can be established by just using a server name (or IP address).</span></span> <span data-ttu-id="2b5b7-121">Se você tiver apenas uma chave SSH, o SCP a procurará no diretório `~/.ssh/` e a usará por padrão para fazer logon na VM.</span><span class="sxs-lookup"><span data-stu-id="2b5b7-121">If you only have one SSH key, SCP looks for it in the `~/.ssh/` directory, and uses it by default to log in to the VM.</span></span>

<span data-ttu-id="2b5b7-122">Para obter mais informações sobre como configurar o `~/.ssh/config` e chaves SSH pública e privada, veja [Create SSH keys](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Criar chaves SSH).</span><span class="sxs-lookup"><span data-stu-id="2b5b7-122">For more information on configuring your `~/.ssh/config` and SSH public and private keys, see [Create SSH keys](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="scp-a-file-to-a-linux-vm"></a><span data-ttu-id="2b5b7-123">Usar o SCP para copiar um arquivo para uma VM Linux</span><span class="sxs-lookup"><span data-stu-id="2b5b7-123">SCP a file to a Linux VM</span></span>

<span data-ttu-id="2b5b7-124">Para o primeiro exemplo, copiamos um arquivo de configuração do Azure para uma VM Linux usada para implantar a automação.</span><span class="sxs-lookup"><span data-stu-id="2b5b7-124">For the first example, we copy an Azure configuration file up to a Linux VM that is used to deploy automation.</span></span> <span data-ttu-id="2b5b7-125">Já que esse arquivo contém credenciais de API do Azure, as quais incluem segredos, a segurança é importante.</span><span class="sxs-lookup"><span data-stu-id="2b5b7-125">Because this file contains Azure API credentials, which include secrets, security is important.</span></span> <span data-ttu-id="2b5b7-126">O túnel criptografado fornecido por SSH protege o conteúdo do arquivo.</span><span class="sxs-lookup"><span data-stu-id="2b5b7-126">The encrypted tunnel provided by SSH protects the contents of the file.</span></span>

<span data-ttu-id="2b5b7-127">O comando a seguir copia o arquivo local *.azure/config* para uma VM do Azure com o FQDN *myserver.eastus.cloudapp.azure.com*. O nome de usuário administrador na VM do Azure é *azureuser*.</span><span class="sxs-lookup"><span data-stu-id="2b5b7-127">The following command copies the local *.azure/config* file to an Azure VM with FQDN *myserver.eastus.cloudapp.azure.com*. The admin user name on the Azure VM is *azureuser*.</span></span> <span data-ttu-id="2b5b7-128">O arquivo é direcionado para o diretório */home/azureuser/*.</span><span class="sxs-lookup"><span data-stu-id="2b5b7-128">The file is targeted to the */home/azureuser/* directory.</span></span> <span data-ttu-id="2b5b7-129">Substitua seus próprios valores nesse comando.</span><span class="sxs-lookup"><span data-stu-id="2b5b7-129">Substitute your own values in this command.</span></span>

```bash
scp ~/.azure/config azureuser@myserver.eastus.cloudapp.com:/home/azureuser/config
```

## <a name="scp-a-directory-from-a-linux-vm"></a><span data-ttu-id="2b5b7-130">Usar o SCP para copiar um diretório de uma VM Linux</span><span class="sxs-lookup"><span data-stu-id="2b5b7-130">SCP a directory from a Linux VM</span></span>

<span data-ttu-id="2b5b7-131">Neste exemplo, copiamos um diretório de arquivos de log da VM Linux para a estação de trabalho.</span><span class="sxs-lookup"><span data-stu-id="2b5b7-131">For this example, we copy a directory of log files from the Linux VM down to your workstation.</span></span> <span data-ttu-id="2b5b7-132">Um arquivo de log pode ou não conter dados confidenciais ou segredos.</span><span class="sxs-lookup"><span data-stu-id="2b5b7-132">A log file may or may not contain sensitive or secret data.</span></span> <span data-ttu-id="2b5b7-133">No entanto, usar o SCP garante que o conteúdo dos arquivos de log é criptografado.</span><span class="sxs-lookup"><span data-stu-id="2b5b7-133">However, using SCP ensures the contents of the log files are encrypted.</span></span> <span data-ttu-id="2b5b7-134">Usar o SCP para transferir os arquivos é a maneira mais fácil de enviar o diretório de log e os arquivos para a estação de trabalho e, ao mesmo tempo, permanecer seguro.</span><span class="sxs-lookup"><span data-stu-id="2b5b7-134">Using SCP to transfer the files is the easiest way to get the log directory and files down to your workstation while also being secure.</span></span>

<span data-ttu-id="2b5b7-135">O comando a seguir copia os arquivos no diretório *inicial/azureuser/logs/* na VM do Azure para o diretório local /tmp:</span><span class="sxs-lookup"><span data-stu-id="2b5b7-135">The following command copies files in the */home/azureuser/logs/* directory on the Azure VM to the local /tmp directory:</span></span>

```bash
scp -r azureuser@myserver.eastus.cloudapp.com:/home/azureuser/logs/. /tmp/
```

<span data-ttu-id="2b5b7-136">O sinalizador `-r` da CLI instrui o SCP a copiar os arquivos e diretórios recursivamente do ponto do diretório listado no comando.</span><span class="sxs-lookup"><span data-stu-id="2b5b7-136">The `-r` cli flag instructs SCP to recursively copy the files and directories from the point of the directory listed in the command.</span></span>  <span data-ttu-id="2b5b7-137">Observe também que a sintaxe de linha de comando é semelhante a um comando de cópia `cp`.</span><span class="sxs-lookup"><span data-stu-id="2b5b7-137">Also notice that the command-line syntax is similar to a `cp` copy command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b5b7-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2b5b7-138">Next steps</span></span>

* [<span data-ttu-id="2b5b7-139">Gerenciar usuários, SSH e verificar ou reparar discos em VMs do Linux do Azure usando a extensão VMAccess</span><span class="sxs-lookup"><span data-stu-id="2b5b7-139">Manage users, SSH, and check or repair disks on Azure Linux VMs using the VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)