---
title: "toocreate aaaUse 2.0 do CLI um aplicativo do AD do Azure e configurá-lo tooaccess API de serviços de mídia do Azure | Microsoft Docs"
description: "Este tópico mostra como toouse 2.0 do CLI toocreate um aplicativo do AD do Azure e configurá-lo tooaccess API de serviços de mídia do Azure."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: c865e2701722374b5dd17b0e20fa848c07065006
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-20-toocreate-an-aad-app-and-configure-it-tooaccess-azure-media-services-api"></a>Use 2.0 do CLI toocreate um aplicativo AAD e configurá-lo tooaccess API de serviços de mídia do Azure

Este tópico mostra como toouse 2.0 do CLI toocreate um aplicativo do Azure Active Directory (AD do Azure) e tooaccess principal do serviço do Azure Media Services recursos. 

## <a name="prerequisites"></a>Pré-requisitos

- Uma conta do Azure. Para obter detalhes, confira [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/). 
- Uma conta dos Serviços de Mídia. Para obter mais informações, consulte [criar uma conta de serviços de mídia do Azure usando o portal do Azure de saudação](media-services-portal-create-account.md).

## <a name="use-hello-azure-cloud-shell"></a>Saudação de usar o Shell de nuvem do Azure

1. Entrar toohello [portal do Azure](https://portal.azure.com/).
2. Inicie Olá nuvem Shell Olá superior no painel de navegação do portal de saudação.

    ![Cloud Shell](./media/media-services-cli-create-and-configure-aad-app/media-services-cli-create-and-configure-aad-app01.png) 

Para obter mais informações, consulte [Visão geral do Azure Cloud Shell](../cloud-shell/overview.md).

## <a name="create-an-azure-ad-app-and-configure-access-toohello-media-account-with-cli-20"></a>Criar um aplicativo do AD do Azure e configurar a conta do media toohello acesso com 2.0 do CLI
 
```azurecli
az login
az ad sp create-for-rbac --name <appName> --password <strong password>
az role assignment create -- assignee < user/app id> --role Contributor --scope <subscription/subscription id>
```

Por exemplo:

```azurecli
az role assignment create --assignee a3e068fa-f739-44e5-ba4d-ad57866e25a1 --role Contributor --scope /subscriptions/0b65e280-7917-4874-9fed-1307f2615ea2/resourceGroups/Default-AzureBatch-SouthCentralUS/providers/microsoft.media/mediaservices/sbbash
```

Neste exemplo, Olá **escopo** é o caminho do recurso completo de saudação para mídia Olá conta dos serviços. No entanto, Olá **escopo** pode estar em qualquer nível.

Por exemplo, pode ser uma saudação níveis a seguir:
 
* Olá **assinatura** nível.
* Olá **grupo de recursos** nível.
* Olá **recurso** nível (por exemplo, uma conta de mídia).

Para obter mais informações, consulte [Criar uma entidade de serviço do Azure com a CLI 2.0 do Azure](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli)

Consulte também [Manage Role-Based o controle de acesso com hello Azure interface de linha de comando](../active-directory/role-based-access-control-manage-access-azure-cli.md). 

## <a name="next-steps"></a>Próximas etapas

Introdução ao [carregando arquivos tooyour conta](media-services-portal-upload-files.md).
