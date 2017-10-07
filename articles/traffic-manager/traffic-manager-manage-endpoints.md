---
title: aaaManage pontos de extremidade no Azure Traffic Manager | Microsoft Docs
description: "Este artigo o ajudará a adicionar, remover, habilitar e desabilitar pontos de extremidade do Gerenciador de Tráfego do Azure."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: ade2bbc2-35a7-43c5-8001-4698f7254526
ms.service: traffic-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/08/2017
ms.author: kumud
ms.openlocfilehash: fc65874ae2eaeb6fca5d8c4f33403c258307bdb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-disable-enable-or-delete-endpoints"></a>Adicionar, desabilitar, habilitar ou excluir pontos de extremidade

recurso de aplicativos Web Olá no serviço de aplicativo do Azure já fornece failover e funcionalidade de roteamento de tráfego de round-robin para sites em um data center, independentemente do modo de site hello. O Azure Traffic Manager permite que você toospecify failover e roteamento de tráfego de round-robin para sites e serviços de nuvem em datacenters diferentes. Olá primeira etapa necessário tooprovide funcionalidade é tooadd Olá nuvem serviço ou site do ponto de extremidade tooTraffic Manager.

Você também pode desabilitar pontos de extremidade individuais que fazem parte de um perfil do Gerenciador de Tráfego. Desabilitar um ponto de extremidade deixa ele como parte do perfil de saudação, mas o perfil de saudação age como se o ponto de extremidade de saudação não estivesse incluído nela. Essa ação é útil para remover temporariamente um ponto de extremidade que esteja no modo de manutenção ou sendo reimplantado. Quando o ponto de extremidade de saudação está funcionando novamente, ele poderá ser habilitado.

> [!NOTE]
> Desabilitar um ponto de extremidade não tem nada toodo com seu estado de implantação no Azure. Um ponto de extremidade Íntegro permanecerá cima e é capaz de tráfego de tooreceive mesmo quando desabilitado no Traffic Manager. Além disso, a desabilitação de um ponto de extremidade em um perfil não afeta seu status em outro perfil.

## <a name="tooadd-a-cloud-service-or-an-app-service-endpoint-tooa-traffic-manager-profile"></a>tooadd um serviço de nuvem ou um tooa de ponto de extremidade de serviço de aplicativo perfil do Traffic Manager

1. Em um navegador, entrar toohello [portal do Azure](http://portal.azure.com).
2. Na barra de pesquisa do portal hello, procure Olá **perfil do Traffic Manager** nome que você deseja toomodify e clique em perfil do Traffic Manager Olá no hello resultados que Olá exibido.
3. Em Olá **perfil do Traffic Manager** folha em Olá **configurações** seção, clique em **pontos de extremidade**.
4. Em Olá **pontos de extremidade** folha que é exibida, clique em **adicionar**.
5. Em Olá **Adicionar ponto de extremidade** folha, completa, da seguinte maneira:
    1. Para **Tipo**, clique em **Ponto de Extremidade do Azure**.
    2. Forneça um **nome** pelo qual você deseja toorecognize esse ponto de extremidade.
    3. Para **tipo de recurso de destino**, de Olá suspenso, escolher tipo de recurso apropriado hello.
    4. Para **recurso de destino**, de Olá lista suspensa, escolha o recurso de destino apropriado Olá tooshow Olá listagem de recursos Olá a mesma assinatura em hello **folha de recursos**. Em Olá **recurso** folha que é exibida, escolha Olá serviço que você deseja tooadd como Olá primeiro ponto de extremidade.
    5. Para **Prioridade**, selecione **1**. Isso resulta em todo o tráfego direcionado de ponto de extremidade toothis se está íntegro.
    6. Mantenha a opção **Adicionar como desabilitado** desmarcada.
    7. Clique em **OK**
6.  Repita as etapas 4 e 5 tooadd Olá próximo Azure ponto de extremidade. Certifique-se de que tooadd com seus **prioridade** valor definido em **2**.
7.  Quando a adição de saudação de ambos os pontos de extremidade estiver concluída, eles são exibidos no Olá **perfil do Traffic Manager** folha juntamente com seu status de monitoramento como **Online**.

> [!NOTE]
> Depois de adicionar ou remover um ponto de extremidade de um perfil usando Olá *Failover* método de roteamento de tráfego, lista de prioridade de failover Olá pode não ser ordenados eles como desejar. Você pode ajustar a ordem de saudação do hello lista de prioridade de Failover na página de configuração de saudação. Para obter mais informações, consulte [Configurar roteamento de tráfego de Failover](traffic-manager-configure-failover-routing-method.md).

## <a name="toodisable-an-endpoint"></a>toodisable um ponto de extremidade

1. Em um navegador, entrar toohello [portal do Azure](http://portal.azure.com).
2. Na barra de pesquisa do portal hello, procure Olá **perfil do Traffic Manager** nome que você deseja toomodify e clique em perfil do Traffic Manager Olá nos resultados de saudação que são exibidos.
3. Em Olá **perfil do Traffic Manager** folha em Olá **configurações** seção, clique em **pontos de extremidade**. 
4. Clique Olá de ponto de extremidade que você deseja toodisable e, em seguida, em Olá **ponto de extremidade** folha que é exibida, clique em **editar**.
5. Em Olá **ponto de extremidade** folha, alterar o status de ponto de extremidade de saudação muito**desabilitado**e, em seguida, clique em **salvar**.
6. Os clientes continuam ponto de extremidade do toosend tráfego toohello por duração de saudação do tempo de vida (TTL). Você pode alterar Olá TTL na página de configuração de saudação do hello perfil do Traffic Manager.

## <a name="tooenable-an-endpoint"></a>tooenable um ponto de extremidade

1. Em um navegador, entrar toohello [portal do Azure](http://portal.azure.com).
2. Na barra de pesquisa do portal hello, procure Olá **perfil do Traffic Manager** nome que você deseja toomodify e clique em perfil do Traffic Manager Olá nos resultados de saudação que são exibidos.
3. Em Olá **perfil do Traffic Manager** folha em Olá **configurações** seção, clique em **pontos de extremidade**. 
4. Clique Olá de ponto de extremidade que você deseja toodisable e, em seguida, em Olá **ponto de extremidade** folha que é exibida, clique em **editar**.
5. Em Olá **ponto de extremidade** folha, alterar o status de ponto de extremidade de saudação muito**habilitado**e, em seguida, clique em **salvar**.
6. Os clientes continuam ponto de extremidade do toosend tráfego toohello por duração de saudação do tempo de vida (TTL). Você pode alterar Olá TTL na página de configuração de saudação do hello perfil do Traffic Manager.

## <a name="toodelete-an-endpoint"></a>toodelete um ponto de extremidade

1. Em um navegador, entrar toohello [portal do Azure](http://portal.azure.com).
2. Na barra de pesquisa do portal hello, procure Olá **perfil do Traffic Manager** nome que você deseja toomodify e clique em perfil do Traffic Manager Olá nos resultados de saudação que são exibidos.
3. Em Olá **perfil do Traffic Manager** folha em Olá **configurações** seção, clique em **pontos de extremidade**. 
4. Clique Olá de ponto de extremidade que você deseja toodisable e, em seguida, em Olá **ponto de extremidade** folha que é exibida, clique em **editar**.
5. Em Olá **ponto de extremidade** folha, alterar o status de ponto de extremidade de saudação muito**habilitado**e, em seguida, clique em **salvar**.


## <a name="next-steps"></a>Próximas etapas

* [Gerenciar perfis do Gerenciador de Tráfego](traffic-manager-manage-profiles.md)
* [Configurar métodos de roteamento](traffic-manager-configure-routing-method.md)
* [Solucionando problemas de estado degradado do Gerenciador de Tráfego](traffic-manager-troubleshooting-degraded.md)
* [Considerações sobre desempenho do Gerenciador de Tráfego](traffic-manager-performance-considerations.md)
* [Operações no Gerenciador de Tráfego (referência de API REST)](http://go.microsoft.com/fwlink/p/?LinkID=313584)

