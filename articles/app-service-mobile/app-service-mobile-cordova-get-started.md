---
title: "Criar um aplicativo Cordova nos Aplicativos Móveis do Serviço de Aplicativo do Azure | Microsoft Docs"
description: "Siga este tutorial para começar a usar back-ends de aplicativos móveis do Azure para desenvolvimento do Apache Cordova"
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
tags: 
keywords: "cordova,javascript,móvel,cliente"
ms.assetid: 0b08fc12-0a80-42d3-9cc1-9b3f8d3e3a3f
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: hero-article
ms.date: 07/07/2017
ms.author: glenga
ms.openlocfilehash: b620465cdc3cfa04933dc6e70163fc32aa9a839b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-apache-cordova-app"></a><span data-ttu-id="d4576-104">Criar um aplicativo Apache Cordova</span><span class="sxs-lookup"><span data-stu-id="d4576-104">Create an Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="d4576-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="d4576-105">Overview</span></span>
<span data-ttu-id="d4576-106">Este tutorial mostra como adicionar um serviço de back-end baseado em nuvem a um aplicativo Apache Cordova móvel usando um back-end de aplicativo móvel do Azure.</span><span class="sxs-lookup"><span data-stu-id="d4576-106">This tutorial shows you how to add a cloud-based backend service to an Apache Cordova mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="d4576-107">Você criará um novo back-end do aplicativo móvel e um aplicativo Apache Cordova simples com *Lista de tarefas pendentes* que armazena dados de aplicativo no Azure.</span><span class="sxs-lookup"><span data-stu-id="d4576-107">You create both a new mobile app backend and a simple *Todo list* Apache Cordova app that stores app data in Azure.</span></span>

<span data-ttu-id="d4576-108">A conclusão deste tutorial é um pré-requisito para todos os outros tutoriais do Apache Cordova sobre como usar o recurso de Aplicativos Móveis no Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="d4576-108">Completing this tutorial is a prerequisite for all other Apache Cordova tutorials about using the Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d4576-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d4576-109">Prerequisites</span></span>
<span data-ttu-id="d4576-110">Para concluir este tutorial, você precisará dos seguintes pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="d4576-110">To complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="d4576-111">Um computador com o [Visual Studio Community 2017] ou mais recente.</span><span class="sxs-lookup"><span data-stu-id="d4576-111">A PC with [Visual Studio Community 2017] or newer.</span></span>
* <span data-ttu-id="d4576-112">[Ferramentas do Visual Studio para Apache Cordova].</span><span class="sxs-lookup"><span data-stu-id="d4576-112">[Visual Studio Tools for Apache Cordova].</span></span>
* <span data-ttu-id="d4576-113">Uma [conta ativa do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d4576-113">An [active Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="d4576-114">Você também pode ignorar o Visual Studio e usar a linha de comando do Apache Cordova diretamente.</span><span class="sxs-lookup"><span data-stu-id="d4576-114">You may also bypass Visual Studio and use the Apache Cordova command line directly.</span></span>  <span data-ttu-id="d4576-115">Usar a linha de comando é útil ao concluir o tutorial em um computador Mac.</span><span class="sxs-lookup"><span data-stu-id="d4576-115">Using the command line is useful when completing the tutorial on a Mac computer.</span></span>  <span data-ttu-id="d4576-116">Compilar aplicativos de cliente do Apache Cordova usando a linha de comando não é coberto por este tutorial.</span><span class="sxs-lookup"><span data-stu-id="d4576-116">Compiling Apache Cordova client applications using the command line is not covered by this tutorial.</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="d4576-117">Criar um back-end de aplicativo móvel do Azure</span><span class="sxs-lookup"><span data-stu-id="d4576-117">Create an Azure mobile app backend</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

[<span data-ttu-id="d4576-118">Assista a um vídeo que mostra etapas semelhantes</span><span class="sxs-lookup"><span data-stu-id="d4576-118">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-1-Create-an-Azure-Mobile-App)

## <a name="configure-the-server-project"></a><span data-ttu-id="d4576-119">Configurar o projeto de servidor</span><span class="sxs-lookup"><span data-stu-id="d4576-119">Configure the server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-apache-cordova-app"></a><span data-ttu-id="d4576-120">Baixe e execute o aplicativo Apache Cordova</span><span class="sxs-lookup"><span data-stu-id="d4576-120">Download and run the Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-cordova-run-app](../../includes/app-service-mobile-cordova-run-app.md)]

## <a name="next-steps"></a><span data-ttu-id="d4576-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d4576-121">Next Steps</span></span>
<span data-ttu-id="d4576-122">Agora que você concluiu este tutorial de início rápido, passe para um dos tutoriais a seguir:</span><span class="sxs-lookup"><span data-stu-id="d4576-122">Now that you completed this quick start tutorial, move on to one of the following tutorials:</span></span>

* <span data-ttu-id="d4576-123">[Adicionar Dados Offline](app-service-mobile-cordova-get-started-offline-data.md) para o aplicativo Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="d4576-123">[Add Offline Data](app-service-mobile-cordova-get-started-offline-data.md) to your Apache Cordova app.</span></span>
* <span data-ttu-id="d4576-124">[Adicionar autenticação](app-service-mobile-cordova-get-started-users.md) ao aplicativo Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="d4576-124">[Add Authentication](app-service-mobile-cordova-get-started-users.md) to your Apache Cordova app.</span></span>
* <span data-ttu-id="d4576-125">[Adicionar notificações por push](app-service-mobile-cordova-get-started-push.md) a seu aplicativo Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="d4576-125">[Add Push Notifications](app-service-mobile-cordova-get-started-push.md) to your Apache Cordova app.</span></span>

<span data-ttu-id="d4576-126">Saiba mais sobre os principais conceitos com o Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="d4576-126">Learn more about key concepts with Azure App Service.</span></span>

* <span data-ttu-id="d4576-127">[Dados Off-line]</span><span class="sxs-lookup"><span data-stu-id="d4576-127">[Offline Data]</span></span>
* <span data-ttu-id="d4576-128">[Autenticação]</span><span class="sxs-lookup"><span data-stu-id="d4576-128">[Authentication]</span></span>
* <span data-ttu-id="d4576-129">[Notificações por Push]</span><span class="sxs-lookup"><span data-stu-id="d4576-129">[Push Notifications]</span></span>

<span data-ttu-id="d4576-130">Saiba como usar os SDKs.</span><span class="sxs-lookup"><span data-stu-id="d4576-130">Learn how to use the SDKs.</span></span>

* <span data-ttu-id="d4576-131">[SDK do Apache Cordova]</span><span class="sxs-lookup"><span data-stu-id="d4576-131">[Apache Cordova SDK]</span></span>
* <span data-ttu-id="d4576-132">[SDK do Servidor ASP.NET]</span><span class="sxs-lookup"><span data-stu-id="d4576-132">[ASP.NET Server SDK]</span></span>
* <span data-ttu-id="d4576-133">[SDK do Servidor Node.js]</span><span class="sxs-lookup"><span data-stu-id="d4576-133">[Node.js Server SDK]</span></span>

<!-- Images. -->

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
<span data-ttu-id="d4576-134">[Visual Studio Community 2017]: http://www.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="d4576-134">[Visual Studio Community 2017]: http://www.visualstudio.com/</span></span>
<span data-ttu-id="d4576-135">[Ferramentas do Visual Studio para Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx</span><span class="sxs-lookup"><span data-stu-id="d4576-135">[Visual Studio Tools for Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx</span></span>
<span data-ttu-id="d4576-136">[Dados Off-line]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="d4576-136">[Offline Data]: app-service-mobile-offline-data-sync.md</span></span>
<span data-ttu-id="d4576-137">[Autenticação]: app-service-mobile-auth.md</span><span class="sxs-lookup"><span data-stu-id="d4576-137">[Authentication]: app-service-mobile-auth.md</span></span>
<span data-ttu-id="d4576-138">[Notificações por Push]: ../notification-hubs/notification-hubs-push-notification-overview.md</span><span class="sxs-lookup"><span data-stu-id="d4576-138">[Push Notifications]: ../notification-hubs/notification-hubs-push-notification-overview.md</span></span>
<span data-ttu-id="d4576-139">[SDK do Apache Cordova]: app-service-mobile-cordova-how-to-use-client-library.md</span><span class="sxs-lookup"><span data-stu-id="d4576-139">[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md</span></span>
<span data-ttu-id="d4576-140">[SDK do Servidor ASP.NET]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md</span><span class="sxs-lookup"><span data-stu-id="d4576-140">[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md</span></span>
<span data-ttu-id="d4576-141">[SDK do Servidor Node.js]: app-service-mobile-node-backend-how-to-use-server-sdk.md</span><span class="sxs-lookup"><span data-stu-id="d4576-141">[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md</span></span>
