---
title: "aaaHow tooCreate v1 um ambiente de serviço de aplicativo"
description: "Descrição do fluxo de criação para ambiente do serviço de aplicativo v1"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: 81bd32cf-7ae5-454b-a0d2-23b57b51af47
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/11/2017
ms.author: ccompy
ms.openlocfilehash: 95feb33854eee5bac02fa68b066e2fc10eb3fede
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-app-service-environment-v1"></a>Como tooCreate v1 um ambiente de serviço de aplicativo 

> [!NOTE]
> Este artigo é sobre Olá v1 do ambiente de serviço de aplicativo. Há uma versão mais recente do hello ambiente de serviço de aplicativo que é mais fácil toouse e é executado na infraestrutura mais avançada. toolearn mais sobre a nova versão de hello começam com hello [Introdução toohello ambiente de serviço de aplicativo](../app-service/app-service-environment/intro.md).
> 

### <a name="overview"></a>Visão geral
Olá ambiente de serviço de aplicativo (ASE) é uma opção de serviço Premium do serviço de aplicativo do Azure que fornece um recurso de configuração avançada que não está disponível em carimbos de multilocatário hello. recurso de ASE Olá essencialmente implanta saudação do serviço de aplicativo do Azure na rede virtual do cliente. saudação de leitura toogain uma maior compreensão dos recursos de saudação oferecida pelos ambientes de serviço de aplicativo [o que é um ambiente de serviço de aplicativo] [ WhatisASE] documentação.

### <a name="before-you-create-your-ase"></a>Antes de criar seu ASE
É importante toobe ciente das coisas Olá que você não pode alterar. Os aspectos que você não pode alterar quanto ao ASE após sua criação são:

* Local
* Assinatura
* Grupo de recursos
* VNET usada
* Sub-rede usada 
* Tamanho da sub-rede

Quando escolher uma rede virtual e especificando uma sub-rede, verifique se ele é grande o suficiente tooaccomodate qualquer crescimento futuro. 

### <a name="creating-an-app-service-environment-v1"></a>Criando um Ambiente do Serviço de Aplicativo v1
toocreate v1 um ambiente de serviço de aplicativo que precisa toosearch hello Azure Marketplace para ***v1 do ambiente de serviço de aplicativo***, ou por meio do novo -> Web + móvel -> ambiente de serviço de aplicativo. toocreate um ASEv1:

1. Forneça o nome de saudação do seu ASE. nome de Olá especificado para Olá ASE será usado para aplicativos de saudação criados no hello ASE. Se o nome da saudação ASE é appsvcenvdemo nome de subdomínio Olá seria. *appsvcenvdemo.p.azurewebsites.net*. Se você tiver criado, portanto, um aplicativo Web chamado *mytestapp*, ele seria endereçável em *mytestapp.appsvcenvdemo.p.azurewebsites.net*. Você não pode usar o espaço em branco no nome de saudação do seu ASE. Se você usar caracteres maiusculos em nome hello, o nome de domínio de Olá será versão minúscula total de saudação do nome. Se você usar um ILB, seu nome do ASE não será usado no subdomínio, mas sim declarado explicitamente durante a criação do ASE
   
    ![][1]
2. Selecione sua assinatura. assinatura de saudação usada para sua ASE também é Olá um serão criados com todos os aplicativos em que ASE. Você pode colocar seu ASE em uma VNet que está em outra assinatura
3. Selecione ou especifique um novo grupo de recursos. grupo de recursos de saudação usado para seu ASE deve ser Olá mesmo que é usado para a sua rede virtual. Se você selecionar uma rede virtual já existente, seleção de grupo de recursos de saudação para seu ASE serão atualizado tooreflect que sua rede virtual.
   
    ![][2]
4. Faça suas seleções de Rede Virtual e Local. Você pode escolher toocreate uma nova rede virtual ou selecione uma rede virtual já existente. Se selecionar uma nova rede virtual, você poderá especificar um nome e local. Olá nova rede virtual terá Olá endereço intervalo 192.168.250.0/23 e uma sub-rede denominada **padrão** que é definido como 192.168.250.0/24. Você pode simplesmente selecionar um VNet pré-existente clássico ou do Gerenciador de Recursos. Olá a seleção do tipo de VIP determina se o ASE pode ser acessado diretamente da saudação internet (externo) ou se ele usa um balanceador de carga interno (ILB). mais sobre eles ler de toolearn [usando um balanceador de carga interno com um ambiente de serviço de aplicativo][ILBASE]. Se você selecionar um tipo de VIP de externos, em seguida, você pode selecionar quantas sistema externo de saudação de endereços IP é criado com para fins IPSSL. Se você selecionar interno necessário subdomínio de saudação toospecify que seu ASE usará. Os ASEs podem ser implantados em redes virtuais que usam os intervalos de endereço público *ou* espaços de endereço *ou* RFC1918 (ou seja, endereços privados). Ordem toouse uma rede virtual com um intervalo de endereços públicos, você precisará toocreate Olá VNet antecipadamente. Quando você seleciona uma rede virtual já existente, você precisará toocreate uma nova sub-rede durante a criação do ASE. **Você não pode usar uma sub-rede criada previamente no portal de saudação. Você poderá criar um ASE com uma sub-rede já existente, se criar o ASE usando um modelo do Resource Manager.** toocreate uma ASE de um modelo use informações de saudação aqui, [criando um ambiente de serviço de aplicativo do modelo] [ ILBAseTemplate] e aqui, [criando um ambiente de serviço de aplicativo do ILB de modelo] [ASEfromTemplate].

### <a name="details"></a>Detalhes
É criado um ASE com dois Front-Ends e dois trabalhos. Olá Front-Ends atuar como pontos de extremidade HTTP/HTTPS hello e enviar tráfego trabalhadores toohello que são funções hello que hospedam seus aplicativos. Você pode ajustar a quantidade de saudação após a criação de ASE e pode até mesmo configurar regras de AutoEscala nesses pools de recursos. Para obter mais detalhes sobre o redimensionamento manual, gerenciamento e monitoramento de um ambiente de serviço de aplicativo acesse aqui: [como tooconfigure um ambiente de serviço de aplicativo][ASEConfig] 

Somente uma ASE saudação pode existir na sub-rede Olá usado pelo Olá ASE. Olá não pode ser usada para algo diferente de saudação ASE

### <a name="after-app-service-environment-v1-creation"></a>Após a criação de um Ambiente do Serviço de Aplicativo v1
Após a criação do ASE é possível ajustar:

* Quantidade de Front-Ends (mínimo: 2)
* Quantidade de processadores (mínimo: 2)
* Quantidade de endereços IP disponíveis para SSL de IP
* Tamanhos de recursos usados por Olá Front-Ends ou trabalho de computação (o tamanho mínimo de Front-End é P2)

Há mais detalhes sobre o dimensionamento, gerenciamento e monitoramento de ambientes de serviço de aplicativo aqui manual: [como tooconfigure um ambiente de serviço de aplicativo][ASEConfig] 

Para obter informações sobre o dimensionamento automático, há um guia aqui: [como tooconfigure AutoEscala para um ambiente de serviço de aplicativo][ASEAutoscale]

Há dependências adicionais que não estão disponíveis para personalização, como o banco de dados de saudação e armazenamento. Essas são tratadas pelo Azure e são fornecidas com o sistema de saudação. Olá sistema armazenamento dá suporte a backup too500 GB para Olá todo o ambiente de serviço de aplicativo e banco de dados de saudação é ajustado pelo Azure conforme necessário, escala de saudação do sistema hello.

## <a name="getting-started"></a>Introdução
Todos os artigos e como-para para ambientes de serviço de aplicativo estão disponíveis no hello [Leiame para ambientes de serviço de aplicativo](../app-service/app-service-app-service-environments-readme.md).

tooget iniciado com o ambiente de serviço de aplicativo v1, consulte [toohello Introdução v1 do ambiente de serviço de aplicativo][WhatisASE]

Para obter mais informações sobre a plataforma do serviço de aplicativo do Azure hello, consulte [do serviço de aplicativo do Azure][AzureAppService].

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!--Image references-->
[1]: ./media/app-service-web-how-to-create-an-app-service-environment/asecreate-basecreateblade.png
[2]: ./media/app-service-web-how-to-create-an-app-service-environment/asecreate-vnetcreation.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[ASEConfig]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/ 
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/ 
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[ILBASE]: http://azure.microsoft.com/documentation/articles/app-service-environment-with-internal-load-balancer/
[ILBAseTemplate]: http://azure.microsoft.com/documentation/templates/201-web-app-ase-create/
[ASEfromTemplate]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-create-ilb-ase-resourcemanager/
