---
title: "Guia de política de aaaSupportability e desativação para o sistema operacional de convidado do Azure | Microsoft Docs"
description: "Fornece informações sobre o que a Microsoft dará suporte em relação ao toohello sistema operacional de convidado do Azure usado pelos serviços de nuvem."
services: cloud-services
documentationcenter: na
author: raiye
manager: timlt
editor: 
ms.assetid: 919dd781-4dc6-4e50-bda8-9632966c5458
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 5/26/2017
ms.author: raiye
ms.openlocfilehash: 6a86c42ac95d12bbf116d900b7afb26fc3fe34e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-guest-os-supportability-and-retirement-policy"></a>Capacidade de suporte e política de desativação do SO convidado do Azure
informações de saudação nesta página referem-se toohello sistema de operacional de convidado do Azure ([sistema operacional convidado](cloud-services-guestos-update-matrix.md)) para funções dos serviços de nuvem web e de trabalho (PaaS). Não é aplicável a máquinas de tooVirtual (IaaS).

A Microsoft tem uma publicação [política de suporte para o sistema operacional convidado de saudação](http://support.microsoft.com/gp/azure-cloud-lifecycle-faq). página Olá que você está lendo agora descreve como Olá política é implementada.

Olá política é

1. A Microsoft oferecerá suporte **Olá pelo menos duas famílias mais recentes do sistema operacional convidado de saudação**. Quando uma família for desativada, os clientes têm 12 meses a partir Olá desativação oficial data tooupdate tooa mais recente com suporte família do SO convidado.
2. A Microsoft oferecerá suporte **Olá pelo menos duas versões mais recentes das famílias de sistema operacional convidado Olá suportada**.
3. A Microsoft oferecerá suporte **Olá pelo menos duas versões mais recentes do SDK do Azure de saudação**. Quando uma versão de hello que SDK está desativado, os clientes terão 12 meses a partir Olá desativação oficial data tooupdate tooa mais recente versão.

Às vezes, pode haver suporte para mais de duas famílias ou versões. Informações oficiais de suporte de sistema operacional convidado serão exibidos na Olá [versões de sistema operacional convidado do Azure e matriz de compatibilidade do SDK](cloud-services-guestos-update-matrix.md).

## <a name="when-a-guest-os-family-or-version-is-retired"></a>Quando uma família ou versão de sistemas operacionais convidados for desativada
Um novo sistema operacional convidado **família** foi introduzido em algum momento após o lançamento da saudação de uma nova versão oficial do sistema de operacional de servidor do Windows hello. Sempre que uma nova família de sistema operacional convidado for introduzida, Microsoft desativará a família de sistemas operacionais convidados mais antiga hello.

Novo sistema operacional convidado **versões** são lançadas a cada mês tooincorporate Olá MSRC atualizações. Devido a saudação atualizações regulares mensais, uma versão de sistema operacional convidado é desabilitada normalmente 60 dias após seu lançamento. Essa atividade mantém pelo menos duas versões de sistema operacional convidado para cada família disponíveis para uso.

### <a name="process-during-a-guest-os-family-retirement"></a>Processo durante a desativação de uma família de sistemas operacionais convidados
Depois de saudação retirada é anunciada, os clientes têm um período de 12 meses "transição" antes de família mais antiga Olá seja oficialmente removida do serviço. Esse período de transição pode ser estendido a critério da saudação da Microsoft. As atualizações serão postadas Olá [versões de sistema operacional convidado do Azure e matriz de compatibilidade do SDK](cloud-services-guestos-update-matrix.md).

Um processo gradual de desativação será iniciado seis (6) meses no período de transição de saudação. Durante esse tempo:

1. A Microsoft notificará os clientes da desativação de saudação.
2. versão mais recente de saudação do hello Azure SDK não oferecerá suporte a família do SO convidado Olá obsoleto.
3. Novas implantações e reimplantações dos serviços de nuvem não serão permitidas na família Olá desativado

A Microsoft continuará toointroduce nova versão do SO convidado incorporar as atualizações mais recentes de MSRC Olá até Olá último dia do período de transição hello, conhecido como hello "data de validade". Data de expiração hello, serviços de nuvem ainda em execução terão suporte no hello SLA do Azure. A Microsoft tem Olá critério tooforce atualizar, excluir ou interromper os serviços após essa data.

### <a name="process-during-a-guest-os-version-retirement"></a>Processo durante a desativação de uma versão do SO convidado
Se os clientes definirem a atualização do sistema operacional convidado tooautomatically, eles nunca terem tooworry sobre como lidar com as versões de sistema operacional convidado. Eles estarão sempre com versão de sistema operacional convidado mais recente da saudação.

Versões do SO convidado são lançadas a cada mês. Devido à taxa de saudação lançamentos regulares, cada versão tem um tempo fixo.

Em 60 dias de vida hello, há uma versão "*desabilitado*". "Desabilitado" significa que a versão Olá é removida do portal de saudação. versão Olá não pode ser definido no arquivo de configuração CSCFG hello. As implantações existentes são mantidas em execução. Mas o código e configuração de implantações de tooexisting de atualizações e novas implantações não serão permitidas.

Algum tempo depois de se tornar "desabilitada" hello versão do SO convidado "*expira*" e todas as instalações que ainda estiverem executando essa versão serão forçosamente atualizadas e definir tooautomatically Olá de atualização de sistema operacional convidado em Olá futuras. Expiração é feita em lotes para que o período de saudação de tempo de desativação tooexpiration pode variar.

Esses períodos podem ser feitos mais nas transições do cliente de tooease critério da Microsoft. As alterações serão comunicadas Olá [versões de sistema operacional convidado do Azure e matriz de compatibilidade do SDK](cloud-services-guestos-update-matrix.md).

### <a name="notifications-during-retirement"></a>Notificações durante a desativação
* **Desativação de família** <br>A Microsoft usará postagens de blog e notificação no portal. Os clientes que ainda estejam usando uma família desativada do sistema operacional convidado serão notificados por meio de administradores de serviço tooassigned comunicação direta (email, mensagens do portal, telefonema). Todas as alterações serão postadas toothis página e hello RSS feed listado no início de saudação desta página.
* **Desativação de versão** <br>Todas as alterações e datas Olá ocorrerem serão lançadas toothis página e hello RSS feed listado no início de saudação desta página, incluindo a versão, desabilitado e expiração. Os administradores de serviços receberão emails se tiverem implantações em execução em uma família ou versão do SO convidado desabilitada. tempo de saudação de emails pode variar. Geralmente, eles são enviados pelo menos um mês antes da desabilitação, embora esse intervalo não seja um SLA oficial.

## <a name="frequently-asked-questions"></a>Perguntas frequentes
**Como posso reduzir os impactos de saudação da migração?**

Recomendamos o uso da família mais recente do sistema operacional convidado para criar seus Serviços de Nuvem.

1. Começar a planejar sua família mais recente do tooa de migração no início.
2. Configure tootest de implantações de teste temporárias seu serviço de nuvem em execução na nova família de saudação.
3. Definir a versão do sistema operacional convidado muito**automático** (osVersion = * no hello [. cscfg](cloud-services-model-and-package.md#cscfg) arquivo) para versões do SO convidado Olá migração toonew ocorra automaticamente.

**E se meu aplicativo web exige uma integração mais profunda com hello sistema operacional?**

Se a arquitetura do aplicativo web depende de recursos subjacentes do sistema operacional de hello, usar os recursos de plataforma com suporte, como [tarefas de inicialização](cloud-services-startup-tasks.md) ou outros mecanismos de extensibilidade. Como alternativa, você também pode usar [máquinas virtuais do Azure](https://azure.microsoft.com/documentation/scenarios/virtual-machines/) (IaaS-infraestrutura como serviço), em que você é responsável por manter Olá subjacente do sistema operacional.

## <a name="next-steps"></a>Próximas etapas
Saudação de revisão mais recente [versões de sistema operacional convidado](cloud-services-guestos-update-matrix.md).
