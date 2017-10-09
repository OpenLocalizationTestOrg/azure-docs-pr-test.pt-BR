---
title: aaaManaging Azure recursos com o Gerenciador de nuvem | Microsoft Docs
description: Saiba como toouse Cloud Explorer toobrowse e gerenciar recursos do Azure no Visual Studio.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 6347dc53-f497-49d5-b29b-e8b9f0e939d7
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/25/2017
ms.author: kraigb
ms.openlocfilehash: 8a81660074d5d04be063df9e25076b7a97586514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-resources-associated-with-your-azure-accounts-in-visual-studio-cloud-explorer"></a>Gerenciar recursos de saudação associados às suas contas do Azure no Visual Studio Cloud Explorer
Cloud Explorer permite que você tooview os recursos do Azure e grupos de recursos, inspecionar suas propriedades e executar ações de diagnóstico do desenvolvedor de chave de dentro do Visual Studio. 

Como Olá [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040), Cloud Explorer baseia-se na pilha do hello Azure Resource Manager. Sendo assim, o Cloud Explorer compreende recursos tais como os grupos de recursos do Azure e serviços do Azure como Aplicativos Lógicos e Aplicativos de API; além disso, ele dá suporte a RBAC [(controle de acesso baseado em função)](active-directory/role-based-access-control-configure.md). 

## <a name="prerequisites"></a>Pré-requisitos
- [2017 do Visual Studio](https://www.visualstudio.com/downloads/) com hello **a carga de trabalho do Azure** selecionado, ou uma versão anterior do Visual Studio com hello [SDK do Microsoft Azure para .NET 2.9](https://www.microsoft.com/en-us/download/details.aspx?id=51657).
- Conta do Microsoft Azure – se não tiver uma conta do Azure, você poderá [inscrever-se para uma avaliação gratuita](http://go.microsoft.com/fwlink/?LinkId=623901) ou [ativar seus benefícios de assinante do Visual Studio](http://go.microsoft.com/fwlink/?LinkId=623901).

> [!NOTE]
> tooview Cloud Explorer, selecione **exibição** > **Cloud Explorer** na barra de menus do hello.   
> 
> 

## <a name="add-an-azure-account-toocloud-explorer"></a>Adicionar um Gerenciador de tooCloud de conta do Azure
recursos de Olá tooview associados a uma conta do Azure, primeiro você deve adicionar Olá conta tooCloud Explorer. 

1. No **Cloud Explorer**, selecione **Configurações de conta do Azure**.

    ![Ícone de configurações de conta do Azure do Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. Selecione **Adicionar nova conta**. 

    ![Link de adicionar a conta do Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/add-account-link.png)

1. Faça logon no toohello conta do Azure cujos recursos você deseja toobrowse. 

1. Depois de conectado tooan conta do Azure, exibem assinaturas Olá associadas a essa conta. Selecione Olá caixas de seleção para assinaturas de conta Olá você deseja toobrowse e, em seguida, selecione **aplicar**. 
 
    ![Soluções de nuvem: selecione toodisplay assinaturas do Azure](media/vs-azure-tools-resources-managing-with-cloud-explorer/select-subscriptions.png)

1. Depois de selecionar assinaturas Olá cujos recursos você deseja toobrowse, as assinaturas e os recursos exibem em Olá Cloud Explorer.

    ![Listagem de recursos do Cloud Explorer para uma conta do Azure](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-listed.png)

## <a name="remove-an-azure-account-from-cloud-explorer"></a>Remover uma conta do Azure do Cloud Explorer 

1. No **Cloud Explorer**, selecione **Configurações de conta do Azure**.

    ![Ícone de configurações de conta do Azure do Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. Selecione Avançar toohello conta a ser tooremove, **remover**.

    ![Ícone de configurações de conta do Azure do Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/remove-account.png)

## <a name="view-resource-types-or-resource-groups"></a>Exibir grupos de recursos ou tipos de recursos
tooview os recursos do Azure, você pode escolher a **tipos de recurso** ou **grupos de recursos** exibição.

1. Em **Cloud Explorer**, selecione Olá suspenso de exibição de recursos.

    ![Exibição do Explorer suspensa lista tooselect Olá desejado recursos de nuvem](media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-view-dropdown.png)

1. No menu de contexto hello, selecione o modo de exibição de saudação desejado: 

    - **Tipos de recurso** exibição - Olá comum usado em Olá [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040), mostra os recursos do Azure, categorizados por seu tipo, como aplicativos web, contas de armazenamento e máquinas virtuais. 
    - **Grupos de recursos** exibir - recursos do Azure categoriza por grupo de recursos do Azure Olá com a qual está associados. Um grupo de recursos é um pacote de recursos do Azure, normalmente usados por um aplicativo específico. toolearn mais sobre grupos de recursos do Azure, consulte [visão geral do Gerenciador de recursos do Azure](./azure-resource-manager/resource-group-overview.md).

    Olá imagem a seguir mostra uma comparação de saudação dois modos de exibição de recursos:

    ![Comparação de modos de exibição de recurso do Cloud Explorer](media/vs-azure-tools-resources-managing-with-cloud-explorer/resource-views-comparison.png)

## <a name="view-and-navigate-resources-in-cloud-explorer"></a>Exibir e navegar por recursos no Cloud Explorer
toonavigate tooan recursos do Azure e exibir suas informações no Gerenciador de nuvem, expanda tipo hello item ou grupo de recursos associados e, em seguida, selecione o recurso de saudação. Quando você seleciona um recurso, informações são exibidas nas guias Olá dois - **ações** e **propriedades** - na parte inferior de saudação do Cloud Explorer. 

- **Ações** guia - listas Olá ações no Gerenciador de nuvem para o recurso de saudação selecionado. Você também pode exibir essas opções clicando Olá recurso tooview seu menu de contexto.

- **Propriedades** guia - mostra propriedades de saudação de recurso hello, como o seu grupo de tipo, a localidade e o recurso ao qual está associado.

Olá imagem a seguir mostra uma comparação de exemplo do que você vê em cada guia para um aplicativo de serviço:

![](./media/vs-azure-tools-resources-managing-with-cloud-explorer/actions-and-properties.png)

Cada recurso tem a ação de saudação **abrir no portal de**. Quando você escolhe essa ação, Cloud Explorer exibe recursos Olá selecionado em Olá [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040). Olá **abrir no portal de** recurso é útil para navegar pelos recursos toodeeply aninhado.

Ações adicionais e valores de propriedade também podem aparecer com base em Olá recursos do Azure. Por exemplo, aplicativos web e aplicativos lógicos também têm ações Olá **abrir no navegador** e **Anexar depurador** além muito**abrir no portal de**. Editores de tooopen ações aparecem quando você escolhe um blob da conta de armazenamento, fila ou tabela. Os aplicativos do Azure têm as propriedades **URL** e **Status**, enquanto os recursos de armazenamento têm as propriedades de cadeia de conexão e chave.

## <a name="find-resources-in-cloud-explorer"></a>Localizar recursos no Cloud Explorer
recursos toolocate com um nome específico em suas assinaturas de conta do Azure, insira o nome de Olá Olá **pesquisa** caixa Cloud Explorer.

![Localizando recursos no Cloud Explorer](./media/vs-azure-tools-resources-managing-with-cloud-explorer/search-for-resources.png)

Como inserir caracteres em Olá **pesquisa** caixa, somente os recursos que correspondem a esses caracteres aparecem na árvore de recursos de saudação.
