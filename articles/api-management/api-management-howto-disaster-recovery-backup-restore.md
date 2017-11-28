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
# <a name="how-tooimplement-disaster-recovery-using-service-backup-and-restore-in-azure-api-management"></a><span data-ttu-id="31bd5-103">Como recuperação de desastres tooimplement usando serviço de backup e restauração no gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="31bd5-103">How tooimplement disaster recovery using service backup and restore in Azure API Management</span></span>
<span data-ttu-id="31bd5-104">Ao escolher toopublish e gerenciar suas APIs por meio do gerenciamento de API do Azure você está aproveitando as vantagens de muitos recursos de infraestrutura e de tolerância de falhas que você teria toodesign, implementar e gerenciar.</span><span class="sxs-lookup"><span data-stu-id="31bd5-104">By choosing toopublish and manage your APIs via Azure API Management you are taking advantage of many fault tolerance and infrastructure capabilities that you would otherwise have toodesign, implement, and manage.</span></span> <span data-ttu-id="31bd5-105">Olá plataforma Azure reduz uma grande parte de possíveis falhas em uma fração do custo de saudação.</span><span class="sxs-lookup"><span data-stu-id="31bd5-105">hello Azure platform mitigates a large fraction of potential failures at a fraction of hello cost.</span></span>

<span data-ttu-id="31bd5-106">toorecover de problemas de disponibilidade que afetam Olá região onde seu serviço de gerenciamento de API hospedado, você deve estar pronto tooreconstitute seu serviço em uma região diferente a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="31bd5-106">toorecover from availability problems affecting hello region where your API Management service is hosted you should be ready tooreconstitute your service in a different region at any time.</span></span> <span data-ttu-id="31bd5-107">Dependendo de suas metas de disponibilidade e o objetivo de tempo de recuperação, você pode desejar tooreserve um serviço de backup em uma ou mais regiões e tente toomaintain sua configuração e conteúdo em sincronia com o serviço de active Olá.</span><span class="sxs-lookup"><span data-stu-id="31bd5-107">Depending on your availability goals and recovery time objective  you might want tooreserve a backup service in one or more regions and try toomaintain their configuration and content in sync with hello active service.</span></span> <span data-ttu-id="31bd5-108">backup do serviço Hello e recurso de restauração fornece Olá bloco de construção necessárias para implementar sua estratégia de recuperação de desastres.</span><span class="sxs-lookup"><span data-stu-id="31bd5-108">hello service backup and restore feature provides hello necessary building block for implementing your disaster recovery strategy.</span></span>

<span data-ttu-id="31bd5-109">Este guia mostra como solicita tooauthenticate Azure Resource Manager e toobackup e restaurar suas instâncias de serviço de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="31bd5-109">This guide shows how tooauthenticate Azure Resource Manager requests, and how toobackup and restore your API Management service instances.</span></span>

> [!NOTE]
> <span data-ttu-id="31bd5-110">processo de saudação para fazer backup e restaurando uma instância do serviço de gerenciamento de API para recuperação de desastres também pode ser usado para a replicação de instâncias de serviço de gerenciamento de API para cenários como preparação.</span><span class="sxs-lookup"><span data-stu-id="31bd5-110">hello process for backing up and restoring an API Management service instance for disaster recovery can also be used for replicating API Management service instances for scenarios such as staging.</span></span>
>
> <span data-ttu-id="31bd5-111">Observe que cada backup expira após 30 dias.</span><span class="sxs-lookup"><span data-stu-id="31bd5-111">Note that each backup expires after 30 days.</span></span> <span data-ttu-id="31bd5-112">Se você tentar toorestore um backup depois que o período de validade de 30 dias Olá expirou, falha na restauração Olá com um `Cannot restore: backup expired` mensagem.</span><span class="sxs-lookup"><span data-stu-id="31bd5-112">If you attempt toorestore a backup after hello 30 day expiration period has expired, hello restore will fail with a `Cannot restore: backup expired` message.</span></span>
>
>

## <a name="authenticating-azure-resource-manager-requests"></a><span data-ttu-id="31bd5-113">Autenticação de solicitações do gerenciador de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="31bd5-113">Authenticating Azure Resource Manager requests</span></span>
> [!IMPORTANT]
> <span data-ttu-id="31bd5-114">Olá API REST para backup e restauração usa o Gerenciador de recursos do Azure e tem um mecanismo de autenticação que Olá APIs REST para gerenciar suas entidades de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="31bd5-114">hello REST API for backup and restore uses Azure Resource Manager and has a different authentication mechanism than hello REST APIs for managing your API Management entities.</span></span> <span data-ttu-id="31bd5-115">Olá etapas desta seção descrevem como tooauthenticate Gerenciador de recursos do Azure solicita.</span><span class="sxs-lookup"><span data-stu-id="31bd5-115">hello steps in this section describe how tooauthenticate Azure Resource Manager requests.</span></span> <span data-ttu-id="31bd5-116">Para mais informações, consulte [Autenticação de solicitações do Gerenciador de Recursos do Azure](http://msdn.microsoft.com/library/azure/dn790557.aspx).</span><span class="sxs-lookup"><span data-stu-id="31bd5-116">For more information, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).</span></span>
>
>

<span data-ttu-id="31bd5-117">Todas as tarefas de saudação que você faz em recursos usando hello Azure Resource Manager devem ser autenticadas com o Active Directory do Azure usando Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="31bd5-117">All of hello tasks that you do on resources using hello Azure Resource Manager must be authenticated with Azure Active Directory using hello following steps.</span></span>

* <span data-ttu-id="31bd5-118">Adicione um locatário do Active Directory do Azure do aplicativo toohello.</span><span class="sxs-lookup"><span data-stu-id="31bd5-118">Add an application toohello Azure Active Directory tenant.</span></span>
* <span data-ttu-id="31bd5-119">Definir permissões para o aplicativo hello que você adicionou.</span><span class="sxs-lookup"><span data-stu-id="31bd5-119">Set permissions for hello application that you added.</span></span>
* <span data-ttu-id="31bd5-120">Obtenha o token de saudação para autenticar solicitações tooAzure Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="31bd5-120">Get hello token for authenticating requests tooAzure Resource Manager.</span></span>

<span data-ttu-id="31bd5-121">Olá primeira etapa é toocreate um aplicativo do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="31bd5-121">hello first step is toocreate an Azure Active Directory application.</span></span> <span data-ttu-id="31bd5-122">Faça logon no hello [Portal clássico do Azure](http://manage.windowsazure.com/) usando assinatura Olá que contém o serviço de gerenciamento de API de instância e navegue toohello **aplicativos** guia para o padrão do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="31bd5-122">Log into hello [Azure Classic Portal](http://manage.windowsazure.com/) using hello subscription that contains your API Management service instance and navigate toohello **Applications** tab for your default Azure Active Directory.</span></span>

> [!NOTE]
> <span data-ttu-id="31bd5-123">Se o diretório do hello Azure Active Directory padrão não é visível tooyour conta, administrador contato Olá Olá Olá de toogrant de assinatura do Azure necessário conta tooyour de permissões.</span><span class="sxs-lookup"><span data-stu-id="31bd5-123">If hello Azure Active Directory default directory is not visible tooyour account, contact hello administrator of hello Azure subscription toogrant hello required permissions tooyour account.</span></span>

![Criar aplicativo do Active Directory do Azure][api-management-add-aad-application]

<span data-ttu-id="31bd5-125">Clique em **Adicionar**, **Adicionar um aplicativo que minha organização está desenvolvendo** e escolha **Aplicativo cliente nativo**.</span><span class="sxs-lookup"><span data-stu-id="31bd5-125">Click **Add**, **Add an application my organization is developing**, and choose **Native client application**.</span></span> <span data-ttu-id="31bd5-126">Insira um nome descritivo e clique em seta Avançar hello.</span><span class="sxs-lookup"><span data-stu-id="31bd5-126">Enter a descriptive name, and click hello next arrow.</span></span> <span data-ttu-id="31bd5-127">Insira uma URL de espaço reservado como `http://resources` para Olá **URI de redirecionamento**, conforme é um campo obrigatório, mas o valor de saudação não é usado mais tarde.</span><span class="sxs-lookup"><span data-stu-id="31bd5-127">Enter a placeholder URL such as `http://resources` for hello **Redirect URI**, as it is a required field, but hello value is not used later.</span></span> <span data-ttu-id="31bd5-128">Clique em aplicativo de saudação do hello caixa de seleção toosave.</span><span class="sxs-lookup"><span data-stu-id="31bd5-128">Click hello check box toosave hello application.</span></span>

<span data-ttu-id="31bd5-129">Depois que o aplicativo hello for salva, clique em **configurar**, role para baixo toohello **permissões tooother aplicativos** seção e, em seguida, clique em **Adicionar aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="31bd5-129">Once hello application is saved, click **Configure**, scroll down toohello **permissions tooother applications** section, and click **Add application**.</span></span>

![Adicionar permissões][api-management-aad-permissions-add]

<span data-ttu-id="31bd5-131">Selecione **Windows** **API de gerenciamento de serviços do Azure** e clique em aplicativo de saudação de tooadd hello caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="31bd5-131">Select **Windows** **Azure Service Management API** and click hello checkbox tooadd hello application.</span></span>

![Adicionar permissões][api-management-aad-permissions]

<span data-ttu-id="31bd5-133">Clique em **permissões delegadas** ao lado de saudação recém-adicionado **Windows** **API de gerenciamento de serviços do Azure** aplicativo, a caixa de seleção Olá **acessar o Azure Gerenciamento de serviço (visualização)**e clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="31bd5-133">Click **Delegated Permissions** beside hello newly added **Windows** **Azure Service Management API** application, check hello box for **Access Azure Service Management (preview)**, and click **Save**.</span></span>

![Adicionar permissões][api-management-aad-delegated-permissions]

<span data-ttu-id="31bd5-135">Olá tooinvoking anterior APIs que geram Olá backup e restaurá-lo, é necessário tooget um token.</span><span class="sxs-lookup"><span data-stu-id="31bd5-135">Prior tooinvoking hello APIs that generate hello backup and restore it, it is necessary tooget a token.</span></span> <span data-ttu-id="31bd5-136">Olá, exemplo a seguir usa Olá [ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) token de saudação do nuget pacote tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="31bd5-136">hello following example uses hello [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) nuget package tooretrieve hello token.</span></span>

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

<span data-ttu-id="31bd5-137">Substituir `{tentand id}`, `{application id}`, e `{redirect uri}` usando Olá instruções a seguir.</span><span class="sxs-lookup"><span data-stu-id="31bd5-137">Replace `{tentand id}`, `{application id}`, and `{redirect uri}` using hello following instructions.</span></span>

<span data-ttu-id="31bd5-138">Substituir `{tenant id}` com a id de locatário de saudação do hello aplicativo do Active Directory do Azure que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="31bd5-138">Replace `{tenant id}` with hello tenant id of hello Azure Active Directory application you just created.</span></span> <span data-ttu-id="31bd5-139">Você pode acessar a id de saudação clicando **exibir pontos de extremidade**.</span><span class="sxs-lookup"><span data-stu-id="31bd5-139">You can access hello id by clicking **View endpoints**.</span></span>

![Pontos de extremidade][api-management-aad-default-directory]

![Pontos de extremidade][api-management-endpoint]

<span data-ttu-id="31bd5-142">Substituir `{application id}` e `{redirect uri}` usando Olá **Id do cliente** e Olá URL da saudação **Uris de redirecionamento** seção do seu aplicativo Active Directory do Azure **configurar**  guia.</span><span class="sxs-lookup"><span data-stu-id="31bd5-142">Replace `{application id}` and `{redirect uri}` using hello **Client Id** and  hello URL from hello **Redirect Uris** section from your Azure Active Directory application's **Configure** tab.</span></span>

![Recursos][api-management-aad-resources]

<span data-ttu-id="31bd5-144">Depois que forem especificados valores hello, exemplo de código hello deve retornar um token toohello semelhante exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="31bd5-144">Once hello values are specified, hello code example should return a token similar toohello following example.</span></span>

![Token][api-management-arm-token]

<span data-ttu-id="31bd5-146">Antes de chamar hello backup e restaurar operações descritas nas seções a seguir de saudação, defina o cabeçalho de solicitação de autorização de saudação da chamada REST.</span><span class="sxs-lookup"><span data-stu-id="31bd5-146">Before calling hello backup and restore operations described in hello following sections, set hello authorization request header for your REST call.</span></span>

```c#
request.Headers.Add(HttpRequestHeader.Authorization, "Bearer " + token);
```

## <span data-ttu-id="31bd5-147"><a name="step1"> </a>Fazer backup de um serviço de Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="31bd5-147"><a name="step1"> </a>Back up an API Management service</span></span>
<span data-ttu-id="31bd5-148">tooback backup uma saudação de problema de serviço de gerenciamento de API solicitação HTTP a seguir:</span><span class="sxs-lookup"><span data-stu-id="31bd5-148">tooback up an API Management service issue hello following HTTP request:</span></span>

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backup?api-version={api-version}`

<span data-ttu-id="31bd5-149">onde:</span><span class="sxs-lookup"><span data-stu-id="31bd5-149">where:</span></span>

* <span data-ttu-id="31bd5-150">`subscriptionId`-id de assinatura de saudação que contém o serviço de gerenciamento de API Olá você está tentando executar toobackup</span><span class="sxs-lookup"><span data-stu-id="31bd5-150">`subscriptionId` - id of hello subscription containing hello API Management service you are attempting toobackup</span></span>
* <span data-ttu-id="31bd5-151">`resourceGroupName`-uma cadeia de caracteres em forma de saudação do 'Api - Default-{região do serviço}' onde `service-region` identifica Olá região do Azure onde Olá serviço de gerenciamento de API que você está tentando toobackup está hospedado, por exemplo,`North-Central-US`</span><span class="sxs-lookup"><span data-stu-id="31bd5-151">`resourceGroupName` - a string in hello form of 'Api-Default-{service-region}' where `service-region` identifies hello Azure region where hello API Management service you are trying toobackup is hosted, e.g. `North-Central-US`</span></span>
* <span data-ttu-id="31bd5-152">`serviceName`-nome de saudação do hello você estiver fazendo um backup do especificado no momento da saudação de sua criação de serviço de gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="31bd5-152">`serviceName` - hello name of hello API Management service you are making a backup of specified at hello time of its creation</span></span>
* <span data-ttu-id="31bd5-153">`api-version` - substitua por `2014-02-14`</span><span class="sxs-lookup"><span data-stu-id="31bd5-153">`api-version` - replace  with `2014-02-14`</span></span>

<span data-ttu-id="31bd5-154">No corpo de saudação da solicitação hello, especifica o nome de conta de armazenamento do Azure de destino hello, chave de acesso, nome do contêiner de blob e o nome do backup:</span><span class="sxs-lookup"><span data-stu-id="31bd5-154">In hello body of hello request, specify hello target Azure storage account name, access key, blob container name, and backup name:</span></span>

```
'{  
    storageAccount : {storage account name for hello backup},  
    accessKey : {access key for hello account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

<span data-ttu-id="31bd5-155">Definir valor Olá Olá `Content-Type` cabeçalho de solicitação muito`application/json`.</span><span class="sxs-lookup"><span data-stu-id="31bd5-155">Set hello value of hello `Content-Type` request header too`application/json`.</span></span>

<span data-ttu-id="31bd5-156">Backup é uma operação demorada que pode levar vários toocomplete de minutos.</span><span class="sxs-lookup"><span data-stu-id="31bd5-156">Backup is a long running operation that may take multiple minutes toocomplete.</span></span>  <span data-ttu-id="31bd5-157">Se Olá solicitação foi bem-sucedida e o processo de backup Olá foi iniciado você receberá um `202 Accepted` código de status de resposta com um `Location` cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="31bd5-157">If hello request was successful and hello backup process was initiated you’ll receive a `202 Accepted` response status code with a `Location` header.</span></span>  <span data-ttu-id="31bd5-158">Verifique 'GET' solicitações de URL toohello Olá `Location` toofind cabeçalho status Olá da operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="31bd5-158">Make 'GET' requests toohello URL in hello `Location` header toofind out hello status of hello operation.</span></span> <span data-ttu-id="31bd5-159">Enquanto Olá backup está em andamento, você continuará tooreceive um código de status '202 aceito'.</span><span class="sxs-lookup"><span data-stu-id="31bd5-159">While hello backup is in progress you will continue tooreceive a '202 Accepted' status code.</span></span> <span data-ttu-id="31bd5-160">Um código de resposta `200 OK` indicará a conclusão bem-sucedida da operação de backup hello.</span><span class="sxs-lookup"><span data-stu-id="31bd5-160">A Response code of `200 OK` will indicate successful completion of hello backup operation.</span></span>

<span data-ttu-id="31bd5-161">Observe Olá restrições a seguir ao fazer uma solicitação de backup.</span><span class="sxs-lookup"><span data-stu-id="31bd5-161">Please note hello following constraints when making a backup request.</span></span>

* <span data-ttu-id="31bd5-162">**Contêiner** especificadas no corpo da solicitação de saudação **devem existir**.</span><span class="sxs-lookup"><span data-stu-id="31bd5-162">**Container** specified in hello request body **must exist**.</span></span>
* <span data-ttu-id="31bd5-163">Enquanto o backup está em andamento, você **não deve tentar quaisquer operações de gerenciamento de serviço** , como atualização ou downgrade de SKU, alteração do nome do domínio, etc.</span><span class="sxs-lookup"><span data-stu-id="31bd5-163">While backup is in progress you **should not attempt any service management operations** such as SKU upgrade or downgrade, domain name change, etc.</span></span>
* <span data-ttu-id="31bd5-164">Restauração de um **backup é garantido apenas para 30 dias** desde o momento de saudação de sua criação.</span><span class="sxs-lookup"><span data-stu-id="31bd5-164">Restore of a **backup is guaranteed only for 30 days** since hello moment of its creation.</span></span>
* <span data-ttu-id="31bd5-165">**Dados de uso** usados para criar relatórios de análise **não está incluído** no backup hello.</span><span class="sxs-lookup"><span data-stu-id="31bd5-165">**Usage data** used for creating analytics reports **is not included** in hello backup.</span></span> <span data-ttu-id="31bd5-166">Use [API de REST de gerenciamento de API do Azure] [ Azure API Management REST API] tooperiodically recuperar os relatórios de análise de segurança.</span><span class="sxs-lookup"><span data-stu-id="31bd5-166">Use [Azure API Management REST API][Azure API Management REST API] tooperiodically retrieve analytics reports for safekeeping.</span></span>
* <span data-ttu-id="31bd5-167">frequência de saudação com a qual você executar backups de serviço afetará seu objetivo de ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="31bd5-167">hello frequency with which you perform service backups will affect your recovery point objective.</span></span> <span data-ttu-id="31bd5-168">toominimize-é recomendável implementar backups regulares, bem como executar backups sob demanda depois de fazer importantes alterações tooyour serviço de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="31bd5-168">toominimize it we advise implementing regular backups as well as performing on-demand backups after making important changes tooyour API Management service.</span></span>
* <span data-ttu-id="31bd5-169">**Alterações** toohello feita configuração de serviço (por exemplo, APIs, políticas, aparência portal do desenvolvedor) durante a operação de backup está em processo **não podem ser incluídos no backup hello e, portanto, serão perdidas**.</span><span class="sxs-lookup"><span data-stu-id="31bd5-169">**Changes** made toohello service configuration (e.g. APIs, policies, developer portal appearance) while backup operation is in process **might not be included in hello backup and therefore will be lost**.</span></span>

## <span data-ttu-id="31bd5-170"><a name="step2"> </a>Restaurar um serviço de Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="31bd5-170"><a name="step2"> </a>Restore an API Management service</span></span>
<span data-ttu-id="31bd5-171">toorestore um serviço de gerenciamento de API de um backup criado anteriormente fazer Olá solicitação HTTP a seguir:</span><span class="sxs-lookup"><span data-stu-id="31bd5-171">toorestore an API Management service from a previously created backup make hello following HTTP request:</span></span>

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/restore?api-version={api-version}`

<span data-ttu-id="31bd5-172">onde:</span><span class="sxs-lookup"><span data-stu-id="31bd5-172">where:</span></span>

* <span data-ttu-id="31bd5-173">`subscriptionId`-id de assinatura de saudação que contém o serviço de gerenciamento de API Olá você está restaurando um backup em</span><span class="sxs-lookup"><span data-stu-id="31bd5-173">`subscriptionId` - id of hello subscription containing hello API Management service you are restoring a backup into</span></span>
* <span data-ttu-id="31bd5-174">`resourceGroupName`-uma cadeia de caracteres em forma de saudação do 'Api - Default-{região do serviço}' onde `service-region` identifica Olá região do Azure onde Olá serviço de gerenciamento de API, você está restaurando um backup em está hospedado, por exemplo,`North-Central-US`</span><span class="sxs-lookup"><span data-stu-id="31bd5-174">`resourceGroupName` - a string in hello form of 'Api-Default-{service-region}' where `service-region` identifies hello Azure region where hello API Management service you are restoring a backup into is hosted, e.g. `North-Central-US`</span></span>
* <span data-ttu-id="31bd5-175">`serviceName`-nome de saudação do hello gerenciamento de API de serviço que está sendo restaurado em especificado no tempo de saudação de sua criação</span><span class="sxs-lookup"><span data-stu-id="31bd5-175">`serviceName` - hello name of hello API Management service being restored into specified at hello time of its creation</span></span>
* <span data-ttu-id="31bd5-176">`api-version` - substitua por `2014-02-14`</span><span class="sxs-lookup"><span data-stu-id="31bd5-176">`api-version` - replace  with `2014-02-14`</span></span>

<span data-ttu-id="31bd5-177">No corpo de Olá da solicitação de saudação, especifique o local do arquivo de backup hello, ou seja, nome da conta de armazenamento do Azure, chave de acesso, nome do contêiner de blob e o nome do backup:</span><span class="sxs-lookup"><span data-stu-id="31bd5-177">In hello body of hello request, specify hello backup file location, i.e. Azure storage account name, access key, blob container name, and backup name:</span></span>

```
'{  
    storageAccount : {storage account name for hello backup},  
    accessKey : {access key for hello account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

<span data-ttu-id="31bd5-178">Definir valor Olá Olá `Content-Type` cabeçalho de solicitação muito`application/json`.</span><span class="sxs-lookup"><span data-stu-id="31bd5-178">Set hello value of hello `Content-Type` request header too`application/json`.</span></span>

<span data-ttu-id="31bd5-179">A restauração é uma operação demorada que pode levar até too30 ou mais toocomplete de minutos.</span><span class="sxs-lookup"><span data-stu-id="31bd5-179">Restore is a long running operation that may take up too30 or more minutes toocomplete.</span></span>  <span data-ttu-id="31bd5-180">Se a solicitação Olá foi bem-sucedida e o processo de restauração Olá foi iniciado você receberá um `202 Accepted` código de status de resposta com um `Location` cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="31bd5-180">If hello request was successful and hello restore process was initiated you’ll receive a `202 Accepted` response status code with a `Location` header.</span></span>  <span data-ttu-id="31bd5-181">Verifique 'GET' solicitações de URL toohello Olá `Location` toofind cabeçalho status Olá da operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="31bd5-181">Make 'GET' requests toohello URL in hello `Location` header toofind out hello status of hello operation.</span></span> <span data-ttu-id="31bd5-182">Enquanto Olá restauração está em andamento, você continuará tooreceive código de status de '202 aceito'.</span><span class="sxs-lookup"><span data-stu-id="31bd5-182">While hello restore is in progress you will continue tooreceive '202 Accepted' status code.</span></span> <span data-ttu-id="31bd5-183">Um código de resposta `200 OK` indicará a conclusão bem-sucedida da operação de restauração de saudação.</span><span class="sxs-lookup"><span data-stu-id="31bd5-183">A response code of `200 OK` will indicate successful completion of hello restore operation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="31bd5-184">**Olá SKU** do serviço hello está sendo restaurado em **devem corresponder** Olá SKU do hello backup do serviço que está sendo restaurado.</span><span class="sxs-lookup"><span data-stu-id="31bd5-184">**hello SKU** of hello service being restored into **must match** hello SKU of hello backed up service being restored.</span></span>
>
> <span data-ttu-id="31bd5-185">**Alterações** toohello feita configuração de serviço (por exemplo, APIs, políticas, aparência portal do desenvolvedor) durante a operação de restauração está em andamento **poderão ser substituídos**.</span><span class="sxs-lookup"><span data-stu-id="31bd5-185">**Changes** made toohello service configuration (e.g. APIs, policies, developer portal appearance) while restore operation is in progress **could be overwritten**.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="31bd5-186">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="31bd5-186">Next steps</span></span>
<span data-ttu-id="31bd5-187">Check-out Olá blogs da Microsoft para duas diferente explicações passo a passo do processo de backup/restauração Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="31bd5-187">Check out hello following Microsoft blogs for two different walkthroughs of hello backup/restore process.</span></span>

* [<span data-ttu-id="31bd5-188">Replicar contas de Gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="31bd5-188">Replicate Azure API Management Accounts</span></span>](https://www.returngis.net/en/2015/06/replicate-azure-api-management-accounts/)
  * <span data-ttu-id="31bd5-189">Obrigado tooGisela para seu artigo toothis de contribuição.</span><span class="sxs-lookup"><span data-stu-id="31bd5-189">Thank you tooGisela for her contribution toothis article.</span></span>
* [<span data-ttu-id="31bd5-190">Gerenciamento de API do Azure: Fazendo backup e restaurando a configuração</span><span class="sxs-lookup"><span data-stu-id="31bd5-190">Azure API Management: Backing Up and Restoring Configuration</span></span>](http://blogs.msdn.com/b/stuartleeks/archive/2015/04/29/azure-api-management-backing-up-and-restoring-configuration.aspx)
  * <span data-ttu-id="31bd5-191">abordagem de saudação detalhada por Stuart não corresponde a orientação oficial hello, mas é muito interessante.</span><span class="sxs-lookup"><span data-stu-id="31bd5-191">hello approach detailed by Stuart does not match hello official guidance but it is very interesting.</span></span>

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
