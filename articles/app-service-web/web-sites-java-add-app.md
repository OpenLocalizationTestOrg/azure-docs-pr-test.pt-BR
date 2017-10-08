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
# <a name="add-a-java-application-tooazure-app-service-web-apps"></a><span data-ttu-id="691fe-103">Adicionar um aplicativo de Java tooAzure aplicativos de Web do serviço de aplicativo</span><span class="sxs-lookup"><span data-stu-id="691fe-103">Add a Java application tooAzure App Service Web Apps</span></span>
<span data-ttu-id="691fe-104">Depois que seu aplicativo web Java inicializou [do serviço de aplicativo do Azure] [ Azure App Service] conforme documentado em [criar um aplicativo da web de Java no serviço de aplicativo do Azure](web-sites-java-get-started.md), você pode carregar seu aplicativo colocando o WAR no hello **webapps** pasta.</span><span class="sxs-lookup"><span data-stu-id="691fe-104">Once you have initialized your Java web app in [Azure App Service][Azure App Service] as documented at [Create a Java web app in Azure App Service](web-sites-java-get-started.md), you can upload your application by placing your WAR in hello **webapps** folder.</span></span>

<span data-ttu-id="691fe-105">Olá toohello do caminho de navegação **webapps** pasta varia com base na maneira como você configurar sua instância de aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="691fe-105">hello navigation path toohello **webapps** folder differs based on how you set up your Web Apps instance.</span></span>

* <span data-ttu-id="691fe-106">Se você configurar seu aplicativo web usando hello Azure Marketplace, Olá caminho toohello **webapps** pasta está na forma de saudação **d:\home\site\wwwroot\bin\application\_server\webapps**, onde **aplicativo\_server** é nome hello saudação do servidor de aplicativos em vigor para a instância de aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="691fe-106">If you set up your web app by using hello Azure Marketplace, hello path toohello **webapps** folder is in hello form **d:\home\site\wwwroot\bin\application\_server\webapps**, where **application\_server** is hello name of hello application server in effect for your Web Apps instance.</span></span> 
* <span data-ttu-id="691fe-107">Se você configurar seu aplicativo web usando a saudação da interface do usuário de configuração do Azure, Olá caminho toohello **webapps** pasta está na forma de saudação **d:\home\site\wwwroot\webapps**.</span><span class="sxs-lookup"><span data-stu-id="691fe-107">If you set up your web app by using hello Azure configuration UI, hello path toohello **webapps** folder is in hello form **d:\home\site\wwwroot\webapps**.</span></span> 

<span data-ttu-id="691fe-108">Observe que você pode usar tooupload de controle de origem, seu aplicativo ou páginas da web, incluindo [cenários de integração contínua](app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="691fe-108">Note that you can use source control tooupload your application or web pages, including [continuous integration scenarios](app-service-continuous-deployment.md).</span></span> <span data-ttu-id="691fe-109">FTP também é uma opção para carregar o aplicativo ou páginas da web; Para obter mais informações sobre como implantar seus aplicativos por FTP, consulte [implantar tooAzure seu aplicativo do serviço de aplicativo].</span><span class="sxs-lookup"><span data-stu-id="691fe-109">FTP is also an option for uploading your application or web pages; for more information about deploying your applications over FTP, see [Deploy your app tooAzure App Service].</span></span>

<span data-ttu-id="691fe-110">Observação para aplicativos da web Tomcat: depois de carregar seu toohello de arquivo WAR **webapps** pasta, o servidor de aplicativos Tomcat Olá detectará que você adicionou a ele e automaticamente carregá-lo.</span><span class="sxs-lookup"><span data-stu-id="691fe-110">Note for Tomcat web apps: Once you've uploaded your WAR file toohello **webapps** folder, hello Tomcat application server will detect that you've added it and will automatically load it.</span></span> <span data-ttu-id="691fe-111">Observe que, se você copiar o diretório de raiz de toohello de arquivos (exceto arquivos WAR), servidor de aplicativo hello precisará toobe reiniciado para que esses arquivos são usados.</span><span class="sxs-lookup"><span data-stu-id="691fe-111">Note that if you copy files (other than WAR files) toohello ROOT directory, hello application server will need toobe restarted before those files are used.</span></span> <span data-ttu-id="691fe-112">funcionalidade de autoload Olá para aplicativos da web Tomcat Java Olá em execução no Azure é baseada em um novo arquivo WAR que está sendo adicionado ou novos arquivos ou diretórios adicionados toohello **webapps** pasta.</span><span class="sxs-lookup"><span data-stu-id="691fe-112">hello autoload functionality for hello Tomcat Java web apps running on Azure is based on a new WAR file being added, or new files or directories added toohello **webapps** folder.</span></span> 

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="691fe-113">Consulte também</span><span class="sxs-lookup"><span data-stu-id="691fe-113">See Also</span></span>
<span data-ttu-id="691fe-114">Para obter mais informações sobre como usar o Azure com Java, consulte Olá [Centro de desenvolvedores de Java do Azure].</span><span class="sxs-lookup"><span data-stu-id="691fe-114">For more information about using Azure with Java, see hello [Azure Java Developer Center].</span></span>

[<span data-ttu-id="691fe-115">application-insights-app-insights-java-get-started</span><span class="sxs-lookup"><span data-stu-id="691fe-115">application-insights-app-insights-java-get-started</span></span>](../application-insights/app-insights-java-get-started.md)

<!-- URL List -->

[Centro de desenvolvedores de Java do Azure]: https://azure.microsoft.com/develop/java/
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
[implantar tooAzure seu aplicativo do serviço de aplicativo]: ./web-sites-deploy.md
