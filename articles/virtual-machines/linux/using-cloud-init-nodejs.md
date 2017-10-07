---
title: "aaaUsing init nuvem toocustomize uma VM do Linux durante a criação no Azure | Microsoft Docs"
description: "Como toocustomize de nuvem init toouse uma VM do Linux durante a criação com hello 1.0 da CLI do Azure"
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/26/2016
ms.author: v-livech
ms.openlocfilehash: b9f480bd04029956d0593bbef931795733cbc2f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-cloud-init-toocustomize-a-linux-vm-during-creation-with-hello-azure-cli-10"></a><span data-ttu-id="760a4-103">Use a nuvem init toocustomize uma VM do Linux durante a criação com hello 1.0 da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="760a4-103">Use cloud-init toocustomize a Linux VM during creation with hello Azure CLI 1.0</span></span>
<span data-ttu-id="760a4-104">Este artigo mostra como toomake uma tooset de script de inicialização de nuvem Olá hostname, atualizar os pacotes instalados e gerenciar contas de usuário.</span><span class="sxs-lookup"><span data-stu-id="760a4-104">This article shows how toomake a cloud-init script tooset hello hostname, update installed packages, and manage user accounts.</span></span>  <span data-ttu-id="760a4-105">scripts de inicialização de nuvem Olá são chamados durante a saudação criação de VM da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="760a4-105">hello cloud-init scripts are called during hello VM creation from Azure CLI.</span></span>  <span data-ttu-id="760a4-106">artigo Olá requer:</span><span class="sxs-lookup"><span data-stu-id="760a4-106">hello article requires:</span></span>

* <span data-ttu-id="760a4-107">uma conta do Azure ([obtenha uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/)).</span><span class="sxs-lookup"><span data-stu-id="760a4-107">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="760a4-108">Olá [CLI do Azure](../../cli-install-nodejs.md) conectado `azure login`.</span><span class="sxs-lookup"><span data-stu-id="760a4-108">hello [Azure CLI](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="760a4-109">Olá CLI do Azure *devem estar no* modo do Azure Resource Manager `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="760a4-109">hello Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="760a4-110">Tarefa de saudação do CLI versões toocomplete</span><span class="sxs-lookup"><span data-stu-id="760a4-110">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="760a4-111">Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:</span><span class="sxs-lookup"><span data-stu-id="760a4-111">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="760a4-112">[1.0 de CLI do Azure](#quick-commands) – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)</span><span class="sxs-lookup"><span data-stu-id="760a4-112">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="760a4-113">[2.0 do CLI do Azure](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="760a4-113">[Azure CLI 2.0](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="quick-commands"></a><span data-ttu-id="760a4-114">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="760a4-114">Quick Commands</span></span>
<span data-ttu-id="760a4-115">Crie um script de nuvem init.txt que define o nome de host hello, todos os pacotes de atualizações e adiciona um tooLinux de usuário sudo.</span><span class="sxs-lookup"><span data-stu-id="760a4-115">Create a cloud-init.txt script that sets hello hostname, updates all packages, and adds a sudo user tooLinux.</span></span>

```sh
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
<span data-ttu-id="760a4-116">Crie um toolaunch do grupo de recursos de VMs em.</span><span class="sxs-lookup"><span data-stu-id="760a4-116">Create a resource group toolaunch VMs into.</span></span>

```azurecli
azure group create myResourceGroup westus
```

<span data-ttu-id="760a4-117">Criar uma VM do Linux usando a nuvem init tooconfigure-lo durante a inicialização.</span><span class="sxs-lookup"><span data-stu-id="760a4-117">Create a Linux VM using cloud-init tooconfigure it during boot.</span></span>

```azurecli
azure vm create \
  -g myResourceGroup \
  -n myVM \
  -l westus \
  -y Linux \
  -f myVMnic \
  -F myVNet \
  -P 10.0.0.0/22 \
  -j mySubnet \
  -k 10.0.0.0/24 \
  -Q canonical:ubuntuserver:14.04.2-LTS:latest \
  -M ~/.ssh/id_rsa.pub \
  -u myAdminUser \
  -C cloud-init.txt
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="760a4-118">Passo a passo detalhado</span><span class="sxs-lookup"><span data-stu-id="760a4-118">Detailed walkthrough</span></span>
### <a name="introduction"></a><span data-ttu-id="760a4-119">Introdução</span><span class="sxs-lookup"><span data-stu-id="760a4-119">Introduction</span></span>
<span data-ttu-id="760a4-120">Quando você inicia uma nova VM do Linux, você obtém uma VM padrão do Linux sem nada personalizado nem pronta para suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="760a4-120">When you launch a new Linux VM, you are getting a standard Linux VM with nothing customized or ready for your needs.</span></span> <span data-ttu-id="760a4-121">[Nuvem init](https://cloudinit.readthedocs.org) é tooinject uma maneira padrão um script ou configurações na VM Linux como ele está sendo inicializado para Olá primeira vez.</span><span class="sxs-lookup"><span data-stu-id="760a4-121">[Cloud-init](https://cloudinit.readthedocs.org) is a standard way tooinject a script or configuration settings into that Linux VM as it is booting up for hello first time.</span></span>

<span data-ttu-id="760a4-122">No Azure, há três maneiras toomake alterações em uma VM do Linux enquanto ele é implantado ou inicializado.</span><span class="sxs-lookup"><span data-stu-id="760a4-122">On Azure, there are a three different ways toomake changes onto a Linux VM as it is being deployed or booted.</span></span>

* <span data-ttu-id="760a4-123">Insira scripts usando a inicialização de nuvem.</span><span class="sxs-lookup"><span data-stu-id="760a4-123">Inject scripts using cloud-init.</span></span>
* <span data-ttu-id="760a4-124">Inserir scripts usando hello Azure [extensão VMAccess](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="760a4-124">Inject scripts using hello Azure [VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
* <span data-ttu-id="760a4-125">Um modelo do Azure usando a inicialização de nuvem.</span><span class="sxs-lookup"><span data-stu-id="760a4-125">An Azure template using cloud-init.</span></span>
* <span data-ttu-id="760a4-126">Um modelo do Azure usando [CustomScriptExtention](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="760a4-126">An Azure template using [CustomScriptExtention](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="760a4-127">scripts de tooinject a qualquer momento após a inicialização:</span><span class="sxs-lookup"><span data-stu-id="760a4-127">tooinject scripts at any time after boot:</span></span>

* <span data-ttu-id="760a4-128">Comandos diretamente do SSH toorun</span><span class="sxs-lookup"><span data-stu-id="760a4-128">SSH toorun commands directly</span></span>
* <span data-ttu-id="760a4-129">Inserir scripts usando hello Azure [extensão VMAccess](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), imperativa ou em um modelo do Azure</span><span class="sxs-lookup"><span data-stu-id="760a4-129">Inject scripts using hello Azure [VMAccess Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), either imperatively or in an Azure template</span></span>
* <span data-ttu-id="760a4-130">Ferramentas de gerenciamento de configuração, como Ansible, Salt, Chef e Puppet.</span><span class="sxs-lookup"><span data-stu-id="760a4-130">Configuration management tools like Ansible, Salt, Chef, and Puppet.</span></span>

> [!NOTE]
> <span data-ttu-id="760a4-131">: Extensão VMAccess executa um script, como a raiz de saudação do mesmo modo usando SSH pode.</span><span class="sxs-lookup"><span data-stu-id="760a4-131">: VMAccess Extension executes a script as root in hello same way using SSH can.</span></span>  <span data-ttu-id="760a4-132">No entanto, usando a extensão de VM Olá permite que vários recursos que ofertas do Azure que podem ser úteis dependendo do cenário.</span><span class="sxs-lookup"><span data-stu-id="760a4-132">However, using hello VM extension enables several features that Azure offers that can be useful depending upon your scenario.</span></span>
> 
> 

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a><span data-ttu-id="760a4-133">Disponibilidade de inicialização de nuvem em aliases de imagem de criação rápida de uma VM do Azure:</span><span class="sxs-lookup"><span data-stu-id="760a4-133">Cloud-init availability on Azure VM quick-create image aliases:</span></span>
| <span data-ttu-id="760a4-134">Alias</span><span class="sxs-lookup"><span data-stu-id="760a4-134">Alias</span></span> | <span data-ttu-id="760a4-135">Editor</span><span class="sxs-lookup"><span data-stu-id="760a4-135">Publisher</span></span> | <span data-ttu-id="760a4-136">Oferta</span><span class="sxs-lookup"><span data-stu-id="760a4-136">Offer</span></span> | <span data-ttu-id="760a4-137">SKU</span><span class="sxs-lookup"><span data-stu-id="760a4-137">SKU</span></span> | <span data-ttu-id="760a4-138">Versão</span><span class="sxs-lookup"><span data-stu-id="760a4-138">Version</span></span> | <span data-ttu-id="760a4-139">inicialização de nuvem</span><span class="sxs-lookup"><span data-stu-id="760a4-139">cloud-init</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="760a4-140">CentOS</span><span class="sxs-lookup"><span data-stu-id="760a4-140">CentOS</span></span> |<span data-ttu-id="760a4-141">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="760a4-141">OpenLogic</span></span> |<span data-ttu-id="760a4-142">Centos</span><span class="sxs-lookup"><span data-stu-id="760a4-142">Centos</span></span> |<span data-ttu-id="760a4-143">7,2</span><span class="sxs-lookup"><span data-stu-id="760a4-143">7.2</span></span> |<span data-ttu-id="760a4-144">mais recente</span><span class="sxs-lookup"><span data-stu-id="760a4-144">latest</span></span> |<span data-ttu-id="760a4-145">não</span><span class="sxs-lookup"><span data-stu-id="760a4-145">no</span></span> |
| <span data-ttu-id="760a4-146">CoreOS</span><span class="sxs-lookup"><span data-stu-id="760a4-146">CoreOS</span></span> |<span data-ttu-id="760a4-147">CoreOS</span><span class="sxs-lookup"><span data-stu-id="760a4-147">CoreOS</span></span> |<span data-ttu-id="760a4-148">CoreOS</span><span class="sxs-lookup"><span data-stu-id="760a4-148">CoreOS</span></span> |<span data-ttu-id="760a4-149">Estável</span><span class="sxs-lookup"><span data-stu-id="760a4-149">Stable</span></span> |<span data-ttu-id="760a4-150">mais recente</span><span class="sxs-lookup"><span data-stu-id="760a4-150">latest</span></span> |<span data-ttu-id="760a4-151">sim</span><span class="sxs-lookup"><span data-stu-id="760a4-151">yes</span></span> |
| <span data-ttu-id="760a4-152">Debian</span><span class="sxs-lookup"><span data-stu-id="760a4-152">Debian</span></span> |<span data-ttu-id="760a4-153">credativ</span><span class="sxs-lookup"><span data-stu-id="760a4-153">credativ</span></span> |<span data-ttu-id="760a4-154">Debian</span><span class="sxs-lookup"><span data-stu-id="760a4-154">Debian</span></span> |<span data-ttu-id="760a4-155">8</span><span class="sxs-lookup"><span data-stu-id="760a4-155">8</span></span> |<span data-ttu-id="760a4-156">mais recente</span><span class="sxs-lookup"><span data-stu-id="760a4-156">latest</span></span> |<span data-ttu-id="760a4-157">não</span><span class="sxs-lookup"><span data-stu-id="760a4-157">no</span></span> |
| <span data-ttu-id="760a4-158">openSUSE</span><span class="sxs-lookup"><span data-stu-id="760a4-158">openSUSE</span></span> |<span data-ttu-id="760a4-159">SUSE</span><span class="sxs-lookup"><span data-stu-id="760a4-159">SUSE</span></span> |<span data-ttu-id="760a4-160">openSUSE</span><span class="sxs-lookup"><span data-stu-id="760a4-160">openSUSE</span></span> |<span data-ttu-id="760a4-161">13.2</span><span class="sxs-lookup"><span data-stu-id="760a4-161">13.2</span></span> |<span data-ttu-id="760a4-162">mais recente</span><span class="sxs-lookup"><span data-stu-id="760a4-162">latest</span></span> |<span data-ttu-id="760a4-163">não</span><span class="sxs-lookup"><span data-stu-id="760a4-163">no</span></span> |
| <span data-ttu-id="760a4-164">RHEL</span><span class="sxs-lookup"><span data-stu-id="760a4-164">RHEL</span></span> |<span data-ttu-id="760a4-165">Redhat</span><span class="sxs-lookup"><span data-stu-id="760a4-165">Redhat</span></span> |<span data-ttu-id="760a4-166">RHEL</span><span class="sxs-lookup"><span data-stu-id="760a4-166">RHEL</span></span> |<span data-ttu-id="760a4-167">7,2</span><span class="sxs-lookup"><span data-stu-id="760a4-167">7.2</span></span> |<span data-ttu-id="760a4-168">mais recente</span><span class="sxs-lookup"><span data-stu-id="760a4-168">latest</span></span> |<span data-ttu-id="760a4-169">não</span><span class="sxs-lookup"><span data-stu-id="760a4-169">no</span></span> |
| <span data-ttu-id="760a4-170">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="760a4-170">UbuntuLTS</span></span> |<span data-ttu-id="760a4-171">Canônico</span><span class="sxs-lookup"><span data-stu-id="760a4-171">Canonical</span></span> |<span data-ttu-id="760a4-172">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="760a4-172">UbuntuServer</span></span> |<span data-ttu-id="760a4-173">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="760a4-173">14.04.4-LTS</span></span> |<span data-ttu-id="760a4-174">mais recente</span><span class="sxs-lookup"><span data-stu-id="760a4-174">latest</span></span> |<span data-ttu-id="760a4-175">sim</span><span class="sxs-lookup"><span data-stu-id="760a4-175">yes</span></span> |

<span data-ttu-id="760a4-176">A Microsoft está trabalhando com nossos parceiros tooget nuvem-init incluído e trabalhando em imagens de saudação que eles fornecem tooAzure.</span><span class="sxs-lookup"><span data-stu-id="760a4-176">Microsoft is working with our partners tooget cloud-init included and working in hello images that they provide tooAzure.</span></span>

## <a name="adding-a-cloud-init-script-toohello-vm-creation-with-hello-azure-cli"></a><span data-ttu-id="760a4-177">Adicionando uma criação de VM nuvem init script toohello com hello CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="760a4-177">Adding a cloud-init script toohello VM creation with hello Azure CLI</span></span>
<span data-ttu-id="760a4-178">toolaunch um script de inicialização de nuvem ao criar uma VM no Azure, especifique o arquivo de inicialização de nuvem de hello usando Olá CLI do Azure `--custom-data` alternar.</span><span class="sxs-lookup"><span data-stu-id="760a4-178">toolaunch a cloud-init script when creating a VM in Azure, specify hello cloud-init file using hello Azure CLI `--custom-data` switch.</span></span>

<span data-ttu-id="760a4-179">Crie um toolaunch do grupo de recursos de VMs em.</span><span class="sxs-lookup"><span data-stu-id="760a4-179">Create a resource group toolaunch VMs into.</span></span>

```azurecli
azure group create myResourceGroup westus
```

<span data-ttu-id="760a4-180">Criar uma VM do Linux usando a nuvem init tooconfigure-lo durante a inicialização.</span><span class="sxs-lookup"><span data-stu-id="760a4-180">Create a Linux VM using cloud-init tooconfigure it during boot.</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubnet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud-init.txt
```

## <a name="creating-a-cloud-init-script-tooset-hello-hostname-of-a-linux-vm"></a><span data-ttu-id="760a4-181">Criando uma nuvem init script tooset Olá nome de host de uma VM do Linux</span><span class="sxs-lookup"><span data-stu-id="760a4-181">Creating a cloud-init script tooset hello hostname of a Linux VM</span></span>
<span data-ttu-id="760a4-182">Uma das configurações mais importantes para qualquer VM do Linux e hello mais simples seria Olá hostname.</span><span class="sxs-lookup"><span data-stu-id="760a4-182">One of hello simplest and most important settings for any Linux VM would be hello hostname.</span></span> <span data-ttu-id="760a4-183">Podemos defini-la com facilidade usando o cloud-init com este script.</span><span class="sxs-lookup"><span data-stu-id="760a4-183">We can easily set this using cloud-init with this script.</span></span>  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a><span data-ttu-id="760a4-184">Script de inicialização de nuvem de exemplo chamado `cloud_config_hostname.txt`.</span><span class="sxs-lookup"><span data-stu-id="760a4-184">Example cloud-init script named `cloud_config_hostname.txt`.</span></span>
```sh
#cloud-config
hostname: myservername
```

<span data-ttu-id="760a4-185">Durante a inicialização inicial de saudação do hello VM, esse script de inicialização de nuvem define Olá hostname muito`myservername`.</span><span class="sxs-lookup"><span data-stu-id="760a4-185">During hello initial startup of hello VM, this cloud-init script sets hello hostname too`myservername`.</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_hostname.txt
```

<span data-ttu-id="760a4-186">Logon e verifique se o nome de host de saudação do hello nova VM.</span><span class="sxs-lookup"><span data-stu-id="760a4-186">Login and verify hello hostname of hello new VM.</span></span>

```bash
ssh myVM
hostname
myservername
```

## <a name="creating-a-cloud-init-script-tooupdate-linux"></a><span data-ttu-id="760a4-187">Criar um script de inicialização de nuvem tooupdate Linux</span><span class="sxs-lookup"><span data-stu-id="760a4-187">Creating a cloud-init script tooupdate Linux</span></span>
<span data-ttu-id="760a4-188">Para segurança, convém seu tooupdate Ubuntu VM na primeira inicialização de saudação.</span><span class="sxs-lookup"><span data-stu-id="760a4-188">For security, you want your Ubuntu VM tooupdate on hello first boot.</span></span>  <span data-ttu-id="760a4-189">Usando a nuvem init podemos fazer que com hello siga script, dependendo da distribuição de Linux Olá que você está usando.</span><span class="sxs-lookup"><span data-stu-id="760a4-189">Using cloud-init we can do that with hello follow script, depending on hello Linux distribution you are using.</span></span>

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-hello-debian-family"></a><span data-ttu-id="760a4-190">Exemplo de script de inicialização de nuvem `cloud_config_apt_upgrade.txt` para Olá família Debian</span><span class="sxs-lookup"><span data-stu-id="760a4-190">Example cloud-init script `cloud_config_apt_upgrade.txt` for hello Debian Family</span></span>
```sh
#cloud-config
apt_upgrade: true
```

<span data-ttu-id="760a4-191">Depois de Linux foi inicializado, todos os pacotes de saudação instalado são atualizados por meio de `apt-get`.</span><span class="sxs-lookup"><span data-stu-id="760a4-191">After Linux has booted, all hello installed packages are updated via `apt-get`.</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_apt_upgrade.txt
```

<span data-ttu-id="760a4-192">Faça logon e verifique se todos os pacotes foram atualizados.</span><span class="sxs-lookup"><span data-stu-id="760a4-192">Login and verify all packages are updated.</span></span>

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

## <a name="creating-a-cloud-init-script-tooadd-a-user-toolinux"></a><span data-ttu-id="760a4-193">Criando um tooadd de script de inicialização de nuvem tooLinux um usuário</span><span class="sxs-lookup"><span data-stu-id="760a4-193">Creating a cloud-init script tooadd a user tooLinux</span></span>
<span data-ttu-id="760a4-194">Uma das primeiras tarefas hello em qualquer nova VM do Linux é tooadd um usuário para si mesmo ou tooavoid usando `root`.</span><span class="sxs-lookup"><span data-stu-id="760a4-194">One of hello first tasks on any new Linux VM is tooadd a user for yourself or tooavoid using `root`.</span></span> <span data-ttu-id="760a4-195">Chaves de SSH são uma prática recomendada de segurança e facilidade de uso e elas são adicionadas toohello `~/.ssh/authorized_keys` arquivo com esse script de inicialização de nuvem.</span><span class="sxs-lookup"><span data-stu-id="760a4-195">SSH keys are best practice for security and for usability and they are added toohello `~/.ssh/authorized_keys` file with this cloud-init script.</span></span>

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a><span data-ttu-id="760a4-196">Script de inicialização de nuvem de exemplo `cloud_config_add_users.txt` para a família Debian</span><span class="sxs-lookup"><span data-stu-id="760a4-196">Example cloud-init script `cloud_config_add_users.txt` for Debian Family</span></span>
```sh
#cloud-config
users:
  - name: myCloudInitAddedAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myUbuntuVM
```

<span data-ttu-id="760a4-197">Depois de Linux foi inicializado, todos os usuários de saudação listado são toohello criado e adicionado sudo grupo.</span><span class="sxs-lookup"><span data-stu-id="760a4-197">After Linux has booted, all hello listed users are created and added toohello sudo group.</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_add_users.txt
```

<span data-ttu-id="760a4-198">Logon e verifique se o usuário Olá recém-criado.</span><span class="sxs-lookup"><span data-stu-id="760a4-198">Login and verify hello newly created user.</span></span>

```bash
ssh myVM
cat /etc/group
```

<span data-ttu-id="760a4-199">Saída</span><span class="sxs-lookup"><span data-stu-id="760a4-199">Output</span></span>

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a><span data-ttu-id="760a4-200">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="760a4-200">Next Steps</span></span>
<span data-ttu-id="760a4-201">Inicialização de nuvem está se tornando um toomodify de maneira padrão sua VM do Linux na inicialização.</span><span class="sxs-lookup"><span data-stu-id="760a4-201">Cloud-init is becoming one standard way toomodify your Linux VM on boot.</span></span> <span data-ttu-id="760a4-202">O Azure também tem extensões VM, que permitem que você toomodify sua LinuxVM na inicialização ou durante a execução.</span><span class="sxs-lookup"><span data-stu-id="760a4-202">Azure also has VM extensions, which allow you toomodify your LinuxVM on boot or while it is running.</span></span> <span data-ttu-id="760a4-203">Por exemplo, você pode usar hello Azure VMAccessExtension tooreset SSH ou informações do usuário enquanto Olá VM está em execução.</span><span class="sxs-lookup"><span data-stu-id="760a4-203">For example, you can use hello Azure VMAccessExtension tooreset SSH or user information while hello VM is running.</span></span> <span data-ttu-id="760a4-204">Com a inicialização de nuvem, você precisaria de uma senha de saudação do tooreset de reinicialização.</span><span class="sxs-lookup"><span data-stu-id="760a4-204">With cloud-init, you would need a reboot tooreset hello password.</span></span>

[<span data-ttu-id="760a4-205">Sobre os recursos e extensões de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="760a4-205">About virtual machine extensions and features</span></span>](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="760a4-206">Gerenciar usuários, SSH e seleção ou discos de reparo em máquinas virtuais do Linux do Azure usando Olá extensão VMAccess</span><span class="sxs-lookup"><span data-stu-id="760a4-206">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

