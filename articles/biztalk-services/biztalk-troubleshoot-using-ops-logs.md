---
title: "os serviços do BizTalk aaaTroubleshoot usando logs de operação | Microsoft Docs"
description: "Solucionar problemas dos Serviços BizTalk usando logs de operação. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 1081a9c6-58cc-4a76-8ac8-11e5e7a6ea27
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 102779ed6e29784f190c28e4102a7d9670614914
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-troubleshoot-using-operation-logs"></a>Serviços BizTalk: solução de problemas usando logs de operação

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

## <a name="what-are-hello-operation-logs"></a>Quais são os Logs de operação Olá
Logs de operação é um recurso de gerenciamento de serviços disponível no hello portal clássico do Azure que permite que você tooview logs de históricos de operações executadas em seus serviços do Azure, incluindo os serviços do BizTalk. Isso permite a você tooview os dados históricos relacionados toomanagement operações de sua assinatura do BizTalk Service volta até 180 dias.

> [!NOTE]
> Este recurso só captura logs para operações de gerenciamento nos serviços do BizTalk, como quando o serviço de saudação foi iniciado, feito para cima, e assim por diante. Essas operações são rastreadas independentemente se eles são executados de saudação portal clássico do Azure ou usando Olá [APIs de REST do serviço BizTalk](http://msdn.microsoft.com/library/azure/dn232347.aspx). Para obter uma lista completa das operações que são acompanhadas usando os Serviços de Gerenciamento, consulte [Operações Acompanhadas Usando os Serviços de Gerenciamento do Azure](#bizops).<br/><br/>
> Isso não captura logs Olá para atividades relacionadas tooBizTalk tempo de execução de serviço (por exemplo, a mensagem processada por pontes, etc.). tooview esses logs, use Olá visão de rastreamento do portal de Serviços BizTalk hello. Para obter mais informações, consulte [Acompanhando as Mensagens](http://msdn.microsoft.com/library/azure/hh949805.aspx).
> 
> 

## <a name="view-biztalk-services-operation-logs"></a>Exibir os logs de operações dos Serviços BizTalk
1. No portal clássico do Azure do hello, selecione **Management Services**e, em seguida, selecione Olá **Logs de operação** guia.
2. Você pode filtrar logs de saudação com base em parâmetros diferentes, como assinatura, intervalo de datas, o tipo de serviço (por exemplo, serviços do BizTalk), nome do serviço ou status da operação de saudação (êxito, falha).
3. Selecione Olá Olá de tooview de marca de seleção de lista filtrada. Olá, imagem a seguir mostra tootestbiztalkservice de atividades relacionadas: ![exibir logs de operação][ViewLogs] 
4. tooview mais informações sobre uma operação específica, selecione a linha hello e clique em **detalhes** na barra de tarefas de saudação na parte inferior da saudação.

## <a name="bizops"></a>Operações acompanhadas usando os Serviços de Gerenciamento do Azure
Olá tabela a seguir lista operações de saudação que são controladas usando serviços de gerenciamento do Azure hello:

| Nome de operação | Tarefa |
| --- | --- |
| CreateBizTalkService |Operação toocreate um BizTalk Service novo |
| DeleteBizTalkService |Operação toodelete um BizTalk Service |
| RestartBizTalkService |Operação toorestart um BizTalk Service |
| StartBizTalkService |Operação toostart um BizTalk Service |
| StopBizTalkService |Operação toostop um BizTalk Service |
| DisableBizTalkService |Operação toodisable um BizTalk Service |
| EnableBizTalkService |Operação tooenable um BizTalk Service |
| BackupBizTalkService |Operação tooback o um BizTalk Service |
| RestoreBizTalkService |Operação toorestore um BizTalk Service de backup especificado |
| SuspendBizTalkService |Operação toosuspend um BizTalk Service |
| ResumeBizTalkService |Operação tooresume um BizTalk Service |
| ScaleBizTalkService |Operação tooscale um BizTalk Service para cima ou para baixo |
| ConfigUpdateBizTalkService |Configuração de saudação de tooupdate de operação de um BizTalk Service |
| ServiceUpdateBizTalkService |Operação tooupgrade ou downgrade de uma versão diferente do BizTalk Service tooa |
| PurgeBackupBizTalkService |Backups de toopurge de operação de saudação BizTalk Service fora do período de retenção de saudação |

## <a name="see-also"></a>Consulte também
* [Fazer o backup do Serviço BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [Restaurar o Serviço BizTalk do backup](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [Serviços BizTalk: gráfico das edições Developer, Basic, Standard e Premium](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [Serviços BizTalk: provisionamento usando o portal clássico do Azure](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [Serviços BizTalk: gráfico do status do provisionamento](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [Serviços BizTalk: guias Painel, Monitor e Escala](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [Serviços BizTalk: limitação](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [Serviços BizTalk: nome e chave do emissor](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [Como posso começar a usar Olá SDK dos Serviços BizTalk do Azure](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[ViewLogs]: ./media/biztalk-troubleshoot-using-ops-logs/Operation-Logs.png

