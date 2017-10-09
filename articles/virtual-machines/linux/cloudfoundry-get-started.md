---
title: aaaGetting iniciado com Foundry de nuvem no Microsoft Azure | Microsoft Docs
description: Executar OSS ou Pivotal Cloud Foundry no Microsoft Azure
services: virtual-machines-linux
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 2a15ffbf-9f86-41e4-b75b-eb44c1a2a7ab
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 01/19/2017
ms.author: seanmck
ms.openlocfilehash: 56300d5a0a75b5a9f46145a49ed3f5daa774375a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-foundry-on-azure"></a>Cloud Foundry no Azure

O Cloud Foundry é um PaaS (plataforma como serviço) de software livre para criação, implantação e operação de aplicativos de 12 fatores desenvolvidos em várias linguagens e estruturas. Este documento descreve as opções de saudação que tem execução Foundry de nuvem no Azure e como você pode começar.

## <a name="cloud-foundry-offerings"></a>Ofertas do Cloud Foundry

Há duas formas de toorun de nuvem Foundry disponível no Azure: nuvem Foundry (OSS CF) de código-fonte aberto e Foundry essencial de nuvem (PCF). Sistemas operacionais CF é um inteiramente [código-fonte aberto](https://github.com/cloudfoundry) versão de nuvem Foundry gerenciados pelo Olá nuvem Foundry Foundation. Essencial Foundry de nuvem é uma distribuição corporativos de nuvem Foundry da Central Software Inc. Vamos examinar algumas das diferenças de saudação entre duas ofertas de saudação.

### <a name="open-source-cloud-foundry"></a>Cloud Foundry de software livre

Você pode implantar sistemas operacionais Foundry de nuvem no Azure pelo primeiro implantar um diretor BOSH e, em seguida, implantar Foundry de nuvem, usando Olá [instruções fornecidas no GitHub](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/blob/master/docs/guidance.md). toolearn mais sobre como usar CF OSS, consulte Olá [documentação](https://docs.cloudfoundry.org/) fornecida pelo Olá nuvem Foundry Foundation.

A Microsoft fornece suporte de melhor esforço para sistemas operacionais CF por meio de saudação canais comunitários a seguir:

- #<a name="bosh-azure-cpi-channel-on-cloud-foundry-slackhttpsslackcloudfoundryorg"></a>canal bosh-azure-cpi no [Cloud Foundry Slack](https://slack.cloudfoundry.org/)
- [lista de endereçamento cf-bosh](https://lists.cloudfoundry.org/pipermail/cf-bosh)
- Problemas do GitHub para Olá [IDC](https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/issues) e [do service broker](https://github.com/Azure/meta-azure-service-broker/issues)

>[!NOTE]
> nível de saudação de suporte para os recursos do Azure, como onde você executa Foundry de nuvem, máquinas virtuais do hello baseia-se no seu contrato de suporte do Azure. Suporte da comunidade de melhor esforço só se aplica a componentes toohello Foundry específicas da nuvem.

### <a name="pivotal-cloud-foundry"></a>Pivotal Cloud Foundry

Essencial Foundry de nuvem inclui Olá mesma plataforma principal como distribuição Olá OSS, juntamente com um conjunto de ferramentas de gerenciamento proprietário e suporte empresarial. toorun PCF no Azure, você deve adquirir uma licença de Pivotal. a oferta PCF Olá de saudação do Azure marketplace inclui uma licença de avaliação de 90 dias.

Olá ferramentas incluem [essencial Operations Manager](http://docs.pivotal.io/pivotalcf/customizing/), um aplicativo web que simplifica a implantação e gerenciamento de uma base de nuvem Foundry, e [essencial Gerenciador de aplicativos](https://docs.pivotal.io/pivotalcf/console/), um aplicativo web para gerenciamento os usuários e aplicativos.

Além disso toohello canais de suporte listados para sistemas operacionais CF acima, uma licença PCF permite que você toocontact Pivotal para obter suporte. Microsoft e Pivotal também tem habilitado fluxos de trabalho de suporte que permitem que você toocontact ambas as partes para obter assistência e têm sua consulta adequadamente roteada dependendo de onde está o problema de saudação.

## <a name="azure-service-broker"></a>Azure Service Broker

Nuvem Foundry incentiva Olá ["aplicativo de fator de doze"](https://12factor.net/) metodologia, que promove uma separação limpa de processos de aplicativos sem monitoração de estado e fazendo services com monitoração de estado. [Os agentes de serviço](https://docs.cloudfoundry.org/services/api.html) oferecem uma tooprovision de maneira consistente e associar tooapplications de serviços de backup. Olá [agente de serviços do Azure](https://github.com/Azure/meta-azure-service-broker) fornece algumas Olá principais serviços do Azure por meio desse canal, incluindo o armazenamento do Azure e SQL Azure.

Se você estiver usando Foundry essencial de nuvem, Olá service broker é também [disponível como um bloco](https://docs.pivotal.io/azure-sb/installing.html) de saudação rede central.

## <a name="related-resources"></a>Recursos relacionados

### <a name="visual-studio-team-services-plugin"></a>Plug-in do Visual Studio Team Services

Nuvem Foundry é adequado tooagile desenvolvimento de software, incluindo o uso de saudação de integração contínua (CI) e fornecimento contínuo (CD). Se você usa o Visual Studio Team Services (VSTS) toomanage seus projetos e deseja tooset backup de um pipeline de CI/CD direcionamento Foundry de nuvem, você poderá usar o hello [VSTS nuvem Foundry compilar extensão](https://marketplace.visualstudio.com/items?itemName=ms-vsts.cloud-foundry-build-extension). Olá plug-in torna tooconfigure simple e automatizar implantações tooCloud Foundry, quer em execução no Azure ou em outro ambiente.

## <a name="next-steps"></a>Próximas etapas

- [Implantar Foundry essencial de nuvem de saudação do Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/partners/pivotal/pivotal-cloud-foundryazure-pcf/)
- [Implantar um aplicativo tooCloud Foundry no Azure](./cloudfoundry-deploy-your-first-app.md)
