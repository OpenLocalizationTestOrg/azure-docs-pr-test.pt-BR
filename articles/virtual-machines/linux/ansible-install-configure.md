---
title: "aaaInstall e configurar Ansible para uso com máquinas virtuais do Azure | Microsoft Docs"
description: Saiba como tooinstall e configurar Ansible para gerenciar recursos do Azure no Ubuntu, CentOS e SLES
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: na
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/25/2017
ms.author: iainfou
ms.openlocfilehash: b33d1893909b6134a5474617c9af2d6e4f627c05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-ansible-toomanage-virtual-machines-in-azure"></a><span data-ttu-id="e81f6-103">Instalar e configurar Ansible toomanage VMs no Azure</span><span class="sxs-lookup"><span data-stu-id="e81f6-103">Install and configure Ansible toomanage virtual machines in Azure</span></span>
<span data-ttu-id="e81f6-104">Este artigo fornece detalhes sobre como tooinstall Ansible e módulos do Azure SDK de Python necessários para alguns dos Olá distribuições de Linux mais comuns.</span><span class="sxs-lookup"><span data-stu-id="e81f6-104">This article details how tooinstall Ansible and required Azure Python SDK modules for some of hello most common Linux distros.</span></span> <span data-ttu-id="e81f6-105">Você pode instalar Ansible em outras distribuições ajustando Olá instalado pacotes toofit sua plataforma específica.</span><span class="sxs-lookup"><span data-stu-id="e81f6-105">You can install Ansible on other distros by adjusting hello installed packages toofit your particular platform.</span></span> <span data-ttu-id="e81f6-106">toocreate Azure recursos de uma maneira segura, você saiba também como toocreate e definir as credenciais para Ansible toouse.</span><span class="sxs-lookup"><span data-stu-id="e81f6-106">toocreate Azure resources in a secure manner, you also learn how toocreate and define credentials for Ansible toouse.</span></span> 

<span data-ttu-id="e81f6-107">Para obter mais opções de instalação e etapas para outras plataformas, consulte Olá [Ansible guia de instalação](https://docs.ansible.com/ansible/intro_installation.html).</span><span class="sxs-lookup"><span data-stu-id="e81f6-107">For more installation options and steps for additional platforms, see hello [Ansible install guide](https://docs.ansible.com/ansible/intro_installation.html).</span></span>


## <a name="install-ansible"></a><span data-ttu-id="e81f6-108">Instalar o Ansible</span><span class="sxs-lookup"><span data-stu-id="e81f6-108">Install Ansible</span></span>
<span data-ttu-id="e81f6-109">Primeiro, crie um grupo de recursos com [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="e81f6-109">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="e81f6-110">Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroupAnsible* em Olá *eastus* local:</span><span class="sxs-lookup"><span data-stu-id="e81f6-110">hello following example creates a resource group named *myResourceGroupAnsible* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroupAnsible --location eastus
```

<span data-ttu-id="e81f6-111">Agora crie uma VM e instalar Ansible para uma saudação distribuições a seguir:</span><span class="sxs-lookup"><span data-stu-id="e81f6-111">Now create a VM and install Ansible for one of hello following distros:</span></span>

- [<span data-ttu-id="e81f6-112">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="e81f6-112">Ubuntu 16.04 LTS</span></span>](#ubuntu1604-lts)
- [<span data-ttu-id="e81f6-113">CentOS 7.3</span><span class="sxs-lookup"><span data-stu-id="e81f6-113">CentOS 7.3</span></span>](#centos-73)
- [<span data-ttu-id="e81f6-114">SLES 12.2 SP2</span><span class="sxs-lookup"><span data-stu-id="e81f6-114">SLES 12.2 SP2</span></span>](#sles-122-sp2)

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="e81f6-115">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="e81f6-115">Ubuntu 16.04 LTS</span></span>
<span data-ttu-id="e81f6-116">Crie uma VM com [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="e81f6-116">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="e81f6-117">Olá, exemplo a seguir cria uma VM denominada *myVMAnsible*:</span><span class="sxs-lookup"><span data-stu-id="e81f6-117">hello following example creates a VM named *myVMAnsible*:</span></span>

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="e81f6-118">SSH tooyour VM usando Olá `publicIpAddress` observado na saudação da operação de criação de saída de hello VM:</span><span class="sxs-lookup"><span data-stu-id="e81f6-118">SSH tooyour VM using hello `publicIpAddress` noted in hello output from hello VM create operation:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="e81f6-119">Na sua VM, instale pacotes de saudação necessária para módulos do Azure SDK de Python hello e Ansible da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="e81f6-119">On your VM, install hello required packages for hello Azure Python SDK modules and Ansible as follows:</span></span>

```bash
## Install pre-requisite packages
sudo apt-get update && sudo apt-get install -y libssl-dev libffi-dev python-dev python-pip

## Install Azure SDKs via pip
pip install "azure==2.0.0rc5" msrestazure

## Install Ansible via apt
sudo apt-get install -y software-properties-common
sudo apt-add-repository -y ppa:ansible/ansible
sudo apt-get update && sudo apt-get install -y ansible
```

<span data-ttu-id="e81f6-120">Agora, vamos passar muito[as credenciais do Azure criar](#create-azure-credentials).</span><span class="sxs-lookup"><span data-stu-id="e81f6-120">Now move on too[Create Azure credentials](#create-azure-credentials).</span></span>


### <a name="centos-73"></a><span data-ttu-id="e81f6-121">CentOS 7.3</span><span class="sxs-lookup"><span data-stu-id="e81f6-121">CentOS 7.3</span></span>
<span data-ttu-id="e81f6-122">Crie uma VM com [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="e81f6-122">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="e81f6-123">Olá, exemplo a seguir cria uma VM denominada *myVMAnsible*:</span><span class="sxs-lookup"><span data-stu-id="e81f6-123">hello following example creates a VM named *myVMAnsible*:</span></span>

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="e81f6-124">SSH tooyour VM usando Olá `publicIpAddress` observado na saudação da operação de criação de saída de hello VM:</span><span class="sxs-lookup"><span data-stu-id="e81f6-124">SSH tooyour VM using hello `publicIpAddress` noted in hello output from hello VM create operation:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="e81f6-125">Na sua VM, instale pacotes de saudação necessária para módulos do Azure SDK de Python hello e Ansible da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="e81f6-125">On your VM, install hello required packages for hello Azure Python SDK modules and Ansible as follows:</span></span>

```bash
## Install pre-requisite packages
sudo yum check-update; sudo yum install -y gcc libffi-devel python-devel openssl-devel epel-release
sudo yum install -y python-pip python-wheel

## Install Azure SDKs via pip
sudo pip install "azure==2.0.0rc5" msrestazure

## Install Ansible via yum
sudo yum install -y ansible
```

<span data-ttu-id="e81f6-126">Agora, vamos passar muito[as credenciais do Azure criar](#create-azure-credentials).</span><span class="sxs-lookup"><span data-stu-id="e81f6-126">Now move on too[Create Azure credentials](#create-azure-credentials).</span></span>


### <a name="sles-122-sp2"></a><span data-ttu-id="e81f6-127">SLES 12.2 SP2</span><span class="sxs-lookup"><span data-stu-id="e81f6-127">SLES 12.2 SP2</span></span>
<span data-ttu-id="e81f6-128">Crie uma VM com [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="e81f6-128">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="e81f6-129">Olá, exemplo a seguir cria uma VM denominada *myVMAnsible*:</span><span class="sxs-lookup"><span data-stu-id="e81f6-129">hello following example creates a VM named *myVMAnsible*:</span></span>

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image SLES \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="e81f6-130">SSH tooyour VM usando Olá `publicIpAddress` observado na saudação da operação de criação de saída de hello VM:</span><span class="sxs-lookup"><span data-stu-id="e81f6-130">SSH tooyour VM using hello `publicIpAddress` noted in hello output from hello VM create operation:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="e81f6-131">Na sua VM, instale pacotes de saudação necessária para módulos do Azure SDK de Python hello e Ansible da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="e81f6-131">On your VM, install hello required packages for hello Azure Python SDK modules and Ansible as follows:</span></span>

```bash
## Install pre-requisite packages
sudo zypper refresh && sudo zypper --non-interactive install gcc libffi-devel-gcc5 python-devel \
    libopenssl-devel python-pip python-setuptools python-azure-sdk

## Install Ansible via zypper
sudo zypper addrepo http://download.opensuse.org/repositories/systemsmanagement/SLE_12_SP2/systemsmanagement.repo
sudo zypper refresh && sudo zypper install ansible
```

<span data-ttu-id="e81f6-132">Agora, vamos passar muito[as credenciais do Azure criar](#create-azure-credentials).</span><span class="sxs-lookup"><span data-stu-id="e81f6-132">Now move on too[Create Azure credentials](#create-azure-credentials).</span></span>


## <a name="create-azure-credentials"></a><span data-ttu-id="e81f6-133">Criar as credenciais do Azure</span><span class="sxs-lookup"><span data-stu-id="e81f6-133">Create Azure credentials</span></span>
<span data-ttu-id="e81f6-134">O Ansible comunica-se com o Azure usando um nome de usuário e uma senha ou uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="e81f6-134">Ansible communicates with Azure using a username and password or a service principal.</span></span> <span data-ttu-id="e81f6-135">Uma entidade de serviço do Azure é uma identidade de segurança que você pode usar com aplicativos, serviços e ferramentas de automação como o Ansible.</span><span class="sxs-lookup"><span data-stu-id="e81f6-135">An Azure service principal is a security identity that you can use with apps, services, and automation tools like Ansible.</span></span> <span data-ttu-id="e81f6-136">Controlar e definir permissões de saudação como entidade de serviço toowhat operações Olá pode executar no Azure.</span><span class="sxs-lookup"><span data-stu-id="e81f6-136">You control and define hello permissions as toowhat operations hello service principal can perform in Azure.</span></span> <span data-ttu-id="e81f6-137">segurança de tooimprove por apenas fornecer um nome de usuário e uma senha, este exemplo cria um serviço básico principal.</span><span class="sxs-lookup"><span data-stu-id="e81f6-137">tooimprove security over just providing a username and password, this example creates a basic service principal.</span></span>

<span data-ttu-id="e81f6-138">Criar um serviço principal com [az ad sp criar-para-rbac](/cli/azure/ad/sp#create-for-rbac) e as credenciais de saudação de saída que Ansible precisa:</span><span class="sxs-lookup"><span data-stu-id="e81f6-138">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output hello credentials that Ansible needs:</span></span>

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

<span data-ttu-id="e81f6-139">Um exemplo da saída de hello de saudação anterior comandos é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="e81f6-139">An example of hello output from hello preceding commands is as follows:</span></span>

```json
[
  "eec5624a-90f8-4386-8a87-02730b5410d5",
  "531dcffa-3aff-4488-99bb-4816c395ea3f",
  "72f988bf-86f1-41af-91ab-2d7cd011db47"
]
```

<span data-ttu-id="e81f6-140">tooauthenticate tooAzure, você também precisa tooobtain ID de sua assinatura do Azure com [Mostrar de conta az](/cli/azure/account#show):</span><span class="sxs-lookup"><span data-stu-id="e81f6-140">tooauthenticate tooAzure, you also need tooobtain your Azure subscription ID with [az account show](/cli/azure/account#show):</span></span>

```azurecli
az account show --query [id] --output tsv
```

<span data-ttu-id="e81f6-141">Use saída Olá desses dois comandos na próxima etapa de saudação.</span><span class="sxs-lookup"><span data-stu-id="e81f6-141">You use hello output from these two commands in hello next step.</span></span>


## <a name="create-ansible-credentials-file"></a><span data-ttu-id="e81f6-142">Criar arquivo de credenciais do Ansible</span><span class="sxs-lookup"><span data-stu-id="e81f6-142">Create Ansible credentials file</span></span>
<span data-ttu-id="e81f6-143">tooprovide credenciais tooAnsible, defina as variáveis de ambiente ou criar um arquivo de credenciais locais.</span><span class="sxs-lookup"><span data-stu-id="e81f6-143">tooprovide credentials tooAnsible, you define environment variables or create a local credentials file.</span></span> <span data-ttu-id="e81f6-144">Para obter mais informações sobre como toodefine Ansible credenciais, consulte [tooAzure fornecendo credenciais módulos](https://docs.ansible.com/ansible/guide_azure.html#providing-credentials-to-azure-modules).</span><span class="sxs-lookup"><span data-stu-id="e81f6-144">For more information about how toodefine Ansible credentials, see [Providing Credentials tooAzure Modules](https://docs.ansible.com/ansible/guide_azure.html#providing-credentials-to-azure-modules).</span></span> 

<span data-ttu-id="e81f6-145">Para um ambiente de desenvolvimento, crie um arquivo de *credenciais* para o Ansible em sua VM host da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="e81f6-145">For a development environment, create a *credentials* file for Ansible on your host VM as follows:</span></span>

```bash
mkdir ~/.azure
vi ~/.azure/credentials
```

<span data-ttu-id="e81f6-146">Olá *credenciais* próprio arquivo combina Olá ID da assinatura com a saída de saudação de criação de uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="e81f6-146">hello *credentials* file itself combines hello subscription ID with hello output of creating a service principal.</span></span> <span data-ttu-id="e81f6-147">Saída de hello anterior [az ad sp criar-para-rbac](/cli/azure/ad/sp#create-for-rbac) comando é Olá mesmo ordem conforme necessário para *client_id*, *segredo*, e *locatário* .</span><span class="sxs-lookup"><span data-stu-id="e81f6-147">Output from hello previous [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) command is hello same order as needed for *client_id*, *secret*, and *tenant*.</span></span> <span data-ttu-id="e81f6-148">Olá seguindo exemplo *credenciais* arquivo mostra esses valores correspondentes a saída anterior hello.</span><span class="sxs-lookup"><span data-stu-id="e81f6-148">hello following example *credentials* file shows these values matching hello previous output.</span></span> <span data-ttu-id="e81f6-149">Insira seus próprios valores da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="e81f6-149">Enter your own values as follows:</span></span>

```bash
[default]
subscription_id=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
client_id=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
secret=b8326643-f7e9-48fb-b0d5-952b68ab3def
tenant=72f988bf-86f1-41af-91ab-2d7cd011db47
```


## <a name="use-ansible-environment-variables"></a><span data-ttu-id="e81f6-150">Usar variáveis de ambiente Ansible</span><span class="sxs-lookup"><span data-stu-id="e81f6-150">Use Ansible environment variables</span></span>
<span data-ttu-id="e81f6-151">Se você for toouse ferramentas como torre Ansible ou Jenkins, você pode definir variáveis de ambiente da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="e81f6-151">If you are going toouse tools such as Ansible Tower or Jenkins, you can define environment variables as follows.</span></span> <span data-ttu-id="e81f6-152">Essas variáveis combinam Olá ID da assinatura com a saída de saudação de criação de um serviço principal.</span><span class="sxs-lookup"><span data-stu-id="e81f6-152">These variables combine hello subscription ID with hello output from creating a service principal.</span></span> <span data-ttu-id="e81f6-153">Saída da saudação anterior [az ad sp criar-para-rbac](/cli/azure/ad/sp#create-for-rbac) comando é Olá mesma ordem conforme necessário para *AZURE_CLIENT_ID*, *AZURE_SECRET*, e *AZURE_ LOCATÁRIO*.</span><span class="sxs-lookup"><span data-stu-id="e81f6-153">Output from hello previous [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) command is hello same order as needed for *AZURE_CLIENT_ID*, *AZURE_SECRET*, and *AZURE_TENANT*.</span></span> 

```bash
export AZURE_SUBSCRIPTION_ID=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
export AZURE_CLIENT_ID=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
export AZURE_SECRET=8326643-f7e9-48fb-b0d5-952b68ab3def
export AZURE_TENANT=72f988bf-86f1-41af-91ab-2d7cd011db47
```

## <a name="next-steps"></a><span data-ttu-id="e81f6-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e81f6-154">Next steps</span></span>
<span data-ttu-id="e81f6-155">Agora você tem Ansible e Olá necessários módulos do Azure SDK de Python instalados e as credenciais definidas para Ansible toouse.</span><span class="sxs-lookup"><span data-stu-id="e81f6-155">You now have Ansible and hello required Azure Python SDK modules installed, and credentials defined for Ansible toouse.</span></span> <span data-ttu-id="e81f6-156">Saiba como muito[criar uma VM com Ansible](ansible-create-vm.md).</span><span class="sxs-lookup"><span data-stu-id="e81f6-156">Learn how too[create a VM with Ansible](ansible-create-vm.md).</span></span> <span data-ttu-id="e81f6-157">Você também pode aprender como muito[criar uma VM do Azure concluída e suporte a recursos com Ansible](ansible-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="e81f6-157">You can also learn how too[create a complete Azure VM and supporting resources with Ansible](ansible-create-complete-vm.md).</span></span>
