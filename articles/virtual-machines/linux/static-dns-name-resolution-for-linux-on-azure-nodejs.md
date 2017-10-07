---
title: "aaaUsing resolução no Azure de nome de DNS interno de VM | Microsoft Docs"
description: "Usando o DNS interno para a resolução de nomes da VM no Azure."
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
ms.date: 12/05/2016
ms.author: v-livech
ms.openlocfilehash: 94fd6577aa51ce5db4dc26649b415ddeeb410eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-internal-dns-for-vm-name-resolution-on-azure"></a>Usando o DNS interno para a resolução de nomes da VM no Azure

Este artigo mostra como tooset estático interno nomes DNS para VMs do Linux usando cartões de NIC Virtual (VNic) e nomes de rótulo DNS. Nomes DNS estáticos são usados para serviços de infraestrutura permanentes como um servidor de build Jenkins, que é usado para este documento ou um servidor Git.

requisitos de saudação são:

* [uma conta do Azure](https://azure.microsoft.com/pricing/free-trial/)
* [arquivos de chave SSH pública e privada](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


## <a name="cli-versions-toocomplete-hello-task"></a>Tarefa de saudação do CLI versões toocomplete
Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:

- [1.0 de CLI do Azure](#quick-commands) – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)
- [2.0 do CLI do Azure](static-dns-name-resolution-for-linux-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação


## <a name="quick-commands"></a>Comandos rápidos

Se você precisar tooquickly realizar tarefa hello, Olá seção a seguir fornece detalhes sobre comandos Olá necessários. Obter mais informações e o contexto para cada etapa pode ser encontrada restante de saudação do documento hello, [Iniciar aqui](#detailed-walkthrough).  

Pré-requisitos: Grupo de Recursos, VNet, NSG com SSH de entrada e Sub-rede.

### <a name="create-a-vnic-with-a-static-internal-dns-name"></a>Criar uma VNic com um nome DNS interno estático

Olá `-r` cli sinalizador é para o rótulo DNS Olá de configuração, que fornece o nome DNS estático Olá para Olá VNic.

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

### <a name="deploy-hello-vm-into-hello-vnet-nsg-and-connect-hello-vnic"></a>Implantar Olá VM em Olá VNet, NSG e conectar Olá VNic

Olá `-N` conecta Olá VNic toohello nova máquina virtual durante a saudação tooAzure de implantação.

```azurecli
azure vm create jenkins \
-g myResourceGroup \
-l westus \
-y linux \
-Q Debian \
-o myStorageAcct \
-u myAdminUser \
-M ~/.ssh/id_rsa.pub \
-F myVNet \
-j mySubnet \
-N jenkinsVNic
```

## <a name="detailed-walkthrough"></a>Passo a passo detalhado

Uma implantação contínua (CiCd) e integração contínua completo infra-estrutura no Azure exige que determinados servidores de servidores toobe vida longa ou estático.  É recomendável que os ativos do Azure como saudação de redes virtuais (VNets) e grupos de segurança de rede (NSGs), deve ser estáticos e vida útil longa recursos que raramente são implantados.  Quando uma rede virtual tiver sido implantada, ele pode ser reutilizado por novas implantações sem nenhuma infraestrutura de toohello efeitos adversos.  Adicionando rede estática de toothis um Git servidor do repositório e um servidor de automação Jenkins oferece CiCd tooyour ambientes de desenvolvimento ou teste.  

Nomes DNS internos podem ser resolvidos apenas em uma rede virtual do Azure.  Como os nomes DNS Olá são internos, eles não são toohello resolvível fora da internet, fornecendo a infra-estrutura de toohello de segurança adicional.

_Substitua os exemplos por sua própria nomenclatura._

## <a name="create-hello-resource-group"></a>Criar grupo de recursos de saudação

Um grupo de recursos é necessário tooorganize tudo o que podemos criar neste passo a passo.  Para obter mais informações sobre os Grupos de Recursos do Azure, consulte [Visão geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

```azurecli
azure group create myResourceGroup \
--location westus
```

## <a name="create-hello-vnet"></a>Criar hello VNet

Olá primeira etapa é toobuild toolaunch uma rede virtual Olá VMs em.  Olá VNet contém uma sub-rede para este passo a passo.  Para obter mais informações sobre VNets do Azure, consulte [criar uma rede virtual usando Olá CLI do Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

```azurecli
azure network vnet create myVNet \
--resource-group myResourceGroup \
--address-prefixes 10.10.0.0/24 \
--location westus
```

## <a name="create-hello-nsg"></a>Criar hello NSG

Olá sub-rede é criado por trás de um grupo de segurança de rede existente, de forma que criamos Olá NSG antes Olá sub-rede.  Os NSGs do Azure são equivalentes tooa firewall na camada de rede de saudação.  Para obter mais informações sobre os NSGs do Azure, consulte [como NSGs toocreate em Olá CLI do Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

```azurecli
azure network nsg create myNSG \
--resource-group myResourceGroup \
--location westus
```

## <a name="add-an-inbound-ssh-allow-rule"></a>Adicionar uma regra de permissão de SSH de entrada

Olá VM Linux precisa ter acesso de saudação à internet para que uma regra que permite a porta de entrada 22 tráfego toobe passado Olá rede tooport 22 na Olá VM do Linux é necessária.

```azurecli
azure network nsg rule create inboundSSH \
--resource-group myResourceGroup \
--nsg-name myNSG \
--access Allow \
--protocol Tcp \
--direction Inbound \
--priority 100 \
--source-address-prefix * \
--source-port-range * \
--destination-address-prefix 10.10.0.0/24 \
--destination-port-range 22
```

## <a name="add-a-subnet-toohello-vnet"></a>Adicionar toohello uma sub-rede VNet

VMs em redes de saudação devem estar localizadas em uma sub-rede.  Cada VNET pode ter várias sub-redes.  Criar uma sub-rede hello e associar sub-redes Olá Olá NSG tooadd uma sub-rede de toohello do firewall.

```azurecli
azure network vnet subnet create mySubNet \
--resource-group myResourceGroup \
--vnet-name myVNet \
--address-prefix 10.10.0.0/26 \
--network-security-group-name myNSG
```

Olá sub-rede agora é adicionada Olá VNet e associado ao hello NSG e regras do NSG hello.

## <a name="creating-static-dns-names"></a>Criando nomes DNS estáticos

O Azure é muito flexível, mas toouse nomes DNS para resolução de nomes de máquinas virtuais, você precisa toocreate-los como Virtual cartões (VNics) usando o DNS de rotulagem de rede.  VNics são importantes para você pode reutilizá-los, conectando-os toodifferent VMs, que mantém Olá VNic como um recurso estático, enquanto Olá VMs pode ser temporário.  Usando o DNS rótulos nos Olá VNic, estamos tooenable capaz de resolução de nome simples de outras VMs em redes de saudação.  Usando nomes resolvível permite que outro servidor de automação VMs tooaccess Olá por nome DNS Olá `Jenkins` ou servidor de Git hello como `gitrepo`.  Crie uma VNic e associá-lo a saudação que sub-rede criada na etapa anterior hello.

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a>Implantar hello VM em Olá VNet e NSG

Agora temos uma rede virtual, uma sub-rede dentro dessa rede virtual e um NSG atuando como um firewall tooprotect nosso sub-rede bloqueando todo o tráfego de entrada exceto 22 de porta para o SSH.  Olá VM agora pode ser implantado nessa infraestrutura de rede existente.

Usando Olá CLI do Azure e Olá `azure vm create` comando, Olá VM do Linux é implantado toohello grupo de recursos do Azure, redes, sub-rede e VNic existentes.  Para obter mais informações sobre como usar o hello CLI toodeploy uma VM completa, consulte [criar um ambiente completo do Linux usando Olá CLI do Azure](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

```azurecli
azure vm create jenkins \
--resource-group myResourceGroup myVM \
--location westus \
--os-type linux \
--image-urn Debian \
--storage-account-name mystorageaccount \
--admin-username myAdminUser \
--ssh-publickey-file ~/.ssh/id_rsa.pub \
--vnet-name myVNet \
--vnet-subnet-name mySubnet \
--nic-name jenkinsVNic
```

Usando Olá CLI sinalizadores de toocall recursos existentes, podemos instruir Olá toodeploy Azure VM dentro da rede existente hello.  tooreiterate, depois que uma rede virtual e a sub-rede forem implantados, eles podem ser mantidos como estáticos ou permanentes de recursos dentro de sua região do Azure.  

## <a name="next-steps"></a>Próximas etapas
* [Criar seu próprio ambiente personalizado para uma VM do Linux usando os comandos da CLI do Azure diretamente](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Criar uma VM do Linux no Azure usando modelos](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
