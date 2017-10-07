---
title: "aaaAzure comparação do serviço de aplicativo, máquinas virtuais, serviço de malha e serviços de nuvem | Microsoft Docs"
description: "Saiba como o toochoose entre o serviço de aplicativo do Azure, máquinas virtuais, Service Fabric e serviços de nuvem para hospedar aplicativos web."
services: app-service\web, virtual-machines, cloud-services
documentationcenter: 
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 7d346a23-532a-42a9-98a8-23b7286d32a8
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: overview
ms.date: 07/07/2016
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 7577332ed049df66178c7b2cd5c440a7f93a7865
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-virtual-machines-service-fabric-and-cloud-services-comparison"></a>Comparação de Serviço de Aplicativo, Máquinas Virtuais, Service Fabric e Serviços de Nuvem do Azure
## <a name="overview"></a>Visão geral
O Azure oferece várias maneiras de sites da web de toohost: [do serviço de aplicativo do Azure][Azure App Service], [máquinas virtuais][Virtual Machines], [Service Fabric ] [ Service Fabric], e [serviços de nuvem][Cloud Services]. Este artigo ajuda você a entender as opções de saudação e fazer a escolha certa Olá para seu aplicativo da web.

Serviço de aplicativo do Azure é a melhor opção Olá para a maioria dos aplicativos web. Implantação e gerenciamento são integradas à plataforma hello, sites podem dimensionar rapidamente toohandle altas cargas de tráfego e Gerenciador de tráfego e balanceamento de carga interna Olá fornecer alta disponibilidade. Você pode mover existente sites tooAzure do serviço de aplicativo facilmente com um [ferramenta de migração on-line](https://www.migratetoazure.net/), usar um aplicativo de código-fonte aberto da saudação Galeria de aplicativos Web, ou criar um novo site usando as ferramentas de sua escolha e hello. Olá [WebJobs] [ WebJobs] recurso torna fácil tooadd em segundo plano trabalho processamento tooyour aplicativo do serviço de aplicativo web.

Service Fabric é uma boa opção se você estiver criando um novo aplicativo ou reescrever em um aplicativo existente toouse uma arquitetura de microsserviço. Aplicativos, que são executados em um pool compartilhado de computadores, podem começar pequenos e crescer toomassive escala com centenas ou milhares de computadores, conforme necessário. Serviços com monitoração de estado torná-lo tooconsistently fácil e confiável armazenam o estado do aplicativo e do Service Fabric gerencia automaticamente o particionamento de serviço, dimensionamento e disponibilidade para você.  O Service Fabric também permite a API Web com OWIN (Open Web Interface for .NET) e ASP.NET Core.  TooApp em comparação com o serviço, o serviço de malha também fornece mais controle sobre ou acesso direto à infraestrutura subjacente hello. Você pode acessar remotamente seus servidores ou configurar as tarefas de inicialização do servidor. Serviços de nuvem é semelhante tooService malha no nível de controle em relação a facilidade de uso, mas agora é um serviço herdado e do Service Fabric é recomendado para novo desenvolvimento.

Se você tiver um aplicativo que exigiria toorun modificações significativas no serviço de aplicativo ou serviço de malha, você poderia escolher máquinas virtuais em ordem toosimplify migrando toohello nuvem. No entanto, configurar corretamente, proteger e manter as VMs requerem muito mais tempo e conhecimento de TI comparados tooAzure do serviço de aplicativo e serviço de malha. Se você estiver pensando em máquinas virtuais do Azure, certifique-se de levar em conta Olá manutenção contínua esforço necessário toopatch, atualizar e gerenciar seu ambiente de máquina virtual. Máquinas Virtuais do Azure são IaaS (Infraestrutura como serviço), enquanto o Serviço de Aplicativo e o Service Fabric são Paas (plataforma como serviço). 

## <a name="features"></a>Comparação de Recursos
Olá a tabela a seguir compara os recursos de saudação do serviço de aplicativo, serviços de nuvem, máquinas virtuais e Service Fabric toohelp que você faz melhor opção de saudação. Para obter informações atuais sobre hello SLA para cada opção, consulte [contratos de nível de serviço do Azure](https://azure.microsoft.com/support/legal/sla/).

| Recurso | Serviço de Aplicativo (aplicativos Web) | Serviços de nuvem (funções Web) | Máquinas Virtuais | Service Fabric | Observações |
| --- | --- | --- | --- | --- | --- |
| Implantação quase instantânea |X | | |X |Implantando um aplicativo ou uma atualização de aplicativo tooa serviço de nuvem, ou criar uma VM, leva vários minutos, pelo menos, Implantando um aplicativo de web do aplicativo tooa leva alguns segundos. |
| Expandir toolarger máquinas sem reimplantação |X | | |X | |
| Instâncias do servidor de Web compartilham conteúdo e configuração, o que significa que você não tem tooredeploy ou reconfigurar conforme você dimensionar. |X | | |X | |
| Vários ambientes de implantação (produção e preparo) |X |X | |X |Serviço de malha permite que você toohave vários ambientes para seus aplicativos ou toodeploy diferentes versões do seu aplicativo lado a lado. |
| Gerenciamento de atualização automática do sistema operacional |X |X | | |Atualizações automáticas do sistema operacional estão planejadas para uma futura versão do Service Fabric. |
| Alternância ininterrupta entre plataformas (alterne facilmente entre 32 bits e 64 bits) |X |X | | | |
| Implantar código com GIT, FTP |X | |X | | |
| Implantar o código com a implantação da Web |X | |X | |Serviços de nuvem suporta o uso de Olá Web Deploy toodeploy atualizações tooindividual de instâncias de função. No entanto, você não pode usá-lo para a implantação inicial de uma função, e se você usar a implantação da Web para uma atualização tiver toodeploy separadamente tooeach instância de uma função. Várias instâncias são necessários na ordem tooqualify para hello SLA do serviço de nuvem para ambientes de produção. |
| Suporte do WebMatrix |X | |X | | |
| Acesso tooservices barramento de serviço, armazenamento, banco de dados SQL |X |X |X |X | |
| Camada de serviços Web ou Web hospedada de uma arquitetura multicamada |X |X |X |X | |
| Camada intermediária de host de uma arquitetura multicamada |X |X |X |X |Aplicativos do serviço de aplicativo web podem facilmente hospedar uma camada intermediária da API REST e Olá [WebJobs](http://go.microsoft.com/fwlink/?linkid=390226) recurso pode hospedar os trabalhos de processamento em segundo plano. Você pode executar trabalhos Web em uma site dedicado tooachieve independente escalabilidade da camada de saudação. visualização de saudação [aplicativos de API](../app-service-api/app-service-api-apps-why-best-platform.md) recurso fornece ainda mais recursos para hospedar os serviços REST. |
| Suporte integrado do MySQL como serviço |X |X |X | |Serviços de nuvem podem integrar o MySQL como um serviço por meio de ofertas de ClearDB, mas não como parte do fluxo de trabalho do hello Portal do Azure. |
| Suporte para ASP.NET, classic ASP, Node.js, PHP, Python |X |X |X |X |Malha do serviço oferece suporte a criação de saudação de um front-end de web usando [ASP.NET 5](../service-fabric/service-fabric-add-a-web-frontend.md) ou você pode implantar qualquer tipo de aplicativo (Node. js, Java etc.) como um [executável de convidado](../service-fabric/service-fabric-deploy-existing-app.md). |
| Expansão toomultiple instâncias sem reimplantação |X |X |X |X |Máquinas virtuais pode expandir toomultiple instâncias, mas serviços Olá executando neles devem ser gravados toohandle nesse expansão. Você tooconfigure um solicitações de tooroute do balanceador de carga entre máquinas Olá e cria um grupo de afinidade tooprevent simultâneas reinicializações de todas as instâncias devido a falhas de hardware ou toomaintenance. |
| Suporte para SSL |X |X |X |X |Para aplicativos Web do Serviço de Aplicativo, o SSL para nomes de domínio personalizados só tem suporte no modo Básico e Padrão. Para obter informações sobre como usar o SSL com os aplicativos Web, consulte [Configurar um certificado SSL para um site do Azure](app-service-web-tutorial-custom-ssl.md). |
| Integração do Visual Studio |X |X |X |X | |
| Depuração Remota |X |X |X | | |
| Implantar código com TFS |X |X |X |X | |
| Isolamento de rede com a [Rede Virtual do Azure](/azure/virtual-network/) |X |X |X |X |Consulte também [Integração de Rede Virtual dos Websites do Azure](https://azure.microsoft.com/blog/2014/09/15/azure-websites-virtual-network-integration/) |
| Suporte a [Gerenciador de Tráfego do Azure](/azure/traffic-manager/) |X |X |X |X | |
| Monitoramento do ponto de extremidade integrado |X |X |X | | |
| Tooservers de acesso de área de trabalho remota | |X |X |X | |
| Instalação de qualquer MSI personalizado | |X |X |X |Serviço de malha permite que você toohost qualquer arquivo como um [executável de convidado](../service-fabric/service-fabric-deploy-existing-app.md) ou você pode instalar qualquer aplicativo em Olá VMs. |
| Tarefas de inicialização toodefine/executar da capacidade | |X |X |X | |
| Pode escutar eventos tooETW | |X |X |X | |

## <a name="scenarios"></a>Cenários e recomendações
Aqui estão alguns cenários comuns de aplicativo com as recomendações conforme toowhich opção de hospedagem web do Azure pode ser mais apropriada para cada um.

* [Preciso de um front-end da web com o processamento em segundo plano e aplicativos de negócios do banco de dados back-end toorun integrados com ativos locais.](#onprem)
* [Preciso de um toohost de maneira confiável acessar meu site corporativo que dimensiona bem e ofertas global.](#corp)
* [Tenho um aplicativo IIS6 em execução no Windows Server 2003.](#iis6)
* [Eu sou um proprietário de negócios de pequeno e preciso de uma maneira de baixo custo toohost meu site, mas com o crescimento futuro em mente.](#smallbusiness)
* [Tenho uma web ou um designer gráfico e desejo toodesign e criação de sites para meus clientes.](#designer)
* [Estou migrando meu aplicativo multicamado com um toohello de front-end da web nuvem.](#multitier)
* [Meu aplicativo depende do Windows altamente personalizados ou ambientes Linux e deseja toomove-toohello nuvem.](#custom)
* [Meu site usa software livre e desejo toohost-lo no Azure.](#oss)
* [Tenho um aplicativo de linha de negócios que precisa de rede corporativa do tooconnect toohello.](#lob)
* [Desejo toohost um serviço web ou API REST para clientes móveis.](#mobile)

### <a id="onprem"></a>Preciso de um front-end da web com o processamento em segundo plano e aplicativos de negócios do banco de dados back-end toorun integrados com ativos locais.
Os Serviço de Aplicativo do Azure é uma ótima solução para aplicativos de negócios complexos. Ele permite que você desenvolver aplicativos que dimensionar automaticamente em uma plataforma com balanceamento de carga, são protegidos com o Active Directory e se conectar a recursos de locais de tooyour. Ele torna esses aplicativos fácil por meio de um portal de alta qualidade e as APIs de gerenciamento e permite que você tenha uma compreensão toogain como os clientes estão usando-los com as ferramentas de análise do aplicativo. Olá [Webjobs] [ Webjobs] recurso permite que você execute processos em segundo plano e tarefas como parte de sua camada de web, enquanto a conectividade híbrida e recursos de rede virtual que oferece recursos de backup local tooon tooconnect fácil. O Serviço de Aplicativo do Azure fornece SLA três noves para aplicativos Web e permite que você:

* Execute seus aplicativos de maneira confiável em uma plataforma de nuvem de autorrecuperação e autocorreção.
* Escale automaticamente em uma rede global de datacenters.
* Faça backup e restaurações para recuperação de desastres.
* Esteja de acordo com os padrões ISO, SOC2 e PCI.
* Integre-se com o Active Directory

### <a id="corp"></a>Preciso de um toohost de maneira confiável acessar meu site corporativo que dimensiona bem e ofertas global.
O Serviço de Aplicativo do Azure é uma ótima solução para hospedar sites corporativos. Ele permite tooscale de aplicativos da web rapidamente e facilmente toomeet demanda em uma rede global de centros de dados. Ele oferece alcance local, tolerância a falhas e gerenciamento de tráfego inteligente. Tudo em uma plataforma que fornece ferramentas de gerenciamento de classe internacional, permitindo que você toogain aprofundado sobre a integridade do site e o tráfego do site rapidamente e facilmente. O Serviço de Aplicativo do Azure fornece SLA três noves para aplicativos Web e permite que você:

* Execute seus sites de maneira confiável em uma plataforma de nuvem de autorrecuperação e autocorreção.
* Escale automaticamente em uma rede global de datacenters.
* Faça backup e restaurações para recuperação de desastres.
* Gerencie logs e o tráfego com ferramentas integradas.
* Esteja de acordo com os padrões ISO, SOC2 e PCI.
* Integre-se com o Active Directory

### <a id="iis6"></a> Tenho um aplicativo IIS6 em execução no Windows Server 2003.
Serviço de aplicativo do Azure torna fácil tooavoid Olá os custos de infraestrutura associados ao migrar aplicativos IIS6 mais antigos. A Microsoft criou [ferramentas de migração fácil toouse e orientação de migração detalhado](https://www.movemetowebsites.net/) que permitem que você toocheck compatibilidade e identificar as alterações que precisam toobe feita. Integração com o Visual Studio, o TFS e ferramentas comuns de CMS torna fácil toodeploy IIS6 aplicativos diretamente toohello de nuvem. Uma vez implantado, Olá Portal do Azure fornece ferramentas de gerenciamento robusto que permitem que você tooscale toomanage custos e a demanda toomeet conforme necessário. Com a ferramenta de migração hello, você pode:

* Rapidamente e facilmente migre sua nuvem de toohello herdado do Windows Server 2003 web application.
* Aceite tooleave seu local no banco de dados SQL anexado toocreate um aplicativo híbrido.
* Mova automaticamente seu banco de dados SQL juntamente com o aplicativo legado.

### <a id="smallbusiness"></a>Eu sou um proprietário de negócios de pequeno e preciso de uma maneira de baixo custo toohost meu site, mas com o crescimento futuro em mente.
O Serviço de Aplicativo do Azure é uma ótima solução para esse cenário, pois você pode começar a usá-lo gratuitamente e, em seguida, adicionar mais recursos quando precisar. Cada aplicativo gratuito da web é fornecido com um domínio fornecido pelo Azure (*sua_empresa*. azurewebsites.net), e a plataforma de saudação inclui ferramentas de implantação e gerenciamento integradas, bem como uma galeria de aplicativos que tornam mais fácil tooget iniciado. Há muitos outros serviços e opções de escala que permitem Olá tooevolve de site com a demanda de aumento de usuário. Com o Serviço de Aplicativo do Azure, você pode:

* Começar com a camada gratuita hello e, em seguida, expandir conforme necessário.
* Use Olá Galeria de aplicativos tooquickly configurar aplicativos web populares, como o WordPress.
* Adicione adicionais do Azure serviços e recursos tooyour aplicativo conforme necessário.
* Proteja seu aplicativo web com HTTPS.

### <a id="designer"></a>Tenho uma web ou um designer gráfico e desejo toodesign e criação de sites para meus clientes
Para desenvolvedores da Web e Web designers, o Serviço de Aplicativo do Azure se integra facilmente com uma variedade de estruturas e ferramentas, inclui suporte à implantação para Git e FTP e oferece uma integração coesa com ferramentas e serviços como Visual Studio e Banco de dados SQL. Com o Serviço de Aplicativo, você pode:

* Use as ferramentas de linha de comando para [tarefas automatizadas][scripting].
* Trabalhe com linguagens populares como [.Net][dotnet], [PHP][PHP], [Node.js][nodejs] e [Python][Python].
* Selecione os três diferentes níveis de dimensionamento para expansão toovery alta capacidade.
* Integração com outros serviços do Azure, como [banco de dados SQL][sqldatabase], [Service Bus] [ servicebus] e [armazenamento] [ Storage], ou ofertas de saudação do parceiro [Azure Store][azurestore], como MySQL e MongoDB.
* Integração com ferramentas como o Visual Studio, Git, WebMatrix, WebDeploy, TFS e FTP.

### <a id="multitier"></a>Estou migrando meu aplicativo multicamado com um toohello de front-end da web nuvem
Se você estiver executando um aplicativo de várias camado, como um servidor web que conecta o banco de dados tooa, o serviço de aplicativo do Azure é uma boa opção que oferece integração total com o banco de dados do SQL Azure. E você pode usar o recurso de WebJobs Olá para executar processos de back-end.

Escolha o Service Fabric para um ou mais dos seus níveis se você precisar de mais controlam sobre o ambiente do servidor de saudação, como Olá tooremote de capacidade para o servidor ou configurar tarefas de inicialização do servidor.

Escolha máquinas virtuais para um ou mais dos seus níveis se você quiser toouse sua própria imagem de máquina ou execute o software de servidor ou serviços que você não pode configurar na malha do serviço.

### <a id="custom"></a>Meu aplicativo depende do Windows altamente personalizados ou ambientes Linux e deseja toomove-toohello nuvem.
Se seu aplicativo requer complexas de instalação ou configuração de software e saudação do sistema operacional, máquinas virtuais provavelmente é Olá melhor solução. Com Máquinas Virtuais, você pode:

* Use Olá toostart de galeria de máquina Virtual com um sistema operacional, como Windows ou Linux e, em seguida, personalizá-lo para seus requisitos de aplicativo.
* Criar e carregar uma imagem personalizada de um toorun de servidor de local existente em uma máquina virtual no Azure.

### <a id="oss"></a>Meu site usa software livre e desejo toohost-lo no Azure
Se a estrutura do código-fonte aberto tem suporte no serviço de aplicativo, idiomas hello e frameworks exigidos pelo seu aplicativo são configuradas automaticamente para você. O Serviço de Aplicativo permite que você:

* Use várias linguagens de software livre populares como [.NET][dotnet], [PHP][PHP], [Node.js][nodejs] e [Python][Python].
* Instale o WordPress, Drupal, Umbraco, DNN e muitos outros aplicativos Web de terceiros.
* Migrar um aplicativo existente ou crie um novo de saudação Galeria de aplicativos.

Se não há suporte para a estrutura do código-fonte aberto no serviço de aplicativo, você pode executá-lo em uma saudação outra opções de hospedagem de web do Azure. Com máquinas virtuais, você pode instalar e configurar o software de saudação na imagem de máquina hello, que pode ser Windows ou Linux.

### <a id="lob"></a>Tenho um aplicativo de linha de negócios que precisa de rede corporativa do tooconnect toohello
Se você quiser toocreate um aplicativo de linha de negócios, seu site pode exigir acesso direto tooservices ou dados na rede corporativa hello. Isso é possível no serviço de aplicativo do Service Fabric e máquinas virtuais usando Olá [serviço de rede Virtual do Azure](/azure/virtual-network/). No serviço de aplicativo, você pode usar o hello [recurso de integração da VNET](https://azure.microsoft.com/blog/2014/09/15/azure-websites-virtual-network-integration/), que permite que seus aplicativos do Azure toorun como se estivesse em sua rede corporativa.

### <a id="mobile"></a>Desejo toohost um serviço web ou API REST para clientes móveis
Serviços web baseados em HTTP permitem que você toosupport uma ampla variedade de clientes, incluindo clientes móveis. Estruturas, como ASP.NET Web API integram com o Visual Studio toomake-toocreate mais fácil e consumirem serviços REST.  Esses serviços são expostos de um ponto de extremidade da web, portanto, é possível toouse qualquer web técnica hospedagem no Azure toosupport neste cenário. No entanto, o Serviço de Aplicativo é uma ótima opção para hospedar APIs REST. Com o Serviço de Aplicativo, você pode:

* Criar rapidamente um [aplicativo móvel](../app-service-mobile/app-service-mobile-value-prop.md) ou [aplicativo de API](../app-service-api/app-service-api-apps-why-best-platform.md) toohost Olá HTTP web Services em um dos data centers globalmente distribuídos do Azure.
* Migrar serviços existentes ou criar novos.
* Obter o SLA de disponibilidade com uma única instância ou expansão máquinas toomultiple dedicado.
* Saudação de uso publicados tooprovide APIs REST tooany HTTP clientes do site, incluindo clientes móveis.

> [!NOTE]
> Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta, vá muito<a href="https://trywebsites.azurewebsites.net/">https://trywebsites.azurewebsites.net</a>, onde você pode imediatamente criar um aplicativo de início de curta duração no serviço de aplicativo do Azure gratuitamente. Nenhum cartão de crédito é exigido, sem compromissos.
> 
> 

## <a id="nextsteps"></a> Próximas etapas
Para obter mais informações sobre opções de hospedagem na web de saudação três, consulte [introduzindo Azure](../fundamentals-introduction-to-azure.md).

tooget iniciado com as opções de saudação escolhida para seu aplicativo, consulte Olá recursos a seguir:

* [Serviço de Aplicativo do Azure](/azure/app-service/)
* [Serviços de nuvem do Azure](/azure/cloud-services/)
* [Máquinas Virtuais do Azure](/azure/virtual-machines/)
* [Service Fabric](/azure/service-fabric/)

<!-- URL List -->

[Azure App Service]: /azure/app-service/
[Cloud Services]: /azure/cloud-services/
[Virtual Machines]: /azure/virtual-machines/
[Service Fabric]: /azure/service-fabric/
[ClearDB]: http://www.cleardb.com/
[WebJobs]: http://go.microsoft.com/fwlink/?linkid=390226&clcid=0x409
[Configuring an SSL certificate for an Azure Website]: app-service-web-tutorial-custom-ssl.md
[azurestore]: https://azuremarketplace.microsoft.com/en-us/marketplace/apps
[scripting]: https://azure.microsoft.com/documentation/scripts/?services=web-sites
[dotnet]: https://azure.microsoft.com/develop/net/
[nodejs]: https://azure.microsoft.com/develop/nodejs/
[PHP]: https://azure.microsoft.com/develop/php/
[Python]: https://azure.microsoft.com/develop/python/
[servicebus]: /azure/service-bus/
[sqldatabase]: /azure/sql-database/
[Storage]: /azure/storage/

<!-- IMG List -->

[ChoicesDiagram]: ./media/choose-web-site-cloud-service-vm/Websites_CloudServices_VMs_3.png
