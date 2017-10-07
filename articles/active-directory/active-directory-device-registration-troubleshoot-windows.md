---
title: "aaaTroubleshooting Olá o registro automático de domínio do AD do Azure em computadores ingressados para Windows 10 e Windows Server 2016 | Microsoft Docs"
description: "Solucionando problemas de registro automático de saudação do domínio do AD do Azure em computadores ingressados para Windows 10 e Windows Server 2016."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 3795323ce9392368b412b3e1208868431e59a74b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-tooazure-ad--windows-10-and-windows-server-2016"></a><span data-ttu-id="e7bab-103">Solucionando problemas de registro automático de domínio Unido computadores tooAzure AD – Windows 10 e Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="e7bab-103">Troubleshooting auto-registration of domain joined computers tooAzure AD – Windows 10 and Windows Server 2016</span></span>

<span data-ttu-id="e7bab-104">Este tópico é aplicável toohello clientes a seguir:</span><span class="sxs-lookup"><span data-stu-id="e7bab-104">This topic is applicable toohello following clients:</span></span>

-   <span data-ttu-id="e7bab-105">Windows 10</span><span class="sxs-lookup"><span data-stu-id="e7bab-105">Windows 10</span></span>
-   <span data-ttu-id="e7bab-106">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="e7bab-106">Windows Server 2016</span></span>

<span data-ttu-id="e7bab-107">Para outros clientes do Windows, consulte [Solucionando problemas de registro automático de domínio Unido computadores tooAzure AD para clientes de nível inferior do Windows](active-directory-device-registration-troubleshoot-windows-legacy.md).</span><span class="sxs-lookup"><span data-stu-id="e7bab-107">For other Windows clients, see [Troubleshooting auto-registration of domain joined computers tooAzure AD for Windows down-level clients](active-directory-device-registration-troubleshoot-windows-legacy.md).</span></span>

<span data-ttu-id="e7bab-108">Este tópico pressupõe que você tenha configurado o registro automático de dispositivos que ingressaram no domínio conforme descrito em descrito em [como tooconfigure o registro automático do Windows ingressado no domínio dispositivos com o Active Directory do Azure](active-directory-device-registration-get-started.md) Olá toosupport os seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="e7bab-108">This topic assumes that you have configured auto-registration of domain-joined devices as outlined in described in [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-device-registration-get-started.md) toosupport hello following scenarios:</span></span>

- [<span data-ttu-id="e7bab-109">Acesso condicional com base em dispositivo</span><span class="sxs-lookup"><span data-stu-id="e7bab-109">Device-based conditional access</span></span>](active-directory-conditional-access-automatic-device-registration-setup.md)

- [<span data-ttu-id="e7bab-110">Roaming corporativo de configurações</span><span class="sxs-lookup"><span data-stu-id="e7bab-110">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="e7bab-111">Configurar o Hello for Business</span><span class="sxs-lookup"><span data-stu-id="e7bab-111">Windows Hello for Business</span></span>](active-directory-azureadjoin-passport-deployment.md)


<span data-ttu-id="e7bab-112">Este documento fornece orientação para solução de problemas sobre como tooresolve potenciais problemas.</span><span class="sxs-lookup"><span data-stu-id="e7bab-112">This document provides troubleshooting guidance on how tooresolve potential issues.</span></span> 

<span data-ttu-id="e7bab-113">Olá registro tem suporte no Windows hello atualização 10 de novembro de 2015 e superior.</span><span class="sxs-lookup"><span data-stu-id="e7bab-113">hello registration is supported in hello Windows 10 November 2015 Update and above.</span></span>  
<span data-ttu-id="e7bab-114">É recomendável usar saudação da atualização de aniversário para habilitar cenários de saudação acima.</span><span class="sxs-lookup"><span data-stu-id="e7bab-114">We recommend using hello Anniversary Update for enabling hello scenarios above.</span></span>

## <a name="step-1-retrieve-hello-registration-status"></a><span data-ttu-id="e7bab-115">Etapa 1: Recuperar o status de registro de saudação</span><span class="sxs-lookup"><span data-stu-id="e7bab-115">Step 1: Retrieve hello registration status</span></span> 

<span data-ttu-id="e7bab-116">**status do registro Olá tooretrieve:**</span><span class="sxs-lookup"><span data-stu-id="e7bab-116">**tooretrieve hello registration status:**</span></span>

1. <span data-ttu-id="e7bab-117">Olá abrir o prompt de comando como administrador.</span><span class="sxs-lookup"><span data-stu-id="e7bab-117">Open hello command prompt as an administrator.</span></span>

2. <span data-ttu-id="e7bab-118">Digite **dsregcmd /status**</span><span class="sxs-lookup"><span data-stu-id="e7bab-118">Type **dsregcmd /status**</span></span>



    <span data-ttu-id="e7bab-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="e7bab-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span></span>
    
        AzureAdJoined : YES
     <span data-ttu-id="e7bab-120">EnterpriseJoined: Nenhum DeviceId: impressão digital de 5820fbe9-60c8-43b0-bb11-44aee233e4e7: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: TpmProtected de provedor de criptografia da plataforma Microsoft: Sim KeySignTest:: deve executar com privilégios elevados tootest.</span><span class="sxs-lookup"><span data-stu-id="e7bab-120">EnterpriseJoined : NO DeviceId : 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint : B753A6679CE720451921302CA873794D94C6204A KeyContainerId : bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider : Microsoft Platform Crypto Provider TpmProtected : YES KeySignTest: : MUST Run elevated tootest.</span></span>
                  <span data-ttu-id="e7bab-121">Idp : login.windows.net TenantId : 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName : Contoso AuthCodeUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl : https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl : https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl : https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl : eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion : 1.0 JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion : 1.0 KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId : urn:ms-drs:enterpriseregistration.windows.net DomainJoined : YES DomainName : CONTOSO</span><span class="sxs-lookup"><span data-stu-id="e7bab-121">Idp : login.windows.net TenantId : 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName : Contoso AuthCodeUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl : https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl : https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl : https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl : eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion : 1.0 JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion : 1.0 KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId : urn:ms-drs:enterpriseregistration.windows.net DomainJoined : YES DomainName : CONTOSO</span></span>
    
    <span data-ttu-id="e7bab-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="e7bab-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span></span>
    
                 NgcSet : YES
               NgcKeyId : {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined : NO
          WamDefaultSet : YES
    <span data-ttu-id="e7bab-123">WamDefaultAuthority : organizations         WamDefaultId : https://login.microsoft.com       WamDefaultGUID : {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt : YES</span><span class="sxs-lookup"><span data-stu-id="e7bab-123">WamDefaultAuthority : organizations         WamDefaultId : https://login.microsoft.com       WamDefaultGUID : {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt : YES</span></span>



## <a name="step-2-evaluate-hello-registration-status"></a><span data-ttu-id="e7bab-124">Etapa 2: Avaliar o status de registro de saudação</span><span class="sxs-lookup"><span data-stu-id="e7bab-124">Step 2: Evaluate hello registration status</span></span> 

<span data-ttu-id="e7bab-125">Examine Olá campos a seguir e certifique-se de que eles têm valores esperados de saudação:</span><span class="sxs-lookup"><span data-stu-id="e7bab-125">Review hello following fields and make sure that they have hello expected values:</span></span>

### <a name="azureadjoined--yes"></a><span data-ttu-id="e7bab-126">AzureAdJoined : YES</span><span class="sxs-lookup"><span data-stu-id="e7bab-126">AzureAdJoined : YES</span></span>  

<span data-ttu-id="e7bab-127">Este campo mostra se o dispositivo de saudação é registrado no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="e7bab-127">This field shows whether hello device is registered with Azure AD.</span></span> <span data-ttu-id="e7bab-128">Se o valor de saudação mostra como 'Não', o registro não foi concluída.</span><span class="sxs-lookup"><span data-stu-id="e7bab-128">If hello value shows as ‘NO’, registration has not completed.</span></span> 

<span data-ttu-id="e7bab-129">**Possíveis causas:**</span><span class="sxs-lookup"><span data-stu-id="e7bab-129">**Possible causes:**</span></span>

- <span data-ttu-id="e7bab-130">Falha na autenticação de computador Olá para o registro.</span><span class="sxs-lookup"><span data-stu-id="e7bab-130">Authentication of hello computer for registration failed.</span></span>

- <span data-ttu-id="e7bab-131">Há um proxy HTTP na organização Olá que não pode ser descoberta pelo computador Olá</span><span class="sxs-lookup"><span data-stu-id="e7bab-131">There is an HTTP proxy in hello organization that cannot be discovered by hello computer</span></span>

- <span data-ttu-id="e7bab-132">computador Olá não pode chegar Azure AD para autenticação ou do Azure DRS para registro</span><span class="sxs-lookup"><span data-stu-id="e7bab-132">hello computer cannot reach Azure AD for authentication or Azure DRS for registration</span></span>

- <span data-ttu-id="e7bab-133">Olá computador podem não estar na rede interna da organização hello ou em VPN com a linha direta de visão tooan controlador de domínio do AD local.</span><span class="sxs-lookup"><span data-stu-id="e7bab-133">hello computer may not be on hello organization’s internal network or on VPN with direct line of sight tooan on-premises AD domain controller.</span></span>

- <span data-ttu-id="e7bab-134">Se o computador Olá tem um TPM, é possível em um estado inválido.</span><span class="sxs-lookup"><span data-stu-id="e7bab-134">If hello computer has a TPM, it may be in a bad state.</span></span>

- <span data-ttu-id="e7bab-135">Pode haver um erro de configuração nos serviços observado anteriormente no documento de saudação que você precisará tooverify novamente.</span><span class="sxs-lookup"><span data-stu-id="e7bab-135">There may be a misconfiguration in services noted in hello document earlier that you will need tooverify again.</span></span> <span data-ttu-id="e7bab-136">Alguns exemplos comuns são:</span><span class="sxs-lookup"><span data-stu-id="e7bab-136">Common examples are:</span></span>

    - <span data-ttu-id="e7bab-137">O servidor de Federação não tem pontos de extremidade WS-Trust habilitados</span><span class="sxs-lookup"><span data-stu-id="e7bab-137">Your federation server does not have WS-Trust endpoints enabled</span></span>

    - <span data-ttu-id="e7bab-138">O servidor de federação pode não permitir a autenticação de entrada de computadores na rede usando a Autenticação Integrada do Windows.</span><span class="sxs-lookup"><span data-stu-id="e7bab-138">Your federation server may not allow inbound authentication from computers in your network using Integrated Windows Authentication.</span></span>

    - <span data-ttu-id="e7bab-139">Não há nenhum objeto de ponto de Conexão de serviço que aponta para o nome de domínio verificado tooyour no AD do Azure na floresta Olá AD qual pertence o computador de saudação</span><span class="sxs-lookup"><span data-stu-id="e7bab-139">There is no Service Connection Point object that points tooyour verified domain name in Azure AD in hello AD forest where hello computer belongs to</span></span>

---

### <a name="domainjoined--yes"></a><span data-ttu-id="e7bab-140">DomainJoined : YES</span><span class="sxs-lookup"><span data-stu-id="e7bab-140">DomainJoined : YES</span></span>  

<span data-ttu-id="e7bab-141">Este campo mostra se o dispositivo Olá é tooan ingressado no Active Directory local ou não.</span><span class="sxs-lookup"><span data-stu-id="e7bab-141">This field shows whether hello device is joined tooan on-premises Active Directory or not.</span></span> <span data-ttu-id="e7bab-142">Se o valor de saudação mostra como **não**, dispositivo Olá não é automaticamente o registro com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7bab-142">If hello value shows as **NO**, hello device cannot auto-register with Azure AD.</span></span> <span data-ttu-id="e7bab-143">Verifique primeiro toohello de associações de dispositivo que Olá local do Active Directory para que ele possa registrar com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e7bab-143">Check first that hello device joins toohello on-premises Active Directory before it can register with Azure AD.</span></span> <span data-ttu-id="e7bab-144">Se você estiver procurando unindo Olá computador tooAzure AD diretamente, vá tooLearn sobre recursos de junção do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e7bab-144">If you are looking for joining hello computer tooAzure AD directly, please go tooLearn about capabilities of Azure Active Directory Join.</span></span>

---

### <a name="workplacejoined--no"></a><span data-ttu-id="e7bab-145">WorkplaceJoined : NO</span><span class="sxs-lookup"><span data-stu-id="e7bab-145">WorkplaceJoined : NO</span></span>  

<span data-ttu-id="e7bab-146">Este campo mostra se o dispositivo de saudação está registrado com o AD do Azure, mas como um dispositivo pessoal (marcado como 'Ingressou no local de trabalho').</span><span class="sxs-lookup"><span data-stu-id="e7bab-146">This field shows whether hello device is registered with Azure AD but as a personal device (marked as ‘Workplace Joined’).</span></span> <span data-ttu-id="e7bab-147">Se esse valor deve aparecer como 'Não' para um computador ingressado no domínio registrado com o Azure AD, porém se ele mostra como Sim, isso significa que uma conta corporativa ou escolar foi concluído o registro do computador adicionado toohello anterior.</span><span class="sxs-lookup"><span data-stu-id="e7bab-147">If this value should show as ‘NO’ for a domain joined computer registered with Azure AD, however if it shows as YES it means that a work or school account was added prior toohello computer completing registration.</span></span> <span data-ttu-id="e7bab-148">Nesse caso a conta de saudação será ignorada se usando a versão de atualização de aniversário de saudação do Windows 10 (1607 quando executar comando de WinVer Olá em Olá janela 'Executar' ou em uma janela de prompt de comando).</span><span class="sxs-lookup"><span data-stu-id="e7bab-148">In this case hello account will be ignored if using hello Anniversary Update version of Windows 10 (1607 when running hello WinVer command in hello ‘Run’ window or a command prompt window).</span></span>

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a><span data-ttu-id="e7bab-149">WamDefaultSet : YES e AzureADPrt : YES</span><span class="sxs-lookup"><span data-stu-id="e7bab-149">WamDefaultSet : YES and AzureADPrt : YES</span></span>
  
<span data-ttu-id="e7bab-150">Esses campos mostram que o usuário Olá foi autenticado com êxito tooAzure AD ao fazer logon no dispositivo toohello.</span><span class="sxs-lookup"><span data-stu-id="e7bab-150">These fields show that hello user has successfully authenticated tooAzure AD upon signing in toohello device.</span></span> <span data-ttu-id="e7bab-151">Se elas mostram 'Nenhum' hello seguem as possíveis causas:</span><span class="sxs-lookup"><span data-stu-id="e7bab-151">If they show ‘NO’ hello following are possible causes:</span></span>

- <span data-ttu-id="e7bab-152">Chave de armazenamento incorreta (STK) no TPM associado Olá dispositivo após o registro (seleção Olá KeySignTest durante a execução com privilégios elevados).</span><span class="sxs-lookup"><span data-stu-id="e7bab-152">Bad storage key (STK) in TPM associated with hello device upon registration (check hello KeySignTest while running elevated).</span></span>

- <span data-ttu-id="e7bab-153">ID de logon alternativo</span><span class="sxs-lookup"><span data-stu-id="e7bab-153">Alternate Login ID</span></span>

- <span data-ttu-id="e7bab-154">Proxy HTTP não encontrado</span><span class="sxs-lookup"><span data-stu-id="e7bab-154">HTTP Proxy not found</span></span>

## <a name="next-steps"></a><span data-ttu-id="e7bab-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e7bab-155">Next steps</span></span>

<span data-ttu-id="e7bab-156">Para obter mais informações, consulte Olá [perguntas frequentes sobre o registro de dispositivo automático](active-directory-device-registration-faq.md)</span><span class="sxs-lookup"><span data-stu-id="e7bab-156">For more information, see hello [Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span> 
