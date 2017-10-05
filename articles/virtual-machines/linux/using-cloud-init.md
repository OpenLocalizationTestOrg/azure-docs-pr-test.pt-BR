---
title: Usar cloud-init para personalizar uma VM Linux | Microsoft Docs
description: "Como usar cloud-init para personalizar uma VM Linux durante a criação com a CLI do Azure 2.0"
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
ms.openlocfilehash: a7a6daad34525683579e25b9591ed28f2bf29c04
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-cloud-init-to-customize-a-linux-vm-during-creation"></a><span data-ttu-id="ee034-103">Usar cloud-init para personalizar uma VM Linux durante a criação</span><span class="sxs-lookup"><span data-stu-id="ee034-103">Use cloud-init to customize a Linux VM during creation</span></span>
<span data-ttu-id="ee034-104">Este artigo mostra como criar um script cloud-init para definir o nome do host, atualizar pacotes instalados e gerenciar contas de usuários com a CLI 2.0 do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee034-104">This article shows you how to make a cloud-init script to set the hostname, update installed packages, and manage user accounts with the Azure CLI 2.0.</span></span> <span data-ttu-id="ee034-105">Os scripts cloud-init são chamados quando você cria uma VM (máquina virtual) usando a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee034-105">The cloud-init scripts are called when you create a virtual machine (VM) from Azure CLI.</span></span> <span data-ttu-id="ee034-106">Para obter uma visão mais detalhada sobre como instalar aplicativos, gravar arquivos de configuração e injetar chaves do Key Vault, consulte [este tutorial](tutorial-automate-vm-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="ee034-106">For a more in-depth overview on installing applications, writing configuration files, and injecting keys from Key Vault, see [this tutorial](tutorial-automate-vm-deployment.md).</span></span> <span data-ttu-id="ee034-107">Você também pode executar essas etapas com a [CLI do Azure 1.0](using-cloud-init-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="ee034-107">You can also perform these steps with the [Azure CLI 1.0](using-cloud-init-nodejs.md).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="ee034-108">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="ee034-108">Quick commands</span></span>
<span data-ttu-id="ee034-109">Crie um script cloud-init.txt que define o nome do host, atualiza todos os pacotes e adiciona um usuário sudo ao Linux.</span><span class="sxs-lookup"><span data-stu-id="ee034-109">Create a cloud-init.txt script that sets the hostname, updates all packages, and adds a sudo user to Linux.</span></span>

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

<span data-ttu-id="ee034-110">Crie um grupo de recursos para iniciar VMs com [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="ee034-110">Create a resource group to launch VMs into with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="ee034-111">O exemplo a seguir cria o grupo de recursos chamado *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="ee034-111">The following example creates the resource group named *myResourceGroup*:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="ee034-112">Crie uma VM Linux com [az vm create](/cli/azure/vm#create) usando cloud-init para configurá-la durante a inicialização com o parâmetro `--custom-data`.</span><span class="sxs-lookup"><span data-stu-id="ee034-112">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot with the `--custom-data` parameter.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="ee034-113">Passo a passo detalhado</span><span class="sxs-lookup"><span data-stu-id="ee034-113">Detailed walkthrough</span></span>
<span data-ttu-id="ee034-114">Quando você inicia uma nova VM do Linux, você obtém uma VM padrão do Linux sem nada personalizado nem pronta para suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="ee034-114">When you launch a new Linux VM, you are getting a standard Linux VM with nothing customized or ready for your needs.</span></span> <span data-ttu-id="ee034-115">[inicialização de nuvem](https://cloudinit.readthedocs.org) é uma maneira padrão de inserir um script ou definições de configuração nessa VM do Linux como se ela estivesse sendo inicializada pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="ee034-115">[Cloud-init](https://cloudinit.readthedocs.org) is a standard way to inject a script or configuration settings into that Linux VM as it is booting up for the first time.</span></span>

<span data-ttu-id="ee034-116">No Azure, há algumas maneiras diferentes de fazer alterações em uma VM do Linux como se ela estivesse sendo implantada ou inicializada.</span><span class="sxs-lookup"><span data-stu-id="ee034-116">On Azure, there are a few different ways to make changes onto a Linux VM as it is being deployed or booted.</span></span>

* <span data-ttu-id="ee034-117">Insira scripts usando a inicialização de nuvem.</span><span class="sxs-lookup"><span data-stu-id="ee034-117">Inject scripts using cloud-init.</span></span>
* <span data-ttu-id="ee034-118">Insira scripts usando a [Extensão VMAccess](using-vmaccess-extension.md)do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee034-118">Inject scripts using the Azure [VMAccess Extension](using-vmaccess-extension.md).</span></span>
* <span data-ttu-id="ee034-119">Um modelo do Azure usando a inicialização de nuvem.</span><span class="sxs-lookup"><span data-stu-id="ee034-119">An Azure template using cloud-init.</span></span>
* <span data-ttu-id="ee034-120">Um modelo do Azure usando [CustomScriptExtention](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="ee034-120">An Azure template using [CustomScriptExtention](extensions-customscript.md).</span></span>

<span data-ttu-id="ee034-121">Para inserir scripts a qualquer momento após a inicialização:</span><span class="sxs-lookup"><span data-stu-id="ee034-121">To inject scripts at any time after boot:</span></span>

* <span data-ttu-id="ee034-122">SSH para executar comandos diretamente</span><span class="sxs-lookup"><span data-stu-id="ee034-122">SSH to run commands directly</span></span>
* <span data-ttu-id="ee034-123">Insira scripts usando a [Extensão VMAccess](using-vmaccess-extension.md)do Azure de forma obrigatória ou em um modelo do Azure</span><span class="sxs-lookup"><span data-stu-id="ee034-123">Inject scripts using the Azure [VMAccess Extension](using-vmaccess-extension.md), either imperatively or in an Azure template</span></span>
* <span data-ttu-id="ee034-124">Ferramentas de gerenciamento de configuração, como Ansible, Salt, Chef e Puppet.</span><span class="sxs-lookup"><span data-stu-id="ee034-124">Configuration management tools like Ansible, Salt, Chef, and Puppet.</span></span>

> [!NOTE]
> <span data-ttu-id="ee034-125">A Extensão VMAccess executa um script como raiz da mesma forma que com o uso do SSH.</span><span class="sxs-lookup"><span data-stu-id="ee034-125">VMAccess Extension executes a script as root in the same way using SSH can.</span></span> <span data-ttu-id="ee034-126">No entanto, o uso a extensão de VM habilita vários recursos oferecidos pelo Azure que podem ser úteis, dependendo do cenário.</span><span class="sxs-lookup"><span data-stu-id="ee034-126">However, using the VM extension enables several features that Azure offers that can be useful depending upon your scenario.</span></span>

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a><span data-ttu-id="ee034-127">Disponibilidade de inicialização de nuvem em aliases de imagem de criação rápida de uma VM do Azure:</span><span class="sxs-lookup"><span data-stu-id="ee034-127">Cloud-init availability on Azure VM quick-create image aliases:</span></span>
| <span data-ttu-id="ee034-128">Alias</span><span class="sxs-lookup"><span data-stu-id="ee034-128">Alias</span></span> | <span data-ttu-id="ee034-129">Editor</span><span class="sxs-lookup"><span data-stu-id="ee034-129">Publisher</span></span> | <span data-ttu-id="ee034-130">Oferta</span><span class="sxs-lookup"><span data-stu-id="ee034-130">Offer</span></span> | <span data-ttu-id="ee034-131">SKU</span><span class="sxs-lookup"><span data-stu-id="ee034-131">SKU</span></span> | <span data-ttu-id="ee034-132">Versão</span><span class="sxs-lookup"><span data-stu-id="ee034-132">Version</span></span> | <span data-ttu-id="ee034-133">inicialização de nuvem</span><span class="sxs-lookup"><span data-stu-id="ee034-133">cloud-init</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="ee034-134">CentOS</span><span class="sxs-lookup"><span data-stu-id="ee034-134">CentOS</span></span> |<span data-ttu-id="ee034-135">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="ee034-135">OpenLogic</span></span> |<span data-ttu-id="ee034-136">Centos</span><span class="sxs-lookup"><span data-stu-id="ee034-136">Centos</span></span> |<span data-ttu-id="ee034-137">7,2</span><span class="sxs-lookup"><span data-stu-id="ee034-137">7.2</span></span> |<span data-ttu-id="ee034-138">mais recente</span><span class="sxs-lookup"><span data-stu-id="ee034-138">latest</span></span> |<span data-ttu-id="ee034-139">não</span><span class="sxs-lookup"><span data-stu-id="ee034-139">no</span></span> |
| <span data-ttu-id="ee034-140">CoreOS</span><span class="sxs-lookup"><span data-stu-id="ee034-140">CoreOS</span></span> |<span data-ttu-id="ee034-141">CoreOS</span><span class="sxs-lookup"><span data-stu-id="ee034-141">CoreOS</span></span> |<span data-ttu-id="ee034-142">CoreOS</span><span class="sxs-lookup"><span data-stu-id="ee034-142">CoreOS</span></span> |<span data-ttu-id="ee034-143">Estável</span><span class="sxs-lookup"><span data-stu-id="ee034-143">Stable</span></span> |<span data-ttu-id="ee034-144">mais recente</span><span class="sxs-lookup"><span data-stu-id="ee034-144">latest</span></span> |<span data-ttu-id="ee034-145">sim</span><span class="sxs-lookup"><span data-stu-id="ee034-145">yes</span></span> |
| <span data-ttu-id="ee034-146">Debian</span><span class="sxs-lookup"><span data-stu-id="ee034-146">Debian</span></span> |<span data-ttu-id="ee034-147">credativ</span><span class="sxs-lookup"><span data-stu-id="ee034-147">credativ</span></span> |<span data-ttu-id="ee034-148">Debian</span><span class="sxs-lookup"><span data-stu-id="ee034-148">Debian</span></span> |<span data-ttu-id="ee034-149">8</span><span class="sxs-lookup"><span data-stu-id="ee034-149">8</span></span> |<span data-ttu-id="ee034-150">mais recente</span><span class="sxs-lookup"><span data-stu-id="ee034-150">latest</span></span> |<span data-ttu-id="ee034-151">não</span><span class="sxs-lookup"><span data-stu-id="ee034-151">no</span></span> |
| <span data-ttu-id="ee034-152">openSUSE</span><span class="sxs-lookup"><span data-stu-id="ee034-152">openSUSE</span></span> |<span data-ttu-id="ee034-153">SUSE</span><span class="sxs-lookup"><span data-stu-id="ee034-153">SUSE</span></span> |<span data-ttu-id="ee034-154">openSUSE</span><span class="sxs-lookup"><span data-stu-id="ee034-154">openSUSE</span></span> |<span data-ttu-id="ee034-155">13.2</span><span class="sxs-lookup"><span data-stu-id="ee034-155">13.2</span></span> |<span data-ttu-id="ee034-156">mais recente</span><span class="sxs-lookup"><span data-stu-id="ee034-156">latest</span></span> |<span data-ttu-id="ee034-157">não</span><span class="sxs-lookup"><span data-stu-id="ee034-157">no</span></span> |
| <span data-ttu-id="ee034-158">RHEL</span><span class="sxs-lookup"><span data-stu-id="ee034-158">RHEL</span></span> |<span data-ttu-id="ee034-159">Redhat</span><span class="sxs-lookup"><span data-stu-id="ee034-159">Redhat</span></span> |<span data-ttu-id="ee034-160">RHEL</span><span class="sxs-lookup"><span data-stu-id="ee034-160">RHEL</span></span> |<span data-ttu-id="ee034-161">7,2</span><span class="sxs-lookup"><span data-stu-id="ee034-161">7.2</span></span> |<span data-ttu-id="ee034-162">mais recente</span><span class="sxs-lookup"><span data-stu-id="ee034-162">latest</span></span> |<span data-ttu-id="ee034-163">não</span><span class="sxs-lookup"><span data-stu-id="ee034-163">no</span></span> |
| <span data-ttu-id="ee034-164">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="ee034-164">UbuntuLTS</span></span> |<span data-ttu-id="ee034-165">Canônico</span><span class="sxs-lookup"><span data-stu-id="ee034-165">Canonical</span></span> |<span data-ttu-id="ee034-166">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="ee034-166">UbuntuServer</span></span> |<span data-ttu-id="ee034-167">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="ee034-167">14.04.4-LTS</span></span> |<span data-ttu-id="ee034-168">mais recente</span><span class="sxs-lookup"><span data-stu-id="ee034-168">latest</span></span> |<span data-ttu-id="ee034-169">sim</span><span class="sxs-lookup"><span data-stu-id="ee034-169">yes</span></span> |

<span data-ttu-id="ee034-170">Estamos trabalhando com parceiros para incluir a inicialização de nuvem e trabalhar nas imagens que eles fornecem para o Azure.</span><span class="sxs-lookup"><span data-stu-id="ee034-170">We are working with our partners to get cloud-init included and working in the images that they provide to Azure.</span></span>

## <a name="add-a-cloud-init-script-to-the-vm-creation-with-the-azure-cli"></a><span data-ttu-id="ee034-171">Adicionar um script cloud-init à criação da VM com a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="ee034-171">Add a cloud-init script to the VM creation with the Azure CLI</span></span>
<span data-ttu-id="ee034-172">Para iniciar um script de inicialização de nuvem ao criar uma VM no Azure, especifique o arquivo de inicialização de nuvem usando o comutador `--custom-data` da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee034-172">To launch a cloud-init script when creating a VM in Azure, specify the cloud-init file using the Azure CLI `--custom-data` switch.</span></span>

<span data-ttu-id="ee034-173">Crie um grupo de recursos para iniciar VMs com [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="ee034-173">Create a resource group to launch VMs into with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="ee034-174">O exemplo a seguir cria o grupo de recursos chamado *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="ee034-174">The following example creates the resource group named *myResourceGroup*:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="ee034-175">Crie uma VM Linux com [az vm create](/cli/azure/vm#create) usando cloud-init para configurá-la durante a inicialização.</span><span class="sxs-lookup"><span data-stu-id="ee034-175">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="create-a-cloud-init-script-to-set-the-hostname-of-a-linux-vm"></a><span data-ttu-id="ee034-176">Criar um script cloud-init para definir o nome do host de uma VM Linux</span><span class="sxs-lookup"><span data-stu-id="ee034-176">Create a cloud-init script to set the hostname of a Linux VM</span></span>
<span data-ttu-id="ee034-177">Uma das configurações mais simples e mais importantes para qualquer VM do Linux seria o nome do host.</span><span class="sxs-lookup"><span data-stu-id="ee034-177">One of the simplest and most important settings for any Linux VM would be the hostname.</span></span> <span data-ttu-id="ee034-178">Podemos defini-la com facilidade usando o cloud-init com este script.</span><span class="sxs-lookup"><span data-stu-id="ee034-178">We can easily set this using cloud-init with this script.</span></span>  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a><span data-ttu-id="ee034-179">Script de inicialização de nuvem de exemplo chamado `cloud_config_hostname.txt`.</span><span class="sxs-lookup"><span data-stu-id="ee034-179">Example cloud-init script named `cloud_config_hostname.txt`.</span></span>
```yaml
#cloud-config
hostname: myservername
```

<span data-ttu-id="ee034-180">Durante a inicialização inicial da VM, esse script cloud-init define o nome do host como *myservername*.</span><span class="sxs-lookup"><span data-stu-id="ee034-180">During the initial startup of the VM, this cloud-init script sets the hostname to *myservername*.</span></span> <span data-ttu-id="ee034-181">Crie uma VM Linux com [az vm create](/cli/azure/vm#create) usando cloud-init para configurá-la durante a inicialização.</span><span class="sxs-lookup"><span data-stu-id="ee034-181">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

<span data-ttu-id="ee034-182">Faça logon e verifique o nome do host das novas VMs.</span><span class="sxs-lookup"><span data-stu-id="ee034-182">Login and verify the hostname of the new VM.</span></span>

```bash
ssh myVM
hostname
myservername
```

## <a name="create-a-cloud-init-script"></a><span data-ttu-id="ee034-183">Criar um script cloud-init</span><span class="sxs-lookup"><span data-stu-id="ee034-183">Create a cloud-init script</span></span>
<span data-ttu-id="ee034-184">Por segurança, é recomendável que a VM do Ubuntu seja atualizada na primeira inicialização.</span><span class="sxs-lookup"><span data-stu-id="ee034-184">For security, you want your Ubuntu VM to update on the first boot.</span></span> <span data-ttu-id="ee034-185">Usando cloud-init, podemos fazer isso com o script a seguir, dependendo da distribuição do Linux que você esteja usando.</span><span class="sxs-lookup"><span data-stu-id="ee034-185">Using cloud-init we can do that with the follow script, depending on the Linux distribution you are using.</span></span>

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-the-debian-family"></a><span data-ttu-id="ee034-186">Script de inicialização de nuvem de exemplo `cloud_config_apt_upgrade.txt` para a família Debian</span><span class="sxs-lookup"><span data-stu-id="ee034-186">Example cloud-init script `cloud_config_apt_upgrade.txt` for the Debian Family</span></span>
```yaml
#cloud-config
apt_upgrade: true
```

<span data-ttu-id="ee034-187">Depois que o Linux for inicializado, todos os pacotes instalados serão atualizados por meio de **apt-get**.</span><span class="sxs-lookup"><span data-stu-id="ee034-187">After Linux has booted, all the installed packages are updated via **apt-get**.</span></span> <span data-ttu-id="ee034-188">Crie uma VM Linux com [az vm create](/cli/azure/vm#create) usando cloud-init para configurá-la durante a inicialização.</span><span class="sxs-lookup"><span data-stu-id="ee034-188">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_apt_upgrade.txt
```

<span data-ttu-id="ee034-189">Faça logon e verifique se todos os pacotes foram atualizados.</span><span class="sxs-lookup"><span data-stu-id="ee034-189">Login and verify all packages are updated.</span></span>

```bash
ssh myUbuntuVM
sudo apt-get upgrade
Reading package lists... Done
Building dependency tree
Reading state information... Done
Calculating upgrade... Done
The following packages have been kept back:
  linux-generic linux-headers-generic linux-image-generic
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
```

## <a name="create-a-cloud-init-script-to-add-a-user-to-linux"></a><span data-ttu-id="ee034-190">Criar um script cloud-init para adicionar um usuário ao Linux</span><span class="sxs-lookup"><span data-stu-id="ee034-190">Create a cloud-init script to add a user to Linux</span></span>
<span data-ttu-id="ee034-191">Uma das primeiras tarefas em qualquer nova VM do Linux é adicionar um usuário para você ou para evitar o uso de *root*.</span><span class="sxs-lookup"><span data-stu-id="ee034-191">One of the first tasks on any new Linux VM is to add a user for yourself or to avoid using *root*.</span></span> <span data-ttu-id="ee034-192">Chaves SSH são uma prática recomendada de segurança e usabilidade e são adicionadas ao arquivo *~/.ssh/authorized_keys* com esse script cloud-init.</span><span class="sxs-lookup"><span data-stu-id="ee034-192">SSH keys are best practice for security and for usability and they are added to the *~/.ssh/authorized_keys* file with this cloud-init script.</span></span>

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a><span data-ttu-id="ee034-193">Script de inicialização de nuvem de exemplo `cloud_config_add_users.txt` para a família Debian</span><span class="sxs-lookup"><span data-stu-id="ee034-193">Example cloud-init script `cloud_config_add_users.txt` for Debian Family</span></span>
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

<span data-ttu-id="ee034-194">Depois que o Linux for inicializado, todos os usuários listados serão criados e adicionados ao grupo sudo.</span><span class="sxs-lookup"><span data-stu-id="ee034-194">After Linux has booted, all the listed users are created and added to the sudo group.</span></span> <span data-ttu-id="ee034-195">Crie uma VM Linux com [az vm create](/cli/azure/vm#create) usando cloud-init para configurá-la durante a inicialização.</span><span class="sxs-lookup"><span data-stu-id="ee034-195">Create a Linux VM with [az vm create](/cli/azure/vm#create) using cloud-init to configure it during boot.</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_add_users.txt
```

<span data-ttu-id="ee034-196">Faça logon e verifique o usuário recém-criado.</span><span class="sxs-lookup"><span data-stu-id="ee034-196">Login and verify the newly created user.</span></span>

```bash
ssh myVM
cat /etc/group
```

<span data-ttu-id="ee034-197">Saída</span><span class="sxs-lookup"><span data-stu-id="ee034-197">Output</span></span>

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a><span data-ttu-id="ee034-198">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ee034-198">Next steps</span></span>
<span data-ttu-id="ee034-199">A inicialização de nuvem está se tornando uma maneira padrão de modificar sua VM do Linux na inicialização.</span><span class="sxs-lookup"><span data-stu-id="ee034-199">Cloud-init is becoming one standard way to modify your Linux VM on boot.</span></span> <span data-ttu-id="ee034-200">O Azure também tem extensões de VM, que permitem modificar a VM do Linux na inicialização ou durante sua execução.</span><span class="sxs-lookup"><span data-stu-id="ee034-200">Azure also has VM extensions, which allow you to modify your LinuxVM on boot or while it is running.</span></span> <span data-ttu-id="ee034-201">Por exemplo, você pode usar a VMAccessExtension do Azure para redefinir informações de SSH ou de usuário durante a execução da VM.</span><span class="sxs-lookup"><span data-stu-id="ee034-201">For example, you can use the Azure VMAccessExtension to reset SSH or user information while the VM is running.</span></span> <span data-ttu-id="ee034-202">Com a inicialização de nuvem, será necessária uma reinicialização para redefinir a senha.</span><span class="sxs-lookup"><span data-stu-id="ee034-202">With cloud-init, you would need a reboot to reset the password.</span></span>

[<span data-ttu-id="ee034-203">Sobre os recursos e extensões de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="ee034-203">About virtual machine extensions and features</span></span>](extensions-features.md)

[<span data-ttu-id="ee034-204">Gerenciar usuários, SSH e verificar ou reparar discos em VMs do Linux do Azure usando a extensão VMAccess</span><span class="sxs-lookup"><span data-stu-id="ee034-204">Manage users, SSH, and check or repair disks on Azure Linux VMs using the VMAccess Extension</span></span>](using-vmaccess-extension.md)