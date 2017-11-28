---
title: "aaaHow tooconfigure o registro automático de dispositivos de domínio do Windows com o Active Directory do Azure | Microsoft Docs"
description: "Configure seu tooregister de dispositivos do Windows ingressado no domínio automática e silenciosa com o Active Directory do Azure."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 1d736eba734418231f12e23a8fc1a93405f129c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-device-registration"></a><span data-ttu-id="53105-103">Introdução ao registro de dispositivos do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="53105-103">Get started with Azure Active Directory device registration</span></span>

<span data-ttu-id="53105-104">Registro de dispositivo do Active Directory do Azure é a base de saudação para cenários de acesso condicional com base no dispositivo.</span><span class="sxs-lookup"><span data-stu-id="53105-104">Azure Active Directory device registration is hello foundation for device-based conditional access scenarios.</span></span> <span data-ttu-id="53105-105">Quando um dispositivo é registrado, registro de dispositivo do Active Directory do Azure fornece dispositivo Olá com uma identidade que é o dispositivo de saudação do tooauthenticate usado quando Olá usuário faz logon.</span><span class="sxs-lookup"><span data-stu-id="53105-105">When a device is registered, Azure Active Directory device registration provides hello device with an identity which is used tooauthenticate hello device when hello user signs in.</span></span> <span data-ttu-id="53105-106">dispositivo Olá autenticado e atributos de saudação do dispositivo hello, podem ser usado tooenforce políticas de acesso condicional para aplicativos hospedados na nuvem hello e local.</span><span class="sxs-lookup"><span data-stu-id="53105-106">hello authenticated device, and hello attributes of hello device, can then be used tooenforce conditional access policies for applications that are hosted in hello cloud and on-premises.</span></span>

<span data-ttu-id="53105-107">Quando combinado com uma solução de management(MDM) de dispositivo móvel como Microsoft Intune, os atributos de dispositivo Olá no Active Directory do Azure são atualizados com informações adicionais sobre o dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="53105-107">When combined with a mobile device management(MDM) solution such as Microsoft Intune, hello device attributes in Azure Active Directory are updated with additional information about hello device.</span></span> <span data-ttu-id="53105-108">Isso permite regras de acesso condicional toocreate que imponham acesso de dispositivos toomeet aos padrões de segurança e conformidade.</span><span class="sxs-lookup"><span data-stu-id="53105-108">This allows you toocreate conditional access rules that enforce access from devices toomeet your standards for security and compliance.</span></span> <span data-ttu-id="53105-109">Para saber mais sobre o registro de dispositivos no Microsoft Intune, veja Registrar dispositivos para gerenciamento no Intune.</span><span class="sxs-lookup"><span data-stu-id="53105-109">For more information on enrolling devices in Microsoft Intune, see Enroll devices for management in Intune.</span></span>
<span data-ttu-id="53105-110">Os cenários habilitados pelo Registro de Dispositivos do Azure Active Directory inclui suporte para dispositivos iOS, Android e Windows.</span><span class="sxs-lookup"><span data-stu-id="53105-110">Scenarios enabled by Azure Active Directory Device Registration Azure Active Directory Device Registration includes support for iOS, Android, and Windows devices.</span></span> <span data-ttu-id="53105-111">cenários de saudação individuais que utilizam o registro de dispositivo do AD do Azure podem ter requisitos e suporte de plataforma mais específicos.</span><span class="sxs-lookup"><span data-stu-id="53105-111">hello individual scenarios that utilize Azure AD Device Registration may have more specific requirements and platform support.</span></span> 

<span data-ttu-id="53105-112">Esses cenários são os seguintes:</span><span class="sxs-lookup"><span data-stu-id="53105-112">These scenarios are as follows:</span></span>

- <span data-ttu-id="53105-113">**Acesso condicional para aplicativos do Office 365 com o Microsoft Intune:** administradores de TI podem provisionar o acesso condicional dispositivo políticas toosecure recursos corporativos, enquanto a saudação mesmo momento que permite aos operadores de informações em dispositivos compatíveis Serviços de saudação tooaccess.</span><span class="sxs-lookup"><span data-stu-id="53105-113">**Conditional access for Office 365 applications with Microsoft Intune:** IT admins can provision conditional access device policies toosecure corporate resources, while at hello same time allowing information workers on compliant devices tooaccess hello services.</span></span> <span data-ttu-id="53105-114">Para saber mais, veja Políticas de dispositivo de acesso condicional para serviços do Office 365.</span><span class="sxs-lookup"><span data-stu-id="53105-114">For more information, see Conditional Access Device Policies for Office 365 services.</span></span>

- <span data-ttu-id="53105-115">**Tooapplications de acesso condicional que estão hospedados no local:** você pode usar dispositivos registrados com políticas de acesso para aplicativos que são configurados toouse do AD FS com o Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="53105-115">**Conditional access tooapplications that are hosted on-premises:** You can use registered devices with access policies for applications that are configured toouse AD FS with Windows Server 2012 R2.</span></span> <span data-ttu-id="53105-116">Para obter mais informações sobre como configurar o acesso condicional para local, consulte [Configurando o acesso condicional local usando o registro do dispositivo do Azure Active Directory](active-directory-device-registration-on-premises-setup.md).</span><span class="sxs-lookup"><span data-stu-id="53105-116">For more information about setting up conditional access for on-premises, see [Setting up On-premises Conditional Access using Azure Active Directory device registration](active-directory-device-registration-on-premises-setup.md).</span></span>

## <a name="setting-up-azure-active-directory-device-registration"></a><span data-ttu-id="53105-117">Configuração do registro de dispositivos Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="53105-117">Setting up Azure Active Directory Device Registration</span></span>

<span data-ttu-id="53105-118">registro de dispositivo toosetup, você tem várias opções:</span><span class="sxs-lookup"><span data-stu-id="53105-118">toosetup device registration, you have multiple options:</span></span>

- <span data-ttu-id="53105-119">Dispositivos podem se registrem ao domínio tooAzure ingressado no AD.</span><span class="sxs-lookup"><span data-stu-id="53105-119">Devices can register when joined tooAzure AD domain.</span></span> <span data-ttu-id="53105-120">Para obter mais informações sobre este tópico, você pode aprender mais sobre as configurações de junção do Azure AD e hello necessárias para usuários de domínio de toojoin AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="53105-120">For more on this topic, you can Learn more about Azure AD Join and hello settings required for users toojoin Azure AD domain.</span></span>

- <span data-ttu-id="53105-121">Dispositivos podem ser registrados quando usuários adicionarem trabalho ou escola contas tooWindows em um dispositivo pessoal ou dispositivos móveis se conectam tooa recursos de trabalho que exigem o registro.</span><span class="sxs-lookup"><span data-stu-id="53105-121">Devices can be registered when users add work or school accounts tooWindows on a personal device or when mobile devices connect tooa work resources requiring registration.</span></span> <span data-ttu-id="53105-122">tooensure isso, você deve habilitar o registro de dispositivo do AD do Azure no hello Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="53105-122">tooensure this, you must enable Azure AD Device Registration in hello Azure Portal.</span></span> 

- <span data-ttu-id="53105-123">Os dispositivos podem ser registrados usando o registro automático de dispositivo para computadores tradicionais ingressados em domínio.</span><span class="sxs-lookup"><span data-stu-id="53105-123">Devices can be registered using automatic device registration for traditional domain-joined machines.</span></span> <span data-ttu-id="53105-124">tooensure isso, você deve primeiro configurar Azure AD Connect antes de continuar com o registro automático do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="53105-124">tooensure this, you must first Setup Azure AD Connect before you continue with automatic device registration.</span></span>

<span data-ttu-id="53105-125">Para obter instruções mais recentes, consulte [como tooconfigure o registro automático do Windows ingressado no domínio dispositivos com o Active Directory do Azure](active-directory-conditional-access-automatic-device-registration-setup.md).</span><span class="sxs-lookup"><span data-stu-id="53105-125">For latest instructions, see [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>  
<span data-ttu-id="53105-126">Você também pode revisar e habilitar ou desabilitar os dispositivos registrados usando Olá Portal do administrador no Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="53105-126">You can also review and enable or disable registered devices using hello Administrator Portal in Azure Active Directory.</span></span>

## <a name="enable-hello-azure-active-directory-device-registration-service"></a><span data-ttu-id="53105-127">Habilitar o serviço de registro de dispositivo do Active Directory do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="53105-127">Enable hello Azure Active Directory device registration service</span></span>

<span data-ttu-id="53105-128">**Olá tooenable serviço de registro de dispositivo do Active Directory do Azure:**</span><span class="sxs-lookup"><span data-stu-id="53105-128">**tooenable hello Azure Active Directory device registration service:**</span></span>

1.  <span data-ttu-id="53105-129">Entre em toohello portal do Microsoft Azure como administrador.</span><span class="sxs-lookup"><span data-stu-id="53105-129">Sign in toohello Microsoft Azure portal as administrator.</span></span>

2.  <span data-ttu-id="53105-130">No painel esquerdo do hello, selecione **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="53105-130">On hello left pane, select **Active Directory**.</span></span>

3.  <span data-ttu-id="53105-131">Na guia de diretório hello, selecione seu diretório.</span><span class="sxs-lookup"><span data-stu-id="53105-131">On hello Directory tab, select your directory.</span></span>

4.  <span data-ttu-id="53105-132">Clique em **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="53105-132">Click **Configure**.</span></span>

5.  <span data-ttu-id="53105-133">Role muito**dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="53105-133">Scroll too**Devices**.</span></span>

6.  <span data-ttu-id="53105-134">Selecione TODOS para OS USUÁRIOS PODEM REGISTRAR SEUS DISPOSITIVOS COM O AZURE AD.</span><span class="sxs-lookup"><span data-stu-id="53105-134">Select ALL for USERS MAY REGISTER THEIR DEVICES WITH AZURE AD.</span></span>

7.  <span data-ttu-id="53105-135">Selecione o número máximo de saudação de dispositivos que você deseja tooauthorize por usuário.</span><span class="sxs-lookup"><span data-stu-id="53105-135">Select hello maximum number of devices you want tooauthorize per user.</span></span>

<span data-ttu-id="53105-136">registro de saudação com Microsoft Intune ou gerenciamento de dispositivo móvel para Office 365 requer o registro de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="53105-136">hello enrollment with Microsoft Intune or Mobile Device Management for Office 365 requires device registration.</span></span> <span data-ttu-id="53105-137">Se você tiver configurado qualquer um desses serviços, a opção **TODOS** estará selecionada e **NONE** estará desabilitado.</span><span class="sxs-lookup"><span data-stu-id="53105-137">If you have configured either of these services, **ALL** is selected and **NONE** is disabled.</span></span> <span data-ttu-id="53105-138">Certifique-se de que eles estão configurados corretamente e tem Olá apropriado de licenciamento.</span><span class="sxs-lookup"><span data-stu-id="53105-138">Please ensure that they are configured correctly and have hello appropriate licensing.</span></span>

<span data-ttu-id="53105-139">Por padrão, a autenticação de dois fatores não está habilitada para o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="53105-139">By default, two-factor authentication is not enabled for hello service.</span></span> <span data-ttu-id="53105-140">No entanto, a autenticação de dois fatores é recomendável ao registrar um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="53105-140">However, two-factor authentication is recommended when registering a device.</span></span>

- <span data-ttu-id="53105-141">Antes de solicitar a autenticação de dois fatores para esse serviço, você deve configurar um provedor de autenticação de dois fatores no Azure Active Directory e configurar as contas de usuário para autenticação multifator, consulte Adicionar autenticação multifator tooAzure do Active Directory</span><span class="sxs-lookup"><span data-stu-id="53105-141">Before requiring two-factor authentication for this service, you must configure a two-factor authentication provider in Azure Active Directory and configure your user accounts for Multi-Factor Authentication, see Adding Multi-Factor Authentication tooAzure Active Directory</span></span>

- <span data-ttu-id="53105-142">Se estiver usando o AD FS com o Windows Server 2012 R2, configure um módulo de autenticação de dois fatores no AD FS. Confira Usar a Autenticação Multifator com os Serviços de Federação do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="53105-142">If you are using AD FS with Windows Server 2012 R2, you must configure a two-factor authentication module in AD FS, see Using Multi-Factor Authentication with Active Directory Federation Services.</span></span>

## <a name="view-and-manage-device-objects-in-azure-active-directory"></a><span data-ttu-id="53105-143">Exibir e gerenciar objetos de dispositivo no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="53105-143">View and manage device objects in Azure Active Directory</span></span>

<span data-ttu-id="53105-144">No portal do administrador do Azure hello, exibir, bloquear e desbloquear dispositivos.</span><span class="sxs-lookup"><span data-stu-id="53105-144">From hello Azure Administrator portal, you can view, block, and unblock devices.</span></span> <span data-ttu-id="53105-145">Um dispositivo que está bloqueado não terá mais acesso tooapplications que são configurados tooallow apenas dispositivos registrados.</span><span class="sxs-lookup"><span data-stu-id="53105-145">A device that is blocked will no longer have access tooapplications that are configured tooallow only registered devices.</span></span>

<span data-ttu-id="53105-146">**tooview e gerenciar objetos de dispositivo no Active Directory do Azure:**</span><span class="sxs-lookup"><span data-stu-id="53105-146">**tooview and manage device objects in Azure Active Directory:**</span></span>
 
1.  <span data-ttu-id="53105-147">Faça logon no toohello portal do Microsoft Azure como administrador.</span><span class="sxs-lookup"><span data-stu-id="53105-147">Log on toohello Microsoft Azure portal as administrator.</span></span>

2.  <span data-ttu-id="53105-148">No painel esquerdo do hello, selecione **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="53105-148">On hello left pane, select **Active Directory**.</span></span>

3.  <span data-ttu-id="53105-149">Selecione seu diretório.</span><span class="sxs-lookup"><span data-stu-id="53105-149">Select your directory.</span></span>

4.  <span data-ttu-id="53105-150">Selecione **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="53105-150">Select **Users**.</span></span> 

5.  <span data-ttu-id="53105-151">Clique em usuário Olá para o qual você deseja que os dispositivos de saudação toosee.</span><span class="sxs-lookup"><span data-stu-id="53105-151">Click hello user for which you want toosee hello devices.</span></span>

6.  <span data-ttu-id="53105-152">Selecione **Dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="53105-152">Select **Devices**.</span></span>

7.  <span data-ttu-id="53105-153">Selecione **Dispositivos Registrados**.</span><span class="sxs-lookup"><span data-stu-id="53105-153">Select **Registered Devices**.</span></span>

<span data-ttu-id="53105-154">Agora, você pode revisar, bloquear ou desbloquear os dispositivos registrados do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="53105-154">Now, you can review, block, or unblock hello user's registered devices.</span></span>
<span data-ttu-id="53105-155">Dispositivos Windows 10 que estão em locais ingressado no domínio e registrados automaticamente não aparecem na guia de usuários de saudação. Use toofind de comando do PowerShell Get-MsolDevice Olá todos os seus dispositivos da empresa.</span><span class="sxs-lookup"><span data-stu-id="53105-155">Windows 10 devices that are on-premises domain-joined and automatically registered do not appear under hello Users tab. Please use hello Get-MsolDevice PowerShell command toofind all your enterprise devices.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="53105-156">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="53105-156">Next steps</span></span>

<span data-ttu-id="53105-157">toosetup automatizada de registro do dispositivo, consulte [como tooconfigure o registro automático do Windows ingressado no domínio dispositivos com o Active Directory do Azure](active-directory-conditional-access-automatic-device-registration-setup.md).</span><span class="sxs-lookup"><span data-stu-id="53105-157">toosetup automated device registration, see [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>


