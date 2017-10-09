---
title: aaaCreate registros de DNS personalizados para um aplicativo web | Microsoft Docs
description: "Como o DNS de domínio personalizado toocreate registros para o aplicativo web usando o DNS do Azure."
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: 6c16608c-4819-44e7-ab88-306cf4d6efe5
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 070c808a55bab922eb624d99ae5c275d8eaa5aaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-dns-records-for-a-web-app-in-a-custom-domain"></a>Criar registros DNS para um aplicativo Web em um domínio personalizado

Você pode usar o DNS do Azure toohost um domínio personalizado para seus aplicativos web. Por exemplo, você está criando um aplicativo web do Azure e deseja que seus usuários tooaccess-lo pelo usando contoso.com ou www.contoso.com como um FQDN.

toodo isso, você tem dois registros de toocreate:

* Um toocontoso.com de apontador registro raiz "A"
* Um "" registro CNAME para o nome de www Olá que aponta toohello um registro

Tenha em mente que, se você criar um registro para um aplicativo web no Azure, Olá que um registro deve ser atualizado manualmente se Olá subjacente endereço IP para alterações de aplicativo web hello.

## <a name="before-you-begin"></a>Antes de começar

Antes de começar, deve primeiro criar uma zona DNS no DNS do Azure e delegar a zona Olá no seu registrador tooAzure DNS.

1. toocreate uma zona DNS, execute as etapas de saudação em [criar uma zona DNS](dns-getstarted-create-dnszone.md).
2. toodelegate tooAzure seu DNS DNS, execute as etapas de saudação em [delegação de domínio DNS](dns-domain-delegation.md).

Depois de criar uma zona e delegação de DNS de tooAzure, em seguida, você pode criar registros para seu domínio personalizado.

## <a name="1-create-an-a-record-for-your-custom-domain"></a>1. Criar um registro A para seu domínio personalizado

Um registro é toomap usado um endereço IP do nome tooits. Saudação de exemplo a seguir é atribuirá como um tooan de registro de um endereço IPv4:

### <a name="step-1"></a>Etapa 1

Crie um registro e atribua tooa $rs variável

```powershell
$rs= New-AzureRMDnsRecordSet -Name "@" -RecordType "A" -ZoneName "contoso.com" -ResourceGroupName "MyAzureResourceGroup" -Ttl 600
```

### <a name="step-2"></a>Etapa 2

Adicionar conjunto de registros Olá IPv4 valor toohello criado anteriormente "@" usando a variável Olá $rs atribuído. Olá valor IPv4 atribuído será o endereço IP de saudação para seu aplicativo web.

endereço IP de saudação toofind para um aplicativo web, siga as etapas de saudação em [configurar um nome de domínio personalizado no serviço de aplicativo do Azure](../app-service-web/app-service-web-tutorial-custom-domain.md).

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Ipv4Address "<your web app IP address>"
```

### <a name="step-3"></a>Etapa 3

Confirme o conjunto de registros Olá alterações toohello. Use `Set-AzureRMDnsRecordSet` Olá tooupload altera toohello tooAzure de conjunto de registros DNS:

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="2-create-a-cname-record-for-your-custom-domain"></a>2. Criar um registro CNAME para seu domínio personalizado

Se o domínio já é gerenciado pelo DNS do Azure (consulte [delegação de domínio DNS](dns-domain-delegation.md), você pode usar Olá Olá exemplo toocreate um registro CNAME para contoso.azurewebsites.net a seguir.

### <a name="step-1"></a>Etapa 1

Abra o PowerShell e crie um novo conjunto de registros CNAME e atribua tooa $rs variável. Este exemplo criará um tipo de conjunto de registros CNAME com um "tempo toolive" de 600 segundos na zona DNS denominado "contoso.com".

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName contoso.com -ResourceGroupName myresourcegroup -Name "www" -RecordType "CNAME" -Ttl 600
```

saudação de exemplo a seguir é a resposta de saudação.

```
Name              : www
ZoneName          : contoso.com
ResourceGroupName : myresourcegroup
Ttl               : 600
Etag              : 8baceeb9-4c2c-4608-a22c-229923ee1856
RecordType        : CNAME
Records           : {}
Tags              : {}
```

### <a name="step-2"></a>Etapa 2

Após Olá conjunto de registros CNAME é criado, você precisará toocreate um valor de alias que vai apontar toohello web app.

Usando Olá atribuídos previamente a variável "$rs" você pode usar o comando do PowerShell Olá abaixo alias de saudação toocreate para Olá web aplicativo contoso.azurewebsites.net.

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "contoso.azurewebsites.net"
```

saudação de exemplo a seguir é a resposta de saudação.

```
    Name              : www
    ZoneName          : contoso.com
    ResourceGroupName : myresourcegroup
    Ttl               : 600
    Etag              : 8baceeb9-4c2c-4608-a22c-229923ee185
    RecordType        : CNAME
    Records           : {contoso.azurewebsites.net}
    Tags              : {}
```

### <a name="step-3"></a>Etapa 3

Confirmar alterações de saudação usando Olá `Set-AzureRMDnsRecordSet` cmdlet:

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

Você pode validar o registro de saudação foi criado corretamente consultando hello "www.contoso.com" usando nslookup, conforme mostrado abaixo:

```
PS C:\> nslookup
Default Server:  Default
Address:  192.168.0.1

> www.contoso.com
Server:  default server
Address:  192.168.0.1

Non-authoritative answer:
Name:    <instance of web app service>.cloudapp.net
Address:  <ip of web app service>
Aliases:  www.contoso.com
contoso.azurewebsites.net
<instance of web app service>.vip.azurewebsites.windows.net
```

## <a name="create-an-awverify-record-for-web-apps"></a>Criar um registro "awverify" para aplicativos Web

Se você decidir toouse um registro a para seu aplicativo web, você deve percorrer um tooensure do processo de verificação é domínio personalizado próprio hello. Essa etapa de verificação é feita criando um registro CNAME especial chamado "awverify". Esta seção aplica-se somente os registros de tooA.

### <a name="step-1"></a>Etapa 1

Crie registro de "awverify" hello. No exemplo hello abaixo, vamos criar registro de "aweverify" Olá para contoso.com tooverify propriedade para o domínio personalizado hello.

```powershell
$rs = New-AzureRMDnsRecordSet -ZoneName "contoso.com" -ResourceGroupName "myresourcegroup" -Name "awverify" -RecordType "CNAME" -Ttl 600
```

saudação de exemplo a seguir é a resposta de saudação.

```
Name              : awverify
ZoneName          : contoso.com
ResourceGroupName : myresourcegroup
Ttl               : 600
Etag              : 8baceeb9-4c2c-4608-a22c-229923ee1856
RecordType        : CNAME
Records           : {}
Tags              : {}
```

### <a name="step-2"></a>Etapa 2

Depois de criar o conjunto de registros "awverify" Olá, atribua o registro CNAME Olá alias definido. O exemplo hello abaixo, podemos atribuirá Olá tooawverify.contoso.azurewebsites.net de alias de conjunto de registros de CNAMe.

```powershell
Add-AzureRMDnsRecordConfig -RecordSet $rs -Cname "awverify.contoso.azurewebsites.net"
```

saudação de exemplo a seguir é a resposta de saudação.

```
    Name              : awverify
    ZoneName          : contoso.com
    ResourceGroupName : myresourcegroup
    Ttl               : 600
    Etag              : 8baceeb9-4c2c-4608-a22c-229923ee185
    RecordType        : CNAME
    Records           : {awverify.contoso.azurewebsites.net}
    Tags              : {}
```

### <a name="step-3"></a>Etapa 3

Confirmar alterações de saudação usando Olá `Set-AzureRMDnsRecordSet cmdlet`, conforme mostrado no comando de saudação abaixo.

```powershell
Set-AzureRMDnsRecordSet -RecordSet $rs
```

## <a name="next-steps"></a>Próximas etapas

Siga as etapas de saudação em [Configurando um nome de domínio personalizado para o serviço de aplicativo](../app-service-web/web-sites-custom-domain-name.md) tooconfigure seu aplicativo de web toouse um domínio personalizado.
