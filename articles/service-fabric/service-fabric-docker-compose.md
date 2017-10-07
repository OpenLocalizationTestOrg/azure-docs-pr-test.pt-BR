---
title: "aaaAzure compor visualização do Service Fabric Docker"
description: "Malha do Azure do serviço aceita Docker compor formato toomake-lo mais fácil contêineres existentes tooorchestrate usando o Service Fabric. No momento, esse suporte está na versão prévia."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: a60d1321fd6ef07b241a98c5ab2b8dfe5d441b53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="docker-compose-application-support-in-azure-service-fabric-preview"></a>Suporte ao aplicativo Docker Compose no Azure Service Fabric (Versão prévia)

Docker usa Olá [docker compose.yml](https://docs.docker.com/compose) arquivo para definir o contêiner de vários aplicativos. toomake-fácil para os clientes familiarizados com o Docker tooorchestrate contêiner aplicativos existentes no Azure Service Fabric, incluímos suporte para compor Docker visualização nativamente na plataforma de saudação. O Service Fabric pode aceitar a versão 3 e posteriores de arquivos `docker-compose.yml`. 

Como esse suporte está na versão prévia, há suporte para apenas um subconjunto de diretivas do Compose. Por exemplo, não há suporte para atualizações de aplicativo. No entanto, você sempre pode remover e implantar aplicativos em vez de atualizá-los.

toouse visualizar, criar o cluster com a versão 5.7 ou superior do tempo de execução do Service Fabric Olá por meio de saudação portal do Azure junto com hello correspondente SDK. 

> [!NOTE]
> Esse recurso está na versão prévia e não tem suporte.

## <a name="deploy-a-docker-compose-file-on-service-fabric"></a>Implantar um arquivo do Docker Compose no Service Fabric

Olá, comandos a seguir criam um aplicativo de malha do serviço (denominado `fabric:/TestContainerApp` em Olá anterior exemplo), que você pode monitorar e gerenciar como qualquer outro aplicativo de malha do serviço. Você pode usar o nome do aplicativo especificado Olá para consultas de integridade.

### <a name="use-powershell"></a>Usar o PowerShell

Crie um aplicativo de serviço compor de malha de um arquivo de docker compose.yml executando Olá comando do PowerShell a seguir:

```powershell
New-ServiceFabricComposeApplication -ApplicationName fabric:/TestContainerApp -Compose docker-compose.yml [-RegistryUserName <>] [-RegistryPassword <>] [-PasswordEncrypted]
```

`RegistryUserName`e `RegistryPassword` consulte toohello contêiner do registro username e password. Depois que você tiver concluído o aplicativo hello, você pode verificar seu status usando Olá comando a seguir:

```powershell
Get-ServiceFabricComposeApplicationStatus -ApplicationName fabric:/TestContainerApp -GetAllPages
```

toodelete Olá compor aplicativos por meio do PowerShell, use Olá comando a seguir:

```powershell
Remove-ServiceFabricComposeApplication  -ApplicationName fabric:/TestContainerApp
```

### <a name="use-azure-service-fabric-cli-sfctl"></a>Usar a CLI do Azure Service Fabric (sfctl)

Como alternativa, você pode usar o hello CLI de malha do serviço de comando a seguir:

```azurecli
sfctl compose create --application-id fabric:/TestContainerApp --compose-file docker-compose.yml [ [ --repo-user --repo-pass --encrypted ] | [ --repo-user ] ] [ --timeout ]
```

Depois que você criou um aplicativo hello, você pode verificar seu status usando Olá comando a seguir:

```azurecli
sfctl compose status --application-id TestContainerApp [ --timeout ]
```

Olá toodelete compor aplicativos, use Olá comando a seguir:

```azurecli
sfctl compose remove  --application-id TestContainerApp [ --timeout ]
```

## <a name="supported-compose-directives"></a>Diretivas do Compose com suporte

Esta visualização dá suporte a um subconjunto das opções de configuração de saudação do formato de versão 3 redigir hello, incluindo Olá primitivos a seguir:

* Serviços > Implantar > Réplicas
* Serviços > Implantar > Posicionamento > Restrições
* Serviços > Implantar > Recursos > Limites
    * -cpu-shares
    * -memory
    * -memory-swap
* Serviços > Comandos
* Serviços > Ambiente
* Serviços > Portas
* Serviços > Imagem
* Serviços > Isolamento (somente para Windows)
* Serviços > Registro em log > Driver
* Serviços > Registro em log > Driver > Opções
* Volume e Implantar > Volume

Configurar o cluster Olá para impor limites de recurso, conforme descrito em [governança de recursos de malha do serviço](service-fabric-resource-governance.md). Todas as outras diretivas do Docker Compose não têm suporte nessa versão prévia.

## <a name="servicednsname-computation"></a>Computação de ServiceDnsName

Se o nome do serviço Olá que você especificar em um arquivo de composição é um nome de domínio totalmente qualificado (ou seja, ele contém um ponto [.]), nome DNS Olá registrado pelo Service Fabric é `<ServiceName>` (incluindo ponto Olá). Caso contrário, cada segmento de caminho no nome do aplicativo hello se torna um rótulo de domínio no nome DNS do serviço hello, com hello primeiro segmento de caminho se torne o rótulo de domínio de nível superior de saudação.

Por exemplo, se Olá especificado o nome do aplicativo é `fabric:/SampleApp/MyComposeApp`, `<ServiceName>.MyComposeApp.SampleApp` seria Olá nome DNS registrado.

## <a name="differences-between-compose-instance-definition-and-service-fabric-application-model-type-definition"></a>Diferenças entre o modelo de aplicativo do Compose (definição de instância) e do Service Fabric (definição de tipo)

Um arquivo docker-compose.yml descreve um conjunto de contêineres implantável, incluindo suas propriedades e configurações.
Por exemplo, o arquivo hello pode conter variáveis de ambiente e portas. Você também pode especificar parâmetros de implantação, como restrições de posicionamento, limites de recursos e nomes DNS, no arquivo de docker compose.yml hello.

Olá [o modelo de aplicativo do Service Fabric](service-fabric-application-model.md) usa tipos de serviço e aplicativo, onde você pode ter muitas instâncias de aplicativo do hello mesmo tipo. Por exemplo, você pode ter uma instância de aplicativo por cliente. Esse modelo baseado em tipo oferece suporte a várias versões do hello mesmo tipo de aplicativo que está registrado com o tempo de execução de saudação.

Por exemplo, o cliente pode ter um aplicativo instanciado com tipo 1.0 de AppTypeA e cliente B pode ter outro aplicativo instanciado com hello mesmo tipo e versão. Definir tipos de aplicativo hello nos manifestos de aplicativo hello e você especificar parâmetros de nome e a implantação de aplicativo hello quando você cria o aplicativo hello.

Embora esse modelo oferece flexibilidade, também planejamos toosupport um modelo de implantação mais simples, com base em instância onde os tipos são implícita do arquivo de manifesto hello. Nesse modelo, cada aplicativo obtém seu próprio manifesto independente. Estamos fazendo a versão prévia desse esforço adicionando suporte para o docker-compose.yml, que é um formato de implantação baseado em instância.

## <a name="next-steps"></a>Próximas etapas

* Leia sobre Olá [modelo de aplicativo do Service Fabric](service-fabric-application-model.md)
* [Introdução à CLI do Service Fabric](service-fabric-cli.md)
