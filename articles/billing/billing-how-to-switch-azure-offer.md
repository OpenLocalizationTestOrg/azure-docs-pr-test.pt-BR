---
title: Alterar oferta de assinatura do Azure | Microsoft Docs
description: Saiba mais sobre como alterar sua assinatura do Azure e mudar para uma oferta diferente usando o Centro de Contas do Azure
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing,top-support-issue
ms.assetid: aae227b3-6d64-4550-a5b6-d359f53f0a59
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: troubleshooting
ms.date: 08/30/2017
ms.author: genli
ms.openlocfilehash: 381994079b7bcaeff08802b06573b977bf631e9d
ms.sourcegitcommit: b07d06ea51a20e32fdc61980667e801cb5db7333
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="change-your-azure-pay-as-you-go-subscription-to-a-different-offer"></a>Alterar sua assinatura Paga Conforme o Uso do Azure para uma oferta diferente

Como um cliente [Pré-pago](https://azure.microsoft.com/offers/ms-azr-0003p/), você pode alterar sua assinatura do Azure para outra oferta no [Centro de Contas](https://account.windowsazure.com/Subscriptions). Por exemplo, você pode usar esse recurso para aproveitar os [créditos mensais para assinantes do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/). 

**Deseja apenas atualizar da avaliação gratuita?** Consulte [atualizar para Pago Conforme o Uso](billing-upgrade-azure-subscription.md).

## <a name="whats-supported"></a>O que tem suporte:

| Da | Para |
| --- | --- |
| Pré-paga |[Desenvolvimento/Teste pré-pago](https://azure.microsoft.com/offers/ms-azr-0023p/) |
| Pré-paga |[Visual Studio Professional](https://azure.microsoft.com/offers/ms-azr-0059p/) |
| Pré-paga |[Visual Studio Test Professional](https://azure.microsoft.com/offers/ms-azr-0060p/) |
| Pré-paga |[Plataformas MSDN](https://azure.microsoft.com/offers/ms-azr-0062p/) |
| Pré-paga |[Visual Studio Enterprise](https://azure.microsoft.com/offers/ms-azr-0063p/) |
| Pré-paga |[Visual Studio Enterprise (Bizspark)](https://azure.microsoft.com/offers/ms-azr-0064p/) |

> [!NOTE]
> Para obter outras alterações da oferta, [contate o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).
>
>

## <a name="switch-subscription-offer"></a>Alternar oferta de assinatura

> [!VIDEO https://channel9.msdn.com/Series/Microsoft-Azure-Tutorials/Switch-to-a-different-Azure-offer/player]
>
>

1. Entre no [Centro de Contas do Azure](https://account.windowsazure.com/Subscriptions).
1. Selecione sua assinatura Pré-paga.
1. Clique em **Alterar para outra oferta**. O botão só estará disponível se você estiver em Pré-pago e com o primeiro período de cobrança.

   ![Observe o botão Alterar oferta do lado direito da página](./media/billing-how-to-switch-azure-offer/switchbutton.png)
1. **Selecione a oferta desejada** da lista de ofertas para as quais sua assinatura pode ser alternada. Essa lista varia com base nas associações em que sua conta está associada. Se nada estiver disponível, verifique a [lista de ofertas disponíveis para as quais você pode alternar](#whats-supported) e confirme se você tem as associações corretas. 

   ![Selecione uma oferta para a qual você deseja alternar](./media/billing-how-to-switch-azure-offer/selectoffer.png)
1. Dependendo da oferta para qual esteja trocando, é provável que você veja uma observação sobre o impacto da troca. Examine a lista cuidadosamente e siga as instruções antes de prosseguir.

   ![Analise as notas](./media/billing-how-to-switch-azure-offer/thingstonote.png)
1. Você pode renomear sua assinatura. Por padrão, podemos defini-la com o nome da nova oferta. Clique em **Alterar Oferta** para concluir o processo.

   ![Clique no botão verde](./media/billing-how-to-switch-azure-offer/confirmpage.png)
1. Sucesso! Sua assinatura foi trocada pela nova oferta.

## <a name="frequently-asked-questions"></a>Perguntas frequentes

### <a name="what-is-an-azure-offer"></a>O que é uma oferta do Azure?

Uma oferta do Azure é o *tipo* de assinatura do Azure que você tem. Por exemplo, [Pré-pago](https://azure.microsoft.com/offers/ms-azr-0003p/), [Azure via Open](https://azure.microsoft.com/offers/ms-azr-0111p/) e [Visual Studio Enterprise](https://azure.microsoft.com/offers/ms-azr-0063p/) são todas ofertas do Azure. Cada oferta apresenta diferentes [termos](https://azure.microsoft.com/support/legal/offer-details/) e alguns têm vantagens especiais. A oferta da sua assinatura pode ser encontrada na página de assinatura do Centro de Contas. Clique no nome da oferta para obter mais detalhes.

   ![Clique no link Oferta no Centro de Contas para obter mais detalhes](./media/billing-how-to-switch-azure-offer/offerlink.png)

### <a name="why-dont-i-see-the-button"></a>Por que não vejo o botão?

Talvez você não veja o botão **Alterar para outra oferta** se:

* Você não está em [Pré-pago](https://azure.microsoft.com/offers/ms-azr-0003p/). No momento, apenas assinaturas Pagas Conforme o Uso podem ser convertidas para outra oferta.
  * Se você estiver em [Avaliação Gratuita](https://azure.microsoft.com/free/), saiba como [fazer upgrade para Pré-pago](billing-upgrade-azure-subscription.md).
  * Para alternar a oferta de uma assinatura diferente, [entre em contato com o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).
* Você ainda está em seu primeiro período de cobrança. Você deve aguardar até que seu primeiro período de cobrança seja concluído antes de poder alternar as ofertas.

### <a name="why-do-i-see-there-are-no-offers-available-in-your-region-or-country-at-this-time"></a>Por que vejo “Não há ofertas disponíveis em seu país ou região no momento”?

* Você pode não estar qualificado para quaisquer alterações de oferta. Verifique a [lista de ofertas disponíveis para as quais você pode mudar](#whats-supported) e certifique-se de que você ativou os benefícios corretos com o Visual Studio ou o Bizspark.
* Algumas ofertas podem não estar disponíveis em todos os países.

### <a name="what-does-switching-azure-offers-do-to-my-service-and-billing"></a>O que a troca das ofertas do Azure oferece ao meu serviço e à cobrança?

Aqui estão os detalhes do que acontece quando você alterna entre as ofertas do Azure no Centro de Contas.

#### <a name="no-service-downtime"></a>Não há tempo de inatividade do serviço

Não há nenhum tempo de inatividade do serviço para os usuários associados à assinatura. No entanto, a nova oferta poderá ter restrições. Por exemplo, algumas ofertas proíbem o uso de produção, portanto, seria necessário mover os recursos de produção para outra assinatura.

#### <a name="quota-increases-are-reset"></a>Os aumentos de cota são redefinidos

Quando você muda de oferta, qualquer [aumento de cota ou de limite acima do limite padrão](../azure-supportability/resource-manager-core-quotas-request.md) é redefinido. Não há nenhum tempo de inatividade do serviço, mesmo que você tenha mais recursos além do limite padrão. Por exemplo, você estiver usando 200 núcleos em sua assinatura, mudar de oferta redefinirá sua cota de núcleos de volta para o valor padrão de 20 núcleos. As VMs que usam os 200 núcleos não são afetadas e continuarão em execução. Se você não fizer outra solicitação de aumento de cota, no entanto, você não poderá provisionar nenhum núcleo adicional.

#### <a name="billing"></a>Cobrança

No dia da alteração, uma fatura é gerada para todos os encargos pendentes. Em seguida, sua assinatura é cobrada pelos termos de preços da nova oferta. O vencimento da cobrança da assinatura será alterado para a data da alteração da oferta. Os dados de uso e de cobrança anteriores à alteração da oferta não serão mantidos, portanto, recomendamos que você baixe uma cópia antes da troca.

### <a name="can-i-migrate-from-pay-as-you-go-to-cloud-solution-providerhttpspartnermicrosoftcomsolutionscloud-reseller-overview-csp-or-enterprise-agreementhttpsazuremicrosoftcompricingenterprise-agreement-ea"></a>Posso migrar de Pré-pago para [Provedor de Soluções na Nuvem](https://partner.microsoft.com/Solutions/cloud-reseller-overview) (CSP) ou [Contrato Enterprise](https://azure.microsoft.com/pricing/enterprise-agreement/) (EA)?

* Para migrar para o CSP, confira [Migração de assinatura com pagamento conforme o uso do Azure para o CSP](https://docs.microsoft.com/azure/cloud-solution-provider/migration/migration-from-payg-to-csp).
* Para migrar para o EA, peça ao Administrador de Registro para adicionar sua conta no EA. Siga as instruções no email de convite para que suas assinaturas sejam movidas para o registro de EA. Para saber mais, confira [Associar uma conta existente](https://ea.azure.com/helpdocs/associateExistingAccount) no portal do EA.

### <a name="can-i-migrate-data-and-services-to-a-new-subscription"></a>Posso migrar dados e serviços para uma nova assinatura?

* Você pode migrar os recursos diretamente para a nova assinatura. Confira [Mover recursos para um novo grupo de recursos ou uma nova assinatura](../azure-resource-manager/resource-group-move-resources.md).
* Para transferir a propriedade de uma assinatura do Azure e todo o conteúdo para outra pessoa, confira [Transferring ownership of an Azure subscription](billing-subscription-transfer.md) (Transferindo a propriedade de uma assinatura do Azure)

## <a name="need-help-contact-support"></a>Precisa de ajuda? Entre em contato com o suporte.

Se ainda tiver dúvidas, [entre em contato com o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) para resolver seu problema rapidamente.
