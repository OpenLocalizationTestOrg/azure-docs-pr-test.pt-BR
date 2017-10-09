---
title: tootopology aaaIntroduction no Inspetor de rede do Azure | Microsoft Docs
description: "Esta página fornece uma visão geral dos recursos de topologia de rede Inspetor Olá"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e753a435-38e0-482b-846b-121cb547555c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 7fa1c5518e4a25a5db999d898a9ee19fd0121db7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tootopology-in-azure-network-watcher"></a>Introdução tootopology no Inspetor de rede do Azure

A topologia retorna um gráfico de recursos de rede em uma rede virtual. gráfico de saudação mostra interconexão de saudação entre Olá recursos toorepresent Olá final tooend a conectividade de rede.

![visão geral da topologia][1]

No portal de saudação topologia retorna objetos de recurso de saudação em um acordo de rede virtual. relações de saudação estão representadas por linhas entre recursos Olá recursos fora da região do observador de rede hello, mesmo que no recurso Olá o grupo não será exibido. recursos Olá retornados na exibição de portal Olá são um subconjunto Olá de componentes de rede que são mostrados. lista completa de saudação de toosee de recursos de rede que você pode usar [PowerShell](network-watcher-topology-powershell.md) ou [REST](network-watcher-topology-rest.md)

> [!NOTE]
> Uma instância do observador de rede é necessária em cada região que você deseja toorun topologia na.

Como recursos são retornados conexão Olá entre eles são modeladas em duas relações.

- **Confinamento** - Exemplo: uma rede virtual contém uma sub-rede que contém uma NIC
- **Associados** - Exemplo: uma NIC está associada a uma VM

### <a name="next-steps"></a>Próximas etapas

Saiba como toouse PowerShell tooretrieve Olá topologia exibir visitando [topologia do observador de rede com o PowerShell](network-watcher-topology-powershell.md)

<!--Image references-->

[1]: ./media/network-watcher-topology-overview/topology.png
