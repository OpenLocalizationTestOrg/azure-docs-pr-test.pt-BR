---
title: aaaIntroduction tooAzure Web App no Linux | Microsoft Docs
description: Saiba mais sobre o Aplicativo Web do Azure no Linux.
keywords: "serviço de aplicativo do azure, linux, oss"
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: bc85eff6-bbdf-410a-93dc-0f1222796676
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 43b9865ade251909a77429eb3e18fe0bcaac3bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-web-app-on-linux"></a>Introdução tooAzure Web App no Linux

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a>Visão geral
Os clientes podem usar o aplicativo Web em aplicativos de web do Linux toohost nativamente no Linux para as pilhas de aplicativos com suporte. Olá, seção a seguir lista as pilhas de aplicativos de saudação que são atualmente suportadas. 

## <a name="features"></a>Recursos
Web App no Linux atualmente suporta Olá pilhas de aplicativos a seguir:

* Node.js
    * 4.4
    * 4.5
    * 6.2
    * 6.6
    * 6.9
    * 6.10
    * 6.11
    * 8.0
    * 8.1
* PHP
    * 5.6
    * 7.0
* .NET Core
    * 1.0
    * 1,1
* Ruby
    * 2.3

Os clientes podem implantar seus aplicativos usando:

* FTP
* Git local
* GitHub
* Bitbucket

Para o dimensionamento de aplicativos:

* Os clientes podem dimensionar os aplicativos web para cima e para baixo, alterando o nível de saudação do seu plano de serviço de aplicativo
* Os clientes podem dimensionar aplicativos e executar várias instâncias do aplicativo dentro dos limites de saudação do seu SKU

Para Kudu, algumas das funcionalidades básicas hello:

* Ambientes
* Implantações
* Console básico
* SSH

Para DevOps:

* Ambientes de preparo
* ACR e CI/CD do DockerHub

## <a name="limitations"></a>Limitações
Olá portal do Azure mostra apenas recursos que atualmente funcionam para o aplicativo Web no Linux e oculta Olá demais. Como podemos habilitar mais recursos, ele ficará visível no portal de saudação.

Alguns recursos, como a integração de rede virtual, a autenticação do Azure Active Directory/de terceiros ou as extensões de site do Kudu, ainda não estão disponíveis. Depois que esses recursos estão disponíveis, atualizamos nossa documentação e o blog sobre alterações de saudação.

Essa visualização pública está disponível atualmente apenas em Olá regiões a seguir:

* Oeste dos EUA
* Leste dos EUA
* Europa Ocidental
* Norte da Europa
* Centro-Sul dos Estados Unidos
* Centro-Norte dos EUA
* Sudeste Asiático
* Ásia Oriental
* Leste da Austrália
* Leste do Japão
* Sul do Brasil
* Sul da Índia

No Linux, os aplicativos Web só é suportado em planos de serviço de aplicativo dedicado hello e não tem uma camada gratuito ou compartilhado. Além disso, planos de Serviço de Aplicativo para aplicativos Web Linux e regulares são mutuamente exclusivos e, portanto, você não pode criar um aplicativo Linux em um plano do serviço de aplicativo não Linux.

No Linux, os aplicativos Web deve ser criado em um grupo de recursos que não contenha os aplicativos web não Linux em hello mesma região.

## <a name="troubleshooting"></a>Solucionar problemas ##

Quando o aplicativo falhar toostart ou se desejar toocheck log de saudação do seu aplicativo, verifique Olá que docker registra no diretório de arquivos de log de saudação. Acesse esse diretório por meio de seu site SCM ou via FTP.
Olá toolog `stdout` e `stderr` de seu contêiner, você precisa tooenable **log do contêiner do Docker** em **Logs de diagnóstico**.

![Habilitando o log][2]

![Usando logs de Docker tooview Kudu][1]

Você pode acessar o site SCM saudação do **ferramentas avançadas de** em Olá **ferramentas de desenvolvimento** menu.

## <a name="next-steps"></a>Próximas etapas
Consulte Olá tooget links de Introdução ao serviço de aplicativo no Linux a seguir. Você pode postar perguntas e problemas no [nosso fórum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).

* [Como toouse um Docker personalizado da imagem para o aplicativo Web do Azure no Linux](app-service-linux-using-custom-docker-image.md)
* [Usando a configuração de PM2 para Node.js no Aplicativo Web do Azure no Linux](app-service-linux-using-nodejs-pm2.md)
* [Usando o .NET Core no Aplicativo Web do Serviço de Aplicativo do Azure no Linux](app-service-linux-using-dotnetcore.md)
* [Usando o Ruby em aplicativos Web do Serviço de Aplicativo do Azure no Linux](app-service-linux-ruby-get-started.md)
* [Perguntas frequentes sobre o Aplicativo Web do Serviço de Aplicativo do Azure no Linux](app-service-linux-faq.md)
* [Suporte de SSH para o Aplicativo Web do Azure no Linux](./app-service-linux-ssh-support.md)
* [Configurar ambientes de preparo no Serviço de Aplicativo do Azure](./web-sites-staged-publishing.md)
* [Implantação contínua do Hub do Docker com o Aplicativo Web do Azure no Linux](./app-service-linux-ci-cd.md)

<!--Image references-->
[1]: ./media/app-service-linux-intro/kudu-docker-logs.png
[2]: ./media/app-service-linux-intro/logging.png