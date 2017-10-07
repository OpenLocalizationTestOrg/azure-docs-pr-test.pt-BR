---
title: "Guia de aaaGet de Introdução para desenvolvedores no Azure | Microsoft Docs"
description: "Este tópico fornece informações essenciais para os desenvolvedores tooget iniciado usando a plataforma do Microsoft Azure Olá para suas necessidades de desenvolvimento."
services: 
cloud: 
documentationcenter: 
author: ggailey777
manager: erikre
ms.assetid: 
ms.service: na
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: glenga
ms.openlocfilehash: 72dc2678db7738923d4bc7783e297fea6fcded83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-guide-for-azure-developers"></a>Guia de introdução para desenvolvedores do Azure

## <a name="what-is-azure"></a>O que é o Azure?

O Azure é uma plataforma completa de nuvem que pode hospedar seus aplicativos existentes, simplificar o desenvolvimento de saudação de novos aplicativos e até mesmo aprimorar aplicativos locais. Azure integra-se de que você precisa toodevelop de serviços de nuvem hello, testar, implantar e gerenciar seus aplicativos — aproveitando as vantagens de eficiência de saudação da nuvem de computação.

Ao hospedar seus aplicativos no Azure, você pode começar por algo pequeno e facilmente escalar seu aplicativo à medida que aumenta a demanda do cliente. O Azure também oferece confiabilidade de saudação que é necessário para aplicativos de alta disponibilidade, incluindo até failover entre diferentes regiões. Olá [portal do Azure](https://portal.azure.com) permite que você gerencie facilmente todos os serviços do Azure. Além disso, também é possível gerenciar seus serviços programaticamente, utilizando modelos e APIs e específicos do serviço.

**Quem deve ler este**: este guia é toohello uma introdução a plataforma Windows Azure para desenvolvedores de aplicativos. Ele fornece orientação e direção que você precisa toostart criar novos aplicativos no Azure ou migrando tooAzure aplicativos existentes.

## <a name="where-do-i-start"></a>Por onde começo?

Com todos os serviços do hello Azure oferece, pode ser um toofigure tarefa intimidadora quais serviços você precisa toosupport sua arquitetura de solução. Saudação de destaques essa seção do Azure services que os desenvolvedores geralmente usam. Para obter uma lista de todos os serviços do Azure, consulte Olá [documentação do Azure](../../index.md).

Primeiro, você deve decidir sobre como toohost seu aplicativo no Azure. Você precisa toomanage toda a infraestrutura como uma máquina virtual (VM). Você pode usar os recursos de gerenciamento de plataforma Olá que o Azure fornece? Talvez você tenha somente a execução de código um framework sem servidor toohost?

Seu aplicativo precisa de armazenamento em nuvem para qual o Azure oferece várias opções. Você pode usufruir da autenticação empresarial do Azure. Além disso, há ferramentas para monitoramento e desenvolvimento baseado em nuvem e a maioria dos serviços de hospedagem oferece integração DevOps.

Agora, vamos examinar alguns serviços específicos de saudação que recomendamos investigando para seus aplicativos.

### <a name="application-hosting"></a>Hospedagem de aplicativos

O Azure fornece várias toorun de ofertas de computação em nuvem seu aplicativo para que você não tenha tooworry sobre detalhes de infraestrutura de saudação. Você pode facilmente escalar verticalmente ou escalar horizontalmente seus recursos à medida que o uso do aplicativo aumenta.

O Azure oferece serviços que dão suporte ao desenvolvimento de aplicativos e necessidades de hospedagem. O Azure fornece a infraestrutura-como-um-serviço (IaaS) toogive você total controle sobre seu aplicativo de hospedagem. As ofertas de plataforma como serviço (PaaS) do Azure fornecem Olá totalmente gerenciado serviços necessários toopower seus aplicativos. Há hospedagem sem servidor mesmo true no Azure em que você só precisa toodo é escrever seu código.

![Opções de hospedagem de aplicativo do Azure](./media/azure-developer-guide/azure-developer-hosting-options.png)


#### <a name="azure-app-service"></a>Serviço de aplicativo do Azure 

Olá toopublish de caminho mais rápido seus projetos baseados na web, considere a possibilidade do serviço de aplicativo do Azure. Serviço de aplicativo torna fácil tooextend sua web toosupport aplicativos clientes móveis e publicar APIs de REST facilmente consumido. Essa plataforma fornece autenticação utilizando provedores sociais, dimensionamento automático baseado em tráfego, teste em produção e implantações baseadas em contêiner e contínuas.

Quando você cria um aplicativo no serviço de aplicativo, selecione um dos seguintes tipos de saudação:

- [Aplicativos Web](../../app-service-web/app-service-web-overview.md):   permite hospedar sites e aplicativos Web escritos em .NET, Java, PHP, Node.js e Python.

- [Aplicativos móveis](../../app-service-mobile/app-service-mobile-value-prop.md): acesso de toosupport estende os aplicativos Web de dispositivos móveis. Permite autenticação com provedores sociais e Azure AD (Azure Active Directory), fornece armazenamento de back-end e integra com [Hubs de Notificação do Azure](../../notification-hubs/notification-hubs-push-notification-overview.md) para notificações por push.

- [Aplicativos de API](../../app-service-api/app-service-api-apps-why-best-platform.md): permite que você mais expor com segurança suas APIs na nuvem Olá com os metadados do Swagger para que os clientes podem consumi-los facilmente.

Porque o compartilhamento de todos os tipos de aplicativo de três Olá tempo de execução do serviço de aplicativo, você pode hospedar um site, suporte para clientes móveis e expor suas APIs no Azure, tudo a partir de Olá mesmo projeto ou solução. toolearn mais sobre o serviço de aplicativo, consulte [como funciona o serviço de aplicativo](../../app-service/app-service-how-works-readme.md).

O Serviço de Aplicativo foi projetado com o DevOps em mente. Ele dá suporte a várias ferramentas para implantações de integração contínua e publicações, incluindo GitHub (webhooks), Jenkins, Visual Studio Team Services, TeamCity e outros.

Você pode migrar seu tooApp de aplicativos serviço existente usando Olá [ferramenta de migração on-line](https://www.migratetoazure.net/).

>**Quando toouse**: usar o serviço de aplicativo quando você estiver migrando tooAzure de aplicativos web existentes, e quando você precisa de uma plataforma de hospedagem totalmente gerenciada para seus aplicativos web. Você também pode usar o serviço de aplicativo quando você precisa de clientes móveis toosupport ou expor APIs REST com seu aplicativo.

>**Introdução**: serviço de aplicativo torna fácil toocreate e implantar seu primeiro [aplicativo web](../../app-service-web/web-sites-dotnet-get-started.md), [aplicativo móvel](../../app-service-mobile/app-service-mobile-ios-get-started.md), ou [aplicativo de API](../../app-service-api/app-service-api-dotnet-get-started.md).

>**Experimente agora**: serviço de aplicativo permite que você fornecer uma plataforma de saudação do aplicativo de curta duração tootry sem ter que toosign uma conta do Azure. Tente plataforma hello e [criar seu aplicativo de serviço de aplicativo do Azure](https://tryappservice.azure.com/).

#### <a name="azure-virtual-machines"></a>Máquinas Virtuais do Azure

Como um provedor de infraestrutura-como-um-serviço (IaaS), o Azure permite que você implante tooor migrar tooeither seu aplicativo Windows ou Linux VMs. Junto com a rede Virtual do Azure, máquinas virtuais do Azure oferece suporte à implantação de saudação do Windows ou Linux VMs tooAzure. Com máquinas virtuais, você tem controle total sobre a configuração da máquina Olá Olá. Ao utilizar VMs, você será responsável por toda a instalação de software para servidores, configuração, manutenção e patches do sistema operacional.

Devido ao nível de saudação do controle que você tiver VMs, você pode executar uma ampla variedade de cargas de trabalho de servidor no Azure que não se ajustam em um modelo de PaaS. Essas cargas de trabalho incluem servidores de banco de dados, Windows Server Active Directory e Microsoft SharePoint. Para obter mais informações, consulte a documentação de máquinas virtuais de saudação para um [Linux](/azure/virtual-machines/linux/) ou [Windows](/azure/virtual-machines/windows/).

>**Quando toouse**: máquinas virtuais de uso quando você quiser total controle sobre seu aplicativo infraestrutura ou toomigrate local aplicativo cargas de trabalho tooAzure sem a necessidade de alterações toomake.

>**Introdução**: criar um [VM Linux](../../virtual-machines/virtual-machines-linux-quick-create-portal.md) ou [VM do Windows](../../virtual-machines/virtual-machines-windows-hero-tutorial.md) de saudação portal do Azure.

#### <a name="azure-functions-serverless"></a>Azure Functions (sem servidor)

Em vez de se preocupar sobre criando e gerenciando um toorun de infraestrutura de aplicativo ou hello todo seu código. E se você apenas pode escrever seu código e que ele seja executado em resposta tooevents ou em um agendamento?  [As funções do Azure](../../azure-functions/functions-overview.md) é um "sem servidor"-estilo de oferta que permite que você escrever apenas Olá código necessário. Com o Azure Functions, a execução do código é disparada por solicitações HTTP, webhooks, eventos de serviço de nuvem ou em um agendamento. É possível codificar em sua linguagem de desenvolvimento de preferência, como C\#, F\#, Node.js, Python ou PHP. Com cobrança com base no consumo, você pague somente pelo tempo de saudação que seu código é executado, e o Azure é dimensionado conforme necessário.

>**Quando toouse**: Use funções do Azure quando você tiver um código que é disparado por outros serviços do Azure, por eventos baseado na web ou em uma agenda. Você também pode usar funções quando você não precisa Olá sobrecarga de um projeto hospedado concluído ou quando você deseja apenas toopay para tempo de saudação que seu código seja executado. mais, consulte toolearn [visão geral de funções do Azure](../../azure-functions/functions-overview.md).

>**Introdução**: siga o tutorial de início rápido de funções hello muito[criar sua primeira função](../../azure-functions/functions-create-first-azure-function.md) do portal de saudação.

>**Experimente agora**: funções do Azure permite executar seu código sem ter que toosign uma conta do Azure. Experimente agora em e [crie sua primeira função do Azure](https://tryappservice.azure.com/).

#### <a name="azure-service-fabric"></a>Azure Service Fabric

Malha do serviço do Azure é uma plataforma de sistemas distribuídos que torna mais fácil toobuild, empacotar, implantar e gerenciar microservices escalonável e confiável. Ele também fornece recursos abrangentes de gerenciamento de aplicativos para provisionamento, implantação, monitoramento, atualização/aplicação de patch e exclusão de aplicativos implantados. Aplicativos, que são executados em um pool compartilhado de computadores, podem começar pequenos e dimensionar toohundreds ou milhares de computadores, conforme necessário.

O Service Fabric dá suporte para WebAPI com Open Web Interface para .NET (OWIN) e ASP.NET Core. Ele fornece SDKs para a construção de serviços no Linux em tanto em .NET Core como Java. toolearn mais sobre o serviço de malha, consulte Olá [Service Fabric aprendizado](https://azure.microsoft.com/documentation/learning-paths/service-fabric/).

>**Quando toouse:** Service Fabric é uma boa opção quando estiver criando um aplicativo ou reconfiguração de um toouse de aplicativo existente uma arquitetura de microsserviço. Use o Service Fabric quando precisar de mais controle sobre ou acesso direto à infraestrutura subjacente hello.

>**Introdução:** [Criar seu primeiro aplicativo Azure Service Fabric](../../service-fabric/service-fabric-create-your-first-application-in-visual-studio.md).

### <a name="enhance-your-applications-with-azure-services"></a>Aprimore seus aplicativos com os serviços do Azure

Além disso, tooapplication de hospedagem, o Azure fornece ofertas de serviço que podem melhorar a funcionalidade hello, desenvolvimento e manutenção de seus aplicativos em nuvem hello e local.

#### <a name="hosted-storage-and-data-access"></a>Armazenamento hospedado e acesso a dados

A maioria dos aplicativos deve armazenar dados, portanto, independentemente de como você decidir toohost seu aplicativo no Azure, considere a possibilidade de um ou mais dos Olá serviços de armazenamento e os dados a seguir.

-   **Banco de dados do SQL Azure**: versão com base em um Azure Olá Microsoft mecanismo do SQL Server para armazenar dados de tabela relacionais na nuvem hello. O Banco de Dados SQL fornece desempenho previsível, escalabilidade sem tempo de inatividade, continuidade dos negócios e proteção de dados.

    >**Quando toouse**: quando o aplicativo requer o armazenamento de dados com integridade referencial, suporte transacional e suporte para consultas TSQL.

    >**Introdução**: [criar um banco de dados SQL em minutos usando o portal do Azure de saudação](../../sql-database/sql-database-get-started.md).

-   **Armazenamento do Azure**: oferece armazenamento durável e altamente disponível para blobs, filas, arquivos e outros tipos de dados não relacionais. Armazenamento fornece a base de armazenamento de saudação para máquinas virtuais.

    >**Quando toouse**: quando o seu aplicativo armazena dados relacionais, como pares chave-valor (tabelas), blobs, compartilhamentos de arquivos ou mensagens (filas).

    >**Introdução**: Escolher entre um desses tipos de armazenamento: [blobs](../../storage/blobs/storage-dotnet-how-to-use-blobs.md), [tabelas](../../cosmos-db/table-storage-how-to-use-dotnet.md),     [filas](../../storage/queues/storage-dotnet-how-to-use-queues.md) ou [arquivos](../../storage/files/storage-dotnet-how-to-use-files.md).

-   **Azure DocumentDB**: um serviço do banco de dados NoSQL totalmente gerenciado e escalonável que possui consultas SQL sobre dados de objeto. É possível acessar o DocumentDB utilizando drivers do MongoDB existentes.
    >**Quando toouse:** quando seu aplicativo precisa de consultas SQL toobe tooexecute capaz em documentos JSON, ou se você estiver usando o MongoDB.

    >**Introdução**: [Compilar um aplicativo de console DocumentDB C#](../../documentdb/documentdb-get-started.md). Se você for um desenvolvedor do MongoDB, consulte [Suporte de protocolo DocumentDB para MongoDB](../../documentdb/documentdb-protocol-mongodb.md).

Você pode usar [do Azure Data Factory](../../data-factory/data-factory-introduction.md) toomove locais existentes tooAzure de dados. Se você não estiver pronto toomove dados na nuvem toohello, [conexões híbridas](../../biztalk-services/integration-hybrid-connection-overview.md) no permite que os serviços do BizTalk que você se conectar a seu serviço de aplicativo hospedado recursos tooon local do aplicativo. Você também pode conectar os serviços de dados e armazenamento tooAzure de aplicativos local.

#### <a name="docker-support"></a>Suporte ao Docker

Os contêineres do Docker, uma forma de virtualização de SO, permitem implantar aplicativos de forma mais eficiente e previsível. Um aplicativo em contêineres funciona em Olá de produção mesmo maneira em seus sistemas de desenvolvimento e teste. É possível gerenciar contêineres utilizando ferramentas do Docker padrão. Você pode usar suas habilidades existentes e toodeploy ferramentas de código aberto popular e gerenciar aplicativos de contêiner no Azure.

O Azure fornece várias maneiras toouse contêineres em seus aplicativos.

-   **Extensão de VM Docker do Azure**: permite que você configure sua VM com tooact de ferramentas do Docker como um host Docker.

    >**Quando toouse**: toogenerate implantações de contêiner consistente para seus aplicativos em uma máquina virtual, ou quando você quiser toouse [Docker Compose](https://docs.docker.com/compose/overview/).

    >**Introdução**: [criar um ambiente de Docker no Azure usando a extensão de VM Docker Olá](../../virtual-machines/virtual-machines-linux-dockerextension.md).

-   **Serviço de contêiner do Azure**: permite que você cria, configura e gerencia um cluster de máquinas virtuais que são pré-configurados toorun em contêineres de aplicativos. toolearn mais sobre o serviço de contêiner, consulte [introdução do serviço de contêiner do Azure](../../container-service/container-service-intro.md).

    >**Quando toouse**: quando você precisar toobuild ambientes de pronto para produção e escalonável que fornece ferramentas adicionais de planejamento e gerenciamento, ou quando você estiver implantando um cluster de Docker Swarm.

    >**Introdução**: [Implantar um cluster de Serviço de Contêiner](../../container-service/dcos-swarm/container-service-deployment.md).

-   **Máquina do Docker**: permite instalar e gerenciar um Mecanismo de Docker em hosts virtuais utilizando comandos docker-machine.

    >**Quando toouse**: quando você precisar protótipo tooquickly um aplicativo por meio da criação de um único host do Docker.

-   **Imagem de Docker personalizada para Serviço de Aplicativo**: permite utilizar contêineres do Docker de um registro de contêiner ou um contêiner de cliente ao implantar um aplicativo Web no Linux.

    >**Quando toouse**: ao implantar um aplicativo web na imagem do Linux tooa Docker.

    >**Introdução**: [Utilizar uma imagem de Docker personalizada para Serviço de Aplicativo no Linux](../../app-service-web/app-service-linux-using-custom-docker-image.md).

### <a name="authentication"></a>Autenticação

É crucial toonot apenas saber quem está usando seus aplicativos, mas também tooyour tooprevent não autorizado acessem os recursos. O Azure fornece tooauthenticate de várias maneiras de seus clientes de aplicativo.

-   **Azure Active Directory (AD do Azure)**: Olá multilocatário, baseados em nuvem de identidade e acesso de serviço de gerenciamento Microsoft. Você pode adicionar o logon único em aplicativos de tooyour (SSO) com a integração com o AD do Azure. Você pode acessar as propriedades de diretório usando hello Azure AD Graph API diretamente ou hello Microsoft Graph API. Você pode integrar com o suporte do AD do Azure para estrutura de autorização do OAuth 2.0 hello e abrir conexão de ID usando pontos de extremidade HTTP/REST nativo e Olá bibliotecas de autenticação multiplatform AD do Azure.

    >**Quando toouse**: tooprovide uma experiência de SSO, trabalhar com dados do gráfico, ou autenticar usuários com base em domínio.

    >**Introdução**: toolearn mais, consulte Olá [guia do desenvolvedor do Active Directory do Azure](../../active-directory/active-directory-developers-guide.md).

-   **Autenticação do serviço de aplicativo**: quando você escolhe toohost do serviço de aplicativo em seu aplicativo, você também pode obter suporte interno a autenticação do AD do Azure, juntamente com os provedores de identidade de redes sociais, incluindo o Facebook, Google, Microsoft e Twitter.

    >**Quando toouse**: quando você deseja que a autenticação tooenable em um aplicativo de serviço de aplicativo usando o AD do Azure, os provedores de identidade de redes sociais, ou ambos.

    >**Introdução**: toolearn mais sobre a autenticação no serviço de aplicativo, consulte [autenticação e autorização no serviço de aplicativo do Azure](../../app-service/app-service-authentication-overview.md).

toolearn mais sobre práticas recomendadas de segurança no Azure, consulte [padrões e práticas recomendadas de segurança do Azure](../../security/security-best-practices-and-patterns.md).

### <a name="monitoring"></a>Monitoramento

Com o aplicativo em funcionamento no Azure, você precisa toobe toomonitor capaz de desempenho, detectar problemas e ver como os clientes estão usando o seu aplicativo. O Azure fornece várias opções de monitoramento.

-   **Visual Studio Application Insights**: serviço hospedado no Azure uma análise extensível que se integra ao Visual Studio toomonitor seus aplicativos web dinâmicos. Ele fornece dados Olá necessários toocontinuously melhorar o desempenho de saudação e usabilidade de seus aplicativos, se estiver hospedados no Azure ou não.

    >**Introdução**: siga Olá [tutorial do Application Insights](../../application-insights/app-insights-overview.md).

-   **Monitor do Azure**: um serviço que ajuda você a toovisualize, consulta, rota, arquivamento e atuar em métricas de saudação e logs gerados pela sua infraestrutura do Azure e recursos. Monitor fornece exibições de dados Olá que você vê no hello portal do Azure e é uma única fonte para monitorar os recursos do Azure.
 
    >**Introdução**: [Introdução ao Azure Monitor](../../monitoring-and-diagnostics/monitoring-get-started.md).

### <a name="devops-integration"></a>Integração de DevOps

Se ele é provisionamento de máquinas virtuais ou publicar seus aplicativos web com a integração contínua, Azure integra-se com a maioria das ferramentas de DevOps populares hello. Com suporte para ferramentas como Jenkins, GitHub, Puppet, Chef, TeamCity, Ansible, VSTS e outros, você pode trabalhar com as ferramentas de saudação que você já tiver e maximizar a sua experiência já existente.

>**Experimente agora:** [experimentar várias integrações do DevOps Olá](https://azure.microsoft.com/try/devops/).

>**Introdução**: toosee DevOps opções para um aplicativo de serviço de aplicativo, consulte [tooAzure implantação contínua do serviço de aplicativo](../../app-service-web/app-service-continuous-deployment.md).


## <a name="azure-regions"></a>Regiões do Azure

O Azure é uma plataforma de nuvem global que está disponível em muitas regiões em torno de Olá, mundo. Ao provisionar um serviço, aplicativo ou máquina virtual no Azure, você é solicitado tooselect uma região que representa um datacenter específico onde seu aplicativo é executado ou onde os dados estão armazenados. Essas regiões correspondem toospecific locais, que são publicadas em Olá [regiões do Azure](https://azure.microsoft.com/regions/) página.

### <a name="choose-hello-best-region-for-your-application-and-data"></a>Escolha a região melhor Olá para seus aplicativos e dados

Um dos benefícios de saudação do uso do Azure é que você pode implantar seus data centers toovarious de aplicativos em todo o mundo de saudação. região Olá escolhido pode afetar o desempenho de saudação do seu aplicativo. Por exemplo, é melhor toochoose uma região toomost mais próximo de sua latência tooreduce de clientes em solicitações de rede. Você também poderá tooselect requisitos legais de saudação do toomeet sua região para distribuir seu aplicativo em determinados países. Ele é sempre um melhor prática toostore aplicativo de dados no hello mesmo datacenter ou em um datacenter, como próximo como possíveis toohello datacenter que está hospedando o seu aplicativo.

### <a name="multi-region-apps"></a>Aplicativos de várias regiões

Embora seja improvável, não é possível para um toogo datacenter inteiro offline devido a um evento como um desastre natural ou uma falha de Internet. É uma melhor aplicativos de negócios essenciais de toohost de prática em mais de um datacenter tooprovide máximo de disponibilidade. Utilizar várias regiões também pode reduzir a latência para usuários globais e oferecer oportunidades adicionais de flexibilidade ao atualizar aplicativos.

Alguns serviços, como a máquina Virtual e serviços de aplicativos, usam [Azure Traffic Manager](../../traffic-manager/traffic-manager-overview.md) tooenable suporte a várias regiões com failover entre os aplicativos de alta disponibilidade enterprise toosupport regiões. Por exemplo, consulte [Arquitetura de referência do Azure: aplicativo Web com alta disponibilidade](../../guidance/guidance-web-apps-multi-region.md).

>**Quando toouse**: quando você tem aplicativos corporativos e de alta disponibilidade que se beneficiam da replicação e failover.

## <a name="how-do-i-manage-my-applications-and-projects"></a>Como fazer para gerenciar meus aplicativos e projetos?

Azure fornece um rico conjunto de experiências para você toocreate e gerenciar recursos do Azure, aplicativos e projetos — programaticamente e Olá [portal do Azure](https://portal.azure.com/).

### <a name="command-line-interfaces-and-powershell"></a>Interfaces de linha de comando e PowerShell

Azure fornece toomanage de duas maneiras seus aplicativos e serviços da linha de comando hello usando Bash, Terminal, Olá prompt de comando ou a ferramenta de linha de comando de escolha. Normalmente, você pode executar Olá mesmo tarefas da linha de comando hello como Olá portal do Azure — como criar e configurar máquinas virtuais, redes virtuais, aplicativos web e outros serviços.

-   [Interface de linha de comando (CLI) do Azure](../../xplat-cli-install.md): permite que você se conectar tooan assinatura do Azure e várias tarefas com base nos recursos do Azure da linha de comando de saudação do programa.

-   [O Azure PowerShell](../../powershell-install-configure.md): fornece um conjunto de módulos com os cmdlets que permitem que você toomanage Azure recursos usando o Windows PowerShell.

### <a name="azure-portal"></a>Portal do Azure

Olá portal do Azure é um aplicativo baseado na web que você pode usar toocreate, gerenciar e remover os serviços e recursos do Azure. Olá portal do Azure está localizado em <https://portal.azure.com>. Ele inclui um painel personalizável, ferramentas para gerenciar recursos do Azure e acesso toosubscription configurações e informações de cobrança. Para obter mais informações, consulte Olá [visão geral do portal do Azure](../../azure-portal-overview.md).

### <a name="rest-apis"></a>APIs REST

Azure baseia-se em um conjunto de APIs de REST que dão suporte a saudação da interface do usuário do portal do Azure. A maioria dessas APIs REST também são toolet com suporte, você provisionar e gerenciar seus recursos do Azure e os aplicativos de qualquer dispositivo conectado à Internet por meio de programação. Para o conjunto completo de saudação de documentação da API REST, consulte Olá [referência do SDK do Azure REST](https://docs.microsoft.com/rest/api/).

### <a name="apis"></a>APIs

Além disso tooREST APIs, muitos serviços do Azure também permitem gerenciar programaticamente os recursos de aplicativos usando SDKs do Azure específica de plataforma, incluindo SDKs para Olá plataformas de desenvolvimento a seguir:

-   [.NET](https://go.microsoft.com/fwlink/?linkid=834925)
-   [Node.js](http://azure.github.io/azure-sdk-for-node/)
-   [Java](https://docs.microsoft.com/java/api/)
-   [PHP](https://github.com/Azure/azure-sdk-for-php/blob/master/README.md)
-   [Python](http://azure-sdk-for-python.readthedocs.io/en/latest/)
-   [Ruby](https://github.com/Azure/azure-sdk-for-ruby/blob/master/README.md)

Serviços como [aplicativos móveis](../../app-service-mobile/app-service-mobile-dotnet-how-to-use-client-library.md) e [Azure Media Services](../../media-services/media-services-dotnet-how-to-use.md) fornecer toolet de SDKs do lado do cliente acessar serviços da web e aplicativos cliente móveis.

### <a name="azure-resource-manager"></a>Gerenciador de Recursos do Azure 
    
Executar seu aplicativo no Azure provavelmente envolve trabalhar com vários serviços do Azure, todos de Olá que seguem a mesma duração do ciclo e pode ser pensada como uma unidade lógica. Por exemplo, um aplicativo Web pode utilizar Aplicativos Web, Banco de Dados SQL, Armazenamento, Cache Redis do Azure e serviços de Rede de Distribuição de Conteúdo do Microsoft Azure. [Gerenciador de recursos do Azure](../../azure-resource-manager/resource-group-overview.md) permite que você trabalhe com recursos de saudação em seu aplicativo como um grupo. Você pode implantar, atualizar ou excluir todos os recursos de saudação em uma única operação coordenado.

Além do toologically agrupar e gerenciar recursos relacionados, Gerenciador de recursos do Azure inclui recursos de implantação que permitem personalizar a implantação de saudação e a configuração de recursos relacionados. Por exemplo, utilizando o Resource Manager é possível implantar e configurar um aplicativo que consiste em máquinas virtuais múltiplas, um balanceador de carga e um Banco de Dados SQL do Azure como uma unidade única.

Essas implantações são desenvolvidas utilizando um modelo do Azure Resource Manager, que é um documento no formato JSON. Os modelos permitem que você defina uma implantação e gerencie seus aplicativos utilizando modelos declarativos, em vez de scripts. Seus modelos podem funcionar para diferentes ambientes, como teste, de preparo e produção. Por exemplo, usando modelos, você pode adicionar um botão tooa do repositório GitHub que implanta o código de saudação no conjunto de tooa Olá repositório de serviços do Azure com um único clique.

>**Quando toouse**: Use o Gerenciador de recursos de modelos quando desejar que uma implantação de modelo para o aplicativo que você pode gerenciar programaticamente por meio de APIs REST, Olá CLI do Azure e o Azure PowerShell.

>**Introdução**: tooget começou a usar modelos, consulte [modelos de autoria do Azure Resource Manager](../../resource-group-authoring-templates.md).

## <a name="understanding-accounts-subscriptions-and-billing"></a>Compreendendo contas, assinaturas e cobrança

Como os desenvolvedores, apreciamos toodive diretamente no código de saudação e tente tooget iniciada mais rápido possível, fazendo com que os aplicativos executados. Queremos certamente tooencourage toostart trabalhando no Azure tão facilmente quanto possível. toohelp tornar fácil, o Azure oferece uma [avaliação gratuita](https://azure.microsoft.com/free/). Alguns serviços até tem uma funcionalidade "Experimente gratuitamente", como [do serviço de aplicativo do Azure](https://tryappservice.azure.com/), que não exige muito até mesmo criar uma conta. Como fun como é toodive em codificação e implantando tooAzure seu aplicativo, também é importante tootake alguns toounderstand tempo como o Azure funciona do ponto de vista de contas de usuário, assinaturas e cobrança.

### <a name="what-is-an-azure-account"></a>O que é uma conta do Azure?

toocreate capaz de toobe ou trabalhar com uma assinatura do Azure, você deve ter uma conta do Azure. Uma conta do Azure é simplesmente uma identidade no Azure AD ou em um diretório, como uma organização corporativa ou de estudante, que é confiável pelo Azure AD. Se você não pertence toosuch uma organização, você sempre pode criar uma assinatura usando sua Account da Microsoft, que é confiável pelo AD do Azure. toolearn mais sobre como integrar o local no Windows Server Active Directory com o AD do Azure, consulte [integrando suas identidades locais ao Active Directory do Azure](../../active-directory/active-directory-aadconnect.md).

Cada assinatura do Azure tem uma relação de confiança com uma instância do Azure AD. Isso significa que ele confia esse diretório tooauthenticate usuários, serviços e dispositivos. Várias assinaturas podem confiar Olá mesmo diretório, mas uma assinatura confia em apenas um diretório. mais, consulte toolearn [assinaturas do Azure como estão associadas com o Azure Active Directory](../../active-directory/active-directory-how-subscriptions-associated-directory.md).

Além disso toodefining identidades de conta do Azure individuais, também chamado *usuários*, você também pode definir *grupos* no AD do Azure. Criar grupos de usuários é tooresources de acesso de toomanage uma boa maneira de uma assinatura usando o controle de acesso baseado em função (RBAC). toolearn como toocreate grupos, consulte [criar um grupo no modo de visualização do Azure Active Directory](../../active-directory/active-directory-groups-create-azure-portal.md). Também é possível criar e gerenciar grupos [utilizando o PowerShell](../../active-directory/active-directory-accessmanagement-groups-settings-v2-cmdlets.md).

### <a name="manage-your-subscriptions"></a>Gerencie suas assinaturas

Uma assinatura é uma unidade lógica de serviços do Azure que é vinculado tooan conta do Azure. Cada conta associada possui uma função em uma assinatura. A cobrança dos serviços do Azure é feita por assinatura. Para obter uma lista de ofertas de assinatura disponíveis Olá por tipo, consulte [detalhes da oferta do Microsoft Azure](https://azure.microsoft.com/support/legal/offer-details/).

#### <a name="administrator-roles"></a>Funções de administrador

Uma assinatura do Azure possui várias funções de administrador da conta que podem ser atribuídas a qualquer momento.

-   **Conta de administrador**: essa função tem controle total sobre a assinatura de saudação e é Olá conta responsável para cobrança.

-   **Administrador de serviço**: essa função tem controle sobre todos os serviços de saudação na assinatura de saudação. Por padrão, isso é hello mesma conta como Olá administrador da conta.

-   **Coadministrador**: essa função tem Olá mesmo acessar como Olá administrador de serviço, exceto que ele não pode alterar a associação de saudação do hello assinatura tooan directory do Azure.

toolearn mais sobre as funções de administrador, consulte [como tooadd ou alterar funções de administrador do Azure](../../billing/billing-add-change-azure-subscription-administrator.md#add-an-admin-for-a-subscription).

#### <a name="resource-groups"></a>Grupos de recursos

Ao fornecer novos serviços do Azure, isso é feito em uma determinada assinatura. Serviços individuais do Azure, que também são chamadas de recursos, são criados no contexto de saudação de um grupo de recursos. Grupos de recursos tornam mais fácil toodeploy e gerenciar recursos de seu aplicativo. Um grupo de recursos deve conter todos os recursos de saudação para seu aplicativo que você deseja toowork com como uma unidade. Você pode mover recursos entre grupos de recursos e até mesmo toodifferent assinaturas. toolearn sobre como mover recursos, consulte [Mover grupo de recursos toonew de recursos ou assinatura](../../resource-group-move-resources.md).

Olá Gerenciador de recursos do Azure é uma excelente ferramenta para visualizar os recursos de saudação que você já tenha criado em sua assinatura. mais, consulte toolearn [tooview do Gerenciador de recursos do uso do Azure e modificar recursos](../../resource-manager-resource-explorer.md).

#### <a name="grant-access-tooresources"></a>Conceder acesso tooresources

Quando você permitir acesso a recursos tooAzure, sempre é uma prática recomendada para fornecer aos usuários Olá menos privilégios tooperform necessário que uma determinada tarefa.

-   **Controle de acesso baseado em função (RBAC)**: no Azure, você pode conceder acesso a contas de toouser (entidades) em um escopo especificado: assinatura, o grupo de recursos ou recursos individuais. RBAC permite implantar um conjunto de recursos em um grupo de recursos e conceder permissões tooa usuário ou grupo específico. Ele também permite limitar acesso tooonly Olá recursos que pertencem a toohello grupo de recursos de destino. Você também pode conceder acesso tooa único recurso, como uma máquina virtual ou a rede virtual. acesso de toogrant, você atribuir um usuário de toohello de função, grupo ou entidade de serviço. Há muitas funções predefinidas, no entanto, você também pode definir suas próprias funções personalizadas.

    >**Quando toouse**: quando precisar de gerenciamento de acesso refinado para usuários e grupos.

    >**Introdução**: toolearn mais, consulte [Introdução ao gerenciamento de acesso no portal do Azure de saudação](../../active-directory/role-based-access-control-what-is.md).

-   **Objetos de entidade de serviço**: além tooproviding acessar toouser entidades e grupos, você pode conceder Olá mesma entidade de serviço tooa de acesso.

    > **Quando toouse**: quando você estiver gerenciando recursos do Azure ou conceder acesso para aplicativos por meio de programação. Para obter mais informações, consulte [Criar suplicação do Active Directory e entidade de serviço](../../resource-group-create-service-principal-portal.md).

#### <a name="tags"></a>Marcas

Gerenciador de recursos do Azure permite atribuir marcas personalizadas tooindividual recursos. Marcas, que são pares chave-valor, podem ser útil quando você precisa de recursos de tooorganize para cobrança ou de monitoramento. Marcas fornecem recursos de tootrack uma maneira em vários grupos de recursos. Você pode atribuir marcas no portal de hello, no modelo do Azure Resource Manager hello, ou programaticamente, usando Olá API REST, Olá CLI do Azure ou o PowerShell. Você pode atribuir várias marcas tooeach recursos. mais, consulte toolearn [usando marcas tooorganize seus recursos do Azure](../../resource-group-using-tags.md).

### <a name="billing"></a>Cobrança

No hello movimento de serviços hospedados toocloud de computação local, rastreamento e a estimativa do uso do serviço e os custos relacionados são problemas significativos. É tooestimate capazes de importantes toobe quais novos recursos custos toorun mensalmente. Você também precisa toobe tooproject capaz de aparência para um determinado mês com base nos gastos atual do hello cobrança hello.

#### <a name="get-resource-usage-data"></a>Obter dados de uso do recurso

O Azure fornece um conjunto de APIs REST de cobrança que dão acesso tooresource consumo e informações de metadados para as assinaturas do Azure. Esses oferecem APIs cobrança Olá toobetter capacidade prever e gerenciar os custos do Azure. É possível acompanhar e analisar os gastos em incrementos por hora, criar alertas de gastos e prever a cobrança futura com base nas tendências de uso atuais.

>**Introdução**: toolearn mais sobre como usar o hello APIs de cobrança, consulte [visão geral do uso de cobrança do Azure e APIs RateCard](../../billing-usage-rate-card-overview.md).

#### <a name="predict-future-costs"></a>Prever os custos futuros

Embora os custos de tooestimate antecipadamente é muito difícil, o Azure tem um [Calculadora de preços](https://azure.microsoft.com/pricing/calculator/) que você pode usar ao estimar o custo de saudação de recursos implantados. Você também pode usar a folha de cobrança Olá no portal de saudação e Olá APIs de REST de cobrança tooestimate futuras custos, com base no consumo atual.

>**Introdução**: Consulte [Visão geral de APIs de uso e RateCard de cobrança do Azure](../../billing-usage-rate-card-overview.md).

#### <a name="set-up-billing-alerts"></a>Configurar alertas de cobrança

Depois que você implantou o seu aplicativo ou solução no Azure, você pode criar alertas que envie um que e-mail quando abordar Olá os limites são definidos no alerta de saudação de gastos.

>**Introdução**: toolearn mais, consulte [configurar alertas para suas assinaturas do Microsoft Azure de cobrança](../../billing-set-up-alerts.md).
