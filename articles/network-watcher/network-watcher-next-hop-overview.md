---
title: aaaIntroduction toonext salto observador de rede do Azure | Microsoft Docs
description: "Esta página fornece uma visão geral Olá observador de rede de recurso do próximo salto"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: febf7bca-e0b7-41d5-838f-a5a40ebc5aac
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 916af736d0d52abadeafed746f0f8a0173b11033
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toonext-hop-in-azure-network-watcher"></a>Salto toonext Introdução observador de rede do Azure

O tráfego de uma VM é enviado tooa destino com base nas rotas efetiva de saudação associadas a uma NIC. Próximo salto obtém o tipo de próximo salto hello e endereço IP de um pacote de uma máquina virtual específica e a NIC. Isso ajuda a toodetermine se hello pacote está sendo direcionado toohello destino ou é holed de tráfego Olá sendo preto. Uma configuração incorreta de rotas por usuário hello, onde um tráfego é direcionado tooan no local ou um dispositivo virtual, pode levar a problemas de tooconnectivity. Próximo salto também retorna a tabela de rotas Olá associada próximo salto de saudação. Ao consultar um próximo salto se rota de saudação é definida como uma rota definida pelo usuário, essa rota será retornada. Caso contrário, o Próximo salto retornará a "Rota do Sistema".

![visão geral do próximo salto][1]

a seguir Olá é uma lista de saudação tipos de próximo salto que podem ser retornados ao consultar o próximo salto.

* Internet
* VirtualAppliance
* VirtualNetworkGateway
* VnetLocal
* HyperNetGateway
* VnetPeering
* Nenhum

### <a name="next-steps"></a>Próximas etapas

Saiba como toouse próximo salto toofind problemas de conectividade de rede visitando [seleção Olá próximo salto em uma máquina virtual](network-watcher-check-next-hop-portal.md)

<!--Image references-->
[1]: ./media/network-watcher-next-hop-overview/figure1.png













