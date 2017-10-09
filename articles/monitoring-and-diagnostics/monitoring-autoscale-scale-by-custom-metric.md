---
title: "aaaGet iniciado com escala automática por métrica personalizada no Azure | Microsoft Docs"
description: "Saiba como tooscale o recurso por métrica personalizada no Azure."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: ancav
ms.openlocfilehash: d3e268ec322698d0d367361cd9c156b21e0fb6e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-auto-scale-by-custom-metric-in-azure"></a>Introdução ao dimensionamento automático usando métricas personalizadas no Azure
Este artigo descreve como tooscale o recurso por uma métrica personalizada no portal do Azure.

Azure AutoEscala Monitor aplica-se apenas tooVirtual conjuntos de escala de máquina (VMSS), os serviços de nuvem, planos de serviço de aplicativo e ambientes de serviço de aplicativo. 

# <a name="lets-get-started"></a>Vamos começar
Este artigo pressupõe que você tenha um aplicativo Web com o Application Insights configurado. Se ainda não tiver um, você poderá [configurar o Application Insights para seu site do ASP.NET][1]

- Abra o [portal do Azure][2]
- Clique no ícone de Monitor do Azure no painel de navegação esquerdo hello.
  ![Inicie o Azure Monitor][3]
- Clique em configuração tooview todos os recursos de saudação automática escala é aplicável, juntamente com seu status atual de dimensionamento automático de dimensionamento automático ![descobrir AutoEscala no monitor do Azure][4]
- Abra a folha de 'dimensionamento automático' no Monitor do Azure e selecione um recurso que você deseja tooscale
> Observação: etapas Olá usam um plano de serviço de aplicativo associado a um aplicativo web que tem informações de aplicativo configuradas.
- Na folha de configuração de escala de Olá para o recurso de hello, observe que a contagem atual de instâncias de saudação é 1. Clique em “Habilitar dimensionamento automático”.
  ![Configuração de dimensionamento para um novo aplicativo Web][5]
- Forneça um nome para configuração da escala de saudação e hello, clique em "Adicionar uma regra". Observe as opções de regra de escala de saudação que é aberto em um painel de contexto no lado direito hello. Por padrão, ele define Olá opção tooscale sua instância de contagem em 1 se percetage de CPU de saudação do recurso de saudação exceder 70%. Alterar origem métrica de saudação na parte superior da saudação muito "Application Insights", selecione Olá recurso insights de aplicativo hello 'Resource' suspenso e métrica personalizada de hello, em seguida, selecione com base no qual você deseja tooscale.
  ![Dimensionamento por métrica personalizada][6]
- Semelhante toohello de etapa anterior, adicione uma regra de escala que ampliar e reduzir a contagem de escala de saudação por 1 se a métrica personalizada Olá estiver abaixo do limite.
  ![Dimensionamento com base na CPU][7]
- Definir Olá instância limites. Por exemplo, se você quiser tooscale entre instâncias de 2 a 5 dependendo flutuações de métrica personalizada hello, definir muito '2', 'mínimo' 'máximo' muito '5' e 'default' muito '2'
> Observação: caso há um problema ao ler as métricas de recurso hello e capacidade atual hello está abaixo de capacidade padrão de Olá, em seguida, tooensure disponibilidade de saudação do recurso Olá, AutoEscala será escalável valor padrão de toohello. Se a capacidade atual Olá já for maior que a capacidade padrão, dimensionamento automático não será dimensionado em.
- Clique em "Salvar"

Parabéns. Agora, com êxito criado seu tooauto de configuração de escala dimensionar seu aplicativo web com base em uma métrica personalizada.

> Observação: hello mesmas etapas são aplicável tooget iniciado com uma função de serviço VMSS ou na nuvem.

<!--Reference-->
[1]: https://docs.microsoft.com/en-us/azure/application-insights/app-insights-asp-net
[2]: https://portal.azure.com
[3]: ./media/monitoring-autoscale-scale-by-custom-metric/azure-monitor-launch.png
[4]: ./media/monitoring-autoscale-scale-by-custom-metric/discover-autoscale-azure-monitor.png
[5]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-by-custom-metric.png
[7]: ./media/monitoring-autoscale-scale-by-custom-metric/autoscale-setting-custom-metrics-ai.png
