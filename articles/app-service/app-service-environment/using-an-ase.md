---
title: "aaaUse um ambiente de serviço de aplicativo do Azure"
description: "Como toocreate, publicar e dimensionar os aplicativos em um ambiente de serviço de aplicativo do Azure"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: a22450c4-9b8b-41d4-9568-c4646f4cf66b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: 30c89e384efc07c560254856c0ca7d4eb4b1f010
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-an-app-service-environment"></a>Usar um ambiente do Serviço de Aplicativo #

## <a name="overview"></a>Visão geral ##

O Ambiente do Serviço de Aplicativo do Azure é uma implantação do Serviço de Aplicativo do Azure em uma sub-rede em uma rede virtual do Azure do cliente. Ele consiste em:

- **Front-ends**: front-ends Olá são onde HTTP/HTTPS termina em um ambiente de serviço de aplicativo (ASE).
- **Os operadores**: trabalhadores Olá são recursos Olá hospedam seus aplicativos.
- **Banco de dados**: banco de dados de saudação contém informações que definem o ambiente de saudação.
- **Armazenamento**: armazenamento de saudação é usado toohost Olá publicado de cliente aplicativos.

> [!NOTE]
> Há duas versões do Ambiente do Serviço de Aplicativo: ASEv1 e ASEv2. ASEv1, você deve gerenciar recursos Olá antes que você pode usá-los. toolearn como tooconfigure e gerenciar ASEv1, consulte [configurar um v1 do ambiente de serviço de aplicativo][ConfigureASEv1]. restante Olá deste artigo se concentra em ASEv2.
>
>

Implante um ASE (ASEv1 e ASEv2) com um VIP externo ou interno para o acesso ao aplicativo. implantação de saudação com um VIP externo é geralmente chamada de uma ASE externo. versão interna Olá é chamado hello ASE ILB porque ele usa um balanceador de carga interno (ILB). toolearn mais sobre Olá ASE ILB, consulte [criar e usar uma ASE ILB][MakeILBASE].

## <a name="create-a-web-app-in-an-ase"></a>Criar um aplicativo Web em um ASE ##

toocreate um aplicativo web em uma ASE, você use Olá mesmo processo ao criá-lo normalmente, mas com algumas pequenas diferenças. Quando você cria um novo plano do Serviço de Aplicativos:

- Em vez de escolher uma localização geográfica na qual toodeploy seu aplicativo, você pode escolher uma ASE como seu local.
- Todos os planos do Serviço de Aplicativo criados em um ASE devem estar em um tipo de preço Isolado.

Se você não tiver uma ASE, você pode criar um, seguindo as instruções de saudação do [criar um ambiente de serviço de aplicativo][MakeExternalASE].

toocreate um aplicativo web em uma ASE:

1. Selecione **Novo** > **Web + Móvel** > **Aplicativo Web**.

2. Insira um nome para o aplicativo web de saudação. Se você já selecionou um plano de serviço de aplicativo em uma ASE, nome de domínio Olá para o aplicativo hello reflete o nome de domínio de saudação do hello ASE.

    ![Seleção de nome de aplicativo Web][1]

3. Selecione uma assinatura.

4. Insira um nome para um novo grupo de recursos ou selecionar **usar existente** e selecione uma opção na lista suspensa de saudação.

5. Selecione um plano do Serviço de Aplicativo existente no ASE ou crie um novo com as seguintes etapas:

    a. Selecione **Criar Novo**.

    b. Insira o nome de saudação para seu plano de serviço de aplicativo.

    c. Selecione seu ASE em Olá **local** lista suspensa.

    d. Selecione o tipo de preço **Isolado**. Selecione **Selecionar**.

    e. Selecione **OK**.
    
    ![Tipos de preço Isolados][2]

6. Selecione **Criar**.

## <a name="how-scale-works"></a>Como funciona a escala ##

Cada aplicativo do Serviço de Aplicativo é executado em um plano do Serviço de Aplicativo. modelo de contêiner de saudação é ambientes manter planos de serviço de aplicativo e planos de serviço de aplicativo mantenha aplicativos. Quando você dimensionar um aplicativo, dimensionar Olá plano de serviço de aplicativo e, portanto, ampliar todos os aplicativos Olá Olá mesmo plano.

Em ASEv2, quando você dimensionar um plano de serviço de aplicativo, infraestrutura Olá necessário é adicionada automaticamente. Há um atraso tooscale operações enquanto infraestrutura Olá é adicionada. ASEv1, infraestrutura Olá necessário deve ser adicionada antes de criar ou expandir seu plano de serviço de aplicativo. 

No serviço de aplicativo de multilocatário hello, dimensionamento é geralmente imediato porque um pool de recursos está prontamente disponível toosupport-lo. Em um ASE, não há nenhum buffer desse tipo e os recursos são alocados conforme a necessidade.

Em uma ASE, você pode dimensionar too100 instâncias. Essas 100 instâncias podem estar todas em um único plano do Serviço de Aplicativo ou ser distribuídas entre vários planos do Serviço de Aplicativo.

## <a name="ip-addresses"></a>Endereços IP ##

Serviço de aplicativo tem Olá capacidade tooallocate um aplicativo de tooan de endereço IP dedicado. Esse recurso está disponível depois de configurar um SSL baseado em IP, conforme descrito em [associar um personalizado SSL certificado tooAzure aplicativos web existentes][ConfigureSSL]. No entanto, em um ASE, há uma exceção notável. Não é possível adicionar IP adicionais endereços toobe usado para um SSL baseado em IP em uma ASE ILB.

Em ASEv1, você precisa endereços IP hello tooallocate como recursos antes de você pode usá-los. Em ASEv2, você usá-los de seu aplicativo exatamente como você faria no multilocatário de saudação do serviço de aplicativo. Sempre há um endereço de reposição na ASEv2 too30 endereços de IP. Sempre que você usar um, outro será adicionado, de forma que sempre haja um endereço imediatamente disponível para uso. Um tempo de atraso é necessário tooallocate outro endereço IP, o que impede a adição de IP endereços em sucessão rápida.

## <a name="front-end-scaling"></a>Dimensionamento de front-end ##

ASEv2, quando você expandir seus planos de serviço de aplicativo, os operadores são automaticamente adicionados toosupport-los. Cada ASE é criado com dois front-ends. Além disso, front-ends Olá dimensionar automaticamente a uma taxa de um front-end para todas as instâncias de 15 nos planos de serviço de aplicativo. Por exemplo, se você tiver 15 instâncias, terá três front-ends. Se você expandir too30 instâncias, você tem quatro front-ends e assim por diante.

Esse número de front-ends deve ser mais do que o suficiente para a maioria dos cenários. No entanto, você pode dimensionar a uma taxa mais rápida. Você pode alterar a taxa de saudação tooas baixa como um front-end para cada cinco instâncias. Há um custo para alterar a taxa de saudação. Para saber mais, veja [Preços do Serviço de Aplicativo do Azure][Pricing].

Recursos do front-end estão ponto de extremidade HTTP/HTTPS de saudação para Olá ASE. Com a configuração de front-end do saudação padrão, o uso de memória por front-end é consistentemente em torno 60 por cento. Cargas de trabalho de cliente não são executadas em um front-end. Olá fator chave para um front-end com respeito tooscale é Olá CPU, o que acontece principalmente por tráfego HTTPS.

## <a name="app-access"></a>Acesso ao aplicativo ##

Em uma ASE externo, o domínio de saudação que é usado quando você cria aplicativos é diferente de multilocatário de saudação do serviço de aplicativo. Ele inclui o nome de saudação do hello ASE. Para obter mais informações sobre como toocreate uma ASE externas, consulte [criar um ambiente de serviço de aplicativo][MakeExternalASE]. nome de domínio de saudação em uma ASE externo aparência *.&lt; asename&gt;. p.azurewebsites.net*. Por exemplo, se seu ASE é denominado _externo ase_ e hospedar um aplicativo chamado _contoso_ em que ASE alcançá-lo no hello seguintes URLs:

- contoso.external-ase.p.azurewebsites.net
- contoso.scm.external-ase.p.azurewebsites.net

Olá URL contoso.scm.external-ase.p.azurewebsites.net é console de Kudu Olá tooaccess usados ou para publicação implantar seu aplicativo por meio da web. Para obter informações sobre o console de Kudu hello, consulte [console Kudu para o serviço de aplicativo do Azure][Kudu]. console de Kudu Olá oferece uma interface da web para depuração, carregando os arquivos, edição de arquivos e muito mais.

Em uma ASE ILB, você pode determinar domínio Olá no momento da implantação. Para obter mais informações sobre como toocreate um ILB ASE, consulte [criar e usar uma ASE ILB][MakeILBASE]. Se você especificar o nome de domínio Olá _ilb ase.info_, Olá aplicativos ASE usam esse domínio durante a criação do aplicativo. Para o aplicativo hello chamado _contoso_, Olá URLs são:

- contoso.ilb-ase.info
- contoso.scm.ilb-ase.info

## <a name="publishing"></a>Publicação ##

Assim como acontece com multilocatário de saudação do serviço de aplicativo, em uma ASE, você pode publicar com:

- Implantação da Web.
- FTP.
- Integração contínua.
- Arrastar e soltar no console do Kudu hello.
- Um IDE como o Visual Studio, Eclipse ou IntelliJ IDEA.

Com uma ASE externo, essas opções de publicação se comportam Olá mesmo. Para saber mais, veja [Implantação no Serviço de Aplicativo do Azure][AppDeploy]. 

a principal diferença Olá com a publicação é com respeito tooan ASE ILB. Com uma ASE ILB, pontos de extremidade de publicação do hello estão disponíveis somente através de saudação ILB. Olá ILB está em um IP particular na sub-rede do ASE Olá na rede virtual hello. Se você não tiver acesso de rede toohello ILB, não é possível publicar todos os aplicativos em que ASE. Conforme observado na [criar e usar uma ASE ILB][MakeILBASE], você precisa tooconfigure DNS para aplicativos de saudação no sistema de saudação. Isso inclui ponto de extremidade SCM hello. Se eles não estiverem definidos corretamente, você não poderá publicar. Seu IDEs também precisa toohello de acesso de rede toohave ILB em ordem toopublish tooit diretamente.

Sistemas de CI baseado na Internet, como GitHub e o Visual Studio Team Services, não funcionam com uma ASE ILB porque o ponto de extremidade de publicação do hello não está acessível pela Internet. Em vez disso, você precisa toouse um sistema de CI que usa um modelo de pull, como o Dropbox.

pontos de extremidade de publicação de saudação para aplicativos em uma ASE ILB usam domínio Olá que Olá com que ASE ILB foi criado. Você pode ver no perfil de publicação do aplicativo hello e na folha de saudação do aplicativo portal (em **visão geral** > **Essentials** e também em **propriedades**). 

## <a name="pricing"></a>Preços ##

Olá preços SKU chamado **isolado** foi criado para uso apenas com ASEv2. Todos os planos de serviço de aplicativo que são hospedados em ASEv2 hello isolado preços SKU. As taxas de plano do Serviço de Aplicativo Isolado podem variar por região. 

Além de planos de preços toohello para o serviço de aplicativo, há uma taxa de simples para ASE em si. Olá taxa simples não são alterados com tamanho de saudação do seu ASE e paga a infraestrutura de saudação ASE um padrão de dimensionamento de taxa de 1 adicionais front-end para todas as instâncias do plano do serviço de aplicativo 15.  

Se a taxa de escala de padrão de saudação de front-1 end para todas as instâncias do plano do serviço de aplicativo 15 não for rápida o suficiente, você pode ajustar a taxa Olá no qual o front-ends são adicionados ou Olá tamanho de saudação front-ends.  Quando você ajustar a taxa de saudação ou tamanho, você paga núcleos de front-end de saudação que não seriam adicionados por padrão.  

Por exemplo, se você ajustar Olá too10 de taxa de escala, é adicionado um front-end para cada 10 instâncias nos planos de serviço de aplicativo. taxas de saudação abrange uma taxa de escala de um front-end para todas as instâncias de 15. Com uma taxa de escala de 10, você pode pagar uma taxa para Olá terceiro front-end que foi adicionado para Olá 10 instâncias do plano de serviço de aplicativo. Toopay para que ele não é necessário quando você chegar 15 instâncias porque ele foi adicionado automaticamente.

Se você Olá tamanho de núcleos de too2 front-ends Olá ajustado, mas não ajustar a taxa de saudação e pagar para Olá núcleos extras.  Uma ASE é criada com 2 front-ends, até mesmo abaixo do limite dimensionamento automático Olá que pago para 2 núcleos adicionais se você tiver aumentado Olá tamanho too2 core front-ends.

Para saber mais, veja [Preços do Serviço de Aplicativo do Azure][Pricing].

## <a name="delete-an-ase"></a>Excluir um ASE ##

toodelete uma ASE: 

1. Use **excluir** na parte superior de saudação do hello **ambiente de serviço de aplicativo** folha. 

2. Insira nome de saudação do seu tooconfirm ASE que você deseja toodelete-lo. Quando você exclui uma ASE, excluir todo o conteúdo de saudação nele também. 

    ![Exclusão de ASE][3]

<!--Image references-->
[1]: ./media/using_an_app_service_environment/usingase-appcreate.png
[2]: ./media/using_an_app_service_environment/usingase-pricingtiers.png
[3]: ./media/using_an_app_service_environment/usingase-delete.png


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
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
