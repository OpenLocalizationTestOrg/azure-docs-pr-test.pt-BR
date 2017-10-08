---
title: aaaUse toomanage portal do Azure recursos do Azure | Microsoft Docs
description: "Use o portal do Azure e gerenciamento de recursos do Azure toomanage seus recursos. Mostra como toowork com recursos de toomonitor painéis."
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 0725bbf2-5913-4c07-af6e-24e11d957fbc
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: 0c89a197a31c5b6dd03ba457cb4d1fdf9f6d00f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-resources-through-portal"></a>Gerenciar recursos do Azure por meio do portal
> [!div class="op_single_selector"]
> * [PowerShell do Azure](powershell-azure-resource-manager.md)
> * [CLI do Azure](xplat-cli-azure-resource-manager.md)
> * [Portal](resource-group-portal.md) 
> * [API REST](resource-manager-rest-api.md)
> 
> 

Este tópico mostra como Olá toouse [portal do Azure](https://portal.azure.com) com [do Azure Resource Manager](resource-group-overview.md) toomanage seus recursos do Azure. toolearn sobre a implantação de recursos por meio do portal hello, consulte [implantar recursos com modelos do Gerenciador de recursos e o portal do Azure](resource-group-template-deploy-portal.md).

Atualmente, não cada serviço suporta Olá portal ou o Gerenciador de recursos. Para esses serviços, você precisa Olá toouse [portal clássico](https://manage.windowsazure.com). Para obter o status de saudação de cada serviço, consulte [gráfico de disponibilidade do portal do Azure](https://azure.microsoft.com/features/azure-portal/availability/).

## <a name="manage-resource-groups"></a>Gerenciar grupos de recursos

Um grupo de recursos é um contêiner que mantém os recursos relacionados a uma solução do Azure. grupo de recursos de saudação pode incluir todos os recursos de saudação para solução hello, ou apenas os recursos que você deseja toomanage como um grupo. Decidir como deseja que os recursos de tooallocate tooresource grupos com base no que torna hello mais sentido para sua organização. Geralmente, adicionar recursos que compartilham Olá mesmo toohello de ciclo de vida mesmo recurso de grupo para que você pode facilmente implantar, atualizar e excluí-los como um grupo. 

grupo de recursos de saudação armazena metadados sobre os recursos de saudação. Portanto, quando você especificar um local para o grupo de recursos hello, você está especificando onde os metadados são armazenados. Por motivos de conformidade, talvez seja necessário tooensure que seus dados são armazenados em uma determinada região.

1. toosee todos os grupos de recursos de saudação em sua assinatura, selecione **grupos de recursos**.
   
    ![procurar grupos de recursos](./media/resource-group-portal/browse-groups.png)
2. toocreate um grupo de recurso vazio, selecione **adicionar**.
   
    ![adicionar grupo de recursos](./media/resource-group-portal/add-resource-group.png)
3. Forneça um nome e local para o novo grupo de recursos hello. Selecione **Criar**.
   
    ![Criar grupo de recursos](./media/resource-group-portal/create-empty-group.png)
4. Talvez seja necessário tooselect **atualizar** toosee grupo de recursos de saudação criado recentemente.
   
    ![atualizar grupo de recursos](./media/resource-group-portal/refresh-resource-groups.png)
5. toocustomize Olá informações exibidas para os grupos de recursos, selecione **colunas**.
   
    ![personalizar colunas](./media/resource-group-portal/select-columns.png)
6. Selecione Olá colunas tooadd e, em seguida, selecione **atualização**.
   
    ![adicionar colunas](./media/resource-group-portal/add-columns.png)
7. toolearn sobre como implantar recursos tooyour novo grupo de recursos, consulte [implantar recursos com modelos do Gerenciador de recursos e o portal do Azure](resource-group-template-deploy-portal.md).
8. Acesso rápido tooa grupo de recursos, você pode fixar o dashboard na tooyour Olá folha.
   
    ![fixar grupo de recursos](./media/resource-group-portal/pin-group.png)
9. painel Olá exibe o grupo de recursos de saudação e seus recursos. Você pode selecionar os grupos de recursos de saudação ou qualquer item de toohello de toonavigate seus recursos.
   
    ![fixar grupo de recursos](./media/resource-group-portal/show-resource-group-dashboard.png)

## <a name="tag-resources"></a>Recursos de marca
Você pode aplicar marcas tooresource grupos e recursos toologically organizar seus ativos. Para obter informações sobre como trabalhar com marcas, consulte [usando marcas tooorganize seus recursos do Azure](resource-group-using-tags.md).

[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]

## <a name="monitor-resources"></a>Monitorar recursos
Quando você seleciona um recurso, a folha de recursos Olá apresenta tabelas para o tipo de recurso de monitoramento e gráficos padrão.

1. Selecione um recurso e observe Olá **monitoramento** seção. Ele inclui gráficos que são relevantes toohello tipo de recurso. Olá imagem a seguir mostra dados de monitoramento de uma conta de armazenamento de padrão de saudação.
   
    ![mostrar o monitoramento](./media/resource-group-portal/show-monitoring.png)
2. Você pode fixar uma seção de saudação folha tooyour painel selecionando as reticências (...) do hello acima seção hello. Você também pode personalizar Olá tamanho Olá seção na folha de saudação ou removê-lo completamente. Hello imagem a seguir mostra como toopin, personalizar, ou remova a saudação da CPU e a seção de memória.
   
    ![fixar seção](./media/resource-group-portal/pin-cpu-section.png)
3. Depois de fixar o dashboard do hello seção toohello, você verá Olá resumo no painel de saudação. E, selecionando-o imediatamente leva toomore detalhes sobre dados saudação.
   
    ![exibir painel](./media/resource-group-portal/view-startboard.png)
4. toocompletely personalizar dados de saudação monitorar por meio do portal hello, navegar do painel de padrão de tooyour e selecione **novo painel**.
   
    ![painel Transações da Web](./media/resource-group-portal/dashboard.png)
5. Nomeie o novo painel e arrastar blocos no painel de saudação. Olá peças são filtradas pelo opções diferentes.
   
    ![painel Transações da Web](./media/resource-group-portal/create-dashboard.png)
   
     toolearn sobre como trabalhar com os painéis, consulte [criação e compartilhamento de painéis no portal do Azure de saudação](../azure-portal/azure-portal-dashboards.md).

## <a name="manage-resources"></a>Gerenciar recursos
Na folha de saudação para um recurso, você ver opções Olá para gerenciar recursos de saudação. portal de saudação apresenta opções de gerenciamento para o tipo de recurso específico. Você ver os comandos de gerenciamento de saudação na superior de saudação da folha de recursos hello e no lado esquerdo da saudação.

![Gerenciar recursos](./media/resource-group-portal/manage-resources.png)

Essas opções, você pode executar operações como iniciar e parar uma máquina virtual ou reconfigurar as propriedades de saudação da máquina virtual de saudação.

## <a name="move-resources"></a>Mover recursos
Se você precisar de grupo de recursos de tooanother toomove recursos ou outra assinatura, consulte [Mover grupo de recursos toonew de recursos ou assinatura](resource-group-move-resources.md).

## <a name="lock-resources"></a>Bloquear recursos
Você pode bloquear uma assinatura, o grupo de recursos ou o recurso tooprevent outros usuários em sua organização acidentalmente excluir ou modificar recursos críticos. Para saber mais, confira [Bloquear recursos com o Gerenciador de Recursos do Azure](resource-group-lock-resources.md).

[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="view-your-subscription-and-costs"></a>Exibir sua assinatura e os custos
Você pode exibir informações sobre sua assinatura e custos de acumulados Olá para todos os seus recursos. Selecione **assinaturas** e assinatura Olá deseja toosee. Você só pode ter um tooselect de assinatura.

![subscription](./media/resource-group-portal/select-subscription.png)

Na folha de assinatura hello, você verá uma taxa de gravação.

![taxa de gravação](./media/resource-group-portal/burn-rate.png)

Haverá também uma divisão de custos por tipo de recurso.

![custo de recurso](./media/resource-group-portal/cost-by-resource.png)

## <a name="export-template"></a>Exportar modelo
Depois de configurar o seu grupo de recursos, convém tooview modelo de Gerenciador de recursos de Olá Olá para grupo de recursos. Exportar modelo de saudação oferece dois benefícios:

1. Você pode facilmente automatizar implantações futuras de solução Olá porque o modelo de saudação contém todos os Olá toda a infraestrutura do.
2. Você pode se familiarizar com sintaxe do modelo observando Olá notação JSON (JavaScript Object) que representa a sua solução.

Para obter as diretrizes passo a passo, confira [Exportar um modelo do Azure Resource Manager a partir dos recursos existentes](resource-manager-export-template.md).

## <a name="delete-resource-group-or-resources"></a>Excluir grupo de recursos ou recursos
Excluir um grupo de recursos exclui todos os recursos de saudação contidos nele. Você também pode excluir recursos individuais de um grupo de recursos. Você deseja tooexercise cuidado quando você excluir um grupo de recursos porque pode haver recursos em outros grupos de recursos que estão vinculado tooit. Gerenciador de recursos não exclui os recursos vinculados, mas eles podem não funcionar corretamente sem recursos Olá esperado.

![excluir grupo](./media/resource-group-portal/delete-group.png)

## <a name="next-steps"></a>Próximas etapas
* logs de atividade tooview, consulte [operações com o Gerenciador de recursos de auditoria](resource-group-audit.md).
* tooview detalhes sobre uma implantação, consulte [Exibir operações de implantação](resource-manager-deployment-operations.md).
* recursos toodeploy por meio do portal hello, consulte [implantar recursos com modelos do Gerenciador de recursos e o portal do Azure](resource-group-template-deploy-portal.md).
* toomanage tooresources de acesso, consulte [usar os recursos de assinatura do Azure função atribuições toomanage acesso tooyour](../active-directory/role-based-access-control-configure.md).
* Para obter diretrizes sobre como as empresas podem usar o Gerenciador de recursos tooeffectively gerenciar assinaturas, consulte [scaffold enterprise do Azure - controle de assinatura prescritivas](resource-manager-subscription-governance.md).

