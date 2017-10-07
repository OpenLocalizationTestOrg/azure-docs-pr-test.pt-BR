---
title: "alertas de integridade de proteção de ponto de extremidade de aaaResolve na Central de segurança do Azure | Microsoft Docs"
description: "Este documento mostra como tooimplement Olá recomendação da Central de segurança do Azure * * resolver Endpoint Protection integridade alertas * *."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 4050f453-98fc-4314-8438-d476469757fb
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/01/2016
ms.author: terrylan
ms.openlocfilehash: 9631d15aa1dfa9003d56332363ae7911061ed0b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-endpoint-protection-health-alerts-in-azure-security-center"></a>Resolver alertas de integridade do Endpoint Protection na Central de segurança do Azure
A Central de Segurança do Azure recomendará que você resolva os alertas de integridade do Endpoint Protection detectados.  Central de segurança permite que você toosee quais máquinas virtuais (VMs) têm falhas de proteção de ponto de extremidade e quantos.

> [!NOTE]
> Este documento apresenta serviço hello usando um exemplo de implantação. Ela não é um guia passo a passo.
> 
> 

## <a name="implement-hello-recommendation"></a>Implementar a recomendação de saudação
1. Em Olá **folha recomendações**, selecione **alertas de integridade de proteção de ponto de extremidade resolver**.
   ![Resolver alertas de integridade de proteção do ponto de extremidade][1]
2. Isso abre a folha de saudação **Falha na proteção de ponto de extremidade** que lista as máquinas virtuais com falhas e Olá número de falhas para cada VM. Selecione uma VM na lista de saudação.
   ![Endpoint protection failure][2]
3. Um **falhas lista** folha abre Olá selecionada de VM, exibindo uma lista de falhas. Selecione uma falha de saudação lista toolearn mais. Isso abrirá uma folha com informações sobre a falha de saudação selecionada.
   ![Lista de falhas][3]
   ![Eventos de falha][4]

## <a name="see-also"></a>Consulte também
toolearn mais sobre o Centro de segurança, consulte o seguinte hello:

* [Definir políticas de segurança na Central de segurança do Azure](security-center-policies.md)– Saiba como tooconfigure as políticas de segurança para sua assinatura do Azure e grupos de recursos.
* [Gerenciar as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md): saiba como as recomendações ajudam a proteger os recursos do Azure.
* [Monitoramento de integridade de segurança na Central de segurança do Azure](security-center-monitoring.md)– Saiba como toomonitor Olá a integridade de seus recursos do Azure.
* [Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md)– Saiba como alertas de toosecurity toomanage e responder.
* [Soluções de parceiro com a Central de segurança do Azure de monitoramento](security-center-partner-solutions.md) – Saiba como toomonitor Olá status de integridade de suas soluções de parceiro.
* [Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md)– localizar perguntas frequentes sobre como usar o serviço de saudação.
* [Blog de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/)– obter notícias mais recentes de segurança do Azure hello e informações.

<!--Image references-->
[1]: ./media/security-center-resolve-endpoint-protection/resolve-endpoint-protection.png
[2]: ./media/security-center-resolve-endpoint-protection/endpoint-protection-failure.png
[3]: ./media/security-center-resolve-endpoint-protection/failure-list.png
[4]: ./media/security-center-resolve-endpoint-protection/failure-event.png
