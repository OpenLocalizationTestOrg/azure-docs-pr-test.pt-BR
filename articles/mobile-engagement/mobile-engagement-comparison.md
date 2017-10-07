---
title: "aaaComparing do Azure Mobile Engagement com outros serviços do Azure semelhantes"
description: "Comparando o Azure Mobile Engagement a outros serviços parecidos do Azure - HockeyApp, AppInsights, Hubs de Notificação"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 1f114775-3a9a-4dd4-8d59-b10d1da9a68b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 0859ae9980d0fa96ffbc0edfbd795ccc58d2c843
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="comparing-azure-mobile-engagement-with-other-similar-azure-services"></a>Comparando o Azure Mobile Engagement a outros serviços parecidos do Azure
lista de saudação de serviços oferecidos pelo Microsoft Azure já está expandindo e às vezes você talvez esteja se perguntando como o Azure Mobile Engagement é diferente do que esse serviço que você acabou de leitura ou saber sobre. Este artigo tenta confusão de saudação tooclear e direciona toochoose do Azure Mobile Engagement quando é mais apropriado para seu uso. 

Azure Mobile Engagement é um serviço de destino especificamente **para comerciantes/CMOs digitais** , mas pode ser usado por qualquer **proprietário do aplicativo móvel ou publicador** que deseja que o uso de saudação tooincrease, retenção e monetização dos seus aplicativos móveis. 

*Ele é uma plataforma SaaS (software como serviço) de envolvimento com o usuário que fornece informações orientadas aos dados sobre uso do aplicativo, segmentação do usuário em tempo real, além de habilitar notificações por push com reconhecimento contextual e mensagens no aplicativo.* 

Dividir essa definição, temos Olá principais características a seguir, que também destaca sua proposta de valor exclusivo:

1. **Notificações por push e mensagens no aplicativo com reconhecimento de contexto**
   
   Este é o foco principal Olá produto Olá - executar as notificações por push personalizados e de destino. E para este toohappen, podemos coletar dados de análise comportamental avançados. 
2. **Informações controladas por dados sobre o uso do aplicativo**
   
   Fornecemos plataforma cruzada SDKs toocollect Olá análise comportamental sobre usuários de aplicativo hello. Observe a análise de comportamento Olá termo (em vez de análise de desempenho), pois vamos nos concentrar em como os usuários do aplicativo hello estão usando o aplicativo hello. Coletamos dados de análise de desempenho básicos sobre erros, falhas etc mas isto é Olá foco de núcleo do produto hello. 
3. **Segmentação de usuários em tempo real**
   
   Depois de coletar dados de análise comportamental de usuários de aplicativos, permitimos que você toosegment seu público-alvo com base em vários parâmetros e os dados coletados tooenable toorun você direcionado campanhas de push. 
4. **Software como um serviço (SaaS):**
   
   Temos um portal separado do portal de gerenciamento do Azure de saudação que é otimizada toointeract e exibir análise comportamental avançado sobre usuários de aplicativo hello e executar push campanhas de marketing. saudação de produto é voltado tooget você ocorrendo em nenhum momento!   

Com esse conjunto de diferenciação em mãos, aqui está como podemos comparar em relação a outras ofertas do Azure aparentemente semelhantes - Observe artigo Olá não faz uma comparação de nível de recurso, mas usa um mais toodefine de abordagem de cenário com base em qual produto funciona melhor:

1. [HockeyApp](https://azure.microsoft.com/services/hockeyapp/) é a solução de DevOps móveis da Microsoft hello. Com ele, distribuir compilações toobeta testadores, coletar dados de falha e obter feedback de usuário. Ele também é integrado ao Visual Studio Team Services, permitindo a compilação fácil de implantações e a integração de itens de trabalho. 
   
   Olá foco aqui é coletar dados de análise de desempenho sobre aplicativos móveis hello e DevOps. Você pode acabar com a integração entre os dois HockeyApps e Mobile Engagement no seu aplicativo e que não serão incomum porque o mesmo que há alguma sobreposição nos dados coletado de hello, Olá principal foco dos produtos de saudação é diferente e eles ajudam a atingir diferentes objetivos para você.  
2. [Application Insights](../application-insights/app-insights-overview.md) se seu aplicativo móvel tem um lado do servidor, e em seguida, você usará do servidor web do Application Insights toomonitor saudação do seu aplicativo, mas para aplicativos móveis do lado do cliente de saudação, você deve usar o HockeyApp. 
3. [Hubs de notificação](https://azure.microsoft.com/services/notification-hubs/) fornece um serviço simples no sentido de saudação que não é necessário um SDK integrado no aplicativo móvel hello e você pode ter controle total do seu aplicativo móvel e permite enviar notificações por push com recursos básicos de marcação. Isso é ótimo para qualquer proprietário de aplicativo que se preocupar menos sobre direcionamento e mais informações de envio/comunicação instantaneamente tootheir os usuários de aplicativo (difusão tooa grande população). 
   
   Observe o foco de saudação aqui sobre o envio de notificações rápidas impressionante com a funcionalidade básica de segmentação. 

Vamos analisar alguns cenários:

1. Tim faz parte da equipe de marketing digital Olá no repositório do Adventure Works que publique aplicativos móveis para os usuários. Objetivo de Tim é tooensure que os usuários de saudação que baixam os aplicativos móveis continuar toouse-lo e com frequência. Isso aumenta não apenas uma marca anexar com os usuários do aplicativo hello, mas também aumenta monetização quando os usuários do aplicativo hello fazer compras usando o aplicativo móvel hello. Para este Tim, será preciso toosend direcionado notificações toohello aplicativo usuários, que consideram útil, tooencourage-los tooopen Olá aplicativo e voltar tooit frequentemente. É nessa situação que Paulo considerará o Mobile Engagement bastante útil. 
2. Joann faz parte da equipe de desenvolvimento de saudação do hello aplicativos móveis da Adventure Works e está procurando um detalhes do produto toolog sobre falhas, exceções e obtenha telemetria do desempenho de um aplicativo. É nessa situação que Clara considerará o HockeyApp bastante útil. Joann pode integrar ambas as credenciais do HockeyApp para o desenvolvedor voltados para cenários e o Azure Mobile Engagement para Tim Olá mesmo Olá de tooget de aplicativo melhor de ambos. 
3. Rodízio faz parte da equipe de desenvolvimento de saudação de saudação de aplicativos móveis na rede Contoso notícias e todos os que quer é toosend out recentes notícias alertas tooall que os usuários sem muita segmentação como Olá notícias alerta é disparado. É nessa situação que Laura considerará o Hubs de Notificação bastante útil. 
   Nesse cenário, é possível no entanto como aplicativo móvel Olá amadurece, há um requisito toodo mais rica segmentação e obter detalhes sobre o comportamento do usuário do aplicativo hello. Neste momento, Robin terá tooevaluate do Azure Mobile Engagement. 

toorecap, finalidade de saudação do Mobile Engagement não é apenas a análise de toocollect - não é "outro produto de análise da Microsoft". Trata-se de enviar notificações por push de destino e para esse destino, podemos coletar dados de análise comportamental mas foco Olá permanece no enviar notificações por push que tornar Olá a maioria dos usuários de aplicativo toohello sentido para que ele não encontrar como spam. 

Para obter mais detalhes, confira este [vídeo rápido](mobile-engagement-overview.md) sobre o Mobile Engagement. 

