---
title: "aaaTroubleshooting híbrida do Active Directory do Azure associado a dispositivos Windows 10 e Windows Server 2016 | Microsoft Docs"
description: "Solução de problemas do Azure Active Directory híbrido ingressado em dispositivos do Windows 10 e do Windows Server 2016."
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
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: cc252d1d0684d6632694afc8a367327794228c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-windows-10-and-windows-server-2016-devices"></a><span data-ttu-id="07e65-103">Solução de problemas do Azure Active Directory híbrido ingressado em dispositivos do Windows 10 e do Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="07e65-103">Troubleshooting hybrid Azure Active Directory joined Windows 10 and Windows Server 2016 devices</span></span> 

<span data-ttu-id="07e65-104">Este tópico é aplicável toohello clientes a seguir:</span><span class="sxs-lookup"><span data-stu-id="07e65-104">This topic is applicable toohello following clients:</span></span>

-   <span data-ttu-id="07e65-105">Windows 10</span><span class="sxs-lookup"><span data-stu-id="07e65-105">Windows 10</span></span>
-   <span data-ttu-id="07e65-106">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="07e65-106">Windows Server 2016</span></span>

<span data-ttu-id="07e65-107">Para outros clientes do Windows, consulte [Solução de problemas do Azure Active Directory híbrido ingressado em dispositivos de nível inferior](device-management-troubleshoot-hybrid-join-windows-legacy.md).</span><span class="sxs-lookup"><span data-stu-id="07e65-107">For other Windows clients, see [Troubleshooting hybrid Azure Active Directory joined down-level devices](device-management-troubleshoot-hybrid-join-windows-legacy.md).</span></span>

<span data-ttu-id="07e65-108">Este tópico pressupõe que você tenha [dispositivos ingressados no configurado híbrida do Active Directory do Azure](device-management-hybrid-azuread-joined-devices-setup.md) Olá toosupport os seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="07e65-108">This topic assumes that you have [configured hybrid Azure Active Directory joined devices](device-management-hybrid-azuread-joined-devices-setup.md) toosupport hello following scenarios:</span></span>

- <span data-ttu-id="07e65-109">Acesso condicional com base em dispositivo</span><span class="sxs-lookup"><span data-stu-id="07e65-109">Device-based conditional access</span></span>

- [<span data-ttu-id="07e65-110">Roaming corporativo de configurações</span><span class="sxs-lookup"><span data-stu-id="07e65-110">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="07e65-111">Configurar o Hello for Business</span><span class="sxs-lookup"><span data-stu-id="07e65-111">Windows Hello for Business</span></span>](active-directory-azureadjoin-passport-deployment.md)


<span data-ttu-id="07e65-112">Este documento fornece orientação para solução de problemas sobre como tooresolve potenciais problemas.</span><span class="sxs-lookup"><span data-stu-id="07e65-112">This document provides troubleshooting guidance on how tooresolve potential issues.</span></span> 


<span data-ttu-id="07e65-113">Para Windows 10 e Windows Server 2016, híbrido do Azure Active Directory junção dá suporte a saudação Windows 10 de novembro de 2015 atualizar e acima.</span><span class="sxs-lookup"><span data-stu-id="07e65-113">For Windows 10 and Windows Server 2016, hybrid Azure Active Directory join supports hello Windows 10 November 2015 Update and above.</span></span> <span data-ttu-id="07e65-114">Recomendamos o uso da atualização de aniversário hello.</span><span class="sxs-lookup"><span data-stu-id="07e65-114">We recommend using hello Anniversary update.</span></span>

## <a name="step-1-retrieve-hello-join-status"></a><span data-ttu-id="07e65-115">Etapa 1: Recuperar o status de junção Olá</span><span class="sxs-lookup"><span data-stu-id="07e65-115">Step 1: Retrieve hello join status</span></span> 

<span data-ttu-id="07e65-116">**status de junção de saudação tooretrieve:**</span><span class="sxs-lookup"><span data-stu-id="07e65-116">**tooretrieve hello join status:**</span></span>

1. <span data-ttu-id="07e65-117">Olá abrir o prompt de comando como administrador</span><span class="sxs-lookup"><span data-stu-id="07e65-117">Open hello command prompt as an administrator</span></span>

2. <span data-ttu-id="07e65-118">Digite **dsregcmd /status**</span><span class="sxs-lookup"><span data-stu-id="07e65-118">Type **dsregcmd /status**</span></span>



    <span data-ttu-id="07e65-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="07e65-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span></span>
    
        AzureAdJoined: YES
     <span data-ttu-id="07e65-120">EnterpriseJoined: Nenhum DeviceId: impressão digital de 5820fbe9-60c8-43b0-bb11-44aee233e4e7: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: TpmProtected de provedor de criptografia da plataforma Microsoft: Sim KeySignTest:: deve executar com privilégios elevados tootest.</span><span class="sxs-lookup"><span data-stu-id="07e65-120">EnterpriseJoined: NO DeviceId: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: Microsoft Platform Crypto Provider TpmProtected: YES KeySignTest: : MUST Run elevated tootest.</span></span>
                  <span data-ttu-id="07e65-121">Idp: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn:ms-drs:enterpriseregistration.windows.net DomainJoined: YES DomainName: CONTOSO</span><span class="sxs-lookup"><span data-stu-id="07e65-121">Idp: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn:ms-drs:enterpriseregistration.windows.net DomainJoined: YES DomainName: CONTOSO</span></span>
    
    <span data-ttu-id="07e65-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="07e65-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span></span>
    
                 NgcSet: YES
               NgcKeyId: {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined: NO
          WamDefaultSet: YES
    <span data-ttu-id="07e65-123">WamDefaultAuthority: organizations         WamDefaultId: https://login.microsoft.com       WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt: YES</span><span class="sxs-lookup"><span data-stu-id="07e65-123">WamDefaultAuthority: organizations         WamDefaultId: https://login.microsoft.com       WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt: YES</span></span>



## <a name="step-2-evaluate-hello-join-status"></a><span data-ttu-id="07e65-124">Etapa 2: Avaliar o status de junção Olá</span><span class="sxs-lookup"><span data-stu-id="07e65-124">Step 2: Evaluate hello join status</span></span> 

<span data-ttu-id="07e65-125">Examine Olá campos a seguir e certifique-se de que eles têm valores esperados de saudação:</span><span class="sxs-lookup"><span data-stu-id="07e65-125">Review hello following fields and make sure that they have hello expected values:</span></span>

### <a name="azureadjoined--yes"></a><span data-ttu-id="07e65-126">AzureAdJoined : YES</span><span class="sxs-lookup"><span data-stu-id="07e65-126">AzureAdJoined : YES</span></span>  

<span data-ttu-id="07e65-127">Este campo indica se o dispositivo de saudação é associado com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07e65-127">This field indicates whether hello device is joined with Azure AD.</span></span> <span data-ttu-id="07e65-128">Se o valor de saudação é **não**, Olá tooAzure junção AD ainda não foi concluída.</span><span class="sxs-lookup"><span data-stu-id="07e65-128">If hello value is **NO**, hello join tooAzure AD has not completed yet.</span></span> 

<span data-ttu-id="07e65-129">**Possíveis causas:**</span><span class="sxs-lookup"><span data-stu-id="07e65-129">**Possible causes:**</span></span>

- <span data-ttu-id="07e65-130">Falha na autenticação de computador Olá para uma junção.</span><span class="sxs-lookup"><span data-stu-id="07e65-130">Authentication of hello computer for a join failed.</span></span>

- <span data-ttu-id="07e65-131">Há um proxy HTTP na organização Olá que não pode ser descoberta pelo computador Olá</span><span class="sxs-lookup"><span data-stu-id="07e65-131">There is an HTTP proxy in hello organization that cannot be discovered by hello computer</span></span>

- <span data-ttu-id="07e65-132">computador Olá não pode chegar tooauthenticate do AD do Azure ou Azure DRS para registro</span><span class="sxs-lookup"><span data-stu-id="07e65-132">hello computer cannot reach Azure AD tooauthenticate or Azure DRS for registration</span></span>

- <span data-ttu-id="07e65-133">Olá computador podem não estar na rede interna da organização hello ou em VPN com a linha direta de visão tooan controlador de domínio do AD local.</span><span class="sxs-lookup"><span data-stu-id="07e65-133">hello computer may not be on hello organization’s internal network or on VPN with direct line of sight tooan on-premises AD domain controller.</span></span>

- <span data-ttu-id="07e65-134">Se o computador de saudação tiver um TPM, ele pode ser em um estado inválido.</span><span class="sxs-lookup"><span data-stu-id="07e65-134">If hello computer has a TPM, it can be in a bad state.</span></span>

- <span data-ttu-id="07e65-135">Pode haver um erro de configuração nos serviços de saudação observado anteriormente no documento de saudação que você precisará tooverify novamente.</span><span class="sxs-lookup"><span data-stu-id="07e65-135">There might be a misconfiguration in hello services noted in hello document earlier that you will need tooverify again.</span></span> <span data-ttu-id="07e65-136">Alguns exemplos comuns são:</span><span class="sxs-lookup"><span data-stu-id="07e65-136">Common examples are:</span></span>

    - <span data-ttu-id="07e65-137">O servidor de Federação não tem pontos de extremidade WS-Trust habilitados</span><span class="sxs-lookup"><span data-stu-id="07e65-137">Your federation server does not have WS-Trust endpoints enabled</span></span>

    - <span data-ttu-id="07e65-138">O servidor de federação não permite a autenticação de entrada de computadores em sua rede usando a Autenticação Integrada do Windows.</span><span class="sxs-lookup"><span data-stu-id="07e65-138">Your federation server does not allow inbound authentication from computers in your network using Integrated Windows Authentication.</span></span>

    - <span data-ttu-id="07e65-139">Não há nenhum objeto de ponto de Conexão de serviço que aponta para o nome de domínio verificado tooyour no AD do Azure na floresta Olá AD qual pertence o computador de saudação</span><span class="sxs-lookup"><span data-stu-id="07e65-139">There is no Service Connection Point object that points tooyour verified domain name in Azure AD in hello AD forest where hello computer belongs to</span></span>

---

### <a name="domainjoined--yes"></a><span data-ttu-id="07e65-140">DomainJoined : YES</span><span class="sxs-lookup"><span data-stu-id="07e65-140">DomainJoined : YES</span></span>  

<span data-ttu-id="07e65-141">Este campo indica se o dispositivo Olá é associado tooan local do Active Directory ou não.</span><span class="sxs-lookup"><span data-stu-id="07e65-141">This field indicates whether hello device is joined tooan on-premises Active Directory or not.</span></span> <span data-ttu-id="07e65-142">Se o valor de saudação é **não**, dispositivo Olá não é possível executar uma junção híbrido do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="07e65-142">If hello value is **NO**, hello device cannot perform a hybrid Azure AD join.</span></span>  

---

### <a name="workplacejoined--no"></a><span data-ttu-id="07e65-143">WorkplaceJoined : NO</span><span class="sxs-lookup"><span data-stu-id="07e65-143">WorkplaceJoined : NO</span></span>  

<span data-ttu-id="07e65-144">Este campo indica se o dispositivo hello está registrado com o Azure AD como um dispositivo pessoal (marcados como *ingressado no local de trabalho*).</span><span class="sxs-lookup"><span data-stu-id="07e65-144">This field indicates whether hello device is registered with Azure AD as a personal device (marked as *Workplace Joined*).</span></span> <span data-ttu-id="07e65-145">Esse valor deve ser **NO** para um computador ingressado no domínio, que também é ingressado no Azure AD híbrido.</span><span class="sxs-lookup"><span data-stu-id="07e65-145">This value should be **NO** for a domain-joined computer that is also hybrid Azure AD joined.</span></span> <span data-ttu-id="07e65-146">Se o valor de saudação é **Sim**, uma conta corporativa ou escolar foi adicionada conclusão toohello anterior de junção do hello híbrido do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="07e65-146">If hello value is **YES**, a work or school account was added prior toohello completion of hello hybrid Azure AD join.</span></span> <span data-ttu-id="07e65-147">Nesse caso, a conta de Olá é ignorada ao usar a versão de atualização de aniversário de saudação do Windows 10 (1607).</span><span class="sxs-lookup"><span data-stu-id="07e65-147">In this case, hello account is ignored when using hello Anniversary Update version of Windows 10 (1607).</span></span>

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a><span data-ttu-id="07e65-148">WamDefaultSet : YES e AzureADPrt : YES</span><span class="sxs-lookup"><span data-stu-id="07e65-148">WamDefaultSet : YES and AzureADPrt : YES</span></span>
  
<span data-ttu-id="07e65-149">Esses campos indicam se o usuário Olá foi autenticado com êxito tooAzure AD ao entrarem no dispositivo toohello.</span><span class="sxs-lookup"><span data-stu-id="07e65-149">These fields indicate whether hello user has successfully authenticated tooAzure AD when signing in toohello device.</span></span> <span data-ttu-id="07e65-150">Se os valores hello são **não**, ele pode ter ocorrido:</span><span class="sxs-lookup"><span data-stu-id="07e65-150">If hello values are **NO**, it could be due:</span></span>

- <span data-ttu-id="07e65-151">Chave de armazenamento incorreta (STK) no TPM associado Olá dispositivo após o registro (seleção Olá KeySignTest durante a execução com privilégios elevados).</span><span class="sxs-lookup"><span data-stu-id="07e65-151">Bad storage key (STK) in TPM associated with hello device upon registration (check hello KeySignTest while running elevated).</span></span>

- <span data-ttu-id="07e65-152">ID de logon alternativo</span><span class="sxs-lookup"><span data-stu-id="07e65-152">Alternate Login ID</span></span>

- <span data-ttu-id="07e65-153">Proxy HTTP não encontrado</span><span class="sxs-lookup"><span data-stu-id="07e65-153">HTTP Proxy not found</span></span>

## <a name="next-steps"></a><span data-ttu-id="07e65-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="07e65-154">Next steps</span></span>

<span data-ttu-id="07e65-155">Para perguntas, consulte Olá [perguntas frequentes sobre o gerenciamento de dispositivos](device-management-faq.md)</span><span class="sxs-lookup"><span data-stu-id="07e65-155">For questions, see hello [device management FAQ](device-management-faq.md)</span></span> 
