---
title: "endereços IP privados de aaaConfigure para VMs (clássico) - portal do Azure | Microsoft Docs"
description: "Saiba como tooconfigure endereços IP para máquinas virtuais (clássico) usando Olá portal do Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: b8ef8367-58b2-42df-9f26-3269980950b8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: df4bfa6768fc9e66db89785b633ffdb0274dbc46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-hello-azure-portal"></a>Configurar endereços IP para uma máquina virtual (clássica) usando Olá portal do Azure

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Este artigo aborda o modelo de implantação clássico hello. Você também pode [gerenciar um endereço IP privado estático no modelo de implantação do Gerenciador de recursos de saudação](virtual-networks-static-private-ip-arm-pportal.md).

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

etapas do exemplo Hello abaixo esperam um ambiente simples já criado. Se você quiser etapas de saudação toorun conforme elas são exibidas neste documento, primeiro criar o ambiente de teste de hello, descrito em [criar uma rede virtual](virtual-networks-create-vnet-classic-pportal.md).

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a>Como toospecify um particular de endereços IP estáticos ao criar uma VM
toocreate uma VM denominada *DNS01* em Olá *front-end* sub-rede de uma rede virtual denominada *TestVNet* com um endereço IP privado estático de *192.168.1.101*, Siga as etapas de saudação abaixo:

1. Em um navegador, navegue toohttp://portal.azure.com e, se necessário, entre com sua conta do Azure.
2. Clique em **novo** > **de computação** > **Windows Server 2012 R2 Datacenter**, observe que Olá **selecionar um modelo de implantação** já lista mostra **clássico**e, em seguida, clique em **criar**.
   
    ![Criar VM no portal do Azure](./media/virtual-networks-static-ip-classic-pportal/figure01.png)
3. Em Olá **criar VM** folha, digite nome de saudação do hello VM toobe criado (*DNS01* em nosso cenário), Olá a conta de administrador local e a senha.
   
    ![Criar VM no portal do Azure](./media/virtual-networks-static-ip-classic-pportal/figure02.png)
4. Clique em **Configuração opcional** > **Rede** > **Rede Virtual**, e, em seguida, clique em **TestVNet**. Se **TestVNet** não estiver disponível, verifique se você está usando Olá *centro dos EUA* local e criou o ambiente de teste Olá descrita no início deste artigo hello.
   
    ![Criar VM no portal do Azure](./media/virtual-networks-static-ip-classic-pportal/figure03.png)
5. Em Olá **rede** folha, verifique se Olá a sub-rede selecionada no momento é *front-end*, em seguida, clique em **endereços IP**, em **aatribuiçãodeendereçoIP** clique **estático**e, em seguida, digite *192.168.1.101* para **endereço IP** conforme mostrado abaixo.
   
    ![Criar VM no portal do Azure](./media/virtual-networks-static-ip-classic-pportal/figure04.png)    
6. Clique em **Okey** em Olá **endereços IP** folha, em seguida, clique em **Okey** em Olá **rede** folha e clique em **Okey**em Olá **configuração opcional** folha.
7. Em Olá **criar VM** folha, clique em **criar**. Aviso Olá bloco abaixo exibido no painel.
   
    ![Criar VM no portal do Azure](./media/virtual-networks-static-ip-classic-pportal/figure05.png)

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a>Como informações de uma VM de endereço de IP privado estático de tooretrieve
tooview Olá privadas informações endereços IP estáticos para Olá VM criada com etapas de saudação acima, execute as etapas de saudação abaixo.

1. No portal do Azure Azure hello, clique em **procurar todos os** > **máquinas virtuais (clássicas)** > **DNS01**  >   **Todas as configurações** > **endereços IP** e observe Olá a atribuição de endereço IP e endereço IP, conforme mostrado abaixo.
   
    ![Criar VM no portal do Azure](./media/virtual-networks-static-ip-classic-pportal/figure06.png)

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a>Como tooremove um particular de endereços IP estáticos de uma VM
tooremove Olá endereço IP privado estático de saudação VM criada anteriormente, execute as etapas de saudação abaixo.

1. De saudação **endereços IP** folha mostrada acima, clique em **dinâmico** toohello à direita do **atribuição de endereço IP**, em seguida, clique em **salvar**e, em seguida, Clique em **Sim**.
   
    ![Criar VM no portal do Azure](./media/virtual-networks-static-ip-classic-pportal/figure07.png)

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a>Como tooadd um endereço IP privado estático endereço tooan existente VM
tooadd um toohello de endereço IP de privado estático VM criada usando Olá etapas acima, siga as etapas de saudação abaixo:

1. De saudação **endereços IP** folha mostrada acima, clique em **estático** toohello à direita do **atribuição de endereço IP**.
2. Digite *192.168.1.101* para **Endereço IP**, clique em **Salvar** e, em seguida, clique em **Sim**.

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre endereços [IP públicos reservados](virtual-networks-reserved-public-ip.md) .
* Saiba mais sobre endereços [ILPIP (IP público em nível de instância)](virtual-networks-instance-level-public-ip.md) .
* Consulte Olá [APIs de REST de IP reservado](https://msdn.microsoft.com/library/azure/dn722420.aspx).

