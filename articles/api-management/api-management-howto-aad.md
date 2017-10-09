---
title: contas de desenvolvedor aaaAuthorize usando o Active Directory do Azure - gerenciamento de API do Azure | Microsoft Docs
description: "Saiba como tooauthorize usuários usando o Active Directory do Azure no gerenciamento de API."
services: api-management
documentationcenter: API Management
author: steved0x
manager: erikre
editor: 
ms.assetid: 33a69a83-94f2-4e4e-9cef-f2a5af3c9732
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: ebf5447a509a47df35e4262138bfcf423cb1dd5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-using-azure-active-directory-in-azure-api-management"></a><span data-ttu-id="6e393-103">Como desenvolvedor de tooauthorize contas usando Active Directory do Azure no gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="6e393-103">How tooauthorize developer accounts using Azure Active Directory in Azure API Management</span></span>
## <a name="overview"></a><span data-ttu-id="6e393-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="6e393-104">Overview</span></span>
<span data-ttu-id="6e393-105">Este guia mostra como tooenable acessar o portal do desenvolvedor toohello para os usuários do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="6e393-105">This guide shows you how tooenable access toohello developer portal for users from Azure Active Directory.</span></span> <span data-ttu-id="6e393-106">Este guia também mostra como toomanage grupos de usuários do Active Directory do Azure, adicionando grupos externos que contêm Olá usuários do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="6e393-106">This guide also shows you how toomanage groups of Azure Active Directory users by adding external groups that contain hello users of an Azure Active Directory.</span></span>

> <span data-ttu-id="6e393-107">Olá toocomplete as etapas neste guia primeiro você deve ter um Azure Active Directory no qual toocreate um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6e393-107">toocomplete hello steps in this guide you must first have an Azure Active Directory in which toocreate an application.</span></span>
> 
> 

## <a name="how-tooauthorize-developer-accounts-using-azure-active-directory"></a><span data-ttu-id="6e393-108">Como desenvolvedor de tooauthorize contas usando Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="6e393-108">How tooauthorize developer accounts using Azure Active Directory</span></span>
<span data-ttu-id="6e393-109">tooget iniciado, clique em **portal do publicador** no portal do Azure para seu serviço de gerenciamento de API de saudação.</span><span class="sxs-lookup"><span data-stu-id="6e393-109">tooget started, click **Publisher portal** in hello Azure portal for your API Management service.</span></span> <span data-ttu-id="6e393-110">Isso leva toohello portal do publicador de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="6e393-110">This takes you toohello API Management publisher portal.</span></span>

![Portal do editor][api-management-management-console]

> <span data-ttu-id="6e393-112">Se você ainda não tiver criado uma instância do serviço de gerenciamento de API, consulte [criar uma instância do serviço de gerenciamento de API] [ Create an API Management service instance] em Olá [Introdução ao gerenciamento de API do Azure] [ Get started with Azure API Management] tutorial.</span><span class="sxs-lookup"><span data-stu-id="6e393-112">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="6e393-113">Clique em **segurança** de saudação **gerenciamento de API** menu Olá esquerda e clique em **identidades externas**.</span><span class="sxs-lookup"><span data-stu-id="6e393-113">Click **Security** from hello **API Management** menu on hello left and click **External Identities**.</span></span>

![Identidades externas][api-management-security-external-identities]

<span data-ttu-id="6e393-115">Clique em **Active Directory do Azure**.</span><span class="sxs-lookup"><span data-stu-id="6e393-115">Click **Azure Active Directory**.</span></span> <span data-ttu-id="6e393-116">Anote Olá **URL de redirecionamento** e passar tooyour Active Directory do Azure no hello Portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="6e393-116">Make a note of hello **Redirect URL** and switch over tooyour Azure Active Directory in hello Azure Classic Portal.</span></span>

![Identidades externas][api-management-security-aad-new]

<span data-ttu-id="6e393-118">Clique em Olá **adicionar** botão toocreate um novo aplicativo do Active Directory do Azure e escolha **adicionar um aplicativo que minha organização esteja desenvolvendo**.</span><span class="sxs-lookup"><span data-stu-id="6e393-118">Click hello **Add** button toocreate a new Azure Active Directory application, and choose **Add an application my organization is developing**.</span></span>

![Adicionar novo aplicativo do Active Directory do Azure][api-management-new-aad-application-menu]

<span data-ttu-id="6e393-120">Insira um nome para o aplicativo hello, selecione **Web aplicativo e/ou API da Web**e clique no botão Avançar hello.</span><span class="sxs-lookup"><span data-stu-id="6e393-120">Enter a name for hello application, select **Web application and/or Web API**, and click hello next button.</span></span>

![Novo aplicativo do Active Directory do Azure][api-management-new-aad-application-1]

<span data-ttu-id="6e393-122">Para **URL de logon**, digite Olá URL de entrada de seu portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="6e393-122">For **Sign-on URL**, enter hello sign-on URL of your developer portal.</span></span> <span data-ttu-id="6e393-123">Neste exemplo, Olá **URL de logon** é `https://aad03.portal.current.int-azure-api.net/signin`.</span><span class="sxs-lookup"><span data-stu-id="6e393-123">In this example, hello **Sign-on URL** is `https://aad03.portal.current.int-azure-api.net/signin`.</span></span> 

<span data-ttu-id="6e393-124">Para Olá **URL de ID do aplicativo**, insira o saudação padrão domínio ou um domínio personalizado para Olá Active Directory do Azure e acrescentar tooit uma cadeia de caracteres exclusiva.</span><span class="sxs-lookup"><span data-stu-id="6e393-124">For hello **App ID URL**, enter either hello default domain or a custom domain for hello Azure Active Directory, and append a unique string tooit.</span></span> <span data-ttu-id="6e393-125">Neste exemplo, Olá domínio padrão de **https://contoso5api.onmicrosoft.com** é usado com o sufixo de saudação do **/api** especificado.</span><span class="sxs-lookup"><span data-stu-id="6e393-125">In this example, hello default domain of **https://contoso5api.onmicrosoft.com** is used with hello suffix of **/api** specified.</span></span>

![Propriedades do novo aplicativo do Active Directory do Azure][api-management-new-aad-application-2]

<span data-ttu-id="6e393-127">Clique em toosave de botão de seleção hello e criar o aplicativo hello e alternar toohello **configurar** guia aplicativo novo do tooconfigure hello.</span><span class="sxs-lookup"><span data-stu-id="6e393-127">Click hello check button toosave and create hello application, and switch toohello **Configure** tab tooconfigure hello new application.</span></span>

![Novo aplicativo do Active Directory do Azure criado][api-management-new-aad-app-created]

<span data-ttu-id="6e393-129">Se vários Active Directories do Azure for toobe usado para esse aplicativo, clique em **Sim** para **aplicativo é multilocatário**.</span><span class="sxs-lookup"><span data-stu-id="6e393-129">If multiple Azure Active Directories are going toobe used for this application, click **Yes** for **Application is multi-tenant**.</span></span> <span data-ttu-id="6e393-130">saudação padrão é **não**.</span><span class="sxs-lookup"><span data-stu-id="6e393-130">hello default is **No**.</span></span>

![Aplicativo é multilocatário][api-management-aad-app-multi-tenant]

<span data-ttu-id="6e393-132">Saudação de cópia **URL de redirecionamento** de saudação **Active Directory do Azure** seção Olá **identidades externas** guia no portal do publicador hello e cole-a saudação **URL de resposta** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="6e393-132">Copy hello **Redirect URL** from hello **Azure Active Directory** section of hello **External Identities** tab in hello publisher portal and paste it into hello **Reply URL** text box.</span></span> 

![URL de resposta][api-management-aad-reply-url]

<span data-ttu-id="6e393-134">Rolar para o fim da saudação toohello configurar guia, selecione Olá **permissões de aplicativo** lista suspensa e verifique **ler dados do diretório**.</span><span class="sxs-lookup"><span data-stu-id="6e393-134">Scroll toohello bottom of hello configure tab, select hello **Application Permissions** drop-down, and check **Read directory data**.</span></span>

![Permissões de aplicativo][api-management-aad-app-permissions]

<span data-ttu-id="6e393-136">Selecione Olá **delegar permissões** lista suspensa e verifique **habilitar logon e ler perfis dos usuários**.</span><span class="sxs-lookup"><span data-stu-id="6e393-136">Select hello **Delegate Permissions** drop-down, and check **Enable sign-on and read users' profiles**.</span></span>

![Permissões delegadas][api-management-aad-delegated-permissions]

> <span data-ttu-id="6e393-138">Para obter mais informações sobre o aplicativo e as permissões delegadas, consulte [acessando Olá Graph API][Accessing hello Graph API].</span><span class="sxs-lookup"><span data-stu-id="6e393-138">For more information about application and delegated permissions, see [Accessing hello Graph API][Accessing hello Graph API].</span></span>
> 
> 

<span data-ttu-id="6e393-139">Saudação de cópia **Id do cliente** toohello área de transferência.</span><span class="sxs-lookup"><span data-stu-id="6e393-139">Copy hello **Client Id** toohello clipboard.</span></span>

![Id do Cliente][api-management-aad-app-client-id]

<span data-ttu-id="6e393-141">Alternar o portal do publicador toohello voltar e cole no hello **Id do cliente** copiado da configuração de aplicativo do Active Directory do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="6e393-141">Switch back toohello publisher portal and paste in hello **Client Id** copied from hello Azure Active Directory application configuration.</span></span>

![Id do Cliente][api-management-client-id]

<span data-ttu-id="6e393-143">Alternar a configuração do Active Directory do Azure toohello voltar e, em seguida, clique em Olá **selecionar duração** suspensa no hello **chaves** seção e especificar um intervalo.</span><span class="sxs-lookup"><span data-stu-id="6e393-143">Switch back toohello Azure Active Directory configuration, and click hello **Select duration** drop-down in hello **Keys** section and specify an interval.</span></span> <span data-ttu-id="6e393-144">Neste exemplo, **1 ano** é usado.</span><span class="sxs-lookup"><span data-stu-id="6e393-144">In this example, **1 year** is used.</span></span>

![Chave][api-management-aad-key-before-save]

<span data-ttu-id="6e393-146">Clique em **salvar** toosave Olá configuração e exibição Olá a chave.</span><span class="sxs-lookup"><span data-stu-id="6e393-146">Click **Save** toosave hello configuration and display hello key.</span></span> <span data-ttu-id="6e393-147">Copiar Olá chave toohello área de transferência.</span><span class="sxs-lookup"><span data-stu-id="6e393-147">Copy hello key toohello clipboard.</span></span>

> <span data-ttu-id="6e393-148">Anote esta chave.</span><span class="sxs-lookup"><span data-stu-id="6e393-148">Make a note of this key.</span></span> <span data-ttu-id="6e393-149">Quando você fechar a janela de configuração do Active Directory do Azure hello, chave de saudação não pode ser exibida novamente.</span><span class="sxs-lookup"><span data-stu-id="6e393-149">Once you close hello Azure Active Directory configuration window, hello key cannot be displayed again.</span></span>
> 
> 

![Chave][api-management-aad-key-after-save]

<span data-ttu-id="6e393-151">Switch back toohello publicador portal e colar Olá chave em Olá **segredo do cliente** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="6e393-151">Switch back toohello publisher portal and paste hello key into hello **Client Secret** text box.</span></span>

![Segredo do cliente][api-management-client-secret]

<span data-ttu-id="6e393-153">**Permitido locatários** Especifica os diretórios que têm acesso toohello APIs da instância de serviço de gerenciamento de API de saudação.</span><span class="sxs-lookup"><span data-stu-id="6e393-153">**Allowed Tenants** specifies which directories have access toohello APIs of hello API Management service instance.</span></span> <span data-ttu-id="6e393-154">Especifique domínios de saudação do hello toowhich de instâncias do Active Directory do Azure você deseja acesso toogrant.</span><span class="sxs-lookup"><span data-stu-id="6e393-154">Specify hello domains of hello Azure Active Directory instances toowhich you want toogrant access.</span></span> <span data-ttu-id="6e393-155">Você pode separar múltiplos domínios com novas linhas, espaços ou vírgulas.</span><span class="sxs-lookup"><span data-stu-id="6e393-155">You can separate multiple domains with newlines, spaces, or commas.</span></span>

![Locatários permitidos][api-management-client-allowed-tenants]


<span data-ttu-id="6e393-157">Depois de saudação desejado a configuração for especificada, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="6e393-157">Once hello desired configuration is specified, click **Save**.</span></span>

![Salvar][api-management-client-allowed-tenants-save]

<span data-ttu-id="6e393-159">Depois de saudação alterações são salvas, usuários Olá Olá especificaram do Active Directory do Azure pode entrar no portal do desenvolvedor toohello, seguindo as etapas de saudação em [fazer logon no portal do desenvolvedor toohello usando uma conta do Active Directory do Azure] [Log in toohello Developer portal using an Azure Active Directory account].</span><span class="sxs-lookup"><span data-stu-id="6e393-159">Once hello changes are saved, hello users in hello specified Azure Active Directory can sign in toohello Developer portal by following hello steps in [Log in toohello Developer portal using an Azure Active Directory account][Log in toohello Developer portal using an Azure Active Directory account].</span></span>

<span data-ttu-id="6e393-160">Vários domínios podem ser especificados em Olá **permitido locatários** seção.</span><span class="sxs-lookup"><span data-stu-id="6e393-160">Multiple domains can be specified in hello **Allowed Tenants** section.</span></span> <span data-ttu-id="6e393-161">Antes de qualquer usuário pode fazer logon de um domínio diferente Olá original em que o aplicativo hello foi registrado, um administrador global do domínio diferente da saudação deve conceder permissão para Olá aplicativo tooaccess dados do diretório.</span><span class="sxs-lookup"><span data-stu-id="6e393-161">Before any user can log in from a different domain than hello original domain where hello application was registered, a global administrator of hello different domain must grant permission for hello application tooaccess directory data.</span></span> <span data-ttu-id="6e393-162">permissão de toogrant administrador global Olá deve ir muito`https://<URL of your developer portal>/aadadminconsent` (por exemplo, https://contoso.portal.azure-api.net/aadadminconsent), digite nome de domínio de saudação de Olá locatário do Active Directory que desejam toogive acesso tooand clique em enviar.</span><span class="sxs-lookup"><span data-stu-id="6e393-162">toogrant permission, hello global administrator should go too`https://<URL of your developer portal>/aadadminconsent` (for example, https://contoso.portal.azure-api.net/aadadminconsent), type in hello domain name of hello Active Directory tenant they want toogive access tooand click Submit.</span></span> <span data-ttu-id="6e393-163">Seguir Olá exemplo, um administrador global do `miaoaad.onmicrosoft.com` está tentando o portal do desenvolvedor específico de toothis de permissão de toogive.</span><span class="sxs-lookup"><span data-stu-id="6e393-163">In hello following example, a global administrator from `miaoaad.onmicrosoft.com` is trying toogive permission toothis particular developer portal.</span></span> 

![Permissões][api-management-aad-consent]

<span data-ttu-id="6e393-165">Na próxima tela de Olá, administrador global Olá serão solicitada tooconfirm a concessão de permissão de saudação.</span><span class="sxs-lookup"><span data-stu-id="6e393-165">In hello next screen, hello global administrator will be prompted tooconfirm giving hello permission.</span></span> 

![Permissões][api-management-permissions-form]

> <span data-ttu-id="6e393-167">Se um administrador global não tenta toolog em antes de permissões são concedidas por um administrador global, Olá tentativa de logon falhar e uma tela de erro é exibida.</span><span class="sxs-lookup"><span data-stu-id="6e393-167">If a non-global administrator tries toolog in before permissions are granted by a global administrator, hello login attempt fails and an error screen is displayed.</span></span>
> 
> 

## <a name="how-tooadd-an-external-azure-active-directory-group"></a><span data-ttu-id="6e393-168">Como tooadd um externas do Azure Active Directory agrupar</span><span class="sxs-lookup"><span data-stu-id="6e393-168">How tooadd an external Azure Active Directory Group</span></span>
<span data-ttu-id="6e393-169">Depois de habilitar o acesso de usuários no Active Directory do Azure, você pode adicionar grupos do Active Directory do Azure para gerenciamento de API toomore facilmente gerenciam associação de saudação de desenvolvedores Olá no grupo de saudação com produtos de saudação desejado.</span><span class="sxs-lookup"><span data-stu-id="6e393-169">After enabling access for users in an Azure Active Directory, you can add Azure Active Directory groups into API Management toomore easily manage hello association of hello developers in hello group with hello desired products.</span></span>

> <span data-ttu-id="6e393-170">tooconfigure um grupo externo do Active Directory do Azure, hello Azure Active Directory primeiro deve ser configurado no guia de identidades Olá pelo procedimento na seção anterior Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="6e393-170">tooconfigure an external Azure Active Directory group, hello Azure Active Directory must first be configured in hello Identities tab by following hello procedure in hello previous section.</span></span> 
> 
> 

<span data-ttu-id="6e393-171">Grupos externos do Active Directory do Azure são adicionados do hello **visibilidade** guia do produto Olá para o qual você deseja que o grupo de toohello toogrant acesso.</span><span class="sxs-lookup"><span data-stu-id="6e393-171">External Azure Active Directory groups are added from hello **Visibility** tab of hello product for which you wish toogrant access toohello group.</span></span> <span data-ttu-id="6e393-172">Clique em **produtos**e clique em nome de saudação do produto desejado hello.</span><span class="sxs-lookup"><span data-stu-id="6e393-172">Click **Products**, and then click hello name of hello desired product.</span></span>

![Configurar produto][api-management-configure-product]

<span data-ttu-id="6e393-174">Alternar toohello **visibilidade** guia e, em seguida, clique em **adicionar grupos do Active Directory do Azure**.</span><span class="sxs-lookup"><span data-stu-id="6e393-174">Switch toohello **Visibility** tab, and click **Add Groups from Azure Active Directory**.</span></span>

![Adicionar grupos][api-management-add-groups]

<span data-ttu-id="6e393-176">Selecione Olá **locatário do Azure Active Directory** da lista suspensa de saudação e, em seguida, nome de saudação de tipo de grupo desejado Olá Olá **grupos** toobe adicionado a caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="6e393-176">Select hello **Azure Active Directory Tenant** from hello drop-down list, and then type hello name of hello desired group in hello **Groups** toobe added text box.</span></span>

![Selecionar grupo][api-management-select-group]

<span data-ttu-id="6e393-178">Este nome de grupo pode ser encontrado na Olá **grupos** lista para Active Directory do Azure, conforme mostrado no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="6e393-178">This group name can be found in hello **Groups** list for your Azure Active Directory, as shown in hello following example.</span></span>

![Lista de grupos do Active Directory do Azure][api-management-aad-groups-list]

<span data-ttu-id="6e393-180">Clique em **adicionar** toovalidate Olá nome do grupo e adicione o grupo de saudação.</span><span class="sxs-lookup"><span data-stu-id="6e393-180">Click **Add** toovalidate hello group name and add hello group.</span></span> <span data-ttu-id="6e393-181">Neste exemplo, Olá **Contoso 5 desenvolvedores** grupo externo é adicionado.</span><span class="sxs-lookup"><span data-stu-id="6e393-181">In this example, hello **Contoso 5 Developers** external group is added.</span></span> 

![Grupo adicionado][api-management-aad-group-added]

<span data-ttu-id="6e393-183">Clique em **salvar** toosave Olá nova seleção de grupo.</span><span class="sxs-lookup"><span data-stu-id="6e393-183">Click **Save** toosave hello new group selection.</span></span>

<span data-ttu-id="6e393-184">Depois de um grupo do Active Directory do Azure foi configurado de um produto, é disponível toobe verificada em Olá **visibilidade** guia Olá outros produtos na instância de serviço de gerenciamento de API de saudação.</span><span class="sxs-lookup"><span data-stu-id="6e393-184">Once an Azure Active Directory group has been configured from one product, it is available toobe checked on hello **Visibility** tab for hello other products in hello API Management service instance.</span></span>

<span data-ttu-id="6e393-185">tooreview e configurar as propriedades de saudação para grupos externos quando eles foram adicionados, clique em nome de saudação do grupo Olá Olá **grupos** guia.</span><span class="sxs-lookup"><span data-stu-id="6e393-185">tooreview and configure hello properties for external groups once they have been added, click hello name of hello group from hello **Groups** tab.</span></span>

![Gerenciar grupos][api-management-groups]

<span data-ttu-id="6e393-187">Aqui você pode editar Olá **nome** e hello **descrição** do grupo de saudação.</span><span class="sxs-lookup"><span data-stu-id="6e393-187">From here you can edit hello **Name** and hello **Description** of hello group.</span></span>

![Editar grupo][api-management-edit-group]

<span data-ttu-id="6e393-189">Usuários de saudação configurado Active Directory do Azure pode entrar no modo de exibição e o portal do desenvolvedor toohello e assinar tooany grupos para os quais têm visibilidade seguindo instruções Olá Olá seção a seguir.</span><span class="sxs-lookup"><span data-stu-id="6e393-189">Users from hello configured Azure Active Directory can sign in toohello Developer portal and view and subscribe tooany groups for which they have visibility by following hello instructions in hello following section.</span></span>

## <a name="how-toolog-in-toohello-developer-portal-using-an-azure-active-directory-account"></a><span data-ttu-id="6e393-190">Como toolog no portal do desenvolvedor toohello usando uma conta do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="6e393-190">How toolog in toohello Developer portal using an Azure Active Directory account</span></span>
<span data-ttu-id="6e393-191">toolog no portal do desenvolvedor hello usando uma conta do Active Directory do Azure configurada nas seções anteriores do hello, abra uma nova janela de navegador usando Olá **URL de logon** na configuração de aplicativo do Active Directory hello e clique em **Active Directory do azure**.</span><span class="sxs-lookup"><span data-stu-id="6e393-191">toolog into hello Developer portal using an Azure Active Directory account configured in hello previous sections, open a new browser window using hello **Sign-on URL** from hello Active Directory application configuration, and click **Azure Active Directory**.</span></span>

![Portal do desenvolvedor][api-management-dev-portal-signin]

<span data-ttu-id="6e393-193">Insira as credenciais de saudação de um dos usuários de saudação no Active Directory do Azure e clique em **entrar**.</span><span class="sxs-lookup"><span data-stu-id="6e393-193">Enter hello credentials of one of hello users in your Azure Active Directory, and click **Sign in**.</span></span>

![Entrar][api-management-aad-signin]

<span data-ttu-id="6e393-195">Pode ser solicitado que você preencha um formulário de registro se qualquer informação adicional for necessária.</span><span class="sxs-lookup"><span data-stu-id="6e393-195">You may be prompted with a registration form if any additional information is required.</span></span> <span data-ttu-id="6e393-196">Preencha o formulário de registro hello e clique em **inscrever**.</span><span class="sxs-lookup"><span data-stu-id="6e393-196">Complete hello registration form and click **Sign up**.</span></span>

![Registro][api-management-complete-registration]

<span data-ttu-id="6e393-198">O usuário agora está conectado ao portal do desenvolvedor Olá para sua instância de serviço de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="6e393-198">Your user is now logged into hello developer portal for your API Management service instance.</span></span>

![Registro completo][api-management-registration-complete]

[api-management-management-console]: ./media/api-management-howto-aad/api-management-management-console.png
[api-management-security-external-identities]: ./media/api-management-howto-aad/api-management-security-external-identities.png
[api-management-security-aad-new]: ./media/api-management-howto-aad/api-management-security-aad-new.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-aad/api-management-new-aad-application-menu.png
[api-management-new-aad-application-1]: ./media/api-management-howto-aad/api-management-new-aad-application-1.png
[api-management-new-aad-application-2]: ./media/api-management-howto-aad/api-management-new-aad-application-2.png
[api-management-new-aad-app-created]: ./media/api-management-howto-aad/api-management-new-aad-app-created.png
[api-management-aad-app-permissions]: ./media/api-management-howto-aad/api-management-aad-app-permissions.png
[api-management-aad-app-client-id]: ./media/api-management-howto-aad/api-management-aad-app-client-id.png
[api-management-client-id]: ./media/api-management-howto-aad/api-management-client-id.png
[api-management-aad-key-before-save]: ./media/api-management-howto-aad/api-management-aad-key-before-save.png
[api-management-aad-key-after-save]: ./media/api-management-howto-aad/api-management-aad-key-after-save.png
[api-management-client-secret]: ./media/api-management-howto-aad/api-management-client-secret.png
[api-management-client-allowed-tenants]: ./media/api-management-howto-aad/api-management-client-allowed-tenants.png
[api-management-client-allowed-tenants-save]: ./media/api-management-howto-aad/api-management-client-allowed-tenants-save.png
[api-management-aad-delegated-permissions]: ./media/api-management-howto-aad/api-management-aad-delegated-permissions.png
[api-management-dev-portal-signin]: ./media/api-management-howto-aad/api-management-dev-portal-signin.png
[api-management-aad-signin]: ./media/api-management-howto-aad/api-management-aad-signin.png
[api-management-complete-registration]: ./media/api-management-howto-aad/api-management-complete-registration.png
[api-management-registration-complete]: ./media/api-management-howto-aad/api-management-registration-complete.png
[api-management-aad-app-multi-tenant]: ./media/api-management-howto-aad/api-management-aad-app-multi-tenant.png
[api-management-aad-reply-url]: ./media/api-management-howto-aad/api-management-aad-reply-url.png
[api-management-aad-consent]: ./media/api-management-howto-aad/api-management-aad-consent.png
[api-management-permissions-form]: ./media/api-management-howto-aad/api-management-permissions-form.png
[api-management-configure-product]: ./media/api-management-howto-aad/api-management-configure-product.png
[api-management-add-groups]: ./media/api-management-howto-aad/api-management-add-groups.png
[api-management-select-group]: ./media/api-management-howto-aad/api-management-select-group.png
[api-management-aad-groups-list]: ./media/api-management-howto-aad/api-management-aad-groups-list.png
[api-management-aad-group-added]: ./media/api-management-howto-aad/api-management-aad-group-added.png
[api-management-groups]: ./media/api-management-howto-aad/api-management-groups.png
[api-management-edit-group]: ./media/api-management-howto-aad/api-management-edit-group.png

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[Accessing hello Graph API]: http://msdn.microsoft.com/library/azure/dn132599.aspx#BKMK_Graph

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

[Log in toohello Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account

