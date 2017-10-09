---
title: "problemas de disponibilidade de aaaApplication e serviço para perguntas frequentes sobre serviços de nuvem do Azure Microsoft | Microsoft Docs"
description: "Este artigo lista Olá perguntas frequentes sobre o aplicativo e a disponibilidade do serviço para serviços de nuvem do Microsoft Azure."
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: cd0d9ba0beb1dc72d4761f8b89c2ecadb51c7e48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="application-and-service-availability-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a>Perguntas frequentes sobre problemas de aplicativo e disponibilidade de serviço para Serviços de Nuvem do Azure

Este artigo inclui as perguntas frequentes sobre problemas de aplicativo e disponibilidade do serviço para [Serviços de Nuvem do Microsoft Azure](https://azure.microsoft.com/services/cloud-services). Você também pode consultar Olá [página de tamanho de VM de serviços de nuvem](cloud-services-sizes-specs.md) para obter informações de tamanho.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="my-role-got-recycled-was-there-any-update-rolled-out-for-my-cloud-service"></a>A minha função foi reciclada. Alguma atualização foi distribuída para meu serviço de nuvem?
Aproximadamente uma vez por mês, a Microsoft libera uma nova versão do SO Convidado para VMs de PaaS do Microsoft Azure. O sistema operacional convidado é apenas uma atualização no pipeline de saudação. Uma versão pode ser afetada por vários outros fatores. Além disso, o Azure é executado em centenas de milhares de computadores. Portanto, é impossível toopredict Olá data e hora exatas quando suas funções serão reinicializadas. Podemos atualizar Olá convidado SO RSS Feed de atualização com informações mais recentes de saudação que temos, mas você deve considerar que relataram um valor aproximado de toobe de tempo. Estamos cientes de que isso é problemático para os clientes e estiver trabalhando em um plano toolimit ou reinicializações de tempo com precisão.

Para obter detalhes completos sobre atualizações recentes do SO Convidado, consulte [Versões do SO Convidado do Azure e matriz de compatibilidade do SDK](cloud-services-guestos-update-matrix.md).

Para obter informações úteis sobre reinicializações e ponteiros detalhes tootechnical de Host de sistema operacional convidado e atualizações, consulte Olá MSDN postagem de blog [função reinicializações de instância devido atualizações de tooOS](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx).

## <a name="why-does-hello-first-request-toomy-cloud-service-after-hello-service-has-been-idle-for-some-time-take-longer-than-usual"></a>Por que Olá primeira solicitação toomy serviço de nuvem depois que o serviço Olá ficar ocioso por algum tempo leva mais tempo?
Quando Olá servidor Web recebe Olá primeira solicitação, ele primeiro recompila código hello e, em seguida, processa a solicitação de saudação. Por que é Olá primeira solicitação demorado do que Olá outras pessoas. Por padrão, o pool de aplicativo hello obtém desligado em casos de inatividade do usuário. o pool de aplicativos Olá também reciclará por padrão cada 1.740 minutos (29 horas).

Pools de aplicativos de serviços de informações da Internet (IIS) podem ser recicladas periodicamente tooavoid estados instável que podem causar falhas de tooapplication, travamentos ou vazamentos de memória.

Olá documentos a seguir ajudarão você a entender e atenuar esse problema:
* [Como corrigir carregamento inicial lento para IIS](http://stackoverflow.com/questions/13386471/fixing-slow-initial-load-for-iis)
* [A primeira solicitação do aplicativo Web IIS 7.5 após reciclagem do pool de aplicativos é muito lenta](http://stackoverflow.com/questions/13917205/iis-7-5-web-application-first-request-after-app-pool-recycle-very-slow)

Se desejar que o comportamento do toochange saudação padrão do IIS, você precisará toouse as tarefas de inicialização, porque se você aplicar manualmente instâncias de função Web toohello alterações, alterações de saudação eventualmente serão perdidas.

Para obter mais informações, consulte [como as tarefas de inicialização tooconfigure e execução de um serviço de nuvem](cloud-services-startup-tasks.md).
