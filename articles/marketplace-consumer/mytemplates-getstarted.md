---
title: aaaGet iniciado com modelos privados | Microsoft Docs
description: "Adicionar, gerenciar e compartilhar seus modelos privados usando Olá portal do Azure, a saudação CLI do Azure ou o PowerShell."
services: marketplace-customer
documentationcenter: 
author: VybavaRamadoss
manager: asimm
editor: 
tags: marketplace, azure-resource-manager
keywords: 
ms.assetid: 6ec20778-b578-4885-acb5-104b0e51ea1a
ms.service: marketplace
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: vybavar
ms.openlocfilehash: 1fe2c6422f62a98f7ae9ba5c61b9639d993f0bca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-private-templates-on-hello-azure-portal"></a>Introdução ao privada modelos em Olá Portal do Azure
Um [do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) modelo é um modelo declarativo usado toodefine sua implantação. Você pode definir Olá toodeploy de recursos para uma solução e especifique os parâmetros e variáveis que permitem valores tooinput para ambientes diferentes. Olá modelo consiste em JSON e expressões que você pode usar valores de tooconstruct para sua implantação.

Você pode usar o hello novo **modelos** recurso Olá [Portal do Azure](https://portal.azure.com) juntamente com hello **Microsoft.Gallery** provedor de recursos como uma extensão de saudação [ Azure Marketplace](https://azure.microsoft.com/marketplace/) tooenable toocreate de usuários, gerenciar e implantar modelos privados de uma biblioteca de pessoal.

Este documento orienta você por meio de adicionar, gerenciar e compartilhar uma particular **modelo** usando Olá Portal do Azure.

## <a name="guidance"></a>Diretrizes
Olá sugestões a seguir ajudará você a aproveitar ao máximo **modelos** ao trabalhar com suas soluções:

* Um **modelo** é um recurso de encapsulamento que contém um modelo do Resource Manager e metadados adicionais. Ele se comporta de maneira muito semelhante tooan item Olá Marketplace. Olá principal diferença é que ele é um item privado como itens do Marketplace públicos toohello contrário.
* Olá **modelos** biblioteca funciona bem para usuários que precisam de toocustomize suas implantações.
* **Modelos** funcionam bem com usuários que precisam de um repositório simples no Azure.
* Comece com um modelo existente do Resource Manager. Encontre modelos no [github](https://github.com/Azure/azure-quickstart-templates) ou [exporte o modelo](../azure-resource-manager/resource-manager-export-template.md) de um grupo de recursos existente.
* **Modelos de** usuário toohello associado que publica-los. nome do publicador Olá é visível tooeveryone que tenha acesso de leitura tooit.
* **Modelos** são recursos do Resource Manager e não podem ser renomeados depois de publicados.

## <a name="add-a-template-resource"></a>Adicionar um recurso de modelo
Há dois toocreate de maneiras um **modelo** recurso Olá portal do Azure.

### <a name="method-1--create-a-new-template-resource-from-a-running-resource-group"></a>Método 1: criar um novo recurso de modelo de um grupo de recursos em execução
1. Navegue tooan grupo de recursos existente no hello Portal do Azure. Selecione **Exportar modelo** em **Configurações**.
2. Depois que o modelo do Gerenciador de recursos de saudação é exportado, use Olá **Salvar modelo** botão toosave-toohello **modelos** repositório. Encontre todos os detalhes sobre a exportação de modelos [aqui](../azure-resource-manager/resource-manager-export-template.md).
   <br /><br />
   ![Exportação do grupo de recursos](media/rg-export-portal1.PNG)  <br />
3. Selecione Olá **salvar tooTemplate** botão de comando.
   <br /><br />
4. Digite hello informações a seguir:
   
   * Nome – nome do objeto de modelo de saudação (Observação: esse é um nome com base do Azure Resource Manager. Todas as restrições de nomenclatura são aplicáveis e ele não pode ser alterado depois de criado).
   * Descrição – resumo rápido sobre o modelo de saudação.
     
     ![Salvar Modelo](media/save-template-portal1.PNG)  <br />
5. Clique em **Salvar**.
   
   > [!NOTE]
   > Olá folha do modelo de exportação mostra notificações quando hello, modelo exportado do Gerenciador de recursos tem erros, mas ainda será capaz de toosave este toohello de modelo do Gerenciador de recursos modelos. Certifique-se de que você verifique e corrija qualquer Gerenciador de recursos de problemas do modelo antes de reimplantação hello exportada modelo do Gerenciador de recursos.
   > 
   > 

### <a name="method-2--add-a-new-template-resource-from-browse"></a>Método 2: adicionar um novo recurso de modelo por meio de navegação
Você também pode adicionar um novo **modelo** do zero usando Olá + adicionar o botão de comando em **procurar > modelos**. Você precisará tooprovide um nome, descrição e hello modelo JSON do Gerenciador de recursos.

![Adicionar Modelo](media/add-template-portal1.PNG)  <br />

> [!NOTE]
> Microsoft.Gallery é um provedor de recursos do Azure baseado em locatário. Olá, recurso de modelo é usuário toohello associado que o criou. Não é uma assinatura específica tooany associado. Uma assinatura precisa toobe escolhido somente ao implantar um modelo.
> 
> 

## <a name="view-template-resources"></a>Exibir recursos de modelo
Todos os **modelos** tooyou disponível pode ser visto no **procurar > modelos**. Isso inclui **modelos** que você criou e os que foram compartilhados com você com vários níveis de permissões. Para obter mais detalhes no hello [controle de acesso](#access-control-for-a-tenant-resource-provider) seção abaixo.

![Exibir Modelo](media/view-template-portal1.PNG)  <br />

Você pode exibir detalhes de saudação de um **modelo** clicando em um item na lista de saudação.

![Exibir Modelo](media/view-template-portal2c.png)  <br />

## <a name="edit-a-template-resource"></a>Editar um recurso de modelo
Você pode iniciar Olá Editar fluxo para um **modelo** por item de saudação clique direito na lista de pesquisa de saudação ou escolhendo o botão de comando de edição de saudação.

![Editar modelo](media/edit-template-portal1a.PNG)  <br />

Você pode editar a descrição de saudação ou texto de modelo do Gerenciador de recursos. Você não pode editar o nome de saudação porque é um nome de recurso do Gerenciador de recursos. Quando você editar o modelo do Gerenciador de recursos de saudação JSON validamos tooensure que é JSON válido. Escolha **Okey** e **salvar** toosave seu modelo atualizado.

![Editar modelo](media/edit-template-portal2a.PNG)  <br />

Uma vez Olá **modelo** é salvo você verá uma notificação de confirmação.

![Editar modelo](media/edit-template-portal3b.png)  <br />

## <a name="deploy-a-template-resource"></a>Implantar um recurso de modelo
Você pode implantar qualquer **Modelo** para o qual tiver permissões de **Leitura**. implantação do fluxo de saudação inicia a folha de implantação de modelo do Azure standard hello. Preencha os valores hello tooproceed de parâmetros de modelo Olá Gerenciador de recursos com a implantação de saudação.

![Implantar o modelo](media/deploy-template-portal1b.png)  <br />

## <a name="share-a-template-resource"></a>Compartilhar um recurso de modelo
Um recurso de **modelo** pode ser compartilhados com seus colegas. Compartilhamento se comporta da mesma forma muito[atribuição de função para qualquer recurso no Azure](../active-directory/role-based-access-control-configure.md). Olá **modelo** proprietário fornece permissões tooother usuários podem interagir com um recurso de modelo. Olá pessoa ou grupo de pessoas que você compartilha Olá **modelo** com será capaz de toosee modelo de Gerenciador de recursos de saudação e suas propriedades de galeria.

### <a name="access-control-for-hello-microsoftgallery-resources"></a>Controle de acesso para recursos de Microsoft.Gallery Olá
| Função | Permissões |
| --- | --- |
| Proprietário |Permite que o controle total sobre o recurso de modelo Olá incluindo compartilhamento |
| Leitor |Permite a leitura e Execute(Deploy) Olá recurso de modelo |
| Colaborador |Permite a permissão de edição e exclusão em Olá recurso de modelo. Usuário não pode compartilhar Olá modelo com outras pessoas |

Selecione **compartilhamento** no item de navegação Olá com um clique direito ou na folha de modo de exibição de saudação de um item específico. Isso inicia uma experiência de compartilhamento.

![Compartilhar modelo](media/share-template-portal1a.png)  <br />

 Agora você pode escolher uma função e tooa um acesso de tooprovide usuário ou grupo específico **modelo**. funções disponíveis Olá são proprietário, o leitor e o colaborador. Para obter mais detalhes no hello [controle de acesso](#access-control-for-a-tenant-resource-provider) seção acima.

![Compartilhar modelo](media/share-template-portal2b.png)  <br />

![Compartilhar modelo](media/share-template-portal3b.png)  <br />

Clique em **Selecionar** e em **Ok**. Agora você pode ver Olá usuários ou grupos adicionados toohello recursos.

![Compartilhar modelo](media/share-template-portal4b.png)  <br />

> [!NOTE]
> Um modelo só pode ser compartilhado com usuários e grupos no hello mesmo locatário do Active Directory do Azure. Se você compartilhar um modelo com um endereço de email que não está em seu locatário, será enviado um convite perguntando Olá toojoin saudação do locatário usuário como convidado.
> 
> 

## <a name="next-steps"></a>Próximas etapas
* toolearn sobre como criar modelos do Gerenciador de recursos, consulte [criando modelos](../azure-resource-manager/resource-group-authoring-templates.md)
* funções de saudação toounderstand você pode usar em um modelo do Gerenciador de recursos, consulte [funções de modelo](../azure-resource-manager/resource-group-template-functions.md)
* Para obter diretrizes sobre como criar os modelos, confira [Práticas recomendadas para a criação de modelos do Gerenciador de Recursos do Azure](../azure-resource-manager/best-practices-resource-manager-design-templates.md)

