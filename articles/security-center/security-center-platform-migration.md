---
title: "aaaAzure migração de plataforma do Centro de segurança | Microsoft Docs"
description: "Este documento explica alguma forma de toohello alterações dados da Central de segurança do Azure é coletada."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 80246b00-bdb8-4bbc-af54-06b7d12acf58
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: yurid
ms.openlocfilehash: 28cb8d85912a3f62941cf113da51070081b5eda2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-platform-migration"></a>Migração de plataforma da Central de Segurança do Azure

A partir do início de junho de 2017, Central de segurança do Azure distribui importante alterações toohello maneira segurança dados são coletados e armazenados.  Essas alterações desbloquear novos recursos como dados de segurança do hello capacidade tooeasily pesquisa e alinha melhor com outro gerenciamento do Azure e o monitoramento dos serviços.

> [!NOTE]
> migração de plataforma Olá não deve afetar os recursos de produção e nenhuma ação é necessária do seu lado.


## <a name="whats-happening-during-this-platform-migration"></a>O que acontece durante a migração de plataforma?

Central de segurança usado anteriormente, dados de segurança de toocollect Olá agente de monitoramento do Azure de suas VMs. Isso inclui informações sobre as configurações de segurança, que são usados tooidentify vulnerabilidades, e eventos de segurança, que são usados toodetect ameaças. Esses dados eram armazenados em suas contas de armazenamento no Azure.

No futuro, que Central de segurança usa Olá Microsoft Monitoring Agent – isso é Olá mesmo agente usado pelo serviço de análise de Log e Olá Operations Management Suite. Dados coletados deste agente são armazenados em qualquer existente *análise de Log* [espaço de trabalho](../log-analytics/log-analytics-manage-access.md) associado à sua assinatura do Azure ou um novo espaço, levando em conta localização geográfica de saudação do hello VM .

## <a name="agent"></a>Agente

Como parte da transição hello, Olá Microsoft Monitoring Agent (para [Windows](../log-analytics/log-analytics-windows-agents.md) ou [Linux](../log-analytics/log-analytics-linux-agents.md)) é instalado em todas as máquinas virtuais do Azure do qual dados está sendo coletados no momento.  Se Olá atual aproveita o hello que VM já possui Olá Microsoft Monitoring Agent instalado, Central de segurança do agente foi instalado.

Para um período de tempo (normalmente de alguns dias), os dois agentes serão executado lado a lado tooensure uma transição suave sem qualquer perda de dados. Isso permitirá que a Microsoft toovalidate que Olá novo pipeline de dados está funcionando antes de interromper o uso de pipeline atual hello. Saudação de uma vez verificada, o agente de monitoramento do Azure será removido de suas VMs. Você não precisa fazer nada. Um email avisará quando todos os clientes forem migrados.
 
Não é recomendável que você desinstalar manualmente Olá agente de monitoramento do Azure durante a migração de saudação como lacunas nos dados de segurança podem resultar. Confira [Suporte e atendimento ao cliente Microsoft](https://support.microsoft.com/contactus/) se precisar de assistência adicional. 

Olá Microsoft Agent de monitoramento do Windows exige que usam a porta TCP 443, ler [guia de solução de problemas do Azure Security Center](security-center-troubleshooting-guide.md) para obter mais informações.


> [!NOTE] 
> Como Olá Microsoft Monitoring Agent pode ser usado por outro gerenciamento do Azure e monitoramento de serviços, o agente de saudação não será desinstalado automaticamente quando você desativa a coleta de dados da Central de segurança. No entanto, você poderá desinstalar manualmente o agente de saudação se necessário.

## <a name="workspace"></a>Espaço de trabalho

Conforme descrito anteriormente, dados coletados do Microsoft Monitoring Agent (em nome da Central de segurança) são armazenados em uma análise Log existente de saudação espaço associado à sua assinatura do Azure ou um novo espaço, considerando Olá de conta localização geográfica do hello VM.

Olá portal do Azure, você pode navegar toosee uma lista de seus espaços de trabalho de análise de Log, incluindo aqueles criados pela Central de segurança. Um grupo de recursos relacionados será criado para novos espaços de trabalho. Ambos seguem esta convenção de nomenclatura:

- Espaço de trabalho: *DefaultWorkspace-[ID da assinatura]-[localização geográfica]*
- Grupo de recursos: *DefaultResouceGroup-[localização geográfica]* 
 
No caso de espaços de trabalho criados pela Central de Segurança, os dados serão retidos por 30 dias. Para espaços de trabalho existentes, retenção baseia-se no espaço de trabalho de saudação de preço.

> [!NOTE]
> Os dados coletados anteriormente pela Central de Segurança permanecem nas suas contas de armazenamento. Após a conclusão da migração hello, você pode excluir essas contas de armazenamento.

### <a name="oms-security-solution"></a>Solução de segurança do OMS 

Para clientes que não têm um solução de segurança do OMS instalada, A Microsoft vai instalá-la em seu espaço de trabalho, mas ela tem como objetivo somente VMs do Azure. Não desinstale essa solução, pois não existe correção automática se isso for feito no console de gerenciamento do OMS.


## <a name="other-updates"></a>Outras atualizações

Em conjunto com a migração de plataforma hello, desenvolvimento atualizações secundárias adicionais:

- Suporte a versões adicionais do sistema operacional. Consulte a lista de saudação [aqui](security-center-faq.md#virtual-machines).
- lista de saudação de vulnerabilidades do sistema operacional será expandida. Consulte a lista de saudação [aqui](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).
- O [preço](https://azure.microsoft.com/pricing/details/security-center/) será proporcional à hora (anteriormente, era diário), o que resulta em economia de custo para alguns clientes.
- Coleta de dados será necessária e habilitada automaticamente para clientes na faixa de preços padrão hello.
- A Central de Segurança do Azure começará a descobrir soluções antimalware que não foram implantadas por meio de extensões do Azure. A descoberta do Symantec Endpoint Protection and Defender para Windows 2016 ficará disponível primeiro.
- Políticas de prevenção e notificações só são configuráveis no hello *assinatura* nível, mas os preços ainda podem ser definido como Olá *grupo de recursos* nível

