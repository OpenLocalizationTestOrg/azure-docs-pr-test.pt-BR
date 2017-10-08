---
title: "aaaCreate um ambiente de serviço de aplicativo do Azure externo"
description: "Explica como toocreate um ambiente de serviço de aplicativo ao criar um aplicativo ou autônomo"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 94dd0222-b960-469c-85da-7fcb98654241
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: f8619534ddd889ea65063733ac6ec11b206e799c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-external-app-service-environment"></a>Como criar um ambiente externo do Serviço de Aplicativo #

O Ambiente do Serviço de Aplicativo do Azure é uma implantação do Serviço de Aplicativo do Azure em uma sub-rede de uma VNet (rede virtual) do Azure. Há dois toodeploy de maneiras de um ambiente de serviço de aplicativo (ASE):

- Com um VIP em um endereço IP externo, geralmente chamado de ASE externo.
- Com hello VIP em um endereço IP interno, geralmente chamado uma ASE ILB, porque o ponto de extremidade interno Olá é um balanceador de carga interno (ILB).

Este artigo mostra como toocreate uma ASE externo. Para obter uma visão geral de saudação ASE, consulte [toohello uma introdução ambiente de serviço de aplicativo][Intro]. Para obter informações sobre como toocreate um ILB ASE, consulte [criar e usar uma ASE ILB][MakeILBASE].

## <a name="before-you-create-your-ase"></a>Antes de criar seu ASE ##

Depois de criar seu ASE, você não pode alterar a seguir hello:

- Local
- Assinatura
- Grupo de recursos
- VNET usada
- Sub-rede usada
- Tamanho da sub-rede

> [!NOTE]
> Quando você escolhe uma rede virtual e especifique uma sub-rede, certifique-se de que é grande o suficiente tooaccommodate futuro crescimento. Recomendamos um tamanho de `/25`, com 128 endereços.
>

## <a name="three-ways-toocreate-an-ase"></a>Três maneiras toocreate uma ASE ##

Há uma ASE toocreate de três maneiras:

- **Durante a criação de um plano do serviço de aplicativo**. Esse método cria Olá ASE e hello plano de serviço de aplicativo em uma única etapa.
- **Como uma ação autônoma**. Este método cria um ASE autônomo, que é um ASE em branco. Esse método é um toocreate de processo uma ASE mais avançado. Use-toocreate uma ASE com um ILB.
- **De um modelo do Azure Resource Manager**. Esse método é para usuários avançados. Para obter mais informações, confira [Como criar um ASE a partir de um modelo][MakeASEfromTemplate].

Uma ASE externo tem um VIP público, o que significa que todos os aplicativos de toohello de tráfego HTTP/HTTPS no hello ASE atinge um endereço IP acessível pela internet. Uma ASE com um ILB tem um endereço IP da sub-rede Olá usado pelo Olá ASE. Olá aplicativos hospedados em uma ASE ILB não são expostos toohello diretamente à internet.

## <a name="create-an-ase-and-an-app-service-plan-together"></a>Criar um ASE e um plano do Serviço de Aplicativo simultaneamente ##

Olá plano de serviço de aplicativo é um contêiner de aplicativos. Ao criar um aplicativo no serviço de aplicativo, você escolhe ou cria um plano do serviço de aplicativo. ambientes de modelo do contêiner de saudação manter planos de serviço de aplicativo e planos de serviço de aplicativo mantenha aplicativos.

toocreate uma ASE durante a criação de um plano de serviço de aplicativo:

1. Em Olá [portal do Azure](https://portal.azure.com/), selecione **novo** > **Web + móvel** > **aplicativo Web**.

    ![Criação de um aplicativo Web][1]

2. Selecione sua assinatura. aplicativo Hello e Olá ASE são criados no hello mesmo assinaturas.

3. Selecione ou crie um grupo de recursos. Você pode usar os grupos de recursos para gerenciar recursos relacionados do Azure como uma unidade. Os grupos de recursos são úteis quando deseja estabelecer regras de controle de acesso baseado em função nos seus aplicativos. Para obter mais informações, consulte Olá [visão geral do Gerenciador de recursos do Azure][ARMOverview].

4. Selecione Olá plano de serviço de aplicativo e, em seguida, selecione **criar novo**.

    ![Plano do serviço de aplicativo novo][2]

5. Em Olá **local** lista suspensa, região hello selecione onde você deseja toocreate Olá ASE. Se você selecionar um ASE existente, não será criado um novo ASE. Olá plano de serviço de aplicativo é criado no hello ASE que você selecionou. 

6. Selecione **preço**e escolha uma saudação **isolado** SKUs de preços. Se você escolher um cartão SKU **isolado** e um local que não seja um ASE; será criado um ASE novo no local. Selecione toostart Olá processo toocreate uma ASE **selecione**. Olá **isolado** SKU está disponível somente em conjunto com uma ASE. Também não é possível usar nenhum outro SKU de preços em um ASE além do **isolado**.

    ![Seleção de tipo de preços][3]

7. Insira o nome de saudação para seu ASE. Esse nome é usado no nome de saudação endereçável para seus aplicativos. Se o nome de saudação do hello ASE é _appsvcenvdemo_, é o nome de domínio Olá *. appsvcenvdemo.p.azurewebsites.net*. Se você criar um aplicativo chamado *mytestapp*, ele será endereçável em mytestapp.appsvcenvdemo.p.azurewebsites.net. Você não pode usar o espaço em branco no nome da saudação. Se você usar caracteres maiusculos, o nome de domínio de saudação é versão minúscula total de saudação do nome.

    ![Nome do plano do serviço de aplicativo novo][4]

8. Especifica os detalhes da sua rede virtual do Azure. Escolha **Criar novo** ou **Selecionar existente**. Olá opção tooselect uma rede virtual existente está disponível somente se você tiver uma rede virtual na região selecionada da saudação. Se você selecionar **criar novo**, insira um nome para Olá VNet. Então, é criado um novo VNet do Resource Manager com o nome inserido. Ele usa o espaço de endereço Olá `192.168.250.0/23` na região selecionada da saudação. Se você escolher **Selecionar Existente**, precisará:

    a. Selecione o bloco de endereço de rede virtual hello, se você tiver mais de um.

    b. Digite um novo nome de sub-rede.

    c. Selecione o tamanho de saudação da sub-rede hello. *Lembre-se tooselect um tamanho grande o suficiente tooaccommodate futuro crescimento de sua ASE.* Recomendamos `/25`, que tem 128 endereços e pode manipular um ASE de tamanho máximo. Não recomendamos `/28`, por exemplo, porque tem somente 16 endereços disponíveis. Infraestrutura usa pelo menos cinco endereços. Em uma sub-rede `/28`, você tem um dimensionamento máximo de 11 instâncias.

    d. Selecione o intervalo IP de sub-rede hello.

9. Selecione **criar** toocreate Olá ASE. Esse processo também cria o plano de serviço de aplicativo hello e aplicativo hello. Olá ASE, o plano de serviço de aplicativo e o aplicativo estão sob Olá a mesma assinatura e também em Olá mesmo grupo de recursos. Se seu ASE precisa de um grupo de recursos separado ou se você precisar de uma ASE ILB, execute Olá etapas toocreate uma ASE por si só.

## <a name="create-an-ase-by-itself"></a>Criar um ASE sozinho ##

Se você criar um ASE autônomo, ele estará vazio. Uma ASE vazia ainda incorrerá em um custo mensal de infraestrutura de saudação. Siga essas etapas toocreate uma ASE com um ILB ou toocreate uma ASE em seu próprio grupo de recursos. Depois de criar seu ASE, você pode criar aplicativos nele usando o processo normal de saudação. Selecione seu novo ASE como local de saudação.

1. Pesquisa hello Azure Marketplace para **ambiente de serviço de aplicativo**, ou selecione **novo** > **Web móvel** > **do serviço de aplicativo Ambiente**. 

2. Digite o nome de saudação do seu ASE. Esse nome é usado para aplicativos de saudação criados no hello ASE. Se o nome da saudação é *mynewdemoase*, é o nome de subdomínio Olá *. mynewdemoase.p.azurewebsites.net*. Se você criar um aplicativo chamado *mytestapp*, ele será endereçável em mytestapp.mynewdemoase.p.azurewebsites.net. Você não pode usar o espaço em branco no nome da saudação. Se você usar caracteres maiusculos, o nome de domínio de saudação é Olá total minúsculas versão Olá nome. Se você usar um ILB, o nome do ASE não será usado no subdomínio, mas sim declarado explicitamente durante a criação do ASE.

    ![Nomenclatura ASE][5]

3. Selecione sua assinatura. Esta assinatura também é hello que todos os aplicativos em Olá ASE usar. Você não pode colocar o seu ASE em uma VNet que está em outra assinatura.

4. Selecione ou especifique um novo grupo de recursos. grupo de recursos de saudação usado para seu ASE deve ser Olá aquele mesmo que é usado para a sua rede virtual. Se você selecionar uma rede virtual existente, a seleção de grupo de recursos de saudação para seu ASE é tooreflect atualizado que sua rede virtual. *Você pode criar uma ASE com um grupo de recursos é diferente do grupo de recursos de rede virtual Olá se você usar um modelo do Gerenciador de recursos.* toocreate uma ASE de um modelo, consulte [criar um ambiente de serviço de aplicativo de um modelo][MakeASEfromTemplate].

    ![Seleção de grupo de recursos][6]

5. Selecione a VNet e o local. Você pode criar uma nova VNet ou selecionar uma VNet existente: 

    * Se selecionar uma VNet nova, você poderá especificar um nome e local. Olá nova rede virtual tem Olá endereço intervalo 192.168.250.0/23 e uma sub-rede denominada padrão. subrede Olá é definido como 192.168.250.0/24. Você só pode selecionar uma VNet do Resource Manager. Olá **VIP tipo** seleção determina se o ASE pode ser acessado diretamente do hello internet (externo) ou se ele usa um ILB. toolearn mais sobre essas opções, consulte [criar e usar um balanceador de carga interno com um ambiente de serviço de aplicativo][MakeILBASE]. 

      * Se você selecionar **externo** para Olá **VIP tipo**, você pode selecionar quantas sistema externo de saudação de endereços IP é criado com para fins SSL com base em IP. 
    
      * Se você selecionar **interno** para Olá **VIP tipo**, você deve especificar o domínio Olá que usa seu ASE. Você pode implantar um ASE em uma VNet que usa os intervalos de endereço público ou privado. toouse uma rede virtual com um intervalo de endereços públicos, você precisa toocreate Olá VNet antecipadamente. 
    
    * Se você selecionar uma rede virtual existente, uma nova sub-rede é criada quando Olá ASE é criado. *Você não pode usar uma sub-rede criada previamente no portal de saudação. Você pode criar um ASE com uma sub-rede existente se usar um modelo do Resource Manager.* toocreate uma ASE de um modelo, consulte [criar um ambiente de serviço de aplicativo de um modelo][MakeASEfromTemplate].

## <a name="app-service-environment-v1"></a>Ambiente do Serviço de Aplicativo v1 ##

Você ainda pode criar instâncias da primeira versão de saudação do ambiente de serviço de aplicativo (ASEv1). toostart que processam Olá pesquisa Marketplace para **v1 do ambiente de serviço de aplicativo**. Criar hello ASE em Olá mesma maneira que você crie Olá autônomo ASE. Quando ele for concluído, o ASEv1 tem dois front-ends e dois trabalhos. Com ASEv1, você deve gerenciar trabalhadores e front-ends hello. Eles não são adicionados automaticamente durante a criação dos planos do serviço de aplicativo. front-ends Olá atuam como pontos de extremidade HTTP/HTTPS hello e enviar tráfego toohello trabalhadores. operadores de saudação são funções hello hospedam seus aplicativos. Você pode ajustar a quantidade Olá de front-ends e trabalhadores depois de criar seu ASE. 

toolearn mais sobre ASEv1, consulte [toohello Introdução v1 do ambiente de serviço de aplicativo][ASEv1Intro]. Para obter mais informações sobre a expansão, gerenciar e monitorar ASEv1, consulte [como um ambiente de serviço de aplicativo de tooconfigure][ConfigureASEv1].

<!--Image references-->
[1]: ./media/how_to_create_an_external_app_service_environment/createexternalase-create.png
[2]: ./media/how_to_create_an_external_app_service_environment/createexternalase-aspcreate.png
[3]: ./media/how_to_create_an_external_app_service_environment/createexternalase-pricing.png
[4]: ./media/how_to_create_an_external_app_service_environment/createexternalase-embeddedcreate.png
[5]: ./media/how_to_create_an_external_app_service_environment/createexternalase-standalonecreate.png
[6]: ./media/how_to_create_an_external_app_service_environment/createexternalase-network.png



<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
