---
title: "aaaAdd tooa um usuário VM do Linux no Azure | Microsoft Docs"
description: "Adicione um usuário tooa VM do Linux no Azure."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f8aa633b-8b75-45d7-b61d-11ac112cedd5
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/18/2016
ms.author: v-livech
ms.openlocfilehash: eed050154adf0cbed2c168e7aa675bd3ded85fcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-user-tooan-azure-vm"></a><span data-ttu-id="a4a91-103">Adicionar um usuário tooan VM do Azure</span><span class="sxs-lookup"><span data-stu-id="a4a91-103">Add a user tooan Azure VM</span></span>
<span data-ttu-id="a4a91-104">Uma das primeiras tarefas hello em qualquer nova VM do Linux é toocreate um novo usuário.</span><span class="sxs-lookup"><span data-stu-id="a4a91-104">One of hello first tasks on any new Linux VM is toocreate a new user.</span></span>  <span data-ttu-id="a4a91-105">Neste artigo, percorremos criando uma conta de usuário do sudo, definir senha de hello, adicionando chaves públicas SSH e finalmente usar `visudo` sudo tooallow sem uma senha.</span><span class="sxs-lookup"><span data-stu-id="a4a91-105">In this article, we walk through creating a sudo user account, setting hello password, adding SSH Public Keys, and finally use `visudo` tooallow sudo without a password.</span></span>

<span data-ttu-id="a4a91-106">Pré-requisitos são: [uma conta do Azure](https://azure.microsoft.com/pricing/free-trial/), [as chaves públicas e privadas SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), um grupo de recursos do Azure e Olá CLI do Azure instalado e alternado tooAzure Gerenciador de recursos usando o modo `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="a4a91-106">Prerequisites are: [an Azure account](https://azure.microsoft.com/pricing/free-trial/), [SSH public and private keys](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), an Azure resource group, and hello Azure CLI installed and switched tooAzure Resource Manager mode using `azure config mode arm`.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="a4a91-107">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="a4a91-107">Quick Commands</span></span>
```bash
# Add a new user on RedHat family distros
sudo useradd -G wheel exampleUser

# Add a new user on Debian family distros
sudo useradd -G sudo exampleUser

# Set a password
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully

# Copy hello SSH Public Key toohello new user
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver

# Change sudoers tooallow no password
# Execute visudo as root tooedit hello /etc/sudoers file
visudo

# On RedHat family distros uncomment this line:
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

# toothis
## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL

# On Debian family distros change this line:
# Allow members of group sudo tooexecute any command
%sudo   ALL=(ALL:ALL) ALL

# toothis
%sudo   ALL=(ALL) NOPASSWD:ALL

# Verify everything
# Verify hello SSH keys & User account
bill@slackware$ ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="a4a91-108">Passo a passo detalhado</span><span class="sxs-lookup"><span data-stu-id="a4a91-108">Detailed Walkthrough</span></span>
### <a name="introduction"></a><span data-ttu-id="a4a91-109">Introdução</span><span class="sxs-lookup"><span data-stu-id="a4a91-109">Introduction</span></span>
<span data-ttu-id="a4a91-110">Uma das tarefas de primeira e mais comum de saudação com um novo servidor é tooadd uma conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="a4a91-110">One of hello first and most common task with a new server is tooadd a user account.</span></span>  <span data-ttu-id="a4a91-111">Logons de raiz devem ser desabilitados e conta de raiz de saudação em si não deve ser usada com o servidor Linux, somente o sudo.</span><span class="sxs-lookup"><span data-stu-id="a4a91-111">Root logins should be disabled and hello root account itself should not be used with your Linux server, only sudo.</span></span>  <span data-ttu-id="a4a91-112">Fornecendo um escalonamento do usuário raiz privilégios usando o sudo-Olá tooadminister de forma adequada e usar o Linux.</span><span class="sxs-lookup"><span data-stu-id="a4a91-112">Giving a user root escalation privileges using sudo it hello proper way tooadminister and use Linux.</span></span>

<span data-ttu-id="a4a91-113">Usando o comando Olá `useradd` estamos adicionando contas de usuário toohello VM do Linux.</span><span class="sxs-lookup"><span data-stu-id="a4a91-113">Using hello command `useradd` we are adding user accounts toohello Linux VM.</span></span>  <span data-ttu-id="a4a91-114">Executar `useradd` modifica `/etc/passwd`, `/etc/shadow`, `/etc/group` e `/etc/gshadow`.</span><span class="sxs-lookup"><span data-stu-id="a4a91-114">Running `useradd` modifies `/etc/passwd`, `/etc/shadow`, `/etc/group`, and `/etc/gshadow`.</span></span>  <span data-ttu-id="a4a91-115">Estamos adicionando um sinalizador de linha de comando toohello `useradd` comando tooalso adicionar Olá novo usuário toohello sudo adequada grupo no Linux.</span><span class="sxs-lookup"><span data-stu-id="a4a91-115">We are adding a command-line flag toohello `useradd` command tooalso add hello new user toohello proper sudo group on Linux.</span></span>  <span data-ttu-id="a4a91-116">Mesmo que você `useradd` cria uma entrada em `/etc/passwd` ele não oferece a nova conta de usuário Olá uma senha.</span><span class="sxs-lookup"><span data-stu-id="a4a91-116">Even thou `useradd` creates an entry into `/etc/passwd` it does not give hello new user account a password.</span></span>  <span data-ttu-id="a4a91-117">Estamos criando uma senha inicial para o novo usuário de saudação usando Olá simples `passwd` comando.</span><span class="sxs-lookup"><span data-stu-id="a4a91-117">We are creating an initial password for hello new user using hello simple `passwd` command.</span></span>  <span data-ttu-id="a4a91-118">Olá última etapa é toomodify Olá sudo regras que comandos tooexecute de usuário com privilégios de sudo tooallow sem ter que tooenter uma senha para cada comando.</span><span class="sxs-lookup"><span data-stu-id="a4a91-118">hello last step is toomodify hello sudo rules tooallow that user tooexecute commands with sudo privileges without having tooenter a password for every command.</span></span>  <span data-ttu-id="a4a91-119">Fazer logon usando a chave privada hello, assumindo que essa conta de usuário está protegido contra atores ruins e vai tooallow sudo acesso sem uma senha.</span><span class="sxs-lookup"><span data-stu-id="a4a91-119">Logging in using hello Private key we are assuming that user account is safe from bad actors and are going tooallow sudo access without a password.</span></span>  

### <a name="adding-a-single-sudo-user-tooan-azure-vm"></a><span data-ttu-id="a4a91-120">Adicionar um usuário de único sudo tooan VM do Azure</span><span class="sxs-lookup"><span data-stu-id="a4a91-120">Adding a single sudo user tooan Azure VM</span></span>
<span data-ttu-id="a4a91-121">Faça logon no toohello VM do Azure usando as chaves de SSH.</span><span class="sxs-lookup"><span data-stu-id="a4a91-121">Log in toohello Azure VM using SSH keys.</span></span>  <span data-ttu-id="a4a91-122">Se você não tiver configurado o acesso de chave pública SSH, leia este artigo primeiro [Using Public Key Authentication with Azure](http://link.to/article)(Usando Autenticação de Chave Pública com o Azure).</span><span class="sxs-lookup"><span data-stu-id="a4a91-122">If you have not setup SSH public key access, complete this article first [Using Public Key Authentication with Azure](http://link.to/article).</span></span>  

<span data-ttu-id="a4a91-123">Olá `useradd` comando for concluído Olá tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a4a91-123">hello `useradd` command completes hello following tasks:</span></span>

* <span data-ttu-id="a4a91-124">Criar uma nova conta de usuário</span><span class="sxs-lookup"><span data-stu-id="a4a91-124">create a new user account</span></span>
* <span data-ttu-id="a4a91-125">criar um novo grupo de usuários com hello mesmo nome</span><span class="sxs-lookup"><span data-stu-id="a4a91-125">create a new user group with hello same name</span></span>
* <span data-ttu-id="a4a91-126">Adicionar uma entrada em branco muito`/etc/passwd`</span><span class="sxs-lookup"><span data-stu-id="a4a91-126">add a blank entry too`/etc/passwd`</span></span>
* <span data-ttu-id="a4a91-127">Adicionar uma entrada em branco muito`/etc/gpasswd`</span><span class="sxs-lookup"><span data-stu-id="a4a91-127">add a blank entry too`/etc/gpasswd`</span></span>

<span data-ttu-id="a4a91-128">Olá `-G` sinalizador de linha de comando adiciona Olá novo usuário conta toohello adequado Linux grupo dando a nova conta de usuário Olá privilégios de escalonamento de raiz.</span><span class="sxs-lookup"><span data-stu-id="a4a91-128">hello `-G` command-line flag adds hello new user account toohello proper Linux group giving hello new user account root escalation privileges.</span></span>

#### <a name="add-hello-user"></a><span data-ttu-id="a4a91-129">Adicionar usuário Olá</span><span class="sxs-lookup"><span data-stu-id="a4a91-129">Add hello user</span></span>
```bash
# On RedHat family distros
sudo useradd -G wheel exampleUser

# On Debian family distros
sudo useradd -G sudo exampleUser
```

#### <a name="set-a-password"></a><span data-ttu-id="a4a91-130">Definir uma senha</span><span class="sxs-lookup"><span data-stu-id="a4a91-130">Set a password</span></span>
<span data-ttu-id="a4a91-131">Olá `useradd` comando cria o usuário hello e adiciona uma entrada tooboth `/etc/passwd` e `/etc/gpasswd` , mas não definem senha hello.</span><span class="sxs-lookup"><span data-stu-id="a4a91-131">hello `useradd` command creates hello user and adds an entry tooboth `/etc/passwd` and `/etc/gpasswd` but does not actually set hello password.</span></span>  <span data-ttu-id="a4a91-132">Olá senha é toohello entrada adicionada usando Olá `passwd` comando.</span><span class="sxs-lookup"><span data-stu-id="a4a91-132">hello password is added toohello entry using hello `passwd` command.</span></span>

```bash
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
```

<span data-ttu-id="a4a91-133">Agora temos um usuário com privilégios de sudo no servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="a4a91-133">We now have a user with sudo privileges on hello server.</span></span>

### <a name="add-your-ssh-public-key-toohello-new-user-account"></a><span data-ttu-id="a4a91-134">Adicione sua chave pública SSH toohello nova conta de usuário</span><span class="sxs-lookup"><span data-stu-id="a4a91-134">Add your SSH Public Key toohello new user account</span></span>
<span data-ttu-id="a4a91-135">Em seu computador, use Olá `ssh-copy-id` comando com a nova senha hello.</span><span class="sxs-lookup"><span data-stu-id="a4a91-135">From your machine, use hello `ssh-copy-id` command with hello new password.</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver
```

### <a name="using-visudo-tooallow-sudo-usage-without-a-password"></a><span data-ttu-id="a4a91-136">Usando visudo tooallow sudo uso sem uma senha</span><span class="sxs-lookup"><span data-stu-id="a4a91-136">Using visudo tooallow sudo usage without a password</span></span>
<span data-ttu-id="a4a91-137">Usando `visudo` tooedit Olá `/etc/sudoers` arquivo adiciona alguns camadas de proteção contra incorretamente modificar esse arquivo importante.</span><span class="sxs-lookup"><span data-stu-id="a4a91-137">Using `visudo` tooedit hello `/etc/sudoers` file adds a few layers of protection against incorrectly modifying this important file.</span></span>  <span data-ttu-id="a4a91-138">Após a execução `visudo`, Olá `/etc/sudoers` arquivo está bloqueado tooensure nenhum outro usuário pode fazer alterações enquanto ela está sendo editada ativamente.</span><span class="sxs-lookup"><span data-stu-id="a4a91-138">Upon executing `visudo`, hello `/etc/sudoers` file is locked tooensure no other user can make changes while it is actively being edited.</span></span>  <span data-ttu-id="a4a91-139">Olá `/etc/sudoers` arquivo também é verificado quanto a erros por `visudo` quando você tentar toosave ou sair e não é possível salvar um arquivo sudoers quebrada.</span><span class="sxs-lookup"><span data-stu-id="a4a91-139">hello `/etc/sudoers` file is also checked for mistakes by `visudo` when you attempt toosave or exit so you cannot save a broken sudoers file.</span></span>

<span data-ttu-id="a4a91-140">Já temos os usuários no grupo de padrão correto Olá para sudo acesso.</span><span class="sxs-lookup"><span data-stu-id="a4a91-140">We already have users in hello correct default group for sudo access.</span></span>  <span data-ttu-id="a4a91-141">Agora, vamos tooenable esses grupos toouse sudo com e sem senha.</span><span class="sxs-lookup"><span data-stu-id="a4a91-141">Now we are going tooenable those groups toouse sudo with no password.</span></span>

```bash
# Execute visudo as root tooedit hello /etc/sudoers file
visudo

# On RedHat family distros uncomment this line:
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

# toothis
## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL

# On Debian family distros change this line:
# Allow members of group sudo tooexecute any command
%sudo   ALL=(ALL:ALL) ALL

# toothis
%sudo   ALL=(ALL) NOPASSWD:ALL
```

### <a name="verify-hello-user-ssh-keys-and-sudo"></a><span data-ttu-id="a4a91-142">Verifique se o usuário hello, ssh chaves e sudo</span><span class="sxs-lookup"><span data-stu-id="a4a91-142">Verify hello user, ssh keys, and sudo</span></span>
```bash
# Verify hello SSH keys & User account
ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```
