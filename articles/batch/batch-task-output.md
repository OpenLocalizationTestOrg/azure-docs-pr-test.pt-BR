---
title: "resultados de aaaPersist ou logs de concluída dados tooa de trabalhos e tarefas de armazenamento - lote do Azure | Microsoft Docs"
description: "Saiba mais sobre as diferentes opções para persistir dados de saída de trabalhos e tarefas em Lote. Você pode persistir dados tooAzure armazenamento ou tooanother armazenar."
services: batch
author: tamram
manager: timlt
editor: 
ms.assetid: 16e12d0e-958c-46c2-a6b8-7843835d830e
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/16/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f0b11e387f1694e1ce3e9573db7f6013f0154cad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="persist-job-and-task-output"></a>Persistir saída de tarefa e de trabalho

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

Alguns exemplos comuns de saída de tarefa incluem:

- Arquivos criados quando os dados de entrada de processos de tarefa hello.
- Arquivos de log associados à execução da tarefa. 

Este artigo descreve várias opções para persistir saída e hello cenários de tarefas para o qual cada opção é mais apropriada.   

## <a name="about-hello-batch-file-conventions-standard"></a>Sobre padrão de convenções de arquivo em lotes Olá

Lote define um conjunto opcional de convenções de nomenclatura de arquivos de saída de tarefa no Armazenamento do Azure. Olá [padrão de convenções de arquivo em lotes](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) descreve estas convenções. padrão de convenções de arquivo Hello determina os nomes de saudação de saudação contêiner e blob de caminho de destino no armazenamento do Azure para um arquivo de saída determinada com base nos nomes de saudação do hello trabalhos e tarefas.

É o tooyou se você decidir toouse Olá convenções de arquivo padrão para nomear os arquivos de dados de saída. Você também pode nomear Olá destino contêiner e blob, no entanto, você deseja. Se você usar Olá convenções de arquivo padrão de nomeação de arquivos de saída, os arquivos de saída estão disponíveis para exibição no hello [portal do Azure][portal].

Há algumas maneiras diferentes que você pode usar o padrão de convenções de arquivo hello:

- Se você estiver usando arquivos de saída do hello lote serviço API toopersist, você pode escolher contêineres de destino tooname e blobs de acordo com o toohello convenções de arquivo padrão. Olá API do serviço de lote permite que você toopersist arquivos de saída no código do cliente, sem modificar seu aplicativo de tarefa.
- Se você estiver desenvolvendo com o .NET, você pode usar o hello [biblioteca convenções de arquivo de lote do Azure para .NET][nuget_package]. Uma vantagem de usar essa biblioteca é que ele oferece suporte a consultas tootheir ID ou a finalidade de acordo com seus arquivos de saída. funcionalidade de consulta interna Olá torna fácil tooaccess arquivos de saída de um aplicativo cliente ou de outras tarefas. No entanto, seu aplicativo com a tarefa deve ser modificado toocall biblioteca de convenções de arquivo. Para obter mais informações, consulte a referência de saudação para Olá [biblioteca convenções de arquivo para .NET](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.aspx).
- Se você estiver desenvolvendo com um idioma diferente do .NET, você pode implementar Olá convenções de arquivo padrão em seu aplicativo.

## <a name="design-considerations-for-persisting-output"></a>Considerações de design para manter a saída 

Ao projetar sua solução de lote, considere o seguinte Olá fatores relacionado toojob e saídas de tarefas.

* **Tempo de vida de nó de computação**: os nós de computação geralmente são transitórios, especialmente em pools com dimensionamento automático habilitado. Saída de uma tarefa que é executado em um nó está disponível somente ao nó Olá existe e somente no período de retenção de arquivo hello definidas para a tarefa hello. Se uma tarefa produz saída que pode ser necessária após a conclusão da tarefa hello, tarefa Olá deve carregar seu repositório saída arquivos tooa durável, como o armazenamento do Azure.

* **Armazenamento de saída**: o Armazenamento do Azure é recomendado como um armazenamento de dados para a saída da tarefa, mas você pode usar qualquer armazenamento durável. Armazenamento gravar tooAzure de saída de tarefa é integrado ao Olá API do serviço de lote. Se você usar outra forma de armazenamento durável, você precisará de saída da lógica de aplicativo toowrite Olá toopersist tarefas por conta própria.   

* **Recuperação de saída**: você pode recuperar a saída da tarefa diretamente de nós de computação de saudação em seu pool ou armazenamento do Azure ou outro repositório de dados se você tiver persistente a saída da tarefa. tooretrieve uma tarefa de saída do diretamente de um nó de computação, você precisa de nome de arquivo hello e seu local de saída no nó de saudação. Se você mantiver a saída de tarefa tooAzure armazenamento, em seguida, você precisa de arquivo de toohello de caminho completo Olá nos arquivos de saída do armazenamento do Azure toodownload Olá com hello SDK de armazenamento do Azure.

* **Exibindo a saída**: quando você navega a tarefa em hello Azure portal e selecione lotes tooa **arquivos no nó**, você verá todos os arquivos associados à tarefa hello, Olá não apenas os arquivos de saída que você está interessado. Novamente, os arquivos em nós de computação estão disponíveis apenas enquanto o nó Olá existe e somente em tempo de retenção de arquivo hello definidas para a tarefa hello. saída da tarefa de tooview que você tiver mantido tooAzure armazenamento, você pode usar Olá portal do Azure ou um aplicativo de cliente de armazenamento do Azure como Olá [Azure Storage Explorer][storage_explorer]. tooview dados no armazenamento do Azure com o portal de saudação ou outra ferramenta de saída, você deve saber o local do arquivo hello e navegue tooit diretamente.

## <a name="options-for-persisting-output"></a>Opções para manter a saída

Dependendo do cenário, há algumas abordagens diferentes, você pode colocar a saída da tarefa toopersist:

- Use a API do serviço de lote de saudação.  
- Use a biblioteca de convenções de arquivo em lotes de saudação para .NET.  
- Implemente Olá convenções do arquivo de lote padrão em seu aplicativo.
- Implementar uma solução de movimentação de arquivo personalizada.

Olá seções a seguir descreve cada abordagem mais detalhadamente.

### <a name="use-hello-batch-service-api"></a>Usar a API do serviço de lote Olá

Com a versão de 2017-05-01, Olá serviço de lote adiciona suporte para especificar os arquivos de saída no armazenamento do Azure para dados de tarefa quando você [adicionar um trabalho tooa](https://docs.microsoft.com/rest/api/batchservice/add-a-task-to-a-job) ou [adicionar uma coleção de trabalho de tooa tarefas](https://docs.microsoft.com/rest/api/batchservice/add-a-collection-of-tasks-to-a-job).

Olá API do serviço de lote dá suporte a tooan de dados persistentes tarefa conta de armazenamento do Azure dos pools criados com a configuração de máquina virtual de saudação. Com hello API do serviço de lote, você pode persistir os dados de tarefa sem modificar o aplicativo hello que executa a tarefa. Você pode opcionalmente aderir toohello [padrão de convenções de arquivo em lotes](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) para nomeação de arquivos de saudação que você persistir tooAzure armazenamento. 

Use a tarefa de toopersist de saudação API do serviço de lote de saída quando:

- Você deseja toopersist dados tarefas em lote e o Gerenciador de tarefas em pools criados com a configuração de máquina virtual de saudação.
- Deseja que o contêiner de armazenamento do Azure de tooan toopersist dados com um nome arbitrário.
- Você deseja que o contêiner de armazenamento do Azure toopersist dados tooan chamado acordo toohello [padrão de convenções de arquivo em lotes](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions). 

> [!NOTE]
> Olá API do serviço de lote não oferece suporte a dados persistentes de tarefas em execução em pools criados com a configuração de serviço de nuvem hello. Para obter informações sobre a tarefa persistente de saída de pools de configuração de serviços de nuvem hello, consulte [Manter trabalhos e tarefas tooAzure de dados armazenamento com biblioteca de convenções de arquivo em lotes Olá para .NET toopersist](batch-task-output-file-conventions.md)
> 
> 

Para obter mais informações sobre a saída da tarefa persistentes com hello API do serviço de lote, consulte [persistir dados de tarefa tooAzure armazenamento com a API do serviço de lote de saudação](batch-task-output-files.md). Consulte também Olá projeto no GitHub, que demonstra como a biblioteca de cliente de lote toouse Olá para tarefas do .NET toopersist saída toodurable armazenamento de exemplo [PersistOutputs] [github_persistoutputs].

### <a name="use-hello-batch-file-conventions-library-for-net"></a>Use a biblioteca de convenções de arquivo em lotes de saudação para .NET

Desenvolvedores criar soluções de lote com c# e o .NET podem usar Olá [biblioteca convenções de arquivo para .NET] [ nuget_package] toopersist tarefa dados tooan conta de armazenamento do Azure, de acordo com o toohello [arquivo em lotes Convenções padrão](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions). biblioteca de convenções de arquivo Hello manipula tooAzure de arquivos de saída móvel armazenamento e nomenclatura contêineres de destino e blobs de forma bem conhecida.

Olá convenções arquivo biblioteca ofereça suporte a consultar arquivos de saída por ID ou finalidade, tornando fácil toolocate-los sem a necessidade de saudação completos arquivo URIs. 

Use a biblioteca de convenções de arquivo em lotes de saudação para .NET toopersist tarefa saída quando:

- Você deseja toostream dados tooAzure armazenamento enquanto a tarefa Olá ainda está em execução.
- Você deseja toopersist dados pools criados com a configuração do serviço de nuvem hello ou configuração de máquina virtual de saudação.
- O aplicativo cliente ou outras tarefas no hello toolocate necessidades de trabalho e baixar arquivos de saída de tarefas por ID ou por finalidade. 
- Você deseja que o carregamento inicial ou apontando para a verificação de tooperform de resultados inicias.
- Você deseja tooview saída da tarefa no hello portal do Azure.

Para obter mais informações sobre a saída da tarefa persistentes com biblioteca de convenções de arquivo hello para .NET, consulte [Manter trabalhos e tarefas tooAzure de dados armazenamento com biblioteca de convenções de arquivo em lotes Olá para .NET toopersist ](batch-task-output-file-conventions.md). Consulte também Olá projeto no GitHub, que demonstra como biblioteca de convenções de arquivo hello toouse para tarefas do .NET toopersist toodurable armazenamento de saída de exemplo [PersistOutputs] [github_persistoutputs].

Olá projeto de exemplo [PersistOutputs] [github_persistoutputs] no GitHub demonstra como a biblioteca de cliente de lote toouse Olá para tarefas do .NET toopersist saída toodurable armazenamento.

### <a name="implement-hello-batch-file-conventions-standard"></a>Implementar Olá convenções padrão de arquivo de lote

Se você estiver usando um idioma diferente do .NET, você pode implementar Olá [padrão de convenções de arquivo em lotes](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) em seu próprio aplicativo. 

Talvez você queira tooimplement saudação padrão de nomenclatura de arquivo convenções por conta própria quando desejar que um esquema de nomenclatura comprovado, ou quando desejar que a saída da tarefa tooview em Olá portal do Azure.

### <a name="implement-a-custom-file-movement-solution"></a>Implementar uma solução de movimentação de arquivo personalizada

Você também pode implementar sua própria solução de movimentação de arquivo completa. Use esta abordagem quando:

- Deseja que o repositório de dados de tooa toopersist tarefa dados que não seja o armazenamento do Azure. repositório de dados tooupload arquivos tooa como SQL Azure ou DataLake do Azure, você pode criar um script personalizado ou o local do executável tooupload toothat. Em seguida, você pode chamá-lo na linha de comando Olá depois de executar o executável principal. Por exemplo, em um nó do Windows, você pode chamar estes dois comandos:`doMyWork.exe && uploadMyFilesToSql.exe`
- Você deseja que o carregamento inicial ou apontando para a verificação de tooperform de resultados inicias.
- Você deseja toomaintain o controle granular sobre o tratamento de erros. Por exemplo, talvez você queira tooimplement sua própria solução se você quiser toouse tarefa dependência ações tootake determinados carregar ações com base em códigos de saída de tarefa específica. Para obter mais informações sobre ações de dependência de tarefas, consulte [criar dependências toorun tarefas que dependem de outras tarefas](batch-task-dependencies.md). 

## <a name="next-steps"></a>Próximas etapas

- Explorar usando Olá novos recursos nos dados de tarefa toopersist Olá API do serviço de lote no [persistir dados de tarefa tooAzure armazenamento com a API do serviço de lote de saudação](batch-task-output-files.md).
- Saiba como usar a biblioteca de convenções de arquivo em lotes Olá para .NET em [Manter trabalhos e tarefas tooAzure de dados armazenamento com biblioteca de convenções de arquivo em lotes Olá para .NET toopersist ](batch-task-output-file-conventions.md).
- Consulte Olá [PersistOutputs] [github_persistoutputs] toodurable armazenamento de saída do projeto de exemplo no GitHub, que demonstra como toouse ambos Olá biblioteca de cliente do Batch para .NET e biblioteca de convenções de arquivo de saudação para tarefa de toopersist .NET.

[nuget_package]: https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files
[portal]: https://portal.azure.com
[storage_explorer]: http://storageexplorer.com/
