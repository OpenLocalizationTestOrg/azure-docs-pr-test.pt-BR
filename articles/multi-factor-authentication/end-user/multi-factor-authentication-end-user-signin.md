---
title: "Experiência de entrada no Azure MFA com a verificação em duas etapas | Microsoft Docs"
description: "Esta página fornecerá orientações sobre onde você deve procurar os vários métodos de conexão disponíveis com o MFA do Azure."
keywords: "autenticação do usuário, experiência de conexão, conectar com telefone celular, conectar com telefone do escritório"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: b310b762-471b-4b26-887a-a321c9e81d46
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/02/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: end-user
ms.openlocfilehash: d12115be61ca00dfb86dd822ccae9f9096fa796a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="the-sign-in-experience-with-azure-multi-factor-authentication"></a><span data-ttu-id="6642b-104">A experiência de conexão com a Autenticação Multifator do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="6642b-104">The sign-in experience with Azure Multi-Factor Authentication</span></span>
> [!NOTE]
> <span data-ttu-id="6642b-105">A finalidade deste artigo é examinar uma experiência de conexão típica.</span><span class="sxs-lookup"><span data-stu-id="6642b-105">The purpose of this article is to walk through a typical sign-in experience.</span></span> <span data-ttu-id="6642b-106">Para obter ajuda com a conexão ou resolver problemas, consulte [Problemas com a Autenticação Multifator do Microsoft Azure](multi-factor-authentication-end-user-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="6642b-106">For help with signing in, or to troubleshoot problems, see [Having trouble with Azure Multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span></span>

## <a name="what-will-your-sign-in-experience-be"></a><span data-ttu-id="6642b-107">Qual será sua experiência de conexão?</span><span class="sxs-lookup"><span data-stu-id="6642b-107">What will your sign-in experience be?</span></span>
<span data-ttu-id="6642b-108">Sua experiência de conexão varia, dependendo do que você escolhe usar como o segundo fator: uma chamada telefônica, um aplicativo de autenticação ou textos.</span><span class="sxs-lookup"><span data-stu-id="6642b-108">Your sign-in experience differs depending on what you choose to use as your second factor: a phone call, an authentication app, or texts.</span></span> <span data-ttu-id="6642b-109">Escolha a opção que melhor descreve o que você está fazendo:</span><span class="sxs-lookup"><span data-stu-id="6642b-109">Choose the option that best describes what you are doing:</span></span>

| <span data-ttu-id="6642b-110">Como entrar no Azure?</span><span class="sxs-lookup"><span data-stu-id="6642b-110">How do you sign in?</span></span> | 
| --- |
| [<span data-ttu-id="6642b-111">Com uma chamada telefônica para meu telefone celular ou comercial</span><span class="sxs-lookup"><span data-stu-id="6642b-111">With a phone call to my mobile or office phone</span></span>](#signing-in-with-a-phone-call) |
| [<span data-ttu-id="6642b-112">Com um texto para meu telefone celular</span><span class="sxs-lookup"><span data-stu-id="6642b-112">With a text to my mobile phone</span></span>](#signing-in-with-a-text-message)
| [<span data-ttu-id="6642b-113">Com notificações do aplicativo Microsoft Authenticator</span><span class="sxs-lookup"><span data-stu-id="6642b-113">With notifications from the Microsoft Authenticator app</span></span>](#signing-in-with-the-microsoft-authenticator-app-using-notification) |
| [<span data-ttu-id="6642b-114">Com códigos de verificação do aplicativo Microsoft Authenticator</span><span class="sxs-lookup"><span data-stu-id="6642b-114">With verification codes from the Microsoft Authenticator app</span></span>](#signing-in-with-the-microsoft-authenticator-app-using-verification-code) |
| [<span data-ttu-id="6642b-115">Com um método alternativo, porque não consigo usar meu método preferido agora</span><span class="sxs-lookup"><span data-stu-id="6642b-115">With an alternate method, because I can't use my preferred method right now</span></span>](#signing-in-with-an-alternate-method) |

## <a name="signing-in-with-a-phone-call"></a><span data-ttu-id="6642b-116">Conectando com uma chamada telefônica</span><span class="sxs-lookup"><span data-stu-id="6642b-116">Signing in with a phone call</span></span>
<span data-ttu-id="6642b-117">As informações a seguir descrevem a experiência de verificação em duas etapas com uma chamada para seu telefone celular ou comercial.</span><span class="sxs-lookup"><span data-stu-id="6642b-117">The following information describes the two-step verification experience with a call to your mobile or office phone.</span></span>

1. <span data-ttu-id="6642b-118">Entre em um aplicativo ou serviço, como o Office 365, usando seu nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="6642b-118">Sign in to an application or service such as Office 365 using your username and password.</span></span>  
2. <span data-ttu-id="6642b-119">A Microsoft liga para você.</span><span class="sxs-lookup"><span data-stu-id="6642b-119">Microsoft calls you.</span></span>  
3. <span data-ttu-id="6642b-120">Atenda o telefone e pressione a tecla #.</span><span class="sxs-lookup"><span data-stu-id="6642b-120">Answer the phone and hit the # key.</span></span>  

## <a name="signing-in-with-a-text-message"></a><span data-ttu-id="6642b-121">Conectando com uma mensagem de texto</span><span class="sxs-lookup"><span data-stu-id="6642b-121">Signing in with a text message</span></span>
<span data-ttu-id="6642b-122">As seguintes informações descrevem a experiência de verificação em duas etapas com uma mensagem de texto para seu telefone celular:</span><span class="sxs-lookup"><span data-stu-id="6642b-122">The following information describes the two-step verification experience with a text message to your mobile phone:</span></span>

1. <span data-ttu-id="6642b-123">Entre em um aplicativo ou serviço, como o Office 365, usando seu nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="6642b-123">Sign in to an application or service such as Office 365 using your username and password.</span></span> 
2. <span data-ttu-id="6642b-124">A Microsoft envia para você uma mensagem de texto com um código numérico.</span><span class="sxs-lookup"><span data-stu-id="6642b-124">Microsoft sends you a text message that contains a number code.</span></span> 
3. <span data-ttu-id="6642b-125">Insira o código na caixa fornecida na página de conexão.</span><span class="sxs-lookup"><span data-stu-id="6642b-125">Enter the code in the box provided on the sign-in page.</span></span> 

## <a name="signing-in-with-the-microsoft-authenticator-app"></a><span data-ttu-id="6642b-126">Entrando com o aplicativo Microsoft Authenticator</span><span class="sxs-lookup"><span data-stu-id="6642b-126">Signing in with the Microsoft Authenticator app</span></span> 
<span data-ttu-id="6642b-127">As informações a seguir descrevem a experiência do uso do aplicativo Microsoft Authenticator para verificações em duas etapas.</span><span class="sxs-lookup"><span data-stu-id="6642b-127">The following information describes the experience of using the Microsoft Authenticator app for two-step verifications.</span></span> <span data-ttu-id="6642b-128">Há duas maneiras diferentes de usar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6642b-128">There are two different ways to use the app.</span></span> <span data-ttu-id="6642b-129">Você pode receber notificações por push no seu dispositivo ou abrir o aplicativo para obter um código de verificação.</span><span class="sxs-lookup"><span data-stu-id="6642b-129">You can receive push notifications on your device, or you can open the app to get a verification code.</span></span>

### <a name="to-sign-in-with-a-notification-from-the-microsoft-authenticator-app"></a><span data-ttu-id="6642b-130">Para entrar com uma notificação enviada pelo aplicativo Microsoft Authenticator</span><span class="sxs-lookup"><span data-stu-id="6642b-130">To sign in with a notification from the Microsoft Authenticator app</span></span>
1. <span data-ttu-id="6642b-131">Entre em um aplicativo ou serviço, como o Office 365, usando seu nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="6642b-131">Sign in to an application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="6642b-132">A Microsoft envia uma notificação ao aplicativo Microsoft Authenticator no seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6642b-132">Microsoft sends a notification to the Microsoft Authenticator app on your device.</span></span>

  ![A Microsoft envia notificação](./media/multi-factor-authentication-end-user-signin/notify.png)

3. <span data-ttu-id="6642b-134">Abra a notificação no seu telefone e selecione a opção **Verificar**.</span><span class="sxs-lookup"><span data-stu-id="6642b-134">Open the notification on your phone and select the **Verify** key.</span></span> <span data-ttu-id="6642b-135">Se sua empresa exigir um PIN, digite-o aqui.</span><span class="sxs-lookup"><span data-stu-id="6642b-135">If your company requires a PIN, enter it here.</span></span>
4. <span data-ttu-id="6642b-136">Agora você deve estar conectado.</span><span class="sxs-lookup"><span data-stu-id="6642b-136">You should now be signed in.</span></span>

### <a name="to-sign-in-using-a-verification-code-with-the-microsoft-authenticator-app"></a><span data-ttu-id="6642b-137">Para entrar usando um código de verificação com o aplicativo Microsoft Authenticator</span><span class="sxs-lookup"><span data-stu-id="6642b-137">To sign in using a verification code with the Microsoft Authenticator app</span></span>

<span data-ttu-id="6642b-138">Se você usar o aplicativo Microsoft Authenticator para obter códigos de verificação, ao abrir o aplicativo, você verá um número sob o nome de sua conta.</span><span class="sxs-lookup"><span data-stu-id="6642b-138">If you use the Microsoft Authenticator app to get verification codes, then when you open the app you see a number under your account name.</span></span> <span data-ttu-id="6642b-139">Ele muda a cada 30 segundos, para que não seja usado duas vezes.</span><span class="sxs-lookup"><span data-stu-id="6642b-139">This number changes every 30 seconds so that you don't use the same number twice.</span></span> <span data-ttu-id="6642b-140">Quando tiver de informar o código de verificação, abra o aplicativo e use o número que aparecer na tela.</span><span class="sxs-lookup"><span data-stu-id="6642b-140">When you're asked for a verification code, open the app and use whatever number is currently displayed.</span></span> 

1. <span data-ttu-id="6642b-141">Entre em um aplicativo ou serviço, como o Office 365, usando seu nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="6642b-141">Sign in to an application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="6642b-142">A Microsoft solicita que você insira um código de verificação.</span><span class="sxs-lookup"><span data-stu-id="6642b-142">Microsoft prompts you for a verification code.</span></span>

  ![Inserir código de verificação](./media/multi-factor-authentication-end-user-signin/verify3.png)

3. <span data-ttu-id="6642b-144">Abra o aplicativo Microsoft Authenticator em seu telefone e digite o código na caixa de conexão.</span><span class="sxs-lookup"><span data-stu-id="6642b-144">Open the Microsoft Authenticator app on your phone and enter the code in the box where you are signing in.</span></span>

## <a name="signing-in-with-an-alternate-method"></a><span data-ttu-id="6642b-145">Conectando-se com um método alternativo</span><span class="sxs-lookup"><span data-stu-id="6642b-145">Signing in with an alternate method</span></span>
<span data-ttu-id="6642b-146">Às vezes, pode ser que o telefone ou dispositivo que você tem não seja o seu método de verificação de preferência.</span><span class="sxs-lookup"><span data-stu-id="6642b-146">Sometimes you don't have the phone or device that you set up as your preferred verification method.</span></span> <span data-ttu-id="6642b-147">É por isso que recomendamos que faça o backup da conta.</span><span class="sxs-lookup"><span data-stu-id="6642b-147">This situation is why we recommend that you set up backup methods for your account.</span></span> <span data-ttu-id="6642b-148">A seção a seguir mostra como se conectar com um método alternativo quando o método primário não está disponível.</span><span class="sxs-lookup"><span data-stu-id="6642b-148">The following section shows you how to sign in with an alternate method when your primary method may not be available.</span></span>

1. <span data-ttu-id="6642b-149">Entre em um aplicativo ou serviço, como o Office 365, usando seu nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="6642b-149">Sign in to an application or service such as Office 365 using your username and password.</span></span>
2. <span data-ttu-id="6642b-150">Selecione **Usar uma opção de verificação diferente**.</span><span class="sxs-lookup"><span data-stu-id="6642b-150">Select **Use a different verification option**.</span></span> <span data-ttu-id="6642b-151">Você verá opções de verificação diferentes, de acordo com a quantidade configurada.</span><span class="sxs-lookup"><span data-stu-id="6642b-151">You see different verification options based on how many you have setup.</span></span>
3. <span data-ttu-id="6642b-152">Escolha um método alternativo e conecte-se.</span><span class="sxs-lookup"><span data-stu-id="6642b-152">Choose an alternate method and sign in.</span></span>

  ![Usar método alternativo](./media/multi-factor-authentication-end-user-signin/alt.png)

## <a name="next-steps"></a><span data-ttu-id="6642b-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6642b-154">Next steps</span></span>

<span data-ttu-id="6642b-155">Se você tiver problemas para entrar usando a verificação em duas etapas, consulte [Problemas com a Autenticação Multifator do Microsoft Azure](multi-factor-authentication-end-user-troubleshoot.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="6642b-155">If you have problems signing in with two-step verification, get more information at [Having trouble with Azure Multi-Factor Authentication](multi-factor-authentication-end-user-troubleshoot.md).</span></span>

<span data-ttu-id="6642b-156">Aprenda a [Gerenciar suas configurações de verificação em duas etapas](multi-factor-authentication-end-user-manage-settings.md).</span><span class="sxs-lookup"><span data-stu-id="6642b-156">Learn how to [Manage your two-step verification settings](multi-factor-authentication-end-user-manage-settings.md).</span></span>

<span data-ttu-id="6642b-157">Descubra como [Começar a usar o aplicativo Microsoft Authenticator](microsoft-authenticator-app-how-to.md) para poder entrar usando notificações, em vez de textos e chamadas telefônicas.</span><span class="sxs-lookup"><span data-stu-id="6642b-157">Find out how to [Get started with the Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) so that you can use notifications to sign in, instead of texts and phone calls.</span></span> 