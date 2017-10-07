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
ms.date: 06/16/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 6a1aab753f5456ed06ba7979ab05f70f29b4ddee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-automatic-registration-of-windows-domain-joined-devices-with-azure-active-directory"></a><span data-ttu-id="75afd-103">Como o registro automático do Windows tooconfigure domínio dispositivos com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="75afd-103">How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory</span></span>

<span data-ttu-id="75afd-104">toouse [acesso condicional com base no dispositivo do Active Directory do Azure](active-directory-conditional-access-azure-portal.md), os computadores devem ser registrados com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="75afd-104">toouse [Azure Active Directory device-based conditional access](active-directory-conditional-access-azure-portal.md), your computers must be registered with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="75afd-105">Você pode obter uma lista de dispositivos registrados em sua organização usando Olá [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet Olá [módulo do Azure Active Directory PowerShell](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="75afd-105">You can get a list of registered devices in your organization by using hello [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in hello [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span> 

<span data-ttu-id="75afd-106">Este artigo fornece as etapas de saudação para configurar o registro automático de dispositivos de domínio do Windows hello com o Azure AD em sua organização.</span><span class="sxs-lookup"><span data-stu-id="75afd-106">This article provides you with hello steps for configuring hello automatic registration of Windows domain-joined devices with Azure AD in your organization.</span></span>


<span data-ttu-id="75afd-107">Para saber mais sobre:</span><span class="sxs-lookup"><span data-stu-id="75afd-107">For more information about:</span></span>

- <span data-ttu-id="75afd-108">Acesso condicional, confira [Acesso condicional com base no dispositivo ao Azure Active Directory](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="75afd-108">Conditional access, see [Azure Active Directory device-based conditional access](active-directory-conditional-access-azure-portal.md).</span></span> 
- <span data-ttu-id="75afd-109">Dispositivos Windows 10 no local de trabalho hello e experiências Olá aprimorada quando registrado com o AD do Azure, consulte [Windows 10 para a empresa Olá: usar dispositivos para o trabalho](active-directory-azureadjoin-windows10-devices-overview.md).</span><span class="sxs-lookup"><span data-stu-id="75afd-109">Windows 10 devices in hello workplace and hello enhanced experiences when registered with Azure AD, see [Windows 10 for hello enterprise: Use devices for work](active-directory-azureadjoin-windows10-devices-overview.md).</span></span>
- <span data-ttu-id="75afd-110">Windows 10 Enterprise E3 em CSP, consulte Olá [Windows 10 Enterprise E3 na visão geral do CSP](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview).</span><span class="sxs-lookup"><span data-stu-id="75afd-110">Windows 10 Enterprise E3 in CSP, see hello [Windows 10 Enterprise E3 in CSP Overview](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="75afd-111">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="75afd-111">Before you begin</span></span>

<span data-ttu-id="75afd-112">Antes de começar a configurar o registro automático de dispositivos de domínio do Windows hello em seu ambiente, você deve se familiarizar com cenários de saudação com suporte e as restrições de saudação.</span><span class="sxs-lookup"><span data-stu-id="75afd-112">Before you start configuring hello automatic registration of Windows domain-joined devices in your environment, you should familiarize yourself with hello supported scenarios and hello constraints.</span></span>  

<span data-ttu-id="75afd-113">tooimprove legibilidade de saudação de descrições de hello, este tópico usa Olá termos a seguir:</span><span class="sxs-lookup"><span data-stu-id="75afd-113">tooimprove hello readability of hello descriptions, this topic uses hello following term:</span></span> 

- <span data-ttu-id="75afd-114">**Dispositivos do Windows atuais** -este termo se refere a dispositivos que ingressaram no toodomain executando o Windows 10 ou Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="75afd-114">**Windows current devices** - This term refers toodomain-joined devices running Windows 10 or Windows Server 2016.</span></span>
- <span data-ttu-id="75afd-115">**Dispositivos de baixo nível do Windows** -este termo se refere a tooall **suporte** dispositivos Windows ingressados no domínio que estão executando o Windows 10 nem Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="75afd-115">**Windows down-level devices** - This term refers tooall **supported** domain-joined Windows devices that are neither running Windows 10 nor Windows Server 2016.</span></span>  


### <a name="windows-current-devices"></a><span data-ttu-id="75afd-116">Dispositivos atuais do Windows</span><span class="sxs-lookup"><span data-stu-id="75afd-116">Windows current devices</span></span>

- <span data-ttu-id="75afd-117">Para dispositivos que executam o sistema de operacional de desktop do Windows hello, é recomendável usar a atualização de aniversário do Windows 10 (versão 1607) ou posterior.</span><span class="sxs-lookup"><span data-stu-id="75afd-117">For devices running hello Windows desktop operating system, we recommend using Windows 10 Anniversary Update (version 1607) or later.</span></span> 
- <span data-ttu-id="75afd-118">Olá registro atuais de dispositivos do Windows **é** suporte em ambientes de não-federado, como configurações de sincronização de hash de senha.</span><span class="sxs-lookup"><span data-stu-id="75afd-118">hello registration of Windows current devices **is** supported in non-federated environments such as password hash sync configurations.</span></span>  


### <a name="windows-down-level-devices"></a><span data-ttu-id="75afd-119">Dispositivos de nível inferior do Windows</span><span class="sxs-lookup"><span data-stu-id="75afd-119">Windows down-level devices</span></span>

- <span data-ttu-id="75afd-120">Olá dispositivos de baixo nível do Windows a seguir têm suporte:</span><span class="sxs-lookup"><span data-stu-id="75afd-120">hello following Windows down-level devices are supported:</span></span>
    - <span data-ttu-id="75afd-121">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="75afd-121">Windows 8.1</span></span>
    - <span data-ttu-id="75afd-122">Windows 7</span><span class="sxs-lookup"><span data-stu-id="75afd-122">Windows 7</span></span>
    - <span data-ttu-id="75afd-123">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="75afd-123">Windows Server 2012 R2</span></span>
    - <span data-ttu-id="75afd-124">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="75afd-124">Windows Server 2012</span></span>
    - <span data-ttu-id="75afd-125">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="75afd-125">Windows Server 2008 R2</span></span>
- <span data-ttu-id="75afd-126">Olá registro de dispositivos de baixo nível do Windows **é** suporte em ambientes de não-federado por meio de perfeita Single Sign On [do Azure Active Directory perfeita Single Sign-On](https://aka.ms/hybrid/sso).</span><span class="sxs-lookup"><span data-stu-id="75afd-126">hello registration of Windows down-level devices **is** supported in non-federated environments through Seamless Single Sign On [Azure Active Directory Seamless Single Sign-On](https://aka.ms/hybrid/sso).</span></span>
- <span data-ttu-id="75afd-127">Olá registro de dispositivos de baixo nível do Windows **não é** com suporte para dispositivos usando perfis de roaming.</span><span class="sxs-lookup"><span data-stu-id="75afd-127">hello registration of Windows down-level devices **is not** supported for devices using roaming profiles.</span></span> <span data-ttu-id="75afd-128">Se você depender da mobilidade de perfis ou configurações, use o Windows 10.</span><span class="sxs-lookup"><span data-stu-id="75afd-128">If you are relying on roaming of profiles or settings, use Windows 10.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="75afd-129">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="75afd-129">Prerequisites</span></span>

<span data-ttu-id="75afd-130">Antes de iniciar a habilitação Olá o registro automático de dispositivos que ingressaram no domínio em sua organização, você precisa toomake-se de que você está executando uma versão atualizada do AD do Azure se conectar.</span><span class="sxs-lookup"><span data-stu-id="75afd-130">Before you start enabling hello auto-registration of domain-joined devices in your organization, you need toomake sure that you are running an up-to-date version of Azure AD connect.</span></span>

<span data-ttu-id="75afd-131">Azure AD Connect:</span><span class="sxs-lookup"><span data-stu-id="75afd-131">Azure AD Connect:</span></span>

- <span data-ttu-id="75afd-132">Mantém a associação de saudação entre a conta de computador de saudação de seu local no Active Directory (AD) e o objeto de dispositivo de saudação no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="75afd-132">Keeps hello association between hello computer account in your on-premises Active Directory (AD) and hello device object in Azure AD.</span></span> 
- <span data-ttu-id="75afd-133">Permite outros recursos relacionados ao dispositivo, como o Windows Hello for Business.</span><span class="sxs-lookup"><span data-stu-id="75afd-133">Enables other device related features like Windows Hello for Business.</span></span>



## <a name="configuration-steps"></a><span data-ttu-id="75afd-134">Etapas da configuração</span><span class="sxs-lookup"><span data-stu-id="75afd-134">Configuration steps</span></span>

<span data-ttu-id="75afd-135">Este tópico inclui etapas Olá necessária para todos os cenários de configuração típica.</span><span class="sxs-lookup"><span data-stu-id="75afd-135">This topic includes hello required steps for all typical configuration scenarios.</span></span>  
<span data-ttu-id="75afd-136">Use Olá tabela tooget uma visão geral das etapas de saudação que são necessários para o cenário a seguir:</span><span class="sxs-lookup"><span data-stu-id="75afd-136">Use hello following table tooget an overview of hello steps that are required for your scenario:</span></span>  



| <span data-ttu-id="75afd-137">Etapas</span><span class="sxs-lookup"><span data-stu-id="75afd-137">Steps</span></span>                                      | <span data-ttu-id="75afd-138">Sincronização de hash de senha e do Windows atual</span><span class="sxs-lookup"><span data-stu-id="75afd-138">Windows current and password hash sync</span></span> | <span data-ttu-id="75afd-139">Windows atual e a federação</span><span class="sxs-lookup"><span data-stu-id="75afd-139">Windows current and federation</span></span> | <span data-ttu-id="75afd-140">Nível inferior do Windows</span><span class="sxs-lookup"><span data-stu-id="75afd-140">Windows down-level</span></span> |
| :--                                        | :-:                                    | :-:                            | :-:                |
| <span data-ttu-id="75afd-141">Etapa 1: configurar o ponto de conexão de serviço</span><span class="sxs-lookup"><span data-stu-id="75afd-141">Step 1: Configure service connection point</span></span> | ![Verificação][1]                            | ![Verificação][1]                    | ![Verificação][1]        |
| <span data-ttu-id="75afd-145">Etapa 2: configurar a emissão de declarações</span><span class="sxs-lookup"><span data-stu-id="75afd-145">Step 2: Setup issuance of claims</span></span>           |                                        | ![Verificação][1]                    | ![Verificação][1]        |
| <span data-ttu-id="75afd-148">Etapa 3: habilitar dispositivos não Windows 10</span><span class="sxs-lookup"><span data-stu-id="75afd-148">Step 3: Enable non-Windows 10 devices</span></span>      |                                        |                                | ![Verificação][1]        |
| <span data-ttu-id="75afd-150">Etapa 4: implantação de controle e distribuição</span><span class="sxs-lookup"><span data-stu-id="75afd-150">Step 4: Control deployment and rollout</span></span>     | ![Verificação][1]                            | ![Verificação][1]                    | ![Verificação][1]        |
| <span data-ttu-id="75afd-154">Etapa 5: verificar os dispositivos registrados</span><span class="sxs-lookup"><span data-stu-id="75afd-154">Step 5: Verify registered devices</span></span>          | ![Verificação][1]                            | ![Verificação][1]                    | ![Verificação][1]        |



## <a name="step-1-configure-service-connection-point"></a><span data-ttu-id="75afd-158">Etapa 1: configurar o ponto de conexão de serviço</span><span class="sxs-lookup"><span data-stu-id="75afd-158">Step 1: Configure service connection point</span></span>

<span data-ttu-id="75afd-159">objeto de SCP (ponto) de conexão de serviço de saudação é usado por seus dispositivos durante saudação registro toodiscover informações de locatário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="75afd-159">hello service connection point (SCP) object is used by your devices during hello registration toodiscover Azure AD tenant information.</span></span> <span data-ttu-id="75afd-160">Em seu local do Active Directory (AD), o objeto SCP Olá Olá o registro automático de dispositivos que ingressaram no domínio deve existir no hello nomenclatura contexto partição de configuração da floresta do computador hello.</span><span class="sxs-lookup"><span data-stu-id="75afd-160">In your on-premises Active Directory (AD), hello SCP object for hello auto-registration of domain-joined devices must exist in hello configuration naming context partition of hello computer's forest.</span></span> <span data-ttu-id="75afd-161">Há apenas um contexto de nomenclatura de configuração por floresta.</span><span class="sxs-lookup"><span data-stu-id="75afd-161">There is only one configuration naming context per forest.</span></span> <span data-ttu-id="75afd-162">Em uma configuração do Active Directory de várias floresta, o ponto de conexão de serviço Olá deve existir em todas as florestas de computadores que ingressaram no domínio.</span><span class="sxs-lookup"><span data-stu-id="75afd-162">In a multi-forest Active Directory configuration, hello service connection point must exist in all forests containing domain-joined computers.</span></span>

<span data-ttu-id="75afd-163">Você pode usar o hello [ **Get-ADRootDSE** ](https://technet.microsoft.com/library/ee617246.aspx) cmdlet tooretrieve Olá contexto de nomenclatura configuração da floresta.</span><span class="sxs-lookup"><span data-stu-id="75afd-163">You can use hello [**Get-ADRootDSE**](https://technet.microsoft.com/library/ee617246.aspx) cmdlet tooretrieve hello configuration naming context of your forest.</span></span>  

<span data-ttu-id="75afd-164">Para uma floresta com o nome de domínio do Active Directory Olá *fabrikam.com*, Olá contexto de nomenclatura de configuração é:</span><span class="sxs-lookup"><span data-stu-id="75afd-164">For a forest with hello Active Directory domain name *fabrikam.com*, hello configuration naming context is:</span></span>

`CN=Configuration,DC=fabrikam,DC=com`

<span data-ttu-id="75afd-165">Em sua floresta, o objeto Olá SCP para Olá o registro automático de dispositivos que ingressaram no domínio está localizado em:</span><span class="sxs-lookup"><span data-stu-id="75afd-165">In your forest, hello SCP object for hello auto-registration of domain-joined devices is located at:</span></span>  

`CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,[Your Configuration Naming Context]`

<span data-ttu-id="75afd-166">Dependendo de como você implantou o Azure AD Connect, objeto de SCP Olá pode ter já foi configurado.</span><span class="sxs-lookup"><span data-stu-id="75afd-166">Depending on how you have deployed Azure AD Connect, hello SCP object may have already been configured.</span></span>
<span data-ttu-id="75afd-167">Você pode verificar a existência de saudação do objeto hello e recuperar valores de descoberta hello usando Olá script do Windows PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="75afd-167">You can verify hello existence of hello object and retrieve hello discovery values using hello following Windows PowerShell script:</span></span> 

    $scp = New-Object System.DirectoryServices.DirectoryEntry;

    $scp.Path = "LDAP://CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=fabrikam,DC=com";

    $scp.Keywords;

<span data-ttu-id="75afd-168">Olá **$scp. Palavras-chave** saída mostra informações de locatário de saudação do AD do Azure, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="75afd-168">hello **$scp.Keywords** output shows hello Azure AD tenant information, for example:</span></span>

    azureADName:microsoft.com
    azureADId:72f988bf-86f1-41af-91ab-2d7cd011db47

<span data-ttu-id="75afd-169">Se o ponto de conexão de serviço Olá não existir, você pode criá-lo executando Olá `Initialize-ADSyncDomainJoinedComputerSync` cmdlet no seu servidor do Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="75afd-169">If hello service connection point does not exist, you can create it by running hello `Initialize-ADSyncDomainJoinedComputerSync` cmdlet on your Azure AD Connect server.</span></span> <span data-ttu-id="75afd-170">Credenciais de administrador corporativo é necessário toorun esse cmdlet.</span><span class="sxs-lookup"><span data-stu-id="75afd-170">Enterprise admin credential is required toorun this cmdlet.</span></span>  
<span data-ttu-id="75afd-171">Olá cmdlet:</span><span class="sxs-lookup"><span data-stu-id="75afd-171">hello cmdlet:</span></span>

- <span data-ttu-id="75afd-172">Cria o ponto de conexão de serviço Olá na floresta do Active Directory de saudação do Azure AD Connect está conectado ao.</span><span class="sxs-lookup"><span data-stu-id="75afd-172">Creates hello service connection point in hello Active Directory forest Azure AD Connect is connected to.</span></span> 
- <span data-ttu-id="75afd-173">Exige que você Olá toospecify `AdConnectorAccount` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="75afd-173">Requires you toospecify hello `AdConnectorAccount` parameter.</span></span> <span data-ttu-id="75afd-174">Essa é a conta de saudação que é configurada como o Active Directory, conecte-se a conta de conector no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="75afd-174">This is hello account that is configured as Active Directory connector account in Azure AD connect.</span></span> 


<span data-ttu-id="75afd-175">Olá, script a seguir mostra um exemplo para usar o cmdlet hello.</span><span class="sxs-lookup"><span data-stu-id="75afd-175">hello following script shows an example for using hello cmdlet.</span></span> <span data-ttu-id="75afd-176">Nesse script, `$aadAdminCred = Get-Credential` exige que você tootype um nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="75afd-176">In this script, `$aadAdminCred = Get-Credential` requires you tootype a user name.</span></span> <span data-ttu-id="75afd-177">Você precisa de nome de usuário Olá tooprovide no formato de nome principal (UPN) do usuário hello (`user@example.com`).</span><span class="sxs-lookup"><span data-stu-id="75afd-177">You need tooprovide hello user name in hello user principal name (UPN) format (`user@example.com`).</span></span> 


    Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1";

    $aadAdminCred = Get-Credential;

    Initialize-ADSyncDomainJoinedComputerSync –AdConnectorAccount [connector account name] -AzureADCredentials $aadAdminCred;

<span data-ttu-id="75afd-178">Olá `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="75afd-178">hello `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:</span></span>

- <span data-ttu-id="75afd-179">Usa o módulo do Active Directory PowerShell hello, que se baseia em serviços Web do Active Directory em execução em um controlador de domínio.</span><span class="sxs-lookup"><span data-stu-id="75afd-179">Uses hello Active Directory PowerShell module, which relies on Active Directory Web Services running on a domain controller.</span></span> <span data-ttu-id="75afd-180">Os Serviços Web do Active Directory têm suporte em controladores de domínio executando o Windows Server 2008 R2 e posterior.</span><span class="sxs-lookup"><span data-stu-id="75afd-180">Active Directory Web Services is supported on domain controllers running Windows Server 2008 R2 and later.</span></span>
- <span data-ttu-id="75afd-181">Só há suporte para Olá **MSOnline PowerShell versão do módulo 1.1.166.0**.</span><span class="sxs-lookup"><span data-stu-id="75afd-181">Is only supported by hello **MSOnline PowerShell module version 1.1.166.0**.</span></span> <span data-ttu-id="75afd-182">toodownload neste módulo, use [link](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span><span class="sxs-lookup"><span data-stu-id="75afd-182">toodownload this module, use this [link](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span></span>   

<span data-ttu-id="75afd-183">Para controladores de domínio que executam o Windows Server 2008 ou versões anteriores, use script de saudação abaixo de ponto de conexão de serviço toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="75afd-183">For domain controllers running Windows Server 2008 or earlier versions, use hello script below toocreate hello service connection point.</span></span>

<span data-ttu-id="75afd-184">Em uma configuração de várias floresta, você deve usar o hello ponto de conexão de serviço do script toocreate Olá em cada floresta onde existem computadores a seguir:</span><span class="sxs-lookup"><span data-stu-id="75afd-184">In a multi-forest configuration, you should use hello following script toocreate hello service connection point in each forest where computers exist:</span></span>
 
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


## <a name="step-2-setup-issuance-of-claims"></a><span data-ttu-id="75afd-185">Etapa 2: configurar a emissão de declarações</span><span class="sxs-lookup"><span data-stu-id="75afd-185">Step 2: Setup issuance of claims</span></span>

<span data-ttu-id="75afd-186">No Azure federado configuração do AD, dispositivos contam com os serviços de Federação do Active Directory (AD FS) ou uma parte 3 de tooAzure de tooauthenticate de serviço de Federação AD local.</span><span class="sxs-lookup"><span data-stu-id="75afd-186">In a federated Azure AD configuration, devices rely on Active Directory Federation Services (AD FS) or a 3rd party on-premises federation service tooauthenticate tooAzure AD.</span></span> <span data-ttu-id="75afd-187">Dispositivos autenticam tooget um tooregister de token de acesso em relação a saudação do Azure Active Directory Device Registration Service (DRS do Azure).</span><span class="sxs-lookup"><span data-stu-id="75afd-187">Devices authenticate tooget an access token tooregister against hello Azure Active Directory Device Registration Service (Azure DRS).</span></span>

<span data-ttu-id="75afd-188">Windows dispositivos atuais se autenticar usando a autenticação integrada do Windows tooan WS-Trust ponto de extremidade ativo (versões 1.3 ou 2005) hospedado pelo serviço de federação local hello.</span><span class="sxs-lookup"><span data-stu-id="75afd-188">Windows current devices authenticate using Integrated Windows Authentication tooan active WS-Trust endpoint (either 1.3 or 2005 versions) hosted by hello on-premises federation service.</span></span>

> [!NOTE]
> <span data-ttu-id="75afd-189">Ao usar o AD FS, **adfs/services/trust/13/windowstransport** ou **adfs/services/trust/2005/windowstransport** devem ser habilitados.</span><span class="sxs-lookup"><span data-stu-id="75afd-189">When using AD FS, either **adfs/services/trust/13/windowstransport** or **adfs/services/trust/2005/windowstransport** must be enabled.</span></span> <span data-ttu-id="75afd-190">Se você estiver usando Olá Proxy de autenticação da Web, também Certifique-se de que esse ponto de extremidade é publicado por meio do proxy de saudação.</span><span class="sxs-lookup"><span data-stu-id="75afd-190">If you are using hello Web Authentication Proxy, also ensure that this endpoint is published through hello proxy.</span></span> <span data-ttu-id="75afd-191">Você pode ver quais pontos de extremidade são habilitados por meio do console de gerenciamento de saudação do AD FS em **Service > pontos de extremidade**.</span><span class="sxs-lookup"><span data-stu-id="75afd-191">You can see what end-points are enabled through hello AD FS management console under **Service > Endpoints**.</span></span>
>
><span data-ttu-id="75afd-192">Se você não tiver o AD FS como seu serviço de federação local, siga as instruções de saudação do seu toomake fornecedor se que eles dão suporte a WS-Trust 1.3 ou pontos de extremidade de 2005 e que eles são publicados por meio de saudação (MEX) do arquivo de troca de metadados.</span><span class="sxs-lookup"><span data-stu-id="75afd-192">If you don’t have AD FS as your on-premises federation service, follow hello instructions of your vendor toomake sure they support WS-Trust 1.3 or 2005 end-points and that these are published through hello Metadata Exchange file (MEX).</span></span>

<span data-ttu-id="75afd-193">Olá seguintes declarações devem existir no token Olá recebida pelo Azure DRS para toocomplete de registro do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="75afd-193">hello following claims must exist in hello token received by Azure DRS for device registration toocomplete.</span></span> <span data-ttu-id="75afd-194">DRS Azure criará um objeto de dispositivo no AD do Azure com algumas dessas informações que são usadas pelo objeto de dispositivo do Azure AD Connect tooassociate Olá recém-criado com hello computador conta local.</span><span class="sxs-lookup"><span data-stu-id="75afd-194">Azure DRS will create a device object in Azure AD with some of this information which is then used by Azure AD Connect tooassociate hello newly created device object with hello computer account on-premises.</span></span>

* `http://schemas.microsoft.com/ws/2012/01/accounttype`
* `http://schemas.microsoft.com/identity/claims/onpremobjectguid`
* `http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`

<span data-ttu-id="75afd-195">Se você tiver mais de um nome de domínio verificado, você precisa tooprovide Olá declaração para os computadores a seguir:</span><span class="sxs-lookup"><span data-stu-id="75afd-195">If you have more than one verified domain name, you need tooprovide hello following claim for computers:</span></span>

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`

<span data-ttu-id="75afd-196">Se você já esteja emitindo uma declaração de ImmutableID (por exemplo, a ID de logon alternativo), será necessário tooprovide uma declaração correspondente para computadores:</span><span class="sxs-lookup"><span data-stu-id="75afd-196">If you are already issuing an ImmutableID claim (e.g., alternate login ID) you need tooprovide one corresponding claim for computers:</span></span>

* `http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`

<span data-ttu-id="75afd-197">Em Olá seções a seguir, você pode encontrar informações sobre:</span><span class="sxs-lookup"><span data-stu-id="75afd-197">In hello following sections, you find information about:</span></span>
 
- <span data-ttu-id="75afd-198">os valores Hello cada declaração deve ter</span><span class="sxs-lookup"><span data-stu-id="75afd-198">hello values each claim should have</span></span>
- <span data-ttu-id="75afd-199">Como uma definição se pareceria no AD FS</span><span class="sxs-lookup"><span data-stu-id="75afd-199">How a definition would look like in AD FS</span></span>

<span data-ttu-id="75afd-200">definição de saudação ajuda tooverify se houver valores hello, ou se você precisa toocreate-los.</span><span class="sxs-lookup"><span data-stu-id="75afd-200">hello definition helps you tooverify whether hello values are present or if you need toocreate them.</span></span>

> [!NOTE]
> <span data-ttu-id="75afd-201">Se você não usar o AD FS para o servidor de federação local, siga tooissue de configuração apropriada do fornecedor instruções toocreate Olá essas declarações.</span><span class="sxs-lookup"><span data-stu-id="75afd-201">If you don’t use AD FS for your on-premises federation server, follow your vendor's instructions toocreate hello appropriate configuration tooissue these claims.</span></span>

### <a name="issue-account-type-claim"></a><span data-ttu-id="75afd-202">Emitir declaração de tipo de conta</span><span class="sxs-lookup"><span data-stu-id="75afd-202">Issue account type claim</span></span>

<span data-ttu-id="75afd-203">**`http://schemas.microsoft.com/ws/2012/01/accounttype`**-Esta declaração deve conter um valor de **DJ**, que identifica o dispositivo hello como um computador ingressado no domínio.</span><span class="sxs-lookup"><span data-stu-id="75afd-203">**`http://schemas.microsoft.com/ws/2012/01/accounttype`** - This claim must contain a value of **DJ**, which identifies hello device as a domain-joined computer.</span></span> <span data-ttu-id="75afd-204">No AD FS, você pode adicionar uma regra de transformação de emissão que se parece com o seguinte:</span><span class="sxs-lookup"><span data-stu-id="75afd-204">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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

### <a name="issue-objectguid-of-hello-computer-account-on-premises"></a><span data-ttu-id="75afd-205">Execute o objectGUID do hello computador conta local</span><span class="sxs-lookup"><span data-stu-id="75afd-205">Issue objectGUID of hello computer account on-premises</span></span>

<span data-ttu-id="75afd-206">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`**-Esta declaração deve conter Olá **objectGUID** valor Olá conta de computador local.</span><span class="sxs-lookup"><span data-stu-id="75afd-206">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`** - This claim must contain hello **objectGUID** value of hello on-premises computer account.</span></span> <span data-ttu-id="75afd-207">No AD FS, você pode adicionar uma regra de transformação de emissão que se parece com o seguinte:</span><span class="sxs-lookup"><span data-stu-id="75afd-207">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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
 
### <a name="issue-objectsid-of-hello-computer-account-on-premises"></a><span data-ttu-id="75afd-208">Problema objectSID Olá computador conta local</span><span class="sxs-lookup"><span data-stu-id="75afd-208">Issue objectSID of hello computer account on-premises</span></span>

<span data-ttu-id="75afd-209">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`**-Esta declaração deve conter Olá Olá **objectSid** valor Olá conta de computador local.</span><span class="sxs-lookup"><span data-stu-id="75afd-209">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`** - This claim must contain hello hello **objectSid** value of hello on-premises computer account.</span></span> <span data-ttu-id="75afd-210">No AD FS, você pode adicionar uma regra de transformação de emissão que se parece com o seguinte:</span><span class="sxs-lookup"><span data-stu-id="75afd-210">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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

### <a name="issue-issuerid-for-computer-when-multiple-verified-domain-names-in-azure-ad"></a><span data-ttu-id="75afd-211">Emita o issuerID de computador quando houver vários nomes de domínio verificados no Azure AD</span><span class="sxs-lookup"><span data-stu-id="75afd-211">Issue issuerID for computer when multiple verified domain names in Azure AD</span></span>

<span data-ttu-id="75afd-212">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`**-Esta declaração deve conter Olá identificador URI (Uniform Resource) de qualquer um dos Olá verificar nomes de domínio que se conectam com hello token de emissão Olá federation service (AD FS ou 3ª parte) local.</span><span class="sxs-lookup"><span data-stu-id="75afd-212">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`** - This claim must contain hello Uniform Resource Identifier (URI) of any of hello verified domain names that connect with hello on-premises federation service (AD FS or 3rd party) issuing hello token.</span></span> <span data-ttu-id="75afd-213">No AD FS, você pode adicionar regras de transformação de emissão que pareçam Olá aquelas abaixo em que ordem específica após Olá aquelas acima.</span><span class="sxs-lookup"><span data-stu-id="75afd-213">In AD FS, you can add issuance transform rules that look like hello ones below in that specific order after hello ones above.</span></span> <span data-ttu-id="75afd-214">Observe que essa regra de saudação do problema de tooexplicitly uma regra para os usuários é necessário.</span><span class="sxs-lookup"><span data-stu-id="75afd-214">Please note that one rule tooexplicitly issue hello rule for users is necessary.</span></span> <span data-ttu-id="75afd-215">Em regras de saudação abaixo, uma regra primeiro identificar o usuário vs. autenticação de computador é adicionada.</span><span class="sxs-lookup"><span data-stu-id="75afd-215">In hello rules below, a first rule identifying user vs. computer authentication is added.</span></span>

    @RuleName = "Issue account type with hello value User when its not a computer"
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
    
    @RuleName = "Capture UPN when AccountType is User and issue hello IssuerID"
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


<span data-ttu-id="75afd-216">Declaração de saudação acima,</span><span class="sxs-lookup"><span data-stu-id="75afd-216">In hello claim above,</span></span>

- <span data-ttu-id="75afd-217">`$<domain>`é a URL do serviço Olá AD FS</span><span class="sxs-lookup"><span data-stu-id="75afd-217">`$<domain>` is hello AD FS service URL</span></span>
- <span data-ttu-id="75afd-218">`<verified-domain-name>`é um espaço reservado é necessário tooreplace com um de seus nomes de domínio verificado no AD do Azure</span><span class="sxs-lookup"><span data-stu-id="75afd-218">`<verified-domain-name>` is a placeholder you need tooreplace with one of your verified domain names in Azure AD</span></span>



<span data-ttu-id="75afd-219">Para obter mais detalhes sobre nomes de domínio verificado, consulte [adicionar um nome de domínio personalizado tooAzure do Active Directory](active-directory-add-domain.md).</span><span class="sxs-lookup"><span data-stu-id="75afd-219">For more details about verified domain names, see [Add a custom domain name tooAzure Active Directory](active-directory-add-domain.md).</span></span>  
<span data-ttu-id="75afd-220">tooget uma lista de seus domínios da empresa verificados, você pode usar o hello [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="75afd-220">tooget a list of your verified company domains, you can use hello [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet.</span></span> 

![Get-MsolDomain](./media/active-directory-conditional-access-automatic-device-registration-setup/01.png)

### <a name="issue-immutableid-for-computer-when-one-for-users-exist-eg-alternate-login-id-is-set"></a><span data-ttu-id="75afd-222">Emitir o ImmutableID de computador quando houver um para o usuário (por exemplo, a ID de login alternativa é definida)</span><span class="sxs-lookup"><span data-stu-id="75afd-222">Issue ImmutableID for computer when one for users exist (e.g. alternate login ID is set)</span></span>

<span data-ttu-id="75afd-223">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`** - Essa declaração deve conter um valor válido para computadores.</span><span class="sxs-lookup"><span data-stu-id="75afd-223">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`** - This claim must contain a valid value for computers.</span></span> <span data-ttu-id="75afd-224">No AD FS, você pode criar uma regra de transformação de emissão da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="75afd-224">In AD FS, you can create an issuance transform rule as follows:</span></span>

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

### <a name="helper-script-toocreate-hello-ad-fs-issuance-transform-rules"></a><span data-ttu-id="75afd-225">Regras de transformação de auxiliar script toocreate Olá AD FS emissão</span><span class="sxs-lookup"><span data-stu-id="75afd-225">Helper script toocreate hello AD FS issuance transform rules</span></span>

<span data-ttu-id="75afd-226">Hello script a seguir ajudará com a criação de saudação de emissão de saudação transformar regras descritas acima.</span><span class="sxs-lookup"><span data-stu-id="75afd-226">hello following script helps you with hello creation of hello issuance transform rules described above.</span></span>

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
    $rule4 = '@RuleName = "Issue account type with hello value User when it is not a computer"
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
    
    @RuleName = "Capture UPN when AccountType is User and issue hello IssuerID"
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

### <a name="remarks"></a><span data-ttu-id="75afd-227">Comentários</span><span class="sxs-lookup"><span data-stu-id="75afd-227">Remarks</span></span> 

- <span data-ttu-id="75afd-228">Esse script acrescenta Olá regras toohello existente regras.</span><span class="sxs-lookup"><span data-stu-id="75afd-228">This script appends hello rules toohello existing rules.</span></span> <span data-ttu-id="75afd-229">Script de saudação não são executadas duas vezes porque Olá conjuntos de regras será adicionado duas vezes.</span><span class="sxs-lookup"><span data-stu-id="75afd-229">Do not run hello script twice because hello set of rules would be added twice.</span></span> <span data-ttu-id="75afd-230">Certifique-se de que nenhuma regra correspondente existe para essas declarações (em condições de correspondente Olá) antes de executar o script hello novamente.</span><span class="sxs-lookup"><span data-stu-id="75afd-230">Make sure that no corresponding rules exist for these claims (under hello corresponding conditions) before running hello script again.</span></span>

- <span data-ttu-id="75afd-231">Se você tiver vários nomes de domínio verificado (conforme mostrado no portal de saudação do AD do Azure ou por meio do cmdlet Get-MsolDomains de saudação), definir o valor de saudação do **$multipleVerifiedDomainNames** Olá script muito**$true**.</span><span class="sxs-lookup"><span data-stu-id="75afd-231">If you have multiple verified domain names (as shown in hello Azure AD portal or via hello Get-MsolDomains cmdlet), set hello value of **$multipleVerifiedDomainNames** in hello script too**$true**.</span></span> <span data-ttu-id="75afd-232">Além disso, certifique-se de remover qualquer declaração de issuerid existente que possa ter sido criada pelo Azure AD Connect ou por outros meios.</span><span class="sxs-lookup"><span data-stu-id="75afd-232">Also make sure that you remove any existing issuerid claim that might have been created by Azure AD Connect or via other means.</span></span> <span data-ttu-id="75afd-233">Aqui está um exemplo dessa regra:</span><span class="sxs-lookup"><span data-stu-id="75afd-233">Here is an example for this rule:</span></span>


        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"]
        => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)",  "http://${domain}/adfs/services/trust/")); 

- <span data-ttu-id="75afd-234">Se você já tiver emitido um **ImmutableID** de declaração para contas de usuário, defina o valor de saudação do **$immutableIDAlreadyIssuedforUsers** Olá script muito**$true**.</span><span class="sxs-lookup"><span data-stu-id="75afd-234">If you have already issued an **ImmutableID** claim  for user accounts, set hello value of **$immutableIDAlreadyIssuedforUsers** in hello script too**$true**.</span></span>

## <a name="step-3-enable-windows-down-level-devices"></a><span data-ttu-id="75afd-235">Etapa 3: habilitar dispositivos de nível inferior do Windows</span><span class="sxs-lookup"><span data-stu-id="75afd-235">Step 3: Enable Windows down-level devices</span></span>

<span data-ttu-id="75afd-236">Se alguns dos seus dispositivos associados ao domínio forem dispositivos de nível inferior do Windows, você precisa:</span><span class="sxs-lookup"><span data-stu-id="75afd-236">If some of your domain-joined devices Windows down-level devices, you need to:</span></span>

- <span data-ttu-id="75afd-237">Defina uma política no AD do Azure tooenable tooregister os dispositivos dos usuários.</span><span class="sxs-lookup"><span data-stu-id="75afd-237">Set a policy in Azure AD tooenable users tooregister devices.</span></span>
 
- <span data-ttu-id="75afd-238">Configurar o local federação serviço tooissue declarações toosupport **Windows IWA (autenticação integrada)** para registro do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="75afd-238">Configure your on-premises federation service tooissue claims toosupport **Integrated Windows Authentication (IWA)** for device registration.</span></span>
 
- <span data-ttu-id="75afd-239">Adicione Olá AD do Azure dispositivo autenticação ponto de extremidade toohello local Intranet zonas tooavoid certificado solicita ao autenticar o dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="75afd-239">Add hello Azure AD device authentication end-point toohello local Intranet zones tooavoid certificate prompts when authenticating hello device.</span></span>

### <a name="set-policy-in-azure-ad-tooenable-users-tooregister-devices"></a><span data-ttu-id="75afd-240">Definir a diretiva no AD do Azure tooenable tooregister os dispositivos dos usuários</span><span class="sxs-lookup"><span data-stu-id="75afd-240">Set policy in Azure AD tooenable users tooregister devices</span></span>

<span data-ttu-id="75afd-241">tooregister dispositivos de nível inferior do Windows, você precisa toomake-se de que Olá configuração tooallow usuários tooregister dispositivos no AD do Azure está definida.</span><span class="sxs-lookup"><span data-stu-id="75afd-241">tooregister Windows down-level devices, you need toomake sure that hello setting tooallow users tooregister devices in Azure AD is set.</span></span> <span data-ttu-id="75afd-242">Olá portal do Azure, você encontrará essa configuração em:</span><span class="sxs-lookup"><span data-stu-id="75afd-242">In hello Azure portal, you can find this setting under:</span></span>

`Azure Active Directory > Users and groups > Device settings`
    
<span data-ttu-id="75afd-243">Olá seguinte política deve ser definida muito**todos os**: **os usuários podem registrar seus dispositivos com o Azure AD**</span><span class="sxs-lookup"><span data-stu-id="75afd-243">hello following policy must be set too**All**: **Users may register their devices with Azure AD**</span></span>

![Registrar dispositivos](./media/active-directory-conditional-access-automatic-device-registration-setup/23.png)


### <a name="configure-on-premises-federation-service"></a><span data-ttu-id="75afd-245">Configurar o serviço de federação local</span><span class="sxs-lookup"><span data-stu-id="75afd-245">Configure on-premises federation service</span></span> 

<span data-ttu-id="75afd-246">Seu serviço de federação local deve oferecer suporte à emissão Olá **authenticationmehod** e **wiaormultiauthn** declarações durante o recebimento de uma autenticação solicitar a terceira parte confiável toohello AD do Azure mantém um resouce_params parâmetro com um valor codificado conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="75afd-246">Your on-premises federation service must support issuing hello **authenticationmehod** and **wiaormultiauthn** claims when receiving an authentication request toohello Azure AD relying party holding a resouce_params parameter with an encoded value as shown below:</span></span>

    eyJQcm9wZXJ0aWVzIjpbeyJLZXkiOiJhY3IiLCJWYWx1ZSI6IndpYW9ybXVsdGlhdXRobiJ9XX0

    which decoded is {"Properties":[{"Key":"acr","Value":"wiaormultiauthn"}]}

<span data-ttu-id="75afd-247">Quando essa solicitação chega, serviço de federação local Olá deve autenticar o usuário hello usando a autenticação integrada do Windows e ao ser bem-sucedido, ele deverá emitir Olá duas declarações a seguir:</span><span class="sxs-lookup"><span data-stu-id="75afd-247">When such a request comes, hello on-premises federation service must authenticate hello user using Integrated Windows Authentication and upon success, it must issue hello following two claims:</span></span>

    http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows
    http://schemas.microsoft.com/claims/wiaormultiauthn

<span data-ttu-id="75afd-248">No AD FS, você deve adicionar esse método de autenticação Olá passa por uma regra de transformação de emissão.</span><span class="sxs-lookup"><span data-stu-id="75afd-248">In AD FS, you must add an issuance transform rule that passes-through hello authentication method.</span></span>  

<span data-ttu-id="75afd-249">**tooadd essa regra:**</span><span class="sxs-lookup"><span data-stu-id="75afd-249">**tooadd this rule:**</span></span>

1. <span data-ttu-id="75afd-250">No console de gerenciamento do hello AD FS, vá muito`AD FS > Trust Relationships > Relying Party Trusts`.</span><span class="sxs-lookup"><span data-stu-id="75afd-250">In hello AD FS management console, go too`AD FS > Trust Relationships > Relying Party Trusts`.</span></span>
2. <span data-ttu-id="75afd-251">Objeto de confiança de terceiros confiável Olá plataforma de identidade do Microsoft Office 365 e, em seguida, selecione **editar regras de declaração**.</span><span class="sxs-lookup"><span data-stu-id="75afd-251">Right-click hello Microsoft Office 365 Identity Platform relying party trust object, and then select **Edit Claim Rules**.</span></span>
3. <span data-ttu-id="75afd-252">Em Olá **regras de transformação de emissão** guia, selecione **Adicionar regra**.</span><span class="sxs-lookup"><span data-stu-id="75afd-252">On hello **Issuance Transform Rules** tab, select **Add Rule**.</span></span>
4. <span data-ttu-id="75afd-253">Em Olá **regra de declaração** lista de modelo, selecione **enviar declarações usando uma regra personalizada**.</span><span class="sxs-lookup"><span data-stu-id="75afd-253">In hello **Claim rule** template list, select **Send Claims Using a Custom Rule**.</span></span>
5. <span data-ttu-id="75afd-254">Selecione **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="75afd-254">Select **Next**.</span></span>
6. <span data-ttu-id="75afd-255">Em Olá **nome da regra de declaração** , digite **regra de declaração de método de autenticação**.</span><span class="sxs-lookup"><span data-stu-id="75afd-255">In hello **Claim rule name** box, type **Auth Method Claim Rule**.</span></span>
7. <span data-ttu-id="75afd-256">Em Olá **regra de declaração** caixa, Olá tipo regra a seguir:</span><span class="sxs-lookup"><span data-stu-id="75afd-256">In hello **Claim rule** box, type hello following rule:</span></span>

    `c:[Type == "http://schemas.microsoft.com/claims/authnmethodsreferences"] => issue(claim = c);`

8. <span data-ttu-id="75afd-257">No servidor de federação, digite o comando do PowerShell Olá abaixo depois de substituir  **\<RPObjectName\>**  com hello terceira parte confiável nome do objeto para o objeto de confiança de terceiros confiável do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="75afd-257">On your federation server, type hello PowerShell command below after replacing **\<RPObjectName\>** with hello relying party object name for your Azure AD relying party trust object.</span></span> <span data-ttu-id="75afd-258">Geralmente, este objeto é nomeado como **Plataforma de Identidade do Microsoft Office 365**.</span><span class="sxs-lookup"><span data-stu-id="75afd-258">This object usually is named **Microsoft Office 365 Identity Platform**.</span></span>
   
    `Set-AdfsRelyingPartyTrust -TargetName <RPObjectName> -AllowedAuthenticationClassReferences wiaormultiauthn`

### <a name="add-hello-azure-ad-device-authentication-end-point-toohello-local-intranet-zones"></a><span data-ttu-id="75afd-259">Adicionar zonas de Intranet Local Olá AD do Azure dispositivo autenticação ponto de extremidade toohello</span><span class="sxs-lookup"><span data-stu-id="75afd-259">Add hello Azure AD device authentication end-point toohello Local Intranet zones</span></span>

<span data-ttu-id="75afd-260">certificado tooavoid avisa quando os usuários no registro de dispositivos autenticar tooAzure AD, você pode enviar uma saudação de tooadd política tooyour dispositivos que ingressaram no domínio seguindo a zona de Intranet Local toohello URL no Internet Explorer:</span><span class="sxs-lookup"><span data-stu-id="75afd-260">tooavoid certificate prompts when users in register devices authenticate tooAzure AD you can push a policy tooyour domain-joined devices tooadd hello following URL toohello Local Intranet zone in Internet Explorer:</span></span>

`https://device.login.microsoftonline.com`

## <a name="step-4-control-deployment-and-rollout"></a><span data-ttu-id="75afd-261">Etapa 4: implantação de controle e distribuição</span><span class="sxs-lookup"><span data-stu-id="75afd-261">Step 4: Control deployment and rollout</span></span>

<span data-ttu-id="75afd-262">Quando você concluiu as etapas de saudação necessários, dispositivos que ingressaram no domínio são tooautomatically pronto registrar com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="75afd-262">When you have completed hello required steps, domain-joined devices are ready tooautomatically register with Azure AD.</span></span> <span data-ttu-id="75afd-263">Todos os dispositivos associados ao domínio que executarem a Atualização de Aniversário do Windows 10 e o Windows Server 2016 serão registrados automaticamente no Azure AD na reinicialização do dispositivo ou no login.</span><span class="sxs-lookup"><span data-stu-id="75afd-263">All domain-joined devices running Windows 10 Anniversary Update and Windows Server 2016 automatically register with Azure AD at device restart or user sign-in.</span></span> <span data-ttu-id="75afd-264">Registrar novos dispositivos com o Azure AD quando o dispositivo Olá é reiniciado após a conclusão da operação de junção de domínio hello.</span><span class="sxs-lookup"><span data-stu-id="75afd-264">New devices register with Azure AD when hello device restarts after hello domain join operation is completed.</span></span>

<span data-ttu-id="75afd-265">Dispositivos que foram anteriormente ingressos tooAzure AD (por exemplo, para o Intune) transição muito"*ingressado no domínio, registrado no AAD*"; no entanto, levará algum tempo para esse processo toocomplete em todos os dispositivos de vencimento toohello normal fluxo de atividade de usuário e domínio.</span><span class="sxs-lookup"><span data-stu-id="75afd-265">Devices that were previously workplace-joined tooAzure AD (for example for Intune) transition too“*Domain Joined, AAD Registered*”; however it takes some time for this process toocomplete across all devices due toohello normal flow of domain and user activity.</span></span>

### <a name="remarks"></a><span data-ttu-id="75afd-266">Comentários</span><span class="sxs-lookup"><span data-stu-id="75afd-266">Remarks</span></span>

- <span data-ttu-id="75afd-267">Você pode usar uma distribuição de saudação do toocontrol de objeto diretiva de grupo de registro automático do Windows 10 e computadores de domínio do Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="75afd-267">You can use a Group Policy object toocontrol hello rollout of automatic registration of Windows 10 and Windows Server 2016 domain-joined computers.</span></span>

- <span data-ttu-id="75afd-268">Windows 10 de novembro de 2015 atualizar automaticamente registra com o Azure AD **somente** se o objeto de diretiva de grupo de distribuição de saudação é definido.</span><span class="sxs-lookup"><span data-stu-id="75afd-268">Windows 10 November 2015 Update automatically registers with Azure AD **only** if hello rollout Group Policy object is set.</span></span>

- <span data-ttu-id="75afd-269">toorollout Olá o registro automático de computadores de nível inferior do Windows, você pode implantar um [pacote do Windows Installer](#windows-installer-packages-for-non-windows-10-computers) toocomputers que você selecionar.</span><span class="sxs-lookup"><span data-stu-id="75afd-269">toorollout hello automatic registration of Windows down-level computers, you can deploy a [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) toocomputers that you select.</span></span>

- <span data-ttu-id="75afd-270">Se você enviar por push a dispositivos que ingressaram no domínio tooWindows 8.1 objeto diretiva de grupo hello, registro será tentado. No entanto, é recomendável que você use Olá [pacote do Windows Installer](#windows-installer-packages-for-non-windows-10-computers) tooregister todos os seus dispositivos de baixo nível do Windows.</span><span class="sxs-lookup"><span data-stu-id="75afd-270">If you push hello Group Policy object tooWindows 8.1 domain-joined devices, registration will be attempted; however it is recommended that you use hello [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) tooregister all your Windows down-level devices.</span></span> 

### <a name="create-a-group-policy-object"></a><span data-ttu-id="75afd-271">Criar um objeto de Política de Grupo</span><span class="sxs-lookup"><span data-stu-id="75afd-271">Create a Group Policy object</span></span> 

<span data-ttu-id="75afd-272">distribuição de saudação toocontrol de registro automático de computadores com Windows atuais, você deve implantar Olá **registrar os computadores do domínio como dispositivos** dispositivos de toohello de objeto de diretiva de grupo que deseja tooregister.</span><span class="sxs-lookup"><span data-stu-id="75afd-272">toocontrol hello rollout of automatic registration of Windows current computers, you should deploy hello **Register domain-joined computers as devices** Group Policy object toohello devices you want tooregister.</span></span> <span data-ttu-id="75afd-273">Por exemplo, você pode implantar o grupo de segurança de tooa ou unidade organizacional do hello política tooan.</span><span class="sxs-lookup"><span data-stu-id="75afd-273">For example, you can deploy hello policy tooan organizational unit or tooa security group.</span></span>

<span data-ttu-id="75afd-274">**política de saudação tooset:**</span><span class="sxs-lookup"><span data-stu-id="75afd-274">**tooset hello policy:**</span></span>

1. <span data-ttu-id="75afd-275">Abra **Gerenciador do servidor**e, em seguida, ir muito`Tools > Group Policy Management`.</span><span class="sxs-lookup"><span data-stu-id="75afd-275">Open **Server Manager**, and then go too`Tools > Group Policy Management`.</span></span>
2. <span data-ttu-id="75afd-276">Vá toohello nó do domínio que corresponde a toohello domínio onde você deseja tooactivate o registro automático de computadores com Windows atuais.</span><span class="sxs-lookup"><span data-stu-id="75afd-276">Go toohello domain node that corresponds toohello domain where you want tooactivate auto-registration of Windows current computers.</span></span>
3. <span data-ttu-id="75afd-277">Clique com o botão direito do mouse em **Objetos de Política de Grupo** e selecione **Novo**.</span><span class="sxs-lookup"><span data-stu-id="75afd-277">Right-click **Group Policy Objects**, and then select **New**.</span></span>
4. <span data-ttu-id="75afd-278">Insira um nome para o objeto de Política de Grupo.</span><span class="sxs-lookup"><span data-stu-id="75afd-278">Type a name for your Group Policy object.</span></span> <span data-ttu-id="75afd-279">Por exemplo, *tooAzure o registro automático AD*.</span><span class="sxs-lookup"><span data-stu-id="75afd-279">For example, *Automatic Registration tooAzure AD*.</span></span> <span data-ttu-id="75afd-280">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="75afd-280">Select **OK**.</span></span>
5. <span data-ttu-id="75afd-281">Clique com o botão direito do mouse em seu novo objeto de Política de Grupo e selecione **Editar**.</span><span class="sxs-lookup"><span data-stu-id="75afd-281">Right-click your new Group Policy object, and then select **Edit**.</span></span>
6. <span data-ttu-id="75afd-282">Vá muito**configuração do computador** > **políticas** > **modelos administrativos** > **Windows Componentes** > **registro de dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="75afd-282">Go too**Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Device Registration**.</span></span> <span data-ttu-id="75afd-283">Clique com o botão direito do mouse em **Registrar computadores associados ao domínio como dispositivos** e selecione **Editar**.</span><span class="sxs-lookup"><span data-stu-id="75afd-283">Right-click **Register domain-joined computers as devices**, and then select **Edit**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="75afd-284">Este modelo de diretiva de grupo foi renomeado de versões anteriores do console de gerenciamento de política de grupo de saudação.</span><span class="sxs-lookup"><span data-stu-id="75afd-284">This Group Policy template has been renamed from earlier versions of hello Group Policy Management console.</span></span> <span data-ttu-id="75afd-285">Se você estiver usando uma versão anterior do console Olá, vá muito`Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span><span class="sxs-lookup"><span data-stu-id="75afd-285">If you are using an earlier version of hello console, go too`Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span></span> 

7. <span data-ttu-id="75afd-286">Selecione **Habilitado** e selecione **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="75afd-286">Select **Enabled**, and then select **Apply**.</span></span>
8. <span data-ttu-id="75afd-287">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="75afd-287">Select **OK**.</span></span>
9. <span data-ttu-id="75afd-288">Saudação de link local de tooa de objeto de diretiva de grupo de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="75afd-288">Link hello Group Policy object tooa location of your choice.</span></span> <span data-ttu-id="75afd-289">Por exemplo, você pode vincular unidade organizacional específica de tooa.</span><span class="sxs-lookup"><span data-stu-id="75afd-289">For example, you can link it tooa specific organizational unit.</span></span> <span data-ttu-id="75afd-290">Você também pode vinculá-lo tooa o grupo de segurança específico de computadores que se registrar automaticamente com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="75afd-290">You also could link it tooa specific security group of computers that automatically register with Azure AD.</span></span> <span data-ttu-id="75afd-291">tooset essa política para todos os computadores ingressados em domínio Windows 10 e Windows Server 2016 em sua organização, o domínio toohello de objeto de diretiva de grupo do link hello.</span><span class="sxs-lookup"><span data-stu-id="75afd-291">tooset this policy for all domain-joined Windows 10 and Windows Server 2016 computers in your organization, link hello Group Policy object toohello domain.</span></span>

### <a name="windows-installer-packages-for-non-windows-10-computers"></a><span data-ttu-id="75afd-292">Pacotes do Windows Installer para computadores que não são do Windows 10</span><span class="sxs-lookup"><span data-stu-id="75afd-292">Windows Installer packages for non-Windows 10 computers</span></span>

<span data-ttu-id="75afd-293">computadores de nível inferior Windows tooregister ingressado no domínio em um ambiente federado, você pode baixar e instalar esses pacotes do Windows Installer (. msi) do Centro de Download em Olá [Microsoft ingresso no local para computadores sem Windows 10](https://www.microsoft.com/en-us/download/details.aspx?id=53554) página.</span><span class="sxs-lookup"><span data-stu-id="75afd-293">tooregister domain-joined Windows down-level computers in a federated environment, you can download and install these Windows Installer package (.msi) from Download Center at hello [Microsoft Workplace Join for non-Windows 10 computers](https://www.microsoft.com/en-us/download/details.aspx?id=53554) page.</span></span>

<span data-ttu-id="75afd-294">Você pode implantar o pacote de saudação usando um sistema de distribuição de software como o System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="75afd-294">You can deploy hello package by using a software distribution system like System Center Configuration Manager.</span></span> <span data-ttu-id="75afd-295">Olá pacote dá suporte a opções de instalação silenciosa padrão Olá com hello *silencioso* parâmetro.</span><span class="sxs-lookup"><span data-stu-id="75afd-295">hello package supports hello standard silent install options with hello *quiet* parameter.</span></span> <span data-ttu-id="75afd-296">Ramificação atual do System Center Configuration Manager oferece benefícios adicionais de versões anteriores, como registros do hello capacidade tootrack concluída.</span><span class="sxs-lookup"><span data-stu-id="75afd-296">System Center Configuration Manager Current Branch offers additional benefits from earlier versions, like hello ability tootrack completed registrations.</span></span> <span data-ttu-id="75afd-297">Para obter mais informações, consulte [System Center 2016](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span><span class="sxs-lookup"><span data-stu-id="75afd-297">For more information, see [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span></span>

<span data-ttu-id="75afd-298">instalador de saudação cria uma tarefa agendada no sistema de saudação que é executado no contexto de saudação do usuário.</span><span class="sxs-lookup"><span data-stu-id="75afd-298">hello installer creates a scheduled task on hello system that runs in hello user’s context.</span></span> <span data-ttu-id="75afd-299">tarefa Olá é disparada quando o usuário Olá entra em tooWindows.</span><span class="sxs-lookup"><span data-stu-id="75afd-299">hello task is triggered when hello user signs in tooWindows.</span></span> <span data-ttu-id="75afd-300">tarefa Olá silenciosamente registra o dispositivo Olá com o Azure AD com as credenciais do usuário Olá depois de autenticar usando a autenticação integrada do Windows.</span><span class="sxs-lookup"><span data-stu-id="75afd-300">hello task silently registers hello device with Azure AD with hello user credentials after authenticating using Integrated Windows Authentication.</span></span> <span data-ttu-id="75afd-301">tarefa agendada do toosee hello, no dispositivo hello, ir muito**Microsoft** > **ingresso**, e em seguida, acesse a biblioteca do Agendador de tarefas toohello.</span><span class="sxs-lookup"><span data-stu-id="75afd-301">toosee hello scheduled task, in hello device, go too**Microsoft** > **Workplace Join**, and then go toohello Task Scheduler library.</span></span>

## <a name="step-5-verify-registered-devices"></a><span data-ttu-id="75afd-302">Etapa 5: verificar os dispositivos registrados</span><span class="sxs-lookup"><span data-stu-id="75afd-302">Step 5: Verify registered devices</span></span>

<span data-ttu-id="75afd-303">Você pode verificar os dispositivos registrados com êxito em sua organização usando Olá [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet Olá [módulo do Azure Active Directory PowerShell](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="75afd-303">You can check successful registered devices in your organization by using hello [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in hello [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span>

<span data-ttu-id="75afd-304">saída deste cmdlet Olá mostra os dispositivos registrados no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="75afd-304">hello output of this cmdlet shows devices registered in Azure AD.</span></span> <span data-ttu-id="75afd-305">tooget todos os dispositivos, use Olá **-todos os** parâmetro e, em seguida, filtrá-los usando Olá **deviceTrustType** propriedade.</span><span class="sxs-lookup"><span data-stu-id="75afd-305">tooget all devices, use hello **-All** parameter, and then filter them using hello **deviceTrustType** property.</span></span> <span data-ttu-id="75afd-306">Dispositivos associados ao domínio possuem um valor de **Associado ao domínio**.</span><span class="sxs-lookup"><span data-stu-id="75afd-306">Domain joined devices have a value of **Domain Joined**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="75afd-307">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="75afd-307">Next steps</span></span>

* [<span data-ttu-id="75afd-308">Perguntas frequentes sobre o registro de dispositivo automático</span><span class="sxs-lookup"><span data-stu-id="75afd-308">Automatic device registration FAQ</span></span>](active-directory-device-registration-faq.md)
* [<span data-ttu-id="75afd-309">Solucionando problemas de registro automático de domínio Unido computadores tooAzure AD – Windows 10 e Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="75afd-309">Troubleshooting auto-registration of domain joined computers tooAzure AD – Windows 10 and Windows Server 2016</span></span>](active-directory-device-registration-troubleshoot-windows.md)
* [<span data-ttu-id="75afd-310">Solucionando problemas de registro automático de domínio Unido computadores tooAzure AD – não - Windows 10</span><span class="sxs-lookup"><span data-stu-id="75afd-310">Troubleshooting auto-registration of domain joined computers tooAzure AD – non-Windows 10</span></span>](active-directory-device-registration-troubleshoot-windows-legacy.md)
* [<span data-ttu-id="75afd-311">Acesso condicional ao Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="75afd-311">Azure Active Directory conditional access</span></span>](active-directory-conditional-access-azure-portal.md)



<!--Image references-->
[1]: ./media/active-directory-conditional-access-automatic-device-registration-setup/12.png
