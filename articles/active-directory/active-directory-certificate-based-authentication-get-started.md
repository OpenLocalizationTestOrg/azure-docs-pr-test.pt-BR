---
title: "Autenticação baseada em certificado do Azure Active Directory - Introdução | Microsoft Docs"
description: "Aprenda a configurar a autenticação baseada em certificado no seu ambiente"
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
ms.openlocfilehash: 8ebc6f2dd7502fd75ffdd4d5d68338382cb1a46b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-certificate-based-authentication-in-azure-active-directory"></a><span data-ttu-id="0b394-103">Inicie com uma autenticação baseada em certificado do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0b394-103">Get started with certificate-based authentication in Azure Active Directory</span></span>

<span data-ttu-id="0b394-104">A autenticação baseada em certificado permite que você seja autenticado pelo Azure Active Directory com um certificado de cliente em um dispositivo Windows, Android ou iOS ao conectar sua conta do Exchange Online com:</span><span class="sxs-lookup"><span data-stu-id="0b394-104">Certificate-based authentication enables you to be authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span></span> 

- <span data-ttu-id="0b394-105">Aplicativos móveis do Office, como Microsoft Outlook e Microsoft Word</span><span class="sxs-lookup"><span data-stu-id="0b394-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span></span>   

- <span data-ttu-id="0b394-106">Clientes do EAS (Exchange ActiveSync)</span><span class="sxs-lookup"><span data-stu-id="0b394-106">Exchange ActiveSync (EAS) clients</span></span> 

<span data-ttu-id="0b394-107">Configurar esse recurso elimina a necessidade de digitar uma combinação de nome de usuário e senha em determinados emails e aplicativos do Microsoft Office no seu dispositivo móvel.</span><span class="sxs-lookup"><span data-stu-id="0b394-107">Configuring this feature eliminates the need to enter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span> 

<span data-ttu-id="0b394-108">Este tópico:</span><span class="sxs-lookup"><span data-stu-id="0b394-108">This topic:</span></span>

- <span data-ttu-id="0b394-109">Este tópico mostra como configurar e utilizar a autenticação baseada em certificado para usuários de locatários nos planos Office 365 corporativo, Business, educacional e governamental.</span><span class="sxs-lookup"><span data-stu-id="0b394-109">Provides you with the steps to configure and utilize certificate-based authentication for users of tenants in Office 365 Enterprise, Business, Education, and US Government plans.</span></span> <span data-ttu-id="0b394-110">Esse recurso está disponível na visualização em planos do Office 365 para China, defesa governamental e governo federal.</span><span class="sxs-lookup"><span data-stu-id="0b394-110">This feature is available in preview in Office 365 China, US Government Defense, and US Government Federal plans.</span></span> 

- <span data-ttu-id="0b394-111">Pressupõe que você já tem uma [infraestrutura de chave pública (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) e [do AD FS](connect/active-directory-aadconnectfed-whatis.md) configurada.</span><span class="sxs-lookup"><span data-stu-id="0b394-111">Assumes that you already have a [public key infrastructure (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) and [AD FS](connect/active-directory-aadconnectfed-whatis.md) configured.</span></span>    


## <a name="requirements"></a><span data-ttu-id="0b394-112">Requisitos</span><span class="sxs-lookup"><span data-stu-id="0b394-112">Requirements</span></span>

<span data-ttu-id="0b394-113">Para configurar a autenticação baseada em certificado, as seguintes afirmativas devem ser verdadeiras:</span><span class="sxs-lookup"><span data-stu-id="0b394-113">To configure certificate-based authentication, the following must be true:</span></span>  

- <span data-ttu-id="0b394-114">A CBA (Autenticação Baseada em Certificado) tem suporte apenas em ambientes Federados para aplicativos de navegador ou clientes nativos que usam autenticação moderna (ADAL).</span><span class="sxs-lookup"><span data-stu-id="0b394-114">Certificate-based authentication (CBA) is only supported for Federated environments for browser applications or native clients using modern authentication (ADAL).</span></span> <span data-ttu-id="0b394-115">A única exceção é o EAS (Exchange Active Sync) para EXO, que pode ser usado para contas federadas e gerenciadas.</span><span class="sxs-lookup"><span data-stu-id="0b394-115">The one exception is Exchange Active Sync (EAS) for EXO which can be used for both, federated and managed accounts.</span></span> 

- <span data-ttu-id="0b394-116">A autoridade de certificação raiz e qualquer autoridade de certificação intermediária devem ser configuradas no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0b394-116">The root certificate authority and any intermediate certificate authorities must be configured in Azure Active Directory.</span></span>  

- <span data-ttu-id="0b394-117">Cada autoridade de certificação deve ter uma CRL (Lista de Certificados Revogados) que pode ser referenciada por meio de uma URL para a Internet.</span><span class="sxs-lookup"><span data-stu-id="0b394-117">Each certificate authority must have a certificate revocation list (CRL) that can be referenced via an Internet facing URL.</span></span>  

- <span data-ttu-id="0b394-118">Você deve ter pelo menos uma autoridade de certificação configurada no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0b394-118">You must have at least one certificate authority configured in Azure Active Directory.</span></span> <span data-ttu-id="0b394-119">Você pode encontrar etapas relacionadas na seção [Configuração de autoridades de certificação](#step-2-configure-the-certificate-authorities).</span><span class="sxs-lookup"><span data-stu-id="0b394-119">You can find related steps in the [Configure the certificate authorities](#step-2-configure-the-certificate-authorities) section.</span></span>  

- <span data-ttu-id="0b394-120">Para clientes do Exchange ActiveSync, o certificado de cliente deve ter o email roteável do usuário no Exchange Online, seja no valor Nome principal ou Nome RFC822 do campo Nome Alternativo da Entidade.</span><span class="sxs-lookup"><span data-stu-id="0b394-120">For Exchange ActiveSync clients, the client certificate must have the user’s routable email address in Exchange online in either the Principal Name or the RFC822 Name value of the Subject Alternative Name field.</span></span> <span data-ttu-id="0b394-121">O Azure Active Directory mapeia o valor de RFC822 para o atributo Endereço de Proxy no diretório.</span><span class="sxs-lookup"><span data-stu-id="0b394-121">Azure Active Directory maps the RFC822 value to the Proxy Address attribute in the directory.</span></span>  

- <span data-ttu-id="0b394-122">O dispositivo do cliente deve ter acesso a pelo menos uma autoridade de certificação que emite certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="0b394-122">Your client device must have access to at least one certificate authority that issues client certificates.</span></span>  

- <span data-ttu-id="0b394-123">Um certificado de cliente para autenticação de cliente deve ter sido emitido para seu cliente.</span><span class="sxs-lookup"><span data-stu-id="0b394-123">A client certificate for client authentication must have been issued to your client.</span></span>  




## <a name="step-1-select-your-device-platform"></a><span data-ttu-id="0b394-124">Etapa 1: selecione a plataforma do dispositivo</span><span class="sxs-lookup"><span data-stu-id="0b394-124">Step 1: Select your device platform</span></span>

<span data-ttu-id="0b394-125">Para a plataforma do dispositivo sob sua responsabilidade, a primeira etapa é examinar o seguinte:</span><span class="sxs-lookup"><span data-stu-id="0b394-125">As a first step, for the device platform you care about, you need to review the following:</span></span>

- <span data-ttu-id="0b394-126">O suporte a aplicativos móveis do Office</span><span class="sxs-lookup"><span data-stu-id="0b394-126">The Office mobile applications support</span></span> 
- <span data-ttu-id="0b394-127">Os requisitos específicos de implementação</span><span class="sxs-lookup"><span data-stu-id="0b394-127">The specific implementation requirements</span></span>  

<span data-ttu-id="0b394-128">As informações relacionadas existentes para as seguintes plataformas de dispositivos:</span><span class="sxs-lookup"><span data-stu-id="0b394-128">The related information exists for the following device platforms:</span></span>

- [<span data-ttu-id="0b394-129">Android</span><span class="sxs-lookup"><span data-stu-id="0b394-129">Android</span></span>](active-directory-certificate-based-authentication-android.md)
- [<span data-ttu-id="0b394-130">iOS</span><span class="sxs-lookup"><span data-stu-id="0b394-130">iOS</span></span>](active-directory-certificate-based-authentication-ios.md)


## <a name="step-2-configure-the-certificate-authorities"></a><span data-ttu-id="0b394-131">Etapa 2: Configuração de autoridades de certificação</span><span class="sxs-lookup"><span data-stu-id="0b394-131">Step 2: Configure the certificate authorities</span></span> 

<span data-ttu-id="0b394-132">Para configurar as autoridades de certificação no Azure Active Directory, carregue o seguinte para cada autoridade de certificação:</span><span class="sxs-lookup"><span data-stu-id="0b394-132">To configure your certificate authorities in Azure Active Directory, for each certificate authority, upload the following:</span></span> 

* <span data-ttu-id="0b394-133">A parte pública do certificado, no formato *.cer*</span><span class="sxs-lookup"><span data-stu-id="0b394-133">The public portion of the certificate, in *.cer* format</span></span> 
* <span data-ttu-id="0b394-134">As URLs para a Internet, em que as CRLs (Listas de Certificados Revogados) residem</span><span class="sxs-lookup"><span data-stu-id="0b394-134">The Internet facing URLs where the Certificate Revocation Lists (CRLs) reside</span></span>

<span data-ttu-id="0b394-135">Veja abaixo o esquema de uma autoridade de certificação:</span><span class="sxs-lookup"><span data-stu-id="0b394-135">The schema for a certificate authority looks as follows:</span></span> 

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

<span data-ttu-id="0b394-136">Para a configuração, você pode usar o [Azure Active Directory PowerShell versão 2](/powershell/azure/install-adv2?view=azureadps-2.0):</span><span class="sxs-lookup"><span data-stu-id="0b394-136">For the configuration, you can use the [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0):</span></span>  

1. <span data-ttu-id="0b394-137">Inicie o Windows PowerShell com os privilégios de administrador.</span><span class="sxs-lookup"><span data-stu-id="0b394-137">Start Windows PowerShell with administrator privileges.</span></span> 
2. <span data-ttu-id="0b394-138">Instale o módulo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0b394-138">Install the Azure AD module.</span></span> <span data-ttu-id="0b394-139">Você precisa instalar a versão [2.0.0.33](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) ou superior.</span><span class="sxs-lookup"><span data-stu-id="0b394-139">You need to install Version [2.0.0.33 ](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) or higher.</span></span>  
   
        Install-Module -Name AzureAD –RequiredVersion 2.0.0.33 

<span data-ttu-id="0b394-140">Como essa é a primeira etapa de configuração, você precisa estabelecer uma conexão com seu locatário.</span><span class="sxs-lookup"><span data-stu-id="0b394-140">As a first configuration step, you need to establish a connection with your tenant.</span></span> <span data-ttu-id="0b394-141">Como existe uma conexão com o seu locatário, você pode revisar, adicionar, excluir e modificar autoridades de certificação confiáveis que são definidas em seu diretório.</span><span class="sxs-lookup"><span data-stu-id="0b394-141">As soon as a connection to your tenant exists, you can review, add, delete and modify the trusted certificate authorities that are defined in your directory.</span></span> 

### <a name="connect"></a><span data-ttu-id="0b394-142">Connect</span><span class="sxs-lookup"><span data-stu-id="0b394-142">Connect</span></span>

<span data-ttu-id="0b394-143">Para estabelecer uma conexão com seu locatário, use o cmdlet [Connect-AzureAD](/powershell/module/azuread/connect-azuread?view=azureadps-2.0):</span><span class="sxs-lookup"><span data-stu-id="0b394-143">To establish a connection with your tenant, use the [Connect-AzureAD](/powershell/module/azuread/connect-azuread?view=azureadps-2.0) cmdlet:</span></span>

    Connect-AzureAD 


### <a name="retrieve"></a><span data-ttu-id="0b394-144">Recuperar</span><span class="sxs-lookup"><span data-stu-id="0b394-144">Retrieve</span></span> 

<span data-ttu-id="0b394-145">Para recuperar as autoridades de certificação confiáveis que são definidas em seu diretório, use o cmdlet [Get-AzureADTrustedCertificateAuthority](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="0b394-145">To retrieve the trusted certificate authorities that are defined in your directory, use the [Get-AzureADTrustedCertificateAuthority](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet.</span></span> 

    Get-AzureADTrustedCertificateAuthority 
 

### <a name="add"></a><span data-ttu-id="0b394-146">Adicionar</span><span class="sxs-lookup"><span data-stu-id="0b394-146">Add</span></span>

<span data-ttu-id="0b394-147">Para criar uma autoridade de certificação confiável, use o cmdlet [New-AzureADTrustedCertificateAuthority](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) e defina o atributo **crlDistributionPoint** para um valor correto:</span><span class="sxs-lookup"><span data-stu-id="0b394-147">To create a trusted certificate authority, use the [New-AzureADTrustedCertificateAuthority](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet and set the **crlDistributionPoint** attribute to a correct value:</span></span> 
   
    $cert=Get-Content -Encoding byte "[LOCATION OF THE CER FILE]" 
    $new_ca=New-Object -TypeName Microsoft.Open.AzureAD.Model.CertificateAuthorityInformation 
    $new_ca.AuthorityType=0 
    $new_ca.TrustedCertificate=$cert 
    $new_ca.crlDistributionPoint=”<CRL Distribution URL>”
    New-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $new_ca 


### <a name="remove"></a><span data-ttu-id="0b394-148">Remover</span><span class="sxs-lookup"><span data-stu-id="0b394-148">Remove</span></span>

<span data-ttu-id="0b394-149">Para remover uma autoridade de certificação confiável, use o cmdlet [Remove-AzureADTrustedCertificateAuthority](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0):</span><span class="sxs-lookup"><span data-stu-id="0b394-149">To remove a trusted certificate authority, use the [Remove-AzureADTrustedCertificateAuthority](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span></span>
   
    $c=Get-AzureADTrustedCertificateAuthority 
    Remove-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[2] 


### <a name="modfiy"></a><span data-ttu-id="0b394-150">Modificar</span><span class="sxs-lookup"><span data-stu-id="0b394-150">Modfiy</span></span>

<span data-ttu-id="0b394-151">Para modificar uma autoridade de certificação confiável, use o cmdlet [Set-AzureADTrustedCertificateAuthority](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0):</span><span class="sxs-lookup"><span data-stu-id="0b394-151">To modify a trusted certificate authority, use the [Set-AzureADTrustedCertificateAuthority](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span></span>

    $c=Get-AzureADTrustedCertificateAuthority 
    $c[0].AuthorityType=1 
    Set-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[0] 


## <a name="step-3-configure-revocation"></a><span data-ttu-id="0b394-152">Etapa 3: configurar a revogação</span><span class="sxs-lookup"><span data-stu-id="0b394-152">Step 3: Configure revocation</span></span>

<span data-ttu-id="0b394-153">Para revogar um certificado do cliente, o Azure Active Directory busca a CRL (Lista de Certificados Revogados) nas URLs carregadas como parte das informações da autoridade de certificado e a armazena em cache.</span><span class="sxs-lookup"><span data-stu-id="0b394-153">To revoke a client certificate, Azure Active Directory fetches the certificate revocation list (CRL) from the URLs uploaded as part of certificate authority information and caches it.</span></span> <span data-ttu-id="0b394-154">O carimbo de data/hora da última publicação (propriedade**Effective Date** ) na CRL é usado para garantir que a CRL continua sendo válida.</span><span class="sxs-lookup"><span data-stu-id="0b394-154">The last publish timestamp (**Effective Date** property) in the CRL is used to ensure the CRL is still valid.</span></span> <span data-ttu-id="0b394-155">A CRL é referenciada periodicamente para revogar o acesso a certificados que fazem parte da lista.</span><span class="sxs-lookup"><span data-stu-id="0b394-155">The CRL is periodically referenced to revoke access to certificates that are a part of the list.</span></span>

<span data-ttu-id="0b394-156">Se uma revogação mais imediata for necessária (por exemplo, se um usuário perder um dispositivo), o token de autorização do usuário poderá ser invalidado.</span><span class="sxs-lookup"><span data-stu-id="0b394-156">If a more instant revocation is required (for example, if a user loses a device), the authorization token of the user can be invalidated.</span></span> <span data-ttu-id="0b394-157">Para invalidar o token de autorização, defina o campo **StsRefreshTokenValidFrom** para esse usuário específico usando o Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0b394-157">To invalidate the authorization token, set the **StsRefreshTokenValidFrom** field for this particular user using Windows PowerShell.</span></span> <span data-ttu-id="0b394-158">Você deve atualizar o campo **StsRefreshTokenValidFrom** para cada usuário do qual deseja revogar o acesso.</span><span class="sxs-lookup"><span data-stu-id="0b394-158">You must update the **StsRefreshTokenValidFrom** field for each user you want to revoke access for.</span></span>

<span data-ttu-id="0b394-159">Para garantir que a revogação persista, é preciso definir **Effective Date** da CRL para uma data posterior ao valor definido por **StsRefreshTokenValidFrom** e garantir que o certificado em questão esteja na CRL.</span><span class="sxs-lookup"><span data-stu-id="0b394-159">To ensure that the revocation persists, you must set the **Effective Date** of the CRL to a date after the value set by **StsRefreshTokenValidFrom** and ensure the certificate in question is in the CRL.</span></span>

<span data-ttu-id="0b394-160">As etapas a seguir descrevem o processo para atualizar e invalidar o token de autorização pela definição do campo **StsRefreshTokenValidFrom** .</span><span class="sxs-lookup"><span data-stu-id="0b394-160">The following steps outline the process for updating and invalidating the authorization token by setting the **StsRefreshTokenValidFrom** field.</span></span> 

<span data-ttu-id="0b394-161">**Para configurar a revogação:**</span><span class="sxs-lookup"><span data-stu-id="0b394-161">**To configure revocation:**</span></span> 

1. <span data-ttu-id="0b394-162">Conecte-se com credenciais de administrador ao serviço MSOL:</span><span class="sxs-lookup"><span data-stu-id="0b394-162">Connect with admin credentials to the MSOL service:</span></span> 
   
        $msolcred = get-credential 
        connect-msolservice -credential $msolcred 

2. <span data-ttu-id="0b394-163">Recupere o valor StsRefreshTokensValidFrom atual para um usuário:</span><span class="sxs-lookup"><span data-stu-id="0b394-163">Retrieve the current StsRefreshTokensValidFrom value for a user:</span></span> 
   
        $user = Get-MsolUser -UserPrincipalName test@yourdomain.com` 
        $user.StsRefreshTokensValidFrom 

3. <span data-ttu-id="0b394-164">Configure um novo valor StsRefreshTokensValidFrom para o usuário igual ao carimbo de data/hora atual:</span><span class="sxs-lookup"><span data-stu-id="0b394-164">Configure a new StsRefreshTokensValidFrom value for the user equal to the current timestamp:</span></span> 
   
        Set-MsolUser -UserPrincipalName test@yourdomain.com -StsRefreshTokensValidFrom ("03/05/2016")

<span data-ttu-id="0b394-165">A data que você define deve estar no futuro.</span><span class="sxs-lookup"><span data-stu-id="0b394-165">The date you set must be in the future.</span></span> <span data-ttu-id="0b394-166">Se a data não estiver no futuro, a propriedade **StsRefreshTokensValidFrom** não será definida.</span><span class="sxs-lookup"><span data-stu-id="0b394-166">If the date is not in the future, the **StsRefreshTokensValidFrom** property is not set.</span></span> <span data-ttu-id="0b394-167">Se a data estiver no futuro, **StsRefreshTokensValidFrom** será definida para a hora atual (não a data indicada pelo comando Set-MsolUser).</span><span class="sxs-lookup"><span data-stu-id="0b394-167">If the date is in the future, **StsRefreshTokensValidFrom** is set to the current time (not the date indicated by Set-MsolUser command).</span></span> 


## <a name="step-4-test-your-configuration"></a><span data-ttu-id="0b394-168">Etapa 4: testar a sua configuração</span><span class="sxs-lookup"><span data-stu-id="0b394-168">Step 4: Test your configuration</span></span>

### <a name="testing-your-certificate"></a><span data-ttu-id="0b394-169">Teste do seu certificado</span><span class="sxs-lookup"><span data-stu-id="0b394-169">Testing your certificate</span></span>

<span data-ttu-id="0b394-170">Como primeiro teste de configuração, entre no [Outlook Web Access](https://outlook.office365.com) ou no [SharePoint Online](https://microsoft.sharepoint.com) usando seu **navegador no dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="0b394-170">As a first configuration test, you should try to sign in to [Outlook Web Access](https://outlook.office365.com) or [SharePoint Online](https://microsoft.sharepoint.com) using your **on-device browser**.</span></span>

<span data-ttu-id="0b394-171">Se a entrada for bem-sucedida, você saberá que:</span><span class="sxs-lookup"><span data-stu-id="0b394-171">If your sign-in is successful, then you know that:</span></span>

- <span data-ttu-id="0b394-172">O certificado de usuário foi provisionado para o seu dispositivo de teste</span><span class="sxs-lookup"><span data-stu-id="0b394-172">The user certificate has been provisioned to your test device</span></span>
- <span data-ttu-id="0b394-173">O AD FS está configurado corretamente</span><span class="sxs-lookup"><span data-stu-id="0b394-173">AD FS is configured correctly</span></span>  


### <a name="testing-office-mobile-applications"></a><span data-ttu-id="0b394-174">Testando aplicativos móveis do Office</span><span class="sxs-lookup"><span data-stu-id="0b394-174">Testing Office mobile applications</span></span>

<span data-ttu-id="0b394-175">**Para testar a autenticação baseada em certificado no seu aplicativo móvel do Office:**</span><span class="sxs-lookup"><span data-stu-id="0b394-175">**To test certificate-based authentication on your mobile Office application:**</span></span> 

1. <span data-ttu-id="0b394-176">No seu dispositivo de teste, instale um aplicativo móvel do Office (por exemplo, OneDrive).</span><span class="sxs-lookup"><span data-stu-id="0b394-176">On your test device, install an Office mobile application (e.g., OneDrive).</span></span>
3. <span data-ttu-id="0b394-177">Inicie o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0b394-177">Launch the application.</span></span> 
4. <span data-ttu-id="0b394-178">Insira seu nome de usuário e escolha o certificado de usuário que deseja usar.</span><span class="sxs-lookup"><span data-stu-id="0b394-178">Enter your user name, and then select the user certificate you want to use.</span></span> 

<span data-ttu-id="0b394-179">Você deve se conectar com êxito.</span><span class="sxs-lookup"><span data-stu-id="0b394-179">You should be successfully signed in.</span></span> 

### <a name="testing-exchange-activesync-client-applications"></a><span data-ttu-id="0b394-180">Testando aplicativos cliente do Exchange ActiveSync</span><span class="sxs-lookup"><span data-stu-id="0b394-180">Testing Exchange ActiveSync client applications</span></span>

<span data-ttu-id="0b394-181">Para acessar o Exchange ActiveSync (EAS) por meio da autenticação baseada em certificado, um perfil do EAS que contém o certificado de cliente deve estar disponível para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0b394-181">To access Exchange ActiveSync (EAS) via certificate-based authentication, an EAS profile containing the client certificate must be available to the application.</span></span> 

<span data-ttu-id="0b394-182">O perfil do EAS deve conter as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="0b394-182">The EAS profile must contain the following information:</span></span>

- <span data-ttu-id="0b394-183">O certificado do usuário a ser usado para autenticação</span><span class="sxs-lookup"><span data-stu-id="0b394-183">The user certificate to be used for authentication</span></span> 

- <span data-ttu-id="0b394-184">O ponto de extremidade do EAS (por exemplo, outlook.office365.com)</span><span class="sxs-lookup"><span data-stu-id="0b394-184">The EAS endpoint (for example, outlook.office365.com)</span></span>

<span data-ttu-id="0b394-185">Um perfil do EAS pode ser configurado e colocado no dispositivo por meio da utilização de um gerenciamento de dispositivo móvel (MDM), como o Intune, ou colocando o certificado manualmente no perfil do EAS no dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0b394-185">An EAS profile can be configured and placed on the device through the utilization of Mobile device management (MDM) such as Intune or by manually placing the certificate in the EAS profile on the device.</span></span>  

### <a name="testing-eas-client-applications-on-android"></a><span data-ttu-id="0b394-186">Testando os aplicativos cliente do EAS no Android</span><span class="sxs-lookup"><span data-stu-id="0b394-186">Testing EAS client applications on Android</span></span>

<span data-ttu-id="0b394-187">**Para testar a autenticação do certificado:**</span><span class="sxs-lookup"><span data-stu-id="0b394-187">**To test certificate authentication:**</span></span>  

1. <span data-ttu-id="0b394-188">Configure um perfil do EAS no aplicativo que atenda aos requisitos acima.</span><span class="sxs-lookup"><span data-stu-id="0b394-188">Configure an EAS profile in the application that satisfies the requirements above.</span></span>  
2. <span data-ttu-id="0b394-189">Abra o aplicativo e verifique a sincronização de email.</span><span class="sxs-lookup"><span data-stu-id="0b394-189">Open the application, and verify that mail is synchronizing.</span></span> 

