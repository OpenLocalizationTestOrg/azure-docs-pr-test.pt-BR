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
# <a name="create-dns-zones-and-record-sets-using-hello-net-sdk"></a>Criar zonas DNS e conjuntos de registros usando o SDK .NET de saudação

Você pode automatizar operações toocreate, excluir ou atualizar zonas de DNS, os conjuntos de registro e registros usando o SDK do DNS com biblioteca de gerenciamento de DNS do .NET. Um projeto completo do Visual Studio está disponível [aqui.](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True)

## <a name="create-a-service-principal-account"></a>Crie uma conta da entidade de serviço

Normalmente, os recursos do acesso programático tooAzure é concedida por meio de uma conta dedicada em vez de suas próprias credenciais de usuário. Essas contas dedicadas são denominadas contas da 'entidade de serviço'. projeto de exemplo hello toouse DNS do SDK do Azure, você primeiro precisa de uma conta de serviço principal de toocreate e atribui permissões corretas hello.

1. Execute [estas instruções](../azure-resource-manager/resource-group-authenticate-service-principal.md) toocreate uma conta de serviço principal (projeto de exemplo do SDK do Azure DNS Olá pressupõe a autenticação baseada em senha).
2. Crie um grupo de recursos ([aqui](../azure-resource-manager/resource-group-template-deploy-portal.md)).
3. Use o RBAC do Azure toogrant Olá serviço conta principal 'Colaborador de zona DNS' permissões toohello grupo de recursos ([aqui está como](../active-directory/role-based-access-control-configure.md).)
4. Se usando o projeto de exemplo do SDK do Azure DNS hello, edite o arquivo de 'program.cs' de saudação da seguinte maneira:

   * Inserir valores corretos Olá Olá tenantId, clientId (também conhecido como a ID de conta), segredo (senha de conta de entidade de serviço) e subscriptionId conforme usado na etapa 1.
   * Insira o nome do grupo de recursos Olá escolhido na etapa 2.
   * Insira um nome de zona do DNS de sua escolha.

## <a name="nuget-packages-and-namespace-declarations"></a>Pacotes NuGet e declarações de namespace

toouse Olá DNS do Azure .NET SDK, você precisa Olá tooinstall **biblioteca de gerenciamento do DNS do Azure** pacote NuGet e outros necessários pacotes do Azure.

1. No **Visual Studio**, abra um projeto ou um novo projeto.
2. Vá muito**ferramentas**  **>**  **NuGet Package Manager**  **>**  **gerenciar pacotes NuGet para Solução...** .
3. Clique em **procurar**, habilitar Olá **incluir pré-lançamento** caixa de seleção e digite **Microsoft.Azure.Management.Dns** na caixa de pesquisa de saudação.
4. Selecione o pacote de saudação e clique em **instalar** tooadd-tooyour o projeto do Visual Studio.
5. Repetir o processo de saudação acima tooalso instalação Olá pacotes a seguir: **Microsoft.Rest.ClientRuntime.Azure.Authentication** e **Microsoft.Azure.Management.ResourceManager**.

## <a name="add-namespace-declarations"></a>Adicionar declarações do namespace

Adicionar Olá seguir declarações de namespace

```cs
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.Dns;
using Microsoft.Azure.Management.Dns.Models;
```

## <a name="initialize-hello-dns-management-client"></a>Inicializar o cliente de gerenciamento de DNS Olá

Olá *DnsManagementClient* contém métodos de saudação e as propriedades necessárias para o gerenciamento de zonas DNS e conjuntos de registros.  Olá código a seguir registra na conta de serviço principal toohello e cria um objeto DnsManagementClient.

```cs
// Build hello service credentials and DNS management client
var serviceCreds = await ApplicationTokenProvider.LoginSilentAsync(tenantId, clientId, secret);
var dnsClient = new DnsManagementClient(serviceCreds);
dnsClient.SubscriptionId = subscriptionId;
```

## <a name="create-or-update-a-dns-zone"></a>Criar ou atualizar uma zona DNS

toocreate uma zona DNS, primeiro um objeto "Zone" é criado parâmetros de zona do DNS do toocontain hello. Como as zonas DNS não são região específica tooa vinculado, o local de saudação é definido too'global'. Neste exemplo, um [do Azure Resource Manager 'tag'](https://azure.microsoft.com/updates/organize-your-azure-resources-with-tags/) também é adicionado toohello zona.

tooactually criar ou atualizar Olá zona no DNS do Azure, que contém parâmetros de zona de saudação de objeto de zona Olá é passada toohello *DnsManagementClient.Zones.CreateOrUpdateAsyc* método.

> [!NOTE]
> DnsManagementClient oferece suporte a três modos de operação: síncrono ('CreateOrUpdate'), assíncrona ('CreateOrUpdateAsync'), ou assíncrono com a resposta HTTP de toohello de acesso ('CreateOrUpdateWithHttpMessagesAsync').  Você pode escolher qualquer um desses modos, dependendo das necessidades de seu aplicativo.

O DNS do Azure dá suporte a [Etags](dns-getstarted-create-dnszone.md)de simultaneidade otimista. Neste exemplo, especificando "*" para o cabeçalho de saudação 'If-None-Match' informa toocreate DNS do Azure uma zona DNS se ainda não existir.  chamada de saudação falhará se uma zona com o nome do hello fornecido já existe no hello fornecido o grupo de recursos.

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

## <a name="create-dns-record-sets-and-records"></a>Criar conjuntos de registros DNS e registros

Os registros DNS são gerenciados como um conjunto de registros. Um conjunto de registros é um conjunto de registros com hello mesmo nome e registre tipo dentro de uma zona.  nome do conjunto de registros de saudação é nome da zona toohello relativo, Olá não o nome DNS totalmente qualificado.

toocreate ou atualizar um conjunto de registros, um objeto de parâmetros "RecordSet" é criado e transmitido muito*DnsManagementClient.RecordSets.CreateOrUpdateAsync*. Como com as zonas DNS, há três modos de operação: síncrono ('CreateOrUpdate'), assíncrona ('CreateOrUpdateAsync'), ou assíncrono com a resposta HTTP de toohello de acesso ('CreateOrUpdateWithHttpMessagesAsync').

Como nas zonas DNS, as operações nos conjuntos de registros incluem suporte para a simultaneidade otimista.  Neste exemplo, pois nem 'If-Match' nem 'If-None-Match' for especificado, o conjunto de registros Olá sempre é criado.  Essa chamada substitui qualquer registro existente com hello mesmo nome e registre o tipo desta zona DNS.

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

## <a name="get-zones-and-record-sets"></a>Obter zonas e conjuntos de registros

Olá *DnsManagementClient.Zones.Get* e *DnsManagementClient.RecordSets.Get* métodos recuperem regiões individuais e conjuntos de registros, respectivamente. Conjuntos de registros são identificados por seu tipo, o nome e a saudação zona e grupo de recursos existam no. As zonas são identificadas por seu grupo de recursos de nome e hello existirem no.

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);
```

## <a name="update-an-existing-record-set"></a>Atualizar um conjunto de registros existente

tooupdate um registro DNS existente definido, recuperar primeiro conjunto de registros Olá, e em seguida, atualizar Olá registro o conteúdo do conjunto, em seguida, enviar alterações hello.  Neste exemplo, podemos especificar Olá que ETag da saudação recuperados registro definido no parâmetro de 'If-Match' hello. chamada de saudação falhará se uma operação simultânea modificou Olá conjunto de registros em Olá enquanto isso.

```cs
var recordSet = dnsClient.RecordSets.Get(resourceGroupName, zoneName, recordSetName, RecordType.A);

// Add a new record toohello local object.  Note that records in a record set must be unique/distinct
recordSet.ARecords.Add(new ARecord("5.6.7.8"));

// Update hello record set in Azure DNS
// Note: ETAG check specified, update will be rejected if hello record set has changed in hello meantime
recordSet = await dnsClient.RecordSets.CreateOrUpdateAsync(resourceGroupName, zoneName, recordSetName, RecordType.A, recordSet, recordSet.Etag);
```

## <a name="list-zones-and-record-sets"></a>Listar zonas e conjuntos de registros

zonas de toolist, use Olá *DnsManagementClient.Zones.List...*  métodos, que oferece suporte a listagem a todas as zonas em um grupo de recursos determinado ou todas as zonas em conjuntos de registros de toolist uma determinada assinatura do Azure (em arquivos de recursos grupos.), usem *DnsManagementClient.RecordSets.List...*  métodos, que oferece suporte a listando todos os conjuntos de registros em uma determinada região ou apenas os conjuntos de registros de um tipo específico.

Observe que ao listar as zonas e os conjuntos de registros, isso resulta em uma paginação.  Olá mostrado no exemplo a seguir como tooiterate por meio de páginas de saudação de resultados. (Um tamanho de página artificialmente pequeno '2' é usado tooforce paginação; na prática, esse parâmetro deve ser omitido e Olá tamanho de página padrão usado).

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

## <a name="next-steps"></a>Próximas etapas

Baixar Olá [projeto de exemplo do SDK do Azure DNS .NET](https://www.microsoft.com/en-us/download/details.aspx?id=47268&WT.mc_id=DX_MVP4025064&e6b34bbe-475b-1abd-2c51-b5034bcdd6d2=True), que inclui mais exemplos de como toouse Olá SDK .NET DNS do Azure, incluindo exemplos para outros tipos de registros de DNS.
