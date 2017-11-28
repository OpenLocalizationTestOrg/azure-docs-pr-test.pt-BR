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
# <a name="code-and-test-azure-functions-locally"></a><span data-ttu-id="f55a1-103">Como codificar e testar o Azure Functions localmente</span><span class="sxs-lookup"><span data-stu-id="f55a1-103">Code and test Azure functions locally</span></span>

<span data-ttu-id="f55a1-104">Durante a saudação [portal do Azure] fornece um conjunto completo de ferramentas para desenvolvimento e teste funções do Azure, muitos desenvolvedores preferem uma experiência de desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="f55a1-104">While hello [Azure portal] provides a full set of tools for developing and testing Azure Functions, many developers prefer a local development experience.</span></span> <span data-ttu-id="f55a1-105">As funções do Azure torna fácil toouse seus favoritos toodevelop de ferramentas de desenvolvimento local e de editor de código e teste suas funções no computador local.</span><span class="sxs-lookup"><span data-stu-id="f55a1-105">Azure Functions makes it easy toouse your favorite code editor and local development tools toodevelop and test your functions on your local computer.</span></span> <span data-ttu-id="f55a1-106">As funções podem disparar eventos no Azure e você pode depurar o as funções de C# e JavaScript em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="f55a1-106">Your functions can trigger on events in Azure, and you can debug your C# and JavaScript functions on your local computer.</span></span> 

<span data-ttu-id="f55a1-107">Se você for um desenvolvedor de C# no Visual Studio, o Azure Functions também [se integrará ao Visual Studio de 2017](functions-develop-vs.md).</span><span class="sxs-lookup"><span data-stu-id="f55a1-107">If you are a Visual Studio C# developer, Azure Functions also [integrates with Visual Studio 2017](functions-develop-vs.md).</span></span>

## <a name="install-hello-azure-functions-core-tools"></a><span data-ttu-id="f55a1-108">Instalar as ferramentas de núcleo de funções hello Azure</span><span class="sxs-lookup"><span data-stu-id="f55a1-108">Install hello Azure Functions Core Tools</span></span>

<span data-ttu-id="f55a1-109">Ferramentas de núcleo de funções do Azure é uma versão local do tempo de execução de funções do Azure Olá que podem ser executados no computador local do Windows.</span><span class="sxs-lookup"><span data-stu-id="f55a1-109">Azure Functions Core Tools is a local version of hello Azure Functions runtime that you can run on your local Windows computer.</span></span> <span data-ttu-id="f55a1-110">Não é um simulador ou emulador.</span><span class="sxs-lookup"><span data-stu-id="f55a1-110">It's not an emulator or simulator.</span></span> <span data-ttu-id="f55a1-111">Ele tem Olá em tempo de execução mesmo que liga funções no Azure.</span><span class="sxs-lookup"><span data-stu-id="f55a1-111">It's hello same runtime that powers Functions in Azure.</span></span>

<span data-ttu-id="f55a1-112">Olá [Azure funções principais ferramentas] é fornecido como um pacote de npm.</span><span class="sxs-lookup"><span data-stu-id="f55a1-112">hello [Azure Functions Core Tools] is provided as an npm package.</span></span> <span data-ttu-id="f55a1-113">Você deve primeiro [instalar o NodeJS](https://docs.npmjs.com/getting-started/installing-node), que inclui npm.</span><span class="sxs-lookup"><span data-stu-id="f55a1-113">You must first [install NodeJS](https://docs.npmjs.com/getting-started/installing-node), which includes npm.</span></span>  

>[!NOTE]
><span data-ttu-id="f55a1-114">Neste momento, o pacote de ferramentas do Azure funções principais de Olá só pode ser instalado em computadores com Windows.</span><span class="sxs-lookup"><span data-stu-id="f55a1-114">At this time, hello Azure Functions Core Tools package can only be installed on Windows computers.</span></span> <span data-ttu-id="f55a1-115">Essa restrição é devido a limitação temporária tooa no host de funções hello.</span><span class="sxs-lookup"><span data-stu-id="f55a1-115">This restriction is due tooa temporary limitation in hello Functions host.</span></span>

<span data-ttu-id="f55a1-116">[Ferramentas de núcleo de funções do Azure] adiciona Olá aliases de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="f55a1-116">[Azure Functions Core Tools] adds hello following command aliases:</span></span>
* <span data-ttu-id="f55a1-117">**func**</span><span class="sxs-lookup"><span data-stu-id="f55a1-117">**func**</span></span>
* <span data-ttu-id="f55a1-118">**azfun**</span><span class="sxs-lookup"><span data-stu-id="f55a1-118">**azfun**</span></span>
* <span data-ttu-id="f55a1-119">**azurefunctions**</span><span class="sxs-lookup"><span data-stu-id="f55a1-119">**azurefunctions**</span></span>

<span data-ttu-id="f55a1-120">Todos esses alias podem ser usados em vez de `func` mostrado nos exemplos de saudação neste tópico.</span><span class="sxs-lookup"><span data-stu-id="f55a1-120">All of these alias can be used instead of `func` shown in hello examples in this topic.</span></span>

## <a name="create-a-local-functions-project"></a><span data-ttu-id="f55a1-121">Criar um projeto de funções local</span><span class="sxs-lookup"><span data-stu-id="f55a1-121">Create a local Functions project</span></span>

<span data-ttu-id="f55a1-122">Quando em execução localmente, um projeto de funções é um diretório com local.settings.json e Olá arquivos host.json.</span><span class="sxs-lookup"><span data-stu-id="f55a1-122">When running locally, a Functions project is a directory that has hello files host.json and local.settings.json.</span></span> <span data-ttu-id="f55a1-123">Esse diretório é Olá equivalente de um aplicativo de função no Azure.</span><span class="sxs-lookup"><span data-stu-id="f55a1-123">This directory is hello equivalent of a function app in Azure.</span></span> <span data-ttu-id="f55a1-124">toolearn mais sobre Olá estrutura de pastas de funções do Azure, consulte Olá [guia de desenvolvedores do Azure funções](functions-reference.md#folder-structure).</span><span class="sxs-lookup"><span data-stu-id="f55a1-124">toolearn more about hello Azure Functions folder structure, see hello [Azure Functions developers guide](functions-reference.md#folder-structure).</span></span>

<span data-ttu-id="f55a1-125">Em um prompt de comando, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="f55a1-125">At a command prompt, run hello following command:</span></span>

```
func init MyFunctionProj
```

<span data-ttu-id="f55a1-126">saída de Hello aparência Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="f55a1-126">hello output looks like hello following example:</span></span>

```
Writing .gitignore
Writing host.json
Writing local.settings.json
Created launch.json
Initialized empty Git repository in D:/Code/Playground/MyFunctionProj/.git/
```

<span data-ttu-id="f55a1-127">tooopt fora da criação de um repositório Git, use a opção de saudação `--no-source-control [-n]`.</span><span class="sxs-lookup"><span data-stu-id="f55a1-127">tooopt out of creating a Git repository, use hello option `--no-source-control [-n]`.</span></span>

<a name="local-settings"></a>

## <a name="local-settings-file"></a><span data-ttu-id="f55a1-128">Arquivo de configurações local</span><span class="sxs-lookup"><span data-stu-id="f55a1-128">Local settings file</span></span>

<span data-ttu-id="f55a1-129">Olá arquivo local.settings.json armazena configurações do aplicativo, cadeias de caracteres de conexão e as configurações para as ferramentas de núcleo de funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="f55a1-129">hello file local.settings.json stores app settings, connection strings, and settings for Azure Functions Core Tools.</span></span> <span data-ttu-id="f55a1-130">Ele tem Olá estrutura a seguir:</span><span class="sxs-lookup"><span data-stu-id="f55a1-130">It has hello following structure:</span></span>

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
| <span data-ttu-id="f55a1-131">Configuração</span><span class="sxs-lookup"><span data-stu-id="f55a1-131">Setting</span></span>      | <span data-ttu-id="f55a1-132">Descrição</span><span class="sxs-lookup"><span data-stu-id="f55a1-132">Description</span></span>                            |
| ------------ | -------------------------------------- |
| <span data-ttu-id="f55a1-133">**IsEncrypted**</span><span class="sxs-lookup"><span data-stu-id="f55a1-133">**IsEncrypted**</span></span> | <span data-ttu-id="f55a1-134">Quando definido muito**true**, todos os valores são criptografados usando uma chave de computador local.</span><span class="sxs-lookup"><span data-stu-id="f55a1-134">When set too**true**, all values are encrypted using a local machine key.</span></span> <span data-ttu-id="f55a1-135">Usado com `func settings` comandos.</span><span class="sxs-lookup"><span data-stu-id="f55a1-135">Used with `func settings` commands.</span></span> <span data-ttu-id="f55a1-136">O valor padrão é **false**.</span><span class="sxs-lookup"><span data-stu-id="f55a1-136">Default value is **false**.</span></span> |
| <span data-ttu-id="f55a1-137">**Valores**</span><span class="sxs-lookup"><span data-stu-id="f55a1-137">**Values**</span></span> | <span data-ttu-id="f55a1-138">Coleção de configuração de aplicativo usada quando executada localmente.</span><span class="sxs-lookup"><span data-stu-id="f55a1-138">Collection of application settings used when running locally.</span></span> <span data-ttu-id="f55a1-139">Adicione o objeto de toothis de configurações do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f55a1-139">Add your application settings toothis object.</span></span>  |
| <span data-ttu-id="f55a1-140">**AzureWebJobsStorage**</span><span class="sxs-lookup"><span data-stu-id="f55a1-140">**AzureWebJobsStorage**</span></span> | <span data-ttu-id="f55a1-141">Conjuntos de Olá toohello de cadeia de caracteres de conexão conta de armazenamento do Azure que é usada internamente pelo tempo de execução de funções do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="f55a1-141">Sets hello connection string toohello Azure Storage account that is used internally by hello Azure Functions runtime.</span></span> <span data-ttu-id="f55a1-142">conta de armazenamento Olá dá suporte a gatilhos da função.</span><span class="sxs-lookup"><span data-stu-id="f55a1-142">hello storage account supports your function's triggers.</span></span> <span data-ttu-id="f55a1-143">Essa configuração de conexão de conta de armazenamento é necessária para todas as funções, exceto para as funções HTTP acionadas.</span><span class="sxs-lookup"><span data-stu-id="f55a1-143">This storage account connection setting is required for all functions except for HTTP triggered functions.</span></span>  |
| <span data-ttu-id="f55a1-144">**AzureWebJobsDashboard**</span><span class="sxs-lookup"><span data-stu-id="f55a1-144">**AzureWebJobsDashboard**</span></span> | <span data-ttu-id="f55a1-145">Define Olá conexão cadeia de caracteres toohello armazenamento do Azure conta é usada toostore Olá função logs.</span><span class="sxs-lookup"><span data-stu-id="f55a1-145">Sets hello connection string toohello Azure Storage account that is used toostore hello function logs.</span></span> <span data-ttu-id="f55a1-146">Esse valor opcional torna os logs de saudação acessível no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="f55a1-146">This optional value makes hello logs accessible in hello portal.</span></span>|
| <span data-ttu-id="f55a1-147">**Host**</span><span class="sxs-lookup"><span data-stu-id="f55a1-147">**Host**</span></span> | <span data-ttu-id="f55a1-148">Configurações nesta seção personalizar o processo de host de funções hello quando em execução localmente.</span><span class="sxs-lookup"><span data-stu-id="f55a1-148">Settings in this section customize hello Functions host process when running locally.</span></span> | 
| <span data-ttu-id="f55a1-149">**LocalHttpPort**</span><span class="sxs-lookup"><span data-stu-id="f55a1-149">**LocalHttpPort**</span></span> | <span data-ttu-id="f55a1-150">Conjuntos de hello a porta padrão usada ao executar o host local de funções hello (`func host start` e `func run`).</span><span class="sxs-lookup"><span data-stu-id="f55a1-150">Sets hello default port used when running hello local Functions host (`func host start` and `func run`).</span></span> <span data-ttu-id="f55a1-151">Olá `--port` opção de linha de comando tem precedência sobre esse valor.</span><span class="sxs-lookup"><span data-stu-id="f55a1-151">hello `--port` command-line option takes precedence over this value.</span></span> |
| <span data-ttu-id="f55a1-152">**CORS**</span><span class="sxs-lookup"><span data-stu-id="f55a1-152">**CORS**</span></span> | <span data-ttu-id="f55a1-153">Define as origens de saudação permitidas para [recursos entre origens (CORS) de compartilhamento](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing).</span><span class="sxs-lookup"><span data-stu-id="f55a1-153">Defines hello origins allowed for [cross-origin resource sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing).</span></span> <span data-ttu-id="f55a1-154">As origens são fornecidas como uma lista separada por vírgulas, sem espaços.</span><span class="sxs-lookup"><span data-stu-id="f55a1-154">Origins are supplied as a comma-separated list with no spaces.</span></span> <span data-ttu-id="f55a1-155">Olá valor curinga (**\***) tem suporte, que permite que as solicitações de qualquer origem.</span><span class="sxs-lookup"><span data-stu-id="f55a1-155">hello wildcard value (**\***) is supported, which allows requests from any origin.</span></span> |
| <span data-ttu-id="f55a1-156">**ConnectionStrings**</span><span class="sxs-lookup"><span data-stu-id="f55a1-156">**ConnectionStrings**</span></span> | <span data-ttu-id="f55a1-157">Contém cadeias de conexão de banco de dados de saudação para suas funções.</span><span class="sxs-lookup"><span data-stu-id="f55a1-157">Contains hello database connection strings for your functions.</span></span> <span data-ttu-id="f55a1-158">Cadeias de caracteres de Conexão no objeto são adicionadas toohello ambiente com o tipo de provedor de saudação do **SqlClient**.</span><span class="sxs-lookup"><span data-stu-id="f55a1-158">Connection strings in this object are added toohello environment with hello provider type of **System.Data.SqlClient**.</span></span>  | 

<span data-ttu-id="f55a1-159">A maioria dos disparadores e associações não têm um **Conexão** propriedade que mapeia o nome de uma configuração de aplicativo ou a variável de ambiente toohello.</span><span class="sxs-lookup"><span data-stu-id="f55a1-159">Most triggers and bindings have a **Connection** property that maps toohello name of an environment variable or app setting.</span></span> <span data-ttu-id="f55a1-160">Para cada propriedade de conexão, deve haver uma configuração de aplicativo definida no arquivo local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="f55a1-160">For each connection property, there must be app setting defined in local.settings.json file.</span></span> 

<span data-ttu-id="f55a1-161">Essas configurações também podem ser lidas em seu código como variáveis de ambiente.</span><span class="sxs-lookup"><span data-stu-id="f55a1-161">These settings can also be read in your code as environment variables.</span></span> <span data-ttu-id="f55a1-162">No C#, use [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) ou [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx).</span><span class="sxs-lookup"><span data-stu-id="f55a1-162">In C#, use [System.Environment.GetEnvironmentVariable](https://msdn.microsoft.com/library/system.environment.getenvironmentvariable(v=vs.110).aspx) or [ConfigurationManager.AppSettings](https://msdn.microsoft.com/library/system.configuration.configurationmanager.appsettings%28v=vs.110%29.aspx).</span></span> <span data-ttu-id="f55a1-163">No JavaScript, use `process.env`.</span><span class="sxs-lookup"><span data-stu-id="f55a1-163">In JavaScript, use `process.env`.</span></span> <span data-ttu-id="f55a1-164">As configurações especificadas como uma variável de ambiente do sistema têm precedência sobre valores no arquivo de local.settings.json hello.</span><span class="sxs-lookup"><span data-stu-id="f55a1-164">Settings specified as a system environment variable take precedence over values in hello local.settings.json file.</span></span> 

<span data-ttu-id="f55a1-165">As configurações no arquivo de local.settings.json Olá só são usadas por ferramentas de funções quando em execução localmente.</span><span class="sxs-lookup"><span data-stu-id="f55a1-165">Settings in hello local.settings.json file are only used by Functions tools when running locally.</span></span> <span data-ttu-id="f55a1-166">Por padrão, essas configurações não são migradas automaticamente quando o projeto de saudação é tooAzure publicado.</span><span class="sxs-lookup"><span data-stu-id="f55a1-166">By default, these settings are not migrated automatically when hello project is published tooAzure.</span></span> <span data-ttu-id="f55a1-167">Saudação de uso `--publish-local-settings` alternar [quando você publica](#publish) toomake-se de que essas configurações são adicionadas toohello função aplicativo no Azure.</span><span class="sxs-lookup"><span data-stu-id="f55a1-167">Use hello `--publish-local-settings` switch [when you publish](#publish) toomake sure these settings are added toohello function app in Azure.</span></span>

<span data-ttu-id="f55a1-168">Quando nenhuma cadeia de caracteres de conexão de armazenamento válido é definida para **AzureWebJobsStorage**, Olá a seguinte mensagem de erro é exibida:</span><span class="sxs-lookup"><span data-stu-id="f55a1-168">When no valid storage connection string is set for **AzureWebJobsStorage**, hello following error message is shown:</span></span>  

><span data-ttu-id="f55a1-169">Valor ausente para AzureWebJobsStorage em local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="f55a1-169">Missing value for AzureWebJobsStorage in local.settings.json.</span></span> <span data-ttu-id="f55a1-170">Isso é necessário para todos os gatilhos diferentes de HTTP.</span><span class="sxs-lookup"><span data-stu-id="f55a1-170">This is required for all triggers other than HTTP.</span></span> <span data-ttu-id="f55a1-171">Você pode executar 'func azure functionary fetch-app-settings <functionAppName>' ou especificar uma cadeia de conexão em local.settings.json.</span><span class="sxs-lookup"><span data-stu-id="f55a1-171">You can run 'func azure functionary fetch-app-settings <functionAppName>' or specify a connection string in local.settings.json.</span></span>
  
[!INCLUDE [Note toonot use local storage](../../includes/functions-local-settings-note.md)]

### <a name="configure-app-settings"></a><span data-ttu-id="f55a1-172">Definir configurações de aplicativo</span><span class="sxs-lookup"><span data-stu-id="f55a1-172">Configure app settings</span></span>

<span data-ttu-id="f55a1-173">tooset um valor para cadeias de caracteres de conexão, você pode fazer um dos seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="f55a1-173">tooset a value for connection strings, you can do one of hello following:</span></span>
* <span data-ttu-id="f55a1-174">Insira a cadeia de caracteres de conexão de saudação do [Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="f55a1-174">Enter hello connection string from [Azure Storage Explorer](http://storageexplorer.com/).</span></span>
* <span data-ttu-id="f55a1-175">Use uma saudação comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="f55a1-175">Use one of hello following commands:</span></span>

    ```
    func azure functionapp fetch-app-settings <FunctionAppName>
    ```
    ```
    func azure functionapp storage fetch-connection-string <StorageAccountName>
    ```
    <span data-ttu-id="f55a1-176">Os dois comandos exigem que você toofirst entrar tooAzure.</span><span class="sxs-lookup"><span data-stu-id="f55a1-176">Both commands require you toofirst sign-in tooAzure.</span></span>

## <a name="create-a-function"></a><span data-ttu-id="f55a1-177">Criar uma função</span><span class="sxs-lookup"><span data-stu-id="f55a1-177">Create a function</span></span>

<span data-ttu-id="f55a1-178">toocreate uma função, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="f55a1-178">toocreate a function, run hello following command:</span></span>

```
func new
``` 
<span data-ttu-id="f55a1-179">`func new`Olá dá suporte a argumentos opcionais a seguir:</span><span class="sxs-lookup"><span data-stu-id="f55a1-179">`func new` supports hello following optional arguments:</span></span>

| <span data-ttu-id="f55a1-180">Argumento</span><span class="sxs-lookup"><span data-stu-id="f55a1-180">Argument</span></span>     | <span data-ttu-id="f55a1-181">Descrição</span><span class="sxs-lookup"><span data-stu-id="f55a1-181">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--language -l`** | <span data-ttu-id="f55a1-182">modelo de saudação linguagem de programação, como c#, F # ou JavaScript.</span><span class="sxs-lookup"><span data-stu-id="f55a1-182">hello template programming language, such as C#, F#, or JavaScript.</span></span> |
| **`--template -t`** | <span data-ttu-id="f55a1-183">nome do modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="f55a1-183">hello template name.</span></span> |
| **`--name -n`** | <span data-ttu-id="f55a1-184">nome da função Hello.</span><span class="sxs-lookup"><span data-stu-id="f55a1-184">hello function name.</span></span> |

<span data-ttu-id="f55a1-185">Por exemplo, toocreate um gatilho de HTTP de JavaScript, execute:</span><span class="sxs-lookup"><span data-stu-id="f55a1-185">For example, toocreate a JavaScript HTTP trigger, run:</span></span>

```
func new --language JavaScript --template HttpTrigger --name MyHttpTrigger
```

<span data-ttu-id="f55a1-186">toocreate uma função disparado em fila, execute:</span><span class="sxs-lookup"><span data-stu-id="f55a1-186">toocreate a queue-triggered function, run:</span></span>

```
func new --language JavaScript --template QueueTrigger --name QueueTriggerJS
```

## <a name="run-functions-locally"></a><span data-ttu-id="f55a1-187">Executar funções localmente</span><span class="sxs-lookup"><span data-stu-id="f55a1-187">Run functions locally</span></span>

<span data-ttu-id="f55a1-188">toorun um projeto de funções, executar o host de funções hello.</span><span class="sxs-lookup"><span data-stu-id="f55a1-188">toorun a Functions project, run hello Functions host.</span></span> <span data-ttu-id="f55a1-189">o host de saudação permite que gatilhos para todas as funções no projeto hello:</span><span class="sxs-lookup"><span data-stu-id="f55a1-189">hello host enables triggers for all functions in hello project:</span></span>

```
func host start
```

<span data-ttu-id="f55a1-190">`func host start`dá suporte a saudação as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="f55a1-190">`func host start` supports hello following options:</span></span>

| <span data-ttu-id="f55a1-191">Opção</span><span class="sxs-lookup"><span data-stu-id="f55a1-191">Option</span></span>     | <span data-ttu-id="f55a1-192">Descrição</span><span class="sxs-lookup"><span data-stu-id="f55a1-192">Description</span></span>                            |
| ------------ | -------------------------------------- |
|**`--port -p`** | <span data-ttu-id="f55a1-193">Olá toolisten de porta local no.</span><span class="sxs-lookup"><span data-stu-id="f55a1-193">hello local port toolisten on.</span></span> <span data-ttu-id="f55a1-194">Valor Padrão: 7071.</span><span class="sxs-lookup"><span data-stu-id="f55a1-194">Default value: 7071.</span></span> |
| **`--debug <type>`** | <span data-ttu-id="f55a1-195">Opções de saudação são `VSCode` e `VS`.</span><span class="sxs-lookup"><span data-stu-id="f55a1-195">hello options are `VSCode` and `VS`.</span></span> |
| **`--cors`** | <span data-ttu-id="f55a1-196">Uma lista separada por vírgulas de origens CORS, sem espaços.</span><span class="sxs-lookup"><span data-stu-id="f55a1-196">A comma-separated list of CORS origins, with no spaces.</span></span> |
| **`--nodeDebugPort -n`** | <span data-ttu-id="f55a1-197">porta Olá Olá nó depurador toouse.</span><span class="sxs-lookup"><span data-stu-id="f55a1-197">hello port for hello node debugger toouse.</span></span> <span data-ttu-id="f55a1-198">Padrão: um valor de launch.json ou 5858.</span><span class="sxs-lookup"><span data-stu-id="f55a1-198">Default: A value from launch.json or 5858.</span></span> |
| **`--debugLevel -d`** | <span data-ttu-id="f55a1-199">nível de rastreamento do console Hello (desativado, detalhado, informações, aviso ou erro).</span><span class="sxs-lookup"><span data-stu-id="f55a1-199">hello console trace level (off, verbose, info, warning, or error).</span></span> <span data-ttu-id="f55a1-200">Padrão: informações.</span><span class="sxs-lookup"><span data-stu-id="f55a1-200">Default: Info.</span></span>|
| **`--timeout -t`** | <span data-ttu-id="f55a1-201">Olá tempo limite para Olá funções host para iniciar, em segundos.</span><span class="sxs-lookup"><span data-stu-id="f55a1-201">hello time out for hello Functions host t     o start, in seconds.</span></span> <span data-ttu-id="f55a1-202">Padrão: 20 segundos.</span><span class="sxs-lookup"><span data-stu-id="f55a1-202">Default: 20 seconds.</span></span>|
| **`--useHttps`** | <span data-ttu-id="f55a1-203">Associar toohttps://localhost: {porta} em vez de toohttp://localhost: {port}.</span><span class="sxs-lookup"><span data-stu-id="f55a1-203">Bind toohttps://localhost:{port} rather than toohttp://localhost:{port}.</span></span> <span data-ttu-id="f55a1-204">Por padrão, essa opção cria um certificado confiável no computador.</span><span class="sxs-lookup"><span data-stu-id="f55a1-204">By default, this option creates a trusted certificate on your computer.</span></span>|
| **`--pause-on-error`** | <span data-ttu-id="f55a1-205">Pausar para entrada adicional antes de sair do processo de saudação.</span><span class="sxs-lookup"><span data-stu-id="f55a1-205">Pause for additional input before exiting hello process.</span></span> <span data-ttu-id="f55a1-206">Útil ao iniciar as ferramentas básicas do Azure Functions de um ambiente de desenvolvimento integrado (IDE).</span><span class="sxs-lookup"><span data-stu-id="f55a1-206">Useful when launching Azure Functions Core Tools from an integrated development environment (IDE).</span></span>|

<span data-ttu-id="f55a1-207">Quando o host de funções hello é iniciado, ele produz funções disparou a URL de HTTP do hello:</span><span class="sxs-lookup"><span data-stu-id="f55a1-207">When hello Functions host starts, it outputs hello URL of HTTP-triggered functions:</span></span>

```
Found hello following functions:
Host.Functions.MyHttpTrigger

ob host started
Http Function MyHttpTrigger: http://localhost:7071/api/MyHttpTrigger
```

### <a name="debug-in-vs-code-or-visual-studio"></a><span data-ttu-id="f55a1-208">Depurar no VSCode ou no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f55a1-208">Debug in VS Code or Visual Studio</span></span>

<span data-ttu-id="f55a1-209">tooattach um depurador passar Olá `--debug` argumento.</span><span class="sxs-lookup"><span data-stu-id="f55a1-209">tooattach a debugger, pass hello `--debug` argument.</span></span> <span data-ttu-id="f55a1-210">funções em JavaScript toodebug, use o código do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f55a1-210">toodebug JavaScript functions, use Visual Studio Code.</span></span> <span data-ttu-id="f55a1-211">Para funções C#, use o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f55a1-211">For C# functions, use Visual Studio.</span></span>

<span data-ttu-id="f55a1-212">funções toodebug c#, use `--debug vs`.</span><span class="sxs-lookup"><span data-stu-id="f55a1-212">toodebug C# functions, use `--debug vs`.</span></span> <span data-ttu-id="f55a1-213">Você também pode usar as [Ferramentas do Visual Studio 2017 no Azure Functions](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span><span class="sxs-lookup"><span data-stu-id="f55a1-213">You can also use [Azure Functions Visual Studio 2017 Tools](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/).</span></span> 

<span data-ttu-id="f55a1-214">host de saudação toolaunch e configure a depuração de JavaScript, execute:</span><span class="sxs-lookup"><span data-stu-id="f55a1-214">toolaunch hello host and set up JavaScript debugging, run:</span></span>

```
func host start --debug vscode
```

<span data-ttu-id="f55a1-215">Em seguida, no código do Visual Studio, no hello **depurar** exibição, selecione **anexar tooAzure funções**.</span><span class="sxs-lookup"><span data-stu-id="f55a1-215">Then, in Visual Studio Code, in hello **Debug** view, select **Attach tooAzure Functions**.</span></span> <span data-ttu-id="f55a1-216">Você pode anexar os pontos de interrupção, inspecionar variáveis e o código por etapas.</span><span class="sxs-lookup"><span data-stu-id="f55a1-216">You can attach breakpoints, inspect variables, and step through code.</span></span>

![Depuração de JavaScript com o Visual Studio Code](./media/functions-run-local/vscode-javascript-debugging.png)

### <a name="passing-test-data-tooa-function"></a><span data-ttu-id="f55a1-218">Função de tooa de dados de teste de passagem</span><span class="sxs-lookup"><span data-stu-id="f55a1-218">Passing test data tooa function</span></span>

<span data-ttu-id="f55a1-219">Você também pode chamar uma função diretamente por meio de `func run <FunctionName>` e fornecer dados de entrada para a função hello.</span><span class="sxs-lookup"><span data-stu-id="f55a1-219">You can also invoke a function directly by using `func run <FunctionName>` and provide input data for hello function.</span></span> <span data-ttu-id="f55a1-220">Esse comando é semelhante toorunning uma função usando Olá **teste** guia Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f55a1-220">This command is similar toorunning a function using hello **Test** tab in hello Azure portal.</span></span> <span data-ttu-id="f55a1-221">Esse comando inicia o host de funções toda hello.</span><span class="sxs-lookup"><span data-stu-id="f55a1-221">This command launches hello entire Functions host.</span></span>

<span data-ttu-id="f55a1-222">`func run`dá suporte a saudação as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="f55a1-222">`func run` supports hello following options:</span></span>

| <span data-ttu-id="f55a1-223">Opção</span><span class="sxs-lookup"><span data-stu-id="f55a1-223">Option</span></span>     | <span data-ttu-id="f55a1-224">Descrição</span><span class="sxs-lookup"><span data-stu-id="f55a1-224">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--content -c`** | <span data-ttu-id="f55a1-225">Conteúdo embutido.</span><span class="sxs-lookup"><span data-stu-id="f55a1-225">Inline content.</span></span> |
| **`--debug -d`** | <span data-ttu-id="f55a1-226">Anexe um processo de host do depurador toohello antes de executar a função hello.</span><span class="sxs-lookup"><span data-stu-id="f55a1-226">Attach a debugger toohello host process before running hello function.</span></span>|
| **`--timeout -t`** | <span data-ttu-id="f55a1-227">Toowait de tempo (em segundos) até que o host local de funções hello está pronto.</span><span class="sxs-lookup"><span data-stu-id="f55a1-227">Time toowait (in seconds) until hello local Functions host is ready.</span></span>|
| **`--file -f`** | <span data-ttu-id="f55a1-228">Olá toouse de nome de arquivo como conteúdo.</span><span class="sxs-lookup"><span data-stu-id="f55a1-228">hello file name toouse as content.</span></span>|
| **`--no-interactive`** | <span data-ttu-id="f55a1-229">Não solicitará a entrada.</span><span class="sxs-lookup"><span data-stu-id="f55a1-229">Does not prompt for input.</span></span> <span data-ttu-id="f55a1-230">Útil para cenários de automação.</span><span class="sxs-lookup"><span data-stu-id="f55a1-230">Useful for automation scenarios.</span></span>|

<span data-ttu-id="f55a1-231">Por exemplo, toocall uma função disparado por HTTP e corpo de conteúdo de passagem, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="f55a1-231">For example, toocall an HTTP-triggered function and pass content body, run hello following command:</span></span>

```
func run MyHttpTrigger -c '{\"name\": \"Azure\"}'
```

## <span data-ttu-id="f55a1-232"><a name="publish"></a>Publicar tooAzure</span><span class="sxs-lookup"><span data-stu-id="f55a1-232"><a name="publish"></a>Publish tooAzure</span></span>

<span data-ttu-id="f55a1-233">toopublish um aplicativo de função funções projeto tooa no Azure, use Olá `publish` comando:</span><span class="sxs-lookup"><span data-stu-id="f55a1-233">toopublish a Functions project tooa function app in Azure, use hello `publish` command:</span></span>

```
func azure functionapp publish <FunctionAppName>
```

<span data-ttu-id="f55a1-234">Você pode usar o hello as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="f55a1-234">You can use hello following options:</span></span>

| <span data-ttu-id="f55a1-235">Opção</span><span class="sxs-lookup"><span data-stu-id="f55a1-235">Option</span></span>     | <span data-ttu-id="f55a1-236">Descrição</span><span class="sxs-lookup"><span data-stu-id="f55a1-236">Description</span></span>                            |
| ------------ | -------------------------------------- |
| **`--publish-local-settings -i`** |  <span data-ttu-id="f55a1-237">Configurações de publicação no local.settings.json tooAzure, solicitando toooverwrite se Olá configuração já existe.</span><span class="sxs-lookup"><span data-stu-id="f55a1-237">Publish settings in local.settings.json tooAzure, prompting toooverwrite if hello setting already exists.</span></span>|
| **`--overwrite-settings -y`** | <span data-ttu-id="f55a1-238">Deve ser usada com `-i`.</span><span class="sxs-lookup"><span data-stu-id="f55a1-238">Must be used with `-i`.</span></span> <span data-ttu-id="f55a1-239">Substitui o AppSettings no Azure com o valor local se for diferente.</span><span class="sxs-lookup"><span data-stu-id="f55a1-239">Overwrites AppSettings in Azure with local value if different.</span></span> <span data-ttu-id="f55a1-240">O padrão é solicitado.</span><span class="sxs-lookup"><span data-stu-id="f55a1-240">Default is prompt.</span></span>|

<span data-ttu-id="f55a1-241">Olá `publish` comando carrega o conteúdo de saudação do diretório do projeto funções hello.</span><span class="sxs-lookup"><span data-stu-id="f55a1-241">hello `publish` command uploads hello contents of hello Functions project directory.</span></span> <span data-ttu-id="f55a1-242">Se você excluir arquivos localmente, Olá `publish` comando não os exclui do Azure.</span><span class="sxs-lookup"><span data-stu-id="f55a1-242">If you delete files locally, hello `publish` command does not delete them from Azure.</span></span> <span data-ttu-id="f55a1-243">Você pode excluir arquivos no Azure usando Olá [ferramenta Kudu](functions-how-to-use-azure-function-app-settings.md#kudu) em Olá [portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="f55a1-243">You can delete files in Azure by using hello [Kudu tool](functions-how-to-use-azure-function-app-settings.md#kudu) in hello [Azure portal].</span></span>

## <a name="next-steps"></a><span data-ttu-id="f55a1-244">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f55a1-244">Next steps</span></span>

<span data-ttu-id="f55a1-245">As principais ferramentas do Azure Functions são [Código-fonte aberto e hospedado no GitHub](https://github.com/azure/azure-functions-cli).</span><span class="sxs-lookup"><span data-stu-id="f55a1-245">Azure Functions Core Tools is [open source and hosted on GitHub](https://github.com/azure/azure-functions-cli).</span></span>  
<span data-ttu-id="f55a1-246">toofile uma solicitação de bug ou recurso, [abrir um problema do GitHub](https://github.com/azure/azure-functions-cli/issues).</span><span class="sxs-lookup"><span data-stu-id="f55a1-246">toofile a bug or feature request, [open a GitHub issue](https://github.com/azure/azure-functions-cli/issues).</span></span> 

<!-- LINKS -->

[Ferramentas básicas do Azure Functions]: https://www.npmjs.com/package/azure-functions-core-tools
[Portal do Azure]: https://portal.azure.com 
