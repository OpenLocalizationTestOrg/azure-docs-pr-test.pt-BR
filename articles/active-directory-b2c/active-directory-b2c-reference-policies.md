---
title: "Azure Active Directory B2C: políticas internas | Microsoft Docs"
description: "Um tópico em estrutura da política extensível saudação do Azure Active Directory B2C e como toocreate vários tipos de política"
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
ms.openlocfilehash: 24bb85eba30f888c6ea7d0401e05235e8eb6ea79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-built-in-policies"></a><span data-ttu-id="82b80-103">Azure Active Directory B2C: políticas internas</span><span class="sxs-lookup"><span data-stu-id="82b80-103">Azure Active Directory B2C: Built-in policies</span></span>


<span data-ttu-id="82b80-104">estrutura da política extensível saudação do B2C do Azure Active Directory (AD do Azure) é a intensidade de núcleo saudação do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="82b80-104">hello extensible policy framework of Azure Active Directory (Azure AD) B2C is hello core strength of hello service.</span></span> <span data-ttu-id="82b80-105">As políticas descrevem totalmente as experiências de identidade do consumidor, como inscrição, entrada ou edição de perfil.</span><span class="sxs-lookup"><span data-stu-id="82b80-105">Policies fully describe consumer identity experiences such as sign-up, sign-in, or profile editing.</span></span> <span data-ttu-id="82b80-106">Por exemplo, uma política de inscrição permite que você toocontrol comportamentos Configurando Olá configurações a seguir:</span><span class="sxs-lookup"><span data-stu-id="82b80-106">For instance, a sign-up policy allows you toocontrol behaviors by configuring hello following settings:</span></span>

* <span data-ttu-id="82b80-107">Tipos (contas sociais, como Facebook) ou local, como endereços de email que os consumidores podem utilizar toosign para o aplicativo hello de conta</span><span class="sxs-lookup"><span data-stu-id="82b80-107">Account types (social accounts such as Facebook or local accounts such as email addresses) that consumers can use toosign up for hello application</span></span>
* <span data-ttu-id="82b80-108">Atributos (por exemplo, nome, código postal e tamanho de sapato) toobe coletados de consumidor Olá durante a inscrição</span><span class="sxs-lookup"><span data-stu-id="82b80-108">Attributes (for example, first name, postal code, and shoe size) toobe collected from hello consumer during sign-up</span></span>
* <span data-ttu-id="82b80-109">Uso da Autenticação Multifator do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="82b80-109">Use of Azure Multi-Factor Authentication</span></span>
* <span data-ttu-id="82b80-110">Olá aparência de todas as páginas de inscrição</span><span class="sxs-lookup"><span data-stu-id="82b80-110">hello look and feel of all sign-up pages</span></span>
* <span data-ttu-id="82b80-111">Informações (que se manifesta como declarações em um token) Olá aplicativo recebe quando termina de execução da diretiva Olá</span><span class="sxs-lookup"><span data-stu-id="82b80-111">Information (which manifests as claims in a token) that hello application receives when hello policy run finishes</span></span>

<span data-ttu-id="82b80-112">Você pode criar várias políticas de tipos diferentes em seu locatário e usá-las em seus aplicativos, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="82b80-112">You can create multiple policies of different types in your tenant and use them in your applications as needed.</span></span> <span data-ttu-id="82b80-113">As políticas podem ser reutilizadas entre os aplicativos.</span><span class="sxs-lookup"><span data-stu-id="82b80-113">Policies can be reused across applications.</span></span> <span data-ttu-id="82b80-114">Essa flexibilidade permite que os desenvolvedores toodefine e modificar as experiências de identidade do consumidor com pouca ou nenhuma tootheir altera o código.</span><span class="sxs-lookup"><span data-stu-id="82b80-114">This flexibility enables developers toodefine and modify consumer identity experiences with minimal or no changes tootheir code.</span></span>

<span data-ttu-id="82b80-115">As políticas estão disponíveis para uso por meio de uma interface simples do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="82b80-115">Policies are available for use via a simple developer interface.</span></span> <span data-ttu-id="82b80-116">O aplicativo dispara uma política usando uma solicitação de autenticação HTTP padrão (passando um parâmetro de política na solicitação de saudação) e recebe um token personalizado como resposta.</span><span class="sxs-lookup"><span data-stu-id="82b80-116">Your application triggers a policy by using a standard HTTP authentication request (passing a policy parameter in hello request) and receives a customized token as response.</span></span> <span data-ttu-id="82b80-117">Por exemplo, Olá única diferença entre solicitações invocar uma política de inscrição e as que invocam uma política de entrada é usada no parâmetro de cadeia de caracteres de consulta hello "p" nome da política hello:</span><span class="sxs-lookup"><span data-stu-id="82b80-117">For example, hello only difference between requests that invoke a sign-up policy and requests that invoke a sign-in policy is hello policy name that's used in hello "p" query string parameter:</span></span>

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

<span data-ttu-id="82b80-118">Para obter mais informações sobre a estrutura da política hello, consulte [esta postagem de blog sobre o Blog de segurança e o Azure AD B2C em Olá Enterprise Mobility](http://blogs.technet.com/b/ad/archive/2015/11/02/a-look-inside-azuread-b2c-with-kim-cameron.aspx).</span><span class="sxs-lookup"><span data-stu-id="82b80-118">For more information about hello policy framework, see [this blog post about Azure AD B2C on hello Enterprise Mobility and Security Blog](http://blogs.technet.com/b/ad/archive/2015/11/02/a-look-inside-azuread-b2c-with-kim-cameron.aspx).</span></span>

## <a name="create-a-sign-up-or-sign-in-policy"></a><span data-ttu-id="82b80-119">Criar uma política de inscrição ou credenciais</span><span class="sxs-lookup"><span data-stu-id="82b80-119">Create a sign-up or sign-in policy</span></span>

<span data-ttu-id="82b80-120">Esta política controla as duas experiências de inscrição e credenciais do consumidor com uma única configuração.</span><span class="sxs-lookup"><span data-stu-id="82b80-120">This policy handles both consumer sign-up & sign-in experiences with a single configuration.</span></span> <span data-ttu-id="82b80-121">Os consumidores são led Olá direita caminho (inscrever ou entrar) dependendo do contexto de saudação.</span><span class="sxs-lookup"><span data-stu-id="82b80-121">Consumers are led down hello right path (sign-up or sign-in) depending on hello context.</span></span> <span data-ttu-id="82b80-122">Ele também descreve o conteúdo de saudação de tokens que o aplicativo hello receberá inscrições bem-sucedida ou entradas.  É um exemplo de código para política de inscrever-se ou entrar Olá [disponível aqui](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span><span class="sxs-lookup"><span data-stu-id="82b80-122">It also describes hello contents of tokens that hello application will receive upon successful sign-ups or sign-ins.  A code sample for hello sign-up or sign-in policy is [available here](active-directory-b2c-devquickstarts-web-dotnet-susi.md).</span></span>  <span data-ttu-id="82b80-123">É recomendável que você use esta política em vez de uma política de inscrição e entrada.</span><span class="sxs-lookup"><span data-stu-id="82b80-123">It is recommened that you use this policy over a sign-up policy and sign-in policy.</span></span>  

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

## <a name="create-a-sign-up-policy"></a><span data-ttu-id="82b80-124">Criar uma política de inscrição</span><span class="sxs-lookup"><span data-stu-id="82b80-124">Create a sign-up policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-up-policy](../../includes/active-directory-b2c-create-sign-up-policy.md)]

## <a name="create-a-sign-in-policy"></a><span data-ttu-id="82b80-125">Usar uma política de entrada</span><span class="sxs-lookup"><span data-stu-id="82b80-125">Create a sign-in policy</span></span>

[!INCLUDE [active-directory-b2c-create-sign-in-policy](../../includes/active-directory-b2c-create-sign-in-policy.md)]

## <a name="create-a-profile-editing-policy"></a><span data-ttu-id="82b80-126">Criar uma política de edição de perfil</span><span class="sxs-lookup"><span data-stu-id="82b80-126">Create a profile editing policy</span></span>

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

## <a name="create-a-password-reset-policy"></a><span data-ttu-id="82b80-127">Criar uma política de redefinição de senha</span><span class="sxs-lookup"><span data-stu-id="82b80-127">Create a password reset policy</span></span>

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

## <a name="frequently-asked-questions"></a><span data-ttu-id="82b80-128">Perguntas frequentes</span><span class="sxs-lookup"><span data-stu-id="82b80-128">Frequently asked questions</span></span>

### <a name="how-do-i-link-a-sign-up-or-sign-in-policy-with-a-password-reset-policy"></a><span data-ttu-id="82b80-129">Como fazer para vincular uma política de inscrição ou entrada a uma política de redefinição de senha?</span><span class="sxs-lookup"><span data-stu-id="82b80-129">How do I link a sign-up or sign-in policy with a password reset policy?</span></span>
<span data-ttu-id="82b80-130">Quando você cria uma política de inscrever-se ou entrar (com contas locais), você verá um **senha Esqueceu?** link na primeira página Olá da experiência de saudação.</span><span class="sxs-lookup"><span data-stu-id="82b80-130">When you create a sign-up or sign-in policy (with local accounts), you see a **Forgot password?** link on hello first page of hello experience.</span></span> <span data-ttu-id="82b80-131">Clicar nesse link não dispara automaticamente uma política de redefinição de senha.</span><span class="sxs-lookup"><span data-stu-id="82b80-131">Clicking this link doesn't automatically trigger a password reset policy.</span></span> 

<span data-ttu-id="82b80-132">Olá em vez disso, o código de erro  **`AADB2C90118`**  é retornado tooyour aplicativo.</span><span class="sxs-lookup"><span data-stu-id="82b80-132">Instead, hello error code **`AADB2C90118`** is returned tooyour app.</span></span> <span data-ttu-id="82b80-133">Seu aplicativo precisa toohandle esse código de erro com a invocação de uma política de redefinição de senha específica.</span><span class="sxs-lookup"><span data-stu-id="82b80-133">Your app needs toohandle this error code by invoking a specific password reset policy.</span></span> <span data-ttu-id="82b80-134">Para obter mais informações, consulte um [exemplo que demonstra a abordagem de saudação de vinculação políticas](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-DotNet-SUSI).</span><span class="sxs-lookup"><span data-stu-id="82b80-134">For more information, see a [sample that demonstrates hello approach of linking policies](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-DotNet-SUSI).</span></span>

### <a name="should-i-use-a-sign-up-or-sign-in-policy-or-a-sign-up-policy-and-a-sign-in-policy"></a><span data-ttu-id="82b80-135">Eu devo usar uma política de inscrição ou entrada ou uma política de inscrição e uma política de entrada?</span><span class="sxs-lookup"><span data-stu-id="82b80-135">Should I use a sign-up or sign-in policy or a sign-up policy and a sign-in policy?</span></span>
<span data-ttu-id="82b80-136">Recomendamos que você use uma política de inscrição ou entrada em vez de usar uma política de inscrição e uma política de entrada.</span><span class="sxs-lookup"><span data-stu-id="82b80-136">We recommend that you use a sign-up or sign-in policy over a sign-up policy and a sign-in policy.</span></span>  

<span data-ttu-id="82b80-137">política de inscrever-se ou entrar Olá tem mais recursos do que a política de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="82b80-137">hello sign-up or sign-in policy has more capabilities than hello sign-in policy.</span></span> <span data-ttu-id="82b80-138">Também permite a personalização da interface do usuário toouse página e tem um melhor suporte para localização.</span><span class="sxs-lookup"><span data-stu-id="82b80-138">It also enables you toouse page UI customization and has better support for localization.</span></span> 

<span data-ttu-id="82b80-139">Olá entrar diretiva é recomendada se você não precisa toolocalize suas políticas, só precisa de recursos de personalização secundárias para a identidade visual e deseja senha redefinição embutida.</span><span class="sxs-lookup"><span data-stu-id="82b80-139">hello sign-in policy is recommended if you don't need toolocalize your policies, only need minor customization capabilities for branding, and want password reset built into it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="82b80-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="82b80-140">Next steps</span></span>
* [<span data-ttu-id="82b80-141">Configuração de token, de sessão e de logon único</span><span class="sxs-lookup"><span data-stu-id="82b80-141">Token, session, and single sign-on configuration</span></span>](active-directory-b2c-token-session-sso.md)
* [<span data-ttu-id="82b80-142">Desabilitar a verificação de email durante a inscrição do consumidor</span><span class="sxs-lookup"><span data-stu-id="82b80-142">Disable email verification during consumer sign-up</span></span>](active-directory-b2c-reference-disable-ev.md)

