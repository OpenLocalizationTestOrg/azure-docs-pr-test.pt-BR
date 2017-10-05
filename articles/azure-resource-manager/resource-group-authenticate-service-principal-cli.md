---
title: Criar identidade para o aplicativo do Azure com a CLI do Azure | Microsoft Docs
description: "Descreve como usar a CLI do Azure para criar um aplicativo do Active Directory do Azure e uma entidade de serviço, e conceder acesso a recursos por meio do controle de acesso baseado em função. Ele mostra como autenticar um aplicativo com uma senha ou certificado."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: c224a189-dd28-4801-b3e3-26991b0eb24d
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 3c5826d58887ff1af4df8e66999d9c1a1643bcc7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="use-azure-cli-to-create-a-service-principal-to-access-resources"></a><span data-ttu-id="27f38-104">Usar a CLI do Azure para criar uma entidade de serviço a fim de acessar recursos</span><span class="sxs-lookup"><span data-stu-id="27f38-104">Use Azure CLI to create a service principal to access resources</span></span>

<span data-ttu-id="27f38-105">Quando você tiver um aplicativo ou script que precisa acessar recursos, poderá configurar uma identidade para o aplicativo e autenticá-lo com suas próprias credenciais.</span><span class="sxs-lookup"><span data-stu-id="27f38-105">When you have an app or script that needs to access resources, you can set up an identity for the app and authenticate the app with its own credentials.</span></span> <span data-ttu-id="27f38-106">Essa identidade é conhecida como uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="27f38-106">This identity is known as a service principal.</span></span> <span data-ttu-id="27f38-107">Essa abordagem permite:</span><span class="sxs-lookup"><span data-stu-id="27f38-107">This approach enables you to:</span></span>

* <span data-ttu-id="27f38-108">Atribuir permissões à identidade do aplicativo que são diferentes de suas próprias permissões.</span><span class="sxs-lookup"><span data-stu-id="27f38-108">Assign permissions to the app identity that are different than your own permissions.</span></span> <span data-ttu-id="27f38-109">Normalmente, essas permissões são restritas a exatamente o que o aplicativo precisa fazer.</span><span class="sxs-lookup"><span data-stu-id="27f38-109">Typically, these permissions are restricted to exactly what the app needs to do.</span></span>
* <span data-ttu-id="27f38-110">Use um certificado para a autenticação ao executar um script autônomo.</span><span class="sxs-lookup"><span data-stu-id="27f38-110">Use a certificate for authentication when executing an unattended script.</span></span>

<span data-ttu-id="27f38-111">Este artigo mostra como usar a [CLI do Azure 1.0](../cli-install-nodejs.md) para configurar um aplicativo a ser executado com suas próprias credenciais e identidade.</span><span class="sxs-lookup"><span data-stu-id="27f38-111">This article shows you how to use [Azure CLI 1.0](../cli-install-nodejs.md) to set up an application to run under its own credentials and identity.</span></span> <span data-ttu-id="27f38-112">Instale a versão mais recente do [Azure CLI 1.0](../cli-install-nodejs.md) para certificar-se de que seu ambiente corresponde aos exemplos neste artigo.</span><span class="sxs-lookup"><span data-stu-id="27f38-112">Install the latest version of [Azure CLI 1.0](../cli-install-nodejs.md) to make sure your environment matches the examples in this article.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="27f38-113">Permissões necessárias</span><span class="sxs-lookup"><span data-stu-id="27f38-113">Required permissions</span></span>
<span data-ttu-id="27f38-114">Para concluir este tópico, você deve ter permissões suficientes no Azure Active Directory e em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="27f38-114">To complete this topic, you must have sufficient permissions in both your Azure Active Directory and your Azure subscription.</span></span> <span data-ttu-id="27f38-115">Especificamente, você deve ser capaz de criar um aplicativo no Active Directory do Azure e atribuir a entidade de serviço a uma função.</span><span class="sxs-lookup"><span data-stu-id="27f38-115">Specifically, you must be able to create an app in the Azure Active Directory, and assign the service principal to a role.</span></span> 

<span data-ttu-id="27f38-116">A maneira mais fácil de verificar se a sua conta tem as permissões adequadas é por meio do portal.</span><span class="sxs-lookup"><span data-stu-id="27f38-116">The easiest way to check whether your account has adequate permissions is through the portal.</span></span> <span data-ttu-id="27f38-117">Consulte [Verificar permissão necessária no portal](resource-group-create-service-principal-portal.md#required-permissions).</span><span class="sxs-lookup"><span data-stu-id="27f38-117">See [Check required permission in portal](resource-group-create-service-principal-portal.md#required-permissions).</span></span>

<span data-ttu-id="27f38-118">Agora, vá para uma seção para ver uma autenticação da [senha](#create-service-principal-with-password) ou do [certificado](#create-service-principal-with-certificate).</span><span class="sxs-lookup"><span data-stu-id="27f38-118">Now, proceed to a section for either [password](#create-service-principal-with-password) or [certificate](#create-service-principal-with-certificate) authentication.</span></span>

## <a name="create-service-principal-with-password"></a><span data-ttu-id="27f38-119">Criar a entidade de serviço com a senha</span><span class="sxs-lookup"><span data-stu-id="27f38-119">Create service principal with password</span></span>
<span data-ttu-id="27f38-120">Nesta seção, você executará as etapas para criar o aplicativo do AD com uma senha e atribuirá a função Leitor à entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="27f38-120">In this section, you perform the steps to create the AD application with a password, and assign the Reader role to the service principal.</span></span>

1. <span data-ttu-id="27f38-121">Entre na sua conta.</span><span class="sxs-lookup"><span data-stu-id="27f38-121">Sign in to your account.</span></span>
   
   ```azurecli
   azure login
   ```
2. <span data-ttu-id="27f38-122">Para criar uma identidade de aplicativo, forneça o nome do aplicativo e uma senha, conforme mostrado no comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="27f38-122">To create an app identity, provide the name of the app and a password, as shown in the following command:</span></span>
     
   ```azurecli
   azure ad sp create -n exampleapp -p {your-password}
   ```
     
   <span data-ttu-id="27f38-123">A nova entidade de serviço será retornada.</span><span class="sxs-lookup"><span data-stu-id="27f38-123">The new service principal is returned.</span></span> <span data-ttu-id="27f38-124">A ID de objeto é necessária ao conceder permissões.</span><span class="sxs-lookup"><span data-stu-id="27f38-124">The Object Id is needed when granting permissions.</span></span> <span data-ttu-id="27f38-125">O guid listado com os Nomes de Entidade de Serviço é necessário ao fazer logon.</span><span class="sxs-lookup"><span data-stu-id="27f38-125">The guid listed with the Service Principal Names is needed when logging in.</span></span> <span data-ttu-id="27f38-126">Esse guid tem o mesmo valor da ID do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="27f38-126">This guid is the same value as the app id.</span></span> <span data-ttu-id="27f38-127">Em aplicativos de exemplo, esse valor é conhecido como `Client ID`.</span><span class="sxs-lookup"><span data-stu-id="27f38-127">In the sample applications, this value is referred to as the `Client ID`.</span></span> 
     
   ```azurecli
   info:    Executing command ad sp create
     
   Creating application exampleapp
     / Creating service principal for application 7132aca4-1bdb-4238-ad81-996ff91d8db+
     data:    Object Id:               ff863613-e5e2-4a6b-af07-fff6f2de3f4e
     data:    Display Name:            exampleapp
     data:    Service Principal Names:
     data:                             7132aca4-1bdb-4238-ad81-996ff91d8db4
     data:                             https://www.contoso.org/example
     info:    ad sp create command OK
   ```

3. <span data-ttu-id="27f38-128">Conceda à entidade de serviço permissões em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="27f38-128">Grant the service principal permissions on your subscription.</span></span> <span data-ttu-id="27f38-129">Neste exemplo, você adiciona a entidade de serviço à função Leitor , que concede permissão para ler todos os recursos na assinatura.</span><span class="sxs-lookup"><span data-stu-id="27f38-129">In this example, you add the service principal to the Reader role, which grants permission to read all resources in the subscription.</span></span> <span data-ttu-id="27f38-130">Para ver outras funções, confira [RBAC: funções internas](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="27f38-130">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span> <span data-ttu-id="27f38-131">Para obter o parâmetro objectid, forneça o a ID de Objeto que você usou ao criar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="27f38-131">For the objectid parameter, provide the Object Id that you used when creating the application.</span></span> <span data-ttu-id="27f38-132">Antes de executar esse comando, dê um tempo para a nova entidade de serviço se propagar pelo Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="27f38-132">Before running this command, you must allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="27f38-133">Geralmente, ao executar esses comandos manualmente, um tempo suficiente já decorreu entre as tarefas.</span><span class="sxs-lookup"><span data-stu-id="27f38-133">When you run these commands manually, usually enough time has elapsed between tasks.</span></span> <span data-ttu-id="27f38-134">Em um script, adicione uma etapa de espera entre os comandos (como `sleep 15`).</span><span class="sxs-lookup"><span data-stu-id="27f38-134">In a script, you should add a step to sleep between the commands (like `sleep 15`).</span></span> <span data-ttu-id="27f38-135">Se você vir um erro informando que a entidade não existe no diretório, execute o comando novamente.</span><span class="sxs-lookup"><span data-stu-id="27f38-135">If you see an error stating the principal does not exist in the directory, rerun the command.</span></span>
   
   ```azurecli
   azure role assignment create --objectId ff863613-e5e2-4a6b-af07-fff6f2de3f4e -o Reader -c /subscriptions/{subscriptionId}/
   ```
   
<span data-ttu-id="27f38-136">É isso!</span><span class="sxs-lookup"><span data-stu-id="27f38-136">That's it!</span></span> <span data-ttu-id="27f38-137">Seu aplicativo do AD e a entidade de serviço estão configurados.</span><span class="sxs-lookup"><span data-stu-id="27f38-137">Your AD application and service principal are set up.</span></span> <span data-ttu-id="27f38-138">A próxima seção mostra como fazer logon com as credenciais por meio da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="27f38-138">The next section shows you how to log in with the credential through Azure CLI.</span></span> <span data-ttu-id="27f38-139">Se você quiser usar a credencial em seu aplicativo de código, não precisará continuar com este tópico.</span><span class="sxs-lookup"><span data-stu-id="27f38-139">If you want to use the credential in your code application, you do not need to continue with this topic.</span></span> <span data-ttu-id="27f38-140">Pode ir para os [aplicativos de amostra](#sample-applications) para ter exemplos de logon com sua ID do aplicativo e senha.</span><span class="sxs-lookup"><span data-stu-id="27f38-140">You can jump to the [Sample applications](#sample-applications) for examples of logging in with your application id and password.</span></span> 

### <a name="provide-credentials-through-azure-cli"></a><span data-ttu-id="27f38-141">Fornecer credenciais por meio da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="27f38-141">Provide credentials through Azure CLI</span></span>
<span data-ttu-id="27f38-142">Agora, você precisa fazer logon como o aplicativo para executar as operações.</span><span class="sxs-lookup"><span data-stu-id="27f38-142">Now, you need to log in as the application to perform operations.</span></span>

1. <span data-ttu-id="27f38-143">Sempre que você entrar como uma entidade de serviço, precisará fornecer a ID do locatário do diretório para seu aplicativo do AD.</span><span class="sxs-lookup"><span data-stu-id="27f38-143">Whenever you sign in as a service principal, you need to provide the tenant id of the directory for your AD app.</span></span> <span data-ttu-id="27f38-144">Um locatário é uma instância do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="27f38-144">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="27f38-145">Para recuperar a id do locatário para sua assinatura autenticada no momento, use:</span><span class="sxs-lookup"><span data-stu-id="27f38-145">To retrieve the tenant id for your currently authenticated subscription, use:</span></span>
   
   ```azurecli
   azure account show
   ```
   
   <span data-ttu-id="27f38-146">Que retorna:</span><span class="sxs-lookup"><span data-stu-id="27f38-146">Which returns:</span></span>
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
     <span data-ttu-id="27f38-147">Se você precisar obter a id de locatário de outra assinatura, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="27f38-147">If you need to get the tenant id of another subscription, use the following command:</span></span>
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. <span data-ttu-id="27f38-148">Se você precisa recuperar a id de cliente a ser usada para fazer logon, use:</span><span class="sxs-lookup"><span data-stu-id="27f38-148">If you need to retrieve the client id to use for logging in, use:</span></span>
   
   ```azurecli
   azure ad sp show -c exampleapp --json
   ```
   
     <span data-ttu-id="27f38-149">O valor a ser usado para fazer logon é o guid listado nos nomes de entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="27f38-149">The value to use for logging in is the guid listed in the service principal names.</span></span>
   
   ```azurecli
   [
     {
       "objectId": "ff863613-e5e2-4a6b-af07-fff6f2de3f4e",
       "objectType": "ServicePrincipal",
       "displayName": "exampleapp",
       "appId": "7132aca4-1bdb-4238-ad81-996ff91d8db4",
       "servicePrincipalNames": [
         "https://www.contoso.org/example",
         "7132aca4-1bdb-4238-ad81-996ff91d8db4"
       ]
     }
   ]
   ```
3. <span data-ttu-id="27f38-150">Faça logon como a entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="27f38-150">Log in as the service principal.</span></span>
   
   ```azurecli
   azure login -u 7132aca4-1bdb-4238-ad81-996ff91d8db4 --service-principal --tenant {tenant-id}
   ```
   
    <span data-ttu-id="27f38-151">Você receberá uma solicitação de senha.</span><span class="sxs-lookup"><span data-stu-id="27f38-151">You are prompted for the password.</span></span> <span data-ttu-id="27f38-152">Forneça a senha especificada durante a criação do aplicativo do AD.</span><span class="sxs-lookup"><span data-stu-id="27f38-152">Provide the password you specified when creating the AD application.</span></span>
   
   ```azurecli
   info:    Executing command login
   Password: ********
   ```

<span data-ttu-id="27f38-153">Agora, você está autenticado como a entidade de serviço para a entidade criada.</span><span class="sxs-lookup"><span data-stu-id="27f38-153">You are now authenticated as the service principal for the service principal that you created.</span></span>

<span data-ttu-id="27f38-154">Como alternativa, você pode invocar operações REST a partir da linha de comando para fazer logon.</span><span class="sxs-lookup"><span data-stu-id="27f38-154">Alternatively, you can invoke REST operations from the command line to log in.</span></span> <span data-ttu-id="27f38-155">Na resposta de autenticação, você pode recuperar o token de acesso para uso com outras operações.</span><span class="sxs-lookup"><span data-stu-id="27f38-155">From the authentication response, you can retrieve the access token for use with other operations.</span></span> <span data-ttu-id="27f38-156">Para obter um exemplo de como recuperar o token de acesso invocando operações REST, consulte [Gerar um token de acesso](resource-manager-rest-api.md#generating-an-access-token).</span><span class="sxs-lookup"><span data-stu-id="27f38-156">For an example of retrieving the access token by invoking REST operations, see [Generating an Access Token](resource-manager-rest-api.md#generating-an-access-token).</span></span>

## <a name="create-service-principal-with-certificate"></a><span data-ttu-id="27f38-157">Criar a entidade de serviço com o certificado</span><span class="sxs-lookup"><span data-stu-id="27f38-157">Create service principal with certificate</span></span>
<span data-ttu-id="27f38-158">Nesta seção, você deve executar as etapas para:</span><span class="sxs-lookup"><span data-stu-id="27f38-158">In this section, you perform the steps to:</span></span>

* <span data-ttu-id="27f38-159">criar um certificado autoassinado</span><span class="sxs-lookup"><span data-stu-id="27f38-159">create a self-signed certificate</span></span>
* <span data-ttu-id="27f38-160">criar o aplicativo do AD com o certificado e a entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="27f38-160">create the AD application with the certificate, and the service principal</span></span>
* <span data-ttu-id="27f38-161">atribuir a função Leitor à entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="27f38-161">assign the Reader role to the service principal</span></span>

<span data-ttu-id="27f38-162">Para concluir essas etapas, você deve ter o [OpenSSL](http://www.openssl.org/) instalado.</span><span class="sxs-lookup"><span data-stu-id="27f38-162">To complete these steps, you must have [OpenSSL](http://www.openssl.org/) installed.</span></span>

1. <span data-ttu-id="27f38-163">Crie um certificado autoassinado.</span><span class="sxs-lookup"><span data-stu-id="27f38-163">Create a self-signed certificate.</span></span>
   
   ```
   openssl req -x509 -days 3650 -newkey rsa:2048 -out cert.pem -nodes -subj '/CN=exampleapp'
   ```

2. <span data-ttu-id="27f38-164">A etapa anterior criou dois arquivos – privkey.pem e cert.pem.</span><span class="sxs-lookup"><span data-stu-id="27f38-164">The preceding step created two files - privkey.pem and cert.pem.</span></span> <span data-ttu-id="27f38-165">Combine as chaves pública e privada em um único arquivo.</span><span class="sxs-lookup"><span data-stu-id="27f38-165">Combine the public and private keys into a single file.</span></span>

   ```
   cat privkey.pem cert.pem > examplecert.pem
   ```

3. <span data-ttu-id="27f38-166">Abra o arquivo **examplecert.pem** e procure a longa sequência de caracteres entre **-----BEGIN CERTIFICATE-----** e **-----END CERTIFICATE-----**.</span><span class="sxs-lookup"><span data-stu-id="27f38-166">Open the **examplecert.pem** file and look for the long sequence of characters between **-----BEGIN CERTIFICATE-----** and **-----END CERTIFICATE-----**.</span></span> <span data-ttu-id="27f38-167">Copie os dados do certificado.</span><span class="sxs-lookup"><span data-stu-id="27f38-167">Copy the certificate data.</span></span> <span data-ttu-id="27f38-168">Você pode passar esses dados como um parâmetro ao criar a entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="27f38-168">You pass this data as a parameter when creating the service principal.</span></span>

4. <span data-ttu-id="27f38-169">Entre na sua conta.</span><span class="sxs-lookup"><span data-stu-id="27f38-169">Sign in to your account.</span></span>

   ```azurecli
   azure login
   ```
5. <span data-ttu-id="27f38-170">Para criar a entidade de serviço, forneça o nome do aplicativo e os dados do certificado, conforme mostrado no seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="27f38-170">To create the service principal, provide the name of the app and the certificate data, as shown in the following command:</span></span>
     
   ```azurecli
   azure ad sp create -n exampleapp --cert-value {certificate data}
   ```
     
   <span data-ttu-id="27f38-171">A nova entidade de serviço será retornada.</span><span class="sxs-lookup"><span data-stu-id="27f38-171">The new service principal is returned.</span></span> <span data-ttu-id="27f38-172">A ID de objeto é necessária ao conceder permissões.</span><span class="sxs-lookup"><span data-stu-id="27f38-172">The Object Id is needed when granting permissions.</span></span> <span data-ttu-id="27f38-173">O guid listado com os Nomes de Entidade de Serviço é necessário ao fazer logon.</span><span class="sxs-lookup"><span data-stu-id="27f38-173">The guid listed with the Service Principal Names is needed when logging in.</span></span> <span data-ttu-id="27f38-174">Esse guid tem o mesmo valor da ID do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="27f38-174">This guid is the same value as the app id.</span></span> <span data-ttu-id="27f38-175">Em aplicativos de exemplo, esse valor é conhecido como a ID do Cliente.</span><span class="sxs-lookup"><span data-stu-id="27f38-175">In the sample applications, this value is referred to as the Client ID.</span></span> 
     
   ```azurecli
   info:    Executing command ad sp create
     
   Creating service principal for application 4fd39843-c338-417d-b549-a545f584a74+
     data:    Object Id:        7dbc8265-51ed-4038-8e13-31948c7f4ce7
     data:    Display Name:     exampleapp
     data:    Service Principal Names:
     data:                      4fd39843-c338-417d-b549-a545f584a745
     data:                      https://www.contoso.org/example
     info:    ad sp create command OK
   ```
6. <span data-ttu-id="27f38-176">Conceda à entidade de serviço permissões em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="27f38-176">Grant the service principal permissions on your subscription.</span></span> <span data-ttu-id="27f38-177">Neste exemplo, você adiciona a entidade de serviço à função Leitor , que concede permissão para ler todos os recursos na assinatura.</span><span class="sxs-lookup"><span data-stu-id="27f38-177">In this example, you add the service principal to the Reader role, which grants permission to read all resources in the subscription.</span></span> <span data-ttu-id="27f38-178">Para ver outras funções, confira [RBAC: funções internas](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="27f38-178">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span> <span data-ttu-id="27f38-179">Para obter o parâmetro objectid, forneça o a ID de Objeto que você usou ao criar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="27f38-179">For the objectid parameter, provide the Object Id that you used when creating the application.</span></span> <span data-ttu-id="27f38-180">Antes de executar esse comando, dê um tempo para a nova entidade de serviço se propagar pelo Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="27f38-180">Before running this command, you must allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="27f38-181">Geralmente, ao executar esses comandos manualmente, um tempo suficiente já decorreu entre as tarefas.</span><span class="sxs-lookup"><span data-stu-id="27f38-181">When you run these commands manually, usually enough time has elapsed between tasks.</span></span> <span data-ttu-id="27f38-182">Em um script, adicione uma etapa de espera entre os comandos (como `sleep 15`).</span><span class="sxs-lookup"><span data-stu-id="27f38-182">In a script, you should add a step to sleep between the commands (like `sleep 15`).</span></span> <span data-ttu-id="27f38-183">Se você vir um erro informando que a entidade não existe no diretório, execute o comando novamente.</span><span class="sxs-lookup"><span data-stu-id="27f38-183">If you see an error stating the principal does not exist in the directory, rerun the command.</span></span>
   
   ```azurecli
   azure role assignment create --objectId 7dbc8265-51ed-4038-8e13-31948c7f4ce7 -o Reader -c /subscriptions/{subscriptionId}/
   ```
  
### <a name="provide-certificate-through-automated-azure-cli-script"></a><span data-ttu-id="27f38-184">Fornecer certificado por meio do script CLI do Azure automatizado</span><span class="sxs-lookup"><span data-stu-id="27f38-184">Provide certificate through automated Azure CLI script</span></span>
<span data-ttu-id="27f38-185">Agora, você precisa fazer logon como o aplicativo para executar as operações.</span><span class="sxs-lookup"><span data-stu-id="27f38-185">Now, you need to log in as the application to perform operations.</span></span>

1. <span data-ttu-id="27f38-186">Sempre que você entrar como uma entidade de serviço, precisará fornecer a ID do locatário do diretório para seu aplicativo do AD.</span><span class="sxs-lookup"><span data-stu-id="27f38-186">Whenever you sign in as a service principal, you need to provide the tenant id of the directory for your AD app.</span></span> <span data-ttu-id="27f38-187">Um locatário é uma instância do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="27f38-187">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="27f38-188">Para recuperar a id do locatário para sua assinatura autenticada no momento, use:</span><span class="sxs-lookup"><span data-stu-id="27f38-188">To retrieve the tenant id for your currently authenticated subscription, use:</span></span>
   
   ```azurecli
   azure account show
   ```
   
   <span data-ttu-id="27f38-189">Que retorna:</span><span class="sxs-lookup"><span data-stu-id="27f38-189">Which returns:</span></span>
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
   <span data-ttu-id="27f38-190">Se você precisar obter a id de locatário de outra assinatura, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="27f38-190">If you need to get the tenant id of another subscription, use the following command:</span></span>
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. <span data-ttu-id="27f38-191">Para recuperar a impressão digital do certificado e remover os caracteres desnecessários, use:</span><span class="sxs-lookup"><span data-stu-id="27f38-191">To retrieve the certificate thumbprint and remove unneeded characters, use:</span></span>
   
   ```
   openssl x509 -in "C:\certificates\examplecert.pem" -fingerprint -noout | sed 's/SHA1 Fingerprint=//g'  | sed 's/://g'
   ```
   
   <span data-ttu-id="27f38-192">Que retorna um valor de impressão digital semelhante a:</span><span class="sxs-lookup"><span data-stu-id="27f38-192">Which returns a thumbprint value similar to:</span></span>
   
   ```
   30996D9CE48A0B6E0CD49DBB9A48059BF9355851
   ```
3. <span data-ttu-id="27f38-193">Se você precisa recuperar a id de cliente a ser usada para fazer logon, use:</span><span class="sxs-lookup"><span data-stu-id="27f38-193">If you need to retrieve the client id to use for logging in, use:</span></span>
   
   ```azurecli
   azure ad sp show -c exampleapp
   ```
   
   <span data-ttu-id="27f38-194">O valor a ser usado para fazer logon é o guid listado nos nomes de entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="27f38-194">The value to use for logging in is the guid listed in the service principal names.</span></span>
     
   ```azurecli
   [
     {
       "objectId": "7dbc8265-51ed-4038-8e13-31948c7f4ce7",
       "objectType": "ServicePrincipal",
       "displayName": "exampleapp",
       "appId": "4fd39843-c338-417d-b549-a545f584a745",
       "servicePrincipalNames": [
         "https://www.contoso.org/example",
         "4fd39843-c338-417d-b549-a545f584a745"
       ]
     }
   ]
   ```
4. <span data-ttu-id="27f38-195">Faça logon como a entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="27f38-195">Log in as the service principal.</span></span>
   
   ```azurecli
   azure login --service-principal --tenant {tenant-id} -u 4fd39843-c338-417d-b549-a545f584a745 --certificate-file C:\certificates\examplecert.pem --thumbprint {thumbprint}
   ```

<span data-ttu-id="27f38-196">Agora, você já deve ser autenticado como a entidade de serviço do aplicativo do Active Directory do Azure criado.</span><span class="sxs-lookup"><span data-stu-id="27f38-196">You are now authenticated as the service principal for the Azure Active Directory application that you created.</span></span>

## <a name="change-credentials"></a><span data-ttu-id="27f38-197">Alterar credenciais</span><span class="sxs-lookup"><span data-stu-id="27f38-197">Change credentials</span></span>

<span data-ttu-id="27f38-198">Para alterar as credenciais para um aplicativo do AD, por causa de uma violação de segurança ou expiração de credencial, use `azure ad app set`.</span><span class="sxs-lookup"><span data-stu-id="27f38-198">To change the credentials for an AD app, either because of a security compromise or a credential expiration, use `azure ad app set`.</span></span>

<span data-ttu-id="27f38-199">Para alterar uma senha, use:</span><span class="sxs-lookup"><span data-stu-id="27f38-199">To change a password, use:</span></span>

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --password p@ssword
```

<span data-ttu-id="27f38-200">Para alterar um valor de certificado, use:</span><span class="sxs-lookup"><span data-stu-id="27f38-200">To change a certificate value, use:</span></span>

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --cert-value {certificate data}
```

## <a name="debug"></a><span data-ttu-id="27f38-201">Depurar</span><span class="sxs-lookup"><span data-stu-id="27f38-201">Debug</span></span>

<span data-ttu-id="27f38-202">Você pode receber os seguintes erros ao criar uma entidade de serviço:</span><span class="sxs-lookup"><span data-stu-id="27f38-202">You may encounter the following errors when creating a service principal:</span></span>

* <span data-ttu-id="27f38-203">**"Authentication_Unauthorized"** ou **"Nenhuma assinatura encontrada no contexto".**</span><span class="sxs-lookup"><span data-stu-id="27f38-203">**"Authentication_Unauthorized"** or **"No subscription found in the context."**</span></span> <span data-ttu-id="27f38-204">– Você verá esse erro quando sua conta não tiver as [permissões necessárias](#required-permissions) no Active Directory do Azure para registrar um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="27f38-204">- You see this error when your account does not have the [required permissions](#required-permissions) on the Azure Active Directory to register an app.</span></span> <span data-ttu-id="27f38-205">Normalmente, você verá esse erro somente quando os usuários administradores no Active Directory do Azure puderem registrar aplicativos e sua conta não for um administrador.</span><span class="sxs-lookup"><span data-stu-id="27f38-205">Typically, you see this error when only admin users in your Azure Active Directory can register apps, and your account is not an admin.</span></span> <span data-ttu-id="27f38-206">Solicite ao administrador para lhe atribuir uma função de administrador ou para permitir que os usuários registrem aplicativos.</span><span class="sxs-lookup"><span data-stu-id="27f38-206">Ask your administrator to either assign you to an administrator role, or to enable users to register apps.</span></span>

* <span data-ttu-id="27f38-207">Sua conta **"não tem autorização para executar a ação 'Microsoft.Authorization/roleAssignments/write' no escopo '/subscriptions/{guid}'".**  – Você verá esse erro quando sua conta não tiver permissões suficientes para atribuir uma função a uma identidade.</span><span class="sxs-lookup"><span data-stu-id="27f38-207">Your account **"does not have authorization to perform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/{guid}'."** - You see this error when your account does not have sufficient permissions to assign a role to an identity.</span></span> <span data-ttu-id="27f38-208">Solicite ao administrador da assinatura para adicioná-lo à função Administrador de Acesso do Usuário.</span><span class="sxs-lookup"><span data-stu-id="27f38-208">Ask your subscription administrator to add you to User Access Administrator role.</span></span>

## <a name="sample-applications"></a><span data-ttu-id="27f38-209">Aplicativos de exemplo</span><span class="sxs-lookup"><span data-stu-id="27f38-209">Sample applications</span></span>
<span data-ttu-id="27f38-210">Para obter informações sobre como fazer logon no aplicativo por meio de diferentes plataformas, consulte:</span><span class="sxs-lookup"><span data-stu-id="27f38-210">For information about logging in as the application through different platforms, see:</span></span>

* [<span data-ttu-id="27f38-211">.NET</span><span class="sxs-lookup"><span data-stu-id="27f38-211">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="27f38-212">Java</span><span class="sxs-lookup"><span data-stu-id="27f38-212">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="27f38-213">Node.js</span><span class="sxs-lookup"><span data-stu-id="27f38-213">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="27f38-214">Python</span><span class="sxs-lookup"><span data-stu-id="27f38-214">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="27f38-215">Ruby</span><span class="sxs-lookup"><span data-stu-id="27f38-215">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a><span data-ttu-id="27f38-216">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="27f38-216">Next steps</span></span>
* <span data-ttu-id="27f38-217">Para ver as etapas detalhadas sobre como integrar um aplicativo no Azure para gerenciar os recursos, consulte [Guia do desenvolvedor para a autorização com a API do Azure Resource Manager](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="27f38-217">For detailed steps on integrating an application into Azure for managing resources, see [Developer's guide to authorization with the Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="27f38-218">Para obter mais informações sobre como usar os certificados e a CLI do Azure, consulte [Autenticação baseada em certificados com as Entidades de Serviço do Azure a partir da linha de comando do Linux](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx).</span><span class="sxs-lookup"><span data-stu-id="27f38-218">To get more information about using certificates and Azure CLI, see [Certificate-based authentication with Azure Service Principals from Linux command line](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx).</span></span> 
* <span data-ttu-id="27f38-219">Para obter uma lista de ações disponíveis que podem ser concedidas ou negadas a usuários, consulte [Operações do Provedor de Recursos do Azure Resource Manager](../active-directory/role-based-access-control-resource-provider-operations.md).</span><span class="sxs-lookup"><span data-stu-id="27f38-219">For a list of available actions that can be granted or denied to users, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>
