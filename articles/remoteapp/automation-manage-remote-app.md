---
title: "Gerenciar Azure RemoteApp usando a Automação do Azure | Microsoft Docs"
description: "Saiba mais sobre como o serviço de Automação do Azure pode ser usado para gerenciar o Azure RemoteApp."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
ms.assetid: 589f01ef-f9c1-4e7b-a040-1b46862d3544
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: magoedte;csand
ms.openlocfilehash: 59ac11f153c0bd74a1106400dbbf5790968b657c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-remoteapp-using-azure-automation"></a>Gerenciando o Azure RemoteApp usando a Automação do Azure
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Leia o [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

Este guia apresentará o serviço de Automação do Azure e como ele pode ser usado para simplificar o gerenciamento do Azure RemoteApp.

## <a name="what-is-azure-automation"></a>O que é Automação do Azure?
[Automação do Azure](../automation/automation-intro.md) é um serviço do Azure para simplificar o gerenciamento de nuvem por meio da automação de processo. Com o uso da Automação do Azure, as tarefas manuais, repetidas com frequência, de execução longa e propensas a erros podem ser automatizadas para aumentar a confiabilidade, a eficiência e o tempo de retorno para sua organização.

A Automação do Azure fornece um mecanismo de execução de fluxo de trabalho altamente confiável e altamente disponível que é dimensionado para atender às suas necessidades. Na Automação do Azure, processos podem ser inicializados manualmente, por sistemas de terceiros ou em intervalos agendados para que as tarefas acontecem exatamente quando necessário.

Reduza o custo operacional e libere a equipe de TI e DevOps para se concentrar no trabalho que agrega valor de negócios, transferindo as tarefas de gerenciamento de nuvem para serem executadas automaticamente pela Automação do Azure.

## <a name="how-can-azure-automation-help-manage-azure-remoteapp"></a>Como a Automação do Azure ajuda a gerenciar o Azure RemoteApp?
O RemoteApp pode ser gerenciado na Automação do Azure usando os cmdlets do PowerShell disponíveis em [Ferramentas PowerShell do Azure](https://msdn.microsoft.com/library/azure/jj156055.aspx). A Automação do Azure tem esses cmdlets do PowerShell do RemoteApp disponíveis imediatamente para que você possa executar todas as tarefas de gerenciamento do RemoteApp dentro do serviço. Você também pode combinar esses cmdlets na Automação do Azure com os cmdlets para outros serviços do Azure, para automatizar tarefas complexas nos serviços do Azure e sistemas de terceiros.

## <a name="next-steps"></a>Próximas etapas
Agora que você aprendeu os fundamentos de Automação do Azure e como ela pode ser usada para gerenciar o Azure RemoteApp, siga estes links para obter mais informações sobre a Automação do Azure.

* Confira o [Guia de introdução](../automation/automation-first-runbook-graphical.md)

