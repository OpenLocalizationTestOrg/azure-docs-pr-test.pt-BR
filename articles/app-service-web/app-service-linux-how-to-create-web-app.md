---
title: "aplicativo em execução no Linux da web de aaaCreate do Azure | Microsoft Docs"
description: "Fluxo de trabalho da criação de aplicativo Web para aplicativo Web do Azure no Linux."
keywords: "serviço de aplicativo do azure, aplicativo web, linux, oss"
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: 3a71d10a-a0fe-4d28-af95-03b2860057d5
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: de1bd030345d5e2a8024012067b5bcaa2cca09dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-web-app-running-on-linux"></a>Criar um aplicativo web em execução no Linux

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


## <a name="use-hello-azure-portal-toocreate-your-web-app"></a>Use Olá toocreate portal do Azure seu aplicativo web
Você pode começar a criar seu aplicativo web no Linux de saudação [portal do Azure](https://portal.azure.com) conforme Olá a imagem a seguir:

![Iniciar a criação de um aplicativo web em Olá portal do Azure][1]

Em seguida, Olá **criar folha** abre conforme Olá a imagem a seguir:

![folha de criar Olá][2]

1. Dê um nome ao aplicativo Web.
2. Escolha um grupo de recursos existente ou crie um novo. (Consulte regiões disponíveis no hello [seção limitações](app-service-linux-intro.md).)
3. Escolha um plano do Serviço de Aplicativo do Azure existente ou crie um. (Consulte as notas de plano do serviço de aplicativo hello [seção limitações](app-service-linux-intro.md).)
4. Escolha o aplicativo hello pilha que você pretende toouse. É possível escolher entre várias versões de Node.js, PHP, .Net Core e Ruby.

Depois que você criou um aplicativo hello, você pode alterar a pilha do aplicativo hello em configurações do aplicativo hello conforme Olá a imagem a seguir:

![Configurações do aplicativo][3]

## <a name="deploy-your-web-app"></a>Implantar o aplicativo Web
Escolhendo **opções de implantação** de fornece portal de gerenciamento Olá você Olá opção toouse local Git ou GitHub repositório toodeploy seu aplicativo. Olá demais instruções hello serão toothose semelhante para um aplicativo web do Linux não. Você pode seguir as instruções de saudação em [implantação local do Git](app-service-deploy-local-git.md) ou [implantação contínua](app-service-continuous-deployment.md) toodeploy seu aplicativo.

Você também pode usar o site do aplicativo tooyour tooupload FTP. Você pode obter o ponto de extremidade do hello FTP para seu aplicativo web do diagnóstico de saudação do seção logs conforme Olá a imagem a seguir:

![Logs de diagnóstico][4]

## <a name="next-steps"></a>Próximas etapas
* [O que é um Aplicativo Web do Azure no Linux?](app-service-linux-intro.md)
* [Usando a configuração de PM2 para Node.js no Aplicativo Web do Azure no Linux](app-service-linux-using-nodejs-pm2.md)
* [Usando o Ruby em aplicativos Web do Serviço de Aplicativo do Azure no Linux](app-service-linux-ruby-get-started.md)
* [Perguntas frequentes sobre o Aplicativo Web do Serviço de Aplicativo do Azure no Linux](app-service-linux-faq.md)

<!--Image references-->
[1]: ./media/app-service-linux-how-to-create-a-web-app/top-level-create.png
[2]: ./media/app-service-linux-how-to-create-a-web-app/create-blade.png
[3]: ./media/app-service-linux-how-to-create-a-web-app/application-settings-change-stack.png
[4]: ./media/app-service-linux-how-to-create-a-web-app/diagnostic-logs-ftp.png
