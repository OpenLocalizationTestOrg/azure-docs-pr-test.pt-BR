---
title: "aaaCreating e usando um balanceador de carga interno com um ambiente de serviço de aplicativo | Microsoft Docs"
description: Criar e usar um ASE com um ILB
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: ad9a1e00-d5e5-413e-be47-e21e5b285dbf
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: 20799f260993d6e81499408e5b547a2e21430174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-an-internal-load-balancer-with-an-app-service-environment"></a>Como usar um Balanceador de Carga Interno com um Ambiente do Serviço do Aplicativo

> [!NOTE] 
> Este artigo é sobre Olá v1 do ambiente de serviço de aplicativo. Há uma versão mais recente do hello ambiente de serviço de aplicativo que é mais fácil toouse e é executado na infraestrutura mais avançada. toolearn mais sobre a nova versão de hello começam com hello [Introdução toohello ambiente de serviço de aplicativo](../app-service/app-service-environment/intro.md).
>

recurso do ambiente de serviço de aplicativo (ASE) Olá é uma opção de serviço Premium do serviço de aplicativo do Azure que fornece um recurso de configuração avançada que não está disponível em carimbos de multilocatário hello. recurso de ASE Olá essencialmente implanta saudação do serviço de aplicativo do Azure no seu Network(VNet) Virtual do Azure. saudação de leitura toogain uma maior compreensão dos recursos de saudação oferecida pelos ambientes de serviço de aplicativo [o que é um ambiente de serviço de aplicativo] [ WhatisASE] documentação. Se você não souber os benefícios de saudação do operando em uma rede virtual ler Olá [perguntas Frequentes de rede Virtual do Azure][virtualnetwork]. 

## <a name="overview"></a>Visão geral
Um ASE pode ser implantado com um ponto de extremidade acessível da internet ou com um endereço IP em sua VNet. Ordem tooset Olá IP endereço tooa endereço de rede virtual é necessário toodeploy seu ASE com um Balancer(ILB) de carga interno. Quando seu ASE é configurado com um ILB, você fornece:

* seu próprio domínio ou subdomínio. toomake fácil, que este documento presume um subdomínio, mas você pode configurá-lo de qualquer maneira. 
* certificado Olá usado para HTTPS
* Gerenciamento de DNS para o subdomínio. 

Em troca, você pode fazer coisas como:

* aplicativos de intranet do host, como aplicativos de negócios, com segurança no hello de linha de nuvem que você acessa por meio de um Site tooSite ou ExpressRoute VPN
* aplicativos de host na nuvem de saudação que não estão listados em servidores DNS públicos
* criar aplicativos back-end isolados da internet, aos quais seus aplicativos front-end podem ser integrados com segurança

#### <a name="disabled-functionality"></a>Funcionalidade desabilitada
Há algumas coisas que você não pode fazer ao usar um ASE com ILB. Entre elas:

* usar IPSSL
* atribuindo endereços IP toospecific aplicativos
* comprar e usar um certificado com um aplicativo por meio do portal hello. É claro ainda pode obter certificados diretamente com uma autoridade de certificação e usá-lo com seus aplicativos, mas não por meio de saudação portal do Azure.

## <a name="creating-an-ilb-ase"></a>Criar um ILB do ASE
A criação de um ILB do ASE não é muito diferente da criação normal de um ASE. Para obter uma discussão mais profunda sobre a criação de uma ASE ler [como um ambiente de serviço de aplicativo de tooCreate][HowtoCreateASE]. Olá toocreate de processo é uma ASE ILB Olá mesmo entre criar uma rede virtual durante a criação do ASE ou selecionar uma rede virtual já existente. toocreate uma ASE ILB: 

1. Em Olá selecione portal do Azure **Novo -> Web + móvel -> ambiente de serviço de aplicativo**
2. Selecione sua assinatura
3. Selecione ou crie um grupo de recursos
4. Selecione ou crie uma VNet
5. Crie uma sub-rede, se você selecionar uma VNet
6. Selecione **Virtual/local de rede-> Configuração de rede virtual** e conjunto hello tooInternal do tipo de VIP
7. Forneça o nome de subdomínio (Isso será subdomínio Olá usado para aplicativos criados neste ASE)
8. Selecione OK e Criar

![][1]

Na folha de rede Virtual hello, há uma opção de configuração de rede virtual. Isso permite a escolha entre um VIP Externo ou um VIP Interno. padrão de saudação é externo. Se você tiver definido tooExternal seu ASE usará um VIP acessível da internet. Se você selecionar Interno, seu ASE será configurado com um ILB em um endereço IP em sua VNet. 

Depois de selecionar interno, Olá tooadd de capacidade mais endereços IP tooyour que ASE é removida e em vez disso, você precisa tooprovide subdomínio de saudação do hello ASE. Em uma ASE com hello um VIP externo nome da saudação ASE é usado no subdomínio Olá para aplicativos criados no que ASE. Se seu ASE foi chamado ***contosotest*** e seu aplicativo em que ASE foi chamado ***mytest*** será subdomínio de saudação do formato de saudação ***contosotest.p.azurewebsites.net*** e Olá URL para esse aplicativo seria ***mytest.contosotest.p.azurewebsites.net***. Se você definir Olá tooInternal do tipo de VIP, seu nome ASE não é usado no subdomínio Olá para Olá ASE. Você pode especificar subdomínio Olá explicitamente. Se o subdomínio foi ***contoso.corp.net*** e um aplicativo é feita em que ASE denominado ***timereporting*** hello, em seguida, a URL para que o aplicativo seria ***timereporting.contoso.corp.net***.

## <a name="apps-in-an-ilb-ase"></a>Aplicativos em um ILB do ASE
Criando um aplicativo em uma ASE ILB é Olá igual ao criar um aplicativo em uma ASE normalmente. 

1. Em Olá selecione portal do Azure **Novo -> Web + móvel -> Web** ou **Mobile** ou **API App**
2. Insira o nome do aplicativo
3. Escolha a assinatura
4. Escolha ou crie um grupo de recursos
5. Selecione ou crie um ASP (Plano do Serviço de Aplicativo). Criar um novo ASP, em seguida, selecione seu ASE como Olá local e o pool do trabalhador Olá selecione desejada seu toobe ASP criado no. Quando você cria Olá ASP selecione seu ASE como Olá local e o pool do trabalhador hello. Ao especificar nome de saudação do aplicativo hello em que você verá esse subdomínio Olá nome do aplicativo é substituído pelo subdomínio Olá para seu ASE. 
6. Selecione Criar. Você deve selecionar Olá **toodashboard Pin** caixa de seleção se desejar Olá tooshow de aplicativo em seu painel. 

![][2]

Em aplicativo de saudação do nome de subdomínio Olá obtém subdomínio de saudação tooreflect atualizada de seu ASE. 

## <a name="post-ilb-ase-creation-validation"></a>Validação posterior à criação do ILB do ASE
Uma ASE ILB é ligeiramente diferente de saudação não - ILB ASE. Como já observado é necessário toomanage seu próprio DNS e você também tem tooprovide seu próprio certificado para conexões HTTPS. 

Depois de criar seu ASE você vai notar esse subdomínio Olá mostra subdomínio Olá especificado e houver um novo item no hello **configuração** menu chamado **ILB certificado**. Olá ASE é criada com um certificado autoassinado que torna mais fácil tootest HTTPS. Olá portal informará que você precisa tooprovide seu próprio certificado para HTTPS, mas se toodrive toohave um certificado que acompanha seu subdomínio. 

![][3]

Se você está simplesmente experimentando coisas e não sei como toocreate um certificado, você pode usar Olá MMC do IIS toocreate do aplicativo de console a própria assinou o certificado. Depois que ela é criada, você pode exportá-lo como um arquivo. pfx e, em seguida, carregá-lo no hello ILB da interface do usuário de certificado. Quando você acessa um site protegido com um certificado autoassinado, seu navegador fornecerá um aviso que Olá site que você está acessando não é segura devido a certificados de saudação do toohello dificuldades toovalidate. Se você quiser tooavoid esse aviso que é necessário um certificado apropriadamente assinado que corresponde a um subdomínio e tem uma cadeia de confiança que é reconhecida pelo seu navegador.

![][6]

Se você quiser tootry Olá fluxo com seus próprios certificados e testar ASE tooyour de acesso HTTP e HTTPS:

1. Vá tooASE da interface do usuário após a criação ASE **ASE -> Configurações -> certificados ILB**
2. Defina o certificado ILB selecionando o arquivo pfx do certificado e forneça a senha. Esta etapa leva um pouco ao tooprocess e mensagem de saudação do que uma operação de dimensionamento está em andamento será mostrada.
3. Obter o endereço ILB de saudação para seu ASE (**ASE -> Propriedades -> endereço IP Virtual**)
4. Crie um aplicativo Web no ASE após a criação 
5. Criar uma máquina virtual se você não tiver um em que VNET (Olá não na mesma sub-rede como Olá ASE ou interrupção de coisas)
6. Configure o DNS para seu subdomínio. Você pode usar um caractere curinga com o subdomínio no DNS ou se você quiser toodo alguns testes simples, editar o arquivo de hosts de saudação em sua VM tooset nome tooVIP IP endereço do aplicativo web. Se seu ASE tinha o nome de subdomínio hello. ilbase.com e você feitas Olá mytestapp do aplicativo web para que ele seria abordado em mytestapp.ilbase.com e definido que em seu arquivo hosts. (No Windows hello arquivo hosts é em C:\Windows\System32\drivers\etc\)
7. Use um navegador no VM e vá toohttp://mytestapp.ilbase.com (ou tudo o que é o nome do aplicativo web com o subdomínio)
8. Use um navegador no VM e vá toohttps://mytestapp.ilbase.com terá tooaccept falta de saudação de segurança se usando um certificado autoassinado. 

endereço IP de saudação para o ILB está listado em suas propriedades como Olá endereço IP Virtual

![][4]

## <a name="using-an-ilb-ase"></a>Como usar um ASE com ILB
#### <a name="network-security-groups"></a>Grupos de segurança de rede
Um ILB ASE habilita o isolamento da rede para seus aplicativos como os aplicativos Olá não estão acessíveis ou até mesmo conhecidos por Olá da internet. Isso é excelente para hospedar sites de intranet, como aplicativos de linha de negócios. Quando você precisa de acesso toorestrict ainda mais você ainda pode usar acesso de toocontrol Groups(NSGs) de segurança de rede no nível de rede de saudação. 

Se você quiser toouse NSGs toofurther restringir o acesso, em seguida, você precisa toomake-se de que você não interrompe a comunicação de saudação que ASE Olá precisa no toooperate de ordem. Embora Olá acesso HTTP/HTTPS é apenas por meio de saudação ILB usado pelo Olá Olá ASE que ASE ainda depende do recurso fora Olá VNet. toosee o acesso à rede é ainda necessário examinar informações de saudação no documento de saudação em [controlando o tráfego de entrada tooan ambiente de serviço de aplicativo] [ ControlInbound] e documento Olá no [rede Detalhes de configuração para ambientes de serviço de aplicativo com o ExpressRoute][ExpressRoute]. 

tooconfigure seus NSGs necessário tooknow Olá IP endereço que é usado pelo Azure toomanage seu ASE. Esse endereço IP também é Olá saído endereço IP de seu ASE, se ele faz solicitações de internet. endereço IP saído Olá para seu ASE permanecerá estático durante saudação de seu ASE. Se você excluir e recriar seu ASE, você obterá um novo endereço IP. toofind esse endereço IP ir muito**Configurações -> propriedades** e localize Olá **endereço de IP de saída**. 

![][5]

#### <a name="general-ilb-ase-management"></a>Gerenciamento geral do ASE com ILB
Gerenciando uma ASE ILB é amplamente Olá igual a gerenciar uma ASE normalmente. Você precisa tooscale a sua toohost de pools de trabalho mais instâncias ASP e aumentar os valores de toohandle maior de servidores de Front-End do tráfego HTTP/HTTPS. Para obter informações gerais sobre como gerenciar a configuração de saudação de uma ASE, leia o documento de saudação em [Configurando um ambiente de serviço de aplicativo][ASEConfig]. 

itens de gerenciamento adicional de saudação são o gerenciamento de certificado e o gerenciamento de DNS. Necessário tooobtain carregar Olá certificado usado para HTTPS após a criação de ILB ASE e substituí-lo antes de expirar. Porque o Azure possui o domínio base Olá podemos fornecer certificados para ASs com um VIP externo. Como o subdomínio Olá usado por uma ASE ILB pode ser qualquer coisa, você precisa tooprovide seu próprio certificado para HTTPS. 

#### <a name="dns-configuration"></a>Configuração de DNS
Ao usar uma saudação VIP externo que DNS é gerenciado pelo Azure. Qualquer aplicativo que criou no seu ASE é adicionado automaticamente tooAzure DNS que é um DNS público. Em uma ASE ILB que toomanage seu próprio DNS. Para um subdomínio específico como contoso.corp.net, será preciso toocreate a que endereço ponto tooyour ILB para registros de DNS:

    * 
    publicação de ftp *.scm 


## <a name="getting-started"></a>Introdução
Todos os artigos e como-para para ambientes de serviço de aplicativo estão disponíveis no hello [Leiame para ambientes de serviço de aplicativo](../app-service/app-service-app-service-environments-readme.md).

tooget iniciado com ambientes de serviço de aplicativo, consulte [tooApp Introdução ambientes de serviço][WhatisASE]

Para obter mais informações sobre a plataforma do serviço de aplicativo do Azure hello, consulte [do serviço de aplicativo do Azure][AzureAppService].

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!--Image references-->
[1]: ./media/app-service-environment-with-internal-load-balancer/ilbase-createilbase.png
[2]: ./media/app-service-environment-with-internal-load-balancer/ilbase-createapp.png
[3]: ./media/app-service-environment-with-internal-load-balancer/ilbase-newase.png
[4]: ./media/app-service-environment-with-internal-load-balancer/ilbase-vip.png
[5]: ./media/app-service-environment-with-internal-load-balancer/ilbase-externalvip.png
[6]: ./media/app-service-environment-with-internal-load-balancer/ilbase-ilbcertificate.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[ControlInbound]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[ExpressRoute]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/
[vnetnsgs]: http://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[ASEConfig]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
