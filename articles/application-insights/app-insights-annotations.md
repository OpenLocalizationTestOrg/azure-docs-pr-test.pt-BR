---
title: "aaaRelease anotações para o Application Insights | Microsoft Docs"
description: "Adicionar implantação ou compilação marcadores de gráficos de explorer tooyour métricas no Application Insights."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 23173e33-d4f2-4528-a730-913a8fd5f02e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: bwren
ms.openlocfilehash: e802d22701cb69e96fd1a6b469ea67454195f77a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="annotations-on-metric-charts-in-application-insights"></a>Anotações sobre gráficos de métricas no Application Insights
As anotações de versão nos gráficos do [Metrics Explorer](app-insights-metrics-explorer.md) mostram onde você implantou uma nova compilação ou outro evento relevante. Elas facilitam toosee fácil se suas alterações tinham efeito no desempenho do aplicativo. Eles podem ser criados automaticamente pelo Olá [sistema de compilação do Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs). Você também pode criar anotações tooflag qualquer evento que você deseja por [criá-las do PowerShell](#create-annotations-from-powershell).

![Exemplo de anotações com correlação visível com tempo de resposta do servidor](./media/app-insights-annotations/00.png)



## <a name="release-annotations-with-vsts-build"></a>Anotações de versão com a compilação VSTS

Anotações de versão são um recurso de compilação de baseado em nuvem hello e versão de serviço do Visual Studio Team Services. 

### <a name="install-hello-annotations-extension-one-time"></a>Instalar a extensão de anotações da saudação (uma vez)
toobe toocreate capaz de versão anotações, você precisará tooinstall um de saudação muitas extensões de serviços de equipe disponíveis no hello Visual Studio Marketplace.

1. Entrar tooyour [do Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online) projeto.
2. No Visual Studio Marketplace, [obter Olá versão anotações extensão](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations)e adicione-a conta de Team Services tooyour.

![Na parte superior direita da página da Web do Team Services, abra o Marketplace. Selecione Visual Team Services e, em Compilação e Versão, escolha Ver mais.](./media/app-insights-annotations/10.png)

Você só precisa toodo desta vez para a sua conta do Visual Studio Team Services. As anotações de versão agora podem ser configuradas para qualquer projeto na sua conta. 

### <a name="configure-release-annotations"></a>Criar anotações de versão

Você precisa de chave de tooget uma API diferente para cada modelo de versão do VSTS.

1. Entrar toohello [Portal do Microsoft Azure](https://portal.azure.com) e abrir o recurso do Application Insights Olá que monitora o seu aplicativo. (Ou [crie um agora](app-insights-overview.md), se você ainda não fez isso.)
2. Abra **Acesso à API**, **ID do Application Insights**.
   
    ![Em portal.azure.com, abra o recurso do Application Insights e escolha Configurações. Abra Acesso à API. Copiar Olá ID do aplicativo](./media/app-insights-annotations/20.png)

4. Em uma janela separada do navegador, abra (ou crie) em modelo de liberação de saudação que gerencia as implantações do Visual Studio Team Services. 
   
    Adicionar uma tarefa e selecione a tarefa de anotação de versão do aplicativo Insights de Olá menu hello.
   
    Saudação de colar **Id do aplicativo** que você copiou da saudação folha de acesso à API.
   
    ![No Visual Studio Team Services, abra Versão, selecione uma definição de versão e escolha Editar. Clique em Adicionar Tarefa e selecione Anotação de Versão do Application Insights. Cole Olá identificação de informações do aplicativo.](./media/app-insights-annotations/30.png)
4. Saudação de conjunto **APIKey** variável do campo tooa `$(ApiKey)`.

5. Na Olá janela do Azure, crie uma nova chave de API e faça uma cópia dele.
   
    ![No hello folha de acesso à API no hello janela do Azure, clique em criar chave de API. Forneça um comentário, marque Gravar anotações e clique em Gerar a Chave. Copie a nova chave de saudação.](./media/app-insights-annotations/40.png)

6. Abra o guia de configuração de saudação do modelo de versão de saudação.
   
    Crie uma definição de variável para `ApiKey`.
   
    Cole seu toohello de chave de API ApiKey definição da variável.
   
    ![Na janela do Team Services hello, selecione a guia de configuração de saudação e clique em Adicionar variável. Defina Olá nome tooApiKey e no valor do hello, cole chave Olá que acabou de ser gerado e clique ícone de cadeado hello.](./media/app-insights-annotations/50.png)
7. Por fim, **salvar** Olá definição de versão.


## <a name="view-annotations"></a>Exibir anotações
Agora, sempre que usar Olá versão modelo toodeploy uma nova versão, uma anotação será enviada tooApplication Insights. anotações de saudação serão exibido nos gráficos do Metrics Explorer.

Clique no qualquer anotação marcador tooopen detalhes sobre a versão de hello, incluindo o solicitante, branch de controle de origem, definição de versão, ambiente e muito mais.

![Clique em qualquer marcador de anotação de versão.](./media/app-insights-annotations/60.png)

## <a name="create-custom-annotations-from-powershell"></a>Criar anotações personalizadas no PowerShell
Você também pode criar anotações de qualquer processo que desejar (sem usar o VS Team System). 


1. Faça uma cópia local do hello [script do Powershell do GitHub](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1).

2. Obter Olá ID do aplicativo e criar uma chave de API de saudação folha de acesso à API.

3. Chame o script hello como este:

```PS

     .\CreateReleaseAnnotation.ps1 `
      -applicationId "<applicationId>" `
      -apiKey "<apiKey>" `
      -releaseName "<myReleaseName>" `
      -releaseProperties @{
          "ReleaseDescription"="a description";
          "TriggerBy"="My Name" }
```

É fácil toomodify script de hello, por exemplo toocreate anotações para Olá anterior.

## <a name="next-steps"></a>Próximas etapas

* [Criar um item de trabalho](app-insights-diagnostic-search.md#create-work-item)
* [Automação com o PowerShell](app-insights-powershell.md)
