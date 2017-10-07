---
title: "Visão geral de integridade do recurso aaaAzure | Microsoft Docs"
description: "Visão geral do Azure Resource Health"
services: Resource health
documentationcenter: 
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: service-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 07/01/2017
ms.author: BernardoAMunoz
ms.openlocfilehash: f06153864090487829f717dc3e8972c78a4a58af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-health-overview"></a>Visão geral do Azure Resource Health
 
O Resource Health ajuda a diagnosticar e obter suporte quando um problema do Azure afeta seus recursos. Ele informa sobre integridade de saudação atuais e anteriores de seus recursos e ajuda a mitigar os problemas. O Resource Health fornece suporte técnico quando você precisa de ajuda com problemas de serviço do Azure.

Enquanto [Status do Azure](https://status.azure.com) informa você sobre problemas de serviço que afetam um amplo conjunto de clientes do Azure, a integridade de recursos fornece um painel personalizado de integridade de saudação de seus recursos. Integridade de recursos mostra todas as vezes Olá seus recursos não estavam disponíveis no hello devido a problemas de serviço tooAzure. Isso torna fácil para você toounderstand se um SLA foi violado. 

## <a name="what-is-considered-a-resource-and-how-does-resource-health-decides-if-a-resource-is-healthy-or-not"></a>O que é considerado um recurso e como o Resource Health decide se um recurso está íntegro ou não?
Um recurso é uma instância criada de um tipo de recurso oferecido por um serviço do Azure por meio do Azure Resource Manager, por exemplo: uma máquina virtual, um aplicativo Web ou um banco de dados SQL.

Integridade de recursos depende de sinais emitidos pelo Olá diferentes serviços do Azure tooassess se um recurso é Íntegro ou não. Se um recurso não está íntegro, integridade de recursos analisa informações adicionais toodetermine Olá origem Olá problema. Ele também identifica ações que Microsoft está demorando problema de saudação toofix ou o que ações tooaddress Olá causam do problema de saudação. 

Lista completa de saudação de revisão dos tipos de recursos e de integridade verifica [integridade de recursos do Azure](resource-health-checks-resource-types.md) para obter detalhes adicionais sobre como a integridade é avaliada.

## <a name="health-status-provided-by-resource-health"></a>Status de integridade fornecida pelo Resource Health
integridade de saudação de um recurso é um dos Olá status a seguir:

### <a name="available"></a>Disponível
serviço de saudação não detectou todos os eventos afetar a integridade de saudação do recurso de saudação. Em casos onde o recurso de saudação se recuperou de tempo de inatividade não planejado durante a saudação última 24 horas, você verá Olá **recuperado recentemente** notificação.

![Máquina virtual disponível do Resource Health](./media/resource-health-overview/Available.png)

### <a name="unavailable"></a>Indisponível
serviço de saudação detectou um evento de plataforma não afetar a integridade de saudação do recurso de saudação ou a plataforma em andamento.

#### <a name="platform-events"></a>Eventos de plataforma
Esses eventos são disparados por vários componentes de saudação infraestrutura do Azure e incluem ações agendadas, como manutenção planejada e incidentes inesperados, como uma reinicialização do host não planejado.

Integridade de recursos fornece detalhes adicionais sobre o evento hello, o processo de recuperação hello e habilita o suporte de toocontact mesmo se você não tiver um ativo do Microsoft contrato de suporte.

![Recurso integridade indisponível máquina de virtual vencimento evento tooplatform](./media/resource-health-overview/Unavailable.png)

#### <a name="non-platform-events"></a>Eventos de não plataforma
Esses eventos são disparados por ações realizadas por usuários, por exemplo parar uma máquina virtual ou alcançar Olá o número máximo de conexões tooa Cache Redis.

![Recurso integridade indisponível máquina de virtual vencimento evento toonon plataforma](./media/resource-health-overview/Unavailable_NonPlatform.png)

### <a name="unknown"></a>Desconhecido
Esse status de integridade indica que o Resource Health não recebeu informações sobre este recurso há mais de 10 minutos. Embora esse status não é uma indicação definitiva do estado de saudação do recurso Olá, é um ponto de dados importantes no processo de solução de problemas de saudação:
* Se estiver executando o recurso hello como status Olá esperado do recurso Olá atualizará tooAvailable após alguns minutos.
* Se você estiver tendo problemas com o recurso de saudação, hello status de integridade desconhecido pode sugerir recursos Olá é afetado por um evento na plataforma de saudação.

![Máquina virtual desconhecida do Resource Health](./media/resource-health-overview/Unknown.png)

## <a name="report-an-incorrect-status"></a>Relatar um status incorreto
Se a qualquer momento você acredita que o status de integridade atual do hello está incorreto, você pode Fale conosco clicando **relatar status de integridade incorreto**. Em casos em que será afetado por um problema do Azure, recomendamos que você toocontact suporte na folha de integridade de recursos de saudação. 

![Status incorreto do Relatório do Resource Health](./media/resource-health-overview/incorrect-status.png)

## <a name="historical-information"></a>Informações de histórico
Você pode acessar o too14 dias de dados de histórico de integridade clicando **Exibir histórico** na folha de integridade do recurso de saudação. 

![Histórico do Relatórios do Resource Health](./media/resource-health-overview/history-blade.png)

## <a name="getting-started"></a>Introdução
tooopen integridade de recursos para um recurso
1.  Entrar hello portal do Azure.
2.  Navegue tooyour recursos.
3.  No menu de recurso Olá localizado no lado esquerdo da saudação, clique em **integridade de recursos**.

![Abra o Resource Health na folha Recurso](./media/resource-health-overview/from-resource-blade.png)

Você também pode acessar a integridade de recursos clicando **mais serviços**e digitando **integridade de recursos** na saudação de tooopen de caixa de texto de filtro **ajuda + suporte** folha. Finalmente, clique em [**Resource Health**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).

![Abra o Resource Health em Mais serviços](./media/resource-health-overview/FromOtherServices.png)

## <a name="next-steps"></a>Próximas etapas

Check-out toolearn esses recursos mais informações sobre a integridade de recursos:
-  [Tipos de recursos e verificações de integridade no Azure Resource Health](resource-health-checks-resource-types.md)
-  [Perguntas frequentes sobre o Azure Resource Health](resource-health-faq.md)




