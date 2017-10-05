---
title: "Criar uma UWP (Plataforma Universal do Windows) que usa Aplicativos Móveis | Microsoft Docs"
description: "Siga este tutorial para começar a usar os back-ends de aplicativo móvel do Azure para desenvolvimento de aplicativos UWP (Plataforma Universal do Windows) em C#, Visual Basic ou JavaScript."
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
ms.openlocfilehash: 5408e032670dda7f149c442e08f52b02abe23f05
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-windows-app"></a><span data-ttu-id="5447c-103">Criar um aplicativo do Windows</span><span class="sxs-lookup"><span data-stu-id="5447c-103">Create a Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="5447c-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="5447c-104">Overview</span></span>
<span data-ttu-id="5447c-105">Este tutorial mostra como adicionar um serviço de back-end baseado na nuvem a um aplicativo UWP (Plataforma Universal do Windows).</span><span class="sxs-lookup"><span data-stu-id="5447c-105">This tutorial shows you how to add a cloud-based backend service to a Universal Windows Platform (UWP) app.</span></span> <span data-ttu-id="5447c-106">Para saber mais, confira [O que são Aplicativos Móveis](app-service-mobile-value-prop.md).</span><span class="sxs-lookup"><span data-stu-id="5447c-106">For more information, see [What are Mobile Apps](app-service-mobile-value-prop.md).</span></span> <span data-ttu-id="5447c-107">A seguir, há capturas de tela do aplicativo concluído:</span><span class="sxs-lookup"><span data-stu-id="5447c-107">The following are screen captures from the completed app:</span></span>

![Aplicativo de área de trabalho concluído](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed-desktop.png)   
<span data-ttu-id="5447c-109">em execução em uma área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="5447c-109">Running on a desktop.</span></span>

![Aplicativo de telefone concluído](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)  
<span data-ttu-id="5447c-111">em execução em um telefone</span><span class="sxs-lookup"><span data-stu-id="5447c-111">Running on a phone</span></span>

<span data-ttu-id="5447c-112">A conclusão desse tutorial é um pré-requisito para todos os outros tutoriais de Aplicativos Móveis para aplicativos UWP.</span><span class="sxs-lookup"><span data-stu-id="5447c-112">Completing this tutorial is a prerequisite for all other Mobile App tutorials for UWP apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5447c-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5447c-113">Prerequisites</span></span>
<span data-ttu-id="5447c-114">Para concluir este tutorial, você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="5447c-114">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="5447c-115">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="5447c-115">An active Azure account.</span></span> <span data-ttu-id="5447c-116">Se você não tem uma conta, você pode se inscrever para uma avaliação do Azure e obter até 10 aplicativos móveis gratuitos que você pode continuar a usar mesmo após o fim do seu período de avaliação.</span><span class="sxs-lookup"><span data-stu-id="5447c-116">If you don't have an account, you can sign up for an Azure trial and get up to 10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="5447c-117">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5447c-117">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="5447c-118">[Visual Studio Community 2015] ou uma versão posterior.</span><span class="sxs-lookup"><span data-stu-id="5447c-118">[Visual Studio Community 2015] or a later version.</span></span>

## <a name="create-a-new-azure-mobile-app-backend"></a><span data-ttu-id="5447c-119">Criar um novo back-end de aplicativo móvel do Azure</span><span class="sxs-lookup"><span data-stu-id="5447c-119">Create a new Azure Mobile App backend</span></span>
<span data-ttu-id="5447c-120">Siga estas etapas para criar um novo back-end de aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="5447c-120">Follow these steps to create a new Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="5447c-121">Você acabou de provisionar um back-end do aplicativo móvel do Azure que pode ser usado pelos aplicativos móveis clientes.</span><span class="sxs-lookup"><span data-stu-id="5447c-121">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="5447c-122">Em seguida, você baixará um projeto do servidor para um back-end simples da "lista de tarefas" e o publicará no Azure.</span><span class="sxs-lookup"><span data-stu-id="5447c-122">Next, you will download a server project for a simple "todo list" backend and publish it to Azure.</span></span>

## <a name="configure-the-server-project"></a><span data-ttu-id="5447c-123">Configurar o projeto de servidor</span><span class="sxs-lookup"><span data-stu-id="5447c-123">Configure the server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-client-project"></a><span data-ttu-id="5447c-124">Baixe e execute o projeto do cliente</span><span class="sxs-lookup"><span data-stu-id="5447c-124">Download and run the client project</span></span>
<span data-ttu-id="5447c-125">Quando você tiver configurado o back-end do Aplicativo Móvel, poderá criar um novo aplicativo cliente ou modificar um aplicativo existente para se conectar ao Azure.</span><span class="sxs-lookup"><span data-stu-id="5447c-125">Once you have configured your Mobile App backend, you can either create a new client app or modify an existing app to connect to Azure.</span></span> <span data-ttu-id="5447c-126">Nesta seção, você baixa um projeto de modelo de aplicativo UWP personalizado para se conectar ao back-end do Aplicativo Móvel.</span><span class="sxs-lookup"><span data-stu-id="5447c-126">In this section, you download a UWP app template project that is customized to connect to your Mobile App backend.</span></span>

1. <span data-ttu-id="5447c-127">De volta à folha **Início rápido** do back-end do Aplicativo Móvel, clique em **Criar um novo aplicativo** > **Baixar** e extraia os arquivos de projeto compactados para o computador local.</span><span class="sxs-lookup"><span data-stu-id="5447c-127">Back in the **Quick start** blade for your Mobile App backend, click **Create a new app** > **Download**, then extract the compressed project files to your local computer.</span></span>

    ![Baixar o projeto de início rápido do Windows](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-app-windows-quickstart.png)
2. <span data-ttu-id="5447c-129">(Opcional) Adicione o projeto de aplicativo UWP à mesma solução que o projeto de servidor.</span><span class="sxs-lookup"><span data-stu-id="5447c-129">(Optional) Add the UWP app project to the same solution as the server project.</span></span> <span data-ttu-id="5447c-130">Isso torna mais fácil depurar e testar o aplicativo e o back-end na mesma solução do Visual Studio, se você optar por fazer isso.</span><span class="sxs-lookup"><span data-stu-id="5447c-130">This makes it easier to debug and test both the app and the backend in the same Visual Studio solution, if you choose to do so.</span></span> <span data-ttu-id="5447c-131">Para adicionar um projeto de aplicativo UWP à solução, você deve estar usando o Visual Studio 2015 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="5447c-131">To add a UWP app project to the solution, you must be using Visual Studio 2015 or a later version.</span></span>
3. <span data-ttu-id="5447c-132">Com o aplicativo UWP como o projeto de inicialização, pressione a tecla F5 para implantar e executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5447c-132">With the UWP app as the startup project, press the F5 key to deploy and run the app.</span></span>
4. <span data-ttu-id="5447c-133">No aplicativo, digite um texto significativo, como *Concluir o tutorial*, na caixa de texto **Inserir um TodoItem** e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="5447c-133">In the app, type meaningful text, such as *Complete the tutorial*, in the **Insert a TodoItem** text box, and then click **Save**.</span></span>

    ![Área de trabalho completa do início rápido do Windows](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-startup.png)

    <span data-ttu-id="5447c-135">Isso envia uma solicitação POST para o novo back-end de aplicativo móvel hospedado no Azure.</span><span class="sxs-lookup"><span data-stu-id="5447c-135">This sends a POST request to the new mobile app backend that's hosted in Azure.</span></span>
5. <span data-ttu-id="5447c-136">(Opcional) Interrompa o aplicativo e reinicie-o em outro dispositivo ou emulador móvel.</span><span class="sxs-lookup"><span data-stu-id="5447c-136">(Optional) Stop the app and restart it on a different device or mobile emulator.</span></span>

    ![Telefone completo do início rápido do Windows](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)

    <span data-ttu-id="5447c-138">Observe que os dados salvos da etapa anterior são carregados do Azure depois que o aplicativo UWP é iniciado.</span><span class="sxs-lookup"><span data-stu-id="5447c-138">Notice that data saved from the previous step is loaded from Azure after the UWP app starts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5447c-139">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5447c-139">Next steps</span></span>
* [<span data-ttu-id="5447c-140">Adicionar autenticação ao seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="5447c-140">Add authentication to your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  <span data-ttu-id="5447c-141">Saiba como autenticar usuários de seu aplicativo com um provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="5447c-141">Learn how to authenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="5447c-142">Adicionar notificações por push ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="5447c-142">Add push notifications to your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  <span data-ttu-id="5447c-143">Saiba como adicionar suporte a notificações por push ao aplicativo e configurar o back-end do Aplicativo Móvel para usar os Hubs de Notificação do Azure para enviar notificações por push.</span><span class="sxs-lookup"><span data-stu-id="5447c-143">Learn how to add push notifications support to your app and configure your Mobile App backend to use Azure Notification Hubs to send push notifications.</span></span>
* [<span data-ttu-id="5447c-144">Habilitar sincronização offline para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="5447c-144">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="5447c-145">Saiba como adicionar suporte offline ao seu aplicativo usando um back-end de Aplicativo Móvel.</span><span class="sxs-lookup"><span data-stu-id="5447c-145">Learn how to add offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="5447c-146">Sincronização offline permite que os usuários finais interajam com um aplicativo móvel, &mdash;exibindo, adicionando ou modificando dados&mdash;, mesmo quando não há conexão de rede.</span><span class="sxs-lookup"><span data-stu-id="5447c-146">Offline sync allows end-users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->
<!-- Images. -->
<!-- URLs. -->
[Mobile App SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[Azure portal]: https://portal.azure.com/
<span data-ttu-id="5447c-147">[Visual Studio Community 2015]: https://go.microsoft.com/fwLink/p/?LinkID=534203</span><span class="sxs-lookup"><span data-stu-id="5447c-147">[Visual Studio Community 2015]: https://go.microsoft.com/fwLink/p/?LinkID=534203</span></span>
