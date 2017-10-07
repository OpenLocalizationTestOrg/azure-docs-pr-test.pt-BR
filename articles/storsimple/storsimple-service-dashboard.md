---
title: "Painel de serviço do Gerenciador de aaaStorSimple | Microsoft Docs"
description: "Descreve o painel do serviço StorSimple Manager hello e explica como toouse-toomonitor integridade de saudação da sua solução StorSimple."
services: storsimple
documentationcenter: 
author: SharS
manager: carmonm
editor: 
ms.assetid: fb0f131d-d60b-45d7-ace2-56d0502e6627
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/24/2016
ms.author: v-sharos
ms.openlocfilehash: dc1197eb5deac337215b260845631a4f04be1011
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-dashboard"></a>Use o painel do serviço StorSimple Manager Olá
## <a name="overview"></a>Visão geral
página de painel de serviço Olá StorSimple Manager fornece um resumo de todos os dispositivos de saudação que são conectado toohello serviço StorSimple Manager, destacando aqueles que precisam de atenção do administrador do sistema. Este tutorial apresenta a página de painel hello, explica a função e o conteúdo do painel hello e descreve Olá as tarefas que você pode executar nessa página.

![Painel de serviço](./media/storsimple-service-dashboard/HCS_ServiceDashboard.png)

painel do serviço StorSimple Manager Olá exibe Olá informações a seguir:

* Em Olá **gráfico** área, você pode ver relevante de métricas de saudação do gráfico para seus dispositivos. Você pode exibir o armazenamento primário de saudação (localmente fixados e em camadas) usado em todos os dispositivos hello, bem como o armazenamento em nuvem Olá consumidos pelos dispositivos em um período de tempo. Use controles de saudação no canto superior direito Olá Olá gráfico toospecify uma escala de tempo de 1 semana, 1 mês, 3 meses ou 1 ano.
* Olá **visão geral de uso** mostra Olá armazenamento primário provisionado e consumido por todos os dispositivos relativos toohello armazenamento total disponível em todos os dispositivos. **Provisionado** refere-se a quantidade de toohello de armazenamento preparado e alocado para uso, enquanto **usado** refere-se toousage de volumes conforme exibido pelos iniciadores Olá dispositivos toohello conectado.
* Olá **alertas** área fornece um instantâneo de todos os alertas ativos de saudação em todos os dispositivos de hello, agrupados pela gravidade do alerta. Clicando em nível de severidade Olá abre Olá **alertas** página, no escopo tooshow esses alertas. Em Olá **alertas** página, você pode clicar em um tooview alertas individuais mais detalhes sobre esse alerta, incluindo todas as ações recomendadas. Você também pode limpar o alerta de saudação se Olá problema foi resolvido.
* Olá **trabalhos** área fornece um instantâneo dos trabalhos recentes em todos os dispositivos conectados tooyour serviço. Contém links que você pode usar toolook em trabalhos que estão atualmente em andamento, os que falharam em Olá últimas 24 horas, ou aqueles que estão agendados toorun em Olá próximas 24 horas.
* Olá **visão rápida** área fornece informações úteis, como o status do serviço, o número de dispositivos conectados toohello serviço, local do serviço de saudação e detalhes da assinatura de saudação que é associado ao serviço de saudação. Também há um log de operações de toohello do link. Clique em Olá link toosee uma lista de todas as operações concluídas de serviço StorSimple Manager.

Você pode usar o hello StorSimple Manager serviço painel página tooinitiate Olá tarefas a seguir:

* Exibir ou regenerar a chave de registro do serviço de saudação.
* Alterar chave de criptografia de dados de serviço de saudação.
* Exibir logs de operação de saudação.

## <a name="view-or-regenerate-hello-service-registration-key"></a>Exibir ou regenerar a chave de registro de serviço Olá
chave de registro do serviço de saudação é tooregister usado um dispositivo do Microsoft Azure StorSimple com o serviço StorSimple Manager hello, para que hello dispositivo aparece na Olá portal clássico do Azure para ações de gerenciamento adicionais. chave de saudação é criada no primeiro dispositivo de saudação e compartilhado com o restante da saudação de seus dispositivos.

Clicando em **chave de registro** (final Olá Olá página) abre Olá **chave de registro de serviço** caixa de diálogo onde você pode qualquer cópia Olá serviço Registro toohello chave de transferência atual ou regenerar a chave de registro de serviço de saudação.

Regenerando chave de saudação não afeta os dispositivos registrados anteriormente: ele afeta somente os dispositivos de saudação registrados com o serviço de saudação depois Olá chave é regenerada.

Para obter mais informações sobre como exibir e gerar go chave do registro Olá serviço muito[chave de registro de serviço Get hello](storsimple-manage-service.md#get-the-service-registration-key).

## <a name="change-hello-service-data-encryption-key"></a>Alterar a chave de criptografia de dados de serviço Olá
Chaves de criptografia de dados de serviço são dados confidenciais do cliente de tooencrypt usadas, como credenciais de conta de armazenamento, que são enviadas de seu dispositivo do StorSimple Manager serviço toohello StorSimple. Você precisará toochange essas chaves periodicamente se sua organização de TI tiver uma política de rotação de chaves em dispositivos de armazenamento de saudação. Olá processo de alteração de chave pode ser ligeiramente diferente dependendo se há um único ou vários dispositivos gerenciados pelo Olá serviço StorSimple Manager.

Alterar chave de criptografia de dados para serviço Olá é um processo de 3 etapas:

1. Usando Olá portal clássico do Azure, autorize uma chave de criptografia do dispositivo toochange Olá serviço dados.
2. Usando o Windows PowerShell para StorSimple, inicie a alteração de criptografia de dados chave serviço hello.
3. Se você tiver mais de um dispositivo StorSimple, atualize a chave de criptografia de dados de serviço de saudação em Olá outros dispositivos.

Olá etapas a seguir descrevem o processo de renovação de Olá para chave de criptografia de dados de serviço de saudação.

[!INCLUDE [storsimple-change-data-encryption-key](../../includes/storsimple-change-data-encryption-key.md)]

## <a name="view-hello-operations-logs"></a>Exibir logs de operações de saudação
Você pode exibir os logs de operação Olá clicando Olá link dos logs disponíveis no hello **visão rápida** painel do painel de saudação. Isso o levará toohello gerenciamento página serviços, onde você pode filtrar e ver Olá registra o serviço StorSimple Manager tooyour específico.

## <a name="next-steps"></a>Próximas etapas
* Saiba como muito[solucionar problemas de um dispositivo StorSimple](storsimple-troubleshoot-operational-device.md).
* Saiba mais sobre como muito[use Olá tooadminister do serviço StorSimple Manager seu dispositivo StorSimple](storsimple-manager-service-administration.md).

