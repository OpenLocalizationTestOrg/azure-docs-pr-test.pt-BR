---
title: Como habilitar o SSO entre aplicativos no Android usando a ADAL | Microsoft Docs
description: "Como usar os recursos do SDK do ADAL para habilitar o Logon Único em seus aplicativos. "
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
ms.openlocfilehash: 9c7e959530a836fe5ddf74708363a636c39b3cc6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-enable-cross-app-sso-on-android-using-adal"></a><span data-ttu-id="1f038-103">Como habilitar o SSO entre aplicativos no Android usando a ADAL</span><span class="sxs-lookup"><span data-stu-id="1f038-103">How to enable cross-app SSO on Android using ADAL</span></span>
<span data-ttu-id="1f038-104">Atualmente, os clientes esperam o recurso de Logon Único (SSO), para que os usuários precisem inserir suas credenciais apenas uma vez, e essas credenciais sejam aplicadas entre os aplicativos.</span><span class="sxs-lookup"><span data-stu-id="1f038-104">Providing Single Sign-On (SSO) so that users only need to enter their credentials once and have those credentials automatically work across applications is now expected by customers.</span></span> <span data-ttu-id="1f038-105">A dificuldade em digitar o nome de usuário e senha em uma tela pequena, muitas vezes combinada com um fator adicional (2FA) como uma chamada telefônica ou um código enviado via texto, se transforma rapidamente em insatisfação se um usuário tiver que fazer isso mais de uma vez para o seu produto.</span><span class="sxs-lookup"><span data-stu-id="1f038-105">The difficulty in entering their username and password on a small screen, often times combined with an additional factor (2FA) like a phone call or a texted code, results in quick dissatisfaction if a user has to do this more than one time for your product.</span></span>

<span data-ttu-id="1f038-106">Além disso, se você aplicar uma plataforma de identidade usada por outros aplicativos, como Contas da Microsoft ou uma conta corporativa do Office365, os clientes esperam que essas credenciais estejam disponíveis em todos os aplicativos, independentemente do fornecedor.</span><span class="sxs-lookup"><span data-stu-id="1f038-106">In addition, if you apply an identity platform that other applications may use such as Microsoft Accounts or a work account from Office365, customers expect that those credentials to be available to use across all their applications no matter the vendor.</span></span>

<span data-ttu-id="1f038-107">A plataforma Microsoft Identity, juntamente com nossos SDKs do Microsoft Identity, faz todo esse trabalho difícil para você e permite que você agrade aos seus clientes com o SSO dentro de seu próprio pacote de aplicativos ou, como ocorre com o nossa funcionalidade de agente e aplicativos autenticadores, em todo o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1f038-107">The Microsoft Identity platform, along with our Microsoft Identity SDKs, does all this hard work for you and gives you the ability to delight your customers with SSO either within your own suite of applications or, as with our broker capability and Authenticator applications, across the entire device.</span></span>

<span data-ttu-id="1f038-108">Este passo a passo informa como configurar nosso SDK dentro de seu aplicativo a fim de fornecer esse benefício aos clientes.</span><span class="sxs-lookup"><span data-stu-id="1f038-108">This walkthrough will tell you how to configure our SDK within your application to provide this benefit to your customers.</span></span>

<span data-ttu-id="1f038-109">Este passo a passo se aplica a:</span><span class="sxs-lookup"><span data-stu-id="1f038-109">This walkthrough applies to:</span></span>

* <span data-ttu-id="1f038-110">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1f038-110">Azure Active Directory</span></span>
* <span data-ttu-id="1f038-111">Active Directory B2C do Azure</span><span class="sxs-lookup"><span data-stu-id="1f038-111">Azure Active Directory B2C</span></span>
* <span data-ttu-id="1f038-112">Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="1f038-112">Azure Active Directory B2B</span></span>
* <span data-ttu-id="1f038-113">Acesso condicional ao Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1f038-113">Azure Active Directory Conditional Access</span></span>

<span data-ttu-id="1f038-114">O documento anterior pressupõe que você sabe como [provisionar aplicativos no portal herdado do Azure Active Directory](active-directory-how-to-integrate.md) e que integrou seu aplicativo ao [SDK do Microsoft Identity para Android](https://github.com/AzureAD/azure-activedirectory-library-for-android).</span><span class="sxs-lookup"><span data-stu-id="1f038-114">The document preceding assumes you know how to [provision applications in the legacy portal for Azure Active Directory](active-directory-how-to-integrate.md) and integrated your application with the [Microsoft Identity Android SDK](https://github.com/AzureAD/azure-activedirectory-library-for-android).</span></span>

## <a name="sso-concepts-in-the-microsoft-identity-platform"></a><span data-ttu-id="1f038-115">Conceitos de SSO na Plataforma do Microsoft Identity</span><span class="sxs-lookup"><span data-stu-id="1f038-115">SSO Concepts in the Microsoft Identity Platform</span></span>
### <a name="microsoft-identity-brokers"></a><span data-ttu-id="1f038-116">Agentes do Microsoft Identity</span><span class="sxs-lookup"><span data-stu-id="1f038-116">Microsoft Identity Brokers</span></span>
<span data-ttu-id="1f038-117">A Microsoft fornece aplicativos para todas as plataformas móveis que permitem o uso das mesmas credenciais em aplicativos de diferentes fornecedores e recursos aprimorados especiais que exigem um único local seguro do qual validar as credenciais.</span><span class="sxs-lookup"><span data-stu-id="1f038-117">Microsoft provides applications for every mobile platform that allow for the bridging of credentials across applications from different vendors and allows for special enhanced features that require a single secure place from where to validate credentials.</span></span> <span data-ttu-id="1f038-118">Chamamos esses recursos de **agentes**.</span><span class="sxs-lookup"><span data-stu-id="1f038-118">We call these **brokers**.</span></span> <span data-ttu-id="1f038-119">No iOS e no Android eles são fornecidos por meio de aplicativos baixáveis que os clientes instalam de forma independente ou que podem ser enviados por push ao dispositivo por uma empresa que gerencia uma parte ou todos os dispositivos para seus funcionários.</span><span class="sxs-lookup"><span data-stu-id="1f038-119">On iOS and Android these are provided through downloadable applications that customers either install independently or can be pushed to the device by a company who manages some or all of the device for their employee.</span></span> <span data-ttu-id="1f038-120">Esses agentes oferecem suporte ao gerenciamento de segurança apenas para alguns aplicativos, ou para todo o dispositivo, com base no desejo dos administradores de TI.</span><span class="sxs-lookup"><span data-stu-id="1f038-120">These brokers support managing security just for some applications or the entire device based on what IT Administrators desire.</span></span> <span data-ttu-id="1f038-121">No Windows, essa funcionalidade é fornecida por um seletor de conta integrado ao sistema operacional, conhecido tecnicamente como o Agente de Autenticação da Web.</span><span class="sxs-lookup"><span data-stu-id="1f038-121">In Windows, this functionality is provided by an account chooser built in to the operating system, known technically as the Web Authentication Broker.</span></span>

<span data-ttu-id="1f038-122">Para saber mais como usamos esses agentes e como os clientes podem vê-los em seu fluxo de logon para a plataforma do Microsoft Identity, continue lendo.</span><span class="sxs-lookup"><span data-stu-id="1f038-122">For more information on how we use these brokers and how your customers might see them in their login flow for the Microsoft Identity platform read on.</span></span>

### <a name="patterns-for-logging-in-on-mobile-devices"></a><span data-ttu-id="1f038-123">Padrões de logon em dispositivos móveis</span><span class="sxs-lookup"><span data-stu-id="1f038-123">Patterns for logging in on mobile devices</span></span>
<span data-ttu-id="1f038-124">O acesso às credenciais em dispositivos segue dois padrões básicos para a plataforma do Microsoft Identity:</span><span class="sxs-lookup"><span data-stu-id="1f038-124">Access to credentials on devices follow two basic patterns for the Microsoft Identity platform:</span></span>

* <span data-ttu-id="1f038-125">Logons assistidos por não agentes</span><span class="sxs-lookup"><span data-stu-id="1f038-125">Non-broker assisted logins</span></span>
* <span data-ttu-id="1f038-126">Logons assistidos por agentes</span><span class="sxs-lookup"><span data-stu-id="1f038-126">Broker assisted logins</span></span>

#### <a name="non-broker-assisted-logins"></a><span data-ttu-id="1f038-127">Logons assistidos por não agentes</span><span class="sxs-lookup"><span data-stu-id="1f038-127">Non-broker assisted logins</span></span>
<span data-ttu-id="1f038-128">Os logons assistidos por não agentes são experiências de logon que ocorrem em linha com o aplicativo e usam o armazenamento local no dispositivo para esse aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1f038-128">Non-broker assisted logins are login experiences that happen inline with the application and use the local storage on the device for that application.</span></span> <span data-ttu-id="1f038-129">Esse armazenamento pode ser compartilhado entre aplicativos, mas as credenciais ficam associadas estritamente ao aplicativo ou pacote de aplicativos que usam essa credencial.</span><span class="sxs-lookup"><span data-stu-id="1f038-129">This storage may be shared across applications but the credentials are tightly bound to the app or suite of apps using that credential.</span></span> <span data-ttu-id="1f038-130">Provavelmente você já experimentou isso em muitos aplicativos móveis ao inserir um nome de usuário e senha dentro do próprio aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1f038-130">You've most likely experienced this in many mobile applications when you enter a username and password within the application itself.</span></span>

<span data-ttu-id="1f038-131">Esses logons têm os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="1f038-131">These logins have the following benefits:</span></span>

* <span data-ttu-id="1f038-132">A experiência de usuário existe totalmente dentro do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1f038-132">User experience exists entirely within the application.</span></span>
* <span data-ttu-id="1f038-133">As credenciais podem ser compartilhadas entre aplicativos assinados com o mesmo certificado, fornecendo uma experiência de logon único para o pacote de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="1f038-133">Credentials can be shared across applications that are signed by the same certificate, providing a single sign-on experience to your suite of applications.</span></span>
* <span data-ttu-id="1f038-134">O controle sobre a experiência de logon é fornecido para o aplicativo antes e depois da entrada.</span><span class="sxs-lookup"><span data-stu-id="1f038-134">Control around the experience of logging in is provided to the application before and after sign-in.</span></span>

<span data-ttu-id="1f038-135">Esses logons têm as seguintes desvantagens:</span><span class="sxs-lookup"><span data-stu-id="1f038-135">These logins have the following drawbacks:</span></span>

* <span data-ttu-id="1f038-136">O usuário não consegue experimentar o logon único em todos os aplicativos que usam um Microsoft Identity, somente entre os Microsoft Identities configurados por seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1f038-136">User cannot experience single-sign on across all apps that use a Microsoft Identity, only across those Microsoft Identities that your application has configured.</span></span>
* <span data-ttu-id="1f038-137">Seu aplicativo não pode ser usado com recursos de negócios mais avançados, como o Acesso Condicional ou no pacote de produtos do InTune.</span><span class="sxs-lookup"><span data-stu-id="1f038-137">Your application cannot be used with more advanced business features such as Conditional Access or use the InTune suite of products.</span></span>
* <span data-ttu-id="1f038-138">Seu aplicativo não dá suporte à autenticação baseada em certificado para usuários corporativos.</span><span class="sxs-lookup"><span data-stu-id="1f038-138">Your application can't support certificate-based authentication for business users.</span></span>

<span data-ttu-id="1f038-139">Veja uma representação de como os SDKs do Microsoft Identity funcionam com o armazenamento compartilhado de seus aplicativos a fim de habilitar o SSO:</span><span class="sxs-lookup"><span data-stu-id="1f038-139">Here is a representation of how the Microsoft Identity SDKs work with the shared storage of your applications to enable SSO:</span></span>

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

#### <a name="broker-assisted-logins"></a><span data-ttu-id="1f038-140">Logons assistidos por agentes</span><span class="sxs-lookup"><span data-stu-id="1f038-140">Broker assisted logins</span></span>
<span data-ttu-id="1f038-141">Os logons assistido por agente são experiências de logon que ocorrem dentro do aplicativo do agente e usam o armazenamento e a segurança do agente para compartilhar as credenciais em todos os aplicativos no dispositivo, e aplicam a plataforma Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="1f038-141">Broker-assisted logins are login experiences that occur within the broker application and use the storage and security of the broker to share credentials across all applications on the device that apply the Microsoft Identity platform.</span></span> <span data-ttu-id="1f038-142">Isso significa que os aplicativos dependem do agente para realizar a entrada dos usuários.</span><span class="sxs-lookup"><span data-stu-id="1f038-142">This means that your applications rely on the broker to sign users in.</span></span> <span data-ttu-id="1f038-143">No iOS e no Android esses agentes são fornecidos por meio de aplicativos baixáveis que os clientes instalam de forma independente ou que podem ser enviados por push ao dispositivo por uma empresa que gerencia o dispositivo para o usuário.</span><span class="sxs-lookup"><span data-stu-id="1f038-143">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed to the device by a company who manages the device for their user.</span></span> <span data-ttu-id="1f038-144">Um exemplo desse tipo de aplicativo é o Microsoft Authenticator no iOS.</span><span class="sxs-lookup"><span data-stu-id="1f038-144">An example of this type of application is the Microsoft Authenticator application on iOS.</span></span> <span data-ttu-id="1f038-145">No Windows, essa funcionalidade é fornecida por um seletor de conta integrado ao sistema operacional, conhecido tecnicamente como o Agente de Autenticação da Web.</span><span class="sxs-lookup"><span data-stu-id="1f038-145">In Windows this functionality is provided by an account chooser built in to the operating system, known technically as the Web Authentication Broker.</span></span>
<span data-ttu-id="1f038-146">A experiência varia de acordo com a plataforma e, às vezes, pode ser perturbador para os usuários se não for gerenciada corretamente.</span><span class="sxs-lookup"><span data-stu-id="1f038-146">The experience varies by platform and can sometimes be disruptive to users if not managed correctly.</span></span> <span data-ttu-id="1f038-147">Provavelmente você estará mais familiarizado com esse padrão se tiver instalado o aplicativo do Facebook e usado o Facebook Connect em outro aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1f038-147">You're probably most familiar with this pattern if you have the Facebook application installed and use Facebook Connect from another application.</span></span> <span data-ttu-id="1f038-148">A plataforma Microsoft Identity usa o mesmo padrão.</span><span class="sxs-lookup"><span data-stu-id="1f038-148">The Microsoft Identity platform uses the same pattern.</span></span>

<span data-ttu-id="1f038-149">Para iOS, isso leva a uma animação de "transição", em que seu aplicativo é enviado ao segundo plano enquanto os aplicativos do Microsoft Authenticator ficam em primeiro plano para o usuário selecionar em qual conta quer entrar.</span><span class="sxs-lookup"><span data-stu-id="1f038-149">For iOS this leads to a "transition" animation where your application is sent to the background while the Microsoft Authenticator applications comes to the foreground for the user to select which account they would like to sign in with.</span></span>  

<span data-ttu-id="1f038-150">Para Android e Windows, o seletor de conta é exibido na parte superior de seu aplicativo, o que é menos perturbador para o usuário.</span><span class="sxs-lookup"><span data-stu-id="1f038-150">For Android and Windows the account chooser is displayed on top of your application which is less disruptive to the user.</span></span>

#### <a name="how-the-broker-gets-invoked"></a><span data-ttu-id="1f038-151">Como o agente é invocado</span><span class="sxs-lookup"><span data-stu-id="1f038-151">How the broker gets invoked</span></span>
<span data-ttu-id="1f038-152">Se um agente compatível for instalado no dispositivo, como o aplicativo Microsoft Authenticator, os SDKs do Microsoft Identity farão automaticamente o trabalho de invocar o agente para você quando um usuário indicar que deseja fazer logon usando qualquer conta da plataforma Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="1f038-152">If a compatible broker is installed on the device, like the Microsoft Authenticator application, the Microsoft Identity SDKs will automatically do the work of invoking the broker for you when a user indicates they wish to log in using any account from the Microsoft Identity platform.</span></span> <span data-ttu-id="1f038-153">Essa conta pode ser uma Conta da Microsoft pessoal, uma conta corporativa ou de estudante ou uma conta que você fornece e hospeda no Azure usando nossos produtos B2C e B2B.</span><span class="sxs-lookup"><span data-stu-id="1f038-153">This account could be a personal Microsoft Account, a work or school account, or an account that you provide and host in Azure using our B2C and B2B products.</span></span> 
 
 #### <a name="how-we-ensure-the-application-is-valid"></a><span data-ttu-id="1f038-154">Como podemos garantir que o aplicativo é válido</span><span class="sxs-lookup"><span data-stu-id="1f038-154">How we ensure the application is valid</span></span>
 
 <span data-ttu-id="1f038-155">A necessidade de garantir a identidade de uma chamada de aplicativo para o agente é fundamental para a segurança fornecida em logons assistidos por agente.</span><span class="sxs-lookup"><span data-stu-id="1f038-155">The need to ensure the identity of an application call the broker is crucial to the security we provide in broker assisted logins.</span></span> <span data-ttu-id="1f038-156">O iOS e o Android não impõem identificadores exclusivos que são válidos somente para um determinado aplicativo, portanto, aplicativos mal-intencionados podem "falsificar" o identificador de um aplicativo legítimo e receber os tokens destinados ao aplicativo legítimo.</span><span class="sxs-lookup"><span data-stu-id="1f038-156">Neither iOS nor Android enforces unique identifiers that are valid only for a given application, so malicious applications may "spoof" a legitimate application's identifier and receive the tokens meant for the legitimate application.</span></span> <span data-ttu-id="1f038-157">Para garantir que estejamos sempre nos comunicando com o aplicativo certo no tempo de execução, pedimos ao desenvolvedor que forneça um redirectURI personalizado ao registrar seu aplicativo com a Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1f038-157">To ensure we are always communicating with the right application at runtime, we ask the developer to provide a custom redirectURI when registering their application with Microsoft.</span></span> <span data-ttu-id="1f038-158">**O modo como os desenvolvedores devem criar esse URI de redirecionamento será abordado com detalhes logo abaixo.**</span><span class="sxs-lookup"><span data-stu-id="1f038-158">**How developers should craft this redirect URI is discussed in detail below.**</span></span> <span data-ttu-id="1f038-159">Este redirectURI personalizado contém a impressão digital do certificado do aplicativo e tem a garantia da Google Play Store de ser exclusivo para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1f038-159">This custom redirectURI contains the certificate thumbprint of the application and is ensured to be unique to the application by the Google Play Store.</span></span> <span data-ttu-id="1f038-160">Quando um aplicativo chama o agente, o agente solicita que o sistema operacional Android o forneça com a impressão digital do certificado que chamou o agente.</span><span class="sxs-lookup"><span data-stu-id="1f038-160">When an application calls the broker, the broker asks the Android operating system to provide it with the certificate thumbprint that called the broker.</span></span> <span data-ttu-id="1f038-161">O agente fornece a impressão digital do certificado para a Microsoft na chamada para nosso sistema de identidade.</span><span class="sxs-lookup"><span data-stu-id="1f038-161">The broker provides this certificate thumbprint to Microsoft in the call to our identity system.</span></span> <span data-ttu-id="1f038-162">Se a impressão digital do certificado do aplicativo não corresponder à impressão digital do certificado fornecida para nós pelo desenvolvedor durante o registro, negaremos o acesso aos tokens do recurso que o aplicativo está solicitando.</span><span class="sxs-lookup"><span data-stu-id="1f038-162">If the certificate thumbprint of the application does not match the certificate thumbprint provided to us by the developer during registration, we will deny access to the tokens for the resource the application is requesting.</span></span> <span data-ttu-id="1f038-163">Essa verificação garante que apenas o aplicativo registrado pelo desenvolvedor receba tokens.</span><span class="sxs-lookup"><span data-stu-id="1f038-163">This check ensures that only the application registered by the developer receives tokens.</span></span>

<span data-ttu-id="1f038-164">**O desenvolvedor pode optar se o SDK do Microsoft Identity chama o agente ou usa o fluxo assistido por não agente.**</span><span class="sxs-lookup"><span data-stu-id="1f038-164">**The developer has the choice of if the Microsoft Identity SDK calls the broker or uses the non-broker assisted flow.**</span></span> <span data-ttu-id="1f038-165">No entanto, se o desenvolvedor optar por não usar o fluxo assistido por agente perderá a vantagem de usar as credenciais de SSO que o usuário já pode ter adicionado ao dispositivo e impede que o aplicativo seja usado com recursos corporativos fornecidos pela Microsoft aos seus clientes, como o Acesso Condicional, recursos de gerenciamento do Intune e autenticação baseada em certificado.</span><span class="sxs-lookup"><span data-stu-id="1f038-165">However if the developer chooses not to use the broker-assisted flow they lose the benefit of using SSO credentials that the user may have already added on the device and prevents their application from being used with business features Microsoft provides its customers such as Conditional Access, Intune Management capabilities, and certificate-based authentication.</span></span>

<span data-ttu-id="1f038-166">Esses logons têm os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="1f038-166">These logins have the following benefits:</span></span>

* <span data-ttu-id="1f038-167">O usuário desfruta do SSO em todos os aplicativos, independentemente do fornecedor.</span><span class="sxs-lookup"><span data-stu-id="1f038-167">User experiences SSO across all their applications no matter the vendor.</span></span>
* <span data-ttu-id="1f038-168">Seu aplicativo pode usar recursos corporativos mais avançados, como o Acesso Condicional ou usar o pacote de produtos do InTune.</span><span class="sxs-lookup"><span data-stu-id="1f038-168">Your application can use more advanced business features such as Conditional Access or use the InTune suite of products.</span></span>
* <span data-ttu-id="1f038-169">Seu aplicativo pode oferecer suporte à autenticação baseada em certificado para usuários corporativos.</span><span class="sxs-lookup"><span data-stu-id="1f038-169">Your application can support certificate-based authentication for business users.</span></span>
* <span data-ttu-id="1f038-170">Uma experiência de entrada muito mais segura, pois a identidade do aplicativo e do usuário são verificadas pelo aplicativo agente com criptografia e algoritmos de segurança adicionais.</span><span class="sxs-lookup"><span data-stu-id="1f038-170">Much more secure sign-in experience as the identity of the application and the user are verified by the broker application with additional security algorithms and encryption.</span></span>

<span data-ttu-id="1f038-171">Esses logons têm as seguintes desvantagens:</span><span class="sxs-lookup"><span data-stu-id="1f038-171">These logins have the following drawbacks:</span></span>

* <span data-ttu-id="1f038-172">No iOS, o usuário sai da experiência de seu aplicativo enquanto as credenciais são escolhidas.</span><span class="sxs-lookup"><span data-stu-id="1f038-172">In iOS the user is transitioned out of your application's experience while credentials are chosen.</span></span>
* <span data-ttu-id="1f038-173">Perda da capacidade de gerenciar a experiência de logon de seus clientes dentro de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1f038-173">Loss of the ability to manage the login experience for your customers within your application.</span></span>

<span data-ttu-id="1f038-174">Veja uma representação de como os SDKs do Microsoft Identity funcionam com os aplicativos agentes a fim de habilitar o SSO:</span><span class="sxs-lookup"><span data-stu-id="1f038-174">Here is a representation of how the Microsoft Identity SDKs work with the broker applications to enable SSO:</span></span>

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

<span data-ttu-id="1f038-175">Com essas informações em mãos, você deve ser capaz de entender melhor e implementar o SSO em seu aplicativo usando a plataforma do Microsoft Identity e os SDKs.</span><span class="sxs-lookup"><span data-stu-id="1f038-175">Armed with this background information you should be able to better understand and implement SSO within your application using the Microsoft Identity platform and SDKs.</span></span>

## <a name="enabling-cross-app-sso-using-adal"></a><span data-ttu-id="1f038-176">Habilitar SSO entre aplicativos usando a ADAL</span><span class="sxs-lookup"><span data-stu-id="1f038-176">Enabling cross-app SSO using ADAL</span></span>
<span data-ttu-id="1f038-177">Aqui, usamos o SDK do Android para ADAL a fim de:</span><span class="sxs-lookup"><span data-stu-id="1f038-177">Here we use the ADAL Android SDK to:</span></span>

* <span data-ttu-id="1f038-178">Ativar o SSO assistido por não agente para seu pacote de aplicativos</span><span class="sxs-lookup"><span data-stu-id="1f038-178">Turn on non-broker assisted SSO for your suite of apps</span></span>
* <span data-ttu-id="1f038-179">Ativar o suporte para SSO assistido por agente</span><span class="sxs-lookup"><span data-stu-id="1f038-179">Turn on support for broker-assisted SSO</span></span>

### <a name="turning-on-sso-for-non-broker-assisted-sso"></a><span data-ttu-id="1f038-180">Ativar o SSO assistido por não agente</span><span class="sxs-lookup"><span data-stu-id="1f038-180">Turning on SSO for non-broker assisted SSO</span></span>
<span data-ttu-id="1f038-181">Para SSO assistido por não agente entre aplicativos, os SDKs do Microsoft Identity gerenciam grande parte da complexidade do SSO para você.</span><span class="sxs-lookup"><span data-stu-id="1f038-181">For non-broker assisted SSO across applications the Microsoft Identity SDKs manage much of the complexity of SSO for you.</span></span> <span data-ttu-id="1f038-182">Isso inclui localizar o usuário correto no cache e manter uma lista de usuários conectados para consulta.</span><span class="sxs-lookup"><span data-stu-id="1f038-182">This includes finding the right user in the cache and maintaining a list of logged in users for you to query.</span></span>

<span data-ttu-id="1f038-183">Para habilitar o SSO entre aplicativos que você possui, é necessário fazer o seguinte:</span><span class="sxs-lookup"><span data-stu-id="1f038-183">To enable SSO across applications you own you need to do the following:</span></span>

1. <span data-ttu-id="1f038-184">Certifique-se de que todos os seus aplicativos usem a mesma ID de Cliente ou de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1f038-184">Ensure all your applications user the same Client ID or Application ID.</span></span>
2. <span data-ttu-id="1f038-185">Certifique-se de que todos os aplicativos tenham o mesmo SharedUserID definido.</span><span class="sxs-lookup"><span data-stu-id="1f038-185">Ensure all your applications have the same SharedUserID set.</span></span>
3. <span data-ttu-id="1f038-186">Certifique-se de que todos os aplicativos compartilhem o mesmo certificado de assinatura da Google Play Store para que você possa compartilhar o armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1f038-186">Ensure that all of your applications share the same signing certificate from the Google Play store so that you can share storage.</span></span>

#### <a name="step-1-using-the-same-client-id--application-id-for-all-the-applications-in-your-suite-of-apps"></a><span data-ttu-id="1f038-187">Etapa 1: Usando a mesma ID de Cliente/ID de Aplicativo para todos os aplicativos em seu pacote de aplicativos</span><span class="sxs-lookup"><span data-stu-id="1f038-187">Step 1: Using the same Client ID / Application ID for all the applications in your suite of apps</span></span>
<span data-ttu-id="1f038-188">Para que a plataforma do Microsoft Identity saiba que tem permissão para compartilhar tokens entre seus aplicativos, cada um dos aplicativos precisará compartilhar a mesma ID de Cliente ou de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1f038-188">In order for the Microsoft Identity platform to know that it's allowed to share tokens across your applications, each of your applications will need to share the same Client ID or Application ID.</span></span> <span data-ttu-id="1f038-189">Esse é o identificador exclusivo fornecido para você quando você registrou seu primeiro aplicativo no portal.</span><span class="sxs-lookup"><span data-stu-id="1f038-189">This is the unique identifier that was provided to you when you registered your first application in the portal.</span></span>

<span data-ttu-id="1f038-190">Você deve estar imaginando como poderá identificar aplicativos diferentes para o serviço do Microsoft Identity se ele usa a mesma ID de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1f038-190">You may be wondering how you will identify different apps to the Microsoft Identity service if it uses the same Application ID.</span></span> <span data-ttu-id="1f038-191">A resposta está nos **URIs de Redirecionamento**.</span><span class="sxs-lookup"><span data-stu-id="1f038-191">The answer is with the **Redirect URIs**.</span></span> <span data-ttu-id="1f038-192">Cada aplicativo pode ter vários URIs de Redirecionamento registrados no portal de integração.</span><span class="sxs-lookup"><span data-stu-id="1f038-192">Each application can have multiple Redirect URIs registered in the onboarding portal.</span></span> <span data-ttu-id="1f038-193">Cada aplicativo em seu pacote terá um URI de redirecionamento diferente.</span><span class="sxs-lookup"><span data-stu-id="1f038-193">Each app in your suite will have a different redirect URI.</span></span> <span data-ttu-id="1f038-194">Veja abaixo um exemplo de como isso acontece.</span><span class="sxs-lookup"><span data-stu-id="1f038-194">An example of how this looks is below:</span></span>

<span data-ttu-id="1f038-195">URI de Redirecionamento do App1: `msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D`</span><span class="sxs-lookup"><span data-stu-id="1f038-195">App1 Redirect URI: `msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D`</span></span>

<span data-ttu-id="1f038-196">URI de Redirecionamento do App2: `msauth://com.example.userapp1/KmB7PxIytyLkbGHuI%2UitkW%2Fejk%4E`</span><span class="sxs-lookup"><span data-stu-id="1f038-196">App2 Redirect URI: `msauth://com.example.userapp1/KmB7PxIytyLkbGHuI%2UitkW%2Fejk%4E`</span></span>

<span data-ttu-id="1f038-197">URI de Redirecionamento do App3: `msauth://com.example.userapp2/Pt85PxIyvbLkbKUtBI%2SitkW%2Fejk%9F`</span><span class="sxs-lookup"><span data-stu-id="1f038-197">App3 Redirect URI: `msauth://com.example.userapp2/Pt85PxIyvbLkbKUtBI%2SitkW%2Fejk%9F`</span></span>

<span data-ttu-id="1f038-198">....</span><span class="sxs-lookup"><span data-stu-id="1f038-198">....</span></span>

<span data-ttu-id="1f038-199">Eles estão aninhados sob a mesma ID de cliente/ID de aplicativo e são pesquisados com base no URI de redirecionamento que você retorna para nós na configuração de seu SDK.</span><span class="sxs-lookup"><span data-stu-id="1f038-199">These are nested under the same client ID / application ID and looked up based on the redirect URI you return to us in your SDK configuration.</span></span>

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


<span data-ttu-id="1f038-200">*Observe que o formato desses URIs de Redirecionamento é explicados abaixo. Você pode usar qualquer URI de Redirecionamento, a menos que você queira oferecer suporte ao agente e, nesse caso, ele deverá ser parecido com o mostrado acima*</span><span class="sxs-lookup"><span data-stu-id="1f038-200">*Note that the format of these Redirect URIs are explained below. You may use any Redirect URI unless you wish to support the broker, in which case they must look something like the above*</span></span>

#### <a name="step-2-configuring-shared-storage-in-android"></a><span data-ttu-id="1f038-201">Etapa 2: Configurando o armazenamento compartilhado no Android</span><span class="sxs-lookup"><span data-stu-id="1f038-201">Step 2: Configuring shared storage in Android</span></span>
<span data-ttu-id="1f038-202">A configuração de `SharedUserID` está além do escopo deste documento, mas é possível saber mais lendo a documentação do Google Android no [Manifesto](http://developer.android.com/guide/topics/manifest/manifest-element.html).</span><span class="sxs-lookup"><span data-stu-id="1f038-202">Setting the `SharedUserID` is beyond the scope of this document but can be learned by reading the Google Android documentation on the [Manifest](http://developer.android.com/guide/topics/manifest/manifest-element.html).</span></span> <span data-ttu-id="1f038-203">O importante é que você decida qual o nome de seu sharedUserID e usar esse nome em todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="1f038-203">What is important is that you decide what you want your sharedUserID will be called and use that across all your applications.</span></span>

<span data-ttu-id="1f038-204">Quando o `SharedUserID` estiver em todos os seus aplicativos, você estará pronto para usar o SSO.</span><span class="sxs-lookup"><span data-stu-id="1f038-204">Once you have the `SharedUserID` in all your applications you are ready to use SSO.</span></span>

> [!WARNING]
> <span data-ttu-id="1f038-205">Quando você compartilha um armazenamento em seus aplicativos, qualquer aplicativo pode excluir usuários ou pior, excluir todos os tokens em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1f038-205">When you share storage across your applications any application can delete users, or worse delete all the tokens across your application.</span></span> <span data-ttu-id="1f038-206">Isso é particularmente desastroso se você tiver aplicativos que dependem dos tokens para o trabalho em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="1f038-206">This is particularly disastrous if you have applications that rely on the tokens to do background work.</span></span> <span data-ttu-id="1f038-207">O compartilhamento do armazenamento significa que você deve ter muito cuidado com toda e qualquer operação de remoção por meio dos SDKs do Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="1f038-207">Sharing storage means that you must be very careful in any and all remove operations through the Microsoft Identity SDKs.</span></span>
> 
> 

<span data-ttu-id="1f038-208">É isso!</span><span class="sxs-lookup"><span data-stu-id="1f038-208">That's it!</span></span> <span data-ttu-id="1f038-209">Agora, o SDK do Microsoft Identity compartilhará as credenciais em todos os seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="1f038-209">The Microsoft Identity SDK will now share credentials across all your applications.</span></span> <span data-ttu-id="1f038-210">A lista de usuários também será compartilhada entre instâncias do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1f038-210">The user list will also be shared across application instances.</span></span>

### <a name="turning-on-sso-for-broker-assisted-sso"></a><span data-ttu-id="1f038-211">Ativar o SSO assistido por agente</span><span class="sxs-lookup"><span data-stu-id="1f038-211">Turning on SSO for broker assisted SSO</span></span>
<span data-ttu-id="1f038-212">A capacidade de um aplicativo usar qualquer agente instalado no dispositivo está **desativada por padrão**.</span><span class="sxs-lookup"><span data-stu-id="1f038-212">The ability for an application to use any broker that is installed on the device is **turned off by default**.</span></span> <span data-ttu-id="1f038-213">Para usar seu aplicativo com o agente, você deve fazer algumas configurações adicionais e adicionar algum código ao seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1f038-213">In order to use your application with the broker you must do some additional configuration and add some code to your application.</span></span>

<span data-ttu-id="1f038-214">Execute estas etapas:</span><span class="sxs-lookup"><span data-stu-id="1f038-214">The steps to follow are:</span></span>

1. <span data-ttu-id="1f038-215">Habilitar o modo de agente na chamada do código do aplicativo para o SDK do MS</span><span class="sxs-lookup"><span data-stu-id="1f038-215">Enable broker mode in your application code's call to the MS SDK</span></span>
2. <span data-ttu-id="1f038-216">Estabelecer um novo URI de redirecionamento e fornecê-lo ao aplicativo e no registro do aplicativo</span><span class="sxs-lookup"><span data-stu-id="1f038-216">Establish a new redirect URI and provide that to both the app and your app registration</span></span>
3. <span data-ttu-id="1f038-217">Configurar as permissões corretas no manifesto do Android</span><span class="sxs-lookup"><span data-stu-id="1f038-217">Setting up the correct permissions in the Android manifest</span></span>

#### <a name="step-1-enable-broker-mode-in-your-application"></a><span data-ttu-id="1f038-218">Etapa 1: habilitar o modo de agente em seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="1f038-218">Step 1: Enable broker mode in your application</span></span>
<span data-ttu-id="1f038-219">A capacidade de seu aplicativo de usar o agente é ativada quando você cria as “configurações” ou configuração inicial da sua instância de autenticação.</span><span class="sxs-lookup"><span data-stu-id="1f038-219">The ability for your application to use the broker is turned on when you create the "settings" or initial setup of your Authentication instance.</span></span> <span data-ttu-id="1f038-220">Faça isso configurando o tipo ApplicationSettings em seu código:</span><span class="sxs-lookup"><span data-stu-id="1f038-220">You do this by setting your ApplicationSettings type in your code:</span></span>

```
AuthenticationSettings.Instance.setUseBroker(true);
```


#### <a name="step-2-establish-a-new-redirect-uri-with-your-url-scheme"></a><span data-ttu-id="1f038-221">Etapa 2: Estabelecer um novo URI de redirecionamento com seu esquema de URL</span><span class="sxs-lookup"><span data-stu-id="1f038-221">Step 2: Establish a new redirect URI with your URL Scheme</span></span>
<span data-ttu-id="1f038-222">Para garantir que sempre retornarmos os tokens de credencial para o aplicativo correto, precisamos ter certeza de que chamamos seu aplicativo de forma que o sistema operacional Android possa verificar.</span><span class="sxs-lookup"><span data-stu-id="1f038-222">In order to ensure that we always return the credential tokens to the correct application, we need to make sure we call back to your application in a way that the Android operating system can verify.</span></span> <span data-ttu-id="1f038-223">O sistema operacional Android usa o hash do certificado no Google Play Store.</span><span class="sxs-lookup"><span data-stu-id="1f038-223">The Android operating system uses the hash of the certificate in the Google Play store.</span></span> <span data-ttu-id="1f038-224">Isso não pode ser falsificado por um aplicativo mal-intencionado.</span><span class="sxs-lookup"><span data-stu-id="1f038-224">This cannot be spoofed by a rogue application.</span></span> <span data-ttu-id="1f038-225">Portanto, podemos aproveitar isso juntamente com o URI do nosso aplicativo de agente para garantir que os tokens sejam retornados para o aplicativo correto.</span><span class="sxs-lookup"><span data-stu-id="1f038-225">Therefore, we leverage this along with the URI of our broker application to ensure that the tokens are returned to the correct application.</span></span> <span data-ttu-id="1f038-226">Precisamos que você estabeleça esse URI de redirecionamento exclusivo em seu aplicativo e defina como um URI de Redirecionamento em nosso portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="1f038-226">We require you to establish this unique redirect URI both in your application and set as a Redirect URI in our developer portal.</span></span>

<span data-ttu-id="1f038-227">O URI de redirecionamento deve ser no formato correto de:</span><span class="sxs-lookup"><span data-stu-id="1f038-227">Your redirect URI must be in the proper form of:</span></span>

`msauth://packagename/Base64UrlencodedSignature`

<span data-ttu-id="1f038-228">ex: *msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D*</span><span class="sxs-lookup"><span data-stu-id="1f038-228">ex: *msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D*</span></span>

<span data-ttu-id="1f038-229">Esse URI de Redirecionamento deve ser especificado no registro de seu aplicativo usando o [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1f038-229">This Redirect URI needs to be specified in your app registration using the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="1f038-230">Para saber mais sobre o registro de aplicativo do Azure AD, confira [Integração com o Azure Active Directory](active-directory-how-to-integrate.md).</span><span class="sxs-lookup"><span data-stu-id="1f038-230">For more information on Azure AD app registration, see [Integrating with Azure Active Directory](active-directory-how-to-integrate.md).</span></span>

#### <a name="step-3-set-up-the-correct-permissions-in-your-application"></a><span data-ttu-id="1f038-231">Etapa 3: Configurar as permissões corretas em seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="1f038-231">Step 3: Set up the correct permissions in your application</span></span>
<span data-ttu-id="1f038-232">Nosso aplicativo de agente no Android usa o recurso de Gerenciador de Contas do sistema operacional Android para gerenciar credenciais nos aplicativos.</span><span class="sxs-lookup"><span data-stu-id="1f038-232">Our broker application in Android uses the Accounts Manager feature of the Android OS to manage credentials across applications.</span></span> <span data-ttu-id="1f038-233">Para usar o agente no Android, seu manifesto de aplicativo deve ter permissões para usar contas do Gerenciador de Contas.</span><span class="sxs-lookup"><span data-stu-id="1f038-233">In order to use the broker in Android your app manifest must have permissions to use AccountManager accounts.</span></span> <span data-ttu-id="1f038-234">Isso é discutido detalhadamente na [documentação do Google para o Gerente de Contas](http://developer.android.com/reference/android/accounts/AccountManager.html)</span><span class="sxs-lookup"><span data-stu-id="1f038-234">This is discussed in detail in the [Google documentation for Account Manager here](http://developer.android.com/reference/android/accounts/AccountManager.html)</span></span>

<span data-ttu-id="1f038-235">Em particular, essas permissões são:</span><span class="sxs-lookup"><span data-stu-id="1f038-235">In particular, these permissions are:</span></span>

```
GET_ACCOUNTS
USE_CREDENTIALS
MANAGE_ACCOUNTS
```

### <a name="youve-configured-sso"></a><span data-ttu-id="1f038-236">Você configurou o SSO!</span><span class="sxs-lookup"><span data-stu-id="1f038-236">You've configured SSO!</span></span>
<span data-ttu-id="1f038-237">Agora, o SDK do Microsoft Identity compartilhará automaticamente as credenciais em seus aplicativos e invocará o agente se ele estiver presente em seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1f038-237">Now the Microsoft Identity SDK will automatically both share credentials across your applications and invoke the broker if it's present on their device.</span></span>

