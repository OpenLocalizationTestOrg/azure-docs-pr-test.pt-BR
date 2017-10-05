---
title: "Sobre Aplicativos Móveis no Serviço de Aplicativo do Azure"
description: "Saiba mais sobre as vantagens que o Serviço de Aplicativo traz para seus aplicativos móveis corporativos."
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: yochayk
editor: 
ms.assetid: 4e96cb9d-a632-4cf6-8219-0810d8ade3f9
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-multiple
ms.devlang: na
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: ac35ff9fe1c5f315c4de08de951f505627ec412b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <span data-ttu-id="153f7-103"><a name="getting-started"> </a>Sobre Aplicativos Móveis no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="153f7-103"><a name="getting-started"> </a>About Mobile Apps in Azure App Service</span></span>
<span data-ttu-id="153f7-104">O Serviço de Aplicativo do Azure é uma oferta de [PaaS](https://azure.microsoft.com/overview/what-is-paas/) (plataforma como um serviço) para desenvolvedores profissionais.</span><span class="sxs-lookup"><span data-stu-id="153f7-104">Azure App Service is a fully managed [platform as a service](https://azure.microsoft.com/overview/what-is-paas/) (PaaS) offering for professional developers.</span></span> <span data-ttu-id="153f7-105">O serviço oferece um conjunto avançado de recursos para cenários Web, móveis e de integração.</span><span class="sxs-lookup"><span data-stu-id="153f7-105">The service brings a rich set of capabilities to web, mobile, and integration scenarios.</span></span> 

<span data-ttu-id="153f7-106">O recurso Aplicativos Móveis do Serviço de Aplicativo do Azure dá aos desenvolvedores empresariais e integradores de sistema uma plataforma de desenvolvimento de aplicativos móveis que é altamente dimensionável e globalmente disponível.</span><span class="sxs-lookup"><span data-stu-id="153f7-106">The Mobile Apps feature of Azure App Service gives enterprise developers and system integrators a mobile-application development platform that's highly scalable and globally available.</span></span>

![Visão geral dos recursos dos Aplicativos Móveis](./media/app-service-mobile-value-prop/overview.png)

## <a name="why-mobile-apps"></a><span data-ttu-id="153f7-108">Por que os aplicativos móveis?</span><span class="sxs-lookup"><span data-stu-id="153f7-108">Why Mobile Apps?</span></span>
<span data-ttu-id="153f7-109">Com o recurso Aplicativos Móveis, você pode:</span><span class="sxs-lookup"><span data-stu-id="153f7-109">With the Mobile Apps feature, you can:</span></span>

* <span data-ttu-id="153f7-110">**Criar aplicativos nativos e multiplataforma**: quer você esteja criando aplicativos nativos iOS, Android e Windows ou aplicativos Xamarin ou Cordova (PhoneGap) multiplataforma, você pode aproveitar o Serviço de Aplicativo usando SDKs nativos.</span><span class="sxs-lookup"><span data-stu-id="153f7-110">**Build native and cross-platform apps**: Whether you're building native iOS, Android, and Windows apps or cross-platform Xamarin or Cordova (PhoneGap) apps, you can take advantage of App Service by using native SDKs.</span></span>
* <span data-ttu-id="153f7-111">**Conectar-se a seus sistemas corporativos**: com o recurso Aplicativos Móveis, você pode adicionar logon corporativo em minutos e conectar-se aos recursos locais ou de nuvem de sua empresa.</span><span class="sxs-lookup"><span data-stu-id="153f7-111">**Connect to your enterprise systems**: With the Mobile Apps feature, you can add corporate sign-in in minutes, and connect to your enterprise on-premises or cloud resources.</span></span>
* <span data-ttu-id="153f7-112">**Criar aplicativos prontos para uso offline com sincronização de dados**: torne sua força de trabalho móvel mais produtiva por meio da criação de aplicativos que trabalham offline e use Aplicativos Móveis para sincronizar dados em segundo plano quando houver conectividade com qualquer uma das suas origens de dados corporativos ou APIs SaaS (software como um serviço).</span><span class="sxs-lookup"><span data-stu-id="153f7-112">**Build offline-ready apps with data sync**: Make your mobile workforce more productive by building apps that work offline, and use Mobile Apps to sync data in the background when connectivity is present with any of your enterprise data sources or software as a service (SaaS) APIs.</span></span>
* <span data-ttu-id="153f7-113">**Notificações por push para milhões em segundos**: atraia seus clientes com notificações instantâneas de envio por push em qualquer dispositivo, personalizadas segundo suas necessidades e enviadas na hora certa.</span><span class="sxs-lookup"><span data-stu-id="153f7-113">**Push notifications to millions in seconds**: Engage your customers with instant push notifications on any device, personalized to their needs and sent when the time is right.</span></span>

## <a name="mobile-apps-features"></a><span data-ttu-id="153f7-114">Recursos dos Aplicativos Móveis</span><span class="sxs-lookup"><span data-stu-id="153f7-114">Mobile Apps features</span></span>
<span data-ttu-id="153f7-115">Os recursos a seguir são importantes para o desenvolvimento móvel habilitado para nuvem:</span><span class="sxs-lookup"><span data-stu-id="153f7-115">The following features are important to cloud-enabled mobile development:</span></span>

* <span data-ttu-id="153f7-116">**Autenticação e autorização**: selecione em uma lista crescente de provedores de identidade, incluindo o Azure Active Directory para autenticação corporativa, além de provedores sociais, como contas do Facebook, do Google, do Twitter e da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="153f7-116">**Authentication and authorization**: Select from an ever-growing list of identity providers, including Azure Active Directory for enterprise authentication, plus social providers such as Facebook, Google, Twitter, and Microsoft accounts.</span></span> <span data-ttu-id="153f7-117">Os Aplicativos Móveis oferecem um serviço OAuth 2.0 para cada provedor.</span><span class="sxs-lookup"><span data-stu-id="153f7-117">Mobile Apps offers an OAuth 2.0 service for each provider.</span></span> <span data-ttu-id="153f7-118">Você também pode integrar o SDK do provedor de identidade à funcionalidade específica do provedor.</span><span class="sxs-lookup"><span data-stu-id="153f7-118">You can also integrate the SDK for the identity provider for provider-specific functionality.</span></span>

    <span data-ttu-id="153f7-119">Descubra mais sobre os nossos [recursos de autenticação].</span><span class="sxs-lookup"><span data-stu-id="153f7-119">Discover more about our [authentication features].</span></span>

* <span data-ttu-id="153f7-120">**Acesso a Dados**: os Aplicativos Móveis fornecem uma fonte de dados OData v3 compatível com dispositivos móveis vinculada ao Banco de Dados SQL do Azure ou a um SQL Server local.</span><span class="sxs-lookup"><span data-stu-id="153f7-120">**Data access**: Mobile Apps provides a mobile-friendly OData v3 data source that's linked to Azure SQL Database or an on-premises SQL server.</span></span> <span data-ttu-id="153f7-121">Como esse serviço pode ser baseado no Entity Framework, você pode integrar facilmente com outros provedores de dados NoSQL e SQL, incluindo o [Armazenamento de Tabelas do Azure], o MongoDB, o [Azure Cosmos DB] e os provedores de API SaaS, como o Office 365 e o Salesforce.com.</span><span class="sxs-lookup"><span data-stu-id="153f7-121">Because this service can be based on Entity Framework, you can easily integrate with other NoSQL and SQL data providers, including [Azure Table storage], MongoDB, [Azure Cosmos DB], and SaaS API providers such as Office 365 and Salesforce.com.</span></span>

* <span data-ttu-id="153f7-122">**Sincronização offline**: os SDKs do nosso cliente facilita a criação de aplicativos móveis robustos e dinâmicos que funcionam com um conjunto de dados offline.</span><span class="sxs-lookup"><span data-stu-id="153f7-122">**Offline sync**: Our client SDKs make it easy to build robust and responsive mobile applications that operate with an offline dataset.</span></span> <span data-ttu-id="153f7-123">Você pode sincronizar esse conjunto de dados automaticamente com os dados de back-end, incluindo o suporte a resolução de conflitos.</span><span class="sxs-lookup"><span data-stu-id="153f7-123">You can sync this dataset automatically with the back-end data, including conflict-resolution support.</span></span>

  <span data-ttu-id="153f7-124">Descubra mais sobre nossos [recursos de dados].</span><span class="sxs-lookup"><span data-stu-id="153f7-124">Discover more about our [data features].</span></span>

* <span data-ttu-id="153f7-125">**Notificações por push**: nossos SDKs de cliente se integram perfeitamente aos recursos de registro dos Hubs de Notificação do Azure, permitindo que você envie notificações por push para milhões de usuários simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="153f7-125">**Push notifications**: Our client SDKs integrate seamlessly with the registration capabilities of Azure Notification Hubs, so you can send push notifications to millions of users simultaneously.</span></span>

  <span data-ttu-id="153f7-126">Descubra mais sobre os nossos [recursos de notificação por push].</span><span class="sxs-lookup"><span data-stu-id="153f7-126">Discover more about our [push notification features].</span></span>

* <span data-ttu-id="153f7-127">**SDKs de Cliente**: fornecemos um conjunto completo de SDKs de Cliente que abrangem o desenvolvimento nativo ([iOS], [Android] e [Windows]), desenvolvimento de plataforma cruzada ([Xamarin.iOS e Xamarin.Android], [Xamarin.Forms]) e o desenvolvimento de aplicativos híbridos ([Apache Cordova]).</span><span class="sxs-lookup"><span data-stu-id="153f7-127">**Client SDKs**: We provide a complete set of client SDKs that cover native development ([iOS], [Android], and [Windows]), cross-platform development ([Xamarin.iOS and Xamarin.Android], [Xamarin.Forms]), and hybrid application development ([Apache Cordova]).</span></span> <span data-ttu-id="153f7-128">Cada SDK de cliente está disponível com uma licença MIT e é software livre.</span><span class="sxs-lookup"><span data-stu-id="153f7-128">Each client SDK is available with an MIT license and is open source.</span></span>

## <a name="azure-app-service-features"></a><span data-ttu-id="153f7-129">Recursos do Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="153f7-129">Azure App Service features</span></span>
<span data-ttu-id="153f7-130">Os recursos de plataforma abaixo são úteis para sites de produção móvel:</span><span class="sxs-lookup"><span data-stu-id="153f7-130">The following platform features are useful for mobile production sites:</span></span>

* <span data-ttu-id="153f7-131">**Dimensionamento automático**: com o Serviço de Aplicativo, você pode escalar verticalmente ou horizontalmente de maneira fácil para lidar com todas as cargas clientes de entrada.</span><span class="sxs-lookup"><span data-stu-id="153f7-131">**Autoscaling**: With App Service, you can quickly scale up or scale out to handle any incoming customer load.</span></span> <span data-ttu-id="153f7-132">Selecione o número e o tamanho das VMs manualmente ou configure o dimensionamento automático para dimensionar seu back-end de aplicativo móvel com base na carga ou a agenda.</span><span class="sxs-lookup"><span data-stu-id="153f7-132">Manually select the number and size of VMs, or set up autoscaling to scale your mobile-app back end based on load or schedule.</span></span>

  <span data-ttu-id="153f7-133">Descubra mais sobre o [dimensionamento automático].</span><span class="sxs-lookup"><span data-stu-id="153f7-133">Discover more about [autoscaling].</span></span>

* <span data-ttu-id="153f7-134">**Ambientes de Preparo**: o Serviço de Aplicativo pode executar várias versões do seu site, permitindo que você execute um teste A/B, um teste em produção como parte de um plano de DevOps maior e o preparo de um novo back-end.</span><span class="sxs-lookup"><span data-stu-id="153f7-134">**Staging environments**: App Service can run multiple versions of your site, so you can perform A/B testing, test in production as part of a larger DevOps plan, and do in-place staging of a new back end.</span></span>

  <span data-ttu-id="153f7-135">Descubra mais sobre [ambientes de preparo].</span><span class="sxs-lookup"><span data-stu-id="153f7-135">Discover more about [staging environments].</span></span>

* <span data-ttu-id="153f7-136">**Implantação contínua**: o Serviço de Aplicativo pode integrar sistemas SCM (Gerenciador de Controle de Serviço) comuns, permitindo que você implante automaticamente uma nova versão do seu back-end por push para uma ramificação de seu sistema SCM.</span><span class="sxs-lookup"><span data-stu-id="153f7-136">**Continuous deployment**: App Service can integrate with common supply chain management (SCM) systems, so you can automatically deploy a new version of your back end by pushing to a branch of your SCM system.</span></span>

  <span data-ttu-id="153f7-137">Descubra mais sobre [opções de implantação].</span><span class="sxs-lookup"><span data-stu-id="153f7-137">Discover more about [deployment options].</span></span>

* <span data-ttu-id="153f7-138">**Rede virtual**: o Serviço de Aplicativo pode se conectar a recursos locais usando a rede virtual, o Azure ExpressRoute ou conexões híbridas.</span><span class="sxs-lookup"><span data-stu-id="153f7-138">**Virtual networking**: App Service can connect to on-premises resources by using virtual network, Azure ExpressRoute, or hybrid connections.</span></span>

  <span data-ttu-id="153f7-139">Descubra mais sobre as [conexões híbridas], as [redes virtuais] e o [ExpressRoute].</span><span class="sxs-lookup"><span data-stu-id="153f7-139">Discover more about [hybrid connections], [virtual networks], and [ExpressRoute].</span></span>

* <span data-ttu-id="153f7-140">**Ambientes Isolados e dedicados**: você pode executar o Serviço de Aplicativo em um ambiente totalmente isolado e dedicado para executar com segurança aplicativos do Serviço de Aplicativo do Azure em alta escala.</span><span class="sxs-lookup"><span data-stu-id="153f7-140">**Isolated and dedicated environments**: You can run App Service in a fully isolated and dedicated environment for securely running Azure App Service apps at high scale.</span></span> <span data-ttu-id="153f7-141">Esse ambiente é ideal para cargas de trabalho de aplicativos que exigem escala alta, isolamento ou acesso seguro à rede.</span><span class="sxs-lookup"><span data-stu-id="153f7-141">This environment is ideal for application workloads that require high scale, isolation, or secure network access.</span></span>

  <span data-ttu-id="153f7-142">Descubra mais sobre os [Ambientes do Serviço de Aplicativo].</span><span class="sxs-lookup"><span data-stu-id="153f7-142">Discover more about [App Service environments].</span></span>

## <a name="next-steps"></a><span data-ttu-id="153f7-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="153f7-143">Next steps</span></span>

<span data-ttu-id="153f7-144">Para começar a usar os Aplicativos Móveis no Serviço de Aplicativo do Azure, conclua o tutorial de [introdução].</span><span class="sxs-lookup"><span data-stu-id="153f7-144">To get started with Mobile Apps in Azure App Service, complete the [getting started] tutorial.</span></span> <span data-ttu-id="153f7-145">O tutorial abrange os fundamentos da produção de um back-end móvel e um cliente de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="153f7-145">The tutorial covers the basics of producing a mobile back end and client of your choice.</span></span> <span data-ttu-id="153f7-146">Ele também aborda a integração de autenticação, sincronização offline e notificações por push.</span><span class="sxs-lookup"><span data-stu-id="153f7-146">It also covers integrating authentication, offline sync, and push notifications.</span></span> <span data-ttu-id="153f7-147">Você pode concluir o tutorial várias vezes, uma vez para cada aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="153f7-147">You can complete the tutorial multiple times, once for each client application.</span></span>

<span data-ttu-id="153f7-148">Para saber mais sobre Aplicativos Móveis, reveja nosso [mapa de aprendizado].</span><span class="sxs-lookup"><span data-stu-id="153f7-148">For more information about Mobile Apps, review our [learning map].</span></span>
<span data-ttu-id="153f7-149">Para obter mais informações sobre a plataforma de Serviço de Aplicativo do Azure, consulte [Serviço de Aplicativo do Azure].</span><span class="sxs-lookup"><span data-stu-id="153f7-149">For more information about the Azure App Service platform, see [Azure App Service].</span></span>

<!-- URLs. -->
[Migrate your mobile service to App Service]: app-service-mobile-migrating-from-mobile-services.md
[Serviço de Aplicativo do Azure]: ../app-service/app-service-value-prop-what-is.md
[introdução]: app-service-mobile-ios-get-started.md
[Armazenamento de Tabelas do Azure]:../cosmos-db/table-storage-how-to-use-dotnet.md
[Azure Cosmos DB]: ../cosmos-db/documentdb-get-started.md
[recursos de autenticação]: ./app-service-mobile-auth.md
[recursos de dados]: ./app-service-mobile-offline-data-sync.md
[recursos de notificação por push]: ../notification-hubs/notification-hubs-push-notification-overview.md
[iOS]: ./app-service-mobile-ios-how-to-use-client-library.md
[Android]: ./app-service-mobile-android-how-to-use-client-library.md
[Windows]: ./app-service-mobile-dotnet-how-to-use-client-library.md
[Xamarin.iOS e Xamarin.Android]: ./app-service-mobile-dotnet-how-to-use-client-library.md
[Xamarin.Forms]: ./app-service-mobile-xamarin-forms-get-started.md
[Apache Cordova]: ./app-service-mobile-cordova-how-to-use-client-library.md
[dimensionamento automático]: ../app-service-web/web-sites-scale.md
[ambientes de preparo]: ../app-service-web/web-sites-staged-publishing.md
[opções de implantação]: ../app-service-web/web-sites-deploy.md
[conexões híbridas]: ../app-service-web/web-sites-hybrid-connection-get-started.md
[redes virtuais]: ../app-service-web/web-sites-integrate-with-vnet.md
[ExpressRoute]: ../app-service-web/app-service-app-service-environment-network-configuration-expressroute.md
[Ambientes do Serviço de Aplicativo]: ../app-service-web/app-service-app-service-environment-intro.md
[mapa de aprendizado]: https://azure.microsoft.com/en-us/documentation/learning-paths/appservice-mobileapps/
