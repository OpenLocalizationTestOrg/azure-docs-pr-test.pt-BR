---
title: artefatos de aaaCreate personalizado para sua VM do DevTest Labs | Microsoft Docs
description: "Saiba como tooauthor seus próprios artefatos para usam com o DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 32dcdc61-ec23-4a01-b731-78c029ea5316
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: tarcher
ms.openlocfilehash: 2bd603bc1241ca6b669a3a276a677729514f0df2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-custom-artifacts-for-your-devtest-labs-vm"></a><span data-ttu-id="80e3a-103">Criar artefatos personalizados para suas VM dos Laboratórios de Desenvolvimento/Teste.</span><span class="sxs-lookup"><span data-stu-id="80e3a-103">Create custom artifacts for your DevTest Labs VM</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/how-to-author-custom-artifacts/player]
> 
> 

## <a name="overview"></a><span data-ttu-id="80e3a-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="80e3a-104">Overview</span></span>
<span data-ttu-id="80e3a-105">**Artefatos** são usado toodeploy e configurar seu aplicativo depois que uma VM é provisionada.</span><span class="sxs-lookup"><span data-stu-id="80e3a-105">**Artifacts** are used toodeploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="80e3a-106">Um artefato é composto por um arquivo de definição de artefato e outros arquivos de script que são armazenados em uma pasta em um repositório git.</span><span class="sxs-lookup"><span data-stu-id="80e3a-106">An artifact consists of an artifact definition file and other script files that are stored in a folder in a git repository.</span></span> <span data-ttu-id="80e3a-107">Arquivos de definição de artefato consistem em JSON e expressões que você pode usar toospecify que você deseja tooinstall em uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="80e3a-107">Artifact definition files consist of JSON and expressions that you can use toospecify what you want tooinstall on a VM.</span></span> <span data-ttu-id="80e3a-108">Por exemplo, você pode definir o nome de saudação de um artefato, toorun de comando e parâmetros que são disponibilizados quando o comando hello está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="80e3a-108">For example, you can define hello name of an artifact, command toorun, and parameters that are made available when hello command is run.</span></span> <span data-ttu-id="80e3a-109">Você pode consultar os arquivos de script tooother no arquivo de definição de artefato Olá por nome.</span><span class="sxs-lookup"><span data-stu-id="80e3a-109">You can refer tooother script files within hello artifact definition file by name.</span></span>

## <a name="artifact-definition-file-format"></a><span data-ttu-id="80e3a-110">Formato do arquivo de definição de artefato</span><span class="sxs-lookup"><span data-stu-id="80e3a-110">Artifact definition file format</span></span>
<span data-ttu-id="80e3a-111">Olá, exemplo a seguir mostra seções Olá que formam a estrutura básica de saudação de um arquivo de definição:</span><span class="sxs-lookup"><span data-stu-id="80e3a-111">hello following example shows hello sections that make up hello basic structure of a definition file:</span></span>

    {
      "$schema": "https://raw.githubusercontent.com/Azure/azure-devtestlab/master/schemas/2016-11-28/dtlArtifacts.json",
      "title": "",
      "description": "",
      "iconUri": "",
      "targetOsType": "",
      "parameters": {
        "<parameterName>": {
          "type": "",
          "displayName": "",
          "description": ""
        }
      },
      "runCommand": {
        "commandToExecute": ""
      }
    }

| <span data-ttu-id="80e3a-112">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="80e3a-112">Element name</span></span> | <span data-ttu-id="80e3a-113">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="80e3a-113">Required?</span></span> | <span data-ttu-id="80e3a-114">Descrição</span><span class="sxs-lookup"><span data-stu-id="80e3a-114">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="80e3a-115">$schema</span><span class="sxs-lookup"><span data-stu-id="80e3a-115">$schema</span></span> |<span data-ttu-id="80e3a-116">Não</span><span class="sxs-lookup"><span data-stu-id="80e3a-116">No</span></span> |<span data-ttu-id="80e3a-117">Local do arquivo de esquema do JSON Olá ajuda no teste de validade Olá Olá do arquivo de definição.</span><span class="sxs-lookup"><span data-stu-id="80e3a-117">Location of hello JSON schema file that helps in testing hello validity of hello definition file.</span></span> |
| <span data-ttu-id="80e3a-118">título</span><span class="sxs-lookup"><span data-stu-id="80e3a-118">title</span></span> |<span data-ttu-id="80e3a-119">Sim</span><span class="sxs-lookup"><span data-stu-id="80e3a-119">Yes</span></span> |<span data-ttu-id="80e3a-120">Nome do artefato Olá exibido no laboratório de saudação.</span><span class="sxs-lookup"><span data-stu-id="80e3a-120">Name of hello artifact displayed in hello lab.</span></span> |
| <span data-ttu-id="80e3a-121">description</span><span class="sxs-lookup"><span data-stu-id="80e3a-121">description</span></span> |<span data-ttu-id="80e3a-122">Sim</span><span class="sxs-lookup"><span data-stu-id="80e3a-122">Yes</span></span> |<span data-ttu-id="80e3a-123">Descrição do artefato Olá exibido no laboratório de saudação.</span><span class="sxs-lookup"><span data-stu-id="80e3a-123">Description of hello artifact displayed in hello lab.</span></span> |
| <span data-ttu-id="80e3a-124">iconUri</span><span class="sxs-lookup"><span data-stu-id="80e3a-124">iconUri</span></span> |<span data-ttu-id="80e3a-125">Não</span><span class="sxs-lookup"><span data-stu-id="80e3a-125">No</span></span> |<span data-ttu-id="80e3a-126">URI do ícone de saudação exibido no laboratório de saudação.</span><span class="sxs-lookup"><span data-stu-id="80e3a-126">Uri of hello icon displayed in hello lab.</span></span> |
| <span data-ttu-id="80e3a-127">targetOsType</span><span class="sxs-lookup"><span data-stu-id="80e3a-127">targetOsType</span></span> |<span data-ttu-id="80e3a-128">Sim</span><span class="sxs-lookup"><span data-stu-id="80e3a-128">Yes</span></span> |<span data-ttu-id="80e3a-129">Sistema operacional de saudação VM onde o artefato está instalado.</span><span class="sxs-lookup"><span data-stu-id="80e3a-129">Operating system of hello VM where artifact is installed.</span></span> <span data-ttu-id="80e3a-130">As opções com suporte são: Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="80e3a-130">Supported options are: Windows and Linux.</span></span> |
| <span data-ttu-id="80e3a-131">parameters</span><span class="sxs-lookup"><span data-stu-id="80e3a-131">parameters</span></span> |<span data-ttu-id="80e3a-132">Não</span><span class="sxs-lookup"><span data-stu-id="80e3a-132">No</span></span> |<span data-ttu-id="80e3a-133">Valores fornecidos quando o comando de instalação do artefato é executado em um computador.</span><span class="sxs-lookup"><span data-stu-id="80e3a-133">Values that are provided when artifact install command is run on a machine.</span></span> <span data-ttu-id="80e3a-134">Isso ajuda a personalizar o artefato.</span><span class="sxs-lookup"><span data-stu-id="80e3a-134">This helps in customizing your artifact.</span></span> |
| <span data-ttu-id="80e3a-135">runCommand</span><span class="sxs-lookup"><span data-stu-id="80e3a-135">runCommand</span></span> |<span data-ttu-id="80e3a-136">Sim</span><span class="sxs-lookup"><span data-stu-id="80e3a-136">Yes</span></span> |<span data-ttu-id="80e3a-137">Comando de instalação do artefato executado em uma VM.</span><span class="sxs-lookup"><span data-stu-id="80e3a-137">Artifact install command that is executed on a VM.</span></span> |

### <a name="artifact-parameters"></a><span data-ttu-id="80e3a-138">Parâmetros do artefato</span><span class="sxs-lookup"><span data-stu-id="80e3a-138">Artifact parameters</span></span>
<span data-ttu-id="80e3a-139">Na seção de parâmetros de saudação do arquivo de definição de saudação, você deve especificar quais valores um usuário pode inserir durante a instalação de um artefato.</span><span class="sxs-lookup"><span data-stu-id="80e3a-139">In hello parameters section of hello definition file, you specify which values a user can input when installing an artifact.</span></span> <span data-ttu-id="80e3a-140">Você pode consultar os valores de toothese no comando de instalação de artefato de saudação.</span><span class="sxs-lookup"><span data-stu-id="80e3a-140">You can refer toothese values in hello artifact install command.</span></span>

<span data-ttu-id="80e3a-141">Você pode definir parâmetros com hello estrutura a seguir:</span><span class="sxs-lookup"><span data-stu-id="80e3a-141">You define parameters with hello following structure:</span></span>

    "parameters": {
        "<parameterName>": {
          "type": "<type-of-parameter-value>",
          "displayName": "<display-name-of-parameter>",
          "description": "<description-of-parameter>"
        }
      }

| <span data-ttu-id="80e3a-142">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="80e3a-142">Element name</span></span> | <span data-ttu-id="80e3a-143">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="80e3a-143">Required?</span></span> | <span data-ttu-id="80e3a-144">Descrição</span><span class="sxs-lookup"><span data-stu-id="80e3a-144">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="80e3a-145">type</span><span class="sxs-lookup"><span data-stu-id="80e3a-145">type</span></span> |<span data-ttu-id="80e3a-146">Sim</span><span class="sxs-lookup"><span data-stu-id="80e3a-146">Yes</span></span> |<span data-ttu-id="80e3a-147">Tipo do valor do parâmetro.</span><span class="sxs-lookup"><span data-stu-id="80e3a-147">Type of parameter value.</span></span> <span data-ttu-id="80e3a-148">Consulte Olá seguindo a lista de tipos permitida de saudação:</span><span class="sxs-lookup"><span data-stu-id="80e3a-148">See hello following list for hello allowed types:</span></span> |
| <span data-ttu-id="80e3a-149">displayName</span><span class="sxs-lookup"><span data-stu-id="80e3a-149">displayName</span></span> |<span data-ttu-id="80e3a-150">Sim</span><span class="sxs-lookup"><span data-stu-id="80e3a-150">Yes</span></span> |<span data-ttu-id="80e3a-151">Nome do parâmetro de saudação que é exibido tooa usuário laboratório hello.</span><span class="sxs-lookup"><span data-stu-id="80e3a-151">Name of hello parameter that is displayed tooa user in hello lab.</span></span> | |
| <span data-ttu-id="80e3a-152">description</span><span class="sxs-lookup"><span data-stu-id="80e3a-152">description</span></span> |<span data-ttu-id="80e3a-153">Sim</span><span class="sxs-lookup"><span data-stu-id="80e3a-153">Yes</span></span> |<span data-ttu-id="80e3a-154">Descrição do parâmetro hello que é exibido no laboratório de saudação.</span><span class="sxs-lookup"><span data-stu-id="80e3a-154">Description of hello parameter that is displayed in hello lab.</span></span> |

<span data-ttu-id="80e3a-155">Olá permitidos são de tipos:</span><span class="sxs-lookup"><span data-stu-id="80e3a-155">hello allowed types are:</span></span>

* <span data-ttu-id="80e3a-156">string - qualquer cadeia de caracteres JSON válida</span><span class="sxs-lookup"><span data-stu-id="80e3a-156">string – any valid JSON string</span></span>
* <span data-ttu-id="80e3a-157">int - qualquer inteiro JSON válido</span><span class="sxs-lookup"><span data-stu-id="80e3a-157">int – any valid JSON integer</span></span>
* <span data-ttu-id="80e3a-158">bool - qualquer booliano JSON válido</span><span class="sxs-lookup"><span data-stu-id="80e3a-158">bool – any valid JSON Boolean</span></span>
* <span data-ttu-id="80e3a-159">array - qualquer matriz JSON válida</span><span class="sxs-lookup"><span data-stu-id="80e3a-159">array – any valid JSON array</span></span>

## <a name="artifact-expressions-and-functions"></a><span data-ttu-id="80e3a-160">Expressões e funções de artefatos</span><span class="sxs-lookup"><span data-stu-id="80e3a-160">Artifact expressions and functions</span></span>
<span data-ttu-id="80e3a-161">Você pode usar a expressão e comando de instalação de artefato de saudação do tooconstruct de funções.</span><span class="sxs-lookup"><span data-stu-id="80e3a-161">You can use expression and functions tooconstruct hello artifact install command.</span></span>
<span data-ttu-id="80e3a-162">Expressões são colocadas entre colchetes ([e]) e são avaliadas quando o artefato de saudação é instalado.</span><span class="sxs-lookup"><span data-stu-id="80e3a-162">Expressions are enclosed with brackets ([ and ]), and are evaluated when hello artifact is installed.</span></span> <span data-ttu-id="80e3a-163">As expressões podem aparecer em qualquer lugar em um valor de cadeia de caracteres JSON e sempre retornam outro valor JSON.</span><span class="sxs-lookup"><span data-stu-id="80e3a-163">Expressions can appear anywhere in a JSON string value and always return another JSON value.</span></span> <span data-ttu-id="80e3a-164">Se você precisa toouse uma cadeia de caracteres literal que começa com um colchete [, você deve usar dois colchetes [[.</span><span class="sxs-lookup"><span data-stu-id="80e3a-164">If you need toouse a literal string that starts with a bracket [, you must use two brackets [[.</span></span>
<span data-ttu-id="80e3a-165">Normalmente, você deve usar expressões com funções tooconstruct um valor.</span><span class="sxs-lookup"><span data-stu-id="80e3a-165">Typically, you use expressions with functions tooconstruct a value.</span></span> <span data-ttu-id="80e3a-166">Assim como no JavaScript, as chamadas de função são formatadas como functionName(arg1,arg2,arg3).</span><span class="sxs-lookup"><span data-stu-id="80e3a-166">Just like in JavaScript, function calls are formatted as functionName(arg1,arg2,arg3).</span></span>

<span data-ttu-id="80e3a-167">Olá lista a seguir mostra as funções comuns:</span><span class="sxs-lookup"><span data-stu-id="80e3a-167">hello following list shows common functions:</span></span>

* <span data-ttu-id="80e3a-168">Parameters(ParameterName) - retorna um valor de parâmetro que é fornecido quando o comando de artefato de saudação é executado.</span><span class="sxs-lookup"><span data-stu-id="80e3a-168">parameters(parameterName) - Returns a parameter value that is provided when hello artifact command is run.</span></span>
* <span data-ttu-id="80e3a-169">concat(arg1,arg2,arg3, …..) -     Combina diversos valores da cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="80e3a-169">concat(arg1,arg2,arg3, …..) -     Combines multiple string values.</span></span> <span data-ttu-id="80e3a-170">Essa função pode conter qualquer número de argumentos.</span><span class="sxs-lookup"><span data-stu-id="80e3a-170">This function can take any number of arguments.</span></span>

<span data-ttu-id="80e3a-171">Olá mostrado no exemplo a seguir como toouse expressões e funções tooconstruct um valor:</span><span class="sxs-lookup"><span data-stu-id="80e3a-171">hello following example shows how toouse expression and functions tooconstruct a value:</span></span>

    runCommand": {
         "commandToExecute": "[concat('powershell.exe -ExecutionPolicy bypass \"& ./startChocolatey.ps1'
    , ' -RawPackagesList ', parameters('packages')
    , ' -Username ', parameters('installUsername')
    , ' -Password ', parameters('installPassword'))]"
    }

## <a name="create-a-custom-artifact"></a><span data-ttu-id="80e3a-172">Criar um artefato personalizado</span><span class="sxs-lookup"><span data-stu-id="80e3a-172">Create a custom artifact</span></span>
<span data-ttu-id="80e3a-173">Crie seu artefato personalizado executando estas etapas:</span><span class="sxs-lookup"><span data-stu-id="80e3a-173">Create your custom artifact by following these steps:</span></span>

1. <span data-ttu-id="80e3a-174">Instalar um editor de JSON - é necessário um toowork do editor de JSON com arquivos de definição de artefato.</span><span class="sxs-lookup"><span data-stu-id="80e3a-174">Install a JSON editor - You need a JSON editor toowork with artifact definition files.</span></span> <span data-ttu-id="80e3a-175">Recomendamos o uso do [Visual Studio Code](https://code.visualstudio.com/), que está disponível para Windows, Linux e OS X.</span><span class="sxs-lookup"><span data-stu-id="80e3a-175">We recommend using [Visual Studio Code](https://code.visualstudio.com/), which is available for Windows, Linux and OS X.</span></span>
2. <span data-ttu-id="80e3a-176">Get artifactfile.json um exemplo - Check-out artefatos Olá criadas pela equipe do Azure DevTest Labs em nosso [repositório GitHub](https://github.com/Azure/azure-devtestlab), em que você criou uma biblioteca avançada de artefatos de ajudarão-lo a criar seus próprios artefatos.</span><span class="sxs-lookup"><span data-stu-id="80e3a-176">Get a sample artifactfile.json - Check out hello artifacts created by Azure DevTest Labs team at our [GitHub repository](https://github.com/Azure/azure-devtestlab), where we have created a rich library of artifacts that help you create your own artifacts.</span></span> <span data-ttu-id="80e3a-177">Baixar um arquivo de definição de artefato e fazer alterações tooit toocreate seus próprios artefatos.</span><span class="sxs-lookup"><span data-stu-id="80e3a-177">Download an artifact definition file and make changes tooit toocreate your own artifacts.</span></span>
3. <span data-ttu-id="80e3a-178">Fazer uso do IntelliSense - aproveite IntelliSense toosee elementos válidos que podem ser usado tooconstruct um arquivo de definição de artefato.</span><span class="sxs-lookup"><span data-stu-id="80e3a-178">Make use of IntelliSense - Leverage IntelliSense toosee valid elements that can be used tooconstruct an artifact definition file.</span></span> <span data-ttu-id="80e3a-179">Você também pode ver Olá diferentes opções para valores de um elemento.</span><span class="sxs-lookup"><span data-stu-id="80e3a-179">You can also see hello different options for values of an element.</span></span> <span data-ttu-id="80e3a-180">Por exemplo, Mostrar IntelliSense Olá duas opções do Windows ou Linux ao editar Olá **targetOsType** elemento.</span><span class="sxs-lookup"><span data-stu-id="80e3a-180">For example, IntelliSense show you hello two choices of Windows or Linux when editing hello **targetOsType** element.</span></span>
4. <span data-ttu-id="80e3a-181">Artefato de saudação do repositório em um [repositório git](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="80e3a-181">Store hello artifact in a [git repository](devtest-lab-add-artifact-repo.md).</span></span>
   
   1. <span data-ttu-id="80e3a-182">Crie um diretório separado para cada artefato onde nome do diretório Olá é Olá mesmo como o nome do artefato hello.</span><span class="sxs-lookup"><span data-stu-id="80e3a-182">Create a separate directory for each artifact where hello directory name is hello same as hello artifact name.</span></span>
   2. <span data-ttu-id="80e3a-183">Armazenar o arquivo de definição de artefato de saudação (artifactfile.json) no diretório de saudação criado por você.</span><span class="sxs-lookup"><span data-stu-id="80e3a-183">Store hello artifact definition file (artifactfile.json) in hello directory you created.</span></span>
   3. <span data-ttu-id="80e3a-184">Comando de instalação de scripts de saudação de repositório que são referenciados de artefato de saudação.</span><span class="sxs-lookup"><span data-stu-id="80e3a-184">Store hello scripts that are referenced from hello artifact install command.</span></span>
      
      <span data-ttu-id="80e3a-185">Veja um exemplo de como uma pasta de artefatos pode ser:</span><span class="sxs-lookup"><span data-stu-id="80e3a-185">Here is an example of how an artifact folder might look:</span></span>
      
      ![Exemplo de repositório git de artefatos](./media/devtest-lab-artifact-author/git-repo.png)
5. <span data-ttu-id="80e3a-187">Adicionar o laboratório de toohello de repositório de artefatos Olá - consulte o artigo toohello, [adicionar um repositório Git para modelos e artefatos](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="80e3a-187">Add hello artifacts repository toohello lab - Refer toohello article, [Add a Git repository for artifacts and templates](devtest-lab-add-artifact-repo.md).</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-articles"></a><span data-ttu-id="80e3a-188">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="80e3a-188">Related articles</span></span>
* [<span data-ttu-id="80e3a-189">Como falhas de artefato de toodiagnose em DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="80e3a-189">How toodiagnose artifact failures in DevTest Labs</span></span>](devtest-lab-troubleshoot-artifact-failure.md)
* [<span data-ttu-id="80e3a-190">Ingressar em um domínio de AD usando um modelo do Gerenciador de recursos no Azure DevTest Labs de tooexisting VM</span><span class="sxs-lookup"><span data-stu-id="80e3a-190">Join a VM tooexisting AD Domain using a resource manager template in Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a><span data-ttu-id="80e3a-191">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="80e3a-191">Next steps</span></span>
* <span data-ttu-id="80e3a-192">Saiba como muito[adicionar um laboratório de tooa do repositório de artefato Git](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="80e3a-192">Learn how too[add a Git artifact repository tooa lab](devtest-lab-add-artifact-repo.md).</span></span>

