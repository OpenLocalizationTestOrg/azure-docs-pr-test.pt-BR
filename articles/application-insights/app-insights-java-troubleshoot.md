---
title: aaaTroubleshoot Application Insights em um projeto da web de Java
description: "Guia de solução de problemas: monitoramento em tempo real aplicativos Java com o Application Insights."
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: ef602767-18f2-44d2-b7ef-42b404edd0e9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: bwren
ms.openlocfilehash: c274c01b1992971fae194c3e510512ca06ab76b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-and-q-and-a-for-application-insights-for-java"></a>Solução de problemas e perguntas e respostas para o Application Insights para Java
Dúvidas ou problemas com o [Azure Application Insights em Java][java]? Aqui estão algumas dicas.

## <a name="build-errors"></a>Erros de compilação
**No Eclipse, quando adicionar Olá SDK do Application Insights via Maven ou Gradle, recebo compilação ou a soma de verificação de erros de validação.**

* Se Olá dependência <version> elemento está usando um padrão com caracteres curinga (por exemplo, (Maven) `<version>[1.0,)</version>` ou (Gradle) `version:'1.0.+'`), tente especificar uma versão específica em vez disso, como `1.0.2`. Consulte Olá [notas de versão](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) para a versão mais recente do hello.

## <a name="no-data"></a>Sem dados
**Adicionei com êxito o Application Insights e executou meu aplicativo, mas nunca vi dados no portal de saudação.**

* Espere um minuto e clique em Atualizar. gráficos de saudação se atualizar periodicamente, mas você também pode atualizar manualmente. intervalo de atualização de saudação depende do intervalo de tempo de saudação do gráfico de saudação.
* Verifique se você tem uma chave de instrumentação definida no arquivo de ApplicationInsights.xml hello (na pasta de recursos de saudação em seu projeto)
* Verifique se não há nenhum `<DisableTelemetry>true</DisableTelemetry>` nó no arquivo xml de saudação.
* Em seu firewall, você pode ter tooopen as portas TCP 80 e 443 para toodc.services.visualstudio.com de tráfego de saída. Consulte Olá [lista completa de exceções do firewall](app-insights-ip-addresses.md)
* Olá Microsoft Azure inicia quadro, examine o mapa de status do serviço de saudação. Se houver algum alertas indicações, aguarde até que eles retornaram tooOK e, em seguida, feche e reabra a folha de aplicativos do Application Insights.
* Ative o log de janela de console do IDE toohello, adicionando um `<SDKLogger />` elemento no nó de raiz de saudação no arquivo de ApplicationInsights.xml hello (na pasta de recursos de saudação em seu projeto) e verificar se há entradas precedidos de [Erro].
* Certifique-se de que Olá correto ApplicationInsights.xml arquivo tem foi carregado com êxito pelo Olá Java SDK, observando mensagens de saída do console Olá para uma instrução "arquivo de configuração foi localizou com êxito".
* Se o arquivo de configuração de saudação não for encontrado, verifique Olá toosee de mensagens de saída em que o arquivo de configuração hello está sendo pesquisado e certifique-se de que Olá que applicationinsights.XML está localizado em um desses locais de pesquisa. Como regra geral, você pode colocar o arquivo de configuração de Olá próximo JARs do hello Application Insights SDK. Por exemplo: Tomcat, isso significaria Olá pasta WEB-INF/lib.

#### <a name="i-used-toosee-data-but-it-has-stopped"></a>Usei toosee dados, mas foi interrompido
* Verificar Olá [status blog](http://blogs.msdn.com/b/applicationinsights-status/).
* Você atingiu sua cota mensal de pontos de dados? Abra configurações/cotas e preços toofind out. Nesse caso, você pode atualizar seu plano ou então pagar por capacidade adicional. Consulte Olá [preços esquema](https://azure.microsoft.com/pricing/details/application-insights/).

#### <a name="i-dont-see-all-hello-data-im-expecting"></a>Não vejo todos os dados de saudação que eu estou esperando
* Abrir hello cotas e preços de folha e verifique se [amostragem](app-insights-sampling.md) está em operação. (transmissão de 100% significa que a amostragem não está em operação.) Olá serviço Application Insights pode ser conjunto tooaccept apenas uma fração de telemetria Olá que chega de seu aplicativo. Isso o ajuda a se manter dentro de sua cota mensal de telemetria. 

## <a name="no-usage-data"></a>Sem dados de uso
**Vejo dados sobre solicitações e tempos de resposta, mas não há dados de exibição de página, de navegador ou de usuário.**

Você configurar com êxito o telemetria do toosend seu aplicativo do servidor de saudação. Agora, a próxima etapa é muito[configurar sua telemetria toosend de páginas da web no navegador da web de saudação][usage].

Como alternativa, se o cliente for um aplicativo em um [telefone ou outro dispositivo][platforms], você poderá enviar telemetria por meio dele. 

Use Olá mesmo tooset de chave de instrumentação a telemetria de cliente e servidor. dados saudação aparecerá em Olá mesmo recurso Application Insights, e você será capaz de toocorrelate eventos do cliente e servidor.


## <a name="disabling-telemetry"></a>Desabilitando a telemetria
**Como desabilitar a coleta da telemetria?**

No código:

```Java

    TelemetryConfiguration config = TelemetryConfiguration.getActive();
    config.setTrackingIsDisabled(true);
```

**Ou** 

Atualize ApplicationInsights.xml (na pasta de recursos de saudação em seu projeto). Adicione a seguinte Olá sob o nó raiz de saudação:

```XML

    <DisableTelemetry>true</DisableTelemetry>
```

Usando o método XML hello, você tem toorestart aplicativo de hello quando você altera o valor de saudação.

## <a name="changing-hello-target"></a>Alterando o destino de saudação
**Como alterar o recurso do Azure ao qual meu projeto envia dados?**

* [Obter a chave de instrumentação de saudação do novo recurso de saudação.][java]
* Se você adicionou o projeto do Application Insights tooyour usando Olá Kit de ferramentas do Azure para Eclipse, clique com botão direito seu projeto da web, selecione **Azure**, **configurar o Application Insights**e alterar a chave de saudação.
* Caso contrário, atualize a chave de saudação na ApplicationInsights.xml na pasta de recursos de saudação em seu projeto.

## <a name="debug-data-from-hello-sdk"></a>Dados de saudação SDK de depuração

**Como posso descobrir qual Olá SDK está fazendo?**

tooget obter mais informações sobre o que está acontecendo em Olá API, adicione `<SDKLogger/>` sob o nó de raiz Olá Olá ApplicationInsights.xml do arquivo de configuração.

Você também pode instruir o arquivo do hello agente toooutput tooa:

```XML

    <SDKLogger type="FILE">
      <enabled>True</enabled>
      <UniquePrefix>JavaSDKLog</UniquePrefix>
    </SDKLogger>
```

Olá arquivos podem ser encontrados em `%temp%\javasdklogs` ou `java.io.tmpdir` no caso do servidor Tomcat.


## <a name="hello-azure-start-screen"></a>tela de início do Azure Hello
**Estou olhando [Olá portal do Azure](https://portal.azure.com). Mapa Olá conte-me algo sobre meu aplicativo?**

Não, ele mostra a integridade de saudação dos servidores do Azure ao redor Olá, mundo.

*Da placa de início do Azure hello (tela inicial), como localizar dados sobre meu aplicativo?*

Supondo que você [configurar seu aplicativo para o Application Insights][java], clique em Procurar, selecione Application Insights e selecione o recurso de aplicativo hello criado para seu aplicativo. tooget há mais rápido no futuro, você pode fixar sua placa de início do aplicativo toohello.

## <a name="intranet-servers"></a>Servidores de intranet
**Posso monitorar um servidor em minha intranet?**

Sim, desde que o servidor pode enviar o portal do Application Insights telemetria toohello por meio de Olá internet pública. 

Em seu firewall, você pode ter tooopen as portas TCP 80 e 443 para toodc.services.visualstudio.com de tráfego de saída e f5.services.visualstudio.com.

## <a name="data-retention"></a>Retenção de dados
**Quanto tempo os dados são retidos no portal de Olá? É seguro?**

Consulte [Privacidade e retenção de dados][data].

## <a name="next-steps"></a>Próximas etapas
**Configurei o Application Insights para meu aplicativo de servidor Java. O que mais posso fazer?**

* [Monitorar a disponibilidade de suas páginas da Web][availability]
* [Monitorar o uso da página da Web][usage]
* [Acompanhar o uso e diagnosticar problemas em seus aplicativos de dispositivos][platforms]
* [Gravar o uso de tootrack de código do aplicativo][track]
* [Capturar logs de diagnóstico][javalogs]

## <a name="get-help"></a>Obter ajuda
* [Stack Overflow](http://stackoverflow.com/questions/tagged/ms-application-insights)

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[data]: app-insights-data-retention-privacy.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[platforms]: app-insights-platforms.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md

