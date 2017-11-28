---
title: aaaCreate e carregar uma VM OpenBSD imagem tooAzure | Microsoft Docs
description: "Saiba como toocreate e carregar um disco rígido virtual (VHD) que contém Olá toocreate de sistema operacional OpenBSD uma máquina virtual do Azure por meio da CLI do Azure"
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 1ef30f32-61c1-4ba8-9542-801d7b18e9bf
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: kyliel
ms.openlocfilehash: 0524f45ea1ecec37e55cbe9d54438a571a831de7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-an-openbsd-disk-image-tooazure"></a><span data-ttu-id="e1de1-103">Criar e carregar um tooAzure de imagem de disco OpenBSD</span><span class="sxs-lookup"><span data-stu-id="e1de1-103">Create and Upload an OpenBSD disk image tooAzure</span></span>
<span data-ttu-id="e1de1-104">Este artigo mostra como toocreate e carregar um disco rígido virtual (VHD) que contém Olá OpenBSD sistema de operacional.</span><span class="sxs-lookup"><span data-stu-id="e1de1-104">This article shows you how toocreate and upload a virtual hard disk (VHD) that contains hello OpenBSD operating system.</span></span> <span data-ttu-id="e1de1-105">Depois que você carregá-lo, você pode usá-lo como toocreate sua própria imagem uma máquina virtual (VM) no Azure por meio da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="e1de1-105">After you upload it, you can use it as your own image toocreate a virtual machine (VM) in Azure through Azure CLI.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="e1de1-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e1de1-106">Prerequisites</span></span>
<span data-ttu-id="e1de1-107">Este artigo pressupõe que você tenha Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="e1de1-107">This article assumes that you have hello following items:</span></span>

* <span data-ttu-id="e1de1-108">**Uma assinatura do Azure** - Se não tiver uma conta, você poderá criar uma em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="e1de1-108">**An Azure subscription** - If you don't have an account, you can create one in just a couple of minutes.</span></span> <span data-ttu-id="e1de1-109">Se você tiver uma assinatura do MSDN, confira [Crédito Azure mensal para assinantes do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="e1de1-109">If you have an MSDN subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="e1de1-110">Caso contrário, saiba como muito[criar uma conta de avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e1de1-110">Otherwise, learn how too[create a free trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span>  
* <span data-ttu-id="e1de1-111">**2.0 do CLI do Azure** -Verifique se você tem hello mais recente [2.0 do CLI do Azure](/cli/azure/install-azure-cli) instalado e registrado no tooyour conta do Azure com [logon az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="e1de1-111">**Azure CLI 2.0** - Make sure you have hello latest [Azure CLI 2.0](/cli/azure/install-azure-cli) installed and logged in tooyour Azure account with [az login](/cli/azure/#login).</span></span>
* <span data-ttu-id="e1de1-112">**Sistema de operacional OpenBSD instalado em um arquivo. vhd** -um sistema de operacional OpenBSD (6.1 versão) deve ser instalado tooa do disco rígido virtual.</span><span class="sxs-lookup"><span data-stu-id="e1de1-112">**OpenBSD operating system installed in a .vhd file** - A supported OpenBSD operating system (6.1 version) must be installed tooa virtual hard disk.</span></span> <span data-ttu-id="e1de1-113">Várias ferramentas existem toocreate arquivos. vhd.</span><span class="sxs-lookup"><span data-stu-id="e1de1-113">Multiple tools exist toocreate .vhd files.</span></span> <span data-ttu-id="e1de1-114">Por exemplo, você pode usar uma solução de virtualização, como o arquivo. vhd do Hyper-V toocreate hello e instalar o sistema operacional de saudação.</span><span class="sxs-lookup"><span data-stu-id="e1de1-114">For example, you can use a virtualization solution such as Hyper-V toocreate hello .vhd file and install hello operating system.</span></span> <span data-ttu-id="e1de1-115">Para obter instruções sobre como tooinstall e use o Hyper-V, consulte [instalar o Hyper-V e criar uma máquina virtual](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="e1de1-115">For instructions about how tooinstall and use Hyper-V, see [Install Hyper-V and create a virtual machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>


## <a name="prepare-openbsd-image-for-azure"></a><span data-ttu-id="e1de1-116">Preparar imagem OpenBSD do Azure</span><span class="sxs-lookup"><span data-stu-id="e1de1-116">Prepare OpenBSD image for Azure</span></span>
<span data-ttu-id="e1de1-117">No hello VM onde você instalou o sistema de operacional Olá OpenBSD 6.1, que adicionou suporte de Hyper-V, conclua Olá procedimentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="e1de1-117">On hello VM where you installed hello OpenBSD operating system 6.1, which added Hyper-V support, complete hello following procedures:</span></span>

1. <span data-ttu-id="e1de1-118">Se DHCP não está habilitado durante a instalação, habilite o serviço de saudação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="e1de1-118">If DHCP is not enabled during installation, enable hello service as follows:</span></span>

    ```sh    
    echo dhcp > /etc/hostname.hvn0
    ```

2. <span data-ttu-id="e1de1-119">Instalar um console serial da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="e1de1-119">Set up a serial console as follows:</span></span>

    ```sh
    echo "stty com0 115200" >> /etc/boot.conf
    echo "set tty com0" >> /etc/boot.conf
    ```

3. <span data-ttu-id="e1de1-120">Configure a instalação do pacote da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="e1de1-120">Configure Package installation as follows:</span></span>

    ```sh
    echo "https://ftp.openbsd.org/pub/OpenBSD" > /etc/installurl
    ```
   
4. <span data-ttu-id="e1de1-121">Por padrão, Olá `root` usuário está desabilitado em máquinas virtuais no Azure.</span><span class="sxs-lookup"><span data-stu-id="e1de1-121">By default, hello `root` user is disabled on virtual machines in Azure.</span></span> <span data-ttu-id="e1de1-122">Os usuários podem executar comandos com privilégios elevados usando Olá `doas` comando OpenBSD VM.</span><span class="sxs-lookup"><span data-stu-id="e1de1-122">Users can run commands with elevated privileges by using hello `doas` command on OpenBSD VM.</span></span> <span data-ttu-id="e1de1-123">Doas é habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="e1de1-123">Doas is enabled by default.</span></span> <span data-ttu-id="e1de1-124">Para obter mais informações, consulte [doas.conf](http://man.openbsd.org/doas.conf.5).</span><span class="sxs-lookup"><span data-stu-id="e1de1-124">For more information, see [doas.conf](http://man.openbsd.org/doas.conf.5).</span></span> 

5. <span data-ttu-id="e1de1-125">Instalar e configurar os pré-requisitos para hello Azure agente da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="e1de1-125">Install and configure prerequisites for hello Azure Agent as follows:</span></span>

    ```sh
    pkg_add py-setuptools openssl git
    ln -sf /usr/local/bin/python2.7 /usr/local/bin/python
    ln -sf /usr/local/bin/python2.7-2to3 /usr/local/bin/2to3
    ln -sf /usr/local/bin/python2.7-config /usr/local/bin/python-config
    ln -sf /usr/local/bin/pydoc2.7  /usr/local/bin/pydoc
    ```

6. <span data-ttu-id="e1de1-126">versão mais recente de saudação do hello agente do Azure sempre pode ser encontrada no [Github](https://github.com/Azure/WALinuxAgent/releases).</span><span class="sxs-lookup"><span data-stu-id="e1de1-126">hello latest release of hello Azure agent can always be found on [Github](https://github.com/Azure/WALinuxAgent/releases).</span></span> <span data-ttu-id="e1de1-127">Instale o agente de saudação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="e1de1-127">Install hello agent as follows:</span></span>

    ```sh
    git clone https://github.com/Azure/WALinuxAgent 
    cd WALinuxAgent
    python setup.py install
    waagent -register-service
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="e1de1-128">Depois de instalar o agente do Azure, é tooverify uma boa ideia que ele está em execução da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="e1de1-128">After you install Azure Agent, it's a good idea tooverify that it's running as follows:</span></span>
    >
    > ```bash
    > ps auxw | grep waagent
    > root     79309  0.0  1.5  9184 15356 p1  S      4:11PM    0:00.46 python /usr/local/sbin/waagent -daemon (python2.7)
    > cat /var/log/waagent.log
    > ```

7. <span data-ttu-id="e1de1-129">Desprovisionamento Olá sistema tooclean-lo e disponibilizá-lo adequado para reprovisionamento.</span><span class="sxs-lookup"><span data-stu-id="e1de1-129">Deprovision hello system tooclean it and make it suitable for reprovisioning.</span></span> <span data-ttu-id="e1de1-130">Olá comando a seguir também exclui última conta de usuário provisionado hello e dados associado de saudação:</span><span class="sxs-lookup"><span data-stu-id="e1de1-130">hello following command also deletes hello last provisioned user account and hello associated data:</span></span>

    ```sh
    waagent -deprovision+user -force
    ```

<span data-ttu-id="e1de1-131">Agora você pode desligar sua VM.</span><span class="sxs-lookup"><span data-stu-id="e1de1-131">Now you can shut down your VM.</span></span>


## <a name="prepare-hello-vhd"></a><span data-ttu-id="e1de1-132">Preparar Olá VHD</span><span class="sxs-lookup"><span data-stu-id="e1de1-132">Prepare hello VHD</span></span>
<span data-ttu-id="e1de1-133">formato do Hello VHDX não tem suporte apenas no Azure, **VHD fixo**.</span><span class="sxs-lookup"><span data-stu-id="e1de1-133">hello VHDX format is not supported in Azure, only **fixed VHD**.</span></span> <span data-ttu-id="e1de1-134">Você pode converter o formato Olá disco toofixed VHD usando o Gerenciador do Hyper-V ou Olá Powershell [convert-vhd](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/convert-vhd) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e1de1-134">You can convert hello disk toofixed VHD format using Hyper-V Manager or hello Powershell [convert-vhd](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/convert-vhd) cmdlet.</span></span> <span data-ttu-id="e1de1-135">Um exemplo é como segue.</span><span class="sxs-lookup"><span data-stu-id="e1de1-135">An example is as following.</span></span>

```powershell
Convert-VHD OpenBSD61.vhdx OpenBSD61.vhd -VHDType Fixed
```

## <a name="create-storage-resources-and-upload"></a><span data-ttu-id="e1de1-136">Criar recursos de armazenamento e carregar</span><span class="sxs-lookup"><span data-stu-id="e1de1-136">Create storage resources and upload</span></span>
<span data-ttu-id="e1de1-137">Primeiro, crie um grupo de recursos com [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="e1de1-137">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="e1de1-138">Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *eastus* local:</span><span class="sxs-lookup"><span data-stu-id="e1de1-138">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="e1de1-139">tooupload seu VHD, crie uma conta de armazenamento com [criar conta de armazenamento az](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="e1de1-139">tooupload your VHD, create a storage account with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="e1de1-140">O nome da conta de armazenamento deve ser exclusivo; portanto, forneça seu próprio nome.</span><span class="sxs-lookup"><span data-stu-id="e1de1-140">Storage account names must be unique, so provide your own name.</span></span> <span data-ttu-id="e1de1-141">Olá, exemplo a seguir cria uma conta de armazenamento denominada *mystorageaccount*:</span><span class="sxs-lookup"><span data-stu-id="e1de1-141">hello following example creates a storage account named *mystorageaccount*:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup \
    --name mystorageaccount \
    --location eastus \
    --sku Premium_LRS
```

<span data-ttu-id="e1de1-142">toocontrol acessar a conta de armazenamento toohello, obtenha a chave de armazenamento de saudação com [lista de chaves de conta de armazenamento az](/cli/azure/storage/account/keys#list) da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="e1de1-142">toocontrol access toohello storage account, obtain hello storage key with [az storage account keys list](/cli/azure/storage/account/keys#list) as follows:</span></span>

```azurecli
STORAGE_KEY=$(az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount \
    --query "[?keyName=='key1']  | [0].value" -o tsv)
```

<span data-ttu-id="e1de1-143">toologically separado Olá VHDs carregar, criar um contêiner na conta de armazenamento Olá com [criar contêiner de armazenamento az](/cli/azure/storage/container#create):</span><span class="sxs-lookup"><span data-stu-id="e1de1-143">toologically separate hello VHDs you upload, create a container within hello storage account with [az storage container create](/cli/azure/storage/container#create):</span></span>

```azurecli
az storage container create \
    --name vhds \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```

<span data-ttu-id="e1de1-144">Por fim, carregue o VHD com [carregamento de blob de armazenamento az](/cli/azure/storage/blob#upload) da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="e1de1-144">Finally, upload your VHD with [az storage blob upload](/cli/azure/storage/blob#upload) as follows:</span></span>

```azurecli
az storage blob upload \
    --container-name vhds \
    --file ./OpenBSD61.vhd \
    --name OpenBSD61.vhd \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```


## <a name="create-vm-from-your-vhd"></a><span data-ttu-id="e1de1-145">Criar VM a partir de seu VHD</span><span class="sxs-lookup"><span data-stu-id="e1de1-145">Create VM from your VHD</span></span>
<span data-ttu-id="e1de1-146">Você pode criar uma VM com um [script de exemplo](../scripts/virtual-machines-linux-cli-sample-create-vm-vhd.md) ou diretamente com [criar vm az](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="e1de1-146">You can create a VM with a [sample script](../scripts/virtual-machines-linux-cli-sample-create-vm-vhd.md) or directly with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="e1de1-147">toospecify Olá OpenBSD VHD carregado, use Olá `--image` parâmetro da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="e1de1-147">toospecify hello OpenBSD VHD you uploaded, use hello `--image` parameter as follows:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myOpenBSD61 \
    --image "https://mystorageaccount.blob.core.windows.net/vhds/OpenBSD61.vhd" \
    --os-type linux \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

<span data-ttu-id="e1de1-148">Obter o endereço IP de saudação para sua VM OpenBSD com [az vm lista--endereços ip](/cli/azure/vm#list-ip-addresses) da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="e1de1-148">Obtain hello IP address for your OpenBSD VM with [az vm list-ip-addresses](/cli/azure/vm#list-ip-addresses) as follows:</span></span>

```azurecli
az vm list-ip-addresses --resource-group myResourceGroup --name myOpenBSD61
```

<span data-ttu-id="e1de1-149">Agora você pode SSH tooyour OpenBSD VM como normal:</span><span class="sxs-lookup"><span data-stu-id="e1de1-149">Now you can SSH tooyour OpenBSD VM as normal:</span></span>
        
```bash
ssh azureuser@<ip address>
```


## <a name="next-steps"></a><span data-ttu-id="e1de1-150">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e1de1-150">Next steps</span></span>
<span data-ttu-id="e1de1-151">Se você quiser tooknow suportam a mais sobre o Hyper-V em OpenBSD6.1, ler [OpenBSD 6.1](https://www.openbsd.org/61.html) e [hyperv.4](http://man.openbsd.org/hyperv.4).</span><span class="sxs-lookup"><span data-stu-id="e1de1-151">If you want tooknow more about Hyper-V support on OpenBSD6.1, read [OpenBSD 6.1](https://www.openbsd.org/61.html) and [hyperv.4](http://man.openbsd.org/hyperv.4).</span></span>

<span data-ttu-id="e1de1-152">Se você quiser toocreate uma VM de disco gerenciado, leia [disco az](/cli/azure/disk).</span><span class="sxs-lookup"><span data-stu-id="e1de1-152">If you want toocreate a VM from managed disk, read [az disk](/cli/azure/disk).</span></span> 
