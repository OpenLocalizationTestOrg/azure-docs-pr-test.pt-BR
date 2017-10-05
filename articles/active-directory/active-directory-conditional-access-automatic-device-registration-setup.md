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
ms.date: 06/16/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: dccd7df6a5f85df4179c7ea7cfc476cfb57f48c0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-automatic-registration-of-windows-domain-joined-devices-with-azure-active-directory"></a><span data-ttu-id="b4ac4-103">Como configurar o registro automático de dispositivos ingressados no domínio do Windows com o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b4ac4-103">How to configure automatic registration of Windows domain-joined devices with Azure Active Directory</span></span>

<span data-ttu-id="b4ac4-104">Para usar o [Acesso condicional baseado no dispositivo do Azure Active Directory](active-directory-conditional-access-azure-portal.md), seus computadores devem estar registrados no Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b4ac4-104">To use [Azure Active Directory device-based conditional access](active-directory-conditional-access-azure-portal.md), your computers must be registered with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="b4ac4-105">Você pode obter uma lista dos dispositivos registrados na sua organização usando o cmdlet [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) no [módulo do Azure Active Directory PowerShell](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="b4ac4-105">You can get a list of registered devices in your organization by using the [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in the [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span> 

<span data-ttu-id="b4ac4-106">Este artigo fornece as etapas para configurar o registro automático de dispositivos ingressados no domínio do Windows com o Azure AD em sua organização.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-106">This article provides you with the steps for configuring the automatic registration of Windows domain-joined devices with Azure AD in your organization.</span></span>


<span data-ttu-id="b4ac4-107">Para saber mais sobre:</span><span class="sxs-lookup"><span data-stu-id="b4ac4-107">For more information about:</span></span>

- <span data-ttu-id="b4ac4-108">Acesso condicional, confira [Acesso condicional com base no dispositivo ao Azure Active Directory](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b4ac4-108">Conditional access, see [Azure Active Directory device-based conditional access](active-directory-conditional-access-azure-portal.md).</span></span> 
- <span data-ttu-id="b4ac4-109">Dispositivos Windows 10 no local de trabalho e as experiências aprimoradas quando registrado com o Azure AD, consulte [Windows 10 para a empresa: usar dispositivos para o trabalho](active-directory-azureadjoin-windows10-devices-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b4ac4-109">Windows 10 devices in the workplace and the enhanced experiences when registered with Azure AD, see [Windows 10 for the enterprise: Use devices for work](active-directory-azureadjoin-windows10-devices-overview.md).</span></span>
- <span data-ttu-id="b4ac4-110">Windows 10 Enterprise E3 no CSP, consulte a [Visão Geral do Windows 10 Enterprise E3 no CSP](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview).</span><span class="sxs-lookup"><span data-stu-id="b4ac4-110">Windows 10 Enterprise E3 in CSP, see the [Windows 10 Enterprise E3 in CSP Overview](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="b4ac4-111">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="b4ac4-111">Before you begin</span></span>

<span data-ttu-id="b4ac4-112">Antes de começar a configurar o registro automático dos dispositivos associados ao domínio do Windows no seu ambiente, você deve se familiarizar com os cenários com suporte e as restrições.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-112">Before you start configuring the automatic registration of Windows domain-joined devices in your environment, you should familiarize yourself with the supported scenarios and the constraints.</span></span>  

<span data-ttu-id="b4ac4-113">Para melhorar a legibilidade das descrições, este tópico usa o termo a seguir:</span><span class="sxs-lookup"><span data-stu-id="b4ac4-113">To improve the readability of the descriptions, this topic uses the following term:</span></span> 

- <span data-ttu-id="b4ac4-114">**Dispositivos atuais do Windows** - este termo refere-se aos dispositivos associados ao domínio que executam o Windows 10 ou o Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-114">**Windows current devices** - This term refers to domain-joined devices running Windows 10 or Windows Server 2016.</span></span>
- <span data-ttu-id="b4ac4-115">**Dispositivos de baixo nível do Windows** - este termo refere-se a todos os dispositivos do Windows associados ao domínio **com suporte** que não estão executando o Windows 10 nem o Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-115">**Windows down-level devices** - This term refers to all **supported** domain-joined Windows devices that are neither running Windows 10 nor Windows Server 2016.</span></span>  


### <a name="windows-current-devices"></a><span data-ttu-id="b4ac4-116">Dispositivos atuais do Windows</span><span class="sxs-lookup"><span data-stu-id="b4ac4-116">Windows current devices</span></span>

- <span data-ttu-id="b4ac4-117">Para os dispositivos que executam o sistema operacional da área de trabalho do Windows, é recomendável usar a Atualização de Aniversário do Windows 10 (versão 1607) ou posterior.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-117">For devices running the Windows desktop operating system, we recommend using Windows 10 Anniversary Update (version 1607) or later.</span></span> 
- <span data-ttu-id="b4ac4-118">O registro de dispositivos atuais do Windows **tem** suporte em ambientes não-federados, como configurações de sincronização de hash de senha.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-118">The registration of Windows current devices **is** supported in non-federated environments such as password hash sync configurations.</span></span>  


### <a name="windows-down-level-devices"></a><span data-ttu-id="b4ac4-119">Dispositivos de nível inferior do Windows</span><span class="sxs-lookup"><span data-stu-id="b4ac4-119">Windows down-level devices</span></span>

- <span data-ttu-id="b4ac4-120">Há suporte para os seguintes dispositivos de nível inferior do Windows:</span><span class="sxs-lookup"><span data-stu-id="b4ac4-120">The following Windows down-level devices are supported:</span></span>
    - <span data-ttu-id="b4ac4-121">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="b4ac4-121">Windows 8.1</span></span>
    - <span data-ttu-id="b4ac4-122">Windows 7</span><span class="sxs-lookup"><span data-stu-id="b4ac4-122">Windows 7</span></span>
    - <span data-ttu-id="b4ac4-123">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="b4ac4-123">Windows Server 2012 R2</span></span>
    - <span data-ttu-id="b4ac4-124">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="b4ac4-124">Windows Server 2012</span></span>
    - <span data-ttu-id="b4ac4-125">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="b4ac4-125">Windows Server 2008 R2</span></span>
- <span data-ttu-id="b4ac4-126">O registro de dispositivos de nível inferior do Windows **tem** suporte em ambientes não federados por meio do Logon Único Contínuo [Logon Único Contínuo do Azure Active Directory](https://aka.ms/hybrid/sso).</span><span class="sxs-lookup"><span data-stu-id="b4ac4-126">The registration of Windows down-level devices **is** supported in non-federated environments through Seamless Single Sign On [Azure Active Directory Seamless Single Sign-On](https://aka.ms/hybrid/sso).</span></span>
- <span data-ttu-id="b4ac4-127">O registro de dispositivos de nível inferior do Windows **não tem** suporte para dispositivos que utilizam perfis móveis.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-127">The registration of Windows down-level devices **is not** supported for devices using roaming profiles.</span></span> <span data-ttu-id="b4ac4-128">Se você depender da mobilidade de perfis ou configurações, use o Windows 10.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-128">If you are relying on roaming of profiles or settings, use Windows 10.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="b4ac4-129">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b4ac4-129">Prerequisites</span></span>

<span data-ttu-id="b4ac4-130">Antes de começar a habilitar o registro automático dos dispositivos associados ao domínio na sua organização, você precisará garantir que esteja executando uma versão atualizada do Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-130">Before you start enabling the auto-registration of domain-joined devices in your organization, you need to make sure that you are running an up-to-date version of Azure AD connect.</span></span>

<span data-ttu-id="b4ac4-131">Azure AD Connect:</span><span class="sxs-lookup"><span data-stu-id="b4ac4-131">Azure AD Connect:</span></span>

- <span data-ttu-id="b4ac4-132">Mantém a associação entre a conta do computador no seu Active Directory (AD) local e o objeto do dispositivo no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-132">Keeps the association between the computer account in your on-premises Active Directory (AD) and the device object in Azure AD.</span></span> 
- <span data-ttu-id="b4ac4-133">Permite outros recursos relacionados ao dispositivo, como o Windows Hello for Business.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-133">Enables other device related features like Windows Hello for Business.</span></span>



## <a name="configuration-steps"></a><span data-ttu-id="b4ac4-134">Etapas da configuração</span><span class="sxs-lookup"><span data-stu-id="b4ac4-134">Configuration steps</span></span>

<span data-ttu-id="b4ac4-135">Este tópico inclui as etapas necessárias para todos os cenários de configuração típicos.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-135">This topic includes the required steps for all typical configuration scenarios.</span></span>  
<span data-ttu-id="b4ac4-136">Use a tabela a seguir para ter uma visão geral das etapas necessárias para o seu cenário:</span><span class="sxs-lookup"><span data-stu-id="b4ac4-136">Use the following table to get an overview of the steps that are required for your scenario:</span></span>  



| <span data-ttu-id="b4ac4-137">Etapas</span><span class="sxs-lookup"><span data-stu-id="b4ac4-137">Steps</span></span>                                      | <span data-ttu-id="b4ac4-138">Sincronização de hash de senha e do Windows atual</span><span class="sxs-lookup"><span data-stu-id="b4ac4-138">Windows current and password hash sync</span></span> | <span data-ttu-id="b4ac4-139">Windows atual e a federação</span><span class="sxs-lookup"><span data-stu-id="b4ac4-139">Windows current and federation</span></span> | <span data-ttu-id="b4ac4-140">Nível inferior do Windows</span><span class="sxs-lookup"><span data-stu-id="b4ac4-140">Windows down-level</span></span> |
| :--                                        | :-:                                    | :-:                            | :-:                |
| <span data-ttu-id="b4ac4-141">Etapa 1: configurar o ponto de conexão de serviço</span><span class="sxs-lookup"><span data-stu-id="b4ac4-141">Step 1: Configure service connection point</span></span> | ![Verificação][1]                            | ![Verificação][1]                    | ![Verificação][1]        |
| <span data-ttu-id="b4ac4-145">Etapa 2: configurar a emissão de declarações</span><span class="sxs-lookup"><span data-stu-id="b4ac4-145">Step 2: Setup issuance of claims</span></span>           |                                        | ![Verificação][1]                    | ![Verificação][1]        |
| <span data-ttu-id="b4ac4-148">Etapa 3: habilitar dispositivos não Windows 10</span><span class="sxs-lookup"><span data-stu-id="b4ac4-148">Step 3: Enable non-Windows 10 devices</span></span>      |                                        |                                | ![Verificação][1]        |
| <span data-ttu-id="b4ac4-150">Etapa 4: implantação de controle e distribuição</span><span class="sxs-lookup"><span data-stu-id="b4ac4-150">Step 4: Control deployment and rollout</span></span>     | ![Verificação][1]                            | ![Verificação][1]                    | ![Verificação][1]        |
| <span data-ttu-id="b4ac4-154">Etapa 5: verificar os dispositivos registrados</span><span class="sxs-lookup"><span data-stu-id="b4ac4-154">Step 5: Verify registered devices</span></span>          | ![Verificação][1]                            | ![Verificação][1]                    | ![Verificação][1]        |



## <a name="step-1-configure-service-connection-point"></a><span data-ttu-id="b4ac4-158">Etapa 1: configurar o ponto de conexão de serviço</span><span class="sxs-lookup"><span data-stu-id="b4ac4-158">Step 1: Configure service connection point</span></span>

<span data-ttu-id="b4ac4-159">O objeto de ponto de conexão de serviço (SCP) é usado por seus dispositivos durante o registro para descobrir informações de locatário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-159">The service connection point (SCP) object is used by your devices during the registration to discover Azure AD tenant information.</span></span> <span data-ttu-id="b4ac4-160">No seu Active Directory (AD) local, o objeto de SCP para o registro automático de dispositivos associados ao domínio deve existir na partição do contexto de nomenclatura da configuração da floresta do computador.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-160">In your on-premises Active Directory (AD), the SCP object for the auto-registration of domain-joined devices must exist in the configuration naming context partition of the computer's forest.</span></span> <span data-ttu-id="b4ac4-161">Há apenas um contexto de nomenclatura de configuração por floresta.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-161">There is only one configuration naming context per forest.</span></span> <span data-ttu-id="b4ac4-162">Em uma configuração de várias florestas do Active Directory, deverá haver um ponto de conexão de serviço em todas as florestas que tiverem computadores associados ao domínio.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-162">In a multi-forest Active Directory configuration, the service connection point must exist in all forests containing domain-joined computers.</span></span>

<span data-ttu-id="b4ac4-163">Você pode usar o cmdlet [ **Get-ADRootDSE**](https://technet.microsoft.com/library/ee617246.aspx) para recuperar o contexto de nomenclatura de configuração da sua floresta.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-163">You can use the [**Get-ADRootDSE**](https://technet.microsoft.com/library/ee617246.aspx) cmdlet to retrieve the configuration naming context of your forest.</span></span>  

<span data-ttu-id="b4ac4-164">Para uma floresta com um nome de domínio do Active Directory *fabrikam.com*, o contexto de nomenclatura de configuração é:</span><span class="sxs-lookup"><span data-stu-id="b4ac4-164">For a forest with the Active Directory domain name *fabrikam.com*, the configuration naming context is:</span></span>

`CN=Configuration,DC=fabrikam,DC=com`

<span data-ttu-id="b4ac4-165">Na sua floresta, o objeto de SCP para o registro automático de dispositivos associados ao domínio está localizado em:</span><span class="sxs-lookup"><span data-stu-id="b4ac4-165">In your forest, the SCP object for the auto-registration of domain-joined devices is located at:</span></span>  

`CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,[Your Configuration Naming Context]`

<span data-ttu-id="b4ac4-166">Dependendo de como você implantou o Azure AD Connect, o objeto SCP pode ter já ter sido configurado.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-166">Depending on how you have deployed Azure AD Connect, the SCP object may have already been configured.</span></span>
<span data-ttu-id="b4ac4-167">Você pode verificar a existência do objeto e recuperar os valores da descoberta usando o seguinte script do Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="b4ac4-167">You can verify the existence of the object and retrieve the discovery values using the following Windows PowerShell script:</span></span> 

    $scp = New-Object System.DirectoryServices.DirectoryEntry;

    $scp.Path = "LDAP://CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=fabrikam,DC=com";

    $scp.Keywords;

<span data-ttu-id="b4ac4-168">A saída **$scp.Keywords** mostra as informações de locatário do Azure AD, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b4ac4-168">The **$scp.Keywords** output shows the Azure AD tenant information, for example:</span></span>

    azureADName:microsoft.com
    azureADId:72f988bf-86f1-41af-91ab-2d7cd011db47

<span data-ttu-id="b4ac4-169">Se o ponto de conexão do serviço não existir, você poderá criá-lo executando o cmdlet `Initialize-ADSyncDomainJoinedComputerSync` no seu servidor do Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-169">If the service connection point does not exist, you can create it by running the `Initialize-ADSyncDomainJoinedComputerSync` cmdlet on your Azure AD Connect server.</span></span> <span data-ttu-id="b4ac4-170">As credenciais do admin corporativo são necessárias para executar este cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-170">Enterprise admin credential is required to run this cmdlet.</span></span>  
<span data-ttu-id="b4ac4-171">O cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b4ac4-171">The cmdlet:</span></span>

- <span data-ttu-id="b4ac4-172">Cria o ponto de conexão de serviço na floresta do Active Directory à qual o Azure AD Connect está conectado.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-172">Creates the service connection point in the Active Directory forest Azure AD Connect is connected to.</span></span> 
- <span data-ttu-id="b4ac4-173">Exige que você especifique o parâmetro `AdConnectorAccount`.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-173">Requires you to specify the `AdConnectorAccount` parameter.</span></span> <span data-ttu-id="b4ac4-174">Essa é a conta que está configurada como a conta do conector do Active Directory no Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-174">This is the account that is configured as Active Directory connector account in Azure AD connect.</span></span> 


<span data-ttu-id="b4ac4-175">O script a seguir mostra um exemplo de uso do cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-175">The following script shows an example for using the cmdlet.</span></span> <span data-ttu-id="b4ac4-176">Nesse script, `$aadAdminCred = Get-Credential` exige que você digite um nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-176">In this script, `$aadAdminCred = Get-Credential` requires you to type a user name.</span></span> <span data-ttu-id="b4ac4-177">Você precisa fornecer o nome de usuário no formato de nome principal (UPN) do usuário (`user@example.com`).</span><span class="sxs-lookup"><span data-stu-id="b4ac4-177">You need to provide the user name in the user principal name (UPN) format (`user@example.com`).</span></span> 


    Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1";

    $aadAdminCred = Get-Credential;

    Initialize-ADSyncDomainJoinedComputerSync –AdConnectorAccount [connector account name] -AzureADCredentials $aadAdminCred;

<span data-ttu-id="b4ac4-178">O cmdlet `Initialize-ADSyncDomainJoinedComputerSync`:</span><span class="sxs-lookup"><span data-stu-id="b4ac4-178">The `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:</span></span>

- <span data-ttu-id="b4ac4-179">Usa o módulo Active Directory PowerShell, que se baseia nos Serviços Web do Active Directory em execução em um controlador de domínio.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-179">Uses the Active Directory PowerShell module, which relies on Active Directory Web Services running on a domain controller.</span></span> <span data-ttu-id="b4ac4-180">Os Serviços Web do Active Directory têm suporte em controladores de domínio executando o Windows Server 2008 R2 e posterior.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-180">Active Directory Web Services is supported on domain controllers running Windows Server 2008 R2 and later.</span></span>
- <span data-ttu-id="b4ac4-181">Há suporte somente para a **versão do módulo 1.1.166.0 do MSOnline PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-181">Is only supported by the **MSOnline PowerShell module version 1.1.166.0**.</span></span> <span data-ttu-id="b4ac4-182">Para baixar este módulo, use este [link](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span><span class="sxs-lookup"><span data-stu-id="b4ac4-182">To download this module, use this [link](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span></span>   

<span data-ttu-id="b4ac4-183">Para controladores de domínio executando o Windows Server 2008 ou versões anteriores, use o script abaixo para criar o ponto de conexão de serviço.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-183">For domain controllers running Windows Server 2008 or earlier versions, use the script below to create the service connection point.</span></span>

<span data-ttu-id="b4ac4-184">Em uma configuração de várias florestas, você deve usar o script a seguir para criar o ponto de conexão de serviço em cada floresta onde existam computadores:</span><span class="sxs-lookup"><span data-stu-id="b4ac4-184">In a multi-forest configuration, you should use the following script to create the service connection point in each forest where computers exist:</span></span>
 
    $verifiedDomain = "contoso.com"    # Replace this with any of your verified domain names in Azure AD
    $tenantID = "72f988bf-86f1-41af-91ab-2d7cd011db47"    # Replace this with you tenant ID
    $configNC = "CN=Configuration,DC=corp,DC=contoso,DC=com"    # Replace this with your AD configuration naming context

    $de = New-Object System.DirectoryServices.DirectoryEntry
    $de.Path = "LDAP://CN=Services," + $configNC

    $deDRC = $de.Children.Add("CN=Device Registration Configuration", "container")
    $deDRC.CommitChanges()

    $deSCP = $deDRC.Children.Add("CN=62a0ff2e-97b9-4513-943f-0d221bd30080", "serviceConnectionPoint")
    $deSCP.Properties["keywords"].Add("azureADName:" + $verifiedDomain)
    $deSCP.Properties["keywords"].Add("azureADId:" + $tenantID)

    $deSCP.CommitChanges()


## <a name="step-2-setup-issuance-of-claims"></a><span data-ttu-id="b4ac4-185">Etapa 2: configurar a emissão de declarações</span><span class="sxs-lookup"><span data-stu-id="b4ac4-185">Step 2: Setup issuance of claims</span></span>

<span data-ttu-id="b4ac4-186">Em uma configuração do Azure AD federada, os dispositivos confiam nos Serviços de Federação do Active Directory (AD FS) ou no serviço de federação local de um terceiro para se autenticar no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-186">In a federated Azure AD configuration, devices rely on Active Directory Federation Services (AD FS) or a 3rd party on-premises federation service to authenticate to Azure AD.</span></span> <span data-ttu-id="b4ac4-187">Os dispositivos são autenticados para obter um token de acesso para se registrar com o Serviço de Registro de Dispositivo (Azure DRS) do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-187">Devices authenticate to get an access token to register against the Azure Active Directory Device Registration Service (Azure DRS).</span></span>

<span data-ttu-id="b4ac4-188">Os dispositivos atuais do Windows são autenticados usando a Autenticação Integrada do Windows para um ponto de extremidade WS-Trust ativo (versões 1.3 ou 2005) hospedado pelo serviço de federação local.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-188">Windows current devices authenticate using Integrated Windows Authentication to an active WS-Trust endpoint (either 1.3 or 2005 versions) hosted by the on-premises federation service.</span></span>

> [!NOTE]
> <span data-ttu-id="b4ac4-189">Ao usar o AD FS, **adfs/services/trust/13/windowstransport** ou **adfs/services/trust/2005/windowstransport** devem ser habilitados.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-189">When using AD FS, either **adfs/services/trust/13/windowstransport** or **adfs/services/trust/2005/windowstransport** must be enabled.</span></span> <span data-ttu-id="b4ac4-190">Se você estiver usando o proxy Web de autenticação, verifique também se esse ponto de extremidade pode ser publicado por meio do proxy.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-190">If you are using the Web Authentication Proxy, also ensure that this endpoint is published through the proxy.</span></span> <span data-ttu-id="b4ac4-191">Você pode ver quais pontos de extremidade são habilitados por meio do console de gerenciamento do AD FS em **Serviço > pontos de extremidade**.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-191">You can see what end-points are enabled through the AD FS management console under **Service > Endpoints**.</span></span>
>
><span data-ttu-id="b4ac4-192">Se você não tiver o AD FS como seu serviço de federação local, siga as instruções do seu fornecedor para garantir que ele ofereça suporte aos pontos de extremidade WS-Trust 1.3 ou 2005 e que eles sejam publicados por meio do Arquivo de Troca de Metadados (MEX).</span><span class="sxs-lookup"><span data-stu-id="b4ac4-192">If you don’t have AD FS as your on-premises federation service, follow the instructions of your vendor to make sure they support WS-Trust 1.3 or 2005 end-points and that these are published through the Metadata Exchange file (MEX).</span></span>

<span data-ttu-id="b4ac4-193">As seguintes declarações devem existir no token recebido pelo DRS do Azure para que o registro do dispositivo seja concluído.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-193">The following claims must exist in the token received by Azure DRS for device registration to complete.</span></span> <span data-ttu-id="b4ac4-194">O DRS do Azure criará um objeto de dispositivo no Azure AD com algumas dessas informações que são usadas pelo Azure AD Connect para associar o objeto de dispositivo recém-criado à conta do computador local.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-194">Azure DRS will create a device object in Azure AD with some of this information which is then used by Azure AD Connect to associate the newly created device object with the computer account on-premises.</span></span>

* `http://schemas.microsoft.com/ws/2012/01/accounttype`
* `http://schemas.microsoft.com/identity/claims/onpremobjectguid`
* `http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`

<span data-ttu-id="b4ac4-195">Se você tiver mais de um nome de domínio verificado, precisará fornecer a seguinte declaração para os computadores:</span><span class="sxs-lookup"><span data-stu-id="b4ac4-195">If you have more than one verified domain name, you need to provide the following claim for computers:</span></span>

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`

<span data-ttu-id="b4ac4-196">Se você já estiver emitindo uma declaração ImmutableID (por exemplo, a ID de logon alternativo), precisará fornecer uma declaração correspondente para os computadores:</span><span class="sxs-lookup"><span data-stu-id="b4ac4-196">If you are already issuing an ImmutableID claim (e.g., alternate login ID) you need to provide one corresponding claim for computers:</span></span>

* `http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`

<span data-ttu-id="b4ac4-197">Nas seções a seguir, você encontrará informações sobre:</span><span class="sxs-lookup"><span data-stu-id="b4ac4-197">In the following sections, you find information about:</span></span>
 
- <span data-ttu-id="b4ac4-198">Os valores de que cada declaração deve ter</span><span class="sxs-lookup"><span data-stu-id="b4ac4-198">The values each claim should have</span></span>
- <span data-ttu-id="b4ac4-199">Como uma definição se pareceria no AD FS</span><span class="sxs-lookup"><span data-stu-id="b4ac4-199">How a definition would look like in AD FS</span></span>

<span data-ttu-id="b4ac4-200">A definição ajuda você a verificar se os valores estão presentes ou se você precisa criá-los.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-200">The definition helps you to verify whether the values are present or if you need to create them.</span></span>

> [!NOTE]
> <span data-ttu-id="b4ac4-201">Se você não usar o AD FS para o servidor de federação local, siga as instruções do fornecedor para criar a configuração adequada para emitir essas declarações.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-201">If you don’t use AD FS for your on-premises federation server, follow your vendor's instructions to create the appropriate configuration to issue these claims.</span></span>

### <a name="issue-account-type-claim"></a><span data-ttu-id="b4ac4-202">Emitir declaração de tipo de conta</span><span class="sxs-lookup"><span data-stu-id="b4ac4-202">Issue account type claim</span></span>

<span data-ttu-id="b4ac4-203">**`http://schemas.microsoft.com/ws/2012/01/accounttype`** - Essa declaração deve conter um valor de **DJ**, que identifica o dispositivo como um computador associado ao domínio.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-203">**`http://schemas.microsoft.com/ws/2012/01/accounttype`** - This claim must contain a value of **DJ**, which identifies the device as a domain-joined computer.</span></span> <span data-ttu-id="b4ac4-204">No AD FS, você pode adicionar uma regra de transformação de emissão que se parece com o seguinte:</span><span class="sxs-lookup"><span data-stu-id="b4ac4-204">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

    @RuleName = "Issue account type for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "DJ"
    );

### <a name="issue-objectguid-of-the-computer-account-on-premises"></a><span data-ttu-id="b4ac4-205">Emita o objectGUID da conta do computador local</span><span class="sxs-lookup"><span data-stu-id="b4ac4-205">Issue objectGUID of the computer account on-premises</span></span>

<span data-ttu-id="b4ac4-206">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`** - Essa declaração deve conter o valor do **objectGUID** da conta do computador local.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-206">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`** - This claim must contain the **objectGUID** value of the on-premises computer account.</span></span> <span data-ttu-id="b4ac4-207">No AD FS, você pode adicionar uma regra de transformação de emissão que se parece com o seguinte:</span><span class="sxs-lookup"><span data-stu-id="b4ac4-207">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

    @RuleName = "Issue object GUID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/identity/claims/onpremobjectguid"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );
 
### <a name="issue-objectsid-of-the-computer-account-on-premises"></a><span data-ttu-id="b4ac4-208">Emita o objectSID da conta do computador local</span><span class="sxs-lookup"><span data-stu-id="b4ac4-208">Issue objectSID of the computer account on-premises</span></span>

<span data-ttu-id="b4ac4-209">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`** - Essa declaração deve conter o valor do **objectSid** da conta do computador local.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-209">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`** - This claim must contain the the **objectSid** value of the on-premises computer account.</span></span> <span data-ttu-id="b4ac4-210">No AD FS, você pode adicionar uma regra de transformação de emissão que se parece com o seguinte:</span><span class="sxs-lookup"><span data-stu-id="b4ac4-210">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

    @RuleName = "Issue objectSID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(claim = c2);

### <a name="issue-issuerid-for-computer-when-multiple-verified-domain-names-in-azure-ad"></a><span data-ttu-id="b4ac4-211">Emita o issuerID de computador quando houver vários nomes de domínio verificados no Azure AD</span><span class="sxs-lookup"><span data-stu-id="b4ac4-211">Issue issuerID for computer when multiple verified domain names in Azure AD</span></span>

<span data-ttu-id="b4ac4-212">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`** - Essa declaração deve conter o Uniform Resource Identifier (URI) de qualquer um dos nomes de domínio verificados que se conectam ao serviço de federação local (AD FS ou terceiro) que emite o token.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-212">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`** - This claim must contain the Uniform Resource Identifier (URI) of any of the verified domain names that connect with the on-premises federation service (AD FS or 3rd party) issuing the token.</span></span> <span data-ttu-id="b4ac4-213">No AD FS, você pode adicionar regras de transformação de emissão parecidas com aquelas abaixo na ordem específica após as mostradas acima.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-213">In AD FS, you can add issuance transform rules that look like the ones below in that specific order after the ones above.</span></span> <span data-ttu-id="b4ac4-214">Observe que é necessária uma regra para emitir explicitamente a regra para usuários.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-214">Please note that one rule to explicitly issue the rule for users is necessary.</span></span> <span data-ttu-id="b4ac4-215">Nas regras abaixo, é adicionada uma primeira regra de identificação do usuário vs. a autenticação do computador.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-215">In the rules below, a first rule identifying user vs. computer authentication is added.</span></span>

    @RuleName = "Issue account type with the value User when its not a computer"
    NOT EXISTS(
    [
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "DJ"
    ]
    )
    => add(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "User"
    );
    
    @RuleName = "Capture UPN when AccountType is User and issue the IssuerID"
    c1:[
        Type == "http://schemas.xmlsoap.org/claims/UPN"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "User"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = regexreplace(
        c1.Value, 
        ".+@(?<domain>.+)", 
        "http://${domain}/adfs/services/trust/"
        )
    );
    
    @RuleName = "Issue issuerID for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = "http://<verified-domain-name>/adfs/services/trust/"
    );


<span data-ttu-id="b4ac4-216">Na declaração acima,</span><span class="sxs-lookup"><span data-stu-id="b4ac4-216">In the claim above,</span></span>

- <span data-ttu-id="b4ac4-217">`$<domain>` é a URL de serviço do AD FS</span><span class="sxs-lookup"><span data-stu-id="b4ac4-217">`$<domain>` is the AD FS service URL</span></span>
- <span data-ttu-id="b4ac4-218">`<verified-domain-name>` é um espaço reservado que você precisa substituir por um de seus nomes de domínio verificado no Azure AD</span><span class="sxs-lookup"><span data-stu-id="b4ac4-218">`<verified-domain-name>` is a placeholder you need to replace with one of your verified domain names in Azure AD</span></span>



<span data-ttu-id="b4ac4-219">Para obter mais detalhes sobre nomes de domínio verificados, confira [Adicionar um nome de domínio ao Azure Active Directory](active-directory-add-domain.md).</span><span class="sxs-lookup"><span data-stu-id="b4ac4-219">For more details about verified domain names, see [Add a custom domain name to Azure Active Directory](active-directory-add-domain.md).</span></span>  
<span data-ttu-id="b4ac4-220">Para obter uma lista dos domínios da empresa verificados, você pode usar o cmdlet [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0).</span><span class="sxs-lookup"><span data-stu-id="b4ac4-220">To get a list of your verified company domains, you can use the [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet.</span></span> 

![Get-MsolDomain](./media/active-directory-conditional-access-automatic-device-registration-setup/01.png)

### <a name="issue-immutableid-for-computer-when-one-for-users-exist-eg-alternate-login-id-is-set"></a><span data-ttu-id="b4ac4-222">Emitir o ImmutableID de computador quando houver um para o usuário (por exemplo, a ID de login alternativa é definida)</span><span class="sxs-lookup"><span data-stu-id="b4ac4-222">Issue ImmutableID for computer when one for users exist (e.g. alternate login ID is set)</span></span>

<span data-ttu-id="b4ac4-223">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`** - Essa declaração deve conter um valor válido para computadores.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-223">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`** - This claim must contain a valid value for computers.</span></span> <span data-ttu-id="b4ac4-224">No AD FS, você pode criar uma regra de transformação de emissão da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="b4ac4-224">In AD FS, you can create an issuance transform rule as follows:</span></span>

    @RuleName = "Issue ImmutableID for computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ] 
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );

### <a name="helper-script-to-create-the-ad-fs-issuance-transform-rules"></a><span data-ttu-id="b4ac4-225">Script auxiliar para criar regras de transformação de emissão do AD FS</span><span class="sxs-lookup"><span data-stu-id="b4ac4-225">Helper script to create the AD FS issuance transform rules</span></span>

<span data-ttu-id="b4ac4-226">O script a seguir o ajudará com a criação das regras de transformação de emissão descritas acima.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-226">The following script helps you with the creation of the issuance transform rules described above.</span></span>

    $multipleVerifiedDomainNames = $false
    $immutableIDAlreadyIssuedforUsers = $false
    $oneOfVerifiedDomainNames = 'example.com'   # Replace example.com with one of your verified domains
    
    $rule1 = '@RuleName = "Issue account type for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "DJ"
    );'

    $rule2 = '@RuleName = "Issue object GUID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/identity/claims/onpremobjectguid"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );'

    $rule3 = '@RuleName = "Issue objectSID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(claim = c2);'

    $rule4 = ''
    if ($multipleVerifiedDomainNames -eq $true) {
    $rule4 = '@RuleName = "Issue account type with the value User when it is not a computer"
    NOT EXISTS(
    [
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "DJ"
    ]
    )
    => add(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "User"
    );
    
    @RuleName = "Capture UPN when AccountType is User and issue the IssuerID"
    c1:[
        Type == "http://schemas.xmlsoap.org/claims/UPN"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "User"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = regexreplace(
        c1.Value, 
        ".+@(?<domain>.+)", 
        "http://${domain}/adfs/services/trust/"
        )
    );
    
    @RuleName = "Issue issuerID for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = "http://' + $oneOfVerifiedDomainNames + '/adfs/services/trust/"
    );'
    }

    $rule5 = ''
    if ($immutableIDAlreadyIssuedforUsers -eq $true) {
    $rule5 = '@RuleName = "Issue ImmutableID for computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ] 
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );'
    }

    $existingRules = (Get-ADFSRelyingPartyTrust -Identifier urn:federation:MicrosoftOnline).IssuanceTransformRules 

    $updatedRules = $existingRules + $rule1 + $rule2 + $rule3 + $rule4 + $rule5

    $crSet = New-ADFSClaimRuleSet -ClaimRule $updatedRules 

    Set-AdfsRelyingPartyTrust -TargetIdentifier urn:federation:MicrosoftOnline -IssuanceTransformRules $crSet.ClaimRulesString 

### <a name="remarks"></a><span data-ttu-id="b4ac4-227">Comentários</span><span class="sxs-lookup"><span data-stu-id="b4ac4-227">Remarks</span></span> 

- <span data-ttu-id="b4ac4-228">Esse script acrescenta as regras às regras existentes.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-228">This script appends the rules to the existing rules.</span></span> <span data-ttu-id="b4ac4-229">Não execute o script duas vezes porque o conjunto de regras seria adicionado duas vezes.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-229">Do not run the script twice because the set of rules would be added twice.</span></span> <span data-ttu-id="b4ac4-230">Certifique-se de que não exista nenhuma regra correspondente para essas declarações (sob as condições correspondentes) antes de executar o script novamente.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-230">Make sure that no corresponding rules exist for these claims (under the corresponding conditions) before running the script again.</span></span>

- <span data-ttu-id="b4ac4-231">Se você tiver vários nomes de domínio verificados (conforme mostrado no portal do Azure AD ou por meio do cmdlet Get-MsolDomains), defina o valor de **$multipleVerifiedDomainNames** no script para **$true**.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-231">If you have multiple verified domain names (as shown in the Azure AD portal or via the Get-MsolDomains cmdlet), set the value of **$multipleVerifiedDomainNames** in the script to **$true**.</span></span> <span data-ttu-id="b4ac4-232">Além disso, certifique-se de remover qualquer declaração de issuerid existente que possa ter sido criada pelo Azure AD Connect ou por outros meios.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-232">Also make sure that you remove any existing issuerid claim that might have been created by Azure AD Connect or via other means.</span></span> <span data-ttu-id="b4ac4-233">Aqui está um exemplo dessa regra:</span><span class="sxs-lookup"><span data-stu-id="b4ac4-233">Here is an example for this rule:</span></span>


        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"]
        => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)",  "http://${domain}/adfs/services/trust/")); 

- <span data-ttu-id="b4ac4-234">Se você já tiver emitido uma declaração **ImmutableID** para contas de usuário, defina o valor de **$immutableIDAlreadyIssuedforUsers** no script para **$true**.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-234">If you have already issued an **ImmutableID** claim  for user accounts, set the value of **$immutableIDAlreadyIssuedforUsers** in the script to **$true**.</span></span>

## <a name="step-3-enable-windows-down-level-devices"></a><span data-ttu-id="b4ac4-235">Etapa 3: habilitar dispositivos de nível inferior do Windows</span><span class="sxs-lookup"><span data-stu-id="b4ac4-235">Step 3: Enable Windows down-level devices</span></span>

<span data-ttu-id="b4ac4-236">Se alguns dos seus dispositivos associados ao domínio forem dispositivos de nível inferior do Windows, você precisa:</span><span class="sxs-lookup"><span data-stu-id="b4ac4-236">If some of your domain-joined devices Windows down-level devices, you need to:</span></span>

- <span data-ttu-id="b4ac4-237">Definir uma política no Azure AD para permitir que os usuários registrem dispositivos.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-237">Set a policy in Azure AD to enable users to register devices.</span></span>
 
- <span data-ttu-id="b4ac4-238">Configurar o serviço de federação local para emitir declarações para dar suporte à **autenticação integrada do Windows (IWA)** para o registro de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-238">Configure your on-premises federation service to issue claims to support **Integrated Windows Authentication (IWA)** for device registration.</span></span>
 
- <span data-ttu-id="b4ac4-239">Adicionar o ponto de extremidade de autenticação de dispositivo do Azure AD às zonas da Intranet local para evitar prompts de certificação ao autenticar o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-239">Add the Azure AD device authentication end-point to the local Intranet zones to avoid certificate prompts when authenticating the device.</span></span>

### <a name="set-policy-in-azure-ad-to-enable-users-to-register-devices"></a><span data-ttu-id="b4ac4-240">Definir uma política no Azure AD para permitir que os usuários registrem dispositivos</span><span class="sxs-lookup"><span data-stu-id="b4ac4-240">Set policy in Azure AD to enable users to register devices</span></span>

<span data-ttu-id="b4ac4-241">Para registrar dispositivos de nível inferior do Windows, você precisa garantir que a configuração para permitir que os usuários registrem dispositivos no Azure AD esteja definida.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-241">To register Windows down-level devices, you need to make sure that the setting to allow users to register devices in Azure AD is set.</span></span> <span data-ttu-id="b4ac4-242">Você pode encontrar essa configuração no Portal do Azure em:</span><span class="sxs-lookup"><span data-stu-id="b4ac4-242">In the Azure portal, you can find this setting under:</span></span>

`Azure Active Directory > Users and groups > Device settings`
    
<span data-ttu-id="b4ac4-243">A política a seguir deve ser definida como **Todos** : **os usuários podem registrar seus dispositivos com o Azure AD**</span><span class="sxs-lookup"><span data-stu-id="b4ac4-243">The following policy must be set to **All**: **Users may register their devices with Azure AD**</span></span>

![Registrar dispositivos](./media/active-directory-conditional-access-automatic-device-registration-setup/23.png)


### <a name="configure-on-premises-federation-service"></a><span data-ttu-id="b4ac4-245">Configurar o serviço de federação local</span><span class="sxs-lookup"><span data-stu-id="b4ac4-245">Configure on-premises federation service</span></span> 

<span data-ttu-id="b4ac4-246">O serviço de federação local deve oferecer suporte ao emitir as declarações **authenticationmehod** e **wiaormultiauthn** ao receber uma solicitação de autenticação para a terceira parte confiável do Azure AD com um parâmetro resouce_params com um valor codificado como mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="b4ac4-246">Your on-premises federation service must support issuing the **authenticationmehod** and **wiaormultiauthn** claims when receiving an authentication request to the Azure AD relying party holding a resouce_params parameter with an encoded value as shown below:</span></span>

    eyJQcm9wZXJ0aWVzIjpbeyJLZXkiOiJhY3IiLCJWYWx1ZSI6IndpYW9ybXVsdGlhdXRobiJ9XX0

    which decoded is {"Properties":[{"Key":"acr","Value":"wiaormultiauthn"}]}

<span data-ttu-id="b4ac4-247">Quando essa solicitação chega, o serviço de federação local deve autenticar o usuário usando a Autenticação Integrada do Windows e, se ela for bem-sucedida, ele deverá emitir as duas declarações a seguir:</span><span class="sxs-lookup"><span data-stu-id="b4ac4-247">When such a request comes, the on-premises federation service must authenticate the user using Integrated Windows Authentication and upon success, it must issue the following two claims:</span></span>

    http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows
    http://schemas.microsoft.com/claims/wiaormultiauthn

<span data-ttu-id="b4ac4-248">No AD FS, você precisa adicionar uma regra de transformação de emissão que passe pelo método de autenticação.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-248">In AD FS, you must add an issuance transform rule that passes-through the authentication method.</span></span>  

<span data-ttu-id="b4ac4-249">**Para adicionar essa regra:**</span><span class="sxs-lookup"><span data-stu-id="b4ac4-249">**To add this rule:**</span></span>

1. <span data-ttu-id="b4ac4-250">No console de gerenciamento do AD FS, vá para `AD FS > Trust Relationships > Relying Party Trusts`.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-250">In the AD FS management console, go to `AD FS > Trust Relationships > Relying Party Trusts`.</span></span>
2. <span data-ttu-id="b4ac4-251">Clique com o botão direito do mouse no objeto de confiança de terceira parte confiável da Plataforma de Identidade do Microsoft Office 365 e selecione **Editar Regras de Declaração**.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-251">Right-click the Microsoft Office 365 Identity Platform relying party trust object, and then select **Edit Claim Rules**.</span></span>
3. <span data-ttu-id="b4ac4-252">Na guia **Regras de Transformação de Emissão**, selecione **Adicionar Regra**.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-252">On the **Issuance Transform Rules** tab, select **Add Rule**.</span></span>
4. <span data-ttu-id="b4ac4-253">Na lista de modelos **Regra de declaração**, selecione **Enviar Declarações Usando uma Regra Personalizada**.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-253">In the **Claim rule** template list, select **Send Claims Using a Custom Rule**.</span></span>
5. <span data-ttu-id="b4ac4-254">Selecione **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-254">Select **Next**.</span></span>
6. <span data-ttu-id="b4ac4-255">Na caixa **Nome da regra de declaração**, digite **Regra de Declaração de Método de Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-255">In the **Claim rule name** box, type **Auth Method Claim Rule**.</span></span>
7. <span data-ttu-id="b4ac4-256">Na caixa **Regra de declaração** , digite a seguinte regra:</span><span class="sxs-lookup"><span data-stu-id="b4ac4-256">In the **Claim rule** box, type the following rule:</span></span>

    `c:[Type == "http://schemas.microsoft.com/claims/authnmethodsreferences"] => issue(claim = c);`

8. <span data-ttu-id="b4ac4-257">No servidor de federação, digite o comando do PowerShell abaixo após substituir  **\<RPObjectName\>**  pelo nome do objeto da terceira parte confiável para o seu objeto de terceira parte confiável do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-257">On your federation server, type the PowerShell command below after replacing **\<RPObjectName\>** with the relying party object name for your Azure AD relying party trust object.</span></span> <span data-ttu-id="b4ac4-258">Geralmente, este objeto é nomeado como **Plataforma de Identidade do Microsoft Office 365**.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-258">This object usually is named **Microsoft Office 365 Identity Platform**.</span></span>
   
    `Set-AdfsRelyingPartyTrust -TargetName <RPObjectName> -AllowedAuthenticationClassReferences wiaormultiauthn`

### <a name="add-the-azure-ad-device-authentication-end-point-to-the-local-intranet-zones"></a><span data-ttu-id="b4ac4-259">Adicione o ponto de extremidade de autenticação de dispositivo do Azure AD para Zonas da Intranet Local</span><span class="sxs-lookup"><span data-stu-id="b4ac4-259">Add the Azure AD device authentication end-point to the Local Intranet zones</span></span>

<span data-ttu-id="b4ac4-260">Para evitar prompts de certificado quando os usuários dos dispositivos de registro fizerem a autenticação no Azure AD, você poderá enviar uma política para os seus dispositivos associados ao domínio para adicionar a seguinte URL na zona da Intranet Local no Internet Explorer:</span><span class="sxs-lookup"><span data-stu-id="b4ac4-260">To avoid certificate prompts when users in register devices authenticate to Azure AD you can push a policy to your domain-joined devices to add the following URL to the Local Intranet zone in Internet Explorer:</span></span>

`https://device.login.microsoftonline.com`

## <a name="step-4-control-deployment-and-rollout"></a><span data-ttu-id="b4ac4-261">Etapa 4: implantação de controle e distribuição</span><span class="sxs-lookup"><span data-stu-id="b4ac4-261">Step 4: Control deployment and rollout</span></span>

<span data-ttu-id="b4ac4-262">Quando você tiver concluído as etapas necessárias, os dispositivos associados ao domínio estarão prontos para se registrar automaticamente com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-262">When you have completed the required steps, domain-joined devices are ready to automatically register with Azure AD.</span></span> <span data-ttu-id="b4ac4-263">Todos os dispositivos associados ao domínio que executarem a Atualização de Aniversário do Windows 10 e o Windows Server 2016 serão registrados automaticamente no Azure AD na reinicialização do dispositivo ou no login.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-263">All domain-joined devices running Windows 10 Anniversary Update and Windows Server 2016 automatically register with Azure AD at device restart or user sign-in.</span></span> <span data-ttu-id="b4ac4-264">Novos dispositivos serão registrados com o Azure AD quando o dispositivo reiniciar depois que a operação de ingresso no domínio for concluída.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-264">New devices register with Azure AD when the device restarts after the domain join operation is completed.</span></span>

<span data-ttu-id="b4ac4-265">Os dispositivos que foram anteriormente ingressados no local de trabalho na transição do Azure AD (por exemplo, no Intune) para "*Ingressado no Domínio, Registrado no AAD*". No entanto, levará algum tempo para que esse processo seja concluído em todos os dispositivos devido ao fluxo normal de atividade do usuário e do domínio.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-265">Devices that were previously workplace-joined to Azure AD (for example for Intune) transition to “*Domain Joined, AAD Registered*”; however it takes some time for this process to complete across all devices due to the normal flow of domain and user activity.</span></span>

### <a name="remarks"></a><span data-ttu-id="b4ac4-266">Comentários</span><span class="sxs-lookup"><span data-stu-id="b4ac4-266">Remarks</span></span>

- <span data-ttu-id="b4ac4-267">Você pode usar um objeto de Política de Grupo para controlar a distribuição de registro automático de computadores associados ao domínio do Windows 10 e do Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-267">You can use a Group Policy object to control the rollout of automatic registration of Windows 10 and Windows Server 2016 domain-joined computers.</span></span>

- <span data-ttu-id="b4ac4-268">A Atualização de 10 de novembro de 2015 do Windows será registrada automaticamente com o Azure AD **apenas** se o objeto da Política de Grupo de distribuição for definido.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-268">Windows 10 November 2015 Update automatically registers with Azure AD **only** if the rollout Group Policy object is set.</span></span>

- <span data-ttu-id="b4ac4-269">Para distribuir o registro automático dos computadores de nível inferior do Windows, você pode implantar um [pacote do Windows Installer](#windows-installer-packages-for-non-windows-10-computers) nos computadores que selecionar.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-269">To rollout the automatic registration of Windows down-level computers, you can deploy a [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) to computers that you select.</span></span>

- <span data-ttu-id="b4ac4-270">Se você enviar o objeto de Política de Grupo para dispositivos associados ao domínio do Windows 8.1, será feita uma tentativa de registro. No entanto, é recomendável que você use o [pacote do Windows Installer](#windows-installer-packages-for-non-windows-10-computers) para registrar todos os seus dispositivos de nível inferior do Windows.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-270">If you push the Group Policy object to Windows 8.1 domain-joined devices, registration will be attempted; however it is recommended that you use the [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) to register all your Windows down-level devices.</span></span> 

### <a name="create-a-group-policy-object"></a><span data-ttu-id="b4ac4-271">Criar um objeto de Política de Grupo</span><span class="sxs-lookup"><span data-stu-id="b4ac4-271">Create a Group Policy object</span></span> 

<span data-ttu-id="b4ac4-272">Para controlar a distribuição do registro automático de computadores atuais do Windows, você pode implantar a Política de Grupo **Registrar computadores associados ao domínio como dispositivos** nos computadores que deseja registrar.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-272">To control the rollout of automatic registration of Windows current computers, you should deploy the **Register domain-joined computers as devices** Group Policy object to the devices you want to register.</span></span> <span data-ttu-id="b4ac4-273">Por exemplo, você pode implantar a política em uma unidade organizacional ou um grupo de segurança.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-273">For example, you can deploy the policy to an organizational unit or to a security group.</span></span>

<span data-ttu-id="b4ac4-274">**Para definir a política:**</span><span class="sxs-lookup"><span data-stu-id="b4ac4-274">**To set the policy:**</span></span>

1. <span data-ttu-id="b4ac4-275">Abra o **Gerenciador do Servidor** e depois vá para `Tools > Group Policy Management`.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-275">Open **Server Manager**, and then go to `Tools > Group Policy Management`.</span></span>
2. <span data-ttu-id="b4ac4-276">Vá para o nó de domínio que corresponde ao domínio em que você deseja ativar o registro automático de computadores atuais do Windows.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-276">Go to the domain node that corresponds to the domain where you want to activate auto-registration of Windows current computers.</span></span>
3. <span data-ttu-id="b4ac4-277">Clique com o botão direito do mouse em **Objetos de Política de Grupo** e selecione **Novo**.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-277">Right-click **Group Policy Objects**, and then select **New**.</span></span>
4. <span data-ttu-id="b4ac4-278">Insira um nome para o objeto de Política de Grupo.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-278">Type a name for your Group Policy object.</span></span> <span data-ttu-id="b4ac4-279">Por exemplo, *Registro Automático no Azure AD*.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-279">For example, *Automatic Registration to Azure AD*.</span></span> <span data-ttu-id="b4ac4-280">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-280">Select **OK**.</span></span>
5. <span data-ttu-id="b4ac4-281">Clique com o botão direito do mouse em seu novo objeto de Política de Grupo e selecione **Editar**.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-281">Right-click your new Group Policy object, and then select **Edit**.</span></span>
6. <span data-ttu-id="b4ac4-282">Vá para **Configuração do Computador** > **Políticas** > **Modelos Administrativos** > **Componentes do Windows** > **Registro de Dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-282">Go to **Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Device Registration**.</span></span> <span data-ttu-id="b4ac4-283">Clique com o botão direito do mouse em **Registrar computadores associados ao domínio como dispositivos** e selecione **Editar**.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-283">Right-click **Register domain-joined computers as devices**, and then select **Edit**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b4ac4-284">Esse modelo de Política de Grupo foi renomeado de versões anteriores do console de Gerenciamento de Política de Grupo.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-284">This Group Policy template has been renamed from earlier versions of the Group Policy Management console.</span></span> <span data-ttu-id="b4ac4-285">Se você estiver usando uma versão anterior do console, vá para `Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-285">If you are using an earlier version of the console, go to `Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span></span> 

7. <span data-ttu-id="b4ac4-286">Selecione **Habilitado** e selecione **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-286">Select **Enabled**, and then select **Apply**.</span></span>
8. <span data-ttu-id="b4ac4-287">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-287">Select **OK**.</span></span>
9. <span data-ttu-id="b4ac4-288">Vincule o objeto da Política de Grupo a um local de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-288">Link the Group Policy object to a location of your choice.</span></span> <span data-ttu-id="b4ac4-289">Por exemplo, você pode vinculá-lo a uma unidade organizacional específica.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-289">For example, you can link it to a specific organizational unit.</span></span> <span data-ttu-id="b4ac4-290">Você também pode vinculá-lo a um grupo específico de computadores que se registram automaticamente no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-290">You also could link it to a specific security group of computers that automatically register with Azure AD.</span></span> <span data-ttu-id="b4ac4-291">Para definir essa política para todos os computadores com Windows 10 e Windows Server 2016 ingressados no domínio em sua organização, vincule o objeto de Política de Grupo ao domínio.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-291">To set this policy for all domain-joined Windows 10 and Windows Server 2016 computers in your organization, link the Group Policy object to the domain.</span></span>

### <a name="windows-installer-packages-for-non-windows-10-computers"></a><span data-ttu-id="b4ac4-292">Pacotes do Windows Installer para computadores que não são do Windows 10</span><span class="sxs-lookup"><span data-stu-id="b4ac4-292">Windows Installer packages for non-Windows 10 computers</span></span>

<span data-ttu-id="b4ac4-293">Para registrar computadores de nível inferior do Windows associados ao domínio em um ambiente federado, você pode baixar e instalar esses pacotes do Windows Installer (.msi) do Centro de Downloads na página [Microsoft Workplace Join para computadores não-Windows 10](https://www.microsoft.com/en-us/download/details.aspx?id=53554) .</span><span class="sxs-lookup"><span data-stu-id="b4ac4-293">To register domain-joined Windows down-level computers in a federated environment, you can download and install these Windows Installer package (.msi) from Download Center at the [Microsoft Workplace Join for non-Windows 10 computers](https://www.microsoft.com/en-us/download/details.aspx?id=53554) page.</span></span>

<span data-ttu-id="b4ac4-294">Você pode implantar o pacote usando um sistema de distribuição de software como o System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-294">You can deploy the package by using a software distribution system like System Center Configuration Manager.</span></span> <span data-ttu-id="b4ac4-295">O pacote dá suporte às opções de instalação silenciosa padrão com o parâmetro *quiet*.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-295">The package supports the standard silent install options with the *quiet* parameter.</span></span> <span data-ttu-id="b4ac4-296">O System Center Configuration Manager Current Branch oferece benefícios adicionais em relação às versões anteriores, como a capacidade de monitorar registros concluídos.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-296">System Center Configuration Manager Current Branch offers additional benefits from earlier versions, like the ability to track completed registrations.</span></span> <span data-ttu-id="b4ac4-297">Para obter mais informações, consulte [System Center 2016](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span><span class="sxs-lookup"><span data-stu-id="b4ac4-297">For more information, see [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span></span>

<span data-ttu-id="b4ac4-298">O instalador cria uma tarefa agendada no sistema que é executada no contexto do usuário.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-298">The installer creates a scheduled task on the system that runs in the user’s context.</span></span> <span data-ttu-id="b4ac4-299">A tarefa é disparada quando o usuário entra no Windows.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-299">The task is triggered when the user signs in to Windows.</span></span> <span data-ttu-id="b4ac4-300">A tarefa registra silenciosamente o dispositivo no Azure AD com as credenciais do usuário após a autenticação usando a Autenticação Integrada do Windows.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-300">The task silently registers the device with Azure AD with the user credentials after authenticating using Integrated Windows Authentication.</span></span> <span data-ttu-id="b4ac4-301">Para ver a tarefa agendada, no dispositivo, vá para o **Microsoft** > **Workplace Join** e depois para a biblioteca do Agendador de Tarefas.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-301">To see the scheduled task, in the device, go to **Microsoft** > **Workplace Join**, and then go to the Task Scheduler library.</span></span>

## <a name="step-5-verify-registered-devices"></a><span data-ttu-id="b4ac4-302">Etapa 5: verificar os dispositivos registrados</span><span class="sxs-lookup"><span data-stu-id="b4ac4-302">Step 5: Verify registered devices</span></span>

<span data-ttu-id="b4ac4-303">Você pode obter uma lista dos dispositivos registrados com sucesso na sua organização usando o cmdlet [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) no [módulo do Azure Active Directory PowerShell](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="b4ac4-303">You can check successful registered devices in your organization by using the [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in the [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span>

<span data-ttu-id="b4ac4-304">A saída deste cmdlet mostra os dispositivos registrados no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-304">The output of this cmdlet shows devices registered in Azure AD.</span></span> <span data-ttu-id="b4ac4-305">Para obter todos os dispositivos, use o parâmetro **-Todos** e, em seguida, filtre-os usando a propriedade **deviceTrustType**.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-305">To get all devices, use the **-All** parameter, and then filter them using the **deviceTrustType** property.</span></span> <span data-ttu-id="b4ac4-306">Dispositivos associados ao domínio possuem um valor de **Associado ao domínio**.</span><span class="sxs-lookup"><span data-stu-id="b4ac4-306">Domain joined devices have a value of **Domain Joined**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4ac4-307">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b4ac4-307">Next steps</span></span>

* [<span data-ttu-id="b4ac4-308">Perguntas frequentes sobre o registro de dispositivo automático</span><span class="sxs-lookup"><span data-stu-id="b4ac4-308">Automatic device registration FAQ</span></span>](active-directory-device-registration-faq.md)
* [<span data-ttu-id="b4ac4-309">Solução de problemas de registro automático de computadores ingressados no domínio do Azure AD – Windows 10 e Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="b4ac4-309">Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016</span></span>](active-directory-device-registration-troubleshoot-windows.md)
* [<span data-ttu-id="b4ac4-310">Solução de problemas de registro automático de computadores associados ao domínio do Azure AD – não Windows 10</span><span class="sxs-lookup"><span data-stu-id="b4ac4-310">Troubleshooting auto-registration of domain joined computers to Azure AD – non-Windows 10</span></span>](active-directory-device-registration-troubleshoot-windows-legacy.md)
* [<span data-ttu-id="b4ac4-311">Acesso condicional ao Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b4ac4-311">Azure Active Directory conditional access</span></span>](active-directory-conditional-access-azure-portal.md)



<!--Image references-->
[1]: ./media/active-directory-conditional-access-automatic-device-registration-setup/12.png
