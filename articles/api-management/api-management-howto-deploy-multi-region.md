---
title: "aaaDeploy gerenciamento de API do Azure services toomultiple Azure regiões | Microsoft Docs"
description: "Saiba como toodeploy um gerenciamento de API do Azure serviço instância toomultiple Azure regiões."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 47389ad6-f865-4706-833f-846115e22e4d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 04a3e762261237d73a769320a21363f99f1d20cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-an-azure-api-management-service-instance-toomultiple-azure-regions"></a>Como toodeploy um gerenciamento de API do Azure serviço instância toomultiple Azure regiões
Gerenciamento de API dá suporte à implantação de várias regiões, que permite que a API editores toodistribute um único serviço de gerenciamento de API em qualquer número de regiões do Azure desejados. Isso ajuda a reduzir a solicitação de latência percebida pelos consumidores de API distribuídos geograficamente e também melhora a disponibilidade do serviço se uma região ficar offline. 

Quando um serviço de gerenciamento de API é criado inicialmente, ele contém apenas um [unidade] [ unit] e reside em uma única região do Azure, que é designada como Olá região primária. Regiões adicionais podem ser adicionados facilmente por meio de saudação Portal do Azure. Um servidor de gateway de gerenciamento de API é implantado tooeach região e tráfego de chamada será gateway mais próximo toohello roteadas. Se uma região de ficar offline, o tráfego de saudação é automaticamente redirecionada toohello próximo gateway mais próximo. 

> [!IMPORTANT]
> Implantação de várias regiões só está disponível no hello  **[Premium] [ Premium]**  camada.
> 
> 

## <a name="add-region"></a>Implantar uma API de gerenciamento serviço instância tooa nova região
> [!NOTE]
> Se você ainda não tiver criado uma instância do serviço de gerenciamento de API, consulte [criar uma instância do serviço de gerenciamento de API] [ Create an API Management service instance] em Olá [Introdução ao gerenciamento de API do Azure] [ Get started with Azure API Management] tutorial.
> 
> 

No hello Portal do Azure, navegue toohello **escala e preços** página da sua instância do serviço de gerenciamento de API. 

![Guia Escala][api-management-scale-service]

toodeploy tooa nova região, clique em **+ adicionar região** na barra de ferramentas de saudação.

![Adicionar região][api-management-add-region]

Selecione o local de saudação da lista suspensa de saudação e definir Olá número de unidades para o com o controle deslizante de saudação.

![Especificar unidades][api-management-select-location-units]

Clique em **adicionar** tooplace sua seleção na tabela de locais de saudação. 

Repita esse processo até que todos os locais configurados e clique em **salvar** do processo de implantação do hello barra de ferramentas toostart hello.

## <a name="remove-region"> </a>Excluir uma instância do serviço de Gerenciamento de API de um local
No hello Portal do Azure, navegue toohello **escala e preços** página da sua instância do serviço de gerenciamento de API. 

![Guia Escala][api-management-scale-service]

Para o local de saudação você gostaria que tooremove abrir menu de contexto de saudação usando Olá **...**  botão na direita da tabela Olá Olá. Selecione Olá **excluir** opção.

![Remover região][api-management-remove-region]

Confirmar exclusão de saudação e clique em **salvar** tooapply alterações de saudação.

[api-management-management-console]: ./media/api-management-howto-deploy-multi-region/api-management-management-console.png

[api-management-scale-service]: ./media/api-management-howto-deploy-multi-region/api-management-scale-service.png
[api-management-add-region]: ./media/api-management-howto-deploy-multi-region/api-management-add-region.png
[api-management-select-location-units]: ./media/api-management-howto-deploy-multi-region/api-management-select-location-units.png
[api-management-remove-region]: ./media/api-management-howto-deploy-multi-region/api-management-remove-region.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Get started with Azure API Management]: api-management-get-started.md

[Deploy an API Management service instance tooa new region]: #add-region
[Delete an API Management service instance from a region]: #remove-region

[unit]: http://azure.microsoft.com/pricing/details/api-management/
[Premium]: http://azure.microsoft.com/pricing/details/api-management/

