---
title: "aaaStore e exibir dados de diagnóstico no armazenamento do Azure | Microsoft Docs"
description: "Obter dados de diagnóstico do Azure no Armazenamento do Azure e exibi-los"
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: tysonn
ms.assetid: 18e0780d-43e7-41e4-b8e9-f1fb9a36eb03
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: robb
ms.openlocfilehash: dd47a2ef6d6488c80c102c72b2ebf6ca6d2e473f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="store-and-view-diagnostic-data-in-azure-storage"></a>Armazenar e exibir dados de diagnóstico no Armazenamento do Azure
Dados de diagnóstico não são armazenados permanentemente, a menos que você transferir emulador de armazenamento do Microsoft Azure toohello ou tooAzure armazenamento. Quando estiverem no armazenamento, eles poderão ser exibidos com uma das várias ferramentas disponíveis.

## <a name="specify-a-storage-account"></a>Especificar uma conta de armazenamento
Você especificar conta de armazenamento de saudação que você deseja toouse no arquivo ServiceConfiguration cscfg hello. informações de conta de saudação são definidas como uma cadeia de caracteres de conexão em uma definição de configuração. Olá, exemplo a seguir mostra cadeia de conexão padrão Olá criada para um novo projeto de serviço de nuvem no Visual Studio:

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
    </ConfigurationSettings>
```

Você pode alterar esses informações de conta de tooprovide da cadeia de conexão para uma conta de armazenamento do Azure.

Dependendo do tipo de saudação de dados de diagnóstico que está sendo coletados, o diagnóstico do Azure usa o serviço de Blob hello ou serviço de tabela de saudação. Olá tabela a seguir mostra as fontes de dados de saudação que são mantidas e seu formato.

| Fonte de dados | Formato de armazenamento |
| --- | --- |
| Logs do Azure |Tabela |
| Logs do IIS 7.0 |Blob |
| Logs de infraestrutura do Diagnóstico do Azure |Tabela |
| Logs de Rastreamento de Solicitação com Falha |Blob |
| Log de eventos do Windows |Tabela |
| Contadores de desempenho |Tabela |
| Despejos de falhas |Blob |
| Logs de erros personalizados |Blob |

## <a name="transfer-diagnostic-data"></a>Transferir dados de diagnóstico
2.5 do SDK e posterior, dados de diagnóstico Olá solicitação tootransfer podem ocorrer por meio do arquivo de configuração de saudação. Você pode transferir dados de diagnóstico em intervalos agendados, como especificado na configuração de saudação.

Para SDK 2.4 e anterior pode solicitar dados de diagnóstico tootransfer hello como programaticamente por meio do arquivo de configuração de saudação. abordagem programática Olá permite transferências sob demanda de toodo.

> [!IMPORTANT]
> Quando você transfere dados de diagnóstico tooan conta de armazenamento do Azure, incorre em custos Olá para recursos de armazenamento que usa os dados de diagnóstico.
> 
> 

## <a name="store-diagnostic-data"></a>Armazenar dados de diagnóstico
Dados de log são armazenados no armazenamento de BLOBs ou tabelas com hello nomes a seguir:

**Tabelas**

* **WadLogsTable** - Logs escritos em código usando o ouvinte de rastreamento de saudação.
* **WADDiagnosticInfrastructureLogsTable** - monitor de diagnóstico e alterações de configuração.
* **WADDirectoriesTable** – diretórios de monitor de diagnóstico que hello está monitorando.  Isso inclui logs do IIS, logs de solicitação do IIS com falha e diretórios personalizados.  local Olá Olá blob do arquivo de log especificado no campo de contêiner de saudação e nome de saudação do blob Olá é no campo RelativePath de saudação.  campo AbsolutePath de saudação indica Olá local e o nome do arquivo hello como existia na máquina virtual do Azure de saudação.
* **WADPerformanceCountersTable** – contadores de desempenho.
* **WADWindowsEventLogsTable** – logs de Eventos do Windows.

**Blobs**

* **wad-control-container** – (somente para o SDK 2.4 e anterior) contém arquivos de configuração XML de saudação que controla Olá diagnóstico do Azure.
* **wad-iis-failedreqlogfiles** – contém informações de logs de solicitação com falha do IIS.
* **wad-iis-logfiles** – contém informações sobre logs do IIS.
* **"custom"** – um contêiner personalizado com base na configuração dos diretórios que são monitorados pelo monitor de diagnóstico hello.  Olá nome desse contêiner de blob será especificado em WADDirectoriesTable.

## <a name="tools-tooview-diagnostic-data"></a>Dados de diagnóstico de tooview de ferramentas
Várias ferramentas são dados de saudação tooview disponível depois que ele toostorage transferido. Por exemplo:

* Gerenciador de servidores no Visual Studio - se você tiver instalado as ferramentas do Azure Olá para Microsoft Visual Studio, você pode usar nó de armazenamento do Azure Olá no Gerenciador de servidores tooview dados somente leitura blob e tabela de suas contas de armazenamento do Azure. Você pode exibir dados de conta do emulador de armazenamento local e também de contas de armazenamento que você criou para o Azure. Para obter mais informações, veja [Procurando e gerenciando recursos de armazenamento com o Gerenciador de Servidores](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md).
* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) é um aplicativo autônomo que permite que você tooeasily o trabalho com dados de armazenamento do Azure no Linux, Windows e OSX.
* [O estúdio de gerenciamento do Azure](http://www.cerebrata.com/products/azure-management-studio/introduction) inclui o Azure Diagnostics Manager que permite que você tooview, baixar e gerenciar dados de diagnóstico de Olá coletados pelos aplicativos Olá em execução no Azure.

## <a name="next-steps"></a>Próximas etapas
[Fluxo de saudação do rastreamento em um aplicativo de serviços de nuvem com o diagnóstico do Azure](cloud-services-dotnet-diagnostics-trace-flow.md)

