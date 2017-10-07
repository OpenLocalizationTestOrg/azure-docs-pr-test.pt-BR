---
title: "aaaOverview de malha do serviço e contêineres | Microsoft Docs"
description: "Uma visão geral do serviço de malha e hello o uso de aplicativos de microsserviço toodeploy contêineres. Este artigo fornece uma visão geral de como contêineres podem ser usados e Olá recursos disponíveis no Service Fabric."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: c98b3fcb-c992-4dd9-b67d-2598a9bf8aab
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 5/16/2017
ms.author: msfussell
ms.openlocfilehash: fce94c4b476351c90f23f706aab8bc17319cce22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-and-containers"></a>Service Fabric e contêineres
> [!NOTE]
> Esse recurso está em versão prévia para Linux.  Implantar contêineres, não há suporte para cluster do Service Fabric tooa no Windows 10 ainda (em breve). 
>   

## <a name="introduction"></a>Introdução
O Azure Service Fabric é um [orquestrador](service-fabric-cluster-resource-manager-introduction.md) de serviços entre um cluster de computadores, com anos de uso e otimização em grande escala dos serviços da Microsoft. Os serviços podem ser desenvolvidos de várias maneiras de usar Olá [modelos de programação do Service Fabric](service-fabric-choose-framework.md) toodeploying [convidado executáveis](service-fabric-deploy-existing-app.md). Por padrão, o Service Fabric implanta e ativa esses serviços como processos. Processos fornecem ativação mais rápida hello e maior uso de densidade de recursos de saudação em um cluster. O Service Fabric também pode implantar serviços em imagens de contêiner. É importante, você pode combinar serviços em processos e serviços em contêineres Olá mesmo aplicativo. 

## <a name="containers-and-service-fabric-roadmap"></a>Mapa dos contêineres e do Service Fabric
Há vários aprimoramentos de orquestração de contêiner com o Service Fabric planejados para versões futuras. Entre eles estão recursos para aprimoramento de rede com suporte para redes virtuais dentro de um aplicativo, recursos de segurança, diagnóstico aprimorado e suporte para ferramentas. Serviço de malha permite que você toocreate aplicativos contêineres empacotados com o código existente (por exemplo, aplicativos de IIS MVC) a mistura de serviços desenvolvidos usando modelos de programação Olá Service Fabric.  Você pode executar vários aplicativos em um único cluster. 

## <a name="what-are-containers"></a>O que são contêineres?
Contêineres são encapsulados, implantadas individualmente componentes que são executados como instâncias isoladas em Olá mesmo kernel tootake aproveitar virtualização que fornece um sistema operacional. Portanto, cada aplicativo e suas bibliotecas de tempo de execução, dependências e sistema executar dentro de um contêiner com exibição de contêiner próprio isolada toohello acesso completo, privada construções do sistema operacional. Junto com a portabilidade, esse nível de isolamento de segurança e recursos é principal benefício Olá para usar contêineres com o Service Fabric, que executa os serviços nos processos caso contrário.

Contêineres são uma tecnologia de virtualização que virtualiza a saudação de sistema operacional subjacente de aplicativos. Contêineres fornecem um ambiente imutável para toorun de aplicativos com vários níveis de isolamento. Os contêineres executar diretamente sobre o kernel hello e tem uma visão isolada saudação do sistema de arquivos e outros recursos. As máquinas toovirtual comparados contêineres têm Olá vantagens a seguir:

* **Pequeno**: contêineres usam um único espaço e camada de versões e atualizações tooincrease eficiência de armazenamento.
* **Fast**: contêineres não têm tooboot um sistema operacional completo, para que possam começar muito mais rapidamente, normalmente em segundos.
* **Portabilidade**: uma imagem de aplicativo em contêineres pode ser toorun porta na nuvem hello, no local, dentro das máquinas virtuais ou diretamente nos computadores físicos.
* **Governança de recursos**: um contêiner pode limitar os recursos físicos Olá pode consumir em seu host.

## <a name="container-types"></a>Tipos de contêiner
Service Fabric dá suporte a contêineres do Linux e Windows e também dá suporte ao modo de isolamento de Hyper-V em Olá último. 

### <a name="docker-containers-on-linux"></a>Contêineres de Docker no Linux
Docker fornece toocreate APIs de alto nível e gerenciar contêineres sobre contêineres de kernel do Linux. Hub do docker é um repositório central toostore e recuperar imagens de contêiner.
Para obter um tutorial, consulte [implantar um contêiner de Docker tooService malha](service-fabric-get-started-containers-linux.md).

### <a name="windows-server-containers"></a>Contêineres do Windows Server
Windows Server 2016 fornece dois tipos diferentes de contêineres diferentes no nível de saudação do isolamento fornecido. Contêineres do Windows Server e do Docker são semelhantes pois ambos têm o namespace e o arquivo de sistema isolamento mas compartilhamento Olá kernel com host Olá em que estiverem sendo executados. No Linux, esse isolamento sempre foi fornecido por `cgroups` e `namespaces`, e os contêineres do Windows Server se comportam da mesma forma.

Contêineres do Hyper-V do Windows fornecem mais segurança e isolamento, porque cada contêiner não compartilham o núcleo do sistema operacional Olá outros contêineres ou com host hello. Com esse nível mais alto de isolamento de segurança, os contêineres do Hyper-V são indicados para cenários hostis e multilocatários.
Para obter um tutorial, consulte [implantar um tooService de contêiner do Windows Fabric](service-fabric-get-started-containers.md).

Olá seguinte figura mostra Olá tipos diferentes de níveis de isolamento e virtualização disponíveis no sistema operacional de saudação.
![Plataforma Service Fabric][Image1]

## <a name="scenarios-for-using-containers"></a>Cenários de uso de contêineres
Estes são exemplos típicos em que um contêiner é uma boa opção:

* **IIS comparar e deslocar**: se você tiver [ASP.NET MVC](https://www.asp.net/mvc) aplicativos que você deseja toocontinue toouse, coloque-o em um contêiner em vez de migrá-los tooASP.NET Core. Esses aplicativos ASP.NET MVC dependem do IIS (Serviços de Informações da Internet). Você pode empacotar esses aplicativos em imagens de contêiner de saudação pré-criados imagem do IIS e implantá-los com o Service Fabric. Consulte [imagens de contêiner no Windows Server](https://msdn.microsoft.com/virtualization/windowscontainers/quick_start/quick_start_images) para obter informações sobre como toocreate imagens do IIS.
* **Combinar contêineres e microsserviços do Service Fabric**: use uma imagem existente do contêiner para parte do seu aplicativo. Por exemplo, você pode usar o hello [contêiner NGINX](https://hub.docker.com/_/nginx/) para Olá web front-end de seus aplicativos e serviços com monitoração de estado para Olá computação mais intensiva de back-end.
* **Reduzir o impacto de serviços "vizinhos com ruídos"**: você pode usar a capacidade de governança de recursos Olá contêineres toorestrict Olá de recursos de que usa um serviço em um host. Se os serviços podem consumir muitos recursos e afetar o desempenho de saudação de terceiros (como uma operação demorada, semelhante a consulta), considere colocar esses serviços em contêineres com controle de recursos.

## <a name="service-fabric-support-for-containers"></a>Suporte ao Service Fabric para contêineres
Atualmente, o Service Fabric dá suporte à implantação de contêineres de Docker em contêineres do Linux e do Windows Server no Windows Server 2016, junto com o suporte para o modo de isolamento do Hyper-V. 

Em Olá Service Fabric [modelo de aplicativo](service-fabric-application-model.md), um contêiner representa um host de aplicativo no qual o serviço várias réplicas são colocadas. Malha do serviço pode executar qualquer contêiner, e o cenário de saudação é semelhante toohello [cenário executável de convidado](service-fabric-deploy-existing-app.md), onde você pode empacotar um aplicativo existente dentro de um contêiner. Este cenário é Olá-caso de uso comum para contêineres, e os exemplos incluem a execução de um aplicativo escrito usando qualquer linguagem ou estruturas, mas não usando internos modelos de programação do Service Fabric hello.

Além disso, você também pode executar os serviços do Service Fabric dentro de contêineres. Suporte para serviços de malha do serviço em execução dentro de contêineres é limitado no momento, mas toobe aprimorada em versões futuras.

* **Serviços sem estado confiáveis dentro de contêineres**: serviços confiável sem estado usando serviços confiáveis hello, só há suporte para modelos de programação no Linux. O suporte para os Reliable Services sem estado em contêineres do Windows será adicionado em uma versão futura.
* **Serviços com monitoração de estado dentro de contêineres**: esses serviços usam o modelo de programação Reliable Actors ou serviços confiáveis hello. O suporte para a execução de serviços com estado em contêineres será adicionado em uma versão futura.

O Service Fabric tem vários recursos de contêiner que ajudam a compilar de aplicativos compostos por microsserviços em contêineres. Saudação de ofertas do Service Fabric recursos de serviços em contêineres a seguir:

* Implantação e ativação de imagem de contêiner.
* Governança de recursos.
* Autenticação do repositório.
* Mapeamento de porta de toohost de porta do contêiner.
* Descoberta e comunicação de contêiner para contêiner.
* Capacidade tooconfigure e definir variáveis de ambiente.

## <a name="next-steps"></a>Próximas etapas
Neste artigo, você aprendeu sobre contêineres, que o Service Fabric é um orquestrador de contêiner e que o Service Fabric tem recursos que dão suporte a contêineres. Como uma próxima etapa, mostraremos sobre exemplos de cada Olá recursos tooshow você como toouse-los.

[Implantar um contêiner de Windows tooService malha no Windows Server 2016](service-fabric-get-started-containers.md)

[Implantar um contêiner de Docker tooService malha no Linux](service-fabric-get-started-containers-linux.md)

[Image1]: media/service-fabric-containers/Service-Fabric-Types-of-Isolation.png
