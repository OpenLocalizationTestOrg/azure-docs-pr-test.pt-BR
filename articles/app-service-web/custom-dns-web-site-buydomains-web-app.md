---
title: "aaaBuy um nome de domínio personalizado para aplicativos Web do Azure"
description: "Saiba como nome do toobuy um domínio personalizado com um aplicativo web no serviço de aplicativo do Azure."
services: app-service\web
documentationcenter: 
author: cephalin
manager: cfowler
editor: 
ms.assetid: 70fb0e6e-8727-4cca-ba82-98a4d21586ff
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: cephalin
ms.openlocfilehash: 2ff61a3f27020516c917fe105ece99eb2a5754b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="buy-a-custom-domain-name-for-azure-web-apps"></a>Comprar um nome de domínio personalizado para aplicativos Web do Azure

Domínios do Serviço de Aplicativo (versão prévia) são domínios de nível superior gerenciados diretamente no Azure. Eles tornam mais fácil toomanage os domínios personalizados [aplicativos Web do Azure](app-service-web-overview.md). Este tutorial mostra como toobuy um domínio de aplicativo de serviço e atribuir DNS nomes tooAzure os aplicativos Web.

Este artigo é para o Serviço de Aplicativo do Azure (aplicativos Web, aplicativos de API, aplicativos móveis, aplicativos lógicos). Para a máquina virtual do Azure ou no armazenamento do Azure, consulte [tooAzure de domínio do serviço de aplicativo atribuir VM ou armazenamento do Azure](https://blogs.msdn.microsoft.com/appserviceteam/2017/07/31/assign-app-service-domain-to-azure-vm-or-azure-storage/). Para serviços de nuvem, consulte [Configurando um nome de domínio personalizado para um serviço de nuvem do Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).

## <a name="prerequisites"></a>Pré-requisitos

toocomplete este tutorial:

* [Crie um aplicativo do Serviço de Aplicativo](/azure/app-service/) ou use um aplicativo que você criou para outro tutorial.

## <a name="prepare-hello-app"></a>Preparar o aplicativo hello

domínios personalizados de toouse em aplicativos Web do Azure, seu aplicativo web [plano de serviço de aplicativo](https://azure.microsoft.com/pricing/details/app-service/) deve ser uma camada paga (**compartilhado**, **básica**, **padrão**, ou **Premium**). Nesta etapa, verifique se que esse aplicativo da web hello é em Olá suportado de preço.

### <a name="sign-in-tooazure"></a>Entrar tooAzure

Olá abrir [portal do Azure](https://portal.azure.com) e entre com sua conta do Azure.

### <a name="navigate-toohello-app-in-hello-azure-portal"></a>Navegue toohello aplicativo hello portal do Azure

No menu à esquerda do hello, selecione **serviços de aplicativos**e, em seguida, selecione o nome de saudação do aplicativo hello.

![Navegação do portal tooAzure aplicativo](./media/app-service-web-tutorial-custom-domain/select-app.png)

Página de gerenciamento Olá de saudação do aplicativo de serviço de aplicativo é exibida.  

### <a name="check-hello-pricing-tier"></a>Saudação de verificação de preço

No hello barra de navegação de página de aplicativo hello esquerda, role toohello **configurações** seção e selecione **escalar verticalmente (plano de serviço de aplicativo)**.

![Menu Escalar verticalmente](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

camada atual do aplicativo Hello é realçada por uma borda azul. Verificar toomake se esse aplicativo hello não está em Olá **livre** camada. DNS personalizado não é suportada no hello **livre** camada. 

![Verificar tipo de preço](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

Se hello plano de serviço de aplicativo não é **livre**, feche Olá **Escolher tipo de preços** página e ir muito[domínio de saudação comprar](#buy-the-domain).

### <a name="scale-up-hello-app-service-plan"></a>Dimensionar o hello plano de serviço de aplicativo

Selecione qualquer uma das camadas não estão livres de saudação (**compartilhado**, **básica**, **padrão**, ou **Premium**). 

Clique em **Selecionar**.

![Verificar tipo de preço](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

Quando você vir Olá notificação a seguir, a operação de escala de saudação foi concluída.

![Confirmação da operação de escala](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

## <a name="buy-hello-domain"></a>Comprar Olá domínio

### <a name="sign-in-tooazure"></a>Entrar tooAzure
Olá abrir [portal do Azure](https://portal.azure.com/) e entre com sua conta do Azure.

### <a name="launch-buy-domains"></a>Inicializar Comprar domínio
Em Olá **aplicativos Web** , clique em nome de saudação do seu aplicativo web, selecione **configurações**e, em seguida, selecione **domínios personalizados**
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

Em Olá **domínios personalizados** , clique em **comprar domínios**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-1.png)

### <a name="configure-hello-domain-purchase"></a>Configurar a compra de domínio Olá

Em Olá **domínio de serviço de aplicativo** página Olá **pesquisar domínio** caixa, digite o nome de domínio de saudação deseja toobuy e tipo `Enter`. Olá sugeridos domínios disponíveis são mostrados abaixo de caixa de texto de saudação. Selecione um ou mais domínios que você deseja toobuy. 
   
![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-2.png)

Clique em Olá **as informações de contato** e preencha o formulário de informações de contato do domínio hello. Quando terminar, clique em **Okey** página de domínio do serviço de aplicativo toohello tooreturn.
   
É importante preencher todos os campos obrigatórios com a máxima precisão possível. Dados incorretos para informações de contato podem resultar em domínios de toopurchase de falha. 

Em seguida, selecione opções de saudação desejada para seu domínio. Consulte Olá explicações para a tabela a seguir:

| Configuração | Valor sugerido | Descrição |
|-|-|-|
|Renovação automática | **Habilitar** | Renova seu Domínio do Serviço de Aplicativo automaticamente todo ano. Seu cartão de crédito é cobrado Olá mesmo preço de compra no momento de saudação da renovação. |
|Proteção de privacidade | Habilitar | Aceitar muito "Proteção de privacidade," que está incluída no preço de compra Olá _gratuitamente_ (exceto para os domínios de nível superior cujo registro não suportam a proteção de privacidade, como _. co.in_, _. Co.uk_, e assim por diante). |
| Atribuir nomes de host padrão | **www** e **@** | Selecione Olá desejado associações de nome de host, se desejado. Quando Olá domínio compra operação estiver concluída, seu aplicativo web pode ser acessado em nomes de host de saudação selecionada. Se Olá web aplicativo estiver atrás de [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/), você não vir o domínio raiz da saudação opção tooassign hello (@), pois o Gerenciador de tráfego não não suporte a registros. Você pode fazer alterações toohello atribuições de nome de host após a conclusão da compra de domínio hello. |

### <a name="accept-terms-and-purchase"></a>Aceitar os termos e comprar

Clique em **termos legais** tooreview termos de saudação e encargos hello, clique em **comprar**.

> [!NOTE]
> Domínios do serviço de aplicativo usam domínios de saudação toohost DNS do Azure. Além disso toohello taxa de registro de domínio, os encargos de uso do Azure DNS se aplicam. Para obter informações, consulte [Preços do DNS do Azure](https://azure.microsoft.com/pricing/details/dns/).
>
>

Em Olá **domínio de serviço de aplicativo** , clique em **Okey**. Enquanto a operação de saudação está em andamento, você verá Olá notificações a seguir:

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-validate.png)

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-purchase-success.png)

### <a name="test-hello-hostnames"></a>Saudação de nomes de host de teste

Se você tiver atribuído padrão nomes de host tooyour web app, você também verá uma notificação de êxito para cada nome de host selecionado. 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

Você também verá nomes de host de saudação selecionada no hello **domínios personalizados** página Olá **nomes de host** seção. 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added.png)

nomes de host tootest hello, navegue toohello listado os nomes de host no navegador de saudação. No exemplo hello Olá anterior a captura de tela, tente navegar too_kontoso.net_ e _www.kontoso.net_.

## <a name="assign-hostnames-tooweb-app"></a>Atribuir nomes de host tooweb aplicativo

Se você escolher não tooassign um ou mais nomes de host padrão tooyour web a aplicativo durante a saudação processo de compra, ou se você precisar tooassign um nome de host não listados, você pode atribuir um nome de host a qualquer momento.

Você também pode atribuir nomes de host em tooany de domínio do serviço de aplicativo hello outro aplicativo da web. Olá etapas dependem se hello domínio de aplicativo do serviço e aplicativo web de saudação pertencem toohello mesma assinatura.

- Assinatura diferente: mapear registros de DNS personalizados do aplicativo da web toohello Olá domínio de serviço de aplicativo como um domínio externamente adquirido. Para obter informações sobre DNS personalizado adicionando nomes tooan domínio de serviço de aplicativo, consulte [gerenciar registros de DNS personalizados](#custom). toomap um aplicativo web de tooa de domínio externo de adquiridas, consulte [mapear um tooAzure de nome DNS de personalizada existente aplicativos Web](app-service-web-tutorial-custom-domain.md). 
- Mesma assinatura: Olá Use as etapas a seguir.

### <a name="launch-add-hostname"></a>Inicializar adição de nome do host
Em Olá **serviços de aplicativos** página, o nome de saudação select de seu aplicativo web que você deseja tooassign os nomes de host para selecionar **configurações**e, em seguida, selecione **domínios personalizados**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-6.png)

Certifique-se de que seu domínio adquirido está listado no hello **domínios de serviço de aplicativo** seção, mas não selecioná-lo. 

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-select-domain.png)

> [!NOTE]
> Todos os domínios de serviço de aplicativo de saudação mesma assinatura são mostrados no Olá web app **domínios personalizados** página. Se seu domínio está na assinatura do aplicativo da web hello, mas você não pode vê-lo em seu aplicativo da web hello **domínios personalizados** página, tente reabrir Olá **domínios personalizados** página ou atualizar Olá página da Web. Além disso, verifique sino de notificação Olá na parte superior de saudação do hello portal do Azure para falhas de criação ou de andamento.
>
>

Selecione **Adicionar nome do host**.

### <a name="configure-hostname"></a>Configurar nome do host
Em Olá **Adicionar nome de host** caixa de diálogo, digite o nome de domínio totalmente qualificado de saudação do seu domínio do serviço de aplicativo ou qualquer subdomínio. Por exemplo:

- kontoso.net
- www.kontoso.net
- abc.kontoso.net

Quando terminar, selecione **Validar**. tipo de registro de nome de host de saudação é selecionado automaticamente para você.

Selecione **Adicionar nome do host**.

Quando a saudação operação estiver concluída, você verá uma notificação de êxito para Olá atribuído um nome de host.  

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-bind-success.png)

### <a name="close-add-hostname"></a>Feche Adicionar nome do host
Em Olá **Adicionar nome de host** página, atribua a qualquer outro nome de host tooyour aplicativo da web, conforme desejado. Quando terminar, feche Olá **Adicionar nome de host** página.

Agora você deve ver hostname(s) Olá atribuída recentemente em seu aplicativo **domínios personalizados** página.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostnames-added2.png)

### <a name="test-hello-hostnames"></a>Saudação de nomes de host de teste

Navegue toohello listado os nomes de host no navegador de saudação. No exemplo hello Olá anterior a captura de tela, tente navegar too_abc.kontoso.net_.

<a name="custom" />

## <a name="manage-custom-dns-records"></a>Gerenciar registros DNS personalizados

No Azure, os registros DNS para um Domínio do Serviço de Aplicativo são gerenciados usando [DNS do Azure](https://azure.microsoft.com/services/dns/). Você pode adicionar, remover e atualizar registros DNS, assim como para um domínio adquirido externamente.

### <a name="open-app-service-domain"></a>Abrir o Domínio do Serviço de Aplicativo

No hello portal do Azure, no menu da esquerda hello, selecione **mais serviços** > **domínios de serviço de aplicativo**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

Selecione Olá toomanage de domínio. 

### <a name="access-dns-zone"></a>Acessar zona DNS

No menu da esquerda do domínio hello, selecione **zona DNS**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-dns-zone.png)

Essa ação abre Olá [zona DNS](../dns/dns-zones-records.md) página do seu domínio do serviço de aplicativo no DNS do Azure. Para obter informações sobre como tooedit registros DNS, consulte [como zonas DNS toomanage Olá portal do Azure](../dns/dns-operations-dnszones-portal.md).

## <a name="cancel-purchase-delete-domain"></a>Cancelar compra (excluir domínio)

Depois de comprar Olá domínio de serviço de aplicativo, você tem cinco dias toocancel sua compra, para obter um reembolso total. Depois de cinco dias, você pode excluir Olá domínio de serviço de aplicativo, mas não pode receber um reembolso.

### <a name="open-app-service-domain"></a>Abrir o Domínio do Serviço de Aplicativo

No hello portal do Azure, no menu da esquerda hello, selecione **mais serviços** > **domínios de serviço de aplicativo**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-access.png)

Selecione Olá domínio tooyou deseja toocancel ou excluir. 

### <a name="delete-hostname-bindings"></a>Excluir associações de nome de host

No menu da esquerda do domínio hello, selecione **associações de Hostname**. associações de nome de host de saudação de todos os serviços do Azure são listadas aqui.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-hostname-bindings.png)

Você não pode excluir Olá domínio de serviço de aplicativo até que todas as associações de nome de host são excluídas.

Exclua cada associação de nome do host selecionando **…** > **Excluir**. Depois que todas as associações de saudação são excluídas, selecione **salvar**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-delete-hostname-bindings.png)

### <a name="cancel-or-delete"></a>Cancelar ou excluir

No menu da esquerda do domínio hello, selecione **visão geral**. 

Se Olá cancelamento no domínio Olá adquirido não período, selecione **cancelar a compra**. Caso contrário, você verá um botão **Excluir** em vez disso. domínio de saudação toodelete sem um reembolso, selecione **excluir**.

![](./media/custom-dns-web-site-buydomains-web-app/dncmntask-cname-buydomains-cancel.png)

Selecione **Okey** tooconfirm operação de saudação. Se você não quiser tooproceed, clique em qualquer lugar fora da caixa de diálogo de confirmação de saudação.

Após a conclusão da operação de hello, domínio Olá é liberado da sua assinatura e disponível para qualquer pessoa toopurchase novamente. 
