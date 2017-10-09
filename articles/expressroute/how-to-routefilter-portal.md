---
title: 'Configurar os filtros de rota para o emparelhamento da Microsoft do Azure ExpressRoute: Portal | Microsoft Docs'
description: "Este artigo descreve como os filtros de rota tooconfigure para usar o Microsoft Peering Olá portal do Azure"
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/25/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 2a47d465ec5f175d9510cef94606f70f036f0862
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-route-filters-for-microsoft-peering"></a>Configurar os filtros de rota para o emparelhamento da Microsoft

Filtros de rota são uma maneira tooconsume um subconjunto de serviços com suporte por meio de emparelhamento da Microsoft. Olá etapas nesta ajuda de artigo, configurar e gerenciar filtros de rotas para circuitos do ExpressRoute.

Dynamics 365 serviços e serviços do Office 365, como o Exchange Online, SharePoint Online e Skype for Business, são acessíveis por meio de emparelhamento da Microsoft hello. Quando emparelhamento da Microsoft é configurado em um circuito de rota expressa, todos os serviços de toothese relacionados prefixos são anunciados através de sessões BGP Olá estabelecidas. Um valor de comunidade BGP é anexado tooevery prefixo tooidentify Olá serviço oferecido por meio de prefixo hello. Para obter uma lista de valores de comunidade BGP hello e serviços de saudação são mapeados para, consulte [comunidades BGP](expressroute-routing.md#bgp).

Se você precisar de serviços de conectividade do tooall, um grande número de prefixos é anunciado através do BGP. Isso aumenta consideravelmente o tamanho Olá Olá de tabelas de rotas mantida por roteadores na rede. Se você planejar tooconsume apenas um subconjunto de serviços oferecido por meio de emparelhamento da Microsoft, você pode reduzir o tamanho de saudação de suas tabelas de rota de duas maneiras. Você pode:

- Filtre prefixos indesejados aplicando filtros de rota nas comunidades do BGP. Essa é uma prática de rede padrão e é usada frequentemente em várias redes.

- Definir filtros de rota e aplicá-las tooyour circuito de rota expressa. Um filtro de rota é um novo recurso que permite que você selecione lista de saudação de serviços que você planeje tooconsume por meio de emparelhamento da Microsoft. Roteadores de rota expressa somente enviam a lista de saudação de prefixos que pertencem a serviços toohello identificados no filtro de rota hello.

### <a name="about"></a>Sobre filtros de rota

Quando o emparelhamento da Microsoft é configurado no seu circuito de rota expressa, roteadores de borda Microsoft hello estabelecerem um par de sessões BGP com roteadores de borda da saudação (seu ou seu provedor de conectividade). Nenhuma rota é rede tooyour anunciado. rede de tooyour de anúncios de rota tooenable, você deve associar um filtro de rota.

Um filtro de roteamento permite identificar os serviços que você deseja tooconsume por meio de emparelhamento da Microsoft do seu circuito de rota expressa. É essencialmente uma lista de permissões de todos os valores de comunidade BGP hello. Quando o recurso de filtro de rota é definido e anexado tooan circuito de rota expressa, todos os prefixos que mapeiam valores de comunidade BGP toohello são rede tooyour anunciado.

toobe tooattach capaz de filtros de rota com serviços do Office 365 neles, você deve ter serviços do Office 365 tooconsume autorização por meio de rota expressa. Se você não estiver autorizado tooconsume Office 365 services por meio de rota expressa, filtros de rota Olá operação tooattach falhará. Para obter mais informações sobre o processo de autorização hello, consulte [rota expressa do Azure para o Office 365](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd). Os serviços de conectividade tooDynamics 365 não requer nenhuma autorização anterior.

> [!IMPORTANT]
> Emparelhamento da Microsoft de circuitos ExpressRoute que foram configurados anterior tooAugust 1, 2017 terá todos os prefixos de serviço anunciados através do emparelhamento da Microsoft, mesmo se os filtros de roteamento não estão definidos. Emparelhamento da Microsoft de circuitos de rota expressa configurados em ou após 1 de agosto de 2017 não terá quaisquer prefixos anunciados até que um filtro de rota é anexado toohello circuito.
> 
> 

### <a name="workflow"></a>Fluxo de trabalho

toosuccessfully de toobe capaz de se conectar a tooservices por meio de emparelhamento da Microsoft, você deve concluir Olá etapas de configuração a seguir:

- Você deve ter um circuito de ExpressRoute ativado que tenha o Microsoft emparelhamento provisionado. Você pode usar o hello tooaccomplish instruções a seguir estas tarefas:
  - [Criar um circuito de rota expressa](expressroute-howto-circuit-portal-resource-manager.md) e ter o circuito Olá habilitado por seu provedor de conectividade antes de continuar. Olá circuito de rota expressa deve estar em um estado habilitado e configurado.
  - [Criar emparelhamento da Microsoft](expressroute-howto-routing-portal-resource-manager.md) se você gerenciar sessões de BGP de saudação diretamente. Ou então, faça com que seu provedor de conectividade provisione emparelhamento da Microsoft para o circuito.

-  Você deve criar e configurar um filtro de rota.
    - Identificar Olá serviços tooconsume por meio de emparelhamento da Microsoft
    - Identificar Olá lista de valores de comunidade BGP associados aos serviços de saudação
    - Criar uma regra tooallow Olá prefixo lista correspondente Olá valores de comunidade do BGP

-  Você deve anexar um circuito de rota expressa toohello do filtro de rota hello.

## <a name="before-you-begin"></a>Antes de começar

Antes de começar a configuração, verifique se que você atende Olá critérios a seguir:

 - Saudação de revisão [pré-requisitos](expressroute-prerequisites.md) e [fluxos de trabalho](expressroute-workflows.md) antes de começar a configuração.

 - Você deve ter um circuito do ExpressRoute ativo. Siga as instruções de saudação muito[criar um circuito de rota expressa](expressroute-howto-circuit-portal-resource-manager.md) e ter o circuito Olá habilitado por seu provedor de conectividade antes de continuar. Olá circuito de rota expressa deve estar em um estado habilitado e configurado.

 - Você deve ter um emparelhamento da Microsoft ativo. Siga as instruções em [Criar e modificar a configuração de emparelhamento](expressroute-howto-routing-portal-resource-manager.md)


## <a name="prefixes"></a>Etapa 1. Obter uma lista de prefixos e valores de comunidade BGP

### <a name="1-get-a-list-of-bgp-community-values"></a>1. Obter uma lista de valores de comunidade BGP

Os valores de comunidade BGP associados aos serviços acessíveis por meio de emparelhamento da Microsoft está disponível em Olá [requisitos de roteamento de rota expressa](expressroute-routing.md) página.

### <a name="2-make-a-list-of-hello-values-that-you-want-toouse"></a>2. Faça uma lista de valores de saudação que você deseja toouse

Faça uma lista de valores de comunidade BGP, que você deseja toouse no filtro de rota hello. Por exemplo, Olá valor de comunidade BGP para serviços do Dynamics 365 é 12076:5040.

## <a name="filter"></a>Etapa 2. Criar um filtro de rota e uma regra de filtro

Um filtro de rota pode ter apenas uma regra e regra Olá deve ser do tipo 'Permitir'. Essa regra pode ter uma lista de valores de comunidade BGP associados a ela.

### <a name="1-create-a-route-filter"></a>1. Criar um filtro de rota
Você pode criar um filtro de rota selecionando Olá opção toocreate um novo recurso. Clique em **novo** > **rede** > **RouteFilter**, conforme mostrado no Olá a imagem a seguir:

![Criar um filtro de rota](.\media\how-to-routefilter-portal\CreateRouteFilter1.png)

Você deve colocar o filtro de rota Olá em um grupo de recursos. 

![Criar um filtro de rota](.\media\how-to-routefilter-portal\CreateRouteFilter.png)

### <a name="2-create-a-filter-rule"></a>2. Criar uma regra de filtro

Você pode adicionar e atualizar regras selecionando Olá gerenciar guia de regra para o filtro de rota.

![Criar um filtro de rota](.\media\how-to-routefilter-portal\ManageRouteFilter.png)


Você pode selecionar Olá serviços que você deseja tooconnect toofrom Olá lista suspensa e salvar a regra de saudação quando terminar.

![Criar um filtro de rota](.\media\how-to-routefilter-portal\AddRouteFilterRule.png)


## <a name="attach"></a>Etapa 3. Anexar o circuito de rota expressa tooan do filtro de rota Olá

Você pode anexar o circuito de tooa de filtro de rota Olá selecionando o botão de "Adicionar circuito" hello e selecionando circuito de rota expressa Olá na lista suspensa de saudação.

![Criar um filtro de rota](.\media\how-to-routefilter-portal\AddCktToRouteFilter.png)

## <a name="getproperties"></a>Propriedades de saudação tooget de um filtro de rota

Você pode exibir as propriedades de um filtro de rota quando você abre o recurso Olá no portal de saudação.

![Criar um filtro de rota](.\media\how-to-routefilter-portal\ViewRouteFilter.png)


## <a name="updateproperties"></a>Propriedades de saudação tooupdate de um filtro de rota

Você pode atualizar a lista de saudação do BGP comunidade valores tooa anexado circuito selecionando o botão hello "Gerenciar regra".


![Criar um filtro de rota](.\media\how-to-routefilter-portal\ManageRouteFilter.png)

![Criar um filtro de rota](.\media\how-to-routefilter-portal\AddRouteFilterRule.png) 


## <a name="detach"></a>toodetach um filtro de roteamento de um circuito de rota expressa

toodetach um circuito do filtro de rota hello, clique com o botão direito no circuito hello e clique no "desassociar".

![Criar um filtro de rota](.\media\how-to-routefilter-portal\DetachRouteFilter.png) 


## <a name="delete"></a>toodelete um filtro de rota

Você pode excluir um filtro de rota, selecionando o botão de exclusão de saudação. 

![Criar um filtro de rota](.\media\how-to-routefilter-portal\DeleteRouteFilter.png) 

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre a rota expressa, consulte Olá [perguntas Frequentes do ExpressRoute](expressroute-faqs.md).
