---
title: "etapas de criação de projeto Avançar malha aaaService | Microsoft Docs"
description: "Este artigo contém o conjunto de tooa de links de tarefas básicas de desenvolvimento para a malha do serviço"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 299d1f97-1ca9-440d-9f81-d1d0dd2bf4df
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: rwike77
ms.openlocfilehash: 45598bfabedf280fba8af449ef920f40b409a609
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="your-service-fabric-application-and-next-steps"></a>O seu aplicativo do Service Fabric e as próximas etapas
O seu aplicativo do Service Fabric do Azure foi criado. Este artigo descreve a composição de saudação do seu projeto e algumas das próximas etapas possíveis.

## <a name="your-application"></a>Seu aplicativo
Cada novo aplicativo inclui um projeto de aplicativo. Pode haver um ou dois projetos adicionais, dependendo do tipo de saudação do serviço escolhido.

### <a name="hello-application-project"></a>projeto de aplicativo Hello
projeto de aplicativo Hello consiste em:

* Um conjunto de serviços de toohello de referências que compõem seu aplicativo.
* Três publicar perfis (1-nó Local, 5-nó Local e nuvem) que você pode usar toomaintain preferências para trabalhar com diferentes ambientes – como ponto de extremidade de cluster de tooa relacionados preferências e se tooperform atualizar implantações por padrão.
* Três arquivos de parâmetro aplicativo (o mesmo que acima) que você pode usar configurações de aplicativo específico do ambiente toomaintain, como o número de saudação de toocreate de partições para um serviço.
* Um script de implantação que você pode usar toodeploy seu aplicativo de linha de comando hello ou como parte de um pipeline de implantação e a integração contínuo automatizado.
* manifesto de aplicativo Hello, que descreve o aplicativo hello. Você pode encontrar hello manifesto na pasta de ApplicationPackageRoot hello.

### <a name="stateless-service"></a>Serviço sem estado
Quando você adiciona um novo serviço sem monitoração de estado, o Visual Studio adiciona uma solução de tooyour de projeto de serviço que inclui um tipo que descendem do `StatelessService`. serviço de saudação incrementa uma variável local em um contador.

### <a name="stateful-service"></a>Serviço com estado
Quando você adiciona um novo serviço com monitoração de estado, o Visual Studio adiciona uma solução de tooyour de projeto de serviço que inclui um tipo que descendem do `StatefulService`. Olá, serviço incrementa um contador em seu `RunAsync` método e armazena o resultado da saudação em um `ReliableDictionary`.

### <a name="actor-service"></a>Serviço de ator
Quando você adiciona um novo ator confiável, o Visual Studio adiciona o Gerenciador de tooyour dois projetos: um projeto de ator e um projeto de interface.

projeto de ator Olá fornece métodos para a configuração e Obtendo o valor de saudação de um contador que é confiável persistente em estado de saudação do ator. Olá interface projeto fornece uma interface que outros serviços podem usar o ator de saudação tooinvoke.

### <a name="stateless-web-api"></a>API Web sem monitoração de estado
projeto de API da Web sem monitoração de estado Olá fornece básico que você pode usar tooopen seus clientes de tooexternal do aplicativo de serviço web. Para obter mais informações sobre como o projeto de saudação estruturado, consulte [serviços de API da Web do serviço do Fabric com OWIN auto-hospedagem](service-fabric-reliable-services-communication-webapi.md).


### <a name="aspnet-core"></a>Núcleo do ASP.NET
Olá SDK do Service Fabric fornece Olá mesmo conjunto de modelos do ASP.NET Core que estão disponíveis para projetos do ASP.NET Core de autônomo: vazio, [API da Web][aspnet-webapi], e [aplicativo Web][aspnet-webapp].

### <a name="guest-executables-and-guest-containers"></a>Executáveis de convidado e contêineres de convidado

Um serviço de malha 'Convidado' é um serviço que não é compilado com modelos de programação da plataforma hello. Você pode empacotar binários Olá para o convidado ou [diretamente no pacote de aplicativo hello](service-fabric-deploy-existing-app.md) ou [por meio de uma imagem de contêiner](service-fabric-deploy-container.md). Em ambos os casos, o Visual Studio cria Olá artefatos necessários no hello **ApplicationPackageRoot** pasta do projeto de aplicativo hello. Visual Studio não irá criar um novo projeto de serviço porque o código Olá já existe em outro lugar. Se você quiser toomanage seu convidado projetos junto com o projeto de aplicativo do Service Fabric hello, você pode adicioná-los toohello mesma solução do Visual Studio.

## <a name="next-steps"></a>Próximas etapas
### <a name="create-an-azure-cluster"></a>Criar um cluster do Azure
Olá SDK do Service Fabric fornece um cluster local para desenvolvimento e teste. toocreate um cluster no Azure, consulte [Configurando um cluster do Service Fabric do portal do Azure de saudação][create-cluster-in-portal].

### <a name="publish-your-application-tooazure"></a>Publicar seu aplicativo tooAzure
Você pode publicar seu aplicativo diretamente do Visual Studio tooan cluster do Azure. como fazer isso, consulte toolearn [publicar seu aplicativo tooAzure][publish-app-to-azure].

### <a name="use-service-fabric-explorer-toovisualize-your-cluster"></a>Usar o Gerenciador do Service Fabric toovisualize seu cluster
Service Fabric Explorer oferece uma maneira fácil toovisualize seu cluster, incluindo aplicativos implantados e layout físico. mais, consulte toolearn [visualizando o cluster usando o Gerenciador do Service Fabric][visualize-with-sfx].

### <a name="version-and-upgrade-your-services"></a>Versão e atualização de serviços
O Service Fabric permite controle de versão independente e atualização de serviços independentes em um aplicativo. mais, consulte toolearn [controle de versão e atualizar seus serviços][app-upgrade-tutorial].

### <a name="configure-continuous-integration-with-visual-studio-team-services"></a>Configurar a integração contínua com o Visual Studio Team Services
toolearn como você pode configurar um processo de integração contínua para seu aplicativo de malha do serviço, consulte [configurar a integração contínua com o Visual Studio Team Services][ci-with-vso].

<!-- Links -->
[add-web-frontend]: service-fabric-add-a-web-frontend.md
[create-cluster-in-portal]: service-fabric-cluster-creation-via-portal.md
[publish-app-to-azure]: service-fabric-publish-app-remote-cluster.md
[visualize-with-sfx]: service-fabric-visualizing-your-cluster.md
[ci-with-vso]: service-fabric-set-up-continuous-integration.md
[reliable-services-webapi]: service-fabric-reliable-services-communication-webapi.md
[app-upgrade-tutorial]: service-fabric-application-upgrade-tutorial.md
[aspnet-webapi]: https://docs.asp.net/en/latest/tutorials/first-web-api.html
[aspnet-webapp]: https://docs.asp.net/en/latest/tutorials/first-mvc-app/index.html
