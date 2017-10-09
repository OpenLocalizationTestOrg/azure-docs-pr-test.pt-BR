---
title: aaaSolution direcionamento no OMS | Microsoft Docs
description: "Direcionamento de solução é um recurso no OMS Operations Management Suite () que permite que você toolimit gerenciamento soluções tooa conjunto específico de agentes.  Este artigo descreve como toocreate uma configuração de escopo e aplicá-lo tooa solução."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1f054a4e-6243-4a66-a62a-0031adb750d8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2017
ms.author: bwren
ms.openlocfilehash: 6f8c8109e0d9e282e18724bf8b673b10de8e498a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-solution-targeting-in-operations-management-suite-oms-tooscope-management-solutions-toospecific-agents-preview"></a>Usar solução direcionamento no OMS Operations Management Suite () em agentes de toospecific de soluções de gerenciamento de tooscope (visualização)
Quando você adiciona uma solução tooOMS, ele será automaticamente implantado por tooall Windows e Linux agentes conectados tooyour análise de Log espaço de trabalho padrão.  Talvez você queira toomanage sua quantidade Olá custos e limite de dados coletada para uma solução limitando-tooa determinado conjunto de agentes.  Este artigo descreve como toouse **solução direcionamento** que é um recurso do OMS que permite que você tooapply um escopo tooyour soluções.

## <a name="how-tootarget-a-solution"></a>Como uma solução de tootarget
Há três tootargeting de etapas uma solução conforme descrito nas seções a seguir de saudação.  Observe que você precisará portal do OMS hello e Olá portal do Azure para etapas diferentes.


### <a name="1-create-a-computer-group"></a>1. Criar um grupo de computadores
Especificar computadores Olá que você deseja tooinclude em um escopo criando um [grupo de computadores](../log-analytics/log-analytics-computer-groups.md) na análise de Log.  grupo de computadores Olá pode ser com base em uma pesquisa de log ou importado de outras fontes, como o Active Directory ou grupos do WSUS. Como [descrito abaixo](#solutions-and-agents-that-cant-be-targeted), somente os computadores que estão diretamente conectados tooLog análise será incluída no escopo de saudação.

Depois que você tiver criado no seu espaço de trabalho de grupo de computadores hello, você deverá incluí-lo em uma configuração de escopo pode ser aplicada tooone ou mais soluções.
 
 
 ### <a name="2-create-a-scope-configuration"></a>2. Criar uma configuração de escopo
 Um **configuração de escopo** inclui um ou mais grupos de computadores e podem ser aplicada tooone ou mais soluções. 
 
 Crie uma configuração de escopo usando Olá processo a seguir.  

 1. Olá portal do Azure no, navegue muito**análise de Log** e selecione seu espaço de trabalho.
 2. Nas propriedades de saudação de espaço de trabalho de saudação em **fontes de dados de espaço de trabalho** selecione **configurações de escopo**.
 3. Clique em **adicionar** toocreate uma nova configuração de escopo.
 4. Digite um **nome** para a configuração de escopo de saudação.
 5. Clique em **Selecionar Grupos de Computadores**.
 6. Selecione o grupo de computadores de saudação que você criou e, opcionalmente, quaisquer outros grupos tooadd toohello configuração.  Clique em **Selecionar**.  
 6. Clique em **Okey** toocreate configuração de escopo de saudação. 


 ### <a name="3-apply-hello-scope-configuration-tooa-solution"></a>3. Aplica a solução de tooa de configuração de escopo de saudação.
Depois que você tiver uma configuração de escopo, em seguida, você pode aplicar tooone ou mais soluções.  Observe que, embora uma única configuração de escopo possa ser usada com várias soluções, cada solução só poderá usar uma configuração de escopo.

Aplica uma configuração de escopo usando Olá processo a seguir.  

 1. Olá portal do Azure no, navegue muito**análise de Log** e selecione seu espaço de trabalho.
 2. Nas propriedades de saudação do espaço de trabalho Olá selecione **soluções**.
 3. Clique na solução de saudação desejado tooscope.
 4. Nas propriedades de saudação para solução de saudação em **fontes de dados de espaço de trabalho** selecione **solução direcionamento**.  Se a opção de saudação não está disponível, em seguida, [essa solução não pode ser direcionada](#solutions-and-agents-that-cant-be-targeted).
 5. Clique em **Adicionar configuração de escopo**.  Se você já tiver uma solução de toothis configuração aplicada essa opção estará indisponível.  Você deve remover a configuração existente Olá antes de adicionar outro.
 6. Clique em configuração de escopo de saudação que você criou.
 7. Saudação de inspeção **Status** de saudação configuração tooensure que mostra **êxito**.  Se o status de saudação indica um erro, clique em Olá reticências à direita da toohello da configuração hello e selecione **Editar configuração de escopo** toomake alterações.

## <a name="solutions-and-agents-that-cant-be-targeted"></a>Soluções e agentes que não podem ser direcionados
A seguir é os critérios de saudação para agentes e soluções que não podem ser usadas com o direcionamento de solução.

- Direcionamento de solução só se aplica toosolutions que implantar tooagents.
- Direcionamento de solução se aplica somente toosolutions fornecido pela Microsoft.  Ele não se aplica a toosolutions [criado por você mesmo ou parceiros](operations-management-suite-solutions-creating.md).
- Você só pode filtrar agentes que se conectam diretamente tooLog análise.  Soluções implantará automaticamente os agentes tooany que fazem parte de um grupo de gerenciamento do Operations Manager conectado se eles estão incluídos em uma configuração de escopo.

### <a name="exceptions"></a>Exceções
Direcionamento de solução não pode ser usado com hello soluções a seguir, embora elas se ajustarem Olá mencionado critérios.

- Avaliação de Integridade do Agente

## <a name="next-steps"></a>Próximas etapas
- Saiba mais sobre as soluções de gerenciamento, incluindo soluções Olá tooinstall disponível em seu ambiente no [espaço de trabalho tooyour soluções de gerenciamento de análise de logs do Azure adicionar](../log-analytics/log-analytics-add-solutions.md).
- Saiba mais sobre como criar grupos de computadores em [Grupos de computadores em pesquisas de logs do Log Analytics](../log-analytics/log-analytics-computer-groups.md).