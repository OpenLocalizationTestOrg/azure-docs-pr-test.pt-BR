---
title: "Atualização de aplicativos: serialização de dados | Microsoft Docs"
description: "Práticas recomendadas para a serialização de dados e como ela afeta as atualizações de aplicativo sem interrupção."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: a5f36366-a2ab-4ae3-bb08-bc2f9533bc5a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 1b65dfd3813423550631490640a81953864f58e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-data-serialization-affects-an-application-upgrade"></a>Como a serialização de dados afeta a atualização de um aplicativo
Em um [atualização de aplicativo móvel](service-fabric-application-upgrade.md), atualização de saudação é aplicado tooa subconjunto de nós, um domínio de atualização por vez. Durante esse processo, alguns domínios de atualização estão na versão mais recente de saudação do seu aplicativo, e alguns domínios de atualização estão na versão mais antiga de saudação do seu aplicativo. Durante a distribuição de Olá Olá nova versão do seu aplicativo deve ser capaz de tooread Olá antigo dos seus dados e versão antiga de saudação do seu aplicativo deve ser capaz de tooread Olá nova versão dos dados. Se o formato de dados Olá não for frente e para trás atualização Olá compatível, podem falhar, ou pior, dados pode ser perdido ou corrompido. Este artigo discute o que constitui o formato de dados e oferece as práticas recomendadas para garantir que seus dados sejam compatíveis de uma versão para outra.

## <a name="what-makes-up-your-data-format"></a>O que compõe o seu formato de dados?
No Azure Service Fabric, dados de saudação que são persistidos e replicados vêm de suas classes c#. Para aplicativos que usam [coleções confiável](service-fabric-reliable-services-reliable-collections.md), que dados são objetos de saudação em dicionários confiável hello e filas. Para aplicativos que usam [Reliable Actors](service-fabric-reliable-actors-introduction.md), que é Olá fazendo o estado de ator hello. Essas classes c# devem ser serializáveis toobe persistida e replicada. Portanto, o formato de dados de saudação é definido pelos campos de saudação e propriedades que são serializadas, bem como eles são serializados. Por exemplo, em um `IReliableDictionary<int, MyClass>` dados saudação são um serializado `int` e um serializado `MyClass`.

### <a name="code-changes-that-result-in-a-data-format-change"></a>Alterações de código que resultam em uma alteração no formato dos dados
Desde que o formato de dados de saudação é determinado pelas classes c#, as alterações toohello classes podem causar uma alteração de formato de dados. É preciso ter cuidado tooensure uma atualização sem interrupção pode lidar com alteração de formato de dados de saudação. Exemplos que podem causar alterações no formato de dados:

* Adicionar ou remover campos ou propriedades
* Renomear campos ou propriedades
* Alterar os tipos de campos ou propriedades Olá
* Alterar o namespace ou nome de classe Olá

### <a name="data-contract-as-hello-default-serializer"></a>Contrato de dados como Olá serializador padrão
serializador Olá é geralmente responsável por ler dados saudação e desserializá-lo na versão atual do hello, mesmo se os dados saudação estão em uma versão ou *mais recente* versão. Olá, serializador padrão é hello [serializador de contrato de dados](https://msdn.microsoft.com/library/ms733127.aspx), que tem regras de controle de versão bem definido. Confiável coleções permitem Olá serializador toobe substituído, mas atores confiável no momento não. o serializador de dados Olá desempenha um papel importante em permitir atualizações sem interrupção. o serializador de contrato de dados Olá é serializador Olá que recomendamos para aplicativos do Service Fabric.

## <a name="how-hello-data-format-affects-a-rolling-upgrade"></a>Como o formato de dados Olá afeta uma atualização sem interrupção
Durante uma atualização sem interrupção, há dois cenários principais, onde poderá encontrar mais antigas serializador hello ou *mais recente* versão dos dados:

1. Depois que um nó é atualizado e inicia o backup, serializador novo Olá carregará dados de saudação que estava toodisk persistido por uma versão antiga hello.
2. Durante a saudação atualização sem interrupção, o cluster Olá conterá uma mistura de versões antigas e novas de saudação do seu código. Como réplicas podem ser colocadas em diferentes domínios de atualização e réplicas de enviam dados tooeach outros, hello antigo e/ou nova versão de seus dados pode ser encontrado por versão de novo e/ou antigo de saudação do seu serializador.

> [!NOTE]
> Olá "nova versão" e "antigo" aqui, consulte toohello versão do código que está sendo executado. Olá "novo serializador" refere-se o código do serializador toohello que está sendo executado na nova versão de saudação do seu aplicativo. Hello "novos dados" se refere a classe c# toohello serializado da nova versão de saudação do seu aplicativo.
> 
> 

Olá duas versões de código e formato de dados deve ser frente e para trás compatível. Se eles não forem compatíveis, Olá atualização sem interrupção pode falhar ou dados podem ser perdidos. Olá atualização sem interrupção pode falhar porque o código hello ou serializador pode gerar exceções ou uma falha ao encontrar hello outra versão. Dados podem ser perdidos se, por exemplo, uma nova propriedade foi adicionada, mas o serializador antigo Olá descarta durante a desserialização.

Contrato de dados é hello recomendado solução para assegurar que seus dados sejam compatíveis. Ele possui regras de versão bem definidas para adição, remoção e alteração de campos. Ele também tem suporte para lidar com campos desconhecidos, conectando-se ao processo de serialização e desserialização hello e lidar com herança de classe. Para saber mais, confira [Usando o contrato de dados](https://msdn.microsoft.com/library/ms733127.aspx).

## <a name="next-steps"></a>Próximas etapas
[Atualização do aplicativo usando o Visual Studio](service-fabric-application-upgrade-tutorial.md) orienta você durante a atualização de aplicativo usando o Visual Studio.

[Atualização do aplicativo usando o PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) orienta você uma atualização de aplicativo usando o PowerShell.

Controle como seu aplicativo é atualizado usando [Parâmetros de Atualização](service-fabric-application-upgrade-parameters.md).

Saiba como toouse funcionalidade avançada ao atualizar seu aplicativo referindo-se muito[tópicos avançados](service-fabric-application-upgrade-advanced.md).

Corrigir problemas comuns em atualizações de aplicativo consultando etapas toohello [de solução de problemas de atualizações de aplicativo ](service-fabric-application-upgrade-troubleshooting.md).

