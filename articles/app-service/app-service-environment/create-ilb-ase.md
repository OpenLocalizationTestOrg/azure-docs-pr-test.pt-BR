---
title: "aaaCreate e usar um balanceador de carga interno com um ambiente de serviço de aplicativo do Azure"
description: "Obter detalhes sobre como toocreate e usar um ambiente de serviço de aplicativo do Azure isolado da internet"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 0f4c1fa4-e344-46e7-8d24-a25e247ae138
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: d019ca6f231c3acfdab4cd380db375a076802f7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-use-an-internal-load-balancer-with-an-app-service-environment"></a>Como criar e usar um balanceador de carga interno com um ambiente do Serviço de Aplicativo #

 O Ambiente do Serviço de Aplicativo do Azure é uma implantação do Serviço de Aplicativo do Azure em uma sub-rede de uma VNet (rede virtual) do Azure. Há dois toodeploy de maneiras de um ambiente de serviço de aplicativo (ASE): 

- Com um VIP em um endereço IP externo, geralmente chamado de ASE externo.
- Com um VIP em um endereço IP interno, geralmente chamado uma ASE ILB, porque o ponto de extremidade interno Olá é um balanceador de carga interno (ILB). 

Este artigo mostra como toocreate uma ASE ILB. Para obter uma visão geral sobre Olá ASE, consulte [ambientes de serviço Introdução tooApp][Intro]. toolearn como toocreate uma ASE externas, consulte [criar uma ASE externo][MakeExternalASE].

## <a name="overview"></a>Visão geral ##

Um ASE pode ser implantado com um ponto de extremidade acessível pela Internet ou com um endereço IP em sua VNet. tooset tooa endereço de rede virtual, Olá ASE deve ser implantado com um ILB de endereço IP de saudação. Para implantar o ASE com um ILB, você deve fornecer:

-   Seu próprio domínio, que você usa quando cria seus aplicativos.
-   certificado de saudação usado para HTTPS.
-   Gerenciamento de DNS para o seu domínio.

Em troca, você pode fazer coisas como:

-   Aplicativos de intranet do host com segurança na nuvem hello, o que você pode acessar por meio de um site a site ou VPN de rota expressa do Azure.
-   Aplicativos de host na nuvem Olá que não estiverem em servidores DNS públicos.
-   Criar aplicativos back-end isolados da Internet, que podem ser integrados com seus aplicativos front-end com segurança.

### <a name="disabled-functionality"></a>Funcionalidade desabilitada ###

Há algumas coisas que você não pode fazer ao usar um ASE ILB:

-   Usar SSL baseado em IP.
-   Atribua endereços IP toospecific aplicativos.
-   Comprar e usar um certificado com um aplicativo por meio de saudação portal do Azure. Você pode obter certificados diretamente de uma autoridade de certificação e usá-los com seus aplicativos. Não é possível obtê-las por meio de saudação portal do Azure.

## <a name="create-an-ilb-ase"></a>Criar um ASE ILB ##

toocreate uma ASE ILB:

1. No portal do Azure de Olá, selecione **novo** > **Web + móvel** > **ambiente de serviço de aplicativo**.

2. Selecione sua assinatura.

3. Selecione ou crie um grupo de recursos.

4. Selecione ou crie uma VNet.

5. Se você selecionar uma rede virtual existente, será necessário toocreate uma saudação de toohold sub-rede ASE. Certifique-se de tooset uma sub-rede tamanho grande o suficiente tooaccommodate qualquer crescimento futuro de sua ASE. O tamanho recomendado é `/25`, que tem 128 endereços e é compatível com um ASE com tamanho máximo. Olá você pode selecionar o tamanho mínimo é um `/28`. Depois que precisa de infraestrutura, esse tamanho pode ser dimensionado tooa máximo 11 instâncias.

    * Ir além da saudação padrão de no máximo de 100 instâncias nos planos de serviço de aplicativo.

    * Dimensione cerca de 100, mas com dimensionamento de front-end mais rápido.

6. Selecione **Rede Virtual/Local** > **Configuração de Rede Virtual**. Saudação de conjunto **VIP tipo** muito**interno**.

7. Digite um nome de domínio. Este domínio é hello usado para aplicativos criados neste ASE. Há algumas restrições. Ele não pode ser:

    * net   

    * azurewebsites.net

    * p.azurewebsites.net

    * &lt;asename&gt;.p.azurewebsites.net

   o nome de domínio personalizado Olá usado para aplicativos e nome de domínio Olá usado pelo seu ASE não pode se sobrepor. Para uma ASE ILB com o nome de domínio Olá _contoso.com_, você não pode usar nomes de domínio personalizado para seus aplicativos, como:

    * www.contoso.com

    * abcd.def.contoso.com

    * abcd.contoso.com

   Se você souber os nomes de domínio personalizados Olá para seus aplicativos, escolha um domínio para Olá ASE ILB que não tem um conflito com esses nomes de domínio personalizado. Neste exemplo, você pode usar algo como *contoso internal.com* para domínio de saudação do seu ASE porque que não entra em conflito com nomes de domínio personalizado que terminam em *. contoso.com*.

8. Selecione **OK** e, então, selecione **Criar**.

    ![Criação de ASE][1]

Em Olá **rede Virtual** folha, há um **configuração de rede Virtual** opção. Você pode usá-lo tooselect um VIP externo ou um VIP interno. saudação padrão é **externo**. Se você selecionar **Externo**, o seu ASE usará um VIP acessível pela Internet. Se você selecionar **Interno**, o seu ASE será configurado com um ILB em um endereço IP na sua VNet.

Depois de selecionar **interno**, Olá capacidade tooadd mais endereços IP tooyour ASE é removido. Em vez disso, você precisa tooprovide domínio Olá Olá ASE. Em uma ASE com um VIP externo, o nome de saudação do hello que ASE é usado no domínio Olá para aplicativos criados no que ASE.

Se você definir **VIP tipo** muito**interno**, seu nome ASE não é usado no domínio Olá para Olá ASE. Você pode especificar domínio Olá explicitamente. Se o domínio for *contoso.corp.net* e criar um aplicativo que ASE denominado *timereporting*, Olá URL para que o aplicativo é timereporting.contoso.corp.net.


## <a name="create-an-app-in-an-ilb-ase"></a>Como criar um aplicativo em uma ASE ILB ##

Criar um aplicativo em uma ASE ILB em Olá mesma maneira que você cria um aplicativo em uma ASE normalmente.

1. No portal do Azure de Olá, selecione **novo** > **Web + móvel** > **Web** ou **Mobile** ou  **Aplicativo de API**.

2. Insira o nome de saudação do aplicativo hello.

3. Selecione a assinatura de saudação.

4. Selecione ou crie um grupo de recursos.

5. Selecione ou crie um plano do Serviço de Aplicativo. Se você quiser toocreate um novo plano de serviço de aplicativo, selecione seu ASE como local de saudação. Selecione o pool do trabalhador Olá onde você deseja que seu toobe de plano de serviço de aplicativo criado. Quando você cria Olá plano de serviço de aplicativo, selecione seu ASE como Olá local e o pool do trabalhador hello. Quando você especifica o nome de saudação do aplicativo hello, domínio Olá em nome do aplicativo é substituído por domínio Olá para seu ASE.

6. Selecione **Criar**. Se você desejar Olá tooappear de aplicativo em seu painel, selecione o **toodashboard Pin** caixa de seleção.

    ![Criação do plano do Serviço de Aplicativo][2]

    Em **nome do aplicativo**, nome de domínio de saudação é domínio de saudação tooreflect atualizada de seu ASE.

## <a name="post-ilb-ase-creation-validation"></a>Validação posterior à criação do ASE ILB ##

Uma ASE ILB é ligeiramente diferente de saudação não - ILB ASE. Como já observado, você precisa toomanage seu próprio DNS. Você também tem tooprovide seu próprio certificado para conexões HTTPS.

Depois de criar seu ASE, nome de domínio Olá mostra domínio Olá especificado. Um novo item chamado **Certificado ILB** aparece no menu **Configurações**. Olá ASE é criada com um certificado que não especifica o domínio do ILB ASE hello. Se você usar o hello ASE com esse certificado, seu navegador informa que é inválido. Esse certificado torna mais fácil tootest HTTPS, mas você precisa tooupload seu próprio certificado associado tooyour ILB ASE domínio. Essa etapa é necessária independentemente se o seu certificado é auto-assinado ou adquirido de uma autoridade de certificação.

![Nome de domínio ASE ILB][3]

O ASE ILB precisa de um certificado SSL válido. Use autoridades de certificação internas, compre um certificado de um emissor externo ou use um certificado auto-assinado. Independentemente de fonte de saudação do certificado SSL hello, hello seguintes atributos de certificado necessário toobe configurado corretamente:

* **Entidade**: este atributo deve ser definido como too*.your-raiz domínio aqui.
* **Nome Alternativo da Entidade**: esse atributo deve incluir **.seu-domínio-raiz-aqui* e **.scm.seu-domínio-raiz-aqui*. SSL conexões toohello site SCM/Kudu associado a cada aplicativo usar um endereço de formulário Olá *your-app-name.scm.your-root-domain-here*.

Certificado SSL da saudação de Convert/Salvar como um arquivo. pfx. arquivo. pfx de saudação deve incluir todos os intermediário e raiz certificados. Proteja-o com uma senha.

Se você quiser toocreate um certificado autoassinado, você pode usar comandos do PowerShell Olá aqui. Ser toouse-se de que seu nome de domínio em vez de ASE ILB *internal.contoso.com*: 

    $certificate = New-SelfSignedCertificate -certstorelocation cert:\localmachine\my -dnsname "\*.internal-contoso.com","\*.scm.internal-contoso.com"
    
    $certThumbprint = "cert:\localMachine\my\" +$certificate.Thumbprint
    $password = ConvertTo-SecureString -String "CHANGETHISPASSWORD" -Force -AsPlainText
    
    $fileName = "exportedcert.pfx" 
    Export-PfxCertificate -cert $certThumbprint -FilePath $fileName -Password $password

certificado Olá que geram desses comandos do PowerShell é sinalizado por navegadores porque Olá certificado não foi criado por uma autoridade de certificação que está na cadeia de confiança de seu navegador. tooget um certificado de confiança do seu navegador, primeiramente ele de uma autoridade de certificação comercial na cadeia de confiança de seu navegador. 

![Defina o certificado ILB][4]

tooupload seus próprios certificados e o acesso de teste:

1. Depois de saudação ASE é criado, vá toohello ASE da interface do usuário. Selecione **ASE** > **Configurações** > **Certificado ILB**.

2. tooset certificado ILB hello, selecione Olá certificado. pfx arquivo e insira a senha de saudação. Esta etapa leva alguns tooprocess de tempo. Será exibida uma mensagem informando que uma operação de carregamento está em andamento.

3. Obter o endereço ILB de saudação para seu ASE. Selecione **ASE** > **Propriedades** > **Endereço IP Virtual**.

4. Crie um aplicativo web no seu ASE depois Olá ASE é criado.

5. Se não tiver uma VM naquela VNet, crie uma.

    > [!NOTE] 
    > Não tente toocreate essa VM em Olá mesma sub-rede como Olá ASE porque irá falhar ou causar problemas.
    >
    >

6. Saudação de conjunto de DNS para seu domínio ASE. Você pode usar um caractere curinga com o seu domínio no DNS. toodo alguns simples testa, edite o arquivo de hosts de saudação em sua VM tooset Olá web aplicativo nome toohello endereço IP VIP:

    a. Se seu ASE tem o nome de domínio de saudação _. ilbase.com_ e criar o aplicativo web de saudação chamado _mytestapp_, é abordada em _mytestapp.ilbase.com_. Você então definir _mytestapp.ilbase.com_ endereço do tooresolve toohello ILB. (No Windows, o arquivo de hosts do hello está em _C:\Windows\System32\drivers\etc\_.)

    b. tootest web implantação publicação ou acesso toohello avançado do console, crie um registro para _mytestapp.scm.ilbase.com_.

7. Use um navegador nessa VM e acesse http://mytestapp.ilbase.com. (Ou vá toowhatever que é o nome do aplicativo web com o seu domínio).

8. Use um navegador nessa VM e acesse https://mytestapp.ilbase.com. Se você usar um certificado autoassinado, aceite a falta de saudação de segurança.

    endereço IP Olá para o ILB está listado em **endereços IP**. Essa lista também tem endereços IP de saudação usados pelo VIP externo hello e tráfego de entrada de gerenciamento.

    ![Endereço IP do ILB][5]

### <a name="web-jobs-functions-and-hello-ilb-ase"></a>Web trabalhos, funções e Olá ASE ILB

Funções e trabalhos da web têm suporte em uma ASE ILB, mas para Olá toowork portal com eles, você deve ter o site SCM do toohello de acesso de rede.  Isso significa que seu navegador deve ser em um host que está em ou rede virtual toohello conectada.  

Quando você usa funções do Azure em uma ASE ILB, você pode receber uma mensagem de erro que diz "não é capaz de tooretrieve suas funções no momento. Tente novamente mais tarde.” Esse erro ocorre porque Olá funções da interface do usuário utiliza o site SCM Olá via HTTPS e certificado de raiz de saudação não está na cadeia de navegador de saudação de confiança. Os trabalhos da Web têm um problema semelhante. tooavoid esse problema, você pode fazer um dos seguintes hello:

- Adicione repositório de certificados confiáveis de tooyour Olá certificado. Isso desbloqueia o Edge e o Internet Explorer.
- Usar o Chrome e acesse o site SCM do toohello primeiro, aceitar o certificado não confiável hello e vá toohello portal.
- Use um certificado comercial que esteja na sua cadeia de navegadores confiáveis.  Isso é Olá melhor opção.  

## <a name="dns-configuration"></a>Configuração de DNS ##

Quando você usar um VIP externo, Olá DNS é gerenciado pelo Azure. Qualquer aplicativo que criou no seu ASE é adicionado automaticamente tooAzure DNS, que é um DNS público. Em um ASE ILB, é necessário gerenciar seu próprio DNS. Para um determinado domínio como _contoso.net_, você precisa toocreate DNS A registros no DNS, endereço ponto tooyour ILB para:

- *.contoso.net
- *.scm.contoso.net

Se seu domínio ILB ASE é usado para várias coisas fora este ASE, talvez seja necessário toomanage DNS em cada nome por aplicativo. Esse método é um desafio, pois você precisará tooadd cada novo nome de aplicativo em seu DNS ao criá-lo. Por esse motivo, recomendamos que você use um domínio dedicado.

## <a name="publish-with-an-ilb-ase"></a>Publicação com um ASE ILB ##

Para cada aplicativo criado, há dois pontos de extremidade. Em um ASE ILB, você tem *&lt;nome do aplicativo>.&lt;Domínio do ASE ILB>* e *&lt;nome do aplicativo>.scm.&lt;Domínio do ASE ILB>*. 

nome do site SCM Olá leva console de Kudu toohello, chamado hello **portal avançado**no hello portal do Azure. console de Kudu Olá lhe permite exibir as variáveis de ambiente, explorar Olá disco, use um console e muito mais. Para obter mais informações, consulte [Console do Kudu para o Serviço de Aplicativo do Azure][Kudu]. 

Multilocatário de saudação do serviço de aplicativo e em uma ASE externos, não há logon único entre Olá portal do Azure e o console de Kudu hello. Para Olá ASE ILB, no entanto, você precisa toouse seu toosign credenciais publicação no console do Kudu hello.

Sistemas de CI baseado na Internet, como GitHub e o Visual Studio Team Services, não funcionam com uma ASE ILB porque o ponto de extremidade de publicação do hello não está acessível pela internet. Em vez disso, você precisa toouse um sistema de CI que usa um modelo de pull, como o Dropbox.

pontos de extremidade de publicação de saudação para aplicativos em uma ASE ILB usam domínio Olá que Olá com que ASE ILB foi criado. Este domínio é exibido no perfil de publicação do aplicativo hello e na folha de portal do aplicativo hello (**visão geral** > **Essentials** e também **propriedades**). Se você tiver uma ASE ILB com subdomínio Olá *contoso.net* e um aplicativo chamado *mytest*, use *mytest.contoso.net* para FTP e *mytest.scm.contoso.net*  para implantação da web.

## <a name="couple-an-ilb-ase-with-a-waf-device"></a>Como acoplar um ASE ILB com um dispositivo WAF ##

Serviço de aplicativo do Azure fornece várias medidas de segurança que protegem o sistema hello. Eles também ajudam a toodetermine se um aplicativo foi violado. Olá melhor proteção para um aplicativo web é toocouple uma plataforma de hospedagem, como o serviço de aplicativo do Azure, com um firewall do aplicativo web (WAF). Como Olá ASE ILB tem um ponto de extremidade do aplicativo de isolamento de rede, é apropriado para um uso.

toolearn mais sobre como tooconfigure ASE o ILB com um dispositivo WAF, consulte [configurar um firewall do aplicativo web com seu ambiente de serviço de aplicativo][ASEWAF]. Este artigo mostra como toouse um dispositivo virtual Barracuda com seu ASE. Outra opção é toouse Gateway de aplicativo do Azure. Application Gateway usa Olá OWASP core regras toosecure todos os aplicativos são colocados por trás dele. Para obter mais informações sobre o Application Gateway, consulte [firewall do aplicativo de web do Azure Introdução toohello][AppGW].

## <a name="get-started"></a>Introdução ##

Todos os artigos e como-tooinstructions para ASs estão disponíveis no [Leiame para ambientes de serviço de aplicativo][ASEReadme].

* tooget iniciado com ASs, consulte [ambientes de serviço Introdução tooApp][Intro].
* Para obter mais informações sobre a plataforma do serviço de aplicativo do Azure hello, consulte [do serviço de aplicativo do Azure](http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/).
 
<!--Image references-->
[1]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-network.png
[2]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-webapp.png
[3]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-certificate.png
[4]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-certificate2.png
[5]: ./media/creating_and_using_an_internal_load_balancer_with_app_service_environment/createilbase-ipaddresses.png

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
