---
title: "Visão geral detalhada de planos de aaaAzure do serviço de aplicativo | Microsoft Docs"
description: "Saiba como os planos do Serviço de Aplicativo para o Serviço de Aplicativo do Azure funcionam e como eles beneficiam sua experiência de gerenciamento."
keywords: "serviço de aplicativo, serviço de aplicativo do azure, escala, escalonável, plano de serviço de aplicativo, custo de serviço de aplicativo"
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: dea3f41e-cf35-481b-a6bc-33d7fc9d01b1
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: byvinyal
ms.openlocfilehash: b384790d9e69b234ca69ac591164c48a4b6ed210
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-plans-in-depth-overview"></a>Visão geral detalhada de planos de serviço de aplicativo do Azure

Planos de serviço de aplicativo representam a coleção de saudação de recursos físicos usados toohost seus aplicativos.

Os Planos do Serviço de Aplicativo definem:

- Região (Oeste dos EUA, Leste dos EUA, etc.)
- Contagem da escala (uma, duas, três instâncias, etc.)
- Tamanha da instância (Pequena, Média, Grande)
- SKU (Gratuito, Compartilhado, Básico, Standard, Premium)

Aplicativos Web, Aplicativos Móveis, Aplicativos de API, Aplicativos de Funções (ou Funções) no [Serviço de Aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) todos executados em um plano do Serviço de Aplicativo.  Aplicativos em Olá mesma assinatura e região podem compartilhar um plano de serviço de aplicativo. 

Todos os aplicativos atribuídos tooan **plano de serviço de aplicativo** compartilham recursos Olá definidos por ela. Esse compartilhamento economiza dinheiro ao hospedar vários aplicativos em um único plano do Serviço de Aplicativo.

O **plano de serviço de aplicativo** pode ser dimensionada de **livre** e **compartilhado** SKUs muito**básica**, **padrão**, e **Premium** SKUs dando a você acessam os recursos de toomore e recursos ao longo de saudação maneira.

Se seu plano de serviço de aplicativo está definido muito**básica** SKU ou superior, em seguida, você pode controlar Olá **tamanho** e dimensionar a contagem de saudação VMs.

Por exemplo, se seu plano é configurado toouse duas instâncias de "pequeno" na camada de serviço standard Olá, todos os aplicativos que estão associados esse plano é executado em ambas as instâncias. Os aplicativos também têm características do nível de serviço padrão do acesso toohello. Instâncias do plano nas quais aplicativos estão em execução são totalmente gerenciadas e altamente disponíveis.

> [!IMPORTANT]
> Olá **SKU** e **escala** de saudação do serviço de aplicativo plano determina o número de custo e não hello de saudação de aplicativos hospedados nele.

Este artigo explora Olá principais características, como camada e escala de um plano de serviço de aplicativo e como eles entram em ação ao gerenciar seus aplicativos.

## <a name="apps-and-app-service-plans"></a>Aplicativos e planos do Serviço de Aplicativo

Um aplicativo no Serviço de Aplicativo pode ser associado a apenas um plano de Serviço de Aplicativo de cada vez.

Os aplicativos e os planos estão contidos em **grupo de recursos**. Um grupo de recursos serve como o limite de ciclo de vida de Olá para cada recurso que está dentro dele. Você pode usar toomanage de grupos de recursos todas as partes de saudação de um aplicativo.

Como um único grupo de recursos pode ter vários planos de serviço de aplicativo, você pode alocar aplicativos diferentes recursos físicos toodifferent.

Por exemplo, você pode dividir os recursos entre ambientes de desenvolvimento, teste e produção. Ter ambientes separados para desenvolvimento/teste e produção permite isolar recursos. Dessa forma, em relação a uma nova versão de seus aplicativos de teste de carga não compete para Olá mesmo recursos como seus aplicativos de produção, o que estão atendendo clientes reais.

Quando você tem vários planos em um único grupo de recursos, também pode definir um aplicativo que abrange várias regiões geográficas.

Por exemplo, um aplicativo altamente disponível executando em duas regiões incluirá pelo menos dois planos, um para cada região e um aplicativo associado com cada plano. Em tal situação, todas as cópias de saudação do aplicativo hello, em seguida, estão contidas em um único grupo de recursos. Ter um grupo de recursos com vários planos e vários aplicativos torna fácil toomanage, controle e exibir a integridade de saudação do aplicativo hello.

## <a name="create-an-app-service-plan-or-use-existing-one"></a>Criar um Plano do Serviço de Aplicativo ou usar um existente

Ao criar um aplicativo, você deverá considerar a criação de um grupo de recursos. Em Olá outro lado, se este aplicativo é um componente para um aplicativo maior, criá-lo no grupo de recursos de saudação que é alocado para o aplicativo maior.

Se o aplicativo hello é um aplicativo totalmente novo ou parte de uma maior, você pode escolher toouse um toohost plano existente-lo ou criar um novo. Essa decisão é mais uma questão de capacidade e carga esperada.

É recomendável isolar seu aplicativo em um novo Plano do Serviço de Aplicativo quando:

- O aplicativo faz uso intensivo de recursos.
- Aplicativo tem diferente fatores de dimensionamento de saudação outros aplicativos hospedados em um plano existente.
- O aplicativo precisa de recursos em uma região geográfica diferente.

Dessa forma, você pode alocar um novo conjunto de recursos para seu aplicativo e ter mais controle sobre seus aplicativos.

## <a name="create-an-app-service-plan"></a>Criar um plano de Serviço de Aplicativo

> [!TIP]
> Se você tiver um ambiente de serviço de aplicativo, você pode examinar Olá documentação específica tooApp ambientes de serviço aqui: [criar um plano de serviço de aplicativo em um ambiente de serviço de aplicativo](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)

Você pode criar um plano de serviço de aplicativo vazio de saudação experiência de navegação do plano de serviço de aplicativo ou como parte da criação do aplicativo.

Em Olá [portal do Azure](https://portal.azure.com), clique em **novo** > **Web + móvel**e, em seguida, selecione **aplicativo Web** ou outro tipo de aplicativo de serviço de aplicativo.

![Crie um aplicativo em Olá portal do Azure.][createWebApp]

Em seguida, você pode selecionar ou criar hello plano de serviço de aplicativo para o novo aplicativo de saudação.

 ![Crie um plano do Serviço de Aplicativo.][createASP]

toocreate um plano de serviço de aplicativo, clique em **[+] criar novos**, Olá tipo **plano de serviço de aplicativo** nome e, em seguida, selecione adequados **local**. Clique em **preço**e, em seguida, selecione uma camada de preços apropriada para o serviço de saudação. Selecione **exibir todos os** tooview preços mais opções, como **livre** e **compartilhado**. Depois que você selecionou Olá preço, clique em Olá **selecione** botão.

## <a name="move-an-app-tooa-different-app-service-plan"></a>Mover um plano de serviço de aplicativo diferente do aplicativo tooa

Você pode mover um plano de serviço de aplicativo diferente do aplicativo tooa Olá [portal do Azure](https://portal.azure.com). Você pode mover aplicativos entre planos como planos de saudação estão no hello mesmo grupo de recursos e a região geográfica.

toomove um plano de tooanother do aplicativo:

- Navegue toohello aplicativo que você deseja toomove.
- Em Olá **Menu**, procure Olá **plano do serviço de aplicativo** seção.
- Selecione **plano de serviço de aplicativo de alteração** toostart processo de saudação.

**Plano de serviço de aplicativo de alteração** abre Olá **plano de serviço de aplicativo** seletor. Neste ponto, você pode escolher um toomove plano existente este aplicativo em.

> [!IMPORTANT]
> plano de serviço de aplicativo Hello select da interface do usuário é filtrado por Olá critérios a seguir:
> - Encontra Olá mesmo grupo de recursos
> - Existe no hello mesma região geográfica
> - Encontra Olá mesmo espaço na Web
>
> Um espaço Web é uma construção lógica dentro do Serviço de Aplicativo que define um agrupamento de recursos do servidor. Uma região geográfica (por exemplo, oeste dos EUA) contém muitos espaços na Web em clientes de tooallocate ordem usando o serviço de aplicativo. Atualmente, recursos de serviço de aplicativo não capaz de toobe movido entre espaços na Web.
>

![Seletor de plano do Serviço de Aplicativo.][change]

Cada plano tem seu próprio tipo de preço. Por exemplo, a movimentação de um site de uma camada de padrão de tooa camada gratuita, permite que todos os aplicativos atribuídos tooit toouse Olá recursos e da camada de saudação padrão.

## <a name="clone-an-app-tooa-different-app-service-plan"></a>Clonar um plano de serviço de aplicativo diferente do aplicativo tooa

Se você quiser toomove Olá aplicativo tooa uma região diferente, uma alternativa é aplicativo clonagem. A clonagem faz uma cópia do seu aplicativo em um novo plano do Serviço de Aplicativo existente em qualquer região.

Você pode encontrar **aplicativo Clone** em Olá **ferramentas de desenvolvimento** seção do menu hello.

> [!IMPORTANT]
> A clonagem tem algumas limitações que você pode ler a respeito em [Clonagem de aplicativo do Serviço de Aplicativo do Azure usando o portal do Azure](../app-service-web/app-service-web-app-cloning-portal.md).

## <a name="scale-an-app-service-plan"></a>Dimensionar um plano de Serviço de Aplicativo

Há três tooscale de maneiras de um plano:

- **Alterar plano de saudação do preço**. Um plano na camada básica Olá pode ser convertido tooStandard e todos os aplicativos atribuídos tooit toouse recursos de saudação da camada de saudação padrão.
- **Alterar o tamanho da instância do plano Olá**. Por exemplo, um plano na camada básica de saudação que usa pequenas instâncias pode ser alterado toouse grandes instâncias. Todos os aplicativos que estão associados esse plano agora podem usar memória adicional hello e recursos da CPU que Olá oferece maior de tamanho de instância.
- **Alterar a contagem de instâncias do plano Olá**. Por exemplo, um plano padrão que é expandido toothree instâncias pode ser dimensionado too10 instâncias. Um plano Premium pode ser expandido too20 instâncias (assunto tooavailability). Todos os aplicativos que estão associados esse plano agora podem usar memória adicional hello e recursos da CPU que Olá oferece maior de contagem de instância.

Você pode alterar Olá tamanho de instância e de camada de preços clicando Olá **aumentar** item em configurações para o aplicativo hello ou Olá plano de serviço de aplicativo. As alterações aplicam toohello plano de serviço de aplicativo e afetam todos os aplicativos que ele hospeda.

 ![Tooscale de valores do conjunto de backup de um aplicativo.][pricingtier]

## <a name="app-service-plan-cleanup"></a>Limpeza do Plano do Serviço de Aplicativo

> [!IMPORTANT]
> **Planos de serviço de aplicativo** com nenhuma toothem aplicativos associados ainda incorrendo em encargos, pois eles continuam a capacidade de computação tooreserve hello.

tooavoid inesperados encargos, quando o aplicativo do último Olá hospedado em um plano de serviço de aplicativo for excluído, Olá vazio resultante plano de serviço de aplicativo também será excluído.

## <a name="summary"></a>Resumo

Os planos de Serviço de Aplicativo representam um conjunto de recursos e capacidades que pode ser compartilhado entre seus aplicativos. Planos de serviço de aplicativo dê Olá conjunto de tooa do flexibilidade tooallocate aplicativos específicos de recursos e otimizar ainda mais a utilização de recursos do Azure. Dessa forma, se você quiser toosave dinheiro em seu ambiente de teste, você pode compartilhar um plano entre vários aplicativos. Você também pode maximizar a produtividade para seu ambiente de produção dimensionando-o em várias regiões e planos.

## <a name="whats-changed"></a>O que mudou

- Uma alteração de toohello do guia de sites tooApp serviço, consulte: [do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)

[pricingtier]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/appserviceplan-pricingtier.png
[assign]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/assing-appserviceplan.png
[change]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/change-appserviceplan.png
[createASP]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-appserviceplan.png
[createWebApp]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-web-app.png
