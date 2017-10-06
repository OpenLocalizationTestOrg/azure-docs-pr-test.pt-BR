---
title: "aaaYou não pode chegar lá daqui em diante Olá portal do Azure de um dispositivo Windows | Microsoft Docs"
description: "Saiba onde não é possível obter aqui chega do e o que você pode verificar tooavoid em execução nesta caixa de diálogo."
services: active-directory
keywords: acesso condicional baseado em dispositivo, registro de dispositivo, habilitar registro de dispositivo, registro de dispositivo e MDM
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8ad0156c-0812-4855-8563-6fbff6194174
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: eda2aa10fbff5b3e515723219f61c1cb6f634e29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="you-cant-get-there-from-here-on-a-windows-device"></a><span data-ttu-id="c9ac4-104">Não é possível chegar lá a partir deste ponto em um dispositivo do Windows</span><span class="sxs-lookup"><span data-stu-id="c9ac4-104">You can't get there from here on a Windows device</span></span>

<span data-ttu-id="c9ac4-105">Durante uma tentativa de, por exemplo, acessar a intranet do SharePoint Online de sua organização, você pode encontrar uma página informando que *não é possível ir daqui até lá*.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-105">During an attempt to, for example, access your organization's SharePoint Online intranet you might run into a page that states that *you can't get there from here*.</span></span> <span data-ttu-id="c9ac4-106">Você está vendo esta página porque o administrador tiver configurado uma política de acesso condicional que impede que os recursos da empresa do acesso tooyour sob determinadas condições.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-106">You are seeing this page, because your administrator has configured a conditional access policy that prevents access tooyour organization's resources under certain conditions.</span></span> <span data-ttu-id="c9ac4-107">Embora seja necessário toocontact helpdesk ou tooget seu administrador que esse problema é resolvido, há algumas coisas que você pode experimentar por conta própria, primeiro.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-107">While it might be necessary toocontact helpdesk or your administrator tooget this problem solved, there are a few things you can try out yourself, first.</span></span>

<span data-ttu-id="c9ac4-108">Se você estiver usando um **Windows** dispositivo, você deve verificar Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="c9ac4-108">If you are using a **Windows** device, you should check hello following:</span></span>

- <span data-ttu-id="c9ac4-109">Você está usando um navegador com suporte?</span><span class="sxs-lookup"><span data-stu-id="c9ac4-109">Are you using a supported browser?</span></span>

- <span data-ttu-id="c9ac4-110">Você está executando uma versão com suporte do Windows em seu dispositivo?</span><span class="sxs-lookup"><span data-stu-id="c9ac4-110">Are you running a supported version of Windows on your device?</span></span>

- <span data-ttu-id="c9ac4-111">O dispositivo é compatível?</span><span class="sxs-lookup"><span data-stu-id="c9ac4-111">Is your device compliant?</span></span>






## <a name="supported-browser"></a><span data-ttu-id="c9ac4-112">Navegador com suporte</span><span class="sxs-lookup"><span data-stu-id="c9ac4-112">Supported browser</span></span>

<span data-ttu-id="c9ac4-113">Se o administrador tiver configurado uma política de acesso condicional, você só poderá acessar os recursos de sua organização usando um navegador com suporte.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-113">If your administrator has configured a conditional access policy, you can only access your organization's resources by using a supported browser.</span></span> <span data-ttu-id="c9ac4-114">Em um dispositivo com Windows, há suporte apenas para o **Internet Explorer** e o **Edge**.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-114">On a Windows device, only **Internet Explorer** and **Edge** are supported.</span></span>

<span data-ttu-id="c9ac4-115">Você pode identificar facilmente se você não pode acessar um recurso devido navegador sem suporte tooan examinando a seção de detalhes de saudação da página de erro hello:</span><span class="sxs-lookup"><span data-stu-id="c9ac4-115">You can easily identify whether you can't access a resource due tooan unsupported browser by looking at hello details section of hello error page:</span></span>

<span data-ttu-id="c9ac4-116">![Mensagem "Você não pode acessar esse lugar daqui" para navegadores sem suporte](./media/active-directory-conditional-access-device-remediation/02.png "Cenário")</span><span class="sxs-lookup"><span data-stu-id="c9ac4-116">!["You can't get there from here" message for unsupported browsers](./media/active-directory-conditional-access-device-remediation/02.png "Scenario")</span></span>

<span data-ttu-id="c9ac4-117">correção somente Olá é toouse um navegador que oferece suporte a aplicativo hello para sua plataforma de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-117">hello only remediation is toouse a browser that hello application supports for your device platform.</span></span> <span data-ttu-id="c9ac4-118">Para obter uma lista completa dos navegadores com suporte, consulte [Navegadores com suporte](active-directory-conditional-access-supported-apps.md#supported-browsers-for-device-based-policies).</span><span class="sxs-lookup"><span data-stu-id="c9ac4-118">For a complete list of supported browsers, see [supported browsers](active-directory-conditional-access-supported-apps.md#supported-browsers-for-device-based-policies).</span></span>  


## <a name="supported-versions-of-windows"></a><span data-ttu-id="c9ac4-119">Versões com suporte do Windows</span><span class="sxs-lookup"><span data-stu-id="c9ac4-119">Supported versions of Windows</span></span>

<span data-ttu-id="c9ac4-120">Olá seguinte deve ser verdadeiro sobre o sistema de operacional do Windows hello em seu dispositivo:</span><span class="sxs-lookup"><span data-stu-id="c9ac4-120">hello following must be true about hello Windows operating system on your device:</span></span> 

- <span data-ttu-id="c9ac4-121">Se você estiver executando um sistema operacional de desktop Windows em seu dispositivo, ele precisa toobe Windows 7 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-121">If you are running a Windows desktop operating system on your device, it needs toobe Windows 7 or later.</span></span>
- <span data-ttu-id="c9ac4-122">Se você estiver executando um sistema operacional do Windows server em seu dispositivo, ele precisa toobe Windows Server 2008 R2 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-122">If you are running a Windows server operating system on your device, it needs toobe Windows Server 2008 R2 or later.</span></span> 


## <a name="compliant-device"></a><span data-ttu-id="c9ac4-123">Dispositivo em conformidade</span><span class="sxs-lookup"><span data-stu-id="c9ac4-123">Compliant device</span></span>

<span data-ttu-id="c9ac4-124">O administrador pode ter configurado uma política de acesso condicional que permite que os recursos da organização de tooyour acesso somente de dispositivos compatíveis.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-124">Your administrator might have configured a conditional access policy that allows access tooyour organization's resources only from compliant devices.</span></span> <span data-ttu-id="c9ac4-125">toobe compatível, que o dispositivo deve ser qualquer tooyour ingressado no Active Directory local ou Unidos tooyour Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-125">toobe compliant, your device must be either joined tooyour on-premises Active Directory or joined tooyour Azure Active Directory.</span></span>

<span data-ttu-id="c9ac4-126">Você pode identificar facilmente se você não pode acessar um recurso devido tooa dispositivo que não é compatível com examinando a seção de detalhes de saudação da página de erro hello:</span><span class="sxs-lookup"><span data-stu-id="c9ac4-126">You can easily identify whether you can't access a resource due tooa device that is not compliant by looking at hello details section of hello error page:</span></span>
 
<span data-ttu-id="c9ac4-127">![Mensagens "Você não pode acessar esse lugar daqui" para dispositivos não registrados](./media/active-directory-conditional-access-device-remediation/01.png "Cenário")</span><span class="sxs-lookup"><span data-stu-id="c9ac4-127">!["You can't get there from here" messages for unregistered devices](./media/active-directory-conditional-access-device-remediation/01.png "Scenario")</span></span>


### <a name="is-your-device-joined-tooan-on-premises-active-directory"></a><span data-ttu-id="c9ac4-128">É o seu dispositivo ingressado tooan do Active Directory local?</span><span class="sxs-lookup"><span data-stu-id="c9ac4-128">Is your device joined tooan on-premises Active Directory?</span></span>

<span data-ttu-id="c9ac4-129">**Se o dispositivo é associado tooan local do Active Directory em sua organização:**</span><span class="sxs-lookup"><span data-stu-id="c9ac4-129">**If your device is joined tooan on-premises Active Directory in your organization:**</span></span>

1. <span data-ttu-id="c9ac4-130">Certifique-se de que você entrar no tooWindows usando sua conta de trabalho (sua conta do Active Directory).</span><span class="sxs-lookup"><span data-stu-id="c9ac4-130">Make sure that you sign in tooWindows by using your work account (your Active Directory account).</span></span>
2. <span data-ttu-id="c9ac4-131">Conecte-se a rede corporativa tooyour por meio de uma rede virtual privada (VPN) ou DirectAccess.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-131">Connect tooyour corporate network via a virtual private network (VPN) or DirectAccess.</span></span>
3. <span data-ttu-id="c9ac4-132">Depois que você está conectado, pressione a tecla de logotipo do Windows hello + toolock chave Olá L a sessão do Windows.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-132">After you are connected, press hello Windows logo key + hello L key toolock your Windows session.</span></span>
4. <span data-ttu-id="c9ac4-133">Desbloqueie a sessão do Windows inserindo as credenciais de sua conta corporativa.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-133">Unlock your Windows session by entering your work account credentials.</span></span>
5. <span data-ttu-id="c9ac4-134">Aguarde um minuto e, em seguida, tente novamente tooaccess Olá aplicativo ou serviço.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-134">Wait for a minute, and then try again tooaccess hello application or service.</span></span>
6. <span data-ttu-id="c9ac4-135">Se você vir Olá mesma página, clique em hello **mais detalhes** link e, em seguida, contate o administrador com detalhes de saudação.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-135">If you see hello same page, click hello **More details** link, and then contact your administrator with hello details.</span></span>


### <a name="is-your-device-not-joined-tooan-on-premises-active-directory"></a><span data-ttu-id="c9ac4-136">É tooan seu dispositivo não fizer parte do Active Directory local?</span><span class="sxs-lookup"><span data-stu-id="c9ac4-136">Is your device not joined tooan on-premises Active Directory?</span></span>

<span data-ttu-id="c9ac4-137">Se seu dispositivo não tiver ingressado tooan do Active Directory local e execute o Windows 10, você tem duas opções:</span><span class="sxs-lookup"><span data-stu-id="c9ac4-137">If your device is not joined tooan on-premises Active Directory and runs Windows 10, you have two options:</span></span>

* <span data-ttu-id="c9ac4-138">Executar o Ingresso do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9ac4-138">Run Azure AD Join</span></span>
* <span data-ttu-id="c9ac4-139">Adicionar seu trabalho ou escolar tooWindows de conta</span><span class="sxs-lookup"><span data-stu-id="c9ac4-139">Add your work or school account tooWindows</span></span>

<span data-ttu-id="c9ac4-140">Para saber mais sobre como essas opções são diferentes, veja [Usando dispositivos Windows 10 em seu local de trabalho](active-directory-azureadjoin-windows10-devices.md).</span><span class="sxs-lookup"><span data-stu-id="c9ac4-140">For information about how these options are different, see [Using Windows 10 devices in your workplace](active-directory-azureadjoin-windows10-devices.md).</span></span>  
<span data-ttu-id="c9ac4-141">Se o seu dispositivo:</span><span class="sxs-lookup"><span data-stu-id="c9ac4-141">If your device:</span></span>

- <span data-ttu-id="c9ac4-142">Pertence tooyour organização, você deve executar a junção do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-142">Belongs tooyour organization, you should run Azure AD Join.</span></span>
- <span data-ttu-id="c9ac4-143">É um dispositivo pessoal ou um Windows phone, você deve adicionar o seu trabalho ou de estudante tooWindows de conta</span><span class="sxs-lookup"><span data-stu-id="c9ac4-143">Is a personal device or a Windows phone, you should add your work or school account tooWindows</span></span> 



#### <a name="azure-ad-join-on-windows-10"></a><span data-ttu-id="c9ac4-144">Ingresso no Azure AD no Windows 10</span><span class="sxs-lookup"><span data-stu-id="c9ac4-144">Azure AD Join on Windows 10</span></span>

<span data-ttu-id="c9ac4-145">Olá etapas toojoin tooAzure seu dispositivo AD são vinculados versão de saudação do Windows 10 que estão sendo executadas nele.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-145">hello steps toojoin your device tooAzure AD are tied hello version of Windows 10 you are running on it.</span></span> <span data-ttu-id="c9ac4-146">versão de hello toodetermine do sistema operacional Windows 10, execute Olá **winver** comando:</span><span class="sxs-lookup"><span data-stu-id="c9ac4-146">toodetermine hello version of your Windows 10 operating system, run hello **winver** command:</span></span> 

![Versão do Windows](./media/active-directory-conditional-access-device-remediation/03.png )


<span data-ttu-id="c9ac4-148">**Atualização de Aniversário do Windows 10 (Versão 1607):**</span><span class="sxs-lookup"><span data-stu-id="c9ac4-148">**Windows 10 Anniversary Update (Version 1607):**</span></span>

1. <span data-ttu-id="c9ac4-149">Olá abrir **configurações** aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-149">Open hello **Settings** app.</span></span>
2. <span data-ttu-id="c9ac4-150">Clique em **Contas** > **Acesso corporativo ou de estudante**.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-150">Click **Accounts** > **Access work or school**.</span></span>
3. <span data-ttu-id="c9ac4-151">Clique em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-151">Click **Connect**.</span></span>
4. <span data-ttu-id="c9ac4-152">Clique em **ingressar tooAzure este dispositivo AD**.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-152">Click **Join this device tooAzure AD**.</span></span>
5. <span data-ttu-id="c9ac4-153">Autenticar organização tooyour, fornecem autenticação multifator, se solicitado e, em seguida, execute as etapas de saudação que são mostradas.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-153">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
6. <span data-ttu-id="c9ac4-154">Saia e entre com sua conta corporativa.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-154">Sign out, and then sign in with your work account.</span></span>
7. <span data-ttu-id="c9ac4-155">Tente novamente o aplicativo hello de tooaccess.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-155">Try again tooaccess hello application.</span></span>

<span data-ttu-id="c9ac4-156">**Atualização do Windows de 10 de novembro de 2015 (Versão 1511):**</span><span class="sxs-lookup"><span data-stu-id="c9ac4-156">**Windows 10 November 2015 Update (Version 1511):**</span></span>

1. <span data-ttu-id="c9ac4-157">Olá abrir **configurações** aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-157">Open hello **Settings** app.</span></span>
2. <span data-ttu-id="c9ac4-158">Clique em **Sistema** > **Sobre**.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-158">Click **System** > **About**.</span></span>
3. <span data-ttu-id="c9ac4-159">Clique em **Ingressar no Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-159">Click **Join Azure AD**.</span></span>
4. <span data-ttu-id="c9ac4-160">Autenticar organização tooyour, fornecem autenticação multifator, se solicitado e, em seguida, execute as etapas de saudação que são mostradas.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-160">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
5. <span data-ttu-id="c9ac4-161">Saia e entre com sua conta corporativa (sua conta do Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c9ac4-161">Sign out, and then sign in with your work account (your Azure AD account).</span></span>
6. <span data-ttu-id="c9ac4-162">Tente novamente o aplicativo hello de tooaccess.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-162">Try again tooaccess hello application.</span></span>


#### <a name="workplace-join-on-windows-81"></a><span data-ttu-id="c9ac4-163">Workplace Join para Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="c9ac4-163">Workplace Join on Windows 8.1</span></span>

<span data-ttu-id="c9ac4-164">Se o dispositivo não estiver associado ao domínio e executa o Windows 8.1, toodo um ingresso e registrar-se no Microsoft Intune, Olá seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c9ac4-164">If your device is not domain-joined and runs Windows 8.1, toodo a Workplace Join and enroll in Microsoft Intune, do hello following steps:</span></span>

1. <span data-ttu-id="c9ac4-165">Abra **Configurações do PC**.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-165">Open **PC Settings**.</span></span>
2. <span data-ttu-id="c9ac4-166">Clique em **Rede** > **Local de Trabalho**.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-166">Click **Network** > **Workplace**.</span></span>
3. <span data-ttu-id="c9ac4-167">Clique em **Ingressar**.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-167">Click **Join**.</span></span>
4. <span data-ttu-id="c9ac4-168">Autenticar organização tooyour, fornecem autenticação multifator, se solicitado e, em seguida, execute as etapas de saudação que são mostradas.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-168">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
5. <span data-ttu-id="c9ac4-169">Clique em **Ativar**.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-169">Click **Turn on**.</span></span>
6. <span data-ttu-id="c9ac4-170">Tente novamente o aplicativo hello de tooaccess.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-170">Try again tooaccess hello application.</span></span>



#### <a name="add-your-work-or-school-account-toowindows"></a><span data-ttu-id="c9ac4-171">Adicionar seu trabalho ou escolar tooWindows de conta</span><span class="sxs-lookup"><span data-stu-id="c9ac4-171">Add your work or school account tooWindows</span></span> 


<span data-ttu-id="c9ac4-172">**Atualização de Aniversário do Windows 10 (Versão 1607):**</span><span class="sxs-lookup"><span data-stu-id="c9ac4-172">**Windows 10 Anniversary Update (Version 1607):**</span></span>

1. <span data-ttu-id="c9ac4-173">Olá abrir **configurações** aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-173">Open hello **Settings** app.</span></span>
2. <span data-ttu-id="c9ac4-174">Clique em **Contas** > **Acesso corporativo ou de estudante**.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-174">Click **Accounts** > **Access work or school**.</span></span>
3. <span data-ttu-id="c9ac4-175">Clique em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-175">Click **Connect**.</span></span>
4. <span data-ttu-id="c9ac4-176">Autenticar organização tooyour, fornecem autenticação multifator, se solicitado e, em seguida, execute as etapas de saudação que são mostradas.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-176">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
5. <span data-ttu-id="c9ac4-177">Tente novamente o aplicativo hello de tooaccess.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-177">Try again tooaccess hello application.</span></span>


<span data-ttu-id="c9ac4-178">**Atualização do Windows de 10 de novembro de 2015 (Versão 1511):**</span><span class="sxs-lookup"><span data-stu-id="c9ac4-178">**Windows 10 November 2015 Update (Version 1511):**</span></span>

1. <span data-ttu-id="c9ac4-179">Olá abrir **configurações** aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-179">Open hello **Settings** app.</span></span>
2. <span data-ttu-id="c9ac4-180">Clique em **Contas** > **Suas contas**.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-180">Click **Accounts** > **Your accounts**.</span></span>
3. <span data-ttu-id="c9ac4-181">Clique em **Adicionar conta corporativa ou de estudante**.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-181">Click **Add work or school account**.</span></span>
4. <span data-ttu-id="c9ac4-182">Autenticar organização tooyour, fornecem autenticação multifator, se solicitado e, em seguida, execute as etapas de saudação que são mostradas.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-182">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
5. <span data-ttu-id="c9ac4-183">Tente novamente o aplicativo hello de tooaccess.</span><span class="sxs-lookup"><span data-stu-id="c9ac4-183">Try again tooaccess hello application.</span></span>





## <a name="next-steps"></a><span data-ttu-id="c9ac4-184">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c9ac4-184">Next steps</span></span>
[<span data-ttu-id="c9ac4-185">Acesso condicional ao Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c9ac4-185">Azure Active Directory conditional access</span></span>](active-directory-conditional-access.md)

