---
title: "aaaMonitor Surface hub com análise de logs do Azure | Microsoft Docs"
description: "Usar a saudação Surface Hub solução tootrack Olá integridade de seus Hubs de superfície e entender como eles estão sendo usados."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 8b4e56bc-2d4f-4648-a236-16e9e732ebef
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 623d30e749cafdd4a34ba0c5b3408164f1b4a95b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-surface-hubs-with-log-analytics-tootrack-their-health"></a>Monitore Surface hub com análise de Log tootrack sua integridade

![Símbolo do Surface Hub](./media/log-analytics-surface-hubs/surface-hub-symbol.png)

Este artigo descreve como você pode usar o hello solução Surface Hub em dispositivos de Microsoft Surface Hub toomonitor análise de Log com hello Microsoft Operations Management Suite (OMS). Faça a análise ajuda a que acompanhar integridade Olá seus hubs de superfície, bem como entender como eles estão sendo usados.

Cada Surface Hub tem Olá que Microsoft Monitoring Agent instalado. O agente de saudação que você pode enviar dados de sua tooOMS Surface Hub. Arquivos de log são lidos a partir de sua superfície Hubs e são, em seguida, são enviados toohello serviço do OMS. Problemas como servidores offline, Olá calendário não está sincronizando ou conta de saudação do dispositivo é toolog não é possível para o Skype são mostrados no OMS no painel do hello Surface Hub. Usando dados de saudação no painel de saudação, você pode identificar dispositivos que não estão em execução, ou que têm outros problemas e potencialmente aplicar correções para problemas de saudação detectado.

## <a name="installing-and-configuring-hello-solution"></a>Instalando e configurando a solução Olá
Use Olá tooinstall informações a seguir e configurar a solução de saudação. Em ordem toomanage seus Hubs de superfície da saudação Microsoft Operations Management Suite (OMS), você precisará Olá a seguir:

* Uma assinatura válida muito[OMS](http://www.microsoft.com/oms).
* Um [assinatura OMS](https://azure.microsoft.com/pricing/details/log-analytics/) nível que darão suporte a saudação número de dispositivos que você deseja toomonitor. Os preços do OMS variam dependendo de quantos dispositivos estão registrados e a quantidade de dados que ele processa. Você vai querer tootake isso em consideração ao planejar a distribuição de Surface Hub.

Em seguida, você irá adicionar uma assinatura Microsoft Azure existente do OMS assinatura tooyour ou criar um novo espaço de trabalho diretamente por meio do portal do OMS hello. Instruções detalhadas para usar o método podem ser encontradas em [Introdução ao Log Analytics](log-analytics-get-started.md). Depois do hello assinatura do OMS é, há tooenroll de duas maneiras dos dispositivos Surface Hub:

* Automaticamente por meio do Intune
* Manualmente por meio das **configurações** em seu dispositivo do Surface Hub.

## <a name="set-up-monitoring"></a>Configurar monitoramento
Você pode monitorar a integridade de saudação e atividade do seu Hub de superfície usando a análise de Log no OMS. Você pode registrar Olá Surface Hub no OMS usando o Intune ou localmente usando **configurações** em Olá Surface Hub.

## <a name="connect-surface-hubs-toooms-through-intune"></a>Conectar Hubs superfície tooOMS por meio do Intune
Você vai precisar Olá ID do espaço de trabalho e a chave de espaço de trabalho espaço de trabalho do OMS Olá que irão gerenciar seus Hubs de superfície. Você pode obter do portal do OMS hello.

Intune é um produto da Microsoft que permite que você toocentrally gerenciar definições de configuração do OMS Olá são aplicada tooone ou mais dos seus dispositivos. Siga estas etapas tooconfigure seus dispositivos por meio do Intune:

1. Entrar tooIntune.
2. Navegue muito**configurações** > **fontes conectadas**.
3. Criar ou editar uma política com base no modelo do hello Surface Hub.
4. Navegue toohello seção OMS (Insights operacionais) de diretiva de saudação e adicionar Olá *ID do espaço de trabalho* e *chave do espaço de trabalho* toohello política.
5. Salve a política de saudação.
6. Associe a política de saudação com o grupo de dispositivos apropriado hello.

   ![Política do Intune](./media/log-analytics-surface-hubs/intune.png)

Intune é sincronizado, em seguida, configurações do OMS Olá com dispositivos de saudação do grupo-alvo hello, registrá-los em seu espaço de trabalho do OMS.

## <a name="connect-surface-hubs-toooms-using-hello-settings-app"></a>Conectar Hubs superfície tooOMS usando o aplicativo de configurações de saudação
Você vai precisar Olá ID do espaço de trabalho e a chave de espaço de trabalho espaço de trabalho do OMS Olá que irão gerenciar seus Hubs de superfície. Você pode obter do portal do OMS hello.

Se você não usar o Intune toomanage seu ambiente, você pode registrar manualmente por meio de dispositivos **configurações** em cada Surface Hub:

1. No seu Surface Hub, abra **Configurações**.
2. Insira as credenciais de administrador de dispositivo hello quando solicitado.
3. Clique em **este dispositivo**e Olá em **monitoramento**, clique em **definir configurações de OMS**.
4. Selecione **Habilitar monitoramento**.
5. No diálogo de configurações do OMS hello, digite Olá **ID do espaço de trabalho** e tipo hello **chave do espaço de trabalho**.  
   ![configurações](./media/log-analytics-surface-hubs/settings.png)
6. Clique em **Okey** toocomplete configuração de saudação.

Uma confirmação será exibida informando se Olá configuração OMS foi iniciado com êxito aplicado toohello dispositivo. Se ela foi, aparecerá uma mensagem informando que o agente de saudação conectado com êxito o serviço OMS toohello. dispositivo Hello, em seguida, começa a enviar dados tooOMS onde você pode exibir e agir sobre ele.

## <a name="monitor-surface-hubs"></a>Monitorar Surface Hubs
Monitorar os Surface Hubs usando o OMS é muito parecido com o monitoramento de todos os outros dispositivos registrados.

1. Entrar toohello portal do OMS.
2. Navegue dashboard do pacote de solução toohello Surface Hub.
3. A integridade do dispositivo é exibida.

   ![Painel do Surface Hub](./media/log-analytics-surface-hubs/surface-hub-dashboard.png)

Você pode criar [alertas](log-analytics-alerts.md) com base em pesquisas de log existentes ou personalizadas. Usando Olá Olá de dados que OMS coleta dos seus Hubs de superfície, você pode procurar problemas e alerta em condições de saudação que você define para seus dispositivos.

## <a name="next-steps"></a>Próximas etapas
* Use [pesquisas de Log na análise de Log](log-analytics-log-searches.md) tooview informações detalhadas e Surface Hub.
* Criar [alertas](log-analytics-alerts.md) toonotify quando ocorrem problemas com seu Surface hub.
