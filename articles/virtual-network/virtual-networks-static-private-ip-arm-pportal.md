---
title: "endereços IP privados de aaaConfigure para VMs - portal do Azure | Microsoft Docs"
description: "Saiba como tooconfigure endereços IP para máquinas virtuais usando Olá portal do Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 11245645-357d-4358-9a14-dd78e367b494
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 474161303cdf8cb98e16ffd7cef6b74debdbc49a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-portal"></a>Configurar endereços IP para uma máquina virtual usando Olá portal do Azure

> [!div class="op_single_selector"]
> * [Portal do Azure](virtual-networks-static-private-ip-arm-pportal.md)
> * [PowerShell](virtual-networks-static-private-ip-arm-ps.md)
> * [CLI do Azure](virtual-networks-static-private-ip-arm-cli.md)
> * [Portal do Azure (Clássico)](virtual-networks-static-private-ip-classic-pportal.md)
> * [PowerShell (Clássico)](virtual-networks-static-private-ip-classic-ps.md)
> * [CLI do Azure (Clássica)](virtual-networks-static-private-ip-classic-cli.md)


[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Este artigo aborda o modelo de implantação do Gerenciador de recursos de saudação. Você também pode [gerenciar o endereço IP privado estático no modelo de implantação clássico Olá](virtual-networks-static-private-ip-classic-pportal.md).

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

etapas do exemplo Hello abaixo esperam um ambiente simples já criado. Se você quiser etapas de saudação toorun conforme elas são exibidas neste documento, primeiro criar o ambiente de teste de hello, descrito em [criar uma rede virtual](virtual-networks-create-vnet-arm-pportal.md).

## <a name="how-toocreate-a-vm-for-testing-static-private-ip-addresses"></a>Como toocreate uma máquina virtual para teste de IP privado estático endereços
Você não pode definir um endereço IP privado estático durante a criação de saudação de uma VM no modo de implantação do Gerenciador de recursos de saudação usando Olá portal do Azure. Primeiro você deve criar hello VM, tehn defina sua toobe IP privado estático.

toocreate uma VM denominada *DNS01* em Olá *front-end* sub-rede de uma rede virtual denominada *TestVNet*, siga as etapas de saudação abaixo.

1. Em um navegador, navegue toohttp://portal.azure.com e, se necessário, entre com sua conta do Azure.
2. Clique em **novo** > **de computação** > **Windows Server 2012 R2 Datacenter**, observe que Olá **selecionar um modelo de implantação** já lista mostra **Gerenciador de recursos de**e, em seguida, clique em **criar**, como mostrado na figura de saudação abaixo.
   
    ![Criar VM no portal do Azure](./media/virtual-networks-static-ip-arm-pportal/figure01.png)
3. Em Olá **Noções básicas de** folha, digite nome de saudação do hello VM toobe criado (*DNS01* em nosso cenário), Olá a conta de administrador local e senha, como mostrado na figura abaixo a saudação.
   
    ![Folha de Noções básicas](./media/virtual-networks-static-ip-arm-pportal/figure02.png)
4. Tornar-se de saudação **local** selecionado é *centro dos EUA*, em seguida, clique em **selecionar existentes** em **grupo de recursos**, clique **Grupo de recursos** novamente, em seguida, clique em *TestRG*e, em seguida, clique em **Okey**.
   
    ![Folha de Noções básicas](./media/virtual-networks-static-ip-arm-pportal/figure03.png)
5. Em Olá **escolher um tamanho de** folha, selecione **A1 padrão**e, em seguida, clique em **selecione**.
   
    ![Escolha uma folha de tamanho](./media/virtual-networks-static-ip-arm-pportal/figure04.png)    
6. No **configurações** folha, verifique Olá se seguintes propriedades são definidas são definidas com valores de saudação abaixo e, em seguida, clique em **Okey**.
   
    -**Conta de armazenamento**: *vnetstorage*
   
   * **Rede**: *TestVNet*
   * **Sub-rede**: *FrontEnd*
     
     ![Escolha uma folha de tamanho](./media/virtual-networks-static-ip-arm-pportal/figure05.png)     
7. Em Olá **resumo** folha, clique em **Okey**. Aviso Olá bloco abaixo exibido no painel.
   
    ![Criar VM no portal do Azure](./media/virtual-networks-static-ip-arm-pportal/figure06.png)

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a>Como informações de uma VM de endereço de IP privado estático de tooretrieve
tooview Olá privadas informações endereços IP estáticos para Olá VM criada com etapas de saudação acima, execute as etapas de saudação abaixo.

1. No portal do Azure Azure hello, clique em **procurar todos os** > **máquinas virtuais** > **DNS01** > **todos configurações de** > **interfaces de rede** e, em seguida, clique na interface de rede somente Olá listado.
   
    ![Implantando o bloco VM](./media/virtual-networks-static-ip-arm-pportal/figure07.png)
2. Em Olá **interface de rede** folha, clique em **todas as configurações** > **endereços IP** e observe hello **atribuição** e **Endereço IP** valores.
   
    ![Implantando o bloco VM](./media/virtual-networks-static-ip-arm-pportal/figure08.png)

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a>Como tooadd um endereço IP privado estático endereço tooan existente VM
tooadd um toohello de endereço IP de privado estático VM criada usando Olá etapas acima, siga as etapas de saudação abaixo:

1. De saudação **endereços IP** folha mostrada acima, clique em **estático** em **atribuição**.
2. Digite *192.168.1.101* para **Endereço IP**, e, em seguida, clique em **Salvar**.
   
    ![Criar VM no portal do Azure](./media/virtual-networks-static-ip-arm-pportal/figure09.png)

> [!NOTE]
> Se, depois de clicar em **salvar** você notar que a atribuição Olá ainda está definida muito**dinâmico**, isso significa que o endereço IP hello digitado já está em uso. Tente um endereço IP diferente.
> 
> 

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a>Como tooremove um particular de endereços IP estáticos de uma VM
tooremove Olá endereço IP privado estático de saudação VM criada acima, conclua Olá etapa a seguir:

De saudação **endereços IP** folha mostrada acima, clique em **dinâmico** em **atribuição**e, em seguida, clique em **salvar**.

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre endereços [IP públicos reservados](virtual-networks-reserved-public-ip.md) .
* Saiba mais sobre endereços [ILPIP (IP público em nível de instância)](virtual-networks-instance-level-public-ip.md) .
* Consulte Olá [APIs de REST de IP reservado](https://msdn.microsoft.com/library/azure/dn722420.aspx).

