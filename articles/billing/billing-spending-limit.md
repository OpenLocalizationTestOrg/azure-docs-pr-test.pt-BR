---
title: limite de gastos do Azure de aaaUnderstand | Microsoft Docs
description: Descreve como funciona de limite de gastos do Azure e tooremove-lo
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: genli
ms.openlocfilehash: ed01401a07c3d0e7edebe42fb1482b7b60b1df51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-spending-limit-and-how-tooremove-it"></a>Entender o limite de gastos do Azure e como tooremove-lo

O limite de gastos do Azure representa o quanto sua assinatura do Azure pode gastar. Todos os novos clientes que inscreverem-se para a oferta de avaliação de saudação ou ofertas que inclui os créditos em vários meses têm Olá ativado por padrão de limite de gastos. saudação de limite de gastos é $0. Isso não pode ser alterado. limite de gastos de saudação não está disponível para tipos de assinatura, como assinaturas de pré-pago e panos de compromisso. Consulte Olá [lista completa de ofertas do Azure e a disponibilidade de saudação do limite de gastos de saudação](https://azure.microsoft.com/support/legal/offer-details/).

## <a name="what-happens-when-i-reach-hello-spending-limit"></a>O que acontece quando eu alcançar o limite de gastos de saudação?

Quando seu uso resulta em encargos que utilize Olá quantidade mensal incluída na sua oferta, serviços de saudação implantado estão desabilitados para o restante de saudação do mês de cobrança. Por exemplo, os Serviços de Nuvem implantados são removidos do ambiente de produção, e suas máquinas virtuais do Azure são interrompidas e desalocadas. tooprevent seus serviços sejam desativados, você pode escolher tooremove seu limite de gastos. Quando os serviços estiverem desativados, dados de saudação em suas contas de armazenamento e bancos de dados estão disponíveis em um modo somente leitura para os administradores. Olá começo da saudação próximo mês de cobrança, se sua oferta inclui créditos em vários meses, sua assinatura será habilitada novamente. Em seguida, você pode reimplantar seus serviços de nuvem e tem bancos de dados e contas de armazenamento tooyour acesso completo.

Depois que a assinatura de avaliação gratuita Olá atinge Olá limite de gastos, você pode reabilitar Olá assinatura e que ele seja automaticamente [oferta pré-pagas padrão de atualização tooour](billing-upgrade-azure-subscription.md) dentro de 90 dias.

Você recebe notificações quando você atinge o limite de gastos para sua oferta de saudação. Faça logon no toohello [Centro de contas Azure](https://account.windowsazure.com), selecione **conta**e, em seguida, selecione **assinaturas**. Você verá as notificações sobre assinaturas que atingiram o limite de gastos de saudação.

## <a name="things-you-are-charged-for-even-if-you-have-a-spending-limit-enabled"></a>Coisas pelas quais você é cobrado mesmo que esteja com um limite de gastos habilitado

Alguns serviços do Azure e [compras no Marketplace](https://azure.microsoft.com/marketplace/) pode incorrer encargos no método de pagamento da saudação (CC) mesmo se um limite de gastos é definido. Os exemplos são licenças do Visual studio, Active Directory do Azure premium, planos de suporte e a maioria dos softwares de terceiros serviços vendidos pela Olá Marketplace com a marca.


## <a name="when-not-toouse-hello-spending-limit"></a>Quando não toouse Olá limite de gastos

limite de gastos de saudação pode impedir que você implantar ou usar determinados marketplace e serviços da Microsoft. Aqui estão os cenários de saudação onde você deve remover Olá limite de gastos em sua assinatura.

- Planejar toodeploy primeiras imagens de terceiros como Oracle e serviços como o Visual Studio Team Services. Este cenário faz com que você tooexceed seu limite de gastos quase imediatamente e faz com que seu toobe assinatura desabilitada.

- Você tem serviços que não podem ser interrompidos.

- Serviços e recursos com configurações, como endereços de IP virtual que você não deseja toolose. Essas configurações são perdidas quando Olá serviços e recursos são desalocados.


## <a name="remove-hello-spending-limit"></a>Remover limite de gastos de saudação

Você pode remover Olá gastos limite a qualquer momento, como há um método de pagamento válido associado à sua assinatura. Para obter ofertas que tem crédito nos vários meses, você também pode habilitar novamente Olá limite de gastos no início de saudação do seu próximo ciclo de cobrança.

tooremove seu limite de gastos, siga estas etapas:

1. Faça logon no toohello [Centro de contas Azure](https://account.windowsazure.com).

2. Selecione uma assinatura.

3. Se a assinatura de saudação é desabilitada devido toohello limite de gastos seja atingido, clique nesta notificação: "Assinatura atingiu o limite de gastos de saudação e foi desabilitado tooprevent encargos." Caso contrário, clique em **remover limite de gastos** em Olá **STATUS da assinatura** área.

4. Selecione uma opção que é adequada para você.

|Opção|Efeito|
|-------|-----|
|Remover o limite de gastos indefinidamente|Remove o limite de gasto sem ativá-lo automaticamente no início de saudação do hello próximo período de cobrança de saudação.|
|Remover limite de gastos para Olá atual período de cobrança|Remove o limite de gastos para que ele ativa novamente automaticamente no início de saudação do hello próximo período de cobrança de saudação.|

## <a name="need-help-contact-support"></a>Precisa de ajuda? Entre em contato com o suporte.
Se você ainda precisar de Ajuda, [entre em contato com o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget seu problema resolvido rapidamente.
