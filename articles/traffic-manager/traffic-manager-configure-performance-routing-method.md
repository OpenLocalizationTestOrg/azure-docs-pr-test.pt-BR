---
title: "usando o Azure Traffic Manager do método de roteamento de tráfego de desempenho aaaConfigure | Microsoft Docs"
description: "Este artigo explica como tooconfigure tooroute Traffic Manager tráfego toohello de ponto de extremidade com a menor latência"
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
ms.openlocfilehash: d0ccd4c9de411844c6f36068859265244f4aa52b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-performance-traffic-routing-method"></a>Configurar o método de roteamento de tráfego Olá desempenho

Olá método de roteamento de tráfego de desempenho permite ponto de extremidade do toodirect tráfego toohello com a menor latência Olá da rede saudação do cliente. Normalmente, Olá datacenter com a menor latência de saudação é hello mais próximo na distância geográfica. Esse método de roteamento de tráfego não consegue considerar as alterações em tempo real à configuração ou à carga de rede.

##  <a name="tooconfigure-performance-routing-method"></a>método de roteamento de desempenho tooconfigure

1. Em um navegador, entrar toohello [portal do Azure](http://portal.azure.com). Caso ainda não tenha uma conta, você pode se inscrever para obter uma [avaliação gratuita por um mês](https://azure.microsoft.com/free/). 
2. Na barra de pesquisa do portal hello, procure Olá **perfis do Traffic Manager** e clique em nome do perfil Olá que você deseja que o método de roteamento de saudação tooconfigure para.
3. Em Olá **perfil do Traffic Manager** folha, verifique se ambos Olá serviços de nuvem e sites que você deseja tooinclude em sua configuração estão presentes.
4. Em Olá **configurações** seção, clique em **configuração**e em Olá **configuração** folha, completa, da seguinte maneira:
    1. Em **Configurações do método de roteamento de tráfego**, para **Método de roteamento** selecione **Desempenho**.
    2. Saudação de conjunto **as configurações do monitor de ponto de extremidade** idênticos para todos os cada ponto de extremidade neste perfil da seguinte maneira:
        1. Selecione Olá apropriado **protocolo**e especifique Olá **porta** número. 
        2. Para **Caminho**, digite uma barra "/" */*. pontos de extremidade toomonitor, você deve especificar um caminho e nome de arquivo. A barra "/" é uma entrada válida para o caminho relativo do hello e indica se o arquivo hello está no diretório raiz de saudação (padrão).
        3. Na parte superior de saudação da página de saudação, clique em **salvar**.
5.  Teste alterações de saudação em sua configuração da seguinte maneira:
    1.  Na barra de pesquisa do portal Olá, procurar por nome de perfil do Traffic Manager hello e clique em perfil do Traffic Manager Olá nos resultados de saudação que Olá exibido.
    2.  Em Olá **Traffic Manager** folha de perfil, clique em **visão geral**.
    3.  Olá **perfil do Traffic Manager** folha exibe o nome DNS de saudação do perfil do Traffic Manager recém-criado. Isso pode ser usado por qualquer clientes (por exemplo, navegando tooit usando um navegador da web) tooget roteada toohello certo ponto de extremidade conforme determinado pelo tipo de roteamento hello. Nesse caso, todas as solicitações são toohello roteado de ponto de extremidade com a menor latência Olá da rede saudação do cliente.
6. Depois que o perfil do Traffic Manager está funcionando, edite o registro DNS de saudação no seu toopoint de servidor DNS autoritativo seu nome de domínio da empresa domínio nome toohello Gerenciador de tráfego.

![Configurando o método de roteamento de tráfego de desempenho usando o Gerenciador de Tráfego][1]

## <a name="next-steps"></a>Próximas etapas

- Saiba mais sobre o [método de roteamento de tráfego ponderado](traffic-manager-configure-weighted-routing-method.md).
- Saiba mais sobre o [método de roteamento de prioridade](traffic-manager-configure-priority-routing-method.md).
- Saiba mais sobre o [método de roteamento geográfico](traffic-manager-configure-geographic-routing-method.md).
- Saiba como muito[testar as configurações do Gerenciador de tráfego](traffic-manager-testing-settings.md).

<!--Image references-->
[1]: ./media/traffic-manager-performance-routing-method/traffic-manager-performance-routing-method.png