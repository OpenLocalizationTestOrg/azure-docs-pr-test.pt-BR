---
title: "Adicionar um certificado SSL ao seu aplicativo de serviço de aplicativo do Azure | Microsoft Docs"
description: "Saiba como adicionar um certificado SSL ao seu aplicativo de serviço de aplicativo."
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
ms.openlocfilehash: 191dd7240ad15b4936a72bc27a2d0162350f3afb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="buy-and-configure-an-ssl-certificate-for-your-azure-app-service"></a><span data-ttu-id="ed3c1-103">Comprar e configurar um certificado SSL para seu Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="ed3c1-103">Buy and Configure an SSL Certificate for your Azure App Service</span></span>

<span data-ttu-id="ed3c1-104">Neste tutorial, você irá proteger seu aplicativo web com a compra de um certificado SSL para o  **[serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714)** armazená-los em segurança no [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis)e associá-lo a um domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-104">In this tutorial, you will secure your web app by purchasing an SSL certificate for your **[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)**, securely storing it in [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis), and associating it with a custom domain.</span></span>

## <a name="step-1---log-in-to-azure"></a><span data-ttu-id="ed3c1-105">Etapa 1 - Fazer logon no Azure</span><span class="sxs-lookup"><span data-stu-id="ed3c1-105">Step 1 - Log in to Azure</span></span>

<span data-ttu-id="ed3c1-106">Faça logon no Portal do Azure em http://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="ed3c1-106">Log in to the Azure portal at http://portal.azure.com</span></span>

## <a name="step-2---place-an-ssl-certificate-order"></a><span data-ttu-id="ed3c1-107">Etapa 2: Fazer um pedido de certificado SSL</span><span class="sxs-lookup"><span data-stu-id="ed3c1-107">Step 2 - Place an SSL Certificate order</span></span>

<span data-ttu-id="ed3c1-108">Você pode fazer um pedido de certificado SSL, criando um novo [certificado de serviço de aplicativo](https://portal.azure.com/#create/Microsoft.SSL) no **portal do Azure**.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-108">You can place an SSL Certificate order by creating a new [App Service Certificate](https://portal.azure.com/#create/Microsoft.SSL) In the **Azure portal**.</span></span>

![Criação de certificado](./media/app-service-web-purchase-ssl-web-site/createssl.png)

<span data-ttu-id="ed3c1-110">Insira um amigável **nome** para o SSL de certificado e insira o **nome de domínio**</span><span class="sxs-lookup"><span data-stu-id="ed3c1-110">Enter a friendly **Name** for your SSL certificate and enter the **Domain Name**</span></span>

> [!NOTE]
> <span data-ttu-id="ed3c1-111">Essa é uma das partes mais importantes do processo de compra.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-111">This is one of the most critical parts of the purchase process.</span></span> <span data-ttu-id="ed3c1-112">Digite corretamente o nome do host (domínio personalizado) que você deseja proteger com esse certificado.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-112">Make sure to enter correct host name (custom domain) that you want to protect with this certificate.</span></span> <span data-ttu-id="ed3c1-113">**NÃO** acrescente WWW ao nome do host.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-113">**DO NOT** append the Host name with WWW.</span></span> 
>

<span data-ttu-id="ed3c1-114">Selecione seu **assinatura**, **grupo de recursos**, e **SKU de certificado**</span><span class="sxs-lookup"><span data-stu-id="ed3c1-114">Select your **Subscription**, **Resource Group**, and **Certificate SKU**</span></span>

> [!WARNING]
> <span data-ttu-id="ed3c1-115">Certificados de serviço de aplicativo só podem ser usados por outros serviços de aplicativo dentro da mesma assinatura.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-115">App Service Certificates can only be used by other App Services within the same subscription.</span></span>  
>

## <a name="step-3---store-the-certificate-in-azure-key-vault"></a><span data-ttu-id="ed3c1-116">Etapa 3: Armazenar o certificado no Cofre da Chave do Azure</span><span class="sxs-lookup"><span data-stu-id="ed3c1-116">Step 3 - Store the certificate in Azure Key Vault</span></span>

> [!NOTE]
> <span data-ttu-id="ed3c1-117">O [Cofre da Chave](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) do Azure ajuda a proteger chaves criptográficas e segredos usados por aplicativos e serviços em nuvem.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-117">[Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) is an Azure service that helps safeguard cryptographic keys and secrets used by cloud applications and services.</span></span>
>

<span data-ttu-id="ed3c1-118">Após a conclusão da compra do Certificado SSL, você precisará abrir a folha Recursos dos [Certificados de Serviço de Aplicativo](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders).</span><span class="sxs-lookup"><span data-stu-id="ed3c1-118">Once the SSL Certificate purchase is complete, you need to open [App Service Certificates](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders) Resource blade.</span></span>

![inserir imagem de pronto para armazenar no KV](./media/app-service-web-purchase-ssl-web-site/ReadyKV.png)

<span data-ttu-id="ed3c1-120">Você perceberá que o status do certificado é **"Emissão Pendente"** , pois há mais algumas etapas que precisam ser concluídas antes de começar a usar esses certificados.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-120">You will notice that Certificate status is **“Pending Issuance”** as there are few more steps you need to complete before you can start using this certificate.</span></span>

<span data-ttu-id="ed3c1-121">Clique em **"Configuração do Certificado"** na folha Propriedades do Certificado e clique em **"Etapa 1: Armazenar"** para armazenar esse certificado no Cofre de Chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-121">Click **Certificate Configuration** inside Certificate Properties blade and Click on **Step 1: Store** to store this certificate in Azure Key Vault.</span></span>

<span data-ttu-id="ed3c1-122">Na folha **"Status do Cofre de Chaves"**, clique em **"Repositório do Cofre de Chaves"** para escolher um Cofre de Chaves existente a fim de armazenar esse certificado **OU "Criar Novo Cofre de Chaves"** para criar um novo Cofre de Chaves no mesmo grupo de recursos e na mesma assinatura.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-122">From **Key Vault Status** Blade, click **Key Vault Repository** to choose an existing Key Vault to store this certificate **OR Create New Key Vault** to create new Key Vault inside same subscription and resource group.</span></span>

> [!NOTE]
> <span data-ttu-id="ed3c1-123">O cofre da chave do Azure tem encargos mínimo para armazenar o certificado.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-123">Azure Key Vault has minimal charges for storing this certificate.</span></span>
> <span data-ttu-id="ed3c1-124">Para obter mais informações, consulte  **[detalhes de preços do Azure Key Vault](https://azure.microsoft.com/pricing/details/key-vault/)**.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-124">For more information, see **[Azure Key Vault Pricing Details](https://azure.microsoft.com/pricing/details/key-vault/)**.</span></span>
>

<span data-ttu-id="ed3c1-125">Depois de selecionar o repositório de Cofre de chave para armazenar esse certificado, o **armazenar** opção tiverem êxito.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-125">Once you have selected the Key Vault Repository to store this certificate in, the **Store** option should show success.</span></span>

![Inserir imagem de sucesso de repositório em KV](./media/app-service-web-purchase-ssl-web-site/KVStoreSuccess.png)

## <a name="step-4---verify-the-domain-ownership"></a><span data-ttu-id="ed3c1-127">Etapa 4: Verificar a propriedade do domínio</span><span class="sxs-lookup"><span data-stu-id="ed3c1-127">Step 4 - Verify the Domain Ownership</span></span>

> [!NOTE]
> <span data-ttu-id="ed3c1-128">Há três tipos de verificação de domínio de certificados de serviço de aplicativo com suporte: verificação do domínio, email, Manual.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-128">There are three types of domain verification supported by App service Certificates: Domain, Mail, Manual Verification.</span></span> <span data-ttu-id="ed3c1-129">Eles são explicados em mais detalhes no [seção avançada](#advanced).</span><span class="sxs-lookup"><span data-stu-id="ed3c1-129">These are explained in more details in the [Advanced section](#advanced).</span></span>

<span data-ttu-id="ed3c1-130">Da mesma **configuração do certificado** folha que você usou na etapa 3, clique em **etapa 2: Verifique se**.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-130">From the same **Certificate Configuration** blade you used in Step 3, click **Step 2: Verify**.</span></span>

<span data-ttu-id="ed3c1-131">**Verificação de domínio** é o processo mais conveniente **somente se** que  **[adquirido seu domínio personalizado do serviço de aplicativo do Azure.](custom-dns-web-site-buydomains-web-app.md)**</span><span class="sxs-lookup"><span data-stu-id="ed3c1-131">**Domain Verification** This is the most convenient process **ONLY IF** you have **[purchased your custom domain from Azure App Service.](custom-dns-web-site-buydomains-web-app.md)**</span></span>
<span data-ttu-id="ed3c1-132">Clique no botão **"Verificar"** para concluir esta etapa.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-132">Click on **Verify** button to complete this step.</span></span>

![Inserir imagem de verificação de domínio](./media/app-service-web-purchase-ssl-web-site/DomainVerificationRequired.png)

<span data-ttu-id="ed3c1-134">Depois de clicar em **Verify**, use o **atualização** botão até que o **Verify** opção deve mostrar o êxito.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-134">After clicking **Verify**, use the **Refresh** button until the **Verify** option should show success.</span></span>

![Inserir imagem de verificar o êxito na KV](./media/app-service-web-purchase-ssl-web-site/KVVerifySuccess.png)

## <a name="step-5---assign-certificate-to-app-service-app"></a><span data-ttu-id="ed3c1-136">Etapa 5: Atribuir o certificado ao Aplicativo do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="ed3c1-136">Step 5 - Assign Certificate to App Service App</span></span>

> [!NOTE]
> <span data-ttu-id="ed3c1-137">Antes de executar as etapas nesta seção, você precisa ter associado um nome de domínio personalizado ao seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-137">Before performing the steps in this section, you must have associated a custom domain name with your app.</span></span> <span data-ttu-id="ed3c1-138">Para saber mais, confira **[Configurando um nome de domínio personalizado para um aplicativo Web.](app-service-web-tutorial-custom-domain.md)**</span><span class="sxs-lookup"><span data-stu-id="ed3c1-138">For more information, see **[Configuring a custom domain name for a web app.](app-service-web-tutorial-custom-domain.md)**</span></span>
>

<span data-ttu-id="ed3c1-139">No  **[portal do Azure](https://portal.azure.com/)**, clique a opção **Serviço de Aplicativo** à esquerda da página.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-139">In the **[Azure portal](https://portal.azure.com/)**, click the **App Service** option on the left of the page.</span></span>

<span data-ttu-id="ed3c1-140">Clique no nome do aplicativo ao qual você deseja atribuir a esse certificado.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-140">Click the name of your app to which you want to assign this certificate.</span></span>

<span data-ttu-id="ed3c1-141">Em **Configurações**, clique em **Certificados SSL**.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-141">In the **Settings**, click **SSL certificates**.</span></span>

<span data-ttu-id="ed3c1-142">Clique em **Importar Certificado do Serviço de Aplicativo** e selecione o certificado que você acabou de adquirir.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-142">Click **Import App Service Certificate** and select the certificate that you just purchased.</span></span>

![inserir imagem de Importar Certificado](./media/app-service-web-purchase-ssl-web-site/ImportCertificate.png)

<span data-ttu-id="ed3c1-144">No **associações ssl** seção clique **adicionar associações**e use os menus suspensos para selecionar o nome de domínio a ser protegido com SSL e o certificado a usar.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-144">In the **ssl bindings** section Click on **Add bindings**, and use the dropdowns to select the domain name to secure with SSL, and the certificate to use.</span></span> <span data-ttu-id="ed3c1-145">Você também pode selecionar se deseja usar **[SNI (Indicação de Nome de Servidor)](http://en.wikipedia.org/wiki/Server_Name_Indication)** ou SSL baseado em IP.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-145">You may also select whether to use **[Server Name Indication (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)** or IP based SSL.</span></span>

![inserir imagem de Associações SSL](./media/app-service-web-purchase-ssl-web-site/SSLBindings.png)

<span data-ttu-id="ed3c1-147">Clique em **Adicionar Associação** para salvar as alterações e habilitar o SSL.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-147">Click **Add Binding** to save the changes and enable SSL.</span></span>

> [!NOTE]
> <span data-ttu-id="ed3c1-148">Se você selecionou **SSL com base em IP** e seu domínio personalizado foi configurado pelo uso de um registro A, você deverá executar as seguintes etapas adicionais.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-148">If you selected **IP based SSL** and your custom domain is configured using an A record, you must perform the following additional steps.</span></span> <span data-ttu-id="ed3c1-149">Eles são explicados em mais detalhes no [seção avançada](#Advanced).</span><span class="sxs-lookup"><span data-stu-id="ed3c1-149">These are explained in more details in the [Advanced section](#Advanced).</span></span>

<span data-ttu-id="ed3c1-150">Neste ponto, você poderá visitar o seu aplicativo usando `HTTPS://` em vez de `HTTP://` para verificar se o certificado foi configurado corretamente.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-150">At this point, you should be able to visit your app using `HTTPS://` instead of `HTTP://` to verify that the certificate has been configured correctly.</span></span>

<!--![insert image of https](./media/app-service-web-purchase-ssl-web-site/Https.png)-->

## <a name="step-6---management-tasks"></a><span data-ttu-id="ed3c1-151">Etapa 6 – Tarefas de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="ed3c1-151">Step 6 - Management tasks</span></span>

### <a name="azure-cli"></a><span data-ttu-id="ed3c1-152">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="ed3c1-152">Azure CLI</span></span>

<span data-ttu-id="ed3c1-153">[!code-azurecli[principal](../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Associar um certificado SSL personalizado a um aplicativo Web")]</span><span class="sxs-lookup"><span data-stu-id="ed3c1-153">[!code-azurecli[main](../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")]</span></span> 

### <a name="powershell"></a><span data-ttu-id="ed3c1-154">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ed3c1-154">PowerShell</span></span>

<span data-ttu-id="ed3c1-155">[!code-powershell[principal](../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Associar um certificado SSL personalizado a um aplicativo Web")]</span><span class="sxs-lookup"><span data-stu-id="ed3c1-155">[!code-powershell[main](../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate to a web app")]</span></span>

## <a name="advanced"></a><span data-ttu-id="ed3c1-156">Avançado</span><span class="sxs-lookup"><span data-stu-id="ed3c1-156">Advanced</span></span>

### <a name="verifying-domain-ownership"></a><span data-ttu-id="ed3c1-157">Verificando a propriedade de domínio</span><span class="sxs-lookup"><span data-stu-id="ed3c1-157">Verifying Domain Ownership</span></span>

<span data-ttu-id="ed3c1-158">Há dois outros tipos de suporte para certificados de serviço do aplicativo de verificação de domínio: Mail e Verificação Manual.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-158">There are two more types of domain verification supported by App service Certificates: Mail, and Manual Verification.</span></span>

#### <a name="mail-verification"></a><span data-ttu-id="ed3c1-159">Verificação por email</span><span class="sxs-lookup"><span data-stu-id="ed3c1-159">Mail Verification</span></span>

<span data-ttu-id="ed3c1-160">Um email de verificação já foi enviado para os endereços de email associados a esse domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-160">Verification email has already been sent to the Email Address(es) associated with this custom domain.</span></span>
<span data-ttu-id="ed3c1-161">Para concluir a etapa de verificação por email, abra o email e clique no link de verificação.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-161">To complete the Email verification step, open the email and click the verification link.</span></span>

![Inserir imagem de verificação de email](./media/app-service-web-purchase-ssl-web-site/KVVerifyEmailSuccess.png)

<span data-ttu-id="ed3c1-163">Se você precisar reenviar o email de verificação, clique no botão **Reenviar Email**.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-163">If you need to resend the verification email, click the **Resend Email** button.</span></span>

#### <a name="manual-verification"></a><span data-ttu-id="ed3c1-164">Verificação manual</span><span class="sxs-lookup"><span data-stu-id="ed3c1-164">Manual Verification</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ed3c1-165">Verificação da página da Web em HTML (funciona somente com SKU de Certificado Padrão)</span><span class="sxs-lookup"><span data-stu-id="ed3c1-165">HTML Web Page Verification (only works with Standard Certificate SKU)</span></span>
>

1. <span data-ttu-id="ed3c1-166">Crie um arquivo HTML chamado **"starfield.html"**</span><span class="sxs-lookup"><span data-stu-id="ed3c1-166">Create an HTML file named **"starfield.html"**</span></span>

1. <span data-ttu-id="ed3c1-167">O conteúdo desse arquivo deve ser o nome exato do Token de verificação de domínio.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-167">Content of this file should be the exact name of the Domain Verification Token.</span></span> <span data-ttu-id="ed3c1-168">(Você pode copiar o token na folha Status de Verificação de Domínio)</span><span class="sxs-lookup"><span data-stu-id="ed3c1-168">(You can copy the token from the Domain Verification Status Blade)</span></span>

1. <span data-ttu-id="ed3c1-169">Carregue esse arquivo na raiz do servidor Web que hospeda seu domínio`/.well-known/pki-validation/starfield.html`</span><span class="sxs-lookup"><span data-stu-id="ed3c1-169">Upload this file at the root of the web server hosting your domain `/.well-known/pki-validation/starfield.html`</span></span>

1. <span data-ttu-id="ed3c1-170">Clique em **"Atualizar"** para atualizar o Status do certificado após a verificação.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-170">Click **Refresh** to update the certificate status after verification is completed.</span></span> <span data-ttu-id="ed3c1-171">Pode demorar alguns minutos até a verificação ser concluída.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-171">It might take few minutes for verification to complete.</span></span>

> [!TIP]
> <span data-ttu-id="ed3c1-172">Verifique se um terminal usando `curl -G http://<domain>/.well-known/pki-validation/starfield.html` a resposta deve conter o `<verification-token>`.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-172">Verify in a terminal using `curl -G http://<domain>/.well-known/pki-validation/starfield.html` the response should contain the `<verification-token>`.</span></span>

#### <a name="dns-txt-record-verification"></a><span data-ttu-id="ed3c1-173">Verificação de registro TXT do DNS</span><span class="sxs-lookup"><span data-stu-id="ed3c1-173">DNS TXT Record Verification</span></span>

1. <span data-ttu-id="ed3c1-174">Usando o gerenciador de DNS, crie um registro TXT no subdomínio `@` com um valor igual ao Token de Verificação de Domínio.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-174">Using your DNS manager, Create a TXT record on the `@` subdomain with value equal to the Domain Verification Token.</span></span>
1. <span data-ttu-id="ed3c1-175">Clique em **"Atualizar"** para atualizar o Status do certificado após a verificação.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-175">Click **“Refresh”** to update the Certificate status after verification is completed.</span></span>

> [!TIP]
> <span data-ttu-id="ed3c1-176">Você precisa criar um registro TXT em `@.<domain>` com o valor `<verification-token>`.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-176">You need to create a TXT record on `@.<domain>` with value `<verification-token>`.</span></span>

### <a name="assign-certificate-to-app-service-app"></a><span data-ttu-id="ed3c1-177">Atribuir o certificado ao Aplicativo do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="ed3c1-177">Assign Certificate to App Service App</span></span>

<span data-ttu-id="ed3c1-178">Se você selecionou **SSL baseado em IP** e seu domínio personalizado foi configurado pelo uso de um registro A, você deverá executar as seguintes etapas adicionais:</span><span class="sxs-lookup"><span data-stu-id="ed3c1-178">If you selected **IP based SSL** and your custom domain is configured using an A record, you must perform the following additional steps:</span></span>

<span data-ttu-id="ed3c1-179">Depois de ter configurado uma associação de SSL baseada em IP, um endereço IP dedicado é atribuído ao seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-179">After you have configured an IP based SSL binding, a dedicated IP address is assigned to your app.</span></span> <span data-ttu-id="ed3c1-180">Encontre esse endereço IP na página **Domínio personalizado** nas configurações do aplicativo, logo acima da seção **Nomes de host**.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-180">You can find this IP address on the **Custom domain** page under settings of your app, right above the **Hostnames** section.</span></span> <span data-ttu-id="ed3c1-181">Ele é listado como **endereço IP externo**</span><span class="sxs-lookup"><span data-stu-id="ed3c1-181">It is listed as **External IP Address**</span></span>

![inserir imagem de IP SSL](./media/app-service-web-purchase-ssl-web-site/virtual-ip-address.png)

<span data-ttu-id="ed3c1-183">Observe que esse endereço IP será diferente do endereço IP virtual usado anteriormente para configurar o registro A de seu domínio.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-183">Note that this IP address is different than the virtual IP address used previously to configure the A record for your domain.</span></span> <span data-ttu-id="ed3c1-184">Se você estiver configurado para usar SSL baseado em SNI ou não estão configurados para usar SSL, nenhum endereço será listado para essa entrada.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-184">If you are configured to use SNI based SSL, or are not configured to use SSL, no address is listed for this entry.</span></span>

<span data-ttu-id="ed3c1-185">Usando as ferramentas fornecidas pelo registro de nomes de domínio, modifique o registro A de seu nome de domínio personalizado para redirecionar para o endereço IP da etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-185">Using the tools provided by your domain name registrar, modify the A record for your custom domain name to point to the IP address from the previous step.</span></span>

## <a name="rekey-and-sync-the-certificate"></a><span data-ttu-id="ed3c1-186">Criar novas chaves e sincronizar o certificado</span><span class="sxs-lookup"><span data-stu-id="ed3c1-186">Rekey and Sync the Certificate</span></span>

<span data-ttu-id="ed3c1-187">Se você precisar rechaveamento seu certificado, selecione **rechaveamento e sincronizar** opção **propriedades do certificado** folha.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-187">If you ever need to Rekey your certificate, select **Rekey and Sync** option from **Certificate Properties** Blade.</span></span>

<span data-ttu-id="ed3c1-188">Clique no botão **"Criar Nova Chave"** para iniciar o processo.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-188">Click **Rekey** Button to initiate the process.</span></span> <span data-ttu-id="ed3c1-189">Esse processo pode demorar de um a 10 minutos para ser concluído.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-189">This process can take 1-10 minutes to complete.</span></span>

![inserir imagem de Nova Chave SSL](./media/app-service-web-purchase-ssl-web-site/Rekey.png)

<span data-ttu-id="ed3c1-191">A criação de uma nova chave para o certificado causará a emissão de um novo certificado pela autoridade de certificação.</span><span class="sxs-lookup"><span data-stu-id="ed3c1-191">Rekeying your certificate rolls the certificate with a new certificate issued from the certificate authority.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ed3c1-192">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ed3c1-192">Next Steps</span></span>

* [<span data-ttu-id="ed3c1-193">Adicionar uma rede de fornecimento de conteúdo</span><span class="sxs-lookup"><span data-stu-id="ed3c1-193">Add a Content Delivery Network</span></span>](app-service-web-tutorial-content-delivery-network.md)