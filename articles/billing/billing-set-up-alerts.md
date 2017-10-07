---
title: "aaaSet os alertas de crédito ou de cobrança de assinaturas do Azure | Microsoft Docs"
description: "Descreve como você pode configurar alertas na sua conta do Azure para que possa evitar surpresas na cobrança."
keywords: "alerta de crédito, alerta de cobrança"
services: 
documentationcenter: 
author: vikdesai
manager: tonguyen
editor: 
tags: billing
ms.assetid: 9b7b3eeb-cd9d-4690-86a3-51b1e2a8974f
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: vikdesai
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 711b9c72c59874792b0e229cdc5ec0fa517c24c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-billing-or-credit-alerts-for-your-microsoft-azure-subscriptions"></a>Configurar alertas de cobrança ou de crédito para assinaturas do Microsoft Azure
Se você estiver Olá administrador da conta para uma assinatura do Azure, você pode usar o hello Azure cobrança serviço Alerta alertas de cobrança toocreate personalizado que ajudam a monitorar e gerenciar a atividade de cobrança para suas contas do Azure.

Esse serviço é na visualização, portanto, você precisa tooenable-lo na página de recursos de visualização de saudação primeiro.

## <a name="set-hello-alert-threshold-and-email-recipients"></a>Definir Olá alertas limite e destinatários de email
1. Visite [página de recursos de visualização de saudação](https://account.windowsazure.com/PreviewFeatures) e habilitar **serviço de alerta de cobrança**.

1. Após receber a confirmação de email de Olá Olá serviço de cobrança é ativado para sua assinatura, visite [página de assinaturas Olá](https://account.windowsazure.com/Subscriptions) no portal de conta hello. Clique na assinatura Olá você deseja toomonitor e, em seguida, clique em **alertas**.

    ![Captura de tela da exibição de assinaturas de saudação do Centro de conta do Azure, com alertas realçado][Image1]

2. Em seguida, clique em **adicionar alerta** toocreate o primeiro deles. Você pode definir um total de cinco alertas de cobrança por assinatura, com um limite diferente e até tootwo destinatários de email para cada alerta.

    ![Captura de tela da saudação exibir alertas, onde você pode adicionar alerta][Image2]

3. Quando você adiciona um alerta, dê a ele um nome exclusivo, escolha um limite de gasto e escolha Olá endereços de email onde os alertas são enviados. Ao configurar o limite de saudação, você pode escolher um **Total de cobrança** ou um **crédito monetário** de saudação **alerta para** lista. Para um total de cobrança, um alerta é enviado quando o gasto da assinatura excede o limite de saudação. Para um crédito monetário, um alerta é enviado quando os créditos monetários caem abaixo do limite de saudação. Créditos monetários geralmente se aplicam a assinaturas de avaliação e o Visual Studio tooFree.

    ![Captura de tela de modo de exibição de alerta de adição de hello, onde você pode configurar os destinatários][Image3]

O Azure suporta qualquer endereço de email mas não verifique se o endereço de email Olá funciona, portanto, verifique erros de digitação.

## <a name="check-on-your-alerts"></a>Verificar os seus alertas
Depois de configurar alertas, Olá Centro de contas lista e mostra quantos mais você pode configurar. Para cada alerta, você pode ver Olá data e hora de envio, se é um alerta do Total de cobrança ou crédito monetário e limite Olá que você configurar. formato de data e hora da saudação é 24 horas Hora Universal coordenada (UTC) e data de saudação é o formato aaaa-mm-dd. Clique Olá além de assiná-lo para um alerta no hello lista tooedit ou Olá Lixeira toodelete-lo.

## <a name="billing-alerts-for-enterprise-agreement-ea-customers"></a>Alertas de cobrança para clientes do EA (Enterprise Agreement)
Os clientes do EA podem obter alertas para cada departamento em um registro configurando cotas de gasto. Consulte [departamento gastos cotas](https://ea.azure.com/helpdocs/departmentSpendingQuotas) em tooget portal de EA Olá iniciado.

## <a name="learn-more-about-azure-cost-management"></a>Saiba mais sobre o gerenciamento de custos do Azure
- Estimar os custos usando Olá [Calculadora de preços](https://azure.microsoft.com/pricing/calculator/), [custo total de cálculo de propriedade](https://aka.ms/azure-tco-calculator), e quando você adiciona um serviço.
- [Analise o uso e os custos regularmente no Portal do Azure](billing-getting-started.md#costs).
- Ative [Recomendações de custo do Assistente do Azure](../advisor/advisor-cost-recommendations.md).

mais, consulte toolearn [orientações sobre o gerenciamento de custos do Azure](billing-getting-started.md).

[Image1]: ./media/azure-billing-set-up-alerts/billingalert1.png 
[Image2]: ./media/azure-billing-set-up-alerts/billingalert2.png
[Image3]: ./media/azure-billing-set-up-alerts/billingalerts3.png 
