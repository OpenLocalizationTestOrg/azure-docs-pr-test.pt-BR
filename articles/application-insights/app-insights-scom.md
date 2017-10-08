---
title: "a integração com o Application Insights aaaSCOM | Microsoft Docs"
description: "Se você for um usuário do SCOM, monitore o desempenho e diagnostique problemas com o Application Insights. Painéis abrangentes, alertas inteligentes, poderosas ferramentas de diagnóstico e de consultas de análise."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 606e9d03-c0e6-4a77-80e8-61b75efacde0
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/12/2016
ms.author: bwren
ms.openlocfilehash: ee9ad462610fd916098a0e292c5bd44f2a873c10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="application-performance-monitoring-using-application-insights-for-scom"></a>Monitoramento de desempenho de aplicativos usando o Application Insights para SCOM
Se você usar o System Center Operations Manager (SCOM) toomanage seus servidores, você pode monitorar o desempenho e diagnosticar problemas de desempenho com a Ajuda de saudação do [Azure Application Insights](app-insights-asp-net.md). O Application Insights monitora solicitações de entrada do seu aplicativo Web, chamadas REST e SQL de saída, exceções e rastreamentos de log. Ele fornece painéis com gráficos de métricas e alertas inteligentes, bem como poderosas consultas analíticas e pesquisa de diagnóstico sobre essa telemetria. 

Você pode ativar o monitoramento do Application Insights usando um pacote de gerenciamento do SCOM.

## <a name="before-you-start"></a>Antes de começar
Supomos que:

* Você está familiarizado com o SCOM e usar o SCOM 2012 R2 ou 2016 toomanage o IIS servidores da web.
* Você já tiver instalado nos servidores de um aplicativo web que você deseja toomonitor com o Application Insights.
* A versão da estrutura de aplicativo seja o .NET 4.5 ou posterior.
* Você tem acesso tooa assinatura em [Microsoft Azure](https://azure.com) e pode entrar toohello [portal do Azure](https://portal.azure.com). Sua organização pode ter uma assinatura e pode adicionar sua tooit de conta da Microsoft.

(equipe de desenvolvimento Olá pode criar hello [SDK do Application Insights](app-insights-asp-net.md) no aplicativo web de saudação. Essa instrumentação do tempo de compilação dá maior flexibilidade na escrita de telemetria personalizada. No entanto, não importa: você pode seguir etapas Olá descritas aqui, com ou sem Olá SDK incorporado.)

## <a name="one-time-install-application-insights-management-pack"></a>(Uma vez) Instalar o pacote de gerenciamento do Application Insights
Na máquina de saudação onde você executa o Operations Manager:

1. Desinstale qualquer versão antiga do pacote de gerenciamento de saudação:
   1. No Operations Manager, abra Administração, Pacotes de Gerenciamento. 
   2. Exclua a versão antiga do hello.
2. Baixe e instale o pacote de gerenciamento de saudação do catálogo de saudação.
3. Reinicie o Operations Manager.

## <a name="create-a-management-pack"></a>Criar um pacote de gerenciamento
1. No Operations Manager, abra **Criação**, **.NET... com Application Insights**, **Assistente para Adicionar Monitoramento** e escolha novamente **.NET... com Application Insights**.
   
    ![](./media/app-insights-scom/020.png)
2. Configuração de saudação do nome depois de seu aplicativo. (Necessário tooinstrument um aplicativo por vez.)
   
    ![](./media/app-insights-scom/030.png)
3. Olá na mesma página do assistente, crie um novo gerenciamento de pacote, ou selecione um pacote que você criou anteriormente para o Application Insights.
   
     (Olá Application Insights [pacote de gerenciamento](https://technet.microsoft.com/library/cc974491.aspx) é um modelo, na qual você cria uma instância. Você pode reutilizar Olá mesmo instância mais tarde.)

    ![Na guia Propriedades gerais de Olá, digite o nome de saudação do aplicativo hello. Clique em Novo e digite um nome para um pacote de gerenciamento. Clique em OK e em Avançar.](./media/app-insights-scom/040.png)

1. Escolha um aplicativo que você deseja toomonitor. o recurso de pesquisa Olá pesquisa entre aplicativos instalados em seus servidores.
   
    ![Na guia que tooMonitor, clique em Adicionar, digite parte do nome do aplicativo hello, clique em Pesquisar, escolha o aplicativo hello e, em seguida, adicionar, Okey.](./media/app-insights-scom/050.png)
   
    campo de escopo de monitoramento opcional Olá pode ser usado toospecify um subconjunto dos seus servidores, se você não quiser toomonitor Olá aplicativo em todos os servidores.
2. Na próxima página do assistente hello, primeiro você deve fornecer toosign suas credenciais no tooMicrosoft do Azure.
   
    Nessa página, você escolher o recurso do Application Insights Olá onde você deseja toobe de dados de telemetria Olá analisados e exibidos. 
   
   * Se o aplicativo hello foi configurado para o Application Insights durante o desenvolvimento, selecione o recurso existente.
   * Caso contrário, crie um novo recurso chamado para o aplicativo hello. Se houver outros aplicativos que são componentes de saudação mesmo sistema, colocá-los em Olá mesmo grupo de recursos, toomake acesso toohello telemetria mais fácil toomanage.
     
     Você pode alterar essas configurações posteriormente.
     
     ![Na guia de configurações do Application Insights, clique em 'entrar' e forneça suas credenciais de conta da Microsoft para o Azure. Em seguida, escolha uma assinatura, um grupo de recursos e um recurso.](./media/app-insights-scom/060.png)
3. Assistente de saudação concluída.
   
    ![Clicar em Criar](./media/app-insights-scom/070.png)

Repita esse procedimento para cada aplicativo que você deseja toomonitor.

Se você precisar de configurações de toochange mais tarde, abra novamente as propriedades de saudação do monitor de saudação da janela de criação de saudação.

![Em Criação, selecione Monitoramento de Desempenho de Aplicativo .NET com o Application Insights, selecione o monitor e clique em Propriedades.](./media/app-insights-scom/080.png)

## <a name="verify-monitoring"></a>Verificar o monitoramento
monitor de saudação que você instalou pesquisas para seu aplicativo em todos os servidores. Onde encontrar o aplicativo hello, ele configura o Application Insights Status Monitor toomonitor Olá aplicativo. Se necessário, ele instala primeiro Status Monitor no servidor de saudação.

Você pode verificar quais instâncias do aplicativo hello encontrado:

![Em Monitoramento, abra o Application Insights](./media/app-insights-scom/100.png)

## <a name="view-telemetry-in-application-insights"></a>Exibir a telemetria no Application Insights
Em Olá [portal do Azure](https://portal.azure.com), procurar toohello recursos para seu aplicativo. Você [vê gráficos mostrando telemetria](app-insights-dashboards.md) do seu aplicativo. (Se ele ainda não mostrado para cima na página principal do hello ainda, clique em fluxo ao vivo de métricas.)

## <a name="next-steps"></a>Próximas etapas
* [Configurar um painel](app-insights-dashboards.md) gráficos mais importantes do hello juntos toobring este e outros aplicativos de monitoramento.
* [Saiba mais sobre métricas](app-insights-metrics-explorer.md)
* [Configurar alertas](app-insights-alerts.md)
* [Diagnosticar problemas de desempenho](app-insights-detect-triage-diagnose.md)
* [Consultas de análise poderosas](app-insights-analytics.md)
* [Testes de disponibilidade na Web](app-insights-monitor-web-app-availability.md)

