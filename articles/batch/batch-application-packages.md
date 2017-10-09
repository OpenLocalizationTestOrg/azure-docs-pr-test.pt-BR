---
title: "pacotes de aplicativos aaaInstall em nós de computação - lote do Azure | Microsoft Docs"
description: "Recurso de pacotes de aplicativos Use saudação do lote do Azure tooeasily gerenciar vários aplicativos e nós de computação de versões para instalação em lote."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 3b6044b7-5f65-4a27-9d43-71e1863d16cf
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 683be7b7f1bd5db7835332016f6dccb72f45c3b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-applications-toocompute-nodes-with-batch-application-packages"></a>Implantar aplicativos toocompute nós com pacotes de aplicativos de lote

recurso de pacotes de aplicativos de saudação do lote do Azure fornece fácil gerenciamento de aplicativos de tarefa e sua implantação toohello nós de computação em seu pool. Com pacotes de aplicativos, você pode carregar e gerenciar várias versões de aplicativos Olá que executar suas tarefas, incluindo seus arquivos de suporte. Automaticamente, em seguida, pode implantar um ou mais desses aplicativos toohello nós de computação em seu pool.

Neste artigo, você aprenderá como tooupload e gerenciar pacotes de aplicativos no hello portal do Azure. Em seguida, você aprenderá como tooinstall-los em um pool nós de computação com hello [Batch .NET] [ api_net] biblioteca.

> [!NOTE]
> 
> Os pacotes de aplicativos têm suporte em todos os pools do Lote criados após 5 de julho de 2017. Eles têm suporte em pools de lote criados entre 10 de março de 2016 e 5 de julho de 2017 somente se o pool de saudação foi criado usando uma configuração de serviço de nuvem. Pools de lote criados too10 anterior de março de 2016 não dão suporte a pacotes de aplicativos.
>
> Olá, APIs para criar e gerenciar pacotes de aplicativos fazem parte da saudação [Batch Management .NET] [[api_net_mgmt]] biblioteca. APIs para instalar os pacotes de aplicativo em um nó de computação Hello fazem parte da saudação [Batch .NET] [ api_net] biblioteca.  
>
> recurso de pacotes de aplicativo Hello descrito aqui substitui o recurso de aplicativos em lotes Olá disponível em versões anteriores do serviço de saudação.
> 
> 

## <a name="application-package-requirements"></a>Requisitos do pacote de aplicativos
pacotes de aplicativos toouse, é necessário muito[vincular uma conta de armazenamento do Azure](#link-a-storage-account) tooyour conta do lote.

Este recurso foi introduzido no [API REST do lote] [ api_rest] versão 2015-12-01.2.2 e Olá correspondente [Batch .NET] [ api_net] versão da biblioteca 3.1.0. É recomendável que você sempre use mais recente versão da API Olá ao trabalhar com o lote.

> [!NOTE]
> Os pacotes de aplicativos têm suporte em todos os pools do Lote criados após 5 de julho de 2017. Eles têm suporte em pools de lote criados entre 10 de março de 2016 e 5 de julho de 2017 somente se o pool de saudação foi criado usando uma configuração de serviço de nuvem. Pools de lote criados too10 anterior de março de 2016 não dão suporte a pacotes de aplicativos.
>
>

## <a name="about-applications-and-application-packages"></a>Sobre aplicativos e pacotes de aplicativos
Em lote do Azure, uma *aplicativo* refere-se o conjunto de tooa de binários com controle de versão que podem ser baixados automaticamente toohello nós de computação no pool de. Um *pacote de aplicativo* refere-se tooa *conjunto específico* desses binários e representa um determinado *versão* do aplicativo hello.

![Diagrama de alto nível de aplicativos e pacotes de aplicativos][1]

### <a name="applications"></a>Aplicativos
Um aplicativo em lote contém uma ou mais aplicativos, pacotes e especifica opções de configuração para o aplicativo hello. Por exemplo, um aplicativo pode especificar o saudação padrão aplicativo pacote versão tooinstall em nós de computação e se seus pacotes podem ser atualizados ou excluídos.

### <a name="application-packages"></a>pacotes de aplicativos
Um pacote de aplicativo é um arquivo. zip que contém os binários do aplicativo hello e arquivos de suporte que são necessários para seu aplicativo de saudação do toorun de tarefas. Cada pacote de aplicativo representa uma versão específica do aplicativo hello.

Você pode especificar os pacotes de aplicativos em níveis de pool e tarefa hello. Você pode especificar um ou mais desses pacotes e (opcionalmente) uma versão quando você cria uma tarefa ou um pool.

* **Pacotes de aplicativos do pool** são implantados muito*cada* nó no pool de saudação. Os aplicativos são implantados quando um nó ingressa em um pool e quando ele é reinicializado ou tem a imagem recriada.
  
    Os pacotes de aplicativos do pool são adequados quando todos os nós em um pool executam as tarefas de um trabalho. Você pode especificar um ou mais pacotes de aplicativos quando cria um pool e pode adicionar ou atualizar os pacotes de um pool existente. Se você atualizar os pacotes de aplicativos de um pool existente, você deve reiniciar o novo pacote seus nós tooinstall hello.
* **Pacotes de aplicativos de tarefas** são implantados somente do nó de computação tooa toorun um tarefa agendada, apenas antes de executar a linha de comando da tarefa de saudação. Se especificado de saudação versão e o pacote de aplicativo já está no nó de saudação, ele não for reimplantado e pacote existente de saudação é usado.
  
    Pacotes de aplicativos de tarefas são úteis em ambientes de pool compartilhado, onde diferentes trabalhos são executados em um pool e pool de saudação não será excluído quando um trabalho é concluído. Se o trabalho tiver menos tarefas que os nós no pool hello, pacotes de aplicativos de tarefa podem minimizar transferência de dados desde que o aplicativo é implantado toohello apenas nós que executam tarefas.
  
    Outros cenários que podem aproveitar os pacotes de aplicativos de tarefa são os trabalhos que executam um aplicativo grande, mas para um pequeno número de tarefas. Por exemplo, uma fase de pré-processamento ou uma tarefa de mesclagem, onde o aplicativo hello de pré-processamento ou de mesclagem é pesado, pode se beneficiar do uso pacotes de aplicativos de tarefa.

> [!IMPORTANT]
> Há restrições no número de saudação de aplicativos e pacotes de aplicativos dentro de uma conta de lote e no tamanho de pacote de aplicativo máximo hello. Consulte [cotas e limites de saudação do serviço Azure Batch](batch-quota-limit.md) para obter detalhes sobre esses limites.
> 
> 

### <a name="benefits-of-application-packages"></a>Benefícios dos pacotes de aplicativos
Pacotes de aplicativos podem simplificar o código de saudação em sua solução de lote e aplicativos do hello de sobrecarga toomanage necessário Olá inferiores executar suas tarefas.

Com pacotes de aplicativos, tarefas do início do pool não tem toospecify uma longa lista de recursos individuais arquivos tooinstall em nós de saudação. Você não tem toomanually gerenciar várias versões dos seus arquivos de aplicativo no armazenamento do Azure ou em seus nós. E, você não precisa tooworry sobre como gerar [URLs da SAS](../storage/common/storage-dotnet-shared-access-signature-part-1.md) tooprovide acessar toohello arquivos em sua conta de armazenamento. Lote funciona no plano de fundo de saudação com pacotes de aplicativos de toostore de armazenamento do Azure e implantá-las toocompute nós.

> [!NOTE] 
> Olá tamanho total de uma tarefa de início deve ser menor ou igual too32768 caracteres, incluindo arquivos de recurso e variáveis de ambiente. Se a tarefa de inicialização exceder esse limite, usar pacotes de aplicativos é outra opção. Você pode também criar um arquivo compactado que contém os arquivos de recurso, carregá-lo como um blob de tooAzure armazenamento e descompacte-o na linha de comando de saudação da tarefa inicial. 
>
>

## <a name="upload-and-manage-applications"></a>Carregar e gerenciar aplicativos
Você pode usar o hello [portal do Azure] [ portal] ou hello [Batch Management .NET](batch-management-dotnet.md) pacotes de aplicativos de biblioteca toomanage Olá em sua conta do lote. Em seguida Olá seções, primeiro, mostramos como toolink uma conta de armazenamento, em seguida, discuta adicionar aplicativos e pacotes e gerenciá-las com hello portal.

### <a name="link-a-storage-account"></a>Vincular uma conta de armazenamento
toouse pacotes de aplicativos, primeiro você deve vincular uma conta de armazenamento do Azure tooyour conta do lote. Se você ainda não tiver configurado uma conta de armazenamento, hello portal do Azure exibe uma saudação aviso primeira vez que você clicar em Olá **aplicativos** lado a lado no hello **conta de lote** folha.

> [!IMPORTANT]
> Lote atualmente oferece suporte a *somente* Olá **geral** tipo de conta de armazenamento, conforme descrito na etapa 5, [criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account), na [sobre o Azure contas de armazenamento](../storage/common/storage-create-storage-account.md). Vincular ao vincular uma conta de armazenamento do Azure tooyour conta em lotes, *somente* um **geral** conta de armazenamento.
> 
> 

![Aviso de 'Nenhuma conta de armazenamento configurada' no portal do Azure][9]

Olá lote serviço usa Olá associados toostore da conta de armazenamento seus pacotes de aplicativos. Depois de vincular duas contas de hello, lote pode implantar automaticamente pacotes de saudação armazenados em nós de computação tooyour do conta de armazenamento Olá vinculado. toolink uma conta de armazenamento tooyour conta do lote, clique em **configurações de conta de armazenamento** em Olá **aviso** folha e depois clique em **conta de armazenamento** em Olá **Conta de armazenamento** folha.

![Folha Escolher conta de armazenamento no portal do Azure][10]

Recomendamos que você crie uma conta de armazenamento para usar *especificamente* com sua conta do Lote e que a selecione aqui. Para obter detalhes sobre como toocreate uma conta de armazenamento, consulte "Criar uma conta de armazenamento" [contas de armazenamento do Azure sobre](../storage/common/storage-create-storage-account.md). Depois de criar uma conta de armazenamento, você pode, em seguida, vinculá-lo tooyour conta do lote usando Olá **conta de armazenamento** folha.

> [!WARNING]
> Olá serviço de lote usa toostore de armazenamento do Azure seus pacotes de aplicativos como blobs de bloco. Você está [cobrada como normal] [ storage_pricing] para dados de blob de bloco hello. Ter certeza de que tamanho de saudação de tooconsider e número de seus pacotes de aplicativos e remover periodicamente os custos de toominimize pacotes substituídos.
> 
> 

### <a name="view-current-applications"></a>Exibir aplicativos atuais
aplicativos de saudação tooview em sua conta de lote, clique em Olá **aplicativos** item de menu no menu esquerdo de saudação ao exibir hello **conta de lote** folha.

![Bloco Aplicativos][2]

Selecionar essa opção de menu abre Olá **aplicativos** folha:

![Listar aplicativos][3]

Olá **aplicativos** folha exibe Olá ID de cada aplicativo em sua conta e Olá propriedades a seguir:

* **Pacotes**: Olá número de versões associadas a este aplicativo.
* **Versão padrão**: versão do aplicativo hello instalado se você não indica uma versão quando você especificar o aplicativo hello para um pool. Essa configuração é opcional.
* **Permitir atualizações**: valor de saudação que especifica se o pacote de atualizações, exclusões e adições são permitidos. Se isso for definido muito**não**, exclusões e atualizações de pacote estão desabilitadas para o aplicativo hello. Apenas novas versões do pacote de aplicativos poderão ser adicionadas. saudação padrão é **Sim**.

### <a name="view-application-details"></a>Exibir detalhes do aplicativo
folha de saudação tooopen que inclui detalhes de saudação para um aplicativo hello de aplicativo, selecione em Olá **aplicativos** folha.

![Detalhes do aplicativo][4]

Na folha de detalhes do aplicativo hello, você pode configurar Olá seguindo as configurações para seu aplicativo.

* **Permitir atualizações**: especifique se seus pacotes de aplicativos podem ser atualizados ou excluídos. Consulte "Atualizar ou excluir um pacote de aplicativos" mais adiante neste artigo.
* **Versão padrão**: especificar um padrão aplicativo pacote toodeploy toocompute nós.
* **Nome de exibição**: especificar amigável para um nome que sua solução pode usar quando ele exibe informações sobre o aplicativo hello, por exemplo, no hello da interface do usuário de um serviço que você fornecer tooyour clientes por meio de lote de lote.

### <a name="add-a-new-application"></a>Adicionar um novo aplicativo
toocreate um novo aplicativo, adicione um pacote de aplicativos e especifique uma ID de aplicativo nova e exclusiva. Olá primeiro pacote de aplicativos que você adicionar a nova ID de aplicativo hello também cria Olá novo aplicativo.

Clique em **adicionar** em Olá **aplicativos** saudação do folha tooopen **novo aplicativo** folha.

![Folha Novo aplicativo no portal do Azure][5]

Olá **novo aplicativo** folha fornece a seguinte Olá campos toospecify configurações de saudação do seu pacote de aplicativos e o novo aplicativo.

**ID do aplicativo**

Este campo especifica a ID de saudação do seu novo aplicativo, que é o assunto toohello padrão ID de lote do Azure as regras de validação. regras de saudação para fornecer uma ID de aplicativo são da seguinte maneira:

* Em nós do Windows, Olá ID pode conter qualquer combinação de caracteres alfanuméricos, hifens e sublinhados. Em nós do Linux, são permitidos somente caracteres alfanuméricos e sublinhados.
* Não pode conter mais de 64 caracteres.
* Deve ser exclusivo dentro de saudação conta do lote.
* Não diferencia maiúsculas de minúsculas e preserva maiúsculas e minúsculas.

**Versão**

Este campo especifica a versão de Olá Olá do pacote de aplicativo que está carregando. Cadeias de caracteres de versão são toohello assunto regras de validação a seguir:

* Em nós do Windows, a cadeia de caracteres de versão Olá pode conter qualquer combinação de caracteres alfanuméricos, hifens, sublinhados e pontos. Em nós do Linux, a cadeia de caracteres de versão Olá pode conter apenas caracteres alfanuméricos e sublinhados.
* Não pode conter mais de 64 caracteres.
* Deve ser exclusivo dentro do aplicativo hello.
* Não diferenciam maiúsculas de minúsculas e preservam maiúsculas e minúsculas.

**Pacote de aplicativos**

Este campo especifica um arquivo. zip Olá que contém os binários do aplicativo hello e arquivos de suporte que são necessários tooexecute Olá aplicativo. Clique em Olá **selecionar um arquivo** caixa ou hello pasta ícone toobrowse tooand selecionar um arquivo. zip que contém os arquivos do aplicativo.

Depois de selecionar um arquivo, clique em **Okey** toobegin Olá carregamento tooAzure armazenamento. Quando a operação de carregamento de saudação for concluída, o portal de saudação exibe uma notificação e fecha a folha de saudação. Dependendo do tamanho de saudação do arquivo hello que você está carregando e Olá a velocidade de sua conexão de rede, essa operação pode levar algum tempo.

> [!WARNING]
> Não feche Olá **novo aplicativo** folha antes da operação de carregamento de saudação conclusão. Isso irá parar o processo de carregamento de saudação.
> 
> 

### <a name="add-a-new-application-package"></a>Adicionar um novo pacote de aplicativos
tooadd uma nova versão do pacote de aplicativo para um aplicativo existente, selecione um aplicativo no hello **aplicativos** folha, clique em **pacotes**, em seguida, clique em **adicionar** tooopen Olá **Adicionar pacote** folha.

![Folha Adicionar pacote de aplicativos no portal do Azure][8]

Como você pode ver, campos de saudação correspondem da saudação **novo aplicativo** folha, mas Olá **id do aplicativo** caixa está desabilitada. Como você fez para o novo aplicativo de hello, especifique Olá **versão** para o novo pacote, procurar tooyour **pacote de aplicativo** . zip do arquivo, em seguida, clique em **Okey** Olá tooupload pacote.

### <a name="update-or-delete-an-application-package"></a>Atualizar ou excluir um pacote de aplicativos
tooupdate ou excluir um pacote de aplicativo existente, folha de detalhes aberta Olá para o aplicativo hello, clique em **pacotes** tooopen Olá **pacotes** folha, clique em Olá **reticências**na linha de saudação saudação do pacote de aplicativo que você deseja toomodify e selecione Olá ação que você deseja tooperform.

![Atualizar ou excluir pacote no portal do Azure][7]

**Atualizar**

Quando você clica em **atualização**, Olá *pacote de atualização* folha é exibida. Esta folha é semelhante toohello *novo pacote de aplicativo* folha, no entanto, somente o campo seleção do pacote hello estiver habilitado, permitindo que você toospecify um novo tooupload de arquivo ZIP.

![Folha do pacote de atualização no portal do Azure][11]

**Excluir**

Quando você clica em **excluir**, você será solicitado a exclusão da versão do pacote de saudação Olá tooconfirm e lote exclui o pacote de saudação do armazenamento do Azure. Se você excluir a versão padrão de saudação de um aplicativo, Olá **versão padrão** configuração é removida para o aplicativo hello.

![Excluir aplicativo ][12]

## <a name="install-applications-on-compute-nodes"></a>Instalar aplicativos em nós de computação
Agora que você aprendeu como o aplicativo toomanage pacotes com hello portal do Azure, podemos discutir como toodeploy-los toocompute nós e executá-los com as tarefas em lote.

### <a name="install-pool-application-packages"></a>Instalar pacotes de aplicativos do pool
tooinstall um pacote de aplicativo em todos os nós de computação em um pool, especifique um ou mais pacotes de aplicativo *referências* para pool de saudação. pacotes de aplicativos de saudação que você especificar para um pool são instalados em cada nó de computação ao nó une pool hello e ao nó de saudação é reinicializado ou recriar a imagem.

No .NET do Lote, especifique um ou mais [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref] quando você criar um novo pool ou para um pool existente. Olá [ApplicationPackageReference] [ net_pkgref] classe especifica uma ID de aplicativo e a versão tooinstall em um pool de nós de computação.

```csharp
// Create hello unbound CloudPool
CloudPool myCloudPool =
    batchClient.PoolOperations.CreatePool(
        poolId: "myPool",
        targetDedicatedComputeNodes: 1,
        virtualMachineSize: "small",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

// Specify hello application and version tooinstall on hello compute nodes
myCloudPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "litware",
        Version = "1.1001.2b" }
};

// Commit hello pool so that it's created in hello Batch service. As hello nodes join
// hello pool, hello specified application package is installed on each.
await myCloudPool.CommitAsync();
```

> [!IMPORTANT]
> Se uma implantação de pacote do aplicativo falhar por algum motivo, marcas de serviço de lote Olá Olá nó [inutilizável][net_nodestate], e nenhum tarefas estão agendadas para execução nesse nó. Nesse caso, você deve **reiniciar** Olá implantação de pacote de saudação do nó tooreinitiate. Nó de saudação reiniciar também permite que agendamento de tarefas no nó Olá novamente.
> 
> 

### <a name="install-task-application-packages"></a>Instalar pacotes de aplicativos de tarefa
Pool tooa semelhante, que você especifique o pacote de aplicativos *referências* para uma tarefa. Quando uma tarefa está agendada toorun em um nó, pacote de saudação é baixado e extraído antes de linha de comando da tarefa Olá é executada. Se um pacote especificado e a versão já estiver instalado no nó hello, pacote de saudação não é baixado e pacote existente Olá é usado.

tooinstall um pacote de aplicativo de tarefas, configurar da tarefa Olá [CloudTask][net_cloudtask].[ ApplicationPackageReferences] [ net_cloudtask_pkgref] propriedade:

```csharp
CloudTask task =
    new CloudTask(
        "litwaretask001",
        "cmd /c %AZ_BATCH_APP_PACKAGE_LITWARE%\\litware.exe -args -here");

task.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference
    {
        ApplicationId = "litware",
        Version = "1.1001.2b"
    }
};
```

## <a name="execute-hello-installed-applications"></a>Executar aplicativos Olá instalado
Hello pacotes que você especificou para uma tarefa ou um pool são baixados e extraídos tooa chamado diretório dentro de saudação `AZ_BATCH_ROOT_DIR` do nó de saudação. Lote também cria uma variável de ambiente que contém a saudação caminho toohello chamado de diretório. As linhas de comando da tarefa use essa variável de ambiente ao referenciar o aplicativo hello no nó de saudação. 

Em nós do Windows, a variável de saudação está no hello formato a seguir:

```
Windows:
AZ_BATCH_APP_PACKAGE_APPLICATIONID#version
```

Em nós do Linux, o formato de saudação é ligeiramente diferente. Pontos (.), hifens (-) e sinais numéricos (#) são toounderscores bidimensional na variável de ambiente hello. Por exemplo:

```
Linux:
AZ_BATCH_APP_PACKAGE_APPLICATIONID_version
```

`APPLICATIONID`e `version` são valores que correspondem a toohello aplicativo e a versão do pacote que você especificou para implantação. Por exemplo, se você tiver especificado que a versão 2.7 do aplicativo *blender* devem ser instalados em nós do Windows, as linhas de comando da tarefa usaria essa tooaccess de variável de ambiente seus arquivos:

```
Windows:
AZ_BATCH_APP_PACKAGE_BLENDER#2.7
```

Em nós do Linux, especifique a variável de ambiente Olá neste formato:

```
Linux:
AZ_BATCH_APP_PACKAGE_BLENDER_2_7
``` 

Quando você carrega um pacote de aplicativo, você pode especificar um tooyour de toodeploy de versão do padrão de nós de computação. Se você tiver especificado uma versão padrão para um aplicativo, você pode omitir o sufixo da versão de hello quando você referenciar o aplicativo hello. Você pode especificar versão do aplicativo saudação padrão em Olá portal do Azure, na folha de aplicativos hello, conforme mostrado no [carregar e gerenciar aplicativos](#upload-and-manage-applications).

Por exemplo, se você definir "2.7" como versão padrão de saudação para o aplicativo *blender*e suas tarefas de referenciam Olá variável de ambiente a seguir, os nós do Windows executará a versão 2.7:

`AZ_BATCH_APP_PACKAGE_BLENDER`

Olá, trecho de código a seguir mostra uma linha de comando do exemplo tarefa que inicia a versão padrão Olá Olá *blender* aplicativo:

```csharp
string taskId = "blendertask01";
string commandLine =
    @"cmd /c %AZ_BATCH_APP_PACKAGE_BLENDER%\blender.exe -args -here";
CloudTask blenderTask = new CloudTask(taskId, commandLine);
```

> [!TIP]
> Consulte [configurações de ambiente para tarefas](batch-api-basics.md#environment-settings-for-tasks) em Olá [visão geral do recurso de lote](batch-api-basics.md) para obter mais informações sobre configurações de ambiente do nó de computação.
> 
> 

## <a name="update-a-pools-application-packages"></a>Atualizar pacotes de aplicativos de um pool
Se um pool existente já tiver sido configurado com um pacote de aplicativo, você pode especificar um novo pacote para o pool de saudação. Se você especificar uma nova referência de pacote para um pool, Olá aplicar a seguir:

* Olá serviço de lote instala o pacote de especificado mais recentemente de saudação em todos os nós que unem pool hello e em qualquer nó existente que é reinicializado ou recriar a imagem.
* Computação nós que já estão no pool hello quando você atualizar referências de pacote de saudação não instalam automaticamente o novo pacote de aplicativo hello. Esses computação nós devem ser reinicializados ou imagem recriada tooreceive Olá novo pacote.
* Quando um novo pacote é implantado, Olá criar variáveis de ambiente refletem novas referências de pacote de aplicativo hello.

Neste exemplo, pool existente Olá tem versão 2.7 do hello *blender* aplicativo configurado como um de seus [CloudPool][net_cloudpool].[ ApplicationPackageReferences][net_cloudpool_pkgref]. nós do pool de saudação tooupdate com a versão 2.76b, especifique um novo [ApplicationPackageReference] [ net_pkgref] com hello nova versão e alterações de saudação de confirmação.

```csharp
string newVersion = "2.76b";
CloudPool boundPool = await batchClient.PoolOperations.GetPoolAsync("myPool");
boundPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "blender",
        Version = newVersion }
};
await boundPool.CommitAsync();
```

Agora que hello nova versão tiver sido configurado, Olá serviço de lote instala a versão 2.76b tooany *novo* nó que une Olá pool. tooinstall 2.76b em nós Olá *já* no pool de hello, reinicializar ou refazer imagem-los. Observe que nós reinicializada mantenham arquivos Olá de implantações de pacote anterior.

## <a name="list-hello-applications-in-a-batch-account"></a>Lista de aplicativos de saudação em uma conta de lote
Você pode listar aplicativos hello e seus pacotes em uma conta de lote usando Olá [ApplicationOperations][net_appops].[ ListApplicationSummaries] [ net_appops_listappsummaries] método.

```csharp
// List hello applications and their application packages in hello Batch account.
List<ApplicationSummary> applications = await batchClient.ApplicationOperations.ListApplicationSummaries().ToListAsync();
foreach (ApplicationSummary app in applications)
{
    Console.WriteLine("ID: {0} | Display Name: {1}", app.Id, app.DisplayName);

    foreach (string version in app.Versions)
    {
        Console.WriteLine("  {0}", version);
    }
}
```

## <a name="wrap-up"></a>Conclusão
Com pacotes de aplicativos, você pode ajudar seus clientes selecione Olá aplicativos para seus trabalhos e especifique Olá versão exata toouse durante o processamento de trabalhos com o serviço de lote habilitado. Você também pode fornecer capacidade Olá para tooupload seus clientes e controlar seus próprios aplicativos em seu serviço.

## <a name="next-steps"></a>Próximas etapas
* Olá [API REST do lote] [ api_rest] também fornece suporte toowork com pacotes de aplicativos. Por exemplo, consulte Olá [applicationPackageReferences] [ rest_add_pool_with_packages] elemento [adicionar uma conta do pool de tooan] [ rest_add_pool] para obter informações sobre como toospecify tooinstall de pacotes usando Olá API REST. Consulte [aplicativos] [ rest_applications] para obter detalhes sobre como informações do aplicativo tooobtain usando Olá API REST do lote.
* Saiba como tooprogrammatically [gerenciar contas de lote do Azure e cotas com o Batch Management .NET](batch-management-dotnet.md). Olá [Batch Management .NET][api_net_mgmt] biblioteca pode habilitar os recursos de criação e exclusão de conta para o lote de aplicativo ou serviço.

[api_net]: https://docs.microsoft.com/dotnet/api/overview/azure/batch/client?view=azure-dotnet
[api_net_mgmt]: https://docs.microsoft.com/dotnet/api/overview/azure/batch/management?view=azure-dotnet
[api_rest]: https://docs.microsoft.com/en-us/rest/api/batchservice/
[batch_mgmt_nuget]: https://www.nuget.org/packages/Microsoft.Azure.Management.Batch/
[github_samples]: https://github.com/Azure/azure-batch-samples
[storage_pricing]: https://azure.microsoft.com/pricing/details/storage/
[net_appops]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationoperations.aspx
[net_appops_listappsummaries]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationoperations.listapplicationsummaries.aspx
[net_cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_cloudpool_pkgref]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.applicationpackagereferences.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudtask.aspx
[net_cloudtask_pkgref]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudtask.applicationpackagereferences.aspx
[net_nodestate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.state.aspx
[net_pkgref]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationpackagereference.aspx
[portal]: https://portal.azure.com
[rest_applications]: https://msdn.microsoft.com/library/azure/mt643945.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[rest_add_pool_with_packages]: https://msdn.microsoft.com/library/azure/dn820174.aspx#bk_apkgreference

[1]: ./media/batch-application-packages/app_pkg_01.png "Diagrama de alto nível de pacotes de aplicativos"
[2]: ./media/batch-application-packages/app_pkg_02.png "Bloco Aplicativos no portal do Azure"
[3]: ./media/batch-application-packages/app_pkg_03.png "Folha Aplicativos no portal do Azure"
[4]: ./media/batch-application-packages/app_pkg_04.png "Folha Detalhes do aplicativo no portal do Azure"
[5]: ./media/batch-application-packages/app_pkg_05.png "Folha Novo aplicativo no portal do Azure"
[7]: ./media/batch-application-packages/app_pkg_07.png "Menu suspenso Atualizar ou excluir pacotes no portal do Azure"
[8]: ./media/batch-application-packages/app_pkg_08.png "Folha Novo pacote de aplicativos no portal do Azure"
[9]: ./media/batch-application-packages/app_pkg_09.png "Alerta Nenhuma conta de armazenamento vinculada"
[10]: ./media/batch-application-packages/app_pkg_10.png "Folha Escolher conta de armazenamento no portal do Azure"
[11]: ./media/batch-application-packages/app_pkg_11.png "Folha do pacote de atualização no portal do Azure"
[12]: ./media/batch-application-packages/app_pkg_12.png "Caixa de diálogo de confirmação Excluir pacote no portal do Azure"
