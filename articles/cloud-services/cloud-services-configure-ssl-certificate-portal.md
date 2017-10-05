---
title: "Configurar SSL para um serviço de nuvem | Microsoft Docs"
description: "Saiba como especificar um ponto de extremidade HTTPS para uma função Web e como carregar um certificado SSL para proteger seu aplicativo. Esses exemplos usam o portal do Azure."
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
ms.openlocfilehash: e5c8c3b098772c0586712305a577b24a6f0d924c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-ssl-for-an-application-in-azure"></a><span data-ttu-id="7a4b1-104">Configurando SSL para um aplicativo no Azure</span><span class="sxs-lookup"><span data-stu-id="7a4b1-104">Configuring SSL for an application in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7a4b1-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7a4b1-105">Azure portal</span></span>](cloud-services-configure-ssl-certificate-portal.md)
> * [<span data-ttu-id="7a4b1-106">Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="7a4b1-106">Azure classic portal</span></span>](cloud-services-configure-ssl-certificate.md)
>

<span data-ttu-id="7a4b1-107">A criptografia SSL (Secure Socket Layer) é o método mais usado para proteger dados enviados pela Internet.</span><span class="sxs-lookup"><span data-stu-id="7a4b1-107">Secure Socket Layer (SSL) encryption is the most commonly used method of securing data sent across the internet.</span></span> <span data-ttu-id="7a4b1-108">Esta tarefa comum aborda como especificar um ponto de extremidade HTTPS para uma função Web e como carregar um certificado SSL para proteger seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7a4b1-108">This common task discusses how to specify an HTTPS endpoint for a web role and how to upload an SSL certificate to secure your application.</span></span>

> [!NOTE]
> <span data-ttu-id="7a4b1-109">Os procedimentos descritos nesta tarefa se aplicam aos Serviços de Nuvem do Azure; para os Serviços de Aplicativos, veja [isto](../app-service-web/web-sites-configure-ssl-certificate.md).</span><span class="sxs-lookup"><span data-stu-id="7a4b1-109">The procedures in this task apply to Azure Cloud Services; for App Services, see [this](../app-service-web/web-sites-configure-ssl-certificate.md).</span></span>
>

<span data-ttu-id="7a4b1-110">Essa tarefa usa uma implantação de produção.</span><span class="sxs-lookup"><span data-stu-id="7a4b1-110">This task uses a production deployment.</span></span> <span data-ttu-id="7a4b1-111">Informações sobre o uso de uma implantação de preparo são fornecidas no final deste tópico.</span><span class="sxs-lookup"><span data-stu-id="7a4b1-111">Information on using a staging deployment is provided at the end of this topic.</span></span>

<span data-ttu-id="7a4b1-112">Leia [isto](cloud-services-how-to-create-deploy-portal.md) primeiro se você ainda não tiver criado um serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="7a4b1-112">Read [this](cloud-services-how-to-create-deploy-portal.md) first if you have not yet created a cloud service.</span></span>

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a><span data-ttu-id="7a4b1-113">Etapa 1: Obter um certificado SSL</span><span class="sxs-lookup"><span data-stu-id="7a4b1-113">Step 1: Get an SSL certificate</span></span>
<span data-ttu-id="7a4b1-114">Para configurar SSL de um aplicativo, você deve primeiro obter um certificado SSL assinado por uma Autoridade de Certificação (CA), um terceiro confiável que emita certificados com essa finalidade.</span><span class="sxs-lookup"><span data-stu-id="7a4b1-114">To configure SSL for an application, you first need to get an SSL certificate that has been signed by a Certificate Authority (CA), a trusted third party who issues certificates for this purpose.</span></span> <span data-ttu-id="7a4b1-115">Se ainda não tiver um, você precisará obtê-lo junto a uma empresa que venda certificados SSL.</span><span class="sxs-lookup"><span data-stu-id="7a4b1-115">If you do not already have one, you need to obtain one from a company that sells SSL certificates.</span></span>

<span data-ttu-id="7a4b1-116">O certificado deve atender aos seguintes requisitos para certificados SSL no Azure:</span><span class="sxs-lookup"><span data-stu-id="7a4b1-116">The certificate must meet the following requirements for SSL certificates in Azure:</span></span>

* <span data-ttu-id="7a4b1-117">O certificado deve conter uma chave privada.</span><span class="sxs-lookup"><span data-stu-id="7a4b1-117">The certificate must contain a private key.</span></span>
* <span data-ttu-id="7a4b1-118">O certificado deve ser criado para troca de chaves, exportável para um arquivo Troca de Informações Pessoais (.pfx).</span><span class="sxs-lookup"><span data-stu-id="7a4b1-118">The certificate must be created for key exchange, exportable to a Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="7a4b1-119">O nome de assunto do certificado deve corresponder ao domínio usado para acessar o serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="7a4b1-119">The certificate's subject name must match the domain used to access the cloud service.</span></span> <span data-ttu-id="7a4b1-120">Você não pode obter um certificado SSL de uma autoridade de certificação (CA) para o domínio cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="7a4b1-120">You cannot obtain an SSL certificate from a certificate authority (CA) for the cloudapp.net domain.</span></span> <span data-ttu-id="7a4b1-121">Você deve adquirir um nome de domínio personalizado para usar quando acessar o serviço.</span><span class="sxs-lookup"><span data-stu-id="7a4b1-121">You must acquire a custom domain name to use when access your service.</span></span> <span data-ttu-id="7a4b1-122">Quando você solicitar um certificado de uma autoridade de certificação, o nome de assunto do certificado deve corresponder ao nome de domínio personalizado usado para acessar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7a4b1-122">When you request a certificate from a CA, the certificate's subject name must match the custom domain name used to access your application.</span></span> <span data-ttu-id="7a4b1-123">Por exemplo, se o nome de domínio personalizado for **contoso.com**, você pode solicitar um certificado da autoridade de certificação para ***.contoso.com** ou **www.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="7a4b1-123">For example, if your custom domain name is **contoso.com** you would request a certificate from your CA for ***.contoso.com** or **www.contoso.com**.</span></span>
* <span data-ttu-id="7a4b1-124">O certificado deve usar, no mínimo, uma criptografia de 2048 bits.</span><span class="sxs-lookup"><span data-stu-id="7a4b1-124">The certificate must use a minimum of 2048-bit encryption.</span></span>

<span data-ttu-id="7a4b1-125">Para fins de teste, você pode [criar](cloud-services-certs-create.md) e usar um certificado autoassinado.</span><span class="sxs-lookup"><span data-stu-id="7a4b1-125">For test purposes, you can [create](cloud-services-certs-create.md) and use a self-signed certificate.</span></span> <span data-ttu-id="7a4b1-126">Um certificado autoassinado não é autenticado por meio de uma autoridade de certificação e pode usar o domínio cloudapp.net como a URL do site.</span><span class="sxs-lookup"><span data-stu-id="7a4b1-126">A self-signed certificate is not authenticated through a CA and can use the cloudapp.net domain as the website URL.</span></span> <span data-ttu-id="7a4b1-127">Por exemplo, a tarefa a seguir usa um certificado autoassinado na qual o nome comum (CN) utilizado no certificado é **sslexample.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="7a4b1-127">For example, the following task uses a self-signed certificate in which the common name (CN) used in the certificate is **sslexample.cloudapp.net**.</span></span>

<span data-ttu-id="7a4b1-128">Em seguida, você deve incluir informações sobre o certificado nos arquivos de definição e configuração do serviço.</span><span class="sxs-lookup"><span data-stu-id="7a4b1-128">Next, you must include information about the certificate in your service definition and service configuration files.</span></span>

<span data-ttu-id="7a4b1-129"><a name="modify"> </a></span><span class="sxs-lookup"><span data-stu-id="7a4b1-129"><a name="modify"> </a></span></span>

## <a name="step-2-modify-the-service-definition-and-configuration-files"></a><span data-ttu-id="7a4b1-130">Etapa 2: Modificar a definição de serviço e arquivos de configuração</span><span class="sxs-lookup"><span data-stu-id="7a4b1-130">Step 2: Modify the service definition and configuration files</span></span>
<span data-ttu-id="7a4b1-131">O aplicativo deve ser configurado para usar o certificado, e um ponto de extremidade HTTPS deve ser adicionado.</span><span class="sxs-lookup"><span data-stu-id="7a4b1-131">Your application must be configured to use the certificate, and an HTTPS endpoint must be added.</span></span> <span data-ttu-id="7a4b1-132">Dessa forma, os arquivos de definição e configuração do serviço precisam ser atualizados.</span><span class="sxs-lookup"><span data-stu-id="7a4b1-132">As a result, the service definition and service configuration files need to be updated.</span></span>

1. <span data-ttu-id="7a4b1-133">No ambiente de desenvolvimento, abra o arquivo de definição de serviço (CSDEF), adicione uma seção **Certificados** dentro da seção **WebRole** e inclua as seguintes informações sobre o certificado (e os certificados intermediários):</span><span class="sxs-lookup"><span data-stu-id="7a4b1-133">In your development environment, open the service definition file (CSDEF), add a **Certificates** section within the **WebRole** section, and include the following information about the certificate (and intermediate certificates):</span></span>

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

   <span data-ttu-id="7a4b1-134">A seção **Certificados** define o nome do nosso certificado, seu local e o nome do repositório no qual está localizado.</span><span class="sxs-lookup"><span data-stu-id="7a4b1-134">The **Certificates** section defines the name of our certificate, its location, and the name of the store where it is located.</span></span>

   <span data-ttu-id="7a4b1-135">As permissões (atributo `permisionLevel`) podem ser definidas como um dos seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="7a4b1-135">Permissions (`permisionLevel` attribute) can be set to one of the following values:</span></span>

   | <span data-ttu-id="7a4b1-136">Valor da permissão</span><span class="sxs-lookup"><span data-stu-id="7a4b1-136">Permission Value</span></span> | <span data-ttu-id="7a4b1-137">Descrição</span><span class="sxs-lookup"><span data-stu-id="7a4b1-137">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="7a4b1-138">limitedOrElevated</span><span class="sxs-lookup"><span data-stu-id="7a4b1-138">limitedOrElevated</span></span> |<span data-ttu-id="7a4b1-139">**(Padrão)** Todos os processos de função podem acessar a chave privada.</span><span class="sxs-lookup"><span data-stu-id="7a4b1-139">**(Default)** All role processes can access the private key.</span></span> |
   | <span data-ttu-id="7a4b1-140">elevado</span><span class="sxs-lookup"><span data-stu-id="7a4b1-140">elevated</span></span> |<span data-ttu-id="7a4b1-141">Somente processos elevados podem acessar a chave privada.</span><span class="sxs-lookup"><span data-stu-id="7a4b1-141">Only elevated processes can access the private key.</span></span> |

2. <span data-ttu-id="7a4b1-142">No arquivo de definição de serviço, adicione um elemento **InputEndpoint** dentro da seção **Pontos de extremidade** para habilitar HTTPS:</span><span class="sxs-lookup"><span data-stu-id="7a4b1-142">In your service definition file, add an **InputEndpoint** element within the **Endpoints** section to enable HTTPS:</span></span>

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

3. <span data-ttu-id="7a4b1-143">No arquivo de definição de serviço, adicione um elemento de **Associação** dentro da seção **Sites**.</span><span class="sxs-lookup"><span data-stu-id="7a4b1-143">In your service definition file, add a **Binding** element within the **Sites** section.</span></span> <span data-ttu-id="7a4b1-144">Este elemento adiciona uma associação HTTPS para mapear o ponto de extremidade para o site:</span><span class="sxs-lookup"><span data-stu-id="7a4b1-144">This element adds an HTTPS binding to map the endpoint to your site:</span></span>

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

   <span data-ttu-id="7a4b1-145">Todas as alterações obrigatórias no arquivo de definição de serviço foram concluídas, mas você continua precisando adicionar as informações de certificado ao arquivo de configuração de serviço.</span><span class="sxs-lookup"><span data-stu-id="7a4b1-145">All the required changes to the service definition file have been completed; but, you still need to add the certificate information to the service configuration file.</span></span>
4. <span data-ttu-id="7a4b1-146">Em seu arquivo de configuração de serviço (CSCFG), ServiceConfiguration.Cloud.cscfg, adicione um valor de **Certificados** com o do seu certificado.</span><span class="sxs-lookup"><span data-stu-id="7a4b1-146">In your service configuration file (CSCFG), ServiceConfiguration.Cloud.cscfg, add a **Certificates** value with that of your certificate.</span></span> <span data-ttu-id="7a4b1-147">O exemplo de código a seguir fornece detalhes da seção **Certificados**, exceto para o valor de impressão digital.</span><span class="sxs-lookup"><span data-stu-id="7a4b1-147">The following code sample provides details of the **Certificates** section, except for the thumbprint value.</span></span>

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

<span data-ttu-id="7a4b1-148">(Este exemplo usa **sha1** para o algoritmo de impressão digital.</span><span class="sxs-lookup"><span data-stu-id="7a4b1-148">(This example uses **sha1** for the thumbprint algorithm.</span></span> <span data-ttu-id="7a4b1-149">Especifique o valor apropriado ao algoritmo thumbprint do certificado.)</span><span class="sxs-lookup"><span data-stu-id="7a4b1-149">Specify the appropriate value for your certificate's thumbprint algorithm.)</span></span>

<span data-ttu-id="7a4b1-150">Agora que os arquivos de definição e configuração do serviço foram atualizados, empacote a implantação para carregamento no Azure.</span><span class="sxs-lookup"><span data-stu-id="7a4b1-150">Now that the service definition and service configuration files have been updated, package your deployment for uploading to Azure.</span></span> <span data-ttu-id="7a4b1-151">Se você está usando **cspack**, não use o sinalizador **/generateConfigurationFile**, pois ele substituirá as informações de certificado que você acabou de inserir.</span><span class="sxs-lookup"><span data-stu-id="7a4b1-151">If you are using **cspack**, don't use the **/generateConfigurationFile** flag, as that will overwrite the certificate information you just inserted.</span></span>

## <a name="step-3-upload-a-certificate"></a><span data-ttu-id="7a4b1-152">Etapa 3: Carregar um certificado</span><span class="sxs-lookup"><span data-stu-id="7a4b1-152">Step 3: Upload a certificate</span></span>
<span data-ttu-id="7a4b1-153">Conecte-se ao Portal do Azure e...</span><span class="sxs-lookup"><span data-stu-id="7a4b1-153">Connect to the Azure portal and...</span></span>

1. <span data-ttu-id="7a4b1-154">Na seção **Todos os recursos** do Portal, selecione seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="7a4b1-154">In the **All resources** section of the Portal, select your cloud service.</span></span>

    ![Publicar o serviço de nuvem](media/cloud-services-configure-ssl-certificate-portal/browse.png)

2. <span data-ttu-id="7a4b1-156">Clique em **Certificados**.</span><span class="sxs-lookup"><span data-stu-id="7a4b1-156">Click **Certificates**.</span></span>

    ![Clique no ícone de certificados](media/cloud-services-configure-ssl-certificate-portal/certificate-item.png)

3. <span data-ttu-id="7a4b1-158">Clique em **Carregar** na parte superior da área de certificados.</span><span class="sxs-lookup"><span data-stu-id="7a4b1-158">Click **Upload** at the top of the certificates area.</span></span>

    ![Clique no item de menu Carregar](media/cloud-services-configure-ssl-certificate-portal/Upload_menu.png)

4. <span data-ttu-id="7a4b1-160">Forneça o **Arquivo**, **Senha** e clique em **Carregar** na parte inferior da área de entrada de dados.</span><span class="sxs-lookup"><span data-stu-id="7a4b1-160">Provide the **File**, **Password**, then click **Upload** at the bottom of the data entry area.</span></span>

## <a name="step-4-connect-to-the-role-instance-by-using-https"></a><span data-ttu-id="7a4b1-161">Etapa 4: Conectar-se à instância da função usando HTTPS</span><span class="sxs-lookup"><span data-stu-id="7a4b1-161">Step 4: Connect to the role instance by using HTTPS</span></span>
<span data-ttu-id="7a4b1-162">Agora que sua implantação está ativa e em execução no Azure, você pode se conectar a ela usando HTTPS.</span><span class="sxs-lookup"><span data-stu-id="7a4b1-162">Now that your deployment is up and running in Azure, you can connect to it using HTTPS.</span></span>

1. <span data-ttu-id="7a4b1-163">Clique na **URL do Site** para abrir o navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="7a4b1-163">Click the **Site URL** to open up the web browser.</span></span>

   ![Clique na URL do site](media/cloud-services-configure-ssl-certificate-portal/navigate.png)

2. <span data-ttu-id="7a4b1-165">No navegador da Web, modifique o link para usar **http** sem vez de **http**, e visite a página.</span><span class="sxs-lookup"><span data-stu-id="7a4b1-165">In your web browser, modify the link to use **https** instead of **http**, and then visit the page.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7a4b1-166">Se estiver usando um certificado autoassinado, ao navegar até um ponto de extremidade HTTPS associado com o certificado autoassinado, você poderá ver um erro de certificado no navegador.</span><span class="sxs-lookup"><span data-stu-id="7a4b1-166">If you are using a self-signed certificate, when you browse to an HTTPS endpoint that's associated with the self-signed certificate you may see a certificate error in the browser.</span></span> <span data-ttu-id="7a4b1-167">O uso de um certificado assinado por uma certificação confiável elimina esse problema; enquanto isso, você pode ignorar o erro.</span><span class="sxs-lookup"><span data-stu-id="7a4b1-167">Using a certificate signed by a trusted certification authority eliminates this problem; in the meantime, you can ignore the error.</span></span> <span data-ttu-id="7a4b1-168">(Outra opção é adicionar o certificado autoassinado ao repositório de certificado da autoridade de certificado confiável do usuário.)</span><span class="sxs-lookup"><span data-stu-id="7a4b1-168">(Another option is to add the self-signed certificate to the user's trusted certificate authority certificate store.)</span></span>
   >
   >

   ![Visualização de site](media/cloud-services-configure-ssl-certificate-portal/show-site.png)

   > [!TIP]
   > <span data-ttu-id="7a4b1-170">Se quiser usar SSL em uma implantação de preparação em lugar de uma implantação da produção, você precisará determinar primeiro o URL usado na implantação de preparação.</span><span class="sxs-lookup"><span data-stu-id="7a4b1-170">If you want to use SSL for a staging deployment instead of a production deployment, you'll first need to determine the URL used for the staging deployment.</span></span> <span data-ttu-id="7a4b1-171">Após o serviço de nuvem ter sido implantado, a URL para o ambiente de preparo será determinada pelo GUID da **ID da Implantação** neste formato: `https://deployment-id.cloudapp.net/`</span><span class="sxs-lookup"><span data-stu-id="7a4b1-171">Once your cloud service has been deployed, the URL to the staging environment is determined by the **Deployment ID** GUID in this format: `https://deployment-id.cloudapp.net/`</span></span>  
   >
   > <span data-ttu-id="7a4b1-172">Criar um certificado com o nome comum (CN) igual à URL baseada em GUID (por exemplo, **328187776e774ceda8fc57609d404462.cloudapp.net**).</span><span class="sxs-lookup"><span data-stu-id="7a4b1-172">Create a certificate with the common name (CN) equal to the GUID-based URL (for example, **328187776e774ceda8fc57609d404462.cloudapp.net**).</span></span> <span data-ttu-id="7a4b1-173">Use o portal para adicionar o certificado ao serviço de nuvem preparado.</span><span class="sxs-lookup"><span data-stu-id="7a4b1-173">Use the portal to add the certificate to your staged cloud service.</span></span> <span data-ttu-id="7a4b1-174">Em seguida, adicione as informações de certificado aos arquivos CSDEF e CSCFG, reempacote seu aplicativo e atualize a implantação preparada usando o novo pacote.</span><span class="sxs-lookup"><span data-stu-id="7a4b1-174">Then, add the certificate information to your CSDEF and CSCFG files, repackage your application, and update your staged deployment to use the new package.</span></span>
   >

## <a name="next-steps"></a><span data-ttu-id="7a4b1-175">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7a4b1-175">Next steps</span></span>
* <span data-ttu-id="7a4b1-176">[Configuração geral do serviço de nuvem](cloud-services-how-to-configure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7a4b1-176">[General configuration of your cloud service](cloud-services-how-to-configure-portal.md).</span></span>
* <span data-ttu-id="7a4b1-177">Saiba como [implantar um serviço de nuvem](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7a4b1-177">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="7a4b1-178">Configurar um [nome de domínio personalizado](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7a4b1-178">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="7a4b1-179">[Gerenciar seu serviço de nuvem](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7a4b1-179">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
