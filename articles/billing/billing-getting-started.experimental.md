---
title: "aaaPrevent inesperados custos, gerenciar cobrança - Azure | Microsoft Docs"
description: Saiba como tooavoid inesperados encargos na sua conta do Azure. Use recursos de gerenciamento e controle de custos para uma assinatura do Microsoft Azure.
services: 
documentationcenter: 
author: tonguyen10
manager: tonguyen
editor: 
tags: billing
ms.assetid: 482191ac-147e-4eb6-9655-c40c13846672
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/10/2017
ms.author: tonguyen
ms.openlocfilehash: d380f27861531351ac8e570469c59a84b9ca99e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="prevent-unexpected-charges-with-azure-billing-and-cost-management"></a>Evite cobranças inesperadas com o gerenciamento de custo e a cobrança do Azure

Quando você se inscrever para o Azure, há várias coisas que você pode fazer tooget uma ideia melhor dos seus gastos. Olá [Calculadora de preços](https://azure.microsoft.com/pricing/calculator/) pode fornecer uma estimativa de custos antes de criar um recurso do Azure. Olá [portal do Azure](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) fornece análise de custo atual hello e previsão para sua assinatura. Se você quiser toogroup e compreender os custos de diferentes projetos ou equipes, examine [marcação de recurso](../azure-resource-manager/resource-group-using-tags.md). Se sua organização tiver um sistema de relatórios que você prefere toouse, confira Olá [cobrança APIs](billing-usage-rate-card-overview.md). 

Você também pode [baixar após faturas e detalhes de arquivos de uso](billing-download-azure-invoice-daily-usage-date.md) toomake se houve cobrança corretamente. Para obter mais informações sobre como comparar seu uso diário com sua fatura, consulte [Entenda sua fatura do Microsoft Azure](billing-understand-your-bill.md).

Se sua assinatura através de um Enterprise Agreement (EA), provedor de solução de nuvem (CSP) ou os patrocinadores do Azure, em seguida, muitos recursos neste artigo não se aplicam tooyou. Em vez disso, temos um conjunto diferente de ferramentas que pode ser usado para o gerenciamento de custo. Consulte [Recursos adicionais do EA, CSP e Sponsorship](#other-offers).

Se sua assinatura for uma Avaliação Gratuita, do [Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/), do AIO (Azure via Open) ou BizSpark, sua assinatura será desativada automaticamente quando todos os créditos forem usados. Saiba mais sobre [os limites de gastos](#spending-limit) tooavoid com sua assinatura unexpectantly desabilitada. 

## <a name="get-estimated-costs-before-adding-azure-services"></a>Obter custos estimados antes de adicionar serviços do Azure

### <a name="estimate-cost-online-using-hello-pricing-calculator"></a>Estimar o custo online usando a Calculadora de preços de saudação

Check-out Olá [Calculadora de preços](https://azure.microsoft.com/pricing/calculator/) tooget um custo estimado mensal do serviço Olá você está interessado. Você pode adicionar qualquer tooget de recursos do Azure de terceiros primeiro uma estimativa de custo.

![Captura de tela da saudação menu Calculadora de preços](./media/billing-getting-started/pricing-calc.png)

Por exemplo, um A1 Windows Máquina Virtual (VM) é estimado toocost US $ 66.96/mês em horas de computação se deixá-lo executando o tempo todo hello:

![Captura de tela de Calculadora de preços Olá indicando que uma VM do Windows A1 estimado toocost US $ 66.96 por mês](./media/billing-getting-started/pricing-calcVM.png)

Para obter mais informações sobre preços, consulte estas [Perguntas frequentes](https://azure.microsoft.com/pricing/faq/). Ou, se você quiser tootalk tooan vendedor do Azure, entre em contato com 1-800-867-1389.

### <a name="review-hello-estimated-cost-in-hello-azure-portal"></a>Custo de saudação estimado de revisão em Olá portal do Azure

Normalmente quando você adiciona um serviço em Olá portal do Azure, há um modo de exibição que mostra um custo estimado semelhante por mês. Por exemplo, quando você escolhe o tamanho de saudação de VM do Windows, você ver Olá estimado custo mensal de horas de computação da saudação:

![Exemplo: uma VM do Windows A1 é estimado toocost US $ 66.96 por mês](./media/billing-getting-started/vm-size-cost.PNG)

### <a name="set-up-billing-alerts"></a>Configurar alertas de cobrança

Configure alertas de cobrança tooget emails quando os custos de uso excederam um valor que você especificar. Se você tiver créditos mensais, configure alertas para o uso de um valor especificado. Para obter mais informações, veja [Configurar alertas de cobrança para suas assinaturas do Microsoft Azure](billing-set-up-alerts.md).

![Captura de tela de um email de alerta de cobrança](./media/billing-getting-started/billing-alert.png)

> [!NOTE]
> Este recurso ainda está em visualização e,portanto, verifique seu uso regularmente.

Talvez você queira toouse Olá estimativa de custo da saudação Calculadora de preços como uma diretriz para o primeiro alerta.

### <a name="spending-limit"></a>Verifique se você tem um limite de gastos ativado

Se você tiver uma assinatura que usa créditos, em seguida, Olá limite de gastos é ativado para você por padrão. Dessa forma, quando você gasta todo o seu crédito, não há cobrança a mais no seu cartão de crédito. Consulte Olá [lista completa de ofertas do Azure e a disponibilidade de saudação do limite de gastos](https://azure.microsoft.com/support/legal/offer-details/).

No entanto, se você atingir o limite de gastos, os serviços serão desabilitados. Isso significa que suas VMs serão desalocadas. tooavoid o tempo de inatividade de serviço, você deve desativar Olá limite de gastos. O excedente é cobrado em seu cartão de crédito cadastrado. 

toosee se você já tem limite de gastos, vá toohello [exibir assinaturas no hello Centro de contas](https://account.windowsazure.com/Subscriptions). Uma faixa será exibida se o limite de gastos estiver ativo:

![Captura de tela que mostra um aviso sobre gastos limite sendo em Olá Centro de contas](./media/billing-getting-started/spending-limit-banner.PNG)

Clique em faixa hello e siga os prompts tooremove Olá limite de gastos. Se você não inseriu as informações de cartão de crédito quando você se inscreveu, você deve inserir Olá tooremove limite de gastos. Para obter mais informações, consulte [Azure limite de gastos – como ele funciona e como tooenable ou removê-lo](https://azure.microsoft.com/pricing/spending-limits/).

## <a name="ways-toomonitor-your-costs-when-using-azure-services"></a>Maneiras toomonitor os custos ao usar os serviços do Azure

### <a name="tags"></a>Adicionar marcas tooyour recursos toogroup seus dados de cobrança

Você pode usar dados de cobrança de toogroup marcas para serviços com suporte. Por exemplo, se você executar várias VMs para equipes diferentes, você pode usar marcas toocategorize custos por centro de custo (h, marketing, finanças) ou ambiente (teste de pré-produção, produção). 

![Captura de tela que mostra a configuração de marcas no portal de saudação](./media/billing-getting-started/tags.PNG)

marcas de saudação aparecem ao longo de custo diferente modos de exibição de relatório. Por exemplo, elas são visíveis logo no [modo de exibição de análise de custo](#costs) e no [. csv de uso detalhado](#invoice-and-usage) após o primeiro período de cobrança.

Para obter mais informações, consulte [usando marcas tooorganize seus recursos do Azure](../azure-resource-manager/resource-group-using-tags.md).

### <a name="costs"></a>Verifique o portal de saudação para análise de custo regularmente e taxa de gravação

Depois de colocar seus serviços em funcionamento, verifique regularmente quanto eles estão custando. Você pode ver Olá atual gastos e a taxa de gravação no portal do Azure. 

1. Visite Olá [folha de assinaturas no portal do Azure](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) e selecione uma assinatura.

2. Você deve ver a divisão de custo hello e taxa de gravação na folha de pop-up de saudação. Não podem ter suporte para a sua oferta (será exibido um aviso superior Olá).

    ![Captura de tela de taxa de gravação e divisão em Olá portal do Azure](./media/billing-getting-started/burn-rate.PNG)

3. Clique em **análise de custo** Olá lista toohello toosee esquerdo Olá divisão de custo por recurso. Aguarde 24 horas depois de adicionar um serviço para Olá toopopulate de dados.

    ![Captura de tela de exibição de análise de custo Olá no portal do Azure](./media/billing-getting-started/cost-analysis.PNG)

4. Você pode filtrar por propriedades diferentes, como [marcas](#tags), grupo de recursos e período de tempo. Clique em **aplicar** filtros de saudação tooconfirm e **baixar** se você quiser tooexport Olá exibição tooa Comma-Separated arquivo CSV (valores).

5. Além disso, você pode clicar em um recurso toosee gastar histórico e quanto recurso Olá custos de cada dia.

    ![Captura de tela de saudação gastar o modo de exibição de histórico no portal do Azure](./media/billing-getting-started/costhistory.PNG)

É recomendável que você verifique os custos de saudação que consulte estimativas Olá exibido quando você selecionou Olá serviços. Se os custos de saudação totalmente diferem das estimativas, verifique Olá plano de preços (A1 vs A0 VM, por exemplo) que você selecionou para os seus recursos. 

### <a name="consider-enabling-cost-cutting-features-like-auto-shutdown-for-vms"></a>Considere a possibilidade de habilitar recursos de redução de custos, como desligamento automático de VMs

Dependendo do cenário, você pode configurar o desligamento automático para suas VMs em Olá portal do Azure. Para saber mais, confira [Desligamento automático de máquinas virtuais usando o Azure Resource Manager](https://azure.microsoft.com/blog/announcing-auto-shutdown-for-vms-using-azure-resource-manager/).

![Captura de tela da opção de desligamento automático no portal de saudação](./media/billing-getting-started/auto-shutdown.PNG)

Desligamento automático não Olá mesmo que quando você desligar dentro Olá VM com as opções de energia. Autodesligamento interrompe e desaloca toostop suas VMs cobranças adicionais. Para saber mais, confira os estados de VM nas Perguntas frequentes sobre preços de [VMs Linux](https://azure.microsoft.com/pricing/details/virtual-machines/linux/) e [VMs Windows](https://azure.microsoft.com/pricing/details/virtual-machines/windows/).

Para obter mais recursos de redução de custos para os ambientes de desenvolvimento e teste, confira [Azure DevTest Labs](https://azure.microsoft.com/services/devtest-lab/).

### <a name="turn-on-and-check-out-azure-advisor-recommendations"></a>Habilitar e conferir as recomendações do Azure Advisor

[O Azure Advisor](../advisor/advisor-overview.md) é um recurso de visualização que ajuda a reduzir os custos identificando recursos com baixa utilização. Ative no hello portal do Azure:

![Captura de tela do botão Azure Advisor no portal do Azure](./media/billing-getting-started/advisor-button.PNG)

Em seguida, você pode obter recomendações viáveis Olá **custo** guia no painel de Supervisor hello:

![Captura de tela de exemplo de recomendação de custo do Advisor](./media/billing-getting-started/advisor-action.PNG)

Para saber mais, veja [Advisor Cost recommendations](../advisor/advisor-cost-recommendations.md) (Recomendações de custo do Advisor).

### <a name="billing-api"></a>API de Cobrança

Use nossos dados de uso get cobrança API tooprogrammatically. Use hello RateCard API e Olá API uso junto tooget seu uso cobrado. Para saber mais, confira [Obtenha informações sobre o consumo de recursos do Microsoft Azure](billing-usage-rate-card-overview.md).

## <a name="other-offers"></a> Casos especiais e recursos adicionais

### <a name="ea-csp-and-sponsorship-customers"></a>Clientes EA, CSP de patrocínio
Fale tooyour gerente de conta ou parceiro do Azure tooget iniciado.

| Oferta | Recursos |
|-------------------------------|-----------------------------------------------------------------------------------|
| EA (Enterprise Agreement) | [Portal EA](https://ea.azure.com/), [documentos de ajuda](https://ea.azure.com/helpdocs) e [relatório do Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-enterprise/) |
| Programa do CSP (Provedor de Soluções na Nuvem) | Fale tooyour provedor |
| Azure Sponsorship | [Portal do Sponsorship](https://www.microsoftazuresponsorships.com/) |

Se você estiver gerenciando IT para uma organização de grande porte, recomendamos a leitura [scaffold Azure enterprise](../azure-resource-manager/resource-manager-subscription-governance.md) e hello [enterprise TI white paper](http://download.microsoft.com/download/F/F/F/FFF60E6C-DBA1-4214-BEFD-3130C340B138/Azure_Onboarding_Guide_for_IT_Organizations_EN_US.pdf) (download. PDF, apenas em inglês).

### <a name="check-your-subscription-and-access"></a>Verificar assinatura e acesso

Exibindo custos exigem [informações do nível de assinaturas de acesso toobilling](billing-manage-access.md), mas Olá administrador da conta só pode acessar Olá [Centro de contas](https://account.windowsazure.com/Home/Index), altere as informações de cobrança e gerenciar assinaturas. Olá administrador da conta é a pessoa de saudação que passou pelo processo de inscrição de saudação. Para obter mais informações, consulte [adicionar ou alterar funções de administrador do Azure que gerenciam a assinatura de saudação ou serviços](billing-add-change-azure-subscription-administrator.md).

toosee se você estiver Olá administrador da conta, vá toohello [folha de assinaturas no portal do Azure de saudação](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) e examine a lista de saudação de assinaturas que você tem acesso ao. Procure **Minha Função**. Se estiver indicado *Administrador de conta*, tudo bem. Se estiver indicado *Proprietário*, você não tem todos os privilégios.

![Captura de tela de sua função na exibição de assinaturas no portal do Azure de saudação do hello](./media/billing-getting-started/sub-blade-view.PNG)

Se você não estiver Olá administrador da conta, alguém provavelmente dá acesso parcial via [controle de acesso baseado em função do Azure Active Directory](../active-directory/role-based-access-control-configure.md) (RBAC). toomanage assinaturas e alterar informações de cobrança [localizar Olá conta administrador](billing-subscription-transfer.md#whoisaa) e peça-lhes tarefas de saudação tooperform ou [transferir Olá assinatura tooyou](billing-subscription-transfer.md).

Se o administrador da conta não está mais com a sua organização e você precisar toomanage cobrança, [entre em contato com o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). 
## <a name="need-help-contact-support"></a>Precisa de ajuda? Contate o suporte

Se você precisar de Ajuda, [entre em contato com o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget seu problema resolvido rapidamente.
