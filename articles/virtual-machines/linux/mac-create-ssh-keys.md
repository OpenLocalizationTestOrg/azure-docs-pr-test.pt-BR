---
title: aaaCreate e use um SSH par de chaves para VMs do Linux no Azure | Microsoft Docs
description: "Como toocreate e use um par de chamadas chaves público e privado SSH para VMs do Linux no Azure tooimprove Olá segurança saudação do processo de autenticação."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 34ae9482-da3e-4b2d-9d0d-9d672aa42498
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/14/2017
ms.author: iainfou
ms.openlocfilehash: 7fb94841d34d5bc006f3134adf91102ddce5f174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-use-an-ssh-public-and-private-key-pair-for-linux-vms-in-azure"></a><span data-ttu-id="efb63-103">Como toocreate e usar uma chave pública e privada do SSH par para VMs do Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="efb63-103">How toocreate and use an SSH public and private key pair for Linux VMs in Azure</span></span>
<span data-ttu-id="efb63-104">Com um par de chaves de SSH (secure shell), você pode criar máquinas virtuais (VMs) no Azure que usam as chaves de SSH para autenticação, eliminando a necessidade de saudação para senhas toolog em.</span><span class="sxs-lookup"><span data-stu-id="efb63-104">With a secure shell (SSH) key pair, you can create virtual machines (VMs) in Azure that use SSH keys for authentication, eliminating hello need for passwords toolog in.</span></span> <span data-ttu-id="efb63-105">Este artigo mostra como tooquickly gerar e usar um par de arquivo de chave pública e privada SSH versão 2 do protocolo RSA para VMs do Linux.</span><span class="sxs-lookup"><span data-stu-id="efb63-105">This article shows you how tooquickly generate and use an SSH protocol version 2 RSA public and private key file pair for Linux VMs.</span></span> <span data-ttu-id="efb63-106">Para obter mais etapas e exemplos adicionais, consulte [detalhadas certificados e pares de chave SSH do etapas toocreate](create-ssh-keys-detailed.md).</span><span class="sxs-lookup"><span data-stu-id="efb63-106">For more detailed steps and additional examples, see [detailed steps toocreate SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

## <a name="create-an-ssh-key-pair"></a><span data-ttu-id="efb63-107">Criar um par de chaves SSH</span><span class="sxs-lookup"><span data-stu-id="efb63-107">Create an SSH key pair</span></span>
<span data-ttu-id="efb63-108">Saudação de uso `ssh-keygen` arquivos de comando toocreate SSH públicos e privados chave por padrão criado no hello `~/.ssh` diretório, mas você pode especificar um local diferente e senha adicional (uma senha tooaccess Olá arquivo de chave privada) quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="efb63-108">Use hello `ssh-keygen` command toocreate SSH public and private key files that are by default created in hello `~/.ssh` directory, but you can specify a different location and additional passphrase (a password tooaccess hello private key file) when prompted.</span></span> <span data-ttu-id="efb63-109">Execute Olá comando a seguir de um shell Bash, responder a prompts Olá com suas próprias informações.</span><span class="sxs-lookup"><span data-stu-id="efb63-109">Run hello following command from a Bash shell, answering hello prompts with your own information.</span></span>

```bash
ssh-keygen -t rsa -b 2048
```

## <a name="use-hello-ssh-key-pair"></a><span data-ttu-id="efb63-110">Use o par de chaves de SSH Olá</span><span class="sxs-lookup"><span data-stu-id="efb63-110">Use hello SSH key pair</span></span>
<span data-ttu-id="efb63-111">chave pública de saudação que você coloca na sua VM do Linux no Azure é armazenados por padrão em `~/.ssh/id_rsa.pub`, a menos que você alterou o local de hello quando você criou.</span><span class="sxs-lookup"><span data-stu-id="efb63-111">hello public key that you place on your Linux VM in Azure is by default stored in `~/.ssh/id_rsa.pub`, unless you changed hello location when you created them.</span></span> <span data-ttu-id="efb63-112">Se você usar o hello [2.0 do CLI do Azure](/cli/azure) toocreate sua VM, especifique o local de saudação dessa chave pública quando você usar o hello [criar vm az](/cli/azure/vm#create) com hello `--ssh-key-path` opção.</span><span class="sxs-lookup"><span data-stu-id="efb63-112">If you use hello [Azure CLI 2.0](/cli/azure) toocreate your VM, specify hello location of this public key when you use hello [az vm create](/cli/azure/vm#create) with hello `--ssh-key-path` option.</span></span> <span data-ttu-id="efb63-113">Se você copia e cola conteúdo de saudação de toouse do arquivo de chave pública Olá Olá portal do Azure ou um modelo do Gerenciador de recursos, certifique-se de que não copiar nenhum espaço em branco adicional.</span><span class="sxs-lookup"><span data-stu-id="efb63-113">If you copy and paste hello contents of hello public key file toouse in hello Azure portal or a Resource Manager template, make sure you don't copy any additional whitespace.</span></span> <span data-ttu-id="efb63-114">Por exemplo, se você usar OS X, você pode direcionar o arquivo de chave pública hello (por padrão, **~/.ssh/id_rsa.pub**) muito**pbcopy** toocopy conteúdo de saudação (há outros programas de Linux que Olá a mesma coisa, como `xclip`).</span><span class="sxs-lookup"><span data-stu-id="efb63-114">For example, if you use OS X, you can pipe hello public key file (by default, **~/.ssh/id_rsa.pub**) too**pbcopy** toocopy hello contents (there are other Linux programs that do hello same thing, such as `xclip`).</span></span>

<span data-ttu-id="efb63-115">Se você não estiver familiarizado com as chaves públicas SSH, veja sua chave pública executando `cat` da seguinte forma, substituindo `~/.ssh/id_rsa.pub` por seu próprio local de arquivo de chave pública:</span><span class="sxs-lookup"><span data-stu-id="efb63-115">If you're not familiar with SSH public keys, you can see your public key by running `cat` as follows, replacing `~/.ssh/id_rsa.pub` with your own public key file location:</span></span>

```bash
cat ~/.ssh/id_rsa.pub
```

<span data-ttu-id="efb63-116">Com a chave pública de saudação em sua VM do Azure, usando o SSH tooyour VM Olá endereço IP ou nome DNS da VM (Lembre-se de tooreplace `azureuser` e `myvm.westus.cloudapp.azure.com` abaixo com o nome de usuário de administrador hello e IP ou nome de domínio totalmente qualificado do hello-- endereço):</span><span class="sxs-lookup"><span data-stu-id="efb63-116">With hello public key on your Azure VM, SSH tooyour VM using hello IP address or DNS name of your VM (remember tooreplace `azureuser` and `myvm.westus.cloudapp.azure.com` below with hello admin username and hello fully qualified domain name -- or IP address):</span></span>

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

<span data-ttu-id="efb63-117">Se você forneceu uma senha quando você criou o par de chaves, insira a senha de saudação quando solicitado durante o processo de logon hello.</span><span class="sxs-lookup"><span data-stu-id="efb63-117">If you provided a passphrase when you created your key pair, enter hello passphrase when prompted during hello login process.</span></span> <span data-ttu-id="efb63-118">(servidor de saudação é adicionado tooyour `~/.ssh/known_hosts` pasta e você não será solicitado tooconnect novamente até que a chave pública de saudação em suas alterações de VM do Azure ou o nome do servidor de saudação é removido do `~/.ssh/known_hosts`.)</span><span class="sxs-lookup"><span data-stu-id="efb63-118">(hello server is added tooyour `~/.ssh/known_hosts` folder, and you won't be asked tooconnect again until hello public key on your Azure VM changes or hello server name is removed from `~/.ssh/known_hosts`.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="efb63-119">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="efb63-119">Next steps</span></span>

<span data-ttu-id="efb63-120">Máquinas virtuais criadas usando as chaves de SSH são por padrão configurado com senhas desabilitadas, toomake forçada bruta adivinhação tentativas muito mais caro e, portanto, difícil.</span><span class="sxs-lookup"><span data-stu-id="efb63-120">VMs created using SSH keys are by default configured with passwords disabled, toomake brute-forced guessing attempts vastly more expensive and therefore difficult.</span></span> <span data-ttu-id="efb63-121">Este tópico descreve como criar um par de chaves SSH simples para uso rápido.</span><span class="sxs-lookup"><span data-stu-id="efb63-121">This topic describes creating a simple SSH key pair for quick usage.</span></span> <span data-ttu-id="efb63-122">Se você precisa de mais ajuda na criação de par de chaves de SSH ou exige certificados adicionais, consulte [detalhadas certificados e pares de chave SSH do etapas toocreate](create-ssh-keys-detailed.md).</span><span class="sxs-lookup"><span data-stu-id="efb63-122">If you need more assistance in creating your SSH key pair or require additional certificates, see [Detailed steps toocreate SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

<span data-ttu-id="efb63-123">Você pode criar máquinas virtuais que usam o par de chaves de SSH usando Olá portal do Azure, CLI e modelos:</span><span class="sxs-lookup"><span data-stu-id="efb63-123">You can create VMs that use your SSH key pair using hello Azure portal, CLI, and templates:</span></span>

* [<span data-ttu-id="efb63-124">Criar uma VM do Linux segura usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="efb63-124">Create a secure Linux VM using hello Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="efb63-125">Criar uma VM do Linux segura usando hello Azure CLI 2.0)</span><span class="sxs-lookup"><span data-stu-id="efb63-125">Create a secure Linux VM using hello Azure CLI 2.0)</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="efb63-126">Criar uma VM do Linux segura usando um modelo do Azure</span><span class="sxs-lookup"><span data-stu-id="efb63-126">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
