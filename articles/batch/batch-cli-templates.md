---
title: "aaaRun do Azure Batch trabalhos de ponta a ponta sem escrever código (visualização) | Microsoft Docs"
description: "Crie arquivos de modelo para pools de lote de toocreate Olá CLI do Azure, trabalhos e tarefas."
services: batch
author: mscurrell
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: na
ms.topic: article
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: markscu
ms.openlocfilehash: c0434d09766451f6ba516efbad949834711ee819
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a>Usar modelos CLI do Lote do Azure e o arquivo de transferência (Versão prévia)

Usando Olá CLI do Azure é possível toorun trabalhos de lote sem escrever código.

Arquivos de modelo podem ser criados e usados com hello CLI do Azure que permitem que o lote pools, trabalhos e tarefas toobe criado. Arquivos de entrada de trabalho podem ser carregados facilmente a conta de armazenamento Olá associada Olá lote conta e o trabalho de saída arquivos baixados.

## <a name="overview"></a>Visão geral

Toohello uma extensão CLI do Azure permite que o lote toobe usado-a ponta por usuários que não são desenvolvedores. Um pool pode ser criado, carregado de dados de entrada, trabalhos e tarefas associadas criadas, e Olá resultante saída dados baixados – nenhum código obrigatório, Olá CLI que está sendo usada diretamente ou que está sendo integrado em scripts.

Criar modelos de lote no hello [suporte de lote existente no hello CLI do Azure](https://docs.microsoft.com/azure/batch/batch-cli-get-started#json-files-for-resource-creation) que permite que os arquivos JSON toospecify valores de propriedade para a criação de saudação de pools, trabalhos, tarefas e outros itens. Com modelos de lote, hello seguintes recursos são adicionados em que é possível com os arquivos JSON hello:

-   Parâmetros podem ser definidos. Quando Olá modelo é usado, somente os valores de parâmetro hello são item Olá toocreate especificado com outros valores de propriedade do item que está sendo especificada no corpo do modelo de saudação. Um usuário que entende o que lote e toobe a aplicativos executados em lote pode criar modelos, a especificação de pool de trabalho e valores de propriedade da tarefa. Um usuário menos familiarizados com o lote e/ou os aplicativos só precisa os valores hello toospecify para parâmetros de saudação definido.

-   Fábricas de tarefa de trabalho criar uma ou mais tarefas associadas a um trabalho, evitando Olá necessário para muitas tarefas definições toobe criado e simplificar significativamente o envio de trabalho.


Arquivos de dados de entrada necessário toobe fornecido para trabalhos e geralmente são produzidos, arquivos de dados de saída. Uma conta de armazenamento está associada, por padrão, com cada lote de conta e arquivos podem ser facilmente transferido tooand desta conta de armazenamento usando a CLI, sem codificação e nenhuma credencial de armazenamento necessária.

Por exemplo, [ffmpeg](http://ffmpeg.org/) é um aplicativo popular que processa arquivos de áudio e vídeo. Olá CLI de lote do Azure pode ser usado tooinvoke ffmpeg tootranscode fonte arquivos de vídeo toodifferent resoluções.

-   Um modelo de pool é criado. usuário de Olá criar modelo Olá sabe como toocall Olá ffmpeg aplicativo e seus requisitos. Olá, elas especificam OS apropriado, VM de tamanho, como ffmpeg está instalado (de um pacote de aplicativo ou usando um Gerenciador de pacotes, por exemplo) e outros valores de propriedade do pool. Parâmetros são criados quando o modelo de saudação é usado, somente id do pool hello e número de VMs necessário toobe especificado.

-   Um modelo de trabalho é criado. modelo de criação Olá Olá usuário sabe como ffmpeg necessidades toobe chamado resolução de vídeo tooa diferente da origem de tootranscode e especifica a linha de comando da tarefa de saudação; Eles também sabem que é uma pasta que contém arquivos de vídeo de origem hello, com uma tarefa obrigatória por arquivo de entrada.

-   Um usuário final com um conjunto de arquivos de vídeo tootranscode primeiro cria um pool usando o modelo de pool hello, especificando somente id do pool hello e número de VMs necessárias. Eles podem, em seguida, carregue Olá tootranscode de arquivos de origem. Um trabalho pode ser enviado usando o modelo de trabalho hello, especificando somente a id do pool de hello e local dos arquivos de origem Olá carregado. trabalho em lotes de saudação é criado com uma tarefa por arquivo de entrada que está sendo gerado. Por fim, Olá transcodificado nos arquivos de saída podem ser o download.

## <a name="installation"></a>Instalação

capacidade de transferência de arquivo e o modelo de saudação exige um toobe extensão instalada.

Para obter instruções sobre como ver tooinstall Olá CLI do Azure [instalar o Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).

Uma vez Olá que CLI do Azure foi instalado, Olá extensão pode ser instalada usando o seguinte comando CLI do lote:

```azurecli
az component update --add batch-extensions --allow-third-party
```

Para obter mais informações sobre Olá extensão em lotes, consulte [do Microsoft Azure lote CLI extensões do Windows, Mac e Linux](https://github.com/Azure/azure-batch-cli-extensions#microsoft-azure-batch-cli-extensions-for-windows-mac-and-linux).

## <a name="templates"></a>Modelos

Olá CLI de lote do Azure permite que os itens como grupos, trabalhos e tarefas toobe criados, especificando um arquivo JSON que contém os valores e nomes de propriedade. Por exemplo:

```azurecli
az batch pool create –-json-file AppPool.json
```

Modelos de lote do Azure são semelhantes tooAzure Gerenciador de recursos modelos, na funcionalidade e a sintaxe. Elas são arquivos JSON que contêm valores e nomes de propriedade do item, mas adicionar Olá principais conceitos a seguir:

-   **Parâmetros**

    -   Permitir toobe de valores de propriedade especificado em uma seção de corpo, com apenas os valores de parâmetro necessidade toobe fornecido ao modelo de saudação é usado. Por exemplo, a definição completa Olá para um pool pôde ser colocada no corpo de saudação e apenas um parâmetro definido para a id do pool; apenas uma cadeia de id do pool, portanto, precisa toocreate toobe fornecido um pool.
        
    -   corpo do modelo de saudação pode ser criado por uma pessoa com conhecimento do lote e Olá aplicativos toobe execute o lote; somente os valores para parâmetros definidos pelo autor do hello devem ser fornecidos quando Olá modelo é usado. Um usuário sem Olá lote detalhada e/ou dados de conhecimento do aplicativo, portanto, podem usar os modelos.

-   **Variáveis**

    -   Permitir toobe de valores simples ou complexos de parâmetro especificado em um local e usado em um ou mais locais do corpo do modelo de saudação. Variáveis podem simplificar e reduzir o tamanho de saudação do modelo hello, bem como tornar mais fácil manutenção tendo um propriedades de toochange local cujo valor pode ser alterado.

-   **Construções de nível superior**

    -   Algumas construções de nível superior estão disponíveis no modelo de saudação que ainda não estão disponíveis no hello APIs de lote. Por exemplo, uma fábrica de tarefas pode ser definida em um modelo de trabalho que cria várias tarefas de trabalho hello usando uma definição de tarefa comum. Essas construções evitar Olá necessidade toocode para dinamicamente crie vários arquivos JSON, como um arquivo por tarefa, bem como criar script arquivos tooinstall aplicativos por meio de um Gerenciador de pacotes, por exemplo.

    -   Em algum ponto, onde aplicável, que essas construções podem ser adicionados toothe lote serviço e está disponível em Olá APIs de lote, interfaces do usuário, etc.

### <a name="pool-templates"></a>Modelos de pool

Além disso, toohello recursos de modelo padrão de parâmetros e variáveis, Olá construções de nível superior a seguir são suportados pelo modelo de pool de saudação:

-   **Referências do pacote**

    -   Opcionalmente, permite que software toobe copiado toopool nós usando o pacote gerentes. Gerenciador de pacotes de saudação e a id do pacote são especificados. Sendo toodeclare capaz de um ou mais pacotes evita Olá necessidade toocreate um script que obtém os pacotes de saudação necessários, Olá script de instalação e execute o script hello em cada nó de pool.

a seguir Olá é um exemplo de um modelo que cria um pool de VMs do Linux com ffmpeg instalado e apenas requer um número de cadeia de caracteres e hello da id de pool de máquinas virtuais toobe fornecido toouse:

```json
{
    "parameters": {
        "nodeCount": {
            "type": "int",
            "metadata": {
                "description": "hello number of pool nodes"
            }
        },
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "hello pool id "
            }
        }
    },
    "pool": {
        "type": "Microsoft.Batch/batchAccounts/pools",
        "apiVersion": "2016-12-01",
        "properties": {
            "id": "[parameters('poolId')]",
            "virtualMachineConfiguration": {
                "imageReference": {
                    "publisher": "Canonical",
                    "offer": "UbuntuServer",
                    "sku": "16.04.0-LTS",
                    "version": "latest"
                },
                "nodeAgentSKUId": "batch.node.ubuntu 16.04"
            },
            "vmSize": "STANDARD_D3_V2",
            "targetDedicatedNodes": "[parameters('nodeCount')]",
            "enableAutoScale": false,
            "maxTasksPerNode": 1,
            "packageReferences": [
                {
                    "type": "aptPackage",
                    "id": "ffmpeg"
                }
            ]
        }
    }
}
```

Se o arquivo de modelo de saudação foi nomeado _ffmpeg.json do pool de_, em seguida, o modelo Olá seria invocado da seguinte maneira:

```azurecli
az batch pool create --template pool-ffmpeg.json
```

### <a name="job-templates"></a>Modelos de trabalho

Além disso, toohello recursos de modelo padrão de parâmetros e variáveis, Olá construções de nível superior a seguir são suportados pelo modelo de trabalho hello:

-   **Fábrica de tarefas**

    -   Com base em uma definição de tarefa, cria várias tarefas para um trabalho. Três tipos de fábrica de tarefas têm suporte – limpeza paramétrica, tarefa por arquivo e coleção de tarefas.

Olá seguinte é um exemplo de um modelo que cria um trabalho que usa ffmpeg para transcodificar tooone de arquivos de vídeo MP4 de duas resoluções mais baixas, com uma tarefa criada por um arquivo de vídeo de origem:

```json
{
    "parameters": {
        "poolId": {
            "type": "string",
            "metadata": {
                "description": "hello name of Azure Batch pool which runs hello job"
            }
        },
        "jobId": {
            "type": "string",
            "metadata": {
                "description": "hello name of Azure Batch job"
            }
        },
        "resolution": {
            "type": "string",
            "defaultValue": "428x240",
            "allowedValues": [
                "428x240",
                "854x480"
            ],
            "metadata": {
                "description": "Target video resolution"
            }
        }
    },
    "job": {
        "type": "Microsoft.Batch/batchAccounts/jobs",
        "apiVersion": "2016-12-01",
        "properties": {
            "id": "[parameters('jobId')]",
            "constraints": {
                "maxWallClockTime": "PT5H",
                "maxTaskRetryCount": 1
            },
            "poolInfo": {
                "poolId": "[parameters('poolId')]"
            },
            "taskFactory": {
                "type": "taskPerFile",
                "source": { 
                    "fileGroup": "ffmpeg-input"
                },
                "repeatTask": {
                    "commandLine": "ffmpeg -i {fileName} -y -s [parameters('resolution')] -strict -2 {fileNameWithoutExtension}_[parameters('resolution')].mp4",
                    "resourceFiles": [
                        {
                            "blobSource": "{url}",
                            "filePath": "{fileName}"
                        }
                    ],
                    "outputFiles": [
                        {
                            "filePattern": "{fileNameWithoutExtension}_[parameters('resolution')].mp4",
                            "destination": {
                                "autoStorage": {
                                    "path": "{fileNameWithoutExtension}_[parameters('resolution')].mp4",
                                    "fileGroup": "ffmpeg-output"
                                }
                            },
                            "uploadOptions": {
                                "uploadCondition": "TaskSuccess"
                            }
                        }
                    ]
                }
            },
            "onAllTasksComplete": "terminatejob"
        }
    }
}
```

Se o arquivo de modelo de saudação foi nomeado _ffmpeg.json trabalho_, em seguida, o modelo Olá seria invocado da seguinte maneira:

```azurecli
az batch job create --template job-ffmpeg.json
```

## <a name="file-groups-and-file-transfer"></a>Transferência de arquivos e grupos de arquivo

A maioria dos trabalhos e tarefas exigem arquivos de entrada e produzem arquivos de saída. Os dois arquivos de entrada e arquivos de saída necessário normalmente toobe transferido, do nó de toohello Olá cliente ou do cliente do hello nó toohello. Olá extensão CLI de lote do Azure abstrai a transferência de arquivo ausente e utiliza a conta de armazenamento de saudação que é criada por padrão para cada conta do lote.

Um grupo de arquivos é igual a tooa contêiner que é criado no hello conta de armazenamento do Azure. grupo de arquivos Olá pode ter subpastas.

Olá extensão CLI de lote fornece comandos para carregar arquivos do grupo de arquivos especificado tooa cliente e baixar arquivos de cliente de tooa de grupo Olá arquivo especificado.

```azurecli
az batch file upload --local-path c:\source_videos\*.mp4 
    --file-group ffmpeg-input

az batch file download --file-group ffmpeg-output --local-path
    c:\output_lowres_videos
```

Modelos de pool e trabalho permitem que os arquivos armazenados em toobe de grupos de arquivo especificado para a cópia em nós de pool ou desativar o pool de nós novamente tooa o grupo de arquivos. Por exemplo, no modelo de trabalho especificado anteriormente, Olá grupo "ffmpeg-entrada de arquivo" for especificado para a fábrica de tarefas Olá como local de Olá Olá vídeo de arquivos de origem copiado para baixo para o nó Olá para transcodificação; Olá grupo "ffmpeg-saída de arquivo" é usado como o local onde os arquivos de saída transcodificado Olá são hello copiados nó de saudação toofrom executar cada tarefa.

## <a name="summary"></a>Resumo

Suporte de transferência de arquivo e o modelo atualmente foram adicionados apenas toohello CLI do Azure. meta de saudação é tooexpand Olá público-alvo que pode usar toousers de lote que não é necessário o código de toodevelop usando Olá APIs de lote, como os pesquisadores, usuários e assim por diante. Sem codificação, usuários com conhecimento do Azure, lote e Olá aplicativos toobe executado por lote podem criar modelos para criação de pool e de trabalho. Com os parâmetros de modelo, os usuários sem conhecimento detalhado dos aplicativos de lote e hello podem usar modelos de saudação.

Experimente Olá extensão de lote para Olá CLI do Azure e fornecer comentários ou sugestões, a saudação em comentários para este artigo ou por meio de saudação [Fórum do Azure Batch](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch).

## <a name="next-steps"></a>Próximas etapas

- Consulte a postagem de blog de modelos de lote Olá: [trabalhos em execução em lote do Azure usando Olá CLI do Azure – nenhum código necessário](https://azure.microsoft.com/en-us/blog/running-azure-batch-jobs-using-the-azure-cli-no-code-required/).
- Documentação detalhada de instalação e uso, exemplos e código-fonte estão disponíveis no hello [repositório GitHub Azure](https://github.com/Azure/azure-batch-cli-extensions).
