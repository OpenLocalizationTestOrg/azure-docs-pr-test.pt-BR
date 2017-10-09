---
title: "usando o Azure Traffic Manager do método de roteamento de tráfego aaaConfigure geográfica | Microsoft Docs"
description: "Este artigo explica como tooconfigure Olá método de roteamento de tráfego geográficos usando o Azure Traffic Manager"
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
ms.date: 03/22/2017
ms.author: kumud
ms.openlocfilehash: 4142389211ae54e7feea6564641e01e4477491e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-geographic-traffic-routing-method-using-traffic-manager"></a>Configurar o método de roteamento de tráfego geográfico do hello usando o Gerenciador de tráfego

Olá método de roteamento de tráfego geográfica permite que o tráfego do toodirect toospecific pontos de extremidade com base na localização geográfica hello, onde são originados de solicitações de saudação. Este tutorial mostra como toocreate um Gerenciador de tráfego de perfil com esse método de roteamento e configurar o tráfego de tooreceive Olá pontos de extremidade de regiões geográficas específicas.

## <a name="create-a-traffic-manager-profile"></a>Criar um perfil do Gerenciador de Tráfego

1. Em um navegador, entrar toohello [portal do Azure](http://portal.azure.com). Caso ainda não tenha uma conta, você pode se inscrever para obter uma [avaliação gratuita por um mês](https://azure.microsoft.com/free/).
2. No menu de Hub hello, clique em **novo** > **rede** > **ver todos os**e, em seguida, clique em **perfil do Traffic Manager**Olá tooopen **perfil do Traffic Manager criar** folha.
3. Em Olá **perfil do Traffic Manager criar** folha:
    1. Forneça um nome para seu perfil. Esse nome precisa toobe exclusivos dentro de saudação trafficmanager.net região e resultará em nome DNS Olá <profilename>, trafficmanager.net que ser usadas tooaccess perfil do Traffic Manager.
    2. Selecione Olá **geográfico** método de roteamento.
    3. Selecione a assinatura de saudação em que deseja toocreate esse perfil.
    4. Use um grupo de recursos existente ou crie um novo tooplace de grupo de recursos esse perfil em. Se você escolher toocreate um novo grupo de recursos, use Olá **local do grupo de recursos** local de saudação toospecify suspensa saudação do grupo de recursos. Essa configuração se refere local toohello saudação do grupo de recursos e não tem impacto sobre Olá perfil do Traffic Manager que será implantado globalmente.
    5. Depois de clicar em **Criar**, seu perfil do Gerenciador de Tráfego será criado e implantada globalmente.

![Criar um perfil do Gerenciador de Tráfego](./media/traffic-manager-geographic-routing-method/create-traffic-manager-profile.png)

## <a name="add-endpoints"></a>Adicionar pontos de extremidade

1. Pesquisar por nome do perfil do Traffic Manager Olá que você acabou de criar na barra de pesquisa do portal hello e clique no resultado de saudação quando ele for exibido.
2. Navegue muito**configurações** -> **pontos de extremidade** na folha de Gerenciador de tráfego de saudação.
3. Clique em **adicionar** tooshow Olá **Adicionar ponto de extremidade** folha.
3. Em Olá **pontos de extremidade** folha, clique em **adicionar** e em Olá **Adicionar ponto de extremidade** folha que é exibida, preencha o seguinte:
4. Selecione **tipo** dependendo do tipo de saudação do ponto de extremidade que você está adicionando. Para perfis de roteamento geográfico usados na produção, é altamente recomendável usar tipos de ponto de extremidade aninhados que contenham um perfil filho com mais de um ponto de extremidade. Para obter mais detalhes, confira as [perguntas frequentes sobre métodos de roteamento de tráfego geográfico](traffic-manager-FAQs.md).
5. Forneça um **nome** pelo qual você deseja toorecognize esse ponto de extremidade.
6. Determinados campos nessa folha dependem do tipo de saudação do ponto de extremidade que você está adicionando:
    1. Se você estiver adicionando um ponto de extremidade do Azure, selecione Olá **tipo de recurso de destino** e hello **destino** com base em recurso Olá deseja tráfego toodirect
    2. Se você estiver adicionando um **externo** ponto de extremidade, fornecer Olá **o nome de domínio totalmente qualificado (FQDN)** para seu ponto de extremidade.
    3. Se você estiver adicionando um **ponto de extremidade aninhadas**, selecione Olá **recurso de destino** que corresponde o perfil toohello filho deseja toouse e especificar Olá **decontagemdepontosdeextremidadedomínimofilho**.
7. No hello seção de mapeamento de localização geográfica, use Olá suspenso de regiões de saudação tooadd de onde você deseja que o ponto de extremidade do tráfego enviado de toobe toothis. Você deve adicionar pelo menos uma região e pode ter várias regiões mapeadas.
8. Repita essa etapa para todos os pontos de extremidade você deseja tooadd sob esse perfil

![Adicionar um ponto de extremidade do Gerenciador de Tráfego](./media/traffic-manager-geographic-routing-method/add-traffic-manager-endpoint.png)

## <a name="use-hello-traffic-manager-profile"></a>Usar perfil do Traffic Manager Olá
1.  Na barra de pesquisa do portal hello, procure Olá **perfil do Traffic Manager** nome que criado na saudação anterior seção e clique no perfil do Gerenciador de tráfego de saudação em Olá resultados que Olá exibido.
2. Em Olá **perfil do Traffic Manager** folha, clique em **visão geral**.
3. Olá **perfil do Traffic Manager** folha exibe o nome DNS de saudação do perfil do Traffic Manager recém-criado. Isso pode ser usado por qualquer clientes (por exemplo, navegando tooit usando um navegador da web) tooget roteada toohello certo ponto de extremidade conforme determinado pelo tipo de roteamento hello.  No caso de saudação de roteamento geográfico, Traffic Manager analisa Olá IP de origem da solicitação de entrada hello e determina a região de saudação do qual ele é de origem. Se essa região é o ponto de extremidade de tooan mapeado, o tráfego é roteado toothere. Se esta região não está mapeada tooan de ponto de extremidade, o Traffic Manager retorna uma resposta de consulta NODATA.

## <a name="next-steps"></a>Próximas etapas

- Saiba mais sobre [Método de roteamento de tráfego geográfico](traffic-manager-routing-methods.md#geographic).
- Saiba como muito[testar as configurações do Gerenciador de tráfego](traffic-manager-testing-settings.md).
