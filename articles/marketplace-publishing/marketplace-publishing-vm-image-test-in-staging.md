---
title: "aaaTest sua VM oferecem para Olá Marketplace | Microsoft Docs"
description: Entenda como tootest sua VM da imagem para hello Azure Marketplace.
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 7a41c3c6-625c-4478-b804-e124dee89040
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: hascipio
ms.openlocfilehash: ab166d2c3c536810a3a8f48330f0482b9b4e58d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="test-your-vm-offer-for-hello-azure-marketplace-in-staging"></a>Testar sua oferta VM para hello Azure Marketplace em preparo
Significa o SKU em uma "área restrita" onde você pode testar e validar sua funcionalidade antes de implantá-la toohello Marketplace particular de distribuição de preparo. Olá SKU aparece no preparo como faria cliente tooa que implantou a ele. A imagem VM deve ser toostaging toobe certificados enviada por push.

## <a name="step-1-push-your-offer-toostaging"></a>Etapa 1: Push toostaging sua oferta
1. Em Olá **publicar** , clique em **Push tooStaging**.
   
    ![desenho](media/marketplace-publishing-vm-image-test-in-staging/vm-image-push-to-staging.png)
2. Se Olá Portal de publicação notifica sobre erros, corrija-os.
3. Em Olá **quem pode acessar sua oferta preparada?** caixa de diálogo caixa, digite Olá lista de assinaturas do Azure que você usará toopreview sua oferta Olá [portal de visualização do Azure](https://portal.azure.com).
   
   > [!NOTE]
   > No caso de Máquinas Virtuais e modelos de Solução, **não** coloque em lista de branca assinaturas do tipo CSP, DreamSpark ou Azure via Open.
   > 
   > 

    > No caso de máquinas virtuais, quando você clica no botão Olá **tooSTAGING PUSH**, Olá etapas a seguir é executada por trás da cena hello. Você será tooview capaz de andamento de saudação de cada etapa na guia publicação Olá Olá portal de publicação. Você deve verificar essa página em intervalos regulares (até o status de saudação mostra teste) para obter quaisquer informações de falha que precisam de correção do seu final.

    > - No primeiro sua solicitação de preparo vai toohello equipe de certificação que validar Olá vhd. No entanto, se sua solicitação tem somente alterações de marketing, em seguida, Olá certificação etapa será ignorada.
    > - Após a conclusão da certificação Olá, a replicação inicial de oferta Olá em todos os Olá datacenters do Azure. Ele geralmente leva 24-48hours para Olá replicação toocomplete mas pode levar até semana tooa dependendo do tamanho de saudação do vhd de saudação. No entanto, se sua solicitação tem somente alterações de marketing, replicação de saudação é mais rápida.
    > - Quando Olá replicação for concluída, em seguida, oferta Olá estará disponível no hello [portal do Azure](http:/portal.azure.com). Em que Olá tempo status se tornar testados no hello portal de publicação. Uma oferta de preparada está visível no hello [portal do Azure](http:/portal.azure.com) usando apenas Olá identificações de email associadas à assinatura Olá preparada com quais Olá oferta.

1. Entrar toohello [portal de visualização do Azure](https://portal.azure.com) usando uma saudação assinaturas do Azure listadas na etapa anterior hello.
2. Encontre sua oferta e valide seus pontos de imagem VM:
   
   * Certifique-se de que conteúdo de marketing exibida corretamente no hello Marketplace.
   * Implantação de ponta a ponta da imagem VM hello.
     
      ![img-map-portal](media/marketplace-publishing-push-to-staging/pubportal-mapping-azure-portal.jpg)

> [!IMPORTANT]
> Sua oferta permanecem no preparo até que você notificar a Microsoft por meio do Portal de publicação de saudação [**publicar** guia > clique no botão de saudação **"Solicitar aprovação tooPush tooProduction"**] que você está pronto toopush tooproduction. Este é um toohave tempo ideal que verificar todos os membros da equipe sobre tudo em preparação para a sua oferta vai listados.
> 
> Olá plataforma de preparo foi projetado para teste oferta Olá em um modo de visualização, publisher Olá. É enfaticamente desaconselhável usar essa plataforma para fins comerciais.
> 
> 

## <a name="next-steps"></a>Próximas etapas
Agora que sua oferta "preparada" e testar sua funcionalidade e conteúdo de marketing, você poderá publicar final toohello fase, **etapa 4**: [Implantando toohello sua oferta Marketplace](marketplace-publishing-push-to-production.md).

## <a name="see-also"></a>Consulte também
* [Guia de Introdução: como toopublish toohello uma oferta do Azure Marketplace](marketplace-publishing-getting-started.md)

