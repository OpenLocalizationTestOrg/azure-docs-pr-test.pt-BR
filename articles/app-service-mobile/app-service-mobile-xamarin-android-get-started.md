---
title: "aaaGet iniciado com aplicativos móveis do Azure para aplicativos xamarin"
description: "Siga este tutorial tooget iniciado usando aplicativos móveis do Azure para o desenvolvimento do Xamarin Android"
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
ms.openlocfilehash: 38710660d9328fe3c068efca972f76aa8b6e049b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinandroid-app"></a><span data-ttu-id="0ac45-103">Criar um Aplicativo Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="0ac45-103">Create a Xamarin.Android App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="0ac45-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="0ac45-104">Overview</span></span>
<span data-ttu-id="0ac45-105">Este tutorial mostra como tooadd um back-end baseado em nuvem tooa xamarin aplicativo de serviço.</span><span class="sxs-lookup"><span data-stu-id="0ac45-105">This tutorial shows you how tooadd a cloud-based backend service tooa Xamarin.Android app.</span></span> <span data-ttu-id="0ac45-106">Para saber mais, confira [O que são Aplicativos Móveis](app-service-mobile-value-prop.md).</span><span class="sxs-lookup"><span data-stu-id="0ac45-106">For more information, see [What are Mobile Apps](app-service-mobile-value-prop.md).</span></span>

<span data-ttu-id="0ac45-107">É uma captura de tela do aplicativo hello concluída abaixo:</span><span class="sxs-lookup"><span data-stu-id="0ac45-107">A screenshot from hello completed app is below:</span></span>

![][0]

<span data-ttu-id="0ac45-108">A conclusão deste tutorial é um pré-requisito para todos os outros tutoriais de Aplicativos Móveis para aplicativos Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="0ac45-108">Completing this tutorial is a prerequisite for all other Mobile Apps tutorials for Xamarin.Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0ac45-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0ac45-109">Prerequisites</span></span>
<span data-ttu-id="0ac45-110">toocomplete neste tutorial, você precisa Olá pré-requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="0ac45-110">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="0ac45-111">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="0ac45-111">An active Azure account.</span></span> <span data-ttu-id="0ac45-112">Se você não tiver uma conta, inscreva-se para um avaliação do Azure e começar a aplicativos móveis livre de too10.</span><span class="sxs-lookup"><span data-stu-id="0ac45-112">If you don't have an account, sign up for an Azure trial and get up too10 free Mobile Apps.</span></span> <span data-ttu-id="0ac45-113">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0ac45-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="0ac45-114">Visual Studio com Xamarin.</span><span class="sxs-lookup"><span data-stu-id="0ac45-114">Visual Studio with Xamarin.</span></span> <span data-ttu-id="0ac45-115">Veja [Setup and Install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) (Configuração e instalação para Visual Studio e Xamarin).</span><span class="sxs-lookup"><span data-stu-id="0ac45-115">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) for instructions.</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="0ac45-116">Criar um back-end de aplicativo móvel do Azure</span><span class="sxs-lookup"><span data-stu-id="0ac45-116">Create an Azure Mobile App backend</span></span>
<span data-ttu-id="0ac45-117">Siga essas etapas toocreate um back-end do aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="0ac45-117">Follow these steps toocreate a Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="0ac45-118">Você acabou de provisionar um back-end do aplicativo móvel do Azure que pode ser usado pelos aplicativos móveis clientes.</span><span class="sxs-lookup"><span data-stu-id="0ac45-118">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="0ac45-119">Em seguida, baixar um projeto do servidor para um simples "lista de tarefas" back-end e publicá-lo tooAzure.</span><span class="sxs-lookup"><span data-stu-id="0ac45-119">Next, download a server project for a simple "todo list" backend and publish it tooAzure.</span></span>

## <a name="configure-hello-server-project"></a><span data-ttu-id="0ac45-120">Configurar o projeto do servidor de saudação</span><span class="sxs-lookup"><span data-stu-id="0ac45-120">Configure hello server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinandroid-app"></a><span data-ttu-id="0ac45-121">Baixe e execute o aplicativo de xamarin Olá</span><span class="sxs-lookup"><span data-stu-id="0ac45-121">Download and run hello Xamarin.Android app</span></span>
1. <span data-ttu-id="0ac45-122">Em **baixar e executar o projeto xamarin**, clique em Olá **baixar** botão.</span><span class="sxs-lookup"><span data-stu-id="0ac45-122">Under **Download and run your Xamarin.Android project**, click hello **Download** button.</span></span>

      <span data-ttu-id="0ac45-123">Salvar o computador local do hello projeto compactado arquivo tooyour e anote onde você salvá-lo.</span><span class="sxs-lookup"><span data-stu-id="0ac45-123">Save hello compressed project file tooyour local computer, and make a note of where you save it.</span></span>
2. <span data-ttu-id="0ac45-124">Olá pressione **F5** chave projeto de saudação toobuild e iniciar o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="0ac45-124">Press hello **F5** key toobuild hello project and start hello app.</span></span>
3. <span data-ttu-id="0ac45-125">No aplicativo hello, digite o texto significativo, como *tutorial completo Olá* e, em seguida, clique em Olá **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="0ac45-125">In hello app, type meaningful text, such as *Complete hello tutorial* and then click hello **Add** button.</span></span>

    ![][10]

    <span data-ttu-id="0ac45-126">Dados de solicitação de saudação são inseridos na tabela de TodoItem de saudação.</span><span class="sxs-lookup"><span data-stu-id="0ac45-126">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="0ac45-127">Itens armazenados na tabela de saudação são retornados pelo back-end de aplicativo móvel hello e os dados aparecem na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="0ac45-127">Items stored in hello table are returned by hello mobile app backend, and the data appears in hello list.</span></span>

   > [!NOTE]
   > <span data-ttu-id="0ac45-128">Você pode examinar o código Olá que acessa o tooquery de back-end do aplicativo móvel e inserir dados, que são encontrados no hello arquivo ToDoActivity.cs c#.</span><span class="sxs-lookup"><span data-stu-id="0ac45-128">You can review hello code that accesses your mobile app backend tooquery and insert data, which is found in hello ToDoActivity.cs C# file.</span></span>
   >
   >

## <a name="next-steps"></a><span data-ttu-id="0ac45-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0ac45-129">Next steps</span></span>
* [<span data-ttu-id="0ac45-130">Adicionar aplicativo de tooyour sincronização Offline</span><span class="sxs-lookup"><span data-stu-id="0ac45-130">Add Offline Sync tooyour app</span></span>](app-service-mobile-xamarin-android-get-started-offline-data.md)
* [<span data-ttu-id="0ac45-131">Adicionar autenticação tooyour aplicativo</span><span class="sxs-lookup"><span data-stu-id="0ac45-131">Add authentication tooyour app </span></span>](app-service-mobile-xamarin-android-get-started-users.md)
* [<span data-ttu-id="0ac45-132">Adicionar aplicativo de xamarin de tooyour de notificações por push</span><span class="sxs-lookup"><span data-stu-id="0ac45-132">Add push notifications tooyour Xamarin.Android app</span></span>](app-service-mobile-xamarin-android-get-started-push.md)
* [<span data-ttu-id="0ac45-133">Como toouse Olá gerenciada do cliente para aplicativos móveis do Azure</span><span class="sxs-lookup"><span data-stu-id="0ac45-133">How toouse hello managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Images. -->
[0]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-completed-android.png
[6]: ./media/app-service-mobile-xamarin-android-get-started/mobile-portal-quickstart-xamarin.png
[8]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-vs.png
[9]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-xs.png
[10]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-startup-android.png

<!-- URLs. -->
[Azure Portal]: https://azure.portal.com/
[Visual Studio]: https://go.microsoft.com/fwLink/p/?LinkID=534203
