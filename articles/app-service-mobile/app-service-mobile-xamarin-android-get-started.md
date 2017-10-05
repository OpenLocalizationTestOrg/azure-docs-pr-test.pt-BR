---
title: "Introdução aos aplicativos móveis do Azure para aplicativos Xamarin Android"
description: "Siga este tutorial para começar a usar os Aplicativos Móveis do Azure para desenvolvimento Android Xamarin"
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 81649dd3-544f-40ff-b9b7-60c66d683e60
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 6b41fd8090dd771fc40769c134bad258b3d4bd36
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-xamarinandroid-app"></a><span data-ttu-id="3d956-103">Criar um Aplicativo Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="3d956-103">Create a Xamarin.Android App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="3d956-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="3d956-104">Overview</span></span>
<span data-ttu-id="3d956-105">Este tutorial mostra como adicionar um serviço de back-end baseado em nuvem a um aplicativo Xamarin Android.</span><span class="sxs-lookup"><span data-stu-id="3d956-105">This tutorial shows you how to add a cloud-based backend service to a Xamarin.Android app.</span></span> <span data-ttu-id="3d956-106">Para saber mais, confira [O que são Aplicativos Móveis](app-service-mobile-value-prop.md).</span><span class="sxs-lookup"><span data-stu-id="3d956-106">For more information, see [What are Mobile Apps](app-service-mobile-value-prop.md).</span></span>

<span data-ttu-id="3d956-107">Uma captura de tela do aplicativo completo está disponível abaixo:</span><span class="sxs-lookup"><span data-stu-id="3d956-107">A screenshot from the completed app is below:</span></span>

![][0]

<span data-ttu-id="3d956-108">A conclusão deste tutorial é um pré-requisito para todos os outros tutoriais de Aplicativos Móveis para aplicativos Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="3d956-108">Completing this tutorial is a prerequisite for all other Mobile Apps tutorials for Xamarin.Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3d956-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3d956-109">Prerequisites</span></span>
<span data-ttu-id="3d956-110">Para concluir este tutorial, você precisará dos seguintes pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="3d956-110">To complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="3d956-111">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="3d956-111">An active Azure account.</span></span> <span data-ttu-id="3d956-112">Se você não tiver uma conta, inscreva-se para uma avaliação do Azure e obtenha até 10 aplicativos móveis gratuitos.</span><span class="sxs-lookup"><span data-stu-id="3d956-112">If you don't have an account, sign up for an Azure trial and get up to 10 free Mobile Apps.</span></span> <span data-ttu-id="3d956-113">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3d956-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="3d956-114">Visual Studio com Xamarin.</span><span class="sxs-lookup"><span data-stu-id="3d956-114">Visual Studio with Xamarin.</span></span> <span data-ttu-id="3d956-115">Veja [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) (Configuração e instalação para Visual Studio e Xamarin).</span><span class="sxs-lookup"><span data-stu-id="3d956-115">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) for instructions.</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="3d956-116">Criar um back-end de aplicativo móvel do Azure</span><span class="sxs-lookup"><span data-stu-id="3d956-116">Create an Azure Mobile App backend</span></span>
<span data-ttu-id="3d956-117">Siga estas etapas para criar um back-end de aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="3d956-117">Follow these steps to create a Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="3d956-118">Você acabou de provisionar um back-end do aplicativo móvel do Azure que pode ser usado pelos aplicativos móveis clientes.</span><span class="sxs-lookup"><span data-stu-id="3d956-118">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="3d956-119">Em seguida, baixe um projeto do servidor para um back-end simples da "lista de tarefas" e publique-o no Azure.</span><span class="sxs-lookup"><span data-stu-id="3d956-119">Next, download a server project for a simple "todo list" backend and publish it to Azure.</span></span>

## <a name="configure-the-server-project"></a><span data-ttu-id="3d956-120">Configurar o projeto de servidor</span><span class="sxs-lookup"><span data-stu-id="3d956-120">Configure the server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-xamarinandroid-app"></a><span data-ttu-id="3d956-121">Baixar e executar o aplicativo Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="3d956-121">Download and run the Xamarin.Android app</span></span>
1. <span data-ttu-id="3d956-122">Em **Baixar e executar seu projeto Xamarin.Android**, clique no botão **Baixar**.</span><span class="sxs-lookup"><span data-stu-id="3d956-122">Under **Download and run your Xamarin.Android project**, click the **Download** button.</span></span>

      <span data-ttu-id="3d956-123">Salve o arquivo do projeto compactado em seu computador local e anote onde ele foi salvo.</span><span class="sxs-lookup"><span data-stu-id="3d956-123">Save the compressed project file to your local computer, and make a note of where you save it.</span></span>
2. <span data-ttu-id="3d956-124">Pressione a tecla **F5** para compilar o projeto e iniciar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3d956-124">Press the **F5** key to build the project and start the app.</span></span>
3. <span data-ttu-id="3d956-125">No aplicativo, digite um texto significativo, como *Concluir o tutorial* e depois clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="3d956-125">In the app, type meaningful text, such as *Complete the tutorial* and then click the **Add** button.</span></span>

    ![][10]

    <span data-ttu-id="3d956-126">Os dados da solicitação são inseridos na tabela TodoItem.</span><span class="sxs-lookup"><span data-stu-id="3d956-126">Data from the request is inserted into the TodoItem table.</span></span> <span data-ttu-id="3d956-127">Itens armazenados na tabela são retornados pelo back-end do aplicativo móvel e os dados aparecem na lista.</span><span class="sxs-lookup"><span data-stu-id="3d956-127">Items stored in the table are returned by the mobile app backend, and the data appears in the list.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3d956-128">Você pode examinar o código que acessa o back-end do aplicativo móvel para consultar e inserir dados que estão localizados no arquivo ToDoActivity.cs C#.</span><span class="sxs-lookup"><span data-stu-id="3d956-128">You can review the code that accesses your mobile app backend to query and insert data, which is found in the ToDoActivity.cs C# file.</span></span>
   >
   >

## <a name="next-steps"></a><span data-ttu-id="3d956-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3d956-129">Next steps</span></span>
* [<span data-ttu-id="3d956-130">Adicionar sincronização offline ao seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="3d956-130">Add Offline Sync to your app</span></span>](app-service-mobile-xamarin-android-get-started-offline-data.md)
* [<span data-ttu-id="3d956-131">Adicionar autenticação ao seu aplicativo </span><span class="sxs-lookup"><span data-stu-id="3d956-131">Add authentication to your app </span></span>](app-service-mobile-xamarin-android-get-started-users.md)
* [<span data-ttu-id="3d956-132">Adicionar notificações por push ao seu aplicativo Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="3d956-132">Add push notifications to your Xamarin.Android app</span></span>](app-service-mobile-xamarin-android-get-started-push.md)
* [<span data-ttu-id="3d956-133">Como usar o cliente gerenciado para aplicativos móveis do Azure</span><span class="sxs-lookup"><span data-stu-id="3d956-133">How to use the managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Images. -->
[0]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-completed-android.png
[6]: ./media/app-service-mobile-xamarin-android-get-started/mobile-portal-quickstart-xamarin.png
[8]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-vs.png
[9]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-xs.png
[10]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-startup-android.png

<!-- URLs. -->
[Azure Portal]: https://azure.portal.com/
[Visual Studio]: https://go.microsoft.com/fwLink/p/?LinkID=534203
