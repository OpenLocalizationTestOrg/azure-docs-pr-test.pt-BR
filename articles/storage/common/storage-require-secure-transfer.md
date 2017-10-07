---
title: "transferência segura de aaaRequire no armazenamento do Azure | Microsoft Docs"
description: "Saiba mais sobre o recurso de \"Exigir a transferência segura\" Olá para armazenamento do Azure e como tooenable-lo."
services: storage
documentationcenter: na
author: fhryo-msft
manager: Jason.Hogg
editor: fhryo-msft
ms.assetid: 
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 06/20/2017
ms.author: fryu
ms.openlocfilehash: 27f745c5e771b50213c1dbb39dee081947be1f39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="require-secure-transfer"></a>Requer transferência segura

opção Hello "transferência segura necessária" aumenta a segurança de saudação da sua conta de armazenamento, permitindo que apenas solicitações toohello conta de armazenamento de conexões seguras. Por exemplo, ao chamar APIs REST tooaccess sua conta de armazenamento, você deve se conectar usando HTTPS. Todas as solicitações utilizando HTTP serão rejeitadas quando a "Transferência segura obrigatória" estiver habilitada.

Quando você estiver usando o serviço de arquivos do Azure Olá, qualquer conexão sem criptografia falhará ao "Seguro transferência necessária" está habilitado. Isso inclui cenários de uso de SMB 2.1, SMB 3.0 sem criptografia e alguns tipos de saudação cliente Linux SMB. 

Por padrão, a opção de hello "transferência segura necessária" está desabilitada.

> [!NOTE]
> Como o armazenamento do Azure não dá suporte a HTTPS para nomes de domínio personalizado, essa opção não será aplicada ao usar um nome de domínio personalizado.

## <a name="enable-secure-transfer-required-in-hello-azure-portal"></a>Habilitar o "Transferência segura necessária" hello portal do Azure

Você pode habilitar hello "transferência segura necessária" configurar ambos ao criar uma conta de armazenamento no hello [portal do Azure](https://portal.azure.com)e para contas de armazenamento existente.

### <a name="require-secure-transfer-when-you-create-a-storage-account"></a>Requerer transferência segura ao criar uma conta de armazenamento

1. Olá abrir **criar conta de armazenamento** folha em Olá portal do Azure.
1. Em **Transferência segura obrigatória**, selecione **habilitado**.

  ![captura de tela](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_1.png)

### <a name="require-secure-transfer-for-an-existing-storage-account"></a>Requer transferência segura de uma conta de armazenamento existente

1. Selecione uma conta de armazenamento existente na Olá portal do Azure.
1. Selecione **configuração** em **configurações** na folha de menu de conta de armazenamento hello.
1. Em **Transferência segura obrigatória**, selecione **habilitado**.

  ![captura de tela](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_2.png)

## <a name="enable-secure-transfer-required-programmatically"></a>Habilitar "Transferência segura obrigatória" Programaticamente

nome da configuração Olá é _supportsHttpsTrafficOnly_ nas propriedades da conta de armazenamento. Você pode habilitar a configuração "Transferência segura obrigatória" com a API REST, ferramentas ou bibliotecas:

* **API REST** (Versão: 2016-12-01): [pacote de lançamento](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)
* **PowerShell** (Versão: 4.1.0): [pacote de lançamento](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)
* **CLI** (Versão: 2.0.11): [pacote de lançamento](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)
* **NodeJS** (Versão: 1.1.0): [pacote de lançamento](https://www.npmjs.com/package/azure-arm-storage/)
* **SDK do .NET SDK** (Versão: 6.3.0): [pacote de lançamento](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)
* **SDK do Python** (Versão: 1.1.0): [pacote de lançamento](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)
* **SDK do Ruby** (Versão: 0.11.0): [pacote de lançamento](https://rubygems.org/gems/azure_mgmt_storage)

### <a name="enable-secure-transfer-required-setting-with-rest-api"></a>Habilitar a configuração "Transferência segura obrigatória" com a API REST

toosimplify testes com API REST, você pode usar [ArmClient](https://github.com/projectkudu/ARMClient) toocall de linha de comando.

 Você pode usar abaixo da configuração de saudação de toocheck de linha de comando com hello API REST:

```
# Login Azure and proceed with your credentials
> armclient login

> armclient GET  /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01
```

Em resposta hello, você pode encontrar _supportsHttpsTrafficOnly_ configuração. Exemplo:

```Json
{
  "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}",
  "kind": "Storage",
  ...
  "properties": {
    ...
    "supportsHttpsTrafficOnly": false
  },
  "type": "Microsoft.Storage/storageAccounts"
}
```

Você pode usar abaixo da configuração de saudação de tooenable de linha de comando com hello API REST:

```
# Login Azure and proceed with your credentials
> armclient login

> armclient PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01 < Input.json
```
Exemplo de Input.json:
```Json
{
  "location": "westus",
  "properties": {
    "supportsHttpsTrafficOnly": true
  }
}
```

## <a name="next-steps"></a>Próximas etapas
Armazenamento do Azure fornece um conjunto abrangente de recursos de segurança, que juntos permitem que os desenvolvedores de aplicativos seguros toobuild. Para obter mais detalhes, visite Olá [guia de segurança do armazenamento](storage-security-guide.md).
