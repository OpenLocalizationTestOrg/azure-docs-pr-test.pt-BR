---
title: "aaaDeploying um novo serviço da web no aprendizado de máquina do Azure | Microsoft Docs"
description: "serviço web baseado em fluxo de trabalho de saudação de implantação de um BRAÇO"
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: a358b04f-0d08-4d50-820e-eeac971854cf
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: v-donglo
ROBOTS: NOINDEX
redirect_url: machine-learning-publish-a-machine-learning-web-service
redirect_document_id: True
ms.openlocfilehash: 2cbfda44b97a6b992fbdfdfb0c761e6c9e169035
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-new-web-service"></a>Implantar um novo serviço Web
Agora de aprendizado de máquina do Microsoft Azure fornece serviços web baseados em [do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) permitindo novas opções de plano de cobrança e implantar as regiões de toomultiple do serviço web.

Olá fluxo de trabalho geral toodeploy um serviço web usando serviços Web de aprendizado de máquina do Microsoft Azure é:

* Criar um teste preditivo
* implantá-lo
* configurar seu nome
* Plano de Faturamento
* testá-lo
* consumi-lo.

Olá gráfico a seguir ilustra o fluxo de trabalho de saudação.

![Fluxo de trabalho de implantação de serviço Web][1]

## <a name="deploy-web-service-from-studio"></a>Implantar serviço Web do Studio
toodeploy uma experiência como um novo serviço web. Entrar no estúdio de aprendizado de máquina do hello e criar um novo serviço web de previsão. 

**Observação**: se você já implantou um teste como um serviço Web clássico, não poderá implantá-lo como um novo serviço Web.

Clique em **executar** final Olá Olá experimentar tela e, em seguida, clique em **implantar o serviço da Web** e **implantar o serviço de Web [novo]**. página de implantação de saudação do Gerenciador de serviço de Web de aprendizado de máquina Olá será aberto.

## <a name="machine-learning-web-service-manager-deploy-experiment-page"></a>Página de teste de implantação do Gerente de Serviços Web de Machine Learning
Na página de teste implantar hello, insira um nome para o serviço web de saudação.
Selecione um plano de preços. Se você tiver um plano de preços existente, que você poderá selecioná-lo, caso contrário, você deve criar um novo plano de preço para o serviço de saudação. 

1. Em Olá **plano de preço** lista suspensa, selecione um plano existente ou selecione Olá **selecione novo plano** opção.
2. Em **nome do plano de**, digite um nome que identifique Olá plano na sua conta.
3. Selecione uma saudação **níveis mensal planejar**. Observe que as camadas de plano de saudação padrão toohello planos para a sua região padrão e o serviço web é implantado toothat região.

Clique em **implantar** e Olá página de início rápido para o serviço web é aberta.

## <a name="quickstart-page"></a>Página Início Rápido
página de início rápido de serviço Olá web fornece acesso e orientação em tarefas mais comuns hello, que você irá executar depois de criar um novo serviço web. A partir daqui, você pode acessar facilmente os dois Olá **teste** página e **consumir** página.

## <a name="testing-your-web-service"></a>Testando seu serviço Web
Na página de início rápido de saudação, clique em Testar serviço web em tarefas comuns.   

serviço web tootest hello como um serviço de solicitação-resposta (RR):

* Clique em **teste** na barra de menus do hello.
* Clique em **Solicitação-Resposta**.
* Insira os valores apropriados para colunas de entrada hello de sua experiência.
* Clique em **Solicitação-Resposta**.

Resultados serão exibido no lado direito Olá da página de saudação.

tootest um serviço de web do serviço de execução de lote (BES), você usará um arquivo CSV:

* Clique em **teste** na barra de menus do hello.
* Clique em **Lote**.
* Em sua entrada, clique em Procurar e navegue tooyour arquivo de dados de exemplo.
* Clique em **Testar**.

status de saudação do teste é exibido em **testar trabalhos de lote**.

## <a name="consuming-your-web-service"></a>Consumindo seu serviço Web
Quando implantado como um serviço Web, os testes de Azure Machine Learning fornecem uma API REST que pode ser consumida por uma ampla variedade de dispositivos e plataformas. Isso ocorre porque as mensagens formatadas em Olá API REST simples aceita e responde com JSON. Olá, portal de aprendizado de máquina do Azure fornece código que pode ser usado toocall Olá web Services em R, c# e Python.

Na página de consomem hello, você encontrará:

* Olá API de chave e URI para o consumo de serviço da web em aplicativos.
* Tookick de modelos de aplicativo web e Excel iniciar o processo de consumo.
* Código de exemplo em c#, python e R tooget iniciado.

Para obter mais informações sobre o consumo de serviços web, consulte [como tooconsume um serviço Web de aprendizado de máquina do Azure](machine-learning-consume-web-services.md).

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre o consumo dos serviços Web, consulte:

[Como tooconsume um serviço Web de aprendizado de máquina do Azure](machine-learning-consume-web-services.md)

[Serviços Web do Azure Machine Learning: implantação e consumo](machine-learning-deploy-consume-web-service-guide.md)

<!--Image references-->
[1]: ./media/machine-learning-webservice-deploy-a-web-service/armdeploymentworkflow.png


<!--links-->
