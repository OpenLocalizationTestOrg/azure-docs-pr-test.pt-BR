---
title: aaaConnect tooa VM do Windows Server | Microsoft Docs
description: "Saiba como tooconnect e fazer logon usando o tooa VM do Windows hello modelo de implantação do Azure de Gerenciador de recursos de portal e hello."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ef62b02e-bf35-468d-b4c3-71b63fe7f409
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/01/2017
ms.author: cynthn
ms.openlocfilehash: dc397f435ef165ae5af09f1d037ad3d520bb7ac3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconnect-and-log-on-tooan-azure-virtual-machine-running-windows"></a>Como tooconnect e logon tooan virtuais do Azure do computador que executa o Windows
Você usará Olá **conectar** botão Olá toostart portal do Azure uma sessão de área de trabalho remota (RDP) de uma área de trabalho do Windows. Primeiro você se conectar a máquina virtual de toohello e você fizer logon.

Se você estiver tentando tooconnect tooa VM do Windows de um Mac, você precisa tooinstall como um cliente RDP para Mac [a área de trabalho remota Microsoft](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).

## <a name="connect-toohello-virtual-machine"></a>Conecte-se a máquina virtual de toohello
1. Se você ainda não fez isso, entre no toohello [portal do Azure](https://portal.azure.com/).
2. No menu de Hub hello, clique em **máquinas virtuais**.
3. Selecione máquina virtual de Olá Olá lista.
4. Na folha de saudação para a máquina virtual de saudação, clique em **conectar**.
   
    ![Captura de tela da saudação mostrando portal do Azure como tooconnect tooyour VM.](./media/connect-logon/connect.png)
   
   > [!TIP]
   > Se hello **conectar** botão no portal de saudação está desativada e não tooAzure conectado por meio de um [rota expressa](../../expressroute/expressroute-introduction.md) ou [VPN Site a Site](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) conexão, você precisa toocreate e Atribua a VM um endereço IP público antes de usar o RDP. Leia mais sobre [endereços IP públicos no Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).
   > 
   > 

## <a name="log-on-toohello-virtual-machine"></a>Faça logon na máquina virtual de toohello
[!INCLUDE [virtual-machines-log-on-win-server](../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a>Próximas etapas
Se você tiver problemas ao tentar tooconnect, consulte [conexões de área de trabalho remota solucionar](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Este artigo orienta você no diagnóstico e na solução de problemas comuns.

