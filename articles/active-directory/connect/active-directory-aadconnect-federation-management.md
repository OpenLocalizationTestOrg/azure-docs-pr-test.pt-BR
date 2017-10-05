---
title: "Gerenciamento e personalização dos Serviços de Federação do Active Directory com o Azure AD Connect | Microsoft Docs"
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
ms.openlocfilehash: 14f03542a6553c5bb697192828368ffe6b96441c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="manage-and-customize-active-directory-federation-services-by-using-azure-ad-connect"></a><span data-ttu-id="8e58d-104">Gerenciar e personalizar os Serviços de Federação do Active Directory usando o Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="8e58d-104">Manage and customize Active Directory Federation Services by using Azure AD Connect</span></span>
<span data-ttu-id="8e58d-105">Este artigo descreve como gerenciar e personalizar os Serviços de Federação do Active Directory (AD FS) usando o Azure Active Directory (Azure AD) Connect.</span><span class="sxs-lookup"><span data-stu-id="8e58d-105">This article describes how to manage and customize Active Directory Federation Services (AD FS) by using Azure Active Directory (Azure AD) Connect.</span></span> <span data-ttu-id="8e58d-106">Ele também inclui outras tarefas comuns do AD FS que você pode precisar realizar para obter uma configuração completa de um farm do AD FS.</span><span class="sxs-lookup"><span data-stu-id="8e58d-106">It also includes other common AD FS tasks that you might need to do for a complete configuration of an AD FS farm.</span></span>

| <span data-ttu-id="8e58d-107">Tópico</span><span class="sxs-lookup"><span data-stu-id="8e58d-107">Topic</span></span> | <span data-ttu-id="8e58d-108">O que ele abrange</span><span class="sxs-lookup"><span data-stu-id="8e58d-108">What it covers</span></span> |
|:--- |:--- |
| <span data-ttu-id="8e58d-109">**Gerenciar o AD FS**</span><span class="sxs-lookup"><span data-stu-id="8e58d-109">**Manage AD FS**</span></span> | |
| [<span data-ttu-id="8e58d-110">Reparar a relação de confiança</span><span class="sxs-lookup"><span data-stu-id="8e58d-110">Repair the trust</span></span>](#repairthetrust) |<span data-ttu-id="8e58d-111">Como reparar a confiança de federação com o Office 365.</span><span class="sxs-lookup"><span data-stu-id="8e58d-111">How to repair the federation trust with Office 365.</span></span> |
| [<span data-ttu-id="8e58d-112">Federar ao Azure AD usando uma ID de logon alternativa </span><span class="sxs-lookup"><span data-stu-id="8e58d-112">Federate with Azure AD using alternate login ID </span></span>](#alternateid) | <span data-ttu-id="8e58d-113">Configurar a federação usando uma ID de logon alternativa</span><span class="sxs-lookup"><span data-stu-id="8e58d-113">Configure federation using alternate login ID</span></span>  |
| [<span data-ttu-id="8e58d-114">Adicionar um servidor do AD FS</span><span class="sxs-lookup"><span data-stu-id="8e58d-114">Add an AD FS server</span></span>](#addadfsserver) |<span data-ttu-id="8e58d-115">Como expandir o farm do AD FS com um servidor adicional do AD FS.</span><span class="sxs-lookup"><span data-stu-id="8e58d-115">How to expand an AD FS farm with an additional AD FS server.</span></span> |
| [<span data-ttu-id="8e58d-116">Adicionar um Servidor Proxy de Aplicativo Web do AD FS</span><span class="sxs-lookup"><span data-stu-id="8e58d-116">Add an AD FS Web Application Proxy server</span></span>](#addwapserver) |<span data-ttu-id="8e58d-117">Como expandir um farm do AD FS com um servidor WAP (Proxy de Aplicativo Web) adicional.</span><span class="sxs-lookup"><span data-stu-id="8e58d-117">How to expand an AD FS farm with an additional Web Application Proxy (WAP) server.</span></span> |
| [<span data-ttu-id="8e58d-118">Adicionar um domínio federado</span><span class="sxs-lookup"><span data-stu-id="8e58d-118">Add a federated domain</span></span>](#addfeddomain) |<span data-ttu-id="8e58d-119">Como adicionar um domínio federado.</span><span class="sxs-lookup"><span data-stu-id="8e58d-119">How to add a federated domain.</span></span> |
| [<span data-ttu-id="8e58d-120">Atualizar o certificado SSL</span><span class="sxs-lookup"><span data-stu-id="8e58d-120">Update the SSL certificate</span></span>](active-directory-aadconnectfed-ssl-update.md)| <span data-ttu-id="8e58d-121">Como atualizar o certificado SSL para um farm do AD FS.</span><span class="sxs-lookup"><span data-stu-id="8e58d-121">How to update the SSL certificate for an AD FS farm.</span></span> |
| <span data-ttu-id="8e58d-122">**Personalizar o AD FS**</span><span class="sxs-lookup"><span data-stu-id="8e58d-122">**Customize AD FS**</span></span> | |
| [<span data-ttu-id="8e58d-123">Adicionar uma ilustração ou um logotipo da empresa personalizado</span><span class="sxs-lookup"><span data-stu-id="8e58d-123">Add a custom company logo or illustration</span></span>](#customlogo) |<span data-ttu-id="8e58d-124">Como personalizar uma página de entrada do AD FS com um logotipo e uma ilustração da empresa.</span><span class="sxs-lookup"><span data-stu-id="8e58d-124">How to customize an AD FS sign-in page with a company logo and illustration.</span></span> |
| [<span data-ttu-id="8e58d-125">Adicionar uma descrição de entrada</span><span class="sxs-lookup"><span data-stu-id="8e58d-125">Add a sign-in description</span></span>](#addsignindescription) |<span data-ttu-id="8e58d-126">Como adicionar uma descrição de página de entrada.</span><span class="sxs-lookup"><span data-stu-id="8e58d-126">How to add a sign-in page description.</span></span> |
| [<span data-ttu-id="8e58d-127">Modificar regras de declaração do AD FS</span><span class="sxs-lookup"><span data-stu-id="8e58d-127">Modify AD FS claim rules</span></span>](#modclaims) |<span data-ttu-id="8e58d-128">Como modificar declarações do AD FS para vários cenários de federação.</span><span class="sxs-lookup"><span data-stu-id="8e58d-128">How to modify AD FS claims for various federation scenarios.</span></span> |

## <a name="manage-ad-fs"></a><span data-ttu-id="8e58d-129">Gerenciar o AD FS</span><span class="sxs-lookup"><span data-stu-id="8e58d-129">Manage AD FS</span></span>
<span data-ttu-id="8e58d-130">Você pode realizar várias tarefas relacionadas ao AD FS no Azure AD com mínima intervenção do usuário usando o assistente do Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="8e58d-130">You can perform various AD FS-related tasks in Azure AD Connect with minimal user intervention by using the Azure AD Connect wizard.</span></span> <span data-ttu-id="8e58d-131">Após instalar o Azure AD Connect executando o assistente, você pode executar o assistente novamente para realizar tarefas adicionais.</span><span class="sxs-lookup"><span data-stu-id="8e58d-131">After you've finished installing Azure AD Connect by running the wizard, you can run the wizard again to perform additional tasks.</span></span>

## <span data-ttu-id="8e58d-132">Reparar a relação de confiança <a name=repairthetrust></a></span><span class="sxs-lookup"><span data-stu-id="8e58d-132">Repair the trust <a name=repairthetrust></a></span></span>
<span data-ttu-id="8e58d-133">Você pode usar o Azure AD Connect para verificar a integridade atual da confiança do AD FS e Azure AD e tomar as medidas apropriadas para reparar a relação de confiança.</span><span class="sxs-lookup"><span data-stu-id="8e58d-133">You can use Azure AD Connect to check the current health of the AD FS and Azure AD trust and take appropriate actions to repair the trust.</span></span> <span data-ttu-id="8e58d-134">Siga estas etapas para reparar a confiança do Azure AD e AD FS.</span><span class="sxs-lookup"><span data-stu-id="8e58d-134">Follow these steps to repair your Azure AD and AD FS trust.</span></span>

1. <span data-ttu-id="8e58d-135">Selecione **Reparar a relação de confiança do AAD e do ADFS** na lista de tarefas adicionais.</span><span class="sxs-lookup"><span data-stu-id="8e58d-135">Select **Repair AAD and ADFS Trust** from the list of additional tasks.</span></span>
   <span data-ttu-id="8e58d-136">![Reparar a relação de confiança do AAD e do ADFS](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)</span><span class="sxs-lookup"><span data-stu-id="8e58d-136">![Repair AAD and ADFS Trust](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)</span></span>

2. <span data-ttu-id="8e58d-137">Na página **Conectar ao Azure AD**, forneça suas credenciais de administrador global do Azure AD e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="8e58d-137">On the **Connect to Azure AD** page, provide your global administrator credentials for Azure AD, and click **Next**.</span></span>
   <span data-ttu-id="8e58d-138">![Conecte-se ao AD do Azure](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)</span><span class="sxs-lookup"><span data-stu-id="8e58d-138">![Connect to Azure AD](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)</span></span>

3. <span data-ttu-id="8e58d-139">Na página **Credenciais de acesso remoto** , digite as credenciais de administrador de domínio.</span><span class="sxs-lookup"><span data-stu-id="8e58d-139">On the **Remote access credentials** page, enter the credentials for the domain administrator.</span></span>

   ![Credenciais de acesso remoto](media/active-directory-aadconnect-federation-management/RepairADTrust3.PNG)

    <span data-ttu-id="8e58d-141">Depois que você clicar em **Avançar**, o Azure AD Connect verificará a integridade do certificado e mostrará eventuais problemas.</span><span class="sxs-lookup"><span data-stu-id="8e58d-141">After you click **Next**, Azure AD Connect checks for certificate health and shows any issues.</span></span>

    ![Estado de certificados](media/active-directory-aadconnect-federation-management/RepairADTrust4.PNG)

    <span data-ttu-id="8e58d-143">A página **Pronto para configurar** mostra a lista de ações que serão executadas para reparar a confiança.</span><span class="sxs-lookup"><span data-stu-id="8e58d-143">The **Ready to configure** page shows the list of actions that will be performed to repair the trust.</span></span>

    ![Pronto para configurar](media/active-directory-aadconnect-federation-management/RepairADTrust5.PNG)

4. <span data-ttu-id="8e58d-145">Clique em **Instalar** para reparar a relação de confiança.</span><span class="sxs-lookup"><span data-stu-id="8e58d-145">Click **Install** to repair the trust.</span></span>

> [!NOTE]
> <span data-ttu-id="8e58d-146">O Azure AD Connect só pode reparar ou agir em relação a certificados autoassinados.</span><span class="sxs-lookup"><span data-stu-id="8e58d-146">Azure AD Connect can only repair or act on certificates that are self-signed.</span></span> <span data-ttu-id="8e58d-147">O Azure AD Connect não pode reparar certificados de terceiros.</span><span class="sxs-lookup"><span data-stu-id="8e58d-147">Azure AD Connect can't repair third-party certificates.</span></span>

## <span data-ttu-id="8e58d-148">Federar ao Azure AD usando uma AlternateID <a name=alternateid></a></span><span class="sxs-lookup"><span data-stu-id="8e58d-148">Federate with Azure AD using AlternateID <a name=alternateid></a></span></span>
<span data-ttu-id="8e58d-149">É recomendável que o nome UPN local e o nome UPN na nuvem sejam mantidos iguais.</span><span class="sxs-lookup"><span data-stu-id="8e58d-149">It is recommended that the on-premises User Principal Name(UPN) and the cloud User Principal Name are kept the same.</span></span> <span data-ttu-id="8e58d-150">Se o UPN local usar um domínio não roteável (por exemplo,</span><span class="sxs-lookup"><span data-stu-id="8e58d-150">If the on-premises UPN uses a non-routable domain (ex.</span></span> <span data-ttu-id="8e58d-151">Contoso.local) ou não puder ser alterado devido a dependências do aplicativo local, recomendamos configurar uma ID de logon alternativa.</span><span class="sxs-lookup"><span data-stu-id="8e58d-151">Contoso.local) or cannot be changed due to local application dependencies, we recommend setting up alternate login ID.</span></span> <span data-ttu-id="8e58d-152">A ID de logon alternativa permite configurar uma experiência de logon na qual os usuários podem se conectar com um atributo que não seja o UPN, como o email.</span><span class="sxs-lookup"><span data-stu-id="8e58d-152">Alternate login ID allows you to configure a sign-in experience where users can sign in with an attribute other than their UPN, such as mail.</span></span> <span data-ttu-id="8e58d-153">A opção para o nome UPN no Azure AD Connect usa como padrão o atributo userPrincipalName no Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8e58d-153">The choice for User Principal Name in Azure AD Connect defaults to the userPrincipalName attribute in Active Directory.</span></span> <span data-ttu-id="8e58d-154">Se você escolher qualquer outro atributo para o nome UPN e estiver federando com o uso do AD FS, o Azure AD Connect configurará o AD FS para a ID de logon alternativa.</span><span class="sxs-lookup"><span data-stu-id="8e58d-154">If you choose any other attribute for User Principal Name and are federating using AD FS, then Azure AD Connect will configure AD FS for alternate login ID.</span></span> <span data-ttu-id="8e58d-155">Um exemplo de escolha de um atributo diferente para o nome UPN é mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="8e58d-155">An example of choosing a different attribute for User Principal Name is shown below:</span></span>

![Seleção de atributo de ID alternativa](media/active-directory-aadconnect-federation-management/attributeselection.png)

<span data-ttu-id="8e58d-157">A configuração da ID de logon alternativa do AD FS consiste em duas etapas principais:</span><span class="sxs-lookup"><span data-stu-id="8e58d-157">Configuring alternate login ID for AD FS consists of two main steps:</span></span>
1. <span data-ttu-id="8e58d-158">**Configurar o conjunto certo de declarações de emissão**: as regras de declaração de emissão no objeto de confiança de terceira parte confiável do Azure AD são modificadas para usar o atributo UserPrincipalName selecionado como a ID alternativa do usuário.</span><span class="sxs-lookup"><span data-stu-id="8e58d-158">**Configure the right set of issuance claims**: The issuance claim rules in the Azure AD relying party trust are modified to use the selected UserPrincipalName attribute as the alternate ID of the user.</span></span>
2. <span data-ttu-id="8e58d-159">**Habilitar a ID de logon alternativa na configuração do AD FS**: a configuração do AD FS é atualizada, de forma que o AD FS possa consultar usuários nas florestas apropriadas usando a ID alternativa.</span><span class="sxs-lookup"><span data-stu-id="8e58d-159">**Enable alternate login ID in the AD FS configuration**: The AD FS configuration is updated so that AD FS can look up users in the appropriate forests using the alternate ID.</span></span> <span data-ttu-id="8e58d-160">Há suporte para essa configuração no AD FS no Windows Server 2012 R2 (com KB2919355) ou posterior.</span><span class="sxs-lookup"><span data-stu-id="8e58d-160">This configuration is supported for AD FS on Windows Server 2012 R2 (with KB2919355) or later.</span></span> <span data-ttu-id="8e58d-161">Se os servidores do AD FS forem 2012 R2, o Azure AD Connect verificará a presença do KB obrigatório.</span><span class="sxs-lookup"><span data-stu-id="8e58d-161">If the AD FS servers are 2012 R2, Azure AD Connect checks for the presence of the required KB.</span></span> <span data-ttu-id="8e58d-162">Se o KB não for detectado, um aviso será exibido após a conclusão da configuração, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="8e58d-162">If the KB is not detected, a warning will be displayed after configuration completes, as shown below:</span></span>

    ![Aviso de ausência de KB no 2012R2](media/active-directory-aadconnect-federation-management/kbwarning.png)

    <span data-ttu-id="8e58d-164">Para corrigir a configuração no caso de um KB ausente, instale o [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) obrigatório e repare a relação de confiança usando [Reparar relação de confiança entre o AAD e o AD FS](#repairthetrust).</span><span class="sxs-lookup"><span data-stu-id="8e58d-164">To rectify the configuration in case of missing KB, install the required [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) and then repair the trust using [Repair AAD and AD FS Trust](#repairthetrust).</span></span>

> [!NOTE]
> <span data-ttu-id="8e58d-165">Para obter mais informações sobre alternateID e as etapas para configurá-la manualmente, leia [Configurando a ID de logon alternativa](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)</span><span class="sxs-lookup"><span data-stu-id="8e58d-165">For more information on alternateID and steps to manually configure, read [Configuring Alternate Login ID](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)</span></span>

## <span data-ttu-id="8e58d-166">Adicionar um servidor do AD FS <a name=addadfsserver></a></span><span class="sxs-lookup"><span data-stu-id="8e58d-166">Add an AD FS server <a name=addadfsserver></a></span></span>

> [!NOTE]
> <span data-ttu-id="8e58d-167">Para adicionar um servidor do AD FS, o Azure AD Connect requer o arquivo de certificado PFX.</span><span class="sxs-lookup"><span data-stu-id="8e58d-167">To add an AD FS server, Azure AD Connect requires the PFX certificate.</span></span> <span data-ttu-id="8e58d-168">Portanto, você só poderá executar essa operação se tiver configurado o farm do AD FS usando o Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="8e58d-168">Therefore, you can perform this operation only if you configured the AD FS farm by using Azure AD Connect.</span></span>

1. <span data-ttu-id="8e58d-169">Selecione **Implantar um Servidor de Federação adicional** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="8e58d-169">Select **Deploy an additional Federation Server**, and click **Next**.</span></span>

   ![Servidor de federação adicional](media/active-directory-aadconnect-federation-management/AddNewADFSServer1.PNG)

2. <span data-ttu-id="8e58d-171">Na página **Conectar ao Azure AD**, digite suas credenciais de administrador global do Azure AD e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="8e58d-171">On the **Connect to Azure AD** page, enter your global administrator credentials for Azure AD, and click **Next**.</span></span>

   ![Conecte-se ao AD do Azure](media/active-directory-aadconnect-federation-management/AddNewADFSServer2.PNG)

3. <span data-ttu-id="8e58d-173">Forneça as credenciais de administrador de domínio.</span><span class="sxs-lookup"><span data-stu-id="8e58d-173">Provide the domain administrator credentials.</span></span>

   ![Credenciais de administrador de domínio](media/active-directory-aadconnect-federation-management/AddNewADFSServer3.PNG)

4. <span data-ttu-id="8e58d-175">O Azure AD Connect solicita a senha do arquivo PFX que você forneceu ao configurar o novo farm do AD FS com o Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="8e58d-175">Azure AD Connect asks for the password of the PFX file that you provided while configuring your new AD FS farm with Azure AD Connect.</span></span> <span data-ttu-id="8e58d-176">Clique em **Digitar Senha** para fornecer a senha para o arquivo PFX.</span><span class="sxs-lookup"><span data-stu-id="8e58d-176">Click **Enter Password** to provide the password for the PFX file.</span></span>

   ![Senha de certificado](media/active-directory-aadconnect-federation-management/AddNewADFSServer4.PNG)

    ![Especificar certificado SSL](media/active-directory-aadconnect-federation-management/AddNewADFSServer5.PNG)

5. <span data-ttu-id="8e58d-179">Na página **Servidores do AD FS** , insira o nome do servidor ou o endereço IP a ser adicionado ao farm do AD FS.</span><span class="sxs-lookup"><span data-stu-id="8e58d-179">On the **AD FS Servers** page, enter the server name or IP address to be added to the AD FS farm.</span></span>

   ![Servidores do AD FS](media/active-directory-aadconnect-federation-management/AddNewADFSServer6.PNG)

6. <span data-ttu-id="8e58d-181">Clique em **Avançar** e passe pela página **Configurar** final.</span><span class="sxs-lookup"><span data-stu-id="8e58d-181">Click **Next**, and go through the final **Configure** page.</span></span> <span data-ttu-id="8e58d-182">Após o Azure AD Connect terminar de adicionar os servidores no farm do AD FS, você terá a opção de verificar a conectividade.</span><span class="sxs-lookup"><span data-stu-id="8e58d-182">After Azure AD Connect has finished adding the servers to the AD FS farm, you will be given the option to verify the connectivity.</span></span>

   ![Pronto para configurar](media/active-directory-aadconnect-federation-management/AddNewADFSServer7.PNG)

    ![Instalação concluída](media/active-directory-aadconnect-federation-management/AddNewADFSServer8.PNG)

## <span data-ttu-id="8e58d-185">Adicionar um servidor WAP do AD FS <a name=addwapserver></a></span><span class="sxs-lookup"><span data-stu-id="8e58d-185">Add an AD FS WAP server <a name=addwapserver></a></span></span>

> [!NOTE]
> <span data-ttu-id="8e58d-186">Para adicionar um servidor WAP, o Azure AD Connect requer o arquivo de certificado PFX.</span><span class="sxs-lookup"><span data-stu-id="8e58d-186">To add a WAP server, Azure AD Connect requires the PFX certificate.</span></span> <span data-ttu-id="8e58d-187">Portanto, você só poderá executar essa operação se tiver configurado o farm do AD FS usando o Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="8e58d-187">Therefore, you can only perform this operation if you configured the AD FS farm by using Azure AD Connect.</span></span>

1. <span data-ttu-id="8e58d-188">Selecione **Implantar Proxy de Aplicativo Web** na lista de tarefas disponíveis.</span><span class="sxs-lookup"><span data-stu-id="8e58d-188">Select **Deploy Web Application Proxy** from the list of available tasks.</span></span>

   ![Implantar o proxy de aplicativo Web](media/active-directory-aadconnect-federation-management/WapServer1.PNG)

2. <span data-ttu-id="8e58d-190">Forneça as credenciais de administrador global do Azure.</span><span class="sxs-lookup"><span data-stu-id="8e58d-190">Provide the Azure global administrator credentials.</span></span>

   ![Conecte-se ao AD do Azure](media/active-directory-aadconnect-federation-management/wapserver2.PNG)

3. <span data-ttu-id="8e58d-192">Na página **Especificar certificado SSL**, forneça a senha para o arquivo PFX que você forneceu ao configurar o farm do AD FS com o Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="8e58d-192">On the **Specify SSL certificate** page, provide the password for the PFX file that you provided when you configured the AD FS farm with Azure AD Connect.</span></span>
   <span data-ttu-id="8e58d-193">![Senha de certificado](media/active-directory-aadconnect-federation-management/WapServer3.PNG)</span><span class="sxs-lookup"><span data-stu-id="8e58d-193">![Certificate password](media/active-directory-aadconnect-federation-management/WapServer3.PNG)</span></span>

    ![Especificar certificado SSL](media/active-directory-aadconnect-federation-management/WapServer4.PNG)

4. <span data-ttu-id="8e58d-195">Adicione o servidor a ser adicionado como um servidor WAP.</span><span class="sxs-lookup"><span data-stu-id="8e58d-195">Add the server to be added as a WAP server.</span></span> <span data-ttu-id="8e58d-196">Já que o servidor WAP pode não estar ingressado no domínio, o assistente solicita as credenciais administrativas para o servidor que está sendo adicionado.</span><span class="sxs-lookup"><span data-stu-id="8e58d-196">Because the WAP server might not be joined to the domain, the wizard asks for administrative credentials to the server being added.</span></span>

   ![Credenciais administrativas de servidor](media/active-directory-aadconnect-federation-management/WapServer5.PNG)

5. <span data-ttu-id="8e58d-198">Na página **Credenciais de confiança de proxy** , forneça as credenciais administrativas para configurar a confiança de proxy e acessar o servidor primário no farm do AD FS.</span><span class="sxs-lookup"><span data-stu-id="8e58d-198">On the **Proxy trust credentials** page, provide administrative credentials to configure the proxy trust and access the primary server in the AD FS farm.</span></span>

   ![Credenciais de confiança de proxy](media/active-directory-aadconnect-federation-management/WapServer6.PNG)

6. <span data-ttu-id="8e58d-200">Na página **Pronto para configurar** , o assistente mostra a lista de ações que serão executadas.</span><span class="sxs-lookup"><span data-stu-id="8e58d-200">On the **Ready to configure** page, the wizard shows the list of actions that will be performed.</span></span>

   ![Pronto para configurar](media/active-directory-aadconnect-federation-management/WapServer7.PNG)

7. <span data-ttu-id="8e58d-202">Clique em **Instalar** para concluir a configuração.</span><span class="sxs-lookup"><span data-stu-id="8e58d-202">Click **Install** to finish the configuration.</span></span> <span data-ttu-id="8e58d-203">Depois que a configuração for concluída, o assistente lhe dará a opção para verificar a conectividade com os servidores.</span><span class="sxs-lookup"><span data-stu-id="8e58d-203">After the configuration is complete, the wizard gives you the option to verify the connectivity to the servers.</span></span> <span data-ttu-id="8e58d-204">Clique em **Verificar** para verificar a conectividade.</span><span class="sxs-lookup"><span data-stu-id="8e58d-204">Click **Verify** to check connectivity.</span></span>

   ![Instalação concluída](media/active-directory-aadconnect-federation-management/WapServer8.PNG)

## <span data-ttu-id="8e58d-206">Adicionar um domínio federado <a name=addfeddomain></a></span><span class="sxs-lookup"><span data-stu-id="8e58d-206">Add a federated domain <a name=addfeddomain></a></span></span>

<span data-ttu-id="8e58d-207">É fácil adicionar um domínio a ser federado com o Azure AD usando o Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="8e58d-207">It's easy to add a domain to be federated with Azure AD by using Azure AD Connect.</span></span> <span data-ttu-id="8e58d-208">O Azure AD Connect adiciona o domínio para federação e modifica as regras de declaração para refletir corretamente o emissor quando você tem vários domínios federados com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e58d-208">Azure AD Connect adds the domain for federation and modifies the claim rules to correctly reflect the issuer when you have multiple domains federated with Azure AD.</span></span>

1. <span data-ttu-id="8e58d-209">Para adicionar um domínio federado, selecione a tarefa **Adicionar um domínio do Azure AD adicional**.</span><span class="sxs-lookup"><span data-stu-id="8e58d-209">To add a federated domain, select the task **Add an additional Azure AD domain**.</span></span>

   ![Domínio do Azure AD adicional](media/active-directory-aadconnect-federation-management/AdditionalDomain1.PNG)

2. <span data-ttu-id="8e58d-211">Na próxima página do assistente, forneça as credenciais de administrador global do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e58d-211">On the next page of the wizard, provide the global administrator credentials for Azure AD.</span></span>

   ![Conecte-se ao AD do Azure](media/active-directory-aadconnect-federation-management/AdditionalDomain2.PNG)

3. <span data-ttu-id="8e58d-213">Na página **Credenciais de acesso remoto** , forneça as credenciais do administrador de domínio.</span><span class="sxs-lookup"><span data-stu-id="8e58d-213">On the **Remote access credentials** page, provide the domain administrator credentials.</span></span>

   ![Credenciais de acesso remoto](media/active-directory-aadconnect-federation-management/additionaldomain3.PNG)

4. <span data-ttu-id="8e58d-215">Na próxima página, o assistente fornece uma lista de domínios do Azure AD com os quais você pode federar seu diretório local.</span><span class="sxs-lookup"><span data-stu-id="8e58d-215">On the next page, the wizard provides a list of Azure AD domains that you can federate your on-premises directory with.</span></span> <span data-ttu-id="8e58d-216">Escolha o domínio na lista.</span><span class="sxs-lookup"><span data-stu-id="8e58d-216">Choose the domain from the list.</span></span>

   ![Domínio do Azure AD](media/active-directory-aadconnect-federation-management/AdditionalDomain4.PNG)

    <span data-ttu-id="8e58d-218">Depois de escolher o domínio, o assistente fornece as informações apropriadas sobre outras ações que o assistente realizará e o impacto da configuração.</span><span class="sxs-lookup"><span data-stu-id="8e58d-218">After you choose the domain, the wizard provides you with appropriate information about further actions that the wizard will take and the impact of the configuration.</span></span> <span data-ttu-id="8e58d-219">Em alguns casos, se você selecionar um domínio que ainda não seja verificado no Azure AD, o assistente fornecerá informações para ajudá-lo a verificar o domínio.</span><span class="sxs-lookup"><span data-stu-id="8e58d-219">In some cases, if you select a domain that isn't yet verified in Azure AD, the wizard provides you with information to help you verify the domain.</span></span> <span data-ttu-id="8e58d-220">Confira [Adicionar seu nome de domínio personalizado ao Azure Active Directory](../active-directory-add-domain.md) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="8e58d-220">See [Add your custom domain name to Azure Active Directory](../active-directory-add-domain.md) for more details.</span></span>

5. <span data-ttu-id="8e58d-221">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="8e58d-221">Click **Next**.</span></span> <span data-ttu-id="8e58d-222">A página **Pronto para configurar** mostra a lista de ações que o Azure AD Connect executará.</span><span class="sxs-lookup"><span data-stu-id="8e58d-222">The **Ready to configure** page shows the list of actions that Azure AD Connect will perform.</span></span> <span data-ttu-id="8e58d-223">Clique em **Instalar** para concluir a configuração.</span><span class="sxs-lookup"><span data-stu-id="8e58d-223">Click **Install** to finish the configuration.</span></span>

   ![Pronto para configurar](media/active-directory-aadconnect-federation-management/AdditionalDomain5.PNG)

> [!NOTE]
> <span data-ttu-id="8e58d-225">Os usuários do domínio federado adicionado devem ser sincronizados antes que eles possam fazer logon no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e58d-225">Users from the added federated domain must be synchronized before they will be able to login to Azure AD.</span></span>

## <a name="ad-fs-customization"></a><span data-ttu-id="8e58d-226">Personalização do AD FS</span><span class="sxs-lookup"><span data-stu-id="8e58d-226">AD FS customization</span></span>
<span data-ttu-id="8e58d-227">As seções a seguir fornecem detalhes sobre algumas das tarefas comuns que talvez você precise executar ao personalizar a página de entrada do AD FS.</span><span class="sxs-lookup"><span data-stu-id="8e58d-227">The following sections provide details about some of the common tasks that you might have to perform when you customize your AD FS sign-in page.</span></span>

## <span data-ttu-id="8e58d-228">Adicionar uma ilustração ou um logotipo da empresa personalizado <a name=customlogo></a></span><span class="sxs-lookup"><span data-stu-id="8e58d-228">Add a custom company logo or illustration <a name=customlogo></a></span></span>
<span data-ttu-id="8e58d-229">Para alterar o logotipo da empresa que é exibido na página de **Entrada**, use o cmdlet e sintaxe do Windows PowerShell a seguir.</span><span class="sxs-lookup"><span data-stu-id="8e58d-229">To change the logo of the company that's displayed on the **Sign-in** page, use the following Windows PowerShell cmdlet and syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="8e58d-230">As dimensões recomendadas para o logotipo são 260x35 a 96 dpi com um tamanho do arquivo máximo de 10 KB.</span><span class="sxs-lookup"><span data-stu-id="8e58d-230">The recommended dimensions for the logo are 260 x 35 @ 96 dpi with a file size no greater than 10 KB.</span></span>

    Set-AdfsWebTheme -TargetName default -Logo @{path="c:\Contoso\logo.PNG"}

> [!NOTE]
> <span data-ttu-id="8e58d-231">O parâmetro *TargetName* é obrigatório.</span><span class="sxs-lookup"><span data-stu-id="8e58d-231">The *TargetName* parameter is required.</span></span> <span data-ttu-id="8e58d-232">O tema padrão liberado com o AD FS é denominado Default.</span><span class="sxs-lookup"><span data-stu-id="8e58d-232">The default theme that's released with AD FS is named Default.</span></span>

## <span data-ttu-id="8e58d-233">Adicionar uma descrição de entrada <a name=addsignindescription></a></span><span class="sxs-lookup"><span data-stu-id="8e58d-233">Add a sign-in description <a name=addsignindescription></a></span></span>
<span data-ttu-id="8e58d-234">Para adicionar uma descrição à página de **Entrada**, use o seguinte cmdlet e sintaxe do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8e58d-234">To add a sign-in page description to the **Sign-in page**, use the following Windows PowerShell cmdlet and syntax.</span></span>

    Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in to Contoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>"

## <span data-ttu-id="8e58d-235">Modificar regras de declaração do AD FS <a name=modclaims></a></span><span class="sxs-lookup"><span data-stu-id="8e58d-235">Modify AD FS claim rules <a name=modclaims></a></span></span>
<span data-ttu-id="8e58d-236">O AD FS dá suporte a uma linguagem de declarações avançada que você pode usar para criar regras de declaração personalizada.</span><span class="sxs-lookup"><span data-stu-id="8e58d-236">AD FS supports a rich claim language that you can use to create custom claim rules.</span></span> <span data-ttu-id="8e58d-237">Para obter mais informações, confira [A função da linguagem de regras de declaração](https://technet.microsoft.com/library/dd807118.aspx).</span><span class="sxs-lookup"><span data-stu-id="8e58d-237">For more information, see [The Role of the Claim Rule Language](https://technet.microsoft.com/library/dd807118.aspx).</span></span>

<span data-ttu-id="8e58d-238">As seções a seguir descrevem como você pode escrever regras personalizadas para alguns cenários relacionadas à federação do Azure AD e AD FS.</span><span class="sxs-lookup"><span data-stu-id="8e58d-238">The following sections describe how you can write custom rules for some scenarios that relate to Azure AD and AD FS federation.</span></span>

### <a name="immutable-id-conditional-on-a-value-being-present-in-the-attribute"></a><span data-ttu-id="8e58d-239">Condicional de ID imutável em um valor presente no atributo</span><span class="sxs-lookup"><span data-stu-id="8e58d-239">Immutable ID conditional on a value being present in the attribute</span></span>
<span data-ttu-id="8e58d-240">O Azure AD Connect permite que você especifique um atributo a ser usado como âncora de origem quando objetos são sincronizados ao Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e58d-240">Azure AD Connect lets you specify an attribute to be used as a source anchor when objects are synced to Azure AD.</span></span> <span data-ttu-id="8e58d-241">Se o valor do atributo personalizado não estiver vazio, convém emitir uma declaração de ID imutável.</span><span class="sxs-lookup"><span data-stu-id="8e58d-241">If the value in the custom attribute is not empty, you might want to issue an immutable ID claim.</span></span>

<span data-ttu-id="8e58d-242">Por exemplo, você pode selecionar **ms-ds-consistencyguid** como o atributo de âncora de origem e talvez deseje emitir **ImmutableID** como **ms-ds-consistencyguid**, caso o atributo tenha um valor em relação a ele.</span><span class="sxs-lookup"><span data-stu-id="8e58d-242">For example, you might select **ms-ds-consistencyguid** as the attribute for the source anchor and issue **ImmutableID** as **ms-ds-consistencyguid** in case the attribute has a value against it.</span></span> <span data-ttu-id="8e58d-243">Se não houver um valor com o atributo, atribua **objectGuid** como a ID imutável.</span><span class="sxs-lookup"><span data-stu-id="8e58d-243">If there's no value against the attribute, issue **objectGuid** as the immutable ID.</span></span> <span data-ttu-id="8e58d-244">Você pode construir o conjunto de regras de declaração personalizada, conforme descrito na seção a seguir.</span><span class="sxs-lookup"><span data-stu-id="8e58d-244">You can construct the set of custom claim rules as described in the following section.</span></span>

<span data-ttu-id="8e58d-245">**Regra 1: consultar atributos**</span><span class="sxs-lookup"><span data-stu-id="8e58d-245">**Rule 1: Query attributes**</span></span>

    c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]
    => add(store = "Active Directory", types = ("http://contoso.com/ws/2016/02/identity/claims/objectguid", "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"), query = "; objectGuid,ms-ds-consistencyguid;{0}", param = c.Value);

<span data-ttu-id="8e58d-246">Nessa regra, você simplesmente consulta os valores de **ms-ds-consistencyguid** e **objectGuid** do usuário do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8e58d-246">In this rule, you're querying the values of **ms-ds-consistencyguid** and **objectGuid** for the user from Active Directory.</span></span> <span data-ttu-id="8e58d-247">Altere o nome do repositório para um nome de armazenamento apropriado em sua implantação do AD FS.</span><span class="sxs-lookup"><span data-stu-id="8e58d-247">Change the store name to an appropriate store name in your AD FS deployment.</span></span> <span data-ttu-id="8e58d-248">Também altere o tipo de declarações para um tipo apropriado para a federação, conforme definido para **objectGuid** e **ms-ds-consistencyguid**.</span><span class="sxs-lookup"><span data-stu-id="8e58d-248">Also change the claims type to a proper claims type for your federation, as defined for **objectGuid** and **ms-ds-consistencyguid**.</span></span>

<span data-ttu-id="8e58d-249">Além disso, usando **add** e não **issue**, você evita adicionar uma emissão de saída à entidade e pode usar os valores como valores intermediários.</span><span class="sxs-lookup"><span data-stu-id="8e58d-249">Also, by using **add** and not **issue**, you avoid adding an outgoing issue for the entity, and can use the values as intermediate values.</span></span> <span data-ttu-id="8e58d-250">Você emitirá a declaração em uma regra mais recente depois de estabelecer o valor a ser usado como a ID imutável.</span><span class="sxs-lookup"><span data-stu-id="8e58d-250">You will issue the claim in a later rule after you establish which value to use as the immutable ID.</span></span>

<span data-ttu-id="8e58d-251">**Regra 2: verificar se ms-ds-consistencyguid existe para o usuário**</span><span class="sxs-lookup"><span data-stu-id="8e58d-251">**Rule 2: Check if ms-ds-consistencyguid exists for the user**</span></span>

    NOT EXISTS([Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"])
    => add(Type = "urn:anandmsft:tmp/idflag", Value = "useguid");

<span data-ttu-id="8e58d-252">Essa regra define um sinalizador temporário chamado **idflag** que é definido como **useguid** se não há nenhum **ms-ds-consistencyguid** populado para o usuário.</span><span class="sxs-lookup"><span data-stu-id="8e58d-252">This rule defines a temporary flag called **idflag** that is set to **useguid** if there's no **ms-ds-consistencyguid** populated for the user.</span></span> <span data-ttu-id="8e58d-253">A lógica por trás disso é o fato de que o AD FS não permite declarações vazias.</span><span class="sxs-lookup"><span data-stu-id="8e58d-253">The logic behind this is the fact that AD FS doesn't allow empty claims.</span></span> <span data-ttu-id="8e58d-254">Assim, quando você adiciona as declarações http://contoso.com/ws/2016/02/identity/claims/objectguid e http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid à Regra 1, você só acabará com uma declaração **msdsconsistencyguid** se o valor for populado para o usuário.</span><span class="sxs-lookup"><span data-stu-id="8e58d-254">So when you add claims http://contoso.com/ws/2016/02/identity/claims/objectguid and http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid in Rule 1, you end up with an **msdsconsistencyguid** claim only if the value is populated for the user.</span></span> <span data-ttu-id="8e58d-255">Se ele não estiver populado, o AD FS verá que ele terá um valor vazio e o descartará imediatamente.</span><span class="sxs-lookup"><span data-stu-id="8e58d-255">If it isn't populated, AD FS sees that it will have an empty value and drops it immediately.</span></span> <span data-ttu-id="8e58d-256">Todos os objetos terão **objectGuid**. Portanto, essa declaração sempre estará presente após a Regra 1 ser executada.</span><span class="sxs-lookup"><span data-stu-id="8e58d-256">All objects will have **objectGuid**, so that claim will always be there after Rule 1 is executed.</span></span>

<span data-ttu-id="8e58d-257">**Regra 3: emitir ms-ds-consistencyguid como a ID imutável, se estiver presente**</span><span class="sxs-lookup"><span data-stu-id="8e58d-257">**Rule 3: Issue ms-ds-consistencyguid as immutable ID if it's present**</span></span>

    c:[Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c.Value);

<span data-ttu-id="8e58d-258">Essa é uma verificação **Exist** implícita.</span><span class="sxs-lookup"><span data-stu-id="8e58d-258">This is an implicit **Exist** check.</span></span> <span data-ttu-id="8e58d-259">Se o valor para a declaração existir, emita-o como a ID imutável.</span><span class="sxs-lookup"><span data-stu-id="8e58d-259">If the value for the claim exists, then issue that as the immutable ID.</span></span> <span data-ttu-id="8e58d-260">O exemplo anterior usa a declaração **nameidentifier** .</span><span class="sxs-lookup"><span data-stu-id="8e58d-260">The previous example uses the **nameidentifier** claim.</span></span> <span data-ttu-id="8e58d-261">Você precisará alterar isso para o tipo de declaração adequado para a ID imutável no seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="8e58d-261">You'll have to change this to the appropriate claim type for the immutable ID in your environment.</span></span>

<span data-ttu-id="8e58d-262">**Regra 4: emitir o objectGuid como a ID imutável se ms-ds-consistencyGuid não estiver presente**</span><span class="sxs-lookup"><span data-stu-id="8e58d-262">**Rule 4: Issue objectGuid as immutable ID if ms-ds-consistencyGuid is not present**</span></span>

    c1:[Type == "urn:anandmsft:tmp/idflag", Value =~ "useguid"]
    && c2:[Type == "http://contoso.com/ws/2016/02/identity/claims/objectguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c2.Value);

<span data-ttu-id="8e58d-263">Nessa regra, você simplesmente verifica o sinalizador temporário **idflag**.</span><span class="sxs-lookup"><span data-stu-id="8e58d-263">In this rule, you're simply checking the temporary flag **idflag**.</span></span> <span data-ttu-id="8e58d-264">Você decide se deve emitir a declaração com base em seu valor.</span><span class="sxs-lookup"><span data-stu-id="8e58d-264">You decide whether to issue the claim based on its value.</span></span>

> [!NOTE]
> <span data-ttu-id="8e58d-265">A sequência dessas regras é importante.</span><span class="sxs-lookup"><span data-stu-id="8e58d-265">The sequence of these rules is important.</span></span>

### <a name="sso-with-a-subdomain-upn"></a><span data-ttu-id="8e58d-266">SSO com um subdomínio UPN</span><span class="sxs-lookup"><span data-stu-id="8e58d-266">SSO with a subdomain UPN</span></span>
<span data-ttu-id="8e58d-267">Você pode adicionar mais de um domínio a ser federado usando o Azure AD Connect, conforme descrito em [Adicionar um novo domínio federado](active-directory-aadconnect-federation-management.md#addfeddomain).</span><span class="sxs-lookup"><span data-stu-id="8e58d-267">You can add more than one domain to be federated by using Azure AD Connect, as described in [Add a new federated domain](active-directory-aadconnect-federation-management.md#addfeddomain).</span></span> <span data-ttu-id="8e58d-268">Você deve modificar a declaração de nome UPN para que a ID do emissor corresponda ao domínio raiz e não ao subdomínio, pois o domínio raiz federado também abrange o filho.</span><span class="sxs-lookup"><span data-stu-id="8e58d-268">You must modify the user principal name (UPN) claim so that the issuer ID corresponds to the root domain and not the subdomain, because the federated root domain also covers the child.</span></span>

<span data-ttu-id="8e58d-269">Por padrão, a regra da declaração da ID do emissor é definida como:</span><span class="sxs-lookup"><span data-stu-id="8e58d-269">By default, the claim rule for issuer ID is set as:</span></span>

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

![Declaração de ID do emissor padrão](media/active-directory-aadconnect-federation-management/issuer_id_default.png)

<span data-ttu-id="8e58d-271">A regra padrão simplesmente usa o sufixo do UPN na declaração da ID do emissor.</span><span class="sxs-lookup"><span data-stu-id="8e58d-271">The default rule simply takes the UPN suffix and uses it in the issuer ID claim.</span></span> <span data-ttu-id="8e58d-272">Por exemplo, John é um usuário em sub.contoso.com e contoso.com é federado com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e58d-272">For example, John is a user in sub.contoso.com, and contoso.com is federated with Azure AD.</span></span> <span data-ttu-id="8e58d-273">João insere john@sub.contoso.com como o nome de usuário ao entrar no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e58d-273">John enters john@sub.contoso.com as the username while signing in to Azure AD.</span></span> <span data-ttu-id="8e58d-274">A regra de declaração de ID de emissor padrão no AD FS lida com isso da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="8e58d-274">The default issuer ID claim rule in AD FS handles it in the following manner:</span></span>

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(john@sub.contoso.com, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

<span data-ttu-id="8e58d-275">**Valor de declaração:**  http://sub.contoso.com/adfs/services/trust/</span><span class="sxs-lookup"><span data-stu-id="8e58d-275">**Claim value:**  http://sub.contoso.com/adfs/services/trust/</span></span>

<span data-ttu-id="8e58d-276">Para ter apenas o domínio raiz no valor de declaração do emissor, altere a regra de declaração para corresponder ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="8e58d-276">To have only the root domain in the issuer claim value, change the claim rule to match the following:</span></span>

    c:[Type == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “^((.*)([.|@]))?(?<domain>[^.]*[.].*)$”, “http://${domain}/adfs/services/trust/“));

## <a name="next-steps"></a><span data-ttu-id="8e58d-277">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8e58d-277">Next steps</span></span>
<span data-ttu-id="8e58d-278">Saiba mais sobre as [opções de entrada do usuário](active-directory-aadconnect-user-signin.md).</span><span class="sxs-lookup"><span data-stu-id="8e58d-278">Learn more about [user sign-in options](active-directory-aadconnect-user-signin.md).</span></span>
