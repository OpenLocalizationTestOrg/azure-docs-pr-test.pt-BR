---
title: "aaaMoving ExpressRoute circuitos do clássico tooResource Manager | Microsoft Docs"
description: "Esta página fornece uma visão geral do que você precisa tooknow sobre ponte hello clássico e modelos de implantação do Gerenciador de recursos de saudação."
documentationcenter: na
services: expressroute
author: ganesr
manager: carmonm
editor: 
ms.assetid: bdf01217-1a98-4ec0-a08e-d84fd37f78af
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/02/2017
ms.author: ganesr
ms.openlocfilehash: c901d2cda01aec409b528d29fc937ac6afaea511
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="moving-expressroute-circuits-from-hello-classic-toohello-resource-manager-deployment-model"></a>Movendo circuitos ExpressRoute de saudação clássico toohello modelo de implantação do Gerenciador de recursos
Este artigo fornece uma visão geral do que significa toomove um circuito de rota expressa do Azure de saudação clássico toohello modelo de implantação do Gerenciador de recursos do Azure.

Você pode usar uma única rota expressa circuito tooconnect toovirtual redes que são implantados em Olá clássico e modelos de implantação do Gerenciador de recursos de saudação. Um circuito de rota expressa, independentemente de como ele é criado, agora pode vincular redes toovirtual entre os dois modelos de implantação.

![Um circuito de rota expressa que vincula toovirtual redes em ambos os modelos de implantação](./media/expressroute-move/expressroute-move-1.png)

## <a name="expressroute-circuits-that-are-created-in-hello-classic-deployment-model"></a>Circuitos de rota expressa que são criados no modelo de implantação clássico Olá
Circuitos de rota expressa que são criados no modelo de implantação clássico Olá necessário toobe movido toohello Gerenciador de recursos modelo primeiro tooenable conectividade tooboth Olá clássico e hello Gerenciador de recursos implantação modelos de implantação. Não há perda de conectividade nem interrupção quando uma conexão está sendo movida. Todos os links de circuito virtual de rede no modelo de implantação clássico hello (Olá na mesma assinatura e entre assinaturas) são preservados.

Após a movimentação de saudação é concluída com êxito, hello circuito de rota expressa parece, executa e parece exatamente um circuito de rota expressa que foi criado no modelo de implantação do Gerenciador de recursos de saudação. Agora você pode criar conexões de redes toovirtual no modelo de implantação do Gerenciador de recursos de saudação.

Depois que um circuito de rota expressa foi movido toohello modelo de implantação de Gerenciador de recursos, você pode gerenciar o ciclo de vida de saudação do hello circuito de rota expressa apenas usando o modelo de implantação do Gerenciador de recursos de saudação. Isso significa que você pode realizar operações como adição/atualização/exclusão emparelhamentos, atualizar propriedades de circuito (como largura de banda, SKU e tipo de cobrança) e excluir circuitos apenas no modelo de implantação do Gerenciador de recursos de saudação. Consulte a seção toohello abaixo em circuitos criados no modelo de implantação do Gerenciador de recursos Olá para obter mais detalhes sobre como gerenciar modelos de implantação do acesso tooboth.

Você não tem tooinvolve mover seu Olá de tooperform do provedor de conectividade.

## <a name="expressroute-circuits-that-are-created-in-hello-resource-manager-deployment-model"></a>Circuitos de rota expressa que são criados no modelo de implantação do Gerenciador de recursos de saudação
Você pode habilitar os circuitos ExpressRoute que são criados no toobe de modelo de implantação de Gerenciador de recursos de saudação acessíveis de ambos os modelos de implantação. Nenhum circuito de rota expressa em sua assinatura pode ser habilitado toobe acessado de ambos os modelos de implantação.

* Circuitos do ExpressRoute que foram criados no modelo de implantação do Gerenciador de recursos de saudação não tem o modelo de implantação clássico toohello acesso por padrão.
* Circuitos de rota expressa que foram movidos do modelo de implantação do hello implantação clássica modelo toohello Resource manager são acessíveis de ambos os modelos de implantação por padrão.
* Um circuito de rota expressa sempre tem acesso toohello Gerenciador de recursos modelo de implantação, independentemente se ela foi criada em Olá Gerenciador de recursos ou o modelo de implantação clássico. Isso significa que você pode criar conexões toovirtual redes criadas Olá modelo de implantação do Gerenciador de recursos seguindo as instruções em [como redes virtuais toolink](expressroute-howto-linkvnet-arm.md).
* Modelo de implantação clássico toohello acesso é controlado pela Olá **allowClassicOperations** parâmetro hello circuito de rota expressa.

> [!IMPORTANT]
> Todas as cotas são documentadas em Olá [limites de serviço](../azure-subscription-service-limits.md) página se aplica. Por exemplo, um circuito padrão pode ter no máximo 10 links/conexões de rede virtual entre Olá clássico e modelos de implantação do Gerenciador de recursos de saudação.
> 
> 

## <a name="controlling-access-toohello-classic-deployment-model"></a>Controlando o modelo de implantação clássico toohello de acesso
Você pode habilitar uma única rota expressa circuito toolink toovirtual redes em ambos os modelos de implantação, configuração Olá **allowClassicOperations** parâmetro hello circuito de rota expressa.

Configuração **allowClassicOperations** tooTRUE permite que as redes virtuais toolink de ambos os modelos de implantação toohello circuito de rota expressa. Você pode vincular redes toovirtual no modelo de implantação clássico hello, diretrizes a seguir em [como toolink de redes virtuais no hello modelo de implantação clássico](expressroute-howto-linkvnet-classic.md). Você pode vincular redes toovirtual no modelo de implantação do Gerenciador de recursos de saudação pelo seguinte orientação na [como toolink de redes virtuais no hello modelo de implantação do Gerenciador de recursos](expressroute-howto-linkvnet-arm.md).

Configuração **allowClassicOperations** tooFALSE blocos acessar toohello circuito do modelo de implantação clássico hello. No entanto, todos os links de rede virtual no modelo de implantação clássico Olá são preservados. Nesse caso, Olá circuito de rota expressa não estiver visível no modelo de implantação clássico hello.

## <a name="supported-operations-in-hello-classic-deployment-model"></a>As operações com suporte no modelo de implantação clássico Olá
Olá clássicas operações a seguir têm suporte em uma rota expressa circuito quando **allowClassicOperations** está definida tooTRUE:

* Obter informações do circuito do ExpressRoute
* Links de rede virtual criar/atualizar/get/excluir redes virtuais tooclassic
* Criar/atualizar/obter/excluir autorizações de link da rede virtual para a conectividade entre as assinaturas

Não é possível executar Olá clássicas operações a seguir quando **allowClassicOperations** está definida tooTRUE:

* Criar/atualizar/obter/excluir emparelhamentos BGP (Border Gateway Protocol ) para os emparelhamentos dos Azures privado e público, e da Microsoft
* Excluir circuitos do ExpressRoute

## <a name="communication-between-hello-classic-and-hello-resource-manager-deployment-models"></a>Comunicação entre hello clássico e modelos de implantação do Gerenciador de recursos de saudação
Olá circuito de rota expressa age como uma ponte entre hello clássico e modelos de implantação do Gerenciador de recursos de saudação. Se ambas as redes virtuais são vinculado toohello o tráfego entre máquinas virtuais em redes virtuais no modelo de implantação clássico hello e as redes virtuais em fluxos de modelo de implantação Olá Gerenciador de recursos por meio de rota expressa mesmo circuito de rota expressa.

Taxa de transferência agregada é limitada pela capacidade de taxa de transferência Olá Olá virtual do gateway de rede. O tráfego não insira redes do provedor de conectividade hello ou seu nesses casos. Fluxo do tráfego entre redes virtuais Olá é totalmente contido dentro de rede da Microsoft hello.

## <a name="access-tooazure-public-and-microsoft-peering-resources"></a>Acesso público de tooAzure e recursos de emparelhamento da Microsoft
Você pode continuar tooaccess recursos que são geralmente acessíveis por meio do emparelhamento público do Azure e emparelhamento da Microsoft sem interrupções.  

## <a name="whats-supported"></a>O que tem suporte
Esta seção descreve o que tem suporte para os circuitos do ExpressRoute:

* Você pode usar uma única rota expressa circuito tooaccess redes virtuais que são implantados em hello clássico e modelos de implantação do Gerenciador de recursos de saudação.
* Você pode mover um circuito de rota expressa de saudação clássico toohello modelo de implantação do Gerenciador de recursos. Depois que ele for movido, Olá circuito de rota expressa parece parece e é executado como qualquer outro circuito de rota expressa é criado no modelo de implantação do Gerenciador de recursos de saudação.
* Você pode mover apenas o circuito de rota expressa hello. Os links do circuito, redes virtuais e gateways VPN não podem ser movidos com essa operação.
* Depois que um circuito de rota expressa foi movido toohello modelo de implantação de Gerenciador de recursos, você pode gerenciar o ciclo de vida de saudação do hello circuito de rota expressa apenas usando o modelo de implantação do Gerenciador de recursos de saudação. Isso significa que você pode realizar operações como adição/atualização/exclusão emparelhamentos, atualizar propriedades de circuito (como largura de banda, SKU e tipo de cobrança) e excluir circuitos apenas no modelo de implantação do Gerenciador de recursos de saudação.
* Olá circuito de rota expressa age como uma ponte entre hello clássico e modelos de implantação do Gerenciador de recursos de saudação. Se ambas as redes virtuais são vinculado toohello o tráfego entre máquinas virtuais em redes virtuais no modelo de implantação clássico hello e as redes virtuais em fluxos de modelo de implantação Olá Gerenciador de recursos por meio de rota expressa mesmo circuito de rota expressa.
* Há suporte para a conectividade entre assinaturas Olá clássico e modelos de implantação do Gerenciador de recursos de saudação.
* Depois de mover um circuito de rota expressa do modelo do hello modelo clássico toohello Azure Resource Manager, você pode [migrar Olá de redes virtuais vinculadas toohello circuito de rota expressa](expressroute-migration-classic-resource-manager.md).

## <a name="whats-not-supported"></a>O que não tem suporte
Esta seção descreve o que não tem suporte para os circuitos do ExpressRoute:

* Gerenciando Olá ciclo de vida de um circuito de rota expressa do modelo de implantação clássico hello.
* Suporte de controle de acesso (RBAC) baseada em função para o modelo de implantação clássico hello. Você não pode executar o RBAC controles tooa circuito no modelo de implantação clássico hello. Qualquer administrador/coadministrator de assinatura de saudação podem criar ou remover o circuito de toohello redes virtuais.

## <a name="configuration"></a>Configuração
Siga as instruções de saudação descritas [mover um circuito de rota expressa do modelo de implantação do Gerenciador de recursos de toohello clássico de Olá](expressroute-howto-move-arm.md).

## <a name="next-steps"></a>Próximas etapas
* [Migrar Olá de redes virtuais vinculadas toohello circuito de rota expressa do modelo do hello modelo clássico toohello Gerenciador de recursos do Azure](expressroute-migration-classic-resource-manager.md)
* Para obter informações sobre o fluxo de trabalho, consulte [Fluxos de trabalho de provisionamento e estados do circuito do ExpressRoute](expressroute-workflows.md).
* tooconfigure sua conexão de rota expressa:
  
  * [Criar um circuito do ExpressRoute](expressroute-howto-circuit-arm.md)
  * [Configurar o roteamento](expressroute-howto-routing-arm.md)
  * [Vincular um circuito de rota expressa do tooan de rede virtual](expressroute-howto-linkvnet-arm.md)

