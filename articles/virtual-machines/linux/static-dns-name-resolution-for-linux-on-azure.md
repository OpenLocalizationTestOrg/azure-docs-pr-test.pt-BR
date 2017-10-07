---
title: "aaaUse resolução com hello 2.0 do CLI do Azure de nome de DNS interno de VM | Microsoft Docs"
description: "Como a rede virtual toocreate placas de interface e usar interno do DNS para resolução de nome VM no Azure com hello 2.0 do CLI do Azure"
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
ms.devlang: azurecli
ms.topic: article
ms.date: 02/16/2017
ms.author: v-livech
ms.openlocfilehash: b3c4bfd3ab698f7b25d763ba9e60dd7984f6269d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-virtual-network-interface-cards-and-use-internal-dns-for-vm-name-resolution-on-azure"></a>Criar placas de adaptador de rede virtual e usar DNS interno para resolução de nome da VM no Azure
Este artigo mostra como tooset estático internos nomes DNS para VMs do Linux usando virtual rede placas de interface (vNics) e nomes de rótulo DNS com hello 2.0 do CLI do Azure. Você também pode executar essas etapas com hello [Azure CLI 1.0](static-dns-name-resolution-for-linux-on-azure-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Nomes DNS estáticos são usados para serviços de infraestrutura permanentes como um servidor de build Jenkins, que é usado para este documento ou um servidor Git.

requisitos de saudação são:

* [uma conta do Azure](https://azure.microsoft.com/pricing/free-trial/)
* [arquivos de chave SSH pública e privada](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a>Comandos rápidos
Se você precisar tooquickly realizar tarefa hello, Olá seção a seguir fornece detalhes sobre comandos Olá necessários. Obter mais informações e o contexto para cada etapa pode ser encontrada no restante de saudação do documento hello, [Iniciar aqui](#detailed-walkthrough). tooperform essas etapas, você precisa hello mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) instalado e conectado através de conta do Azure tooan [logon az](/cli/azure/#login).

Pré-requisitos: grupo de recursos, rede virtual e sub-rede, grupo de segurança de rede com o SSH de entrada.

### <a name="create-a-virtual-network-interface-card-with-a-static-internal-dns-name"></a>Criar uma placa de interface de rede virtual com um nome DNS interno estático
Criar hello vNic com [nic da rede az criar](/cli/azure/network/nic#create). Olá `--internal-dns-name` sinalizador CLI é para o rótulo DNS Olá de configuração, que fornece o nome DNS estático de saudação de placa de interface de rede virtual (vNic) de saudação. Olá, exemplo a seguir cria uma vNic denominada `myNic`, conecta toohello `myVnet` rede virtual e cria um registro de nome DNS interno chamado `jenkins`:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

### <a name="deploy-a-vm-and-connect-hello-vnic"></a>Implantar uma VM e conecte-se Olá vNic
Crie uma VM com [az vm create](/cli/azure/vm#create). Olá `--nics` sinalizador conecta Olá vNic toohello VM durante a saudação tooAzure de implantação. Olá, exemplo a seguir cria uma VM denominada `myVM` com discos gerenciado do Azure e anexa Olá vNic denominado `myNic` de saudação anterior etapa:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="detailed-walkthrough"></a>Passo a passo detalhado

Uma implantação contínua (CiCd) e integração contínua completo infra-estrutura no Azure exige que determinados servidores de servidores toobe vida longa ou estático. É recomendável que os ativos do Azure como Olá redes virtuais e grupos de segurança de rede são estáticos e vida útil longa recursos que raramente são implantados. Quando uma rede virtual tiver sido implantada, ele pode ser reutilizado por novas implantações sem nenhuma infraestrutura de toohello efeitos adversos. Mais tarde, você pode adicionar um servidor de repositório Git ou um servidor de automação Jenkins oferece a rede virtual do CiCd toothis para seus ambientes de desenvolvimento ou teste.  

Nomes DNS internos podem ser resolvidos apenas em uma rede virtual do Azure. Como os nomes DNS Olá são internos, eles não são toohello resolvível fora da internet, fornecendo a infra-estrutura de toohello de segurança adicional.

Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores. Os nomes de parâmetro de exemplo incluem `myResourceGroup`, `myNic` e `myVM`.

## <a name="create-hello-resource-group"></a>Criar grupo de recursos de saudação
Primeiro, crie o grupo de recursos de saudação com [criar grupo az](/cli/azure/group#create). Olá, exemplo a seguir cria um grupo de recursos denominado `myResourceGroup` em Olá `westus` local:

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-hello-virtual-network"></a>Criar rede virtual Olá

Olá próxima etapa é toobuild toolaunch uma rede virtual Olá VMs em. rede virtual Olá contém uma sub-rede para este passo a passo. Para obter mais informações sobre redes virtuais do Azure, consulte [criar uma rede virtual usando Olá CLI do Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

Criar rede virtual de saudação com [criar redes de rede az](/cli/azure/network/vnet#create). Olá, exemplo a seguir cria uma rede virtual denominada `myVnet` e sub-rede denominada `mySubnet`:

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

## <a name="create-hello-network-security-group"></a>Criar grupo de segurança de rede de saudação
Grupos de segurança de rede do Azure são equivalentes tooa firewall na camada de rede hello. Para obter mais informações sobre grupos de segurança de rede, consulte [como NSGs toocreate em Olá CLI do Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

Criar grupo de segurança de rede Olá com [criar az rede nsg](/cli/azure/network/nsg#create). Olá, exemplo a seguir cria um grupo de segurança de rede denominado `myNetworkSecurityGroup`:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-rule-tooallow-ssh"></a>Adicionar uma regra de entrada de tooallow SSH
Adicionar uma regra de entrada para o grupo de segurança de rede Olá com [criar regra de nsg rede az](/cli/azure/network/nsg/rule#create). Olá, exemplo a seguir cria uma regra denominada `myRuleAllowSSH`:

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myRuleAllowSSH \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --source-address-prefix '*' \
    --source-port-range '*' \
    --destination-address-prefix '*' \
    --destination-port-range 22 \
    --access allow
```

## <a name="associate-hello-subnet-with-hello-network-security-group"></a>Associar sub-redes Olá Olá grupo de segurança de rede
tooassociate sub-rede Olá Olá grupo de segurança de rede, use [atualização de sub-rede da rede virtual de rede az](/cli/azure/network/vnet/subnet#update). Hello, exemplo a seguir associa o nome de sub-rede Olá `mySubnet` com hello grupo de segurança de rede denominado `myNetworkSecurityGroup`:

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```


## <a name="create-hello-virtual-network-interface-card-and-static-dns-names"></a>Criar a placa de interface de rede virtual hello e nomes DNS estático
O Azure é muito flexível, mas toouse nomes DNS para resolução de nome VM, você precisa de placas de interface de rede virtual toocreate (vNics) que incluem um rótulo DNS. vNics são importantes para você pode reutilizá-los, conectando-os VMs toodifferent ciclo de vida de infraestrutura de saudação. Essa abordagem mantém Olá vNic como um recurso estático enquanto Olá VMs pode ser temporário. Usando o DNS rotulagem no vNic hello, estamos tooenable capaz de resolução de nome simples de outras VMs em redes de saudação. Usando nomes resolvível permite que outro servidor de automação VMs tooaccess Olá por nome DNS Olá `Jenkins` ou servidor de Git hello como `gitrepo`.  

Criar hello vNic com [nic da rede az criar](/cli/azure/network/nic#create). Olá, exemplo a seguir cria uma vNic denominada `myNic`, conecta toohello `myVnet` rede virtual denominado `myVnet`e cria um registro de nome DNS interno chamado `jenkins`:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

## <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a>Implantar Olá VM na infraestrutura de rede virtual Olá
Agora temos uma rede virtual e sub-rede, um grupo de segurança de rede atuando como um firewall tooprotect nosso sub-rede bloqueando todo o tráfego de entrada exceto porta 22 para SSH e uma vNic. Agora a VM pode ser implantada nessa infraestrutura de rede existente.

Crie uma VM com [az vm create](/cli/azure/vm#create). Olá, exemplo a seguir cria uma VM denominada `myVM` com discos gerenciado do Azure e anexa Olá vNic denominado `myNic` de saudação anterior etapa:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

Usando Olá CLI sinalizadores de toocall recursos existentes, podemos instruir Olá toodeploy Azure VM dentro da rede existente hello. tooreiterate, depois que uma rede virtual e a sub-rede forem implantados, eles podem ser mantidos como estáticos ou permanentes de recursos dentro de sua região do Azure.  

## <a name="next-steps"></a>Próximas etapas
* [Criar seu próprio ambiente personalizado para uma VM do Linux usando os comandos da CLI do Azure diretamente](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Criar uma VM do Linux no Azure usando modelos](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
