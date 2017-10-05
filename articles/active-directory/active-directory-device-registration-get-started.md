---
title: "Como configurar o registro automático de dispositivos ingressados no domínio do Windows com o Azure Active Directory| Microsoft Docs"
description: "Configure seus dispositivos de domínio do Windows para serem registrados de forma automática e silenciosa com o Azure Active Directory."
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
ms.openlocfilehash: 38750050e8525272079e1f3a5509da1e8f0a557b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-azure-active-directory-device-registration"></a><span data-ttu-id="260f9-103">Introdução ao registro de dispositivos do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="260f9-103">Get started with Azure Active Directory device registration</span></span>

<span data-ttu-id="260f9-104">O registro de dispositivo do Azure Active Directory é a base para cenários de acesso condicional com base no dispositivo.</span><span class="sxs-lookup"><span data-stu-id="260f9-104">Azure Active Directory device registration is the foundation for device-based conditional access scenarios.</span></span> <span data-ttu-id="260f9-105">Quando um dispositivo é registrado, o registro de dispositivo do Azure Active Directory fornece o dispositivo com uma identidade que é usada para autenticar o dispositivo quando o usuário faz logon.</span><span class="sxs-lookup"><span data-stu-id="260f9-105">When a device is registered, Azure Active Directory device registration provides the device with an identity which is used to authenticate the device when the user signs in.</span></span> <span data-ttu-id="260f9-106">O dispositivo autenticado e os atributos desse dispositivo podem, em seguida, ser usados para impor políticas de acesso condicional para aplicativos locais e hospedados em nuvem.</span><span class="sxs-lookup"><span data-stu-id="260f9-106">The authenticated device, and the attributes of the device, can then be used to enforce conditional access policies for applications that are hosted in the cloud and on-premises.</span></span>

<span data-ttu-id="260f9-107">Quando combinado com uma solução de MDM (gerenciamento de dispositivo móvel), como o Microsoft Intune, os atributos do dispositivo no Azure Active Directory são atualizados com informações adicionais sobre o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="260f9-107">When combined with a mobile device management(MDM) solution such as Microsoft Intune, the device attributes in Azure Active Directory are updated with additional information about the device.</span></span> <span data-ttu-id="260f9-108">Isso permite que você crie regras de acesso condicional que imponham que o acesso dos dispositivos atendam aos padrões de segurança e conformidade.</span><span class="sxs-lookup"><span data-stu-id="260f9-108">This allows you to create conditional access rules that enforce access from devices to meet your standards for security and compliance.</span></span> <span data-ttu-id="260f9-109">Para saber mais sobre o registro de dispositivos no Microsoft Intune, veja Registrar dispositivos para gerenciamento no Intune.</span><span class="sxs-lookup"><span data-stu-id="260f9-109">For more information on enrolling devices in Microsoft Intune, see Enroll devices for management in Intune.</span></span>
<span data-ttu-id="260f9-110">Os cenários habilitados pelo Registro de Dispositivos do Azure Active Directory inclui suporte para dispositivos iOS, Android e Windows.</span><span class="sxs-lookup"><span data-stu-id="260f9-110">Scenarios enabled by Azure Active Directory Device Registration Azure Active Directory Device Registration includes support for iOS, Android, and Windows devices.</span></span> <span data-ttu-id="260f9-111">Os cenários individuais que utilizam o registro de dispositivo do AD do Azure podem ter requisitos e suporte de plataforma mais específicos.</span><span class="sxs-lookup"><span data-stu-id="260f9-111">The individual scenarios that utilize Azure AD Device Registration may have more specific requirements and platform support.</span></span> 

<span data-ttu-id="260f9-112">Esses cenários são os seguintes:</span><span class="sxs-lookup"><span data-stu-id="260f9-112">These scenarios are as follows:</span></span>

- <span data-ttu-id="260f9-113">**Acesso condicional para aplicativos do Office 365 com o Microsoft Intune:** os administradores de TI podem provisionar políticas de dispositivo de acesso condicional para proteger recursos corporativos e, simultaneamente, permitir que os trabalhadores de informações em dispositivos compatíveis acessem os serviços.</span><span class="sxs-lookup"><span data-stu-id="260f9-113">**Conditional access for Office 365 applications with Microsoft Intune:** IT admins can provision conditional access device policies to secure corporate resources, while at the same time allowing information workers on compliant devices to access the services.</span></span> <span data-ttu-id="260f9-114">Para saber mais, veja Políticas de dispositivo de acesso condicional para serviços do Office 365.</span><span class="sxs-lookup"><span data-stu-id="260f9-114">For more information, see Conditional Access Device Policies for Office 365 services.</span></span>

- <span data-ttu-id="260f9-115">**Acesso Condicional a aplicativos que são hospedados localmente:** é possível usar dispositivos registrados com políticas de acesso para aplicativos configurados para usar o AD FS com o Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="260f9-115">**Conditional access to applications that are hosted on-premises:** You can use registered devices with access policies for applications that are configured to use AD FS with Windows Server 2012 R2.</span></span> <span data-ttu-id="260f9-116">Para obter mais informações sobre como configurar o acesso condicional para local, consulte [Configurando o acesso condicional local usando o registro do dispositivo do Azure Active Directory](active-directory-device-registration-on-premises-setup.md).</span><span class="sxs-lookup"><span data-stu-id="260f9-116">For more information about setting up conditional access for on-premises, see [Setting up On-premises Conditional Access using Azure Active Directory device registration](active-directory-device-registration-on-premises-setup.md).</span></span>

## <a name="setting-up-azure-active-directory-device-registration"></a><span data-ttu-id="260f9-117">Configuração do registro de dispositivos Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="260f9-117">Setting up Azure Active Directory Device Registration</span></span>

<span data-ttu-id="260f9-118">Para configurar o registro de dispositivo, há várias opções:</span><span class="sxs-lookup"><span data-stu-id="260f9-118">To setup device registration, you have multiple options:</span></span>

- <span data-ttu-id="260f9-119">Os dispositivos podem ser registrados ao ingressar no domínio do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="260f9-119">Devices can register when joined to Azure AD domain.</span></span> <span data-ttu-id="260f9-120">Para saber mais sobre esse tópico, aprenda mais sobre o ingresso do Azure AD e as configurações necessárias para os usuários ingressarem no domínio do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="260f9-120">For more on this topic, you can Learn more about Azure AD Join and the settings required for users to join Azure AD domain.</span></span>

- <span data-ttu-id="260f9-121">Os dispositivos podem ser registrados quando os usuários adicionarem contas corporativas ou de estudante ao Windows em um dispositivo pessoal, ou quando os dispositivos móveis se conectarem a um recurso de trabalho que exige registro.</span><span class="sxs-lookup"><span data-stu-id="260f9-121">Devices can be registered when users add work or school accounts to Windows on a personal device or when mobile devices connect to a work resources requiring registration.</span></span> <span data-ttu-id="260f9-122">Para garantir isso, habilite o Registro de Dispositivos do Azure AD no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="260f9-122">To ensure this, you must enable Azure AD Device Registration in the Azure Portal.</span></span> 

- <span data-ttu-id="260f9-123">Os dispositivos podem ser registrados usando o registro automático de dispositivo para computadores tradicionais ingressados em domínio.</span><span class="sxs-lookup"><span data-stu-id="260f9-123">Devices can be registered using automatic device registration for traditional domain-joined machines.</span></span> <span data-ttu-id="260f9-124">Para garantir isso, você deve primeiro configurar Azure AD Connect antes de continuar com o registro automático.</span><span class="sxs-lookup"><span data-stu-id="260f9-124">To ensure this, you must first Setup Azure AD Connect before you continue with automatic device registration.</span></span>

<span data-ttu-id="260f9-125">Para obter as instruções mais recentes, confira [Como configurar o registro automático de dispositivos ingressados no domínio do Windows com o Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span><span class="sxs-lookup"><span data-stu-id="260f9-125">For latest instructions, see [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>  
<span data-ttu-id="260f9-126">Você também pode exibir e habilitar ou desabilitar dispositivos registrados usando o Portal de administrador no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="260f9-126">You can also review and enable or disable registered devices using the Administrator Portal in Azure Active Directory.</span></span>

## <a name="enable-the-azure-active-directory-device-registration-service"></a><span data-ttu-id="260f9-127">Habilitar o serviço de registro de dispositivos do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="260f9-127">Enable the Azure Active Directory device registration service</span></span>

<span data-ttu-id="260f9-128">**Para habilitar o serviço de registro de dispositivos do Azure Active Directory**</span><span class="sxs-lookup"><span data-stu-id="260f9-128">**To enable the Azure Active Directory device registration service:**</span></span>

1.  <span data-ttu-id="260f9-129">Entre no Portal do Microsoft Azure como administrador.</span><span class="sxs-lookup"><span data-stu-id="260f9-129">Sign in to the Microsoft Azure portal as administrator.</span></span>

2.  <span data-ttu-id="260f9-130">No painel esquerdo, selecione **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="260f9-130">On the left pane, select **Active Directory**.</span></span>

3.  <span data-ttu-id="260f9-131">Na guia Diretório, selecione o diretório.</span><span class="sxs-lookup"><span data-stu-id="260f9-131">On the Directory tab, select your directory.</span></span>

4.  <span data-ttu-id="260f9-132">Clique em **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="260f9-132">Click **Configure**.</span></span>

5.  <span data-ttu-id="260f9-133">Role até **Dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="260f9-133">Scroll to **Devices**.</span></span>

6.  <span data-ttu-id="260f9-134">Selecione TODOS para OS USUÁRIOS PODEM REGISTRAR SEUS DISPOSITIVOS COM O AZURE AD.</span><span class="sxs-lookup"><span data-stu-id="260f9-134">Select ALL for USERS MAY REGISTER THEIR DEVICES WITH AZURE AD.</span></span>

7.  <span data-ttu-id="260f9-135">Selecione o número máximo de dispositivos que deseja autorizar por usuário.</span><span class="sxs-lookup"><span data-stu-id="260f9-135">Select the maximum number of devices you want to authorize per user.</span></span>

<span data-ttu-id="260f9-136">O registro com o Microsoft Intune ou o Gerenciamento de Dispositivos Móveis para o Office 365 exige registro do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="260f9-136">The enrollment with Microsoft Intune or Mobile Device Management for Office 365 requires device registration.</span></span> <span data-ttu-id="260f9-137">Se você tiver configurado qualquer um desses serviços, a opção **TODOS** estará selecionada e **NONE** estará desabilitado.</span><span class="sxs-lookup"><span data-stu-id="260f9-137">If you have configured either of these services, **ALL** is selected and **NONE** is disabled.</span></span> <span data-ttu-id="260f9-138">Verifique se eles estão configurados corretamente e possuem o licenciamento apropriado.</span><span class="sxs-lookup"><span data-stu-id="260f9-138">Please ensure that they are configured correctly and have the appropriate licensing.</span></span>

<span data-ttu-id="260f9-139">Por padrão, a autenticação de dois fatores não está habilitada para o serviço.</span><span class="sxs-lookup"><span data-stu-id="260f9-139">By default, two-factor authentication is not enabled for the service.</span></span> <span data-ttu-id="260f9-140">No entanto, a autenticação de dois fatores é recomendável ao registrar um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="260f9-140">However, two-factor authentication is recommended when registering a device.</span></span>

- <span data-ttu-id="260f9-141">Antes de solicitar a autenticação de dois fatores para esse serviço, você deve configurar um provedor de autenticação de dois fatores no Active Directory do Azure e configurar suas contas de usuário para Multi-Factor Authentication. Consulte Adicionando Multi-Factor Authentication para o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="260f9-141">Before requiring two-factor authentication for this service, you must configure a two-factor authentication provider in Azure Active Directory and configure your user accounts for Multi-Factor Authentication, see Adding Multi-Factor Authentication to Azure Active Directory</span></span>

- <span data-ttu-id="260f9-142">Se estiver usando o AD FS com o Windows Server 2012 R2, configure um módulo de autenticação de dois fatores no AD FS. Confira Usar a Autenticação Multifator com os Serviços de Federação do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="260f9-142">If you are using AD FS with Windows Server 2012 R2, you must configure a two-factor authentication module in AD FS, see Using Multi-Factor Authentication with Active Directory Federation Services.</span></span>

## <a name="view-and-manage-device-objects-in-azure-active-directory"></a><span data-ttu-id="260f9-143">Exibir e gerenciar objetos de dispositivo no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="260f9-143">View and manage device objects in Azure Active Directory</span></span>

<span data-ttu-id="260f9-144">No portal de administrador do Azure, você pode exibir, bloquear e desbloquear os dispositivos.</span><span class="sxs-lookup"><span data-stu-id="260f9-144">From the Azure Administrator portal, you can view, block, and unblock devices.</span></span> <span data-ttu-id="260f9-145">Um dispositivo bloqueado não terá acesso aos aplicativos que estão configurados para permitir apenas os dispositivos registrados.</span><span class="sxs-lookup"><span data-stu-id="260f9-145">A device that is blocked will no longer have access to applications that are configured to allow only registered devices.</span></span>

<span data-ttu-id="260f9-146">**Para exibir e gerenciar objetos de dispositivo no Azure Active Directory**</span><span class="sxs-lookup"><span data-stu-id="260f9-146">**To view and manage device objects in Azure Active Directory:**</span></span>
 
1.  <span data-ttu-id="260f9-147">Faça logon no Portal do Microsoft Azure como administrador.</span><span class="sxs-lookup"><span data-stu-id="260f9-147">Log on to the Microsoft Azure portal as administrator.</span></span>

2.  <span data-ttu-id="260f9-148">No painel esquerdo, selecione **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="260f9-148">On the left pane, select **Active Directory**.</span></span>

3.  <span data-ttu-id="260f9-149">Selecione seu diretório.</span><span class="sxs-lookup"><span data-stu-id="260f9-149">Select your directory.</span></span>

4.  <span data-ttu-id="260f9-150">Selecione **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="260f9-150">Select **Users**.</span></span> 

5.  <span data-ttu-id="260f9-151">Clique no usuário para o qual você deseja ver os dispositivos.</span><span class="sxs-lookup"><span data-stu-id="260f9-151">Click the user for which you want to see the devices.</span></span>

6.  <span data-ttu-id="260f9-152">Selecione **Dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="260f9-152">Select **Devices**.</span></span>

7.  <span data-ttu-id="260f9-153">Selecione **Dispositivos Registrados**.</span><span class="sxs-lookup"><span data-stu-id="260f9-153">Select **Registered Devices**.</span></span>

<span data-ttu-id="260f9-154">Agora você pode ver, bloquear ou desbloquear os dispositivos registrados dos usuários.</span><span class="sxs-lookup"><span data-stu-id="260f9-154">Now, you can review, block, or unblock the user's registered devices.</span></span>
<span data-ttu-id="260f9-155">Dispositivos com Windows 10 ingressados em um domínio local e automaticamente registrados não aparecem na guia Usuários.</span><span class="sxs-lookup"><span data-stu-id="260f9-155">Windows 10 devices that are on-premises domain-joined and automatically registered do not appear under the Users tab.</span></span> <span data-ttu-id="260f9-156">Use o comando do PowerShell Get-MsolDevice para localizar todos os dispositivos da empresa.</span><span class="sxs-lookup"><span data-stu-id="260f9-156">Please use the Get-MsolDevice PowerShell command to find all your enterprise devices.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="260f9-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="260f9-157">Next steps</span></span>

<span data-ttu-id="260f9-158">Para configurar o registro automatizado do dispositivo, confira [Como configurar o registro automático de dispositivos ingressados no domínio do Windows com o Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span><span class="sxs-lookup"><span data-stu-id="260f9-158">To setup automated device registration, see [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>


