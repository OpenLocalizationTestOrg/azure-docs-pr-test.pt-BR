---
title: "aaaHow toomonitor um serviço de nuvem | Microsoft Docs"
description: "Saiba como toomonitor serviços de nuvem usando Olá portal clássico do Azure."
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: 5c48d2fb-b8ea-420f-80df-7aebe2b66b1b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2015
ms.author: adegeo
ms.openlocfilehash: ee98c56e0b98b85d75a5c1d796800069c4f06d20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomonitor-cloud-services"></a>Como os serviços de nuvem tooMonitor
[!INCLUDE [disclaimer](../../includes/disclaimer.md)]

Você pode monitorar `key` métricas de desempenho para os serviços de nuvem em Olá portal clássico do Azure. Você pode definir a saudação detalhado para cada função de serviço e nível de monitoramento toominimal e pode personalizar a saudação telas de monitoramento. Dados de monitoramento detalhados são armazenados em uma conta de armazenamento, que pode ser acessado fora Olá portal. 

Monitores de monitoramento no portal clássico do Azure de saudação são altamente configurável. Você pode escolher métricas Olá deseja toomonitor na lista de métricas de Olá Olá **Monitor** página e você pode escolher quais métricas tooplot nos gráficos de métricas no hello **Monitor** painel de página e hello. 

## <a name="concepts"></a>Conceitos
Por padrão, o monitoramento mínimo é fornecido para um novo serviço de nuvem usando os contadores de desempenho coletados do sistema de operacional de host Olá para instâncias de funções hello (máquinas virtuais). mínimo de métricas de saudação é limitada tooCPU porcentagem, dados, para dados, taxa de transferência de leitura de disco e taxa de transferência de gravação do disco. Configurando o monitoramento detalhado, você pode receber métricas adicionais com base nos dados de desempenho em máquinas virtuais de saudação (instâncias de função). métricas detalhadas Olá permitem uma análise mais próxima dos problemas que ocorrem durante operações de aplicativo.

Por padrão, dados de contador de desempenho de instâncias de função é de amostra e transferidos da instância de função hello em intervalos de 3 minutos. Quando você habilita o monitoramento detalhado, dados de contador de desempenho bruto de saudação são agregados para cada instância de função e em instâncias de função para cada função em intervalos de 5 minutos, 1 hora e 12 horas. Olá dados agregados são limpos após 10 dias.

Depois de habilitar o monitoramento detalhado, Olá agregado dados de monitoramento são armazenados em tabelas na conta de armazenamento. tooenable detalhado de monitoramento para uma função, você deve configurar uma cadeia de caracteres de conexão de diagnóstico que vincula toohello conta de armazenamento. Você pode usar contas de armazenamento diferentes para funções diferentes.

Os custos de armazenamento permitindo que aumenta de monitoramento detalhada relacionado toodata armazenamento, transferência de dados e transações de armazenamento. O monitoramento mínimo não requer uma conta de armazenamento. dados de saudação para métricas de saudação que são expostos no nível de monitoramento mínimo Olá não são armazenados em sua conta de armazenamento, mesmo que você defina Olá tooverbose nível de monitoramento.

## <a name="how-to-configure-monitoring-for-cloud-services"></a>Tutorial: Configurar o monitoramento para serviços de nuvem
Use Olá seguindo os procedimentos tooconfigure detalhado ou mínimo de monitoramento no hello portal clássico do Azure. 

### <a name="before-you-begin"></a>Antes de começar
* Criar um *clássico* Olá de toostore de conta de armazenamento dados de monitoramento. Você pode usar contas de armazenamento diferentes para funções diferentes. Para obter mais informações, consulte [como uma conta de armazenamento do toocreate](../storage/common/storage-create-storage-account.md#create-a-storage-account).
* Habilite o Diagnóstico do Azure para as funções do seu serviço de nuvem. Consulte [Configurando os diagnósticos para os Serviços de Nuvem](cloud-services-dotnet-diagnostics.md).

Verifique se a cadeia de caracteres de conexão de diagnóstico hello está presente na configuração da função hello. Você não pode ativar o monitoramento detalhado até que você habilitar o diagnóstico do Azure e inclui uma cadeia de caracteres de conexão de diagnóstico na configuração de funções hello.   

> [!NOTE]
> Projetos direcionados 2.5 do SDK do Azure não incluíam o cadeia de caracteres de conexão de diagnóstico Olá automaticamente no modelo de projeto de saudação. Para esses projetos, você precisa toomanually Adicionar configuração de função de toohello Olá diagnóstico conexão cadeia de caracteres.
> 
> 

**toomanually Adicionar configuração de tooRole de cadeia de caracteres de conexão de diagnóstico**

1. Projeto de serviço de nuvem Olá aberto no Visual Studio
2. Clique duas vezes em Olá **função** tooopen Olá designer de função e selecione Olá **configurações** guia
3. Procure por uma configuração chamada **Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString**. 
4. Se essa configuração não estiver presente, clique em Olá **Adicionar configuração** botão tooadd-toohello configuração e alteração Olá tipo para Olá nova configuração muito**ConnectionString**
5. Definir valor Olá Olá de cadeia de caracteres de conexão clicando no hello **...**  botão. Isso abrirá uma caixa de diálogo permitindo que você tooselect uma conta de armazenamento.
   
    ![Configurações do Visual Studio](./media/cloud-services-how-to-monitor/CloudServices_Monitor_VisualStudioDiagnosticsConnectionString.png)

### <a name="toochange-hello-monitoring-level-tooverbose-or-minimal"></a>Olá toochange tooverbose nível de monitoramento ou mínima
1. Em Olá [portal clássico do Azure](https://manage.windowsazure.com/), abra Olá **configurar** página para implantação de serviço de nuvem hello.
2. Em **Nível**, clique em **Detalhado** ou **Mínimo**. 
3. Clique em **Salvar**.

Após você ativar o monitoramento detalhado, você deve começar a ver Olá dados de monitoramento no portal clássico do Azure de saudação na hora de saudação.

dados do contador de desempenho bruto Hello e dados agregados de monitoramentos são armazenados na conta de armazenamento Olá nas tabelas qualificados por ID de implantação Olá para as funções hello. 

## <a name="how-to-receive-alerts-for-cloud-service-metrics"></a>Tutorial: Receber alertas para métricas dos serviços de nuvem
Você pode receber alertas baseados nas métricas de monitoramento do serviço de nuvem. Em Olá **Management Services** Olá de página do portal clássico do Azure, você pode criar uma regra tootrigger um alerta quando a métrica de saudação escolhida atinge um valor que você especificar. Você também pode escolher toohave enviado email quando Olá alerta for disparado. Para saber mais, confira [Como: receber notificações de alerta e gerenciar regras de alerta no Azure](http://go.microsoft.com/fwlink/?LinkId=309356).

## <a name="how-to-add-metrics-toohello-metrics-table"></a>Como: adicionar a tabela de métricas de toohello de métricas
1. Em Olá [portal clássico do Azure](http://manage.windowsazure.com/), abra Olá **Monitor** página Olá serviço de nuvem.
   
    Por padrão, a tabela de métricas de saudação exibe um subconjunto das métricas disponíveis hello. Olá ilustração métricas no modo detalhado saudação padrão para um serviço de nuvem, que é o contador de desempenho memória \ MBytes toohello limitado, com dados agregados no nível de função hello. Use **adicionar métricas** Olá a agregação adicionais tooselect e toomonitor de métricas de nível de função no portal clássico do Azure.
   
    ![Exibição detalhada](./media/cloud-services-how-to-monitor/CloudServices_DefaultVerboseDisplay.png)
2. tabela de métricas da toohello tooadd métricas:
   
   1. Clique em **adicionar métricas** tooopen **escolher métricas**, conforme mostrado abaixo.
      
       métrica de disponível primeiro Olá é expandido tooshow opções que estão disponíveis. Para cada métrica, a opção do topo Olá exibe dados agregados de monitoramentos para todas as funções. Além disso, você pode escolher funções individuais toodisplay dados.
      
       ![Adicionar Métricas](./media/cloud-services-how-to-monitor/CloudServices_AddMetrics.png)
   2. tooselect toodisplay de métricas
      
      * Clique em Olá a seta para baixo, Olá tooexpand métrica Olá opções de monitoramento.
      * Olá selecione a caixa de seleção para cada opção que deseja toodisplay de monitoramento.
        
        Você pode exibir a métrica too50 na tabela de métricas de saudação.
        
        > [!TIP]
        > No monitoramento detalhado, lista de métricas de saudação pode conter várias métricas. toodisplay uma barra de rolagem, passe o mouse sobre Olá direita da caixa de diálogo de saudação. lista de Olá toofilter, clique Olá ícone de pesquisa e insira o texto na caixa de pesquisa hello, conforme mostrado abaixo.
        > 
        > 
        
        ![Pesquisa de métricas adicionadas](./media/cloud-services-how-to-monitor/CloudServices_AddMetrics_Search.png)
3. Após concluir a seleção de métricas, clique em OK (marca de seleção).
   
    Olá métricas selecionadas são adicionadas toohello tabela de métricas, conforme mostrado abaixo.
   
    ![métricas de monitoramento](./media/cloud-services-how-to-monitor/CloudServices_Monitor_UpdatedMetrics.png)
4. toodelete uma métrica da tabela de métricas de saudação, clique em tooselect métrica Olá e depois clique em **excluir métrica**. (Você poderá ver **Excluir Métricas** somente quando uma métrica for selecionada).

### <a name="tooadd-custom-metrics-toohello-metrics-table"></a>tabela de métricas de toohello tooadd métricas personalizadas
Olá **detalhado** nível de monitoramento fornece uma lista de métricas padrão que você pode monitorar no portal de saudação. Além disso toothese você pode monitorar qualquer métricas personalizadas ou contadores de desempenho definidos por seu aplicativo por meio do portal hello.

Olá etapas a seguir pressupõem que você tenha ativado **detalhado** nível de monitoramento e configurou seus contadores de desempenho personalizados de toocollect e transferência de aplicativo. 

contadores de desempenho personalizados Olá toodisplay em Olá portal, você precisa tooupdate Olá configuração em wad-control-container:

1. Abrir o blob wad-control-container de saudação em sua conta de armazenamento de diagnóstico. Você pode usar o Visual Studio ou outra toodo de Gerenciador de armazenamento isso.
   
    ![Gerenciador de Servidores do Visual Studio](./media/cloud-services-how-to-monitor/CloudServices_Monitor_VisualStudioBlobExplorer.png)
2. Navegar usando saudação padrão de caminho de blob Olá **RoleName/DeploymentId/RoleInstance** configuração de saudação toofind para sua instância de função. 
   
    ![Gerenciador de Armazenamento do Visual Studio](./media/cloud-services-how-to-monitor/CloudServices_Monitor_VisualStudioStorage.png)
3. Baixar o arquivo de configuração de saudação para sua instância de função e atualizá-lo tooinclude nenhum contador de desempenho personalizados. Por exemplo, toomonitor *Bytes de gravação de disco/s* para hello *unidade C* adicionar seguintes Olá em **PerformanceCounters\Subscriptions** nó
   
    ```xml
    <PerformanceCounterConfiguration>
    <CounterSpecifier>\LogicalDisk(C:)\Disk Write Bytes/sec</CounterSpecifier>
    <SampleRateInSeconds>180</SampleRateInSeconds>
    </PerformanceCounterConfiguration>
    ```
4. Salve alterações hello e carregamento Olá configuração arquivo back toohello substituindo o mesmo local Olá arquivo existente no blob de saudação.
5. Alternar para o modo tooVerbose em Olá configuração do portal clássica do Azure. Se você estivesse em modo detalhado já terá tootoggle tooverbose de toominimal e vice-versa.
6. o contador de desempenho personalizados Olá estarão disponível em Olá **adicionar métricas** caixa de diálogo. 

## <a name="how-to-customize-hello-metrics-chart"></a>Como: personalizar o gráfico de métricas de saudação
1. Na tabela de métricas de saudação, selecione too6 tooplot de métricas no gráfico de métricas de saudação. tooselect uma métrica, clique em caixa de seleção de saudação em seu lado esquerdo. tooremove uma métrica do gráfico de métricas hello, desmarque sua caixa de seleção na tabela de métricas de saudação.
   
    Como selecionar métricas na tabela de métricas de saudação, métricas de saudação são adicionadas toohello gráfico de métricas. Em uma exibição específica, uma **n mais** lista suspensa contém cabeçalhos de métrica que não se ajusta a exibição de saudação.
2. tooswitch entre exibir valores relativos (valor final somente para cada métrica) e valores absolutos (eixo de Y exibido), selecione relativo ou absoluto na parte superior de saudação do gráfico de saudação.
   
    ![Relativo ou Absoluto](./media/cloud-services-how-to-monitor/CloudServices_Monitor_RelativeAbsolute.png)
3. gráfico de métricas Olá do intervalo de tempo de Olá toochange exibe, selecione 1 hora, 24 horas ou 7 dias na parte superior de saudação do gráfico de saudação.
   
    ![Período de exibição do monitoramento](./media/cloud-services-how-to-monitor/CloudServices_Monitor_DisplayPeriod.png)
   
    No gráfico de métricas do painel hello, método hello para métricas de plotagem é diferente. Um conjunto padrão de métricas está disponível e métricas são adicionadas ou removidas, selecionando o cabeçalho de métrica de saudação.

### <a name="toocustomize-hello-metrics-chart-on-hello-dashboard"></a>gráfico de métricas de saudação toocustomize no painel de saudação
1. Abra o painel de Olá Olá serviço de nuvem.
2. Adicionar ou remover métricas de gráfico de saudação:
   
   * tooplot uma nova caixa de seleção Olá métrica, selecione para métrica Olá nos cabeçalhos de gráfico de saudação. Em uma exibição específica, clique em Olá seta por  ***n* ? métricas** tooplot não é possível exibir uma área de cabeçalho Olá métrica do gráfico.
   * toodelete uma métrica que é plotada no gráfico de hello, Olá desmarque a caixa de seleção por seu cabeçalho.
   
3. Alterne entre exibições **Relativas** e **Absoluta**.
4. Escolha 1 hora, 24 horas ou 7 dias de dados toodisplay.

## <a name="how-to-access-verbose-monitoring-data-outside-hello-azure-classic-portal"></a>Como: acessar dados de monitoramento detalhados fora Olá portal clássico do Azure
Dados de monitoramento detalhados são armazenados em tabelas em contas de armazenamento Olá que você especificar para cada função. Para cada implantação de serviço de nuvem, seis tabelas são criadas para a função hello. Duas tabelas são criadas para cada (5 minutos, 1 hora e 12 horas). Uma dessas tabelas armazena as agregações de nível de função; Olá outras agregações de repositórios de tabela para instâncias de função. 

os nomes de tabela Olá têm Olá formato a seguir:

```
WAD*deploymentID*PT*aggregation_interval*[R|RI]Table
```

onde:

* *deploymentID* é hello GUID atribuído toohello implantação de serviço de nuvem
* *aggregation_interval* = 5M, 1H ou 12H
* agregações de nível de função = R
* agregações para instâncias de função = RI

Por exemplo, hello tabelas a seguir seriam armazenar dados de monitoramento detalhados agregados em intervalos de 1 hora:

```
WAD8b7c4233802442b494d0cc9eb9d8dd9fPT1HRTable (hourly aggregations for hello role)

WAD8b7c4233802442b494d0cc9eb9d8dd9fPT1HRITable (hourly aggregations for role instances)
```
