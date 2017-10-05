---
title: 'Azure Active Directory Domain Services: Implantar o Proxy de Aplicativo do Azure Active Directory | Microsoft Docs'
description: "Usar o Proxy de Aplicativo do Azure AD nos domínios gerenciados do Azure Active Directory Domain Services"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: c158c67a82e12501386179e19bc75fd852d7e308
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-azure-ad-application-proxy-on-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="d2c3a-103">Implantar o Proxy de Aplicativo do Azure AD em um domínio gerenciado do Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="d2c3a-103">Deploy Azure AD Application Proxy on an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="d2c3a-104">O Proxy de Aplicativo do Active Directory (AD) do Azure o ajuda a dar suporte a funcionários remotos publicando aplicativos locais para serem acessados via Internet.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-104">Azure Active Directory (AD) Application Proxy helps you support remote workers by publishing on-premises applications to be accessed over the internet.</span></span> <span data-ttu-id="d2c3a-105">Com o Azure AD Domain Services, agora você pode usar modelo lift-and-shift em aplicativos herdados executados localmente para os Serviços de Infraestrutura do Azure.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-105">With Azure AD Domain Services, you can now lift-and-shift legacy applications running on-premises to Azure Infrastructure Services.</span></span> <span data-ttu-id="d2c3a-106">Depois, publique esses aplicativos usando o Proxy de Aplicativo do Azure AD, a fim de fornecer acesso remoto seguro aos usuários em sua organização.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-106">You can then publish these applications using the Azure AD Application Proxy, to provide secure remote access to users in your organization.</span></span>

<span data-ttu-id="d2c3a-107">Se você for um novo usuário do Proxy de Aplicativo do Azure AD, aprenda mais sobre este recurso com o artigo: [Como fornecer acesso remoto seguro a aplicativos locais](../active-directory/active-directory-application-proxy-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d2c3a-107">If you're new to the Azure AD Application Proxy, learn more about this feature with the following article: [How to provide secure remote access to on-premises applications](../active-directory/active-directory-application-proxy-get-started.md).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="d2c3a-108">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="d2c3a-108">Before you begin</span></span>
<span data-ttu-id="d2c3a-109">Para executar as tarefas listadas neste artigo, você precisa do seguinte:</span><span class="sxs-lookup"><span data-stu-id="d2c3a-109">To perform the tasks listed in this article, you need:</span></span>

1. <span data-ttu-id="d2c3a-110">Uma **assinatura do Azure**válida.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-110">A valid **Azure subscription**.</span></span>
2. <span data-ttu-id="d2c3a-111">Um **diretório do AD do Azure** - seja sincronizado com um diretório local ou com um diretório somente na nuvem.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-111">An **Azure AD directory** - either synchronized with an on-premises directory or a cloud-only directory.</span></span>
3. <span data-ttu-id="d2c3a-112">É necessário ter uma **licença Básica ou Premium do Azure AD** para usar o Proxy de Aplicativo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-112">An **Azure AD Basic or Premium license** is required to use the Azure AD Application Proxy.</span></span>
4. <span data-ttu-id="d2c3a-113">**Serviços de Domínio do Azure AD** devem ser habilitados para o diretório do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-113">**Azure AD Domain Services** must be enabled for the Azure AD directory.</span></span> <span data-ttu-id="d2c3a-114">Se você ainda não tiver feito isso, execute todas as tarefas descritas no [guia de Introdução](active-directory-ds-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="d2c3a-114">If you haven't done so, follow all the tasks outlined in the [Getting Started guide](active-directory-ds-getting-started.md).</span></span>

<br>

## <a name="task-1---enable-azure-ad-application-proxy-for-your-azure-ad-directory"></a><span data-ttu-id="d2c3a-115">Tarefa 1: Habilitar o Proxy de Aplicativo do Azure AD para o diretório do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2c3a-115">Task 1 - Enable Azure AD Application Proxy for your Azure AD directory</span></span>
<span data-ttu-id="d2c3a-116">Execute as etapas a seguir para habilitar o Proxy de Aplicativo do Azure AD para seu diretório do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-116">Perform the following steps to enable the Azure AD Application Proxy for your Azure AD directory.</span></span>

1. <span data-ttu-id="d2c3a-117">Entre como administrador no [Portal do Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d2c3a-117">Sign in as an administrator in the [Azure portal](http://portal.azure.com).</span></span>

2. <span data-ttu-id="d2c3a-118">Clique em **Azure Active Directory** para exibir a visão geral do diretório.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-118">Click **Azure Active Directory** to bring up the directory overview.</span></span> <span data-ttu-id="d2c3a-119">Clique em **Aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-119">Click **Enterprise applications**.</span></span>

    ![Selecionar um diretório do Azure AD](./media/app-proxy/app-proxy-enable-start.png)
3. <span data-ttu-id="d2c3a-121">Clique em **Proxy de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-121">Click **Application proxy**.</span></span> <span data-ttu-id="d2c3a-122">Se você não tiver uma assinatura Básica ou Premium do Azure AD, verá uma opção para habilitar uma versão de avaliação.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-122">If you do not have an Azure AD Basic or Azure AD Premium subscription, you see an option to enable a trial.</span></span> <span data-ttu-id="d2c3a-123">Alterne **Habilitar Proxy de Aplicativo?** para **Habilitar** e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-123">Toggle **Enable Application Proxy?** to **Enable** and click **Save**.</span></span>

    ![Habilitar Proxy de Aplicativo](./media/app-proxy/app-proxy-enable-proxy-blade.png)
4. <span data-ttu-id="d2c3a-125">Para baixar o conector, clique no botão **Conector**.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-125">To download the connector, click the **Connector** button.</span></span>

    ![Baixe o conector](./media/app-proxy/app-proxy-enabled-download-connector.png)
5. <span data-ttu-id="d2c3a-127">Na página de download, aceite os termos de licença e o contrato de privacidade e clique no botão **Baixar**.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-127">On the download page, accept the license terms and privacy agreement and click the **Download** button.</span></span>

    ![Confirme o download](./media/app-proxy/app-proxy-enabled-confirm-download.png)


## <a name="task-2---provision-domain-joined-windows-servers-to-deploy-the-azure-ad-application-proxy-connector"></a><span data-ttu-id="d2c3a-129">Tarefa 2: Provisionar servidores Windows ingressados em domínio para implantar o conector do Proxy de Aplicativo do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2c3a-129">Task 2 - Provision domain-joined Windows servers to deploy the Azure AD Application Proxy connector</span></span>
<span data-ttu-id="d2c3a-130">Você precisa de máquinas virtuais com Windows Server ingressadas em domínio nas quais pode instalar o conector do Proxy de Aplicativo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-130">You need domain-joined Windows Server virtual machines on which you can install the Azure AD Application Proxy connector.</span></span> <span data-ttu-id="d2c3a-131">Dependendo dos aplicativos que estão sendo publicados, você pode optar por provisionar vários servidores nos quais o conector está instalado.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-131">Depending on the applications being published, you may choose to provision multiple servers on which the connector is installed.</span></span> <span data-ttu-id="d2c3a-132">Essa opção de implantação fornece mais disponibilidade e ajuda a lidar com cargas mais pesadas de autenticação.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-132">This deployment option gives you greater availability and helps handle heavier authentication loads.</span></span>

<span data-ttu-id="d2c3a-133">Provisione os servidores do conector na mesma rede virtual (ou uma rede virtual conectada/emparelhada), na qual você habilitou seu domínio gerenciado do Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-133">Provision the connector servers on the same virtual network (or a connected/peered virtual network), in which you have enabled your Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="d2c3a-134">Da mesma forma, os servidores que hospedam os aplicativos publicados por meio do Proxy de Aplicativo precisam ser instalados na mesma rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-134">Similarly, the servers hosting the applications you publish via the Application Proxy need to be installed on the same Azure virtual network.</span></span>

<span data-ttu-id="d2c3a-135">Para provisionar os servidores do conector, execute as tarefas descritas no artigo [Ingressar uma máquina virtual do Windows em um domínio gerenciado](active-directory-ds-admin-guide-join-windows-vm.md).</span><span class="sxs-lookup"><span data-stu-id="d2c3a-135">To provision connector servers, follow the tasks outlined in the article titled [Join a Windows virtual machine to a managed domain](active-directory-ds-admin-guide-join-windows-vm.md).</span></span>


## <a name="task-3---install-and-register-the-azure-ad-application-proxy-connector"></a><span data-ttu-id="d2c3a-136">Tarefa 3: Instalar e registrar o conector do Proxy de Aplicativo do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2c3a-136">Task 3 - Install and register the Azure AD Application Proxy Connector</span></span>
<span data-ttu-id="d2c3a-137">Antes, você provisionou uma máquina virtual com Windows Server e ingressou no domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-137">Previously, you provisioned a Windows Server virtual machine and joined it to the managed domain.</span></span> <span data-ttu-id="d2c3a-138">Nesta tarefa, você instalará o conector do Proxy de Aplicativo do Azure AD nesta máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-138">In this task, you will install the Azure AD Application Proxy connector on this virtual machine.</span></span>

1. <span data-ttu-id="d2c3a-139">Copie o pacote de instalação do conector na VM na qual você instalou o conector do Proxy de Aplicativo Web do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-139">Copy the connector installation package to the VM on which you install the Azure AD Web Application Proxy connector.</span></span>

2. <span data-ttu-id="d2c3a-140">Execute **AADApplicationProxyConnectorInstaller.exe** na máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-140">Run **AADApplicationProxyConnectorInstaller.exe** on the virtual machine.</span></span> <span data-ttu-id="d2c3a-141">Aceite os termos de licença de software.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-141">Accept the software license terms.</span></span>

    ![Aceite os termos de instalação](./media/app-proxy/app-proxy-install-connector-terms.png)
3. <span data-ttu-id="d2c3a-143">Durante a instalação, você receberá uma solicitação para registrar o conector com o Proxy de Aplicativo de seu locatário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-143">During installation, you are prompted to register the connector with the Application Proxy of your Azure AD directory.</span></span>
    * <span data-ttu-id="d2c3a-144">Forneça suas **credenciais de administrador global do Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-144">Provide your **Azure AD global administrator credentials**.</span></span> <span data-ttu-id="d2c3a-145">Seu locatário de administrador global pode ser diferente das suas credenciais do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-145">Your global administrator tenant may be different from your Microsoft Azure credentials.</span></span>
    * <span data-ttu-id="d2c3a-146">A conta de administrador usada para registrar o conector deve pertencer ao mesmo diretório no qual você habilitou o serviço Proxy de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-146">The administrator account used to register the connector must belong to the same directory where you enabled the Application Proxy service.</span></span> <span data-ttu-id="d2c3a-147">Por exemplo, se o domínio de locatário for contoso.com, o administrador deverá ser admin@contoso.com ou qualquer outro alias válido nesse domínio.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-147">For example, if the tenant domain is contoso.com, the admin should be admin@contoso.com or any other valid alias on that domain.</span></span>
    * <span data-ttu-id="d2c3a-148">Se a Configuração de Segurança Aprimorada do Internet Explorer estiver ativada no servidor em que você estiver instalando o conector, a tela de registro poderá ser bloqueada.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-148">If IE Enhanced Security Configuration is turned on for the server where you are installing the connector, the registration screen might be blocked.</span></span> <span data-ttu-id="d2c3a-149">Siga as instruções na mensagem de erro para permitir o acesso.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-149">To allow access, follow the instructions in the error message.</span></span> <span data-ttu-id="d2c3a-150">Certifique-se de que a Segurança Melhorada do Internet Explorer está desativada.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-150">Make sure that Internet Explorer Enhanced Security is off.</span></span>
    * <span data-ttu-id="d2c3a-151">Se o registro do conector não for bem-sucedido, confira [Solucionar problemas de Proxy de Aplicativo](../active-directory/active-directory-application-proxy-troubleshoot.md).</span><span class="sxs-lookup"><span data-stu-id="d2c3a-151">If connector registration does not succeed, see [Troubleshoot Application Proxy](../active-directory/active-directory-application-proxy-troubleshoot.md).</span></span>

    ![Conector instalado](./media/app-proxy/app-proxy-connector-installed.png)
4. <span data-ttu-id="d2c3a-153">Para garantir o funcionamento correto do conector, execute a Solução de Problemas do Conector do Proxy de Aplicativo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-153">To ensure the connector works properly, run the Azure AD Application Proxy Connector Troubleshooter.</span></span> <span data-ttu-id="d2c3a-154">O resultado da execução da solução de problemas deve ser um relatório de êxito.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-154">You should see a successful report after running the troubleshooter.</span></span>

    ![Êxito da solução de problemas](./media/app-proxy/app-proxy-connector-troubleshooter.png)
5. <span data-ttu-id="d2c3a-156">Você deverá ver o conector recém-instalado listado na página do Proxy de aplicativo em seu diretório do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-156">You should see the newly installed connector listed on the Application proxy page in your Azure AD directory.</span></span>

    ![](./media/app-proxy/app-proxy-connector-page.png)

> [!NOTE]
> <span data-ttu-id="d2c3a-157">Escolha instalar os conectores em vários servidores para garantir a alta disponibilidade aos aplicativos de autenticação publicados por meio do Proxy de Aplicativo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-157">You may choose to install connectors on multiple servers to guarantee high availability for authenticating applications published through the Azure AD Application Proxy.</span></span> <span data-ttu-id="d2c3a-158">Execute as mesmas etapas listadas acima para instalar o conector em outros servidores ingressados em seu domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-158">Perform the same steps listed above to install the connector on other servers joined to your managed domain.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="d2c3a-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d2c3a-159">Next Steps</span></span>
<span data-ttu-id="d2c3a-160">Você configurou o Proxy de Aplicativo do Azure AD e o integrou a seu domínio gerenciado do Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-160">You have set up the Azure AD Application Proxy and integrated it with your Azure AD Domain Services managed domain.</span></span>

* <span data-ttu-id="d2c3a-161">**Migrar seus aplicativos para máquinas virtuais do Azure:** use o modelo lift-and-shift para migrar seus aplicativos de servidores locais para máquinas virtuais do Azure ingressadas em seu domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-161">**Migrate your applications to Azure virtual machines:** You can lift-and-shift your applications from on-premises servers to Azure virtual machines joined to your managed domain.</span></span> <span data-ttu-id="d2c3a-162">Isso ajuda você a se livrar dos custos com infraestrutura gerados pela execução de servidores localmente.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-162">Doing so helps you get rid of the infrastructure costs of running servers on-premises.</span></span>

* <span data-ttu-id="d2c3a-163">**Publicar aplicativos usando o Proxy de Aplicativo do Azure AD:** publique aplicativos em execução em suas máquinas virtuais do Azure usando o Proxy de Aplicativo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-163">**Publish applications using Azure AD Application Proxy:** Publish applications running on your Azure virtual machines using the Azure AD Application Proxy.</span></span> <span data-ttu-id="d2c3a-164">Para saber mais, confira [publicar aplicativos usando o Proxy de Aplicativo do Azure AD](../active-directory/application-proxy-publish-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="d2c3a-164">For more information, see [publish applications using Azure AD Application Proxy](../active-directory/application-proxy-publish-azure-portal.md)</span></span>


## <a name="deployment-note---publish-iwa-integrated-windows-authentication-applications-using-azure-ad-application-proxy"></a><span data-ttu-id="d2c3a-165">Nota sobre a implantação: publique aplicativos IWA (Autenticação Integrada do Windows) usando o Proxy de Aplicativo do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2c3a-165">Deployment note - Publish IWA (Integrated Windows Authentication) applications using Azure AD Application Proxy</span></span>
<span data-ttu-id="d2c3a-166">Habilite o logon único para seus aplicativos usando a IWA (Autenticação Integrada do Windows) concedendo permissão aos Conectores de Proxy de Aplicativo para representar usuários e enviar e receber tokens em seu nome.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-166">Enable single sign-on to your applications using Integrated Windows Authentication (IWA) by granting Application Proxy Connectors permission to impersonate users, and send and receive tokens on their behalf.</span></span> <span data-ttu-id="d2c3a-167">Configure a KCD (Delegação restrita de kerberos) para que o conector conceda as permissões necessárias para o acesso de recursos no domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-167">Configure kerberos constrained delegation (KCD) for the connector to grant the required permissions to access resources on the managed domain.</span></span> <span data-ttu-id="d2c3a-168">Use o mecanismo KCD baseado em recursos em domínios gerenciados para aumentar a segurança.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-168">Use the resource-based KCD mechanism on managed domains for increased security.</span></span>


### <a name="enable-resource-based-kerberos-constrained-delegation-for-the-azure-ad-application-proxy-connector"></a><span data-ttu-id="d2c3a-169">Habilitar a delegação restrita de kerberos com base em recursos para o conector de Proxy de Aplicativo do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2c3a-169">Enable resource-based kerberos constrained delegation for the Azure AD Application Proxy connector</span></span>
<span data-ttu-id="d2c3a-170">O conector do Proxy de Aplicativo do Azure deve ser configurado para KCD (delegação restrita de kerberos), para que possa representar usuários no domínio gerenciado.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-170">The Azure Application Proxy connector should be configured for kerberos constrained delegation (KCD), so it can impersonate users on the managed domain.</span></span> <span data-ttu-id="d2c3a-171">Em um domínio gerenciado do Azure AD Domain Services, você não tem privilégios de administrador de domínio.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-171">On an Azure AD Domain Services managed domain, you do not have domain administrator privileges.</span></span> <span data-ttu-id="d2c3a-172">Portanto, **não é possível configurar um KCD tradicional no nível da conta em um domínio gerenciado**.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-172">Therefore, **traditional account-level KCD cannot be configured on a managed domain**.</span></span>

<span data-ttu-id="d2c3a-173">Use o KCD baseado em recursos conforme descrito neste [artigo](active-directory-ds-enable-kcd.md).</span><span class="sxs-lookup"><span data-stu-id="d2c3a-173">Use resource-based KCD as described in this [article](active-directory-ds-enable-kcd.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d2c3a-174">Você precisará ser um membro do grupo "Administradores do controlador de domínio do AAD" para administrar o domínio gerenciado usando cmdlets do AD PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-174">You need to be a member of the 'AAD DC Administrators' group, to administer the managed domain using AD PowerShell cmdlets.</span></span>
>
>

<span data-ttu-id="d2c3a-175">Use o cmdlet Get-ADComputer do PowerShell para recuperar as configurações do computador no qual o conector de Proxy de Aplicativo do Azure AD está instalado.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-175">Use the Get-ADComputer PowerShell cmdlet to retrieve the settings for the computer on which the Azure AD Application Proxy connector is installed.</span></span>
```
$ConnectorComputerAccount = Get-ADComputer -Identity contoso100-proxy.contoso100.com
```

<span data-ttu-id="d2c3a-176">Depois disso, use o cmdlet Set-ADComputer para configurar o KCD baseado em recursos para o servidor do recurso.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-176">Thereafter, use the Set-ADComputer cmdlet to set up resource-based KCD for the resource server.</span></span>
```
Set-ADComputer contoso100-resource.contoso100.com -PrincipalsAllowedToDelegateToAccount $ConnectorComputerAccount
```

<span data-ttu-id="d2c3a-177">Se você tiver implantado vários conectores de Proxy de Aplicativo em seu domínio gerenciado, será necessário configurar o KCD baseado em recursos para cada instância do conector.</span><span class="sxs-lookup"><span data-stu-id="d2c3a-177">If you have deployed multiple Application Proxy connectors on your managed domain, you need to configure resource-based KCD for each such connector instance.</span></span>


## <a name="related-content"></a><span data-ttu-id="d2c3a-178">Conteúdo relacionado</span><span class="sxs-lookup"><span data-stu-id="d2c3a-178">Related Content</span></span>
* [<span data-ttu-id="d2c3a-179">Serviços de Domínio do Azure AD - guia de Introdução</span><span class="sxs-lookup"><span data-stu-id="d2c3a-179">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="d2c3a-180">Configurar a Delegação Restrita de Kerberos em um domínio gerenciado</span><span class="sxs-lookup"><span data-stu-id="d2c3a-180">Configure Kerberos Constrained Delegation on a managed domain</span></span>](active-directory-ds-enable-kcd.md)
* [<span data-ttu-id="d2c3a-181">Visão geral da Delegação Restrita de Kerberos</span><span class="sxs-lookup"><span data-stu-id="d2c3a-181">Kerberos Constrained Delegation Overview</span></span>](https://technet.microsoft.com/library/jj553400.aspx)
