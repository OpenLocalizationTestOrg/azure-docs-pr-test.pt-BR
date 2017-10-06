---
title: "aaaUsing Ruby no Azure serviço de aplicativo Web App no Linux | Microsoft Docs"
description: "Usando o Ruby no Aplicativo Web do Serviço de Aplicativo do Azure no Linux."
keywords: "serviço de aplicativo do azure, aplicativo Web, perguntas frequentes, linux, oss, ruby"
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: 45692cb3bf1da9ff65b9466055029bfaef8b7d8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-ruby-in-web-app-on-linux"></a>Usando o Ruby no Aplicativo Web no Linux #

Com hello mais recente atualização tooour back-end, introduzimos o suporte para v.2.3 Ruby. Ao definir a configuração de saudação de seu aplicativo da web de Linux, você pode alterar pilha do aplicativo hello.

## <a name="using-hello-azure-portal"></a>Usando Olá portal do Azure ##

No menu novo, Olá no hello [portal do Azure](https://portal.azure.com), você pode escolher que toocreate um aplicativo Web no Linux de Olá Web + móvel opção conforme Olá a imagem a seguir:

![Iniciar a criação de um aplicativo web em Olá portal do Azure][1]

Em seguida, Olá **criar folha** abre conforme Olá a imagem a seguir:

![folha de criar Olá][2]

1. Dê um nome ao aplicativo Web.
2. Escolha um grupo de recursos existente ou crie um novo. (Consulte regiões disponíveis no hello [seção limitações](app-service-linux-intro.md).)
3. Escolha um plano do Serviço de Aplicativo do Azure existente ou crie um. (Consulte as notas de plano do serviço de aplicativo hello [seção limitações](app-service-linux-intro.md).)
4. Escolha pilhas de tempo de execução interna Olá Olá Ruby.

Depois que seu aplicativo web Ruby é criado, você pode implantar tooit usando Git ou FTP.

toolearn mais sobre a criação de um aplicativo Ruby, verifique Olá [get guia de Introdução](app-service-linux-ruby-get-started.md)

## <a name="next-steps"></a>Próximas etapas
* [O que é o Aplicativo Web no Linux?](app-service-linux-intro.md)
* [TooAzure local de implantação do Git do serviço de aplicativo](app-service-deploy-local-git.md)
* [Perguntas frequentes sobre o Aplicativo Web do Serviço de Aplicativo do Azure no Linux](app-service-linux-faq.md)
* [Criar um aplicativo Ruby com o Aplicativo Web do Azure no Linux](app-service-linux-ruby-get-started.md)

<!--Image references-->
[1]: ./media/app-service-linux-using-ruby/New-Linux.png
[2]: ./media/app-service-linux-using-ruby/Ruby-UX.png