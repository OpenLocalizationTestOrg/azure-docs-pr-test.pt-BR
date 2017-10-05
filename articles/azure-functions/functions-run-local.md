---
title: "Desenvolver e executar funções do Azure localmente | Microsoft Docs"
description: "Saiba como codificar e testar o Azure Functions no computador local antes de executá-las no Azure Functions."
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
ms.openlocfilehash: bbe03973dbd7c70463caa6d1a45efae2ec722c05
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="code-and-test-azure-functions-locally"></a><span data-ttu-id="c74ad-103">Como codificar e testar o Azure Functions localmente</span><span class="sxs-lookup"><span data-stu-id="c74ad-103">Code and test Azure functions locally</span></span>

<span data-ttu-id="c74ad-104">Enquanto o [Portal do Azure] fornece um conjunto completo de ferramentas para desenvolvimento e teste do Azure Functions, muitos desenvolvedores preferem uma experiência de desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="c74ad-104">While the [Azure portal] provides a full set of tools for developing and testing Azure Functions, many developers prefer a local development experience.</span></span> <span data-ttu-id="c74ad-105">O Azure Functions facilita a utilização do seu editor de códigos favorito e das ferramentas de desenvolvimento locais para desenvolver e testar as funções em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="c74ad-105">Azure Functions makes it easy to use your favorite code editor and local development tools to develop and test your functions on your local computer.</span></span> <span data-ttu-id="c74ad-106">As funções podem disparar eventos no Azure e você pode depurar o as funções de C# e JavaScript em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="c74ad-106">Your functions can trigger on events in Azure, and you can debug your C# and JavaScript functions on your local computer.</span></span> 

<span data-ttu-id="c74ad-107">Se você for um desenvolvedor de C# no Visual Studio, o Azure Functions também [se integrará ao Visual Studio de 2017](functions-develop-vs.md).</span><span class="sxs-lookup"><span data-stu-id="c74ad-107">If you are a Visual Studio C# developer, Azure Functions also [integrates with Visual Studio 2017](functions-develop-vs.md).</span></span>

## <a name="install-the-azure-functions-core-tools"></a><span data-ttu-id="c74ad-108">Instalação das ferramentas básicas do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="c74ad-108">Install the Azure Functions Core Tools</span></span>

<span data-ttu-id="c74ad-109">As Ferramentas básicas do Azure Functions são uma versão local do tempo de execução do Azure Functions que pode ser executada no computador local do Windows.</span><span class="sxs-lookup"><span data-stu-id="c74ad-109">Azure Functions Core Tools is a local version of the Azure Functions runtime that you can run on your local Windows computer.</span></span> <span data-ttu-id="c74ad-110">Não é um simulador ou emulador.</span><span class="sxs-lookup"><span data-stu-id="c74ad-110">It's not an emulator or simulator.</span></span> <span data-ttu-id="c74ad-111">É o mesmo tempo de execução que potencializa as funções no Azure.</span><span class="sxs-lookup"><span data-stu-id="c74ad-111">It's the same runtime that powers Functions in Azure.</span></span>

<span data-ttu-id="c74ad-112">As [ferramentas básicas do Azure Functions] são fornecidas como um pacote de npm.</span><span class="sxs-lookup"><span data-stu-id="c74ad-112">The [Azure Functions Core Tools] is provided as an npm package.</span></span> <span data-ttu-id="c74ad-113">Você deve primeiro [instalar o NodeJS](https://docs.npmjs.com/getting-started/installing-node), que inclui npm.</span><span class="sxs-lookup"><span data-stu-id="c74ad-113">You must first [install NodeJS](https://docs.npmjs.com/getting-started/installing-node), which includes npm.</span></span>  

>[!NOTE]
><span data-ttu-id="c74ad-114">Neste momento, o pacote de ferramentas básicas do Azure Functions só pode ser instalado em computadores Windows.</span><span class="sxs-lookup"><span data-stu-id="c74ad-114">At this time, the Azure Functions Core Tools package can only be installed on Windows computers.</span></span> <span data-ttu-id="c74ad-115">Essa restrição é devido a uma limitação temporária no host do Functions.</span><span class="sxs-lookup"><span data-stu-id="c74ad-115">This restriction is due to a temporary limitation in the Functions host.</span></span>

<span data-ttu-id="c74ad-116">[ferramentas básicas do Azure Functions] adicionam os aliases de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="c74ad-116">[Azure Functions Core Tools] adds the following command aliases:</span></span>
* <span data-ttu-id="c74ad-117">**func**</span><span class="sxs-lookup"><span data-stu-id="c74ad-117">**func**</span></span>
* <span data-ttu-id="c74ad-118">**azfun**</span><span class="sxs-lookup"><span data-stu-id="c74ad-118">**azfun**</span></span>
* <span data-ttu-id="c74ad-119">**azurefunctions**</span><span class="sxs-lookup"><span data-stu-id="c74ad-119">**azurefunctions**</span></span>

<span data-ttu-id="c74ad-120">Todos esses alias podem ser usados em vez de `func` mostrado nos exemplos neste tópico.</span><span class="sxs-lookup"><span data-stu-id="c74ad-120">All of these alias can be used instead of `func` shown in the examples in this topic.</span></span>

## <a name="create-a-local-functions-project"></a><span data-ttu-id="c74ad-121">Criar um projeto de funções local</span><span class="sxs-lookup"><span data-stu-id="c74ad-121">Create a local Functions project</span></span>

<span data-ttu-id="c74ad-122">Quando estiver em execução localmente, um projeto de funções é um diretório que tem os arquivos host.json e local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="c74ad-122">When running locally, a Functions project is a directory that has the files host.json and local.settings.json.</span></span> <span data-ttu-id="c74ad-123">Esse diretório é o equivalente ao de um aplicativo de funções no Azure.</span><span class="sxs-lookup"><span data-stu-id="c74ad-123">This directory is the equivalent of a function app in Azure.</span></span> <span data-ttu-id="c74ad-124">Para saber mais sobre a estrutura de pastas do Azure Functions, consulte o [guia de desenvolvedores do Azure Functions](functions-reference.md#folder-structure).</span><span class="sxs-lookup"><span data-stu-id="c74ad-124">To learn more about the Azure Functions folder structure, see the [Azure Functions developers guide](functions-reference.md#folder-structure).</span></span>

<span data-ttu-id="c74ad-125">No prompt de comando, execute o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="c74ad-125">At a command prompt, run the following command:</span></span>

```
func init MyFunctionProj
```

<span data-ttu-id="c74ad-126">A saída se parece com o seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="c74ad-126">The output looks like the following example:</span></span>

```
Writing .gitignore
Writing host.json
Writing local.settings.json
Created launch.json
Initialized empty Git repository in D:/Code/Playground/MyFunctionProj/.git/
```

<span data-ttu-id="c74ad-127">Para recusar a criação de um repositório Git, use a opção `--no-source-control [-n]`.</span><span class="sxs-lookup"><span data-stu-id="c74ad-127">To opt out of creating a Git repository, use the option `--no-source-control [-n]`.</span></span>

<a name="local-settings"></a>

## <a name="local-settings-file"></a><span data-ttu-id="c74ad-128">Arquivo de configurações local</span><span class="sxs-lookup"><span data-stu-id="c74ad-128">Local settings file</span></span>

<span data-ttu-id="c74ad-129">O arquivo local.settings.json armazena as configurações do aplicativo, as cadeias de conexão e as configurações para as Ferramentas básicas do Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="c74ad-129">The file local.settings.json stores app settings, connection strings, and settings for Azure Functions Core Tools.</span></span> <span data-ttu-id="c74ad-130">Ele contém a seguinte estrutura:</span><span class="sxs-lookup"><span data-stu-id="c74ad-130">It has the following structure:</span></span>

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
| <span data-ttu-id="c74ad-131">Configuração</span><span class="sxs-lookup"><span data-stu-id="c74ad-131">Setting</span></span>      | <span data-ttu-id="c74ad-132">Descrição</span><span class="sxs-lookup"><span data-stu-id="c74ad-132">Description</span></span>                            |
| ------------ | -------------------------------------- |
| <span data-ttu-id="c74ad-133">**IsEncrypted**</span><span class="sxs-lookup"><span data-stu-id="c74ad-133">**IsEncrypted**</span></span> | <span data-ttu-id="c74ad-134">Quando definidos como **true**, todos os valores são criptografados usando uma chave de computador local.</span><span class="sxs-lookup"><span data-stu-id="c74ad-134">When set to **true**, all values are encrypted using a local machine key.</span></span> <span data-ttu-id="c74ad-135">Usado com `func settings` comandos.</span><span class="sxs-lookup"><span data-stu-id="c74ad-135">Used with `func settings` commands.</span></span> <span data-ttu-id="c74ad-136">O valor padrão é **false**.</span><span class="sxs-lookup"><span data-stu-id="c74ad-136">Default value is **false**.</span></span> |
| <span data-ttu-id="c74ad-137">**Valores**</span><span class="sxs-lookup"><span data-stu-id="c74ad-137">**Values**</span></span> | <span data-ttu-id="c74ad-138">Coleção de configuração de aplicativo usada quando executada localmente.</span><span class="sxs-lookup"><span data-stu-id="c74ad-138">Collection of application settings used when running locally.</span></span> <span data-ttu-id="c74ad-139">Adicione as configurações do aplicativo neste objeto.</span><span class="sxs-lookup"><span data-stu-id="c74ad-139">Add your application settings to this object.</span></span>  |
| <span data-ttu-id="c74ad-140">**AzureWebJobsStorage**</span><span class="sxs-lookup"><span data-stu-id="c74ad-140">**AzureWebJobsStorage**</span></span> | <span data-ttu-id="c74ad-141">Define a cadeia de conexão para a conta de armazenamento do Azure que é usada internamente pelo tempo de execução do Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="c74ad-141">Sets the connection string to the Azure Storage account that is used internally by the Azure Functions runtime.</span></span> <span data-ttu-id="c74ad-142">A conta de armazenamento dá suporte aos gatilhos da função.</span><span class="sxs-lookup"><span data-stu-id="c74ad-142">The storage account supports your function's triggers.</span></span> <span data-ttu-id="c74ad-143">Essa configuração de conexão de conta de armazenamento é necessária para todas as funções, exceto para as funções HTTP acionadas.</span><span class="sxs-lookup"><span data-stu-id="c74ad-143">This storage account connection setting is required for all functions except for HTTP triggered functions.</span></span>  |
| <span data-ttu-id="c74ad-144">**AzureWebJobsDashboard**</span><span class="sxs-lookup"><span data-stu-id="c74ad-144">**AzureWebJobsDashboard**</span></span> | <span data-ttu-id="c74ad-145">Define a cadeia de conexão para a conta de armazenamento do Azure que é usada para armazenar os logs de função.</span><span class="sxs-lookup"><span data-stu-id="c74ad-145">Sets the connection string to the Azure Storage account that is used to store the function logs.</span></span> <span data-ttu-id="c74ad-146">Esse valor opcional torna os logs acessíveis no portal.</span><span class="sxs-lookup"><span data-stu-id="c74ad-146">This optional value makes the logs accessible in the portal.</span></span>|
| <span data-ttu-id="c74ad-147">**Host**</span><span class="sxs-lookup"><span data-stu-id="c74ad-147">**Host**</span></span> | <span data-ttu-id="c74ad-148">As configurações nesta seção personalizam o processo de host do Functions quando executadas localmente.</span><span class="sxs-lookup"><span data-stu-id="c74ad-148">Settings in this section customize the Functions host process when running locally.</span></span> | 
| <span data-ttu-id="c74ad-149">**LocalHttpPort**</span><span class="sxs-lookup"><span data-stu-id="c74ad-149">**LocalHttpPort**</span></span> | <span data-ttu-id="c74ad-150">Define a porta padrão usada ao executar o host local do Functions (`func host start` e `func run`).</span><span class="sxs-lookup"><span data-stu-id="c74ad-150">Sets the default port used when running the local Functions host (`func host start` and `func run`).</span></span> <span data-ttu-id="c74ad-151">A opção de linha de comando `--port` tem precedência sobre esse valor.</span><span class="sxs-lookup"><span data-stu-id="c74ad-151">The `--port` command-line option takes precedence over this value.</span></span> |
| <span data-ttu-id="c74ad-152">**CORS**</span><span class="sxs-lookup"><span data-stu-id="c74ad-152">**CORS**</span></span> | <span data-ttu-id="c74ad-153">Define as origens permitidas para [CORS (Compartilhamento de recurso entre origens)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing).</span><span class="sxs-lookup"><span data-stu-id="c74ad-153">Defines the origins allowed for [cross-origin resource sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing).</span></span> <span data-ttu-id="c74ad-154">As origens são fornecidas como uma lista separada por vírgulas, sem espaços.</span><span class="sxs-lookup"><span data-stu-id="c74ad-154">Origins are supplied as a comma-separated list with no spaces.</span></span> <span data-ttu-id="c74ad-155">Há suporte para o valor do caractere curinga (**\***), que permite solicitações de qualquer origem.</span><span class="sxs-lookup"><span data-stu-id="c74ad-155">The wildcard value (**\***) is supported, which allows requests from any origin.</span></span> |
| <span data-ttu-id="c74ad-156">**ConnectionStrings**</span><span class="sxs-lookup"><span data-stu-id="c74ad-156">**ConnectionStrings**</span></span> | <span data-ttu-id="c74ad-157">Contém as cadeias de caracteres de conexão de banco de dados para suas funções.</span><span class="sxs-lookup"><span data-stu-id="c74ad-157">Contains the database connection strings for your functions.</span></span> <span data-ttu-id="c74ad-158">As cadeias de caracteres de conexão neste objeto são adicionadas ao ambiente com o tipo de provedor de **System.Data.SqlClient**.</span><span class="sxs-lookup"><span data-stu-id="c74ad-158">Connection strings in this object are added to the environment with the provider type of **System.Data.SqlClient**.</span></span>  | 

<span data-ttu-id="c74ad-159">A maioria dos gatilhos e associações têm uma propriedade **Conexão** que mapeia para o nome de uma variável de ambiente ou configuração de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c74ad-159">Most triggers and bindings have a **Connection** property that maps to the name of an environment variable or app setting.</span></span> <span data-ttu-id="c74ad-160">Para cada propriedade de conexão, deve haver uma configuração de aplicativo definida no arquivo local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="c74ad-160">For each connection property, there must be app setting defined in local.settings.json file.</span></span> 

<span data-ttu-id="c74ad-161">Essas configurações também podem ser lidas em seu código como variáveis de ambiente.</span><span class="sxs-lookup"><span data-stu-id="c74ad-161">These settings can also be read in your code as environment variables.</span></span> <span data-ttu-id="c74ad-162">No C#, use [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) ou [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="c74ad-162">In C#, use [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) or [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx).</span></span> <span data-ttu-id="c74ad-163">No JavaScript, use `process.env`.</span><span class="sxs-lookup"><span data-stu-id="c74ad-163">In JavaScript, use `process.env`.</span></span> <span data-ttu-id="c74ad-164">As configurações especificadas como uma variável de ambiente do sistema prevalecem sobre os valores no arquivo local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="c74ad-164">Settings specified as a system environment variable take precedence over values in the local.settings.json file.</span></span> 

<span data-ttu-id="c74ad-165">As configurações no arquivo local.settings.json só são usadas pelas ferramentas do Functions quando são executadas localmente.</span><span class="sxs-lookup"><span data-stu-id="c74ad-165">Settings in the local.settings.json file are only used by Functions tools when running locally.</span></span> <span data-ttu-id="c74ad-166">Por padrão, essas configurações não são migradas automaticamente quando o projeto é publicado no Azure.</span><span class="sxs-lookup"><span data-stu-id="c74ad-166">By default, these settings are not migrated automatically when the project is published to Azure.</span></span> <span data-ttu-id="c74ad-167">Use a opção `--publish-local-settings` [quando publicar](#publish) para se certificar de que essas configurações serão adicionadas ao aplicativo de funções no Azure.</span><span class="sxs-lookup"><span data-stu-id="c74ad-167">Use the `--publish-local-settings` switch [when you publish](#publish) to make sure these settings are added to the function app in Azure.</span></span>

<span data-ttu-id="c74ad-168">Se nenhuma cadeia de conexão de armazenamento válida for definida como **AzureWebJobsStorage**, a seguinte mensagem de erro será exibida:</span><span class="sxs-lookup"><span data-stu-id="c74ad-168">When no valid storage connection string is set for **AzureWebJobsStorage**, the following error message is shown:</span></span>  

><span data-ttu-id="c74ad-169">Valor ausente para AzureWebJobsStorage em local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="c74ad-169">Missing value for AzureWebJobsStorage in local.settings.json.</span></span> <span data-ttu-id="c74ad-170">Isso é necessário para todos os gatilhos diferentes de HTTP.</span><span class="sxs-lookup"><span data-stu-id="c74ad-170">This is required for all triggers other than HTTP.</span></span> <span data-ttu-id="c74ad-171">Você pode executar 'func azure functionary fetch-app-settings <functionAppName>' ou especificar uma cadeia de conexão em local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="c74ad-171">You can run 'func azure functionary fetch-app-settings <functionAppName>' or specify a connection string in local.settings.json.</span></span>
  
[!INCLUDE [Note to not use local storage](../../includes/functions-local-settings-note.md)]

### <a name="configure-app-settings"></a><span data-ttu-id="c74ad-172">Definir configurações de aplicativo</span><span class="sxs-lookup"><span data-stu-id="c74ad-172">Configure app settings</span></span>

<span data-ttu-id="c74ad-173">Para definir um valor para cadeias de conexão, você pode fazer o seguinte:</span><span class="sxs-lookup"><span data-stu-id="c74ad-173">To set a value for connection strings, you can do one of the following:</span></span>
* <span data-ttu-id="c74ad-174">Insira a cadeia de conexão do [Gerenciador de Armazenamento do Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="c74ad-174">Enter the connection string from [Azure Storage Explorer](http://storageexplorer.com/).</span></span>
* <span data-ttu-id="c74ad-175">Use um dos seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="c74ad-175">Use one of the following commands:</span></span>

    ```
    func azure functionapp fetch-app-settings <FunctionAppName>
    ```
    ```
    func azure functionapp storage fetch-connection-string <StorageAccountName>
    ```
    <span data-ttu-id="c74ad-176">Os dois comandos exigem que você entre no Azure primeiro.</span><span class="sxs-lookup"><span data-stu-id="c74ad-176">Both commands require you to first sign-in to Azure.</span></span>

## <a name="create-a-function"></a><span data-ttu-id="c74ad-177">Criar uma função</span><span class="sxs-lookup"><span data-stu-id="c74ad-177">Create a function</span></span>

<span data-ttu-id="c74ad-178">Para criar uma função, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="c74ad-178">To create a function, run the following command:</span></span>

```
func new
``` 
<span data-ttu-id="c74ad-179">`func new` dá suporte para os seguintes argumentos opcionais:</span><span class="sxs-lookup"><span data-stu-id="c74ad-179">`func new` supports the following optional arguments:</span></span>

| <span data-ttu-id="c74ad-180">Argumento</span><span class="sxs-lookup"><span data-stu-id="c74ad-180">Argument</span></span>     | <span data-ttu-id="c74ad-181">Descrição</span><span class="sxs-lookup"><span data-stu-id="c74ad-181">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--language -l`** | <span data-ttu-id="c74ad-182">A linguagem de programação modelo, como C#, F# ou JavaScript.</span><span class="sxs-lookup"><span data-stu-id="c74ad-182">The template programming language, such as C#, F#, or JavaScript.</span></span> |
| **`--template -t`** | <span data-ttu-id="c74ad-183">O nome do modelo.</span><span class="sxs-lookup"><span data-stu-id="c74ad-183">The template name.</span></span> |
| **`--name -n`** | <span data-ttu-id="c74ad-184">O nome da função.</span><span class="sxs-lookup"><span data-stu-id="c74ad-184">The function name.</span></span> |

<span data-ttu-id="c74ad-185">Por exemplo, para criar um gatilho de HTTP de JavaScript, execute:</span><span class="sxs-lookup"><span data-stu-id="c74ad-185">For example, to create a JavaScript HTTP trigger, run:</span></span>

```
func new --language JavaScript --template HttpTrigger --name MyHttpTrigger
```

<span data-ttu-id="c74ad-186">Para criar uma função ativada por fila, execute:</span><span class="sxs-lookup"><span data-stu-id="c74ad-186">To create a queue-triggered function, run:</span></span>

```
func new --language JavaScript --template QueueTrigger --name QueueTriggerJS
```

## <a name="run-functions-locally"></a><span data-ttu-id="c74ad-187">Executar funções localmente</span><span class="sxs-lookup"><span data-stu-id="c74ad-187">Run functions locally</span></span>

<span data-ttu-id="c74ad-188">Para executar um projeto de funções, execute o host de funções.</span><span class="sxs-lookup"><span data-stu-id="c74ad-188">To run a Functions project, run the Functions host.</span></span> <span data-ttu-id="c74ad-189">O host permite os gatilhos para todas as funções no projeto:</span><span class="sxs-lookup"><span data-stu-id="c74ad-189">The host enables triggers for all functions in the project:</span></span>

```
func host start
```

<span data-ttu-id="c74ad-190">`func host start` dá suporte para as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="c74ad-190">`func host start` supports the following options:</span></span>

| <span data-ttu-id="c74ad-191">Opção</span><span class="sxs-lookup"><span data-stu-id="c74ad-191">Option</span></span>     | <span data-ttu-id="c74ad-192">Descrição</span><span class="sxs-lookup"><span data-stu-id="c74ad-192">Description</span></span>                            |
| ------------ | -------------------------------------- |
|**`--port -p`** | <span data-ttu-id="c74ad-193">A porta local na qual escutar.</span><span class="sxs-lookup"><span data-stu-id="c74ad-193">The local port to listen on.</span></span> <span data-ttu-id="c74ad-194">Valor Padrão: 7071.</span><span class="sxs-lookup"><span data-stu-id="c74ad-194">Default value: 7071.</span></span> |
| **`--debug <type>`** | <span data-ttu-id="c74ad-195">As opções são `VSCode` e `VS`.</span><span class="sxs-lookup"><span data-stu-id="c74ad-195">The options are `VSCode` and `VS`.</span></span> |
| **`--cors`** | <span data-ttu-id="c74ad-196">Uma lista separada por vírgulas de origens CORS, sem espaços.</span><span class="sxs-lookup"><span data-stu-id="c74ad-196">A comma-separated list of CORS origins, with no spaces.</span></span> |
| **`--nodeDebugPort -n`** | <span data-ttu-id="c74ad-197">A porta para usar o depurador de nós.</span><span class="sxs-lookup"><span data-stu-id="c74ad-197">The port for the node debugger to use.</span></span> <span data-ttu-id="c74ad-198">Padrão: um valor de launch.json ou 5858.</span><span class="sxs-lookup"><span data-stu-id="c74ad-198">Default: A value from launch.json or 5858.</span></span> |
| **`--debugLevel -d`** | <span data-ttu-id="c74ad-199">O nível de rastreamento do console (desativado, detalhado, informações, aviso ou erro).</span><span class="sxs-lookup"><span data-stu-id="c74ad-199">The console trace level (off, verbose, info, warning, or error).</span></span> <span data-ttu-id="c74ad-200">Padrão: informações.</span><span class="sxs-lookup"><span data-stu-id="c74ad-200">Default: Info.</span></span>|
| **`--timeout -t`** | <span data-ttu-id="c74ad-201">O tempo limite para o host do Functions ser iniciado, em segundos.</span><span class="sxs-lookup"><span data-stu-id="c74ad-201">The time out for the Functions host t     o start, in seconds.</span></span> <span data-ttu-id="c74ad-202">Padrão: 20 segundos.</span><span class="sxs-lookup"><span data-stu-id="c74ad-202">Default: 20 seconds.</span></span>|
| **`--useHttps`** | <span data-ttu-id="c74ad-203">Associar a https://localhost:{port} em vez de a http://localhost:{port}.</span><span class="sxs-lookup"><span data-stu-id="c74ad-203">Bind to https://localhost:{port} rather than to http://localhost:{port}.</span></span> <span data-ttu-id="c74ad-204">Por padrão, essa opção cria um certificado confiável no computador.</span><span class="sxs-lookup"><span data-stu-id="c74ad-204">By default, this option creates a trusted certificate on your computer.</span></span>|
| **`--pause-on-error`** | <span data-ttu-id="c74ad-205">Pausar para entrada adicional antes de encerrar o processo.</span><span class="sxs-lookup"><span data-stu-id="c74ad-205">Pause for additional input before exiting the process.</span></span> <span data-ttu-id="c74ad-206">Útil ao iniciar as ferramentas básicas do Azure Functions de um ambiente de desenvolvimento integrado (IDE).</span><span class="sxs-lookup"><span data-stu-id="c74ad-206">Useful when launching Azure Functions Core Tools from an integrated development environment (IDE).</span></span>|

<span data-ttu-id="c74ad-207">Quando o host de funções é iniciado, ele gera as funções acionadas por URL de HTTP:</span><span class="sxs-lookup"><span data-stu-id="c74ad-207">When the Functions host starts, it outputs the URL of HTTP-triggered functions:</span></span>

```
Found the following functions:
Host.Functions.MyHttpTrigger

ob host started
Http Function MyHttpTrigger: http://localhost:7071/api/MyHttpTrigger
```

### <a name="debug-in-vs-code-or-visual-studio"></a><span data-ttu-id="c74ad-208">Depurar no VSCode ou no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c74ad-208">Debug in VS Code or Visual Studio</span></span>

<span data-ttu-id="c74ad-209">Para anexar um depurador, passe o argumento `--debug`.</span><span class="sxs-lookup"><span data-stu-id="c74ad-209">To attach a debugger, pass the `--debug` argument.</span></span> <span data-ttu-id="c74ad-210">Para depurar funções de JavaScript, use o Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="c74ad-210">To debug JavaScript functions, use Visual Studio Code.</span></span> <span data-ttu-id="c74ad-211">Para funções C#, use o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c74ad-211">For C# functions, use Visual Studio.</span></span>

<span data-ttu-id="c74ad-212">Para depurar funções C#, use `--debug vs`.</span><span class="sxs-lookup"><span data-stu-id="c74ad-212">To debug C# functions, use `--debug vs`.</span></span> <span data-ttu-id="c74ad-213">Você também pode usar as [Ferramentas do Visual Studio 2017 no Azure Functions](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span><span class="sxs-lookup"><span data-stu-id="c74ad-213">You can also use [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span></span> 

<span data-ttu-id="c74ad-214">Para iniciar o host e configurar a depuração de JavaScript, execute:</span><span class="sxs-lookup"><span data-stu-id="c74ad-214">To launch the host and set up JavaScript debugging, run:</span></span>

```
func host start --debug vscode
```

<span data-ttu-id="c74ad-215">Em seguida, no Visual Studio Code, na exibição **Depurar**, selecione **Anexar ao Azure Functions**.</span><span class="sxs-lookup"><span data-stu-id="c74ad-215">Then, in Visual Studio Code, in the **Debug** view, select **Attach to Azure Functions**.</span></span> <span data-ttu-id="c74ad-216">Você pode anexar os pontos de interrupção, inspecionar variáveis e o código por etapas.</span><span class="sxs-lookup"><span data-stu-id="c74ad-216">You can attach breakpoints, inspect variables, and step through code.</span></span>

![Depuração de JavaScript com o Visual Studio Code](./media/functions-run-local/vscode-javascript-debugging.png)

### <a name="passing-test-data-to-a-function"></a><span data-ttu-id="c74ad-218">Transferência dos dados de teste para uma função</span><span class="sxs-lookup"><span data-stu-id="c74ad-218">Passing test data to a function</span></span>

<span data-ttu-id="c74ad-219">Você também pode invocar uma função diretamente usando `func run <FunctionName>` e fornecer dados de entrada para a função.</span><span class="sxs-lookup"><span data-stu-id="c74ad-219">You can also invoke a function directly by using `func run <FunctionName>` and provide input data for the function.</span></span> <span data-ttu-id="c74ad-220">Esse comando é semelhante à execução de uma função usando a guia **Testar** no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c74ad-220">This command is similar to running a function using the **Test** tab in the Azure portal.</span></span> <span data-ttu-id="c74ad-221">Esse comando inicia todo o host de funções.</span><span class="sxs-lookup"><span data-stu-id="c74ad-221">This command launches the entire Functions host.</span></span>

<span data-ttu-id="c74ad-222">`func run` dá suporte para as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="c74ad-222">`func run` supports the following options:</span></span>

| <span data-ttu-id="c74ad-223">Opção</span><span class="sxs-lookup"><span data-stu-id="c74ad-223">Option</span></span>     | <span data-ttu-id="c74ad-224">Descrição</span><span class="sxs-lookup"><span data-stu-id="c74ad-224">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--content -c`** | <span data-ttu-id="c74ad-225">Conteúdo embutido.</span><span class="sxs-lookup"><span data-stu-id="c74ad-225">Inline content.</span></span> |
| **`--debug -d`** | <span data-ttu-id="c74ad-226">Anexe um depurador ao processo de host antes de executar a função.</span><span class="sxs-lookup"><span data-stu-id="c74ad-226">Attach a debugger to the host process before running the function.</span></span>|
| **`--timeout -t`** | <span data-ttu-id="c74ad-227">Tempo de espera (em segundos) até que o host local de funções esteja pronto.</span><span class="sxs-lookup"><span data-stu-id="c74ad-227">Time to wait (in seconds) until the local Functions host is ready.</span></span>|
| **`--file -f`** | <span data-ttu-id="c74ad-228">O nome do arquivo a ser usado como conteúdo.</span><span class="sxs-lookup"><span data-stu-id="c74ad-228">The file name to use as content.</span></span>|
| **`--no-interactive`** | <span data-ttu-id="c74ad-229">Não solicitará a entrada.</span><span class="sxs-lookup"><span data-stu-id="c74ad-229">Does not prompt for input.</span></span> <span data-ttu-id="c74ad-230">Útil para cenários de automação.</span><span class="sxs-lookup"><span data-stu-id="c74ad-230">Useful for automation scenarios.</span></span>|

<span data-ttu-id="c74ad-231">Por exemplo, para chamar uma função ativada por HTTP e passar o corpo do conteúdo, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="c74ad-231">For example, to call an HTTP-triggered function and pass content body, run the following command:</span></span>

```
func run MyHttpTrigger -c '{\"name\": \"Azure\"}'
```

## <span data-ttu-id="c74ad-232"><a name="publish"></a>Publicar no Azure</span><span class="sxs-lookup"><span data-stu-id="c74ad-232"><a name="publish"></a>Publish to Azure</span></span>

<span data-ttu-id="c74ad-233">Para publicar um projeto de funções em um aplicativo de funções no Azure, use o comando `publish`:</span><span class="sxs-lookup"><span data-stu-id="c74ad-233">To publish a Functions project to a function app in Azure, use the `publish` command:</span></span>

```
func azure functionapp publish <FunctionAppName>
```

<span data-ttu-id="c74ad-234">É possível usar as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="c74ad-234">You can use the following options:</span></span>

| <span data-ttu-id="c74ad-235">Opção</span><span class="sxs-lookup"><span data-stu-id="c74ad-235">Option</span></span>     | <span data-ttu-id="c74ad-236">Descrição</span><span class="sxs-lookup"><span data-stu-id="c74ad-236">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--publish-local-settings -i`** |  <span data-ttu-id="c74ad-237">Configurações de publicação em local.settings.json do Azure, a solicitação para substituir se a configuração já existe.</span><span class="sxs-lookup"><span data-stu-id="c74ad-237">Publish settings in local.settings.json to Azure, prompting to overwrite if the setting already exists.</span></span>|
| **`--overwrite-settings -y`** | <span data-ttu-id="c74ad-238">Deve ser usada com `-i`.</span><span class="sxs-lookup"><span data-stu-id="c74ad-238">Must be used with `-i`.</span></span> <span data-ttu-id="c74ad-239">Substitui o AppSettings no Azure com o valor local se for diferente.</span><span class="sxs-lookup"><span data-stu-id="c74ad-239">Overwrites AppSettings in Azure with local value if different.</span></span> <span data-ttu-id="c74ad-240">O padrão é solicitado.</span><span class="sxs-lookup"><span data-stu-id="c74ad-240">Default is prompt.</span></span>|

<span data-ttu-id="c74ad-241">O comando `publish` faz upload o conteúdo do diretório do projeto de funções.</span><span class="sxs-lookup"><span data-stu-id="c74ad-241">The `publish` command uploads the contents of the Functions project directory.</span></span> <span data-ttu-id="c74ad-242">Se você excluir arquivos localmente, o comando `publish` não os excluirá do Azure.</span><span class="sxs-lookup"><span data-stu-id="c74ad-242">If you delete files locally, the `publish` command does not delete them from Azure.</span></span> <span data-ttu-id="c74ad-243">Você pode excluir arquivos no Azure usando a [ferramenta Kudu](functions-how-to-use-azure-function-app-settings.md#kudu) no [Portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="c74ad-243">You can delete files in Azure by using the [Kudu tool](functions-how-to-use-azure-function-app-settings.md#kudu) in the [Azure portal].</span></span>

## <a name="next-steps"></a><span data-ttu-id="c74ad-244">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c74ad-244">Next steps</span></span>

<span data-ttu-id="c74ad-245">As principais ferramentas do Azure Functions são [Código-fonte aberto e hospedado no GitHub](https://github.com/azure/azure-functions-cli).</span><span class="sxs-lookup"><span data-stu-id="c74ad-245">Azure Functions Core Tools is [open source and hosted on GitHub](https://github.com/azure/azure-functions-cli).</span></span>  
<span data-ttu-id="c74ad-246">Para arquivar uma solicitação de bug ou recurso, [abra um problema do GitHub](https://github.com/azure/azure-functions-cli/issues).</span><span class="sxs-lookup"><span data-stu-id="c74ad-246">To file a bug or feature request, [open a GitHub issue](https://github.com/azure/azure-functions-cli/issues).</span></span> 

<!-- LINKS -->

[ferramentas básicas do Azure Functions]: https://www.npmjs.com/package/azure-functions-core-tools
[Portal do Azure]: https://portal.azure.com 
