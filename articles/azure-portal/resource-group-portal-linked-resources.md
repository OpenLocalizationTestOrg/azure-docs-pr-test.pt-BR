---
title: "Galeria de bloco aaaRelated e recursos vinculados em Olá"
description: "Saiba mais sobre recursos relacionados e vinculados que são exibidos na Galeria de bloco de saudação do portal de visualização do Azure hello."
services: azure-portal
documentationcenter: 
author: adamabdelhamed
manager: wpickett
editor: 
ms.assetid: dba96d29-f518-49c8-bfd2-f14cecb44cbf
ms.service: azure-portal
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/16/2015
ms.author: adamab
ms.openlocfilehash: c8f99be8e23dc9641ec3cd3169604b33a4b049f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="related-and-linked-resources-in-hello-tile-gallery"></a>Recursos relacionados e vinculados na Galeria de bloco Olá
Galeria de bloco Olá permite toofind blocos para um recurso específico e arraste-os para a folha atual. Usando a Galeria de bloco hello, você pode criar exibições de gerenciamento que abrangem recursos. Para qualquer recurso especificado, Olá relacionadas a recursos incluem todos os recursos de saudação em seu grupo de recursos e todos os recursos que vinculam tooor do recurso de saudação.

## <a name="linked-resources-in-resource-manager"></a>Recursos vinculados no Resource Manager
Vinculando é um recurso do hello Gerenciador de recursos.  Isso permite que você toodeclare relações entre os recursos mesmo se eles não estão no hello mesmo grupo de recursos. Vinculação não tem impacto no tempo de execução de saudação de seus recursos, sem afetar a cobrança e nenhum impacto sobre o acesso baseado em função.  Ele é simplesmente um mecanismo que você pode usar toorepresent relações para que a experiência de ferramentas, como a Galeria de bloco Olá pode fornecer um gerenciamento avançado.  As ferramentas podem inspecionar links hello usando links Olá API e fornecer experiências de gerenciamento de relacionamento personalizado também. 

## <a name="how-do-i-link-my-resources"></a>Como vinculo meus recursos?
Quando você criar recursos por meio do portal hello ou implantando um modelo por meio do Azure PowerShell ou CLI do Azure, os links são criados automaticamente para alguns recursos dependentes. Você pode vincular também programaticamente os recursos usando Olá [API de REST de recursos vinculados](/rest/api/resources/resourcelinks).

## <a name="next-steps"></a>Próximas etapas
* Se você precisar de uma introdução toowriting recurso Gerenciador de modelos, consulte [criar modelos](../azure-resource-manager/resource-group-authoring-templates.md).
* toounderstand mais sobre como trabalhar com grupos de recursos por meio do portal hello, consulte [usando os recursos do Azure de toomanage portal do Azure Olá](../azure-resource-manager/resource-group-portal.md).

