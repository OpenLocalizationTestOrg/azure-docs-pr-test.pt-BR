---
title: "estatísticas de tempo de aaaReal no Azure CDN | Microsoft Docs"
description: "Estatísticas em tempo real fornecem dados em tempo real sobre o desempenho de saudação da CDN do Azure durante a entrega de conteúdo tooyour clientes."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: c7989340-1172-4315-acbb-186ba34dd52a
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 68900a5092b767e45c1fdf9cef2cd03f55f38a6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-stats-in-microsoft-azure-cdn"></a>Estatísticas em tempo real na CDN do Microsoft Azure
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a>Visão geral
Este documento explica as estatísticas em tempo real na CDN do Microsoft Azure.  Essa funcionalidade fornece dados em tempo real, como largura de banda, o status de cache e conexões simultâneas tooyour CDN perfil durante a entrega de conteúdo tooyour clientes. Isso permite o monitoramento contínuo da integridade de saudação do seu serviço a qualquer momento, incluindo eventos de ativação.

Olá gráficos a seguir está disponível:

* [Largura de banda](#bandwidth)
* [Códigos de status](#status-codes)
* [Status do Cache](#cache-statuses)
* [Conexões](#connections)

## <a name="accessing-real-time-stats"></a>Acessando as estatísticas em tempo real
1. Em Olá [Portal do Azure](https://portal.azure.com), procurar tooyour perfil CDN.
   
    ![Folha Perfil CDN](./media/cdn-real-time-stats/cdn-profile-blade.png)
2. Na folha de perfil CDN hello, clique em Olá **gerenciar** botão.
   
    ![botão gerenciar da folha Perfil CDN](./media/cdn-real-time-stats/cdn-manage-btn.png)
   
    portal de gerenciamento de CDN Olá é aberto.
3. Passe o mouse sobre Olá **análise** guia, em seguida, passe o mouse sobre Olá **estatísticas em tempo real** flutuante.  Clique em **Objeto grande de HTTP**.
   
    ![Portal de gerenciamento da CDN](./media/cdn-real-time-stats/cdn-premium-portal.png)
   
    gráficos de estatísticas em tempo real de saudação são exibidos.

Cada um dos gráficos de saudação exibe estatísticas em tempo real para o período de tempo de saudação selecionado, começando quando Olá página for carregada.  gráficos de saudação são atualizadas automaticamente em alguns segundos.  Olá **atualizar gráfico** botão, se presente, limpará gráfico hello, após o qual ele só exibirá dados saudação selecionado.

## <a name="bandwidth"></a>Largura de banda
![Gráfico da largura de banda](./media/cdn-real-time-stats/cdn-bandwidth.png)

Olá **largura de banda** gráfico exibe a quantidade de saudação de largura de banda usada para a plataforma atual Olá por período de tempo de saudação selecionado. a parte sombreada saudação do gráfico de saudação indica o uso de largura de banda. a quantidade exata Olá de largura de banda está sendo usada no momento é exibida diretamente abaixo de gráfico de linha de saudação.

## <a name="status-codes"></a>Códigos de status
![Gráfico do código de status](./media/cdn-real-time-stats/cdn-status-codes.png)

Olá **códigos de Status** gráfico indica quantas vezes determinados códigos de resposta HTTP estão ocorrendo em um período de tempo de saudação selecionado.

> [!TIP]
> Para obter uma descrição de cada opção do código de status HTTP, confira [Códigos de Status HTTP da CDN do Azure](https://msdn.microsoft.com/library/mt759238.aspx).
> 
> 

Uma lista de códigos de status HTTP é exibida diretamente acima gráfico hello. Essa lista indica cada código de status que pode ser incluído no gráfico de linha hello e o número atual de saudação de ocorrências por segundo para esse código de status. Por padrão, uma linha é exibida para cada um desses códigos de status no gráfico de saudação. No entanto, você pode escolher tooonly códigos de status de saudação do monitor que têm um significado especial para a sua configuração de CDN. toodo isso, verifique os códigos de status de saudação desejado e desmarque todas as outras opções e clique em **atualizar gráfico**. 

Você pode ocultar temporariamente os dados registrados para um código de status específico.  De legenda Olá diretamente abaixo gráfico hello, clique em código de status de saudação deseja toohide. código de status de saudação ficará oculta imediatamente do gráfico de saudação. Clicando novamente o código de status que fará com que esse toobe opção exibida novamente.

## <a name="cache-statuses"></a>Status do Cache
![Gráficos dos Status do Cache](./media/cdn-real-time-stats/cdn-cache-status.png)

Olá **Cache status** gráfico indica quantas vezes determinados tipos de status do cache estão ocorrendo por período de tempo de saudação selecionado. 

> [!TIP]
> Para obter uma descrição de cada opção do código de status do cache, consulte [Códigos de Status do Cache da CDN do Azure](https://msdn.microsoft.com/library/mt759237.aspx).
> 
> 

Uma lista de códigos de status do cache é exibida diretamente acima gráfico hello. Essa lista indica cada código de status que pode ser incluído no gráfico de linha hello e o número atual de saudação de ocorrências por segundo para esse código de status. Por padrão, uma linha é exibida para cada um desses códigos de status no gráfico de saudação. No entanto, você pode escolher tooonly códigos de status de saudação do monitor que têm um significado especial para a sua configuração de CDN. toodo isso, verifique os códigos de status de saudação desejado e desmarque todas as outras opções e clique em **atualizar gráfico**. 

Você pode ocultar temporariamente os dados registrados para um código de status específico.  De legenda Olá diretamente abaixo gráfico hello, clique em código de status de saudação deseja toohide. código de status de saudação ficará oculta imediatamente do gráfico de saudação. Clicando novamente o código de status que fará com que esse toobe opção exibida novamente.

## <a name="connections"></a>Conexões
![Gráfico das Conexões](./media/cdn-real-time-stats/cdn-connections.png)

Esse gráfico indica quantas conexões foram estabelecidas tooyour os servidores de borda. Cada solicitação de um ativo que passa por nossos resultados da CDN em uma conexão.

## <a name="next-steps"></a>Próximas etapas
* Receba uma notificação com [Alertas em tempo real no Azure CDN](cdn-real-time-alerts.md)
* Saiba mais com os [relatórios HTTP avançados](cdn-advanced-http-reports.md)
* Analisar os [padrões de uso](cdn-analyze-usage-patterns.md)

