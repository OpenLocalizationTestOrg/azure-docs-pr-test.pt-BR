---
title: "recuperação de desastres aaaImplement usando backup e restauração no gerenciamento de API do Azure | Microsoft Docs"
description: "Saiba como toouse de backup e restauração de recuperação de desastres tooperform no gerenciamento de API do Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 6f10be3c-f796-4a6c-bacd-7931b6aa82af
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 058bfb579e3a3f51fb1dac8ea37eb4fdbc83a4ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimplement-disaster-recovery-using-service-backup-and-restore-in-azure-api-management"></a>Como recuperação de desastres tooimplement usando serviço de backup e restauração no gerenciamento de API do Azure
Ao escolher toopublish e gerenciar suas APIs por meio do gerenciamento de API do Azure você está aproveitando as vantagens de muitos recursos de infraestrutura e de tolerância de falhas que você teria toodesign, implementar e gerenciar. Olá plataforma Azure reduz uma grande parte de possíveis falhas em uma fração do custo de saudação.

toorecover de problemas de disponibilidade que afetam Olá região onde seu serviço de gerenciamento de API hospedado, você deve estar pronto tooreconstitute seu serviço em uma região diferente a qualquer momento. Dependendo de suas metas de disponibilidade e o objetivo de tempo de recuperação, você pode desejar tooreserve um serviço de backup em uma ou mais regiões e tente toomaintain sua configuração e conteúdo em sincronia com o serviço de active Olá. backup do serviço Hello e recurso de restauração fornece Olá bloco de construção necessárias para implementar sua estratégia de recuperação de desastres.

Este guia mostra como solicita tooauthenticate Azure Resource Manager e toobackup e restaurar suas instâncias de serviço de gerenciamento de API.

> [!NOTE]
> processo de saudação para fazer backup e restaurando uma instância do serviço de gerenciamento de API para recuperação de desastres também pode ser usado para a replicação de instâncias de serviço de gerenciamento de API para cenários como preparação.
>
> Observe que cada backup expira após 30 dias. Se você tentar toorestore um backup depois que o período de validade de 30 dias Olá expirou, falha na restauração Olá com um `Cannot restore: backup expired` mensagem.
>
>

## <a name="authenticating-azure-resource-manager-requests"></a>Autenticação de solicitações do gerenciador de recursos do Azure
> [!IMPORTANT]
> Olá API REST para backup e restauração usa o Gerenciador de recursos do Azure e tem um mecanismo de autenticação que Olá APIs REST para gerenciar suas entidades de gerenciamento de API. Olá etapas desta seção descrevem como tooauthenticate Gerenciador de recursos do Azure solicita. Para mais informações, consulte [Autenticação de solicitações do Gerenciador de Recursos do Azure](http://msdn.microsoft.com/library/azure/dn790557.aspx).
>
>

Todas as tarefas de saudação que você faz em recursos usando hello Azure Resource Manager devem ser autenticadas com o Active Directory do Azure usando Olá etapas a seguir.

* Adicione um locatário do Active Directory do Azure do aplicativo toohello.
* Definir permissões para o aplicativo hello que você adicionou.
* Obtenha o token de saudação para autenticar solicitações tooAzure Gerenciador de recursos.

Olá primeira etapa é toocreate um aplicativo do Active Directory do Azure. Faça logon no hello [Portal clássico do Azure](http://manage.windowsazure.com/) usando assinatura Olá que contém o serviço de gerenciamento de API de instância e navegue toohello **aplicativos** guia para o padrão do Active Directory do Azure.

> [!NOTE]
> Se o diretório do hello Azure Active Directory padrão não é visível tooyour conta, administrador contato Olá Olá Olá de toogrant de assinatura do Azure necessário conta tooyour de permissões.

![Criar aplicativo do Active Directory do Azure][api-management-add-aad-application]

Clique em **Adicionar**, **Adicionar um aplicativo que minha organização está desenvolvendo** e escolha **Aplicativo cliente nativo**. Insira um nome descritivo e clique em seta Avançar hello. Insira uma URL de espaço reservado como `http://resources` para Olá **URI de redirecionamento**, conforme é um campo obrigatório, mas o valor de saudação não é usado mais tarde. Clique em aplicativo de saudação do hello caixa de seleção toosave.

Depois que o aplicativo hello for salva, clique em **configurar**, role para baixo toohello **permissões tooother aplicativos** seção e, em seguida, clique em **Adicionar aplicativo**.

![Adicionar permissões][api-management-aad-permissions-add]

Selecione **Windows** **API de gerenciamento de serviços do Azure** e clique em aplicativo de saudação de tooadd hello caixa de seleção.

![Adicionar permissões][api-management-aad-permissions]

Clique em **permissões delegadas** ao lado de saudação recém-adicionado **Windows** **API de gerenciamento de serviços do Azure** aplicativo, a caixa de seleção Olá **acessar o Azure Gerenciamento de serviço (visualização)**e clique em **salvar**.

![Adicionar permissões][api-management-aad-delegated-permissions]

Olá tooinvoking anterior APIs que geram Olá backup e restaurá-lo, é necessário tooget um token. Olá, exemplo a seguir usa Olá [ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) token de saudação do nuget pacote tooretrieve.

```c#
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System;

namespace GetTokenResourceManagerRequests
{
    class Program
    {
        static void Main(string[] args)
        {
            var authenticationContext = new AuthenticationContext("https://login.microsoftonline.com/{tenant id}");
            var result = authenticationContext.AcquireToken("https://management.azure.com/", {application id}, new Uri({redirect uri});

            if (result == null) {
                throw new InvalidOperationException("Failed tooobtain hello JWT token");
            }

            Console.WriteLine(result.AccessToken);

            Console.ReadLine();
        }
    }
}
```

Substituir `{tentand id}`, `{application id}`, e `{redirect uri}` usando Olá instruções a seguir.

Substituir `{tenant id}` com a id de locatário de saudação do hello aplicativo do Active Directory do Azure que você acabou de criar. Você pode acessar a id de saudação clicando **exibir pontos de extremidade**.

![Pontos de extremidade][api-management-aad-default-directory]

![Pontos de extremidade][api-management-endpoint]

Substituir `{application id}` e `{redirect uri}` usando Olá **Id do cliente** e Olá URL da saudação **Uris de redirecionamento** seção do seu aplicativo Active Directory do Azure **configurar**  guia.

![Recursos][api-management-aad-resources]

Depois que forem especificados valores hello, exemplo de código hello deve retornar um token toohello semelhante exemplo a seguir.

![Token][api-management-arm-token]

Antes de chamar hello backup e restaurar operações descritas nas seções a seguir de saudação, defina o cabeçalho de solicitação de autorização de saudação da chamada REST.

```c#
request.Headers.Add(HttpRequestHeader.Authorization, "Bearer " + token);
```

## <a name="step1"> </a>Fazer backup de um serviço de Gerenciamento de API
tooback backup uma saudação de problema de serviço de gerenciamento de API solicitação HTTP a seguir:

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backup?api-version={api-version}`

onde:

* `subscriptionId`-id de assinatura de saudação que contém o serviço de gerenciamento de API Olá você está tentando executar toobackup
* `resourceGroupName`-uma cadeia de caracteres em forma de saudação do 'Api - Default-{região do serviço}' onde `service-region` identifica Olá região do Azure onde Olá serviço de gerenciamento de API que você está tentando toobackup está hospedado, por exemplo,`North-Central-US`
* `serviceName`-nome de saudação do hello você estiver fazendo um backup do especificado no momento da saudação de sua criação de serviço de gerenciamento de API
* `api-version` - substitua por `2014-02-14`

No corpo de saudação da solicitação hello, especifica o nome de conta de armazenamento do Azure de destino hello, chave de acesso, nome do contêiner de blob e o nome do backup:

```
'{  
    storageAccount : {storage account name for hello backup},  
    accessKey : {access key for hello account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

Definir valor Olá Olá `Content-Type` cabeçalho de solicitação muito`application/json`.

Backup é uma operação demorada que pode levar vários toocomplete de minutos.  Se Olá solicitação foi bem-sucedida e o processo de backup Olá foi iniciado você receberá um `202 Accepted` código de status de resposta com um `Location` cabeçalho.  Verifique 'GET' solicitações de URL toohello Olá `Location` toofind cabeçalho status Olá da operação de saudação. Enquanto Olá backup está em andamento, você continuará tooreceive um código de status '202 aceito'. Um código de resposta `200 OK` indicará a conclusão bem-sucedida da operação de backup hello.

Observe Olá restrições a seguir ao fazer uma solicitação de backup.

* **Contêiner** especificadas no corpo da solicitação de saudação **devem existir**.
* Enquanto o backup está em andamento, você **não deve tentar quaisquer operações de gerenciamento de serviço** , como atualização ou downgrade de SKU, alteração do nome do domínio, etc.
* Restauração de um **backup é garantido apenas para 30 dias** desde o momento de saudação de sua criação.
* **Dados de uso** usados para criar relatórios de análise **não está incluído** no backup hello. Use [API de REST de gerenciamento de API do Azure] [ Azure API Management REST API] tooperiodically recuperar os relatórios de análise de segurança.
* frequência de saudação com a qual você executar backups de serviço afetará seu objetivo de ponto de recuperação. toominimize-é recomendável implementar backups regulares, bem como executar backups sob demanda depois de fazer importantes alterações tooyour serviço de gerenciamento de API.
* **Alterações** toohello feita configuração de serviço (por exemplo, APIs, políticas, aparência portal do desenvolvedor) durante a operação de backup está em processo **não podem ser incluídos no backup hello e, portanto, serão perdidas**.

## <a name="step2"> </a>Restaurar um serviço de Gerenciamento de API
toorestore um serviço de gerenciamento de API de um backup criado anteriormente fazer Olá solicitação HTTP a seguir:

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/restore?api-version={api-version}`

onde:

* `subscriptionId`-id de assinatura de saudação que contém o serviço de gerenciamento de API Olá você está restaurando um backup em
* `resourceGroupName`-uma cadeia de caracteres em forma de saudação do 'Api - Default-{região do serviço}' onde `service-region` identifica Olá região do Azure onde Olá serviço de gerenciamento de API, você está restaurando um backup em está hospedado, por exemplo,`North-Central-US`
* `serviceName`-nome de saudação do hello gerenciamento de API de serviço que está sendo restaurado em especificado no tempo de saudação de sua criação
* `api-version` - substitua por `2014-02-14`

No corpo de Olá da solicitação de saudação, especifique o local do arquivo de backup hello, ou seja, nome da conta de armazenamento do Azure, chave de acesso, nome do contêiner de blob e o nome do backup:

```
'{  
    storageAccount : {storage account name for hello backup},  
    accessKey : {access key for hello account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

Definir valor Olá Olá `Content-Type` cabeçalho de solicitação muito`application/json`.

A restauração é uma operação demorada que pode levar até too30 ou mais toocomplete de minutos.  Se a solicitação Olá foi bem-sucedida e o processo de restauração Olá foi iniciado você receberá um `202 Accepted` código de status de resposta com um `Location` cabeçalho.  Verifique 'GET' solicitações de URL toohello Olá `Location` toofind cabeçalho status Olá da operação de saudação. Enquanto Olá restauração está em andamento, você continuará tooreceive código de status de '202 aceito'. Um código de resposta `200 OK` indicará a conclusão bem-sucedida da operação de restauração de saudação.

> [!IMPORTANT]
> **Olá SKU** do serviço hello está sendo restaurado em **devem corresponder** Olá SKU do hello backup do serviço que está sendo restaurado.
>
> **Alterações** toohello feita configuração de serviço (por exemplo, APIs, políticas, aparência portal do desenvolvedor) durante a operação de restauração está em andamento **poderão ser substituídos**.
>
>

## <a name="next-steps"></a>Próximas etapas
Check-out Olá blogs da Microsoft para duas diferente explicações passo a passo do processo de backup/restauração Olá a seguir.

* [Replicar contas de Gerenciamento de API do Azure](https://www.returngis.net/en/2015/06/replicate-azure-api-management-accounts/)
  * Obrigado tooGisela para seu artigo toothis de contribuição.
* [Gerenciamento de API do Azure: Fazendo backup e restaurando a configuração](http://blogs.msdn.com/b/stuartleeks/archive/2015/04/29/azure-api-management-backing-up-and-restoring-configuration.aspx)
  * abordagem de saudação detalhada por Stuart não corresponde a orientação oficial hello, mas é muito interessante.

[Backup an API Management service]: #step1
[Restore an API Management service]: #step2


[Azure API Management REST API]: http://msdn.microsoft.com/library/azure/dn781421.aspx

[api-management-add-aad-application]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-add-aad-application.png

[api-management-aad-permissions]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-permissions.png
[api-management-aad-permissions-add]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-permissions-add.png
[api-management-aad-delegated-permissions]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-delegated-permissions.png
[api-management-aad-default-directory]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-default-directory.png
[api-management-aad-resources]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-aad-resources.png
[api-management-arm-token]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-arm-token.png
[api-management-endpoint]: ./media/api-management-howto-disaster-recovery-backup-restore/api-management-endpoint.png
