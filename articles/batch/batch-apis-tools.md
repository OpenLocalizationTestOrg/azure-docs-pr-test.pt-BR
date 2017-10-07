---
title: "soluções de aaaUse ferramentas e APIs de lote do Azure toodevelop em larga escala processamento paralelo | Microsoft Docs"
description: "Saiba mais sobre hello APIs e ferramentas disponíveis para o desenvolvimento de soluções com o serviço de lote do Azure hello."
services: batch
author: tamram
manager: timlt
ms.service: batch
ms.topic: get-started-article
ms.date: 03/08/2017
ms.author: tamram
ms.openlocfilehash: ca75a1a63b3e7e6b0805e79a63685bc49aaaca8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-batch-apis-and-tools"></a>Visão geral das ferramentas e APIs de Lote

Processamento paralelas cargas de trabalho com o lote do Azure normalmente é feito por meio de programação, usando uma saudação [APIs de lote](#batch-development-apis). Seu aplicativo cliente ou serviço pode usar o hello APIs de lote toocommunicate com hello serviço de lote. Com hello APIs de lote, você pode criar e gerenciar pools de nós de computação, de máquinas virtuais ou serviços de nuvem. Em seguida, você pode agendar trabalhos e tarefas toorun em nós. 

Com eficiência, você pode processar cargas de trabalho em larga escala para sua organização ou fornecer um front-end do serviço tooyour clientes para que eles podem executar trabalhos e tarefas – sob demanda ou em um agendamento – em um, centenas ou mesmo milhares de nós. Você também pode usar o Lote do Azure como parte de um fluxo de trabalho maior, gerenciado por ferramentas como o [Azure Data Factory](../data-factory/data-factory-data-processing-using-batch.md?toc=%2fazure%2fbatch%2ftoc.json).

> [!TIP]
> Quando você estiver pronto toodig em toohello API de lote para uma compreensão mais detalhada de saudação recursos que ele fornece, check-out Olá [visão geral do recurso de lote para desenvolvedores](batch-api-basics.md).
> 
> 

## <a name="azure-accounts-for-batch-development"></a>Contas do Azure para desenvolvimento de Lote
Ao desenvolver soluções de lote, você usará Olá contas no Microsoft Azure a seguir.

* **Conta e assinatura do Azure** – se ainda não tiver uma assinatura do Azure, você poderá ativar o [benefício de assinante do MSDN][msdn_benefits] ou inscrever-se para uma [conta gratuita do Azure][free_account]. Ao criar uma conta, uma assinatura padrão será criada para você.
* **Conta do Lote** - recursos do Lote do Azure, incluindo pools, nós de computação, trabalhos e tarefas, são associados a uma conta do Lote do Azure. Quando seu aplicativo faz uma solicitação no serviço de lote de hello, ele autentica a solicitação de saudação usando o nome da conta do Azure Batch Olá Olá URL da conta hello e uma chave de acesso. Você pode [criar conta de lote](batch-account-create-portal.md) em Olá portal do Azure.
* **Conta de armazenamento** – o Lote inclui suporte interno para trabalhar com arquivos no [Armazenamento do Azure][azure_storage]. Quase todos os cenários de lote usa o armazenamento de BLOBs do Azure para preparo programas Olá que executam as tarefas e os dados de saudação que eles processem e para o armazenamento de saudação de dados de saída que elas geram. toocreate uma conta de armazenamento, consulte [contas de armazenamento do Azure sobre](../storage/common/storage-create-storage-account.md).

## <a name="batch-service-apis"></a>APIs de serviço do Lote

Os aplicativos e serviços podem emitir chamadas de API REST diretas ou usar um ou mais Olá toorun de bibliotecas de cliente a seguir e gerenciar suas cargas de trabalho de lote do Azure.

| API | Referência de API | Baixar | Tutorial | Exemplos de código | Mais informações |
| --- | --- | --- | --- | --- | --- |
| **REST do Lote** |[MSDN][batch_rest] |N/D |- |- | [Versões com suporte](https://docs.microsoft.com/rest/api/batchservice/batch-service-rest-api-versioning) |
| **.NET do Lote** |[docs.microsoft.com][api_net] |[NuGet ][api_net_nuget] |[Tutorial](batch-dotnet-get-started.md) |[GitHub][api_sample_net] | [Notas de versão](http://aka.ms/batch-net-dataplane-changelog) |
| **Python em lotes** |[readthedocs.io][api_python] |[PyPI][api_python_pypi] |[Tutorial](batch-python-tutorial.md)|[GitHub][api_sample_python] | [Leiame](https://github.com/Azure/azure-sdk-for-python/blob/master/doc/batch.rst) |
| **Lote do Node.js** |[github.io][api_nodejs] |[npm][api_nodejs_npm] |- |- | [Leiame](https://github.com/Azure/azure-sdk-for-node/tree/master/lib/services/batch) |
| **Lote Java** |[github.io][api_java] |[Maven][api_java_jar] |- |[Leiame][api_sample_java] | [Leiame](https://github.com/Azure/azure-batch-sdk-for-java)|

## <a name="batch-management-apis"></a>APIs de Gerenciamento do Lote

Olá APIs do Gerenciador de recursos do Azure para o lote fornecem acesso programático tooBatch contas. Usando essas APIs, você pode gerenciar programaticamente contas do Lote, cotas e pacotes de aplicativos.  

| API | Referência de API | Baixar | Tutorial | Exemplos de código |
| --- | --- | --- | --- | --- |
| **Gerenciador de Recursos do Lote REST** |[docs.microsoft.com][api_rest_mgmt] |N/D |- |[GitHub](https://github.com/Azure-Samples/batch-dotnet-manage-batch-accounts) |
| **Gerenciador de Recursos do Lote .NET** |[docs.microsoft.com][api_net_mgmt] |[NuGet ][api_net_mgmt_nuget] | [Tutorial](batch-management-dotnet.md) |[GitHub][api_sample_net] |

## <a name="batch-command-line-tools"></a>Ferramentas de linha de comando do Lote

Essas ferramentas de linha de comando fornecem Olá a mesma funcionalidade como Olá APIs de gerenciamento de lote e o serviço de lote: 

* [Cmdlets do PowerShell do lote][batch_ps]: Olá cmdlets do Azure Batch Olá [Azure PowerShell](/powershell/azure/overview) módulo habilitar recursos de lote toomanage com o PowerShell.
* [CLI do Azure](/cli/azure/overview): hello Azure Interface de linha de comando (CLI do Azure) é um conjunto de ferramentas de plataforma cruzada que fornece os comandos do shell para interagir com muitos serviços do Azure, incluindo o serviço de lote hello e serviço de gerenciamento de lote. Consulte [recursos de lote gerenciar com CLI do Azure](batch-cli-get-started.md) para obter mais informações sobre como usar o hello CLI do Azure com o lote.

## <a name="other-tools-for-application-development"></a>Outras ferramentas para desenvolvimento de aplicativos

Aqui estão algumas ferramentas adicionais que podem ser úteis para compilar e depurar seus aplicativos e serviços do Lote:

* [Portal do Azure][portal]: criar, monitorar e excluir pools de lote, trabalhos e tarefas no hello Azure folhas de lote do portal. Você pode exibir informações de status de saudação para esses e outros recursos enquanto executar seus trabalhos e até mesmo baixar arquivos de nós de computação de saudação em seus pools. Por exemplo, você pode baixar uma `stderr.txt` de uma tarefa com falha durante a solução de problemas. Você também pode baixar arquivos de área de trabalho remota (RDP) que você pode usar toolog toocompute nós.
* [Gerenciador de lote do Azure][batch_explorer]: Gerenciador de lote fornece funcionalidade de gerenciamento de recursos de lote semelhante como Olá portal do Azure, mas em um aplicativo do Windows Presentation Foundation (WPF) cliente autônomo. Um dos aplicativos de exemplo .NET em lotes Olá disponíveis em [GitHub][github_samples], compilá-lo com o Visual Studio 2015 ou mais recente e usá-lo toobrowse e gerenciar recursos de saudação em sua conta do lote enquanto você desenvolve e depurar suas soluções de lote. Exibir trabalho, o pool e detalhes da tarefa, baixam arquivos de nós de computação e se conectar toonodes remotamente usando arquivos de área de trabalho remota (RDP), que você pode baixar com o Gerenciador de lote.
* [Microsoft Azure Storage Explorer][storage_explorer]: enquanto não é estritamente uma ferramenta de lote do Azure, Olá Storage Explorer é toohave de outra ferramenta valiosa durante o desenvolvimento e depuração suas soluções de lote.

## <a name="additional-resources"></a>Recursos adicionais

- toolearn sobre o log de eventos do aplicativo em lotes, consulte [Log de eventos para avaliação de diagnóstica e monitoramento de soluções de lote](batch-diagnostics.md). Para obter uma referência sobre eventos gerados pelo serviço de lote de saudação, consulte [análise de lote](batch-analytics.md).
- Para obter informações sobre variáveis de ambiente para nós de computação, consulte [Variáveis de ambiente do nó de computação do Lote do Azure](batch-compute-node-environment-variables.md).

## <a name="next-steps"></a>Próximas etapas

* Saudação de leitura [visão geral do recurso de lote para desenvolvedores](batch-api-basics.md), informações essenciais para qualquer pessoa toouse lote de preparação. artigo Olá contém informações mais detalhadas sobre os recursos de serviço de lote como pools, nós, trabalhos e tarefas e Olá muitos recursos da API que você pode usar ao criar seu aplicativo de lote.
* [Introdução à biblioteca do lote do Azure de saudação para .NET](batch-dotnet-get-started.md) toolearn como toouse c# e Olá tooexecute de biblioteca do .NET em lotes uma carga de trabalho simple usando um fluxo de trabalho comuns do lote. Este artigo deve ser um de seu primeiro interrompido enquanto aprende como toouse Olá serviço de lote. Também há um [versão do Python](batch-python-tutorial.md) tutorial hello.
* Baixar Olá [código amostras no GitHub] [ github_samples] toosee como c# e Python pode fazer a interface com lote tooschedule e processo de exemplo cargas de trabalho.
* Check-out Olá [de aprendizado em lotes] [ learning_path] tooget uma ideia de recursos de saudação tooyou disponíveis que você saiba toowork com o lote.


[azure_storage]: https://azure.microsoft.com/services/storage/
[api_java]: http://azure.github.io/azure-sdk-for-java/
[api_java_jar]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-batch%22
[api_net]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_nuget]: https://www.nuget.org/packages/Azure.Batch/
[api_rest_mgmt]: https://docs.microsoft.com/\rest/api/batchmanagement/
[api_net_mgmt]: https://msdn.microsoft.com/library/azure/mt463120.aspx
[api_net_mgmt_nuget]: https://www.nuget.org/packages/Microsoft.Azure.Management.Batch/
[api_nodejs]: http://azure.github.io/azure-sdk-for-node/azure-batch/latest/
[api_nodejs_npm]: https://www.npmjs.com/package/azure-batch
[api_python]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.html
[api_python_pypi]: https://pypi.python.org/pypi/azure-batch
[api_sample_net]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp
[api_sample_python]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch
[api_sample_java]: https://github.com/Azure/azure-batch-samples/tree/master/Java/
[batch_ps]: /powershell/resourcemanager/azurerm.batch/v2.7.0/azurerm.batch
[batch_rest]: https://msdn.microsoft.com/library/azure/Dn820158.aspx
[free_account]: https://azure.microsoft.com/free/
[github_samples]: https://github.com/Azure/azure-batch-samples
[learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[msdn_benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[batch_explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[storage_explorer]: http://storageexplorer.com/
[portal]: https://portal.azure.com
