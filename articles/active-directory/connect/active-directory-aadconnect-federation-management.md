---
title: "aaaActive Directory Federation Services personalização com o Azure AD Connect e gerenciamento | Microsoft Docs"
description: "Gerenciamento do AD FS com o Azure AD Connect e personalização da experiência de entrada do AD FS do usuário com o Azure AD e o PowerShell."
keywords: "AD FS, ADFS, gerenciamento do AD FS, AAD Connect, Conectar, entrada, personalização do AD FS, reparar confiança, O365, federação, terceira parte confiável"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 2593b6c6-dc3f-46ef-8e02-a8e2dc4e9fb9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 361a2bfd6d7a6993dbe773d6ea039ad1afc6346a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-and-customize-active-directory-federation-services-by-using-azure-ad-connect"></a><span data-ttu-id="cd931-104">Gerenciar e personalizar os Serviços de Federação do Active Directory usando o Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="cd931-104">Manage and customize Active Directory Federation Services by using Azure AD Connect</span></span>
<span data-ttu-id="cd931-105">Este artigo descreve como toomanage e personalizar os serviços de Federação do Active Directory (AD FS) usando o Connect do Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="cd931-105">This article describes how toomanage and customize Active Directory Federation Services (AD FS) by using Azure Active Directory (Azure AD) Connect.</span></span> <span data-ttu-id="cd931-106">Ele também inclui outras tarefas comuns do AD FS que talvez você precise toodo para concluir a configuração de um farm do AD FS.</span><span class="sxs-lookup"><span data-stu-id="cd931-106">It also includes other common AD FS tasks that you might need toodo for a complete configuration of an AD FS farm.</span></span>

| <span data-ttu-id="cd931-107">Tópico</span><span class="sxs-lookup"><span data-stu-id="cd931-107">Topic</span></span> | <span data-ttu-id="cd931-108">O que ele abrange</span><span class="sxs-lookup"><span data-stu-id="cd931-108">What it covers</span></span> |
|:--- |:--- |
| <span data-ttu-id="cd931-109">**Gerenciar o AD FS**</span><span class="sxs-lookup"><span data-stu-id="cd931-109">**Manage AD FS**</span></span> | |
| [<span data-ttu-id="cd931-110">Reparar confiança Olá</span><span class="sxs-lookup"><span data-stu-id="cd931-110">Repair hello trust</span></span>](#repairthetrust) |<span data-ttu-id="cd931-111">Como a federação de saudação toorepair confiança com o Office 365.</span><span class="sxs-lookup"><span data-stu-id="cd931-111">How toorepair hello federation trust with Office 365.</span></span> |
| [<span data-ttu-id="cd931-112">Federar ao Azure AD usando uma ID de logon alternativa </span><span class="sxs-lookup"><span data-stu-id="cd931-112">Federate with Azure AD using alternate login ID </span></span>](#alternateid) | <span data-ttu-id="cd931-113">Configurar a federação usando uma ID de logon alternativa</span><span class="sxs-lookup"><span data-stu-id="cd931-113">Configure federation using alternate login ID</span></span>  |
| [<span data-ttu-id="cd931-114">Adicionar um servidor do AD FS</span><span class="sxs-lookup"><span data-stu-id="cd931-114">Add an AD FS server</span></span>](#addadfsserver) |<span data-ttu-id="cd931-115">Como tooexpand um AD FS do farm com um servidor do AD FS adicional.</span><span class="sxs-lookup"><span data-stu-id="cd931-115">How tooexpand an AD FS farm with an additional AD FS server.</span></span> |
| [<span data-ttu-id="cd931-116">Adicionar um Servidor Proxy de Aplicativo Web do AD FS</span><span class="sxs-lookup"><span data-stu-id="cd931-116">Add an AD FS Web Application Proxy server</span></span>](#addwapserver) |<span data-ttu-id="cd931-117">Como tooexpand um AD FS do farm com um servidor de Proxy de aplicativo da Web (WAP) adicional.</span><span class="sxs-lookup"><span data-stu-id="cd931-117">How tooexpand an AD FS farm with an additional Web Application Proxy (WAP) server.</span></span> |
| [<span data-ttu-id="cd931-118">Adicionar um domínio federado</span><span class="sxs-lookup"><span data-stu-id="cd931-118">Add a federated domain</span></span>](#addfeddomain) |<span data-ttu-id="cd931-119">Como tooadd um domínio federado.</span><span class="sxs-lookup"><span data-stu-id="cd931-119">How tooadd a federated domain.</span></span> |
| [<span data-ttu-id="cd931-120">Atualizar o certificado SSL de saudação</span><span class="sxs-lookup"><span data-stu-id="cd931-120">Update hello SSL certificate</span></span>](active-directory-aadconnectfed-ssl-update.md)| <span data-ttu-id="cd931-121">Como tooupdate Olá SSL de certificado para um farm do AD FS.</span><span class="sxs-lookup"><span data-stu-id="cd931-121">How tooupdate hello SSL certificate for an AD FS farm.</span></span> |
| <span data-ttu-id="cd931-122">**Personalizar o AD FS**</span><span class="sxs-lookup"><span data-stu-id="cd931-122">**Customize AD FS**</span></span> | |
| [<span data-ttu-id="cd931-123">Adicionar uma ilustração ou um logotipo da empresa personalizado</span><span class="sxs-lookup"><span data-stu-id="cd931-123">Add a custom company logo or illustration</span></span>](#customlogo) |<span data-ttu-id="cd931-124">Como toocustomize um AD FS sign-in de página com um logotipo da empresa e a ilustração.</span><span class="sxs-lookup"><span data-stu-id="cd931-124">How toocustomize an AD FS sign-in page with a company logo and illustration.</span></span> |
| [<span data-ttu-id="cd931-125">Adicionar uma descrição de entrada</span><span class="sxs-lookup"><span data-stu-id="cd931-125">Add a sign-in description</span></span>](#addsignindescription) |<span data-ttu-id="cd931-126">Como tooadd um entrada na página de descrição.</span><span class="sxs-lookup"><span data-stu-id="cd931-126">How tooadd a sign-in page description.</span></span> |
| [<span data-ttu-id="cd931-127">Modificar regras de declaração do AD FS</span><span class="sxs-lookup"><span data-stu-id="cd931-127">Modify AD FS claim rules</span></span>](#modclaims) |<span data-ttu-id="cd931-128">Como toomodify do AD FS declarações para vários cenários de Federação.</span><span class="sxs-lookup"><span data-stu-id="cd931-128">How toomodify AD FS claims for various federation scenarios.</span></span> |

## <a name="manage-ad-fs"></a><span data-ttu-id="cd931-129">Gerenciar o AD FS</span><span class="sxs-lookup"><span data-stu-id="cd931-129">Manage AD FS</span></span>
<span data-ttu-id="cd931-130">Você pode executar várias tarefas de AD FS relacionados no Azure AD Connect com mínima intervenção do usuário usando o Assistente do hello Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="cd931-130">You can perform various AD FS-related tasks in Azure AD Connect with minimal user intervention by using hello Azure AD Connect wizard.</span></span> <span data-ttu-id="cd931-131">Depois de instalar o Azure AD Connect pelo Assistente de saudação em execução, você pode executar o Assistente de saudação novamente tooperform tarefas adicionais.</span><span class="sxs-lookup"><span data-stu-id="cd931-131">After you've finished installing Azure AD Connect by running hello wizard, you can run hello wizard again tooperform additional tasks.</span></span>

## <span data-ttu-id="cd931-132">Reparar confiança Olá<a name=repairthetrust></a></span><span class="sxs-lookup"><span data-stu-id="cd931-132">Repair hello trust <a name=repairthetrust></a></span></span>
<span data-ttu-id="cd931-133">Você pode usar a integridade atual do Azure AD Connect toocheck Olá de saudação do AD FS e a confiança do AD do Azure e tomar as ações apropriadas toorepair Olá confiança.</span><span class="sxs-lookup"><span data-stu-id="cd931-133">You can use Azure AD Connect toocheck hello current health of hello AD FS and Azure AD trust and take appropriate actions toorepair hello trust.</span></span> <span data-ttu-id="cd931-134">Siga estas etapas toorepair do Azure AD e o AD FS confiam.</span><span class="sxs-lookup"><span data-stu-id="cd931-134">Follow these steps toorepair your Azure AD and AD FS trust.</span></span>

1. <span data-ttu-id="cd931-135">Selecione **AAD reparo e a relação de confiança do ADFS** de lista de saudação de tarefas adicionais.</span><span class="sxs-lookup"><span data-stu-id="cd931-135">Select **Repair AAD and ADFS Trust** from hello list of additional tasks.</span></span>
   <span data-ttu-id="cd931-136">![Reparar a relação de confiança do AAD e do ADFS](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)</span><span class="sxs-lookup"><span data-stu-id="cd931-136">![Repair AAD and ADFS Trust](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)</span></span>

2. <span data-ttu-id="cd931-137">Em Olá **conectar tooAzure AD** , forneça suas credenciais de administrador global do AD do Azure e, em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="cd931-137">On hello **Connect tooAzure AD** page, provide your global administrator credentials for Azure AD, and click **Next**.</span></span>
   <span data-ttu-id="cd931-138">![Conecte-se tooAzure AD](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)</span><span class="sxs-lookup"><span data-stu-id="cd931-138">![Connect tooAzure AD](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)</span></span>

3. <span data-ttu-id="cd931-139">Em Olá **credenciais de acesso remoto** insira credenciais Olá para o administrador de domínio hello.</span><span class="sxs-lookup"><span data-stu-id="cd931-139">On hello **Remote access credentials** page, enter hello credentials for hello domain administrator.</span></span>

   ![Credenciais de acesso remoto](media/active-directory-aadconnect-federation-management/RepairADTrust3.PNG)

    <span data-ttu-id="cd931-141">Depois que você clicar em **Avançar**, o Azure AD Connect verificará a integridade do certificado e mostrará eventuais problemas.</span><span class="sxs-lookup"><span data-stu-id="cd931-141">After you click **Next**, Azure AD Connect checks for certificate health and shows any issues.</span></span>

    ![Estado de certificados](media/active-directory-aadconnect-federation-management/RepairADTrust4.PNG)

    <span data-ttu-id="cd931-143">Olá **tooconfigure pronto** página Olá mostra a lista de ações que serão executadas toorepair confiança de saudação.</span><span class="sxs-lookup"><span data-stu-id="cd931-143">hello **Ready tooconfigure** page shows hello list of actions that will be performed toorepair hello trust.</span></span>

    ![Tooconfigure pronto](media/active-directory-aadconnect-federation-management/RepairADTrust5.PNG)

4. <span data-ttu-id="cd931-145">Clique em **instalar** toorepair confiança de saudação.</span><span class="sxs-lookup"><span data-stu-id="cd931-145">Click **Install** toorepair hello trust.</span></span>

> [!NOTE]
> <span data-ttu-id="cd931-146">O Azure AD Connect só pode reparar ou agir em relação a certificados autoassinados.</span><span class="sxs-lookup"><span data-stu-id="cd931-146">Azure AD Connect can only repair or act on certificates that are self-signed.</span></span> <span data-ttu-id="cd931-147">O Azure AD Connect não pode reparar certificados de terceiros.</span><span class="sxs-lookup"><span data-stu-id="cd931-147">Azure AD Connect can't repair third-party certificates.</span></span>

## <span data-ttu-id="cd931-148">Federar ao Azure AD usando uma AlternateID <a name=alternateid></a></span><span class="sxs-lookup"><span data-stu-id="cd931-148">Federate with Azure AD using AlternateID <a name=alternateid></a></span></span>
<span data-ttu-id="cd931-149">É recomendável que Olá Principal do usuário Name(UPN) local e nuvem Olá Nome Principal do usuário são mantidos Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="cd931-149">It is recommended that hello on-premises User Principal Name(UPN) and hello cloud User Principal Name are kept hello same.</span></span> <span data-ttu-id="cd931-150">Se Olá UPN local usa um domínio não roteáveis (ex.</span><span class="sxs-lookup"><span data-stu-id="cd931-150">If hello on-premises UPN uses a non-routable domain (ex.</span></span> <span data-ttu-id="cd931-151">Contoso. local) ou não pode ser alterado devido a dependências do aplicativo toolocal, é recomendável definir a ID de logon alternativo.</span><span class="sxs-lookup"><span data-stu-id="cd931-151">Contoso.local) or cannot be changed due toolocal application dependencies, we recommend setting up alternate login ID.</span></span> <span data-ttu-id="cd931-152">ID de logon alternativo permite que você tooconfigure uma experiência de entrada no qual os usuários podem entrar com um atributo diferente de seu UPN, como email.</span><span class="sxs-lookup"><span data-stu-id="cd931-152">Alternate login ID allows you tooconfigure a sign-in experience where users can sign in with an attribute other than their UPN, such as mail.</span></span> <span data-ttu-id="cd931-153">opção de saudação para nome Principal do usuário no atributo do Azure AD Connect padrões toohello userPrincipalName no Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cd931-153">hello choice for User Principal Name in Azure AD Connect defaults toohello userPrincipalName attribute in Active Directory.</span></span> <span data-ttu-id="cd931-154">Se você escolher qualquer outro atributo para o nome UPN e estiver federando com o uso do AD FS, o Azure AD Connect configurará o AD FS para a ID de logon alternativa.</span><span class="sxs-lookup"><span data-stu-id="cd931-154">If you choose any other attribute for User Principal Name and are federating using AD FS, then Azure AD Connect will configure AD FS for alternate login ID.</span></span> <span data-ttu-id="cd931-155">Um exemplo de escolha de um atributo diferente para o nome UPN é mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="cd931-155">An example of choosing a different attribute for User Principal Name is shown below:</span></span>

![Seleção de atributo de ID alternativa](media/active-directory-aadconnect-federation-management/attributeselection.png)

<span data-ttu-id="cd931-157">A configuração da ID de logon alternativa do AD FS consiste em duas etapas principais:</span><span class="sxs-lookup"><span data-stu-id="cd931-157">Configuring alternate login ID for AD FS consists of two main steps:</span></span>
1. <span data-ttu-id="cd931-158">**Configurar conjunto de declarações de emissão certo Olá**: regras de declaração de emissão de saudação na terceira parte confiável Olá AD do Azure de confiança são modificadas toouse Olá selecionado UserPrincipalName atributo como Olá ID alternativa do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="cd931-158">**Configure hello right set of issuance claims**: hello issuance claim rules in hello Azure AD relying party trust are modified toouse hello selected UserPrincipalName attribute as hello alternate ID of hello user.</span></span>
2. <span data-ttu-id="cd931-159">**Habilitar identificação de logon alternativo na configuração de saudação do AD FS**: configuração do hello AD FS é atualizada para que o AD FS pode pesquisar usuários Olá florestas apropriado usando a ID alternativa Olá</span><span class="sxs-lookup"><span data-stu-id="cd931-159">**Enable alternate login ID in hello AD FS configuration**: hello AD FS configuration is updated so that AD FS can look up users in hello appropriate forests using hello alternate ID.</span></span> <span data-ttu-id="cd931-160">Há suporte para essa configuração no AD FS no Windows Server 2012 R2 (com KB2919355) ou posterior.</span><span class="sxs-lookup"><span data-stu-id="cd931-160">This configuration is supported for AD FS on Windows Server 2012 R2 (with KB2919355) or later.</span></span> <span data-ttu-id="cd931-161">Se Olá AD FS servidores 2012 R2, as verificações do Azure AD Connect presença Olá Olá necessário KB.</span><span class="sxs-lookup"><span data-stu-id="cd931-161">If hello AD FS servers are 2012 R2, Azure AD Connect checks for hello presence of hello required KB.</span></span> <span data-ttu-id="cd931-162">Se hello KB não for detectado, um aviso aparecerá após a conclusão da configuração, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="cd931-162">If hello KB is not detected, a warning will be displayed after configuration completes, as shown below:</span></span>

    ![Aviso de ausência de KB no 2012R2](media/active-directory-aadconnect-federation-management/kbwarning.png)

    <span data-ttu-id="cd931-164">configuração de saudação toorectify no caso de KB ausente, instale Olá necessário [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) e repare Olá confiança usando [reparar AAD e confiança do AD FS](#repairthetrust).</span><span class="sxs-lookup"><span data-stu-id="cd931-164">toorectify hello configuration in case of missing KB, install hello required [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) and then repair hello trust using [Repair AAD and AD FS Trust](#repairthetrust).</span></span>

> [!NOTE]
> <span data-ttu-id="cd931-165">Para obter mais informações sobre toomanually alternateID e etapas de configurar, ler [Configurando ID de logon alternativo](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)</span><span class="sxs-lookup"><span data-stu-id="cd931-165">For more information on alternateID and steps toomanually configure, read [Configuring Alternate Login ID](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)</span></span>

## <span data-ttu-id="cd931-166">Adicionar um servidor do AD FS <a name=addadfsserver></a></span><span class="sxs-lookup"><span data-stu-id="cd931-166">Add an AD FS server <a name=addadfsserver></a></span></span>

> [!NOTE]
> <span data-ttu-id="cd931-167">servidor tooadd um AD FS, do Azure AD Connect exige o certificado de PFX hello.</span><span class="sxs-lookup"><span data-stu-id="cd931-167">tooadd an AD FS server, Azure AD Connect requires hello PFX certificate.</span></span> <span data-ttu-id="cd931-168">Portanto, você pode executar esta operação somente se você configurou o farm do hello AD FS usando o Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="cd931-168">Therefore, you can perform this operation only if you configured hello AD FS farm by using Azure AD Connect.</span></span>

1. <span data-ttu-id="cd931-169">Selecione **Implantar um Servidor de Federação adicional** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="cd931-169">Select **Deploy an additional Federation Server**, and click **Next**.</span></span>

   ![Servidor de federação adicional](media/active-directory-aadconnect-federation-management/AddNewADFSServer1.PNG)

2. <span data-ttu-id="cd931-171">Em Olá **conectar tooAzure AD** , insira suas credenciais de administrador global do AD do Azure e, em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="cd931-171">On hello **Connect tooAzure AD** page, enter your global administrator credentials for Azure AD, and click **Next**.</span></span>

   ![Conecte-se tooAzure AD](media/active-directory-aadconnect-federation-management/AddNewADFSServer2.PNG)

3. <span data-ttu-id="cd931-173">Forneça credenciais de administrador de domínio de saudação.</span><span class="sxs-lookup"><span data-stu-id="cd931-173">Provide hello domain administrator credentials.</span></span>

   ![Credenciais de administrador de domínio](media/active-directory-aadconnect-federation-management/AddNewADFSServer3.PNG)

4. <span data-ttu-id="cd931-175">Azure AD Connect solicita uma senha de saudação do arquivo PFX Olá que você forneceu ao configurar seu novo farm do AD FS com o Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="cd931-175">Azure AD Connect asks for hello password of hello PFX file that you provided while configuring your new AD FS farm with Azure AD Connect.</span></span> <span data-ttu-id="cd931-176">Clique em **digitar senha** tooprovide senha Olá arquivo PFX de saudação.</span><span class="sxs-lookup"><span data-stu-id="cd931-176">Click **Enter Password** tooprovide hello password for hello PFX file.</span></span>

   ![Senha de certificado](media/active-directory-aadconnect-federation-management/AddNewADFSServer4.PNG)

    ![Especificar certificado SSL](media/active-directory-aadconnect-federation-management/AddNewADFSServer5.PNG)

5. <span data-ttu-id="cd931-179">Em Olá **servidores do AD FS** , insira o nome do servidor de saudação ou toobe de endereço IP adicionado farm do toohello AD FS.</span><span class="sxs-lookup"><span data-stu-id="cd931-179">On hello **AD FS Servers** page, enter hello server name or IP address toobe added toohello AD FS farm.</span></span>

   ![Servidores do AD FS](media/active-directory-aadconnect-federation-management/AddNewADFSServer6.PNG)

6. <span data-ttu-id="cd931-181">Clique em **próximo**e percorrer Olá final **configurar** página.</span><span class="sxs-lookup"><span data-stu-id="cd931-181">Click **Next**, and go through hello final **Configure** page.</span></span> <span data-ttu-id="cd931-182">Depois que o Azure AD Connect concluiu a adição de farm do hello servidores toohello AD FS, você terá conectividade de Olá Olá opção tooverify.</span><span class="sxs-lookup"><span data-stu-id="cd931-182">After Azure AD Connect has finished adding hello servers toohello AD FS farm, you will be given hello option tooverify hello connectivity.</span></span>

   ![Tooconfigure pronto](media/active-directory-aadconnect-federation-management/AddNewADFSServer7.PNG)

    ![Instalação concluída](media/active-directory-aadconnect-federation-management/AddNewADFSServer8.PNG)

## <span data-ttu-id="cd931-185">Adicionar um servidor WAP do AD FS <a name=addwapserver></a></span><span class="sxs-lookup"><span data-stu-id="cd931-185">Add an AD FS WAP server <a name=addwapserver></a></span></span>

> [!NOTE]
> <span data-ttu-id="cd931-186">tooadd um servidor WAP, Azure AD Connect exige o certificado de PFX hello.</span><span class="sxs-lookup"><span data-stu-id="cd931-186">tooadd a WAP server, Azure AD Connect requires hello PFX certificate.</span></span> <span data-ttu-id="cd931-187">Portanto, você pode executar esta operação somente se você configurou o farm do hello AD FS usando o Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="cd931-187">Therefore, you can only perform this operation if you configured hello AD FS farm by using Azure AD Connect.</span></span>

1. <span data-ttu-id="cd931-188">Selecione **implantar o Proxy de aplicativo Web** da lista de saudação de tarefas disponíveis.</span><span class="sxs-lookup"><span data-stu-id="cd931-188">Select **Deploy Web Application Proxy** from hello list of available tasks.</span></span>

   ![Implantar o proxy de aplicativo Web](media/active-directory-aadconnect-federation-management/WapServer1.PNG)

2. <span data-ttu-id="cd931-190">Forneça credenciais de administrador global do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="cd931-190">Provide hello Azure global administrator credentials.</span></span>

   ![Conecte-se tooAzure AD](media/active-directory-aadconnect-federation-management/wapserver2.PNG)

3. <span data-ttu-id="cd931-192">Em Olá **certificado SSL especificar** , forneça a senha de saudação para arquivo PFX Olá fornecido quando você configurou o farm do hello AD FS com o Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="cd931-192">On hello **Specify SSL certificate** page, provide hello password for hello PFX file that you provided when you configured hello AD FS farm with Azure AD Connect.</span></span>
   <span data-ttu-id="cd931-193">![Senha de certificado](media/active-directory-aadconnect-federation-management/WapServer3.PNG)</span><span class="sxs-lookup"><span data-stu-id="cd931-193">![Certificate password](media/active-directory-aadconnect-federation-management/WapServer3.PNG)</span></span>

    ![Especificar certificado SSL](media/active-directory-aadconnect-federation-management/WapServer4.PNG)

4. <span data-ttu-id="cd931-195">Adicione Olá server toobe adicionado como um servidor WAP.</span><span class="sxs-lookup"><span data-stu-id="cd931-195">Add hello server toobe added as a WAP server.</span></span> <span data-ttu-id="cd931-196">Como servidor WAP de saudação não pode ser toohello ingressado no domínio, o Assistente de saudação solicita servidor toohello de credenciais administrativas que está sendo adicionado.</span><span class="sxs-lookup"><span data-stu-id="cd931-196">Because hello WAP server might not be joined toohello domain, hello wizard asks for administrative credentials toohello server being added.</span></span>

   ![Credenciais administrativas de servidor](media/active-directory-aadconnect-federation-management/WapServer5.PNG)

5. <span data-ttu-id="cd931-198">Em Olá **credenciais de relação de confiança de Proxy** página, forneça proxy de saudação tooconfigure credenciais administrativas de confiança e acesso saudação do servidor primária no farm de saudação do AD FS.</span><span class="sxs-lookup"><span data-stu-id="cd931-198">On hello **Proxy trust credentials** page, provide administrative credentials tooconfigure hello proxy trust and access hello primary server in hello AD FS farm.</span></span>

   ![Credenciais de confiança de proxy](media/active-directory-aadconnect-federation-management/WapServer6.PNG)

6. <span data-ttu-id="cd931-200">Em Olá **tooconfigure pronto** página, o assistente Olá mostra lista Olá das ações que serão executadas.</span><span class="sxs-lookup"><span data-stu-id="cd931-200">On hello **Ready tooconfigure** page, hello wizard shows hello list of actions that will be performed.</span></span>

   ![Tooconfigure pronto](media/active-directory-aadconnect-federation-management/WapServer7.PNG)

7. <span data-ttu-id="cd931-202">Clique em **instalar** toofinish configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="cd931-202">Click **Install** toofinish hello configuration.</span></span> <span data-ttu-id="cd931-203">Após a conclusão da configuração hello, fornece de assistente Olá Olá tooverify opção Olá servidores toohello de conectividade.</span><span class="sxs-lookup"><span data-stu-id="cd931-203">After hello configuration is complete, hello wizard gives you hello option tooverify hello connectivity toohello servers.</span></span> <span data-ttu-id="cd931-204">Clique em **verificar** toocheck conectividade.</span><span class="sxs-lookup"><span data-stu-id="cd931-204">Click **Verify** toocheck connectivity.</span></span>

   ![Instalação concluída](media/active-directory-aadconnect-federation-management/WapServer8.PNG)

## <span data-ttu-id="cd931-206">Adicionar um domínio federado <a name=addfeddomain></a></span><span class="sxs-lookup"><span data-stu-id="cd931-206">Add a federated domain <a name=addfeddomain></a></span></span>

<span data-ttu-id="cd931-207">É fácil tooadd toobe um domínio federado com o Azure AD usando o Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="cd931-207">It's easy tooadd a domain toobe federated with Azure AD by using Azure AD Connect.</span></span> <span data-ttu-id="cd931-208">Azure AD Connect adiciona o domínio Olá para federação e modifica declaração Olá regras toocorrectly refletir emissor hello quando você tiver vários domínios federados com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cd931-208">Azure AD Connect adds hello domain for federation and modifies hello claim rules toocorrectly reflect hello issuer when you have multiple domains federated with Azure AD.</span></span>

1. <span data-ttu-id="cd931-209">tooadd um domínio federado, tarefa Olá selecione **adicionar um domínio do AD do Azure**.</span><span class="sxs-lookup"><span data-stu-id="cd931-209">tooadd a federated domain, select hello task **Add an additional Azure AD domain**.</span></span>

   ![Domínio do Azure AD adicional](media/active-directory-aadconnect-federation-management/AdditionalDomain1.PNG)

2. <span data-ttu-id="cd931-211">Na próxima página do Assistente de Olá Olá, forneça credenciais de administrador global de saudação do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="cd931-211">On hello next page of hello wizard, provide hello global administrator credentials for Azure AD.</span></span>

   ![Conecte-se tooAzure AD](media/active-directory-aadconnect-federation-management/AdditionalDomain2.PNG)

3. <span data-ttu-id="cd931-213">Em Olá **credenciais de acesso remoto** , forneça credenciais de administrador de domínio hello.</span><span class="sxs-lookup"><span data-stu-id="cd931-213">On hello **Remote access credentials** page, provide hello domain administrator credentials.</span></span>

   ![Credenciais de acesso remoto](media/active-directory-aadconnect-federation-management/additionaldomain3.PNG)

4. <span data-ttu-id="cd931-215">Na página seguinte do hello, o Assistente de saudação fornece uma lista de domínios do AD do Azure que você pode federar o seu diretório local com.</span><span class="sxs-lookup"><span data-stu-id="cd931-215">On hello next page, hello wizard provides a list of Azure AD domains that you can federate your on-premises directory with.</span></span> <span data-ttu-id="cd931-216">Escolha domínio Olá Olá lista.</span><span class="sxs-lookup"><span data-stu-id="cd931-216">Choose hello domain from hello list.</span></span>

   ![Domínio do Azure AD](media/active-directory-aadconnect-federation-management/AdditionalDomain4.PNG)

    <span data-ttu-id="cd931-218">Depois que você escolher o domínio Olá, Assistente Olá fornece informações adequadas sobre outras ações que Olá assistente será levar e Olá impacto da configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="cd931-218">After you choose hello domain, hello wizard provides you with appropriate information about further actions that hello wizard will take and hello impact of hello configuration.</span></span> <span data-ttu-id="cd931-219">Em alguns casos, se você selecionar um domínio que ainda não é verificado no AD do Azure, Olá fornecerá informações toohelp verificar domínio hello.</span><span class="sxs-lookup"><span data-stu-id="cd931-219">In some cases, if you select a domain that isn't yet verified in Azure AD, hello wizard provides you with information toohelp you verify hello domain.</span></span> <span data-ttu-id="cd931-220">Consulte [adicionar seu nome de domínio personalizado tooAzure do Active Directory](../active-directory-add-domain.md) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="cd931-220">See [Add your custom domain name tooAzure Active Directory](../active-directory-add-domain.md) for more details.</span></span>

5. <span data-ttu-id="cd931-221">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="cd931-221">Click **Next**.</span></span> <span data-ttu-id="cd931-222">Olá **tooconfigure pronto** página mostra Olá lista de ações do Azure AD Connect realizada.</span><span class="sxs-lookup"><span data-stu-id="cd931-222">hello **Ready tooconfigure** page shows hello list of actions that Azure AD Connect will perform.</span></span> <span data-ttu-id="cd931-223">Clique em **instalar** toofinish configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="cd931-223">Click **Install** toofinish hello configuration.</span></span>

   ![Tooconfigure pronto](media/active-directory-aadconnect-federation-management/AdditionalDomain5.PNG)

> [!NOTE]
> <span data-ttu-id="cd931-225">Os usuários de saudação adicionados domínio federado deve ser sincronizado antes que eles serão capazes de toologin tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="cd931-225">Users from hello added federated domain must be synchronized before they will be able toologin tooAzure AD.</span></span>

## <a name="ad-fs-customization"></a><span data-ttu-id="cd931-226">Personalização do AD FS</span><span class="sxs-lookup"><span data-stu-id="cd931-226">AD FS customization</span></span>
<span data-ttu-id="cd931-227">Olá seções a seguir fornecem detalhes sobre algumas das tarefas comuns de saudação que você possa ter tooperform quando você personalizar sua página de entrada do AD FS.</span><span class="sxs-lookup"><span data-stu-id="cd931-227">hello following sections provide details about some of hello common tasks that you might have tooperform when you customize your AD FS sign-in page.</span></span>

## <span data-ttu-id="cd931-228">Adicionar uma ilustração ou um logotipo da empresa personalizado <a name=customlogo></a></span><span class="sxs-lookup"><span data-stu-id="cd931-228">Add a custom company logo or illustration <a name=customlogo></a></span></span>
<span data-ttu-id="cd931-229">logotipo de saudação toochange da empresa de saudação que é exibido na Olá **entrar** página, use Olá seguindo a sintaxe e cmdlet do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cd931-229">toochange hello logo of hello company that's displayed on hello **Sign-in** page, use hello following Windows PowerShell cmdlet and syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="cd931-230">Olá recomendado dimensões para o logotipo de saudação são 260x35 96 dpi com um tamanho de arquivo maior do que 10 KB.</span><span class="sxs-lookup"><span data-stu-id="cd931-230">hello recommended dimensions for hello logo are 260 x 35 @ 96 dpi with a file size no greater than 10 KB.</span></span>

    Set-AdfsWebTheme -TargetName default -Logo @{path="c:\Contoso\logo.PNG"}

> [!NOTE]
> <span data-ttu-id="cd931-231">Olá *TargetName* parâmetro é obrigatório.</span><span class="sxs-lookup"><span data-stu-id="cd931-231">hello *TargetName* parameter is required.</span></span> <span data-ttu-id="cd931-232">o tema padrão Olá liberado com o AD FS é denominado Default.</span><span class="sxs-lookup"><span data-stu-id="cd931-232">hello default theme that's released with AD FS is named Default.</span></span>

## <span data-ttu-id="cd931-233">Adicionar uma descrição de entrada <a name=addsignindescription></a></span><span class="sxs-lookup"><span data-stu-id="cd931-233">Add a sign-in description <a name=addsignindescription></a></span></span>
<span data-ttu-id="cd931-234">tooadd um toohello de descrição de página de entrada **página de entrada**, use Olá seguindo a sintaxe e cmdlet do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cd931-234">tooadd a sign-in page description toohello **Sign-in page**, use hello following Windows PowerShell cmdlet and syntax.</span></span>

    Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in tooContoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>"

## <span data-ttu-id="cd931-235">Modificar regras de declaração do AD FS <a name=modclaims></a></span><span class="sxs-lookup"><span data-stu-id="cd931-235">Modify AD FS claim rules <a name=modclaims></a></span></span>
<span data-ttu-id="cd931-236">O AD FS oferece suporte a um idioma de declaração avançados que você pode usar regras de declaração toocreate personalizado.</span><span class="sxs-lookup"><span data-stu-id="cd931-236">AD FS supports a rich claim language that you can use toocreate custom claim rules.</span></span> <span data-ttu-id="cd931-237">Para obter mais informações, consulte [Olá a função de linguagem da regra de declaração de saudação](https://technet.microsoft.com/library/dd807118.aspx).</span><span class="sxs-lookup"><span data-stu-id="cd931-237">For more information, see [hello Role of hello Claim Rule Language](https://technet.microsoft.com/library/dd807118.aspx).</span></span>

<span data-ttu-id="cd931-238">Olá seções a seguir descrevem como você pode escrever regras personalizadas para alguns cenários que se relacionam tooAzure AD e Federação do AD FS.</span><span class="sxs-lookup"><span data-stu-id="cd931-238">hello following sections describe how you can write custom rules for some scenarios that relate tooAzure AD and AD FS federation.</span></span>

### <a name="immutable-id-conditional-on-a-value-being-present-in-hello-attribute"></a><span data-ttu-id="cd931-239">ID imutável condicional em um valor de estarem presentes no atributo Olá</span><span class="sxs-lookup"><span data-stu-id="cd931-239">Immutable ID conditional on a value being present in hello attribute</span></span>
<span data-ttu-id="cd931-240">Conexão do AD do Azure permite que você especifique um toobe atributo usado como uma âncora de origem quando objetos são sincronizados tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="cd931-240">Azure AD Connect lets you specify an attribute toobe used as a source anchor when objects are synced tooAzure AD.</span></span> <span data-ttu-id="cd931-241">Se o valor de saudação no atributo personalizado Olá não está vazio, convém tooissue uma declaração de ID imutável.</span><span class="sxs-lookup"><span data-stu-id="cd931-241">If hello value in hello custom attribute is not empty, you might want tooissue an immutable ID claim.</span></span>

<span data-ttu-id="cd931-242">Por exemplo, você pode selecionar **ms-ds-consistencyguid** como atributo de saudação de âncora de origem hello e problema **ImmutableID** como **ms-ds-consistencyguid** em maiusculas Olá o atributo tem um valor em relação a ela.</span><span class="sxs-lookup"><span data-stu-id="cd931-242">For example, you might select **ms-ds-consistencyguid** as hello attribute for hello source anchor and issue **ImmutableID** as **ms-ds-consistencyguid** in case hello attribute has a value against it.</span></span> <span data-ttu-id="cd931-243">Se não houver nenhum valor com atributo hello, emitir **objectGuid** como Olá ID imutável.</span><span class="sxs-lookup"><span data-stu-id="cd931-243">If there's no value against hello attribute, issue **objectGuid** as hello immutable ID.</span></span> <span data-ttu-id="cd931-244">Você pode construir o conjunto de saudação de regras de declaração personalizada conforme descrito em Olá seção a seguir.</span><span class="sxs-lookup"><span data-stu-id="cd931-244">You can construct hello set of custom claim rules as described in hello following section.</span></span>

<span data-ttu-id="cd931-245">**Regra 1: consultar atributos**</span><span class="sxs-lookup"><span data-stu-id="cd931-245">**Rule 1: Query attributes**</span></span>

    c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]
    => add(store = "Active Directory", types = ("http://contoso.com/ws/2016/02/identity/claims/objectguid", "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"), query = "; objectGuid,ms-ds-consistencyguid;{0}", param = c.Value);

<span data-ttu-id="cd931-246">Essa regra, você está consultando valores hello **ms-ds-consistencyguid** e **objectGuid** para o usuário de saudação do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cd931-246">In this rule, you're querying hello values of **ms-ds-consistencyguid** and **objectGuid** for hello user from Active Directory.</span></span> <span data-ttu-id="cd931-247">Alterar nome de armazenamento apropriado de tooan Olá repositório de nome em sua implantação do AD FS.</span><span class="sxs-lookup"><span data-stu-id="cd931-247">Change hello store name tooan appropriate store name in your AD FS deployment.</span></span> <span data-ttu-id="cd931-248">Também alterar Olá declarações tooa declarações adequadas tipo para a federação, conforme definido para **objectGuid** e **ms-ds-consistencyguid**.</span><span class="sxs-lookup"><span data-stu-id="cd931-248">Also change hello claims type tooa proper claims type for your federation, as defined for **objectGuid** and **ms-ds-consistencyguid**.</span></span>

<span data-ttu-id="cd931-249">Além disso, usando **adicionar** e não **problema**, evite a adição de um problema de saída para a entidade Olá e pode usar valores hello como valores intermediários.</span><span class="sxs-lookup"><span data-stu-id="cd931-249">Also, by using **add** and not **issue**, you avoid adding an outgoing issue for hello entity, and can use hello values as intermediate values.</span></span> <span data-ttu-id="cd931-250">Você emitir Olá declaração em uma regra posteriormente depois de estabelecer quais toouse valor como Olá ID imutável.</span><span class="sxs-lookup"><span data-stu-id="cd931-250">You will issue hello claim in a later rule after you establish which value toouse as hello immutable ID.</span></span>

<span data-ttu-id="cd931-251">**Regra 2: Verifique se o ms-ds-consistencyguid existe para o usuário Olá**</span><span class="sxs-lookup"><span data-stu-id="cd931-251">**Rule 2: Check if ms-ds-consistencyguid exists for hello user**</span></span>

    NOT EXISTS([Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"])
    => add(Type = "urn:anandmsft:tmp/idflag", Value = "useguid");

<span data-ttu-id="cd931-252">Essa regra define um sinalizador temporário chamado **idflag** que está definido muito**useguid** se não houver nenhum **ms-ds-consistencyguid** preenchido para usuário hello.</span><span class="sxs-lookup"><span data-stu-id="cd931-252">This rule defines a temporary flag called **idflag** that is set too**useguid** if there's no **ms-ds-consistencyguid** populated for hello user.</span></span> <span data-ttu-id="cd931-253">Olá lógica isso é o fato de saudação que o AD FS não permite declarações vazias.</span><span class="sxs-lookup"><span data-stu-id="cd931-253">hello logic behind this is hello fact that AD FS doesn't allow empty claims.</span></span> <span data-ttu-id="cd931-254">Portanto, quando você adicionar declarações http://contoso.com/ws/2016/02/identity/claims/objectguid e http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid na regra 1, você acabará com uma **msdsconsistencyguid** declaração somente se Olá valor é preenchido para usuário hello.</span><span class="sxs-lookup"><span data-stu-id="cd931-254">So when you add claims http://contoso.com/ws/2016/02/identity/claims/objectguid and http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid in Rule 1, you end up with an **msdsconsistencyguid** claim only if hello value is populated for hello user.</span></span> <span data-ttu-id="cd931-255">Se ele não estiver populado, o AD FS verá que ele terá um valor vazio e o descartará imediatamente.</span><span class="sxs-lookup"><span data-stu-id="cd931-255">If it isn't populated, AD FS sees that it will have an empty value and drops it immediately.</span></span> <span data-ttu-id="cd931-256">Todos os objetos terão **objectGuid**. Portanto, essa declaração sempre estará presente após a Regra 1 ser executada.</span><span class="sxs-lookup"><span data-stu-id="cd931-256">All objects will have **objectGuid**, so that claim will always be there after Rule 1 is executed.</span></span>

<span data-ttu-id="cd931-257">**Regra 3: emitir ms-ds-consistencyguid como a ID imutável, se estiver presente**</span><span class="sxs-lookup"><span data-stu-id="cd931-257">**Rule 3: Issue ms-ds-consistencyguid as immutable ID if it's present**</span></span>

    c:[Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c.Value);

<span data-ttu-id="cd931-258">Essa é uma verificação **Exist** implícita.</span><span class="sxs-lookup"><span data-stu-id="cd931-258">This is an implicit **Exist** check.</span></span> <span data-ttu-id="cd931-259">Se valor Olá Olá declaração, em seguida, emita que como Olá imutável identificação.</span><span class="sxs-lookup"><span data-stu-id="cd931-259">If hello value for hello claim exists, then issue that as hello immutable ID.</span></span> <span data-ttu-id="cd931-260">usa o exemplo anterior Olá Olá **nameidentifier** de declaração.</span><span class="sxs-lookup"><span data-stu-id="cd931-260">hello previous example uses hello **nameidentifier** claim.</span></span> <span data-ttu-id="cd931-261">Você terá toochange esse tipo de declaração adequado toohello de ID imutável Olá em seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="cd931-261">You'll have toochange this toohello appropriate claim type for hello immutable ID in your environment.</span></span>

<span data-ttu-id="cd931-262">**Regra 4: emitir o objectGuid como a ID imutável se ms-ds-consistencyGuid não estiver presente**</span><span class="sxs-lookup"><span data-stu-id="cd931-262">**Rule 4: Issue objectGuid as immutable ID if ms-ds-consistencyGuid is not present**</span></span>

    c1:[Type == "urn:anandmsft:tmp/idflag", Value =~ "useguid"]
    && c2:[Type == "http://contoso.com/ws/2016/02/identity/claims/objectguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c2.Value);

<span data-ttu-id="cd931-263">Nessa regra, simplesmente você está verificando o sinalizador temporário Olá **idflag**.</span><span class="sxs-lookup"><span data-stu-id="cd931-263">In this rule, you're simply checking hello temporary flag **idflag**.</span></span> <span data-ttu-id="cd931-264">Você decide se tooissue Olá declaração com base em seu valor.</span><span class="sxs-lookup"><span data-stu-id="cd931-264">You decide whether tooissue hello claim based on its value.</span></span>

> [!NOTE]
> <span data-ttu-id="cd931-265">sequência de saudação dessas regras é importante.</span><span class="sxs-lookup"><span data-stu-id="cd931-265">hello sequence of these rules is important.</span></span>

### <a name="sso-with-a-subdomain-upn"></a><span data-ttu-id="cd931-266">SSO com um subdomínio UPN</span><span class="sxs-lookup"><span data-stu-id="cd931-266">SSO with a subdomain UPN</span></span>
<span data-ttu-id="cd931-267">Você pode adicionar mais de um toobe domínio federado usando o Azure AD Connect, conforme descrito em [adicionar um novo domínio federado](active-directory-aadconnect-federation-management.md#addfeddomain).</span><span class="sxs-lookup"><span data-stu-id="cd931-267">You can add more than one domain toobe federated by using Azure AD Connect, as described in [Add a new federated domain](active-directory-aadconnect-federation-management.md#addfeddomain).</span></span> <span data-ttu-id="cd931-268">Você deve modificar Olá declaração de nome principal (UPN) do usuário para que hello emissor ID corresponde toohello domínio de raiz e não o subdomínio hello, porque o domínio de raiz federado Olá também aborda filhos hello.</span><span class="sxs-lookup"><span data-stu-id="cd931-268">You must modify hello user principal name (UPN) claim so that hello issuer ID corresponds toohello root domain and not hello subdomain, because hello federated root domain also covers hello child.</span></span>

<span data-ttu-id="cd931-269">Por padrão, Olá regra de declaração de emissor ID está definido como:</span><span class="sxs-lookup"><span data-stu-id="cd931-269">By default, hello claim rule for issuer ID is set as:</span></span>

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

![Declaração de ID do emissor padrão](media/active-directory-aadconnect-federation-management/issuer_id_default.png)

<span data-ttu-id="cd931-271">regra de padrão de saudação simplesmente usa o sufixo UPN hello e usa-o na declaração de ID do emissor de saudação.</span><span class="sxs-lookup"><span data-stu-id="cd931-271">hello default rule simply takes hello UPN suffix and uses it in hello issuer ID claim.</span></span> <span data-ttu-id="cd931-272">Por exemplo, John é um usuário em sub.contoso.com e contoso.com é federado com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cd931-272">For example, John is a user in sub.contoso.com, and contoso.com is federated with Azure AD.</span></span> <span data-ttu-id="cd931-273">Insere John john@sub.contoso.com como Olá nome de usuário ao entrar tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="cd931-273">John enters john@sub.contoso.com as hello username while signing in tooAzure AD.</span></span> <span data-ttu-id="cd931-274">regra de declaração de ID saudação padrão emissor no AD FS manipule em Olá maneira a seguir:</span><span class="sxs-lookup"><span data-stu-id="cd931-274">hello default issuer ID claim rule in AD FS handles it in hello following manner:</span></span>

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(john@sub.contoso.com, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

<span data-ttu-id="cd931-275">**Valor de declaração:**  http://sub.contoso.com/adfs/services/trust/</span><span class="sxs-lookup"><span data-stu-id="cd931-275">**Claim value:**  http://sub.contoso.com/adfs/services/trust/</span></span>

<span data-ttu-id="cd931-276">toohave somente Olá domínio raiz emissor Olá valor de declaração, alterar Olá declaração regra toomatch Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="cd931-276">toohave only hello root domain in hello issuer claim value, change hello claim rule toomatch hello following:</span></span>

    c:[Type == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “^((.*)([.|@]))?(?<domain>[^.]*[.].*)$”, “http://${domain}/adfs/services/trust/“));

## <a name="next-steps"></a><span data-ttu-id="cd931-277">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cd931-277">Next steps</span></span>
<span data-ttu-id="cd931-278">Saiba mais sobre as [opções de entrada do usuário](active-directory-aadconnect-user-signin.md).</span><span class="sxs-lookup"><span data-stu-id="cd931-278">Learn more about [user sign-in options](active-directory-aadconnect-user-signin.md).</span></span>
