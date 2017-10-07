---
title: aaaHow tooenable SSO entre aplicativo no Android usando o ADAL | Microsoft Docs
description: "Como toouse recursos de saudação do hello tooenable SDK ADAL logon único em seus aplicativos. "
services: active-directory
documentationcenter: 
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: 40710225-05ab-40a3-9aec-8b4e96b6b5e7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: android
ms.devlang: java
ms.topic: article
ms.date: 04/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 3867e15030e5516464e4dbd92ba35894430daf00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooenable-cross-app-sso-on-android-using-adal"></a><span data-ttu-id="43be1-103">Como tooenable SSO entre aplicativo no Android usando o ADAL</span><span class="sxs-lookup"><span data-stu-id="43be1-103">How tooenable cross-app SSO on Android using ADAL</span></span>
<span data-ttu-id="43be1-104">Fornecer Single Sign-On (SSO) para que usuários só precisam tooenter suas credenciais de uma vez e tem as credenciais de trabalho automaticamente em todos os aplicativos agora é esperado por clientes.</span><span class="sxs-lookup"><span data-stu-id="43be1-104">Providing Single Sign-On (SSO) so that users only need tooenter their credentials once and have those credentials automatically work across applications is now expected by customers.</span></span> <span data-ttu-id="43be1-105">Dificuldade de saudação inserir seu nome de usuário e senha em uma tela pequena, geralmente vezes combinados com um fator adicional (2FA) como uma chamada telefônica ou um código enviado por texto, resulta em insatisfação rápida se um usuário tem toodo isso mais de uma vez para o seu produto.</span><span class="sxs-lookup"><span data-stu-id="43be1-105">hello difficulty in entering their username and password on a small screen, often times combined with an additional factor (2FA) like a phone call or a texted code, results in quick dissatisfaction if a user has toodo this more than one time for your product.</span></span>

<span data-ttu-id="43be1-106">Além disso, se você aplicar uma plataforma de identidade que outros aplicativos podem usar como Accounts da Microsoft ou uma conta de trabalho do Office 365, os clientes esperam que os toobe de credenciais disponíveis toouse em todos os seus aplicativos não importa fornecedor hello.</span><span class="sxs-lookup"><span data-stu-id="43be1-106">In addition, if you apply an identity platform that other applications may use such as Microsoft Accounts or a work account from Office365, customers expect that those credentials toobe available toouse across all their applications no matter hello vendor.</span></span>

<span data-ttu-id="43be1-107">Olá plataforma do Microsoft Identity, juntamente com nossos SDKs de identidade da Microsoft, tudo isso funciona rígido para você e fornece a você Olá capacidade toodelight seus clientes com o SSO em seu próprio conjunto de aplicativos ou, como com nosso recurso de agente e um autenticador aplicativos, em todo dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="43be1-107">hello Microsoft Identity platform, along with our Microsoft Identity SDKs, does all this hard work for you and gives you hello ability toodelight your customers with SSO either within your own suite of applications or, as with our broker capability and Authenticator applications, across hello entire device.</span></span>

<span data-ttu-id="43be1-108">Este passo a passo mostrará como tooconfigure nossa SDK em seu aplicativo tooprovide clientes de tooyour esse benefício.</span><span class="sxs-lookup"><span data-stu-id="43be1-108">This walkthrough will tell you how tooconfigure our SDK within your application tooprovide this benefit tooyour customers.</span></span>

<span data-ttu-id="43be1-109">Este passo a passo se aplica a:</span><span class="sxs-lookup"><span data-stu-id="43be1-109">This walkthrough applies to:</span></span>

* <span data-ttu-id="43be1-110">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="43be1-110">Azure Active Directory</span></span>
* <span data-ttu-id="43be1-111">Active Directory B2C do Azure</span><span class="sxs-lookup"><span data-stu-id="43be1-111">Azure Active Directory B2C</span></span>
* <span data-ttu-id="43be1-112">Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="43be1-112">Azure Active Directory B2B</span></span>
* <span data-ttu-id="43be1-113">Acesso condicional ao Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="43be1-113">Azure Active Directory Conditional Access</span></span>

<span data-ttu-id="43be1-114">documento de saudação anterior pressupõe que você sabe como muito[provisionar aplicativos no portal herdados de saudação do Azure Active Directory](active-directory-how-to-integrate.md) e seu aplicativo integrado com hello [Microsoft Identity Android SDK](https://github.com/AzureAD/azure-activedirectory-library-for-android) .</span><span class="sxs-lookup"><span data-stu-id="43be1-114">hello document preceding assumes you know how too[provision applications in hello legacy portal for Azure Active Directory](active-directory-how-to-integrate.md) and integrated your application with hello [Microsoft Identity Android SDK](https://github.com/AzureAD/azure-activedirectory-library-for-android).</span></span>

## <a name="sso-concepts-in-hello-microsoft-identity-platform"></a><span data-ttu-id="43be1-115">Conceitos de SSO em Olá plataforma de identidade da Microsoft</span><span class="sxs-lookup"><span data-stu-id="43be1-115">SSO Concepts in hello Microsoft Identity Platform</span></span>
### <a name="microsoft-identity-brokers"></a><span data-ttu-id="43be1-116">Agentes do Microsoft Identity</span><span class="sxs-lookup"><span data-stu-id="43be1-116">Microsoft Identity Brokers</span></span>
<span data-ttu-id="43be1-117">Microsoft oferece aos aplicativos para cada plataforma móvel que permitem Olá ponte de credenciais nos aplicativos de fornecedores diferentes e permite recursos aprimorados especiais que exigem um único local seguro de onde toovalidate credenciais.</span><span class="sxs-lookup"><span data-stu-id="43be1-117">Microsoft provides applications for every mobile platform that allow for hello bridging of credentials across applications from different vendors and allows for special enhanced features that require a single secure place from where toovalidate credentials.</span></span> <span data-ttu-id="43be1-118">Chamamos esses recursos de **agentes**.</span><span class="sxs-lookup"><span data-stu-id="43be1-118">We call these **brokers**.</span></span> <span data-ttu-id="43be1-119">No iOS e Android, eles são fornecidos por meio de aplicativos para download que os clientes instalar independente ou podem ser enviados toohello dispositivo por uma empresa que gerencia alguns ou todos os dispositivos de saudação para seus funcionários.</span><span class="sxs-lookup"><span data-stu-id="43be1-119">On iOS and Android these are provided through downloadable applications that customers either install independently or can be pushed toohello device by a company who manages some or all of hello device for their employee.</span></span> <span data-ttu-id="43be1-120">Esses agentes dão suporte à segurança de gerenciamento apenas para alguns aplicativos ou todo dispositivo de saudação com base no qual os administradores de TI deseja.</span><span class="sxs-lookup"><span data-stu-id="43be1-120">These brokers support managing security just for some applications or hello entire device based on what IT Administrators desire.</span></span> <span data-ttu-id="43be1-121">No Windows, essa funcionalidade é fornecida por um seletor de conta interna do sistema operacional de toohello, tecnicamente conhecido como Olá agente de autenticação da Web.</span><span class="sxs-lookup"><span data-stu-id="43be1-121">In Windows, this functionality is provided by an account chooser built in toohello operating system, known technically as hello Web Authentication Broker.</span></span>

<span data-ttu-id="43be1-122">Para obter mais informações sobre como usamos esses agentes e como os clientes podem vê-los em seu fluxo de logon para a plataforma do Microsoft Identity Olá ler no.</span><span class="sxs-lookup"><span data-stu-id="43be1-122">For more information on how we use these brokers and how your customers might see them in their login flow for hello Microsoft Identity platform read on.</span></span>

### <a name="patterns-for-logging-in-on-mobile-devices"></a><span data-ttu-id="43be1-123">Padrões de logon em dispositivos móveis</span><span class="sxs-lookup"><span data-stu-id="43be1-123">Patterns for logging in on mobile devices</span></span>
<span data-ttu-id="43be1-124">Acesso toocredentials em dispositivos execute dois padrões básicos para a plataforma do Microsoft Identity hello:</span><span class="sxs-lookup"><span data-stu-id="43be1-124">Access toocredentials on devices follow two basic patterns for hello Microsoft Identity platform:</span></span>

* <span data-ttu-id="43be1-125">Logons assistidos por não agentes</span><span class="sxs-lookup"><span data-stu-id="43be1-125">Non-broker assisted logins</span></span>
* <span data-ttu-id="43be1-126">Logons assistidos por agentes</span><span class="sxs-lookup"><span data-stu-id="43be1-126">Broker assisted logins</span></span>

#### <a name="non-broker-assisted-logins"></a><span data-ttu-id="43be1-127">Logons assistidos por não agentes</span><span class="sxs-lookup"><span data-stu-id="43be1-127">Non-broker assisted logins</span></span>
<span data-ttu-id="43be1-128">Logons de agente não assistidos são experiências de logon que ocorrem em linha com o aplicativo hello e usam o armazenamento local de saudação no dispositivo Olá para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="43be1-128">Non-broker assisted logins are login experiences that happen inline with hello application and use hello local storage on hello device for that application.</span></span> <span data-ttu-id="43be1-129">Esse armazenamento pode ser compartilhado entre aplicativos, mas credenciais de saudação estão estreitamente acoplado toohello aplicativo ou pacote de aplicativos que usam essa credencial.</span><span class="sxs-lookup"><span data-stu-id="43be1-129">This storage may be shared across applications but hello credentials are tightly bound toohello app or suite of apps using that credential.</span></span> <span data-ttu-id="43be1-130">Você provavelmente já passou isso em muitos aplicativos móveis quando você inserir um nome de usuário e senha dentro do próprio aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="43be1-130">You've most likely experienced this in many mobile applications when you enter a username and password within hello application itself.</span></span>

<span data-ttu-id="43be1-131">Esses logons têm Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="43be1-131">These logins have hello following benefits:</span></span>

* <span data-ttu-id="43be1-132">Experiência do usuário existe completamente no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="43be1-132">User experience exists entirely within hello application.</span></span>
* <span data-ttu-id="43be1-133">As credenciais podem ser compartilhadas entre aplicativos que são assinados por Olá mesmo certificado, fornecendo um conjunto de tooyour experiência de logon único de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="43be1-133">Credentials can be shared across applications that are signed by hello same certificate, providing a single sign-on experience tooyour suite of applications.</span></span>
* <span data-ttu-id="43be1-134">Controle de experiência de saudação de logon é fornecido toohello aplicativo antes e depois de entrar.</span><span class="sxs-lookup"><span data-stu-id="43be1-134">Control around hello experience of logging in is provided toohello application before and after sign-in.</span></span>

<span data-ttu-id="43be1-135">Esses logons têm Olá seguintes desvantagens:</span><span class="sxs-lookup"><span data-stu-id="43be1-135">These logins have hello following drawbacks:</span></span>

* <span data-ttu-id="43be1-136">O usuário não consegue experimentar o logon único em todos os aplicativos que usam um Microsoft Identity, somente entre os Microsoft Identities configurados por seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="43be1-136">User cannot experience single-sign on across all apps that use a Microsoft Identity, only across those Microsoft Identities that your application has configured.</span></span>
* <span data-ttu-id="43be1-137">O aplicativo não pode ser usado com recursos mais avançados de negócios, como acesso condicional ou use Olá InTune pacote de produtos.</span><span class="sxs-lookup"><span data-stu-id="43be1-137">Your application cannot be used with more advanced business features such as Conditional Access or use hello InTune suite of products.</span></span>
* <span data-ttu-id="43be1-138">Seu aplicativo não dá suporte à autenticação baseada em certificado para usuários corporativos.</span><span class="sxs-lookup"><span data-stu-id="43be1-138">Your application can't support certificate-based authentication for business users.</span></span>

<span data-ttu-id="43be1-139">Aqui está uma representação de como os SDKs de identidade do Microsoft hello funcionam com armazenamento Olá compartilhado de sua tooenable aplicativos SSO:</span><span class="sxs-lookup"><span data-stu-id="43be1-139">Here is a representation of how hello Microsoft Identity SDKs work with hello shared storage of your applications tooenable SSO:</span></span>

```
+------------+ +------------+  +-------------+
|            | |            |  |             |
|   App 1    | |   App 2    |  |   App 3     |
|            | |            |  |             |
|            | |            |  |             |
+------------+ +------------+  +-------------+
| Azure SDK  | | Azure SDK  |  | Azure SDK   |
+------------+-+------------+--+-------------+
|                                            |
|            App Shared Storage              |
+--------------------------------------------+
```

#### <a name="broker-assisted-logins"></a><span data-ttu-id="43be1-140">Logons assistidos por agentes</span><span class="sxs-lookup"><span data-stu-id="43be1-140">Broker assisted logins</span></span>
<span data-ttu-id="43be1-141">Logons assistido por agente são experiências de logon que ocorrem no aplicativo de broker hello e usam armazenamento hello e segurança de credenciais do hello broker tooshare em todos os aplicativos no dispositivo de saudação que se aplicam a plataforma do Microsoft Identity hello.</span><span class="sxs-lookup"><span data-stu-id="43be1-141">Broker-assisted logins are login experiences that occur within hello broker application and use hello storage and security of hello broker tooshare credentials across all applications on hello device that apply hello Microsoft Identity platform.</span></span> <span data-ttu-id="43be1-142">Isso significa que seus aplicativos usam Olá broker toosign usuários.</span><span class="sxs-lookup"><span data-stu-id="43be1-142">This means that your applications rely on hello broker toosign users in.</span></span> <span data-ttu-id="43be1-143">No iOS e Android esses agentes são fornecidos por meio de aplicativos para download que os clientes instalar independente ou podem ser enviados toohello dispositivo por uma empresa que gerencia o dispositivo Olá para o usuário.</span><span class="sxs-lookup"><span data-stu-id="43be1-143">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed toohello device by a company who manages hello device for their user.</span></span> <span data-ttu-id="43be1-144">Um exemplo desse tipo de aplicativo é um aplicativo do Microsoft Authenticator hello no iOS.</span><span class="sxs-lookup"><span data-stu-id="43be1-144">An example of this type of application is hello Microsoft Authenticator application on iOS.</span></span> <span data-ttu-id="43be1-145">No Windows, essa funcionalidade é fornecida por um seletor de conta interna do sistema operacional de toohello, tecnicamente conhecido como Olá agente de autenticação da Web.</span><span class="sxs-lookup"><span data-stu-id="43be1-145">In Windows this functionality is provided by an account chooser built in toohello operating system, known technically as hello Web Authentication Broker.</span></span>
<span data-ttu-id="43be1-146">experiência de saudação varia por plataforma e às vezes pode ser toousers interrupções se não gerenciados corretamente.</span><span class="sxs-lookup"><span data-stu-id="43be1-146">hello experience varies by platform and can sometimes be disruptive toousers if not managed correctly.</span></span> <span data-ttu-id="43be1-147">Você provavelmente está mais familiarizado com esse padrão se você tiver o aplicativo do Facebook hello instalado e usa o Facebook Connect de outro aplicativo.</span><span class="sxs-lookup"><span data-stu-id="43be1-147">You're probably most familiar with this pattern if you have hello Facebook application installed and use Facebook Connect from another application.</span></span> <span data-ttu-id="43be1-148">Olá, usos de plataforma do Microsoft Identity Olá mesmo padrão.</span><span class="sxs-lookup"><span data-stu-id="43be1-148">hello Microsoft Identity platform uses hello same pattern.</span></span>

<span data-ttu-id="43be1-149">Para iOS isso leva animação de "transição" tooa onde seu aplicativo é enviado toohello em segundo plano enquanto os aplicativos do Microsoft Authenticator Olá vem toohello em primeiro plano para Olá usuário tooselect qual conta gostariam toosign com.</span><span class="sxs-lookup"><span data-stu-id="43be1-149">For iOS this leads tooa "transition" animation where your application is sent toohello background while hello Microsoft Authenticator applications comes toohello foreground for hello user tooselect which account they would like toosign in with.</span></span>  

<span data-ttu-id="43be1-150">Para a conta de saudação do Android e Windows seletor é exibida na parte superior de seu aplicativo de usuário de toohello menos interrupções.</span><span class="sxs-lookup"><span data-stu-id="43be1-150">For Android and Windows hello account chooser is displayed on top of your application which is less disruptive toohello user.</span></span>

#### <a name="how-hello-broker-gets-invoked"></a><span data-ttu-id="43be1-151">Como o agente de saudação obtém chamado</span><span class="sxs-lookup"><span data-stu-id="43be1-151">How hello broker gets invoked</span></span>
<span data-ttu-id="43be1-152">Se um agente compatível estiver instalado no dispositivo hello, como Olá aplicativo Microsoft Authenticator, Olá SDKs do Microsoft Identity será automaticamente Olá invocar broker Olá para você quando um usuário indica desejarem toolog usando qualquer conta de trabalho plataforma do Microsoft Identity Hello.</span><span class="sxs-lookup"><span data-stu-id="43be1-152">If a compatible broker is installed on hello device, like hello Microsoft Authenticator application, hello Microsoft Identity SDKs will automatically do hello work of invoking hello broker for you when a user indicates they wish toolog in using any account from hello Microsoft Identity platform.</span></span> <span data-ttu-id="43be1-153">Essa conta pode ser uma Conta da Microsoft pessoal, uma conta corporativa ou de estudante ou uma conta que você fornece e hospeda no Azure usando nossos produtos B2C e B2B.</span><span class="sxs-lookup"><span data-stu-id="43be1-153">This account could be a personal Microsoft Account, a work or school account, or an account that you provide and host in Azure using our B2C and B2B products.</span></span> 
 
 #### <a name="how-we-ensure-hello-application-is-valid"></a><span data-ttu-id="43be1-154">Como podemos garantir que o aplicativo hello é válido</span><span class="sxs-lookup"><span data-stu-id="43be1-154">How we ensure hello application is valid</span></span>
 
 <span data-ttu-id="43be1-155">Olá necessidade tooensure Olá identidade um agente do aplicativo chamada hello é crucial toohello segurança que fornecemos em logons de broker assistido.</span><span class="sxs-lookup"><span data-stu-id="43be1-155">hello need tooensure hello identity of an application call hello broker is crucial toohello security we provide in broker assisted logins.</span></span> <span data-ttu-id="43be1-156">IOS, nem Android impõe identificadores exclusivos que só são válidos para um determinado aplicativo, para que aplicativos mal-intencionados podem "falsificar" identificador de um aplicativo legítimo e receber tokens Olá destinam-se para o aplicativo legítimo hello.</span><span class="sxs-lookup"><span data-stu-id="43be1-156">Neither iOS nor Android enforces unique identifiers that are valid only for a given application, so malicious applications may "spoof" a legitimate application's identifier and receive hello tokens meant for hello legitimate application.</span></span> <span data-ttu-id="43be1-157">tooensure que é sempre se comunicam com o aplicativo correto hello em tempo de execução, solicitamos Olá desenvolvedor tooprovide um redirectURI personalizado ao registrar seu aplicativo com a Microsoft.</span><span class="sxs-lookup"><span data-stu-id="43be1-157">tooensure we are always communicating with hello right application at runtime, we ask hello developer tooprovide a custom redirectURI when registering their application with Microsoft.</span></span> <span data-ttu-id="43be1-158">**O modo como os desenvolvedores devem criar esse URI de redirecionamento será abordado com detalhes logo abaixo.**</span><span class="sxs-lookup"><span data-stu-id="43be1-158">**How developers should craft this redirect URI is discussed in detail below.**</span></span> <span data-ttu-id="43be1-159">Este redirectURI personalizado contém a impressão digital do certificado de saudação do aplicativo hello e é garantido toobe toohello exclusivo aplicativo pela Olá Google Play Store.</span><span class="sxs-lookup"><span data-stu-id="43be1-159">This custom redirectURI contains hello certificate thumbprint of hello application and is ensured toobe unique toohello application by hello Google Play Store.</span></span> <span data-ttu-id="43be1-160">Quando um aplicativo chama broker hello, broker Olá solicita tooprovide do sistema operacional Android Olá com hello impressão digital do certificado que broker chamado hello.</span><span class="sxs-lookup"><span data-stu-id="43be1-160">When an application calls hello broker, hello broker asks hello Android operating system tooprovide it with hello certificate thumbprint that called hello broker.</span></span> <span data-ttu-id="43be1-161">broker Olá fornece essa tooMicrosoft de impressão digital do certificado no sistema de identidade Olá chamada tooour.</span><span class="sxs-lookup"><span data-stu-id="43be1-161">hello broker provides this certificate thumbprint tooMicrosoft in hello call tooour identity system.</span></span> <span data-ttu-id="43be1-162">Se certificado Olá impressão digital do aplicativo hello não coincide com a impressão digital do certificado Olá fornecido toous pelo desenvolvedor Olá durante o registro, podemos negará o acesso toohello tokens para Olá recurso Olá aplicativo está solicitando.</span><span class="sxs-lookup"><span data-stu-id="43be1-162">If hello certificate thumbprint of hello application does not match hello certificate thumbprint provided toous by hello developer during registration, we will deny access toohello tokens for hello resource hello application is requesting.</span></span> <span data-ttu-id="43be1-163">Essa verificação garante que apenas aplicativo hello registrado pelo desenvolvedor Olá recebe tokens.</span><span class="sxs-lookup"><span data-stu-id="43be1-163">This check ensures that only hello application registered by hello developer receives tokens.</span></span>

<span data-ttu-id="43be1-164">**desenvolvedor Olá possui escolha de saudação do se Olá SDK do Microsoft Identity chama broker hello ou usa Olá sem agente assistido fluxo.**</span><span class="sxs-lookup"><span data-stu-id="43be1-164">**hello developer has hello choice of if hello Microsoft Identity SDK calls hello broker or uses hello non-broker assisted flow.**</span></span> <span data-ttu-id="43be1-165">No entanto se o desenvolvedor de saudação escolher não toouse Olá assistido broker fluxo percam benefício de saudação do uso de credenciais de SSO usuário Olá já tenha adicionado no dispositivo hello e impede que seu aplicativo está sendo usado com recursos da empresa Microsoft oferece a seus clientes, como acesso condicional, recursos de gerenciamento do Intune e autenticação baseada em certificado.</span><span class="sxs-lookup"><span data-stu-id="43be1-165">However if hello developer chooses not toouse hello broker-assisted flow they lose hello benefit of using SSO credentials that hello user may have already added on hello device and prevents their application from being used with business features Microsoft provides its customers such as Conditional Access, Intune Management capabilities, and certificate-based authentication.</span></span>

<span data-ttu-id="43be1-166">Esses logons têm Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="43be1-166">These logins have hello following benefits:</span></span>

* <span data-ttu-id="43be1-167">Usuário experiências SSO entre todos os seus aplicativos, independentemente do fornecedor de saudação.</span><span class="sxs-lookup"><span data-stu-id="43be1-167">User experiences SSO across all their applications no matter hello vendor.</span></span>
* <span data-ttu-id="43be1-168">Seu aplicativo pode usar recursos de negócios mais avançados como acesso condicional ou conjunto de InTune Olá de produtos.</span><span class="sxs-lookup"><span data-stu-id="43be1-168">Your application can use more advanced business features such as Conditional Access or use hello InTune suite of products.</span></span>
* <span data-ttu-id="43be1-169">Seu aplicativo pode oferecer suporte à autenticação baseada em certificado para usuários corporativos.</span><span class="sxs-lookup"><span data-stu-id="43be1-169">Your application can support certificate-based authentication for business users.</span></span>
* <span data-ttu-id="43be1-170">Muito mais segura experiência de entrada no como identidade de saudação do aplicativo hello e usuário Olá sejam verificadas pelo aplicativo de broker hello com criptografia e algoritmos de segurança adicional.</span><span class="sxs-lookup"><span data-stu-id="43be1-170">Much more secure sign-in experience as hello identity of hello application and hello user are verified by hello broker application with additional security algorithms and encryption.</span></span>

<span data-ttu-id="43be1-171">Esses logons têm Olá seguintes desvantagens:</span><span class="sxs-lookup"><span data-stu-id="43be1-171">These logins have hello following drawbacks:</span></span>

* <span data-ttu-id="43be1-172">No iOS usuário Olá foi transicionado fora do processo do aplicativo enquanto as credenciais são escolhidas.</span><span class="sxs-lookup"><span data-stu-id="43be1-172">In iOS hello user is transitioned out of your application's experience while credentials are chosen.</span></span>
* <span data-ttu-id="43be1-173">Perda de logon de Olá Olá capacidade toomanage experiência para os clientes dentro de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="43be1-173">Loss of hello ability toomanage hello login experience for your customers within your application.</span></span>

<span data-ttu-id="43be1-174">Aqui está uma representação de como Olá SDKs do Microsoft Identity trabalho com hello broker tooenable aplicativos SSO:</span><span class="sxs-lookup"><span data-stu-id="43be1-174">Here is a representation of how hello Microsoft Identity SDKs work with hello broker applications tooenable SSO:</span></span>

```
+------------+ +------------+   +-------------+
|            | |            |   |             |
|   App 1    | |   App 2    |   |   Someone   |
|            | |            |   |    Else's   |
|            | |            |   |     App     |
+------------+ +------------+   +-------------+
|  ADAL SDK  | |  ADAL SDK  |   |  ADAL SDK   |
+-----+------+-+-----+------+-  +-------+-----+
      |              |                  |
      |       +------v------+           |
      |       |             |           |
      |       | Microsoft   |           |
      +-------> Broker      |^----------+
              | Application
              |             |
              +-------------+
              |             |
              |   Broker    |
              |   Storage   |
              |             |
              +-------------+

```

<span data-ttu-id="43be1-175">Com essas informações de plano de fundo deve ser capaz de toobetter entender e implementar o SSO dentro de seu aplicativo usando a plataforma do Microsoft Identity hello e SDKs.</span><span class="sxs-lookup"><span data-stu-id="43be1-175">Armed with this background information you should be able toobetter understand and implement SSO within your application using hello Microsoft Identity platform and SDKs.</span></span>

## <a name="enabling-cross-app-sso-using-adal"></a><span data-ttu-id="43be1-176">Habilitar SSO entre aplicativos usando a ADAL</span><span class="sxs-lookup"><span data-stu-id="43be1-176">Enabling cross-app SSO using ADAL</span></span>
<span data-ttu-id="43be1-177">Aqui usamos Olá ADAL SDK do Android para:</span><span class="sxs-lookup"><span data-stu-id="43be1-177">Here we use hello ADAL Android SDK to:</span></span>

* <span data-ttu-id="43be1-178">Ativar o SSO assistido por não agente para seu pacote de aplicativos</span><span class="sxs-lookup"><span data-stu-id="43be1-178">Turn on non-broker assisted SSO for your suite of apps</span></span>
* <span data-ttu-id="43be1-179">Ativar o suporte para SSO assistido por agente</span><span class="sxs-lookup"><span data-stu-id="43be1-179">Turn on support for broker-assisted SSO</span></span>

### <a name="turning-on-sso-for-non-broker-assisted-sso"></a><span data-ttu-id="43be1-180">Ativar o SSO assistido por não agente</span><span class="sxs-lookup"><span data-stu-id="43be1-180">Turning on SSO for non-broker assisted SSO</span></span>
<span data-ttu-id="43be1-181">Para SSO de assistido sem agente em todos os aplicativos Olá SDKs do Microsoft Identity gerenciar grande parte da complexidade de saudação do SSO para você.</span><span class="sxs-lookup"><span data-stu-id="43be1-181">For non-broker assisted SSO across applications hello Microsoft Identity SDKs manage much of hello complexity of SSO for you.</span></span> <span data-ttu-id="43be1-182">Isso inclui localizar usuário Olá no cache de saudação e manter uma lista de usuários conectados para você tooquery.</span><span class="sxs-lookup"><span data-stu-id="43be1-182">This includes finding hello right user in hello cache and maintaining a list of logged in users for you tooquery.</span></span>

<span data-ttu-id="43be1-183">tooenable SSO entre os aplicativos que você possui que precisar Olá toodo a seguir:</span><span class="sxs-lookup"><span data-stu-id="43be1-183">tooenable SSO across applications you own you need toodo hello following:</span></span>

1. <span data-ttu-id="43be1-184">Verifique se todos os seu aplicativos usuário Olá mesma ID de cliente ou a ID do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="43be1-184">Ensure all your applications user hello same Client ID or Application ID.</span></span>
2. <span data-ttu-id="43be1-185">Certifique-se de que todos os seus aplicativos tenham Olá que mesmo SharedUserID definido.</span><span class="sxs-lookup"><span data-stu-id="43be1-185">Ensure all your applications have hello same SharedUserID set.</span></span>
3. <span data-ttu-id="43be1-186">Certifique-se de que todos os seu Olá de compartilhamento de aplicativos mesmo certificado de autenticação do Google Play da saudação armazenar para que você pode compartilhar o armazenamento.</span><span class="sxs-lookup"><span data-stu-id="43be1-186">Ensure that all of your applications share hello same signing certificate from hello Google Play store so that you can share storage.</span></span>

#### <a name="step-1-using-hello-same-client-id--application-id-for-all-hello-applications-in-your-suite-of-apps"></a><span data-ttu-id="43be1-187">Etapa 1: Usando Olá a mesma ID de cliente / ID de aplicativo para todos os aplicativos em seu pacote de aplicativos de Olá</span><span class="sxs-lookup"><span data-stu-id="43be1-187">Step 1: Using hello same Client ID / Application ID for all hello applications in your suite of apps</span></span>
<span data-ttu-id="43be1-188">Para tooknow de plataforma do Microsoft Identity Olá que é permitido tooshare tokens em seus aplicativos, cada um dos aplicativos precisará tooshare Olá mesma ID de cliente ou a ID do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="43be1-188">In order for hello Microsoft Identity platform tooknow that it's allowed tooshare tokens across your applications, each of your applications will need tooshare hello same Client ID or Application ID.</span></span> <span data-ttu-id="43be1-189">Este é o identificador exclusivo de saudação fornecida tooyou quando você registrou seu primeiro aplicativo no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="43be1-189">This is hello unique identifier that was provided tooyou when you registered your first application in hello portal.</span></span>

<span data-ttu-id="43be1-190">Você deve estar se perguntando como você identificará os diferentes aplicativos toohello serviço do Microsoft Identity se ele usa Olá ID do mesmo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="43be1-190">You may be wondering how you will identify different apps toohello Microsoft Identity service if it uses hello same Application ID.</span></span> <span data-ttu-id="43be1-191">resposta de saudação é com hello **URIs de redirecionamento**.</span><span class="sxs-lookup"><span data-stu-id="43be1-191">hello answer is with hello **Redirect URIs**.</span></span> <span data-ttu-id="43be1-192">Cada aplicativo pode ter vários URIs de redirecionamento registrado no portal de integração de saudação.</span><span class="sxs-lookup"><span data-stu-id="43be1-192">Each application can have multiple Redirect URIs registered in hello onboarding portal.</span></span> <span data-ttu-id="43be1-193">Cada aplicativo em seu pacote terá um URI de redirecionamento diferente.</span><span class="sxs-lookup"><span data-stu-id="43be1-193">Each app in your suite will have a different redirect URI.</span></span> <span data-ttu-id="43be1-194">Veja abaixo um exemplo de como isso acontece.</span><span class="sxs-lookup"><span data-stu-id="43be1-194">An example of how this looks is below:</span></span>

<span data-ttu-id="43be1-195">URI de Redirecionamento do App1: `msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D`</span><span class="sxs-lookup"><span data-stu-id="43be1-195">App1 Redirect URI: `msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D`</span></span>

<span data-ttu-id="43be1-196">URI de Redirecionamento do App2: `msauth://com.example.userapp1/KmB7PxIytyLkbGHuI%2UitkW%2Fejk%4E`</span><span class="sxs-lookup"><span data-stu-id="43be1-196">App2 Redirect URI: `msauth://com.example.userapp1/KmB7PxIytyLkbGHuI%2UitkW%2Fejk%4E`</span></span>

<span data-ttu-id="43be1-197">URI de Redirecionamento do App3: `msauth://com.example.userapp2/Pt85PxIyvbLkbKUtBI%2SitkW%2Fejk%9F`</span><span class="sxs-lookup"><span data-stu-id="43be1-197">App3 Redirect URI: `msauth://com.example.userapp2/Pt85PxIyvbLkbKUtBI%2SitkW%2Fejk%9F`</span></span>

<span data-ttu-id="43be1-198">....</span><span class="sxs-lookup"><span data-stu-id="43be1-198">....</span></span>

<span data-ttu-id="43be1-199">Esses são aninhados em Olá a mesma ID de cliente / ID do aplicativo e pesquisada Olá com base em redirecionam URI retornar toous em sua configuração de SDK.</span><span class="sxs-lookup"><span data-stu-id="43be1-199">These are nested under hello same client ID / application ID and looked up based on hello redirect URI you return toous in your SDK configuration.</span></span>

```
+-------------------+
|                   |
|  Client ID        |
+---------+---------+
          |
          |           +-----------------------------------+
          |           |  App 1 Redirect URI               |
          +----------^+                                   |
          |           +-----------------------------------+
          |
          |           +-----------------------------------+
          +----------^+  App 2 Redirect URI               |
          |           |                                   |
          |           +-----------------------------------+
          |
          +----------^+-----------------------------------+
                      |  App 3 Redirect URI               |
                      |                                   |
                      +-----------------------------------+

```


<span data-ttu-id="43be1-200">*Observe que o formato desses URIs de redirecionamento de Olá são explicados abaixo. Você pode usar qualquer URI de redirecionamento, a menos que você deseja que o agente de saudação toosupport, caso em que eles devem ter a aparência Olá acima*</span><span class="sxs-lookup"><span data-stu-id="43be1-200">*Note that hello format of these Redirect URIs are explained below. You may use any Redirect URI unless you wish toosupport hello broker, in which case they must look something like hello above*</span></span>

#### <a name="step-2-configuring-shared-storage-in-android"></a><span data-ttu-id="43be1-201">Etapa 2: Configurando o armazenamento compartilhado no Android</span><span class="sxs-lookup"><span data-stu-id="43be1-201">Step 2: Configuring shared storage in Android</span></span>
<span data-ttu-id="43be1-202">Saudação de configuração `SharedUserID` está além do escopo deste documento hello, mas podem ser aprendidos lendo Olá documentação Google Android Olá [manifesto](http://developer.android.com/guide/topics/manifest/manifest-element.html).</span><span class="sxs-lookup"><span data-stu-id="43be1-202">Setting hello `SharedUserID` is beyond hello scope of this document but can be learned by reading hello Google Android documentation on hello [Manifest](http://developer.android.com/guide/topics/manifest/manifest-element.html).</span></span> <span data-ttu-id="43be1-203">O importante é que você decida qual o nome de seu sharedUserID e usar esse nome em todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="43be1-203">What is important is that you decide what you want your sharedUserID will be called and use that across all your applications.</span></span>

<span data-ttu-id="43be1-204">Depois que você tiver Olá `SharedUserID` em todos os seus aplicativos, você está pronto toouse SSO.</span><span class="sxs-lookup"><span data-stu-id="43be1-204">Once you have hello `SharedUserID` in all your applications you are ready toouse SSO.</span></span>

> [!WARNING]
> <span data-ttu-id="43be1-205">Quando você compartilhar o armazenamento em seus aplicativos de qualquer aplicativo pode excluir usuários ou pior excluir todos os tokens de saudação em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="43be1-205">When you share storage across your applications any application can delete users, or worse delete all hello tokens across your application.</span></span> <span data-ttu-id="43be1-206">Isso é particularmente desastroso se você tiver aplicativos que dependem de trabalho em segundo plano do hello tokens toodo.</span><span class="sxs-lookup"><span data-stu-id="43be1-206">This is particularly disastrous if you have applications that rely on hello tokens toodo background work.</span></span> <span data-ttu-id="43be1-207">Compartilhamento de armazenamento significa que você seja muito cuidado ao remover todas as operações por meio de saudação SDKs do Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="43be1-207">Sharing storage means that you must be very careful in any and all remove operations through hello Microsoft Identity SDKs.</span></span>
> 
> 

<span data-ttu-id="43be1-208">É isso!</span><span class="sxs-lookup"><span data-stu-id="43be1-208">That's it!</span></span> <span data-ttu-id="43be1-209">Olá SDK do Microsoft Identity agora compartilharão as credenciais em todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="43be1-209">hello Microsoft Identity SDK will now share credentials across all your applications.</span></span> <span data-ttu-id="43be1-210">lista de saudação do usuário também será compartilhada entre instâncias do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="43be1-210">hello user list will also be shared across application instances.</span></span>

### <a name="turning-on-sso-for-broker-assisted-sso"></a><span data-ttu-id="43be1-211">Ativar o SSO assistido por agente</span><span class="sxs-lookup"><span data-stu-id="43be1-211">Turning on SSO for broker assisted SSO</span></span>
<span data-ttu-id="43be1-212">Olá capacidade para um toouse de aplicativo é qualquer agente instalado no dispositivo Olá **desativado por padrão**.</span><span class="sxs-lookup"><span data-stu-id="43be1-212">hello ability for an application toouse any broker that is installed on hello device is **turned off by default**.</span></span> <span data-ttu-id="43be1-213">Em ordem toouse seu aplicativo com o agente de saudação fazer algumas configurações adicionais e adicionar algum aplicativo tooyour de código.</span><span class="sxs-lookup"><span data-stu-id="43be1-213">In order toouse your application with hello broker you must do some additional configuration and add some code tooyour application.</span></span>

<span data-ttu-id="43be1-214">Olá etapas toofollow são:</span><span class="sxs-lookup"><span data-stu-id="43be1-214">hello steps toofollow are:</span></span>

1. <span data-ttu-id="43be1-215">Habilitar o modo de agente na toohello de chamada do código do aplicativo SDK MS</span><span class="sxs-lookup"><span data-stu-id="43be1-215">Enable broker mode in your application code's call toohello MS SDK</span></span>
2. <span data-ttu-id="43be1-216">Estabelecer um novo URI de redirecionamento e fornecer o aplicativo hello tooboth e seu registro de aplicativo</span><span class="sxs-lookup"><span data-stu-id="43be1-216">Establish a new redirect URI and provide that tooboth hello app and your app registration</span></span>
3. <span data-ttu-id="43be1-217">Configurando permissões corretas de saudação no manifesto do Android Olá</span><span class="sxs-lookup"><span data-stu-id="43be1-217">Setting up hello correct permissions in hello Android manifest</span></span>

#### <a name="step-1-enable-broker-mode-in-your-application"></a><span data-ttu-id="43be1-218">Etapa 1: habilitar o modo de agente em seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="43be1-218">Step 1: Enable broker mode in your application</span></span>
<span data-ttu-id="43be1-219">capacidade de saudação para o agente do aplicativo toouse Olá é ativada quando você cria configurações"hello" ou a configuração inicial da sua instância de autenticação.</span><span class="sxs-lookup"><span data-stu-id="43be1-219">hello ability for your application toouse hello broker is turned on when you create hello "settings" or initial setup of your Authentication instance.</span></span> <span data-ttu-id="43be1-220">Faça isso configurando o tipo ApplicationSettings em seu código:</span><span class="sxs-lookup"><span data-stu-id="43be1-220">You do this by setting your ApplicationSettings type in your code:</span></span>

```
AuthenticationSettings.Instance.setUseBroker(true);
```


#### <a name="step-2-establish-a-new-redirect-uri-with-your-url-scheme"></a><span data-ttu-id="43be1-221">Etapa 2: Estabelecer um novo URI de redirecionamento com seu esquema de URL</span><span class="sxs-lookup"><span data-stu-id="43be1-221">Step 2: Establish a new redirect URI with your URL Scheme</span></span>
<span data-ttu-id="43be1-222">Tooensure ordem que estamos sempre retornar credencial Olá tokens de aplicativo correto toohello, precisamos toomake se que chamar novamente tooyour aplicativo de forma que Olá sistema operacional Android pode verificar.</span><span class="sxs-lookup"><span data-stu-id="43be1-222">In order tooensure that we always return hello credential tokens toohello correct application, we need toomake sure we call back tooyour application in a way that hello Android operating system can verify.</span></span> <span data-ttu-id="43be1-223">sistema de operacional Android Olá usa o hash de saudação do certificado de saudação em Olá loja Google Play.</span><span class="sxs-lookup"><span data-stu-id="43be1-223">hello Android operating system uses hello hash of hello certificate in hello Google Play store.</span></span> <span data-ttu-id="43be1-224">Isso não pode ser falsificado por um aplicativo mal-intencionado.</span><span class="sxs-lookup"><span data-stu-id="43be1-224">This cannot be spoofed by a rogue application.</span></span> <span data-ttu-id="43be1-225">Portanto, podemos utilizar isso junto com hello URI do nosso tooensure de aplicativo de agente que tokens Olá são retornados de aplicativo correto toohello.</span><span class="sxs-lookup"><span data-stu-id="43be1-225">Therefore, we leverage this along with hello URI of our broker application tooensure that hello tokens are returned toohello correct application.</span></span> <span data-ttu-id="43be1-226">É necessário tooestablish você no seu aplicativo e defina o URI de redirecionamento exclusivo como um URI de redirecionamento em nosso portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="43be1-226">We require you tooestablish this unique redirect URI both in your application and set as a Redirect URI in our developer portal.</span></span>

<span data-ttu-id="43be1-227">O URI de redirecionamento deve estar no formato adequado de saudação do:</span><span class="sxs-lookup"><span data-stu-id="43be1-227">Your redirect URI must be in hello proper form of:</span></span>

`msauth://packagename/Base64UrlencodedSignature`

<span data-ttu-id="43be1-228">ex: *msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D*</span><span class="sxs-lookup"><span data-stu-id="43be1-228">ex: *msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D*</span></span>

<span data-ttu-id="43be1-229">Esse URI de redirecionamento precisa toobe especificado em seu registro de aplicativo usando Olá [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="43be1-229">This Redirect URI needs toobe specified in your app registration using hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="43be1-230">Para saber mais sobre o registro de aplicativo do Azure AD, confira [Integração com o Azure Active Directory](active-directory-how-to-integrate.md).</span><span class="sxs-lookup"><span data-stu-id="43be1-230">For more information on Azure AD app registration, see [Integrating with Azure Active Directory](active-directory-how-to-integrate.md).</span></span>

#### <a name="step-3-set-up-hello-correct-permissions-in-your-application"></a><span data-ttu-id="43be1-231">Etapa 3: Definir as permissões corretas de Olá em seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="43be1-231">Step 3: Set up hello correct permissions in your application</span></span>
<span data-ttu-id="43be1-232">Nosso aplicativo de agente no Android usa o recurso de Gerenciador de contas de saudação de credenciais de toomanage de sistema operacional Android Olá entre aplicativos.</span><span class="sxs-lookup"><span data-stu-id="43be1-232">Our broker application in Android uses hello Accounts Manager feature of hello Android OS toomanage credentials across applications.</span></span> <span data-ttu-id="43be1-233">No agente de saudação toouse ordem no Android o manifesto do aplicativo deve ter contas de AccountManager de toouse de permissões.</span><span class="sxs-lookup"><span data-stu-id="43be1-233">In order toouse hello broker in Android your app manifest must have permissions toouse AccountManager accounts.</span></span> <span data-ttu-id="43be1-234">Isso é discutido em detalhes no hello [Google documentação para o gerente de conta aqui](http://developer.android.com/reference/android/accounts/AccountManager.html)</span><span class="sxs-lookup"><span data-stu-id="43be1-234">This is discussed in detail in hello [Google documentation for Account Manager here](http://developer.android.com/reference/android/accounts/AccountManager.html)</span></span>

<span data-ttu-id="43be1-235">Em particular, essas permissões são:</span><span class="sxs-lookup"><span data-stu-id="43be1-235">In particular, these permissions are:</span></span>

```
GET_ACCOUNTS
USE_CREDENTIALS
MANAGE_ACCOUNTS
```

### <a name="youve-configured-sso"></a><span data-ttu-id="43be1-236">Você configurou o SSO!</span><span class="sxs-lookup"><span data-stu-id="43be1-236">You've configured SSO!</span></span>
<span data-ttu-id="43be1-237">Agora Olá SDK do Microsoft Identity automaticamente as credenciais de compartilhamento em seus aplicativos e invocar broker Olá caso ele esteja presente em seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="43be1-237">Now hello Microsoft Identity SDK will automatically both share credentials across your applications and invoke hello broker if it's present on their device.</span></span>

