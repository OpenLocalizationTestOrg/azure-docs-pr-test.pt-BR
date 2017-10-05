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
# <a name="add-a-java-application-to-azure-app-service-web-apps"></a><span data-ttu-id="febd2-103">Adicionar um aplicativo Java a Aplicativos Web do Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="febd2-103">Add a Java application to Azure App Service Web Apps</span></span>
<span data-ttu-id="febd2-104">Após inicializar seu aplicativo Web do Java no [Serviço de Aplicativo do Azure][Azure App Service], conforme documentado em [Criar um aplicativo Web do Java no Serviço de Aplicativo do Azure](web-sites-java-get-started.md), você poderá carregar o aplicativo colocando o WAR na pasta **webapps**.</span><span class="sxs-lookup"><span data-stu-id="febd2-104">Once you have initialized your Java web app in [Azure App Service][Azure App Service] as documented at [Create a Java web app in Azure App Service](web-sites-java-get-started.md), you can upload your application by placing your WAR in the **webapps** folder.</span></span>

<span data-ttu-id="febd2-105">O caminho de navegação para a pasta **webapps** varia dependendo de como você configurou sua instância dos Aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="febd2-105">The navigation path to the **webapps** folder differs based on how you set up your Web Apps instance.</span></span>

* <span data-ttu-id="febd2-106">Se você configurar o aplicativo Web usando o Azure Marketplace, o caminho para a pasta **webapps** estará no formato **d:\home\site\wwwroot\bin\application\_server\webapps**, em que **application\_server** é o nome do servidor de aplicativos em vigor para a instância dos Aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="febd2-106">If you set up your web app by using the Azure Marketplace, the path to the **webapps** folder is in the form **d:\home\site\wwwroot\bin\application\_server\webapps**, where **application\_server** is the name of the application server in effect for your Web Apps instance.</span></span> 
* <span data-ttu-id="febd2-107">Se você configurar o aplicativo Web usando a interface do usuário de configuração do Azure, o caminho para a pasta **webapps** estará no formato **d:\home\site\wwwroot\webapps**.</span><span class="sxs-lookup"><span data-stu-id="febd2-107">If you set up your web app by using the Azure configuration UI, the path to the **webapps** folder is in the form **d:\home\site\wwwroot\webapps**.</span></span> 

<span data-ttu-id="febd2-108">Observe que você pode usar o controle do código-fonte para carregar o aplicativo ou páginas da web, incluindo [cenários de integração contínua](app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="febd2-108">Note that you can use source control to upload your application or web pages, including [continuous integration scenarios](app-service-continuous-deployment.md).</span></span> <span data-ttu-id="febd2-109">O FTP também é uma opção para carregar seu aplicativo ou páginas da web. Para obter mais informações sobre como implantar aplicativos por FTP, confira [Implantar seu aplicativo no Serviço de Aplicativo do Azure].</span><span class="sxs-lookup"><span data-stu-id="febd2-109">FTP is also an option for uploading your application or web pages; for more information about deploying your applications over FTP, see [Deploy your app to Azure App Service].</span></span>

<span data-ttu-id="febd2-110">Observação para aplicativos Web Tomcat: assim que você tiver carregado seu arquivo WAR na pasta **webapps** , o servidor do aplicativo Tomcat detectará que você o adicionou e o carregará automaticamente.</span><span class="sxs-lookup"><span data-stu-id="febd2-110">Note for Tomcat web apps: Once you've uploaded your WAR file to the **webapps** folder, the Tomcat application server will detect that you've added it and will automatically load it.</span></span> <span data-ttu-id="febd2-111">Observe que se você copiar arquivos (diferentes de arquivos WAR) no diretório raiz, o servidor de aplicativos precisará ser reiniciado para que esses arquivos sejam usados.</span><span class="sxs-lookup"><span data-stu-id="febd2-111">Note that if you copy files (other than WAR files) to the ROOT directory, the application server will need to be restarted before those files are used.</span></span> <span data-ttu-id="febd2-112">A funcionalidade de carregamento automático dos aplicativos Web Tomcat Java em execução no Azure baseia-se na adição de um novo arquivo WAR ou da adição de novos arquivos ou diretórios à pasta **webapps** .</span><span class="sxs-lookup"><span data-stu-id="febd2-112">The autoload functionality for the Tomcat Java web apps running on Azure is based on a new WAR file being added, or new files or directories added to the **webapps** folder.</span></span> 

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="febd2-113">Consulte também</span><span class="sxs-lookup"><span data-stu-id="febd2-113">See Also</span></span>
<span data-ttu-id="febd2-114">Para obter mais informações sobre como usar o Azure com o Java, confira a [Central de desenvolvimento Java do Azure].</span><span class="sxs-lookup"><span data-stu-id="febd2-114">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

[<span data-ttu-id="febd2-115">application-insights-app-insights-java-get-started</span><span class="sxs-lookup"><span data-stu-id="febd2-115">application-insights-app-insights-java-get-started</span></span>](../application-insights/app-insights-java-get-started.md)

<!-- URL List -->

<span data-ttu-id="febd2-116">[Central de desenvolvimento Java do Azure]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="febd2-116">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
<span data-ttu-id="febd2-117">[Implantar seu aplicativo no Serviço de Aplicativo do Azure]: ./web-sites-deploy.md</span><span class="sxs-lookup"><span data-stu-id="febd2-117">[Deploy your app to Azure App Service]: ./web-sites-deploy.md</span></span>
