---
title: "Considerações sobre o aaaNetworking com um ambiente de serviço de aplicativo do Azure"
description: "Explica o tráfego de rede Olá ASE e como tooset NSGs e UDRs com seu ASE"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 955a4d84-94ca-418d-aa79-b57a5eb8cb85
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: ccompy
ms.openlocfilehash: d4d3000f4d4d75814b1e6d47079d967334eb1a3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="networking-considerations-for-an-app-service-environment"></a>Considerações de rede para um ambiente do Serviço de Aplicativo #

## <a name="overview"></a>Visão geral ##

 O [Ambiente do Serviço de Aplicativo][Intro] do Azure é uma implantação do Serviço de Aplicativo do Azure em uma sub-rede da sua VNet (VNet) do Azure. Há dois tipos de implantação para um ASE (ambiente de Serviço de Aplicativo):

- **ASE externo**: expõe Olá aplicativos hospedados ASE em um endereço IP acessível pela internet. Para saber mais, confira [Criar um ASE externo][MakeExternalASE].
- **ILB ASE**: expõe Olá aplicativos hospedados ASE em um endereço IP dentro de sua rede virtual. ponto de extremidade interno Olá é um balanceador de carga interno (ILB), por isso, ela é chamada uma ASE ILB. Para saber mais, confira [Criar e usar um ASE ILB][MakeILBASE].

Agora há duas versões do Ambiente do Serviço de Aplicativo: ASEv1 e ASEv2. Para obter informações sobre ASEv1, consulte [tooApp Introdução v1 do ambiente de serviço][ASEv1Intro]. O ASEv1 pode ser implantado em uma VNet clássica ou do Resource Manager. Um ASEv2 só pode ser implantado em uma VNet do Resource Manager.

Todas as chamadas de uma ASE que vão toohello internet deixe Olá redes por meio de um VIP atribuído Olá ASE. Olá IP público desse VIP é, em seguida, Olá IP de origem para todas as chamadas de saudação ASE que vão toohello internet. Se Olá aplicativos no seu ASE fazer chamadas tooresources na sua rede virtual ou por uma VPN, Olá IP de origem é uma saudação IPs na sub-rede Olá usado pelo seu ASE. Como Olá ASE em Olá VNet, também pode acessar recursos em Olá VNet sem qualquer configuração adicional. Se Olá rede virtual é conectada tooyour rede de local, aplicativos no seu ASE também terá acesso tooresources existe. Você não precisa tooconfigure Olá ASE ou seu aplicativo qualquer adicional.

![ASE externo][1] 

Se você tiver uma ASE externo, VIP público Olá também é o ponto de extremidade de saudação que seus aplicativos ASE resolver toofor:

* HTTP/S. 
* FTP/S. 
* Implantação da Web.
* Depuração remota.

![ILB ASE][2]

Se você tiver uma ASE ILB, o endereço IP de saudação do hello ILB é ponto de extremidade de saudação para HTTP/S, FTP/S, implantação da web e a depuração remota.

portas de acesso de aplicativo normal Olá são:

| Uso | Da | muito|
|----------|---------|-------------|
|  HTTP/HTTPS  | Configurável pelo usuário |  80, 443 |
|  FTP/FTPS    | Configurável pelo usuário |  21, 990, 10001-10020 |
|  Depuração remota no Visual Studio  |  Configurável pelo usuário |  4016, 4018, 4020, 4022 |

Isso será verdadeiro se você estiver em um ASE externo ou em um ASE ILB. Se você estiver em uma ASE externo, você atingir essas portas no VIP público hello. Se você estiver em uma ASE ILB, você atingir essas portas no hello ILB. Se você bloquear a porta 443, pode haver um efeito em alguns recursos apresentados no portal de saudação. Para saber mais, confira [Dependências do portal](#portaldep).

## <a name="ase-dependencies"></a>Dependências do ASE ##

Uma dependência de acesso de entrada do ASE é:

| Uso | Da | muito|
|-----|------|----|
| Gerenciamento | Endereços de gerenciamento do Serviço de Aplicativo | Sub-rede ASE: 454, 455 |
|  Comunicação interna ASE | Sub-rede ASE: todas as portas | Sub-rede ASE: todas as portas
|  Permitir a entrada do Azure Load Balancer | Azure Load Balancer | Sub-rede ASE: todas as portas
|  Endereços IP atribuídos ao aplicativo | Endereços atribuído de aplicativo | Sub-rede ASE: todas as portas

Olá o tráfego de entrada fornece comando e controle de saudação ASE no monitoramento de toosystem de adição. IPs de origem Olá para esse tráfego são listadas na Olá [gerenciamento ASE endereços] [ ASEManagement] documento. configuração de segurança de rede Olá precisa de acesso tooallow todos os IPs em portas 454 e 455.

Dentro da sub-rede Olá ASE há muitas portas usadas para comunicação de componente interno e eles podem alterar.  Isso exige que todas as portas de saudação em Olá ASE sub-rede toobe acessível da sub-rede de ASE hello. 

Para comunicação de saudação entre balanceador de carga do Azure hello e portas mínimas do Olá Olá ASE sub-rede que toobe necessário abrir são 454 e 455 de 16001. porta 16001 Olá é usada para tráfego de atividade de manter entre o balanceador de carga hello e ASE hello. Se você estiver usando uma ASE ILB, você pode bloquear o tráfego para baixo toojust Olá 454, 455, 16001 portas.  Se você estiver usando uma ASE externo necessário tootake em portas de acesso conta saudação normal do aplicativo.  Se você estiver usando endereços de aplicativo atribuído é necessário tooopen-tooall portas.  Quando um endereço é atribuído um aplicativo específico tooa, o balanceador de carga Olá usará portas que não são conhecidas com antecedência toosend HTTP e HTTPS tráfego toohello ASE.

Se você estiver usando endereços IP de aplicativo atribuído é necessário tooallow tráfego da saudação que IPS atribuídos subrede tooyour aplicativos toohello ASE.

Para acesso de saída, um ASE depende de vários sistemas externos. Essas dependências de sistema são definidas com nomes DNS e não mapeiam tooa fixa o conjunto de endereços IP. Assim, Olá ASE requer acesso de saída de hello ASE sub-rede tooall IPs externos em uma variedade de portas. Uma ASE tem Olá dependências de saída a seguir:

| Uso | Da | muito|
|-----|------|----|
| Armazenamento do Azure | Sub-rede ASE | table.core.windows.net, blob.core.windows.net, queue.core.windows.net, file.core.windows.net: 80, 443, 445 (445 só é necessário para o ASEv1). |
| Banco de Dados SQL do Azure | Sub-rede ASE | database.windows.net: 1433, 11000-11999, 14000-14999 (Para saber mais, confira [Uso da porta do Banco de Dados SQL V12](../../sql-database/sql-database-develop-direct-route-ports-adonet-v12.md).)|
| Gerenciamento do Azure | Sub-rede ASE | management.core.windows.net, management.azure.com: 443 
| Verificação de certificado SSL |  Sub-rede ASE            |  ocsp.msocsp.com, mscrl.microsoft.com, crl.microsoft.com: 443
| Azure Active Directory        | Sub-rede ASE            |  Internet: 443
| Gerenciamento do Serviço de Aplicativo        | Sub-rede ASE            |  Internet: 443
| DNS do Azure                     | Sub-rede ASE            |  Internet: 53
| Comunicação interna ASE    | Sub-rede ASE: todas as portas |  Sub-rede ASE: todas as portas

Se Olá ASE perde o acesso dependências toothese, ele deixará de funcionar. Quando isso acontece tempo suficiente, Olá ASE está suspenso.

### <a name="customer-dns"></a>DNS do cliente ###

Se hello VNet está configurada com um servidor DNS definido pelo cliente, cargas de trabalho de locatário Olá usarão-lo. Olá ASE ainda precisa toocommunicate com DNS do Azure para fins de gerenciamento. 

Se hello VNet estiver configurado com um cliente DNS no Olá outro lado de uma VPN, servidor DNS Olá deve ser acessível da sub-rede Olá que contém ASE hello.

<a name="portaldep"></a>

## <a name="portal-dependencies"></a>Dependências do portal ##

Dependências funcionais do toohello ASE de adição, há alguns experiência do portal toohello relacionados itens extras. Alguns dos recursos de saudação do hello portal do Azure dependem de acesso direto too_SCM site_. Para cada aplicativo no Serviço de Aplicativo do Azure, há duas URLs. Olá primeira URL é tooaccess seu aplicativo. Olá, segundo URL é tooaccess Olá SCM site, o que também é chamado de saudação _console Kudu_. Os recursos que usam o site SCM Olá incluem:

-   Trabalhos da Web
-   Funções
-   Streaming de log
-   Kudu
-   Extensões
-   Gerenciador de Processos
-   Console

Quando você usa uma ASE ILB, Olá SCM ainda não está acessível de fora da saudação VNet de internet. Quando seu aplicativo está hospedado em uma ASE ILB, alguns recursos não funcionarão no portal de saudação.  

Muitos desses recursos que dependem do site SCM Olá também estão disponíveis diretamente no console do Kudu hello. Você pode conectar tooit diretamente em vez de por meio do portal de saudação. Se seu aplicativo estiver hospedado em uma ASE ILB, use o toosign credenciais publicação no. site Olá URL tooaccess Olá SCM de um aplicativo hospedado em uma ASE ILB tem Olá formato a seguir: 

```
<appname>.scm.<domain name hello ILB ASE was created with> 
```

Se seu ASE ILB é o nome de domínio de saudação *contoso.net* e o nome do aplicativo é *testapp*, aplicativo hello é atingido em *testapp.contoso.net*. site SCM Olá que acompanha é atingido em *testapp.scm.contoso.net*.

### <a name="functions-and-web-jobs"></a>Funções e trabalhos Web ###

Funções e Web dependem Olá SCM site mas têm suporte para uso no portal de hello, mesmo que seus aplicativos estejam em uma ASE ILB, contanto que seu navegador pode acessar o site SCM hello.  Se você estiver usando um certificado autoassinado com seu ASE ILB, você precisará tooenable seu tootrust de navegador de certificado.  Para o IE e borda que significa que o certificado de saudação tem toobe na relação de confiança de computador Olá armazenar.  Se você estiver usando o Chrome, em seguida, o que significa que você aceita o certificado Olá no navegador Olá anteriormente supostamente atingindo o site de scm Olá diretamente.  Olá melhor solução é toouse um certificado comercial na cadeia de confiança do navegador de saudação.  

## <a name="ase-ip-addresses"></a>Endereços IP do ASE ##

Uma ASE tem alguns toobe de endereços IP atento. Eles são:

- **Endereço IP público de entrada**: usado para o tráfego de aplicativo em um ASE externo e o tráfego de gerenciamento em um ASE externo e em um ASE ILB.
- **Saída IP público**: usado como hello "de" IP para conexões de saída do ASE Olá Olá que deixe VNet, que não são roteadas para baixo de uma VPN.
- **Endereço IP do ILB**: se você usar um ASE ILB.
- **Endereços SSL com base em IP atribuídos ao aplicativo**: possível somente com um ASE externo e quando o SSL baseado em IP está configurado.

Todos esses endereços IP são facilmente visíveis em um ASEv2 no portal do Azure de saudação do hello ASE da interface do usuário. Se você tiver uma ASE ILB, IP de Olá Olá ILB está listado.

![Endereços IP][3]

### <a name="app-assigned-ip-addresses"></a>Endereços IP atribuídos ao aplicativo ###

Com uma ASE externos, você pode atribuir endereços IP tooindividual aplicativos. Você não pode fazer isso com um ASE ILB. Para obter mais informações sobre como tooconfigure toohave seu aplicativo seu próprio endereço IP, consulte [associar um personalizado SSL certificado tooAzure aplicativos web existentes](../../app-service-web/app-service-web-tutorial-custom-ssl.md).

Quando um aplicativo tem seu próprio endereço SSL com base em IP, Olá ASE reserva dois endereços IP portas toomap toothat. É uma porta para o tráfego HTTP e hello outra porta é para HTTPS. Essas portas são listadas na Olá ASE da interface do usuário na seção de endereços IP hello. O tráfego deve ser capaz de tooreach essas portas de saudação VIP ou Olá aplicativos não estão acessíveis. Esse requisito é tooremember importante quando você configura grupos de segurança de rede (NSGs).

## <a name="network-security-groups"></a>Grupos de segurança de rede ##

[Grupos de segurança de rede] [ NSGs] fornecer acesso à rede toocontrol Olá capacidade dentro de uma rede virtual. Quando você usar o portal de hello, há implícita negar regra no hello menor prioridade toodeny tudo. O que você cria são suas regras de permissão.

Em uma ASE, você não tem acesso toohello VMs usadas toohost Olá ASE em si. Elas estão em uma assinatura gerenciada pela Microsoft. Se você quiser toorestrict acesso toohello aplicativos Olá ASE, defina os NSGs na sub-rede do ASE hello. Dessa forma, preste muita atenção dependências de ASE toohello. Se você bloquear todas as dependências, Olá ASE para de funcionar.

Os NSGs podem ser configurados por meio de saudação portal do Azure ou por meio do PowerShell. informações de saudação aqui mostram Olá portal do Azure. Criar e gerenciar os NSGs no portal de saudação como um recurso de nível superior em **rede**.

Quando hello requisitos de entrada e saídos são levados em conta, Olá NSGs deve ter aparência semelhante NSGs toohello mostrados neste exemplo. Olá intervalo de endereços de rede virtual é _192.168.250.0/16_, e é Olá sub-rede Olá ASE em _192.168.251.128/25_.

requisitos de entrada duas primeiras Olá para Olá ASE toofunction são exibidos na parte superior de saudação da lista Olá neste exemplo. Eles habilitar o gerenciamento de ASE e permitem Olá ASE toocommunicate com ele mesmo. Olá outras entradas são todos os locatários configurável e podem controlar aplicativos hospedados ASE em rede acesso toohello. 

![Regras de segurança de entrada][4]

Uma regra padrão permite Olá IPs na sub-rede de ASE Olá VNet tootalk toohello. Outra regra padrão permite que o balanceador de carga hello, também conhecido como VIP público hello, toocommunicate com hello ASE. regras de padrão de saudação toosee, selecione **padrão regras** toohello próximo **adicionar** ícone. Se você colocar um deny tudo regra depois Olá NSG regras mostrado, impedir que o tráfego entre Olá VIP e ASE hello. tooprevent o tráfego proveniente de dentro Olá VNet, adicione seu próprios tooallow regra entrada. Usar um tooAzureLoadBalancer igual de origem com um destino de **qualquer** e um intervalo de portas de  **\*** . Como regra NSG de saudação é aplicado toohello ASE sub-rede, você não precisa toobe específico no destino hello.

Se você tiver atribuído um aplicativo de tooyour de endereço IP, certifique-se de que manter Olá portas abertas. portas de saudação toosee, selecione **ambiente de serviço de aplicativo** > **endereços IP**.  

Todos os itens de Olá Olá regras de saída a seguir mostrados são necessárias, exceto o último item do hello. Elas permitem que dependências ASE de toohello de acesso de rede que foram observadas anteriormente neste artigo. Se você bloquear qualquer uma delas, o ASE deixará de funcionar. último o item na lista de Olá Olá permite que seu toocommunicate ASE com outros recursos na sua rede virtual.

![Regras de segurança de saída][5]

Depois que seus NSGs são definidas, atribua toohello sub-rede seu ASE em. Se você não lembrar Olá ASE redes ou sub-redes, você poderá ver isso Olá ASE do portal de gerenciamento. tooassign Olá subrede tooyour NSG, vá toohello sub-rede da interface do usuário e selecione Olá NSG.

## <a name="routes"></a>Rotas ##

As rotas costumam se tornar problemáticas principalmente quando você configura a VNet com o Azure ExpressRoute. Há três tipos de rotas em uma VNet:

-   Rotas do sistema
-   Rotas BGP
-   UDRs (Rotas Definidas pelo Usuário)

Rotas de BGP que substituem as rotas do sistema. UDRs que substituem as rotas de BGP. Para saber mais sobre rotas em redes virtuais do Azure, confira [Visão geral das rotas definidas pelo usuário][UDRs].

banco de dados do SQL Azure Olá Olá ASE usa sistema de saudação toomanage tem um firewall. Ele requer comunicação toooriginate da saudação VIP público ASE. Conexões toohello SQL database do hello ASE será negado se eles são enviados para baixo Olá conexão de rota expressa e outro endereço de IP.

Se as solicitações de gerenciamento de tooincoming respostas são enviadas Olá rota expressa, endereço de resposta de saudação é diferente de destino original da saudação. Essa incompatibilidade interrompe a comunicação TCP hello.

Para sua toowork ASE enquanto sua rede virtual é configurado com uma rota expressa, hello mais fácil coisa toodo é:

-   Configurar rota expressa tooadvertise _0.0.0.0/0_. Por padrão, ele forçar túneis para todo o tráfego de saída local.
-   Crie um UDR. Aplicá-lo a sub-rede toohello que contém a saudação ASE com um prefixo de endereço _0.0.0.0/0_ e um próximo salto tipo de _Internet_.

Se você fizer essas duas alterações, destinado a internet tráfego originado da sub-rede de ASE Olá não forçado Olá rota expressa e hello ASE funciona. 

> [!IMPORTANT]
> rotas de saudação definidas em um UDR devem ser precedência tootake específica o suficiente sobre qualquer rotas anunciadas pela configuração de rota expressa hello. Hello exemplo anterior usa o intervalo de endereços do hello amplo 0.0.0.0/0. É possível que ele seja acidentalmente substituído pelos anúncios de rota que usam intervalos de endereços mais específicos.
>
> ASs não têm suporte com as configurações de rota expressa entre-anunciam rotas de saudação emparelhamento público toohello emparelhamento particular caminho. Configurações do ExpressRoute com emparelhamento público configurado recebem anúncios de rota da Microsoft. anúncios de saudação contêm um grande conjunto de intervalos de endereços IP do Microsoft Azure. Se os intervalos de endereços Olá entre anunciados no caminho de emparelhamento privado hello, todos os pacotes de saída de rede da sub-rede de saudação do ASE são infraestrutura de rede local do cliente de tooa em túnel de força. No momento, não há suporte para esse fluxo de rede com ASEs. Um problema de toothis de solução é toostop as rotas entre publicidade Olá emparelhamento público toohello emparelhamento particular caminho.

toocreate um UDR, siga estas etapas:

1. Vá toohello portal do Azure. Selecione **Rede** > **Tabelas de Rota**.

2. Criar uma nova tabela de rota em Olá mesma região que sua rede virtual.

3. Dentro da interface do usuário da tabela de rota, selecione **Rotas** > **Adicionar**.

4. Saudação de conjunto **tipo do próximo salto** muito**Internet** e hello **prefixo de endereço** muito**0.0.0.0/0**. Selecione **Salvar**.

    Você verá algo parecido com hello seguinte:

    ![Rotas funcionais][6]

5. Depois de criar a nova tabela de rotas hello, vá toohello sub-rede que contém seu ASE. Selecione sua tabela de rotas na lista de saudação do portal hello. Depois que você salva a alteração de hello, você deve ver, em seguida, Olá NSGs e rotas anotadas com a sua sub-rede.

    ![NSGs e rotas][7]

### <a name="deploy-into-existing-azure-virtual-networks-that-are-integrated-with-expressroute"></a>Implantar em redes virtuais existentes do Azure integradas ao ExpressRoute ###

toodeploy seu ASE em uma rede virtual que esteja integrada com o ExpressRoute, pré-configurar sub-rede Olá onde você deseja ASE Olá implantado. Em seguida, usar um toodeploy de modelo do Gerenciador de recursos-lo. toocreate uma ASE em uma rede virtual que já tenha configurada de rota expressa:

- Crie uma saudação de toohost sub-rede ASE.

    > [!NOTE]
    > Nada mais pode estar na sub-rede Olá mas ASE hello. Ser toochoose-se de um espaço de endereço que possibilita o crescimento futuro. Você não poderá alterar essa configuração mais tarde. Recomendamos um tamanho de `/25`, com 128 endereços.

- Criar UDRs (por exemplo, tabelas de rota), conforme descrito anteriormente e defina que na sub-rede hello.
- Criar hello ASE usando um modelo do Gerenciador de recursos, conforme descrito em [criar uma ASE usando um modelo do Gerenciador de recursos][MakeASEfromTemplate].

<!--Image references-->
[1]: ./media/network_considerations_with_an_app_service_environment/networkase-overflow.png
[2]: ./media/network_considerations_with_an_app_service_environment/networkase-overflow2.png
[3]: ./media/network_considerations_with_an_app_service_environment/networkase-ipaddresses.png
[4]: ./media/network_considerations_with_an_app_service_environment/networkase-inboundnsg.png
[5]: ./media/network_considerations_with_an_app_service_environment/networkase-outboundnsg.png
[6]: ./media/network_considerations_with_an_app_service_environment/networkase-udr.png
[7]: ./media/network_considerations_with_an_app_service_environment/networkase-subnet.png

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
[ASEManagement]: ./management-addresses.md
