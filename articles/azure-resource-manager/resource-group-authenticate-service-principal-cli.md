---
title: aaaCreate identidade para o aplicativo do Azure com a CLI do Azure | Microsoft Docs
description: "Descreve como controlam a CLI do Azure de toouse toocreate um aplicativo do Active Directory do Azure e entidade de serviço e conceder acesso a tooresources por meio de acesso baseado em função. Ele mostra como tooauthenticate aplicativo com uma senha ou certificado."
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
ms.openlocfilehash: 0d693ec801d4f4d6c24ec420580776e73014b325
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-cli-toocreate-a-service-principal-tooaccess-resources"></a><span data-ttu-id="7e7ec-104">Usar um serviço principal tooaccess recursos de toocreate CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="7e7ec-104">Use Azure CLI toocreate a service principal tooaccess resources</span></span>

<span data-ttu-id="7e7ec-105">Quando você tiver um aplicativo ou script que precisa de recursos de tooaccess, você pode configurar uma identidade para o aplicativo hello e autenticar o aplicativo hello com suas próprias credenciais.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-105">When you have an app or script that needs tooaccess resources, you can set up an identity for hello app and authenticate hello app with its own credentials.</span></span> <span data-ttu-id="7e7ec-106">Essa identidade é conhecida como uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-106">This identity is known as a service principal.</span></span> <span data-ttu-id="7e7ec-107">Essa abordagem permite:</span><span class="sxs-lookup"><span data-stu-id="7e7ec-107">This approach enables you to:</span></span>

* <span data-ttu-id="7e7ec-108">Atribua permissões de identidade de aplicativo toohello que são diferentes de suas próprias permissões.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-108">Assign permissions toohello app identity that are different than your own permissions.</span></span> <span data-ttu-id="7e7ec-109">Normalmente, essas permissões são restrito tooexactly toodo precisa de qual aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-109">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span>
* <span data-ttu-id="7e7ec-110">Use um certificado para a autenticação ao executar um script autônomo.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-110">Use a certificate for authentication when executing an unattended script.</span></span>

<span data-ttu-id="7e7ec-111">Este artigo mostra como toouse [Azure CLI 1.0](../cli-install-nodejs.md) tooset backup toorun um aplicativo em suas próprias credenciais e identidade.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-111">This article shows you how toouse [Azure CLI 1.0](../cli-install-nodejs.md) tooset up an application toorun under its own credentials and identity.</span></span> <span data-ttu-id="7e7ec-112">Instalar a versão mais recente de saudação do [Azure CLI 1.0](../cli-install-nodejs.md) toomake se seu ambiente corresponde exemplos Olá neste artigo.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-112">Install hello latest version of [Azure CLI 1.0](../cli-install-nodejs.md) toomake sure your environment matches hello examples in this article.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="7e7ec-113">Permissões necessárias</span><span class="sxs-lookup"><span data-stu-id="7e7ec-113">Required permissions</span></span>
<span data-ttu-id="7e7ec-114">toocomplete neste tópico, você deve ter permissões suficientes no Active Directory do Azure e sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-114">toocomplete this topic, you must have sufficient permissions in both your Azure Active Directory and your Azure subscription.</span></span> <span data-ttu-id="7e7ec-115">Especificamente, você deve ser capaz de toocreate um aplicativo de saudação do Active Directory do Azure e atribuir função de tooa principal do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-115">Specifically, you must be able toocreate an app in hello Azure Active Directory, and assign hello service principal tooa role.</span></span> 

<span data-ttu-id="7e7ec-116">Olá mais fácil toocheck de maneira se sua conta tem permissões suficientes é por meio do portal hello.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-116">hello easiest way toocheck whether your account has adequate permissions is through hello portal.</span></span> <span data-ttu-id="7e7ec-117">Consulte [Verificar permissão necessária no portal](resource-group-create-service-principal-portal.md#required-permissions).</span><span class="sxs-lookup"><span data-stu-id="7e7ec-117">See [Check required permission in portal](resource-group-create-service-principal-portal.md#required-permissions).</span></span>

<span data-ttu-id="7e7ec-118">Agora, continuar tooa seção devido a um [senha](#create-service-principal-with-password) ou [certificado](#create-service-principal-with-certificate) autenticação.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-118">Now, proceed tooa section for either [password](#create-service-principal-with-password) or [certificate](#create-service-principal-with-certificate) authentication.</span></span>

## <a name="create-service-principal-with-password"></a><span data-ttu-id="7e7ec-119">Criar a entidade de serviço com a senha</span><span class="sxs-lookup"><span data-stu-id="7e7ec-119">Create service principal with password</span></span>
<span data-ttu-id="7e7ec-120">Nesta seção, execute Olá etapas toocreate Olá aplicativo AD com uma senha e atribuir a entidade de serviço Olá leitor função toohello.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-120">In this section, you perform hello steps toocreate hello AD application with a password, and assign hello Reader role toohello service principal.</span></span>

1. <span data-ttu-id="7e7ec-121">Entre na conta de tooyour.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-121">Sign in tooyour account.</span></span>
   
   ```azurecli
   azure login
   ```
2. <span data-ttu-id="7e7ec-122">toocreate uma identidade de aplicativo, forneça Olá nome do aplicativo hello e uma senha, conforme mostrado na Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7e7ec-122">toocreate an app identity, provide hello name of hello app and a password, as shown in hello following command:</span></span>
     
   ```azurecli
   azure ad sp create -n exampleapp -p {your-password}
   ```
     
   <span data-ttu-id="7e7ec-123">entidade de serviço novo Olá é retornado.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-123">hello new service principal is returned.</span></span> <span data-ttu-id="7e7ec-124">Olá Id de objeto é necessária quando a concessão de permissões.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-124">hello Object Id is needed when granting permissions.</span></span> <span data-ttu-id="7e7ec-125">Olá guid listado com hello nomes da entidade de serviço é necessária durante o logon.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-125">hello guid listed with hello Service Principal Names is needed when logging in.</span></span> <span data-ttu-id="7e7ec-126">Esse guid é hello mesmo valor de id do aplicativo hello. Em aplicativos de exemplo hello, esse valor é chamado tooas Olá `Client ID`.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-126">This guid is hello same value as hello app id. In hello sample applications, this value is referred tooas hello `Client ID`.</span></span> 
     
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

3. <span data-ttu-id="7e7ec-127">Conceder permissões de principal de serviço Olá em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-127">Grant hello service principal permissions on your subscription.</span></span> <span data-ttu-id="7e7ec-128">Neste exemplo, você deve adicionar função Leitor do hello serviço toohello principal, que concede permissão tooread todos os recursos na assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-128">In this example, you add hello service principal toohello Reader role, which grants permission tooread all resources in hello subscription.</span></span> <span data-ttu-id="7e7ec-129">Para ver outras funções, confira [RBAC: funções internas](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="7e7ec-129">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span> <span data-ttu-id="7e7ec-130">Para o parâmetro objectid Olá fornecem Olá Id de objeto que você usou ao criar o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-130">For hello objectid parameter, provide hello Object Id that you used when creating hello application.</span></span> <span data-ttu-id="7e7ec-131">Antes de executar esse comando, você deve permitir algum tempo para Olá novo serviço principal toopropagate em todo o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-131">Before running this command, you must allow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="7e7ec-132">Geralmente, ao executar esses comandos manualmente, um tempo suficiente já decorreu entre as tarefas.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-132">When you run these commands manually, usually enough time has elapsed between tasks.</span></span> <span data-ttu-id="7e7ec-133">Em um script, você deve adicionar um toosleep etapa entre comandos hello (como `sleep 15`).</span><span class="sxs-lookup"><span data-stu-id="7e7ec-133">In a script, you should add a step toosleep between hello commands (like `sleep 15`).</span></span> <span data-ttu-id="7e7ec-134">Se você vir que uma saudação de erro informando principal não existe no diretório hello, execute novamente o comando de saudação.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-134">If you see an error stating hello principal does not exist in hello directory, rerun hello command.</span></span>
   
   ```azurecli
   azure role assignment create --objectId ff863613-e5e2-4a6b-af07-fff6f2de3f4e -o Reader -c /subscriptions/{subscriptionId}/
   ```
   
<span data-ttu-id="7e7ec-135">É isso!</span><span class="sxs-lookup"><span data-stu-id="7e7ec-135">That's it!</span></span> <span data-ttu-id="7e7ec-136">Seu aplicativo do AD e a entidade de serviço estão configurados.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-136">Your AD application and service principal are set up.</span></span> <span data-ttu-id="7e7ec-137">Olá próxima seção mostra como toolog com hello as credenciais por meio da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-137">hello next section shows you how toolog in with hello credential through Azure CLI.</span></span> <span data-ttu-id="7e7ec-138">Se você quiser credencial de saudação toouse em seu aplicativo de código, não é necessário toocontinue neste tópico.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-138">If you want toouse hello credential in your code application, you do not need toocontinue with this topic.</span></span> <span data-ttu-id="7e7ec-139">Você pode ir toohello [aplicativos de exemplo](#sample-applications) para obter exemplos de registro em log com a id de aplicativo e a senha.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-139">You can jump toohello [Sample applications](#sample-applications) for examples of logging in with your application id and password.</span></span> 

### <a name="provide-credentials-through-azure-cli"></a><span data-ttu-id="7e7ec-140">Fornecer credenciais por meio da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="7e7ec-140">Provide credentials through Azure CLI</span></span>
<span data-ttu-id="7e7ec-141">Agora, você precisa toolog em operações de tooperform aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-141">Now, you need toolog in as hello application tooperform operations.</span></span>

1. <span data-ttu-id="7e7ec-142">Sempre que você entrar como uma entidade de serviço, você precisa tooprovide id de locatário de saudação do diretório de saudação para seu aplicativo do AD.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-142">Whenever you sign in as a service principal, you need tooprovide hello tenant id of hello directory for your AD app.</span></span> <span data-ttu-id="7e7ec-143">Um locatário é uma instância do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-143">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="7e7ec-144">id de locatário tooretrieve Olá para sua assinatura autenticada no momento, use:</span><span class="sxs-lookup"><span data-stu-id="7e7ec-144">tooretrieve hello tenant id for your currently authenticated subscription, use:</span></span>
   
   ```azurecli
   azure account show
   ```
   
   <span data-ttu-id="7e7ec-145">Que retorna:</span><span class="sxs-lookup"><span data-stu-id="7e7ec-145">Which returns:</span></span>
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
     <span data-ttu-id="7e7ec-146">Se você precisar de id de locatário Olá tooget de outra assinatura, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7e7ec-146">If you need tooget hello tenant id of another subscription, use hello following command:</span></span>
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. <span data-ttu-id="7e7ec-147">Se você precisar tooretrieve Olá cliente id toouse para fazer logon, use:</span><span class="sxs-lookup"><span data-stu-id="7e7ec-147">If you need tooretrieve hello client id toouse for logging in, use:</span></span>
   
   ```azurecli
   azure ad sp show -c exampleapp --json
   ```
   
     <span data-ttu-id="7e7ec-148">Olá valor toouse para log em é o guid de saudação listado em nomes de entidade de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-148">hello value toouse for logging in is hello guid listed in hello service principal names.</span></span>
   
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
3. <span data-ttu-id="7e7ec-149">Faça logon como entidade de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-149">Log in as hello service principal.</span></span>
   
   ```azurecli
   azure login -u 7132aca4-1bdb-4238-ad81-996ff91d8db4 --service-principal --tenant {tenant-id}
   ```
   
    <span data-ttu-id="7e7ec-150">Você será solicitado a senha hello.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-150">You are prompted for hello password.</span></span> <span data-ttu-id="7e7ec-151">Forneça a senha de saudação que você especificou ao criar o aplicativo hello AD.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-151">Provide hello password you specified when creating hello AD application.</span></span>
   
   ```azurecli
   info:    Executing command login
   Password: ********
   ```

<span data-ttu-id="7e7ec-152">Agora você está autenticado como entidade de serviço Olá Olá entidade de serviço que você criou.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-152">You are now authenticated as hello service principal for hello service principal that you created.</span></span>

<span data-ttu-id="7e7ec-153">Como alternativa, você pode chamar operações REST do hello toolog de linha de comando no.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-153">Alternatively, you can invoke REST operations from hello command line toolog in.</span></span> <span data-ttu-id="7e7ec-154">De resposta de autenticação hello, você pode recuperar o token de acesso de saudação para uso com outras operações.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-154">From hello authentication response, you can retrieve hello access token for use with other operations.</span></span> <span data-ttu-id="7e7ec-155">Para obter um exemplo de recuperar o token de acesso de saudação ao chamar operações REST, consulte [gerar um Token de acesso](resource-manager-rest-api.md#generating-an-access-token).</span><span class="sxs-lookup"><span data-stu-id="7e7ec-155">For an example of retrieving hello access token by invoking REST operations, see [Generating an Access Token](resource-manager-rest-api.md#generating-an-access-token).</span></span>

## <a name="create-service-principal-with-certificate"></a><span data-ttu-id="7e7ec-156">Criar a entidade de serviço com o certificado</span><span class="sxs-lookup"><span data-stu-id="7e7ec-156">Create service principal with certificate</span></span>
<span data-ttu-id="7e7ec-157">Nesta seção, você deve executar etapas Olá para:</span><span class="sxs-lookup"><span data-stu-id="7e7ec-157">In this section, you perform hello steps to:</span></span>

* <span data-ttu-id="7e7ec-158">criar um certificado autoassinado</span><span class="sxs-lookup"><span data-stu-id="7e7ec-158">create a self-signed certificate</span></span>
* <span data-ttu-id="7e7ec-159">Criar hello aplicativo AD com certificado hello e entidade de serviço Olá</span><span class="sxs-lookup"><span data-stu-id="7e7ec-159">create hello AD application with hello certificate, and hello service principal</span></span>
* <span data-ttu-id="7e7ec-160">atribuir a entidade de serviço Olá leitor função toohello</span><span class="sxs-lookup"><span data-stu-id="7e7ec-160">assign hello Reader role toohello service principal</span></span>

<span data-ttu-id="7e7ec-161">toocomplete essas etapas, você deve ter [OpenSSL](http://www.openssl.org/) instalado.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-161">toocomplete these steps, you must have [OpenSSL](http://www.openssl.org/) installed.</span></span>

1. <span data-ttu-id="7e7ec-162">Crie um certificado autoassinado.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-162">Create a self-signed certificate.</span></span>
   
   ```
   openssl req -x509 -days 3650 -newkey rsa:2048 -out cert.pem -nodes -subj '/CN=exampleapp'
   ```

2. <span data-ttu-id="7e7ec-163">Olá anterior etapa criado dois arquivos - privkey.pem e cert.pem.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-163">hello preceding step created two files - privkey.pem and cert.pem.</span></span> <span data-ttu-id="7e7ec-164">Combine as chaves públicas e privadas Olá em um único arquivo.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-164">Combine hello public and private keys into a single file.</span></span>

   ```
   cat privkey.pem cert.pem > examplecert.pem
   ```

3. <span data-ttu-id="7e7ec-165">Olá abrir **examplecert.pem** de arquivo e procure a sequência longa de saudação de caracteres entre **---iniciar certificado---** e **---concluir certificado---**.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-165">Open hello **examplecert.pem** file and look for hello long sequence of characters between **-----BEGIN CERTIFICATE-----** and **-----END CERTIFICATE-----**.</span></span> <span data-ttu-id="7e7ec-166">Copie dados do certificado hello.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-166">Copy hello certificate data.</span></span> <span data-ttu-id="7e7ec-167">Você pode passar esses dados como um parâmetro ao criar hello entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-167">You pass this data as a parameter when creating hello service principal.</span></span>

4. <span data-ttu-id="7e7ec-168">Entre na conta de tooyour.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-168">Sign in tooyour account.</span></span>

   ```azurecli
   azure login
   ```
5. <span data-ttu-id="7e7ec-169">entidade de serviço do toocreate Olá, fornece nome de saudação do aplicativo hello e dados do certificado Olá, conforme mostrado no comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="7e7ec-169">toocreate hello service principal, provide hello name of hello app and hello certificate data, as shown in hello following command:</span></span>
     
   ```azurecli
   azure ad sp create -n exampleapp --cert-value {certificate data}
   ```
     
   <span data-ttu-id="7e7ec-170">entidade de serviço novo Olá é retornado.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-170">hello new service principal is returned.</span></span> <span data-ttu-id="7e7ec-171">Olá Id de objeto é necessária quando a concessão de permissões.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-171">hello Object Id is needed when granting permissions.</span></span> <span data-ttu-id="7e7ec-172">Olá guid listado com hello nomes da entidade de serviço é necessária durante o logon.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-172">hello guid listed with hello Service Principal Names is needed when logging in.</span></span> <span data-ttu-id="7e7ec-173">Esse guid é hello mesmo valor de id do aplicativo hello. Em aplicativos de exemplo hello, esse valor é chamado tooas Olá ID do cliente.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-173">This guid is hello same value as hello app id. In hello sample applications, this value is referred tooas hello Client ID.</span></span> 
     
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
6. <span data-ttu-id="7e7ec-174">Conceder permissões de principal de serviço Olá em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-174">Grant hello service principal permissions on your subscription.</span></span> <span data-ttu-id="7e7ec-175">Neste exemplo, você deve adicionar função Leitor do hello serviço toohello principal, que concede permissão tooread todos os recursos na assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-175">In this example, you add hello service principal toohello Reader role, which grants permission tooread all resources in hello subscription.</span></span> <span data-ttu-id="7e7ec-176">Para ver outras funções, confira [RBAC: funções internas](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="7e7ec-176">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span> <span data-ttu-id="7e7ec-177">Para o parâmetro objectid Olá fornecem Olá Id de objeto que você usou ao criar o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-177">For hello objectid parameter, provide hello Object Id that you used when creating hello application.</span></span> <span data-ttu-id="7e7ec-178">Antes de executar esse comando, você deve permitir algum tempo para Olá novo serviço principal toopropagate em todo o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-178">Before running this command, you must allow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="7e7ec-179">Geralmente, ao executar esses comandos manualmente, um tempo suficiente já decorreu entre as tarefas.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-179">When you run these commands manually, usually enough time has elapsed between tasks.</span></span> <span data-ttu-id="7e7ec-180">Em um script, você deve adicionar um toosleep etapa entre comandos hello (como `sleep 15`).</span><span class="sxs-lookup"><span data-stu-id="7e7ec-180">In a script, you should add a step toosleep between hello commands (like `sleep 15`).</span></span> <span data-ttu-id="7e7ec-181">Se você vir que uma saudação de erro informando principal não existe no diretório hello, execute novamente o comando de saudação.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-181">If you see an error stating hello principal does not exist in hello directory, rerun hello command.</span></span>
   
   ```azurecli
   azure role assignment create --objectId 7dbc8265-51ed-4038-8e13-31948c7f4ce7 -o Reader -c /subscriptions/{subscriptionId}/
   ```
  
### <a name="provide-certificate-through-automated-azure-cli-script"></a><span data-ttu-id="7e7ec-182">Fornecer certificado por meio do script CLI do Azure automatizado</span><span class="sxs-lookup"><span data-stu-id="7e7ec-182">Provide certificate through automated Azure CLI script</span></span>
<span data-ttu-id="7e7ec-183">Agora, você precisa toolog em operações de tooperform aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-183">Now, you need toolog in as hello application tooperform operations.</span></span>

1. <span data-ttu-id="7e7ec-184">Sempre que você entrar como uma entidade de serviço, você precisa tooprovide id de locatário de saudação do diretório de saudação para seu aplicativo do AD.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-184">Whenever you sign in as a service principal, you need tooprovide hello tenant id of hello directory for your AD app.</span></span> <span data-ttu-id="7e7ec-185">Um locatário é uma instância do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-185">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="7e7ec-186">id de locatário tooretrieve Olá para sua assinatura autenticada no momento, use:</span><span class="sxs-lookup"><span data-stu-id="7e7ec-186">tooretrieve hello tenant id for your currently authenticated subscription, use:</span></span>
   
   ```azurecli
   azure account show
   ```
   
   <span data-ttu-id="7e7ec-187">Que retorna:</span><span class="sxs-lookup"><span data-stu-id="7e7ec-187">Which returns:</span></span>
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
   <span data-ttu-id="7e7ec-188">Se você precisar de id de locatário Olá tooget de outra assinatura, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7e7ec-188">If you need tooget hello tenant id of another subscription, use hello following command:</span></span>
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. <span data-ttu-id="7e7ec-189">tooretrieve Olá a impressão digital do certificado e remova os caracteres desnecessários, use:</span><span class="sxs-lookup"><span data-stu-id="7e7ec-189">tooretrieve hello certificate thumbprint and remove unneeded characters, use:</span></span>
   
   ```
   openssl x509 -in "C:\certificates\examplecert.pem" -fingerprint -noout | sed 's/SHA1 Fingerprint=//g'  | sed 's/://g'
   ```
   
   <span data-ttu-id="7e7ec-190">Que retorna um valor de impressão digital semelhante a:</span><span class="sxs-lookup"><span data-stu-id="7e7ec-190">Which returns a thumbprint value similar to:</span></span>
   
   ```
   30996D9CE48A0B6E0CD49DBB9A48059BF9355851
   ```
3. <span data-ttu-id="7e7ec-191">Se você precisar tooretrieve Olá cliente id toouse para fazer logon, use:</span><span class="sxs-lookup"><span data-stu-id="7e7ec-191">If you need tooretrieve hello client id toouse for logging in, use:</span></span>
   
   ```azurecli
   azure ad sp show -c exampleapp
   ```
   
   <span data-ttu-id="7e7ec-192">Olá valor toouse para log em é o guid de saudação listado em nomes de entidade de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-192">hello value toouse for logging in is hello guid listed in hello service principal names.</span></span>
     
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
4. <span data-ttu-id="7e7ec-193">Faça logon como entidade de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-193">Log in as hello service principal.</span></span>
   
   ```azurecli
   azure login --service-principal --tenant {tenant-id} -u 4fd39843-c338-417d-b549-a545f584a745 --certificate-file C:\certificates\examplecert.pem --thumbprint {thumbprint}
   ```

<span data-ttu-id="7e7ec-194">Agora você está autenticado como entidade de serviço Olá para Olá aplicativo do Active Directory do Azure que você criou.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-194">You are now authenticated as hello service principal for hello Azure Active Directory application that you created.</span></span>

## <a name="change-credentials"></a><span data-ttu-id="7e7ec-195">Alterar credenciais</span><span class="sxs-lookup"><span data-stu-id="7e7ec-195">Change credentials</span></span>

<span data-ttu-id="7e7ec-196">toochange Olá credenciais para um aplicativo do AD, devido a um comprometimento de segurança ou uma expiração de credenciais, usar `azure ad app set`.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-196">toochange hello credentials for an AD app, either because of a security compromise or a credential expiration, use `azure ad app set`.</span></span>

<span data-ttu-id="7e7ec-197">toochange uma senha, use:</span><span class="sxs-lookup"><span data-stu-id="7e7ec-197">toochange a password, use:</span></span>

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --password p@ssword
```

<span data-ttu-id="7e7ec-198">toochange um valor de certificado, use:</span><span class="sxs-lookup"><span data-stu-id="7e7ec-198">toochange a certificate value, use:</span></span>

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --cert-value {certificate data}
```

## <a name="debug"></a><span data-ttu-id="7e7ec-199">Depurar</span><span class="sxs-lookup"><span data-stu-id="7e7ec-199">Debug</span></span>

<span data-ttu-id="7e7ec-200">Você pode encontrar hello os erros a seguir ao criar uma entidade de serviço:</span><span class="sxs-lookup"><span data-stu-id="7e7ec-200">You may encounter hello following errors when creating a service principal:</span></span>

* <span data-ttu-id="7e7ec-201">**"Authentication_Unauthorized"** ou **"nenhuma assinatura encontrada no contexto de Olá".**</span><span class="sxs-lookup"><span data-stu-id="7e7ec-201">**"Authentication_Unauthorized"** or **"No subscription found in hello context."**</span></span> <span data-ttu-id="7e7ec-202">-Você vir esse erro quando sua conta não tem Olá [as permissões necessárias](#required-permissions) no Active Directory do Azure de saudação tooregister um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-202">- You see this error when your account does not have hello [required permissions](#required-permissions) on hello Azure Active Directory tooregister an app.</span></span> <span data-ttu-id="7e7ec-203">Normalmente, você verá esse erro somente quando os usuários administradores no Active Directory do Azure puderem registrar aplicativos e sua conta não for um administrador. Peça ao seu administrador tooeither atribuir a função administrador tooan ou tooenable usuários tooregister aplicativos.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-203">Typically, you see this error when only admin users in your Azure Active Directory can register apps, and your account is not an admin. Ask your administrator tooeither assign you tooan administrator role, or tooenable users tooregister apps.</span></span>

* <span data-ttu-id="7e7ec-204">Sua conta **"não tem autorização tooperform ação 'Microsoft.Authorization/roleAssignments/write' no escopo 'assinaturas / {guid}'."**  -Consulte esse erro quando sua conta não tem suficientes tooassign de permissões uma identidade de tooan de função.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-204">Your account **"does not have authorization tooperform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/{guid}'."** - You see this error when your account does not have sufficient permissions tooassign a role tooan identity.</span></span> <span data-ttu-id="7e7ec-205">Peça ao seu tooadd do administrador de assinatura função administrador do acesso tooUser.</span><span class="sxs-lookup"><span data-stu-id="7e7ec-205">Ask your subscription administrator tooadd you tooUser Access Administrator role.</span></span>

## <a name="sample-applications"></a><span data-ttu-id="7e7ec-206">Aplicativos de exemplo</span><span class="sxs-lookup"><span data-stu-id="7e7ec-206">Sample applications</span></span>
<span data-ttu-id="7e7ec-207">Para obter informações sobre como fazer logon como um aplicativo hello através de diferentes plataformas, consulte:</span><span class="sxs-lookup"><span data-stu-id="7e7ec-207">For information about logging in as hello application through different platforms, see:</span></span>

* [<span data-ttu-id="7e7ec-208">.NET</span><span class="sxs-lookup"><span data-stu-id="7e7ec-208">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="7e7ec-209">Java</span><span class="sxs-lookup"><span data-stu-id="7e7ec-209">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="7e7ec-210">Node.js</span><span class="sxs-lookup"><span data-stu-id="7e7ec-210">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="7e7ec-211">Python</span><span class="sxs-lookup"><span data-stu-id="7e7ec-211">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="7e7ec-212">Ruby</span><span class="sxs-lookup"><span data-stu-id="7e7ec-212">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a><span data-ttu-id="7e7ec-213">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7e7ec-213">Next steps</span></span>
* <span data-ttu-id="7e7ec-214">Para obter etapas detalhadas sobre como integrar um aplicativo do Azure para gerenciar recursos, consulte [tooauthorization de guia do desenvolvedor com hello API do Gerenciador de recursos do Azure](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="7e7ec-214">For detailed steps on integrating an application into Azure for managing resources, see [Developer's guide tooauthorization with hello Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="7e7ec-215">tooget obter mais informações sobre como usar certificados e a CLI do Azure, consulte [autenticação baseada em certificado com entidades de serviço do Azure, na linha de comando do Linux](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx).</span><span class="sxs-lookup"><span data-stu-id="7e7ec-215">tooget more information about using certificates and Azure CLI, see [Certificate-based authentication with Azure Service Principals from Linux command line](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx).</span></span> 
* <span data-ttu-id="7e7ec-216">Para obter uma lista de ações disponíveis que podem ser concedidas ou negadas toousers, consulte [operações do provedor de recursos do Gerenciador de recursos do Azure](../active-directory/role-based-access-control-resource-provider-operations.md).</span><span class="sxs-lookup"><span data-stu-id="7e7ec-216">For a list of available actions that can be granted or denied toousers, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>
