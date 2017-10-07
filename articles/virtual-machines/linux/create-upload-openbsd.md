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
# <a name="create-and-upload-an-openbsd-disk-image-tooazure"></a>Criar e carregar um tooAzure de imagem de disco OpenBSD
Este artigo mostra como toocreate e carregar um disco rígido virtual (VHD) que contém Olá OpenBSD sistema de operacional. Depois que você carregá-lo, você pode usá-lo como toocreate sua própria imagem uma máquina virtual (VM) no Azure por meio da CLI do Azure.


## <a name="prerequisites"></a>Pré-requisitos
Este artigo pressupõe que você tenha Olá itens a seguir:

* **Uma assinatura do Azure** - Se não tiver uma conta, você poderá criar uma em apenas alguns minutos. Se você tiver uma assinatura do MSDN, confira [Crédito Azure mensal para assinantes do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/). Caso contrário, saiba como muito[criar uma conta de avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).  
* **2.0 do CLI do Azure** -Verifique se você tem hello mais recente [2.0 do CLI do Azure](/cli/azure/install-azure-cli) instalado e registrado no tooyour conta do Azure com [logon az](/cli/azure/#login).
* **Sistema de operacional OpenBSD instalado em um arquivo. vhd** -um sistema de operacional OpenBSD (6.1 versão) deve ser instalado tooa do disco rígido virtual. Várias ferramentas existem toocreate arquivos. vhd. Por exemplo, você pode usar uma solução de virtualização, como o arquivo. vhd do Hyper-V toocreate hello e instalar o sistema operacional de saudação. Para obter instruções sobre como tooinstall e use o Hyper-V, consulte [instalar o Hyper-V e criar uma máquina virtual](http://technet.microsoft.com/library/hh846766.aspx).


## <a name="prepare-openbsd-image-for-azure"></a>Preparar imagem OpenBSD do Azure
No hello VM onde você instalou o sistema de operacional Olá OpenBSD 6.1, que adicionou suporte de Hyper-V, conclua Olá procedimentos a seguir:

1. Se DHCP não está habilitado durante a instalação, habilite o serviço de saudação da seguinte maneira:

    ```sh    
    echo dhcp > /etc/hostname.hvn0
    ```

2. Instalar um console serial da seguinte maneira:

    ```sh
    echo "stty com0 115200" >> /etc/boot.conf
    echo "set tty com0" >> /etc/boot.conf
    ```

3. Configure a instalação do pacote da seguinte maneira:

    ```sh
    echo "https://ftp.openbsd.org/pub/OpenBSD" > /etc/installurl
    ```
   
4. Por padrão, Olá `root` usuário está desabilitado em máquinas virtuais no Azure. Os usuários podem executar comandos com privilégios elevados usando Olá `doas` comando OpenBSD VM. Doas é habilitado por padrão. Para obter mais informações, consulte [doas.conf](http://man.openbsd.org/doas.conf.5). 

5. Instalar e configurar os pré-requisitos para hello Azure agente da seguinte maneira:

    ```sh
    pkg_add py-setuptools openssl git
    ln -sf /usr/local/bin/python2.7 /usr/local/bin/python
    ln -sf /usr/local/bin/python2.7-2to3 /usr/local/bin/2to3
    ln -sf /usr/local/bin/python2.7-config /usr/local/bin/python-config
    ln -sf /usr/local/bin/pydoc2.7  /usr/local/bin/pydoc
    ```

6. versão mais recente de saudação do hello agente do Azure sempre pode ser encontrada no [Github](https://github.com/Azure/WALinuxAgent/releases). Instale o agente de saudação da seguinte maneira:

    ```sh
    git clone https://github.com/Azure/WALinuxAgent 
    cd WALinuxAgent
    python setup.py install
    waagent -register-service
    ```

    > [!IMPORTANT]
    > Depois de instalar o agente do Azure, é tooverify uma boa ideia que ele está em execução da seguinte maneira:
    >
    > ```bash
    > ps auxw | grep waagent
    > root     79309  0.0  1.5  9184 15356 p1  S      4:11PM    0:00.46 python /usr/local/sbin/waagent -daemon (python2.7)
    > cat /var/log/waagent.log
    > ```

7. Desprovisionamento Olá sistema tooclean-lo e disponibilizá-lo adequado para reprovisionamento. Olá comando a seguir também exclui última conta de usuário provisionado hello e dados associado de saudação:

    ```sh
    waagent -deprovision+user -force
    ```

Agora você pode desligar sua VM.


## <a name="prepare-hello-vhd"></a>Preparar Olá VHD
formato do Hello VHDX não tem suporte apenas no Azure, **VHD fixo**. Você pode converter o formato Olá disco toofixed VHD usando o Gerenciador do Hyper-V ou Olá Powershell [convert-vhd](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/convert-vhd) cmdlet. Um exemplo é como segue.

```powershell
Convert-VHD OpenBSD61.vhdx OpenBSD61.vhd -VHDType Fixed
```

## <a name="create-storage-resources-and-upload"></a>Criar recursos de armazenamento e carregar
Primeiro, crie um grupo de recursos com [az group create](/cli/azure/group#create). Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *eastus* local:

```azurecli
az group create --name myResourceGroup --location eastus
```

tooupload seu VHD, crie uma conta de armazenamento com [criar conta de armazenamento az](/cli/azure/storage/account#create). O nome da conta de armazenamento deve ser exclusivo; portanto, forneça seu próprio nome. Olá, exemplo a seguir cria uma conta de armazenamento denominada *mystorageaccount*:

```azurecli
az storage account create --resource-group myResourceGroup \
    --name mystorageaccount \
    --location eastus \
    --sku Premium_LRS
```

toocontrol acessar a conta de armazenamento toohello, obtenha a chave de armazenamento de saudação com [lista de chaves de conta de armazenamento az](/cli/azure/storage/account/keys#list) da seguinte maneira:

```azurecli
STORAGE_KEY=$(az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount \
    --query "[?keyName=='key1']  | [0].value" -o tsv)
```

toologically separado Olá VHDs carregar, criar um contêiner na conta de armazenamento Olá com [criar contêiner de armazenamento az](/cli/azure/storage/container#create):

```azurecli
az storage container create \
    --name vhds \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```

Por fim, carregue o VHD com [carregamento de blob de armazenamento az](/cli/azure/storage/blob#upload) da seguinte maneira:

```azurecli
az storage blob upload \
    --container-name vhds \
    --file ./OpenBSD61.vhd \
    --name OpenBSD61.vhd \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```


## <a name="create-vm-from-your-vhd"></a>Criar VM a partir de seu VHD
Você pode criar uma VM com um [script de exemplo](../scripts/virtual-machines-linux-cli-sample-create-vm-vhd.md) ou diretamente com [criar vm az](/cli/azure/vm#create). toospecify Olá OpenBSD VHD carregado, use Olá `--image` parâmetro da seguinte maneira:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myOpenBSD61 \
    --image "https://mystorageaccount.blob.core.windows.net/vhds/OpenBSD61.vhd" \
    --os-type linux \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

Obter o endereço IP de saudação para sua VM OpenBSD com [az vm lista--endereços ip](/cli/azure/vm#list-ip-addresses) da seguinte maneira:

```azurecli
az vm list-ip-addresses --resource-group myResourceGroup --name myOpenBSD61
```

Agora você pode SSH tooyour OpenBSD VM como normal:
        
```bash
ssh azureuser@<ip address>
```


## <a name="next-steps"></a>Próximas etapas
Se você quiser tooknow suportam a mais sobre o Hyper-V em OpenBSD6.1, ler [OpenBSD 6.1](https://www.openbsd.org/61.html) e [hyperv.4](http://man.openbsd.org/hyperv.4).

Se você quiser toocreate uma VM de disco gerenciado, leia [disco az](/cli/azure/disk). 
