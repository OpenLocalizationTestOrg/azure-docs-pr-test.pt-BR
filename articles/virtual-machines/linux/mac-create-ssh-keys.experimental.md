---
title: "Criar um par de chaves SSH para máquinas virtuais Linux no Azure | Microsoft Docs"
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
ms.openlocfilehash: 19acd4efca7ef043f31b436b96f9129caee9591b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-ssh-public-and-private-key-pair-for-linux-vms"></a><span data-ttu-id="56881-103">Criar um par de chaves SSH pública e privada para VMs Linux</span><span class="sxs-lookup"><span data-stu-id="56881-103">Create an SSH public and private key pair for Linux VMs</span></span>

<span data-ttu-id="56881-104">Este artigo mostra como gerar um par de arquivos de chave pública e privada RSA do protocolo SSH versão 2 para uso com VMs Linux.</span><span class="sxs-lookup"><span data-stu-id="56881-104">This article shows you how to generate an SSH protocol version 2 RSA public and private key file pair to use with Linux VMs.</span></span>  <span data-ttu-id="56881-105">Com um par de chaves SSH, você pode criar máquinas virtuais no Azure que tenham como padrão o uso de chaves SSH para autenticação, eliminando a necessidade de senhas para fazer logon.</span><span class="sxs-lookup"><span data-stu-id="56881-105">With an SSH key pair, you can create Virtual Machines on Azure that default to using SSH keys for authentication, eliminating the need for passwords to log in.</span></span>  <span data-ttu-id="56881-106">As senhas podem ser adivinhadas e podem abrir suas VMs para tentativas de uso contínuo de força bruta para adivinhá-las.</span><span class="sxs-lookup"><span data-stu-id="56881-106">Passwords can be guessed, and open your VMs up to relentless brute force attempts to guess your password.</span></span> <span data-ttu-id="56881-107">As VMs criadas com os Modelos do Azure ou com o `azure-cli` podem incluir sua chave pública SSH como parte da implantação, removendo uma etapa de configuração pós-implantação que consiste na desabilitação de logons com senha para SSH.</span><span class="sxs-lookup"><span data-stu-id="56881-107">VMs created with Azure Templates or the `azure-cli` can include your SSH public key as part of the deployment, removing a post deployment configuration step of disabling password logins for SSH.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="56881-108">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="56881-108">Quick Commands</span></span>

<span data-ttu-id="56881-109">Execute os comandos a seguir de um shell Bash, substituindo os exemplos por suas próprias escolhas.</span><span class="sxs-lookup"><span data-stu-id="56881-109">Run the following commands from a Bash shell, replacing the examples with your own choices.</span></span>

<span data-ttu-id="56881-110">O arquivo de chave pública SSH é criado por padrão em `~/.ssh/id_rsa.pub`.</span><span class="sxs-lookup"><span data-stu-id="56881-110">Your SSH public key file is by default created at `~/.ssh/id_rsa.pub`.</span></span> <span data-ttu-id="56881-111">Quando receber a solicitação para usar o comando a seguir, crie uma "senha" para proteger sua chave privada.</span><span class="sxs-lookup"><span data-stu-id="56881-111">When prompted using the following command, you should create a "passphrase" to secure your private key.</span></span> <span data-ttu-id="56881-112">(A senha é usada para criptografar a chave privada.)</span><span class="sxs-lookup"><span data-stu-id="56881-112">(The passphrase is a password used to encrypt your private key.)</span></span>

```bash
ssh-keygen -t rsa -b 2048 
```

<span data-ttu-id="56881-113">Adicione a chave recém-criada em `ssh-agent`:</span><span class="sxs-lookup"><span data-stu-id="56881-113">Add the newly created key to `ssh-agent`:</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

> [!IMPORTANT] 
> <span data-ttu-id="56881-114">Os comandos acima funcionam em sistemas operacionais Linux de quase todas as distribuições, mas não funcionam, necessariamente, em contêineres, pois o ambiente pode ser radicalmente restrito.</span><span class="sxs-lookup"><span data-stu-id="56881-114">The above commands work on Linux operating systems of almost all distributions, but do not necessarily work in containers, as the environment can be radically constrained.</span></span> 

## <a name="detailed-walkthrough"></a><span data-ttu-id="56881-115">Passo a passo detalhado</span><span class="sxs-lookup"><span data-stu-id="56881-115">Detailed Walkthrough</span></span>

<span data-ttu-id="56881-116">Usar as chaves públicas e privadas do SSH é a maneira mais fácil de fazer logon em servidores Linux.</span><span class="sxs-lookup"><span data-stu-id="56881-116">Using SSH public and private keys is the easiest way to log in to your Linux servers.</span></span> <span data-ttu-id="56881-117">[criptografia de chave pública](https://en.wikipedia.org/wiki/Public-key_cryptography) fornece uma maneira muito mais segura de fazer logon na VM BSD ou do Linux no Azure do que as senhas, que podem ser obtidas por força bruta muito mais facilmente.</span><span class="sxs-lookup"><span data-stu-id="56881-117">[Public-key cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography) provides a much more secure way to log in to your Linux or BSD VM in Azure than passwords, which can be brute-forced far more easily.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="56881-118">Sua chave pública pode ser compartilhada com qualquer pessoa; mas apenas você (ou sua infraestrutura de segurança local) possui sua chave privada.</span><span class="sxs-lookup"><span data-stu-id="56881-118">Your public key can be shared with anyone; but only you (or your local security infrastructure) possess your private key.</span></span>  <span data-ttu-id="56881-119">A chave privada SSH deve ter uma [senha bastante segura](https://www.xkcd.com/936/)(fonte:[xkcd.com](https://xkcd.com)) para protegê-la.</span><span class="sxs-lookup"><span data-stu-id="56881-119">The SSH private key should have a [very secure password](https://www.xkcd.com/936/) (source:[xkcd.com](https://xkcd.com)) to safeguard it.</span></span>  <span data-ttu-id="56881-120">Esta senha é apenas para acessar a chave privada do SSH e **não é** a senha da conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="56881-120">This password is just to access the private SSH key and **is not** the user account password.</span></span>  <span data-ttu-id="56881-121">Quando você adiciona uma senha para a chave SSH, ela criptografa a chave privada usando AES de 128 bits, para que a chave privada seja inútil sem a senha para descriptografá-la.</span><span class="sxs-lookup"><span data-stu-id="56881-121">When you add a password to your SSH key, it encrypts the private key using 128-bit AES, so that the private key is useless without the password to decrypt it.</span></span>  <span data-ttu-id="56881-122">Se um invasor roubasse sua chave privada e se ela não tivesse uma senha, ele poderia usar essa chave privada para fazer logon em qualquer servidor com a chave pública correspondente.</span><span class="sxs-lookup"><span data-stu-id="56881-122">If an attacker stole your private key and that key did not have a password, they would be able to use that private key to log in to any servers that have the corresponding public key.</span></span>  <span data-ttu-id="56881-123">Se uma chave privada for protegida por senha, ela não poderá ser usada por esse invasor, o que é uma camada adicional de segurança para sua infraestrutura no Azure.</span><span class="sxs-lookup"><span data-stu-id="56881-123">If a private key is password protected it cannot be used by that attacker, providing an additional layer of security for your infrastructure on Azure.</span></span>

<span data-ttu-id="56881-124">Este artigo cria arquivos de chave pública e privada RSA do protocolo SSH versão 2, recomendados para implantações no Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="56881-124">This article creates SSH protocol version 2 RSA public and private key files, which are recommended for deployments on the Resource Manager.</span></span>  <span data-ttu-id="56881-125">Chaves *SSH-rsa* são necessárias no [portal](https://portal.azure.com) para implantações clássicas e do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="56881-125">*ssh-rsa* keys are required on the [portal](https://portal.azure.com) for both classic and Resource Manager deployments.</span></span>

## <a name="disable-ssh-passwords-by-using-ssh-keys"></a><span data-ttu-id="56881-126">Desabilitar senhas SSH usando chaves SSH</span><span class="sxs-lookup"><span data-stu-id="56881-126">Disable SSH passwords by using SSH keys</span></span>

<span data-ttu-id="56881-127">O Azure requer chaves públicas e privadas de pelo menos 2048 bits em formato ssh-rsa.</span><span class="sxs-lookup"><span data-stu-id="56881-127">Azure requires at least 2048-bit, ssh-rsa format public and private keys.</span></span> <span data-ttu-id="56881-128">Para criar as chaves, use `ssh-keygen`, que faz uma série de perguntas e, em seguida, grava uma chave privada e uma chave pública correspondente.</span><span class="sxs-lookup"><span data-stu-id="56881-128">To create the keys use `ssh-keygen`, which asks a series of questions and then writes a private key and a matching public key.</span></span> <span data-ttu-id="56881-129">Quando uma VM do Azure é criada, a chave pública é copiada para `~/.ssh/authorized_keys`.</span><span class="sxs-lookup"><span data-stu-id="56881-129">When an Azure VM is created, the public key is copied to `~/.ssh/authorized_keys`.</span></span>  <span data-ttu-id="56881-130">As chaves SSH no `~/.ssh/authorized_keys` são usadas para desafiar o cliente para coincidir com a chave privada correspondente em uma conexão de logon SSH.</span><span class="sxs-lookup"><span data-stu-id="56881-130">SSH keys in `~/.ssh/authorized_keys` are used to challenge the client to match the corresponding private key on an SSH login connection.</span></span>  <span data-ttu-id="56881-131">Quando uma VM Linux do Azure é criada usando chaves SSH para autenticação, o Azure configura o servidor SSHD para não permitir logons com senha, apenas com chaves SSH.</span><span class="sxs-lookup"><span data-stu-id="56881-131">When an Azure Linux VM is created using SSH keys for authentication, Azure configures the SSHD server to not allow password logins, only SSH keys.</span></span>  <span data-ttu-id="56881-132">Portanto, ao criar VMs Linux do Azure com chaves SSH, você pode ajudar a proteger a implantação de VM e evitar a etapa de configuração pós-implantação típica de desabilitar as senhas no arquivo de configuração sshd_config.</span><span class="sxs-lookup"><span data-stu-id="56881-132">Therefore, by creating Azure Linux VMs with SSH keys, you can help secure the VM deployment and save yourself the typical post-deployment configuration step of disabling passwords in the sshd_config config file.</span></span>

## <a name="using-ssh-keygen"></a><span data-ttu-id="56881-133">Usando ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="56881-133">Using ssh-keygen</span></span>

<span data-ttu-id="56881-134">Esse comando cria um par de chaves SSH (criptografado) protegido por senha usando o RSA de 2048 bits e é comentado para identificá-lo facilmente.</span><span class="sxs-lookup"><span data-stu-id="56881-134">This command creates a password secured (encrypted) SSH key pair using 2048-bit RSA and it is commented to easily identify it.</span></span>  

<span data-ttu-id="56881-135">As chaves SSH são mantidas por padrão no diretório `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="56881-135">SSH keys are by default kept in the `~/.ssh` directory.</span></span>  <span data-ttu-id="56881-136">Se você não tiver um diretório `~/.ssh`, o comando `ssh-keygen` o criará para você com as permissões corretas.</span><span class="sxs-lookup"><span data-stu-id="56881-136">If you do not have a `~/.ssh` directory, the `ssh-keygen` command creates it for you with the correct permissions.</span></span>

```bash
ssh-keygen \
-t rsa \
-b 2048 
```

<span data-ttu-id="56881-137">*Comando explicado*</span><span class="sxs-lookup"><span data-stu-id="56881-137">*Command explained*</span></span>

<span data-ttu-id="56881-138">`ssh-keygen` = programa usado para criar as chaves</span><span class="sxs-lookup"><span data-stu-id="56881-138">`ssh-keygen` = the program used to create the keys</span></span>

<span data-ttu-id="56881-139">`-t rsa` = tipo de chave a ser criada, que é o formato RSA [wikipedia](https://en.wikipedia.org/wiki/RSA_(cryptosystem)</span><span class="sxs-lookup"><span data-stu-id="56881-139">`-t rsa` = type of key to create which is the RSA format [wikipedia](https://en.wikipedia.org/wiki/RSA_(cryptosystem)</span></span>

<span data-ttu-id="56881-140">`-b 2048` = bits da chave</span><span class="sxs-lookup"><span data-stu-id="56881-140">`-b 2048` = bits of the key</span></span>


## <a name="classic-portal-and-x509-certs"></a><span data-ttu-id="56881-141">Portal clássico e certificados x.509</span><span class="sxs-lookup"><span data-stu-id="56881-141">Classic portal and X.509 certs</span></span>

<span data-ttu-id="56881-142">Se você está usando o [portal clássico](https://manage.windowsazure.com/) do Azure, ele requer certificados x.509 para as chaves SSH.</span><span class="sxs-lookup"><span data-stu-id="56881-142">If you are using the Azure [classic portal](https://manage.windowsazure.com/), it requires X.509 certs for the SSH keys.</span></span>  <span data-ttu-id="56881-143">Outros tipos de chaves públicas SSH não são permitidos. Elas *devem* ser certificados x.509.</span><span class="sxs-lookup"><span data-stu-id="56881-143">No other types of SSH public keys are allowed, they *must* be X.509 certs.</span></span>

<span data-ttu-id="56881-144">Para criar um certificado x.509 de sua chave privada do SSH-RSA existente:</span><span class="sxs-lookup"><span data-stu-id="56881-144">To create an X.509 cert from your existing SSH-RSA private key:</span></span>

```bash
openssl req -x509 \
-key ~/.ssh/id_rsa \
-nodes \
-days 365 \
-newkey rsa:2048 \
-out ~/.ssh/id_rsa.pem
```

## <a name="classic-deploy-using-asm"></a><span data-ttu-id="56881-145">Implantação clássica usando `asm`</span><span class="sxs-lookup"><span data-stu-id="56881-145">Classic deploy using `asm`</span></span>

<span data-ttu-id="56881-146">Se estiver usando o modelo de implantação clássica (CLI de gerenciamento de serviços do Azure `asm`), você poderá usar uma chave pública SSH-RSA ou uma chave formatada como RFC4716 em um contêiner **.pem**.</span><span class="sxs-lookup"><span data-stu-id="56881-146">If you are using the classic deploy model (Azure service management CLI `asm`), you can use an SSH-RSA public key or an RFC4716 formatted key in a **.pem** container.</span></span>  <span data-ttu-id="56881-147">A chave pública SSH-RSA é a que foi criada anteriormente neste artigo usando `ssh-keygen`.</span><span class="sxs-lookup"><span data-stu-id="56881-147">The SSH-RSA public key is what was created earlier in this article using `ssh-keygen`.</span></span>

<span data-ttu-id="56881-148">Para criar uma chave formatada RFC4716 com base em uma chave pública SSH existente:</span><span class="sxs-lookup"><span data-stu-id="56881-148">To create a RFC4716 formatted key from an existing SSH public key:</span></span>

```bash
ssh-keygen \
-f ~/.ssh/id_rsa.pub \
-e \
-m RFC4716 > ~/.ssh/id_ssh2.pem
```

## <a name="example-of-ssh-keygen"></a><span data-ttu-id="56881-149">Exemplo de ssh-keygen</span><span class="sxs-lookup"><span data-stu-id="56881-149">Example of ssh-keygen</span></span>

```bash
ssh-keygen -t rsa -b 2048 -C "ahmet@myserver"
Generating public/private rsa key pair.
Enter file in which to save the key (/home/ahmet/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/ahmet/.ssh/id_rsa.
Your public key has been saved in /home/ahmet/.ssh/id_rsa.pub.
The key fingerprint is:
14:a3:cb:3e:78:ad:25:cc:55:e9:0c:08:e5:d1:a9:08 ahmet@myserver
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

<span data-ttu-id="56881-150">Arquivos de chave salvos:</span><span class="sxs-lookup"><span data-stu-id="56881-150">Saved key files:</span></span>

`Enter file in which to save the key (/home/ahmet/.ssh/id_rsa): ~/.ssh/id_rsa`

<span data-ttu-id="56881-151">O nome do par de chaves para este artigo.</span><span class="sxs-lookup"><span data-stu-id="56881-151">The key pair name for this article.</span></span>  <span data-ttu-id="56881-152">Ter um par de chaves denominado **id_rsa** é o padrão e algumas ferramentas podem esperar o nome de arquivo da chave privada **id_rsa**, portanto, ter um é uma boa ideia.</span><span class="sxs-lookup"><span data-stu-id="56881-152">Having a key pair named **id_rsa** is the default and some tools might expect the **id_rsa** private key file name so having one is a good idea.</span></span> <span data-ttu-id="56881-153">O diretório `~/.ssh/` é o local padrão para os pares de chave SSH e o arquivo de configuração SSH.</span><span class="sxs-lookup"><span data-stu-id="56881-153">The directory `~/.ssh/` is the default location for SSH key pairs and the SSH config file.</span></span>  <span data-ttu-id="56881-154">Se não for especificado com um caminho completo, `ssh-keygen` criará as chaves no diretório de trabalho atual e não o `~/.ssh` padrão.</span><span class="sxs-lookup"><span data-stu-id="56881-154">If not specified with a full path, `ssh-keygen` will create the keys in the current working directory, not the default `~/.ssh`.</span></span>

<span data-ttu-id="56881-155">Uma listagem do diretório `~/.ssh` .</span><span class="sxs-lookup"><span data-stu-id="56881-155">A listing of the `~/.ssh` directory.</span></span>

```bash
ls -al ~/.ssh
-rw------- 1 ahmet staff  1675 Aug 25 18:04 id_rsa
-rw-r--r-- 1 ahmet staff   410 Aug 25 18:04 rsa.pub
```

<span data-ttu-id="56881-156">Senha da chave:</span><span class="sxs-lookup"><span data-stu-id="56881-156">Key Password:</span></span>

`Enter passphrase (empty for no passphrase):`

<span data-ttu-id="56881-157">`ssh-keygen` refere-se a uma senha usada para criptografar a chave privada como "senha".</span><span class="sxs-lookup"><span data-stu-id="56881-157">`ssh-keygen` refers to a password used to encrypt the private key as "a passphrase."</span></span>  <span data-ttu-id="56881-158">É *altamente* recomendável adicionar uma senha a seus pares de chave.</span><span class="sxs-lookup"><span data-stu-id="56881-158">It is *strongly* recommended to add a passphrase to your key pairs.</span></span> <span data-ttu-id="56881-159">Sem uma senha para proteger a chave privada, qualquer pessoa com o arquivo da chave pode usá-lo para fazer logon em qualquer servidor com a chave pública correspondente.</span><span class="sxs-lookup"><span data-stu-id="56881-159">Without a passphrase protecting the private key, anyone with the key file can use it to log in to any server that has the corresponding public key.</span></span> <span data-ttu-id="56881-160">Portanto, adicionar uma senha oferece mais proteção no caso de alguém obter acesso a seu arquivo de chave privada, dando-lhe tempo para alterar as chaves usadas para autenticá-lo.</span><span class="sxs-lookup"><span data-stu-id="56881-160">Adding a passphrase offers more protection in case someone is able to gain access to your private key file, giving you time to change the keys used to authenticate you.</span></span>

## <a name="using-ssh-agent-to-store-your-private-key-password"></a><span data-ttu-id="56881-161">Usando ssh-agent para armazenar sua senha de chave privada</span><span class="sxs-lookup"><span data-stu-id="56881-161">Using ssh-agent to store your private key password</span></span>

<span data-ttu-id="56881-162">Para evitar a digitação da senha do arquivo de chave privada em cada logon do SSH, você poderá usar `ssh-agent` para armazenar em cache a senha do arquivo de chave privada.</span><span class="sxs-lookup"><span data-stu-id="56881-162">To avoid typing your private key file passphrase with every SSH login, you can use `ssh-agent` to cache your private key file password.</span></span> <span data-ttu-id="56881-163">Se você estiver usando um Mac, a cadeia de chaves do OSX armazena com segurança suas senhas de chave privadas quando `ssh-agent`é chamado.</span><span class="sxs-lookup"><span data-stu-id="56881-163">If you are using a Mac, the OSX Keychain securely stores the private key passwords when you invoke `ssh-agent`.</span></span>

<span data-ttu-id="56881-164">Verifique e use `ssh-agent` e `ssh-add` para informar o sistema SSH sobre os arquivos de chave, para que a senha não precise ser usada interativamente.</span><span class="sxs-lookup"><span data-stu-id="56881-164">Verify and use `ssh-agent` and `ssh-add` to inform the SSH system about the key files so that the passphrase will not need to be used interactively.</span></span>

```bash
eval "$(ssh-agent -s)"
```

<span data-ttu-id="56881-165">Agora, adicione a chave privada ao `ssh-agent` usando o comando `ssh-add`.</span><span class="sxs-lookup"><span data-stu-id="56881-165">Now add the private key to `ssh-agent` using the command `ssh-add`.</span></span>

```bash
ssh-add ~/.ssh/id_rsa
```

<span data-ttu-id="56881-166">Agora, a senha da chave privada é armazenada no `ssh-agent`.</span><span class="sxs-lookup"><span data-stu-id="56881-166">The private key password is now stored in `ssh-agent`.</span></span>

## <a name="using-ssh-copy-id-to-install-the-new-key"></a><span data-ttu-id="56881-167">Usar `ssh-copy-id` para instalar a nova chave</span><span class="sxs-lookup"><span data-stu-id="56881-167">Using `ssh-copy-id` to install the new key</span></span>
<span data-ttu-id="56881-168">Se você já tiver criado uma VM, instale a nova chave pública SSH para sua VM Linux com o seguinte comando, substituindo o nome de usuário da VM e o endereço do servidor por seus próprios valores:</span><span class="sxs-lookup"><span data-stu-id="56881-168">If you have already created a VM you can install the new SSH public key to your Linux VM with the following command, replacing the VM username and the server address with your own values:</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub ahmet@myserver
```

## <a name="create-and-configure-an-ssh-config-file"></a><span data-ttu-id="56881-169">Criar e configurar um arquivo de configuração do SSH</span><span class="sxs-lookup"><span data-stu-id="56881-169">Create and configure an SSH config file</span></span>

<span data-ttu-id="56881-170">É uma prática recomendada criar e configurar um arquivo `~/.ssh/config` para acelerar os logons e otimizar o comportamento do seu cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="56881-170">It is a best practice to create and configure an `~/.ssh/config` file to speed up log ins and for optimizing your SSH client behavior.</span></span>

<span data-ttu-id="56881-171">O exemplo a seguir mostra uma configuração padrão.</span><span class="sxs-lookup"><span data-stu-id="56881-171">The following example shows a standard configuration.</span></span>

### <a name="create-the-file"></a><span data-ttu-id="56881-172">Criar o arquivo</span><span class="sxs-lookup"><span data-stu-id="56881-172">Create the file</span></span>

```bash
touch ~/.ssh/config
```

### <a name="edit-the-file-to-add-the-new-ssh-configuration"></a><span data-ttu-id="56881-173">Edite o arquivo a fim de adicionar a nova configuração de SSH:</span><span class="sxs-lookup"><span data-stu-id="56881-173">Edit the file to add the new SSH configuration:</span></span>

```bash
vim ~/.ssh/config
```

### <a name="example-sshconfig-file"></a><span data-ttu-id="56881-174">Exemplo de arquivo `~/.ssh/config`:</span><span class="sxs-lookup"><span data-stu-id="56881-174">Example `~/.ssh/config` file:</span></span>

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

<span data-ttu-id="56881-175">Essa configuração de SSH fornece seções para cada serviço para habilitar cada um deles com seu próprio par de chaves dedicado.</span><span class="sxs-lookup"><span data-stu-id="56881-175">This SSH config gives you sections for each server to enable each to have its own dedicated key pair.</span></span> <span data-ttu-id="56881-176">As configurações padrão (`Host *`) são para quaisquer hosts que não correspondam a qualquer um dos hosts específicos acima no arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="56881-176">The default settings (`Host *`) are for any hosts that do not match any of the specific hosts higher up in the config file.</span></span>

### <a name="config-file-explained"></a><span data-ttu-id="56881-177">Arquivo de configuração explicado</span><span class="sxs-lookup"><span data-stu-id="56881-177">Config file explained</span></span>

<span data-ttu-id="56881-178">`Host` = o nome do host sendo chamado no terminal.</span><span class="sxs-lookup"><span data-stu-id="56881-178">`Host` = the name of the host being called on the terminal.</span></span>  <span data-ttu-id="56881-179">`ssh fedora22` instrui `SSH` a usar os valores no bloco de configurações rotulado como `Host fedora22` OBSERVAÇÃO: o host pode ser qualquer rótulo lógico para o uso e não representa o nome de host real de qualquer servidor.</span><span class="sxs-lookup"><span data-stu-id="56881-179">`ssh fedora22` tells `SSH` to use the values in the settings block labeled `Host fedora22`  NOTE: Host can be any label that is logical for your usage and does not represent the actual hostname of any server.</span></span>

<span data-ttu-id="56881-180">`Hostname 102.160.203.241` = o endereço IP ou o nome DNS do servidor acessado.</span><span class="sxs-lookup"><span data-stu-id="56881-180">`Hostname 102.160.203.241` = the IP address or DNS name for the server being accessed.</span></span>

<span data-ttu-id="56881-181">`User ahmet` = a conta de usuário remoto a ser usada ao fazer logon no servidor.</span><span class="sxs-lookup"><span data-stu-id="56881-181">`User ahmet` = the remote user account to use when logging in to the server.</span></span>

<span data-ttu-id="56881-182">`PubKeyAuthentication yes` = instrui o SSH desejado a usar uma chave SSH para fazer logon.</span><span class="sxs-lookup"><span data-stu-id="56881-182">`PubKeyAuthentication yes` = tells SSH you want to use an SSH key to log in.</span></span>

<span data-ttu-id="56881-183">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = a chave privada SSH e a chave pública correspondente a serem usadas para autenticação.</span><span class="sxs-lookup"><span data-stu-id="56881-183">`IdentityFile /home/ahmet/.ssh/id_id_rsa` = the SSH private key and corresponding public key to use for authentication.</span></span>

## <a name="ssh-into-linux-without-a-password"></a><span data-ttu-id="56881-184">SSH no Linux sem uma senha</span><span class="sxs-lookup"><span data-stu-id="56881-184">SSH into Linux without a password</span></span>

<span data-ttu-id="56881-185">Agora que tem um par de chaves SSH e um arquivo de configuração do SSH configurado, você pode fazer logon na VM do Linux de forma rápida e segura.</span><span class="sxs-lookup"><span data-stu-id="56881-185">Now that you have an SSH key pair and a configured SSH config file, you are able to log in to your Linux VM quickly and securely.</span></span> <span data-ttu-id="56881-186">Na primeira vez que você fizer logon em um servidor usando uma chave SSH, o comando solicitará a senha para esse arquivo de chave.</span><span class="sxs-lookup"><span data-stu-id="56881-186">The first time you log in to a server using an SSH key the command prompts you for the passphrase for that key file.</span></span>

```bash
ssh fedora22
```

### <a name="command-explained"></a><span data-ttu-id="56881-187">Comando explicado</span><span class="sxs-lookup"><span data-stu-id="56881-187">Command explained</span></span>

<span data-ttu-id="56881-188">Quando `ssh fedora22` é executado, primeiro o SSH localiza e carrega todas as configurações do bloco `Host fedora22`, em seguida, carrega todas as configurações restantes a partir do último bloco, `Host *`.</span><span class="sxs-lookup"><span data-stu-id="56881-188">When `ssh fedora22` is executed SSH first locates and loads any settings from the `Host fedora22` block, and then loads all the remaining settings from the last block, `Host *`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="56881-189">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="56881-189">Next Steps</span></span>

<span data-ttu-id="56881-190">A próxima etapa é criar VMs do Linux do Azure usando a nova chave pública SSH.</span><span class="sxs-lookup"><span data-stu-id="56881-190">Next up is to create Azure Linux VMs using the new SSH public key.</span></span>  <span data-ttu-id="56881-191">As VMs do Azure criadas com uma chave pública SSH como o logon estão mais protegidas do que as VMs criadas com as senhas do método de logon padrão.</span><span class="sxs-lookup"><span data-stu-id="56881-191">Azure VMs that are created with an SSH public key as the login are better secured than VMs created with the default login method, passwords.</span></span>  <span data-ttu-id="56881-192">As VMs do Azure criadas com chaves SSH são por padrão configuradas com senhas desabilitadas, evitando tentativas de adivinhação por força bruta.</span><span class="sxs-lookup"><span data-stu-id="56881-192">Azure VMs created using SSH keys are by default configured with passwords disabled, avoiding brute-forced guessing attempts.</span></span> <span data-ttu-id="56881-193">Se você precisar de mais ajuda com a criação de seu par de chaves SSH, ou precisar de outros certificados, por exemplo, para uso com o portal clássico, confira [Etapas detalhadas para criar pares de chave SSH e certificados](create-ssh-keys-detailed.md).</span><span class="sxs-lookup"><span data-stu-id="56881-193">If you need more assistance in creating your SSH key pair or require additional certificates, such as for use with the classic portal, see [Detailed steps to create SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

* [<span data-ttu-id="56881-194">Criar uma VM do Linux segura usando um modelo do Azure</span><span class="sxs-lookup"><span data-stu-id="56881-194">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="56881-195">Criar uma VM Linux segura usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="56881-195">Create a secure Linux VM using the Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="56881-196">Criar uma VM Linux segura usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="56881-196">Create a secure Linux VM using the Azure CLI</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
