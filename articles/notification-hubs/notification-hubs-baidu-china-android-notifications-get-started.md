---
title: "aaaGet iniciado com Hubs de notificação do Azure usando Baidu | Microsoft Docs"
description: "Neste tutorial, você aprenderá como dispositivos toouse Hubs de notificação do Azure toopush notificações tooAndroid usando Baidu."
services: notification-hubs
documentationcenter: android
author: ysxu
manager: erikre
editor: 
ms.assetid: 23bde1ea-f978-43b2-9eeb-bfd7b9edc4c1
ms.service: notification-hubs
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: mobile-baidu
ms.workload: mobile
ms.date: 08/19/2016
ms.author: yuaxu
ms.openlocfilehash: 2767fdd3bb04674e7a531634237cc05cd8c21cb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-using-baidu"></a><span data-ttu-id="96bd3-103">Introdução aos Hubs de Notificação usando o Baidu</span><span class="sxs-lookup"><span data-stu-id="96bd3-103">Get started with Notification Hubs using Baidu</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="96bd3-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="96bd3-104">Overview</span></span>
<span data-ttu-id="96bd3-105">Push de nuvem do Baidu é um serviço de nuvem chinês que você pode usar dispositivos de toomobile de notificações de push toosend.</span><span class="sxs-lookup"><span data-stu-id="96bd3-105">Baidu cloud push is a Chinese cloud service that you can use toosend push notifications toomobile devices.</span></span> <span data-ttu-id="96bd3-106">Esse serviço é útil na China, onde entregar notificações de push tooAndroid é complexo devido à presença de saudação de lojas de aplicativos diferentes e enviar por push de serviços, além disso toohello disponibilidade de dispositivos Android que não são normalmente conectado tooGCM (Google Nuvem de mensagens).</span><span class="sxs-lookup"><span data-stu-id="96bd3-106">This service is useful in China, where delivering push notifications tooAndroid is complex because of hello presence of different app stores and push services, in addition toohello availability of Android devices that are not typically connected tooGCM (Google Cloud Messaging).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="96bd3-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="96bd3-107">Prerequisites</span></span>
<span data-ttu-id="96bd3-108">Este tutorial exige:</span><span class="sxs-lookup"><span data-stu-id="96bd3-108">This tutorial requires:</span></span>

* <span data-ttu-id="96bd3-109">SDK do Android (vamos supor que você use Eclipse), que você pode baixar da saudação <a href="http://go.microsoft.com/fwlink/?LinkId=389797">site Android</a></span><span class="sxs-lookup"><span data-stu-id="96bd3-109">Android SDK (we assume that you use Eclipse), which you can download from hello <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android site</a></span></span>
* <span data-ttu-id="96bd3-110">[SDK para Android de Serviços Móveis]</span><span class="sxs-lookup"><span data-stu-id="96bd3-110">[Mobile Services Android SDK]</span></span>
* <span data-ttu-id="96bd3-111">[Baidu Push Android SDK]</span><span class="sxs-lookup"><span data-stu-id="96bd3-111">[Baidu Push Android SDK]</span></span>

> [!NOTE]
> <span data-ttu-id="96bd3-112">toocomplete neste tutorial, você deve ter uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="96bd3-112">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="96bd3-113">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="96bd3-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="96bd3-114">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-baidu-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="96bd3-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-baidu-get-started%2F).</span></span>
> 
> 

## <a name="create-a-baidu-account"></a><span data-ttu-id="96bd3-115">Criar uma conta de Baidu</span><span class="sxs-lookup"><span data-stu-id="96bd3-115">Create a Baidu account</span></span>
<span data-ttu-id="96bd3-116">toouse Baidu, você deve ter uma conta do Baidu.</span><span class="sxs-lookup"><span data-stu-id="96bd3-116">toouse Baidu, you must have a Baidu account.</span></span> <span data-ttu-id="96bd3-117">Se você já tiver um, faça logon toohello [Baidu portal] e ignorar toohello próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="96bd3-117">If you already have one, log in toohello [Baidu portal] and skip toohello next step.</span></span> <span data-ttu-id="96bd3-118">Caso contrário, consulte Olá seguindo as instruções sobre como toocreate uma conta do Baidu.</span><span class="sxs-lookup"><span data-stu-id="96bd3-118">Otherwise, see hello following instructions on how toocreate a Baidu account.</span></span>  

1. <span data-ttu-id="96bd3-119">Vá toohello [Baidu portal] e clique em Olá**登录**(**Login**) link.</span><span class="sxs-lookup"><span data-stu-id="96bd3-119">Go toohello [Baidu portal] and click hello **登录** (**Login**) link.</span></span> <span data-ttu-id="96bd3-120">Clique em**立即注册**toostart processo de registro de conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="96bd3-120">Click **立即注册** toostart hello account registration process.</span></span>
   
   ![][1]
2. <span data-ttu-id="96bd3-121">Insira os detalhes de saudação necessária — phone/código de verificação, senha e endereço de email — e clique em **inscrição**.</span><span class="sxs-lookup"><span data-stu-id="96bd3-121">Enter hello required details—phone/email address, password, and verification code—and click **Signup**.</span></span>
   
   ![][2]
3. <span data-ttu-id="96bd3-122">Você receberá um endereço de email de toohello de email inserido com um link tooactivate sua conta do Baidu.</span><span class="sxs-lookup"><span data-stu-id="96bd3-122">You will be sent an email toohello email address that you entered with a link tooactivate your Baidu account.</span></span>
   
   ![][3]
4. <span data-ttu-id="96bd3-123">Faça logon na conta de email tooyour, abra o email de ativação do Baidu hello e clique tooactivate de link de ativação de saudação sua conta do Baidu.</span><span class="sxs-lookup"><span data-stu-id="96bd3-123">Log in tooyour email account, open hello Baidu activation mail, and click hello activation link tooactivate your Baidu account.</span></span>
   
   ![][4]

<span data-ttu-id="96bd3-124">Depois que você tiver uma conta de Baidu ativada, faça logon em toohello [Baidu portal].</span><span class="sxs-lookup"><span data-stu-id="96bd3-124">Once you have an activated Baidu account, log in toohello [Baidu portal].</span></span>

## <a name="register-as-a-baidu-developer"></a><span data-ttu-id="96bd3-125">Registrar-se como desenvolvedor Baidu</span><span class="sxs-lookup"><span data-stu-id="96bd3-125">Register as a Baidu developer</span></span>
1. <span data-ttu-id="96bd3-126">Depois de fazer logon em toohello [Baidu portal], clique em**更多 >>** (**mais**).</span><span class="sxs-lookup"><span data-stu-id="96bd3-126">Once you have logged in toohello [Baidu portal], click **更多>>** (**more**).</span></span>
   
      ![][5]
2. <span data-ttu-id="96bd3-127">Role para baixo na Olá**站长与开发者服务 (serviços de desenvolvedor e Webmaster)** seção e clique em**百度开放云平台**(**Baidu abrir plataforma de nuvem**).</span><span class="sxs-lookup"><span data-stu-id="96bd3-127">Scroll down in hello **站长与开发者服务 (Webmaster and Developer Services)** section and click **百度开放云平台** (**Baidu open cloud platform**).</span></span>
   
      ![][6]
3. <span data-ttu-id="96bd3-128">Na próxima página do hello, clique em**开发者服务**(**serviços de desenvolvedor**) no canto superior direito de saudação.</span><span class="sxs-lookup"><span data-stu-id="96bd3-128">On hello next page, click **开发者服务** (**Developer Services**) on hello top-right corner.</span></span>
   
      ![][7]
4. <span data-ttu-id="96bd3-129">Na próxima página do hello, clique em**注册开发者**(**desenvolvedores registrados**) no menu de saudação no canto superior direito de saudação.</span><span class="sxs-lookup"><span data-stu-id="96bd3-129">On hello next page, click **注册开发者** (**Registered Developers**) from hello menu on hello top-right corner.</span></span>
   
      ![][8]
5. <span data-ttu-id="96bd3-130">Insira seu nome, uma descrição e um número de telefone celular para receber uma mensagem de texto de verificação e, em seguida, clique em **送验证码** (**Enviar Código de Verificação**).</span><span class="sxs-lookup"><span data-stu-id="96bd3-130">Enter your name, a description, and a mobile phone number for receiving a verification text message, and then click **送验证码** (**Send Verification Code**).</span></span> <span data-ttu-id="96bd3-131">Para números de telefone internacional, é necessário código de país Olá tooenclose entre parênteses.</span><span class="sxs-lookup"><span data-stu-id="96bd3-131">For international phone numbers, you need tooenclose hello country code in parentheses.</span></span> <span data-ttu-id="96bd3-132">Por exemplo, para um número dos Estados Unidos, ele será **(1) 1234567890**.</span><span class="sxs-lookup"><span data-stu-id="96bd3-132">For example, for a United States number, it is **(1)1234567890**.</span></span>
   
      ![][9]
6. <span data-ttu-id="96bd3-133">Em seguida, você deve receber uma mensagem de texto com um número de verificação, conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="96bd3-133">You should then receive a text message with a verification number, as shown in hello following example:</span></span>
   
      ![][10]
7. <span data-ttu-id="96bd3-134">Insira o número de verificação de saudação da mensagem de saudação em**验证码**(**código de confirmação**).</span><span class="sxs-lookup"><span data-stu-id="96bd3-134">Enter hello verification number from hello message in **验证码** (**Confirmation code**).</span></span>
8. <span data-ttu-id="96bd3-135">Por fim, concluir o registro de desenvolvedor de saudação aceitar Olá Baidu contrato e clicando em**提交**(**enviar**).</span><span class="sxs-lookup"><span data-stu-id="96bd3-135">Finally, complete hello developer registration by accepting hello Baidu agreement and clicking **提交** (**Submit**).</span></span> <span data-ttu-id="96bd3-136">Você verá Olá página após a conclusão bem-sucedida do registro a seguir:</span><span class="sxs-lookup"><span data-stu-id="96bd3-136">You will see hello following page on successful completion of registration:</span></span>
   
      ![][11]

## <a name="create-a-baidu-cloud-push-project"></a><span data-ttu-id="96bd3-137">Criar um projeto de envio na nuvem Baidu</span><span class="sxs-lookup"><span data-stu-id="96bd3-137">Create a Baidu cloud push project</span></span>
<span data-ttu-id="96bd3-138">Quando você cria um projeto de envio na nuvem Baidu, você recebe sua ID de aplicativo, chave API e a chave secreta.</span><span class="sxs-lookup"><span data-stu-id="96bd3-138">When you create a Baidu cloud push project, you receive your app ID, API key, and secret key.</span></span>

1. <span data-ttu-id="96bd3-139">Depois de fazer logon em toohello [Baidu portal], clique em**更多 >>** (**mais**).</span><span class="sxs-lookup"><span data-stu-id="96bd3-139">Once you have logged in toohello [Baidu portal], click **更多>>** (**more**).</span></span>
   
      ![][5]
2. <span data-ttu-id="96bd3-140">Role para baixo na Olá**站长与开发者服务**(**Webmaster e serviços de desenvolvedor**) seção e clique em**百度开放云平台**(**Baidu abrir plataforma de nuvem**).</span><span class="sxs-lookup"><span data-stu-id="96bd3-140">Scroll down in hello **站长与开发者服务** (**Webmaster and Developer Services**) section and click **百度开放云平台** (**Baidu open cloud platform**).</span></span>
   
      ![][6]
3. <span data-ttu-id="96bd3-141">Na próxima página do hello, clique em**开发者服务**(**serviços de desenvolvedor**) no canto superior direito de saudação.</span><span class="sxs-lookup"><span data-stu-id="96bd3-141">On hello next page, click **开发者服务** (**Developer Services**) on hello top-right corner.</span></span>
   
      ![][7]
4. <span data-ttu-id="96bd3-142">Na próxima página do hello, clique em**云推送**(**Push de nuvem**) do hello**云服务**(**serviços de nuvem**) seção.</span><span class="sxs-lookup"><span data-stu-id="96bd3-142">On hello next page, click **云推送** (**Cloud Push**) from hello **云服务** (**Cloud Services**) section.</span></span>
   
      ![][12]
5. <span data-ttu-id="96bd3-143">Quando você for um desenvolvedor registrado, você ver**管理控制台**(**Console de gerenciamento**) no menu superior hello.</span><span class="sxs-lookup"><span data-stu-id="96bd3-143">Once you are a registered developer, you see **管理控制台** (**Management Console**) at hello top menu.</span></span> <span data-ttu-id="96bd3-144">Clique em **开发者服务管理** (**Gerenciamento de Serviço de Desenvolvedores**).</span><span class="sxs-lookup"><span data-stu-id="96bd3-144">Click **开发者服务管理** (**Developers Service Management**).</span></span>
   
      ![][13]
6. <span data-ttu-id="96bd3-145">Na próxima página do hello, clique em**创建工程**(**criar projeto**).</span><span class="sxs-lookup"><span data-stu-id="96bd3-145">On hello next page, click **创建工程** (**Create Project**).</span></span>
   
      ![][14]
7. <span data-ttu-id="96bd3-146">Insira um nome de aplicativo e clique em **创建** (**Criar**).</span><span class="sxs-lookup"><span data-stu-id="96bd3-146">Enter an application name and click **创建** (**Create**).</span></span>
   
      ![][15]
8. <span data-ttu-id="96bd3-147">Após a criação bem-sucedida de um projeto de push da nuvem Baidu, você verá uma página com a **ID de Aplicativo**, **Chave de API** e **Chave Secreta**.</span><span class="sxs-lookup"><span data-stu-id="96bd3-147">Upon successful creation of a Baidu cloud push project, you see a page with **AppID**, **API Key**, and **Secret Key**.</span></span> <span data-ttu-id="96bd3-148">Anote a chave de API hello e chave secreta, que vamos usar mais tarde.</span><span class="sxs-lookup"><span data-stu-id="96bd3-148">Make a note of hello API key and secret key, which we will use later.</span></span>
   
      ![][16]
9. <span data-ttu-id="96bd3-149">Configurar projeto Olá para notificações por push clicando**云推送**(**por Push de nuvem**) no painel esquerdo da saudação.</span><span class="sxs-lookup"><span data-stu-id="96bd3-149">Configure hello project for push notifications by clicking **云推送** (**Cloud Push**) on hello left pane.</span></span>
   
      ![][31]
10. <span data-ttu-id="96bd3-150">Na página seguinte do hello, clique em Olá**推送设置**(**enviar por Push configurações**) botão.</span><span class="sxs-lookup"><span data-stu-id="96bd3-150">On hello next page, click hello **推送设置** (**Push settings**) button.</span></span>
    
    ![][32]  
11. <span data-ttu-id="96bd3-151">Na página de configuração hello, adicionar nome do pacote de saudação que você usará em seu projeto Android em Olá**应用包名**(**pacote de aplicativo**) campo e, em seguida, clique em**保存设置**( **Salvar**).</span><span class="sxs-lookup"><span data-stu-id="96bd3-151">On hello configuration page, add hello package name that you will be using in your Android project in hello **应用包名** (**Application package**) field, and then click **保存设置** (**Save**).</span></span>  
    
    ![][33]

<span data-ttu-id="96bd3-152">Consulte Olá**保存成功!** Mensagem (**salva com êxito!**).</span><span class="sxs-lookup"><span data-stu-id="96bd3-152">You see hello **保存成功！** (**Successfully saved!**) message.</span></span>

## <a name="configure-your-notification-hub"></a><span data-ttu-id="96bd3-153">Configurar seu Hub de Notificação</span><span class="sxs-lookup"><span data-stu-id="96bd3-153">Configure your notification hub</span></span>
1. <span data-ttu-id="96bd3-154">Entrar toohello [Portal clássico do Azure]e, em seguida, clique em **+ novo** na parte inferior da saudação da tela hello.</span><span class="sxs-lookup"><span data-stu-id="96bd3-154">Sign in toohello [Azure Classic Portal], and then click **+NEW** at hello bottom of hello screen.</span></span>
2. <span data-ttu-id="96bd3-155">Clique em **Serviços de Aplicativos**, em **Barramento de Serviço**, em **Hub de Notificação** e em **Criação Rápida**.</span><span class="sxs-lookup"><span data-stu-id="96bd3-155">Click **App Services**, click **Service Bus**, click **Notification Hub**, and then click **Quick Create**.</span></span>
3. <span data-ttu-id="96bd3-156">Forneça um nome para sua **Hub de notificação**, selecione Olá **região** e hello **Namespace** onde este hub de notificação será criado e, em seguida, clique em  **Criar um novo Hub de notificação**.</span><span class="sxs-lookup"><span data-stu-id="96bd3-156">Provide a name for your **Notification Hub**, select hello **Region** and hello **Namespace** where this notification hub will be created, and then click **Create a New Notification Hub**.</span></span>  
   
      ![][17]
4. <span data-ttu-id="96bd3-157">Clique em Olá namespace em que você criou seu hub de notificação e, em seguida, clique em **Hubs de notificação** na parte superior da saudação.</span><span class="sxs-lookup"><span data-stu-id="96bd3-157">Click hello namespace in which you created your notification hub, and then click **Notification Hubs** at hello top.</span></span>
   
      ![][18]
5. <span data-ttu-id="96bd3-158">Hub de notificação Olá selecione que você criou e, em seguida, clique em **configurar** no menu superior hello.</span><span class="sxs-lookup"><span data-stu-id="96bd3-158">Select hello notification hub that you created, and then click **Configure** from hello top menu.</span></span>
   
      ![][19]
6. <span data-ttu-id="96bd3-159">Role para baixo toohello **as configurações de notificação baidu** seção e insira a chave de API de saudação e a chave secreta que você obteve do console do Baidu Olá anteriormente para seu projeto de envio por push de nuvem do Baidu.</span><span class="sxs-lookup"><span data-stu-id="96bd3-159">Scroll down toohello **baidu notification settings** section and enter hello API key and secret key that you obtained from hello Baidu console previously for your Baidu cloud push project.</span></span> <span data-ttu-id="96bd3-160">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="96bd3-160">Click **Save**.</span></span>
   
      ![][20]
7. <span data-ttu-id="96bd3-161">Clique em Olá **painel** guia na parte superior de Olá Olá hub de notificação e, em seguida, clique em **Exibir cadeia de Conexão**.</span><span class="sxs-lookup"><span data-stu-id="96bd3-161">Click hello **Dashboard** tab at hello top for hello notification hub, and then click **View Connection String**.</span></span>
   
      ![][21]
8. <span data-ttu-id="96bd3-162">Anote Olá **DefaultListenSharedAccessSignature** e **DefaultFullSharedAccessSignature** de saudação **acessar as informações de conexão** janela.</span><span class="sxs-lookup"><span data-stu-id="96bd3-162">Make a note of hello **DefaultListenSharedAccessSignature** and **DefaultFullSharedAccessSignature** from hello **Access connection information** window.</span></span>
   
    ![][22]

## <a name="connect-your-app-toohello-notification-hub"></a><span data-ttu-id="96bd3-163">Conecte-se o seu hub de notificação do aplicativo toohello</span><span class="sxs-lookup"><span data-stu-id="96bd3-163">Connect your app toohello notification hub</span></span>
1. <span data-ttu-id="96bd3-164">No Eclipse ADT, crie um novo projeto Android (**Arquivo** > **Novo** > **Projeto de Aplicativo Android**).</span><span class="sxs-lookup"><span data-stu-id="96bd3-164">In Eclipse ADT, create a new Android project (**File** > **New** > **Android Application Project**).</span></span>
   
    ![][23]
2. <span data-ttu-id="96bd3-165">Insira um **nome do aplicativo** e certifique-se de que Olá **mínimo necessário SDK** versão está definida muito**API 16: Android 4.1**.</span><span class="sxs-lookup"><span data-stu-id="96bd3-165">Enter an **Application Name** and ensure that hello **Minimum Required SDK** version is set too**API 16: Android 4.1**.</span></span>
   
    ![][24]
3. <span data-ttu-id="96bd3-166">Clique em **próximo** e continuar após o Assistente de saudação até Olá **Criar atividade** janela é exibida.</span><span class="sxs-lookup"><span data-stu-id="96bd3-166">Click **Next** and continue following hello wizard until hello **Create Activity** window appears.</span></span> <span data-ttu-id="96bd3-167">Verifique se **atividade em branco** está selecionado e, por fim, selecione **concluir** toocreate um novo aplicativo Android.</span><span class="sxs-lookup"><span data-stu-id="96bd3-167">Make sure that **Blank Activity** is selected, and finally select **Finish** toocreate a new Android Application.</span></span>
   
    ![][25]
4. <span data-ttu-id="96bd3-168">Certifique-se de que Olá **destino de compilação de projeto** está definida corretamente.</span><span class="sxs-lookup"><span data-stu-id="96bd3-168">Make sure that hello **Project Build Target** is set correctly.</span></span>
   
    ![][26]
5. <span data-ttu-id="96bd3-169">Baixe o arquivo de 0.4.jar de hubs de notificação de saudação do hello **arquivos** guia da saudação [notificação-Hubs-Android-SDK em Bintray](https://bintray.com/microsoftazuremobile/SDK/Notification-Hubs-Android-SDK/0.4).</span><span class="sxs-lookup"><span data-stu-id="96bd3-169">Download hello notification-hubs-0.4.jar file from hello **Files** tab of hello [Notification-Hubs-Android-SDK on Bintray](https://bintray.com/microsoftazuremobile/SDK/Notification-Hubs-Android-SDK/0.4).</span></span> <span data-ttu-id="96bd3-170">Adicionar Olá arquivo toohello **bibliotecas** pasta de projeto do Eclipse e atualização Olá *bibliotecas* pasta.</span><span class="sxs-lookup"><span data-stu-id="96bd3-170">Add hello file toohello **libs** folder of your Eclipse project, and refresh hello *libs* folder.</span></span>
6. <span data-ttu-id="96bd3-171">Baixe e descompacte Olá [Baidu Push Android SDK], abra Olá **bibliotecas** pasta e, em seguida, Olá cópia **pushservice x.y.z** jar do arquivo e hello **armeabi**  &  **mips** pastas no hello **bibliotecas** pasta do seu aplicativo Android.</span><span class="sxs-lookup"><span data-stu-id="96bd3-171">Download and unzip hello [Baidu Push Android SDK], open hello **libs** folder, and then copy hello **pushservice-x.y.z** jar file and hello **armeabi** & **mips** folders in hello **libs** folder of your Android application.</span></span>
7. <span data-ttu-id="96bd3-172">Olá abrir **AndroidManifest.xml** arquivo do seu Android do projeto e adicionar permissões de saudação que são exigidas pelo Olá Baidu SDK.</span><span class="sxs-lookup"><span data-stu-id="96bd3-172">Open hello **AndroidManifest.xml** file of your Android project and add hello permissions that are required by hello Baidu SDK.</span></span>
   
        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.READ_PHONE_STATE" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.WRITE_SETTINGS" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
        <uses-permission android:name="android.permission.DISABLE_KEYGUARD" />
        <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
        <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
        <uses-permission android:name="android.permission.ACCESS_DOWNLOAD_MANAGER" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION" />
8. <span data-ttu-id="96bd3-173">Adicionar Olá **android: name** propriedade tooyour **aplicativo** elemento **AndroidManifest.xml**, substituindo *yourprojectname* (para exemplo, **com.example.BaiduTest**).</span><span class="sxs-lookup"><span data-stu-id="96bd3-173">Add hello **android:name** property tooyour **application** element in **AndroidManifest.xml**, replacing *yourprojectname* (for example, **com.example.BaiduTest**).</span></span> <span data-ttu-id="96bd3-174">Verifique se o nome do projeto corresponde Olá um que você configurou no console do Baidu hello.</span><span class="sxs-lookup"><span data-stu-id="96bd3-174">Make sure that this project name matches hello one that you configured in hello Baidu console.</span></span>
   
        <application android:name="yourprojectname.DemoApplication"
9. <span data-ttu-id="96bd3-175">Adicionar Olá seguinte configuração dentro do elemento de aplicativo hello após Olá **. MainActivity** elemento da atividade, substituindo *yourprojectname* (por exemplo, **com.example.BaiduTest**):</span><span class="sxs-lookup"><span data-stu-id="96bd3-175">Add hello following configuration within hello application element after hello **.MainActivity** activity element, replacing *yourprojectname* (for example, **com.example.BaiduTest**):</span></span>
   
        <receiver android:name="yourprojectname.MyPushMessageReceiver">
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.MESSAGE" />
                <action android:name="com.baidu.android.pushservice.action.RECEIVE" />
                <action android:name="com.baidu.android.pushservice.action.notification.CLICK" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.baidu.android.pushservice.PushServiceReceiver"
            android:process=":bdservice_v1">
            <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED" />
                <action android:name="android.net.conn.CONNECTIVITY_CHANGE" />
                <action android:name="com.baidu.android.pushservice.action.notification.SHOW" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.baidu.android.pushservice.RegistrationReceiver"
            android:process=":bdservice_v1">
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.METHOD" />
                <action android:name="com.baidu.android.pushservice.action.BIND_SYNC" />
            </intent-filter>
            <intent-filter>
                <action android:name="android.intent.action.PACKAGE_REMOVED"/>
                <data android:scheme="package" />
            </intent-filter>
        </receiver>
   
        <service
            android:name="com.baidu.android.pushservice.PushService"
            android:exported="true"
            android:process=":bdservice_v1"  >
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.PUSH_SERVICE" />
            </intent-filter>
        </service>
10. <span data-ttu-id="96bd3-176">Adicionar uma nova classe chamada **ConfigurationSettings.java** toohello projeto.</span><span class="sxs-lookup"><span data-stu-id="96bd3-176">Add a new class called **ConfigurationSettings.java** toohello project.</span></span>
    
     ![][28]
    
     ![][29]
11. <span data-ttu-id="96bd3-177">Adicione Olá tooit de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="96bd3-177">Add hello following code tooit:</span></span>
    
        public class ConfigurationSettings {
                public static String API_KEY = "...";
                public static String NotificationHubName = "...";
                public static String NotificationHubConnectionString = "...";
            }
    
    <span data-ttu-id="96bd3-178">Definir o valor de saudação do **API_KEY** com o que você recuperou do projeto da nuvem Baidu Olá anteriormente, **NotificationHubName** com seu nome de hub de notificação de saudação Portal clássico do Azure e  **NotificationHubConnectionString** com DefaultListenSharedAccessSignature de saudação Portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="96bd3-178">Set hello value of **API_KEY** with what you retrieved from hello Baidu cloud project earlier, **NotificationHubName** with your notification hub name from hello Azure Classic Portal and **NotificationHubConnectionString** with DefaultListenSharedAccessSignature from hello Azure Classic Portal.</span></span>
12. <span data-ttu-id="96bd3-179">Adicionar uma nova classe chamada **DemoApplication.java**e adicione Olá tooit de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="96bd3-179">Add a new class called **DemoApplication.java**, and add hello following code tooit:</span></span>
    
        import com.baidu.frontia.FrontiaApplication;
    
        public class DemoApplication extends FrontiaApplication {
            @Override
            public void onCreate() {
                super.onCreate();
            }
        }
13. <span data-ttu-id="96bd3-180">Adicionar uma nova classe chamada **MyPushMessageReceiver.java**e adicione Olá tooit de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="96bd3-180">Add another new class called **MyPushMessageReceiver.java**, and add hello following code tooit.</span></span> <span data-ttu-id="96bd3-181">É classe Olá identificadores Olá notificações por push que são recebidas do servidor de envio por push do hello Baidu.</span><span class="sxs-lookup"><span data-stu-id="96bd3-181">It is hello class that handles hello push notifications that are received from hello Baidu push server.</span></span>
    
        import java.util.List;
        import android.content.Context;
        import android.os.AsyncTask;
        import android.util.Log;
        import com.baidu.frontia.api.FrontiaPushMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub;
    
        public class MyPushMessageReceiver extends FrontiaPushMessageReceiver {
            /** TAG tooLog */
            public static NotificationHub hub = null;
            public static String mChannelId, mUserId;
            public static final String TAG = MyPushMessageReceiver.class
                    .getSimpleName();
    
            @Override
            public void onBind(Context context, int errorCode, String appid,
                    String userId, String channelId, String requestId) {
                String responseString = "onBind errorCode=" + errorCode + " appid="
                        + appid + " userId=" + userId + " channelId=" + channelId
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
                mChannelId = channelId;
                mUserId = userId;
    
                try {
                    if (hub == null) {
                        hub = new NotificationHub(
                                ConfigurationSettings.NotificationHubName,
                                ConfigurationSettings.NotificationHubConnectionString,
                                context);
                        Log.i(TAG, "Notification hub initialized");
                    }
                } catch (Exception e) {
                   Log.e(TAG, e.getMessage());
                }
    
                registerWithNotificationHubs();
            }
    
            private void registerWithNotificationHubs() {
               new AsyncTask<Void, Void, Void>() {
                  @Override
                  protected Void doInBackground(Void... params) {
                     try {
                         hub.registerBaidu(mUserId, mChannelId);
                         Log.i(TAG, "Registered with Notification Hub - '"
                                 + ConfigurationSettings.NotificationHubName + "'"
                                 + " with UserId - '"
                                 + mUserId + "' and Channel Id - '"
                                 + mChannelId + "'");
                     } catch (Exception e) {
                         Log.e(TAG, e.getMessage());
                     }
                     return null;
                 }
               }.execute(null, null, null);
            }
    
            @Override
            public void onSetTags(Context context, int errorCode,
                    List<String> sucessTags, List<String> failTags, String requestId) {
                String responseString = "onSetTags errorCode=" + errorCode
                        + " sucessTags=" + sucessTags + " failTags=" + failTags
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onDelTags(Context context, int errorCode,
                    List<String> sucessTags, List<String> failTags, String requestId) {
                String responseString = "onDelTags errorCode=" + errorCode
                        + " sucessTags=" + sucessTags + " failTags=" + failTags
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onListTags(Context context, int errorCode, List<String> tags,
                    String requestId) {
                String responseString = "onListTags errorCode=" + errorCode + " tags="
                        + tags;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onUnbind(Context context, int errorCode, String requestId) {
                String responseString = "onUnbind errorCode=" + errorCode
                        + " requestId = " + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onNotificationClicked(Context context, String title,
                    String description, String customContentString) {
                String notifyString = "title=\"" + title + "\" description=\""
                        + description + "\" customContent=" + customContentString;
                Log.d(TAG, notifyString);
            }
    
            @Override
            public void onMessage(Context context, String message,
                    String customContentString) {
                String messageString = "message=\"" + message + "\" customContentString=" + customContentString;
                Log.d(TAG, messageString);
            }
        }
14. <span data-ttu-id="96bd3-182">Abra **MainActivity.java**e adicione Olá após toohello **onCreate** método:</span><span class="sxs-lookup"><span data-stu-id="96bd3-182">Open **MainActivity.java**, and add hello following toohello **onCreate** method:</span></span>
    
            PushManager.startWork(getApplicationContext(),
                    PushConstants.LOGIN_TYPE_API_KEY, ConfigurationSettings.API_KEY);
15. <span data-ttu-id="96bd3-183">Abra Olá seguindo as instruções de importação na parte superior da saudação:</span><span class="sxs-lookup"><span data-stu-id="96bd3-183">Open hello following import statements at hello top:</span></span>
    
            import com.baidu.android.pushservice.PushConstants;
            import com.baidu.android.pushservice.PushManager;

## <a name="send-notifications-tooyour-app"></a><span data-ttu-id="96bd3-184">Enviar notificações tooyour aplicativo</span><span class="sxs-lookup"><span data-stu-id="96bd3-184">Send notifications tooyour app</span></span>
<span data-ttu-id="96bd3-185">Você pode testar rapidamente a receber notificações em seu aplicativo pelo envio de notificações em Olá [portal do Azure](https://portal.azure.com/) usando Olá **enviar** botão no hub de notificação hello, conforme mostrado no hello tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="96bd3-185">You can quickly test receiving notifications in your app by sending notifications in hello [Azure portal](https://portal.azure.com/) using hello **Send** button on hello notification hub, as shown in hello following screen:</span></span>

![](./media/notification-hubs-baidu-get-started/notification-hub-test-send-baidu.png)

<span data-ttu-id="96bd3-186">Notificações por push normalmente são enviadas em um serviço de back-end como Serviços Móveis ou ASP.NET usando uma biblioteca compatível.</span><span class="sxs-lookup"><span data-stu-id="96bd3-186">Push notifications are normally sent in a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="96bd3-187">Se uma biblioteca não está disponível para o back-end, você pode usar o hello API REST diretamente as mensagens de notificação toosend.</span><span class="sxs-lookup"><span data-stu-id="96bd3-187">If a library is not available for your back-end, you can use hello REST API directly toosend notification messages .</span></span>

<span data-ttu-id="96bd3-188">Neste tutorial, podemos manter a simplicidade e demonstrar a testar seu aplicativo de cliente por meio do envio de notificações usando Olá SDK .NET para hubs de notificação em um aplicativo de console, em vez de um serviço de back-end.</span><span class="sxs-lookup"><span data-stu-id="96bd3-188">In this tutorial, we keep it simple and just demonstrate testing your client app by sending notifications using hello .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="96bd3-189">É recomendável Olá [usar Hubs de notificação toopush notificações toousers](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) tutorial como a próxima etapa hello para enviar notificações de um back-end do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="96bd3-189">We recommend hello [Use Notification Hubs toopush notifications toousers](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) tutorial as hello next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="96bd3-190">No entanto, a saudação abordagens a seguir pode ser usada para enviar notificações:</span><span class="sxs-lookup"><span data-stu-id="96bd3-190">However, hello following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="96bd3-191">**Interface REST**: você pode dar suporte à notificação em qualquer plataforma de back-end usando Olá [interface REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="96bd3-191">**REST Interface**:  You can support notification on any backend platform using  hello [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="96bd3-192">**SDK .NET de Hubs de notificação do Microsoft Azure**: em Olá Gerenciador de pacotes do Nuget para Visual Studio, execute [Microsoft.Azure.NotificationHubs Install-Package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="96bd3-192">**Microsoft Azure Notification Hubs .NET SDK**: In hello Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="96bd3-193">**Node.js**: [como toouse Hubs de notificação do Node. js](notification-hubs-nodejs-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="96bd3-193">**Node.js**: [How toouse Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>
* <span data-ttu-id="96bd3-194">**Aplicativos móveis**: para obter um exemplo de como toosend notificações de um back-end aplicativos de celular do serviço de aplicativo do Azure que esteja integrado com Hubs de notificação, consulte [aplicativo móvel de tooyour adicionar de notificações por push](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="96bd3-194">**Mobile Apps**: For an example of how toosend notifications from an Azure App Service Mobile Apps backend that's integrated with Notification Hubs, see [Add push notifications tooyour mobile app](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span></span>
* <span data-ttu-id="96bd3-195">**Java / PHP**: para obter um exemplo de como as notificações de toosend usando Olá APIs REST, consulte "como toouse Hubs de notificação do Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span><span class="sxs-lookup"><span data-stu-id="96bd3-195">**Java / PHP**: For an example of how toosend notifications by using hello REST APIs, see "How toouse Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

## <a name="optional-send-notifications-from-a-net-console-app"></a><span data-ttu-id="96bd3-196">(Opcional) Enviar notificações de um aplicativo de console do .NET.</span><span class="sxs-lookup"><span data-stu-id="96bd3-196">(Optional) Send notifications from a .NET console app.</span></span>
<span data-ttu-id="96bd3-197">Nesta seção, vamos mostrar o envio de uma notificação usando um aplicativo de console do .NET.</span><span class="sxs-lookup"><span data-stu-id="96bd3-197">In this section, we show sending a notification using a .NET console app.</span></span>

1. <span data-ttu-id="96bd3-198">Crie um novo aplicativo de console do Visual C#:</span><span class="sxs-lookup"><span data-stu-id="96bd3-198">Create a new Visual C# console application:</span></span>
   
    ![][30]
2. <span data-ttu-id="96bd3-199">Olá janela do Console do Gerenciador de pacotes, definido Olá **projeto padrão** tooyour novo projeto de aplicativo de console e na janela de console hello, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="96bd3-199">In hello Package Manager Console window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="96bd3-200">Essa instrução adiciona um toohello Referência SDK de Hubs de notificação do Azure usando Olá <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pacote NuGet de Hubs Microsoft.Azure.Notification</a>.</span><span class="sxs-lookup"><span data-stu-id="96bd3-200">This instruction adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
3. <span data-ttu-id="96bd3-201">Arquivo hello abrir **Program.cs** e adicione o seguinte hello usando a instrução:</span><span class="sxs-lookup"><span data-stu-id="96bd3-201">Open hello file **Program.cs** and add hello following using statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
4. <span data-ttu-id="96bd3-202">No seu `Program` de classe, adicione Olá método a seguir e substitua *DefaultFullSharedAccessSignatureSASConnectionString* e *NotificationHubName* com valores hello que você tem.</span><span class="sxs-lookup"><span data-stu-id="96bd3-202">In your `Program` class, add hello following method and replace *DefaultFullSharedAccessSignatureSASConnectionString* and *NotificationHubName* with hello values that you have.</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("DefaultFullSharedAccessSignatureSASConnectionString", "NotificationHubName");
            string message = "{\"title\":\"((Notification title))\",\"description\":\"Hello from Azure\"}";
            var result = await hub.SendBaiduNativeNotificationAsync(message);
        }
5. <span data-ttu-id="96bd3-203">Adicionar Olá seguintes linhas no seu **principal** método:</span><span class="sxs-lookup"><span data-stu-id="96bd3-203">Add hello following lines in your **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();

## <a name="test-your-app"></a><span data-ttu-id="96bd3-204">Testar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="96bd3-204">Test your app</span></span>
<span data-ttu-id="96bd3-205">tootest neste aplicativo com um telefone real, basta conectar Olá computador do telefone tooyour usando um cabo USB.</span><span class="sxs-lookup"><span data-stu-id="96bd3-205">tootest this app with an actual phone, just connect hello phone tooyour computer by using a USB cable.</span></span> <span data-ttu-id="96bd3-206">Essa ação carrega o aplicativo para telefone Olá anexado.</span><span class="sxs-lookup"><span data-stu-id="96bd3-206">This action loads your app onto hello attached phone.</span></span>

<span data-ttu-id="96bd3-207">tootest esse aplicativo com o emulador do Windows hello, Olá Eclipse superior barra de ferramentas, clique **executar**e, em seguida, selecione seu aplicativo: ele inicia o emulador do Windows hello, carga, e é executado Olá aplicativo.</span><span class="sxs-lookup"><span data-stu-id="96bd3-207">tootest this app with hello emulator, on hello Eclipse top toolbar, click **Run**, and then select your app: it starts hello emulator, loads, and runs hello app.</span></span>

<span data-ttu-id="96bd3-208">aplicativo Hello recupera Olá 'userId' e 'channelId' de saudação serviço de notificação por Push do Baidu e registra com o hub de notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="96bd3-208">hello app retrieves hello 'userId' and 'channelId' from hello Baidu Push notification service and registers with hello notification hub.</span></span>

<span data-ttu-id="96bd3-209">toosend uma notificação de teste, você pode usar o guia de depuração de saudação do hello Portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="96bd3-209">toosend a test notification, you can use hello debug tab of hello Azure Classic Portal.</span></span> <span data-ttu-id="96bd3-210">Se você criou um aplicativo de console hello .NET para o Visual Studio, basta pressione tecla F5 de saudação no aplicativo do Visual Studio toorun hello.</span><span class="sxs-lookup"><span data-stu-id="96bd3-210">If you built hello .NET console application for Visual Studio, just press hello F5 key in Visual Studio toorun hello application.</span></span> <span data-ttu-id="96bd3-211">aplicativo Hello envia uma notificação que aparece na área de notificação superior de saudação do seu dispositivo ou emulador.</span><span class="sxs-lookup"><span data-stu-id="96bd3-211">hello application sends a notification that appears in hello top notification area of your device or emulator.</span></span>

<!-- Images. -->
[1]: ./media/notification-hubs-baidu-get-started/BaiduRegistration.png
[2]: ./media/notification-hubs-baidu-get-started/BaiduRegistrationInput.png
[3]: ./media/notification-hubs-baidu-get-started/BaiduConfirmation.png
[4]: ./media/notification-hubs-baidu-get-started/BaiduActivationEmail.png
[5]: ./media/notification-hubs-baidu-get-started/BaiduRegistrationMore.png
[6]: ./media/notification-hubs-baidu-get-started/BaiduOpenCloudPlatform.png
[7]: ./media/notification-hubs-baidu-get-started/BaiduDeveloperServices.png
[8]: ./media/notification-hubs-baidu-get-started/BaiduDeveloperRegistration.png
[9]: ./media/notification-hubs-baidu-get-started/BaiduDevRegistrationInput.png
[10]: ./media/notification-hubs-baidu-get-started/BaiduDevRegistrationConfirmation.png
[11]: ./media/notification-hubs-baidu-get-started/BaiduDevConfirmationFinal.png
[12]: ./media/notification-hubs-baidu-get-started/BaiduCloudPush.png
[13]: ./media/notification-hubs-baidu-get-started/BaiduDevSvcMgmt.png
[14]: ./media/notification-hubs-baidu-get-started/BaiduCreateProject.png
[15]: ./media/notification-hubs-baidu-get-started/BaiduCreateProjectInput.png
[16]: ./media/notification-hubs-baidu-get-started/BaiduProjectKeys.png
[17]: ./media/notification-hubs-baidu-get-started/AzureNHCreation.png
[18]: ./media/notification-hubs-baidu-get-started/NotificationHubs.png
[19]: ./media/notification-hubs-baidu-get-started/NotificationHubsConfigure.png
[20]: ./media/notification-hubs-baidu-get-started/NotificationHubBaiduConfigure.png
[21]: ./media/notification-hubs-baidu-get-started/NotificationHubsConnectionStringView.png
[22]: ./media/notification-hubs-baidu-get-started/NotificationHubsConnectionString.png
[23]: ./media/notification-hubs-baidu-get-started/EclipseNewProject.png
[24]: ./media/notification-hubs-baidu-get-started/EclipseProjectCreation.png
[25]: ./media/notification-hubs-baidu-get-started/EclipseBlankActivity.png
[26]: ./media/notification-hubs-baidu-get-started/EclipseProjectBuildProperty.png
[27]: ./media/notification-hubs-baidu-get-started/EclipseBaiduReferences.png
[28]: ./media/notification-hubs-baidu-get-started/EclipseNewClass.png
[29]: ./media/notification-hubs-baidu-get-started/EclipseConfigSettingsClass.png
[30]: ./media/notification-hubs-baidu-get-started/ConsoleProject.png
[31]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig1.png
[32]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig2.png
[33]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig3.png

<!-- URLs. -->
[SDK para Android de Serviços Móveis]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Baidu Push Android SDK]: http://developer.baidu.com/wiki/index.php?title=docs/cplat/push/sdk/clientsdk
[Portal clássico do Azure]: https://manage.windowsazure.com/
[Baidu portal]: http://www.baidu.com/
