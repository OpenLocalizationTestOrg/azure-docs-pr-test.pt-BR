---
title: "IoT Hub alta disponibilidade e recuperação de desastres de aaaAzure | Microsoft Docs"
description: "Descreve recursos hello Azure e o IoT Hub que ajudam você a toobuild soluções altamente disponíveis de Azure IoT com recursos de recuperação de desastres."
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: ae320e58-aa20-45b9-abdc-fa4faae8e6dd
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/16/2016
ms.author: elioda
ms.openlocfilehash: 74e1fa1682258819ffb3fd84eb79e42fc6e4120f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="iot-hub-high-availability-and-disaster-recovery"></a>Alta disponibilidade e recuperação de desastres do Hub IoT
Como um serviço do Azure, o IoT Hub fornece alta disponibilidade (HA) usando redundâncias no nível de região do Azure hello, sem qualquer trabalho adicional exigido pela solução de saudação. plataforma do Microsoft Azure Olá também inclui recursos toohelp criar soluções com recursos de recuperação de desastres ou disponibilidade entre regiões. Se você quiser tooprovide global, alta disponibilidade entre regiões para dispositivos ou usuários, criar e preparar suas soluções tootake aproveitar esses recursos de recuperação de desastres do Azure. artigo Olá [orientação técnica de continuidade de negócios do Azure](../resiliency/resiliency-technical-guidance.md) descreve recursos internos Olá no Azure para continuidade de negócios e recuperação de desastres. Olá [recuperação de desastres e alta disponibilidade para aplicativos do Azure] [ Disaster recovery and high availability for Azure applications] paper fornece diretrizes de arquitetura sobre estratégias para aplicativos do Azure tooachieve alta disponibilidade e recuperação de desastres.

## <a name="azure-iot-hub-dr"></a>DR do Hub IoT do Azure
Além disso toointra região HA, IoT Hub implementa mecanismos de failover para a recuperação de desastres que não exigem nenhuma intervenção do usuário hello. Recuperação de desastres de Hub IoT é iniciada automaticamente e tem um objetivo de tempo de recuperação (RTO) de 26 de 2 horas e Olá objetivos de ponto de recuperação (RPOs) a seguir.

| Funcionalidade | RPO |
| --- | --- |
| Disponibilidade de serviço para operações de registro e comunicação |Possível perda de CName |
| Dados de identidade no registro de identidade |Perda de dados de 0 a 5 minutos |
| Mensagens do dispositivo para a nuvem |Todas as mensagens não lidas são perdidas |
| Mensagens de monitoramento de operações |Todas as mensagens não lidas são perdidas |
| Mensagens da nuvem para o dispositivo |Perda de dados de 0 a 5 minutos |
| Fila de comentários da nuvem para o dispositivo |Todas as mensagens não lidas são perdidas |

## <a name="regional-failover-with-iot-hub"></a>Failover regional com o Hub IoT
Um tratamento completo das topologias de implantação em soluções de IoT está fora do escopo deste artigo hello. Olá artigo Olá *failover regional* modelo de implantação para a finalidade de saudação de alta disponibilidade e recuperação de desastres.

Em um modelo de failover regional, Olá solução back end executa principalmente em um datacenter local e um hub IoT secundário e um back-end são implantados em outro local do datacenter. Se o hub IoT de saudação no datacenter primário Olá sofre uma interrupção ou conectividade de rede de saudação do data center principal do hello dispositivo toohello é interrompida. Dispositivos usam um ponto de extremidade de serviço secundário, sempre que o gateway primário de saudação não pode ser alcançado. Com um recurso de failover entre regiões, disponibilidade de solução de saudação pode ser melhorada além de alta disponibilidade saudação de uma única região.

Em um nível alto, tooimplement um modelo de failover regional com o IoT Hub, você precisa seguir hello:

* **Um hub IoT e o dispositivo de roteamento lógica secundário**: no caso de saudação de uma interrupção do serviço em sua região primária, dispositivos devem iniciar conexão região secundária do tooyour. Considerando a natureza de reconhecimento de estado de saudação da maioria dos serviços envolvidos, é comum para o processo de failover entre região solução administradores tootrigger hello. Olá melhor maneira toocommunicate Olá novo ponto de extremidade toodevices, mantendo o controle do processo de saudação é toohave-los regularmente um *assistente* serviço para Olá active ponto de extremidade atual. Olá Assistente serviço pode ser um aplicativo web que é replicado e mantido acessível usando técnicas de redirecionamento de DNS (por exemplo, usando [Azure Traffic Manager][Azure Traffic Manager]).
* **Replicação de registro de identidade** -toobe utilizável, o hub IoT secundário de saudação deve conter todas as identidades de dispositivo que podem se conectar a solução toohello. Olá solução deve manter backups replicados geograficamente de identidades de dispositivo e carregá-los toohello secundário IoT hub antes de alternar ponto de extremidade ativo para dispositivos Olá Olá. funcionalidade de exportação de identidade de dispositivo de saudação do IoT Hub é útil neste contexto. Para saber mais, confira [Guia do desenvolvedor do Hub IoT ‑ Registro de identidade][IoT Hub developer guide - identity registry].
* **Mesclando lógica** - quando região primária Olá fica disponível novamente, todos Olá estado e dados que foram criados no site secundário Olá devem ser região primária toohello back migrados. Esse estado e os dados relacionado principalmente toodevice identidades e metadados de aplicativo, que devem ser mesclados com o hub IoT principal de saudação e qualquer outra loja na região primária Olá específicas do aplicativo. toosimplify nesta etapa, você deve usar operações idempotentes. Operações de idempotente minimizar Olá efeitos colaterais de saudação eventual consistente a distribuição de eventos e de duplicatas ou fora de ordem entrega de eventos. Além disso, a lógica do aplicativo hello deve ser projetado tootolerate possíveis inconsistências ou "ligeiramente" fora do estado de data. Essa situação pode ocorrer devido a toohello mais tempo que leva para o sistema de saudação muito "reparar" com base nos objetivos de ponto de recuperação (RPO).

## <a name="next-steps"></a>Próximas etapas
Siga essas toolearn links mais sobre Azure IoT Hub:

* [Introdução aos Hubs IoT (Tutorial)][lnk-get-started]
* [O que é o Hub IoT do Azure?][What is Azure IoT Hub?]

[Disaster recovery and high availability for Azure applications]: ../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md
[Azure Business Continuity Technical Guidance]: https://azure.microsoft.com/documentation/articles/resiliency-technical-guidance/
[Azure Traffic Manager]: https://azure.microsoft.com/documentation/services/traffic-manager/
[IoT Hub developer guide - identity registry]: iot-hub-devguide-identity-registry.md

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[What is Azure IoT Hub?]: iot-hub-what-is-iot-hub.md
