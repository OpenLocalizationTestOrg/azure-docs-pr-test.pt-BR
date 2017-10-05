---
title: Criar e carregar uma imagem de VM OpenBSD no Azure | Microsoft Docs
description: "Saiba como criar e carregar um disco rígido virtual (VHD) que contenha um sistema operacional OpenBSD para criar uma máquina virtual do Azure por meio da CLI do Azure"
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
ms.openlocfilehash: 716c07f6a738189d6cf2b3caafa16b753927d182
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="create-and-upload-an-openbsd-disk-image-to-azure"></a><span data-ttu-id="0c685-103">Criar e carregar uma imagem de disco OpenBSD no Azure</span><span class="sxs-lookup"><span data-stu-id="0c685-103">Create and Upload an OpenBSD disk image to Azure</span></span>
<span data-ttu-id="0c685-104">Este artigo mostra como criar e carregar um disco rígido virtual (VHD) que contém o sistema operacional OpenBSD.</span><span class="sxs-lookup"><span data-stu-id="0c685-104">This article shows you how to create and upload a virtual hard disk (VHD) that contains the OpenBSD operating system.</span></span> <span data-ttu-id="0c685-105">Depois de carregá-lo, você pode usá-lo como sua própria imagem para criar uma máquina virtual (VM) no Azure por meio da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="0c685-105">After you upload it, you can use it as your own image to create a virtual machine (VM) in Azure through Azure CLI.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="0c685-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0c685-106">Prerequisites</span></span>
<span data-ttu-id="0c685-107">Este artigo pressupõe que você tenha os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="0c685-107">This article assumes that you have the following items:</span></span>

* <span data-ttu-id="0c685-108">**Uma assinatura do Azure** - Se não tiver uma conta, você poderá criar uma em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="0c685-108">**An Azure subscription** - If you don't have an account, you can create one in just a couple of minutes.</span></span> <span data-ttu-id="0c685-109">Se você tiver uma assinatura do MSDN, confira [Crédito Azure mensal para assinantes do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="0c685-109">If you have an MSDN subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="0c685-110">Caso contrário, saiba como [criar uma conta de avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0c685-110">Otherwise, learn how to [create a free trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span>  
* <span data-ttu-id="0c685-111">**CLI 2.0 do Azure** - Certifique-se de que você tenha instalado a versão mais recente da [CLI 2.0 do Azure](/cli/azure/install-azure-cli) e entrado em uma conta do Azure usando [login az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="0c685-111">**Azure CLI 2.0** - Make sure you have the latest [Azure CLI 2.0](/cli/azure/install-azure-cli) installed and logged in to your Azure account with [az login](/cli/azure/#login).</span></span>
* <span data-ttu-id="0c685-112">**Sistema operacional OpenBSD instalado em um arquivo .vhd** - É necessário instalar um sistema operacional OpenBSD (versão 6.1) com suporte em um disco rígido virtual.</span><span class="sxs-lookup"><span data-stu-id="0c685-112">**OpenBSD operating system installed in a .vhd file** - A supported OpenBSD operating system (6.1 version) must be installed to a virtual hard disk.</span></span> <span data-ttu-id="0c685-113">Existem várias ferramentas para criar arquivos .vhd.</span><span class="sxs-lookup"><span data-stu-id="0c685-113">Multiple tools exist to create .vhd files.</span></span> <span data-ttu-id="0c685-114">Por exemplo, você pode usar uma solução de virtualização, como o Hyper-V, para criar o arquivo .vhd e instalar o sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="0c685-114">For example, you can use a virtualization solution such as Hyper-V to create the .vhd file and install the operating system.</span></span> <span data-ttu-id="0c685-115">Para obter instruções sobre como instalar e usar o Hyper-V, confira [Instalar o Hyper-V e criar uma máquina virtual](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="0c685-115">For instructions about how to install and use Hyper-V, see [Install Hyper-V and create a virtual machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>


## <a name="prepare-openbsd-image-for-azure"></a><span data-ttu-id="0c685-116">Preparar imagem OpenBSD do Azure</span><span class="sxs-lookup"><span data-stu-id="0c685-116">Prepare OpenBSD image for Azure</span></span>
<span data-ttu-id="0c685-117">Na VM em que você instalou o sistema de operacional OpenBSD 6.1, que adicionou suporte Hyper-V, conclua os procedimentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="0c685-117">On the VM where you installed the OpenBSD operating system 6.1, which added Hyper-V support, complete the following procedures:</span></span>

1. <span data-ttu-id="0c685-118">Se DHCP não está habilitado durante a instalação, habilite o serviço da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="0c685-118">If DHCP is not enabled during installation, enable the service as follows:</span></span>

    ```sh    
    echo dhcp > /etc/hostname.hvn0
    ```

2. <span data-ttu-id="0c685-119">Instalar um console serial da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="0c685-119">Set up a serial console as follows:</span></span>

    ```sh
    echo "stty com0 115200" >> /etc/boot.conf
    echo "set tty com0" >> /etc/boot.conf
    ```

3. <span data-ttu-id="0c685-120">Configure a instalação do pacote da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="0c685-120">Configure Package installation as follows:</span></span>

    ```sh
    echo "https://ftp.openbsd.org/pub/OpenBSD" > /etc/installurl
    ```
   
4. <span data-ttu-id="0c685-121">Por padrão, o usuário `root` encontra-se desabilitado nas máquinas virtuais no Azure.</span><span class="sxs-lookup"><span data-stu-id="0c685-121">By default, the `root` user is disabled on virtual machines in Azure.</span></span> <span data-ttu-id="0c685-122">Os usuários podem executar comandos com privilégios elevados usando o comando `doas` na VM OpenBSD.</span><span class="sxs-lookup"><span data-stu-id="0c685-122">Users can run commands with elevated privileges by using the `doas` command on OpenBSD VM.</span></span> <span data-ttu-id="0c685-123">Doas é habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="0c685-123">Doas is enabled by default.</span></span> <span data-ttu-id="0c685-124">Para obter mais informações, consulte [doas.conf](http://man.openbsd.org/doas.conf.5).</span><span class="sxs-lookup"><span data-stu-id="0c685-124">For more information, see [doas.conf](http://man.openbsd.org/doas.conf.5).</span></span> 

5. <span data-ttu-id="0c685-125">Instalar e configurar os pré-requisitos para o agente do Azure da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="0c685-125">Install and configure prerequisites for the Azure Agent as follows:</span></span>

    ```sh
    pkg_add py-setuptools openssl git
    ln -sf /usr/local/bin/python2.7 /usr/local/bin/python
    ln -sf /usr/local/bin/python2.7-2to3 /usr/local/bin/2to3
    ln -sf /usr/local/bin/python2.7-config /usr/local/bin/python-config
    ln -sf /usr/local/bin/pydoc2.7  /usr/local/bin/pydoc
    ```

6. <span data-ttu-id="0c685-126">A versão mais recente do agente do Azure sempre pode ser encontrada no [Github](https://github.com/Azure/WALinuxAgent/releases).</span><span class="sxs-lookup"><span data-stu-id="0c685-126">The latest release of the Azure agent can always be found on [Github](https://github.com/Azure/WALinuxAgent/releases).</span></span> <span data-ttu-id="0c685-127">Instale o agente da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="0c685-127">Install the agent as follows:</span></span>

    ```sh
    git clone https://github.com/Azure/WALinuxAgent 
    cd WALinuxAgent
    python setup.py install
    waagent -register-service
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="0c685-128">Depois de instalar o agente do Azure, convém verificar se ele está em execução da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="0c685-128">After you install Azure Agent, it's a good idea to verify that it's running as follows:</span></span>
    >
    > ```bash
    > ps auxw | grep waagent
    > root     79309  0.0  1.5  9184 15356 p1  S      4:11PM    0:00.46 python /usr/local/sbin/waagent -daemon (python2.7)
    > cat /var/log/waagent.log
    > ```

7. <span data-ttu-id="0c685-129">Desprovisione o sistema para limpá-lo e torná-lo adequado para o reprovisionamento.</span><span class="sxs-lookup"><span data-stu-id="0c685-129">Deprovision the system to clean it and make it suitable for reprovisioning.</span></span> <span data-ttu-id="0c685-130">O comando a seguir também exclui a última conta de usuário provisionada e os dados associados:</span><span class="sxs-lookup"><span data-stu-id="0c685-130">The following command also deletes the last provisioned user account and the associated data:</span></span>

    ```sh
    waagent -deprovision+user -force
    ```

<span data-ttu-id="0c685-131">Agora você pode desligar sua VM.</span><span class="sxs-lookup"><span data-stu-id="0c685-131">Now you can shut down your VM.</span></span>


## <a name="prepare-the-vhd"></a><span data-ttu-id="0c685-132">Preparar o VHD</span><span class="sxs-lookup"><span data-stu-id="0c685-132">Prepare the VHD</span></span>
<span data-ttu-id="0c685-133">O formato VHDX não tem suporte no Azure, somente o **VHD fixo**.</span><span class="sxs-lookup"><span data-stu-id="0c685-133">The VHDX format is not supported in Azure, only **fixed VHD**.</span></span> <span data-ttu-id="0c685-134">Você pode converter o disco no formato VHD fixo usando o Gerenciador do Hyper-V ou o cmdlet [convert-vhd](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/convert-vhd) do Powershell.</span><span class="sxs-lookup"><span data-stu-id="0c685-134">You can convert the disk to fixed VHD format using Hyper-V Manager or the Powershell [convert-vhd](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/convert-vhd) cmdlet.</span></span> <span data-ttu-id="0c685-135">Um exemplo é como segue.</span><span class="sxs-lookup"><span data-stu-id="0c685-135">An example is as following.</span></span>

```powershell
Convert-VHD OpenBSD61.vhdx OpenBSD61.vhd -VHDType Fixed
```

## <a name="create-storage-resources-and-upload"></a><span data-ttu-id="0c685-136">Criar recursos de armazenamento e carregar</span><span class="sxs-lookup"><span data-stu-id="0c685-136">Create storage resources and upload</span></span>
<span data-ttu-id="0c685-137">Primeiro, crie um grupo de recursos com [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="0c685-137">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="0c685-138">O exemplo a seguir cria um grupo de recursos chamado *myResourceGroup* na localização *eastus*:</span><span class="sxs-lookup"><span data-stu-id="0c685-138">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="0c685-139">Para carregar seu VHD, crie uma conta de armazenamento com [criar conta de armazenamento az](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="0c685-139">To upload your VHD, create a storage account with [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="0c685-140">O nome da conta de armazenamento deve ser exclusivo; portanto, forneça seu próprio nome.</span><span class="sxs-lookup"><span data-stu-id="0c685-140">Storage account names must be unique, so provide your own name.</span></span> <span data-ttu-id="0c685-141">O exemplo a seguir cria uma conta de armazenamento chamada *mystorageaccount*:</span><span class="sxs-lookup"><span data-stu-id="0c685-141">The following example creates a storage account named *mystorageaccount*:</span></span>

```azurecli
az storage account create --resource-group myResourceGroup \
    --name mystorageaccount \
    --location eastus \
    --sku Premium_LRS
```

<span data-ttu-id="0c685-142">Para controlar o acesso à conta de armazenamento, obter a chave de armazenamento com [az storage account keys list](/cli/azure/storage/account/keys#list) da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="0c685-142">To control access to the storage account, obtain the storage key with [az storage account keys list](/cli/azure/storage/account/keys#list) as follows:</span></span>

```azurecli
STORAGE_KEY=$(az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount \
    --query "[?keyName=='key1']  | [0].value" -o tsv)
```

<span data-ttu-id="0c685-143">Para separar logicamente os VHDs que você carregue, crie um contêiner dentro da conta de armazenamento com [criar contêiner de armazenamento az](/cli/azure/storage/container#create):</span><span class="sxs-lookup"><span data-stu-id="0c685-143">To logically separate the VHDs you upload, create a container within the storage account with [az storage container create](/cli/azure/storage/container#create):</span></span>

```azurecli
az storage container create \
    --name vhds \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```

<span data-ttu-id="0c685-144">Por fim, carregue o VHD com [carregamento de blob de armazenamento az](/cli/azure/storage/blob#upload) da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="0c685-144">Finally, upload your VHD with [az storage blob upload](/cli/azure/storage/blob#upload) as follows:</span></span>

```azurecli
az storage blob upload \
    --container-name vhds \
    --file ./OpenBSD61.vhd \
    --name OpenBSD61.vhd \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```


## <a name="create-vm-from-your-vhd"></a><span data-ttu-id="0c685-145">Criar VM a partir de seu VHD</span><span class="sxs-lookup"><span data-stu-id="0c685-145">Create VM from your VHD</span></span>
<span data-ttu-id="0c685-146">Você pode criar uma VM com um [script de exemplo](../scripts/virtual-machines-linux-cli-sample-create-vm-vhd.md) ou diretamente com [criar vm az](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="0c685-146">You can create a VM with a [sample script](../scripts/virtual-machines-linux-cli-sample-create-vm-vhd.md) or directly with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="0c685-147">Para especificar o VHD OpenBSD carregado, use o parâmetro `--image` da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="0c685-147">To specify the OpenBSD VHD you uploaded, use the `--image` parameter as follows:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myOpenBSD61 \
    --image "https://mystorageaccount.blob.core.windows.net/vhds/OpenBSD61.vhd" \
    --os-type linux \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

<span data-ttu-id="0c685-148">Obter o endereço IP para sua VM OpenBSD com [az vm lista--endereços ip](/cli/azure/vm#list-ip-addresses) da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="0c685-148">Obtain the IP address for your OpenBSD VM with [az vm list-ip-addresses](/cli/azure/vm#list-ip-addresses) as follows:</span></span>

```azurecli
az vm list-ip-addresses --resource-group myResourceGroup --name myOpenBSD61
```

<span data-ttu-id="0c685-149">Agora você pode SSH para sua VM OpenBSD normal:</span><span class="sxs-lookup"><span data-stu-id="0c685-149">Now you can SSH to your OpenBSD VM as normal:</span></span>
        
```bash
ssh azureuser@<ip address>
```


## <a name="next-steps"></a><span data-ttu-id="0c685-150">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0c685-150">Next steps</span></span>
<span data-ttu-id="0c685-151">Se você quiser saber mais sobre o suporte de Hyper-V em OpenBSD6.1, leia [OpenBSD 6.1](https://www.openbsd.org/61.html) e [hyperv.4](http://man.openbsd.org/hyperv.4).</span><span class="sxs-lookup"><span data-stu-id="0c685-151">If you want to know more about Hyper-V support on OpenBSD6.1, read [OpenBSD 6.1](https://www.openbsd.org/61.html) and [hyperv.4](http://man.openbsd.org/hyperv.4).</span></span>

<span data-ttu-id="0c685-152">Se você quiser criar uma VM de disco gerenciado, leia [disco az](/cli/azure/disk).</span><span class="sxs-lookup"><span data-stu-id="0c685-152">If you want to create a VM from managed disk, read [az disk](/cli/azure/disk).</span></span> 