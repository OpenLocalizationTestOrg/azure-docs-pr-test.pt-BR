---
title: aaaDevelop localmente com hello Azure Cosmos DB emulador | Microsoft Docs
description: "Usando hello Azure Cosmos DB emulador, você pode desenvolver e testar seu aplicativo localmente para livre, sem criar uma assinatura do Azure."
services: cosmos-db
documentationcenter: 
keywords: Emulador do Azure Cosmos DB
author: arramac
manager: jhubbard
editor: 
ms.assetid: 90b379a6-426b-4915-9635-822f1a138656
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: arramac
ms.openlocfilehash: fb5449489e5f71664e72d8e11e583315be371bf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-cosmos-db-emulator-for-local-development-and-testing"></a>Use hello Azure Cosmos DB emulador para teste e desenvolvimento local

<table>
<tr>
  <td><strong>Binários</strong></td>
  <td>[Baixar MSI](https://aka.ms/cosmosdb-emulator)</td>
</tr>
<tr>
  <td><strong>Docker</strong></td>
  <td>[Hub de Docker](https://hub.docker.com/r/microsoft/azure-documentdb-emulator/)</td>
</tr>
<tr>
  <td><strong>Fonte de Docker</strong></td>
  <td>[Github](https://github.com/azure/azure-documentdb-emulator-docker)</td>
</tr>
</table>
  
Hello Azure Cosmos DB emulador fornece um ambiente local que emula Olá serviço de banco de dados do Azure Cosmos para fins de desenvolvimento. Usando hello Azure Cosmos DB emulador, você pode desenvolver e testar seu aplicativo localmente, sem criar uma assinatura do Azure ou incorrer em todos os custos. Quando estiver satisfeito com como seu aplicativo está funcionando no hello Azure Cosmos DB emulador, você pode alternar toousing uma conta de banco de dados do Azure Cosmos na nuvem hello.

Este artigo aborda Olá tarefas a seguir: 

> [!div class="checklist"]
> * Instalando Olá emulador
> * Executando Olá emulador no Docker para Windows
> * Autenticar solicitações
> * Usando Olá Explorador de dados em Olá emulador
> * Exportar certificados SSL
> * Chamar hello emulador da linha de comando Olá
> * Coletar arquivos de rastreamento

É recomendável que guia de Introdução observando Olá seguindo o vídeo, onde Kirill Gavrylyuk mostra como tooget iniciada com hello Azure Cosmos DB emulador. Observe que o vídeo Olá refere-se toohello emulador como Olá emulador de documentos, mas própria ferramenta de saudação foi renomeada hello Azure Cosmos DB emulador desde colar vídeo hello. Todas as informações no hello vídeo são ainda são precisas para hello Azure Cosmos DB emulador. 

> [!VIDEO https://channel9.msdn.com/Events/Connect/2016/192/player]
> 
> 

## <a name="how-hello-emulator-works"></a>Como funciona a saudação emulador
Olá emulador do Azure Cosmos DB emula uma alta fidelidade de saudação serviço de banco de dados do Azure Cosmos. Ele dá suporte a uma funcionalidade idêntica ao Azure Cosmos DB, incluindo suporte para criar e consultar documentos JSON, provisionar e dimensionar coleções, bem como executar procedimentos armazenados e gatilhos. Você pode desenvolver e testar aplicativos usando hello Azure Cosmos DB emulador e implantá-las tooAzure em escala global fazendo apenas uma única configuração de alterar o ponto de extremidade de conexão de toohello para o banco de dados do Azure Cosmos.

Enquanto criamos uma emulação de local de alta fidelidade do serviço de banco de dados do Azure Cosmos real hello, a implementação de saudação do hello Azure Cosmos DB emulador é diferente do serviço de saudação. Por exemplo, hello Azure Cosmos DB emulador usa componentes de sistema operacional padrão como o sistema de arquivos local Olá para persistência e a pilha do protocolo HTTPS para conectividade. Isso significa que algumas funcionalidades que se baseia na infraestrutura do Azure, como replicação global, latência de milissegundo dígito de leituras/gravações e níveis de consistência ajustáveis não estão disponíveis por meio de hello Azure Cosmos DB emulador.

> [!NOTE]
> Neste Olá tempo Data Explorer no hello emulador só oferece suporte a criação de saudação de coleções de API de documentos e MongoDB. Atualmente, o Hello Data Explorer no emulador de saudação não oferece suporte para a criação de saudação de tabelas e gráficos. 

## <a name="system-requirements"></a>Requisitos do sistema
Olá emulador do Azure Cosmos DB tem Olá requisitos de hardware e software a seguir:

* Requisitos de software
  * Windows Server 2012 R2, Windows Server 2016 ou Windows 10
*   Requisitos mínimos de hardware
  * 2 GB de RAM
  * Espaço disponível no disco rígido de 10 GB

## <a name="installation"></a>Instalação
Você pode baixar e instalar hello Azure Cosmos DB emulador da saudação [Microsoft Download Center](https://aka.ms/cosmosdb-emulator). 

> [!NOTE]
> tooinstall, configurar e executar hello Azure Cosmos DB emulador, você deve ter privilégios administrativos no computador de saudação.

## <a name="running-on-docker-for-windows"></a>Executar no Docker para Windows

Olá emulador do Azure Cosmos banco de dados pode ser executado no Docker para Windows. Olá emulador não funciona no Docker para Oracle Linux.

Uma vez que [Docker para Windows](https://www.docker.com/docker-windows) instalado, você pode extrair imagem do emulador de saudação do Hub do Docker executando Olá após o comando do shell favorito (cmd.exe, PowerShell, etc.).

```      
docker pull microsoft/azure-cosmosdb-emulator 
```
imagem toostart hello, executar Olá comandos a seguir.

``` 
md %LOCALAPPDATA%\CosmosDBEmulatorCert 2>nul
docker run -v %LOCALAPPDATA%\CosmosDBEmulatorCert:c:\CosmosDBEmulator\CosmosDBEmulatorCert -P -t -i microsoft/azure-cosmosdb-emulator 
```

resposta de saudação tem a aparência a seguir toohello semelhante:

```
Starting Emulator
Emulator Endpoint: https://172.20.229.193:8081/
Master Key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==
Exporting SSL Certificate
You can import hello SSL certificate from an administrator command prompt on hello host by running:
cd /d %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
--------------------------------------------------------------------------------------------------
Starting interactive shell
``` 

Fechando interativa do shell hello quando Olá emulador foi iniciado será contêiner de desligamento Olá emulador do Windows.

Usar o ponto de extremidade de saudação e chave mestra da resposta de saudação no seu cliente e Importar certificado SSL da saudação para seu host. Olá tooimport certificado SSL, Olá a seguir de um prompt de comando do administrador:

```
cd %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
```


## <a name="start-hello-emulator"></a>Iniciar o emulador de saudação

Olá toostart emulador de banco de dados do Cosmos do Azure, selecione botão de início de saudação ou pressione a tecla do Windows hello. Comece digitando **emulador de banco de dados do Azure Cosmos**e selecione Olá emulador da lista de saudação de aplicativos. 

![Selecione Olá início botão ou pressione Olá tecla Windows, comece a digitar * * Azure Cosmos DB emulador * * e selecione Olá emulador da lista de saudação de aplicativos](./media/local-emulator/database-local-emulator-start.png)

Quando o emulador de saudação estiver em execução, você verá um ícone na Olá área de notificação de barra de tarefas do Windows. ![Notificação na barra de tarefas do emulador local do Azure Cosmos DB](./media/local-emulator/database-local-emulator-taskbar.png)

Olá emulador do Azure Cosmos DB por padrão é executado saudação do computador local ("localhost") escuta na porta 8081.

Hello Azure Cosmos DB emulador é instalado por padrão toohello `C:\Program Files\Azure Cosmos DB Emulator` directory. Você também pode iniciar e parar o emulador de saudação da saudação de linha de comando. Veja [Referência da ferramenta de linha de comando](#command-line) para obter mais informações.

## <a name="start-data-explorer"></a>Iniciar o Data Explorer

Quando o emulador do Azure Cosmos DB Olá inicia abrirá automaticamente hello Azure Cosmos DB Data Explorer no navegador. Olá endereço aparecerá como [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html). Se você fechar Olá explorer e gostaria de toore-open-lo mais tarde, você pode abrir Olá URL no seu navegador ou iniciá-lo do hello Azure Cosmos DB emulador no hello ícone de bandeja do Windows, conforme mostrado abaixo.

![Iniciador do Data Explorer do emulador local do Azure Cosmos DB](./media/local-emulator/database-local-emulator-data-explorer-launcher.png)

## <a name="checking-for-updates"></a>Procurando atualizações
O Data Explorer indica se há uma nova atualização disponível para download. 

> [!NOTE]
> Os dados criados em uma versão de hello Azure Cosmos DB emulador não são garantidos toobe acessível ao usar uma versão diferente. Se você precisar toopersist seus dados de longo prazo do hello, é recomendável que você armazene esses dados em uma conta de banco de dados do Azure Cosmos, em vez de em hello Azure Cosmos DB emulador. 

## <a name="authenticating-requests"></a>Autenticar solicitações
Assim como com o banco de dados do Azure Cosmos na nuvem hello, todas as solicitações feitas em relação a saudação emulador do Azure Cosmos banco de dados devem ser autenticada. Hello Azure Cosmos DB emulador dá suporte a uma única conta fixa e uma chave de autenticação conhecido para a autenticação de chave mestra. A conta e a chave são credenciais de somente Olá permitidas para uso com hello Azure Cosmos DB emulador. Eles são:

    Account name: localhost:<port>
    Account key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==

> [!NOTE]
> chave mestra de saudação suportado pelo hello Azure Cosmos DB emulador destina-se a uso apenas com o emulador de saudação. Você não pode usar a conta de banco de dados do Azure Cosmos de produção e a chave com hello Azure Cosmos DB emulador. 

> [!NOTE] 
> Se você iniciou o emulador de saudação com hello opção /Key, use a tecla Olá gerado em vez de "C2y6yDjf5 Relational + ob0N8A7Cgv30VRDJIWEHLM + 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw = ="

Além disso, apenas Olá serviço de banco de dados do Azure Cosmos, hello Azure Cosmos DB emulador oferece suporte apenas para proteger a comunicação via SSL.

## <a name="running-hello-emulator-on-a-local-network"></a>Emulador de saudação em execução em uma rede local

Você pode executar o emulador de saudação em uma rede local. tooenable acesso à rede, especifique a opção de /AllowNetworkAccess Olá Olá [linha de comando](#command-line-syntax), que também requer que você especifique /Key = key_string ou /KeyFile = file_name. Você pode usar /GenKeyFile = file_name toogenerate um arquivo com uma chave aleatória antecipadamente.  Em seguida, você pode passar essa muito /keyfile = file_name ou /Key = contents_of_file.

acesso à rede tooenable para Olá Olá usuário deve desligar emulador de saudação e excluir o diretório de dados do emulador hello (C:\Users\user_name\AppData\Local\CosmosDBEmulator).

## <a name="developing-with-hello-emulator"></a>Desenvolvendo com hello emulador
Depois de você ter hello emulador Cosmos banco de dados do Azure em execução em sua área de trabalho, você pode usar qualquer suporte [banco de dados do SDK do Azure Cosmos](documentdb-sdk-dotnet.md) ou hello [API de REST do banco de dados do Azure Cosmos](/rest/api/documentdb/) toointeract com hello emulador. Olá emulador do Azure Cosmos DB também inclui um Gerenciador de dados interno que permite que você crie coleções para Olá documentos e MongoDB APIs e exibir e editar documentos sem gravar qualquer código.   

    // Connect toohello Azure Cosmos DB Emulator running locally
    DocumentClient client = new DocumentClient(
        new Uri("https://localhost:8081"), 
        "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==");

Se você estiver usando [o banco de dados do Azure Cosmos suporte de protocolo para o MongoDB](mongodb-introduction.md), use Olá cadeia de caracteres de conexão a seguir:

    mongodb://localhost:C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==@localhost:10255/admin?ssl=true&3t.sslSelfSignedCerts=true

Você pode usar as ferramentas existentes como [Studio do Azure DocumentDB](https://github.com/mingaliu/DocumentDBStudio) tooconnect toohello emulador do Azure Cosmos banco de dados. Também é possível migrar dados entre hello Azure Cosmos DB emulador e serviço de banco de dados do Azure Cosmos hello usando Olá [ferramenta de migração de dados de banco de dados do Azure Cosmos](https://github.com/azure/azure-documentdb-datamigrationtool).

> [!NOTE] 
> Se você iniciou o emulador de saudação com hello opção /Key, use a tecla Olá gerado em vez de "C2y6yDjf5 Relational + ob0N8A7Cgv30VRDJIWEHLM + 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw = ="

Usando o emulador do Windows Azure Cosmos DB hello, por padrão, você pode criar coleções com uma partição única too25 ou 1 coleção particionada. Para obter mais informações sobre como alterar esse valor, consulte [configuração Olá PartitionCount valor](#set-partitioncount).

## <a name="export-hello-ssl-certificate"></a>Exportar o certificado SSL Olá

Linguagens .NET e o tempo de execução use Olá repositório de certificados do Windows toosecurely conectam emulador local do banco de dados do Azure Cosmos toohello. Outras linguagens têm seu próprio método de gerenciar e usar certificados. O Java usa seu próprio [repositório de certificados](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) enquanto o Python usa [wrappers de soquete](https://docs.python.org/2/library/ssl.html).

Em ordem tooobtain toouse um certificado com linguagens e tempos de execução que não integram Olá repositório de certificados do Windows você precisará tooexport usando Olá Gerenciador de certificados do Windows. Você pode iniciá-lo executando certlm.msc ou siga as instruções passo a passo de saudação em [exportar hello Azure Cosmos DB emulador certificados](./local-emulator-export-ssl-certificates.md). Quando o Gerenciador de certificados Olá estiver em execução, abra Olá pessoal de certificados conforme mostrado abaixo e exportar Olá certificado com o nome amigável do hello "DocumentDBEmulatorCertificate" como o arquivo de x. 509 (. cer) codificado em BASE 64.

![Certificado SSL do emulador local do Azure Cosmos DB](./media/local-emulator/database-local-emulator-ssl_certificate.png)

certificado x. 509 de saudação pode ser importado para o repositório de certificados do Java hello, seguindo as instruções de saudação do [adicionando um toohello certificado repositório de certificados de autoridade de certificação de Java](https://docs.microsoft.com/azure/java-add-certificate-ca-store). Depois que o certificado Olá é importado no repositório de certificados Olá, aplicativos Java e MongoDB será toohello tooconnect capaz de emulador do Azure Cosmos banco de dados.

Ao conectar o emulador toohello de Python e Node.js SDKs, verificação de SSL está desabilitada.

## <a id="command-line"></a>Referência da ferramenta de linha de comando
Do local de instalação Olá, você pode usar Olá toostart de linha de comando e interromper o emulador de saudação, configurar opções e executar outras operações.

### <a name="command-line-syntax"></a>Sintaxe da linha de comando

    CosmosDB.Emulator.exe [/Shutdown] [/DataPath] [/Port] [/MongoPort] [/DirectPorts] [/Key] [/EnableRateLimiting] [/DisableRateLimiting] [/NoUI] [/NoExplorer] [/?]

lista de saudação tooview de opções, digite `CosmosDB.Emulator.exe /?` no prompt de comando hello.

<table>
<tr>
  <td><strong>Opção</strong></td>
  <td><strong>Descrição</strong></td>
  <td><strong>Comando</strong></td>
  <td><strong>Argumentos</strong></td>
</tr>
<tr>
  <td>[No arguments]</td>
  <td>Inicia hello Azure Cosmos DB emulador com as configurações padrão.</td>
  <td>CosmosDB.Emulator.exe</td>
  <td></td>
</tr>
<tr>
  <td>[Ajuda]</td>
  <td>Exibe a lista de saudação do suporte para argumentos de linha de comando.</td>
  <td>CosmosDB.Emulator.exe /?</td>
  <td></td>
</tr>
<tr>
  <td>Shutdown</td>
  <td>Olá emulador do Azure Cosmos banco de dados é desligado.</td>
  <td>CosmosDB.Emulator.exe /Shutdown</td>
  <td></td>
</tr>
<tr>
  <td>DataPath</td>
  <td>Especifica o caminho de saudação em quais arquivos de dados toostore. O padrão é %LocalAppdata%\CosmosDBEmulator.</td>
  <td>CosmosDB.Emulator.exe /DataPath=&lt;datapath&gt;</td>
  <td>&lt;datapath&gt;: um caminho acessível</td>
</tr>
<tr>
  <td>Porta</td>
  <td>Especifica o toouse de número de porta Olá emulador do Windows hello.  O padrão é 8081.</td>
  <td>CosmosDB.Emulator.exe /Port=&lt;porta&gt;</td>
  <td>&lt;port&gt;: único número de porta</td>
</tr>
<tr>
  <td>MongoPort</td>
  <td>Especifica o toouse de número de porta Olá para fins de compatibilidade do MongoDB API. O padrão é 10255.</td>
  <td>CosmosDB.Emulator.exe /MongoPort=&lt;mongoport&gt;</td>
  <td>&lt;mongoport&gt;: único número de porta</td>
</tr>
<tr>
  <td>DirectPorts</td>
  <td>Especifica a saudação toouse de portas para conectividade direta. Os padrões são 10251,10252,10253,10254.</td>
  <td>CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</td>
  <td>&lt;directports&gt;: lista de 4 portas delimitadas por vírgula</td>
</tr>
<tr>
  <td>Chave</td>
  <td>Chave de autorização para o emulador de saudação. Chave deve ser Olá codificação de base 64 de um vetor de 64 bytes.</td>
  <td>CosmosDB.Emulator.exe /Key:&lt;chave&gt;</td>
  <td>&lt;chave&gt;: chave deve ser Olá codificação de base 64 de um vetor de 64 bits</td>
</tr>
<tr>
  <td>EnableRateLimiting</td>
  <td>Especifica que o comportamento de limitação da taxa de solicitação está habilitado.</td>
  <td>CosmosDB.Emulator.exe /EnableRateLimiting</td>
  <td></td>
</tr>
<tr>
  <td>DisableRateLimiting</td>
  <td>Especifica que o comportamento de limitação da taxa de solicitação está desabilitado.</td>
  <td>CosmosDB.Emulator.exe /DisableRateLimiting</td>
  <td></td>
</tr>
<tr>
  <td>NoUI</td>
  <td>Não mostre o emulador Olá interface do usuário.</td>
  <td>CosmosDB.Emulator.exe /NoUI</td>
  <td></td>
</tr>
<tr>
  <td>NoExplorer</td>
  <td>Não mostra o gerenciador de documentos na inicialização.</td>
  <td>CosmosDB.Emulator.exe /NoExplorer</td>
  <td></td>
</tr>
<tr>
  <td>PartitionCount</td>
  <td>Especifica o número máximo de saudação de coleções particionadas. Consulte [alterar número de saudação de coleções](#set-partitioncount) para obter mais informações.</td>
  <td>CosmosDB.Emulator.exe /PartitionCount=&lt;partitioncount&gt;</td>
  <td>&lt;contagemdepartições&gt;: número máximo permitido de coleções de partição única. O padrão é 25. O máximo permitido é 250.</td>
</tr>
<tr>
  <td>DefaultPartitionCount</td>
  <td>Especifica o número de partições para uma coleção particionada padrão de saudação.</td>
  <td>CosmosDB.Emulator.exe /DefaultPartitionCount=&lt;defaultpartitioncount&gt;</td>
  <td>&lt;defaultpartitioncount&gt; O padrão é 25.</td>
</tr>
<tr>
  <td>AllowNetworkAccess</td>
  <td>Permite acessar emulador toohello em uma rede. Você também deve transmitir /Key =&lt;key_string&gt; ou /KeyFile =&lt;file_name&gt; tooenable acesso à rede.</td>
  <td>CosmosDB.Emulator.exe /AllowNetworkAccess /Key=&lt;key_string&gt;<br><br>ou o<br><br>CosmosDB.Emulator.exe /AllowNetworkAccess /KeyFile=&lt;file_name&gt;</td>
  <td></td>
</tr>
<tr>
  <td>NoFirewall</td>
  <td>Não ajuste as regras de firewall quando /AllowNetworkAccess for usado.</td>
  <td>CosmosDB.Emulator.exe /NoFirewall</td>
  <td></td>
</tr>
<tr>
  <td>GenKeyFile</td>
  <td>Gere uma nova chave de autorização e salve o arquivo especificado toohello. chave de saudação gerada pode ser usada com hello /Key ou /KeyFile opções.</td>
  <td>CosmosDB.Emulator.exe /GenKeyFile =&lt;caminho tookey arquivo&gt;</td>
  <td></td>
</tr>
<tr>
  <td>Consistência</td>
  <td>Defina o nível de consistência do hello padrão para a conta de saudação.</td>
  <td>CosmosDB.Emulator.exe /Consistency=&lt;consistência&gt;</td>
  <td>&lt;consistência&gt;: valor deve ser um dos seguintes Olá [níveis de consistência](consistency-levels.md): BoundedStaleness, forte, Eventual ou sessão.  valor padrão de saudação é a sessão.</td>
</tr>
<tr>
  <td>?</td>
  <td>Mostre mensagem de saudação do ajuda.</td>
  <td></td>
  <td></td>
</tr>
</table>

## <a name="differences-between-hello-azure-cosmos-db-emulator-and-azure-cosmos-db"></a>Diferenças entre hello Azure Cosmos DB emulador e o banco de dados do Azure Cosmos 
Como hello Azure Cosmos DB emulador fornece um ambiente emulado em execução em uma estação de trabalho de desenvolvedor local, existem algumas diferenças na funcionalidade entre emulador hello e uma conta de banco de dados do Azure Cosmos na nuvem hello:

* Hello Azure Cosmos DB emulador dá suporte a apenas uma única conta fixa e uma chave mestra conhecida.  Regeneração da chave não é possível em hello Azure Cosmos DB emulador.
* Hello Azure Cosmos DB emulador não é um serviço escalonável e não oferecerão suporte a um grande número de coleções.
* Hello Azure Cosmos DB emulador não simular diferentes [níveis de consistência do banco de dados do Azure Cosmos](consistency-levels.md).
* Hello Azure Cosmos DB emulador não simular [várias regiões replicação](distribute-data-globally.md).
* Olá emulador do Azure Cosmos banco de dados não oferece suporte a substituições de cota de serviço Olá que estão disponíveis no serviço de banco de dados do Azure Cosmos hello (por exemplo, limites de tamanho do documento, armazenamento maior coleção particionada).
* Como a cópia do hello Azure Cosmos DB emulador pode não ser backup toodate com alterações mais recentes de saudação com o serviço de banco de dados do Azure Cosmos hello, por favor [Planejador de capacidade do banco de dados do Azure Cosmos](https://www.documentdb.com/capacityplanner) taxa de transferência da produção de estimativa tooaccurately (RUs) necessidades do seu aplicativo.

## <a id="set-partitioncount"></a>Alterar o número de saudação de coleções

Por padrão, você pode criar coleções com uma partição única too25 ou 1 coleção particionada usando hello Azure Cosmos DB emulador. Modificando Olá **PartitionCount** valor, você pode criar coleções com uma partição única too250 ou 10 coleções particionadas, ou qualquer combinação de saudação duas que não excedam único 250 partições (onde 1 particionados coleção = 25 coleção de partição única).

Se você tentar toocreate uma coleção depois que a contagem de partição atual Olá foi excedida, o emulador Olá lança uma exceção de ServiceUnavailable, com a seguinte mensagem de saudação.

    Sorry, we are currently experiencing high demand in this region, 
    and cannot fulfill your request at this time. We work continuously 
    toobring more and more capacity online, and encourage you tootry again. 
    Please do not hesitate tooemail docdbswat@microsoft.com at any time or 
    for any reason. ActivityId: 29da65cc-fba1-45f9-b82c-bf01d78a1f91

número de saudação do toochange de coleções disponíveis toohello Azure Cosmos DB Emulator, Olá a seguir:

1. Exclua todos os dados locais do emulador do Azure Cosmos DB clicando Olá **emulador de banco de dados do Azure Cosmos** ícone na bandeja do sistema hello e, em seguida, clicando em **Redefinir dados...** .
2. Exclua todos os dados de emulador desta pasta C:\Users\user_name\AppData\Local\CosmosDBEmulator.
3. Saia de todas as instâncias abertas clicando Olá **emulador de banco de dados do Azure Cosmos** ícone na bandeja do sistema hello e, em seguida, clicando em **saída**. Pode levar um minuto para tooexit de todas as instâncias.
4. Instale a versão mais recente Olá de saudação [emulador de banco de dados do Azure Cosmos](https://aka.ms/cosmosdb-emulator).
5. Iniciar o emulador de saudação com hello sinalizador PartitionCount definindo um valor < = 250. Por exemplo: `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.

## <a name="troubleshooting"></a>Solucionar problemas

Use Olá dicas toohelp solucionar problemas encontrados com o emulador do Azure Cosmos DB Olá a seguir:

- Se você instalou uma nova versão do emulador de saudação e houver erros, certifique-se de que redefinir os dados. Você pode redefinir os dados clicando hello Azure Cosmos DB emulador ícone na bandeja do sistema hello e, em seguida, clicando em Redefinir dados... Se isso não resolver erros de saudação, você pode desinstalar e reinstalar o aplicativo hello. Consulte [desinstalar um emulador local Olá](#uninstall) para obter instruções.

- Se o emulador do Azure Cosmos DB Olá falhar, coletar arquivos de despejo da pasta c:\Users\user_name\AppData\Local\CrashDumps, compactá-los e anexá-los tooan email muito[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).

- Se você enfrentar falhas em CosmosDB.StartupEntryPoint.exe, execute Olá comando a seguir em um prompt de comando do administrador:`lodctr /R` 

- Se você encontrar um problema de conectividade, [coletar arquivos de rastreamento](#trace-files), compactá-los e anexá-los email tooan muito[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).

- Se você receber um **serviço indisponível** mensagem, hello emulador poderia estar falhando tooinitialize da pilha de rede hello. Toosee de seleção se você tiver Olá Pulse secure cliente ou Juniper redes cliente instalado, como drivers de filtro de rede podem causar um problema de saudação. A desinstalação de drivers de filtro de rede de terceiros geralmente corrige o problema de saudação.

### <a id="trace-files"></a>Coletar arquivos de rastreamento

toocollect depuração rastreamentos, executados Olá comandos a seguir em um prompt de comando administrativo:

1. `cd /d "%ProgramFiles%\Azure Cosmos DB Emulator"`
2. `CosmosDB.Emulator.exe /shutdown`. Inspecionar Olá bandeja toomake se Olá programa do sistema foi desligado, pode levar um minuto. Você também pode simplesmente clicar **Exit** na interface de usuário do hello Azure Cosmos DB emulador.
3. `CosmosDB.Emulator.exe /starttraces`
4. `CosmosDB.Emulator.exe`
5. Reproduza o problema de saudação. Se o Gerenciador de dados não está funcionando, você só precisa toowait para Olá navegador tooopen para alguns erros de saudação do toocatch segundos.
5. `CosmosDB.Emulator.exe /stoptraces`
6. Navegue muito`%ProgramFiles%\Azure Cosmos DB Emulator` e localizar o arquivo de docdbemulator_000001.etl hello.
7. Envie o arquivo de ETL de saudação junto com as etapas de reprodução muito[ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com) para depuração.

### <a id="uninstall"></a>Desinstalar Olá emulador local

1. Saia de todas as instâncias abertas do hello emulador local clicando duas vezes o ícone do emulador do Azure Cosmos DB Olá na bandeja do sistema Olá, e, em seguida, clicar em Sair. Pode levar um minuto para tooexit de todas as instâncias.
2. Na caixa de pesquisa do Windows hello, digite **aplicativos e recursos** e clique em Olá **aplicativos e recursos (configurações do sistema)** resultados.
3. Na lista de saudação de aplicativos, vá muito**emulador de banco de dados do Azure Cosmos**, selecioná-la, clique em **desinstalação**, em seguida, confirme e clique em **desinstalação** novamente.
4. Quando o aplicativo hello é desinstalado, navegue tooC:\Users\<usuário > \AppData\Local\CosmosDBEmulator e excluir a pasta de saudação. 

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você fez a seguir hello:

> [!div class="checklist"]
> * Instalado Olá emulador local
> * Saudação de RAND emulador no Docker para Windows
> * Autenticou solicitações
> * Usado Olá Explorador de dados em Olá emulador
> * Exportou certificados SSL
> * Chamado hello emulador da linha de comando Olá
> * Coletou arquivos de rastreamento

Neste tutorial, você aprendeu como toouse Olá emulador local para local de desenvolvimento gratuito. Agora você pode continuar tutorial próxima toohello e aprender como certificados de emulador SSL tooexport. 

> [!div class="nextstepaction"]
> [Exportar certificados de emulador do Azure Cosmos DB Olá](local-emulator-export-ssl-certificates.md)
