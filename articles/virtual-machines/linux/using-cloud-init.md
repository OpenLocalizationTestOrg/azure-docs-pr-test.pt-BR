---
title: aaaUse init nuvem toocustomize uma VM do Linux | Microsoft Docs
description: "Como toocustomize de nuvem init toouse uma VM do Linux durante a criação com hello 2.0 do CLI do Azure"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 195c22cd-4629-4582-9ee3-9749493f1d72
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: e7297e162fc73f0da42f195bec2fcbe23b310c1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-cloud-init-toocustomize-a-linux-vm-during-creation"></a><span data-ttu-id="c5f53-103">Use a nuvem init toocustomize uma VM do Linux durante a criação</span><span class="sxs-lookup"><span data-stu-id="c5f53-103">Use cloud-init toocustomize a Linux VM during creation</span></span>
<span data-ttu-id="c5f53-104">Este artigo mostra como toomake uma tooset de script de inicialização de nuvem Olá hostname, atualizar os pacotes instalados e gerenciar contas de usuário com hello 2.0 do CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="c5f53-104">This article shows you how toomake a cloud-init script tooset hello hostname, update installed packages, and manage user accounts with hello Azure CLI 2.0.</span></span> <span data-ttu-id="c5f53-105">scripts de inicialização de nuvem Olá são chamados quando você criar uma máquina virtual (VM) da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="c5f53-105">hello cloud-init scripts are called when you create a virtual machine (VM) from Azure CLI.</span></span> <span data-ttu-id="c5f53-106">Para obter uma visão mais detalhada sobre como instalar aplicativos, gravar arquivos de configuração e injetar chaves do Key Vault, consulte [este tutorial](tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="c5f53-106">For a more in-depth overview on installing applications, writing configuration files, and injecting keys from Key Vault, see [this tutorial](tutorial-automate-vm-deployment.md).</span></span> <span data-ttu-id="c5f53-107">Você também pode executar essas etapas com hello [Azure CLI 1.0](using-cloud-init-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="c5f53-107">You can also perform these steps with hello [Azure CLI 1.0](using-cloud-init-nodejs.md).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="c5f53-108">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="c5f53-108">Quick commands</span></span>
<span data-ttu-id="c5f53-109">Crie um script de nuvem init.txt que define o nome de host hello, todos os pacotes de atualizações e adiciona um tooLinux de usuário sudo.</span><span class="sxs-lookup"><span data-stu-id="c5f53-109">Create a cloud-init.txt script that sets hello hostname, updates all packages, and adds a sudo user tooLinux.</span></span>

```yaml
#cloud-config
hostname: myVMhostname
apt_upgrade: true
users:
  - name: myNewAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myVM
```

<span data-ttu-id="c5f53-110">Criar um toolaunch do grupo de recursos VMs em com [criar grupo az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="c5f53-110">Create a resource group toolaunch VMs into with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="c5f53-111">Olá, exemplo a seguir cria grupo de recursos de saudação chamado *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="c5f53-111">hello following example creates hello resource group named *myResourceGroup*:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="c5f53-112">Criar uma VM do Linux com [criar vm az](/cli/azure/vm#create) usando tooconfigure nuvem init-lo durante a inicialização com hello `--custom-data` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="c5f53-112">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot with hello `--custom-data` parameter.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="c5f53-113">Passo a passo detalhado</span><span class="sxs-lookup"><span data-stu-id="c5f53-113">Detailed walkthrough</span></span>
<span data-ttu-id="c5f53-114">Quando você inicia uma nova VM do Linux, você obtém uma VM padrão do Linux sem nada personalizado nem pronta para suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="c5f53-114">When you launch a new Linux VM, you are getting a standard Linux VM with nothing customized or ready for your needs.</span></span> <span data-ttu-id="c5f53-115">[Nuvem init](https://cloudinit.readthedocs.org) é tooinject uma maneira padrão um script ou configurações na VM Linux como ele está sendo inicializado para Olá primeira vez.</span><span class="sxs-lookup"><span data-stu-id="c5f53-115">[Cloud-init](https://cloudinit.readthedocs.org) is a standard way tooinject a script or configuration settings into that Linux VM as it is booting up for hello first time.</span></span>

<span data-ttu-id="c5f53-116">No Azure, há algumas maneiras diferentes toomake alterações em uma VM do Linux que está sendo implantado ou inicializado.</span><span class="sxs-lookup"><span data-stu-id="c5f53-116">On Azure, there are a few different ways toomake changes onto a Linux VM as it is being deployed or booted.</span></span>

* <span data-ttu-id="c5f53-117">Insira scripts usando a inicialização de nuvem.</span><span class="sxs-lookup"><span data-stu-id="c5f53-117">Inject scripts using cloud-init.</span></span>
* <span data-ttu-id="c5f53-118">Inserir scripts usando hello Azure [extensão VMAccess](using-vmaccess-extension.md).</span><span class="sxs-lookup"><span data-stu-id="c5f53-118">Inject scripts using hello Azure [VMAccess Extension](using-vmaccess-extension.md).</span></span>
* <span data-ttu-id="c5f53-119">Um modelo do Azure usando a inicialização de nuvem.</span><span class="sxs-lookup"><span data-stu-id="c5f53-119">An Azure template using cloud-init.</span></span>
* <span data-ttu-id="c5f53-120">Um modelo do Azure usando [CustomScriptExtention](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="c5f53-120">An Azure template using [CustomScriptExtention](extensions-customscript.md).</span></span>

<span data-ttu-id="c5f53-121">scripts de tooinject a qualquer momento após a inicialização:</span><span class="sxs-lookup"><span data-stu-id="c5f53-121">tooinject scripts at any time after boot:</span></span>

* <span data-ttu-id="c5f53-122">Comandos diretamente do SSH toorun</span><span class="sxs-lookup"><span data-stu-id="c5f53-122">SSH toorun commands directly</span></span>
* <span data-ttu-id="c5f53-123">Inserir scripts usando hello Azure [extensão VMAccess](using-vmaccess-extension.md), imperativa ou em um modelo do Azure</span><span class="sxs-lookup"><span data-stu-id="c5f53-123">Inject scripts using hello Azure [VMAccess Extension](using-vmaccess-extension.md), either imperatively or in an Azure template</span></span>
* <span data-ttu-id="c5f53-124">Ferramentas de gerenciamento de configuração, como Ansible, Salt, Chef e Puppet.</span><span class="sxs-lookup"><span data-stu-id="c5f53-124">Configuration management tools like Ansible, Salt, Chef, and Puppet.</span></span>

> [!NOTE]
> <span data-ttu-id="c5f53-125">Extensão VMAccess executa um script, como a raiz de saudação do mesmo modo usando SSH pode.</span><span class="sxs-lookup"><span data-stu-id="c5f53-125">VMAccess Extension executes a script as root in hello same way using SSH can.</span></span> <span data-ttu-id="c5f53-126">No entanto, usando a extensão de VM Olá permite que vários recursos que ofertas do Azure que podem ser úteis dependendo do cenário.</span><span class="sxs-lookup"><span data-stu-id="c5f53-126">However, using hello VM extension enables several features that Azure offers that can be useful depending upon your scenario.</span></span>

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a><span data-ttu-id="c5f53-127">Disponibilidade de inicialização de nuvem em aliases de imagem de criação rápida de uma VM do Azure:</span><span class="sxs-lookup"><span data-stu-id="c5f53-127">Cloud-init availability on Azure VM quick-create image aliases:</span></span>
| <span data-ttu-id="c5f53-128">Alias</span><span class="sxs-lookup"><span data-stu-id="c5f53-128">Alias</span></span> | <span data-ttu-id="c5f53-129">Editor</span><span class="sxs-lookup"><span data-stu-id="c5f53-129">Publisher</span></span> | <span data-ttu-id="c5f53-130">Oferta</span><span class="sxs-lookup"><span data-stu-id="c5f53-130">Offer</span></span> | <span data-ttu-id="c5f53-131">SKU</span><span class="sxs-lookup"><span data-stu-id="c5f53-131">SKU</span></span> | <span data-ttu-id="c5f53-132">Versão</span><span class="sxs-lookup"><span data-stu-id="c5f53-132">Version</span></span> | <span data-ttu-id="c5f53-133">inicialização de nuvem</span><span class="sxs-lookup"><span data-stu-id="c5f53-133">cloud-init</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="c5f53-134">CentOS</span><span class="sxs-lookup"><span data-stu-id="c5f53-134">CentOS</span></span> |<span data-ttu-id="c5f53-135">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="c5f53-135">OpenLogic</span></span> |<span data-ttu-id="c5f53-136">Centos</span><span class="sxs-lookup"><span data-stu-id="c5f53-136">Centos</span></span> |<span data-ttu-id="c5f53-137">7,2</span><span class="sxs-lookup"><span data-stu-id="c5f53-137">7.2</span></span> |<span data-ttu-id="c5f53-138">mais recente</span><span class="sxs-lookup"><span data-stu-id="c5f53-138">latest</span></span> |<span data-ttu-id="c5f53-139">não</span><span class="sxs-lookup"><span data-stu-id="c5f53-139">no</span></span> |
| <span data-ttu-id="c5f53-140">CoreOS</span><span class="sxs-lookup"><span data-stu-id="c5f53-140">CoreOS</span></span> |<span data-ttu-id="c5f53-141">CoreOS</span><span class="sxs-lookup"><span data-stu-id="c5f53-141">CoreOS</span></span> |<span data-ttu-id="c5f53-142">CoreOS</span><span class="sxs-lookup"><span data-stu-id="c5f53-142">CoreOS</span></span> |<span data-ttu-id="c5f53-143">Estável</span><span class="sxs-lookup"><span data-stu-id="c5f53-143">Stable</span></span> |<span data-ttu-id="c5f53-144">mais recente</span><span class="sxs-lookup"><span data-stu-id="c5f53-144">latest</span></span> |<span data-ttu-id="c5f53-145">sim</span><span class="sxs-lookup"><span data-stu-id="c5f53-145">yes</span></span> |
| <span data-ttu-id="c5f53-146">Debian</span><span class="sxs-lookup"><span data-stu-id="c5f53-146">Debian</span></span> |<span data-ttu-id="c5f53-147">credativ</span><span class="sxs-lookup"><span data-stu-id="c5f53-147">credativ</span></span> |<span data-ttu-id="c5f53-148">Debian</span><span class="sxs-lookup"><span data-stu-id="c5f53-148">Debian</span></span> |<span data-ttu-id="c5f53-149">8</span><span class="sxs-lookup"><span data-stu-id="c5f53-149">8</span></span> |<span data-ttu-id="c5f53-150">mais recente</span><span class="sxs-lookup"><span data-stu-id="c5f53-150">latest</span></span> |<span data-ttu-id="c5f53-151">não</span><span class="sxs-lookup"><span data-stu-id="c5f53-151">no</span></span> |
| <span data-ttu-id="c5f53-152">openSUSE</span><span class="sxs-lookup"><span data-stu-id="c5f53-152">openSUSE</span></span> |<span data-ttu-id="c5f53-153">SUSE</span><span class="sxs-lookup"><span data-stu-id="c5f53-153">SUSE</span></span> |<span data-ttu-id="c5f53-154">openSUSE</span><span class="sxs-lookup"><span data-stu-id="c5f53-154">openSUSE</span></span> |<span data-ttu-id="c5f53-155">13.2</span><span class="sxs-lookup"><span data-stu-id="c5f53-155">13.2</span></span> |<span data-ttu-id="c5f53-156">mais recente</span><span class="sxs-lookup"><span data-stu-id="c5f53-156">latest</span></span> |<span data-ttu-id="c5f53-157">não</span><span class="sxs-lookup"><span data-stu-id="c5f53-157">no</span></span> |
| <span data-ttu-id="c5f53-158">RHEL</span><span class="sxs-lookup"><span data-stu-id="c5f53-158">RHEL</span></span> |<span data-ttu-id="c5f53-159">Redhat</span><span class="sxs-lookup"><span data-stu-id="c5f53-159">Redhat</span></span> |<span data-ttu-id="c5f53-160">RHEL</span><span class="sxs-lookup"><span data-stu-id="c5f53-160">RHEL</span></span> |<span data-ttu-id="c5f53-161">7,2</span><span class="sxs-lookup"><span data-stu-id="c5f53-161">7.2</span></span> |<span data-ttu-id="c5f53-162">mais recente</span><span class="sxs-lookup"><span data-stu-id="c5f53-162">latest</span></span> |<span data-ttu-id="c5f53-163">não</span><span class="sxs-lookup"><span data-stu-id="c5f53-163">no</span></span> |
| <span data-ttu-id="c5f53-164">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="c5f53-164">UbuntuLTS</span></span> |<span data-ttu-id="c5f53-165">Canônico</span><span class="sxs-lookup"><span data-stu-id="c5f53-165">Canonical</span></span> |<span data-ttu-id="c5f53-166">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="c5f53-166">UbuntuServer</span></span> |<span data-ttu-id="c5f53-167">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="c5f53-167">14.04.4-LTS</span></span> |<span data-ttu-id="c5f53-168">mais recente</span><span class="sxs-lookup"><span data-stu-id="c5f53-168">latest</span></span> |<span data-ttu-id="c5f53-169">sim</span><span class="sxs-lookup"><span data-stu-id="c5f53-169">yes</span></span> |

<span data-ttu-id="c5f53-170">Estamos trabalhando com nossos parceiros tooget nuvem-init incluído e trabalhar com imagens Olá que eles fornecem tooAzure.</span><span class="sxs-lookup"><span data-stu-id="c5f53-170">We are working with our partners tooget cloud-init included and working in hello images that they provide tooAzure.</span></span>

## <a name="add-a-cloud-init-script-toohello-vm-creation-with-hello-azure-cli"></a><span data-ttu-id="c5f53-171">Adicionar uma criação de VM nuvem init script toohello com hello CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="c5f53-171">Add a cloud-init script toohello VM creation with hello Azure CLI</span></span>
<span data-ttu-id="c5f53-172">toolaunch um script de inicialização de nuvem ao criar uma VM no Azure, especifique o arquivo de inicialização de nuvem de hello usando Olá CLI do Azure `--custom-data` alternar.</span><span class="sxs-lookup"><span data-stu-id="c5f53-172">toolaunch a cloud-init script when creating a VM in Azure, specify hello cloud-init file using hello Azure CLI `--custom-data` switch.</span></span>

<span data-ttu-id="c5f53-173">Criar um toolaunch do grupo de recursos VMs em com [criar grupo az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="c5f53-173">Create a resource group toolaunch VMs into with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="c5f53-174">Olá, exemplo a seguir cria grupo de recursos de saudação chamado *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="c5f53-174">hello following example creates hello resource group named *myResourceGroup*:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="c5f53-175">Criar uma VM do Linux com [criar vm az](/cli/azure/vm#create) usando tooconfigure nuvem init-lo durante a inicialização.</span><span class="sxs-lookup"><span data-stu-id="c5f53-175">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="create-a-cloud-init-script-tooset-hello-hostname-of-a-linux-vm"></a><span data-ttu-id="c5f53-176">Criar uma nuvem init script tooset Olá nome de host de uma VM do Linux</span><span class="sxs-lookup"><span data-stu-id="c5f53-176">Create a cloud-init script tooset hello hostname of a Linux VM</span></span>
<span data-ttu-id="c5f53-177">Uma das configurações mais importantes para qualquer VM do Linux e hello mais simples seria Olá hostname.</span><span class="sxs-lookup"><span data-stu-id="c5f53-177">One of hello simplest and most important settings for any Linux VM would be hello hostname.</span></span> <span data-ttu-id="c5f53-178">Podemos defini-la com facilidade usando o cloud-init com este script.</span><span class="sxs-lookup"><span data-stu-id="c5f53-178">We can easily set this using cloud-init with this script.</span></span>  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a><span data-ttu-id="c5f53-179">Script de inicialização de nuvem de exemplo chamado `cloud_config_hostname.txt`.</span><span class="sxs-lookup"><span data-stu-id="c5f53-179">Example cloud-init script named `cloud_config_hostname.txt`.</span></span>
```yaml
#cloud-config
hostname: myservername
```

<span data-ttu-id="c5f53-180">Durante a inicialização inicial de saudação do hello VM, esse script de inicialização de nuvem define Olá hostname muito*myservername*.</span><span class="sxs-lookup"><span data-stu-id="c5f53-180">During hello initial startup of hello VM, this cloud-init script sets hello hostname too*myservername*.</span></span> <span data-ttu-id="c5f53-181">Criar uma VM do Linux com [criar vm az](/cli/azure/vm#create) usando tooconfigure nuvem init-lo durante a inicialização.</span><span class="sxs-lookup"><span data-stu-id="c5f53-181">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

<span data-ttu-id="c5f53-182">Logon e verifique se o nome de host de saudação do hello nova VM.</span><span class="sxs-lookup"><span data-stu-id="c5f53-182">Login and verify hello hostname of hello new VM.</span></span>

```bash
ssh myVM
hostname
myservername
```

## <a name="create-a-cloud-init-script"></a><span data-ttu-id="c5f53-183">Criar um script cloud-init</span><span class="sxs-lookup"><span data-stu-id="c5f53-183">Create a cloud-init script</span></span>
<span data-ttu-id="c5f53-184">Para segurança, convém seu tooupdate Ubuntu VM na primeira inicialização de saudação.</span><span class="sxs-lookup"><span data-stu-id="c5f53-184">For security, you want your Ubuntu VM tooupdate on hello first boot.</span></span> <span data-ttu-id="c5f53-185">Usando a nuvem init podemos fazer que com hello siga script, dependendo da distribuição de Linux Olá que você está usando.</span><span class="sxs-lookup"><span data-stu-id="c5f53-185">Using cloud-init we can do that with hello follow script, depending on hello Linux distribution you are using.</span></span>

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-hello-debian-family"></a><span data-ttu-id="c5f53-186">Exemplo de script de inicialização de nuvem `cloud_config_apt_upgrade.txt` para Olá família Debian</span><span class="sxs-lookup"><span data-stu-id="c5f53-186">Example cloud-init script `cloud_config_apt_upgrade.txt` for hello Debian Family</span></span>
```yaml
#cloud-config
apt_upgrade: true
```

<span data-ttu-id="c5f53-187">Depois de Linux foi inicializado, todos os pacotes de saudação instalado são atualizados por meio de **apt get**.</span><span class="sxs-lookup"><span data-stu-id="c5f53-187">After Linux has booted, all hello installed packages are updated via **apt-get**.</span></span> <span data-ttu-id="c5f53-188">Criar uma VM do Linux com [criar vm az](/cli/azure/vm#create) usando tooconfigure nuvem init-lo durante a inicialização.</span><span class="sxs-lookup"><span data-stu-id="c5f53-188">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_apt_upgrade.txt
```

<span data-ttu-id="c5f53-189">Faça logon e verifique se todos os pacotes foram atualizados.</span><span class="sxs-lookup"><span data-stu-id="c5f53-189">Login and verify all packages are updated.</span></span>

```bash
ssh myUbuntuVM
sudo apt-get upgrade
Reading package lists... Done
Building dependency tree
Reading state information... Done
Calculating upgrade... Done
hello following packages have been kept back:
  linux-generic linux-headers-generic linux-image-generic
0 upgraded, 0 newly installed, 0 tooremove and 0 not upgraded.
```

## <a name="create-a-cloud-init-script-tooadd-a-user-toolinux"></a><span data-ttu-id="c5f53-190">Criar um tooadd de script de inicialização de nuvem tooLinux um usuário</span><span class="sxs-lookup"><span data-stu-id="c5f53-190">Create a cloud-init script tooadd a user tooLinux</span></span>
<span data-ttu-id="c5f53-191">Uma das primeiras tarefas hello em qualquer nova VM do Linux é tooadd um usuário para si mesmo ou tooavoid usando *raiz*.</span><span class="sxs-lookup"><span data-stu-id="c5f53-191">One of hello first tasks on any new Linux VM is tooadd a user for yourself or tooavoid using *root*.</span></span> <span data-ttu-id="c5f53-192">Chaves de SSH são uma prática recomendada de segurança e facilidade de uso e elas são adicionadas toohello *~/.ssh/authorized_keys* arquivo com esse script de inicialização de nuvem.</span><span class="sxs-lookup"><span data-stu-id="c5f53-192">SSH keys are best practice for security and for usability and they are added toohello *~/.ssh/authorized_keys* file with this cloud-init script.</span></span>

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a><span data-ttu-id="c5f53-193">Script de inicialização de nuvem de exemplo `cloud_config_add_users.txt` para a família Debian</span><span class="sxs-lookup"><span data-stu-id="c5f53-193">Example cloud-init script `cloud_config_add_users.txt` for Debian Family</span></span>
```yaml
#cloud-config
users:
  - name: myCloudInitAddedAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myUbuntuVM
```

<span data-ttu-id="c5f53-194">Depois de Linux foi inicializado, todos os usuários de saudação listado são toohello criado e adicionado sudo grupo.</span><span class="sxs-lookup"><span data-stu-id="c5f53-194">After Linux has booted, all hello listed users are created and added toohello sudo group.</span></span> <span data-ttu-id="c5f53-195">Criar uma VM do Linux com [criar vm az](/cli/azure/vm#create) usando tooconfigure nuvem init-lo durante a inicialização.</span><span class="sxs-lookup"><span data-stu-id="c5f53-195">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init tooconfigure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_add_users.txt
```

<span data-ttu-id="c5f53-196">Logon e verifique se o usuário Olá recém-criado.</span><span class="sxs-lookup"><span data-stu-id="c5f53-196">Login and verify hello newly created user.</span></span>

```bash
ssh myVM
cat /etc/group
```

<span data-ttu-id="c5f53-197">Saída</span><span class="sxs-lookup"><span data-stu-id="c5f53-197">Output</span></span>

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a><span data-ttu-id="c5f53-198">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c5f53-198">Next steps</span></span>
<span data-ttu-id="c5f53-199">Inicialização de nuvem está se tornando um toomodify de maneira padrão sua VM do Linux na inicialização.</span><span class="sxs-lookup"><span data-stu-id="c5f53-199">Cloud-init is becoming one standard way toomodify your Linux VM on boot.</span></span> <span data-ttu-id="c5f53-200">O Azure também tem extensões VM, que permitem que você toomodify sua LinuxVM na inicialização ou durante a execução.</span><span class="sxs-lookup"><span data-stu-id="c5f53-200">Azure also has VM extensions, which allow you toomodify your LinuxVM on boot or while it is running.</span></span> <span data-ttu-id="c5f53-201">Por exemplo, você pode usar hello Azure VMAccessExtension tooreset SSH ou informações do usuário enquanto Olá VM está em execução.</span><span class="sxs-lookup"><span data-stu-id="c5f53-201">For example, you can use hello Azure VMAccessExtension tooreset SSH or user information while hello VM is running.</span></span> <span data-ttu-id="c5f53-202">Com a inicialização de nuvem, você precisaria de uma senha de saudação do tooreset de reinicialização.</span><span class="sxs-lookup"><span data-stu-id="c5f53-202">With cloud-init, you would need a reboot tooreset hello password.</span></span>

[<span data-ttu-id="c5f53-203">Sobre os recursos e extensões de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="c5f53-203">About virtual machine extensions and features</span></span>](extensions-features.md)

[<span data-ttu-id="c5f53-204">Gerenciar usuários, SSH e seleção ou discos de reparo em máquinas virtuais do Linux do Azure usando Olá extensão VMAccess</span><span class="sxs-lookup"><span data-stu-id="c5f53-204">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension</span></span>](using-vmaccess-extension.md)
