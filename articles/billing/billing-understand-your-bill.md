---
title: aaaUnderstand sua conta do Azure | Microsoft Docs
description: "Saiba como tooread e entender seu uso e cobrança para sua assinatura do Azure"
services: 
documentationcenter: 
author: tonguyen10
manager: tonguyen
editor: 
tags: billing
ms.assetid: 32eea268-161c-4b93-8774-bc435d78a8c9
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/14/2017
ms.author: tonguyen
ms.openlocfilehash: a3195eb129b1576e8cb665aa6f88a1a2647edd78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-your-bill-for-microsoft-azure"></a>Entenda sua fatura do Microsoft Azure
toounderstand do Azure cobrar, compare sua fatura com detalhadas arquivo de uso diário hello e hello relatórios de gerenciamento no portal do Azure de saudação de custo.

tooobtain um PDF da fatura e uma cópia do seu detalhadas diário uso CSV download do arquivo, consulte [obter do Azure da fatura e diário dados de uso de cobrança](billing-download-azure-invoice-daily-usage-date.md). 

Para termos e descrições detalhados de sua fatura e arquivo de uso diário detalhado, consulte [Compreender os termos em sua fatura do Microsoft Azure](billing-understand-your-invoice.md) e [Compreender os termos em seu uso detalhado do Microsoft Azure](billing-understand-your-usage.md). 

Para obter detalhes sobre Olá relatórios de gerenciamento de custos, consulte [gerenciamento de custos do portal do Azure](https://docs.microsoft.com/en-us/azure/billing/billing-getting-started).


## <a name="charges"></a>Como ter certeza de que encargos Olá na minha fatura estão corretos?
Se há um encargo na fatura sobre o qual você deseja obter mais detalhes, há duas opções.

### <a name="option-1-review-your-invoice-and-compare-hello-usage-and-costs-with-hello-detailed-usage-csv-file"></a>Opção 1: Examine sua fatura e compare custos e uso de saudação com hello detalhada arquivo CSV de uso

Olá arquivo CSV de uso detalhadas mostra os encargos por período de cobrança e de uso diário. tooget seu uso detalhado arquivo CSV, consulte [obter do Azure da fatura e diário dados de uso de cobrança](https://docs.microsoft.com/en-us/azure/billing/billing-download-azure-invoice-daily-usage-date).

Encargos de uso são exibidos no nível de medidor hello. Hello seguintes termos significam Olá iguais em ambos os fatura hello e Olá arquivo detalhadas de uso. Por exemplo, Olá cobrança ciclo na fatura Olá é o período de cobrança toohello equivalente mostrado no arquivo de uso detalhadas hello.

 | Fatura (PDF) | Uso detalhado (CSV)|
 | --- | --- |
|Ciclo de cobrança | Período de Cobrança |
 |Nome |Categoria de medidor |
 |Tipo |Subcategoria de Medidor |
 |Recurso |Nome do medidor |
 |Região |Região do medidor |
 |Consumido |Quantidade consumida |
 |Incluso |Quantidade incluída |
 |Faturável |Quantidade de excesso |

Olá **encargos de uso** seção da fatura tem o valor total de saudação de cada medidor que foi consumida durante o período de cobrança. Por exemplo, hello seguinte captura de tela mostra uma taxa de uso para Olá serviço Agendador do Azure.

![Encargos de uso da fatura](./media/billing-understand-your-bill/1.png)

Olá **instrução** seção de seu uso detalhadas CSV mostra Olá mesmo custo. Ambos os Olá *consumido* quantidade e *valor* fatura de saudação de correspondência.

![Encargos de uso de CSV](./media/billing-understand-your-bill/2.png)

toosee uma análise gratuitamente em uma base diária, vá toohello **uso diário** seção Olá CSV. Filtrar por "Agendador" em *categoria medidor* e você pode ver quais medidor de saudação dias foi usado e quanto foi consumido. Olá *recurso* e *grupo de recursos* informações também são listadas para comparação. Olá *consumido* valores devem somar do toowhat mostrado na fatura hello.

![Seção de uso diária em Olá CSV](./media/billing-understand-your-bill/3.png)

custo de saudação tooget por dia, multiplique Olá *consumido* quantidades com hello *taxa* valor da saudação **instrução** seção.

toolearn mais sobre a fatura hello, consulte [entender sua fatura do Azure](billing-understand-your-invoice.md).

toolearn sobre cada uma das colunas Olá Olá CSV, consulte [entender seu uso detalhadas do Azure](billing-understand-your-invoice.md).

### <a name="option-2-review-your-invoice-and-compare-with-hello-usage-and-costs-in-hello-azure-portal"></a>Opção 2: Examinar sua fatura e comparar com o uso de saudação e os custos de saudação portal do Azure

Olá portal do Azure pode ajudá-lo a verificar se as cobranças. Olá portal do Azure fornece gráficos de gerenciamento de custo para uma visão geral de seus encargos de uso e hello em sua fatura.

toocontinue com exemplo hello acima, visite Olá [página assinaturas](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade), selecione sua assinatura e, em seguida, escolha **análise de custo**. A partir daí, você pode especificar o período de tempo de saudação e consulte encargos de uso para serviço de Agendador do Azure hello.

![Exibição de análise de custo no portal do Azure](./media/billing-understand-your-bill/4.png)

toosee Olá diário divisão de custo em **custo histórico**, clique em linha de saudação.

![Exibição de histórico de custo no Portal do Azure](./media/billing-understand-your-bill/5.png)

mais, consulte toolearn [impedir que inesperado custos com gerenciamento de custos e de cobrança do Azure](billing-getting-started.md#costs).

## <a name="external"></a>E quanto a cobranças de serviço externo?
Serviços externos (também conhecidos como pedidos do Azure Marketplace) são fornecidos por fornecedores de serviços independentes e são cobrados separadamente. encargos de saudação não aparecem em sua fatura do Azure. mais, consulte toolearn [entender o Azure cobra serviço externo](billing-understand-your-azure-marketplace-charges.md).

## <a name="payment"></a>Como fazer um pagamento?

Se você configurar um cartão de crédito ou um cartão de débito como seu método de pagamento, pagamento Olá será cobrado automaticamente dentro de 10 dias após o término do período de cobrança hello. Na sua declaração de cartão de crédito, o item de linha de saudação diria **MSFT Azure**.

Se você [pagar por faturamento](billing-how-to-pay-by-invoice.md), enviar seu local de toohello pagamento listada na parte inferior da saudação da fatura. Para obter mais ajuda, [entre em contato com o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).

## <a name="how-do-i-check-hello-status-of-a-payment-made-by-credit-card"></a>Como verificar o status de saudação de um pagamento feito por cartão de crédito?

[Crie um tíquete de suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooask para status de saudação do pagamento. 

## <a name="tips-for-cost-management"></a>Dicas para gerenciamento de custos
- Estimar os custos usando Olá [Calculadora de preços](https://azure.microsoft.com/pricing/calculator/) e [custo total de cálculo de propriedade](https://aka.ms/azure-tco-calculator)e obter Olá [obter informações de preços para cada serviço](https://azure.microsoft.com/en-us/pricing/).
- [Configurar alertas de cobrança](billing-set-up-alerts.md).
- [Examine o uso e custos regularmente no portal do Azure de saudação](billing-getting-started.md#costs).

## <a name="need-help-contact-support"></a>Precisa de ajuda? Entre em contato com o suporte.

Se você ainda precisar de Ajuda, [entre em contato com o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget seu problema resolvido rapidamente.
