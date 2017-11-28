---
title: "aaaCreate um Windows UWP (plataforma Universal) que usa em aplicativos móveis | Microsoft Docs"
description: "Siga este tutorial tooget iniciado com o uso de back-ends dos aplicativos móveis do Azure para desenvolvimento de aplicativos do Windows UWP (plataforma Universal) no c#, Visual Basic ou JavaScript."
services: app-service\mobile
documentationcenter: windows
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 47124296-2908-4d92-85e0-05c4aa6db916
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: d0f57bca5a8195b8b0461b8f7a0d8516371d56a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-app"></a><span data-ttu-id="175fa-103">Criar um aplicativo do Windows</span><span class="sxs-lookup"><span data-stu-id="175fa-103">Create a Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="175fa-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="175fa-104">Overview</span></span>
<span data-ttu-id="175fa-105">Este tutorial mostra como tooadd um back-end baseado em nuvem tooa Windows UWP (plataforma Universal) aplicativo de serviço.</span><span class="sxs-lookup"><span data-stu-id="175fa-105">This tutorial shows you how tooadd a cloud-based backend service tooa Universal Windows Platform (UWP) app.</span></span> <span data-ttu-id="175fa-106">Para saber mais, confira [O que são Aplicativos Móveis](app-service-mobile-value-prop.md).</span><span class="sxs-lookup"><span data-stu-id="175fa-106">For more information, see [What are Mobile Apps](app-service-mobile-value-prop.md).</span></span> <span data-ttu-id="175fa-107">Olá seguem capturas de tela do aplicativo hello concluída:</span><span class="sxs-lookup"><span data-stu-id="175fa-107">hello following are screen captures from hello completed app:</span></span>

![Aplicativo de área de trabalho concluído](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed-desktop.png)   
<span data-ttu-id="175fa-109">em execução em uma área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="175fa-109">Running on a desktop.</span></span>

![Aplicativo de telefone concluído](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)  
<span data-ttu-id="175fa-111">em execução em um telefone</span><span class="sxs-lookup"><span data-stu-id="175fa-111">Running on a phone</span></span>

<span data-ttu-id="175fa-112">A conclusão desse tutorial é um pré-requisito para todos os outros tutoriais de Aplicativos Móveis para aplicativos UWP.</span><span class="sxs-lookup"><span data-stu-id="175fa-112">Completing this tutorial is a prerequisite for all other Mobile App tutorials for UWP apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="175fa-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="175fa-113">Prerequisites</span></span>
<span data-ttu-id="175fa-114">toocomplete neste tutorial, você precisa Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="175fa-114">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="175fa-115">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="175fa-115">An active Azure account.</span></span> <span data-ttu-id="175fa-116">Se você não tiver uma conta, você pode inscrever-se para uma avaliação do Azure e obter o too10 livre aplicativos móveis que você pode continuar usando até mesmo após o término de sua avaliação.</span><span class="sxs-lookup"><span data-stu-id="175fa-116">If you don't have an account, you can sign up for an Azure trial and get up too10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="175fa-117">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="175fa-117">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="175fa-118">[Visual Studio Community 2015] ou uma versão posterior.</span><span class="sxs-lookup"><span data-stu-id="175fa-118">[Visual Studio Community 2015] or a later version.</span></span>

## <a name="create-a-new-azure-mobile-app-backend"></a><span data-ttu-id="175fa-119">Criar um novo back-end de aplicativo móvel do Azure</span><span class="sxs-lookup"><span data-stu-id="175fa-119">Create a new Azure Mobile App backend</span></span>
<span data-ttu-id="175fa-120">Siga essas etapas toocreate um novo back-end do aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="175fa-120">Follow these steps toocreate a new Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="175fa-121">Você acabou de provisionar um back-end do aplicativo móvel do Azure que pode ser usado pelos aplicativos móveis clientes.</span><span class="sxs-lookup"><span data-stu-id="175fa-121">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="175fa-122">Em seguida, você baixará um projeto do servidor para um simples "lista de tarefas" back-end e publicá-lo tooAzure.</span><span class="sxs-lookup"><span data-stu-id="175fa-122">Next, you will download a server project for a simple "todo list" backend and publish it tooAzure.</span></span>

## <a name="configure-hello-server-project"></a><span data-ttu-id="175fa-123">Configurar o projeto do servidor de saudação</span><span class="sxs-lookup"><span data-stu-id="175fa-123">Configure hello server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-client-project"></a><span data-ttu-id="175fa-124">Baixe e execute o projeto de saudação do cliente</span><span class="sxs-lookup"><span data-stu-id="175fa-124">Download and run hello client project</span></span>
<span data-ttu-id="175fa-125">Quando você tiver configurado seu back-end do aplicativo móvel, você pode criar um novo aplicativo de cliente ou modificar um tooAzure de tooconnect de aplicativo existente.</span><span class="sxs-lookup"><span data-stu-id="175fa-125">Once you have configured your Mobile App backend, you can either create a new client app or modify an existing app tooconnect tooAzure.</span></span> <span data-ttu-id="175fa-126">Nesta seção, você baixar um projeto de modelo de aplicativo UWP que é o back-end de aplicativo móvel de tooyour tooconnect personalizado.</span><span class="sxs-lookup"><span data-stu-id="175fa-126">In this section, you download a UWP app template project that is customized tooconnect tooyour Mobile App backend.</span></span>

1. <span data-ttu-id="175fa-127">Em Olá **início rápido** folha para seu back-end do aplicativo móvel, clique em **criar um novo aplicativo** > **baixar**, extraia os arquivos de projeto Olá compactado tooyour de computador local.</span><span class="sxs-lookup"><span data-stu-id="175fa-127">Back in hello **Quick start** blade for your Mobile App backend, click **Create a new app** > **Download**, then extract hello compressed project files tooyour local computer.</span></span>

    ![Baixar o projeto de início rápido do Windows](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-app-windows-quickstart.png)
2. <span data-ttu-id="175fa-129">(Opcional) Adicionar toohello de projeto de aplicativo UWP Olá mesma solução que o projeto do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="175fa-129">(Optional) Add hello UWP app project toohello same solution as hello server project.</span></span> <span data-ttu-id="175fa-130">Isso facilita toodebug e teste ambos Olá Olá e aplicativos back-end em Olá mesma solução do Visual Studio, se você escolher toodo isso.</span><span class="sxs-lookup"><span data-stu-id="175fa-130">This makes it easier toodebug and test both hello app and hello backend in hello same Visual Studio solution, if you choose toodo so.</span></span> <span data-ttu-id="175fa-131">tooadd uma solução de toohello de projeto de aplicativo UWP, você deve estar usando o Visual Studio 2015 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="175fa-131">tooadd a UWP app project toohello solution, you must be using Visual Studio 2015 or a later version.</span></span>
3. <span data-ttu-id="175fa-132">Com o aplicativo UWP hello como projeto de inicialização hello, pressione Olá F5 chave toodeploy e aplicativo hello execução.</span><span class="sxs-lookup"><span data-stu-id="175fa-132">With hello UWP app as hello startup project, press hello F5 key toodeploy and run hello app.</span></span>
4. <span data-ttu-id="175fa-133">No aplicativo hello, digite o texto significativo, como *tutorial completo Olá*, em Olá **inserir um TodoItem** caixa de texto e clique **salvar**.</span><span class="sxs-lookup"><span data-stu-id="175fa-133">In hello app, type meaningful text, such as *Complete hello tutorial*, in hello **Insert a TodoItem** text box, and then click **Save**.</span></span>

    ![Área de trabalho completa do início rápido do Windows](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-startup.png)

    <span data-ttu-id="175fa-135">Isso envia um POST solicitação toohello novo aplicativo móvel back-end que está hospedado no Azure.</span><span class="sxs-lookup"><span data-stu-id="175fa-135">This sends a POST request toohello new mobile app backend that's hosted in Azure.</span></span>
5. <span data-ttu-id="175fa-136">(Opcional) Interromper um aplicativo hello e reiniciá-lo em outro dispositivo ou emulador móvel.</span><span class="sxs-lookup"><span data-stu-id="175fa-136">(Optional) Stop hello app and restart it on a different device or mobile emulator.</span></span>

    ![Telefone completo do início rápido do Windows](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)

    <span data-ttu-id="175fa-138">Observe que os dados salvos da etapa anterior Olá seja carregados do Azure após o início do aplicativo UWP de saudação.</span><span class="sxs-lookup"><span data-stu-id="175fa-138">Notice that data saved from hello previous step is loaded from Azure after hello UWP app starts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="175fa-139">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="175fa-139">Next steps</span></span>
* [<span data-ttu-id="175fa-140">Adicionar autenticação tooyour aplicativo</span><span class="sxs-lookup"><span data-stu-id="175fa-140">Add authentication tooyour app</span></span>](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  <span data-ttu-id="175fa-141">Saiba como tooauthenticate usuários do seu aplicativo com um provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="175fa-141">Learn how tooauthenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="175fa-142">Adicionar aplicativo de tooyour de notificações por push</span><span class="sxs-lookup"><span data-stu-id="175fa-142">Add push notifications tooyour app</span></span>](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  <span data-ttu-id="175fa-143">Saiba como notificações por push de tooadd dão suporte ao aplicativo tooyour e configurar seu aplicativo móvel back-end toouse Hubs de notificação do Azure toosend as notificações por push.</span><span class="sxs-lookup"><span data-stu-id="175fa-143">Learn how tooadd push notifications support tooyour app and configure your Mobile App backend toouse Azure Notification Hubs toosend push notifications.</span></span>
* [<span data-ttu-id="175fa-144">Habilitar sincronização offline para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="175fa-144">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="175fa-145">Saiba como off-line tooadd dão suporte ao seu aplicativo usar um back-end do aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="175fa-145">Learn how tooadd offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="175fa-146">Sincronização offline permite que os usuários finais toointeract com um aplicativo móvel&mdash;exibindo, adicionando ou modificando dados&mdash;mesmo quando não há nenhuma conexão de rede.</span><span class="sxs-lookup"><span data-stu-id="175fa-146">Offline sync allows end-users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->
<!-- Images. -->
<!-- URLs. -->
[Mobile App SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2015]: https://go.microsoft.com/fwLink/p/?LinkID=534203
