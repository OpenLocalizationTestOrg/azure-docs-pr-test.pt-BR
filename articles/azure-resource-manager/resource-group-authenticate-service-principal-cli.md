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
# <a name="use-azure-cli-toocreate-a-service-principal-tooaccess-resources"></a>Usar um serviço principal tooaccess recursos de toocreate CLI do Azure

Quando você tiver um aplicativo ou script que precisa de recursos de tooaccess, você pode configurar uma identidade para o aplicativo hello e autenticar o aplicativo hello com suas próprias credenciais. Essa identidade é conhecida como uma entidade de serviço. Essa abordagem permite:

* Atribua permissões de identidade de aplicativo toohello que são diferentes de suas próprias permissões. Normalmente, essas permissões são restrito tooexactly toodo precisa de qual aplicativo hello.
* Use um certificado para a autenticação ao executar um script autônomo.

Este artigo mostra como toouse [Azure CLI 1.0](../cli-install-nodejs.md) tooset backup toorun um aplicativo em suas próprias credenciais e identidade. Instalar a versão mais recente de saudação do [Azure CLI 1.0](../cli-install-nodejs.md) toomake se seu ambiente corresponde exemplos Olá neste artigo.

## <a name="required-permissions"></a>Permissões necessárias
toocomplete neste tópico, você deve ter permissões suficientes no Active Directory do Azure e sua assinatura do Azure. Especificamente, você deve ser capaz de toocreate um aplicativo de saudação do Active Directory do Azure e atribuir função de tooa principal do serviço de saudação. 

Olá mais fácil toocheck de maneira se sua conta tem permissões suficientes é por meio do portal hello. Consulte [Verificar permissão necessária no portal](resource-group-create-service-principal-portal.md#required-permissions).

Agora, continuar tooa seção devido a um [senha](#create-service-principal-with-password) ou [certificado](#create-service-principal-with-certificate) autenticação.

## <a name="create-service-principal-with-password"></a>Criar a entidade de serviço com a senha
Nesta seção, execute Olá etapas toocreate Olá aplicativo AD com uma senha e atribuir a entidade de serviço Olá leitor função toohello.

1. Entre na conta de tooyour.
   
   ```azurecli
   azure login
   ```
2. toocreate uma identidade de aplicativo, forneça Olá nome do aplicativo hello e uma senha, conforme mostrado na Olá comando a seguir:
     
   ```azurecli
   azure ad sp create -n exampleapp -p {your-password}
   ```
     
   entidade de serviço novo Olá é retornado. Olá Id de objeto é necessária quando a concessão de permissões. Olá guid listado com hello nomes da entidade de serviço é necessária durante o logon. Esse guid é hello mesmo valor de id do aplicativo hello. Em aplicativos de exemplo hello, esse valor é chamado tooas Olá `Client ID`. 
     
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

3. Conceder permissões de principal de serviço Olá em sua assinatura. Neste exemplo, você deve adicionar função Leitor do hello serviço toohello principal, que concede permissão tooread todos os recursos na assinatura de saudação. Para ver outras funções, confira [RBAC: funções internas](../active-directory/role-based-access-built-in-roles.md). Para o parâmetro objectid Olá fornecem Olá Id de objeto que você usou ao criar o aplicativo hello. Antes de executar esse comando, você deve permitir algum tempo para Olá novo serviço principal toopropagate em todo o Active Directory do Azure. Geralmente, ao executar esses comandos manualmente, um tempo suficiente já decorreu entre as tarefas. Em um script, você deve adicionar um toosleep etapa entre comandos hello (como `sleep 15`). Se você vir que uma saudação de erro informando principal não existe no diretório hello, execute novamente o comando de saudação.
   
   ```azurecli
   azure role assignment create --objectId ff863613-e5e2-4a6b-af07-fff6f2de3f4e -o Reader -c /subscriptions/{subscriptionId}/
   ```
   
É isso! Seu aplicativo do AD e a entidade de serviço estão configurados. Olá próxima seção mostra como toolog com hello as credenciais por meio da CLI do Azure. Se você quiser credencial de saudação toouse em seu aplicativo de código, não é necessário toocontinue neste tópico. Você pode ir toohello [aplicativos de exemplo](#sample-applications) para obter exemplos de registro em log com a id de aplicativo e a senha. 

### <a name="provide-credentials-through-azure-cli"></a>Fornecer credenciais por meio da CLI do Azure
Agora, você precisa toolog em operações de tooperform aplicativo hello.

1. Sempre que você entrar como uma entidade de serviço, você precisa tooprovide id de locatário de saudação do diretório de saudação para seu aplicativo do AD. Um locatário é uma instância do Active Directory do Azure. id de locatário tooretrieve Olá para sua assinatura autenticada no momento, use:
   
   ```azurecli
   azure account show
   ```
   
   Que retorna:
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
     Se você precisar de id de locatário Olá tooget de outra assinatura, use Olá comando a seguir:
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. Se você precisar tooretrieve Olá cliente id toouse para fazer logon, use:
   
   ```azurecli
   azure ad sp show -c exampleapp --json
   ```
   
     Olá valor toouse para log em é o guid de saudação listado em nomes de entidade de serviço hello.
   
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
3. Faça logon como entidade de serviço hello.
   
   ```azurecli
   azure login -u 7132aca4-1bdb-4238-ad81-996ff91d8db4 --service-principal --tenant {tenant-id}
   ```
   
    Você será solicitado a senha hello. Forneça a senha de saudação que você especificou ao criar o aplicativo hello AD.
   
   ```azurecli
   info:    Executing command login
   Password: ********
   ```

Agora você está autenticado como entidade de serviço Olá Olá entidade de serviço que você criou.

Como alternativa, você pode chamar operações REST do hello toolog de linha de comando no. De resposta de autenticação hello, você pode recuperar o token de acesso de saudação para uso com outras operações. Para obter um exemplo de recuperar o token de acesso de saudação ao chamar operações REST, consulte [gerar um Token de acesso](resource-manager-rest-api.md#generating-an-access-token).

## <a name="create-service-principal-with-certificate"></a>Criar a entidade de serviço com o certificado
Nesta seção, você deve executar etapas Olá para:

* criar um certificado autoassinado
* Criar hello aplicativo AD com certificado hello e entidade de serviço Olá
* atribuir a entidade de serviço Olá leitor função toohello

toocomplete essas etapas, você deve ter [OpenSSL](http://www.openssl.org/) instalado.

1. Crie um certificado autoassinado.
   
   ```
   openssl req -x509 -days 3650 -newkey rsa:2048 -out cert.pem -nodes -subj '/CN=exampleapp'
   ```

2. Olá anterior etapa criado dois arquivos - privkey.pem e cert.pem. Combine as chaves públicas e privadas Olá em um único arquivo.

   ```
   cat privkey.pem cert.pem > examplecert.pem
   ```

3. Olá abrir **examplecert.pem** de arquivo e procure a sequência longa de saudação de caracteres entre **---iniciar certificado---** e **---concluir certificado---**. Copie dados do certificado hello. Você pode passar esses dados como um parâmetro ao criar hello entidade de serviço.

4. Entre na conta de tooyour.

   ```azurecli
   azure login
   ```
5. entidade de serviço do toocreate Olá, fornece nome de saudação do aplicativo hello e dados do certificado Olá, conforme mostrado no comando a seguir de saudação:
     
   ```azurecli
   azure ad sp create -n exampleapp --cert-value {certificate data}
   ```
     
   entidade de serviço novo Olá é retornado. Olá Id de objeto é necessária quando a concessão de permissões. Olá guid listado com hello nomes da entidade de serviço é necessária durante o logon. Esse guid é hello mesmo valor de id do aplicativo hello. Em aplicativos de exemplo hello, esse valor é chamado tooas Olá ID do cliente. 
     
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
6. Conceder permissões de principal de serviço Olá em sua assinatura. Neste exemplo, você deve adicionar função Leitor do hello serviço toohello principal, que concede permissão tooread todos os recursos na assinatura de saudação. Para ver outras funções, confira [RBAC: funções internas](../active-directory/role-based-access-built-in-roles.md). Para o parâmetro objectid Olá fornecem Olá Id de objeto que você usou ao criar o aplicativo hello. Antes de executar esse comando, você deve permitir algum tempo para Olá novo serviço principal toopropagate em todo o Active Directory do Azure. Geralmente, ao executar esses comandos manualmente, um tempo suficiente já decorreu entre as tarefas. Em um script, você deve adicionar um toosleep etapa entre comandos hello (como `sleep 15`). Se você vir que uma saudação de erro informando principal não existe no diretório hello, execute novamente o comando de saudação.
   
   ```azurecli
   azure role assignment create --objectId 7dbc8265-51ed-4038-8e13-31948c7f4ce7 -o Reader -c /subscriptions/{subscriptionId}/
   ```
  
### <a name="provide-certificate-through-automated-azure-cli-script"></a>Fornecer certificado por meio do script CLI do Azure automatizado
Agora, você precisa toolog em operações de tooperform aplicativo hello.

1. Sempre que você entrar como uma entidade de serviço, você precisa tooprovide id de locatário de saudação do diretório de saudação para seu aplicativo do AD. Um locatário é uma instância do Active Directory do Azure. id de locatário tooretrieve Olá para sua assinatura autenticada no momento, use:
   
   ```azurecli
   azure account show
   ```
   
   Que retorna:
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
   Se você precisar de id de locatário Olá tooget de outra assinatura, use Olá comando a seguir:
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. tooretrieve Olá a impressão digital do certificado e remova os caracteres desnecessários, use:
   
   ```
   openssl x509 -in "C:\certificates\examplecert.pem" -fingerprint -noout | sed 's/SHA1 Fingerprint=//g'  | sed 's/://g'
   ```
   
   Que retorna um valor de impressão digital semelhante a:
   
   ```
   30996D9CE48A0B6E0CD49DBB9A48059BF9355851
   ```
3. Se você precisar tooretrieve Olá cliente id toouse para fazer logon, use:
   
   ```azurecli
   azure ad sp show -c exampleapp
   ```
   
   Olá valor toouse para log em é o guid de saudação listado em nomes de entidade de serviço hello.
     
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
4. Faça logon como entidade de serviço hello.
   
   ```azurecli
   azure login --service-principal --tenant {tenant-id} -u 4fd39843-c338-417d-b549-a545f584a745 --certificate-file C:\certificates\examplecert.pem --thumbprint {thumbprint}
   ```

Agora você está autenticado como entidade de serviço Olá para Olá aplicativo do Active Directory do Azure que você criou.

## <a name="change-credentials"></a>Alterar credenciais

toochange Olá credenciais para um aplicativo do AD, devido a um comprometimento de segurança ou uma expiração de credenciais, usar `azure ad app set`.

toochange uma senha, use:

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --password p@ssword
```

toochange um valor de certificado, use:

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --cert-value {certificate data}
```

## <a name="debug"></a>Depurar

Você pode encontrar hello os erros a seguir ao criar uma entidade de serviço:

* **"Authentication_Unauthorized"** ou **"nenhuma assinatura encontrada no contexto de Olá".** -Você vir esse erro quando sua conta não tem Olá [as permissões necessárias](#required-permissions) no Active Directory do Azure de saudação tooregister um aplicativo. Normalmente, você verá esse erro somente quando os usuários administradores no Active Directory do Azure puderem registrar aplicativos e sua conta não for um administrador. Peça ao seu administrador tooeither atribuir a função administrador tooan ou tooenable usuários tooregister aplicativos.

* Sua conta **"não tem autorização tooperform ação 'Microsoft.Authorization/roleAssignments/write' no escopo 'assinaturas / {guid}'."**  -Consulte esse erro quando sua conta não tem suficientes tooassign de permissões uma identidade de tooan de função. Peça ao seu tooadd do administrador de assinatura função administrador do acesso tooUser.

## <a name="sample-applications"></a>Aplicativos de exemplo
Para obter informações sobre como fazer logon como um aplicativo hello através de diferentes plataformas, consulte:

* [.NET](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [Java](/java/azure/java-sdk-azure-authenticate)
* [Node.js](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [Python](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [Ruby](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a>Próximas etapas
* Para obter etapas detalhadas sobre como integrar um aplicativo do Azure para gerenciar recursos, consulte [tooauthorization de guia do desenvolvedor com hello API do Gerenciador de recursos do Azure](resource-manager-api-authentication.md).
* tooget obter mais informações sobre como usar certificados e a CLI do Azure, consulte [autenticação baseada em certificado com entidades de serviço do Azure, na linha de comando do Linux](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx). 
* Para obter uma lista de ações disponíveis que podem ser concedidas ou negadas toousers, consulte [operações do provedor de recursos do Gerenciador de recursos do Azure](../active-directory/role-based-access-control-resource-provider-operations.md).
