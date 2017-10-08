---
title: aaaUse toodeploy portal do Azure recursos do Azure | Microsoft Docs
description: Use o portal do Azure e gerenciamento de recursos do Azure toodeploy seus recursos.
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 2c98a4aa-8d9f-4a0a-b764-214dbe8ed009
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: 5a5217f94c8dfc0c1ebd613903ea3dcbe1197bfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-portal"></a>Implantar recursos com modelos do Resource Manager e o portal do Azure
> [!div class="op_single_selector"]
> * [PowerShell](resource-group-template-deploy.md)
> * [CLI do Azure](resource-group-template-deploy-cli.md)
> * [Portal](resource-group-template-deploy-portal.md)
> * [API REST](resource-group-template-deploy-rest.md)
> 
> 

Este tópico mostra como Olá toouse [portal do Azure](https://portal.azure.com) com [do Azure Resource Manager](resource-group-overview.md) toodeploy seus recursos do Azure. toolearn sobre como gerenciar seus recursos, consulte [recursos de gerenciamento Azure por meio do portal](resource-group-portal.md).

Atualmente, não cada serviço suporta Olá portal ou o Gerenciador de recursos. Para esses serviços, você precisa Olá toouse [portal clássico](https://manage.windowsazure.com). Para obter o status de saudação de cada serviço, consulte [gráfico de disponibilidade do portal do Azure](https://azure.microsoft.com/features/azure-portal/availability/).

## <a name="create-resource-group"></a>Criar grupo de recursos
1. toocreate um grupo de recurso vazio, selecione **novo** > **gerenciamento** > **grupo de recursos**.
   
    ![criar grupo de recursos vazio](./media/resource-group-template-deploy-portal/create-empty-group.png)
2. Dê a ele um nome e uma localização e, se necessário, selecione uma assinatura. É necessário tooprovide um local para o grupo de recursos Olá porque o grupo de recursos de saudação armazena metadados sobre os recursos de saudação. Por motivos de conformidade, talvez você queira toospecify onde os metadados são armazenados. Em geral, é recomendável que você especifique um local em que a maioria de seus recursos residirá. Usando Olá mesmo local pode simplificar seu modelo.
   
    ![definir valores de grupo](./media/resource-group-template-deploy-portal/set-group-properties.png)

## <a name="deploy-resources-from-marketplace"></a>Implantar recursos do Marketplace
Depois de criar um grupo de recursos, você pode implantar recursos tooit de saudação Marketplace. Olá Marketplace fornece soluções predefinidas para cenários comuns.

1. toostart uma implantação, selecione **novo** e o tipo de saudação do recurso que deseja toodeploy. Em seguida, procure versão específica de saudação do recurso Olá você gostaria que toodeploy.
   
    ![implantar recurso](./media/resource-group-template-deploy-portal/deploy-resource.png)
2. Se você não vir a solução em particular Olá você gostaria que toodeploy, você pode pesquisar Olá Marketplace para ele.
   
    ![pesquisar no Marketplace](./media/resource-group-template-deploy-portal/search-resource.png)
3. Dependendo do tipo de saudação do recurso selecionado, você tem uma coleção de propriedades relevantes tooset antes da implantação. Essas opções não são mostradas aqui, pois elas variam com base no tipo de recurso. Para todos os tipos, você deve selecionar um grupo de recursos de destino. imagem a seguir Olá mostra como toocreate um aplicativo web e implantá-lo toohello grupo de recursos que você criou.
   
    ![Criar grupo de recursos](./media/resource-group-template-deploy-portal/select-existing-group.png)
   
    Como alternativa, você pode decidir toocreate um grupo de recursos ao implantar seus recursos. Selecione **criar novo** e dê um nome de grupo de recursos de saudação.
   
    ![criar novo grupo de recursos](./media/resource-group-template-deploy-portal/select-new-group.png)
4. Sua implantação será iniciada. implantação de saudação pode levar alguns minutos. Quando Olá implantação for concluída, você verá uma notificação.
   
    ![exibir notificação](./media/resource-group-template-deploy-portal/view-notification.png)
5. Depois de implantar seus recursos, você pode adicionar mais grupo de recursos toohello de recursos usando Olá **adicionar** comando folha de grupo de recursos de saudação.
   
    ![adicionar recurso](./media/resource-group-template-deploy-portal/add-resource.png)

## <a name="deploy-resources-from-custom-template"></a>Implantar recursos de um modelo personalizado
Se você quiser tooexecute uma implantação, mas não usa qualquer um dos modelos de saudação em Olá Marketplace, você pode criar um modelo personalizado que define a infraestrutura de saudação para sua solução. toolearn sobre a criação de modelos, consulte [modelos de autoria do Azure Resource Manager](resource-group-authoring-templates.md).

1. toodeploy um modelo personalizado por meio do portal hello, selecione **novo**e iniciar a pesquisa **implantação de modelo** até que você pode selecionar opções de saudação.
   
    ![procurar implantação de modelo](./media/resource-group-template-deploy-portal/search-template.png)
2. Selecione **implantação de modelo** de recursos disponíveis do hello.
   
    ![selecionar implantação de modelo](./media/resource-group-template-deploy-portal/select-template.png)
3. Depois de iniciar a implantação de modelo Olá, abra o modelo em branco Olá disponível para personalizar.
   
    ![criar modelo](./media/resource-group-template-deploy-portal/show-custom-template.png)
   
    No editor de hello, adicione a sintaxe JSON Olá que define os recursos de saudação deseja toodeploy. Selecione **Salvar** quando terminar. Para obter orientação sobre como escrever a sintaxe JSON hello, consulte [passo a passo do Gerenciador de recursos modelo](resource-manager-template-walkthrough.md).
   
    ![editar modelo](./media/resource-group-template-deploy-portal/edit-template.png)
4. Ou, você pode selecionar um modelo pré-existente de saudação [modelos de início rápido do Azure](https://azure.microsoft.com/documentation/templates/). Esses modelos são contribuídos pela comunidade de saudação. Abrangem vários cenários comuns e alguém pode ter adicionado um modelo semelhante toowhat que você está tentando toodeploy. Você pode pesquisar Olá modelos toofind algo que corresponde ao seu cenário.
   
    ![selecionar modelo de início rápido](./media/resource-group-template-deploy-portal/select-quickstart-template.png)
   
    Você pode exibir o modelo selecionado Olá no editor de saudação.
5. Depois de fornecer Olá todos os outros valores, selecione **criar** toodeploy modelo de saudação. 
   
    ![implantar modelo](./media/resource-group-template-deploy-portal/create-custom-deploy.png)

## <a name="deploy-resources-from-a-template-saved-tooyour-account"></a>Implantar recursos de um modelo salvo tooyour conta
Olá portal permite que você toosave tooyour um modelo conta do Azure e reimplantá-lo mais tarde. Para obter mais informações sobre como trabalhar com esses salvo modelos, [começar com modelos privados no portal do Azure de saudação](../marketplace-consumer/mytemplates-getstarted.md).

1. Selecione de seus modelos salvos, toofind **procurar** > **modelos**.
   
    ![procurar modelos](./media/resource-group-template-deploy-portal/browse-templates.png)
2. Na lista de saudação de modelos salvos tooyour conta, selecione Olá aquele que você deseja toowork em.
   
    ![modelos salvos](./media/resource-group-template-deploy-portal/saved-templates.png)
3. Selecione **implantar** tooredeploy Isso salva o modelo.
   
    ![implantar modelo salvo](./media/resource-group-template-deploy-portal/deploy-saved-template.png)

## <a name="next-steps"></a>Próximas etapas
* Consulte os logs de auditoria tooview [operações com o Gerenciador de recursos de auditoria](resource-group-audit.md).
* tootroubleshoot erros de implantação, consulte [Exibir operações de implantação](resource-manager-deployment-operations.md).
* tooretrieve um modelo de uma implantação ou o grupo de recursos, consulte [exportar do Azure Resource Manager modelo de recursos existentes](resource-manager-export-template.md).
* Para obter diretrizes sobre como as empresas podem usar o Gerenciador de recursos tooeffectively gerenciar assinaturas, consulte [scaffold enterprise do Azure - controle de assinatura prescritivas](resource-manager-subscription-governance.md).

