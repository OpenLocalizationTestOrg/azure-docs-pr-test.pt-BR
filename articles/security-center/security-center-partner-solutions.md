---
title: "soluções de parceiros de aaaManaging na Central de segurança do Azure | Microsoft Docs"
description: "Este documento orienta a como a Central de segurança do Azure permite que você monitor com um status de integridade de saudação rapidamente suas soluções de parceiros integrados com sua assinatura do Azure."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 70c076ef-3ad4-4000-a0c1-0ac0c9796ff1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: terrylan
ms.openlocfilehash: fc97aedf709b9044bfd3d4ecae0b58d5fa716bbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-partner-solutions-with-azure-security-center"></a>Monitoramento de soluções de parceiros com a Central de Segurança do Azure
Este documento o orienta como toomonitor Olá status de integridade de suas soluções de parceiros na Central de segurança do Azure.

> [!NOTE]
> Este documento apresenta serviço hello usando um exemplo de implantação. Este documento não é um guia passo a passo.
>
>

## <a name="monitoring-partner-solutions"></a>Monitoramento das soluções de parceiros
Olá **soluções de parceiros** bloco Olá **Central de segurança** permite folha monitorar em um status de integridade de saudação rapidamente suas soluções de parceiros que estão integradas com sua assinatura do Azure.

![Bloco Soluções de parceiros][1]

Olá **soluções de parceiros** lado a lado exibe o saudação várias soluções de parceiros integrados com sua assinatura. Se não houver nenhum soluções integradas, o bloco Olá exibe o número de Olá zero.

integridade de saudação tooview suas soluções de parceiros:

1. Selecione Olá **soluções de parceiros** lado a lado. Olá **soluções de parceiros** folha abre exibindo uma lista de suas soluções de parceiro conectado tooSecurity Center.

   ![Soluções de parceiros][3]

   saudação status de uma solução de parceiro pode ser:

   * Protegido (verde) - não há qualquer problema de integridade
   * Não íntegro (vermelho) - há um problema de integridade que requer atenção imediata
   * Parado reporting (laranja) - solução Olá parou a relatar sua integridade.
   * Status da proteção desconhecido (laranja) - integridade Olá de solução de saudação é desconhecido no momento devido tooa falhado o processo de adição de uma nova solução existente de toohello de recursos.
   * Não relatar (cinza) - solução de saudação não relatou qualquer coisa ainda, status de uma solução pode ser não relatados se recentemente foi conectado e ainda está sendo implantado.

2. Selecione uma solução de parceiro. Neste exemplo, permite que selecione Olá **Qualys** solução.  Uma folha abre mostrando recursos associados do status de saudação de solução de parceiro de saudação e solução de saudação. Selecione **console de solução** experiência de gerenciamento de parceiros de saudação tooopen para esta solução.

   ![Detalhes da solução de parceiro][4]
3. Voltar toohello **Qualys** folha e selecione **Link VM**. Olá **aplicativos de Link** folha é aberta. Aqui você pode conectar a solução de parceiro de toohello de recursos.

   ![Solução de toopartner de recursos do link][5]

## <a name="next-steps"></a>Próximas etapas
Neste documento, você foram introduzida toohello **soluções de parceiros** lado a lado na Central de segurança. toolearn mais sobre o Centro de segurança, consulte Olá artigos a seguir:

* [Definir políticas de segurança na Central de segurança do Azure](security-center-policies.md) — Saiba como tooconfigure as políticas de segurança para sua assinatura do Azure e grupos de recursos.
* [Gerenciando as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md) : saiba como as recomendações ajudam a proteger os recursos do Azure.
* [Monitoramento de integridade de segurança na Central de segurança do Azure](security-center-monitoring.md) — Saiba como toomonitor Olá a integridade de seus recursos do Azure.
* [Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md) — Saiba como alertas de toosecurity toomanage e responder.
* [Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md) — localizar perguntas frequentes sobre como usar o serviço de saudação.
* [Blog de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) — Obtenha notícias mais recentes de segurança do Azure hello e informações.

<!--Image references-->
[1]: ./media/security-center-partner-solutions/partner-solutions-tile.png
[3]: ./media/security-center-partner-solutions/partner-solutions.png
[4]: ./media/security-center-partner-solutions/partner-solutions-detail.png
[5]: ./media/security-center-partner-solutions/link-applications.png
