---
title: Habilitar acesso remoto ao SharePoint com o Proxy de Aplicativo do Azure AD | Microsoft Docs
description: "Aborda os conceitos básicos sobre como integrar um servidor do SharePoint local com o Proxy de Aplicativo do Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 97eeec3b3936bcbef6ac3966b890332901bcb153
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="enable-remote-access-to-sharepoint-with-azure-ad-application-proxy"></a><span data-ttu-id="31b1a-103">Habilitar acesso remoto ao SharePoint com o Proxy de Aplicativo do Azure AD</span><span class="sxs-lookup"><span data-stu-id="31b1a-103">Enable remote access to SharePoint with Azure AD Application Proxy</span></span>

<span data-ttu-id="31b1a-104">Este artigo descreve como integrar um servidor local do SharePoint ao proxy de aplicativo do Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="31b1a-104">This article discusses how to integrate an on-premises SharePoint server with Azure Active Directory (Azure AD) Application Proxy.</span></span>

<span data-ttu-id="31b1a-105">Para habilitar o acesso remoto ao SharePoint com o Proxy de aplicativo do Azure AD, siga as seções neste artigo passo a passo.</span><span class="sxs-lookup"><span data-stu-id="31b1a-105">To enable remote access to SharePoint with Azure AD Application Proxy, follow the sections in this article step by step.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="31b1a-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="31b1a-106">Prerequisites</span></span>

<span data-ttu-id="31b1a-107">Este artigo pressupõe que você já tenha o SharePoint 2013 ou mais recente no seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="31b1a-107">This article assumes that you already have SharePoint 2013 or newer in your environment.</span></span> <span data-ttu-id="31b1a-108">Além disso, considere os seguintes pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="31b1a-108">In addition, consider the following prerequisites:</span></span>

* <span data-ttu-id="31b1a-109">O SharePoint inclui suporte nativo a Kerberos.</span><span class="sxs-lookup"><span data-stu-id="31b1a-109">SharePoint includes native Kerberos support.</span></span> <span data-ttu-id="31b1a-110">Portanto, os usuários que acessam sites internos remotamente por meio do Proxy de Aplicativo do Azure AD podem supor que terão uma experiência de SSO (logon único).</span><span class="sxs-lookup"><span data-stu-id="31b1a-110">Therefore, users who are accessing internal sites remotely through Azure AD Application Proxy can assume to have a single sign-on (SSO) experience.</span></span>

* <span data-ttu-id="31b1a-111">Você precisa fazer algumas mudanças na configuração do seu servidor do SharePoint.</span><span class="sxs-lookup"><span data-stu-id="31b1a-111">You need to make a few configuration changes to your SharePoint server.</span></span> <span data-ttu-id="31b1a-112">É recomendável usar um ambiente de preparo.</span><span class="sxs-lookup"><span data-stu-id="31b1a-112">We recommend using a staging environment.</span></span> <span data-ttu-id="31b1a-113">Dessa forma, você pode fazer atualizações no servidor de preparo primeiro e depois facilitar um ciclo de testes antes de passar para o de produção.</span><span class="sxs-lookup"><span data-stu-id="31b1a-113">This way, you can make updates to your staging server first, and then facilitate a testing cycle before going into production.</span></span>

* <span data-ttu-id="31b1a-114">Supomos que você já configurou o SSL para SharePoint, pois exigimos o SSL na URL publicada.</span><span class="sxs-lookup"><span data-stu-id="31b1a-114">We assume that you have already set up SSL for SharePoint, because we require SSL on the published URL.</span></span> <span data-ttu-id="31b1a-115">Você precisa ter o SSL habilitado no site interno a fim de assegurar que os links sejam enviados/mapeados corretamente.</span><span class="sxs-lookup"><span data-stu-id="31b1a-115">You need to have SSL enabled on your internal site, to ensure that links are sent/mapped correctly.</span></span> <span data-ttu-id="31b1a-116">Se você ainda não configurou o SSL, consulte [Configurar o SSL para o SharePoint 2013](https://blogs.msdn.microsoft.com/fabdulwahab/2013/01/20/configure-ssl-for-sharepoint-2013) para obter instruções.</span><span class="sxs-lookup"><span data-stu-id="31b1a-116">If you haven't configured SSL, see [Configure SSL for SharePoint 2013](https://blogs.msdn.microsoft.com/fabdulwahab/2013/01/20/configure-ssl-for-sharepoint-2013) for instructions.</span></span> <span data-ttu-id="31b1a-117">Além disso, verifique se o computador conector confia no certificado que você emite.</span><span class="sxs-lookup"><span data-stu-id="31b1a-117">Also, make sure that the connector machine trusts the certificate that you issue.</span></span> <span data-ttu-id="31b1a-118">(O certificado não precisa ser emitido publicamente.)</span><span class="sxs-lookup"><span data-stu-id="31b1a-118">(The certificate does not need to be publicly issued.)</span></span>

## <a name="step-1-set-up-single-sign-on-to-sharepoint"></a><span data-ttu-id="31b1a-119">Parte 1: configurar o logon único para o SharePoint</span><span class="sxs-lookup"><span data-stu-id="31b1a-119">Step 1: Set up single sign-on to SharePoint</span></span>

<span data-ttu-id="31b1a-120">Nossos clientes querem a melhor experiência de SSO para seus aplicativos de back-end, nesse caso, o SharePoint Server.</span><span class="sxs-lookup"><span data-stu-id="31b1a-120">Our customers want the best SSO experience for their back-end applications, SharePoint server in this case.</span></span> <span data-ttu-id="31b1a-121">Nesse cenário comum do Azure AD, o usuário se autenticará apenas uma vez, pois não será mais solicitado que ele faça isso novamente.</span><span class="sxs-lookup"><span data-stu-id="31b1a-121">In this common Azure AD scenario, the user is authenticated only once, because they will not be prompted for authentication again.</span></span>

<span data-ttu-id="31b1a-122">Para aplicativos locais que exigem ou usam a autenticação do Windows, você pode obter SSO usando o protocolo de autenticação Kerberos e um recurso chamado KCD (delegação restrita de Kerberos).</span><span class="sxs-lookup"><span data-stu-id="31b1a-122">For on-premises applications that require or use Windows authentication, you can achieve SSO by using the Kerberos authentication protocol and a feature called Kerberos constrained delegation (KCD).</span></span> <span data-ttu-id="31b1a-123">A KCD, quando configurada, permite que o conector do proxy de aplicativo obtenha um tíquete/token do Windows para um usuário, mesmo que ele não tenha entrado no Windows diretamente.</span><span class="sxs-lookup"><span data-stu-id="31b1a-123">KCD, when configured, allows the Application Proxy connector to obtain a windows ticket/token for a user, even if the user hasn’t signed in to Windows directly.</span></span> <span data-ttu-id="31b1a-124">Para saber mais sobre a KCD, confira [Visão geral da delegação restrita de Kerberos](https://technet.microsoft.com/library/jj553400.aspx).</span><span class="sxs-lookup"><span data-stu-id="31b1a-124">To learn more about KCD, see [Kerberos Constrained Delegation Overview](https://technet.microsoft.com/library/jj553400.aspx).</span></span>

<span data-ttu-id="31b1a-125">Para configurar o KCD para um servidor do SharePoint, use os procedimentos nas seções sequenciais a seguir:</span><span class="sxs-lookup"><span data-stu-id="31b1a-125">To set up KCD for a SharePoint server, use the procedures in the following sequential sections:</span></span>

### <a name="ensure-that-sharepoint-is-running-under-a-service-account"></a><span data-ttu-id="31b1a-126">Certificar-se de que SharePoint está em execução como uma conta de serviço</span><span class="sxs-lookup"><span data-stu-id="31b1a-126">Ensure that SharePoint is running under a service account</span></span>

<span data-ttu-id="31b1a-127">Primeiro, certifique-se de que o SharePoint está em execução em uma conta de serviço e não no sistema local, serviço local ou serviço de rede.</span><span class="sxs-lookup"><span data-stu-id="31b1a-127">First, make sure that SharePoint is running under a defined service account--not local system, local service, or network service.</span></span> <span data-ttu-id="31b1a-128">Faça isso para que você possa anexar SPNs (nomes da entidade de serviço) a uma conta válida.</span><span class="sxs-lookup"><span data-stu-id="31b1a-128">Do this so that you can attach service principal names (SPNs) to a valid account.</span></span> <span data-ttu-id="31b1a-129">Os SPNs são a maneira como o protocolo Kerberos identifica serviços diferentes.</span><span class="sxs-lookup"><span data-stu-id="31b1a-129">SPNs are how the Kerberos protocol identifies different services.</span></span> <span data-ttu-id="31b1a-130">E você precisará da conta mais tarde para configurar a KCD.</span><span class="sxs-lookup"><span data-stu-id="31b1a-130">And you will need the account later to configure the KCD.</span></span>

<span data-ttu-id="31b1a-131">Para garantir que seus sites estejam em execução em uma conta de serviço definida, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="31b1a-131">To ensure that your sites are running under a defined service account, perform the following steps:</span></span>

1. <span data-ttu-id="31b1a-132">Abra o site **Administração Central do SharePoint 2013**.</span><span class="sxs-lookup"><span data-stu-id="31b1a-132">Open the **SharePoint 2013 Central Administration** site.</span></span>
2. <span data-ttu-id="31b1a-133">Vá para **Segurança** e selecione **Configurar contas de serviço**.</span><span class="sxs-lookup"><span data-stu-id="31b1a-133">Go to **Security** and select **Configure service accounts**.</span></span>
3. <span data-ttu-id="31b1a-134">Selecione **Pool de Aplicativos Web – SharePoint – 80**.</span><span class="sxs-lookup"><span data-stu-id="31b1a-134">Select **Web Application Pool - SharePoint - 80**.</span></span> <span data-ttu-id="31b1a-135">As opções podem ser ligeiramente diferentes com base no nome do seu pool Web ou caso o pool Web use o SSL por padrão.</span><span class="sxs-lookup"><span data-stu-id="31b1a-135">The options may be slightly different based on the name of your web pool, or if the web pool uses SSL by default.</span></span>

  ![Opções para configurar uma conta de serviço](./media/application-proxy-remote-sharepoint/remote-sharepoint-service-web-application.png)

4. <span data-ttu-id="31b1a-137">Se **Selecionar uma conta para este componente** for **Serviço Local** ou **Serviço de Rede**, você precisará criar uma conta.</span><span class="sxs-lookup"><span data-stu-id="31b1a-137">If **Select an account for this component** is **Local Service** or **Network Service**, you need to create an account.</span></span> <span data-ttu-id="31b1a-138">Caso contrário, você já poderá passar para a próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="31b1a-138">If not, you're finished and can move to the next section.</span></span>
5. <span data-ttu-id="31b1a-139">Escolha **Registrar uma nova conta gerenciada**.</span><span class="sxs-lookup"><span data-stu-id="31b1a-139">Select **Register new managed account**.</span></span> <span data-ttu-id="31b1a-140">Depois que a conta é criada, é preciso definir o **Pool de Aplicativos Web** antes de poder usá-la.</span><span class="sxs-lookup"><span data-stu-id="31b1a-140">After your account is created, you must set **Web Application Pool** before you can use the account.</span></span>

> [!NOTE]
<span data-ttu-id="31b1a-141">Você precisará ter uma conta do Azure AD criada anteriormente para o serviço.</span><span class="sxs-lookup"><span data-stu-id="31b1a-141">You need to have a previously created Azure AD account for the service.</span></span> <span data-ttu-id="31b1a-142">Sugerimos que você permita uma alteração automática de senha.</span><span class="sxs-lookup"><span data-stu-id="31b1a-142">We suggest that you allow for an automatic password change.</span></span> <span data-ttu-id="31b1a-143">Para obter mais informações sobre o conjunto completo de etapas e a solução de problemas, confira [Configurar a alteração automática da senha no SharePoint 2013](https://technet.microsoft.com/library/ff724280.aspx).</span><span class="sxs-lookup"><span data-stu-id="31b1a-143">For more information about the full set of steps and troubleshooting issues, see [Configure automatic password change in SharePoint 2013](https://technet.microsoft.com/library/ff724280.aspx).</span></span>

### <a name="configure-sharepoint-for-kerberos"></a><span data-ttu-id="31b1a-144">Configurar o SharePoint para Kerberos</span><span class="sxs-lookup"><span data-stu-id="31b1a-144">Configure SharePoint for Kerberos</span></span>

<span data-ttu-id="31b1a-145">Você usa a KCD para executar o logon único no servidor do SharePoint e isso funciona somente com o Kerberos.</span><span class="sxs-lookup"><span data-stu-id="31b1a-145">You use KCD to perform single sign-on to the SharePoint server, and this works only with Kerberos.</span></span>

<span data-ttu-id="31b1a-146">Para configurar o site do SharePoint para autenticação Kerberos:</span><span class="sxs-lookup"><span data-stu-id="31b1a-146">To configure your SharePoint site for Kerberos authentication:</span></span>

1. <span data-ttu-id="31b1a-147">Abra o site **Administração Central do SharePoint 2013**.</span><span class="sxs-lookup"><span data-stu-id="31b1a-147">Open the **SharePoint 2013 Central Administration** site.</span></span>
2. <span data-ttu-id="31b1a-148">Vá para **Gerenciamento de Aplicativos**, selecione **Gerenciar aplicativos Web** e selecione seu site do SharePoint.</span><span class="sxs-lookup"><span data-stu-id="31b1a-148">Go to **Application Management**, select **Manage web applications**, and select your SharePoint site.</span></span> <span data-ttu-id="31b1a-149">Neste exemplo, é **SharePoint - 80**.</span><span class="sxs-lookup"><span data-stu-id="31b1a-149">In this example, it is **SharePoint - 80**.</span></span>

  ![Selecionar o site do SharePoint](./media/application-proxy-remote-sharepoint/remote-sharepoint-manage-web-applications.png)

3. <span data-ttu-id="31b1a-151">Clique em **Provedores de Autenticação** na barra de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="31b1a-151">Click **Authentication Providers** on the toolbar.</span></span>
4. <span data-ttu-id="31b1a-152">Na caixa **Provedores de Autenticação**, clique em **Zona Padrão** para exibir as configurações.</span><span class="sxs-lookup"><span data-stu-id="31b1a-152">In the **Authentication Providers** box, click **Default Zone** to view the settings.</span></span>
5. <span data-ttu-id="31b1a-153">Na caixa de diálogo **Editar Autenticação**, role para baixo até ver **Tipos de Autenticação por Declarações** e verifique se ambas as opções **Habilitar Autenticação do Windows** e **Autenticação Integrada do Windows** estão selecionadas.</span><span class="sxs-lookup"><span data-stu-id="31b1a-153">In the **Edit Authentication** dialog box, scroll down until you see **Claims Authentication Types** and ensure that both **Enable Windows Authentication** and **Integrated Windows Authentication** are selected.</span></span>
6. <span data-ttu-id="31b1a-154">Na caixa suspensa, verifique se a opção **Negociar (Kerberos)** está selecionada.</span><span class="sxs-lookup"><span data-stu-id="31b1a-154">In the drop-down box, make sure that **Negotiate (Kerberos)** is selected.</span></span>

  ![Caixa de diálogo Editar Autenticação](./media/application-proxy-remote-sharepoint/remote-sharepoint-service-edit-authentication.png)

7. <span data-ttu-id="31b1a-156">Na parte inferior da caixa de diálogo **Editar Autenticação**, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="31b1a-156">At the bottom of the **Edit Authentication** dialog box, click **Save**.</span></span>

### <a name="set-a-service-principal-name-for-the-sharepoint-service-account"></a><span data-ttu-id="31b1a-157">Definir um nome da entidade de serviço para a conta de serviço do SharePoint</span><span class="sxs-lookup"><span data-stu-id="31b1a-157">Set a service principal name for the SharePoint service account</span></span>

<span data-ttu-id="31b1a-158">Antes de configurar a KCD, você precisa identificar o serviço do SharePoint em execução como a conta de serviço que você configurou.</span><span class="sxs-lookup"><span data-stu-id="31b1a-158">Before you configure the KCD, you need to identify the SharePoint service running as the service account that you've configured.</span></span> <span data-ttu-id="31b1a-159">Você pode fazer isso configurando um SPN.</span><span class="sxs-lookup"><span data-stu-id="31b1a-159">You do this by setting an SPN.</span></span> <span data-ttu-id="31b1a-160">Para saber mais, confira [Service Principal Names](https://technet.microsoft.com/library/cc961723.aspx) (Nomes da entidade de serviço).</span><span class="sxs-lookup"><span data-stu-id="31b1a-160">For more information, see [Service Principal Names](https://technet.microsoft.com/library/cc961723.aspx).</span></span>

<span data-ttu-id="31b1a-161">O formato SPN é:</span><span class="sxs-lookup"><span data-stu-id="31b1a-161">The SPN format is:</span></span>

```
<service class>/<host>:<port>
```

<span data-ttu-id="31b1a-162">No formato SPN:</span><span class="sxs-lookup"><span data-stu-id="31b1a-162">In the SPN format:</span></span>

* <span data-ttu-id="31b1a-163">_service class_ é um nome exclusivo para o serviço.</span><span class="sxs-lookup"><span data-stu-id="31b1a-163">_service class_ is a unique name for the service.</span></span> <span data-ttu-id="31b1a-164">Para o SharePoint, você usa **HTTP**.</span><span class="sxs-lookup"><span data-stu-id="31b1a-164">For SharePoint, you use **HTTP**.</span></span>

* <span data-ttu-id="31b1a-165">_host_ é o domínio totalmente qualificado ou o nome NetBIOS do host no qual o serviço está em execução.</span><span class="sxs-lookup"><span data-stu-id="31b1a-165">_host_ is the fully qualified domain or NetBIOS name of the host that the service is running on.</span></span> <span data-ttu-id="31b1a-166">Para um site do SharePoint, esse texto pode ser a URL do site, dependendo da versão do IIS que você está usando.</span><span class="sxs-lookup"><span data-stu-id="31b1a-166">For a SharePoint site, this text might need to be the URL of the site, depending on the version of IIS that you're using.</span></span>

* <span data-ttu-id="31b1a-167">_port_ é opcional.</span><span class="sxs-lookup"><span data-stu-id="31b1a-167">_port_ is optional.</span></span>

<span data-ttu-id="31b1a-168">Se o FQDN do servidor do SharePoint for:</span><span class="sxs-lookup"><span data-stu-id="31b1a-168">If the FQDN of the SharePoint server is:</span></span>

```
sharepoint.demo.o365identity.us
```

<span data-ttu-id="31b1a-169">Nesse caso, o SPN será:</span><span class="sxs-lookup"><span data-stu-id="31b1a-169">Then the SPN is:</span></span>

```
HTTP/ sharepoint.demo.o365identity.us demo
```

<span data-ttu-id="31b1a-170">Talvez você precise definir SPNs para sites específicos em seu servidor.</span><span class="sxs-lookup"><span data-stu-id="31b1a-170">You might also need to set SPNs for specific sites on your server.</span></span> <span data-ttu-id="31b1a-171">Para obter mais informações, confira [Configurar a autenticação Kerberos](https://technet.microsoft.com/library/cc263449(v=office.12).aspx).</span><span class="sxs-lookup"><span data-stu-id="31b1a-171">For more information, see [Configure Kerberos authentication](https://technet.microsoft.com/library/cc263449(v=office.12).aspx).</span></span> <span data-ttu-id="31b1a-172">Preste muita atenção à seção "Criar nomes da entidade de serviço para seus aplicativos Web usando a autenticação Kerberos".</span><span class="sxs-lookup"><span data-stu-id="31b1a-172">Pay close attention to the section "Create Service Principal Names for your Web applications using Kerberos authentication."</span></span>

<span data-ttu-id="31b1a-173">A maneira mais fácil de você definir SPNs é seguir os formatos de SPN que podem já estar presentes para seus sites.</span><span class="sxs-lookup"><span data-stu-id="31b1a-173">The easiest way for you to set SPNs is to follow the SPN formats that may already be present for your sites.</span></span> <span data-ttu-id="31b1a-174">Copie esses SPNs a serem registrados na conta de serviço.</span><span class="sxs-lookup"><span data-stu-id="31b1a-174">Copy those SPNs to register against the service account.</span></span> <span data-ttu-id="31b1a-175">Para fazer isso:</span><span class="sxs-lookup"><span data-stu-id="31b1a-175">To do this:</span></span>

1. <span data-ttu-id="31b1a-176">Navegue até o site com o SPN de outro computador.</span><span class="sxs-lookup"><span data-stu-id="31b1a-176">Browse to the site with the SPN from another machine.</span></span>
 <span data-ttu-id="31b1a-177">Quando você faz isso, o conjunto relevante de tíquetes Kerberos são armazenados em cache no computador.</span><span class="sxs-lookup"><span data-stu-id="31b1a-177">When you do, the relevant set of Kerberos tickets is cached on the machine.</span></span> <span data-ttu-id="31b1a-178">Esses tíquetes contêm o SPN do local de destino para o qual você navegou.</span><span class="sxs-lookup"><span data-stu-id="31b1a-178">These tickets contain the SPN of the target site that you browsed to.</span></span>

2. <span data-ttu-id="31b1a-179">Podemos extrair o SPN desse site usando uma ferramenta chamada [Klist](http://web.mit.edu/kerberos/krb5-devel/doc/user/user_commands/klist.html).</span><span class="sxs-lookup"><span data-stu-id="31b1a-179">You can pull the SPN for that site by using a tool called [Klist](http://web.mit.edu/kerberos/krb5-devel/doc/user/user_commands/klist.html).</span></span> <span data-ttu-id="31b1a-180">Em uma janela Comando em execução no mesmo contexto do usuário que acessou o site no navegador, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="31b1a-180">In a command window that's running in the same context as the user who accessed the site in the browser, run the following command:</span></span>
```
Klist
```
<span data-ttu-id="31b1a-181">Klist retorna então o conjunto de SPNs de destino.</span><span class="sxs-lookup"><span data-stu-id="31b1a-181">Klist then returns the set of target SPNs.</span></span> <span data-ttu-id="31b1a-182">Neste exemplo, o valor realçado é o SPN necessário:</span><span class="sxs-lookup"><span data-stu-id="31b1a-182">In this example, the highlighted value is the SPN that's needed:</span></span>

  ![Resultados do Klist de exemplo](./media/application-proxy-remote-sharepoint/remote-sharepoint-target-service.png)

4. <span data-ttu-id="31b1a-184">Agora que você tem o SPN, é preciso ter certeza de que ele está configurado corretamente na conta de serviço que você configurou anteriormente para o Aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="31b1a-184">Now that you have the SPN, you need to make sure that it's configured correctly on the service account that you set up for the web application earlier.</span></span> <span data-ttu-id="31b1a-185">Execute o comando a seguir no prompt de comando como um administrador do domínio:</span><span class="sxs-lookup"><span data-stu-id="31b1a-185">Run the following command from the command prompt as an administrator of the domain:</span></span>

 ```
 setspn -S http/sharepoint.demo.o365identity.us demo\sp_svc
 ```

 <span data-ttu-id="31b1a-186">Esse comando define o SPN para a conta de serviço do SharePoint em execução como _demo\sp_svc_.</span><span class="sxs-lookup"><span data-stu-id="31b1a-186">This command sets the SPN for the SharePoint service account running as _demo\sp_svc_.</span></span>

 <span data-ttu-id="31b1a-187">Substitua _http/sharepoint.demo.o365identity.us_ pelo SPN do seu servidor e _demo\sp_svc_ pela conta de serviço no seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="31b1a-187">Replace _http/sharepoint.demo.o365identity.us_ with the SPN for your server and _demo\sp_svc_ with the service account in your environment.</span></span> <span data-ttu-id="31b1a-188">O comando Setspn pesquisa pelo SPN antes de adicioná-lo.</span><span class="sxs-lookup"><span data-stu-id="31b1a-188">The Setspn command searches for the SPN before it adds it.</span></span> <span data-ttu-id="31b1a-189">Nesse caso, você poderá ver um erro **Valor de SPN duplicado**.</span><span class="sxs-lookup"><span data-stu-id="31b1a-189">In this case, you might see a **Duplicate SPN Value** error.</span></span> <span data-ttu-id="31b1a-190">Caso esse erro seja exibido, verifique se o valor está associado à conta de serviço.</span><span class="sxs-lookup"><span data-stu-id="31b1a-190">If you see this error, make sure that the value is associated with the service account.</span></span>

<span data-ttu-id="31b1a-191">Você pode verificar se o SPN foi adicionado executando o comando Setspn com a opção -I.</span><span class="sxs-lookup"><span data-stu-id="31b1a-191">You can verify that the SPN was added by running the Setspn command with the -l option.</span></span> <span data-ttu-id="31b1a-192">Para saber mais sobre esse comando, confira [Setspn](https://technet.microsoft.com/library/cc731241.aspx).</span><span class="sxs-lookup"><span data-stu-id="31b1a-192">To learn more about this command, see [Setspn](https://technet.microsoft.com/library/cc731241.aspx).</span></span>

### <a name="ensure-that-the-connector-is-set-as-a-trusted-delegate-to-sharepoint"></a><span data-ttu-id="31b1a-193">Certificar-se de que o conector está definido como um delegado confiável para o SharePoint</span><span class="sxs-lookup"><span data-stu-id="31b1a-193">Ensure that the connector is set as a trusted delegate to SharePoint</span></span>

<span data-ttu-id="31b1a-194">Configure a KCD para que o serviço Proxy de Aplicativo do Azure AD seja capaz de delegar identidades do usuário ao serviço do SharePoint.</span><span class="sxs-lookup"><span data-stu-id="31b1a-194">Configure the KCD so that the Azure AD Application Proxy service can delegate user identities to the SharePoint service.</span></span> <span data-ttu-id="31b1a-195">Faça isso habilitando o conector Proxy de Aplicativo para recuperar tíquetes Kerberos para seus usuários que foram autenticados no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="31b1a-195">You do this by enabling the Application Proxy connector to retrieve Kerberos tickets for your users who have been authenticated in Azure AD.</span></span> <span data-ttu-id="31b1a-196">Em seguida, esse servidor passa o contexto ao aplicativo de destino, ou o SharePoint, nesse caso.</span><span class="sxs-lookup"><span data-stu-id="31b1a-196">Then that server passes the context to the target application, or SharePoint in this case.</span></span>

<span data-ttu-id="31b1a-197">Para configurar a KCD, repita as etapas a seguir para cada computador conector:</span><span class="sxs-lookup"><span data-stu-id="31b1a-197">To configure the KCD, repeat the following steps for each connector machine:</span></span>

1. <span data-ttu-id="31b1a-198">Faça logon como um administrador de domínio em um DC e abra **Usuários e Computadores do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="31b1a-198">Log in as a domain administrator to a DC, and then open **Active Directory Users and Computers**.</span></span>
2. <span data-ttu-id="31b1a-199">Encontre o computador em que o conector está em sendo executado.</span><span class="sxs-lookup"><span data-stu-id="31b1a-199">Find the computer that the connector is running on.</span></span> <span data-ttu-id="31b1a-200">Neste exemplo, ele é o mesmo servidor do SharePoint.</span><span class="sxs-lookup"><span data-stu-id="31b1a-200">In this example, it's the same SharePoint server.</span></span>
3. <span data-ttu-id="31b1a-201">Clique duas vezes no computador e então clique na guia **Delegação**.</span><span class="sxs-lookup"><span data-stu-id="31b1a-201">Double-click the computer, and then click the **Delegation** tab.</span></span>
4. <span data-ttu-id="31b1a-202">Verifique se as configurações de delegações estão definidas como **Confiar neste computador para delegação somente para os serviços especificados** e selecione **Usar qualquer protocolo de autenticação**.</span><span class="sxs-lookup"><span data-stu-id="31b1a-202">Ensure that the delegation settings are set to **Trust this computer for delegation to the specified services only**, and then select **Use any authentication protocol**.</span></span>

  ![Configurações de delegação](./media/application-proxy-remote-sharepoint/remote-sharepoint-delegation-box.png)

5. <span data-ttu-id="31b1a-204">Clique no botão **Adicionar**, clique em **Usuários ou Computadores** e localize a conta de serviço.</span><span class="sxs-lookup"><span data-stu-id="31b1a-204">Click the **Add** button, click **Users or Computers**, and locate the service account.</span></span>

  ![Adicionar o SPN à conta de serviço](./media/application-proxy-remote-sharepoint/remote-sharepoint-users-computers.png)

6. <span data-ttu-id="31b1a-206">Na lista de SPNs, selecione aquele que você criou anteriormente para a conta de serviço.</span><span class="sxs-lookup"><span data-stu-id="31b1a-206">In the list of SPNs, select the one that you created earlier for the service account.</span></span>
7. <span data-ttu-id="31b1a-207">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="31b1a-207">Click **OK**.</span></span> <span data-ttu-id="31b1a-208">Clique em **OK** novamente para salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="31b1a-208">Click **OK** again to save the changes.</span></span>

## <a name="step-2-enable-remote-access-to-sharepoint"></a><span data-ttu-id="31b1a-209">Etapa 2: Habilitar acesso remoto ao SharePoint</span><span class="sxs-lookup"><span data-stu-id="31b1a-209">Step 2: Enable remote access to SharePoint</span></span>

<span data-ttu-id="31b1a-210">Agora, com o SharePoint para Kerberos habilitado e a KCD configurada, você está pronto para configurar o logon único para o SharePoint.</span><span class="sxs-lookup"><span data-stu-id="31b1a-210">Now that you’ve enabled SharePoint for Kerberos and configured KCD, you're ready to set up single sign-on to SharePoint.</span></span> <span data-ttu-id="31b1a-211">No conector, você pode publicar o farm do SharePoint para acesso remoto por meio do Proxy de Aplicativo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="31b1a-211">Then from the connector, you can publish the SharePoint farm for remote access through Azure AD Application Proxy.</span></span>

<span data-ttu-id="31b1a-212">Para executar as etapas a seguir, você precisa ser um membro da Função Administrador Global na conta do Azure Active Directory da sua organização.</span><span class="sxs-lookup"><span data-stu-id="31b1a-212">To perform the following steps, you need to be a member of the Global Administrator Role in your organization's Azure Active Directory account.</span></span>

1. <span data-ttu-id="31b1a-213">Entre no [Portal do Azure](https://manage.windowsazure.com) e localize seu locatário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="31b1a-213">Sign in to the [Azure portal](https://manage.windowsazure.com) and find your Azure AD tenant.</span></span>
2. <span data-ttu-id="31b1a-214">Clique em **Aplicativos** e em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="31b1a-214">Click **Applications**, and then click **Add**.</span></span>
3. <span data-ttu-id="31b1a-215">Selecione **Publicar um aplicativo que estará acessível fora de sua rede**.</span><span class="sxs-lookup"><span data-stu-id="31b1a-215">Select **Publish an application that will be accessible from outside your network**.</span></span> <span data-ttu-id="31b1a-216">Caso não visualize essa opção, verifique se você configurou o Azure AD Básico ou Premium no locatário.</span><span class="sxs-lookup"><span data-stu-id="31b1a-216">If you don’t see this option, make sure that you have Azure AD Basic or Premium set up in the tenant.</span></span>
4. <span data-ttu-id="31b1a-217">Preencha cada uma das opções como demonstrado a seguir:</span><span class="sxs-lookup"><span data-stu-id="31b1a-217">Complete each of the options as follows:</span></span>
 * <span data-ttu-id="31b1a-218">**Nome**: use qualquer valor que você queira, por exemplo, **SharePoint**.</span><span class="sxs-lookup"><span data-stu-id="31b1a-218">**Name**: Use any value that you want--for example, **SharePoint**.</span></span>
 * <span data-ttu-id="31b1a-219">**URL interna**: essa é a URL do site do SharePoint internamente, como **https://SharePoint/**.</span><span class="sxs-lookup"><span data-stu-id="31b1a-219">**Internal URL**: This is the URL of the SharePoint site internally, such as **https://SharePoint/**.</span></span> <span data-ttu-id="31b1a-220">Neste exemplo, certifique-se de usar **https**.</span><span class="sxs-lookup"><span data-stu-id="31b1a-220">In this example, make sure to use **https**.</span></span>
 * <span data-ttu-id="31b1a-221">**Método de Pré-autenticação**: selecione **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="31b1a-221">**Preauthentication Method**: Select **Azure Active Directory**.</span></span>

  ![Opções para adicionar um aplicativo](./media/application-proxy-remote-sharepoint/remote-sharepoint-add-application.png)

5. <span data-ttu-id="31b1a-223">Depois que o aplicativo for publicado, clique na guia **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="31b1a-223">After the app is published, click the **Configure** tab.</span></span>
6. <span data-ttu-id="31b1a-224">Role para baixo até a opção **Traduzir URL nos Cabeçalhos**.</span><span class="sxs-lookup"><span data-stu-id="31b1a-224">Scroll down to the option **Translate URL in Headers**.</span></span> <span data-ttu-id="31b1a-225">O valor padrão é **SIM**.</span><span class="sxs-lookup"><span data-stu-id="31b1a-225">The default value is **YES**.</span></span> <span data-ttu-id="31b1a-226">Altere-o para **NÃO**.</span><span class="sxs-lookup"><span data-stu-id="31b1a-226">Change it to **NO**.</span></span>

 <span data-ttu-id="31b1a-227">O SharePoint usa o valor _Cabeçalho de Host_ para pesquisar o site.</span><span class="sxs-lookup"><span data-stu-id="31b1a-227">SharePoint uses the _Host Header_ value to look up the site.</span></span> <span data-ttu-id="31b1a-228">Ele também gera links com base nesse valor.</span><span class="sxs-lookup"><span data-stu-id="31b1a-228">It also generates links based on this value.</span></span> <span data-ttu-id="31b1a-229">O resultado final é a certeza de que qualquer link que o SharePoint gere será uma URL publicada corretamente definida para usar a URL externa.</span><span class="sxs-lookup"><span data-stu-id="31b1a-229">The net effect is to make sure that any link that SharePoint generates is a published URL that is correctly set to use the external URL.</span></span> <span data-ttu-id="31b1a-230">Configurar o valor para **SIM** também permite que o conector encaminhe a solicitação ao aplicativo de back-end.</span><span class="sxs-lookup"><span data-stu-id="31b1a-230">Setting the value to **YES** also enables the connector to forward the request to the back-end application.</span></span> <span data-ttu-id="31b1a-231">No entanto, configurar o valor como **NÃO** significa que o conector não enviará o nome de host interno.</span><span class="sxs-lookup"><span data-stu-id="31b1a-231">However, setting the value to **NO** means that the connector will not send the internal host name.</span></span> <span data-ttu-id="31b1a-232">Em vez disso, o conector envia o cabeçalho do host como a URL publicada para o aplicativo de back-end.</span><span class="sxs-lookup"><span data-stu-id="31b1a-232">Instead, the connector sends the host header as the published URL to the back-end application.</span></span>

 <span data-ttu-id="31b1a-233">Além disso, para garantir que o SharePoint aceite essa URL, você precisa concluir mais uma configuração no servidor do SharePoint.</span><span class="sxs-lookup"><span data-stu-id="31b1a-233">Also, to ensure that SharePoint accepts this URL, you need to complete one more configuration on the SharePoint server.</span></span> <span data-ttu-id="31b1a-234">Você fará isso na próxima seção.</span><span class="sxs-lookup"><span data-stu-id="31b1a-234">You'll do that in the next section.</span></span>

7. <span data-ttu-id="31b1a-235">Defina o **Método de Autenticação Interna** como **Autenticação Integrada do Windows**.</span><span class="sxs-lookup"><span data-stu-id="31b1a-235">Change **Internal Authentication Method** to **Integrated Windows Authentication**.</span></span> <span data-ttu-id="31b1a-236">Se seu locatário do Azure AD usar um UPN na nuvem diferente do UPN local, lembre-se de atualizar também a **Identidade de Logon Delegada**.</span><span class="sxs-lookup"><span data-stu-id="31b1a-236">If your Azure AD tenant uses a UPN in the cloud that's different from the UPN on-premises, remember to update **Delegated Login Identity** as well.</span></span>
8. <span data-ttu-id="31b1a-237">Defina o **SPN do Aplicativo Interno** para o valor que você definiu anteriormente.</span><span class="sxs-lookup"><span data-stu-id="31b1a-237">Set **Internal Application SPN** to the value that you set earlier.</span></span> <span data-ttu-id="31b1a-238">Por exemplo, **http/sharepoint.demo.o365identity.us**.</span><span class="sxs-lookup"><span data-stu-id="31b1a-238">For example, use **http/sharepoint.demo.o365identity.us**.</span></span>
9. <span data-ttu-id="31b1a-239">Atribua o aplicativo aos usuários de destino.</span><span class="sxs-lookup"><span data-stu-id="31b1a-239">Assign the application to your target users.</span></span>

<span data-ttu-id="31b1a-240">Seu aplicativo deve ser semelhante ao seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="31b1a-240">Your application should look similar to the following example:</span></span>

  ![Aplicativo concluído](./media/application-proxy-remote-sharepoint/remote-sharepoint-internal-application-spn.png)

## <a name="step-3-ensure-that-sharepoint-knows-about-the-external-url"></a><span data-ttu-id="31b1a-242">Etapa 3: assegurar que o SharePoint saiba sobre a URL externa</span><span class="sxs-lookup"><span data-stu-id="31b1a-242">Step 3: Ensure that SharePoint knows about the external URL</span></span>

<span data-ttu-id="31b1a-243">A última etapa é assegurar que o SharePoint possa localizar o site com base na URL externa, assim, ele renderizará links baseados nessa URL externa.</span><span class="sxs-lookup"><span data-stu-id="31b1a-243">Your last step to ensure that SharePoint can find the site based on the external URL, so that it will render links based on that external URL.</span></span> <span data-ttu-id="31b1a-244">Faça isso configurando mapeamentos alternativos de acesso para o site do SharePoint.</span><span class="sxs-lookup"><span data-stu-id="31b1a-244">You do this by configuring alternate access mappings for the SharePoint site.</span></span>

1. <span data-ttu-id="31b1a-245">Abra o site **Administração Central do SharePoint 2013**.</span><span class="sxs-lookup"><span data-stu-id="31b1a-245">Open the **SharePoint 2013 Central Administration** site.</span></span>
2. <span data-ttu-id="31b1a-246">Em **Configurações do Sistema**, selecione **Configurar Mapeamentos Alternativos de Acesso**.</span><span class="sxs-lookup"><span data-stu-id="31b1a-246">Under **System Settings**, select **Configure Alternate Access Mappings**.</span></span>

 <span data-ttu-id="31b1a-247">Isso abre a caixa **Mapeamentos Alternativos de Acesso**.</span><span class="sxs-lookup"><span data-stu-id="31b1a-247">This opens the **Alternate Access Mappings** box.</span></span>

  ![Caixa Mapeamentos Alternativos de Acesso](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access1.png)

3. <span data-ttu-id="31b1a-249">Na lista suspensa ao lado de **Coleções de Mapeamentos Alternativos de Acesso**, selecione **Alterar Coleção de Mapeamentos Alternativos de Acesso**.</span><span class="sxs-lookup"><span data-stu-id="31b1a-249">In the drop-down list beside **Alternate Access Mapping Collection**, select **Change Alternate Access Mapping Collection**.</span></span>
4. <span data-ttu-id="31b1a-250">Selecione o seu site, por exemplo **SharePoint – 80**.</span><span class="sxs-lookup"><span data-stu-id="31b1a-250">Select your site--for example, **SharePoint - 80**.</span></span>

  ![Selecionar um site](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access2.png)

5. <span data-ttu-id="31b1a-252">Você pode optar por adicionar a URL publicada como uma URL interna ou uma URL pública.</span><span class="sxs-lookup"><span data-stu-id="31b1a-252">You can choose to add the published URL as either an internal URL or a public URL.</span></span> <span data-ttu-id="31b1a-253">Este exemplo usa uma URL pública como a extranet.</span><span class="sxs-lookup"><span data-stu-id="31b1a-253">This example uses a public URL as the extranet.</span></span>
6. <span data-ttu-id="31b1a-254">Clique em **Editar URLs Públicas** no caminho **Extranet** e insira o caminho para o aplicativo publicado, como na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="31b1a-254">Click **Edit Public URLs** in the **Extranet** path, and then enter the path for the published application, as in the previous step.</span></span> <span data-ttu-id="31b1a-255">Por exemplo, **https://sharepoint-iddemo.msappproxy.net**.</span><span class="sxs-lookup"><span data-stu-id="31b1a-255">For example, enter **https://sharepoint-iddemo.msappproxy.net**.</span></span>

  ![Inserindo o caminho](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access3.png)

7. <span data-ttu-id="31b1a-257">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="31b1a-257">Click **Save**.</span></span>

 <span data-ttu-id="31b1a-258">Agora você pode acessar o site do SharePoint externamente por meio do Proxy de Aplicativo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="31b1a-258">You can now access the SharePoint site externally via Azure AD Application Proxy.</span></span>

## <a name="next-steps"></a><span data-ttu-id="31b1a-259">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="31b1a-259">Next steps</span></span>

- [<span data-ttu-id="31b1a-260">Como fornecer acesso remoto seguro a aplicativos locais</span><span class="sxs-lookup"><span data-stu-id="31b1a-260">How to provide secure remote access to on-premises applications</span></span>](active-directory-application-proxy-get-started.md)
- [<span data-ttu-id="31b1a-261">Noções básicas sobre conectores de Proxy de Aplicativo do Azure AD</span><span class="sxs-lookup"><span data-stu-id="31b1a-261">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
- [<span data-ttu-id="31b1a-262">Publicando o SharePoint 2016 e o Servidor do Office Online com o Proxy de Aplicativo do Azure AD</span><span class="sxs-lookup"><span data-stu-id="31b1a-262">Publishing SharePoint 2016 and Office Online Server with Azure AD Application Proxy</span></span>](https://blogs.technet.microsoft.com/dawiese/2016/06/09/publishing-sharepoint-2016-and-office-online-server-with-azure-ad-application-proxy/)
