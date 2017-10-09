---
title: "aaaProtecting suas máquinas virtuais na Central de segurança do Azure | Microsoft Docs"
description: "Este documento endereça as recomendações na Central de Segurança do Azure que ajudam a proteger suas máquinas virtuais e cumprir as políticas de segurança."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 47fa1f76-683d-4230-b4ed-d123fef9a3e8
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: terrylan
ms.openlocfilehash: 926c04974f61215b4a3e02646f23dafb87c793e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-your-virtual-machines-in-azure-security-center"></a>Protegendo suas máquinas virtuais na Central de Segurança do Azure
Central de segurança do Azure analisa o estado de segurança Olá seus recursos do Azure. Quando a Central de segurança identifica possíveis vulnerabilidades de segurança, ele cria recomendações que o guiam pelo processo de saudação de Configurando controles de saudação necessário.  Recomendações se aplicam a tipos de recurso tooAzure: máquinas virtuais (VMs), redes, aplicativos e SQL.

Este artigo aborda as recomendações que se aplicam a tooVMs.  As recomendações de VM giram em torno da coleta de dados, aplicando atualizações do sistema, provisionamento o antimalware, criptografando os discos da VM e muito mais.  Uso tabela Olá abaixo como uma referência toohelp você entender o que cada um deles será feito se você aplicá-lo e recomendações de VM disponíveis de saudação.

## <a name="available-vm-recommendations"></a>Recomendações disponíveis da VM
| Recomendações | Descrição |
| --- | --- |
| [Habilitar coleta de dados para assinaturas](security-center-enable-data-collection.md) |Recomenda-se de que você ativar a coleta de dados na política de segurança Olá para cada uma das suas assinaturas e todas as máquinas virtuais (VMs) em suas assinaturas. |
| [Habilitar a criptografia para a Conta de Armazenamento do Azure](security-center-enable-encryption-for-storage-account.md) | Recomenda a habilitação da Criptografia do Serviço de Armazenamento do Azure para dados em repouso. Criptografia de serviço de armazenamento (SSE) funciona criptografando dados hello quando ele é gravado tooAzure armazenamento e descriptografa antes da recuperação. SSE está disponível somente para Olá serviço Blob do Azure e pode ser usado para blobs de bloco, blobs de página e blobs de acréscimo. mais, consulte toolearn [criptografia do serviço de armazenamento de dados em repouso](../storage/common/storage-service-encryption.md).</br>A SSE tem suporte apenas nas contas de armazenamento do Resource Manager. Atualmente, não há suporte para contas de armazenamento clássicas. saudação de toounderstand clássica e modelos de implantação do Gerenciador de recursos, consulte [modelos de implantação do Azure](../azure-classic-rm.md). |
| [Corrigir as vulnerabilidades do sistema operacional](security-center-remediate-os-vulnerabilities.md) |Recomenda que você a alinhar as configurações do sistema operacional com hello recomendado regras de configuração, por exemplo, não permitem toobe senhas salva. |
| [Aplicar atualizações do sistema](security-center-apply-system-updates.md) |Recomenda que você implante tooVMs atualizações críticas e segurança de sistema ausente. |
| [Aplicar um controle de acesso à rede Just-In-Time](security-center-just-in-time.md) | Recomenda que você aplique acesso à VM just in time. Olá apenas no recurso de tempo está no modo de visualização e disponível no hello camada padrão da Central de segurança. Consulte [preços](security-center-pricing.md) camadas de preços do toolearn mais sobre o Centro de segurança. |
| [Reinicializar após as atualizações do sistema](security-center-apply-system-updates.md#reboot-after-system-updates) |Recomenda que você reinicialize um processo de saudação do VM toocomplete de aplicação de atualizações do sistema. |
| [Instalar proteção do ponto de extremidade](security-center-install-endpoint-protection.md) |Recomenda-se de que você forneça antimalware programas tooVMs (VMs do Windows somente). |
| [Resolver alertas de integridade do Endpoint Protection](security-center-resolve-endpoint-protection-health-alerts.md) |Recomenda que você resolva falhas do Endpoint Protection. |
| [Habilitar o Agente de VM](security-center-enable-vm-agent.md) |Permite que você toosee que exigem VMs Olá agente de VM. Olá VM Agent deve ser instalado em máquinas virtuais no patch tooprovision de ordem de varredura, verificação de linha de base e os programas antimalware. Olá agente VM é instalado por padrão para VMs que são implantados de saudação do Azure Marketplace. artigo Olá [agente de VM e extensões – parte 2](http://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/) fornece informações sobre como tooinstall Olá agente de VM. |
| [Aplicar a criptografia de disco](security-center-apply-disk-encryption.md) |Recomenda de que você criptografe os discos de VM usando o Azure Disk Encryption (VMs do Windows e do Linux). Criptografia é recomendada para Olá SO e os volumes de dados na sua VM. |
| [Atualizar a versão do sistema operacional](security-center-update-os-version.md) |Recomenda que você atualize a versão de sistema operacional (SO) Olá para seu serviço de nuvem toohello versão mais recente disponível para a família de sistemas operacionais.  toolearn mais sobre serviços de nuvem, consulte Olá [visão geral dos serviços de nuvem](../cloud-services/cloud-services-choose-me.md). |
| [Avaliação de vulnerabilidade não instalada](security-center-vulnerability-assessment-recommendations.md) |Recomenda que você instale uma solução de avaliação de vulnerabilidade na VM. |
| [Corrigir vulnerabilidades](security-center-vulnerability-assessment-recommendations.md#review-the-recommendation) |Permite que você toosee sistema e do aplicativo vulnerabilidades detectadas pela solução de avaliação de vulnerabilidade Olá instalada na sua VM. |

## <a name="see-also"></a>Consulte também
toolearn mais informações sobre recomendações que se aplicam a tipos de recursos do Azure tooother, consulte Olá seguinte:

* [Protegendo seus aplicativos na Central de segurança do Azure](security-center-application-recommendations.md)
* [Protegendo sua rede na Central de Segurança do Azure](security-center-network-recommendations.md)
* [Protegendo o serviço do SQL Azure na Central de Segurança do Azure](security-center-sql-service-recommendations.md)

toolearn mais sobre o Centro de segurança, consulte o seguinte hello:

* [Definir políticas de segurança na Central de segurança do Azure](security-center-policies.md) – Saiba como tooconfigure as políticas de segurança para sua assinatura do Azure e grupos de recursos.
* [Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md) – Saiba como alertas de toosecurity toomanage e responder.
* [Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md) – localizar perguntas frequentes sobre como usar o serviço de saudação.
