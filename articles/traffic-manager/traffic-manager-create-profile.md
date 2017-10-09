---
title: aaaCreate um perfil do Traffic Manager no Azure | Microsoft Docs
description: "Este artigo descreve como toocreate um perfil do Gerenciador de tráfego"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: kumud
ms.openlocfilehash: 5cd3d2903552c9a0427da41a73f6f38f6b0afc1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-traffic-manager-profile"></a>Criar um perfil do Gerenciador de Tráfego

Este artigo descreve como um perfil com **prioridade** tipo de roteamento pode ser criado pontos de extremidade de aplicativos Web do Azure tootwo tooroute usuários. Usando Olá **prioridade** roteamento tipo, todo o tráfego é roteado toohello primeiro ponto de extremidade enquanto Olá segundo é mantido como backup. Como resultado, os usuários podem ser roteadas toohello segundo ponto de extremidade se o primeiro ponto de extremidade de saudação se tornará não íntegro.

Neste artigo, dois pontos de extremidade criados anteriormente do aplicativo Web do Azure são perfil do Gerenciador de tráfego associado toothis recém-criado. toolearn mais informações sobre como toocreate pontos de extremidade de aplicativo Web do Azure, visite Olá [página de documentação de aplicativos Web do Azure](https://docs.microsoft.com/azure/app-service-web/). Você pode adicionar qualquer ponto de extremidade que tem um nome DNS e está acessível pela internet pública e o que estamos usando pontos de extremidade de aplicativos Web do Azure como um exemplo de hello.

### <a name="create-a-traffic-manager-profile"></a>Criar um perfil do Gerenciador de Tráfego
1. Em um navegador, entrar toohello [portal do Azure](http://portal.azure.com). Caso ainda não tenha uma conta, você pode se inscrever para obter uma [avaliação gratuita por um mês](https://azure.microsoft.com/free/). 
2. Em Olá **Hub** menu, clique em **novo** > **rede** > **ver todos os**, clique em **tráfego Gerenciador de** saudação do perfil tooopen **perfil do Traffic Manager criar** folha, em seguida, clique em **criar**.
3. Em Olá **perfil do Traffic Manager criar** folha, completa, da seguinte maneira:
    1. Em **Nome**, forneça um nome para seu perfil. Esse nome precisa toobe exclusivos dentro de saudação trafficmanager.net região e resulta em nomes DNS Olá <name>, trafficmanager.net que é usado tooaccess perfil do Traffic Manager.
    2. Em **método de roteamento**, selecione Olá **prioridade** método de roteamento.
    3. Em **assinatura**, selecione Olá assinatura você deseja toocreate esse perfil em
    4. Em **grupo de recursos**, criar um novo tooplace de grupo de recursos esse perfil em.
    5. Em **local do grupo de recursos**, selecione o local de Olá Olá do grupo de recursos. Essa configuração se refere local toohello saudação do grupo de recursos e não tem impacto sobre Olá perfil do Traffic Manager que será implantado globalmente.
    6. Clique em **Criar**.
    7. Quando a implantação global saudação do perfil do Traffic Manager é concluída, ele é listado no grupo de recursos do respectivos como um dos recursos de saudação.

    ![Criar um perfil do Gerenciador de Tráfego](./media/traffic-manager-create-profile/Create-traffic-manager-profile.png)

## <a name="add-traffic-manager-endpoints"></a>Adicionar pontos de extremidade do Gerenciador de Tráfego

1. Na barra de pesquisa do portal hello, procure Olá **perfil do Traffic Manager** nome que você criou no hello antecede o perfil do Gerenciador de tráfego Olá seção e clique no hello resultados que Olá exibido.
2. Em Olá **perfil do Traffic Manager** folha em Olá **configurações** seção, clique em **pontos de extremidade**.
3. Em Olá **pontos de extremidade** folha que é exibida, clique em **adicionar**.
4. Em Olá **Adicionar ponto de extremidade** folha, completa, da seguinte maneira:
    1. Para **Tipo**, clique em **Ponto de Extremidade do Azure**.
    2. Forneça um **nome** pelo qual você deseja toorecognize esse ponto de extremidade.
    3. Para **Tipo de recurso de destino**, clique em **Serviço de Aplicativo**.
    4. Para **recurso de destino**, clique em **escolher um aplicativo de serviço** tooshow listagem de saudação do hello aplicativos Web em hello mesma assinatura. Em Olá **recurso** folha que é exibida, escolha Olá que você deseja tooadd como Olá primeiro ponto de extremidade do serviço de aplicativo.
    5. Para **Prioridade**, selecione **1**. Isso resulta em todo o tráfego direcionado de ponto de extremidade toothis se está íntegro.
    6. Mantenha a opção **Adicionar como desabilitado** desmarcada.
    7. Clique em **OK**
5.  Repita as etapas 3 e 4 para Olá próximo aplicativos Web do Azure ponto de extremidade. Certifique-se de que tooadd com seus **prioridade** valor definido em **2**.
6.  Quando a adição de saudação de ambos os pontos de extremidade estiver concluída, eles são exibidos no Olá **perfil do Traffic Manager** folha juntamente com seu status de monitoramento como **Online**.

    ![Adicionar um ponto de extremidade do Gerenciador de Tráfego](./media/traffic-manager-create-profile/add-traffic-manager-endpoint.png)

## <a name="use-hello-traffic-manager-profile"></a>Usar perfil do Traffic Manager Olá
1.  Na barra de pesquisa do portal hello, procure Olá **perfil do Traffic Manager** nome que você criou na saudação anterior de seção. Nos resultados de saudação que são exibidos, clique em perfil do Gerenciador de tráfego de saudação.
2. Em Olá **perfil do Traffic Manager** folha, clique em **visão geral**.
3. Olá **perfil do Traffic Manager** folha exibe o nome DNS de saudação do perfil do Traffic Manager recém-criado. Isso pode ser usado por qualquer clientes (por exemplo, navegando tooit usando um navegador da web) tooget roteada toohello certo ponto de extremidade conforme determinado pelo tipo de roteamento hello. Nesse caso, todas as solicitações são roteadas toohello primeiro ponto de extremidade e se o Traffic Manager detecta sejam problemáticos, tráfego de saudação passam automaticamente toohello próximo ponto de extremidade.

## <a name="delete-hello-traffic-manager-profile"></a>Excluir perfil do Gerenciador de tráfego Olá
Quando não é mais necessário, exclua o grupo de recursos hello e perfil do Traffic Manager Olá que você criou. toodo assim, selecione o grupo de recursos de saudação do hello **perfil do Traffic Manager** folha e clique em **excluir**.

## <a name="next-steps"></a>Próximas etapas

- Saiba mais sobre [tipos de roteamento](traffic-manager-routing-methods.md).
- Saiba mais sobre os tipos de ponto de extremidade [tipos de ponto de extremidade](traffic-manager-endpoint-types.md).
- Saiba mais sobre [monitoramento do ponto de extremidade](traffic-manager-monitoring.md).



