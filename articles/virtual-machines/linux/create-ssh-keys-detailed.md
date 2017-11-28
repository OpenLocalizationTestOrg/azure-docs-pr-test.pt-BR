---
title: Etapas detalhadas para criar um par de chaves SSH para VMs Linux no Azure | Microsoft Docs
description: "Aprenda as etapas adicionais para criar um par de chaves SSH pública e privada para VMs Linux no Azure, junto com certificados específicos para diversos casos de uso."
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
ms.openlocfilehash: d4548c6f21d04effd57ea36e4fc0d15f77568903
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="detailed-walk-through-to-create-an-ssh-key-pair-and-additional-certificates-for-a-linux-vm-in-azure"></a><span data-ttu-id="85f1d-103">Passo a passo detalhado para criar um par de chaves SSH e certificados adicionais para uma VM Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="85f1d-103">Detailed walk through to create an SSH key pair and additional certificates for a Linux VM in Azure</span></span>
<span data-ttu-id="85f1d-104">Com um par de chaves SSH, você pode criar máquinas virtuais no Azure que tenham como padrão o uso de chaves SSH para autenticação, eliminando a necessidade de senhas para fazer logon.</span><span class="sxs-lookup"><span data-stu-id="85f1d-104">With an SSH key pair, you can create Virtual Machines on Azure that default to using SSH keys for authentication, eliminating the need for passwords to log in.</span></span> <span data-ttu-id="85f1d-105">As senhas podem ser adivinhadas e podem abrir suas VMs para tentativas de uso contínuo de força bruta para adivinhá-las.</span><span class="sxs-lookup"><span data-stu-id="85f1d-105">Passwords can be guessed, and open your VMs up to relentless brute force attempts to guess your password.</span></span> <span data-ttu-id="85f1d-106">As VMs criadas com a CLI do Azure ou com modelos do Resource Manager podem incluir sua chave pública SSH como parte da implantação, removendo uma etapa de configuração pós-implantação que consiste na desabilitação de logons com senha para SSH.</span><span class="sxs-lookup"><span data-stu-id="85f1d-106">VMs created with the Azure CLI or Resource Manager templates can include your SSH public key as part of the deployment, removing a post deployment configuration step of disabling password logins for SSH.</span></span> <span data-ttu-id="85f1d-107">Este artigo fornece etapas detalhadas e exemplos adicionais de geração de certificados, por exemplo, para uso com máquinas virtuais Linux.</span><span class="sxs-lookup"><span data-stu-id="85f1d-107">This article provides detailed steps and additional examples of generating certificates, such as for use with Linux virtual machines.</span></span> <span data-ttu-id="85f1d-108">Se você quiser criar e usar rapidamente um par de chaves SSH, confira [Como criar um par de chaves SSH pública e privada para VMs Linux no Azure](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="85f1d-108">If you want to quickly create and use an SSH key pair, see [How to create an SSH public and private key pair for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

## <a name="understanding-ssh-keys"></a><span data-ttu-id="85f1d-109">Noções básicas das chaves SSH</span><span class="sxs-lookup"><span data-stu-id="85f1d-109">Understanding SSH keys</span></span>

<span data-ttu-id="85f1d-110">Usar as chaves públicas e privadas do SSH é a maneira mais fácil de fazer logon em servidores Linux.</span><span class="sxs-lookup"><span data-stu-id="85f1d-110">Using SSH public and private keys is the easiest way to log in to your Linux servers.</span></span> <span data-ttu-id="85f1d-111">[criptografia de chave pública](https://en.wikipedia.org/wiki/Public-key_cryptography) fornece uma maneira muito mais segura de fazer logon na VM BSD ou do Linux no Azure do que as senhas, que podem ser obtidas por força bruta muito mais facilmente.</span><span class="sxs-lookup"><span data-stu-id="85f1d-111">[Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) provides a much more secure way to log in to your Linux or BSD VM in Azure than passwords, which can be brute-forced far more easily.</span></span>

<span data-ttu-id="85f1d-112">Sua chave pública pode ser compartilhada com qualquer pessoa; mas apenas você (ou sua infraestrutura de segurança local) possui sua chave privada.</span><span class="sxs-lookup"><span data-stu-id="85f1d-112">Your public key can be shared with anyone; but only you (or your local security infrastructure) possess your private key.</span></span>  <span data-ttu-id="85f1d-113">A chave privada SSH deve ter uma [senha bastante segura](https://www.xkcd.com/936/)(fonte:[xkcd.com](https://xkcd.com)) para protegê-la.</span><span class="sxs-lookup"><span data-stu-id="85f1d-113">The SSH private key should have a [very secure password](https://www.xkcd.com/936/) (source:[xkcd.com](https://xkcd.com)) to safeguard it.</span></span>  <span data-ttu-id="85f1d-114">Esta senha serve apenas para acessar o arquivo de chave SSH privada e **não é** a senha da conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="85f1d-114">This password is just to access the private SSH key file and **is not** the user account password.</span></span>  <span data-ttu-id="85f1d-115">Quando você adiciona uma senha para a chave SSH, ela criptografa a chave privada usando AES de 128 bits, para que a chave privada seja inútil sem a senha para descriptografá-la.</span><span class="sxs-lookup"><span data-stu-id="85f1d-115">When you add a password to your SSH key, it encrypts the private key using 128-bit AES, so that the private key is useless without the password to decrypt it.</span></span>  <span data-ttu-id="85f1d-116">Se um invasor roubasse sua chave privada e se ela não tivesse uma senha, ele poderia usar essa chave privada para fazer logon em qualquer servidor com a chave pública correspondente.</span><span class="sxs-lookup"><span data-stu-id="85f1d-116">If an attacker stole your private key and that key did not have a password, they would be able to use that private key to log in to any servers that have the corresponding public key.</span></span>  <span data-ttu-id="85f1d-117">Se uma chave privada for protegida por senha, ela não poderá ser usada por esse invasor, o que é uma camada adicional de segurança para sua infraestrutura no Azure.</span><span class="sxs-lookup"><span data-stu-id="85f1d-117">If a private key is password protected it cannot be used by that attacker, providing an additional layer of security for your infrastructure on Azure.</span></span>

<span data-ttu-id="85f1d-118">Este artigo cria um par de arquivos de chave pública e privada RSA do protocolo SSH versão 2 (também chamadas de chaves "ssh-rsa"), recomendadas para implantações com o Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="85f1d-118">This article creates an SSH protocol version 2 RSA public and private key file pair (also referred to as "ssh-rsa" keys), which are recommended for deployments with Azure Resource Manager.</span></span> <span data-ttu-id="85f1d-119">Chaves *SSH-rsa* são necessárias no [portal](https://portal.azure.com) para implantações clássicas e do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="85f1d-119">*ssh-rsa* keys are required on the [portal](https://portal.azure.com) for both classic and Resource Manager deployments.</span></span>

## <a name="ssh-keys-use-and-benefits"></a><span data-ttu-id="85f1d-120">Benefícios e uso das chaves SSH</span><span class="sxs-lookup"><span data-stu-id="85f1d-120">SSH keys use and benefits</span></span>

<span data-ttu-id="85f1d-121">O Azure exige pelo menos chaves pública e privada no formato RSA de 2048 bits,protocolo SSH versão 2; o arquivo de chave pública tem o formato de contêiner `.pub`.</span><span class="sxs-lookup"><span data-stu-id="85f1d-121">Azure requires at least 2048-bit, SSH protocol version 2 RSA format public and private keys; the public key file has the `.pub` container format.</span></span> <span data-ttu-id="85f1d-122">Para criar as chaves, use `ssh-keygen`, que faz uma série de perguntas e, em seguida, grava uma chave privada e uma chave pública correspondente.</span><span class="sxs-lookup"><span data-stu-id="85f1d-122">To create the keys use `ssh-keygen`, which asks a series of questions and then writes a private key and a matching public key.</span></span> <span data-ttu-id="85f1d-123">Quando uma VM do Azure é criada, o Azure copia a chave pública para a pasta `~/.ssh/authorized_keys` na VM.</span><span class="sxs-lookup"><span data-stu-id="85f1d-123">When an Azure VM is created, Azure copies the public key to the `~/.ssh/authorized_keys` folder on the VM.</span></span> <span data-ttu-id="85f1d-124">As chaves SSH no `~/.ssh/authorized_keys` são usadas para desafiar o cliente para coincidir com a chave privada correspondente em uma conexão de logon SSH.</span><span class="sxs-lookup"><span data-stu-id="85f1d-124">SSH keys in `~/.ssh/authorized_keys` are used to challenge the client to match the corresponding private key on an SSH login connection.</span></span>  <span data-ttu-id="85f1d-125">Quando uma VM Linux do Azure é criada usando chaves SSH para autenticação, o Azure configura o servidor SSHD para não permitir logons com senha, apenas com chaves SSH.</span><span class="sxs-lookup"><span data-stu-id="85f1d-125">When an Azure Linux VM is created using SSH keys for authentication, Azure configures the SSHD server to not allow password logins, only SSH keys.</span></span>  <span data-ttu-id="85f1d-126">Portanto, ao criar VMs Linux do Azure com chaves SSH, você pode ajudar a proteger a implantação de VM e evitar a etapa de configuração pós-implantação típica de desabilitar as senhas no arquivo de **sshd_config**.</span><span class="sxs-lookup"><span data-stu-id="85f1d-126">Therefore, by creating Azure Linux VMs with SSH keys, you can help secure the VM deployment and save yourself the typical post-deployment configuration step of disabling passwords in the **sshd_config** file.</span></span>

## <a name="using-ssh-keygen"></a><span data-ttu-id="85f1d-127">Usando ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="85f1d-127">Using ssh-keygen</span></span>

<span data-ttu-id="85f1d-128">Esse comando cria um par de chaves SSH (criptografado) protegido por senha usando o RSA de 2048 bits e é comentado para identificá-lo facilmente.</span><span class="sxs-lookup"><span data-stu-id="85f1d-128">This command creates a password secured (encrypted) SSH key pair using 2048-bit RSA and it is commented to easily identify it.</span></span>  

<span data-ttu-id="85f1d-129">As chaves SSH são mantidas por padrão no diretório `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="85f1d-129">SSH keys are by default kept in the `~/.ssh` directory.</span></span>  <span data-ttu-id="85f1d-130">Se você não tiver um diretório `~/.ssh`, o comando `ssh-keygen` o criará para você com as permissões corretas.</span><span class="sxs-lookup"><span data-stu-id="85f1d-130">If you do not have a `~/.ssh` directory, the `ssh-keygen` command creates it for you with the correct permissions.</span></span>

```bash
ssh-keygen \
    -t rsa \
    -b 2048 \
    -C "azureuser@myserver" \
    -f ~/.ssh/id_rsa \
    -N mypassword
```

<span data-ttu-id="85f1d-131">*Comando explicado*</span><span class="sxs-lookup"><span data-stu-id="85f1d-131">*Command explained*</span></span>

<span data-ttu-id="85f1d-132">`ssh-keygen` = programa usado para criar as chaves</span><span class="sxs-lookup"><span data-stu-id="85f1d-132">`ssh-keygen` = the program used to create the keys</span></span>

<span data-ttu-id="85f1d-133">`-t rsa` = tipo de chave para criar que é o formato RSA [wikipédia][parênteses final](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `) 
 `-b 2048` = bits da chave</span><span class="sxs-lookup"><span data-stu-id="85f1d-133">`-t rsa` = type of key to create which is the RSA format [wikipedia][parens at end](`https://en.wikipedia.org/wiki/RSA_(cryptosystem) `)
`-b 2048` = bits of the key</span></span>

<span data-ttu-id="85f1d-134">`-C "azureuser@myserver"` = um comentário acrescentado ao fim do arquivo de chave pública para identificá-lo facilmente.</span><span class="sxs-lookup"><span data-stu-id="85f1d-134">`-C "azureuser@myserver"` = a comment appended to the end of the public key file to easily identify it.</span></span>  <span data-ttu-id="85f1d-135">Normalmente, um email é usado como o comentário, mas você pode usar o que funcionar melhor para sua infraestrutura.</span><span class="sxs-lookup"><span data-stu-id="85f1d-135">Normally an email is used as the comment but you can use whatever works best for your infrastructure.</span></span>

## <a name="classic-deploy-using-asm"></a><span data-ttu-id="85f1d-136">Implantação clássica usando `asm`</span><span class="sxs-lookup"><span data-stu-id="85f1d-136">Classic deploy using `asm`</span></span>

<span data-ttu-id="85f1d-137">Se estiver usando o modelo de implantação clássica (modo `asm` na CLI), você poderá usar uma chave pública SSH-RSA ou uma chave formatada como RFC4716 em um contêiner pem.</span><span class="sxs-lookup"><span data-stu-id="85f1d-137">If you are using the classic deployment model (`asm` mode in the CLI), you can use an SSH-RSA public key or an RFC4716 formatted key in a pem container.</span></span>  <span data-ttu-id="85f1d-138">A chave pública SSH-RSA é a que foi criada anteriormente neste artigo usando `ssh-keygen`.</span><span class="sxs-lookup"><span data-stu-id="85f1d-138">The SSH-RSA public key is what was created earlier in this article using `ssh-keygen`.</span></span>

<span data-ttu-id="85f1d-139">Para criar uma chave formatada RFC4716 com base em uma chave pública SSH existente:</span><span class="sxs-lookup"><span data-stu-id="85f1d-139">To create a RFC4716 formatted key from an existing SSH public key:</span></span>

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a><span data-ttu-id="85f1d-140">Exemplo de ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="85f1d-140">Example of ssh-keygen</span></span>

```bash
ssh-keygen -t rsa -b 2048 -C "azureuser@myserver"
Generating public/private rsa key pair.
Enter file in which to save the key (/home/azureuser/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/azureuser/.ssh/id_rsa.
Your public key has been saved in /home/azureuser/.ssh/id_rsa.pub.
The key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 azureuser@myserver
The keys randomart image is:
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

<span data-ttu-id="85f1d-141">Arquivos de chave salvos:</span><span class="sxs-lookup"><span data-stu-id="85f1d-141">Saved key files:</span></span>

`Enter file in which to save the key (/home/azureuser/.ssh/id_rsa): ~/.ssh/id_rsa`

<span data-ttu-id="85f1d-142">O nome do par de chaves para este artigo.</span><span class="sxs-lookup"><span data-stu-id="85f1d-142">The key pair name for this article.</span></span>  <span data-ttu-id="85f1d-143">Ter um par de chaves denominado **id_rsa** é o padrão e algumas ferramentas podem esperar o nome de arquivo da chave privada **id_rsa**, portanto, ter um é uma boa ideia.</span><span class="sxs-lookup"><span data-stu-id="85f1d-143">Having a key pair named **id_rsa** is the default and some tools might expect the **id_rsa** private key file name so having one is a good idea.</span></span> <span data-ttu-id="85f1d-144">O diretório `~/.ssh/` é o local padrão para os pares de chave SSH e o arquivo de configuração SSH.</span><span class="sxs-lookup"><span data-stu-id="85f1d-144">The directory `~/.ssh/` is the default location for SSH key pairs and the SSH config file.</span></span>  <span data-ttu-id="85f1d-145">Se não for especificado com um caminho completo, `ssh-keygen` criará as chaves no diretório de trabalho atual e não o `~/.ssh` padrão.</span><span class="sxs-lookup"><span data-stu-id="85f1d-145">If not specified with a full path, `ssh-keygen` creates the keys in the current working directory, not the default `~/.ssh`.</span></span>

<span data-ttu-id="85f1d-146">Uma listagem do diretório `~/.ssh` .</span><span class="sxs-lookup"><span data-stu-id="85f1d-146">A listing of the `~/.ssh` directory.</span></span>

```bash
ls -al ~/.ssh
-rw------- 1 azureuser staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 azureuser staff   410 Aug 25 18:04 id_rsa.pub
```

<span data-ttu-id="85f1d-147">Senha da chave:</span><span class="sxs-lookup"><span data-stu-id="85f1d-147">Key Password:</span></span>

`Enter passphrase (empty for no passphrase):`

<span data-ttu-id="85f1d-148">`ssh-keygen` refere-se a uma senha usada para o arquivo de chave privada como uma "senha".</span><span class="sxs-lookup"><span data-stu-id="85f1d-148">`ssh-keygen` refers to a password for the private key file as "a passphrase."</span></span>  <span data-ttu-id="85f1d-149">É *altamente* recomendável adicionar uma senha aos seus pares de chave.</span><span class="sxs-lookup"><span data-stu-id="85f1d-149">It is *strongly* recommended to add a password to your private key.</span></span> <span data-ttu-id="85f1d-150">Sem uma senha para proteger o par de chaves, qualquer pessoa com o arquivo poderá usá-lo para fazer logon em qualquer servidor com a chave pública correspondente.</span><span class="sxs-lookup"><span data-stu-id="85f1d-150">Without a password protecting the key file, anyone with the file can use it to log in to any server that has the corresponding public key.</span></span> <span data-ttu-id="85f1d-151">Portanto, adicionar uma senha oferece mais proteção no caso de alguém obter acesso a seu arquivo de chave privada, dando-lhe tempo para alterar as chaves usadas para autenticá-lo.</span><span class="sxs-lookup"><span data-stu-id="85f1d-151">Adding a password (passphrase) offers more protection in case someone is able to gain access to your private key file, given you time to change the keys used to authenticate you.</span></span>

## <a name="using-ssh-agent-to-store-your-private-key-password"></a><span data-ttu-id="85f1d-152">Usando ssh-agent para armazenar sua senha de chave privada</span><span class="sxs-lookup"><span data-stu-id="85f1d-152">Using ssh-agent to store your private key password</span></span>

<span data-ttu-id="85f1d-153">Para evitar a digitação da senha do arquivo de chave privada em cada logon do SSH, você poderá usar `ssh-agent` para armazenar em cache a senha do arquivo de chave privada.</span><span class="sxs-lookup"><span data-stu-id="85f1d-153">To avoid typing your private key file password with every SSH login, you can use `ssh-agent` to cache your private key file password.</span></span> <span data-ttu-id="85f1d-154">Se você estiver usando um Mac, a cadeia de chaves do OSX armazena com segurança suas senhas de chave privadas quando `ssh-agent`é chamado.</span><span class="sxs-lookup"><span data-stu-id="85f1d-154">If you are using a Mac, the OSX Keychain securely stores the private key passwords when you invoke `ssh-agent`.</span></span>

<span data-ttu-id="85f1d-155">Verifique e use ssh-agent e ssh-add para informar o sistema SSH sobre os arquivos de chave, para que a frase secreta não precise ser usada interativamente.</span><span class="sxs-lookup"><span data-stu-id="85f1d-155">Verify and use ssh-agent and ssh-add to inform the SSH system about the key files so that the passphrase will not need to be used interactively.</span></span>

```bash
eval "$(ssh-agent -s)"
```

<span data-ttu-id="85f1d-156">Agora, adicione a chave privada ao `ssh-agent` usando o comando `ssh-add`.</span><span class="sxs-lookup"><span data-stu-id="85f1d-156">Now add the private key to `ssh-agent` using the command `ssh-add`.</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

<span data-ttu-id="85f1d-157">Agora, a senha da chave privada é armazenada no `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="85f1d-157">The private key password is now stored in `ssh-agent`.</span></span>

## <a name="using-ssh-copy-id-to-copy-the-key-to-an-existing-vm"></a><span data-ttu-id="85f1d-158">Usar `ssh-copy-id` para copiar a chave a uma VM existente</span><span class="sxs-lookup"><span data-stu-id="85f1d-158">Using `ssh-copy-id` to copy the key to an existing VM</span></span>
<span data-ttu-id="85f1d-159">Se já tiver criado uma VM, você poderá instalar a nova chave pública SSH à VM do Linux com:</span><span class="sxs-lookup"><span data-stu-id="85f1d-159">If you have already created a VM you can install the new SSH public key to your Linux VM with:</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a><span data-ttu-id="85f1d-160">Criar e configurar um arquivo de configuração do SSH</span><span class="sxs-lookup"><span data-stu-id="85f1d-160">Create and configure an SSH config file</span></span>

<span data-ttu-id="85f1d-161">É uma prática recomendada criar e configurar um arquivo `~/.ssh/config` para acelerar os logons e otimizar o comportamento do seu cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="85f1d-161">It is a recommended best practice to create and configure an `~/.ssh/config` file to speed up log ins and for optimizing your SSH client behavior.</span></span>

<span data-ttu-id="85f1d-162">O exemplo a seguir mostra uma configuração padrão.</span><span class="sxs-lookup"><span data-stu-id="85f1d-162">The following example shows a standard configuration.</span></span>

### <a name="create-the-file"></a><span data-ttu-id="85f1d-163">Criar o arquivo</span><span class="sxs-lookup"><span data-stu-id="85f1d-163">Create the file</span></span>

```bash
touch ~/.ssh/config
```

### <a name="edit-the-file-to-add-the-new-ssh-configuration"></a><span data-ttu-id="85f1d-164">Edite o arquivo a fim de adicionar a nova configuração de SSH:</span><span class="sxs-lookup"><span data-stu-id="85f1d-164">Edit the file to add the new SSH configuration:</span></span>

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a><span data-ttu-id="85f1d-165">Exemplo de arquivo `~/.ssh/config`:</span><span class="sxs-lookup"><span data-stu-id="85f1d-165">Example `~/.ssh/config` file:</span></span>

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

<span data-ttu-id="85f1d-166">Essa configuração de SSH fornece seções para cada serviço para habilitar cada um deles com seu próprio par de chaves dedicado.</span><span class="sxs-lookup"><span data-stu-id="85f1d-166">This SSH config gives you sections for each server to enable each to have its own dedicated key pair.</span></span> <span data-ttu-id="85f1d-167">As configurações padrão (`Host *`) são para quaisquer hosts que não correspondam a qualquer um dos hosts específicos acima no arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="85f1d-167">The default settings (`Host *`) are for any hosts that do not match any of the specific hosts higher up in the config file.</span></span>

### <a name="config-file-explained"></a><span data-ttu-id="85f1d-168">Arquivo de configuração explicado</span><span class="sxs-lookup"><span data-stu-id="85f1d-168">Config file explained</span></span>

<span data-ttu-id="85f1d-169">`Host` = o nome do host sendo chamado no terminal.</span><span class="sxs-lookup"><span data-stu-id="85f1d-169">`Host` = the name of the host being called on the terminal.</span></span>  <span data-ttu-id="85f1d-170">`ssh fedora22` instrui `SSH` a usar os valores no bloco de configurações rotulado como `Host fedora22` OBSERVAÇÃO: o host pode ser qualquer rótulo lógico para o uso e não representa o nome de host real de qualquer servidor.</span><span class="sxs-lookup"><span data-stu-id="85f1d-170">`ssh fedora22` tells `SSH` to use the values in the settings block labeled `Host fedora22`  NOTE: Host can be any label that is logical for your usage and does not represent the actual hostname of any server.</span></span>

<span data-ttu-id="85f1d-171">`Hostname 102.160.203.241` = o endereço IP ou o nome DNS do servidor acessado.</span><span class="sxs-lookup"><span data-stu-id="85f1d-171">`Hostname 102.160.203.241` = the IP address or DNS name for the server being accessed.</span></span>

<span data-ttu-id="85f1d-172">`User ahmet` = a conta de usuário remoto a ser usada ao fazer logon no servidor.</span><span class="sxs-lookup"><span data-stu-id="85f1d-172">`User ahmet` = the remote user account to use when logging in to the server.</span></span>

<span data-ttu-id="85f1d-173">`PubKeyAuthentication yes` = instrui o SSH desejado a usar uma chave SSH para fazer logon.</span><span class="sxs-lookup"><span data-stu-id="85f1d-173">`PubKeyAuthentication yes` = tells SSH you want to use an SSH key to log in.</span></span>

<span data-ttu-id="85f1d-174">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = a chave privada SSH e a chave pública correspondente a serem usadas para autenticação.</span><span class="sxs-lookup"><span data-stu-id="85f1d-174">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = the SSH private key and corresponding public key to use for authentication.</span></span>

## <a name="ssh-into-linux-without-a-password"></a><span data-ttu-id="85f1d-175">SSH no Linux sem uma senha</span><span class="sxs-lookup"><span data-stu-id="85f1d-175">SSH into Linux without a password</span></span>

<span data-ttu-id="85f1d-176">Agora que tem um par de chaves SSH e um arquivo de configuração do SSH configurado, você pode fazer logon na VM do Linux de forma rápida e segura.</span><span class="sxs-lookup"><span data-stu-id="85f1d-176">Now that you have an SSH key pair and a configured SSH config file, you are able to log in to your Linux VM quickly and securely.</span></span> <span data-ttu-id="85f1d-177">Na primeira vez que você fizer logon em um servidor usando uma chave SSH, o comando solicitará a senha para esse arquivo de chave.</span><span class="sxs-lookup"><span data-stu-id="85f1d-177">The first time you log in to a server using an SSH key the command prompts you for the passphrase for that key file.</span></span>

```bash
ssh fedora22
```

### <a name="command-explained"></a><span data-ttu-id="85f1d-178">Comando explicado</span><span class="sxs-lookup"><span data-stu-id="85f1d-178">Command explained</span></span>

<span data-ttu-id="85f1d-179">Quando `ssh fedora22` é executado, primeiro o SSH localiza e carrega todas as configurações do bloco `Host fedora22`, em seguida, carrega todas as configurações restantes a partir do último bloco, `Host *`.</span><span class="sxs-lookup"><span data-stu-id="85f1d-179">When `ssh fedora22` is executed SSH first locates and loads any settings from the `Host fedora22` block, and then loads all the remaining settings from the last block, `Host *`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="85f1d-180">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="85f1d-180">Next Steps</span></span>

<span data-ttu-id="85f1d-181">A próxima etapa é criar VMs do Linux do Azure usando a nova chave pública SSH.</span><span class="sxs-lookup"><span data-stu-id="85f1d-181">Next up is to create Azure Linux VMs using the new SSH public key.</span></span>  <span data-ttu-id="85f1d-182">As VMs do Azure criadas com uma chave pública SSH como o logon estão mais protegidas do que as VMs criadas com as senhas do método de logon padrão.</span><span class="sxs-lookup"><span data-stu-id="85f1d-182">Azure VMs that are created with an SSH public key as the login are better secured than VMs created with the default login method, passwords.</span></span>  <span data-ttu-id="85f1d-183">As VMs do Azure criadas com chaves SSH são por padrão configuradas com senhas desabilitadas, evitando tentativas de adivinhação por força bruta.</span><span class="sxs-lookup"><span data-stu-id="85f1d-183">Azure VMs created using SSH keys are by default configured with passwords disabled, avoiding brute-forced guessing attempts.</span></span>

* [<span data-ttu-id="85f1d-184">Criar uma VM do Linux segura usando um modelo do Azure</span><span class="sxs-lookup"><span data-stu-id="85f1d-184">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="85f1d-185">Criar uma VM Linux segura usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="85f1d-185">Create a secure Linux VM using the Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="85f1d-186">Criar uma VM Linux segura usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="85f1d-186">Create a secure Linux VM using the Azure CLI</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
