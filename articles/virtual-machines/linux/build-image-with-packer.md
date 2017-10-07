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
# <a name="how-toouse-packer-toocreate-linux-virtual-machine-images-in-azure"></a>Como as imagens de máquina virtual do toouse Packer toocreate Linux no Azure
Cada máquina virtual (VM) no Azure é criada a partir de uma imagem que define hello distribuição Linux e a versão do sistema operacional. As imagens podem incluir configurações e aplicativos pré-instalados. Hello Azure Marketplace fornece muitas imagens primeira e terceiro para distribuições mais comuns e ambientes de aplicativo, ou você pode criar suas próprias necessidades de tooyour personalizadas de imagens personalizadas. Este artigo detalha como toouse Olá abrir a ferramenta de origem [Packer](https://www.packer.io/) toodefine e criar imagens personalizadas no Azure.


## <a name="create-azure-resource-group"></a>Criar um grupo de recursos do Azure
Durante o processo de compilação hello, Packer cria temporários recursos do Azure, ele cria a VM de origem hello. toocapture que a VM de origem para uso como uma imagem, você deve definir um grupo de recursos. Hello saída do processo de compilação Packer Olá é armazenada no grupo de recursos.

Crie um grupo de recursos com [az group create](/cli/azure/group#create). Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *eastus* local:

```azurecli
az group create -n myResourceGroup -l eastus
```


## <a name="create-azure-credentials"></a>Criar as credenciais do Azure
O Packer se autentica no Azure usando uma entidade de serviço. Uma entidade de serviço do Azure é uma identidade de segurança que você pode usar com aplicativos, serviços e ferramentas de automação como o Packer. Controlar e definir permissões de saudação como entidade de serviço toowhat operações Olá pode executar no Azure.

Criar um serviço principal com [az ad sp criar-para-rbac](/cli/azure/ad/sp#create-for-rbac) e as credenciais de saudação de saída que Packer precisa:

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

Um exemplo da saída de hello de saudação anterior comandos é o seguinte:

```azurecli
"f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
"0e760437-bf34-4aad-9f8d-870be799c55d",
"72f988bf-86f1-41af-91ab-2d7cd011db47"
```

tooauthenticate tooAzure, você também precisa tooobtain ID de sua assinatura do Azure com [Mostrar de conta az](/cli/azure/account#show):

```azurecli
az account show --query [id] --output tsv
```

Use saída Olá desses dois comandos na próxima etapa de saudação.


## <a name="define-packer-template"></a>Definir modelo do Packer
toobuild imagens, criar um modelo como um arquivo JSON. No modelo de hello, definir construtores e provisioners realizarem Olá real do processo de compilação. Packer tem um [provedor do Azure](https://www.packer.io/docs/builders/azure.html) que permite a você toodefine Azure recursos, como credenciais do serviço principal do hello criados no hello anterior da etapa.

Crie um arquivo chamado *ubuntu.json* e colar Olá conteúdo a seguir. Insira seus próprios valores para os seguintes hello:

| Parâmetro                           | Onde tooobtain |
|-------------------------------------|----------------------------------------------------|
| *client_id*                         | Primeira linha da saída do comando create `az ad sp` – *appId* |
| *client_secret*                     | Segunda linha da saída do comando create `az ad sp` – *password* |
| *tenant_id*                         | Terceira linha da saída do comando create `az ad sp` – *tenant* |
| *subscription_id*                   | Saída do comando `az account show` |
| *managed_image_resource_group_name* | Nome do grupo de recursos que você criou na etapa primeiro Olá |
| *managed_image_name*                | Nome de imagem de disco gerenciado Olá criado |


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

Este modelo cria uma imagem Ubuntu 16.04 LTS, instala NGINX e deprovisions Olá VM.

> [!NOTE]
> Se você expandir este credenciais do usuário do modelo tooprovision, ajustar o comando de provedor Olá deprovisions Olá tooread do agente do Azure `-deprovision` em vez de `deprovision+user`.
> Olá `+user` sinalizador remove todas as contas de usuário da VM de origem hello.


## <a name="build-packer-image"></a>Criar uma imagem do Packer
Se ainda não tiver instalado em seu computador local, de Packer [siga as instruções de instalação do hello Packer](https://www.packer.io/docs/install/index.html).

Crie imagem Olá especificando seu Packer arquivo de modelo da seguinte maneira:

```bash
./packer build ubuntu.json
```

Um exemplo da saída de hello de saudação anterior comandos é o seguinte:

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


## <a name="create-vm-from-azure-image"></a>Criar uma VM com base em uma Imagem do Azure
Agora você pode criar uma VM com base na Imagem com [az vm create](/cli/azure/vm#create). Especificar Olá imagem criado com hello `--image` parâmetro. Olá, exemplo a seguir cria uma VM denominada *myVM* de *myPackerImage* e gera as chaves de SSH se eles ainda não existir:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image myPackerImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

Ele usa Olá toocreate de alguns minutos VM. Quando Olá VM tiver sido criado, tome nota da saudação `publicIpAddress` exibido pelo Olá CLI do Azure. Esse endereço é o site NGINX Olá tooaccess usado por meio de um navegador da web.

tooallow web tooreach tráfego sua VM, abra a porta 80 da saudação da Internet com [az vm abrir portas](/cli/azure/vm#open-port):

```azurecli
az vm open-port \
    --resource-group myResourceGroup \
    --name myVM \
    --port 80
```

## <a name="test-vm-and-nginx"></a>Testar a VM e o NGINX
Agora você pode abrir um navegador da web e digite `http://publicIpAddress` na barra de endereços de saudação. Fornecer seu próprio público endereço IP da saudação VM criar processo. página NGINX saudação padrão é exibida como Olá exemplo a seguir:

![Site padrão NGINX](./media/build-image-with-packer/nginx.png) 


## <a name="next-steps"></a>Próximas etapas
Neste exemplo, você usou Packer toocreate uma imagem de VM com NGINX já instalado. Você pode usar esta imagem VM junto com a implantação fluxos de trabalho existentes, como toodeploy tooVMs seu aplicativo criado a partir de saudação imagem com Ansible, Chef ou Puppet.

Para obter outros modelos de exemplo do Packer para outras distribuições do Linux, consulte [este repositório GitHub](https://github.com/hashicorp/packer/tree/master/examples/azure).