---
title: "saudação de toouse aaaHow SendGrid serviço de email (Node. js) | Microsoft Docs"
description: "Saiba como enviar email com hello SendGrid serviço de email no Azure. Exemplos escritos usando Olá Node. js API de código."
services: 
documentationcenter: nodejs
author: erikre
manager: wpickett
editor: 
ms.assetid: cac444b4-26b0-45ea-9c3d-eca28d57dacb
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 01/05/2016
ms.author: erikre
ms.openlocfilehash: fd617b6aaa656e7b5dd51c51ebb0db1e848450f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosend-email-using-sendgrid-from-nodejs"></a>Como tooSend Email usando o SendGrid do Node. js
Este guia demonstra como tooperform as tarefas de programação comuns com o SendGrid email serviço no Azure. exemplos de saudação são gravados usando Olá API Node. js. Olá cenários abordados incluem **construindo email**, **enviar email**, **adicionar anexos**, **usando filtros**e **Atualizando propriedades**. Para obter mais informações sobre SendGrid e enviar email, consulte Olá [próximas etapas](#next-steps) seção.

## <a name="what-is-hello-sendgrid-email-service"></a>O que é Olá SendGrid serviço de Email?
SendGrid é um [serviço de email baseado em nuvem] que fornece uma [entrega de email transacional], escalabilidade e análise em tempo real confiáveis com APIs flexíveis que facilitam a integração personalizada. Os cenários comuns de uso do SendGrid incluem:

* Enviar automaticamente confirmações toocustomers
* Administração de listas de distribuição para enviar aos clientes mensalmente panfletos eletrônicos e ofertas especiais
* Coleta de métrica em tempo real para, por exemplo, email bloqueado e capacidade de resposta do cliente
* Gerando relatórios toohelp identificar tendências
* Encaminhamento de consultas dos clientes
* Notificações de email de seu aplicativo

Para obter mais informações, consulte [https://sendgrid.com](https://sendgrid.com).

## <a name="create-a-sendgrid-account"></a>Criar uma conta do SendGrid
[!INCLUDE [sendgrid-sign-up](../includes/sendgrid-sign-up.md)]

## <a name="reference-hello-sendgrid-nodejs-module"></a>Saudação de referência módulo de Node.js do SendGrid
módulo do SendGrid Olá para Node. js pode ser instalado por meio do Gerenciador de pacotes de nó de saudação (npm) usando o comando a seguir de saudação:

    npm install sendgrid

Após a instalação, você pode exigir o módulo Olá em seu aplicativo usando Olá código a seguir:

    var sendgrid = require('sendgrid')(sendgrid_username, sendgrid_password);

módulo do SendGrid Olá exporta Olá **SendGrid** e **Email** funções.
**SendGrid** é responsável por enviar email por meio da API da Web, enquanto **Email** encapsula uma mensagem de email.

## <a name="how-to-create-an-email"></a>Como: criar um email
Criando uma mensagem de email usando o módulo de SendGrid Olá envolve criar primeiro uma mensagem de email usando a função de Email hello e, em seguida, enviá-lo usando a função do SendGrid hello. a seguir Olá é um exemplo de como criar uma nova mensagem usando a função de Email hello:

    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

Você também pode especificar uma mensagem de HTML para clientes que dão suporte a ele definindo a propriedade de html hello. Por exemplo:

    html: This is a sample <b>HTML<b> email message.

Definir as propriedades de texto e html Olá fornece normal fallback para conteúdo de texto para clientes que não oferece suporte a mensagens em HTML.

Para obter mais informações sobre todas as propriedades com suporte pelo Olá função Email, consulte [sendgrid nodejs][sendgrid-nodejs].

## <a name="how-to-send-an-email"></a>Como: enviar um email
Depois de criar uma mensagem de email usando Olá função de Email, você pode enviar usando Olá Web API fornecida pelo SendGrid. 

### <a name="web-api"></a>API Web
    sendgrid.send(email, function(err, json){
        if(err) { return console.error(err); }
        console.log(json);
    });

> [!NOTE]
> Enquanto Olá acima exemplos mostram passagem em uma função de retorno de chamada e de objeto de email, você também diretamente pode chamar a função de envio de saudação especificando diretamente as propriedades de email. Por exemplo:  
> 
> `````
> sendgrid.send({
> to: 'john@contoso.com',
> from: 'anna@contoso.com',
> subject: 'test mail',
> text: 'This is a sample email message.'
> });
> `````
> 
> 

## <a name="how-to-add-an-attachment"></a>Como: adicionar um anexo
Anexos podem ser adicionados a mensagem tooa, especificando nomes de arquivo hello e caminhos Olá **arquivos** propriedade. saudação de exemplo a seguir demonstra enviando um anexo:

    sendgrid.send({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.',
        files: [
            {
                filename:     '',           // required only if file.content is used.
                contentType:  '',           // optional
                cid:          '',           // optional, used toospecify cid for inline content
                path:         '',           //
                url:          '',           // == One of these three options is required
                content:      ('' | Buffer) //
            }
        ],
    });

> [!NOTE]
> Ao usar o hello **arquivos** propriedade, o arquivo hello deve ser acessível por meio de [fs.readFile](http://nodejs.org/docs/v0.6.7/api/fs.html#fs.readFile). Se o arquivo hello desejar tooattach estiver hospedado no armazenamento do Azure, como em um contêiner de Blob, é necessário primeiro copiar armazenamento de toolocal arquivo hello ou tooan unidade do Azure antes de ser enviado como um anexo usando Olá **arquivos** propriedade.
> 
> 

## <a name="how-to-use-filters-tooenable-footers-and-tracking"></a>Como: usar filtros tooEnable rodapés e controle
SendGrid fornece a funcionalidade de email adicionais por meio do uso de saudação de filtros. Essas são as configurações que podem ser adicionadas tooan a mensagem de email para habilitar a funcionalidade específica, como habilitar o controle de clique, do Google analytics, assinatura de controle, e assim por diante. Para obter uma lista completa de filtros, consulte [Configurações de filtro][Filter Settings].

Os filtros podem ser aplicadas tooa mensagem usando Olá **filtros** propriedade.
Cada filtro é especificado por um hash que possui configurações específicas de filtro.
Olá exemplos a seguir demonstram o rodapé hello e clique em filtros de rastreamento:

### <a name="footer"></a>Rodapé
    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

    email.setFilters({
        'footer': {
            'settings': {
                'enable': 1,
                'text/plain': 'This is a text footer.'
            }
        }
    });

    sendgrid.send(email);

### <a name="click-tracking"></a>Acompanhamento de cliques
    var email = new sendgrid.Email({
        to: 'john@contoso.com',
        from: 'anna@contoso.com',
        subject: 'test mail',
        text: 'This is a sample email message.'
    });

    email.setFilters({
        'clicktrack': {
            'settings': {
                'enable': 1
            }
        }
    });

    sendgrid.send(email);

## <a name="how-to-update-email-properties"></a>Como atualizar as propriedades do e-mail
Algumas propriedades de email podem ser substituídas usando  **definir*propriedade** * ou ser acrescentados usando  **adicionar*propriedade** *. Por exemplo, você pode adicionar destinatários adicionais ao usar

    email.addTo('jeff@contoso.com');

ou definir um filtro usando

    email.addFilter('footer', 'enable', 1);
    email.addFilter('footer', 'text/html', '<strong>boo</strong>');

Para obter mais informações, consulte [sendgrid nodejs][sendgrid-nodejs].

## <a name="how-to-use-additional-sendgrid-services"></a>Como: usar serviços adicionais do SendGrid
SendGrid oferece APIs baseado na web que você pode usar uma funcionalidade adicional tooleverage SendGrid de seu aplicativo do Azure. Para obter detalhes completos, consulte Olá [documentação da API do SendGrid][SendGrid API documentation].

## <a name="next-steps"></a>Próximas etapas
Agora que você aprendeu as Noções básicas sobre Olá Olá serviço de Email do SendGrid, siga essas toolearn links mais.

* Repositório de módulo de Node.js do SendGrid: [sendgrid nodejs][sendgrid-nodejs]
* Documentação da API do SendGrid: <https://sendgrid.com/docs>
* Oferta especial de SendGrid para clientes Azure: [http://sendgrid.com/azure.html](https://sendgrid.com/windowsazure.html)

[special offer]: https://sendgrid.com/windowsazure.html
[sendgrid-nodejs]: https://github.com/sendgrid/sendgrid-nodejs
[Filter Settings]: https://sendgrid.com/docs/API_Reference/SMTP_API/apps.html
[SendGrid API documentation]: https://sendgrid.com/docs
[serviço de email baseado em nuvem]: https://sendgrid.com/email-solutions
[entrega de email transacional]: https://sendgrid.com/transactional-email
