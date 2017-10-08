---
title: "aaaCreate um aplicativo web em um ambiente de serviço de aplicativo v1"
description: "Saiba como toocreate web apps e planos de serviço de aplicativo em um ambiente de serviço de aplicativo v1"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: 983ba055-e9e4-495a-9342-fd3708dcc9ac
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/11/2017
ms.author: ccompy
ms.openlocfilehash: 322ef344517c54247b102fb4920e35645986ef98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-in-an-app-service-environment-v1"></a>Criar um aplicativo Web em um Ambiente do Serviço de Aplicativo v1

> [!NOTE]
> Este artigo é sobre Olá v1 do ambiente de serviço de aplicativo.  Há uma versão mais recente do hello ambiente de serviço de aplicativo que é mais fácil toouse e é executado na infraestrutura mais avançada. toolearn mais sobre a nova versão de hello começam com hello [Introdução toohello ambiente de serviço de aplicativo](../app-service/app-service-environment/intro.md).
> 

## <a name="overview"></a>Visão geral
Este tutorial mostra como toocreate de aplicativos web e planos de serviço de aplicativo em um [v1 do ambiente de serviço de aplicativo](app-service-app-service-environment-intro.md) (ASE). 

> [!NOTE]
> Se você quiser toolearn como toocreate um aplicativo web, mas não é necessário toodo-lo em um ambiente de serviço de aplicativo, consulte [criar um aplicativo web .NET](app-service-web-get-started-dotnet.md) ou uma saudação relacionados tutoriais para outros idiomas e estruturas.
> 
> 

## <a name="prerequisites"></a>Pré-requisitos
Este tutorial supõe que você tenha criado um Ambiente de Serviço de Aplicativo. Se você ainda não tiver feito isso, consulte [Criar um Ambiente de Serviço de Aplicativo](app-service-web-how-to-create-an-app-service-environment.md). 

## <a name="create-a-web-app"></a>Criar um aplicativo Web
1. Em Olá [Portal do Azure](https://portal.azure.com/), clique em **Novo > Web + móvel > aplicativo Web**. 
   
    ![][1]
2. Selecione sua assinatura.  
   
    Se você tiver várias assinaturas esteja ciente de que toocreate um aplicativo em seu ambiente de serviço de aplicativo, você precisa toouse Olá a mesma assinatura que você usou ao criar o ambiente de saudação. 
3. Selecione ou crie um grupo de recursos.
   
    *Grupos de recursos* habilitar você toomanage relacionadas a recursos do Azure como uma unidade e são úteis ao estabelecer *controle de acesso baseado em função* regras (RBAC) para seus aplicativos. Para saber mais, confira [Visão geral do Azure Resource Manager][ResourceGroups]. 
4. Selecione ou crie um plano do Serviço de Aplicativo.
   
    *planos do Serviço de Aplicativo* são conjuntos gerenciados de aplicativos Web.  Normalmente quando você seleciona a preços, preço Olá cobrado é aplicado toohello o plano do serviço de aplicativo em vez de aplicativos individuais toohello. Em uma ASE pagar para computação Olá instâncias alocadas toohello ASE em vez do que você tenha listado com o ASP.  tooscale número Olá de instâncias de um aplicativo web dimensionar as instâncias de saudação do seu plano de serviço de aplicativo e afeta todos os aplicativos da web de saudação no plano.  Alguns recursos, como a integração de rede virtual ou de slots do site também têm restrições de quantidade no plano de saudação.  Para saber mais, consulte [Visão geral de planos do Serviço de Aplicativo do Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)
   
    Você pode identificar Olá que planos de serviço de aplicativo em seu ASE examinando o local de saudação que é observado em nome do plano de saudação.  
   
    ![][5]
   
    Se você quiser toouse um plano de serviço de aplicativo que já existe no seu ambiente de serviço de aplicativo, selecione-o. Se você quiser toocreate um novo plano de serviço de aplicativo, consulte Olá deste tutorial, a seção seguinte [criar um plano de serviço de aplicativo em um ambiente de serviço de aplicativo](#createplan).
5. Insira nome de saudação para seu aplicativo web e, em seguida, clique em **criar**. 
   
    Se seu ASE usa uma URL de saudação do VIP externo de um aplicativo em uma ASE é: [*sitename*]. [ *nome do seu ambiente de serviço de aplicativo*]. p.azurewebsites.net em vez de [*sitename*]. azurewebsites.net
   
    Se seu ASE usa uma URL interna VIP e Olá de um aplicativo que ASE é: [*sitename*]. [ *subdomínio especificado durante a criação de ASE*]   
    Depois de selecionar o ASP durante a criação do ASE você verá subdomínio Olá atualizar abaixo **nome**

## <a name="createplan"></a> Criar um plano do Serviço de Aplicativo
Quando você cria um plano do Serviço de Aplicativo em um Ambiente do Serviço de Aplicativo, as opções do seu trabalhador serão diferentes caso não haja trabalhadores compartilhados em um ASE.  trabalhadores Olá ter toouse são Olá aqueles que foram alocados ASE toohello pelo administrador hello.  Isso significa que toocreate um novo plano, é necessário mais que o número total de saudação de instâncias do pool de trabalho dos ASE trabalhadores alocados tooyour toohave em todos os seus planos já nesse pool de trabalho.  Se você não tem suficiente trabalhadores em seu toocreate de pool do trabalhador ASE seu plano, é necessário toowork com seu tooget de admin ASE-los adicionados.

Outra diferença com planos de serviço de aplicativo hospedado por um ambiente de serviço de aplicativo é a falta de saudação de preços de seleção.  Quando você tiver um ambiente de serviço de aplicativo você estiver pagando para recursos de computação usados pelo sistema hello e não tiver adicionados encargos para planos de saudação nesse ambiente.  Normalmente, quando você cria um plano do Serviço de Aplicativo, você seleciona um plano de preços que determina sua cobrança.  Um ambiente do serviço de aplicativo é essencialmente um local privado onde você pode criar conteúdo.  Você paga pelo ambiente de saudação e não toohost seu conteúdo.

Olá instruções a seguir mostram como toocreate um aplicativo de serviço plano enquanto você estiver criando um aplicativo web, como explicado na seção anterior de saudação tutorial hello.

1. Clique em **criar novo** em Olá plano seleção da interface do usuário e fornecer um nome para o plano como faria normalmente fora de uma ASE.
2. Selecione ASE Olá que você deseja toouse em sua seleção de local.
   
    Como um Ambiente do Serviço de Aplicativo é, essencialmente, um local de implantação particular, ele é mostrado no Local. 
   
    ![][2]
   
    Após a seleção de uma ASE no seletor de local de hello, Olá atualizações de interface do usuário de criação de plano do serviço de aplicativo.  local de saudação agora mostra nome de saudação do hello sistema ASE e região Olá está em e Olá seletor de plano de preços é substituído por um seletor de pool do trabalhador.  
   
    ![][3]

### <a name="selecting-a-worker-pool"></a>Selecionando o pool de trabalho
Normalmente, no serviço de aplicativo do Azure e fora de um ambiente de serviço de aplicativo, há 3 tamanhos de computação que estão disponíveis com a seleção de saudação de um plano de preço dedicado.  De maneira semelhante, para uma ASE você pode definir até too3 pools de trabalhadores e especificar o tamanho de computação de saudação que é usado para esse pool de trabalho.  Isso significa que para locatários de saudação ASE é que, em vez de selecionar um plano de preços com tamanho de computação para o plano de serviço de aplicativo, você seleciona o que é chamado de um *pool do trabalhador*.  

seleção de pool do trabalhador Olá interface do usuário mostra o tamanho de computação de saudação usado para esse pool de trabalho abaixo do nome de saudação.  Olá quantidade disponível refere-se toohow muitas instâncias de computação estão disponíveis para uso nesse pool.  pool total Hello, na verdade, pode ter mais instâncias que esse número, mas esse valor se refere a toosimply quantos não estão em uso.  Se você precisar tooadjust tooadd seu ambiente de serviço de aplicativo computação mais recursos, consulte [configurando seu ambiente de serviço de aplicativo](app-service-web-configure-an-app-service-environment.md).

![][4]

Neste exemplo, você verá apenas dois pools de trabalho disponíveis. Isso ocorre porque o administrador do ASE Olá alocados somente hosts nesses pools de dois trabalho.  Olá terceiro aparecerão quando houver VMs alocadas para ele.  

## <a name="after-web-app-creation"></a>Após a criação do aplicativo Web
Há algumas considerações para executar aplicativos da web e gerenciar planos de serviço de aplicativo em uma ASE que precisam toobe levada em conta.  

Conforme observado anteriormente, proprietário Olá Olá ASE é responsável por tamanho de saudação do sistema hello e assim eles também são responsáveis para garantir que existe suficiente Olá toohost de capacidade desejadas planos de serviço de aplicativo. Se não houver nenhum trabalhador disponível, você não poderá ser capaz de toocreate seu plano de serviço de aplicativo.  Isso também é verdadeiro tooscaling backup de seu aplicativo web.  Se precisar de mais instâncias, você teria tooget seu tooadd de administração do ambiente de serviço de aplicativo mais trabalhadores.

Depois de criar seu aplicativo web e o plano de serviço de aplicativo é uma boa ideia tooscale-o.  Em uma ASE é sempre necessário toohave pelo menos 2 instâncias de sua tolerância a falhas do serviço de aplicativo plano tooprovide para seus aplicativos.  Dimensionamento de um aplicativo de serviço plano em uma ASE é Olá mesmo normalmente por meio de saudação plano de serviço de aplicativo da interface do usuário.  Para obter mais informações sobre como dimensionar, [como tooscale um aplicativo web em um ambiente de serviço de aplicativo](app-service-web-scale-a-web-app-in-an-app-service-environment.md)

<!--Image references-->
[1]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createaspnewwebapp.png
[2]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createasplocation.png
[3]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createaspselected.png
[4]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/createaspworkerpool.png
[5]: ./media/app-service-web-how-to-create-a-web-app-in-an-ase/selectaspinase.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[Appserviceplans]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[HowtoScale]: http://azure.microsoft.com/documentation/articles/app-service-web-scale-a-web-app-in-an-app-service-environment
[HowtoConfigureASE]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment
[ResourceGroups]: ../azure-resource-manager/resource-group-overview.md
[AzurePowershell]: http://azure.microsoft.com/documentation/articles/powershell-install-configure/
