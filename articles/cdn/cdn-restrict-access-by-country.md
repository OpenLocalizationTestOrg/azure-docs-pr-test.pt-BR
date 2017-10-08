---
title: "aaaRestrict conteúdo da CDN do Azure por país | Microsoft Docs"
description: "Saiba como toorestrict acesso tooyour Azure CDN conteúdo usando Olá recurso filtragem de replicação geográfica."
services: cdn
documentationcenter: 
author: lichard
manager: akucer
editor: 
ms.assetid: 12c17cc5-28ee-4b0b-ba22-2266be2e786a
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: ffdd994612b6c9cfbf1a6e29d260709b4afa86e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="restrict-azure-cdn-content-by-country"></a>Restringir conteúdo da CDN do Azure por país

## <a name="overview"></a>Visão geral
Quando um usuário solicita o conteúdo, por padrão, o conteúdo de saudação é atendido, independentemente de onde o usuário Olá feita essa solicitação de. Em alguns casos, convém toorestrict acessar o conteúdo de tooyour por país. Este tópico explica como Olá toouse **filtragem geográfica** recurso na ordem tooconfigure Olá tooallow ou bloquear acesso ao serviço por país.

> [!IMPORTANT]
> produtos de Verizon e Akamai Olá fornecem Olá a mesma funcionalidade de filtragem de replicação geográfica, mas tem uma pequena diferença na códigos de país te dão suporte. Consulte a etapa 3 para diferenças de toohello um link.


Para obter informações sobre as considerações que se aplicam a tooconfiguring esse tipo de restrição, consulte Olá [considerações](cdn-restrict-access-by-country.md#considerations) seção final Olá Olá tópico.  

![Filtragem de País](./media/cdn-filtering/cdn-country-filtering-akamai.png)

## <a name="step-1-define-hello-directory-path"></a>Etapa 1: Definir o caminho do diretório Olá
Selecione o ponto de extremidade no portal de saudação e Olá filtragem geográfica guia Olá toofind de navegação à esquerda para acessar esse recurso.

Ao configurar um filtro de país, você deve especificar os usuários do hello caminho relativo toohello local toowhich serão permitidos ou negados o acesso. Você pode aplicar a filtragem geográfica para todos os arquivos com "/" ou pastas selecionadas, especificando os caminhos de diretório "/pictures/". Você também pode aplicar a filtragem geográfica tooa arquivo único, especificando o arquivo hello e omitindo Olá barra "/ imagens/cidade.png".

Filtro de caminho do diretório de exemplo:

    /                                 
    /Photos/
    /Photos/Strasbourg/
      /Photos/Strasbourg/city.png

## <a name="step-2-define-hello-action-block-or-allow"></a>Etapa 2: Definir a ação de saudação: bloquear ou permitir
**Bloquear:** usuários de saudação especificaram países serão negadas acesso tooassets solicitada pelo caminho recursiva. Se nenhuma outra opção de filtragem de país tiver sido configurada para esse local, então, todos os outros usuários terão acesso permitido.

**Permitir:** apenas os usuários de saudação especificaram países poderão ser tooassets de acesso solicitado do caminho recursiva.

## <a name="step-3-define-hello-countries"></a>Etapa 3: Definir países Olá
Selecione Olá países que você deseja tooblock ou permitir para o caminho de saudação. 

Por exemplo, a regra de saudação do bloqueio /Photos/Strasbourg/filtrará arquivos, incluindo:

    http://<endpoint>.azureedge.net/Photos/Strasbourg/1000.jpg
    http://<endpoint>.azureedge.net/Photos/Strasbourg/Cathedral/1000.jpg


### <a name="country-codes"></a>Códigos de país
Olá **filtragem geográfica** recurso usa países país códigos toodefine saudação do qual uma solicitação será permitida ou bloqueada para um diretório protegido. Você encontrará Olá códigos de país de [códigos de país do Azure CDN](https://msdn.microsoft.com/library/mt761717.aspx). 

## <a id="considerations"></a>Considerações
* Pode levar até too90 minutos Verizon ou alguns minutos com Akamai, para efeito de tootake do alterações tooyour país filtragem configuração.
* Esse recurso não oferece suporte a caracteres curinga (por exemplo, ‘*’).
* configuração de filtragem geográfica Olá associada com o caminho relativo da saudação será aplicadas recursivamente toothat caminho.
* Somente uma regra pode ser aplicada toohello mesmo caminho relativo (não é possível criar vários filtros de país que toohello ponto mesmo caminho relativo. No entanto, uma pasta pode ter vários filtros de país. Isso é devido a natureza de recursiva toohello de filtros de país. Em outras palavras, uma subpasta de uma pasta configurada anteriormente pode ter um filtro de país diferente atribuído.

