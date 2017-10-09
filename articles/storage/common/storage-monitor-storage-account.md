---
title: aaaHow toomonitor uma conta de armazenamento do Azure | Microsoft Docs
description: "Saiba como toomonitor uma conta de armazenamento no Azure usando Olá portal do Azure."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: b83cba7b-4627-4ba7-b5d0-f1039fe30e78
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: marsma
ms.openlocfilehash: 9a939e0b5db687c1b7b7857399321f681df2056a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-storage-account-in-hello-azure-portal"></a>Monitorar uma conta de armazenamento Olá portal do Azure

[Análise de Armazenamento do Azure](../storage-analytics.md) fornece métricas para todos os serviços de armazenamento e logs para blobs, filas e tabelas. Você pode usar o hello [portal do Azure](https://portal.azure.com) tooconfigure quais métricas e os logs é registrado para sua conta e configurar gráficos que fornece representações visuais dos seus dados de métricas.

> [!NOTE]
> Há custos associados com a análise de dados de monitoramento no hello portal do Azure. Para obter mais informações, consulte [Análise de armazenamento e cobrança](/rest/api/storageservices/Storage-Analytics-and-Billing).
>
> O Armazenamento de arquivos do Azure atualmente dá suporte às métricas de Análise de Armazenamento, mas ainda não dá suporte ao registro em log.
>
> Contas de armazenamento com um tipo de replicação de armazenamento com redundância de zona (ZRS) atualmente não têm métricas hello ou recurso de log habilitado.
> 
> Para obter um guia detalhado sobre como usar a análise de armazenamento e outra ferramentas tooidentify, diagnosticar e solucionar problemas relacionados ao armazenamento do Azure, consulte [monitorar, diagnosticar e solucionar problemas de armazenamento do Microsoft Azure](../storage-monitoring-diagnosing-troubleshooting.md).
>

## <a name="configure-monitoring-for-a-storage-account"></a>Configurar o monitoramento para uma conta de armazenamento

1. Em Olá [portal do Azure](https://portal.azure.com), selecione **contas de armazenamento**, em seguida, Olá nome tooopen Olá conta painel da conta armazenamento.
1. Selecione **diagnóstico** em Olá **monitoramento** seção da folha de menu hello.

    ![Opções de monitoramento](./media/storage-monitor-storage-account/stg-enable-metrics-00.png)

1. Selecione Olá **tipo** de dados de métricas para cada **service** desejar toomonitor e Olá **política de retenção** para dados de saudação. Você também pode desabilitar o monitoramento definindo **Status** muito**Off**.

    ![Opções de monitoramento](./media/storage-monitor-storage-account/stg-enable-metrics-01.png)

   Há dois tipos de métricas que você pode habilitar para cada serviço. Ambas são habilitadas por padrão para novas contas de armazenamento:

   * **Agregação**: coleta métricas como percentuais de entrada/saída, disponibilidade, latência e sucesso. Essas métricas são agregadas Olá blob, fila, tabela e serviços de arquivo.
   * **Por API**: em adição toohello as métricas agregadas, coleta Olá mesmo conjunto de métricas para cada operação de armazenamento em Olá API do serviço de armazenamento do Azure.

   política de retenção de dados do tooset hello, mover Olá **retenção (dias)** controle deslizante ou insira Olá número de dias de dados tooretain, de 1 too365. padrão de saudação de novas contas de armazenamento é sete dias. Se você não quiser tooset uma política de retenção, insira zero. Se não houver nenhuma política de retenção, cabe tooyou toodelete Olá dados de monitoramento.

   > [!WARNING]
   > Você é cobrado quando exclui manualmente dados de métricas. Dados de análise obsoleta (mais antigos do que sua política de retenção de dados) são excluídos pelo sistema hello, sem nenhum custo. É recomendável definir uma política de retenção com base em quanto tempo deseja que os dados de análise de armazenamento tooretain para sua conta. Confira [Quais são os encargos quando você habilita as métricas de armazenamento?](../common/storage-enable-and-view-metrics.md#what-charges-do-you-incur-when-you-enable-storage-metrics) para obter mais informações.
   >

1. Quando você terminar a configuração de monitoramento hello, selecione **salvar**.

Um conjunto de métricas padrão é exibido nos gráficos na folha de conta de armazenamento hello, bem como folhas de serviço individual da saudação (blob, fila, tabela e arquivo). Depois de habilitar as métricas para um serviço, pode levar até horas tooan para tooappear de dados em seus gráficos. Você pode selecionar **editar** em alguma das métricas de gráfico muito[configurar quais métricas](#how-to-customize-metrics-charts) são exibidas no gráfico de saudação.

Você pode desabilitar a coleção de métricas e registro em log definindo **Status** muito**Off**.

> [!NOTE]
> Armazenamento do Azure usa [armazenamento de tabela](../common/storage-introduction.md#table-storage) toostore métricas de saudação da sua conta de armazenamento e os repositórios Olá métricas em tabelas em sua conta. Para obter mais informações, confira: [Como as métricas são armazenadas](../common/storage-analytics.md#how-metrics-are-stored).
>

## <a name="customize-metrics-charts"></a>Personalizar gráficos de métricas

Use Olá toochoose do procedimento a seguir que tooview de métricas de armazenamento em um gráfico de métricas. 

1. Iniciar, exibindo um gráfico de métricas de armazenamento na Olá portal do Azure. Você pode encontrar os gráficos Olá **folha da conta de armazenamento** e em Olá **métricas** folha para um serviço individual (blob, fila, tabela, arquivo).

   Neste exemplo, trabalhamos com hello seguindo o gráfico exibido no hello **folha da conta de armazenamento**:

   ![Seleção de gráfico no portal do Azure](./media/storage-monitor-storage-account/stg-customize-chart-00.png)

1. Em seguida, clique em qualquer lugar dentro de saudação do hello gráfico tooopen **métrica** folha. Selecione **Editar gráfico** tooopen Olá **Editar gráfico** folha.

   ![Editar botão de gráfico na folha de gráfico](./media/storage-monitor-storage-account/stg-customize-chart-01.png)

1. Em hello **Editar gráfico** folha, selecione Olá **intervalo de tempo** de saudação toodisplay de métricas no gráfico de saudação e hello **service** (blob, fila, tabela, arquivo) cujas métricas que você deseja toodisplay. Aqui, selecionamos Olá toodisplay após métricas da semana para o serviço de blob hello:

   ![Seleção de intervalo e o serviço de tempo na folha do hello Editar gráfico](./media/storage-monitor-storage-account/stg-customize-chart-02.png)

1. Selecione Olá individuais **métricas** você tinha como exibido no gráfico de hello, em seguida, clique em **Okey**. Por exemplo, aqui é escolhida Olá toodisplay *ContainerCount* e *ObjectCount* métricas:

   ![Seleção de métrica individual na folha Editar Gráfico](./media/storage-monitor-storage-account/stg-customize-chart-03.png)

As configurações de gráfico não afeta coleção hello, agregação ou armazenamento de dados na conta de armazenamento de saudação de monitoramento, Olá somente a exibição de dados de métricas de.

### <a name="metrics-availability-in-charts"></a>Disponibilidade de métricas em gráficos

lista de saudação de alterações de métricas disponíveis com base no qual o serviço que você escolheu na lista suspensa de saudação e tipo de unidade de saudação do gráfico de saudação que você está editando. Por exemplo, você só poderá selecionar as métricas de percentual como *PercentNetworkError* e *PercentThrottlingError* se estiver editando um gráfico que exiba as unidades em percentual:

![Gráfico de porcentagem de erro de solicitação em Olá portal do Azure](./media/storage-monitor-storage-account/stg-customize-chart-04.png)

### <a name="metrics-resolution"></a>Resolução de métricas

métricas de saudação selecionado no diagnóstico determina a resolução de saudação das métricas de saudação que estão disponíveis para sua conta:

* O monitoramento **Agregado** fornece métricas como percentuais de entrada/saída, disponibilidade, latência e sucesso. Essas métricas são agregadas de saudação blob, tabela, arquivo e serviços de fila.
* **Por API** fornece a resolução mais refinada, com métricas disponíveis para operações de armazenamento individuais, além de toohello agregações de nível de serviço.

## <a name="configure-metrics-alerts"></a>Configurar alertas de métricas

Você pode criar alertas toonotify quando os limites foram atingidos para métricas de recursos de armazenamento.

1. Olá tooopen **folha de regras de alerta**, role para baixo toohello **monitoramento** seção Olá **folha Menu** e selecione **regras de alerta**.
1. Selecione **adicionar alerta** tooopen Olá **adicionar uma regra de alerta** folha
1. Selecione um **recurso** (blob, arquivo, fila, tabela) de Olá suspensa e insira um **nome** e **descrição** para a nova regra de alerta.
1. Selecione Olá **métrica** para o qual você gostaria que tooadd um alerta, um alerta **condição**e um **limite**. alterações de tipo de unidade de limite de saudação dependendo da métrica de saudação escolhida. Por exemplo, "count" é do tipo de unidade Olá para *ContainerCount*, enquanto a unidade Olá Olá *PercentNetworkError* métrica é uma porcentagem.
1. Selecione Olá **período**. As métricas que atingir ou excederam Olá limite dentro de gatilho de período Olá um alerta.
1. (Opcional) Configurar notificações de **Email** e **Webhook**. Para obter mais informações sobre webhooks, confira [Configurar um webhook em um alerta de métrica do Azure](../../monitoring-and-diagnostics/insights-webhooks-alerts.md). Se você não configurar notificações por email ou webhook, os alertas serão exibidos somente em Olá portal do Azure.

!['Adicionar uma regra de alerta' folha em Olá portal do Azure](./media/storage-monitor-storage-account/stg-alert-rules-01.png)

## <a name="add-metrics-charts-toohello-portal-dashboard"></a>Adicionar gráficos de métricas toohello painel portal

Você pode adicionar gráficos de métricas de armazenamento do Azure para qualquer um dos seu painel do portal de tooyour de contas do armazenamento.

1. Clique em selecionar **Editar painel** ao exibir o painel da saudação [portal do Azure](https://portal.azure.com).
1. Em Olá **bloco galeria**, selecione **localizar blocos por** > **tipo**.
1. Selecione **Tipo** > **Contas de armazenamento**.
1. Em **recursos**, selecione a conta de armazenamento de saudação cujas métricas que você deseja tooadd toohello painel.
1. Selecione **Categorias** > **Monitoramento**.
1. Gráfico de arrastar e soltar Olá lado a lado em seu painel de métrica de saudação desejado exibida. Repita para todas as métricas que deseja exibidas no painel de saudação. Em Olá a imagem a seguir, é realçado hello "Blobs - Total de solicitações" gráfico como um exemplo, mas todos os gráficos de saudação estão disponíveis para posicionamento em seu painel.

   ![Galeria de blocos no portal do Azure](./media/storage-monitor-storage-account/stg-customize-dashboard-01.png)
1. Selecione **feito personalizando** superior de saudação do painel hello quando você terminar adicionando gráficos.

Depois de ter adicionado o painel de tooyour de gráficos, você pode personalizá-los conforme descrito em [personalizar gráficos de métricas](#how-to-customize-metrics-charts).

## <a name="configure-logging"></a>Configurar o registro em log

Você pode instruir o logs de diagnóstico do armazenamento do Azure toosave para leitura, gravação e excluir solicitações de saudação blob, tabela e serviços de fila. política de retenção de dados Olá definir também se aplica a toothese logs.

> [!NOTE]
> O Armazenamento de arquivos do Azure atualmente dá suporte às métricas de Análise de Armazenamento, mas ainda não dá suporte ao registro em log.
>

1. Em Olá [portal do Azure](https://portal.azure.com), selecione **contas de armazenamento**, Olá nome da folha de conta Olá armazenamento conta tooopen Olá armazenamento.
1. Selecione **diagnóstico** em Olá **monitoramento** seção da folha de menu hello.

    ![Item de menu de diagnóstico em monitoramento em Olá portal do Azure.](./media/storage-monitor-storage-account/stg-enable-metrics-00.png)
    
1. Certifique-se de **Status** está definido muito**na**e selecione hello **serviços** para o qual você gostaria que o log de tooenable.

    ![Configure o log no hello portal do Azure.](./media/storage-monitor-storage-account/stg-enable-logging-01.png)
1. Clique em **Salvar**.

Olá logs de diagnóstico são salvos em um contêiner de blob denominado $logs em sua conta de armazenamento. Você pode exibir dados de log de saudação usando um Gerenciador de armazenamento como Olá [Gerenciador de armazenamento do Microsoft](http://storageexplorer.com), ou programaticamente usando a biblioteca de cliente de armazenamento hello ou o PowerShell.

Para obter informações sobre como acessar o contêiner de saudação $logs, consulte [acessar dados de Log e habilitando o log de armazenamento](/rest/api/storageservices/enabling-storage-logging-and-accessing-log-data).

## <a name="next-steps"></a>Próximas etapas

* Encontre mais detalhes sobre [métricas, logs e cobrança](../storage-analytics.md) para Análise de Armazenamento.
* [Habilitar métricas do Armazenamento do Azure e exibir dados de métricas](../storage-enable-and-view-metrics.md) usando o PowerShell e de forma programática com C#.
