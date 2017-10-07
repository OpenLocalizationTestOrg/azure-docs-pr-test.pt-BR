---
title: "aaaConfigure uma cadeia de caracteres de conexão para o armazenamento do Azure | Microsoft Docs"
description: "Configure uma cadeia de conexão para uma conta de Armazenamento do Azure. Uma cadeia de caracteres de conexão contém informações de saudação tooauthenticate de acesso necessário tooa conta de armazenamento de seu aplicativo em tempo de execução."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: ecb0acb5-90a9-4eb2-93e6-e9860eda5e53
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: marsma
ms.openlocfilehash: 80c38a6f8f0d4f06b99e7c487647b984e01d1772
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-storage-connection-strings"></a>Configurar cadeias de conexão do Armazenamento do Azure

Uma cadeia de caracteres de conexão inclui informações de autenticação de saudação necessárias para os dados do aplicativo tooaccess em uma conta de armazenamento do Azure em tempo de execução. Você pode configurar cadeias de conexão para:

* Conecte-se toohello emulador de armazenamento do Azure.
* Acesse uma conta de armazenamento no Azure.
* Acessar recursos especificados no Azure por uma SAS (Assinatura de Acesso Compartilhado).

[!INCLUDE [storage-account-key-note-include](../../includes/storage-account-key-note-include.md)]

## <a name="storing-your-connection-string"></a>Armazenar a sua cadeia de conexão
Seu aplicativo precisa de cadeia de caracteres de conexão Olá de tooaccess em tempo de execução tooauthenticate solicitações feitas tooAzure armazenamento. Você tem várias opções diferentes para armazenar a cadeia de conexão:

* Um aplicativo em execução na área de trabalho hello, ou em um dispositivo pode armazenar a cadeia de caracteres de conexão de saudação em uma **App. config** ou **Web. config** arquivo. Adicionar toohello de cadeia de caracteres de conexão Olá **AppSettings** seção nesses arquivos.
* Um aplicativo em execução em um serviço de nuvem do Azure pode armazenar a cadeia de caracteres de conexão de saudação em Olá [arquivo de esquema (. cscfg) de configuração de serviço do Azure](https://msdn.microsoft.com/library/ee758710.aspx). Adicionar toohello de cadeia de caracteres de conexão Olá **ConfigurationSettings** seção do arquivo de configuração do serviço de saudação.
* Você pode usar a cadeia de conexão diretamente no seu código. Na maioria dos cenários, no entanto, recomendamos armazenar sua cadeia de conexão em um arquivo de configuração.

Armazenar a cadeia de conexão em um arquivo de configuração torna tooswitch de cadeia de caracteres de conexão tooupdate fácil Olá entre o emulador de armazenamento hello e uma conta de armazenamento do Azure na nuvem hello. Você só precisa ambiente de destino tooedit Olá conexão cadeia de caracteres toopoint tooyour.

Você pode usar o hello [Gerenciador de configuração do Microsoft Azure](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) tooaccess sua conexão de cadeia de caracteres em tempo de execução, independentemente de onde o aplicativo está sendo executado.

## <a name="create-a-connection-string-for-hello-storage-emulator"></a>Criar uma cadeia de caracteres de conexão para o emulador de armazenamento Olá
[!INCLUDE [storage-emulator-connection-string-include](../../includes/storage-emulator-connection-string-include.md)]

Para obter mais informações sobre o emulador de armazenamento hello, consulte [usar o emulador de armazenamento do Azure Olá para desenvolvimento e teste](storage-use-emulator.md).

## <a name="create-a-connection-string-for-an-azure-storage-account"></a>Criar uma cadeia de conexão para uma conta de Armazenamento do Azure
toocreate uma cadeia de caracteres de conexão para sua conta de armazenamento do Azure, formato a seguir de saudação do uso. Indique se deseja tooconnect toohello conta de armazenamento por meio de HTTPS (recomendado) ou HTTP, substitua `myAccountName` com o nome da saudação de sua conta de armazenamento e substitua `myAccountKey` com sua chave de acesso da conta:

`DefaultEndpointsProtocol=[http|https];AccountName=myAccountName;AccountKey=myAccountKey`

Por exemplo, a cadeia de conexão pode parecer com o seguinte:

`DefaultEndpointsProtocol=https;AccountName=storagesample;AccountKey=<account-key>`

Embora o Armazenamento do Azure dê suporte a HTTP e HTTPS em uma cadeia de conexão, *usar HTTPS é altamente recomendável*.

> [!TIP]
> Você pode encontrar as cadeias de caracteres de conexão da sua conta de armazenamento no hello [portal do Azure](https://portal.azure.com). Navegue muito**configurações** > **chaves de acesso** em cadeias de conexão de toosee da sua conta de armazenamento menu folha para ambas as chaves de acesso primária e secundária.
>

## <a name="create-a-connection-string-using-a-shared-access-signature"></a>Criar uma cadeia de conexão usando uma assinatura de acesso compartilhado
[!INCLUDE [storage-use-sas-in-connection-string-include](../../includes/storage-use-sas-in-connection-string-include.md)]

## <a name="create-a-connection-string-for-an-explicit-storage-endpoint"></a>Criar uma cadeia de conexão para um ponto de extremidade explícito do armazenamento
Você pode especificar pontos de extremidade de serviço explícito em sua cadeia de conexão em vez de usar pontos de extremidade saudação padrão. toocreate uma cadeia de caracteres de conexão que especifica um ponto de extremidade explícito, especificar ponto de extremidade de serviço completo Olá para cada serviço, incluindo a especificação do protocolo de saudação (HTTP ou HTTPS (recomendado)), Olá formato a seguir:

```
DefaultEndpointsProtocol=[http|https];
BlobEndpoint=myBlobEndpoint;
FileEndpoint=myFileEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
AccountName=myAccountName;
AccountKey=myAccountKey
```

Um cenário em que talvez você queira toospecify um ponto de extremidade explícito é quando você mapeou o tooa de ponto de extremidade de armazenamento de Blob [domínio personalizado](storage-custom-domain-name.md). Nesse caso, você pode especificar o ponto de extremidade personalizado para o armazenamento de Blobs em sua cadeia de conexão. Você pode especificar opcionalmente saudação padrão pontos de extremidade Olá outros serviços se seu aplicativo usa.

Aqui está um exemplo de uma cadeia de caracteres de conexão que especifica um ponto de extremidade explícito para Olá serviço Blob:

```
# Blob endpoint only
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
AccountName=storagesample;
AccountKey=<account-key>
```

Este exemplo especifica os pontos de extremidade explícitos para todos os serviços, incluindo um domínio personalizado para Olá serviço Blob:

```
# All service endpoints
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
FileEndpoint=https://myaccount.file.core.windows.net;
QueueEndpoint=https://myaccount.queue.core.windows.net;
TableEndpoint=https://myaccount.table.core.windows.net;
AccountName=storagesample;
AccountKey=<account-key>
```

valores de ponto de extremidade de saudação em uma cadeia de conexão são usadas tooconstruct solicitação de saudação serviços de armazenamento toohello URIs e ditam formulário Olá URIs são retornados tooyour código.

Se você tiver mapeado um domínio personalizado do ponto de extremidade tooa de armazenamento e omite esse ponto de extremidade de uma cadeia de conexão, em seguida, você não será capaz de toouse essa conexão tooaccess de dados string nesse serviço no seu código.

> [!IMPORTANT]
> Valores de ponto de extremidade de serviço em suas cadeias de conexão devem ser URIs bem formados, incluindo `https://` (recomendado) ou `http://`. Porque o armazenamento do Azure ainda não suporta o HTTPS para domínios personalizados, você *deve* especificar `http://` para qualquer ponto de extremidade URI que aponta o domínio personalizado tooa.
>

### <a name="create-a-connection-string-with-an-endpoint-suffix"></a>Criar uma cadeia de conexão com um sufixo de ponto de extremidade
toocreate uma conexão de cadeia de caracteres para um serviço de armazenamento em regiões ou instâncias com sufixos de ponto de extremidade diferente, como do Azure na China ou Azure Government, Olá use formato de cadeia de caracteres de conexão a seguir. Indique se deseja tooconnect toohello conta de armazenamento por meio de HTTPS (recomendado) ou HTTP, substitua `myAccountName` com nome de saudação da sua conta de armazenamento, substitua `myAccountKey` com sua chave de acesso da conta e substituir `mySuffix` com hello URI sufixo:

```
DefaultEndpointsProtocol=[http|https];
AccountName=myAccountName;
AccountKey=myAccountKey;
EndpointSuffix=mySuffix;
```

Aqui está um exemplo de cadeia de conexão para serviços de armazenamento no Azure China:

```
DefaultEndpointsProtocol=https;
AccountName=storagesample;
AccountKey=<account-key>;
EndpointSuffix=core.chinacloudapi.cn;
```

## <a name="parsing-a-connection-string"></a>Analisando uma cadeia de conexão
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="next-steps"></a>Próximas etapas
* [Usar o emulador de armazenamento do Azure Olá para desenvolvimento e teste](storage-use-emulator.md)
* [Gerenciadores do Armazenamento do Azure](storage-explorers.md)
* [Uso de SAS (Assinaturas de Acesso Compartilhado)](storage-dotnet-shared-access-signature-part-1.md)

