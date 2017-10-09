---
title: "usando o Azure Traffic Manager do método de roteamento de tráfego de prioridade aaaConfigure | Microsoft Docs"
description: "Este artigo explica como prioridade de saudação tooconfigure tráfego método de roteamento no Gerenciador de tráfego"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 6dca6de1-18f7-4962-bd98-6055771fab22
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/20/2017
ms.author: kumud
ms.openlocfilehash: dd3e3bb2a727e5ea087cee35962c8e6f7c357282
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-priority-traffic-routing-method-in-traffic-manager"></a>Configurar o método de roteamento de tráfego de prioridade no Gerenciador de Tráfego

Independentemente do modo de site hello, sites do Azure já fornecem a funcionalidade de failover para sites em um data center (também conhecido como região). O Gerenciador de Tráfego fornece failover para sites em diferentes data centers.

Um padrão comum para failover de serviço é toosend tráfego tooa principal serviço e fornecer um conjunto de serviços de backup idênticos para failover. Olá etapas a seguir explicam como tooconfigure isso priorizadas failover com sites e serviços de nuvem do Azure:

## <a name="tooconfigure-hello-priority-traffic-routing-method"></a>método de roteamento de tráfego tooconfigure Olá prioridade

1. Em um navegador, entrar toohello [portal do Azure](http://portal.azure.com). Caso ainda não tenha uma conta, você pode se inscrever para obter uma [avaliação gratuita por um mês](https://azure.microsoft.com/free/). 
2. Na barra de pesquisa do portal hello, procure Olá **perfis do Traffic Manager** e clique em nome do perfil Olá que você deseja que o método de roteamento de saudação tooconfigure para.
3. Em Olá **perfil do Traffic Manager** folha, verifique se ambos Olá serviços de nuvem e sites que você deseja tooinclude em sua configuração estão presentes.
4. Em Olá **configurações** seção, clique em **configuração**e em Olá **configuração** folha, completa, da seguinte maneira:
    1. Para **configurações do método de roteamento de tráfego**, verifique se o método de roteamento de tráfego Olá é **prioridade**. Se não estiver, clique em **prioridade** na lista suspensa hello.
    2. Saudação de conjunto **as configurações do monitor de ponto de extremidade** idênticos para todos os cada ponto de extremidade neste perfil da seguinte maneira:
        1. Selecione Olá apropriado **protocolo**e especifique Olá **porta** número. 
        2. Para **Caminho**, digite uma barra "/" */*. pontos de extremidade toomonitor, você deve especificar um caminho e nome de arquivo. A barra "/" é uma entrada válida para o caminho relativo do hello e indica se o arquivo hello está no diretório raiz de saudação (padrão).
        3. Na parte superior de saudação da página de saudação, clique em **salvar**.
5. Em Olá **configurações** seção, clique em **pontos de extremidade**.
6. Em Olá **pontos de extremidade** folha, ordem de prioridade de saudação revisão para seus pontos de extremidade. Quando você seleciona Olá **prioridade** método de roteamento de tráfego, Olá ordem dos pontos de extremidade Olá selecionado faz diferença. Verifique se a ordem de prioridade de saudação de pontos de extremidade.  ponto de extremidade primário Hello está no topo. Clique duas vezes na ordem de saudação que é exibida. todas as solicitações serão roteadas toohello primeiro ponto de extremidade e se o Traffic Manager detecta sejam problemáticos, tráfego de saudação passam automaticamente toohello próximo ponto de extremidade. 
7. toochange Olá ordem de prioridade de ponto de extremidade, clique em ponto de extremidade Olá e em Olá **ponto de extremidade** folha que é exibida, clique em **editar** e alterar Olá **prioridade** valor conforme necessário . 
8. Clique em **salvar** toosave alterar configurações de ponto de extremidade de saudação.
9. Depois de concluir as alterações de configuração, clique em **salvar** final Olá Olá página.
10. Teste alterações de saudação em sua configuração da seguinte maneira:
    1.  Na barra de pesquisa do portal Olá, procurar por nome de perfil do Traffic Manager hello e clique em perfil do Traffic Manager Olá nos resultados de saudação que Olá exibido.
    2.  Em Olá **Traffic Manager** folha de perfil, clique em **visão geral**.
    3.  Olá **perfil do Traffic Manager** folha exibe o nome DNS de saudação do perfil do Traffic Manager recém-criado. Isso pode ser usado por qualquer clientes (por exemplo, navegando tooit usando um navegador da web) tooget roteada toohello certo ponto de extremidade conforme determinado pelo tipo de roteamento hello. Nesse caso todas as solicitações são roteadas toohello primeiro ponto de extremidade e se o Traffic Manager detecta sejam problemáticos, tráfego de saudação passam automaticamente toohello próximo ponto de extremidade.
11. Depois que o perfil do Traffic Manager está funcionando, edite o registro DNS de saudação no seu toopoint de servidor DNS autoritativo seu nome de domínio da empresa domínio nome toohello Gerenciador de tráfego.

![Configurando o método de roteamento de tráfego de prioridade usando o Gerenciador de Tráfego][1]

## <a name="next-steps"></a>Próximas etapas


- Saiba mais sobre o [método de roteamento de tráfego ponderado](traffic-manager-configure-weighted-routing-method.md).
- Saiba mais sobre o [método de roteamento de desempenho](traffic-manager-configure-performance-routing-method.md).
- Saiba mais sobre o [método de roteamento geográfico](traffic-manager-configure-geographic-routing-method.md).
- Saiba como muito[testar as configurações do Gerenciador de tráfego](traffic-manager-testing-settings.md).

<!--Image references-->
[1]: ./media/traffic-manager-priority-routing-method/traffic-manager-priority-routing-method.png