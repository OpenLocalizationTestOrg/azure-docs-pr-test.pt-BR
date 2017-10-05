---
title: Criar uma VM Linux usando a CLI 1.0 do Azure | Microsoft Docs
description: Criar uma VM Linux no Azure usando a CLI 1.0 do Azure
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
ms.assetid: facb1115-2b4e-4ef3-9905-330e42beb686
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: 
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/15/2016
ms.author: v-livech
ms.openlocfilehash: ec1b34e4f539d2e95bb1f99fca3a6a0ec682ef51
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-linux-vm-using-the-azure-cli-10"></a><span data-ttu-id="0946a-103">Criar uma VM Linux usando a CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="0946a-103">Create a Linux VM using the Azure CLI 1.0</span></span>

<span data-ttu-id="0946a-104">Este artigo mostra como implantar rapidamente uma nova VM (máquina virtual) no Azure usando o comando `azure vm quick-create` na CLI (interface de linha de comando) do Azure.</span><span class="sxs-lookup"><span data-stu-id="0946a-104">This article shows how to quickly deploy a Linux virtual machine (VM) on Azure by using the `azure vm quick-create` command in the Azure command-line interface (CLI).</span></span> <span data-ttu-id="0946a-105">O comando `quick-create` implanta uma VM em uma infraestrutura básica e protegida que você pode usar para criar um protótipo ou testar um conceito rapidamente.</span><span class="sxs-lookup"><span data-stu-id="0946a-105">The `quick-create` command deploys a VM inside a basic, secure infrastructure that you can use to prototype or test a concept rapidly.</span></span>

> [!NOTE]
<span data-ttu-id="0946a-106">Para criar uma VM usando a CLI do Azure 2.0, consulte [Criar uma VM com a CLI do Azure](../windows/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0946a-106">To create a VM using the Azure CLI 2.0, see [Create a VM with the Azure CLI](../windows/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="0946a-107">Você também pode implantar rapidamente uma VM do Linux usando o [portal do Azure](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0946a-107">You can also quickly deploy a Linux VM by using the [Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="0946a-108">O artigo exige [arquivos de chave SSH pública e privada](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0946a-108">The article requires an [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="quick-commands"></a><span data-ttu-id="0946a-109">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="0946a-109">Quick commands</span></span>

<span data-ttu-id="0946a-110">O exemplo a seguir mostra como implantar uma VM CoreOS e anexar sua chave SSH (Secure Shell) (seus argumentos podem ser diferentes):</span><span class="sxs-lookup"><span data-stu-id="0946a-110">The following example shows how to deploy a CoreOS VM and attach your Secure Shell (SSH) key (your arguments might be different):</span></span>

```azurecli
azure vm quick-create -M ~/.ssh/id_rsa.pub -Q CoreOS
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="0946a-111">Passo a passo detalhado</span><span class="sxs-lookup"><span data-stu-id="0946a-111">Detailed walkthrough</span></span>

<span data-ttu-id="0946a-112">A instrução a seguir tem uma VM UbuntuLTS sendo implantada, passo a passo, com explicações do que cada etapa está realizando.</span><span class="sxs-lookup"><span data-stu-id="0946a-112">The following walkthrough has an UbuntuLTS VM being deployed, step by step, with explanations of what each step is doing.</span></span>

## <a name="vm-quick-create-aliases"></a><span data-ttu-id="0946a-113">Aliases de criação rápida de VM</span><span class="sxs-lookup"><span data-stu-id="0946a-113">VM quick-create aliases</span></span>

<span data-ttu-id="0946a-114">Uma maneira rápida de escolher uma distribuição é usar os aliases da CLI do Azure mapeados para as distribuições do SO mais comuns.</span><span class="sxs-lookup"><span data-stu-id="0946a-114">A quick way to choose a distribution is to use the Azure CLI aliases mapped to the most common OS distributions.</span></span> <span data-ttu-id="0946a-115">A tabela a seguir lista os aliases (a partir da CLI do Azure versão 0.10).</span><span class="sxs-lookup"><span data-stu-id="0946a-115">The following table lists the aliases (as of Azure CLI version 0.10).</span></span> <span data-ttu-id="0946a-116">Todas as implantações que usam `quick-create` são por padrão VMs com suporte de armazenamento SSD (unidade de estado sólido), que oferecem provisionamento mais rápido e acesso a disco de alto desempenho.</span><span class="sxs-lookup"><span data-stu-id="0946a-116">All deployments that use `quick-create` default to VMs that are backed by solid-state drive (SSD) storage, which offers faster provisioning and high-performance disk access.</span></span> <span data-ttu-id="0946a-117">(Esses aliases do representam uma pequena parte das distribuições disponíveis no Azure.</span><span class="sxs-lookup"><span data-stu-id="0946a-117">(These aliases represent a tiny portion of the available distributions on Azure.</span></span> <span data-ttu-id="0946a-118">Veja mais imagens no Azure Marketplace [pesquisando uma imagem no PowerShell](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [na Web](https://azure.microsoft.com/marketplace/virtual-machines/) ou [carregando sua própria imagem personalizada](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).)</span><span class="sxs-lookup"><span data-stu-id="0946a-118">Find more images in the Azure Marketplace by [searching for an image in PowerShell](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), [on the web](https://azure.microsoft.com/marketplace/virtual-machines/), or [upload your own custom image](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).)</span></span>

| <span data-ttu-id="0946a-119">Alias</span><span class="sxs-lookup"><span data-stu-id="0946a-119">Alias</span></span> | <span data-ttu-id="0946a-120">Editor</span><span class="sxs-lookup"><span data-stu-id="0946a-120">Publisher</span></span> | <span data-ttu-id="0946a-121">Oferta</span><span class="sxs-lookup"><span data-stu-id="0946a-121">Offer</span></span> | <span data-ttu-id="0946a-122">SKU</span><span class="sxs-lookup"><span data-stu-id="0946a-122">SKU</span></span> | <span data-ttu-id="0946a-123">Versão</span><span class="sxs-lookup"><span data-stu-id="0946a-123">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="0946a-124">CentOS</span><span class="sxs-lookup"><span data-stu-id="0946a-124">CentOS</span></span> |<span data-ttu-id="0946a-125">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="0946a-125">OpenLogic</span></span> |<span data-ttu-id="0946a-126">CentOS</span><span class="sxs-lookup"><span data-stu-id="0946a-126">CentOS</span></span> |<span data-ttu-id="0946a-127">7,2</span><span class="sxs-lookup"><span data-stu-id="0946a-127">7.2</span></span> |<span data-ttu-id="0946a-128">mais recente</span><span class="sxs-lookup"><span data-stu-id="0946a-128">latest</span></span> |
| <span data-ttu-id="0946a-129">CoreOS</span><span class="sxs-lookup"><span data-stu-id="0946a-129">CoreOS</span></span> |<span data-ttu-id="0946a-130">CoreOS</span><span class="sxs-lookup"><span data-stu-id="0946a-130">CoreOS</span></span> |<span data-ttu-id="0946a-131">CoreOS</span><span class="sxs-lookup"><span data-stu-id="0946a-131">CoreOS</span></span> |<span data-ttu-id="0946a-132">Estável</span><span class="sxs-lookup"><span data-stu-id="0946a-132">Stable</span></span> |<span data-ttu-id="0946a-133">mais recente</span><span class="sxs-lookup"><span data-stu-id="0946a-133">latest</span></span> |
| <span data-ttu-id="0946a-134">Debian</span><span class="sxs-lookup"><span data-stu-id="0946a-134">Debian</span></span> |<span data-ttu-id="0946a-135">credativ</span><span class="sxs-lookup"><span data-stu-id="0946a-135">credativ</span></span> |<span data-ttu-id="0946a-136">Debian</span><span class="sxs-lookup"><span data-stu-id="0946a-136">Debian</span></span> |<span data-ttu-id="0946a-137">8</span><span class="sxs-lookup"><span data-stu-id="0946a-137">8</span></span> |<span data-ttu-id="0946a-138">mais recente</span><span class="sxs-lookup"><span data-stu-id="0946a-138">latest</span></span> |
| <span data-ttu-id="0946a-139">openSUSE</span><span class="sxs-lookup"><span data-stu-id="0946a-139">openSUSE</span></span> |<span data-ttu-id="0946a-140">SUSE</span><span class="sxs-lookup"><span data-stu-id="0946a-140">SUSE</span></span> |<span data-ttu-id="0946a-141">openSUSE</span><span class="sxs-lookup"><span data-stu-id="0946a-141">openSUSE</span></span> |<span data-ttu-id="0946a-142">13.2</span><span class="sxs-lookup"><span data-stu-id="0946a-142">13.2</span></span> |<span data-ttu-id="0946a-143">mais recente</span><span class="sxs-lookup"><span data-stu-id="0946a-143">latest</span></span> |
| <span data-ttu-id="0946a-144">RHEL</span><span class="sxs-lookup"><span data-stu-id="0946a-144">RHEL</span></span> |<span data-ttu-id="0946a-145">Red Hat</span><span class="sxs-lookup"><span data-stu-id="0946a-145">Red Hat</span></span> |<span data-ttu-id="0946a-146">RHEL</span><span class="sxs-lookup"><span data-stu-id="0946a-146">RHEL</span></span> |<span data-ttu-id="0946a-147">7,2</span><span class="sxs-lookup"><span data-stu-id="0946a-147">7.2</span></span> |<span data-ttu-id="0946a-148">mais recente</span><span class="sxs-lookup"><span data-stu-id="0946a-148">latest</span></span> |
| <span data-ttu-id="0946a-149">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="0946a-149">UbuntuLTS</span></span> |<span data-ttu-id="0946a-150">Canônico</span><span class="sxs-lookup"><span data-stu-id="0946a-150">Canonical</span></span> |<span data-ttu-id="0946a-151">Ubuntu Server</span><span class="sxs-lookup"><span data-stu-id="0946a-151">Ubuntu Server</span></span> |<span data-ttu-id="0946a-152">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="0946a-152">14.04.4-LTS</span></span> |<span data-ttu-id="0946a-153">mais recente</span><span class="sxs-lookup"><span data-stu-id="0946a-153">latest</span></span> |

<span data-ttu-id="0946a-154">As seções a seguir usam o alias `UbuntuLTS` para a opção **ImageURN ()** (`-Q`) a fim de implantar um servidor Ubuntu LTS 14.04.4.</span><span class="sxs-lookup"><span data-stu-id="0946a-154">The following sections use the `UbuntuLTS` alias for the **ImageURN** option (`-Q`) to deploy an Ubuntu 14.04.4 LTS Server.</span></span>

<span data-ttu-id="0946a-155">O exemplo de `quick-create` anterior somente chamou o sinalizador `-M` para identificar a chave pública SSH a ser carregada durante a desativação de senhas de SSH e, portanto, você receberá uma solicitação para fornecer os seguintes argumentos:</span><span class="sxs-lookup"><span data-stu-id="0946a-155">The previous `quick-create` example only called out the `-M` flag to identify the SSH public key to upload while disabling SSH passwords, so you are prompted for the following arguments:</span></span>

* <span data-ttu-id="0946a-156">nome do grupo de recursos (qualquer cadeia de caracteres costuma funcionar bem para o primeiro grupo de recursos do Azure)</span><span class="sxs-lookup"><span data-stu-id="0946a-156">resource group name (any string is typically fine for your first Azure resource group)</span></span>
* <span data-ttu-id="0946a-157">Nome da VM</span><span class="sxs-lookup"><span data-stu-id="0946a-157">VM name</span></span>
* <span data-ttu-id="0946a-158">local (`westus` ou `westeurope` são bons padrões)</span><span class="sxs-lookup"><span data-stu-id="0946a-158">location (`westus` or `westeurope` are good defaults)</span></span>
* <span data-ttu-id="0946a-159">Linux (para permitir que o Azure saiba qual é o sistema operacional desejado)</span><span class="sxs-lookup"><span data-stu-id="0946a-159">linux (to let Azure know which OS you want)</span></span>
* <span data-ttu-id="0946a-160">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="0946a-160">username</span></span>

<span data-ttu-id="0946a-161">O exemplo a seguir especifica todos os valores para que nenhuma outra notificação seja necessária.</span><span class="sxs-lookup"><span data-stu-id="0946a-161">The following example specifies all the values so that no further prompting is required.</span></span> <span data-ttu-id="0946a-162">Enquanto houver um `~/.ssh/id_rsa.pub` como arquivo de chave pública de formato ssh-rsa, ele funcionará como está:</span><span class="sxs-lookup"><span data-stu-id="0946a-162">So long as you have an `~/.ssh/id_rsa.pub` as a ssh-rsa format public key file, it works as is:</span></span>

```azurecli
azure vm quick-create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --admin-username myAdminUser \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --image-urn UbuntuLTS
```

<span data-ttu-id="0946a-163">A saída deve ser semelhante ao bloco de saída a seguir:</span><span class="sxs-lookup"><span data-stu-id="0946a-163">The output should look like the following output block:</span></span>

```azurecli
info:    Executing command vm quick-create
+ Listing virtual machine sizes available in the location "westus"
+ Looking up the VM "myVM"
info:    Verifying the public key SSH file: /Users/ahmet/.ssh/id_rsa.pub
info:    Using the VM Size "Standard_DS1"
info:    The [OS, Data] Disk or image configuration requires storage account
+ Looking up the storage account cli16330708391032639673
+ Looking up the NIC "examp-westu-1633070839-nic"
info:    An nic with given name "examp-westu-1633070839-nic" not found, creating a new one
+ Looking up the virtual network "examp-westu-1633070839-vnet"
info:    Preparing to create new virtual network and subnet
/ Creating a new virtual network "examp-westu-1633070839-vnet" [address prefix: "10.0.0.0/16"] with subnet "examp-westu-1633070839-snet" [address prefix: "10.+.1.0/24"]
+ Looking up the virtual network "examp-westu-1633070839-vnet"
+ Looking up the subnet "examp-westu-1633070839-snet" under the virtual network "examp-westu-1633070839-vnet"
info:    Found public ip parameters, trying to setup PublicIP profile
+ Looking up the public ip "examp-westu-1633070839-pip"
info:    PublicIP with given name "examp-westu-1633070839-pip" not found, creating a new one
+ Creating public ip "examp-westu-1633070839-pip"
+ Looking up the public ip "examp-westu-1633070839-pip"
+ Creating NIC "examp-westu-1633070839-nic"
+ Looking up the NIC "examp-westu-1633070839-nic"
+ Looking up the storage account clisto1710997031examplev
+ Creating VM "myVM"
+ Looking up the VM "myVM"
+ Looking up the NIC "examp-westu-1633070839-nic"
+ Looking up the public ip "examp-westu-1633070839-pip"
data:    Id                              :/subscriptions/2<--snip-->d/resourceGroups/exampleResourceGroup/providers/Microsoft.Compute/virtualMachines/exampleVMName
data:    ProvisioningState               :Succeeded
data:    Name                            :exampleVMName
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_DS1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :Canonical
data:        Offer                       :UbuntuServer
data:        Sku                         :14.04.4-LTS
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :clic7fadb847357e9cf-os-1473374894359
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://cli16330708391032639673.blob.core.windows.net/vhds/clic7fadb847357e9cf-os-1473374894359.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM
data:      User Name                     :myAdminUser
data:      Linux Configuration:
data:        Disable Password Auth       :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-33-42-FB
data:          Provisioning State        :Succeeded
data:          Name                      :examp-westu-1633070839-nic
data:          Location                  :westus
data:            Public IP address       :138.91.247.29
data:            FQDN                    :examp-westu-1633070839-pip.westus.cloudapp.azure.com
data:
data:    Diagnostics Profile:
data:      BootDiagnostics Enabled       :true
data:      BootDiagnostics StorageUri    :https://clisto1710997031examplev.blob.core.windows.net/
data:
data:      Diagnostics Instance View:
info:    vm quick-create command OK
```

## <a name="log-in-to-the-new-vm"></a><span data-ttu-id="0946a-164">Faça logon na nova VM</span><span class="sxs-lookup"><span data-stu-id="0946a-164">Log in to the new VM</span></span>
<span data-ttu-id="0946a-165">Entre na VM usando o endereço IP público listado na saída.</span><span class="sxs-lookup"><span data-stu-id="0946a-165">Log in to your VM by using the public IP address listed in the output.</span></span> <span data-ttu-id="0946a-166">Você também pode usar o FQDN (nome de domínio totalmente qualificado) que está listado:</span><span class="sxs-lookup"><span data-stu-id="0946a-166">You can also use the fully qualified domain name (FQDN) that's listed:</span></span>

```bash
ssh -i ~/.ssh/id_rsa.pub ahmet@138.91.247.29
```

<span data-ttu-id="0946a-167">O processo de logon deve ter uma aparência semelhante ao seguinte bloco de saída:</span><span class="sxs-lookup"><span data-stu-id="0946a-167">The login process should look something like the following output block:</span></span>

```bash
Warning: Permanently added '138.91.247.29' (ECDSA) to the list of known hosts.
Welcome to Ubuntu 14.04.4 LTS (GNU/Linux 3.19.0-65-generic x86_64)

 * Documentation:  https://help.ubuntu.com/

  System information as of Thu Sep  8 22:50:57 UTC 2016

  System load: 0.63              Memory usage: 2%   Processes:       81
  Usage of /:  39.6% of 1.94GB   Swap usage:   0%   Users logged in: 0

  Graph this data and manage this system at:
    https://landscape.canonical.com/

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.



The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

myAdminUser@myVM:~$
```

## <a name="next-steps"></a><span data-ttu-id="0946a-168">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0946a-168">Next steps</span></span>
<span data-ttu-id="0946a-169">O comando `azure vm quick-create` é a maneira de implantar rapidamente uma VM para que você possa fazer logon em um shell bash e começar a trabalhar.</span><span class="sxs-lookup"><span data-stu-id="0946a-169">The `azure vm quick-create` command is the way to quickly deploy a VM so you can log in to a bash shell and get working.</span></span> <span data-ttu-id="0946a-170">No entanto, o uso de `vm quick-create` não lhe dá amplo controle e não permite que você crie um ambiente mais complexo.</span><span class="sxs-lookup"><span data-stu-id="0946a-170">However, using `vm quick-create` does not give you extensive control nor does it enable you to create a more complex environment.</span></span>  <span data-ttu-id="0946a-171">Para implantar uma VM do Linux personalizada para sua infraestrutura, você pode seguir qualquer um destes artigos:</span><span class="sxs-lookup"><span data-stu-id="0946a-171">To deploy a Linux VM that's customized for your infrastructure, you can follow any of these articles:</span></span>

* [<span data-ttu-id="0946a-172">Criar seu próprio ambiente personalizado para uma VM do Linux usando os comandos da CLI do Azure diretamente</span><span class="sxs-lookup"><span data-stu-id="0946a-172">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="0946a-173">Criar uma VM do Linux Protegida por SSH no Azure usando modelos</span><span class="sxs-lookup"><span data-stu-id="0946a-173">Create an SSH Secured Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

<span data-ttu-id="0946a-174">Você também pode [usar o driver do Azure `docker-machine` com vários comandos para criar rapidamente uma VM do Linux como um host do docker](docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0946a-174">You can also [use the `docker-machine` Azure driver with various commands to quickly create a Linux VM as a docker host](docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
