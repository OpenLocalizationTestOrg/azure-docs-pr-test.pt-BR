---
title: "Registros de contêiner do Docker privado no Azure | Microsoft Docs"
description: "Introdução ao serviço de Registro de Contêiner do Azure, fornecendo registros Docker privados gerenciados baseados em nuvem."
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
ms.openlocfilehash: fd0356286be46f99fd9ab8eabc53256103038407
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-private-docker-container-registries"></a>Introdução aos registros de contêiner do Docker privado


O Registro de Contêiner do Azure é um serviço gerenciado do [registro Docker](https://docs.docker.com/registry/) com base no Docker Registry 2.0 de fonte aberta. Criar e manter registros de contêiner do Azure para armazenar e gerenciar suas imagens privadas de [contêiner Docker](https://www.docker.com/what-docker). Use registros de contêiner no Azure com o desenvolvimento de contêiner e os pipelines de implantação existentes e tire proveito da experiência da comunidade do Docker.

Para obter informações sobre o Docker e contêineres, confira:

* [Guia do usuário do Docker](https://docs.docker.com/engine/userguide/)




## <a name="use-cases"></a>Casos de uso
Obtenha imagens de um registro de contêiner do Azure para vários destinos de implantação:

* **Sistemas de orquestração escalonáveis** que gerenciam aplicativos em contêineres em clusters de hosts, incluindo [CD/SO](https://docs.mesosphere.com/), [Docker Swarm](https://docs.docker.com/swarm/) e [Kubernetes](http://kubernetes.io/docs/).
* **Serviços do Azure** que dão suporte à criação e execução de aplicativos em grande escala, incluindo [Serviço de Contêiner](../container-service/index.yml), [Serviço de Aplicativo](/app-service/index.md), [Lote](../batch/index.md), [Service Fabric](/azure/service-fabric/) e outros.

Os desenvolvedores também podem enviar um registro de contêiner como parte de um fluxo de trabalho de desenvolvimento do contêiner. Por exemplo, direcione uma ferramenta de implantação e integração contínua de destino como [Visual Studio Team Services](https://www.visualstudio.com/docs/overview) ou [Jenkins](https://jenkins.io/) a um Registro de contêiner.





## <a name="key-concepts"></a>Principais conceitos
* **Registro** - crie um ou mais registros de contêiner em sua assinatura do Azure. Cada registro é apoiado por uma [conta de armazenamento](../storage/common/storage-introduction.md) padrão do Azure no mesmo local. Aproveite o armazenamento local e de rede fechada de suas imagens de contêiner criando um registro no mesmo local do Azure de suas implantações. Um nome de registro totalmente qualificado tem a forma `myregistry.azurecr.io`.

  Você [controla o acesso](container-registry-authentication.md) a um registro de contêiner usando uma [entidade de serviço](../active-directory/active-directory-application-objects.md) com suporte do Azure Active Directory ou uma conta de administrador fornecida. Execute o comando `docker login` padrão para se autenticar em um registro.

* **Registro Gerenciado** - uma camada que oferece recursos adicionais para registros em três SKUs - Basic, Standard e Premium. As imagens dessas SKUs são armazenadas nas Contas de Armazenamento gerenciadas pelo serviço de Registros de Contêiner do Azure, o que melhora a confiabilidade e habilita novos recursos. Os novos recursos incluem a integração de webhook, a autenticação de repositório com o Azure Active Directory e o suporte à funcionalidade de exclusão. Os usuários têm a opção de escolher entre registros gerenciados ou de criar um registro apoiado por suas próprias Contas do Armazenamento ao criar registros.

* **Repositório** - um registro contém um ou mais repositórios, que são grupos de imagens de contêiner. O Registro de Contêiner do Azure dá suporte a namespaces do repositório de vários níveis. Esse recurso permite que você agrupe coleções de imagens relacionadas a um aplicativo específico ou uma coleção de aplicativos para equipes de desenvolvimento ou operacionais específicas. Por exemplo:

  * `myregistry.azurecr.io/aspnetcore:1.0.1` representa uma imagem de toda a empresa
  * `myregistry.azurecr.io/warrantydept/dotnet-build` representa uma imagem usada para criar aplicativos .NET, compartilhados no departamento de garantia
  * `myregistry.azrecr.io/warrantydept/customersubmissions/web` representa uma imagem da Web, agrupada no aplicativo de envios do cliente, pertencente ao departamento de garantia

* **Imagem** - armazenada em um repositório, cada imagem é um instantâneo somente leitura de um contêiner do Docker. Registros de contêiner do Azure podem incluir imagens do Windows e Linux. Você controla os nomes de imagem para todas as implantações de contêiner. Use [comandos do Docker](https://docs.docker.com/engine/reference/commandline/) padrão para envio de imagens em um repositório ou extraia uma imagem de um repositório.

* **Contêiner** - um contêiner define um aplicativo de software e suas dependências encapsuladas em um sistema de arquivos completo, incluindo código, tempo de execução, ferramentas do sistema e bibliotecas. Execute os contêineres do Docker com base nas imagens do Windows ou Linux que você obtém de um registro de contêiner. Contêineres em execução em um único computador compartilham o kernel do sistema operacional. Contêineres Docker são totalmente portáteis para todas as principais distribuições Linux, Mac e Windows.




## <a name="next-steps"></a>Próximas etapas
* [Criar um registro de contêiner usando o portal do Azure](container-registry-get-started-portal.md)
* [Criar um registro de contêiner usando a CLI do Azure](container-registry-get-started-azure-cli.md)
* [Enviar por push sua primeira imagem usando a CLI do Docker](container-registry-get-started-docker-cli.md)
* Para criar um fluxo de trabalho de implantação e integração contínua usando o Visual Studio Team Services, o Serviço de Contêiner do Azure e Registro de Contêiner do Azure, veja [Este tutorial](../container-service/dcos-swarm/container-service-docker-swarm-setup-ci-cd.md).
* Se quiser configurar seu próprio Registro privado do Docker no Azure (sem um ponto de extremidade público), confira [Implantando seu próprio Registro privado do Docker no Azure](../virtual-machines/virtual-machines-linux-docker-registry-in-blob-storage.md).
