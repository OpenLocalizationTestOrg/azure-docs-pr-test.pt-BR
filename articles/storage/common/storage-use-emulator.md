---
title: "emulador de armazenamento do Azure aaaUse Olá para desenvolvimento e teste | Microsoft Docs"
description: "emulador de armazenamento do Azure Olá fornece um ambiente de desenvolvimento local livre para desenvolver e testar seus aplicativos de armazenamento do Azure. Saiba como solicitações são autenticadas, como tooconnect toohello emulador de seu aplicativo e como toouse Olá a ferramenta de linha de comando."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: f480b059-df8a-4a63-b05a-7f2f5d1f5c2a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: marsma
ms.openlocfilehash: 7cbe6ef5f172bb526c9d8a329b2fe9e6c0ec59d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-storage-emulator-for-development-and-testing"></a>Usar o emulador de armazenamento do Azure Olá para desenvolvimento e teste

emulador de armazenamento do Microsoft Azure Olá fornece um ambiente local que emula os serviços do Azure Blob, fila e tabela Olá para fins de desenvolvimento. Usando o emulador de armazenamento hello, você pode testar seu aplicativo nos serviços de armazenamento Olá localmente, sem criar uma assinatura do Azure ou incorrer em custos de qualquer. Quando estiver satisfeito com o funcionamento seu aplicativo no emulador hello, você pode alternar toousing uma conta de armazenamento do Azure na nuvem hello.

## <a name="get-hello-storage-emulator"></a>Obter o emulador de armazenamento Olá
Olá emulador de armazenamento está disponível como parte da saudação [SDK do Microsoft Azure](https://azure.microsoft.com/downloads/). Você também pode instalar o emulador de armazenamento hello usando Olá [instalador autônomo](https://go.microsoft.com/fwlink/?linkid=717179&clcid=0x409) (download direto). emulador de armazenamento do tooinstall hello, você deve ter privilégios administrativos no computador.

emulador de armazenamento Olá atualmente é executado somente no Windows. Para aqueles que considerar um emulador de armazenamento para Linux, uma opção é a comunidade Olá mantida, o emulador de armazenamento do código-fonte aberto [Azurite](https://github.com/arafato/azurite).

> [!NOTE]
> Os dados criados em uma versão do emulador de armazenamento Olá não são garantidos toobe acessível ao usar uma versão diferente. Se você precisar toopersist seus dados de longo prazo do hello, é recomendável que você armazene esses dados em uma conta de armazenamento do Azure, em vez de no emulador de armazenamento hello.
> <p/>
> emulador de armazenamento Olá depende versões específicas de bibliotecas de OData hello. Substituir Olá OData DLLs usadas pelo emulador de armazenamento Olá com outras versões não tem suporte e pode causar um comportamento inesperado. No entanto, qualquer versão do OData com suporte pelo serviço de armazenamento de saudação pode ser usado toosend solicitações toohello emulador.
>

## <a name="how-hello-storage-emulator-works"></a>Como funciona o emulador de armazenamento Olá
emulador de armazenamento Olá usa uma instância local do Microsoft SQL Server e serviços de armazenamento do Azure tooemulate do sistema de arquivos local hello. Por padrão, o emulador de armazenamento Olá usa um banco de dados no Microsoft SQL Server 2012 Express LocalDB. Você pode escolher uma instância local do SQL Server em vez de instância de LocalDB Olá para tooconfigure tooaccess de emulador de armazenamento de saudação. Para obter mais informações, consulte Olá [iniciar e inicializar Olá emulador de armazenamento](#start-and-initialize-the-storage-emulator) seção mais adiante neste artigo.

emulador de armazenamento Olá conecta tooSQL Server ou LocalDB usando a autenticação do Windows.

Existem algumas diferenças na funcionalidade entre o emulador de armazenamento hello e serviços de armazenamento do Azure. Para obter mais informações sobre essas diferenças, consulte Olá [diferenças entre o emulador de armazenamento hello e armazenamento do Azure](#differences-between-the-storage-emulator-and-azure-storage) seção mais adiante neste artigo.

## <a name="start-and-initialize-hello-storage-emulator"></a>Iniciar e inicializar o emulador de armazenamento Olá
emulador de armazenamento do Azure de saudação toostart:
1. Selecione Olá **iniciar** Olá botão ou pressione **Windows** chave.
1. Comece digitando `Azure Storage Emulator`.
1. Selecione o emulador de saudação da lista de saudação de aplicativos exibidos.

Quando o emulador de armazenamento Olá é iniciado, será exibida uma janela de Prompt de comando. Usar este console janela toostart e parar Olá emulador de armazenamento, limpe os dados, obter o status e inicializar o emulador de saudação. Para obter mais informações, consulte Olá [referência de ferramenta de linha de comando do emulador de armazenamento](#storage-emulator-command-line-tool-reference) seção mais adiante neste artigo.

Quando o emulador de saudação estiver em execução, você verá um ícone na Olá área de notificação de barra de tarefas do Windows.

Quando você fechar a janela de Prompt de comando de emulador de armazenamento Olá, o emulador de armazenamento Olá continuará toorun. toobring a janela de console do emulador de armazenamento Olá novamente, siga Olá etapas anteriores, como se estivesse iniciando o emulador de armazenamento hello.

Olá primeira vez que executar o emulador de armazenamento hello, ambiente de armazenamento local de saudação é inicializado para você. o processo de inicialização Olá cria um banco de dados no LocalDB e reserva portas HTTP para cada serviço de armazenamento local.

emulador de armazenamento Olá também é instalado por padrão`C:\Program Files (x86)\Microsoft SDKs\Azure\Storage Emulator`.

> [!TIP]
> Você pode usar o hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) toowork com recursos de emulador de armazenamento local. Procure por "(desenvolvimento)" em "Contas de armazenamento" na árvore de recursos do Gerenciador de armazenamento Olá depois de instalado e iniciado o emulador de armazenamento hello.
>

### <a name="initialize-hello-storage-emulator-toouse-a-different-sql-database"></a>Inicializar toouse emulador de armazenamento Olá outro banco de dados SQL
Você pode usar Olá armazenamento emulador ferramenta de linha de comando tooinitialize Olá armazenamento emulador toopoint tooa SQL banco de dados instância diferente da instância de LocalDB saudação padrão:

1. Janela de console do emulador de armazenamento Olá aberta conforme descrito em Olá [iniciar e inicializar Olá emulador de armazenamento](#start-and-initialize-the-storage-emulator) seção.
1. Na janela de console hello, digite Olá a seguir de comando, onde `<SQLServerInstance>` é nome Olá Olá instância do SQL Server. toouse LocalDB, especifique `(localdb)\MSSQLLocalDb` como instância do SQL Server hello.

  `AzureStorageEmulator.exe init /server <SQLServerInstance>`

  Você também pode usar o hello comando, que direciona o hello emulador toouse Olá instância padrão do SQL Server a seguir:

  `AzureStorageEmulator.exe init /server .\\`

  Ou, você pode usar o hello comando, que reinicializa a instância de LocalDB Olá banco de dados toohello padrão a seguir:

  `AzureStorageEmulator.exe init /forceCreate`

Para saber mais sobre esses comandos, consulte [Referência da ferramenta de linha de comando do emulador de armazenamento](#storage-emulator-command-line-tool-reference).

> [!TIP]
> Você pode usar o hello [Microsoft SQL Server Management Studio](/sql/ssms/download-sql-server-management-studio-ssms) toomanage (SSMS) instâncias do SQL Server, incluindo a instalação de LocalDB hello. Em Olá SMSS **conectar tooServer** caixa de diálogo, especifique `(localdb)\MSSQLLocalDb` em Olá **nome do servidor:** instância do campo tooconnect toohello LocalDB.

## <a name="authenticating-requests-against-hello-storage-emulator"></a>Autenticar solicitações no emulador de armazenamento Olá
Depois de instalado e iniciado o emulador de armazenamento hello, você pode testar seu código em relação a ela. Assim como acontece com o armazenamento do Azure na nuvem hello, cada solicitação feita no emulador de armazenamento Olá deve ser autenticada, a menos que seja uma solicitação anônima. Você pode autenticar solicitações no emulador de armazenamento hello usando a autenticação de chave compartilhada ou com uma assinatura de acesso compartilhado (SAS).

### <a name="authenticate-with-shared-key-credentials"></a>Autenticar com credenciais de Chave Compartilhada
[!INCLUDE [storage-emulator-connection-string-include](../../../includes/storage-emulator-connection-string-include.md)]

Para obter mais informações sobre cadeias de conexão, consulte [Configurar cadeias de conexão do Armazenamento do Azure](../storage-configure-connection-string.md).

### <a name="authenticate-with-a-shared-access-signature"></a>Autenticar com assinatura de acesso compartilhado
Algumas bibliotecas de cliente de armazenamento do Azure, como a biblioteca de Xamarin hello, só oferecem suporte à autenticação com um token de acesso compartilhado (SAS) de assinatura. Você pode criar o token SAS hello usando uma ferramenta como Olá [Gerenciador de armazenamento](http://storageexplorer.com/) ou outro aplicativo que oferece suporte à autenticação de chave compartilhada.

Você também pode gerar um token SAS usando o Azure PowerShell. Olá exemplo a seguir gera um token SAS com contêiner de blob tooa permissões completas:

1. Instale o Azure PowerShell se você ainda não fez isso (usando a versão mais recente Olá de saudação cmdlets do PowerShell do Azure é recomendado). Para obter instruções de instalação, consulte [Instalar e configurar o Azure PowerShell](/powershell/azure/install-azurerm-ps).
2. Abra o Azure PowerShell e execute Olá comandos a seguir, substituindo `ACCOUNT_NAME` e `ACCOUNT_KEY==` com suas próprias credenciais, e `CONTAINER_NAME` com um nome de sua escolha:

```powershell
$context = New-AzureStorageContext -StorageAccountName "ACCOUNT_NAME" -StorageAccountKey "ACCOUNT_KEY=="

New-AzureStorageContainer CONTAINER_NAME -Permission Off -Context $context

$now = Get-Date

New-AzureStorageContainerSASToken -Name CONTAINER_NAME -Permission rwdl -ExpiryTime $now.AddDays(1.0) -Context $context -FullUri
```

assinatura de acesso compartilhado resultante URI Olá para o novo contêiner de saudação deve ser semelhante a:

```
https://storageaccount.blob.core.windows.net/sascontainer?sv=2012-02-12&se=2015-07-08T00%3A12%3A08Z&sr=c&sp=wl&sig=t%2BbzU9%2B7ry4okULN9S0wst%2F8MCUhTjrHyV9rDNLSe8g%3Dsss
```

assinatura de acesso compartilhado Olá criada com este exemplo é válida para um dia. assinatura de saudação concede acesso total (leitura, gravação, exclusão, lista) tooblobs dentro do contêiner de saudação.

Para saber mais sobre assinaturas de acesso compartilhado, confira [Uso de SAS (Assinaturas de Acesso Compartilhado) no Armazenamento do Azure](../storage-dotnet-shared-access-signature-part-1.md).

## <a name="addressing-resources-in-hello-storage-emulator"></a>Endereçamento de recursos no emulador de armazenamento Olá
Olá pontos de extremidade de serviço para o emulador de armazenamento Olá são diferentes de uma conta de armazenamento do Azure. diferença de saudação é porque o computador local Olá não executa resolução de nome de domínio, que exigem endereços locais do toobe de pontos de extremidade de emulador do hello armazenamento.

Ao endereçar um recurso em uma conta de armazenamento do Azure, você pode usar Olá esquema a seguir. nome da conta de saudação é parte do nome de host URI hello e recurso de saudação que é endereçado faz parte do caminho de URI de saudação:

`<http|https>://<account-name>.<service-name>.core.windows.net/<resource-path>`

Por exemplo, hello URI a seguir é um endereço válido para um blob em uma conta de armazenamento do Azure:

`https://myaccount.blob.core.windows.net/mycontainer/myblob.txt`

No entanto, Olá emulador de armazenamento, porque o computador local Olá não executa resolução de nome de domínio, nome da conta Olá faz parte do caminho URI de saudação em vez do nome de host de saudação. Use Olá seguindo o formato URI para um recurso no emulador de armazenamento hello:

`http://<local-machine-address>:<port>/<account-name>/<resource-path>`

Por exemplo, hello seguinte endereço pode ser usado para acessar um blob no emulador de armazenamento hello:

`http://127.0.0.1:10000/myaccount/mycontainer/myblob.txt`

pontos de extremidade de serviço de saudação para o emulador de armazenamento Olá são:

* Serviço Blob: `http://127.0.0.1:10000/<account-name>/<resource-path>`
* Serviço Fila: `http://127.0.0.1:10001/<account-name>/<resource-path>`
* Serviço Tabela: `http://127.0.0.1:10002/<account-name>/<resource-path>`

### <a name="addressing-hello-account-secondary-with-ra-grs"></a>Conta de endereçamento Olá secundária com RA-GRS
A partir da versão 3.1, o emulador de armazenamento Olá dá suporte a replicação com redundância geográfica com acesso de leitura (RA-GRS). Para recursos de armazenamento em nuvem hello e no emulador local hello, você pode acessar o local secundário Olá acrescentando - nome da conta toohello secundário. Por exemplo, a saudação endereço a seguir pode ser usada para acessar um blob usando a réplica secundária somente leitura Olá no emulador de armazenamento hello:

`http://127.0.0.1:10000/myaccount-secondary/mycontainer/myblob.txt`

> [!NOTE]
> Para toohello acesso programático secundário com o emulador de armazenamento hello, use Olá biblioteca de cliente de armazenamento para .NET versão 3.2 ou posterior. Consulte Olá [biblioteca de cliente de armazenamento do Microsoft Azure para .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx) para obter detalhes.
>
>

## <a name="storage-emulator-command-line-tool-reference"></a>Referência da ferramenta de linha de comando do emulador de armazenamento
A partir da versão 3.0, uma janela do console é exibida quando você inicia o hello emulador de armazenamento. Use a linha de comando de Olá Olá console janela toostart e parar Olá emulador, bem como a consulta de status e executar outras operações.

> [!NOTE]
> Se você tiver Olá instalado do emulador de computação do Microsoft Azure, um ícone de bandeja do sistema é exibida quando você inicia o hello emulador de armazenamento. Clique duas vezes em Olá ícone tooreveal um menu que fornece uma maneira gráfica toostart e parar Olá emulador de armazenamento.
>
>

### <a name="command-line-syntax"></a>Sintaxe da linha de comando
`AzureStorageEmulator.exe [start] [stop] [status] [clear] [init] [help]`

### <a name="options"></a>Opções
lista de saudação tooview de opções, digite `/help` no prompt de comando hello.

| Opção | Descrição | Command | Argumentos |
| --- | --- | --- | --- |
| **Iniciar** |Inicia o emulador de armazenamento hello. |`AzureStorageEmulator.exe start [-inprocess]` |*-inprocess*: iniciar o emulador de saudação no processo atual de saudação em vez de criar um novo processo. |
| **Parar** |Paradas Olá emulador de armazenamento. |`AzureStorageEmulator.exe stop` | |
| **Status** |Imprime Olá status do emulador de armazenamento hello. |`AzureStorageEmulator.exe status` | |
| **Limpar** |Limpa os dados de saudação em todos os serviços especificados na linha de comando hello. |`AzureStorageEmulator.exe clear [blob] [table] [queue] [all]                                                    ` |*blob*: limpa os dados do blob. <br/>*fila*: limpa os dados da fila. <br/>*tabela*: limpa os dados de tabela. <br/>*todos*: limpa todos os dados em todos os serviços. |
| **Init** |Executa a inicialização única tooset o emulador de saudação. |<code>AzureStorageEmulator.exe init [-server serverName] [-sqlinstance instanceName] [-forcecreate&#124;-skipcreate] [-reserveports&#124;-unreserveports] [-inprocess]</code> |*-server nomedoservidor \ NomedaInstância*: Especifica o servidor de saudação hospedando a instância do SQL hello. <br/>*instanceName - sqlinstance*: especifica nome de saudação do hello toobe de instância SQL usada na instância de servidor padrão hello. <br/>*-forcecreate*: força a criação do banco de dados SQL hello, mesmo se ele já existe. <br/>*-skipcreate*: ignora a criação do banco de dados do SQL hello. Isso tem precedência sobre -forcecreate.<br/>*-reserveports*: tentativas de portas de saudação HTTP tooreserve associadas aos serviços de saudação.<br/>*-unreserveports*: tentativas tooremove reservas para portas Olá HTTP associadas aos serviços de saudação. Isso tem precedência sobre -reserveports.<br/>*-inprocess*: realiza a inicialização no processo atual de saudação em vez de gerar um novo processo. processo de saudação atual deve ser iniciado com permissões elevadas se a alteração de reservas de porta. |

## <a name="differences-between-hello-storage-emulator-and-azure-storage"></a>Diferenças entre o emulador de armazenamento hello e armazenamento do Azure
Como o emulador de armazenamento Olá é um ambiente emulado em execução em uma instância local do SQL, há diferenças na funcionalidade entre o emulador hello e uma conta de armazenamento do Azure na nuvem hello:

* emulador de armazenamento Olá oferece suporte a apenas uma única conta fixa e uma chave de autenticação conhecida.
* emulador de armazenamento Olá não é um serviço de armazenamento escalonável e não oferece suporte a um grande número de clientes simultâneos.
* Conforme descrito em [endereçamento de recursos no emulador de armazenamento Olá](#addressing-resources-in-the-storage-emulator), recursos sejam resolvidos de forma diferente no emulador de armazenamento Olá em comparação com uma conta de armazenamento do Azure. Essa diferença é como resolução de nome de domínio está disponível na nuvem hello, mas não no computador local de saudação.
* A partir da versão 3.1, conta do emulador de armazenamento Olá dá suporte a replicação com redundância geográfica com acesso de leitura (RA-GRS). No emulador do Windows hello, todas as contas têm RA-GRS habilitado, e nunca há qualquer atraso entre as réplicas primárias e secundárias hello. operações de obter status do serviço Blob, obter status do serviço de fila e obter status do serviço tabela Olá têm suporte na conta de saudação secundária e sempre retornará o valor Olá Olá `LastSyncTime` elemento de resposta como Olá atual tempo acordo toohello subjacente Banco de dados SQL.
* Olá serviço de arquivo e pontos de extremidade de serviço de protocolo SMB não têm suporte no emulador de armazenamento hello.
* Se você usar uma versão dos serviços de armazenamento de saudação que ainda não é suportada pelo emulador hello, o emulador de armazenamento Olá retornará um erro de VersionNotSupportedByEmulator (código de status HTTP 400 - Solicitação incorreta).

### <a name="differences-for-blob-storage"></a>Diferenças do armazenamento de blob
Olá diferenças a seguir se aplicam a armazenamento tooBlob no emulador hello:

* emulador de armazenamento Olá só oferece suporte a tamanhos de blob a too2 GB.
* Cópia incremental permite que os instantâneos de toobe de blobs substituído copiado, que retorna uma falha no serviço de saudação.
* O recurso Obter Diferença de Intervalos de Páginas não funciona entre os instantâneos copiados com o uso de um Blob de Cópia Incremental.
* Uma operação de colocar Blob poderá ser bem-sucedida em um blob existente no emulador de armazenamento Olá com uma concessão ativa, mesmo se a ID de concessão de saudação não foi especificado na solicitação de saudação.
* Anexe o emulador de saudação não dá suporte a operações de Blob. Tentar uma operação em um blob de anexo retornará um erro FeatureNotSupportedByEmulator (código de status HTTP 400 - Solicitação incorreta).

### <a name="differences-for-table-storage"></a>Diferenças do armazenamento de tabela
Olá diferenças a seguir se aplicam a armazenamento tooTable no emulador hello:

* Propriedades de data no hello serviço tabela no emulador de armazenamento Olá suportam apenas intervalo Olá suportado pelo SQL Server 2005 (são necessário toobe posterior a 1º de janeiro de 1753). Todas as datas anteriores a 1º de janeiro de 1753 são alteradas toothis valor. Olá, precisão de datas é limitado toohello precisão do SQL Server 2005, que significa que as datas são precisas too1/300 de segundo.
* emulador de armazenamento Olá dá suporte a valores de propriedade de chave linha e chave de partição de menos de 512 bytes cada. Além disso, Olá tamanho total do nome da conta Olá, nome da tabela e nomes de propriedade de chave juntos não pode exceder 900 bytes.
* tamanho total de saudação de uma linha em uma tabela no emulador de armazenamento Olá é tooless limitado de 1 MB.
* No emulador de armazenamento hello, propriedades de dados do tipo `Edm.Guid` ou `Edm.Binary` suporte somente Olá `Equal (eq)` e `NotEqual (ne)` cadeias de caracteres de filtro de operadores de comparação na consulta.

### <a name="differences-for-queue-storage"></a>Diferenças do armazenamento de fila
Não há nenhum armazenamento de tooQueue específico diferenças no emulador de saudação.

## <a name="storage-emulator-release-notes"></a>Notas de versão do emulador de armazenamento
### <a name="version-52"></a>Versão 5.2
* emulador de armazenamento Olá agora oferece suporte à versão de 2017-04-17 Olá de serviços de armazenamento nos pontos de extremidade de serviço de Blob, fila e tabela.
* Correção de um bug em que os valores de propriedade de tabela não estavam sendo codificados corretamente.

### <a name="version-51"></a>Versão 5.1
* Correção de bug em que o emulador de armazenamento Olá estava retornando Olá `DataServiceVersion` cabeçalho em algumas respostas em que o serviço Olá não foi.

### <a name="version-50"></a>Versão 5.0
* instalador de emulador de armazenamento Olá não verificará mais MSSQL existente e instala o .NET Framework.
* instalador de emulador de armazenamento Olá não cria o banco de dados de saudação como parte da instalação. O banco de dados ainda será criado como parte da inicialização se necessário.
* A criação de banco de dados não requer elevação.
* Reservas de porta não são mais necessários para a inicialização.
* Adiciona Olá as opções a seguir muito`init`: `-reserveports` (requer elevação), `-unreserveports` (requer elevação), `-skipcreate`.
* Olá opção de interface do usuário o emulador de armazenamento no ícone de bandeja do sistema Olá agora inicia Olá interface de linha de comando. Olá antiga interface gráfica do usuário não está mais disponível.
* Algumas DLLs foram removidas ou renomeadas.

### <a name="version-46"></a>Versão 4.6
* emulador de armazenamento Olá agora oferece suporte à versão 2016-05-31 Olá de serviços de armazenamento em pontos de extremidade de serviço Blob, fila e tabela.

### <a name="version-45"></a>Versão 4.5
* Correção de bug que causou a inicialização e a instalação de saudação toofail de emulador de armazenamento quando Olá fazendo o banco de dados foi renomeado.

### <a name="version-44"></a>Versão 4.4
* emulador de armazenamento Olá agora oferece suporte à versão 2015-12-11 Olá de serviços de armazenamento em pontos de extremidade de serviço Blob, fila e tabela.
* Olá coleta de lixo do emulador de armazenamento de dados de blob agora é mais eficiente ao lidar com um grande número de blobs.
* Correção de bug que causou o contêiner toobe ACL XML validado ligeiramente diferente de como o serviço de armazenamento de saudação faz isso.
* Correção de bug que fez com que, às vezes, max e min toobe de valores de data e hora relatado no fuso horário incorreto hello.

### <a name="version-43"></a>Versão 4.3
* emulador de armazenamento Olá agora oferece suporte à versão 2015-07-08 Olá de serviços de armazenamento em pontos de extremidade de serviço Blob, fila e tabela.

### <a name="version-42"></a>Versão 4.2
* emulador de armazenamento Olá agora oferece suporte à versão 2015-04-05 Olá de serviços de armazenamento em pontos de extremidade de serviço Blob, fila e tabela.

### <a name="version-41"></a>Versão 4.1
* emulador de armazenamento Olá agora dá suporte a versão 2015-02-21 Olá de serviços de armazenamento no Blob, fila e tabela de pontos de extremidade, exceto para os novos recursos de Blob de acréscimo hello.
* Se você usar uma versão dos serviços de armazenamento de saudação que ainda não é suportada pelo emulador Olá, o emulador Olá retorna uma mensagem de erro significativo. É recomendável usar a versão mais recente de saudação do emulador hello. Se você encontrar um erro de VersionNotSupportedByEmulator (código de status HTTP 400 - Solicitação incorreta), baixe a versão mais recente saudação do emulador de armazenamento hello.
* Correção de bug no qual uma corrida condição que causou tabela entidade dados toobe incorreta durante as operações de mesclagem simultâneos.

### <a name="version-40"></a>Versão 4.0
* emulador de armazenamento Olá executável foi renomeado muito*AzureStorageEmulator.exe*.

### <a name="version-32"></a>Versão 3.2
* emulador de armazenamento Olá agora dá suporte a versão 2014-02-14 dos serviços de armazenamento de saudação em pontos de extremidade de serviço Blob, fila e tabela. Pontos de extremidade de serviço de arquivo não têm suporte no momento no emulador de armazenamento hello. Consulte [controle de versão para Olá serviços de armazenamento do Azure](/rest/api/storageservices/Versioning-for-the-Azure-Storage-Services) para obter detalhes sobre a versão 2014-02-14.

### <a name="version-31"></a>Versão 3.1
* Agora há suporte para o armazenamento com redundância geográfica com acesso de leitura (RA-GRS) no emulador de armazenamento hello. Status do serviço Blob Olá obter, obter status do serviço de fila e obter APIs de estatísticas de serviço de tabela têm suporte para a conta de saudação secundária e sempre retornará o valor de saudação do elemento de resposta de LastSyncTime hello como Olá atual toohello acordo de tempo subjacente SQL banco de dados. Para toohello acesso programático secundário com o emulador de armazenamento hello, use Olá biblioteca de cliente de armazenamento para .NET versão 3.2 ou posterior. Consulte Olá biblioteca de cliente de armazenamento do Microsoft Azure para referência do .NET para obter detalhes.

### <a name="version-30"></a>Versão 3.0
* emulador de armazenamento do Azure Olá não é enviado em Olá mesmo pacote que o emulador de computação do hello.
* interface gráfica do usuário do Hello storage emulator está preterida em favor de uma interface de linha de comando programável. Para obter detalhes sobre a interface de linha de comando hello, consulte a referência da ferramenta de linha de comando do armazenamento emulador. interface gráfica Olá continuará toobe presente na versão 3.0, mas ele só pode ser acessado quando Olá emulador de computação é instalado, clicando duas vezes no ícone de bandeja do sistema hello e selecionando Mostrar UI do emulador de armazenamento.
* A versão 2013-08-15 dos serviços de armazenamento do Azure Olá agora tem suporte total. (Anteriormente nesta versão só tinha suporte do emulador de armazenamento versão 2.2.1 Preview.)

## <a name="next-steps"></a>Próximas etapas

* Avaliar o emulador de armazenamento de plataforma cruzada, mantida a comunidade de código aberto Olá [Azurite](https://github.com/arafato/azurite). 
* [Exemplos de armazenamento do Azure usando o .NET](../storage-samples-dotnet.md) contém exemplos de código tooseveral links você pode usar ao desenvolver seu aplicativo.
* Você pode usar o hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) toowork com recursos na sua conta de armazenamento de nuvem e no emulador de armazenamento hello.
