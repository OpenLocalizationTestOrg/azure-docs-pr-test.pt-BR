---
title: "zonas DNS aaaCreate e conjuntos de registros DNS do Azure usando Olá .NET SDK | Microsoft Docs"
description: "Como registro e zonas DNS toocreate define no DNS do Azure usando o SDK .NET de saudação."
services: dns
documentationcenter: na
author: jtuliani
manager: carmonm
ms.assetid: eed99b87-f4d4-4fbf-a926-263f7e30b884
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/19/2016
ms.author: jonatul
ms.openlocfilehash: e3bab98b13b787427219acb7ec55e53490512fe7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-dns-zones-and-record-sets-using-hello-net-sdk"></a><span data-ttu-id="f5cf9-103">Criar zonas DNS e conjuntos de registros usando o SDK .NET de saudação</span><span class="sxs-lookup"><span data-stu-id="f5cf9-103">Create DNS zones and record sets using hello .NET SDK</span></span>

<span data-ttu-id="f5cf9-104">Você pode automatizar operações toocreate, excluir ou atualizar zonas de DNS, os conjuntos de registro e registros usando o SDK do DNS com biblioteca de gerenciamento de DNS do .NET.</span><span class="sxs-lookup"><span data-stu-id="f5cf9-104">You can automate operations toocreate, delete, or update DNS zones, record sets, and records by using DNS SDK with .NET DNS Management library.</span></span> <span data-ttu-id="f5cf9-105">Um projeto completo do Visual Studio está disponível [aqui.](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True)</span><span class="sxs-lookup"><span data-stu-id="f5cf9-105">A full Visual Studio project is available [here.](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True)</span></span>

## <a name="create-a-service-principal-account"></a><span data-ttu-id="f5cf9-106">Crie uma conta da entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="f5cf9-106">Create a service principal account</span></span>

<span data-ttu-id="f5cf9-107">Normalmente, os recursos do acesso programático tooAzure é concedida por meio de uma conta dedicada em vez de suas próprias credenciais de usuário.</span><span class="sxs-lookup"><span data-stu-id="f5cf9-107">Typically, programmatic access tooAzure resources is granted via a dedicated account rather than your own user credentials.</span></span> <span data-ttu-id="f5cf9-108">Essas contas dedicadas são denominadas contas da 'entidade de serviço'.</span><span class="sxs-lookup"><span data-stu-id="f5cf9-108">These dedicated accounts are called 'service principal' accounts.</span></span> <span data-ttu-id="f5cf9-109">projeto de exemplo hello toouse DNS do SDK do Azure, você primeiro precisa de uma conta de serviço principal de toocreate e atribui permissões corretas hello.</span><span class="sxs-lookup"><span data-stu-id="f5cf9-109">toouse hello Azure DNS SDK sample project, you first need toocreate a service principal account and assign it hello correct permissions.</span></span>

1. <span data-ttu-id="f5cf9-110">Execute [estas instruções](../azure-resource-manager/resource-group-authenticate-service-principal.md) toocreate uma conta de serviço principal (projeto de exemplo do SDK do Azure DNS Olá pressupõe a autenticação baseada em senha).</span><span class="sxs-lookup"><span data-stu-id="f5cf9-110">Follow [these instructions](../azure-resource-manager/resource-group-authenticate-service-principal.md) toocreate a service principal account (hello Azure DNS SDK sample project assumes password-based authentication.)</span></span>
2. <span data-ttu-id="f5cf9-111">Crie um grupo de recursos ([aqui](../azure-resource-manager/resource-group-template-deploy-portal.md)).</span><span class="sxs-lookup"><span data-stu-id="f5cf9-111">Create a resource group ([here's how](../azure-resource-manager/resource-group-template-deploy-portal.md)).</span></span>
3. <span data-ttu-id="f5cf9-112">Use o RBAC do Azure toogrant Olá serviço conta principal 'Colaborador de zona DNS' permissões toohello grupo de recursos ([aqui está como](../active-directory/role-based-access-control-configure.md).)</span><span class="sxs-lookup"><span data-stu-id="f5cf9-112">Use Azure RBAC toogrant hello service principal account 'DNS Zone Contributor' permissions toohello resource group ([here's how](../active-directory/role-based-access-control-configure.md).)</span></span>
4. <span data-ttu-id="f5cf9-113">Se usando o projeto de exemplo do SDK do Azure DNS hello, edite o arquivo de 'program.cs' de saudação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="f5cf9-113">If using hello Azure DNS SDK sample project, edit hello 'program.cs' file as follows:</span></span>

   * <span data-ttu-id="f5cf9-114">Inserir valores corretos Olá Olá tenantId, clientId (também conhecido como a ID de conta), segredo (senha de conta de entidade de serviço) e subscriptionId conforme usado na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="f5cf9-114">Insert hello correct values for hello tenantId, clientId (also known as account ID), secret (service principal account password) and subscriptionId as used in step 1.</span></span>
   * <span data-ttu-id="f5cf9-115">Insira o nome do grupo de recursos Olá escolhido na etapa 2.</span><span class="sxs-lookup"><span data-stu-id="f5cf9-115">Enter hello resource group name chosen in step 2.</span></span>
   * <span data-ttu-id="f5cf9-116">Insira um nome de zona do DNS de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="f5cf9-116">Enter a DNS zone name of your choice.</span></span>

## <a name="nuget-packages-and-namespace-declarations"></a><span data-ttu-id="f5cf9-117">Pacotes NuGet e declarações de namespace</span><span class="sxs-lookup"><span data-stu-id="f5cf9-117">NuGet packages and namespace declarations</span></span>

<span data-ttu-id="f5cf9-118">toouse Olá DNS do Azure .NET SDK, você precisa Olá tooinstall **biblioteca de gerenciamento do DNS do Azure** pacote NuGet e outros necessários pacotes do Azure.</span><span class="sxs-lookup"><span data-stu-id="f5cf9-118">toouse hello Azure DNS .NET SDK, you need tooinstall hello **Azure DNS Management Library** NuGet package and other required Azure packages.</span></span>

1. <span data-ttu-id="f5cf9-119">No **Visual Studio**, abra um projeto ou um novo projeto.</span><span class="sxs-lookup"><span data-stu-id="f5cf9-119">In **Visual Studio**, open a project or new project.</span></span>
2. <span data-ttu-id="f5cf9-120">Vá muito**ferramentas**  **>**  **NuGet Package Manager**  **>**  **gerenciar pacotes NuGet para Solução...** .</span><span class="sxs-lookup"><span data-stu-id="f5cf9-120">Go too**Tools** **>** **NuGet Package Manager** **>** **Manage NuGet Packages for Solution...**.</span></span>
3. <span data-ttu-id="f5cf9-121">Clique em **procurar**, habilitar Olá **incluir pré-lançamento** caixa de seleção e digite **Microsoft.Azure.Management.Dns** na caixa de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="f5cf9-121">Click **Browse**, enable hello **Include prerelease** checkbox, and type **Microsoft.Azure.Management.Dns** in hello search box.</span></span>
4. <span data-ttu-id="f5cf9-122">Selecione o pacote de saudação e clique em **instalar** tooadd-tooyour o projeto do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f5cf9-122">Select hello package and click **Install** tooadd it tooyour Visual Studio project.</span></span>
5. <span data-ttu-id="f5cf9-123">Repetir o processo de saudação acima tooalso instalação Olá pacotes a seguir: **Microsoft.Rest.ClientRuntime.Azure.Authentication** e **Microsoft.Azure.Management.ResourceManager**.</span><span class="sxs-lookup"><span data-stu-id="f5cf9-123">Repeat hello process above tooalso install hello following packages: **Microsoft.Rest.ClientRuntime.Azure.Authentication** and **Microsoft.Azure.Management.ResourceManager**.</span></span>

## <a name="add-namespace-declarations"></a><span data-ttu-id="f5cf9-124">Adicionar declarações do namespace</span><span class="sxs-lookup"><span data-stu-id="f5cf9-124">Add namespace declarations</span></span>

<span data-ttu-id="f5cf9-125">Adicionar Olá seguir declarações de namespace</span><span class="sxs-lookup"><span data-stu-id="f5cf9-125">Add hello following namespace declarations</span></span>

```cs
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.Dns;
using Microsoft.Azure.Management.Dns.Models;
```

## <a name="initialize-hello-dns-management-client"></a><span data-ttu-id="f5cf9-126">Inicializar o cliente de gerenciamento de DNS Olá</span><span class="sxs-lookup"><span data-stu-id="f5cf9-126">Initialize hello DNS management client</span></span>

<span data-ttu-id="f5cf9-127">Olá *DnsManagementClient* contém métodos de saudação e as propriedades necessárias para o gerenciamento de zonas DNS e conjuntos de registros.</span><span class="sxs-lookup"><span data-stu-id="f5cf9-127">hello *DnsManagementClient* contains hello methods and properties necessary for managing DNS zones and recordsets.</span></span>  <span data-ttu-id="f5cf9-128">Olá código a seguir registra na conta de serviço principal toohello e cria um objeto DnsManagementClient.</span><span class="sxs-lookup"><span data-stu-id="f5cf9-128">hello following code logs in toohello service principal account and creates a DnsManagementClient object.</span></span>

```cs
// Build hello service credentials and DNS management client
var serviceCreds = await ApplicationTokenProvider.LoginSilentAsync(tenantId, clientId, secret);
var dnsClient = new DnsManagementClient(serviceCreds);
dnsClient.SubscriptionId = subscriptionId;
```

## <a name="create-or-update-a-dns-zone"></a><span data-ttu-id="f5cf9-129">Criar ou atualizar uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="f5cf9-129">Create or update a DNS zone</span></span>

<span data-ttu-id="f5cf9-130">toocreate uma zona DNS, primeiro um objeto "Zone" é criado parâmetros de zona do DNS do toocontain hello.</span><span class="sxs-lookup"><span data-stu-id="f5cf9-130">toocreate a DNS zone, first a "Zone" object is created toocontain hello DNS zone parameters.</span></span> <span data-ttu-id="f5cf9-131">Como as zonas DNS não são região específica tooa vinculado, o local de saudação é definido too'global'.</span><span class="sxs-lookup"><span data-stu-id="f5cf9-131">Because DNS zones are not linked tooa specific region, hello location is set too'global'.</span></span> <span data-ttu-id="f5cf9-132">Neste exemplo, um [do Azure Resource Manager 'tag'](https://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/) também é adicionado toohello zona.</span><span class="sxs-lookup"><span data-stu-id="f5cf9-132">In this example, an [Azure Resource Manager 'tag'](https://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/) is also added toohello zone.</span></span>

<span data-ttu-id="f5cf9-133">tooactually criar ou atualizar Olá zona no DNS do Azure, que contém parâmetros de zona de saudação de objeto de zona Olá é passada toohello *DnsManagementClient.Zones.CreateOrUpdateAsyc* método.</span><span class="sxs-lookup"><span data-stu-id="f5cf9-133">tooactually create or update hello zone in Azure DNS, hello zone object containing hello zone parameters is passed toohello *DnsManagementClient.Zones.CreateOrUpdateAsyc* method.</span></span>

> [!NOTE]
> <span data-ttu-id="f5cf9-134">DnsManagementClient oferece suporte a três modos de operação: síncrono ('CreateOrUpdate'), assíncrona ('CreateOrUpdateAsync'), ou assíncrono com a resposta HTTP de toohello de acesso ('CreateOrUpdateWithHttpMessagesAsync').</span><span class="sxs-lookup"><span data-stu-id="f5cf9-134">DnsManagementClient supports three modes of operation: synchronous ('CreateOrUpdate'), asynchronous ('CreateOrUpdateAsync'), or asynchronous with access toohello HTTP response ('CreateOrUpdateWithHttpMessagesAsync').</span></span>  <span data-ttu-id="f5cf9-135">Você pode escolher qualquer um desses modos, dependendo das necessidades de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f5cf9-135">You can choose any of these modes, depending on your application needs.</span></span>

<span data-ttu-id="f5cf9-136">O DNS do Azure dá suporte a [Etags](dns-getstarted-create-dnszone.md)de simultaneidade otimista.</span><span class="sxs-lookup"><span data-stu-id="f5cf9-136">Azure DNS supports optimistic concurrency, called [Etags](dns-getstarted-create-dnszone.md).</span></span> <span data-ttu-id="f5cf9-137">Neste exemplo, especificando "*" para o cabeçalho de saudação 'If-None-Match' informa toocreate DNS do Azure uma zona DNS se ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="f5cf9-137">In this example, specifying "*" for hello 'If-None-Match' header tells Azure DNS toocreate a DNS zone if one does not already exist.</span></span>  <span data-ttu-id="f5cf9-138">chamada de saudação falhará se uma zona com o nome do hello fornecido já existe no hello fornecido o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f5cf9-138">hello call fails if a zone with hello given name already exists in hello given resource group.</span></span>

```cs
// Create zone parameters
var dnsZoneParams = new Zone("global"); // All DNS zones must have location = "global"

// Create a Azure Resource Manager 'tag'.  This is optional.  You can add multiple tags
dnsZoneParams.Tags = new Dictionary<string, string>();
dnsZoneParams.Tags.Add("dept", "finance");

// Create hello actual zone.
// Note: Uses 'If-None-Match *' ETAG check, so will fail if hello zone exists already.
// Note: For non-async usage, call dnsClient.Zones.CreateOrUpdate(resourceGroupName, zoneName, dnsZoneParams, null, "*")
// Note: For getting hello http response, call dnsClient.Zones.CreateOrUpdateWithHttpMessagesAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*")
var dnsZone = await dnsClient.Zones.CreateOrUpdateAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*");
```

## <a name="create-dns-record-sets-and-records"></a><span data-ttu-id="f5cf9-139">Criar conjuntos de registros DNS e registros</span><span class="sxs-lookup"><span data-stu-id="f5cf9-139">Create DNS record sets and records</span></span>

<span data-ttu-id="f5cf9-140">Os registros DNS são gerenciados como um conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="f5cf9-140">DNS records are managed as a record set.</span></span> <span data-ttu-id="f5cf9-141">Um conjunto de registros é um conjunto de registros com hello mesmo nome e registre tipo dentro de uma zona.</span><span class="sxs-lookup"><span data-stu-id="f5cf9-141">A record set is a set of records with hello same name and record type within a zone.</span></span>  <span data-ttu-id="f5cf9-142">nome do conjunto de registros de saudação é nome da zona toohello relativo, Olá não o nome DNS totalmente qualificado.</span><span class="sxs-lookup"><span data-stu-id="f5cf9-142">hello record set name is relative toohello zone name, not hello fully qualified DNS name.</span></span>

<span data-ttu-id="f5cf9-143">toocreate ou atualizar um conjunto de registros, um objeto de parâmetros "RecordSet" é criado e transmitido muito*DnsManagementClient.RecordSets.CreateOrUpdateAsync*.</span><span class="sxs-lookup"><span data-stu-id="f5cf9-143">toocreate or update a record set, a "RecordSet" parameters object is created and passed too*DnsManagementClient.RecordSets.CreateOrUpdateAsync*.</span></span> <span data-ttu-id="f5cf9-144">Como com as zonas DNS, há três modos de operação: síncrono ('CreateOrUpdate'), assíncrona ('CreateOrUpdateAsync'), ou assíncrono com a resposta HTTP de toohello de acesso ('CreateOrUpdateWithHttpMessagesAsync').</span><span class="sxs-lookup"><span data-stu-id="f5cf9-144">As with DNS zones, there are three modes of operation: synchronous ('CreateOrUpdate'), asynchronous ('CreateOrUpdateAsync'), or asynchronous with access toohello HTTP response ('CreateOrUpdateWithHttpMessagesAsync').</span></span>

<span data-ttu-id="f5cf9-145">Como nas zonas DNS, as operações nos conjuntos de registros incluem suporte para a simultaneidade otimista.</span><span class="sxs-lookup"><span data-stu-id="f5cf9-145">As with DNS zones, operations on record sets include support for optimistic concurrency.</span></span>  <span data-ttu-id="f5cf9-146">Neste exemplo, pois nem 'If-Match' nem 'If-None-Match' for especificado, o conjunto de registros Olá sempre é criado.</span><span class="sxs-lookup"><span data-stu-id="f5cf9-146">In this example, since neither 'If-Match' nor 'If-None-Match' are specified, hello record set is always created.</span></span>  <span data-ttu-id="f5cf9-147">Essa chamada substitui qualquer registro existente com hello mesmo nome e registre o tipo desta zona DNS.</span><span class="sxs-lookup"><span data-stu-id="f5cf9-147">This call overwrites any existing record set with hello same name and record type in this DNS zone.</span></span>

```cs
// Create record set parameters
var recordSetParams = new RecordSet();
recordSetParams.TTL = 3600;

// Add records toohello record set parameter object.  In this case, we'll add a record of type 'A'
recordSetParams.ARecords = new List<ARecord>();
recordSetParams.ARecords.Add(new ARecord("1.2.3.4"));

// Add metadata toohello record set.  Similar tooAzure Resource Manager tags, this is optional and you can add multiple metadata name/value pairs
recordSetParams.Metadata = new Dictionary<string, string>();
recordSetParams.Metadata.Add("user", "Mary");

// Create hello actual record set in Azure DNS
// Note: no ETAG checks specified, will overwrite existing record set if one exists
var recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSetParams);
```

## <a name="get-zones-and-record-sets"></a><span data-ttu-id="f5cf9-148">Obter zonas e conjuntos de registros</span><span class="sxs-lookup"><span data-stu-id="f5cf9-148">Get zones and record sets</span></span>

<span data-ttu-id="f5cf9-149">Olá *DnsManagementClient.Zones.Get* e *DnsManagementClient.RecordSets.Get* métodos recuperem regiões individuais e conjuntos de registros, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="f5cf9-149">hello *DnsManagementClient.Zones.Get* and *DnsManagementClient.RecordSets.Get* methods retrieve individual zones and record sets, respectively.</span></span> <span data-ttu-id="f5cf9-150">Conjuntos de registros são identificados por seu tipo, o nome e a saudação zona e grupo de recursos existam no.</span><span class="sxs-lookup"><span data-stu-id="f5cf9-150">RecordSets are identified by their type, name, and hello zone and resource group they exist in.</span></span> <span data-ttu-id="f5cf9-151">As zonas são identificadas por seu grupo de recursos de nome e hello existirem no.</span><span class="sxs-lookup"><span data-stu-id="f5cf9-151">Zones are identified by their name and hello resource group they exist in.</span></span>

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);
```

## <a name="update-an-existing-record-set"></a><span data-ttu-id="f5cf9-152">Atualizar um conjunto de registros existente</span><span class="sxs-lookup"><span data-stu-id="f5cf9-152">Update an existing record set</span></span>

<span data-ttu-id="f5cf9-153">tooupdate um registro DNS existente definido, recuperar primeiro conjunto de registros Olá, e em seguida, atualizar Olá registro o conteúdo do conjunto, em seguida, enviar alterações hello.</span><span class="sxs-lookup"><span data-stu-id="f5cf9-153">tooupdate an existing DNS record set, first retrieve hello record set, then update hello record set contents, then submit hello change.</span></span>  <span data-ttu-id="f5cf9-154">Neste exemplo, podemos especificar Olá que ETag da saudação recuperados registro definido no parâmetro de 'If-Match' hello.</span><span class="sxs-lookup"><span data-stu-id="f5cf9-154">In this example, we specify hello 'Etag' from hello retrieved record set in hello 'If-Match' parameter.</span></span> <span data-ttu-id="f5cf9-155">chamada de saudação falhará se uma operação simultânea modificou Olá conjunto de registros em Olá enquanto isso.</span><span class="sxs-lookup"><span data-stu-id="f5cf9-155">hello call fails if a concurrent operation has modified hello record set in hello meantime.</span></span>

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);

// Add a new record toohello local object.  Note that records in a record set must be unique/distinct
recordSet.ARecords.Add(new ARecord("5.6.7.8"));

// Update hello record set in Azure DNS
// Note: ETAG check specified, update will be rejected if hello record set has changed in hello meantime
recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSet, recordSet.Etag);
```

## <a name="list-zones-and-record-sets"></a><span data-ttu-id="f5cf9-156">Listar zonas e conjuntos de registros</span><span class="sxs-lookup"><span data-stu-id="f5cf9-156">List zones and record sets</span></span>

<span data-ttu-id="f5cf9-157">zonas de toolist, use Olá *DnsManagementClient.Zones.List...*  métodos, que oferece suporte a listagem a todas as zonas em um grupo de recursos determinado ou todas as zonas em conjuntos de registros de toolist uma determinada assinatura do Azure (em arquivos de recursos grupos.), usem *DnsManagementClient.RecordSets.List...*  métodos, que oferece suporte a listando todos os conjuntos de registros em uma determinada região ou apenas os conjuntos de registros de um tipo específico.</span><span class="sxs-lookup"><span data-stu-id="f5cf9-157">toolist zones, use hello *DnsManagementClient.Zones.List...* methods, which support listing either all zones in a given resource group or all zones in a given Azure subscription (across resource groups.) toolist record sets, use *DnsManagementClient.RecordSets.List...* methods, which support either listing all record sets in a given zone or only those record sets of a specific type.</span></span>

<span data-ttu-id="f5cf9-158">Observe que ao listar as zonas e os conjuntos de registros, isso resulta em uma paginação.</span><span class="sxs-lookup"><span data-stu-id="f5cf9-158">Note when listing zones and record sets that results may be paginated.</span></span>  <span data-ttu-id="f5cf9-159">Olá mostrado no exemplo a seguir como tooiterate por meio de páginas de saudação de resultados.</span><span class="sxs-lookup"><span data-stu-id="f5cf9-159">hello following example shows how tooiterate through hello pages of results.</span></span> <span data-ttu-id="f5cf9-160">(Um tamanho de página artificialmente pequeno '2' é usado tooforce paginação; na prática, esse parâmetro deve ser omitido e Olá tamanho de página padrão usado).</span><span class="sxs-lookup"><span data-stu-id="f5cf9-160">(An artificially small page size of '2' is used tooforce paging; in practice this parameter should be omitted and hello default page size used.)</span></span>

```cs
// Note: in this demo, we'll use a very small page size (2 record sets) toodemonstrate paging
// In practice, tooimprove performance you would use a large page size or just use hello system default
int recordSets = 0;
var page = await dnsClient.RecordSets.ListAllInResourceGroupAsync(resourceGroupName, zoneName, "2");
recordSets += page.Count();

while (page.NextPageLink != null)
{
    page = await dnsClient.RecordSets.ListAllInResourceGroupNextAsync(page.NextPageLink);
    recordSets += page.Count();
}
```

## <a name="next-steps"></a><span data-ttu-id="f5cf9-161">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f5cf9-161">Next steps</span></span>

<span data-ttu-id="f5cf9-162">Baixar Olá [projeto de exemplo do SDK do Azure DNS .NET](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True), que inclui mais exemplos de como toouse Olá SDK .NET DNS do Azure, incluindo exemplos para outros tipos de registros de DNS.</span><span class="sxs-lookup"><span data-stu-id="f5cf9-162">Download hello [Azure DNS .NET SDK sample project](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True), which includes further examples of how toouse hello Azure DNS .NET SDK, including examples for other DNS record types.</span></span>
