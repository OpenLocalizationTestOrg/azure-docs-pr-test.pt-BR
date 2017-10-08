---
title: "registros de contêiner de Docker aaaPrivate no Azure | Microsoft Docs"
description: "Introdução toohello serviço de registro de contêiner do Azure, fornecendo os registros de Docker baseado em nuvem, gerenciados e privados."
services: container-registry
documentationcenter: 
author: stevelas
manager: balans
editor: dlepow
tags: 
keywords: 
ms.assetid: ee2b652b-fb7c-455b-8275-b8d4d08ffeb3
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/24/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f6edcf0bf947b7770ee0a4e4a5cfbf4ef8b7392a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooprivate-docker-container-registries"></a>Registros de contêiner de Docker de tooprivate de Introdução


Registro de contêiner do Azure é gerenciada [registro Docker](https://docs.docker.com/registry/) serviço baseado em Olá 2.0 do código-fonte aberto Docker do registro. Criar e manter toostore de registros do contêiner do Azure e gerenciar seu privada [contêiner Docker](https://www.docker.com/what-docker) imagens. Use registros de contêiner no Azure com o desenvolvimento de contêiner existente e os pipelines de implantação e desenhar no corpo de saudação de experiência de comunidade do Docker.

Para obter informações sobre o Docker e contêineres, confira:

* [Guia do usuário do Docker](https://docs.docker.com/engine/userguide/)




## <a name="use-cases"></a>Casos de uso
Extrair imagens de um contêiner do Azure destinos da implantação toovarious do registro:

* **Sistemas de orquestração escalonáveis** que gerenciam aplicativos em contêineres em clusters de hosts, incluindo [CD/SO](https://docs.mesosphere.com/), [Docker Swarm](https://docs.docker.com/swarm/) e [Kubernetes](http://kubernetes.io/docs/).
* **Serviços do Azure** que dão suporte à criação e execução de aplicativos em grande escala, incluindo [Serviço de Contêiner](../container-service/index.yml), [Serviço de Aplicativo](/app-service/index.md), [Lote](../batch/index.md), [Service Fabric](/azure/service-fabric/) e outros.

Os desenvolvedores também podem enviar por push tooa registro de contêiner como parte de um fluxo de trabalho de desenvolvimento do contêiner. Por exemplo, direcione uma ferramenta de implantação e integração contínua de destino como [Visual Studio Team Services](https://www.visualstudio.com/docs/overview) ou [Jenkins](https://jenkins.io/) a um Registro de contêiner.





## <a name="key-concepts"></a>Principais conceitos
* **Registro** - crie um ou mais registros de contêiner em sua assinatura do Azure. Cada registro é apoiado por um Azure padrão [conta de armazenamento](../storage/common/storage-introduction.md) em Olá mesmo local. Tirar proveito do armazenamento local, rede o fechamento das suas imagens de contêiner, criando um registro na Olá mesmo local do Azure que suas implantações. Um nome totalmente qualificado do registro tem o formato de saudação `myregistry.azurecr.io`.

  Você [controlar o acesso](container-registry-authentication.md) tooa registro de contêiner usando um backup do Azure Active Directory [entidade de serviço](../active-directory/active-directory-application-objects.md) ou uma conta de administrador fornecida. Saudação de execução padrão `docker login` tooauthenticate de comando com um registro.

* **Registro Gerenciado** - uma camada que oferece recursos adicionais para registros em três SKUs - Basic, Standard e Premium. imagens de saudação nessas SKUs são armazenadas nas contas de armazenamento gerenciado pelo Olá serviço registros de contêiner do Azure, o que melhora a confiabilidade e permite que os novos recursos. Os novos recursos incluem a integração de webhook, a autenticação de repositório com o Azure Active Directory e o suporte à funcionalidade de exclusão. Os usuários têm Olá opção toochoose entre registros gerenciados ou toocreate um registro apoiado por suas próprias contas de armazenamento ao criar registros.

* **Repositório** - um registro contém um ou mais repositórios, que são grupos de imagens de contêiner. O Registro de Contêiner do Azure dá suporte a namespaces do repositório de vários níveis. Esse recurso permite que você toogroup coleções de aplicativo específico de tooa relacionados de imagens, ou uma coleção de desenvolvimento de toospecific aplicativos ou equipes operacionais. Por exemplo:

  * `myregistry.azurecr.io/aspnetcore:1.0.1` representa uma imagem de toda a empresa
  * `myregistry.azurecr.io/warrantydept/dotnet-build`representa uma imagem usada toobuild .NET aplicativos, compartilhados entre o departamento de garantia Olá
  * `myregistry.azrecr.io/warrantydept/customersubmissions/web`representa uma imagem de web, agrupada no aplicativo de envios de cliente hello, Olá garantia departamento

* **Imagem** - armazenada em um repositório, cada imagem é um instantâneo somente leitura de um contêiner do Docker. Registros de contêiner do Azure podem incluir imagens do Windows e Linux. Você controla os nomes de imagem para todas as implantações de contêiner. Padrão de uso [comandos](https://docs.docker.com/engine/reference/commandline/) toopush imagens em um repositório, ou uma imagem de um repositório de pull.

* **Contêiner** - um contêiner define um aplicativo de software e suas dependências encapsuladas em um sistema de arquivos completo, incluindo código, tempo de execução, ferramentas do sistema e bibliotecas. Execute os contêineres do Docker com base nas imagens do Windows ou Linux que você obtém de um registro de contêiner. Contêineres em execução em um único computador compartilham o núcleo do sistema operacional hello. Contêineres do docker são totalmente portáteis tooall principais distribuições de Linux, Mac e Windows.




## <a name="next-steps"></a>Próximas etapas
* [Criar um registro de contêiner usando Olá portal do Azure](container-registry-get-started-portal.md)
* [Criar um registro de contêiner usando Olá CLI do Azure](container-registry-get-started-azure-cli.md)
* [Enviar por push sua primeira imagem usando Olá CLI do Docker](container-registry-get-started-docker-cli.md)
* toobuild uma integração contínua e fluxo de trabalho de implantação usando o Visual Studio Team Services, serviço de contêiner do Azure e registro de contêiner do Azure, consulte [este tutorial](../container-service/dcos-swarm/container-service-docker-swarm-setup-ci-cd.md).
* Se desejar tooset seu próprios Docker particular do registro no Azure (sem um ponto de extremidade público), consulte [implantar seu próprio privada Docker registro no Azure](../virtual-machines/virtual-machines-linux-docker-registry-in-blob-storage.md).
