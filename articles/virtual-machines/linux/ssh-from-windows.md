---
title: chaves de aaaUse SSH com o Windows para VMs do Linux | Microsoft Docs
description: "Saiba como toogenerate e usar SSH de chaves em uma máquina de virtual do Windows computador tooconnect tooa Linux no Azure."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 2cacda3b-7949-4036-bd5d-837e8b09a9c8
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: danlep
ms.openlocfilehash: 6c44217332538857cc2ca2e85de4b476aa71251c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-ssh-keys-with-windows-on-azure"></a><span data-ttu-id="d23ba-103">Como chaves de tooUse SSH com o Windows no Azure</span><span class="sxs-lookup"><span data-stu-id="d23ba-103">How tooUse SSH keys with Windows on Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d23ba-104">Windows</span><span class="sxs-lookup"><span data-stu-id="d23ba-104">Windows</span></span>](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> * [<span data-ttu-id="d23ba-105">Linux/Mac</span><span class="sxs-lookup"><span data-stu-id="d23ba-105">Linux/Mac</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
>
>

<span data-ttu-id="d23ba-106">Quando você se conectar tooLinux (máquinas virtuais) no Azure, você deve usar [criptografia de chave pública](https://wikipedia.org/wiki/Public-key_cryptography) tooprovide um toolog de maneira mais segura em tooyour VM do Linux.</span><span class="sxs-lookup"><span data-stu-id="d23ba-106">When you connect tooLinux virtual machines (VMs) in Azure, you should use [public-key cryptography](https://wikipedia.org/wiki/Public-key_cryptography) tooprovide a more secure way toolog in tooyour Linux VM.</span></span> <span data-ttu-id="d23ba-107">Esse processo envolve uma troca de chaves pública e privada usando Olá SSH (secure shell) comando tooauthenticate em vez de um nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="d23ba-107">This process involves a public and private key exchange using hello secure shell (SSH) command tooauthenticate yourself rather than a username and password.</span></span> <span data-ttu-id="d23ba-108">As senhas são vulneráveis toobrute ataques, especialmente em VMs com a Internet, como servidores web.</span><span class="sxs-lookup"><span data-stu-id="d23ba-108">Passwords are vulnerable toobrute-force attacks, especially on Internet-facing VMs such as web servers.</span></span> <span data-ttu-id="d23ba-109">Este artigo fornece uma visão geral das chaves de SSH como toogenerate Olá chaves apropriadas em um computador com Windows.</span><span class="sxs-lookup"><span data-stu-id="d23ba-109">This article provides an overview of SSH keys and how toogenerate hello appropriate keys on a Windows computer.</span></span>

## <a name="overview-of-ssh-and-keys"></a><span data-ttu-id="d23ba-110">Visão geral do SSH e das chaves</span><span class="sxs-lookup"><span data-stu-id="d23ba-110">Overview of SSH and keys</span></span>
<span data-ttu-id="d23ba-111">Você pode fazer logon com segurança no tooyour VM Linux usando as chaves públicas e privadas:</span><span class="sxs-lookup"><span data-stu-id="d23ba-111">You can securely log in tooyour Linux VM by using public and private keys:</span></span>

* <span data-ttu-id="d23ba-112">Olá **chave pública** é colocado em sua VM do Linux ou qualquer outro serviço que você deseja toouse com criptografia de chave pública.</span><span class="sxs-lookup"><span data-stu-id="d23ba-112">hello **public key** is placed on your Linux VM, or any other service that you wish toouse with public-key cryptography.</span></span>
* <span data-ttu-id="d23ba-113">Olá **chave privada** que você está presente tooyour VM Linux quando você fizer logon, tooverify sua identidade.</span><span class="sxs-lookup"><span data-stu-id="d23ba-113">hello **private key** is what you present tooyour Linux VM when you log in, tooverify your identity.</span></span> <span data-ttu-id="d23ba-114">Proteja essa chave privada.</span><span class="sxs-lookup"><span data-stu-id="d23ba-114">Protect this private key.</span></span> <span data-ttu-id="d23ba-115">Não a compartilhe.</span><span class="sxs-lookup"><span data-stu-id="d23ba-115">Do not share it.</span></span>

<span data-ttu-id="d23ba-116">Essas chaves públicas e privadas podem ser usadas em vários serviços e VMs.</span><span class="sxs-lookup"><span data-stu-id="d23ba-116">These public and private keys can be used on multiple VMs and services.</span></span> <span data-ttu-id="d23ba-117">Não é necessário um par de chaves para cada VM ou serviço que você deseja tooaccess.</span><span class="sxs-lookup"><span data-stu-id="d23ba-117">You do not need a pair of keys for each VM or service you wish tooaccess.</span></span> <span data-ttu-id="d23ba-118">Para obter uma visão mais detalhada, confira [criptografia de chave pública](https://wikipedia.org/wiki/Public-key_cryptography).</span><span class="sxs-lookup"><span data-stu-id="d23ba-118">For a more detailed overview, see [public-key cryptography](https://wikipedia.org/wiki/Public-key_cryptography).</span></span>

<span data-ttu-id="d23ba-119">O SSH é um protocolo de conexão criptografada que permite logons seguros por conexões não protegidas.</span><span class="sxs-lookup"><span data-stu-id="d23ba-119">SSH is an encrypted connection protocol that allows secure logins over unsecured connections.</span></span> <span data-ttu-id="d23ba-120">É o protocolo de conexão padrão Olá para VMs do Linux hospedado no Azure.</span><span class="sxs-lookup"><span data-stu-id="d23ba-120">It is hello default connection protocol for Linux VMs hosted in Azure.</span></span> <span data-ttu-id="d23ba-121">Embora SSH próprio fornece uma conexão criptografada, usando senhas com conexões SSH ainda deixa Olá VM vulnerável toobrute ataques ou adivinhação de senhas.</span><span class="sxs-lookup"><span data-stu-id="d23ba-121">Although SSH itself provides an encrypted connection, using passwords with SSH connections still leaves hello VM vulnerable toobrute-force attacks or guessing of passwords.</span></span> <span data-ttu-id="d23ba-122">Um método mais seguro e preferencial de conexão tooa VM usando o SSH está usando essas chaves públicas e privadas, também conhecido como chaves SSH.</span><span class="sxs-lookup"><span data-stu-id="d23ba-122">A more secure and preferred method of connecting tooa VM using SSH is by using these public and private keys, also known as SSH keys.</span></span>

<span data-ttu-id="d23ba-123">Se você não desejar que as chaves de SSH toouse, você ainda pode fazer logon no tooyour VMs do Linux usando uma senha.</span><span class="sxs-lookup"><span data-stu-id="d23ba-123">If you do not wish toouse SSH keys, you can still log in tooyour Linux VMs using a password.</span></span> <span data-ttu-id="d23ba-124">Se sua VM não estiver toohello exposto à Internet, usar as senhas pode ser suficiente.</span><span class="sxs-lookup"><span data-stu-id="d23ba-124">If your VM is not exposed toohello Internet, using passwords may be sufficient.</span></span> <span data-ttu-id="d23ba-125">No entanto, ainda precisar toomanage suas senhas para cada VM do Linux e manter políticas de senha íntegro e práticas recomendadas, como comprimento mínimo da senha e atualizá-las regularmente.</span><span class="sxs-lookup"><span data-stu-id="d23ba-125">However, you still need toomanage your passwords for each Linux VM and maintain healthy password policies and practices, such as minimum password length and regularly updating them.</span></span> <span data-ttu-id="d23ba-126">use Olá de chaves SSH reduz a complexidade de saudação do gerenciamento de credenciais individuais em várias VMs.</span><span class="sxs-lookup"><span data-stu-id="d23ba-126">hello use of SSH keys reduces hello complexity of managing individual credentials across multiple VMs.</span></span>

## <a name="windows-packages-and-ssh-clients"></a><span data-ttu-id="d23ba-127">Pacotes do Windows e clientes SSH</span><span class="sxs-lookup"><span data-stu-id="d23ba-127">Windows packages and SSH clients</span></span>
<span data-ttu-id="d23ba-128">Conecte-se tooand gerenciar VMs do Linux no Azure usando um **cliente SSH**.</span><span class="sxs-lookup"><span data-stu-id="d23ba-128">You connect tooand manage Linux VMs in Azure using an **SSH client**.</span></span> <span data-ttu-id="d23ba-129">Os computadores Windows geralmente não têm um cliente SSH instalado.</span><span class="sxs-lookup"><span data-stu-id="d23ba-129">Windows computers do not typically have an SSH client installed.</span></span> <span data-ttu-id="d23ba-130">saudação de atualização de aniversário do Windows 10 adicionado Bash para Windows e mais recente atualização do Windows 10 criadores hello fornece atualizações adicionais.</span><span class="sxs-lookup"><span data-stu-id="d23ba-130">hello Windows 10 Anniversary Update added Bash for Windows, and hello latest Windows 10 Creators Update provides additional updates.</span></span> <span data-ttu-id="d23ba-131">Este subsistema Windows para Linux permite utilitários toorun e acesso como um cliente SSH nativamente dentro de um shell Bash.</span><span class="sxs-lookup"><span data-stu-id="d23ba-131">This Windows Subsystem for Linux allows you toorun and access utilities such as an SSH client natively within a Bash shell.</span></span> <span data-ttu-id="d23ba-132">Você pode seguir qualquer um dos documentos do Linux hello, tais como [como pares de chave SSH toogenerate para Linux](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="d23ba-132">You can then follow any of hello Linux docs, such as [How toogenerate SSH key pairs for Linux](mac-create-ssh-keys.md).</span></span> <span data-ttu-id="d23ba-133">O Bash para Windows ainda está em desenvolvimento e é considerado uma versão beta.</span><span class="sxs-lookup"><span data-stu-id="d23ba-133">Bash for Windows is still under development, and is considered a beta release.</span></span> <span data-ttu-id="d23ba-134">Para saber mais sobre o Bash para Windows, confira [Bash on Ubuntu on Windows](https://msdn.microsoft.com/commandline/wsl/about) (Bash no Ubuntu no Windows).</span><span class="sxs-lookup"><span data-stu-id="d23ba-134">For more information about Bash for Windows, see [Bash on Ubuntu on Windows](https://msdn.microsoft.com/commandline/wsl/about).</span></span>

<span data-ttu-id="d23ba-135">Se você quiser toouse algo diferente de Bash para Windows, estão incluídos comuns Windows SSH clientes que você pode instalar Olá pacotes a seguir:</span><span class="sxs-lookup"><span data-stu-id="d23ba-135">If you wish toouse something other than Bash for Windows, common Windows SSH clients you can install are included in hello following packages:</span></span>

* [<span data-ttu-id="d23ba-136">Git for Windows</span><span class="sxs-lookup"><span data-stu-id="d23ba-136">Git For Windows</span></span>](https://git-for-windows.github.io/)
* [<span data-ttu-id="d23ba-137">puTTY</span><span class="sxs-lookup"><span data-stu-id="d23ba-137">puTTY</span></span>](http://www.chiark.greenend.org.uk/~sgtatham/putty/)
* [<span data-ttu-id="d23ba-138">MobaXterm</span><span class="sxs-lookup"><span data-stu-id="d23ba-138">MobaXterm</span></span>](http://mobaxterm.mobatek.net/)
* [<span data-ttu-id="d23ba-139">Cygwin</span><span class="sxs-lookup"><span data-stu-id="d23ba-139">Cygwin</span></span>](https://cygwin.com/)


## <a name="which-key-files-do-you-need-toocreate"></a><span data-ttu-id="d23ba-140">Arquivos de chave que você precisa toocreate?</span><span class="sxs-lookup"><span data-stu-id="d23ba-140">Which key files do you need toocreate?</span></span>
<span data-ttu-id="d23ba-141">O Azure requer chaves públicas e privadas de pelo menos 2048 bits em formato **ssh-rsa**.</span><span class="sxs-lookup"><span data-stu-id="d23ba-141">Azure requires at least 2048-bit, **ssh-rsa** formatted public and private keys.</span></span> <span data-ttu-id="d23ba-142">Se você estiver gerenciando recursos do Azure usando o modelo de implantação clássico hello, você também precisa toogenerate um PEM (`.pem` arquivo).</span><span class="sxs-lookup"><span data-stu-id="d23ba-142">If you are managing Azure resources using hello Classic deployment model, you also need toogenerate a PEM (`.pem` file).</span></span>

<span data-ttu-id="d23ba-143">Aqui estão os cenários de implantação hello e tipos de saudação de arquivos que você usa em cada:</span><span class="sxs-lookup"><span data-stu-id="d23ba-143">Here are hello deployment scenarios, and hello types of files you use in each:</span></span>

1. <span data-ttu-id="d23ba-144">**SSH-rsa** chaves são necessárias para qualquer implantação usando Olá [portal do Azure](https://portal.azure.com)e as implantações do Gerenciador de recursos usando Olá [CLI do Azure](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="d23ba-144">**ssh-rsa** keys are required for any deployment using hello [Azure portal](https://portal.azure.com), and Resource Manager deployments using hello [Azure CLI](../../cli-install-nodejs.md).</span></span>
   * <span data-ttu-id="d23ba-145">Geralmente, essas chaves são tudo do que a maioria das pessoas precisa.</span><span class="sxs-lookup"><span data-stu-id="d23ba-145">These keys are usually all most people need.</span></span>
2. <span data-ttu-id="d23ba-146">Um `.pem` arquivo é necessário toocreate VMs usando Olá clássico implantação.</span><span class="sxs-lookup"><span data-stu-id="d23ba-146">A `.pem` file is required toocreate VMs using hello Classic deployment.</span></span> <span data-ttu-id="d23ba-147">Essas chaves são suportadas em implantações clássico ao usar Olá [portal do Azure](https://portal.azure.com) ou [CLI do Azure](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="d23ba-147">These keys are supported in Classic deployments when using hello [Azure portal](https://portal.azure.com) or [Azure CLI](../../cli-install-nodejs.md).</span></span>
   * <span data-ttu-id="d23ba-148">Você só precisa toocreate essas outras chaves e certificados se você estiver gerenciando recursos criados usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="d23ba-148">You only need toocreate these additional keys and certificates if you are managing resources created using hello Classic deployment model.</span></span>

## <a name="install-git-for-windows"></a><span data-ttu-id="d23ba-149">Instalar o Git for Windows</span><span class="sxs-lookup"><span data-stu-id="d23ba-149">Install Git for Windows</span></span>
<span data-ttu-id="d23ba-150">seção anterior Hello listados vários pacotes que incluem hello `openssl` ferramenta para Windows.</span><span class="sxs-lookup"><span data-stu-id="d23ba-150">hello preceding section listed several packages that include hello `openssl` tool for Windows.</span></span> <span data-ttu-id="d23ba-151">Essa ferramenta é que as chaves públicas e privadas toocreate necessários.</span><span class="sxs-lookup"><span data-stu-id="d23ba-151">This tool is needed toocreate public and private keys.</span></span> <span data-ttu-id="d23ba-152">Olá detalhes de exemplos a seguir como tooinstall e usar **Git para Windows**, embora você pode escolher qualquer pacote que você preferir.</span><span class="sxs-lookup"><span data-stu-id="d23ba-152">hello following examples detail how tooinstall and use **Git for Windows**, though you can choose whichever package you prefer.</span></span> <span data-ttu-id="d23ba-153">**Git para Windows** oferece acesso toosome software de código-fonte aberto adicional ([OSS](https://en.wikipedia.org/wiki/Open-source_software)) ferramentas e utilitários que podem ser úteis ao trabalhar com VMs do Linux.</span><span class="sxs-lookup"><span data-stu-id="d23ba-153">**Git for Windows** gives you access toosome additional open-source software ([OSS](https://en.wikipedia.org/wiki/Open-source_software)) tools and utilities that may be useful as you work with Linux VMs.</span></span>

1. <span data-ttu-id="d23ba-154">Baixe e instale o **Git para Windows** de saudação local a seguir: [https://git-for-windows.github.io/](https://git-for-windows.github.io/).</span><span class="sxs-lookup"><span data-stu-id="d23ba-154">Download and install **Git for Windows** from hello following location: [https://git-for-windows.github.io/](https://git-for-windows.github.io/).</span></span>
2. <span data-ttu-id="d23ba-155">Aceitar opções padrão de saudação durante a saudação processo de instalação, a menos que seja absolutamente necessário toochange-los.</span><span class="sxs-lookup"><span data-stu-id="d23ba-155">Accept hello default options during hello install process unless you specifically need toochange them.</span></span>
3. <span data-ttu-id="d23ba-156">Executar **Git Bash** de saudação **Menu Iniciar** > **Git** > **Git Bash**.</span><span class="sxs-lookup"><span data-stu-id="d23ba-156">Run **Git Bash** from hello **Start Menu** > **Git** > **Git Bash**.</span></span> <span data-ttu-id="d23ba-157">console de saudação parece semelhante toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="d23ba-157">hello console looks similar toohello following example:</span></span>

    ![Shell do Bash do Git para Windows](./media/ssh-from-windows/git-bash-window.png)

## <a name="create-a-private-key"></a><span data-ttu-id="d23ba-159">Criar uma chave privada</span><span class="sxs-lookup"><span data-stu-id="d23ba-159">Create a private key</span></span>
1. <span data-ttu-id="d23ba-160">No seu **Git Bash** janela, use `openssl.exe` toocreate uma chave privada.</span><span class="sxs-lookup"><span data-stu-id="d23ba-160">In your **Git Bash** window, use `openssl.exe` toocreate a private key.</span></span> <span data-ttu-id="d23ba-161">Olá, exemplo a seguir cria uma chave chamada `myPrivateKey` e certificado denominado `myCert.pem`:</span><span class="sxs-lookup"><span data-stu-id="d23ba-161">hello following example creates a key named `myPrivateKey` and certificate named `myCert.pem`:</span></span>

    ```bash
    openssl.exe req -x509 -nodes -days 365 -newkey rsa:2048 \
        -keyout myPrivateKey.key -out myCert.pem
    ```

    <span data-ttu-id="d23ba-162">saída de Hello parece semelhante toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="d23ba-162">hello output looks similar toohello following example:</span></span>

    ```bash
    Generating a 2048 bit RSA private key
    .......................................+++
    .......................+++
    writing new private key too'myPrivateKey.key'
    -----
    You are about toobe asked tooenter information that will be incorporated
    into your certificate request.
    What you are about tooenter is what is called a Distinguished Name or a DN.
    There are quite a few fields but you can leave some blank
    For some fields there will be a default value,
    If you enter '.', hello field will be left blank.
    -----
    Country Name (2 letter code) [AU]:
    ```

   <span data-ttu-id="d23ba-163">Se o bash relatar um erro, tente abrir uma nova janela de **Bash do Git** com privilégios elevados.</span><span class="sxs-lookup"><span data-stu-id="d23ba-163">If bash reports an error, try opening a new **Git Bash** window with elevated privileges.</span></span> <span data-ttu-id="d23ba-164">Em seguida, execute novamente a saudação `openssl` comando.</span><span class="sxs-lookup"><span data-stu-id="d23ba-164">Then, rerun hello `openssl` command.</span></span>

2. <span data-ttu-id="d23ba-165">Saudação de resposta solicita o nome de país, local, nome da organização, etc.</span><span class="sxs-lookup"><span data-stu-id="d23ba-165">Answer hello prompts for country name, location, organization name, etc.</span></span>
3. <span data-ttu-id="d23ba-166">A chave e o certificado novos são criados no diretório atual de trabalho.</span><span class="sxs-lookup"><span data-stu-id="d23ba-166">Your new private key and certificate are created in your current working directory.</span></span> <span data-ttu-id="d23ba-167">Como medida de segurança, você deve definir as permissões de saudação em sua chave privada para que somente você pode acessá-lo:</span><span class="sxs-lookup"><span data-stu-id="d23ba-167">As a security measure, you should set hello permissions on your private key so that only you can access it:</span></span>

    ```bash
    chmod 0600 myPrivateKey.key
    ```

4. <span data-ttu-id="d23ba-168">Olá [próxima seção](#create-a-private-key-for-putty) detalhes usando PuTTYgen tooboth exibir e usar a chave pública hello e criar uma chave privada específicos para usar PuTTY tooSSH tooLinux VMs.</span><span class="sxs-lookup"><span data-stu-id="d23ba-168">hello [next section](#create-a-private-key-for-putty) details using PuTTYgen tooboth view and use hello public key, and create a private key specific for using PuTTY tooSSH tooLinux VMs.</span></span> <span data-ttu-id="d23ba-169">comando a seguir Hello gera um arquivo de chave pública denominado `myPublicKey.key` que você pode usar imediatamente:</span><span class="sxs-lookup"><span data-stu-id="d23ba-169">hello following command generates a public key file named `myPublicKey.key` that you can use right away:</span></span>

    ```bash
    openssl.exe rsa -pubout -in myPrivateKey.key -out myPublicKey.key
    ```

5. <span data-ttu-id="d23ba-170">Se você precisar de recursos de clássico toomanage também, converter Olá `myCert.pem` muito`myCert.cer` (X509 codificado em DER certificado).</span><span class="sxs-lookup"><span data-stu-id="d23ba-170">If you also need toomanage Classic resources, convert hello `myCert.pem` too`myCert.cer` (DER encoded X509 certificate).</span></span> <span data-ttu-id="d23ba-171">Executar esta etapa opcional somente se você precisar toospecifically gerenciar recursos de clássico mais antigos.</span><span class="sxs-lookup"><span data-stu-id="d23ba-171">Perform this optional step only if you need toospecifically manage older Classic resources.</span></span>

    <span data-ttu-id="d23ba-172">Converta o certificado de saudação usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="d23ba-172">Convert hello certificate using hello following command:</span></span>

    ```bash
    openssl.exe  x509 -outform der -in myCert.pem -out myCert.cer
    ```

## <a name="create-a-private-key-for-putty"></a><span data-ttu-id="d23ba-173">Criar uma chave privada para PuTTY</span><span class="sxs-lookup"><span data-stu-id="d23ba-173">Create a private key for PuTTY</span></span>
<span data-ttu-id="d23ba-174">O PuTTY é um cliente SSH comum do Windows.</span><span class="sxs-lookup"><span data-stu-id="d23ba-174">PuTTY is a common SSH client for Windows.</span></span> <span data-ttu-id="d23ba-175">Você está livre toouse qualquer cliente SSH que desejar.</span><span class="sxs-lookup"><span data-stu-id="d23ba-175">You are free toouse any SSH client that you wish.</span></span> <span data-ttu-id="d23ba-176">toouse PuTTY, você precisa toocreate um tipo de chave - uma chave privada de PuTTY (PPK) adicional.</span><span class="sxs-lookup"><span data-stu-id="d23ba-176">toouse PuTTY, you need toocreate an additional type of key - a PuTTY Private Key (PPK).</span></span> <span data-ttu-id="d23ba-177">Se você não desejar toouse PuTTY, ignore esta seção.</span><span class="sxs-lookup"><span data-stu-id="d23ba-177">If you do not wish toouse PuTTY, skip this section.</span></span>

<span data-ttu-id="d23ba-178">Olá, exemplo a seguir cria essa chave privada adicional especificamente para toouse PuTTY:</span><span class="sxs-lookup"><span data-stu-id="d23ba-178">hello following example creates this additional private key specifically for PuTTY toouse:</span></span>

1. <span data-ttu-id="d23ba-179">Use **Git Bash** tooconvert seu privada da chave em uma chave privada do RSA que PuTTYgen pode entender.</span><span class="sxs-lookup"><span data-stu-id="d23ba-179">Use **Git Bash** tooconvert your private key into an RSA private key that PuTTYgen can understand.</span></span> <span data-ttu-id="d23ba-180">Olá, exemplo a seguir cria uma chave chamada `myPrivateKey_rsa` da chave existente de saudação chamado `myPrivateKey`:</span><span class="sxs-lookup"><span data-stu-id="d23ba-180">hello following example creates a key named `myPrivateKey_rsa` from hello existing key named `myPrivateKey`:</span></span>

    ```bash
    openssl rsa -in ./myPrivateKey.key -out myPrivateKey_rsa
    ```

    <span data-ttu-id="d23ba-181">Como medida de segurança, você deve definir as permissões de saudação em sua chave privada para que somente você pode acessá-lo:</span><span class="sxs-lookup"><span data-stu-id="d23ba-181">As a security measure, you should set hello permissions on your private key so that only you can access it:</span></span>

    ```bash
    chmod 0600 myPrivateKey_rsa
    ```
2. <span data-ttu-id="d23ba-182">Baixar e executar PuTTYgen Olá local a seguir: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span><span class="sxs-lookup"><span data-stu-id="d23ba-182">Download and run PuTTYgen from hello following location: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span></span>
3. <span data-ttu-id="d23ba-183">Clique em menu Olá: **arquivo** > **chave privada de carga**</span><span class="sxs-lookup"><span data-stu-id="d23ba-183">Click hello menu: **File** > **Load Private Key**</span></span>
4. <span data-ttu-id="d23ba-184">Localize sua chave privada (`myPrivateKey_rsa` no exemplo anterior de saudação).</span><span class="sxs-lookup"><span data-stu-id="d23ba-184">Locate your private key (`myPrivateKey_rsa` in hello previous example).</span></span> <span data-ttu-id="d23ba-185">diretório padrão de Hello quando você iniciar **Git Bash** é `C:\Users\%username%`.</span><span class="sxs-lookup"><span data-stu-id="d23ba-185">hello default directory when you start **Git Bash** is `C:\Users\%username%`.</span></span> <span data-ttu-id="d23ba-186">Alterar tooshow de filtro de arquivo hello **todos os arquivos (\*.\*)** :</span><span class="sxs-lookup"><span data-stu-id="d23ba-186">Change hello file filter tooshow **All Files (\*.\*)**:</span></span>

    ![Carregar a chave privada existente de saudação em PuTTYgen](./media/ssh-from-windows/load-private-key.png)
5. <span data-ttu-id="d23ba-188">Clique em **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="d23ba-188">Click **Open**.</span></span> <span data-ttu-id="d23ba-189">Um prompt indica que essa chave Olá foi importado com êxito:</span><span class="sxs-lookup"><span data-stu-id="d23ba-189">A prompt indicates that hello key has been successfully imported:</span></span>

    ![Chave tooPuTTYgen foram importados com êxito](./media/ssh-from-windows/successfully-imported-key.png)
6. <span data-ttu-id="d23ba-191">Clique em **Okey** tooclose prompt de saudação.</span><span class="sxs-lookup"><span data-stu-id="d23ba-191">Click **OK** tooclose hello prompt.</span></span>
7. <span data-ttu-id="d23ba-192">chave pública Olá é exibido na parte superior de saudação do hello **PuTTYgen** janela.</span><span class="sxs-lookup"><span data-stu-id="d23ba-192">hello public key is displayed at hello top of hello **PuTTYgen** window.</span></span> <span data-ttu-id="d23ba-193">Copie e cole essa chave pública Olá portal do Azure ou o modelo do Gerenciador de recursos do Azure quando você criar uma VM do Linux.</span><span class="sxs-lookup"><span data-stu-id="d23ba-193">You copy and paste this public key into hello Azure portal or Azure Resource Manager template when you create a Linux VM.</span></span> <span data-ttu-id="d23ba-194">Você também pode clicar em **salva a chave pública** toosave um computador tooyour de cópia:</span><span class="sxs-lookup"><span data-stu-id="d23ba-194">You can also click **Save public key** toosave a copy tooyour computer:</span></span>

    ![Salvar o arquivo de chave pública PuTTY](./media/ssh-from-windows/save-public-key.png)

    <span data-ttu-id="d23ba-196">Olá exemplo a seguir mostra como você copie e cole essa chave pública a saudação portal do Azure quando você criar uma VM do Linux.</span><span class="sxs-lookup"><span data-stu-id="d23ba-196">hello following example shows how you would copy and paste this public key into hello Azure portal when you create a Linux VM.</span></span> <span data-ttu-id="d23ba-197">chave pública Olá normalmente é armazenado no `~/.ssh/authorized_keys` em sua nova VM.</span><span class="sxs-lookup"><span data-stu-id="d23ba-197">hello public key is typically then stored in `~/.ssh/authorized_keys` on your new VM.</span></span>

    ![Use a chave pública quando você cria uma máquina virtual no hello portal do Azure](./media/ssh-from-windows/use-public-key-azure-portal.png)
8. <span data-ttu-id="d23ba-199">De volta ao **PuTTYgen**, clique em **Salvar chave privada**:</span><span class="sxs-lookup"><span data-stu-id="d23ba-199">Back in **PuTTYgen**, Click **Save private Key**:</span></span>

    ![Salvar o arquivo de chave privada PuTTY](./media/ssh-from-windows/save-ppk-file.png)

   > [!WARNING]
   > <span data-ttu-id="d23ba-201">Um prompt solicita se você deseja toocontinue sem inserir uma senha para a sua chave.</span><span class="sxs-lookup"><span data-stu-id="d23ba-201">A prompt asks if you wish toocontinue without entering a passphrase for your key.</span></span> <span data-ttu-id="d23ba-202">Uma frase secreta é como uma chave privada de tooyour anexado de senha.</span><span class="sxs-lookup"><span data-stu-id="d23ba-202">A passphrase is like a password attached tooyour private key.</span></span> <span data-ttu-id="d23ba-203">Mesmo se alguém tooobtain sua chave privada, eles ainda não seria capaz de tooauthenticate usando apenas a chave de saudação.</span><span class="sxs-lookup"><span data-stu-id="d23ba-203">Even if someone were tooobtain your private key, they still would not be able tooauthenticate using just hello key.</span></span> <span data-ttu-id="d23ba-204">Também precisam Olá senha.</span><span class="sxs-lookup"><span data-stu-id="d23ba-204">They would also need hello passphrase.</span></span> <span data-ttu-id="d23ba-205">Sem uma senha, se alguém obtiver sua chave privada, que possam fazer logon no tooany VM ou serviço que usa essa chave.</span><span class="sxs-lookup"><span data-stu-id="d23ba-205">Without a passphrase, if someone obtains your private key, they can log in tooany VM or service that uses that key.</span></span> <span data-ttu-id="d23ba-206">É recomendável criar uma frase secreta.</span><span class="sxs-lookup"><span data-stu-id="d23ba-206">We recommend you create a passphrase.</span></span> <span data-ttu-id="d23ba-207">No entanto, não se você esquecer a senha de hello, há nenhuma maneira toorecovê-lo.</span><span class="sxs-lookup"><span data-stu-id="d23ba-207">However, if you forget hello passphrase, there is no way toorecover it.</span></span>
   >
   >

    <span data-ttu-id="d23ba-208">Se você desejar tooenter uma senha, clique em **não**, insira uma senha na janela principal de PuTTYgen hello e, em seguida, clique em **salva a chave privada** novamente.</span><span class="sxs-lookup"><span data-stu-id="d23ba-208">If you wish tooenter a passphrase, click **No**, enter a passphrase in hello main PuTTYgen window, and then click **Save private key** again.</span></span> <span data-ttu-id="d23ba-209">Caso contrário, clique em **Sim** toocontinue sem fornecer a senha opcional hello.</span><span class="sxs-lookup"><span data-stu-id="d23ba-209">Otherwise, click **Yes** toocontinue without providing hello optional passphrase.</span></span>
9. <span data-ttu-id="d23ba-210">Insira um nome e local toosave seu arquivo PPK.</span><span class="sxs-lookup"><span data-stu-id="d23ba-210">Enter a name and location toosave your PPK file.</span></span>

## <a name="use-putty-toossh-tooa-linux-machine"></a><span data-ttu-id="d23ba-211">Usar Putty tooSSH tooa computador Linux</span><span class="sxs-lookup"><span data-stu-id="d23ba-211">Use Putty tooSSH tooa Linux Machine</span></span>
<span data-ttu-id="d23ba-212">Repetindo, PuTTY é um cliente de SSH comum do Windows.</span><span class="sxs-lookup"><span data-stu-id="d23ba-212">Again, PuTTY is a common SSH client for Windows.</span></span> <span data-ttu-id="d23ba-213">Você está livre toouse qualquer cliente SSH que desejar.</span><span class="sxs-lookup"><span data-stu-id="d23ba-213">You are free toouse any SSH client that you wish.</span></span> <span data-ttu-id="d23ba-214">Olá detalhes de etapas a seguir como toouse seu tooauthenticate chave privada com sua VM do Azure usando o SSH.</span><span class="sxs-lookup"><span data-stu-id="d23ba-214">hello following steps detail how toouse your private key tooauthenticate with your Azure VM using SSH.</span></span> <span data-ttu-id="d23ba-215">etapas de saudação são semelhantes em outros clientes de chave SSH em termos de necessidade tooload seu Olá tooauthenticate chave privada conexão SSH.</span><span class="sxs-lookup"><span data-stu-id="d23ba-215">hello steps are similar in other SSH key clients in terms of needing tooload your private key tooauthenticate hello SSH connection.</span></span>

1. <span data-ttu-id="d23ba-216">Download e execução putty do hello seguinte local: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span><span class="sxs-lookup"><span data-stu-id="d23ba-216">Download and run putty from hello following location: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span></span>
2. <span data-ttu-id="d23ba-217">Preencha o nome de host de saudação ou endereço IP da VM de saudação portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="d23ba-217">Fill in hello host name or IP address of your VM from hello Azure portal:</span></span>

    ![Abrir nova conexão PuTTY](./media/ssh-from-windows/putty-new-connection.png)
3. <span data-ttu-id="d23ba-219">Antes de selecionar **Abrir**, clique em **Conexão** > **SSH** > **guia Autenticação**. Procurar tooand selecione sua chave privada:</span><span class="sxs-lookup"><span data-stu-id="d23ba-219">Before selecting **Open**, click **Connection** > **SSH** > **Auth** tab. Browse tooand select your private key:</span></span>

    ![Selecionar a Chave Privada PuTTY para autenticação](./media/ssh-from-windows/putty-auth-dialog.png)
4. <span data-ttu-id="d23ba-221">Clique em **abrir** tooconnect tooyour virtual machine</span><span class="sxs-lookup"><span data-stu-id="d23ba-221">Click **Open** tooconnect tooyour virtual machine</span></span>

## <a name="next-steps"></a><span data-ttu-id="d23ba-222">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d23ba-222">Next steps</span></span>
<span data-ttu-id="d23ba-223">Você também pode gerar as chaves públicas e privadas Olá [usando OS X e Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d23ba-223">You can also generate hello public and private keys [using OS X and Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="d23ba-224">Para obter mais informações sobre Bash para Windows e os benefícios de saudação de ter as ferramentas de OSS prontamente disponíveis no seu computador Windows, consulte [Bash no Ubuntu no Windows](https://msdn.microsoft.com/commandline/wsl/about).</span><span class="sxs-lookup"><span data-stu-id="d23ba-224">For more information about Bash for Windows and hello benefits of having OSS tools readily available on your Windows computer, see [Bash on Ubuntu on Windows](https://msdn.microsoft.com/commandline/wsl/about).</span></span>

<span data-ttu-id="d23ba-225">Se você tiver problemas ao usar SSH tooconnect tooyour VMs do Linux, consulte [solucionar problemas de SSH conexões tooan VM do Linux Azure](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d23ba-225">If you have trouble using SSH tooconnect tooyour Linux VMs, see [Troubleshoot SSH connections tooan Azure Linux VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
