---
title: "atualização de aplicativo de malha aaaService | Microsoft Docs"
description: "Este artigo fornece uma introdução tooupgrading um aplicativo de malha do serviço, incluindo modos de atualização escolhendo e executando verificações de integridade."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 803c9c63-373a-4d6a-8ef2-ea97e16e88dd
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 6f649ef4a5c0afab682522bcba7d2d66a4268ead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade"></a>Atualização de aplicativos do Service Fabric
Um aplicativo do Azure Service Fabric é uma coleção de serviços. Durante uma atualização, o Service Fabric compara Olá novo [o manifesto do aplicativo](service-fabric-application-model.md#describe-an-application) com versão anterior do hello e determina quais serviços de aplicativo hello exigem atualizações. Service Fabric compara versão Olá números no serviço Olá manifestos com números de versão de saudação na versão anterior do hello. Se um serviço não foi alterado, ele não foi atualizado.

## <a name="rolling-upgrades-overview"></a>Visão geral das atualizações sem interrupção
Em uma atualização sem interrupção do aplicativo, a atualização de saudação é executada em estágios. Em cada estágio, a atualização de saudação é aplicado tooa subconjunto de nós no cluster hello, chamado de um domínio de atualização. Como resultado, o aplicativo hello permanece disponível durante a atualização de saudação. Durante a atualização de saudação cluster Olá pode conter uma mistura de versões antigas e novas de saudação.

Por esse motivo, as versões de saudação dois devem ser frente e para trás compatível. Se eles não forem compatíveis, o administrador do aplicativo hello é responsável por uma disponibilidade toomaintain de atualização de várias fases de preparação. Em uma atualização de várias fases, primeira etapa de saudação está atualizando versão intermediária tooan aplicativo hello que é compatível com a versão anterior de saudação. Olá segunda etapa é tooupgrade Olá versão final que quebras de compatibilidade com a versão de pré-atualização hello, mas é compatível com versão intermediária hello.

Domínios de atualização são especificados no manifesto do cluster hello quando você configurar o cluster hello. Os domínios de atualização não recebem atualizações em uma ordem específica. Um domínio de atualização é uma unidade lógica de implantação para um aplicativo. Domínios de atualização permitem Olá serviços tooremain a alta disponibilidade durante uma atualização.

As atualizações sem interrupção não são possíveis se Olá for aplicado tooall nós no cluster hello, que é o caso de saudação quando o aplicativo hello tem apenas um domínio de atualização. Essa abordagem não é recomendável, pois o serviço Olá fica inativo e não está disponível no momento de saudação da atualização. Além disso, o Azure não fornece qualquer garantia quando um cluster é configurado com apenas um domínio de atualização.

## <a name="health-checks-during-upgrades"></a>Verificações de integridade durante atualizações
Para uma atualização, as diretivas de integridade tem toobe definido (ou valores padrão podem ser usados). Uma atualização é chamada com êxito quando todos os domínios de atualização são atualizados em Olá especificado tempos limite e quando a atualização de todos os domínios são considerados íntegros.  Um domínio de atualização Íntegro significa que esse domínio de atualização Olá passado todas as verificações de integridade Olá especificadas na política de integridade de saudação. Por exemplo, uma política de integridade pode obrigar que todos os serviços em uma instância do aplicativo estejam *íntegros*, de acordo com a definição de integridade do Service Fabric.

As políticas e verificações de integridade durante a atualização feita pelo Service Fabric são independentes do serviço e do aplicativo. Ou seja, nenhum teste específico de serviço é realizado.  Por exemplo, o serviço pode ter um requisito de taxa de transferência, mas o Service Fabric não tem a taxa de transferência do hello informações toocheck. Consulte toohello [artigos de integridade](service-fabric-health-introduction.md) para verificações de saudação que são executadas. verificações de saudação que ocorrem durante uma atualização incluir testa se o pacote de aplicativo hello foi copiado corretamente, se Olá instância foi iniciada e assim por diante.

integridade do aplicativo Hello é uma agregação de entidades de filho de saudação do aplicativo hello. Em resumo, Service Fabric avalia a integridade de saudação do aplicativo hello por meio de integridade Olá relatado no aplicativo hello. Também avalia a integridade Olá de todos os serviços de saudação para o aplicativo hello dessa maneira. Adicional do Service Fabric avalia a integridade de saudação dos serviços de aplicativo hello agregando integridade Olá de seus filhos, como réplicas do serviço hello. Quando a política de integridade de aplicativo hello for satisfeita, atualização Olá pode continuar. Se a política de integridade de saudação for violada, a atualização do aplicativo hello falhará.

## <a name="upgrade-modes"></a>Modos de atualização
Olá modo que recomendamos para atualização de aplicativo é Olá monitorado, que é o modo de saudação usado com frequência. Modo monitorado executa a atualização de saudação na atualização de um domínio e se as verificações de integridade de todos os passagem (por Olá política especificada), move em toohello próximo domínio de atualização automaticamente.  Se as verificações de integridade falharem e/ou tempos limite é atingido, Olá é ou reverter a atualização para o domínio de atualização de saudação ou modo Olá é alterado toounmonitored manual. Você pode configurar Olá toochoose atualização um desses dois modos para atualizações que falharam. 

Não monitorado de modo manual precisa de intervenção manual depois de cada atualização em um domínio de atualização, tookick off Olá atualização no próximo domínio de atualização hello. Nenhuma verificação de integridade do Service Fabric é executada. administrador Olá executa verificações de integridade ou status de saudação antes de Iniciar atualização Olá Olá próximo domínio de atualização.

## <a name="upgrade-default-services"></a>Fazer upgrade dos serviços padrão
Serviços de padrão de aplicativo de malha do serviço podem ser atualizados durante o processo de atualização de saudação de um aplicativo. Serviços padrão são definidos em Olá [o manifesto do aplicativo](service-fabric-application-model.md#describe-an-application). saudação de regras padrão da atualização de serviços padrão é:

1. Serviços de saudação novo padrão [o manifesto do aplicativo](service-fabric-application-model.md#describe-an-application) que não existe no cluster Olá são criados.
> [!TIP]
> [EnableDefaultServicesUpgrade](service-fabric-cluster-fabric-settings.md#fabric-settings-that-you-can-customize) precisa toobe definir tootrue tooenable Olá regras a seguir. Esse recurso é compatível com a v5.5.

2. Os serviços padrão existentes no [manifesto do aplicativo](service-fabric-application-model.md#describe-an-application) anterior e na nova versão são atualizados. Descrições de serviços na nova versão de hello substituiria aqueles já está em cluster hello. A atualização do aplicativo é revertida automaticamente na falha de atualização do serviço padrão.
3. Serviços de saudação anterior padrão [o manifesto do aplicativo](service-fabric-application-model.md#describe-an-application) , mas não na nova versão de hello serão excluídos. **Observe que essa exclusão de serviços padrão não pode ser revertida.**

No caso de um aplicativo de atualização é revertida, serviços padrão são toohello revertido status antes do início da atualização. Mas os serviços excluídos nunca poderão ser criados.

## <a name="application-upgrade-flowchart"></a>Fluxograma de atualização de aplicativo
fluxograma Olá este parágrafo a seguir pode ajudá-lo a entender o processo de atualização de saudação de um aplicativo de malha do serviço. Em particular, descreve o fluxo de Olá Olá como tempos-limite, inclusive *HealthCheckStableDuration*, *HealthCheckRetryTimeout*, e *UpgradeHealthCheckInterval*, ajuda a controlar quando Olá atualização no domínio de uma atualização é considerada um sucesso ou falha.

![processo de atualização Olá para um aplicativo de serviço de malha][image]

## <a name="next-steps"></a>Próximas etapas
[Atualização do aplicativo usando o Visual Studio](service-fabric-application-upgrade-tutorial.md) orienta você durante a atualização de aplicativo usando o Visual Studio.

[Atualização do aplicativo usando o PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) orienta você uma atualização de aplicativo usando o PowerShell.

Controle como seu aplicativo é atualizado usando [Parâmetros de Atualização](service-fabric-application-upgrade-parameters.md).

Verifique suas atualizações de aplicativo compatível aprendendo como toouse [serialização de dados](service-fabric-application-upgrade-data-serialization.md).

Saiba como toouse funcionalidade avançada ao atualizar seu aplicativo referindo-se muito[tópicos avançados](service-fabric-application-upgrade-advanced.md).

Corrigir problemas comuns em atualizações de aplicativo consultando etapas toohello [de solução de problemas de atualizações de aplicativo](service-fabric-application-upgrade-troubleshooting.md).

[image]: media/service-fabric-application-upgrade/service-fabric-application-upgrade-flowchart.png
