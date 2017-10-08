---
title: aaaCreate um novo recurso do Application Insights do Azure | Microsoft Docs
description: Configure manualmente o monitoramento do Application Insights para um novo aplicativo em tempo real.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 878b007e-161c-4e36-8ab2-3d7047d8a92d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: bwren
ms.openlocfilehash: 3aba7045e1f8fe43d473f0be01dd52106ab992a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-insights-resource"></a>Criar um recurso do Application Insights
O Azure Application Insights exibe dados sobre o seu aplicativo em um *recurso* do Microsoft Azure. Criando um novo recurso, portanto, é parte de [Configurando um novo aplicativo Application Insights toomonitor][start]. Em muitos casos, criar um recurso pode ser feito automaticamente pelo Olá IDE. Mas em alguns casos, você cria um recurso manualmente - por exemplo, toohave de recursos separado para desenvolvimento e produção compilações do seu aplicativo.

Depois que você criou o recurso hello, você obter sua chave de instrumentação e usa esse Olá tooconfigure SDK no aplicativo hello. links de chave de recurso Olá Olá recursos de toohello de telemetria.

## <a name="sign-up-toomicrosoft-azure"></a>Inscreva-se tooMicrosoft do Azure
Se você ainda não tiver uma [conta da Microsoft, obtenha uma agora mesmo](http://live.com). (Se usar serviços como Outlook.com, OneDrive, Windows Phone ou XBox Live, você já tem uma conta da Microsoft.)

Você também precisa de uma assinatura muito[Microsoft Azure](http://azure.com). Se sua equipe ou organização tiver uma assinatura do Azure, Olá proprietário pode adicionar você tooit, usando seu Windows Live ID. Você será cobrado apenas pelo que usa. plano básico do saudação padrão permite que uma determinada quantidade de uso experimental gratuita.

Quando você tem acesso tooa assinatura, faça logon no Insights tooApplication em [http://portal.azure.com](https://portal.azure.com)e usar toologin seu Live ID.

## <a name="create-an-application-insights-resource"></a>Criar um recurso do Application Insights
Em Olá [portal.azure.com](https://portal.azure.com), adicionar um recurso do Application Insights:

![Clique em Novo, Application Insights](./media/app-insights-create-new-resource/01-new.png)

* **Tipo de aplicativo** afeta o que você vê na folha de visão geral de saudação e as propriedades de saudação disponíveis no [explorer métrica][metrics]. Se você não vir seu tipo de aplicativo, selecione Geral.
* **Assinatura** é a sua conta de pagamento no Azure.
* **Grupo de recursos** é uma conveniência para o gerenciamento de propriedades, como controle de acesso. Se você já criou outros recursos do Azure, você pode escolher tooput este novo recurso Olá mesmo grupo.
* **Local** é onde podemos manter seus dados.
* **PIN toodashboard** coloca um bloco de acesso rápido para o recurso em sua Home page do Azure. Recomendável.

Quando seu aplicativo tiver sido criado, uma nova folha será aberta. Essa folha mostra os dados de uso e de desempenho do seu aplicativo. 

tooit back tooget próxima vez que você fizer logon no tooAzure, procure o bloco de início rápido do aplicativo em Olá iniciar placa (tela inicial). Ou clique em Procurar toofind-lo.

## <a name="copy-hello-instrumentation-key"></a>Copie a chave de instrumentação Olá
chave de instrumentação Olá identifica o recurso de saudação que você criou. Necessário toogive toohello SDK.

![Clique em Essentials, Olá chave de instrumentação, CTRL + C](./media/app-insights-create-new-resource/02-props.png)

## <a name="install-hello-sdk-in-your-app"></a>Instalar Olá SDK em seu aplicativo
Instale SDK do Application Insights de saudação em seu aplicativo. Esta etapa depende muito do tipo de saudação do seu aplicativo. 

Use Olá instrumentação chave tooconfigure [Olá SDK que você instala em seu aplicativo][start].

Olá SDK inclui módulos padrão que enviar telemetria sem a necessidade de toowrite qualquer código. ações do usuário tootrack ou diagnosticar problemas em mais detalhes, [usar Olá API] [ api] toosend sua telemetria.

## <a name="monitor"></a>Consultar os dados de telemetria
Fechar Olá rápido iniciar folha de aplicativos folha tooreturn tooyour Olá portal do Azure.

Clique em Olá pesquisa bloco toosee [pesquisa diagnóstico][diagnostic], onde os eventos primeiro Olá aparecem. 

Se você estiver esperando mais dados, clique em **Atualizar** depois de alguns segundos.

## <a name="creating-a-resource-automatically"></a>Criando um recurso automaticamente
Você pode escrever um [script do PowerShell](app-insights-powershell.md) toocreate um recurso automaticamente.

## <a name="next-steps"></a>Próximas etapas
* [Criar um painel](app-insights-dashboards.md)
* [Pesquisa de Diagnóstico](app-insights-diagnostic-search.md)
* [Explorar métricas](app-insights-metrics-explorer.md)
* [Escrever consultas do Analytics](app-insights-analytics.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[diagnostic]: app-insights-diagnostic-search.md
[metrics]: app-insights-metrics-explorer.md
[start]: app-insights-overview.md

