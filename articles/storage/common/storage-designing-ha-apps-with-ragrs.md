---
title: "aaaDesigning aplicativos altamente disponíveis usando o armazenamento com redundância geográfica do Azure acesso de leitura (RA-GRS) | Microsoft Docs"
description: "Como toouse Azure RA-GRS armazenamento tooarchitect um aplicativo altamente disponível flexível suficiente toohandle interrupções."
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 8f040b0f-8926-4831-ac07-79f646f31926
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 1/19/2017
ms.author: robinsh
ms.openlocfilehash: e4a9fe7ef33eecd894408b3c1ef59920a248d1bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="designing-highly-available-applications-using-ra-grs"></a>Criando aplicativos altamente disponíveis usando RA-GRS

Um recurso comum das infraestruturas de nuvem é que elas fornecem uma plataforma altamente disponível para hospedar aplicativos. Os desenvolvedores de aplicativos baseados em nuvem devem considerar cuidadosamente como tooleverage usuários de tootheir essa plataforma toodeliver aplicativos altamente disponíveis. Este artigo se concentra especificamente em como os desenvolvedores podem usar toomake de armazenamento de redundância geográfica (RA-GRS) de acesso de leitura de armazenamento do Azure Olá seus aplicativos mais disponíveis.

Há quatro opções de redundância: LRS (armazenamento com redundância local), ZRS (armazenamento com redundância de zona), GRS (armazenamento com redundância geográfica) e RA-GRS (armazenamento com redundância geográfica com acesso de leitura). Vamos toodiscuss GRS e RA-GRS neste artigo. Com o GRS, três cópias de seus dados são mantidas na região primária hello, que você selecionou ao configurar a conta de armazenamento hello. Três cópias adicionais são mantidas de forma assíncrona em uma região secundária especificada pelo Azure. RA-GRS é Olá mesma coisa que GRS, exceto que você tem acesso de leitura toohello segunda cópia. Para obter mais informações sobre as diferentes opções de redundância de armazenamento do Azure hello, consulte [replicação de armazenamento do Azure](https://docs.microsoft.com/en-us/azure/storage/storage-redundancy). artigo de replicação Olá também mostra Olá emparelhamentos de regiões de saudação primários e secundários.

Há trechos de código incluídos neste artigo, e um exemplo completo de tooa link final Olá que você pode baixar e executar.

## <a name="key-features-of-ra-grs"></a>Principais recursos do RA-GRS

Antes de falarmos sobre como toouse armazenamento RA-GRS, vamos falar sobre suas propriedades e comportamento.

* Armazenamento do Azure mantém uma cópia somente leitura de dados de saudação que armazenar em sua região primária em uma região secundária; conforme observado acima, o serviço de armazenamento de saudação determina a localização de Olá da região secundária hello.

* cópia de somente leitura Olá é [finalmente consistente](https://en.wikipedia.org/wiki/Eventual_consistency) com dados Olá na região primária hello.

* Para blobs, tabelas e filas, você pode consultar a região secundária Olá para um *hora da última sincronização* valor que indica quando ocorreu a última replicação Olá da região secundária do hello toohello primário. (Não há suporte para isso no Armazenamento de Arquivos do Azure, os quais não têm redundância RA-GRS no momento.)

* Você pode usar o hello toointeract de biblioteca de cliente de armazenamento com dados de saudação em qualquer região primária ou secundária de saudação. Você também pode redirecionar solicitações de leitura automaticamente região secundária toohello se uma região primária do toohello de solicitação de leitura o tempo limite.

* Se houver um problema grave que afetam a acessibilidade de saudação de dados de saudação na região primária hello, Olá, equipe do Azure pode disparar um failover geográfico, no ponto em que as entradas DNS Olá apontando região primária toohello será região secundária do toohello toopoint alterados.

* Se ocorrer um failover geográfico, Azure selecione um novo local secundário e replicar o local de toothat dados hello e Olá secundário tooit de entradas DNS do ponto. ponto de extremidade secundário Olá estarão disponível até que a conta de armazenamento Olá concluiu a replicação. Para obter mais informações, consulte [que toodo se ocorrer uma interrupção de armazenamento do Azure](https://docs.microsoft.com/en-us/azure/storage/storage-disaster-recovery-guidance).

## <a name="application-design-considerations-when-using-ra-grs"></a>Considerações de design de aplicativo ao usar RA-GRS

Olá principal finalidade deste artigo é tooshow você como um aplicativo que continuará toofunction (embora em uma capacidade limitada) até mesmo em caso de Olá de um desastre de grande proporções dados primários de saudação do toodesign center. Isso é feito com seu transitório do aplicativo toohandle ou problemas de execução longa alternando tooread da região secundária Olá enquanto há um problema e alternar de volta quando a região primária hello está disponível novamente.

### <a name="using-eventually-consistent-data"></a>Usando dados eventualmente consistentes

Esta solução pressupõe que ele é tooreturn okey o que poderia ser o aplicativo de chamada de toohello dados obsoletos. Porque os dados secundários Olá seja finalmente consistentes, é possível que dados saudação foi escritos toohello principal mas Olá atualização toohello secundário não foi concluída replicando quando a região primária Olá tornou-se inacessível.

Por exemplo, o cliente pode enviar uma atualização bem-sucedida e Olá primário foi vá para baixo antes atualização hello é propagado toohello secundário. Nesse caso, se o cliente hello, em seguida, solicita dados de saudação tooread novamente, ele recebe dados obsoletos saudação em vez de dados atualizado de saudação. Você deve decidir se isso for aceitável e nesse caso, como você cliente Olá será uma mensagem. Você verá como toocheck Olá hora da última sincronização Olá secundário dados posteriormente neste artigo toosee se Olá secundário for atualizado.

### <a name="handling-services-separately-or-all-together"></a>Tratamento de serviços separadamente ou em conjunto

Embora provavelmente não é possível para um serviço toobecome indisponível enquanto hello outros serviços ainda totalmente funcionais. Você podem identificador Olá repetições e o modo somente leitura para cada serviço separadamente (blobs, filas, tabelas), ou você pode manipular novas tentativas genericamente para todos os serviços de armazenamento Olá juntos.

Por exemplo, se você usar filas e blobs em seu aplicativo, você pode decidir tooput em erros de nova tentativa de toohandle de código separado para cada um deles. Em seguida, se você obter uma nova tentativa do serviço de blob Olá, mas o serviço de fila Olá ainda está funcionando, apenas parte de saudação do seu aplicativo que trata os blobs será afetado. Se você decidir toohandle serviço de armazenamento de todas as tentativas de forma genérica e um serviço de blob toohello chamada retornará um erro reproduzível, solicitações tooboth Olá blob service e serviço de fila hello serão afetados.

Por fim, isso depende de complexidade de saudação do seu aplicativo. Você pode decidir não falhas de saudação toohandle pelo serviço, mas em vez disso tooredirect solicitações para todos os storage services toohello região secundária de leitura e executar o aplicativo hello no modo somente leitura quando detectar um problema com qualquer serviço de armazenamento na região primária hello.

### <a name="other-considerations"></a>Outras considerações

Esses são Olá outras considerações, discutiremos no restante deste artigo hello.

*   Lidar com repetições de solicitações de leitura usando o padrão de disjuntor Olá

*   Dados finalmente consistente e hello hora da última sincronização

*   Testando

## <a name="running-your-application-in-read-only-mode"></a>Executando o aplicativo no modo somente leitura

toouse armazenamento RA-GRS, você deve ser solicitações de leitura de ambos os capaz de toohandle falhado e falha de solicitações de atualização (com atualização nesse caso, significando inserções, atualizações e exclusões). Se hello primário data center falhar, ler solicitações podem ser redirecionadas toohello data center secundário, mas não de solicitações de atualização porque Olá secundário é somente leitura. Por esse motivo, é necessário algum toorun de maneira seu aplicativo no modo somente leitura.

Por exemplo, você pode definir um sinalizador que será verificado antes de enviar qualquer serviço de armazenamento de toohello de solicitações de atualização. Quando uma das solicitações de atualização de saudação passa pelo, você pode ignorá-la e retornar um cliente de toohello resposta apropriada. Você pode até mesmo desejada toodisable totalmente determinados recursos até Olá problema seja resolvido e notificar os usuários que esses recursos estão temporariamente indisponíveis.

Se você decidir toohandle erros para cada serviço separadamente, você também precisará toohandle Olá capacidade toorun seu aplicativo no modo somente leitura pelo serviço. Você pode ter sinalizadores de somente leitura para cada serviço que pode ser habilitado e desabilitado e o identificador Olá sinalizador apropriado em locais apropriados de saudação em seu código.

Sendo toorun capaz de seu aplicativo no modo somente leitura tem outro benefício de lado – ele fornece a funcionalidade limitada de saudação capacidade tooensure durante uma atualização do aplicativo principal. Você pode disparar toorun seu aplicativo em somente leitura modo e toohello de ponto de data center secundário, garantindo que ninguém está acessando dados de saudação na região primária Olá ao fazer atualizações.

## <a name="handling-updates-when-running-in-read-only-mode"></a>Tratamento de atualizações ao executar no modo somente leitura

Há muitas maneiras toohandle atualização solicitações durante a execução no modo somente leitura. Não abordaremos isso de forma abrangente, mas, em geral, há alguns padrões a serem considerados.

1.  Você pode responder tooyour usuário e peça que eles são não está aceitando atualizações. Por exemplo, um sistema de gerenciamento de contatos pode habilitar os clientes tooaccess informações de contato, mas não fazer atualizações.

2.  Você pode enfileirar as atualizações em outra região. Nesse caso, você deve gravar sua fila de tooa de solicitações de atualização pendente em uma região diferente e, em seguida, ter uma maneira tooprocess essas solicitações depois Olá data center primário fica online novamente. Nesse cenário, você deve informar a cliente Olá atualização Olá solicitada foi enfileirada para processamento posterior.

3.  Você pode escrever suas atualizações tooa conta de armazenamento em outra região. Em seguida, quando Olá data center principal volta a ficar online, você pode ter uma maneira toomerge essas atualizações em dados primários hello, dependendo da estrutura de saudação dos dados de saudação. Por exemplo, se você estiver criando arquivos separados com um carimbo de data/hora no nome hello, você pode copiar essas região primária do toohello backup de arquivos. Isso funciona para algumas cargas de trabalho, como dados de log e iOT.

## <a name="handling-retries"></a>Lidar com repetições

Como saber quais são os erros com nova tentativa? Isso é determinado pela biblioteca de cliente de armazenamento hello. Por exemplo, um erro 404 (não encontrado de recurso) não é reproduzível porque não é provavelmente tooresult sucesso repetindo a ele. Em Olá outro lado, um erro 500 for reproduzível porque ele é um erro de servidor, e pode ser simplesmente um problema temporário. Para obter mais detalhes, confira Olá [abrir o código-fonte para Olá classe ExponentialRetry](https://github.com/Azure/azure-storage-net/blob/87b84b3d5ee884c7adc10e494e2c7060956515d0/Lib/Common/RetryPolicies/ExponentialRetry.cs) na biblioteca de cliente de armazenamento Olá .NET. (Procure Olá método ShouldRetry).

### <a name="read-requests"></a>Solicitações de leitura

Solicitações de leitura podem ser redirecionado toosecondary armazenamento se houver um problema com o armazenamento principal. Como mencionado acima na [usando eventualmente dados consistentes](#using-eventually-consistent-data), ele deve ser aceitável para seu aplicativo toopotentially leia dados obsoletos. Se você estiver usando Olá armazenamento cliente biblioteca tooaccess dados RA-GRS, você pode especificar o comportamento de repetição de saudação de uma solicitação de leitura, definindo um valor para Olá **LocationMode** tooone propriedade seguinte hello:

*   **PrimaryOnly** (Olá padrão)

*   **PrimaryThenSecondary**

*   **SecondaryOnly**

*   **SecondaryThenPrimary**

Quando você define Olá **LocationMode** muito**PrimaryThenSecondary**, se a saudação inicial ler toohello solicitação ponto de extremidade primário falha com um erro reproduzível, cliente Olá automaticamente faz outra leitura solicitação de ponto de extremidade secundário toohello. Se o erro de saudação é um tempo limite do servidor, cliente Olá terá toowait para tooexpire de tempo limite de saudação antes de receber um erro reproduzível do serviço de saudação.

Há basicamente dois cenários tooconsider ao decidir como erro com nova tentativa de tooa toorespond:

*   Este é um problema isolado e ponto de extremidade primário solicitações subsequentes toohello não retornará um erro reproduzível. Um exemplo é quando há um erro de rede temporário.

    Nesse cenário, não há nenhuma penalidade de desempenho significativa em ter **LocationMode** definido muito**PrimaryThenSecondary** como isso acontece apenas raramente.

*   Este é um problema com pelo menos um dos serviços de armazenamento de saudação na região primária hello e todos os serviços de toothat solicitações subsequentes na região primária Olá provavelmente tooreturn reproduzível erros por um período de tempo. Um exemplo disso é se a região primária Olá é totalmente inacessível.

    Nesse cenário, há uma penalidade de desempenho porque todas as suas solicitações de leitura tente primeiro o ponto de extremidade primário hello, aguarde Olá tooexpire de tempo limite e alternar ponto de extremidade secundário toohello.

Para esses cenários, você deve identificar que há um problema contínuo com o ponto de extremidade primário hello e enviar todas as solicitações de leitura diretamente o ponto de extremidade secundário, definindo toohello Olá **LocationMode** propriedade muito **SecondaryOnly**. Neste momento, você deve também alterar Olá toorun de aplicativo no modo somente leitura. Essa abordagem é conhecida como Olá [padrão de disjuntor](https://msdn.microsoft.com/library/dn589784.aspx).

### <a name="update-requests"></a>Solicitações de atualização

padrão de disjuntor Olá também pode ser aplicadas tooupdate solicitações. No entanto, solicitações de atualização não podem ser redirecionada toosecondary armazenamento, que é somente leitura. Para essas solicitações, você deve deixar Olá **LocationMode** propriedade definida muito**PrimaryOnly** (Olá padrão). toohandle esses erros, você pode aplicar um solicitações toothese métrica – como 10 falhas em uma linha – e quando o limite é atingido, o aplicativo hello em modo somente leitura. Você pode usar Olá mesmo métodos para retornar tooupdate o modo como as descritas abaixo na próxima seção, sobre o padrão de disjuntor Olá Olá.

## <a name="circuit-breaker-pattern"></a>Padrão de Disjuntor

Usando o padrão de disjuntor Olá em seu aplicativo pode impedir que ele repetir uma operação que é provavelmente toofail repetidamente. Ele permite Olá aplicativo toocontinue toorun em vez de colocar o tempo durante a operação de saudação é repetida exponencialmente. Ela também detecta quando falhas Olá foi corrigido, em que o aplicativo hello de tempo pode Repita a operação hello.

### <a name="how-tooimplement-hello-circuit-breaker-pattern"></a>Como tooimplement Olá padrão de Disjuntor

tooidentify que há um problema contínuo com um ponto de extremidade primário, você pode monitorar a frequência cliente Olá encontra erros de nova tentativa. Como cada caso é diferente, é preciso toodecide no limite de saudação desejado toouse para Olá decisão tooswitch toohello ponto de extremidade secundário e execute o aplicativo hello no modo somente leitura. Por exemplo, você pode decidir switch de saudação tooperform se há 10 falhas em uma linha com nenhuma êxitos. Outro exemplo é tooswitch se falhar de 90% das solicitações de saudação em um período de 2 minutos.

Para o primeiro cenário de hello, simplesmente, você pode manter uma contagem de falhas de saudação e se houver êxito antes de alcançar Olá Olá máximo, defina contagem back toozero. Para o segundo cenário de hello, tooimplement unidirecional é toouse Olá MemoryCache objeto (.NET). Para cada solicitação, adicionar um cache de toohello CacheItem, definir Olá valor toosuccess (1) ou falha (0) e definir minutos de too2 de tempo de expiração de saudação do agora (ou o que é a restrição de tempo). Quando é atingido o tempo de expiração de uma entrada, entrada hello será removida automaticamente. Isso lhe dará uma janela de dois minutos sem interrupção. Cada vez que um serviço de armazenamento de toohello de solicitação, primeiro você usar uma consulta Linq em Olá MemoryCache objeto toocalculate Olá porcentagem de êxitos somando os valores hello e dividindo por contagem de saudação. Quando a porcentagem de êxitos Olá cai abaixo de limite (por exemplo, 10%), definir Olá **LocationMode** propriedade para solicitações de leitura muito**SecondaryOnly** e aplicativo hello em modo somente leitura antes de alternar continuar.

limite de saudação de erros usado toodetermine ao comutador de saudação toomake pode variar de serviço tooservice em seu aplicativo, portanto, você deve considerar tornando-os parâmetros configuráveis. Isso também é onde você decidir toohandle erros de nova tentativa de cada serviço separadamente ou como uma, conforme discutido anteriormente.

Outra consideração é como toohandle várias instâncias de um aplicativo e quais toodo quando detectar erros de nova tentativa em cada instância. Por exemplo, você pode ter 20 VMs em execução com hello carregado do mesmo aplicativo. Você lida com cada instância separadamente? Se uma instância inicia com problemas, você deseja toolimit Olá resposta toojust que uma instância ou desejar tootry toohave todas as instâncias de respondem em Olá mesmo quando uma instância tem um problema? Manipular instâncias Olá separadamente é muito mais simples do que a tentativa de resposta de saudação toocoordinate entre eles, mas como fazer isso depende da arquitetura do aplicativo.

### <a name="options-for-monitoring-hello-error-frequency"></a>Opções de frequência de erro de saudação de monitoramento

Você tem três opções principais para monitoramento de frequência de saudação de novas tentativas na região primária do hello em ordem toodetermine quando tooswitch por região secundária toohello e alteração Olá toorun de aplicativo no modo somente leitura.

*   Adicionar um manipulador para Olá [ **repetindo** ](http://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.operationcontext.retrying.aspx) evento em Olá [ **OperationContext** ](http://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.operationcontext.aspx) passar solicitações de armazenamento tooyour – isso é hello do objeto método exibido neste artigo e usado em Olá que acompanha o exemplo. Esses eventos acionam sempre que o cliente Olá repete uma solicitação, permitindo que você tootrack frequência cliente Olá encontra erros de nova tentativa em um ponto de extremidade primário.

    ```csharp 
    operationContext.Retrying += (sender, arguments) =>
    {
        // Retrying in hello primary region
        if (arguments.Request.Host == primaryhostname)
            ...
    };
    ```

*   Em Olá [ **avaliar** ](http://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.retrypolicies.iextendedretrypolicy.evaluate.aspx) método em uma política de repetição personalizada, você pode executar código personalizado sempre que uma repetição ocorre. Em adição toorecording quando uma repetição ocorre, isso também permite que você Olá oportunidade toomodify seu comportamento de repetição.

    ```csharp 
    public RetryInfo Evaluate(RetryContext retryContext,
    OperationContext operationContext)
    {
        var statusCode = retryContext.LastRequestResult.HttpStatusCode;
        if (retryContext.CurrentRetryCount >= this.maximumAttempts
        || ((statusCode &gt;= 300 && statusCode &lt; 500 && statusCode != 408)
        || statusCode == 501 // Not Implemented
        || statusCode == 505 // Version Not Supported
            ))
        {
        // Do not retry
            return null;
        }

        // Monitor retries in hello primary location
        ...

        // Determine RetryInterval and TargetLocation
        RetryInfo info =
            CreateRetryInfo(retryContext.CurrentRetryCount);

        return info;
    }
    ```

*   Olá, terceira abordagem é tooimplement um componente de monitoramento personalizado em seu aplicativo que executa ping continuamente em seu ponto de extremidade de armazenamento principal com fictício ler solicitações (como ler um blob pequeno) toodetermine sua integridade. Isso deve exigir alguns recursos, mas não uma quantidade significativa. Quando um problema é descoberto que atinge o limite, em seguida, você executará comutador hello muito**SecondaryOnly** e modo somente leitura.

Em algum momento, você desejará tooswitch toousing back Olá ponto de extremidade primário e permitir atualizações. Se usando um dos primeiros dois métodos de saudação listados acima, você pode simplesmente alternar ponto de extremidade primário toohello back e habilitar o modo de atualização após um período arbitrariamente selecionado ou o número de operações foi executado. Você pode, em seguida, permitir que ele percorrer a lógica de repetição Olá novamente. Se Olá problema foi corrigido, ele continuará ponto de extremidade primário toouse hello e permitir atualizações. Se ainda houver um problema, ele irá mais uma vez alternar ponto de extremidade secundário toohello voltar e o modo somente leitura após a falha de critérios de saudação que você definiu.

Para o cenário de terceiro hello, quando o ponto de extremidade do ping Olá armazenamento primário torna-se com êxito novamente, você pode disparar retornar Olá muito**PrimaryOnly** e continuar a permitir atualizações.

## <a name="handling-eventually-consistent-data"></a>Manipulação de dados eventualmente consistentes

RA-GRS funciona por transações de replicação da região secundária do hello toohello primário. Esse processo de replicação garante que dados de saudação na região secundária Olá são *finalmente consistente*. Isso significa que todas as transações de saudação na região primária Olá eventualmente aparecerá na região secundária hello, mas que pode haver um atraso antes que elas sejam exibidas, e que não há nenhuma garantia de transações Olá chegam na região secundária do hello em Olá mesma ordem que na qual eles foram aplicados originalmente na região primária hello. Se as transações chegam na região secundária do hello fora de ordem, você *pode* considerar seus dados no hello região secundária toobe em um estado inconsistente até que o serviço de saudação alcança.

Olá, tabela a seguir mostra um exemplo do que pode acontecer quando você atualizar os detalhes de saudação do toomake funcionário a um membro da saudação *administradores* função. Para bem Olá deste exemplo, é necessário atualizar Olá **funcionário** entidade e atualizar um **função administrador** entidade com uma contagem do número total de saudação de administradores. Observe como Olá atualizações são aplicadas fora de ordem na região secundária hello.

| **Hora** | **Transação**                                            | **Replicação**                       | **Hora da Última Sincronização** | **Resultado** |
|----------|------------------------------------------------------------|---------------------------------------|--------------------|------------| 
| T0       | Transação A: <br> Inserir funcionário <br> entidade no principal |                                   |                    | A transação A inserido tooprimary,<br> ainda não replicada. |
| T1       |                                                            | Transação A <br> replicada para<br> secundário | T1 | A transação A replicadas toosecondary. <br>Hora da Última Sincronização atualizada.    |
| T2       | Transação B:<br>Atualização<br> entidade de funcionário<br> no principal  |                                | T1                 | Transação B gravado tooprimary,<br> ainda não replicada.  |
| T3       | Transação C:<br> Atualização <br>administrator<br>entidade de função em<br>primary |                    | T1                 | Transação C gravado tooprimary,<br> ainda não replicada.  |
| *T4*     |                                                       | Transação C <br>replicada para<br> secundário | T1         | Transação C replicada toosecondary.<br>LastSyncTime não atualizado porque <br>a transação B ainda não foi replicada.|
| *T5*     | Ler entidades <br>de secundário                           |                                  | T1                 | Obter valor obsoleto de saudação de funcionário <br> porque a transação B não foi <br> replicada ainda. Obter o novo valor Olá para<br> a entidade de função de administrador porque C foi<br> replicada. A Hora da Última Sincronização ainda não<br> foi atualizada porque a transação B<br> não foi replicada. Você pode ver que a<br>entidade da função de administrador está inconsistente <br>como Olá entidade data/hora é após <br>Olá hora da última sincronização. |
| *T6*     |                                                      | Transação B<br> replicada para<br> secundário | T6                 | *T6* – todas as transações até C <br>foram replicadas; a Hora da Última Sincronização<br> foi atualizada. |

Neste exemplo, suponha que Olá cliente comutadores tooreading da região secundária do hello na T5. Ela pode ler com êxito Olá **função de administrador** entidade neste momento, mas a entidade Olá contém um valor para contagem de saudação de administradores que não é consistente com o número de saudação do **funcionário** entidades que são marcados como administradores na região secundária Olá neste momento. O cliente simplesmente pode exibir esse valor, com o risco de saudação que se trata de informações inconsistentes. Como alternativa, Olá cliente pode tentar toodetermine que Olá **função administrador** está em um estado potencialmente inconsistente porque atualizações Olá aconteceram fora de ordem e informam o usuário Olá desse fato.

toorecognize que contém dados potencialmente inconsistentes, o cliente Olá pode usar o valor Olá Olá *hora da última sincronização* que você pode obter a qualquer momento por meio de um serviço de armazenamento de consultas. Isso informa Olá hora do dados de saudação na região secundária Olá últimos consistente e ao serviço de saudação aplicado todas Olá transações anteriores toothat ponto no tempo. No exemplo hello mostrado acima, depois que o serviço Olá insere hello **funcionário** entidade na região secundária hello, Olá hora da última sincronização está definido muito*T1*. Ele permanece em *T1* até que as atualizações de serviço de Olá Olá **funcionário** entidade na região secundária do hello quando ele está definido muito*T6*. Se o cliente de saudação recupera Olá hora da última sincronização quando lê entidade Olá *T5*, ele pode compará-la com carimbo de hora Olá na entidade hello. Se timestamp Olá na entidade Olá é posterior à saudação sincronização pela última vez, em seguida, hello entidade está em um estado inconsistente potencialmente e você pode colocar tudo o que é a ação apropriada Olá para seu aplicativo. Usar este campo requer que você saiba quando Olá última atualização toohello primário foi concluída.

## <a name="testing"></a>Testando

É importante tootest que seu aplicativo se comporta conforme o esperado quando encontra erros de nova tentativa. Por exemplo, você precisa tootest que Olá aplicativo comutadores toohello secundário e no modo somente leitura quando ela detecta um problema e volta quando região primária Olá fica disponível novamente. toodo isso, você precisa de uma maneira toosimulate reproduzível os erros e controlar a frequência que ocorrem.

Você pode usar [Fiddler](http://www.telerik.com/fiddler) toointercept e modificar as respostas HTTP em um script. Esse script pode identificar as respostas que vêm do ponto de extremidade primário e alterar Olá tooone de código de status HTTP que Olá que reconhece biblioteca de cliente de armazenamento como um erro reproduzível. Este trecho de código mostra um exemplo simples de um script do Fiddler que intercepta as respostas tooread solicitações contra Olá **employeedata** tooreturn tabela 502 status:

```java
static function OnBeforeResponse(oSession: Session) {
    ...
    if ((oSession.hostname == "\[yourstorageaccount\].table.core.windows.net")
      && (oSession.PathAndQuery.StartsWith("/employeedata?$filter"))) {
        oSession.responseCode = 502;
    }
}
```

Você pode estender esse exemplo toointercept uma variedade maior de solicitações e alterar apenas Olá **responseCode** em algumas delas toobetter simular um cenário do mundo real. Para obter mais informações sobre como personalizar os scripts do Fiddler, consulte [modificando uma solicitação ou resposta](http://docs.telerik.com/fiddler/KnowledgeBase/FiddlerScript/ModifyRequestOrResponse) em Olá documentação Fiddler.

Se você tiver feito limites Olá para alternar entre o aplicativo somente tooread modo pode ser configurado, será mais fácil comportamento de saudação tootest com volumes de transações de não produção.

## <a name="next-steps"></a>Próximas etapas

* Para obter mais informações sobre acesso de leitura a redundância geográfica, incluindo outro exemplo de como Olá LastSyncTime for definido, consulte [opções de redundância de armazenamento do Windows Azure e armazenamento geograficamente redundante de acesso de leitura](https://blogs.msdn.microsoft.com/windowsazurestorage/2013/12/11/windows-azure-storage-redundancy-options-and-read-access-geo-redundant-storage/).

* Para obter um exemplo completo mostrando como toomake Olá alternar e voltar entre pontos de extremidade primário e secundário Olá, consulte [exemplos do Azure – usando Olá padrão de disjuntor com armazenamento de RA-GRS](https://github.com/Azure-Samples/storage-dotnet-circuit-breaker-pattern-ha-apps-using-ra-grs).
