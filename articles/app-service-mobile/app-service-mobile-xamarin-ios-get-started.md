---
title: "Introdução aos Aplicativos Móveis do Serviço de Aplicativo do Azure para aplicativos Xamarin.iOS | Microsoft Docs"
description: "Siga este tutorial para começar a usar os Aplicativos Móveis para desenvolvimento do Xamarin.iOS."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 14428794-52ad-4b51-956c-deb296cafa34
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: syntaxc4
ms.openlocfilehash: 8dc965df2cd45366970effb29f246b0045a94717
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-xamarinios-app"></a><span data-ttu-id="d2aa0-103">Criar um aplicativo Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="d2aa0-103">Create a Xamarin.iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="d2aa0-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="d2aa0-104">Overview</span></span>
<span data-ttu-id="d2aa0-105">Este tutorial mostra como adicionar um serviço de back-end baseado em nuvem a um aplicativo móvel Xamarin.iOS usando um back-end de Aplicativo Móvel do Azure.</span><span class="sxs-lookup"><span data-stu-id="d2aa0-105">This tutorial shows you how to add a cloud-based backend service to a Xamarin.iOS mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="d2aa0-106">Você cria um novo back-end do aplicativo móvel e um aplicativo Xamarin.iOS *Todo list* simples que armazena dados de aplicativo no Azure.</span><span class="sxs-lookup"><span data-stu-id="d2aa0-106">You create both a new mobile app backend and a simple *Todo list* Xamarin.iOS app that stores app data in Azure.</span></span>

<span data-ttu-id="d2aa0-107">Concluir este tutorial é um pré-requisito para todos os outros tutoriais do Xamarin.iOS sobre como usar o recurso de Aplicativos Móveis no Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="d2aa0-107">Completing this tutorial is a prerequisite for all other Xamarin.iOS tutorials about using the Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d2aa0-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d2aa0-108">Prerequisites</span></span>
<span data-ttu-id="d2aa0-109">Para concluir este tutorial, você precisará dos seguintes pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="d2aa0-109">To complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="d2aa0-110">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="d2aa0-110">An active Azure account.</span></span> <span data-ttu-id="d2aa0-111">Caso você não tenha uma conta, inscreva-se para uma avaliação do Azure e obtenha até 10 aplicativos móveis gratuitos que você pode continuar a usar mesmo após o fim do seu período de avaliação.</span><span class="sxs-lookup"><span data-stu-id="d2aa0-111">If you don't have an account, sign up for an Azure trial and get up to 10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="d2aa0-112">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d2aa0-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="d2aa0-113">Visual Studio com Xamarin.</span><span class="sxs-lookup"><span data-stu-id="d2aa0-113">Visual Studio with Xamarin.</span></span> <span data-ttu-id="d2aa0-114">Veja [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) (Configuração e instalação para Visual Studio e Xamarin).</span><span class="sxs-lookup"><span data-stu-id="d2aa0-114">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) for instructions.</span></span>
* <span data-ttu-id="d2aa0-115">Um Mac com Xcode v7.0 ou posterior e o Xamarin Studio Community instalados.</span><span class="sxs-lookup"><span data-stu-id="d2aa0-115">A Mac with Xcode v7.0 or later and Xamarin Studio Community installed.</span></span> <span data-ttu-id="d2aa0-116">Veja [Configuração e instalação para Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) e [Configuração, instalação e verificações para usuários do Mac](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span><span class="sxs-lookup"><span data-stu-id="d2aa0-116">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) and [Setup, install, and verifications for Mac users](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="d2aa0-117">Criar um back-end de aplicativo móvel do Azure</span><span class="sxs-lookup"><span data-stu-id="d2aa0-117">Create an Azure Mobile App backend</span></span>
<span data-ttu-id="d2aa0-118">Siga estas etapas para criar um back-end de aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="d2aa0-118">Follow these steps to create a Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-the-server-project"></a><span data-ttu-id="d2aa0-119">Configurar o projeto de servidor</span><span class="sxs-lookup"><span data-stu-id="d2aa0-119">Configure the server project</span></span>
<span data-ttu-id="d2aa0-120">Você acabou de provisionar um back-end do aplicativo móvel do Azure que pode ser usado pelos aplicativos móveis clientes.</span><span class="sxs-lookup"><span data-stu-id="d2aa0-120">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="d2aa0-121">Em seguida, baixe um projeto do servidor para um back-end simples da "lista de tarefas" e publique-o no Azure.</span><span class="sxs-lookup"><span data-stu-id="d2aa0-121">Next, download a server project for a simple "todo list" backend and publish it to Azure.</span></span>

<span data-ttu-id="d2aa0-122">Siga as etapas a seguir para configurar o projeto de servidor para usar o back-end Node.js ou .NET.</span><span class="sxs-lookup"><span data-stu-id="d2aa0-122">Follow the following steps to configure the server project to use either the Node.js or .NET backend.</span></span>

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-xamarinios-app"></a><span data-ttu-id="d2aa0-123">Baixar e executar o aplicativo Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="d2aa0-123">Download and run the Xamarin.iOS app</span></span>
1. <span data-ttu-id="d2aa0-124">Abra o [portal do Azure] em uma janela de navegador.</span><span class="sxs-lookup"><span data-stu-id="d2aa0-124">Open the [Azure portal] in a browser window.</span></span>
2. <span data-ttu-id="d2aa0-125">Na folha configurações do seu Aplicativo Móvel, clique em **Introdução** > **Xamarin.iOS**.</span><span class="sxs-lookup"><span data-stu-id="d2aa0-125">On the settings blade for your Mobile App, click **Get Started** > **Xamarin.iOS**.</span></span> <span data-ttu-id="d2aa0-126">Na etapa 3, clique em **Criar um novo aplicativo** se essa opção ainda não tiver sido selecionada.</span><span class="sxs-lookup"><span data-stu-id="d2aa0-126">Under step 3, click **Create a new app** if it's not already selected.</span></span>  <span data-ttu-id="d2aa0-127">Em seguida, clique no botão **Baixar** .</span><span class="sxs-lookup"><span data-stu-id="d2aa0-127">Next click the **Download** button.</span></span>

      <span data-ttu-id="d2aa0-128">Um aplicativo cliente que se conecta ao seu back-end móvel é baixado.</span><span class="sxs-lookup"><span data-stu-id="d2aa0-128">A client application that connects to your mobile backend is downloaded.</span></span> <span data-ttu-id="d2aa0-129">Salve o arquivo do projeto compactado em seu computador local e anote onde ele foi salvo.</span><span class="sxs-lookup"><span data-stu-id="d2aa0-129">Save the compressed project file to your local computer, and make a note of where you save it.</span></span>
3. <span data-ttu-id="d2aa0-130">Extraia o projeto que você baixou e abra-o no Xamarin Studio (ou no Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="d2aa0-130">Extract the project that you downloaded, and then open it in Xamarin Studio (or Visual Studio).</span></span>

    ![][9]

    ![][8]
4. <span data-ttu-id="d2aa0-131">Pressione a tecla F5 para compilar o projeto e iniciar o aplicativo no emulador do iPhone.</span><span class="sxs-lookup"><span data-stu-id="d2aa0-131">Press the F5 key to build the project and start the app in the iPhone emulator.</span></span>
5. <span data-ttu-id="d2aa0-132">No aplicativo, digite um texto significativo, como *Saiba mais sobre o Xamarin* e clique no botão **+**.</span><span class="sxs-lookup"><span data-stu-id="d2aa0-132">In the app, type meaningful text, such as *Learn Xamarin*, and then click the **+** button.</span></span>

    ![][10]

    <span data-ttu-id="d2aa0-133">Os dados da solicitação são inseridos na tabela TodoItem.</span><span class="sxs-lookup"><span data-stu-id="d2aa0-133">Data from the request is inserted into the TodoItem table.</span></span> <span data-ttu-id="d2aa0-134">Itens armazenados na tabela são retornados pelo back-end do aplicativo móvel e os dados são exibidos na lista.</span><span class="sxs-lookup"><span data-stu-id="d2aa0-134">Items stored in the table are returned by the mobile app backend, and the data is displayed in the list.</span></span>

> [!NOTE]
> <span data-ttu-id="d2aa0-135">Você pode examinar o código que acessa seu back-end de aplicativo móvel para consultar e inserir dados no arquivo C# QSTodoService.cs.</span><span class="sxs-lookup"><span data-stu-id="d2aa0-135">You can review the code that accesses your mobile app backend to query and insert data in the QSTodoService.cs C# file.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="d2aa0-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d2aa0-136">Next steps</span></span>
* [<span data-ttu-id="d2aa0-137">Adicionar sincronização offline ao seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="d2aa0-137">Add Offline Sync to your app</span></span>](app-service-mobile-xamarin-ios-get-started-offline-data.md)
* [<span data-ttu-id="d2aa0-138">Adicionar autenticação ao seu aplicativo </span><span class="sxs-lookup"><span data-stu-id="d2aa0-138">Add authentication to your app </span></span>](app-service-mobile-xamarin-ios-get-started-users.md)
* [<span data-ttu-id="d2aa0-139">Adicionar notificações por push ao seu aplicativo Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="d2aa0-139">Add push notifications to your Xamarin.Android app</span></span>](app-service-mobile-xamarin-ios-get-started-push.md)
* [<span data-ttu-id="d2aa0-140">Como usar o cliente gerenciado para aplicativos móveis do Azure</span><span class="sxs-lookup"><span data-stu-id="d2aa0-140">How to use the managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Anchors. -->
[Getting started with mobile app backends]:#getting-started
[Create a new mobile app backend]:#create-new-service
[Next Steps]:#next-steps

<!-- Images. -->
[6]: ./media/app-service-mobile-xamarin-ios-get-started/xamarin-ios-quickstart.png
[8]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-xamarin-project-ios-vs.png
[9]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-xamarin-project-ios-xs.png
[10]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-quickstart-startup-ios.png

<!-- URLs. -->
<span data-ttu-id="d2aa0-141">[portal do Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="d2aa0-141">[Azure portal]: https://portal.azure.com/</span></span>
