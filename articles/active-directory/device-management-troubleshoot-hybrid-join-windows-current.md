---
title: "Solução de problemas do Azure Active Directory híbrido ingressado em dispositivos do Windows 10 e do Windows Server 2016 | Microsoft Docs"
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
ms.openlocfilehash: 51962c14a3c32bbfa9a613fa203cc48cfea50c0b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-windows-10-and-windows-server-2016-devices"></a><span data-ttu-id="d6596-103">Solução de problemas do Azure Active Directory híbrido ingressado em dispositivos do Windows 10 e do Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="d6596-103">Troubleshooting hybrid Azure Active Directory joined Windows 10 and Windows Server 2016 devices</span></span> 

<span data-ttu-id="d6596-104">Este tópico é aplicável aos seguintes clientes:</span><span class="sxs-lookup"><span data-stu-id="d6596-104">This topic is applicable to the following clients:</span></span>

-   <span data-ttu-id="d6596-105">Windows 10</span><span class="sxs-lookup"><span data-stu-id="d6596-105">Windows 10</span></span>
-   <span data-ttu-id="d6596-106">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="d6596-106">Windows Server 2016</span></span>

<span data-ttu-id="d6596-107">Para outros clientes do Windows, consulte [Solução de problemas do Azure Active Directory híbrido ingressado em dispositivos de nível inferior](device-management-troubleshoot-hybrid-join-windows-legacy.md).</span><span class="sxs-lookup"><span data-stu-id="d6596-107">For other Windows clients, see [Troubleshooting hybrid Azure Active Directory joined down-level devices](device-management-troubleshoot-hybrid-join-windows-legacy.md).</span></span>

<span data-ttu-id="d6596-108">Este tópico pressupõe que você tenha [dispositivos configurados e ingressados no Azure Active Directory híbrido](device-management-hybrid-azuread-joined-devices-setup.md) para dar suporte aos seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="d6596-108">This topic assumes that you have [configured hybrid Azure Active Directory joined devices](device-management-hybrid-azuread-joined-devices-setup.md) to support the following scenarios:</span></span>

- <span data-ttu-id="d6596-109">Acesso condicional com base em dispositivo</span><span class="sxs-lookup"><span data-stu-id="d6596-109">Device-based conditional access</span></span>

- [<span data-ttu-id="d6596-110">Roaming corporativo de configurações</span><span class="sxs-lookup"><span data-stu-id="d6596-110">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="d6596-111">Configurar o Hello for Business</span><span class="sxs-lookup"><span data-stu-id="d6596-111">Windows Hello for Business</span></span>](active-directory-azureadjoin-passport-deployment.md)


<span data-ttu-id="d6596-112">Este documento fornece diretrizes de solução de problemas sobre como resolver os problemas potenciais.</span><span class="sxs-lookup"><span data-stu-id="d6596-112">This document provides troubleshooting guidance on how to resolve potential issues.</span></span> 


<span data-ttu-id="d6596-113">Para Windows 10 e Windows Server 2016, o ingresso do Azure Active Directory híbrido oferece suporte à atualização de 10 de novembro de 2015 e superior do Windows 10.</span><span class="sxs-lookup"><span data-stu-id="d6596-113">For Windows 10 and Windows Server 2016, hybrid Azure Active Directory join supports the Windows 10 November 2015 Update and above.</span></span> <span data-ttu-id="d6596-114">Recomendamos usar a atualização de Aniversário.</span><span class="sxs-lookup"><span data-stu-id="d6596-114">We recommend using the Anniversary update.</span></span>

## <a name="step-1-retrieve-the-join-status"></a><span data-ttu-id="d6596-115">Etapa 1: Recuperar o status do ingresso</span><span class="sxs-lookup"><span data-stu-id="d6596-115">Step 1: Retrieve the join status</span></span> 

<span data-ttu-id="d6596-116">**Para recuperar o status do ingresso:**</span><span class="sxs-lookup"><span data-stu-id="d6596-116">**To retrieve the join status:**</span></span>

1. <span data-ttu-id="d6596-117">Abra o prompt de comando como administrador</span><span class="sxs-lookup"><span data-stu-id="d6596-117">Open the command prompt as an administrator</span></span>

2. <span data-ttu-id="d6596-118">Digite **dsregcmd /status**</span><span class="sxs-lookup"><span data-stu-id="d6596-118">Type **dsregcmd /status**</span></span>



    <span data-ttu-id="d6596-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="d6596-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span></span>
    
        AzureAdJoined: YES
     <span data-ttu-id="d6596-120">EnterpriseJoined: NO DeviceId: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: Microsoft Platform Crypto Provider TpmProtected: YES KeySignTest: : MUST Run elevated to test.</span><span class="sxs-lookup"><span data-stu-id="d6596-120">EnterpriseJoined: NO DeviceId: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: Microsoft Platform Crypto Provider TpmProtected: YES KeySignTest: : MUST Run elevated to test.</span></span>
                  <span data-ttu-id="d6596-121">Idp: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn:ms-drs:enterpriseregistration.windows.net DomainJoined: YES DomainName: CONTOSO</span><span class="sxs-lookup"><span data-stu-id="d6596-121">Idp: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn:ms-drs:enterpriseregistration.windows.net DomainJoined: YES DomainName: CONTOSO</span></span>
    
    <span data-ttu-id="d6596-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="d6596-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span></span>
    
                 NgcSet: YES
               NgcKeyId: {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined: NO
          WamDefaultSet: YES
    <span data-ttu-id="d6596-123">WamDefaultAuthority: organizations         WamDefaultId: https://login.microsoft.com       WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt: YES</span><span class="sxs-lookup"><span data-stu-id="d6596-123">WamDefaultAuthority: organizations         WamDefaultId: https://login.microsoft.com       WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt: YES</span></span>



## <a name="step-2-evaluate-the-join-status"></a><span data-ttu-id="d6596-124">Etapa 2: Avaliar o status do ingresso</span><span class="sxs-lookup"><span data-stu-id="d6596-124">Step 2: Evaluate the join status</span></span> 

<span data-ttu-id="d6596-125">Examine os seguintes campos e garanta que eles tenham os valores esperados:</span><span class="sxs-lookup"><span data-stu-id="d6596-125">Review the following fields and make sure that they have the expected values:</span></span>

### <a name="azureadjoined--yes"></a><span data-ttu-id="d6596-126">AzureAdJoined : YES</span><span class="sxs-lookup"><span data-stu-id="d6596-126">AzureAdJoined : YES</span></span>  

<span data-ttu-id="d6596-127">Esse campo indica se o dispositivo ingressou no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d6596-127">This field indicates whether the device is joined with Azure AD.</span></span> <span data-ttu-id="d6596-128">Se o valor for **NO**, a associação ao Azure AD ainda não terá sido concluída.</span><span class="sxs-lookup"><span data-stu-id="d6596-128">If the value is **NO**, the join to Azure AD has not completed yet.</span></span> 

<span data-ttu-id="d6596-129">**Possíveis causas:**</span><span class="sxs-lookup"><span data-stu-id="d6596-129">**Possible causes:**</span></span>

- <span data-ttu-id="d6596-130">Falha na autenticação do computador para um ingresso.</span><span class="sxs-lookup"><span data-stu-id="d6596-130">Authentication of the computer for a join failed.</span></span>

- <span data-ttu-id="d6596-131">Há um proxy HTTP na organização que não pode ser descoberto pelo computador</span><span class="sxs-lookup"><span data-stu-id="d6596-131">There is an HTTP proxy in the organization that cannot be discovered by the computer</span></span>

- <span data-ttu-id="d6596-132">O computador não pode alcançar o Azure AD para autenticação, ou o Azure DRS para registro</span><span class="sxs-lookup"><span data-stu-id="d6596-132">The computer cannot reach Azure AD to authenticate or Azure DRS for registration</span></span>

- <span data-ttu-id="d6596-133">O computador pode não estar na rede interna da organização ou em VPN com a linha de visão direta para um controlador de domínio do AD local.</span><span class="sxs-lookup"><span data-stu-id="d6596-133">The computer may not be on the organization’s internal network or on VPN with direct line of sight to an on-premises AD domain controller.</span></span>

- <span data-ttu-id="d6596-134">Se o computador tiver um TPM, poderá estar em um estado inválido.</span><span class="sxs-lookup"><span data-stu-id="d6596-134">If the computer has a TPM, it can be in a bad state.</span></span>

- <span data-ttu-id="d6596-135">Pode haver um erro de configuração nos serviços, observado anteriormente no documento, que você precisará verificar novamente.</span><span class="sxs-lookup"><span data-stu-id="d6596-135">There might be a misconfiguration in the services noted in the document earlier that you will need to verify again.</span></span> <span data-ttu-id="d6596-136">Alguns exemplos comuns são:</span><span class="sxs-lookup"><span data-stu-id="d6596-136">Common examples are:</span></span>

    - <span data-ttu-id="d6596-137">O servidor de Federação não tem pontos de extremidade WS-Trust habilitados</span><span class="sxs-lookup"><span data-stu-id="d6596-137">Your federation server does not have WS-Trust endpoints enabled</span></span>

    - <span data-ttu-id="d6596-138">O servidor de federação não permite a autenticação de entrada de computadores em sua rede usando a Autenticação Integrada do Windows.</span><span class="sxs-lookup"><span data-stu-id="d6596-138">Your federation server does not allow inbound authentication from computers in your network using Integrated Windows Authentication.</span></span>

    - <span data-ttu-id="d6596-139">Não há nenhum objeto de Ponto de Conexão de Serviço que aponta para o seu nome de domínio verificado no Azure AD na floresta do AD à qual o computador pertence</span><span class="sxs-lookup"><span data-stu-id="d6596-139">There is no Service Connection Point object that points to your verified domain name in Azure AD in the AD forest where the computer belongs to</span></span>

---

### <a name="domainjoined--yes"></a><span data-ttu-id="d6596-140">DomainJoined : YES</span><span class="sxs-lookup"><span data-stu-id="d6596-140">DomainJoined : YES</span></span>  

<span data-ttu-id="d6596-141">Esse campo indica se o dispositivo ingressou em um Active Directory local ou não.</span><span class="sxs-lookup"><span data-stu-id="d6596-141">This field indicates whether the device is joined to an on-premises Active Directory or not.</span></span> <span data-ttu-id="d6596-142">Se o valor for **NO**, o dispositivo não poderá executar um ingresso do Azure AD híbrido.</span><span class="sxs-lookup"><span data-stu-id="d6596-142">If the value is **NO**, the device cannot perform a hybrid Azure AD join.</span></span>  

---

### <a name="workplacejoined--no"></a><span data-ttu-id="d6596-143">WorkplaceJoined : NO</span><span class="sxs-lookup"><span data-stu-id="d6596-143">WorkplaceJoined : NO</span></span>  

<span data-ttu-id="d6596-144">Esse campo indica se o dispositivo está registrado no Azure AD como um dispositivo pessoal (marcado como *Ingressado no Espaço de Trabalho*).</span><span class="sxs-lookup"><span data-stu-id="d6596-144">This field indicates whether the device is registered with Azure AD as a personal device (marked as *Workplace Joined*).</span></span> <span data-ttu-id="d6596-145">Esse valor deve ser **NO** para um computador ingressado no domínio, que também é ingressado no Azure AD híbrido.</span><span class="sxs-lookup"><span data-stu-id="d6596-145">This value should be **NO** for a domain-joined computer that is also hybrid Azure AD joined.</span></span> <span data-ttu-id="d6596-146">Se o valor for **YES**, uma conta corporativa ou de estudante terá sido adicionada antes da conclusão do ingresso do Azure AD híbrido.</span><span class="sxs-lookup"><span data-stu-id="d6596-146">If the value is **YES**, a work or school account was added prior to the completion of the hybrid Azure AD join.</span></span> <span data-ttu-id="d6596-147">Nesse caso, a conta é ignorada ao usar a versão de Atualização de Aniversário do Windows 10 (1607).</span><span class="sxs-lookup"><span data-stu-id="d6596-147">In this case, the account is ignored when using the Anniversary Update version of Windows 10 (1607).</span></span>

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a><span data-ttu-id="d6596-148">WamDefaultSet : YES e AzureADPrt : YES</span><span class="sxs-lookup"><span data-stu-id="d6596-148">WamDefaultSet : YES and AzureADPrt : YES</span></span>
  
<span data-ttu-id="d6596-149">Esses campos indicam se o usuário foi autenticado com êxito no Azure AD ao se conectar ao dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d6596-149">These fields indicate whether the user has successfully authenticated to Azure AD when signing in to the device.</span></span> <span data-ttu-id="d6596-150">Se os valores forem **NO**, talvez o motivo seja:</span><span class="sxs-lookup"><span data-stu-id="d6596-150">If the values are **NO**, it could be due:</span></span>

- <span data-ttu-id="d6596-151">STK (chave de armazenamento) inválida no TPM associada ao dispositivo no registro (verifique o KeySignTest durante a execução com privilégios elevados).</span><span class="sxs-lookup"><span data-stu-id="d6596-151">Bad storage key (STK) in TPM associated with the device upon registration (check the KeySignTest while running elevated).</span></span>

- <span data-ttu-id="d6596-152">ID de logon alternativo</span><span class="sxs-lookup"><span data-stu-id="d6596-152">Alternate Login ID</span></span>

- <span data-ttu-id="d6596-153">Proxy HTTP não encontrado</span><span class="sxs-lookup"><span data-stu-id="d6596-153">HTTP Proxy not found</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6596-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d6596-154">Next steps</span></span>

<span data-ttu-id="d6596-155">Para perguntas, consulte as [Perguntas frequentes sobre o gerenciamento de dispositivos](device-management-faq.md)</span><span class="sxs-lookup"><span data-stu-id="d6596-155">For questions, see the [device management FAQ](device-management-faq.md)</span></span> 