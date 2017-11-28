---
title: "par de chave aaaCreate um SSH para máquinas virtuais do Linux no Azure | Microsoft Docs"
description: "Crie um par de chaves SSH pública e privada para VMs Linux do Azure com segurança."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: 
ms.assetid: 34ae9482-da3e-4b2d-9d0d-9d672aa42498
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/08/2017
ms.author: rasquill
ms.openlocfilehash: c4c7cec77c9b48295f2a28c8179b30a4dc38a555
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-ssh-public-and-private-key-pair-for-linux-vms"></a><span data-ttu-id="c7bf6-103">Criar um par de chaves SSH pública e privada para VMs Linux</span><span class="sxs-lookup"><span data-stu-id="c7bf6-103">Create an SSH public and private key pair for Linux VMs</span></span>

<span data-ttu-id="c7bf6-104">Este artigo mostra como toogenerate um protocolo versão 2 RSA pública e privada chave SSH arquivo toouse par com VMs do Linux.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-104">This article shows you how toogenerate an SSH protocol version 2 RSA public and private key file pair toouse with Linux VMs.</span></span>  <span data-ttu-id="c7bf6-105">Com um par de chaves de SSH, você pode criar máquinas virtuais no Azure que padrão toousing as chaves de SSH para a autenticação, eliminando a necessidade de saudação para senhas toolog em.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-105">With an SSH key pair, you can create Virtual Machines on Azure that default toousing SSH keys for authentication, eliminating hello need for passwords toolog in.</span></span>  <span data-ttu-id="c7bf6-106">As senhas podem ser adivinhadas e abra suas VMs backup toorelentless tooguess de tentativas de força bruta sua senha.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-106">Passwords can be guessed, and open your VMs up toorelentless brute force attempts tooguess your password.</span></span> <span data-ttu-id="c7bf6-107">Máquinas virtuais criadas com modelos do Azure ou hello `azure-cli` pode incluir a sua chave pública SSH como parte da implantação hello, removendo a etapa de configuração de implantação de postagem de desabilitar os logons de senha para o SSH.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-107">VMs created with Azure Templates or hello `azure-cli` can include your SSH public key as part of hello deployment, removing a post deployment configuration step of disabling password logins for SSH.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="c7bf6-108">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="c7bf6-108">Quick Commands</span></span>

<span data-ttu-id="c7bf6-109">Execute Olá comandos a seguir de um shell Bash, substituindo os exemplos de saudação com suas próprias opções.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-109">Run hello following commands from a Bash shell, replacing hello examples with your own choices.</span></span>

<span data-ttu-id="c7bf6-110">O arquivo de chave pública SSH é criado por padrão em `~/.ssh/id_rsa.pub`.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-110">Your SSH public key file is by default created at `~/.ssh/id_rsa.pub`.</span></span> <span data-ttu-id="c7bf6-111">Quando solicitado usando Olá comando a seguir, você deve criar um toosecure "senha" sua chave privada.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-111">When prompted using hello following command, you should create a "passphrase" toosecure your private key.</span></span> <span data-ttu-id="c7bf6-112">(Olá senha é que uma senha usada tooencrypt sua chave privada).</span><span class="sxs-lookup"><span data-stu-id="c7bf6-112">(hello passphrase is a password used tooencrypt your private key.)</span></span>

```bash
ssh-keygen -t rsa -b 2048 
```

<span data-ttu-id="c7bf6-113">Adicionar chave Olá recém-criado muito`ssh-agent`:</span><span class="sxs-lookup"><span data-stu-id="c7bf6-113">Add hello newly created key too`ssh-agent`:</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

> [!IMPORTANT] 
> <span data-ttu-id="c7bf6-114">Olá acima comandos funcionam em sistemas operacionais de Linux de quase todas as distribuições, mas não necessariamente funcionam em contêineres, como o ambiente de saudação pode ser restringido radicalmente.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-114">hello above commands work on Linux operating systems of almost all distributions, but do not necessarily work in containers, as hello environment can be radically constrained.</span></span> 

## <a name="detailed-walkthrough"></a><span data-ttu-id="c7bf6-115">Passo a passo detalhado</span><span class="sxs-lookup"><span data-stu-id="c7bf6-115">Detailed Walkthrough</span></span>

<span data-ttu-id="c7bf6-116">Usar as chaves públicas e privadas SSH é Olá toolog de maneira mais fácil em servidores Linux de tooyour.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-116">Using SSH public and private keys is hello easiest way toolog in tooyour Linux servers.</span></span> <span data-ttu-id="c7bf6-117">[Criptografia de chave pública](https://en.wikipedia.org/wiki/Public-key_cryptography) fornece um toolog de maneira muito mais seguro em tooyour Linux ou BSD VM no Azure que senhas, que podem ser forçado bruta muito mais facilmente.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-117">[Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) provides a much more secure way toolog in tooyour Linux or BSD VM in Azure than passwords, which can be brute-forced far more easily.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c7bf6-118">Sua chave pública pode ser compartilhada com qualquer pessoa; mas apenas você (ou sua infraestrutura de segurança local) possui sua chave privada.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-118">Your public key can be shared with anyone; but only you (or your local security infrastructure) possess your private key.</span></span>  <span data-ttu-id="c7bf6-119">a chave privada SSH Olá deve ter uma [senha segura muito](https://www.xkcd.com/936/) (fonte:[xkcd.com](https://xkcd.com)) toosafeguard-lo.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-119">hello SSH private key should have a [very secure password](https://www.xkcd.com/936/) (source:[xkcd.com](https://xkcd.com)) toosafeguard it.</span></span>  <span data-ttu-id="c7bf6-120">Esta senha é a chave SSH tooaccess apenas Olá privada e **não é** senha de conta de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-120">This password is just tooaccess hello private SSH key and **is not** hello user account password.</span></span>  <span data-ttu-id="c7bf6-121">Quando você adiciona uma chave SSH tooyour senha, ele criptografa chave privada de saudação usando AES de 128 bits, para que hello chave privada é inútil sem Olá senha toodecrypt-lo.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-121">When you add a password tooyour SSH key, it encrypts hello private key using 128-bit AES, so that hello private key is useless without hello password toodecrypt it.</span></span>  <span data-ttu-id="c7bf6-122">Se um invasor roubar sua chave privada e que a chave não tem uma senha, seria capaz de toouse ou privada da chave toolog em servidores tooany que tem uma chave pública correspondente de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-122">If an attacker stole your private key and that key did not have a password, they would be able toouse that private key toolog in tooany servers that have hello corresponding public key.</span></span>  <span data-ttu-id="c7bf6-123">Se uma chave privada for protegida por senha, ela não poderá ser usada por esse invasor, o que é uma camada adicional de segurança para sua infraestrutura no Azure.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-123">If a private key is password protected it cannot be used by that attacker, providing an additional layer of security for your infrastructure on Azure.</span></span>

<span data-ttu-id="c7bf6-124">Este artigo cria o protocolo SSH versão 2 RSA públicos e privados arquivos de chave, que são recomendados para implantações de saudação Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-124">This article creates SSH protocol version 2 RSA public and private key files, which are recommended for deployments on hello Resource Manager.</span></span>  <span data-ttu-id="c7bf6-125">*SSH-rsa* as chaves são necessárias Olá [portal](https://portal.azure.com) para clássico e implantações do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-125">*ssh-rsa* keys are required on hello [portal](https://portal.azure.com) for both classic and Resource Manager deployments.</span></span>

## <a name="disable-ssh-passwords-by-using-ssh-keys"></a><span data-ttu-id="c7bf6-126">Desabilitar senhas SSH usando chaves SSH</span><span class="sxs-lookup"><span data-stu-id="c7bf6-126">Disable SSH passwords by using SSH keys</span></span>

<span data-ttu-id="c7bf6-127">O Azure requer chaves públicas e privadas de pelo menos 2048 bits em formato ssh-rsa.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-127">Azure requires at least 2048-bit, ssh-rsa format public and private keys.</span></span> <span data-ttu-id="c7bf6-128">Olá toocreate chaves use `ssh-keygen`, que faz uma série de perguntas e, em seguida, grava uma chave privada e uma chave pública correspondente.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-128">toocreate hello keys use `ssh-keygen`, which asks a series of questions and then writes a private key and a matching public key.</span></span> <span data-ttu-id="c7bf6-129">Quando uma VM do Azure é criada, a chave pública Olá é copiado muito`~/.ssh/authorized_keys`.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-129">When an Azure VM is created, hello public key is copied too`~/.ssh/authorized_keys`.</span></span>  <span data-ttu-id="c7bf6-130">As chaves de SSH no `~/.ssh/authorized_keys` são usados toochallenge Olá cliente toomatch Olá chave privada correspondente em uma conexão de logon SSH.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-130">SSH keys in `~/.ssh/authorized_keys` are used toochallenge hello client toomatch hello corresponding private key on an SSH login connection.</span></span>  <span data-ttu-id="c7bf6-131">Quando uma VM do Linux do Azure é criada usando as chaves de SSH para autenticação, o Azure configura Olá SSHD server toonot permitir logons de senha, somente as chaves de SSH.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-131">When an Azure Linux VM is created using SSH keys for authentication, Azure configures hello SSHD server toonot allow password logins, only SSH keys.</span></span>  <span data-ttu-id="c7bf6-132">Portanto, ao criar VMs do Linux do Azure com as chaves de SSH, pode ajudam na implantação de VM Olá segura e economizar etapa de configuração de pós-implantação típica de saudação de desabilitar as senhas no arquivo de configuração sshd_config hello.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-132">Therefore, by creating Azure Linux VMs with SSH keys, you can help secure hello VM deployment and save yourself hello typical post-deployment configuration step of disabling passwords in hello sshd_config config file.</span></span>

## <a name="using-ssh-keygen"></a><span data-ttu-id="c7bf6-133">Usando ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="c7bf6-133">Using ssh-keygen</span></span>

<span data-ttu-id="c7bf6-134">Este comando cria uma senha protegida (criptografado) par de chaves de SSH utilizando RSA de 2048 bits e é comentado tooeasily identificá-lo.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-134">This command creates a password secured (encrypted) SSH key pair using 2048-bit RSA and it is commented tooeasily identify it.</span></span>  

<span data-ttu-id="c7bf6-135">SSH chaves por padrão são mantido em Olá `~/.ssh` directory.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-135">SSH keys are by default kept in hello `~/.ssh` directory.</span></span>  <span data-ttu-id="c7bf6-136">Se você não tiver um `~/.ssh` diretório, Olá `ssh-keygen` comando cria para você com hello permissões corretas.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-136">If you do not have a `~/.ssh` directory, hello `ssh-keygen` command creates it for you with hello correct permissions.</span></span>

```bash
ssh-keygen \
-t rsa \
-b 2048 
```

<span data-ttu-id="c7bf6-137">*Comando explicado*</span><span class="sxs-lookup"><span data-stu-id="c7bf6-137">*Command explained*</span></span>

<span data-ttu-id="c7bf6-138">`ssh-keygen`= Olá programa usado toocreate Olá chaves</span><span class="sxs-lookup"><span data-stu-id="c7bf6-138">`ssh-keygen` = hello program used toocreate hello keys</span></span>

<span data-ttu-id="c7bf6-139">`-t rsa`= tipo de chave toocreate Olá RSA formato [wikipedia](https://en.wikipedia.org/wiki/RSA_(cryptosystem)</span><span class="sxs-lookup"><span data-stu-id="c7bf6-139">`-t rsa` = type of key toocreate which is hello RSA format [wikipedia](https://en.wikipedia.org/wiki/RSA_(cryptosystem)</span></span>

<span data-ttu-id="c7bf6-140">`-b 2048`= bits da chave de saudação</span><span class="sxs-lookup"><span data-stu-id="c7bf6-140">`-b 2048` = bits of hello key</span></span>


## <a name="classic-portal-and-x509-certs"></a><span data-ttu-id="c7bf6-141">Portal clássico e certificados x.509</span><span class="sxs-lookup"><span data-stu-id="c7bf6-141">Classic portal and X.509 certs</span></span>

<span data-ttu-id="c7bf6-142">Se você estiver usando hello Azure [portal clássico](https://manage.windowsazure.com/), ele requer certificados x. 509 para chaves SSH hello.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-142">If you are using hello Azure [classic portal](https://manage.windowsazure.com/), it requires X.509 certs for hello SSH keys.</span></span>  <span data-ttu-id="c7bf6-143">Outros tipos de chaves públicas SSH não são permitidos. Elas *devem* ser certificados x.509.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-143">No other types of SSH public keys are allowed, they *must* be X.509 certs.</span></span>

<span data-ttu-id="c7bf6-144">toocreate um certificado x. 509 de sua chave privada do SSH-RSA existente:</span><span class="sxs-lookup"><span data-stu-id="c7bf6-144">toocreate an X.509 cert from your existing SSH-RSA private key:</span></span>

```bash
openssl req -x509 \
-key ~/.ssh/id_rsa \
-nodes \
-days 365 \
-newkey rsa:2048 \
-out ~/.ssh/id_rsa.pem
```

## <a name="classic-deploy-using-asm"></a><span data-ttu-id="c7bf6-145">Implantação clássica usando `asm`</span><span class="sxs-lookup"><span data-stu-id="c7bf6-145">Classic deploy using `asm`</span></span>

<span data-ttu-id="c7bf6-146">Se você estiver usando clássico Olá implantar modelo (CLI de gerenciamento de serviço do Azure `asm`), você pode usar uma chave pública SSH-RSA ou um RFC4716 formatado chave em um **. PEM** contêiner.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-146">If you are using hello classic deploy model (Azure service management CLI `asm`), you can use an SSH-RSA public key or an RFC4716 formatted key in a **.pem** container.</span></span>  <span data-ttu-id="c7bf6-147">chave pública SSH-RSA de saudação é o que foi criado anteriormente neste artigo usando `ssh-keygen`.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-147">hello SSH-RSA public key is what was created earlier in this article using `ssh-keygen`.</span></span>

<span data-ttu-id="c7bf6-148">toocreate um RFC4716 formatado chave de uma chave pública de SSH existente:</span><span class="sxs-lookup"><span data-stu-id="c7bf6-148">toocreate a RFC4716 formatted key from an existing SSH public key:</span></span>

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a><span data-ttu-id="c7bf6-149">Exemplo de ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="c7bf6-149">Example of ssh-keygen</span></span>

```bash
ssh-keygen -t rsa -b 2048 -C "ahmet@myserver"
Generating public/private rsa key pair.
Enter file in which toosave hello key (/home/ahmet/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/ahmet/.ssh/id_rsa.
Your public key has been saved in /home/ahmet/.ssh/id_rsa.pub.
hello key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 ahmet@myserver
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

<span data-ttu-id="c7bf6-150">Arquivos de chave salvos:</span><span class="sxs-lookup"><span data-stu-id="c7bf6-150">Saved key files:</span></span>

`Enter file in which toosave hello key (/home/ahmet/.ssh/id_rsa): ~/.ssh/id_rsa`

<span data-ttu-id="c7bf6-151">nome do par de chaves Olá para este artigo.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-151">hello key pair name for this article.</span></span>  <span data-ttu-id="c7bf6-152">Ter um par de chaves denominado **id_rsa** saudação padrão e algumas ferramentas podem esperar Olá **id_rsa** nome de arquivo de chave privada para ter um é uma boa ideia.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-152">Having a key pair named **id_rsa** is hello default and some tools might expect hello **id_rsa** private key file name so having one is a good idea.</span></span> <span data-ttu-id="c7bf6-153">diretório de saudação `~/.ssh/` é saudação padrão local para os pares de chave SSH e arquivo de configuração SSH hello.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-153">hello directory `~/.ssh/` is hello default location for SSH key pairs and hello SSH config file.</span></span>  <span data-ttu-id="c7bf6-154">Se não for especificado com um caminho completo, `ssh-keygen` será criar chaves Olá no diretório de trabalho atual hello, Olá não padrão `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-154">If not specified with a full path, `ssh-keygen` will create hello keys in hello current working directory, not hello default `~/.ssh`.</span></span>

<span data-ttu-id="c7bf6-155">Uma lista de saudação `~/.ssh` directory.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-155">A listing of hello `~/.ssh` directory.</span></span>

```bash
ls -al ~/.ssh
-rw------- 1 ahmet staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 ahmet staff   410 Aug 25 18:04 rsa.pub
```

<span data-ttu-id="c7bf6-156">Senha da chave:</span><span class="sxs-lookup"><span data-stu-id="c7bf6-156">Key Password:</span></span>

`Enter passphrase (empty for no passphrase):`

<span data-ttu-id="c7bf6-157">`ssh-keygen`refere-se a chave privada do hello tooa senha usada tooencrypt como "senha".</span><span class="sxs-lookup"><span data-stu-id="c7bf6-157">`ssh-keygen` refers tooa password used tooencrypt hello private key as "a passphrase."</span></span>  <span data-ttu-id="c7bf6-158">É *fortemente* recomendado tooadd pares de chave de tooyour uma frase secreta.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-158">It is *strongly* recommended tooadd a passphrase tooyour key pairs.</span></span> <span data-ttu-id="c7bf6-159">Sem uma frase secreta proteção Olá chave privada, qualquer pessoa com o arquivo de chave Olá pode usá-lo toolog no servidor tooany que tem uma chave pública correspondente hello.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-159">Without a passphrase protecting hello private key, anyone with hello key file can use it toolog in tooany server that has hello corresponding public key.</span></span> <span data-ttu-id="c7bf6-160">Adicionar uma frase secreta oferece mais proteção caso alguém é capaz de toogain acesso tooyour arquivo de chave privada, fornecendo chaves de saudação do tempo toochange usado tooauthenticate você.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-160">Adding a passphrase offers more protection in case someone is able toogain access tooyour private key file, giving you time toochange hello keys used tooauthenticate you.</span></span>

## <a name="using-ssh-agent-toostore-your-private-key-password"></a><span data-ttu-id="c7bf6-161">Usando o ssh agente toostore sua senha da chave privada</span><span class="sxs-lookup"><span data-stu-id="c7bf6-161">Using ssh-agent toostore your private key password</span></span>

<span data-ttu-id="c7bf6-162">senha do arquivo tooavoid digitar sua chave privada com cada logon SSH, você pode usar `ssh-agent` toocache sua senha do arquivo de chave privada.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-162">tooavoid typing your private key file passphrase with every SSH login, you can use `ssh-agent` toocache your private key file password.</span></span> <span data-ttu-id="c7bf6-163">Se você estiver usando um Mac, Olá OSX chaves armazena com segurança senhas de chave particular hello quando você chamar `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-163">If you are using a Mac, hello OSX Keychain securely stores hello private key passwords when you invoke `ssh-agent`.</span></span>

<span data-ttu-id="c7bf6-164">Verificar e usar `ssh-agent` e `ssh-add` tooinform Olá sistema SSH sobre arquivos de chave Olá para que a senha hello, não será necessário toobe usado interativamente.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-164">Verify and use `ssh-agent` and `ssh-add` tooinform hello SSH system about hello key files so that hello passphrase will not need toobe used interactively.</span></span>

```bash
eval "$(ssh-agent -s)"
```

<span data-ttu-id="c7bf6-165">Agora adicione chave privada Olá muito`ssh-agent` usando o comando Olá `ssh-add`.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-165">Now add hello private key too`ssh-agent` using hello command `ssh-add`.</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

<span data-ttu-id="c7bf6-166">senha da chave privada Olá agora é armazenada no `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-166">hello private key password is now stored in `ssh-agent`.</span></span>

## <a name="using-ssh-copy-id-tooinstall-hello-new-key"></a><span data-ttu-id="c7bf6-167">Usando `ssh-copy-id` nova chave de saudação tooinstall</span><span class="sxs-lookup"><span data-stu-id="c7bf6-167">Using `ssh-copy-id` tooinstall hello new key</span></span>
<span data-ttu-id="c7bf6-168">Se você já tiver criado uma máquina virtual, você pode instalar Olá novo SSH pública chave tooyour VM do Linux com hello comando a seguir, substituindo o nome de usuário do hello VM e o endereço do servidor de saudação com seus próprios valores:</span><span class="sxs-lookup"><span data-stu-id="c7bf6-168">If you have already created a VM you can install hello new SSH public key tooyour Linux VM with hello following command, replacing hello VM username and hello server address with your own values:</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a><span data-ttu-id="c7bf6-169">Criar e configurar um arquivo de configuração do SSH</span><span class="sxs-lookup"><span data-stu-id="c7bf6-169">Create and configure an SSH config file</span></span>

<span data-ttu-id="c7bf6-170">Ele é um toocreate de prática recomendada e configurar um `~/.ssh/config` toospeed arquivo backup logons e para otimizar o comportamento do seu cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-170">It is a best practice toocreate and configure an `~/.ssh/config` file toospeed up log ins and for optimizing your SSH client behavior.</span></span>

<span data-ttu-id="c7bf6-171">saudação de exemplo a seguir mostra uma configuração padrão.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-171">hello following example shows a standard configuration.</span></span>

### <a name="create-hello-file"></a><span data-ttu-id="c7bf6-172">Criar arquivo hello</span><span class="sxs-lookup"><span data-stu-id="c7bf6-172">Create hello file</span></span>

```bash
touch ~/.ssh/config
```

### <a name="edit-hello-file-tooadd-hello-new-ssh-configuration"></a><span data-ttu-id="c7bf6-173">Edite saudação arquivo tooadd Olá nova configuração de SSH:</span><span class="sxs-lookup"><span data-stu-id="c7bf6-173">Edit hello file tooadd hello new SSH configuration:</span></span>

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a><span data-ttu-id="c7bf6-174">Exemplo de arquivo `~/.ssh/config`:</span><span class="sxs-lookup"><span data-stu-id="c7bf6-174">Example `~/.ssh/config` file:</span></span>

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

<span data-ttu-id="c7bf6-175">Essa configuração SSH fornece você seções para cada servidor tooenable cada toohave seu próprio par de chaves dedicado.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-175">This SSH config gives you sections for each server tooenable each toohave its own dedicated key pair.</span></span> <span data-ttu-id="c7bf6-176">Olá configurações padrão (`Host *`) são para os hosts que não corresponde a nenhum dos hosts Olá específicos acima no arquivo de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-176">hello default settings (`Host *`) are for any hosts that do not match any of hello specific hosts higher up in hello config file.</span></span>

### <a name="config-file-explained"></a><span data-ttu-id="c7bf6-177">Arquivo de configuração explicado</span><span class="sxs-lookup"><span data-stu-id="c7bf6-177">Config file explained</span></span>

<span data-ttu-id="c7bf6-178">`Host`= nome de saudação do host hello está sendo chamado em Olá terminal.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-178">`Host` = hello name of hello host being called on hello terminal.</span></span>  <span data-ttu-id="c7bf6-179">`ssh fedora22`informa `SSH` toouse valores de saudação no bloco de configurações de saudação rotulada `Host fedora22` Observação: Host pode ser qualquer rótulo lógicas para seu uso e não representam o nome de host real de qualquer servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-179">`ssh fedora22` tells `SSH` toouse hello values in hello settings block labeled `Host fedora22`  NOTE: Host can be any label that is logical for your usage and does not represent hello actual hostname of any server.</span></span>

<span data-ttu-id="c7bf6-180">`Hostname 102.160.203.241`= endereço IP de saudação ou nome DNS para o servidor de saudação que está sendo acessado.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-180">`Hostname 102.160.203.241` = hello IP address or DNS name for hello server being accessed.</span></span>

<span data-ttu-id="c7bf6-181">`User ahmet`= Olá toouse de conta de usuário remoto ao fazer logon no servidor de toohello.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-181">`User ahmet` = hello remote user account toouse when logging in toohello server.</span></span>

<span data-ttu-id="c7bf6-182">`PubKeyAuthentication yes`= informa SSH deseja toouse um toolog de chave SSH.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-182">`PubKeyAuthentication yes` = tells SSH you want toouse an SSH key toolog in.</span></span>

<span data-ttu-id="c7bf6-183">`IdentityFile /home/ahmet/.ssh/id_id_rsa`= a chave privada SSH hello e toouse correspondente de chave pública para autenticação.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-183">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = hello SSH private key and corresponding public key toouse for authentication.</span></span>

## <a name="ssh-into-linux-without-a-password"></a><span data-ttu-id="c7bf6-184">SSH no Linux sem uma senha</span><span class="sxs-lookup"><span data-stu-id="c7bf6-184">SSH into Linux without a password</span></span>

<span data-ttu-id="c7bf6-185">Agora que você tem um par de chave SSH e um arquivo de configuração de SSH configurado, será possível toolog em tooyour VM Linux rapidamente e com segurança.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-185">Now that you have an SSH key pair and a configured SSH config file, you are able toolog in tooyour Linux VM quickly and securely.</span></span> <span data-ttu-id="c7bf6-186">Olá primeira vez que você efetuar logon no servidor de tooa usando um prompts de comando Olá chave SSH você para senha Olá para esse arquivo de chave.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-186">hello first time you log in tooa server using an SSH key hello command prompts you for hello passphrase for that key file.</span></span>

```bash
ssh fedora22
```

### <a name="command-explained"></a><span data-ttu-id="c7bf6-187">Comando explicado</span><span class="sxs-lookup"><span data-stu-id="c7bf6-187">Command explained</span></span>

<span data-ttu-id="c7bf6-188">Quando `ssh fedora22` é executado SSH primeiro localiza e carrega as configurações de saudação `Host fedora22` bloco e, em seguida, carrega todos os Olá restantes Configur Olá último bloco, `Host *`.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-188">When `ssh fedora22` is executed SSH first locates and loads any settings from hello `Host fedora22` block, and then loads all hello remaining settings from hello last block, `Host *`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7bf6-189">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c7bf6-189">Next Steps</span></span>

<span data-ttu-id="c7bf6-190">Próximo backup é toocreate VMs do Linux do Azure usando Olá novo Gerenciador de virtualização.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-190">Next up is toocreate Azure Linux VMs using hello new SSH public key.</span></span>  <span data-ttu-id="c7bf6-191">Máquinas virtuais do Azure que são criados com uma chave pública SSH como logon Olá são mais seguro que máquinas virtuais criadas com o método de logon padrão hello, as senhas.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-191">Azure VMs that are created with an SSH public key as hello login are better secured than VMs created with hello default login method, passwords.</span></span>  <span data-ttu-id="c7bf6-192">As VMs do Azure criadas com chaves SSH são por padrão configuradas com senhas desabilitadas, evitando tentativas de adivinhação por força bruta.</span><span class="sxs-lookup"><span data-stu-id="c7bf6-192">Azure VMs created using SSH keys are by default configured with passwords disabled, avoiding brute-forced guessing attempts.</span></span> <span data-ttu-id="c7bf6-193">Se você precisa de mais ajuda na criação de par de chaves de SSH ou exige certificados adicionais, por exemplo, para uso com o portal clássico do hello, consulte [detalhadas certificados e pares de chave SSH do etapas toocreate](create-ssh-keys-detailed.md).</span><span class="sxs-lookup"><span data-stu-id="c7bf6-193">If you need more assistance in creating your SSH key pair or require additional certificates, such as for use with hello classic portal, see [Detailed steps toocreate SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

* [<span data-ttu-id="c7bf6-194">Criar uma VM do Linux segura usando um modelo do Azure</span><span class="sxs-lookup"><span data-stu-id="c7bf6-194">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="c7bf6-195">Criar uma VM do Linux segura usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c7bf6-195">Create a secure Linux VM using hello Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="c7bf6-196">Criar uma VM do Linux segura usando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="c7bf6-196">Create a secure Linux VM using hello Azure CLI</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
