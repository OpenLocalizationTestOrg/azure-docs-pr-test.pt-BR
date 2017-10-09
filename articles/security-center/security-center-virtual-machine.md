---
title: "aaaAzure Central de segurança e máquinas virtuais do Azure | Microsoft Docs"
description: "Este documento ajuda toounderstand como Central de segurança do Azure pode proteger você máquinas virtuais do Azure."
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 5fe5a12c-5d25-430c-9d47-df9438b1d7c5
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/24/2017
ms.author: yurid
ms.openlocfilehash: d5e80e9341263a57f3100cb032a066f037e913a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-and-azure-virtual-machines"></a>Central de Segurança do Azure e Máquinas Virtuais do Azure
[Central de segurança do Azure](https://azure.microsoft.com/services/security-center/) ajuda a evitar, detectar e responder toothreats. Ela permite o gerenciamento de políticas e o monitoramento da segurança integrada entre suas assinaturas do Azure, ajuda a detectar ameaças que poderiam passar despercebidas e funciona com uma enorme variedade de soluções de segurança.

Este artigo mostra como a Central de Segurança pode ajudá-lo a proteger suas VMs (Máquinas Virtuais) do Azure.

## <a name="why-use-security-center"></a>Por que usar a Central de Segurança?
A Central de Segurança ajuda a proteger os dados de máquinas virtuais no Azure, fornecendo visibilidade para configurações de segurança da máquina virtual. Quando a Central de segurança protege suas VMs, Olá recursos a seguir estarão disponível:

* Configurações de segurança do sistema operacional (SO) com hello recomendado regras de configuração
* Segurança do sistema e atualizações críticas que estão ausentes
* Recomendações de proteção de ponto de extremidade
* Validação de criptografia de disco
* Avaliação de vulnerabilidade e remediação
* Detecção de ameaças

Além disso toohelping proteger suas VMs do Azure, Central de segurança também fornece monitoramento de segurança e gerenciamento de serviços de nuvem, serviços de aplicativos, redes virtuais e muito mais. 

> [!NOTE]
> Consulte [tooAzure Introdução a Central de segurança](security-center-intro.md) toolearn mais sobre o Centro de segurança do Azure.
> 
> 

## <a name="prerequisites"></a>Pré-requisitos
tooget iniciado com a Central de segurança do Azure, você precisa tooknow e considere Olá seguinte:

* Você deve ter um tooMicrosoft de assinatura do Azure. Confira [Preços da Central de Segurança](https://azure.microsoft.com/pricing/details/security-center/) para obter mais informações sobre as camadas gratuitas e padrão da Central de Segurança.
* Planejar a adoção da Central de segurança, consulte [guia de planejamento e operações da Central de segurança do Azure](security-center-planning-and-operations-guide.md) toolearn mais informações sobre considerações de planejamento e operações.
* Para obter informações sobre suporte do sistema operacional, confira [FAQ (Perguntas Frequentes) sobre a Central de Segurança do Azure](security-center-faq.md). 

## <a name="set-security-policy"></a>Definir políticas de segurança
Toobe de necessidades de coleção de dados habilitado para que esse centro de segurança do Azure pode coletar informações de saudação precisa tooprovide recomendações e os alertas gerados com base na política de segurança de saudação configurados. Na Figura Olá abaixo, você pode ver que **coleta de dados** foi ativado **em**.

Uma política de segurança define o conjunto de saudação de controles que são recomendados para recursos em Olá especificado assinatura ou grupo de recursos. Antes de habilitar a política de segurança, você deve ter habilitada a coleta de dados, a Central de segurança coleta dados de suas máquinas virtuais na ordem tooassess seu estado de segurança, forneça recomendações de segurança e alertá-lo toothreats. Central de segurança, você define para suas assinaturas do Azure ou grupos de recursos da empresa tooyour as necessidades de segurança e tipo de saudação de aplicativos ou confidencialidade dos dados de saudação em cada assinatura de acordo com as políticas. 

![Política de segurança](./media/security-center-virtual-machine/security-center-virtual-machine-fig1.png)

> [!NOTE]
> toolearn mais sobre cada **política de prevenção de** disponível, consulte [definir políticas de segurança](security-center-policies.md) artigo.
> 
> 

## <a name="manage-security-recommendations"></a>Gerenciar recomendações de segurança
Central de segurança analisa o estado de segurança Olá seus recursos do Azure. Quando a Central de Segurança identifica possíveis vulnerabilidades de segurança, cria recomendações. recomendações de saudação orientará você durante processo de saudação do configurando controles de saudação necessário.

Depois de definir uma política de segurança, Central de segurança analisa o estado de segurança Olá seus recursos tooidentify as vulnerabilidades potenciais. recomendações de saudação são mostradas em um formato de tabela em que cada linha representa uma recomendação específica. Olá tabela a seguir fornece alguns exemplos de recomendações para máquinas virtuais do Azure e o que cada um deles será feito se você aplicá-lo. Quando você seleciona uma recomendação, você receberá informações que mostra como tooimplement Olá recomendação na Central de segurança.

| Recomendações | Descrição |
| --- | --- |
| [Habilitar coleta de dados para assinaturas](security-center-enable-data-collection.md) |Recomenda-se de que você ativar a coleta de dados na política de segurança Olá para cada uma das suas assinaturas e todas as máquinas virtuais (VMs) em suas assinaturas. |
| [Corrigir as vulnerabilidades do sistema operacional](security-center-remediate-os-vulnerabilities.md) |Recomenda que você a alinhar as configurações do sistema operacional com hello recomendado regras de configuração, por exemplo, não permitem toobe senhas salva. |
| [Aplicar atualizações do sistema](security-center-apply-system-updates.md) |Recomenda que você implante tooVMs atualizações críticas e segurança de sistema ausente. |
| [Reinicializar após as atualizações do sistema](security-center-apply-system-updates.md#reboot-after-system-updates) |Recomenda que você reinicialize um processo de saudação do VM toocomplete de aplicação de atualizações do sistema. |
| [Instalar proteção do ponto de extremidade](security-center-install-endpoint-protection.md) |Recomenda-se de que você forneça antimalware programas tooVMs (VMs do Windows somente). |
| [Resolver alertas de integridade do Endpoint Protection](security-center-resolve-endpoint-protection-health-alerts.md) |Recomenda que você resolva falhas do Endpoint Protection. |
| [Habilitar o Agente de VM](security-center-enable-vm-agent.md) |Permite que você toosee que exigem VMs Olá agente de VM. Olá VM Agent deve ser instalado em máquinas virtuais no patch tooprovision de ordem de varredura, verificação de linha de base e os programas antimalware. Olá agente VM é instalado por padrão para VMs que são implantados de saudação do Azure Marketplace. artigo Olá [agente de VM e extensões – parte 2](http://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/) fornece informações sobre como tooinstall Olá agente de VM. |
| [Aplicar a criptografia de disco](security-center-apply-disk-encryption.md) |Recomenda de que você criptografe os discos de VM usando o Azure Disk Encryption (VMs do Windows e do Linux). Criptografia é recomendada para Olá SO e os volumes de dados na sua VM. |
| [Avaliação de vulnerabilidade não instalada](security-center-vulnerability-assessment-recommendations.md) |Recomenda que você instale uma solução de avaliação de vulnerabilidade na VM. |
| [Corrigir vulnerabilidades](security-center-vulnerability-assessment-recommendations.md#review-the-recommendation) |Permite que você toosee sistema e do aplicativo vulnerabilidades detectadas pela solução de avaliação de vulnerabilidade Olá instalada na sua VM. |

> [!NOTE]
> toolearn mais informações sobre recomendações, consulte [Gerenciando recomendações de segurança](security-center-recommendations.md) artigo.
> 
> 

## <a name="monitor-security-health"></a>Monitorar integridade da segurança
Depois de habilitar [políticas de segurança](security-center-policies.md) para recursos de uma assinatura, a Central de segurança analisará segurança Olá das vulnerabilidades potenciais tooidentify recursos.  Você pode exibir o estado de segurança de saudação de seus recursos, junto com os problemas no hello **integridade da segurança do recurso** folha. Quando você clica em **máquinas virtuais** em Olá **segurança do recurso** bloco de integridade, Olá **máquinas virtuais** folha será aberta com recomendações para suas VMs. 

![Integridade da segurança](./media/security-center-virtual-machine/security-center-virtual-machine-fig2.png)

## <a name="manage-and-respond-toosecurity-alerts"></a>Gerenciar e responder a alertas de toosecurity
Central de segurança automaticamente coleta, analisa e integra dados de log de seus recursos do Azure, rede hello e soluções de parceiros conectado (como o firewall e o ponto de extremidade soluções de proteção), ameaças reais toodetect e reduzir falsos positivos. Utilizando uma agregação diferentes de [recursos de detecção](security-center-detection-capabilities.md), Central de segurança é capaz de toogenerate priorizada alertas de segurança toohelp investigar o problema hello e fornecer recomendações sobre como rapidamente tooremediate ataques possíveis.

![Alertas de segurança](./media/security-center-virtual-machine/security-center-virtual-machine-fig3.png)

Selecione um toolearn de alerta de segurança mais sobre o evento Olá que disparou o alerta hello e, se houver, etapas que você precisam tootake tooremediate um ataque. Os alertas de segurança são agrupados por [tipo](security-center-alerts-type.md) e data.

## <a name="see-also"></a>Consulte também
toolearn mais sobre o Centro de segurança, consulte o seguinte hello:

* [Definir políticas de segurança na Central de segurança do Azure](security-center-policies.md) – Saiba como tooconfigure as políticas de segurança para sua assinatura do Azure e grupos de recursos.
* [Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md) – Saiba como alertas de toosecurity toomanage e responder.
* [Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md) – localizar perguntas frequentes sobre como usar o serviço de saudação.

