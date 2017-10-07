---
title: "Visão geral da integridade do serviço aaaAzure | Microsoft Docs"
description: "Informações personalizadas sobre como seus aplicativos do Azure são afetados pela manutenção e pelos problemas de serviço atuais e futuros do Azure."
services: Resource health
documentationcenter: 
author: rboucher
manager: 
editor: 
ms.assetid: 
ms.service: service-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 07/07/2017
ms.author: robb
ms.openlocfilehash: 2b536ee2f19757d4f2baf5529866c3d159a4670c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-health"></a>Integridade de serviço do Azure
A integridade de serviço do Azure fornece informações em tempo hábil e personalizadas a respeito de quando problemas nos serviços do Azure afetam seus serviços.  Ela também ajuda você a se preparar para a próxima manutenção planejada.

## <a name="service-health-events"></a>Eventos de Integridade do Serviço
A integridade do serviço controla os três tipos de eventos de integridade que podem afetar seus recursos:
1. **Problemas de serviço** -Olá de problemas em serviços do Azure que afetam você no momento. 
2. **Manutenção planejada** -próxima manutenção que possa afetar a disponibilidade de saudação de seus serviços em Olá futuras.  
3. **Aconselhamento de integridade** – alterações nos serviços do Azure que exigem sua atenção. Exemplos incluem quando os recursos do Azure são preteridos ou se você excede uma cota de uso.

    ![Eventos de integridade do serviço](./media/service-health-overview/azure-service-health-overview-7.png)

## <a name="get-started-with-service-health"></a>Introdução à integridade de serviço
toolaunch seu painel de integridade do serviço, selecione Olá integridade do serviço de bloco no seu painel do portal. Se você removeu anteriormente bloco hello, ou você estiver usando o painel personalizado, procurar por serviço de integridade do serviço em "Serviços mais" (parte inferior esquerda no painel).
![Introdução à integridade de serviço](./media/service-health-overview/azure-service-health-overview-1.png)

## <a name="see-current-issues-which-impact-your-services"></a>Ver problemas atuais que afetam seus serviços
Olá **problemas de serviço** exibe quaisquer problemas contínuos em serviços do Azure que estão afetando seus recursos. Você pode entender quando Olá problema começou e os serviços e as regiões são afetadas. Você também pode ler hello mais recente atualização toounderstand o Azure está fazendo o problema de saudação tooresolve. 
![Gerenciar problema de serviço](./media/service-health-overview/azure-service-health-overview-2.png)

Escolha Olá **impacto potencial** lista específica de saudação do toosee de guia de recursos possui que talvez seja afetado pelo problema hello. Você pode baixar uma lista CSV de tooshare esses recursos com sua equipe.
![Gerenciar o problema de serviço – impacto](./media/service-health-overview/azure-service-health-overview-4.png)

## <a name="get-links-and-downloadable-explanations"></a>Obter links e explicações para download 
Você pode obter um link para Olá problema toouse no seu sistema de gerenciamento de problema. Você pode baixar o PDF e, às vezes, tooshare de arquivos CSV com pessoas que não têm acesso toohello portal do Azure.   
![Gerenciar problema de serviço – gerenciamento de problemas](./media/service-health-overview/azure-service-health-overview-3.png)

## <a name="get-support-from-microsoft"></a>Obter suporte da Microsoft
Se o recurso é deixado em um estado inválido até mesmo após Olá problema for resolvido, contate o suporte.  Use links de suporte Olá Olá à direita da página de saudação.  

## <a name="pin-a-personalized-health-map-tooyour-dashboard"></a>Fixar um painel de tooyour do mapa de integridade personalizado
Filtre a integridade do serviço tooshow suas assinaturas essenciais aos negócios, regiões e tipos de recursos. Salve filtro hello e fixar um painel portal tooyour de mapa personalizado integridade mundo. 
![Filtrar mapa de integridade personalizado](./media/service-health-overview/azure-service-health-overview-6a.png)
![Fixar um mapa de integridade personalizado](./media/service-health-overview/azure-service-health-overview-6b.png)

## <a name="configure-service-health-alerts"></a>Configurar alertas de Integridade de Serviço
A integridade do serviço do Azure se integra ao tooalert do Monitor do Azure você por meio de emails, mensagens de texto e notificações de webhook quando os recursos essenciais são afetados. Configure um alerta de log de atividade para eventos de integridade do serviço apropriado hello. Rota que pessoas apropriadas de toohello em sua organização usando grupos de ação de alerta. Para obter mais informações, consulte [Configurar alertas para a Integridade do Serviço](../monitoring-and-diagnostics/monitoring-activity-log-alerts-on-service-notifications.md)

# <a name="next-steps"></a>Próximas etapas
Configure alertas para receber notificações de problemas de integridade. Para obter mais informações, consulte [Configurar alertas do Service Health](../monitoring-and-diagnostics/monitoring-activity-log-alerts-on-service-notifications.md). 