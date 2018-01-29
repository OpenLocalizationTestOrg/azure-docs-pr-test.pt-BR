---
title: "Integração do SCOM com o Application Insights | Microsoft Docs"
description: "Se você for um usuário do SCOM, monitore o desempenho e diagnostique problemas com o Application Insights. Painéis abrangentes, alertas inteligentes, poderosas ferramentas de diagnóstico e de consultas de análise."
services: application-insights
documentationcenter: 
author: mrbullwinkle
manager: carmonm
ms.assetid: 606e9d03-c0e6-4a77-80e8-61b75efacde0
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/12/2016
ms.author: mbullwin
ms.openlocfilehash: 35ea37b751909e14e616a965462b832e4e51bae0
ms.sourcegitcommit: e462e5cca2424ce36423f9eff3a0cf250ac146ad
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/01/2017
---
# <a name="application-performance-monitoring-using-application-insights-for-scom"></a>Monitoramento de desempenho de aplicativos usando o Application Insights para SCOM
Se você usar o SCOM (System Center Operations Manager) para gerenciar seus servidores, poderá monitorar o desempenho e diagnosticar os problemas de desempenho com a ajuda do [Azure Application Insights](app-insights-asp-net.md). O Application Insights monitora solicitações de entrada do seu aplicativo Web, chamadas REST e SQL de saída, exceções e rastreamentos de log. Ele fornece painéis com gráficos de métricas e alertas inteligentes, bem como poderosas consultas analíticas e pesquisa de diagnóstico sobre essa telemetria. 

Você pode ativar o monitoramento do Application Insights usando um pacote de gerenciamento do SCOM.

## <a name="before-you-start"></a>Antes de começar
Supomos que:

* Você esteja familiarizado com o SCOM e use o SCOM 2012 R2 ou 2016 para gerenciar os servidores Web do IIS.
* Você já tenha instalado nos servidores um aplicativo Web que você deseja monitorar com o Application Insights.
* A versão da estrutura de aplicativo seja o .NET 4.5 ou posterior.
* Você tem acesso a uma assinatura no [Microsoft Azure](https://azure.com) e pode entrar no [portal do Azure](https://portal.azure.com). Se sua organização já tiver uma assinatura, sua conta da Microsoft poderá ser adicionada.

(A equipe de desenvolvimento pode criar o [SDK do Application Insights](app-insights-asp-net.md) no aplicativo Web. Essa instrumentação do tempo de compilação dá maior flexibilidade na escrita de telemetria personalizada. No entanto, não importa: você pode seguir as etapas descritas aqui, com ou sem o SDK interno).

## <a name="one-time-install-application-insights-management-pack"></a>(Uma vez) Instalar o pacote de gerenciamento do Application Insights
No computador em que você executa o Operations Manager:

1. Desinstale qualquer versão antiga do pacote de gerenciamento:
   1. No Operations Manager, abra Administração, Pacotes de Gerenciamento. 
   2. Exclua a versão antiga.
2. Baixe e instale o pacote de gerenciamento do catálogo.
3. Reinicie o Operations Manager.

## <a name="create-a-management-pack"></a>Criar um pacote de gerenciamento
1. No Operations Manager, abra **Criação**, **.NET... com Application Insights**, **Assistente para Adicionar Monitoramento** e escolha novamente **.NET... com Application Insights**.
   
    ![](./media/app-insights-scom/020.png)
2. Dê à configuração o nome do seu aplicativo. (Você precisa instrumentar um aplicativo por vez).
   
    ![](./media/app-insights-scom/030.png)
3. Na mesma página do assistente, crie um novo pacote de gerenciamento ou selecione um pacote criado anteriormente para o Application Insights.
   
     (O [pacote de gerenciamento](https://technet.microsoft.com/library/cc974491.aspx) do Application Insights é um modelo no qual você cria uma instância. Você pode reutilizar a mesma instância posteriormente).

    ![Na guia Propriedades Gerais, digite o nome do aplicativo. Clique em Novo e digite um nome para um pacote de gerenciamento. Clique em OK e em Avançar.](./media/app-insights-scom/040.png)

1. Escolha um aplicativo que você deseja monitorar. O recurso de pesquisa procura entre aplicativos instalados nos servidores.
   
    ![Na guia O Que Monitorar, clique em Adicionar, digite parte do nome do aplicativo, clique em Pesquisar, escolha o aplicativo e, então, Adicionar, OK.](./media/app-insights-scom/050.png)
   
    O campo Escopo de monitoramento opcional pode ser usado para especificar um subconjunto de seus servidores se você não quiser monitorar o aplicativo em todos os servidores.
2. Na próxima página do assistente, forneça suas credenciais para entrar no Microsoft Azure.
   
    Nessa página, você deve escolher o recurso Application Insights onde deseja que os dados de telemetria sejam analisados e exibidos. 
   
   * Se o aplicativo tiver sido configurado para o Application Insights durante o desenvolvimento, selecione o recurso existente.
   * Caso contrário, crie um novo recurso nomeado para o aplicativo. Se houver outros aplicativos que sejam componentes do mesmo sistema, coloque-os no mesmo grupo de recursos para facilitar o gerenciamento da telemetria.
     
     Você pode alterar essas configurações posteriormente.
     
     ![Na guia de configurações do Application Insights, clique em 'entrar' e forneça suas credenciais de conta da Microsoft para o Azure. Em seguida, escolha uma assinatura, um grupo de recursos e um recurso.](./media/app-insights-scom/060.png)
3. Conclua o assistente.
   
    ![Clicar em Criar](./media/app-insights-scom/070.png)

Repita esse procedimento para cada aplicativo que você deseja monitorar.

Se você precisar alterar as configurações mais tarde, abra as propriedades do monitor na janela de criação novamente.

![Em Criação, selecione Monitoramento de Desempenho de Aplicativo .NET com o Application Insights, selecione o monitor e clique em Propriedades.](./media/app-insights-scom/080.png)

## <a name="verify-monitoring"></a>Verificar o monitoramento
O monitor instalado procura seu aplicativo em todos os servidores. Onde ele encontrar o aplicativo, configurará o Application Insights Status Monitor para monitorar o aplicativo. Se necessário, primeiro ele instala o Monitor de Status no servidor.

Você pode verificar quais instâncias do aplicativo encontrado:

![Em Monitoramento, abra o Application Insights](./media/app-insights-scom/100.png)

## <a name="view-telemetry-in-application-insights"></a>Exibir a telemetria no Application Insights
No [portal do Azure](https://portal.azure.com), navegue até o recurso para o seu aplicativo. Você [vê gráficos mostrando telemetria](app-insights-dashboards.md) do seu aplicativo. (Se ele ainda não tiver sido mostrado na página principal, clique no Live Metrics Stream).

## <a name="next-steps"></a>Próximas etapas
* [Configure um painel](app-insights-dashboards.md) para reunir os gráficos mais importantes que monitoram esse e outros aplicativos.
* [Saiba mais sobre métricas](app-insights-metrics-explorer.md)
* [Configurar alertas](app-insights-alerts.md)
* [Diagnosticar problemas de desempenho](app-insights-detect-triage-diagnose.md)
* [Consultas de análise poderosas](app-insights-analytics.md)
* [Testes de disponibilidade na Web](app-insights-monitor-web-app-availability.md)

