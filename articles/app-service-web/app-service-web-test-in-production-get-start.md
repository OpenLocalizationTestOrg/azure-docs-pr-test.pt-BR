---
title: "aaaGet de Introdução ao teste em produção para aplicativos Web"
description: "Saiba mais sobre Olá teste no recurso de produção (dica) em aplicativos de Web do serviço de aplicativo do Azure."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 4623468d-886e-4203-8012-8f86deb2790b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: cephalin
ms.openlocfilehash: 2ddbd532ffe2a4f3e07fd386d9741a3fde3639ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-test-in-production-for-web-apps"></a>Introdução ao teste em produção para Aplicativos Web
O teste em produção, ou teste dinâmico do seu aplicativo Web usando o tráfego do cliente em tempo real, é uma estratégia de teste que está cada vez mais sendo integrada pelos desenvolvedores de aplicativos em sua metodologia de [desenvolvimento ágil](https://en.wikipedia.org/wiki/Agile_software_development) . Ele permite tootest qualidade de saudação de seus aplicativos com o tráfego de usuário em tempo real em seu ambiente de produção, como toosynthesized contrário dados em um ambiente de teste. Ao expor os novos usuários tooreal aplicativo, você pode ser informados no problemas reais hello, que seu aplicativo pode enfrentar quando ele é implantado. Você pode verificar a funcionalidade de hello, desempenho e valor de suas atualizações de aplicativo no volume hello, a velocidade e a variedade de tráfego de usuário real, o que você nunca pode aproximar-se em um ambiente de teste.

## <a name="traffic-routing-in-app-service-web-apps"></a>Roteamento de Tráfego nos Aplicativos Web do Serviço de Aplicativo
Com hello roteamento de tráfego de recursos em [do serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714), você pode direcionar uma parte de tooone de tráfego do usuário em tempo real ou mais [slots de implantação](web-sites-staged-publishing.md)e, em seguida, analisar seu aplicativo com [aplicativo do Azure Insights](/services/application-insights/) ou [do Azure HDInsight](/services/hdinsight/), ou uma ferramenta de terceiros, como [New Relic](/marketplace/partners/newrelic/newrelic/) toovalidate sua alteração. Por exemplo, você pode implementar Olá os seguintes cenários com o serviço de aplicativo:

* Descobrir bugs funcionais ou identificar afunilamentos de desempenho em sua implantação de todo o toosite atualizações anteriores
* Executar "teste controlado voos" alterações medindo métricas de usabilidade Olá beta aplicativo
* Aumentar gradualmente tooa nova atualização e normalmente de volta para a versão atual do toohello se ocorrer um erro 
* Otimize os resultados de negócios do seu aplicativo executando [testes A/B](https://en.wikipedia.org/wiki/A/B_testing) ou [testes multivariados](https://en.wikipedia.org/wiki/Multivariate_testing_in_marketing) em vários slots de implantação

### <a name="requirements-for-using-traffic-routing-in-web-apps"></a>Requisitos para usar o Roteamento de Tráfego em Aplicativos Web
* Seu aplicativo Web deve ser executado na camada **Standard** ou **Premium**, pois ela é necessária para vários slots de implantação.
* Em ordem toowork corretamente, roteamento de tráfego exige toobe cookies habilitado no navegador Olá dos usuários. Roteamento de tráfego usa cookies toopin um slot de implantação do cliente navegador tooa para sessão de cliente de Olá Olá vida.
* O Roteamento de Tráfego dá suporte a cenários avançados do TiP por meio de cmdlets do Azure PowerShell.

## <a name="route-traffic-segment-tooa-deployment-slot"></a>Slot de implantação tooa do segmento de tráfego de rota
No nível básico de saudação em cada cenário de ponta, é possível rotear um percentual predefinido do seu slot de implantação de produção não tooa tráfego ao vivo. toodo isso, execute Olá estas etapas abaixo:

> [!NOTE]
> Olá etapas aqui pressupõe que você já tem um [slot de implantação de produção não](web-sites-staged-publishing.md) e que Olá desejado de conteúdo do aplicativo web já está [implantado](web-sites-deploy.md) tooit.
> 
> 

1. Faça logon no hello [Portal do Azure](https://portal.azure.com/).
2. Na folha de seu aplicativo Web, clique em **Configurações** > **Roteamento de Tráfego**.
   ![](./media/app-service-web-test-in-production/01-traffic-routing.png)
3. Slot de saudação selecione que você deseja tooroute tráfego tooand Olá porcentagem Olá total tráfego é desejado e clique em **salvar**.
   
    ![](./media/app-service-web-test-in-production/02-select-slot.png)
4. Vá folha do slot de implantação toohello. Agora você deve ver o tráfego em tempo real que está sendo roteado tooit.
   
    ![](./media/app-service-web-test-in-production/03-traffic-routed.png)

Depois da configuração do roteamento de tráfego, Olá especificado percentual de clientes serão tooyour aleatoriamente roteados slot de não produção. No entanto, é importante toonote que depois que um cliente é slot específico tooa automaticamente roteado, será toothat "fixo" slot para vida Olá dessa sessão de cliente. Isso usando uma sessão de usuário do cookie toopin hello. Se você inspecionar solicitações Olá HTTP, você encontrará um `TipMix` cookie em cada solicitação subsequente.

![](./media/app-service-web-test-in-production/04-tip-cookie.png)

## <a name="force-client-requests-tooa-specific-slot"></a>Forçar slot específico de tooa de solicitações de cliente
Em adição tooautomatic roteamento de tráfego, o serviço de aplicativo é slot específico do tooa tooroute capaz de solicitações. Isso é útil quando você deseja que seu tooopt capaz de toobe usuários-para ou sair do aplicativo beta. toodo isso, use Olá `x-ms-routing-name` parâmetro de consulta.

tooreroute usuários tooa slot específico usando `x-ms-routing-name`, você deve assegurar-se de que slot Olá já foi adicionada a lista de roteamento de tráfego toohello. Como você deseja tooroute tooa slot explicitamente, não importa porcentagem roteamento real Olá definida por você. Se desejar, você pode criar um "link beta" que os usuários podem clicar tooaccess Olá aplicativo beta.

![](./media/app-service-web-test-in-production/06-enable-x-ms-routing-name.png)

### <a name="opt-users-out-of-beta-app"></a>Recusar usuários do aplicativo beta
usuários toolet recusar a seu aplicativo beta, por exemplo, você pode colocar esse link na página da web:

    <a href="<webappname>.azurewebsites.net/?x-ms-routing-name=self">Go back tooproduction app</a>

Olá a cadeia de caracteres `x-ms-routing-name=self` Especifica o slot de produção de hello. Após hello link de saudação do acesso do navegador cliente, não apenas ele redirecionado toohello slot de produção, mas todas as solicitações subsequentes irão conter Olá `x-ms-routing-name=self` cookie que fixa o slot de produção Olá sessão toohello.

![](./media/app-service-web-test-in-production/05-access-production-slot.png)

### <a name="opt-users-in-toobeta-app"></a>Aceitar usuários no aplicativo toobeta
aceitar usuários toolet tooyour beta aplicativos, conjunto Olá mesmo consultar o nome do parâmetro toohello do slot de não produção de hello, por exemplo:

        <webappname>.azurewebsites.net/?x-ms-routing-name=staging

## <a name="more-resources"></a>Mais recursos
* [Configurar ambientes de preparo para aplicativos Web no Serviço de Aplicativo do Azure](web-sites-staged-publishing.md)
* [Implantar um aplicativo complexo de modo previsível no Azure](app-service-deploy-complex-application-predictably.md)
* [Desenvolvimento de software Agile com o Serviço de Aplicativo do Azure](app-service-agile-software-development.md)
* [Usar ambientes de Operações de Desenvolvimento com eficiência em seus aplicativos Web](app-service-web-staged-publishing-realworld-scenarios.md)

