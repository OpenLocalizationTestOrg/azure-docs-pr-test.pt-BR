---
title: aaaUse Backup do Azure tooreplace sua infraestrutura de fita | Microsoft Docs
description: "Saiba como o Backup do Azure fornece a semântica semelhantes a fita que permite que você toobackup e restaurar dados no Azure"
services: backup
documentationcenter: 
author: trinadhk
manager: vijayts
editor: 
ms.assetid: 2e1bb67d-986c-4437-8056-3a63169b4214
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 1/10/2017
ms.author: saurse;trinadhk;markgal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4c5b095d95d39267c54b1eed9427bda09658bb94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-your-long-term-storage-from-tape-toohello-azure-cloud"></a>Mover o armazenamento de longo prazo de fita toohello nuvem do Azure
Os clientes do Backup do Azure e do System Center Data Protection Manager podem:

* Fazer backup de dados em agendas que melhor atenda às necessidades organizacionais hello.
* Manter os dados de backup Olá por períodos mais longos
* Tornar o Azure parte das necessidades de retenção de longo prazo (em vez de fita).

Este artigo explica como os clientes podem habilitar políticas de backup e retenção. Os clientes que usam fitas tooaddress seu longo-prazo-suas necessidades de retenção agora tem uma alternativa viável e poderosa com disponibilidade Olá desse recurso. Olá recurso está habilitado na versão mais recente de saudação do hello Azure Backup (que está disponível [aqui](http://aka.ms/azurebackup_agent)). Os clientes do System Center DPM devem atualizar para, pelo menos, o DPM 2012 R2 UR5 antes de usar o DPM com hello serviço Backup do Azure.

## <a name="what-is-hello-backup-schedule"></a>O que é Olá agendamento de Backup?
agendamento de backup Olá indica a frequência de Olá Olá da operação de backup. Por exemplo, configurações Olá Olá tela a seguir indicam que os backups são realizados diariamente às 18: 00 e à meia-noite.

![Agendamento diário](./media/backup-azure-backup-cloud-as-tape/dailybackupschedule.png)

Os clientes também podem agendar um backup semanal. Por exemplo, hello configurações em Olá tela a seguir indicam que os backups são realizados a cada alternativa domingo & quarta-feira em 9:30 da manhã e 1:00 AM.

![Agendamento semanal](./media/backup-azure-backup-cloud-as-tape/weeklybackupschedule.png)

## <a name="what-is-hello-retention-policy"></a>O que é Olá política de retenção?
política de retenção de saudação especifica a duração de saudação para o qual o backup Olá deve ser armazenado. Em vez de especificar apenas uma "política simples" para todos os pontos de backup, os clientes podem especificar políticas de retenção diferentes com base em quando é feito backup hello. Por exemplo, a saudação ponto de backup feito diariamente, que serve como um ponto de recuperação operacional, é preservado por 90 dias. ponto de backup Olá colocado no final de saudação de cada trimestre para fins de auditoria é preservado por mais tempo.

![Política de retenção](./media/backup-azure-backup-cloud-as-tape/retentionpolicy.png)

Olá número total de pontos de retenção"" especificados nesta política é 90 (pontos de diários) + 40 (um para cada trimestre para 10 anos) = 130.

## <a name="example--putting-both-together"></a>Exemplo – Juntando ambos
![Tela de exemplo](./media/backup-azure-backup-cloud-as-tape/samplescreen.png)

1. **Política de retenção diária**: os backups diários são armazenados por sete dias.
2. **Política de retenção semanal**: os backups feitos aos sábados, à meia-noite e às 18h, serão preservados por quatro semanas
3. **Política de retenção mensal**: Backups feitos em meia-noite e 18h00 de saudação Último sábado de cada mês são preservados por 12 meses
4. **Política de retenção anual**: Backups feitos à meia-noite Olá Último sábado de março, cada são preservados para 10 anos

Olá número total de pontos de retenção"" (do qual um cliente pode restaurar dados de pontos) em Olá diagrama anterior é calculado da seguinte forma:

* dois pontos por dia por sete dias = 14 pontos de recuperação
* dois pontos por semana por quatro semanas = oito pontos de recuperação
* dois pontos por mês por 12 meses = 24 pontos de recuperação
* um ponto por ano por 10 anos = 10 pontos de recuperação

Olá o número total de pontos de recuperação é 56.

> [!NOTE]
> O backup do Azure não tem uma restrição para o número de pontos de recuperação.
>
>

## <a name="advanced-configuration"></a>Configuração avançada
Clicando em **modificar** em Olá antes da tela, os clientes têm mais flexibilidade para especificar agendamentos de retenção.

![Modificar](./media/backup-azure-backup-cloud-as-tape/modify.png)

## <a name="next-steps"></a>Próximas etapas
Para saber mais sobre o Backup do Azure, veja:

* [Introdução tooAzure Backup](backup-introduction-to-azure-backup.md)
* [Teste o Backup do Azure](backup-try-azure-backup-in-10-mins.md)
