---
title: "aaaTroubleshoot Azure problemas de inscrição | Microsoft Docs"
description: Descreve como tootroubleshoot alguns Azure comum inscrever problemas.
services: 
documentationcenter: 
author: JiangChen79
manager: adpick
editor: 
tags: billing,top-support-issue
ms.assetid: a0907da1-cb2d-41d1-a97f-43841fabe355
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: cjiang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ee649bfc3be7ba1fe2dd863fac09e1c2311d835b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-sign-up-issues-for-azure"></a>Solucionar problemas de inscrição do Azure
Se você não pode se inscrever para o Azure, use dicas de saudação em problemas comuns de tootroubleshoot neste artigo. Caso tenha um problema com seu cartão de crédito durante a inscrição, consulte [Seu cartão de débito ou crédito é recusado durante a inscrição do Azure](billing-credit-card-fails-during-azure-sign-up.md). Se você tiver uma conta do Azure, mas não pode entrar no, consulte [não consigo entrar toomanage minha assinatura do Azure](billing-cannot-login-subscription.md).

## <a name="progress-bar-hangs-in-identity-verification-by-card-section"></a>A barra de progresso trava na seção "Verificação de identidade por cartão"

verificação de identidade toocomplete Olá por cartão, cookies de terceiros devem ser permitidos para seu navegador.

![Captura de tela de verificação de identidade pela seção de cartão deslocado durante a inscrição de saudação](./media/billing-troubleshoot-azure-sign-up-issues/identity-verification-hangs.PNG)

As etapas a seguir do uso Olá tooupdate configurações de cookie do navegador.

1. Se você estiver usando o Chrome, vá muito**configurações** > **Mostrar configurações avançadas** > **privacidade** > **conteúdo configurações de**. Desmarque a opção **Bloquear cookies de terceiros e dados do site**.
2. Se você estiver usando borda, ir muito**configurações** > **visualizar configurações avançadas** > **Cookies**. Selecione **Não bloquear cookies**.
3. Atualizar Olá página de inscrição do Azure e verificar se o problema de saudação é resolvido.
4. Se a atualização de saudação não resolver o problema de Olá, feche e reinicie o navegador e tente novamente.

## <a name="credit-card-form-doesnt-support-my-billing-address"></a>O formulário de cartão de crédito não dá suporte ao meu endereço para cobrança
Seu endereço para cobrança precisa toobe no país Olá que você selecionou na Olá **sobre você** seção. Certifique-se de que selecionar o país correto hello.

## <a name="no-text-messages-or-calls-during-sign-up-account-verification"></a>Nenhuma mensagem de texto ou chamada durante a verificação da conta de inscrição
Enquanto ele é normalmente mais rápido, pode levar até toofour minutos para toobe de código de verificação entregues. Digite para verificação de número de telefone Olá não é armazenado como um número de contato para a conta de saudação.

Estas são algumas outras dicas:
* Um número de telefone VOIP não pode ser usado para o processo de verificação de telefone hello.
* Número de telefone de saudação Verifique inserir, incluindo o código do país Olá selecionado no menu suspenso de saudação.
* Se o seu telefone não recebe as mensagens de texto (SMS), tente Olá **telefonar para mim** opção.
* Verifique se o telefone pode receber chamadas ou mensagens SMS de um número dos Estados Unidos.

Quando você receber a mensagem de saudação do texto ou chamada telefônica, insira o código que você recebe na caixa de texto de saudação.

## <a name="credit-card-declined-or-not-accepted"></a>Cartão de crédito recusado ou não aceito
Cartões de crédito ou débito pré-pago ou virtuais não são aceitos como pagamentos de assinaturas do Azure. toosee o que mais pode causar o toobe cartão recusada, consulte [o débito ou um cartão de crédito é recusada Azure inscrição](billing-credit-card-fails-during-azure-sign-up.md).

## <a name="free-trial-is-not-available"></a>"A Avaliação Gratuita não está disponível"
Você já usou uma assinatura do Azure no hello anterior? Olá contrato de termos de uso do Azure limita a ativação da avaliação gratuita somente para um usuário que seja tooAzure novo. Se você já teve qualquer outro tipo de assinatura do Azure, não poderá ativar uma avaliação gratuita. Considere inscrever-se em uma [assinatura Pré-paga](https://azure.microsoft.com/offers/ms-azr-0003p/).

## <a name="i-saw-a-charge-on-my-free-trial-account"></a>Observei um encargo em minha conta de Avaliação Gratuita
Você pode ver uma pequena verificação manter sua conta de cartão de crédito após a inscrição, qual é removido dentro de 3 dias too5. Se estiver preocupado com o gerenciamento de custos, leia mais sobre como [evitar custos inesperados](https://docs.microsoft.com/azure/billing/billing-getting-started).

## <a name="cant-activate-azure-benefit-plan-like-msdn-bizspark-bizsparkplus-or-mpn"></a>Não consigo ativar um plano de benefícios do Azure, por exemplo, MSDN, BizSpark, BizSparkPlus ou MPN
Certifique-se de que você está usando entrada direita Olá credenciais. Marque Olá benefício do programa toomake-se de que você está qualificado. 

* MSDN
  * Verifique o status de qualificação na [página da sua conta MSDN](https://msdn.microsoft.com/subscriptions/manage/default.aspx).
  * Se você não pode verificar seu status, entre em contato com o hello [centros de serviço de cliente de assinaturas do MSDN](https://msdn.microsoft.com/subscriptions/contactus.aspx)
* BizSpark
  * Entrar toohello [BizSpark portal](https://www.microsoft.com/bizspark/default.aspx#start-two) e verificar o status de sua qualificação para BizSpark e BizSpark Plus.
  * Se você não pode verificar o status, você pode [obter ajuda nos fóruns de BizSpark Olá](http://aka.ms/bzforums).
* MPN
  * Entrar toohello [portal MPN](https://mspartner.microsoft.com/en/us/Pages/Locale.aspx) e verifique se o status de qualificação. Se você tiver Olá apropriado [competências de plataforma de nuvem](https://mspartner.microsoft.com/en/us/pages/membership/cloud-platform-competency.aspx), você pode estar qualificado para benefícios adicionais.
  * Se não conseguir verificar seu status, contate o [suporte do MPN](https://mspartner.microsoft.com/en/us/Pages/Support/Premium/contact-support.aspx).

## <a name="cant-activate-new-azure-in-open-subscription"></a>Não consigo ativar uma nova assinatura do Azure via Open
toocreate uma assinatura do Azure em aberto, você deve ter uma chave de ativação de serviço Online (OSA) válido com pelo menos um tooit de token associada do Azure em aberto. Se você não tiver uma chave OSA, contate um dos Parceiros da Microsoft listados no [Microsoft Pinpoint](http://pinpoint.microsoft.com/).

## <a name="need-help-contact-support"></a>Precisa de ajuda? Entre em contato com o suporte.
Se você ainda precisar de Ajuda, [entre em contato com o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget seu problema resolvido rapidamente.
