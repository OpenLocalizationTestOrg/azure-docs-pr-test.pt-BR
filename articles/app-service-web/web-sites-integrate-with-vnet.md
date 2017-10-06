---
title: aaaIntegrate um aplicativo com uma rede Virtual do Azure
description: "Mostra como tooconnect um aplicativo de serviço de aplicativo do Azure tooa existente ou nova rede virtual do Azure"
services: app-service
documentationcenter: 
author: ccompy
manager: erikre
editor: cephalin
ms.assetid: 90bc6ec6-133d-4d87-a867-fcf77da75f5a
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: ccompy
ms.openlocfilehash: a93c504481400245b02220b541a008a7c874d10a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-your-app-with-an-azure-virtual-network"></a>Integrar seu aplicativo Web a uma Rede Virtual do Azure
Este documento descreve o recurso de integração de rede virtual do serviço de aplicativo do Azure hello e mostra como tooset-lo com aplicativos em [do serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714). Se você estiver familiarizado com redes virtuais do Azure (VNets), esse é um recurso que permite que você tooplace muitos dos recursos do Azure em uma rede de internet não routeable que você controlar o acessem. Essas redes podem ser redes locais de tooyour conectado usando uma variedade de tecnologias de VPN. toolearn mais sobre redes virtuais do Azure, inicie com informações de saudação aqui: [visão geral da rede Virtual do Azure][VNETOverview]. 

saudação do serviço de aplicativo do Azure tem duas formas. 

1. sistemas de vários locatários Olá que dão suporte a gama completa de saudação de planos de preços
2. recurso de premium do ambiente de serviço de aplicativo (ASE) de saudação, que implanta em sua rede virtual. 

Este documento passa pela Integração VNet e não pelo Ambiente de Serviço de Aplicativo. Se você quiser toolearn mais sobre o recurso de saudação ASE, começar com informações de saudação aqui: [introdução do ambiente de serviço de aplicativo][ASEintro].

Integração da VNet fornece seu tooresources de acesso do aplicativo web em sua rede virtual, mas não concede acesso privado tooyour web aplicativo de rede virtual hello. Acesso ao site privada refere-se toomaking seu aplicativo somente é acessível de uma rede privada, como de dentro de uma rede virtual do Azure. O acesso de site privado só está disponível com um ASE configurado com um ILB (Balanceador de carga interno). Para obter detalhes sobre como usar uma ASE ILB, inicie com o artigo de saudação aqui: [criando e usando uma ASE ILB][ILBASE]. 

Um cenário comum onde você usaria a integração da VNet é habilitando o acesso do seu banco de dados de tooa de aplicativo da web ou um serviço da web em execução em uma máquina virtual em sua rede virtual do Azure. Com a integração de rede virtual, você não precisa tooexpose um ponto de extremidade público para aplicativos em sua VM mas pode usar Olá privada internet não roteável endereços. 

recurso de integração da VNet Hello:

* requer um plano de preços Standard, Premium ou Isolado 
* funciona com VNet clássica ou do Gerenciador de Recursos 
* dá suporte a TCP e UDP
* funciona com aplicativos Web, móveis e de API
* permite que um tooonly tooconnect do aplicativo 1 rede virtual por vez
* permite que o toofive VNets toobe integrado com um plano de serviço de aplicativo 
* permite Olá mesmo toobe de rede virtual usada por vários aplicativos em um plano de serviço de aplicativo
* oferece suporte a um SLA de 99,9% de conclusão toohello SLA Olá Gateway de rede virtual

Há algumas coisas a que a integração VNet não dá suporte, incluindo:

* montagem de unidade
* integração ao AD 
* NetBios
* acesso a site privado

### <a name="getting-started"></a>Introdução
Aqui estão algumas coisas tookeep em mente antes de conectar sua rede virtual de tooa de aplicativo web:

* A integração VNet só funciona com aplicativos em um plano de preços **Standard**, **Premium** ou **Isolado**. Se você habilitar o recurso de saudação e, em seguida, dimensionar seu tooan de plano de serviço de aplicativo sem suporte preços do plano de seus aplicativos percam toohello suas conexões VNets que estão usando. 
* Se sua rede virtual de destino já existir, ele deverá ter VPN ponto a site habilitada com um gateway de roteamento dinâmico para que possa ser conectada tooan aplicativo. Se o gateway estiver configurado com roteamento Estático, não será possível habilitar a opção ponto a site da VPN (Rede virtual privada).
* Olá rede virtual deve estar no hello mesma assinatura que o Plan(ASP) de serviço do aplicativo. 
* Olá aplicativos que se integram com uma rede virtual usam Olá DNS especificado para essa rede virtual.
* Por padrão, seus aplicativos de integração somente rotear o tráfego em sua rede virtual com base nas rotas Olá que estão definidas na sua rede virtual. 

## <a name="enabling-vnet-integration"></a>Habilitar a integração VNet
Este documento destina-se principalmente em usando Olá portal do Azure para a integração de rede virtual. tooenable integração da VNet com seu aplicativo usando o PowerShell, execute instruções de saudação aqui: [conectar sua rede virtual do aplicativo tooyour usando PowerShell][IntPowershell].

Você tem Olá opção tooconnect seu aplicativo tooa existente ou nova rede virtual. Se você criar uma nova rede como parte de seu processo de integração, em seguida, além de criar toojust Olá VNet, um gateway de roteamento dinâmico é pré-configurado para você e ponto tooSite VPN estiver habilitada. 

> [!NOTE]
> A configuração de uma nova integração da rede virtual pode levar vários minutos. 
> 
> 

tooenable integração da rede virtual, abra o aplicativo configurações e, em seguida, selecione a rede. Saudação da interface do usuário que abre oferece três opções de rede. Este guia só aborda a integração VNet, mas as Conexões Híbridas e Ambientes de Serviço de Aplicativo são discutidos neste documento. 

Se seu aplicativo não estiver na saudação correta de preços do plano, Olá da interface do usuário permite que você tooscale sua tooa plano superior preços do plano de sua escolha.

![][1]

### <a name="enabling-vnet-integration-with-a-pre-existing-vnet"></a>Habilitar a integração VNet com uma VNet já existente
Saudação da interface do usuário de integração de rede virtual permite que você tooselect em uma lista de seus VNets. Olá VNets clássico indicar que eles são, com a palavra hello "Clássico" em nome de rede virtual toohello próximo parênteses. Olá lista é classificada de modo que hello VNets Gerenciador de recursos são listados primeiro. Olá imagem mostrada abaixo, você verá que pode ser selecionada apenas um VNet. Há vários motivos para uma VNet ficar esmaecida, incluindo:

* saudação de rede virtual está em outra assinatura que sua conta tem acesso ao
* saudação de rede virtual não tem ponto tooSite habilitado
* saudação de rede virtual não tem um gateway de roteamento dinâmico

![][2]

integração tooenable simplesmente clique no hello VNet que você deseja toointegrate com. Depois de selecionar Olá VNet, seu aplicativo será reiniciado automaticamente para Olá alterações tootake efeito. 

##### <a name="enable-point-toosite-in-a-classic-vnet"></a>Habilitar tooSite ponto em uma rede virtual clássica
Se a sua rede virtual não tem um gateway nem tem tooSite ponto, você tem tooset que primeiro backup. toodo isso para uma rede virtual clássica, vá toohello [portal do Azure] [ AzurePortal] e exibir lista de saudação de Networks(classic) Virtual. A partir daqui, clique na rede de saudação desejado toointegrate com e clique na caixa grande de saudação em Essentials chamado conexões VPN. A partir daqui, você pode criar seu VPN ponto toosite e até ter criar um gateway. Depois que você passe por Olá ponto toosite com a experiência de criação de gateway é cerca de 30 minutos antes de estar pronto. 

![][8]

##### <a name="enabling-point-toosite-in-a-resource-manager-vnet"></a>Habilitar ponto tooSite em uma VNet do Gerenciador de recursos
tooconfigure um Gerenciador de recursos de VNet com um gateway e tooSite ponto, você pode usar o PowerShell conforme documentado aqui, [configurar uma ponto para Site conexão tooa rede virtual usando o PowerShell] [ V2VNETP2S] ou use Olá portal do Azure conforme documentado aqui, [configurar um ponto para Site conexão tooa redes usando o portal do Azure de Olá][V2VNETPortal]. Saudação da interface do usuário tooperform esse recurso ainda não está disponível. Observe que você precisa toocreate certificados para configuração de ponto tooSite hello. Isso é configurado automaticamente quando você se conecta a seu toohello WebApp VNet. 

### <a name="creating-a-pre-configured-vnet"></a>Criar uma VNet pré-configurada
Se você quiser toocreate uma nova rede virtual que está configurada com um gateway e ponto a Site, da interface do usuário do sistema de rede do serviço de aplicativo hello tem Olá recurso toodo que mas apenas para uma rede virtual Gerenciador de recursos. Se você deseja toocreate uma VNet clássico com um gateway e ponto a Site, será necessário toodo isso manualmente por meio da interface de usuário de rede hello. 

toocreate VNet um Gerenciador de recursos por meio de saudação VNet integração da interface do usuário, basta selecionar **criar nova rede Virtual** e forneça o:

* Nome da VNET
* Bloco de endereço da VNET
* Nome da sub-rede
* Bloco de endereço da sub-rede
* Bloco de endereço do Gateway
* Bloco de endereço Ponto a site

Se desejar que esta tooany de tooconnect VNet outras redes, você deve evitar espaço de endereço IP que se sobrepõe a essas redes de separação. 

> [!NOTE]
> Criação da VNet do Gerenciador de recursos com um gateway leva cerca de 30 minutos e atualmente não se integra Olá VNet com seu aplicativo. Depois que sua rede virtual é criada com o gateway Olá você precisa toocome tooyour back aplicativo da interface do usuário de integração de rede virtual e selecione sua nova rede virtual.
> 
> 

![][3]

As VNets do Azure normalmente são criadas dentro de endereços de rede privada. Por saudação padrão integração da VNet recurso roteia todo o tráfego destinado a esses intervalos de endereços IP em sua rede virtual. intervalos de endereços IP privados Olá são:

* 10.0.0.0/8 - isso é Olá mesmo como 10.0.0.0 - 10.255.255.255
* 172.16.0.0/12 - isso é Olá mesmo como 172.16.0.0 - 172.31.255.255 
* 192.168.0.0/16 - isso é Olá mesmo como 192.168.0.0 - 192.168.255.255

Olá espaço de endereço de rede virtual precisa toobe especificado na notação CIDR. Se você estiver familiarizado com notação CIDR, ele é um método para especificar os blocos de endereço usando um endereço IP e um número inteiro que representa a máscara de rede de saudação. Como uma referência rápida, considere que 10.1.0.0/24 seria 256 endereços e 10.1.0.0/25 seria 128 endereços. Um endereço IPv4 com um /32 seria apenas 1 endereço. 

Se você definir aqui Olá informações do servidor DNS, que é definido para a sua rede virtual. Após a criação de rede virtual, você pode editar essas informações de saudação experiências de usuário de rede virtual. Se você alterar Olá DNS de saudação VNet, você precisa tooperform uma operação de sincronização de rede.

Quando você cria uma VNet clássico usando Olá da interface do usuário de integração de rede virtual, ele cria uma rede virtual no hello mesmo grupo de recursos que seu aplicativo. 

## <a name="how-hello-system-works"></a>Como funciona o sistema Olá
Sob as coberturas de saudação esse recurso se baseia nos tooconnect de tecnologia VPN ponto a Site tooyour seu aplicativo VNet. Aplicativos no Serviço de Aplicativo do Azure têm uma arquitetura de sistema multilocatário, que impede o provisionamento de um aplicativo diretamente em uma VNet, como ocorre com máquinas virtuais. Criando-se na tecnologia de ponto para site limitamos rede acesso toojust Olá máquina virtual que hospeda aplicativo hello. Acesso a rede toohello será restringida ainda mais nesses hosts de aplicativo para que seus aplicativos só possam acessar redes de saudação que configurá-las tooaccess. 

![][4]

Se você ainda não configurou um servidor DNS à sua rede virtual, seu aplicativo precisará toouse recurso de tooreach de endereços IP em redes de saudação. Ao usar endereços IP, lembre-se de que o benefício principal de saudação desse recurso é que ele permite que você toouse endereços privados do hello dentro de sua rede privada. Se você definir seu aplicativo backup toouse endereços IP públicos para uma das suas VMs, você não estiver usando o recurso de integração da VNet hello e está se comunicando por Olá da internet.

## <a name="managing-hello-vnet-integrations"></a>Gerenciando Olá integrações de rede virtual
Olá tooconnect de capacidade e desconecte tooa que rede virtual está em um nível de aplicativo. As operações que podem afetar a saudação integração da rede virtual entre vários aplicativos estão em um nível ASP. De saudação da interface do usuário que é mostrada no nível de aplicativo hello, você pode obter os detalhes em sua rede virtual. Maioria dos Olá mesmas informações também são mostradas no hello ASP níveis. 

![][5]

Na página de Status do recurso de rede hello, você pode ver se seu aplicativo estiver conectado tooyour VNet. Se o gateway da VNet estiver inativo por qualquer motivo, ele aparecerá como não conectado. 

informações de saudação tem agora tooyou disponível no aplicativo hello nível interface do usuário de integração de rede virtual é Olá mesmo como informações de detalhe de saudação obtido Olá ASP. Estes são os itens:

* Nome de rede virtual - este link abre Olá rede virtual do Azure da interface do usuário
* Local – isso reflete o local de saudação da sua rede virtual. É possível toointegrate com uma rede virtual em outro local.
* Status do certificado - não há certificados usados toosecure Olá VPN conexão entre o aplicativo hello e hello VNet. Isso reflete uma tooensure de teste que eles estão em sincronizado.
* Status do gateway - devem seus gateways fique inativo por algum motivo, em seguida, o aplicativo não pode acessar recursos em Olá VNet. 
* Espaço de endereço de rede virtual - este é o espaço de endereço IP Olá para sua rede virtual. 
* Espaço de endereço de ponto de tooSite - este é o espaço de endereço IP hello ponto toosite para sua rede virtual. Seu aplicativo mostra comunicação como provenientes de uma saudação IPs nesse espaço de endereço. 
* Espaço de endereço do site toosite - você pode usar o Site tooSite VPNs tooconnect tooyour sua rede virtual local recursos ou tooother VNet. Você tem que configurado e em seguida, os intervalos de IP hello definido com que a conexão VPN aparece aqui.
* Servidores DNS – Se você tiver servidores DNS configurados com sua VNet, eles serão listados aqui.
* IPs roteadas toohello VNet - há uma lista de endereços IP que sua rede virtual foi definida para o roteamento e esses endereços exibidos aqui. 

operação somente Hello, que você pode executar no modo de aplicativo hello de integração VNet é toodisconnect seu aplicativo do hello rede virtual está conectada atualmente à. toodo isso simplesmente, clique em Desconectar na parte superior da saudação. Essa ação não altera sua VNet. Olá rede virtual e sua configuração incluindo gateways Olá permanece inalterado. Em seguida, toodelete sua rede virtual, é necessário toofirst delete Olá recursos como gateways de saudação. 

Olá Exibir plano de serviço de aplicativo tem um número de operações adicionais. Ele é também acessado diferente que do aplicativo hello. Olá tooreach interface de usuário de rede do ASP simplesmente abra sua interface de usuário do ASP e role para baixo. Há um elemento de interface do usuário chamado Status do Recurso de Rede. Ele fornece alguns pequenos detalhes sobre a integração VNet. Clicar nessa interface do usuário abre Olá da interface do usuário de Status do recurso de rede. Se você clicar em "Clique aqui toomanage", Olá da interface do usuário que lista Olá integrações de rede virtual neste ASP abre.

![][6]

local de saudação do hello ASP é bom tooremember ao examinar os locais de saudação do hello VNets que você estiver integrando. Quando Olá rede virtual está em outro local tiver problemas de latência toosee muito mais prováveis. 

Olá VNets integrado ao é um lembrete em VNets quantos de que seus aplicativos estão integrados com este ASP e quantos você pode ter. 

toosee adicionado a cada VNet, basta clicar na Olá VNet que você está interessado em detalhes. Além de detalhes de toohello que foram observados anteriormente, você também pode ver uma lista de aplicativos de saudação neste ASP que estão usando essa rede virtual. 

Com respeito tooactions há são duas ações primárias. Olá primeiro é tooadd rotas Olá capacidade unidade tráfego deixar seu aplicativo em sua rede virtual. ação de segundo Olá é certificados de toosync de capacidade de saudação e informações de rede.

![][7]

**Roteamento** conforme observado anteriormente rotas Olá que estão definidas na sua rede virtual são o que é usado para direcionar o tráfego em sua rede virtual do seu aplicativo. Há alguns usos que onde os clientes querem toosend tráfego de saída adicionais de um aplicativo em redes de saudação e para eles essa funcionalidade é fornecida. O que acontece tráfego toohello depois do cliente de saudação toohow configura sua rede virtual. 

**Certificados** Olá certificado Status reflete uma verificação que está sendo executada pelo Olá toovalidate do serviço de aplicativo que certificados Olá que estamos usando Olá conexão VPN ainda são válidos. Ao habilitar a integração de rede virtual, se isso for toothat de integração primeira rede virtual Olá de todos os aplicativos neste ASP, haverá uma troca necessária de segurança de saudação tooensure certificados de conexão de saudação. Junto com certificados Olá obtemos a configuração do DNS hello, rotas e outras coisas semelhantes que descrevem a rede de saudação.
Se esses certificados ou informações de rede for alterado, você precisa tooclick "Rede de sincronização". **Observação**: quando você clica em "Sincronização Rede", pode causar uma breve interrupção na conectividade entre o aplicativo e a VNet. Enquanto seu aplicativo não for reiniciado, a perda de conectividade Olá pode causar seu site toonot funcionam corretamente. 

## <a name="accessing-on-premises-resources"></a>Como acessar recursos locais
Um dos benefícios de saudação do recurso de integração da VNet Olá é que se sua rede virtual está conectado tooyour local rede com uma VPN de tooSite do Site, seus aplicativos podem ter recursos de locais de tooyour de acesso do seu aplicativo. Para este toowork embora talvez seja necessário tooupdate seu gateway de VPN local com hello encaminha para o intervalo de IP tooSite ponto. Ao Olá Site tooSite VPN é primeiro configurar scripts de saudação usada tooconfigure ele deve definir rotas, incluindo sua VPN tooSite ponto. Se você adicionar Olá ponto tooSite VPN depois de criar seu tooSite Site VPN, será necessário rotas de saudação tooupdate manualmente. Obter detalhes sobre como toodo que varia de acordo com gateway e não são descritos aqui. 

> [!NOTE]
> recurso de integração da VNet Olá não integrar um aplicativo com uma rede virtual que possui um Gateway de rota expressa. Mesmo que Olá Gateway de rota expressa é configurado no [modo de coexistência] [ VPNERCoex] Olá integração da VNet não funciona. Se você precisa de recursos de tooaccess por meio de uma conexão de rota expressa, você pode usar um [ambiente de serviço de aplicativo][ASE], que é executado em sua rede virtual.
> 
> 

## <a name="pricing-details"></a>Detalhes de preço
Existem alguns preços nuances deve estar atento ao usar o recurso de integração da VNet hello. Há 3 encargos relacionados toohello usar esse recurso:

* Requisitos de tipo de preço do ASP
* Custos de transferência de dados
* Custos de gateway de VPN.

Para que seu toouse capaz de toobe aplicativos esse recurso, eles precisam toobe em um padrão ou um plano de serviço de aplicativo Premium. Você pode ver mais detalhes sobre esses custos aqui: [Preço do Serviço de Aplicativo][ASPricing]. 

Devido a tooSite ponto VPNs são tratadas de forma toohello, você sempre ter um encargo para dados de saída por meio de sua conexão de rede virtual integração mesmo se Olá VNet estiver em Olá mesmo Datacenter. toosee quais são esses encargos, dê uma olhada aqui: [detalhes de preços de transferência de dados][DataPricing]. 

Olá último item é custo Olá de gateways de rede virtual hello. Se não precisar de gateways de saudação algo como Site tooSite VPNs, você estiver pagando para recurso de integração da VNet gateways toosupport hello. Há detalhes sobre esses custos aqui: [Preço de Gateway de VPN][VNETPricing]. 

## <a name="troubleshooting"></a>Solucionar problemas
Enquanto o recurso de saudação é fácil tooset backup, isso não significa que a sua experiência será problema livre. Se você encontrar problemas para acessar seu ponto de extremidade desejado há são alguns utilitários que você pode usar a conectividade de tootest do console do aplicativo hello. Há duas experiências de console que você pode usar. Um é do console do Kudu hello e Olá outros console Olá que você pode entrar no portal do Azure de saudação. console de Kudu toohello tooget de seu aplicativo acesse tooTools -> Kudu. Isso é Olá mesmo que o muito [sitename]. scm.azurewebsites.net. Depois que abre toohello basta ir depuração console guia tooget toohello console hospedado portal do Azure, em seguida, a partir de seu aplicativo acesse tooTools -> Console. 

#### <a name="tools"></a>Ferramentas
o ping de ferramentas Hello, nslookup e tracert não funcionarão por meio do console Olá devido a restrições de toosecurity. void de saudação toofill existe foram duas ferramentas separadas adicionadas. Funcionalidade de ordem de DNS tootest adicionamos uma ferramenta chamada nameresolver.exe. Olá sintaxe é:

    nameresolver.exe hostname [optional: DNS Server]

Você pode usar nomes de host do nameresolver toocheck Olá que seu aplicativo depende. Dessa forma você pode testar se você tem tudo configurado incorretamente com o DNS ou talvez não tenha o servidor DNS tooyour acesso.

ferramenta da próxima Olá permite tootest para combinação de host e porta de tooa de conectividade do TCP. Essa ferramenta é chamada tcpping.exe e Olá sintaxe é:

    tcpping.exe hostname [optional: port]

Utilitário de tcpping Olá informa se você pode entrar em um host específico e uma porta. Ele só pode mostrar o êxito se: há um aplicativo de escuta na combinação de host e porta Olá e não há acesso de rede do host do aplicativo toohello especificado e a porta.

#### <a name="debugging-access-toovnet-hosted-resources"></a>Depuração tooVNet acesso a recursos hospedados
Há várias coisas que podem impedir que seu aplicativo alcance um host e uma porta específicos. A maioria do tempo de saudação é um dos três coisas:

* **Há um firewall em Olá maneira** se você tiver um firewall de forma hello, você atingirá o tempo limite TCP de saudação. Nesse caso, de 21 segundos. Use a conectividade do hello tcpping ferramenta tootest. Tempos limite TCP pode ser devido a coisas toomany além de firewalls, mas iniciar de lá. 
* **Não é possível acessar o DNS** Olá DNS limite é de três segundos por servidor DNS. Se você tiver dois servidores DNS, o tempo limite de saudação é 6 segundos. Use nameresolver toosee se o DNS está funcionando. Lembre-se de que você não pode usar nslookup que não usam Olá DNS de sua rede virtual é configurada com.
* **Intervalo inválido de P2S IP** precisa de intervalo IP de ponto toosite Olá toobe em intervalos IP privados Olá RFC 1918 (10.0.0.0-10.255.255.255 / 172.16.0.0-172.31.255.255 / 192.168.0.0-192.168.255.255). Se o intervalo de saudação usar IPs fora que, coisas não funcionarão. 

Se esses itens não respondem a seu problema, procure primeiro para tarefas simples, Olá como: 

* Olá Gateway são mostrados como estando backup no portal de Olá?
* Os certificados são mostrados como sincronizados?
* Qualquer pessoa alterar configuração de rede Olá sem fazer "Rede de sincronização" em páginas ASP de saudação afetada? 

Se o gateway estiver inativo, ative-o. Se os certificados estão fora de sincronizado, vá toohello ASP view de integração de sua rede virtual e ocorrências de "Rede de sincronização". Se você suspeitar de que houve uma configuração de rede virtual tooyour alteração feita e não era sincronização faria com sua páginas ASP, vá toohello ASP view de integração de sua rede virtual e ocorrências de "Rede de sincronização" apenas como um lembrete, isso faz com que uma breve interrupção com sua conexão de rede virtual e seus aplicativos . 

Se tudo isso é bom, você precisa toodig em um pouco mais:

* Há são todos os outros aplicativos usando os recursos de tooreach integração da VNet no hello mesma rede virtual? 
* Você vá toohello console de aplicativo e usar tcpping tooreach todos os outros recursos na sua rede virtual? 

Se qualquer uma das Olá acima forem verdadeira, em seguida, a integração de rede virtual é bom e problema Olá é em outro lugar. Isso é que ele obtém toobe mais desafiador porque não há nenhum toosee de maneira simples porque você não conseguir acessar uma host: porta. Algumas das causas Olá incluem:

* você tiver um firewall para cima em seu host impedindo acesso toohello aplicativo porta de seu intervalo de IP toosite ponto. O cruzamento de sub-redes geralmente exige acesso Público.
* o host de destino está inoperante
* seu aplicativo está inoperante
* você tinha IP errado hello ou nome de host
* seu aplicativo está escutando em uma porta diferente da que você esperava. Você pode verificar isso indo até que o host e usando "netstat - aon" do prompt de comando hello. Isso mostra qual ID de processo está escutando em qual porta. 
* os grupos de segurança de rede são configurados de modo que elas impedem que acessar tooyour host de aplicativo e a porta de seu intervalo de IP de ponto toosite

Lembre-se de que você não sabe quais IP no intervalo IP de ponto tooSite que seu aplicativo usará para que você precisa ter acesso de tooallow de todo o intervalo hello. 

As etapas de depuração adicionais incluem:

* Faça logon em outra VM em sua rede virtual e tente tooreach a recurso do host: porta de lá. Existem alguns utilitários de ping do TCP que você pode usar para essa finalidade, ou até mesmo usar o telnet, se for o caso. Olá finalidade aqui é toodetermine apenas se há conectividade dessa VM do outro. 
* abrir um aplicativo na outra VM e acessar toothat host e a porta de console de saudação do seu aplicativo de teste

#### <a name="on-premises-resources"></a>Recursos locais ####
Se seu aplicativo não pode acessar recursos locais, a primeira coisa que Olá deve verificar é se você pode acessar um recurso na sua rede virtual. Se isso funcionar, tente tooreach aplicativo de local hello de uma VM em Olá VNet. Você pode usar o telnet ou um utilitário de ping de TCP. Se sua VM não pode acessar o recurso local, verifique se que sua conexão de VPN Site tooSite está funcionando. Se ele está funcionando, marque Olá mesmas coisas observadas anteriormente, bem como a configuração de gateway local hello e status. 

Agora se sua rede virtual hospedado VM pode acessar o sistema local, mas seu aplicativo não motivo Olá é provavelmente uma das seguintes hello:

* suas rotas não estão configuradas com seus intervalos IP toosite ponto no seu gateway local
* os grupos de segurança de rede estão bloqueando o acesso para o intervalo de IP de ponto tooSite
* Os firewalls de local estão bloqueando o tráfego de seu intervalo IP de ponto tooSite
* Você tem um usuário definido Route(UDR) na sua rede virtual que impede que o tráfego de tooSite ponto com base em atingir sua rede local

## <a name="hybrid-connections-and-app-service-environments"></a>Conexões híbridas e ambientes de serviço de aplicativo
Há três recursos que permitem acessar os recursos tooVNet hospedado. Eles são:

* Integração VNet
* Conexões Híbridas
* Ambientes de Serviço de Aplicativo

Conexões híbridas requer tooinstall um agente de retransmissão chamado hello Manager(HCM) de Conexão híbrida na sua rede. Olá HCM precisa toobe tooconnect capaz de tooAzure e também tooyour aplicativo. Essa solução é especialmente boa usando uma rede remota, como sua rede local ou mesmo outra rede hospedada em nuvem, já que não exige um ponto de extremidade acessível pela Internet. Olá HCM só é executado no Windows e você pode ter até toofive instâncias em execução tooprovide alta disponibilidade. Conexões híbridas só oferece suporte a TCP embora e cada ponto de extremidade HC tem combinação do toomatch tooa host: porta específica. 

recurso do ambiente de serviço de aplicativo Hello permite que você toorun uma instância de saudação do serviço de aplicativo do Azure na sua rede virtual. Isso permite que seus aplicativos acessem os recursos de sua VNet sem etapas adicionais. Alguns dos Olá outros benefícios de um ambiente de serviço de aplicativo são que você pode usar os operadores de Dv2 com base em com too14 GB de RAM. Outra vantagem é que você pode dimensionar Olá sistema toomeet suas necessidades. Diferentemente dos ambientes de vários locatários Olá onde o ASP é limitado too20 instâncias, em uma ASE, você pode dimensionar too100 instâncias de ASP. Uma das coisas Olá que obter com uma ASE que não com a integração de rede virtual é que um ambiente de serviço de aplicativo podem trabalhar com uma VPN ExpressRoute. 

Embora haja que alguns usam sobreposição de caso, nenhum desses recursos outros pode substituir qualquer hello. Saber quais toouse de recurso é necessidades tooyour associado. Por exemplo:

* Se você for um desenvolvedor e deseja simplesmente toorun um site no Azure e tivê-lo acessar o banco de dados de saudação na estação de trabalho de saudação em sua mesa, hello mais fácil coisa toouse é conexões híbridas. 
* Se você é uma grande organização que deseja tooput um grande número de propriedades da web na nuvem pública hello e gerenciá-los em sua própria rede, você deseja toogo com hello ambiente de serviço de aplicativo. 
* Se você tiver um número de serviço de aplicativo hospedado aplicativos e deseja simplesmente tooaccess recursos na sua rede virtual, integração da VNet é toogo de maneira hello. 

Além de casos de uso de hello, existem algumas simplicidade relacionados aspectos. Se sua rede virtual já está conectado tooyour de rede, em seguida, usando a integração de rede virtual no local ou um ambiente de serviço de aplicativo é uma maneira fácil tooconsume recursos locais. Em Olá outro lado, se sua rede virtual não é tooyour local rede conectada é muito que mais tooset sobrecarga backup toosite um site VPN com sua rede virtual em comparação com a instalação Olá HCM. 

Além Olá diferenças funcionais, também são preços diferenças. recurso do ambiente de serviço de aplicativo Hello é um serviço de Premium oferecendo mas Olá oferece a maioria das possibilidades de configuração de rede além tooother excelentes recursos. Integração da rede virtual pode ser usada com o padrão ou páginas ASP o Premium e é perfeita para consumir com segurança os recursos na sua rede virtual da saudação multilocatário do serviço de aplicativo. Conexões híbridas atualmente depende de um conta, que tem níveis que iniciar livre e, em seguida, obtém progressivamente mais caro de preços com base na quantidade de saudação é necessário o BizTalk. Quando se trata de tooworking em várias redes no entanto, não há nenhum outro recurso, como conexões híbridas, que pode habilitar recursos tooaccess em mais de 100 redes separadas. 

<!--Image references-->
[1]: ./media/web-sites-integrate-with-vnet/vnetint-upgradeplan.png
[2]: ./media/web-sites-integrate-with-vnet/vnetint-existingvnet.png
[3]: ./media/web-sites-integrate-with-vnet/vnetint-createvnet.png
[4]: ./media/web-sites-integrate-with-vnet/vnetint-howitworks.png
[5]: ./media/web-sites-integrate-with-vnet/vnetint-appmanage.png
[6]: ./media/web-sites-integrate-with-vnet/vnetint-aspmanage.png
[7]: ./media/web-sites-integrate-with-vnet/vnetint-aspmanagedetail.png
[8]: ./media/web-sites-integrate-with-vnet/vnetint-vnetp2s.png

<!--Links-->
[VNETOverview]: http://azure.microsoft.com/documentation/articles/virtual-networks-overview/ 
[AzurePortal]: http://portal.azure.com/
[ASPricing]: http://azure.microsoft.com/pricing/details/app-service/
[VNETPricing]: http://azure.microsoft.com/pricing/details/vpn-gateway/
[DataPricing]: http://azure.microsoft.com/pricing/details/data-transfers/
[V2VNETP2S]: http://azure.microsoft.com/documentation/articles/vpn-gateway-howto-point-to-site-rm-ps/
[IntPowershell]: http://azure.microsoft.com/documentation/articles/app-service-vnet-integration-powershell/
[ASEintro]: http://docs.microsoft.com/azure/app-service/app-service-environment/intro
[ILBASE]: http://docs.microsoft.com/azure/app-service/app-service-environment/create-ilb-ase
[V2VNETPortal]: https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal
[VPNERCoex]: http://docs.microsoft.com/en-us/azure/expressroute/expressroute-howto-coexist-resource-manager
[ASE]: http://docs.microsoft.com/azure/app-service/app-service-environment/intro
