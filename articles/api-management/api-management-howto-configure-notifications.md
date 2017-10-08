---
title: "notificações de aaaConfigure e email modelos no gerenciamento de API do Azure | Microsoft Docs"
description: "Saiba como tooconfigure notificações e email modelos no gerenciamento de API do Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: ee25f26d-4752-433b-af9c-3817db38aed5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: dc23289c25a1641992b73cb955099b3f207b6968
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-notifications-and-email-templates-in-azure-api-management"></a>Como notificações tooconfigure e email modelos no gerenciamento de API do Azure
Gerenciamento de API permite Olá tooconfigure notificações sobre eventos específicos e modelos de email de saudação tooconfigure que são usada toocommunicate com administradores hello e desenvolvedores de uma instância de gerenciamento de API. Este tópico mostra como as notificações tooconfigure Olá eventos disponíveis e fornece uma visão geral de como configurar modelos de email de saudação usados para esses eventos.

## <a name="publisher-notifications"> </a>Configurar notificações do editor
notificações de tooconfigure, clique em **portal do publicador** em hello Portal do Azure para seu serviço de gerenciamento de API. Isso leva toohello portal do publicador de gerenciamento de API.

![Portal do editor][api-management-management-console]

> [!NOTE] 
> Se você ainda não tiver criado uma instância do serviço de gerenciamento de API, consulte [criar uma instância do serviço de gerenciamento de API] [ Create an API Management service instance] em Olá [Introdução ao gerenciamento de API do Azure] [ Get started with Azure API Management] tutorial.

Clique em **notificações** de saudação **gerenciamento de API** menu Olá deixado tooview notificações disponíveis hello.

![Notificações do editor][api-management-publisher-notifications]

Olá lista de eventos a seguir pode ser configurada para notificações.

* **Solicitações de assinatura (que exige aprovação)** - Olá destinatários de email especificado e os usuários receberão notificações por email sobre solicitações de assinatura para exigir a aprovação de produtos de API.
* **Novas assinaturas** - Olá destinatários de email especificado e os usuários receberão notificações por email sobre novas assinaturas de produto de API.
* **Solicitações de galeria de aplicativos** - Olá destinatários de email especificado e os usuários receberão notificações por email quando novos aplicativos forem enviados toohello Galeria de aplicativos.
* **Cco** - Olá destinatários de email especificado e os usuários receberão o email com cópia oculta do toodevelopers de todos os emails enviados.
* **Novo problema ou comentário** - Olá destinatários de email especificado e os usuários receberão notificações por email quando um novo problema ou comentário é enviado no portal do desenvolvedor de saudação.
* **Mensagem de fechar conta** - Olá destinatários de email especificado e os usuários receberão notificações por email quando uma conta é fechada.
* **Próximo limite de cota de assinatura** - Olá destinatários de email a seguir e os usuários receberão notificações por email quando o uso de assinatura obtém toousage fechar cota.

Para cada evento, você pode especificar os destinatários de email usando a caixa de texto de endereço de email de saudação ou você pode selecionar os usuários de uma lista.

endereços de email do toospecify Olá toobe notificado, digite-os na caixa de texto de endereço de email de saudação. Se tiver diversos endereços de email, separe-os por vírgula.

![Destinatários da notificação][api-management-email-addresses]

toospecify Olá usuários toobe notificado, clique em **Adicionar destinatário**, Olá caixa ao lado de saudação usuários toobe notificado de seleção e clique em **Okey**.

> [!NOTE] 
> Somente os administradores são exibidos na lista de saudação.


Depois de configurar os destinatários de notificações de saudação, clique em **salvar** tooapply Olá atualizado destinatários de notificação.

> [!NOTE] 
> Se você sair Olá **publicador notificações** portal do publicador Olá guia alerta se há alterações não salvas.


## <a name="email-templates"> </a>Configurar modelos de email
Gerenciamento de API fornece modelos de email para Olá mensagens de email que são enviadas em curso de saudação de administrar e usar o serviço de saudação. Olá, modelos de email a seguir é fornecido.

* Envio à galeria de aplicativos aprovado
* Carta de despedida do desenvolvedor
* Notificação de limite de cota se aproximando
* Convidar usuário
* Novo comentário adicionado tooan problema
* Novo problema recebido
* Nova assinatura ativada
* Confirmação de renovação de assinatura
* Solicitação de assinatura negada
* Solicitação de assinatura recebida

Esses modelos podem ser modificados da forma desejada.

tooview e configurar modelos de email de saudação para sua instância de gerenciamento de API, clique em **notificações** de saudação **gerenciamento de API** menu saudação à esquerda e selecione Olá **modelos de Email**  guia.

![Modelos de email][api-management-email-templates]

tooview ou modificar um modelo específico, selecione-o da saudação **modelos** lista suspensa.

![Lista de modelos de email][api-management-email-templates-list]

Cada modelo de email tem um assunto em texto sem formatação e uma definição de corpo em formato HTML. Cada item pode ser personalizado da forma desejada.

![Editor de modelos de email][api-management-email-template]

Olá **parâmetros** lista contém uma lista de parâmetros, que, quando inserido em Olá assunto ou corpo, será o valor substituído Olá designado quando Olá email é enviado. tooinsert um parâmetro, coloque o cursor de saudação em que você deseja Olá parâmetro toogo e clique em Olá seta toohello esquerda do nome de parâmetro hello.

Clique em **visualização** ou **enviar um teste** toosee como email hello serão pesquisar ou enviar um email de teste.

> [!NOTE] 
> parâmetros de saudação não são substituídos por valores reais quando visualizar ou enviar um teste.

modelo de email do toohello toosave Olá alterações, clique em **salvar**, ou clique em alterações de saudação toocancel **Cancelar**.
 

[api-management-management-console]: ./media/api-management-howto-configure-notifications/api-management-management-console.png
[api-management-publisher-notifications]: ./media/api-management-howto-configure-notifications/api-management-publisher-notifications.png
[api-management-email-addresses]: ./media/api-management-howto-configure-notifications/api-management-email-addresses.png


[api-management-email-templates]: ./media/api-management-howto-configure-notifications/api-management-email-templates.png
[api-management-email-templates-list]: ./media/api-management-howto-configure-notifications/api-management-email-templates-list.png
[api-management-email-template]: ./media/api-management-howto-configure-notifications/api-management-email-template.png


[Configure publisher notifications]: #publisher-notifications
[Configure email templates]: #email-templates

[How toocreate and use groups]: api-management-howto-create-groups.md
[How tooassociate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
