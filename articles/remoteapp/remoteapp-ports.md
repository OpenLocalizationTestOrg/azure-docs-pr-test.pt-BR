---
title: aaaList de toowhitelist URLs e portas para o Azure RemoteApp implantado na rede virtual do cliente | Microsoft Docs
description: "Saiba quais portas e URLs, você precisará tooconfigure para comunicação por meio do Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: mghosh1616
manager: mbaldwin
ms.assetid: 5a001ff7-14c9-47fa-9b39-78fd5a5f0250
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 039866f7b64ac763ca833d66031ade3def1d3543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="list-of-ports-and-urls-toopermit-access-for-azure-remoteapp-deployed-in-customer-virtual-network"></a>Lista de URLs e portas de acesso de toopermit para o Azure RemoteApp implantado no cliente de rede Virtual
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

Se você estiver implantando uma coleção de nuvem ou híbrida do RemoteApp do Azure em uma rede virtual (VNET), examine Olá informações de porta a seguir. Para obter mais informações sobre redes virtuais, consulte [Visão Geral da Rede Virtual](../virtual-network/virtual-networks-overview.md). Se você tiver criado um grupo de segurança de rede (NSG) restringindo os recursos de rede virtual do tráfego toohello em sua coleção, certifique-se de saudação portas a seguir é permitidas por meio de políticas de segurança de saudação na rede virtual hello e acessível. Para obter mais informações sobre grupos de segurança de rede, consulte [O que é um Grupo de Segurança de Rede? (NSG)](../virtual-network/virtual-networks-nsg.md).

## <a name="azure-remoteapp-subnet-needs-access-toothese-endpoints-and-urls"></a>Sub-rede RemoteApp do Azure precisa de pontos de extremidade do acesso toothese e URLs:
* *.servicebus.windows.net
* *.servicebus.net
* https://*.remoteapp.windowsazure.com  
* https://www.remoteapp.windowsazure.com 
* https://*remoteapp.windowsazure.com  
* https://*.core.windows.net  
* Saída: TCP: TCP: 443, 9351, 9352, 10101-10175 
* Opcional – UDP: 10201-10275  

## <a name="azure-remoteapp-clients-need-access-toothese-endpoints-and-urls"></a>Clientes do RemoteApp do Azure precisam acessar pontos de extremidade de toothese e URLs:
Por clientes que quero dizer Olá desktops, dispositivos etc. que as pessoas use tooconnect toohello aplicativos implantados em Olá coleção do RemoteApp do Azure.

* https://telemetry.remoteapp.windowsazure.com  
* https://*.RemoteApp.WindowsAzure.com (portas UDP opcionais de saudação são para esse endereço) 
* https://login.windows.net  
* https://login.microsoftonline.com  
* https://www.remoteapp.windowsazure.com 
* https://*.core.windows.net  
* Saída: TCP: 443  
* Opcional - UDP: 3391 

