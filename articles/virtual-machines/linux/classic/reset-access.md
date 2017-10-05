---
title: Redefinir chave SSH e senha de VM do Linux da CLI | Microsoft Docs
description: "Como usar a extensão VMAccess da CLI (Interface de linha de comando) do Azure para redefinir uma chave SSH ou uma senha de VM do Linux, corrigir a configuração de SSH e verificar a consistência de disco"
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
ms.openlocfilehash: 74765877e7836d6878284b350a25d8355dc83d7d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-reset-a-linux-vm-password-or-ssh-key-fix-the-ssh-configuration-and-check-disk-consistency-using-the-vmaccess-extension"></a><span data-ttu-id="ab357-103">Como redefinir uma senha de VM do Linux ou chave SSH, corrigir a configuração de SSH e verificar a consistência de disco usando a extensão VMAccess</span><span class="sxs-lookup"><span data-stu-id="ab357-103">How to reset a Linux VM password or SSH key, fix the SSH configuration, and check disk consistency using the VMAccess extension</span></span>
<span data-ttu-id="ab357-104">Se você não pode se conectar a uma máquina virtual Linux no Azure devido a uma senha esquecida, uma chave do Secure Shell (SSH) incorreta ou um problema com a configuração do SSH, use a extensão VMAccessForLinux com a CLI do Azure para redefinir a senha ou chave SSH ou corrigir a configuração do SSH e verificar a consistência do disco.</span><span class="sxs-lookup"><span data-stu-id="ab357-104">If you can't connect to a Linux virtual machine on Azure because of a forgotten password, an incorrect Secure Shell (SSH) key, or a problem with the SSH configuration, use the VMAccessForLinux extension with the Azure CLI to reset the password or SSH key, fix the SSH configuration, and check disk consistency.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="ab357-105">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ab357-105">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ab357-106">Este artigo aborda o uso do modelo de implantação Clássica.</span><span class="sxs-lookup"><span data-stu-id="ab357-106">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="ab357-107">A Microsoft recomenda que a maioria das implantações novas use o modelo do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="ab357-107">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="ab357-108">Saiba como [executar estas etapas usando o modelo do Resource Manager](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span><span class="sxs-lookup"><span data-stu-id="ab357-108">Learn how to [perform these steps using the Resource Manager model](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span></span>

<span data-ttu-id="ab357-109">Com a CLI do Azure, você poderá usar o comando **azure vm extension set** na sua interface de linha de comando (Bash, Terminal, Prompt de comando) para acessar comandos.</span><span class="sxs-lookup"><span data-stu-id="ab357-109">With the Azure CLI, you use the **azure vm extension set** command from your command-line interface (Bash, Terminal, Command prompt) to access commands.</span></span> <span data-ttu-id="ab357-110">Execute **azure help vm extension set** para ver o uso detalhado da extensão.</span><span class="sxs-lookup"><span data-stu-id="ab357-110">Run **azure help vm extension set** for detailed extension usage.</span></span>

<span data-ttu-id="ab357-111">Com o CLI do Azure, você pode realizar as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="ab357-111">With the Azure CLI, you can do the following tasks:</span></span>

* [<span data-ttu-id="ab357-112">Redefinir a senha</span><span class="sxs-lookup"><span data-stu-id="ab357-112">Reset the password</span></span>](#pwresetcli)
* [<span data-ttu-id="ab357-113">Redefinir a chave SSH</span><span class="sxs-lookup"><span data-stu-id="ab357-113">Reset the SSH key</span></span>](#sshkeyresetcli)
* [<span data-ttu-id="ab357-114">Redefinir a senha e a chave SSH</span><span class="sxs-lookup"><span data-stu-id="ab357-114">Reset the password and the SSH key</span></span>](#resetbothcli)
* [<span data-ttu-id="ab357-115">Criar uma nova conta de usuário sudo</span><span class="sxs-lookup"><span data-stu-id="ab357-115">Create a new sudo user account</span></span>](#createnewsudocli)
* [<span data-ttu-id="ab357-116">Redefinir a configuração de SSH</span><span class="sxs-lookup"><span data-stu-id="ab357-116">Reset the SSH configuration</span></span>](#sshconfigresetcli)
* [<span data-ttu-id="ab357-117">Excluir um usuário</span><span class="sxs-lookup"><span data-stu-id="ab357-117">Delete a user</span></span>](#deletecli)
* [<span data-ttu-id="ab357-118">Exibir o status da extensão VMAccess</span><span class="sxs-lookup"><span data-stu-id="ab357-118">Display the status of the VMAccess extension</span></span>](#statuscli)
* [<span data-ttu-id="ab357-119">Verificar a consistência dos discos adicionados</span><span class="sxs-lookup"><span data-stu-id="ab357-119">Check consistency of added disks</span></span>](#checkdisk)
* [<span data-ttu-id="ab357-120">Reparar discos adicionados na sua VM do Linux</span><span class="sxs-lookup"><span data-stu-id="ab357-120">Repair added disks on your Linux VM</span></span>](#repairdisk)

## <a name="prerequisites"></a><span data-ttu-id="ab357-121">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ab357-121">Prerequisites</span></span>
<span data-ttu-id="ab357-122">Você precisará fazer o seguinte:</span><span class="sxs-lookup"><span data-stu-id="ab357-122">You will need to do the following:</span></span>

* <span data-ttu-id="ab357-123">Você também precisará [instalar a CLI do Azure](../../../cli-install-nodejs.md) e [conectar-se à sua assinatura](../../../xplat-cli-connect.md) para usar recursos do Azure associados à sua conta.</span><span class="sxs-lookup"><span data-stu-id="ab357-123">You will need to [install the Azure CLI](../../../cli-install-nodejs.md) and [connect to your subscription](../../../xplat-cli-connect.md) to use Azure resources associated with your account.</span></span>
* <span data-ttu-id="ab357-124">Defina o modo correto para o modelo de implantação clássico digitando o seguinte no prompt de comando:</span><span class="sxs-lookup"><span data-stu-id="ab357-124">Set the correct mode for the classic deployment model by typing the following at the command prompt:</span></span>
    ``` 
        azure config mode asm
    ```
* <span data-ttu-id="ab357-125">Tenha uma nova senha ou conjunto de chaves SSH, se quiser redefinir um deles.</span><span class="sxs-lookup"><span data-stu-id="ab357-125">Have a new password or set of SSH keys, if you want to reset either one.</span></span> <span data-ttu-id="ab357-126">Você não precisa deles para redefinir a configuração de SSH.</span><span class="sxs-lookup"><span data-stu-id="ab357-126">You don't need these if you want to reset the SSH configuration.</span></span>

## <span data-ttu-id="ab357-127"><a name="pwresetcli"></a>Redefinir a senha</span><span class="sxs-lookup"><span data-stu-id="ab357-127"><a name="pwresetcli"></a>Reset the password</span></span>
1. <span data-ttu-id="ab357-128">Crie um arquivo no seu computador local chamado PrivateConf.json com essas linhas.</span><span class="sxs-lookup"><span data-stu-id="ab357-128">Create a file on your local computer named PrivateConf.json with these lines.</span></span> <span data-ttu-id="ab357-129">Substitua **myUserName** e **myP@ssW0rd** pelo seu próprio nome de usuário e senha e defina sua própria data de expiração.</span><span class="sxs-lookup"><span data-stu-id="ab357-129">Replace **myUserName** and **myP@ssW0rd** with your own user name and password and set your own date for expiration.</span></span>

    ```   
        {
        "username":"myUserName",
        "password":"myP@ssW0rd",
        "expiration":"2020-01-01"
        }
    ```
        
2. <span data-ttu-id="ab357-130">Execute esse comando, substituindo **myVM** pelo nome da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ab357-130">Run this command, substituting the name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* –-private-config-path PrivateConf.json
    ```

## <span data-ttu-id="ab357-131"><a name="sshkeyresetcli"></a>Redefinir a chave SSH</span><span class="sxs-lookup"><span data-stu-id="ab357-131"><a name="sshkeyresetcli"></a>Reset the SSH key</span></span>
1. <span data-ttu-id="ab357-132">Crie um arquivo chamado PrivateConf.json com esse conteúdo.</span><span class="sxs-lookup"><span data-stu-id="ab357-132">Create a file named PrivateConf.json with these contents.</span></span> <span data-ttu-id="ab357-133">Substitua os valores **myUserName** e **mySSHKey** pelas suas próprias informações.</span><span class="sxs-lookup"><span data-stu-id="ab357-133">Replace the **myUserName** and **mySSHKey** values with your own information.</span></span>

    ```   
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey"
        }
    ```
2. <span data-ttu-id="ab357-134">Execute esse comando, substituindo **myVM** pelo nome da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ab357-134">Run this command, substituting the name of your virtual machine for **myVM**.</span></span>
   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json

## <span data-ttu-id="ab357-135"><a name="resetbothcli"></a>Redefinir a senha e a chave SSH</span><span class="sxs-lookup"><span data-stu-id="ab357-135"><a name="resetbothcli"></a>Reset both the password and the SSH key</span></span>
1. <span data-ttu-id="ab357-136">Crie um arquivo chamado PrivateConf.json com esse conteúdo.</span><span class="sxs-lookup"><span data-stu-id="ab357-136">Create a file named PrivateConf.json with these contents.</span></span> <span data-ttu-id="ab357-137">Substitua os valores **myUserName**, **mySSHKey** e **myP@ssW0rd** pelas suas próprias informações.</span><span class="sxs-lookup"><span data-stu-id="ab357-137">Replace the **myUserName**, **mySSHKey** and **myP@ssW0rd** values with your own information.</span></span>

    ``` 
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey",
        "password":"myP@ssW0rd"
        }
    ```

2. <span data-ttu-id="ab357-138">Execute esse comando, substituindo **myVM** pelo nome da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ab357-138">Run this command, substituting the name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set MyVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="ab357-139"><a name="createnewsudocli"></a>Criar uma nova conta de usuário sudo</span><span class="sxs-lookup"><span data-stu-id="ab357-139"><a name="createnewsudocli"></a>Create a new sudo user account</span></span>

<span data-ttu-id="ab357-140">Se você esquecer seu nome de usuário, você pode usar VMAccess para criar um novo com a autoridade sudo.</span><span class="sxs-lookup"><span data-stu-id="ab357-140">If you forget your user name, you can use VMAccess to create a new one with the sudo authority.</span></span> <span data-ttu-id="ab357-141">Nesse caso, o nome de usuário e a senha existente não serão modificados.</span><span class="sxs-lookup"><span data-stu-id="ab357-141">In this case, the existing user name and password will not be modified.</span></span>

<span data-ttu-id="ab357-142">Para criar um novo usuário sudo com senha de acesso, use o script em [Redefinir a senha](#pwresetcli) e especifique o novo nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="ab357-142">To create a new sudo user with password access, use the script in [Reset the password](#pwresetcli) and specify the new user name.</span></span>

<span data-ttu-id="ab357-143">Para criar um novo usuário sudo com senha de acesso, use o script em [Redefinir a chave SSH](#sshkeyresetcli) e especifique o novo nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="ab357-143">To create a new sudo user with SSH key access, use the script in [Reset the SSH key](#sshkeyresetcli) and specify the new user name.</span></span>

<span data-ttu-id="ab357-144">Você também pode usar [Redefinir a senha e a chave SSH](#resetbothcli) para criar um novo usuário com senha e o acesso à chave de SSH.</span><span class="sxs-lookup"><span data-stu-id="ab357-144">You can also use [Reset the password and the SSH key](#resetbothcli) to create a new user with both password and SSH key access.</span></span>

## <span data-ttu-id="ab357-145"><a name="sshconfigresetcli"></a>Redefinir a configuração de SSH</span><span class="sxs-lookup"><span data-stu-id="ab357-145"><a name="sshconfigresetcli"></a>Reset the SSH configuration</span></span>
<span data-ttu-id="ab357-146">Se a configuração do SSH está em um estado indesejado, você também pode perder o acesso à VM.</span><span class="sxs-lookup"><span data-stu-id="ab357-146">If the SSH configuration is in an undesired state, you might also lose access to the VM.</span></span> <span data-ttu-id="ab357-147">Você pode usar a extensão VMAccess para redefinir a configuração para seu estado padrão.</span><span class="sxs-lookup"><span data-stu-id="ab357-147">You can use the VMAccess extension to reset the configuration to its default state.</span></span> <span data-ttu-id="ab357-148">Para fazer isso, basta definir a chave "reset_ssh" como "True".</span><span class="sxs-lookup"><span data-stu-id="ab357-148">To do so, you just need to set the “reset_ssh” key to “True”.</span></span> <span data-ttu-id="ab357-149">A extensão reinicia o servidor SSH, abre a porta SSH na sua VM e redefine a configuração SSH como padrão.</span><span class="sxs-lookup"><span data-stu-id="ab357-149">The extension will restart the SSH server, open the SSH port on your VM, and reset the SSH configuration to default values.</span></span> <span data-ttu-id="ab357-150">A conta de usuário (nome, senha ou chaves SSH) não será alterada.</span><span class="sxs-lookup"><span data-stu-id="ab357-150">The user account (name, password or SSH keys) will not be changed.</span></span>

> [!NOTE]
> <span data-ttu-id="ab357-151">O arquivo de configuração SSH está localizado em /etc/ssh/sshd_config.</span><span class="sxs-lookup"><span data-stu-id="ab357-151">The SSH configuration file that gets reset is located at /etc/ssh/sshd_config.</span></span>
> 
> 

1. <span data-ttu-id="ab357-152">Crie um arquivo chamado PrivateConf.json com esse conteúdo.</span><span class="sxs-lookup"><span data-stu-id="ab357-152">Create a file named PrivateConf.json with this content.</span></span>

    ```   
        {
        "reset_ssh":"True"
        }
    ```

2. <span data-ttu-id="ab357-153">Execute esse comando, substituindo **myVM** pelo nome da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ab357-153">Run this command, substituting the name of your virtual machine for **myVM**.</span></span> 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="ab357-154"><a name="deletecli"></a>Excluir um usuário</span><span class="sxs-lookup"><span data-stu-id="ab357-154"><a name="deletecli"></a>Delete a user</span></span>
<span data-ttu-id="ab357-155">Se você deseja excluir uma conta de usuário sem efetuar login à VM diretamente, você pode usar este script.</span><span class="sxs-lookup"><span data-stu-id="ab357-155">If you want to delete a user account without logging into to the VM directly, you can use this script.</span></span>

1. <span data-ttu-id="ab357-156">Crie um arquivo chamado PrivateConf.json com esse conteúdo, substituindo o nome de usuário a ser removido em **removeUserName**.</span><span class="sxs-lookup"><span data-stu-id="ab357-156">Create a file named PrivateConf.json with this content, substituting the user name to remove for **removeUserName**.</span></span> 

    ```   
        {
        "remove_user":"removeUserName"
        }
    ```

2. <span data-ttu-id="ab357-157">Execute esse comando, substituindo **myVM** pelo nome da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ab357-157">Run this command, substituting the name of your virtual machine for **myVM**.</span></span> 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="ab357-158"><a name="statuscli"></a>Exibir o status da extensão VMAccess</span><span class="sxs-lookup"><span data-stu-id="ab357-158"><a name="statuscli"></a>Display the status of the VMAccess extension</span></span>
<span data-ttu-id="ab357-159">Para exibir o status da extensão VMAccess, execute este comando.</span><span class="sxs-lookup"><span data-stu-id="ab357-159">To display the status of the VMAccess extension, run this command.</span></span>

```
        azure vm extension get
```

## <span data-ttu-id="ab357-160"><a name='checkdisk'></a>Verificar a consistência dos discos adicionados</span><span class="sxs-lookup"><span data-stu-id="ab357-160"><a name='checkdisk'></a>Check consistency of added disks</span></span>
<span data-ttu-id="ab357-161">Para executar fsck em todos os discos na sua máquina virtual Linux, você precisará fazer o seguinte:</span><span class="sxs-lookup"><span data-stu-id="ab357-161">To run fsck on all disks in your Linux virtual machine, you will need to do the following:</span></span>

1. <span data-ttu-id="ab357-162">Crie um arquivo chamado PublicConf.json com esse conteúdo.</span><span class="sxs-lookup"><span data-stu-id="ab357-162">Create a file named PublicConf.json with this content.</span></span> <span data-ttu-id="ab357-163">A verificação de disco tem um valor booliano para se deseja verificar os discos anexados à sua máquina virtual ou não.</span><span class="sxs-lookup"><span data-stu-id="ab357-163">Check Disk takes a boolean for whether to check disks attached to your virtual machine or not.</span></span> 

    ```   
        {   
        "check_disk": "true"
        }
    ```

2. <span data-ttu-id="ab357-164">Execute esse comando, substituindo o nome da máquina virtual em **myVM**.</span><span class="sxs-lookup"><span data-stu-id="ab357-164">Run this command to execute, substituting the name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json 
    ```

## <span data-ttu-id="ab357-165"><a name='repairdisk'></a>Reparar discos</span><span class="sxs-lookup"><span data-stu-id="ab357-165"><a name='repairdisk'></a>Repair disks</span></span>
<span data-ttu-id="ab357-166">Para reparar discos que não são de montagem ou tem erros de configuração de montagem, use a extensão VMAccess para redefinir a configuração de montagem em sua máquina virtual do Linux.</span><span class="sxs-lookup"><span data-stu-id="ab357-166">To repair disks that are not mounting or have mount configuration errors, use the VMAccess extension to reset the mount configuration on your Linux virtual machine.</span></span> <span data-ttu-id="ab357-167">Substitua o nome do seu disco em **myDisk**.</span><span class="sxs-lookup"><span data-stu-id="ab357-167">Substituting the name of your disk for **myDisk**.</span></span>

1. <span data-ttu-id="ab357-168">Crie um arquivo chamado PublicConf.json com esse conteúdo.</span><span class="sxs-lookup"><span data-stu-id="ab357-168">Create a file named PublicConf.json with this content.</span></span> 

    ```   
        {
        "repair_disk":"true",
        "disk_name":"myDisk"
        }
    ```

2. <span data-ttu-id="ab357-169">Execute esse comando, substituindo o nome da máquina virtual em **myVM**.</span><span class="sxs-lookup"><span data-stu-id="ab357-169">Run this command to execute, substituting the name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json
    ```

## <a name="next-steps"></a><span data-ttu-id="ab357-170">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ab357-170">Next steps</span></span>
* <span data-ttu-id="ab357-171">Se você quiser usar os cmdlets do Azure PowerShell ou os modelos do Azure Resource Manager para redefinir a senha ou chave SSH, corrigir a configuração de SSH e verificar a consistência do disco, veja a [documentação da extensão VMAccess no GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span><span class="sxs-lookup"><span data-stu-id="ab357-171">If you want to use Azure PowerShell cmdlets or Azure Resource Manager templates to reset the password or SSH key, fix the SSH configuration, and check disk consistency, see the [VMAccess extension documentation on GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span></span> 
* <span data-ttu-id="ab357-172">Você também pode usar o [portal do Azure](https://portal.azure.com) para redefinir a senha ou a chave SSH de uma VM do Linux implantada no modelo de implantação clássico.</span><span class="sxs-lookup"><span data-stu-id="ab357-172">You can also use the [Azure portal](https://portal.azure.com) to reset the password or SSH key of a Linux VM deployed in the classic deployment model.</span></span> <span data-ttu-id="ab357-173">No momento, não é possível usar o portal para fazer isso para uma VM do Linux implantada no modelo de implantação do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="ab357-173">You can't currently use the portal do to this for a Linux VM deployed in the Resource Manager deployment model.</span></span>
* <span data-ttu-id="ab357-174">Veja [Sobre os recursos e extensões de máquina virtual](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obter mais informações sobre como usar extensões de VM para máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="ab357-174">See [About virtual machine extensions and features](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more about using VM extensions for Azure virtual machines.</span></span>

