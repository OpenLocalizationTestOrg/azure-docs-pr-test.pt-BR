---
title: aaaPublish WebApplicationVM | Microsoft Docs
description: "Saiba como toodeploy uma máquina virtual de tooa de aplicativo de web. Este script cria recursos Olá necessários em sua assinatura do Azure se não existirem."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: de4cec95-f73f-44d9-babd-9f47f2633cdb
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: e4b52b620bebf44b87ddfc3b19c155bb65111814
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-webapplicationvm-windows-powershell-script"></a>Publish-WebApplicationVM (script do Windows PowerShell)
Implanta uma máquina virtual de tooa de aplicativo de web. script Hello cria recursos Olá necessários em sua assinatura do Azure se não existirem.

```
Publish-WebApplicationVM
–Configuration <configuration>
-SubscriptionName <subscriptionName>
-WebDeployPackage <packageName>
-VMPassword @{Name = "name"; Password = "password")
-DatabaseServerPassword @{Name = "name"; Password = "password"}
-SendHostMessagesToOutput
-Verbose
```

### <a name="configuration"></a>Configuração
Olá caminho toohello arquivo de configuração JSON que descreve os detalhes de saudação da implantação de saudação.

| Aliases | nenhum |
| --- | --- |
| Obrigatório? |verdadeiro |
| Position |nomeado |
| Valor padrão |nenhum |
| Aceitar entrada do Pipeline? |false |
| Aceitar caracteres curinga? |false |

### <a name="subscriptionname"></a>SubscriptionName
nome de saudação do hello assinatura do Azure no qual você deseja toocreate Olá VM.

| Aliases | nenhum |
| --- | --- |
| Obrigatório? |false |
| Position |nomeado |
| Valor padrão |Usa assinatura primeiro Olá no arquivo de assinatura de saudação |
| Aceitar entrada do Pipeline? |false |
| Aceitar caracteres curinga? |false |

### <a name="webdeploypackage"></a>WebDeployPackage
Olá caminho toohello web implantação pacote toopublish toohello máquina virtual. Você pode criar esse pacote usando o Assistente de publicar Web Olá no Visual Studio. Consulte [Como: criar um pacote de implantação da Web no Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).

| Aliases | nenhum |
| --- | --- |
| Obrigatório? |false |
| Position |nomeado |
| Valor padrão |nenhum |
| Aceitar entrada do Pipeline? |false |
| Aceitar caracteres curinga? |false |

### <a name="allowuntrusted"></a>AllowUntrusted
Se verdadeiro, permita o uso de saudação de certificados que não são assinados por uma autoridade raiz confiável.

| Aliases | nenhum |
| --- | --- |
| Obrigatório? |false |
| Position |nomeado |
| Valor padrão |false |
| Aceitar entrada do Pipeline? |false |
| Aceitar caracteres curinga? |false |

### <a name="vmpassword"></a>VMPassword
credenciais de saudação para conta de máquina virtual de saudação. Exemplo: - VMPassword @{nome = "admin"; Senha = "password"}

| Aliases | nenhum |
| --- | --- |
| Obrigatório? |false |
| Position |nomeado |
| Valor padrão |nenhum |
| Aceitar entrada do Pipeline? |false |
| Aceitar caracteres curinga? |false |

### <a name="databaseserverpassword"></a>DatabaseServerPassword
credenciais Olá Olá banco de dados SQL no Azure. Exemplo: - DatabaseServerPassword @{nome = "admin"; Senha = "password"}

| Aliases | nenhum |
| --- | --- |
| Obrigatório? |false |
| Position |nomeado |
| Valor padrão |nenhum |
| Aceitar entrada do Pipeline? |false |
| Aceitar caracteres curinga? |false |

### <a name="sendhostmessagestooutput"></a>SendHostMessagesToOutput
Se true, impressão mensagens de saudação script toohello fluxo de saída.

| Aliases | nenhum |
| --- | --- |
| Obrigatório? |false |
| Position |nomeado |
| Valor padrão |false |
| Aceitar entrada do Pipeline? |false |
| Aceitar caracteres curinga? |false |

## <a name="remarks"></a>Comentários
Para obter uma explicação completa de como toouse Olá script toocreate desenvolvimento e ambientes de teste, consulte [ambientes de teste e usando Scripts do Windows PowerShell tooPublish tooDev](vs-azure-tools-publishing-using-powershell-scripts.md).

arquivo de configuração JSON Olá Especifica detalhes de saudação do que é toobe implantado. Ela inclui informações de saudação que você especificou quando criou o projeto hello, como nome hello, grupo de afinidade, imagem do VHD e tamanho da máquina virtual de saudação. Ele também inclui pontos de extremidade de saudação na máquina virtual de hello, Olá tooprovision de bancos de dados, se houver e parâmetros de implantação de web. saudação de código a seguir mostra um exemplo de arquivo de configuração de JSON:

```
{
    "environmentSettings": {
        "cloudService": {
            "name": "myvmname",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myvmname",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201404.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [
                    {
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [
            {
                "connectionStringName": "",
                "databaseName": "",
                "serverName": "",
                "user": "",
                "password": ""
            }
        ],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

Você pode editar o arquivo de configuração do hello JSON toochange o que é provisionado. Uma máquina virtual e um serviço de nuvem são necessários, mas Olá seção de banco de dados é opcional.

