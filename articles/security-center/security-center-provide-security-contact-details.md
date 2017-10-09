---
title: "detalhes de contato de segurança aaaProvide na Central de segurança do Azure | Microsoft Docs"
description: "Este documento mostra como segurança tooprovide contatar detalhes na Central de segurança do Azure."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 26b5dcb4-ce3f-4f22-8d56-d2bf743cfc90
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 6c378c9c84c6e4fce70b2541e4cc121018700269
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="provide-security-contact-details-in-azure-security-center"></a>Fornecer detalhes de contato de segurança na Central de segurança do Azure
A Central de Segurança do Azure recomendará que você forneça detalhes de contato de segurança para sua assinatura do Azure se ainda não fez isso. Essa informação será usada pelo Microsoft toocontact se Olá Microsoft Security Response Center (MSRC) descobre que seu cliente tiver sido acessado por uma parte ilegal ou não autorizada. MSRC executa selecione segurança monitoramento de saudação rede do Azure e a infraestrutura e recebe reclamações abuso e de inteligência de ameaça de terceiros.

Uma notificação por email seja enviada na Olá primeiro diário ocorrência de um alerta e apenas para alertas de gravidade. As preferências de email só podem ser configuradas para políticas de assinatura. Grupos de recursos dentro de uma assinatura herdarão essas configurações.

> [!NOTE]
> Este documento apresenta serviço hello usando um exemplo de implantação.  Ela não é um guia passo a passo.
>
>

## <a name="implement-hello-recommendation"></a>Implementar a recomendação de saudação
1. Em Olá **recomendações** folha, selecione **fornecer detalhes de contato de segurança**.
   ![Fornecer contato de segurança][1]
2. Isso abre a folha de saudação **fornecer detalhes de contato de segurança**. Selecione informações de contato tooprovide do hello assinatura do Azure.
   ![Fornecer detalhes de contato de segurança][2]
3. Uma segunda folha **Fornecer detalhes de contato de segurança** será aberta.

   * Insira o endereço de email de contato de segurança hello ou endereços separados por vírgulas. Não é um número de toohello limite de endereços de email que você pode inserir.
   * Insira um número de telefone internacional de contato de segurança.
   * tooreceive emails sobre alertas de gravidade, ative a opção de saudação **enviar-me emails sobre alertas**.
   * Olá futuro, você terá os proprietários de toosubscription de notificações de email toosend de opção hello. Esta opção está esmaecida no momento.
   * Selecione **Okey** tooapply segurança de saudação entre em contato com assinatura de tooyour de informações.

## <a name="see-also"></a>Consulte também
toolearn mais sobre o Centro de segurança, consulte o seguinte hello:

* [Definir políticas de segurança na Central de segurança do Azure](security-center-policies.md) – Saiba como tooconfigure as políticas de segurança para sua assinatura do Azure e grupos de recursos.
* [Gerenciar as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md) : saiba como as recomendações ajudam a proteger os recursos do Azure.
* [Monitoramento de integridade de segurança na Central de segurança do Azure](security-center-monitoring.md) – Saiba como toomonitor Olá a integridade de seus recursos do Azure.
* [Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md) – Saiba como alertas de toosecurity toomanage e responder.
* [Soluções de parceiro com a Central de segurança do Azure de monitoramento](security-center-partner-solutions.md) – Saiba como toomonitor Olá status de integridade de suas soluções de parceiro.
* [Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md) – localizar perguntas frequentes sobre como usar o serviço de saudação.
* [Blog de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) – obter notícias mais recentes de segurança do Azure hello e informações.

<!--Image references-->
[1]: ./media/security-center-provide-security-contacts/provide-contacts.png
[2]:./media/security-center-provide-security-contacts/provide-contact-details.png
