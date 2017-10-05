---
title: Aplicativo Microsoft Authenticator para telefones celulares | Microsoft Docs
description: "Saiba como atualizar para a versão mais recente do Azure Authenticator."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 3065a1ee-f253-41f0-a68d-2bd84af5ffba
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: kgremban
ms.reviewer: librown
ms.custom: H1Hack27Feb2017, end-user
ms.openlocfilehash: 6bcb6d9f7a1e9b241fa70690016b03d6eb5887ab
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-the-microsoft-authenticator-app"></a><span data-ttu-id="19917-103">Introdução ao aplicativo Microsoft Authenticator</span><span class="sxs-lookup"><span data-stu-id="19917-103">Get started with the Microsoft Authenticator app</span></span>
<span data-ttu-id="19917-104">O aplicativo Microsoft Authenticator fornece um nível adicional de segurança em sua conta corporativa ou de estudante (por exemplo, bsimon@contoso.com) ou conta da Microsoft (por exemplo, bsimon@outlook.com).</span><span class="sxs-lookup"><span data-stu-id="19917-104">The Microsoft Authenticator app provides an additional level of security in your work or school account (for example, bsimon@contoso.com) or your Microsoft account (for example, bsimon@outlook.com).</span></span>

<span data-ttu-id="19917-105">O aplicativo funciona de uma das duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="19917-105">The app works in one of two ways:</span></span>

* <span data-ttu-id="19917-106">**Notificação**.</span><span class="sxs-lookup"><span data-stu-id="19917-106">**Notification**.</span></span> <span data-ttu-id="19917-107">O aplicativo pode ajudar a evitar o acesso não autorizado a contas e interromper transações fraudulentas enviando uma notificação para seu smartphone ou tablet.</span><span class="sxs-lookup"><span data-stu-id="19917-107">The app can help prevent unauthorized access to accounts and stop fraudulent transactions by pushing a notification to your smartphone or tablet.</span></span> <span data-ttu-id="19917-108">Basta ver a notificação e se ela for legítima, selecione **Verificar**.</span><span class="sxs-lookup"><span data-stu-id="19917-108">Simply view the notification, and if it's legitimate, select **Verify**.</span></span> <span data-ttu-id="19917-109">Caso contrário, você pode selecionar **Negar**.</span><span class="sxs-lookup"><span data-stu-id="19917-109">Otherwise, you can select **Deny**.</span></span> 
* <span data-ttu-id="19917-110">**Código de verificação**.</span><span class="sxs-lookup"><span data-stu-id="19917-110">**Verification code**.</span></span> <span data-ttu-id="19917-111">O aplicativo pode ser usado como um token de software para gerar um código de verificação OAuth.</span><span class="sxs-lookup"><span data-stu-id="19917-111">The app can be used as a software token to generate an OAuth verification code.</span></span> <span data-ttu-id="19917-112">Depois de inserir o nome de usuário e senha, insira o código fornecido pelo aplicativo na tela de entrada.</span><span class="sxs-lookup"><span data-stu-id="19917-112">After you enter your username and password, you enter the code provided by the app into the sign-in screen.</span></span> <span data-ttu-id="19917-113">O código de verificação oferece uma segunda forma de autenticação.</span><span class="sxs-lookup"><span data-stu-id="19917-113">The verification code provides a second form of authentication.</span></span>

<span data-ttu-id="19917-114">O aplicativo Microsoft Authenticator substitui o aplicativo Azure Authenticator.</span><span class="sxs-lookup"><span data-stu-id="19917-114">The Microsoft Authenticator app replaces the Azure Authenticator app.</span></span> <span data-ttu-id="19917-115">O aplicativo Azure Authenticator ainda está funcionando, mas se você decidir ir para o novo aplicativo Microsoft Authenticator, este artigo poderá ajudar.</span><span class="sxs-lookup"><span data-stu-id="19917-115">The Azure Authenticator app still works, but if you decide to move to the new Microsoft Authenticator app, this article can assist you.</span></span>  

## <a name="opt-in-for-two-step-verification"></a><span data-ttu-id="19917-116">Aceitar a verificação em duas etapas</span><span class="sxs-lookup"><span data-stu-id="19917-116">Opt in for two-step verification</span></span>

<span data-ttu-id="19917-117">O aplicativo Microsoft Authenticator não funciona por si só.</span><span class="sxs-lookup"><span data-stu-id="19917-117">The Microsoft Authenticator app doesn't work by itself.</span></span> <span data-ttu-id="19917-118">Configure cada uma das suas contas para solicitarem a você um segundo método de verificação após você entrar com seu nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="19917-118">Configure each of your accounts to prompt you for a second verification method after you sign in with your username and password.</span></span> 

<span data-ttu-id="19917-119">Para uma conta corporativa ou de estudante, geralmente você não pode escolher esse recurso.</span><span class="sxs-lookup"><span data-stu-id="19917-119">For a work or school account, you don't usually get to choose this feature for yourself.</span></span> <span data-ttu-id="19917-120">Em vez disso, um administrador de segurança aceita em seu nome e o notifica para registrar os métodos de verificação para sua conta.</span><span class="sxs-lookup"><span data-stu-id="19917-120">Instead, a security administrator opts in on your behalf and then notifies you to register verification methods for your account.</span></span> <span data-ttu-id="19917-121">Se esta situação se aplica a você, saiba mais em [A Autenticação Multifator do Azure significa para mim](multi-factor-authentication-end-user.md).</span><span class="sxs-lookup"><span data-stu-id="19917-121">If this scenario applies to you, learn more in [What does Azure Multi-Factor Authentication mean for me](multi-factor-authentication-end-user.md).</span></span>

<span data-ttu-id="19917-122">Para uma conta pessoal, você precisa configurar a verificação em duas etapas por conta própria.</span><span class="sxs-lookup"><span data-stu-id="19917-122">For a personal account, you need to set up two-step verification for yourself.</span></span> <span data-ttu-id="19917-123">Se você tem uma conta da Microsoft, essas etapas estão disponíveis em [Sobre a verificação em duas etapas](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification).</span><span class="sxs-lookup"><span data-stu-id="19917-123">If you have a Microsoft account, those steps are available in [About two-step verification](https://support.microsoft.com/help/12408/microsoft-account-about-two-step-verification).</span></span> 

<span data-ttu-id="19917-124">Você também pode usar o Microsoft Authenticator com contas não Microsoft.</span><span class="sxs-lookup"><span data-stu-id="19917-124">You can also use the Microsoft Authenticator with non-Microsoft accounts.</span></span> <span data-ttu-id="19917-125">Eles podem chamar o recurso de algo diferente de verificação em duas etapas, mas você poderá encontrá-lo nas configurações de segurança ou de conexão.</span><span class="sxs-lookup"><span data-stu-id="19917-125">They may call the feature something other than two-step verification, but you should be able to find it under security or sign-in settings.</span></span> 

## <a name="install-the-app"></a><span data-ttu-id="19917-126">Instalar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="19917-126">Install the app</span></span>
<span data-ttu-id="19917-127">O aplicativo Microsoft Authenticator está disponível para [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072) e [iOS](http://go.microsoft.com/fwlink/?Linkid=825073).</span><span class="sxs-lookup"><span data-stu-id="19917-127">The Microsoft Authenticator app is available for [Windows Phone](http://go.microsoft.com/fwlink/?Linkid=825071), [Android](http://go.microsoft.com/fwlink/?Linkid=825072), and [iOS](http://go.microsoft.com/fwlink/?Linkid=825073).</span></span>

## <a name="add-accounts-to-the-app"></a><span data-ttu-id="19917-128">Adicionar contas ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="19917-128">Add accounts to the app</span></span>
<span data-ttu-id="19917-129">Para cada conta que você deseja adicionar ao aplicativo Microsoft Authenticator, use um destes procedimentos:</span><span class="sxs-lookup"><span data-stu-id="19917-129">For each account that you want to add to the Microsoft Authenticator app, use one of the following procedures:</span></span>

### <a name="add-a-personal-microsoft-account-to-the-app"></a><span data-ttu-id="19917-130">Adicionar uma conta pessoal da Microsoft ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="19917-130">Add a personal Microsoft account to the app</span></span>

<span data-ttu-id="19917-131">Para ter uma conta pessoal da Microsoft (aquela que você usa para entrar no Outlook.com, Xbox, Skype etc.), basta entrar em sua conta no aplicativo Microsoft Authenticator.</span><span class="sxs-lookup"><span data-stu-id="19917-131">For a personal Microsoft account (one that you use to sign in to Outlook.com, Xbox, Skype, etc.), all you have to do is sign in to your account in the Microsoft Authenticator app.</span></span>

### <a name="add-a-work-or-school-account-to-the-app-using-the-qr-code-scanner"></a><span data-ttu-id="19917-132">Adicionar uma conta corporativa ou de estudante ao aplicativo usando o scanner de código QR</span><span class="sxs-lookup"><span data-stu-id="19917-132">Add a work or school account to the app using the QR code scanner</span></span>
1. <span data-ttu-id="19917-133">Vá para a tela de configurações da verificação de segurança.</span><span class="sxs-lookup"><span data-stu-id="19917-133">Go to the security verification settings screen.</span></span>  <span data-ttu-id="19917-134">Para obter mais informações sobre como acessar essa tela, consulte [Alterando as configurações de segurança](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page).</span><span class="sxs-lookup"><span data-stu-id="19917-134">For information on how to get to this screen, see [Changing your security settings](multi-factor-authentication-end-user-manage-settings.md#where-to-find-the-settings-page).</span></span>
2. <span data-ttu-id="19917-135">Marque a caixa ao lado de **Aplicativo autenticador** e selecione **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="19917-135">Check the box next to **Authenticator app** then select **Configure**.</span></span>

    ![Botão Configurar na tela de configurações da verificação de segurança](./media/authenticator-app-how-to/azureauthe.png)

    <span data-ttu-id="19917-137">Isso abre uma tela com um código QR.</span><span class="sxs-lookup"><span data-stu-id="19917-137">This brings up a screen with a QR code on it.</span></span>

    ![Tela que fornece o código QR](./media/authenticator-app-how-to/barcode2.png)
3. <span data-ttu-id="19917-139">Abra o aplicativo Microsoft Authenticator.</span><span class="sxs-lookup"><span data-stu-id="19917-139">Open the Microsoft Authenticator app.</span></span> <span data-ttu-id="19917-140">Na tela de **contas**, selecione **+**, em seguida, especifique que você deseja adicionar uma conta corporativa ou de estudante.</span><span class="sxs-lookup"><span data-stu-id="19917-140">On the **accounts** screen, select **+**, and then specify that you want to add a work or school account.</span></span>
4. <span data-ttu-id="19917-141">Use a câmera para verificar o código QR e selecione **Concluído** para fechar a tela do código QR.</span><span class="sxs-lookup"><span data-stu-id="19917-141">Use the camera to scan the QR code, and then select **Done** to close the QR code screen.</span></span>

    <span data-ttu-id="19917-142">Se a câmera não estiver funcionando corretamente, [insira o código QR e a URL manualmente](#add-an-account-to-the-app-manually).</span><span class="sxs-lookup"><span data-stu-id="19917-142">If your camera is not working properly, you can [enter the QR code and URL manually](#add-an-account-to-the-app-manually).</span></span>

5. <span data-ttu-id="19917-143">Quando o aplicativo mostrar o nome de sua conta com um código de seis dígitos abaixo dela, você terá concluído.</span><span class="sxs-lookup"><span data-stu-id="19917-143">When the app shows your account name with a six-digit code underneath it, you're done.</span></span> 

    ![Tela de contas](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-to-the-app-manually"></a><span data-ttu-id="19917-145">Adicionar manualmente uma conta ao aplicativo</span><span class="sxs-lookup"><span data-stu-id="19917-145">Add an account to the app manually</span></span>
1. <span data-ttu-id="19917-146">Vá para a tela de configurações da verificação de segurança.</span><span class="sxs-lookup"><span data-stu-id="19917-146">Go to the security verification settings screen.</span></span>  <span data-ttu-id="19917-147">Para obter mais informações sobre como acessar essa tela, consulte [Alterando as configurações de segurança](multi-factor-authentication-end-user-manage-settings.md).</span><span class="sxs-lookup"><span data-stu-id="19917-147">For information on how to get to this screen, see [Changing your security settings](multi-factor-authentication-end-user-manage-settings.md).</span></span>
2. <span data-ttu-id="19917-148">Selecione **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="19917-148">Select **Configure**.</span></span>

    ![Botão Configurar na tela de configurações da verificação de segurança](./media/authenticator-app-how-to/azureauthe.png)

    <span data-ttu-id="19917-150">Isso abre uma tela com um código QR.</span><span class="sxs-lookup"><span data-stu-id="19917-150">This brings up a screen with a QR code on it.</span></span>  <span data-ttu-id="19917-151">Observe o código e a URL.</span><span class="sxs-lookup"><span data-stu-id="19917-151">Note the code and URL.</span></span>

    ![Tela que fornece o código QR e a URL](./media/authenticator-app-how-to/barcode2.png)
3. <span data-ttu-id="19917-153">Abra o aplicativo Microsoft Authenticator.</span><span class="sxs-lookup"><span data-stu-id="19917-153">Open the Microsoft Authenticator app.</span></span> <span data-ttu-id="19917-154">Na tela de **contas**, selecione **+**, em seguida, especifique que você deseja adicionar uma conta corporativa ou de estudante.</span><span class="sxs-lookup"><span data-stu-id="19917-154">On the **accounts** screen, select **+**, and then specify that you want to add a work or school account.</span></span>

4. <span data-ttu-id="19917-155">No scanner, selecione **inserir o código manualmente**.</span><span class="sxs-lookup"><span data-stu-id="19917-155">In the scanner, select **enter code manually**.</span></span>

    ![Tela para verificar um código QR](./media/multi-factor-authentication-end-user-first-time/scan2.png)
5. <span data-ttu-id="19917-157">Insira o código e a URL nas caixas apropriadas no aplicativo e selecione **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="19917-157">Enter the code and the URL in the appropriate boxes in the app, then select **Finish**.</span></span>

    ![Tela para inserir código e a URL](./media/authenticator-app-how-to/manual.png)

6. <span data-ttu-id="19917-159">Quando o aplicativo mostrar o nome de sua conta com um código de seis dígitos abaixo dela, você terá concluído.</span><span class="sxs-lookup"><span data-stu-id="19917-159">When the app shows your account name with a six-digit code underneath it, you're done.</span></span>

    ![Tela de contas](./media/authenticator-app-how-to/accounts.png)

### <a name="add-an-account-to-the-app-using-touch-id"></a><span data-ttu-id="19917-161">Adicionar uma conta ao aplicativo usando o Touch ID</span><span class="sxs-lookup"><span data-stu-id="19917-161">Add an account to the app using Touch ID</span></span>
<span data-ttu-id="19917-162">O aplicativo Microsoft Authenticator no iOS dá suporte ao Touch ID.</span><span class="sxs-lookup"><span data-stu-id="19917-162">The Microsoft Authenticator app on iOS supports Touch ID.</span></span>  <span data-ttu-id="19917-163">A Autenticação Multifator do Azure permite que as organizações exijam um PIN para os dispositivos.</span><span class="sxs-lookup"><span data-stu-id="19917-163">Azure Multi-Factor Authentication allows organizations to require a PIN for devices.</span></span> <span data-ttu-id="19917-164">Com o Touch ID, os usuários do iOS não precisam inserir um PIN.</span><span class="sxs-lookup"><span data-stu-id="19917-164">With Touch ID, iOS users don’t need to enter a PIN.</span></span> <span data-ttu-id="19917-165">Em vez disso, eles podem digitalizar sua impressão digital e selecionar **Aprovar**.</span><span class="sxs-lookup"><span data-stu-id="19917-165">Instead, they can scan their fingerprint and select **Approve**.</span></span>

<span data-ttu-id="19917-166">A configuração do Touch ID com o Microsoft Authenticator é simples.</span><span class="sxs-lookup"><span data-stu-id="19917-166">Setting up Touch ID with Microsoft Authenticator is simple.</span></span> <span data-ttu-id="19917-167">Você conclui um desafio de verificação normal com um PIN.</span><span class="sxs-lookup"><span data-stu-id="19917-167">You complete a normal verification challenge with a PIN.</span></span> <span data-ttu-id="19917-168">Se seu dispositivo der suporte ao o Touch ID, o Microsoft Authenticator irá configurá-lo automaticamente para essa conta.</span><span class="sxs-lookup"><span data-stu-id="19917-168">If your device supports Touch ID, Microsoft Authenticator sets it up automatically for that account.</span></span>

![Verificação da configuração do Touch ID](./media/authenticator-app-how-to/touchid1.png)

<span data-ttu-id="19917-170">Desse ponto em diante, quando você precisar verificar sua entrada, selecionará a notificação por push recebida e digitalizará sua impressão digital em vez de inserir seu PIN.</span><span class="sxs-lookup"><span data-stu-id="19917-170">From that point forward, when you're required to verify your sign-in, you select the received push notification and scan your fingerprint instead of entering your PIN.</span></span>

![Notificação por push](./media/authenticator-app-how-to/touchid2.png)

## <a name="use-the-app-when-you-sign-in"></a><span data-ttu-id="19917-172">Usar o aplicativo ao entrar</span><span class="sxs-lookup"><span data-stu-id="19917-172">Use the app when you sign in</span></span>

<span data-ttu-id="19917-173">Depois que sua conta for adicionada ao aplicativo, você precisará fazer uma verificação de teste para verificar se tudo foi configurado corretamente.</span><span class="sxs-lookup"><span data-stu-id="19917-173">Once your account is added to the app, you may be prompted to do a test verification to make sure everything was configured correctly.</span></span> <span data-ttu-id="19917-174">Depois disso, você terminou!</span><span class="sxs-lookup"><span data-stu-id="19917-174">After that, you're done!</span></span> <span data-ttu-id="19917-175">Você não precisa fazer mais nada até a próxima vez que entrar.</span><span class="sxs-lookup"><span data-stu-id="19917-175">You don't need to do anything else until the next time you sign in.</span></span>

<span data-ttu-id="19917-176">Se você optar por usar códigos de verificação no aplicativo, começará a vê-los na home page.</span><span class="sxs-lookup"><span data-stu-id="19917-176">If you chose to use verification codes in the app, you start to see them on the home page.</span></span> <span data-ttu-id="19917-177">Eles são alterados a cada 30 segundos para que você sempre tenha um novo código quando precisar de um.</span><span class="sxs-lookup"><span data-stu-id="19917-177">They change every 30 seconds so that you always have a new code when you need one.</span></span> <span data-ttu-id="19917-178">Mas você não precisa fazer nada com eles até que você entre e seja solicitado que você insira um código de verificação.</span><span class="sxs-lookup"><span data-stu-id="19917-178">But you don't need to do anything with them until you sign in and are prompted to enter a verification code.</span></span>  