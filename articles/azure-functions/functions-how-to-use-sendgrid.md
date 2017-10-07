---
title: "aaaHow toouse SendGrid nas funções do Azure | Microsoft Docs"
description: "Mostra como toouse SendGrid em funções do Azure"
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 01/31/2017
ms.author: rachelap
ms.openlocfilehash: a0ffdae04e5924c773d2d26427626fc1f570f7ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-sendgrid-in-azure-functions"></a>Como toouse SendGrid em funções do Azure

## <a name="sendgrid-overview"></a>Visão geral do SendGrid

Suporte de funções do Azure SendGrid saída associações tooenable suas mensagens de email de toosend funções com algumas linhas de código e uma conta do SendGrid.

API do SendGrid toouse Olá em uma função do Azure, você deve ter uma [conta do SendGrid](http://SendGrid.com). Além disso, você deve ter uma chave de API do SendGrid. Faça logon na conta do SendGrid de tooyour e clique **configurações** , em seguida, **chave API** chave toogenerate uma API. Mantenha essa chave disponível, pois você a usará em uma etapa futura.

Agora você está pronto toocreate um aplicativo de função do Azure.

## <a name="create-an-azure-function-app"></a>Criar um Aplicativo de funções do Azure 

Aplicativos do Azure Function são contêineres para uma ou mais Azure Functions. Azure Functions são exatamente isso, uma função. Cada função do Azure é gatilho tooone associado, que é um evento que faz com que o hello função toorun.
Cada função pode conter qualquer número de associações de entrada ou saída. Associações são serviços que podem ser usados em uma função. SendGrid é uma saída de associação que você pode usar o email toosend. 

1. Faça logon no portal do Azure de toohello e [criar um aplicativo de função do Azure](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) ou abrir um aplicativo de função existente. 
2. Crie uma função do Azure. tookeep-o simples, escolha um gatilho manual e c#. 

 ![Criar uma função do Azure](./media/functions-how-to-use-sendgrid/functions-new-function-manual-trigger-page.png)

## <a name="configure-sendgrid-for-use-in-an-azure-function-app"></a>Configure o SendGrid para uso em um aplicativo de funções do Azure

Você deve armazenar sua chave de API do SendGrid como um toouse de configuração do aplicativo em uma função. campo de ApiKey Olá não é sua chave de API do SendGrid real, mas um configuração de aplicativo definir que representa a sua chave de API real. Armazenar a chave dessa maneira é para segurança, pois ela é separada de qualquer código ou arquivos que possam ser verificados no controle do código-fonte.

- Crie uma chave **AppSettings** nas **Configurações de Aplicativo** de seu aplicativo de funções.

 ![Criar uma função do Azure](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-api-key-app-settings.png)

## <a name="configure-sendgrid-output-bindings"></a>Configurar associações de saída do SendGrid

O SendGrid está disponível como uma associação de saída da função do Azure. associação de saída toocreate um SendGrid:

1. Vá toohello **integrar** guia da função Olá Olá portal do Azure.
2. Clique em **nova saída** toocreate um SendGrid associação de saída.
3. Preencha Olá **chave API** e **nome de parâmetro de mensagem** propriedades. Se desejar, você pode inserir Olá outras propriedades agora ou codificá-los em vez disso. Essas configurações podem ser usadas como padrões.

 ![Configurar associações de saída do SendGrid](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-output-bindings.png)

Adicionar uma função de tooa associação cria um arquivo chamado **function.json** na pasta da função. Esse arquivo contém todos os Olá as mesmas informações que você vê no hello da função do Azure **integrar** guia, mas o formato Json. Saudação de configuração **ApiKey**, **mensagem**, e **de** campos criaram Olá Olá entradas a seguir **function.json** arquivo: 

```json
{
  "bindings": [    
    {
      "type": "sendGrid",
      "name": "message",
      "apiKey": "SendGridKey",
      "direction": "out",
      "from": "azure@contoso.com"
    }
  ],
  "disabled": false
}
```

Se preferir, você poderá modificar esse arquivo diretamente, por conta própria.

Agora que você criou e configurou hello função de aplicativo e função, você pode escrever Olá código toosend um email.

## <a name="write-code-that-creates-and-sends-email"></a>Escrever um código que cria e envia um email

Olá API do SendGrid contém todos os Olá comandos necessário toocreate e enviar um email.  

- Substitua o código de saudação em função hello com hello código a seguir:

```cs
#r "SendGrid"
using System;
using SendGrid.Helpers.Mail;

public static void Run(TraceWriter log, string input, out Mail message)
{
    message = new Mail
    {        
        Subject = "Azure news"          
    };

    var personalization = new Personalization();
    // change tooemail of recipient
    personalization.AddTo(new Email("MoreEmailPlease@contoso.com"));   

    Content content = new Content
    {
        Type = "text/plain",
        Value = input
    };
    message.AddContent(content);
    message.AddPersonalization(personalization);
}
```

Aviso Olá primeira linha contém Olá ```#r``` diretiva que faz referência ao assembly do SendGrid hello. Depois disso, você pode usar um ```using``` instrução toomore acessar facilmente os objetos de saudação naquele namespace. No código hello, criar instâncias de ```Mail```, ```Personalization```, e ```Content``` objetos de saudação API do SendGrid que compõem o email de saudação. Quando você retorna a mensagem de saudação, SendGrid a entrega. 

Olá assinatura da função também contém um extra de parâmetro de tipo out ```Mail``` chamado ```message```. Ambas as associações de entrada e saída expressam a si mesmas como parâmetros de função no código. 

2. Teste seu código clicando **teste** e inserindo uma mensagem no hello **corpo da solicitação** campo, em seguida, clicando em Olá **executar** botão.

 ![Testar seu código](./media/functions-how-to-use-sendgrid/functions-develop-test-sendgrid.png)

3. Verificar email tooverify SendGrid enviado email hello. Ele deve ir endereço toohello no código de saudação da etapa 1 e contém a mensagem de saudação do hello **corpo da solicitação**.

## <a name="next-steps"></a>Próximas etapas
Este artigo demonstrou como toouse Olá SendGrid toocreate de serviço e enviar email. toolearn mais sobre como usar funções do Azure em seus aplicativos, consulte Olá seguintes tópicos: 

- [Práticas recomendadas para funções do Azure](functions-best-practices.md) lista alguns toouse práticas recomendada durante a criação de funções do Azure.

- [Referência do desenvolvedor do Azure Functions](functions-reference.md) Referência do programador para a codificação de funções e a definição de gatilhos e de associações.

- [Testando o Azure Functions](functions-test-a-function.md) Descreve várias ferramentas e técnicas para testar suas funções.