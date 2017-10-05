---
title: "Implementar a recuperação de desastre usando backup e restauração no Gerenciamento de API do Azure | Microsoft Docs"
description: "Saiba como usar o backup e restauração para executar a recuperação de desastres no Gerenciamento de API no Azure."
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
ms.openlocfilehash: 07c0265490cfae733133b6e0c938f90f9b392da4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-implement-disaster-recovery-using-service-backup-and-restore-in-azure-api-management"></a><span data-ttu-id="fdf6e-103">Como implementar a recuperação de desastre usando o backup de serviço e restaurar no Gerenciamento de API no Azure</span><span class="sxs-lookup"><span data-stu-id="fdf6e-103">How to implement disaster recovery using service backup and restore in Azure API Management</span></span>
<span data-ttu-id="fdf6e-104">Ao escolher publicar e gerenciar suas APIs através do Gerenciamento de API do Azure, você está tirando proveito de muitos recursos de tolerância e infraestrutura que você precisaria criar, implementar e gerenciar.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-104">By choosing to publish and manage your APIs via Azure API Management you are taking advantage of many fault tolerance and infrastructure capabilities that you would otherwise have to design, implement, and manage.</span></span> <span data-ttu-id="fdf6e-105">A plataforma Azure atenua grande parte das falhas potenciais a uma fração do custo.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-105">The Azure platform mitigates a large fraction of potential failures at a fraction of the cost.</span></span>

<span data-ttu-id="fdf6e-106">Para se recuperar de problemas de disponibilidade que afetam a região onde o serviço de Gerenciamento de API está hospedado, você deverá estar pronto para reconstituir seu serviço em uma região diferente a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-106">To recover from availability problems affecting the region where your API Management service is hosted you should be ready to reconstitute your service in a different region at any time.</span></span> <span data-ttu-id="fdf6e-107">Dependendo de suas metas de disponibilidade e objetivo de tempo de recuperação, você pode querer reservar um serviço de backup em uma ou mais regiões e tentar manter suas configurações e conteúdos na sincronização com o serviço ativo.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-107">Depending on your availability goals and recovery time objective  you might want to reserve a backup service in one or more regions and try to maintain their configuration and content in sync with the active service.</span></span> <span data-ttu-id="fdf6e-108">O backup do serviço e o recurso de restauração fornece o bloco de criação necessário para implementação de sua estratégia de recuperação de desastre.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-108">The service backup and restore feature provides the necessary building block for implementing your disaster recovery strategy.</span></span>

<span data-ttu-id="fdf6e-109">Este guia mostra como autenticar solicitações do Gerenciador de Recursos do Azure e como fazer backup e restaurar suas instâncias de serviço de Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-109">This guide shows how to authenticate Azure Resource Manager requests, and how to backup and restore your API Management service instances.</span></span>

> [!NOTE]
> <span data-ttu-id="fdf6e-110">O processo de backup e restauração de uma instância do serviço Gerenciamento de API para recuperação de desastres também pode ser usado para replicar as instâncias de serviço Gerenciamento de API para cenários como preparação.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-110">The process for backing up and restoring an API Management service instance for disaster recovery can also be used for replicating API Management service instances for scenarios such as staging.</span></span>
>
> <span data-ttu-id="fdf6e-111">Observe que cada backup expira após 30 dias.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-111">Note that each backup expires after 30 days.</span></span> <span data-ttu-id="fdf6e-112">Se você tentar restaurar um backup após o período de expiração de 30 dias, a restauração falhará com uma mensagem `Cannot restore: backup expired`.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-112">If you attempt to restore a backup after the 30 day expiration period has expired, the restore will fail with a `Cannot restore: backup expired` message.</span></span>
>
>

## <a name="authenticating-azure-resource-manager-requests"></a><span data-ttu-id="fdf6e-113">Autenticação de solicitações do gerenciador de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="fdf6e-113">Authenticating Azure Resource Manager requests</span></span>
> [!IMPORTANT]
> <span data-ttu-id="fdf6e-114">A API REST para backup e restauração usa o Gerenciador de Recursos do Azure e tem um mecanismo de autenticação diferentes das APIs REST para gerenciar suas entidades de Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-114">The REST API for backup and restore uses Azure Resource Manager and has a different authentication mechanism than the REST APIs for managing your API Management entities.</span></span> <span data-ttu-id="fdf6e-115">As etapas desta seção descrevem como autenticar solicitações do Gerenciador de Recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-115">The steps in this section describe how to authenticate Azure Resource Manager requests.</span></span> <span data-ttu-id="fdf6e-116">Para mais informações, consulte [Autenticação de solicitações do Gerenciador de Recursos do Azure](http://msdn.microsoft.com/library/azure/dn790557.aspx).</span><span class="sxs-lookup"><span data-stu-id="fdf6e-116">For more information, see [Authenticating Azure Resource Manager requests](http://msdn.microsoft.com/library/azure/dn790557.aspx).</span></span>
>
>

<span data-ttu-id="fdf6e-117">Todas as tarefas que você faz em recursos usando o Gerenciador de Recursos do Azure devem ser autenticadas com o Active Directory do Azure usando as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-117">All of the tasks that you do on resources using the Azure Resource Manager must be authenticated with Azure Active Directory using the following steps.</span></span>

* <span data-ttu-id="fdf6e-118">Adicione um aplicativo no locatário do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-118">Add an application to the Azure Active Directory tenant.</span></span>
* <span data-ttu-id="fdf6e-119">Defina permissões para o aplicativo que você adicionou.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-119">Set permissions for the application that you added.</span></span>
* <span data-ttu-id="fdf6e-120">Obtenha o token para autenticar solicitações ao Gerenciador de Recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-120">Get the token for authenticating requests to Azure Resource Manager.</span></span>

<span data-ttu-id="fdf6e-121">A primeira etapa é criar um aplicativo do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-121">The first step is to create an Azure Active Directory application.</span></span> <span data-ttu-id="fdf6e-122">Faça logon no [Portal Clássico do Azure](http://manage.windowsazure.com/) usando a assinatura que contém sua instância de serviço Gerenciamento de API e navegue até a guia **Aplicativos** para o Active Directory do Azure padrão.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-122">Log into the [Azure Classic Portal](http://manage.windowsazure.com/) using the subscription that contains your API Management service instance and navigate to the **Applications** tab for your default Azure Active Directory.</span></span>

> [!NOTE]
> <span data-ttu-id="fdf6e-123">Se o diretório padrão do Active Directory do Azure não é visível para sua conta, contate o administrador da assinatura do Azure para conceder as permissões necessárias para sua conta.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-123">If the Azure Active Directory default directory is not visible to your account, contact the administrator of the Azure subscription to grant the required permissions to your account.</span></span>

![Criar aplicativo do Active Directory do Azure][api-management-add-aad-application]

<span data-ttu-id="fdf6e-125">Clique em **Adicionar**, **Adicionar um aplicativo que minha organização está desenvolvendo** e escolha **Aplicativo cliente nativo**.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-125">Click **Add**, **Add an application my organization is developing**, and choose **Native client application**.</span></span> <span data-ttu-id="fdf6e-126">Insira um nome descritivo e clique na seta Avançar.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-126">Enter a descriptive name, and click the next arrow.</span></span> <span data-ttu-id="fdf6e-127">Insira uma URL de espaço reservado como `http://resources` para o **URI de redirecionamento**, que é um campo obrigatório, mas o valor não é usado posteriormente.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-127">Enter a placeholder URL such as `http://resources` for the **Redirect URI**, as it is a required field, but the value is not used later.</span></span> <span data-ttu-id="fdf6e-128">Clique na caixa de seleção para salvar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-128">Click the check box to save the application.</span></span>

<span data-ttu-id="fdf6e-129">Quando o aplicativo estiver salvo, clique em **Configurar**, role para baixo até a seção **Permissões para outros aplicativos** e clique em **Adicionar aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-129">Once the application is saved, click **Configure**, scroll down to the **permissions to other applications** section, and click **Add application**.</span></span>

![Adicionar permissões][api-management-aad-permissions-add]

<span data-ttu-id="fdf6e-131">Selecione **Windows** **API de gerenciamento de serviços do Azure** e clique na caixa de seleção para adicionar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-131">Select **Windows** **Azure Service Management API** and click the checkbox to add the application.</span></span>

![Adicionar permissões][api-management-aad-permissions]

<span data-ttu-id="fdf6e-133">Clique em **Permissões delegadas** ao lado do aplicativo recém-adicionado **API de gerenciamento de serviços** do **Microsoft Azure**, marque a caixa **Acessar o gerenciamento de serviço do Azure (visualização)** e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-133">Click **Delegated Permissions** beside the newly added **Windows** **Azure Service Management API** application, check the box for **Access Azure Service Management (preview)**, and click **Save**.</span></span>

![Adicionar permissões][api-management-aad-delegated-permissions]

<span data-ttu-id="fdf6e-135">Antes de chamar as APIs que geram o backup e o restauram, é necessário obter um token.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-135">Prior to invoking the APIs that generate the backup and restore it, it is necessary to get a token.</span></span> <span data-ttu-id="fdf6e-136">O exemplo a seguir usa o pacote do nuget [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) para recuperar o token.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-136">The following example uses the [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory) nuget package to retrieve the token.</span></span>

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
                throw new InvalidOperationException("Failed to obtain the JWT token");
            }

            Console.WriteLine(result.AccessToken);

            Console.ReadLine();
        }
    }
}
```

<span data-ttu-id="fdf6e-137">Substitua `{tentand id}`, `{application id}` e `{redirect uri}` usando as instruções a seguir.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-137">Replace `{tentand id}`, `{application id}`, and `{redirect uri}` using the following instructions.</span></span>

<span data-ttu-id="fdf6e-138">Substitua `{tenant id}` com a ID de locatário do aplicativo do Active Directory do Azure que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-138">Replace `{tenant id}` with the tenant id of the Azure Active Directory application you just created.</span></span> <span data-ttu-id="fdf6e-139">Você pode acessar a ID clicando em **Exibir pontos de extremidade**.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-139">You can access the id by clicking **View endpoints**.</span></span>

![Pontos de extremidade][api-management-aad-default-directory]

![Pontos de extremidade][api-management-endpoint]

<span data-ttu-id="fdf6e-142">Substitua `{application id}` e `{redirect uri}` usando a **ID do cliente** e a URL da seção **URIs de Redirecionamento** da guia **Configurar** do aplicativo Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-142">Replace `{application id}` and `{redirect uri}` using the **Client Id** and  the URL from the **Redirect Uris** section from your Azure Active Directory application's **Configure** tab.</span></span>

![Recursos][api-management-aad-resources]

<span data-ttu-id="fdf6e-144">Depois que os valores são especificados, o exemplo de código deve retornar um token semelhante ao exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-144">Once the values are specified, the code example should return a token similar to the following example.</span></span>

![Token][api-management-arm-token]

<span data-ttu-id="fdf6e-146">Antes de chamar as operações de backup e restauração descritas nas seções a seguir, defina o cabeçalho de solicitação de autorização para a chamada de REST.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-146">Before calling the backup and restore operations described in the following sections, set the authorization request header for your REST call.</span></span>

```c#
request.Headers.Add(HttpRequestHeader.Authorization, "Bearer " + token);
```

## <span data-ttu-id="fdf6e-147"><a name="step1"> </a>Fazer backup de um serviço de Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="fdf6e-147"><a name="step1"> </a>Back up an API Management service</span></span>
<span data-ttu-id="fdf6e-148">Para fazer backup de um serviço de Gerenciamento de API, execute a seguinte solicitação HTTP:</span><span class="sxs-lookup"><span data-stu-id="fdf6e-148">To back up an API Management service issue the following HTTP request:</span></span>

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/backup?api-version={api-version}`

<span data-ttu-id="fdf6e-149">onde:</span><span class="sxs-lookup"><span data-stu-id="fdf6e-149">where:</span></span>

* <span data-ttu-id="fdf6e-150">`subscriptionId` - ID da assinatura contendo o serviço de Gerenciamento de API do qual você está tentando fazer backup</span><span class="sxs-lookup"><span data-stu-id="fdf6e-150">`subscriptionId` - id of the subscription containing the API Management service you are attempting to backup</span></span>
* <span data-ttu-id="fdf6e-151">`resourceGroupName` - uma cadeia de caracteres na forma de “Api-Default-{service-region}”, em que `service-region` identifica a região do Azure onde o serviço de Gerenciamento de API que você está tentando fazer backup é hospedado, por exemplo, `North-Central-US`</span><span class="sxs-lookup"><span data-stu-id="fdf6e-151">`resourceGroupName` - a string in the form of 'Api-Default-{service-region}' where `service-region` identifies the Azure region where the API Management service you are trying to backup is hosted, e.g. `North-Central-US`</span></span>
* <span data-ttu-id="fdf6e-152">`serviceName` - o nome do serviço de Gerenciamento de API que você está fazendo um backup em específico, no momento de sua criação</span><span class="sxs-lookup"><span data-stu-id="fdf6e-152">`serviceName` - the name of the API Management service you are making a backup of specified at the time of its creation</span></span>
* <span data-ttu-id="fdf6e-153">`api-version` - substitua por `2014-02-14`</span><span class="sxs-lookup"><span data-stu-id="fdf6e-153">`api-version` - replace  with `2014-02-14`</span></span>

<span data-ttu-id="fdf6e-154">No corpo da solicitação, especifique o nome da conta de armazenamento de destino do Azure, a chave de acesso, o nome do contêiner Blob e o nome de backup:</span><span class="sxs-lookup"><span data-stu-id="fdf6e-154">In the body of the request, specify the target Azure storage account name, access key, blob container name, and backup name:</span></span>

```
'{  
    storageAccount : {storage account name for the backup},  
    accessKey : {access key for the account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

<span data-ttu-id="fdf6e-155">Defina o valor do cabeçalho de solicitação `Content-Type` para `application/json`.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-155">Set the value of the `Content-Type` request header to `application/json`.</span></span>

<span data-ttu-id="fdf6e-156">O backup é uma operação longa de execução que pode levar vários minutos para concluir.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-156">Backup is a long running operation that may take multiple minutes to complete.</span></span>  <span data-ttu-id="fdf6e-157">Se a solicitação foi bem sucedida e o processo de backup foi iniciado, você receberá um código de status de resposta `202 Accepted` com um cabeçalho `Location`.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-157">If the request was successful and the backup process was initiated you’ll receive a `202 Accepted` response status code with a `Location` header.</span></span>  <span data-ttu-id="fdf6e-158">Faça solicitações “GET” para a URL no cabeçalho do `Location` para descobrir o status da operação.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-158">Make 'GET' requests to the URL in the `Location` header to find out the status of the operation.</span></span> <span data-ttu-id="fdf6e-159">Enquanto o backup está em andamento, você continuará a receber um código de status “202 Aceito”.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-159">While the backup is in progress you will continue to receive a '202 Accepted' status code.</span></span> <span data-ttu-id="fdf6e-160">Um código de resposta de `200 OK` indicará a conclusão com sucesso da operação de backup.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-160">A Response code of `200 OK` will indicate successful completion of the backup operation.</span></span>

<span data-ttu-id="fdf6e-161">Observe as restrições a seguir ao fazer uma solicitação de backup.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-161">Please note the following constraints when making a backup request.</span></span>

* <span data-ttu-id="fdf6e-162">O **contêiner** especificado no corpo solicitado **tem que existir**.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-162">**Container** specified in the request body **must exist**.</span></span>
* <span data-ttu-id="fdf6e-163">Enquanto o backup está em andamento, você **não deve tentar quaisquer operações de gerenciamento de serviço** , como atualização ou downgrade de SKU, alteração do nome do domínio, etc.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-163">While backup is in progress you **should not attempt any service management operations** such as SKU upgrade or downgrade, domain name change, etc.</span></span>
* <span data-ttu-id="fdf6e-164">A restauração de um **backup é garantida somente por 30 dias** desde o momento de sua criação.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-164">Restore of a **backup is guaranteed only for 30 days** since the moment of its creation.</span></span>
* <span data-ttu-id="fdf6e-165">Os **dados de uso** utilizados para a criação de relatórios de análise **não estão incluídos** no backup.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-165">**Usage data** used for creating analytics reports **is not included** in the backup.</span></span> <span data-ttu-id="fdf6e-166">Use o [API REST de Gerenciamento de API do Azure][Azure API Management REST API] para recuperar periodicamente os relatórios analíticos por questões de segurança.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-166">Use [Azure API Management REST API][Azure API Management REST API] to periodically retrieve analytics reports for safekeeping.</span></span>
* <span data-ttu-id="fdf6e-167">A frequência com que você executa os backups de serviço afetarão seu objetivo do ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-167">The frequency with which you perform service backups will affect your recovery point objective.</span></span> <span data-ttu-id="fdf6e-168">Para minimizar, aconselhamos a implementação de backups regular, bem como a execução de backups sob demanda depois de fazer alterações importantes para seu serviço de Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-168">To minimize it we advise implementing regular backups as well as performing on-demand backups after making important changes to your API Management service.</span></span>
* <span data-ttu-id="fdf6e-169">As **alterações** feitas à configuração de serviço (por exemplo, APIs, políticas, aparência do portal do desenvolvedor) enquanto a operação de backup está em andamento **podem não ser incluídas no backup e, portanto, serão perdidas**.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-169">**Changes** made to the service configuration (e.g. APIs, policies, developer portal appearance) while backup operation is in process **might not be included in the backup and therefore will be lost**.</span></span>

## <span data-ttu-id="fdf6e-170"><a name="step2"> </a>Restaurar um serviço de Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="fdf6e-170"><a name="step2"> </a>Restore an API Management service</span></span>
<span data-ttu-id="fdf6e-171">Para restaurar um serviço de Gerenciamento de API de um backup criado anteriormente faz a seguinte solicitação HTTP:</span><span class="sxs-lookup"><span data-stu-id="fdf6e-171">To restore an API Management service from a previously created backup make the following HTTP request:</span></span>

`POST https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/restore?api-version={api-version}`

<span data-ttu-id="fdf6e-172">onde:</span><span class="sxs-lookup"><span data-stu-id="fdf6e-172">where:</span></span>

* <span data-ttu-id="fdf6e-173">`subscriptionId` - ID da assinatura contendo o serviço de Gerenciamento de API que você está restaurando um backup em</span><span class="sxs-lookup"><span data-stu-id="fdf6e-173">`subscriptionId` - id of the subscription containing the API Management service you are restoring a backup into</span></span>
* <span data-ttu-id="fdf6e-174">`resourceGroupName` - uma cadeia de caracteres na forma de “Api-Default-{service-region}”, em que `service-region` identifica a região do Azure onde o serviço de Gerenciamento de API que você está restaurando é armazenado, por exemplo, `North-Central-US`</span><span class="sxs-lookup"><span data-stu-id="fdf6e-174">`resourceGroupName` - a string in the form of 'Api-Default-{service-region}' where `service-region` identifies the Azure region where the API Management service you are restoring a backup into is hosted, e.g. `North-Central-US`</span></span>
* <span data-ttu-id="fdf6e-175">`serviceName` - o nome do serviço de Gerenciamento de API para o qual está sendo realizada a restauração, especificado no momento de sua criação</span><span class="sxs-lookup"><span data-stu-id="fdf6e-175">`serviceName` - the name of the API Management service being restored into specified at the time of its creation</span></span>
* <span data-ttu-id="fdf6e-176">`api-version` - substitua por `2014-02-14`</span><span class="sxs-lookup"><span data-stu-id="fdf6e-176">`api-version` - replace  with `2014-02-14`</span></span>

<span data-ttu-id="fdf6e-177">No corpo da solicitação, especifique o local de arquivo de backup, por exemplo, o nome da conta de armazenamento do Azure, chave de acesso, nome do contêiner Blob e nome de backup:</span><span class="sxs-lookup"><span data-stu-id="fdf6e-177">In the body of the request, specify the backup file location, i.e. Azure storage account name, access key, blob container name, and backup name:</span></span>

```
'{  
    storageAccount : {storage account name for the backup},  
    accessKey : {access key for the account},  
    containerName : {backup container name},  
    backupName : {backup blob name}  
}'
```

<span data-ttu-id="fdf6e-178">Defina o valor do cabeçalho de solicitação `Content-Type` para `application/json`.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-178">Set the value of the `Content-Type` request header to `application/json`.</span></span>

<span data-ttu-id="fdf6e-179">Restaure uma operação longa de execução que pode levar até 30 minutos ou mais para concluir.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-179">Restore is a long running operation that may take up to 30 or more minutes to complete.</span></span>  <span data-ttu-id="fdf6e-180">Se a solicitação foi bem sucedida e o processo de restauração foi iniciado, você receberá um código de status de resposta `202 Accepted` com um cabeçalho do `Location`.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-180">If the request was successful and the restore process was initiated you’ll receive a `202 Accepted` response status code with a `Location` header.</span></span>  <span data-ttu-id="fdf6e-181">Faça solicitações “GET” para a URL no cabeçalho do `Location` para descobrir o status da operação.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-181">Make 'GET' requests to the URL in the `Location` header to find out the status of the operation.</span></span> <span data-ttu-id="fdf6e-182">Enquanto a restauração está em andamento, você continuará a receber o código de status “202 Aceito”.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-182">While the restore is in progress you will continue to receive '202 Accepted' status code.</span></span> <span data-ttu-id="fdf6e-183">Um código de resposta `200 OK` indicará a conclusão com sucesso da operação de restauração.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-183">A response code of `200 OK` will indicate successful completion of the restore operation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fdf6e-184">**O SKU** do serviço que está sendo restaurado **tem que corresponder** ao SKU do serviço de backup sendo restaurado.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-184">**The SKU** of the service being restored into **must match** the SKU of the backed up service being restored.</span></span>
>
> <span data-ttu-id="fdf6e-185">As **alterações** feitas na configuração do serviço (por exemplo, APIs, políticas, aparência do portal do desenvolvedor) enquanto restauram a operação que está em andamento **podem ser substituídas**.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-185">**Changes** made to the service configuration (e.g. APIs, policies, developer portal appearance) while restore operation is in progress **could be overwritten**.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="fdf6e-186">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fdf6e-186">Next steps</span></span>
<span data-ttu-id="fdf6e-187">Confira os seguintes blogs da Microsoft para duas diferentes orientações passo a passo do processo de backup/restauração.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-187">Check out the following Microsoft blogs for two different walkthroughs of the backup/restore process.</span></span>

* [<span data-ttu-id="fdf6e-188">Replicar contas de Gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="fdf6e-188">Replicate Azure API Management Accounts</span></span>](https://www.returngis.net/en/2015/06/replicate-azure-api-management-accounts/)
  * <span data-ttu-id="fdf6e-189">Agradecemos a Gisela por sua contribuição neste artigo.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-189">Thank you to Gisela for her contribution to this article.</span></span>
* [<span data-ttu-id="fdf6e-190">Gerenciamento de API do Azure: Fazendo backup e restaurando a configuração</span><span class="sxs-lookup"><span data-stu-id="fdf6e-190">Azure API Management: Backing Up and Restoring Configuration</span></span>](http://blogs.msdn.com/b/stuartleeks/archive/2015/04/29/azure-api-management-backing-up-and-restoring-configuration.aspx)
  * <span data-ttu-id="fdf6e-191">A abordagem detalhada por Stuart não coincide com as diretrizes oficiais, mas é muito interessante.</span><span class="sxs-lookup"><span data-stu-id="fdf6e-191">The approach detailed by Stuart does not match the official guidance but it is very interesting.</span></span>

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
