---
title: Associar um certificado SSL personalizado existente a aplicativos Web do Azure | Microsoft Docs
description: "Saiba como associar um certificado SSL personalizado a seu aplicativo Web, back-end do aplicativo móvel ou aplicativo de API no Serviço de Aplicativo do Azure."
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
ms.openlocfilehash: 15c31ae5451a31dff2df08047ee43e75edacc127
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="bind-an-existing-custom-ssl-certificate-to-azure-web-apps"></a><span data-ttu-id="60f2f-103">Associar um certificado SSL personalizado existente a aplicativos Web do Azure</span><span class="sxs-lookup"><span data-stu-id="60f2f-103">Bind an existing custom SSL certificate to Azure Web Apps</span></span>

<span data-ttu-id="60f2f-104">Os Aplicativos Web do Azure fornecem um serviço de hospedagem na Web altamente escalonável e com aplicação automática de patch.</span><span class="sxs-lookup"><span data-stu-id="60f2f-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="60f2f-105">Este tutorial mostra como associar um certificado SSL personalizado que você adquiriu de uma autoridade de certificação confiável para [aplicativos Web do Azure](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="60f2f-105">This tutorial shows you how to bind a custom SSL certificate that you purchased from a trusted certificate authority to [Azure Web Apps](app-service-web-overview.md).</span></span> <span data-ttu-id="60f2f-106">Quando você terminar, você poderá acessar seu aplicativo Web no ponto de extremidade HTTPS do seu domínio DNS personalizado.</span><span class="sxs-lookup"><span data-stu-id="60f2f-106">When you're finished, you'll be able to access your web app at the HTTPS endpoint of your custom DNS domain.</span></span>

![Aplicativo Web com certificado SSL personalizado](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

<span data-ttu-id="60f2f-108">Neste tutorial, você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="60f2f-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="60f2f-109">Atualizar o tipo de preço do aplicativo</span><span class="sxs-lookup"><span data-stu-id="60f2f-109">Upgrade your app's pricing tier</span></span>
> * <span data-ttu-id="60f2f-110">Associar o certificado SSL personalizado ao Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="60f2f-110">Bind your custom SSL certificate to App Service</span></span>
> * <span data-ttu-id="60f2f-111">Impor HTTPS para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="60f2f-111">Enforce HTTPS for your app</span></span>
> * <span data-ttu-id="60f2f-112">Automatizar a associação de certificado SSL com scripts</span><span class="sxs-lookup"><span data-stu-id="60f2f-112">Automate SSL certificate binding with scripts</span></span>

> [!NOTE]
> <span data-ttu-id="60f2f-113">Se você precisar obter um certificado SSL personalizado, você poderá obtê-lo diretamente no Portal do Azure e associá-lo ao seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="60f2f-113">If you need to get a custom SSL certificate, you can get one in the Azure portal directly and bind it to your web app.</span></span> <span data-ttu-id="60f2f-114">Siga o [tutorial de Certificados do Serviço de Aplicativo](web-sites-purchase-ssl-web-site.md).</span><span class="sxs-lookup"><span data-stu-id="60f2f-114">Follow the [App Service Certificates tutorial](web-sites-purchase-ssl-web-site.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="60f2f-115">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="60f2f-115">Prerequisites</span></span>

<span data-ttu-id="60f2f-116">Para concluir este tutorial:</span><span class="sxs-lookup"><span data-stu-id="60f2f-116">To complete this tutorial:</span></span>

- [<span data-ttu-id="60f2f-117">Crie um aplicativo do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="60f2f-117">Create an App Service app</span></span>](/azure/app-service/)
- [<span data-ttu-id="60f2f-118">Mapear um nome DNS personalizado para o aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="60f2f-118">Map a custom DNS name to your web app</span></span>](app-service-web-tutorial-custom-domain.md)
- <span data-ttu-id="60f2f-119">Adquirir um certificado SSL de uma autoridade de certificado confiável</span><span class="sxs-lookup"><span data-stu-id="60f2f-119">Acquire an SSL certificate from a trusted certificate authority</span></span>

<a name="requirements"></a>

### <a name="requirements-for-your-ssl-certificate"></a><span data-ttu-id="60f2f-120">Requisitos para o certificado SSL</span><span class="sxs-lookup"><span data-stu-id="60f2f-120">Requirements for your SSL certificate</span></span>

<span data-ttu-id="60f2f-121">Para usar o certificado no Serviço de Aplicativo, o certificado deve atender a todos os seguintes requisitos:</span><span class="sxs-lookup"><span data-stu-id="60f2f-121">To use a certificate in App Service, the certificate must meet all the following requirements:</span></span>

* <span data-ttu-id="60f2f-122">Assinado por uma autoridade de certificado confiável</span><span class="sxs-lookup"><span data-stu-id="60f2f-122">Signed by a trusted certificate authority</span></span>
* <span data-ttu-id="60f2f-123">Exportado como um arquivo PFX protegido por senha</span><span class="sxs-lookup"><span data-stu-id="60f2f-123">Exported as a password-protected PFX file</span></span>
* <span data-ttu-id="60f2f-124">Conter chave privada com pelo menos 2.048 bits de extensão</span><span class="sxs-lookup"><span data-stu-id="60f2f-124">Contains private key at least 2048 bits long</span></span>
* <span data-ttu-id="60f2f-125">Conter todos os certificados intermediários na cadeia de certificados</span><span class="sxs-lookup"><span data-stu-id="60f2f-125">Contains all intermediate certificates in the certificate chain</span></span>

> [!NOTE]
> <span data-ttu-id="60f2f-126">Os **certificados ECC (Criptografia de Curva Elíptica)** podem funcionar com o Serviço de Aplicativo, mas não são abordados neste artigo.</span><span class="sxs-lookup"><span data-stu-id="60f2f-126">**Elliptic Curve Cryptography (ECC) certificates** can work with App Service but are not covered by this article.</span></span> <span data-ttu-id="60f2f-127">Trabalhe com sua autoridade de certificação seguindo exatamente estas etapas para criar certificados ECC.</span><span class="sxs-lookup"><span data-stu-id="60f2f-127">Work with your certificate authority on the exact steps to create ECC certificates.</span></span>

## <a name="prepare-your-web-app"></a><span data-ttu-id="60f2f-128">Preparar o aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="60f2f-128">Prepare your web app</span></span>

<span data-ttu-id="60f2f-129">Para associar um certificado SSL personalizado ao aplicativo Web, o [Plano do Serviço de Aplicativo](https://azure.microsoft.com/pricing/details/app-service/) deve estar na camada **Básica**, **Standard** ou **Premium**.</span><span class="sxs-lookup"><span data-stu-id="60f2f-129">To bind a custom SSL certificate to your web app, your [App Service plan](https://azure.microsoft.com/pricing/details/app-service/) must be in the **Basic**, **Standard**, or **Premium** tier.</span></span> <span data-ttu-id="60f2f-130">Nesta etapa, você precisa ter certeza de que seu aplicativo Web está no tipo de preço com suporte.</span><span class="sxs-lookup"><span data-stu-id="60f2f-130">In this step, you make sure that your web app is in the supported pricing tier.</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="60f2f-131">Fazer logon no Azure</span><span class="sxs-lookup"><span data-stu-id="60f2f-131">Log in to Azure</span></span>

<span data-ttu-id="60f2f-132">Abra o [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="60f2f-132">Open the [Azure portal](https://portal.azure.com).</span></span>

### <a name="navigate-to-your-web-app"></a><span data-ttu-id="60f2f-133">Navegue até seu aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="60f2f-133">Navigate to your web app</span></span>

<span data-ttu-id="60f2f-134">No menu à esquerda, clique em **Serviços de Aplicativos** e, em seguida, clique no nome do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="60f2f-134">From the left menu, click **App Services**, and then click the name of your web app.</span></span>

![Selecionar aplicativo Web](./media/app-service-web-tutorial-custom-ssl/select-app.png)

<span data-ttu-id="60f2f-136">Você aterrissou na página de gerenciamento do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="60f2f-136">You have landed in the management page of your web app.</span></span>  

### <a name="check-the-pricing-tier"></a><span data-ttu-id="60f2f-137">Verifique o tipo de preço</span><span class="sxs-lookup"><span data-stu-id="60f2f-137">Check the pricing tier</span></span>

<span data-ttu-id="60f2f-138">No painel de navegação à esquerda da página do aplicativo Web, role até a seção **Configurações** e selecione **Escalar verticalmente (plano do Serviço de Aplicativo)**.</span><span class="sxs-lookup"><span data-stu-id="60f2f-138">In the left-hand navigation of your web app page, scroll to the **Settings** section and select **Scale up (App Service plan)**.</span></span>

![Menu Escalar verticalmente](./media/app-service-web-tutorial-custom-ssl/scale-up-menu.png)

<span data-ttu-id="60f2f-140">Certifique-se de que o aplicativo Web não esteja na camada **Gratuita** ou **Compartilhada**.</span><span class="sxs-lookup"><span data-stu-id="60f2f-140">Check to make sure that your web app is not in the **Free** or **Shared** tier.</span></span> <span data-ttu-id="60f2f-141">A camada atual do seu aplicativo Web é realçada por uma caixa azul escuro.</span><span class="sxs-lookup"><span data-stu-id="60f2f-141">Your web app's current tier is highlighted by a dark blue box.</span></span>

![Verificar tipo de preço](./media/app-service-web-tutorial-custom-ssl/check-pricing-tier.png)

<span data-ttu-id="60f2f-143">Não há suporte para SSL personalizado nas camadas **Gratuito** ou **Compartilhado**.</span><span class="sxs-lookup"><span data-stu-id="60f2f-143">Custom SSL is not supported in the **Free** or **Shared** tier.</span></span> <span data-ttu-id="60f2f-144">Se precisar escalar verticalmente, siga as etapas da próxima seção.</span><span class="sxs-lookup"><span data-stu-id="60f2f-144">If you need to scale up, follow the steps in the next section.</span></span> <span data-ttu-id="60f2f-145">Caso contrário, feche a página **Escolher o tipo de preço** e vá para [Carregar e associar o certificado SSL](#upload).</span><span class="sxs-lookup"><span data-stu-id="60f2f-145">Otherwise, close the **Choose your pricing tier** page and skip to [Upload and bind your SSL certificate](#upload).</span></span>

### <a name="scale-up-your-app-service-plan"></a><span data-ttu-id="60f2f-146">Escalar verticalmente seu Plano do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="60f2f-146">Scale up your App Service plan</span></span>

<span data-ttu-id="60f2f-147">Selecione uma das camadas **Básico**, **Standard** ou **Premium**.</span><span class="sxs-lookup"><span data-stu-id="60f2f-147">Select one of the **Basic**, **Standard**, or **Premium** tiers.</span></span>

<span data-ttu-id="60f2f-148">Clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="60f2f-148">Click **Select**.</span></span>

![Escolha um tipo de preço](./media/app-service-web-tutorial-custom-ssl/choose-pricing-tier.png)

<span data-ttu-id="60f2f-150">Quando você receber a notificação a seguir, a operação de escala terá sido concluída.</span><span class="sxs-lookup"><span data-stu-id="60f2f-150">When you see the following notification, the scale operation is complete.</span></span>

![Escalar verticalmente a notificação](./media/app-service-web-tutorial-custom-ssl/scale-notification.png)

<a name="upload"></a>

## <a name="bind-your-ssl-certificate"></a><span data-ttu-id="60f2f-152">Associar o certificado SSL</span><span class="sxs-lookup"><span data-stu-id="60f2f-152">Bind your SSL certificate</span></span>

<span data-ttu-id="60f2f-153">Você está pronto para carregar seu certificado SSL para o aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="60f2f-153">You are ready to upload your SSL certificate to your web app.</span></span>

### <a name="merge-intermediate-certificates"></a><span data-ttu-id="60f2f-154">Mesclar certificados intermediários</span><span class="sxs-lookup"><span data-stu-id="60f2f-154">Merge intermediate certificates</span></span>

<span data-ttu-id="60f2f-155">Se a autoridade de certificação fornecer vários certificados na cadeia de certificados, você precisará mesclar os certificados na ordem.</span><span class="sxs-lookup"><span data-stu-id="60f2f-155">If your certificate authority gives you multiple certificates in the certificate chain, you need to merge the certificates in order.</span></span> 

<span data-ttu-id="60f2f-156">Para fazer isso, abra cada certificado recebido em um editor de texto.</span><span class="sxs-lookup"><span data-stu-id="60f2f-156">To do this, open each certificate you received in a text editor.</span></span> 

<span data-ttu-id="60f2f-157">Crie um arquivo para o certificado mesclado, chamado _mergedcertificate.crt_.</span><span class="sxs-lookup"><span data-stu-id="60f2f-157">Create a file for the merged certificate, called _mergedcertificate.crt_.</span></span> <span data-ttu-id="60f2f-158">Em um editor de texto, copie o conteúdo de cada certificado para esse arquivo.</span><span class="sxs-lookup"><span data-stu-id="60f2f-158">In a text editor, copy the content of each certificate into this file.</span></span> <span data-ttu-id="60f2f-159">A ordem dos certificados deve ser parecida com o seguinte modelo:</span><span class="sxs-lookup"><span data-stu-id="60f2f-159">The order of your certificates should look like the following template:</span></span>

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

### <a name="export-certificate-to-pfx"></a><span data-ttu-id="60f2f-160">Exportar o certificado para PFX</span><span class="sxs-lookup"><span data-stu-id="60f2f-160">Export certificate to PFX</span></span>

<span data-ttu-id="60f2f-161">Exporte o certificado SSL mesclado com a chave privada com a qual a solicitação de certificado foi gerada.</span><span class="sxs-lookup"><span data-stu-id="60f2f-161">Export your merged SSL certificate with the private key that your certificate request was generated with.</span></span>

<span data-ttu-id="60f2f-162">Se você gerou a solicitação de certificado usando o OpenSSL, isso significa que você criou um arquivo de chave privada.</span><span class="sxs-lookup"><span data-stu-id="60f2f-162">If you generated your certificate request using OpenSSL, then you have created a private key file.</span></span> <span data-ttu-id="60f2f-163">Para exportar o certificado para PFX, execute o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="60f2f-163">To export your certificate to PFX, run the following command.</span></span> <span data-ttu-id="60f2f-164">Substitua os espaços reservados _&lt;private-key-file>_ e _&lt;merged-certificate-file>_.</span><span class="sxs-lookup"><span data-stu-id="60f2f-164">Replace the placeholders _&lt;private-key-file>_ and _&lt;merged-certificate-file>_.</span></span>

```
openssl pkcs12 -export -out myserver.pfx -inkey <private-key-file> -in <merged-certificate-file>  
```

<span data-ttu-id="60f2f-165">Quando solicitado, defina uma senha de exportação.</span><span class="sxs-lookup"><span data-stu-id="60f2f-165">When prompted, define an export password.</span></span> <span data-ttu-id="60f2f-166">Você usará essa senha quando carregar o certificado SSL para o Serviço de Aplicativo posteriormente.</span><span class="sxs-lookup"><span data-stu-id="60f2f-166">You'll use this password when uploading your SSL certificate to App Service later.</span></span>

<span data-ttu-id="60f2f-167">Se você usou o IIS ou o _Certreq.exe_ para gerar a solicitação de certificado, instale o certificado no computador local e, em seguida, [exporte o certificado para PFX](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).</span><span class="sxs-lookup"><span data-stu-id="60f2f-167">If you used IIS or _Certreq.exe_ to generate your certificate request, install the certificate to your local machine, and then [export the certificate to PFX](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).</span></span>

### <a name="upload-your-ssl-certificate"></a><span data-ttu-id="60f2f-168">Carregar o certificado SSL</span><span class="sxs-lookup"><span data-stu-id="60f2f-168">Upload your SSL certificate</span></span>

<span data-ttu-id="60f2f-169">Para carregar o certificado SSL, clique em **Certificados SSL** no painel de navegação esquerdo do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="60f2f-169">To upload your SSL certificate, click **SSL certificates** in the left navigation of your web app.</span></span>

<span data-ttu-id="60f2f-170">Clique em **Carregar Certificado**.</span><span class="sxs-lookup"><span data-stu-id="60f2f-170">Click **Upload Certificate**.</span></span>

<span data-ttu-id="60f2f-171">Em **Arquivo de Certificado PFX**, selecione o arquivo PFX.</span><span class="sxs-lookup"><span data-stu-id="60f2f-171">In **PFX Certificate File**, select your PFX file.</span></span> <span data-ttu-id="60f2f-172">Em **Senha do certificado**, digite a senha que você criou ao exportar o arquivo PFX.</span><span class="sxs-lookup"><span data-stu-id="60f2f-172">In **Certificate password**, type the password that you created when you exported the PFX file.</span></span>

<span data-ttu-id="60f2f-173">Clique em **Carregar**.</span><span class="sxs-lookup"><span data-stu-id="60f2f-173">Click **Upload**.</span></span>

![Carregar um certificado](./media/app-service-web-tutorial-custom-ssl/upload-certificate.png)

<span data-ttu-id="60f2f-175">Quando o Serviço de Aplicativo terminar de carregar o certificado, ele aparecerá na página **Certificados SSL**.</span><span class="sxs-lookup"><span data-stu-id="60f2f-175">When App Service finishes uploading your certificate, it appears in the **SSL certificates** page.</span></span>

![Certificado carregado](./media/app-service-web-tutorial-custom-ssl/certificate-uploaded.png)

### <a name="bind-your-ssl-certificate"></a><span data-ttu-id="60f2f-177">Associar o certificado SSL</span><span class="sxs-lookup"><span data-stu-id="60f2f-177">Bind your SSL certificate</span></span>

<span data-ttu-id="60f2f-178">Na seção **Associações SSL**, clique em **Adicionar associação**.</span><span class="sxs-lookup"><span data-stu-id="60f2f-178">In the **SSL bindings** section, click **Add binding**.</span></span>

<span data-ttu-id="60f2f-179">Na página **Adicionar Associação SSL**, use os menus suspensos para selecionar o nome de domínio a ser protegido e o certificado a ser usado.</span><span class="sxs-lookup"><span data-stu-id="60f2f-179">In the **Add SSL Binding** page, use the dropdowns to select the domain name to secure, and the certificate to use.</span></span>

> [!NOTE]
> <span data-ttu-id="60f2f-180">Se você carregou o certificado, mas não consegue ver os nomes de domínio no menu suspenso **Nome do host**, tente atualizar a página do navegador.</span><span class="sxs-lookup"><span data-stu-id="60f2f-180">If you have uploaded your certificate but don't see the domain name(s) in the **Hostname** dropdown, try refreshing the browser page.</span></span>
>
>

<span data-ttu-id="60f2f-181">Em **Tipo SSL**, selecione se deseja usar **[SNI (Indicação de Nome de Servidor)](http://en.wikipedia.org/wiki/Server_Name_Indication)** ou SSL baseado em IP.</span><span class="sxs-lookup"><span data-stu-id="60f2f-181">In **SSL Type**, select whether to use **[Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** or IP-based SSL.</span></span>

- <span data-ttu-id="60f2f-182">**SSL baseado em SNI** – várias associações SSL baseadas em SNI podem ser adicionadas.</span><span class="sxs-lookup"><span data-stu-id="60f2f-182">**SNI-based SSL** - Multiple SNI-based SSL bindings may be added.</span></span> <span data-ttu-id="60f2f-183">Esta opção permite que vários certificados SSL protejam vários domínios no mesmo endereço IP.</span><span class="sxs-lookup"><span data-stu-id="60f2f-183">This option allows multiple SSL certificates to secure multiple domains on the same IP address.</span></span> <span data-ttu-id="60f2f-184">Navegadores mais modernos (incluindo Internet Explorer, Chrome, Firefox e Opera) dão suporte ao SNI (encontre informações de suporte ao navegador mais abrangentes em [Indicação de Nome de Servidor](http://wikipedia.org/wiki/Server_Name_Indication)).</span><span class="sxs-lookup"><span data-stu-id="60f2f-184">Most modern browsers (including Internet Explorer, Chrome, Firefox, and Opera) support SNI (find more comprehensive browser support information at [Server Name Indication](http://wikipedia.org/wiki/Server_Name_Indication)).</span></span>
- <span data-ttu-id="60f2f-185">**SSL baseado em IP** – apenas uma associação SSL baseada em IP pode ser adicionada.</span><span class="sxs-lookup"><span data-stu-id="60f2f-185">**IP-based SSL** - Only one IP-based SSL binding may be added.</span></span> <span data-ttu-id="60f2f-186">Esta opção permite apenas um certificado SSL para proteger um endereço IP público dedicado.</span><span class="sxs-lookup"><span data-stu-id="60f2f-186">This option allows only one SSL certificate to secure a dedicated public IP address.</span></span> <span data-ttu-id="60f2f-187">Para proteger vários domínios, você deve protegê-los todos usando o mesmo certificado SSL.</span><span class="sxs-lookup"><span data-stu-id="60f2f-187">To secure multiple domains, you must secure them all using the same SSL certificate.</span></span> <span data-ttu-id="60f2f-188">Essa é a opção tradicional para associação de SSL.</span><span class="sxs-lookup"><span data-stu-id="60f2f-188">This is the traditional option for SSL binding.</span></span>

<span data-ttu-id="60f2f-189">Clique em **Adicionar Associação**.</span><span class="sxs-lookup"><span data-stu-id="60f2f-189">Click **Add Binding**.</span></span>

![Associar Certificado SSL](./media/app-service-web-tutorial-custom-ssl/bind-certificate.png)

<span data-ttu-id="60f2f-191">Quando o Serviço de Aplicativo terminar de carregar o certificado, ele aparecerá nas seções de **associações SSL**.</span><span class="sxs-lookup"><span data-stu-id="60f2f-191">When App Service finishes uploading your certificate, it appears in the **SSL bindings** sections.</span></span>

![Certificado associado ao aplicativo Web](./media/app-service-web-tutorial-custom-ssl/certificate-bound.png)

## <a name="remap-a-record-for-ip-ssl"></a><span data-ttu-id="60f2f-193">Remapear um registro para IP SSL</span><span class="sxs-lookup"><span data-stu-id="60f2f-193">Remap A record for IP SSL</span></span>

<span data-ttu-id="60f2f-194">Se você não usar SSL com base em IP em seu aplicativo Web, pule para [Testar o HTTPS para seu domínio personalizado](#test).</span><span class="sxs-lookup"><span data-stu-id="60f2f-194">If you don't use IP-based SSL in your web app, skip to [Test HTTPS for your custom domain](#test).</span></span>

<span data-ttu-id="60f2f-195">Por padrão, o seu aplicativo Web usa um endereço IP público compartilhado.</span><span class="sxs-lookup"><span data-stu-id="60f2f-195">By default, your web app uses a shared public IP address.</span></span> <span data-ttu-id="60f2f-196">Quando você associa um certificado ao SSL baseado em IP, o Serviço de Aplicativo cria um novo endereço IP dedicado para o aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="60f2f-196">When you bind a certificate with IP-based SSL, App Service creates a new, dedicated IP address for your web app.</span></span>

<span data-ttu-id="60f2f-197">Se você tiver mapeado um registro A para seu aplicativo Web, atualize o Registro do domínio com esse novo endereço IP dedicado.</span><span class="sxs-lookup"><span data-stu-id="60f2f-197">If you have mapped an A record to your web app, update your domain registry with this new, dedicated IP address.</span></span>

<span data-ttu-id="60f2f-198">A página **domínio personalizado** de seu aplicativo Web é atualizada com o novo endereço IP dedicado.</span><span class="sxs-lookup"><span data-stu-id="60f2f-198">Your web app's **Custom domain** page is updated with the new, dedicated IP address.</span></span> <span data-ttu-id="60f2f-199">[Copie esse endereço IP](app-service-web-tutorial-custom-domain.md#info) e, em seguida, [remapeie o registro](app-service-web-tutorial-custom-domain.md#map-an-a-record) para esse novo endereço IP.</span><span class="sxs-lookup"><span data-stu-id="60f2f-199">[Copy this IP address](app-service-web-tutorial-custom-domain.md#info), then [remap the A record](app-service-web-tutorial-custom-domain.md#map-an-a-record) to this new IP address.</span></span>

<a name="test"></a>

## <a name="test-https"></a><span data-ttu-id="60f2f-200">Testar HTTPS</span><span class="sxs-lookup"><span data-stu-id="60f2f-200">Test HTTPS</span></span>

<span data-ttu-id="60f2f-201">Agora, tudo o que resta fazer é certificar-se de que o HTTPS funcione com seu domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="60f2f-201">All that's left to do now is to make sure that HTTPS works for your custom domain.</span></span> <span data-ttu-id="60f2f-202">Em vários navegadores, navegue até `https://<your.custom.domain>` para ver se ele leva até seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="60f2f-202">In various browsers, browse to `https://<your.custom.domain>` to see that it serves up your web app.</span></span>

![Navegação no Portal para o aplicativo do Azure](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

> [!NOTE]
> <span data-ttu-id="60f2f-204">Se o seu aplicativo Web retorna erros de validação de certificado, você provavelmente está usando um certificado autoassinado.</span><span class="sxs-lookup"><span data-stu-id="60f2f-204">If your web app gives you certificate validation errors, you're probably using a self-signed certificate.</span></span>
>
> <span data-ttu-id="60f2f-205">Se não for o caso, talvez você tenha deixado de fora certificados intermediários quando exportou o certificado para o arquivo PFX.</span><span class="sxs-lookup"><span data-stu-id="60f2f-205">If that's not the case, you may have left out intermediate certificates when you export your certificate to the PFX file.</span></span>

<a name="bkmk_enforce"></a>

## <a name="enforce-https"></a><span data-ttu-id="60f2f-206">Impor HTTPS</span><span class="sxs-lookup"><span data-stu-id="60f2f-206">Enforce HTTPS</span></span>

<span data-ttu-id="60f2f-207">O Serviço de Aplicativo *não* impõe o HTTPS, de modo que qualquer um ainda pode acessar seu aplicativo Web usando HTTP.</span><span class="sxs-lookup"><span data-stu-id="60f2f-207">App Service does *not* enforce HTTPS, so anyone can still access your web app using HTTP.</span></span> <span data-ttu-id="60f2f-208">Para impor o HTTPS ao aplicativo Web, defina uma regra de reescrita no arquivo _web.config_ do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="60f2f-208">To enforce HTTPS for your web app, define a rewrite rule in the _web.config_ file for your web app.</span></span> <span data-ttu-id="60f2f-209">Todo aplicativo do Serviço de Aplicativo usa esse arquivo, independentemente da estrutura de linguagem do seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="60f2f-209">App Service uses this file, regardless of the language framework of your web app.</span></span>

> [!NOTE]
> <span data-ttu-id="60f2f-210">Há um redirecionamento de solicitações específico a um idioma.</span><span class="sxs-lookup"><span data-stu-id="60f2f-210">There is language-specific redirection of requests.</span></span> <span data-ttu-id="60f2f-211">O ASP.NET MVC pode usar o filtro [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) em vez da regra de reescrita em _web.config_.</span><span class="sxs-lookup"><span data-stu-id="60f2f-211">ASP.NET MVC can use the [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filter instead of the rewrite rule in _web.config_.</span></span>

<span data-ttu-id="60f2f-212">Se você é um desenvolvedor do .NET, você deve estar relativamente familiarizado com esse arquivo.</span><span class="sxs-lookup"><span data-stu-id="60f2f-212">If you're a .NET developer, you should be relatively familiar with this file.</span></span> <span data-ttu-id="60f2f-213">Ele está na raiz de sua solução.</span><span class="sxs-lookup"><span data-stu-id="60f2f-213">It is in the root of your solution.</span></span>

<span data-ttu-id="60f2f-214">Como alternativa, se você desenvolve com PHP, Node.js, Python ou Java, há uma chance de termos gerado esse arquivo em seu nome no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="60f2f-214">Alternatively, if you develop with PHP, Node.js, Python, or Java, there is a chance we generated this file on your behalf in App Service.</span></span>

<span data-ttu-id="60f2f-215">Conecte-se ao ponto de extremidade FTP do seu aplicativo Web, seguindo as instruções em [Implantar seu aplicativo no Serviço de Aplicativo do Azure usando FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="60f2f-215">Connect to your web app's FTP endpoint by following the instructions at [Deploy your app to Azure App Service using FTP/S](app-service-deploy-ftp.md).</span></span>

<span data-ttu-id="60f2f-216">Esse arquivo deve estar localizado em _/home/site/wwwroot_.</span><span class="sxs-lookup"><span data-stu-id="60f2f-216">This file should be located in _/home/site/wwwroot_.</span></span> <span data-ttu-id="60f2f-217">Caso contrário, crie um arquivo _web.config_ nesta pasta com o seguinte XML:</span><span class="sxs-lookup"><span data-stu-id="60f2f-217">If not, create a _web.config_ file in this folder with the following XML:</span></span>

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

<span data-ttu-id="60f2f-218">Para um arquivo _web.config_ existente, copie todo o elemento `<rule>` para o elemento `configuration/system.webServer/rewrite/rules` do _web.config_.</span><span class="sxs-lookup"><span data-stu-id="60f2f-218">For an existing _web.config_ file, copy the entire `<rule>` element into your _web.config_'s `configuration/system.webServer/rewrite/rules` element.</span></span> <span data-ttu-id="60f2f-219">Se houver outros elementos `<rule>` no _web.config_, coloque o elemento `<rule>` copiado antes dos outros elementos `<rule>`.</span><span class="sxs-lookup"><span data-stu-id="60f2f-219">If there are other `<rule>` elements in your _web.config_, place the copied `<rule>` element before the other `<rule>` elements.</span></span>

<span data-ttu-id="60f2f-220">Essa regra retorna um HTTP 301 (redirecionamento permanente) para o protocolo HTTPS sempre que o usuário fizer uma solicitação HTTP ao aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="60f2f-220">This rule returns an HTTP 301 (permanent redirect) to the HTTPS protocol whenever the user makes an HTTP request to your web app.</span></span> <span data-ttu-id="60f2f-221">Por exemplo, ele redireciona de `http://contoso.com` para `https://contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="60f2f-221">For example, it redirects from `http://contoso.com` to `https://contoso.com`.</span></span>

<span data-ttu-id="60f2f-222">Para obter mais informações sobre o Módulo de Reescrita de URL do IIS, consulte a documentação [Reescrita de URL](http://www.iis.net/downloads/microsoft/url-rewrite) .</span><span class="sxs-lookup"><span data-stu-id="60f2f-222">For more information on the IIS URL Rewrite module, see the [URL Rewrite](http://www.iis.net/downloads/microsoft/url-rewrite) documentation.</span></span>

## <a name="enforce-https-for-web-apps-on-linux"></a><span data-ttu-id="60f2f-223">Impor o HTTPS a aplicativos Web no Linux</span><span class="sxs-lookup"><span data-stu-id="60f2f-223">Enforce HTTPS for Web Apps on Linux</span></span>

<span data-ttu-id="60f2f-224">O Serviço de Aplicativo no Linux *não* impõe o HTTPS e, portanto, qualquer pessoa ainda pode acessar o aplicativo Web usando o HTTP.</span><span class="sxs-lookup"><span data-stu-id="60f2f-224">App Service on Linux does *not* enforce HTTPS, so anyone can still access your web app using HTTP.</span></span> <span data-ttu-id="60f2f-225">Para impor o HTTPS ao aplicativo Web, defina uma regra de reescrita no arquivo _.htaccess_ do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="60f2f-225">To enforce HTTPS for your web app, define a rewrite rule in the _.htaccess_ file for your web app.</span></span> 

<span data-ttu-id="60f2f-226">Conecte-se ao ponto de extremidade FTP do seu aplicativo Web, seguindo as instruções em [Implantar seu aplicativo no Serviço de Aplicativo do Azure usando FTP/S](app-service-deploy-ftp.md).</span><span class="sxs-lookup"><span data-stu-id="60f2f-226">Connect to your web app's FTP endpoint by following the instructions at [Deploy your app to Azure App Service using FTP/S](app-service-deploy-ftp.md).</span></span>

<span data-ttu-id="60f2f-227">Em _/home/site/wwwroot_, crie um arquivo _.htaccess_ com o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="60f2f-227">In _/home/site/wwwroot_, create an _.htaccess_ file with the following code:</span></span>

```
RewriteEngine On
RewriteCond %{HTTP:X-ARR-SSL} ^$
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

<span data-ttu-id="60f2f-228">Essa regra retorna um HTTP 301 (redirecionamento permanente) para o protocolo HTTPS sempre que o usuário fizer uma solicitação HTTP ao aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="60f2f-228">This rule returns an HTTP 301 (permanent redirect) to the HTTPS protocol whenever the user makes an HTTP request to your web app.</span></span> <span data-ttu-id="60f2f-229">Por exemplo, ele redireciona de `http://contoso.com` para `https://contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="60f2f-229">For example, it redirects from `http://contoso.com` to `https://contoso.com`.</span></span>

## <a name="automate-with-scripts"></a><span data-ttu-id="60f2f-230">Automatizar com scripts</span><span class="sxs-lookup"><span data-stu-id="60f2f-230">Automate with scripts</span></span>

<span data-ttu-id="60f2f-231">Você pode automatizar associações SSL para seu aplicativo Web com scripts, usando a [CLI do Azure](/cli/azure/install-azure-cli) ou o [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="60f2f-231">You can automate SSL bindings for your web app with scripts, using the [Azure CLI](/cli/azure/install-azure-cli) or [Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="azure-cli"></a><span data-ttu-id="60f2f-232">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="60f2f-232">Azure CLI</span></span>

<span data-ttu-id="60f2f-233">O comando a seguir carrega um arquivo PFX exportado e obtém a impressão digital.</span><span class="sxs-lookup"><span data-stu-id="60f2f-233">The following command uploads an exported PFX file and gets the thumbprint.</span></span>

```bash
thumbprint=$(az appservice web config ssl upload \
    --name <app_name> \
    --resource-group <resource_group_name> \
    --certificate-file <path_to_PFX_file> \
    --certificate-password <PFX_password> \
    --query thumbprint \
    --output tsv)
```

<span data-ttu-id="60f2f-234">O comando a seguir adiciona uma associação de SSL baseado em SNI usando a impressão digital do comando anterior.</span><span class="sxs-lookup"><span data-stu-id="60f2f-234">The following command adds an SNI-based SSL binding, using the thumbprint from the previous command.</span></span>

```bash
az appservice web config ssl bind \
    --name <app_name> \
    --resource-group <resource_group_name>
    --certificate-thumbprint $thumbprint \
    --ssl-type SNI \
```

### <a name="azure-powershell"></a><span data-ttu-id="60f2f-235">PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="60f2f-235">Azure PowerShell</span></span>

<span data-ttu-id="60f2f-236">O comando a seguir carrega um arquivo PFX exportado e adiciona uma associação de SSL baseado em SNI.</span><span class="sxs-lookup"><span data-stu-id="60f2f-236">The following command uploads an exported PFX file and adds an SNI-based SSL binding.</span></span>

```PowerShell
New-AzureRmWebAppSSLBinding `
    -WebAppName <app_name> `
    -ResourceGroupName <resource_group_name> `
    -Name <dns_name> `
    -CertificateFilePath <path_to_PFX_file> `
    -CertificatePassword <PFX_password> `
    -SslState SniEnabled
```

## <a name="next-steps"></a><span data-ttu-id="60f2f-237">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="60f2f-237">Next steps</span></span>

<span data-ttu-id="60f2f-238">Neste tutorial, você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="60f2f-238">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="60f2f-239">Atualizar o tipo de preço do aplicativo</span><span class="sxs-lookup"><span data-stu-id="60f2f-239">Upgrade your app's pricing tier</span></span>
> * <span data-ttu-id="60f2f-240">Associar o certificado SSL personalizado ao Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="60f2f-240">Bind your custom SSL certificate to App Service</span></span>
> * <span data-ttu-id="60f2f-241">Impor HTTPS para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="60f2f-241">Enforce HTTPS for your app</span></span>
> * <span data-ttu-id="60f2f-242">Automatizar a associação de certificado SSL com scripts</span><span class="sxs-lookup"><span data-stu-id="60f2f-242">Automate SSL certificate binding with scripts</span></span>

<span data-ttu-id="60f2f-243">Vá para o próximo tutorial para saber como usar a Rede de Distribuição de Conteúdo do Azure.</span><span class="sxs-lookup"><span data-stu-id="60f2f-243">Advance to the next tutorial to learn how to use Azure Content Delivery Network.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="60f2f-244">Adicionar uma CDN (Rede de Distribuição de Conteúdo) a um Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="60f2f-244">Add a Content Delivery Network (CDN) to an Azure App Service</span></span>](app-service-web-tutorial-content-delivery-network.md)
