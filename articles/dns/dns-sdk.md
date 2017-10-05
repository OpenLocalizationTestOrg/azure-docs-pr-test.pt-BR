---
title: Criar zonas DNS e conjuntos de registros no DNS do Azure usando o SDK do .NET | Microsoft Docs
description: Como criar zonas DNS e conjuntos de registros no DNS do Azure usando o SDK do .NET.
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
ms.openlocfilehash: c0fb0be8da1c0ca48a4d43ea027d30a0bc17fe30
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-dns-zones-and-record-sets-using-the-net-sdk"></a><span data-ttu-id="33402-103">Criar zonas DNS e conjuntos de registros usando o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="33402-103">Create DNS zones and record sets using the .NET SDK</span></span>

<span data-ttu-id="33402-104">Você pode automatizar operações para criar, excluir ou atualizar zonas DNS, conjuntos de registros e registros usando o SDK do DNS com a biblioteca de gerenciamento do DNS .NET.</span><span class="sxs-lookup"><span data-stu-id="33402-104">You can automate operations to create, delete, or update DNS zones, record sets, and records by using DNS SDK with .NET DNS Management library.</span></span> <span data-ttu-id="33402-105">Um projeto completo do Visual Studio está disponível [aqui.](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True)</span><span class="sxs-lookup"><span data-stu-id="33402-105">A full Visual Studio project is available [here.](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True)</span></span>

## <a name="create-a-service-principal-account"></a><span data-ttu-id="33402-106">Crie uma conta da entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="33402-106">Create a service principal account</span></span>

<span data-ttu-id="33402-107">Normalmente, o acesso programático aos recursos do Azure é concedido por meio de uma conta dedicada, em vez de suas próprias credenciais de usuário.</span><span class="sxs-lookup"><span data-stu-id="33402-107">Typically, programmatic access to Azure resources is granted via a dedicated account rather than your own user credentials.</span></span> <span data-ttu-id="33402-108">Essas contas dedicadas são denominadas contas da 'entidade de serviço'.</span><span class="sxs-lookup"><span data-stu-id="33402-108">These dedicated accounts are called 'service principal' accounts.</span></span> <span data-ttu-id="33402-109">Para usar o projeto de exemplo SDK do DNS do Azure, você precisa primeiro criar uma conta da entidade de serviço e atribuir as permissões corretas.</span><span class="sxs-lookup"><span data-stu-id="33402-109">To use the Azure DNS SDK sample project, you first need to create a service principal account and assign it the correct permissions.</span></span>

1. <span data-ttu-id="33402-110">Siga [estas instruções](../azure-resource-manager/resource-group-authenticate-service-principal.md) para criar uma conta da entidade de serviço (o projeto de exemplo SDK do DNS do Azure pressupõe uma autenticação baseada em senhas.)</span><span class="sxs-lookup"><span data-stu-id="33402-110">Follow [these instructions](../azure-resource-manager/resource-group-authenticate-service-principal.md) to create a service principal account (the Azure DNS SDK sample project assumes password-based authentication.)</span></span>
2. <span data-ttu-id="33402-111">Crie um grupo de recursos ([aqui](../azure-resource-manager/resource-group-template-deploy-portal.md)).</span><span class="sxs-lookup"><span data-stu-id="33402-111">Create a resource group ([here's how](../azure-resource-manager/resource-group-template-deploy-portal.md)).</span></span>
3. <span data-ttu-id="33402-112">Use o RBAC do Azure para conceder à conta da entidade de serviço permissões do 'Colaborador da Zona DNS' para o grupo de recursos ([aqui](../active-directory/role-based-access-control-configure.md).)</span><span class="sxs-lookup"><span data-stu-id="33402-112">Use Azure RBAC to grant the service principal account 'DNS Zone Contributor' permissions to the resource group ([here's how](../active-directory/role-based-access-control-configure.md).)</span></span>
4. <span data-ttu-id="33402-113">Se você usar o projeto de exemplo SDK do DNS do Azure, edite o arquivo 'program.cs' como a seguir:</span><span class="sxs-lookup"><span data-stu-id="33402-113">If using the Azure DNS SDK sample project, edit the 'program.cs' file as follows:</span></span>

   * <span data-ttu-id="33402-114">Insira os valores corretos para tenantId, clientId (também conhecida como ID da conta), secret (senha da conta da entidade de serviço) e subscriptionId, como usados na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="33402-114">Insert the correct values for the tenantId, clientId (also known as account ID), secret (service principal account password) and subscriptionId as used in step 1.</span></span>
   * <span data-ttu-id="33402-115">Insira o nome do grupo de recursos escolhido na etapa 2.</span><span class="sxs-lookup"><span data-stu-id="33402-115">Enter the resource group name chosen in step 2.</span></span>
   * <span data-ttu-id="33402-116">Insira um nome de zona do DNS de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="33402-116">Enter a DNS zone name of your choice.</span></span>

## <a name="nuget-packages-and-namespace-declarations"></a><span data-ttu-id="33402-117">Pacotes NuGet e declarações de namespace</span><span class="sxs-lookup"><span data-stu-id="33402-117">NuGet packages and namespace declarations</span></span>

<span data-ttu-id="33402-118">Para usar o SDK do .NET de DNS, você precisa instalar o pacote NuGet da **Biblioteca de Gerenciamento de DNS do Azure** e outros pacotes do Azure requeridos.</span><span class="sxs-lookup"><span data-stu-id="33402-118">To use the Azure DNS .NET SDK, you need to install the **Azure DNS Management Library** NuGet package and other required Azure packages.</span></span>

1. <span data-ttu-id="33402-119">No **Visual Studio**, abra um projeto ou um novo projeto.</span><span class="sxs-lookup"><span data-stu-id="33402-119">In **Visual Studio**, open a project or new project.</span></span>
2. <span data-ttu-id="33402-120">Acesse **Ferramentas** **>** **Gerenciamento de Pacotes NuGet** **>** **Gerenciar Pacotes NuGet para Solução...**.</span><span class="sxs-lookup"><span data-stu-id="33402-120">Go to **Tools** **>** **NuGet Package Manager** **>** **Manage NuGet Packages for Solution...**.</span></span>
3. <span data-ttu-id="33402-121">Clique em **Procurar**, marque a caixa de seleção **Incluir pré-lançamento** e digite **Microsoft.Azure.Management.Dns** na caixa de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="33402-121">Click **Browse**, enable the **Include prerelease** checkbox, and type **Microsoft.Azure.Management.Dns** in the search box.</span></span>
4. <span data-ttu-id="33402-122">Selecione o pacote e clique em **Instalar** adicioná-lo a seu projeto do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="33402-122">Select the package and click **Install** to add it to your Visual Studio project.</span></span>
5. <span data-ttu-id="33402-123">Repita o processo acima para também instalar os seguintes pacotes: **Microsoft.Rest.ClientRuntime.Azure.Authentication** e **Microsoft.Azure.Management.ResourceManager**.</span><span class="sxs-lookup"><span data-stu-id="33402-123">Repeat the process above to also install the following packages: **Microsoft.Rest.ClientRuntime.Azure.Authentication** and **Microsoft.Azure.Management.ResourceManager**.</span></span>

## <a name="add-namespace-declarations"></a><span data-ttu-id="33402-124">Adicionar declarações do namespace</span><span class="sxs-lookup"><span data-stu-id="33402-124">Add namespace declarations</span></span>

<span data-ttu-id="33402-125">Adicionar as declarações do namespace a seguir</span><span class="sxs-lookup"><span data-stu-id="33402-125">Add the following namespace declarations</span></span>

```cs
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.Dns;
using Microsoft.Azure.Management.Dns.Models;
```

## <a name="initialize-the-dns-management-client"></a><span data-ttu-id="33402-126">Inicializar o cliente de gerenciamento do DNS</span><span class="sxs-lookup"><span data-stu-id="33402-126">Initialize the DNS management client</span></span>

<span data-ttu-id="33402-127">*DnsManagementClient* contém os métodos e as propriedades necessárias para gerenciar conjuntos de registros e zonas DNS.</span><span class="sxs-lookup"><span data-stu-id="33402-127">The *DnsManagementClient* contains the methods and properties necessary for managing DNS zones and recordsets.</span></span>  <span data-ttu-id="33402-128">O código a seguir faz logon na conta da entidade de serviço e cria um objeto DnsManagementClient.</span><span class="sxs-lookup"><span data-stu-id="33402-128">The following code logs in to the service principal account and creates a DnsManagementClient object.</span></span>

```cs
// Build the service credentials and DNS management client
var serviceCreds = await ApplicationTokenProvider.LoginSilentAsync(tenantId, clientId, secret);
var dnsClient = new DnsManagementClient(serviceCreds);
dnsClient.SubscriptionId = subscriptionId;
```

## <a name="create-or-update-a-dns-zone"></a><span data-ttu-id="33402-129">Criar ou atualizar uma zona DNS</span><span class="sxs-lookup"><span data-stu-id="33402-129">Create or update a DNS zone</span></span>

<span data-ttu-id="33402-130">Para criar uma zona DNS, primeiro é criado um objeto "Zona" para conter os parâmetros de zona do DNS.</span><span class="sxs-lookup"><span data-stu-id="33402-130">To create a DNS zone, first a "Zone" object is created to contain the DNS zone parameters.</span></span> <span data-ttu-id="33402-131">Como as zonas do DNS não estão vinculadas a uma região específica, o local é definido para ‘global’.</span><span class="sxs-lookup"><span data-stu-id="33402-131">Because DNS zones are not linked to a specific region, the location is set to 'global'.</span></span> <span data-ttu-id="33402-132">Neste exemplo, uma [’marcação’ Azure Resource Manager](https://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/) também é adicionada à zona.</span><span class="sxs-lookup"><span data-stu-id="33402-132">In this example, an [Azure Resource Manager 'tag'](https://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/) is also added to the zone.</span></span>

<span data-ttu-id="33402-133">Para realmente criar ou atualizar a zona no DNS do Azure, o objeto de zona que contém os parâmetros da zona é passado para o método *DnsManagementClient.Zones.CreateOrUpdateAsyc* .</span><span class="sxs-lookup"><span data-stu-id="33402-133">To actually create or update the zone in Azure DNS, the zone object containing the zone parameters is passed to the *DnsManagementClient.Zones.CreateOrUpdateAsyc* method.</span></span>

> [!NOTE]
> <span data-ttu-id="33402-134">O DnsManagementClient oferece suporte a três modos de operação: síncrono ('CreateOrUpdate'), assíncrono ('CreateOrUpdateAsync') ou assíncrono com acesso à resposta HTTP ('CreateOrUpdateWithHttpMessagesAsync').</span><span class="sxs-lookup"><span data-stu-id="33402-134">DnsManagementClient supports three modes of operation: synchronous ('CreateOrUpdate'), asynchronous ('CreateOrUpdateAsync'), or asynchronous with access to the HTTP response ('CreateOrUpdateWithHttpMessagesAsync').</span></span>  <span data-ttu-id="33402-135">Você pode escolher qualquer um desses modos, dependendo das necessidades de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="33402-135">You can choose any of these modes, depending on your application needs.</span></span>

<span data-ttu-id="33402-136">O DNS do Azure dá suporte a [Etags](dns-getstarted-create-dnszone.md)de simultaneidade otimista.</span><span class="sxs-lookup"><span data-stu-id="33402-136">Azure DNS supports optimistic concurrency, called [Etags](dns-getstarted-create-dnszone.md).</span></span> <span data-ttu-id="33402-137">Neste exemplo, especificar "*" para o cabeçalho 'If-None-Match' informa ao DNS do Azure para criar uma zona DNS, caso ainda não exista.</span><span class="sxs-lookup"><span data-stu-id="33402-137">In this example, specifying "*" for the 'If-None-Match' header tells Azure DNS to create a DNS zone if one does not already exist.</span></span>  <span data-ttu-id="33402-138">A chamada falhará se uma zona com o nome fornecido já existir no grupo de recursos dado.</span><span class="sxs-lookup"><span data-stu-id="33402-138">The call fails if a zone with the given name already exists in the given resource group.</span></span>

```cs
// Create zone parameters
var dnsZoneParams = new Zone("global"); // All DNS zones must have location = "global"

// Create a Azure Resource Manager 'tag'.  This is optional.  You can add multiple tags
dnsZoneParams.Tags = new Dictionary<string, string>();
dnsZoneParams.Tags.Add("dept", "finance");

// Create the actual zone.
// Note: Uses 'If-None-Match *' ETAG check, so will fail if the zone exists already.
// Note: For non-async usage, call dnsClient.Zones.CreateOrUpdate(resourceGroupName, zoneName, dnsZoneParams, null, "*")
// Note: For getting the http response, call dnsClient.Zones.CreateOrUpdateWithHttpMessagesAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*")
var dnsZone = await dnsClient.Zones.CreateOrUpdateAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*");
```

## <a name="create-dns-record-sets-and-records"></a><span data-ttu-id="33402-139">Criar conjuntos de registros DNS e registros</span><span class="sxs-lookup"><span data-stu-id="33402-139">Create DNS record sets and records</span></span>

<span data-ttu-id="33402-140">Os registros DNS são gerenciados como um conjunto de registros.</span><span class="sxs-lookup"><span data-stu-id="33402-140">DNS records are managed as a record set.</span></span> <span data-ttu-id="33402-141">Um conjunto de registros é um conjunto de registros com o mesmo nome e tipo de registro dentro de uma zona.</span><span class="sxs-lookup"><span data-stu-id="33402-141">A record set is a set of records with the same name and record type within a zone.</span></span>  <span data-ttu-id="33402-142">O nome do conjunto de registros é relativo ao nome da zona, não ao nome DNS totalmente qualificado.</span><span class="sxs-lookup"><span data-stu-id="33402-142">The record set name is relative to the zone name, not the fully qualified DNS name.</span></span>

<span data-ttu-id="33402-143">Para criar ou atualizar um conjunto de registros, um objeto de parâmetros "RecordSet" é criado e passado para *DnsManagementClient.RecordSets.CreateOrUpdateAsync*.</span><span class="sxs-lookup"><span data-stu-id="33402-143">To create or update a record set, a "RecordSet" parameters object is created and passed to *DnsManagementClient.RecordSets.CreateOrUpdateAsync*.</span></span> <span data-ttu-id="33402-144">Como nas zonas DNS, há três modos de operação: síncrono ('CreateOrUpdate'), assíncrono ('CreateOrUpdateAsync') ou assíncrono com acesso à resposta HTTP ('CreateOrUpdateWithHttpMessagesAsync').</span><span class="sxs-lookup"><span data-stu-id="33402-144">As with DNS zones, there are three modes of operation: synchronous ('CreateOrUpdate'), asynchronous ('CreateOrUpdateAsync'), or asynchronous with access to the HTTP response ('CreateOrUpdateWithHttpMessagesAsync').</span></span>

<span data-ttu-id="33402-145">Como nas zonas DNS, as operações nos conjuntos de registros incluem suporte para a simultaneidade otimista.</span><span class="sxs-lookup"><span data-stu-id="33402-145">As with DNS zones, operations on record sets include support for optimistic concurrency.</span></span>  <span data-ttu-id="33402-146">Neste exemplo, como 'If-Match' nem 'If-None-Match' são especificados, o conjunto de registros sempre é criado.</span><span class="sxs-lookup"><span data-stu-id="33402-146">In this example, since neither 'If-Match' nor 'If-None-Match' are specified, the record set is always created.</span></span>  <span data-ttu-id="33402-147">Esta chamada substitui qualquer conjunto de registros existente com o mesmo nome e tipo de registro nessa zona DNS.</span><span class="sxs-lookup"><span data-stu-id="33402-147">This call overwrites any existing record set with the same name and record type in this DNS zone.</span></span>

```cs
// Create record set parameters
var recordSetParams = new RecordSet();
recordSetParams.TTL = 3600;

// Add records to the record set parameter object.  In this case, we'll add a record of type 'A'
recordSetParams.ARecords = new List<ARecord>();
recordSetParams.ARecords.Add(new ARecord("1.2.3.4"));

// Add metadata to the record set.  Similar to Azure Resource Manager tags, this is optional and you can add multiple metadata name/value pairs
recordSetParams.Metadata = new Dictionary<string, string>();
recordSetParams.Metadata.Add("user", "Mary");

// Create the actual record set in Azure DNS
// Note: no ETAG checks specified, will overwrite existing record set if one exists
var recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSetParams);
```

## <a name="get-zones-and-record-sets"></a><span data-ttu-id="33402-148">Obter zonas e conjuntos de registros</span><span class="sxs-lookup"><span data-stu-id="33402-148">Get zones and record sets</span></span>

<span data-ttu-id="33402-149">Os métodos *DnsManagementClient.Zones.Get* e *DnsManagementClient.RecordSets.Get* recuperem as zonas individuais e conjuntos de registros, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="33402-149">The *DnsManagementClient.Zones.Get* and *DnsManagementClient.RecordSets.Get* methods retrieve individual zones and record sets, respectively.</span></span> <span data-ttu-id="33402-150">RecordSets são identificados por seu tipo, nome e zona e grupo de recursos nos quais existem.</span><span class="sxs-lookup"><span data-stu-id="33402-150">RecordSets are identified by their type, name, and the zone and resource group they exist in.</span></span> <span data-ttu-id="33402-151">As zonas são identificadas por seu nome e o grupo de recursos em que existem.</span><span class="sxs-lookup"><span data-stu-id="33402-151">Zones are identified by their name and the resource group they exist in.</span></span>

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);
```

## <a name="update-an-existing-record-set"></a><span data-ttu-id="33402-152">Atualizar um conjunto de registros existente</span><span class="sxs-lookup"><span data-stu-id="33402-152">Update an existing record set</span></span>

<span data-ttu-id="33402-153">Para atualizar um conjunto de registros DNS existente, primeiro recupere o conjunto de registros e atualize o conteúdo do conjunto, em seguida, envie a alteração.</span><span class="sxs-lookup"><span data-stu-id="33402-153">To update an existing DNS record set, first retrieve the record set, then update the record set contents, then submit the change.</span></span>  <span data-ttu-id="33402-154">Neste exemplo, especificamos 'Etag' a partir do conjunto de registros recuperado no parâmetro 'If-Match'.</span><span class="sxs-lookup"><span data-stu-id="33402-154">In this example, we specify the 'Etag' from the retrieved record set in the 'If-Match' parameter.</span></span> <span data-ttu-id="33402-155">A chamada falhará se uma operação simultânea modificou o conjunto de registros nesse meio tempo.</span><span class="sxs-lookup"><span data-stu-id="33402-155">The call fails if a concurrent operation has modified the record set in the meantime.</span></span>

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);

// Add a new record to the local object.  Note that records in a record set must be unique/distinct
recordSet.ARecords.Add(new ARecord("5.6.7.8"));

// Update the record set in Azure DNS
// Note: ETAG check specified, update will be rejected if the record set has changed in the meantime
recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSet, recordSet.Etag);
```

## <a name="list-zones-and-record-sets"></a><span data-ttu-id="33402-156">Listar zonas e conjuntos de registros</span><span class="sxs-lookup"><span data-stu-id="33402-156">List zones and record sets</span></span>

<span data-ttu-id="33402-157">Para listar as zonas, use os métodos *DnsManagementClient.Zones.List...*, que oferecem suporte listando todas as zonas em um grupo de recursos dado ou todas as zonas em uma determinada assinatura do Azure (entre os grupos de recursos.) Para listar os conjuntos de registros, use os métodos *DnsManagementClient.RecordSets.List...*, que oferecem suporte listando todos os conjuntos de registros em uma determinada região ou apenas os conjuntos de registros de um tipo específico.</span><span class="sxs-lookup"><span data-stu-id="33402-157">To list zones, use the *DnsManagementClient.Zones.List...* methods, which support listing either all zones in a given resource group or all zones in a given Azure subscription (across resource groups.) To list record sets, use *DnsManagementClient.RecordSets.List...* methods, which support either listing all record sets in a given zone or only those record sets of a specific type.</span></span>

<span data-ttu-id="33402-158">Observe que ao listar as zonas e os conjuntos de registros, isso resulta em uma paginação.</span><span class="sxs-lookup"><span data-stu-id="33402-158">Note when listing zones and record sets that results may be paginated.</span></span>  <span data-ttu-id="33402-159">O exemplo a seguir mostra como percorrer as páginas de resultados.</span><span class="sxs-lookup"><span data-stu-id="33402-159">The following example shows how to iterate through the pages of results.</span></span> <span data-ttu-id="33402-160">(Um tamanho de página '2' artificialmente pequeno é usado para forçar a paginação; na prática, esse parâmetro deve ser omitido e o tamanho de página padrão usado.)</span><span class="sxs-lookup"><span data-stu-id="33402-160">(An artificially small page size of '2' is used to force paging; in practice this parameter should be omitted and the default page size used.)</span></span>

```cs
// Note: in this demo, we'll use a very small page size (2 record sets) to demonstrate paging
// In practice, to improve performance you would use a large page size or just use the system default
int recordSets = 0;
var page = await dnsClient.RecordSets.ListAllInResourceGroupAsync(resourceGroupName, zoneName, "2");
recordSets += page.Count();

while (page.NextPageLink != null)
{
    page = await dnsClient.RecordSets.ListAllInResourceGroupNextAsync(page.NextPageLink);
    recordSets += page.Count();
}
```

## <a name="next-steps"></a><span data-ttu-id="33402-161">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="33402-161">Next steps</span></span>

<span data-ttu-id="33402-162">Baixe o [projeto de exemplo SDK do .NET do DNS do Azure](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True), que inclui mais exemplos de como usar o SDK do .NET do DNS do Azure, incluindo exemplos para outros tipos de registro de DNS.</span><span class="sxs-lookup"><span data-stu-id="33402-162">Download the [Azure DNS .NET SDK sample project](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True), which includes further examples of how to use the Azure DNS .NET SDK, including examples for other DNS record types.</span></span>
