---
title: "instrução aaaSwitch para ações diferentes em aplicativos do Azure lógica | Microsoft Docs"
description: "Escolha tooperform ações diferentes em aplicativos de lógica com base nos valores de expressão, usando uma instrução switch"
services: logic-apps
keywords: "Instrução switch"
author: derek1ee
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: LADocs; deli
ms.openlocfilehash: 09ed7e4a752003aba157e9156bf4dc89ef86f5ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="perform-different-actions-in-logic-apps-with-a-switch-statement"></a>Executar diferentes ações nos aplicativos lógicos com uma instrução switch

Ao criar um fluxo de trabalho, você geralmente tem tootake ações diferentes com base no valor de saudação de um objeto ou uma expressão. Por exemplo, convém toobehave de aplicativo sua lógica diferente com base no código de status de saudação de uma solicitação HTTP, ou uma opção selecionada em um email.

Você pode usar um tooimplement de instrução switch esses cenários. Seu aplicativo lógico pode avaliar um token ou uma expressão e escolha caso Olá Olá Olá de tooexecute do mesmo valor especificado de ações. Apenas um caso deve coincidir com a instrução de comutador hello.

> [!TIP]
> Assim como ocorre em todas as linguagens de programação, as instruções switch só dão suporte a operadores de igualdade. Se precisar de outros operadores relacionais, como “maior que”, use uma instrução de condição.
> comportamento de execução determinística tooensure, casos devem conter um valor exclusivo e estático em vez de tokens dinâmicos ou uma expressão.

## <a name="prerequisites"></a>Pré-requisitos

- Uma assinatura ativa do Azure. Se você não tiver uma assinatura ativa do Azure, [criar uma conta gratuita](https://azure.microsoft.com/free/), ou tente [Aplicativos Lógicos gratuitamente](https://tryappservice.azure.com/).
- [Conhecimento básico sobre aplicativos lógicos](logic-apps-what-are-logic-apps.md)

## <a name="add-a-switch-statement-tooyour-workflow"></a>Adicionar um fluxo de trabalho de tooyour de instrução switch

tooshow como uma instrução switch funciona, este exemplo cria um aplicativo lógico monitora arquivos carregados tooDropbox. Quando novos arquivos de saudação forem carregados, o aplicativo de lógica de saudação envia aprovador tooan email escolhe se tootransfer tooSharePoint esses arquivos. aplicativo Hello usa uma instrução switch que executa ações diferentes com base no valor de Olá Olá aprovador seleciona.

1. Crie um aplicativo lógico e selecione este gatilho: **Dropbox – Quando um arquivo é criado**.

   ![Use Dropbox - quando um arquivo é criado um gatilho](./media/logic-apps-switch-case/dropbox-trigger.jpg)

2. Em gatilho hello, adicione esta ação: **Outlook.com - enviar email de aprovação**

   > [!TIP]
   > O aplicativos lógicos também dão suporte a cenários de envio de email de aprovação de uma conta do Outlook do Office 365.

   - Se você não tiver uma conexão existente, será solicitado que você toocreate um.
   - Preencha os campos de saudação necessário. Por exemplo, em **para**, especifique Olá endereço de email para enviar email do aprovador hello.
   - Em **User Options**, digite `Approve, Reject`.

   ![Configurar conexão](./media/logic-apps-switch-case/send-approval-email-action.jpg)

3. Adicione uma instrução switch.

   - Selecione **+ Nova etapa** > **... Mais** > **Adicionar um caso de opção**. 
   - Agora, desejamos tooselect Olá ação tooperform com base em Olá `SelectedOptions` de saída de hello *enviar email de aprovação* ação. 
   Você pode encontrar esse campo em Olá **adicionar conteúdo dinâmico** seletor.
   - Use *caso 1* toohandle quando seleciona aprovador Olá `Approve`.
     - Se aprovada, copie Olá original arquivo tooSharePoint Online com hello [ **SharePoint Online - criar o arquivo** ação](../connectors/connectors-create-api-sharepointonline.md).
     - Adicione outra ação no hello toonotify caso usuários que um novo arquivo está disponível no SharePoint.
   - Adicionar outro toohandle caso quando o usuário seleciona `Reject`.
     - Se rejeitada, envie um email de notificação informando outros aprovadores que arquivo hello é rejeitado e nenhuma ação adicional é necessária.
   - `SelectedOptions`fornece apenas duas opções, portanto deixarmos Olá **padrão** caso vazio.

   ![Instrução switch](./media/logic-apps-switch-case/switch.jpg)

   > [!NOTE]
   > Uma instrução switch precisa de pelo menos um caso no caso de padrão de toohello de adição.

4. Após a instrução de comutador hello, excluir Olá original arquivo carregado tooDropbox adicionando esta ação: **Dropbox - excluir arquivo**

5. Salve seu aplicativo lógico. Teste seu aplicativo carregando um arquivo tooDropbox. Em breve, você deverá receber um email de aprovação. Selecione uma opção e observar o comportamento da saudação.

   > [!TIP]
   > Check-out como muito[monitorar seus aplicativos lógicos](logic-apps-monitor-your-logic-apps.md).

## <a name="understand-hello-code-behind-switch-statements"></a>Entender o código Olá instruções switch

Agora que você criou com êxito um aplicativo lógico usando uma instrução switch, vamos dar uma olhada na definição de código Olá atrás de instrução de comutador hello.

```json
"Switch": {
    "type": "Switch",
    "expression": "@body('Send_approval_email')?['SelectedOption']",
    "cases": {
        "Case 1" : {
            "case" : "Approved",
            "actions" : {}
        },
        "Case 2" : {
            "case" : "Rejected",
            "actions" : {}
        }
    },
    "default": {
        "actions": {}
    },
    "runAfter": {
        "Send_approval_email": [
            "Succeeded"
        ]
    }
}
```

* `"Switch"`é o nome de saudação da instrução de comutador hello, que pode ser renomeado para facilitar a leitura. 
* `"type": "Switch"`indica que a ação de saudação é uma instrução switch. 
* `"expression"`é a opção selecionada do aprovador Olá neste exemplo e é avaliado em relação a cada caso declarado posteriormente na definição de saudação. 
* `"cases"` pode conter qualquer quantidade de casos. Para cada caso, `"Case *"` é nome do padrão de saudação do caso de Olá, que pode ser renomeado para facilitar a leitura. 
`"case"`Especifica o rótulo case hello, que Olá usos de expressão de switch para comparação e deve ser um valor constante e exclusivo. Se nenhum dos casos Olá correspondem a expressão de comutador hello, ações sob `"default"` são executados.

## <a name="get-help"></a>Obter ajuda

tooask perguntas, responder a perguntas e veja que outros usuários de aplicativos do Azure lógicos estão fazendo, visite Olá [Fórum de aplicativos do Azure lógica](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp aprimorar aplicativos do Azure lógica e os conectores, votar ou enviar ideias em Olá [site de comentários do usuário de aplicativos do Azure lógica](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Próximas etapas

- Saiba como muito[adicionar condições](logic-apps-use-logic-app-features.md)
- Saiba mais sobre [tratamento de erro e exceção](logic-apps-exception-handling.md)
- Descubra mais [funcionalidades da linguagem do fluxo de trabalho](logic-apps-author-definitions.md)