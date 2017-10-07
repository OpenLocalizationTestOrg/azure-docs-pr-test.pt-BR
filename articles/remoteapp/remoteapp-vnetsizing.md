---
title: "informações de aaaSizing para uma rede virtual no Azure RemoteApp | Microsoft Docs"
description: "Saiba mais sobre os requisitos de endereço IP da saudação do Azure RemoteApp em execução com uma rede virtual"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b6e1c4ba-0236-42b2-bced-69353bf211be
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: f98b831af32c41740b258d122b3e18765be08d97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sizing-information-for-a-vnet-in-azure-remoteapp"></a>Dimensionamento de informações de um VNET no RemoteApp do Azure
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

Quando você usa o Azure RemoteApp com uma rede virtual (VNET), o RemoteApp usa endereços IP de sub-rede hello. Com base em escala de saudação do seu serviço RemoteApp, é necessário tooensure sua sub-rede tem endereços IP suficientes disponíveis para máquinas virtuais de RemoteApp. Embora essa orientação de dimensionamento não seja perfeita, visto o modo como o RemoteApp faz a rotação dinâmica de máquinas virtuais para cima e para baixo dentro de uma coleção, ele ajudará a calcular o intervalo de sub-rede. Isso é especialmente importante que, quando um serviço do RemoteApp é colocado em uma rede virtual, não é possível aumentar o tamanho da sub-rede Olá sem remover o RemoteApp.

Para cada coleção do RemoteApp que você deseja toorun na capacidade máxima, você deve ter 100 endereços IP disponíveis. Por exemplo, se você tiver uma coleção do RemoteApp no plano de saudação padrão e deseja toohave Olá máximo 500 usuários, você deve ter 100 endereços IP para essa coleção. Da mesma forma, você precisa 100 endereços IP para uma coleção do RemoteApp no plano básico de saudação com 800 usuários. Se você planejar toohave menos usuários (menor que o máximo de saudação), você pode reduzir a endereços IP hello necessários por coleção. requisito de tamanho mínimo de sub-rede Olá é 30 endereços IP (/ 27).

Check-out Olá seguindo informações toomake-se de que sua rede virtual está configurada e funcionando propertly:

* [Migrar de uma tooan de rede virtual pessoal VNET do Azure](remoteapp-migratevnet.md)
* [Validar Olá toouse de rede virtual do Azure com o Azure RemoteApp](remoteapp-vnet.md)

