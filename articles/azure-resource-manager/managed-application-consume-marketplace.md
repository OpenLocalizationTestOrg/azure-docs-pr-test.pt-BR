---
title: aaaConsume o aplicativo gerenciado no marketplace do Azure | Microsoft Docs
description: "Describeshow toocreate um aplicativo gerenciado do Azure que está disponível por meio de saudação Marketplace."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/11/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 9ae6e11a3f63eb58a9f3199364b5606a7afe5618
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="consume-azure-managed-applications-in-hello-marketplace"></a>Consumir Azure aplicativos em Olá Marketplace gerenciados

Conforme discutido em Olá [visão geral de aplicativos gerenciados](managed-application-overview.md) artigo, há dois cenários Olá final tooend experiência. Um é publicador hello ou fornecedor que deseja toocreate um aplicativo gerenciado para uso por clientes. Olá segundo é cliente do final de saudação ou consumidor de saudação do aplicativo hello gerenciado. Este artigo aborda o segundo cenário de saudação. Descreve como você pode implantar um aplicativo gerenciado de saudação do Microsoft Azure Marketplace.

## <a name="create-from-hello-marketplace"></a>Criar a partir de saudação Marketplace

Implantar um aplicativo gerenciado de saudação Marketplace é semelhante toodeploying qualquer tipo de recursos de saudação Marketplace. 

No portal de saudação, selecione **+ novo** e pesquisa para o tipo de saudação do toodeploy da solução. Selecione opções disponíveis de Olá, Olá um que é necessário.

![pesquisar soluções](./media/managed-application-consume-marketplace/search-apps.png)

Examine o resumo de saudação do aplicativo hello e selecione **criar**.

![criar aplicativo gerenciado](./media/managed-application-consume-marketplace/create-marketplace-managed-app.png)

Como qualquer outra solução, você verá campos tooprovide valores para. Esses campos variam por tipo de saudação do aplicativo gerenciado que você criar. 

## <a name="view-support-information"></a>Exibir informações de suporte

Após ter implantado seu aplicativo gerenciado, exiba informações de suporte de saudação para o aplicativo hello. Na folha de aplicativo gerenciado hello, informações de suporte de saudação são listadas.

![suporte](./media/managed-application-consume-marketplace/support.png)

## <a name="view-publisher-permissions"></a>Exibir permissões de publicador

fornecedor Olá que gerencia seu aplicativo é concedido acesso tooyour recursos. toosee essas permissões, selecione **autorizações**.

![autorizações](./media/managed-application-consume-marketplace/authorizations.png)

## <a name="next-steps"></a>Próximas etapas

* Para obter informações sobre como publicar um aplicativo gerenciado no hello Marketplace, consulte [aplicativos gerenciados do Azure no Marketplace](managed-application-author-marketplace.md).
* toopublish aplicativos gerenciados que são somente toousers disponíveis em sua organização, consulte [criar e publicar o aplicativo gerenciado do catálogo do serviço](managed-application-publishing.md).
* tooconsume aplicativos gerenciados que são somente toousers disponíveis em sua organização, consulte [consumir um aplicativo gerenciado do serviço de catálogo](managed-application-consumption.md).
