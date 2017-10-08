---
title: "aaaConfigure SSL para um serviço de nuvem | Microsoft Docs"
description: "Saiba como toospecify um ponto de extremidade HTTPS para uma função web e como tooupload um SSL certificado toosecure seu aplicativo. Esses exemplos usam Olá portal do Azure."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 371ba204-48b6-41af-ab9f-ed1d64efe704
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: adegeo
ms.openlocfilehash: b19283bb7b0e95374f2ae9c3532eb1effc7d6a9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-ssl-for-an-application-in-azure"></a><span data-ttu-id="69726-104">Configurando SSL para um aplicativo no Azure</span><span class="sxs-lookup"><span data-stu-id="69726-104">Configuring SSL for an application in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="69726-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="69726-105">Azure portal</span></span>](cloud-services-configure-ssl-certificate-portal.md)
> * [<span data-ttu-id="69726-106">Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="69726-106">Azure classic portal</span></span>](cloud-services-configure-ssl-certificate.md)
>

<span data-ttu-id="69726-107">Criptografia do Secure Socket Layer (SSL) é o método de hello mais comumente usada de proteção de dados enviados pela Olá internet.</span><span class="sxs-lookup"><span data-stu-id="69726-107">Secure Socket Layer (SSL) encryption is hello most commonly used method of securing data sent across hello internet.</span></span> <span data-ttu-id="69726-108">Essa tarefa comum discute como toospecify um ponto de extremidade HTTPS para uma função web e como tooupload um SSL certificado toosecure seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="69726-108">This common task discusses how toospecify an HTTPS endpoint for a web role and how tooupload an SSL certificate toosecure your application.</span></span>

> [!NOTE]
> <span data-ttu-id="69726-109">procedimentos de saudação nesta tarefa se aplicam a serviços de nuvem tooAzure; para serviços de aplicativos, consulte [isso](../app-service-web/web-sites-configure-ssl-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="69726-109">hello procedures in this task apply tooAzure Cloud Services; for App Services, see [this](../app-service-web/web-sites-configure-ssl-certificate.md).</span></span>
>

<span data-ttu-id="69726-110">Essa tarefa usa uma implantação de produção.</span><span class="sxs-lookup"><span data-stu-id="69726-110">This task uses a production deployment.</span></span> <span data-ttu-id="69726-111">Informações sobre o uso de uma implantação de preparo são fornecidas no final deste tópico hello.</span><span class="sxs-lookup"><span data-stu-id="69726-111">Information on using a staging deployment is provided at hello end of this topic.</span></span>

<span data-ttu-id="69726-112">Leia [isto](cloud-services-how-to-create-deploy-portal.md) primeiro se você ainda não tiver criado um serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="69726-112">Read [this](cloud-services-how-to-create-deploy-portal.md) first if you have not yet created a cloud service.</span></span>

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a><span data-ttu-id="69726-113">Etapa 1: Obter um certificado SSL</span><span class="sxs-lookup"><span data-stu-id="69726-113">Step 1: Get an SSL certificate</span></span>
<span data-ttu-id="69726-114">tooconfigure SSL para um aplicativo, você primeiro precisa tooget um certificado SSL assinado por uma autoridade de certificação (CA), um terceiro confiável que emite certificados para essa finalidade.</span><span class="sxs-lookup"><span data-stu-id="69726-114">tooconfigure SSL for an application, you first need tooget an SSL certificate that has been signed by a Certificate Authority (CA), a trusted third party who issues certificates for this purpose.</span></span> <span data-ttu-id="69726-115">Se você ainda não tiver um, será necessário tooobtain uma empresa que vende certificados SSL.</span><span class="sxs-lookup"><span data-stu-id="69726-115">If you do not already have one, you need tooobtain one from a company that sells SSL certificates.</span></span>

<span data-ttu-id="69726-116">certificado de saudação deve atender aos Olá seguindo os requisitos para certificados SSL no Azure:</span><span class="sxs-lookup"><span data-stu-id="69726-116">hello certificate must meet hello following requirements for SSL certificates in Azure:</span></span>

* <span data-ttu-id="69726-117">certificado de saudação deve conter uma chave privada.</span><span class="sxs-lookup"><span data-stu-id="69726-117">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="69726-118">certificado de saudação deve ser criado para troca de chaves, exportável tooa arquivo de troca de informações pessoais (. pfx).</span><span class="sxs-lookup"><span data-stu-id="69726-118">hello certificate must be created for key exchange, exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="69726-119">Hello nome da entidade do certificado deve corresponder o serviço de nuvem do hello domínio usado tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="69726-119">hello certificate's subject name must match hello domain used tooaccess hello cloud service.</span></span> <span data-ttu-id="69726-120">Você não pode obter um certificado SSL de uma autoridade de certificação (CA) para o domínio do hello cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="69726-120">You cannot obtain an SSL certificate from a certificate authority (CA) for hello cloudapp.net domain.</span></span> <span data-ttu-id="69726-121">Você deve adquirir um toouse de nome de domínio personalizado ao seu serviço de acesso.</span><span class="sxs-lookup"><span data-stu-id="69726-121">You must acquire a custom domain name toouse when access your service.</span></span> <span data-ttu-id="69726-122">Quando você solicitar um certificado de uma autoridade de certificação, nome da entidade do certificado Olá deve corresponder Olá domínio personalizado nome usado tooaccess seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="69726-122">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name used tooaccess your application.</span></span> <span data-ttu-id="69726-123">Por exemplo, se o nome de domínio personalizado for **contoso.com**, você pode solicitar um certificado da autoridade de certificação para ***.contoso.com** ou **www.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="69726-123">For example, if your custom domain name is **contoso.com** you would request a certificate from your CA for ***.contoso.com** or **www.contoso.com**.</span></span>
* <span data-ttu-id="69726-124">certificado Olá deve usar um mínimo de criptografia de 2048 bits.</span><span class="sxs-lookup"><span data-stu-id="69726-124">hello certificate must use a minimum of 2048-bit encryption.</span></span>

<span data-ttu-id="69726-125">Para fins de teste, você pode [criar](cloud-services-certs-create.md) e usar um certificado autoassinado.</span><span class="sxs-lookup"><span data-stu-id="69726-125">For test purposes, you can [create](cloud-services-certs-create.md) and use a self-signed certificate.</span></span> <span data-ttu-id="69726-126">Um certificado autoassinado não é autenticado por meio de uma autoridade de certificação e pode usar o domínio cloudapp.net de saudação como Olá URL do site.</span><span class="sxs-lookup"><span data-stu-id="69726-126">A self-signed certificate is not authenticated through a CA and can use hello cloudapp.net domain as hello website URL.</span></span> <span data-ttu-id="69726-127">Por exemplo, hello tarefa a seguir usa um certificado autoassinado no qual Olá nome comum (CN) utilizado no certificado de saudação é **sslexample.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="69726-127">For example, hello following task uses a self-signed certificate in which hello common name (CN) used in hello certificate is **sslexample.cloudapp.net**.</span></span>

<span data-ttu-id="69726-128">Em seguida, você deve incluir informações sobre o certificado de saudação em sua definição de serviço e arquivos de configuração de serviço.</span><span class="sxs-lookup"><span data-stu-id="69726-128">Next, you must include information about hello certificate in your service definition and service configuration files.</span></span>

<span data-ttu-id="69726-129"><a name="modify"> </a></span><span class="sxs-lookup"><span data-stu-id="69726-129"><a name="modify"> </a></span></span>

## <a name="step-2-modify-hello-service-definition-and-configuration-files"></a><span data-ttu-id="69726-130">Etapa 2: Modificar arquivos de definição e configuração de serviço Olá</span><span class="sxs-lookup"><span data-stu-id="69726-130">Step 2: Modify hello service definition and configuration files</span></span>
<span data-ttu-id="69726-131">Seu aplicativo deve ser o certificado de saudação toouse configurado e um ponto de extremidade HTTPS deve ser adicionado.</span><span class="sxs-lookup"><span data-stu-id="69726-131">Your application must be configured toouse hello certificate, and an HTTPS endpoint must be added.</span></span> <span data-ttu-id="69726-132">Como resultado, hello definição de serviço e arquivos de configuração de serviço necessário toobe atualizado.</span><span class="sxs-lookup"><span data-stu-id="69726-132">As a result, hello service definition and service configuration files need toobe updated.</span></span>

1. <span data-ttu-id="69726-133">Em seu ambiente de desenvolvimento, abra o arquivo de definição de serviço (CSDEF) hello, adicione um **certificados** seção dentro de saudação **WebRole** seção e incluir Olá informações a seguir o certificado (e certificados intermediários):</span><span class="sxs-lookup"><span data-stu-id="69726-133">In your development environment, open hello service definition file (CSDEF), add a **Certificates** section within hello **WebRole** section, and include hello following information about the certificate (and intermediate certificates):</span></span>

   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Certificates>
            <Certificate name="SampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="My"
                        permissionLevel="limitedOrElevated" />
            <!-- IMPORTANT! Unless your certificate is either
            self-signed or signed directly by hello CA root, you
            must include all hello intermediate certificates
            here. You must list them here, even if they are
            not bound tooany endpoints. Failing toolist any of
            hello intermediate certificates may cause hard-to-reproduce
            interoperability problems on some clients.-->
            <Certificate name="CAForSampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="CA"
                        permissionLevel="limitedOrElevated" />
        </Certificates>
    ...
    </WebRole>
    ```

   <span data-ttu-id="69726-134">Olá **certificados** seção define o nome de saudação do nosso certificado, seu local e o nome de saudação do repositório Olá onde ele está localizado.</span><span class="sxs-lookup"><span data-stu-id="69726-134">hello **Certificates** section defines hello name of our certificate, its location, and hello name of hello store where it is located.</span></span>

   <span data-ttu-id="69726-135">Permissões (`permisionLevel` atributo) pode ser tooone de conjunto de saudação seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="69726-135">Permissions (`permisionLevel` attribute) can be set tooone of hello following values:</span></span>

   | <span data-ttu-id="69726-136">Valor da permissão</span><span class="sxs-lookup"><span data-stu-id="69726-136">Permission Value</span></span> | <span data-ttu-id="69726-137">Descrição</span><span class="sxs-lookup"><span data-stu-id="69726-137">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="69726-138">limitedOrElevated</span><span class="sxs-lookup"><span data-stu-id="69726-138">limitedOrElevated</span></span> |<span data-ttu-id="69726-139">**(Padrão)**  Todos os processos de função podem acessar a chave privada hello.</span><span class="sxs-lookup"><span data-stu-id="69726-139">**(Default)** All role processes can access hello private key.</span></span> |
   | <span data-ttu-id="69726-140">elevado</span><span class="sxs-lookup"><span data-stu-id="69726-140">elevated</span></span> |<span data-ttu-id="69726-141">Somente os processos elevados podem acessar a chave privada hello.</span><span class="sxs-lookup"><span data-stu-id="69726-141">Only elevated processes can access hello private key.</span></span> |

2. <span data-ttu-id="69726-142">Em seu arquivo de definição de serviço, adicionar um **InputEndpoint** elemento dentro do hello **pontos de extremidade** seção tooenable HTTPS:</span><span class="sxs-lookup"><span data-stu-id="69726-142">In your service definition file, add an **InputEndpoint** element within hello **Endpoints** section tooenable HTTPS:</span></span>

   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Endpoints>
            <InputEndpoint name="HttpsIn" protocol="https" port="443"
                certificate="SampleCertificate" />
        </Endpoints>
    ...
    </WebRole>
    ```

3. <span data-ttu-id="69726-143">Em seu arquivo de definição de serviço, adicionar um **associação** elemento dentro do hello **Sites** seção.</span><span class="sxs-lookup"><span data-stu-id="69726-143">In your service definition file, add a **Binding** element within hello **Sites** section.</span></span> <span data-ttu-id="69726-144">Esse elemento adiciona uma associação de HTTPS toomap o site do ponto de extremidade tooyour:</span><span class="sxs-lookup"><span data-stu-id="69726-144">This element adds an HTTPS binding toomap the endpoint tooyour site:</span></span>

   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Sites>
            <Site name="Web">
                <Bindings>
                    <Binding name="HttpsIn" endpointName="HttpsIn" />
                </Bindings>
            </Site>
        </Sites>
    ...
    </WebRole>
    ```

   <span data-ttu-id="69726-145">Arquivo de definição de todos os Olá alterações necessárias toohello serviço foram concluídas; Porém, você continua precisando tooadd Olá certificado informações ao arquivo de configuração do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="69726-145">All hello required changes toohello service definition file have been completed; but, you still need tooadd hello certificate information to hello service configuration file.</span></span>
4. <span data-ttu-id="69726-146">Em seu arquivo de configuração de serviço (CSCFG), ServiceConfiguration.Cloud.cscfg, adicione um valor de **Certificados** com o do seu certificado.</span><span class="sxs-lookup"><span data-stu-id="69726-146">In your service configuration file (CSCFG), ServiceConfiguration.Cloud.cscfg, add a **Certificates** value with that of your certificate.</span></span> <span data-ttu-id="69726-147">Olá, exemplo de código a seguir fornece detalhes de saudação **certificados** seção, exceto pelo valor de impressão digital de saudação.</span><span class="sxs-lookup"><span data-stu-id="69726-147">hello following code sample provides details of hello **Certificates** section, except for hello thumbprint value.</span></span>

   ```xml
    <Role name="Deployment">
    ...
        <Certificates>
            <Certificate name="SampleCertificate"
                thumbprint="9427befa18ec6865a9ebdc79d4c38de50e6316ff"
                thumbprintAlgorithm="sha1" />
            <Certificate name="CAForSampleCertificate"
                thumbprint="79d4c38de50e6316ff9427befa18ec6865a9ebdc"
                thumbprintAlgorithm="sha1" />
        </Certificates>
    ...
    </Role>
    ```

<span data-ttu-id="69726-148">(Este exemplo usa **sha1** para algoritmo de impressão digital de saudação.</span><span class="sxs-lookup"><span data-stu-id="69726-148">(This example uses **sha1** for hello thumbprint algorithm.</span></span> <span data-ttu-id="69726-149">Especificar valor de saudação apropriado para o algoritmo de impressão digital do certificado).</span><span class="sxs-lookup"><span data-stu-id="69726-149">Specify hello appropriate value for your certificate's thumbprint algorithm.)</span></span>

<span data-ttu-id="69726-150">Agora que os arquivos de configuração Olá serviço definição e o serviço foi atualizados, sua implantação para carregar tooAzure do pacote.</span><span class="sxs-lookup"><span data-stu-id="69726-150">Now that hello service definition and service configuration files have been updated, package your deployment for uploading tooAzure.</span></span> <span data-ttu-id="69726-151">Se você está usando **cspack**, não use o sinalizador **/generateConfigurationFile**, pois ele substituirá as informações de certificado que você acabou de inserir.</span><span class="sxs-lookup"><span data-stu-id="69726-151">If you are using **cspack**, don't use the **/generateConfigurationFile** flag, as that will overwrite the certificate information you just inserted.</span></span>

## <a name="step-3-upload-a-certificate"></a><span data-ttu-id="69726-152">Etapa 3: Carregar um certificado</span><span class="sxs-lookup"><span data-stu-id="69726-152">Step 3: Upload a certificate</span></span>
<span data-ttu-id="69726-153">Conecte-se toohello portal do Azure e...</span><span class="sxs-lookup"><span data-stu-id="69726-153">Connect toohello Azure portal and...</span></span>

1. <span data-ttu-id="69726-154">Em Olá **todos os recursos** seção Olá Portal, selecione seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="69726-154">In hello **All resources** section of hello Portal, select your cloud service.</span></span>

    ![Publicar o serviço de nuvem](media/cloud-services-configure-ssl-certificate-portal/browse.png)

2. <span data-ttu-id="69726-156">Clique em **Certificados**.</span><span class="sxs-lookup"><span data-stu-id="69726-156">Click **Certificates**.</span></span>

    ![Clique Olá certificados ícone](media/cloud-services-configure-ssl-certificate-portal/certificate-item.png)

3. <span data-ttu-id="69726-158">Clique em **carregar** na parte superior de saudação da área de certificados de saudação.</span><span class="sxs-lookup"><span data-stu-id="69726-158">Click **Upload** at hello top of hello certificates area.</span></span>

    ![Clique em item de menu de carregamento de saudação](media/cloud-services-configure-ssl-certificate-portal/Upload_menu.png)

4. <span data-ttu-id="69726-160">Fornecer Olá **arquivo**, **senha**, em seguida, clique em **carregar** na parte inferior de Olá Olá entrada da área de dados.</span><span class="sxs-lookup"><span data-stu-id="69726-160">Provide hello **File**, **Password**, then click **Upload** at hello bottom of hello data entry area.</span></span>

## <a name="step-4-connect-toohello-role-instance-by-using-https"></a><span data-ttu-id="69726-161">Etapa 4: Conectar a instância de função toohello usando HTTPS</span><span class="sxs-lookup"><span data-stu-id="69726-161">Step 4: Connect toohello role instance by using HTTPS</span></span>
<span data-ttu-id="69726-162">Agora que sua implantação estiver em execução no Azure, você pode conectar tooit usando HTTPS.</span><span class="sxs-lookup"><span data-stu-id="69726-162">Now that your deployment is up and running in Azure, you can connect tooit using HTTPS.</span></span>

1. <span data-ttu-id="69726-163">Clique em Olá **URL do Site** tooopen navegador da web hello.</span><span class="sxs-lookup"><span data-stu-id="69726-163">Click hello **Site URL** tooopen up hello web browser.</span></span>

   ![Clique em Olá URL do Site](media/cloud-services-configure-ssl-certificate-portal/navigate.png)

2. <span data-ttu-id="69726-165">No navegador da web, modifique Olá link toouse **https** em vez de **http**e, em seguida, visite a página de saudação.</span><span class="sxs-lookup"><span data-stu-id="69726-165">In your web browser, modify hello link toouse **https** instead of **http**, and then visit hello page.</span></span>

   > [!NOTE]
   > <span data-ttu-id="69726-166">Se você estiver usando um certificado autoassinado, quando você procurar o ponto de extremidade HTTPS de tooan associada com um certificado autoassinado hello, que você verá um erro de certificado no navegador de saudação.</span><span class="sxs-lookup"><span data-stu-id="69726-166">If you are using a self-signed certificate, when you browse tooan HTTPS endpoint that's associated with hello self-signed certificate you may see a certificate error in hello browser.</span></span> <span data-ttu-id="69726-167">Usando um certificado assinado por uma autoridade de certificação confiável elimina esse problema; em Olá enquanto isso, você pode ignorar o erro de saudação.</span><span class="sxs-lookup"><span data-stu-id="69726-167">Using a certificate signed by a trusted certification authority eliminates this problem; in hello meantime, you can ignore hello error.</span></span> <span data-ttu-id="69726-168">(Outra opção é o repositório de certificados do usuário do toohello certificado autoassinado Olá tooadd certificado confiável autoridade.)</span><span class="sxs-lookup"><span data-stu-id="69726-168">(Another option is tooadd hello self-signed certificate toohello user's trusted certificate authority certificate store.)</span></span>
   >
   >

   ![Visualização de site](media/cloud-services-configure-ssl-certificate-portal/show-site.png)

   > [!TIP]
   > <span data-ttu-id="69726-170">Se você quiser toouse SSL para uma implantação de preparo, em vez de uma implantação de produção, você precisará primeiro toodetermine Olá URL usada para implantação de preparo de saudação.</span><span class="sxs-lookup"><span data-stu-id="69726-170">If you want toouse SSL for a staging deployment instead of a production deployment, you'll first need toodetermine hello URL used for hello staging deployment.</span></span> <span data-ttu-id="69726-171">Quando o serviço de nuvem tiver sido implantado, Olá URL toohello ambiente de preparo é determinado pelo Olá **ID de implantação** GUID neste formato:`https://deployment-id.cloudapp.net/`</span><span class="sxs-lookup"><span data-stu-id="69726-171">Once your cloud service has been deployed, hello URL toohello staging environment is determined by hello **Deployment ID** GUID in this format: `https://deployment-id.cloudapp.net/`</span></span>  
   >
   > <span data-ttu-id="69726-172">Criar um certificado com hello comuns CN (nome) toohello igual com base em GUID URL (por exemplo, **328187776e774ceda8fc57609d404462.cloudapp.net**).</span><span class="sxs-lookup"><span data-stu-id="69726-172">Create a certificate with hello common name (CN) equal toohello GUID-based URL (for example, **328187776e774ceda8fc57609d404462.cloudapp.net**).</span></span> <span data-ttu-id="69726-173">Use Olá tooadd portal Olá certificado tooyour testados serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="69726-173">Use hello portal tooadd hello certificate tooyour staged cloud service.</span></span> <span data-ttu-id="69726-174">Em seguida, adicione Olá certificado informações tooyour CSDEF arquivos e CSCFG, reempacotar seu aplicativo e atualizar sua implantação de preparo toouse Olá novo pacote de.</span><span class="sxs-lookup"><span data-stu-id="69726-174">Then, add hello certificate information tooyour CSDEF and CSCFG files, repackage your application, and update your staged deployment toouse hello new package.</span></span>
   >

## <a name="next-steps"></a><span data-ttu-id="69726-175">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="69726-175">Next steps</span></span>
* <span data-ttu-id="69726-176">[Configuração geral do serviço de nuvem](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="69726-176">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="69726-177">Saiba como muito[implantar um serviço de nuvem](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="69726-177">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="69726-178">Configurar um [nome de domínio personalizado](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="69726-178">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="69726-179">[Gerenciar seu serviço de nuvem](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="69726-179">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
