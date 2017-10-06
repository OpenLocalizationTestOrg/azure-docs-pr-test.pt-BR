---
title: "aaaLogging para serviços web do aprendizado de máquina | Microsoft Docs"
description: "Saiba como serviços da web de registro em log tooenable para aprendizado de máquina. Registro em log informações adicionais toohelp Olá APIs de solução de problemas."
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: c54d41e1-0300-46ef-bbfc-d6f7dca85086
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/15/2017
ms.author: raymondl;garye
ms.openlocfilehash: ed23933d52d2151af658af2307d7df8743071f65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-logging-for-machine-learning-web-services"></a>Habilitar o log de serviços Web de Machine Learning
Este documento fornece informações sobre Olá log capacidade de serviços web do aprendizado de máquina. Registro em log informações adicionais, além de um número de erro e uma mensagem, que pode ajudá-lo a solucionar problemas de seu toohello chama APIs de aprendizado de máquina.  

## <a name="how-tooenable-logging-for-a-web-service"></a>Como o log tooenable para um serviço Web

Habilitar o registro de saudação [serviços de Web de aprendizado de máquina do Azure](https://services.azureml.net) portal. 

1. Entrar no portal de serviços de Web de aprendizado de máquina do Azure toohello em [https://services.azureml.net](https://services.azureml.net). Para um serviço web clássico, você também pode obter toohello portal clicando **nova experiência de serviços Web** na página de serviços de Web do aprendizado de máquina Olá no estúdio de aprendizado de máquina.

   ![Novo link de Experiência dos Serviços Web](media/machine-learning-web-services-logging/new-web-services-experience-link.png)

2. Na barra de menus superior hello, clique em **serviços Web** para um novo serviço da web, ou clique em **Web Services clássico** para um clássico de serviço web.

   ![Selecione serviços Web Novos ou Clássicos](media/machine-learning-web-services-logging/select-web-service.png)

3. Para um novo serviço da web, clique em nome do serviço web hello. Para um serviço web clássico, clique em nome do serviço web hello e clique em ponto de extremidade apropriado Olá na próxima página de saudação.

4. Na barra de menus superior hello, clique em **configurar**.

5. Saudação de conjunto **Habilitar log** opção muito*erro* (toolog somente erros) ou *todas as* (para registro em log completo).

   ![Selecionar o nível de log](media/machine-learning-web-services-logging/enable-logging.png)

6. Clique em **Salvar**.

7. Para serviços da web de clássico, criar hello **ml diagnóstico** contêiner.

   Todos os logs de serviço web são mantidos em um contêiner de blob denominado **ml diagnóstico** na conta de armazenamento Olá associada ao serviço web de saudação. Para novos serviços da web, esse contêiner é criado Olá primeira vez que você acessar o serviço web de saudação. Para serviços da web de clássico, você precisar de toocreate Olá contêiner se ele ainda não existir. 

   1. Em Olá [portal do Azure](https://portal.azure.com), vá toohello conta de armazenamento associada ao serviço da web de saudação.

   2. Em **Serviço Blob**, clique em **Contêineres**.

   3. Se contêiner Olá **ml diagnóstico** não existe, clique em **+ contêiner**, dê a saudação contêiner Olá nome "ml de diagnóstico" e selecione Olá **tipo de acesso** como "Blob". Clique em **OK**.

      ![Selecionar o nível de log](media/machine-learning-web-services-logging/create-ml-diagnostics-container.png)

> [!TIP]
>
> Para um serviço web clássico, Olá painel de serviços Web no estúdio de aprendizado de máquina também tem um registro em log do comutador tooenable. No entanto, como log agora é gerenciado por meio do portal de serviços Web hello, é necessário tooenable log por meio do portal Olá conforme descrito neste artigo. Se você tiver habilitado o log no Studio, em seguida, no Portal de serviços da Web de Olá, desabilite o log e habilitá-lo novamente.


## <a name="hello-effects-of-enabling-logging"></a>efeitos de saudação de habilitar o registro em log
Quando o log está habilitado, diagnóstico hello e erros de ponto de extremidade do serviço Olá web são registrados em Olá **ml diagnóstico** contêiner de blob em Olá conta de armazenamento do Azure vinculada ao espaço de trabalho do usuário hello. Este contêiner contém todas as informações de diagnóstico Olá para todos os pontos de serviço web Olá para todos os espaços de trabalho Olá associados a esta conta de armazenamento.

Olá logs podem ser exibidos usando qualquer um dos Olá várias ferramentas tooexplore disponível uma conta de armazenamento do Azure. Olá mais fácil pode ser toonavigate toohello conta de armazenamento Olá portal do Azure, clique em **contêineres**e, em seguida, clique em contêiner Olá **ml diagnóstico**.  

## <a name="log-blob-detail-information"></a>Informações detalhadas do log blob
Cada blob no contêiner de saudação contém informações de diagnóstico de saudação para exatamente um Olá ações a seguir:

* A execução do método hello execução em lotes  
* A execução do método hello solicitação-resposta  
* Inicialização de um contêiner de Request-Response

nome de saudação de cada blob tem um prefixo de saudação formulário a seguir: 


`{Workspace Id}-{Web service Id}-{Endpoint Id}/{Log type}`


Onde _tipo de Log_ é uma saudação valores a seguir:  

* lote  
* pontuação/solicitações  
* pontuação/init  

