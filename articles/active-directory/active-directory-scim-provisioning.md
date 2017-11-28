---
title: "aaaUsing sistema para o gerenciamento de identidade de domínio cruzado provisionar automaticamente os usuários e grupos do Active Directory do Azure tooapplications | Microsoft Docs"
description: "Active Directory do Azure podem provisionar automaticamente os usuários e grupos tooany aplicativo ou a identidade do repositório que é apoiado por um serviço web com interface Olá definido na especificação do protocolo SCIM de saudação"
services: active-directory
documentationcenter: 
author: asmalser-msft
manager: femila
editor: 
ms.assetid: 4d86f3dc-e2d3-4bde-81a3-4a0e092551c0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/28/2017
ms.author: asmalser
ms.reviewer: asmalser
ms.custom: aaddev;it-pro;oldportal
ms.openlocfilehash: 43045c97e68d0d22db598dcb5ec23481c4e97718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-system-for-cross-domain-identity-management-tooautomatically-provision-users-and-groups-from-azure-active-directory-tooapplications"></a><span data-ttu-id="daf98-103">Usando o sistema de gerenciamento de identidade de domínio cruzado tooautomatically provisionar os usuários e grupos do Active Directory do Azure tooapplications</span><span class="sxs-lookup"><span data-stu-id="daf98-103">Using System for Cross-Domain Identity Management tooautomatically provision users and groups from Azure Active Directory tooapplications</span></span>

## <a name="overview"></a><span data-ttu-id="daf98-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="daf98-104">Overview</span></span>
<span data-ttu-id="daf98-105">Azure Active Directory (AD do Azure) podem provisionar automaticamente os usuários e grupos tooany aplicativo ou a identidade do repositório que é apoiado por um serviço web com interface Olá definido no hello [sistema de gerenciamento de identidade de domínio cruzado (SCIM) 2.0 especificação de protocolo](https://tools.ietf.org/html/draft-ietf-scim-api-19).</span><span class="sxs-lookup"><span data-stu-id="daf98-105">Azure Active Directory (Azure AD) can automatically provision users and groups tooany application or identity store that is fronted by a web service with hello interface defined in hello [System for Cross-Domain Identity Management (SCIM) 2.0 protocol specification](https://tools.ietf.org/html/draft-ietf-scim-api-19).</span></span> <span data-ttu-id="daf98-106">Active Directory do Azure pode enviar solicitações toocreate, modificar ou excluir o serviço de web de toohello atribuído de usuários e grupos.</span><span class="sxs-lookup"><span data-stu-id="daf98-106">Azure Active Directory can send requests toocreate, modify, or delete assigned users and groups toohello web service.</span></span> <span data-ttu-id="daf98-107">serviço web de Hello, em seguida, pode traduzir essas solicitações em operações no repositório de identidades de destino hello.</span><span class="sxs-lookup"><span data-stu-id="daf98-107">hello web service can then translate those requests into operations on hello target identity store.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="daf98-108">A Microsoft recomenda que você gerencie o AD do Azure usando Olá [Centro de administração do AD do Azure](https://aad.portal.azure.com) em Olá portal do Azure em vez de usar Olá portal clássico do Azure mencionado neste artigo.</span><span class="sxs-lookup"><span data-stu-id="daf98-108">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> 



<span data-ttu-id="daf98-109">![][0]
*Figura 1: Provisionamento do repositório de identidades do Active Directory do Azure tooan por meio de um serviço web*</span><span class="sxs-lookup"><span data-stu-id="daf98-109">![][0]
*Figure 1: Provisioning from Azure Active Directory tooan identity store via a web service*</span></span>

<span data-ttu-id="daf98-110">Esse recurso pode ser usado em conjunto com a funcionalidade de "traga seu próprio aplicativo" hello no AD do Azure tooenable-logon único e provisionamento para aplicativos que fornecem ou são apoiados por um serviço da web SCIM de usuário automático.</span><span class="sxs-lookup"><span data-stu-id="daf98-110">This capability can be used in conjunction with hello “bring your own app” capability in Azure AD tooenable single sign-on and automatic user provisioning for applications that provide or are fronted by a SCIM web service.</span></span>

<span data-ttu-id="daf98-111">Há dois casos de uso para utilizar SCIM no Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="daf98-111">There are two use cases for using SCIM in Azure Active Directory:</span></span>

* <span data-ttu-id="daf98-112">**Provisionamento de usuários e grupos tooapplications que oferecem suporte a SCIM** aplicativos que suportam SCIM 2.0 e usar os tokens de portador OAuth para autenticação funciona com o AD do Azure sem configuração.</span><span class="sxs-lookup"><span data-stu-id="daf98-112">**Provisioning users and groups tooapplications that support SCIM** Applications that support SCIM 2.0 and use OAuth bearer tokens for authentication works with Azure AD without configuration.</span></span>
* <span data-ttu-id="daf98-113">**Criar sua própria solução de provisionamento para aplicativos que oferecem suporte a outros provisionamento baseado em API** para aplicativos não-SCIM, você pode criar um tootranslate de ponto de extremidade SCIM entre o ponto de extremidade do hello SCIM do AD do Azure e oferece suporte a qualquer API Olá aplicativo para provisionamento do usuário.</span><span class="sxs-lookup"><span data-stu-id="daf98-113">**Build your own provisioning solution for applications that support other API-based provisioning** For non-SCIM applications, you can create a SCIM endpoint tootranslate between hello Azure AD SCIM endpoint and any API hello application supports for user provisioning.</span></span> <span data-ttu-id="daf98-114">toohelp desenvolver um ponto de extremidade SCIM, fornecemos bibliotecas de infraestrutura de linguagem comum (CLI) junto com exemplos de código que mostram como toodo fornecem um ponto de extremidade SCIM e traduzir mensagens SCIM.</span><span class="sxs-lookup"><span data-stu-id="daf98-114">toohelp you develop a SCIM endpoint, we provide Common Language Infrastructure (CLI) libraries along with code samples that show you how toodo provide a SCIM endpoint and translate SCIM messages.</span></span>  

## <a name="provisioning-users-and-groups-tooapplications-that-support-scim"></a><span data-ttu-id="daf98-115">Provisionamento de usuários e grupos tooapplications que oferecem suporte a SCIM</span><span class="sxs-lookup"><span data-stu-id="daf98-115">Provisioning users and groups tooapplications that support SCIM</span></span>
<span data-ttu-id="daf98-116">O AD do Azure pode ser configurado tooautomatically atribuído de provisionar usuários e grupos tooapplications que implementam um [sistema para o gerenciamento de identidade de domínio cruzado 2 (SCIM)](https://tools.ietf.org/html/draft-ietf-scim-api-19) serviço web e aceitar os tokens de portador OAuth para autenticação .</span><span class="sxs-lookup"><span data-stu-id="daf98-116">Azure AD can be configured tooautomatically provision assigned users and groups tooapplications that implement a [System for Cross-domain Identity Management 2 (SCIM)](https://tools.ietf.org/html/draft-ietf-scim-api-19) web service and accept OAuth bearer tokens for authentication.</span></span> <span data-ttu-id="daf98-117">Aplicativos dentro da especificação de saudação SCIM 2.0 devem atender a esses requisitos:</span><span class="sxs-lookup"><span data-stu-id="daf98-117">Within hello SCIM 2.0 specification, applications must meet these requirements:</span></span>

* <span data-ttu-id="daf98-118">Oferece suporte à criação de usuários e/ou grupos, de acordo com a seção 3.3 da saudação protocolo SCIM.</span><span class="sxs-lookup"><span data-stu-id="daf98-118">Supports creating users and/or groups, as per section 3.3 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="daf98-119">Dá suporte à modificação de usuários e/ou grupos com solicitações de patch de acordo com a seção 3.5.2 Olá protocolo SCIM.</span><span class="sxs-lookup"><span data-stu-id="daf98-119">Supports modifying users and/or groups with patch requests as per section 3.5.2 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="daf98-120">Dá suporte à recuperação de um recurso conhecido de acordo com a seção 3.4.1 Olá protocolo SCIM.</span><span class="sxs-lookup"><span data-stu-id="daf98-120">Supports retrieving a known resource as per section 3.4.1 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="daf98-121">Oferece suporte ao consultar os usuários e/ou grupos, de acordo com a seção 3.4.2 Olá protocolo SCIM.</span><span class="sxs-lookup"><span data-stu-id="daf98-121">Supports querying users and/or groups, as per section 3.4.2 of hello SCIM protocol.</span></span>  <span data-ttu-id="daf98-122">Por padrão, os usuários são consultados por externalId e os grupos são consultados por displayName.</span><span class="sxs-lookup"><span data-stu-id="daf98-122">By default, users are queried by externalId and groups are queried by displayName.</span></span>  
* <span data-ttu-id="daf98-123">Dá suporte à consulta de usuário por ID e pelo Gerenciador de acordo com a seção 3.4.2 Olá protocolo SCIM.</span><span class="sxs-lookup"><span data-stu-id="daf98-123">Supports querying user by ID and by manager as per section 3.4.2 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="daf98-124">Oferece suporte ao consultar grupos por ID e por membro de acordo com a seção 3.4.2 Olá protocolo SCIM.</span><span class="sxs-lookup"><span data-stu-id="daf98-124">Supports querying groups by ID and by member as per section 3.4.2 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="daf98-125">Aceita tokens de portador OAuth para autorização de acordo com a seção 2.1 de saudação protocolo SCIM.</span><span class="sxs-lookup"><span data-stu-id="daf98-125">Accepts OAuth bearer tokens for authorization as per section 2.1 of hello SCIM protocol.</span></span>

<span data-ttu-id="daf98-126">Verifique com o seu provedor de aplicativo ou na documentação do seu provedor de aplicativo as declarações de compatibilidade com esses requisitos.</span><span class="sxs-lookup"><span data-stu-id="daf98-126">Check with your application provider, or your application provider's documentation for statements of compatibility with these requirements.</span></span>

### <a name="getting-started"></a><span data-ttu-id="daf98-127">Introdução</span><span class="sxs-lookup"><span data-stu-id="daf98-127">Getting started</span></span>
<span data-ttu-id="daf98-128">Aplicativos que dão suporte ao perfil SCIM Olá descrito neste artigo podem ser conectado tooAzure do Active Directory usando o recurso de "não Galeria aplicativo hello" na Galeria de aplicativos de saudação do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="daf98-128">Applications that support hello SCIM profile described in this article can be connected tooAzure Active Directory using hello "non-gallery application" feature in hello Azure AD application gallery.</span></span> <span data-ttu-id="daf98-129">Depois de conectado, o Azure AD executa um processo de sincronização a cada 20 minutos em que ele consulta o ponto de extremidade do aplicativo hello SCIM para atribuídas a usuários e grupos e cria ou modifica-los de acordo com toohello detalhes da atribuição.</span><span class="sxs-lookup"><span data-stu-id="daf98-129">Once connected, Azure AD runs a synchronization process every 20 minutes where it queries hello application's SCIM endpoint for assigned users and groups, and creates or modifies them according toohello assignment details.</span></span>

<span data-ttu-id="daf98-130">**tooconnect um aplicativo que oferece suporte a SCIM:**</span><span class="sxs-lookup"><span data-stu-id="daf98-130">**tooconnect an application that supports SCIM:**</span></span>

1. <span data-ttu-id="daf98-131">Entrar muito[Olá portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="daf98-131">Sign in too[hello Azure portal](https://portal.azure.com).</span></span> 
2. <span data-ttu-id="daf98-132">Procurar muito * * Active Directory do Azure > aplicativos da empresa e selecione **novo aplicativo > todos os > aplicativo Galeria não**.</span><span class="sxs-lookup"><span data-stu-id="daf98-132">Browse too**Azure Active Directory > Enterprise Applications, and select **New application > All > Non-gallery application**.</span></span>
3. <span data-ttu-id="daf98-133">Insira um nome para seu aplicativo e clique em **adicionar** ícone toocreate um objeto de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="daf98-133">Enter a name for your application, and click **Add** icon toocreate an app object.</span></span>
    
  <span data-ttu-id="daf98-134">![][1]
  *Figura 2: Galeria de aplicativos do Azure AD*</span><span class="sxs-lookup"><span data-stu-id="daf98-134">![][1]
*Figure 2: Azure AD application gallery*</span></span>
    
4. <span data-ttu-id="daf98-135">Na tela de resultante hello, selecione Olá **provisionamento** guia na coluna esquerda hello.</span><span class="sxs-lookup"><span data-stu-id="daf98-135">In hello resulting screen, select hello **Provisioning** tab in hello left column.</span></span>
5. <span data-ttu-id="daf98-136">Em Olá **modo de provisionamento** menu, selecione **automática**.</span><span class="sxs-lookup"><span data-stu-id="daf98-136">In hello **Provisioning Mode** menu, select **Automatic**.</span></span>
    
  <span data-ttu-id="daf98-137">![][2]
  *Figura 3: Configurar o provisionamento em Olá portal do Azure*</span><span class="sxs-lookup"><span data-stu-id="daf98-137">![][2]
*Figure 3: Configuring provisioning in hello Azure portal*</span></span>
    
6. <span data-ttu-id="daf98-138">Em Olá **URL do locatário** , digite a URL de saudação do ponto de extremidade do aplicativo hello SCIM.</span><span class="sxs-lookup"><span data-stu-id="daf98-138">In hello **Tenant URL** field, enter hello URL of hello application's SCIM endpoint.</span></span> <span data-ttu-id="daf98-139">Exemplo: https://api.contoso.com/scim/v2/</span><span class="sxs-lookup"><span data-stu-id="daf98-139">Example: https://api.contoso.com/scim/v2/</span></span>
7. <span data-ttu-id="daf98-140">Se o ponto de extremidade do hello SCIM requer um token de portador OAuth de um emissor que não sejam do AD do Azure, Olá cópia necessário token de portador OAuth em Olá opcional **segredo do Token** campo.</span><span class="sxs-lookup"><span data-stu-id="daf98-140">If hello SCIM endpoint requires an OAuth bearer token from an issuer other than Azure AD, then copy hello required OAuth bearer token into hello optional **Secret Token** field.</span></span> <span data-ttu-id="daf98-141">Se esse campo estiver em branco, o Azure AD incluiu um token de portador OAuth emitido do Azure AD com cada solicitação.</span><span class="sxs-lookup"><span data-stu-id="daf98-141">If this field is left blank, then Azure AD included an OAuth bearer token issued from Azure AD with each request.</span></span> <span data-ttu-id="daf98-142">Aplicativos que usam o Azure AD como provedor de identidade podem validar esse token emitido pelo Azure AD.</span><span class="sxs-lookup"><span data-stu-id="daf98-142">Apps that use Azure AD as an identity provider can validate this Azure AD -issued token.</span></span>
8. <span data-ttu-id="daf98-143">Clique em Olá **Conexão de teste** botão toohave Active Directory do Azure tentativa tooconnect toohello SCIM ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="daf98-143">Click hello **Test Connection** button toohave Azure Active Directory attempt tooconnect toohello SCIM endpoint.</span></span> <span data-ttu-id="daf98-144">Se Olá tentativas falharem, informações de erro são exibidas.</span><span class="sxs-lookup"><span data-stu-id="daf98-144">If hello attempts fail, error information is displayed.</span></span>  
9. <span data-ttu-id="daf98-145">Se tiver êxito Olá tentativas tooconnect toohello aplicativo, clique em **salvar** toosave credenciais de administrador de saudação.</span><span class="sxs-lookup"><span data-stu-id="daf98-145">If hello attempts tooconnect toohello application succeed, then click **Save** toosave hello admin credentials.</span></span>
10. <span data-ttu-id="daf98-146">Em Olá **mapeamentos** seção, há dois conjuntos selecionáveis de mapeamentos de atributos: um para objetos de usuário e outro para objetos de grupo.</span><span class="sxs-lookup"><span data-stu-id="daf98-146">In hello **Mappings** section, there are two selectable sets of attribute mappings: one for user objects and one for group objects.</span></span> <span data-ttu-id="daf98-147">Selecione cada um atributos de saudação de tooreview que são sincronizados do Active Directory do Azure tooyour aplicativo.</span><span class="sxs-lookup"><span data-stu-id="daf98-147">Select each one tooreview hello attributes that are synchronized from Azure Active Directory tooyour app.</span></span> <span data-ttu-id="daf98-148">Olá atributos selecionados como **correspondência** propriedades são usadas toomatch Olá usuários e grupos em seu aplicativo para operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="daf98-148">hello attributes selected as **Matching** properties are used toomatch hello users and groups in your app for update operations.</span></span> <span data-ttu-id="daf98-149">Selecione Olá toocommit de botão de salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="daf98-149">Select hello Save button toocommit any changes.</span></span>

    >[!NOTE]
    ><span data-ttu-id="daf98-150">Opcionalmente, você pode desabilitar a sincronização de objetos de grupo desabilitando hello "grupos" mapeamento.</span><span class="sxs-lookup"><span data-stu-id="daf98-150">You can optionally disable syncing of group objects by disabling hello "groups" mapping.</span></span> 

11. <span data-ttu-id="daf98-151">Em **configurações**, Olá **escopo** campo define quais usuários e/ou grupos são sincronizados.</span><span class="sxs-lookup"><span data-stu-id="daf98-151">Under **Settings**, hello **Scope** field defines which users and or groups are synchronized.</span></span> <span data-ttu-id="daf98-152">Selecionar "Sincronização atribuído apenas usuários e grupos" (recomendado) sincronizará apenas os usuários e grupos atribuídos no hello **usuários e grupos** guia.</span><span class="sxs-lookup"><span data-stu-id="daf98-152">Selecting "Sync only assigned users and groups" (recommended) will only sync users and groups assigned in hello **Users and groups** tab.</span></span>
12. <span data-ttu-id="daf98-153">Depois que a configuração estiver concluída, alterar Olá **Status de provisionamento** muito**em**.</span><span class="sxs-lookup"><span data-stu-id="daf98-153">Once your configuration is complete, change hello **Provisioning Status** too**On**.</span></span>
13. <span data-ttu-id="daf98-154">Clique em **salvar** toostart Olá serviço de provisionamento do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="daf98-154">Click **Save** toostart hello Azure AD provisioning service.</span></span> 
14. <span data-ttu-id="daf98-155">Se sincronizar apenas atribuídas a usuários e grupos (recomendados), ser se Olá de tooselect **usuários e grupos** guia e atribua usuários hello e/ou grupos que você deseja toosync.</span><span class="sxs-lookup"><span data-stu-id="daf98-155">If syncing only assigned users and groups (recommended), be sure tooselect hello **Users and groups** tab and assign hello users and/or groups you wish toosync.</span></span>

<span data-ttu-id="daf98-156">Depois que a sincronização inicial Olá foi iniciado, você pode usar o hello **logs de auditoria** guia toomonitor progresso, que mostra todas as ações executadas pelo Olá provisionar um serviço em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="daf98-156">Once hello initial synchronization has started, you can use hello **Audit logs** tab toomonitor progress, which shows all actions performed by hello provisioning service on your app.</span></span> <span data-ttu-id="daf98-157">Para obter mais informações sobre como o provisionamento de saudação do AD do Azure tooread registra, consulte [relatórios sobre o provisionamento de conta de usuário automático](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="daf98-157">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

>[!NOTE]
><span data-ttu-id="daf98-158">a sincronização inicial Olá leva tooperform mais que as sincronizações subsequentes, que ocorrem aproximadamente a cada 20 minutos desde que o serviço hello está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="daf98-158">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> 


## <a name="building-your-own-provisioning-solution-for-any-application"></a><span data-ttu-id="daf98-159">Criando sua própria solução de provisionamento para qualquer aplicativo</span><span class="sxs-lookup"><span data-stu-id="daf98-159">Building your own provisioning solution for any application</span></span>
<span data-ttu-id="daf98-160">Ao criar um serviço Web SCIM que interaja com o Active Directory do Azure, você poderá habilitar o logon único e o provisionamento de usuário automático para praticamente qualquer aplicativo que forneça uma API de provisionamento de usuário SOAP ou REST.</span><span class="sxs-lookup"><span data-stu-id="daf98-160">By creating a SCIM web service that interfaces with Azure Active Directory, you can enable single sign-on and automatic user provisioning for virtually any application that provides a REST or SOAP user provisioning API.</span></span>

<span data-ttu-id="daf98-161">Veja como ele funciona:</span><span class="sxs-lookup"><span data-stu-id="daf98-161">Here’s how it works:</span></span>

1. <span data-ttu-id="daf98-162">O AD do Azure fornece uma biblioteca CLI denominada [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/).</span><span class="sxs-lookup"><span data-stu-id="daf98-162">Azure AD provides a common language infrastructure library named [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/).</span></span> <span data-ttu-id="daf98-163">Os desenvolvedores e integradores de sistema podem usar essa toocreate de biblioteca e implantar uma empresa de serviço web baseado em SCIM capaz de se conectar o armazenamento de identidade do aplicativo do AD do Azure tooany.</span><span class="sxs-lookup"><span data-stu-id="daf98-163">System integrators and developers can use this library toocreate and deploy a SCIM-based web service endpoint capable of connecting Azure AD tooany application’s identity store.</span></span>
2. <span data-ttu-id="daf98-164">Mapeamentos de são implementados no Olá web serviço toomap Olá usuário padronizado toohello usuário esquema e o protocolo exigido pelo aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="daf98-164">Mappings are implemented in hello web service toomap hello standardized user schema toohello user schema and protocol required by hello application.</span></span>
3. <span data-ttu-id="daf98-165">URL de ponto de extremidade Hello está registrado no AD do Azure como parte de um aplicativo personalizado na Galeria de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="daf98-165">hello endpoint URL is registered in Azure AD as part of a custom application in hello application gallery.</span></span>
4. <span data-ttu-id="daf98-166">Usuários e grupos são atribuídos toothis aplicativo no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="daf98-166">Users and groups are assigned toothis application in Azure AD.</span></span> <span data-ttu-id="daf98-167">Após a atribuição, eles são colocados em um aplicativo de destino toohello fila toobe sincronizado.</span><span class="sxs-lookup"><span data-stu-id="daf98-167">Upon assignment, they are put into a queue toobe synchronized toohello target application.</span></span> <span data-ttu-id="daf98-168">processo de sincronização de Olá tratamento fila Olá é executado a cada 20 minutos.</span><span class="sxs-lookup"><span data-stu-id="daf98-168">hello synchronization process handling hello queue runs every 20 minutes.</span></span>

### <a name="code-samples"></a><span data-ttu-id="daf98-169">Exemplos de código</span><span class="sxs-lookup"><span data-stu-id="daf98-169">Code Samples</span></span>
<span data-ttu-id="daf98-170">toomake esse processo, um conjunto de [exemplos de código](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) são fornecidas que criar um ponto de extremidade de serviço do SCIM web e demonstre o provisionamento automático.</span><span class="sxs-lookup"><span data-stu-id="daf98-170">toomake this process easier, a set of [code samples](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) are provided that create a SCIM web service endpoint and demonstrate automatic provisioning.</span></span> <span data-ttu-id="daf98-171">Um dos exemplos é de um provedor que mantém um arquivo com linhas de valores separados por vírgula representando usuários e grupos.</span><span class="sxs-lookup"><span data-stu-id="daf98-171">One sample is of a provider that maintains a file with rows of comma-separated values representing users and groups.</span></span>  <span data-ttu-id="daf98-172">Olá outros é de um provedor que opera no serviço de gerenciamento de acesso e identidade do Amazon Web Services hello.</span><span class="sxs-lookup"><span data-stu-id="daf98-172">hello other is of a provider that operates on hello Amazon Web Services Identity and Access Management service.</span></span>  

<span data-ttu-id="daf98-173">**Pré-requisitos**</span><span class="sxs-lookup"><span data-stu-id="daf98-173">**Prerequisites**</span></span>

* <span data-ttu-id="daf98-174">Visual Studio 2013 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="daf98-174">Visual Studio 2013 or later</span></span>
* [<span data-ttu-id="daf98-175">SDK do Azure para .NET</span><span class="sxs-lookup"><span data-stu-id="daf98-175">Azure SDK for .NET</span></span>](https://azure.microsoft.com/downloads/)
* <span data-ttu-id="daf98-176">Computador Windows que dá suporte a saudação ASP.NET framework 4.5 toobe usado como Olá ponto de extremidade SCIM.</span><span class="sxs-lookup"><span data-stu-id="daf98-176">Windows machine that supports hello ASP.NET framework 4.5 toobe used as hello SCIM endpoint.</span></span> <span data-ttu-id="daf98-177">Esta máquina deve ser acessível da nuvem de saudação</span><span class="sxs-lookup"><span data-stu-id="daf98-177">This machine must be accessible from hello cloud</span></span>
* [<span data-ttu-id="daf98-178">Uma assinatura do Azure com uma versão de avaliação ou licenciada do Azure AD Premium</span><span class="sxs-lookup"><span data-stu-id="daf98-178">An Azure subscription with a trial or licensed version of Azure AD Premium</span></span>](https://azure.microsoft.com/services/active-directory/)
* <span data-ttu-id="daf98-179">exemplo de AWS Amazon Hello requer bibliotecas do hello [AWS Kit de ferramentas do Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html).</span><span class="sxs-lookup"><span data-stu-id="daf98-179">hello Amazon AWS sample requires libraries from hello [AWS Toolkit for Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html).</span></span> <span data-ttu-id="daf98-180">Para obter mais informações, consulte Olá Leiame arquivo incluído com o exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="daf98-180">For more information, see hello README file included with hello sample.</span></span>

### <a name="getting-started"></a><span data-ttu-id="daf98-181">Introdução</span><span class="sxs-lookup"><span data-stu-id="daf98-181">Getting Started</span></span>
<span data-ttu-id="daf98-182">Olá tooimplement de maneira mais fácil solicitações de um ponto de extremidade SCIM pode aceitar a configuração do AD do Azure é toobuild e implantar o exemplo de código de saudação que gera o arquivo de valores separados por vírgulas (CSV) de tooa Olá usuários provisionados.</span><span class="sxs-lookup"><span data-stu-id="daf98-182">hello easiest way tooimplement a SCIM endpoint that can accept provisioning requests from Azure AD is toobuild and deploy hello code sample that outputs hello provisioned users tooa comma-separated value (CSV) file.</span></span>

<span data-ttu-id="daf98-183">**toocreate um ponto de extremidade SCIM de exemplo:**</span><span class="sxs-lookup"><span data-stu-id="daf98-183">**toocreate a sample SCIM endpoint:**</span></span>

1. <span data-ttu-id="daf98-184">Baixar pacote de exemplo de código Olá em [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)</span><span class="sxs-lookup"><span data-stu-id="daf98-184">Download hello code sample package at [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)</span></span>
2. <span data-ttu-id="daf98-185">Descompacte o pacote hello e colocá-lo em seu computador Windows em um local como C:\AzureAD-BYOA-Provisioning-Samples\.</span><span class="sxs-lookup"><span data-stu-id="daf98-185">Unzip hello package and place it on your Windows machine at a location such as C:\AzureAD-BYOA-Provisioning-Samples\.</span></span>
3. <span data-ttu-id="daf98-186">Nessa pasta, inicie a solução de FileProvisioningAgent Olá no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="daf98-186">In this folder, launch hello FileProvisioningAgent solution in Visual Studio.</span></span>
4. <span data-ttu-id="daf98-187">Selecione **Ferramentas > Gerenciador de biblioteca de pacote > Package Manager Console**e executar Olá comandos Olá FileProvisioningAgent projeto tooresolve Olá solução referências a seguir:</span><span class="sxs-lookup"><span data-stu-id="daf98-187">Select **Tools > Library Package Manager > Package Manager Console**, and execute hello following commands for hello FileProvisioningAgent project tooresolve hello solution references:</span></span>
  ```` 
   Install-Package Microsoft.SystemForCrossDomainIdentityManagement
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   Install-Package Microsoft.Owin.Diagnostics
   Install-Package Microsoft.Owin.Host.SystemWeb
  ````
5. <span data-ttu-id="daf98-188">Compile o projeto de FileProvisioningAgent de saudação.</span><span class="sxs-lookup"><span data-stu-id="daf98-188">Build hello FileProvisioningAgent project.</span></span>
6. <span data-ttu-id="daf98-189">Iniciar o aplicativo do Prompt de comando Olá no Windows (como administrador) e usar Olá **cd** comando toochange Olá diretório tooyour **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug** pasta.</span><span class="sxs-lookup"><span data-stu-id="daf98-189">Launch hello Command Prompt application in Windows (as an Administrator), and use hello **cd** command toochange hello directory tooyour **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug** folder.</span></span>
7. <span data-ttu-id="daf98-190">Execute Olá comando a seguir, substituindo < endereço ip > pelo nome de domínio ou endereço IP de saudação do computador do Windows hello:</span><span class="sxs-lookup"><span data-stu-id="daf98-190">Run hello following command, replacing <ip-address> with hello IP address or domain name of hello Windows machine:</span></span>
  ````   
   FileAgnt.exe http://<ip-address>:9000 TargetFile.csv
  ````
8. <span data-ttu-id="daf98-191">No Windows em **configurações do Windows > configurações de Internet e rede**, selecione Olá **Firewall do Windows > Configurações avançadas**e criar um **regra de entrada** que permite acesso de entrada tooport 9000.</span><span class="sxs-lookup"><span data-stu-id="daf98-191">In Windows under **Windows Settings > Network & Internet Settings**, select hello **Windows Firewall > Advanced Settings**, and create an **Inbound Rule** that allows inbound access tooport 9000.</span></span>
9. <span data-ttu-id="daf98-192">Se o computador do Windows hello estiver atrás de um roteador, Olá roteador necessidades toobe configurado tooperform conversão de acesso de rede entre sua porta 9000 que é toohello exposto à internet e porta 9000 no computador do Windows hello.</span><span class="sxs-lookup"><span data-stu-id="daf98-192">If hello Windows machine is behind a router, hello router needs toobe configured tooperform Network Access Translation between its port 9000 that is exposed toohello internet, and port 9000 on hello Windows machine.</span></span> <span data-ttu-id="daf98-193">Isso é necessário para o AD do Azure toobe capaz de tooaccess esse ponto de extremidade na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="daf98-193">This is required for Azure AD toobe able tooaccess this endpoint in hello cloud.</span></span>

<span data-ttu-id="daf98-194">**tooregister Olá exemplo SCIM ponto de extremidade no AD do Azure:**</span><span class="sxs-lookup"><span data-stu-id="daf98-194">**tooregister hello sample SCIM endpoint in Azure AD:**</span></span>

1. <span data-ttu-id="daf98-195">Entrar muito[Olá portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="daf98-195">Sign in too[hello Azure portal](https://portal.azure.com).</span></span> 
2. <span data-ttu-id="daf98-196">Procurar muito * * Active Directory do Azure > aplicativos da empresa e selecione **novo aplicativo > todos os > aplicativo Galeria não**.</span><span class="sxs-lookup"><span data-stu-id="daf98-196">Browse too**Azure Active Directory > Enterprise Applications, and select **New application > All > Non-gallery application**.</span></span>
3. <span data-ttu-id="daf98-197">Insira um nome para seu aplicativo e clique em **adicionar** ícone toocreate um objeto de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="daf98-197">Enter a name for your application, and click **Add** icon toocreate an app object.</span></span> <span data-ttu-id="daf98-198">objeto de aplicativo Hello criado é aplicativo de destino de saudação toorepresent pretendido você seria provisionamento tooand implementação de ponto de extremidade SCIM Olá único de logon para o e não apenas.</span><span class="sxs-lookup"><span data-stu-id="daf98-198">hello application object created is intended toorepresent hello target app you would be provisioning tooand implementing single sign-on for, and not just hello SCIM endpoint.</span></span>
4. <span data-ttu-id="daf98-199">Na tela de resultante hello, selecione Olá **provisionamento** guia na coluna esquerda hello.</span><span class="sxs-lookup"><span data-stu-id="daf98-199">In hello resulting screen, select hello **Provisioning** tab in hello left column.</span></span>
5. <span data-ttu-id="daf98-200">Em Olá **modo de provisionamento** menu, selecione **automática**.</span><span class="sxs-lookup"><span data-stu-id="daf98-200">In hello **Provisioning Mode** menu, select **Automatic**.</span></span>
    
  <span data-ttu-id="daf98-201">![][2]
  *Figura 4: Configurar o provisionamento em Olá portal do Azure*</span><span class="sxs-lookup"><span data-stu-id="daf98-201">![][2]
*Figure 4: Configuring provisioning in hello Azure portal*</span></span>
    
6. <span data-ttu-id="daf98-202">Em Olá **URL do locatário** digite Olá expostos à internet URL e a porta de seu ponto de extremidade SCIM.</span><span class="sxs-lookup"><span data-stu-id="daf98-202">In hello **Tenant URL** field, enter hello internet-exposed URL and port of your SCIM endpoint.</span></span> <span data-ttu-id="daf98-203">Isso seria algo como http://testmachine.contoso.com:9000 ou http://<ip-address>:9000/, onde < endereço ip > é Olá internet expostos IP endereço.</span><span class="sxs-lookup"><span data-stu-id="daf98-203">This would be something like http://testmachine.contoso.com:9000 or http://<ip-address>:9000/, where <ip-address> is hello internet exposed IP address.</span></span>  
7. <span data-ttu-id="daf98-204">Se o ponto de extremidade do hello SCIM requer um token de portador OAuth de um emissor que não sejam do AD do Azure, Olá cópia necessário token de portador OAuth em Olá opcional **segredo do Token** campo.</span><span class="sxs-lookup"><span data-stu-id="daf98-204">If hello SCIM endpoint requires an OAuth bearer token from an issuer other than Azure AD, then copy hello required OAuth bearer token into hello optional **Secret Token** field.</span></span> <span data-ttu-id="daf98-205">Se esse campo for deixado em branco, o Azure AD incluirá um token de portador OAuth emitido do Azure AD com cada solicitação.</span><span class="sxs-lookup"><span data-stu-id="daf98-205">If this field is left blank, then Azure AD will include an OAuth bearer token issued from Azure AD with each request.</span></span> <span data-ttu-id="daf98-206">Aplicativos que usam o Azure AD como provedor de identidade podem validar esse token emitido pelo Azure AD.</span><span class="sxs-lookup"><span data-stu-id="daf98-206">Apps that use Azure AD as an identity provider can validate this Azure AD -issued token.</span></span>
8. <span data-ttu-id="daf98-207">Clique em Olá **Conexão de teste** botão toohave Active Directory do Azure tentativa tooconnect toohello SCIM ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="daf98-207">Click hello **Test Connection** button toohave Azure Active Directory attempt tooconnect toohello SCIM endpoint.</span></span> <span data-ttu-id="daf98-208">Se Olá tentativas falharem, informações de erro são exibidas.</span><span class="sxs-lookup"><span data-stu-id="daf98-208">If hello attempts fail, error information is displayed.</span></span>  
9. <span data-ttu-id="daf98-209">Se tiver êxito Olá tentativas tooconnect toohello aplicativo, clique em **salvar** toosave credenciais de administrador de saudação.</span><span class="sxs-lookup"><span data-stu-id="daf98-209">If hello attempts tooconnect toohello application succeed, then click **Save** toosave hello admin credentials.</span></span>
10. <span data-ttu-id="daf98-210">Em Olá **mapeamentos** seção, há dois conjuntos selecionáveis de mapeamentos de atributos: um para objetos de usuário e outro para objetos de grupo.</span><span class="sxs-lookup"><span data-stu-id="daf98-210">In hello **Mappings** section, there are two selectable sets of attribute mappings: one for user objects and one for group objects.</span></span> <span data-ttu-id="daf98-211">Selecione cada um atributos de saudação de tooreview que são sincronizados do Active Directory do Azure tooyour aplicativo.</span><span class="sxs-lookup"><span data-stu-id="daf98-211">Select each one tooreview hello attributes that are synchronized from Azure Active Directory tooyour app.</span></span> <span data-ttu-id="daf98-212">Olá atributos selecionados como **correspondência** propriedades são usadas toomatch Olá usuários e grupos em seu aplicativo para operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="daf98-212">hello attributes selected as **Matching** properties are used toomatch hello users and groups in your app for update operations.</span></span> <span data-ttu-id="daf98-213">Selecione Olá toocommit de botão de salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="daf98-213">Select hello Save button toocommit any changes.</span></span>
11. <span data-ttu-id="daf98-214">Em **configurações**, Olá **escopo** campo define quais usuários e/ou grupos são sincronizados.</span><span class="sxs-lookup"><span data-stu-id="daf98-214">Under **Settings**, hello **Scope** field defines which users and or groups are synchronized.</span></span> <span data-ttu-id="daf98-215">Selecionar "Sincronização atribuído apenas usuários e grupos" (recomendado) sincronizará apenas os usuários e grupos atribuídos no hello **usuários e grupos** guia.</span><span class="sxs-lookup"><span data-stu-id="daf98-215">Selecting "Sync only assigned users and groups" (recommended) will only sync users and groups assigned in hello **Users and groups** tab.</span></span>
12. <span data-ttu-id="daf98-216">Depois que a configuração estiver concluída, alterar Olá **Status de provisionamento** muito**em**.</span><span class="sxs-lookup"><span data-stu-id="daf98-216">Once your configuration is complete, change hello **Provisioning Status** too**On**.</span></span>
13. <span data-ttu-id="daf98-217">Clique em **salvar** toostart Olá serviço de provisionamento do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="daf98-217">Click **Save** toostart hello Azure AD provisioning service.</span></span> 
14. <span data-ttu-id="daf98-218">Se sincronizar apenas atribuídas a usuários e grupos (recomendados), ser se Olá de tooselect **usuários e grupos** guia e atribua usuários hello e/ou grupos que você deseja toosync.</span><span class="sxs-lookup"><span data-stu-id="daf98-218">If syncing only assigned users and groups (recommended), be sure tooselect hello **Users and groups** tab and assign hello users and/or groups you wish toosync.</span></span>

<span data-ttu-id="daf98-219">Depois que a sincronização inicial Olá foi iniciado, você pode usar o hello **logs de auditoria** guia toomonitor progresso, que mostra todas as ações executadas pelo Olá provisionar um serviço em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="daf98-219">Once hello initial synchronization has started, you can use hello **Audit logs** tab toomonitor progress, which shows all actions performed by hello provisioning service on your app.</span></span> <span data-ttu-id="daf98-220">Para obter mais informações sobre como o provisionamento de saudação do AD do Azure tooread registra, consulte [relatórios sobre o provisionamento de conta de usuário automático](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="daf98-220">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

<span data-ttu-id="daf98-221">a etapa final Olá verificar exemplo hello é tooopen Olá arquivo TargetFile.csv na pasta de \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug Olá no seu computador Windows.</span><span class="sxs-lookup"><span data-stu-id="daf98-221">hello final step in verifying hello sample is tooopen hello TargetFile.csv file in hello \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug folder on your Windows machine.</span></span> <span data-ttu-id="daf98-222">Após a saudação processo de provisionamento é executada, esse arquivo mostra detalhes de saudação de todos os atribuídos e provisionado usuários e grupos.</span><span class="sxs-lookup"><span data-stu-id="daf98-222">Once hello provisioning process is run, this file shows hello details of all assigned and provisioned users and groups.</span></span>

### <a name="development-libraries"></a><span data-ttu-id="daf98-223">Bibliotecas de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="daf98-223">Development libraries</span></span>
<span data-ttu-id="daf98-224">toodevelop seu próprio serviço da web que está em conformidade com a especificação de SCIM toohello, primeiro você se familiarizar com hello bibliotecas a seguir fornecido pela Microsoft toohelp acelerar o processo de desenvolvimento de saudação:</span><span class="sxs-lookup"><span data-stu-id="daf98-224">toodevelop your own web service that conforms toohello SCIM specification, first familiarize yourself with hello following libraries provided by Microsoft toohelp accelerate hello development process:</span></span> 

1. <span data-ttu-id="daf98-225">As bibliotecas Common Language Infrastructure (CLI) são oferecidas para uso com linguagens que se baseiam na infraestrutura em questão, como C#.</span><span class="sxs-lookup"><span data-stu-id="daf98-225">Common Language Infrastructure (CLI) libraries are offered for use with languages based on that infrastructure, such as C#.</span></span> <span data-ttu-id="daf98-226">Uma dessas bibliotecas, [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), declara uma interface, Microsoft.SystemForCrossDomainIdentityManagement.IProvider, mostrada na ilustração a seguir de saudação: um usando bibliotecas de saudação do desenvolvedor deve implementar essa interface com uma classe que pode ser chamada, genericamente, como um provedor.</span><span class="sxs-lookup"><span data-stu-id="daf98-226">One of those libraries, [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), declares an interface, Microsoft.SystemForCrossDomainIdentityManagement.IProvider, shown in hello following illustration:  A developer using hello libraries would implement that interface with a class that may be referred to, generically, as a provider.</span></span> <span data-ttu-id="daf98-227">bibliotecas de saudação habilitar Olá desenvolvedor toodeploy um serviço web que está em conformidade com a especificação de SCIM toohello.</span><span class="sxs-lookup"><span data-stu-id="daf98-227">hello libraries enable hello developer toodeploy a web service that conforms toohello SCIM specification.</span></span> <span data-ttu-id="daf98-228">serviço web de saudação ou pode ser hospedado em serviços de informações da Internet ou de qualquer assembly executável do Common Language Infrastructure.</span><span class="sxs-lookup"><span data-stu-id="daf98-228">hello web service can be either hosted within Internet Information Services, or any executable Common Language Infrastructure assembly.</span></span> <span data-ttu-id="daf98-229">Solicitação é convertida em métodos do provedor de toohello chamadas, que poderiam ser programados Olá toooperate de desenvolvedor em algum armazenamento de identidade.</span><span class="sxs-lookup"><span data-stu-id="daf98-229">Request is translated into calls toohello provider’s methods, which would be programmed by hello developer toooperate on some identity store.</span></span>
  
  ![][3]
  
2. <span data-ttu-id="daf98-230">[Express manipuladores de rotas](http://expressjs.com/guide/routing.html) estão disponíveis para analisar objetos de solicitação de Node. js que representam chamadas (conforme definido pela especificação de SCIM de saudação), feitas serviço de web tooa Node. js.</span><span class="sxs-lookup"><span data-stu-id="daf98-230">[Express route handlers](http://expressjs.com/guide/routing.html) are available for parsing node.js request objects representing calls (as defined by hello SCIM specification), made tooa node.js web service.</span></span>   

### <a name="building-a-custom-scim-endpoint"></a><span data-ttu-id="daf98-231">Criando um ponto de extremidade SCIM personalizado</span><span class="sxs-lookup"><span data-stu-id="daf98-231">Building a Custom SCIM Endpoint</span></span>
<span data-ttu-id="daf98-232">Usando bibliotecas de CLI hello, os desenvolvedores que usam essas bibliotecas podem hospedar seus serviços de qualquer assembly do Common Language Infrastructure executável, ou em serviços de informações da Internet.</span><span class="sxs-lookup"><span data-stu-id="daf98-232">Using hello CLI libraries, developers using those libraries can host their services within any executable Common Language Infrastructure assembly, or within Internet Information Services.</span></span> <span data-ttu-id="daf98-233">Aqui está o código de exemplo para hospedar um serviço em um assembly executável, no endereço Olá http://localhost:9000:</span><span class="sxs-lookup"><span data-stu-id="daf98-233">Here is sample code for hosting a service within an executable assembly, at hello address http://localhost:9000:</span></span> 

    private static void Main(string[] arguments)
    {
    // Microsoft.SystemForCrossDomainIdentityManagement.IMonitor, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IProvider and 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service are all defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service.dll.  

    Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor = 
      new DevelopersMonitor();
    Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider = 
      new DevelopersProvider(arguments[1]);
    Microsoft.SystemForCrossDomainIdentityManagement.Service webService = null;
    try
    {
        webService = new WebService(monitor, provider);
        webService.Start("http://localhost:9000");

        Console.ReadKey(true);
    }
    finally
    {
        if (webService != null)
        {
            webService.Dispose();
            webService = null;
        }
    }
    }

    public class WebService : Microsoft.SystemForCrossDomainIdentityManagement.Service
    {
    private Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor;
    private Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider;

    public WebService(
      Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitoringBehavior, 
      Microsoft.SystemForCrossDomainIdentityManagement.IProvider providerBehavior)
    {
        this.monitor = monitoringBehavior;
        this.provider = providerBehavior;
    }

    public override IMonitor MonitoringBehavior
    {
        get
        {
            return this.monitor;
        }

        set
        {
            this.monitor = value;
        }
    }

    public override IProvider ProviderBehavior
    {
        get
        {
            return this.provider;
        }

        set
        {
            this.provider = value;
        }
    }
    }

<span data-ttu-id="daf98-234">Esse serviço deve ter um HTTP endereço e servidor de certificado de autenticação de quais hello autoridade de certificação raiz é um dos seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="daf98-234">This service must have an HTTP address and server authentication certificate of which hello root certification authority is one of hello following:</span></span> 

* <span data-ttu-id="daf98-235">CNNIC</span><span class="sxs-lookup"><span data-stu-id="daf98-235">CNNIC</span></span>
* <span data-ttu-id="daf98-236">Comodo</span><span class="sxs-lookup"><span data-stu-id="daf98-236">Comodo</span></span>
* <span data-ttu-id="daf98-237">CyberTrust</span><span class="sxs-lookup"><span data-stu-id="daf98-237">CyberTrust</span></span>
* <span data-ttu-id="daf98-238">DigiCert</span><span class="sxs-lookup"><span data-stu-id="daf98-238">DigiCert</span></span>
* <span data-ttu-id="daf98-239">GeoTrust</span><span class="sxs-lookup"><span data-stu-id="daf98-239">GeoTrust</span></span>
* <span data-ttu-id="daf98-240">GlobalSign</span><span class="sxs-lookup"><span data-stu-id="daf98-240">GlobalSign</span></span>
* <span data-ttu-id="daf98-241">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="daf98-241">Go Daddy</span></span>
* <span data-ttu-id="daf98-242">Verisign</span><span class="sxs-lookup"><span data-stu-id="daf98-242">Verisign</span></span>
* <span data-ttu-id="daf98-243">WoSign</span><span class="sxs-lookup"><span data-stu-id="daf98-243">WoSign</span></span>

<span data-ttu-id="daf98-244">Um certificado de autenticação de servidor pode ser associado tooa porta em um host do Windows usando o utilitário de shell de rede Olá:</span><span class="sxs-lookup"><span data-stu-id="daf98-244">A server authentication certificate can be bound tooa port on a Windows host using hello network shell utility:</span></span> 

    netsh http add sslcert ipport=0.0.0.0:443 certhash=0000000000003ed9cd0c315bbb6dc1c08da5e6 appid={00112233-4455-6677-8899-AABBCCDDEEFF}  

<span data-ttu-id="daf98-245">Aqui, o valor de Olá fornecido para o argumento de certhash Olá é impressão digital de saudação do certificado Olá, enquanto o valor de Olá fornecido para o argumento de appid Olá é um identificador global exclusivo arbitrário.</span><span class="sxs-lookup"><span data-stu-id="daf98-245">Here, hello value provided for hello certhash argument is hello thumbprint of hello certificate, while hello value provided for hello appid argument is an arbitrary globally unique identifier.</span></span>  

<span data-ttu-id="daf98-246">serviço de saudação toohost em serviços de informações da Internet, um desenvolvedor criaria um assembly de biblioteca de código CLA com uma classe chamada inicialização no espaço para nome padrão de saudação do assembly hello.</span><span class="sxs-lookup"><span data-stu-id="daf98-246">toohost hello service within Internet Information Services, a developer would build a CLA code library assembly with a class named Startup in hello default namespace of hello assembly.</span></span>  <span data-ttu-id="daf98-247">Veja um exemplo dessa classe:</span><span class="sxs-lookup"><span data-stu-id="daf98-247">Here is a sample of such a class:</span></span> 

    public class Startup
    {
    // Microsoft.SystemForCrossDomainIdentityManagement.IWebApplicationStarter, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IMonitor and  
    // Microsoft.SystemForCrossDomainIdentityManagement.Service are all defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service.dll.  

    Microsoft.SystemForCrossDomainIdentityManagement.IWebApplicationStarter starter;

    public Startup()
    {
        Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor = 
          new DevelopersMonitor();
        Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider = 
          new DevelopersProvider();
        this.starter = 
          new Microsoft.SystemForCrossDomainIdentityManagement.WebApplicationStarter(
            provider, 
            monitor);
    }

    public void Configuration(
      Owin.IAppBuilder builder) // Defined in in Owin.dll.  
    {
        this.starter.ConfigureApplication(builder);
    }
    }

### <a name="handling-endpoint-authentication"></a><span data-ttu-id="daf98-248">Manipulando a autenticação do ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="daf98-248">Handling endpoint authentication</span></span>
<span data-ttu-id="daf98-249">As solicitações do Active Directory do Azure incluem um token de portador do OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="daf98-249">Requests from Azure Active Directory include an OAuth 2.0 bearer token.</span></span>   <span data-ttu-id="daf98-250">Qualquer solicitação de saudação serviço receptor deve autenticar emissor hello como sendo o Active Directory do Azure em nome do locatário do Active Directory do Azure Olá esperado, para acesso toohello serviço de web do Azure Active Directory Graph.</span><span class="sxs-lookup"><span data-stu-id="daf98-250">Any service receiving hello request should authenticate hello issuer as being Azure Active Directory on behalf of hello expected Azure Active Directory tenant, for access toohello Azure Active Directory Graph web service.</span></span>  <span data-ttu-id="daf98-251">Token Olá, emissor de saudação é identificado por uma declaração de iss, como "iss": "https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/".</span><span class="sxs-lookup"><span data-stu-id="daf98-251">In hello token, hello issuer is identified by an iss claim, like, "iss":"https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/".</span></span>  <span data-ttu-id="daf98-252">Neste exemplo, o endereço de base de saudação do valor de declaração hello, https://sts.windows.net, identifica o Active Directory do Azure como Olá emissor, enquanto o segmento de endereço relativo, cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, hello é um identificador exclusivo do hello Azure Active Locatário de diretório em nome do qual Olá token foi emitido.</span><span class="sxs-lookup"><span data-stu-id="daf98-252">In this example, hello base address of hello claim value, https://sts.windows.net, identifies Azure Active Directory as hello issuer, while hello relative address segment, cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, is a unique identifier of hello Azure Active Directory tenant on behalf of which hello token was issued.</span></span>  <span data-ttu-id="daf98-253">Se Olá token foi emitido para acessar o serviço web do Azure Active Directory Graph hello, em seguida, identificador Olá desse serviço, 00000002-0000-0000-c000-000000000000, deve ser no valor de saudação do aud do token de saudação de declaração.</span><span class="sxs-lookup"><span data-stu-id="daf98-253">If hello token was issued for accessing hello Azure Active Directory Graph web service, then hello identifier of that service, 00000002-0000-0000-c000-000000000000, should be in hello value of hello token’s aud claim.</span></span>  

<span data-ttu-id="daf98-254">Os desenvolvedores que usam bibliotecas CLA Olá fornecidas pela Microsoft para a criação de um serviço SCIM podem autenticar solicitações do Azure Active Directory usando o pacote do ActiveDirectory Olá seguindo estas etapas:</span><span class="sxs-lookup"><span data-stu-id="daf98-254">Developers using hello CLA libraries provided by Microsoft for building a SCIM service can authenticate requests from Azure Active Directory using hello Microsoft.Owin.Security.ActiveDirectory package by following these steps:</span></span> 

1. <span data-ttu-id="daf98-255">Em um provedor implementa a propriedade de Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior de saudação fazendo com que ele retornar um toobe método chamado sempre que o serviço Olá é iniciado:</span><span class="sxs-lookup"><span data-stu-id="daf98-255">In a provider, implement hello Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior property by having it return a method toobe called whenever hello service is started:</span></span> 

  ````
    public override Action\<Owin.IAppBuilder, System.Web.Http.HttpConfiguration.HttpConfiguration\> StartupBehavior
    {
      get
      {
        return this.OnServiceStartup;
      }
    }

    private void OnServiceStartup(
      Owin.IAppBuilder applicationBuilder,  // Defined in Owin.dll.  
      System.Web.Http.HttpConfiguration configuration)  // Defined in System.Web.Http.dll.  
    {
    }
  ````

2. <span data-ttu-id="daf98-256">Adicione Olá após código toothat método toohave tooany qualquer solicitação de pontos de extremidade do serviço Olá autenticado como bearing um token emitido pelo Active Directory do Azure em nome de um locatário especificado, para acesso toohello serviço de web do Azure AD Graph:</span><span class="sxs-lookup"><span data-stu-id="daf98-256">Add hello following code toothat method toohave any request tooany of hello service’s endpoints authenticated as bearing a token issued by Azure Active Directory on behalf of a specified tenant, for access toohello Azure AD Graph web service:</span></span> 

  ````
    private void OnServiceStartup(
      Owin.IAppBuilder applicationBuilder IAppBuilder applicationBuilder, 
      System.Web.Http.HttpConfiguration HttpConfiguration configuration)
    {
      // IFilter is defined in System.Web.Http.dll.  
      System.Web.Http.Filters.IFilter authorizationFilter = 
        new System.Web.Http.AuthorizeAttribute(); // Defined in System.Web.Http.dll.configuration.Filters.Add(authorizationFilter);

      // SystemIdentityModel.Tokens.TokenValidationParameters is defined in    
      // System.IdentityModel.Token.Jwt.dll.
      SystemIdentityModel.Tokens.TokenValidationParameters tokenValidationParameters =     
        new TokenValidationParameters()
        {
          ValidAudience = "00000002-0000-0000-c000-000000000000"
        };

      // WindowsAzureActiveDirectoryBearerAuthenticationOptions is defined in 
      // Microsoft.Owin.Security.ActiveDirectory.dll
      Microsoft.Owin.Security.ActiveDirectory.
      WindowsAzureActiveDirectoryBearerAuthenticationOptions authenticationOptions =
        new WindowsAzureActiveDirectoryBearerAuthenticationOptions()    {
        TokenValidationParameters = tokenValidationParameters,
        Tenant = "03F9FCBC-EA7B-46C2-8466-F81917F3C15E" // Substitute hello appropriate tenant’s 
                                                      // identifier for this one.  
      };

      applicationBuilder.UseWindowsAzureActiveDirectoryBearerAuthentication(authenticationOptions);
    }
  ````


## <a name="user-and-group-schema"></a><span data-ttu-id="daf98-257">Esquema de usuários e grupos</span><span class="sxs-lookup"><span data-stu-id="daf98-257">User and group schema</span></span>
<span data-ttu-id="daf98-258">Active Directory do Azure pode provisionar os dois tipos de recursos tooSCIM serviços da web.</span><span class="sxs-lookup"><span data-stu-id="daf98-258">Azure Active Directory can provision two types of resources tooSCIM web services.</span></span>  <span data-ttu-id="daf98-259">Esses tipos de recurso são usuários e grupos.</span><span class="sxs-lookup"><span data-stu-id="daf98-259">Those types of resources are users and groups.</span></span>  

<span data-ttu-id="daf98-260">Recursos do usuário são identificados pelo identificador do esquema hello, urn: ietf:params:scim:schemas:extension:enterprise:2.0:User, que está incluído nesta especificação de protocolo: http://tools.ietf.org/html/draft-ietf-scim-core-schema.</span><span class="sxs-lookup"><span data-stu-id="daf98-260">User resources are identified by hello schema identifier, urn:ietf:params:scim:schemas:extension:enterprise:2.0:User, which is included in this protocol specification: http://tools.ietf.org/html/draft-ietf-scim-core-schema.</span></span>  <span data-ttu-id="daf98-261">mapeamento de padrão de saudação de atributos de saudação de usuários em atributos do Active Directory do Azure toohello de recursos de urn: ietf:params:scim:schemas:extension:enterprise:2.0:User é fornecido na tabela 1, abaixo.</span><span class="sxs-lookup"><span data-stu-id="daf98-261">hello default mapping of hello attributes of users in Azure Active Directory toohello attributes of urn:ietf:params:scim:schemas:extension:enterprise:2.0:User resources is provided in table 1, below.</span></span>  

<span data-ttu-id="daf98-262">Recursos do grupo são identificados pelo identificador do esquema hello, http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span><span class="sxs-lookup"><span data-stu-id="daf98-262">Group resources are identified by hello schema identifier, http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span></span>  <span data-ttu-id="daf98-263">Tabela 2, abaixo, o mapeamento de padrão mostra Olá de atributos de saudação de grupos de atributos do Active Directory do Azure toohello de recursos de http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span><span class="sxs-lookup"><span data-stu-id="daf98-263">Table 2, below, shows hello default mapping of hello attributes of groups in Azure Active Directory toohello attributes of http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group resources.</span></span>  

### <a name="table-1-default-user-attribute-mapping"></a><span data-ttu-id="daf98-264">Tabela 1: Mapeamento padrão de atributo do usuário</span><span class="sxs-lookup"><span data-stu-id="daf98-264">Table 1: Default user attribute mapping</span></span>
| <span data-ttu-id="daf98-265">Usuário do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="daf98-265">Azure Active Directory user</span></span> | <span data-ttu-id="daf98-266">urn:ietf:params:scim:schemas:extension:enterprise:2.0:User</span><span class="sxs-lookup"><span data-stu-id="daf98-266">urn:ietf:params:scim:schemas:extension:enterprise:2.0:User</span></span> |
| --- | --- |
| <span data-ttu-id="daf98-267">IsSoftDeleted</span><span class="sxs-lookup"><span data-stu-id="daf98-267">IsSoftDeleted</span></span> |<span data-ttu-id="daf98-268">ativo</span><span class="sxs-lookup"><span data-stu-id="daf98-268">active</span></span> |
| <span data-ttu-id="daf98-269">displayName</span><span class="sxs-lookup"><span data-stu-id="daf98-269">displayName</span></span> |<span data-ttu-id="daf98-270">displayName</span><span class="sxs-lookup"><span data-stu-id="daf98-270">displayName</span></span> |
| <span data-ttu-id="daf98-271">Facsimile-TelephoneNumber</span><span class="sxs-lookup"><span data-stu-id="daf98-271">Facsimile-TelephoneNumber</span></span> |<span data-ttu-id="daf98-272">phoneNumbers[type eq "fax"].value</span><span class="sxs-lookup"><span data-stu-id="daf98-272">phoneNumbers[type eq "fax"].value</span></span> |
| <span data-ttu-id="daf98-273">givenName</span><span class="sxs-lookup"><span data-stu-id="daf98-273">givenName</span></span> |<span data-ttu-id="daf98-274">name.givenName</span><span class="sxs-lookup"><span data-stu-id="daf98-274">name.givenName</span></span> |
| <span data-ttu-id="daf98-275">jobTitle</span><span class="sxs-lookup"><span data-stu-id="daf98-275">jobTitle</span></span> |<span data-ttu-id="daf98-276">título</span><span class="sxs-lookup"><span data-stu-id="daf98-276">title</span></span> |
| <span data-ttu-id="daf98-277">mail</span><span class="sxs-lookup"><span data-stu-id="daf98-277">mail</span></span> |<span data-ttu-id="daf98-278">emails[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="daf98-278">emails[type eq "work"].value</span></span> |
| <span data-ttu-id="daf98-279">mailNickname</span><span class="sxs-lookup"><span data-stu-id="daf98-279">mailNickname</span></span> |<span data-ttu-id="daf98-280">externalId</span><span class="sxs-lookup"><span data-stu-id="daf98-280">externalId</span></span> |
| <span data-ttu-id="daf98-281">manager</span><span class="sxs-lookup"><span data-stu-id="daf98-281">manager</span></span> |<span data-ttu-id="daf98-282">manager</span><span class="sxs-lookup"><span data-stu-id="daf98-282">manager</span></span> |
| <span data-ttu-id="daf98-283">Serviço Móvel</span><span class="sxs-lookup"><span data-stu-id="daf98-283">mobile</span></span> |<span data-ttu-id="daf98-284">phoneNumbers[type eq "mobile"].value</span><span class="sxs-lookup"><span data-stu-id="daf98-284">phoneNumbers[type eq "mobile"].value</span></span> |
| <span data-ttu-id="daf98-285">ID do objeto</span><span class="sxs-lookup"><span data-stu-id="daf98-285">objectId</span></span> |<span data-ttu-id="daf98-286">ID</span><span class="sxs-lookup"><span data-stu-id="daf98-286">id</span></span> |
| <span data-ttu-id="daf98-287">postalCode</span><span class="sxs-lookup"><span data-stu-id="daf98-287">postalCode</span></span> |<span data-ttu-id="daf98-288">addresses[type eq "work"].postalCode</span><span class="sxs-lookup"><span data-stu-id="daf98-288">addresses[type eq "work"].postalCode</span></span> |
| <span data-ttu-id="daf98-289">proxy-Addresses</span><span class="sxs-lookup"><span data-stu-id="daf98-289">proxy-Addresses</span></span> |<span data-ttu-id="daf98-290">emails[type eq "other"].Value</span><span class="sxs-lookup"><span data-stu-id="daf98-290">emails[type eq "other"].Value</span></span> |
| <span data-ttu-id="daf98-291">physical-Delivery-OfficeName</span><span class="sxs-lookup"><span data-stu-id="daf98-291">physical-Delivery-OfficeName</span></span> |<span data-ttu-id="daf98-292">addresses[type eq "other"].Formatted</span><span class="sxs-lookup"><span data-stu-id="daf98-292">addresses[type eq "other"].Formatted</span></span> |
| <span data-ttu-id="daf98-293">streetAddress</span><span class="sxs-lookup"><span data-stu-id="daf98-293">streetAddress</span></span> |<span data-ttu-id="daf98-294">addresses[type eq "work"].streetAddress</span><span class="sxs-lookup"><span data-stu-id="daf98-294">addresses[type eq "work"].streetAddress</span></span> |
| <span data-ttu-id="daf98-295">sobrenome</span><span class="sxs-lookup"><span data-stu-id="daf98-295">surname</span></span> |<span data-ttu-id="daf98-296">name.familyName</span><span class="sxs-lookup"><span data-stu-id="daf98-296">name.familyName</span></span> |
| <span data-ttu-id="daf98-297">telephone-Number</span><span class="sxs-lookup"><span data-stu-id="daf98-297">telephone-Number</span></span> |<span data-ttu-id="daf98-298">phoneNumbers[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="daf98-298">phoneNumbers[type eq "work"].value</span></span> |
| <span data-ttu-id="daf98-299">user-PrincipalName</span><span class="sxs-lookup"><span data-stu-id="daf98-299">user-PrincipalName</span></span> |<span data-ttu-id="daf98-300">userName</span><span class="sxs-lookup"><span data-stu-id="daf98-300">userName</span></span> |

### <a name="table-2-default-group-attribute-mapping"></a><span data-ttu-id="daf98-301">Tabela 2: Mapeamento padrão de atributo do grupo</span><span class="sxs-lookup"><span data-stu-id="daf98-301">Table 2: Default group attribute mapping</span></span>
| <span data-ttu-id="daf98-302">Grupo do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="daf98-302">Azure Active Directory group</span></span> | <span data-ttu-id="daf98-303">http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group</span><span class="sxs-lookup"><span data-stu-id="daf98-303">http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group</span></span> |
| --- | --- |
| <span data-ttu-id="daf98-304">displayName</span><span class="sxs-lookup"><span data-stu-id="daf98-304">displayName</span></span> |<span data-ttu-id="daf98-305">externalId</span><span class="sxs-lookup"><span data-stu-id="daf98-305">externalId</span></span> |
| <span data-ttu-id="daf98-306">mail</span><span class="sxs-lookup"><span data-stu-id="daf98-306">mail</span></span> |<span data-ttu-id="daf98-307">emails[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="daf98-307">emails[type eq "work"].value</span></span> |
| <span data-ttu-id="daf98-308">mailNickname</span><span class="sxs-lookup"><span data-stu-id="daf98-308">mailNickname</span></span> |<span data-ttu-id="daf98-309">displayName</span><span class="sxs-lookup"><span data-stu-id="daf98-309">displayName</span></span> |
| <span data-ttu-id="daf98-310">membros</span><span class="sxs-lookup"><span data-stu-id="daf98-310">members</span></span> |<span data-ttu-id="daf98-311">membros</span><span class="sxs-lookup"><span data-stu-id="daf98-311">members</span></span> |
| <span data-ttu-id="daf98-312">ID do objeto</span><span class="sxs-lookup"><span data-stu-id="daf98-312">objectId</span></span> |<span data-ttu-id="daf98-313">ID</span><span class="sxs-lookup"><span data-stu-id="daf98-313">id</span></span> |
| <span data-ttu-id="daf98-314">proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="daf98-314">proxyAddresses</span></span> |<span data-ttu-id="daf98-315">emails[type eq "other"].Value</span><span class="sxs-lookup"><span data-stu-id="daf98-315">emails[type eq "other"].Value</span></span> |

## <a name="user-provisioning-and-de-provisioning"></a><span data-ttu-id="daf98-316">Provisionamento e desprovisionamento de usuários</span><span class="sxs-lookup"><span data-stu-id="daf98-316">User provisioning and de-provisioning</span></span>
<span data-ttu-id="daf98-317">Olá mensagens de saudação do ilustração mostra que o Active Directory do Azure envia tooa SCIM serviço toomanage saudação do ciclo de vida de um usuário em outro repositório de identidade a seguir.</span><span class="sxs-lookup"><span data-stu-id="daf98-317">hello following illustration shows hello messages that Azure Active Directory sends tooa SCIM service toomanage hello lifecycle of a user in another identity store.</span></span> <span data-ttu-id="daf98-318">diagrama de saudação também mostra como um serviço SCIM implementado usando bibliotecas CLI Olá fornecido pela Microsoft para criar que tais serviços essas solicitações se traduz em métodos de toohello chamadas de um provedor.</span><span class="sxs-lookup"><span data-stu-id="daf98-318">hello diagram also shows how a SCIM service implemented using hello CLI libraries provided by Microsoft for building such services translate those requests into calls toohello methods of a provider.</span></span>  

<span data-ttu-id="daf98-319">![][4]
*Figura 5: Sequência de provisionamento e desprovisionamento de usuário*</span><span class="sxs-lookup"><span data-stu-id="daf98-319">![][4]
*Figure 5: User provisioning and de-provisioning sequence*</span></span>

1. <span data-ttu-id="daf98-320">Consultas do Active Directory do Azure Olá serviço para um usuário com um valor de atributo externalId correspondência do valor de atributo de mailNickname Olá de um usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="daf98-320">Azure Active Directory queries hello service for a user with an externalId attribute value matching hello mailNickname attribute value of a user in Azure AD.</span></span> <span data-ttu-id="daf98-321">Olá consulta é expressa como uma solicitação do protocolo HTTP (Hypertext Transfer), como neste exemplo, no qual jyoung é um exemplo de um mailNickname de um usuário no Active Directory do Azure:</span><span class="sxs-lookup"><span data-stu-id="daf98-321">hello query is expressed as a Hypertext Transfer Protocol (HTTP) request such as this example, wherein jyoung is a sample of a mailNickname of a user in Azure Active Directory:</span></span> 
  ````
    GET https://.../scim/Users?filter=externalId eq jyoung HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="daf98-322">Se serviço Olá foi criado usando bibliotecas de Common Language Infrastructure Olá fornecidas pela Microsoft para a implementação de serviços SCIM, em seguida, solicitação Olá é convertida em toohello uma chamada de método de consulta do provedor do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="daf98-322">If hello service was built using hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then hello request is translated into a call toohello Query method of hello service’s provider.</span></span>  <span data-ttu-id="daf98-323">Aqui está a assinatura de saudação do método:</span><span class="sxs-lookup"><span data-stu-id="daf98-323">Here is hello signature of that method:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Protocol.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource[]> Query(
      Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters parameters, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="daf98-324">Esta é a definição de saudação da interface de Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters hello:</span><span class="sxs-lookup"><span data-stu-id="daf98-324">Here is hello definition of hello Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters interface:</span></span> 
  ````
    public interface IQueryParameters: 
      Microsoft.SystemForCrossDomainIdentityManagement.IRetrievalParameters
    {
        System.Collections.Generic.IReadOnlyCollection <Microsoft.SystemForCrossDomainIdentityManagement.IFilter> AlternateFilters 
        { get; }
    }

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IRetrievalParameters
    {
      system.Collections.Generic.IReadOnlyCollection<string> ExcludedAttributePaths 
      { get; }
      System.Collections.Generic.IReadOnlyCollection<string> RequestedAttributePaths 
      { get; }
      string SchemaIdentifier 
      { get; }
    }

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IFilter
    {
        Microsoft.SystemForCrossDomainIdentityManagement.IFilter AdditionalFilter 
          { get; set; }
        string AttributePath 
          { get; } 
        Microsoft.SystemForCrossDomainIdentityManagement.ComparisonOperator FilterOperator 
          { get; }
        string ComparisonValue 
          { get; }
    }

    public enum Microsoft.SystemForCrossDomainIdentityManagement.ComparisonOperator
    {
        Equals
    }
  ````
  <span data-ttu-id="daf98-325">Em Olá seguindo o exemplo de uma consulta para um usuário com um valor especificado para o atributo de externalId hello, valores de argumentos Olá passados toohello método de consulta são:</span><span class="sxs-lookup"><span data-stu-id="daf98-325">In hello following sample of a query for a user with a given value for hello externalId attribute, values of hello arguments passed toohello Query method are:</span></span> 
  * <span data-ttu-id="daf98-326">parameters.AlternateFilters.Count: 1</span><span class="sxs-lookup"><span data-stu-id="daf98-326">parameters.AlternateFilters.Count: 1</span></span>
  * <span data-ttu-id="daf98-327">parameters.AlternateFilters.ElementAt(0).AttributePath: "externalId"</span><span class="sxs-lookup"><span data-stu-id="daf98-327">parameters.AlternateFilters.ElementAt(0).AttributePath: "externalId"</span></span>
  * <span data-ttu-id="daf98-328">parameters.AlternateFilters.ElementAt(0).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="daf98-328">parameters.AlternateFilters.ElementAt(0).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="daf98-329">parameters.AlternateFilter.ElementAt(0).ComparisonValue: "jyoung"</span><span class="sxs-lookup"><span data-stu-id="daf98-329">parameters.AlternateFilter.ElementAt(0).ComparisonValue: "jyoung"</span></span>
  * <span data-ttu-id="daf98-330">correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin.RequestId"]</span><span class="sxs-lookup"><span data-stu-id="daf98-330">correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin.RequestId"]</span></span> 

2. <span data-ttu-id="daf98-331">Se Olá resposta tooa toohello web serviço de consulta para um usuário com um valor de atributo externalId que coincide com o valor do atributo mailNickname Olá de um usuário não retornar todos os usuários, Active Directory do Azure solicita que provisão de serviço Olá um usuário correspondente toohello um no Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="daf98-331">If hello response tooa query toohello web service for a user with an externalId attribute value that matches hello mailNickname attribute value of a user does not return any users, then Azure Active Directory requests that hello service provision a user corresponding toohello one in Azure Active Directory.</span></span>  <span data-ttu-id="daf98-332">Veja um exemplo de tal solicitação:</span><span class="sxs-lookup"><span data-stu-id="daf98-332">Here is an example of such a request:</span></span> 
  ````
    POST https://.../scim/Users HTTP/1.1
    Authorization: Bearer ...
    Content-type: application/json
    {
      "schemas":
      [
        "urn:ietf:params:scim:schemas:core:2.0:User",
        "urn:ietf:params:scim:schemas:extension:enterprise:2.0User"],
      "externalId":"jyoung",
      "userName":"jyoung",
      "active":true,
      "addresses":null,
      "displayName":"Joy Young",
      "emails": [
        {
          "type":"work",
          "value":"jyoung@Contoso.com",
          "primary":true}],
      "meta": {
        "resourceType":"User"},
       "name":{
        "familyName":"Young",
        "givenName":"Joy"},
      "phoneNumbers":null,
      "preferredLanguage":null,
      "title":null,
      "department":null,
      "manager":null}
  ````
  <span data-ttu-id="daf98-333">bibliotecas de Common Language Infrastructure Olá fornecidas pela Microsoft para a implementação de serviços SCIM significa que a solicitação toohello uma chamada de método de criação de saudação do provedor de.</span><span class="sxs-lookup"><span data-stu-id="daf98-333">hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services would translate that request into a call toohello Create method of hello service’s provider.</span></span>  <span data-ttu-id="daf98-334">método Create da saudação tem essa assinatura:</span><span class="sxs-lookup"><span data-stu-id="daf98-334">hello Create method has this signature:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> Create(
      Microsoft.SystemForCrossDomainIdentityManagement.Resource resource, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="daf98-335">Em uma solicitação tooprovision um usuário, o valor de saudação do argumento de recurso Olá é uma instância de saudação Microsoft.SystemForCrossDomainIdentityManagement.</span><span class="sxs-lookup"><span data-stu-id="daf98-335">In a request tooprovision a user, hello value of hello resource argument is an instance of hello Microsoft.SystemForCrossDomainIdentityManagement.</span></span> <span data-ttu-id="daf98-336">Classe Core2EnterpriseUser, definida na biblioteca de Microsoft.SystemForCrossDomainIdentityManagement.Schemas hello.</span><span class="sxs-lookup"><span data-stu-id="daf98-336">Core2EnterpriseUser class, defined in hello Microsoft.SystemForCrossDomainIdentityManagement.Schemas library.</span></span>  <span data-ttu-id="daf98-337">Se o usuário de Olá Olá solicitação tooprovision for bem-sucedida, em seguida, hello implementação do método hello é tooreturn esperada uma instância do hello Microsoft.SystemForCrossDomainIdentityManagement.</span><span class="sxs-lookup"><span data-stu-id="daf98-337">If hello request tooprovision hello user succeeds, then hello implementation of hello method is expected tooreturn an instance of hello Microsoft.SystemForCrossDomainIdentityManagement.</span></span> <span data-ttu-id="daf98-338">Classe Core2EnterpriseUser, com valor de saudação da propriedade do identificador de Olá definir toohello o identificador exclusivo do usuário recentemente provisionados hello.</span><span class="sxs-lookup"><span data-stu-id="daf98-338">Core2EnterpriseUser class, with hello value of hello Identifier property set toohello unique identifier of hello newly provisioned user.</span></span>  

3. <span data-ttu-id="daf98-339">tooupdate um usuário conhecido tooexist em um repositório de identidade apoiado por um SCIM, Active Directory do Azure continua solicitando o estado atual de saudação do usuário do serviço de saudação com uma solicitação, como:</span><span class="sxs-lookup"><span data-stu-id="daf98-339">tooupdate a user known tooexist in an identity store fronted by an SCIM, Azure Active Directory proceeds by requesting hello current state of that user from hello service with a request such as:</span></span> 
  ````
    GET ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="daf98-340">Em um serviço criado usando bibliotecas de Common Language Infrastructure Olá fornecidas pela Microsoft para a implementação de serviços SCIM, a solicitação de saudação é convertida em toohello uma chamada de método de recuperação de saudação do provedor de.</span><span class="sxs-lookup"><span data-stu-id="daf98-340">In a service built using hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, hello request is translated into a call toohello Retrieve method of hello service’s provider.</span></span>  <span data-ttu-id="daf98-341">Aqui está a assinatura de saudação do método de recuperação hello:</span><span class="sxs-lookup"><span data-stu-id="daf98-341">Here is hello signature of hello Retrieve method:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource and 
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters 
    // are defined in Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  
    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> 
       Retrieve(
         Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters 
           parameters, 
           string correlationIdentifier);

    public interface 
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters:   
        IRetrievalParameters
        {
          Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier 
            ResourceIdentifier 
              { get; }
    }
    public interface Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier
    {
        string Identifier 
          { get; set; }
        string Microsoft.SystemForCrossDomainIdentityManagement.SchemaIdentifier 
          { get; set; }
    }
  ````
  <span data-ttu-id="daf98-342">No exemplo de saudação do estado atual de saudação do tooretrieve solicitação de um usuário, valores hello das propriedades de saudação do objeto de saudação fornecido como valor de saudação do argumento de parâmetros de saudação são:</span><span class="sxs-lookup"><span data-stu-id="daf98-342">In hello example of a request tooretrieve hello current state of a user, hello values of hello properties of hello object provided as hello value of hello parameters argument are as follows:</span></span> 
  
  * <span data-ttu-id="daf98-343">Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="daf98-343">Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="daf98-344">SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="daf98-344">SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

4. <span data-ttu-id="daf98-345">Se um atributo de referência for toobe atualizado, em seguida, Active Directory do Azure consultas Olá serviço toodetermine ou não hello atual valor do atributo de referência de saudação no repositório de identidades Olá apoiado por serviço Olá já corresponde o valor de saudação do atributo no Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="daf98-345">If a reference attribute is toobe updated, then Azure Active Directory queries hello service toodetermine whether or not hello current value of hello reference attribute in hello identity store fronted by hello service already matches hello value of that attribute in Azure Active Directory.</span></span> <span data-ttu-id="daf98-346">Para usuários, Olá somente de quais hello valor atual é consultado dessa maneira é Olá manager atributo.</span><span class="sxs-lookup"><span data-stu-id="daf98-346">For users, hello only attribute of which hello current value is queried in this way is hello manager attribute.</span></span> <span data-ttu-id="daf98-347">Aqui está um exemplo de uma solicitação toodetermine se o atributo de gerente de saudação de um objeto específico do usuário atualmente tem um determinado valor:</span><span class="sxs-lookup"><span data-stu-id="daf98-347">Here is an example of a request toodetermine whether hello manager attribute of a particular user object currently has a certain value:</span></span> 
  ````
    GET ~/scim/Users?filter=id eq 54D382A4-2050-4C03-94D1-E769F1D15682 and manager eq 2819c223-7f76-453a-919d-413861904646&attributes=id HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="daf98-348">Olá valor de parâmetro de consulta de atributos hello, id, significa que se existe um objeto de usuário que satisfaz a expressão Olá fornecido como valor de saudação do parâmetro de consulta de filtro de saudação, serviço Olá é esperado toorespond com um urn: ietf:params:scim:schemas: núcleo: 2.0:User ou urn: ietf:params:scim:schemas:extension:enterprise:2.0:User recursos, incluindo apenas o valor de saudação do atributo de id do recurso.</span><span class="sxs-lookup"><span data-stu-id="daf98-348">hello value of hello attributes query parameter, id, signifies that if a user object exists that satisfies hello expression provided as hello value of hello filter query parameter, then hello service is expected toorespond with a urn:ietf:params:scim:schemas:core:2.0:User or urn:ietf:params:scim:schemas:extension:enterprise:2.0:User resource, including only hello value of that resource’s id attribute.</span></span>  <span data-ttu-id="daf98-349">Olá valor Olá **id** atributo conhecido toohello solicitante.</span><span class="sxs-lookup"><span data-stu-id="daf98-349">hello value of hello **id** attribute is known toohello requestor.</span></span> <span data-ttu-id="daf98-350">Ele está incluído no valor de saudação do parâmetro de consulta de filtro Olá; Olá finalidade pedindo a ela é realmente toorequest uma representação mínima de um recurso que satisfazem a expressão de filtro hello como uma indicação de se qualquer tal objeto existente.</span><span class="sxs-lookup"><span data-stu-id="daf98-350">It is included in hello value of hello filter query parameter; hello purpose of asking for it is actually toorequest a minimal representation of a resource that satisfying hello filter expression as an indication of whether or not any such object exists.</span></span>   

  <span data-ttu-id="daf98-351">Se serviço Olá foi criado usando bibliotecas de Common Language Infrastructure Olá fornecidas pela Microsoft para a implementação de serviços SCIM, em seguida, solicitação Olá é convertida em toohello uma chamada de método de consulta do provedor do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="daf98-351">If hello service was built using hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then hello request is translated into a call toohello Query method of hello service’s provider.</span></span> <span data-ttu-id="daf98-352">valor de saudação das propriedades de saudação do objeto de saudação fornecido como valor de saudação do argumento de parâmetros de saudação são da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="daf98-352">hello value of hello properties of hello object provided as hello value of hello parameters argument are as follows:</span></span> 
  
  * <span data-ttu-id="daf98-353">parameters.AlternateFilters.Count: 2</span><span class="sxs-lookup"><span data-stu-id="daf98-353">parameters.AlternateFilters.Count: 2</span></span>
  * <span data-ttu-id="daf98-354">parameters.AlternateFilters.ElementAt(x).AttributePath: "id"</span><span class="sxs-lookup"><span data-stu-id="daf98-354">parameters.AlternateFilters.ElementAt(x).AttributePath: "id"</span></span>
  * <span data-ttu-id="daf98-355">parameters.AlternateFilters.ElementAt(x).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="daf98-355">parameters.AlternateFilters.ElementAt(x).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="daf98-356">parameters.AlternateFilter.ElementAt(x).ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="daf98-356">parameters.AlternateFilter.ElementAt(x).ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="daf98-357">parameters.AlternateFilters.ElementAt(y).AttributePath: "manager"</span><span class="sxs-lookup"><span data-stu-id="daf98-357">parameters.AlternateFilters.ElementAt(y).AttributePath: "manager"</span></span>
  * <span data-ttu-id="daf98-358">parameters.AlternateFilters.ElementAt(y).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="daf98-358">parameters.AlternateFilters.ElementAt(y).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="daf98-359">parameters.AlternateFilter.ElementAt(y).ComparisonValue: "2819c223-7f76-453a-919d-413861904646"</span><span class="sxs-lookup"><span data-stu-id="daf98-359">parameters.AlternateFilter.ElementAt(y).ComparisonValue: "2819c223-7f76-453a-919d-413861904646"</span></span>
  * <span data-ttu-id="daf98-360">parameters.RequestedAttributePaths.ElementAt(0): "id"</span><span class="sxs-lookup"><span data-stu-id="daf98-360">parameters.RequestedAttributePaths.ElementAt(0): "id"</span></span>
  * <span data-ttu-id="daf98-361">parameters.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="daf98-361">parameters.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

  <span data-ttu-id="daf98-362">Aqui, valor de saudação do índice Olá x pode ser 0 e valor Olá Olá índice y pode ser 1, ou Olá valor x pode ser 1 e valor Olá y pode ser 0, dependendo da ordem de saudação de expressões de saudação do parâmetro de consulta de filtro de saudação.</span><span class="sxs-lookup"><span data-stu-id="daf98-362">Here, hello value of hello index x may be 0 and hello value of hello index y may be 1, or hello value of x may be 1 and hello value of y may be 0, depending on hello order of hello expressions of hello filter query parameter.</span></span>   

5. <span data-ttu-id="daf98-363">Aqui está um exemplo de uma solicitação de tooupdate de serviço do Active Directory do Azure tooan SCIM um usuário:</span><span class="sxs-lookup"><span data-stu-id="daf98-363">Here is an example of a request from Azure Active Directory tooan SCIM service tooupdate a user:</span></span> 
  ````
    PATCH ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
    Content-type: application/json
    {
      "schemas": 
      [
        "urn:ietf:params:scim:api:messages:2.0:PatchOp"],
      "Operations":
      [
        {
          "op":"Add",
          "path":"manager",
          "value":
            [
              {
                "$ref":"http://.../scim/Users/2819c223-7f76-453a-919d-413861904646",
                "value":"2819c223-7f76-453a-919d-413861904646"}]}]}
  ````
  <span data-ttu-id="daf98-364">bibliotecas do Microsoft Common Language Infrastructure Olá para implementar serviços SCIM converterá solicitação Olá em toohello uma chamada de método de atualização do provedor do serviço hello.</span><span class="sxs-lookup"><span data-stu-id="daf98-364">hello Microsoft Common Language Infrastructure libraries for implementing SCIM services would translate hello request into a call toohello Update method of hello service’s provider.</span></span> <span data-ttu-id="daf98-365">Aqui está a assinatura Olá Olá método de atualização:</span><span class="sxs-lookup"><span data-stu-id="daf98-365">Here is hello signature of hello Update method:</span></span> 
  ````
    // System.Threading.Tasks.Tasks and 
    // System.Collections.Generic.IReadOnlyCollection<T>
    // are defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IPatch, 
    // Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation, 
    // Microsoft.SystemForCrossDomainIdentityManagement.OperationName, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IPath and 
    // Microsoft.SystemForCrossDomainIdentityManagement.OperationValue 
    // are all defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 

    System.Threading.Tasks.Task Update(
      Microsoft.SystemForCrossDomainIdentityManagement.IPatch patch, 
      string correlationIdentifier);

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IPatch
    {
    Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase 
      PatchRequest 
        { get; set; }
    Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier 
      ResourceIdentifier 
        { get; set; }        
    }

    public class PatchRequest2: 
      Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase
    {
    public System.Collections.Generic.IReadOnlyCollection
      <Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation> 
        Operations
        { get;}

    public void AddOperation(
      Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation operation);
    }

    public class PatchOperation
    {
    public Microsoft.SystemForCrossDomainIdentityManagement.OperationName 
      Name
      { get; set; }

    public Microsoft.SystemForCrossDomainIdentityManagement.IPath 
      Path
      { get; set; }

    public System.Collections.Generic.IReadOnlyCollection
      <Microsoft.SystemForCrossDomainIdentityManagement.OperationValue> Value
      { get; }

    public void AddValue(
      Microsoft.SystemForCrossDomainIdentityManagement.OperationValue value);
    }

    public enum OperationName
    {
      Add,
      Remove,
      Replace
    }

    public interface IPath
    {
      string AttributePath { get; }
      System.Collections.Generic.IReadOnlyCollection<IFilter> SubAttributes { get; }
      Microsoft.SystemForCrossDomainIdentityManagement.IPath ValuePath { get; }
    }

    public class OperationValue
    {
      public string Reference
      { get; set; }

      public string Value
      { get; set; }
    }
  ````
    <span data-ttu-id="daf98-366">No exemplo hello de uma solicitação de tooupdate um usuário, o objeto de saudação fornecido como valor de saudação do argumento de patch Olá tem esses valores de propriedade:</span><span class="sxs-lookup"><span data-stu-id="daf98-366">In hello example of a request tooupdate a user, hello object provided as hello value of hello patch argument has these property values:</span></span> 
  
  * <span data-ttu-id="daf98-367">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="daf98-367">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="daf98-368">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="daf98-368">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>
  * <span data-ttu-id="daf98-369">(PatchRequest as PatchRequest2).Operations.Count: 1</span><span class="sxs-lookup"><span data-stu-id="daf98-369">(PatchRequest as PatchRequest2).Operations.Count: 1</span></span>
  * <span data-ttu-id="daf98-370">(PatchRequest as PatchRequest2).Operations.ElementAt(0).OperationName: OperationName.Add</span><span class="sxs-lookup"><span data-stu-id="daf98-370">(PatchRequest as PatchRequest2).Operations.ElementAt(0).OperationName: OperationName.Add</span></span>
  * <span data-ttu-id="daf98-371">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Path.AttributePath: "manager"</span><span class="sxs-lookup"><span data-stu-id="daf98-371">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Path.AttributePath: "manager"</span></span>
  * <span data-ttu-id="daf98-372">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.Count: 1</span><span class="sxs-lookup"><span data-stu-id="daf98-372">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.Count: 1</span></span>
  * <span data-ttu-id="daf98-373">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Reference: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646</span><span class="sxs-lookup"><span data-stu-id="daf98-373">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Reference: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646</span></span>
  * <span data-ttu-id="daf98-374">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Value: 2819c223-7f76-453a-919d-413861904646</span><span class="sxs-lookup"><span data-stu-id="daf98-374">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Value: 2819c223-7f76-453a-919d-413861904646</span></span>

6. <span data-ttu-id="daf98-375">um usuário de um repositório de identidade de provisionar toode apoiado por um serviço SCIM, AD do Azure envia uma solicitação, como:</span><span class="sxs-lookup"><span data-stu-id="daf98-375">toode-provision a user from an identity store fronted by an SCIM service, Azure AD sends a request such as:</span></span> 
  ````
    DELETE ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="daf98-376">Se o serviço de saudação foi criado usando bibliotecas de Common Language Infrastructure Olá fornecidas pela Microsoft para a implementação de serviços SCIM, em seguida, solicitação Olá é convertida em toohello uma chamada de método de exclusão de saudação do provedor de.</span><span class="sxs-lookup"><span data-stu-id="daf98-376">If hello service was built using hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then hello request is translated into a call toohello Delete method of hello service’s provider.</span></span>   <span data-ttu-id="daf98-377">Esse método tem esta assinatura:</span><span class="sxs-lookup"><span data-stu-id="daf98-377">That method has this signature:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // is defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 
    System.Threading.Tasks.Task Delete(
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier  
        resourceIdentifier, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="daf98-378">objeto Olá fornecido como valor de saudação do argumento de resourceIdentifier Olá tem esses valores de propriedade no exemplo hello de uma solicitação toode-provisionar um usuário:</span><span class="sxs-lookup"><span data-stu-id="daf98-378">hello object provided as hello value of hello resourceIdentifier argument has these property values in hello example of a request toode-provision a user:</span></span> 
  
  * <span data-ttu-id="daf98-379">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="daf98-379">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="daf98-380">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="daf98-380">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

## <a name="group-provisioning-and-de-provisioning"></a><span data-ttu-id="daf98-381">Provisionamento e desprovisionamento de grupo</span><span class="sxs-lookup"><span data-stu-id="daf98-381">Group provisioning and de-provisioning</span></span>
<span data-ttu-id="daf98-382">Olá mensagens de saudação do ilustração mostra que AcD Azure envia tooa SCIM serviço toomanage saudação do ciclo de vida de um grupo em outro repositório de identidade a seguir.</span><span class="sxs-lookup"><span data-stu-id="daf98-382">hello following illustration shows hello messages that Azure AcD sends tooa SCIM service toomanage hello lifecycle of a group in another identity store.</span></span>  <span data-ttu-id="daf98-383">Essas mensagens são diferentes de mensagens de saudação pertencente toousers de três maneiras:</span><span class="sxs-lookup"><span data-stu-id="daf98-383">Those messages differ from hello messages pertaining toousers in three ways:</span></span> 

* <span data-ttu-id="daf98-384">esquema de saudação de um recurso de grupo é identificada como http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span><span class="sxs-lookup"><span data-stu-id="daf98-384">hello schema of a group resource is identified as http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span></span>  
* <span data-ttu-id="daf98-385">Solicitações tooretrieve grupos estipulam atributo Olá membros é toobe excluído de qualquer recurso fornecido na solicitação de toohello de resposta.</span><span class="sxs-lookup"><span data-stu-id="daf98-385">Requests tooretrieve groups stipulate that hello members attribute is toobe excluded from any resource provided in response toohello request.</span></span>  
* <span data-ttu-id="daf98-386">Toodetermine solicitações se um atributo de referência tem um determinado valor são solicitações sobre o atributo de membros de saudação.</span><span class="sxs-lookup"><span data-stu-id="daf98-386">Requests toodetermine whether a reference attribute has a certain value are requests about hello members attribute.</span></span>  

<span data-ttu-id="daf98-387">![][5]
*Figura 6: sequência de provisionamento e desprovisionamento de grupo*</span><span class="sxs-lookup"><span data-stu-id="daf98-387">![][5]
*Figure 6: Group provisioning and de-provisioning sequence*</span></span>

## <a name="related-articles"></a><span data-ttu-id="daf98-388">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="daf98-388">Related articles</span></span>
* [<span data-ttu-id="daf98-389">Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="daf98-389">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="daf98-390">Automatizar o provisionamento de usuário/desprovisionamento tooSaaS aplicativos</span><span class="sxs-lookup"><span data-stu-id="daf98-390">Automate User Provisioning/Deprovisioning tooSaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="daf98-391">Personalizando os mapeamentos de atributos para provisionamento de usuários</span><span class="sxs-lookup"><span data-stu-id="daf98-391">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="daf98-392">Escrevendo expressões para mapeamentos de atributo</span><span class="sxs-lookup"><span data-stu-id="daf98-392">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="daf98-393">Filtros de escopo para provisionamento de usuários</span><span class="sxs-lookup"><span data-stu-id="daf98-393">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="daf98-394">Notificações de provisionamento de conta</span><span class="sxs-lookup"><span data-stu-id="daf98-394">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="daf98-395">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS</span><span class="sxs-lookup"><span data-stu-id="daf98-395">List of Tutorials on How tooIntegrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[0]: ./media/active-directory-scim-provisioning/scim-figure-1.PNG
[1]: ./media/active-directory-scim-provisioning/scim-figure-2a.PNG
[2]: ./media/active-directory-scim-provisioning/scim-figure-2b.PNG
[3]: ./media/active-directory-scim-provisioning/scim-figure-3.PNG
[4]: ./media/active-directory-scim-provisioning/scim-figure-4.PNG
[5]: ./media/active-directory-scim-provisioning/scim-figure-5.PNG
