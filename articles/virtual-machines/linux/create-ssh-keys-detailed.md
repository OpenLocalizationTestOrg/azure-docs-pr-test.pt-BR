---
title: etapas de aaaDetailed toocreate um SSH par de chaves para VMs do Linux no Azure | Microsoft Docs
description: "Saiba mais sobre etapas adicionais toocreate um par de chamadas chaves público e privado SSH para VMs do Linux no Azure, junto com certificados específicos para casos de uso diferentes."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 6/28/2017
ms.author: danlep
ms.openlocfilehash: 9ac52ef4dc87e73b9c07ccc323adc955829e2014
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="detailed-walk-through-toocreate-an-ssh-key-pair-and-additional-certificates-for-a-linux-vm-in-azure"></a><span data-ttu-id="2d9a4-103">Detalhadas passo a passo toocreate um par de chave SSH e certificados adicionais para uma VM do Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="2d9a4-103">Detailed walk through toocreate an SSH key pair and additional certificates for a Linux VM in Azure</span></span>
<span data-ttu-id="2d9a4-104">Com um par de chaves de SSH, você pode criar máquinas virtuais no Azure que padrão toousing as chaves de SSH para a autenticação, eliminando a necessidade de saudação para senhas toolog em.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-104">With an SSH key pair, you can create Virtual Machines on Azure that default toousing SSH keys for authentication, eliminating hello need for passwords toolog in.</span></span> <span data-ttu-id="2d9a4-105">As senhas podem ser adivinhadas e abra suas VMs backup toorelentless tooguess de tentativas de força bruta sua senha.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-105">Passwords can be guessed, and open your VMs up toorelentless brute force attempts tooguess your password.</span></span> <span data-ttu-id="2d9a4-106">Máquinas virtuais criadas com modelos de saudação CLI do Azure ou o Gerenciador de recursos podem incluir sua chave pública SSH como parte da implantação hello, removendo a etapa de configuração de implantação de postagem de desabilitar os logons de senha para o SSH.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-106">VMs created with hello Azure CLI or Resource Manager templates can include your SSH public key as part of hello deployment, removing a post deployment configuration step of disabling password logins for SSH.</span></span> <span data-ttu-id="2d9a4-107">Este artigo fornece etapas detalhadas e exemplos adicionais de geração de certificados, por exemplo, para uso com máquinas virtuais Linux.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-107">This article provides detailed steps and additional examples of generating certificates, such as for use with Linux virtual machines.</span></span> <span data-ttu-id="2d9a4-108">Se você quiser tooquickly criar e usar um par de chave SSH, consulte [como toocreate uma chave pública e privada do SSH par para VMs do Linux no Azure](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="2d9a4-108">If you want tooquickly create and use an SSH key pair, see [How toocreate an SSH public and private key pair for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

## <a name="understanding-ssh-keys"></a><span data-ttu-id="2d9a4-109">Noções básicas das chaves SSH</span><span class="sxs-lookup"><span data-stu-id="2d9a4-109">Understanding SSH keys</span></span>

<span data-ttu-id="2d9a4-110">Usar as chaves públicas e privadas SSH é Olá toolog de maneira mais fácil em servidores Linux de tooyour.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-110">Using SSH public and private keys is hello easiest way toolog in tooyour Linux servers.</span></span> <span data-ttu-id="2d9a4-111">[Criptografia de chave pública](https://en.wikipedia.org/wiki/Public-key_cryptography) fornece um toolog de maneira muito mais seguro em tooyour Linux ou BSD VM no Azure que senhas, que podem ser forçado bruta muito mais facilmente.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-111">[Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) provides a much more secure way toolog in tooyour Linux or BSD VM in Azure than passwords, which can be brute-forced far more easily.</span></span>

<span data-ttu-id="2d9a4-112">Sua chave pública pode ser compartilhada com qualquer pessoa; mas apenas você (ou sua infraestrutura de segurança local) possui sua chave privada.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-112">Your public key can be shared with anyone; but only you (or your local security infrastructure) possess your private key.</span></span>  <span data-ttu-id="2d9a4-113">a chave privada SSH Olá deve ter uma [senha segura muito](https://www.xkcd.com/936/) (fonte:[xkcd.com](https://xkcd.com)) toosafeguard-lo.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-113">hello SSH private key should have a [very secure password](https://www.xkcd.com/936/) (source:[xkcd.com](https://xkcd.com)) toosafeguard it.</span></span>  <span data-ttu-id="2d9a4-114">Essa senha é tooaccess apenas Olá SSH arquivo de chave privada e **não é** senha de conta de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-114">This password is just tooaccess hello private SSH key file and **is not** hello user account password.</span></span>  <span data-ttu-id="2d9a4-115">Quando você adiciona uma chave SSH tooyour senha, ele criptografa chave privada de saudação usando AES de 128 bits, para que hello chave privada é inútil sem Olá senha toodecrypt-lo.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-115">When you add a password tooyour SSH key, it encrypts hello private key using 128-bit AES, so that hello private key is useless without hello password toodecrypt it.</span></span>  <span data-ttu-id="2d9a4-116">Se um invasor roubar sua chave privada e que a chave não tem uma senha, seria capaz de toouse ou privada da chave toolog em servidores tooany que tem uma chave pública correspondente de saudação.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-116">If an attacker stole your private key and that key did not have a password, they would be able toouse that private key toolog in tooany servers that have hello corresponding public key.</span></span>  <span data-ttu-id="2d9a4-117">Se uma chave privada for protegida por senha, ela não poderá ser usada por esse invasor, o que é uma camada adicional de segurança para sua infraestrutura no Azure.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-117">If a private key is password protected it cannot be used by that attacker, providing an additional layer of security for your infrastructure on Azure.</span></span>

<span data-ttu-id="2d9a4-118">Este artigo cria uma protocolo SSH versão 2 pares de arquivo de chave pública e privada de RSA (também chamado tooas "ssh-rsa" as chaves), que são recomendados para implantações com o Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-118">This article creates an SSH protocol version 2 RSA public and private key file pair (also referred tooas "ssh-rsa" keys), which are recommended for deployments with Azure Resource Manager.</span></span> <span data-ttu-id="2d9a4-119">*SSH-rsa* as chaves são necessárias Olá [portal](https://portal.azure.com) para clássico e implantações do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-119">*ssh-rsa* keys are required on hello [portal](https://portal.azure.com) for both classic and Resource Manager deployments.</span></span>

## <a name="ssh-keys-use-and-benefits"></a><span data-ttu-id="2d9a4-120">Benefícios e uso das chaves SSH</span><span class="sxs-lookup"><span data-stu-id="2d9a4-120">SSH keys use and benefits</span></span>

<span data-ttu-id="2d9a4-121">O Azure requer pelo menos 2048 bits, protocolo de SSH versão 2 RSA formato chaves públicas e privadas; o arquivo de chave pública Olá tem Olá `.pub` formato de contêiner.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-121">Azure requires at least 2048-bit, SSH protocol version 2 RSA format public and private keys; hello public key file has hello `.pub` container format.</span></span> <span data-ttu-id="2d9a4-122">Olá toocreate chaves use `ssh-keygen`, que faz uma série de perguntas e, em seguida, grava uma chave privada e uma chave pública correspondente.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-122">toocreate hello keys use `ssh-keygen`, which asks a series of questions and then writes a private key and a matching public key.</span></span> <span data-ttu-id="2d9a4-123">Quando uma VM do Azure é criada, as cópias do Azure Olá toohello chave pública `~/.ssh/authorized_keys` pasta Olá VM.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-123">When an Azure VM is created, Azure copies hello public key toohello `~/.ssh/authorized_keys` folder on hello VM.</span></span> <span data-ttu-id="2d9a4-124">As chaves de SSH no `~/.ssh/authorized_keys` são usados toochallenge Olá cliente toomatch Olá chave privada correspondente em uma conexão de logon SSH.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-124">SSH keys in `~/.ssh/authorized_keys` are used toochallenge hello client toomatch hello corresponding private key on an SSH login connection.</span></span>  <span data-ttu-id="2d9a4-125">Quando uma VM do Linux do Azure é criada usando as chaves de SSH para autenticação, o Azure configura Olá SSHD server toonot permitir logons de senha, somente as chaves de SSH.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-125">When an Azure Linux VM is created using SSH keys for authentication, Azure configures hello SSHD server toonot allow password logins, only SSH keys.</span></span>  <span data-ttu-id="2d9a4-126">Portanto, ao criar VMs do Linux do Azure com as chaves de SSH, você pode ajudar a saudação VM implantação segura e economizar etapa de configuração de pós-implantação típica de saudação de desabilitar as senhas no hello **sshd_config** arquivo.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-126">Therefore, by creating Azure Linux VMs with SSH keys, you can help secure hello VM deployment and save yourself hello typical post-deployment configuration step of disabling passwords in hello **sshd_config** file.</span></span>

## <a name="using-ssh-keygen"></a><span data-ttu-id="2d9a4-127">Usando ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="2d9a4-127">Using ssh-keygen</span></span>

<span data-ttu-id="2d9a4-128">Este comando cria uma senha protegida (criptografado) par de chaves de SSH utilizando RSA de 2048 bits e é comentado tooeasily identificá-lo.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-128">This command creates a password secured (encrypted) SSH key pair using 2048-bit RSA and it is commented tooeasily identify it.</span></span>  

<span data-ttu-id="2d9a4-129">SSH chaves por padrão são mantido em Olá `~/.ssh` directory.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-129">SSH keys are by default kept in hello `~/.ssh` directory.</span></span>  <span data-ttu-id="2d9a4-130">Se você não tiver um `~/.ssh` diretório, Olá `ssh-keygen` comando cria para você com hello permissões corretas.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-130">If you do not have a `~/.ssh` directory, hello `ssh-keygen` command creates it for you with hello correct permissions.</span></span>

```bash
ssh-keygen \
    -t rsa \
    -b 2048 \
    -C "azureuser@myserver" \
    -f ~/.ssh/id_rsa \
    -N mypassword
```

<span data-ttu-id="2d9a4-131">*Comando explicado*</span><span class="sxs-lookup"><span data-stu-id="2d9a4-131">*Command explained*</span></span>

<span data-ttu-id="2d9a4-132">`ssh-keygen`= Olá programa usado toocreate Olá chaves</span><span class="sxs-lookup"><span data-stu-id="2d9a4-132">`ssh-keygen` = hello program used toocreate hello keys</span></span>

<span data-ttu-id="2d9a4-133">`-t rsa`= tipo de chave toocreate Olá RSA formato [wikipedia][parênteses final](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `) 
 `-b 2048` = bits da chave de saudação</span><span class="sxs-lookup"><span data-stu-id="2d9a4-133">`-t rsa` = type of key toocreate which is hello RSA format [wikipedia][parens at end](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `)
`-b 2048` = bits of hello key</span></span>

<span data-ttu-id="2d9a4-134">`-C "azureuser@myserver"`= um comentário toohello acrescentados final de tooeasily do arquivo de chave pública de saudação identificá-lo.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-134">`-C "azureuser@myserver"` = a comment appended toohello end of hello public key file tooeasily identify it.</span></span>  <span data-ttu-id="2d9a4-135">Normalmente um email é usado como comentário hello mas você pode usar o que funciona melhor para sua infraestrutura.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-135">Normally an email is used as hello comment but you can use whatever works best for your infrastructure.</span></span>

## <a name="classic-deploy-using-asm"></a><span data-ttu-id="2d9a4-136">Implantação clássica usando `asm`</span><span class="sxs-lookup"><span data-stu-id="2d9a4-136">Classic deploy using `asm`</span></span>

<span data-ttu-id="2d9a4-137">Se você estiver usando o modelo de implantação clássico hello (`asm` modo no hello CLI), você pode usar uma chave pública SSH-RSA ou um RFC4716 formatado chave em um contêiner de pem.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-137">If you are using hello classic deployment model (`asm` mode in hello CLI), you can use an SSH-RSA public key or an RFC4716 formatted key in a pem container.</span></span>  <span data-ttu-id="2d9a4-138">chave pública SSH-RSA de saudação é o que foi criado anteriormente neste artigo usando `ssh-keygen`.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-138">hello SSH-RSA public key is what was created earlier in this article using `ssh-keygen`.</span></span>

<span data-ttu-id="2d9a4-139">toocreate um RFC4716 formatado chave de uma chave pública de SSH existente:</span><span class="sxs-lookup"><span data-stu-id="2d9a4-139">toocreate a RFC4716 formatted key from an existing SSH public key:</span></span>

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a><span data-ttu-id="2d9a4-140">Exemplo de ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="2d9a4-140">Example of ssh-keygen</span></span>

```bash
ssh-keygen -t rsa -b 2048 -C "azureuser@myserver"
Generating public/private rsa key pair.
Enter file in which toosave hello key (/home/azureuser/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/azureuser/.ssh/id_rsa.
Your public key has been saved in /home/azureuser/.ssh/id_rsa.pub.
hello key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 azureuser@myserver
hello keys randomart image is:
+--[ RSA 2048]----+
|        o o. .   |
|      E. = .o    |
|      ..o...     |
|     . o....     |
|      o S =      |
|     . + O       |
|      + = =      |
|       o +       |
|        .        |
+-----------------+
```

<span data-ttu-id="2d9a4-141">Arquivos de chave salvos:</span><span class="sxs-lookup"><span data-stu-id="2d9a4-141">Saved key files:</span></span>

`Enter file in which toosave hello key (/home/azureuser/.ssh/id_rsa): ~/.ssh/id_rsa`

<span data-ttu-id="2d9a4-142">nome do par de chaves Olá para este artigo.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-142">hello key pair name for this article.</span></span>  <span data-ttu-id="2d9a4-143">Ter um par de chaves denominado **id_rsa** saudação padrão e algumas ferramentas podem esperar Olá **id_rsa** nome de arquivo de chave privada para ter um é uma boa ideia.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-143">Having a key pair named **id_rsa** is hello default and some tools might expect hello **id_rsa** private key file name so having one is a good idea.</span></span> <span data-ttu-id="2d9a4-144">diretório de saudação `~/.ssh/` é saudação padrão local para os pares de chave SSH e arquivo de configuração SSH hello.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-144">hello directory `~/.ssh/` is hello default location for SSH key pairs and hello SSH config file.</span></span>  <span data-ttu-id="2d9a4-145">Se não for especificado com um caminho completo, `ssh-keygen` cria chaves Olá no diretório de trabalho atual do hello, não padrão de saudação `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-145">If not specified with a full path, `ssh-keygen` creates hello keys in hello current working directory, not hello default `~/.ssh`.</span></span>

<span data-ttu-id="2d9a4-146">Uma lista de saudação `~/.ssh` directory.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-146">A listing of hello `~/.ssh` directory.</span></span>

```bash
ls -al ~/.ssh
-rw------- 1 azureuser staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 azureuser staff   410 Aug 25 18:04 id_rsa.pub
```

<span data-ttu-id="2d9a4-147">Senha da chave:</span><span class="sxs-lookup"><span data-stu-id="2d9a4-147">Key Password:</span></span>

`Enter passphrase (empty for no passphrase):`

<span data-ttu-id="2d9a4-148">`ssh-keygen`refere-se tooa senha para o arquivo de chave privada hello como "senha".</span><span class="sxs-lookup"><span data-stu-id="2d9a4-148">`ssh-keygen` refers tooa password for hello private key file as "a passphrase."</span></span>  <span data-ttu-id="2d9a4-149">É *fortemente* recomendado tooadd uma chave privada de tooyour de senha.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-149">It is *strongly* recommended tooadd a password tooyour private key.</span></span> <span data-ttu-id="2d9a4-150">Sem um senha proteção Olá arquivo de chave, qualquer pessoa com arquivo hello pode usá-lo toolog no servidor tooany que tem uma chave pública correspondente hello.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-150">Without a password protecting hello key file, anyone with hello file can use it toolog in tooany server that has hello corresponding public key.</span></span> <span data-ttu-id="2d9a4-151">Adicionar uma senha (senha) oferece mais proteção caso alguém é capaz de toogain acesso tooyour arquivo de chave privada, concede a você as chaves de saudação do tempo toochange usado tooauthenticate você.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-151">Adding a password (passphrase) offers more protection in case someone is able toogain access tooyour private key file, given you time toochange hello keys used tooauthenticate you.</span></span>

## <a name="using-ssh-agent-toostore-your-private-key-password"></a><span data-ttu-id="2d9a4-152">Usando o ssh agente toostore sua senha da chave privada</span><span class="sxs-lookup"><span data-stu-id="2d9a4-152">Using ssh-agent toostore your private key password</span></span>

<span data-ttu-id="2d9a4-153">tooavoid digitar a senha do arquivo de chave privada com cada logon SSH, você pode usar `ssh-agent` toocache sua senha do arquivo de chave privada.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-153">tooavoid typing your private key file password with every SSH login, you can use `ssh-agent` toocache your private key file password.</span></span> <span data-ttu-id="2d9a4-154">Se você estiver usando um Mac, Olá OSX chaves armazena com segurança senhas de chave particular hello quando você chamar `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-154">If you are using a Mac, hello OSX Keychain securely stores hello private key passwords when you invoke `ssh-agent`.</span></span>

<span data-ttu-id="2d9a4-155">Verificar e usar ssh agente e ssh-adicionar tooinform Olá SSH sistema sobre arquivos de chave Olá para que a senha hello, não será necessário toobe usado interativamente.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-155">Verify and use ssh-agent and ssh-add tooinform hello SSH system about hello key files so that hello passphrase will not need toobe used interactively.</span></span>

```bash
eval "$(ssh-agent -s)"
```

<span data-ttu-id="2d9a4-156">Agora adicione chave privada Olá muito`ssh-agent` usando o comando Olá `ssh-add`.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-156">Now add hello private key too`ssh-agent` using hello command `ssh-add`.</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

<span data-ttu-id="2d9a4-157">senha da chave privada Olá agora é armazenada no `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-157">hello private key password is now stored in `ssh-agent`.</span></span>

## <a name="using-ssh-copy-id-toocopy-hello-key-tooan-existing-vm"></a><span data-ttu-id="2d9a4-158">Usando `ssh-copy-id` toocopy Olá tooan de chave existente VM</span><span class="sxs-lookup"><span data-stu-id="2d9a4-158">Using `ssh-copy-id` toocopy hello key tooan existing VM</span></span>
<span data-ttu-id="2d9a4-159">Se você já tiver criado uma máquina virtual, você pode instalar Olá novo SSH pública chave tooyour VM do Linux com:</span><span class="sxs-lookup"><span data-stu-id="2d9a4-159">If you have already created a VM you can install hello new SSH public key tooyour Linux VM with:</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a><span data-ttu-id="2d9a4-160">Criar e configurar um arquivo de configuração do SSH</span><span class="sxs-lookup"><span data-stu-id="2d9a4-160">Create and configure an SSH config file</span></span>

<span data-ttu-id="2d9a4-161">É uma melhor toocreate de prática recomendada e configurar um `~/.ssh/config` toospeed arquivo backup logons e para otimizar o comportamento do seu cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-161">It is a recommended best practice toocreate and configure an `~/.ssh/config` file toospeed up log ins and for optimizing your SSH client behavior.</span></span>

<span data-ttu-id="2d9a4-162">saudação de exemplo a seguir mostra uma configuração padrão.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-162">hello following example shows a standard configuration.</span></span>

### <a name="create-hello-file"></a><span data-ttu-id="2d9a4-163">Criar arquivo hello</span><span class="sxs-lookup"><span data-stu-id="2d9a4-163">Create hello file</span></span>

```bash
touch ~/.ssh/config
```

### <a name="edit-hello-file-tooadd-hello-new-ssh-configuration"></a><span data-ttu-id="2d9a4-164">Edite saudação arquivo tooadd Olá nova configuração de SSH:</span><span class="sxs-lookup"><span data-stu-id="2d9a4-164">Edit hello file tooadd hello new SSH configuration:</span></span>

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a><span data-ttu-id="2d9a4-165">Exemplo de arquivo `~/.ssh/config`:</span><span class="sxs-lookup"><span data-stu-id="2d9a4-165">Example `~/.ssh/config` file:</span></span>

```bash
# Azure Keys
Host fedora22
  Hostname 102.160.203.241
  User ahmet
# ./Azure Keys
# Default Settings
Host *
  PubkeyAuthentication=yes
  IdentitiesOnly=yes
  ServerAliveInterval=60
  ServerAliveCountMax=30
  ControlMaster auto
  ControlPath ~/.ssh/SSHConnections/ssh-%r@%h:%p
  ControlPersist 4h
  IdentityFile ~/.ssh/id_rsa
```

<span data-ttu-id="2d9a4-166">Essa configuração SSH fornece você seções para cada servidor tooenable cada toohave seu próprio par de chaves dedicado.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-166">This SSH config gives you sections for each server tooenable each toohave its own dedicated key pair.</span></span> <span data-ttu-id="2d9a4-167">Olá configurações padrão (`Host *`) são para os hosts que não corresponde a nenhum dos hosts Olá específicos acima no arquivo de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-167">hello default settings (`Host *`) are for any hosts that do not match any of hello specific hosts higher up in hello config file.</span></span>

### <a name="config-file-explained"></a><span data-ttu-id="2d9a4-168">Arquivo de configuração explicado</span><span class="sxs-lookup"><span data-stu-id="2d9a4-168">Config file explained</span></span>

<span data-ttu-id="2d9a4-169">`Host`= nome de saudação do host hello está sendo chamado em Olá terminal.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-169">`Host` = hello name of hello host being called on hello terminal.</span></span>  <span data-ttu-id="2d9a4-170">`ssh fedora22`informa `SSH` toouse valores de saudação no bloco de configurações de saudação rotulada `Host fedora22` Observação: Host pode ser qualquer rótulo lógicas para seu uso e não representam o nome de host real de qualquer servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-170">`ssh fedora22` tells `SSH` toouse hello values in hello settings block labeled `Host fedora22`  NOTE: Host can be any label that is logical for your usage and does not represent hello actual hostname of any server.</span></span>

<span data-ttu-id="2d9a4-171">`Hostname 102.160.203.241`= endereço IP de saudação ou nome DNS para o servidor de saudação que está sendo acessado.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-171">`Hostname 102.160.203.241` = hello IP address or DNS name for hello server being accessed.</span></span>

<span data-ttu-id="2d9a4-172">`User ahmet`= Olá toouse de conta de usuário remoto ao fazer logon no servidor de toohello.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-172">`User ahmet` = hello remote user account toouse when logging in toohello server.</span></span>

<span data-ttu-id="2d9a4-173">`PubKeyAuthentication yes`= informa SSH deseja toouse um toolog de chave SSH.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-173">`PubKeyAuthentication yes` = tells SSH you want toouse an SSH key toolog in.</span></span>

<span data-ttu-id="2d9a4-174">`IdentityFile /home/ahmet/.ssh/id_id_rsa`= a chave privada SSH hello e toouse correspondente de chave pública para autenticação.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-174">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = hello SSH private key and corresponding public key toouse for authentication.</span></span>

## <a name="ssh-into-linux-without-a-password"></a><span data-ttu-id="2d9a4-175">SSH no Linux sem uma senha</span><span class="sxs-lookup"><span data-stu-id="2d9a4-175">SSH into Linux without a password</span></span>

<span data-ttu-id="2d9a4-176">Agora que você tem um par de chave SSH e um arquivo de configuração de SSH configurado, será possível toolog em tooyour VM Linux rapidamente e com segurança.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-176">Now that you have an SSH key pair and a configured SSH config file, you are able toolog in tooyour Linux VM quickly and securely.</span></span> <span data-ttu-id="2d9a4-177">Olá primeira vez que você efetuar logon no servidor de tooa usando um prompts de comando Olá chave SSH você para senha Olá para esse arquivo de chave.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-177">hello first time you log in tooa server using an SSH key hello command prompts you for hello passphrase for that key file.</span></span>

```bash
ssh fedora22
```

### <a name="command-explained"></a><span data-ttu-id="2d9a4-178">Comando explicado</span><span class="sxs-lookup"><span data-stu-id="2d9a4-178">Command explained</span></span>

<span data-ttu-id="2d9a4-179">Quando `ssh fedora22` é executado SSH primeiro localiza e carrega as configurações de saudação `Host fedora22` bloco e, em seguida, carrega todos os Olá restantes Configur Olá último bloco, `Host *`.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-179">When `ssh fedora22` is executed SSH first locates and loads any settings from hello `Host fedora22` block, and then loads all hello remaining settings from hello last block, `Host *`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2d9a4-180">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2d9a4-180">Next Steps</span></span>

<span data-ttu-id="2d9a4-181">Próximo backup é toocreate VMs do Linux do Azure usando Olá novo Gerenciador de virtualização.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-181">Next up is toocreate Azure Linux VMs using hello new SSH public key.</span></span>  <span data-ttu-id="2d9a4-182">Máquinas virtuais do Azure que são criados com uma chave pública SSH como logon Olá são mais seguro que máquinas virtuais criadas com o método de logon padrão hello, as senhas.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-182">Azure VMs that are created with an SSH public key as hello login are better secured than VMs created with hello default login method, passwords.</span></span>  <span data-ttu-id="2d9a4-183">As VMs do Azure criadas com chaves SSH são por padrão configuradas com senhas desabilitadas, evitando tentativas de adivinhação por força bruta.</span><span class="sxs-lookup"><span data-stu-id="2d9a4-183">Azure VMs created using SSH keys are by default configured with passwords disabled, avoiding brute-forced guessing attempts.</span></span>

* [<span data-ttu-id="2d9a4-184">Criar uma VM do Linux segura usando um modelo do Azure</span><span class="sxs-lookup"><span data-stu-id="2d9a4-184">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="2d9a4-185">Criar uma VM do Linux segura usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="2d9a4-185">Create a secure Linux VM using hello Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="2d9a4-186">Criar uma VM do Linux segura usando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="2d9a4-186">Create a secure Linux VM using hello Azure CLI</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
