---
title: aaaCannot excluir uma rede virtual no Azure | Microsoft Docs
description: "Saiba como tootroubleshoot Olá problema em que você não pode excluir uma rede virtual no Azure."
services: virtual-network
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: genli
ms.openlocfilehash: a9050ab238ccb0380fd46130430222efb8f42388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-failed-toodelete-a-virtual-network-in-azure"></a>Solução de problemas: Falha toodelete uma rede virtual no Azure

Você poderá receber erros ao tentar toodelete uma rede virtual no Microsoft Azure. Este artigo fornece toohelp de etapas de solução de problemas é resolver esse problema. 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-guidance"></a>Diretriz de solução de problemas 

1. [Verifique se um gateway de rede virtual está em execução na rede virtual Olá](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).
2. [Verifique se um gateway de aplicativo está em execução na rede virtual Olá](#check-whether-an-application-gateway-is-running-in-the-virtual-network).
3. [Verifique se o serviço de domínio do Azure Active Directory está habilitado na rede virtual Olá](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).
4. [Verificar se a rede virtual Olá é conectado tooother recurso](#check-whether-the-virtual-network-is-connected-to-other-resource).
5. [Verifique se uma máquina virtual ainda está em execução na rede virtual Olá](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).
6. [Verifique se a rede virtual hello está preso em migração](#check-whether-the-virtual-network-is-stuck-in-migration).

## <a name="troubleshooting-steps"></a>Etapas para solucionar problemas

### <a name="check-whether-a-virtual-network-gateway-is-running-in-hello-virtual-network"></a>Verifique se um gateway de rede virtual está em execução na rede virtual Olá

rede virtual do tooremove hello, remova primeiro o gateway de rede virtual hello.

Para redes virtuais clássicas, vá toohello **visão geral** página Olá clássico virtual em rede Olá portal do Azure. Em Olá **conexões VPN** seção, se o gateway de saudação está em execução na rede virtual hello, você verá Olá IP endereço do gateway de saudação. 

![Verifique se o gateway está em execução](media/virtual-network-troubleshoot-cannot-delete-vnet/classic-gateway.png)

Para redes virtuais, consulte toohello **visão geral** página da rede virtual hello. Verificar **dispositivos conectados** para gateway de rede virtual hello.

![Verifique o dispositivo conectado Olá](media/virtual-network-troubleshoot-cannot-delete-vnet/vnet-gateway.png)

Antes de remover gateway hello, primeiro remova qualquer **Conexão** objetos no gateway hello. 

### <a name="check-whether-an-application-gateway-is-running-in-hello-virtual-network"></a>Verifique se um gateway de aplicativo está em execução na rede virtual Olá

Vá toohello **visão geral** página da rede virtual hello. Verificar Olá **dispositivos conectados** para gateway de aplicativo hello.

![Verifique o dispositivo conectado Olá](media/virtual-network-troubleshoot-cannot-delete-vnet/app-gateway.png)

Se houver um application gateway, você deve removê-lo antes de você pode excluir a rede virtual hello.

### <a name="check-whether-azure-active-directory-domain-service-is-enabled-in-hello-virtual-network"></a>Verifique se o serviço de domínio do Azure Active Directory está habilitado na rede virtual Olá

Se Olá serviço de domínio do Active Directory é a rede virtual do toohello habilitado e conectado, você não pode excluir esta rede virtual. 

![Verifique o dispositivo conectado Olá](media/virtual-network-troubleshoot-cannot-delete-vnet/enable-domain-services.png)

toodisable Olá serviço, siga estas etapas:

1. Vá toohello [portal clássico do Azure](https://manage.windowsazure.com).
2. No painel esquerdo do hello, selecione **do Active Directory**.
3. Selecione o diretório de Azure Active Directory (AD do Azure) de saudação que tem o serviço de domínio do Active Directory habilitada.
4. Selecione Olá **configurar** guia.
5. Em **dos serviços de domínio**, alterar Olá **habilitar serviços de domínio para este diretório** opção muito**não**.  

### <a name="check-whether-hello-virtual-network-is-connected-tooother-resource"></a>Verificar se a rede virtual Olá é conectado tooother recursos

Verifique se há Links de Circuito, conexões e emparelhamentos de rede virtual. Qualquer um deles pode causar um toofail de exclusão de rede virtual. 

Olá ordem exclusão recomendado é o seguinte:

1. Conexões de gateway
2. Gateways
3. IPs
4. Emparelhamentos de rede virtual
5. ASE (Ambiente do Serviço de Aplicativo)

### <a name="check-whether-a-virtual-machine-is-still-running-in-hello-virtual-network"></a>Verifique se uma máquina virtual ainda está em execução na rede virtual Olá

Certifique-se de que nenhuma máquina virtual é na rede virtual hello.

### <a name="check-whether-hello-virtual-network-is-stuck-in-migration"></a>Verifique se a rede virtual hello está preso na migração

Se a rede virtual hello está preso em um estado de migração, ele não pode ser excluído. Execute Olá após a migração de saudação do comando tooabort e, em seguida, excluir a rede virtual hello.

    Move-AzureVirtualNetwork -VirtualNetworkName "Name" -Abort

## <a name="next-steps"></a>Próximas etapas

- [Rede Virtual do Azure](virtual-networks-overview.md)
- [Perguntas frequentes sobre a rede virtual do Azure (Perguntas frequentes)](virtual-networks-faq.md)