---
title: "Introdução aos Hubs de Notificação do Azure usando o Baidu | Microsoft Docs"
description: "Neste tutorial, você aprenderá a usar os Hubs de Notificação do Azure para enviar notificações por push aos dispositivos Android que usam o Baidu."
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
ms.openlocfilehash: df3bbda15e1245b6068c2b8290d0c96856051f1f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-notification-hubs-using-baidu"></a><span data-ttu-id="c2f9a-103">Introdução aos Hubs de Notificação usando o Baidu</span><span class="sxs-lookup"><span data-stu-id="c2f9a-103">Get started with Notification Hubs using Baidu</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="c2f9a-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="c2f9a-104">Overview</span></span>
<span data-ttu-id="c2f9a-105">O envio de nuvem Baidu é um serviço na nuvem chinês que você pode usar para enviar notificações por push para dispositivos móveis.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-105">Baidu cloud push is a Chinese cloud service that you can use to send push notifications to mobile devices.</span></span> <span data-ttu-id="c2f9a-106">Esse serviço é útil na China, onde a entrega de notificações por push para o Android é complexa devido à presença de diferentes lojas de aplicativos e serviços de notificações por push, bem como a disponibilidade dos dispositivos Android que não estão normalmente conectados ao GCM (Google Cloud Messaging).</span><span class="sxs-lookup"><span data-stu-id="c2f9a-106">This service is useful in China, where delivering push notifications to Android is complex because of the presence of different app stores and push services, in addition to the availability of Android devices that are not typically connected to GCM (Google Cloud Messaging).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c2f9a-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c2f9a-107">Prerequisites</span></span>
<span data-ttu-id="c2f9a-108">Este tutorial exige:</span><span class="sxs-lookup"><span data-stu-id="c2f9a-108">This tutorial requires:</span></span>

* <span data-ttu-id="c2f9a-109">SDK do Android (supondo que você usa o Eclipse), que pode ser baixado no <a href="http://go.microsoft.com/fwlink/?LinkId=389797">site do Android</a></span><span class="sxs-lookup"><span data-stu-id="c2f9a-109">Android SDK (we assume that you use Eclipse), which you can download from the <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android site</a></span></span>
* <span data-ttu-id="c2f9a-110">[SDK para Android de Serviços Móveis]</span><span class="sxs-lookup"><span data-stu-id="c2f9a-110">[Mobile Services Android SDK]</span></span>
* <span data-ttu-id="c2f9a-111">[SDK do Android Push Baidu]</span><span class="sxs-lookup"><span data-stu-id="c2f9a-111">[Baidu Push Android SDK]</span></span>

> [!NOTE]
> <span data-ttu-id="c2f9a-112">Para concluir este tutorial, você precisa ter uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-112">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="c2f9a-113">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="c2f9a-114">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-baidu-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="c2f9a-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-baidu-get-started%2F).</span></span>
> 
> 

## <a name="create-a-baidu-account"></a><span data-ttu-id="c2f9a-115">Criar uma conta de Baidu</span><span class="sxs-lookup"><span data-stu-id="c2f9a-115">Create a Baidu account</span></span>
<span data-ttu-id="c2f9a-116">Para usar o Baidu, você deve ter uma conta do Baidu.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-116">To use Baidu, you must have a Baidu account.</span></span> <span data-ttu-id="c2f9a-117">Se você já tiver uma, faça logon no [portal do Baidu] e vá para a próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-117">If you already have one, log in to the [Baidu portal] and skip to the next step.</span></span> <span data-ttu-id="c2f9a-118">Caso contrário, veja as instruções abaixo sobre como criar uma conta do Baidu.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-118">Otherwise, see the following instructions on how to create a Baidu account.</span></span>  

1. <span data-ttu-id="c2f9a-119">Vá para o [portal do Baidu] e clique no link **登录** (**Login**).</span><span class="sxs-lookup"><span data-stu-id="c2f9a-119">Go to the [Baidu portal] and click the **登录** (**Login**) link.</span></span> <span data-ttu-id="c2f9a-120">Clique em **立即注册** para iniciar o processo de registro de conta.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-120">Click **立即注册** to start the account registration process.</span></span>
   
   ![][1]
2. <span data-ttu-id="c2f9a-121">Insira os detalhes necessários – telefone/endereço de email, senha e código de verificação – e clique em **Inscrever-se**.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-121">Enter the required details—phone/email address, password, and verification code—and click **Signup**.</span></span>
   
   ![][2]
3. <span data-ttu-id="c2f9a-122">Você receberá um email no endereço de email inserido com um link para ativar sua conta do Baidu.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-122">You will be sent an email to the email address that you entered with a link to activate your Baidu account.</span></span>
   
   ![][3]
4. <span data-ttu-id="c2f9a-123">Faça logon em sua conta de email, abra o email de ativação do Baidu e clique no link de ativação para ativar sua conta do Baidu.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-123">Log in to your email account, open the Baidu activation mail, and click the activation link to activate your Baidu account.</span></span>
   
   ![][4]

<span data-ttu-id="c2f9a-124">Depois de ativar uma conta do Baidu, faça logon no [portal do Baidu].</span><span class="sxs-lookup"><span data-stu-id="c2f9a-124">Once you have an activated Baidu account, log in to the [Baidu portal].</span></span>

## <a name="register-as-a-baidu-developer"></a><span data-ttu-id="c2f9a-125">Registrar-se como desenvolvedor Baidu</span><span class="sxs-lookup"><span data-stu-id="c2f9a-125">Register as a Baidu developer</span></span>
1. <span data-ttu-id="c2f9a-126">Depois de fazer logon no [portal do Baidu], clique em **更多 >>** (**mais**).</span><span class="sxs-lookup"><span data-stu-id="c2f9a-126">Once you have logged in to the [Baidu portal], click **更多>>** (**more**).</span></span>
   
      ![][5]
2. <span data-ttu-id="c2f9a-127">Role para baixo na seção **站长与开发者服务 (Webmaster e Serviços de Desenvolvedor)** e clique em **百度开放云平台** (**Baidu - abrir a plataforma de nuvem**).</span><span class="sxs-lookup"><span data-stu-id="c2f9a-127">Scroll down in the **站长与开发者服务 (Webmaster and Developer Services)** section and click **百度开放云平台** (**Baidu open cloud platform**).</span></span>
   
      ![][6]
3. <span data-ttu-id="c2f9a-128">Na página seguinte, clique em **开发者服务** (**Serviços de Desenvolvedor**) no canto superior direito.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-128">On the next page, click **开发者服务** (**Developer Services**) on the top-right corner.</span></span>
   
      ![][7]
4. <span data-ttu-id="c2f9a-129">Na página seguinte, clique em **注册开发者** (**Desenvolvedores Registrados**) no menu no canto superior direito.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-129">On the next page, click **注册开发者** (**Registered Developers**) from the menu on the top-right corner.</span></span>
   
      ![][8]
5. <span data-ttu-id="c2f9a-130">Insira seu nome, uma descrição e um número de telefone celular para receber uma mensagem de texto de verificação e, em seguida, clique em **送验证码** (**Enviar Código de Verificação**).</span><span class="sxs-lookup"><span data-stu-id="c2f9a-130">Enter your name, a description, and a mobile phone number for receiving a verification text message, and then click **送验证码** (**Send Verification Code**).</span></span> <span data-ttu-id="c2f9a-131">Para números de telefone internacionais, você precisa colocar o código do país entre parênteses.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-131">For international phone numbers, you need to enclose the country code in parentheses.</span></span> <span data-ttu-id="c2f9a-132">Por exemplo, para um número dos Estados Unidos, ele será **(1) 1234567890**.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-132">For example, for a United States number, it is **(1)1234567890**.</span></span>
   
      ![][9]
6. <span data-ttu-id="c2f9a-133">Em seguida, você deve receber uma mensagem de texto com um número de verificação, conforme mostrado no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="c2f9a-133">You should then receive a text message with a verification number, as shown in the following example:</span></span>
   
      ![][10]
7. <span data-ttu-id="c2f9a-134">Insira o número de verificação da mensagem no **验证码** (**Código de confirmação**).</span><span class="sxs-lookup"><span data-stu-id="c2f9a-134">Enter the verification number from the message in **验证码** (**Confirmation code**).</span></span>
8. <span data-ttu-id="c2f9a-135">Por fim, conclua o registro de desenvolvedor ao aceitar o Contrato de Baidu e clicar em **提交** (**Enviar**).</span><span class="sxs-lookup"><span data-stu-id="c2f9a-135">Finally, complete the developer registration by accepting the Baidu agreement and clicking **提交** (**Submit**).</span></span> <span data-ttu-id="c2f9a-136">Você verá a seguinte página na conclusão bem-sucedida do registro:</span><span class="sxs-lookup"><span data-stu-id="c2f9a-136">You will see the following page on successful completion of registration:</span></span>
   
      ![][11]

## <a name="create-a-baidu-cloud-push-project"></a><span data-ttu-id="c2f9a-137">Criar um projeto de envio na nuvem Baidu</span><span class="sxs-lookup"><span data-stu-id="c2f9a-137">Create a Baidu cloud push project</span></span>
<span data-ttu-id="c2f9a-138">Quando você cria um projeto de envio na nuvem Baidu, você recebe sua ID de aplicativo, chave API e a chave secreta.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-138">When you create a Baidu cloud push project, you receive your app ID, API key, and secret key.</span></span>

1. <span data-ttu-id="c2f9a-139">Depois de fazer logon no [portal do Baidu], clique em **更多 >>** (**mais**).</span><span class="sxs-lookup"><span data-stu-id="c2f9a-139">Once you have logged in to the [Baidu portal], click **更多>>** (**more**).</span></span>
   
      ![][5]
2. <span data-ttu-id="c2f9a-140">Role para baixo na seção **站长与开发者服务** (**Webmaster e Serviços de Desenvolvedor**) e clique em **百度开放云平台** (**Baidu - abrir a plataforma de nuvem**).</span><span class="sxs-lookup"><span data-stu-id="c2f9a-140">Scroll down in the **站长与开发者服务** (**Webmaster and Developer Services**) section and click **百度开放云平台** (**Baidu open cloud platform**).</span></span>
   
      ![][6]
3. <span data-ttu-id="c2f9a-141">Na página seguinte, clique em **开发者服务** (**Serviços de Desenvolvedor**) no canto superior direito.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-141">On the next page, click **开发者服务** (**Developer Services**) on the top-right corner.</span></span>
   
      ![][7]
4. <span data-ttu-id="c2f9a-142">Na página seguinte, clique em **云推送** (**Push de nuvem**) na seção **云服务** (**Serviços de nuvem**).</span><span class="sxs-lookup"><span data-stu-id="c2f9a-142">On the next page, click **云推送** (**Cloud Push**) from the **云服务** (**Cloud Services**) section.</span></span>
   
      ![][12]
5. <span data-ttu-id="c2f9a-143">Quando você for um desenvolvedor registrado, verá **管理控制台** (**Console de Gerenciamento**) no menu superior.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-143">Once you are a registered developer, you see **管理控制台** (**Management Console**) at the top menu.</span></span> <span data-ttu-id="c2f9a-144">Clique em **开发者服务管理** (**Gerenciamento de Serviço de Desenvolvedores**).</span><span class="sxs-lookup"><span data-stu-id="c2f9a-144">Click **开发者服务管理** (**Developers Service Management**).</span></span>
   
      ![][13]
6. <span data-ttu-id="c2f9a-145">Na página seguinte, clique em **创建工程** (**Criar projeto**).</span><span class="sxs-lookup"><span data-stu-id="c2f9a-145">On the next page, click **创建工程** (**Create Project**).</span></span>
   
      ![][14]
7. <span data-ttu-id="c2f9a-146">Insira um nome de aplicativo e clique em **创建** (**Criar**).</span><span class="sxs-lookup"><span data-stu-id="c2f9a-146">Enter an application name and click **创建** (**Create**).</span></span>
   
      ![][15]
8. <span data-ttu-id="c2f9a-147">Após a criação bem-sucedida de um projeto de push da nuvem Baidu, você verá uma página com a **ID de Aplicativo**, **Chave de API** e **Chave Secreta**.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-147">Upon successful creation of a Baidu cloud push project, you see a page with **AppID**, **API Key**, and **Secret Key**.</span></span> <span data-ttu-id="c2f9a-148">Anote a chave de API e a chave secreta, que usaremos mais tarde.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-148">Make a note of the API key and secret key, which we will use later.</span></span>
   
      ![][16]
9. <span data-ttu-id="c2f9a-149">Configure o projeto para notificações por push clicando em **云推送** (**Push da nuvem**) no painel esquerdo.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-149">Configure the project for push notifications by clicking **云推送** (**Cloud Push**) on the left pane.</span></span>
   
      ![][31]
10. <span data-ttu-id="c2f9a-150">Na página seguinte, clique no botão **推送设置** (**Configurações de push**).</span><span class="sxs-lookup"><span data-stu-id="c2f9a-150">On the next page, click the **推送设置** (**Push settings**) button.</span></span>
    
    ![][32]  
11. <span data-ttu-id="c2f9a-151">Na página de configuração, adicione o nome do pacote que você usará em seu projeto Android no campo **应用包名** (**Pacote de aplicativos**) e, em seguida, clique em **保存设置** (**Salvar**).</span><span class="sxs-lookup"><span data-stu-id="c2f9a-151">On the configuration page, add the package name that you will be using in your Android project in the **应用包名** (**Application package**) field, and then click **保存设置** (**Save**).</span></span>  
    
    ![][33]

<span data-ttu-id="c2f9a-152">Você verá a **保存成功！** Mensagem (**salva com êxito!**).</span><span class="sxs-lookup"><span data-stu-id="c2f9a-152">You see the **保存成功！** (**Successfully saved!**) message.</span></span>

## <a name="configure-your-notification-hub"></a><span data-ttu-id="c2f9a-153">Configurar seu Hub de Notificação</span><span class="sxs-lookup"><span data-stu-id="c2f9a-153">Configure your notification hub</span></span>
1. <span data-ttu-id="c2f9a-154">Entre no [Portal Clássico do Azure]e clique em **+NOVO** na parte inferior da tela.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-154">Sign in to the [Azure Classic Portal], and then click **+NEW** at the bottom of the screen.</span></span>
2. <span data-ttu-id="c2f9a-155">Clique em **Serviços de Aplicativos**, em **Barramento de Serviço**, em **Hub de Notificação** e em **Criação Rápida**.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-155">Click **App Services**, click **Service Bus**, click **Notification Hub**, and then click **Quick Create**.</span></span>
3. <span data-ttu-id="c2f9a-156">Forneça um nome para o seu **Hub de Notificação**, selecione a **Região** e o **Namespace** onde esse hub de notificação será criado e depois clique em **Criar um Novo Hub de Notificação**.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-156">Provide a name for your **Notification Hub**, select the **Region** and the **Namespace** where this notification hub will be created, and then click **Create a New Notification Hub**.</span></span>  
   
      ![][17]
4. <span data-ttu-id="c2f9a-157">Clique no namespace que você criou no hub de notificação e em **Hubs de Notificação** na parte superior.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-157">Click the namespace in which you created your notification hub, and then click **Notification Hubs** at the top.</span></span>
   
      ![][18]
5. <span data-ttu-id="c2f9a-158">Selecione o hub de notificação que você criou e clique em **Configurar** no menu superior.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-158">Select the notification hub that you created, and then click **Configure** from the top menu.</span></span>
   
      ![][19]
6. <span data-ttu-id="c2f9a-159">Role para baixo até a seção **configurações de notificação do Baidu** e insira a chave de API e a chave secreta obtidas do console do Baidu anteriormente para o seu projeto de push de nuvem do Baidu.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-159">Scroll down to the **baidu notification settings** section and enter the API key and secret key that you obtained from the Baidu console previously for your Baidu cloud push project.</span></span> <span data-ttu-id="c2f9a-160">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-160">Click **Save**.</span></span>
   
      ![][20]
7. <span data-ttu-id="c2f9a-161">Clique na guia **Painel** na parte superior do hub de notificação e depois clique em **Exibir Cadeia de Conexão**.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-161">Click the **Dashboard** tab at the top for the notification hub, and then click **View Connection String**.</span></span>
   
      ![][21]
8. <span data-ttu-id="c2f9a-162">Anote a **DefaultListenSharedAccessSignature** e a **DefaultFullSharedAccessSignature** na janela de **Informações de conexão de acesso**.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-162">Make a note of the **DefaultListenSharedAccessSignature** and **DefaultFullSharedAccessSignature** from the **Access connection information** window.</span></span>
   
    ![][22]

## <a name="connect-your-app-to-the-notification-hub"></a><span data-ttu-id="c2f9a-163">Conectar seu aplicativo ao hub de notificação</span><span class="sxs-lookup"><span data-stu-id="c2f9a-163">Connect your app to the notification hub</span></span>
1. <span data-ttu-id="c2f9a-164">No Eclipse ADT, crie um novo projeto Android (**Arquivo** > **Novo** > **Projeto de Aplicativo Android**).</span><span class="sxs-lookup"><span data-stu-id="c2f9a-164">In Eclipse ADT, create a new Android project (**File** > **New** > **Android Application Project**).</span></span>
   
    ![][23]
2. <span data-ttu-id="c2f9a-165">Insira um **Nome de Aplicativo** e verifique se a versão do **SDK Mínimo Necessário** está definida como **API 16: Android 4.1**.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-165">Enter an **Application Name** and ensure that the **Minimum Required SDK** version is set to **API 16: Android 4.1**.</span></span>
   
    ![][24]
3. <span data-ttu-id="c2f9a-166">Clique em **Avançar** e continue seguindo o assistente até que a janela **Criar Atividade** seja exibida.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-166">Click **Next** and continue following the wizard until the **Create Activity** window appears.</span></span> <span data-ttu-id="c2f9a-167">Verifique se **Atividade em branco** está selecionada e selecione **Concluir** para criar um novo Aplicativo do Android.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-167">Make sure that **Blank Activity** is selected, and finally select **Finish** to create a new Android Application.</span></span>
   
    ![][25]
4. <span data-ttu-id="c2f9a-168">Verifique se o **Destino da Compilação do Projeto** está definido corretamente.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-168">Make sure that the **Project Build Target** is set correctly.</span></span>
   
    ![][26]
5. <span data-ttu-id="c2f9a-169">Baixe o arquivo notification-hubs-0.4.jar da guia **Arquivos** do [Notification-Hubs-Android-SDK no Bintray](https://bintray.com/microsoftazuremobile/SDK/Notification-Hubs-Android-SDK/0.4).</span><span class="sxs-lookup"><span data-stu-id="c2f9a-169">Download the notification-hubs-0.4.jar file from the **Files** tab of the [Notification-Hubs-Android-SDK on Bintray](https://bintray.com/microsoftazuremobile/SDK/Notification-Hubs-Android-SDK/0.4).</span></span> <span data-ttu-id="c2f9a-170">Adicione o arquivo à pasta **libs** do seu projeto Eclipse e atualize a pasta *libs* .</span><span class="sxs-lookup"><span data-stu-id="c2f9a-170">Add the file to the **libs** folder of your Eclipse project, and refresh the *libs* folder.</span></span>
6. <span data-ttu-id="c2f9a-171">Baixe e descompacte o [SDK do Android Push Baidu], abra a pasta **libs** e copie o arquivo JAR **pushservice-x.y.z** e as pastas **armeabi** & **mips** na pasta **libs** de seu aplicativo do Android.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-171">Download and unzip the [Baidu Push Android SDK], open the **libs** folder, and then copy the **pushservice-x.y.z** jar file and the **armeabi** & **mips** folders in the **libs** folder of your Android application.</span></span>
7. <span data-ttu-id="c2f9a-172">Abra o arquivo **AndroidManifest.xml** de seu projeto do Android e adicione as permissões exigidas pelo SDK do Baidu.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-172">Open the **AndroidManifest.xml** file of your Android project and add the permissions that are required by the Baidu SDK.</span></span>
   
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
8. <span data-ttu-id="c2f9a-173">Adicione a propriedade **android:name** ao elemento **application** em **AndroidManifest.xml** substituindo *yourprojectname* (por exemplo, **com.example.BaiduTest**).</span><span class="sxs-lookup"><span data-stu-id="c2f9a-173">Add the **android:name** property to your **application** element in **AndroidManifest.xml**, replacing *yourprojectname* (for example, **com.example.BaiduTest**).</span></span> <span data-ttu-id="c2f9a-174">Verifique se esse nome de projeto corresponde ao projeto que você configurou no console do Baidu.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-174">Make sure that this project name matches the one that you configured in the Baidu console.</span></span>
   
        <application android:name="yourprojectname.DemoApplication"
9. <span data-ttu-id="c2f9a-175">Adicione a seguinte configuração dentro do elemento de aplicativo após o elemento de atividade **.MainActivity** substituindo *yourprojectname* (por exemplo, **com.example.BaiduTest**):</span><span class="sxs-lookup"><span data-stu-id="c2f9a-175">Add the following configuration within the application element after the **.MainActivity** activity element, replacing *yourprojectname* (for example, **com.example.BaiduTest**):</span></span>
   
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
10. <span data-ttu-id="c2f9a-176">Adicione uma nova classe chamada **ConfigurationSettings.java** ao projeto.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-176">Add a new class called **ConfigurationSettings.java** to the project.</span></span>
    
     ![][28]
    
     ![][29]
11. <span data-ttu-id="c2f9a-177">Adicione os seguintes códigos a ela:</span><span class="sxs-lookup"><span data-stu-id="c2f9a-177">Add the following code to it:</span></span>
    
        public class ConfigurationSettings {
                public static String API_KEY = "...";
                public static String NotificationHubName = "...";
                public static String NotificationHubConnectionString = "...";
            }
    
    <span data-ttu-id="c2f9a-178">Defina o valor de **API_KEY** com o que você recuperou do projeto de nuvem do Baidu anteriormente, **NotificationHubName** com o nome do hub de notificação do Portal Clássico do Azure e **NotificationHubConnectionString** com a DefaultListenSharedAccessSignature do Portal Clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-178">Set the value of **API_KEY** with what you retrieved from the Baidu cloud project earlier, **NotificationHubName** with your notification hub name from the Azure Classic Portal and **NotificationHubConnectionString** with DefaultListenSharedAccessSignature from the Azure Classic Portal.</span></span>
12. <span data-ttu-id="c2f9a-179">Adicione uma nova classe chamada **DemoApplication.java**e adicione o seguinte código a ela:</span><span class="sxs-lookup"><span data-stu-id="c2f9a-179">Add a new class called **DemoApplication.java**, and add the following code to it:</span></span>
    
        import com.baidu.frontia.FrontiaApplication;
    
        public class DemoApplication extends FrontiaApplication {
            @Override
            public void onCreate() {
                super.onCreate();
            }
        }
13. <span data-ttu-id="c2f9a-180">Adicione outra nova classe chamada **MyPushMessageReceiver.java**e adicione o código abaixo a ela.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-180">Add another new class called **MyPushMessageReceiver.java**, and add the following code to it.</span></span> <span data-ttu-id="c2f9a-181">É a classe que manipula as notificações por push recebidas do servidor de push do Baidu.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-181">It is the class that handles the push notifications that are received from the Baidu push server.</span></span>
    
        import java.util.List;
        import android.content.Context;
        import android.os.AsyncTask;
        import android.util.Log;
        import com.baidu.frontia.api.FrontiaPushMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub;
    
        public class MyPushMessageReceiver extends FrontiaPushMessageReceiver {
            /** TAG to Log */
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
14. <span data-ttu-id="c2f9a-182">Abra **MainActivity.java** e adicione o seguinte ao método **onCreate**:</span><span class="sxs-lookup"><span data-stu-id="c2f9a-182">Open **MainActivity.java**, and add the following to the **onCreate** method:</span></span>
    
            PushManager.startWork(getApplicationContext(),
                    PushConstants.LOGIN_TYPE_API_KEY, ConfigurationSettings.API_KEY);
15. <span data-ttu-id="c2f9a-183">Abra as seguintes instruções de importação na parte superior:</span><span class="sxs-lookup"><span data-stu-id="c2f9a-183">Open the following import statements at the top:</span></span>
    
            import com.baidu.android.pushservice.PushConstants;
            import com.baidu.android.pushservice.PushManager;

## <a name="send-notifications-to-your-app"></a><span data-ttu-id="c2f9a-184">Enviar notificações para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="c2f9a-184">Send notifications to your app</span></span>
<span data-ttu-id="c2f9a-185">Você pode testar rapidamente o recebimento de notificações em seu aplicativo ao enviar notificações no [Portal do Azure](https://portal.azure.com/) usando o botão **Enviar** no hub de notificação, como mostra a tela abaixo:</span><span class="sxs-lookup"><span data-stu-id="c2f9a-185">You can quickly test receiving notifications in your app by sending notifications in the [Azure portal](https://portal.azure.com/) using the **Send** button on the notification hub, as shown in the following screen:</span></span>

![](./media/notification-hubs-baidu-get-started/notification-hub-test-send-baidu.png)

<span data-ttu-id="c2f9a-186">Notificações por push normalmente são enviadas em um serviço de back-end como Serviços Móveis ou ASP.NET usando uma biblioteca compatível.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-186">Push notifications are normally sent in a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="c2f9a-187">Se a biblioteca não estiver disponível para seu back-end, você também poderá usar a API REST diretamente para enviar mensagens de notificação.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-187">If a library is not available for your back-end, you can use the REST API directly to send notification messages .</span></span>

<span data-ttu-id="c2f9a-188">Neste tutorial, optamos pela simplicidade e só demonstraremos os testes do aplicativo cliente enviando notificações usando o SDK do .NET para hubs de notificação em um aplicativo de console em vez de um serviço de back-end.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-188">In this tutorial, we keep it simple and just demonstrate testing your client app by sending notifications using the .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="c2f9a-189">Recomendamos o tutorial [Usar Hubs de Notificação para enviar notificações por push aos usuários](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) como a próxima etapa de envio de notificações de back-end do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-189">We recommend the [Use Notification Hubs to push notifications to users](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) tutorial as the next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="c2f9a-190">No entanto, as abordagens a seguir podem ser usadas para o envio de notificações:</span><span class="sxs-lookup"><span data-stu-id="c2f9a-190">However, the following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="c2f9a-191">**Interface REST**: você pode dar suporte à notificação em qualquer plataforma de back-end usando a [Interface REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="c2f9a-191">**REST Interface**:  You can support notification on any backend platform using  the [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="c2f9a-192">**SDK do .NET dos Hubs de Notificações do Microsoft Azure**: no Gerenciador de Pacotes do Nuget para o Visual Studio, execute [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="c2f9a-192">**Microsoft Azure Notification Hubs .NET SDK**: In the Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="c2f9a-193">**Node.js** : [Como usar os Hubs de Notificação de Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="c2f9a-193">**Node.js**: [How to use Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>
* <span data-ttu-id="c2f9a-194">**Aplicativos móveis**: para obter um exemplo de como enviar notificações de um back-end dos Aplicativos Móveis do Serviço de Aplicativo do Azure que esteja integrado com Hubs de notificação, confira [Adicionar notificação por push para seu aplicativo móvel](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="c2f9a-194">**Mobile Apps**: For an example of how to send notifications from an Azure App Service Mobile Apps backend that's integrated with Notification Hubs, see [Add push notifications to your mobile app](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span></span>
* <span data-ttu-id="c2f9a-195">**Java/PHP**: para obter um exemplo de como enviar notificações usando as APIs REST, confira "Como usar os Hubs de Notificação do Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span><span class="sxs-lookup"><span data-stu-id="c2f9a-195">**Java / PHP**: For an example of how to send notifications by using the REST APIs, see "How to use Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

## <a name="optional-send-notifications-from-a-net-console-app"></a><span data-ttu-id="c2f9a-196">(Opcional) Enviar notificações de um aplicativo de console do .NET.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-196">(Optional) Send notifications from a .NET console app.</span></span>
<span data-ttu-id="c2f9a-197">Nesta seção, vamos mostrar o envio de uma notificação usando um aplicativo de console do .NET.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-197">In this section, we show sending a notification using a .NET console app.</span></span>

1. <span data-ttu-id="c2f9a-198">Crie um novo aplicativo de console do Visual C#:</span><span class="sxs-lookup"><span data-stu-id="c2f9a-198">Create a new Visual C# console application:</span></span>
   
    ![][30]
2. <span data-ttu-id="c2f9a-199">Na janela do Console do Gerenciador de Pacotes, defina o **Projeto padrão** como o seu novo projeto de aplicativo do console e execute o seguinte comando na janela do console:</span><span class="sxs-lookup"><span data-stu-id="c2f9a-199">In the Package Manager Console window, set the **Default project** to your new console application project, and then in the console window, execute the following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="c2f9a-200">Essa instrução adiciona uma referência ao SDK dos Hubs de Notificação do Azure usando o <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">pacote NuGet Microsoft.Azure.Notification Hubs</a>.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-200">This instruction adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
3. <span data-ttu-id="c2f9a-201">Abra o arquivo **Program.cs** e adicione o seguinte usando a instrução:</span><span class="sxs-lookup"><span data-stu-id="c2f9a-201">Open the file **Program.cs** and add the following using statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
4. <span data-ttu-id="c2f9a-202">Na classe `Program`, adicione o método a seguir e substitua *DefaultFullSharedAccessSignatureSASConnectionString* e *NotificationHubName* pelos valores que você tem.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-202">In your `Program` class, add the following method and replace *DefaultFullSharedAccessSignatureSASConnectionString* and *NotificationHubName* with the values that you have.</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("DefaultFullSharedAccessSignatureSASConnectionString", "NotificationHubName");
            string message = "{\"title\":\"((Notification title))\",\"description\":\"Hello from Azure\"}";
            var result = await hub.SendBaiduNativeNotificationAsync(message);
        }
5. <span data-ttu-id="c2f9a-203">Adicione as seguintes linhas ao método **Main** :</span><span class="sxs-lookup"><span data-stu-id="c2f9a-203">Add the following lines in your **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();

## <a name="test-your-app"></a><span data-ttu-id="c2f9a-204">Testar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="c2f9a-204">Test your app</span></span>
<span data-ttu-id="c2f9a-205">Para testar este aplicativo com um telefone real, basta conectá-lo ao seu computador com um cabo USB.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-205">To test this app with an actual phone, just connect the phone to your computer by using a USB cable.</span></span> <span data-ttu-id="c2f9a-206">Essa ação carregará seu aplicativo no telefone conectado.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-206">This action loads your app onto the attached phone.</span></span>

<span data-ttu-id="c2f9a-207">Para testar este aplicativo com o emulador, na barra de ferramentas superior do Eclipse, clique em **Executar**e selecione seu aplicativo: ele inicia o emulador, carrega e executa o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-207">To test this app with the emulator, on the Eclipse top toolbar, click **Run**, and then select your app: it starts the emulator, loads, and runs the app.</span></span>

<span data-ttu-id="c2f9a-208">O aplicativo recupera 'userId' e 'channelId' do serviço de notificação por push do Baidu e é registrado no hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-208">The app retrieves the 'userId' and 'channelId' from the Baidu Push notification service and registers with the notification hub.</span></span>

<span data-ttu-id="c2f9a-209">Para enviar uma notificação de teste, você poderá usar a guia de depuração do Portal Clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-209">To send a test notification, you can use the debug tab of the Azure Classic Portal.</span></span> <span data-ttu-id="c2f9a-210">Se você criar o aplicativo de console do .NET para o Visual Studio, bastará pressionar a tecla F5 no Visual Studio para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-210">If you built the .NET console application for Visual Studio, just press the F5 key in Visual Studio to run the application.</span></span> <span data-ttu-id="c2f9a-211">O aplicativo envia uma notificação que é exibida na área superior da notificação do seu dispositivo ou emulador.</span><span class="sxs-lookup"><span data-stu-id="c2f9a-211">The application sends a notification that appears in the top notification area of your device or emulator.</span></span>

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
<span data-ttu-id="c2f9a-212">[SDK para Android de Serviços Móveis]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409</span><span class="sxs-lookup"><span data-stu-id="c2f9a-212">[Mobile Services Android SDK]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409</span></span>
<span data-ttu-id="c2f9a-213">[SDK do Android Push Baidu]: http://developer.baidu.com/wiki/index.php?title=docs/cplat/push/sdk/clientsdk</span><span class="sxs-lookup"><span data-stu-id="c2f9a-213">[Baidu Push Android SDK]: http://developer.baidu.com/wiki/index.php?title=docs/cplat/push/sdk/clientsdk</span></span>
<span data-ttu-id="c2f9a-214">[Portal Clássico do Azure]: https://manage.windowsazure.com/</span><span class="sxs-lookup"><span data-stu-id="c2f9a-214">[Azure Classic Portal]: https://manage.windowsazure.com/</span></span>
<span data-ttu-id="c2f9a-215">[portal do Baidu]: http://www.baidu.com/</span><span class="sxs-lookup"><span data-stu-id="c2f9a-215">[Baidu portal]: http://www.baidu.com/</span></span>
