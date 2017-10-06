---
title: "aaaIssuer nome e chave do emissor nos Serviços BizTalk | Microsoft Docs"
description: "Saiba como o nome do emissor tooretrieve e chave do emissor de barramento de serviço ou controle de acesso (ACS) nos Serviços BizTalk. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 067fe356-d1aa-420f-b2f2-1a418686470a
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: cc84c2820724ae3e7fc7c40ddbcd83a169add911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-issuer-name-and-issuer-key"></a>Serviços BizTalk: nome e chave do emissor

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Serviços BizTalk do Azure usa Olá nome do emissor de barramento de serviço e chave do emissor, Olá nome do emissor de controle de acesso e chave do emissor. Especificamente:

| Tarefa | Qual nome e chave do emissor |
| --- | --- |
| Implantando seu aplicativo do Visual Studio |Nome e chave do emissor do Controle de Acesso |
| Configurando Olá Portal de Serviços BizTalk do Azure |Nome e chave do emissor do Controle de Acesso |
| Criar retransmissões de LOB com hello serviços de adaptador do BizTalk no Visual Studio |Nome e chave do emissor do Service Bus |

Este tópico lista Olá etapas tooretrieve Olá nome do emissor e chave do emissor. 

## <a name="access-control-issuer-name-and-issuer-key"></a>Nome e chave do emissor do Controle de Acesso
Olá, nome do emissor de controle de acesso e a chave do emissor são usados pelo seguinte hello:

* Seu aplicativo de serviço BizTalk do Azure criado no Visual Studio: toosuccessfully implantar seu aplicativo do BizTalk Service no Visual Studio tooAzure, digite hello nome do emissor de controle de acesso e a chave do emissor. 
* Olá Portal de Serviços BizTalk do Azure: quando você cria um BizTalk Service e abre Olá Portal de serviços do BizTalk, o nome do emissor de controle de acesso e a chave do emissor são registradas automaticamente para implantações com hello os mesmos valores de controle de acesso.

### <a name="get-hello-access-control-issuer-name-and-issuer-key"></a>Obter Olá nome do emissor de controle de acesso e a chave do emissor

ACS toouse para autenticação e get hello valores do nome do emissor e chave do emissor, hello etapas gerais incluem:

1. Instalar Olá [cmdlets do Powershell do Azure](https://azure.microsoft.com/documentation/articles/powershell-install-configure/).
2. Adicionar sua conta do Azure: `Add-AzureAccount`
3. Retornar o nome da sua assinatura: `get-azuresubscription`
4. Selecionar sua assinatura: `select-azuresubscription <name of your subscription>` 
5. Criar um novo namespace: `new-azuresbnamespace <name for hello service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`

    Exemplo:`new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`
      
5. Quando Olá novo namespace do ACS é criado (o que pode levar vários minutos), os valores de nome do emissor e chave do emissor Olá são listados na cadeia de caracteres de conexão de saudação: 

    ```
    Name                  : biztalksbnamespace
    Region                : South Central US
    DefaultKey            : abcdefghijklmnopqrstuvwxyz
    Status                : Active
    CreatedAt             : 10/18/2016 9:36:30 PM
    AcsManagementEndpoint : https://biztalksbnamespace-sb.accesscontrol.windows.net/
    ServiceBusEndpoint    : https://biztalksbnamespace.servicebus.windows.net/
    ConnectionString      : Endpoint=sb://biztalksbnamespace.servicebus.windows.net/;SharedSecretIssuer=owner;SharedSecretValue=abcdefghijklmnopqrstuvwxyz
    NamespaceType         : Messaging
    ```

toosummarize:  
Nome do Emissor = SharedSecretIssuer  
Chave do Emissor = SharedSecretKey

Mais informações sobre Olá [New-AzureSBNamespace](https://msdn.microsoft.com/library/dn495165.aspx) cmdlet. 

## <a name="service-bus-issuer-name-and-issuer-key"></a>Nome e chave do emissor do Service Bus
O nome e a chave do emissor do Barramento de Serviço são usados pelos Serviços do Adaptador do BizTalk. No seu projeto de Serviços BizTalk no Visual Studio, você usar o sistema de linha de negócios (LOB) do hello serviços de adaptador do BizTalk tooconnect tooan local. tooconnect, criar hello retransmissão LOB e insira os detalhes do sistema LOB. Ao fazer isso, você também inserir hello nome do emissor de barramento de serviço e a chave do emissor.

### <a name="tooretrieve-hello-service-bus-issuer-name-and-issuer-key"></a>Olá tooretrieve nome do emissor de barramento de serviço e a chave do emissor
1. Entrar toohello [portal clássico do Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. No painel de navegação esquerdo hello, selecione **barramento de serviço**.
3. Selecione seu namespace. Na barra de tarefas hello, selecione **informações de Conexão**. Isso exibe o saudação **emissor padrão** (nome do emissor) e **chave padrão** (chave de emissor). Os valores podem ser copiados.  

toosummarize:  
Nome do Emissor = Emissor Padrão  
Chave do Emissor = Chave Padrão

## <a name="next"></a>Avançar
Tópicos adicionais dos Serviços BizTalk do Azure:

* [Instalando Olá SDK dos Serviços BizTalk do Azure](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [Tutoriais: Serviços BizTalk do Azure](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [Como posso começar a usar Olá SDK dos Serviços BizTalk do Azure](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [Serviços BizTalk do Azure](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a>Consulte também
* [Como: usar serviço de gerenciamento de ACS tooConfigure identidades de serviço](http://go.microsoft.com/fwlink/p/?LinkID=303942)<br/>
* [Serviços BizTalk: gráfico das edições Developer, Basic, Standard e Premium](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [Serviços BizTalk: provisionamento usando o portal clássico do Azure](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [Serviços BizTalk: gráfico do status do provisionamento](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [Serviços BizTalk: guias Painel, Monitor e Escala](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [Serviços BizTalk: backup e restauração](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [Serviços BizTalk: limitação](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>

