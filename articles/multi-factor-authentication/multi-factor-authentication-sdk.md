---
title: aaaMFA software development kit para aplicativos personalizados | Microsoft Docs
description: "Este artigo mostra como toodownload e use Olá verificação do SDK do Azure MFA tooenable em duas etapas para seus aplicativos personalizados."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 1c152f67-be02-42a5-a0c7-246fb6b34377
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: 10e02e844bf3928575bfca79dbc34717a31a08b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="building-multi-factor-authentication-into-custom-apps-sdk"></a><span data-ttu-id="8425b-103">Criando uma autenticação multifator em aplicativos personalizados (SDK)</span><span class="sxs-lookup"><span data-stu-id="8425b-103">Building Multi-Factor Authentication into Custom Apps (SDK)</span></span>

<span data-ttu-id="8425b-104">Olá possibilita a Azure multi-Factor Authentication Software Development Kit (SDK) Olá que criação de verificação em duas etapas diretamente na entrada ou transação processos de aplicativos no seu locatário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="8425b-104">hello Azure Multi-Factor Authentication Software Development Kit (SDK) lets you build two-step verification directly into hello sign-in or transaction processes of applications in your Azure AD tenant.</span></span>

<span data-ttu-id="8425b-105">Olá SDK multi-Factor Authentication está disponível para c#, Visual Basic (.NET), Java, Perl, PHP e Ruby.</span><span class="sxs-lookup"><span data-stu-id="8425b-105">hello Multi-Factor Authentication SDK is available for C#, Visual Basic (.NET), Java, Perl, PHP, and Ruby.</span></span> <span data-ttu-id="8425b-106">Olá SDK fornece um wrapper fino em torno de verificação em duas etapas.</span><span class="sxs-lookup"><span data-stu-id="8425b-106">hello SDK provides a thin wrapper around two-step verification.</span></span> <span data-ttu-id="8425b-107">Ele inclui tudo o que você precisa toowrite seu código, incluindo arquivos de código fonte comentados, arquivos de exemplo e um arquivo Leiame detalhado.</span><span class="sxs-lookup"><span data-stu-id="8425b-107">It includes everything you need toowrite your code, including commented source code files, example files, and a detailed ReadMe file.</span></span> <span data-ttu-id="8425b-108">Cada SDK também inclui um certificado e a chave privada para criptografar transações que são exclusivo tooyour provedor de autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="8425b-108">Each SDK also includes a certificate and private key for encrypting transactions that are unique tooyour Multi-Factor Authentication Provider.</span></span> <span data-ttu-id="8425b-109">Contanto que você tenha um provedor, você pode baixar Olá SDK nos tantos idiomas e formatos conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="8425b-109">As long as you have a provider, you can download hello SDK in as many languages and formats as you need.</span></span>

<span data-ttu-id="8425b-110">estrutura Olá Olá APIs no SDK multi-Factor Authentication da saudação é simple.</span><span class="sxs-lookup"><span data-stu-id="8425b-110">hello structure of hello APIs in hello Multi-Factor Authentication SDK is simple.</span></span> <span data-ttu-id="8425b-111">Fazer com que uma função chamada tooan API com parâmetros de opção multifator hello (como o modo de verificação) e dados de usuário (como toocall de número de telefone de saudação ou Olá PIN número toovalidate).</span><span class="sxs-lookup"><span data-stu-id="8425b-111">Make a single function call tooan API with hello multi-factor option parameters (like verification mode) and user data (like hello telephone number toocall or hello PIN number toovalidate).</span></span> <span data-ttu-id="8425b-112">Olá, APIs traduzem Olá chamada de função em toohello de solicitações de serviços web serviço baseado em nuvem do Azure multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="8425b-112">hello APIs translate hello function call into web services requests toohello cloud-based Azure Multi-Factor Authentication Service.</span></span> <span data-ttu-id="8425b-113">Todas as chamadas devem incluir um certificado privado de toohello de referência que é incluído em cada SDK.</span><span class="sxs-lookup"><span data-stu-id="8425b-113">All calls must include a reference toohello private certificate that is included in every SDK.</span></span>

<span data-ttu-id="8425b-114">Como Olá APIs não têm acesso toousers registrado no Active Directory do Azure, você deve fornecer informações de usuário em um arquivo ou banco de dados.</span><span class="sxs-lookup"><span data-stu-id="8425b-114">Because hello APIs do not have access toousers registered in Azure Active Directory, you must provide user information in a file or database.</span></span> <span data-ttu-id="8425b-115">Além disso, Olá APIs não fornecem recursos de gerenciamento de registro ou de usuário, portanto, você precisa toobuild esses processos em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8425b-115">Also, hello APIs do not provide enrollment or user management features, so you need toobuild these processes into your application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8425b-116">toodownload Olá SDK, você precisa toocreate um provedor de autenticação multifator do Azure, mesmo se você tiver licenças de Azure MFA, AAD Premium ou EMS.</span><span class="sxs-lookup"><span data-stu-id="8425b-116">toodownload hello SDK, you need toocreate an Azure Multi-Factor Auth Provider even if you have Azure MFA, AAD Premium, or EMS licenses.</span></span> <span data-ttu-id="8425b-117">Se você criar um provedor de autenticação multifator do Azure para essa finalidade e já tiver licenças, verifique se toocreate Olá provedor com hello **por usuário habilitado** modelo.</span><span class="sxs-lookup"><span data-stu-id="8425b-117">If you create an Azure Multi-Factor Auth Provider for this purpose and already have licenses, make sure toocreate hello Provider with hello **Per Enabled User** model.</span></span> <span data-ttu-id="8425b-118">Em seguida, vincule toohello diretório Olá provedor contém Olá licenças de Azure MFA, o Azure AD Premium ou EMS.</span><span class="sxs-lookup"><span data-stu-id="8425b-118">Then, link hello Provider toohello directory that contains hello Azure MFA, Azure AD Premium, or EMS licenses.</span></span> <span data-ttu-id="8425b-119">Essa configuração garante que você será cobrado somente se você tiver mais de usuários exclusivos usando Olá SDK que número de saudação de licenças que você possui.</span><span class="sxs-lookup"><span data-stu-id="8425b-119">This configuration ensures that you are only billed if you have more unique users using hello SDK than hello number of licenses you own.</span></span>


## <a name="download-hello-sdk"></a><span data-ttu-id="8425b-120">Baixe o SDK de saudação</span><span class="sxs-lookup"><span data-stu-id="8425b-120">Download hello SDK</span></span>
<span data-ttu-id="8425b-121">Baixar Olá SDK do Azure multi-Factor requer um [provedor do Azure multi-Factor Auth](multi-factor-authentication-get-started-auth-provider.md).</span><span class="sxs-lookup"><span data-stu-id="8425b-121">Downloading hello Azure Multi-Factor SDK requires an [Azure Multi-Factor Auth Provider](multi-factor-authentication-get-started-auth-provider.md).</span></span>  <span data-ttu-id="8425b-122">Isso requer uma assinatura completa do Azure, mesmo que você já possua as licenças do Azure MFA, Azure AD Premium ou Enterprise Mobility Suite.</span><span class="sxs-lookup"><span data-stu-id="8425b-122">This requires a full Azure subscription, even if Azure MFA, Azure AD Premium, or Enterprise Mobility Suite licenses are owned.</span></span>  <span data-ttu-id="8425b-123">Olá toodownload SDK, navegue toohello Portal de gerenciamento de vários fatores.</span><span class="sxs-lookup"><span data-stu-id="8425b-123">toodownload hello SDK, navigate toohello Multi-Factor Management Portal.</span></span> <span data-ttu-id="8425b-124">Você pode acessar portal Olá Gerenciando Olá provedor de autenticação multifator diretamente, ou clicando Olá **"Go toohello portal"** link na página de configurações do serviço MFA de saudação.</span><span class="sxs-lookup"><span data-stu-id="8425b-124">You can reach hello portal either by managing hello Multi-Factor Auth Provider directly, or by clicking hello **"Go toohello portal"** link on hello MFA service settings page.</span></span>

### <a name="download-from-hello-azure-classic-portal"></a><span data-ttu-id="8425b-125">Download de saudação portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="8425b-125">Download from hello Azure classic portal</span></span>
1. <span data-ttu-id="8425b-126">Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com) como um administrador.</span><span class="sxs-lookup"><span data-stu-id="8425b-126">Sign in toohello [Azure classic portal](https://manage.windowsazure.com) as an Administrator.</span></span>
2. <span data-ttu-id="8425b-127">Olá esquerda, selecione **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8425b-127">On hello left, select **Active Directory**.</span></span>
3. <span data-ttu-id="8425b-128">Na página do Active Directory, Olá, em selecione top Olá **provedores de autenticação multifator**</span><span class="sxs-lookup"><span data-stu-id="8425b-128">On hello Active Directory page, at hello top select **Multi-Factor Auth Providers**</span></span>
4. <span data-ttu-id="8425b-129">Na parte inferior da saudação selecione **gerenciar**.</span><span class="sxs-lookup"><span data-stu-id="8425b-129">At hello bottom select **Manage**.</span></span> <span data-ttu-id="8425b-130">Uma nova página é aberta.</span><span class="sxs-lookup"><span data-stu-id="8425b-130">A new page opens.</span></span>
5. <span data-ttu-id="8425b-131">Na saudação à esquerda, na parte inferior da saudação, clique em **SDK**.</span><span class="sxs-lookup"><span data-stu-id="8425b-131">On hello left, at hello bottom, click **SDK**.</span></span>
   <span data-ttu-id="8425b-132"><center>![Baixar](./media/multi-factor-authentication-sdk/download.png)</center></span><span class="sxs-lookup"><span data-stu-id="8425b-132"><center>![Download](./media/multi-factor-authentication-sdk/download.png)</center></span></span>
6. <span data-ttu-id="8425b-133">Selecione o idioma de saudação desejado e clicar em links de download associadas uma saudação.</span><span class="sxs-lookup"><span data-stu-id="8425b-133">Select hello language you want and click one hello associated download links.</span></span>
7. <span data-ttu-id="8425b-134">Salve o download de saudação.</span><span class="sxs-lookup"><span data-stu-id="8425b-134">Save hello download.</span></span>

### <a name="download-from-hello-service-settings"></a><span data-ttu-id="8425b-135">Fazer o download das configurações de serviço Olá</span><span class="sxs-lookup"><span data-stu-id="8425b-135">Download from hello service settings</span></span>
1. <span data-ttu-id="8425b-136">Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com) como um administrador.</span><span class="sxs-lookup"><span data-stu-id="8425b-136">Sign in toohello [Azure classic portal](https://manage.windowsazure.com) as an Administrator.</span></span>
2. <span data-ttu-id="8425b-137">Olá esquerda, selecione **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8425b-137">On hello left, select **Active Directory**.</span></span>
3. <span data-ttu-id="8425b-138">Clique duas vezes em sua instância do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="8425b-138">Double-click your instance of Azure AD.</span></span>
4. <span data-ttu-id="8425b-139">Com clique superior Olá **configurar**</span><span class="sxs-lookup"><span data-stu-id="8425b-139">At hello top click **Configure**</span></span>
5. <span data-ttu-id="8425b-140">Em autenticação multifator, selecione **Gerenciar configurações de serviço**
   ![Download](./media/multi-factor-authentication-sdk/download2.png)</span><span class="sxs-lookup"><span data-stu-id="8425b-140">Under multi-factor authentication, select **Manage service settings**
![Download](./media/multi-factor-authentication-sdk/download2.png)</span></span>
6. <span data-ttu-id="8425b-141">Na página de configurações de serviços hello, na parte inferior da saudação da tela hello clique **Go toohello portal**.</span><span class="sxs-lookup"><span data-stu-id="8425b-141">On hello services settings page, at hello bottom of hello screen click **Go toohello portal**.</span></span> <span data-ttu-id="8425b-142">Uma nova página é aberta.</span><span class="sxs-lookup"><span data-stu-id="8425b-142">A new page opens.</span></span>
   <span data-ttu-id="8425b-143">![Baixar](./media/multi-factor-authentication-sdk/download3a.png)</span><span class="sxs-lookup"><span data-stu-id="8425b-143">![Download](./media/multi-factor-authentication-sdk/download3a.png)</span></span>
7. <span data-ttu-id="8425b-144">Na saudação à esquerda, na parte inferior da saudação, clique em **SDK**.</span><span class="sxs-lookup"><span data-stu-id="8425b-144">On hello left, at hello bottom, click **SDK**.</span></span>
8. <span data-ttu-id="8425b-145">Selecione o idioma de saudação desejado e clicar em links de download associadas uma saudação.</span><span class="sxs-lookup"><span data-stu-id="8425b-145">Select hello language you want and click one hello associated download links.</span></span>
9. <span data-ttu-id="8425b-146">Salve o download de saudação.</span><span class="sxs-lookup"><span data-stu-id="8425b-146">Save hello download.</span></span>

## <a name="whats-in-hello-sdk"></a><span data-ttu-id="8425b-147">Novidades no hello SDK</span><span class="sxs-lookup"><span data-stu-id="8425b-147">What's in hello SDK</span></span>
<span data-ttu-id="8425b-148">Olá SDK inclui Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="8425b-148">hello SDK includes hello following items:</span></span>

* <span data-ttu-id="8425b-149">**LEIAME**.</span><span class="sxs-lookup"><span data-stu-id="8425b-149">**README**.</span></span> <span data-ttu-id="8425b-150">Explica como toouse Olá APIs de autenticação multifator em um aplicativo novo ou existente.</span><span class="sxs-lookup"><span data-stu-id="8425b-150">Explains how toouse hello Multi-Factor Authentication APIs in a new or existing application.</span></span>
* <span data-ttu-id="8425b-151">**Arquivos de origem** para Autenticação Multifator</span><span class="sxs-lookup"><span data-stu-id="8425b-151">**Source files** for Multi-Factor Authentication</span></span>
* <span data-ttu-id="8425b-152">**Certificado de cliente** que você use toocommunicate com hello serviço multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="8425b-152">**Client certificate** that you use toocommunicate with hello Multi-Factor Authentication service</span></span>
* <span data-ttu-id="8425b-153">**Chave privada** certificado Olá</span><span class="sxs-lookup"><span data-stu-id="8425b-153">**Private key** for hello certificate</span></span>
* <span data-ttu-id="8425b-154">**Resultados da chamada.**</span><span class="sxs-lookup"><span data-stu-id="8425b-154">**Call results.**</span></span> <span data-ttu-id="8425b-155">Uma lista de códigos do resultado da chamada.</span><span class="sxs-lookup"><span data-stu-id="8425b-155">A list of call result codes.</span></span> <span data-ttu-id="8425b-156">tooopen esse arquivo, use um aplicativo com formatação de texto, como o WordPad.</span><span class="sxs-lookup"><span data-stu-id="8425b-156">tooopen this file, use an application with text formatting, such as WordPad.</span></span> <span data-ttu-id="8425b-157">Olá Use chamar tootest de códigos de resultado e solucionar problemas de implementação de saudação do multi-Factor Authentication em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8425b-157">Use hello call result codes tootest and troubleshoot hello implementation of Multi-Factor Authentication in your application.</span></span> <span data-ttu-id="8425b-158">Eles não são códigos de status de autenticação.</span><span class="sxs-lookup"><span data-stu-id="8425b-158">They are not authentication status codes.</span></span>
* <span data-ttu-id="8425b-159">**Exemplos.**</span><span class="sxs-lookup"><span data-stu-id="8425b-159">**Examples.**</span></span> <span data-ttu-id="8425b-160">Código de exemplo para uma implementação básica de trabalho do Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="8425b-160">Sample code for a basic working implementation of Multi-Factor Authentication.</span></span>

> [!WARNING]
> <span data-ttu-id="8425b-161">certificado de cliente de saudação é um certificado privado único que foi gerado especialmente para você.</span><span class="sxs-lookup"><span data-stu-id="8425b-161">hello client certificate is a unique private certificate that was generated especially for you.</span></span> <span data-ttu-id="8425b-162">Não compartilhe nem perca este arquivo.</span><span class="sxs-lookup"><span data-stu-id="8425b-162">Do not share or lose this file.</span></span> <span data-ttu-id="8425b-163">É a segurança de saudação tooensuring chave das suas comunicações com o serviço de autenticação multifator hello.</span><span class="sxs-lookup"><span data-stu-id="8425b-163">It’s your key tooensuring hello security of your communications with hello Multi-Factor Authentication service.</span></span>

## <a name="code-sample"></a><span data-ttu-id="8425b-164">Exemplo de código</span><span class="sxs-lookup"><span data-stu-id="8425b-164">Code sample</span></span>
<span data-ttu-id="8425b-165">Este exemplo de código mostra como toouse Olá APIs em Olá voz de modo padrão do SDK do Azure multi-Factor Authentication tooadd chamar aplicativo tooyour de verificação.</span><span class="sxs-lookup"><span data-stu-id="8425b-165">This code sample shows you how toouse hello APIs in hello Azure Multi-Factor Authentication SDK tooadd standard mode voice call verification tooyour application.</span></span> <span data-ttu-id="8425b-166">O modo padrão é uma chamada telefônica que Olá tooby do usuário responde pressionando a tecla # de saudação.</span><span class="sxs-lookup"><span data-stu-id="8425b-166">Standard mode is a telephone call that hello user responds tooby pressing hello # key.</span></span>

<span data-ttu-id="8425b-167">Este exemplo usa Olá c# .NET 2.0 SDK multi-Factor Authentication em um aplicativo ASP.NET básico com a lógica do lado do servidor c#, mas o processo de saudação é semelhante em outras linguagens.</span><span class="sxs-lookup"><span data-stu-id="8425b-167">This example uses hello C# .NET 2.0 Multi-Factor Authentication SDK in a basic ASP.NET application with C# server-side logic, but hello process is similar in other languages.</span></span> <span data-ttu-id="8425b-168">Como Olá SDK inclui arquivos de origem, arquivos não executáveis, você pode criar arquivos de saudação e faz referência a eles ou incluí-los diretamente em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8425b-168">Because hello SDK includes source files, not executable files, you can build hello files and reference them or include them directly in your application.</span></span>

> [!NOTE]
> <span data-ttu-id="8425b-169">Ao implementar a autenticação multifator, use métodos adicionais de saudação (chamada telefônica ou mensagem de texto) como toosupplement verificação secundária ou terciária seu método de autenticação primária (nome de usuário e senha).</span><span class="sxs-lookup"><span data-stu-id="8425b-169">When implementing Multi-Factor Authentication, use hello additional methods (phone call or text message) as secondary or tertiary verification toosupplement your primary authentication method (username and password).</span></span> <span data-ttu-id="8425b-170">Esses métodos não foram desenvolvidos para serem usados como métodos de autenticação primária.</span><span class="sxs-lookup"><span data-stu-id="8425b-170">These methods are not designed as primary authentication methods.</span></span>

### <a name="code-sample-overview"></a><span data-ttu-id="8425b-171">Visão geral do exemplo de código</span><span class="sxs-lookup"><span data-stu-id="8425b-171">Code Sample Overview</span></span>
<span data-ttu-id="8425b-172">Esse código de exemplo para um aplicativo de demonstração simples da web usa uma chamada telefônica com autenticação # resposta de chave tooverify saudação do usuário.</span><span class="sxs-lookup"><span data-stu-id="8425b-172">This sample code for a simple web demo application uses a telephone call with a # key response tooverify hello user's authentication.</span></span> <span data-ttu-id="8425b-173">Esse fator de chamada telefônica é conhecido no Multi-Factor Authentication como modo padrão.</span><span class="sxs-lookup"><span data-stu-id="8425b-173">This telephone call factor is known in Multi-Factor Authentication as standard mode.</span></span>

<span data-ttu-id="8425b-174">código do lado do cliente Olá não inclui nenhum elemento específico de autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="8425b-174">hello client-side code does not include any Multi-Factor Authentication-specific elements.</span></span> <span data-ttu-id="8425b-175">Como fatores de autenticação adicionais de saudação são independentes da autenticação primária Olá, você pode adicioná-los sem alterar a interface de logon existente hello.</span><span class="sxs-lookup"><span data-stu-id="8425b-175">Because hello additional authentication factors are independent of hello primary authentication, you can add them without changing hello existing sign-on interface.</span></span> <span data-ttu-id="8425b-176">Olá APIs em Olá SDK multi-Factor lhe permitem personalizar a experiência do usuário hello, mas talvez não seja necessário toochange nada em todos os.</span><span class="sxs-lookup"><span data-stu-id="8425b-176">hello APIs in hello Multi-Factor SDK let you customize hello user experience, but you might not need toochange anything at all.</span></span>

<span data-ttu-id="8425b-177">código do servidor de saudação adiciona a autenticação de modo padrão na etapa 2.</span><span class="sxs-lookup"><span data-stu-id="8425b-177">hello server-side code adds standard-mode authentication in Step 2.</span></span> <span data-ttu-id="8425b-178">Ele cria um objeto de PfAuthParams com parâmetros de saudação que são necessários para a verificação de modo padrão: nome de usuário, o número e o modo de telefone e Olá certificado de cliente caminho toohello (CertFilePath), que é necessário em cada chamada.</span><span class="sxs-lookup"><span data-stu-id="8425b-178">It creates a PfAuthParams object with hello parameters that are required for standard-mode verification: username, telephone number, and mode, and hello path toohello client certificate (CertFilePath), which is required in each call.</span></span> <span data-ttu-id="8425b-179">Para ver uma demonstração de todos os parâmetros no PfAuthParams, consulte o arquivo de exemplo hello em Olá SDK.</span><span class="sxs-lookup"><span data-stu-id="8425b-179">For a demonstration of all parameters in PfAuthParams, see hello Example file in hello SDK.</span></span>

<span data-ttu-id="8425b-180">Em seguida, o código de saudação passa função pf_authenticate() do hello PfAuthParams objeto toohello.</span><span class="sxs-lookup"><span data-stu-id="8425b-180">Next, hello code passes hello PfAuthParams object toohello pf_authenticate() function.</span></span> <span data-ttu-id="8425b-181">valor de retorno de saudação indica êxito hello ou falha de autenticação de saudação.</span><span class="sxs-lookup"><span data-stu-id="8425b-181">hello return value indicates hello success or failure of hello authentication.</span></span> <span data-ttu-id="8425b-182">Olá parâmetros, callStatus e errorID, contêm informações de resultado de chamada adicional.</span><span class="sxs-lookup"><span data-stu-id="8425b-182">hello out parameters, callStatus, and errorID, contain additional call result information.</span></span> <span data-ttu-id="8425b-183">códigos de resultado de chamada Hello estão documentados no arquivo de resultados de chamada hello em Olá SDK.</span><span class="sxs-lookup"><span data-stu-id="8425b-183">hello call result codes are documented in hello call results file in hello SDK.</span></span>

<span data-ttu-id="8425b-184">Essa implementação mínima pode ser escrita apenas em algumas linhas.</span><span class="sxs-lookup"><span data-stu-id="8425b-184">This minimal implementation can be written in a few lines.</span></span> <span data-ttu-id="8425b-185">No entanto, no código de produção, você inclui tratamento de erro mais sofisticado, código adicional de banco de dados e uma experiência de usuário aprimorada.</span><span class="sxs-lookup"><span data-stu-id="8425b-185">However, in production code, you would include more sophisticated error handling, additional database code, and an enhanced user experience.</span></span>

### <a name="web-client-code"></a><span data-ttu-id="8425b-186">Código do cliente Web</span><span class="sxs-lookup"><span data-stu-id="8425b-186">Web Client Code</span></span>
<span data-ttu-id="8425b-187">a seguir Olá é código de cliente da web para uma página de demonstração.</span><span class="sxs-lookup"><span data-stu-id="8425b-187">hello following is web client code for a demo page.</span></span>

    <%@ Page Language="C#" AutoEventWireup="true" CodeFile="Default.aspx.cs" Inherits="\_Default" %>

    <!DOCTYPE html>

    <html xmlns="http://www.w3.org/1999/xhtml">
    <head runat="server">
    <title>Multi-Factor Authentication Demo</title>
    </head>
    <body>
    <h1>Azure Multi-Factor Authentication Demo</h1>
    <form id="form1" runat="server">

    <div style="width:auto; float:left">
    Username:&nbsp;<br />
    Password:&nbsp;<br />
    </div>

    <div">
    <asp:TextBox id="username" runat="server" width="100px"/><br />
    <asp:Textbox id="password" runat="server" width="100px" TextMode="password" /><br />
    </div>

    <asp:Button id="btnSubmit" runat="server" Text="Log in" onClick="btnSubmit_Click"/>

    <p><asp:Label ID="lblResult" runat="server"></asp:Label></p>

    </form>
    </body>
    </html>


### <a name="server-side-code"></a><span data-ttu-id="8425b-188">Código do servidor</span><span class="sxs-lookup"><span data-stu-id="8425b-188">Server-Side Code</span></span>
<span data-ttu-id="8425b-189">Olá após o código do lado do servidor, autenticação multifator é configurada e executada na etapa 2.</span><span class="sxs-lookup"><span data-stu-id="8425b-189">In hello following server-side code, Multi-Factor Authentication is configured and run in Step 2.</span></span> <span data-ttu-id="8425b-190">Modo padrão (MODE_STANDARD) é que um usuário de saudação do telefonema toowhich responde pressionando a tecla # de saudação.</span><span class="sxs-lookup"><span data-stu-id="8425b-190">Standard mode (MODE_STANDARD) is a telephone call toowhich hello user responds by pressing hello # key.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.Web.UI;
    using System.Web.UI.WebControls;

    public partial class \_Default : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
        }

        protected void btnSubmit_Click(object sender, EventArgs e)
        {
            // Step 1: Validate hello username and password
            if (username.Text != "Contoso" || password.Text != "password")
            {
                lblResult.ForeColor = System.Drawing.Color.Red;
                lblResult.Text = "Username or password incorrect.";
            }
            else
            {
                // Step 2: Perform multi-factor authentication

                // Add call details from hello user database.
                PfAuthParams pfAuthParams = new PfAuthParams();
                pfAuthParams.Username = username.Text;
                pfAuthParams.Phone = "5555555555";
                pfAuthParams.Mode = pf_auth.MODE_STANDARD;

                // Specify a client certificate
                // NOTE: This file contains hello private key for hello client
                // certificate. It must be stored with appropriate file
                // permissions.
                pfAuthParams.CertFilePath = "c:\\cert_key.p12";

                // Perform phone-based authentication
                int callStatus;
                int errorId;

                if(pf_auth.pf_authenticate(pfAuthParams, out callStatus, out errorId))
                {
                    lblResult.ForeColor = System.Drawing.Color.Green;
                    lblResult.Text = "Multi-Factor Authentication succeeded.";
                }
                else
                {
                    lblResult.ForeColor = System.Drawing.Color.Red;
                    lblResult.Text = "Multi-Factor Authentication failed.";
                }
            }

        }
    }
