---
title: "Usar o sistema para gerenciamento de identidade de domínio cruzado provisiona automaticamente usuários e grupos do Azure Active Directory a aplicativos | Microsoft Docs"
description: "O Azure Active Directory pode provisionar automaticamente usuários e grupos a qualquer repositório de identidades ou aplicativos que seja administrado por um serviço Web com a interface definida na especificação do protocolo SCIM."
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
ms.openlocfilehash: 91978cee88d55c99bcb63c63cdaf01581ae84668
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="using-system-for-cross-domain-identity-management-to-automatically-provision-users-and-groups-from-azure-active-directory-to-applications"></a><span data-ttu-id="c98e2-103">Usar o sistema de gerenciamento de identidade de domínio cruzado para provisionar automaticamente usuários e grupos do Azure Active Directory a aplicativos</span><span class="sxs-lookup"><span data-stu-id="c98e2-103">Using System for Cross-Domain Identity Management to automatically provision users and groups from Azure Active Directory to applications</span></span>

## <a name="overview"></a><span data-ttu-id="c98e2-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="c98e2-104">Overview</span></span>
<span data-ttu-id="c98e2-105">O Azure Active Directory (Azure AD) pode provisionar automaticamente usuários e grupos para qualquer repositório de identidades ou aplicativos que seja administrado por um serviço Web com a interface definida na [especificação do protocolo Sistema de Gerenciamento de Identidade entre Domínios (SCIM) 2.0](https://tools.ietf.org/html/draft-ietf-scim-api-19).</span><span class="sxs-lookup"><span data-stu-id="c98e2-105">Azure Active Directory (Azure AD) can automatically provision users and groups to any application or identity store that is fronted by a web service with the interface defined in the [System for Cross-Domain Identity Management (SCIM) 2.0 protocol specification](https://tools.ietf.org/html/draft-ietf-scim-api-19).</span></span> <span data-ttu-id="c98e2-106">O Azure Active Directory pode enviar solicitações para criar, modificar ou excluir usuários e grupos atribuídos ao serviço Web.</span><span class="sxs-lookup"><span data-stu-id="c98e2-106">Azure Active Directory can send requests to create, modify, or delete assigned users and groups to the web service.</span></span> <span data-ttu-id="c98e2-107">O serviço Web pode então converter essas solicitações em operações no repositório de identidades de destino.</span><span class="sxs-lookup"><span data-stu-id="c98e2-107">The web service can then translate those requests into operations on the target identity store.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="c98e2-108">A Microsoft recomenda que você gerencie o Azure AD usando o [Centro de administração do AD do Azure](https://aad.portal.azure.com) no portal do Azure em vez de usar o portal clássico do Azure mencionado neste artigo.</span><span class="sxs-lookup"><span data-stu-id="c98e2-108">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> 



<span data-ttu-id="c98e2-109">![][0]
*Figura 1: Provisionando do Azure Active Directory a um repositório de identidades por meio de um serviço Web*</span><span class="sxs-lookup"><span data-stu-id="c98e2-109">![][0]
*Figure 1: Provisioning from Azure Active Directory to an identity store via a web service*</span></span>

<span data-ttu-id="c98e2-110">Esse recurso pode ser usado juntamente com o recurso "traga seu próprio aplicativo" no Azure AD para habilitar o logon único e o provisionamento automático de usuário de aplicativos que forneçam ou comecem com um serviço Web SCIM.</span><span class="sxs-lookup"><span data-stu-id="c98e2-110">This capability can be used in conjunction with the “bring your own app” capability in Azure AD to enable single sign-on and automatic user provisioning for applications that provide or are fronted by a SCIM web service.</span></span>

<span data-ttu-id="c98e2-111">Há dois casos de uso para utilizar SCIM no Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="c98e2-111">There are two use cases for using SCIM in Azure Active Directory:</span></span>

* <span data-ttu-id="c98e2-112">**Provisionamento de usuários e grupos a aplicativos que dão suporte a SCIM** Aplicativos que dão suporte a SCIM 2.0 e usam tokens de portador OAuth para autenticação funcionam com o Azure AD sem necessidade de configuração.</span><span class="sxs-lookup"><span data-stu-id="c98e2-112">**Provisioning users and groups to applications that support SCIM** Applications that support SCIM 2.0 and use OAuth bearer tokens for authentication works with Azure AD without configuration.</span></span>
* <span data-ttu-id="c98e2-113">**Criar a sua própria solução de provisionamento para aplicativos que dão suporte a outro provisionamento baseado em API** para aplicativos não SCIM, você pode criar um ponto de extremidade SCIM para converter entre o ponto de extremidade SCIM do Azure AD e qualquer API à qual o aplicativo dê suporte para provisionamento de usuários.</span><span class="sxs-lookup"><span data-stu-id="c98e2-113">**Build your own provisioning solution for applications that support other API-based provisioning** For non-SCIM applications, you can create a SCIM endpoint to translate between the Azure AD SCIM endpoint and any API the application supports for user provisioning.</span></span> <span data-ttu-id="c98e2-114">Para ajudá-lo a desenvolver um ponto de extremidade SCIM, fornecemos bibliotecas Common Language Infrastructure (CLI) com exemplos de código que mostram como fornecer um ponto de extremidade SCIM e converter mensagens SCIM.</span><span class="sxs-lookup"><span data-stu-id="c98e2-114">To help you develop a SCIM endpoint, we provide Common Language Infrastructure (CLI) libraries along with code samples that show you how to do provide a SCIM endpoint and translate SCIM messages.</span></span>  

## <a name="provisioning-users-and-groups-to-applications-that-support-scim"></a><span data-ttu-id="c98e2-115">Provisionamento de usuários e grupos a aplicativos que dão suporte a SCIM</span><span class="sxs-lookup"><span data-stu-id="c98e2-115">Provisioning users and groups to applications that support SCIM</span></span>
<span data-ttu-id="c98e2-116">O Azure AD pode ser configurado para provisionar automaticamente usuários e grupos atribuídos a aplicativos que implementam um serviço Web de [Sistema de Gerenciamento de Identidade entre Domínios 2 (SCIM)](https://tools.ietf.org/html/draft-ietf-scim-api-19) e aceitam tokens de portador OAuth para autenticação.</span><span class="sxs-lookup"><span data-stu-id="c98e2-116">Azure AD can be configured to automatically provision assigned users and groups to applications that implement a [System for Cross-domain Identity Management 2 (SCIM)](https://tools.ietf.org/html/draft-ietf-scim-api-19) web service and accept OAuth bearer tokens for authentication.</span></span> <span data-ttu-id="c98e2-117">Dentro da especificação SCIM 2.0, os aplicativos devem satisfazer estes requisitos:</span><span class="sxs-lookup"><span data-stu-id="c98e2-117">Within the SCIM 2.0 specification, applications must meet these requirements:</span></span>

* <span data-ttu-id="c98e2-118">Dar suporte à criação de usuários e/ou grupos, de acordo com a seção 3.3 do protocolo SCIM.</span><span class="sxs-lookup"><span data-stu-id="c98e2-118">Supports creating users and/or groups, as per section 3.3 of the SCIM protocol.</span></span>  
* <span data-ttu-id="c98e2-119">Dar suporte à modificação de usuários e/ou grupos com solicitações de patch, de acordo com a seção 3.5.2 do protocolo SCIM.</span><span class="sxs-lookup"><span data-stu-id="c98e2-119">Supports modifying users and/or groups with patch requests as per section 3.5.2 of the SCIM protocol.</span></span>  
* <span data-ttu-id="c98e2-120">Dar suporte à recuperação de um recurso conhecido, de acordo com a seção 3.4.1 do protocolo SCIM.</span><span class="sxs-lookup"><span data-stu-id="c98e2-120">Supports retrieving a known resource as per section 3.4.1 of the SCIM protocol.</span></span>  
* <span data-ttu-id="c98e2-121">Dar suporte a consultas de usuários e/ou grupos, de acordo com a seção 3.4.2 do protocolo SCIM.</span><span class="sxs-lookup"><span data-stu-id="c98e2-121">Supports querying users and/or groups, as per section 3.4.2 of the SCIM protocol.</span></span>  <span data-ttu-id="c98e2-122">Por padrão, os usuários são consultados por externalId e os grupos são consultados por displayName.</span><span class="sxs-lookup"><span data-stu-id="c98e2-122">By default, users are queried by externalId and groups are queried by displayName.</span></span>  
* <span data-ttu-id="c98e2-123">Dar suporte a consultas de usuário por ID e pelo gerenciador, de acordo com a seção 3.4.2 do protocolo SCIM.</span><span class="sxs-lookup"><span data-stu-id="c98e2-123">Supports querying user by ID and by manager as per section 3.4.2 of the SCIM protocol.</span></span>  
* <span data-ttu-id="c98e2-124">Dar suporte a consultas de grupos por ID e por membro, de acordo com a seção 3.4.2 do protocolo SCIM.</span><span class="sxs-lookup"><span data-stu-id="c98e2-124">Supports querying groups by ID and by member as per section 3.4.2 of the SCIM protocol.</span></span>  
* <span data-ttu-id="c98e2-125">Aceitar tokens de portador OAuth para autorização, de acordo com a seção 2.1 do protocolo SCIM.</span><span class="sxs-lookup"><span data-stu-id="c98e2-125">Accepts OAuth bearer tokens for authorization as per section 2.1 of the SCIM protocol.</span></span>

<span data-ttu-id="c98e2-126">Verifique com o seu provedor de aplicativo ou na documentação do seu provedor de aplicativo as declarações de compatibilidade com esses requisitos.</span><span class="sxs-lookup"><span data-stu-id="c98e2-126">Check with your application provider, or your application provider's documentation for statements of compatibility with these requirements.</span></span>

### <a name="getting-started"></a><span data-ttu-id="c98e2-127">Introdução</span><span class="sxs-lookup"><span data-stu-id="c98e2-127">Getting started</span></span>
<span data-ttu-id="c98e2-128">Os aplicativos que dão suporte ao perfil SCIM descrito neste artigo podem ser conectados ao Azure Active Directory usando o recurso de "aplicativo não galeria" na galeria de aplicativos do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c98e2-128">Applications that support the SCIM profile described in this article can be connected to Azure Active Directory using the "non-gallery application" feature in the Azure AD application gallery.</span></span> <span data-ttu-id="c98e2-129">Uma vez conectado, o Azure AD executa um processo de sincronização a cada 20 minutos, em que ele consulta o ponto de extremidade SCIM do aplicativo para os usuários e grupos atribuídos e os cria ou modifica de acordo com os detalhes da atribuição.</span><span class="sxs-lookup"><span data-stu-id="c98e2-129">Once connected, Azure AD runs a synchronization process every 20 minutes where it queries the application's SCIM endpoint for assigned users and groups, and creates or modifies them according to the assignment details.</span></span>

<span data-ttu-id="c98e2-130">**Para conectar um aplicativo que dê suporte a SCIM:**</span><span class="sxs-lookup"><span data-stu-id="c98e2-130">**To connect an application that supports SCIM:**</span></span>

1. <span data-ttu-id="c98e2-131">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c98e2-131">Sign in to [the Azure portal](https://portal.azure.com).</span></span> 
2. <span data-ttu-id="c98e2-132">Navegue até **Azure Active Directory > Aplicativos empresariais e selecione **Novo aplicativo > Todos > Aplicativo inexistente na galeria**.</span><span class="sxs-lookup"><span data-stu-id="c98e2-132">Browse to **Azure Active Directory > Enterprise Applications, and select **New application > All > Non-gallery application**.</span></span>
3. <span data-ttu-id="c98e2-133">Insira um nome para seu aplicativo e clique no ícone **Adicionar** para criar um objeto de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c98e2-133">Enter a name for your application, and click **Add** icon to create an app object.</span></span>
    
  <span data-ttu-id="c98e2-134">![][1]
  *Figura 2: Galeria de aplicativos do Azure AD*</span><span class="sxs-lookup"><span data-stu-id="c98e2-134">![][1]
*Figure 2: Azure AD application gallery*</span></span>
    
4. <span data-ttu-id="c98e2-135">Na tela de resultados, selecione a guia **Provisionamento** na coluna esquerda.</span><span class="sxs-lookup"><span data-stu-id="c98e2-135">In the resulting screen, select the **Provisioning** tab in the left column.</span></span>
5. <span data-ttu-id="c98e2-136">No menu **Modo de Provisionamento**, selecione **Automático**.</span><span class="sxs-lookup"><span data-stu-id="c98e2-136">In the **Provisioning Mode** menu, select **Automatic**.</span></span>
    
  <span data-ttu-id="c98e2-137">![][2]
  *Figura 3: Configurar o provisionamento no Portal do Azure*</span><span class="sxs-lookup"><span data-stu-id="c98e2-137">![][2]
*Figure 3: Configuring provisioning in the Azure portal*</span></span>
    
6. <span data-ttu-id="c98e2-138">No campo **URL do locatário** , insira a URL do ponto de extremidade do SCIM do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c98e2-138">In the **Tenant URL** field, enter the URL of the application's SCIM endpoint.</span></span> <span data-ttu-id="c98e2-139">Exemplo: https://api.contoso.com/scim/v2/</span><span class="sxs-lookup"><span data-stu-id="c98e2-139">Example: https://api.contoso.com/scim/v2/</span></span>
7. <span data-ttu-id="c98e2-140">Se o ponto de extremidade SCIM exigir um token de portador OAuth de um emissor diferente do Azure AD, copie o token de portador OAuth necessário para o campo opcional **Token Secreto**.</span><span class="sxs-lookup"><span data-stu-id="c98e2-140">If the SCIM endpoint requires an OAuth bearer token from an issuer other than Azure AD, then copy the required OAuth bearer token into the optional **Secret Token** field.</span></span> <span data-ttu-id="c98e2-141">Se esse campo estiver em branco, o Azure AD incluiu um token de portador OAuth emitido do Azure AD com cada solicitação.</span><span class="sxs-lookup"><span data-stu-id="c98e2-141">If this field is left blank, then Azure AD included an OAuth bearer token issued from Azure AD with each request.</span></span> <span data-ttu-id="c98e2-142">Aplicativos que usam o Azure AD como provedor de identidade podem validar esse token emitido pelo Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c98e2-142">Apps that use Azure AD as an identity provider can validate this Azure AD -issued token.</span></span>
8. <span data-ttu-id="c98e2-143">Clique no botão **Testar conectividade** o Azure Active Directory tente se conectar ao ponto de extremidade do SCIM.</span><span class="sxs-lookup"><span data-stu-id="c98e2-143">Click the **Test Connection** button to have Azure Active Directory attempt to connect to the SCIM endpoint.</span></span> <span data-ttu-id="c98e2-144">Se as tentativas falharem, as informações de erro serão exibidas.</span><span class="sxs-lookup"><span data-stu-id="c98e2-144">If the attempts fail, error information is displayed.</span></span>  
9. <span data-ttu-id="c98e2-145">Se as tentativas de conexão ao aplicativo forem bem-sucedidas, clique em **Salvar** para salvar as credenciais de administrador.</span><span class="sxs-lookup"><span data-stu-id="c98e2-145">If the attempts to connect to the application succeed, then click **Save** to save the admin credentials.</span></span>
10. <span data-ttu-id="c98e2-146">Na seção **Mapeamento**, há dois conjuntos selecionáveis de mapeamentos de atributos: um para objetos de usuário e outro para objetos de grupo.</span><span class="sxs-lookup"><span data-stu-id="c98e2-146">In the **Mappings** section, there are two selectable sets of attribute mappings: one for user objects and one for group objects.</span></span> <span data-ttu-id="c98e2-147">Selecione cada um para revisar os atributos que são sincronizados do Azure Active Directory para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c98e2-147">Select each one to review the attributes that are synchronized from Azure Active Directory to your app.</span></span> <span data-ttu-id="c98e2-148">Os atributos selecionados como propriedades **Correspondentes** serão usados para fazer a correspondência entre os usuários e os grupos no seu aplicativo para operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="c98e2-148">The attributes selected as **Matching** properties are used to match the users and groups in your app for update operations.</span></span> <span data-ttu-id="c98e2-149">Selecione o botão Salvar para confirmar as alterações.</span><span class="sxs-lookup"><span data-stu-id="c98e2-149">Select the Save button to commit any changes.</span></span>

    >[!NOTE]
    ><span data-ttu-id="c98e2-150">Opcionalmente, você pode desabilitar a sincronização dos objetos de grupo desabilitando o mapeamento "grupos".</span><span class="sxs-lookup"><span data-stu-id="c98e2-150">You can optionally disable syncing of group objects by disabling the "groups" mapping.</span></span> 

11. <span data-ttu-id="c98e2-151">Em **Configurações**, o campo **Escopo** define quais usuários e/ou grupos são sincronizados.</span><span class="sxs-lookup"><span data-stu-id="c98e2-151">Under **Settings**, the **Scope** field defines which users and or groups are synchronized.</span></span> <span data-ttu-id="c98e2-152">Selecionar "Sincronizar apenas usuários e grupos atribuídos" (recomendado) sincroniza somente usuários e grupos atribuídos na guia **Usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="c98e2-152">Selecting "Sync only assigned users and groups" (recommended) will only sync users and groups assigned in the **Users and groups** tab.</span></span>
12. <span data-ttu-id="c98e2-153">Depois que a configuração estiver concluída, altere o **Status de provisionamento** para **Ligado**.</span><span class="sxs-lookup"><span data-stu-id="c98e2-153">Once your configuration is complete, change the **Provisioning Status** to **On**.</span></span>
13. <span data-ttu-id="c98e2-154">Clique em **Salvar** para iniciar o serviço de provisionamento do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c98e2-154">Click **Save** to start the Azure AD provisioning service.</span></span> 
14. <span data-ttu-id="c98e2-155">Caso esteja sincronizando apenas usuários e grupos atribuídos (recomendado), certifique-se de selecionar a guia **Usuários e grupos** e designar os usuários e/ou grupos que você deseja sincronizar.</span><span class="sxs-lookup"><span data-stu-id="c98e2-155">If syncing only assigned users and groups (recommended), be sure to select the **Users and groups** tab and assign the users and/or groups you wish to sync.</span></span>

<span data-ttu-id="c98e2-156">Depois de iniciada a sincronização inicial, você pode usar a guia **Logs de auditoria** para monitorar o progresso, que mostra todas as ações executadas pelo serviço de provisionamento em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c98e2-156">Once the initial synchronization has started, you can use the **Audit logs** tab to monitor progress, which shows all actions performed by the provisioning service on your app.</span></span> <span data-ttu-id="c98e2-157">Para obter mais informações sobre como ler os logs de provisionamento do Azure AD, consulte [Relatando o provisionamento automático de conta de usuário](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="c98e2-157">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

>[!NOTE]
><span data-ttu-id="c98e2-158">Observe que a sincronização inicial levará mais tempo do que as sincronizações subsequentes, que ocorrem aproximadamente a cada 20 minutos, desde que o serviço esteja em execução.</span><span class="sxs-lookup"><span data-stu-id="c98e2-158">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> 


## <a name="building-your-own-provisioning-solution-for-any-application"></a><span data-ttu-id="c98e2-159">Criando sua própria solução de provisionamento para qualquer aplicativo</span><span class="sxs-lookup"><span data-stu-id="c98e2-159">Building your own provisioning solution for any application</span></span>
<span data-ttu-id="c98e2-160">Ao criar um serviço Web SCIM que interaja com o Active Directory do Azure, você poderá habilitar o logon único e o provisionamento de usuário automático para praticamente qualquer aplicativo que forneça uma API de provisionamento de usuário SOAP ou REST.</span><span class="sxs-lookup"><span data-stu-id="c98e2-160">By creating a SCIM web service that interfaces with Azure Active Directory, you can enable single sign-on and automatic user provisioning for virtually any application that provides a REST or SOAP user provisioning API.</span></span>

<span data-ttu-id="c98e2-161">Veja como ele funciona:</span><span class="sxs-lookup"><span data-stu-id="c98e2-161">Here’s how it works:</span></span>

1. <span data-ttu-id="c98e2-162">O AD do Azure fornece uma biblioteca CLI denominada [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/).</span><span class="sxs-lookup"><span data-stu-id="c98e2-162">Azure AD provides a common language infrastructure library named [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/).</span></span> <span data-ttu-id="c98e2-163">Os desenvolvedores e integradores de sistema podem usar essa biblioteca para criar e implantar um ponto de extremidade de serviço Web baseado em SCIM capaz de conectar o AD do Azure ao repositório de identidades de qualquer aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c98e2-163">System integrators and developers can use this library to create and deploy a SCIM-based web service endpoint capable of connecting Azure AD to any application’s identity store.</span></span>
2. <span data-ttu-id="c98e2-164">Os mapeamentos são implementados no serviço Web para mapear o esquema de usuário padronizado para o esquema de usuário e o protocolo exigido pelo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c98e2-164">Mappings are implemented in the web service to map the standardized user schema to the user schema and protocol required by the application.</span></span>
3. <span data-ttu-id="c98e2-165">A URL do ponto de extremidade é registrada no AD do Azure como parte de um aplicativo personalizado na galeria de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="c98e2-165">The endpoint URL is registered in Azure AD as part of a custom application in the application gallery.</span></span>
4. <span data-ttu-id="c98e2-166">Os usuários e grupos são atribuídos a esse aplicativo no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c98e2-166">Users and groups are assigned to this application in Azure AD.</span></span> <span data-ttu-id="c98e2-167">Na atribuição, eles são colocados em uma fila para serem sincronizados com o aplicativo de destino.</span><span class="sxs-lookup"><span data-stu-id="c98e2-167">Upon assignment, they are put into a queue to be synchronized to the target application.</span></span> <span data-ttu-id="c98e2-168">O processo de sincronização que trata a fila é executado a cada 20 minutos.</span><span class="sxs-lookup"><span data-stu-id="c98e2-168">The synchronization process handling the queue runs every 20 minutes.</span></span>

### <a name="code-samples"></a><span data-ttu-id="c98e2-169">Exemplos de código</span><span class="sxs-lookup"><span data-stu-id="c98e2-169">Code Samples</span></span>
<span data-ttu-id="c98e2-170">Para facilitar esse processo, será fornecido um conjunto de [exemplos de código](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) que cria um ponto de extremidade de serviço Web SCIM e demonstra o provisionamento automático.</span><span class="sxs-lookup"><span data-stu-id="c98e2-170">To make this process easier, a set of [code samples](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) are provided that create a SCIM web service endpoint and demonstrate automatic provisioning.</span></span> <span data-ttu-id="c98e2-171">Um dos exemplos é de um provedor que mantém um arquivo com linhas de valores separados por vírgula representando usuários e grupos.</span><span class="sxs-lookup"><span data-stu-id="c98e2-171">One sample is of a provider that maintains a file with rows of comma-separated values representing users and groups.</span></span>  <span data-ttu-id="c98e2-172">O outro é de um provedor que opera no serviço de Gerenciamento de Acesso e Identidade do Amazon Web Services.</span><span class="sxs-lookup"><span data-stu-id="c98e2-172">The other is of a provider that operates on the Amazon Web Services Identity and Access Management service.</span></span>  

<span data-ttu-id="c98e2-173">**Pré-requisitos**</span><span class="sxs-lookup"><span data-stu-id="c98e2-173">**Prerequisites**</span></span>

* <span data-ttu-id="c98e2-174">Visual Studio 2013 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="c98e2-174">Visual Studio 2013 or later</span></span>
* [<span data-ttu-id="c98e2-175">SDK do Azure para .NET</span><span class="sxs-lookup"><span data-stu-id="c98e2-175">Azure SDK for .NET</span></span>](https://azure.microsoft.com/downloads/)
* <span data-ttu-id="c98e2-176">Computador com Windows que ofereça suporte à estrutura ASP.NET 4.5 a ser usado como o ponto de extremidade SCIM.</span><span class="sxs-lookup"><span data-stu-id="c98e2-176">Windows machine that supports the ASP.NET framework 4.5 to be used as the SCIM endpoint.</span></span> <span data-ttu-id="c98e2-177">Esse computador deve poder ser acessado da nuvem</span><span class="sxs-lookup"><span data-stu-id="c98e2-177">This machine must be accessible from the cloud</span></span>
* [<span data-ttu-id="c98e2-178">Uma assinatura do Azure com uma versão de avaliação ou licenciada do Azure AD Premium</span><span class="sxs-lookup"><span data-stu-id="c98e2-178">An Azure subscription with a trial or licensed version of Azure AD Premium</span></span>](https://azure.microsoft.com/services/active-directory/)
* <span data-ttu-id="c98e2-179">O exemplo do Amazon AWS requer bibliotecas do [Kit de Ferramentas do AWS para Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html).</span><span class="sxs-lookup"><span data-stu-id="c98e2-179">The Amazon AWS sample requires libraries from the [AWS Toolkit for Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html).</span></span> <span data-ttu-id="c98e2-180">Para obter mais informações, consulte o arquivo LEIAME incluído no exemplo.</span><span class="sxs-lookup"><span data-stu-id="c98e2-180">For more information, see the README file included with the sample.</span></span>

### <a name="getting-started"></a><span data-ttu-id="c98e2-181">Introdução</span><span class="sxs-lookup"><span data-stu-id="c98e2-181">Getting Started</span></span>
<span data-ttu-id="c98e2-182">A maneira mais fácil de implementar um ponto de extremidade SCIM que possa aceitar solicitações de provisionamento do AD do Azure é criando e implantando o exemplo de código que gera os usuários provisionados em um arquivo CSV (valores separados por vírgula).</span><span class="sxs-lookup"><span data-stu-id="c98e2-182">The easiest way to implement a SCIM endpoint that can accept provisioning requests from Azure AD is to build and deploy the code sample that outputs the provisioned users to a comma-separated value (CSV) file.</span></span>

<span data-ttu-id="c98e2-183">**Para criar um exemplo de ponto de extremidade SCIM:**</span><span class="sxs-lookup"><span data-stu-id="c98e2-183">**To create a sample SCIM endpoint:**</span></span>

1. <span data-ttu-id="c98e2-184">Baixe o pacote de exemplo de códigos de [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)</span><span class="sxs-lookup"><span data-stu-id="c98e2-184">Download the code sample package at [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)</span></span>
2. <span data-ttu-id="c98e2-185">Descompacte o pacote e coloque-o no seu computador com Windows em um local como C:\AzureAD-BYOA-Provisioning-Samples\.</span><span class="sxs-lookup"><span data-stu-id="c98e2-185">Unzip the package and place it on your Windows machine at a location such as C:\AzureAD-BYOA-Provisioning-Samples\.</span></span>
3. <span data-ttu-id="c98e2-186">Nessa pasta, inicie a solução FileProvisioningAgent no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c98e2-186">In this folder, launch the FileProvisioningAgent solution in Visual Studio.</span></span>
4. <span data-ttu-id="c98e2-187">Selecione **Ferramentas > Gerenciador de Pacotes de Biblioteca > Console do Gerenciador de Pacotes** e execute os seguintes comandos para o projeto FileProvisioningAgent resolver as referências de solução:</span><span class="sxs-lookup"><span data-stu-id="c98e2-187">Select **Tools > Library Package Manager > Package Manager Console**, and execute the following commands for the FileProvisioningAgent project to resolve the solution references:</span></span>
  ```` 
   Install-Package Microsoft.SystemForCrossDomainIdentityManagement
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   Install-Package Microsoft.Owin.Diagnostics
   Install-Package Microsoft.Owin.Host.SystemWeb
  ````
5. <span data-ttu-id="c98e2-188">Compile o projeto FileProvisioningAgent.</span><span class="sxs-lookup"><span data-stu-id="c98e2-188">Build the FileProvisioningAgent project.</span></span>
6. <span data-ttu-id="c98e2-189">Inicie o aplicativo Prompt de Comando no Windows (como administrador) e use o comando **cd** para alterar o diretório para a sua pasta **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug**.</span><span class="sxs-lookup"><span data-stu-id="c98e2-189">Launch the Command Prompt application in Windows (as an Administrator), and use the **cd** command to change the directory to your **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug** folder.</span></span>
7. <span data-ttu-id="c98e2-190">Execute o seguinte comando, substituindo <ip-address> pelo endereço IP ou pelo nome de domínio do computador com Windows:</span><span class="sxs-lookup"><span data-stu-id="c98e2-190">Run the following command, replacing <ip-address> with the IP address or domain name of the Windows machine:</span></span>
  ````   
   FileAgnt.exe http://<ip-address>:9000 TargetFile.csv
  ````
8. <span data-ttu-id="c98e2-191">No Windows, em **Configurações do Windows > Configurações de Rede e Internet**, selecione o **Firewall do Windows > Configurações Avançadas** e crie uma **Regra de Entrada** que permita acesso de entrada na porta 9000.</span><span class="sxs-lookup"><span data-stu-id="c98e2-191">In Windows under **Windows Settings > Network & Internet Settings**, select the **Windows Firewall > Advanced Settings**, and create an **Inbound Rule** that allows inbound access to port 9000.</span></span>
9. <span data-ttu-id="c98e2-192">Se o computador com Windows estiver atrás de um roteador, precisará ser configurado para executar a Network Access Translation entre sua porta 9000 exposta à Internet e a porta 9000 no computador com Windows.</span><span class="sxs-lookup"><span data-stu-id="c98e2-192">If the Windows machine is behind a router, the router needs to be configured to perform Network Access Translation between its port 9000 that is exposed to the internet, and port 9000 on the Windows machine.</span></span> <span data-ttu-id="c98e2-193">Isso é necessário para que o AD do Azure possa acessar esse ponto de extremidade na nuvem.</span><span class="sxs-lookup"><span data-stu-id="c98e2-193">This is required for Azure AD to be able to access this endpoint in the cloud.</span></span>

<span data-ttu-id="c98e2-194">**Para registrar o exemplo de ponto de extremidade SCIM no AD do Azure:**</span><span class="sxs-lookup"><span data-stu-id="c98e2-194">**To register the sample SCIM endpoint in Azure AD:**</span></span>

1. <span data-ttu-id="c98e2-195">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c98e2-195">Sign in to [the Azure portal](https://portal.azure.com).</span></span> 
2. <span data-ttu-id="c98e2-196">Navegue até **Azure Active Directory > Aplicativos empresariais e selecione **Novo aplicativo > Todos > Aplicativo inexistente na galeria**.</span><span class="sxs-lookup"><span data-stu-id="c98e2-196">Browse to **Azure Active Directory > Enterprise Applications, and select **New application > All > Non-gallery application**.</span></span>
3. <span data-ttu-id="c98e2-197">Insira um nome para seu aplicativo e clique no ícone **Adicionar** para criar um objeto de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c98e2-197">Enter a name for your application, and click **Add** icon to create an app object.</span></span> <span data-ttu-id="c98e2-198">O objeto de aplicativo criado destina-se a representar o aplicativo de destino para o qual você estará provisionando e implementando o logon único, e não apenas o ponto de extremidade SCIM.</span><span class="sxs-lookup"><span data-stu-id="c98e2-198">The application object created is intended to represent the target app you would be provisioning to and implementing single sign-on for, and not just the SCIM endpoint.</span></span>
4. <span data-ttu-id="c98e2-199">Na tela de resultados, selecione a guia **Provisionamento** na coluna esquerda.</span><span class="sxs-lookup"><span data-stu-id="c98e2-199">In the resulting screen, select the **Provisioning** tab in the left column.</span></span>
5. <span data-ttu-id="c98e2-200">No menu **Modo de Provisionamento**, selecione **Automático**.</span><span class="sxs-lookup"><span data-stu-id="c98e2-200">In the **Provisioning Mode** menu, select **Automatic**.</span></span>
    
  <span data-ttu-id="c98e2-201">![][2]
  *Figura 4: Configurar o provisionamento no Portal do Azure*</span><span class="sxs-lookup"><span data-stu-id="c98e2-201">![][2]
*Figure 4: Configuring provisioning in the Azure portal*</span></span>
    
6. <span data-ttu-id="c98e2-202">No campo **URL do locatário**, insira a URL exposta à Internet e a porta do seu ponto de extremidade SCIM.</span><span class="sxs-lookup"><span data-stu-id="c98e2-202">In the **Tenant URL** field, enter the internet-exposed URL and port of your SCIM endpoint.</span></span> <span data-ttu-id="c98e2-203">Isso seria algo como http://testmachine.contoso.com:9000 or http://<ip-address>:9000/, em que <ip-address> é o endereço IP exposto na Internet.</span><span class="sxs-lookup"><span data-stu-id="c98e2-203">This would be something like http://testmachine.contoso.com:9000 or http://<ip-address>:9000/, where <ip-address> is the internet exposed IP address.</span></span>  
7. <span data-ttu-id="c98e2-204">Se o ponto de extremidade SCIM exigir um token de portador OAuth de um emissor diferente do Azure AD, copie o token de portador OAuth necessário para o campo opcional **Token Secreto**.</span><span class="sxs-lookup"><span data-stu-id="c98e2-204">If the SCIM endpoint requires an OAuth bearer token from an issuer other than Azure AD, then copy the required OAuth bearer token into the optional **Secret Token** field.</span></span> <span data-ttu-id="c98e2-205">Se esse campo for deixado em branco, o Azure AD incluirá um token de portador OAuth emitido do Azure AD com cada solicitação.</span><span class="sxs-lookup"><span data-stu-id="c98e2-205">If this field is left blank, then Azure AD will include an OAuth bearer token issued from Azure AD with each request.</span></span> <span data-ttu-id="c98e2-206">Aplicativos que usam o Azure AD como provedor de identidade podem validar esse token emitido pelo Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c98e2-206">Apps that use Azure AD as an identity provider can validate this Azure AD -issued token.</span></span>
8. <span data-ttu-id="c98e2-207">Clique no botão **Testar conectividade** o Azure Active Directory tente se conectar ao ponto de extremidade do SCIM.</span><span class="sxs-lookup"><span data-stu-id="c98e2-207">Click the **Test Connection** button to have Azure Active Directory attempt to connect to the SCIM endpoint.</span></span> <span data-ttu-id="c98e2-208">Se as tentativas falharem, as informações de erro serão exibidas.</span><span class="sxs-lookup"><span data-stu-id="c98e2-208">If the attempts fail, error information is displayed.</span></span>  
9. <span data-ttu-id="c98e2-209">Se as tentativas de conexão ao aplicativo forem bem-sucedidas, clique em **Salvar** para salvar as credenciais de administrador.</span><span class="sxs-lookup"><span data-stu-id="c98e2-209">If the attempts to connect to the application succeed, then click **Save** to save the admin credentials.</span></span>
10. <span data-ttu-id="c98e2-210">Na seção **Mapeamento**, há dois conjuntos selecionáveis de mapeamentos de atributos: um para objetos de usuário e outro para objetos de grupo.</span><span class="sxs-lookup"><span data-stu-id="c98e2-210">In the **Mappings** section, there are two selectable sets of attribute mappings: one for user objects and one for group objects.</span></span> <span data-ttu-id="c98e2-211">Selecione cada um para revisar os atributos que são sincronizados do Azure Active Directory para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c98e2-211">Select each one to review the attributes that are synchronized from Azure Active Directory to your app.</span></span> <span data-ttu-id="c98e2-212">Os atributos selecionados como propriedades **Correspondentes** serão usados para fazer a correspondência entre os usuários e os grupos no seu aplicativo para operações de atualização.</span><span class="sxs-lookup"><span data-stu-id="c98e2-212">The attributes selected as **Matching** properties are used to match the users and groups in your app for update operations.</span></span> <span data-ttu-id="c98e2-213">Selecione o botão Salvar para confirmar as alterações.</span><span class="sxs-lookup"><span data-stu-id="c98e2-213">Select the Save button to commit any changes.</span></span>
11. <span data-ttu-id="c98e2-214">Em **Configurações**, o campo **Escopo** define quais usuários e/ou grupos são sincronizados.</span><span class="sxs-lookup"><span data-stu-id="c98e2-214">Under **Settings**, the **Scope** field defines which users and or groups are synchronized.</span></span> <span data-ttu-id="c98e2-215">Selecionar "Sincronizar apenas usuários e grupos atribuídos" (recomendado) sincroniza somente usuários e grupos atribuídos na guia **Usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="c98e2-215">Selecting "Sync only assigned users and groups" (recommended) will only sync users and groups assigned in the **Users and groups** tab.</span></span>
12. <span data-ttu-id="c98e2-216">Depois que a configuração estiver concluída, altere o **Status de provisionamento** para **Ligado**.</span><span class="sxs-lookup"><span data-stu-id="c98e2-216">Once your configuration is complete, change the **Provisioning Status** to **On**.</span></span>
13. <span data-ttu-id="c98e2-217">Clique em **Salvar** para iniciar o serviço de provisionamento do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c98e2-217">Click **Save** to start the Azure AD provisioning service.</span></span> 
14. <span data-ttu-id="c98e2-218">Caso esteja sincronizando apenas usuários e grupos atribuídos (recomendado), certifique-se de selecionar a guia **Usuários e grupos** e designar os usuários e/ou grupos que você deseja sincronizar.</span><span class="sxs-lookup"><span data-stu-id="c98e2-218">If syncing only assigned users and groups (recommended), be sure to select the **Users and groups** tab and assign the users and/or groups you wish to sync.</span></span>

<span data-ttu-id="c98e2-219">Depois de iniciada a sincronização inicial, você pode usar a guia **Logs de auditoria** para monitorar o progresso, que mostra todas as ações executadas pelo serviço de provisionamento em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c98e2-219">Once the initial synchronization has started, you can use the **Audit logs** tab to monitor progress, which shows all actions performed by the provisioning service on your app.</span></span> <span data-ttu-id="c98e2-220">Para obter mais informações sobre como ler os logs de provisionamento do Azure AD, consulte [Relatando o provisionamento automático de conta de usuário](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="c98e2-220">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

<span data-ttu-id="c98e2-221">A etapa final da verificação do exemplo é abrir o arquivo TargetFile.csv da pasta \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug no seu computador com Windows.</span><span class="sxs-lookup"><span data-stu-id="c98e2-221">The final step in verifying the sample is to open the TargetFile.csv file in the \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug folder on your Windows machine.</span></span> <span data-ttu-id="c98e2-222">Depois que o processo de provisionamento é executado, esse arquivo mostra os detalhes de todos os usuários e grupos provisionados e atribuídos.</span><span class="sxs-lookup"><span data-stu-id="c98e2-222">Once the provisioning process is run, this file shows the details of all assigned and provisioned users and groups.</span></span>

### <a name="development-libraries"></a><span data-ttu-id="c98e2-223">Bibliotecas de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="c98e2-223">Development libraries</span></span>
<span data-ttu-id="c98e2-224">Para desenvolver seu próprio serviço Web em conformidade com a especificação do SCIM, em primeiro lugar, familiarize-se com as seguintes bibliotecas fornecidas pela Microsoft, que ajudam a acelerar o processo de desenvolvimento:</span><span class="sxs-lookup"><span data-stu-id="c98e2-224">To develop your own web service that conforms to the SCIM specification, first familiarize yourself with the following libraries provided by Microsoft to help accelerate the development process:</span></span> 

1. <span data-ttu-id="c98e2-225">As bibliotecas Common Language Infrastructure (CLI) são oferecidas para uso com linguagens que se baseiam na infraestrutura em questão, como C#.</span><span class="sxs-lookup"><span data-stu-id="c98e2-225">Common Language Infrastructure (CLI) libraries are offered for use with languages based on that infrastructure, such as C#.</span></span> <span data-ttu-id="c98e2-226">Uma dessas bibliotecas, [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), declara uma interface, Microsoft.SystemForCrossDomainIdentityManagement.IProvider, mostrada na ilustração a seguir: Um desenvolvedor que usa as bibliotecas implementa essa interface com uma classe que pode ser referenciada, de modo genérico, como provedor.</span><span class="sxs-lookup"><span data-stu-id="c98e2-226">One of those libraries, [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), declares an interface, Microsoft.SystemForCrossDomainIdentityManagement.IProvider, shown in the following illustration:  A developer using the libraries would implement that interface with a class that may be referred to, generically, as a provider.</span></span> <span data-ttu-id="c98e2-227">As bibliotecas permitem que o desenvolvedor implante um serviço Web que esteja em conformidade com a especificação de SCIM.</span><span class="sxs-lookup"><span data-stu-id="c98e2-227">The libraries enable the developer to deploy a web service that conforms to the SCIM specification.</span></span> <span data-ttu-id="c98e2-228">O serviço Web pode ser hospedado em Serviços de Informações da Internet ou pode ser qualquer assembly executável de Common Language Infrastructure.</span><span class="sxs-lookup"><span data-stu-id="c98e2-228">The web service can be either hosted within Internet Information Services, or any executable Common Language Infrastructure assembly.</span></span> <span data-ttu-id="c98e2-229">A solicitação é convertida em chamadas aos métodos do provedor, que podem ser programadas pelo desenvolvedor para operar em algum repositório de identidades.</span><span class="sxs-lookup"><span data-stu-id="c98e2-229">Request is translated into calls to the provider’s methods, which would be programmed by the developer to operate on some identity store.</span></span>
  
  ![][3]
  
2. <span data-ttu-id="c98e2-230">[Manipuladores de ExpressRoute](http://expressjs.com/guide/routing.html) estão disponíveis para análise de objetos de solicitação node.js que representam chamadas (como definido pela especificação do SCIM) feitas para um serviço Web node.js.</span><span class="sxs-lookup"><span data-stu-id="c98e2-230">[Express route handlers](http://expressjs.com/guide/routing.html) are available for parsing node.js request objects representing calls (as defined by the SCIM specification), made to a node.js web service.</span></span>   

### <a name="building-a-custom-scim-endpoint"></a><span data-ttu-id="c98e2-231">Criando um ponto de extremidade SCIM personalizado</span><span class="sxs-lookup"><span data-stu-id="c98e2-231">Building a Custom SCIM Endpoint</span></span>
<span data-ttu-id="c98e2-232">Usando as bibliotecas CLI, os desenvolvedores podem hospedar seus serviços em qualquer assembly executável da Common Language Infrastructure ou nos Serviços de Informações da Internet.</span><span class="sxs-lookup"><span data-stu-id="c98e2-232">Using the CLI libraries, developers using those libraries can host their services within any executable Common Language Infrastructure assembly, or within Internet Information Services.</span></span> <span data-ttu-id="c98e2-233">Veja um exemplo de código para hospedar um serviço em um assembly executável no endereço http://localhost:9000:</span><span class="sxs-lookup"><span data-stu-id="c98e2-233">Here is sample code for hosting a service within an executable assembly, at the address http://localhost:9000:</span></span> 

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

<span data-ttu-id="c98e2-234">Esse serviço deve ter um endereço HTTP e um certificado de autenticação de servidor do qual a autoridade de certificação raiz é uma destas:</span><span class="sxs-lookup"><span data-stu-id="c98e2-234">This service must have an HTTP address and server authentication certificate of which the root certification authority is one of the following:</span></span> 

* <span data-ttu-id="c98e2-235">CNNIC</span><span class="sxs-lookup"><span data-stu-id="c98e2-235">CNNIC</span></span>
* <span data-ttu-id="c98e2-236">Comodo</span><span class="sxs-lookup"><span data-stu-id="c98e2-236">Comodo</span></span>
* <span data-ttu-id="c98e2-237">CyberTrust</span><span class="sxs-lookup"><span data-stu-id="c98e2-237">CyberTrust</span></span>
* <span data-ttu-id="c98e2-238">DigiCert</span><span class="sxs-lookup"><span data-stu-id="c98e2-238">DigiCert</span></span>
* <span data-ttu-id="c98e2-239">GeoTrust</span><span class="sxs-lookup"><span data-stu-id="c98e2-239">GeoTrust</span></span>
* <span data-ttu-id="c98e2-240">GlobalSign</span><span class="sxs-lookup"><span data-stu-id="c98e2-240">GlobalSign</span></span>
* <span data-ttu-id="c98e2-241">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="c98e2-241">Go Daddy</span></span>
* <span data-ttu-id="c98e2-242">Verisign</span><span class="sxs-lookup"><span data-stu-id="c98e2-242">Verisign</span></span>
* <span data-ttu-id="c98e2-243">WoSign</span><span class="sxs-lookup"><span data-stu-id="c98e2-243">WoSign</span></span>

<span data-ttu-id="c98e2-244">Um certificado de autenticação de servidor pode ser associado a uma porta em um host do Windows usando o utilitário de shell de rede:</span><span class="sxs-lookup"><span data-stu-id="c98e2-244">A server authentication certificate can be bound to a port on a Windows host using the network shell utility:</span></span> 

    netsh http add sslcert ipport=0.0.0.0:443 certhash=0000000000003ed9cd0c315bbb6dc1c08da5e6 appid={00112233-4455-6677-8899-AABBCCDDEEFF}  

<span data-ttu-id="c98e2-245">Aqui, o valor fornecido para o argumento certhash é a impressão digital do certificado, enquanto o valor fornecido para o argumento appid é um identificador global exclusivo arbitrário.</span><span class="sxs-lookup"><span data-stu-id="c98e2-245">Here, the value provided for the certhash argument is the thumbprint of the certificate, while the value provided for the appid argument is an arbitrary globally unique identifier.</span></span>  

<span data-ttu-id="c98e2-246">Para hospedar o serviço nos Serviços de Informações da Internet, um desenvolvedor cria um assembly de biblioteca de códigos da CLA com uma classe chamada Startup no namespace padrão do assembly.</span><span class="sxs-lookup"><span data-stu-id="c98e2-246">To host the service within Internet Information Services, a developer would build a CLA code library assembly with a class named Startup in the default namespace of the assembly.</span></span>  <span data-ttu-id="c98e2-247">Veja um exemplo dessa classe:</span><span class="sxs-lookup"><span data-stu-id="c98e2-247">Here is a sample of such a class:</span></span> 

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

### <a name="handling-endpoint-authentication"></a><span data-ttu-id="c98e2-248">Manipulando a autenticação do ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="c98e2-248">Handling endpoint authentication</span></span>
<span data-ttu-id="c98e2-249">As solicitações do Active Directory do Azure incluem um token de portador do OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="c98e2-249">Requests from Azure Active Directory include an OAuth 2.0 bearer token.</span></span>   <span data-ttu-id="c98e2-250">Qualquer serviço que recebe a solicitação deve autenticar o emissor como sendo o Azure Active Directory em nome do locatário esperado do Azure Active Directory, para acesso ao serviço Web Graph do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c98e2-250">Any service receiving the request should authenticate the issuer as being Azure Active Directory on behalf of the expected Azure Active Directory tenant, for access to the Azure Active Directory Graph web service.</span></span>  <span data-ttu-id="c98e2-251">No token, o emissor é identificado por uma declaração de iss, como "iss": "https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/".</span><span class="sxs-lookup"><span data-stu-id="c98e2-251">In the token, the issuer is identified by an iss claim, like, "iss":"https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/".</span></span>  <span data-ttu-id="c98e2-252">Neste exemplo, o endereço base do valor da declaração, https://sts.windows.net, identifica o Azure Active Directory como o emissor, enquanto o segmento do endereço relativo, cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, é um identificador exclusivo do locatário do Azure Active Directory em nome do qual o token foi emitido.</span><span class="sxs-lookup"><span data-stu-id="c98e2-252">In this example, the base address of the claim value, https://sts.windows.net, identifies Azure Active Directory as the issuer, while the relative address segment, cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, is a unique identifier of the Azure Active Directory tenant on behalf of which the token was issued.</span></span>  <span data-ttu-id="c98e2-253">Se o token tiver sido emitido para acessar um serviço Web Graph do Azure Active Directory, o identificador desse serviço, 00000002-0000-0000-c000-000000000000, deverá estar no valor da declaração aud do token.</span><span class="sxs-lookup"><span data-stu-id="c98e2-253">If the token was issued for accessing the Azure Active Directory Graph web service, then the identifier of that service, 00000002-0000-0000-c000-000000000000, should be in the value of the token’s aud claim.</span></span>  

<span data-ttu-id="c98e2-254">Os desenvolvedores que usam as bibliotecas CLA fornecidas pela Microsoft para criação de um serviço SCIM podem autenticar solicitações do Azure Active Directory usando o pacote Microsoft.Owin.Security.ActiveDirectory seguindo estas etapas:</span><span class="sxs-lookup"><span data-stu-id="c98e2-254">Developers using the CLA libraries provided by Microsoft for building a SCIM service can authenticate requests from Azure Active Directory using the Microsoft.Owin.Security.ActiveDirectory package by following these steps:</span></span> 

1. <span data-ttu-id="c98e2-255">Em um provedor, implemente a propriedade Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior fazendo com que ela retorne um método a ser chamado sempre que o serviço é iniciado:</span><span class="sxs-lookup"><span data-stu-id="c98e2-255">In a provider, implement the Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior property by having it return a method to be called whenever the service is started:</span></span> 

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

2. <span data-ttu-id="c98e2-256">Adicione o código a seguir ao método para que as solicitações a qualquer um dos pontos de extremidade do serviço sejam autenticados como sendo um token emitido pelo Azure Active Directory em nome de um locatário especificado para acesso ao serviço Web Graph do Azure AD:</span><span class="sxs-lookup"><span data-stu-id="c98e2-256">Add the following code to that method to have any request to any of the service’s endpoints authenticated as bearing a token issued by Azure Active Directory on behalf of a specified tenant, for access to the Azure AD Graph web service:</span></span> 

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
        Tenant = "03F9FCBC-EA7B-46C2-8466-F81917F3C15E" // Substitute the appropriate tenant’s 
                                                      // identifier for this one.  
      };

      applicationBuilder.UseWindowsAzureActiveDirectoryBearerAuthentication(authenticationOptions);
    }
  ````


## <a name="user-and-group-schema"></a><span data-ttu-id="c98e2-257">Esquema de usuários e grupos</span><span class="sxs-lookup"><span data-stu-id="c98e2-257">User and group schema</span></span>
<span data-ttu-id="c98e2-258">O Azure Active Directory pode provisionar dois tipos de recurso aos serviços Web SCIM.</span><span class="sxs-lookup"><span data-stu-id="c98e2-258">Azure Active Directory can provision two types of resources to SCIM web services.</span></span>  <span data-ttu-id="c98e2-259">Esses tipos de recurso são usuários e grupos.</span><span class="sxs-lookup"><span data-stu-id="c98e2-259">Those types of resources are users and groups.</span></span>  

<span data-ttu-id="c98e2-260">Os recursos de usuário são identificados pelo identificador do esquema, urn:ietf:params:scim:schemas:extension:enterprise:2.0:User, que está incluído nesta especificação de protocolo: http://tools.ietf.org/html/draft-ietf-scim-core-schema.</span><span class="sxs-lookup"><span data-stu-id="c98e2-260">User resources are identified by the schema identifier, urn:ietf:params:scim:schemas:extension:enterprise:2.0:User, which is included in this protocol specification: http://tools.ietf.org/html/draft-ietf-scim-core-schema.</span></span>  <span data-ttu-id="c98e2-261">O mapeamento padrão dos atributos de usuários no Active Directory do Azure para os atributos dos recursos urn:ietf:params:scim:schemas:extension:enterprise:2.0:User é fornecido na tabela 1, abaixo.</span><span class="sxs-lookup"><span data-stu-id="c98e2-261">The default mapping of the attributes of users in Azure Active Directory to the attributes of urn:ietf:params:scim:schemas:extension:enterprise:2.0:User resources is provided in table 1, below.</span></span>  

<span data-ttu-id="c98e2-262">Os recursos de grupo são identificados pelo identificador do esquema, http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span><span class="sxs-lookup"><span data-stu-id="c98e2-262">Group resources are identified by the schema identifier, http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span></span>  <span data-ttu-id="c98e2-263">A tabela 2 abaixo mostra o mapeamento padrão de atributos de grupos no Azure Active Directory para os atributos de recursos de http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span><span class="sxs-lookup"><span data-stu-id="c98e2-263">Table 2, below, shows the default mapping of the attributes of groups in Azure Active Directory to the attributes of http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group resources.</span></span>  

### <a name="table-1-default-user-attribute-mapping"></a><span data-ttu-id="c98e2-264">Tabela 1: Mapeamento padrão de atributo do usuário</span><span class="sxs-lookup"><span data-stu-id="c98e2-264">Table 1: Default user attribute mapping</span></span>
| <span data-ttu-id="c98e2-265">Usuário do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="c98e2-265">Azure Active Directory user</span></span> | <span data-ttu-id="c98e2-266">urn:ietf:params:scim:schemas:extension:enterprise:2.0:User</span><span class="sxs-lookup"><span data-stu-id="c98e2-266">urn:ietf:params:scim:schemas:extension:enterprise:2.0:User</span></span> |
| --- | --- |
| <span data-ttu-id="c98e2-267">IsSoftDeleted</span><span class="sxs-lookup"><span data-stu-id="c98e2-267">IsSoftDeleted</span></span> |<span data-ttu-id="c98e2-268">ativo</span><span class="sxs-lookup"><span data-stu-id="c98e2-268">active</span></span> |
| <span data-ttu-id="c98e2-269">displayName</span><span class="sxs-lookup"><span data-stu-id="c98e2-269">displayName</span></span> |<span data-ttu-id="c98e2-270">displayName</span><span class="sxs-lookup"><span data-stu-id="c98e2-270">displayName</span></span> |
| <span data-ttu-id="c98e2-271">Facsimile-TelephoneNumber</span><span class="sxs-lookup"><span data-stu-id="c98e2-271">Facsimile-TelephoneNumber</span></span> |<span data-ttu-id="c98e2-272">phoneNumbers[type eq "fax"].value</span><span class="sxs-lookup"><span data-stu-id="c98e2-272">phoneNumbers[type eq "fax"].value</span></span> |
| <span data-ttu-id="c98e2-273">givenName</span><span class="sxs-lookup"><span data-stu-id="c98e2-273">givenName</span></span> |<span data-ttu-id="c98e2-274">name.givenName</span><span class="sxs-lookup"><span data-stu-id="c98e2-274">name.givenName</span></span> |
| <span data-ttu-id="c98e2-275">jobTitle</span><span class="sxs-lookup"><span data-stu-id="c98e2-275">jobTitle</span></span> |<span data-ttu-id="c98e2-276">título</span><span class="sxs-lookup"><span data-stu-id="c98e2-276">title</span></span> |
| <span data-ttu-id="c98e2-277">mail</span><span class="sxs-lookup"><span data-stu-id="c98e2-277">mail</span></span> |<span data-ttu-id="c98e2-278">emails[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="c98e2-278">emails[type eq "work"].value</span></span> |
| <span data-ttu-id="c98e2-279">mailNickname</span><span class="sxs-lookup"><span data-stu-id="c98e2-279">mailNickname</span></span> |<span data-ttu-id="c98e2-280">externalId</span><span class="sxs-lookup"><span data-stu-id="c98e2-280">externalId</span></span> |
| <span data-ttu-id="c98e2-281">manager</span><span class="sxs-lookup"><span data-stu-id="c98e2-281">manager</span></span> |<span data-ttu-id="c98e2-282">manager</span><span class="sxs-lookup"><span data-stu-id="c98e2-282">manager</span></span> |
| <span data-ttu-id="c98e2-283">Serviço Móvel</span><span class="sxs-lookup"><span data-stu-id="c98e2-283">mobile</span></span> |<span data-ttu-id="c98e2-284">phoneNumbers[type eq "mobile"].value</span><span class="sxs-lookup"><span data-stu-id="c98e2-284">phoneNumbers[type eq "mobile"].value</span></span> |
| <span data-ttu-id="c98e2-285">ID do objeto</span><span class="sxs-lookup"><span data-stu-id="c98e2-285">objectId</span></span> |<span data-ttu-id="c98e2-286">ID</span><span class="sxs-lookup"><span data-stu-id="c98e2-286">id</span></span> |
| <span data-ttu-id="c98e2-287">postalCode</span><span class="sxs-lookup"><span data-stu-id="c98e2-287">postalCode</span></span> |<span data-ttu-id="c98e2-288">addresses[type eq "work"].postalCode</span><span class="sxs-lookup"><span data-stu-id="c98e2-288">addresses[type eq "work"].postalCode</span></span> |
| <span data-ttu-id="c98e2-289">proxy-Addresses</span><span class="sxs-lookup"><span data-stu-id="c98e2-289">proxy-Addresses</span></span> |<span data-ttu-id="c98e2-290">emails[type eq "other"].Value</span><span class="sxs-lookup"><span data-stu-id="c98e2-290">emails[type eq "other"].Value</span></span> |
| <span data-ttu-id="c98e2-291">physical-Delivery-OfficeName</span><span class="sxs-lookup"><span data-stu-id="c98e2-291">physical-Delivery-OfficeName</span></span> |<span data-ttu-id="c98e2-292">addresses[type eq "other"].Formatted</span><span class="sxs-lookup"><span data-stu-id="c98e2-292">addresses[type eq "other"].Formatted</span></span> |
| <span data-ttu-id="c98e2-293">streetAddress</span><span class="sxs-lookup"><span data-stu-id="c98e2-293">streetAddress</span></span> |<span data-ttu-id="c98e2-294">addresses[type eq "work"].streetAddress</span><span class="sxs-lookup"><span data-stu-id="c98e2-294">addresses[type eq "work"].streetAddress</span></span> |
| <span data-ttu-id="c98e2-295">sobrenome</span><span class="sxs-lookup"><span data-stu-id="c98e2-295">surname</span></span> |<span data-ttu-id="c98e2-296">name.familyName</span><span class="sxs-lookup"><span data-stu-id="c98e2-296">name.familyName</span></span> |
| <span data-ttu-id="c98e2-297">telephone-Number</span><span class="sxs-lookup"><span data-stu-id="c98e2-297">telephone-Number</span></span> |<span data-ttu-id="c98e2-298">phoneNumbers[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="c98e2-298">phoneNumbers[type eq "work"].value</span></span> |
| <span data-ttu-id="c98e2-299">user-PrincipalName</span><span class="sxs-lookup"><span data-stu-id="c98e2-299">user-PrincipalName</span></span> |<span data-ttu-id="c98e2-300">userName</span><span class="sxs-lookup"><span data-stu-id="c98e2-300">userName</span></span> |

### <a name="table-2-default-group-attribute-mapping"></a><span data-ttu-id="c98e2-301">Tabela 2: Mapeamento padrão de atributo do grupo</span><span class="sxs-lookup"><span data-stu-id="c98e2-301">Table 2: Default group attribute mapping</span></span>
| <span data-ttu-id="c98e2-302">Grupo do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="c98e2-302">Azure Active Directory group</span></span> | <span data-ttu-id="c98e2-303">http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group</span><span class="sxs-lookup"><span data-stu-id="c98e2-303">http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group</span></span> |
| --- | --- |
| <span data-ttu-id="c98e2-304">displayName</span><span class="sxs-lookup"><span data-stu-id="c98e2-304">displayName</span></span> |<span data-ttu-id="c98e2-305">externalId</span><span class="sxs-lookup"><span data-stu-id="c98e2-305">externalId</span></span> |
| <span data-ttu-id="c98e2-306">mail</span><span class="sxs-lookup"><span data-stu-id="c98e2-306">mail</span></span> |<span data-ttu-id="c98e2-307">emails[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="c98e2-307">emails[type eq "work"].value</span></span> |
| <span data-ttu-id="c98e2-308">mailNickname</span><span class="sxs-lookup"><span data-stu-id="c98e2-308">mailNickname</span></span> |<span data-ttu-id="c98e2-309">displayName</span><span class="sxs-lookup"><span data-stu-id="c98e2-309">displayName</span></span> |
| <span data-ttu-id="c98e2-310">membros</span><span class="sxs-lookup"><span data-stu-id="c98e2-310">members</span></span> |<span data-ttu-id="c98e2-311">membros</span><span class="sxs-lookup"><span data-stu-id="c98e2-311">members</span></span> |
| <span data-ttu-id="c98e2-312">ID do objeto</span><span class="sxs-lookup"><span data-stu-id="c98e2-312">objectId</span></span> |<span data-ttu-id="c98e2-313">ID</span><span class="sxs-lookup"><span data-stu-id="c98e2-313">id</span></span> |
| <span data-ttu-id="c98e2-314">proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="c98e2-314">proxyAddresses</span></span> |<span data-ttu-id="c98e2-315">emails[type eq "other"].Value</span><span class="sxs-lookup"><span data-stu-id="c98e2-315">emails[type eq "other"].Value</span></span> |

## <a name="user-provisioning-and-de-provisioning"></a><span data-ttu-id="c98e2-316">Provisionamento e desprovisionamento de usuários</span><span class="sxs-lookup"><span data-stu-id="c98e2-316">User provisioning and de-provisioning</span></span>
<span data-ttu-id="c98e2-317">A seguinte ilustração mostra as mensagens que o Azure Active Directory envia a um serviço SCIM para gerenciar o ciclo de vida de um usuário em outro repositório de identidades.</span><span class="sxs-lookup"><span data-stu-id="c98e2-317">The following illustration shows the messages that Azure Active Directory sends to a SCIM service to manage the lifecycle of a user in another identity store.</span></span> <span data-ttu-id="c98e2-318">O diagrama também mostra como um serviço SCIM implementado usando as bibliotecas CLI fornecidas pela Microsoft para a criação de tais serviços converte as solicitações em chamadas para os métodos de um provedor.</span><span class="sxs-lookup"><span data-stu-id="c98e2-318">The diagram also shows how a SCIM service implemented using the CLI libraries provided by Microsoft for building such services translate those requests into calls to the methods of a provider.</span></span>  

<span data-ttu-id="c98e2-319">![][4]
*Figura 5: Sequência de provisionamento e desprovisionamento de usuário*</span><span class="sxs-lookup"><span data-stu-id="c98e2-319">![][4]
*Figure 5: User provisioning and de-provisioning sequence*</span></span>

1. <span data-ttu-id="c98e2-320">O Azure Active Directory consulta o serviço para procurar um usuário com um valor de atributo externalId correspondente ao valor de atributo mailNickname de um usuário no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c98e2-320">Azure Active Directory queries the service for a user with an externalId attribute value matching the mailNickname attribute value of a user in Azure AD.</span></span> <span data-ttu-id="c98e2-321">A consulta é expressa como solicitação HTTP como no exemplo, na qual jyoung é o exemplo de um mailNickname de um usuário no Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="c98e2-321">The query is expressed as a Hypertext Transfer Protocol (HTTP) request such as this example, wherein jyoung is a sample of a mailNickname of a user in Azure Active Directory:</span></span> 
  ````
    GET https://.../scim/Users?filter=externalId eq jyoung HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="c98e2-322">Se o serviço foi criado usando as bibliotecas Common Language Infrastructure fornecidas pela Microsoft para implementação de serviços SCIM, a solicitação é convertida em uma chamada ao método Query do provedor de serviços.</span><span class="sxs-lookup"><span data-stu-id="c98e2-322">If the service was built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then the request is translated into a call to the Query method of the service’s provider.</span></span>  <span data-ttu-id="c98e2-323">Veja a assinatura desse método:</span><span class="sxs-lookup"><span data-stu-id="c98e2-323">Here is the signature of that method:</span></span> 
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
  <span data-ttu-id="c98e2-324">Veja a definição da interface Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters:</span><span class="sxs-lookup"><span data-stu-id="c98e2-324">Here is the definition of the Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters interface:</span></span> 
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
  <span data-ttu-id="c98e2-325">No exemplo a seguir de uma consulta para um usuário com um valor fornecido para o atributo externalId, os valores dos argumentos passados para o método Query são:</span><span class="sxs-lookup"><span data-stu-id="c98e2-325">In the following sample of a query for a user with a given value for the externalId attribute, values of the arguments passed to the Query method are:</span></span> 
  * <span data-ttu-id="c98e2-326">parameters.AlternateFilters.Count: 1</span><span class="sxs-lookup"><span data-stu-id="c98e2-326">parameters.AlternateFilters.Count: 1</span></span>
  * <span data-ttu-id="c98e2-327">parameters.AlternateFilters.ElementAt(0).AttributePath: "externalId"</span><span class="sxs-lookup"><span data-stu-id="c98e2-327">parameters.AlternateFilters.ElementAt(0).AttributePath: "externalId"</span></span>
  * <span data-ttu-id="c98e2-328">parameters.AlternateFilters.ElementAt(0).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="c98e2-328">parameters.AlternateFilters.ElementAt(0).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="c98e2-329">parameters.AlternateFilter.ElementAt(0).ComparisonValue: "jyoung"</span><span class="sxs-lookup"><span data-stu-id="c98e2-329">parameters.AlternateFilter.ElementAt(0).ComparisonValue: "jyoung"</span></span>
  * <span data-ttu-id="c98e2-330">correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin.RequestId"]</span><span class="sxs-lookup"><span data-stu-id="c98e2-330">correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin.RequestId"]</span></span> 

2. <span data-ttu-id="c98e2-331">Se a resposta a uma consulta ao serviço Web para procurar um usuário com um valor de atributo externalId que corresponda ao valor de atributo mailNickname de um usuário não retornar nenhum usuário, o Azure Active Directory solicitará que o serviço provisione um usuário correspondente ao usuário no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c98e2-331">If the response to a query to the web service for a user with an externalId attribute value that matches the mailNickname attribute value of a user does not return any users, then Azure Active Directory requests that the service provision a user corresponding to the one in Azure Active Directory.</span></span>  <span data-ttu-id="c98e2-332">Veja um exemplo de tal solicitação:</span><span class="sxs-lookup"><span data-stu-id="c98e2-332">Here is an example of such a request:</span></span> 
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
  <span data-ttu-id="c98e2-333">As bibliotecas Common Language Infrastructure fornecidas pela Microsoft para implementação dos serviços SCIM convertem essa solicitação em uma chamada ao método Create do provedor de serviços.</span><span class="sxs-lookup"><span data-stu-id="c98e2-333">The Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services would translate that request into a call to the Create method of the service’s provider.</span></span>  <span data-ttu-id="c98e2-334">O método Create tem essa assinatura:</span><span class="sxs-lookup"><span data-stu-id="c98e2-334">The Create method has this signature:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> Create(
      Microsoft.SystemForCrossDomainIdentityManagement.Resource resource, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="c98e2-335">Em uma solicitação para provisionar um usuário, o valor do argumento de recurso é uma instância da classe Microsoft.SystemForCrossDomainIdentityManagement.</span><span class="sxs-lookup"><span data-stu-id="c98e2-335">In a request to provision a user, the value of the resource argument is an instance of the Microsoft.SystemForCrossDomainIdentityManagement.</span></span> <span data-ttu-id="c98e2-336">Core2EnterpriseUser, definida na biblioteca Microsoft.SystemForCrossDomainIdentityManagement.Schemas.</span><span class="sxs-lookup"><span data-stu-id="c98e2-336">Core2EnterpriseUser class, defined in the Microsoft.SystemForCrossDomainIdentityManagement.Schemas library.</span></span>  <span data-ttu-id="c98e2-337">Se a solicitação de provisionamento de usuário for bem-sucedida, a implementação do método deverá retornar uma instância da classe Microsoft.SystemForCrossDomainIdentityManagement.</span><span class="sxs-lookup"><span data-stu-id="c98e2-337">If the request to provision the user succeeds, then the implementation of the method is expected to return an instance of the Microsoft.SystemForCrossDomainIdentityManagement.</span></span> <span data-ttu-id="c98e2-338">Classe Core2EnterpriseUser, com o valor da propriedade Identifier definido como o identificador exclusivo do usuário recentemente provisionado.</span><span class="sxs-lookup"><span data-stu-id="c98e2-338">Core2EnterpriseUser class, with the value of the Identifier property set to the unique identifier of the newly provisioned user.</span></span>  

3. <span data-ttu-id="c98e2-339">Para atualizar um usuário conhecido que existe em um repositório de identidades administrado por um SCIM, o Azure Active Directory prossegue solicitando o estado atual desse usuário no serviço com uma solicitação como:</span><span class="sxs-lookup"><span data-stu-id="c98e2-339">To update a user known to exist in an identity store fronted by an SCIM, Azure Active Directory proceeds by requesting the current state of that user from the service with a request such as:</span></span> 
  ````
    GET ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="c98e2-340">Em um serviço criado usando as bibliotecas Common Language Infrastructure fornecidas pela Microsoft para implementação de serviços SCIM, a solicitação é convertida em uma chamada ao método Retrieve do provedor de serviços.</span><span class="sxs-lookup"><span data-stu-id="c98e2-340">In a service built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, the request is translated into a call to the Retrieve method of the service’s provider.</span></span>  <span data-ttu-id="c98e2-341">Veja a assinatura do método Retrieve:</span><span class="sxs-lookup"><span data-stu-id="c98e2-341">Here is the signature of the Retrieve method:</span></span> 
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
  <span data-ttu-id="c98e2-342">No exemplo de uma solicitação para recuperar o estado atual de um usuário, os valores das propriedades do objeto fornecidos como o valor do argumento de parâmetros são:</span><span class="sxs-lookup"><span data-stu-id="c98e2-342">In the example of a request to retrieve the current state of a user, the values of the properties of the object provided as the value of the parameters argument are as follows:</span></span> 
  
  * <span data-ttu-id="c98e2-343">Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="c98e2-343">Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="c98e2-344">SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="c98e2-344">SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

4. <span data-ttu-id="c98e2-345">Se um atributo de referência deve ser atualizado, o Azure Active Directory consulta o serviço para determinar se o valor atual do atributo de referência no repositório de identidades administrado pelo serviço já corresponde ou não ao valor desse atributo no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c98e2-345">If a reference attribute is to be updated, then Azure Active Directory queries the service to determine whether or not the current value of the reference attribute in the identity store fronted by the service already matches the value of that attribute in Azure Active Directory.</span></span> <span data-ttu-id="c98e2-346">Para usuários, o único atributo no qual o valor atual é consultado dessa forma é o atributo de gerenciador.</span><span class="sxs-lookup"><span data-stu-id="c98e2-346">For users, the only attribute of which the current value is queried in this way is the manager attribute.</span></span> <span data-ttu-id="c98e2-347">Veja o exemplo de uma solicitação para determinar se o atributo de gerenciador de um objeto de usuário específico atualmente tem um determinado valor:</span><span class="sxs-lookup"><span data-stu-id="c98e2-347">Here is an example of a request to determine whether the manager attribute of a particular user object currently has a certain value:</span></span> 
  ````
    GET ~/scim/Users?filter=id eq 54D382A4-2050-4C03-94D1-E769F1D15682 and manager eq 2819c223-7f76-453a-919d-413861904646&attributes=id HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="c98e2-348">O valor do parâmetro de consulta de atributos, id, significa que, se existir um objeto de usuário que atenda à expressão fornecida como o valor do parâmetro de consulta de filtro, o serviço deverá responder com um recurso urn:ietf:params:scim:schemas:core:2.0:User ou urn:ietf:params:scim:schemas:extension:enterprise:2.0:User, incluindo apenas o valor do atributo id desse recurso.</span><span class="sxs-lookup"><span data-stu-id="c98e2-348">The value of the attributes query parameter, id, signifies that if a user object exists that satisfies the expression provided as the value of the filter query parameter, then the service is expected to respond with a urn:ietf:params:scim:schemas:core:2.0:User or urn:ietf:params:scim:schemas:extension:enterprise:2.0:User resource, including only the value of that resource’s id attribute.</span></span>  <span data-ttu-id="c98e2-349">O valor do atributo **id** é do conhecimento do solicitante.</span><span class="sxs-lookup"><span data-stu-id="c98e2-349">The value of the **id** attribute is known to the requestor.</span></span> <span data-ttu-id="c98e2-350">Ele é incluído no valor do parâmetro de consulta de filtro; a finalidade de solicitá-lo, na verdade, é solicitar uma representação mínima de um recurso que atenda à expressão de filtro como uma indicação da existência ou não de tal objeto.</span><span class="sxs-lookup"><span data-stu-id="c98e2-350">It is included in the value of the filter query parameter; the purpose of asking for it is actually to request a minimal representation of a resource that satisfying the filter expression as an indication of whether or not any such object exists.</span></span>   

  <span data-ttu-id="c98e2-351">Se o serviço foi criado usando as bibliotecas Common Language Infrastructure fornecidas pela Microsoft para implementação de serviços SCIM, a solicitação é convertida em uma chamada ao método Query do provedor de serviços.</span><span class="sxs-lookup"><span data-stu-id="c98e2-351">If the service was built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then the request is translated into a call to the Query method of the service’s provider.</span></span> <span data-ttu-id="c98e2-352">O valor das propriedades do objeto fornecido como o valor do argumento de parâmetros é:</span><span class="sxs-lookup"><span data-stu-id="c98e2-352">The value of the properties of the object provided as the value of the parameters argument are as follows:</span></span> 
  
  * <span data-ttu-id="c98e2-353">parameters.AlternateFilters.Count: 2</span><span class="sxs-lookup"><span data-stu-id="c98e2-353">parameters.AlternateFilters.Count: 2</span></span>
  * <span data-ttu-id="c98e2-354">parameters.AlternateFilters.ElementAt(x).AttributePath: "id"</span><span class="sxs-lookup"><span data-stu-id="c98e2-354">parameters.AlternateFilters.ElementAt(x).AttributePath: "id"</span></span>
  * <span data-ttu-id="c98e2-355">parameters.AlternateFilters.ElementAt(x).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="c98e2-355">parameters.AlternateFilters.ElementAt(x).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="c98e2-356">parameters.AlternateFilter.ElementAt(x).ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="c98e2-356">parameters.AlternateFilter.ElementAt(x).ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="c98e2-357">parameters.AlternateFilters.ElementAt(y).AttributePath: "manager"</span><span class="sxs-lookup"><span data-stu-id="c98e2-357">parameters.AlternateFilters.ElementAt(y).AttributePath: "manager"</span></span>
  * <span data-ttu-id="c98e2-358">parameters.AlternateFilters.ElementAt(y).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="c98e2-358">parameters.AlternateFilters.ElementAt(y).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="c98e2-359">parameters.AlternateFilter.ElementAt(y).ComparisonValue: "2819c223-7f76-453a-919d-413861904646"</span><span class="sxs-lookup"><span data-stu-id="c98e2-359">parameters.AlternateFilter.ElementAt(y).ComparisonValue: "2819c223-7f76-453a-919d-413861904646"</span></span>
  * <span data-ttu-id="c98e2-360">parameters.RequestedAttributePaths.ElementAt(0): "id"</span><span class="sxs-lookup"><span data-stu-id="c98e2-360">parameters.RequestedAttributePaths.ElementAt(0): "id"</span></span>
  * <span data-ttu-id="c98e2-361">parameters.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="c98e2-361">parameters.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

  <span data-ttu-id="c98e2-362">Aqui, o valor do índice x pode ser 0 e o valor do índice y pode ser 1, ou o valor de x pode ser 1 e o valor de y pode ser 0, dependendo da ordem das expressões do parâmetro do filtro de consulta.</span><span class="sxs-lookup"><span data-stu-id="c98e2-362">Here, the value of the index x may be 0 and the value of the index y may be 1, or the value of x may be 1 and the value of y may be 0, depending on the order of the expressions of the filter query parameter.</span></span>   

5. <span data-ttu-id="c98e2-363">Veja um exemplo de uma solicitação do Azure Active Directory a um serviço SCIM para atualizar um usuário:</span><span class="sxs-lookup"><span data-stu-id="c98e2-363">Here is an example of a request from Azure Active Directory to an SCIM service to update a user:</span></span> 
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
  <span data-ttu-id="c98e2-364">As bibliotecas Common Language Infrastructure fornecidas pela Microsoft para implementação dos serviços SCIM convertem a solicitação em uma chamada ao método Update do provedor de serviços.</span><span class="sxs-lookup"><span data-stu-id="c98e2-364">The Microsoft Common Language Infrastructure libraries for implementing SCIM services would translate the request into a call to the Update method of the service’s provider.</span></span> <span data-ttu-id="c98e2-365">Veja a assinatura do método Update:</span><span class="sxs-lookup"><span data-stu-id="c98e2-365">Here is the signature of the Update method:</span></span> 
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
    <span data-ttu-id="c98e2-366">No exemplo de uma solicitação para atualizar um usuário, o objeto fornecido como valor do argumento de patch tem estes valores de propriedade:</span><span class="sxs-lookup"><span data-stu-id="c98e2-366">In the example of a request to update a user, the object provided as the value of the patch argument has these property values:</span></span> 
  
  * <span data-ttu-id="c98e2-367">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="c98e2-367">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="c98e2-368">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="c98e2-368">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>
  * <span data-ttu-id="c98e2-369">(PatchRequest as PatchRequest2).Operations.Count: 1</span><span class="sxs-lookup"><span data-stu-id="c98e2-369">(PatchRequest as PatchRequest2).Operations.Count: 1</span></span>
  * <span data-ttu-id="c98e2-370">(PatchRequest as PatchRequest2).Operations.ElementAt(0).OperationName: OperationName.Add</span><span class="sxs-lookup"><span data-stu-id="c98e2-370">(PatchRequest as PatchRequest2).Operations.ElementAt(0).OperationName: OperationName.Add</span></span>
  * <span data-ttu-id="c98e2-371">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Path.AttributePath: "manager"</span><span class="sxs-lookup"><span data-stu-id="c98e2-371">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Path.AttributePath: "manager"</span></span>
  * <span data-ttu-id="c98e2-372">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.Count: 1</span><span class="sxs-lookup"><span data-stu-id="c98e2-372">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.Count: 1</span></span>
  * <span data-ttu-id="c98e2-373">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Reference: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646</span><span class="sxs-lookup"><span data-stu-id="c98e2-373">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Reference: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646</span></span>
  * <span data-ttu-id="c98e2-374">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Value: 2819c223-7f76-453a-919d-413861904646</span><span class="sxs-lookup"><span data-stu-id="c98e2-374">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Value: 2819c223-7f76-453a-919d-413861904646</span></span>

6. <span data-ttu-id="c98e2-375">Para desprovisionar um usuário de um repositório de identidades administrado por um serviço SCIM, o Azure AD envia uma solicitação como esta:</span><span class="sxs-lookup"><span data-stu-id="c98e2-375">To de-provision a user from an identity store fronted by an SCIM service, Azure AD sends a request such as:</span></span> 
  ````
    DELETE ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="c98e2-376">Se o serviço tiver sido criado usando as bibliotecas Common Language Infrastructure fornecidas pela Microsoft para implementação de serviços SCIM, a solicitação é convertida em uma chamada ao método Delete do provedor de serviços.</span><span class="sxs-lookup"><span data-stu-id="c98e2-376">If the service was built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then the request is translated into a call to the Delete method of the service’s provider.</span></span>   <span data-ttu-id="c98e2-377">Esse método tem esta assinatura:</span><span class="sxs-lookup"><span data-stu-id="c98e2-377">That method has this signature:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // is defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 
    System.Threading.Tasks.Task Delete(
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier  
        resourceIdentifier, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="c98e2-378">O objeto fornecido como valor do argumento resourceIdentifier tem estes valores de propriedade no exemplo de uma solicitação para desprovisionar um usuário:</span><span class="sxs-lookup"><span data-stu-id="c98e2-378">The object provided as the value of the resourceIdentifier argument has these property values in the example of a request to de-provision a user:</span></span> 
  
  * <span data-ttu-id="c98e2-379">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="c98e2-379">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="c98e2-380">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="c98e2-380">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

## <a name="group-provisioning-and-de-provisioning"></a><span data-ttu-id="c98e2-381">Provisionamento e desprovisionamento de grupo</span><span class="sxs-lookup"><span data-stu-id="c98e2-381">Group provisioning and de-provisioning</span></span>
<span data-ttu-id="c98e2-382">A seguinte ilustração mostra as mensagens que o Azure AD envia a um serviço SCIM para gerenciar o ciclo de vida de um grupo em outro repositório de identidades.</span><span class="sxs-lookup"><span data-stu-id="c98e2-382">The following illustration shows the messages that Azure AcD sends to a SCIM service to manage the lifecycle of a group in another identity store.</span></span>  <span data-ttu-id="c98e2-383">Essas mensagens são diferentes das mensagens pertencentes aos usuários em três aspectos:</span><span class="sxs-lookup"><span data-stu-id="c98e2-383">Those messages differ from the messages pertaining to users in three ways:</span></span> 

* <span data-ttu-id="c98e2-384">O esquema de um recurso de grupo é identificado como http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span><span class="sxs-lookup"><span data-stu-id="c98e2-384">The schema of a group resource is identified as http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span></span>  
* <span data-ttu-id="c98e2-385">As solicitações para recuperar grupos estipulam que o atributo de membros deve ser excluído de qualquer recurso fornecido em resposta à solicitação.</span><span class="sxs-lookup"><span data-stu-id="c98e2-385">Requests to retrieve groups stipulate that the members attribute is to be excluded from any resource provided in response to the request.</span></span>  
* <span data-ttu-id="c98e2-386">As solicitações para determinar se um atributo de referência tem um determinado valor são sobre o atributo de membros.</span><span class="sxs-lookup"><span data-stu-id="c98e2-386">Requests to determine whether a reference attribute has a certain value are requests about the members attribute.</span></span>  

<span data-ttu-id="c98e2-387">![][5]
*Figura 6: sequência de provisionamento e desprovisionamento de grupo*</span><span class="sxs-lookup"><span data-stu-id="c98e2-387">![][5]
*Figure 6: Group provisioning and de-provisioning sequence*</span></span>

## <a name="related-articles"></a><span data-ttu-id="c98e2-388">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="c98e2-388">Related articles</span></span>
* [<span data-ttu-id="c98e2-389">Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="c98e2-389">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="c98e2-390">Automatizar o provisionamento/desprovisionamento de usuários para aplicativos SaaS</span><span class="sxs-lookup"><span data-stu-id="c98e2-390">Automate User Provisioning/Deprovisioning to SaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="c98e2-391">Personalizando os mapeamentos de atributos para provisionamento de usuários</span><span class="sxs-lookup"><span data-stu-id="c98e2-391">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="c98e2-392">Escrevendo expressões para mapeamentos de atributo</span><span class="sxs-lookup"><span data-stu-id="c98e2-392">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="c98e2-393">Filtros de escopo para provisionamento de usuários</span><span class="sxs-lookup"><span data-stu-id="c98e2-393">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="c98e2-394">Notificações de provisionamento de conta</span><span class="sxs-lookup"><span data-stu-id="c98e2-394">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="c98e2-395">Lista de tutoriais sobre como integrar aplicativos SaaS</span><span class="sxs-lookup"><span data-stu-id="c98e2-395">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[0]: ./media/active-directory-scim-provisioning/scim-figure-1.PNG
[1]: ./media/active-directory-scim-provisioning/scim-figure-2a.PNG
[2]: ./media/active-directory-scim-provisioning/scim-figure-2b.PNG
[3]: ./media/active-directory-scim-provisioning/scim-figure-3.PNG
[4]: ./media/active-directory-scim-provisioning/scim-figure-4.PNG
[5]: ./media/active-directory-scim-provisioning/scim-figure-5.PNG
