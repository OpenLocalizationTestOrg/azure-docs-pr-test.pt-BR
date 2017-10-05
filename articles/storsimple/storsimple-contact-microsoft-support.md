---
title: "Registrar tíquete de suporte para o StorSimple série 8000 | Microsoft Docs"
description: "Saiba como criar uma solicitação de suporte e iniciar uma sessão de suporte em seu dispositivo StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 2ebc20fe-f490-4749-8e43-c9fac86f1676
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/27/2017
ms.author: alkohli;anbacker
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cecc2566b432e897b5eff0c12e66598f0518ed80
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="contact-microsoft-support-for-your-storsimple"></a><span data-ttu-id="87685-103">Contate o Suporte da Microsoft para obter ajuda com seu StorSimple</span><span class="sxs-lookup"><span data-stu-id="87685-103">Contact Microsoft Support for your StorSimple</span></span>
<span data-ttu-id="87685-104">Se tiver problemas com sua solução Microsoft Azure StorSimple, você poderá criar uma solicitação de serviço de suporte técnico.</span><span class="sxs-lookup"><span data-stu-id="87685-104">If you encounter any issues with your Microsoft Azure StorSimple solution, you can create a service request for technical support.</span></span> <span data-ttu-id="87685-105">Em uma sessão online com seu engenheiro de suporte, talvez você precise iniciar uma sessão de suporte em seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="87685-105">In an online session with your support engineer, you may also need to start a support session on your StorSimple device.</span></span> <span data-ttu-id="87685-106">Este artigo orienta você sobre:</span><span class="sxs-lookup"><span data-stu-id="87685-106">This article walks you through:</span></span>

* <span data-ttu-id="87685-107">Como criar uma solicitação de suporte.</span><span class="sxs-lookup"><span data-stu-id="87685-107">How to create a support request.</span></span>
* <span data-ttu-id="87685-108">Como iniciar uma sessão de suporte na interface do Windows PowerShell de seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="87685-108">How to start a support session in the Windows PowerShell interface of your StorSimple device.</span></span>

<span data-ttu-id="87685-109">Examine os [SLAs e informações de suporte ao StorSimple 8000 Series](https://msdn.microsoft.com/library/mt433077.aspx) antes de criar uma solicitação de suporte.</span><span class="sxs-lookup"><span data-stu-id="87685-109">Review the [StorSimple 8000 Series Support SLAs and information](https://msdn.microsoft.com/library/mt433077.aspx) before you create a Support request.</span></span>

## <a name="create-a-support-request"></a><span data-ttu-id="87685-110">Criar uma solicitação de suporte</span><span class="sxs-lookup"><span data-stu-id="87685-110">Create a support request</span></span>
<span data-ttu-id="87685-111">Execute as seguintes etapas para criar uma solicitação de suporte:</span><span class="sxs-lookup"><span data-stu-id="87685-111">Perform the following steps to create a support request:</span></span>

#### <a name="to-create-a-support-request"></a><span data-ttu-id="87685-112">Para criar uma solicitação de suporte</span><span class="sxs-lookup"><span data-stu-id="87685-112">To create a support request</span></span>
1. <span data-ttu-id="87685-113">No [Portal Clássico do Azure](https://manage.windowsazure.com/), no canto superior direito, clique no nome da sua conta e em **Contatar o Suporte da Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="87685-113">In the [Azure classic portal](https://manage.windowsazure.com/), in the upper right corner, click your account name and then click **Contact Microsoft Support**.</span></span>
   
    ![Contate o Suporte da MS por meio do Portal de Gerenciamento](./media/storsimple-contact-microsoft-support/Ibiza1.png)
2. <span data-ttu-id="87685-115">Você será redirecionado para o novo portal do Azure (portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="87685-115">You will be redirected to the new Azure portal (portal.azure.com).</span></span> <span data-ttu-id="87685-116">Clique no bloco **Nova solicitação de suporte** .</span><span class="sxs-lookup"><span data-stu-id="87685-116">Click the **New support request** tile.</span></span>
   
    ![Contate o Suporte da MS por meio do novo portal](./media/storsimple-contact-microsoft-support/Ibiza2.png)
   
    <span data-ttu-id="87685-118">No lado direito da tela, é exibido o painel **Nova solicitação de suporte** .</span><span class="sxs-lookup"><span data-stu-id="87685-118">On the right side of the screen, the **New support request** pane appears.</span></span> 
   
    ![Painel de nova solicitação de suporte](./media/storsimple-contact-microsoft-support/Ibiza3a.png)
3. <span data-ttu-id="87685-120">Na caixa de diálogo **Fundamentos** , preencha o seguinte:</span><span class="sxs-lookup"><span data-stu-id="87685-120">In the **Basics** dialog box, complete the following:</span></span>                                
   
   1. <span data-ttu-id="87685-121">Na lista suspensa **Tipo de problema**, selecione **Técnico**.</span><span class="sxs-lookup"><span data-stu-id="87685-121">From the **Issue type** drop-down list , select **Technical**.</span></span>
   2. <span data-ttu-id="87685-122">Selecione uma **Assinatura** na lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="87685-122">Select a **Subscription** from the drop-down list.</span></span>
   3. <span data-ttu-id="87685-123">Na lista suspensa **Serviço**, selecione o **StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="87685-123">From the **Service** drop-down list, select **StorSimple**.</span></span> 
   4. <span data-ttu-id="87685-124">Selecione um **Plano de suporte** na lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="87685-124">Select a **Support plan** from the drop-down list.</span></span> <span data-ttu-id="87685-125">É necessário um plano de suporte pago para habilitar o Suporte Técnico.</span><span class="sxs-lookup"><span data-stu-id="87685-125">You need a paid support plan to enable Technical Support.</span></span>
4. <span data-ttu-id="87685-126">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="87685-126">Click **Next**.</span></span> <span data-ttu-id="87685-127">A caixa de diálogo **Problema** é exibida.</span><span class="sxs-lookup"><span data-stu-id="87685-127">The **Problem** dialog box appears.</span></span>
   
    ![Painel de nova solicitação de suporte](./media/storsimple-contact-microsoft-support/Ibiza5a.png) 
5. <span data-ttu-id="87685-129">Na caixa de diálogo **Problema** , preencha o seguinte:</span><span class="sxs-lookup"><span data-stu-id="87685-129">In the **Problem** dialog box, complete the following:</span></span>
   
   1. <span data-ttu-id="87685-130">Selecione um nível de **Severidade** na lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="87685-130">Select a **Severity** level from the drop-down list.</span></span>
   2. <span data-ttu-id="87685-131">Selecione um **Tipo de problema** na lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="87685-131">Select a **Problem type** from the drop-down list.</span></span>
   3. <span data-ttu-id="87685-132">Selecione uma **Categoria** na lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="87685-132">Select a **Category** from the drop-down list.</span></span> 
   4. <span data-ttu-id="87685-133">Descreva seu problema brevemente na caixa **Detalhes** .</span><span class="sxs-lookup"><span data-stu-id="87685-133">In the **Details** box, briefly describe your issue.</span></span>
   5. <span data-ttu-id="87685-134">Na caixa **Período** , indique a data, hora e fuso horário correspondentes à ocorrência mais recente do seu problema.</span><span class="sxs-lookup"><span data-stu-id="87685-134">In the **Time frame** box, indicate the date, time, and time zone that corresponds to the most recent occurrence of your issue.</span></span>
   6. <span data-ttu-id="87685-135">Em **Upload do arquivo**, clique no ícone de pasta para procurar o pacote de suporte.</span><span class="sxs-lookup"><span data-stu-id="87685-135">Under **File upload**, click the folder icon to browse to your support package.</span></span>
   7. <span data-ttu-id="87685-136">Marque a caixa de seleção **Compartilhar informações de diagnóstico** .</span><span class="sxs-lookup"><span data-stu-id="87685-136">Select the **Share diagnostic information** check box.</span></span>
6. <span data-ttu-id="87685-137">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="87685-137">Click **Next**.</span></span> <span data-ttu-id="87685-138">A caixa de diálogo das **Informações de contato** é exibida.</span><span class="sxs-lookup"><span data-stu-id="87685-138">The **Contact information** dialog box appears.</span></span>
   
    ![Painel de nova solicitação de suporte](./media/storsimple-contact-microsoft-support/Ibiza6a.png) 
7. <span data-ttu-id="87685-140">Insira suas informações de contato e selecione um método de contato (telefone ou email).</span><span class="sxs-lookup"><span data-stu-id="87685-140">Enter your contact information and select a contact method (phone or email).</span></span> 
8. <span data-ttu-id="87685-141">Marque a caixa de seleção **Salvar alterações de contato para futuras solicitações de suporte** .</span><span class="sxs-lookup"><span data-stu-id="87685-141">Select the **Save contact changes for future support requests** check box.</span></span>
9. <span data-ttu-id="87685-142">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="87685-142">Click **Create**.</span></span>

<span data-ttu-id="87685-143">Depois que você enviar sua solicitação, um engenheiro de Suporte entrará em contato com você assim que possível para prosseguir com sua solicitação.</span><span class="sxs-lookup"><span data-stu-id="87685-143">After you have submitted your request, a Support engineer will contact you as soon as possible to proceed with your request.</span></span>

## <a name="start-a-support-session-in-windows-powershell-for-storsimple"></a><span data-ttu-id="87685-144">Iniciar uma sessão de suporte no Windows PowerShell para StorSimple</span><span class="sxs-lookup"><span data-stu-id="87685-144">Start a support session in Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="87685-145">Para solucionar problemas que possam ocorrer com o dispositivo StorSimple, você precisará contatar a equipe de Suporte da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="87685-145">To troubleshoot any issues that you might experience with the StorSimple device, you will need to engage with the Microsoft Support team.</span></span> <span data-ttu-id="87685-146">O Suporte da Microsoft talvez precise usar uma sessão de suporte para fazer logon em seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="87685-146">Microsoft Support may need to use a support session to log on to your device.</span></span> 

<span data-ttu-id="87685-147">Execute as seguintes etapas para iniciar uma sessão de suporte:</span><span class="sxs-lookup"><span data-stu-id="87685-147">Perform the following steps to start a support session:</span></span>

#### <a name="to-start-a-support-session"></a><span data-ttu-id="87685-148">Para iniciar uma sessão de suporte</span><span class="sxs-lookup"><span data-stu-id="87685-148">To start a support session</span></span>
1. <span data-ttu-id="87685-149">Acesse o dispositivo diretamente usando o console serial ou por meio de uma sessão de telnet de um computador remoto.</span><span class="sxs-lookup"><span data-stu-id="87685-149">Access the device directly by using the serial console or through a telnet session from a remote computer.</span></span> <span data-ttu-id="87685-150">Para fazer isso, execute as etapas em [Usar o PuTTY para conectar-se ao console serial do dispositivo](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="87685-150">To do this, follow the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="87685-151">Na sessão que será aberta, pressione a tecla **Enter** para obter um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="87685-151">In the session that opens, press the **Enter** key to get a command prompt.</span></span>
3. <span data-ttu-id="87685-152">No menu do console serial, escolha a opção 1, **Efetuar login com acesso total**.</span><span class="sxs-lookup"><span data-stu-id="87685-152">In the serial console menu, select option 1, **Log in with full access**.</span></span>
4. <span data-ttu-id="87685-153">No prompt, digite a seguinte senha:</span><span class="sxs-lookup"><span data-stu-id="87685-153">At the prompt, type the following password:</span></span> 
   
    `Password1`
5. <span data-ttu-id="87685-154">No prompt, digite o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="87685-154">At the prompt, type the following command:</span></span>
   
    `Enable-HcsSupportAccess`
6. <span data-ttu-id="87685-155">Uma cadeia de caracteres criptografada será apresentada a você.</span><span class="sxs-lookup"><span data-stu-id="87685-155">An encrypted string will be presented to you.</span></span> <span data-ttu-id="87685-156">Copie a cadeia de caracteres para um editor de texto como o Bloco de Notas.</span><span class="sxs-lookup"><span data-stu-id="87685-156">Copy this string into a text editor such as Notepad.</span></span>
7. <span data-ttu-id="87685-157">Salve a cadeia de caracteres e envie-a em uma mensagem de email ao Suporte da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="87685-157">Save this string and send it in an email message to Microsoft Support.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="87685-158">Você pode desabilitar o acesso ao suporte executando `Disable-HcsSupportAccess`.</span><span class="sxs-lookup"><span data-stu-id="87685-158">You can disable support access by running `Disable-HcsSupportAccess`.</span></span> <span data-ttu-id="87685-159">O dispositivo StorSimple também tentará desabilitar o acesso ao suporte oito horas após a sessão ser iniciada.</span><span class="sxs-lookup"><span data-stu-id="87685-159">The StorSimple device will also attempt to disable support access 8 hours after the session was initiated.</span></span> <span data-ttu-id="87685-160">É uma prática recomendada alterar as credenciais de seu dispositivo StorSimple após iniciar uma sessão de suporte.</span><span class="sxs-lookup"><span data-stu-id="87685-160">It is a best practice to change your StorSimple device credentials after initiating a support session.</span></span>
> 
> 

