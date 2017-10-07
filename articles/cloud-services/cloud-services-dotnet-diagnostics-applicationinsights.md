---
title: "aaaTroubleshoot serviços de nuvem usando o Application Insights | Microsoft Docs"
description: "Saiba como o serviço de nuvem tootroubleshoot emite usando dados do Application Insights tooprocess do diagnóstico do Azure."
services: cloud-services
documentationcenter: .net
author: sbtron
manager: timlt
editor: tysonn
ms.assetid: e93f387b-ef29-4731-ae41-0676722accb6
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: saurabh
ms.openlocfilehash: 972924d9e6d1fe33d5c19b006d482de52ffb0ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-cloud-services-using-application-insights"></a>Solucionar problemas de Serviços de Nuvem usando o Application Insights
Com [Azure SDK 2.8](https://azure.microsoft.com/downloads/) e extensão de diagnóstico do Azure 1.5, você pode enviar dados de diagnóstico do Azure para seu serviço de nuvem diretamente tooApplication Insights. Olá logs coletados pelo diagnóstico do Azure&mdash;incluindo logs de aplicativo, Logs de eventos do Windows, os Logs do ETW e contadores de desempenho&mdash;podem ser enviados tooApplication Insights. Em seguida, você pode visualizar essas informações no portal do Application Insights Olá da interface do usuário. Em seguida, você pode usar o hello SDK do Application Insights tooget panorama de métricas e os logs que vêm de seu aplicativo, bem como sistema hello e dados de nível de infraestrutura que vêm do diagnóstico do Azure.

## <a name="configure-azure-diagnostics-toosend-data-tooapplication-insights"></a>Configurar o diagnóstico do Azure toosend dados tooApplication Insights
Siga essas tooset etapas a sua nuvem serviço projeto toosend diagnóstico do Azure dados tooApplication Insights.

1. No Gerenciador de soluções do Visual Studio, clique em uma função e selecione **propriedades** designer de função tooopen hello.

    ![Propriedades da função Gerenciador de Soluções][1]

2. Em Olá **diagnóstico** seção saudação do designer de função, selecione Olá **enviar dados de diagnóstico tooApplication Insights** opção.

    ![Designer de função enviar informações de tooapplication de dados de diagnósticos][2]

3. Na caixa de diálogo de Olá pop-up, selecione o recurso do Application Insights Olá que dados de diagnóstico do Azure Olá toosend devem. caixa de diálogo Olá permite tooselect um recurso existente do Application Insights de sua assinatura ou toomanually especificar uma chave de instrumentação para um recurso do Application Insights. Para saber mais sobre como criar um recurso do Application Insights, confira [Criar um novo recurso do Application Insights](../application-insights/app-insights-create-new-resource.md).

    ![selecionar recurso do application insights][3]

    Depois que você adicionou o recurso do Application Insights hello, chave de instrumentação Olá para esse recurso é armazenada como uma configuração de serviço com o nome da saudação **APPINSIGHTS_INSTRUMENTATIONKEY**. Você pode alterar essa configuração para cada ambiente ou configuração de serviço. toodo portanto, selecione uma configuração diferente de saudação **configuração do serviço** lista e especifique uma nova chave de instrumentação para essa configuração.

    ![selecionar configuração de serviço][4]

    Olá **APPINSIGHTS_INSTRUMENTATIONKEY** configuração será usada pela extensão de diagnóstico do Visual Studio tooconfigure Olá com hello apropriado do Application Insights informações sobre o recurso durante a publicação. configuração de saudação é uma maneira conveniente de definir chaves de instrumentação diferentes para configurações de serviço diferentes. O Visual Studio converter essa configuração e inseri-lo na configuração da extensão pública do diagnóstico Olá durante a saudação processo de publicação. processo de saudação toosimplify de configuração de extensão de diagnóstico Olá com o PowerShell, saída do pacote de saudação do Visual Studio também contém Olá pública XML de configuração com a chave de instrumentação do Application Insights apropriado hello. arquivos de configuração pública Olá são criados na pasta de extensões hello e seguem o padrão de saudação *PaaSDiagnostics.&lt; RoleName&gt;. PubConfig.xml*. Todas as implantações com base em PowerShell podem usar este padrão toomap cada função tooa de configuração.

4) toosend de diagnóstico do Azure tooconfigure todos os contadores de desempenho e logs de nível de erro coletados pelo tooApplication de agente de diagnóstico do Azure Olá Insights, habilitar Olá **enviar dados de diagnóstico tooApplication Insights** opção. 

    Se você quiser toofurther configurar quais dados são enviados tooApplication Insights, você deve editar manualmente Olá *wadcfgx* arquivo para cada função. Consulte [tooApplication de dados toosend de configurar o diagnóstico do Azure Insights](#configure-azure-diagnostics-to-send-data-to-application-insights) toolearn mais sobre como atualizar manualmente a configuração de saudação.

Quando o serviço de nuvem de saudação configurado toosend informações de tooapplication de dados de diagnóstico do Azure, você pode implantá-lo tooAzure normalmente, certificando-se de saudação extensão de diagnóstico do Azure está habilitada. Para saber mais, confira [Como publicar um serviço de nuvem usando o Visual Studio](../vs-azure-tools-publishing-a-cloud-service.md).  

## <a name="viewing-azure-diagnostics-data-in-application-insights"></a>Exibindo dados do Diagnóstico do Azure no Application Insights
Olá telemetria de diagnóstica do Azure aparece na Olá Application Insights recurso configurado para o serviço de nuvem.

Tipos de log de diagnóstico do Azure mapeiam tooApplication conceitos de informações das seguintes maneiras:

* Contadores de desempenho são exibidos como Métricas Personalizadas no Application Insights.
* Logs de Eventos do Windows são mostrados como Rastreamentos e Eventos Personalizados no Application Insights.
* Logs de Aplicativo, logs de ETW e logs de Infraestrutura de Diagnóstico são mostrados como Rastreamentos no Application Insights.

tooview dados de diagnóstico do Azure no Application Insights, siga um destes procedimentos Olá:

* Use [do Metrics explorer](../application-insights/app-insights-metrics-explorer.md) toovisualize qualquer personalizado contadores de desempenho ou contagens de diferentes tipos de eventos de Log de eventos do Windows.

    ![Métricas personalizadas no Metrics Explorer][5]

* Use [pesquisa](../application-insights/app-insights-diagnostic-search.md) toosearch em logs de rastreamento de saudação enviadas pelo diagnóstico do Azure. Por exemplo, se uma exceção não tratada causou Olá função toocrash e reciclagem, informações sobre a exceção de saudação aparece na Olá *aplicativo* canal de *Log de eventos do Windows*. Você pode usar pesquisa toolook em Olá erro de Log de eventos do Windows e obter o rastreamento de pilha completa de saudação para Olá exceção toohelp localizar Olá causa Olá problema.

    ![Pesquisar rastreamentos][6]

## <a name="next-steps"></a>Próximas etapas
* [Adicionar serviço de nuvem Olá SDK do Application Insights tooyour](../application-insights/app-insights-cloudservices.md) toosend dados sobre solicitações, exceções, dependências e qualquer telemetria personalizada de seu aplicativo. Quando combinado com dados de diagnóstico do Azure hello, essas informações você pode obter uma visão completa do seu aplicativo e do sistema, todos na Olá mesmo recurso do Application Insight.  

<!--Image references-->
[1]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/solution-explorer-properties.png
[2]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/role-designer-sendtoappinsights.png
[3]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/select-appinsights-resource.png
[4]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/role-designer-appinsights-serviceconfig.png
[5]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/metrics-explorer-custom-metrics.png
[6]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/search-windowseventlog-error.png
