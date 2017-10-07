---
title: aaaHow toocreate imagens da VM Azure Linux com Packer | Microsoft Docs
description: "Saiba como imagens de toocreate Packer toouse de máquinas virtuais Linux no Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/18/2017
ms.author: iainfou
ms.openlocfilehash: 5990598859e73efac477884bc8de5fd5138bf6e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-packer-toocreate-linux-virtual-machine-images-in-azure"></a><span data-ttu-id="78fbb-103">Como as imagens de máquina virtual do toouse Packer toocreate Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="78fbb-103">How toouse Packer toocreate Linux virtual machine images in Azure</span></span>
<span data-ttu-id="78fbb-104">Cada máquina virtual (VM) no Azure é criada a partir de uma imagem que define hello distribuição Linux e a versão do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="78fbb-104">Each virtual machine (VM) in Azure is created from an image that defines hello Linux distribution and OS version.</span></span> <span data-ttu-id="78fbb-105">As imagens podem incluir configurações e aplicativos pré-instalados.</span><span class="sxs-lookup"><span data-stu-id="78fbb-105">Images can include pre-installed applications and configurations.</span></span> <span data-ttu-id="78fbb-106">Hello Azure Marketplace fornece muitas imagens primeira e terceiro para distribuições mais comuns e ambientes de aplicativo, ou você pode criar suas próprias necessidades de tooyour personalizadas de imagens personalizadas.</span><span class="sxs-lookup"><span data-stu-id="78fbb-106">hello Azure Marketplace provides many first and third-party images for most common distributions and application environments, or you can create your own custom images tailored tooyour needs.</span></span> <span data-ttu-id="78fbb-107">Este artigo detalha como toouse Olá abrir a ferramenta de origem [Packer](https://www.packer.io/) toodefine e criar imagens personalizadas no Azure.</span><span class="sxs-lookup"><span data-stu-id="78fbb-107">This article details how toouse hello open source tool [Packer](https://www.packer.io/) toodefine and build custom images in Azure.</span></span>


## <a name="create-azure-resource-group"></a><span data-ttu-id="78fbb-108">Criar um grupo de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="78fbb-108">Create Azure resource group</span></span>
<span data-ttu-id="78fbb-109">Durante o processo de compilação hello, Packer cria temporários recursos do Azure, ele cria a VM de origem hello.</span><span class="sxs-lookup"><span data-stu-id="78fbb-109">During hello build process, Packer creates temporary Azure resources as it builds hello source VM.</span></span> <span data-ttu-id="78fbb-110">toocapture que a VM de origem para uso como uma imagem, você deve definir um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="78fbb-110">toocapture that source VM for use as an image, you must define a resource group.</span></span> <span data-ttu-id="78fbb-111">Hello saída do processo de compilação Packer Olá é armazenada no grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="78fbb-111">hello output from hello Packer build process is stored in this resource group.</span></span>

<span data-ttu-id="78fbb-112">Crie um grupo de recursos com [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="78fbb-112">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="78fbb-113">Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *eastus* local:</span><span class="sxs-lookup"><span data-stu-id="78fbb-113">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create -n myResourceGroup -l eastus
```


## <a name="create-azure-credentials"></a><span data-ttu-id="78fbb-114">Criar as credenciais do Azure</span><span class="sxs-lookup"><span data-stu-id="78fbb-114">Create Azure credentials</span></span>
<span data-ttu-id="78fbb-115">O Packer se autentica no Azure usando uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="78fbb-115">Packer authenticates with Azure using a service principal.</span></span> <span data-ttu-id="78fbb-116">Uma entidade de serviço do Azure é uma identidade de segurança que você pode usar com aplicativos, serviços e ferramentas de automação como o Packer.</span><span class="sxs-lookup"><span data-stu-id="78fbb-116">An Azure service principal is a security identity that you can use with apps, services, and automation tools like Packer.</span></span> <span data-ttu-id="78fbb-117">Controlar e definir permissões de saudação como entidade de serviço toowhat operações Olá pode executar no Azure.</span><span class="sxs-lookup"><span data-stu-id="78fbb-117">You control and define hello permissions as toowhat operations hello service principal can perform in Azure.</span></span>

<span data-ttu-id="78fbb-118">Criar um serviço principal com [az ad sp criar-para-rbac](/cli/azure/ad/sp#create-for-rbac) e as credenciais de saudação de saída que Packer precisa:</span><span class="sxs-lookup"><span data-stu-id="78fbb-118">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output hello credentials that Packer needs:</span></span>

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

<span data-ttu-id="78fbb-119">Um exemplo da saída de hello de saudação anterior comandos é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="78fbb-119">An example of hello output from hello preceding commands is as follows:</span></span>

```azurecli
"f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
"0e760437-bf34-4aad-9f8d-870be799c55d",
"72f988bf-86f1-41af-91ab-2d7cd011db47"
```

<span data-ttu-id="78fbb-120">tooauthenticate tooAzure, você também precisa tooobtain ID de sua assinatura do Azure com [Mostrar de conta az](/cli/azure/account#show):</span><span class="sxs-lookup"><span data-stu-id="78fbb-120">tooauthenticate tooAzure, you also need tooobtain your Azure subscription ID with [az account show](/cli/azure/account#show):</span></span>

```azurecli
az account show --query [id] --output tsv
```

<span data-ttu-id="78fbb-121">Use saída Olá desses dois comandos na próxima etapa de saudação.</span><span class="sxs-lookup"><span data-stu-id="78fbb-121">You use hello output from these two commands in hello next step.</span></span>


## <a name="define-packer-template"></a><span data-ttu-id="78fbb-122">Definir modelo do Packer</span><span class="sxs-lookup"><span data-stu-id="78fbb-122">Define Packer template</span></span>
<span data-ttu-id="78fbb-123">toobuild imagens, criar um modelo como um arquivo JSON.</span><span class="sxs-lookup"><span data-stu-id="78fbb-123">toobuild images, you create a template as a JSON file.</span></span> <span data-ttu-id="78fbb-124">No modelo de hello, definir construtores e provisioners realizarem Olá real do processo de compilação.</span><span class="sxs-lookup"><span data-stu-id="78fbb-124">In hello template, you define builders and provisioners that carry out hello actual build process.</span></span> <span data-ttu-id="78fbb-125">Packer tem um [provedor do Azure](https://www.packer.io/docs/builders/azure.html) que permite a você toodefine Azure recursos, como credenciais do serviço principal do hello criados no hello anterior da etapa.</span><span class="sxs-lookup"><span data-stu-id="78fbb-125">Packer has a [provisioner for Azure](https://www.packer.io/docs/builders/azure.html) that allows you toodefine Azure resources, such as hello service principal credentials created in hello preceding step.</span></span>

<span data-ttu-id="78fbb-126">Crie um arquivo chamado *ubuntu.json* e colar Olá conteúdo a seguir.</span><span class="sxs-lookup"><span data-stu-id="78fbb-126">Create a file named *ubuntu.json* and paste hello following content.</span></span> <span data-ttu-id="78fbb-127">Insira seus próprios valores para os seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="78fbb-127">Enter your own values for hello following:</span></span>

| <span data-ttu-id="78fbb-128">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="78fbb-128">Parameter</span></span>                           | <span data-ttu-id="78fbb-129">Onde tooobtain</span><span class="sxs-lookup"><span data-stu-id="78fbb-129">Where tooobtain</span></span> |
|-------------------------------------|----------------------------------------------------|
| <span data-ttu-id="78fbb-130">*client_id*</span><span class="sxs-lookup"><span data-stu-id="78fbb-130">*client_id*</span></span>                         | <span data-ttu-id="78fbb-131">Primeira linha da saída do comando create `az ad sp` – *appId*</span><span class="sxs-lookup"><span data-stu-id="78fbb-131">First line of output from `az ad sp` create command - *appId*</span></span> |
| <span data-ttu-id="78fbb-132">*client_secret*</span><span class="sxs-lookup"><span data-stu-id="78fbb-132">*client_secret*</span></span>                     | <span data-ttu-id="78fbb-133">Segunda linha da saída do comando create `az ad sp` – *password*</span><span class="sxs-lookup"><span data-stu-id="78fbb-133">Second line of output from `az ad sp` create command - *password*</span></span> |
| <span data-ttu-id="78fbb-134">*tenant_id*</span><span class="sxs-lookup"><span data-stu-id="78fbb-134">*tenant_id*</span></span>                         | <span data-ttu-id="78fbb-135">Terceira linha da saída do comando create `az ad sp` – *tenant*</span><span class="sxs-lookup"><span data-stu-id="78fbb-135">Third line of output from `az ad sp` create command - *tenant*</span></span> |
| <span data-ttu-id="78fbb-136">*subscription_id*</span><span class="sxs-lookup"><span data-stu-id="78fbb-136">*subscription_id*</span></span>                   | <span data-ttu-id="78fbb-137">Saída do comando `az account show`</span><span class="sxs-lookup"><span data-stu-id="78fbb-137">Output from `az account show` command</span></span> |
| <span data-ttu-id="78fbb-138">*managed_image_resource_group_name*</span><span class="sxs-lookup"><span data-stu-id="78fbb-138">*managed_image_resource_group_name*</span></span> | <span data-ttu-id="78fbb-139">Nome do grupo de recursos que você criou na etapa primeiro Olá</span><span class="sxs-lookup"><span data-stu-id="78fbb-139">Name of resource group you created in hello first step</span></span> |
| <span data-ttu-id="78fbb-140">*managed_image_name*</span><span class="sxs-lookup"><span data-stu-id="78fbb-140">*managed_image_name*</span></span>                | <span data-ttu-id="78fbb-141">Nome de imagem de disco gerenciado Olá criado</span><span class="sxs-lookup"><span data-stu-id="78fbb-141">Name for hello managed disk image that is created</span></span> |


```json
{
  "builders": [{
    "type": "azure-arm",

    "client_id": "f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
    "client_secret": "0e760437-bf34-4aad-9f8d-870be799c55d",
    "tenant_id": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "subscription_id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx",

    "managed_image_resource_group_name": "myResourceGroup",
    "managed_image_name": "myPackerImage",

    "os_type": "Linux",
    "image_publisher": "Canonical",
    "image_offer": "UbuntuServer",
    "image_sku": "16.04-LTS",

    "azure_tags": {
        "dept": "Engineering",
        "task": "Image deployment"
    },

    "location": "East US",
    "vm_size": "Standard_DS2_v2"
  }],
  "provisioners": [{
    "execute_command": "chmod +x {{ .Path }}; {{ .Vars }} sudo -E sh '{{ .Path }}'",
    "inline": [
      "apt-get update",
      "apt-get upgrade -y",
      "apt-get -y install nginx",

      "/usr/sbin/waagent -force -deprovision+user && export HISTSIZE=0 && sync"
    ],
    "inline_shebang": "/bin/sh -x",
    "type": "shell"
  }]
}
```

<span data-ttu-id="78fbb-142">Este modelo cria uma imagem Ubuntu 16.04 LTS, instala NGINX e deprovisions Olá VM.</span><span class="sxs-lookup"><span data-stu-id="78fbb-142">This template builds an Ubuntu 16.04 LTS image, installs NGINX, then deprovisions hello VM.</span></span>

> [!NOTE]
> <span data-ttu-id="78fbb-143">Se você expandir este credenciais do usuário do modelo tooprovision, ajustar o comando de provedor Olá deprovisions Olá tooread do agente do Azure `-deprovision` em vez de `deprovision+user`.</span><span class="sxs-lookup"><span data-stu-id="78fbb-143">If you expand on this template tooprovision user credentials, adjust hello provisioner command that deprovisions hello Azure agent tooread `-deprovision` rather than `deprovision+user`.</span></span>
> <span data-ttu-id="78fbb-144">Olá `+user` sinalizador remove todas as contas de usuário da VM de origem hello.</span><span class="sxs-lookup"><span data-stu-id="78fbb-144">hello `+user` flag removes all user accounts from hello source VM.</span></span>


## <a name="build-packer-image"></a><span data-ttu-id="78fbb-145">Criar uma imagem do Packer</span><span class="sxs-lookup"><span data-stu-id="78fbb-145">Build Packer image</span></span>
<span data-ttu-id="78fbb-146">Se ainda não tiver instalado em seu computador local, de Packer [siga as instruções de instalação do hello Packer](https://www.packer.io/docs/install/index.html).</span><span class="sxs-lookup"><span data-stu-id="78fbb-146">If you don't already have Packer installed on your local machine, [follow hello Packer installation instructions](https://www.packer.io/docs/install/index.html).</span></span>

<span data-ttu-id="78fbb-147">Crie imagem Olá especificando seu Packer arquivo de modelo da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="78fbb-147">Build hello image by specifying your Packer template file as follows:</span></span>

```bash
./packer build ubuntu.json
```

<span data-ttu-id="78fbb-148">Um exemplo da saída de hello de saudação anterior comandos é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="78fbb-148">An example of hello output from hello preceding commands is as follows:</span></span>

```bash
azure-arm output will be in this color.

==> azure-arm: Running builder ...
    azure-arm: Creating Azure Resource Manager (ARM) client ...
==> azure-arm: Creating resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> Location          : ‘East US’
==> azure-arm:  -> Tags              :
==> azure-arm:  ->> dept : Engineering
==> azure-arm:  ->> task : Image deployment
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> DeploymentName    : ‘pkrdpswtxmqm7ly’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> DeploymentName    : ‘pkrdpswtxmqm7ly’
==> azure-arm: Getting hello VM’s IP address ...
==> azure-arm:  -> ResourceGroupName   : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> PublicIPAddressName : ‘packerPublicIP’
==> azure-arm:  -> NicName             : ‘packerNic’
==> azure-arm:  -> Network Connection  : ‘PublicEndpoint’
==> azure-arm:  -> IP Address          : ‘40.76.218.147’
==> azure-arm: Waiting for SSH toobecome available...
==> azure-arm: Connected tooSSH!
==> azure-arm: Provisioning with shell script: /var/folders/h1/ymh5bdx15wgdn5hvgj1wc0zh0000gn/T/packer-shell868574263
    azure-arm: WARNING! hello waagent service will be stopped.
    azure-arm: WARNING! Cached DHCP leases will be deleted.
    azure-arm: WARNING! root password will be disabled. You will not be able toologin as root.
    azure-arm: WARNING! /etc/resolvconf/resolv.conf.d/tail and /etc/resolvconf/resolv.conf.d/original will be deleted.
    azure-arm: WARNING! packer account and entire home directory will be deleted.
==> azure-arm: Querying hello machine’s properties ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> ComputeName       : ‘pkrvmswtxmqm7ly’
==> azure-arm:  -> Managed OS Disk   : ‘/subscriptions/guid/resourceGroups/packer-Resource-Group-swtxmqm7ly/providers/Microsoft.Compute/disks/osdisk’
==> azure-arm: Powering off machine ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> ComputeName       : ‘pkrvmswtxmqm7ly’
==> azure-arm: Capturing image ...
==> azure-arm:  -> Compute ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> Compute Name              : ‘pkrvmswtxmqm7ly’
==> azure-arm:  -> Compute Location          : ‘East US’
==> azure-arm:  -> Image ResourceGroupName   : ‘myResourceGroup’
==> azure-arm:  -> Image Name                : ‘myPackerImage’
==> azure-arm:  -> Image Location            : ‘eastus’
==> azure-arm: Deleting resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm: Deleting hello temporary OS disk ...
==> azure-arm:  -> OS Disk : skipping, managed disk was used...
Build ‘azure-arm’ finished.

==> Builds finished. hello artifacts of successful builds are:
--> azure-arm: Azure.ResourceManagement.VMImage:

ManagedImageResourceGroupName: myResourceGroup
ManagedImageName: myPackerImage
ManagedImageLocation: eastus
```


## <a name="create-vm-from-azure-image"></a><span data-ttu-id="78fbb-149">Criar uma VM com base em uma Imagem do Azure</span><span class="sxs-lookup"><span data-stu-id="78fbb-149">Create VM from Azure Image</span></span>
<span data-ttu-id="78fbb-150">Agora você pode criar uma VM com base na Imagem com [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="78fbb-150">You can now create a VM from your Image with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="78fbb-151">Especificar Olá imagem criado com hello `--image` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="78fbb-151">Specify hello Image you created with hello `--image` parameter.</span></span> <span data-ttu-id="78fbb-152">Olá, exemplo a seguir cria uma VM denominada *myVM* de *myPackerImage* e gera as chaves de SSH se eles ainda não existir:</span><span class="sxs-lookup"><span data-stu-id="78fbb-152">hello following example creates a VM named *myVM* from *myPackerImage* and generates SSH keys if they do not already exist:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image myPackerImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="78fbb-153">Ele usa Olá toocreate de alguns minutos VM.</span><span class="sxs-lookup"><span data-stu-id="78fbb-153">It takes a few minutes toocreate hello VM.</span></span> <span data-ttu-id="78fbb-154">Quando Olá VM tiver sido criado, tome nota da saudação `publicIpAddress` exibido pelo Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="78fbb-154">Once hello VM has been created, take note of hello `publicIpAddress` displayed by hello Azure CLI.</span></span> <span data-ttu-id="78fbb-155">Esse endereço é o site NGINX Olá tooaccess usado por meio de um navegador da web.</span><span class="sxs-lookup"><span data-stu-id="78fbb-155">This address is used tooaccess hello NGINX site via a web browser.</span></span>

<span data-ttu-id="78fbb-156">tooallow web tooreach tráfego sua VM, abra a porta 80 da saudação da Internet com [az vm abrir portas](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="78fbb-156">tooallow web traffic tooreach your VM, open port 80 from hello Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli
az vm open-port \
    --resource-group myResourceGroup \
    --name myVM \
    --port 80
```

## <a name="test-vm-and-nginx"></a><span data-ttu-id="78fbb-157">Testar a VM e o NGINX</span><span class="sxs-lookup"><span data-stu-id="78fbb-157">Test VM and NGINX</span></span>
<span data-ttu-id="78fbb-158">Agora você pode abrir um navegador da web e digite `http://publicIpAddress` na barra de endereços de saudação.</span><span class="sxs-lookup"><span data-stu-id="78fbb-158">Now you can open a web browser and enter `http://publicIpAddress` in hello address bar.</span></span> <span data-ttu-id="78fbb-159">Fornecer seu próprio público endereço IP da saudação VM criar processo.</span><span class="sxs-lookup"><span data-stu-id="78fbb-159">Provide your own public IP address from hello VM create process.</span></span> <span data-ttu-id="78fbb-160">página NGINX saudação padrão é exibida como Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="78fbb-160">hello default NGINX page is displayed as in hello following example:</span></span>

![Site padrão NGINX](./media/build-image-with-packer/nginx.png) 


## <a name="next-steps"></a><span data-ttu-id="78fbb-162">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="78fbb-162">Next steps</span></span>
<span data-ttu-id="78fbb-163">Neste exemplo, você usou Packer toocreate uma imagem de VM com NGINX já instalado.</span><span class="sxs-lookup"><span data-stu-id="78fbb-163">In this example, you used Packer toocreate a VM image with NGINX already installed.</span></span> <span data-ttu-id="78fbb-164">Você pode usar esta imagem VM junto com a implantação fluxos de trabalho existentes, como toodeploy tooVMs seu aplicativo criado a partir de saudação imagem com Ansible, Chef ou Puppet.</span><span class="sxs-lookup"><span data-stu-id="78fbb-164">You can use this VM image alongside existing deployment workflows, such as toodeploy your app tooVMs created from hello Image with Ansible, Chef, or Puppet.</span></span>

<span data-ttu-id="78fbb-165">Para obter outros modelos de exemplo do Packer para outras distribuições do Linux, consulte [este repositório GitHub](https://github.com/hashicorp/packer/tree/master/examples/azure).</span><span class="sxs-lookup"><span data-stu-id="78fbb-165">For additional example Packer templates for other Linux distros, see [this GitHub repo](https://github.com/hashicorp/packer/tree/master/examples/azure).</span></span>