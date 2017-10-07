---
title: "aaaHow toodeploy um serviço Web regiões toomultiple | Microsoft Docs"
description: "Etapas toodeploy (cópia) regiões de tooother um novo serviço da Web."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: cgronlun
ms.assetid: 36c60411-f2db-4ee2-9b66-b1f1d77a8f44
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 21fcdb96f118c60ed98b60b1b2df833766c7c8bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-web-service-toomultiple-regions"></a>Como um serviço Web de toodeploy toomultiple regiões
Olá serviços Web do Azure nova permitem tooeasily implantar um regiões de toomultiple de serviço web sem a necessidade de várias assinaturas ou espaços de trabalho. 

Os preços são região específica, que portanto, você deve definir um plano de cobrança para cada região na qual você implantará o serviço web de saudação.

## <a name="toocreate-a-plan-in-another-region"></a>toocreate um plano em outra região
1. Entre nos [serviços Web de Microsoft Azure Machine Learning](https://services.azureml.net/).
2. Clique em Olá **planos** opção de menu.
3. Em planos de saudação pela página de exibição, clique em **novo**.
4. De saudação **assinatura** suspenso, assinatura Olá selecione em quais Olá novo plano residirá.
5. De saudação **região** lista suspensa, selecione uma região para um novo plano de saudação. Olá opções do plano para a região selecionada hello serão exibidos no hello **opções do plano de** seção da página de saudação.
6. De saudação **grupo de recursos** lista suspensa, selecione um recurso de grupo para o plano de saudação. Em mais informações sobre grupos de recursos, confira [Visão geral do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).
7. Em **nome do plano de** nome de saudação do tipo de plano de hello.
8. Em **opções do plano de**, clique no nível de cobrança Olá para o novo plano de saudação.
9. Clique em **Criar**.

## <a name="deploying-hello-web-service-tooanother-region"></a>Implantação de região de tooanother Olá web service
1. Clique em Olá **serviços Web** opção de menu.
2. Selecione Olá serviço Web que você está implantando tooa nova região.
3. Clique em **Copiar**.
4. Em **nome do serviço Web**, digite um novo nome para o serviço web de saudação.
5. Em **Web descrição do serviço**, digite uma descrição para o serviço web de saudação.
6. De saudação **assinatura** suspenso, assinatura Olá selecione em quais Olá novo serviço da web residirá.
7. De saudação **grupo de recursos** lista suspensa, selecione um recurso de grupo do serviço web de saudação. Em mais informações sobre grupos de recursos, confira [Visão geral do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).
8. De saudação **região** suspenso, região Olá selecione quais toodeploy Olá no serviço na web.
9. De saudação **conta de armazenamento** lista suspensa, selecione uma conta de armazenamento no qual Olá toostore de serviço da web.
10. De saudação **plano de preço** lista suspensa, selecione um plano na região de saudação selecionado na etapa 8.
11. Clique em **Copiar**.

