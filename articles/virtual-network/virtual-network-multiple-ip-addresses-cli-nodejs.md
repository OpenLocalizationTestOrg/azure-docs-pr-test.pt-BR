---
title: "aaaVM com vários endereços IP usando Olá 1.0 da CLI do Azure | Microsoft Docs"
description: "Saiba como tooassign vários endereços IP tooa máquina virtual usando Olá 1.0 da CLI do Azure | Gerenciador de recursos."
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/17/2016
ms.author: annahar
ms.openlocfilehash: 83ad48e67309fb21d5aca967d4f2c01afdc0b5cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-azure-cli-10"></a>Atribuir vários endereços IP toovirtual máquinas usando 1.0 da CLI do Azure

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

Este artigo explica como toocreate uma máquina virtual (VM) por meio de saudação do Azure Resource Manager implantação do modelo usando Olá 1.0 da CLI do Azure. Tooresources criado por meio do modelo de implantação clássico Olá não podem ser atribuídos a vários endereços IP. toolearn mais sobre modelos de implantação do Azure, leia Olá [entender os modelos de implantação](../resource-manager-deployment-model.md) artigo.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a>Criar uma VM com vários endereços IP

Você pode concluir essa tarefa usando Olá CLI do Azure 1.0 (Este artigo) ou hello [Azure CLI 2.0](virtual-network-multiple-ip-addresses-cli.md). etapas Olá que seguem explicam como toocreate um exemplo VM com IP vários endereços, conforme descrito no cenário de saudação. Altere os nomes da variável e os tipos de endereço IP como exigido por sua implementação.

1. Instalar e configurar hello Azure CLI 1.0 por Olá seguir as etapas em Olá [instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artigo e faça logon em sua conta do Azure com hello `azure-login` comando.

2. Crie um grupo de recursos:
    
    ```azurecli
    RgName=myResourceGroup
    Location=westcentralus
    azure group create --name $RgName --location $Location
    ```
3. Criar uma rede virtual:

    ```azurecli
    azure network vnet create --resource-group $RgName --location $Location --name myVNet \
    --address-prefixes 10.0.0.0/16
    ```
4. Crie uma sub-rede na rede virtual hello:

    ```azurecli
    azure network vnet subnet create --name mySubnet --resource-group $RgName --vnet-name myVNet \
    --address-prefix 10.0.0.0/24
    ```
    
5. Crie uma conta de armazenamento para Olá VM. Antes de executar Olá após o comando, substitua *mystorageaccount* com um nome exclusivo. nome da saudação deve ser exclusivo no Azure:

    ```azurecli
    az storage account create --resource-group $RgName --location $Location --name mystorageaccount \
    --kind Storage --sku Standard_LRS
    ```

6. Criar hello configurações de IP de uma NIC e atribuir Olá IP configurações toohello NIC em. Você pode adicionar, remover ou alterar as configurações de saudação conforme necessário. Olá configurações a seguir é descrita no cenário de saudação:

    **IPConfig-1**

    Digite os comandos de saudação que seguem toocreate:

    - Um recurso de endereço IP público com um endereço IP público estático
    - Uma NIC, atribuição de endereço IP público de saudação e um tooit de endereço IP privado estático.
    
    Substituir *mypublicdns* com um nome que seja exclusivo dentro de saudação local do Azure.

      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP1 \
      --domain-name-label mypublicdns --allocation-method Static
        
      azure network nic create --resource-group $RgName --location $Location --name myNic1 \
      --private-ip-address 10.0.0.4 --subnet-name mySubnet --subnet-vnet-name myVNet \
      --subnet-name mySubnet --public-ip-name myPublicIP1
      ```

      > [!NOTE]
      > Endereços IP públicos têm um valor nominal. toolearn mais sobre endereços IP de preços, ler Olá [preço do endereço IP](https://azure.microsoft.com/pricing/details/ip-addresses) página. Há um número de toohello limite de endereços IP públicos que podem ser usados em uma assinatura. mais sobre os limites de Olá Olá de leitura de toolearn [Azure limita](../azure-subscription-service-limits.md#networking-limits) artigo.

    **IPConfig-2**

     Um novo recurso de endereço IP público e uma nova configuração de IP com um endereço IP público estático e um endereço IP privado estático, digite Olá toocreate comandos a seguir:
    
      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP2
      --domain-name-label mypublicdns2 --allocation-method Static

      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --name IPConfig-2
      --private-ip-address 10.0.0.5 --public-ip-name myPublicIP2
      ```

    **IPConfig-3**

    Digite hello comandos toocreate uma configuração de IP com um endereço IP privado estático e nenhum endereço IP público a seguir:

      ```azurecli
      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --private-ip-address 10.0.0.6 \
      --name IPConfig-3
      ```

    >[!NOTE] 
    >Embora este artigo atribui todos os tooa de configurações de IP NIC único, você também pode atribuir várias tooany de configurações de IP NIC em uma VM. toolearn como ler de uma VM com várias NICs, toocreate Olá criar uma VM com o artigo de várias NICs.

7. Criar uma VM do Linux 

    ```azurecli
    az vm create --resource-group $RgName --name myVM1 --location $Location --nics myNic1 \
    --image UbuntuLTS --ssh-key-value ~/.ssh/id_rsa.pub --admin-username azureuser
    ```

    toochange Olá VM tamanho tooStandard DS2 v2, por exemplo, basta adicionar Olá propriedade a seguir `--vm-size Standard_DS3_v2` toohello `azure vm create` comando na etapa 6.

8. Insira Olá Olá do comando tooview NIC a seguir e Olá as configurações de IP associadas:

    ```azurecli
    azure network nic show --resource-group $RgName --name myNic1
    ```
9. IP privado de saudação adicionar endereços toohello sistema de operacional VM por etapas para seu sistema operacional no Olá Olá [tooa sistema de operacional VM de endereços de IP adicionar](#os-config) deste artigo.

## <a name="add"></a>Adicionar endereços IP tooa VM

Você pode adicionar adicionais pública e privada IP endereços tooan existente NIC completando as etapas de saudação que seguem. exemplos de saudação incrementar Olá [cenário](#Scenario) descrito neste artigo.

1. Abra a CLI do Azure e completa hello restantes etapas nesta seção dentro de uma única sessão CLI. Se você ainda não tiver a CLI do Azure instalado e configurado, Olá concluir etapas no hello [instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artigo e faça logon em sua conta do Azure.

2. Conclua as etapas de saudação em uma das seguintes seções, com base nas necessidades de saudação:

    - **Adicionar um endereço IP privado**
    
        tooadd um tooa de endereço IP privado NIC, você deve criar uma configuração de IP usando o comando de saudação abaixo. endereço estático Olá deve ser um endereço não usado para a sub-rede de saudação.

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic1 \
        --private-ip-address 10.0.0.7 --name IPConfig-4
        ```
        Crie quantas configurações forem necessárias, usando nomes de configuração exclusivos e endereços IP privados (para configurações com endereços IP estáticos).

    - **Adicionar um endereço IP público**
    
        Um endereço IP público é adicionado ao associá-la tooeither uma nova configuração de IP ou uma configuração de IP existente. Conclua as etapas de saudação em uma saudação próximas seções, você precisa.

        > [!NOTE]
        > Endereços IP públicos têm um valor nominal. toolearn mais sobre endereços IP de preços, ler Olá [preço do endereço IP](https://azure.microsoft.com/pricing/details/ip-addresses) página. Há um número de toohello limite de endereços IP públicos que podem ser usados em uma assinatura. mais sobre os limites de Olá Olá de leitura de toolearn [Azure limita](../azure-subscription-service-limits.md#networking-limits) artigo.
        >

        **Associar Olá recurso tooa nova configuração de IP**
    
        Sempre que você adicionar um endereço IP público em uma nova configuração de IP, também deverá adicionar um endereço IP privado, pois todas as configurações de IP devem ter um endereço IP privado. Você pode adicionar um recurso de endereço IP público existente ou criar um novo. toocreate uma nova, digite Olá comando a seguir:

        ```azurecli
        azure network public-ip create --resource-group myResourceGroup --location westcentralus --name myPublicIP3 \
        --domain-name-label mypublicdns3
        ```

        toocreate uma nova configuração de IP com um endereço IP privado estático e Olá associados *myPublicIP3* IP público recurso de endereço, digite Olá comando a seguir:

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic --name IPConfig-4 \
        --private-ip-address 10.0.0.8 --public-ip-name myPublicIP3
        ```

        **Associar a configuração de IP existente do hello recursos tooan**

        Um recurso de endereço IP público só pode ser a configuração de IP tooan associado que ainda não tiver um associado. Você pode determinar se uma configuração de IP tem um endereço IP público associado inserindo Olá comando a seguir:

        ```azurecli
        azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
        ```

        Procure um toohello semelhante de linha que segue para 3 IPConfig no hello retornado de saída:

        ```         
        Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
        IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
        IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet
        ```
          
        Desde Olá **IP público** coluna para *IpConfig 3* está em branco, nenhum recurso de endereço IP público é tooit atualmente associado. Você pode adicionar um existente pública IP endereço recurso tooIpConfig-3, ou insira Olá toocreate comando um a seguir:

        ```azurecli
        azure network public-ip create --resource-group  myResourceGroup --location westcentralus \
        --name myPublicIP3 --domain-name-label mypublicdns3 --allocation-method Static
        ```

        Digite hello recurso toohello existente IP configuração denominada do endereço IP público do tooassociate Olá de comando a seguir *3 IPConfig*:
        ```azurecli
        azure network nic ip-config set --resource-group myResourceGroup --nic-name myNic1 --name IPConfig-3 \
        --public-ip-name myPublicIP3
        ```

3. Exibir endereços IP privados de saudação e Olá pública IP endereço recursos atribuído toohello NIC inserindo Olá o comando a seguir:

    ```azurecli
    azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
    ```

      Olá retornado é de saída a seguir toohello semelhante:
      ```
      Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        
      default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
      IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
      IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet  myPublicIP3
      ```
4. Adicionar endereços IP privados Olá adicionado o sistema operacional do toohello NIC toohello VM seguindo instruções Olá Olá [tooa sistema de operacional VM de endereços de IP adicionar](#os-config) deste artigo. Não adicione Olá pública IP endereços toohello sistema operacional.

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
