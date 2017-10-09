---
title: "aaaGet iniciado com o dimensionamento automático no Azure | Microsoft Docs"
description: Saiba como tooscale seus recursos no Azure.
author: rajram
manager: rboucher
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: rajram
ms.openlocfilehash: 6b3c3f4529018dcaf9691c538fec63dfbb3cea06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-autoscale-in-azure"></a>Introdução ao dimensionamento automático no Azure
Este artigo descreve como tooset suas configurações de dimensionamento automático para o recurso no portal do Microsoft Azure hello.

Dimensionamento automático de Monitor do Azure se aplica apenas conjuntos de escala de máquina toovirtual, serviços de nuvem, planos de serviço de aplicativo do Azure e ambientes de serviço de aplicativo. 

## <a name="discover-hello-autoscale-settings-in-your-subscription"></a>Descobrir as configurações de dimensionamento automático de saudação em sua assinatura
Você pode descobrir todos os recursos de saudação para o qual o dimensionamento automático é aplicável no Monitor do Azure. Use Olá seguindo as etapas para obter uma explicação passo a passo:

1. Olá abrir [portal do Azure.][1]
2. Clique hello Azure ícone no painel esquerdo da saudação.
  ![Abra o Azure Monitor][2]
3. Clique em **AutoEscala** tooview todos os recursos de saudação para o dimensionamento automático é aplicável, juntamente com seu status atual de dimensionamento automático.
  ![Descubra o dimensionamento automático no Azure Monitor][3]

Você pode usar o painel de filtro de saudação em tooscope de saudação principais recursos de tooselect Olá lista em um grupo de recursos específicos, tipos específicos de recursos ou um recurso específico.

Para cada recurso, você encontrará a contagem atual de instâncias hello e status da AutoEscala hello. Olá AutoEscala status pode ser:

- **Não configurado**: você ainda não habilitou o dimensionamento automático para este recurso.
- **Habilitado**: você habilitou o dimensionamento automático para este recurso.
- **Desabilitado**: você desabilitou o dimensionamento automático para este recurso.

## <a name="create-your-first-autoscale-setting"></a>Crie sua primeira configuração de dimensionamento automático

Agora vamos por meio de uma simples passo toocreate sua primeira configuração de dimensionamento automático.

1. Olá abrir **AutoEscala** folha no Monitor do Azure e selecione um recurso que você deseja tooscale. (hello etapas a seguir usam um plano de serviço de aplicativo associado a um aplicativo web. Você pode [criar seu primeiro aplicativo Web ASP.NET no Azure em 5 minutos.][4])
2. Observe que a contagem atual de instâncias de saudação é 1. Clique em **Habilitar dimensionamento automático**.
  ![Configuração de dimensionamento para um novo aplicativo Web][5]
3. Forneça um nome para a configuração da escala hello e, em seguida, clique em **adicionar uma regra**. Observe as opções de regra de escala de saudação que são abertos como um painel de contexto Olá direita. Por padrão, isso define Olá opção tooscale sua instância de contagem em 1 se Olá percentual de CPU do recurso Olá exceder 70 por cento. Deixe-o com seus valores padrão e clique em **Adicionar**.
  ![Criar configuração dimensionamento para um aplicativo Web][6]
4. Agora, você criou sua primeira regra de dimensionamento. Observe que Olá UX recomenda práticas recomendadas e declara que "é recomendável toohave pelo menos uma escala na regra." toodo para:
  
    a. Clique em **Adicionar uma Regra**. 

    b. Definir **operador** muito**menor**.

    c. Definir **limite** muito**20**.

    d. Definir **operação** muito**diminuir a contagem por**.

   Agora, você deve ter uma configuração de dimensionamento que expande/reduz com base no uso da CPU.
   ![Dimensionamento com base na CPU][8]
5. Clique em **Salvar**.

Parabéns! Agora você já criou com êxito sua primeira tooautoscale de configuração de escala seu aplicativo web com base no uso da CPU.

> [!NOTE] 
> Olá, mesmas etapas são aplicável tooget iniciado com uma escala de máquina virtual função de serviço de nuvem ou conjunto.

## <a name="other-considerations"></a>Outras considerações
### <a name="scale-based-on-a-schedule"></a>Dimensionamento com base em um planejamento
Além disso tooscale com base na CPU, você pode definir sua escala diferente para dias específicos da semana hello.

1. Clique em **Adicionar uma condição de dimensionamento**.
2. Configurando regras de modo e hello de escala de saudação é Olá mesmo como condição de padrão de saudação.
3. Selecione **Repita dias específicos** para agendamento de saudação.
4. Selecione os dias hello e a hora de início/término hello para quando a condição de escala Olá deve ser aplicada.

![Condição de dimensionamento com base no agendamento][9]
### <a name="scale-differently-on-specific-dates"></a>Dimensionar de forma diferente em datas específicas
Além disso tooscale com base na CPU, você pode definir sua escala diferente para datas específicas.

1. Clique em **Adicionar uma condição de dimensionamento**.
2. Configurando regras de modo e hello de escala de saudação é Olá mesmo como condição de padrão de saudação.
3. Selecione **especificar datas de início/término** para agendamento de saudação.
4. Selecione as datas de início/término hello e a hora de início/término hello para quando a condição de escala Olá deve ser aplicada.

![Condição de dimensionamento com base em datas][10]

### <a name="view-hello-scale-history-of-your-resource"></a>Exibir o histórico de escala de saudação do recurso
Sempre que o recurso é dimensionado para cima ou para baixo, um evento é registrado no log de atividades de saudação. Você pode exibir histórico de escala de saudação do recurso para Olá últimas 24 horas, alternando toohello **histórico de execução** guia.

![Histórico da execução][11]

Se você desejar tooview Olá escala completa histórico (para cima too90 dias), selecione **clique aqui toosee mais detalhes**. log de atividades de saudação é aberta, com o dimensionamento automático previamente selecionado para o recurso e categoria.

### <a name="view-hello-scale-definition-of-your-resource"></a>Exibir definição de escala de saudação do recurso
Dimensionamento automático é um recurso do Gerenciador de Recursos do Azure. Você pode exibir a definição de escala de saudação em JSON, alternando toohello **JSON** guia.

![Definição de escala][12]

Você pode fazer alterações no JSON diretamente, se necessário. Essas alterações serão refletidas depois que você as salvar.

### <a name="disable-autoscale-and-manually-scale-your-instances"></a>Desabilitar a escala automática e dimensionar suas instâncias manualmente
Pode haver momentos quando desejar toodisable sua configuração atual de escala e Dimensionar manualmente o recurso.

Clique em Olá **desabilitar dimensionamento automático** botão na parte superior da saudação.
![Desabilitar dimensionamento automático][13]

> [!NOTE] 
> Esta opção desabilita a sua configuração. No entanto, você pode voltar tooit depois de habilitar o dimensionamento automático novamente. 

Agora você pode definir número de saudação de instâncias que você deseja tooscale toomanually.

![Definir dimensionamento manual][14]

Você sempre pode retornar tooAutoscale clicando **habilitar a AutoEscala** e **salvar**.

## <a name="next-steps"></a>Próximas etapas
- [Criar um alerta de Log da atividade toomonitor todas as operações de mecanismo de dimensionamento automático em sua assinatura](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert)
- [Criar um alerta de Log da atividade toomonitor todas as falhas operações de escala-em/expansão de dimensionamento automático em sua assinatura](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)

<!--Reference-->
[1]:https://portal.azure.com
[2]: ./media/monitoring-autoscale-get-started/azure-monitor-launch.png
[3]: ./media/monitoring-autoscale-get-started/discover-autoscale-azure-monitor.png
[4]: https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-get-started-dotnet
[5]: ./media/monitoring-autoscale-get-started/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-get-started/create-scale-setting-web-app.png
[7]: ./media/monitoring-autoscale-get-started/scale-in-recommendation.png
[8]: ./media/monitoring-autoscale-get-started/scale-based-on-cpu.png
[9]: ./media/monitoring-autoscale-get-started/scale-condition-schedule.png
[10]: ./media/monitoring-autoscale-get-started/scale-condition-dates.png
[11]: ./media/monitoring-autoscale-get-started/scale-history.png
[12]: ./media/monitoring-autoscale-get-started/scale-definition-json.png
[13]: ./media/monitoring-autoscale-get-started/disable-autoscale.png
[14]: ./media/monitoring-autoscale-get-started/set-manualscale.png

