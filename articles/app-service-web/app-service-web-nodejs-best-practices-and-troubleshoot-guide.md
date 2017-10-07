---
title: "práticas recomendadas de aaaBest e guia de solução de problemas para aplicativos de nó em aplicativos Web do Azure"
description: "Saiba Olá práticas recomendadas e etapas de solução de problemas para aplicativos de nó em aplicativos Web do Azure."
services: app-service\web
documentationcenter: nodejs
author: ranjithr
manager: wadeh
editor: 
ms.assetid: 387ea217-7910-4468-8987-9a1022a99bef
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 06/06/2016
ms.author: ranjithr
ms.openlocfilehash: 975898142a224f14df1091a46d16e9074d9e2831
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-and-troubleshooting-guide-for-node-applications-on-azure-web-apps"></a>Guia de solução de problemas e práticas recomendadas para aplicativos de nó em Aplicativos Web do Azure
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

Neste artigo, você aprenderá Olá práticas recomendadas e etapas de solução de problemas para [aplicativos node](app-service-web-get-started-nodejs.md) em execução no Azure Webapps (com [iisnode](https://github.com/azure/iisnode)).

> [!WARNING]
> Tenha cuidado ao usar as etapas de solução de problemas no site de produção. Recomendação é tootroubleshoot seu aplicativo na instalação, por exemplo, o slot de preparação de não produção e Olá problema for corrigido, trocar o slot de preparo com o slot de produção.
> 
> 

## <a name="iisnode-configuration"></a>Configuração de IISNOD
Isso [arquivo de esquema](https://github.com/Azure/iisnode/blob/master/src/config/iisnode_schema_x64.xml) mostra todas as configurações de saudação que podem ser configuradas para iisnode. Algumas das configurações de saudação que serão úteis para seu aplicativo são:

* nodeProcessCountPerApplication
  
    Essa configuração controla o número de saudação de processos de nó que são iniciados por aplicativo do IIS. O valor padrão é 1. Você pode iniciar do node.exe tantos como sua contagem de núcleos VM, definindo essa too0. Valor recomendado é 0 para a maioria dos aplicativos, portanto você pode utilizar todos os núcleos de saudação em seu computador. Node.exe é single threaded para um node.exe consumirá um máximo de 1 núcleo tooget máximo desempenho e fora do seu aplicativo do nó seria conveniente tooutilize todos os núcleos.
* nodeProcessCommandLine
  
    Essa configuração controla Olá caminho toohello node.exe. Você pode definir essa versão do valor toopoint tooyour node.exe.
* maxConcurrentRequestsPerProcess
  
    Essa configuração controla o número máximo de saudação de solicitações simultâneas enviadas pelo iisnode tooeach node.exe. No azure webapps, Olá padrão valor é infinito. Você não terá tooworry sobre essa configuração. Fora do azure webapps, o valor padrão de saudação é 1024. Você talvez queira tooconfigure dependendo de quantas solicitações seu aplicativo obtém e rapidez seu aplicativo processa cada solicitação.
* maxNamedPipeConnectionRetry
  
    Essa configuração controla o número máximo de saudação de vezes iisnode tentará fazer conexão em Olá nomeado solicitação de saudação do pipe toosend sobre toonode.exe. Essa configuração em combinação com namedPipeConnectionRetryDelay determina o tempo limite total de saudação de cada solicitação dentro de iisnode. O valor padrão é 200 no Azure Webapps. Total Timeout em segundos = (maxNamedPipeConnectionRetry \* namedPipeConnectionRetryDelay)/1000
* namedPipeConnectionRetryDelay
  
    Essa quantidade de saudação de controles de configuração do iisnode de tempo (em ms) irá aguardar entre cada repetição toosend solicitação toonode.exe sobre Olá pipe nomeado. O valor padrão é 250 ms.
    Total Timeout em segundos = (maxNamedPipeConnectionRetry \* namedPipeConnectionRetryDelay)/1000
  
    Por padrão, Olá o tempo de espera total em iisnode no azure webapps é 200 \* 250ms = 50 segundos.
* logDirectory
  
    Essa configuração controla o diretório Olá onde iisnode registrará stdout/stderr. Valor padrão é iisnode, que é relativo toohello script principal diretório (diretório onde server.js principal está presente)
* debuggerExtensionDll
  
    Essa configuração controla qual versão de node-inspector o iisnode usará ao depurar o aplicativo de nó. No momento iisnode de Inspetor de 0.7.3.dll e iisnode inspector.dll Olá apenas 2 valores são válidos para esta configuração. O valor padrão é iisnode-inspector-0.7.3.dll. versão do iisnode de Inspetor de 0.7.3.dll usa o nó de Inspetor de 0.7.3 e usa os websockets, portanto, será necessário tooenable websockets em seu aplicativo Web do azure toouse nesta versão. Consulte <http://www.ranjithr.com/?p=98> para obter mais detalhes sobre como tooconfigure iisnode toouse Olá Inspetor de nó de novo.
* flushResponse
  
    comportamento padrão de saudação do IIS é que ele armazena em buffer os dados de resposta backup too4MB antes de liberar, ou até o término de saudação da resposta hello, o que ocorrer primeiro. iisnode oferece uma configuração toooverride esse comportamento: tooflush um fragmento do corpo de entidade de resposta Olá assim que iisnode recebe do node.exe, é necessário tooset Olá iisnode/@flushResponse atributo no Web. config too'true':
  
    ```
    <configuration>    
        <system.webServer>    
            <!-- ... -->    
            <iisnode flushResponse="true" />    
        </system.webServer>    
    </configuration>
    ```
  
    Habilitar a eliminação de cada fragmento do corpo de entidade de resposta Olá aumenta a sobrecarga de desempenho que reduz a taxa de transferência de saudação do sistema Olá, aproximadamente 5% (a partir de v0.1.13), portanto, é melhor tooscope este tooendpoints somente de configuração que requerem resposta de streaming (por exemplo, usando Olá <location> elemento Olá Web. config)
  
    Em toothis de adição para streaming de aplicativos, você precisará tooalso responseBufferLimit de conjunto de seu too0 de manipulador do iisnode.
  
    ```
    <handlers>    
        <add name="iisnode" path="app.js" verb="\*" modules="iisnode" responseBufferLimit="0"/>    
    </handlers>
    ```
* watchedFiles
  
    Essa é uma lista de arquivos separados por ponto e vírgula que serão observados para detectar alterações. Um arquivo de tooa alteração faz com que Olá toorecycle de aplicativo. Cada entrada consiste em um nome de diretório opcional e o nome de arquivo necessários que são toohello relativo diretório onde o ponto de entrada principal do aplicativo hello está localizado. Caracteres curinga é permitida na parte de nome de arquivo hello somente. O valor padrão é “\*.js;web.config”
* recycleSignalEnabled
  
    O valor padrão é falso. Se habilitada, o aplicativo de nó pode se conectar a tooa pipe nomeado (a variável de ambiente IISNODE\_controle\_PIPE) e enviar uma mensagem de "reciclagem". Normalmente, isso causará Olá w3wp toorecycle.
* idlePageOutTimePeriod
  
    O valor padrão é 0, o que significa que esse recurso está desabilitado. Quando set toosome valor maior que 0, iisnode pagina todos os seus filhos processa cada 'idlePageOutTimePeriod' milissegundos. toounderstand o que a paginação significa, consulte toothis [documentação](https://msdn.microsoft.com/library/windows/desktop/ms682606.aspx). Essa configuração será útil para aplicativos que consomem muita memória e deseja toopageout memória toodisk ocasionalmente toofree alguns RAM.

> [!WARNING]
> Tenha cuidado ao habilitar as definições de configuração a seguir nos aplicativos de produção de hello. Recomendação é toonot habilitá-los em aplicativos de produção.
> 
> 

* debugHeaderEnabled
  
    valor padrão de saudação é false. Se definir tootrue, iisnode adicionará uma resposta cabeçalho depuração iisnode tooevery HTTP resposta HTTP envia o valor do cabeçalho iisnode-debug Olá é uma URL. As partes individuais de informações de diagnóstico podem ser obtidas examinando o fragmento de URL Olá, mas uma visualização muito melhor é obtida abrindo Olá URL no navegador de saudação.
* loggingEnabled
  
    Essa configuração controla o registro em log de saudação de stdout e stderr iisnode. Iisnode irá capturar stdout/stderr a partir de processos de nó, que ela inicia e escrever toohello diretório especificado na configuração de 'logDirectory' hello. Depois que isso esteja habilitado, seu aplicativo escreverá sistema de arquivos toohello logs e, dependendo da quantidade de saudação de log feito pelo aplicativo hello, pode haver implicações de desempenho.
* devErrorsEnabled
  
    O valor padrão é falso. Quando definido como tootrue, iisnode exibirá o código de status HTTP da saudação e código de erro do Win32 no seu navegador. código do win32 Olá poderão ser úteis na depuração de determinados tipos de problemas.
* debuggingEnabled (não habilitar em sites de produção ativos)
  
    Essa configuração controla o recurso de depuração. Iisnode é integrado a node-inspector. Habilitando essa configuração, você habilita a depuração do aplicativo de nó. Quando essa configuração está habilitada, iisnode será layout Olá Inspetor de nó necessário arquivos 'debuggerVirtualDir' pasta de aplicativo hello primeiro depuração solicitação tooyour nó. Você pode carregar o Inspetor de nó Olá enviando uma solicitação toohttp://yoursite/server.js/debug. Você pode controlar o segmento de URL de depuração Olá com configuração de 'debuggerPathSegment'. Por padrão, debuggerPathSegment='debug'. Você pode definir essa GUID tooa por exemplo, para que seja mais difícil toobe descoberto por outros.
  
    Confira este [link](https://tomasz.janczuk.org/2011/11/debug-nodejs-applications-on-windows.html) para obter mais detalhes sobre a depuração.

## <a name="scenarios-and-recommendationstroubleshooting"></a>Cenários e recomendações/solução de problemas
### <a name="my-node-application-is-making-too-many-outbound-calls"></a>O aplicativo de nó está fazendo muitas chamadas de saída.
Muitos aplicativos desejaria toomake conexões de saída como parte de sua operação regular. Por exemplo, quando uma solicitação chega, seu aplicativo do nó seria deseja toocontact uma API REST em outro lugar e obter uma solicitação de saudação tooprocess informações. Ao fazer chamadas http ou https, você desejaria toouse um agente de keep alive. Por exemplo, você pode usar o módulo de agentkeepalive de saudação como seu agente de keep alive ao fazer essas chamadas de saída. Isso garante que soquetes Olá são reutilizados em seu aplicativo Web do azure VM e reduzindo sobrecarga de saudação de criação de novos soquetes para cada solicitação de saída. Além disso, isso garante que você está usando um número menor de soquetes toomake que muitas solicitações de saída e, portanto, você não exceda maxSockets Olá alocadas por VM. Recomendação no Azure Webapps seria tooset Olá agentKeepAlive maxSockets valor total de tooa de 160 sockets por VM. Isso significa que, se você tiver 4 node.exe em execução no hello VM, você desejaria tooset Olá agentKeepAlive maxSockets too40 por node.exe que é de 160 total por VM.

Exemplo de configuração [agentKeepALive](https://www.npmjs.com/package/agentkeepalive):

```
var keepaliveAgent = new Agent({    
    maxSockets: 40,    
    maxFreeSockets: 10,    
    timeout: 60000,    
    keepAliveTimeout: 300000    
});
```

Este exemplo pressupõe que haja quatro node.exe em execução na VM. Se você tiver um número diferente de node.exe em execução no hello VM, você terá toomodify Olá maxSockets configuração adequadamente.

### <a name="my-node-application-is-consuming-too-much-cpu"></a>Meu aplicativo de nó está consumindo muita CPU.
Você provavelmente obterá uma recomendação do Azure Webapps no portal sobre o alto consumo de cpu. Você também pode configurar monitores toowatch para determinados [métricas](web-sites-monitor.md). Ao verificar o uso de CPU de saudação em hello [painel do Portal do Azure](../application-insights/app-insights-web-monitor-performance.md), verifique se valores MAX Olá CPU você perca os valores de pico de saudação.
Em casos em que você acha que seu aplicativo está consumindo muito da CPU e você não pode explicar, você precisará tooprofile seu aplicativo de nó.

### 
#### <a name="profiling-your-node-application-on-azure-webapps-with-v8-profiler"></a>Criar o perfil do aplicativo de nó no Azure Webapps com o V8-Profiler
Por exemplo, permite que significa que você tenha um aplicativo do Olá mundo que você deseja tooprofile, conforme mostrado abaixo:

```
var http = require('http');    
function WriteConsoleLog() {    
    for(var i=0;i<99999;++i) {    
        console.log('hello world');    
    }    
}

function HandleRequest() {    
    WriteConsoleLog();    
}

http.createServer(function (req, res) {    
    res.writeHead(200, {'Content-Type': 'text/html'});    
    HandleRequest();    
    res.end('Hello world!');    
}).listen(process.env.PORT);
```

Vá tooyour scm site https://yoursite.scm.azurewebsites.net/DebugConsole

Você verá um prompt de comando, conforme mostrado abaixo. Vá para o diretório site/wwwroot

![](./media/app-service-web-nodejs-best-practices-and-troubleshoot-guide/scm_install_v8.png)

Execute o comando hello "npm install v8 profiler"

Isso deve instalar o v8-profiler no diretório node\_modules e todas as suas dependências.
Agora, edite seu tooprofile server.js seu aplicativo.

```
var http = require('http');    
var profiler = require('v8-profiler');    
var fs = require('fs');

function WriteConsoleLog() {    
    for(var i=0;i<99999;++i) {    
        console.log('hello world');    
    }    
}

function HandleRequest() {    
    profiler.startProfiling('HandleRequest');    
    WriteConsoleLog();    
    fs.writeFileSync('profile.cpuprofile', JSON.stringify(profiler.stopProfiling('HandleRequest')));    
}

http.createServer(function (req, res) {    
    res.writeHead(200, {'Content-Type': 'text/html'});    
    HandleRequest();    
    res.end('Hello world!');    
}).listen(process.env.PORT);
```

Olá acima alterações será criar o perfil de função de WriteConsoleLog hello e depois escrever Olá too'profile.cpuprofile de saída de perfil ' arquivo sob o wwwroot do site. Envie um aplicativo de tooyour de solicitação. Você verá um arquivo 'profile.cpuprofile' criado no site wwwroot.

![](./media/app-service-web-nodejs-best-practices-and-troubleshoot-guide/scm_profile.cpuprofile.png)

Baixar este arquivo e você precisará tooopen este arquivo com as ferramentas do Chrome F12. Pressionar F12 no chrome, clique no hello "Guia Perfis". Clique no botão "Carregar". Selecione o arquivo profile.cpuprofile que você acabou de baixar. Clique no perfil de saudação que acabou de ser carregado.

![](./media/app-service-web-nodejs-best-practices-and-troubleshoot-guide/chrome_tools_view.png)

Você verá que 95% de tempo de saudação foi consumida pela função WriteConsoleLog, conforme mostrado abaixo. Isso também mostra os números de linha exata de saudação e arquivos de origem que causam o problema de saudação.

### <a name="my-node-application-is-consuming-too-much-memory"></a>Meu aplicativo de nó está consumindo muita memória.
Você provavelmente obterá uma recomendação do Azure Webapps no portal sobre o alto consumo de memória. Você também pode configurar monitores toowatch para determinados [métricas](web-sites-monitor.md). Ao verificar o uso de memória de saudação no hello [painel do Portal do Azure](../application-insights/app-insights-web-monitor-performance.md), verifique se os valores MAX para memória Olá você perca os valores de pico de saudação.

#### <a name="leak-detection-and-heap-diffing-for-nodejs"></a>Detecção de perda e Comparação de Heap para node.js
Você pode usar [memwatch nó](https://github.com/lloyd/node-memwatch) perdas toohelp identificam a memória.
Você pode instalar memwatch assim como o criador de perfil v8 e editar que seu código toocapture e comparação heaps tooidentify Olá vazamentos de memória em seu aplicativo.

### <a name="my-nodeexes-are-getting-killed-randomly"></a>Os arquivos node.exe estão sendo encerrados aleatoriamente
Há alguns motivos pelos quais isso pode ocorrer:

1. Seu aplicativo está gerando exceções não capturadas – d: seleção de entre\\inicial\\LogFiles\\aplicativo\\arquivo de log Errors para obter detalhes de saudação na exceção de saudação. Este arquivo tem o rastreamento de pilha Olá para que você possa corrigir seu aplicativo com base nisso.
2. O aplicativo está consumindo muita memória, o que está impedindo outros processos de serem iniciados. Se memória total de VM Olá too100 fechar % node.exe foi interrompida por Olá processo manager toolet outros processos obter toodo uma chance algum trabalho. toofix isso, verifique se seu aplicativo não haverá vazamento de memória ou se seu aplicativo precisa realmente toouse muita memória, dimensionar o tooa VM maior com muito mais RAM.

### <a name="my-node-application-does-not-start"></a>O aplicativo de nó não é iniciado
Se o aplicativo está retornando Erros 500 na inicialização, pode haver alguns motivos:

1. Node.exe não está presente no local correto hello. Verifique a configuração nodeProcessCommandLine.
2. Arquivo de script principal não está presente no local correto hello. Web. config e certifique-se de que nome Olá Olá principal do arquivo de script no arquivo de script principal de Olá Olá manipuladores seção correspondências.
3. Configuração de Web. config não está correta – Consulte Olá nomes/valores de configurações.
4. Inicialização a frio – seu aplicativo estiver demorando muito toostartup. Se o aplicativo demorar mais do que (maxNamedPipeConnectionRetry \* namedPipeConnectionRetryDelay)/1000 segundos, iisnode retornará um erro 500. Aumente os valores de saudação do toomatch configurações que seu aplicativo Iniciar tempo tooprevent iisnode de tempo limite e retornar Olá 500 Erro.

### <a name="my-node-application-crashed"></a>Meu aplicativo de nó falhou
Seu aplicativo está gerando exceções não capturadas – d: seleção de entre\\inicial\\LogFiles\\aplicativo\\arquivo de log Errors para obter detalhes de saudação na exceção de saudação. Este arquivo tem o rastreamento de pilha Olá para que você possa corrigir seu aplicativo com base nisso.

### <a name="my-node-application-takes-too-much-time-toostartup-cold-start"></a>Meu aplicativo node leva muito toostartup de tempo (Iniciar frio)
O motivo mais comum para isso é que o aplicativo hello tem muitos arquivos no nó de saudação\_módulos e Olá aplicativo tentativas tooload maioria desses arquivos durante a inicialização. Por padrão, como os arquivos residem no compartilhamento de rede Olá em Webapps do Azure, carregando muitos arquivos pode levar algum tempo.
Algumas soluções toomake isso mais rápido são:

1. Verifique se que você tem uma estrutura simples de dependência e nenhuma dependência duplicada usando npm3 tooinstall seus módulos.
2. Tente carregar toolazy seu nó\_módulos e não carregar todos os módulos de saudação na inicialização. Isso significa que toorequire('module') de chamada hello deve ser feita quando você realmente precisa dentro da função hello tentar toouse módulo de saudação.
3. O Azure Webapps oferece um recurso chamado cache local. Esse recurso copia o conteúdo de saudação rede compartilhamento toohello disco local no hello VM. Olá como arquivos de saudação são locais, tempo de nó de carregamento\_módulos é muito mais rápido. -Neste [documentação](../app-service/app-service-local-cache.md) explica como toouse Cache Local em mais detalhes.

## <a name="iisnode-http-status-and-substatus"></a>Substatus e status http de IISNODE
Isso [arquivo de origem](https://github.com/Azure/iisnode/blob/master/src/iisnode/cnodeconstants.h) lista todos os Olá possíveis status/substatus combinação iisnode pode retornar no caso de erro.

Habilitar FREB para o código de erro win32 do aplicativo toosee hello (certifique-se de habilitar FREB somente em sites de não produção por motivos de desempenho).

| Status Http | SubStatus Http | Razão Possível? |
| --- | --- | --- |
| 500 |1000 |Houve algum problema distribuindo Olá solicitação tooIISNODE – Verifique se node.exe foi iniciado. Node.exe pode ter falhado na inicialização. Verifique se há erros na configuração de web.config. |
| 500 |1001 |-Win32Error 0x2 - o aplicativo não está respondendo toohello URL. Reescrita de URL de verificação de regras ou se seu aplicativo express rotas correto de saudação definidas. -Win32Error 0x6d – pipe nomeado está ocupado – Node.exe não está aceitando solicitações porque o pipe hello está ocupado. Verifique o alto uso da cpu. - Outros erros – verifique se node.exe falhou. |
| 500 |1002 |Falha de node.exe – confira d:\\home\\LogFiles\\logging-errors.txt para o rastreamento de pilha. |
| 500 |1003 |Configuração de pipe problema – você nunca verá isso mas se você fizer isso, Olá chamado pipe configuração está incorreta. |
| 500 |1004-1018 |Ocorreu algum erro ao enviar resposta de saudação solicitação ou processamento de saudação de node.exe. Verifique se node.exe falhou. verifique d:\\home\\LogFiles\\logging-errors.txt para rastrear a pilha. |
| 503 |1000 |Não há memória tooallocate mais conexões de pipe nomeadas. Verifique por que o aplicativo está consumindo tanta memória. Verifique o valor da configuração maxConcurrentRequestsPerProcess. Se ele não infinito e você tem muitas solicitações, aumentar esse valor tooprevent esse erro. |
| 503 |1001 |Solicitação não pôde ser expedida toonode.exe porque a reciclagem do aplicativo hello. Após a reciclagem do aplicativo hello, as solicitações devem ser atendidas normalmente. |
| 503 |1002 |Verificação de código de erro win32 por motivo real – a solicitação não pôde ser expedida tooa node.exe. |
| 503 |1003 |O pipe nomeado está muito ocupado – verifique se o nó está consumindo muita CPU |

Há uma configuração no NODE.exe chamada NODE\_PENDING\_PIPE\_INSTANCES. Por padrão, fora do Azure Webapps, esse valor é 4. Isso significa que node.exe só pode aceitar 4 solicitações em um horário Olá pipe nomeado. No Azure Webapps, esse valor é definido too5000 e esse valor deve ser suficiente para a maioria dos aplicativos de nó em execução no azure webapps. Você não deve ver 503.1003 no azure webapps porque temos um valor alto para Olá nó\_pendente\_PIPE\_INSTÂNCIAS.  |

## <a name="more-resources"></a>Mais recursos
Siga essas toolearn links mais sobre aplicativos node.js no serviço de aplicativo do Azure.

* [Get started with Node.js web apps in Azure App Service (Introdução aos aplicativos Web do Node.js no Serviço de Aplicativo do Azure)](app-service-web-get-started-nodejs.md)
* [Como toodebug um Node. js web app no serviço de aplicativo do Azure](web-sites-nodejs-debug.md)
* [Usando Módulos no Node.js com aplicativos do Microsoft Azure](../nodejs-use-node-modules-azure-apps.md)
* [Aplicativos Web do Serviço de Aplicativo do Azure: Node.js](https://blogs.msdn.microsoft.com/silverlining/2012/06/14/windows-azure-websites-node-js/)
* [Centro de Desenvolvedores do Node.js](../nodejs-use-node-modules-azure-apps.md)
* [Explorando Olá Super segredo Kudu depurar Console](https://azure.microsoft.com/documentation/videos/super-secret-kudu-debug-console-for-azure-web-sites/)

