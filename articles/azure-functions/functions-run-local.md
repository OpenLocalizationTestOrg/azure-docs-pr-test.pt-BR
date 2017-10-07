---
title: "aaaDevelop e execução do Azure funciona localmente | Microsoft Docs"
description: "Saiba como toocode e teste do Azure funciona no computador local antes de executá-los em funções do Azure."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
ms.assetid: 242736be-ec66-4114-924b-31795fd18884
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: multiple
ms.topic: article
ms.date: 07/12/2017
ms.author: glenga
ms.openlocfilehash: 342ed4d6df41a2d2df9067948e19e347bb52c844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="code-and-test-azure-functions-locally"></a>Como codificar e testar o Azure Functions localmente

Durante a saudação [portal do Azure] fornece um conjunto completo de ferramentas para desenvolvimento e teste funções do Azure, muitos desenvolvedores preferem uma experiência de desenvolvimento local. As funções do Azure torna fácil toouse seus favoritos toodevelop de ferramentas de desenvolvimento local e de editor de código e teste suas funções no computador local. As funções podem disparar eventos no Azure e você pode depurar o as funções de C# e JavaScript em seu computador local. 

Se você for um desenvolvedor de C# no Visual Studio, o Azure Functions também [se integrará ao Visual Studio de 2017](functions-develop-vs.md).

## <a name="install-hello-azure-functions-core-tools"></a>Instalar as ferramentas de núcleo de funções hello Azure

Ferramentas de núcleo de funções do Azure é uma versão local do tempo de execução de funções do Azure Olá que podem ser executados no computador local do Windows. Não é um simulador ou emulador. Ele tem Olá em tempo de execução mesmo que liga funções no Azure.

Olá [Azure funções principais ferramentas] é fornecido como um pacote de npm. Você deve primeiro [instalar o NodeJS](https://docs.npmjs.com/getting-started/installing-node), que inclui npm.  

>[!NOTE]
>Neste momento, o pacote de ferramentas do Azure funções principais de Olá só pode ser instalado em computadores com Windows. Essa restrição é devido a limitação temporária tooa no host de funções hello.

[Ferramentas de núcleo de funções do Azure] adiciona Olá aliases de comando a seguir:
* **func**
* **azfun**
* **azurefunctions**

Todos esses alias podem ser usados em vez de `func` mostrado nos exemplos de saudação neste tópico.

## <a name="create-a-local-functions-project"></a>Criar um projeto de funções local

Quando em execução localmente, um projeto de funções é um diretório com local.settings.json e Olá arquivos host.json. Esse diretório é Olá equivalente de um aplicativo de função no Azure. toolearn mais sobre Olá estrutura de pastas de funções do Azure, consulte Olá [guia de desenvolvedores do Azure funções](functions-reference.md#folder-structure).

Em um prompt de comando, execute Olá comando a seguir:

```
func init MyFunctionProj
```

saída de Hello aparência Olá exemplo a seguir:

```
Writing .gitignore
Writing host.json
Writing local.settings.json
Created launch.json
Initialized empty Git repository in D:/Code/Playground/MyFunctionProj/.git/
```

tooopt fora da criação de um repositório Git, use a opção de saudação `--no-source-control [-n]`.

<a name="local-settings"></a>

## <a name="local-settings-file"></a>Arquivo de configurações local

Olá arquivo local.settings.json armazena configurações do aplicativo, cadeias de caracteres de conexão e as configurações para as ferramentas de núcleo de funções do Azure. Ele tem Olá estrutura a seguir:

```json
{
  "IsEncrypted": false,   
  "Values": {
    "AzureWebJobsStorage": "<connection string>", 
    "AzureWebJobsDashboard": "<connection string>", 
  },
  "Host": {
    "LocalHttpPort": 7071, 
    "CORS": "*" 
  },
  "ConnectionStrings": {
    "SQLConnectionString": "Value"
  }
}
```
| Configuração      | Descrição                            |
| ------------ | -------------------------------------- |
| **IsEncrypted** | Quando definido muito**true**, todos os valores são criptografados usando uma chave de computador local. Usado com `func settings` comandos. O valor padrão é **false**. |
| **Valores** | Coleção de configuração de aplicativo usada quando executada localmente. Adicione o objeto de toothis de configurações do aplicativo.  |
| **AzureWebJobsStorage** | Conjuntos de Olá toohello de cadeia de caracteres de conexão conta de armazenamento do Azure que é usada internamente pelo tempo de execução de funções do Azure hello. conta de armazenamento Olá dá suporte a gatilhos da função. Essa configuração de conexão de conta de armazenamento é necessária para todas as funções, exceto para as funções HTTP acionadas.  |
| **AzureWebJobsDashboard** | Define Olá conexão cadeia de caracteres toohello armazenamento do Azure conta é usada toostore Olá função logs. Esse valor opcional torna os logs de saudação acessível no portal de saudação.|
| **Host** | Configurações nesta seção personalizar o processo de host de funções hello quando em execução localmente. | 
| **LocalHttpPort** | Conjuntos de hello a porta padrão usada ao executar o host local de funções hello (`func host start` e `func run`). Olá `--port` opção de linha de comando tem precedência sobre esse valor. |
| **CORS** | Define as origens de saudação permitidas para [recursos entre origens (CORS) de compartilhamento](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing). As origens são fornecidas como uma lista separada por vírgulas, sem espaços. Olá valor curinga (**\***) tem suporte, que permite que as solicitações de qualquer origem. |
| **ConnectionStrings** | Contém cadeias de conexão de banco de dados de saudação para suas funções. Cadeias de caracteres de Conexão no objeto são adicionadas toohello ambiente com o tipo de provedor de saudação do **SqlClient**.  | 

A maioria dos disparadores e associações não têm um **Conexão** propriedade que mapeia o nome de uma configuração de aplicativo ou a variável de ambiente toohello. Para cada propriedade de conexão, deve haver uma configuração de aplicativo definida no arquivo local.settings.json. 

Essas configurações também podem ser lidas em seu código como variáveis de ambiente. No C#, use [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) ou [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx). No JavaScript, use `process.env`. As configurações especificadas como uma variável de ambiente do sistema têm precedência sobre valores no arquivo de local.settings.json hello. 

As configurações no arquivo de local.settings.json Olá só são usadas por ferramentas de funções quando em execução localmente. Por padrão, essas configurações não são migradas automaticamente quando o projeto de saudação é tooAzure publicado. Saudação de uso `--publish-local-settings` alternar [quando você publica](#publish) toomake-se de que essas configurações são adicionadas toohello função aplicativo no Azure.

Quando nenhuma cadeia de caracteres de conexão de armazenamento válido é definida para **AzureWebJobsStorage**, Olá a seguinte mensagem de erro é exibida:  

>Valor ausente para AzureWebJobsStorage em local.settings.json. Isso é necessário para todos os gatilhos diferentes de HTTP. Você pode executar 'func azure functionary fetch-app-settings <functionAppName>' ou especificar uma cadeia de conexão em local.settings.json.
  
[!INCLUDE [Note toonot use local storage](../../includes/functions-local-settings-note.md)]

### <a name="configure-app-settings"></a>Definir configurações de aplicativo

tooset um valor para cadeias de caracteres de conexão, você pode fazer um dos seguintes hello:
* Insira a cadeia de caracteres de conexão de saudação do [Azure Storage Explorer](http://storageexplorer.com/).
* Use uma saudação comandos a seguir:

    ```
    func azure functionapp fetch-app-settings <FunctionAppName>
    ```
    ```
    func azure functionapp storage fetch-connection-string <StorageAccountName>
    ```
    Os dois comandos exigem que você toofirst entrar tooAzure.

## <a name="create-a-function"></a>Criar uma função

toocreate uma função, execute Olá comando a seguir:

```
func new
``` 
`func new`Olá dá suporte a argumentos opcionais a seguir:

| Argumento     | Descrição                            |
| ------------ | -------------------------------------- |
| **`--language -l`** | modelo de saudação linguagem de programação, como c#, F # ou JavaScript. |
| **`--template -t`** | nome do modelo de saudação. |
| **`--name -n`** | nome da função Hello. |

Por exemplo, toocreate um gatilho de HTTP de JavaScript, execute:

```
func new --language JavaScript --template HttpTrigger --name MyHttpTrigger
```

toocreate uma função disparado em fila, execute:

```
func new --language JavaScript --template QueueTrigger --name QueueTriggerJS
```

## <a name="run-functions-locally"></a>Executar funções localmente

toorun um projeto de funções, executar o host de funções hello. o host de saudação permite que gatilhos para todas as funções no projeto hello:

```
func host start
```

`func host start`dá suporte a saudação as opções a seguir:

| Opção     | Descrição                            |
| ------------ | -------------------------------------- |
|**`--port -p`** | Olá toolisten de porta local no. Valor Padrão: 7071. |
| **`--debug <type>`** | Opções de saudação são `VSCode` e `VS`. |
| **`--cors`** | Uma lista separada por vírgulas de origens CORS, sem espaços. |
| **`--nodeDebugPort -n`** | porta Olá Olá nó depurador toouse. Padrão: um valor de launch.json ou 5858. |
| **`--debugLevel -d`** | nível de rastreamento do console Hello (desativado, detalhado, informações, aviso ou erro). Padrão: informações.|
| **`--timeout -t`** | Olá tempo limite para Olá funções host para iniciar, em segundos. Padrão: 20 segundos.|
| **`--useHttps`** | Associar toohttps://localhost: {porta} em vez de toohttp://localhost: {port}. Por padrão, essa opção cria um certificado confiável no computador.|
| **`--pause-on-error`** | Pausar para entrada adicional antes de sair do processo de saudação. Útil ao iniciar as ferramentas básicas do Azure Functions de um ambiente de desenvolvimento integrado (IDE).|

Quando o host de funções hello é iniciado, ele produz funções disparou a URL de HTTP do hello:

```
Found hello following functions:
Host.Functions.MyHttpTrigger

ob host started
Http Function MyHttpTrigger: http://localhost:7071/api/MyHttpTrigger
```

### <a name="debug-in-vs-code-or-visual-studio"></a>Depurar no VSCode ou no Visual Studio

tooattach um depurador passar Olá `--debug` argumento. funções em JavaScript toodebug, use o código do Visual Studio. Para funções C#, use o Visual Studio.

funções toodebug c#, use `--debug vs`. Você também pode usar as [Ferramentas do Visual Studio 2017 no Azure Functions](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/). 

host de saudação toolaunch e configure a depuração de JavaScript, execute:

```
func host start --debug vscode
```

Em seguida, no código do Visual Studio, no hello **depurar** exibição, selecione **anexar tooAzure funções**. Você pode anexar os pontos de interrupção, inspecionar variáveis e o código por etapas.

![Depuração de JavaScript com o Visual Studio Code](./media/functions-run-local/vscode-javascript-debugging.png)

### <a name="passing-test-data-tooa-function"></a>Função de tooa de dados de teste de passagem

Você também pode chamar uma função diretamente por meio de `func run <FunctionName>` e fornecer dados de entrada para a função hello. Esse comando é semelhante toorunning uma função usando Olá **teste** guia Olá portal do Azure. Esse comando inicia o host de funções toda hello.

`func run`dá suporte a saudação as opções a seguir:

| Opção     | Descrição                            |
| ------------ | -------------------------------------- |
| **`--content -c`** | Conteúdo embutido. |
| **`--debug -d`** | Anexe um processo de host do depurador toohello antes de executar a função hello.|
| **`--timeout -t`** | Toowait de tempo (em segundos) até que o host local de funções hello está pronto.|
| **`--file -f`** | Olá toouse de nome de arquivo como conteúdo.|
| **`--no-interactive`** | Não solicitará a entrada. Útil para cenários de automação.|

Por exemplo, toocall uma função disparado por HTTP e corpo de conteúdo de passagem, execute Olá comando a seguir:

```
func run MyHttpTrigger -c '{\"name\": \"Azure\"}'
```

## <a name="publish"></a>Publicar tooAzure

toopublish um aplicativo de função funções projeto tooa no Azure, use Olá `publish` comando:

```
func azure functionapp publish <FunctionAppName>
```

Você pode usar o hello as opções a seguir:

| Opção     | Descrição                            |
| ------------ | -------------------------------------- |
| **`--publish-local-settings -i`** |  Configurações de publicação no local.settings.json tooAzure, solicitando toooverwrite se Olá configuração já existe.|
| **`--overwrite-settings -y`** | Deve ser usada com `-i`. Substitui o AppSettings no Azure com o valor local se for diferente. O padrão é solicitado.|

Olá `publish` comando carrega o conteúdo de saudação do diretório do projeto funções hello. Se você excluir arquivos localmente, Olá `publish` comando não os exclui do Azure. Você pode excluir arquivos no Azure usando Olá [ferramenta Kudu](functions-how-to-use-azure-function-app-settings.md#kudu) em Olá [portal do Azure].

## <a name="next-steps"></a>Próximas etapas

As principais ferramentas do Azure Functions são [Código-fonte aberto e hospedado no GitHub](https://github.com/azure/azure-functions-cli).  
toofile uma solicitação de bug ou recurso, [abrir um problema do GitHub](https://github.com/azure/azure-functions-cli/issues). 

<!-- LINKS -->

[Ferramentas básicas do Azure Functions]: https://www.npmjs.com/package/azure-functions-core-tools
[Portal do Azure]: https://portal.azure.com 
