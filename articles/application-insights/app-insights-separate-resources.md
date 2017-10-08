---
title: "Telemetria aaaSeparating de desenvolvimento, teste e de versão no Azure Application Insights | Microsoft Docs"
description: "Telemetria direto toodifferent recursos carimbos de desenvolvimento, teste e produção."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 578e30f0-31ed-4f39-baa8-01b4c2f310c9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: a294c8c70f46d7c29b460461c3494c83e13a0cbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="separating-telemetry-from-development-test-and-production"></a>Separação da telemetria de desenvolvimento, teste e produção

Quando você estiver desenvolvendo a próxima versão Olá de um aplicativo web, você não deseja toomix backup Olá [Application Insights](app-insights-overview.md) Telemetria da versão nova hello e Olá já foi liberado. tooavoid confusão, enviar telemetria de saudação do desenvolvimento diferentes fases tooseparate recursos do Application Insights, com chaves de instrumentação separado (ikeys). toomake-lo mais fácil toochange Olá instrumentação chave como uma versão é movida de um estágio tooanother, pode ser útil tooset Olá ikey no código, em vez de no arquivo de configuração de saudação. 

(Se o sistema for um Serviço de Nuvem do Azure, haverá [outro método de configuração de ikeys separados](app-insights-cloudservices.md).)

## <a name="about-resources-and-instrumentation-keys"></a>Sobre recursos e chaves de instrumentação

Ao configurar o monitoramento do Application Insights para seu aplicativo Web, você cria um *recurso* do Application Insights no Microsoft Azure. Abrir este recurso no hello portal do Azure em ordem toosee e analisar a telemetria Olá coletada do seu aplicativo. Olá recurso é identificado por um *chave de instrumentação* (ikey). Quando você instala o hello Application Insights pacote toomonitor seu aplicativo, você configurá-lo com a chave de instrumentação hello, para que ele saiba onde toosend Olá telemetria.

Normalmente, você escolher recursos separados toouse ou um único recurso compartilhado em cenários diferentes:

* Aplicativos independentes e diferentes – use um recurso separado e a ikey para cada aplicativo.
* Vários componentes ou funções de aplicativo de negócios - Use um [único recurso compartilhado](app-insights-monitor-multi-role-apps.md) para todos os aplicativos de componente de hello. Telemetria pode ser filtrada ou segmentada por propriedade de cloud_RoleName hello.
* Desenvolvimento, teste e liberação - usam um recurso separado e ikey para versões do sistema de saudação em 'carimbo' ou a fase de produção.
* Teste A | B – use um único recurso. Crie um tooadd TelemetryInitializer telemetria de toohello uma propriedade que identifica as variantes de saudação.


## <a name="dynamic-ikey"></a> Chave de instrumentação dinâmica

toomake mais fácil toochange Olá ikey como código Olá move entre estágios de produção, configurá-lo no código em vez de no arquivo de configuração de saudação.

Chave de saudação definida em um método de inicialização, como global.aspx.cs em um serviço ASP.NET:

*C#*

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey = 
          // - for example -
          WebConfigurationManager.AppSettings["ikey"];
      ...

Neste exemplo, Olá ikeys para recursos diferentes Olá são colocadas em diferentes versões do arquivo de configuração de web hello. Trocando arquivo de configuração de web de saudação - que pode ser feito como parte do script de liberação Olá - alternará o recurso de destino hello.

### <a name="web-pages"></a>Páginas da Web
Olá iKey também é usado em páginas da web do seu aplicativo, no hello [script que você obteve na folha de início rápido de saudação](app-insights-javascript.md). Em vez de codificá-lo literalmente em script hello, gerá-lo do estado do servidor de saudação. Por exemplo, em um aplicativo ASP.NET:

*JavaScript no Razor*

    <script type="text/javascript">
    // Standard Application Insights web page script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      "@Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="create-additional-application-insights-resources"></a>Criar recursos adicionais do Application Insights
Telemetria tooseparate para componentes de aplicativo diferente ou para carimbos diferentes (desenvolvimento/teste/produção) de saudação mesmo componente, em seguida, você terá toocreate um novo recurso do Application Insights.

Em Olá [portal.azure.com](https://portal.azure.com), adicionar um recurso do Application Insights:

![Clique em Novo, Application Insights](./media/app-insights-separate-resources/01-new.png)

* **Tipo de aplicativo** afeta o que você vê na folha de visão geral de saudação e as propriedades de saudação disponíveis no [explorer métrica](app-insights-metrics-explorer.md). Se você não vir o tipo de aplicativo, escolha um dos tipos de web de saudação para páginas da web.
* **grupo de recursos** é uma conveniência para o gerenciamento de propriedades, como [controle de acesso](app-insights-resources-roles-access-control.md)do Microsoft Azure. Você pode usar grupos de recursos separados para desenvolvimento, teste e produção.
* **Assinatura** é a sua conta de pagamento no Azure.
* **Local** é onde podemos manter seus dados. Atualmente ele não pode ser alterado. 
* **Adicionar toodashboard** coloca um bloco de acesso rápido para o recurso em sua Home page do Azure. 

Criando recurso Olá leva alguns segundos. Quando estiver pronto, você verá um alerta.

(Você pode escrever um [script do PowerShell](app-insights-powershell-script-create-resource.md) toocreate um recurso automaticamente.)

### <a name="getting-hello-instrumentation-key"></a>Obtendo chave de instrumentação Olá
chave de instrumentação Olá identifica o recurso de saudação que você criou. 

![Clique em Essentials, Olá chave de instrumentação, CTRL + C](./media/app-insights-separate-resources/02-props.png)

É necessário chaves de instrumentação de saudação de todos os toowhich de recursos de saudação seu aplicativo irá enviar dados.

## <a name="filter-on-build-number"></a>Filtrar por número de compilação
Quando você publica uma nova versão do seu aplicativo, você desejará telemetria de saudação toobe tooseparate capaz de compilações diferentes.

Você pode definir a propriedade de versão do aplicativo hello para que você pode filtrar [pesquisa](app-insights-diagnostic-search.md) e [explorer métrica](app-insights-metrics-explorer.md) resultados.

![Filtragem em uma propriedade](./media/app-insights-separate-resources/050-filter.png)

Há vários métodos diferentes de configuração de propriedade de versão do aplicativo hello.

* Definir diretamente:

    `telemetryClient.Context.Component.Version = typeof(MyProject.MyClass).Assembly.GetName().Version;`
* Quebrar a linha em uma [inicializador de telemetria](app-insights-api-custom-events-metrics.md#defaults) tooensure todas as instâncias de TelemetryClient são configuradas de forma consistente.
* [ASP.NET] Versão do conjunto de saudação em `BuildInfo.config`. módulo de web Hello escolherá versão de saudação do nó de BuildLabel hello. Incluir esse arquivo em seu projeto e lembre-se de tooset Olá copiar sempre propriedade no Gerenciador de soluções.

    ```XML

    <?xml version="1.0" encoding="utf-8"?>
    <DeploymentEvent xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/VisualStudio/DeploymentEvent/2013/06">
      <ProjectName>AppVersionExpt</ProjectName>
      <Build type="MSBuild">
        <MSBuild>
          <BuildLabel kind="label">1.0.0.2</BuildLabel>
        </MSBuild>
      </Build>
    </DeploymentEvent>

    ```
* [ASP.NET] Gerar automaticamente BuildInfo.config no MSBuild. toodo isso, adicione alguns tooyour de linhas `.csproj` arquivo:

    ```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
    ```

    Isso gera um arquivo chamado *yourProjectName*. Olá BuildInfo.config. o processo de publicação renomeia tooBuildInfo.config.

    rótulo de compilação Olá contém um espaço reservado (autogen _...) quando compilado com o Visual Studio. Mas quando compilado com o MSBuild, ele será preenchido com o número correto da versão de saudação.

    como o conjunto Olá versão tooallow números de versão do MSBuild toogenerate, `1.0.*` em AssemblyReference.cs

## <a name="version-and-release-tracking"></a>Versão e controle de versão
versão do aplicativo hello tootrack, certifique-se de `buildinfo.config` é gerado pelo seu processo Microsoft Build Engine. No arquivo. csproj, adicione:  

```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
```

Quando ele tem informações de compilação hello, módulo de web do Application Insights Olá adiciona automaticamente **versão do aplicativo** como tooevery uma propriedade de telemetria. Que permite que você toofilter versão quando você executar [pesquisas diagnósticas](app-insights-diagnostic-search.md), ou quando você [explorar métricas](app-insights-metrics-explorer.md).

No entanto, observe que o número de versão de compilação Olá é gerado apenas por Olá Microsoft Build Engine, não pelo desenvolvedor de saudação de compilação no Visual Studio.

### <a name="release-annotations"></a>Anotações da versão
Se você usar o Visual Studio Team Services, você pode [obter um marcador de anotação](app-insights-annotations.md) adicionado tooyour gráficos sempre que uma nova versão. Olá a imagem a seguir mostra como esse marcador é exibido.

![Captura de tela de anotação de versão de exemplo em um gráfico](./media/app-insights-asp-net/release-annotation.png)
## <a name="next-steps"></a>Próximas etapas

* [Recursos compartilhados para várias funções](app-insights-monitor-multi-role-apps.md)
* [Criar um toodistinguish de inicializador de telemetria A | Variantes de B](app-insights-api-filtering-sampling.md#add-properties)
