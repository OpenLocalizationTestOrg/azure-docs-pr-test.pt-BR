---
title: "aaaDownload Azure dados de uso da fatura e diário cobrança | Microsoft Docs"
description: "Descreve como toodownload ou exibir sua cobrança do Azure fatura e dados de uso diário."
keywords: "fatura de cobrança, download de fatura, fatura do Azure, uso do Azure"
services: 
documentationcenter: 
author: genlin
manager: tonguyen
editor: 
tags: billing
ms.assetid: 6d568d1d-3bd6-4348-97d0-1098b5fe0661
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: genli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2826df10f39914fcaeb9985271dadde550c68dfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="download-or-view-your-azure-billing-invoice-and-daily-usage-data"></a>Baixar ou exibir a fatura de cobrança e os dados de uso diário do Azure
Você pode baixar a fatura do hello [portal do Azure](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) ou enviá-lo por email. toodownload seu uso diário, vá toohello [Centro de contas Azure](https://account.windowsazure.com). Somente determinadas funções têm permissão tooget fatura e uso de informações, como Olá administrador da conta de cobrança. toolearn mais sobre como obter acesso toobilling informações, consulte [gerenciar acesso tooAzure usando funções de cobrança](billing-manage-access.md).

## <a name="get-your-invoice-in-email-pdf"></a>Obter sua fatura por email (.pdf)
Você pode ativar e configurar destinatários adicionais tooreceive fatura do Azure em um email. Esse recurso pode não estar disponível para determinadas assinaturas, como ofertas de suporte, Enterprise Agreements ou Azure via Open.

1. Selecione sua assinatura do hello [folha assinaturas](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade). Aceitação para todas as assinaturas que você possui. Clique em **Faturas** e em **Enviar minha fatura por email**. 

    ![Captura de tela que mostra o fluxo de consentimento Olá](./media/billing-download-azure-invoice-daily-usage-date/InvoicesDeepLink.PNG)
    
2. Clique em **aceitar** e aceite os termos de saudação.

    ![Captura de tela que mostra o fluxo de consentimento Olá](./media/billing-download-azure-invoice-daily-usage-date/InvoiceArticleStep2.PNG)
 
3. Depois que você aceitou o contrato de saudação, você pode configurar outros destinatários.

    ![Captura de tela que mostra o fluxo de consentimento Olá](./media/billing-download-azure-invoice-daily-usage-date/InvoiceArticleStep3.PNG)
    
Se você não obtiver um email após seguir as etapas de saudação, verifique se seu endereço de email está correto no hello [preferências de comunicação em seu perfil](https://account.windowsazure.com/profile).

## <a name="download-invoice-from-azure-portal-pdf"></a>Baixar fatura no Portal do Azure (.pdf)

1. Selecione sua assinatura do hello [folha assinaturas](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) no portal do Azure como [um usuário com acesso tooinvoices](billing-manage-access.md).

2. Selecione **Faturas**. 

    ![Captura de tela que mostra a opção de uso e de cobrança Olá](./media/billing-download-azure-invoice-daily-usage-date/billingandusage.png) 

3. Clique em **fatura baixar** tooview uma cópia de sua fatura do PDF. Se ele for **não disponível**, consulte [por que não vejo uma fatura para Olá último período de cobrança?](#noinvoice)

    ![Captura de tela que mostra os períodos de cobrança, opção de download hello e total de cobranças para cada período de cobrança](./media/billing-download-azure-invoice-daily-usage-date/billing4.png)

4. Você também pode exibir seu uso diário clicando o período de cobrança hello. 

Para saber mais sobre a fatura, confira [Entenda sua fatura do Microsoft Azure](billing-understand-your-bill.md). Para obter ajuda sobre como gerenciar custos, consulte [Evitar custos inesperados com o gerenciamento de custo e cobrança do Azure](billing-getting-started.md).

## <a name="download-usage-from-hello-account-center-csv"></a>Baixar o uso de saudação Centro de contas (. csv)

1. O logon no hello [Centro de contas Azure](https://account.windowsazure.com/subscriptions) como Olá administrador da conta.

2. Selecione a assinatura de saudação do qual você deseja informações de fatura e uso de saudação.

3. Clique em **HISTÓRICO DE COBRANÇA**. 

    ![Captura de tela que mostra a opção de histórico de cobrança](./media/billing-download-azure-invoice-daily-usage-date/Billinghisotry.png)

4. Você pode ver as instruções para Olá últimos seis períodos de cobrança e Olá atual não cobrado período. 

    ![Captura de tela que mostra os períodos de cobrança, opções toodownload fatura e uso diário e encargos total para cada período de cobrança](./media/billing-download-azure-invoice-daily-usage-date/billingSum.png)

5. Selecione **exibir instrução atual** toosee uma estimativa de seus encargos na estimativa de saudação do tempo Olá foi gerada. Essas informações são atualizadas diariamente e talvez não incluam todo o seu uso. Sua fatura mensal pode ser diferente dessa estimativa.

    ![Captura de tela que mostra a opção de exibir instrução atual Olá](./media/billing-download-azure-invoice-daily-usage-date/billingSum2.png)

    ![Captura de tela que mostra Olá estimativa de cobrança atual](./media/billing-download-azure-invoice-daily-usage-date/billingSum3.png)

6. Selecione **baixar uso** toodownload Olá dados de uso diário como um arquivo CSV. Se você vir duas versões disponíveis, baixe a versão 2.

    ![Captura de tela que mostra a opção de baixar uso Olá](./media/billing-download-azure-invoice-daily-usage-date/DLusage.png)

Olá administrador da conta pode acessar o Centro de contas do Azure hello. Outros administradores de cobrança, como um proprietário, poderão obter informações de uso usando Olá [cobrança APIs](billing-usage-rate-card-overview.md).

Para saber mais sobre o uso diário, confira [Entenda sua fatura do Microsoft Azure](billing-understand-your-bill.md). Para obter ajuda sobre como gerenciar custos, consulte [Evitar custos inesperados com o gerenciamento de custo e cobrança do Azure](billing-getting-started.md).

## <a name="noinvoice"></a>Por que não vejo uma fatura para Olá último período de cobrança?

Pode haver vários motivos pelos quais você não vê uma fatura:

- Você tem um valor de crédito mensal com sua assinatura que não foi ultrapassado ou você tem uma Avaliação Gratuita. Uma fatura é gerada somente quando você é um devedor.

- É menor que 30 dias a partir do dia Olá que inscrito tooAzure.

- fatura Olá não foi gerada ainda. Aguarde até o final de saudação do período de cobrança hello.

- Se você não tiver Olá administrador da conta, faturas mais antigas não podem ser tooyou disponível.

## <a name="need-help-contact-support"></a>Precisa de ajuda? Entre em contato com o suporte.
Se você ainda tiver mais perguntas, [entre em contato com o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget seu problema resolvido rapidamente.

