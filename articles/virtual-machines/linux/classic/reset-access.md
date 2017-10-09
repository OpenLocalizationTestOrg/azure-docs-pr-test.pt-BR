---
title: "aaaReset senha de VM do Linux e SSH chave da saudação CLI | Microsoft Docs"
description: "Como toouse Olá extensão VMAccess de saudação do Azure Interface de linha de comando (CLI) tooreset uma senha de VM do Linux ou uma chave SSH, corrija a configuração de SSH hello e verificar a consistência de disco"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: d975eb70-5ff1-40d1-a634-8dd2646dcd17
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: cynthn
ms.openlocfilehash: 1650ad64fb982627ae9f90b1a8209bb56bac7004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-a-linux-vm-password-or-ssh-key-fix-hello-ssh-configuration-and-check-disk-consistency-using-hello-vmaccess-extension"></a><span data-ttu-id="80dc9-103">Como tooreset uma senha de VM do Linux ou chave SSH, corrija a configuração de SSH hello e verificar a consistência de disco usando a extensão VMAccess Olá</span><span class="sxs-lookup"><span data-stu-id="80dc9-103">How tooreset a Linux VM password or SSH key, fix hello SSH configuration, and check disk consistency using hello VMAccess extension</span></span>
<span data-ttu-id="80dc9-104">Se você não pode se conectar a máquina virtual do tooa Linux no Azure devido a uma senha esquecida, uma chave do Secure Shell (SSH) incorreto ou um problema com a configuração de SSH hello, usar Olá extensão VMAccessForLinux com hello CLI do Azure tooreset Olá senha ou chave SSH, corrigir Olá configuração de SSH e verificar a consistência de disco.</span><span class="sxs-lookup"><span data-stu-id="80dc9-104">If you can't connect tooa Linux virtual machine on Azure because of a forgotten password, an incorrect Secure Shell (SSH) key, or a problem with hello SSH configuration, use hello VMAccessForLinux extension with hello Azure CLI tooreset hello password or SSH key, fix hello SSH configuration, and check disk consistency.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="80dc9-105">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="80dc9-105">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="80dc9-106">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="80dc9-106">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="80dc9-107">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="80dc9-107">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="80dc9-108">Saiba como muito[executar essas etapas usando o modelo do Gerenciador de recursos de saudação](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span><span class="sxs-lookup"><span data-stu-id="80dc9-108">Learn how too[perform these steps using hello Resource Manager model](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span></span>

<span data-ttu-id="80dc9-109">Com hello CLI do Azure, você usar Olá **conjunto de extensão de vm do azure** comando comandos de tooaccess sua interface de linha de comando (Bash, Terminal, prompt de comando).</span><span class="sxs-lookup"><span data-stu-id="80dc9-109">With hello Azure CLI, you use hello **azure vm extension set** command from your command-line interface (Bash, Terminal, Command prompt) tooaccess commands.</span></span> <span data-ttu-id="80dc9-110">Execute **azure help vm extension set** para ver o uso detalhado da extensão.</span><span class="sxs-lookup"><span data-stu-id="80dc9-110">Run **azure help vm extension set** for detailed extension usage.</span></span>

<span data-ttu-id="80dc9-111">Com hello CLI do Azure, você pode fazer Olá seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="80dc9-111">With hello Azure CLI, you can do hello following tasks:</span></span>

* [<span data-ttu-id="80dc9-112">Redefinir senha Olá</span><span class="sxs-lookup"><span data-stu-id="80dc9-112">Reset hello password</span></span>](#pwresetcli)
* [<span data-ttu-id="80dc9-113">Redefinir a chave SSH Olá</span><span class="sxs-lookup"><span data-stu-id="80dc9-113">Reset hello SSH key</span></span>](#sshkeyresetcli)
* [<span data-ttu-id="80dc9-114">Redefinir a chave SSH de senha e Olá Olá</span><span class="sxs-lookup"><span data-stu-id="80dc9-114">Reset hello password and hello SSH key</span></span>](#resetbothcli)
* [<span data-ttu-id="80dc9-115">Criar uma nova conta de usuário sudo</span><span class="sxs-lookup"><span data-stu-id="80dc9-115">Create a new sudo user account</span></span>](#createnewsudocli)
* [<span data-ttu-id="80dc9-116">Redefinir a configuração de SSH Olá</span><span class="sxs-lookup"><span data-stu-id="80dc9-116">Reset hello SSH configuration</span></span>](#sshconfigresetcli)
* [<span data-ttu-id="80dc9-117">Excluir um usuário</span><span class="sxs-lookup"><span data-stu-id="80dc9-117">Delete a user</span></span>](#deletecli)
* [<span data-ttu-id="80dc9-118">Exibir status Olá Olá extensão VMAccess</span><span class="sxs-lookup"><span data-stu-id="80dc9-118">Display hello status of hello VMAccess extension</span></span>](#statuscli)
* [<span data-ttu-id="80dc9-119">Verificar a consistência dos discos adicionados</span><span class="sxs-lookup"><span data-stu-id="80dc9-119">Check consistency of added disks</span></span>](#checkdisk)
* [<span data-ttu-id="80dc9-120">Reparar discos adicionados na sua VM do Linux</span><span class="sxs-lookup"><span data-stu-id="80dc9-120">Repair added disks on your Linux VM</span></span>](#repairdisk)

## <a name="prerequisites"></a><span data-ttu-id="80dc9-121">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="80dc9-121">Prerequisites</span></span>
<span data-ttu-id="80dc9-122">Você precisará a seguir Olá toodo:</span><span class="sxs-lookup"><span data-stu-id="80dc9-122">You will need toodo hello following:</span></span>

* <span data-ttu-id="80dc9-123">Você precisará de muito[instalar Olá CLI do Azure](../../../cli-install-nodejs.md) e [conectar assinatura tooyour](../../../xplat-cli-connect.md) toouse Azure recursos associados à sua conta.</span><span class="sxs-lookup"><span data-stu-id="80dc9-123">You will need too[install hello Azure CLI](../../../cli-install-nodejs.md) and [connect tooyour subscription](../../../xplat-cli-connect.md) toouse Azure resources associated with your account.</span></span>
* <span data-ttu-id="80dc9-124">Conjunto Olá modo correto para modelo de implantação clássico Olá digitando o seguinte Olá no prompt de comando hello:</span><span class="sxs-lookup"><span data-stu-id="80dc9-124">Set hello correct mode for hello classic deployment model by typing hello following at hello command prompt:</span></span>
    ``` 
        azure config mode asm
    ```
* <span data-ttu-id="80dc9-125">Tem uma nova senha ou um conjunto de chaves SSH, se você quiser tooreset qualquer um.</span><span class="sxs-lookup"><span data-stu-id="80dc9-125">Have a new password or set of SSH keys, if you want tooreset either one.</span></span> <span data-ttu-id="80dc9-126">Você não precisa dessas se desejar que a configuração de SSH tooreset hello.</span><span class="sxs-lookup"><span data-stu-id="80dc9-126">You don't need these if you want tooreset hello SSH configuration.</span></span>

## <span data-ttu-id="80dc9-127"><a name="pwresetcli"></a>Redefinir senha Olá</span><span class="sxs-lookup"><span data-stu-id="80dc9-127"><a name="pwresetcli"></a>Reset hello password</span></span>
1. <span data-ttu-id="80dc9-128">Crie um arquivo no seu computador local chamado PrivateConf.json com essas linhas.</span><span class="sxs-lookup"><span data-stu-id="80dc9-128">Create a file on your local computer named PrivateConf.json with these lines.</span></span> <span data-ttu-id="80dc9-129">Substitua **myUserName** e **myP@ssW0rd** pelo seu próprio nome de usuário e senha e defina sua própria data de expiração.</span><span class="sxs-lookup"><span data-stu-id="80dc9-129">Replace **myUserName** and **myP@ssW0rd** with your own user name and password and set your own date for expiration.</span></span>

    ```   
        {
        "username":"myUserName",
        "password":"myP@ssW0rd",
        "expiration":"2020-01-01"
        }
    ```
        
2. <span data-ttu-id="80dc9-130">Execute este comando, substituindo Olá nome da máquina virtual para **myVM**.</span><span class="sxs-lookup"><span data-stu-id="80dc9-130">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* –-private-config-path PrivateConf.json
    ```

## <span data-ttu-id="80dc9-131"><a name="sshkeyresetcli"></a>Redefinir a chave SSH Olá</span><span class="sxs-lookup"><span data-stu-id="80dc9-131"><a name="sshkeyresetcli"></a>Reset hello SSH key</span></span>
1. <span data-ttu-id="80dc9-132">Crie um arquivo chamado PrivateConf.json com esse conteúdo.</span><span class="sxs-lookup"><span data-stu-id="80dc9-132">Create a file named PrivateConf.json with these contents.</span></span> <span data-ttu-id="80dc9-133">Substituir saudação **myUserName** e **mySSHKey** valores com suas próprias informações.</span><span class="sxs-lookup"><span data-stu-id="80dc9-133">Replace hello **myUserName** and **mySSHKey** values with your own information.</span></span>

    ```   
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey"
        }
    ```
2. <span data-ttu-id="80dc9-134">Execute este comando, substituindo Olá nome da máquina virtual para **myVM**.</span><span class="sxs-lookup"><span data-stu-id="80dc9-134">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span>
   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json

## <span data-ttu-id="80dc9-135"><a name="resetbothcli"></a>Redefinir senha hello e a chave SSH Olá</span><span class="sxs-lookup"><span data-stu-id="80dc9-135"><a name="resetbothcli"></a>Reset both hello password and hello SSH key</span></span>
1. <span data-ttu-id="80dc9-136">Crie um arquivo chamado PrivateConf.json com esse conteúdo.</span><span class="sxs-lookup"><span data-stu-id="80dc9-136">Create a file named PrivateConf.json with these contents.</span></span> <span data-ttu-id="80dc9-137">Substituir saudação **myUserName**, **mySSHKey** e  **myP@ssW0rd**  valores com suas próprias informações.</span><span class="sxs-lookup"><span data-stu-id="80dc9-137">Replace hello **myUserName**, **mySSHKey** and **myP@ssW0rd** values with your own information.</span></span>

    ``` 
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey",
        "password":"myP@ssW0rd"
        }
    ```

2. <span data-ttu-id="80dc9-138">Execute este comando, substituindo Olá nome da máquina virtual para **myVM**.</span><span class="sxs-lookup"><span data-stu-id="80dc9-138">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set MyVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="80dc9-139"><a name="createnewsudocli"></a>Criar uma nova conta de usuário sudo</span><span class="sxs-lookup"><span data-stu-id="80dc9-139"><a name="createnewsudocli"></a>Create a new sudo user account</span></span>

<span data-ttu-id="80dc9-140">Se você esquecer o nome de usuário, você pode usar VMAccess toocreate um novo com a autoridade de sudo hello.</span><span class="sxs-lookup"><span data-stu-id="80dc9-140">If you forget your user name, you can use VMAccess toocreate a new one with hello sudo authority.</span></span> <span data-ttu-id="80dc9-141">Olá nesse caso, o nome de usuário e senha não será modificada.</span><span class="sxs-lookup"><span data-stu-id="80dc9-141">In this case, hello existing user name and password will not be modified.</span></span>

<span data-ttu-id="80dc9-142">toocreate um novo usuário sudo com acesso de senha, use script de saudação em [redefinição da senha Olá](#pwresetcli) e especifique o novo nome de usuário hello.</span><span class="sxs-lookup"><span data-stu-id="80dc9-142">toocreate a new sudo user with password access, use hello script in [Reset hello password](#pwresetcli) and specify hello new user name.</span></span>

<span data-ttu-id="80dc9-143">toocreate um novo usuário sudo com acesso de chave SSH, usar o script de saudação em [chave SSH Olá redefinição](#sshkeyresetcli) e especifique o novo nome de usuário hello.</span><span class="sxs-lookup"><span data-stu-id="80dc9-143">toocreate a new sudo user with SSH key access, use hello script in [Reset hello SSH key](#sshkeyresetcli) and specify hello new user name.</span></span>

<span data-ttu-id="80dc9-144">Você também pode usar [Redefinir senha hello e a chave SSH Olá](#resetbothcli) toocreate um novo usuário com senha e o acesso à chave de SSH.</span><span class="sxs-lookup"><span data-stu-id="80dc9-144">You can also use [Reset hello password and hello SSH key](#resetbothcli) toocreate a new user with both password and SSH key access.</span></span>

## <span data-ttu-id="80dc9-145"><a name="sshconfigresetcli"></a>Redefinir a configuração de SSH Olá</span><span class="sxs-lookup"><span data-stu-id="80dc9-145"><a name="sshconfigresetcli"></a>Reset hello SSH configuration</span></span>
<span data-ttu-id="80dc9-146">Se a configuração de SSH hello está em um estado indesejado, você também poderá perder acesso toohello VM.</span><span class="sxs-lookup"><span data-stu-id="80dc9-146">If hello SSH configuration is in an undesired state, you might also lose access toohello VM.</span></span> <span data-ttu-id="80dc9-147">Você pode usar o hello VMAccess extensão tooreset Olá configuração tooits estado padrão.</span><span class="sxs-lookup"><span data-stu-id="80dc9-147">You can use hello VMAccess extension tooreset hello configuration tooits default state.</span></span> <span data-ttu-id="80dc9-148">toodo assim, você apenas precisa tooset hello "reset_ssh" chave muito "True".</span><span class="sxs-lookup"><span data-stu-id="80dc9-148">toodo so, you just need tooset hello “reset_ssh” key too“True”.</span></span> <span data-ttu-id="80dc9-149">extensão Olá reiniciar o servidor SSH Olá, abra a porta na sua VM SSH Olá e redefinir Olá SSH configuração toodefault valores.</span><span class="sxs-lookup"><span data-stu-id="80dc9-149">hello extension will restart hello SSH server, open hello SSH port on your VM, and reset hello SSH configuration toodefault values.</span></span> <span data-ttu-id="80dc9-150">conta de usuário da saudação (nome, a senha ou as chaves de SSH) não será alterada.</span><span class="sxs-lookup"><span data-stu-id="80dc9-150">hello user account (name, password or SSH keys) will not be changed.</span></span>

> [!NOTE]
> <span data-ttu-id="80dc9-151">arquivo de configuração do SSH Olá é redefinido está localizado em /etc/ssh/sshd_config.</span><span class="sxs-lookup"><span data-stu-id="80dc9-151">hello SSH configuration file that gets reset is located at /etc/ssh/sshd_config.</span></span>
> 
> 

1. <span data-ttu-id="80dc9-152">Crie um arquivo chamado PrivateConf.json com esse conteúdo.</span><span class="sxs-lookup"><span data-stu-id="80dc9-152">Create a file named PrivateConf.json with this content.</span></span>

    ```   
        {
        "reset_ssh":"True"
        }
    ```

2. <span data-ttu-id="80dc9-153">Execute este comando, substituindo Olá nome da máquina virtual para **myVM**.</span><span class="sxs-lookup"><span data-stu-id="80dc9-153">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span> 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="80dc9-154"><a name="deletecli"></a>Excluir um usuário</span><span class="sxs-lookup"><span data-stu-id="80dc9-154"><a name="deletecli"></a>Delete a user</span></span>
<span data-ttu-id="80dc9-155">Se você quiser toodelete uma conta de usuário sem efetuar login no toohello VM diretamente, você pode usar esse script.</span><span class="sxs-lookup"><span data-stu-id="80dc9-155">If you want toodelete a user account without logging into toohello VM directly, you can use this script.</span></span>

1. <span data-ttu-id="80dc9-156">Crie um arquivo chamado PrivateConf.json com esse conteúdo, substituindo Olá tooremove de nome de usuário para **removeUserName**.</span><span class="sxs-lookup"><span data-stu-id="80dc9-156">Create a file named PrivateConf.json with this content, substituting hello user name tooremove for **removeUserName**.</span></span> 

    ```   
        {
        "remove_user":"removeUserName"
        }
    ```

2. <span data-ttu-id="80dc9-157">Execute este comando, substituindo Olá nome da máquina virtual para **myVM**.</span><span class="sxs-lookup"><span data-stu-id="80dc9-157">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span> 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="80dc9-158"><a name="statuscli"></a>Exibir status Olá Olá extensão VMAccess</span><span class="sxs-lookup"><span data-stu-id="80dc9-158"><a name="statuscli"></a>Display hello status of hello VMAccess extension</span></span>
<span data-ttu-id="80dc9-159">status toodisplay Olá Olá extensão VMAccess, execute este comando.</span><span class="sxs-lookup"><span data-stu-id="80dc9-159">toodisplay hello status of hello VMAccess extension, run this command.</span></span>

```
        azure vm extension get
```

## <span data-ttu-id="80dc9-160"><a name='checkdisk'></a>Verificar a consistência dos discos adicionados</span><span class="sxs-lookup"><span data-stu-id="80dc9-160"><a name='checkdisk'></a>Check consistency of added disks</span></span>
<span data-ttu-id="80dc9-161">toorun fsck em todos os discos em sua máquina virtual do Linux, você precisará a seguir Olá toodo:</span><span class="sxs-lookup"><span data-stu-id="80dc9-161">toorun fsck on all disks in your Linux virtual machine, you will need toodo hello following:</span></span>

1. <span data-ttu-id="80dc9-162">Crie um arquivo chamado PublicConf.json com esse conteúdo.</span><span class="sxs-lookup"><span data-stu-id="80dc9-162">Create a file named PublicConf.json with this content.</span></span> <span data-ttu-id="80dc9-163">Verificar disco tem um valor booleano para se toocheck discos anexados a máquina virtual de tooyour ou não.</span><span class="sxs-lookup"><span data-stu-id="80dc9-163">Check Disk takes a boolean for whether toocheck disks attached tooyour virtual machine or not.</span></span> 

    ```   
        {   
        "check_disk": "true"
        }
    ```

2. <span data-ttu-id="80dc9-164">Executar tooexecute esse comando, substituindo Olá nome da máquina virtual para **myVM**.</span><span class="sxs-lookup"><span data-stu-id="80dc9-164">Run this command tooexecute, substituting hello name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json 
    ```

## <span data-ttu-id="80dc9-165"><a name='repairdisk'></a>Reparar discos</span><span class="sxs-lookup"><span data-stu-id="80dc9-165"><a name='repairdisk'></a>Repair disks</span></span>
<span data-ttu-id="80dc9-166">discos toorepair não montar ou que possuem erros de configuração de montagem, use Olá VMAccess tooreset Olá montagem configuração da extensão na sua máquina virtual do Linux.</span><span class="sxs-lookup"><span data-stu-id="80dc9-166">toorepair disks that are not mounting or have mount configuration errors, use hello VMAccess extension tooreset hello mount configuration on your Linux virtual machine.</span></span> <span data-ttu-id="80dc9-167">Substituindo o nome de saudação do disco para **myDisk**.</span><span class="sxs-lookup"><span data-stu-id="80dc9-167">Substituting hello name of your disk for **myDisk**.</span></span>

1. <span data-ttu-id="80dc9-168">Crie um arquivo chamado PublicConf.json com esse conteúdo.</span><span class="sxs-lookup"><span data-stu-id="80dc9-168">Create a file named PublicConf.json with this content.</span></span> 

    ```   
        {
        "repair_disk":"true",
        "disk_name":"myDisk"
        }
    ```

2. <span data-ttu-id="80dc9-169">Executar tooexecute esse comando, substituindo Olá nome da máquina virtual para **myVM**.</span><span class="sxs-lookup"><span data-stu-id="80dc9-169">Run this command tooexecute, substituting hello name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json
    ```

## <a name="next-steps"></a><span data-ttu-id="80dc9-170">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="80dc9-170">Next steps</span></span>
* <span data-ttu-id="80dc9-171">Se você quiser toouse cmdlets do PowerShell do Azure ou a senha do Gerenciador de recursos do Azure modelos tooreset hello ou a chave SSH, corrija a configuração de SSH Olá e verificar a consistência de disco, consulte Olá [documentação de extensão VMAccess no GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span><span class="sxs-lookup"><span data-stu-id="80dc9-171">If you want toouse Azure PowerShell cmdlets or Azure Resource Manager templates tooreset hello password or SSH key, fix hello SSH configuration, and check disk consistency, see hello [VMAccess extension documentation on GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span></span> 
* <span data-ttu-id="80dc9-172">Você também pode usar o hello [portal do Azure](https://portal.azure.com) tooreset senha de saudação ou chave SSH de uma VM do Linux implantadas no modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="80dc9-172">You can also use hello [Azure portal](https://portal.azure.com) tooreset hello password or SSH key of a Linux VM deployed in hello classic deployment model.</span></span> <span data-ttu-id="80dc9-173">No momento, você não pode usar saudação portal toothis para uma VM do Linux é implantado no modelo de implantação do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="80dc9-173">You can't currently use hello portal do toothis for a Linux VM deployed in hello Resource Manager deployment model.</span></span>
* <span data-ttu-id="80dc9-174">Veja [Sobre os recursos e extensões de máquina virtual](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obter mais informações sobre como usar extensões de VM para máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="80dc9-174">See [About virtual machine extensions and features](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more about using VM extensions for Azure virtual machines.</span></span>

