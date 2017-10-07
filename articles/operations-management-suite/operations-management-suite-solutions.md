---
title: aaaSolutions no OMS Operations Management Suite () | Microsoft Docs
description: "Soluções de estendem a funcionalidade de saudação do Operations Management Suite (OMS), fornecendo os cenários de pacotes de gerenciamento que os clientes podem adicionar tootheir espaço de trabalho do OMS.  Este artigo fornece detalhes sobre soluções personalizadas criadas por clientes e parceiros."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 1f054a4e-6243-4a66-a62a-0031adb750d8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/01/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5b5a538f1bc4b5577bec94db08bd43668bc6584a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-management-solutions-in-operations-management-suite-oms-preview"></a>Trabalhando com soluções de gerenciamento no OMS (Operations Management Suite) (Versão prévia)
> [!NOTE]
> Esta é uma documentação preliminar para soluções de gerenciamento no OMS, que estão atualmente em visualização.    
> 
> 

Soluções de gerenciamento de estendem a funcionalidade de saudação do Operations Management Suite (OMS), fornecendo os cenários de pacotes de gerenciamento que os clientes podem adicionar tootheir ambiente.  Além disso muito[soluções fornecidas pela Microsoft](../log-analytics/log-analytics-add-solutions.md), parceiros e clientes podem criar toobe de soluções de gerenciamento usados em seu próprio ambiente ou feita toocustomers disponíveis por meio da comunidade de saudação.

## <a name="finding-and-installing-management-solutions"></a>Localizando e instalando soluções de gerenciamento
Há vários métodos para localizar e instalar as soluções de gerenciamento, conforme descrito em Olá seções a seguir.

### <a name="azure-marketplace"></a>Azure Marketplace
Soluções de gerenciamento fornecido pela Microsoft e parceiros confiáveis podem ser instalados do hello Azure Marketplace em Olá portal do Azure.

1. Faça logon em toohello portal do Azure.
2. No painel esquerdo do hello, selecione **mais serviços**.
3. O Role para baixo demais**soluções** ou tipo *soluções* em Olá **filtro** caixa de diálogo.
4. Clique em Olá **+ adicionar** botão.
5. Procurar soluções que você está interessado no navegando, clicando em Olá **filtro** botão ou digitando Olá **Everthing pesquisa** caixa.
6. Clique em um tooview de item do marketplace as informações detalhadas.
7. Clique em **criar** tooopen Olá **adicionar solução** painel.
8. Será solicitada toorequired informações como Olá [OMS espaço de trabalho e a conta de automação](#oms-workspace-and-automation-account) além toovalues para todos os parâmetros Olá solução.
9. Clique em **criar** tooinstall solução de saudação.

### <a name="oms-portal"></a>Portal do OMS
Soluções de gerenciamento fornecidas pela Microsoft podem ser instaladas do hello Galeria de soluções no portal do OMS hello.

1. Faça logon em toohello portal do OMS.
2. Clique em Olá **Galeria de soluções** lado a lado.
3. Na página de galeria de soluções do OMS hello, saiba mais sobre cada solução disponível. Clique Olá nome de solução de saudação que você deseja tooadd tooOMS.
4. Na página de saudação de solução de saudação que você escolheu, informações detalhadas sobre solução de saudação são exibidas. Clique em **Adicionar**.
5. Um novo bloco para solução de saudação que você adicionou aparece na Olá página Visão geral do OMS e você pode começar a usá-lo depois que o serviço OMS Olá processa seus dados.

### <a name="azure-quickstart-templates"></a>Modelos de início rápido do Azure
Membros da comunidade Olá podem enviar tooAzure soluções de gerenciamento modelos de início rápido.  Você pode baixar esses modelos para instalação posterior ou inspecioná-los toolearn como muito[criar suas próprias soluções](#creating-a-solution).

1. Siga o processo Olá descrito em [OMS espaço de trabalho e a conta de automação](#oms-workspace-and-automation-account) toolink um espaço de trabalho e a conta.
2. Vá muito[modelos de início rápido do Azure](https://azure.microsoft.com/documentation/templates/).  
3. Pesquise uma solução na qual você esteja interessado.
4. Selecione solução Olá Olá resultados tooview seus detalhes.
5. Clique em Olá **implantar tooAzure** botão.
6. Você será tooprovide solicitadas informações como o grupo de recursos de saudação e o local na adição toovalues para todos os parâmetros na solução de saudação.
7. Clique em **compra** tooinstall solução de saudação.

### <a name="deploy-azure-resource-manager-template"></a>Implantar o modelo do Azure Resource Manager
As soluções que você obteve de comunidade hello, ou que você [criar por conta própria](#creating-a-solution) são implementados como um modelo do Gerenciador de recursos, e você pode usar qualquer um dos métodos de saudação padrão para [implantar um modelo de](../azure-resource-manager/resource-group-template-deploy-portal.md).  Observe que, antes de instalar a solução hello, você deve criar e vincular Olá [OMS espaço de trabalho e a conta de automação](#oms-workspace-and-automation-account).

## <a name="oms-workspace-and-automation-account"></a>Espaço de trabalho do OMS e Conta de automação
A maioria das soluções de gerenciamento exigem um [espaço de trabalho do OMS](../log-analytics/log-analytics-manage-access.md) toocontain modos de exibição e um [conta de automação](../automation/automation-security-overview.md#automation-account-overview) toocontain runbooks e recursos relacionados. Olá espaço de trabalho e conta deve atender a saudação requisitos a seguir.

* Uma solução só pode usar um espaço de trabalho do OMS e uma conta de automação.  
* Olá espaço de trabalho do OMS e usado por uma solução de conta de automação devem ser vinculado tooone outro. Um espaço de trabalho do OMS só pode ser vinculado tooone conta de automação e uma conta de automação só pode ser vinculado tooone espaço de trabalho do OMS.
* toobe vinculado, Olá espaço de trabalho do OMS e Olá de automação de conta deve estar no mesmo grupo de recursos e região.  exceção de saudação é um espaço de trabalho do OMS na região Leste dos EUA e e a conta de automação no Leste dos EUA 2.

### <a name="creating-a-link-between-an-oms-workspace-and-automation-account"></a>Criar um vínculo entre um espaço de trabalho do OMS e a conta de automação
Como especificar o espaço de trabalho OMS hello e conta de automação depende do método de instalação Olá para sua solução.

* Quando você instala uma solução da Microsoft por meio do portal do OMS hello, ele é instalado no espaço de trabalho Olá de atual do OMS e nenhuma conta de automação é necessária.
* Quando você instala uma solução por meio de saudação do Azure Marketplace, você será solicitado para um espaço de trabalho do OMS e a conta de automação e link Olá entre eles é criado para você.  
* Para soluções fora hello Azure Marketplace, você deve vincular o espaço de trabalho OMS hello e conta de automação antes de instalar a solução de saudação.  Você pode fazer isso selecionando qualquer solução no hello Azure Marketplace e selecionando o espaço de trabalho OMS hello e conta de automação.  Você não tem tooactually instalar solução Olá porque Olá link será criado como o espaço de trabalho do hello OMS e a conta de automação estão selecionadas.  Depois de criar o link hello, em seguida, você pode usar esse espaço de trabalho do OMS e a conta de automação para qualquer solução. 

### <a name="verifying-hello-link-between-an-oms-workspace-and-automation-account"></a>Verificando link de saudação entre um espaço de trabalho do OMS e a conta de automação
Você pode verificar Olá link entre um espaço de trabalho do OMS e uma conta de automação usando Olá procedimento a seguir.

1. Selecione a conta de automação de saudação em Olá portal do Azure.
2. Rolar para o fim da saudação toohello **configurações** painel.
3. Se houver uma seção chamada **recursos do OMS** em Olá **configurações** painel e, em seguida, essa conta é anexado tooan espaço de trabalho do OMS.
4. Selecione **espaço de trabalho** tooview detalhes de saudação do espaço de trabalho do OMS Olá vinculado toothis conta de automação.

## <a name="listing-management-solutions"></a>Listando as soluções de gerenciamento
Use Olá seguindo o procedimento tootooview Olá soluções de gerenciamento Olá de espaços de trabalho vinculado tooyour assinatura do Azure.

1. Faça logon em toohello portal do Azure.
2. No painel esquerdo do hello, selecione **mais serviços**.
3. O Role para baixo demais**soluções** ou tipo *soluções* em Olá **filtro** caixa de diálogo.
4. Soluções instaladas em todos os seus espaços de trabalho serão listadas.

Observe que você pode exibir apenas soluções de Microsoft hello instaladas no espaço de trabalho atual hello usando o portal do OMS hello.

## <a name="removing-a-management-solution"></a>Removendo uma solução de gerenciamento
Quando uma solução de gerenciamento é removida, todos os recursos de solução de saudação também serão removidos.  

1. Localizar solução Olá no hello Azure portal usando o procedimento Olá [listando soluções](#listing-solutions).
2. Selecione a solução de saudação deseja tooremove.
3. Clique em Olá **excluir** botão.

## <a name="creating-a-management-solution"></a>Criando uma solução de gerenciamento
Diretrizes completas sobre como criar soluções de gerenciamento estão disponíveis em [Criando soluções no OMS (Operations Management Suite)](operations-management-suite-solutions-creating.md). 

## <a name="next-steps"></a>Próximas etapas
* Pesquise entre os [Modelos de Início Rápido do Azure](https://azure.microsoft.com/documentation/templates) para obter exemplos de diferentes modelos do Resource Manager.
* Crie suas próprias [soluções de gerenciamento](operations-management-suite-solutions-creating.md).

