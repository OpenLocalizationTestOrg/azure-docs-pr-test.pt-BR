---
title: "Azure Active Directory B2C: políticas internas | Microsoft Docs"
description: "Um tópico sobre a estrutura de política extensível do Active Directory B2C do Azure e como criar vários tipos de política"
services: active-directory-b2c
documentationcenter: 
author: sama
manager: mbaldwin
editor: PatAltimore
ms.assetid: 0d453e72-7f70-4aa2-953d-938d2814d5a9
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: sama
ms.openlocfilehash: daad3af089afdf76b930053728bb11a5cf4c2a92
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-built-in-policies"></a><span data-ttu-id="9e0b1-103">Azure Active Directory B2C: políticas internas</span><span class="sxs-lookup"><span data-stu-id="9e0b1-103">Azure Active Directory B2C: Built-in policies</span></span>


<span data-ttu-id="9e0b1-104">A estrutura de política extensível do Azure AD (Azure Active Directory) B2C é o principal ponto forte do serviço.</span><span class="sxs-lookup"><span data-stu-id="9e0b1-104">The extensible policy framework of Azure Active Directory (Azure AD) B2C is the core strength of the service.</span></span> <span data-ttu-id="9e0b1-105">As políticas descrevem totalmente as experiências de identidade do consumidor, como inscrição, entrada ou edição de perfil.</span><span class="sxs-lookup"><span data-stu-id="9e0b1-105">Policies fully describe consumer identity experiences such as sign-up, sign-in, or profile editing.</span></span> <span data-ttu-id="9e0b1-106">Por exemplo, uma política de inscrição permite controlar comportamentos definindo as seguintes configurações:</span><span class="sxs-lookup"><span data-stu-id="9e0b1-106">For instance, a sign-up policy allows you to control behaviors by configuring the following settings:</span></span>

* <span data-ttu-id="9e0b1-107">Tipos de conta (contas sociais, como o Facebook ou contas locais, como um endereço de email) que os consumidores podem usar para se inscrever no aplicativo</span><span class="sxs-lookup"><span data-stu-id="9e0b1-107">Account types (social accounts such as Facebook or local accounts such as email addresses) that consumers can use to sign up for the application</span></span>
* <span data-ttu-id="9e0b1-108">Atributos (como nome, código postal e tamanho do calçado, por exemplo) que serão coletados junto ao consumidor durante a inscrição</span><span class="sxs-lookup"><span data-stu-id="9e0b1-108">Attributes (for example, first name, postal code, and shoe size) to be collected from the consumer during sign-up</span></span>
* <span data-ttu-id="9e0b1-109">Uso da Autenticação Multifator do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="9e0b1-109">Use of Azure Multi-Factor Authentication</span></span>
* <span data-ttu-id="9e0b1-110">A aparência e funcionalidade de todas as páginas de inscrição</span><span class="sxs-lookup"><span data-stu-id="9e0b1-110">The look and feel of all sign-up pages</span></span>
* <span data-ttu-id="9e0b1-111">Informações (que se manifestam como declarações em um token) que o aplicativo recebe quando a execução da política é concluída</span><span class="sxs-lookup"><span data-stu-id="9e0b1-111">Information (which manifests as claims in a token) that the application receives when the policy run finishes</span></span>

<span data-ttu-id="9e0b1-112">Você pode criar várias políticas de tipos diferentes em seu locatário e usá-las em seus aplicativos, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="9e0b1-112">You can create multiple policies of different types in your tenant and use them in your applications as needed.</span></span> <span data-ttu-id="9e0b1-113">As políticas podem ser reutilizadas entre os aplicativos.</span><span class="sxs-lookup"><span data-stu-id="9e0b1-113">Policies can be reused across applications.</span></span> <span data-ttu-id="9e0b1-114">Essa flexibilidade permite aos desenvolvedores definir e modificar experiências de identidade do consumidor com pouca ou nenhuma alteração no código.</span><span class="sxs-lookup"><span data-stu-id="9e0b1-114">This flexibility enables developers to define and modify consumer identity experiences with minimal or no changes to their code.</span></span>

<span data-ttu-id="9e0b1-115">As políticas estão disponíveis para uso por meio de uma interface simples do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="9e0b1-115">Policies are available for use via a simple developer interface.</span></span> <span data-ttu-id="9e0b1-116">O aplicativo dispara uma política usando uma solicitação de autenticação HTTP padrão (passando um parâmetro de política na solicitação) e recebe um token personalizado como resposta.</span><span class="sxs-lookup"><span data-stu-id="9e0b1-116">Your application triggers a policy by using a standard HTTP authentication request (passing a policy parameter in the request) and receives a customized token as response.</span></span> <span data-ttu-id="9e0b1-117">Por exemplo, a única diferença entre solicitações que invocam uma política de inscrição e aquelas que invocam uma política de entrada é o nome da política usado no parâmetro de cadeia de caracteres de consulta "p":</span><span class="sxs-lookup"><span data-stu-id="9e0b1-117">For example, the only difference between requests that invoke a sign-up policy and requests that invoke a sign-in policy is the policy name that's used in the "p" query string parameter:</span></span>

```

https://login.microsoftonline.com/contosob2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e      // Your registered Application ID
&redirect_uri=https%3A%2F%2Flocalhost%3A44321%2F    // Your registered Reply URL, url encoded
&response_mode=form_post                            // 'query', 'form_post' or 'fragment'
&response_type=id_token
&scope=openid
&nonce=dummy
&state=12345                                        // Any value provided by your application
&p=b2c_1_siup                                       // Your sign-up policy

```

```

https://login.microsoftonline.com/contosob2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e      // Your registered Application ID
&redirect_uri=https%3A%2F%2Flocalhost%3A44321%2F    // Your registered Reply URL, url encoded
&response_mode=form_post                            // 'query', 'form_post' or 'fragment'
&response_type=id_token
&scope=openid
&nonce=dummy
&state=12345                                        // Any value provided by your application
&p=b2c_1_siin                                       // Your sign-in policy

```

<span data-ttu-id="9e0b1-118">Para obter mais informações sobre a estrutura das políticas, consulte [Esta postagem de blog sobre o Azure AD B2C no Blog do Enterprise Mobility and Security](http://blogs.technet.com/b/ad/archive/2015/11/02/a-look-inside-azuread-b2c-with-kim-cameron.aspx).</span><span class="sxs-lookup"><span data-stu-id="9e0b1-118">For more information about the policy framework, see [this blog post about Azure AD B2C on the Enterprise Mobility and Security Blog](http://blogs.technet.com/b/ad/archive/2015/11/02/a-look-inside-azuread-b2c-with-kim-cameron.aspx).</span></span>

## <a name="create-a-sign-up-or-sign-in-policy"></a><span data-ttu-id="9e0b1-119">Criar uma política de inscrição ou credenciais</span><span class="sxs-lookup"><span data-stu-id="9e0b1-119">Create a sign-up or sign-in policy</span></span>

<span data-ttu-id="9e0b1-120">Esta política controla as duas experiências de inscrição e credenciais do consumidor com uma única configuração.</span><span class="sxs-lookup"><span data-stu-id="9e0b1-120">This policy handles both consumer sign-up & sign-in experiences with a single configuration.</span></span> <span data-ttu-id="9e0b1-121">Os consumidores são conduzidos para o caminho certo (inscrição ou credenciais), dependendo do contexto.</span><span class="sxs-lookup"><span data-stu-id="9e0b1-121">Consumers are led down the right path (sign-up or sign-in) depending on the context.</span></span> <span data-ttu-id="9e0b1-122">Ele também descreve o conteúdo de tokens que o aplicativo receberá mediante inscrições ou entradas bem-sucedidas.  Há um exemplo de código para a política de inscrição ou de entrada [disponível aqui](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span><span class="sxs-lookup"><span data-stu-id="9e0b1-122">It also describes the contents of tokens that the application will receive upon successful sign-ups or sign-ins.  A code sample for the sign-up or sign-in policy is [available here](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span>  <span data-ttu-id="9e0b1-123">É recomendável que você use esta política em vez de uma política de inscrição e entrada.</span><span class="sxs-lookup"><span data-stu-id="9e0b1-123">It is recommened that you use this policy over a sign-up policy and sign-in policy.</span></span>  

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

## <a name="create-a-sign-up-policy"></a><span data-ttu-id="9e0b1-124">Criar uma política de inscrição</span><span class="sxs-lookup"><span data-stu-id="9e0b1-124">Create a sign-up policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-up-policy](../../includes/active-directory-b2c-create-sign-up-policy.md)]

## <a name="create-a-sign-in-policy"></a><span data-ttu-id="9e0b1-125">Usar uma política de entrada</span><span class="sxs-lookup"><span data-stu-id="9e0b1-125">Create a sign-in policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-in-policy](../../includes/active-directory-b2c-create-sign-in-policy.md)]

## <a name="create-a-profile-editing-policy"></a><span data-ttu-id="9e0b1-126">Criar uma política de edição de perfil</span><span class="sxs-lookup"><span data-stu-id="9e0b1-126">Create a profile editing policy</span></span>

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

## <a name="create-a-password-reset-policy"></a><span data-ttu-id="9e0b1-127">Criar uma política de redefinição de senha</span><span class="sxs-lookup"><span data-stu-id="9e0b1-127">Create a password reset policy</span></span>

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

## <a name="frequently-asked-questions"></a><span data-ttu-id="9e0b1-128">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="9e0b1-128">Frequently asked questions</span></span>

### <a name="how-do-i-link-a-sign-up-or-sign-in-policy-with-a-password-reset-policy"></a><span data-ttu-id="9e0b1-129">Como fazer para vincular uma política de inscrição ou entrada a uma política de redefinição de senha?</span><span class="sxs-lookup"><span data-stu-id="9e0b1-129">How do I link a sign-up or sign-in policy with a password reset policy?</span></span>
<span data-ttu-id="9e0b1-130">Quando cria uma política de inscrição ou entrada (com contas locais), você vê um link **Esqueceu a senha?** na primeira página da experiência.</span><span class="sxs-lookup"><span data-stu-id="9e0b1-130">When you create a sign-up or sign-in policy (with local accounts), you see a **Forgot password?** link on the first page of the experience.</span></span> <span data-ttu-id="9e0b1-131">Clicar nesse link não dispara automaticamente uma política de redefinição de senha.</span><span class="sxs-lookup"><span data-stu-id="9e0b1-131">Clicking this link doesn't automatically trigger a password reset policy.</span></span> 

<span data-ttu-id="9e0b1-132">Em vez disso, o código de erro **`AADB2C90118`** é retornado para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9e0b1-132">Instead, the error code **`AADB2C90118`** is returned to your app.</span></span> <span data-ttu-id="9e0b1-133">Seu aplicativo precisa lidar com esse código de erro invocando uma política de redefinição de senha específica.</span><span class="sxs-lookup"><span data-stu-id="9e0b1-133">Your app needs to handle this error code by invoking a specific password reset policy.</span></span> <span data-ttu-id="9e0b1-134">Para obter mais informações, consulte um [exemplo que demonstra a abordagem de vinculação de políticas](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-DotNet-SUSI).</span><span class="sxs-lookup"><span data-stu-id="9e0b1-134">For more information, see a [sample that demonstrates the approach of linking policies](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-DotNet-SUSI).</span></span>

### <a name="should-i-use-a-sign-up-or-sign-in-policy-or-a-sign-up-policy-and-a-sign-in-policy"></a><span data-ttu-id="9e0b1-135">Eu devo usar uma política de inscrição ou entrada ou uma política de inscrição e uma política de entrada?</span><span class="sxs-lookup"><span data-stu-id="9e0b1-135">Should I use a sign-up or sign-in policy or a sign-up policy and a sign-in policy?</span></span>
<span data-ttu-id="9e0b1-136">Recomendamos que você use uma política de inscrição ou entrada em vez de usar uma política de inscrição e uma política de entrada.</span><span class="sxs-lookup"><span data-stu-id="9e0b1-136">We recommend that you use a sign-up or sign-in policy over a sign-up policy and a sign-in policy.</span></span>  

<span data-ttu-id="9e0b1-137">A política de inscrição ou entrada tem mais recursos do que a política de entrada.</span><span class="sxs-lookup"><span data-stu-id="9e0b1-137">The sign-up or sign-in policy has more capabilities than the sign-in policy.</span></span> <span data-ttu-id="9e0b1-138">Ela também permite que você use a personalização da interface do usuário da página e tem melhor suporte para localização.</span><span class="sxs-lookup"><span data-stu-id="9e0b1-138">It also enables you to use page UI customization and has better support for localization.</span></span> 

<span data-ttu-id="9e0b1-139">A política de entrada é recomendada se você não precisar localizar suas políticas, precisar apenas de recursos de personalização secundários para a identidade visual e quiser a redefinição de senha embutida.</span><span class="sxs-lookup"><span data-stu-id="9e0b1-139">The sign-in policy is recommended if you don't need to localize your policies, only need minor customization capabilities for branding, and want password reset built into it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e0b1-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9e0b1-140">Next steps</span></span>
* [<span data-ttu-id="9e0b1-141">Configuração de token, de sessão e de logon único</span><span class="sxs-lookup"><span data-stu-id="9e0b1-141">Token, session, and single sign-on configuration</span></span>](active-directory-b2c-token-session-sso.md)
* [<span data-ttu-id="9e0b1-142">Desabilitar a verificação de email durante a inscrição do consumidor</span><span class="sxs-lookup"><span data-stu-id="9e0b1-142">Disable email verification during consumer sign-up</span></span>](active-directory-b2c-reference-disable-ev.md)

