---
title: "aaaAzure diagnóstico versões de esquema de configuração de extensão e histórico | Microsoft Docs"
description: "Contadores de desempenho relevantes toocollecting em máquinas virtuais do Azure, conjuntos de escala de VM, serviço de malha e serviços de nuvem."
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/16/2017
ms.author: robb
ms.openlocfilehash: 854ad118f660810aa38703670284794d658142c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-diagnostics-extention-configuration-schema-versions-and-history"></a>Versões de esquema de configuração da extensão do Diagnóstico do Azure
Esta página de índices versões de esquema de extensão de diagnóstico do Azure é fornecido como parte do hello SDK do Microsoft Azure.  

> [!NOTE]
> Olá extensão de diagnóstico do Azure é o componente Olá usado toocollect contadores de desempenho e outras estatísticas de:
> - Máquinas Virtuais do Azure 
> - Conjuntos de Escala de Máquina Virtual
> - Service Fabric 
> - Serviços de Nuvem 
> - Grupos de segurança de rede
> 
> Esta página só é relevante se você estiver usando um desses serviços.

Olá extensão de diagnóstico do Azure é usado com outros produtos da Microsoft diagnóstico como Monitor do Azure, Application Insights e análise de Log. Para saber mais, veja [Visão geral das ferramentas de monitoramento da Microsoft](monitoring-overview.md).

## <a name="azure-sdk-and-diagnostics-versions-shipping-chart"></a>Gráfico de envio de versões do SDK e Diagnóstico do Azure  

|Versão do SDK do Azure | Versão da extensão do Diagnóstico | Modelo|  
|------------------|-------------------------------|------|  
|1.x               |1.0                            |plug-in|  
|2.0 - 2.4         |1.0                            |plug-in|  
|2.5               |1.2                            |extensão|  
|2.6               |1,3                            |"|  
|2.7               |1.4                            |"|  
|2.8               |1.5                            |"|  
|2,9               |1.6                            |"|
|2.96              |1.7                            |"|
|2.96              |1.8                            |"|
|2.96              |1.8.1                          |"|
|2.96              |1.9                            |"|



 Diagnóstico do Azure versão 1.0 primeiro enviado em um modelo de plug-in--que significa que, quando você instalou Olá SDK do Azure, você obteve versão de saudação do diagnóstico do Azure acompanha a ele.  

 Começando com o SDK 2.5 (Diagnóstico versão 1.2), o diagnóstico do Azure deu tooan modelo de extensão. novos recursos do Hello ferramentas tooutilize só estavam disponíveis em mais recente SDKs do Azure, mas qualquer serviço usando o diagnóstico do Azure escolheria a versão mais recente de envio Olá diretamente do Azure. Por exemplo, qualquer pessoa ainda usando o SDK 2.5 seria Carregando versão mais recente do hello mostrado na tabela anterior de saudação, independentemente se eles estão usando recursos mais recentes de saudação.  

## <a name="schemas-index"></a>Índice de esquemas  
Versões diferentes do Diagnóstico do Azure usam esquemas de configuração diferentes. 

[Esquema de Configuração do Diagnóstico 1.0](azure-diagnostics-schema-1dot0.md)  

[Esquema de Configuração do Diagnóstico 1.2](azure-diagnostics-schema-1dot2.md)  

[Esquema de Configuração do Diagnóstico 1.3 e posterior](azure-diagnostics-schema-1dot3-and-later.md)  

## <a name="version-history"></a>Histórico de versão


### <a name="diagnostics-extension-19"></a>Extensão do Diagnóstico 1.9 
Adicionar suporte ao Docker.


### <a name="diagnostics-extension-181"></a>Extensão do Diagnóstico 1.8.1 
Pode especificar um token SAS em vez de uma chave de conta de armazenamento na configuração privada hello. Se for fornecido um token SAS, chave de conta de armazenamento Olá será ignorado.


```json
{
    "storageAccountName": "diagstorageaccount",
    "storageAccountEndPoint": "https://core.windows.net",
    "storageAccountSasToken": "{sas token}",
    "SecondaryStorageAccounts": {
        "StorageAccount": [
            {
                "name": "secondarydiagstorageaccount",
                "endpoint": "https://core.windows.net",
                "sasToken": "{sas token}"
            }
        ]
    }
}
```

```xml
<PrivateConfig>
    <StorageAccount name="diagstorageaccount" endpoint="https://core.windows.net" sasToken="{sas token}" />
    <SecondaryStorageAccounts>
        <StorageAccount name="secondarydiagstorageaccount" endpoint="https://core.windows.net" sasToken="{sas token}" />
    </SecondaryStorageAccounts>
</PrivateConfig>
```


### <a name="diagnostics-extension-18"></a>Extensão do Diagnóstico 1.8 
Adicionado tooPublicConfig do tipo de armazenamento. StorageType pode ser *Table*, *Blob*, *TableAndBlob*. *Tabela* é saudação padrão.


```json
{
    "WadCfg": {
    },
    "StorageAccount": "diagstorageaccount",
    "StorageType": "TableAndBlob"
}
```

```xml
<PublicConfig>
    <WadCfg />
    <StorageAccount>diagstorageaccount</StorageAccount>
    <StorageType>TableAndBlob</StorageType>
</PublicConfig>
```


### <a name="diagnostics-extension-17"></a>Extensão do Diagnóstico 1.7 
Olá adicionado capacidade tooroute tooEventHub.

### <a name="diagnostics-extension-15"></a>Extensão do diagnóstico 1.5
Adicionada a saudação Coletores de dados de diagnóstico do elemento e hello capacidade toosend muito[Application Insights](../application-insights/app-insights-cloudservices.md) tornando mais fácil problemas de toodiagnose em seu aplicativo, bem como o nível de sistema e a infraestrutura de saudação.

### <a name="azure-sdk-26-and-diagnostics-extension-13"></a>SDK 2.6 do Azure e esquema de extensão 1.3 
Para projetos de serviço de nuvem no Visual Studio, Olá as seguintes alterações foram feita. (Essas alterações também se aplicam a versões toolater do SDK do Azure.)

* emulador local Olá agora dá suporte a diagnóstico. Isso significa que você pode coletar dados de diagnóstico e certifique-se de que seu aplicativo está criando Olá rastreamentos direito enquanto você estiver desenvolvendo e testando no Visual Studio. Olá a cadeia de caracteres de conexão `UseDevelopmentStorage=true` habilita a coleta de dados de diagnóstico durante a execução do seu projeto de serviço de nuvem no Visual Studio usando o emulador de armazenamento do Azure hello. Todos os dados de diagnóstico são coletados na conta de armazenamento da saudação (armazenamento de desenvolvimento).
* cadeia de conexão de conta para armazenamento de diagnóstico Hello (windowsazure) é armazenada novamente no arquivo de configuração (. cscfg) do serviço de saudação. No Azure SDK 2.5 conta de armazenamento de diagnóstico Olá foi especificada no arquivo de wadcfgx de saudação.

Há algumas diferenças importantes entre como cadeia de caracteres de conexão Olá funcionou no SDK do Azure 2.4 e anterior e como ele funciona no Azure SDK 2.6 e posterior.

* No Azure SDK 2.4 e anterior, cadeia de caracteres de conexão Olá foi usada como um tempo de execução por Olá diagnóstico plug-in tooget Olá informações conta de armazenamento para a transferência de logs de diagnóstico.
* No Azure SDK 2.6 e posterior, a cadeia de caracteres de conexão de diagnóstico Olá é usada pela extensão de diagnóstico do Visual Studio tooconfigure Olá com informações de conta de armazenamento apropriado Olá durante a publicação. cadeia de caracteres de conexão Olá permite definir contas de armazenamento diferentes para as configurações de serviço diferente que o Visual Studio usará ao publicar. No entanto, porque o diagnóstico de saudação plug-in não está mais disponível (após 2.5 do SDK do Azure), arquivo. cscfg Olá por si só não é possível habilitar Olá extensão de diagnóstico. Você tem extensão de saudação tooenable separadamente através de ferramentas como o Visual Studio ou PowerShell.
* processo de saudação toosimplify de configuração de extensão de diagnóstico Olá com o PowerShell, saída de pacote de saudação do Visual Studio também contém Olá pública XML de configuração para extensão de diagnóstico Olá para cada função. O Visual Studio usa Olá diagnóstico conexão cadeia de caracteres toopopulate Olá armazenamento conta informações presentes na configuração pública hello. arquivos de configuração pública Olá são criados na pasta de extensões hello e seguem o padrão de saudação PaaSDiagnostics. <RoleName>. PubConfig.xml. Todas as implantações do PowerShell com base podem usar este padrão toomap tooa cada configuração função.
* Olá cadeia de caracteres de conexão no arquivo. cscfg de saudação também é usada por Olá dados de diagnóstico de saudação tooaccess portal do Azure para que possa aparecer em hello **monitoramento** cadeia de caracteres de conexão do guia Olá é necessário tooconfigure Olá serviço tooshow detalhado dados de monitoramento no portal de saudação.

#### <a name="migrating-projects-tooazure-sdk-26-and-later"></a>Migrando projetos tooAzure SDK 2.6 e posterior
Ao migrar do Azure SDK 2.5 tooAzure SDK 2.6 ou posterior, se você tiver uma conta de armazenamento de diagnóstico especificada no arquivo de .wadcfgx Olá, em seguida, ele permanecerá lá. contas tootake aproveitar a flexibilidade de saudação do uso de armazenamento diferentes para configurações de armazenamento diferente, você terá que toomanually Adicionar projeto de tooyour de cadeia de caracteres de conexão de saudação. Se você estiver migrando um projeto do SDK do Azure 2.4 ou tooAzure anterior 2.6 do SDK, em seguida, Olá diagnóstico cadeias de caracteres de conexão são preservadas. No entanto, observe alterações hello como cadeias de caracteres de conexão são tratadas no SDK 2.6 do Azure conforme especificado na seção anterior hello.

#### <a name="how-visual-studio-determines-hello-diagnostics-storage-account"></a>Como o Visual Studio determina a conta de armazenamento de diagnóstico Olá
* Se uma cadeia de caracteres de conexão de diagnóstico é especificada no arquivo. cscfg de hello, Visual Studio usa-extensão de diagnóstico Olá tooconfigure durante a publicação e ao gerar os arquivos de xml de configuração pública Olá durante o empacotamento.
* Se nenhuma cadeia de caracteres de conexão de diagnóstico é especificada no arquivo. cscfg de hello, em seguida, Visual Studio reverterá toousing conta de armazenamento de saudação especificada no hello .wadcfgx tooconfigure Olá diagnóstico extensão de arquivo ao publicar e gerando Olá público arquivos de xml de configuração ao empacotar.
* cadeia de conexão de diagnóstico Olá no arquivo. cscfg de saudação tem precedência sobre a conta de armazenamento Olá no arquivo de .wadcfgx hello. Se uma cadeia de caracteres de conexão de diagnóstico é especificado no arquivo. cscfg hello, em seguida, Visual Studio usa e ignora a conta de armazenamento Olá .wadcfgx.

#### <a name="what-does-hello-update-development-storage-connection-strings-checkbox-do"></a>O que does hello "Atualizar cadeias de conexão de armazenamento de desenvolvimento..." faz a caixa de seleção?
Olá a caixa de seleção **atualizar cadeias de conexão de armazenamento de desenvolvimento para diagnóstico e Caching com credenciais de conta de armazenamento do Microsoft Azure ao publicar tooMicrosoft Azure** oferece uma maneira conveniente tooupdate qualquer cadeias de conexão de conta de armazenamento de desenvolvimento com a conta de armazenamento do Azure Olá especificada durante a publicação.

Por exemplo, suponha que você selecionar essa caixa de seleção e especifica a cadeia de caracteres de conexão de diagnóstico Olá `UseDevelopmentStorage=true`. Quando você publica Olá projeto tooAzure, Visual Studio atualizará automaticamente o cadeia de caracteres de conexão de diagnóstico Olá com conta de armazenamento Olá especificada no Assistente de publicação de saudação. No entanto, se uma conta de armazenamento real foi especificada como cadeia de caracteres de conexão de diagnóstico Olá, em seguida, essa conta é usada em vez disso.

### <a name="diagnostics-functionality-differences-between-azure-sdk-24-and-earlier-and-azure-sdk-25-and-later"></a>Diferenças de funcionalidade de diagnóstico entre SDK do Azure 2.4 e anteriores e SDK do Azure 2.5 e posteriores
Se você estiver atualizando seu projeto do Azure SDK 2.4 tooAzure SDK 2.5 ou posterior, você deve ter em Olá mente diferenças de recursos de diagnóstico a seguir.

* **APIs de configuração estão preteridos** – A configuração programática de diagnóstico está disponível no SDK do Azure 2.4 ou anteriores, mas foi preterida no SDK do Azure 2.5 e posteriores. Se sua configuração de diagnóstico está definida atualmente no código, você precisará tooreconfigure essas configurações a partir do zero no projeto migrado de saudação na ordem de trabalho de tookeep de diagnóstico. arquivo de configuração de diagnóstico Olá para o SDK do Azure 2.4 é wadcfg e wadcfgx 2.5 do SDK do Azure e posterior.
* **Diagnóstico para aplicativos de serviço de nuvem pode ser configurado somente no nível de função hello, não no nível de instância de saudação.**
* **Sempre que você implantar seu aplicativo, a configuração de diagnóstico de saudação é atualizada** – isso pode causar problemas de paridade, se você alterar a configuração de diagnóstico do Gerenciador de servidores e, em seguida, reimplante o aplicativo.
* **No Azure SDK 2.5 e posterior, despejos de memória são configurados no arquivo de configuração de diagnóstico hello, não no código** – se você tiver despejos de memória configurados no código, você terá toomanually configuração de saudação de transferência de arquivo de configuração do código toohello, porque Olá despejos de memória não são transferidos durante a saudação migração tooAzure 2.6 do SDK.

