---
title: "aaaAdd um SSL certificado tooyour aplicativo de serviço de aplicativo do Azure | Microsoft Docs"
description: "Saiba como tooadd um SSL certificado tooyour aplicativo de serviço de aplicativo."
services: app-service
documentationcenter: .net
author: ahmedelnably
manager: stefsch
editor: cephalin
tags: buy-ssl-certificates
ms.assetid: cdb9719a-c8eb-47e5-817f-e15eaea1f5f8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/19/2016
ms.author: apurvajo
ms.openlocfilehash: f4652794ba745790a073264f6a102c64c73e8db0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="buy-and-configure-an-ssl-certificate-for-your-azure-app-service"></a><span data-ttu-id="0fab3-103">Comprar e configurar um certificado SSL para seu Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="0fab3-103">Buy and Configure an SSL Certificate for your Azure App Service</span></span>

<span data-ttu-id="0fab3-104">Neste tutorial, você irá proteger seu aplicativo web com a compra de um certificado SSL para o  **[serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714)** armazená-los em segurança no [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis)e associá-lo a um domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="0fab3-104">In this tutorial, you will secure your web app by purchasing an SSL certificate for your **[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)**, securely storing it in [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis), and associating it with a custom domain.</span></span>

## <a name="step-1---log-in-tooazure"></a><span data-ttu-id="0fab3-105">Etapa 1 - Log em tooAzure</span><span class="sxs-lookup"><span data-stu-id="0fab3-105">Step 1 - Log in tooAzure</span></span>

<span data-ttu-id="0fab3-106">Faça logon no toohello portal do Azure em http://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="0fab3-106">Log in toohello Azure portal at http://portal.azure.com</span></span>

## <a name="step-2---place-an-ssl-certificate-order"></a><span data-ttu-id="0fab3-107">Etapa 2: Fazer um pedido de certificado SSL</span><span class="sxs-lookup"><span data-stu-id="0fab3-107">Step 2 - Place an SSL Certificate order</span></span>

<span data-ttu-id="0fab3-108">Você pode colocar um pedido de certificado SSL, criando um novo [certificado de serviço de aplicativo](https://portal.azure.com/#create/Microsoft.SSL) em Olá **portal do Azure**.</span><span class="sxs-lookup"><span data-stu-id="0fab3-108">You can place an SSL Certificate order by creating a new [App Service Certificate](https://portal.azure.com/#create/Microsoft.SSL) In hello **Azure portal**.</span></span>

![Criação de certificado](./media/app-service-web-purchase-ssl-web-site/createssl.png)

<span data-ttu-id="0fab3-110">Insira um amigável **nome** para o SSL de certificado e insira Olá **nome de domínio**</span><span class="sxs-lookup"><span data-stu-id="0fab3-110">Enter a friendly **Name** for your SSL certificate and enter hello **Domain Name**</span></span>

> [!NOTE]
> <span data-ttu-id="0fab3-111">Esta é uma das partes mais importantes de saudação do processo de compra de saudação.</span><span class="sxs-lookup"><span data-stu-id="0fab3-111">This is one of hello most critical parts of hello purchase process.</span></span> <span data-ttu-id="0fab3-112">Verifique se tooenter corrija o nome do host (domínio personalizado) que você deseja tooprotect com esse certificado.</span><span class="sxs-lookup"><span data-stu-id="0fab3-112">Make sure tooenter correct host name (custom domain) that you want tooprotect with this certificate.</span></span> <span data-ttu-id="0fab3-113">**NÃO** acrescentar o nome de Host de saudação com WWW.</span><span class="sxs-lookup"><span data-stu-id="0fab3-113">**DO NOT** append hello Host name with WWW.</span></span> 
>

<span data-ttu-id="0fab3-114">Selecione seu **assinatura**, **grupo de recursos**, e **SKU de certificado**</span><span class="sxs-lookup"><span data-stu-id="0fab3-114">Select your **Subscription**, **Resource Group**, and **Certificate SKU**</span></span>

> [!WARNING]
> <span data-ttu-id="0fab3-115">Certificados de serviço de aplicativo só pode ser usados por outros serviços de aplicativo no hello mesma assinatura.</span><span class="sxs-lookup"><span data-stu-id="0fab3-115">App Service Certificates can only be used by other App Services within hello same subscription.</span></span>  
>

## <a name="step-3---store-hello-certificate-in-azure-key-vault"></a><span data-ttu-id="0fab3-116">Etapa 3 - certificado de saudação do repositório no cofre de chaves do Azure</span><span class="sxs-lookup"><span data-stu-id="0fab3-116">Step 3 - Store hello certificate in Azure Key Vault</span></span>

> [!NOTE]
> <span data-ttu-id="0fab3-117">O [Cofre da Chave](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) do Azure ajuda a proteger chaves criptográficas e segredos usados por aplicativos e serviços em nuvem.</span><span class="sxs-lookup"><span data-stu-id="0fab3-117">[Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) is an Azure service that helps safeguard cryptographic keys and secrets used by cloud applications and services.</span></span>
>

<span data-ttu-id="0fab3-118">Após a conclusão da saudação aquisição do certificado SSL, você precisa tooopen [certificados de serviço de aplicativo](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders) folha de recursos.</span><span class="sxs-lookup"><span data-stu-id="0fab3-118">Once hello SSL Certificate purchase is complete, you need tooopen [App Service Certificates](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders) Resource blade.</span></span>

![Inserir imagem de toostore pronto em KV](./media/app-service-web-purchase-ssl-web-site/ReadyKV.png)

<span data-ttu-id="0fab3-120">Você observará que o status do certificado é **"Emissão pendente"** , há algumas etapas mais precisar toocomplete antes de começar a usar este certificado.</span><span class="sxs-lookup"><span data-stu-id="0fab3-120">You will notice that Certificate status is **“Pending Issuance”** as there are few more steps you need toocomplete before you can start using this certificate.</span></span>

<span data-ttu-id="0fab3-121">Clique em **configuração do certificado** dentro de folha de propriedades do certificado e clique em **etapa 1: armazenamento** toostore esse certificado no cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="0fab3-121">Click **Certificate Configuration** inside Certificate Properties blade and Click on **Step 1: Store** toostore this certificate in Azure Key Vault.</span></span>

<span data-ttu-id="0fab3-122">De **Status cofre da chave** folha, clique em **chave cofre repositório** toochoose um toostore de Cofre de chaves existente esse certificado **ou criar novo cofre de chaves** toocreate nova chave de cofre dentro da mesmo assinatura e grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="0fab3-122">From **Key Vault Status** Blade, click **Key Vault Repository** toochoose an existing Key Vault toostore this certificate **OR Create New Key Vault** toocreate new Key Vault inside same subscription and resource group.</span></span>

> [!NOTE]
> <span data-ttu-id="0fab3-123">O cofre da chave do Azure tem encargos mínimo para armazenar o certificado.</span><span class="sxs-lookup"><span data-stu-id="0fab3-123">Azure Key Vault has minimal charges for storing this certificate.</span></span>
> <span data-ttu-id="0fab3-124">Para obter mais informações, consulte  **[detalhes de preços do Azure Key Vault](https://azure.microsoft.com/pricing/details/key-vault/)**.</span><span class="sxs-lookup"><span data-stu-id="0fab3-124">For more information, see **[Azure Key Vault Pricing Details](https://azure.microsoft.com/pricing/details/key-vault/)**.</span></span>
>

<span data-ttu-id="0fab3-125">Depois de selecionar Olá repositório de Cofre de chave toostore esse certificado no, Olá **repositório** opção deve mostrar o êxito.</span><span class="sxs-lookup"><span data-stu-id="0fab3-125">Once you have selected hello Key Vault Repository toostore this certificate in, hello **Store** option should show success.</span></span>

![Inserir imagem de sucesso de repositório em KV](./media/app-service-web-purchase-ssl-web-site/KVStoreSuccess.png)

## <a name="step-4---verify-hello-domain-ownership"></a><span data-ttu-id="0fab3-127">Etapa 4 - verificar Olá propriedade do domínio</span><span class="sxs-lookup"><span data-stu-id="0fab3-127">Step 4 - Verify hello Domain Ownership</span></span>

> [!NOTE]
> <span data-ttu-id="0fab3-128">Há três tipos de verificação de domínio de certificados de serviço de aplicativo com suporte: verificação do domínio, email, Manual.</span><span class="sxs-lookup"><span data-stu-id="0fab3-128">There are three types of domain verification supported by App service Certificates: Domain, Mail, Manual Verification.</span></span> <span data-ttu-id="0fab3-129">Essas são explicadas em mais detalhes no hello [avançado seção](#advanced).</span><span class="sxs-lookup"><span data-stu-id="0fab3-129">These are explained in more details in hello [Advanced section](#advanced).</span></span>

<span data-ttu-id="0fab3-130">De Olá mesmo **configuração do certificado** folha que você usou na etapa 3, clique em **etapa 2: Verifique se**.</span><span class="sxs-lookup"><span data-stu-id="0fab3-130">From hello same **Certificate Configuration** blade you used in Step 3, click **Step 2: Verify**.</span></span>

<span data-ttu-id="0fab3-131">**Verificação de domínio** este é o processo mais conveniente Olá **somente se** tiver  **[comprado seu domínio personalizado de serviço de aplicativo do Azure.](custom-dns-web-site-buydomains-web-app.md)**</span><span class="sxs-lookup"><span data-stu-id="0fab3-131">**Domain Verification** This is hello most convenient process **ONLY IF** you have **[purchased your custom domain from Azure App Service.](custom-dns-web-site-buydomains-web-app.md)**</span></span>
<span data-ttu-id="0fab3-132">Clique em **verificar** botão toocomplete nesta etapa.</span><span class="sxs-lookup"><span data-stu-id="0fab3-132">Click on **Verify** button toocomplete this step.</span></span>

![Inserir imagem de verificação de domínio](./media/app-service-web-purchase-ssl-web-site/DomainVerificationRequired.png)

<span data-ttu-id="0fab3-134">Depois de clicar em **verificar**, use Olá **atualizar** botão até Olá **verificar** opção deve mostrar o êxito.</span><span class="sxs-lookup"><span data-stu-id="0fab3-134">After clicking **Verify**, use hello **Refresh** button until hello **Verify** option should show success.</span></span>

![Inserir imagem de verificar o êxito na KV](./media/app-service-web-purchase-ssl-web-site/KVVerifySuccess.png)

## <a name="step-5---assign-certificate-tooapp-service-app"></a><span data-ttu-id="0fab3-136">Etapa 5: atribuir tooApp de certificado do serviço de aplicativo</span><span class="sxs-lookup"><span data-stu-id="0fab3-136">Step 5 - Assign Certificate tooApp Service App</span></span>

> [!NOTE]
> <span data-ttu-id="0fab3-137">Antes de executar as etapas de saudação nesta seção, você deve ter associado um nome de domínio personalizado com seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0fab3-137">Before performing hello steps in this section, you must have associated a custom domain name with your app.</span></span> <span data-ttu-id="0fab3-138">Para saber mais, confira **[Configurando um nome de domínio personalizado para um aplicativo Web.](app-service-web-tutorial-custom-domain.md)**</span><span class="sxs-lookup"><span data-stu-id="0fab3-138">For more information, see **[Configuring a custom domain name for a web app.](app-service-web-tutorial-custom-domain.md)**</span></span>
>

<span data-ttu-id="0fab3-139">Em hello  **[portal do Azure](https://portal.azure.com/)**, clique em Olá **do serviço de aplicativo** opção esquerda Olá da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="0fab3-139">In hello **[Azure portal](https://portal.azure.com/)**, click hello **App Service** option on hello left of hello page.</span></span>

<span data-ttu-id="0fab3-140">Clique em nome de saudação de seu aplicativo toowhich você deseja tooassign esse certificado.</span><span class="sxs-lookup"><span data-stu-id="0fab3-140">Click hello name of your app toowhich you want tooassign this certificate.</span></span>

<span data-ttu-id="0fab3-141">Em Olá **configurações**, clique em **certificados SSL**.</span><span class="sxs-lookup"><span data-stu-id="0fab3-141">In hello **Settings**, click **SSL certificates**.</span></span>

<span data-ttu-id="0fab3-142">Clique em **Importar certificado de serviço de aplicativo** e selecione Olá certificado que você acabou de adquirir.</span><span class="sxs-lookup"><span data-stu-id="0fab3-142">Click **Import App Service Certificate** and select hello certificate that you just purchased.</span></span>

![inserir imagem de Importar Certificado](./media/app-service-web-purchase-ssl-web-site/ImportCertificate.png)

<span data-ttu-id="0fab3-144">Em hello **associações ssl** seção clique **adicionar associações**, usar toosecure de nome de domínio Olá menus suspensos tooselect Olá com SSL e Olá toouse do certificado.</span><span class="sxs-lookup"><span data-stu-id="0fab3-144">In hello **ssl bindings** section Click on **Add bindings**, and use hello dropdowns tooselect hello domain name toosecure with SSL, and hello certificate toouse.</span></span> <span data-ttu-id="0fab3-145">Você também pode selecionar se toouse  **[indicação de nome de servidor (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)**  ou SSL baseado em IP.</span><span class="sxs-lookup"><span data-stu-id="0fab3-145">You may also select whether toouse **[Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** or IP based SSL.</span></span>

![inserir imagem de Associações SSL](./media/app-service-web-purchase-ssl-web-site/SSLBindings.png)

<span data-ttu-id="0fab3-147">Clique em **Adicionar associação** toosave Olá alterações e habilitar o SSL.</span><span class="sxs-lookup"><span data-stu-id="0fab3-147">Click **Add Binding** toosave hello changes and enable SSL.</span></span>

> [!NOTE]
> <span data-ttu-id="0fab3-148">Se você selecionou **SSL baseado em IP** e seu domínio personalizado está configurado para usar um registro, você deve executar etapas adicionais de saudação.</span><span class="sxs-lookup"><span data-stu-id="0fab3-148">If you selected **IP based SSL** and your custom domain is configured using an A record, you must perform hello following additional steps.</span></span> <span data-ttu-id="0fab3-149">Essas são explicadas em mais detalhes no hello [avançado seção](#Advanced).</span><span class="sxs-lookup"><span data-stu-id="0fab3-149">These are explained in more details in hello [Advanced section](#Advanced).</span></span>

<span data-ttu-id="0fab3-150">Neste ponto, você deve ser capaz de toovisit seu aplicativo usando `HTTPS://` em vez de `HTTP://` tooverify que Olá certificado foi configurado corretamente.</span><span class="sxs-lookup"><span data-stu-id="0fab3-150">At this point, you should be able toovisit your app using `HTTPS://` instead of `HTTP://` tooverify that hello certificate has been configured correctly.</span></span>

<!--![insert image of https](./media/app-service-web-purchase-ssl-web-site/Https.png)-->

## <a name="step-6---management-tasks"></a><span data-ttu-id="0fab3-151">Etapa 6 – Tarefas de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="0fab3-151">Step 6 - Management tasks</span></span>

### <a name="azure-cli"></a><span data-ttu-id="0fab3-152">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="0fab3-152">Azure CLI</span></span>

[!code-azurecli[main](../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")] 

### <a name="powershell"></a><span data-ttu-id="0fab3-153">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0fab3-153">PowerShell</span></span>

[!code-powershell[main](../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate to a web app")]

## <a name="advanced"></a><span data-ttu-id="0fab3-154">Avançado</span><span class="sxs-lookup"><span data-stu-id="0fab3-154">Advanced</span></span>

### <a name="verifying-domain-ownership"></a><span data-ttu-id="0fab3-155">Verificando a propriedade de domínio</span><span class="sxs-lookup"><span data-stu-id="0fab3-155">Verifying Domain Ownership</span></span>

<span data-ttu-id="0fab3-156">Há dois outros tipos de suporte para certificados de serviço do aplicativo de verificação de domínio: Mail e Verificação Manual.</span><span class="sxs-lookup"><span data-stu-id="0fab3-156">There are two more types of domain verification supported by App service Certificates: Mail, and Manual Verification.</span></span>

#### <a name="mail-verification"></a><span data-ttu-id="0fab3-157">Verificação por email</span><span class="sxs-lookup"><span data-stu-id="0fab3-157">Mail Verification</span></span>

<span data-ttu-id="0fab3-158">Toohello que endereços de Email associados com este domínio personalizado já foi enviado ao email de verificação.</span><span class="sxs-lookup"><span data-stu-id="0fab3-158">Verification email has already been sent toohello Email Address(es) associated with this custom domain.</span></span>
<span data-ttu-id="0fab3-159">etapa de verificação de Email do toocomplete Olá, abra o email de saudação e clique em link de verificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="0fab3-159">toocomplete hello Email verification step, open hello email and click hello verification link.</span></span>

![Inserir imagem de verificação de email](./media/app-service-web-purchase-ssl-web-site/KVVerifyEmailSuccess.png)

<span data-ttu-id="0fab3-161">Se você precisar de email de verificação tooresend hello, clique em Olá **reenviar Email** botão.</span><span class="sxs-lookup"><span data-stu-id="0fab3-161">If you need tooresend hello verification email, click hello **Resend Email** button.</span></span>

#### <a name="manual-verification"></a><span data-ttu-id="0fab3-162">Verificação manual</span><span class="sxs-lookup"><span data-stu-id="0fab3-162">Manual Verification</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0fab3-163">Verificação da página da Web em HTML (funciona somente com SKU de Certificado Padrão)</span><span class="sxs-lookup"><span data-stu-id="0fab3-163">HTML Web Page Verification (only works with Standard Certificate SKU)</span></span>
>

1. <span data-ttu-id="0fab3-164">Crie um arquivo HTML chamado **"starfield.html"**</span><span class="sxs-lookup"><span data-stu-id="0fab3-164">Create an HTML file named **"starfield.html"**</span></span>

1. <span data-ttu-id="0fab3-165">Conteúdo desse arquivo deve ser nome exato de saudação do hello Token de verificação do domínio.</span><span class="sxs-lookup"><span data-stu-id="0fab3-165">Content of this file should be hello exact name of hello Domain Verification Token.</span></span> <span data-ttu-id="0fab3-166">(Você pode copiar token Olá de saudação folha de Status de verificação de domínio)</span><span class="sxs-lookup"><span data-stu-id="0fab3-166">(You can copy hello token from hello Domain Verification Status Blade)</span></span>

1. <span data-ttu-id="0fab3-167">Carregue esse arquivo na raiz de saudação do servidor de web hello hospede seu domínio`/.well-known/pki-validation/starfield.html`</span><span class="sxs-lookup"><span data-stu-id="0fab3-167">Upload this file at hello root of hello web server hosting your domain `/.well-known/pki-validation/starfield.html`</span></span>

1. <span data-ttu-id="0fab3-168">Clique em **atualizar** tooupdate status do certificado Olá após a conclusão da verificação.</span><span class="sxs-lookup"><span data-stu-id="0fab3-168">Click **Refresh** tooupdate hello certificate status after verification is completed.</span></span> <span data-ttu-id="0fab3-169">Pode levar alguns minutos para toocomplete de verificação.</span><span class="sxs-lookup"><span data-stu-id="0fab3-169">It might take few minutes for verification toocomplete.</span></span>

> [!TIP]
> <span data-ttu-id="0fab3-170">Verifique se um terminal usando `curl -G http://<domain>/.well-known/pki-validation/starfield.html` resposta Olá deve conter Olá `<verification-token>`.</span><span class="sxs-lookup"><span data-stu-id="0fab3-170">Verify in a terminal using `curl -G http://<domain>/.well-known/pki-validation/starfield.html` hello response should contain hello `<verification-token>`.</span></span>

#### <a name="dns-txt-record-verification"></a><span data-ttu-id="0fab3-171">Verificação de registro TXT do DNS</span><span class="sxs-lookup"><span data-stu-id="0fab3-171">DNS TXT Record Verification</span></span>

1. <span data-ttu-id="0fab3-172">Usando o Gerenciador de DNS, criar um registro TXT no hello `@` subdomínio com toohello igual do valor o Token de verificação do domínio.</span><span class="sxs-lookup"><span data-stu-id="0fab3-172">Using your DNS manager, Create a TXT record on hello `@` subdomain with value equal toohello Domain Verification Token.</span></span>
1. <span data-ttu-id="0fab3-173">Clique em **"Atualizar"** tooupdate Olá após a conclusão da verificação de status do certificado.</span><span class="sxs-lookup"><span data-stu-id="0fab3-173">Click **“Refresh”** tooupdate hello Certificate status after verification is completed.</span></span>

> [!TIP]
> <span data-ttu-id="0fab3-174">Você precisa de um registro TXT do toocreate em `@.<domain>` com valor `<verification-token>`.</span><span class="sxs-lookup"><span data-stu-id="0fab3-174">You need toocreate a TXT record on `@.<domain>` with value `<verification-token>`.</span></span>

### <a name="assign-certificate-tooapp-service-app"></a><span data-ttu-id="0fab3-175">Atribuir tooApp de certificado do serviço de aplicativo</span><span class="sxs-lookup"><span data-stu-id="0fab3-175">Assign Certificate tooApp Service App</span></span>

<span data-ttu-id="0fab3-176">Se você selecionou **SSL baseado em IP** e seu domínio personalizado está configurado para usar um registro, você deve executar etapas adicionais de saudação:</span><span class="sxs-lookup"><span data-stu-id="0fab3-176">If you selected **IP based SSL** and your custom domain is configured using an A record, you must perform hello following additional steps:</span></span>

<span data-ttu-id="0fab3-177">Depois que você configurou associação SSL com base em um IP, um endereço IP dedicado é atribuído tooyour aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0fab3-177">After you have configured an IP based SSL binding, a dedicated IP address is assigned tooyour app.</span></span> <span data-ttu-id="0fab3-178">Você pode encontrar esse endereço IP em Olá **domínio personalizado** página em configurações do aplicativo, imediatamente acima Olá **nomes de host** seção.</span><span class="sxs-lookup"><span data-stu-id="0fab3-178">You can find this IP address on hello **Custom domain** page under settings of your app, right above hello **Hostnames** section.</span></span> <span data-ttu-id="0fab3-179">Ele é listado como **endereço IP externo**</span><span class="sxs-lookup"><span data-stu-id="0fab3-179">It is listed as **External IP Address**</span></span>

![inserir imagem de IP SSL](./media/app-service-web-purchase-ssl-web-site/virtual-ip-address.png)

<span data-ttu-id="0fab3-181">Observe que esse endereço IP é diferente do endereço IP virtual de saudação usado anteriormente registro Olá tooconfigure para seu domínio.</span><span class="sxs-lookup"><span data-stu-id="0fab3-181">Note that this IP address is different than hello virtual IP address used previously tooconfigure hello A record for your domain.</span></span> <span data-ttu-id="0fab3-182">Se você estiver configurado toouse SSL baseado em SNI ou não configurado toouse SSL, nenhum endereço será listado para esta entrada.</span><span class="sxs-lookup"><span data-stu-id="0fab3-182">If you are configured toouse SNI based SSL, or are not configured toouse SSL, no address is listed for this entry.</span></span>

<span data-ttu-id="0fab3-183">Usando ferramentas de saudação fornecidas por seu registrador de nome de domínio, modificar Olá um registro para o endereço IP do domínio personalizado nome toopoint toohello da etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="0fab3-183">Using hello tools provided by your domain name registrar, modify hello A record for your custom domain name toopoint toohello IP address from hello previous step.</span></span>

## <a name="rekey-and-sync-hello-certificate"></a><span data-ttu-id="0fab3-184">Rechavear e sincronização Olá certificado</span><span class="sxs-lookup"><span data-stu-id="0fab3-184">Rekey and Sync hello Certificate</span></span>

<span data-ttu-id="0fab3-185">Se você alguma vez precisar tooRekey seu certificado, selecione **rechavear e sincronização** opção **propriedades do certificado** folha.</span><span class="sxs-lookup"><span data-stu-id="0fab3-185">If you ever need tooRekey your certificate, select **Rekey and Sync** option from **Certificate Properties** Blade.</span></span>

<span data-ttu-id="0fab3-186">Clique em **rechavear** botão tooinitiate processo de saudação.</span><span class="sxs-lookup"><span data-stu-id="0fab3-186">Click **Rekey** Button tooinitiate hello process.</span></span> <span data-ttu-id="0fab3-187">Esse processo pode levar de 1 a 10 minutos toocomplete.</span><span class="sxs-lookup"><span data-stu-id="0fab3-187">This process can take 1-10 minutes toocomplete.</span></span>

![inserir imagem de Nova Chave SSL](./media/app-service-web-purchase-ssl-web-site/Rekey.png)

<span data-ttu-id="0fab3-189">Seu certificado de troca de chaves faz o certificado de saudação com um novo certificado emitido da autoridade de certificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="0fab3-189">Rekeying your certificate rolls hello certificate with a new certificate issued from hello certificate authority.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0fab3-190">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0fab3-190">Next Steps</span></span>

* [<span data-ttu-id="0fab3-191">Adicionar uma rede de fornecimento de conteúdo</span><span class="sxs-lookup"><span data-stu-id="0fab3-191">Add a Content Delivery Network</span></span>](app-service-web-tutorial-content-delivery-network.md)