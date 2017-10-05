---
title: "Corrigir as vulnerabilidades do sistema operacional na Central de Segurança do Azure | Microsoft Docs"
description: "Este documento mostra como implementar a recomendação da Central de Segurança do Azure para **Corrigir as vulnerabilidades do sistema operacional**."
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
ms.openlocfilehash: e6b251d5b97c57b3b6f79d14e53fbed5ca37ecb0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="remediate-os-vulnerabilities-in-azure-security-center"></a>Corrigir as vulnerabilidades do sistema operacional na Central de Segurança do Azure
Diariamente, a Central de Segurança do Azure analisa as configurações do sistema operacional (SO) da sua máquina virtual (VM) que podem tornar a VM mais vulnerável a ataques e recomenda as alterações de configuração para corrigir essas vulnerabilidades. A Central de Segurança recomenda que você resolva as vulnerabilidades quando a configuração do SO da VM não seguir as regras de configuração recomendadas.

> [!NOTE]
> Para obter mais informações sobre configurações específicas que estão sendo monitoradas, consulte a [lista de regras de configuração recomendadas](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).
>
>

## <a name="implement-the-recommendation"></a>Implementar a recomendação

> [!NOTE]
> Este documento apresenta o serviço usando uma implantação de exemplo.  Este documento não é um guia passo a passo.
>
>

1. Na folha **Recomendações**, selecione **Corrigir vulnerabilidades do SO**.
   ![Corrigir as vulnerabilidades do sistema operacional][1]

    A folha **Corrigir vulnerabilidades do SO** abre e lista as VMs que tenham configurações de SO que não seguem as regras de configuração recomendadas.  Para cada VM, a folha identifica:

   * **REGRAS COM FALHAS** -- o número de regras de configuração que o SO da VM não segue.
   * **HORA DA ÚLTIMA VERIFICAÇÃO** -- a data e a hora em que a Central de Segurança verificou pela última vez a configuração do SO da VM.
   * **ESTADO** --- o estado atual da vulnerabilidade:

     * Aberta: a vulnerabilidade ainda não foi corrigida
     * Em andamento: a vulnerabilidade está sendo corrigida; não é exigido que você realize nenhuma ação
     * Resolvida: a vulnerabilidade já foi corrigida (quando o problema for resolvido, a entrada será esmaecida)
   * **GRAVIDADE** -- Todas as vulnerabilidades são definidas com uma gravidade Baixa, o que significa que a vulnerabilidade deve ser corrigida, mas não exige atenção imediata.

2. Selecionar uma máquina virtual. Uma folha dessa VM é aberta e exibe as regras que falharam.
   ![Regras de configuração que falharam][2]

3. Selecione uma regra. Neste exemplo, você pode selecionar **A senha deve atender a requisitos de complexidade**. Uma folha será aberta descrevendo a regra com falha e o impacto. Examine os detalhes e considere como as configurações do sistema operacional são aplicadas.
  ![Descrição da regra com falha][3]

  A Central de Segurança usa a Common Configuration Enumeration (CCE) para atribuir identificadores exclusivos para as regras de configuração. As informações a seguir são fornecidas nessa folha:

  - NOME -- o nome da regra
  - GRAVIDADE -- valor de gravidade da CCE de crítico, importante ou aviso
  - CCIED -- identificador exclusivo da CCE para a regra
  - DESCRIÇÃO -- a descrição da regra
  - VULNERABILIDADE -- explicação da vulnerabilidade ou do risco se a regra não for aplicada
  - IMPACTO -- o impacto nos negócios quando a regra é aplicada
  - VALOR ESPERADO -- o valor esperado quando a Central de Segurança analisa a configuração do SO da VM em relação à regra
  - OPERAÇÃO DA REGRA -- a operação da regra usada pela Central de Segurança durante a análise da configuração do SO da VM em relação à regra
  - VALOR REAL -- o valor retornado após a análise da configuração do SO da VM em relação à regra
  - RESULTADO DA AVALIAÇÃO -- o resultado da análise: Aprovado, Falha

## <a name="see-also"></a>Consulte também
Este artigo mostrou como implementar a recomendação da Central de Segurança para "Corrigir vulnerabilidades do sistema operacional". Você pode conferir o conjunto de regras de configuração [aqui](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335). A Central de Segurança usa a Common Configuration Enumeration (CCE) para atribuir identificadores exclusivos para as regras de configuração. Visite o site da [CCE](https://nvd.nist.gov/cce/index.cfm) para obter mais informações.

Para saber mais sobre a Central de Segurança, confira os seguintes recursos:

* [Plataformas com suporte na Central de Segurança do Azure](security-center-os-coverage.md) – fornece uma lista de VMs Windows e Linux com suporte.
* [Configurando políticas de segurança na Central de Segurança do Azure](security-center-policies.md): saiba como configurar políticas de segurança para suas assinaturas e grupos de recursos do Azure.
* [Gerenciar as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md): saiba como as recomendações ajudam a proteger os recursos do Azure.
* [Monitoramento da integridade de segurança na Central de Segurança do Azure](security-center-monitoring.md): saiba como monitorar a integridade dos recursos do Azure.
* [Gerenciando e respondendo a alertas de segurança na Central de Segurança do Azure](security-center-managing-and-responding-alerts.md): aprenda a gerenciar e responder aos alertas de segurança.
* [Monitorando as soluções de parceiros com a Central de Segurança do Azure](security-center-partner-solutions.md) – saiba como monitorar o status de integridade de suas soluções de parceiros.
* [Perguntas frequentes sobre a Central de Segurança do Azure](security-center-faq.md): encontre as perguntas frequentes sobre como usar o serviço.
* [Blog de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/): encontre postagens no blog sobre conformidade e segurança do Azure.

<!--Image references-->
[1]: ./media/security-center-remediate-os-vulnerabilities/recommendation.png
[2]:./media/security-center-remediate-os-vulnerabilities/vm-remediate-os-vulnerabilities.png
[3]: ./media/security-center-remediate-os-vulnerabilities/vulnerability-details.png
