---
title: "aaaStart criar soluções de lote com modelos de projeto do Visual Studio - Azure | Microsoft Docs"
description: "Saiba como os modelos de projeto do Visual Studio podem ajudar você a implementar e executar suas cargas de trabalho de computação intensa no Lote do Azure."
services: batch
documentationcenter: .net
author: fayora
manager: timlt
editor: 
ms.assetid: 5e041ae2-25af-4882-a79e-3aa63c4bfb20
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a61c480ddc4dffd66c01220a137a3e852e39c338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-visual-studio-project-templates-toojump-start-batch-solutions"></a>Usar soluções do Visual Studio project modelos toojump Iniciar em lotes

Olá **Gerenciador de trabalhos** e **modelos do Visual Studio do processador de tarefa** de lote de fornecer código toohelp você tooimplement e executar suas cargas de trabalho com computação intensiva em lote com hello menos esforço. Este documento descreve esses modelos e fornece orientação sobre como toouse-los.

> [!IMPORTANT]
> Este artigo discute somente modelos de toothese aplicável duas informações e pressupõe que você esteja familiarizado com o serviço de lote hello e tooit relacionados conceitos principais: computação de pools, nós, trabalhos e tarefas, tarefas do Gerenciador de trabalho, variáveis de ambiente e outros informações relevantes. Você pode encontrar mais informações em [Noções básicas do lote do Azure](batch-technical-overview.md), [visão geral do recurso de lote para desenvolvedores](batch-api-basics.md), e [Introdução à biblioteca do lote do Azure de saudação para .NET](batch-dotnet-get-started.md).
> 
> 

## <a name="high-level-overview"></a>Visão geral de alto nível
modelos de Gerenciador de trabalhos e tarefas processador Olá podem ser usado toocreate dois componentes úteis:

* Uma tarefa do gerenciador de trabalho que implementa um divisor de trabalho que pode, por sua vez, dividir um trabalho em várias tarefas que podem ser executadas de forma independente, em paralelo.
* Um processador de tarefas que pode ser usados tooperform pré-processando e pós-processamento em torno de uma linha de comando do aplicativo.

Por exemplo, em um cenário de renderização de filme, divisor de trabalho Olá seria transformar um trabalho único de filme em centenas ou milhares de tarefas separadas que processam quadros individuais separadamente. De forma correspondente, processador de tarefa Olá seria invocar Olá renderização de aplicativo e todos os processos dependentes que são necessária toorender cada quadro, bem como executar ações adicionais (por exemplo, copiando Olá renderizado quadro tooa local de armazenamento).

> [!NOTE]
> modelos de Gerenciador de trabalhos e tarefas processador Olá são independentes entre si, assim você pode escolher toouse ambos ou apenas um deles, dependendo dos requisitos de saudação do seu trabalho de computação e em suas preferências.
> 
> 

Conforme mostrado no diagrama de saudação abaixo, um trabalho de computação que usa esses modelos passará por três estágios:

1. código de cliente da saudação (por exemplo, aplicativo, serviço web, etc.) envia um serviço de lote no Azure, especificando como seu programa de Gerenciador de trabalho trabalho manager tarefa Olá de toohello de trabalho.
2. serviço de lote Olá executa a tarefa do Gerenciador de trabalho Olá em um nó de computação e hello trabalho divisor inicia Olá especificado número de tarefas de processador, em como muitos nós de computação conforme necessário, com base nas especificações no código do divisor de trabalho hello e parâmetros de saudação.
3. Olá processador tarefas executam de forma independente, em paralelo, tooprocess os dados de entrada hello e geram dados de saída de saudação.

![Diagrama mostrando como o código do cliente interage com hello serviço de lote][diagram01]

## <a name="prerequisites"></a>Pré-requisitos
toouse modelos de lote hello, você precisará seguir hello:

* Um computador com o Visual Studio 2015 instalado. Modelos de lote atualmente só têm suporte para o Visual Studio 2015.
* modelos de lote Hello, que estão disponíveis no hello [Galeria do Visual Studio] [ vs_gallery] como extensões do Visual Studio. Há duas maneiras de modelos de saudação tooget:
  
  * Instalar os modelos de saudação usando Olá **extensões e atualizações** caixa de diálogo no Visual Studio (para obter mais informações, consulte [Localizando e usando extensões do Visual Studio][vs_find_use_ext]). Em Olá **extensões e atualizações** caixa de diálogo, pesquisa e download Olá duas extensões a seguir:
    
    * Gerenciador de Trabalhos do Lote do Azure com o Divisor de Trabalho
    * Processador de Tarefas do Lote do Azure
  * Baixar modelos de saudação da galeria online Olá para o Visual Studio: [modelos de projeto de lote do Microsoft Azure][vs_gallery_templates]
* Se você planejar Olá toouse [pacotes de aplicativos](batch-application-packages.md) nós de computação do Gerenciador de trabalhos do recurso toodeploy hello e toohello do processador de tarefa em lotes, é necessário toolink uma conta de armazenamento tooyour conta do lote.

## <a name="preparation"></a>Preparação
É recomendável criar uma solução que pode conter seu Gerenciador de trabalho, bem como o processador de tarefa, porque isso pode tornar mais fácil código tooshare entre o Gerenciador de trabalhos e programas de processador da tarefa. toocreate nesta solução, siga estas etapas:

1. Abra o Visual Studio e selecione **Arquivo** > **Novo** > **Projeto**.
2. Em **Modelos**, expanda **Outros Tipos de Projeto**, clique em **Soluções do Visual Studio** e, em seguida, selecione **Solução em Branco**.
3. Digite um nome que descreve a finalidade de aplicativo e hello dessa solução (por exemplo, "LitwareBatchTaskPrograms").
4. toocreate Olá nova solução, clique em **Okey**.

## <a name="job-manager-template"></a>Modelo do Gerenciador de trabalho
modelo do Gerenciador de trabalhos Olá ajuda tooimplement uma tarefa do Gerenciador de trabalho que pode executar Olá ações a seguir:

* Dividir um trabalho em várias tarefas.
* Envie toorun essas tarefas em lote.

> [!NOTE]
> Para saber mais sobre as tarefas do Gerenciador de trabalho, confira [Visão geral do recurso Lote para desenvolvedores](batch-api-basics.md#job-manager-task).
> 
> 

### <a name="create-a-job-manager-using-hello-template"></a>Criar um Gerenciador de trabalho usando o modelo de saudação
tooadd uma solução de toohello do Gerenciador de trabalho que você criou anteriormente, siga estas etapas:

1. Abra sua solução existente no Visual Studio.
2. No Gerenciador de soluções, solução de saudação com o botão direito, clique em **adicionar** > **novo projeto**.
3. No **Visual C#**, clique em **Nuvem** e em **Gerenciador de trabalho do Lote do Azure com o Divisor de trabalho**.
4. Digite um nome que descreva o aplicativo e identifica este projeto como Gerenciador de trabalhos da saudação (por exemplo "GerenciadorDeTrabalhoLitware").
5. projeto de saudação toocreate, clique em **Okey**.
6. Finalmente, referenciado de compilação Olá projeto tooforce Visual Studio tooload todos os pacotes do NuGet e tooverify que Olá projeto é válido antes de começar a modificá-lo.

### <a name="job-manager-template-files-and-their-purpose"></a>Arquivos do modelo do Gerenciador de trabalho e suas finalidades
Quando você cria um projeto usando o modelo do Gerenciador de trabalhos hello, ele gera três grupos de arquivos de código:

* arquivo de programa principal Hello (Program.cs). Ele contém o ponto de entrada de programa hello e manipulação de exceção de nível superior. Você normalmente não precisa toomodify isso.
* diretório do Framework Hello. Isso contém arquivos de saudação responsáveis pelo trabalho 'padrão' hello pelo programa de Gerenciador de trabalho hello – desempacotar parâmetros, adicionando o trabalho de lote de toohello de tarefas, etc. Você normalmente não precisa toomodify esses arquivos.
* arquivo separador Olá trabalho (JobSplitter.cs). É nesse arquivo que você colocará a lógica específica ao aplicativo para a divisão de um trabalho em tarefas.

Obviamente você pode adicionar arquivos adicionais como toosupport necessário seu código de separador de trabalho, dependendo da complexidade de saudação do trabalho Olá divisão lógica.

modelo de saudação também gera arquivos de projeto padrão do .NET como um arquivo. csproj App. config, Packages, etc.

restante Olá desta seção descreve Olá diferentes arquivos e sua estrutura de código e explica o que faz cada classe.

![Visual Studio Gerenciador de soluções mostrando a solução de modelo do Gerenciador de trabalhos Olá][solution_explorer01]

**Arquivos do Framework**

* `Configuration.cs`: Encapsula o carregamento de saudação de dados de configuração de trabalho, como detalhes da conta, as credenciais de conta de armazenamento vinculada, informações de trabalhos e tarefas e parâmetros do trabalho em lotes. Ele também fornece acesso definido tooBatch as variáveis de ambiente (consulte as configurações de ambiente para tarefas, na documentação do lote Olá) por meio da classe Configuration.EnvironmentVariable hello.
* `IConfiguration.cs`: Resumo Olá implementação de classe de configuração de hello, para que você possa de teste de unidade o divisor de trabalho usando um objeto de configuração falsas ou fictícias.
* `JobManager.cs`: Coordena os componentes de saudação do programa de Gerenciador de trabalho Olá. É responsável por Olá Inicializando divisor de trabalho hello, invocando divisor de trabalho Olá, e expedir tarefas Olá retornado pelo emissor da tarefa toohello Olá trabalho divisor.
* `JobManagerException.cs`Representa um erro que exige Olá tooterminate de Gerenciador de trabalho. JobManagerException é usado toowrap 'esperado' erros onde as informações de diagnóstico específicas podem ser fornecidas como parte do encerramento.
* `TaskSubmitter.cs`: Esta classe é responsável tooadding tarefas retornadas por um trabalho em lotes do hello trabalho divisor toohello. classe de JobManager Olá agrega sequência Olá das tarefas em lotes para o trabalho de toohello adição eficiente, mas em tempo hábil, em seguida, chama TaskSubmitter.SubmitTasks em um thread em segundo plano para cada lote.

**Divisor de trabalho**

`JobSplitter.cs`: Essa classe contém a lógica específica do aplicativo para dividir o trabalho de saudação em tarefas. estrutura Hello invoca Olá JobSplitter.Split método tooobtain uma sequência de tarefas, que adiciona trabalho toohello como método hello retorna-los. Isso é classe Olá onde você será injetar lógica de saudação do seu trabalho. Implemente Olá divisão método tooreturn uma sequência de instâncias de CloudTask que representam tarefas Olá no qual você deseja que o trabalho de saudação toopartition.

**Arquivos de projeto de linha de comando .NET padrão**

* `App.config`: arquivo de configuração padrão de aplicativo .NET.
* `Packages.config`: arquivo de dependência padrão do pacote NuGet.
* `Program.cs`: Contém o ponto de entrada de programa hello e manipulação de exceção de nível superior.

### <a name="implementing-hello-job-splitter"></a>Implementando o divisor de trabalho Olá
Quando você abre um projeto de modelo do Gerenciador de trabalhos hello, o projeto Olá terá Olá JobSplitter.cs arquivo aberta por padrão. Você pode implementar Olá dividir lógica para tarefas de Olá na carga de trabalho usando mostrados do método split () Olá abaixo:

```csharp
/// <summary>
/// Gets hello tasks into which toosplit hello job. This is where you inject
/// your application-specific logic for decomposing hello job into tasks.
///
/// hello job manager framework invokes hello Split method for you; you need
/// only tooimplement it, not toocall it yourself. Typically, your
/// implementation should return tasks lazily, for example using a C#
/// iterator and hello "yield return" statement; this allows tasks toobe added
/// and toostart running while splitting is still in progress.
/// </summary>
/// <returns>hello tasks toobe added toohello job. Tasks are added automatically
/// by hello job manager framework as they are returned by this method.</returns>
public IEnumerable<CloudTask> Split()
{
    // Your code for hello split logic goes here.
    int startFrame = Convert.ToInt32(_parameters["StartFrame"]);
    int endFrame = Convert.ToInt32(_parameters["EndFrame"]);

    for (int i = startFrame; i <= endFrame; i++)
    {
        yield return new CloudTask("myTask" + i, "cmd /c dir");
    }
}
```

> [!NOTE]
> Olá anotado seção Olá `Split()` método é somente seção Olá Olá código de modelo do Gerenciador de trabalhos que é destinado para você toomodify adicionando Olá lógica toosplit seus trabalhos para tarefas diferentes. Se você quiser toomodify uma seção diferente do modelo hello, verifique se você é trazido com como funciona o lote e experimentar algumas das Olá [exemplos de código do lote][github_samples].
> 
> 

Sua implementação de Split() tem acesso a:

* Olá parâmetros do trabalho, via Olá `_parameters` campo.
* Olá CloudJob objeto representando trabalho hello, por meio de saudação `_job` campo.
* Olá CloudTask objeto representando tarefa do Gerenciador de trabalho hello, por meio de saudação `_jobManagerTask` campo.

O `Split()` implementação não precisa de trabalho de toohello tooadd tarefas diretamente. Em vez disso, seu código deve retornar uma sequência de objetos CloudTask, e eles serão adicionados toohello trabalho automaticamente pelas classes de framework Olá que invocam divisor de trabalho hello. É comum iterador de toouse do # (`yield return`) tooimplement divisores de trabalho de recursos, como isso permite Olá toostart de tarefas em execução assim que possível em vez de aguardar toobe de todas as tarefas calculados.

**Falha do divisor de trabalho**

Se o divisor de trabalho encontrar um erro, ele deverá:

* Encerrar a sequência de saudação usando Olá c# `yield break` instrução, em que o Gerenciador de trabalhos Olá caso será tratado com êxito; ou
* Gera uma exceção, no qual o Gerenciador de trabalhos Olá caso será tratado como falha e pode ser repetido dependendo de como o cliente Olá tiver configurado).

Em ambos os casos, todas as tarefas já retornado pelo separador de trabalho hello e trabalho em lotes de toohello adicionado será toorun qualificado. Se não quiser que esta toohappen, em seguida, você pode:

* Encerrar trabalho Olá antes de retornar de separador de trabalho Olá
* Formular a coleção de tarefas inteira Olá antes de retorná-lo (ou seja, retornar um `ICollection<CloudTask>` ou `IList<CloudTask>` em vez de implementar o divisor de trabalho usando um iterador de c#)
* Use a tarefa dependências toomake que dependem de todas as tarefas após a conclusão bem-sucedida do Gerenciador de trabalhos Olá Olá

**Novas tentativas do Gerenciador de trabalho**

Se o Gerenciador de trabalhos Olá falhar, pode ser repetida pelo serviço de lote Olá dependendo das configurações de repetição de cliente hello. Em geral, isso é seguro, porque quando framework Olá adiciona o trabalho de toohello de tarefas, ele ignora as tarefas que já existem. No entanto, se o cálculo de tarefas é cara, não poderá tooincur custo de saudação do recálculo tarefas que já foram adicionadas toohello trabalho; Por outro lado, se executar novamente a saudação é toogenerate não garantida Olá mesmas IDs de tarefa e o comportamento de 'Ignorar duplicatas' hello não será iniciada. Nesses casos, você deve projetar seu trabalho divisor toodetect Olá um trabalho que já foi feito e não repita, por exemplo, executando um CloudJob.ListTasks antes de iniciar tarefas tooyield.

### <a name="exit-codes-and-exceptions-in-hello-job-manager-template"></a>Códigos e exceções no modelo do Gerenciador de trabalhos de saudação de saída
Códigos de saída e as exceções fornecem um resultado de saudação do toodetermine mecanismo de execução de um programa, e eles podem ajudar tooidentify quaisquer problemas com a execução de saudação do programa de saudação. modelo do Gerenciador de trabalhos Olá implementa os códigos de saída de hello e exceções descritas nesta seção.

Uma tarefa do Gerenciador de trabalho que é implementada com o modelo do Gerenciador de trabalhos Olá pode retornar três códigos de saída possíveis:

| Código | Descrição |
| --- | --- |
| 0 |Gerenciador de trabalhos Olá foi concluído com êxito. O código do divisor de trabalho foi executado toocompletion e todas as tarefas foram adicionadas toohello trabalho. |
| 1 |tarefa do Gerenciador de trabalho Olá falhou com uma exceção em uma parte 'esperada' do programa de saudação. exceção Olá foi traduzida tooa JobManagerException com informações de diagnóstico e, quando possível, sugestões para resolver Olá falha. |
| 2 |tarefa do Gerenciador de trabalho Olá falhou com uma exceção 'inesperada'. exceção Hello era toostandard conectado de saída, mas o Gerenciador de trabalhos Olá tooadd não é possível quaisquer informações adicionais de diagnóstico ou correção. |

No caso de saudação de falha de tarefa do Gerenciador de trabalho, algumas tarefas podem ainda ter sido adicionadas toohello serviço antes de saudação erro. Essas tarefas serão executadas normalmente. Consulte "Falha do divisor de trabalho" acima para conferir uma discussão desse caminho de código.

Todas as informações de saudação retornadas por exceções são gravadas em arquivos do stderr.txt e stdout.txt. Para saber mais, confira [Manipulação de erro](batch-api-basics.md#error-handling).

### <a name="client-considerations"></a>Considerações do cliente
Esta seção descreve alguns requisitos de implementação do cliente ao invocar um Gerenciador de trabalho com base nesse modelo. Consulte [como toopass parâmetros e variáveis de ambiente Olá código do cliente](#pass-environment-settings) para obter detalhes sobre como passar parâmetros e configurações de ambiente.

**Credenciais obrigatórias**

Em ordem tooadd tarefas toohello do Azure Batch trabalho tarefa do Gerenciador de trabalho Olá requer a URL de conta de lote do Azure e a chave. Você deve passá-la nas variáveis de ambiente chamadas YOUR_BATCH_URL e YOUR_BATCH_KEY. Você pode defini-los no hello Gerenciador de trabalho configurações de ambiente de tarefas. Por exemplo, em um cliente C#:

```csharp
job.JobManagerTask.EnvironmentSettings = new [] {
    new EnvironmentSetting("YOUR_BATCH_URL", "https://account.region.batch.azure.com"),
    new EnvironmentSetting("YOUR_BATCH_KEY", "{your_base64_encoded_account_key}"),
};
```
**Credenciais de armazenamento**

Normalmente, Olá cliente não necessita de tooprovide Olá armazenamento vinculado conta credenciais toohello trabalho tarefa do Gerenciador de porque o (a) a maioria dos gerenciadores de trabalho não é necessário para a conta de armazenamento tooexplicitly acesso Olá vinculado e (b) hello conta de armazenamento vinculada geralmente é fornecida tooall tarefas como a configuração de ambiente comum de trabalho hello. Se você não fornecer Olá vinculado a conta de armazenamento por meio de configurações comuns do ambiente Olá e o Gerenciador de trabalhos Olá requer acesso toolinked armazenamento, você deve fornecer as credenciais de armazenamento Olá vinculado da seguinte maneira:

```csharp
job.JobManagerTask.EnvironmentSettings = new [] {
    /* other environment settings */
    new EnvironmentSetting("LINKED_STORAGE_ACCOUNT", "{storageAccountName}"),
    new EnvironmentSetting("LINKED_STORAGE_KEY", "{storageAccountKey}"),
};
```

**Configurações da tarefa do Gerenciador de trabalho**

cliente Olá deve definir o Gerenciador de trabalhos Olá *killJobOnCompletion* sinalizador muito**false**.

Geralmente é seguro para Olá cliente tooset *runExclusive* muito**false**.

cliente de saudação deve usar o hello *resourceFiles* ou *applicationPackageReferences* toohave Olá trabalho Gerenciador da coleção de executáveis (e suas DLLs necessárias) implantado toohello do nó de computação.

Por padrão, o Gerenciador de trabalhos Olá não será repetido se ele falhar. Dependendo de sua lógica de Gerenciador de trabalho, cliente Olá seja tooenable repetições via *restrições*/*maxTaskRetryCount*.

**Configurações do trabalho**

Se o divisor de trabalho Olá emite tarefas com dependências, o cliente de saudação deve definir tootrue de usesTaskDependencies do trabalho hello.

No modelo de divisão de trabalho Olá, é incomum para clientes toowish tooadd tarefas toojobs além divisor de trabalho que Olá cria. cliente Hello, portanto, normalmente deve definir do trabalho Olá *onAllTasksComplete* muito**terminatejob**.

## <a name="task-processor-template"></a>Modelo de Processador de tarefas
Um modelo de processador de tarefa ajuda tooimplement um processador de tarefa que pode executar Olá ações a seguir:

* Configure informações de saudação exigidas por cada toorun de tarefa de lote.
* Executar todas as ações exigidas por cada tarefa do Lote.
* Salve as saídas de tarefa toopersistent armazenamento.

Embora um processador de tarefa não seja necessário toorun tarefas em lote, a vantagem de chave de saudação do uso de um processador de tarefa é que ele fornece um wrapper tooimplement todas as ações de execução de tarefas em um local. Por exemplo, se você precisar toorun vários aplicativos no contexto de saudação de cada tarefa, ou se você precisar de armazenamento de toopersistent toocopy dados após a conclusão de cada tarefa.

ações de saudação executadas pelo processador de tarefa Olá podem ser como simples ou complexos e muitos ou poucos, conforme exigido por sua carga de trabalho. Além disso, com a implementação de todas as ações de tarefas em um processador de tarefa, você pode prontamente atualizar ou adicionar ações com base nos requisitos de tooapplications ou carga de trabalho de alterações. No entanto, em alguns casos um processador de tarefa não pode ser Olá a solução ideal para sua implementação como ela pode adicionar complexidade desnecessária, por exemplo, ao executar trabalhos que podem ser iniciados rapidamente de uma linha de comando simple.

### <a name="create-a-task-processor-using-hello-template"></a>Criar um processador de tarefa usando o modelo de saudação
tooadd uma solução de toohello de processador da tarefa que você criou anteriormente, siga estas etapas:

1. Abra sua solução existente no Visual Studio.
2. No Gerenciador de soluções, solução de saudação com o botão direito, clique em **adicionar**e, em seguida, clique em **novo projeto**.
3. No **Visual C#**, clique em **Nuvem** e em **Processador de Tarefas do Lote do Azure**.
4. Digite um nome que descreva o aplicativo e identifica este projeto como hello (por exemplo, o processador de tarefa "ProcessadorDeTarefasLitware").
5. projeto de saudação toocreate, clique em **Okey**.
6. Finalmente, referenciado de compilação Olá projeto tooforce Visual Studio tooload todos os pacotes do NuGet e tooverify que Olá projeto é válido antes de começar a modificá-lo.

### <a name="task-processor-template-files-and-their-purpose"></a>Arquivos do modelo do Processador de tarefas e suas finalidades
Quando você cria um projeto usando o modelo de processador de tarefa hello, ele gera três grupos de arquivos de código:

* arquivo de programa principal Hello (Program.cs). Ele contém o ponto de entrada de programa hello e manipulação de exceção de nível superior. Você normalmente não precisa toomodify isso.
* diretório do Framework Hello. Isso contém arquivos de saudação responsáveis pelo trabalho 'padrão' hello pelo programa de Gerenciador de trabalho hello – desempacotar parâmetros, adicionando o trabalho de lote de toohello de tarefas, etc. Você normalmente não precisa toomodify esses arquivos.
* arquivo do processador de tarefa Hello (TaskProcessor.cs). Isso é onde você colocará sua lógica específica do aplicativo para executar uma tarefa (normalmente ao chamar executável existente tooan). Código de pré e pós-processamento, como o download dos dados adicionais ou upload de arquivos de resultados, também é colocado nesse local.

Obviamente você pode adicionar arquivos adicionais como toosupport necessário seu código de processador de tarefas, dependendo da complexidade de saudação do trabalho Olá divisão lógica.

modelo de saudação também gera arquivos de projeto padrão do .NET como um arquivo. csproj App. config, Packages, etc.

restante Olá desta seção descreve Olá diferentes arquivos e sua estrutura de código e explica o que faz cada classe.

![Visual Studio Gerenciador de soluções mostrando a solução de modelo de processador de tarefa Olá][solution_explorer02]

**Arquivos do Framework**

* `Configuration.cs`: Encapsula o carregamento de saudação de dados de configuração de trabalho, como detalhes da conta, as credenciais de conta de armazenamento vinculada, informações de trabalhos e tarefas e parâmetros do trabalho em lotes. Ele também fornece acesso definido tooBatch as variáveis de ambiente (consulte as configurações de ambiente para tarefas, na documentação do lote Olá) por meio da classe Configuration.EnvironmentVariable hello.
* `IConfiguration.cs`: Resumo Olá implementação de classe de configuração de hello, para que você possa de teste de unidade o divisor de trabalho usando um objeto de configuração falsas ou fictícias.
* `TaskProcessorException.cs`Representa um erro que exige Olá tooterminate de Gerenciador de trabalho. TaskProcessorException é usado toowrap 'esperado' erros onde as informações de diagnóstico específicas podem ser fornecidas como parte do encerramento.

**Processador de tarefas**

* `TaskProcessor.cs`: Executa a tarefa de saudação. estrutura Olá invoca o método de TaskProcessor.Run de saudação. Isso é a classe Olá onde você irá injetar a lógica de específicas do aplicativo hello da tarefa. Implemente o método de execução de saudação:
  * Analisar e validar qualquer parâmetro de tarefa
  * Compor Olá linha de comando para qualquer programa externo, você deseja tooinvoke
  * Registrar quaisquer informações de diagnóstico que você possa precisar para fins de depuração
  * Iniciar um processo usando a linha de comando
  * Aguarde a saudação processo tooexit
  * Capturar o código de saída de saudação do hello processo toodetermine se ela teve êxito ou falha
  * Salve os arquivos de saída que você deseja tookeep toopersistent armazenamento

**Arquivos de projeto de linha de comando .NET padrão**

* `App.config`: arquivo de configuração padrão de aplicativo .NET.
* `Packages.config`: arquivo de dependência padrão do pacote NuGet.
* `Program.cs`: Contém o ponto de entrada de programa hello e manipulação de exceção de nível superior.

## <a name="implementing-hello-task-processor"></a>Implementando o processador de tarefa Olá
Quando você abre um projeto de modelo de processador de tarefa hello, o projeto Olá terá Olá TaskProcessor.cs arquivo aberta por padrão. Você pode implementar lógica Olá executar tarefas de saudação na carga de trabalho, usando o método Run () de hello mostrado abaixo:

```csharp
/// <summary>
/// Runs hello task processing logic. This is where you inject
/// your application-specific logic for decomposing hello job into tasks.
///
/// hello task processor framework invokes hello Run method for you; you need
/// only tooimplement it, not toocall it yourself. Typically, your
/// implementation will execute an external program (from resource files or
/// an application package), check hello exit code of that program and
/// save output files toopersistent storage.
/// </summary>
public async Task<int> Run()

{
    try
    {
        //Your code for hello task processor goes here.
        var command = $"compare {_parameters["Frame1"]} {_parameters["Frame2"]} compare.gif";
        using (var process = Process.Start($"cmd /c {command}"))
        {
            process.WaitForExit();
            var taskOutputStorage = new TaskOutputStorage(
            _configuration.StorageAccount,
            _configuration.JobId,
            _configuration.TaskId
            );
            await taskOutputStorage.SaveAsync(
            TaskOutputKind.TaskOutput,
            @"..\stdout.txt",
            @"stdout.txt"
            );
            return process.ExitCode;
        }
    }
    catch (Exception ex)
    {
        throw new TaskProcessorException(
        $"{ex.GetType().Name} exception in run task processor: {ex.Message}",
        ex
        );
    }
}
```
> [!NOTE]
> Hello anotada seção Olá método Run () é a seção apenas saudação do código de modelo de processador de tarefa Olá que é destinado para você toomodify adicionando lógica Olá executar tarefas Olá na carga de trabalho. Se você quiser toomodify uma seção diferente do modelo hello,. primeiro estar familiarizado com como lote funciona por revisar a documentação de lote hello e experimentar alguns dos exemplos de código de lote de saudação.
> 
> 

Olá método Run () é responsável por iniciando a linha de comando hello, iniciando um ou mais processos, aguardando todos os toocomplete de processo, salvar os resultados da saudação e finalmente retornar com um código de saída. Olá método Run () é onde você pode implementar Olá lógica para suas tarefas de processamento. a estrutura de processador tarefas Olá invoca o método de Run () do hello para você. não é necessário toocall-lo por conta própria.

Sua implementação de Run() tem acesso a:

* Olá parâmetros da tarefa, por meio de saudação `_parameters` campo.
* Olá ids de trabalho e tarefa, por meio de saudação `_jobId` e `_taskId` campos.
* configuração da tarefa Hello, por meio de saudação `_configuration` campo.

**Falha da tarefa**

Em caso de falha, será possível sair do método Run () de hello lançando uma exceção, mas isso deixa o manipulador de exceção de nível superior de saudação no controle do código de saída de tarefa hello. Se precisar de código de saída de hello toocontrol para que você possa distinguir diferentes tipos de falha, por exemplo para fins de diagnóstico ou porque alguns modos de falha devem encerrar trabalho hello e outros não devem, você deve sair do método do hello Run (), retornando um código de saída diferente de zero. Isso torna-se o código de saída de tarefa hello.

### <a name="exit-codes-and-exceptions-in-hello-task-processor-template"></a>Sair de códigos e exceções no modelo de processador de tarefa Olá
Códigos de saída e exceções fornecem um resultado de saudação do toodetermine mecanismo de execução de um programa, e eles ajudam a identificar problemas com a execução de saudação do programa de saudação. modelo de processador de tarefa Olá implementa os códigos de saída de hello e exceções descritas nesta seção.

Uma tarefa de processador que é implementada com o modelo de processador de tarefa Olá pode retornar três códigos de saída possíveis:

| Código | Descrição |
| --- | --- |
| [Process.ExitCode][process_exitcode] |processador de tarefa de saudação ficou toocompletion. Observe que isso não significa que você chamou o programa hello foi bem-sucedida – apenas esse processador de tarefa Olá invocou com êxito e executada de qualquer pós-processamento sem exceções. significado de saudação do código de saída de hello depende do programa de saudação invocado – normalmente código de saída 0 significa êxito do programa hello e significa que qualquer outro código de saída Olá programa falhou. |
| 1 |processador de tarefa Olá falhou com uma exceção em uma parte 'esperada' do programa de saudação. exceção Hello foi traduzida tooa `TaskProcessorException` com informações de diagnóstico e, quando possível, sugestões para resolver Olá falha. |
| 2 |processador de tarefa Olá falhou com uma exceção 'inesperada'. exceção Hello era toostandard conectado de saída, mas processador de tarefa Olá tooadd não é possível quaisquer informações adicionais de diagnóstico ou correção. |

> [!NOTE]
> Se o programa hello que invocar usa modos de falha específico de tooindicate de códigos de 1 e 2 de saída, usando códigos de saída 1 e 2 para erros de processador da tarefa é ambíguo. Você pode alterar esses códigos de saída de toodistinctive tarefa processador erro códigos editando os casos de exceção Olá no arquivo Program.cs de saudação.
> 
> 

Todas as informações de saudação retornadas por exceções são gravadas em arquivos do stderr.txt e stdout.txt. Para obter mais informações, consulte o tratamento de erros, Olá documentação do lote.

### <a name="client-considerations"></a>Considerações do cliente
**Credenciais de armazenamento**

Se o processador de tarefa utiliza saídas toopersist de armazenamento de BLOBs do Azure, biblioteca auxiliar da saudação arquivo convenções, por exemplo, usando, em seguida, ele precisa acessar muito*ou* Olá credenciais de conta de armazenamento de nuvem *ou* uma URL de contêiner de blob que inclui uma assinatura de acesso compartilhado (SAS). modelo de saudação inclui suporte para fornecer as credenciais por meio de variáveis de ambiente comuns. O cliente pode passar as credenciais de armazenamento de saudação da seguinte maneira:

```csharp
job.CommonEnvironmentSettings = new [] {
    new EnvironmentSetting("LINKED_STORAGE_ACCOUNT", "{storageAccountName}"),
    new EnvironmentSetting("LINKED_STORAGE_KEY", "{storageAccountKey}"),
};
```

conta de armazenamento Hello está disponível em Olá TaskProcessor classe via Olá `_configuration.StorageAccount` propriedade.

Se você preferir toouse uma URL de contêiner com SAS, você também pode passar isso por meio de uma configuração de ambiente comum de trabalho, mas o modelo de processador Olá tarefas atualmente não incluem suporte interno para este.

**Configuração de armazenamento**

É recomendável que tarefa do Gerenciador de trabalho ou cliente Olá Crie qualquer contêiner exigido pelas tarefas antes de adicionar o trabalho de toohello tarefas hello. Isso é obrigatório que se você usar uma URL de contêiner com SAS, assim uma URL não inclui permissão toocreate Olá contêiner. É recomendável mesmo se você passar credenciais de conta de armazenamento, como ele salva todas as tarefas com toocall CloudBlobContainer.CreateIfNotExistsAsync no contêiner de saudação.

## <a name="pass-parameters-and-environment-variables"></a>Passar parâmetros e variáveis de ambiente
### <a name="pass-environment-settings"></a>Passar configurações de ambiente
Um cliente pode passar a tarefa do Gerenciador de trabalho do informações toohello na forma de saudação de configurações de ambiente. Essas informações podem, em seguida, usadas pela tarefa do Gerenciador de trabalho hello quando o trabalho de computação gerando Olá processador tarefas que serão executado como parte da saudação. Exemplos de informações de saudação que você pode passar como configurações de ambiente são:

* Nome da conta de armazenamento e chaves da conta
* URL da conta do Lote
* Chave da conta do Lote

Olá serviço de lote tem uma tarefa de Gerenciador mecanismo simples toopass ambiente configurações tooa trabalho usando Olá `EnvironmentSettings` propriedade [Microsoft.Azure.Batch.JobManagerTask][net_jobmanagertask].

Por exemplo, tooget Olá `BatchClient` instância para uma conta de lote, você pode passar como variáveis de ambiente do cliente Olá código Olá URL e credenciais de chave para a conta do lote Olá compartilhadas. Da mesma forma, conta de armazenamento do hello tooaccess é vinculada toohello conta de lote, você pode passar o nome de conta de armazenamento hello e chave de conta de armazenamento hello como variáveis de ambiente.

### <a name="pass-parameters-toohello-job-manager-template"></a>Passar o modelo do Gerenciador de trabalho de toohello de parâmetros
Em muitos casos, é útil toopass por trabalho parâmetros toohello trabalho tarefa do Gerenciador, o trabalho de saudação toocontrol dividindo o processo ou tarefas de saudação tooconfigure para Olá trabalho. Você pode fazer isso, carregando um arquivo JSON chamado parameters.json como um arquivo de recurso para a tarefa do Gerenciador de trabalho hello. Olá parâmetros, em seguida, podem se tornar disponíveis no hello `JobSplitter._parameters` campo no modelo do Gerenciador de trabalhos de saudação.

> [!NOTE]
> manipulador de parâmetro internas Olá oferece suporte a apenas os dicionários de cadeia de caracteres de cadeia de caracteres. Se você quiser toopass valores complexos de JSON como valores de parâmetro, será necessário toopass como cadeias de caracteres e analisá-los no separador de trabalho hello ou modificar a estrutura de saudação `Configuration.GetJobParameters` método.
> 
> 

### <a name="pass-parameters-toohello-task-processor-template"></a>Passar o modelo de processador de tarefa toohello parâmetros
Você também pode passar parâmetros tooindividual tarefas implementada usando o modelo de processador de tarefa hello. Assim como com o modelo do Gerenciador de trabalho hello, Olá tarefa processador modelo procura um arquivo de recurso denominado

Parameters.JSON e se encontrado, ele carrega-os como dicionário de parâmetros de saudação. Há duas opções para como toopass parâmetros toohello tarefas do processador de tarefas:

* Reutilize os parâmetros do trabalho Olá JSON. Isso funciona bem se apenas os parâmetros Olá são aqueles de todo o trabalho (por exemplo, uma renderização de altura e largura). toodo isso, ao criar um CloudTask no separador de trabalho hello, adicionar um objeto de arquivo de recurso do referência toohello parameters.json de ResourceFiles da tarefa do Gerenciador trabalho hello (`JobSplitter._jobManagerTask.ResourceFiles`) coleta de ResourceFiles do toohello CloudTask.
* Gerar e carregar um documento de parameters.json específicos da tarefa como parte da execução do divisor de trabalho e fazer referência a esse blob na coleção de arquivos de recursos da tarefa de saudação. Isso é necessário se tarefas diferentes tiverem parâmetros diferentes. Um exemplo seria um cenário de renderização 3D onde o índice do quadro de saudação é passado toohello tarefa como um parâmetro.

> [!NOTE]
> manipulador de parâmetro internas Olá oferece suporte a apenas os dicionários de cadeia de caracteres de cadeia de caracteres. Se você quiser toopass valores complexos de JSON como valores de parâmetro, será necessário toopass como cadeias de caracteres e analisá-los no processador de tarefa hello ou modificar a estrutura de saudação `Configuration.GetTaskParameters` método.
> 
> 

## <a name="next-steps"></a>Próximas etapas
### <a name="persist-job-and-task-output-tooazure-storage"></a>Manter o trabalho e saída tooAzure armazenamento de tarefas
Outra ferramenta útil no desenvolvimento de soluções do Lote são as [Convenções de Arquivo do Lote do Azure][nuget_package]. Use essa biblioteca de classes do .NET (atualmente na visualização) em seu repositório de tooeasily de aplicativos .NET em lotes e recuperar tooand de saídas de tarefa do armazenamento do Azure. [Manter a saída de trabalho e tarefa de lote do Azure](batch-task-output.md) contém uma discussão completa sobre a biblioteca de saudação e seu uso.

### <a name="batch-forum"></a>Fórum do Lote
Olá [Fórum do lote do Azure] [ forum] no MSDN é um ótimo colocar toodiscuss em lotes e fazer perguntas sobre o serviço de saudação. Acesse diretamente as postagens “fixas” úteis e poste suas dúvidas conforme elas surgirem enquanto você cria suas soluções do Lote.

[forum]: https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=azurebatch
[net_jobmanagertask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobmanagertask.aspx
[github_samples]: https://github.com/Azure/azure-batch-samples
[nuget_package]: https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files
[process_exitcode]: https://msdn.microsoft.com/library/system.diagnostics.process.exitcode.aspx
[vs_gallery]: https://visualstudiogallery.msdn.microsoft.com/
[vs_gallery_templates]: https://go.microsoft.com/fwlink/?linkid=820714
[vs_find_use_ext]: https://msdn.microsoft.com/library/dd293638.aspx

[diagram01]: ./media/batch-visual-studio-templates/diagram01.png
[solution_explorer01]: ./media/batch-visual-studio-templates/solution_explorer01.png
[solution_explorer02]: ./media/batch-visual-studio-templates/solution_explorer02.png
