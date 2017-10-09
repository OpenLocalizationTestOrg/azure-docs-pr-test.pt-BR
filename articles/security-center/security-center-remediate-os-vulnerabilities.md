---
title: "vulnerabilidades aaaRemediate SO na Central de segurança do Azure | Microsoft Docs"
description: "Este documento mostra como tooimplement Olá recomendação da Central de segurança do Azure * * OS corrigir vulnerabilidades * *."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 991d41f5-1d17-468d-a66d-83ec1308ab79
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 704103f7fb15835943d74b665d2bd56cb5e0a36d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="remediate-os-vulnerabilities-in-azure-security-center"></a>Corrigir as vulnerabilidades do sistema operacional na Central de Segurança do Azure
Central de segurança do Azure diariamente analisa o sistema de operacional de máquina virtual (VM) (SO) para as configurações que podem fazer Olá VM alterações de configuração de tooattack e recomenda mais vulnerável tooaddress essas vulnerabilidades. Central de segurança recomenda que você resolver vulnerabilidades quando configuração do sistema operacional da VM não corresponde a saudação recomendada regras de configuração.

> [!NOTE]
> Para obter mais informações sobre configurações específicas de saudação que estão sendo monitorados, consulte Olá [lista de regras de configuração recomendada](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).
>
>

## <a name="implement-hello-recommendation"></a>Implementar a recomendação de saudação

> [!NOTE]
> Este documento apresenta serviço hello usando um exemplo de implantação.  Este documento não é um guia passo a passo.
>
>

1. Em Olá **recomendações** folha, selecione **vulnerabilidades do sistema operacional corrigir**.
   ![Corrigir as vulnerabilidades do sistema operacional][1]

    Olá **vulnerabilidades do sistema operacional corrigir** folha é aberta e lista suas VMs com configurações de sistema operacional que não correspondem a saudação recomendada regras de configuração.  Para cada VM, folha Olá identifica:

   * **REGRAS de falha** -Olá número de regras que Olá a configuração do sistema operacional da VM com falha.
   * **HORA da última verificação** - date de hello e o tempo que a Central de segurança verificado pela última vez configuração do sistema operacional da VM hello.
   * **ESTADO** -Olá o estado atual da vulnerabilidade hello:

     * Abrir: vulnerabilidade Olá não tratada ainda
     * Em andamento: Vulnerabilidade hello está sendo aplicada no momento, nenhuma ação é necessária por você
     * Resolvido: vulnerabilidade Olá já foi abordada (quando Olá problema terá sido resolvido, entrada hello está esmaecida)
   * **SEVERIDADE** – todas as vulnerabilidades são definidas tooa severidade baixa, indicando uma vulnerabilidade deve ser resolvida, mas não exigem atenção imediata.

2. Selecionar uma máquina virtual. Uma folha para que o VM abre e exibe as regras de saudação que falharam.
   ![Regras de configuração que falharam][2]

3. Selecione uma regra. Neste exemplo, você pode selecionar **A senha deve atender a requisitos de complexidade**. Uma folha abre descrevendo impacto de regra e Olá Olá falhado. Examine os detalhes de saudação e considere como são aplicadas as configurações do sistema operacional.
  ![Descrição para a regra com falha Olá][3]

  Central de segurança usa identificadores exclusivos de tooassign de enumeração de configuração comuns (CCE) para as regras de configuração. Olá informações a seguir é fornecida nesta folha:

  - NOME -- o nome da regra
  - GRAVIDADE -- valor de gravidade da CCE de crítico, importante ou aviso
  - CCIED – Identificador exclusivo CCE para regra de saudação
  - DESCRIÇÃO -- a descrição da regra
  - VULNERABILIDADE -- explicação da vulnerabilidade ou do risco se a regra não for aplicada
  - IMPACTO -- o impacto nos negócios quando a regra é aplicada
  - VALOR esperado – Valor esperado quando a Central de segurança analisa sua configuração de sistema operacional da VM em relação a regra de saudação
  - – REGRA regra operação usada pela Central de segurança durante a análise da configuração do sistema operacional da VM em relação a regra de saudação
  - VALOR real – O valor retornado após a análise da configuração do sistema operacional da VM em relação a regra de saudação
  - RESULTADO DA AVALIAÇÃO -- o resultado da análise: Aprovado, Falha

## <a name="see-also"></a>Consulte também
Este artigo lhe mostrou como tooimplement Olá Central de segurança recomendação "corrigir OS vulnerabilidades." Você pode examinar o conjunto de saudação de regras de configuração [aqui](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335). Central de segurança usa identificadores exclusivos de tooassign CCE (Common Configuration Enumeration) para as regras de configuração. Visite Olá [CCE](https://nvd.nist.gov/cce/index.cfm) site para obter mais informações.

toolearn mais sobre o Centro de segurança, consulte Olá recursos a seguir:

* [Plataformas com suporte na Central de Segurança do Azure](security-center-os-coverage.md) – fornece uma lista de VMs Windows e Linux com suporte.
* [Definir políticas de segurança na Central de segurança do Azure](security-center-policies.md) -Saiba como tooconfigure as políticas de segurança para sua assinatura do Azure e grupos de recursos.
* [Gerenciar as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md): saiba como as recomendações ajudam a proteger os recursos do Azure.
* [Monitoramento de integridade de segurança na Central de segurança do Azure](security-center-monitoring.md) -Saiba como toomonitor Olá a integridade de seus recursos do Azure.
* [Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md) -Saiba como alertas de toosecurity toomanage e responder.
* [Soluções de parceiro com a Central de segurança do Azure de monitoramento](security-center-partner-solutions.md) -Saiba como toomonitor Olá status de integridade de suas soluções de parceiro.
* [Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md) -perguntas frequentes sobre como usar o serviço de saudação de localizar.
* [Blog de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/): encontre postagens no blog sobre conformidade e segurança do Azure.

<!--Image references-->
[1]: ./media/security-center-remediate-os-vulnerabilities/recommendation.png
[2]:./media/security-center-remediate-os-vulnerabilities/vm-remediate-os-vulnerabilities.png
[3]: ./media/security-center-remediate-os-vulnerabilities/vulnerability-details.png
