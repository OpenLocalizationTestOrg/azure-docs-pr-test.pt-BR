---
title: "aaaHow tooScale um aplicativo em um ambiente de serviço de aplicativo"
description: "Escalando um aplicativo em um Ambiente do Serviço de Aplicativo"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: jimbe
ms.assetid: 78eb1e49-4fcd-49e7-b3c7-f1906f0f22e3
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/17/2016
ms.author: ccompy
ms.openlocfilehash: 08916eac056c46bf8cb6edffbf96285317b32062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-apps-in-an-app-service-environment"></a>Escalando aplicativos em um Ambiente do Serviço de Aplicativo
Saudação do serviço de aplicativo do Azure há normalmente três itens, que você pode dimensionar:

* plano de preços
* tamanho do trabalho 
* número de instâncias.

Em uma ASE, não há nenhuma necessidade tooselect ou alterar Olá preços do plano.  Em termos de recursos, ele já está no nível de recurso de preços Premium.  

Com respeito tooworker tamanhos, Olá ASE administrador pode atribuir o tamanho de saudação do hello toobe de recursos de computação usada para cada pool de trabalho.  Isso significa que você pode ter o Pool de Trabalhadores 1 com recursos de computação P4 e o Pool de Trabalhadores 2 com recursos de computação P1, se desejado.  Eles não têm toobe na ordem de tamanho.  Para obter detalhes sobre tamanhos de saudação e seus preços documento hello aqui, consulte [preços de serviço de aplicativo do Azure][AppServicePricing].  Isso deixa Olá opções de dimensionamento para aplicativos web e planos de serviço de aplicativo em um ambiente de serviço de aplicativo toobe:

* seleção do pool de trabalhadores
* número de instâncias

Alterar o item é feito por meio de saudação apropriado de interface de usuário para seu ASE hospedado planos de serviço de aplicativo.  

![][1]

Você não pode expandir o ASP além do número de saudação de recursos de computação disponíveis no pool do trabalhador Olá que o ASP está em.  Se você precisar de recursos nesse pool de trabalho de computação precisa tooget seu tooadd de administrador ASE-los.  Para obter informações em torno de reconfiguração seu ASE Leia informações Olá aqui: [como um ambiente de serviço de aplicativo de tooConfigure][HowtoConfigureASE].  Também convém tootake aproveitar Olá com base em agendamento ou métricas de capacidade de tooadd ASE AutoEscala recursos.  tooget para ver mais detalhes sobre como configurar o dimensionamento automático para o ambiente de saudação ASE próprio [como tooconfigure AutoEscala para um ambiente de serviço de aplicativo][ASEAutoscale].

Você pode criar aplicativos de vários planos de serviço usando os recursos de computação de pools de trabalho diferente, ou você pode usar Olá mesmo pool de trabalho.  Por exemplo, se você tiver recursos de computação disponíveis (10) no trabalho Pool 1, você pode escolher o plano de serviço de um aplicativo toocreate usando os recursos de computação (6) e um serviço de aplicativo de segundo plano que usa os recursos de computação (4).

### <a name="scaling-hello-number-of-instances"></a>Escalonar Olá número de instâncias
Quando você cria seu aplicativo Web em um Ambiente do Serviço de Aplicativo, ele começa com uma instância.  Você pode expandir tooadditional tooprovide de instâncias adicional de computação recursos para seu aplicativo.   

Se seu ASE tiver capacidade suficiente, isso é muito simples.  Você vai tooyour plano de serviço aplicativo que contém sites Olá você deseja tooscale backup e selecione a escala.  Isso abre a saudação da interface do usuário em que você pode definir escala Olá para o ASP ou configurar regras de dimensionamento automático para o ASP manualmente.  seu aplicativo simplesmente conjunto de escalas de toomanually ***o dimensionamento por*** muito***uma contagem de instâncias que inseri manualmente***.  Daqui arraste quantity do hello controle deslizante toohello desejado ou insira Olá caixa próxima toohello controle deslizante.  

![][2] 

regras de AutoEscala Olá para um ASP em um trabalho ASE Olá mesmo que eles normalmente.  É possível selecionar ***Percentual de CPU*** em ***Escalar por*** e criar regras de autoescala para o ASP com base no percentual de CPU ou criar regras mais complexas usando ***regras de agendamento e desempenho***.  toosee concluir mais detalhes sobre como configurar o guia de saudação de uso de dimensionamento automático aqui [dimensionar um aplicativo de serviço de aplicativo do Azure][AppScale]. 

### <a name="worker-pool-selection"></a>seleção do pool de trabalhadores
Conforme observado anteriormente, seleção de pool do trabalhador Olá é acessada de saudação ASP da interface do usuário.  Abra a folha de saudação para Olá ASP que você deseja tooscale e selecione o pool de trabalho.  Você verá todos os pools de trabalhadores Olá que você configurou em seu ambiente de serviço de aplicativo.  Se você tiver somente um trabalhador pool, em seguida, você só verá um pool de saudação listado.  toochange o ASP do pool que trabalho está em, basta selecionar pool de trabalho Olá você deseja que seu toomove plano do serviço de aplicativo para.  

![][3]

Antes de mover o ASP do trabalho de um pool tooanother é importante toomake-se de que você terá a capacidade adequada para o ASP.  Na lista de saudação de pools de trabalho, não só é o nome do pool de trabalho Olá listado, mas você também pode ver quantos operadores estão disponíveis nesse pool de trabalho.  Certifique-se de que há suficiente toocontain de instâncias disponíveis seu plano de serviço de aplicativo.  Se você precisa de mais recursos de computação no pool do trabalhador Olá desejar toomove para, em seguida, obter seu tooadd de administrador ASE-los.  

> [!NOTE]
> Mover um ASP do pool de um trabalho fará com que a frio inicia de saudação aplicativos em que o ASP.  Isso pode causar toorun de solicitações lenta como seu aplicativo está frio iniciado em novos recursos de computação hello.  Olá inicialização a frio pode ser evitada usando Olá [passiva, o recurso de aplicativo] [ AppWarmup] no serviço de aplicativo do Azure.  módulo de inicialização do aplicativo Hello descrito no artigo Olá também funciona para frios porque o processo de inicialização de saudação também é chamado quando os aplicativos estão frios iniciado em novos recursos de computação. 
> 
> 

## <a name="getting-started"></a>Introdução
tooget iniciado com ambientes de serviço de aplicativo, consulte [como tooCreate um ambiente de serviço de aplicativo][HowtoCreateASE]

Para obter mais informações sobre a plataforma do serviço de aplicativo do Azure hello, consulte [do serviço de aplicativo do Azure][AzureAppService].

<!--Image references-->
[1]: ./media/app-service-web-scale-a-web-app-in-an-app-service-environment/aseappscale-aspblade.png
[2]: ./media/app-service-web-scale-a-web-app-in-an-app-service-environment/aseappscale-manualscale.png
[3]: ./media/app-service-web-scale-a-web-app-in-an-app-service-environment/aseappscale-sizescale.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[ScaleWebapp]: http://azure.microsoft.com/documentation/articles/web-sites-scale/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[HowtoConfigureASE]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
[CreateWebappinASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-a-web-app-in-an-ase/
[Appserviceplans]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/ 
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[AppScale]: http://azure.microsoft.com/documentation/articles/web-sites-scale/
[AppWarmup]: http://ruslany.net/2015/09/how-to-warm-up-azure-web-app-during-deployment-slots-swap/
