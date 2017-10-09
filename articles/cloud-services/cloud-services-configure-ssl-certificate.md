---
title: "aaaConfigure SSL para um serviço de nuvem (clássicos) | Microsoft Docs"
description: "Saiba como toospecify um ponto de extremidade HTTPS para uma função web e como tooupload um SSL certificado toosecure seu aplicativo."
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 4cbb7f38-7994-454d-b4f0-7259b558c766
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/14/2016
ms.author: adegeo
ms.openlocfilehash: a1ca031b98af49d371977a208ed24f6dc8ea2ac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-ssl-for-an-application-in-azure"></a><span data-ttu-id="99791-103">Configurando SSL para um aplicativo no Azure</span><span class="sxs-lookup"><span data-stu-id="99791-103">Configuring SSL for an application in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="99791-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="99791-104">Azure portal</span></span>](cloud-services-configure-ssl-certificate-portal.md)
> * [<span data-ttu-id="99791-105">Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="99791-105">Azure classic portal</span></span>](cloud-services-configure-ssl-certificate.md)
> 
> 

<span data-ttu-id="99791-106">Criptografia do Secure Socket Layer (SSL) é o método de hello mais comumente usada de proteção de dados enviados pela Olá internet.</span><span class="sxs-lookup"><span data-stu-id="99791-106">Secure Socket Layer (SSL) encryption is hello most commonly used method of securing data sent across hello internet.</span></span> <span data-ttu-id="99791-107">Essa tarefa comum discute como toospecify um ponto de extremidade HTTPS para uma função web e como tooupload um SSL certificado toosecure seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="99791-107">This common task discusses how toospecify an HTTPS endpoint for a web role and how tooupload an SSL certificate toosecure your application.</span></span>

> [!NOTE]
> <span data-ttu-id="99791-108">procedimentos de saudação nesta tarefa se aplicam a serviços de nuvem tooAzure; para serviços de aplicativos, consulte [isso](../app-service-web/web-sites-configure-ssl-certificate.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="99791-108">hello procedures in this task apply tooAzure Cloud Services; for App Services, see [this](../app-service-web/web-sites-configure-ssl-certificate.md) article.</span></span>
> 
> 

<span data-ttu-id="99791-109">Essa tarefa usa uma implantação de produção.</span><span class="sxs-lookup"><span data-stu-id="99791-109">This task uses a production deployment.</span></span> <span data-ttu-id="99791-110">Informações sobre o uso de uma implantação de preparo são fornecidas no final deste tópico hello.</span><span class="sxs-lookup"><span data-stu-id="99791-110">Information on using a staging deployment is provided at hello end of this topic.</span></span>

<span data-ttu-id="99791-111">Leia [este](cloud-services-how-to-create-deploy.md) artigo primeiro se você ainda não tiver criado um serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="99791-111">Read [this](cloud-services-how-to-create-deploy.md) article first if you have not yet created a cloud service.</span></span>

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a><span data-ttu-id="99791-112">Etapa 1: Obter um certificado SSL</span><span class="sxs-lookup"><span data-stu-id="99791-112">Step 1: Get an SSL certificate</span></span>
<span data-ttu-id="99791-113">tooconfigure SSL para um aplicativo, você primeiro precisa tooget um certificado SSL assinado por uma autoridade de certificação (CA), um terceiro confiável que emite certificados para essa finalidade.</span><span class="sxs-lookup"><span data-stu-id="99791-113">tooconfigure SSL for an application, you first need tooget an SSL certificate that has been signed by a Certificate Authority (CA), a trusted third party who issues certificates for this purpose.</span></span> <span data-ttu-id="99791-114">Se você ainda não tiver um, será necessário tooobtain uma empresa que vende certificados SSL.</span><span class="sxs-lookup"><span data-stu-id="99791-114">If you do not already have one, you need tooobtain one from a company that sells SSL certificates.</span></span>

<span data-ttu-id="99791-115">certificado de saudação deve atender aos Olá seguindo os requisitos para certificados SSL no Azure:</span><span class="sxs-lookup"><span data-stu-id="99791-115">hello certificate must meet hello following requirements for SSL certificates in Azure:</span></span>

* <span data-ttu-id="99791-116">certificado de saudação deve conter uma chave privada.</span><span class="sxs-lookup"><span data-stu-id="99791-116">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="99791-117">certificado de saudação deve ser criado para troca de chaves, exportável tooa arquivo de troca de informações pessoais (. pfx).</span><span class="sxs-lookup"><span data-stu-id="99791-117">hello certificate must be created for key exchange, exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="99791-118">Hello nome da entidade do certificado deve corresponder o serviço de nuvem do hello domínio usado tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="99791-118">hello certificate's subject name must match hello domain used tooaccess hello cloud service.</span></span> <span data-ttu-id="99791-119">Você não pode obter um certificado SSL de uma autoridade de certificação (CA) para o domínio do hello cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="99791-119">You cannot obtain an SSL certificate from a certificate authority (CA) for hello cloudapp.net domain.</span></span> <span data-ttu-id="99791-120">Você deve adquirir um toouse de nome de domínio personalizado ao seu serviço de acesso.</span><span class="sxs-lookup"><span data-stu-id="99791-120">You must acquire a custom domain name toouse when access your service.</span></span> <span data-ttu-id="99791-121">Quando você solicitar um certificado de uma autoridade de certificação, nome da entidade do certificado Olá deve corresponder Olá domínio personalizado nome usado tooaccess seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="99791-121">When you request a certificate from a CA, hello certificate's subject name must match hello custom domain name used tooaccess your application.</span></span> <span data-ttu-id="99791-122">Por exemplo, se o nome de domínio personalizado for **contoso.com**, você pode solicitar um certificado da autoridade de certificação para ***.contoso.com** ou **www.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="99791-122">For example, if your custom domain name is **contoso.com** you would request a certificate from your CA for ***.contoso.com** or **www.contoso.com**.</span></span>
* <span data-ttu-id="99791-123">certificado Olá deve usar um mínimo de criptografia de 2048 bits.</span><span class="sxs-lookup"><span data-stu-id="99791-123">hello certificate must use a minimum of 2048-bit encryption.</span></span>

<span data-ttu-id="99791-124">Para fins de teste, você pode [criar](cloud-services-certs-create.md) e usar um certificado autoassinado.</span><span class="sxs-lookup"><span data-stu-id="99791-124">For test purposes, you can [create](cloud-services-certs-create.md) and use a self-signed certificate.</span></span> <span data-ttu-id="99791-125">Um certificado autoassinado não é autenticado por meio de uma autoridade de certificação e pode usar o domínio cloudapp.net de saudação como Olá URL do site.</span><span class="sxs-lookup"><span data-stu-id="99791-125">A self-signed certificate is not authenticated through a CA and can use hello cloudapp.net domain as hello website URL.</span></span> <span data-ttu-id="99791-126">Por exemplo, hello tarefa a seguir usa um certificado autoassinado no qual Olá nome comum (CN) utilizado no certificado de saudação é **sslexample.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="99791-126">For example, hello following task uses a self-signed certificate in which hello common name (CN) used in hello certificate is **sslexample.cloudapp.net**.</span></span>

<span data-ttu-id="99791-127">Em seguida, você deve incluir informações sobre o certificado de saudação em sua definição de serviço e arquivos de configuração de serviço.</span><span class="sxs-lookup"><span data-stu-id="99791-127">Next, you must include information about hello certificate in your service definition and service configuration files.</span></span>

## <a name="step-2-modify-hello-service-definition-and-configuration-files"></a><span data-ttu-id="99791-128">Etapa 2: Modificar arquivos de definição e configuração de serviço Olá</span><span class="sxs-lookup"><span data-stu-id="99791-128">Step 2: Modify hello service definition and configuration files</span></span>
<span data-ttu-id="99791-129">Seu aplicativo deve ser o certificado de saudação toouse configurado e um ponto de extremidade HTTPS deve ser adicionado.</span><span class="sxs-lookup"><span data-stu-id="99791-129">Your application must be configured toouse hello certificate, and an HTTPS endpoint must be added.</span></span> <span data-ttu-id="99791-130">Como resultado, hello definição de serviço e arquivos de configuração de serviço necessário toobe atualizado.</span><span class="sxs-lookup"><span data-stu-id="99791-130">As a result, hello service definition and service configuration files need toobe updated.</span></span>

1. <span data-ttu-id="99791-131">Em seu ambiente de desenvolvimento, abra o arquivo de definição de serviço (CSDEF) hello, adicione um **certificados** seção dentro de saudação **WebRole** seção e incluir Olá informações a seguir o certificado (e certificados intermediários):</span><span class="sxs-lookup"><span data-stu-id="99791-131">In your development environment, open hello service definition file (CSDEF), add a **Certificates** section within hello **WebRole** section, and include hello following information about the certificate (and intermediate certificates):</span></span>
   
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
   
   <span data-ttu-id="99791-132">Olá **certificados** seção define o nome de saudação do nosso certificado, seu local e o nome de saudação do repositório Olá onde ele está localizado.</span><span class="sxs-lookup"><span data-stu-id="99791-132">hello **Certificates** section defines hello name of our certificate, its location, and hello name of hello store where it is located.</span></span>
   
   <span data-ttu-id="99791-133">Permissões (`permisionLevel` atributo) pode ser tooone de conjunto de saudação seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="99791-133">Permissions (`permisionLevel` attribute) can be set tooone of hello following values:</span></span>
   
   | <span data-ttu-id="99791-134">Valor da permissão</span><span class="sxs-lookup"><span data-stu-id="99791-134">Permission Value</span></span> | <span data-ttu-id="99791-135">Descrição</span><span class="sxs-lookup"><span data-stu-id="99791-135">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="99791-136">limitedOrElevated</span><span class="sxs-lookup"><span data-stu-id="99791-136">limitedOrElevated</span></span> |<span data-ttu-id="99791-137">**(Padrão)**  Todos os processos de função podem acessar a chave privada hello.</span><span class="sxs-lookup"><span data-stu-id="99791-137">**(Default)** All role processes can access hello private key.</span></span> |
   | <span data-ttu-id="99791-138">elevado</span><span class="sxs-lookup"><span data-stu-id="99791-138">elevated</span></span> |<span data-ttu-id="99791-139">Somente os processos elevados podem acessar a chave privada hello.</span><span class="sxs-lookup"><span data-stu-id="99791-139">Only elevated processes can access hello private key.</span></span> |
2. <span data-ttu-id="99791-140">Em seu arquivo de definição de serviço, adicionar um **InputEndpoint** elemento dentro do hello **pontos de extremidade** seção tooenable HTTPS:</span><span class="sxs-lookup"><span data-stu-id="99791-140">In your service definition file, add an **InputEndpoint** element within hello **Endpoints** section tooenable HTTPS:</span></span>
   
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

3. <span data-ttu-id="99791-141">Em seu arquivo de definição de serviço, adicionar um **associação** elemento dentro do hello **Sites** seção.</span><span class="sxs-lookup"><span data-stu-id="99791-141">In your service definition file, add a **Binding** element within hello **Sites** section.</span></span> <span data-ttu-id="99791-142">Esta seção adiciona uma associação de HTTPS toomap o site do ponto de extremidade tooyour:</span><span class="sxs-lookup"><span data-stu-id="99791-142">This section adds an HTTPS binding toomap the endpoint tooyour site:</span></span>
   
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
   
   <span data-ttu-id="99791-143">Arquivo de definição de todos os Olá alterações necessárias toohello serviço foram concluídas, mas ainda precisar de informações de certificado de saudação tooadd ao arquivo de configuração do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="99791-143">All hello required changes toohello service definition file have been completed, but you still need tooadd hello certificate information to hello service configuration file.</span></span>
4. <span data-ttu-id="99791-144">Em seu arquivo de configuração de serviço (CSCFG), ServiceConfiguration, adicione um **certificados** seção dentro de saudação **função** seção, substituindo o valor de impressão digital do exemplo hello mostrado abaixo com que do seu certificado:</span><span class="sxs-lookup"><span data-stu-id="99791-144">In your service configuration file (CSCFG), ServiceConfiguration.Cloud.cscfg, add a **Certificates** section within hello **Role** section, replacing hello sample thumbprint value shown below with that of your certificate:</span></span>
   
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

<span data-ttu-id="99791-145">(Olá precede o exemplo usa **sha1** para algoritmo de impressão digital de saudação.</span><span class="sxs-lookup"><span data-stu-id="99791-145">(hello preceding example uses **sha1** for hello thumbprint algorithm.</span></span> <span data-ttu-id="99791-146">Especificar valor de saudação apropriado para o algoritmo de impressão digital do certificado).</span><span class="sxs-lookup"><span data-stu-id="99791-146">Specify hello appropriate value for your certificate's thumbprint algorithm.)</span></span>

<span data-ttu-id="99791-147">Agora que os arquivos de configuração Olá serviço definição e o serviço foi atualizados, sua implantação para carregar tooAzure do pacote.</span><span class="sxs-lookup"><span data-stu-id="99791-147">Now that hello service definition and service configuration files have been updated, package your deployment for uploading tooAzure.</span></span> <span data-ttu-id="99791-148">Caso esteja usando **cspack**, não use o sinalizador **/generateConfigurationFile**, pois ele substituirá as informações de certificado que você acabou de inserir.</span><span class="sxs-lookup"><span data-stu-id="99791-148">If you are using **cspack**, don't use the **/generateConfigurationFile** flag, as that overwrites the certificate information you inserted.</span></span>

## <a name="step-3-upload-a-certificate"></a><span data-ttu-id="99791-149">Etapa 3: Carregar um certificado</span><span class="sxs-lookup"><span data-stu-id="99791-149">Step 3: Upload a certificate</span></span>
<span data-ttu-id="99791-150">O pacote de implantação foi atualizada toouse certificado de saudação e um ponto de extremidade HTTPS foi adicionado.</span><span class="sxs-lookup"><span data-stu-id="99791-150">Your deployment package has been updated toouse hello certificate, and an HTTPS endpoint has been added.</span></span> <span data-ttu-id="99791-151">Agora você pode carregar Olá tooAzure de pacote e o certificado com hello portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="99791-151">Now you can upload hello package and certificate tooAzure with hello Azure classic portal.</span></span>

1. <span data-ttu-id="99791-152">Faça logon no toohello [portal clássico do Azure][Azure classic portal].</span><span class="sxs-lookup"><span data-stu-id="99791-152">Log in toohello [Azure classic portal][Azure classic portal].</span></span> 
2. <span data-ttu-id="99791-153">Clique em **serviços de nuvem** no painel de navegação do lado esquerdo da saudação.</span><span class="sxs-lookup"><span data-stu-id="99791-153">Click **Cloud Services** on hello left-side navigation pane.</span></span>
3. <span data-ttu-id="99791-154">Clique no serviço de nuvem Olá desejado.</span><span class="sxs-lookup"><span data-stu-id="99791-154">Click hello desired cloud service.</span></span>
4. <span data-ttu-id="99791-155">Clique em Olá **certificados** guia.</span><span class="sxs-lookup"><span data-stu-id="99791-155">Click hello **Certificates** tab.</span></span>
   
    ![Clique em Guia de certificados Olá](./media/cloud-services-configure-ssl-certificate/click-cert.png)

5. <span data-ttu-id="99791-157">Clique em Olá **carregar** botão.</span><span class="sxs-lookup"><span data-stu-id="99791-157">Click hello **Upload** button.</span></span>
   
    ![Carregar](./media/cloud-services-configure-ssl-certificate/upload-button.png)
    
6. <span data-ttu-id="99791-159">Fornecer Olá **arquivo**, **senha**, em seguida, clique em **concluir** (Olá a marca de seleção).</span><span class="sxs-lookup"><span data-stu-id="99791-159">Provide hello **File**, **Password**, then click **Complete** (hello checkmark).</span></span>

## <a name="step-4-connect-toohello-role-instance-by-using-https"></a><span data-ttu-id="99791-160">Etapa 4: Conectar a instância de função toohello usando HTTPS</span><span class="sxs-lookup"><span data-stu-id="99791-160">Step 4: Connect toohello role instance by using HTTPS</span></span>
<span data-ttu-id="99791-161">Agora que sua implantação estiver em execução no Azure, você pode conectar tooit usando HTTPS.</span><span class="sxs-lookup"><span data-stu-id="99791-161">Now that your deployment is up and running in Azure, you can connect tooit using HTTPS.</span></span>

1. <span data-ttu-id="99791-162">Em Olá portal clássico do Azure, selecione sua implantação, clique em link Olá em **URL do Site**.</span><span class="sxs-lookup"><span data-stu-id="99791-162">In hello Azure classic portal, select your deployment, then click hello link under **Site URL**.</span></span>
   
   ![Determinar URL do site][2]
2. <span data-ttu-id="99791-164">No navegador da web, modifique Olá link toouse **https** em vez de **http**e, em seguida, visite a página de saudação.</span><span class="sxs-lookup"><span data-stu-id="99791-164">In your web browser, modify hello link toouse **https** instead of **http**, and then visit hello page.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="99791-165">Se você estiver usando um certificado autoassinado, quando você procurar o ponto de extremidade HTTPS de tooan associada com um certificado autoassinado hello, que você verá um erro de certificado no navegador de saudação.</span><span class="sxs-lookup"><span data-stu-id="99791-165">If you are using a self-signed certificate, when you browse tooan HTTPS endpoint that's associated with hello self-signed certificate you may see a certificate error in hello browser.</span></span> <span data-ttu-id="99791-166">Usando um certificado assinado por uma autoridade de certificação confiável elimina esse problema; em Olá enquanto isso, você pode ignorar o erro de saudação.</span><span class="sxs-lookup"><span data-stu-id="99791-166">Using a certificate signed by a trusted certification authority eliminates this problem; in hello meantime, you can ignore hello error.</span></span> <span data-ttu-id="99791-167">(Outra opção é o repositório de certificados do usuário do toohello certificado autoassinado Olá tooadd certificado confiável autoridade.)</span><span class="sxs-lookup"><span data-stu-id="99791-167">(Another option is tooadd hello self-signed certificate toohello user's trusted certificate authority certificate store.)</span></span>
   > 
   > 
   
   ![Site de exemplo SSL][3]

<span data-ttu-id="99791-169">Se você quiser toouse SSL para uma implantação de preparo, em vez de uma implantação de produção, você primeiro precisa toodetermine Olá URL usada para implantação de preparo de saudação.</span><span class="sxs-lookup"><span data-stu-id="99791-169">If you want toouse SSL for a staging deployment instead of a production deployment, you first need toodetermine hello URL used for hello staging deployment.</span></span> <span data-ttu-id="99791-170">Implante seu ambiente de preparo do toohello de serviço de nuvem sem a inclusão de um certificado ou qualquer informação de certificado.</span><span class="sxs-lookup"><span data-stu-id="99791-170">Deploy your cloud service toohello staging environment without including a certificate or any certificate information.</span></span> <span data-ttu-id="99791-171">Uma vez implantado, você pode determinar Olá baseado em GUID URL, que é listado em Olá portal clássico do Azure **URL do Site** campo.</span><span class="sxs-lookup"><span data-stu-id="99791-171">Once deployed, you can determine hello GUID-based URL, which is listed in hello Azure classic portal's **Site URL** field.</span></span> <span data-ttu-id="99791-172">Criar um certificado com hello comuns CN (nome) toohello igual com base em GUID URL (por exemplo, **32818777-6e77-4ced-a8fc-57609d404462.cloudapp.net**).</span><span class="sxs-lookup"><span data-stu-id="99791-172">Create a certificate with hello common name (CN) equal toohello GUID-based URL (for example, **32818777-6e77-4ced-a8fc-57609d404462.cloudapp.net**).</span></span> <span data-ttu-id="99791-173">Use Olá tooadd de portal clássico do Azure Olá certificado tooyour testados serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="99791-173">Use hello Azure classic portal tooadd hello certificate tooyour staged cloud service.</span></span> <span data-ttu-id="99791-174">Em seguida, adicione Olá certificado informações tooyour CSDEF arquivos e CSCFG, reempacotar seu aplicativo e atualizar sua implantação de preparo toouse Olá novo pacote de.</span><span class="sxs-lookup"><span data-stu-id="99791-174">Then, add hello certificate information tooyour CSDEF and CSCFG files, repackage your application, and update your staged deployment toouse hello new package.</span></span>

## <a name="next-steps"></a><span data-ttu-id="99791-175">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="99791-175">Next steps</span></span>
* <span data-ttu-id="99791-176">[Configuração geral do serviço de nuvem](cloud-services-how-to-configure.md).</span><span class="sxs-lookup"><span data-stu-id="99791-176">[General configuration of your cloud service](cloud-services-how-to-configure.md).</span></span>
* <span data-ttu-id="99791-177">Saiba como muito[implantar um serviço de nuvem](cloud-services-how-to-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="99791-177">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy.md).</span></span>
* <span data-ttu-id="99791-178">Configurar um [nome de domínio personalizado](cloud-services-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="99791-178">Configure a [custom domain name](cloud-services-custom-domain-name.md).</span></span>
* <span data-ttu-id="99791-179">[Gerenciar seu serviço de nuvem](cloud-services-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="99791-179">[Manage your cloud service](cloud-services-how-to-manage.md).</span></span>

[Azure classic portal]: http://manage.windowsazure.com
[0]: ./media/cloud-services-configure-ssl-certificate/CreateCloudService.png
[1]: ./media/cloud-services-configure-ssl-certificate/AddCertificate.png
[2]: ./media/cloud-services-configure-ssl-certificate/CopyURL.png
[3]: ./media/cloud-services-configure-ssl-certificate/SSLCloudService.png
[4]: ./media/cloud-services-configure-ssl-certificate/AddCertificateComplete.png  
