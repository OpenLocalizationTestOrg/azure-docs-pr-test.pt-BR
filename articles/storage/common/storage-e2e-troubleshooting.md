---
title: "aaaTroubleshooting de armazenamento do Azure com o diagnóstico & Message Analyzer | Microsoft Docs"
description: "Um tutorial que demonstra a solução de problemas ponta a ponta com Análise de Armazenamento do Azure, AzCopy e Analisador de Mensagem da Microsoft"
services: storage
documentationcenter: dotnet
author: robinsh
manager: timlt
ms.assetid: 643372a3-1c07-4e88-b4ef-042512a43086
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/15/2017
ms.author: robinsh
ms.openlocfilehash: 2d7a2a14b2e8da01b566ac3dec19996f0ef88cc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="end-to-end-troubleshooting-using-azure-storage-metrics-and-logging-azcopy-and-message-analyzer"></a>Solução de problemas ponta a ponta usando métricas de Armazenamento do Azure e registro em log, AzCopy e Analisador de Mensagem
[!INCLUDE [storage-selector-portal-e2e-troubleshooting](../../../includes/storage-selector-portal-e2e-troubleshooting.md)]

Diagnóstico e solução de problemas são habilidades chaves para a criação e o suporte a aplicativos de clientes com o Armazenamento do Microsoft Azure. Devido a natureza toohello distribuída de um aplicativo do Azure, diagnosticar e solucionar erros e problemas de desempenho podem ser mais complexos do que em ambientes tradicionais.

Neste tutorial, demonstraremos como tooidentify determinados erros que podem afetar o desempenho e solucionar os erros de ponta a ponta usando as ferramentas fornecidas pela Microsoft e armazenamento do Azure, no aplicativo cliente do pedido toooptimize hello.

Este tutorial fornece uma exploração prática de um cenário de solução de problemas de ponta a ponta. Para aplicativos de armazenamento do Azure uma tootroubleshooting guia conceituais detalhadas, consulte [monitorar, diagnosticar e solucionar problemas de armazenamento do Microsoft Azure](storage-monitoring-diagnosing-troubleshooting.md).

## <a name="tools-for-troubleshooting-azure-storage-applications"></a>Ferramentas para solucionar problemas de aplicativos de armazenamento do Azure
aplicativos de cliente tootroubleshoot usando o armazenamento do Microsoft Azure, você pode usar uma combinação de ferramentas toodetermine quando um problema ocorreu e que causa Olá problema Olá pode ser. Essas ferramentas incluem:

* **Análise de Armazenamento do Azure**. [A Análise de Armazenamento do Azure](/rest/api/storageservices/Storage-Analytics) fornece métricas e registro em log para o Armazenamento do Azure.
  
  * **A métrica de armazenamento** controla as métricas de transação e as métricas de capacidade para sua conta de armazenamento. Uso de métricas, você pode determinar como seu aplicativo está executando o acordo tooa várias medidas diferentes. Consulte [esquema de tabela de métricas de análise de armazenamento](/rest/api/storageservices/Storage-Analytics-Metrics-Table-Schema) para obter mais informações sobre tipos de saudação de métricas controladas pela análise de armazenamento.
  * **O log de armazenamento** registra cada log de solicitações de toohello lado de servidor de tooa de serviços de armazenamento do Azure. Olá log rastreia dados detalhados para cada solicitação, incluindo a operação de saudação executada, status de saudação de operação hello e informações de latência. Consulte [formato de Log de análise de armazenamento](/rest/api/storageservices/Storage-Analytics-Log-Format) para obter mais informações sobre os dados de solicitação e resposta Olá escrito toohello logs pela análise de armazenamento.

> [!NOTE]
> Contas de armazenamento com um tipo de replicação de armazenamento com redundância de zona (ZRS) não têm métricas hello ou recurso de log habilitado no momento. 
> 
> 

* **Portal do Azure**. Você pode configurar o log e métricas para sua conta de armazenamento Olá [portal do Azure](https://portal.azure.com). Você também pode exibir gráficos que mostram o desempenho do seu aplicativo ao longo do tempo e configurar alertas toonotify que se seu aplicativo executa diferente que o esperado para uma métrica especificada.
  
    Consulte [monitorar uma conta de armazenamento no portal do Azure de saudação](storage-monitor-storage-account.md) para obter informações sobre como configurar o monitoramento em Olá portal do Azure.
* **AzCopy**. Logs do servidor para o armazenamento do Azure são armazenados como blobs, assim você pode usar AzCopy toocopy Olá log blobs tooa diretório local para análise usando o Microsoft Message Analyzer. Consulte [transferir dados com o utilitário de linha de comando AzCopy de hello](storage-use-azcopy.md) para obter mais informações sobre AzCopy.
* **Analisador de Mensagem da Microsoft**. Analisador de mensagem é uma ferramenta que consome os arquivos de log e exibe dados de log em um formato visual que torna mais fácil toofilter, pesquisa e grupo de dados de log em conjuntos úteis que você pode usar tooanalyze erros e problemas de desempenho. Consulte o [Guia Operacional do Analisador de Mensagem da Microsoft](http://technet.microsoft.com/library/jj649776.aspx) para obter mais informações sobre o Analisador de Mensagem.

## <a name="about-hello-sample-scenario"></a>Sobre o cenário de exemplo hello
Para este tutorial, vamos examinar um cenário onde as métricas de armazenamento do Azure indicam uma taxa de sucesso de porcentagem baixa de um aplicativo que chama o armazenamento do Azure. Olá métrica de taxa baixa de êxito de porcentagem (mostrado como **PercentSuccess** em Olá [portal do Azure](https://portal.azure.com) e nas tabelas de métricas de saudação) controla as operações que tenha êxito, mas que retornam um código de status HTTP for maior que 299. Nos arquivos de log de armazenamento no servidor de saudação, essas operações são registradas com um status de transação **ClientOtherErrors**. Para obter mais detalhes sobre a métrica de sucesso de porcentagem baixa hello, consulte [métricas mostram PercentSuccess baixa ou entradas de log de análise possuem operações com status de transação de ClientOtherErrors](storage-monitoring-diagnosing-troubleshooting.md#metrics-show-low-percent-success).

Operações de armazenamento do Azure podem retornar códigos de status HTTP maior 299 como parte de sua funcionalidade normal. Mas esses erros em alguns casos indicam que você pode ser capaz de toooptimize seu aplicativo cliente para melhor desempenho.

Nesse cenário, consideraremos um toobe de taxa de sucesso de porcentagem baixa algo abaixo de 100%. Você pode escolher um métrico nível diferente, no entanto, de acordo com as necessidades de tooyour. É recomendável que, durante o teste do seu aplicativo, você estabeleça uma tolerância de linha de base para suas principais métricas de desempenho. Por exemplo, você pode determinar, com base nos testes, que seu aplicativo deve ter uma taxa de porcentagem de êxitos consistente de 90% ou 85%. Se seus dados de métricas mostram que aplicativo hello é desviam-se de que esse número, você pode investigar o que pode estar causando o aumento de saudação.

Em nosso cenário de exemplo, quando estabelecemos métrica de taxa de sucesso de porcentagem hello está abaixo de 100%, podemos examinar Olá logs toofind Olá erros que correlacionam toohello métricas e usá-los toofigure o que está causando Olá inferior porcentagem sucesso. Vamos examinar especificamente erros no intervalo de 400 hello. Em seguida, examinaremos com mais detalhes os erros 404 (não encontrado).

### <a name="some-causes-of-400-range-errors"></a>Algumas causas de erros no intervalo 400
exemplos de saudação abaixo mostra uma amostragem de alguns erros de intervalo de 400 para solicitações em relação ao armazenamento de Blob do Azure e suas causas possíveis. Qualquer um desses erros, bem como erros no intervalo de 300 hello e intervalo de 500 hello, podem contribuir taxa de sucesso de porcentagem baixa de tooa.

Observe que listas de saudação abaixo estão distantes de conclusão. Consulte [Status e códigos de erro](http://msdn.microsoft.com/library/azure/dd179382.aspx) no MSDN para obter detalhes sobre erros gerais de armazenamento do Azure e tooeach de erros específicas dos serviços de armazenamento de saudação.

**Exemplos do Código de Status 404 (Não Encontrado)**

Ocorre quando uma operação de leitura em um contêiner ou blob falha porque Olá blob ou contêiner não foi encontrado.

* Ocorre se um contêiner ou blob tiver sido excluído por outro cliente antes desta solicitação.
* Ocorre se você estiver usando uma chamada de API que cria Olá contêiner ou blob depois de verificar se ele existe. Olá CreateIfNotExists APIs tornar um cabeçalho chamar toocheck primeiro quanto à existência de saudação do hello contêiner ou blob; Se não existir, será retornado um erro 404 e, em seguida, uma segunda chamada PUT é feita toowrite Olá contêiner ou blob.

**Exemplos do Código de Status 409 (Conflito)**

* Ocorre se você usar um toocreate de API de criar um novo contêiner ou blob, sem verificar a existência do primeiro e um contêiner ou blob com esse nome já existe.
* Ocorre se um contêiner que está sendo excluído e você tentar toocreate um novo contêiner com mesmo nome antes da conclusão operação de exclusão de saudação do hello.
* Ocorre se você especificar uma concessão em um contêiner ou blob e já houver uma concessão presente.

**Exemplos do Código de Status 412 (Falha na Pré-condição)**

* Ocorre quando a condição de saudação especificada por um cabeçalho condicional não foi atendida.
* Ocorre quando a ID de concessão Olá especificada não coincide com ID de concessão Olá Olá contêiner ou blob.

## <a name="generate-log-files-for-analysis"></a>Gerar arquivos de log para análise
Neste tutorial, usaremos Message Analyzer toowork com três tipos diferentes de arquivos de log, embora você poderia escolher toowork com qualquer uma destas:

* Olá **log de servidor**, que é criado quando você habilita o log de armazenamento do Azure. log do servidor de saudação contém dados sobre cada operação chamado em um dos serviços de armazenamento do Azure Olá - blob, fila, tabela e arquivo. registro do servidor de saudação indica qual operação foi chamada e o código de status foi retornados, bem como outros detalhes sobre Olá solicitação e resposta.
* Olá **log do cliente .NET**, que é criado quando você habilita o log de cliente de dentro de seu aplicativo .NET. log de saudação do cliente inclui informações detalhadas sobre como cliente Olá prepara solicitação hello e recebe e processa a resposta de saudação.
* Olá **log de rastreamento de rede HTTP**, que coleta dados sobre dados de solicitação e resposta HTTP/HTTPS, incluindo para operações no armazenamento do Azure. Neste tutorial, vamos irá gerar o rastreamento de rede Olá por meio do analisador de mensagem.

### <a name="configure-server-side-logging-and-metrics"></a>Configurar o log de servidor e métricas
Primeiro, vamos precisar tooconfigure log de armazenamento do Azure e métricas, para que tenhamos dados de saudação tooanalyze de aplicativo de cliente. Você pode configurar o registro em log e métricas de várias maneiras – via Olá [portal do Azure](https://portal.azure.com), usando o PowerShell, ou programaticamente. Consulte [Habilitando as métricas de armazenamento e Exibindo os dados da métrica](http://msdn.microsoft.com/library/azure/dn782843.aspx) e [Habilitando o registro em log de armazenamento e Acessando os dados de log](http://msdn.microsoft.com/library/azure/dn782840.aspx) no MSDN para obter detalhes sobre como configurar o registro em log e as métricas.

**Por meio de saudação portal do Azure**

Olá tooconfigure log e métricas para sua conta de armazenamento usando [portal do Azure](https://portal.azure.com), siga as instruções de saudação em [monitorar uma conta de armazenamento no portal do Azure de saudação](storage-monitor-storage-account.md).

> [!NOTE]
> Não é possível tooset métricas de minuto usando Olá portal do Azure. No entanto, é recomendável que você defini-las para fins deste tutorial hello e para investigar problemas de desempenho com o seu aplicativo. Você pode definir as métricas de minuto usando o PowerShell, conforme mostrado abaixo, ou programaticamente usando a biblioteca de cliente de armazenamento hello.
> 
> Observe que Olá portal do Azure não pode exibir métricas por minuto, somente as métricas de hora.
> 
> 

**Por meio do PowerShell**

tooget iniciado com o PowerShell do Azure, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).

1. Saudação de uso [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0) tooadd cmdlet toohello janela do PowerShell de conta de usuário do Azure:
   
    ```powershell
    Add-AzureAccount
    ```

2. Em Olá **entrar tooMicrosoft Azure** janela, digite Olá o endereço de email e senha associados à sua conta. Azure autentica e salva informações de credencial hello e, em seguida, fecha a janela de saudação.
3. Definir saudação padrão armazenamento conta toohello conta de armazenamento que você está usando para o tutorial Olá executando esses comandos na janela do PowerShell hello:
   
    ```powershell
    $SubscriptionName = 'Your subscription name'
    $StorageAccountName = 'yourstorageaccount'
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

4. Habilite log para Olá serviço Blob de armazenamento:
   
    ```powershell
    Set-AzureStorageServiceLoggingProperty -ServiceType Blob -LoggingOperations Read,Write,Delete -PassThru -RetentionDays 7 -Version 1.0
    ```

5. Habilitar as métricas de armazenamento para Olá serviço Blob, tornando-se de que tooset **- MetricsType** muito`Minute`:
   
    ```powershell
    Set-AzureStorageServiceMetricsProperty -ServiceType Blob -MetricsType Minute -MetricsLevel ServiceAndApi -PassThru -RetentionDays 7 -Version 1.0
    ```

### <a name="configure-net-client-side-logging"></a>Configurar o log de cliente .NET
tooconfigure do cliente do registro em log para um aplicativo .NET, habilitar o diagnóstico do .NET no arquivo de configuração do aplicativo hello (Web. config ou App. config). Consulte [cliente fazendo com hello biblioteca de cliente de armazenamento do .NET](http://msdn.microsoft.com/library/azure/dn782839.aspx) e [em log com o SDK de armazenamento do Microsoft Azure para Java de saudação do cliente](http://msdn.microsoft.com/library/azure/dn782844.aspx) no MSDN para obter detalhes.

log de cliente de saudação inclui informações detalhadas sobre como cliente Olá prepara solicitação hello e recebe e processa a resposta de saudação.

Olá biblioteca de cliente de armazenamento armazena dados de log do lado do cliente no local de saudação especificado no arquivo de configuração do aplicativo hello (Web. config ou App. config).

### <a name="collect-a-network-trace"></a>Coletar um rastreamento de rede
Você pode usar o analisador de mensagem toocollect um rastreamento de rede HTTP/HTTPS enquanto seu aplicativo cliente está em execução. Usos do analisador de mensagem [Fiddler](http://www.telerik.com/fiddler) em Olá back-end. Antes de você coletar o rastreamento de rede hello, recomendamos que você configure o tráfego HTTPS do Fiddler toorecord sem criptografia:

1. Instale o [Fiddler](http://www.telerik.com/download/fiddler).
2. Inicie o Fiddler.
3. Selecione **Ferramentas| Opções do Fiddler**.
4. Na caixa de diálogo de opções de saudação, certifique-se de que **capturar HTTPS conecta** e **descriptografar o tráfego HTTPS** estiverem selecionadas, conforme mostrado abaixo.

![Configurar Opções do Fiddler](./media/storage-e2e-troubleshooting/fiddler-options-1.png)

Tutorial Olá, coletar e salvar um rastreamento de rede pela primeira vez no analisador de mensagem, em seguida, criar um rastreamento do analysis sessão tooanalyze hello e Olá logs. toocollect um rastreamento de rede no analisador de mensagem:

1. No Analisador de Mensagem, selecione **Arquivo | Rastreamento Rápido | HTTPS Sem Criptografia**.
2. rastreamento de saudação começará imediatamente. Selecione **parar** toostop Olá rastreamento de modo que é possível configurar somente o tráfego de armazenamento tootrace.
3. Selecione **editar** tooedit sessão de rastreamento de saudação.
4. Selecione Olá **configurar** link toohello direito da saudação **Microsoft-Pef-WebProxy** provedor ETW.
5. Em Olá **configurações avançadas** caixa de diálogo, clique em Olá **provedor** guia.
6. Em Olá **filtro de nome de host** , especifique os pontos de extremidade de armazenamento, separados por espaços. Por exemplo, você pode especificar os pontos de extremidade: alterar `storagesample` toohello nome de sua conta de armazenamento:

    ```   
    storagesample.blob.core.windows.net storagesample.queue.core.windows.net storagesample.table.core.windows.net
    ```

7. Sair da caixa de diálogo hello e, em seguida, clique em **reiniciar** toobegin coleta de rastreamento Olá com filtro de nome de host de saudação em vigor, para que somente o tráfego de rede de armazenamento do Azure está incluído no rastreamento de saudação.

> [!NOTE]
> Após coletar o rastreamento de rede, é altamente recomendável que você reverter as configurações de saudação que você pode ter sido alterado no tráfego do Fiddler toodecrypt HTTPS. Na caixa de diálogo de opções do Fiddler hello, desmarque Olá **capturar HTTPS conecta** e **descriptografar o tráfego HTTPS** caixas de seleção.
> 
> 

Consulte [usando recursos de rastreamento de rede Olá](http://technet.microsoft.com/library/jj674819.aspx) no Technet para obter mais detalhes.

## <a name="review-metrics-data-in-hello-azure-portal"></a>Analisar dados de métricas em Olá portal do Azure
Depois que seu aplicativo estiver sendo executada por um período de tempo, você pode examinar os gráficos de métricas Olá que aparecem no hello [portal do Azure](https://portal.azure.com) tooobserve como seu serviço esteve executando.

Navega pela primeira vez, a conta de armazenamento tooyour Olá portal do Azure. Por padrão, o monitoramento de um gráfico com hello **percentagem de sucesso** métrica é exibida na folha de conta hello. Se você modificou anteriormente diferentes métricas do hello gráfico toodisplay, adicione Olá **percentagem de sucesso** métrica.

Você verá agora **percentagem de sucesso** no gráfico de monitoramento de hello, juntamente com quaisquer outras métricas você tiver adicionado. Cenário de saudação que vamos investigar lado analisando logs Olá no analisador de mensagem, taxa de sucesso de porcentagem de saudação é um pouco abaixo de 100%.

Para obter mais detalhes sobre como adicionar e personalizar gráficos de métricas, consulte [Personalizar gráficos de métricas](storage-monitor-storage-account.md#customize-metrics-charts).

> [!NOTE]
> Ele pode demorar algum tempo para que sua tooappear de dados de métricas em Olá portal do Azure depois de habilitar as métricas de armazenamento. Isso ocorre porque as métricas de hora para Olá hora anterior não são exibidas no hello portal do Azure até Olá hora atual expirou. Além disso, métricas de minutos não são atualmente exibidas no hello portal do Azure. Portanto, dependendo de quando você habilita as métricas, pode levar a dados de métricas de toosee tootwo horas.
> 
> 

## <a name="use-azcopy-toocopy-server-logs-tooa-local-directory"></a>Use AzCopy toocopy server logs tooa diretório local
Armazenamento do Azure grava tooblobs de dados de log do servidor, enquanto as métricas são gravadas tootables. Blobs de log estão disponíveis no hello conhecido `$logs` contêiner para sua conta de armazenamento. Blobs de log são nomeados hierarquicamente por ano, mês, dia e hora, para que você possa localizar facilmente o intervalo de saudação de tempo que você deseja tooinvestigate. Por exemplo, em Olá `storagesample` conta, contêiner Olá para blobs de log Olá para 01/02/2015, de 8-9: 00, é `https://storagesample.blob.core.windows.net/$logs/blob/2015/01/08/0800`. os blobs individuais Olá neste contêiner são nomeados em sequência, começando com `000000.log`.

Você pode usar toodownload de ferramenta de linha de comando AzCopy Olá esses local do log do lado do servidor de arquivos tooa de sua escolha na sua máquina local. Por exemplo, você pode usar o hello seguindo os arquivos de log do comando toodownload Olá para operações de blob que levaram colocar em 2 de janeiro de 2015 toohello pasta `C:\Temp\Logs\Server`; substituir `<storageaccountname>` com o nome de saudação da sua conta de armazenamento e `<storageaccountkey>` com seu chave de acesso da conta:

```azcopy
AzCopy.exe /Source:http://<storageaccountname>.blob.core.windows.net/$logs /Dest:C:\Temp\Logs\Server /Pattern:"blob/2015/01/02" /SourceKey:<storageaccountkey> /S /V
```
AzCopy está disponível para download em Olá [Downloads do Azure](https://azure.microsoft.com/downloads/) página. Para obter detalhes sobre como usar AzCopy, consulte [transferir dados com o utilitário de linha de comando AzCopy de hello](storage-use-azcopy.md).

Para obter informações adicionais sobre como baixar os logs do servidor, confira [Download Storage Logging log data](http://msdn.microsoft.com/library/azure/dn782840.aspx#DownloadingStorageLogginglogdata)(Baixar dados de log do Log de Armazenamento).

## <a name="use-microsoft-message-analyzer-tooanalyze-log-data"></a>Usar dados de log do Microsoft Message Analyzer tooanalyze
O Analisador de Mensagem da Microsoft é uma ferramenta para capturar, exibir e analisar o tráfego, eventos e outras mensagens de sistema ou aplicativo em cenários de diagnóstico e solução de problemas de mensagens de protocolo. Analisador de mensagem também permite que você tooload, agregação e analisar dados de log e arquivos de rastreamento salvos. Para obter mais informações sobre o Analisador de Mensagem, consulte [Guia Operacional do Analisador de Mensagem da Microsoft](http://technet.microsoft.com/library/jj649776.aspx).

Analisador de mensagem inclui ativos para o armazenamento do Azure que o ajudarão a tooanalyze logs do servidor, cliente e rede. Nesta seção, discutiremos como toouse tooaddress essas ferramentas Olá problema de baixo percentual sucesso Olá logs de armazenamento.

### <a name="download-and-install-message-analyzer-and-hello-azure-storage-assets"></a>Baixe e instale o analisador de mensagem e hello ativos de armazenamento do Azure
1. Baixar [Message Analyzer](http://www.microsoft.com/download/details.aspx?id=44226) de Olá Microsoft Download Center e execute o instalador de saudação.
2. Inicie o Analisador de Mensagem.
3. De saudação **ferramentas** menu, selecione **Asset Manager**. Em Olá **Asset Manager** caixa de diálogo, selecione **Downloads**, em seguida, filtre **armazenamento do Azure**. Você verá Olá ativos de armazenamento do Azure, conforme mostrado na imagem de saudação abaixo.
4. Clique em **sincronização de todos os itens exibidos** tooinstall Olá ativos de armazenamento do Azure. ativos de saudação disponíveis incluem:
   * **Regras de cores do armazenamento do Azure:** regras de cores do armazenamento do Azure permitem que você toodefine filtros especiais que usam a cor do texto, e os estilos toohighlight mensagens que contêm informações específicas em um rastreamento.
   * **Gráficos de Armazenamento do Azure:** os gráficos de Armazenamento do Azure são gráficos predefinidos que representam os dados de log do servidor. Observe que toouse gráficos de armazenamento do Azure no momento, você talvez só carga log do servidor de saudação em Olá grade de análise.
   * **Analisadores de armazenamento do Azure:** saudação do cliente de armazenamento do Azure analisadores análise Olá armazenamento do Azure, o servidor e o HTTP registra em log em ordem toodisplay em Olá grade de análise.
   * **Filtros de armazenamento do Azure:** filtros de armazenamento do Azure são critérios predefinidos que você pode usar tooquery seus dados em Olá grade de análise.
   * **Layouts do modo de armazenamento do Azure:** layouts do modo de armazenamento do Azure são layouts de coluna predefinidos e agrupamentos em Olá grade de análise.
5. Reinicie o analisador de mensagem depois de instalar os ativos de saudação.

![Gerenciador de Ativos do Analisador de Mensagem](./media/storage-e2e-troubleshooting/mma-start-page-1.png)

> [!NOTE]
> Instale todos os ativos de armazenamento do Azure Olá mostrados para fins de saudação deste tutorial.
> 
> 

### <a name="import-your-log-files-into-message-analyzer"></a>Importar os arquivos de log para o Analisador de Mensagem
Você pode importar todos os arquivos de log salvos (do servidor, cliente e rede) para uma única sessão do Analisador de Mensagem da Microsoft para análise.

1. Em Olá **arquivo** no analisador de mensagem da Microsoft, clique em **nova sessão**e, em seguida, clique em **sessão em branco**. Em Olá **nova sessão** caixa de diálogo, digite um nome para sua sessão de análise. Em Olá **detalhes da sessão** do painel, clique em Olá **arquivos** botão.
2. dados de rastreamento tooload Olá rede gerados pelo analisador de mensagem, clique em **adicionar arquivos**, procurar toohello no local onde você salvou o arquivo .matp da sessão de rastreamento da web, arquivo de .matp Olá select, e clique em **abrir**.
3. dados de log do servidor de saudação tooload, clique em **adicionar arquivos**, procure toohello local onde você baixou os logs do servidor, selecione os arquivos de log Olá para o intervalo de tempo Olá desejado tooanalyze e clique em **abrir**. Em seguida, no hello **detalhes da sessão** painel, a saudação do conjunto **configuração de Log de texto** suspenso para cada arquivo de log do lado do servidor de muito**AzureStorageLog** tooensure que a Microsoft Analisador de mensagem pode analisar o arquivo de log Olá corretamente.
4. dados de log do cliente de saudação tooload, clique em **adicionar arquivos**, procure toohello local onde você salvou os logs do lado do cliente, selecione os arquivos de log Olá desejado tooanalyze e clique em **abrir**. Em seguida, no hello **detalhes da sessão** painel, a saudação do conjunto **configuração de Log de texto** suspenso para cada arquivo de log do lado do cliente muito**AzureStorageClientDotNetV4** tooensure que Microsoft Message Analyzer pode analisar o arquivo de log Olá corretamente.
5. Clique em **iniciar** em Olá **nova sessão** dados de log de saudação de tooload e análise de caixa de diálogo. Exibe dados de log de saudação na grade de análise do analisador de mensagem de saudação.

imagem de saudação abaixo mostra uma sessão de exemplo configurada com o servidor, cliente e arquivos de log de rastreamento de rede.

![Configurar Sessão do Analisador de Mensagem](./media/storage-e2e-troubleshooting/configure-mma-session-1.png)

Observe que o Analisador de Mensagem carrega arquivos de log na memória. Se você tiver um grande conjunto de dados de log, você desejará toofilter na ordem tooget Olá melhor desempenho do analisador de mensagem.

Primeiro, determinar o período de tempo de saudação que você está interessado em examinar e manter esse período de tempo menor possível. Em muitos casos, você desejará tooreview um período de minutos ou horas no máximo. Importe o menor conjunto Olá logs que pode atender às suas necessidades.

Se você ainda tiver uma grande quantidade de dados de log, em seguida, convém toospecify um toofilter de filtro de sessão seus dados de log antes de carregá-lo. Em Olá **sessão filtro** caixa, selecione Olá **biblioteca** botão toochoose um filtro predefinido; por exemplo, escolha **Global tempo filtro I** de saudação filtros de armazenamento do Azure toofilter em um intervalo de tempo. Você pode editar Olá filtro critérios toospecify Olá começando e terminando o carimbo de hora para o intervalo de saudação deseja toosee. Você também pode filtrar em um código de status específico; Por exemplo, você pode escolher as entradas de log somente tooload onde o código de status de saudação é 404.

Para obter mais informações sobre como importar os dados de log para o Analisador de Mensagem da Microsoft, consulte [Recuperar Dados da Mensagem](http://technet.microsoft.com/library/dn772437.aspx) no TechNet.

### <a name="use-hello-client-request-id-toocorrelate-log-file-data"></a>Usar dados de arquivo hello cliente solicitação ID toocorrelate log
Olá biblioteca de cliente de armazenamento do Azure gera automaticamente uma ID de solicitação de cliente exclusivos para cada solicitação. Esse valor é escrito toohello log do cliente, log de servidor de saudação e rastreamento de rede hello, para que você pode usá-lo toocorrelate dados em todos os três logs no analisador de mensagem. Consulte [ID de solicitação do cliente](storage-monitoring-diagnosing-troubleshooting.md#client-request-id) para obter informações adicionais sobre o cliente Olá ID da solicitação

seções de saudação abaixo descrevem como toouse pré-configurado e modos de exibição de layout personalizado toocorrelate e agrupar dados com base na solicitação de cliente de saudação ID.

### <a name="select-a-view-layout-toodisplay-in-hello-analysis-grid"></a>Selecione um toodisplay de layout do modo de exibição no hello grade de análise
saudação de ativos de armazenamento para o analisador de mensagem incluir Layouts de exibição de armazenamento do Azure, são exibições pré-configurado que você pode usar toodisplay seus dados com colunas e agrupamentos útil para cenários diferentes. Você também pode criar layouts de modo de exibição personalizado e salvá-los para reutilização.

Olá figura abaixo mostra o hello **exibição Layout** menu, disponível ao selecionar **exibição Layout** da faixa de opções de barra de ferramentas de saudação. layouts do modo Olá para o armazenamento do Azure são agrupados em Olá **armazenamento do Azure** nó no menu de saudação. Você pode procurar `Azure Storage` no hello toofilter de caixa de pesquisa no armazenamento do Azure exiba apenas os layouts. Você também pode selecionar Olá estrela próxima tooa exibição layout toomake it um favorito e exibi-lo na parte superior de saudação do menu hello.

![Menu Layout de Exibição](./media/storage-e2e-troubleshooting/view-layout-menu.png)

toobegin com select **agrupados por módulo e ClientRequestID**. Esse layout de exibição agrupa os dados de log de todos os três logs, primeiro pela ID de solicitação do cliente, depois pelo arquivo de log de origem (ou **Módulo** no Analisador de Mensagem). Nesta exibição, você pode fazer uma busca detalhada em uma ID de solicitação de cliente específico e ver os dados de todos os três arquivos de log para essa ID de solicitação de cliente.

imagem de saudação abaixo mostra estes layout exibir aplicado toohello log dados de exemplo, com um subconjunto de colunas exibidas. Você pode ver que para uma ID de solicitação de cliente específico, Olá Analysis grade exibe dados de log de saudação do cliente, o log do servidor e o rastreamento de rede.

![Layout de Exibição do Armazenamento do Azure](./media/storage-e2e-troubleshooting/view-layout-client-request-id-module.png)

> [!NOTE]
> Arquivos de log diferentes têm diferentes colunas, para que quando os dados de vários arquivos de log são exibidos em Olá grade de análise, algumas colunas não podem conter todos os dados para uma determinada linha. Por exemplo, na Figura Olá acima, as linhas de log do cliente não mostram nenhum dado para Olá **Timestamp**, **TimeElapsed**, **fonte**, e **dedestino** colunas, porque essas colunas não existem no log de saudação do cliente, mas existem no rastreamento de rede hello. Da mesma forma, Olá **Timestamp** coluna exibe dados de carimbo de hora de log do servidor de saudação, mas nenhum dado é exibido para Olá **TimeElapsed**, **fonte**, e  **Destino** colunas, que não fazem parte do log de saudação do servidor.
> 
> 

Além disso layouts do modo de armazenamento do Azure de saudação de toousing, também pode definir e salvar seus próprios layouts do modo de exibição. Você pode selecionar outros campos desejados para o agrupamento de dados e salve o agrupamento de saudação como parte de seu layout personalizado também.

### <a name="apply-color-rules-toohello-analysis-grid"></a>Aplicar regras de cor toohello grade de análise
Olá ativos de armazenamento também incluem regras de cor, que oferecem que um visual significa tooidentify diferentes tipos de erros em Olá grade de análise. Olá regras de cor predefinidos aplicam tooHTTP erros, para que eles aparecem somente para rastreamento de log e de rede do servidor de saudação.

regras de cores tooapply, selecione **regras de cores** da faixa de opções do hello barra de ferramentas. Você verá as regras de cores de armazenamento do Azure Olá no menu de saudação. Tutorial de saudação, selecione **erros de cliente (StatusCode entre 400 e 499)**, conforme mostrado na imagem de saudação abaixo.

![Layout de Exibição do Armazenamento do Azure](./media/storage-e2e-troubleshooting/color-rules-menu.png)

Além disso toousing Olá armazenamento do Azure regras de cores, você também pode definir e salvar suas próprias regras de cor.

### <a name="group-and-filter-log-data-toofind-400-range-errors"></a>Agrupar e filtrar dados de log toofind erros de intervalo de 400
Em seguida, vamos agrupar e filtrar toofind de dados de log Olá todos os erros no intervalo de saudação 400.

1. Localizar Olá **StatusCode** coluna Olá grade de análise, coluna de saudação atalho título e selecione **grupo**.
2. Em seguida, agrupa Olá **ClientRequestId** coluna. Você verá que dados Olá Olá que Analysis grade agora é organizada por status de código e por solicitação do cliente ID.
3. Exibir janela de ferramenta do filtro de exibição Olá se ainda não estiver sendo exibida. Na faixa de opções de barra de ferramentas hello, selecione **janelas de ferramentas**, em seguida, **filtro de exibição**.
4. erros toofilter Olá log dados toodisplay apenas do intervalo de 400, adicionar Olá toohello de critérios de filtro a seguir **filtro de exibição** janela e clique em **aplicar**:

    ```   
    (AzureStorageLog.StatusCode >= 400 && AzureStorageLog.StatusCode <=499) || (HTTP.StatusCode >= 400 && HTTP.StatusCode <= 499)
    ```

imagem de saudação abaixo mostra os resultados de saudação desse agrupamento e o filtro. Olá expansão **ClientRequestID** campo abaixo Olá agrupamento para o código de status 409, por exemplo, mostra uma operação que resultou no código de status.

![Layout de Exibição do Armazenamento do Azure](./media/storage-e2e-troubleshooting/400-range-errors1.png)

Depois de aplicar esse filtro, você verá que são excluídas linhas do log de saudação do cliente, como Olá log do cliente não inclui um **StatusCode** coluna. toobegin com, vamos examinar o servidor de saudação e rede rastreamento registra toolocate 404 erros e, em seguida, retornaremos toohello cliente tooexamine Olá cliente operações de log que levaram toothem.

> [!NOTE]
> Você pode filtrar Olá **StatusCode** coluna e ainda exibir dados de todos os três logs, incluindo Olá log do cliente, se você adicionar uma expressão de filtro de toohello que inclui entradas de log em que o código de status de saudação é nulo. tooconstruct esta expressão de filtro, use:
> 
> <code>&#42;StatusCode >= 400 or !&#42;StatusCode</code>
> 
> Esse filtro retorna todas as linhas de cliente Olá log e somente as linhas do log de saudação do servidor e o log HTTP onde o código de status de saudação é maior que 400. Se você o aplicar layout de exibição toohello agrupada por ID de solicitação do cliente e o módulo, você pode pesquisar ou toofind de entradas de log a rolar Olá aquelas em que todos os três logs são representados.   
> 
> 

### <a name="filter-log-data-toofind-404-errors"></a>Filtrar dados de log toofind 404 erros
Olá ativos de armazenamento incluem filtros predefinidos que você pode usar toonarrow erros de saudação de toofind de dados de log ou tendências que você está procurando. Em seguida, podemos vai aplicar dois filtros predefinidos: uma que filtra o servidor de saudação e logs de rastreamento de rede para 404 erros e outra que filtra dados Olá em um intervalo de tempo especificado.

1. Exibir janela de ferramenta do filtro de exibição Olá se ainda não estiver sendo exibida. Na faixa de opções de barra de ferramentas hello, selecione **janelas de ferramentas**, em seguida, **filtro de exibição**.
2. Na janela de filtro de exibição hello, selecione **biblioteca**e pesquisar `Azure Storage` Olá toofind filtros de armazenamento do Azure. Filtro de saudação Select para **404 (não encontrado) de mensagens em todos os logs**.
3. Saudação de exibição **biblioteca** menu novamente, localize e selecione Olá **filtro de tempo Global**.
4. Edite os carimbos de hora Olá mostrados no intervalo de toohello filtro Olá que desejar tooview. Isso ajudará o intervalo de saudação do toonarrow de tooanalyze de dados.
5. O filtro deve aparecer semelhante toohello exemplo a seguir. Clique em **aplicar** tooapply Olá filtro toohello grade de análise.

    ```   
    ((AzureStorageLog.StatusCode == 404 || HTTP.StatusCode == 404)) And
    (#Timestamp >= 2014-10-20T16:36:38 and #Timestamp <= 2014-10-20T16:36:39)
    ```

    ![Layout de Exibição do Armazenamento do Azure](./media/storage-e2e-troubleshooting/404-filtered-errors1.png)

### <a name="analyze-your-log-data"></a>Analisar os dados de log
Agora que agrupadas e filtrar os dados, você pode examinar os detalhes de saudação de solicitações individuais que geraram 404 erros. No layout de exibição atual hello, dados de saudação são agrupados por ID de solicitação do cliente, em seguida, pela fonte de log. Desde que nós estamos filtrando em solicitações onde o campo de StatusCode Olá contém 404, veremos apenas servidor hello e dados de rastreamento de rede, não Olá cliente dados de log.

imagem de saudação abaixo mostra uma solicitação específica em que uma operação obter Blob gerou 404 porque não existia blob hello. Observe que algumas colunas foram removidas do modo de exibição padrão nos dados relevantes do pedido toodisplay Olá Olá.

![Logs de Rastreamento Filtrados do Servidor e da Rede](./media/storage-e2e-troubleshooting/server-filtered-404-error.png)

Em seguida, vai correlacionamos essa ID de solicitação do cliente com hello toosee de dados de log de cliente que cliente de saudação ações estava demorando quando ocorreu um erro de saudação. Você pode exibir uma nova exibição de grade de análise para estas sessão tooview Olá log dados do cliente, que é aberto em uma segunda guia:

1. Primeiro, copie o valor de saudação do hello **ClientRequestId** área de transferência do campo toohello. Você pode fazer isso marcando ou linha, localizando Olá **ClientRequestId** campo, clicando duas vezes no valor dos dados hello e escolhendo **cópia 'ClientRequestId'**.
2. Na faixa de opções de barra de ferramentas hello, selecione **novo Visualizador**, em seguida, selecione **Analysis grade** tooopen uma nova guia do novo guia Olá mostra todos os dados nos arquivos de log, sem agrupamento, filtragem ou regras de cores.
3. Na faixa de opções de barra de ferramentas hello, selecione **exibição Layout**, em seguida, selecione **todas as colunas de cliente .NET** em Olá **armazenamento do Azure** seção. Este layout de exibição mostra dados de log de saudação do cliente, bem como Olá logs de rastreamento de rede e o servidor. Por padrão, ela é classificada em Olá **MessageNumber** coluna.
4. Em seguida, procure o log de cliente Olá Olá ID de solicitação de cliente Na faixa de opções de barra de ferramentas hello, selecione **encontrar mensagens**, em seguida, especifique um filtro personalizado na ID de solicitação de cliente de saudação do hello **localizar** campo. Use esta sintaxe para filtro hello, especificando sua ID de solicitação do cliente:

    ```
    *ClientRequestId == "398bac41-7725-484b-8a69-2a9e48fc669a"
    ```

Analisador de mensagem localiza e seleciona Olá primeira entrada de log em que os critérios de pesquisa Olá corresponde Olá ID de solicitação de cliente No log de cliente hello, existem várias entradas para cada ID de solicitação do cliente, portanto, talvez você queira toogroup-los em hello **ClientRequestId** toomake de campo-lo mais fácil toosee-los todos juntos. imagem Olá abaixo mostra todas as mensagens de saudação no cliente de saudação de log para Olá especificado a ID de solicitação do cliente.

![Log do cliente mostrando erros 404](./media/storage-e2e-troubleshooting/client-log-analysis-grid1.png)

Usando dados Olá mostrados em layouts de exibição Olá nessas duas guias, você pode analisar Olá toodetermine de dados de solicitação que pode ter causado o erro hello. Você também pode examinar solicitações que antecederam esse um toosee se um evento anterior talvez possam ter levado erro 404 toohello. Por exemplo, você pode examinar as entradas de log do cliente Olá anterior neste toodetermine de ID de solicitação do cliente se o blob Olá pode ter sido excluído, ou se o erro Olá venceu toohello aplicativo de cliente chamar uma API CreateIfNotExists em um contêiner ou blob. No log de cliente Olá, você pode encontrar o endereço de saudação do blob no hello **descrição** campo; no servidor de saudação e logs de rastreamento de rede, essas informações aparecem no hello **resumo** campo.

Depois que você sabe o endereço de saudação do blob de saudação que gerou o erro 404 de saudação, você poderá investigar mais. Se você pesquisar entradas de log de saudação para outras mensagens associadas com operações em Olá mesmo blob, você pode verificar se o cliente Olá excluído anteriormente entidade hello.

## <a name="analyze-other-types-of-storage-errors"></a>Analisar outros tipos de erros de armazenamento
Agora que você estiver familiarizado com o analisador de mensagem tooanalyze seus dados de log, você pode analisar outros tipos de erros usando o modo de exibição de pesquisa/filtragem, regras de cores e layouts. Olá tabelas abaixo lista alguns problemas que você pode encontrar e Olá critérios de filtro, você pode usar toolocate-los. Para obter mais informações sobre como construir filtros e o analisador de mensagem de saudação filtragem de idioma, consulte [filtrando dados de mensagem](http://technet.microsoft.com/library/jj819365.aspx).

| tooInvestigate... | Use a Expressão do Filtro... | Expressão aplica-se tooLog (cliente, servidor, rede, todos) |
| --- | --- | --- |
| Atrasos inesperados na entrega de mensagens em uma fila |AzureStorageClientDotNetV4.Description contém "Repetindo a operação que falhou". |Cliente |
| Aumento de HTTP no PercentThrottlingError |HTTP.Response.StatusCode   == 500 &#124;&#124; HTTP.Response.StatusCode == 503 |Rede |
| Aumento em PercentTimeoutError |HTTP.Response.StatusCode   == 500 |Rede |
| Aumento em PercentTimeoutError (todos) |*StatusCode   == 500 |Todos |
| Aumento em PercentNetworkError |AzureStorageClientDotNetV4.EventLogEntry.Level   < 2 |Cliente |
| Mensagens HTTP 403 (Proibido) |HTTP.Response.StatusCode   == 403 |Rede |
| Mensagens HTTP 404 (Não encontrado) |HTTP.Response.StatusCode   == 404 |Rede |
| 404 (todos) |*StatusCode   == 404 |Todos |
| Problema de autorização de SAS (Assinatura de Acesso Compartilhado) |AzureStorageLog.RequestStatus ==  "SASAuthorizationError" |Rede |
| Mensagens HTTP 409 (Conflito) |HTTP.Response.StatusCode   == 409 |Rede |
| 409 (todos) |*StatusCode   == 409 |Todos |
| Baixo PercentSuccess ou as entradas de log analíticas têm operações com status de transação de ClientOtherErrors |AzureStorageLog.RequestStatus ==   "ClientOtherError" |Servidor |
| Aviso Nagle |((AzureStorageLog.EndToEndLatencyMS   - AzureStorageLog.ServerLatencyMS) > (AzureStorageLog.ServerLatencyMS *   1.5)) and (AzureStorageLog.RequestPacketSize <1460) and (AzureStorageLog.EndToEndLatencyMS -   AzureStorageLog.ServerLatencyMS >= 200) |Servidor |
| Intervalo de horas nos logs de Servidor e Rede |#Timestamp   >= 2014-10-20T16:36:38 e #Timestamp <= 2014-10-20T16:36:39 |Servidor, Rede |
| Intervalo de horas nos logs de Servidor |AzureStorageLog.Timestamp   >= 2014-10-20T16:36:38 e AzureStorageLog.Timestamp <=   2014-10-20T16:36:39 |Servidor |

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre cenários de ponta a ponta para solução de problemas no Armazenamento do Azure, consulte estes recursos:

* [Monitoramento, diagnóstico e solução de problemas de Armazenamento do Microsoft Azure](storage-monitoring-diagnosing-troubleshooting.md)
* [Análise de Armazenamento](http://msdn.microsoft.com/library/azure/hh343270.aspx)
* [Monitorar uma conta de armazenamento Olá portal do Azure](storage-monitor-storage-account.md)
* [Transferência de dados com hello AzCopy utilitário de linha de comando](storage-use-azcopy.md)
* [Guia Operacional do Analisador de Mensagem da Microsoft](http://technet.microsoft.com/library/jj649776.aspx)
