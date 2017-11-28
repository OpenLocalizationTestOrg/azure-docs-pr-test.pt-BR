---
title: "aaaGet iniciado com aplicativos de celular do serviço de aplicativo do Azure para aplicativos xamarin | Microsoft Docs"
description: "Siga este tutorial tooget iniciado com o uso de aplicativos móveis para o desenvolvimento do xamarin."
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
ms.openlocfilehash: 524c5ac4d8a29d7cb858f74132aad5d6e2201d02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinios-app"></a><span data-ttu-id="ee61d-103">Criar um aplicativo Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="ee61d-103">Create a Xamarin.iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="ee61d-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="ee61d-104">Overview</span></span>
<span data-ttu-id="ee61d-105">Este tutorial mostra como tooadd um back-end baseado em nuvem serviço aplicativo móvel do xamarin tooa usando um back-end do aplicativo móvel do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee61d-105">This tutorial shows you how tooadd a cloud-based backend service tooa Xamarin.iOS mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="ee61d-106">Você cria um novo back-end do aplicativo móvel e um aplicativo Xamarin.iOS *Todo list* simples que armazena dados de aplicativo no Azure.</span><span class="sxs-lookup"><span data-stu-id="ee61d-106">You create both a new mobile app backend and a simple *Todo list* Xamarin.iOS app that stores app data in Azure.</span></span>

<span data-ttu-id="ee61d-107">Concluir este tutorial é um pré-requisito para todos os outros tutoriais do xamarin sobre como usar o recurso de aplicativos móveis Olá no serviço de aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee61d-107">Completing this tutorial is a prerequisite for all other Xamarin.iOS tutorials about using hello Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ee61d-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ee61d-108">Prerequisites</span></span>
<span data-ttu-id="ee61d-109">toocomplete neste tutorial, você precisa Olá pré-requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="ee61d-109">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="ee61d-110">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee61d-110">An active Azure account.</span></span> <span data-ttu-id="ee61d-111">Se você não tiver uma conta, inscreva-se para uma avaliação do Azure e começar a too10 livre aplicativos móveis que você pode continuar usando até mesmo após o término de sua avaliação.</span><span class="sxs-lookup"><span data-stu-id="ee61d-111">If you don't have an account, sign up for an Azure trial and get up too10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="ee61d-112">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ee61d-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="ee61d-113">Visual Studio com Xamarin.</span><span class="sxs-lookup"><span data-stu-id="ee61d-113">Visual Studio with Xamarin.</span></span> <span data-ttu-id="ee61d-114">Veja [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) (Configuração e instalação para Visual Studio e Xamarin).</span><span class="sxs-lookup"><span data-stu-id="ee61d-114">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) for instructions.</span></span>
* <span data-ttu-id="ee61d-115">Um Mac com Xcode v7.0 ou posterior e o Xamarin Studio Community instalados.</span><span class="sxs-lookup"><span data-stu-id="ee61d-115">A Mac with Xcode v7.0 or later and Xamarin Studio Community installed.</span></span> <span data-ttu-id="ee61d-116">Veja [Configuração e instalação para Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) e [Configuração, instalação e verificações para usuários do Mac](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span><span class="sxs-lookup"><span data-stu-id="ee61d-116">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) and [Setup, install, and verifications for Mac users](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="ee61d-117">Criar um back-end de aplicativo móvel do Azure</span><span class="sxs-lookup"><span data-stu-id="ee61d-117">Create an Azure Mobile App backend</span></span>
<span data-ttu-id="ee61d-118">Siga essas etapas toocreate um back-end do aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="ee61d-118">Follow these steps toocreate a Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-hello-server-project"></a><span data-ttu-id="ee61d-119">Configurar o projeto do servidor de saudação</span><span class="sxs-lookup"><span data-stu-id="ee61d-119">Configure hello server project</span></span>
<span data-ttu-id="ee61d-120">Você acabou de provisionar um back-end do aplicativo móvel do Azure que pode ser usado pelos aplicativos móveis clientes.</span><span class="sxs-lookup"><span data-stu-id="ee61d-120">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="ee61d-121">Em seguida, baixar um projeto do servidor para um simples "lista de tarefas" back-end e publicá-lo tooAzure.</span><span class="sxs-lookup"><span data-stu-id="ee61d-121">Next, download a server project for a simple "todo list" backend and publish it tooAzure.</span></span>

<span data-ttu-id="ee61d-122">Siga Olá seguindo as etapas tooconfigure Olá servidor projeto toouse ou Olá Node. js ou .NET back-end.</span><span class="sxs-lookup"><span data-stu-id="ee61d-122">Follow hello following steps tooconfigure hello server project toouse either hello Node.js or .NET backend.</span></span>

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinios-app"></a><span data-ttu-id="ee61d-123">Baixe e execute o aplicativo de xamarin Olá</span><span class="sxs-lookup"><span data-stu-id="ee61d-123">Download and run hello Xamarin.iOS app</span></span>
1. <span data-ttu-id="ee61d-124">Olá abrir [portal do Azure] em uma janela do navegador.</span><span class="sxs-lookup"><span data-stu-id="ee61d-124">Open hello [Azure portal] in a browser window.</span></span>
2. <span data-ttu-id="ee61d-125">Na folha de configurações de saudação para seu aplicativo móvel, clique em **começar** > **xamarin**.</span><span class="sxs-lookup"><span data-stu-id="ee61d-125">On hello settings blade for your Mobile App, click **Get Started** > **Xamarin.iOS**.</span></span> <span data-ttu-id="ee61d-126">Na etapa 3, clique em **Criar um novo aplicativo** se essa opção ainda não tiver sido selecionada.</span><span class="sxs-lookup"><span data-stu-id="ee61d-126">Under step 3, click **Create a new app** if it's not already selected.</span></span>  <span data-ttu-id="ee61d-127">Em seguida clique Olá **baixar** botão.</span><span class="sxs-lookup"><span data-stu-id="ee61d-127">Next click hello **Download** button.</span></span>

      <span data-ttu-id="ee61d-128">Um aplicativo cliente que se conecta de back-end do tooyour móvel é baixado.</span><span class="sxs-lookup"><span data-stu-id="ee61d-128">A client application that connects tooyour mobile backend is downloaded.</span></span> <span data-ttu-id="ee61d-129">Salve o arquivo de projeto compactado de saudação em seu computador local e anote onde você salvá-lo.</span><span class="sxs-lookup"><span data-stu-id="ee61d-129">Save hello compressed project file to your local computer, and make a note of where you save it.</span></span>
3. <span data-ttu-id="ee61d-130">Extraia o projeto Olá que você baixou e abra-o no Xamarin Studio (ou o Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="ee61d-130">Extract hello project that you downloaded, and then open it in Xamarin Studio (or Visual Studio).</span></span>

    ![][9]

    ![][8]
4. <span data-ttu-id="ee61d-131">Pressione projeto de Olá Olá F5 toobuild chave e iniciar o aplicativo hello no emulador do iPhone hello.</span><span class="sxs-lookup"><span data-stu-id="ee61d-131">Press hello F5 key toobuild hello project and start hello app in hello iPhone emulator.</span></span>
5. <span data-ttu-id="ee61d-132">No aplicativo hello, digite o texto significativo, como *Saiba Xamarin*e, em seguida, clique em Olá  **+**  botão.</span><span class="sxs-lookup"><span data-stu-id="ee61d-132">In hello app, type meaningful text, such as *Learn Xamarin*, and then click hello **+** button.</span></span>

    ![][10]

    <span data-ttu-id="ee61d-133">Dados de solicitação de saudação são inseridos na tabela de TodoItem de saudação.</span><span class="sxs-lookup"><span data-stu-id="ee61d-133">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="ee61d-134">Itens armazenados na tabela de saudação são retornados pelo back-end de aplicativo móvel hello e os dados são exibidos na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="ee61d-134">Items stored in hello table are returned by hello mobile app backend, and the data is displayed in hello list.</span></span>

> [!NOTE]
> <span data-ttu-id="ee61d-135">Você pode examinar o código Olá que acessa o tooquery de back-end do aplicativo móvel e inserir dados em Olá arquivo QSTodoService.cs c#.</span><span class="sxs-lookup"><span data-stu-id="ee61d-135">You can review hello code that accesses your mobile app backend tooquery and insert data in hello QSTodoService.cs C# file.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="ee61d-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ee61d-136">Next steps</span></span>
* [<span data-ttu-id="ee61d-137">Adicionar aplicativo de tooyour sincronização Offline</span><span class="sxs-lookup"><span data-stu-id="ee61d-137">Add Offline Sync tooyour app</span></span>](app-service-mobile-xamarin-ios-get-started-offline-data.md)
* [<span data-ttu-id="ee61d-138">Adicionar autenticação tooyour aplicativo</span><span class="sxs-lookup"><span data-stu-id="ee61d-138">Add authentication tooyour app </span></span>](app-service-mobile-xamarin-ios-get-started-users.md)
* [<span data-ttu-id="ee61d-139">Adicionar aplicativo de xamarin de tooyour de notificações por push</span><span class="sxs-lookup"><span data-stu-id="ee61d-139">Add push notifications tooyour Xamarin.Android app</span></span>](app-service-mobile-xamarin-ios-get-started-push.md)
* [<span data-ttu-id="ee61d-140">Como toouse Olá gerenciada do cliente para aplicativos móveis do Azure</span><span class="sxs-lookup"><span data-stu-id="ee61d-140">How toouse hello managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)

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
[portal do Azure]: https://portal.azure.com/
