---
title: "Gerencie expiração de armazenamento Blob do Azure na Rede de Distribuição de Conteúdo do Microsoft Azure | Microsoft Docs"
description: "Aprenda sobre as opções para controlar a vida útil de blobs no cache do Azure CDN."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: ad4801e9-d09a-49bf-b35c-efdc4e6034e8
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 11/10/2017
ms.author: mazha
ms.openlocfilehash: 6f82ae396a17f903a522c716f73a5f7d2de660e7
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="manage-expiration-of-azure-blob-storage-in-azure-content-delivery-network"></a>Gerencie expiração de armazenamento Blob do Azure na Rede de Distribuição de Conteúdo do Microsoft Azure
> [!div class="op_single_selector"]
> * [Conteúdo da Web do Azure](cdn-manage-expiration-of-cloud-service-content.md)
> * [Armazenamento de Blobs do Azure](cdn-manage-expiration-of-blob-content.md)
> 
> 

O [Serviço de armazenamento de blobs](../storage/common/storage-introduction.md#blob-storage) no Armazenamento do Azure é uma das várias origens baseadas no Azure integradas à CDN (Rede de Distribuição de Conteúdo) do Azure. Qualquer conteúdo de blob publicamente acessível pode ser armazenado em cache no Azure CDN até que o tempo de vida (TTL) seja decorrido. A vida útil é determinada pelo cabeçalho `Cache-Control` na resposta HTTP do servidor de origem. Este artigo descreve várias maneiras que você pode definir o cabeçalho `Cache-Control` em um blob no Armazenamento do Azure.

Também é possível controlar as configurações de cache do portal do Azure, definindo as [regras de cache da CDN](cdn-caching-rules.md). Se você configurar uma ou mais regras de cache e definir o comportamento do cache para **Substituir** ou **Ignorar cache**, as configurações de cache fornecidas pela origem discutidas neste artigo serão ignoradas. Para obter informações sobre conceitos gerais de cache, consulte [Como funciona o cache](cdn-how-caching-works.md).

> [!TIP]
> Você pode optar por não definir nenhuma vida útil em um blob. Nesse caso, a CDN do Azure aplica automaticamente um TTL padrão de sete dias, exceto se você tiver configurado as regras de cache no portal do Azure. Esse padrão TTL aplica-se somente para otimizações de entrega da web gerais. Para otimizações de arquivo grande, o TTL padrão é de um dia e para otimizações de streaming de mídia, o TTL padrão é um ano.
> 
> Para obter mais informações sobre como a CDN do Azure trabalha para acelerar o acesso a blob e outros arquivos, consulte [Visão geral da Rede de Distribuição de Conteúdo do Azure](cdn-overview.md).
> 
> Para mais informações sobre o Armazenamento de Blobs do Azure, confira [Introdução ao armazenamento de Blobs](https://docs.microsoft.com/azure/storage/blobs/storage-blobs-introduction).
 

## <a name="setting-cache-control-headers-by-using-azure-powershell"></a>Configurando cabeçalhos de Cache-Control usando Azure PowerShell
[Azure PowerShell](/powershell/azure/overview) é uma das maneiras mais rápidas e eficientes de administrar os serviços do Azure. Use o cmdlet `Get-AzureStorageBlob` para obter uma referência para o blob, em seguida, defina a propriedade `.ICloudBlob.Properties.CacheControl`. 

Por exemplo:

```powershell
# Create a storage context
$context = New-AzureStorageContext -StorageAccountName "<storage account name>" -StorageAccountKey "<storage account key>"

# Get a reference to the blob
$blob = Get-AzureStorageBlob -Context $context -Container "<container name>" -Blob "<blob name>"

# Set the CacheControl property to expire in 1 hour (3600 seconds)
$blob.ICloudBlob.Properties.CacheControl = "max-age=3600"

# Send the update to the cloud
$blob.ICloudBlob.SetProperties()
```

> [!TIP]
> Você também pode usar o PowerShell para [gerenciar os perfis e os pontos de extremidade da CDN](cdn-manage-powershell.md).
> 
>

## <a name="setting-cache-control-headers-by-using-net"></a>Configurando cabeçalhos de Cache-Control usando .NET
Para definir o cabeçalho `Cache-Control` de um blob usando o código .NET, use a [Biblioteca do Cliente de Armazenamento do Azure para .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) a fim de definir a propriedade [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx).

Por exemplo:

```csharp
class Program
{
    const string connectionString = "<storage connection string>";
    static void Main()
    {
        // Retrieve storage account information from connection string
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);

        // Create a blob client for interacting with the blob service.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

        // Create a reference to the container
        CloudBlobContainer container = blobClient.GetContainerReference("<container name>");

        // Create a reference to the blob
        CloudBlob blob = container.GetBlobReference("<blob name>");

        // Set the CacheControl property to expire in 1 hour (3600 seconds)
        blob.Properties.CacheControl = "max-age=3600";

        // Update the blob's properties in the cloud
        blob.SetProperties();
    }
}
```

> [!TIP]
> Existem mais exemplos de código .NET disponíveis nos [Exemplos de Armazenamento de Blobs do Azure para .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).
> 

## <a name="setting-cache-control-headers-by-using-other-methods"></a>Configurando cabeçalhos de Cache-Control usando outros métodos

### <a name="azure-storage-explorer"></a>Gerenciador de Armazenamento do Azure
Com [Azure Storage Explorer](https://azure.microsoft.com/en-us/features/storage-explorer/), você pode exibir e editar seus recursos de armazenamento de blob, incluindo propriedades, como a propriedade *CacheControl*. 

Para atualizar a propriedade *CacheControl* de um blob com o Gerenciador de Armazenamento do Microsoft Azure:
   1. Selecione um blob e, em seguida, **Propriedades** no menu de contexto. 
   2. Role para baixo até a propriedade *CacheControl*.
   3. Insira um valor e, em seguida, clique em **Salvar**.


![Propriedades do Gerenciador do Armazenamento do Microsoft Azure](./media/cdn-manage-expiration-of-blob-content/cdn-storage-explorer-properties.png)

### <a name="azure-command-line-interface"></a>Interface de linha de comando do Azure
Com a [Interface de linha de comando (CLI) do Azure](https://docs.microsoft.com/cli/azure/overview?view=azure-cli-latest), você pode gerenciar recursos de blob do Azure a partir da linha de comando. Para definir um cabeçalho de cache-control ao carregar um blob com a CLI do Azure, defina a propriedade *cacheControl* usando a opção `-p`. O exemplo a seguir mostra como definir o TTL para uma hora (3600 segundos):
  
```azurecli
azure storage blob upload -c <connectionstring> -p cacheControl="max-age=3600" .\test.txt myContainer test.txt
```

### <a name="azure-storage-services-rest-api"></a>API REST de serviços de armazenamento do Azure
Você pode usar o [API REST de serviços de armazenamento do Azure](https://msdn.microsoft.com/library/azure/dd179355.aspx) para definir explicitamente a propriedade *x-ms-blob-cache-control* usando as seguintes operações em uma solicitação:
  
   - [Colocar Blob](https://msdn.microsoft.com/en-us/library/azure/dd179451.aspx)
   - [Colocar lista de blocos](https://msdn.microsoft.com/en-us/library/azure/dd179467.aspx)
   - [Definir propriedades de Blob](https://msdn.microsoft.com/library/azure/ee691966.aspx)

## <a name="testing-the-cache-control-header"></a>Testando o cabeçalho de Controle de Cache
Você pode facilmente verificar as configurações TTL dos seus blobs. Com as [ferramentas para desenvolvedores](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) do seu navegador, teste se o blob inclui `Cache-Control` no cabeçalho de resposta. Você também pode usar uma ferramenta como [Wget](https://www.gnu.org/software/wget/), [Postman](https://www.getpostman.com/) ou [Fiddler](http://www.telerik.com/fiddler) para examinar os cabeçalhos de resposta.

## <a name="next-steps"></a>Próximas etapas
* [Saiba como gerenciar a expiração do conteúdo do Serviço de Nuvem na CDN do Azure](cdn-manage-expiration-of-cloud-service-content.md)
* [Saiba mais sobre conceitos de cache](cdn-how-caching-works.md)

