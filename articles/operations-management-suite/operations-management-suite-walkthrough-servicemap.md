---
title: "Mapa de solução de aaaService self individual demonstração | Microsoft Docs"
description: "Mapa de serviço é uma solução no OMS Operations Management Suite () que detecta automaticamente os componentes do aplicativo no Windows e mapas e sistemas Linux Olá comunicação entre serviços.  Esta é uma demonstração de seu próprio ritmo self que percorre o uso do mapa de serviço tooidentify e diagnosticar um problema simulado em um aplicativo web."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 9dc437b9-e83c-45da-917c-cb4f4d8d6333
ms.service: operations-management-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: bwren
ms.openlocfilehash: 13f26241cd55a9b35c07d6ca52760a968abffc64
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="operations-management-suite-oms-self-paced-demo---service-map"></a>Demonstração individualizada do OMS (Operations Management Suite) - Mapa de Serviço
Esta é uma demonstração self individual que orienta a usar Olá [solução de mapa de serviço](operations-management-suite-service-map.md) no Operations Management Suite (OMS) tooidentify e diagnosticar um problema simulado em um aplicativo web.  Mapa de serviço detecta automaticamente os componentes do aplicativo em sistemas Windows e Linux e mapas Olá comunicação entre serviços.  Ele também consolida os dados coletados por outros tooassist de serviços do OMS na análise de desempenho e identificar problemas.  Você também usará [pesquisas de log na análise de Log](../log-analytics/log-analytics-log-searches.md) toodrill para baixo nos dados coletados no problema na ordem tooidentify Olá raiz.


## <a name="scenario-description"></a>Descrição do cenário
Você acabou de receber uma notificação de que o aplicativo de Portal do cliente ACME hello está tendo problemas de desempenho.  Olá única informação que você tem é que esses problemas iniciado aproximadamente 4:00 am PST hoje.  Não estiver completamente certo de todos os componentes de saudação portal Olá é dependente que não seja um conjunto de servidores web.  

## <a name="components-and-features-used"></a>Componentes e recursos usados
- [Solução do Mapa de Serviço](operations-management-suite-service-map.md)
- [Pesquisas de log do Log Analytics](../log-analytics/log-analytics-log-searches.md)


## <a name="walk-through"></a>Passo a passo

### <a name="1-connect-toohello-oms-experience-center"></a>1. Conecte-se toohello OMS experiência central
Este passo a passo usa Olá [Operations Management Suite experiência Center](https://experience.mms.microsoft.com/) que fornece um ambiente completo de OMS com dados de exemplo. Siga este link para iniciar, forneça suas informações e selecione Olá **Insight and Analytics** cenário.


### <a name="2-start-service-map"></a>2. Iniciar o Mapa de Serviço
Iniciar a solução de mapa de serviço Olá clicando no hello **mapa de serviço** lado a lado.

![Bloco Mapa de Serviço](media/operations-management-suite-walkthrough-servicemap/tile.png)

console de mapa de serviço Olá é exibido.  Em Olá painel esquerdo é uma lista de computadores em seu ambiente com o agente de mapa de serviço Olá instalado.  Você selecionará Olá computador que você tooview desta lista.

![Lista de computadores](media/operations-management-suite-walkthrough-servicemap/computer-list.png)


### <a name="3-view-computer"></a>3. Exibir computador
Sabemos que os servidores de web hello são chamados AcmeWFE001 e AcmeWFE002, para que esta parece ser um lugar razoável toostart.  Clique em **AcmeWFE001**.  Isso exibe o mapa de saudação para AcmeWFE001 e todas as suas dependências.  Você pode ver quais processos estão em execução no computador selecionado hello e quais serviços externos se comunicam com.

![Servidor Web](media/operations-management-suite-walkthrough-servicemap/web-server.png)

Estamos preocupados sobre desempenho de saudação do nosso web aplicativo então clique na Olá **AcmeAppPool (Pool de aplicativos do IIS)** processo.  Exibe detalhes de saudação para esse processo e destaca as suas dependências.  

![Pool de Aplicativos](media/operations-management-suite-walkthrough-servicemap/app-pool.png)


### <a name="4-change-time-window"></a>4. Alterar janela do tempo

Ouvimos problema Olá iniciado às 4:00 AM, vamos examinar o que estava acontecendo no momento. Clique em **intervalo de tempo** e alterar Olá tempo too4: 00 AM PST (lembre-Olá data atual e ajustar seu fuso horário local) com uma duração de 20 minutos.

![Seletor de Tempo](./media/operations-management-suite-walkthrough-servicemap/time-picker.png)


### <a name="5-view-alert"></a>5. Exibir alerta

Agora vemos que Olá **acmetomcat** dependência tem um alerta exibido, que é o nosso problema potencial.  Clique no ícone de alerta de saudação em **acmetomcat** tooshow detalhes Olá alerta hello.  Podemos ver que a utilização da CPU está crítica e podemos expandi-la para obter mais detalhes.  Provavelmente é isso que está causando o desempenho lento. 

![Alerta](./media/operations-management-suite-walkthrough-servicemap/alert.png)


### <a name="6-view-performance"></a>6. Exibir desempenho

Vamos examinar o **acmetomcat** com mais atenção.  Clique em Olá superior direita do **acmetomcat** e selecione **carregar o mapa de servidor** tooshow Olá detalhes e as dependências para esta máquina. Pode, em seguida, analisamos um pouco mais esses tooverify de contadores de desempenho nosso suspeita.  Selecione Olá **desempenho** saudação do guia toodisplay [contadores de desempenho coletados pela análise de Log](../log-analytics/log-analytics-data-sources-performance-counters.md) pelo intervalo de tempo de saudação.  Podemos ver que estamos periódicos picos de saudação de processador e memória.

![Desempenho](./media/operations-management-suite-walkthrough-servicemap/performance.png)


### <a name="7-view-change-tracking"></a>7. Exibir controle de alterações
Vejamos se conseguimos descobrir o que pode ter causado essa utilização elevada.  Clique em Olá **resumo** guia.  Isso fornece informações que o OMS coletou de computador hello como falha conexões, alertas críticos e alterações de software.  Seções com informações recentes interessantes já devem ser expandidas, e você pode expandir outras informações de tooinspect seções que eles contêm.


Se o **Controle de Alterações** ainda não estiver aberto, expanda-o.  Isso mostra as informações coletadas pelo Olá [solução controle de alterações](../log-analytics/log-analytics-change-tracking.md).  Parece que houve uma alteração do software feita durante a janela do tempo.  Clique em **Software** tooget detalhes.  Um processo de backup foi adicionado toohello máquina logo após 4:00 AM, então isso aparece veículo de saudação do toobe de recursos em excesso Olá sendo consumida.

![Controle de alterações](./media/operations-management-suite-walkthrough-servicemap/change-tracking.png)



### <a name="8-view-details-in-log-search"></a>8. Exibir detalhes na Pesquisa de Logs
Podemos pode verificar isso ainda mais examinando Olá informações detalhadas de desempenho coletadas no repositório de análise de Log de saudação.  Clique em Olá **alertas** guia novamente e, em seguida, em uma saudação **alta utilização da CPU** alertas.  Clique em **Mostrar na Pesquisa de Logs**.  Isso abre a janela de pesquisa de Log de saudação onde você pode executar [pesquisas de log](../log-analytics/log-analytics-log-searches.md) contra os dados armazenados no repositório de saudação.  Mapa de serviço já preenchido um queriy nos tooretrieve alerta de saudação estamos interessados.  

![Pesquisa de log](./media/operations-management-suite-walkthrough-servicemap/log-search.png)


### <a name="9-open-saved-search"></a>9. Abrir pesquisa salva
Vamos ver se podemos obter mais detalhes sobre coleta de desempenho de saudação que gerou este alerta e verifique se o nosso suspeita de que os problemas de saudação são causados por esse processo de backup.  Alterar o intervalo de tempo de saudação muito**6 horas**.  Em seguida, clique em **Favoritos** e role para baixo toohello salvada procura **mapa de serviço**.  Essas são as consultas criadas especificamente para a análise.  Clique em **5 Primeiros Processos por CPU para acmetomcat**.

![Pesquisa salva](./media/operations-management-suite-walkthrough-servicemap/saved-search.png)


Esta consulta retorna uma lista de saudação processos 5 principais consome processador em **acmetomcat**.  Você pode inspecionar Olá consulta tooget uma linguagem de consulta Introdução toohello usada para pesquisas de log.  Se você estava interessado em processos de saudação em outros computadores, você pode modificar Olá consulta tooretrieve essas informações.

Nesse caso, podemos ver que o processo de backup Olá consistentemente consome aproximadamente 60% da CPU do servidor de aplicativo hello.  É óbvio que esse novo processo é responsável por nosso problema de desempenho.  Nossa solução seria obviamente tooremove esse novo software de servidor de aplicativos de saudação de backup.  Nós realmente pode aproveitar o estado de configuração desejado (DSC) gerenciados pelas políticas de toodefine de automação do Azure que certifique-se de que esse processo é executado nunca nesses sistemas críticos.


## <a name="summary-points"></a>Pontos do resumo
- O[Mapa de Serviço](operations-management-suite-service-map.md) fornece uma exibição de todo o aplicativo, mesmo que você não conheça todos os servidores e dependências.
- Mapa de serviço anexa os dados coletados por outros toohelp de soluções do OMS identificar problemas com seu aplicativo e sua infraestrutura subjacente.
- [Pesquisas de log](../log-analytics/log-analytics-log-searches.md) permitem a você toodrill para baixo em dados específicos coletados no repositório de análise de Log de saudação.    

## <a name="next-steps"></a>Próximas etapas
- Saiba mais sobre o [Mapa de Serviço](operations-management-suite-service-map.md).
- [Implante e configure o](operations-management-suite-service-map-configure.md) Mapa de Serviço.
- Saiba mais sobre o [Log Analytics](../log-analytics/log-analytics-overview.md) que é necessário para o Mapa de Serviço e armazena os dados operacionais guardados por agentes.