---
title: "Adicionar um aplicativo Java a Aplicativos Web do Serviço de Aplicativo do Azure"
description: "Este tutorial mostra como adicionar uma página ou um aplicativo à sua instância de Aplicativos Web do Serviço de Aplicativo de Azure que já está configurada para usar o Java."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9b46528b-e2d0-4f26-b8d7-af94bd8c31ef
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: c28e7c499ed02b759df580f4b14a971b6aec5b67
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="add-a-java-application-to-azure-app-service-web-apps"></a>Adicionar um aplicativo Java a Aplicativos Web do Serviço de Aplicativo do Azure
Após inicializar seu aplicativo Web do Java no [Serviço de Aplicativo do Azure][Azure App Service], conforme documentado em [Criar um aplicativo Web do Java no Serviço de Aplicativo do Azure](web-sites-java-get-started.md), você poderá carregar o aplicativo colocando o WAR na pasta **webapps**.

O caminho de navegação para a pasta **webapps** varia dependendo de como você configurou sua instância dos Aplicativos Web.

* Se você configurar o aplicativo Web usando o Azure Marketplace, o caminho para a pasta **webapps** estará no formato **d:\home\site\wwwroot\bin\application\_server\webapps**, em que **application\_server** é o nome do servidor de aplicativos em vigor para a instância dos Aplicativos Web. 
* Se você configurar o aplicativo Web usando a interface do usuário de configuração do Azure, o caminho para a pasta **webapps** estará no formato **d:\home\site\wwwroot\webapps**. 

Observe que você pode usar o controle do código-fonte para carregar o aplicativo ou páginas da web, incluindo [cenários de integração contínua](app-service-continuous-deployment.md). O FTP também é uma opção para carregar seu aplicativo ou páginas da web. Para obter mais informações sobre como implantar aplicativos por FTP, confira [Implantar seu aplicativo no Serviço de Aplicativo do Azure].

Observação para aplicativos Web Tomcat: assim que você tiver carregado seu arquivo WAR na pasta **webapps** , o servidor do aplicativo Tomcat detectará que você o adicionou e o carregará automaticamente. Observe que se você copiar arquivos (diferentes de arquivos WAR) no diretório raiz, o servidor de aplicativos precisará ser reiniciado para que esses arquivos sejam usados. A funcionalidade de carregamento automático dos aplicativos Web Tomcat Java em execução no Azure baseia-se na adição de um novo arquivo WAR ou da adição de novos arquivos ou diretórios à pasta **webapps** . 

<a name="see-also"></a>

## <a name="see-also"></a>Consulte também
Para obter mais informações sobre como usar o Azure com o Java, confira a [Central de desenvolvimento Java do Azure].

[application-insights-app-insights-java-get-started](../application-insights/app-insights-java-get-started.md)

<!-- URL List -->

[Central de desenvolvimento Java do Azure]: https://azure.microsoft.com/develop/java/
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
[Implantar seu aplicativo no Serviço de Aplicativo do Azure]: ./web-sites-deploy.md
