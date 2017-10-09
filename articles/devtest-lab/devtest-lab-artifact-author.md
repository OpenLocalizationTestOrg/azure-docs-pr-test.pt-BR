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
# <a name="create-custom-artifacts-for-your-devtest-labs-vm"></a>Criar artefatos personalizados para suas VM dos Laboratórios de Desenvolvimento/Teste.
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/how-to-author-custom-artifacts/player]
> 
> 

## <a name="overview"></a>Visão geral
**Artefatos** são usado toodeploy e configurar seu aplicativo depois que uma VM é provisionada. Um artefato é composto por um arquivo de definição de artefato e outros arquivos de script que são armazenados em uma pasta em um repositório git. Arquivos de definição de artefato consistem em JSON e expressões que você pode usar toospecify que você deseja tooinstall em uma máquina virtual. Por exemplo, você pode definir o nome de saudação de um artefato, toorun de comando e parâmetros que são disponibilizados quando o comando hello está sendo executado. Você pode consultar os arquivos de script tooother no arquivo de definição de artefato Olá por nome.

## <a name="artifact-definition-file-format"></a>Formato do arquivo de definição de artefato
Olá, exemplo a seguir mostra seções Olá que formam a estrutura básica de saudação de um arquivo de definição:

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

| Nome do elemento | Obrigatório? | Descrição |
| --- | --- | --- |
| $schema |Não |Local do arquivo de esquema do JSON Olá ajuda no teste de validade Olá Olá do arquivo de definição. |
| título |Sim |Nome do artefato Olá exibido no laboratório de saudação. |
| description |Sim |Descrição do artefato Olá exibido no laboratório de saudação. |
| iconUri |Não |URI do ícone de saudação exibido no laboratório de saudação. |
| targetOsType |Sim |Sistema operacional de saudação VM onde o artefato está instalado. As opções com suporte são: Windows e Linux. |
| parameters |Não |Valores fornecidos quando o comando de instalação do artefato é executado em um computador. Isso ajuda a personalizar o artefato. |
| runCommand |Sim |Comando de instalação do artefato executado em uma VM. |

### <a name="artifact-parameters"></a>Parâmetros do artefato
Na seção de parâmetros de saudação do arquivo de definição de saudação, você deve especificar quais valores um usuário pode inserir durante a instalação de um artefato. Você pode consultar os valores de toothese no comando de instalação de artefato de saudação.

Você pode definir parâmetros com hello estrutura a seguir:

    "parameters": {
        "<parameterName>": {
          "type": "<type-of-parameter-value>",
          "displayName": "<display-name-of-parameter>",
          "description": "<description-of-parameter>"
        }
      }

| Nome do elemento | Obrigatório? | Descrição |
| --- | --- | --- |
| type |Sim |Tipo do valor do parâmetro. Consulte Olá seguindo a lista de tipos permitida de saudação: |
| displayName |Sim |Nome do parâmetro de saudação que é exibido tooa usuário laboratório hello. | |
| description |Sim |Descrição do parâmetro hello que é exibido no laboratório de saudação. |

Olá permitidos são de tipos:

* string - qualquer cadeia de caracteres JSON válida
* int - qualquer inteiro JSON válido
* bool - qualquer booliano JSON válido
* array - qualquer matriz JSON válida

## <a name="artifact-expressions-and-functions"></a>Expressões e funções de artefatos
Você pode usar a expressão e comando de instalação de artefato de saudação do tooconstruct de funções.
Expressões são colocadas entre colchetes ([e]) e são avaliadas quando o artefato de saudação é instalado. As expressões podem aparecer em qualquer lugar em um valor de cadeia de caracteres JSON e sempre retornam outro valor JSON. Se você precisa toouse uma cadeia de caracteres literal que começa com um colchete [, você deve usar dois colchetes [[.
Normalmente, você deve usar expressões com funções tooconstruct um valor. Assim como no JavaScript, as chamadas de função são formatadas como functionName(arg1,arg2,arg3).

Olá lista a seguir mostra as funções comuns:

* Parameters(ParameterName) - retorna um valor de parâmetro que é fornecido quando o comando de artefato de saudação é executado.
* concat(arg1,arg2,arg3, …..) -     Combina diversos valores da cadeia de caracteres. Essa função pode conter qualquer número de argumentos.

Olá mostrado no exemplo a seguir como toouse expressões e funções tooconstruct um valor:

    runCommand": {
         "commandToExecute": "[concat('powershell.exe -ExecutionPolicy bypass \"& ./startChocolatey.ps1'
    , ' -RawPackagesList ', parameters('packages')
    , ' -Username ', parameters('installUsername')
    , ' -Password ', parameters('installPassword'))]"
    }

## <a name="create-a-custom-artifact"></a>Criar um artefato personalizado
Crie seu artefato personalizado executando estas etapas:

1. Instalar um editor de JSON - é necessário um toowork do editor de JSON com arquivos de definição de artefato. Recomendamos o uso do [Visual Studio Code](https://code.visualstudio.com/), que está disponível para Windows, Linux e OS X.
2. Get artifactfile.json um exemplo - Check-out artefatos Olá criadas pela equipe do Azure DevTest Labs em nosso [repositório GitHub](https://github.com/Azure/azure-devtestlab), em que você criou uma biblioteca avançada de artefatos de ajudarão-lo a criar seus próprios artefatos. Baixar um arquivo de definição de artefato e fazer alterações tooit toocreate seus próprios artefatos.
3. Fazer uso do IntelliSense - aproveite IntelliSense toosee elementos válidos que podem ser usado tooconstruct um arquivo de definição de artefato. Você também pode ver Olá diferentes opções para valores de um elemento. Por exemplo, Mostrar IntelliSense Olá duas opções do Windows ou Linux ao editar Olá **targetOsType** elemento.
4. Artefato de saudação do repositório em um [repositório git](devtest-lab-add-artifact-repo.md).
   
   1. Crie um diretório separado para cada artefato onde nome do diretório Olá é Olá mesmo como o nome do artefato hello.
   2. Armazenar o arquivo de definição de artefato de saudação (artifactfile.json) no diretório de saudação criado por você.
   3. Comando de instalação de scripts de saudação de repositório que são referenciados de artefato de saudação.
      
      Veja um exemplo de como uma pasta de artefatos pode ser:
      
      ![Exemplo de repositório git de artefatos](./media/devtest-lab-artifact-author/git-repo.png)
5. Adicionar o laboratório de toohello de repositório de artefatos Olá - consulte o artigo toohello, [adicionar um repositório Git para modelos e artefatos](devtest-lab-add-artifact-repo.md).

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-articles"></a>Artigos relacionados
* [Como falhas de artefato de toodiagnose em DevTest Labs](devtest-lab-troubleshoot-artifact-failure.md)
* [Ingressar em um domínio de AD usando um modelo do Gerenciador de recursos no Azure DevTest Labs de tooexisting VM](http://www.visualstudiogeeks.com/blog/DevOps/Join-a-VM-to-existing-AD-domain-using-ARM-template-AzureDevTestLabs)

## <a name="next-steps"></a>Próximas etapas
* Saiba como muito[adicionar um laboratório de tooa do repositório de artefato Git](devtest-lab-add-artifact-repo.md).

