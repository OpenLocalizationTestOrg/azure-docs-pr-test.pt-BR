---
title: "aaaWindows conteúdo do SDK de aplicativos Universal"
description: "Saiba mais sobre o conteúdo de saudação do hello SDK de aplicativos Universal do Windows para o Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8fa1b701-1c2b-4aec-940c-06c974ef5405
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: a8013d2433c0be62d737c8bc6e8360ed79bbe532
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-sdk-content"></a>Conteúdo do SDK de aplicativos do Windows Universal
Este documento lista e descreve o conteúdo de saudação implantado por Olá SDK em seu aplicativo.

## <a name="hello-resources-folder"></a>Olá `/Resources` pasta
Esta pasta contém todos os recursos de saudação do Mobile Engagement precisa. Você também pode personalizá-los toofit seu aplicativo.

* `EngagementConfiguration.xml`: Olá o arquivo de configuração do Mobile Engagement, que é onde você pode personalizar as configurações do Mobile Engagement (cadeia de caracteres de conexão do Mobile Engagement, falha de relatório...).

### <a name="html-folder"></a>/pasta html
* `EngagementNotification.html`: Olá `Notification` web design do modo de exibição html para faixas no aplicativo.
* `EngagementAnnouncement.html`: Olá `Announcement` web design do modo de exibição html para exibições intersticiais no aplicativo.

### <a name="images-folder"></a>/pasta imagens
* `EngagementIconNotification.png`: ícone de marca de saudação exibido no hello à esquerda de uma notificação, substituí-lo por seu ícone de marca.
* `EngagementIconOk.png`: Olá `Ok` ícone Olá alcance de páginas de conteúdo para o botão de ação ou validação de saudação.
* `EngagementIconNOK.png`: Olá `NOK` ícone usado quando o botão de validação Olá Olá alcance de páginas de conteúdo está desabilitado.
* `EngagementIconClose.png`: Olá `Close` ícone de saudação alcançar notificações e conteúdo de saudação ignorar botão.

### <a name="overlay-folder"></a>/pasta sobreposição
* `EngagementPageOverlay.cs`: página de sobreposição de saudação responsável por adicionar Olá contrato alcançar o filho de tooits de interface do usuário no aplicativo.

