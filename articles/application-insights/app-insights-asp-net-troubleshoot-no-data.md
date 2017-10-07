---
title: aaaTroubleshooting nenhum dado - Application Insights para .NET
description: "Não consegue ver os dados no Application Insights do Azure? Tente aqui."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: e231569f-1b38-48f8-a744-6329f41d91d3
ms.service: application-insights
ms.workload: mobile
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 261c25c89884c46e41bbc305474ac854360221ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-no-data---application-insights-for-net"></a>Solução de problemas de ausência de dados - Application Insights para .NET
## <a name="some-of-my-telemetry-is-missing"></a>Parte da minha telemetria está ausente
*No Application Insights, vejo apenas uma fração dos eventos de saudação que estão sendo gerados pelo meu aplicativo.*

* Se você estiver vendo consistentemente Olá mesmo fração, sua conclusão provavelmente tooadaptive [amostragem](app-insights-sampling.md). tooconfirm isso, abra a pesquisa (da folha de visão geral de saudação) e examinar uma instância de uma solicitação ou outro evento. Na parte inferior da saudação da seção de propriedades de saudação, clique em detalhes da propriedade completo tooget "…". Se Contagem de solicitações for > 1, a amostragem estará em operação. 
* Caso contrário, é possível que você esteja atingindo um [limite de taxa de dados](app-insights-pricing.md#limits-summary) para seu plano de preços. Esses limites são aplicados por minuto.

## <a name="no-data-from-my-server"></a>Nenhum dado do meu servidor
*Instalei meu aplicativo em meu servidor Web e agora não vejo nenhuma telemetria dele. Ele funcionou corretamente no meu computador de desenvolvimento.*

* Provavelmente um problema de firewall. [Definir exceções de firewall para dados do Application Insights toosend](app-insights-ip-addresses.md).

*Eu [instalou o Monitor de Status](app-insights-monitor-performance-live-website-now.md) em Meus aplicativos do web server toomonitor existente. Não consigo ver todos os resultados.*

* Veja [Solução de problemas do Monitor de Status](app-insights-monitor-performance-live-website-now.md#troubleshooting-runtime-configuration-of-application-insights). 

## <a name="q01"></a>A opção “Adicionar o Application Insights” não existe no Visual Studio
*Quando clico com o botão direito em um projeto existente no Gerenciador de Soluções, não vejo opções do Application Insights.*

* Nem todos os tipos de projeto .NET são suportados pelas ferramentas de saudação. Há suporte para projetos Web e WCF. Para outros tipos de projeto, como aplicativos de área de trabalho ou serviço, você ainda pode [adicionar um projeto do SDK do Application Insights tooyour manualmente](app-insights-windows-desktop.md).
* Certifique-se de que você tem o [Visual Studio 2013 Atualização 3 ou posterior](http://go.microsoft.com/fwlink/?LinkId=397827). Ela vem pré-instalado com ferramentas de análise do desenvolvedor, que fornecem Olá SDK do Application Insights.
* Escolha **Ferramentas**, **Extensões e Atualizações** e verifique se as **Ferramentas de Análise do Desenvolvedor** estão instaladas e habilitadas. Nesse caso, clique em **atualizações** toosee se houver uma atualização disponível.
* Abrir caixa de diálogo Olá novo projeto e escolha o aplicativo Web do ASP.NET. Se você vir Olá opção Application Insights, em seguida, Olá ferramentas estão instaladas. Caso contrário, tente desinstalar e, em seguida, reinstalar Olá ferramentas do Application Insights.

## <a name="q02"></a>Falha ao adicionar o Application Insights
*Quando tento projeto existente do tooan tooadd Application Insights, é exibida uma mensagem de erro.*

Causas mais prováveis:

* Falha na comunicação com o portal do Application Insights Olá; ou
* Há algum problema com sua conta do Azure;
* Você só tiver [acesso de leitura toohello assinatura ou grupo onde você estava tentando novo recurso do toocreate Olá](app-insights-resources-roles-access-control.md).

Correção:

* Verifique se você forneceu credenciais de logon para direita Olá conta do Azure. 
* No navegador, verifique se você tem acesso toohello [portal do Azure](https://portal.azure.com). Abra Configurações e veja se há alguma restrição.
* [Projeto existente do adicionar Application Insights tooyour](app-insights-asp-net.md): no Gerenciador de soluções, clique com botão direito seu projeto e escolha "Adicionar Application Insights".
* Se ainda não estiver funcionando, siga Olá [procedimento manual](app-insights-windows-services.md) tooadd um recurso no portal de saudação e, em seguida, adicione o projeto de tooyour SDK de saudação. 

## <a name="emptykey"></a>Recebo um erro "Chave de instrumentação não pode ser vazio"
Parece que algo deu errado enquanto você instalava o Application Insights, ou talvez um adaptador de registro em log.

No Gerenciador de Soluções, clique com o botão direito no projeto e escolha **Application Insights > Configurar Application Insights**. Você obterá uma caixa de diálogo que solicita a você toosign no tooAzure e crie um recurso do Application Insights, ou use novamente um existente.

## <a name="NuGetBuild"></a> "Pacotes NuGet estão ausentes" no meu servidor de build
*Tudo o que cria Okey quando eu estou depuração em minha máquina de desenvolvimento, mas recebo uma mensagem de erro do NuGet no servidor de compilação de saudação.*

Consulte [Restauração do Pacote NuGet](http://docs.nuget.org/Consume/Package-Restore) e [Restauração Automática do Pacote](http://docs.nuget.org/Consume/package-restore/migrating-to-automatic-package-restore).

## <a name="missing-menu-command-tooopen-application-insights-from-visual-studio"></a>Faltando tooopen de comando de menu do Application Insights do Visual Studio
*Quando eu clico com o botão direito do mouse no Gerenciador de Soluções do meu projeto, não vejo os comandos do Application Insights ou não vejo um comando Abrir Application Insights.*

Causas mais prováveis:

* Se você criou manualmente o recurso do Application Insights hello ou projeto de saudação é de um tipo que não é suportado pelas ferramentas do Application Insights hello.
* ferramentas de análise do desenvolvedor Olá estão desabilitadas no Visual Studio. 
* O Visual Studio é anterior à versão 2013 Atualização 3.

Correção:

* Verifique se a versão do Visual Studio é a 2013 atualização 3 ou posterior.
* Escolha **Ferramentas**, **Extensões e Atualizações** e verifique se as **Ferramentas de Análise do Desenvolvedor** estão instaladas e habilitadas. Nesse caso, clique em **atualizações** toosee se houver uma atualização disponível.
* Clique com o botão direito do mouse no projeto no Gerenciador de Soluções. Se você vir o comando Olá **Application Insights > configurar o Application Insights**, usá-lo tooconnect o recurso de toohello de projeto no hello serviço Application Insights.

Caso contrário, o tipo de projeto não tem suporte diretamente pelas ferramentas do Application Insights hello. toosee sua telemetria, entrar toohello [portal do Azure](https://portal.azure.com), escolha o Application Insights na barra de navegação à esquerda do hello e selecione seu aplicativo.

## <a name="access-denied-on-opening-application-insights-from-visual-studio"></a>“Acesso negado” ao abrir o Application Insights a partir do Visual Studio
*Olá comando de menu 'Abrir Application Insights' leva me toohello portal do Azure, mas eu recebo um erro "acesso negado".*

![](./media/app-insights-asp-net-troubleshoot-no-data/access-denied.png)

Olá Microsoft entrada que você usou no navegador padrão não tem acesso muito[Olá recurso que foi criado quando o Application Insights foi adicionado o aplicativo toothis](app-insights-asp-net.md). Há duas razões prováveis: 

* Você tem mais de uma conta da Microsoft - pode ser um trabalho e uma conta pessoal da Microsoft? Olá entrada que você usou no navegador padrão foi para uma conta diferente de Olá tendo acesso muito[adicionar Application Insights toohello projeto](app-insights-asp-net.md). 
  
  * Correção: Clique em seu nome na parte superior direita da janela do navegador hello e sair. Entre com hello conta que tenha acesso. Em seguida, na barra de navegação à esquerda do hello, clique em Application Insights e selecione seu aplicativo.
* Alguém adicionou o projeto de toohello do Application Insights e esqueceram toogive você [grupo de recursos do acesso toohello](app-insights-resources-roles-access-control.md) no qual ela foi criada. 
  
  * Correção: Se eles usou uma conta organizacional, eles poderão adicionar você team toohello; ou eles podem conceder a você acesso individual toohello grupo de recursos.

## <a name="asset-not-found-on-opening-application-insights-from-visual-studio"></a>“Ativo não encontrado” ao abrir o Application Insights do Visual Studio
*Olá comando de menu 'Abrir Application Insights' leva me toohello portal do Azure, mas eu recebo um erro 'ativo não encontrado'.*

Causas mais prováveis:

* saudação de recurso do Application Insights para seu aplicativo foi excluída; ou
* chave de instrumentação Olá foi definida ou alterada no applicationinsights. config editá-lo diretamente, sem atualizar o arquivo de projeto hello. 

chave de instrumentação Olá em controles de Applicationinsights onde telemetria Olá é enviada. Uma linha no arquivo de projeto Olá controla qual recurso é aberto quando você usar o comando Olá no Visual Studio. 

Correção:

* No Gerenciador de soluções, clique com botão direito hello e escolha Application Insights, configurar o Application Insights. Na caixa de diálogo Olá, escolha a telemetria de toosend tooan recurso existente ou criar um novo. Ou:
* Abrir o recurso de saudação diretamente. Entrar muito[Olá portal do Azure](https://portal.azure.com), clique Application Insights na barra de navegação à esquerda do hello e, em seguida, selecione seu aplicativo.

## <a name="where-do-i-find-my-telemetry"></a>Onde posso encontrar minha telemetria?
*Entrei em toohello [portal do Microsoft Azure](https://portal.azure.com), e estou olhando Olá painel da página inicial do Azure. Como eu encontro meus dados no Application Insights?*

* Na barra de navegação à esquerda do hello, clique em Application Insights, em seguida, o nome do aplicativo. Se você não tiver nenhum projeto existe, é necessário muito[adicionar ou configurar o Application Insights no seu projeto web](app-insights-asp-net.md).
  
    Lá, você verá alguns gráficos de resumo. Você pode clicá-los toosee mais detalhes.
* No Visual Studio, enquanto você estiver depurando seu aplicativo, clique botão do Application Insights hello.

## <a name="q03"></a> Nenhum dado do servidor (ou nenhum dado)
*Executei meu aplicativo e, em seguida, abrir o serviço do Application Insights Olá no Microsoft Azure, mas todos Olá gráficos Mostrar ' Saiba como toocollect... ' ou 'Não configurado'.* Ou *somente Exibição de Página e dados de usuário, mas nenhum dado do servidor.*

* Execute seu aplicativo em modo de depuração no Visual Studio (F5). Use aplicativo hello assim como toogenerate alguns telemetria. Verifique se você pode ver os eventos registrados na janela de saída do Visual Studio hello. 
  
    ![](./media/app-insights-asp-net-troubleshoot-no-data/output-window.png)
* No portal do Application Insights hello, abra [pesquisa diagnóstico](app-insights-diagnostic-search.md). Os dados normalmente aparecem aqui primeiro.
* Clique o botão de atualização de saudação. folha de saudação próprio atualiza periodicamente, mas você também pode fazer isso manualmente. intervalo de atualização de saudação é mais longo para intervalos de tempo maior.
* Verifique as chaves de instrumentação Olá correspondem. Na folha principal de saudação para seu aplicativo no portal do Application Insights hello, em Olá **Essentials** suspensa, examine **chave de instrumentação**. Em seguida, em seu projeto no Visual Studio, abra applicationinsights. config e localize Olá `<instrumentationkey>`. Verifique se Olá duas chaves são iguais. Caso contrário:
  
  * No portal de Olá, clique Application Insights e procure o recurso de aplicativo hello com chave direita da saudação; ou
  * No Gerenciador de soluções do Visual Studio, clique com botão direito hello e escolha o Application Insights, configurar. Redefina Olá aplicativo toosend telemetria toohello de recurso correta.
  * Se você não encontrar hello chaves correspondentes, verifique se você estiver usando Olá mesmo credenciais de entrada no Visual Studio como toohello portal.
    
    ![](./media/app-insights-asp-net-troubleshoot-no-data/ikey-check.png)
* Em Olá [dashboard inicial do Microsoft Azure](https://portal.azure.com), examine o mapa de serviço de integridade de saudação. Se houver algum alertas indicações, aguarde até que eles retornaram tooOK e, em seguida, feche e reabra a folha de aplicativos do Application Insights.
* Verifique também o [nosso blog de status](http://blogs.msdn.com/b/applicationinsights-status/).
* Foi gravar qualquer código de saudação [SDK do lado do servidor](app-insights-api-custom-events-metrics.md) que pode alterar a chave de instrumentação Olá no `TelemetryClient` instâncias ou no `TelemetryContext`? Ou gravou uma [configuração de filtro ou de amostragem](app-insights-api-filtering-sampling.md) que possa estar filtrando em excesso?
* Se você editou o applicationinsights. config, Verifique atentamente Olá configuração [TelemetryInitializers e TelemetryProcessors](app-insights-api-filtering-sampling.md). Um tipo nomeado incorretamente ou o parâmetro não pode causar Olá SDK toosend nenhum dado.

## <a name="q04"></a>Nenhum dado sobre Exibições de Página, Navegadores, Uso
*Vejo dados em tempo de resposta do servidor e gráficos de solicitações do servidor, mas nenhum dado em tempo de carregamento do modo de exibição de página ou em Olá navegador ou em folhas de uso.*

dados de saudação vêm de scripts em páginas da web de saudação. 

* Se você adicionou o Application Insights tooan existente de projeto da web, [você tiver scripts de saudação tooadd manualmente](app-insights-javascript.md).
* Tenha certeza de que o Internet Explorer não está exibindo o site no modo de Compatibilidade.
* Usar o recurso de depuração do navegador da saudação (F12 em alguns navegadores, rede, em seguida, escolha) tooverify dados estão sendo enviados muito`dc.services.visualstudio.com`.

## <a name="no-dependency-or-exception-data"></a>Nenhum dado de dependência ou de exceção
Confira [telemetria de dependência](app-insights-asp-net-dependencies.md) e [telemetria de exceção](app-insights-asp-net-exceptions.md).

## <a name="no-performance-data"></a>Nenhum dado de desempenho
Haverá dados de desempenho (CPU, taxa de E/S, etc.) disponíveis para [serviços Web Java](app-insights-java-collectd.md), [aplicativos da área de trabalho do Windows](app-insights-windows-desktop.md), [aplicativos Web e serviços do IIS se você instalar o Status Monitor](app-insights-monitor-performance-live-website-now.md) e os [Serviços de Nuvem do Azure](app-insights-azure.md). Encontre-os em Configurações, Servidores.

Esses dados não estão disponíveis para sites do Azure.

## <a name="no-server-data-since-i-published-hello-app-toomy-server"></a>Nenhum dado (servidor) desde que publiquei Olá servidor toomy de aplicativos
* Verifique se você realmente copiados Olá todos os Microsoft. DLLs de ApplicationInsights toohello server, junto com Microsoft.Diagnostics.Instrumentation.Extensions.Intercept.dll
* Em seu firewall, você pode ter muito[abrir algumas portas TCP](app-insights-ip-addresses.md#data-access-api).
* Se você tiver um proxy toosend toouse fora da sua rede corporativa, definir [defaultProxy](https://msdn.microsoft.com/library/aa903360.aspx) em Web. config
* Windows Server 2008: Verifique se você instalou Olá atualizações a seguir: [KB2468871](https://support.microsoft.com/kb/2468871), [KB2533523](https://support.microsoft.com/kb/2533523), [KB2600217](https://support.microsoft.com/kb/2600217).

## <a name="i-used-toosee-data-but-it-has-stopped"></a>Usei toosee dados, mas foi interrompido
* Verificar Olá [status blog](http://blogs.msdn.com/b/applicationinsights-status/).
* Você atingiu sua cota mensal de pontos de dados? Abra hello configurações/cotas e preços toofind-out. Nesse caso, você pode atualizar seu plano ou então pagar por capacidade adicional. Consulte Olá [preços esquema](https://azure.microsoft.com/pricing/details/application-insights/).

## <a name="i-dont-see-all-hello-data-im-expecting"></a>Não vejo todos os dados de saudação que eu estou esperando
Se seu aplicativo envia um lote de dados e você estiver usando hello SDK do Application Insights para ASP.NET versão 2.0.0-beta3 ou posterior, Olá [amostragem adaptável](app-insights-sampling.md) recurso pode operar e enviar apenas uma porcentagem da sua telemetria. 

Você pode desativá-lo, mas isso não é recomendado. A amostragem é projetada para que a telemetria relacionada seja corretamente transmitida para fins de diagnóstico. 

## <a name="wrong-geographical-data-in-user-telemetry"></a>Dados geográficos errados na telemetria do usuário
dimensões de país, região e cidade Olá são derivados de endereços IP e nem sempre são precisas.

## <a name="exception-method-not-found-on-running-in-azure-cloud-services"></a>Exceção "método não encontrado" em execução nos Serviços de Nuvem do Azure
Você compilou para .NET 4.6? O 4.6 não tem suporte automático nas funções dos Serviços de Nuvem do Azure. [Instale o 4.6 em cada função](../cloud-services/cloud-services-dotnet-install-dotnet.md) antes de executar seu aplicativo.

## <a name="still-not-working"></a>Ainda não está funcionando...
* [Fórum do Application Insights](https://social.msdn.microsoft.com/Forums/vstudio/en-US/home?forum=ApplicationInsights)

