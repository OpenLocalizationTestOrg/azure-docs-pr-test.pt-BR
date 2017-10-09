---
title: "código de aaaCustom para aplicativos do Azure lógica com funções do Azure | Microsoft Docs"
description: "Criar e executar código personalizado para Aplicativo Lógico do Azure com o Azure Functions"
services: logic-apps,functions
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 9fab1050-cfbc-4a8b-b1b3-5531bee92856
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 18b3821ed7e434feb568b9b96e9a5a2189dba3bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-and-run-custom-code-for-logic-apps-through-azure-functions"></a>Adicionar e executar código personalizado para aplicativos lógicos por meio do Azure Functions

toorun personalizado trechos de código do c# ou Node. js em aplicativos lógicos, você pode criar funções personalizadas por meio das funções do Azure. 
O [Azure Functions](../azure-functions/functions-overview.md) oferece uma computação sem servidor no Microsoft Azure e é útil para realizar estas tarefas:

* Formatação avançada ou computação de campos em um aplicativos lógicos
* Execute cálculos em um fluxo de trabalho.
* Estender a funcionalidade do aplicativo hello lógica com funções que têm suporte em c# ou Node. js

## <a name="create-custom-functions-for-your-logic-apps"></a>Criar funções personalizadas para aplicativos lógicos

É recomendável que você crie uma função no portal do Azure funções hello, de saudação **Webhook genérico - nó** ou **Webhook genérico - C#** modelos. resultado de saudação cria um preenchido automaticamente de um modelo que aceita `application/json` de um aplicativo lógico. Funções que você cria com esses modelos são detectadas automaticamente e aparecer em Olá lógica Designer do aplicativo em **funções do Azure em minha região.**

Em Olá portal do Azure, Olá **integrar** painel para sua função, o modelo deve mostrar que **modo** definido muito**Webhook** e **Webhook tipo** está definido muito**JSON genérico**. 

Funções de Webhook aceitar uma solicitação e passá-lo no método hello por meio de um `data` variável. Você pode acessar as propriedades de saudação da carga usando a notação como `data.function-name`. Por exemplo, uma função JavaScript simples que converte um valor DateTime em uma cadeia de caracteres de data aparência Olá exemplo a seguir:

```
function start(req, res){
    var data = req.body;
    res = {
        body: data.date.ToDateString();
    }
}
```

## <a name="call-azure-functions-from-logic-apps"></a>Chamar o Azure Functions de aplicativos lógicos

contêineres de saudação toolist em sua assinatura e a função hello selecione que você deseja toocall, no Designer de lógica de aplicativo, clique em Olá **ações** menu e selecione uma das **funções do Azure em minha região**.

Depois de selecionar a função hello, será solicitado toospecify um objeto de carga de entrada. Este objeto é uma mensagem de saudação Olá lógica aplicativo envia toohello função e deve ser um objeto JSON. Por exemplo, se você quiser toopass em Olá **última modificação** data de um disparador da equipe de vendas, carga de função hello pode parecer semelhante a este exemplo:

![Data da última modificação][1]

## <a name="trigger-logic-apps-from-a-function"></a>Disparar aplicativos lógicos a partir de uma função

Você pode disparar um aplicativo lógico de dentro de uma função. Constule [Aplicativos lógicos como pontos de extremidade escaláveis](logic-apps-http-endpoint.md). Criar um aplicativo de lógica que tem um gatilho manual, em seguida, de dentro de sua função, gerar uma URL de gatilho manual toohello HTTP POST com carga Olá que quer enviar toohello lógica aplicativo.

### <a name="create-a-function-from-logic-app-designer"></a>Criar uma função do Designer de Aplicativos Lógicos

Você também pode criar uma função de webhook Node. js do designer de saudação. Primeiro, selecione **Azure Functions em minha região** , em seguida, escolha um contêiner de sua função. Se você ainda não tiver um contêiner, você precisa toocreate de saudação [portal do Azure funções](https://functions.azure.com/signin). Em seguida, selecione **Criar Novo**.  

toogenerate um modelo com base em dados de saudação que você deseja toocompute, especifique o objeto de contexto de saudação que você planeje toopass em uma função. Esse objeto deve ser um objeto JSON. Por exemplo, se você passar no conteúdo do arquivo hello de uma ação de FTP, carga de contexto de saudação é semelhante a este exemplo:

![Conteúdo do contexto][2]

> [!NOTE]
> Porque esse objeto não foi convertido como uma cadeia de caracteres, o conteúdo de saudação é adicionado diretamente toohello carga JSON. No entanto, ocorrerá um erro se o objeto de saudação não é um token JSON (ou seja, uma cadeia de caracteres ou JSON/matriz object). objeto de saudação toocast como uma cadeia de caracteres, adicionar aspas, conforme mostrado na primeira ilustração Olá neste artigo.
> 

designer de Hello, em seguida, gera um modelo de função que você pode criar embutido. Variáveis são previamente criadas com base no contexto de saudação que você planeje toopass em função hello.

<!--Image references-->
[1]: ./media/logic-apps-azure-functions/callfunction.png
[2]: ./media/logic-apps-azure-functions/createfunction.png
