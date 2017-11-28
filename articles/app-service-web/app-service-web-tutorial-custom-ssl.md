---
title: aaaBind um SSL personalizado existente tooAzure os aplicativos Web de certificado | Microsoft Docs
description: "Saiba tootoobind um aplicativo da web personalizado SSL certificado tooyour, back-end do aplicativo móvel ou aplicativo de API no serviço de aplicativo do Azure."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 5d5bf588-b0bb-4c6d-8840-1b609cfb5750
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 06/23/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 3503ba9f96c8ea8d18451e8bf9a9b441797ef44d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="bind-an-existing-custom-ssl-certificate-tooazure-web-apps"></a><span data-ttu-id="dde0e-103">Associar um tooAzure de certificado SSL de personalizada existente aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="dde0e-103">Bind an existing custom SSL certificate tooAzure Web Apps</span></span>

<span data-ttu-id="dde0e-104">Os aplicativos Web do Azure fornecem um serviço de hospedagem na Web altamente escalonável, com aplicação automática de patches.</span><span class="sxs-lookup"><span data-stu-id="dde0e-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="dde0e-105">Este tutorial mostra como toobind um SSL personalizado de certificado que você adquirido de uma autoridade de certificação confiável muito[aplicativos Web do Azure](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dde0e-105">This tutorial shows you how toobind a custom SSL certificate that you purchased from a trusted certificate authority too[Azure Web Apps](app-service-web-overview.md).</span></span> <span data-ttu-id="dde0e-106">Quando você terminar, você será capaz de tooaccess seu aplicativo web no ponto de extremidade HTTPS de saudação do seu domínio DNS personalizado.</span><span class="sxs-lookup"><span data-stu-id="dde0e-106">When you're finished, you'll be able tooaccess your web app at hello HTTPS endpoint of your custom DNS domain.</span></span>

![Aplicativo Web com certificado SSL personalizado](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

<span data-ttu-id="dde0e-108">Neste tutorial, você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="dde0e-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="dde0e-109">Atualizar o tipo de preço do aplicativo</span><span class="sxs-lookup"><span data-stu-id="dde0e-109">Upgrade your app's pricing tier</span></span>
> * <span data-ttu-id="dde0e-110">Associar seu tooApp de certificado SSL personalizado serviço</span><span class="sxs-lookup"><span data-stu-id="dde0e-110">Bind your custom SSL certificate tooApp Service</span></span>
> * <span data-ttu-id="dde0e-111">Impor HTTPS para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="dde0e-111">Enforce HTTPS for your app</span></span>
> * <span data-ttu-id="dde0e-112">Automatizar a associação de certificado SSL com scripts</span><span class="sxs-lookup"><span data-stu-id="dde0e-112">Automate SSL certificate binding with scripts</span></span>

> [!NOTE]
> <span data-ttu-id="dde0e-113">Se você precisar tooget um certificado SSL personalizado, você pode obtê-la no portal do Azure de saudação diretamente e associá-lo tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="dde0e-113">If you need tooget a custom SSL certificate, you can get one in hello Azure portal directly and bind it tooyour web app.</span></span> <span data-ttu-id="dde0e-114">Siga Olá [tutorial de certificados de serviço de aplicativo](web-sites-purchase-ssl-web-site.md).</span><span class="sxs-lookup"><span data-stu-id="dde0e-114">Follow hello [App Service Certificates tutorial](web-sites-purchase-ssl-web-site.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dde0e-115">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="dde0e-115">Prerequisites</span></span>

<span data-ttu-id="dde0e-116">toocomplete este tutorial:</span><span class="sxs-lookup"><span data-stu-id="dde0e-116">toocomplete this tutorial:</span></span>

- [<span data-ttu-id="dde0e-117">Crie um aplicativo do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="dde0e-117">Create an App Service app</span></span>](/azure/app-service/)
- [<span data-ttu-id="dde0e-118">Mapear um nome DNS personalizado, tooyour aplicativo da web</span><span class="sxs-lookup"><span data-stu-id="dde0e-118">Map a custom DNS name tooyour web app</span></span>](app-service-web-tutorial-custom-domain.md)
- <span data-ttu-id="dde0e-119">Adquirir um certificado SSL de uma autoridade de certificado confiável</span><span class="sxs-lookup"><span data-stu-id="dde0e-119">Acquire an SSL certificate from a trusted certificate authority</span></span>

<a name="requirements"></a>

### <a name="requirements-for-your-ssl-certificate"></a><span data-ttu-id="dde0e-120">Requisitos para o certificado SSL</span><span class="sxs-lookup"><span data-stu-id="dde0e-120">Requirements for your SSL certificate</span></span>

<span data-ttu-id="dde0e-121">toouse um certificado no serviço de aplicativo, o certificado de saudação deve atender aos Olá todos os requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="dde0e-121">toouse a certificate in App Service, hello certificate must meet all hello following requirements:</span></span>

* <span data-ttu-id="dde0e-122">Assinado por uma autoridade de certificado confiável</span><span class="sxs-lookup"><span data-stu-id="dde0e-122">Signed by a trusted certificate authority</span></span>
* <span data-ttu-id="dde0e-123">Exportado como um arquivo PFX protegido por senha</span><span class="sxs-lookup"><span data-stu-id="dde0e-123">Exported as a password-protected PFX file</span></span>
* <span data-ttu-id="dde0e-124">Conter chave privada com pelo menos 2.048 bits de extensão</span><span class="sxs-lookup"><span data-stu-id="dde0e-124">Contains private key at least 2048 bits long</span></span>
* <span data-ttu-id="dde0e-125">Contém todos os certificados intermediários na cadeia de certificados de saudação</span><span class="sxs-lookup"><span data-stu-id="dde0e-125">Contains all intermediate certificates in hello certificate chain</span></span>

> [!NOTE]
> <span data-ttu-id="dde0e-126">Os **certificados ECC (Criptografia de Curva Elíptica)** podem funcionar com o Serviço de Aplicativo, mas não são abordados neste artigo.</span><span class="sxs-lookup"><span data-stu-id="dde0e-126">**Elliptic Curve Cryptography (ECC) certificates** can work with App Service but are not covered by this article.</span></span> <span data-ttu-id="dde0e-127">Trabalhar com a autoridade de certificação em certificados ECC Olá as etapas exatas toocreate.</span><span class="sxs-lookup"><span data-stu-id="dde0e-127">Work with your certificate authority on hello exact steps toocreate ECC certificates.</span></span>

## <a name="prepare-your-web-app"></a><span data-ttu-id="dde0e-128">Preparar o aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="dde0e-128">Prepare your web app</span></span>

<span data-ttu-id="dde0e-129">toobind um SSL personalizado de certificado tooyour web app, seu [plano de serviço de aplicativo](https://azure.microsoft.com/pricing/details/app-service/) deve estar no hello **básica**, **padrão**, ou **Premium** camada.</span><span class="sxs-lookup"><span data-stu-id="dde0e-129">toobind a custom SSL certificate tooyour web app, your [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be in hello **Basic**, **Standard**, or **Premium** tier.</span></span> <span data-ttu-id="dde0e-130">Nesta etapa, você garantir que seu aplicativo web é no hello aceita preço.</span><span class="sxs-lookup"><span data-stu-id="dde0e-130">In this step, you make sure that your web app is in hello supported pricing tier.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="dde0e-131">Faça logon no tooAzure</span><span class="sxs-lookup"><span data-stu-id="dde0e-131">Log in tooAzure</span></span>

<span data-ttu-id="dde0e-132">Olá abrir [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="dde0e-132">Open hello [Azure portal](https://portal.azure.com).</span></span>

### <a name="navigate-tooyour-web-app"></a><span data-ttu-id="dde0e-133">Navegue tooyour web app</span><span class="sxs-lookup"><span data-stu-id="dde0e-133">Navigate tooyour web app</span></span>

<span data-ttu-id="dde0e-134">No menu à esquerda do hello, clique em **serviços de aplicativos**e, em seguida, clique em nome de saudação do seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="dde0e-134">From hello left menu, click **App Services**, and then click hello name of your web app.</span></span>

![Selecionar aplicativo Web](./media/app-service-web-tutorial-custom-ssl/select-app.png)

<span data-ttu-id="dde0e-136">Você descarregou na página de gerenciamento de saudação do seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="dde0e-136">You have landed in hello management page of your web app.</span></span>  

### <a name="check-hello-pricing-tier"></a><span data-ttu-id="dde0e-137">Saudação de verificação de preço</span><span class="sxs-lookup"><span data-stu-id="dde0e-137">Check hello pricing tier</span></span>

<span data-ttu-id="dde0e-138">Na navegação do lado esquerdo Olá da página de aplicativo da web, role toohello **configurações** seção e selecione **escalar verticalmente (plano de serviço de aplicativo)**.</span><span class="sxs-lookup"><span data-stu-id="dde0e-138">In hello left-hand navigation of your web app page, scroll toohello **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Menu Escalar verticalmente](./media/app-service-web-tutorial-custom-ssl/scale-up-menu.png)

<span data-ttu-id="dde0e-140">Verificar toomake-se de que seu aplicativo web não está em Olá **livre** ou **compartilhado** camada.</span><span class="sxs-lookup"><span data-stu-id="dde0e-140">Check toomake sure that your web app is not in hello **Free** or **Shared** tier.</span></span> <span data-ttu-id="dde0e-141">A camada atual do seu aplicativo Web é realçada por uma caixa azul escuro.</span><span class="sxs-lookup"><span data-stu-id="dde0e-141">Your web app's current tier is highlighted by a dark blue box.</span></span>

![Verificar tipo de preço](./media/app-service-web-tutorial-custom-ssl/check-pricing-tier.png)

<span data-ttu-id="dde0e-143">Não há suporte para SSL personalizado Olá **livre** ou **compartilhado** camada.</span><span class="sxs-lookup"><span data-stu-id="dde0e-143">Custom SSL is not supported in hello **Free** or **Shared** tier.</span></span> <span data-ttu-id="dde0e-144">Se for necessário tooscale backup, siga etapas Olá Olá próxima seção.</span><span class="sxs-lookup"><span data-stu-id="dde0e-144">If you need tooscale up, follow hello steps in hello next section.</span></span> <span data-ttu-id="dde0e-145">Caso contrário, feche Olá **Escolher tipo de preços** página e ir muito[carregar e associar o certificado SSL](#upload).</span><span class="sxs-lookup"><span data-stu-id="dde0e-145">Otherwise, close hello **Choose your pricing tier** page and skip too[Upload and bind your SSL certificate](#upload).</span></span>

### <a name="scale-up-your-app-service-plan"></a><span data-ttu-id="dde0e-146">Escalar verticalmente seu Plano do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="dde0e-146">Scale up your App Service plan</span></span>

<span data-ttu-id="dde0e-147">Selecione uma saudação **básica**, **padrão**, ou **Premium** camadas.</span><span class="sxs-lookup"><span data-stu-id="dde0e-147">Select one of hello **Basic**, **Standard**, or **Premium** tiers.</span></span>

<span data-ttu-id="dde0e-148">Clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="dde0e-148">Click **Select**.</span></span>

![Escolha um tipo de preço](./media/app-service-web-tutorial-custom-ssl/choose-pricing-tier.png)

<span data-ttu-id="dde0e-150">Quando você vir Olá notificação a seguir, a operação de escala de saudação foi concluída.</span><span class="sxs-lookup"><span data-stu-id="dde0e-150">When you see hello following notification, hello scale operation is complete.</span></span>

![Escalar verticalmente a notificação](./media/app-service-web-tutorial-custom-ssl/scale-notification.png)

<a name="upload"></a>

## <a name="bind-your-ssl-certificate"></a><span data-ttu-id="dde0e-152">Associar o certificado SSL</span><span class="sxs-lookup"><span data-stu-id="dde0e-152">Bind your SSL certificate</span></span>

<span data-ttu-id="dde0e-153">Você está pronto tooupload seu aplicativo web de tooyour de certificado SSL.</span><span class="sxs-lookup"><span data-stu-id="dde0e-153">You are ready tooupload your SSL certificate tooyour web app.</span></span>

### <a name="merge-intermediate-certificates"></a><span data-ttu-id="dde0e-154">Mesclar certificados intermediários</span><span class="sxs-lookup"><span data-stu-id="dde0e-154">Merge intermediate certificates</span></span>

<span data-ttu-id="dde0e-155">Se a autoridade de certificação fornece vários certificados na cadeia de certificados hello, você precisa de certificados de saudação toomerge na ordem.</span><span class="sxs-lookup"><span data-stu-id="dde0e-155">If your certificate authority gives you multiple certificates in hello certificate chain, you need toomerge hello certificates in order.</span></span> 

<span data-ttu-id="dde0e-156">toodo isso, abra cada certificado que você recebeu em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="dde0e-156">toodo this, open each certificate you received in a text editor.</span></span> 

<span data-ttu-id="dde0e-157">Criar um arquivo para o certificado mesclada hello, chamado _mergedcertificate.crt_.</span><span class="sxs-lookup"><span data-stu-id="dde0e-157">Create a file for hello merged certificate, called _mergedcertificate.crt_.</span></span> <span data-ttu-id="dde0e-158">Em um editor de texto, copie o conteúdo de saudação de cada certificado para este arquivo.</span><span class="sxs-lookup"><span data-stu-id="dde0e-158">In a text editor, copy hello content of each certificate into this file.</span></span> <span data-ttu-id="dde0e-159">ordem Olá seus certificados deve ser semelhantes Olá modelo a seguir:</span><span class="sxs-lookup"><span data-stu-id="dde0e-159">hello order of your certificates should look like hello following template:</span></span>

```
-----BEGIN CERTIFICATE-----
<your Base64 encoded SSL certificate>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded intermediate certificate 1>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded intermediate certificate 2>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded root certificate>
-----END CERTIFICATE-----
```

### <a name="export-certificate-toopfx"></a><span data-ttu-id="dde0e-160">Exportar o certificado tooPFX</span><span class="sxs-lookup"><span data-stu-id="dde0e-160">Export certificate tooPFX</span></span>

<span data-ttu-id="dde0e-161">Exporte o certificado SSL mesclado com chave privada de saudação que sua solicitação de certificado foi gerada com.</span><span class="sxs-lookup"><span data-stu-id="dde0e-161">Export your merged SSL certificate with hello private key that your certificate request was generated with.</span></span>

<span data-ttu-id="dde0e-162">Se você gerou a solicitação de certificado usando o OpenSSL, isso significa que você criou um arquivo de chave privada.</span><span class="sxs-lookup"><span data-stu-id="dde0e-162">If you generated your certificate request using OpenSSL, then you have created a private key file.</span></span> <span data-ttu-id="dde0e-163">tooexport tooPFX seu certificado, execute Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="dde0e-163">tooexport your certificate tooPFX, run hello following command.</span></span> <span data-ttu-id="dde0e-164">Substitua os espaços reservados de saudação  _&lt;o arquivo de chave privada >_ e  _&lt;arquivo mesclado de certificado >_.</span><span class="sxs-lookup"><span data-stu-id="dde0e-164">Replace hello placeholders _&lt;private-key-file>_ and _&lt;merged-certificate-file>_.</span></span>

```
openssl pkcs12 -export -out myserver.pfx -inkey <private-key-file> -in <merged-certificate-file>  
```

<span data-ttu-id="dde0e-165">Quando solicitado, defina uma senha de exportação.</span><span class="sxs-lookup"><span data-stu-id="dde0e-165">When prompted, define an export password.</span></span> <span data-ttu-id="dde0e-166">Você usará essa senha ao carregar o SSL certificado tooApp serviço mais tarde.</span><span class="sxs-lookup"><span data-stu-id="dde0e-166">You'll use this password when uploading your SSL certificate tooApp Service later.</span></span>

<span data-ttu-id="dde0e-167">Se você usou o IIS ou _Certreq.exe_ toogenerate sua solicitação de certificado, a instalação Olá certificado tooyour computador local e, em seguida, [exportar Olá certificado tooPFX](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).</span><span class="sxs-lookup"><span data-stu-id="dde0e-167">If you used IIS or _Certreq.exe_ toogenerate your certificate request, install hello certificate tooyour local machine, and then [export hello certificate tooPFX](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).</span></span>

### <a name="upload-your-ssl-certificate"></a><span data-ttu-id="dde0e-168">Carregar o certificado SSL</span><span class="sxs-lookup"><span data-stu-id="dde0e-168">Upload your SSL certificate</span></span>

<span data-ttu-id="dde0e-169">tooupload seu certificado SSL, clique em **certificados SSL** de saudação à esquerda de navegação de seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="dde0e-169">tooupload your SSL certificate, click **SSL certificates** in hello left navigation of your web app.</span></span>

<span data-ttu-id="dde0e-170">Clique em **Carregar Certificado**.</span><span class="sxs-lookup"><span data-stu-id="dde0e-170">Click **Upload Certificate**.</span></span>

<span data-ttu-id="dde0e-171">Em **Arquivo de Certificado PFX**, selecione o arquivo PFX.</span><span class="sxs-lookup"><span data-stu-id="dde0e-171">In **PFX Certificate File**, select your PFX file.</span></span> <span data-ttu-id="dde0e-172">Em **senha do certificado**, digite a senha de saudação que você criou ao exportar o arquivo PFX de saudação.</span><span class="sxs-lookup"><span data-stu-id="dde0e-172">In **Certificate password**, type hello password that you created when you exported hello PFX file.</span></span>

<span data-ttu-id="dde0e-173">Clique em **Carregar**.</span><span class="sxs-lookup"><span data-stu-id="dde0e-173">Click **Upload**.</span></span>

![Carregar um certificado](./media/app-service-web-tutorial-custom-ssl/upload-certificate.png)

<span data-ttu-id="dde0e-175">Quando o serviço de aplicativo terminar de carregar seu certificado, ela aparece no hello **certificados SSL** página.</span><span class="sxs-lookup"><span data-stu-id="dde0e-175">When App Service finishes uploading your certificate, it appears in hello **SSL certificates** page.</span></span>

![Certificado carregado](./media/app-service-web-tutorial-custom-ssl/certificate-uploaded.png)

### <a name="bind-your-ssl-certificate"></a><span data-ttu-id="dde0e-177">Associar o certificado SSL</span><span class="sxs-lookup"><span data-stu-id="dde0e-177">Bind your SSL certificate</span></span>

<span data-ttu-id="dde0e-178">Em Olá **associações SSL** seção, clique em **Adicionar associação**.</span><span class="sxs-lookup"><span data-stu-id="dde0e-178">In hello **SSL bindings** section, click **Add binding**.</span></span>

<span data-ttu-id="dde0e-179">Em Olá **Adicionar associação de SSL** página, use toosecure de nome de domínio Olá menus suspensos tooselect hello e Olá toouse de certificado.</span><span class="sxs-lookup"><span data-stu-id="dde0e-179">In hello **Add SSL Binding** page, use hello dropdowns tooselect hello domain name toosecure, and hello certificate toouse.</span></span>

> [!NOTE]
> <span data-ttu-id="dde0e-180">Se você carregar seu certificado, mas não vir Olá nomes de domínio em Olá **Hostname** suspenso, tente atualizar a página do navegador hello.</span><span class="sxs-lookup"><span data-stu-id="dde0e-180">If you have uploaded your certificate but don't see hello domain name(s) in hello **Hostname** dropdown, try refreshing hello browser page.</span></span>
>
>

<span data-ttu-id="dde0e-181">Em **tipo SSL**, selecione se toouse  **[indicação de nome de servidor (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)**  ou SSL com base em IP.</span><span class="sxs-lookup"><span data-stu-id="dde0e-181">In **SSL Type**, select whether toouse **[Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** or IP-based SSL.</span></span>

- <span data-ttu-id="dde0e-182">**SSL baseado em SNI** – várias associações SSL baseadas em SNI podem ser adicionadas.</span><span class="sxs-lookup"><span data-stu-id="dde0e-182">**SNI-based SSL** - Multiple SNI-based SSL bindings may be added.</span></span> <span data-ttu-id="dde0e-183">Essa opção permite que vários toosecure de certificados SSL vários domínios em Olá mesmo endereço IP.</span><span class="sxs-lookup"><span data-stu-id="dde0e-183">This option allows multiple SSL certificates toosecure multiple domains on hello same IP address.</span></span> <span data-ttu-id="dde0e-184">Navegadores mais modernos (incluindo Internet Explorer, Chrome, Firefox e Opera) dão suporte ao SNI (encontre informações de suporte ao navegador mais abrangentes em [Indicação de Nome de Servidor](http://wikipedia.org/wiki/Server_Name_Indication)).</span><span class="sxs-lookup"><span data-stu-id="dde0e-184">Most modern browsers (including Internet Explorer, Chrome, Firefox, and Opera) support SNI (find more comprehensive browser support information at [Server Name Indication](http://wikipedia.org/wiki/Server_Name_Indication)).</span></span>
- <span data-ttu-id="dde0e-185">**SSL baseado em IP** – apenas uma associação SSL baseada em IP pode ser adicionada.</span><span class="sxs-lookup"><span data-stu-id="dde0e-185">**IP-based SSL** - Only one IP-based SSL binding may be added.</span></span> <span data-ttu-id="dde0e-186">Essa opção permite que apenas um toosecure de certificado SSL para um endereço IP público dedicado.</span><span class="sxs-lookup"><span data-stu-id="dde0e-186">This option allows only one SSL certificate toosecure a dedicated public IP address.</span></span> <span data-ttu-id="dde0e-187">toosecure vários domínios, você deve protegê-los todos usando Olá mesmo certificado SSL.</span><span class="sxs-lookup"><span data-stu-id="dde0e-187">toosecure multiple domains, you must secure them all using hello same SSL certificate.</span></span> <span data-ttu-id="dde0e-188">Essa é a opção tradicional Olá para uma associação SSL.</span><span class="sxs-lookup"><span data-stu-id="dde0e-188">This is hello traditional option for SSL binding.</span></span>

<span data-ttu-id="dde0e-189">Clique em **Adicionar Associação**.</span><span class="sxs-lookup"><span data-stu-id="dde0e-189">Click **Add Binding**.</span></span>

![Associar Certificado SSL](./media/app-service-web-tutorial-custom-ssl/bind-certificate.png)

<span data-ttu-id="dde0e-191">Quando o serviço de aplicativo terminar de carregar seu certificado, ela aparece no hello **associações SSL** seções.</span><span class="sxs-lookup"><span data-stu-id="dde0e-191">When App Service finishes uploading your certificate, it appears in hello **SSL bindings** sections.</span></span>

![Certificado associado tooweb aplicativo](./media/app-service-web-tutorial-custom-ssl/certificate-bound.png)

## <a name="remap-a-record-for-ip-ssl"></a><span data-ttu-id="dde0e-193">Remapear um registro para IP SSL</span><span class="sxs-lookup"><span data-stu-id="dde0e-193">Remap A record for IP SSL</span></span>

<span data-ttu-id="dde0e-194">Se você não usar SSL com base em IP em seu aplicativo web, ignorar muito[HTTPS de teste para seu domínio personalizado](#test).</span><span class="sxs-lookup"><span data-stu-id="dde0e-194">If you don't use IP-based SSL in your web app, skip too[Test HTTPS for your custom domain](#test).</span></span>

<span data-ttu-id="dde0e-195">Por padrão, o seu aplicativo Web usa um endereço IP público compartilhado.</span><span class="sxs-lookup"><span data-stu-id="dde0e-195">By default, your web app uses a shared public IP address.</span></span> <span data-ttu-id="dde0e-196">Quando você associa um certificado ao SSL baseado em IP, o Serviço de Aplicativo cria um novo endereço IP dedicado para o aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="dde0e-196">When you bind a certificate with IP-based SSL, App Service creates a new, dedicated IP address for your web app.</span></span>

<span data-ttu-id="dde0e-197">Se você tiver mapeado um aplicativo de web de registro tooyour um, atualize o registro de domínio com esse novo endereço IP dedicado.</span><span class="sxs-lookup"><span data-stu-id="dde0e-197">If you have mapped an A record tooyour web app, update your domain registry with this new, dedicated IP address.</span></span>

<span data-ttu-id="dde0e-198">Seu aplicativo de web **domínio personalizado** página é atualizada com o endereço IP de novo, dedicado hello.</span><span class="sxs-lookup"><span data-stu-id="dde0e-198">Your web app's **Custom domain** page is updated with hello new, dedicated IP address.</span></span> <span data-ttu-id="dde0e-199">[Copiar esse endereço IP](app-service-web-tutorial-custom-domain.md#info), em seguida, [remapear Olá um registro](app-service-web-tutorial-custom-domain.md#map-an-a-record) toothis novo endereço IP.</span><span class="sxs-lookup"><span data-stu-id="dde0e-199">[Copy this IP address](app-service-web-tutorial-custom-domain.md#info), then [remap hello A record](app-service-web-tutorial-custom-domain.md#map-an-a-record) toothis new IP address.</span></span>

<a name="test"></a>

## <a name="test-https"></a><span data-ttu-id="dde0e-200">Testar HTTPS</span><span class="sxs-lookup"><span data-stu-id="dde0e-200">Test HTTPS</span></span>

<span data-ttu-id="dde0e-201">Tudo o que tiver saído toodo agora é toomake-se de que o HTTPS funciona para seu domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="dde0e-201">All that's left toodo now is toomake sure that HTTPS works for your custom domain.</span></span> <span data-ttu-id="dde0e-202">Em vários navegadores, procurar muito`https://<your.custom.domain>` toosee que serve o seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="dde0e-202">In various browsers, browse too`https://<your.custom.domain>` toosee that it serves up your web app.</span></span>

![Navegação do portal tooAzure aplicativo](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

> [!NOTE]
> <span data-ttu-id="dde0e-204">Se o seu aplicativo Web retorna erros de validação de certificado, você provavelmente está usando um certificado autoassinado.</span><span class="sxs-lookup"><span data-stu-id="dde0e-204">If your web app gives you certificate validation errors, you're probably using a self-signed certificate.</span></span>
>
> <span data-ttu-id="dde0e-205">Se não for o caso de Olá, você talvez tenha deixado os certificados intermediários, quando você exportar o arquivo PFX do certificado toohello.</span><span class="sxs-lookup"><span data-stu-id="dde0e-205">If that's not hello case, you may have left out intermediate certificates when you export your certificate toohello PFX file.</span></span>

<a name="bkmk_enforce"></a>

## <a name="enforce-https"></a><span data-ttu-id="dde0e-206">Impor HTTPS</span><span class="sxs-lookup"><span data-stu-id="dde0e-206">Enforce HTTPS</span></span>

<span data-ttu-id="dde0e-207">O Serviço de Aplicativo *não* impõe o HTTPS, de modo que qualquer um ainda pode acessar seu aplicativo Web usando HTTP.</span><span class="sxs-lookup"><span data-stu-id="dde0e-207">App Service does *not* enforce HTTPS, so anyone can still access your web app using HTTP.</span></span> <span data-ttu-id="dde0e-208">tooenforce HTTPS para o aplicativo web, definir uma regra de regravação de saudação _Web. config_ arquivo para seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="dde0e-208">tooenforce HTTPS for your web app, define a rewrite rule in hello _web.config_ file for your web app.</span></span> <span data-ttu-id="dde0e-209">Serviço de aplicativo usa esse arquivo, independentemente da estrutura de linguagem de saudação do seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="dde0e-209">App Service uses this file, regardless of hello language framework of your web app.</span></span>

> [!NOTE]
> <span data-ttu-id="dde0e-210">Há um redirecionamento de solicitações específico a um idioma.</span><span class="sxs-lookup"><span data-stu-id="dde0e-210">There is language-specific redirection of requests.</span></span> <span data-ttu-id="dde0e-211">ASP.NET MVC pode usar Olá [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filtro em vez de regra de regravação de saudação em _Web. config_.</span><span class="sxs-lookup"><span data-stu-id="dde0e-211">ASP.NET MVC can use hello [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filter instead of hello rewrite rule in _web.config_.</span></span>

<span data-ttu-id="dde0e-212">Se você é um desenvolvedor do .NET, você deve estar relativamente familiarizado com esse arquivo.</span><span class="sxs-lookup"><span data-stu-id="dde0e-212">If you're a .NET developer, you should be relatively familiar with this file.</span></span> <span data-ttu-id="dde0e-213">Ele é Olá raiz de sua solução.</span><span class="sxs-lookup"><span data-stu-id="dde0e-213">It is in hello root of your solution.</span></span>

<span data-ttu-id="dde0e-214">Como alternativa, se você desenvolve com PHP, Node.js, Python ou Java, há uma chance de termos gerado esse arquivo em seu nome no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dde0e-214">Alternatively, if you develop with PHP, Node.js, Python, or Java, there is a chance we generated this file on your behalf in App Service.</span></span>

<span data-ttu-id="dde0e-215">Conecte-se o ponto de extremidade do aplicativo da web tooyour FTP seguindo as instruções de saudação em [implantar tooAzure seu aplicativo do serviço de aplicativo usando o FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="dde0e-215">Connect tooyour web app's FTP endpoint by following hello instructions at [Deploy your app tooAzure App Service using FTP/S](app-service-deploy-ftp.md).</span></span>

<span data-ttu-id="dde0e-216">Esse arquivo deve estar localizado em _/home/site/wwwroot_.</span><span class="sxs-lookup"><span data-stu-id="dde0e-216">This file should be located in _/home/site/wwwroot_.</span></span> <span data-ttu-id="dde0e-217">Caso contrário, crie um _Web. config_ arquivo nessa pasta com hello XML a seguir:</span><span class="sxs-lookup"><span data-stu-id="dde0e-217">If not, create a _web.config_ file in this folder with hello following XML:</span></span>

```xml   
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <!-- BEGIN rule ELEMENT FOR HTTPS REDIRECT -->
        <rule name="Force HTTPS" enabled="true">
          <match url="(.*)" ignoreCase="false" />
          <conditions>
            <add input="{HTTPS}" pattern="off" />
          </conditions>
          <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" appendQueryString="true" redirectType="Permanent" />
        </rule>
        <!-- END rule ELEMENT FOR HTTPS REDIRECT -->
      </rules>
    </rewrite>
  </system.webServer>
</configuration>
```

<span data-ttu-id="dde0e-218">Existe uma _Web. config_ de arquivo, copie todo Olá `<rule>` elemento em seu _Web. config_do `configuration/system.webServer/rewrite/rules` elemento.</span><span class="sxs-lookup"><span data-stu-id="dde0e-218">For an existing _web.config_ file, copy hello entire `<rule>` element into your _web.config_'s `configuration/system.webServer/rewrite/rules` element.</span></span> <span data-ttu-id="dde0e-219">Se houver outros `<rule>` elementos no seu _Web. config_, Olá local copiado `<rule>` elemento antes Olá outros `<rule>` elementos.</span><span class="sxs-lookup"><span data-stu-id="dde0e-219">If there are other `<rule>` elements in your _web.config_, place hello copied `<rule>` element before hello other `<rule>` elements.</span></span>

<span data-ttu-id="dde0e-220">Essa regra retorna um protocolo HTTPS toohello HTTP 301 (redirecionamento permanente) sempre que o usuário Olá faz com que um aplicativo web de tooyour de solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="dde0e-220">This rule returns an HTTP 301 (permanent redirect) toohello HTTPS protocol whenever hello user makes an HTTP request tooyour web app.</span></span> <span data-ttu-id="dde0e-221">Por exemplo, ele redireciona de `http://contoso.com` muito`https://contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="dde0e-221">For example, it redirects from `http://contoso.com` too`https://contoso.com`.</span></span>

<span data-ttu-id="dde0e-222">Para obter mais informações sobre o módulo de reescrita de URL para IIS hello, consulte Olá [reescrita de URL](http://www.iis.net/downloads/microsoft/url-rewrite) documentação.</span><span class="sxs-lookup"><span data-stu-id="dde0e-222">For more information on hello IIS URL Rewrite module, see hello [URL Rewrite](http://www.iis.net/downloads/microsoft/url-rewrite) documentation.</span></span>

## <a name="enforce-https-for-web-apps-on-linux"></a><span data-ttu-id="dde0e-223">Impor o HTTPS a aplicativos Web no Linux</span><span class="sxs-lookup"><span data-stu-id="dde0e-223">Enforce HTTPS for Web Apps on Linux</span></span>

<span data-ttu-id="dde0e-224">O Serviço de Aplicativo no Linux *não* impõe o HTTPS e, portanto, qualquer pessoa ainda pode acessar o aplicativo Web usando o HTTP.</span><span class="sxs-lookup"><span data-stu-id="dde0e-224">App Service on Linux does *not* enforce HTTPS, so anyone can still access your web app using HTTP.</span></span> <span data-ttu-id="dde0e-225">tooenforce HTTPS para o aplicativo web, definir uma regra de regravação de saudação _htaccess_ arquivo para seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="dde0e-225">tooenforce HTTPS for your web app, define a rewrite rule in hello _.htaccess_ file for your web app.</span></span> 

<span data-ttu-id="dde0e-226">Conecte-se o ponto de extremidade do aplicativo da web tooyour FTP seguindo as instruções de saudação em [implantar tooAzure seu aplicativo do serviço de aplicativo usando o FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="dde0e-226">Connect tooyour web app's FTP endpoint by following hello instructions at [Deploy your app tooAzure App Service using FTP/S](app-service-deploy-ftp.md).</span></span>

<span data-ttu-id="dde0e-227">Em _/home/site/wwwroot_, crie um _htaccess_ arquivo com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="dde0e-227">In _/home/site/wwwroot_, create an _.htaccess_ file with hello following code:</span></span>

```
RewriteEngine On
RewriteCond %{HTTP:X-ARR-SSL} ^$
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

<span data-ttu-id="dde0e-228">Essa regra retorna um protocolo HTTPS toohello HTTP 301 (redirecionamento permanente) sempre que o usuário Olá faz com que um aplicativo web de tooyour de solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="dde0e-228">This rule returns an HTTP 301 (permanent redirect) toohello HTTPS protocol whenever hello user makes an HTTP request tooyour web app.</span></span> <span data-ttu-id="dde0e-229">Por exemplo, ele redireciona de `http://contoso.com` muito`https://contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="dde0e-229">For example, it redirects from `http://contoso.com` too`https://contoso.com`.</span></span>

## <a name="automate-with-scripts"></a><span data-ttu-id="dde0e-230">Automatizar com scripts</span><span class="sxs-lookup"><span data-stu-id="dde0e-230">Automate with scripts</span></span>

<span data-ttu-id="dde0e-231">Você pode automatizar associações SSL para seu aplicativo web com scripts, usando Olá [CLI do Azure](/cli/azure/install-azure-cli) ou [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dde0e-231">You can automate SSL bindings for your web app with scripts, using hello [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="azure-cli"></a><span data-ttu-id="dde0e-232">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="dde0e-232">Azure CLI</span></span>

<span data-ttu-id="dde0e-233">Olá comando a seguir carrega um arquivo PFX exportado e obtém a impressão digital de saudação.</span><span class="sxs-lookup"><span data-stu-id="dde0e-233">hello following command uploads an exported PFX file and gets hello thumbprint.</span></span>

```bash
thumbprint=$(az appservice web config ssl upload \
    --name <app_name> \
    --resource-group <resource_group_name> \
    --certificate-file <path_to_PFX_file> \
    --certificate-password <PFX_password> \
    --query thumbprint \
    --output tsv)
```

<span data-ttu-id="dde0e-234">Olá comando a seguir adiciona uma associação de SSL baseado em SNI, usando a impressão digital de saudação do comando anterior hello.</span><span class="sxs-lookup"><span data-stu-id="dde0e-234">hello following command adds an SNI-based SSL binding, using hello thumbprint from hello previous command.</span></span>

```bash
az appservice web config ssl bind \
    --name <app_name> \
    --resource-group <resource_group_name>
    --certificate-thumbprint $thumbprint \
    --ssl-type SNI \
```

### <a name="azure-powershell"></a><span data-ttu-id="dde0e-235">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="dde0e-235">Azure PowerShell</span></span>

<span data-ttu-id="dde0e-236">Olá comando a seguir carrega um arquivo PFX exportado e adiciona uma associação SSL de SNI.</span><span class="sxs-lookup"><span data-stu-id="dde0e-236">hello following command uploads an exported PFX file and adds an SNI-based SSL binding.</span></span>

```PowerShell
New-AzureRmWebAppSSLBinding `
    -WebAppName <app_name> `
    -ResourceGroupName <resource_group_name> `
    -Name <dns_name> `
    -CertificateFilePath <path_to_PFX_file> `
    -CertificatePassword <PFX_password> `
    -SslState SniEnabled
```

## <a name="next-steps"></a><span data-ttu-id="dde0e-237">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dde0e-237">Next steps</span></span>

<span data-ttu-id="dde0e-238">Neste tutorial, você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="dde0e-238">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="dde0e-239">Atualizar o tipo de preço do aplicativo</span><span class="sxs-lookup"><span data-stu-id="dde0e-239">Upgrade your app's pricing tier</span></span>
> * <span data-ttu-id="dde0e-240">Associar seu tooApp de certificado SSL personalizado serviço</span><span class="sxs-lookup"><span data-stu-id="dde0e-240">Bind your custom SSL certificate tooApp Service</span></span>
> * <span data-ttu-id="dde0e-241">Impor HTTPS para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="dde0e-241">Enforce HTTPS for your app</span></span>
> * <span data-ttu-id="dde0e-242">Automatizar a associação de certificado SSL com scripts</span><span class="sxs-lookup"><span data-stu-id="dde0e-242">Automate SSL certificate binding with scripts</span></span>

<span data-ttu-id="dde0e-243">Avançar toolearn tutorial do próximo toohello como toouse rede de fornecimento de conteúdo do Azure.</span><span class="sxs-lookup"><span data-stu-id="dde0e-243">Advance toohello next tutorial toolearn how toouse Azure Content Delivery Network.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="dde0e-244">Adicionar uma tooan de rede de fornecimento de conteúdo (CDN) do serviço de aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="dde0e-244">Add a Content Delivery Network (CDN) tooan Azure App Service</span></span>](app-service-web-tutorial-content-delivery-network.md)
