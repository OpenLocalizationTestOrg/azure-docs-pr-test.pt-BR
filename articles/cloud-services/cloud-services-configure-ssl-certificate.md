---
title: "Configurar o SSL para um serviço de nuvem (clássico) | Microsoft Docs"
description: "Saiba como especificar um ponto de extremidade HTTPS para uma função Web e como carregar um certificado SSL para proteger seu aplicativo."
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
ms.openlocfilehash: edb9aaf6dae11c9b8a171b22bc8a17003f80d86b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-ssl-for-an-application-in-azure"></a><span data-ttu-id="d2b09-103">Configurando SSL para um aplicativo no Azure</span><span class="sxs-lookup"><span data-stu-id="d2b09-103">Configuring SSL for an application in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d2b09-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d2b09-104">Azure portal</span></span>](cloud-services-configure-ssl-certificate-portal.md)
> * [<span data-ttu-id="d2b09-105">Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="d2b09-105">Azure classic portal</span></span>](cloud-services-configure-ssl-certificate.md)
> 
> 

<span data-ttu-id="d2b09-106">A criptografia SSL (Secure Socket Layer) é o método mais usado para proteger dados enviados pela Internet.</span><span class="sxs-lookup"><span data-stu-id="d2b09-106">Secure Socket Layer (SSL) encryption is the most commonly used method of securing data sent across the internet.</span></span> <span data-ttu-id="d2b09-107">Esta tarefa comum aborda como especificar um ponto de extremidade HTTPS para uma função Web e como carregar um certificado SSL para proteger seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d2b09-107">This common task discusses how to specify an HTTPS endpoint for a web role and how to upload an SSL certificate to secure your application.</span></span>

> [!NOTE]
> <span data-ttu-id="d2b09-108">Os procedimentos descritos nesta tarefa se aplicam aos Serviços de Nuvem do Azure; para os Serviços de Aplicativos, veja [este](../app-service-web/web-sites-configure-ssl-certificate.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="d2b09-108">The procedures in this task apply to Azure Cloud Services; for App Services, see [this](../app-service-web/web-sites-configure-ssl-certificate.md) article.</span></span>
> 
> 

<span data-ttu-id="d2b09-109">Essa tarefa usa uma implantação de produção.</span><span class="sxs-lookup"><span data-stu-id="d2b09-109">This task uses a production deployment.</span></span> <span data-ttu-id="d2b09-110">Informações sobre o uso de uma implantação de preparo são fornecidas no final deste tópico.</span><span class="sxs-lookup"><span data-stu-id="d2b09-110">Information on using a staging deployment is provided at the end of this topic.</span></span>

<span data-ttu-id="d2b09-111">Leia [este](cloud-services-how-to-create-deploy.md) artigo primeiro se você ainda não tiver criado um serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="d2b09-111">Read [this](cloud-services-how-to-create-deploy.md) article first if you have not yet created a cloud service.</span></span>

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a><span data-ttu-id="d2b09-112">Etapa 1: Obter um certificado SSL</span><span class="sxs-lookup"><span data-stu-id="d2b09-112">Step 1: Get an SSL certificate</span></span>
<span data-ttu-id="d2b09-113">Para configurar SSL de um aplicativo, você deve primeiro obter um certificado SSL assinado por uma Autoridade de Certificação (CA), um terceiro confiável que emita certificados com essa finalidade.</span><span class="sxs-lookup"><span data-stu-id="d2b09-113">To configure SSL for an application, you first need to get an SSL certificate that has been signed by a Certificate Authority (CA), a trusted third party who issues certificates for this purpose.</span></span> <span data-ttu-id="d2b09-114">Se ainda não tiver um, você precisará obtê-lo junto a uma empresa que venda certificados SSL.</span><span class="sxs-lookup"><span data-stu-id="d2b09-114">If you do not already have one, you need to obtain one from a company that sells SSL certificates.</span></span>

<span data-ttu-id="d2b09-115">O certificado deve atender aos seguintes requisitos para certificados SSL no Azure:</span><span class="sxs-lookup"><span data-stu-id="d2b09-115">The certificate must meet the following requirements for SSL certificates in Azure:</span></span>

* <span data-ttu-id="d2b09-116">O certificado deve conter uma chave privada.</span><span class="sxs-lookup"><span data-stu-id="d2b09-116">The certificate must contain a private key.</span></span>
* <span data-ttu-id="d2b09-117">O certificado deve ser criado para troca de chaves, exportável para um arquivo Troca de Informações Pessoais (.pfx).</span><span class="sxs-lookup"><span data-stu-id="d2b09-117">The certificate must be created for key exchange, exportable to a Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="d2b09-118">O nome de assunto do certificado deve corresponder ao domínio usado para acessar o serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="d2b09-118">The certificate's subject name must match the domain used to access the cloud service.</span></span> <span data-ttu-id="d2b09-119">Você não pode obter um certificado SSL de uma autoridade de certificação (CA) para o domínio cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="d2b09-119">You cannot obtain an SSL certificate from a certificate authority (CA) for the cloudapp.net domain.</span></span> <span data-ttu-id="d2b09-120">Você deve adquirir um nome de domínio personalizado para usar quando acessar o serviço.</span><span class="sxs-lookup"><span data-stu-id="d2b09-120">You must acquire a custom domain name to use when access your service.</span></span> <span data-ttu-id="d2b09-121">Quando você solicitar um certificado de uma autoridade de certificação, o nome de assunto do certificado deve corresponder ao nome de domínio personalizado usado para acessar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d2b09-121">When you request a certificate from a CA, the certificate's subject name must match the custom domain name used to access your application.</span></span> <span data-ttu-id="d2b09-122">Por exemplo, se o nome de domínio personalizado for **contoso.com**, você pode solicitar um certificado da autoridade de certificação para ***.contoso.com** ou **www.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="d2b09-122">For example, if your custom domain name is **contoso.com** you would request a certificate from your CA for ***.contoso.com** or **www.contoso.com**.</span></span>
* <span data-ttu-id="d2b09-123">O certificado deve usar, no mínimo, uma criptografia de 2048 bits.</span><span class="sxs-lookup"><span data-stu-id="d2b09-123">The certificate must use a minimum of 2048-bit encryption.</span></span>

<span data-ttu-id="d2b09-124">Para fins de teste, você pode [criar](cloud-services-certs-create.md) e usar um certificado autoassinado.</span><span class="sxs-lookup"><span data-stu-id="d2b09-124">For test purposes, you can [create](cloud-services-certs-create.md) and use a self-signed certificate.</span></span> <span data-ttu-id="d2b09-125">Um certificado autoassinado não é autenticado por meio de uma autoridade de certificação e pode usar o domínio cloudapp.net como a URL do site.</span><span class="sxs-lookup"><span data-stu-id="d2b09-125">A self-signed certificate is not authenticated through a CA and can use the cloudapp.net domain as the website URL.</span></span> <span data-ttu-id="d2b09-126">Por exemplo, a tarefa a seguir usa um certificado autoassinado na qual o nome comum (CN) utilizado no certificado é **sslexample.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="d2b09-126">For example, the following task uses a self-signed certificate in which the common name (CN) used in the certificate is **sslexample.cloudapp.net**.</span></span>

<span data-ttu-id="d2b09-127">Em seguida, você deve incluir informações sobre o certificado nos arquivos de definição e configuração do serviço.</span><span class="sxs-lookup"><span data-stu-id="d2b09-127">Next, you must include information about the certificate in your service definition and service configuration files.</span></span>

## <a name="step-2-modify-the-service-definition-and-configuration-files"></a><span data-ttu-id="d2b09-128">Etapa 2: Modificar a definição de serviço e arquivos de configuração</span><span class="sxs-lookup"><span data-stu-id="d2b09-128">Step 2: Modify the service definition and configuration files</span></span>
<span data-ttu-id="d2b09-129">O aplicativo deve ser configurado para usar o certificado, e um ponto de extremidade HTTPS deve ser adicionado.</span><span class="sxs-lookup"><span data-stu-id="d2b09-129">Your application must be configured to use the certificate, and an HTTPS endpoint must be added.</span></span> <span data-ttu-id="d2b09-130">Dessa forma, os arquivos de definição e configuração do serviço precisam ser atualizados.</span><span class="sxs-lookup"><span data-stu-id="d2b09-130">As a result, the service definition and service configuration files need to be updated.</span></span>

1. <span data-ttu-id="d2b09-131">No ambiente de desenvolvimento, abra o arquivo de definição de serviço (CSDEF), adicione uma seção **Certificados** dentro da seção **WebRole** e inclua as seguintes informações sobre o certificado (e os certificados intermediários):</span><span class="sxs-lookup"><span data-stu-id="d2b09-131">In your development environment, open the service definition file (CSDEF), add a **Certificates** section within the **WebRole** section, and include the following information about the certificate (and intermediate certificates):</span></span>
   
    ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Certificates>
            <Certificate name="SampleCertificate" 
                        storeLocation="LocalMachine" 
                        storeName="My"
                        permissionLevel="limitedOrElevated" />
            <!-- IMPORTANT! Unless your certificate is either
            self-signed or signed directly by the CA root, you
            must include all the intermediate certificates
            here. You must list them here, even if they are
            not bound to any endpoints. Failing to list any of
            the intermediate certificates may cause hard-to-reproduce
            interoperability problems on some clients.-->
            <Certificate name="CAForSampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="CA"
                        permissionLevel="limitedOrElevated" />
        </Certificates>
    ...
    </WebRole>
    ```
   
   <span data-ttu-id="d2b09-132">A seção **Certificados** define o nome do nosso certificado, seu local e o nome do repositório no qual está localizado.</span><span class="sxs-lookup"><span data-stu-id="d2b09-132">The **Certificates** section defines the name of our certificate, its location, and the name of the store where it is located.</span></span>
   
   <span data-ttu-id="d2b09-133">As permissões (atributo `permisionLevel`) podem ser definidas como um dos seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="d2b09-133">Permissions (`permisionLevel` attribute) can be set to one of the following values:</span></span>
   
   | <span data-ttu-id="d2b09-134">Valor da permissão</span><span class="sxs-lookup"><span data-stu-id="d2b09-134">Permission Value</span></span> | <span data-ttu-id="d2b09-135">Descrição</span><span class="sxs-lookup"><span data-stu-id="d2b09-135">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="d2b09-136">limitedOrElevated</span><span class="sxs-lookup"><span data-stu-id="d2b09-136">limitedOrElevated</span></span> |<span data-ttu-id="d2b09-137">**(Padrão)** Todos os processos de função podem acessar a chave privada.</span><span class="sxs-lookup"><span data-stu-id="d2b09-137">**(Default)** All role processes can access the private key.</span></span> |
   | <span data-ttu-id="d2b09-138">elevado</span><span class="sxs-lookup"><span data-stu-id="d2b09-138">elevated</span></span> |<span data-ttu-id="d2b09-139">Somente processos elevados podem acessar a chave privada.</span><span class="sxs-lookup"><span data-stu-id="d2b09-139">Only elevated processes can access the private key.</span></span> |
2. <span data-ttu-id="d2b09-140">No arquivo de definição de serviço, adicione um elemento **InputEndpoint** dentro da seção **Pontos de extremidade** para habilitar HTTPS:</span><span class="sxs-lookup"><span data-stu-id="d2b09-140">In your service definition file, add an **InputEndpoint** element within the **Endpoints** section to enable HTTPS:</span></span>
   
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

3. <span data-ttu-id="d2b09-141">No arquivo de definição de serviço, adicione um elemento de **Associação** dentro da seção **Sites**.</span><span class="sxs-lookup"><span data-stu-id="d2b09-141">In your service definition file, add a **Binding** element within the **Sites** section.</span></span> <span data-ttu-id="d2b09-142">Essa seção adiciona uma associação HTTP para mapear o ponto de extremidade para o site:</span><span class="sxs-lookup"><span data-stu-id="d2b09-142">This section adds an HTTPS binding to map the endpoint to your site:</span></span>
   
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
   
   <span data-ttu-id="d2b09-143">Todas as alterações obrigatórias no arquivo de definição de serviço foram concluídas, mas você continua precisando adicionar as informações de certificado ao arquivo de configuração de serviço.</span><span class="sxs-lookup"><span data-stu-id="d2b09-143">All the required changes to the service definition file have been completed, but you still need to add the certificate information to the service configuration file.</span></span>
4. <span data-ttu-id="d2b09-144">No arquivo de configuração de serviço (CSCFG), ServiceConfiguration.Cloud.cscfg, adicione uma seção **Certificados** na seção **Função**, substituindo o valor de exemplo de impressão digital mostrado abaixo pelo seu certificado:</span><span class="sxs-lookup"><span data-stu-id="d2b09-144">In your service configuration file (CSCFG), ServiceConfiguration.Cloud.cscfg, add a **Certificates** section within the **Role** section, replacing the sample thumbprint value shown below with that of your certificate:</span></span>
   
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

<span data-ttu-id="d2b09-145">(O exemplo acima usa **sha1** para o algoritmo de impressão digital.</span><span class="sxs-lookup"><span data-stu-id="d2b09-145">(The preceding example uses **sha1** for the thumbprint algorithm.</span></span> <span data-ttu-id="d2b09-146">Especifique o valor apropriado ao algoritmo thumbprint do certificado.)</span><span class="sxs-lookup"><span data-stu-id="d2b09-146">Specify the appropriate value for your certificate's thumbprint algorithm.)</span></span>

<span data-ttu-id="d2b09-147">Agora que os arquivos de definição e configuração do serviço foram atualizados, empacote a implantação para carregamento no Azure.</span><span class="sxs-lookup"><span data-stu-id="d2b09-147">Now that the service definition and service configuration files have been updated, package your deployment for uploading to Azure.</span></span> <span data-ttu-id="d2b09-148">Caso esteja usando **cspack**, não use o sinalizador **/generateConfigurationFile**, pois ele substituirá as informações de certificado que você acabou de inserir.</span><span class="sxs-lookup"><span data-stu-id="d2b09-148">If you are using **cspack**, don't use the **/generateConfigurationFile** flag, as that overwrites the certificate information you inserted.</span></span>

## <a name="step-3-upload-a-certificate"></a><span data-ttu-id="d2b09-149">Etapa 3: Carregar um certificado</span><span class="sxs-lookup"><span data-stu-id="d2b09-149">Step 3: Upload a certificate</span></span>
<span data-ttu-id="d2b09-150">O pacote de implantação foi atualizado para usar o certificado, e um ponto de extremidade HTTPS foi adicionado.</span><span class="sxs-lookup"><span data-stu-id="d2b09-150">Your deployment package has been updated to use the certificate, and an HTTPS endpoint has been added.</span></span> <span data-ttu-id="d2b09-151">Agora é possível carregar o pacote e o certificado no Azure com o portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="d2b09-151">Now you can upload the package and certificate to Azure with the Azure classic portal.</span></span>

1. <span data-ttu-id="d2b09-152">Faça logon no [Portal Clássico do Azure][Azure classic portal].</span><span class="sxs-lookup"><span data-stu-id="d2b09-152">Log in to the [Azure classic portal][Azure classic portal].</span></span> 
2. <span data-ttu-id="d2b09-153">Clique em **Serviços de Nuvem** no painel de navegação à esquerda.</span><span class="sxs-lookup"><span data-stu-id="d2b09-153">Click **Cloud Services** on the left-side navigation pane.</span></span>
3. <span data-ttu-id="d2b09-154">Clique no serviço de nuvem desejado.</span><span class="sxs-lookup"><span data-stu-id="d2b09-154">Click the desired cloud service.</span></span>
4. <span data-ttu-id="d2b09-155">Clique na guia **Certificados**.</span><span class="sxs-lookup"><span data-stu-id="d2b09-155">Click the **Certificates** tab.</span></span>
   
    ![Clique na guia Certificados](./media/cloud-services-configure-ssl-certificate/click-cert.png)

5. <span data-ttu-id="d2b09-157">Clique no botão **Carregar** .</span><span class="sxs-lookup"><span data-stu-id="d2b09-157">Click the **Upload** button.</span></span>
   
    ![Carregar](./media/cloud-services-configure-ssl-certificate/upload-button.png)
    
6. <span data-ttu-id="d2b09-159">Forneça o **Arquivo**, a **Senha** e depois clique em **Concluir** (a marca de seleção).</span><span class="sxs-lookup"><span data-stu-id="d2b09-159">Provide the **File**, **Password**, then click **Complete** (the checkmark).</span></span>

## <a name="step-4-connect-to-the-role-instance-by-using-https"></a><span data-ttu-id="d2b09-160">Etapa 4: Conectar-se à instância da função usando HTTPS</span><span class="sxs-lookup"><span data-stu-id="d2b09-160">Step 4: Connect to the role instance by using HTTPS</span></span>
<span data-ttu-id="d2b09-161">Agora que sua implantação está ativa e em execução no Azure, você pode se conectar a ela usando HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d2b09-161">Now that your deployment is up and running in Azure, you can connect to it using HTTPS.</span></span>

1. <span data-ttu-id="d2b09-162">No portal clássico do Azure, selecione a implantação e clique no link em **URL do Site**.</span><span class="sxs-lookup"><span data-stu-id="d2b09-162">In the Azure classic portal, select your deployment, then click the link under **Site URL**.</span></span>
   
   ![Determinar URL do site][2]
2. <span data-ttu-id="d2b09-164">No navegador da Web, modifique o link para usar **http** sem vez de **http**, e visite a página.</span><span class="sxs-lookup"><span data-stu-id="d2b09-164">In your web browser, modify the link to use **https** instead of **http**, and then visit the page.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d2b09-165">Se estiver usando um certificado autoassinado, ao navegar até um ponto de extremidade HTTPS associado com o certificado autoassinado, você poderá ver um erro de certificado no navegador.</span><span class="sxs-lookup"><span data-stu-id="d2b09-165">If you are using a self-signed certificate, when you browse to an HTTPS endpoint that's associated with the self-signed certificate you may see a certificate error in the browser.</span></span> <span data-ttu-id="d2b09-166">O uso de um certificado assinado por uma certificação confiável elimina esse problema; enquanto isso, você pode ignorar o erro.</span><span class="sxs-lookup"><span data-stu-id="d2b09-166">Using a certificate signed by a trusted certification authority eliminates this problem; in the meantime, you can ignore the error.</span></span> <span data-ttu-id="d2b09-167">(Outra opção é adicionar o certificado autoassinado ao repositório de certificado da autoridade de certificado confiável do usuário.)</span><span class="sxs-lookup"><span data-stu-id="d2b09-167">(Another option is to add the self-signed certificate to the user's trusted certificate authority certificate store.)</span></span>
   > 
   > 
   
   ![Site de exemplo SSL][3]

<span data-ttu-id="d2b09-169">Se quiser usar SSL em uma implantação de preparação em lugar de uma implantação da produção, você precisará determinar primeiro o URL usado na implantação de preparação.</span><span class="sxs-lookup"><span data-stu-id="d2b09-169">If you want to use SSL for a staging deployment instead of a production deployment, you first need to determine the URL used for the staging deployment.</span></span> <span data-ttu-id="d2b09-170">Implante o serviço de nuvem no ambiente de preparação sem incluir um certificado ou qualquer informação de certificado.</span><span class="sxs-lookup"><span data-stu-id="d2b09-170">Deploy your cloud service to the staging environment without including a certificate or any certificate information.</span></span> <span data-ttu-id="d2b09-171">Depois de implantado, você poderá determinar a URL baseada em GUID, listada no campo **URL do Site** do portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="d2b09-171">Once deployed, you can determine the GUID-based URL, which is listed in the Azure classic portal's **Site URL** field.</span></span> <span data-ttu-id="d2b09-172">Crie um certificado com o nome comum (CN) igual à URL baseada em GUID (por exemplo, **32818777-6e77-4ced-a8fc-57609d404462.cloudapp.net**).</span><span class="sxs-lookup"><span data-stu-id="d2b09-172">Create a certificate with the common name (CN) equal to the GUID-based URL (for example, **32818777-6e77-4ced-a8fc-57609d404462.cloudapp.net**).</span></span> <span data-ttu-id="d2b09-173">Use o portal clássico do Azure para adicionar o certificado ao serviço de nuvem preparado.</span><span class="sxs-lookup"><span data-stu-id="d2b09-173">Use the Azure classic portal to add the certificate to your staged cloud service.</span></span> <span data-ttu-id="d2b09-174">Em seguida, adicione as informações de certificado aos arquivos CSDEF e CSCFG, reempacote seu aplicativo e atualize a implantação preparada usando o novo pacote.</span><span class="sxs-lookup"><span data-stu-id="d2b09-174">Then, add the certificate information to your CSDEF and CSCFG files, repackage your application, and update your staged deployment to use the new package.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2b09-175">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d2b09-175">Next steps</span></span>
* <span data-ttu-id="d2b09-176">[Configuração geral do serviço de nuvem](cloud-services-how-to-configure.md).</span><span class="sxs-lookup"><span data-stu-id="d2b09-176">[General configuration of your cloud service](cloud-services-how-to-configure.md).</span></span>
* <span data-ttu-id="d2b09-177">Saiba como [implantar um serviço de nuvem](cloud-services-how-to-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="d2b09-177">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy.md).</span></span>
* <span data-ttu-id="d2b09-178">Configurar um [nome de domínio personalizado](cloud-services-custom-domain-name.md).</span><span class="sxs-lookup"><span data-stu-id="d2b09-178">Configure a [custom domain name](cloud-services-custom-domain-name.md).</span></span>
* <span data-ttu-id="d2b09-179">[Gerenciar seu serviço de nuvem](cloud-services-how-to-manage.md).</span><span class="sxs-lookup"><span data-stu-id="d2b09-179">[Manage your cloud service](cloud-services-how-to-manage.md).</span></span>

[Azure classic portal]: http://manage.windowsazure.com
[0]: ./media/cloud-services-configure-ssl-certificate/CreateCloudService.png
[1]: ./media/cloud-services-configure-ssl-certificate/AddCertificate.png
[2]: ./media/cloud-services-configure-ssl-certificate/CopyURL.png
[3]: ./media/cloud-services-configure-ssl-certificate/SSLCloudService.png
[4]: ./media/cloud-services-configure-ssl-certificate/AddCertificateComplete.png  
