---
title: "Introdução ao Aplicativo Web do Azure no Linux | Microsoft Docs"
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
ms.openlocfilehash: 0870f811845ec7c705da13f08abdfa762d25b209
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-azure-web-app-on-linux"></a>Introdução ao Aplicativo Web do Azure no Linux

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a>Visão geral
Os clientes podem usar o Aplicativo Web no Linux para hospedar aplicativos Web nativos no Linux para as pilhas de aplicativos com suporte. A seção a seguir lista as pilhas de aplicativos que têm suporte no momento. 

## <a name="features"></a>Recursos
Atualmente, o Aplicativo Web no Linux dá suporte a estas pilhas de aplicativos:

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

* Os clientes podem escalar ou reduzir verticalmente aplicativos Web, alterando a camada dos respectivos planos do Serviço de Aplicativo
* Os clientes podem escalar horizontalmente seus aplicativos e executar várias instâncias do aplicativo dentro dos limites de seu SKU

Para o Kudu, algumas das funcionalidades básicas:

* Ambientes
* Implantações
* Console básico
* SSH

Para DevOps:

* Ambientes de preparo
* ACR e CI/CD do DockerHub

## <a name="limitations"></a>Limitações
O portal do Azure mostra somente os recursos que funcionam atualmente para o Aplicativo Web no Linux e oculta os demais. Conforme habilitarmos mais recursos, eles ficarão visíveis no portal.

Alguns recursos, como a integração de rede virtual, a autenticação do Azure Active Directory/de terceiros ou as extensões de site do Kudu, ainda não estão disponíveis. Quando esses recursos estiverem disponíveis, atualizaremos nossa documentação e nosso blog sobre as alterações.

Esta visualização pública está disponível atualmente nas seguintes regiões:

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

No Linux, os aplicativos Web só têm suporte nos planos de serviço de aplicativo Dedicados e não têm uma camada Gratuita ou Compartilhada. Além disso, planos de Serviço de Aplicativo para aplicativos Web Linux e regulares são mutuamente exclusivos e, portanto, você não pode criar um aplicativo Linux em um plano do serviço de aplicativo não Linux.

Os Aplicativos Web no Linux devem ser criados em um grupo de recursos que não contenha aplicativos Web não Linux na mesma região.

## <a name="troubleshooting"></a>Solucionar problemas ##

Quando seu aplicativo falhar ao iniciar ou você quiser verificar o log do aplicativo, verifique os logs do Docker no diretório LogFiles. Acesse esse diretório por meio de seu site SCM ou via FTP.
Para registrar `stdout` e `stderr` por meio do contêiner, você precisa habilitar o **Registro em log do Contêiner do Docker** em **Logs de Diagnóstico**.

![Habilitando o log][2]

![Como usar o Kudu para exibir os logs do Docker][1]

Acesse o site SCM nas **Ferramentas Avançadas** no menu **Ferramentas de Desenvolvimento**.

## <a name="next-steps"></a>Próximas etapas
Veja os links a seguir para começar a usar o Serviço de Aplicativo no Linux. Você pode postar perguntas e problemas no [nosso fórum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).

* [Como usar uma imagem personalizada do Docker para o Aplicativo Web do Azure no Linux](app-service-linux-using-custom-docker-image.md)
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