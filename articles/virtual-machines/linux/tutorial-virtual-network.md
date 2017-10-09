---
title: "aaaAzure redes virtuais e máquinas virtuais do Linux | Microsoft Docs"
description: "Tutorial - gerenciar redes virtuais do Azure e máquinas virtuais Linux com hello CLI do Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 57e6bd4de16f0e31d53dc67bf50dc5730d43712b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-networks-and-linux-virtual-machines-with-hello-azure-cli"></a>Gerenciar redes virtuais do Azure e máquinas virtuais Linux com hello CLI do Azure

As máquinas virtuais do Azure usam a rede do Azure para comunicação de rede interna e externa. Este tutorial explica como implantar duas máquinas virtuais e configurar a rede do Azure para essas VMs. exemplos de saudação neste tutorial pressupõem que VMs Olá estiver hospedando um aplicativo web com um banco de dados back-end, no entanto, um aplicativo não é implantado no tutorial de saudação. Neste tutorial, você aprenderá como:

> [!div class="checklist"]
> * Implantar uma rede virtual
> * Criar uma sub-rede em uma rede virtual
> * Anexar a sub-rede de tooa de máquinas virtuais
> * Gerenciar endereços IP públicos de máquina virtual
> * Proteger tráfego da internet de entrada
> * Proteger o tráfego de VM tooVM


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se você escolher tooinstall e usa o hello CLI localmente, este tutorial requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="vm-networking-overview"></a>Visão Geral da VM

Redes virtuais do Azure permitem conexões de rede segura entre máquinas virtuais, Olá internet e outros serviços do Azure como banco de dados do SQL Azure. As redes virtuais são divididas em segmentos lógicos chamados sub-redes. Sub-redes de fluxo de rede toocontrol e como um limite de segurança. Ao implantar uma VM, ele geralmente inclui uma interface de rede virtual, que é anexado tooa sub-rede.

## <a name="deploy-virtual-network"></a>Implantar rede virtual

Para este tutorial, uma única rede virtual é criada com duas sub-redes. Uma sub-rede de front-end para hospedar um aplicativo Web e uma sub-rede de back-end para hospedar um servidor de banco de dados.

Antes de criar uma máquina virtual, crie um grupo de recursos com o [az group create](/cli/azure/group#create). Olá, exemplo a seguir cria um grupo de recursos denominado *myRGNetwork* no local de eastus hello.

```azurecli-interactive 
az group create --name myRGNetwork --location eastus
```

### <a name="create-virtual-network"></a>Criar rede virtual

Nós Olá [criar redes de rede az](/cli/azure/network/vnet#create) comando toocreate uma rede virtual. Neste exemplo, é denominada rede Olá *mvVnet* e recebe um prefixo de endereço *10.0.0.0/16*. Uma sub-rede também é criada com o nome *mySubnetFrontEnd* e um prefixo *10.0.1.0/24*. Posteriormente neste tutorial uma VM de front-end é conectado toothis sub-rede. 

```azurecli-interactive 
az network vnet create \
  --resource-group myRGNetwork \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnetFrontEnd \
  --subnet-prefix 10.0.1.0/24
```

### <a name="create-subnet"></a>Criar sub-rede

Uma nova sub-rede é adicionada usando Olá de rede virtual do toohello [criar sub-rede de rede virtual de rede az](/cli/azure/network/vnet/subnet#create) comando. Neste exemplo, a sub-rede de saudação é chamada *mySubnetBackEnd* e recebe um prefixo de endereço *10.0.2.0/24*. Essa sub-rede é usada com todos os serviços de back-end.

```azurecli-interactive 
az network vnet subnet create \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --address-prefix 10.0.2.0/24
```

Neste ponto, uma rede foi criada e segmentada em duas sub-redes, uma para os serviços de front-end e outra para serviços de back-end. Na próxima seção, Olá, máquinas virtuais são criadas e toothese sub-redes conectadas.

## <a name="understand-public-ip-address"></a>Compreender o endereço IP público

Um endereço IP público permite a recursos do Azure toobe acessíveis no hello da internet. Nesta seção do tutorial hello, uma VM é criada toodemonstrate como toowork com IP público endereços.

### <a name="allocation-method"></a>Método de alocação

Um endereço IP público pode ser alocado como dinâmico ou estático. Por padrão, o endereço IP público é alocado dinamicamente. Os endereços IP dinâmicos são liberados quando uma VM é desalocada. Esse comportamento causar toochange de endereço IP hello durante qualquer operação que inclui uma desalocação da VM.

método de alocação Hello pode ser definido como toostatic, que garante que o endereço IP hello permaneçam atribuído tooa VM, mesmo durante um estado desalocado. Ao usar um endereço IP alocado estaticamente, endereço IP de saudação em si não pode ser especificado. Em vez disso, ele é alocado de um pool de endereços disponíveis.

### <a name="dynamic-allocation"></a>Alocação dinâmica

Ao criar uma VM com hello [criar vm az](/cli/azure/vm#create) comando saudação padrão público alocação método de endereço IP é dinâmico. No hello exemplo a seguir, uma VM é criada com um endereço IP dinâmico. 

```azurecli-interactive 
az vm create \
  --resource-group myRGNetwork \
  --name myFrontEndVM \
  --vnet-name myVnet \
  --subnet mySubnetFrontEnd \
  --nsg myNSGFrontEnd \
  --public-ip-address myFrontEndIP \
  --image UbuntuLTS \
  --generate-ssh-keys
```

### <a name="static-allocation"></a>Alocação estática

Ao criar uma máquina virtual usando Olá [criar vm az](/cli/azure/vm#create) de comando, inclua Olá `--public-ip-address-allocation static` argumento tooassign um endereço IP público estático. Esta operação não será demonstrada neste tutorial, porém na próxima seção, Olá um endereço IP alocada dinamicamente é alterado tooa estaticamente endereço alocado. 

### <a name="change-allocation-method"></a>Alterar método de alocação

método de alocação de endereço IP Hello pode ser alterado usando Olá [atualização de ip público de rede az](/cli/azure/network/public-ip#update) comando. Neste exemplo, Olá o método de alocação de endereço IP da VM front-end é alterado de saudação toostatic.

Primeiro, desalocar Olá VM.

```azurecli-interactive 
az vm deallocate --resource-group myRGNetwork --name myFrontEndVM
```

Saudação de uso [atualização de ip público de rede az](/cli/azure/network/public-ip#update) tooupdate método de alocação de saudação do comando. Nesse caso, Olá `--allocation-method` está sendo definido muito*estático*.

```azurecli-interactive 
az network public-ip update --resource-group myRGNetwork --name myFrontEndIP --allocation-method static
```

Inicie Olá VM.

```azurecli-interactive 
az vm start --resource-group myRGNetwork --name myFrontEndVM --no-wait
```

### <a name="no-public-ip-address"></a>Sem endereço IP público

Geralmente, uma máquina virtual não precisa toobe acessível pela internet de hello. toocreate uma máquina virtual sem um endereço IP público, use Olá `--public-ip-address ""` argumento com um conjunto vazio de aspas duplas. Essa configuração é demonstrada mais tarde neste tutorial

## <a name="secure-network-traffic"></a>Protegem o tráfego de rede

Um grupo de segurança de rede (NSG) contém uma lista de regras de segurança que permitem ou negam tooresources de tráfego de rede conectados a redes virtuais do tooAzure (VNet). Os NSGs podem ser associados toosubnets ou interfaces de rede individuais. Quando um NSG está associado uma interface de rede, ele se aplica somente a saudação associados a VM. Quando um NSG está associado tooa sub-rede, regras de saudação aplicam tooall recursos toohello conectado sub-rede. 

### <a name="network-security-group-rules"></a>Regras de grupo de segurança de rede

As regras NSG definem portas de rede pelas quais o tráfego é permitido ou negado. regras de saudação podem incluir intervalos de endereços IP de origem e de destino para que o tráfego é controlado entre sistemas específicos ou sub-redes. As regras NSG também incluem uma prioridade (entre 1 e 4096). Regras são avaliadas na ordem de saudação de prioridade. Uma regra com uma prioridade 100 é avaliada antes de uma regra com prioridade 200.

Todos os NSGs contêm um conjunto de regras padrão. as regras de saudação padrão não podem ser excluídas, mas porque eles recebem a prioridade mais baixa hello, elas podem ser substituídas pelas regras de saudação que você criar.

- **Rede virtual:** o tráfego que começa e termina em uma rede virtual é permitido nas direções de entrada e saída.
- **Internet:** o tráfego de saída é permitido, mas o tráfego de entrada é bloqueado.
- **Balanceador de carga** -integridade do Azure carga balanceador tooprobe Olá permitir de suas máquinas virtuais e instâncias de função. Se não estiver usando um conjunto de balanceamento de carga, você poderá substituir essa regra.

### <a name="create-network-security-groups"></a>Criar grupos de segurança de rede

Um grupo de segurança de rede pode ser criado no hello mesmo tempo como uma VM usando Olá [criar vm az](/cli/azure/vm#create) comando. Ao fazer isso, Olá NSG está associado com a interface de rede de VMs hello e uma regra NSG é criado automaticamente tooallow tráfego na porta *22* de qualquer fonte. Anteriormente neste tutorial, Olá NSG front-end foi criado automaticamente com hello VM front-end. Uma regra NSG também foi criada para a porta 22 automaticamente. 

Em alguns casos, pode ser útil toopre-criar um NSG, como quando as regras padrão SSH não devem ser criadas ou quando Olá NSG deve ser anexado tooa sub-rede. 

Saudação de uso [criar az rede nsg](/cli/azure/network/nsg#create) comando toocreate um grupo de segurança de rede.

```azurecli-interactive 
az network nsg create --resource-group myRGNetwork --name myNSGBackEnd
```

Em vez de associação de interface de rede do hello NSG tooa, está associado uma sub-rede. Nessa configuração, qualquer que seja anexado toohello sub-rede VM herda as regras NSG hello.

Atualizar subrede existente Olá denominado *mySubnetBackEnd* com hello novo NSG.

```azurecli-interactive 
az network vnet subnet update \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --network-security-group myNSGBackEnd
```

Agora crie uma máquina virtual, que é anexado toohello *mySubnetBackEnd*. Observe que Olá `--nsg` argumento tem um valor de aspas duplas vazios. Um NSG não precisa toobe criado com hello VM. Olá VM é a sub-rede de back-end toohello anexado, que é protegido por hello criado previamente NSG de back-end. Este NSG aplica toohello VM. Além disso, observe aqui que Olá `--public-ip-address` argumento tem um valor de aspas duplas vazios. Essa configuração cria uma VM sem um endereço IP público. 

```azurecli-interactive 
az vm create \
  --resource-group myRGNetwork \
  --name myBackEndVM \
  --vnet-name myVnet \
  --subnet mySubnetBackEnd \
  --public-ip-address "" \
  --nsg "" \
  --image UbuntuLTS \
  --generate-ssh-keys
```

### <a name="secure-incoming-traffic"></a>Proteger o tráfego de entrada

Quando hello front-end VM foi criada, uma regra NSG foi criada tooallow o tráfego de entrada na porta 22. Essa regra permite conexões de SSH toohello VM. Para este exemplo, o tráfego também deve ser permitido na porta *80*. Essa configuração permite que um toobe de aplicativo da web acessado em Olá VM.

Saudação de uso [criar regra de nsg rede az](/cli/azure/network/nsg/rule#create) comando toocreate uma regra de porta *80*.

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGFrontEnd \
  --name http \
  --access allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 200 \
  --source-address-prefix "*" \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range 80
```

Olá front-end VM agora só está acessível na porta *22* e porta *80*. Todos os outros tráfegos de entrada é bloqueado no grupo de segurança de rede hello. Pode ser as configurações de regra NSG toovisualize útil hello. Configuração da regra NSG Olá retorno com hello [lista de regras de rede az](/cli/azure/network/nsg/rule#list) comando. 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGFrontEnd --output table
```

Saída:

```azurecli-interactive 
Access    DestinationAddressPrefix      DestinationPortRange  Direction    Name                 Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -----------------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                                               22  Inbound      default-allow-ssh        1000  Tcp         Succeeded            myRGNetwork      *                      *
Allow     *                                               80  Inbound      http                      200  Tcp         Succeeded            myRGNetwork      *                      *
```

### <a name="secure-vm-toovm-traffic"></a>Proteger o tráfego de VM tooVM

As regras de grupo de segurança de rede também podem se aplicar entre VMs. Neste exemplo, Olá VM front-end precisa toocommunicate com hello VM back-end na porta *22* e *3306*. Essa configuração permite conexões de SSH de Olá VM front-end e também permitir que um aplicativo em Olá toocommunicate front-end de VM com um banco de dados do MySQL de back-end. Todo o tráfego deve ser bloqueado entre Olá máquinas de virtuais de front-end e back-end.

Saudação de uso [criar regra de nsg rede az](/cli/azure/network/nsg/rule#create) comando toocreate uma regra de porta 22. Observe que Olá `--source-address-prefix` argumento especifica um valor de *10.0.1.0/24*. Essa configuração garante que apenas o tráfego de sub-rede front-end Olá é permitido por meio de saudação NSG.

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name SSH \
  --access Allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 100 \
  --source-address-prefix 10.0.1.0/24 \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "22"
```

Agora, adicione uma regra para o tráfego MySQL na porta 3306.

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name MySQL \
  --access Allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 200 \
  --source-address-prefix 10.0.1.0/24 \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "3306"
```

Por fim, porque os NSGs tem uma regra padrão permitindo que todo o tráfego entre VMs em Olá mesmo VNet, uma regra pode ser criada para Olá back-end NSGs tooblock todo o tráfego. Observe aqui que Olá `--priority` recebe um valor de *300*, que é menor do que ambos Olá regras NSG e MySQL. Essa configuração garante que o tráfego SSH e MySQL ainda é permitido pelo Olá NSG.

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name denyAll \
  --access Deny \
  --protocol Tcp \
  --direction Inbound \
  --priority 300 \
  --source-address-prefix "*" \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "*"
```

Olá VM back-end é agora somente acessível na porta *22* e porta *3306* da sub-rede front-end hello. Todos os outros tráfegos de entrada é bloqueado no grupo de segurança de rede hello. Pode ser as configurações de regra NSG toovisualize útil hello. Configuração da regra NSG Olá retorno com hello [lista de regras de rede az](/cli/azure/network/nsg/rule#list) comando. 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGBackEnd --output table
```

Saída:

```azurecli-interactive 
Access    DestinationAddressPrefix    DestinationPortRange    Direction    Name       Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                           22                      Inbound      SSH             100  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Allow     *                           3306                    Inbound      MySQL           200  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Deny      *                           *                       Inbound      denyAll         300  Tcp         Succeeded            myRGNetwork      *                      *
```

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você criou e redes do Azure como máquinas toovirtual relacionados seguras. Você aprendeu como:

> [!div class="checklist"]
> * Implantar uma rede virtual
> * Criar uma sub-rede em uma rede virtual
> * Anexar a sub-rede de tooa de máquinas virtuais
> * Gerenciar endereços IP públicos de máquina virtual
> * Proteger tráfego da internet de entrada
> * Proteger o tráfego de VM tooVM

Avançar toohello toolearn próximo de tutorial sobre como proteger dados em máquinas virtuais usando o backup do Azure. 

> [!div class="nextstepaction"]
> [Fazer backup de máquinas virtuais do Linux no Azure](./tutorial-backup-vms.md)
