---
title: gerenciamento de toodevice aaaIntroduction no Active Directory do Azure | Microsoft Docs
description: "Saiba como o gerenciamento de dispositivos pode ajudá-lo tooget controle os dispositivos de saudação que estão acessando os recursos em seu ambiente."
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
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: e2fc0a3e8d00dc69cf01db9074e34427e396cfcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toodevice-management-in-azure-active-directory"></a><span data-ttu-id="aaac4-103">Gerenciamento de toodevice de Introdução no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="aaac4-103">Introduction toodevice management in Azure Active Directory</span></span>

<span data-ttu-id="aaac4-104">Em um mundo móveis, primeiro, a nuvem, o Azure Active Directory (AD do Azure) permite toodevices de logon único, os aplicativos e serviços de qualquer lugar.</span><span class="sxs-lookup"><span data-stu-id="aaac4-104">In a mobile-first, cloud-first world, Azure Active Directory (Azure AD) enables single sign-on toodevices, apps, and services from anywhere.</span></span> <span data-ttu-id="aaac4-105">Com a proliferação de saudação de dispositivos - incluindo BYOD traga seu próprio dispositivo (), profissionais de TI enfrentam dois objetivos opostos:</span><span class="sxs-lookup"><span data-stu-id="aaac4-105">With hello proliferation of devices - including Bring Your Own Device (BYOD), IT professionals are faced with two opposing goals:</span></span>

- <span data-ttu-id="aaac4-106">Capacitar Olá os usuários finais toobe produtivo sempre e</span><span class="sxs-lookup"><span data-stu-id="aaac4-106">Empower hello end users toobe productive wherever and whenever</span></span>
- <span data-ttu-id="aaac4-107">Proteger os ativos corporativos Olá a qualquer momento</span><span class="sxs-lookup"><span data-stu-id="aaac4-107">Protect hello corporate assets at any time</span></span>

<span data-ttu-id="aaac4-108">Por meio de dispositivos, os usuários recebem acesso tooyour os ativos corporativos.</span><span class="sxs-lookup"><span data-stu-id="aaac4-108">Through devices, your users are getting access tooyour corporate assets.</span></span> <span data-ttu-id="aaac4-109">tooprotect seus recursos corporativos, como um administrador de TI, você deseja toohave controle sobre esses dispositivos.</span><span class="sxs-lookup"><span data-stu-id="aaac4-109">tooprotect your corporate assets, as an IT administrator, you want toohave control over these devices.</span></span> <span data-ttu-id="aaac4-110">Isso permite que você toomake-se de que os usuários estão acessando os recursos de dispositivos que atendem aos padrões de segurança e conformidade.</span><span class="sxs-lookup"><span data-stu-id="aaac4-110">This enables you toomake sure that your users are accessing your resources from devices that meet your standards for security and compliance.</span></span> 

<span data-ttu-id="aaac4-111">Gerenciamento de dispositivo também é foundation Olá para [acesso condicional baseado em dispositivo](active-directory-conditional-access-policy-connected-applications.md).</span><span class="sxs-lookup"><span data-stu-id="aaac4-111">Device management is also hello foundation for [device-based conditional access](active-directory-conditional-access-policy-connected-applications.md).</span></span> <span data-ttu-id="aaac4-112">Com acesso condicional com base no dispositivo, você pode garantir que acesso tooresources em seu ambiente só é possível com dispositivos confiáveis.</span><span class="sxs-lookup"><span data-stu-id="aaac4-112">With device-based conditional access, you can ensure that access tooresources in your environment is only possible with trusted devices.</span></span>   

<span data-ttu-id="aaac4-113">Este tópico explica como funciona o gerenciamento de dispositivo no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="aaac4-113">This topic explains how device management in Azure Active Directory works.</span></span>

## <a name="getting-devices-under-hello-control-of-azure-ad"></a><span data-ttu-id="aaac4-114">Obtendo dispositivos sob o controle de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="aaac4-114">Getting devices under hello control of Azure AD</span></span>

<span data-ttu-id="aaac4-115">tooget um dispositivo sob o controle de saudação do AD do Azure, você tem duas opções:</span><span class="sxs-lookup"><span data-stu-id="aaac4-115">tooget a device under hello control of Azure AD, you have two options:</span></span>

- <span data-ttu-id="aaac4-116">Registro</span><span class="sxs-lookup"><span data-stu-id="aaac4-116">Registering</span></span> 
- <span data-ttu-id="aaac4-117">Adição</span><span class="sxs-lookup"><span data-stu-id="aaac4-117">Joining</span></span>

<span data-ttu-id="aaac4-118">**Registrando** tooAzure um dispositivo AD permite que você toomanage identidade do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="aaac4-118">**Registering** a device tooAzure AD enables you toomanage a device’s identity.</span></span> <span data-ttu-id="aaac4-119">Quando um dispositivo é registrado, o registro de dispositivos do AD do Azure fornece dispositivo Olá com uma identidade que é usada tooauthenticate Olá dispositivo quando um usuário entrar tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="aaac4-119">When a device is registered, Azure AD device registration provides hello device with an identity that is used tooauthenticate hello device when a user signs-in tooAzure AD.</span></span> <span data-ttu-id="aaac4-120">Você pode usar o hello identidade tooenable ou desativar um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="aaac4-120">You can use hello identity tooenable or disable a device.</span></span>

<span data-ttu-id="aaac4-121">Quando combinado com uma solução de management(MDM) de dispositivo móvel como Microsoft Intune, os atributos de dispositivo Olá no AD do Azure são atualizados com informações adicionais sobre o dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="aaac4-121">When combined with a mobile device management(MDM) solution such as Microsoft Intune, hello device attributes in Azure AD are updated with additional information about hello device.</span></span> <span data-ttu-id="aaac4-122">Isso permite regras de acesso condicional toocreate que imponham acesso de dispositivos toomeet aos padrões de segurança e conformidade.</span><span class="sxs-lookup"><span data-stu-id="aaac4-122">This allows you toocreate conditional access rules that enforce access from devices toomeet your standards for security and compliance.</span></span> <span data-ttu-id="aaac4-123">Para saber mais sobre o registro de dispositivos no Microsoft Intune, confira Enroll devices for management in Intune (Registrar dispositivos para gerenciamento no Intune).</span><span class="sxs-lookup"><span data-stu-id="aaac4-123">For more information on enrolling devices in Microsoft Intune, see Enroll devices for management in Intune .</span></span>

<span data-ttu-id="aaac4-124">**Unindo** um dispositivo é uma extensão tooregistering um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="aaac4-124">**Joining** a device is an extension tooregistering a device.</span></span> <span data-ttu-id="aaac4-125">Isso significa, ele fornece todos os benefícios de saudação de registrar um dispositivo e em adição toothis, ele também altera o estado de um dispositivo local hello.</span><span class="sxs-lookup"><span data-stu-id="aaac4-125">This means, it provides you with all hello benefits of registering a device and in addition toothis, it also changes hello local state of a device.</span></span> <span data-ttu-id="aaac4-126">A alteração do estado local Olá permite que o dispositivo de tooa toosign-in de usuários usando uma conta de escola ou trabalho organizacional em vez de uma conta pessoal.</span><span class="sxs-lookup"><span data-stu-id="aaac4-126">Changing hello local state enables your users toosign-in tooa device using an organizational work or school account instead of a personal account.</span></span>

## <a name="azure-ad-registered-devices"></a><span data-ttu-id="aaac4-127">Dispositivos registrados no Azure AD</span><span class="sxs-lookup"><span data-stu-id="aaac4-127">Azure AD registered devices</span></span>   

<span data-ttu-id="aaac4-128">Olá, meta de dispositivos do AD do Azure registrado é tooprovide suporte Olá **BYOD traga seu próprio dispositivo ()** cenário.</span><span class="sxs-lookup"><span data-stu-id="aaac4-128">hello goal of Azure AD registered devices is tooprovide you with support for hello **Bring Your Own Device (BYOD)** scenario.</span></span> <span data-ttu-id="aaac4-129">Nesse cenário, um usuário pode acessar os recursos controlados pelo Azure Active Directory da sua organização usando um dispositivo pessoal.</span><span class="sxs-lookup"><span data-stu-id="aaac4-129">In this scenario, a user can access your organization’s Azure Active Directory controlled resources using a personal device.</span></span>  

![Dispositivos registrados no Azure AD](./media/device-management-introduction/03.png)

<span data-ttu-id="aaac4-131">acesso de saudação baseia-se em uma conta corporativa ou de estudante que foi digitada no dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="aaac4-131">hello access is based on a work or school account that has been entered on hello device.</span></span>  
<span data-ttu-id="aaac4-132">Por exemplo, Windows 10 permite que os usuários tooadd um trabalho ou escola conta tooa PC, tablet ou telefone.</span><span class="sxs-lookup"><span data-stu-id="aaac4-132">For example, Windows 10 enables users tooadd a work or school account tooa personal computer, tablet, or phone.</span></span>  
<span data-ttu-id="aaac4-133">Quando um usuário tiver adicionado um trabalho ou a conta de escola, o dispositivo Olá é registrado com o Azure AD e opcionalmente registrado no sistema de gerenciamento (MDM) do dispositivo móvel Olá sua organização tiver configurado.</span><span class="sxs-lookup"><span data-stu-id="aaac4-133">When a user has added a work or school account, hello device is registered with Azure AD and optionally enrolled in hello mobile device management (MDM) system that your organization has configured.</span></span> <span data-ttu-id="aaac4-134">Os usuários da organização podem adicionar um ou escolar dispositivo pessoal do conta tooa convenientemente:</span><span class="sxs-lookup"><span data-stu-id="aaac4-134">Your organization’s users can add a work or school account tooa personal device conveniently:</span></span>

- <span data-ttu-id="aaac4-135">Ao acessar um aplicativo de trabalho para Olá primeira vez</span><span class="sxs-lookup"><span data-stu-id="aaac4-135">When accessing a work application for hello first time</span></span>
- <span data-ttu-id="aaac4-136">Manualmente por meio de saudação **configurações** menu no caso de saudação do Windows 10</span><span class="sxs-lookup"><span data-stu-id="aaac4-136">Manually via hello **Settings** menu in hello case of Windows 10</span></span> 

<span data-ttu-id="aaac4-137">Você pode configurar dispositivos registrados no Azure AD para Windows 10, iOS, Android e macOS.</span><span class="sxs-lookup"><span data-stu-id="aaac4-137">You can configure Azure AD registered devices for Windows 10, iOS, Android and macOS.</span></span>

## <a name="azure-ad-joined-devices"></a><span data-ttu-id="aaac4-138">Dispositivos adicionados ao Azure AD</span><span class="sxs-lookup"><span data-stu-id="aaac4-138">Azure AD joined devices</span></span>

<span data-ttu-id="aaac4-139">meta de saudação de dispositivos do AD do Azure associado é toosimplify:</span><span class="sxs-lookup"><span data-stu-id="aaac4-139">hello goal of Azure AD joined devices is toosimplify:</span></span>

- <span data-ttu-id="aaac4-140">As implantações de dispositivos Windows que pertencem à organização</span><span class="sxs-lookup"><span data-stu-id="aaac4-140">Windows deployments of work-owned devices</span></span> 
- <span data-ttu-id="aaac4-141">Acesso tooorganizational aplicativos e recursos de dispositivos Windows</span><span class="sxs-lookup"><span data-stu-id="aaac4-141">Access tooorganizational apps and resources from any Windows device</span></span>

![Dispositivos registrados no Azure AD](./media/device-management-introduction/02.png)


<span data-ttu-id="aaac4-143">Essas metas são realizadas por fornecer aos usuários uma experiência de autoatendimento para obtenção de dispositivos de propriedade do trabalho sob o controle de saudação do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="aaac4-143">These goals are accomplished by providing your users with a self-service experience for getting work-owned devices under hello control of Azure AD.</span></span>  
<span data-ttu-id="aaac4-144">A **adição ao Azure AD** destina-se a organizações que usam somente a nuvem/priorizam a nuvem.</span><span class="sxs-lookup"><span data-stu-id="aaac4-144">**Azure AD Join** is intended for organizations that are cloud-first / cloud-only.</span></span> <span data-ttu-id="aaac4-145">Normalmente, são pequenas e médias empresas, que não têm uma infraestrutura do Active Directory local para Windows Server.</span><span class="sxs-lookup"><span data-stu-id="aaac4-145">These are typically small- and medium-sized businesses that do not have an on-premises Windows Server Active Directory infrastructure.</span></span> 

<span data-ttu-id="aaac4-146">Dispositivos do AD do Azure associado a implementação fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="aaac4-146">Implementing Azure AD joined devices provides you with hello following benefits:</span></span>

- <span data-ttu-id="aaac4-147">**Logon único (SSO)** tooyour Azure gerenciados serviços e aplicativos SaaS.</span><span class="sxs-lookup"><span data-stu-id="aaac4-147">**Single-Sign-On (SSO)** tooyour Azure managed SaaS apps and services.</span></span> <span data-ttu-id="aaac4-148">Os usuários não visualizam solicitações adicionais de autenticação ao acessar recursos de trabalho.</span><span class="sxs-lookup"><span data-stu-id="aaac4-148">Your users don’t see additional authentication prompts when accessing work resources.</span></span> <span data-ttu-id="aaac4-149">Olá funcionalidade de SSO é mesmo quando não estiverem conectados toohello rede de domínio disponível.</span><span class="sxs-lookup"><span data-stu-id="aaac4-149">hello SSO functionality is even when they are not connected toohello domain network available.</span></span>

- <span data-ttu-id="aaac4-150">**Roaming em conformidade corporativa** das configurações de usuário entre dispositivos adicionados.</span><span class="sxs-lookup"><span data-stu-id="aaac4-150">**Enterprise compliant roaming** of user settings across joined devices.</span></span> <span data-ttu-id="aaac4-151">Os usuários não precisam tooconnect configurações de toosee de conta (por exemplo, Hotmail) um Microsoft em todos os dispositivos.</span><span class="sxs-lookup"><span data-stu-id="aaac4-151">Users don’t need tooconnect a Microsoft account (for example, Hotmail) toosee settings across devices.</span></span>

- <span data-ttu-id="aaac4-152">**Acesso tooWindows Store para empresas** usando a conta do AD.</span><span class="sxs-lookup"><span data-stu-id="aaac4-152">**Access tooWindows Store for Business** using AD account.</span></span> <span data-ttu-id="aaac4-153">Os usuários podem escolher entre um inventário dos aplicativos pré-selecionada pela organização hello.</span><span class="sxs-lookup"><span data-stu-id="aaac4-153">Your users can choose from an inventory of applications pre-selected by hello organization.</span></span>

- <span data-ttu-id="aaac4-154">**Windows Hello** suporte para recursos de toowork acesso seguro e conveniente.</span><span class="sxs-lookup"><span data-stu-id="aaac4-154">**Windows Hello** support for secure and convenient access toowork resources.</span></span>

- <span data-ttu-id="aaac4-155">**Restrição de acesso** tooapps de apenas os dispositivos que atendem à política de conformidade.</span><span class="sxs-lookup"><span data-stu-id="aaac4-155">**Restriction of access** tooapps from only devices that meet compliance policy.</span></span>

<span data-ttu-id="aaac4-156">Embora a adição ao Azure AD se destine basicamente às organizações que não têm uma infraestrutura do Active Directory local para Windows Server, você certamente também pode usá-la em cenários em que:</span><span class="sxs-lookup"><span data-stu-id="aaac4-156">While Azure AD join is primarily intended for organizations that do not have an on-premises Windows Server Active Directory infrastructure, you can certainly also use it in scenarios where:</span></span>

- <span data-ttu-id="aaac4-157">Você não pode usar uma junção de domínio local, por exemplo, se você precisar de tooget de dispositivos móveis, como tablets e celulares sob controle.</span><span class="sxs-lookup"><span data-stu-id="aaac4-157">You can’t use an on-premises domain join, for example, if you need tooget mobile devices such as tablets and phones under control.</span></span>

- <span data-ttu-id="aaac4-158">Os usuários precisam ter principalmente tooaccess Office 365 ou outros aplicativos SaaS integrados ao AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="aaac4-158">Your users primarily need tooaccess Office 365 or other SaaS apps integrated with Azure AD.</span></span>

- <span data-ttu-id="aaac4-159">Você deseja toomanage um grupo de usuários no AD do Azure, em vez de no Active Directory.</span><span class="sxs-lookup"><span data-stu-id="aaac4-159">You want toomanage a group of users in Azure AD instead of in Active Directory.</span></span> <span data-ttu-id="aaac4-160">Isso pode se aplicar, por exemplo, tooseasonal funcionários, prestadores de serviço ou os alunos.</span><span class="sxs-lookup"><span data-stu-id="aaac4-160">This can apply, for example, tooseasonal workers, contractors, or students.</span></span>

- <span data-ttu-id="aaac4-161">Você deseja tooprovide junção recursos tooworkers em filiais remotas com a infraestrutura limitada local.</span><span class="sxs-lookup"><span data-stu-id="aaac4-161">You want tooprovide joining capabilities tooworkers in remote branch offices with limited on-premises infrastructure.</span></span>

<span data-ttu-id="aaac4-162">Você pode configurar dispositivos adicionados ao Azure AD para dispositivos com Windows 10.</span><span class="sxs-lookup"><span data-stu-id="aaac4-162">You can configure Azure AD joined devices for Windows 10 devices.</span></span>


## <a name="hybrid-azure-ad-joined-devices"></a><span data-ttu-id="aaac4-163">Dispositivos adicionados ao Azure AD híbrido</span><span class="sxs-lookup"><span data-stu-id="aaac4-163">Hybrid Azure AD joined devices</span></span>

<span data-ttu-id="aaac4-164">Para mais de uma década, muitas organizações usou Olá domínio junção tootheir local do Active Directory tooenable:</span><span class="sxs-lookup"><span data-stu-id="aaac4-164">For more than a decade, many organizations have used hello domain join tootheir on-premises Active Directory tooenable:</span></span>

- <span data-ttu-id="aaac4-165">IT departamentos toomanage trabalho dispositivos de propriedade de um local central.</span><span class="sxs-lookup"><span data-stu-id="aaac4-165">IT departments toomanage work-owned devices from a central location.</span></span>

- <span data-ttu-id="aaac4-166">Os usuários toosign em dispositivos de tootheir com seu Active Directory ou de estudante contas.</span><span class="sxs-lookup"><span data-stu-id="aaac4-166">Users toosign in tootheir devices with their Active Directory work or school accounts.</span></span> 

<span data-ttu-id="aaac4-167">Normalmente, as organizações com um volume no local dependem de métodos tooprovision dispositivos de imagem e geralmente usam **System Center Configuration Manager (SCCM)** ou **(GP) da política de grupo** toomanage -los.</span><span class="sxs-lookup"><span data-stu-id="aaac4-167">Typically, organizations with an on-premises footprint rely on imaging methods tooprovision devices, and they often use **System Center Configuration Manager (SCCM)** or **group policy (GP)** toomanage them.</span></span>

<span data-ttu-id="aaac4-168">Se seu ambiente tiver um local espaço AD e você também desejar que se beneficiam de recursos de saudação fornecidos pelo Active Directory do Azure, você pode implementar dispositivos do AD do Azure associado híbrida.</span><span class="sxs-lookup"><span data-stu-id="aaac4-168">If your environment has an on-premises AD footprint and you also want benefit from hello capabilities provided by Azure Active Directory, you can implement hybrid Azure AD joined devices.</span></span> <span data-ttu-id="aaac4-169">Esses são dispositivos que são ambos, tooyour ingressado no Active Directory local e o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="aaac4-169">These are devices that are both, joined tooyour on-premises Active Directory and your Azure Active Directory.</span></span>

![Dispositivos registrados no Azure AD](./media/device-management-introduction/01.png)


<span data-ttu-id="aaac4-171">Você deverá usar dispositivos adicionados ao Azure AD híbrido se:</span><span class="sxs-lookup"><span data-stu-id="aaac4-171">You should use Azure AD hybrid joined devices if:</span></span>

- <span data-ttu-id="aaac4-172">Você tem dispositivos Win32 de toothese implantado de aplicativos que usam NTLM / Kerberos.</span><span class="sxs-lookup"><span data-stu-id="aaac4-172">You have Win32 apps deployed toothese devices that use NTLM / Kerberos.</span></span>

- <span data-ttu-id="aaac4-173">Você precisar de GP ou SCCM / dispositivos de toomanage do DCM.</span><span class="sxs-lookup"><span data-stu-id="aaac4-173">You require GP or SCCM / DCM toomanage devices.</span></span>

- <span data-ttu-id="aaac4-174">Você deseja que os dispositivos toocontinue tooconfigure soluções, geração de imagens toouse para seus funcionários.</span><span class="sxs-lookup"><span data-stu-id="aaac4-174">You want toocontinue toouse imaging solutions tooconfigure devices for your employees.</span></span>

<span data-ttu-id="aaac4-175">É possível configurar dispositivos adicionados ao Azure AD para dispositivos com Windows 10 e de nível inferior, como Windows 8 e Windows 7.</span><span class="sxs-lookup"><span data-stu-id="aaac4-175">You can configure Hybrid Azure AD joined devices for Windows 10 and down-level devices such as Windows 8 and Windows 7.</span></span>

## <a name="summary"></a><span data-ttu-id="aaac4-176">Resumo</span><span class="sxs-lookup"><span data-stu-id="aaac4-176">Summary</span></span>

<span data-ttu-id="aaac4-177">Com o gerenciamento de dispositivo no Azure AD, é possível:</span><span class="sxs-lookup"><span data-stu-id="aaac4-177">With device management in Azure AD, you can:</span></span> 

- <span data-ttu-id="aaac4-178">Simplificar o processo de saudação de colocar os dispositivos sob o controle de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="aaac4-178">Simplify hello process of bringing devices under hello control of Azure AD</span></span>

- <span data-ttu-id="aaac4-179">Fornecer aos usuários com recursos de baseado em nuvem da organização toouse fácil acesso tooyour</span><span class="sxs-lookup"><span data-stu-id="aaac4-179">Provide your users with an easy toouse access tooyour organization’s cloud-based resources</span></span>

<span data-ttu-id="aaac4-180">Como uma regra prática, você deve usar:</span><span class="sxs-lookup"><span data-stu-id="aaac4-180">As a rule of a thumb, you should use:</span></span>

- <span data-ttu-id="aaac4-181">Dispositivos registrados no Azure AD para dispositivos pessoais</span><span class="sxs-lookup"><span data-stu-id="aaac4-181">Azure AD registered devices for personal devices</span></span>

- <span data-ttu-id="aaac4-182">AD do Azure associado dispositivos para dispositivos que não estão ligados tooan AD local</span><span class="sxs-lookup"><span data-stu-id="aaac4-182">Azure AD joined devices for devices that are not joined tooan on-premises AD</span></span> 

- <span data-ttu-id="aaac4-183">Híbrido do AD do Azure associado dispositivos para dispositivos que estão ligados tooan AD local</span><span class="sxs-lookup"><span data-stu-id="aaac4-183">Hybrid Azure AD joined devices for devices that are joined tooan on-premises AD</span></span>     




## <a name="next-steps"></a><span data-ttu-id="aaac4-184">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="aaac4-184">Next steps</span></span>

- <span data-ttu-id="aaac4-185">tooget uma visão geral de como o dispositivo toomanage no hello Azure portal, consulte [gerenciamento de dispositivos usando Olá portal do Azure](device-management-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="aaac4-185">tooget an overview of how toomanage device in hello Azure portal, see [managing devices using hello Azure portal](device-management-azure-portal.md)</span></span>

- <span data-ttu-id="aaac4-186">toolearn mais sobre o acesso condicional com base no dispositivo, consulte [configurar políticas de acesso condicional com base no dispositivo do Active Directory do Azure](active-directory-conditional-access-policy-connected-applications.md).</span><span class="sxs-lookup"><span data-stu-id="aaac4-186">toolearn more about device-based conditional access, see [configure Azure Active Directory device-based conditional access policies](active-directory-conditional-access-policy-connected-applications.md).</span></span>

- <span data-ttu-id="aaac4-187">toosetup híbrido do Azure AD associado dispositivos, consulte [como tooconfigure híbrida do Active Directory do Azure associados dispositivos](device-management-hybrid-azuread-joined-devices-setup.md).</span><span class="sxs-lookup"><span data-stu-id="aaac4-187">toosetup hybrid Azure AD joined devices, see [how tooconfigure hybrid Azure Active Directory joined devices](device-management-hybrid-azuread-joined-devices-setup.md).</span></span>


