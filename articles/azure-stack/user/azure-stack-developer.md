---
title: Desenvolver aplicativos para a pilha do Azure | Microsoft Docs
description: "Saiba mais considerações sobre desenvolvimento de aplicativos de protótipo na pilha do Azure"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: d3ebc6b1-0ffe-4d3e-ba4a-388239d6cdc3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/25/2017
ms.author: helaw
ms.openlocfilehash: 062c17173f87eec8e0eaa3f74323cbf8a8f48571
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/11/2017
---
# <a name="develop-for-azure-stack"></a>Desenvolver para o Azure Stack
Você pode começar a desenvolver aplicativos hoje em dia, mesmo se você não tiver acesso a um ambiente de pilha do Azure. Porque a pilha do Azure fornece os serviços do Microsoft Azure que são executados em seu data center, você pode usar os processos e ferramentas semelhantes para desenvolver em relação a pilha do Azure, como você faria com o Azure.  Com um pouco de preparação e a orientação dos tópicos a seguir, você pode usar o Azure para emular um ambiente de pilha do Azure:

* No Azure, você pode criar modelos de Gerenciador de recursos do Azure que também são passíveis de implantação para a pilha do Azure.  Consulte [considerações sobre o modelo](azure-stack-develop-templates.md) para obter orientação sobre como desenvolver seus modelos para garantir a portabilidade.
* Há uma diferença em disponibilidade do serviço e controle de versão do serviço entre o Azure e a pilha do Azure. Você pode usar o [módulo de política do Azure pilha](azure-stack-policy-module.md) para restringir os tipos de recursos e disponibilidade do serviço do Azure a que está disponível na pilha do Azure. Restringir serviços disponíveis ajudarão seu aplicativo depende de serviços disponíveis para a pilha do Azure.
* O [modelos de início rápido do Azure pilha](https://github.com/Azure/AzureStack-QuickStart-Templates) são exemplos de cenários comuns de como desenvolver seus modelos para que eles possam ser implantados para o Azure e a pilha do Azure.


