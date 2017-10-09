---
title: aaaSupportability de Adicionar conjunto de disponibilidade existente tooan VMs do Azure | Microsoft Docs
description: "Suporte de adição de VMs do Azure tooan conjunto de disponibilidade existente."
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
ms.assetid: 
ms.service: virtual-machines
ms.workload: virtual-machines
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/15/2017
ms.author: delhan
ms.openlocfilehash: dc2bd86b916f1d1a0a0d4c9e870df829434c96b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="supportability-of-adding-azure-vms-tooan-existing-availability-set"></a>Suporte de adição de VMs do Azure tooan conjunto de disponibilidade existente

Ocasionalmente, você poderá encontrar limitações quando você adicionar novas máquinas virtuais (VMs) tooan conjunto de disponibilidade existente. Olá que série VM, você pode combinar em Olá mesmo conjunto de disponibilidade de detalhes de gráfico a seguir.

Aqui está o hello suporte matriz toomix diferentes tipos de máquinas virtuais:

Série e conjunto de disponibilidade|Segunda VM|O |Av2|D|Dv2|Dv3|
|---|---|---|---|---|---|---|
|Primeira VM|||||||
|O ||OK|OK|OK|OK|OK|
|Av2||OK|OK|OK|OK|OK|
|D||OK|OK|OK|OK|OK|
|Dv2||OK|OK|OK|OK|OK|
|Dv3||OK|OK|OK|OK|OK|

Todas as outras séries não podem estar em Olá conjunto de disponibilidade mesmo porque eles exigem um hardware específico.
