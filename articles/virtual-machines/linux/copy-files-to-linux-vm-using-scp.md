---
title: aaaMove arquivos tooand de VMs do Linux do Azure com SCP | Microsoft Docs
description: "Mova arquivos tooand com segurança de uma VM do Linux no Azure usando o SCP e um par de chaves SSH."
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
ms.openlocfilehash: 9e4dce667aa581df74aec3d45a6ba5e52f777d1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-files-tooand-from-a-linux-vm-using-scp"></a><span data-ttu-id="a61d1-103">Mover arquivos tooand de uma VM do Linux usando o SCP</span><span class="sxs-lookup"><span data-stu-id="a61d1-103">Move files tooand from a Linux VM using SCP</span></span>

<span data-ttu-id="a61d1-104">Este artigo mostra como toomove arquivos de backup tooan VM do Linux do Azure em sua estação de trabalho ou de uma VM do Linux do Azure para baixo tooyour estação de trabalho, usando cópia segura (SCP).</span><span class="sxs-lookup"><span data-stu-id="a61d1-104">This article shows how toomove files from your workstation up tooan Azure Linux VM, or from an Azure Linux VM down tooyour workstation, using Secure Copy (SCP).</span></span> <span data-ttu-id="a61d1-105">Mover arquivos entre a estação de trabalho e uma VM Linux, de forma rápida e segura, é uma parte crítica do gerenciamento da infraestrutura do Azure.</span><span class="sxs-lookup"><span data-stu-id="a61d1-105">Moving files between your workstation and a Linux VM, quickly and securely, is critical for managing your Azure infrastructure.</span></span> 

<span data-ttu-id="a61d1-106">Para este artigo, você precisa de uma VM Linux implantada no Azure usando [arquivos de chave SSH pública e privada](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a61d1-106">For this article, you need a Linux VM deployed in Azure using [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="a61d1-107">Você também precisa de um cliente SCP para o computador local.</span><span class="sxs-lookup"><span data-stu-id="a61d1-107">You also need an SCP client for your local computer.</span></span> <span data-ttu-id="a61d1-108">É criado com base em SSH e incluído no shell de Bash saudação padrão da maioria dos computadores Linux e Mac e alguns shells do Windows.</span><span class="sxs-lookup"><span data-stu-id="a61d1-108">It is built on top of SSH and included in hello default Bash shell of most Linux and Mac computers and some Windows shells.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="a61d1-109">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="a61d1-109">Quick commands</span></span>

<span data-ttu-id="a61d1-110">Copiar um arquivo de backup toohello VM do Linux</span><span class="sxs-lookup"><span data-stu-id="a61d1-110">Copy a file up toohello Linux VM</span></span>

```bash
scp file azureuser@azurehost:directory/targetfile
```

<span data-ttu-id="a61d1-111">Copiar um arquivo para baixo de saudação VM do Linux</span><span class="sxs-lookup"><span data-stu-id="a61d1-111">Copy a file down from hello Linux VM</span></span>

```bash
scp azureuser@azurehost:directory/file targetfile
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="a61d1-112">Passo a passo detalhado</span><span class="sxs-lookup"><span data-stu-id="a61d1-112">Detailed walkthrough</span></span>

<span data-ttu-id="a61d1-113">Como exemplos, mover um arquivo de configuração do Azure backup tooa VM do Linux e baixar um diretório de arquivos de log, usando chaves SCP e SSH.</span><span class="sxs-lookup"><span data-stu-id="a61d1-113">As examples, we move an Azure configuration file up tooa Linux VM and pull down a log file directory, both using SCP and SSH keys.</span></span>   

## <a name="ssh-key-pair-authentication"></a><span data-ttu-id="a61d1-114">Autenticação de par de chaves SSH</span><span class="sxs-lookup"><span data-stu-id="a61d1-114">SSH key pair authentication</span></span>

<span data-ttu-id="a61d1-115">SCP usa SSH para a camada de transporte hello.</span><span class="sxs-lookup"><span data-stu-id="a61d1-115">SCP uses SSH for hello transport layer.</span></span> <span data-ttu-id="a61d1-116">Identificadores de SSH Olá autenticação no host de destino hello e ele move o arquivo hello em um túnel criptografado fornecido por padrão com o SSH.</span><span class="sxs-lookup"><span data-stu-id="a61d1-116">SSH handles hello authentication on hello destination host, and it moves hello file in an encrypted tunnel provided by default with SSH.</span></span> <span data-ttu-id="a61d1-117">Para autenticação de SSH, nomes de usuário e senhas podem ser usados.</span><span class="sxs-lookup"><span data-stu-id="a61d1-117">For SSH authentication, usernames and passwords can be used.</span></span> <span data-ttu-id="a61d1-118">No entanto, a autenticação de chaves SSH públicas e privadas é recomendada como uma melhor prática de segurança.</span><span class="sxs-lookup"><span data-stu-id="a61d1-118">However, SSH public and private key authentication are recommended as a security best practice.</span></span> <span data-ttu-id="a61d1-119">Depois de SSH autenticou conexão hello, SCP começa, em seguida, copiar o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="a61d1-119">Once SSH has authenticated hello connection, SCP then begins copying hello file.</span></span> <span data-ttu-id="a61d1-120">Usando um adequadamente configurado `~/.ssh/config` e as chaves públicas e privadas de SSH, conexão Olá SCP podem ser estabelecidas usando apenas um nome de servidor (ou endereço IP).</span><span class="sxs-lookup"><span data-stu-id="a61d1-120">Using a properly configured `~/.ssh/config` and SSH public and private keys, hello SCP connection can be established by just using a server name (or IP address).</span></span> <span data-ttu-id="a61d1-121">Se você tiver apenas uma chave SSH, SCP procura por ele no hello `~/.ssh/` directory e usa por padrão toolog em toohello VM.</span><span class="sxs-lookup"><span data-stu-id="a61d1-121">If you only have one SSH key, SCP looks for it in hello `~/.ssh/` directory, and uses it by default toolog in toohello VM.</span></span>

<span data-ttu-id="a61d1-122">Para obter mais informações sobre como configurar o `~/.ssh/config` e chaves SSH pública e privada, veja [Create SSH keys](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Criar chaves SSH).</span><span class="sxs-lookup"><span data-stu-id="a61d1-122">For more information on configuring your `~/.ssh/config` and SSH public and private keys, see [Create SSH keys](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="scp-a-file-tooa-linux-vm"></a><span data-ttu-id="a61d1-123">SCP tooa um arquivo VM do Linux</span><span class="sxs-lookup"><span data-stu-id="a61d1-123">SCP a file tooa Linux VM</span></span>

<span data-ttu-id="a61d1-124">Por exemplo, primeiro hello, podemos copiar um arquivo de configuração do Azure backup tooa VM do Linux que é automação toodeploy usado.</span><span class="sxs-lookup"><span data-stu-id="a61d1-124">For hello first example, we copy an Azure configuration file up tooa Linux VM that is used toodeploy automation.</span></span> <span data-ttu-id="a61d1-125">Já que esse arquivo contém credenciais de API do Azure, as quais incluem segredos, a segurança é importante.</span><span class="sxs-lookup"><span data-stu-id="a61d1-125">Because this file contains Azure API credentials, which include secrets, security is important.</span></span> <span data-ttu-id="a61d1-126">túnel criptografado Hello, fornecido pelo SSH protege o conteúdo de saudação do arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="a61d1-126">hello encrypted tunnel provided by SSH protects hello contents of hello file.</span></span>

<span data-ttu-id="a61d1-127">Olá seguintes comando cópias Olá local *.azure/config* tooan VM do Azure com o FQDN do arquivo *myserver.eastus.cloudapp.azure.com*. nome de usuário de administrador Olá em hello Azure VM é *azureuser* .</span><span class="sxs-lookup"><span data-stu-id="a61d1-127">hello following command copies hello local *.azure/config* file tooan Azure VM with FQDN *myserver.eastus.cloudapp.azure.com*. hello admin user name on hello Azure VM is *azureuser*.</span></span> <span data-ttu-id="a61d1-128">arquivo Hello é destino toohello */home/azureuser/* directory.</span><span class="sxs-lookup"><span data-stu-id="a61d1-128">hello file is targeted toohello */home/azureuser/* directory.</span></span> <span data-ttu-id="a61d1-129">Substitua seus próprios valores nesse comando.</span><span class="sxs-lookup"><span data-stu-id="a61d1-129">Substitute your own values in this command.</span></span>

```bash
scp ~/.azure/config azureuser@myserver.eastus.cloudapp.com:/home/azureuser/config
```

## <a name="scp-a-directory-from-a-linux-vm"></a><span data-ttu-id="a61d1-130">Usar o SCP para copiar um diretório de uma VM Linux</span><span class="sxs-lookup"><span data-stu-id="a61d1-130">SCP a directory from a Linux VM</span></span>

<span data-ttu-id="a61d1-131">Neste exemplo, podemos copiar um diretório de arquivos de log da saudação VM Linux para baixo tooyour estação de trabalho.</span><span class="sxs-lookup"><span data-stu-id="a61d1-131">For this example, we copy a directory of log files from hello Linux VM down tooyour workstation.</span></span> <span data-ttu-id="a61d1-132">Um arquivo de log pode ou não conter dados confidenciais ou segredos.</span><span class="sxs-lookup"><span data-stu-id="a61d1-132">A log file may or may not contain sensitive or secret data.</span></span> <span data-ttu-id="a61d1-133">No entanto, usar o SCP garante conteúdo Olá Olá dos arquivos de log é criptografado.</span><span class="sxs-lookup"><span data-stu-id="a61d1-133">However, using SCP ensures hello contents of hello log files are encrypted.</span></span> <span data-ttu-id="a61d1-134">Usando arquivos de saudação do SCP tootransfer é tooget de maneira mais fácil Olá Olá diretório de log e arquivos para baixo da estação de trabalho tooyour ao mesmo tempo, além de ser seguro.</span><span class="sxs-lookup"><span data-stu-id="a61d1-134">Using SCP tootransfer hello files is hello easiest way tooget hello log directory and files down tooyour workstation while also being secure.</span></span>

<span data-ttu-id="a61d1-135">Olá comando a seguir copia arquivos de saudação *inicial/azureuser/logs/* diretório no diretório do hello Azure VM toohello /tmp local:</span><span class="sxs-lookup"><span data-stu-id="a61d1-135">hello following command copies files in hello */home/azureuser/logs/* directory on hello Azure VM toohello local /tmp directory:</span></span>

```bash
scp -r azureuser@myserver.eastus.cloudapp.com:/home/azureuser/logs/. /tmp/
```

<span data-ttu-id="a61d1-136">Olá `-r` cli sinalizador instrui SCP toorecursively copiar Olá arquivos e diretórios de ponto de saudação do diretório Olá listado no comando hello.</span><span class="sxs-lookup"><span data-stu-id="a61d1-136">hello `-r` cli flag instructs SCP toorecursively copy hello files and directories from hello point of hello directory listed in hello command.</span></span>  <span data-ttu-id="a61d1-137">Também Observe que Olá sintaxe de linha de comando é semelhante tooa `cp` comando Copiar.</span><span class="sxs-lookup"><span data-stu-id="a61d1-137">Also notice that hello command-line syntax is similar tooa `cp` copy command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a61d1-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a61d1-138">Next steps</span></span>

* [<span data-ttu-id="a61d1-139">Gerenciar usuários, SSH e seleção ou discos de reparo em máquinas virtuais do Linux do Azure usando Olá extensão VMAccess</span><span class="sxs-lookup"><span data-stu-id="a61d1-139">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
