---
title: "perfis do Gerenciador de tráfego do Azure aaaManage | Microsoft Docs"
description: "Este artigo o ajuda a criar, desabilitar, habilitar e excluir um perfil do Gerenciador de Tráfego do Azure."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: f06e0365-0a20-4d08-b7e1-e56025e64f66
ms.service: traffic-manager
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/10/2017
ms.author: kumud
ms.openlocfilehash: 0c6ab0c451581d039514a9de0b525b3937e45a85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-traffic-manager-profile"></a>Gerenciar um perfil de Gerenciador de tráfego do Azure

Perfis do Traffic Manager usam roteamento de tráfego a métodos de distribuição do hello toocontrol de serviços de nuvem do tráfego tooyour ou pontos de extremidade do site. Este artigo explica como toocreate e gerenciar esses perfis.

## <a name="create-a-traffic-manager-profile"></a>Criar um perfil do Gerenciador de Tráfego

Você pode criar um perfil do Gerenciador de tráfego usando Olá portal do Azure. Depois de criar seu perfil, você pode configurar pontos de extremidade, monitoramento e outras configurações Olá portal do Azure. O Traffic Manager oferece suporte a pontos de extremidade too200 por perfil. No entanto, a maioria dos cenários de uso exigem apenas um pequeno número de pontos de extremidade.

### <a name="toocreate-a-traffic-manager-profile"></a>toocreate um perfil do Gerenciador de tráfego

1. Em um navegador, entrar toohello [portal do Azure](http://portal.azure.com). Caso ainda não tenha uma conta, você pode se inscrever para obter uma [avaliação gratuita por um mês](https://azure.microsoft.com/free/). 
2. Em Olá **Hub** menu, clique em **novo** > **rede** > **ver todos os**, clique em **tráfego Gerenciador de** saudação do perfil tooopen **perfil do Traffic Manager criar** folha, em seguida, clique em **criar**.
3. Em Olá **perfil do Traffic Manager criar** folha, completa, da seguinte maneira:
    1. Em **Nome**, forneça um nome para seu perfil. Esse nome precisa toobe exclusivos dentro de saudação trafficmanager.net região e resulta em nomes DNS Olá <name>, trafficmanager.net, que é usado tooaccess perfil do Traffic Manager.
    2. Em **método de roteamento**, selecione Olá **prioridade** método de roteamento.
    3. Em **assinatura**, selecione Olá assinatura você deseja toocreate esse perfil em
    4. Em **grupo de recursos**, criar um novo tooplace de grupo de recursos esse perfil em.
    5. Em **local do grupo de recursos**, selecione o local de Olá Olá do grupo de recursos. Essa configuração se refere local toohello saudação do grupo de recursos e não tem impacto sobre Olá perfil do Traffic Manager que será implantado globalmente.
    6. Clique em **Criar**.
    7. Quando a implantação global saudação do perfil do Traffic Manager é concluída, ele é listado no grupo de recursos do respectivos como um dos recursos de saudação.

## <a name="disable-enable-or-delete-a-profile"></a>Desabilitar, habilitar ou excluir um perfil

Você pode desabilitar um perfil existente para que o Gerenciador de tráfego não se refere a pontos de extremidade do usuário solicitações toohello configurado. Quando você desabilita um perfil do Gerenciador de tráfego, perfil de saudação e informações de saudação contido no perfil de saudação permanecem intactos e podem ser editados na interface do Traffic Manager hello.  Referências continuar quando você reabilitar o perfil de saudação. Quando você cria um perfil do Gerenciador de tráfego no portal do Azure de saudação, ela é habilitada automaticamente. Se você decidir que um perfil não é mais necessário, poderá excluí-lo.

### <a name="toodisable-a-profile"></a>toodisable um perfil

1. Se você estiver usando um nome de domínio personalizado, altere o registro CNAME Olá no servidor DNS da Internet para que ele aponte o perfil do Gerenciador de tráfego tooyour não.
2. Tráfego deixa de ser direcionada toohello pontos de extremidade por meio de configurações de perfil do Traffic Manager hello.
3. Em um navegador, entrar toohello [portal do Azure](http://portal.azure.com).
2. Na barra de pesquisa do portal hello, procure Olá **perfil do Traffic Manager** nome que você deseja toomodify e clique em perfil do Traffic Manager Olá no hello resultados que Olá exibido.
3. Em hello **perfil do Traffic Manager** folha, clique em **visão geral**, na folha de visão geral de saudação clique **desabilitar**e, em seguida, confirme o perfil do Gerenciador de tráfego de saudação toodisable.

### <a name="tooenable-a-profile"></a>tooenable um perfil

1. Em um navegador, entrar toohello [portal do Azure](http://portal.azure.com).
2. Na barra de pesquisa do portal hello, procure Olá **perfil do Traffic Manager** nome que você deseja toomodify e clique em perfil do Traffic Manager Olá no hello resultados que Olá exibido.
3. Em Olá **perfil do Traffic Manager** folha, clique em **visão geral**e, na folha de visão geral de saudação, clique em **habilitar**.
5. Se você estiver usando um nome de domínio personalizado, crie um registro de recurso CNAME em seu nome de domínio DNS de Internet server toopoint toohello do seu perfil do Gerenciador de tráfego.
6. O tráfego é direcionado toohello pontos de extremidade novamente.

### <a name="toodelete-a-profile"></a>toodelete um perfil

1. Certifique-se de que o registro de recurso DNS Olá no servidor DNS da Internet não usa um registro de recurso CNAME que aponte toohello nome de domínio do seu perfil do Gerenciador de tráfego.
2. Na barra de pesquisa do portal hello, procure Olá **perfil do Traffic Manager** nome que você deseja toomodify e clique em perfil do Traffic Manager Olá no hello resultados que Olá exibido.
3. Em Olá **perfil do Traffic Manager** folha, clique em **visão geral**, na folha de visão geral de saudação clique **excluir**e, em seguida, confirme o perfil do Gerenciador de tráfego de saudação toodelete.

## <a name="next-steps"></a>Próximas etapas

* [Adicionar um ponto de extremidade](traffic-manager-endpoints.md)
* [Configurar o método de roteamento de prioridades](traffic-manager-configure-priority-routing-method.md)
* [Configurar o método de roteamento geográfico](traffic-manager-configure-geographic-routing-method.md) 
* [Configurar o método de roteamento ponderado](traffic-manager-configure-weighted-routing-method.md)
* [Configurar o método de roteamento de desempenho](traffic-manager-configure-performance-routing-method.md)
