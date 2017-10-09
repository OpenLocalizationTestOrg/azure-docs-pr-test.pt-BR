---
title: "aaaAzure autenticação baseada em certificado do Active Directory - Introdução | Microsoft Docs"
description: "Saiba como a autenticação baseada em certificado em seu ambiente tooconfigure"
author: MarkusVi
documentationcenter: na
manager: femila
ms.assetid: c6ad7640-8172-4541-9255-770f39ecce0e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 3c73bdf56018c0716085c923a61e9560dbe4004c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-certificate-based-authentication-in-azure-active-directory"></a><span data-ttu-id="917ca-103">Inicie com uma autenticação baseada em certificado do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="917ca-103">Get started with certificate-based authentication in Azure Active Directory</span></span>

<span data-ttu-id="917ca-104">Autenticação baseada em certificado permite que você toobe autenticado pelo Active Directory do Azure com um certificado de cliente em um dispositivo Windows, Android ou iOS ao conectar-se a sua conta do Exchange online para:</span><span class="sxs-lookup"><span data-stu-id="917ca-104">Certificate-based authentication enables you toobe authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span></span> 

- <span data-ttu-id="917ca-105">Aplicativos móveis do Office, como Microsoft Outlook e Microsoft Word</span><span class="sxs-lookup"><span data-stu-id="917ca-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span></span>   

- <span data-ttu-id="917ca-106">Clientes do EAS (Exchange ActiveSync)</span><span class="sxs-lookup"><span data-stu-id="917ca-106">Exchange ActiveSync (EAS) clients</span></span> 

<span data-ttu-id="917ca-107">Configurar esse recurso elimina a necessidade de saudação tooenter um nome de usuário e combinação de senha em determinados email e aplicativos do Microsoft Office em seu dispositivo móvel.</span><span class="sxs-lookup"><span data-stu-id="917ca-107">Configuring this feature eliminates hello need tooenter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span> 

<span data-ttu-id="917ca-108">Este tópico:</span><span class="sxs-lookup"><span data-stu-id="917ca-108">This topic:</span></span>

- <span data-ttu-id="917ca-109">Fornece Olá tooconfigure as etapas e usar a autenticação baseada em certificado para usuários de locatários no Office 365 Enterprise, Business, educação e governo dos Estados Unidos planos.</span><span class="sxs-lookup"><span data-stu-id="917ca-109">Provides you with hello steps tooconfigure and utilize certificate-based authentication for users of tenants in Office 365 Enterprise, Business, Education, and US Government plans.</span></span> <span data-ttu-id="917ca-110">Esse recurso está disponível na visualização em planos do Office 365 para China, defesa governamental e governo federal.</span><span class="sxs-lookup"><span data-stu-id="917ca-110">This feature is available in preview in Office 365 China, US Government Defense, and US Government Federal plans.</span></span> 

- <span data-ttu-id="917ca-111">Pressupõe que você já tem uma [infraestrutura de chave pública (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) e [do AD FS](connect/active-directory-aadconnectfed-whatis.md) configurada.</span><span class="sxs-lookup"><span data-stu-id="917ca-111">Assumes that you already have a [public key infrastructure (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) and [AD FS](connect/active-directory-aadconnectfed-whatis.md) configured.</span></span>    


## <a name="requirements"></a><span data-ttu-id="917ca-112">Requisitos</span><span class="sxs-lookup"><span data-stu-id="917ca-112">Requirements</span></span>

<span data-ttu-id="917ca-113">a autenticação baseada em certificado tooconfigure, Olá deverá ser a seguinte:</span><span class="sxs-lookup"><span data-stu-id="917ca-113">tooconfigure certificate-based authentication, hello following must be true:</span></span>  

- <span data-ttu-id="917ca-114">A CBA (Autenticação Baseada em Certificado) tem suporte apenas em ambientes Federados para aplicativos de navegador ou clientes nativos que usam autenticação moderna (ADAL).</span><span class="sxs-lookup"><span data-stu-id="917ca-114">Certificate-based authentication (CBA) is only supported for Federated environments for browser applications or native clients using modern authentication (ADAL).</span></span> <span data-ttu-id="917ca-115">Olá uma exceção é Exchange Active Sync (EAS) para EXO que pode ser usado para contas, federadas e gerenciadas.</span><span class="sxs-lookup"><span data-stu-id="917ca-115">hello one exception is Exchange Active Sync (EAS) for EXO which can be used for both, federated and managed accounts.</span></span> 

- <span data-ttu-id="917ca-116">autoridade de certificação raiz Hello e autoridades de certificação intermediários devem ser configuradas no Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="917ca-116">hello root certificate authority and any intermediate certificate authorities must be configured in Azure Active Directory.</span></span>  

- <span data-ttu-id="917ca-117">Cada autoridade de certificação deve ter uma CRL (Lista de Certificados Revogados) que pode ser referenciada por meio de uma URL para a Internet.</span><span class="sxs-lookup"><span data-stu-id="917ca-117">Each certificate authority must have a certificate revocation list (CRL) that can be referenced via an Internet facing URL.</span></span>  

- <span data-ttu-id="917ca-118">Você deve ter pelo menos uma autoridade de certificação configurada no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="917ca-118">You must have at least one certificate authority configured in Azure Active Directory.</span></span> <span data-ttu-id="917ca-119">Você pode encontrar etapas relacionadas no hello [Configurar autoridades de certificação Olá](#step-2-configure-the-certificate-authorities) seção.</span><span class="sxs-lookup"><span data-stu-id="917ca-119">You can find related steps in hello [Configure hello certificate authorities](#step-2-configure-the-certificate-authorities) section.</span></span>  

- <span data-ttu-id="917ca-120">Para clientes do Exchange ActiveSync, o certificado de cliente Olá deve ter Olá roteável email usuário endereço no Exchange online em qualquer nome de entidade hello ou Olá valor RFC822 nome do campo de nome alternativo da entidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="917ca-120">For Exchange ActiveSync clients, hello client certificate must have hello user’s routable email address in Exchange online in either hello Principal Name or hello RFC822 Name value of hello Subject Alternative Name field.</span></span> <span data-ttu-id="917ca-121">Active Directory do Azure mapeia o atributo de endereço Proxy Olá RFC822 valor toohello no diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="917ca-121">Azure Active Directory maps hello RFC822 value toohello Proxy Address attribute in hello directory.</span></span>  

- <span data-ttu-id="917ca-122">O dispositivo de cliente deve ter a autoridade de certificação tooat um mínimo de acesso que emite certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="917ca-122">Your client device must have access tooat least one certificate authority that issues client certificates.</span></span>  

- <span data-ttu-id="917ca-123">Um certificado de cliente para autenticação de cliente deve ter sido emitido tooyour cliente.</span><span class="sxs-lookup"><span data-stu-id="917ca-123">A client certificate for client authentication must have been issued tooyour client.</span></span>  




## <a name="step-1-select-your-device-platform"></a><span data-ttu-id="917ca-124">Etapa 1: selecione a plataforma do dispositivo</span><span class="sxs-lookup"><span data-stu-id="917ca-124">Step 1: Select your device platform</span></span>

<span data-ttu-id="917ca-125">Como a primeira etapa para a plataforma de dispositivo Olá importantes para você, você precisa fazer tooreview Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="917ca-125">As a first step, for hello device platform you care about, you need tooreview hello following:</span></span>

- <span data-ttu-id="917ca-126">suporte de aplicativos móveis do Office Olá</span><span class="sxs-lookup"><span data-stu-id="917ca-126">hello Office mobile applications support</span></span> 
- <span data-ttu-id="917ca-127">requisitos de implementação de saudação</span><span class="sxs-lookup"><span data-stu-id="917ca-127">hello specific implementation requirements</span></span>  

<span data-ttu-id="917ca-128">Olá relacionados informações existem para Olá plataformas de dispositivo a seguir:</span><span class="sxs-lookup"><span data-stu-id="917ca-128">hello related information exists for hello following device platforms:</span></span>

- [<span data-ttu-id="917ca-129">Android</span><span class="sxs-lookup"><span data-stu-id="917ca-129">Android</span></span>](active-directory-certificate-based-authentication-android.md)
- [<span data-ttu-id="917ca-130">iOS</span><span class="sxs-lookup"><span data-stu-id="917ca-130">iOS</span></span>](active-directory-certificate-based-authentication-ios.md)


## <a name="step-2-configure-hello-certificate-authorities"></a><span data-ttu-id="917ca-131">Etapa 2: Configurar autoridades de certificação Olá</span><span class="sxs-lookup"><span data-stu-id="917ca-131">Step 2: Configure hello certificate authorities</span></span> 

<span data-ttu-id="917ca-132">tooconfigure as autoridades de certificado no Active Directory do Azure, para cada autoridade de certificação, carregar Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="917ca-132">tooconfigure your certificate authorities in Azure Active Directory, for each certificate authority, upload hello following:</span></span> 

* <span data-ttu-id="917ca-133">Olá parte pública do certificado de saudação em *. cer* formato</span><span class="sxs-lookup"><span data-stu-id="917ca-133">hello public portion of hello certificate, in *.cer* format</span></span> 
* <span data-ttu-id="917ca-134">Olá para URLs onde hello Internet listas de certificados revogados (CRLs) residem</span><span class="sxs-lookup"><span data-stu-id="917ca-134">hello Internet facing URLs where hello Certificate Revocation Lists (CRLs) reside</span></span>

<span data-ttu-id="917ca-135">esquema de saudação para uma autoridade de certificação será semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="917ca-135">hello schema for a certificate authority looks as follows:</span></span> 

    class TrustedCAsForPasswordlessAuth 
    { 
       CertificateAuthorityInformation[] certificateAuthorities;    
    } 

    class CertificateAuthorityInformation 

    { 
        CertAuthorityType authorityType; 
        X509Certificate trustedCertificate; 
        string crlDistributionPoint; 
        string deltaCrlDistributionPoint; 
        string trustedIssuer; 
        string trustedIssuerSKI; 
    }                

    enum CertAuthorityType 
    { 
        RootAuthority = 0, 
        IntermediateAuthority = 1 
    } 

<span data-ttu-id="917ca-136">Para configuração de saudação, você pode usar o hello [versão 2 do Azure Active Directory PowerShell](/powershell/azure/install-adv2?view=azureadps-2.0):</span><span class="sxs-lookup"><span data-stu-id="917ca-136">For hello configuration, you can use hello [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0):</span></span>  

1. <span data-ttu-id="917ca-137">Inicie o Windows PowerShell com os privilégios de administrador.</span><span class="sxs-lookup"><span data-stu-id="917ca-137">Start Windows PowerShell with administrator privileges.</span></span> 
2. <span data-ttu-id="917ca-138">Instale o módulo de saudação do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="917ca-138">Install hello Azure AD module.</span></span> <span data-ttu-id="917ca-139">Você precisa tooinstall versão [2.0.0.33 ](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) ou superior.</span><span class="sxs-lookup"><span data-stu-id="917ca-139">You need tooinstall Version [2.0.0.33 ](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) or higher.</span></span>  
   
        Install-Module -Name AzureAD –RequiredVersion 2.0.0.33 

<span data-ttu-id="917ca-140">Como uma primeira etapa de configuração, você precisa tooestablish uma conexão com seu locatário.</span><span class="sxs-lookup"><span data-stu-id="917ca-140">As a first configuration step, you need tooestablish a connection with your tenant.</span></span> <span data-ttu-id="917ca-141">Assim que um locatário de tooyour conexão existe, você pode revisar, adicionar, excluir e modificar as autoridades de certificação Olá confiável que são definidas em seu diretório.</span><span class="sxs-lookup"><span data-stu-id="917ca-141">As soon as a connection tooyour tenant exists, you can review, add, delete and modify hello trusted certificate authorities that are defined in your directory.</span></span> 

### <a name="connect"></a><span data-ttu-id="917ca-142">Connect</span><span class="sxs-lookup"><span data-stu-id="917ca-142">Connect</span></span>

<span data-ttu-id="917ca-143">tooestablish uma conexão com seu locatário, use Olá [AzureAD conectar](/powershell/module/azuread/connect-azuread?view=azureadps-2.0) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="917ca-143">tooestablish a connection with your tenant, use hello [Connect-AzureAD](/powershell/module/azuread/connect-azuread?view=azureadps-2.0) cmdlet:</span></span>

    Connect-AzureAD 


### <a name="retrieve"></a><span data-ttu-id="917ca-144">Recuperar</span><span class="sxs-lookup"><span data-stu-id="917ca-144">Retrieve</span></span> 

<span data-ttu-id="917ca-145">autoridades de certificação do tooretrieve Olá confiável que são definidas em seu diretório, use Olá [AzureADTrustedCertificateAuthority Get](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="917ca-145">tooretrieve hello trusted certificate authorities that are defined in your directory, use hello [Get-AzureADTrustedCertificateAuthority](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet.</span></span> 

    Get-AzureADTrustedCertificateAuthority 
 

### <a name="add"></a><span data-ttu-id="917ca-146">Adicionar</span><span class="sxs-lookup"><span data-stu-id="917ca-146">Add</span></span>

<span data-ttu-id="917ca-147">toocreate uma autoridade de certificação confiável, use Olá [New-AzureADTrustedCertificateAuthority](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet e conjunto hello **crlDistributionPoint** valor correto tooa do atributo:</span><span class="sxs-lookup"><span data-stu-id="917ca-147">toocreate a trusted certificate authority, use hello [New-AzureADTrustedCertificateAuthority](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet and set hello **crlDistributionPoint** attribute tooa correct value:</span></span> 
   
    $cert=Get-Content -Encoding byte "[LOCATION OF hello CER FILE]" 
    $new_ca=New-Object -TypeName Microsoft.Open.AzureAD.Model.CertificateAuthorityInformation 
    $new_ca.AuthorityType=0 
    $new_ca.TrustedCertificate=$cert 
    $new_ca.crlDistributionPoint=”<CRL Distribution URL>”
    New-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $new_ca 


### <a name="remove"></a><span data-ttu-id="917ca-148">Remover</span><span class="sxs-lookup"><span data-stu-id="917ca-148">Remove</span></span>

<span data-ttu-id="917ca-149">tooremove uma autoridade de certificação confiável, use Olá [AzureADTrustedCertificateAuthority remover](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="917ca-149">tooremove a trusted certificate authority, use hello [Remove-AzureADTrustedCertificateAuthority](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span></span>
   
    $c=Get-AzureADTrustedCertificateAuthority 
    Remove-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[2] 


### <a name="modfiy"></a><span data-ttu-id="917ca-150">Modificar</span><span class="sxs-lookup"><span data-stu-id="917ca-150">Modfiy</span></span>

<span data-ttu-id="917ca-151">toomodify uma autoridade de certificação confiável, use Olá [AzureADTrustedCertificateAuthority conjunto](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="917ca-151">toomodify a trusted certificate authority, use hello [Set-AzureADTrustedCertificateAuthority](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span></span>

    $c=Get-AzureADTrustedCertificateAuthority 
    $c[0].AuthorityType=1 
    Set-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[0] 


## <a name="step-3-configure-revocation"></a><span data-ttu-id="917ca-152">Etapa 3: configurar a revogação</span><span class="sxs-lookup"><span data-stu-id="917ca-152">Step 3: Configure revocation</span></span>

<span data-ttu-id="917ca-153">toorevoke um certificado de cliente do Active Directory do Azure busca certificado Olá a lista de revogação (CRL) de URLs Olá carregado como parte das informações de autoridade de certificado e armazena em cache.</span><span class="sxs-lookup"><span data-stu-id="917ca-153">toorevoke a client certificate, Azure Active Directory fetches hello certificate revocation list (CRL) from hello URLs uploaded as part of certificate authority information and caches it.</span></span> <span data-ttu-id="917ca-154">carimbo de hora da última publicação da saudação (**data de efetivação** propriedade) na Olá CRL é usada tooensure Olá CRL ainda é válido.</span><span class="sxs-lookup"><span data-stu-id="917ca-154">hello last publish timestamp (**Effective Date** property) in hello CRL is used tooensure hello CRL is still valid.</span></span> <span data-ttu-id="917ca-155">Olá CRL é referenciado periodicamente toorevoke acesso toocertificates que fazem parte da lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="917ca-155">hello CRL is periodically referenced toorevoke access toocertificates that are a part of hello list.</span></span>

<span data-ttu-id="917ca-156">Se um instantânea mais revogação for necessária (por exemplo, se um usuário perde um dispositivo), token de autorização de saudação do usuário Olá pode ser invalidado.</span><span class="sxs-lookup"><span data-stu-id="917ca-156">If a more instant revocation is required (for example, if a user loses a device), hello authorization token of hello user can be invalidated.</span></span> <span data-ttu-id="917ca-157">saudação de token, defina de autorização de saudação do tooinvalidate **StsRefreshTokenValidFrom** campo para esse usuário específico usando o Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="917ca-157">tooinvalidate hello authorization token, set hello **StsRefreshTokenValidFrom** field for this particular user using Windows PowerShell.</span></span> <span data-ttu-id="917ca-158">Você deve atualizar Olá **StsRefreshTokenValidFrom** campo para cada usuário que você deseja acesso toorevoke.</span><span class="sxs-lookup"><span data-stu-id="917ca-158">You must update hello **StsRefreshTokenValidFrom** field for each user you want toorevoke access for.</span></span>

<span data-ttu-id="917ca-159">tooensure revogação Olá persistente, você deve definir Olá **data de efetivação** da data de tooa CRL Olá após Olá valor definido por **StsRefreshTokenValidFrom** e certifique-se de saudação certificado em questão está no Olá CRL.</span><span class="sxs-lookup"><span data-stu-id="917ca-159">tooensure that hello revocation persists, you must set hello **Effective Date** of hello CRL tooa date after hello value set by **StsRefreshTokenValidFrom** and ensure hello certificate in question is in hello CRL.</span></span>

<span data-ttu-id="917ca-160">Olá seguindo as etapas da estrutura de tópicos Olá processo de atualização e invalidar o token de autorização Olá por configuração Olá **StsRefreshTokenValidFrom** campo.</span><span class="sxs-lookup"><span data-stu-id="917ca-160">hello following steps outline hello process for updating and invalidating hello authorization token by setting hello **StsRefreshTokenValidFrom** field.</span></span> 

<span data-ttu-id="917ca-161">**revogação de tooconfigure:**</span><span class="sxs-lookup"><span data-stu-id="917ca-161">**tooconfigure revocation:**</span></span> 

1. <span data-ttu-id="917ca-162">Conecte-se com o serviço de MSOL de toohello de credenciais de administrador:</span><span class="sxs-lookup"><span data-stu-id="917ca-162">Connect with admin credentials toohello MSOL service:</span></span> 
   
        $msolcred = get-credential 
        connect-msolservice -credential $msolcred 

2. <span data-ttu-id="917ca-163">Recupere o valor atual de StsRefreshTokensValidFrom Olá para um usuário:</span><span class="sxs-lookup"><span data-stu-id="917ca-163">Retrieve hello current StsRefreshTokensValidFrom value for a user:</span></span> 
   
        $user = Get-MsolUser -UserPrincipalName test@yourdomain.com` 
        $user.StsRefreshTokensValidFrom 

3. <span data-ttu-id="917ca-164">Configure um novo valor de StsRefreshTokensValidFrom para usuário de saudação toohello igual timestamp atual:</span><span class="sxs-lookup"><span data-stu-id="917ca-164">Configure a new StsRefreshTokensValidFrom value for hello user equal toohello current timestamp:</span></span> 
   
        Set-MsolUser -UserPrincipalName test@yourdomain.com -StsRefreshTokensValidFrom ("03/05/2016")

<span data-ttu-id="917ca-165">Data de saudação definir deve estar no hello futuras.</span><span class="sxs-lookup"><span data-stu-id="917ca-165">hello date you set must be in hello future.</span></span> <span data-ttu-id="917ca-166">Se Olá data não estiver no hello futuras, Olá **StsRefreshTokensValidFrom** propriedade não está definida.</span><span class="sxs-lookup"><span data-stu-id="917ca-166">If hello date is not in hello future, hello **StsRefreshTokensValidFrom** property is not set.</span></span> <span data-ttu-id="917ca-167">Se for date de hello em Olá futura, **StsRefreshTokensValidFrom** é definido toohello hora atual (não data Olá indicada pelo comando Set-MsolUser).</span><span class="sxs-lookup"><span data-stu-id="917ca-167">If hello date is in hello future, **StsRefreshTokensValidFrom** is set toohello current time (not hello date indicated by Set-MsolUser command).</span></span> 


## <a name="step-4-test-your-configuration"></a><span data-ttu-id="917ca-168">Etapa 4: testar a sua configuração</span><span class="sxs-lookup"><span data-stu-id="917ca-168">Step 4: Test your configuration</span></span>

### <a name="testing-your-certificate"></a><span data-ttu-id="917ca-169">Teste do seu certificado</span><span class="sxs-lookup"><span data-stu-id="917ca-169">Testing your certificate</span></span>

<span data-ttu-id="917ca-170">Como um primeiro teste de configuração, você deve tentar toosign em muito[Outlook Web Access](https://outlook.office365.com) ou [SharePoint Online](https://microsoft.sharepoint.com) usando seu **navegador no dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="917ca-170">As a first configuration test, you should try toosign in too[Outlook Web Access](https://outlook.office365.com) or [SharePoint Online](https://microsoft.sharepoint.com) using your **on-device browser**.</span></span>

<span data-ttu-id="917ca-171">Se a entrada for bem-sucedida, você saberá que:</span><span class="sxs-lookup"><span data-stu-id="917ca-171">If your sign-in is successful, then you know that:</span></span>

- <span data-ttu-id="917ca-172">certificado de usuário Olá foi provisionado tooyour dispositivo de teste</span><span class="sxs-lookup"><span data-stu-id="917ca-172">hello user certificate has been provisioned tooyour test device</span></span>
- <span data-ttu-id="917ca-173">O AD FS está configurado corretamente</span><span class="sxs-lookup"><span data-stu-id="917ca-173">AD FS is configured correctly</span></span>  


### <a name="testing-office-mobile-applications"></a><span data-ttu-id="917ca-174">Testando aplicativos móveis do Office</span><span class="sxs-lookup"><span data-stu-id="917ca-174">Testing Office mobile applications</span></span>

<span data-ttu-id="917ca-175">**tootest autenticação baseada em certificado em seu aplicativo móvel do Office:**</span><span class="sxs-lookup"><span data-stu-id="917ca-175">**tootest certificate-based authentication on your mobile Office application:**</span></span> 

1. <span data-ttu-id="917ca-176">No seu dispositivo de teste, instale um aplicativo móvel do Office (por exemplo, OneDrive).</span><span class="sxs-lookup"><span data-stu-id="917ca-176">On your test device, install an Office mobile application (e.g., OneDrive).</span></span>
3. <span data-ttu-id="917ca-177">Inicie o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="917ca-177">Launch hello application.</span></span> 
4. <span data-ttu-id="917ca-178">Insira seu nome de usuário e, em seguida, selecione o certificado de usuário de Olá que você deseja que o toouse.</span><span class="sxs-lookup"><span data-stu-id="917ca-178">Enter your user name, and then select hello user certificate you want toouse.</span></span> 

<span data-ttu-id="917ca-179">Você deve se conectar com êxito.</span><span class="sxs-lookup"><span data-stu-id="917ca-179">You should be successfully signed in.</span></span> 

### <a name="testing-exchange-activesync-client-applications"></a><span data-ttu-id="917ca-180">Testando aplicativos cliente do Exchange ActiveSync</span><span class="sxs-lookup"><span data-stu-id="917ca-180">Testing Exchange ActiveSync client applications</span></span>

<span data-ttu-id="917ca-181">tooaccess do Exchange ActiveSync (EAS) por meio da autenticação baseada em certificado, um perfil EAS que contém o certificado de cliente Olá deve ser aplicativo toohello disponíveis.</span><span class="sxs-lookup"><span data-stu-id="917ca-181">tooaccess Exchange ActiveSync (EAS) via certificate-based authentication, an EAS profile containing hello client certificate must be available toohello application.</span></span> 

<span data-ttu-id="917ca-182">Olá perfil de EAS deve conter Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="917ca-182">hello EAS profile must contain hello following information:</span></span>

- <span data-ttu-id="917ca-183">Olá toobe de certificado de usuário usado para autenticação</span><span class="sxs-lookup"><span data-stu-id="917ca-183">hello user certificate toobe used for authentication</span></span> 

- <span data-ttu-id="917ca-184">ponto de extremidade do Hello EAS (por exemplo, outlook.office365.com)</span><span class="sxs-lookup"><span data-stu-id="917ca-184">hello EAS endpoint (for example, outlook.office365.com)</span></span>

<span data-ttu-id="917ca-185">Um perfil de EAS pode ser configurado e colocado Olá dispositivo por meio da utilização de saudação do gerenciamento de dispositivo móvel (MDM) como o Intune ou colocando manualmente certificados Olá em Olá perfil de EAS em dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="917ca-185">An EAS profile can be configured and placed on hello device through hello utilization of Mobile device management (MDM) such as Intune or by manually placing hello certificate in hello EAS profile on hello device.</span></span>  

### <a name="testing-eas-client-applications-on-android"></a><span data-ttu-id="917ca-186">Testando os aplicativos cliente do EAS no Android</span><span class="sxs-lookup"><span data-stu-id="917ca-186">Testing EAS client applications on Android</span></span>

<span data-ttu-id="917ca-187">**autenticação de certificado tootest:**</span><span class="sxs-lookup"><span data-stu-id="917ca-187">**tootest certificate authentication:**</span></span>  

1. <span data-ttu-id="917ca-188">Configure um perfil EAS em aplicativo hello que satisfaz os requisitos de saudação acima.</span><span class="sxs-lookup"><span data-stu-id="917ca-188">Configure an EAS profile in hello application that satisfies hello requirements above.</span></span>  
2. <span data-ttu-id="917ca-189">Abra o aplicativo hello e verificar a sincronização de email.</span><span class="sxs-lookup"><span data-stu-id="917ca-189">Open hello application, and verify that mail is synchronizing.</span></span> 

