---
title: "aaaAzure gerenciados aplicativos Olá Marketplace | Microsoft Docs"
description: "Descreve o Azure aplicativos gerenciados que estão disponíveis por meio de saudação Marketplace."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/09/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: b3cdf3f1fccdd47db699e4892ae8bce35118bfd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-managed-applications-in-hello-marketplace"></a>Aplicativos no hello Marketplace de gerenciado do Azure

 MSPs, ISVs e integradores de sistema (SIs) podem usar aplicativos toooffer gerenciado do Azure aos clientes do Azure Marketplace de tooall soluções. Essas soluções reduzem manutenção hello e sobrecarga de manutenção para os clientes. Editores podem vender infraestrutura e software por meio de saudação Marketplace. Eles podem anexar suporte operacional toomanaged aplicativos e serviços. Para saber mais, consulte [Visão geral do aplicativo gerenciado](managed-application-overview.md).

Este artigo explica como um MSP, ISV ou SI pode publicar um aplicativo toohello Marketplace e torná-lo toocustomers amplamente disponíveis.

## <a name="prerequisites-for-publishing-a-managed-application"></a>Pré-requisitos para publicar um aplicativo gerenciado

Pré-requisitos toolisting em Olá Marketplace:

* Técnicos

    *  Para obter informações sobre a estrutura básica de saudação e a sintaxe de modelos do Azure Resource Manager, consulte [modelos do Azure Resource Manager](resource-group-authoring-templates.md).
    *  soluções de modelo completa tooview, consulte [modelos de início rápido do Azure](https://azure.microsoft.com/en-us/documentation/templates/) ou hello [repositório de modelos de início rápido](https://github.com/azure/azure-quickstart-templates).
    *  Para obter informações sobre como toocreate Olá interface para os clientes que implantar seu aplicativo por meio de saudação Marketplace, consulte [criar um arquivo de definição de interface do usuário](managed-application-createuidefinition-overview.md).

* Não técnico (requisitos de negócios)

    *   Sua empresa ou a sua subsidiária deve estar localizada em um país onde as vendas são suportadas pelo Olá Marketplace.
    *   O produto deve ser licenciado de forma que seja compatível com modelos de cobrança com suporte Olá Marketplace.
    *   Você é responsável para fazer toocustomers de suporte técnico disponíveis de forma comercialmente razoável. suporte de saudação pode ser gratuito, paga, ou por meio da comunidade de suporte.
    *   Você é responsável pelo licenciamento do software e quaisquer dependências de software de terceiros.
    *   Você deve fornecer o conteúdo que atenda aos critérios para sua oferta toobe listados no hello Marketplace e no hello portal do Azure.
    *   Você deve aceitar os termos de toohello de saudação do Azure Marketplace participação políticas e contrato do publicador.
    *   Você deve concordar toocomply com hello termos de uso, declaração de privacidade da Microsoft e contrato de programa de certificados do Microsoft Azure.

## <a name="create-a-new-azure-application-offer"></a>Criar uma nova oferta de aplicativo do Azure

Depois que você atenda aos pré-requisitos de hello, você está pronto toocreate sua oferta do aplicativo gerenciado. Vamos analisar rapidamente uma visão geral de uma oferta e um SKU.

### <a name="offer"></a>Oferta

oferta de saudação de um aplicativo gerenciado corresponde classe tooa do produto da oferta do publicador. Se você tiver um novo tipo de solução/aplicativo que você deseja toomake disponível no hello Marketplace, você pode configurá-lo como uma oferta nova. Uma oferta é uma coleção de SKUs. Cada oferta aparece como sua própria entidade em Olá Marketplace.

### <a name="sku"></a>SKU

Um SKU é Olá menor podem ser comprados unidade de uma oferta. Você pode usar um SKU dentro Olá mesmo toodifferentiate de classe (oferta) de produto entre:

* Diferentes recursos com suporte.
* Se a oferta de saudação é gerenciada ou não.
* Modelos de cobrança com suporte.

Um SKU aparece sob Olá pai oferta no hello Marketplace. Ele aparecerá como sua própria entidade pode ser adquirida em Olá portal do Azure.

### <a name="set-up-an-offer"></a>Configurar uma oferta

1. Entrar toohello [portal Cloud Partner](https://cloudpartner.azure.com/).

2. No painel de navegação Olá Olá esquerda, selecione **+ nova oferta** > **aplicativos do Azure**.

    ![Nova oferta](./media/managed-application-author-marketplace/newOffer.png)

3. Preencher formulários Olá que aparecem no hello deixado no hello **Editor** exibição. Os campos obrigatórios estão marcados com um asterisco vermelho (*).

    ![Configurações da oferta](./media/managed-application-author-marketplace/newOffer_OfferSettings.png)

    Quatro formulários principais são usado toocreate um aplicativo gerenciado:

    a. Configurações da oferta

    b. SKUs

    c. Marketplace

    d. Suporte

Esses formulários são descritos mais detalhadamente nas seções a seguir de saudação.

## <a name="offer-settings-form"></a>Formulário de Configurações de Oferta
Use configurações de oferta este formulário básico toospecify hello.

1. Preencha Olá **oferecem configurações** formulário. campos diferentes Olá são:

    a. **ID da oferta**: este identificador exclusivo identifica oferta hello dentro de um perfil do publicador. Essa ID está visível em URLs de produto, modelos do Resource Manager e relatórios de cobrança. Ele só pode ser composto de caracteres alfanuméricos minúsculos ou traços (-). Olá ID não pode terminar com um traço. Ele é limitado tooa máximo de 50 caracteres. Após a ativação da oferta, esse campo é bloqueado.

    b. **ID do editor**: Use esse perfil de publicador lista suspensa toochoose Olá deseja toopublish esta oferta em. Após a ativação da oferta, esse campo é bloqueado.

    c. **Nome**: este nome para exibição para sua oferta aparece no hello Marketplace e no portal de saudação. Ele pode ter um máximo de 50 caracteres. Inclua um nome de marca reconhecível para o seu produto. Não inclua o nome de sua empresa aqui, a menos que seja a maneira como ela é comercializada. Se você estiver marketing esta oferta em seu próprio site, certifique-se de que o nome hello seja exatamente como ela aparece no seu site.

2. Selecione **salvar** toosave seu progresso. 

## <a name="skus-form"></a>Formulário de SKUs
Olá próxima etapa é tooadd SKUs para sua oferta.

1. Selecione **SKUs** > **Novo SKU**. 

    ![Selecionar novo SKU](./media/managed-application-author-marketplace/newOffer_skus.png)

2. Insira uma **ID de SKU**. Uma ID de SKU é um identificador exclusivo para Olá SKU dentro de uma oferta. Essa ID está visível em URLs de produto, modelos do Resource Manager e relatórios de cobrança. Ele só pode ser composto de caracteres alfanuméricos minúsculos ou traços (-). Olá ID não pode terminar com um traço e é limitado tooa máximo de 50 caracteres. Após a ativação da oferta, esse campo é bloqueado. Pode existir várias SKUs em uma oferta. Você precisa de uma SKU de cada imagem de plano de toopublish.

3. Preencha Olá **detalhes de SKU** seção Olá formulário a seguir:

    ![Fornecer novo SKU](./media/managed-application-author-marketplace/newOffer_newsku.png)

    Preencha Olá campos a seguir:
    
    a. **Título**: insira um título para esse SKU. Esse título aparece na Galeria de saudação para este item.

    b. **Resumo**: insira um breve resumo para esse SKU. Esse texto aparece sob o título de saudação.

    c. **Descrição**: insira uma descrição detalhada sobre Olá SKU.

    d. **Tipo de SKU**: Olá valores permitidos são **aplicativo gerenciado** e **modelos de solução**. Nesse caso, selecione **Aplicativo Gerenciado**.

4. Preencha Olá **detalhes do pacote** seção Olá formulário a seguir:

    ![Pacote](./media/managed-application-author-marketplace/newOffer_newsku_package.png)

    Preencha Olá campos a seguir:

    a. **Versão atual**: insira uma versão para o pacote de saudação carregar. Ele deve estar no formato de saudação `{number}.{number}.{number}{number}`.

    b. **Selecione um arquivo de pacote**: Este pacote contém os seguintes arquivos compactados em um arquivo. zip de saudação:
    * **applianceMainTemplate.json**: arquivo de modelo de implantação de saudação que tenha usado o aplicativo da solução toodeploy hello. Para obter informações sobre como toocreate arquivos de modelo de implantação, consulte [criar seu primeiro modelo do Azure Resource Manager](resource-manager-create-first-template.md).
    * **appliancecreateUIDefinition.json**: este arquivo é usado pelo Olá toogenerate portal do Azure Olá interface do usuário que tenha usado tooprovision essa solução/aplicativo. Para saber mais, consulte [Introdução a CreateUiDefinition](managed-application-createuidefinition-overview.md).
    * **mainTemplate.json**: este arquivo de modelo contém apenas os recursos de Microsoft.Solution/appliances hello. arquivo de mainTemplate Olá inclui Olá propriedades a seguir:

        *  **tipo**: Use **Marketplace** para aplicativos gerenciados no hello Marketplace.
        *  **ManagedResourceGroupId**: este grupo de recursos na assinatura saudação do cliente é onde todos os recursos de saudação definidos no applianceMainTemplate.json são implantados.
        *  **PublisherPackageId**: esta cadeia de caracteres identifica com exclusividade o pacote de saudação. Fornecer valor Olá no formato de saudação do `{publisherId}.{OfferId}.{SKUID}.{PackageVersion}`.

Obter Olá **ID oferecem** e **ID do editor** de saudação publicação portal, conforme mostrado no Olá a imagem a seguir:

![ID da oferta](./media/managed-application-author-marketplace/UniqueString_pubid_offerid.png)
        
Obter Olá **ID do SKU**, conforme mostrado no Olá a imagem a seguir:

![Id do SKU](./media/managed-application-author-marketplace/UniqueString_skuid.png)
        
Obter pacote hello **versão**, conforme mostrado no Olá a imagem a seguir:

![Versão do pacote](./media/managed-application-author-marketplace/UniqueString_packageversion.png)
    
  Com base em Olá anterior exemplos, Olá valor **PublisherPackageId** é `azureappliance-test.ravmanagedapptest.ravpreviewmanagedsku.1.0.0`.

  Exemplo de mainTemplate.json:

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
      "storageAccountNamePrefix": {
        "type": "string",
        "metadata": {
          "description": "Specify hello name of hello storage account"
        }
      },
      "storageAccountType": {
        "type": "string"
      }
    },
    "variables": {
      "managedResourceGroup": "[concat(resourceGroup().id,uniquestring(resourceGroup().id))]"
    },
    "resources": [{
      "type": "Microsoft.Solutions/appliances",
      "apiVersion": "2016-09-01-preview",
      "name": "[concat(parameters('storageAccountNamePrefix'), '-', 'managed')]",
      "location": "[resourceGroup().location]",
      "kind": "marketplace",
      "properties": {
        "managedResourceGroupId": "[variables('managedResourceGroup')]",
        "PublisherPackageId":"azureappliancetest.ravmanagedapptest.ravpreviewmanagedsku.1.0.0",
        "parameters": {
          "storageAccountName": {
            "value": "[parameters('storageAccountNamePrefix')]"
          },
          "storageAccountType": {
            "value": "[parameters('storageAccountType')]"
          }
        }
      }
    }],
    "outputs": {

    }
  }
  ```

Este pacote deve conter todos os outros modelos aninhados ou scripts que são necessário toosuccessfully provisionar este aplicativo. Olá arquivos mainTemplate.json, applianceMainTemplate.json e applianceCreateUIDefinition.json devem estar presentes na pasta raiz de saudação.

* **Autorizações**: esta propriedade define que obtém acesso e hello nível de acesso a recursos de toohello em assinaturas de clientes. publicador de saudação pode usá-lo aplicativo hello de toomanage em nome do cliente hello.
* **PrincipalId**: esta propriedade é o identificador do hello Azure Active Directory (AD do Azure) de um usuário, grupo de usuários ou aplicativos que concedeu permissões específicas nos recursos Olá Olá a assinatura de cliente. saudação de definição de função descreve as permissões de saudação. 
* **Definição de função**: esta propriedade é uma lista de todos os hello controle de acesso baseado em função (RBAC) funções internas fornecidas pelo AD do Azure. Você pode selecionar a função hello que é mais apropriados recursos de saudação do toomanage toouse em nome do cliente hello.

É possível adicionar várias autorizações. Recomendamos que você crie um grupo de usuários do AD e especifica sua ID em **PrincipalId**. Dessa forma, você pode adicionar mais grupo de usuário toohello usuários sem a necessidade de Olá tooupdate Olá SKU.

Para obter mais informações sobre o RBAC, consulte [Introdução ao RBAC no portal do Azure de saudação](../active-directory/role-based-access-control-what-is.md).

## <a name="marketplace-form"></a>Formulário do Marketplace

Olá formulário Marketplace solicita para os campos que aparecem na Olá [Azure Marketplace](https://azuremarketplace.microsoft.com) e Olá [portal do Azure](https://portal.azure.com/).

### <a name="preview-subscription-ids"></a>IDs de assinatura para versão prévia

Insira uma lista de IDs que podem acessar a oferta de saudação após a publicação de assinatura do Azure. Você pode usar esses oferta de saudação visualizada tootest assinaturas listadas em branco antes de você fazê-lo ao vivo. Você pode compilar uma lista de permissões de backup too100 assinaturas no portal de parceiros de saudação.

### <a name="suggested-categories"></a>Categorias sugeridas

Selecione as categorias de toofive da lista de saudação que sua oferta pode ser associada ao melhor. Essas categorias é usado toomap suas categorias de produtos de toohello de oferta que estão disponíveis no hello [Azure Marketplace](https://azuremarketplace.microsoft.com) e hello [portal do Azure](https://portal.azure.com/).

#### <a name="azure-marketplace"></a>Azure Marketplace

Resumo de saudação do seu aplicativo gerenciado exibe Olá campos a seguir:

![Resumo do marketplace](./media/managed-application-author-marketplace/publishvm10.png)

Olá **visão geral** guia de seu aplicativo gerenciado exibe Olá campos a seguir:

![Visão geral do Marketplace](./media/managed-application-author-marketplace/publishvm11.png)

Olá **planos + preços** guia de seu aplicativo gerenciado exibe Olá campos a seguir:

![Planos do marketplace](./media/managed-application-author-marketplace/publishvm15.png)

#### <a name="azure-portal"></a>Portal do Azure

Resumo de saudação do seu aplicativo gerenciado exibe Olá campos a seguir:

![Resumo do portal](./media/managed-application-author-marketplace/publishvm12.png)

Visão geral de saudação do seu aplicativo gerenciado exibe Olá campos a seguir:

![Visão geral do portal](./media/managed-application-author-marketplace/publishvm13.png)

#### <a name="logo-guidelines"></a>Diretrizes de logotipo

Siga estas diretrizes para qualquer logotipo que você carrega no portal de parceiros de nuvem de saudação:

*   Olá design do Azure tem uma paleta de cores simples. Limitar o número de saudação do primário e secundário cores no logotipo.
*   cores de tema de saudação do portal de saudação são brancas e preto. Não use essas cores como cores de plano de fundo Olá do seu logotipo. Use uma cor que torna seu logotipo proeminente no portal de saudação. É recomendável usar cores primárias simples. *Se você usar um plano de fundo transparente, certifique-se de Olá logotipo e o texto não estiverem em branco, preto ou azul.*
*   Não use uma cor de fundo do logotipo hello.
*   Não coloque o texto no logotipo hello, nem mesmo sua empresa ou o nome da marca. Olá aparência de seu logotipo deve ser simples e evitar gradientes.
*   Certifique-se de logotipo Olá não está ampliado.

#### <a name="hero-logo"></a>Logotipo Hero

logotipo do Hello herói é opcional. publicador de saudação pode escolher não tooupload um logotipo herói. Depois que o ícone de herói Olá é carregado, ele não pode ser excluído. Nesse momento, parceiro Olá deve seguir diretrizes de mercado Olá para ícones herói.

Siga estas diretrizes para o ícone do logotipo herói hello:

*   nome de exibição do publicador Hello, título de plano hello e resumo longo de oferta de saudação são exibidos em branco. Portanto, não use uma cor clara para plano de fundo de saudação do ícone de herói hello. Não há permissão para telas de fundo pretas, brancas ou transparentes para ícones hero.
*   Depois de oferta Olá estiver listada, publisher Olá nome para exibição, título do plano de saudação, resumo longo de oferta hello e Olá **criar** botão são inserido programaticamente no logotipo de herói hello. Consequentemente, não digite qualquer texto enquanto você projeta o logotipo de herói hello. Deixe espaço vazio do hello direita como texto de saudação está incluído programaticamente nesse espaço. um espaço vazio para o texto de saudação Olá deve ser 415 x 100 pixels saudação à direita. Ele tem um deslocamento de 370 pixels da saudação esquerda.

    ![Exemplo de logotipo hero](./media/managed-application-author-marketplace/publishvm14.png)

## <a name="support-form"></a>Formulário de suporte

Preencha Olá **suporte** entra em contato com o formulário com o suporte da sua empresa. Essas informações podem ser de contatos da engenharia e do atendimento ao cliente.

## <a name="publish-an-offer"></a>Publicar uma oferta

Depois de preencher todas as seções de saudação, selecione **publicar** toostart processo de saudação que torna seu toocustomers disponíveis da oferta.

## <a name="next-steps"></a>Próximas etapas

* Para aplicativos de toomanaged uma introdução, consulte [visão geral do aplicativo gerenciado](managed-application-overview.md).
* Para obter informações sobre o consumo de um aplicativo gerenciado de saudação Marketplace, consulte [Azure consumir gerenciados aplicativos Olá Marketplace](managed-application-consume-marketplace.md).
* Para obter informações sobre como publicar um aplicativo gerenciado do Catálogo de Serviços, consulte [Criar e publicar um aplicativo gerenciado do Catálogo de Serviços](managed-application-publishing.md).
* Para obter informações sobre como consumir um aplicativo gerenciado do Catálogo de Serviços, consulte [Consumir um aplicativo gerenciado do Catálogo de Serviços](managed-application-consumption.md).
