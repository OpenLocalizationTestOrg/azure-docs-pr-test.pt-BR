---
title: "aaaAdd um aplicativo de Java tooAzure aplicativos de Web do serviço de aplicativo"
description: "Este tutorial mostra como tooadd uma instância de tooyour aplicativo ou página de aplicativo de serviço de aplicativos Web do Azure que já está configurado toouse Java."
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
ms.openlocfilehash: 2feb464b2933921ad2887779a6b7589634e2e2f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-java-application-tooazure-app-service-web-apps"></a>Adicionar um aplicativo de Java tooAzure aplicativos de Web do serviço de aplicativo
Depois que seu aplicativo web Java inicializou [do serviço de aplicativo do Azure] [ Azure App Service] conforme documentado em [criar um aplicativo da web de Java no serviço de aplicativo do Azure](web-sites-java-get-started.md), você pode carregar seu aplicativo colocando o WAR no hello **webapps** pasta.

Olá toohello do caminho de navegação **webapps** pasta varia com base na maneira como você configurar sua instância de aplicativos Web.

* Se você configurar seu aplicativo web usando hello Azure Marketplace, Olá caminho toohello **webapps** pasta está na forma de saudação **d:\home\site\wwwroot\bin\application\_server\webapps**, onde **aplicativo\_server** é nome hello saudação do servidor de aplicativos em vigor para a instância de aplicativos Web. 
* Se você configurar seu aplicativo web usando a saudação da interface do usuário de configuração do Azure, Olá caminho toohello **webapps** pasta está na forma de saudação **d:\home\site\wwwroot\webapps**. 

Observe que você pode usar tooupload de controle de origem, seu aplicativo ou páginas da web, incluindo [cenários de integração contínua](app-service-continuous-deployment.md). FTP também é uma opção para carregar o aplicativo ou páginas da web; Para obter mais informações sobre como implantar seus aplicativos por FTP, consulte [implantar tooAzure seu aplicativo do serviço de aplicativo].

Observação para aplicativos da web Tomcat: depois de carregar seu toohello de arquivo WAR **webapps** pasta, o servidor de aplicativos Tomcat Olá detectará que você adicionou a ele e automaticamente carregá-lo. Observe que, se você copiar o diretório de raiz de toohello de arquivos (exceto arquivos WAR), servidor de aplicativo hello precisará toobe reiniciado para que esses arquivos são usados. funcionalidade de autoload Olá para aplicativos da web Tomcat Java Olá em execução no Azure é baseada em um novo arquivo WAR que está sendo adicionado ou novos arquivos ou diretórios adicionados toohello **webapps** pasta. 

<a name="see-also"></a>

## <a name="see-also"></a>Consulte também
Para obter mais informações sobre como usar o Azure com Java, consulte Olá [Centro de desenvolvedores de Java do Azure].

[application-insights-app-insights-java-get-started](../application-insights/app-insights-java-get-started.md)

<!-- URL List -->

[Centro de desenvolvedores de Java do Azure]: https://azure.microsoft.com/develop/java/
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
[implantar tooAzure seu aplicativo do serviço de aplicativo]: ./web-sites-deploy.md
