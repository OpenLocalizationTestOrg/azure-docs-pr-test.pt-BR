---
title: "aaaCreate um aplicativo Cordova em aplicativos de celular do serviço de aplicativo do Azure | Microsoft Docs"
description: "Siga este tutorial tooget iniciado com o uso de back-ends dos aplicativos móveis do Azure para o desenvolvimento do Apache Cordova"
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
ms.openlocfilehash: 4981cbc0686c15230019ac9f30495f30cbf2c791
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-cordova-app"></a><span data-ttu-id="56064-104">Criar um aplicativo Apache Cordova</span><span class="sxs-lookup"><span data-stu-id="56064-104">Create an Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="56064-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="56064-105">Overview</span></span>
<span data-ttu-id="56064-106">Este tutorial mostra como tooadd um back-end baseado em nuvem serviço aplicativo móvel do Apache Cordova tooan usando um back-end do aplicativo móvel do Azure.</span><span class="sxs-lookup"><span data-stu-id="56064-106">This tutorial shows you how tooadd a cloud-based backend service tooan Apache Cordova mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="56064-107">Você criará um novo back-end do aplicativo móvel e um aplicativo Apache Cordova simples com *Lista de tarefas pendentes* que armazena dados de aplicativo no Azure.</span><span class="sxs-lookup"><span data-stu-id="56064-107">You create both a new mobile app backend and a simple *Todo list* Apache Cordova app that stores app data in Azure.</span></span>

<span data-ttu-id="56064-108">Concluir este tutorial é um pré-requisito para todos os outros tutoriais do Apache Cordova sobre como usar o recurso de aplicativos móveis Olá no serviço de aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="56064-108">Completing this tutorial is a prerequisite for all other Apache Cordova tutorials about using hello Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="56064-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="56064-109">Prerequisites</span></span>
<span data-ttu-id="56064-110">toocomplete neste tutorial, você precisa Olá pré-requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="56064-110">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="56064-111">Um computador com o [Visual Studio Community 2017] ou mais recente.</span><span class="sxs-lookup"><span data-stu-id="56064-111">A PC with [Visual Studio Community 2017] or newer.</span></span>
* <span data-ttu-id="56064-112">[Ferramentas do Visual Studio para Apache Cordova].</span><span class="sxs-lookup"><span data-stu-id="56064-112">[Visual Studio Tools for Apache Cordova].</span></span>
* <span data-ttu-id="56064-113">Uma [conta ativa do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="56064-113">An [active Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="56064-114">Você também pode ignorar o Visual Studio e usar a linha de comando do Apache Cordova Olá diretamente.</span><span class="sxs-lookup"><span data-stu-id="56064-114">You may also bypass Visual Studio and use hello Apache Cordova command line directly.</span></span>  <span data-ttu-id="56064-115">Usando a linha de comando Olá é útil quando concluir Olá tutorial em um computador Mac.</span><span class="sxs-lookup"><span data-stu-id="56064-115">Using hello command line is useful when completing hello tutorial on a Mac computer.</span></span>  <span data-ttu-id="56064-116">Compilar aplicativos de cliente do Apache Cordova usando a linha de comando Olá não é coberto por este tutorial.</span><span class="sxs-lookup"><span data-stu-id="56064-116">Compiling Apache Cordova client applications using hello command line is not covered by this tutorial.</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="56064-117">Criar um back-end de aplicativo móvel do Azure</span><span class="sxs-lookup"><span data-stu-id="56064-117">Create an Azure mobile app backend</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

[<span data-ttu-id="56064-118">Assista a um vídeo que mostra etapas semelhantes</span><span class="sxs-lookup"><span data-stu-id="56064-118">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-1-Create-an-Azure-Mobile-App)

## <a name="configure-hello-server-project"></a><span data-ttu-id="56064-119">Configurar o projeto do servidor de saudação</span><span class="sxs-lookup"><span data-stu-id="56064-119">Configure hello server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-apache-cordova-app"></a><span data-ttu-id="56064-120">Baixe e execute o aplicativo do Apache Cordova Olá</span><span class="sxs-lookup"><span data-stu-id="56064-120">Download and run hello Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-cordova-run-app](../../includes/app-service-mobile-cordova-run-app.md)]

## <a name="next-steps"></a><span data-ttu-id="56064-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="56064-121">Next Steps</span></span>
<span data-ttu-id="56064-122">Agora que você concluiu este tutorial de início rápido, passar tooone de saudação tutoriais a seguir:</span><span class="sxs-lookup"><span data-stu-id="56064-122">Now that you completed this quick start tutorial, move on tooone of hello following tutorials:</span></span>

* <span data-ttu-id="56064-123">[Adicionar dados Offline](app-service-mobile-cordova-get-started-offline-data.md) tooyour Apache Cordova app.</span><span class="sxs-lookup"><span data-stu-id="56064-123">[Add Offline Data](app-service-mobile-cordova-get-started-offline-data.md) tooyour Apache Cordova app.</span></span>
* <span data-ttu-id="56064-124">[Adicionar autenticação](app-service-mobile-cordova-get-started-users.md) tooyour Apache Cordova app.</span><span class="sxs-lookup"><span data-stu-id="56064-124">[Add Authentication](app-service-mobile-cordova-get-started-users.md) tooyour Apache Cordova app.</span></span>
* <span data-ttu-id="56064-125">[Adicionar notificações por Push](app-service-mobile-cordova-get-started-push.md) tooyour Apache Cordova app.</span><span class="sxs-lookup"><span data-stu-id="56064-125">[Add Push Notifications](app-service-mobile-cordova-get-started-push.md) tooyour Apache Cordova app.</span></span>

<span data-ttu-id="56064-126">Saiba mais sobre os principais conceitos com o Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="56064-126">Learn more about key concepts with Azure App Service.</span></span>

* <span data-ttu-id="56064-127">[Dados Off-line]</span><span class="sxs-lookup"><span data-stu-id="56064-127">[Offline Data]</span></span>
* <span data-ttu-id="56064-128">[Autenticação]</span><span class="sxs-lookup"><span data-stu-id="56064-128">[Authentication]</span></span>
* <span data-ttu-id="56064-129">[Notificações por Push]</span><span class="sxs-lookup"><span data-stu-id="56064-129">[Push Notifications]</span></span>

<span data-ttu-id="56064-130">Saiba como toouse Olá SDKs.</span><span class="sxs-lookup"><span data-stu-id="56064-130">Learn how toouse hello SDKs.</span></span>

* <span data-ttu-id="56064-131">[SDK do Apache Cordova]</span><span class="sxs-lookup"><span data-stu-id="56064-131">[Apache Cordova SDK]</span></span>
* <span data-ttu-id="56064-132">[SDK do Servidor ASP.NET]</span><span class="sxs-lookup"><span data-stu-id="56064-132">[ASP.NET Server SDK]</span></span>
* <span data-ttu-id="56064-133">[SDK do Servidor Node.js]</span><span class="sxs-lookup"><span data-stu-id="56064-133">[Node.js Server SDK]</span></span>

<!-- Images. -->

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2017]: http://www.visualstudio.com/
[Ferramentas do Visual Studio para Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[Dados Off-line]: app-service-mobile-offline-data-sync.md
[Autenticação]: app-service-mobile-auth.md
[Notificações por Push]: ../notification-hubs/notification-hubs-push-notification-overview.md
[SDK do Apache Cordova]: app-service-mobile-cordova-how-to-use-client-library.md
[SDK do Servidor ASP.NET]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[SDK do Servidor Node.js]: app-service-mobile-node-backend-how-to-use-server-sdk.md
