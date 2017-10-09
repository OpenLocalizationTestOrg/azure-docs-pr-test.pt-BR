---
title: "ferramentas de aaaCommunity - mover recursos clássicos tooAzure Gerenciador de recursos | Microsoft Docs"
description: "Essa ferramenta Olá catálogos de artigo que foram fornecidas pelo Olá comunidade toohelp migra recursos de IaaS do modelo de implantação do Azure Resource Manager toohello clássico."
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 228b697b-3950-49f5-84bb-283bb56621b1
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: 67d5624a14d12a2d9eb46eb12aef461b706d4589
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="community-tools-toomigrate-iaas-resources-from-classic-tooazure-resource-manager"></a>Recursos de IaaS toomigrate de tooAzure clássico Gerenciador de recursos das ferramentas de comunidade
Essa ferramenta de saudação catálogos artigo que foram fornecidas pelo Olá comunidade tooassist com a migração de recursos de IaaS de modelo de implantação do Azure Resource Manager toohello clássico.

> [!NOTE]
> Não há suporte oficial para essas ferramentas no Suporte da Microsoft. Portanto estão abertos originado no GitHub e estamos felizes tooaccept PRs para correções ou cenários adicionais. tooreport um problema, use Olá GitHub problemas de recurso.
> 
> A migração com essas ferramentas causará tempo de inatividade de sua Máquina Virtual clássica. Se você estiver buscando uma migração da plataforma com suporte, visite 
> 
>   * [Migração de plataforma com suporte de recursos de IaaS de pilha de Gerenciador de recursos de tooAzure clássico](migration-classic-resource-manager-overview.md)
>   * [Migração de clássico tooAzure Gerenciador de recursos de suporte técnico mergulho profundo na plataforma](migration-classic-resource-manager-deep-dive.md)
>   * [Migrar recursos de IaaS de clássico tooAzure Gerenciador de recursos usando o PowerShell do Azure](migration-classic-resource-manager-ps.md)
> 
> 

## <a name="asmmetadataparser"></a>AsmMetadataParser
Esta é uma coleção de ferramentas auxiliar criado como parte de migrações de empresa do gerenciamento de serviços do Azure tooAzure Gerenciador de recursos. Essa ferramenta permite que você tooreplicate sua infraestrutura em outra assinatura, que pode ser usada para teste de migração e passe problemas antes de executar a migração de saudação em sua assinatura de produção.

[Documentação da ferramenta de link toohello](https://github.com/Azure/classic-iaas-resourcemanager-migration/tree/master/AsmToArmMigrationApiToolset)

## <a name="migaz"></a>migAz
migAz é uma opção adicional de toomigrate um conjunto completo de IaaS clássico tooAzure recursos recursos de IaaS do Gerenciador de recursos. Hello migração pode ocorrer dentro de saudação mesma assinatura ou entre diferentes assinaturas e tipos de assinatura (ex: assinaturas de CSP).

[Documentação da ferramenta de link toohello](https://github.com/Azure/migAz)

## <a name="next-steps"></a>Próximas etapas

* [Visão geral da plataforma suportada migração de recursos de IaaS de tooAzure clássico Gerenciador de recursos](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Técnico mergulho profundo na plataforma suportada migração de clássico tooAzure Gerenciador de recursos](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Planejando a migração de recursos de IaaS de tooAzure clássico Gerenciador de recursos](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Usar recursos de IaaS PowerShell toomigrate de tooAzure clássico Gerenciador de recursos](migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Usar recursos de IaaS toomigrate CLI do clássico tooAzure Gerenciador de recursos](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Examinar os erros de migração mais comuns](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Saudação de revisão mais perguntas frequentes sobre migração de recursos de IaaS do clássico tooAzure Gerenciador de recursos](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

