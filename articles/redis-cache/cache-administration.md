---
title: aaaHow tooadminister Cache Redis do Azure | Microsoft Docs
description: "Saiba como tooperform as tarefas de administração como reinicializar e agendar atualizações para o Cache Redis do Azure"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 8c915ae6-5322-4046-9938-8f7832403000
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 07/05/2017
ms.author: sdanie
ms.openlocfilehash: eb24668a3f6264444e7d4daf1ac43b41b12dfe66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadminister-azure-redis-cache"></a>Como tooadminister Cache Redis do Azure
Este tópico descreve como tooperform tarefas de administração como [reinicializando](#reboot) e [agendar atualizações](#schedule-updates) para suas instâncias de Cache Redis do Azure.

## <a name="reboot"></a>Reboot
Olá **reinicializar** folha permite que você tooreboot um ou mais nós de seu cache. Esse recurso de reinicialização permite que você tootest seu aplicativo para garantir a resiliência se houver uma falha de um nó de cache.

![Reboot](./media/cache-administration/redis-cache-administration-reboot.png)

Selecione Olá nós tooreboot e clique em **reinicializar**.

![Reboot](./media/cache-administration/redis-cache-reboot.png)

Se você tiver um cache premium com cluster habilitado, você pode selecionar quais fragmentos de saudação tooreboot de cache.

![Reboot](./media/cache-administration/redis-cache-reboot-cluster.png)

tooreboot um ou mais nós de seu cache, selecione nós de saudação desejado e clique em **reinicializar**. Se você tiver um cache premium com cluster habilitado, selecione tooreboot de fragmentos de saudação desejada e, em seguida, clique em **reinicializar**. Depois de alguns minutos, Olá reinicialização nós selecionados e estiverem online novamente depois de alguns minutos.

impacto de saudação em aplicativos cliente varia dependendo de quais nós reinicializar.

* **Mestre** - ao nó mestre Olá for reinicializado, o Azure falhará de Cache Redis ao nó de réplica toohello e promove o toomaster. Durante esse failover, pode haver um pequeno intervalo em que as conexões podem falhar toohello cache.
* **Subordinada** - ao nó de escravo Olá for reinicializado, normalmente, não há nenhum cliente toocache de impacto.
* **Mestre e escravo** - quando ambos os nós de cache são reiniciados, todos os dados são perdidos no hello cache e conexões toohello cache falharão até que o nó primário Olá volta a ficar online. Se você tiver configurado [persistência de dados](cache-how-to-premium-persistence.md), backup mais recente da saudação é restaurado quando o cache de saudação volta a ficar online, mas qualquer gravações em cache que ocorreu após o backup mais recente hello serão perdidas.
* **O cache de nós de um premium com cluster habilitado** - quando você reiniciar um ou mais nós de um cache premium com clustering habilitado, Olá comportamento de saudação selecionado nós é Olá mesmo como quando você reinicializar o nó correspondente hello ou nós de não clusterizado cache.

> [!IMPORTANT]
> A reinicialização agora está disponível para todos os tipos de preço.
> 
> 

## <a name="reboot-faq"></a>Perguntas frequentes sobre reinicialização
* [Qual o nó deve reinicializar tootest meu aplicativo?](#which-node-should-i-reboot-to-test-my-application)
* [Conexões de cliente Olá cache tooclear pode reinicializar?](#can-i-reboot-the-cache-to-clear-client-connections)
* [Perderei dados do cache se eu fizer uma reinicialização?](#will-i-lose-data-from-my-cache-if-i-do-a-reboot)
* [Posso reinicializar o cache usando o PowerShell, a CLI ou outras ferramentas de gerenciamento?](#can-i-reboot-my-cache-using-powershell-cli-or-other-management-tools)
* [Camadas de preços do que podem usar a funcionalidade de reinicialização Olá?](#what-pricing-tiers-can-use-the-reboot-functionality)

### <a name="which-node-should-i-reboot-tootest-my-application"></a>Qual o nó deve reinicializar tootest meu aplicativo?
tootest resiliência de saudação do seu aplicativo contra falhas de nó primário de saudação do cache, reinicialização Olá **mestre** nó. tootest resiliência de saudação do seu aplicativo contra falhas de nó secundário hello, reinicialização Olá **subordinado** nó. tootest resiliência de saudação do seu aplicativo contra falha total do cache de hello, reinicialize **ambos** nós.

### <a name="can-i-reboot-hello-cache-tooclear-client-connections"></a>Conexões de cliente Olá cache tooclear pode reinicializar?
Sim, se você reinicializar o cache de saudação todas as conexões de cliente são desmarcadas. A reinicialização pode ser útil no caso de Olá onde todas as conexões de cliente são usadas devido a erro de lógica de tooa ou um bug no aplicativo de cliente hello. Cada camada de preços tem diferentes [limites de conexão de cliente](cache-configure.md#default-redis-server-configuration) para Olá vários tamanhos, e quando esses limites são atingidos, conexões de cliente não mais são aceitas. Reinicializar cache Olá fornece uma maneira tooclear todas as conexões de cliente.

> [!IMPORTANT]
> Se você reinicializar as conexões de cliente do cache tooclear, Stackexchange reconecta-se automaticamente depois que o nó de Redis hello está novamente online. Se o problema subjacente Olá não for resolvido, as conexões de cliente de saudação podem continuar toobe usada.
> 
> 

### <a name="will-i-lose-data-from-my-cache-if-i-do-a-reboot"></a>Perderei dados do cache se eu fizer uma reinicialização?
Se você reinicializar ambos Olá **mestre** e **subordinado** nós, todos os dados no cache de hello (ou esse fragmento se você estiver usando um cache premium com cluster habilitado) é perdida. Se você tiver configurado [persistência de dados](cache-how-to-premium-persistence.md), backup mais recente Olá será restaurado quando o cache de saudação volta a ficar online, mas qualquer gravações em cache que ocorreram depois Olá backup foi feito serão perdidas.

Se você reinicializar apenas um de nós hello, dados não são normalmente perdidos, mas ainda pode ser. Por exemplo, se o nó mestre Olá é reinicializado e a gravação em cache está em andamento, dados de saudação de gravação de cache de saudação for perdido. Outro cenário de perda de dados seria se você reinicializar um nó e Olá outro nó acontece toogo inativo devido a falha de tooa em hello simultaneamente. Para obter mais informações sobre possíveis causas de perda de dados, consulte [quais dados toomy com Redis?](https://gist.github.com/JonCole/b6354d92a2d51c141490f10142884ea4#file-whathappenedtomydatainredis-md)

### <a name="can-i-reboot-my-cache-using-powershell-cli-or-other-management-tools"></a>Posso reinicializar o cache usando o PowerShell, a CLI ou outras ferramentas de gerenciamento?
Sim, para o PowerShell obter instruções, consulte [tooreboot um cache Redis](cache-howto-manage-redis-cache-powershell.md#to-reboot-a-redis-cache).

### <a name="what-pricing-tiers-can-use-hello-reboot-functionality"></a>Camadas de preços do que podem usar a funcionalidade de reinicialização Olá?
A reinicialização está disponível para todos os tipos de preço.

## <a name="schedule-updates"></a>Agende atualizações
Olá **agendar atualizações** folha permite que você toodesignate uma janela de manutenção para o cache de camada Premium. Quando a janela de manutenção de saudação for especificada, as atualizações de servidor do Redis são feitas durante essa janela. 

> [!NOTE] 
> janela de manutenção de saudação se aplica apenas atualizações de servidor tooRedis e não tooany Azure atualiza ou atualiza o sistema operacional de toohello de saudação VMs que hospedam o cache de saudação.
> 
> 

![Agende atualizações](./media/cache-administration/redis-schedule-updates.png)

toospecify uma janela de manutenção, verifique dias Olá desejado e especifique a hora de início de janela de manutenção de saudação para cada dia e clique em **Okey**. Observe que o tempo de janela de manutenção de saudação é em UTC. 

> [!NOTE]
> janela de manutenção saudação padrão para atualizações é de cinco horas. Esse valor não é configurável de saudação portal do Azure, mas você pode configurá-lo no PowerShell usando Olá `MaintenanceWindow` parâmetro hello [AzureRmRedisCacheScheduleEntry novo](/powershell/module/azurerm.rediscache/new-azurermrediscachescheduleentry) cmdlet. Para saber mais, confira [Posso gerenciar as atualizações agendadas usando o PowerShell, a CLI ou outras ferramentas de gerenciamento?](#can-i-manage-scheduled-updates-using-powershell-cli-or-other-management-tools)
> 
> 

## <a name="schedule-updates-faq"></a>Perguntas frequentes sobre agendamento de atualizações
* [Quando as atualizações ocorrem se não usar o recurso de atualizações de agenda Olá?](#when-do-updates-occur-if-i-dont-use-the-schedule-updates-feature)
* [O tipo de atualizações feitas durante a saudação agendadas a janela de manutenção?](#what-type-of-updates-are-made-during-the-scheduled-maintenance-window)
* [Posso gerenciar as atualizações agendadas usando o PowerShell, a CLI ou outras ferramentas de gerenciamento?](#can-i-managed-scheduled-updates-using-powershell-cli-or-other-management-tools)
* [Camadas de preços do que podem usar a funcionalidade de atualizações de agenda Olá?](#what-pricing-tiers-can-use-the-schedule-updates-functionality)

### <a name="when-do-updates-occur-if-i-dont-use-hello-schedule-updates-feature"></a>Quando as atualizações ocorrem se não usar o recurso de atualizações de agenda Olá?
Se você não especificar uma janela de manutenção, as atualizações poderão ser feitas a qualquer momento.

### <a name="what-type-of-updates-are-made-during-hello-scheduled-maintenance-window"></a>O tipo de atualizações feitas durante a saudação agendadas a janela de manutenção?
Redis somente as atualizações são feitas durante a janela de manutenção agendada de saudação do servidor. janela de manutenção de saudação não se aplica a atualizações de tooAzure ou atualiza o sistema de operacional VM toohello.

### <a name="can-i-managed-scheduled-updates-using-powershell-cli-or-other-management-tools"></a>Posso gerenciar as atualizações agendadas usando o PowerShell, a CLI ou outras ferramentas de gerenciamento?
Sim, você pode gerenciar as atualizações agendadas usando Olá cmdlets do PowerShell a seguir:

* [Get-AzureRmRedisCachePatchSchedule](/powershell/module/azurerm.rediscache/get-azurermrediscachepatchschedule)
* [New-AzureRmRedisCachePatchSchedule](/powershell/module/azurerm.rediscache/new-azurermrediscachepatchschedule)
* [New-AzureRmRedisCacheScheduleEntry](/powershell/module/azurerm.rediscache/new-azurermrediscachescheduleentry)
* [Remove-AzureRmRedisCachePatchSchedule](/powershell/module/azurerm.rediscache/remove-azurermrediscachepatchschedule)

### <a name="what-pricing-tiers-can-use-hello-schedule-updates-functionality"></a>Camadas de preços do que podem usar a funcionalidade de atualizações de agenda Olá?
Olá **agendar atualizações** recurso só está disponível no premium Olá preço.

## <a name="next-steps"></a>Próximas etapas
* Explore mais recursos da [camada premium do Cache Redis do Azure](cache-premium-tier-intro.md) .

