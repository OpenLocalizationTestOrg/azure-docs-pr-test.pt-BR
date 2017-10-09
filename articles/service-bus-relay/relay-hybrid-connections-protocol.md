---
title: "as conexões de retransmissão híbridas aaaAzure protocolo guia | Microsoft Docs"
description: "Guia de protocolo de Conexões Híbridas de Retransmissão do Azure."
services: service-bus-relay
documentationcenter: na
author: clemensv
manager: timlt
editor: 
ms.assetid: 149f980c-3702-4805-8069-5321275bc3e8
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: sethm;clemensv
ms.openlocfilehash: 2d145d919d606ae4722b063e1baf39fb845a600a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# Protocolo de Conexões Híbridas de Retransmissão do Azure
Retransmissão do Azure é uma das colunas de chave de recurso Olá da plataforma do Azure Service Bus hello. Olá novo *conexões híbridas* recurso de retransmissão é uma evolução segura, protocolo aberto com base em HTTP e WebSockets. Ele substitui o antigo hello, denominado igualmente *Serviços BizTalk* recurso que foi criado em uma base de protocolo proprietário. integração de saudação de conexões híbridas em serviços de aplicativo do Azure continuará toofunction como-é.

O Conexões Híbridas possibilita uma comunicação com transmissão bidirecional binária entre dois aplicativos em rede, durante a qual um ou ambos podem residir atrás de NATs ou de firewalls. Este artigo descreve as interações de cliente Olá com retransmissão de conexões híbridas Olá para conectar clientes no ouvinte e funções de remetente e como ouvintes de aceitam novas conexões.

## Modelo de interação
retransmissão de conexões híbridas Olá conecta duas partes, fornecendo um ponto de encontro Olá nuvem do Azure que as partes podem descobrir e conexão toofrom perspectiva da sua própria rede. Esse ponto de reunião é chamado "Conexão híbrida" neste e em outras documentações, em Olá APIs e também em Olá portal do Azure. Olá conexões híbridas ponto de extremidade de serviço é chamado tooas hello "serviço" para o restante deste artigo hello. o modelo de interação Olá depende de nomenclatura Olá estabelecida por muitas APIs de rede.

Há um ouvinte que primeiro indica conexões de entrada de toohandle de preparação e subsequentemente aceitá-los assim que elas chegam. Em Olá outro lado, há uma conexão de cliente que conecta-se em direção de ouvinte hello, esperando que toobe conexão aceito para estabelecer um caminho de comunicação bidirecional.
"Conectar", "Escutar" e "Aceitar" são Olá mesmo termos localizar na maioria das APIs de soquete.

Qualquer modelo de comunicação retransmitidas tem qualquer uma das partes estabelecer conexões de saída em direção a um ponto de extremidade de serviço, o que torna ouvinte"hello" também um "cliente" em uso colloquial e também pode fazer com que outras sobrecargas de terminologia. terminologia de precisa Hello, portanto, usamos para conexões híbridas é o seguinte:

programas de saudação em ambos os lados de uma conexão são chamados de "clientes", já que eles são o serviço de toohello de clientes. cliente que espera e aceita conexões é o "ouvinte", ou é Hello disse toobe hello "ouvinte função." Olá cliente que inicia uma nova conexão para um ouvinte por meio do serviço de saudação é chamado hello "sender", ou "função de remetente".

### Interações de ouvinte
ouvinte de saudação tem quatro interações com o serviço de saudação; todos os detalhes de transmissão são descritos neste artigo na seção de referência de saudação.

#### Escutar
serviço de toohello de preparação tooindicate um ouvinte é tooaccept pronto conexões, ele cria uma conexão WebSocket saída. o handshake da conexão Olá assume o nome de saudação de uma Conexão híbrida configurada no namespace de retransmissão hello e um token de segurança que confere hello "Escutar" em que o nome.
Quando Olá WebSocket é aceita pelo serviço hello, Olá registro for concluído e Olá estabelecida web que WebSocket é mantida ativa como hello "canal de controle" para habilitar todas as interações subsequentes. serviço de saudação permite que até too25 de ouvintes simultâneos em uma Conexão híbrida. Se há dois ou mais ouvintes ativos, as conexões de entrada são balanceadas entre eles em ordem aleatória; não há garantia de distribuição justa.

#### Aceitar
Quando um remetente abre uma nova conexão no serviço hello, o serviço de saudação escolhe e notifica um dos ouvintes de active Olá em Olá Conexão híbrida. Essa notificação é enviada toohello ouvinte em canal de controle abra hello como uma mensagem JSON contendo URL de saudação do ponto de extremidade de WebSocket Olá Olá ouvinte deve se conectar toofor aceitar conexão de saudação.

Olá URL pode e deve ser usado diretamente pelo ouvinte Olá sem qualquer trabalho extra.
Olá codificado informações só é válido por um curto período de tempo, essencialmente para desde como remetente Olá é disposto toowait para Olá conexão toobe estabelecida ponta a ponta, mas o máximo de tooa de 30 segundos. Olá URL só pode ser usado para a tentativa de uma conexão bem-sucedida. Assim que hello WebSocket conexão com hello reunião de que URL é estabelecida, todas as atividades adicionais neste WebSocket é transmitida do e remetente toohello, sem qualquer intervenção ou interpretação pelo serviço de saudação.

#### Renew
token de segurança de saudação que deve ser usado tooregister ouvinte de saudação e manter que o canal de controle pode expirar enquanto ouvinte hello está ativa. expiração do token Olá não afetam as conexões em andamento, mas fazer toobe de canal de controle Olá descartado pelo serviço de saudação em ou logo após o momento de saudação da expiração. operação de "renovar" Hello é uma mensagem JSON que Olá ouvinte pode enviar token de saudação tooreplace associado ao canal de controle hello, para que hello canal de controle pode ser mantido por longos períodos.

#### Ping
Se o canal de controle Olá permanecer ocioso por um longo tempo, intermediários na forma de saudação, como carga balanceadores ou NATs podem Cancelar conexão de TCP hello. operação de "ping" Hello evita que destina-se toobe atividade enviando uma pequena quantidade de dados no canal de saudação que lembra todos na rota de rede Olá essa conexão hello e também serve como um teste "ativo" para o ouvinte de saudação. Se Olá ping falhar, o canal de controle Olá deve ser considerado inutilizável e ouvinte Olá deve se reconectar.

### Interação de remetente
remetente Olá tem apenas uma única interação com o serviço de saudação: ele se conecta.

#### Connect
operação de "conectar-se" Olá abre um WebSocket no serviço hello, fornecendo nome de saudação do hello Conexão híbrida e (opcionalmente, mas é necessário por padrão) um token de segurança conferir permissões "Enviar" na cadeia de caracteres de consulta de saudação. serviço Olá interage com o ouvinte Olá Olá forma descrita anteriormente e ouvinte Olá cria uma conexão de encontro que está associado com este WebSocket. Após aceitar Olá WebSocket, todas as outras interações em que WebSocket são com um ouvinte conectado.

### Resumo da interação
resultado de saudação desse modelo de interação é que o cliente remetente Olá sair o handshake do WebSocket "normal", que é conectado tooa ouvinte e que não precisam de nenhuma introduções adicionais ou preparação. Esse modelo permite que a praticamente qualquer existente WebSocket cliente implementação tooreadily tirar vantagem da saudação serviço conexões híbridas ao fornecer uma URL construída corretamente em sua camada de cliente do WebSocket.

Olá encontro conexão WebSocket que Olá ouvinte obtém por meio da interação de aceitar também é normal e pode ser entregue tooany WebSocket servidor implementação com alguns mínimo abstração extra que faz distinção entre "aceitar" operações em sua estrutura escutas de rede local e remoto de conexões híbridas "aceitam" operações.

## Referência de protocolo

Esta seção descreve os detalhes de saudação de interações de protocolo hello descritos anteriormente.

Todas as conexões de WebSocket são feitas na porta 443 como uma atualização do HTTPS 1.1, o que é normalmente abstraído por alguma API ou estrutura de WebSocket. A descrição aqui é mantida neutra em termos de implementação, sem sugerir uma estrutura específica.

### Protocolo de ouvinte
protocolo de ouvinte de saudação consiste em dois gestos de conexão e três operações de mensagens.

#### Conexão de canal de controle do ouvinte
canal de controle de saudação é aberto com a criação de uma conexão WebSocket para:

```
wss://{namespace-address}/$hc/{path}?sb-hc-action=...[&sb-hc-id=...]&sb-hc-token=...
```

Olá `namespace-address` é o nome de domínio totalmente qualificado de saudação do namespace do Azure retransmissão Olá hosts Olá Conexão híbrida, normalmente de forma Olá `{myname}.servicebus.windows.net`.

Opções de parâmetro de cadeia de caracteres de consulta de saudação são da seguinte maneira.

| Parâmetro | Obrigatório | Descrição |
| --- | --- | --- |
| `sb-hc-action` |Sim |Olá Olá da função de ouvinte para o parâmetro deve ser **sb-hc-action = escuta** |
| `{path}` |Sim |Olá codificados de URL do caminho da saudação pré-configurado Conexão híbrida tooregister este ouvinte no. Essa expressão é acrescentado toohello fixada `$hc/` parte do caminho. |
| `sb-hc-token` |Sim\* |Olá ouvinte deve fornecer um codificada por URL válido, serviço de barramento compartilhados Token de acesso para namespace hello ou Conexão híbrida que confere Olá **escutar** à direita. |
| `sb-hc-id` |Não |Essa ID opcional fornecida pelo cliente permite o rastreamento de diagnóstico de ponta a ponta. |

Se Olá conexão WebSocket falhar devido a caminho de Conexão híbrida toohello não está sendo registrado, ou um token inválido ou ausente ou algum outro erro, comentários de erro Olá é fornecido usando o modelo de comentários de status de HTTP 1.1 regular de hello. A descrição do status conterá uma ID de acompanhamento de erro que poderá ser comunicada ao pessoal de suporte do Azure:

| Código | Erro | Descrição |
| --- | --- | --- |
| 404 |Não encontrado |Olá Conexão híbrida caminho é inválido ou a URL base Olá está incorreta. |
| 401 |Não Autorizado |o token de segurança Hello está ausente ou malformado ou inválido. |
| 403 |Proibido |o token de segurança Olá não é válido para esse caminho para esta ação. |
| 500 |Erro Interno |Ocorreu um problema no serviço de saudação. |

Se Olá conexão WebSocket é intencionalmente desligado pelo serviço Olá depois que ele foi inicialmente configurado, motivo hello para fazer isso é comunicado usando um código de erro de protocolo WebSocket apropriado juntamente com uma mensagem de erro descritiva que também inclui um controle ID. serviço de saudação não desligará o canal de controle sem encontrar uma condição de erro. Qualquer desligamento normal é controlado de cliente.

| Status WS | Descrição |
| --- | --- |
| 1001 |caminho de Conexão híbrida Olá foi excluído ou desabilitado. |
| 1008 |token de segurança de saudação expirou, portanto a diretiva de autorização de saudação for violada. |
| 1011 |Ocorreu um problema no serviço de saudação. |

### Handshake de aceitação
Olá "aceitar" notificação é enviada pelo ouvinte de toohello serviço Olá pelo canal de controle estabelecida anteriormente como uma mensagem JSON em um quadro de texto do WebSocket. Não há nenhuma mensagem de resposta de toothis.

mensagem contém um objeto JSON denominado "aceitar", que define as seguintes propriedades no momento de saudação:

* **endereço** – Olá toobe de cadeia de caracteres de URL usada para estabelecer Olá WebSocket toothe serviço tooaccept uma conexão de entrada.
* **ID** – Olá identificador exclusivo para essa conexão. Se Olá ID foi fornecido pelo cliente do remetente Olá, é Olá remetente fornecido valor, caso contrário, será um valor gerado pelo sistema.
* **connectHeaders** – todos os cabeçalhos HTTP que foram fornecidos toohello o ponto de extremidade de retransmissão por remetente hello, que também inclui hello protocolo s-WebSocket e os cabeçalhos Sec-WebSocket-extensões.

#### Mensagem de Aceitação

```json
{                                                           
    "accept" : {
        "address" : "wss://168.61.148.205:443/$hc/{path}?..."    
        "id" : "4cb542c3-047a-4d40-a19f-bdc66441e736",  
        "connectHeaders" : {                                         
            "Host" : "...",                                                
            "Sec-WebSocket-Protocol" : "...",                              
            "Sec-WebSocket-Extensions" : "..."                             
        }                                                            
     }                                                         
}
```

Olá endereço URL fornecido no hello mensagem de JSON é usada pelo ouvinte Olá para estabelecer hello WebSocket para aceitar ou rejeitar o soquete de remetente hello.

#### Aceitar o soquete de saudação
tooaccept, o ouvinte Olá estabelece um endereço de toohello fornecido de conexão WebSocket.

Se hello "aceitar" mensagem realiza uma `Sec-WebSocket-Protocol` cabeçalho, espera-se que escuta Olá aceita apenas Olá WebSocket se ele dá suporte a esse protocolo. Além disso, ele define o cabeçalho hello como Olá que WebSocket é estabelecida.

Olá mesmo se aplica a toohello `Sec-WebSocket-Extensions` cabeçalho. Se Olá framework oferece suporte a uma extensão, ela deve definida resposta do hello cabeçalho toohello do lado do servidor de saudação necessária `Sec-WebSocket-Extensions` handshake para extensão de saudação.

Olá URL deve ser usada como-é para estabelecer Olá aceitar o soquete, mas contém os seguintes parâmetros:

| Parâmetro | Obrigatório | Descrição |
| --- | --- | --- |
| `sb-hc-action` |Sim |Para aceitar um soquete, o parâmetro hello deve ser`sb-hc-action=accept` |
| `{path}` |Sim |(consulte Olá parágrafo a seguir) |
| `sb-hc-id` |Não |Consulte a descrição anterior de **id**. |

`{path}`é Olá codificados de URL do caminho da saudação pré-configurado Conexão híbrida na qual tooregister este ouvinte. Essa expressão é acrescentado toothe fixada `$hc/` parte do caminho. 

Olá `path` expressão pode ser estendida com um sufixo e uma expressão de cadeia de caracteres de consulta que segue o nome registrado da saudação após uma barra de separação. Isso permite que Olá remetente cliente toopass expedição argumentos toohello aceitando ouvinte quando não é possível tooinclude HTTP cabeçalhos. Olá expectativa é esse ouvinte Olá framework analisa parte do caminho fixo hello e nome registrado de saudação do caminho e torna restante Olá, possivelmente sem nenhum argumento de cadeia de caracteres de consulta antecedido `sb-`, aplicativo toohello disponível para Decidindo se tooaccept Olá conexão.

Para obter mais informações, consulte hello "Remetente protocolo" a seção seguinte.

Se houver um erro, o serviço de saudação pode responder da seguinte maneira:

| Código | Erro | Descrição |
| --- | --- | --- |
| 403 |Proibido |Olá URL não é válida. |
| 500 |Erro Interno |Ocorreu um problema no serviço de saudação |

Depois que tiver sido estabelecida a conexão hello, Olá servidor é desligado Olá WebSocket ao remetente Olá WebSocket desliga, ou com hello status a seguir:

| Status WS | Descrição |
| --- | --- |
| 1001 |cliente do remetente Olá desliga conexão hello. |
| 1001 |caminho de Conexão híbrida Olá foi excluído ou desabilitado. |
| 1008 |token de segurança de saudação expirou, portanto a diretiva de autorização de saudação for violada. |
| 1011 |Ocorreu um problema no serviço de saudação. |

#### Rejeitar soquete Olá
Rejeitando soquete Olá depois inspecionando "aceitar" mensagem de saudação do requer um handshake semelhante para que hello código de status e a descrição do status de comunicação que pode fluir o motivo da rejeição da saudação fazer toohello remetente.

Escolha de design de protocolo Hello aqui é toouse um handshake WebSocket (ou seja, tooend projetado em um estado de erro definido) para que as implementações de cliente de ouvinte podem continuar toorely em um cliente do WebSocket e não é necessário utilizar um extra, bare cliente HTTP.

soquete tooreject Olá cliente Olá aceita Olá endereço URI da mensagem de saudação do "aceitar" e acrescenta dois tooit de parâmetros de cadeia de caracteres de consulta, da seguinte maneira:

| Param | Obrigatório | Descrição |
| --- | --- | --- |
| statusCode |Sim |Código de status HTTP numérico. |
| statusDescription |Sim |Motivo legível humano Olá rejeição. |

Olá que URI resultante é então usado tooestablish uma conexão WebSocket.

Ao ser concluído corretamente, esse handshake falhará intencionalmente com um código de erro HTTP 410, pois nenhum WebSocket terá sido estabelecido. Se algo der errado, Olá códigos a seguir descreve o erro hello:

| Código | Erro | Descrição |
| --- | --- | --- |
| 403 |Proibido |Olá URL não é válida. |
| 500 |Erro Interno |Ocorreu um problema no serviço de saudação. |

### Renovação de tokens do ouvinte
Quando for token de ouvinte Olá sobre tooexpire, ele pode substituí-lo, enviando um texto quadro toohello serviço por meio do canal de controle Olá estabelecida. A mensagem contém um objeto JSON chamado `renewToken`, que define Olá propriedade a seguir no momento:

* **token** – um token de acesso compartilhado do barramento do serviço válido, codificados de URL para o namespace ou a Conexão híbrida que confere Olá **escutar** à direita.

#### Mensagem renewToken

```json
{                                                                                                                                                                        
    "renewToken" : {                                                                                                                                                      
        "token" : "SharedAccessSignature sr=http%3a%2f%2fcontoso.servicebus.windows.net%2fhyco%2f&amp;sig=XXXXXXXXXX%3d&amp;se=1471633754&amp;skn=SasKeyName"  
    }                                                                                                                                                                     
}
```

Se a validação de token Olá falhar, o acesso foi negado e serviço de nuvem Olá fecha o canal de controle de saudação WebSocket com um erro. Caso contrário, não há nenhuma resposta.

| Status WS | Descrição |
| --- | --- |
| 1008 |token de segurança de saudação expirou, portanto a diretiva de autorização de saudação for violada. |

## Protocolo de remetente
protocolo de remetente de saudação é efetivamente idêntico toohello forma que um ouvinte é estabelecido.
meta de saudação é o máximo de transparência para Olá ponta a ponta WebSocket. endereço de saudação para se conectar a saudação toois que igual de ouvinte hello, mas a ação"hello" é diferente e o token precisa de uma permissão diferente:

```
wss://{namespace-address}/$hc/{path}?sb-hc-action=...&sb-hc-id=...&sbc-hc-token=...
```

Olá *endereço do namespace* é o nome de domínio totalmente qualificado de saudação do namespace do Azure retransmissão Olá hosts Olá Conexão híbrida, normalmente de forma Olá `{myname}.servicebus.windows.net`.

solicitação de saudação pode conter arbitrários cabeçalhos HTTP extras, incluindo aquelas definidas pelo aplicativo. Todos fornecido pelo ouvinte de toohello de fluxo de cabeçalhos e podem ser encontrados no hello `connectHeader` objeto do hello **aceitar** mensagem do controle.

Opções de parâmetro de cadeia de caracteres de consulta de saudação são da seguinte maneira:

| Param | Obrigatório? | Descrição |
| --- | --- | --- |
| `sb-hc-action` |Sim |Para função de remetente hello, o parâmetro hello deve ser `action=connect`. |
| `{path}` |Sim |(consulte Olá parágrafo a seguir) |
| `sb-hc-token` |Sim\* |Olá ouvinte deve fornecer um codificada por URL válido, serviço de barramento compartilhados Token de acesso para namespace hello ou Conexão híbrida que confere Olá **enviar** à direita. |
| `sb-hc-id` |Não |Uma ID opcional que permite que o rastreamento de diagnóstico de ponta a ponta e é feita ouvinte toohello disponível durante a saudação aceitar handshake. |

Olá `{path}` é Olá codificados de URL do caminho da saudação pré-configurado Conexão híbrida na qual tooregister este ouvinte. Olá `path` expressão pode ser estendida com um sufixo e um toocommunicate de expressão de cadeia de caracteres de consulta adicional. Se Olá Conexão híbrida é registrado no caminho de saudação `hyco`, Olá `path` expressão pode ser `hyco/suffix?param=value&...` seguido por parâmetros de cadeia de caracteres de consulta Olá definidos aqui. Assim, uma expressão completa pode ser da seguinte maneira:

```
wss://{namespace-address}/$hc/hyco/suffix?param=value&sb-hc-action=...[&sb-hc-id=...&]sbc-hc-token=...
```

Olá `path` expressão é passada toohello escuta no endereço Olá URI contido na mensagem de controle "aceitar" hello.

Se Olá conexão WebSocket falhar devido a caminho de Conexão híbrida toohello não está sendo registrado, um token inválido ou ausente ou algum outro erro, comentários de erro Olá é fornecido usando o modelo de comentários de status de HTTP 1.1 regular de hello. A descrição do status conterá uma ID de acompanhamento de erro que poderá ser comunicada ao pessoal de suporte do Azure:

| Código | Erro | Descrição |
| --- | --- | --- |
| 404 |Não encontrado |Olá Conexão híbrida caminho é inválido ou a URL base Olá está incorreta. |
| 401 |Não Autorizado |o token de segurança Hello está ausente ou malformado ou inválido. |
| 403 |Proibido |o token de segurança Olá não é válido para este caminho de e para esta ação. |
| 500 |Erro Interno |Ocorreu um problema no serviço de saudação. |

Se Olá conexão WebSocket intencionalmente for desligado pelo serviço Olá depois que ele foi inicialmente configurado, isso porque Olá assim é comunicado usando um código de erro de protocolo WebSocket apropriado juntamente com uma mensagem de erro descritiva que também inclui um ID de rastreamento.

| Status WS | Descrição |
| --- | --- |
| 1000 |ouvinte de saudação desligar soquete hello. |
| 1001 |caminho de Conexão híbrida Olá foi excluído ou desabilitado. |
| 1008 |token de segurança de saudação expirou, portanto a diretiva de autorização de saudação for violada. |
| 1011 |Ocorreu um problema no serviço de saudação. |

## Próximas etapas
* [Perguntas frequentes sobre retransmissão](relay-faq.md)
* [Criar um namespace](relay-create-namespace-portal.md)
* [Introdução ao .NET](relay-hybrid-connections-dotnet-get-started.md)
* [Introdução ao Node](relay-hybrid-connections-node-get-started.md)

