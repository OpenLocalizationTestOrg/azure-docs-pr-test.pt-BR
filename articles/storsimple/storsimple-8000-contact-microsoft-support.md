---
title: "Criar tíquete ou caso de suporte para o StorSimple série 8000 | Microsoft Docs"
description: "Saiba como registrar uma solicitação de suporte e iniciar uma sessão de suporte em seu dispositivo StorSimple da série 8000."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: alkohli;
ms.openlocfilehash: 4b5a14237ce79100f980b2186b2c3c887abaa296
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="contact-microsoft-support"></a><span data-ttu-id="90d5b-103">Contatar o Suporte da Microsoft</span><span class="sxs-lookup"><span data-stu-id="90d5b-103">Contact Microsoft Support</span></span>

<span data-ttu-id="90d5b-104">O Gerenciador de Dispositivos StorSimple fornece a capacidade de **fazer uma nova solicitação de suporte** na folha de resumo de serviço.</span><span class="sxs-lookup"><span data-stu-id="90d5b-104">The StorSimple Device Manager provides the capability to **log a new support request** within the service summary blade.</span></span> <span data-ttu-id="90d5b-105">Se tiver problemas com sua solução StorSimple, você poderá criar uma solicitação de serviço de suporte técnico.</span><span class="sxs-lookup"><span data-stu-id="90d5b-105">If you encounter any issues with your StorSimple solution, you can create a service request for technical support.</span></span> <span data-ttu-id="90d5b-106">Em uma sessão online com seu engenheiro de suporte, talvez você precise iniciar uma sessão de suporte em seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="90d5b-106">In an online session with your support engineer, you may also need to start a support session on your StorSimple device.</span></span> <span data-ttu-id="90d5b-107">Este artigo orienta você sobre:</span><span class="sxs-lookup"><span data-stu-id="90d5b-107">This article walks you through:</span></span>

* <span data-ttu-id="90d5b-108">Como criar uma solicitação de suporte.</span><span class="sxs-lookup"><span data-stu-id="90d5b-108">How to create a support request.</span></span>
* <span data-ttu-id="90d5b-109">Como gerenciar o ciclo de vida de uma solicitação de suporte de dentro do portal.</span><span class="sxs-lookup"><span data-stu-id="90d5b-109">How to manage a support request lifecycle from within the portal.</span></span>
* <span data-ttu-id="90d5b-110">Como iniciar uma sessão de suporte na interface do Windows PowerShell de seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="90d5b-110">How to start a support session in the Windows PowerShell interface of your StorSimple device.</span></span>

<span data-ttu-id="90d5b-111">Examine os [SLAs e informações de suporte ao StorSimple 8000 Series](https://msdn.microsoft.com/library/mt433077.aspx) antes de criar uma solicitação de suporte.</span><span class="sxs-lookup"><span data-stu-id="90d5b-111">Review the [StorSimple 8000 Series Support SLAs and information](https://msdn.microsoft.com/library/mt433077.aspx) before you create a Support request.</span></span>

## <a name="create-a-support-request"></a><span data-ttu-id="90d5b-112">Criar uma solicitação de suporte</span><span class="sxs-lookup"><span data-stu-id="90d5b-112">Create a support request</span></span>

<span data-ttu-id="90d5b-113">Dependendo do seu [plano de suporte](https://azure.microsoft.com/support/plans/), você pode criar tíquetes de suporte para um problema no seu dispositivo StorSimple diretamente da folha de resumo do serviço do Gerenciador de Dispositivos do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="90d5b-113">Depending upon your [support plan](https://azure.microsoft.com/support/plans/), you can create support tickets for an issue on your StorSimple device directly from the StorSimple Device Manager service summary blade.</span></span> <span data-ttu-id="90d5b-114">Execute as seguintes etapas para criar uma solicitação de suporte:</span><span class="sxs-lookup"><span data-stu-id="90d5b-114">Perform the following steps to create a support request:</span></span>

#### <a name="to-create-a-support-request"></a><span data-ttu-id="90d5b-115">Para criar uma solicitação de suporte</span><span class="sxs-lookup"><span data-stu-id="90d5b-115">To create a support request</span></span>

1. <span data-ttu-id="90d5b-116">Vá até o seu serviço do Gerenciador de Dispositivos StorSimple.</span><span class="sxs-lookup"><span data-stu-id="90d5b-116">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="90d5b-117">Nas configurações de resumo de serviço, vá até a seção **SUPORTE + SOLUÇÃO DE PROBLEMAS** e, em seguida, clique em **Nova solicitação de suporte**.</span><span class="sxs-lookup"><span data-stu-id="90d5b-117">In the service summary blade settings, go to **SUPPORT + TROUBLESHOOTING** section and then click **New support request**.</span></span>
     
    ![Contate o Suporte da MS por meio do novo portal](./media/storsimple-8000-contact-microsoft-support/contactsupport1.png)
   
2. <span data-ttu-id="90d5b-119">Na folha **Nova solicitação de suporte**, selecione **Noções Básicas**.</span><span class="sxs-lookup"><span data-stu-id="90d5b-119">In the **New support request** blade, select **Basics**.</span></span> <span data-ttu-id="90d5b-120">Na folha **Básico**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="90d5b-120">In the **Basics** blade, do the following steps:</span></span>
   1. <span data-ttu-id="90d5b-121">Na lista suspensa **Tipo de problema**, selecione **Técnico**.</span><span class="sxs-lookup"><span data-stu-id="90d5b-121">From the **Issue type** drop-down list , select **Technical**.</span></span>
   2. <span data-ttu-id="90d5b-122">O tipo de **Assinatura**, **Serviço** e o **Recurso** (serviço de Gerenciador de Dispositivos StorSimple) atuais são automaticamente escolhidos.</span><span class="sxs-lookup"><span data-stu-id="90d5b-122">The current **Subscription**, **Service** type, and the **Resource** (StorSimple Device Manager service) are automatically chosen.</span></span> 
   3. <span data-ttu-id="90d5b-123">Selecione um **Plano de suporte** na lista suspensa se você tiver vários planos associados à sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="90d5b-123">Select a **Support plan** from the drop-down list if you have multiple plans associated with your subscription.</span></span> <span data-ttu-id="90d5b-124">É necessário um plano de suporte pago para habilitar o Suporte Técnico.</span><span class="sxs-lookup"><span data-stu-id="90d5b-124">You need a paid support plan to enable Technical Support.</span></span>
   4. <span data-ttu-id="90d5b-125">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="90d5b-125">Click **Next**.</span></span>

       ![Contate o Suporte da MS por meio do novo portal](./media/storsimple-8000-contact-microsoft-support/contactsupport2.png)

3. <span data-ttu-id="90d5b-127">Na folha **Nova solicitação de suporte**, selecione **Etapa 2 Problema**.</span><span class="sxs-lookup"><span data-stu-id="90d5b-127">In the **New support request** blade, select **Step 2 Problem**.</span></span> <span data-ttu-id="90d5b-128">Na folha **Problema**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="90d5b-128">In the **Problem** blade, do the following steps:</span></span>
    
    1. <span data-ttu-id="90d5b-129">Escolha a **Gravidade**.</span><span class="sxs-lookup"><span data-stu-id="90d5b-129">Choose the **Severity**.</span></span>
    2. <span data-ttu-id="90d5b-130">Especifique se o problema está relacionado ao dispositivo ou ao serviço do Gerenciador de Dispositivos do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="90d5b-130">Specify if the issue is related to the appliance or the StorSimple Device Manager service.</span></span>
    3. <span data-ttu-id="90d5b-131">Escolha uma **Categoria** para este problema e forneça mais **Detalhes** sobre ele.</span><span class="sxs-lookup"><span data-stu-id="90d5b-131">Choose a **Category** for this issue and provide more **Details** about the issue.</span></span>
    4. <span data-ttu-id="90d5b-132">Forneça a data de início e a hora para o problema.</span><span class="sxs-lookup"><span data-stu-id="90d5b-132">Provide the start date and time for the problem.</span></span>
    5. <span data-ttu-id="90d5b-133">Em **Upload do arquivo**, clique no ícone de pasta para procurar o pacote de suporte.</span><span class="sxs-lookup"><span data-stu-id="90d5b-133">In the **File upload**, click the folder icon to browse to your support package.</span></span>
    6. <span data-ttu-id="90d5b-134">Marque **Compartilhar informações de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="90d5b-134">Check **Share diagnostic information**.</span></span>
    7. <span data-ttu-id="90d5b-135">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="90d5b-135">Click **Next**.</span></span>

       ![Contate o Suporte da MS por meio do novo portal](./media/storsimple-8000-contact-microsoft-support/contactsupport3.png) 

4. <span data-ttu-id="90d5b-137">Na folha **Nova solicitação de suporte**, clique em **Etapa 3 Informações de contato**.</span><span class="sxs-lookup"><span data-stu-id="90d5b-137">In the **New support request** blade, click **Step 3 Contact information**.</span></span> <span data-ttu-id="90d5b-138">Na folha **Informações de contato**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="90d5b-138">In the **Contact information** blade, do the following steps:</span></span>

    1. <span data-ttu-id="90d5b-139">Nas **Opções de contato**, forneça seu método de contato preferencial (telefone ou email) e o idioma.</span><span class="sxs-lookup"><span data-stu-id="90d5b-139">In the **Contact options**, provide your preferred contact method (phone or email) and the language.</span></span> <span data-ttu-id="90d5b-140">O tempo de resposta é selecionado automaticamente com base em seu plano de assinatura.</span><span class="sxs-lookup"><span data-stu-id="90d5b-140">The response time is automatically selected based on your subscription plan.</span></span>
    2. <span data-ttu-id="90d5b-141">Nas Informações de contato, informe seu nome, email, contato opcional e país.</span><span class="sxs-lookup"><span data-stu-id="90d5b-141">In the Contact information, provide your name, email, optional contact, country.</span></span> <span data-ttu-id="90d5b-142">Marque a caixa de seleção **Salvar alterações de contato para futuras solicitações de suporte** .</span><span class="sxs-lookup"><span data-stu-id="90d5b-142">Select the **Save contact changes for future support requests** check box.</span></span>
    3. <span data-ttu-id="90d5b-143">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="90d5b-143">Click **Create**.</span></span>
   
        ![Contate o Suporte da MS por meio do novo portal](./media/storsimple-8000-contact-microsoft-support/contactsupport5.png)   

    <span data-ttu-id="90d5b-145">O Microsoft Support usará essas informações para entrar em contato com você para obter mais informações, diagnóstico e resolução.</span><span class="sxs-lookup"><span data-stu-id="90d5b-145">Microsoft Support will use this information to reach out to you for further information, diagnosis, and resolution.</span></span>
<span data-ttu-id="90d5b-146">Depois que você enviar sua solicitação, um engenheiro de Suporte entrará em contato com você assim que possível para prosseguir com sua solicitação.</span><span class="sxs-lookup"><span data-stu-id="90d5b-146">After you have submitted your request, a Support engineer will contact you as soon as possible to proceed with your request.</span></span>

## <a name="manage-a-support-request"></a><span data-ttu-id="90d5b-147">Gerenciar uma solicitação de suporte</span><span class="sxs-lookup"><span data-stu-id="90d5b-147">Manage a support request</span></span>

<span data-ttu-id="90d5b-148">Depois de criar um tíquete de suporte, você pode gerenciar o ciclo de vida do tíquete de dentro do portal.</span><span class="sxs-lookup"><span data-stu-id="90d5b-148">After creating a support ticket, you can manage the lifecycle of the ticket from within the portal.</span></span>

#### <a name="to-manage-your-support-requests"></a><span data-ttu-id="90d5b-149">Para gerenciar suas solicitações de suporte</span><span class="sxs-lookup"><span data-stu-id="90d5b-149">To manage your support requests</span></span>

1. <span data-ttu-id="90d5b-150">Para acessar a página de ajuda e suporte navegue até **Procurar -> Ajuda + suporte**.</span><span class="sxs-lookup"><span data-stu-id="90d5b-150">To get to the help and support page, navigate to **Browse > Help + support**.</span></span>

    ![Gerenciar solicitações de suporte](./media/storsimple-8000-contact-microsoft-support/managesupport1.png)

2. <span data-ttu-id="90d5b-152">Uma listagem tabular de Todas as solicitações de suporte é exibida na folha **Ajuda + suporte**.</span><span class="sxs-lookup"><span data-stu-id="90d5b-152">A tabular listing of All the support requests is displayed in the **Help + support** blade.</span></span>

    ![Gerenciar solicitações de suporte](./media/storsimple-8000-contact-microsoft-support/managesupport2.png)

3. <span data-ttu-id="90d5b-154">Selecione e clique em uma solicitação de suporte.</span><span class="sxs-lookup"><span data-stu-id="90d5b-154">Select and click a support request.</span></span> <span data-ttu-id="90d5b-155">Você pode exibir o status e os detalhes para esta solicitação.</span><span class="sxs-lookup"><span data-stu-id="90d5b-155">You can view the status and the details for this request.</span></span> <span data-ttu-id="90d5b-156">Clique em **+ Nova mensagem** se desejar acompanhar esta solicitação.</span><span class="sxs-lookup"><span data-stu-id="90d5b-156">Click **+ New message** if you want to follow up on this request.</span></span>

    ![Gerenciar solicitações de suporte](./media/storsimple-8000-contact-microsoft-support/managesupport3.png)

## <a name="start-a-support-session-in-windows-powershell-for-storsimple"></a><span data-ttu-id="90d5b-158">Iniciar uma sessão de suporte no Windows PowerShell para StorSimple</span><span class="sxs-lookup"><span data-stu-id="90d5b-158">Start a support session in Windows PowerShell for StorSimple</span></span>

<span data-ttu-id="90d5b-159">Para solucionar problemas que possam ocorrer com o dispositivo StorSimple, você precisará contatar a equipe de Suporte da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="90d5b-159">To troubleshoot any issues that you might experience with the StorSimple device, you will need to engage with the Microsoft Support team.</span></span> <span data-ttu-id="90d5b-160">O Suporte da Microsoft talvez precise usar uma sessão de suporte para fazer logon em seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="90d5b-160">Microsoft Support may need to use a support session to log on to your device.</span></span>

<span data-ttu-id="90d5b-161">Execute as seguintes etapas para iniciar uma sessão de suporte:</span><span class="sxs-lookup"><span data-stu-id="90d5b-161">Perform the following steps to start a support session:</span></span>

#### <a name="to-start-a-support-session"></a><span data-ttu-id="90d5b-162">Para iniciar uma sessão de suporte</span><span class="sxs-lookup"><span data-stu-id="90d5b-162">To start a support session</span></span>

1. <span data-ttu-id="90d5b-163">Acesse o dispositivo diretamente usando o console serial ou por meio de uma sessão de telnet de um computador remoto.</span><span class="sxs-lookup"><span data-stu-id="90d5b-163">Access the device directly by using the serial console or through a telnet session from a remote computer.</span></span> <span data-ttu-id="90d5b-164">Para fazer isso, execute as etapas em [Usar o PuTTY para conectar-se ao console serial do dispositivo](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="90d5b-164">To do this, follow the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="90d5b-165">Na sessão que será aberta, pressione a tecla **Enter** para obter um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="90d5b-165">In the session that opens, press the **Enter** key to get a command prompt.</span></span>
3. <span data-ttu-id="90d5b-166">No menu do console serial, escolha a opção 1, **Efetuar login com acesso total**.</span><span class="sxs-lookup"><span data-stu-id="90d5b-166">In the serial console menu, select option 1, **Log in with full access**.</span></span>
4. <span data-ttu-id="90d5b-167">No prompt, digite a seguinte senha:</span><span class="sxs-lookup"><span data-stu-id="90d5b-167">At the prompt, type the following password:</span></span>
   
    `Password1`
5. <span data-ttu-id="90d5b-168">No prompt, digite o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="90d5b-168">At the prompt, type the following command:</span></span>
   
    `Enable-HcsSupportAccess`
6. <span data-ttu-id="90d5b-169">Uma cadeia de caracteres criptografada será apresentada a você.</span><span class="sxs-lookup"><span data-stu-id="90d5b-169">An encrypted string will be presented to you.</span></span> <span data-ttu-id="90d5b-170">Copie a cadeia de caracteres para um editor de texto como o Bloco de Notas.</span><span class="sxs-lookup"><span data-stu-id="90d5b-170">Copy this string into a text editor such as Notepad.</span></span>
7. <span data-ttu-id="90d5b-171">Salve a cadeia de caracteres e envie-a em uma mensagem de email ao Suporte da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="90d5b-171">Save this string and send it in an email message to Microsoft Support.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="90d5b-172">Você pode desabilitar o acesso ao suporte executando `Disable-HcsSupportAccess`.</span><span class="sxs-lookup"><span data-stu-id="90d5b-172">You can disable support access by running `Disable-HcsSupportAccess`.</span></span> <span data-ttu-id="90d5b-173">O dispositivo StorSimple também tentará desabilitar o acesso ao suporte oito horas após a sessão ser iniciada.</span><span class="sxs-lookup"><span data-stu-id="90d5b-173">The StorSimple device will also attempt to disable support access 8 hours after the session was initiated.</span></span> <span data-ttu-id="90d5b-174">É uma prática recomendada alterar as credenciais de seu dispositivo StorSimple após iniciar uma sessão de suporte.</span><span class="sxs-lookup"><span data-stu-id="90d5b-174">It is a best practice to change your StorSimple device credentials after initiating a support session.</span></span>


## <a name="next-steps"></a><span data-ttu-id="90d5b-175">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="90d5b-175">Next steps</span></span>

<span data-ttu-id="90d5b-176">Saiba como [diagnosticar e resolver problemas relacionados ao dispositivo StorSimple da série 8000](storsimple-troubleshoot-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="90d5b-176">Learn how to [diagnose and solve problems related to your StorSimple 8000 series device](storsimple-troubleshoot-deployment.md)</span></span>
