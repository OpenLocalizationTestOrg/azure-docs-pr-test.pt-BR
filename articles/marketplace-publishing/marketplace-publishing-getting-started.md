---
title: aaaOverview de como toocreate e implantar uma oferta toohello Marketplace | Microsoft Docs
description: "Entender a saudação de etapas necessárias toobecome um desenvolvedor do Microsoft aprovado e criar e implantar uma imagem de máquina virtual, modelo, o serviço de dados ou serviço de desenvolvedor no hello Azure Marketplace"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 5343bd26-c6e4-4589-85b7-4a2c00bba8ab
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/05/2017
ms.author: hascipio
ms.openlocfilehash: ac5480b98b8b1021a595db951ed9c974f74415dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-and-manage-an-offer-in-hello-azure-marketplace"></a>Publicar e gerenciar uma oferta em hello Azure Marketplace
Este artigo é fornecido toohelp desenvolvedores criarem, implantarem e gerenciam suas soluções listadas no hello Azure Marketplace para outros clientes do Azure e parceiros toopurchase e uso.

## <a name="marketplace-publishing"></a>Publicação do Marketplace
Como um publicador do Azure, você pode distribuir e vender solução inovadora ou desenvolvedores de tooother de serviço, ISVs, e profissionais de TI Olá Marketplace. Por meio de Olá Marketplace, você pode acessar os clientes que desejam tooquickly desenvolvem seus aplicativos baseados em nuvem e soluções móveis. Se sua solução tem como alvo usuários de negócios, convém Olá tooconsider [AppSource](http://appsource.microsoft.com) marketplace.


## <a name="supported-types-of-solutions"></a>Tipos de soluções com suporte
Olá primeira coisa que você deseja toodo como um publicador é toodefine que tipo de solução de sua empresa oferece. Olá Marketplace dá suporte aos seguintes tipos de ofertas de saudação:

|Tipo de solução|Máquina virtual|Modelo de solução|
|---|---|---|
|**Definição**|Imagens pré-configuradas com um sistema operacional totalmente instalado e um ou mais aplicativos. Uma imagem de máquina virtual fornece Olá informações necessárias toocreate e implantar máquinas virtuais em Olá serviço de máquinas virtuais do Azure.|Uma estrutura de dados que pode fazer referência a um ou mais serviços distintos do Azure, incluindo os serviços publicados por outros vendedores. Assinantes do Azure podem usar toodeploy uma ou mais ofertas de maneira única e coordenada.|
|**Exemplo**|Como um editor do Azure, você criou e validou uma VM com um serviço de banco de dados inovador. Outros assinantes do Azure deseja tooprocure e implantar essa VM em seus ambientes de serviço de nuvem.|Como um publicador do Azure, você tiver fornecido um conjunto de serviços no Azure que tornam os serviços de nuvem toodeploy rápido com balanceamento de carga, a segurança aprimorada e alta disponibilidade. Outros assinantes do Azure podem poupar tempo, aquisição de modelo de solução de saudação que atenda aos seus objetivos. Eles não têm toomanually localizar, adquirir, implantar e configurar Olá serviços do Azure iguais ou semelhantes.|

> [!NOTE]
> Algumas etapas são compartilhadas entre tipos diferentes de saudação de soluções e outros toohello distintos de tipo respectivas da solução. Este artigo fornece uma breve visão geral das etapas de saudação toocomplete é necessário para qualquer tipo de solução.

## <a name="publish-a-solution"></a>Publicar uma solução
![Nomear, registrar, publicar](media/marketplace-publishing-getting-started/img01.png)

### <a name="nominate-your-solution-for-pre-approval"></a>Nomear sua solução para pré-aprovação
toopublish uma máquina virtual [solução](https://createopportunity.azurewebsites.net) toohello Marketplace, Olá completa Microsoft Azure Certified **solução indicação formulário**.

>[!NOTE]
> Se você estiver trabalhando com um gerente de conta do parceiro ou um Gerenciador de parceiro DX, peça toonominate sua solução para o programa de saudação do Azure Certified. Você também pode ir toohello [Microsoft Azure Certified](http://createopportunity.azurewebsites.net) página da Web e preencha Olá formulário de aplicativo. Insira o email de saudação de seu gerente de conta de parceiro ou o gerente do parceiro DX em Olá **Microsoft patrocinador contato** caixa.

Se você atender aos critérios de qualificação Olá Olá [políticas de participação do Azure Marketplace](http://go.microsoft.com/fwlink/?LinkID=526833) e a solicitação for aprovada, podemos começar a trabalhar com você tooonboard toohello sua solução Marketplace.

### <a name="register-your-account-as-a-microsoft-seller"></a>Registrar sua conta como um vendedor da Microsoft
Registre sua conta da Microsoft como uma [conta Microsoft Developer](marketplace-publishing-accounts-creation-registration.md).

### <a name="publish-your-solution"></a>Publicar sua solução
toopublish toohello uma solução Marketplace, siga estas etapas:
1. Atender aos requisitos de não-Olá.

    a. Atender Olá [pré-requisitos não-](marketplace-publishing-pre-requisites.md).

    b. Atender Olá [pré-requisitos técnicos de VM](marketplace-publishing-vm-image-creation-prerequisites.md).

    c. Atender Olá [pré-requisitos técnicos de modelo de solução](marketplace-publishing-solution-template-creation-prerequisites.md).

2. Criar sua oferta.

    a. Criar uma oferta de [máquina virtual](marketplace-publishing-vm-image-creation.md).

    b. Criar uma oferta de [modelo de solução](marketplace-publishing-solution-template-creation.md).

3. Criar o [conteúdo de marketing](marketplace-publishing-push-to-staging.md) da sua oferta.

4. Testar sua oferta em preparo.

    a. Testar sua oferta de VM em [preparo](marketplace-publishing-vm-image-test-in-staging.md).

    b. Testar sua oferta de modelo de solução em [preparo](marketplace-publishing-solution-template-test-in-staging.md).

5. Implantar a sua oferta toohello [Marketplace](marketplace-publishing-push-to-production.md).


### <a name="create-and-manage-a-virtual-machine-image"></a>Criar e gerenciar uma imagem de máquina virtual
Criar e gerenciar uma imagem de VM usando estes recursos:
* Criar uma imagem de VM [local](marketplace-publishing-vm-image-creation-on-premise.md).
* Criar uma máquina virtual em execução [Windows hello portal do Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Criar uma máquina virtual em execução [Linux no portal do Azure de saudação](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Solucionar problemas comuns encontrados durante a [criação do VHD](marketplace-publishing-vm-image-creation-troubleshooting.md).

## <a name="manage-your-solution"></a>Gerenciar sua solução
Gerencie a sua solução com a Ajuda de saudação recursos a seguir:
* [Leia o guia de após a produção de hello para a máquina virtual oferece](marketplace-publishing-vm-image-post-publishing.md)
* [Atualizar os detalhes de não-Olá de uma oferta ou uma SKU](marketplace-publishing-vm-image-post-publishing.md#update-the-nontechnical-details-of-an-offer-or-a-sku)
* [Atualizar detalhes técnicos da saudação de uma oferta ou uma SKU](marketplace-publishing-vm-image-post-publishing.md#update-the-technical-details-of-a-sku)
* [Adicionar uma nova SKU em uma oferta listada](marketplace-publishing-vm-image-post-publishing.md#add-a-new-sku-under-a-listed-offer)
* [Alterar a contagem do disco de dados Olá para um SKU listado](marketplace-publishing-vm-image-post-publishing.md#change-the-data-disk-count-for-a-listed-sku)
* [Excluir uma oferta listada do hello Marketplace](marketplace-publishing-vm-image-post-publishing.md)
* [Excluir um SKU listado do hello Marketplace](marketplace-publishing-vm-image-post-publishing.md#delete-a-listed-sku-from-the-marketplace)
* [Excluir a versão atual de saudação de uma SKU listada do hello Marketplace](marketplace-publishing-vm-image-post-publishing.md#delete-the-current-version-of-a-listed-sku-from-the-marketplace)
* [Reverter Olá listando os valores de tooproduction de preço](marketplace-publishing-vm-image-post-publishing.md#revert-the-listing-price-to-production-values)
* [Reverter Olá valores tooproduction do modelo de cobrança](marketplace-publishing-vm-image-post-publishing.md#revert-the-billing-model-to-production-values)
* [Reverter a configuração de visibilidade de saudação de um valor de produção de toohello SKU listado](marketplace-publishing-vm-image-post-publishing.md#revert-the-visibility-setting-of-a-listed-sku-to-the-production-value)
* [Alterar seu incentivo ao revendedor do Provedor de Soluções na Nuvem](marketplace-publishing-csp-incentive.md)
* [Entender seu relatório de pagamento](marketplace-publishing-report-payout.md)
* [Obtenha suporte como um editor](marketplace-publishing-get-publisher-support.md)

## <a name="additional-resources"></a>Recursos adicionais
[Configurar o Azure PowerShell](marketplace-publishing-powershell-setup.md)
