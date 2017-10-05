---
title: "Solucionando problemas do registro automático de computadores ingressados no domínio do Azure AD para Windows 10 e Windows Server 2016 | Microsoft Docs"
description: "Solucionando problemas do registro automático de computadores ingressados no domínio do Azure AD para Windows 10 e Windows Server 2016."
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
ms.openlocfilehash: 5b7f95f302f716d9221b5fae59aa2df5c956a524
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-to-azure-ad--windows-10-and-windows-server-2016"></a><span data-ttu-id="534f8-103">Solução de problemas de registro automático de computadores ingressados no domínio do Azure AD – Windows 10 e Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="534f8-103">Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016</span></span>

<span data-ttu-id="534f8-104">Este tópico é aplicável aos seguintes clientes:</span><span class="sxs-lookup"><span data-stu-id="534f8-104">This topic is applicable to the following clients:</span></span>

-   <span data-ttu-id="534f8-105">Windows 10</span><span class="sxs-lookup"><span data-stu-id="534f8-105">Windows 10</span></span>
-   <span data-ttu-id="534f8-106">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="534f8-106">Windows Server 2016</span></span>

<span data-ttu-id="534f8-107">Para outros clientes Windows, confira [Solução de problemas de registro automático de computadores ingressados no domínio do Azure AD para clientes de nível inferior do Windows](active-directory-device-registration-troubleshoot-windows-legacy.md).</span><span class="sxs-lookup"><span data-stu-id="534f8-107">For other Windows clients, see [Troubleshooting auto-registration of domain joined computers to Azure AD for Windows down-level clients](active-directory-device-registration-troubleshoot-windows-legacy.md).</span></span>

<span data-ttu-id="534f8-108">Este tópico pressupõe que você tenha configurado o registro automático de dispositivos ingressados no domínio conforme descrito em [Como configurar o registro automático de dispositivos ingressados no domínio do Windows com o Azure Active Directory](active-directory-device-registration-get-started.md) para dar suporte aos seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="534f8-108">This topic assumes that you have configured auto-registration of domain-joined devices as outlined in described in [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-device-registration-get-started.md) to support the following scenarios:</span></span>

- [<span data-ttu-id="534f8-109">Acesso condicional com base em dispositivo</span><span class="sxs-lookup"><span data-stu-id="534f8-109">Device-based conditional access</span></span>](active-directory-conditional-access-automatic-device-registration-setup.md)

- [<span data-ttu-id="534f8-110">Roaming corporativo de configurações</span><span class="sxs-lookup"><span data-stu-id="534f8-110">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="534f8-111">Configurar o Hello for Business</span><span class="sxs-lookup"><span data-stu-id="534f8-111">Windows Hello for Business</span></span>](active-directory-azureadjoin-passport-deployment.md)


<span data-ttu-id="534f8-112">Este documento fornece diretrizes de solução de problemas sobre como resolver os problemas potenciais.</span><span class="sxs-lookup"><span data-stu-id="534f8-112">This document provides troubleshooting guidance on how to resolve potential issues.</span></span> 

<span data-ttu-id="534f8-113">O registro tem suporte na Atualização do Windows de 10 de novembro de 2015 e superior.</span><span class="sxs-lookup"><span data-stu-id="534f8-113">The registration is supported in the Windows 10 November 2015 Update and above.</span></span>  
<span data-ttu-id="534f8-114">É recomendável usar a Atualização de Aniversário para habilitar os cenários acima.</span><span class="sxs-lookup"><span data-stu-id="534f8-114">We recommend using the Anniversary Update for enabling the scenarios above.</span></span>

## <a name="step-1-retrieve-the-registration-status"></a><span data-ttu-id="534f8-115">Etapa 1: Recuperar o status do registro</span><span class="sxs-lookup"><span data-stu-id="534f8-115">Step 1: Retrieve the registration status</span></span> 

<span data-ttu-id="534f8-116">**Para recuperar o status do registro:**</span><span class="sxs-lookup"><span data-stu-id="534f8-116">**To retrieve the registration status:**</span></span>

1. <span data-ttu-id="534f8-117">Abra o prompt de comando como administrador.</span><span class="sxs-lookup"><span data-stu-id="534f8-117">Open the command prompt as an administrator.</span></span>

2. <span data-ttu-id="534f8-118">Digite **dsregcmd /status**</span><span class="sxs-lookup"><span data-stu-id="534f8-118">Type **dsregcmd /status**</span></span>



    <span data-ttu-id="534f8-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="534f8-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span></span>
    
        AzureAdJoined : YES
     <span data-ttu-id="534f8-120">EnterpriseJoined : NO DeviceId : 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint : B753A6679CE720451921302CA873794D94C6204A KeyContainerId : bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider : Microsoft Platform Crypto Provider TpmProtected : YES KeySignTest: : MUST Run elevated to test.</span><span class="sxs-lookup"><span data-stu-id="534f8-120">EnterpriseJoined : NO DeviceId : 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint : B753A6679CE720451921302CA873794D94C6204A KeyContainerId : bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider : Microsoft Platform Crypto Provider TpmProtected : YES KeySignTest: : MUST Run elevated to test.</span></span>
                  <span data-ttu-id="534f8-121">Idp : login.windows.net TenantId : 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName : Contoso AuthCodeUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl : https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl : https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl : https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl : eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion : 1.0 JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion : 1.0 KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId : urn:ms-drs:enterpriseregistration.windows.net DomainJoined : YES DomainName : CONTOSO</span><span class="sxs-lookup"><span data-stu-id="534f8-121">Idp : login.windows.net TenantId : 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName : Contoso AuthCodeUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl : https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl : https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl : https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl : eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion : 1.0 JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion : 1.0 KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId : urn:ms-drs:enterpriseregistration.windows.net DomainJoined : YES DomainName : CONTOSO</span></span>
    
    <span data-ttu-id="534f8-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="534f8-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span></span>
    
                 NgcSet : YES
               NgcKeyId : {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined : NO
          WamDefaultSet : YES
    <span data-ttu-id="534f8-123">WamDefaultAuthority : organizations         WamDefaultId : https://login.microsoft.com       WamDefaultGUID : {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt : YES</span><span class="sxs-lookup"><span data-stu-id="534f8-123">WamDefaultAuthority : organizations         WamDefaultId : https://login.microsoft.com       WamDefaultGUID : {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt : YES</span></span>



## <a name="step-2-evaluate-the-registration-status"></a><span data-ttu-id="534f8-124">Etapa 2: Avaliar o status do registro</span><span class="sxs-lookup"><span data-stu-id="534f8-124">Step 2: Evaluate the registration status</span></span> 

<span data-ttu-id="534f8-125">Examine os seguintes campos e garanta que eles tenham os valores esperados:</span><span class="sxs-lookup"><span data-stu-id="534f8-125">Review the following fields and make sure that they have the expected values:</span></span>

### <a name="azureadjoined--yes"></a><span data-ttu-id="534f8-126">AzureAdJoined : YES</span><span class="sxs-lookup"><span data-stu-id="534f8-126">AzureAdJoined : YES</span></span>  

<span data-ttu-id="534f8-127">Esse campo mostra se o dispositivo está registrado no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="534f8-127">This field shows whether the device is registered with Azure AD.</span></span> <span data-ttu-id="534f8-128">Se o valor aparecer como ‘NO’, o registro não foi concluído.</span><span class="sxs-lookup"><span data-stu-id="534f8-128">If the value shows as ‘NO’, registration has not completed.</span></span> 

<span data-ttu-id="534f8-129">**Possíveis causas:**</span><span class="sxs-lookup"><span data-stu-id="534f8-129">**Possible causes:**</span></span>

- <span data-ttu-id="534f8-130">Falha na autenticação do computador para o registro.</span><span class="sxs-lookup"><span data-stu-id="534f8-130">Authentication of the computer for registration failed.</span></span>

- <span data-ttu-id="534f8-131">Há um proxy HTTP na organização que não pode ser descoberto pelo computador</span><span class="sxs-lookup"><span data-stu-id="534f8-131">There is an HTTP proxy in the organization that cannot be discovered by the computer</span></span>

- <span data-ttu-id="534f8-132">O computador não pode alcançar o Azure AD para autenticação ou o Azure DRS para registro</span><span class="sxs-lookup"><span data-stu-id="534f8-132">The computer cannot reach Azure AD for authentication or Azure DRS for registration</span></span>

- <span data-ttu-id="534f8-133">O computador pode não estar na rede interna da organização ou em VPN com a linha de visão direta para um controlador de domínio do AD local.</span><span class="sxs-lookup"><span data-stu-id="534f8-133">The computer may not be on the organization’s internal network or on VPN with direct line of sight to an on-premises AD domain controller.</span></span>

- <span data-ttu-id="534f8-134">Se o computador tiver um TPM, ele poderá estar em um estado inválido.</span><span class="sxs-lookup"><span data-stu-id="534f8-134">If the computer has a TPM, it may be in a bad state.</span></span>

- <span data-ttu-id="534f8-135">Pode haver um erro de configuração nos serviços observado anteriormente no documento que você precisará verificar novamente.</span><span class="sxs-lookup"><span data-stu-id="534f8-135">There may be a misconfiguration in services noted in the document earlier that you will need to verify again.</span></span> <span data-ttu-id="534f8-136">Alguns exemplos comuns são:</span><span class="sxs-lookup"><span data-stu-id="534f8-136">Common examples are:</span></span>

    - <span data-ttu-id="534f8-137">O servidor de Federação não tem pontos de extremidade WS-Trust habilitados</span><span class="sxs-lookup"><span data-stu-id="534f8-137">Your federation server does not have WS-Trust endpoints enabled</span></span>

    - <span data-ttu-id="534f8-138">O servidor de federação pode não permitir a autenticação de entrada de computadores na rede usando a Autenticação Integrada do Windows.</span><span class="sxs-lookup"><span data-stu-id="534f8-138">Your federation server may not allow inbound authentication from computers in your network using Integrated Windows Authentication.</span></span>

    - <span data-ttu-id="534f8-139">Não há nenhum objeto de Ponto de Conexão de Serviço que aponta para o seu nome de domínio verificado no Azure AD na floresta do AD à qual o computador pertence</span><span class="sxs-lookup"><span data-stu-id="534f8-139">There is no Service Connection Point object that points to your verified domain name in Azure AD in the AD forest where the computer belongs to</span></span>

---

### <a name="domainjoined--yes"></a><span data-ttu-id="534f8-140">DomainJoined : YES</span><span class="sxs-lookup"><span data-stu-id="534f8-140">DomainJoined : YES</span></span>  

<span data-ttu-id="534f8-141">Esse campo mostra se o dispositivo ingressou em um Active Directory local ou não.</span><span class="sxs-lookup"><span data-stu-id="534f8-141">This field shows whether the device is joined to an on-premises Active Directory or not.</span></span> <span data-ttu-id="534f8-142">Se o valor aparecer como **NO**, o dispositivo não poderá se registrar automaticamente no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="534f8-142">If the value shows as **NO**, the device cannot auto-register with Azure AD.</span></span> <span data-ttu-id="534f8-143">Certifique-se primeiro de que o dispositivo ingresse no Active Directory local para que ele possa se registrar no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="534f8-143">Check first that the device joins to the on-premises Active Directory before it can register with Azure AD.</span></span> <span data-ttu-id="534f8-144">Se você estiver buscando ingressar o computador no Azure AD diretamente, vá até Learn about capabilities of Azure Active Directory Join (Saiba mais sobre os recursos do Ingresso do Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="534f8-144">If you are looking for joining the computer to Azure AD directly, please go to Learn about capabilities of Azure Active Directory Join.</span></span>

---

### <a name="workplacejoined--no"></a><span data-ttu-id="534f8-145">WorkplaceJoined : NO</span><span class="sxs-lookup"><span data-stu-id="534f8-145">WorkplaceJoined : NO</span></span>  

<span data-ttu-id="534f8-146">Esse campo mostra se o dispositivo está registrado no Azure AD, mas como um dispositivo pessoal (marcado como “Ingressado no Espaço de Trabalho”).</span><span class="sxs-lookup"><span data-stu-id="534f8-146">This field shows whether the device is registered with Azure AD but as a personal device (marked as ‘Workplace Joined’).</span></span> <span data-ttu-id="534f8-147">Se esse valor deve aparecer como 'NO' para um computador ingressado no domínio registrado no Azure AD, mas aparecer como YES, isso significa que uma conta corporativa ou de estudante foi adicionada antes de o computador concluir o registro.</span><span class="sxs-lookup"><span data-stu-id="534f8-147">If this value should show as ‘NO’ for a domain joined computer registered with Azure AD, however if it shows as YES it means that a work or school account was added prior to the computer completing registration.</span></span> <span data-ttu-id="534f8-148">Nesse caso a conta será ignorada se a versão de Atualização de Aniversário do Windows 10 (1607 ao executar o comando WinVer na janela 'Executar' ou em uma janela de prompt de comando) estiver sendo usada.</span><span class="sxs-lookup"><span data-stu-id="534f8-148">In this case the account will be ignored if using the Anniversary Update version of Windows 10 (1607 when running the WinVer command in the ‘Run’ window or a command prompt window).</span></span>

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a><span data-ttu-id="534f8-149">WamDefaultSet : YES e AzureADPrt : YES</span><span class="sxs-lookup"><span data-stu-id="534f8-149">WamDefaultSet : YES and AzureADPrt : YES</span></span>
  
<span data-ttu-id="534f8-150">Esses campos mostram que o usuário foi autenticado com êxito no Azure AD ao se conectar ao dispositivo.</span><span class="sxs-lookup"><span data-stu-id="534f8-150">These fields show that the user has successfully authenticated to Azure AD upon signing in to the device.</span></span> <span data-ttu-id="534f8-151">Se eles mostrarem ‘NO’, os itens a seguir serão possíveis causas:</span><span class="sxs-lookup"><span data-stu-id="534f8-151">If they show ‘NO’ the following are possible causes:</span></span>

- <span data-ttu-id="534f8-152">STK (chave de armazenamento) inválida no TPM associada ao dispositivo no registro (verifique o KeySignTest durante a execução com privilégios elevados).</span><span class="sxs-lookup"><span data-stu-id="534f8-152">Bad storage key (STK) in TPM associated with the device upon registration (check the KeySignTest while running elevated).</span></span>

- <span data-ttu-id="534f8-153">ID de logon alternativo</span><span class="sxs-lookup"><span data-stu-id="534f8-153">Alternate Login ID</span></span>

- <span data-ttu-id="534f8-154">Proxy HTTP não encontrado</span><span class="sxs-lookup"><span data-stu-id="534f8-154">HTTP Proxy not found</span></span>

## <a name="next-steps"></a><span data-ttu-id="534f8-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="534f8-155">Next steps</span></span>

<span data-ttu-id="534f8-156">Para saber mais, veja [Perguntas frequentes sobre o registro de dispositivo automático](active-directory-device-registration-faq.md)</span><span class="sxs-lookup"><span data-stu-id="534f8-156">For more information, see the [Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span> 