---
title: Recursos do aplicativo Web de aaaMove tooanother grupo de recursos
description: "Descreve os cenários de saudação onde você pode mover os aplicativos Web e serviços de aplicativos de tooanother de um grupo de recursos."
services: app-service
documentationcenter: 
author: ZainRizvi
manager: erikre
editor: 
ms.assetid: 22f97607-072e-4d1f-a46f-8d500420c33c
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: zarizvi
ms.openlocfilehash: 931012fee656b7f8a4b2c225c38739a9171d3b2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="supported-move-configurations"></a>Configurações de movimentação com suporte
Você pode mover os recursos de aplicativo Web do Azure usando Olá [Resource Manager mover recursos API](../azure-resource-manager/resource-group-move-resources.md).

Os aplicativos Web do Azure atualmente suporta os seguintes cenários de movimentação de saudação:

* Mover todo o conteúdo de um grupo de recursos (aplicativos da web, planos de serviço de aplicativo e certificados) Olá tooanother grupo de recursos. 
   > [!Note]
   > grupo de recursos de destino de saudação não pode conter todos os recursos Microsoft neste cenário.

* Mova o grupo de recursos diferente tooa de aplicativos web individuais, enquanto ainda hospedando-los em seu plano de serviço de aplicativo atual (Olá aplicativo serviço plano permanece no grupo de recursos antigo Olá).


