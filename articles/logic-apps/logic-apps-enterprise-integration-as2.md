---
title: "mensagens de aaaAS2 para a integração do enterprise B2B - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Troca de mensagens AS2 para integração corporativa B2B com Aplicativos Lógicos do Azure"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: c9b7e1a9-4791-474c-855f-988bd7bf4b7f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: LADocs; mandia
ms.openlocfilehash: 23f9d74dd0ad807e9cdaedb320d60496cfef9bc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="exchange-as2-messages-for-enterprise-integration-with-logic-apps"></a>Troca de mensagens AS2 para integração empresarial com aplicativos lógicos

Para poder trocar mensagens AS2 para Aplicativos Lógicos do Azure, você deve criar um contrato AS2 e armazená-lo em sua conta de integração. Aqui estão as etapas de saudação para contrato toocreate um AS2.

## <a name="before-you-start"></a>Antes de começar

Aqui está a itens Olá que necessários:

* Uma [conta de integração](../logic-apps/logic-apps-enterprise-integration-accounts.md) que já esteja definida e associada à sua assinatura do Azure
* Pelo menos dois [parceiros](logic-apps-enterprise-integration-partners.md) que já são definidos em sua conta de integração e configurado com um qualificador de saudação AS2 em **identidades comerciais**

> [!NOTE]
> Quando você cria um contrato, o conteúdo de Olá no arquivo do contrato de saudação deve corresponder o tipo de contrato hello.    

Depois de [criar uma conta de integração](../logic-apps/logic-apps-enterprise-integration-accounts.md) e [adicionar os parceiros](logic-apps-enterprise-integration-partners.md), você pode criar um contrato AS2 seguindo estas etapas.

## <a name="create-an-as2-agreement"></a>Criar um contrato AS2

1.  Entrar toohello [portal do Azure](http://portal.azure.com "portal do Azure").  

2.  No menu à esquerda do hello, selecione **mais serviços**. Na caixa de pesquisa hello, digite **integração** como filtro. Na lista de resultados de saudação, selecione **contas de integração**.

    > [!TIP]
    > Se você não vir **mais serviços**, você pode ter o menu de saudação tooexpand primeiro. Na parte superior de saudação do menu Olá recolhido, selecione **menu Mostrar**.

    ![Mais serviços, filtre "integração" e selecione "Contas de Integração"](./media/logic-apps-enterprise-integration-agreements/overview-1.png)

3. Em Olá **contas de integração** folha que é aberta, conta de integração hello selecione onde você deseja que o contrato de saudação toocreate.
Caso não encontre nenhuma conta de integração, [crie uma primeiro](../logic-apps/logic-apps-enterprise-integration-accounts.md "O que é uma conta de integração?").  

    ![Selecionar conta de integração Olá onde toocreate Olá contrato](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. Escolha Olá **contratos** lado a lado. Se você não tiver um bloco de contratos, primeiro adicione o bloco de saudação.

    ![Escolha o bloco de "Contratos"](./media/logic-apps-enterprise-integration-agreements/agreement-1.png)

5. Na folha de contratos de saudação é aberto, escolha **adicionar**.

    ![Escolha "Adicionar"](./media/logic-apps-enterprise-integration-agreements/agreement-2.png)

6. Em **Adicionar**, insira um **Nome** para o seu contrato. Para **Tipo de contrato**, selecione **AS2**. Selecione Olá **parceiro Host**, **identidade do Host**, **parceiro convidado**, e **convidado identidade** para o seu contrato.

    ![Fornecer detalhes de contrato](./media/logic-apps-enterprise-integration-agreements/agreement-3.png)  

    | Propriedade | Descrição |
    | --- | --- |
    | Nome |Nome do contrato de saudação |
    | Tipo de contrato | Deve ser AS2 |
    | Parceiro de Host |Um contrato precisa dos parceiros host e convidado. parceiro de host Olá representa a organização de saudação que configura o contrato de saudação. |
    | Identidade do Host |Um identificador para o parceiro de host Olá |
    | Parceiro Convidado |Um contrato precisa dos parceiros host e convidado. parceiro de convidado Olá representa a organização de saudação que está fazendo a empresa com o parceiro de host de saudação. |
    | Identidade do Convidado |Um identificador para o parceiro convidado de saudação |
    | Configurações de Recebimento |Essas propriedades se aplicam a tooall mensagens recebidas por um contrato. |
    | Configurações de Envio |Essas propriedades se aplicam a tooall mensagens enviadas por um contrato. |

## <a name="configure-how-your-agreement-handles-received-messages"></a>Configurar como seu contrato lida com mensagens recebidas

Agora que você definiu propriedades de contrato hello, você pode configurar como este contrato identifica e manipula mensagens de entrada recebidas de seu parceiro por meio deste contrato.

1.  Em **Adicionar**, selecione **Configurações de Recebimento**.
Configure essas propriedades com base no seu contrato de parceiro de saudação que troca mensagens com você. Para obter descrições de propriedade, consulte a tabela de saudação nesta seção.

    ![Configure "Configurações de recebimento"](./media/logic-apps-enterprise-integration-agreements/agreement-4.png)

2. Opcionalmente, você pode substituir as propriedades de saudação de mensagens de entrada selecionando **substituem as propriedades de mensagem**.

3. toorequire todos os toobe de mensagens de entrada conectado, selecione **mensagem deve ser assinada**. De saudação **certificado** , selecione um existente [certificado público do parceiro convidado](../logic-apps/logic-apps-enterprise-integration-certificates.md) para validar a assinatura de saudação em mensagens de saudação. Ou crie o certificado hello, se você não tiver um.

4.  toorequire todas as entrada toobe de mensagens criptografadas, selecione **mensagem deve ser criptografada**. De saudação **certificado** , selecione um existente [certificado particular do parceiro host](../logic-apps/logic-apps-enterprise-integration-certificates.md) para descriptografar as mensagens de entrada. Ou crie o certificado hello, se você não tiver um.

5. Selecione toorequire mensagens toobe compactado, **mensagem deve ser compactada**.

6. Selecione toosend uma mensagem síncrona disposição MDN (notificação) para mensagens recebidas, **enviar MDN**.

7. toosend assinado MDNs para mensagens recebidas, selecionadas **enviar MDN assinada**.

8. toosend MDNs assíncronas para mensagens recebidas, selecione **enviar MDN assíncrona**.

9. Depois de terminar, defina toosave-se de que suas configurações, escolhendo **Okey**.

Agora, o contrato é toohandle pronto entrada mensagens em conformidade tooyour configurações selecionadas.

| Propriedade | Descrição |
| --- | --- |
| Substituir as propriedades de mensagem |Indica que as propriedades nas mensagens recebidas podem ser substituídas. |
| Mensagem deve ser assinada |Requer toobe mensagens assinado digitalmente. Configure convidado Olá certificado público de parceiro para verificação de assinatura.  |
| Mensagem deve ser criptografada |Requer toobe mensagens criptografada. Mensagens não criptografadas são rejeitadas. Configure o certificado particular de parceiro do host de saudação para descriptografar mensagens de saudação.  |
| Mensagem deve ser compactada |Requer toobe mensagens compactado. Mensagens não compactadas são rejeitadas. |
| Texto MDN |saudação padrão disposição MDN (notificação) toobe toohello enviados mensagem remetente da mensagem. |
| Enviar MDN |Requer toobe MDNs enviado. |
| Enviar MDN assinada |Requer toobe MDNs assinado. |
| Algoritmo de Controle de Integridade de Credenciais |Selecione Olá algoritmo toouse para assinar mensagens. |
| Enviar MDN assíncrona | Requer toobe mensagens enviada de forma assíncrona. |
| URL | Especifique a URL de saudação onde toosend Olá MDNs. |

## <a name="configure-how-your-agreement-sends-messages"></a>Configurar como seu contrato envia mensagens

Você pode configurar como este contrato identifica e manipula mensagens de saída que você enviar tooyour parceiros por meio deste contrato.

1.  Em **Adicionar**, selecione **Configurações de Envio**.
Configure essas propriedades com base no seu contrato de parceiro de saudação que troca mensagens com você. Para obter descrições de propriedade, consulte a tabela de saudação nesta seção.

    ![Definir propriedades de "Configurações de envio" hello](./media/logic-apps-enterprise-integration-agreements/agreement-51.png)

2. parceiro de tooyour mensagens assinadas toosend, selecione **ativar a assinatura de mensagens**. Para assinar mensagens de saudação em Olá **algoritmo MIC** lista, selecione Olá *certificado particular do parceiro host algoritmo MIC*. E no hello **certificado** , selecione um existente [certificado particular do parceiro host](../logic-apps/logic-apps-enterprise-integration-certificates.md).

3. parceiro de toohello mensagens criptografadas toosend, selecione **habilitar a criptografia de mensagem**. Para criptografar mensagens de saudação em Olá **algoritmo de criptografia** lista, selecione Olá *algoritmo de certificado público do parceiro convidado*.
E no hello **certificado** , selecione um existente [certificado público do parceiro convidado](../logic-apps/logic-apps-enterprise-integration-certificates.md).

4. mensagem de saudação toocompress, selecione **habilitar a compactação de mensagem**.

5. cabeçalho de content-type toounfold Olá HTTP em uma única linha, selecione **cabeçalhos HTTP Desdobrar**.

6. tooreceive MDNs síncronas para Olá enviadas mensagens, selecionadas **solicitar MDN**.

7. tooreceive assinado MDNs para mensagens de saudação enviada, selecionadas **solicitar MDN assinada**.

8. tooreceive MDNs assíncronas para Olá enviadas mensagens, selecionadas **solicitar MDN assíncrona**. Se você selecionar essa opção, insira a URL de saudação para onde toosend Olá MDNs.

9. toorequire não-repúdio no recebimento, selecione **habilitar NRR**.  

10. Selecione toospecify algoritmo formato toouse em Olá MIC ou entrar Olá cabeçalhos de mensagem de saudação AS2 ou MDN, de saída **formato algoritmo SHA2**.  

11. Depois de terminar, defina toosave-se de que suas configurações, escolhendo **Okey**.

Agora o contrato é toohandle pronto mensagens que estão de acordo com as configurações de tooyour selecionado de saída.

| Propriedade | Descrição |
| --- | --- |
| Habilitar a assinatura de mensagens |Requer que todas as mensagens que são enviadas de saudação toobe de contrato assinado. |
| Algoritmo de Controle de Integridade de Credenciais |Olá toouse de algoritmo de assinatura de mensagens. Configura o certificado particular de parceiro host da saudação algoritmo MIC para assinatura de mensagens de saudação. |
| Certificado |Selecione Olá toouse de certificado para assinar mensagens. Configura Olá host parceiro certificado particular para assinar mensagens de saudação. |
| Habilitar a criptografia de mensagem |Exige a criptografia de todas as mensagens enviadas deste contrato. Configura o algoritmo do hello convidado parceiro certificado público para criptografar mensagens de saudação. |
| Algoritmo de Criptografia |Olá toouse de algoritmo de criptografia para criptografia de mensagens. Configura Olá convidado parceiro certificado público para criptografar mensagens de saudação. |
| Certificado |mensagens de tooencrypt toouse do certificado saudação. Configura Olá convidado parceiro certificado privada para criptografar mensagens de saudação. |
| Habilitar a compactação de mensagem |Exige a compressão de todas as mensagens enviadas deste contrato. |
| Desdobrar cabeçalhos HTTP |Coloca o cabeçalho de content-type Olá HTTP em uma única linha. |
| Solicitar MDN |Exige uma MDN de todas as mensagens enviadas deste contrato. |
| Solicitar MDN assinada |Requer que todos os MDNs que são enviadas contrato toothis toobe assinado. |
| Solicitar MDN assíncrona |Requer assíncrona MDNs toobe enviado toothis contrato. |
| URL |Especifique a URL de saudação onde toosend Olá MDNs. |
| Habilitar NRR |Requer a não-repúdio no recebimento (NRR), um atributo de comunicação que fornece evidência dados Olá foi recebida como abordado. |
| Formato de algoritmo SHA2 |Selecionar algoritmo formato toouse em Olá MIC ou entrar Olá cabeçalhos de mensagem de saudação do AS2 ou MDN de saída |

## <a name="find-your-created-agreement"></a>Como localizar seu contrato criado

1.  Depois de terminar de definir todas as suas propriedades de contrato, em Olá **adicionar** folha, escolha **Okey** toofinish criando seu contrato e retorno tooyour folha de conta de integração.

    Agora seu contrato recém-adicionado é exibido na lista **Contratos**.

2.  Você também pode visualizar seus contratos na visão geral de conta de integração. Na folha sua conta de integração, escolha **visão geral**, em seguida, selecione Olá **contratos** lado a lado. 

    ![Escolha "Contratos" bloco tooview todos os contratos](./media/logic-apps-enterprise-integration-agreements/agreement-6.png)

## <a name="view-hello-swagger"></a>Swagger de saudação do modo de exibição
Consulte Olá [swagger detalhes](/connectors/as2/). 

## <a name="next-steps"></a>Próximas etapas
* [Saiba mais sobre Olá Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Saiba mais sobre o pacote de integração do Enterprise")  
