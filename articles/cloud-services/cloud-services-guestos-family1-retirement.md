---
title: "aaaGuest sistema operacional família 1 desativação Observe | Microsoft Docs"
description: "Fornece informações sobre quando a desativação de hello Azure SO convidado família 1 aconteceu e como toodetermine se você for afetado"
services: cloud-services
documentationcenter: na
author: raiye
manager: timlt
editor: 
ms.assetid: 37b422e9-0713-4a81-a942-f553ef478064
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 5/21/2017
ms.author: raiye
ms.openlocfilehash: fa8b904c6560dbbe4982c301f818c7a5cbc4eacb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="guest-os-family-1-retirement-notice"></a>Aviso de desativação da família 1 de SO convidados
desativação de saudação da família 1 do SO foi anunciada em 1 de junho de 2013.

**2 de setembro de 2014** Olá o sistema operacional de convidado do Azure (SO convidado) família 1. x, que é baseado no sistema operacional de saudação do Windows Server 2008, foi oficialmente desativado. Todas as tentativas toodeploy novos serviços ou atualizações serviços existentes usando a família 1 falharão com uma mensagem de erro informando que Olá que SO convidado família 1 foi desativado.

**3 de novembro de 2014** O suporte estendido para a família 1 dos sistemas operacionais convidados terminou e está totalmente desativado. Todos os serviços que ainda estão na família 1 serão afetados. Podemos interromper esses serviços a qualquer momento. Não há nenhuma garantia que os serviços continuarão toorun, a menos que você atualize-os manualmente por conta própria.

Se você tiver outras perguntas, visite Olá [fóruns de serviços de nuvem](http://social.msdn.microsoft.com/Forums/home?forum=windowsazuredevelopment&filter=alltypes&sort=lastpostdesc) ou [entre em contato com o suporte do Azure](https://azure.microsoft.com/support/options/).

## <a name="are-you-affected"></a>Você foi afetado?
Os serviços de nuvem são afetados se qualquer um dos seguintes Olá se aplica:

1. Você tem um valor de "osFamily ="1"explicitamente especificado no arquivo ServiceConfiguration cscfg Olá para seu serviço de nuvem.
2. Você não tem um valor de osFamily especificado explicitamente no arquivo ServiceConfiguration cscfg Olá para seu serviço de nuvem. Atualmente, sistema Olá usa saudação padrão valor de "1" neste caso.
3. Olá portal do Azure lista o valor da família do sistema operacional convidado como "Windows Server 2008".

toofind quais dos seus serviços de nuvem estão executando quais famílias de sistema operacional, você pode executar Olá seguinte script do PowerShell do Azure, embora você deva [configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs) primeiro. Para obter mais informações sobre o script hello, consulte [Azure convidado sistema operacional família 1 fim da vida útil: junho de 2014](http://blogs.msdn.com/b/ryberry/archive/2014/04/02/azure-guest-os-family-1-end-of-life-june-2014.aspx).

```Powershell
foreach($subscription in Get-AzureSubscription) {
    Select-AzureSubscription -SubscriptionName $subscription.SubscriptionName

    $deployments=get-azureService | get-azureDeployment -ErrorAction Ignore | where {$_.SdkVersion -NE ""}

    $deployments | ft @{Name="SubscriptionName";Expression={$subscription.SubscriptionName}}, ServiceName, SdkVersion, Slot, @{Name="osFamily";Expression={(select-xml -content $_.configuration -xpath "/ns:ServiceConfiguration/@osFamily" -namespace $namespace).node.value }}, osVersion, Status, URL
}
```

Os serviços de nuvem serão afetados pela desativação da família 1 do SO se a coluna de osFamily Olá na saída do script hello está vazia ou contém um "1".

## <a name="recommendations-if-you-are-affected"></a>Recomendações se você for afetado
Recomendamos que você migre seu tooone de funções de serviço de nuvem de famílias de SO convidado Olá com suporte:

**Família 4.x dos SOs convidados** - Windows Server 2012 R2 *(recomendado)*

1. Certifique-se de que seu aplicativo esteja usando o SDK 2.1 ou posterior com o .NET Framework 4.0, 4.5 ou 4.5.1.
2. Definir o arquivo de ServiceConfiguration. cscfg do hello osFamily atributo muito "4" hello em e reimplante o serviço de nuvem.

**Família 3.x dos SOs convidados** - Windows Server 2012

1. Certifique-se de que seu aplicativo esteja usando o SDK 1.8 ou posterior com o .NET Framework 4.0 ou 4.5.
2. Definir o arquivo de ServiceConfiguration. cscfg do hello osFamily atributo muito "3" hello em e reimplante o serviço de nuvem.

**Família 2.x dos SOs convidados** - Windows Server 2008 R2

1. Certifique-se de que seu aplicativo esteja usando o SDK 1.3 e posterior com o .NET Framework 3.5 ou 4.0.
2. Definir o arquivo de ServiceConfiguration. cscfg do hello osFamily atributo muito "2" hello em e reimplante o serviço de nuvem.

## <a name="extended-support-for-guest-os-family-1-ended-nov-3-2014"></a>O suporte estendido para a Família 1 dos sistemas operacionais convidados terminou em 3 de novembro de 2014
Não há mais suporte para serviços de nuvem na família 1 dos sistemas operacionais convidados. Migre da família 1 assim tooavoid possíveis interrupções de serviço.  

## <a name="next-steps"></a>Próximas etapas
Saudação de revisão mais recente [versões de sistema operacional convidado](cloud-services-guestos-update-matrix.md).
