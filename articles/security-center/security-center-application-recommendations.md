---
title: "aaaProtecting seus aplicativos na Central de segurança do Azure | Microsoft Docs"
description: "Este documento endereça as recomendações na Central de Segurança do Azure que ajudam a proteger os recursos do Azure e cumprir as políticas de segurança."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: b5fc7a9e-24b1-415f-b3b5-62a53f5dd424
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/01/2016
ms.author: terrylan
ms.openlocfilehash: da5e02cc2bad55c64e4da14e4e10efd6ddeab39e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-your-applications-in-azure-security-center"></a>Protegendo seus aplicativos na Central de segurança do Azure
Central de segurança do Azure analisa o estado de segurança Olá seus recursos do Azure. Quando a Central de segurança identifica possíveis vulnerabilidades de segurança, ele cria recomendações que o guiam pelo processo de saudação de Configurando controles de saudação necessário.  Recomendações se aplicam a tipos de recurso tooAzure: máquinas virtuais (VMs), redes, aplicativos e SQL.

Este artigo aborda as recomendações que se aplicam a tooapplications.  As recomendações do aplicativo giram em torno da implantação de um firewall do aplicativo Web.  Uso tabela Olá abaixo como uma referência toohelp você entender o que faz cada uma se você aplicá-lo e recomendações de aplicativo disponível de saudação.

## <a name="available-application-recommendations"></a>Recomendações disponíveis do aplicativo
| Recomendações | Descrição |
| --- | --- |
| [Adicione um firewall do aplicativo Web](security-center-add-web-application-firewall.md) |Recomenda que você implante um WAF (firewall do aplicativo Web) para pontos de extremidade da Web. Uma recomendação WAF é mostrada para qualquer IP voltado para uso público (IP de nível de instância ou IP de balanceamento de carga) que tem um grupo de segurança de rede associado com portas de entrada da Web abertas (80,443).</br></br>Central de segurança recomenda que você provisionar um toohelp WAF se proteger contra ataques direcionados a seus aplicativos web em máquinas virtuais e no ambiente de serviço de aplicativo. Um ASE (Ambiente do Serviço de Aplicativo) é uma opção do plano de serviço [Premium](https://azure.microsoft.com/pricing/details/app-service/) do Serviço de Aplicativo do Azure que fornece um ambiente totalmente isolado e dedicado a executar com segurança os aplicativos do Serviço de Aplicativo do Azure. toolearn mais sobre ASE, consulte Olá [documentação do ambiente de serviço de aplicativo](../app-service/app-service-app-service-environments-readme.md).</br></br>Você pode proteger vários aplicativos web na Central de segurança adicionando esses aplicativos tooyour WAF as implantações existentes. |
| [Finalizar a proteção do aplicativo](security-center-add-web-application-firewall.md#finalize-application-protection) |configuração de saudação toocomplete de um WAF, o tráfego deve ser redirecionado toohello WAF dispositivo. Seguir essa recomendação conclui as alterações de configuração necessárias hello. |

## <a name="see-also"></a>Consulte também
toolearn mais informações sobre recomendações que se aplicam a tipos de recursos do Azure tooother, consulte Olá seguinte:

* [Protegendo suas máquinas virtuais na Central de Segurança do Azure](security-center-virtual-machine-recommendations.md)
* [Protegendo sua rede na Central de Segurança do Azure](security-center-network-recommendations.md)
* [Protegendo o serviço do SQL Azure na Central de Segurança do Azure](security-center-sql-service-recommendations.md)

toolearn mais sobre o Centro de segurança, consulte o seguinte hello:

* [Definir políticas de segurança na Central de segurança do Azure](security-center-policies.md) – Saiba como tooconfigure as políticas de segurança para sua assinatura do Azure e grupos de recursos.
* [Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md) – Saiba como alertas de toosecurity toomanage e responder.
* [Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md) – localizar perguntas frequentes sobre como usar o serviço de saudação.
