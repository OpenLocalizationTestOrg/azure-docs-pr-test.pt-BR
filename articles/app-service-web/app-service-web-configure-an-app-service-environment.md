---
title: "aaaHow tooConfigure v1 um ambiente de serviço de aplicativo"
description: "Configuração, gerenciamento e monitoramento de saudação v1 do ambiente de serviço de aplicativo"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: b5a1da49-4cab-460d-b5d2-edd086ec32f4
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: f9539a72517276d8a1e340a408841561e8b8f56d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-an-app-service-environment-v1"></a>Configuração de um Ambiente do Serviço de Aplicativo v1

> [!NOTE]
> Este artigo é sobre Olá v1 do ambiente de serviço de aplicativo.  Há uma versão mais recente do hello ambiente de serviço de aplicativo que é mais fácil toouse e é executado na infraestrutura mais avançada. toolearn mais sobre a nova versão de hello começam com hello [Introdução toohello ambiente de serviço de aplicativo](../app-service/app-service-environment/intro.md).
> 

## <a name="overview"></a>Visão geral
Em um nível elevado, um Ambiente do Serviço de Aplicativo do Azure consiste em vários componentes principais:

* Serviço hospedado de recursos de computação que são executados em Olá ambiente de serviço de aplicativo
* Armazenamento
* Um banco de dados
* Uma VNet (rede virtual) do Azure Clássica (V1) ou do Resource Manager (V2) 
* Uma sub-rede com o serviço do ambiente de serviço de aplicativo hospedado Olá em execução

### <a name="compute-resources"></a>Recursos de computação
Você pode usar os recursos de computação Olá para os pools de recursos de quatro.  Cada ASE (Ambiente do Serviço de Aplicativo) tem um conjunto de front-ends e três pools de trabalho possíveis. Não é necessário toouse todos os pools de trabalho três – se desejar, você pode usar apenas um ou dois.

hosts Olá Olá pools de recursos (front-ends e operadores) não são diretamente acessíveis tootenants. Você não pode usar o protocolo de área de trabalho remota (RDP) tooconnect toothem, alterar o provisionamento ou agir como um administrador neles.

Você pode definir o tamanho e a quantidade de pools de recursos. Em um ASE, você tem quatro opções de tamanho, que são rotuladas P1 a P4. Para obter detalhes sobre esses tamanhos e seus preços, confira [Preços do Serviço de Aplicativo](../app-service/app-service-value-prop-what-is.md).
Alterando a quantidade de saudação ou tamanho é chamado de uma operação em escala.  Apenas uma operação de escala pode ocorrer por vez.

**Front-ends**: front-ends Olá são pontos de extremidade de HTTP/HTTPS Olá para os aplicativos que são mantidos na sua ASE. Você não executar cargas de trabalho em Olá front-ends.

* Um ASE começa com duas P2s, o que é suficiente para cargas de trabalho de desenvolvimento e teste e para cargas de trabalho de produção de nível baixo. É altamente recomendável P3s para tooheavy moderada cargas de trabalho de produção.
* Para cargas de trabalho de produção tooheavy moderada, recomendamos que você tenha pelo menos quatro tooensure P3s há suficientes front-ends executar quando ocorre de manutenção agendada. As atividades de manutenção agendada desligarão um front-end de cada vez. Isso reduz a capacidade de front-end disponível no geral durante as atividades de manutenção.
* Front-ends podem demorar até tooan tooprovision de hora. 
* Para ajustar escala adicional, você deve monitorar o percentual de CPU hello, porcentagem de memória e métricas de solicitações ativas para o pool de front-end de saudação. Se os percentuais de CPU ou memória Olá estiverem acima de 70% ao executar P3s, adicione mais front-ends. Se o valor de solicitações ativas de saudação calcula média too15, o too20 000 000 solicitações por front-end, você também deve adicionar mais front-ends. Olá meta geral é percentuais de memória abaixo de 70% e solicitações ativas média out toobelow 15.000 solicitações por front-end, quando você estiver executando P3s e tookeep da CPU.  

**Os operadores**: trabalhadores Olá estão onde seus aplicativos realmente executam. Quando você escala verticalmente planos do serviço de seu aplicativo usará os funcionários de saudação associados pool do trabalhador.

* Não é possível adicionar trabalhadores instantaneamente. Eles podem ocupar tooan tooprovision de hora.
* A escala de tamanho de saudação de um recurso de computação de qualquer pool levará < 1 hora por domínio de atualização. Há 20 domínios de atualização em um ASE. Se você escala de tamanho de computação de saudação de um pool de trabalho com 10 instâncias, ele pode levar até too10 horas toocomplete.
* Se você alterar o tamanho de Olá Olá de recursos de computação que são usados em um pool de trabalho, você fará com que frios de saudação aplicativos em execução nesse pool de trabalho.

Olá toochange tamanho de recursos de um pool de trabalho que não esteja executando aplicativos de computação de maneira mais rápida de saudação é:

* Reduzi a quantidade de saudação de trabalhadores too2.  a escala mínima Olá para baixo de tamanho no portal de saudação é 2. Levará alguns toodeallocate de minutos suas instâncias. 
* Selecione o novo tamanho de computação hello e número de instâncias. A partir daqui, demorará too2 toocomplete de horas.

Se os aplicativos exigirem um tamanho maior de recursos de computação, não é possível aproveitar orientação de saudação anterior. Em vez de alterar o tamanho de saudação do pool do trabalhador Olá que está hospedando os aplicativos, você pode preencher a outro pool de trabalho com os operadores de tamanho de saudação desejado e mover seus aplicativos em pool toothat.

* Crie instâncias adicionais de saudação do hello necessário calcular o tamanho em outro pool de trabalho. Isso levará a tooan toocomplete de hora.
* Reatribua seus planos de serviço de aplicativo que estão hospedando Olá aplicativos que precisam de um pool de trabalho maior tamanho toohello configurado recentemente. Essa é uma operação rápida que deve levar menos de um minuto toocomplete.  
* Reduzi o pool de trabalho Olá primeiro se não precisar mais dessas instâncias não utilizadas. Essa operação usa toocomplete de alguns minutos.

**Dimensionamento automático**: uma das ferramentas de saudação que podem ajudá-lo a toomanage o consumo de recursos de computação é dimensionamento automático. Você pode usar o dimensionamento automático para o front-end ou para os pools de trabalho. Você pode fazer coisas como o aumento de suas instâncias de qualquer tipo de pool manhã hello e reduzi-lo noite hello. Ou talvez você possa adicionar instâncias quando o número de saudação de trabalhos que estão disponíveis em um pool de trabalho cai abaixo de um certo limite.

Se você deseja que as regras de AutoEscala tooset em torno de métricas de pool de recursos de computação, manter no tempo de saudação mente esse provisionamento requer. Para obter mais detalhes sobre o dimensionamento automático de ambientes de serviço de aplicativo, consulte [como tooconfigure AutoEscala em um ambiente de serviço de aplicativo][ASEAutoscale].

### <a name="storage"></a>Armazenamento
Cada ASE é configurado com 500 GB de armazenamento. Este espaço é usado em todos os aplicativos de Olá Olá ASE. Esse espaço de armazenamento é uma parte da saudação ASE e atualmente não pode ser alternada toouse seu espaço de armazenamento. Se você estiver fazendo ajustes tooyour rede virtual ou segurança, você precisa toostill permitir acesso tooAzure armazenamento – ou Olá ASE não funcionará.

### <a name="database"></a>Banco de dados
banco de dados de Olá mantém informações de saudação que definem o ambiente hello, bem como detalhes Olá Olá aplicativos em execução dentro dele. Isso é muito parte da saudação assinatura mantido pelo Azure. Não é algo que você tenha um toomanipulate capacidade direto. Se você estiver fazendo ajustes tooyour rede virtual ou segurança, você precisa toostill permitir acesso tooSQL Azure – ou Olá ASE não funcionará.

### <a name="network"></a>Rede
Olá rede virtual que é usado com seu ASE pode ser um que você fez quando você criou Olá ASE ou que você fez antecipadamente. Quando você cria sub-redes Olá durante a criação do ASE, ele força toobe Olá ASE em Olá mesmo grupo de recursos, como a rede virtual hello. Se você precisar de grupo de recursos de saudação usado pelo seu toobe ASE diferente da sua rede virtual, em seguida, você precisa toocreate seu ASE usando um modelo do Gerenciador de recursos.

Há algumas restrições na rede virtual de saudação que é usado para uma ASE:

* rede virtual Olá deve ser uma rede virtual regional.
* Deve toobe uma sub-rede com 8 ou mais endereços onde Olá ASE é implantado.
* Depois de uma sub-rede é usado toohost uma ASE, intervalo de endereços de saudação da sub-rede Olá não pode ser alterado. Por esse motivo, é recomendável que essa sub-rede Olá contém pelo menos de 64 endereços tooaccommodate qualquer crescimento futuro de ASE.
* Pode haver nada mais na sub-rede Olá mas ASE hello.

Ao contrário do serviço de saudação hospedado que contém ASE hello, Olá [rede virtual] [ virtualnetwork] e sub-rede estão sob o controle de usuário.  Você pode administrar sua rede virtual por meio de saudação interface de usuário de rede Virtual ou o PowerShell.  Um ASE pode ser implantado em uma VNet clássica ou do Resource Manager.  portal Hello e experiências de API são um pouco diferentes entre clássico e o Gerenciador de recursos VNets mas Olá experiência ASE é Olá mesmo.

Olá VNet toohost usado uma ASE pode usar qualquer um dos endereços de IP de RFC1918 ou pode usar endereços IP públicos.  Se desejar toouse um intervalo IP que não é coberto por RFC1918 (10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16) necessário toocreate seu toobe VNet e sub-rede usada por seu ASE à frente criação ASE.

Como esse recurso coloca saudação do serviço de aplicativo do Azure em sua rede virtual, isso significa que os aplicativos que são hospedados em sua ASE agora podem acessar recursos que estão disponíveis por meio de rota expressa ou site a site redes virtuais privadas (VPNs) diretamente. Olá aplicativos que estão em seu ambiente de serviço de aplicativo não exigem rede recursos tooaccess recursos disponíveis toohello rede virtual adicionais que está hospedando o seu ambiente de serviço de aplicativo. Isso significa que você não precisa toouse tooresources tooget integração da VNET ou conexões híbridas no ou rede virtual tooyour conectado. Você ainda pode usar ambos os recursos que tooaccess recursos nas redes que não estão conectados a rede virtual tooyour.

Por exemplo, você pode usar a integração da VNET toointegrate com uma rede virtual que está em sua assinatura, mas não está conectado toohello rede virtual que é seu ASE em. Você ainda também pode usar conexões híbridas tooaccess recursos em outras redes, exatamente como faria normalmente.  

Se você tiver sua rede virtual configurado com uma VPN ExpressRoute, lembre-se de algumas das necessidades de roteamento de saudação que tenha uma ASE. Há algumas configurações de UDR (rota definida pelo usuário) que são incompatíveis com um ASE. Para obter mais detalhes sobre como executar um ASE em uma rede virtual com o ExpressRoute, confira [Executando um Ambiente de Serviço de Aplicativo em uma rede virtual com o ExpressRoute][ExpressRoute].

#### <a name="securing-inbound-traffic"></a>Protegendo o tráfego de entrada
Há dois toocontrol de métodos principais ASE de tooyour de tráfego de entrada.  Você pode usar o IP toocontrol Groups(NSGs) de segurança de rede endereços podem acessar seu ASE conforme descrito aqui [como o tráfego em um ambiente de serviço de aplicativo de entrada toocontrol](app-service-app-service-environment-control-inbound-traffic.md) e você também pode configurar seu ASE com uma carga interno Balancer(ILB).  Esses recursos também podem ser usados juntas se quiser acesso toorestrict usando NSGs tooyour ASE ILB.

Quando você cria um ASE, ele cria um VIP em sua rede virtual.  Há dois tipos de VIP, internos e externos.  Quando você cria um ASE com um VIP externo, seus aplicativos no ASE poderão ser acessados por meio de um endereço IP que pode ser roteado na Internet. Quando você seleciona seu ASE interno, ele será configurado com um ILB e não poderá ser acessado diretamente pela Internet.  Um ASE ILB ainda requer um VIP externo, mas ele é usado somente para acesso de gerenciamento e manutenção do Azure.  

Durante a criação de ILB ASE você fornece subdomínio Olá usado pelo Olá ASE ILB e terá toomanage seu próprio DNS para o subdomínio Olá que você especificar.  Como você define o nome de subdomínio Olá também é necessário certificado de saudação toomanage usado para acesso HTTPS.  Após ASE criação que tiver solicitado tooprovide certificado de saudação.  ler toolearn mais sobre como criar e usar uma ASE ILB [usando um balanceador de carga interno com um ambiente de serviço de aplicativo][ILBASE]. 

## <a name="portal"></a>Portal
Você pode gerenciar e monitorar seu ambiente de serviço de aplicativo usando a saudação da interface do usuário no portal do Azure de saudação. Se você tiver uma ASE, são provavelmente toosee Olá símbolo do serviço de aplicativo em sua barra lateral. Este símbolo é ambientes de serviço de aplicativo toorepresent usado no hello portal do Azure:

![Símbolo do Ambiente do Serviço de Aplicativo][1]

tooopen Olá da interface do usuário que lista todos os seus ambientes de serviço de aplicativo, você pode usar divisa Olá select ou no ícone de saudação (">" símbolo) na parte inferior de saudação do hello barra lateral tooselect ambientes de serviço de aplicativo. Selecionando uma saudação ASs listados, abra Olá da interface do usuário que é usada toomonitor e gerenciá-lo.

![Interface do usuário para monitorar e gerenciar seu Ambiente de Serviço de Aplicativo][2]

A primeira folha mostra algumas propriedades do seu ASE junto com um gráfico de métricas por pool de recursos. Algumas das propriedades de saudação que são mostradas no hello **Essentials** bloco também são hiperlinks que abrirá a folha de saudação que está associada ele. Por exemplo, você pode selecionar Olá **rede Virtual** nome tooopen a saudação da interface do usuário associada com a rede virtual de saudação seu ASE em execução no. Os **Planos do Serviço de Aplicativo** e os **Aplicativos** abrem folhas que listam esses itens em seu ASE.  

### <a name="monitoring"></a>Monitoramento
Olá gráficos permitem toosee uma variedade de métricas de desempenho em cada pool de recursos. Para o pool de front-end hello, você pode monitorar Olá média de CPU e memória. Para os pools de trabalho, você pode monitorar Olá que é usada e quantidade Olá que está disponível.

Serviço de aplicativo de vários planos podem fazer o uso de trabalhadores de saudação em um pool de trabalho. carga de trabalho de saudação não é distribuída no mesmo modo como com servidores de front-end hello, para uso de CPU e memória Olá não fornecem muito em forma de saudação de informações úteis de saudação. É mais importante tootrack quantos operadores que você usou e estão disponível – especialmente se você estiver gerenciando o sistema para outros toouse.  

Você também pode usar todas as métricas de saudação que podem ser acompanhadas no hello gráficos tooset alertas. Configurar alertas aqui funciona Olá mesmo como em outro lugar no serviço de aplicativo. Você pode configurar um alerta de qualquer Olá **alertas** UI parte ou de busca detalhada em métricas de interface do usuário e selecionando **adicionar alerta**.

![Interface do usuário Métricas][3]

métricas de saudação apenas discutidos são métricas de ambiente de serviço de aplicativo hello. Também há métricas que estão disponíveis no nível do plano de serviço de aplicativo de saudação. Nesse local, o monitoramento de CPU e da memória faz muito sentido.

Em uma ASE todos Olá que planos de serviço de aplicativo são planos de serviço de aplicativo dedicados. Isso significa que o hello somente aplicativos que estão em execução no hello hosts alocadas toothat plano de serviço de aplicativo estão Olá aplicativos no plano de serviço de aplicativo. detalhes de toosee em seu plano de serviço de aplicativo, exibir seu plano de serviço de aplicativo de qualquer uma das listas de Olá Olá ASE da interface do usuário ou de **planos de serviço de aplicativo procurar** (que lista todos eles).   

### <a name="settings"></a>Configurações
Na folha de saudação ASE, há um **configurações** seção que contém vários recursos importantes:

**Configurações de** > **propriedades**: Olá **configurações** folha é aberto automaticamente quando você abre a folha ASE. Olá superior é **propriedades**. Há um número de itens que são redundante toowhat que você vê no aqui **Essentials**, mas o que é muito útil é **endereço IP Virtual**, bem como **endereços de IP de saída**.

![Folha Configurações e propriedades][4]

**Configurações** > **Endereços IP**: ao criar um aplicativo de IP SSL (protocolo SSL) em seu ASE, você precisará de um endereço IP SSL. Em ordem tooobtain um, seu ASE precisa de endereços IP SSL é proprietária que podem ser alocados. Quando um ASE é criado, ele conta com um endereço IP SSL para essa finalidade, mas você pode adicionar mais. Há um custo para endereços de IP SSL adicionais, conforme mostrado no [preços do serviço de aplicativo] [ AppServicePricing] (na seção Olá conexões SSL). preço de saudação adicional é hello preço de IP SSL.

**Configurações de** > **Pool Front-End** / **Pools de trabalhadores**: cada essas folhas de pool de recursos oferece informações de toosee de capacidade de saudação somente no pool de recursos , além de tooproviding controla toofully escala pool de recursos.  

folha de base Olá para cada pool de recursos fornece um gráfico com métricas para o pool de recursos. Assim como com gráficos de saudação da folha de ASE hello, você pode entrar no gráfico de saudação e configurar os alertas conforme desejado. Definir um alerta de folha de ASE Olá para um pool de recursos específicos Olá mesma coisa que fazê-lo do pool de recursos de saudação. Do pool do trabalhador Olá **configurações** folha, ter Olá tooall de acesso aplicativos ou planos de serviço de aplicativo que estão em execução nesse pool de trabalho.

![Interface do usuário de configurações do pool de trabalho][5]

### <a name="portal-scale-capabilities"></a>Recursos de dimensionamento do portal
Existem três operações em escala:

* Alterando o número de saudação de endereços IP no hello ASE que estão disponíveis para uso de SSL de IP.
* Alterar tamanho Olá Olá do recurso de computação que é usado em um pool de recursos.
* Alterando o número de saudação de recursos de computação que são usados no pool de recursos manualmente ou por meio de dimensionamento automático.

No portal de hello, há três toocontrol de maneiras quantos servidores que você tem em seus pools de recursos:

* Uma operação de escala da folha de ASE principal Olá na parte superior da saudação. Você pode fazer o dimensionamento várias alterações de configuração toohello front-end e grupos de trabalho. Elas são aplicadas como uma única operação.
* Uma operação em escala manual do pool de recursos individuais do hello **escala** folha, que está sob **configurações**.
* Dimensionamento automático, que você configura do pool de recursos individuais do hello **escala** folha.

operação de dimensionamento de saudação toouse na folha de ASE Olá, arraste a quantidade de toohello do controle deslizante Olá desejadas e salve. Essa interface do usuário também suporta tamanho Olá alteração.  

![Interface do usuário de escala][6]

os recursos toouse manual ou de dimensionamento automático de saudação em um pool de recursos específico, vá muito**configurações** > **Pool Front-End** / **Pools de trabalhadores** como apropriado. Abra o pool de saudação que você deseja toochange. Vá muito**configurações** > **expansão** ou **configurações** > **aumentar**. Olá **expansão** folha permite toocontrol quantidade de instância. **Aumentar** permite que você toocontrol o tamanho de recursos.  

![Interface do usuário de configurações de escala][7]

## <a name="fault-tolerance-considerations"></a>Considerações sobre a tolerância a falhas
Você pode configurar toouse um ambiente de serviço de aplicativo too55 recursos de computação total. Desses recursos de computação 55, apenas 50 pode ser usado toohost cargas de trabalho. motivo Olá é dupla. Há um mínimo de dois recursos de computação front-end.  Isso deixa a alocação de pool do trabalhador too53 toosupport hello. Tolerância a falhas tooprovide ordem, são necessárias toohave um recurso de computação adicionais que é alocado toohello seguindo as regras de acordo com:

* Cada pool de trabalho precisa de pelo menos 1 recursos de computação adicionais que não está disponível toobe atribuído a uma carga de trabalho.
* Quando a quantidade de saudação de recursos de computação em um pool de trabalho fica acima de um determinado valor, o outro recurso de computação é necessário para tolerância a falhas. Não, esse é o caso de Olá no pool de front-end de saudação.

Dentro de qualquer pool de trabalho único, requisitos de tolerância a falhas de saudação são para um determinado valor de X recursos atribuídos tooa pool de trabalho:

* Se X for entre 2 e 20, o valor de saudação utilizável de recursos de computação que você pode usar para cargas de trabalho é x-1.
* Se X for entre 21 e 40, quantidade Olá utilizável de recursos de computação que você pode usar para cargas de trabalho é X-2.
* Se X for entre 41 e 53, a quantidade de saudação utilizável de recursos de computação que você pode usar para cargas de trabalho é X-3.

requisitos mínimos de saudação tem 2 servidores front-end e 2 trabalhadores.  Com hello acima, em seguida, instruções, aqui estão alguns tooclarify de exemplos:  

* Se você tem 30 trabalhadores em um único pool, 28 deles pode ser usado toohost cargas de trabalho.
* Se você tiver 2 trabalhadores em um único pool, 1 pode ser usado toohost cargas de trabalho.
* Se você tiver 20 trabalhadores em um único pool, 19 pode ser usado toohost cargas de trabalho.  
* Se você tiver 21 trabalhadores em um único pool, 19 ainda somente pode ser usado toohost cargas de trabalho.  

proporção de tolerância a falhas de saudação é importante, mas você precisa tookeep-se de que você dimensione acima a determinados limites. Se você quiser tooadd mais capacidade de 20 instâncias e, em seguida, vá too22 ou superior como 21 não adiciona qualquer mais capacidade. Olá que mesmo é verdadeiro vai acima 40, onde o próximo número de saudação que adiciona capacidade é 42.  

## <a name="deleting-an-app-service-environment"></a>Excluindo um Ambiente do Serviço de Aplicativo
Se você quiser toodelete um ambiente de serviço de aplicativo, em seguida, simplesmente use Olá **excluir** ação na parte superior de saudação da folha de ambiente de serviço de aplicativo hello. Quando você fizer isso, você estará tooenter solicitadas nome de saudação do seu tooconfirm do ambiente de serviço de aplicativo que você realmente deseja toodo. Observe que quando você exclui um ambiente de serviço de aplicativo, você excluir todo o conteúdo de saudação também dentro dele.  

![Interface do usuário Excluir um Ambiente de Serviço de Aplicativo][9]  

## <a name="getting-started"></a>Introdução
tooget iniciado com ambientes de serviço de aplicativo, consulte [como toocreate um ambiente de serviço de aplicativo](app-service-web-how-to-create-an-app-service-environment.md).

Para obter mais informações sobre a plataforma do serviço de aplicativo do Azure hello, consulte [do serviço de aplicativo do Azure](../app-service/app-service-value-prop-what-is.md).

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!--Image references-->
[1]: ./media/app-service-web-configure-an-app-service-environment/ase-icon.png
[2]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-aseblade.png
[3]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-poolchart.png
[4]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-properties.png
[5]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-poolblade.png
[6]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-scalecommand.png
[7]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-poolscale.png
[8]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-pricingtiers.png
[9]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-deletease.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[Appserviceplans]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[HowtoScale]: http://azure.microsoft.com/documentation/articles/app-service-web-scale-a-web-app-in-an-app-service-environment/
[ControlInbound]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[ExpressRoute]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/
[ILBASE]: http://azure.microsoft.com/documentation/articles/app-service-environment-with-internal-load-balancer/
