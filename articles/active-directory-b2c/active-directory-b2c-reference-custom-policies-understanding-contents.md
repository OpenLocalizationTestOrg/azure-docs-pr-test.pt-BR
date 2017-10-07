---
title: "B2C de diretório ativo do Azure: Compreendendo políticas personalizadas de pacote de inicializador Olá | Microsoft Docs"
description: "Um tópico sobre as políticas personalizadas do Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/25/2017
ms.author: joroja
ms.openlocfilehash: 3484e8cc6fa6a9d57c2aa14c0cc9616065892d10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-custom-policies-of-hello-azure-ad-b2c-custom-policy-starter-pack"></a><span data-ttu-id="3899a-103">Noções básicas sobre políticas personalizadas de saudação do pacote de inicializador de política personalizada hello Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="3899a-103">Understanding hello custom policies of hello Azure AD B2C Custom Policy starter pack</span></span>

<span data-ttu-id="3899a-104">Esta seção lista todos os elementos principais de Olá da política de saudação B2C_1A_base que acompanha a saudação **Starter pacote** e que é utilizado para criar suas próprias políticas por meio da herança de saudação do hello *B2C_1A_base_ política de extensões*.</span><span class="sxs-lookup"><span data-stu-id="3899a-104">This section lists all hello core elements of hello B2C_1A_base policy that comes with hello **Starter Pack** and that is leveraged for authoring your own policies through hello inheritance of hello *B2C_1A_base_extensions policy*.</span></span>

<span data-ttu-id="3899a-105">Como tal, ele mais enfoca especialmente Olá já definido de declaração de tipos, transformação de declarações, definições de conteúdo, os provedores de declarações com seus perfis técnica e Olá Jornadas de usuário de núcleo.</span><span class="sxs-lookup"><span data-stu-id="3899a-105">As such, it more particularly focusses on hello already defined claim types, claims transformations, content definitions, claims providers with their technical profile(s), and hello core user journeys.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3899a-106">A Microsoft não oferece nenhuma garantia, expressa ou implícita, com respeito toohello informações fornecidas daqui por diante.</span><span class="sxs-lookup"><span data-stu-id="3899a-106">Microsoft makes no warranties, express or implied, with respect toohello information provided hereafter.</span></span> <span data-ttu-id="3899a-107">As alterações podem ser introduzidas a qualquer momento, antes do tempo de GA, no momento da GA, ou depois.</span><span class="sxs-lookup"><span data-stu-id="3899a-107">Changes may be introduced at any time, before GA time, at GA time, or after.</span></span>

<span data-ttu-id="3899a-108">Suas próprias políticas e a saudação B2C_1A_base_extensions política podem substituir essas definições e estender essa política pai fornecendo outros adicionais conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="3899a-108">Both your own policies and hello B2C_1A_base_extensions policy can override these definitions and extend this parent policy by providing additional ones as needed.</span></span>

<span data-ttu-id="3899a-109">Olá elementos principais de saudação *B2C_1A_base política* são tipos de declaração de transformação de declarações e definições de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="3899a-109">hello core elements of hello *B2C_1A_base policy* are claim types, claims transformations, and content definitions.</span></span> <span data-ttu-id="3899a-110">Esses elementos podem toobe suscetível referenciado em suas próprias políticas, bem como Olá *B2C_1A_base_extensions política*.</span><span class="sxs-lookup"><span data-stu-id="3899a-110">These elements can susceptible toobe referenced in your own policies as well as in hello *B2C_1A_base_extensions policy*.</span></span>

## <a name="claims-schemas"></a><span data-ttu-id="3899a-111">Esquemas de declarações</span><span class="sxs-lookup"><span data-stu-id="3899a-111">Claims schemas</span></span>

<span data-ttu-id="3899a-112">Esses esquemas de declarações são divididos em três seções:</span><span class="sxs-lookup"><span data-stu-id="3899a-112">This claims schemas is divided into three sections:</span></span>

1.  <span data-ttu-id="3899a-113">Uma primeira seção lista as declarações de mínimo de saudação que são necessárias para Olá usuário jornadas toowork corretamente.</span><span class="sxs-lookup"><span data-stu-id="3899a-113">A first section that lists hello minimum claims that are required for hello user journeys toowork properly.</span></span>
2.  <span data-ttu-id="3899a-114">Uma segunda seção que listas Olá declarações necessárias para parâmetros de cadeia de caracteres de consulta e outros parâmetros especiais toobe passado tooother provedores de declarações, especialmente login.microsoftonline.com para autenticação.</span><span class="sxs-lookup"><span data-stu-id="3899a-114">A second section that lists hello claims required for query string parameters and other special parameters toobe passed tooother claims providers, especially login.microsoftonline.com for authentication.</span></span> <span data-ttu-id="3899a-115">**Não modifique essas declarações**.</span><span class="sxs-lookup"><span data-stu-id="3899a-115">**Please do not modify these claims**.</span></span>
3.  <span data-ttu-id="3899a-116">E finalmente uma terceira seção que lista quaisquer declarações adicionais e opcionais que podem ser coletadas de usuário Olá, armazenado no diretório de saudação e enviadas em tokens durante a entrada.</span><span class="sxs-lookup"><span data-stu-id="3899a-116">And eventually a third section that lists any additional, optional claims that can be collected from hello user, stored in hello directory and sent in tokens during sign in.</span></span> <span data-ttu-id="3899a-117">Podem ser adicionadas novas declarações de tipo toobe coletados do usuário hello e/ou enviados no token Olá nesta seção.</span><span class="sxs-lookup"><span data-stu-id="3899a-117">New claims type toobe collected from hello user and/or sent in hello token can be added in this section.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3899a-118">Olá declarações esquema contém restrições em determinados declarações como nomes de usuário e senhas.</span><span class="sxs-lookup"><span data-stu-id="3899a-118">hello claims schema contains restrictions on certain claims such as passwords and usernames.</span></span> <span data-ttu-id="3899a-119">Olá diretiva de confiança do Framework (TF) trata do AD do Azure como qualquer outro provedor de declarações e todas as suas restrições são modeladas na política de premium Olá.</span><span class="sxs-lookup"><span data-stu-id="3899a-119">hello Trust Framework (TF) policy treats Azure AD as any other claims provider and all its restrictions are modelled in hello premium policy.</span></span> <span data-ttu-id="3899a-120">Uma política pode ser modificado tooadd mais restrições ou usar outro provedor de declarações para o armazenamento de credenciais que terá seus próprio restrições.</span><span class="sxs-lookup"><span data-stu-id="3899a-120">A policy could be modified tooadd more restrictions, or use another claims provider for credential storage which will have its own restrictions.</span></span>

<span data-ttu-id="3899a-121">tipos de declaração disponíveis Olá estão listados abaixo.</span><span class="sxs-lookup"><span data-stu-id="3899a-121">hello available claim types are listed below.</span></span>

### <a name="claims-that-are-required-for-hello-user-journeys"></a><span data-ttu-id="3899a-122">Declarações que são necessárias para viagens de usuário Olá</span><span class="sxs-lookup"><span data-stu-id="3899a-122">Claims that are required for hello user journeys</span></span>

<span data-ttu-id="3899a-123">Olá declarações a seguir é necessário para usuário jornadas toowork corretamente:</span><span class="sxs-lookup"><span data-stu-id="3899a-123">hello following claims are required for user journeys toowork properly:</span></span>

| <span data-ttu-id="3899a-124">Tipo de declarações</span><span class="sxs-lookup"><span data-stu-id="3899a-124">Claims type</span></span> | <span data-ttu-id="3899a-125">Descrição</span><span class="sxs-lookup"><span data-stu-id="3899a-125">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="3899a-126">*UserId*</span><span class="sxs-lookup"><span data-stu-id="3899a-126">*UserId*</span></span> | <span data-ttu-id="3899a-127">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="3899a-127">Username</span></span> |
| <span data-ttu-id="3899a-128">*signInName*</span><span class="sxs-lookup"><span data-stu-id="3899a-128">*signInName*</span></span> | <span data-ttu-id="3899a-129">Nome de entrada</span><span class="sxs-lookup"><span data-stu-id="3899a-129">Sign in name</span></span> |
| <span data-ttu-id="3899a-130">*tenantId*</span><span class="sxs-lookup"><span data-stu-id="3899a-130">*tenantId*</span></span> | <span data-ttu-id="3899a-131">Identificador do locatário (ID) do objeto de usuário de saudação no Azure AD B2C Premium</span><span class="sxs-lookup"><span data-stu-id="3899a-131">Tenant identifier (ID) of hello user object in Azure AD B2C Premium</span></span> |
| <span data-ttu-id="3899a-132">*objectId*</span><span class="sxs-lookup"><span data-stu-id="3899a-132">*objectId*</span></span> | <span data-ttu-id="3899a-133">Identificador de objeto (ID) do objeto de usuário de saudação no Azure AD B2C Premium</span><span class="sxs-lookup"><span data-stu-id="3899a-133">Object identifier (ID) of hello user object in Azure AD B2C Premium</span></span> |
| <span data-ttu-id="3899a-134">*password*</span><span class="sxs-lookup"><span data-stu-id="3899a-134">*password*</span></span> | <span data-ttu-id="3899a-135">Senha</span><span class="sxs-lookup"><span data-stu-id="3899a-135">Password</span></span> |
| <span data-ttu-id="3899a-136">*newPassword*</span><span class="sxs-lookup"><span data-stu-id="3899a-136">*newPassword*</span></span> | |
| <span data-ttu-id="3899a-137">*reenterPassword*</span><span class="sxs-lookup"><span data-stu-id="3899a-137">*reenterPassword*</span></span> | |
| <span data-ttu-id="3899a-138">*passwordPolicies*</span><span class="sxs-lookup"><span data-stu-id="3899a-138">*passwordPolicies*</span></span> | <span data-ttu-id="3899a-139">Políticas de senha usadas pela força da senha toodetermine B2C do Azure AD Premium, expiração, etc.</span><span class="sxs-lookup"><span data-stu-id="3899a-139">Password policies used by Azure AD B2C Premium toodetermine password strength, expiry, etc.</span></span> |
| <span data-ttu-id="3899a-140">*sub*</span><span class="sxs-lookup"><span data-stu-id="3899a-140">*sub*</span></span> | |
| <span data-ttu-id="3899a-141">*alternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="3899a-141">*alternativeSecurityId*</span></span> | |
| <span data-ttu-id="3899a-142">*identityProvider*</span><span class="sxs-lookup"><span data-stu-id="3899a-142">*identityProvider*</span></span> | |
| <span data-ttu-id="3899a-143">*displayName*</span><span class="sxs-lookup"><span data-stu-id="3899a-143">*displayName*</span></span> | |
| <span data-ttu-id="3899a-144">*strongAuthenticationPhoneNumber*</span><span class="sxs-lookup"><span data-stu-id="3899a-144">*strongAuthenticationPhoneNumber*</span></span> | <span data-ttu-id="3899a-145">O número de telefone do usuário</span><span class="sxs-lookup"><span data-stu-id="3899a-145">User's telephone number</span></span> |
| <span data-ttu-id="3899a-146">*Verified.strongAuthenticationPhoneNumber*</span><span class="sxs-lookup"><span data-stu-id="3899a-146">*Verified.strongAuthenticationPhoneNumber*</span></span> | |
| <span data-ttu-id="3899a-147">*email*</span><span class="sxs-lookup"><span data-stu-id="3899a-147">*email*</span></span> | <span data-ttu-id="3899a-148">Endereço de email que pode ser usado toocontact Olá usuário</span><span class="sxs-lookup"><span data-stu-id="3899a-148">Email address that can be used toocontact hello user</span></span> |
| <span data-ttu-id="3899a-149">*signInNamesInfo.emailAddress*</span><span class="sxs-lookup"><span data-stu-id="3899a-149">*signInNamesInfo.emailAddress*</span></span> | <span data-ttu-id="3899a-150">Endereço de email que Olá usuário pode usar toosign em</span><span class="sxs-lookup"><span data-stu-id="3899a-150">Email address that hello user can use toosign in</span></span> |
| <span data-ttu-id="3899a-151">*otherMails*</span><span class="sxs-lookup"><span data-stu-id="3899a-151">*otherMails*</span></span> | <span data-ttu-id="3899a-152">Endereços de email que podem ser usado toocontact Olá usuário</span><span class="sxs-lookup"><span data-stu-id="3899a-152">Email addresses that can be used toocontact hello user</span></span> |
| <span data-ttu-id="3899a-153">*userPrincipalName*</span><span class="sxs-lookup"><span data-stu-id="3899a-153">*userPrincipalName*</span></span> | <span data-ttu-id="3899a-154">Nome de usuário conforme armazenado no hello B2C do Azure AD Premium</span><span class="sxs-lookup"><span data-stu-id="3899a-154">Username as stored in hello Azure AD B2C Premium</span></span> |
| <span data-ttu-id="3899a-155">*upnUserName*</span><span class="sxs-lookup"><span data-stu-id="3899a-155">*upnUserName*</span></span> | <span data-ttu-id="3899a-156">Nome de usuário para criar o nome principal do usuário</span><span class="sxs-lookup"><span data-stu-id="3899a-156">Username for creating user principal name</span></span> |
| <span data-ttu-id="3899a-157">*mailNickName*</span><span class="sxs-lookup"><span data-stu-id="3899a-157">*mailNickName*</span></span> | <span data-ttu-id="3899a-158">Nome de nick de email do usuário conforme armazenado no hello B2C do Azure AD Premium</span><span class="sxs-lookup"><span data-stu-id="3899a-158">User's mail nick name as stored in hello Azure AD B2C Premium</span></span> |
| <span data-ttu-id="3899a-159">*newUser*</span><span class="sxs-lookup"><span data-stu-id="3899a-159">*newUser*</span></span> | |
| <span data-ttu-id="3899a-160">*executed-SelfAsserted-Input*</span><span class="sxs-lookup"><span data-stu-id="3899a-160">*executed-SelfAsserted-Input*</span></span> | <span data-ttu-id="3899a-161">Declaração que especifica se os atributos foram coletados do usuário Olá</span><span class="sxs-lookup"><span data-stu-id="3899a-161">Claim that specifies whether attributes were collected from hello user</span></span> |
| <span data-ttu-id="3899a-162">*executed-PhoneFactor-Input*</span><span class="sxs-lookup"><span data-stu-id="3899a-162">*executed-PhoneFactor-Input*</span></span> | <span data-ttu-id="3899a-163">Declaração que especifica se um novo número de telefone foram coletado do usuário Olá</span><span class="sxs-lookup"><span data-stu-id="3899a-163">Claim that specifies whether a new phone number was collected from hello user</span></span> |
| <span data-ttu-id="3899a-164">*authenticationSource*</span><span class="sxs-lookup"><span data-stu-id="3899a-164">*authenticationSource*</span></span> | <span data-ttu-id="3899a-165">Especifica se o usuário Olá foi autenticado no provedor de identidade sociais, login.microsoftonline.com ou conta local</span><span class="sxs-lookup"><span data-stu-id="3899a-165">Specifies whether hello user was authenticated at Social Identity Provider, login.microsoftonline.com, or local account</span></span> |

### <a name="claims-required-for-query-string-parameters-and-other-special-parameters"></a><span data-ttu-id="3899a-166">Declarações necessárias para parâmetros de cadeia de caracteres de consulta e outros parâmetros especiais</span><span class="sxs-lookup"><span data-stu-id="3899a-166">Claims required for query string parameters and other special parameters</span></span>

<span data-ttu-id="3899a-167">Olá seguintes declarações são necessários toopass nos provedores de declarações de tooother parâmetros especiais (incluindo alguns parâmetros de cadeia de caracteres de consulta):</span><span class="sxs-lookup"><span data-stu-id="3899a-167">hello following claims are required toopass on special parameters (including some query string parameters) tooother claims providers:</span></span>

| <span data-ttu-id="3899a-168">Tipo de declarações</span><span class="sxs-lookup"><span data-stu-id="3899a-168">Claims type</span></span> | <span data-ttu-id="3899a-169">Descrição</span><span class="sxs-lookup"><span data-stu-id="3899a-169">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="3899a-170">*nux*</span><span class="sxs-lookup"><span data-stu-id="3899a-170">*nux*</span></span> | <span data-ttu-id="3899a-171">O parâmetro especial passado para toologin.microsoftonline.com de autenticação de conta local</span><span class="sxs-lookup"><span data-stu-id="3899a-171">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="3899a-172">*nca*</span><span class="sxs-lookup"><span data-stu-id="3899a-172">*nca*</span></span> | <span data-ttu-id="3899a-173">O parâmetro especial passado para toologin.microsoftonline.com de autenticação de conta local</span><span class="sxs-lookup"><span data-stu-id="3899a-173">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="3899a-174">*prompt*</span><span class="sxs-lookup"><span data-stu-id="3899a-174">*prompt*</span></span> | <span data-ttu-id="3899a-175">O parâmetro especial passado para toologin.microsoftonline.com de autenticação de conta local</span><span class="sxs-lookup"><span data-stu-id="3899a-175">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="3899a-176">*mkt*</span><span class="sxs-lookup"><span data-stu-id="3899a-176">*mkt*</span></span> | <span data-ttu-id="3899a-177">O parâmetro especial passado para toologin.microsoftonline.com de autenticação de conta local</span><span class="sxs-lookup"><span data-stu-id="3899a-177">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="3899a-178">*lc*</span><span class="sxs-lookup"><span data-stu-id="3899a-178">*lc*</span></span> | <span data-ttu-id="3899a-179">O parâmetro especial passado para toologin.microsoftonline.com de autenticação de conta local</span><span class="sxs-lookup"><span data-stu-id="3899a-179">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="3899a-180">*grant_type*</span><span class="sxs-lookup"><span data-stu-id="3899a-180">*grant_type*</span></span> | <span data-ttu-id="3899a-181">O parâmetro especial passado para toologin.microsoftonline.com de autenticação de conta local</span><span class="sxs-lookup"><span data-stu-id="3899a-181">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="3899a-182">*scope*</span><span class="sxs-lookup"><span data-stu-id="3899a-182">*scope*</span></span> | <span data-ttu-id="3899a-183">O parâmetro especial passado para toologin.microsoftonline.com de autenticação de conta local</span><span class="sxs-lookup"><span data-stu-id="3899a-183">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="3899a-184">*client_id*</span><span class="sxs-lookup"><span data-stu-id="3899a-184">*client_id*</span></span> | <span data-ttu-id="3899a-185">O parâmetro especial passado para toologin.microsoftonline.com de autenticação de conta local</span><span class="sxs-lookup"><span data-stu-id="3899a-185">Special parameter passed for local account authentication toologin.microsoftonline.com</span></span> |
| <span data-ttu-id="3899a-186">*objectIdFromSession*</span><span class="sxs-lookup"><span data-stu-id="3899a-186">*objectIdFromSession*</span></span> | <span data-ttu-id="3899a-187">Parâmetro fornecido pelo saudação padrão sessão gerenciamento provedor tooindicate que Olá id de objeto foi recuperado de uma sessão SSO</span><span class="sxs-lookup"><span data-stu-id="3899a-187">Parameter provided by hello default session management provider tooindicate that hello object id has been retrieved from an SSO session</span></span> |
| <span data-ttu-id="3899a-188">*isActiveMFASession*</span><span class="sxs-lookup"><span data-stu-id="3899a-188">*isActiveMFASession*</span></span> | <span data-ttu-id="3899a-189">Parâmetro fornecido pelo Olá MFA sessão gerenciamento tooindicate que usuário Olá tem uma sessão ativa do MFA</span><span class="sxs-lookup"><span data-stu-id="3899a-189">Parameter provided by hello MFA session management tooindicate that hello user has an active MFA session</span></span> |

### <a name="additional-optional-claims-that-can-be-collected"></a><span data-ttu-id="3899a-190">Declarações adicionais (opcional) que podem ser coletadas</span><span class="sxs-lookup"><span data-stu-id="3899a-190">Additional (optional) claims that can be collected</span></span>

<span data-ttu-id="3899a-191">seguinte Olá declarações são declarações adicionais que possam ser coletadas dos usuários hello, armazenado no diretório hello e enviadas no token de saudação.</span><span class="sxs-lookup"><span data-stu-id="3899a-191">hello following claims are additional claims that can be collected from hello users, stored in hello directory, and sent in hello token.</span></span> <span data-ttu-id="3899a-192">Conforme descrito antes, declarações adicionais podem ser adicionadas a lista de toothis.</span><span class="sxs-lookup"><span data-stu-id="3899a-192">As outlined before, additional claims can be added toothis list.</span></span>

| <span data-ttu-id="3899a-193">Tipo de declarações</span><span class="sxs-lookup"><span data-stu-id="3899a-193">Claims type</span></span> | <span data-ttu-id="3899a-194">Descrição</span><span class="sxs-lookup"><span data-stu-id="3899a-194">Description</span></span> |
|-------------|-------------|
| <span data-ttu-id="3899a-195">*givenName*</span><span class="sxs-lookup"><span data-stu-id="3899a-195">*givenName*</span></span> | <span data-ttu-id="3899a-196">Nome do usuário (também conhecido como primeiro nome)</span><span class="sxs-lookup"><span data-stu-id="3899a-196">User's given name (also known as first name)</span></span> |
| <span data-ttu-id="3899a-197">*surname*</span><span class="sxs-lookup"><span data-stu-id="3899a-197">*surname*</span></span> | <span data-ttu-id="3899a-198">Sobrenome do usuário (também conhecido como nome de família ou último nome)</span><span class="sxs-lookup"><span data-stu-id="3899a-198">User's surname (also known as family name or last name)</span></span> |
| <span data-ttu-id="3899a-199">*Extension_picture*</span><span class="sxs-lookup"><span data-stu-id="3899a-199">*Extension_picture*</span></span> | <span data-ttu-id="3899a-200">Imagem do usuário do social</span><span class="sxs-lookup"><span data-stu-id="3899a-200">User's picture from social</span></span> |

## <a name="claim-transformations"></a><span data-ttu-id="3899a-201">Transformações de declaração</span><span class="sxs-lookup"><span data-stu-id="3899a-201">Claim transformations</span></span>

<span data-ttu-id="3899a-202">transformações de declaração disponíveis Olá estão listadas abaixo.</span><span class="sxs-lookup"><span data-stu-id="3899a-202">hello available claim transformations are listed below.</span></span>

| <span data-ttu-id="3899a-203">Transformação de declaração</span><span class="sxs-lookup"><span data-stu-id="3899a-203">Claim transformation</span></span> | <span data-ttu-id="3899a-204">Descrição</span><span class="sxs-lookup"><span data-stu-id="3899a-204">Description</span></span> |
|----------------------|-------------|
| <span data-ttu-id="3899a-205">*CreateOtherMailsFromEmail*</span><span class="sxs-lookup"><span data-stu-id="3899a-205">*CreateOtherMailsFromEmail*</span></span> | |
| <span data-ttu-id="3899a-206">*CreateRandomUPNUserName*</span><span class="sxs-lookup"><span data-stu-id="3899a-206">*CreateRandomUPNUserName*</span></span> | |
| <span data-ttu-id="3899a-207">*CreateUserPrincipalName*</span><span class="sxs-lookup"><span data-stu-id="3899a-207">*CreateUserPrincipalName*</span></span> | |
| <span data-ttu-id="3899a-208">*CreateSubjectClaimFromObjectID*</span><span class="sxs-lookup"><span data-stu-id="3899a-208">*CreateSubjectClaimFromObjectID*</span></span> | |
| <span data-ttu-id="3899a-209">*CreateSubjectClaimFromAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="3899a-209">*CreateSubjectClaimFromAlternativeSecurityId*</span></span> | |
| <span data-ttu-id="3899a-210">*CreateAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="3899a-210">*CreateAlternativeSecurityId*</span></span> | |

## <a name="content-definitions"></a><span data-ttu-id="3899a-211">Definições de conteúdo</span><span class="sxs-lookup"><span data-stu-id="3899a-211">Content definitions</span></span>

<span data-ttu-id="3899a-212">Esta seção descreve as definições de conteúdo Olá já declaradas no hello *B2C_1A_base* política.</span><span class="sxs-lookup"><span data-stu-id="3899a-212">This section describes hello content definitions already declared in hello *B2C_1A_base* policy.</span></span> <span data-ttu-id="3899a-213">Essas definições de conteúdo são suscetível toobe referenciado, substituído e/ou estendida conforme necessário em suas próprias políticas, bem como Olá *B2C_1A_base_extensions* política.</span><span class="sxs-lookup"><span data-stu-id="3899a-213">These content definitions are susceptible toobe referenced, overridden, and/or extended as needed in your own policies as well as in hello *B2C_1A_base_extensions* policy.</span></span>

| <span data-ttu-id="3899a-214">Provedor de declarações</span><span class="sxs-lookup"><span data-stu-id="3899a-214">Claims provider</span></span> | <span data-ttu-id="3899a-215">Descrição</span><span class="sxs-lookup"><span data-stu-id="3899a-215">Description</span></span> |
|-----------------|-------------|
| <span data-ttu-id="3899a-216">*Facebook*</span><span class="sxs-lookup"><span data-stu-id="3899a-216">*Facebook*</span></span> | |
| <span data-ttu-id="3899a-217">*Local Account SignIn*</span><span class="sxs-lookup"><span data-stu-id="3899a-217">*Local Account SignIn*</span></span> | |
| <span data-ttu-id="3899a-218">*PhoneFactor*</span><span class="sxs-lookup"><span data-stu-id="3899a-218">*PhoneFactor*</span></span> | |
| <span data-ttu-id="3899a-219">*Active Directory do Azure*</span><span class="sxs-lookup"><span data-stu-id="3899a-219">*Azure Active Directory*</span></span> | |
| <span data-ttu-id="3899a-220">*Autodeclarado*</span><span class="sxs-lookup"><span data-stu-id="3899a-220">*Self Asserted*</span></span> | |
| <span data-ttu-id="3899a-221">*Conta local*</span><span class="sxs-lookup"><span data-stu-id="3899a-221">*Local Account*</span></span> | |
| <span data-ttu-id="3899a-222">*Gerenciamento da Sessão*</span><span class="sxs-lookup"><span data-stu-id="3899a-222">*Session Management*</span></span> | |
| <span data-ttu-id="3899a-223">*Mecanismo da política do Trustframework*</span><span class="sxs-lookup"><span data-stu-id="3899a-223">*Trustframework Policy Engine*</span></span> | |
| <span data-ttu-id="3899a-224">*TechnicalProfiles*</span><span class="sxs-lookup"><span data-stu-id="3899a-224">*TechnicalProfiles*</span></span> | |
| <span data-ttu-id="3899a-225">*Emissor do token*</span><span class="sxs-lookup"><span data-stu-id="3899a-225">*Token Issuer*</span></span> | |

## <a name="technical-profiles"></a><span data-ttu-id="3899a-226">Perfis técnicos</span><span class="sxs-lookup"><span data-stu-id="3899a-226">Technical profiles</span></span>

<span data-ttu-id="3899a-227">Esta seção descreve perfis de técnicas Olá já declarados por provedor de declarações no hello *B2C_1A_base* política.</span><span class="sxs-lookup"><span data-stu-id="3899a-227">This section depicts hello technical profiles already declared per claim provider in hello *B2C_1A_base* policy.</span></span> <span data-ttu-id="3899a-228">Esses perfis técnicas são suscetível toobe mais referenciado, substituída, e/ou estendida conforme necessário em suas próprias políticas, bem como Olá *B2C_1A_base_extensions* política.</span><span class="sxs-lookup"><span data-stu-id="3899a-228">These technical profiles are susceptible toobe further referenced, overridden, and/or extended as needed in your own policies as well as in hello *B2C_1A_base_extensions* policy.</span></span>

### <a name="technical-profiles-for-facebook"></a><span data-ttu-id="3899a-229">Perfis técnicos para o Facebook</span><span class="sxs-lookup"><span data-stu-id="3899a-229">Technical profiles for Facebook</span></span>

| <span data-ttu-id="3899a-230">Perfil técnico</span><span class="sxs-lookup"><span data-stu-id="3899a-230">Technical profile</span></span> | <span data-ttu-id="3899a-231">Descrição</span><span class="sxs-lookup"><span data-stu-id="3899a-231">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="3899a-232">*OAUTH do Facebook*</span><span class="sxs-lookup"><span data-stu-id="3899a-232">*Facebook-OAUTH*</span></span> | |

### <a name="technical-profiles-for-local-account-signin"></a><span data-ttu-id="3899a-233">Perfis técnicos para entrada de conta Local</span><span class="sxs-lookup"><span data-stu-id="3899a-233">Technical profiles for Local Account Signin</span></span>

| <span data-ttu-id="3899a-234">Perfil técnico</span><span class="sxs-lookup"><span data-stu-id="3899a-234">Technical profile</span></span> | <span data-ttu-id="3899a-235">Descrição</span><span class="sxs-lookup"><span data-stu-id="3899a-235">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="3899a-236">*Login-NonInteractive*</span><span class="sxs-lookup"><span data-stu-id="3899a-236">*Login-NonInteractive*</span></span> | |

### <a name="technical-profiles-for-phone-factor"></a><span data-ttu-id="3899a-237">Perfis técnicos de Phone Factor</span><span class="sxs-lookup"><span data-stu-id="3899a-237">Technical profiles for Phone Factor</span></span>

| <span data-ttu-id="3899a-238">Perfil técnico</span><span class="sxs-lookup"><span data-stu-id="3899a-238">Technical profile</span></span> | <span data-ttu-id="3899a-239">Descrição</span><span class="sxs-lookup"><span data-stu-id="3899a-239">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="3899a-240">*PhoneFactor-Input*</span><span class="sxs-lookup"><span data-stu-id="3899a-240">*PhoneFactor-Input*</span></span> | |
| <span data-ttu-id="3899a-241">*PhoneFactor-InputOrVerify*</span><span class="sxs-lookup"><span data-stu-id="3899a-241">*PhoneFactor-InputOrVerify*</span></span> | |
| <span data-ttu-id="3899a-242">*PhoneFactor-Verify*</span><span class="sxs-lookup"><span data-stu-id="3899a-242">*PhoneFactor-Verify*</span></span> | |

### <a name="technical-profiles-for-azure-active-directory"></a><span data-ttu-id="3899a-243">Perfis técnicos para Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3899a-243">Technical profiles for Azure Active Directory</span></span>

| <span data-ttu-id="3899a-244">Perfil técnico</span><span class="sxs-lookup"><span data-stu-id="3899a-244">Technical profile</span></span> | <span data-ttu-id="3899a-245">Descrição</span><span class="sxs-lookup"><span data-stu-id="3899a-245">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="3899a-246">*AAD-Common*</span><span class="sxs-lookup"><span data-stu-id="3899a-246">*AAD-Common*</span></span> | <span data-ttu-id="3899a-247">Perfil técnico incluído por Olá outros perfis técnicos AAD xxx</span><span class="sxs-lookup"><span data-stu-id="3899a-247">Technical profile included by hello other AAD-xxx technical profiles</span></span> |
| <span data-ttu-id="3899a-248">*AAD-UserWriteUsingAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="3899a-248">*AAD-UserWriteUsingAlternativeSecurityId*</span></span> | <span data-ttu-id="3899a-249">Perfil técnico para logons sociais</span><span class="sxs-lookup"><span data-stu-id="3899a-249">Technical profile for social logins</span></span> |
| <span data-ttu-id="3899a-250">*AAD-UserReadUsingAlternativeSecurityId*</span><span class="sxs-lookup"><span data-stu-id="3899a-250">*AAD-UserReadUsingAlternativeSecurityId*</span></span> | <span data-ttu-id="3899a-251">Perfil técnico para logons sociais</span><span class="sxs-lookup"><span data-stu-id="3899a-251">Technical profile for social logins</span></span> |
| <span data-ttu-id="3899a-252">*AAD-UserReadUsingAlternativeSecurityId-NoError*</span><span class="sxs-lookup"><span data-stu-id="3899a-252">*AAD-UserReadUsingAlternativeSecurityId-NoError*</span></span> | <span data-ttu-id="3899a-253">Perfil técnico para logons sociais</span><span class="sxs-lookup"><span data-stu-id="3899a-253">Technical profile for social logins</span></span> |
| <span data-ttu-id="3899a-254">*AAD-UserWritePasswordUsingLogonEmail*</span><span class="sxs-lookup"><span data-stu-id="3899a-254">*AAD-UserWritePasswordUsingLogonEmail*</span></span> | <span data-ttu-id="3899a-255">Perfil técnico para contas locais</span><span class="sxs-lookup"><span data-stu-id="3899a-255">Technical profile for local accounts</span></span> |
| <span data-ttu-id="3899a-256">*AAD-UserReadUsingEmailAddress*</span><span class="sxs-lookup"><span data-stu-id="3899a-256">*AAD-UserReadUsingEmailAddress*</span></span> | <span data-ttu-id="3899a-257">Perfil técnico para contas locais</span><span class="sxs-lookup"><span data-stu-id="3899a-257">Technical profile for local accounts</span></span> |
| <span data-ttu-id="3899a-258">*AAD-UserWriteProfileUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="3899a-258">*AAD-UserWriteProfileUsingObjectId*</span></span> | <span data-ttu-id="3899a-259">Perfil técnico para atualizar o registro de usuário usando o objectId</span><span class="sxs-lookup"><span data-stu-id="3899a-259">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="3899a-260">*AAD-UserWritePhoneNumberUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="3899a-260">*AAD-UserWritePhoneNumberUsingObjectId*</span></span> | <span data-ttu-id="3899a-261">Perfil técnico para atualizar o registro de usuário usando o objectId</span><span class="sxs-lookup"><span data-stu-id="3899a-261">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="3899a-262">*AAD-UserWritePasswordUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="3899a-262">*AAD-UserWritePasswordUsingObjectId*</span></span> | <span data-ttu-id="3899a-263">Perfil técnico para atualizar o registro de usuário usando o objectId</span><span class="sxs-lookup"><span data-stu-id="3899a-263">Technical profile for updating user record using objectId</span></span> |
| <span data-ttu-id="3899a-264">*AAD-UserReadUsingObjectId*</span><span class="sxs-lookup"><span data-stu-id="3899a-264">*AAD-UserReadUsingObjectId*</span></span> | <span data-ttu-id="3899a-265">Perfil técnica é usada tooread dados após a autenticação do usuário</span><span class="sxs-lookup"><span data-stu-id="3899a-265">Technical profile is used tooread data after user authenticates</span></span> |

### <a name="technical-profiles-for-self-asserted"></a><span data-ttu-id="3899a-266">Perfis técnicos para autodeclarados</span><span class="sxs-lookup"><span data-stu-id="3899a-266">Technical profiles for Self Asserted</span></span>

| <span data-ttu-id="3899a-267">Perfil técnico</span><span class="sxs-lookup"><span data-stu-id="3899a-267">Technical profile</span></span> | <span data-ttu-id="3899a-268">Descrição</span><span class="sxs-lookup"><span data-stu-id="3899a-268">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="3899a-269">*SelfAsserted-Social*</span><span class="sxs-lookup"><span data-stu-id="3899a-269">*SelfAsserted-Social*</span></span> | |
| <span data-ttu-id="3899a-270">*SelfAsserted-ProfileUpdate*</span><span class="sxs-lookup"><span data-stu-id="3899a-270">*SelfAsserted-ProfileUpdate*</span></span> | |

### <a name="technical-profiles-for-local-account"></a><span data-ttu-id="3899a-271">Perfis técnicos para conta local</span><span class="sxs-lookup"><span data-stu-id="3899a-271">Technical profiles for Local Account</span></span>

| <span data-ttu-id="3899a-272">Perfil técnico</span><span class="sxs-lookup"><span data-stu-id="3899a-272">Technical profile</span></span> | <span data-ttu-id="3899a-273">Descrição</span><span class="sxs-lookup"><span data-stu-id="3899a-273">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="3899a-274">*LocalAccountSignUpWithLogonEmail*</span><span class="sxs-lookup"><span data-stu-id="3899a-274">*LocalAccountSignUpWithLogonEmail*</span></span> | |

### <a name="technical-profiles-for-session-management"></a><span data-ttu-id="3899a-275">Perfis técnicos de gerenciamento de sessão</span><span class="sxs-lookup"><span data-stu-id="3899a-275">Technical profiles for Session Management</span></span>

| <span data-ttu-id="3899a-276">Perfil técnico</span><span class="sxs-lookup"><span data-stu-id="3899a-276">Technical profile</span></span> | <span data-ttu-id="3899a-277">Descrição</span><span class="sxs-lookup"><span data-stu-id="3899a-277">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="3899a-278">*SM-Noop*</span><span class="sxs-lookup"><span data-stu-id="3899a-278">*SM-Noop*</span></span> | |
| <span data-ttu-id="3899a-279">*SM-AAD*</span><span class="sxs-lookup"><span data-stu-id="3899a-279">*SM-AAD*</span></span> | |
| <span data-ttu-id="3899a-280">*SM-SocialSignup*</span><span class="sxs-lookup"><span data-stu-id="3899a-280">*SM-SocialSignup*</span></span> | <span data-ttu-id="3899a-281">Nome do perfil está sendo usado toodisambiguate AAD sessão entre o sinal de backup e entrar</span><span class="sxs-lookup"><span data-stu-id="3899a-281">Profile name is being used toodisambiguate AAD session between sign up and sign in</span></span> |
| <span data-ttu-id="3899a-282">*SM-SocialLogin*</span><span class="sxs-lookup"><span data-stu-id="3899a-282">*SM-SocialLogin*</span></span> | |
| <span data-ttu-id="3899a-283">*SM-MFA*</span><span class="sxs-lookup"><span data-stu-id="3899a-283">*SM-MFA*</span></span> | |

### <a name="technical-profiles-for-trustframework-policy-engine-technicalprofiles"></a><span data-ttu-id="3899a-284">Perfis técnicos para TechnicalProfiles do mecanismo da política do Trustframework</span><span class="sxs-lookup"><span data-stu-id="3899a-284">Technical profiles for Trustframework Policy Engine TechnicalProfiles</span></span>

<span data-ttu-id="3899a-285">No momento, não há perfis de técnicos são definidos para Olá **TechnicalProfiles de mecanismo de política Trustframework** provedor de declarações.</span><span class="sxs-lookup"><span data-stu-id="3899a-285">Currently, no technical profiles are defined for hello **Trustframework Policy Engine TechnicalProfiles** claims provider.</span></span>

### <a name="technical-profiles-for-token-issuer"></a><span data-ttu-id="3899a-286">Perfis técnicos de emissor do Token</span><span class="sxs-lookup"><span data-stu-id="3899a-286">Technical profiles for Token Issuer</span></span>

| <span data-ttu-id="3899a-287">Perfil técnico</span><span class="sxs-lookup"><span data-stu-id="3899a-287">Technical profile</span></span> | <span data-ttu-id="3899a-288">Descrição</span><span class="sxs-lookup"><span data-stu-id="3899a-288">Description</span></span> |
|-------------------|-------------|
| <span data-ttu-id="3899a-289">*JwtIssuer*</span><span class="sxs-lookup"><span data-stu-id="3899a-289">*JwtIssuer*</span></span> | |

## <a name="user-journeys"></a><span data-ttu-id="3899a-290">Percursos do usuário</span><span class="sxs-lookup"><span data-stu-id="3899a-290">User journeys</span></span>

<span data-ttu-id="3899a-291">Esta seção descreve Jornadas de usuário Olá já declaradas no hello *B2C_1A_base* política.</span><span class="sxs-lookup"><span data-stu-id="3899a-291">This section depicts hello user journeys already declared in hello *B2C_1A_base* policy.</span></span> <span data-ttu-id="3899a-292">Esses Jornadas de usuário são suscetível toobe mais referenciado, substituída, e/ou estendida conforme necessário em suas próprias políticas, bem como Olá *B2C_1A_base_extensions* política.</span><span class="sxs-lookup"><span data-stu-id="3899a-292">These user journeys are susceptible toobe further referenced, overridden, and/or extended as needed in your own policies as well as in hello *B2C_1A_base_extensions* policy.</span></span>

| <span data-ttu-id="3899a-293">Percurso do usuário</span><span class="sxs-lookup"><span data-stu-id="3899a-293">User journey</span></span> | <span data-ttu-id="3899a-294">Descrição</span><span class="sxs-lookup"><span data-stu-id="3899a-294">Description</span></span> |
|--------------|-------------|
| <span data-ttu-id="3899a-295">*SignUp*</span><span class="sxs-lookup"><span data-stu-id="3899a-295">*SignUp*</span></span> | |
| <span data-ttu-id="3899a-296">*SignIn*</span><span class="sxs-lookup"><span data-stu-id="3899a-296">*SignIn*</span></span> | |
| <span data-ttu-id="3899a-297">*SignUpOrSignIn*</span><span class="sxs-lookup"><span data-stu-id="3899a-297">*SignUpOrSignIn*</span></span> | |
| <span data-ttu-id="3899a-298">*EditProfile*</span><span class="sxs-lookup"><span data-stu-id="3899a-298">*EditProfile*</span></span> | |
| <span data-ttu-id="3899a-299">*PasswordReset*</span><span class="sxs-lookup"><span data-stu-id="3899a-299">*PasswordReset*</span></span> | |
