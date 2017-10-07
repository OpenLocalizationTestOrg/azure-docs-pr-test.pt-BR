---
title: "endereços IP privados de aaaConfigure para VMs (clássico) - 1.0 da CLI do Azure | Microsoft Docs"
description: "Saiba como tooconfigure endereços IP para máquinas virtuais (clássico) usando hello Azure interface de linha de comando (CLI) 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 17386acf-c708-4103-9b22-ff9bf04b778d
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 417a57181bcf5c2e6101bf3bdf63fc94ebc99df5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-hello-azure-cli-10"></a>Configurar endereços IP para uma máquina virtual (clássica) usando Olá 1.0 da CLI do Azure

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Este artigo aborda o modelo de implantação clássico hello. Você também pode [gerenciar um endereço IP privado estático no modelo de implantação do Gerenciador de recursos de saudação](virtual-networks-static-private-ip-arm-cli.md).

comandos de CLI do Azure de exemplo Hello abaixo esperam um ambiente simples já criado. Se você quiser comandos de saudação toorun conforme elas são exibidas neste documento, primeiro criar o ambiente de teste de hello, descrito em [criar uma rede virtual](virtual-networks-create-vnet-classic-cli.md).

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a>Como toospecify um particular de endereços IP estáticos ao criar uma VM
toocreate uma nova VM denominada *DNS01* em um novo serviço de nuvem chamado *TestService* com base no cenário de saudação acima, siga estas etapas:

1. Se você nunca tiver usado a CLI do Azure, consulte [instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md) e siga as instruções de saudação toohello ponto em que você selecione sua conta do Azure e assinatura.
2. Executar Olá **criar serviço do azure** toocreate serviço de nuvem de saudação do comando.
   
        azure service create TestService --location uscentral
   
    Saída esperada:
   
        info:    Executing command service create
        info:    Creating cloud service
        data:    Cloud service name TestService
        info:    service create command OK
3. Executar Olá **azure criar vm** saudação do comando toocreate VM. Observe o valor de saudação para um endereço IP privado estático. lista de saudação mostrada após a saída de hello explica parâmetros Olá usados.
   
        azure vm create -l centralus -n DNS01 -w TestVNet -S "192.168.1.101" TestService bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2 adminuser AdminP@ssw0rd
   
    Saída esperada:
   
        info:    Executing command vm create
        warn:    --vm-size has not been specified. Defaulting too"Small".
        info:    Looking up image bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2
        info:    Looking up virtual network
        info:    Looking up cloud service
        warn:    --location option will be ignored
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Retrieving storage accounts
        info:    Creating VM
        info:    OK
        info:    vm create command OK
   
   * **-l (ou --location)**. Região do Azure onde Olá VM será criado. Para o nosso cenário, *centralus*.
   * **-n (ou --vm-name)**. Nome da saudação VM toobe criado.
   * **-w (ou --virtual-network-name)**. Nome da saudação redes onde Olá VM será criado. 
   * **-S (ou --static-ip)**. Endereço IP privado estático para Olá VM.
   * **TestService**. Nome do serviço de nuvem Olá onde Olá VM será criado.
   * **bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2**. Imagem usada toocreate hello VM.
   * **adminuser**. Administrador local para Olá VM do Windows.
   * **AdminP@ssw0rd**. Senha de administrador local para Olá VM do Windows.

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a>Como informações de uma VM de endereço de IP privado estático de tooretrieve
tooview Olá IP privado estático informações sobre endereço de saudação VM criada com o script de saudação acima, execute Olá após o comando CLI do Azure e observe o valor Olá *StaticIP rede*:

    azure vm static-ip show DNS01

Saída esperada:

    info:    Executing command vm static-ip show
    info:    Getting virtual machines
    data:    Network StaticIP "192.168.1.101"
    info:    vm static-ip show command OK

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a>Como tooremove um particular de endereços IP estáticos de uma VM
tooremove Olá endereço IP privado estático adicionados toohello VM script hello acima, Olá execução após o comando CLI do Azure:

    azure vm static-ip remove DNS01

Saída esperada:

    info:    Executing command vm static-ip remove
    info:    Getting virtual machines
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip remove command OK

## <a name="how-tooadd-a-static-private-ip-tooan-existing-vm"></a>Como tooadd uma tooan IP privado estático VM existente
tooadd um toohello de endereço IP de privado estático VM criada usando o script hello acima runt comando a seguir:

    azure vm static-ip set DNS01 192.168.1.101

Saída esperada:

    info:    Executing command vm static-ip set
    info:    Getting virtual machines
    info:    Looking up virtual network
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip set command OK

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre endereços [IP públicos reservados](virtual-networks-reserved-public-ip.md) .
* Saiba mais sobre endereços [ILPIP (IP público em nível de instância)](virtual-networks-instance-level-public-ip.md) .
* Consulte Olá [APIs de REST de IP reservado](https://msdn.microsoft.com/library/azure/dn722420.aspx).

