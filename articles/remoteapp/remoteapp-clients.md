---
title: Acessando seus aplicativos em qualquer dispositivo | Microsoft Docs
description: "Saiba quais clientes têm suporte para o Azure RemoteApp e como acessar seus aplicativos."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: fb7bd17d-7aa8-43fd-9278-f96e0e9308e4
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 10a5be6251765b59fac92a33120cedcf8091a677
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="accessing-your-apps-in-azure-remoteapp"></a><span data-ttu-id="fae34-103">Acessando seus aplicativos no Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="fae34-103">Accessing your apps in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="fae34-104">O Azure RemoteApp será descontinuado até 31 de agosto de 2017.</span><span class="sxs-lookup"><span data-stu-id="fae34-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="fae34-105">Leia o [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="fae34-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="fae34-106">Uma das vantagens do RemoteApp do Azure é que você pode acessar os aplicativos de qualquer um dos seus dispositivos.</span><span class="sxs-lookup"><span data-stu-id="fae34-106">One of the beauties of Azure RemoteApp is that you can access apps from any of your devices.</span></span> <span data-ttu-id="fae34-107">Melhor ainda, você pode começar a trabalhar em um dispositivo e transitar sem problemas para um segundo dispositivo e selecioná-lo bem onde parou.</span><span class="sxs-lookup"><span data-stu-id="fae34-107">Even better, you can start working on one device and then seamlessly transition to a second device and pick up right where you left off.</span></span> <span data-ttu-id="fae34-108">Para começar você precisa baixar o cliente apropriado para seu dispositivo e entrar no serviço.</span><span class="sxs-lookup"><span data-stu-id="fae34-108">To get started you need to download the appropriate client for your device and sign in to the service.</span></span>

<span data-ttu-id="fae34-109">Neste tópico, vamos analisar os clientes com suporte atualmente e como baixá-los antes de mostrar como entrar no RemoteApp por meio de cada um dos clientes.</span><span class="sxs-lookup"><span data-stu-id="fae34-109">In this topic, we'll review the clients currently supported and how to download them before I show you how to sign in to RemoteApp from each of the clients.</span></span>

## <a name="supported-clients"></a><span data-ttu-id="fae34-110">Clientes com suporte</span><span class="sxs-lookup"><span data-stu-id="fae34-110">Supported clients</span></span>
<span data-ttu-id="fae34-111">Você pode acessar o RemoteApp usando as etapas a seguir se seu dispositivo estiver executando um dos seguintes sistemas operacionais:</span><span class="sxs-lookup"><span data-stu-id="fae34-111">You can access RemoteApp using the steps below if your device is running one of these operating systems:</span></span>

* <span data-ttu-id="fae34-112">Windows 10</span><span class="sxs-lookup"><span data-stu-id="fae34-112">Windows 10</span></span> 
* <span data-ttu-id="fae34-113">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="fae34-113">Windows 8.1</span></span>
* <span data-ttu-id="fae34-114">Windows 8</span><span class="sxs-lookup"><span data-stu-id="fae34-114">Windows 8</span></span>
* <span data-ttu-id="fae34-115">Windows 7 Service Pack 1</span><span class="sxs-lookup"><span data-stu-id="fae34-115">Windows 7 Service Pack 1</span></span>
* <span data-ttu-id="fae34-116">Windows Phone 8,1</span><span class="sxs-lookup"><span data-stu-id="fae34-116">Windows Phone 8.1</span></span>
* <span data-ttu-id="fae34-117">iOS</span><span class="sxs-lookup"><span data-stu-id="fae34-117">iOS</span></span>
* <span data-ttu-id="fae34-118">Mac OS X</span><span class="sxs-lookup"><span data-stu-id="fae34-118">Mac OS X</span></span>
* <span data-ttu-id="fae34-119">Android</span><span class="sxs-lookup"><span data-stu-id="fae34-119">Android</span></span>

 <span data-ttu-id="fae34-120">E clientes finos?</span><span class="sxs-lookup"><span data-stu-id="fae34-120">What about thin clients?</span></span> <span data-ttu-id="fae34-121">Há suporte para os seguintes clientes finos do Windows Embedded:</span><span class="sxs-lookup"><span data-stu-id="fae34-121">The following Windows Embedded thin clients are supported:</span></span>

* <span data-ttu-id="fae34-122">Windows Embedded Standard 7</span><span class="sxs-lookup"><span data-stu-id="fae34-122">Windows Embedded Standard 7</span></span>
* <span data-ttu-id="fae34-123">Windows Embedded 8 Standard</span><span class="sxs-lookup"><span data-stu-id="fae34-123">Windows Embedded 8 Standard</span></span>
* <span data-ttu-id="fae34-124">Windows Embedded 8.1 Industry Pro</span><span class="sxs-lookup"><span data-stu-id="fae34-124">Windows Embedded 8.1 Industry Pro</span></span>
* <span data-ttu-id="fae34-125">Windows 10 IoT Enterprise</span><span class="sxs-lookup"><span data-stu-id="fae34-125">Windows 10 IoT Enterprise</span></span>

## <a name="downloading-the-client"></a><span data-ttu-id="fae34-126">Baixar o cliente</span><span class="sxs-lookup"><span data-stu-id="fae34-126">Downloading the client</span></span>
<span data-ttu-id="fae34-127">Não importa qual plataforma você esteja usando, o cliente que você precisa que acesse o RemoteApp pode ser encontrado na página [Download do cliente de Área de Trabalho Remota](https://www.remoteapp.windowsazure.com/ClientDownload/AllClients.aspx) .</span><span class="sxs-lookup"><span data-stu-id="fae34-127">No matter what platform you are using, the client you need to access RemoteApp can be found on the [Remote Desktop client download](https://www.remoteapp.windowsazure.com/ClientDownload/AllClients.aspx) page.</span></span>

<span data-ttu-id="fae34-128">Clicar nos links diferentes irá iniciar diretamente baixando o cliente ou enviará você à página de download do cliente na loja de aplicativos para essa plataforma.</span><span class="sxs-lookup"><span data-stu-id="fae34-128">Clicking the different links will either directly start downloading the client or will send you to the client download page in the app store for that platform.</span></span> <span data-ttu-id="fae34-129">Instale o cliente, seguindo as instruções na tela.</span><span class="sxs-lookup"><span data-stu-id="fae34-129">Install the client by following the instructions on the screen.</span></span>

<span data-ttu-id="fae34-130">Depois de ter instalado o cliente no dispositivo e o ter iniciado, vá para a seção correspondente abaixo para saber como entrar no RemoteApp a partir desse cliente.</span><span class="sxs-lookup"><span data-stu-id="fae34-130">Once you have installed the client on your device and launched it, jump to the corresponding section below to learn how to sign in to RemoteApp from that client.</span></span>

## <a name="android"></a><span data-ttu-id="fae34-131">Android</span><span class="sxs-lookup"><span data-stu-id="fae34-131">Android</span></span>
<span data-ttu-id="fae34-132">Depois de instalar o aplicativo de Área de Trabalho Remota da Microsoft a partir do armazenamento do Google Play, você o encontrará em sua lista de aplicativos na **Área de Trabalho Remota**.</span><span class="sxs-lookup"><span data-stu-id="fae34-132">Once you have installed the Microsoft Remote Desktop app from the Google Play store, you can find it in your app list under **Remote Desktop**.</span></span>

1. <span data-ttu-id="fae34-133">Iniciar o aplicativo leva você a um Centro de Conexões vazio, a menos que você já tenha usado o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fae34-133">Launching the app brings you to an empty Connection Center, unless you've already been using the app.</span></span> <span data-ttu-id="fae34-134">Para começar com o Azure RemoteApp, toque no botão para adicionar **""+""** e toque em **Azure RemoteApp**.</span><span class="sxs-lookup"><span data-stu-id="fae34-134">To get started with Azure RemoteApp, tap the add button **""+""** and tap **Azure RemoteApp**.</span></span>    
   
     ![Centro de Conexões Vazio](./media/remoteapp-clients/Android1.png)
2. <span data-ttu-id="fae34-136">Você precisa entrar com seu endereço de email para acessar o serviço.</span><span class="sxs-lookup"><span data-stu-id="fae34-136">You need to sign in with your email address to access the service.</span></span> <span data-ttu-id="fae34-137">Toque em **Introdução**.</span><span class="sxs-lookup"><span data-stu-id="fae34-137">Tap **Get started**.</span></span>
   
    ![Prompt de logon](./media/remoteapp-clients/Android2.png)
3. <span data-ttu-id="fae34-139">Na página seguinte, digite seu **endereço de email** e toque em **Continuar**.</span><span class="sxs-lookup"><span data-stu-id="fae34-139">On the next page, type in your **email address** and tap **Continue**.</span></span> <span data-ttu-id="fae34-140">Isso inicia o processo de entrada usando o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="fae34-140">This begins the sign-in process using Azure Active Directory.</span></span>
   
    ![Primeira página do Active Directory do Azure](./media/remoteapp-clients/Android3.png)
4. <span data-ttu-id="fae34-142">Siga as instruções na tela para entrar com sua conta da Microsoft (antes chamada de “LiveID”) ou a ID da Organização.</span><span class="sxs-lookup"><span data-stu-id="fae34-142">Follow the instructions on the screen to sign in with your Microsoft account (previously called "LiveID") or organization ID.</span></span> <span data-ttu-id="fae34-143">Depois de conectado, pode ser apresentada uma página listando todos os convites que você recebeu.</span><span class="sxs-lookup"><span data-stu-id="fae34-143">Once signed in, you may be presented with a page listing all the invitations you have received.</span></span> <span data-ttu-id="fae34-144">Se estiver, selecione os convites que você confia e toque em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="fae34-144">If you are, select the invitations you trust and tap **Done**.</span></span>    
   
    ![Página de convites](./media/remoteapp-clients/Android4.png)
5. <span data-ttu-id="fae34-146">Após aceitar os convites, a lista de aplicativos que você terá acesso será baixada no dispositivo e disponibilizada no Centro de Conexões.</span><span class="sxs-lookup"><span data-stu-id="fae34-146">After accepting your invitations, the list of apps you have access to will be downloaded to your device and made available in the Connection Center.</span></span> <span data-ttu-id="fae34-147">Toque em um dos aplicativos para começar a usá-lo.</span><span class="sxs-lookup"><span data-stu-id="fae34-147">Tap one of the apps to start using it.</span></span>
   
    ![Centro de Conexões com um feed](./media/remoteapp-clients/Android5.png)
6. <span data-ttu-id="fae34-149">Se você ainda não tiver um convite, pode experimentar o serviço.</span><span class="sxs-lookup"><span data-stu-id="fae34-149">If you do not have an invitation yet, you can still try out the service.</span></span> <span data-ttu-id="fae34-150">Para fazer isso, toque em **Ir para a avaliação gratuita** quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="fae34-150">To do so, tap **Go to free trial** when prompted.</span></span>
   
    ![Prompt do feed de demonstração](./media/remoteapp-clients/Android6.png)
7. <span data-ttu-id="fae34-152">Isso lhe dará acesso a um conjunto básico de aplicativos para começar com o RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="fae34-152">This will give you access to a basic set of apps to get you started with RemoteApp.</span></span>
   
    ![Feed de demonstração do Azure RemoteApp](./media/remoteapp-clients/Android7.png)

## <a name="ios"></a><span data-ttu-id="fae34-154">iOS</span><span class="sxs-lookup"><span data-stu-id="fae34-154">iOS</span></span>
<span data-ttu-id="fae34-155">Depois de instalar o aplicativo de Área de Trabalho Remota da Microsoft a partir do armazenamento do Aplicativo, você o encontrará em sua lista de aplicativos na **Cliente da Área de Trabalho Remota**.</span><span class="sxs-lookup"><span data-stu-id="fae34-155">Once you have installed the Microsoft Remote Desktop app from the App store, you can find it in your app list under **RD Client**.</span></span>

1. <span data-ttu-id="fae34-156">Iniciar o aplicativo leva você a um Centro de Conexões vazio, a menos que você já tenha usado o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fae34-156">Launching the app brings you to an empty Connection Center, unless you've already been using the app.</span></span> <span data-ttu-id="fae34-157">Para começar com o Azure RemoteApp, toque no botão Adicionar **"" +""** e toque em **Adicionar Azure RemoteApp**.</span><span class="sxs-lookup"><span data-stu-id="fae34-157">To get started with Azure RemoteApp, tap the add button **""+""** and tap **Add Azure RemoteApp**.</span></span>
   
    ![Centro de Conexões Vazio](./media/remoteapp-clients/IOS1.png)
2. <span data-ttu-id="fae34-159">Você precisa entrar com seu endereço de email para acessar o serviço e para iniciar esse processo, digite seu **endereço de email** e toque em **Continuar**.</span><span class="sxs-lookup"><span data-stu-id="fae34-159">You need to sign in with your email address to access the service, to start that process, type in your **email address** and tap **Continue**.</span></span>
   
    ![Prompt de logon](./media/remoteapp-clients/picture1.png)
3. <span data-ttu-id="fae34-161">Siga as instruções na tela para entrar com sua conta da Microsoft (LiveID) ou a ID da Organização.</span><span class="sxs-lookup"><span data-stu-id="fae34-161">Follow the instructions on the screen to sign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="fae34-162">Depois de conectado, pode ser apresentada uma página listando todos os convites que você recebeu.</span><span class="sxs-lookup"><span data-stu-id="fae34-162">Once signed in, you may be presented with a page listing all the invitations you have received.</span></span> <span data-ttu-id="fae34-163">Se estiver, selecione os convites que você confia e toque em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="fae34-163">If you are, select the invitations you trust and tap **Done**.</span></span>
   
    ![Página de convites](./media/remoteapp-clients/IOS3.png)
4. <span data-ttu-id="fae34-165">Após aceitar os convites, a lista de aplicativos que você terá acesso será baixada no dispositivo e disponibilizada no Centro de Conexões.</span><span class="sxs-lookup"><span data-stu-id="fae34-165">After accepting your invitations, the list of apps you have access to will be downloaded to your device and made available in the Connection Center.</span></span> <span data-ttu-id="fae34-166">Toque em um dos aplicativos para iniciá-lo e começar a usá-lo.</span><span class="sxs-lookup"><span data-stu-id="fae34-166">Tap one of the apps to launch it and start using it.</span></span>
   
    ![Centro de Conexões com um feed](./media/remoteapp-clients/IOS4.png)
5. <span data-ttu-id="fae34-168">Se você ainda não tiver um convite, pode experimentar o serviço.</span><span class="sxs-lookup"><span data-stu-id="fae34-168">If you do not have an invitation yet, you can still try out the service.</span></span> <span data-ttu-id="fae34-169">Para fazer isso, toque em **Ir para a avaliação gratuita** quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="fae34-169">To do so, tap **Go to free trial** when prompted.</span></span>
   
    ![Prompt do feed de demonstração](./media/remoteapp-clients/IOS5.png)
6. <span data-ttu-id="fae34-171">Isso lhe dará acesso a um conjunto básico de aplicativos para começar com o RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="fae34-171">This will give you access to a basic set of apps to get you started with RemoteApp.</span></span>
   
    ![Feed de demonstração do Azure RemoteApp](./media/remoteapp-clients/IOS6.png)

## <a name="mac-os-x"></a><span data-ttu-id="fae34-173">Mac OS X</span><span class="sxs-lookup"><span data-stu-id="fae34-173">Mac OS X</span></span>
<span data-ttu-id="fae34-174">Depois de instalar o aplicativo de Área de Trabalho Remota da Microsoft a partir do armazenamento do Aplicativo, você o encontrará em sua lista de aplicativos na **Área de Trabalho Remota da Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="fae34-174">Once you have installed the Microsoft Remote Desktop app from the App store, you can find it in your app list under **Microsoft Remote Desktop**.</span></span>

1. <span data-ttu-id="fae34-175">Iniciar o aplicativo leva você a um Centro de Conexões vazio, a menos que você já tenha usado o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fae34-175">Launching the app brings you to an empty Connection Center, unless you've already been using the app.</span></span> <span data-ttu-id="fae34-176">Para começar com o Azure RemoteApp, clique no botão **Azure RemoteApp** .</span><span class="sxs-lookup"><span data-stu-id="fae34-176">To get started with Azure RemoteApp, click the **Azure RemoteApp** button.</span></span>
   
    ![Centro de Conexões Vazio](./media/remoteapp-clients/Mac1.png)
2. <span data-ttu-id="fae34-178">Você precisa entrar com seu endereço de email para acessar o serviço e para iniciar esse processo, toque em **Introdução**.</span><span class="sxs-lookup"><span data-stu-id="fae34-178">You need to sign in with your email address to access the service, to start that process, tap **Get Started**.</span></span>
   
    ![Prompt de logon](./media/remoteapp-clients/Mac2.png)
3. <span data-ttu-id="fae34-180">Na página seguinte, digite seu **endereço de email** e toque em **Continuar**.</span><span class="sxs-lookup"><span data-stu-id="fae34-180">On the next page, type in your **email address** and tap **Continue**.</span></span> <span data-ttu-id="fae34-181">Isso inicia o processo de entrada usando o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="fae34-181">This begins the sign in process using Azure Active Directory.</span></span>
   
    ![Primeira página do Active Directory do Azure](./media/remoteapp-clients/picture2.png)
4. <span data-ttu-id="fae34-183">Siga as instruções na tela para entrar com sua conta da Microsoft (LiveID) ou a ID da Organização.</span><span class="sxs-lookup"><span data-stu-id="fae34-183">Follow the instructions on the screen to sign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="fae34-184">Depois de conectado, pode ser apresentada uma página listando todos os convites que você recebeu.</span><span class="sxs-lookup"><span data-stu-id="fae34-184">Once signed in, you may be presented with a page listing all the invitations you have received.</span></span> <span data-ttu-id="fae34-185">Se estiver, selecione os convites que você confia e feche a caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="fae34-185">If you are, select the invitations you trust and close the dialog.</span></span>
   
    ![Página de convites](./media/remoteapp-clients/Mac4.png)
5. <span data-ttu-id="fae34-187">Após aceitar os convites, a lista de aplicativos que você terá acesso será baixada no dispositivo e disponibilizada no Centro de Conexões.</span><span class="sxs-lookup"><span data-stu-id="fae34-187">After accepting your invitations, the list of apps you have access to will be downloaded to your device and made available in the Connection Center.</span></span> <span data-ttu-id="fae34-188">Toque duas vezes em um dos aplicativos para iniciá-lo e começar a usá-lo.</span><span class="sxs-lookup"><span data-stu-id="fae34-188">Double-click one of the apps to launch it and start using it.</span></span>
   
    ![Centro de Conexões com um feed](./media/remoteapp-clients/Mac5.png)
6. <span data-ttu-id="fae34-190">Se você ainda não tiver um convite, pode experimentar o serviço.</span><span class="sxs-lookup"><span data-stu-id="fae34-190">If you do not have an invitation yet, you can still try out the service.</span></span> <span data-ttu-id="fae34-191">Para fazer isso, clique em **Ir para a avaliação gratuita** quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="fae34-191">To do so, click **Go to free trial** when prompted.</span></span>
   
    ![Prompt do feed de demonstração](./media/remoteapp-clients/Mac6.png)
7. <span data-ttu-id="fae34-193">Isso lhe dará acesso a um conjunto básico de aplicativos para começar com o RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="fae34-193">This will give you access to a basic set of apps to get you started with RemoteApp.</span></span>
   
    ![Feed de demonstração do Azure RemoteApp](./media/remoteapp-clients/Mac7.png)

## <a name="windows-all-supported-versions-except-windows-phone"></a><span data-ttu-id="fae34-195">Windows (Todas as versões com suporte exceto o Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="fae34-195">Windows (All supported versions except Windows Phone)</span></span>
<span data-ttu-id="fae34-196">O cliente será iniciado automaticamente após concluir a instalação, no entanto, quando você precisar acessá-lo novamente mais tarde, ele poderá ser encontrado na lista de aplicativos com o nome **Azure RemoteApp**.</span><span class="sxs-lookup"><span data-stu-id="fae34-196">The client launches automatically after it finishes installing, however when you need to access it again later it can be found in your app list under the name **Azure RemoteApp**.</span></span>

1. <span data-ttu-id="fae34-197">Após iniciar o cliente, a primeira página que você vê apresenta o Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="fae34-197">Ater launching the client, the first page you see welcomes you to Azure RemoteApp.</span></span> <span data-ttu-id="fae34-198">Para continuar, clique em **Introdução**.</span><span class="sxs-lookup"><span data-stu-id="fae34-198">To proceed, click on **Get Started**.</span></span>
   
    ![Página de boas-vindas do cliente Azure RemoteApp](./media/remoteapp-clients/Windows1.png)
2. <span data-ttu-id="fae34-200">A próxima página inicia o processo de entrada do Azure RemoteApp usando o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="fae34-200">The next page starts the sign in process for Azure RemoteApp using Azure Active Directory.</span></span> <span data-ttu-id="fae34-201">Esse processo deve parecer familiar se você já usou os serviços da Microsoft no passado.</span><span class="sxs-lookup"><span data-stu-id="fae34-201">This process should look familiar if you have used Microsoft services in the past.</span></span> <span data-ttu-id="fae34-202">Comece digitando seu **endereço de email** e clique em **Continuar**.</span><span class="sxs-lookup"><span data-stu-id="fae34-202">Start by typing your **email address** and click **Continue**.</span></span>
   
    ![Primeiro prompt do Active Directory do Azure](./media/remoteapp-clients/Windows2.png)
3. <span data-ttu-id="fae34-204">Siga as instruções na tela para entrar com sua conta da Microsoft (LiveID) ou a ID da Organização.</span><span class="sxs-lookup"><span data-stu-id="fae34-204">Follow the instructions on the screen to sign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="fae34-205">Depois de conectado, pode ser apresentada uma página listando todos os convites que você recebeu.</span><span class="sxs-lookup"><span data-stu-id="fae34-205">Once signed in, you may be presented with a page listing all the invitations you have received.</span></span> <span data-ttu-id="fae34-206">Se estiver, selecione os convites que você confia e clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="fae34-206">If you are, select the invitations you trust and click **Done**.</span></span>
   
    ![Página de convites do cliente Azure RemoteApp](./media/remoteapp-clients/Windows3.png)
4. <span data-ttu-id="fae34-208">Após aceitar os convites, a lista de aplicativos que você terá acesso será baixada no dispositivo e disponibilizada no Centro de Conexões.</span><span class="sxs-lookup"><span data-stu-id="fae34-208">After accepting your invitations, the list of apps you have access to will be downloaded to your device and made available in the Connection Center.</span></span> <span data-ttu-id="fae34-209">Toque duas vezes em um dos aplicativos para iniciá-lo e começar a usá-lo.</span><span class="sxs-lookup"><span data-stu-id="fae34-209">Double-click one of the apps to launch it and start using it.</span></span>
   
    ![Centro de Conexões do cliente do Azure RemoteApp](./media/remoteapp-clients/Windows4.png)
5. <span data-ttu-id="fae34-211">Não se preocupe se ninguém enviou um convite ainda, nós ajudamos você!</span><span class="sxs-lookup"><span data-stu-id="fae34-211">If no one has sent you an invitation yet, don't worry we've got you covered!</span></span> <span data-ttu-id="fae34-212">Você ainda terá acesso a uma coleção de demonstração para testar o serviço.</span><span class="sxs-lookup"><span data-stu-id="fae34-212">You'll still have access to a demo collection so you can test out the service.</span></span>
   
    ![Feed de demonstração do Azure RemoteApp](./media/remoteapp-clients/Windows5.png)

## <a name="windows-phone-81"></a><span data-ttu-id="fae34-214">Windows Phone 8,1</span><span class="sxs-lookup"><span data-stu-id="fae34-214">Windows Phone 8.1</span></span>
<span data-ttu-id="fae34-215">Depois de instalar o aplicativo de Área de Trabalho Remota da Microsoft a partir do armazenamento do Windows Phone 8.1, você o encontrará em sua lista de aplicativos na **Área de Trabalho Remota**.</span><span class="sxs-lookup"><span data-stu-id="fae34-215">Once you have installed the Microsoft Remote Desktop app from the Windows Phone 8.1 store, you can find it in your app list under **Remote Desktop**.</span></span>

1. <span data-ttu-id="fae34-216">Iniciar o aplicativo leva você a um Centro de Conexões vazio, a menos que você já tenha usado o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fae34-216">Launching the app brings you directly to an empty Connection Center, unless you've already been using the app.</span></span> <span data-ttu-id="fae34-217">Para começar com o Azure RemoteApp, toque no botão Adicionar **"" +""** na parte inferior da tela.</span><span class="sxs-lookup"><span data-stu-id="fae34-217">To get started with Azure RemoteApp, tap the add button **""+""** at the bottom of the screen.</span></span>
   
    ![Centro de Conexões Vazio](./media/remoteapp-clients/WinPhone1.png)
2. <span data-ttu-id="fae34-219">Em seguida, toque em **Azure RemoteApp**.</span><span class="sxs-lookup"><span data-stu-id="fae34-219">Next, tap on **Azure RemoteApp**.</span></span>
   
    ![Adicionar página de itens](./media/remoteapp-clients/WinPhone2.png)
3. <span data-ttu-id="fae34-221">Você precisa entrar com seu endereço de email para acessar o serviço e para iniciar esse processo, toque em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="fae34-221">You need to sign in with your email address to access the service, to start that process, tap **connect**.</span></span>
   
    ![Prompt de logon](./media/remoteapp-clients/WinPhone3.png)
4. <span data-ttu-id="fae34-223">Na página seguinte, digite seu **endereço de email** e toque em **Continuar**.</span><span class="sxs-lookup"><span data-stu-id="fae34-223">On the next page, type in your **email address** and tap **Continue**.</span></span> <span data-ttu-id="fae34-224">Isso inicia o processo de entrada usando o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="fae34-224">This begins the sign in process using Azure Active Directory.</span></span>
   
    ![Primeira página do Active Directory do Azure](./media/remoteapp-clients/WinPhone4.png)
5. <span data-ttu-id="fae34-226">Siga as instruções na tela para entrar com sua conta da Microsoft (LiveID) ou a ID da Organização.</span><span class="sxs-lookup"><span data-stu-id="fae34-226">Follow the instructions on the screen to sign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="fae34-227">Depois de conectado, pode ser apresentada uma página listando todos os convites que você recebeu.</span><span class="sxs-lookup"><span data-stu-id="fae34-227">Once signed in, you may be presented with a page listing all the invitations you have received.</span></span> <span data-ttu-id="fae34-228">Se estiver, selecione os convites que você confia e toque em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="fae34-228">If you are, select the invitations you trust and tap **save**.</span></span>
   
    ![Página de convites](./media/remoteapp-clients/WinPhone5.png)
6. <span data-ttu-id="fae34-230">Após aceitar os convites, a lista de aplicativos que você terá acesso será baixada no dispositivo e disponibilizada no Centro de Conexões.</span><span class="sxs-lookup"><span data-stu-id="fae34-230">After accepting your invitations, the list of apps you have access to will be downloaded to your device and made available in the Connection Center.</span></span> <span data-ttu-id="fae34-231">Toque em um dos aplicativos para iniciá-lo e começar a usá-lo.</span><span class="sxs-lookup"><span data-stu-id="fae34-231">Tap one of the apps to launch it and start using it.</span></span>
   
    ![Centro de Conexões com um feed](./media/remoteapp-clients/WinPhone6.png)
7. <span data-ttu-id="fae34-233">Se você ainda não tiver um convite, pode experimentar o serviço.</span><span class="sxs-lookup"><span data-stu-id="fae34-233">If you do not have an invitation yet, you can still try out the service.</span></span> <span data-ttu-id="fae34-234">Para fazer isso, toque **sim** quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="fae34-234">To do so, tap **yes** when prompted.</span></span>
   
    ![Prompt do feed de demonstração](./media/remoteapp-clients/WinPhone7.png)
8. <span data-ttu-id="fae34-236">Isso lhe dará acesso a um conjunto básico de aplicativos para começar com o RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="fae34-236">This will give you access to a basic set of apps to get you started with RemoteApp.</span></span>
   
    ![Feed de demonstração do Azure RemoteApp](./media/remoteapp-clients/WinPhone8.png)

