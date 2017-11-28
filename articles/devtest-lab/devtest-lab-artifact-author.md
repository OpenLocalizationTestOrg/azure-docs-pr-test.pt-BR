---
title: Criar artefatos personalizados para sua VM do DevTest Labs | Microsoft Docs
description: "Aprenda a criar seus próprios artefatos para uso com Laboratórios de Desenvolvimento/Teste"
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
ms.openlocfilehash: 2412033daa1d97860dd9f380178622b1ddc590c0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-custom-artifacts-for-your-devtest-labs-vm"></a><span data-ttu-id="a4ee5-103">Criar artefatos personalizados para suas VM dos Laboratórios de Desenvolvimento/Teste.</span><span class="sxs-lookup"><span data-stu-id="a4ee5-103">Create custom artifacts for your DevTest Labs VM</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/how-to-author-custom-artifacts/player]
> 
> 

## <a name="overview"></a><span data-ttu-id="a4ee5-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="a4ee5-104">Overview</span></span>
<span data-ttu-id="a4ee5-105">**Artefatos** são usados para implantar e configurar seu aplicativo após o provisionamento de uma VM.</span><span class="sxs-lookup"><span data-stu-id="a4ee5-105">**Artifacts** are used to deploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="a4ee5-106">Um artefato é composto por um arquivo de definição de artefato e outros arquivos de script que são armazenados em uma pasta em um repositório git.</span><span class="sxs-lookup"><span data-stu-id="a4ee5-106">An artifact consists of an artifact definition file and other script files that are stored in a folder in a git repository.</span></span> <span data-ttu-id="a4ee5-107">Arquivos de definição de artefato são formados por JSON e expressões que você pode usar para especificar o que você deseja instalar em uma VM.</span><span class="sxs-lookup"><span data-stu-id="a4ee5-107">Artifact definition files consist of JSON and expressions that you can use to specify what you want to install on a VM.</span></span> <span data-ttu-id="a4ee5-108">Por exemplo, você pode definir o nome de um artefato, comando a ser executado e parâmetros disponibilizados quando o comando é executado.</span><span class="sxs-lookup"><span data-stu-id="a4ee5-108">For example, you can define the name of an artifact, command to run, and parameters that are made available when the command is run.</span></span> <span data-ttu-id="a4ee5-109">Você pode consultar por nome outros arquivos de script dentro do arquivo de definição de artefato.</span><span class="sxs-lookup"><span data-stu-id="a4ee5-109">You can refer to other script files within the artifact definition file by name.</span></span>

## <a name="artifact-definition-file-format"></a><span data-ttu-id="a4ee5-110">Formato do arquivo de definição de artefato</span><span class="sxs-lookup"><span data-stu-id="a4ee5-110">Artifact definition file format</span></span>
<span data-ttu-id="a4ee5-111">O exemplo a seguir mostra as seções que compõem a estrutura básica de um arquivo de definição:</span><span class="sxs-lookup"><span data-stu-id="a4ee5-111">The following example shows the sections that make up the basic structure of a definition file:</span></span>

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

| <span data-ttu-id="a4ee5-112">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="a4ee5-112">Element name</span></span> | <span data-ttu-id="a4ee5-113">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="a4ee5-113">Required?</span></span> | <span data-ttu-id="a4ee5-114">Descrição</span><span class="sxs-lookup"><span data-stu-id="a4ee5-114">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a4ee5-115">$schema</span><span class="sxs-lookup"><span data-stu-id="a4ee5-115">$schema</span></span> |<span data-ttu-id="a4ee5-116">Não</span><span class="sxs-lookup"><span data-stu-id="a4ee5-116">No</span></span> |<span data-ttu-id="a4ee5-117">Local do arquivo de esquema JSON que ajuda a testar a validade do arquivo de definição.</span><span class="sxs-lookup"><span data-stu-id="a4ee5-117">Location of the JSON schema file that helps in testing the validity of the definition file.</span></span> |
| <span data-ttu-id="a4ee5-118">título</span><span class="sxs-lookup"><span data-stu-id="a4ee5-118">title</span></span> |<span data-ttu-id="a4ee5-119">Sim</span><span class="sxs-lookup"><span data-stu-id="a4ee5-119">Yes</span></span> |<span data-ttu-id="a4ee5-120">Nome do artefato exibido no laboratório.</span><span class="sxs-lookup"><span data-stu-id="a4ee5-120">Name of the artifact displayed in the lab.</span></span> |
| <span data-ttu-id="a4ee5-121">Descrição</span><span class="sxs-lookup"><span data-stu-id="a4ee5-121">description</span></span> |<span data-ttu-id="a4ee5-122">Sim</span><span class="sxs-lookup"><span data-stu-id="a4ee5-122">Yes</span></span> |<span data-ttu-id="a4ee5-123">Descrição do artefato exibido no laboratório.</span><span class="sxs-lookup"><span data-stu-id="a4ee5-123">Description of the artifact displayed in the lab.</span></span> |
| <span data-ttu-id="a4ee5-124">iconUri</span><span class="sxs-lookup"><span data-stu-id="a4ee5-124">iconUri</span></span> |<span data-ttu-id="a4ee5-125">Não</span><span class="sxs-lookup"><span data-stu-id="a4ee5-125">No</span></span> |<span data-ttu-id="a4ee5-126">URI do ícone exibido no laboratório.</span><span class="sxs-lookup"><span data-stu-id="a4ee5-126">Uri of the icon displayed in the lab.</span></span> |
| <span data-ttu-id="a4ee5-127">targetOsType</span><span class="sxs-lookup"><span data-stu-id="a4ee5-127">targetOsType</span></span> |<span data-ttu-id="a4ee5-128">Sim</span><span class="sxs-lookup"><span data-stu-id="a4ee5-128">Yes</span></span> |<span data-ttu-id="a4ee5-129">Sistema operacional da VM na qual o artefato está instalado.</span><span class="sxs-lookup"><span data-stu-id="a4ee5-129">Operating system of the VM where artifact is installed.</span></span> <span data-ttu-id="a4ee5-130">As opções com suporte são: Windows e Linux.</span><span class="sxs-lookup"><span data-stu-id="a4ee5-130">Supported options are: Windows and Linux.</span></span> |
| <span data-ttu-id="a4ee5-131">parameters</span><span class="sxs-lookup"><span data-stu-id="a4ee5-131">parameters</span></span> |<span data-ttu-id="a4ee5-132">Não</span><span class="sxs-lookup"><span data-stu-id="a4ee5-132">No</span></span> |<span data-ttu-id="a4ee5-133">Valores fornecidos quando o comando de instalação do artefato é executado em um computador.</span><span class="sxs-lookup"><span data-stu-id="a4ee5-133">Values that are provided when artifact install command is run on a machine.</span></span> <span data-ttu-id="a4ee5-134">Isso ajuda a personalizar o artefato.</span><span class="sxs-lookup"><span data-stu-id="a4ee5-134">This helps in customizing your artifact.</span></span> |
| <span data-ttu-id="a4ee5-135">runCommand</span><span class="sxs-lookup"><span data-stu-id="a4ee5-135">runCommand</span></span> |<span data-ttu-id="a4ee5-136">Sim</span><span class="sxs-lookup"><span data-stu-id="a4ee5-136">Yes</span></span> |<span data-ttu-id="a4ee5-137">Comando de instalação do artefato executado em uma VM.</span><span class="sxs-lookup"><span data-stu-id="a4ee5-137">Artifact install command that is executed on a VM.</span></span> |

### <a name="artifact-parameters"></a><span data-ttu-id="a4ee5-138">Parâmetros do artefato</span><span class="sxs-lookup"><span data-stu-id="a4ee5-138">Artifact parameters</span></span>
<span data-ttu-id="a4ee5-139">Na seção de parâmetros do arquivo de definição, especifique os valores que um usuário pode inserir ao instalar um artefato.</span><span class="sxs-lookup"><span data-stu-id="a4ee5-139">In the parameters section of the definition file, you specify which values a user can input when installing an artifact.</span></span> <span data-ttu-id="a4ee5-140">Você pode consultar esses valores no comando de instalação do artefato.</span><span class="sxs-lookup"><span data-stu-id="a4ee5-140">You can refer to these values in the artifact install command.</span></span>

<span data-ttu-id="a4ee5-141">Você define parâmetros com a seguinte estrutura:</span><span class="sxs-lookup"><span data-stu-id="a4ee5-141">You define parameters with the following structure:</span></span>

    "parameters": {
        "<parameterName>": {
          "type": "<type-of-parameter-value>",
          "displayName": "<display-name-of-parameter>",
          "description": "<description-of-parameter>"
        }
      }

| <span data-ttu-id="a4ee5-142">Nome do elemento</span><span class="sxs-lookup"><span data-stu-id="a4ee5-142">Element name</span></span> | <span data-ttu-id="a4ee5-143">Obrigatório?</span><span class="sxs-lookup"><span data-stu-id="a4ee5-143">Required?</span></span> | <span data-ttu-id="a4ee5-144">Descrição</span><span class="sxs-lookup"><span data-stu-id="a4ee5-144">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a4ee5-145">type</span><span class="sxs-lookup"><span data-stu-id="a4ee5-145">type</span></span> |<span data-ttu-id="a4ee5-146">Sim</span><span class="sxs-lookup"><span data-stu-id="a4ee5-146">Yes</span></span> |<span data-ttu-id="a4ee5-147">Tipo do valor do parâmetro.</span><span class="sxs-lookup"><span data-stu-id="a4ee5-147">Type of parameter value.</span></span> <span data-ttu-id="a4ee5-148">Veja a lista dos tipos permitidos:</span><span class="sxs-lookup"><span data-stu-id="a4ee5-148">See the following list for the allowed types:</span></span> |
| <span data-ttu-id="a4ee5-149">displayName</span><span class="sxs-lookup"><span data-stu-id="a4ee5-149">displayName</span></span> |<span data-ttu-id="a4ee5-150">Sim</span><span class="sxs-lookup"><span data-stu-id="a4ee5-150">Yes</span></span> |<span data-ttu-id="a4ee5-151">Nome do parâmetro exibido para um usuário no laboratório.</span><span class="sxs-lookup"><span data-stu-id="a4ee5-151">Name of the parameter that is displayed to a user in the lab.</span></span> | |
| <span data-ttu-id="a4ee5-152">Descrição</span><span class="sxs-lookup"><span data-stu-id="a4ee5-152">description</span></span> |<span data-ttu-id="a4ee5-153">Sim</span><span class="sxs-lookup"><span data-stu-id="a4ee5-153">Yes</span></span> |<span data-ttu-id="a4ee5-154">Descrição do parâmetro exibido no laboratório.</span><span class="sxs-lookup"><span data-stu-id="a4ee5-154">Description of the parameter that is displayed in the lab.</span></span> |

<span data-ttu-id="a4ee5-155">Os tipos permitidos são:</span><span class="sxs-lookup"><span data-stu-id="a4ee5-155">The allowed types are:</span></span>

* <span data-ttu-id="a4ee5-156">string - qualquer cadeia de caracteres JSON válida</span><span class="sxs-lookup"><span data-stu-id="a4ee5-156">string – any valid JSON string</span></span>
* <span data-ttu-id="a4ee5-157">int - qualquer inteiro JSON válido</span><span class="sxs-lookup"><span data-stu-id="a4ee5-157">int – any valid JSON integer</span></span>
* <span data-ttu-id="a4ee5-158">bool - qualquer booliano JSON válido</span><span class="sxs-lookup"><span data-stu-id="a4ee5-158">bool – any valid JSON Boolean</span></span>
* <span data-ttu-id="a4ee5-159">array - qualquer matriz JSON válida</span><span class="sxs-lookup"><span data-stu-id="a4ee5-159">array – any valid JSON array</span></span>

## <a name="artifact-expressions-and-functions"></a><span data-ttu-id="a4ee5-160">Expressões e funções de artefatos</span><span class="sxs-lookup"><span data-stu-id="a4ee5-160">Artifact expressions and functions</span></span>
<span data-ttu-id="a4ee5-161">Você pode usar expressões e funções para construir o comando de instalação do artefato.</span><span class="sxs-lookup"><span data-stu-id="a4ee5-161">You can use expression and functions to construct the artifact install command.</span></span>
<span data-ttu-id="a4ee5-162">As expressões são colocadas entre colchetes ([ e ]) e avaliadas quando o artefato é instalado.</span><span class="sxs-lookup"><span data-stu-id="a4ee5-162">Expressions are enclosed with brackets ([ and ]), and are evaluated when the artifact is installed.</span></span> <span data-ttu-id="a4ee5-163">As expressões podem aparecer em qualquer lugar em um valor de cadeia de caracteres JSON e sempre retornam outro valor JSON.</span><span class="sxs-lookup"><span data-stu-id="a4ee5-163">Expressions can appear anywhere in a JSON string value and always return another JSON value.</span></span> <span data-ttu-id="a4ee5-164">Se precisar usar uma cadeia de caracteres literal que comece com um colchete [, você deverá usar dois colchetes [[.</span><span class="sxs-lookup"><span data-stu-id="a4ee5-164">If you need to use a literal string that starts with a bracket [, you must use two brackets [[.</span></span>
<span data-ttu-id="a4ee5-165">Normalmente, você usa expressões com funções para construir um valor.</span><span class="sxs-lookup"><span data-stu-id="a4ee5-165">Typically, you use expressions with functions to construct a value.</span></span> <span data-ttu-id="a4ee5-166">Assim como no JavaScript, as chamadas de função são formatadas como functionName(arg1,arg2,arg3).</span><span class="sxs-lookup"><span data-stu-id="a4ee5-166">Just like in JavaScript, function calls are formatted as functionName(arg1,arg2,arg3).</span></span>

<span data-ttu-id="a4ee5-167">A lista a seguir mostra funções comuns:</span><span class="sxs-lookup"><span data-stu-id="a4ee5-167">The following list shows common functions:</span></span>

* <span data-ttu-id="a4ee5-168">Parameters(ParameterName): Retorna um valor de parâmetro fornecido quando o comando do artefato é executado.</span><span class="sxs-lookup"><span data-stu-id="a4ee5-168">parameters(parameterName) - Returns a parameter value that is provided when the artifact command is run.</span></span>
* <span data-ttu-id="a4ee5-169">concat(arg1,arg2,arg3, …..) -     Combina diversos valores da cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="a4ee5-169">concat(arg1,arg2,arg3, …..) -     Combines multiple string values.</span></span> <span data-ttu-id="a4ee5-170">Essa função pode conter qualquer número de argumentos.</span><span class="sxs-lookup"><span data-stu-id="a4ee5-170">This function can take any number of arguments.</span></span>

<span data-ttu-id="a4ee5-171">O exemplo a seguir mostra como usar expressões e funções para construir um valor:</span><span class="sxs-lookup"><span data-stu-id="a4ee5-171">The following example shows how to use expression and functions to construct a value:</span></span>

    runCommand": {
         "commandToExecute": "[concat('powershell.exe -ExecutionPolicy bypass \"& ./startChocolatey.ps1'
    , ' -RawPackagesList ', parameters('packages')
    , ' -Username ', parameters('installUsername')
    , ' -Password ', parameters('installPassword'))]"
    }

## <a name="create-a-custom-artifact"></a><span data-ttu-id="a4ee5-172">Criar um artefato personalizado</span><span class="sxs-lookup"><span data-stu-id="a4ee5-172">Create a custom artifact</span></span>
<span data-ttu-id="a4ee5-173">Crie seu artefato personalizado executando estas etapas:</span><span class="sxs-lookup"><span data-stu-id="a4ee5-173">Create your custom artifact by following these steps:</span></span>

1. <span data-ttu-id="a4ee5-174">Instalar um editor de JSON: você precisa de um editor de JSON para trabalhar com arquivos de definição de artefato.</span><span class="sxs-lookup"><span data-stu-id="a4ee5-174">Install a JSON editor - You need a JSON editor to work with artifact definition files.</span></span> <span data-ttu-id="a4ee5-175">Recomendamos o uso do [Visual Studio Code](https://code.visualstudio.com/), que está disponível para Windows, Linux e OS X.</span><span class="sxs-lookup"><span data-stu-id="a4ee5-175">We recommend using [Visual Studio Code](https://code.visualstudio.com/), which is available for Windows, Linux and OS X.</span></span>
2. <span data-ttu-id="a4ee5-176">Obter um exemplo de artifactfile.json: verifique os artefatos criados pela equipe dos Laboratórios de Desenvolvimento/Teste do Azure em nosso [repositório GitHub](https://github.com/Azure/azure-devtestlab) , no qual criamos uma vasta biblioteca de artefatos que ajudarão você a criar seus próprios artefatos.</span><span class="sxs-lookup"><span data-stu-id="a4ee5-176">Get a sample artifactfile.json - Check out the artifacts created by Azure DevTest Labs team at our [GitHub repository](https://github.com/Azure/azure-devtestlab), where we have created a rich library of artifacts that help you create your own artifacts.</span></span> <span data-ttu-id="a4ee5-177">Baixe um arquivo de definição de artefato e faça as alterações nele para criar seus próprios artefatos.</span><span class="sxs-lookup"><span data-stu-id="a4ee5-177">Download an artifact definition file and make changes to it to create your own artifacts.</span></span>
3. <span data-ttu-id="a4ee5-178">Usar o IntelliSense: aproveite o IntelliSense para ver os elementos válidos que podem ser usados para construir um arquivo de definição de artefato.</span><span class="sxs-lookup"><span data-stu-id="a4ee5-178">Make use of IntelliSense - Leverage IntelliSense to see valid elements that can be used to construct an artifact definition file.</span></span> <span data-ttu-id="a4ee5-179">Você também pode ver as opções diferentes de valores para um elemento.</span><span class="sxs-lookup"><span data-stu-id="a4ee5-179">You can also see the different options for values of an element.</span></span> <span data-ttu-id="a4ee5-180">Por exemplo, o IntelliSense mostra a você as duas opções, Windows ou Linux, ao editar o elemento **targetOsType** .</span><span class="sxs-lookup"><span data-stu-id="a4ee5-180">For example, IntelliSense show you the two choices of Windows or Linux when editing the **targetOsType** element.</span></span>
4. <span data-ttu-id="a4ee5-181">Armazenar o artefato em um [repositório git](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="a4ee5-181">Store the artifact in a [git repository](devtest-lab-add-artifact-repo.md).</span></span>
   
   1. <span data-ttu-id="a4ee5-182">Crie um diretório separado para cada artefato, em que o nome do diretório é igual ao nome do artefato.</span><span class="sxs-lookup"><span data-stu-id="a4ee5-182">Create a separate directory for each artifact where the directory name is the same as the artifact name.</span></span>
   2. <span data-ttu-id="a4ee5-183">Armazene o arquivo de definição de artefato (artifactfile.json) no diretório que você criou.</span><span class="sxs-lookup"><span data-stu-id="a4ee5-183">Store the artifact definition file (artifactfile.json) in the directory you created.</span></span>
   3. <span data-ttu-id="a4ee5-184">Armazene os scripts referenciados pelo comando de instalação de artefato.</span><span class="sxs-lookup"><span data-stu-id="a4ee5-184">Store the scripts that are referenced from the artifact install command.</span></span>
      
      <span data-ttu-id="a4ee5-185">Veja um exemplo de como uma pasta de artefatos pode ser:</span><span class="sxs-lookup"><span data-stu-id="a4ee5-185">Here is an example of how an artifact folder might look:</span></span>
      
      ![Exemplo de repositório git de artefatos](./media/devtest-lab-artifact-author/git-repo.png)
5. <span data-ttu-id="a4ee5-187">Adicione o repositório de artefatos ao laboratório: consulte o artigo [Adicionar um repositório Git para artefatos e modelos](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="a4ee5-187">Add the artifacts repository to the lab - Refer to the article, [Add a Git repository for artifacts and templates](devtest-lab-add-artifact-repo.md).</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-articles"></a><span data-ttu-id="a4ee5-188">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="a4ee5-188">Related articles</span></span>
* [<span data-ttu-id="a4ee5-189">Como diagnosticar falhas de artefato em DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="a4ee5-189">How to diagnose artifact failures in DevTest Labs</span></span>](devtest-lab-troubleshoot-artifact-failure.md)
* [<span data-ttu-id="a4ee5-190">Ingressar uma VM em um Domínio do AD existente usando um modelo do Resource Manager no Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="a4ee5-190">Join a VM to existing AD Domain using a resource manager template in Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a><span data-ttu-id="a4ee5-191">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a4ee5-191">Next steps</span></span>
* <span data-ttu-id="a4ee5-192">Saiba como [adicionar um repositório de artefatos Git a um laboratório](devtest-lab-add-artifact-repo.md).</span><span class="sxs-lookup"><span data-stu-id="a4ee5-192">Learn how to [add a Git artifact repository to a lab](devtest-lab-add-artifact-repo.md).</span></span>

