---
title: "Análise técnica aprofundada sobre a migração com suporte da plataforma do clássico para o Azure Resource Manager | Microsoft Docs"
description: "Este artigo faz uma análise técnica detalhada sobre a migração de recursos com suporte da plataforma do clássico para o Azure Resource Manager"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 29267453-f894-4180-bb67-dce2a0e062bb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: 557a61f266c494cb6b8003cff945fa1a14348898
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/11/2017
---
# <a name="technical-deep-dive-on-platform-supported-migration-from-classic-to-azure-resource-manager"></a>Análise técnica aprofundada sobre a migração com suporte da plataforma do clássico para o Azure Resource Manager

Vamos fazer uma análise aprofundada da migração do modelo de implantação clássico do Azure para o modelo de implantação do Azure Resource Manager. Nós vamos examinar os recursos no nível da funcionalidade e do recurso para ajudá-lo a entender como a plataforma do Azure migra recursos entre os dois modelos de implantação. Para obter mais informações, leia o artigo de comunicado do serviço - [Migração de recursos de IaaS com suporte da plataforma do clássico para o Azure Resource Manager](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

[!INCLUDE [virtual-machines-common-migration-deep-dive](../../../includes/virtual-machines-common-classic-resource-manager-migration-deep-dive.md)]

## <a name="next-steps"></a>Próximas etapas

* [Visão geral da migração de recursos de IaaS com suporte da plataforma do clássico para o Azure Resource Manager](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Planejamento para a migração de recursos de IaaS do clássico para o Azure Resource Manager](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Usar o PowerShell para migrar recursos de IaaS do clássico para o Azure Resource Manager](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Usar a CLI para migrar recursos de IaaS do clássico para o Azure Resource Manager](migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Ferramentas da comunidade para ajudar com a migração de recursos de IaaS do clássico para o Azure Resource Manager](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Examinar os erros de migração mais comuns](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Confira as perguntas mais frequentes sobre a migração de recursos de IaaS do clássico para o Azure Resource Manager](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
