---
title: "aaaGuide toocreating um modelo de solução para Olá Marketplace | Microsoft Docs"
description: "Instruções detalhadas de como toocreate, certificar e implantar um modelo de solução de imagem de várias VMs para compra em hello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e14e05f2-2385-4ce0-b351-0747cb74ba19
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: b0e7067176337dd0d3f6f6ec04c963f80f706ab0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="guide-toocreate-a-solution-template-for-azure-marketplace"></a>Guia toocreate um modelo de solução para o Azure Marketplace
Depois de concluir a etapa 1, [criação de conta e registro][link-acct-creation], podemos guiada por você na criação de saudação de um modelo de solução compatível com o Azure em [pré-requisitos técnicos para a criação de um modelo de solução](marketplace-publishing-solution-template-creation-prerequisites.md). Agora podemos irá orientá-lo pelas etapas de saudação para criar um modelo de solução para várias VMs Olá [Portal de publicação] [ link-pubportal] para hello Azure Marketplace.

## <a name="create-your-solution-template-offer-in-hello-publishing-portal"></a>Criar sua oferta de modelo de solução em Olá Portal de publicação
Vá muito [https://publish.windowsazure.com](http://publish.windowsazure.com). Ao entrar para Olá primeiro tempo toohello [Portal de publicação](https://publish.windowsazure.com/), use Olá mesma conta com o perfil de vendedor da sua empresa que foi registrado. Posteriormente, você pode adicionar qualquer funcionário da sua empresa como um administrador de co Olá Portal de publicação.

### <a name="1-select-solution-templates"></a>1. Selecione "Modelos de solução"
  ![desenho][img-pubportal-menu-sol-templ]

### <a name="2-create-a-new-solution-template"></a>2. Crie um novo modelo de solução
  ![desenho][img-pubportal-sol-templ-new]

### <a name="3-start-with-topologies"></a>3. Comece com as topologias
Um modelo de solução é um tooall "pai" de suas topologias. Você pode definir várias topologias em uma oferta/modelo de solução. Quando uma oferta é impulsionada toostaging, ela é enviada por push com todas as suas topologias de. Siga as etapas de saudação abaixo toodefine sua oferta:     

* Crie uma topologia: "Identificador de topologia" normalmente é nome de saudação da topologia Olá para o modelo de solução de saudação. Identificador da topologia de saudação é usado na URL de hello, conforme mostrado abaixo:

  Azure Marketplace: http://azure.microsoft.com/marketplace/partners/{PublisherNamespace}/{OfferIdentifier}{TopologyIdentifier}

  Portal do Azure: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{TopologyIdentifier}
* Adicionar uma nova versão.

### <a name="4-get-your-topology-versions-certified"></a>4. Certifique as versões de sua topologia
Carregar um arquivo zip que contém essa versão específica da topologia de saudação de tooprovision de todos os arquivos necessários. O arquivo zip deve conter o seguinte hello:

* Arquivo *mainTemplate.json* e *createUiDefinition.json* no diretório raiz.
* Quaisquer modelos vinculados e todos os scripts necessários.

  > [!TIP]
  > Enquanto os desenvolvedores de trabalho sobre a criação de solução Olá topologias de modelo e recuperá-las certificados, negócios Olá, departamentos de marketing e/ou legais da sua empresa podem trabalhar no conteúdo de marketing e legal de saudação.
  >
  >

## <a name="next-steps"></a>Próximas etapas
Agora que você criou o modelo de solução e carregado o arquivo zip de hello, siga as instruções de Olá Olá [guia de conteúdo de marketing do Marketplace](marketplace-publishing-push-to-staging.md) antes de enviar Olá oferta toostaging. conjunto completo de toosee saudação do marketplace publicando artigos, visite [guia de Introdução: como toopublish toohello uma oferta do Azure Marketplace](marketplace-publishing-getting-started.md).

Você também pode se interessar por estes artigos relacionados:

* Imagens de VM: [Sobre Imagens da Máquina Virtual no Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)
* Extensões de VM: [Visão geral sobre Agente de VM](https://msdn.microsoft.com/library/azure/dn832621.aspx) e [Extensões de VM e Extensões de VM e recursos do Azure](https://msdn.microsoft.com/library/azure/dn606311.aspx)
* Azure Resource Manager: [Criando modelos do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) e [Exemplos de modelos simples](https://github.com/rjmax/ArmExamples)
* Conta de armazenamento limita: [como tooMonitor limitação da conta de armazenamento de](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) e [armazenamento Premium](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)

[img-pubportal-menu-sol-templ]:media/marketplace-publishing-solution-template-creation/pubportal-menu-solution-templates.png
[img-pubportal-sol-templ-new]:media/marketplace-publishing-solution-template-creation/pubportal-solution-template-new.png
[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
[link-pubportal]:https://publish.windowsazure.com
