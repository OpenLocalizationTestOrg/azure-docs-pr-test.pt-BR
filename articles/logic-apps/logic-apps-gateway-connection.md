---
title: "aaaAccess fontes de dados no local para os aplicativos lógicos do Azure | Microsoft Docs"
description: "Configurar o gateway de dados local Olá para que possa acessar fontes de dados em instalações de aplicativos lógicos"
keywords: "acessar dados, local, transferência de dados, criptografia, fontes de dados"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 6cb4449d-e6b8-4c35-9862-15110ae73e6a
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/13/2017
ms.author: LADocs; dimazaid; estfan
ms.openlocfilehash: 1d3deaac5a095316ce78e224dab0c08559bc2ff2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="access-data-sources-on-premises-from-logic-apps-with-hello-on-premises-data-gateway"></a>Acessar fontes de dados em instalações de aplicativos lógicos com o gateway de dados local Olá

tooaccess fontes de dados no local de seus aplicativos lógicos, configure um gateway de dados local que podem usar aplicativos lógicos com conectores com suporte. gateway de saudação atua como uma ponte que fornece transferência de dados rápida e criptografia entre fontes de dados no local e seus aplicativos lógicos. gateway Olá transmite dados de fontes locais em canais criptografados por meio de saudação do Azure Service Bus. Todo o tráfego originado como proteger o tráfego de saída do agente de gateway de saudação. Saiba mais sobre [como funciona o gateway de dados Olá](logic-apps-gateway-install.md#gateway-cloud-service). 

gateway Olá dá suporte a fontes de dados de toothese de conexões no local:

*   BizTalk Server 2016
*   DB2  
*   Sistema de Arquivos
*   Informix
*   MQ
*   MySQL
*   Banco de dados Oracle
*   PostgreSQL
*   Servidor de aplicativos SAP 
*   Servidor de mensagens SAP
*   SharePoint
*   SQL Server
*   Teradata

Estas etapas mostram como tooset backup Olá local toowork de gateway de dados com seus aplicativos lógicos. Para obter mais informações sobre os conectores com suporte, consulte [Conectores para Aplicativo Lógico do Azure](../connectors/apis-list.md). 

Para obter informações sobre como toouse Olá gateway com outros serviços, consulte estes artigos:

*   [Gateway de dados local do Microsoft Power BI](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [Gateway de dados local do Azure Analysis Services](../analysis-services/analysis-services-gateway.md)
*   [Gateway de dados local do Microsoft Flow](https://flow.microsoft.com/documentation/gateway-manage/)
*   [Gateway de dados local do Microsoft PowerApps](https://powerapps.microsoft.com/tutorials/gateway-management/)

## <a name="requirements"></a>Requisitos

* É necessário já ter [instalado o gateway de dados Olá em um computador local](logic-apps-gateway-install.md).

* Quando você entrar no toohello portal do Azure, você tem toouse Olá mesmo trabalho ou escola conta que foi usada muito[instalar o gateway de dados local Olá](logic-apps-gateway-install.md#requirements). Sua conta também deve ter uma assinatura do Azure toouse quando você cria um recurso de gateway no hello portal do Azure para sua instalação do gateway.

* Sua instalação do gateway não pode já ter sido reivindicada por um recurso de gateway do Azure. Você pode associar o recurso gateway instalação tooonly um gateway do Azure. Declaração acontece quando você criar recursos de gateway Olá para que a instalação de saudação não está disponível para outros recursos.

## <a name="set-up-hello-data-gateway-connection"></a>Configurar a conexão de gateway de dados Olá

### <a name="1-install-hello-on-premises-data-gateway"></a>1. Saudação de instalar o gateway de dados local

Se você ainda não fez isso, siga Olá [gateway de dados local do etapas tooinstall Olá](logic-apps-gateway-install.md). Antes de continuar com hello outras etapas, certifique-se de que você instalou o gateway de dados de saudação em um computador local.

<a name="create-gateway-resource"></a>
### <a name="2-create-an-azure-resource-for-hello-on-premises-data-gateway"></a>2. Criar um recurso do Azure para o gateway de dados local Olá

Depois de instalar o gateway de saudação em um computador local, você deve criar o gateway de dados como um recurso no Azure. Essa etapa também associa o recurso de gateway à sua assinatura do Azure.

1. Entrar toohello [portal do Azure](https://portal.azure.com "portal do Azure"). Certifique-se de toouse Olá mesmo trabalho do Azure ou o endereço de email escolar usado tooinstall gateway de saudação.

2. No menu à esquerda do hello no Azure, escolha **novo** > **integração corporativa** > **gateway de dados no local** conforme mostrado aqui:

   ![Localize “Gateway de dados local”](./media/logic-apps-gateway-connection/find-on-premises-data-gateway.png)

3. Em Olá **criar gateway de conexão** folha, fornecer esses detalhes toocreate seu recurso de gateway de dados:

    * **Nome**: insira um nome para o recurso do gateway. 

    * **Assinatura**: selecione Olá tooassociate de assinatura do Azure com o recurso de gateway. 
    Essa assinatura deve ser Olá a mesma assinatura que seu aplicativo lógico.
   
      assinatura do saudação padrão baseia-se em Olá conta do Azure que você usou toosign no.

    * **Grupo de recursos**: crie um grupo de recursos ou selecione um grupo de recursos existente para implantar seu recurso de gateway. 
    Grupos de recursos ajudam a gerenciar os ativos do Azure relacionados como uma coleção.

    * **Local**: Azure restringe esse local toohello mesma região que foi selecionado para o serviço de nuvem do gateway Olá durante [instalação do gateway](logic-apps-gateway-install.md). 

      > [!NOTE]
      > Verifique se o local de recursos de gateway Olá corresponde local do serviço de nuvem de gateway de saudação. Caso contrário, a instalação do gateway pode não aparecer na lista de gateways de saudação instalada para você tooselect na próxima etapa do hello.
      > 
      > Você pode usar diferentes regiões para o recurso de gateway e para seu aplicativo lógico.

    * **Nome da instalação**: se a instalação do gateway não estiver selecionada, selecione gateway Olá instalada anteriormente. 

    tooadd Olá gateway recurso tooyour do painel do Azure, escolha **toodashboard Pin**. 
    Quando terminar, escolha **Criar**.

    Por exemplo:

    ![Forneça detalhes toocreate seu gateway de dados local](./media/logic-apps-gateway-connection/createblade.png)

    toofind ou exibição, o gateway de dados a qualquer momento do hello Azure esquerdo menu principal, vá muito **mais serviços** > **integração corporativa** > **dados locais Gateways**.

    ![Vá muito "Mais serviços", "Enterprise integração", "Gateways de dados no local"](./media/logic-apps-gateway-connection/find-on-premises-data-gateway-enterprise-integration.png)

<a name="connect-logic-app-gateway"></a>
### <a name="3-connect-your-logic-app-toohello-on-premises-data-gateway"></a>3. Conecte-se o gateway de dados lógica aplicativo toohello local

Agora que você criou o recurso de gateway de dados e sua assinatura do Azure associado ao recurso, crie uma conexão entre o gateway de dados de aplicativo e hello lógica.

> [!NOTE]
> Seu local de conexão do gateway deve existir no hello mesma região que seu aplicativo lógico, mas você pode usar um gateway de dados que existe em uma região diferente.

1. No hello portal do Azure, crie ou abra o aplicativo lógica no Designer de lógica do aplicativo.

2. Adicione um conector que dê suporte a conexões locais, como o SQL Server.

3. Ordem de saudação mostrado, selecione **conectar por meio do gateway de dados local**, forneça um nome de conexão exclusivo Olá informações necessárias e selecione Olá recurso de gateway de dados que você deseja toouse. Quando terminar, escolha **Criar**.

   > [!TIP]
   > Um nome de conexão exclusivo ajuda a identificar facilmente essa conexão mais tarde, especialmente quando você cria várias conexões. Se aplicável, também incluem qualificado Olá para seu nome de usuário. 

   ![Criar a conexão entre o aplicativo lógico e o gateway de dados](./media/logic-apps-gateway-connection/blankconnection.png)

Parabéns, sua conexão de gateway agora está pronto para toouse de aplicativo sua lógica.

## <a name="edit-your-gateway-connection-settings"></a>Editar as configurações da conexão do gateway

Depois de criar uma conexão de gateway para seu aplicativo lógico, talvez você queira toolater configurações de saudação de atualização para essa conexão específica.

1. conexão de gateway de saudação toofind:

   * Na folha de aplicativo de lógica de hello, em **ferramentas de desenvolvimento**, selecione **API conexões**. 
   
     Olá **API conexões** painel mostra todas as conexões de API associadas ao seu aplicativo lógica, incluindo as conexões de gateway.

     ![Vá tooyour lógica app, selecione "Conexões de API"](./media/logic-apps-gateway-connection/logic-app-find-api-connections.png)

   * Ou, no hello Azure esquerdo menu principal, vá muito **mais serviços** > **Web e serviços móveis** > **API conexões** para todas as conexões de API incluindo conexões de gateway, que estão associados com sua assinatura do Azure. 

   * Ou, em hello Azure esquerdo menu principal, vá muito**todos os recursos** para todas as conexões de API, incluindo conexões de gateway, que estão associados a sua assinatura do Azure.

2. Selecione a conexão de gateway Olá que você deseja tooview ou editar e escolha **conexão Editar API**.

   > [!TIP]
   > Se as atualizações não têm efeito, tente [interromper e reiniciar o serviço do Windows hello gateway](./logic-apps-gateway-install.md#restart-gateway).

<a name="change-delete-gateway-resource"></a>
## <a name="switch-or-delete-your-on-premises-data-gateway-resource"></a>Mudar ou excluir o recurso de gateway de dados local

toocreate um recurso de gateway diferente, associar seu gateway um recurso diferente ou remova o recurso de gateway de saudação, você poderá excluir o recurso de gateway de saudação sem afetar a instalação do gateway hello. 

1. Menu Olá principal do Azure à esquerda, vá muito**todos os recursos**. 
2. Localize e selecione seu recurso de gateway de dados.
3. Escolha **Gateway de dados no local**e na barra de ferramentas de recurso hello, escolha **excluir**.

<a name="faq"></a>
## <a name="frequently-asked-questions"></a>Perguntas frequentes

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

## <a name="next-steps"></a>Próximas etapas

* [Proteja seus aplicativos lógicos](./logic-apps-securing-a-logic-app.md)
* [Exemplos comuns e cenários de aplicativos lógicos](./logic-apps-examples-and-scenarios.md)
