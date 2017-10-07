---
title: aaaTemplates
description: "Este tópico explica os modelos de hubs de notificação do Azure."
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: a41897bb-5b4b-48b2-bfd5-2e3c65edc37e
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: multiple
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 0149f0c7473e5a4b952905bc8217582b58db2a0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="templates"></a>Modelos
## <a name="overview"></a>Visão geral
Os modelos permitem a um cliente aplicativo toospecify Olá formato exato das notificações de saudação que ele deseja tooreceive. Usando modelos, um aplicativo pode obter várias vantagens, incluindo Olá seguinte:

* Um back-end independente de plataforma
* Notificações personalizadas
* Independência da versão do cliente
* Localização fácil

Esta seção fornece dois exemplos detalhados de como as notificações de independente de plataforma toosend modelos toouse direcionamento todos os seus dispositivos em plataformas e toopersonalize difusão tooeach de dispositivo de notificação.

## <a name="using-templates-cross-platform"></a>Como usar modelos de plataforma cruzada
as notificações por push do Hello maneira padrão toosend é toosend, para cada notificação é enviada, de toobe serviços de notificação de tooplatform uma carga específica (WNS, APNS). Por exemplo, toosend tooAPNS um alerta, a carga de saudação é um objeto Json de saudação formulário a seguir:

    {"aps": {"alert" : "Hello!" }}

toosend uma mensagem de notificação do sistema semelhante em um aplicativo da Windows Store, Olá XML carga é da seguinte maneira:

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">Hello!</text>
        </binding>
      </visual>
    </toast>

Você pode criar cargas similares para MPNS (Windows Phone) e para plataformas de GCM (Android).

Esse requisito força Olá aplicativo back-end tooproduce diferentes cargas para cada plataforma e efetivamente faz Olá back-end responsável por parte da camada de apresentação de saudação do aplicativo hello. Algumas questões incluem a localização e layouts gráficos (especialmente para aplicativos da Windows Store que englobam notificações para vários tipos de blocos).

recurso de modelo de Hubs de notificação de Olá permite que um aplicativo toocreate especiais registros de clientes, chamado de registros do modelo, que incluem, além de toohello conjunto de marcas, um modelo. recurso de modelo do Hello Hubs de notificação permite que um dispositivo de tooassociate do aplicativo cliente com modelos se você estiver trabalhando com instalações (preferidas) ou registros. Considerando Olá anterior exemplos de carga, hello apenas informações de independente de plataforma são Olá real alerta mensagem (Olá!). Um modelo é um conjunto de instruções para Olá Hub de notificação em como tooformat um independente de plataforma de mensagens para o registro de saudação do que o aplicativo cliente específico. Olá anterior de exemplo, mensagem independente de plataforma de saudação é uma propriedade única: **mensagem = Olá!**.

Olá figura abaixo ilustra Olá acima do processo:

![](./media/notification-hubs-templates/notification-hubs-hello.png)

modelo de saudação para o registro do aplicativo cliente Olá iOS é o seguinte:

    {"aps": {"alert": "$(message)"}}

saudação de modelo correspondente para o aplicativo de cliente de armazenamento do Windows hello é:

    <toast>
        <visual>
            <binding template=\"ToastText01\">
                <text id=\"1\">$(message)</text>
            </binding>
        </visual>
    </toast>

Observe que Olá mensagem real é substituído Olá expressão $(mensagem). Essa expressão instrui Olá Hub de notificação, sempre que ele envia uma mensagem toothis registro específico, toobuild uma mensagem que segue a ele e comutadores no valor comum hello.

Se você estiver trabalhando com o modelo de instalação, chave de "modelos" hello instalação contém um JSON de vários modelos. Se você estiver trabalhando com o modelo de registro, aplicativo de cliente hello pode criar vários registros em ordem toouse vários modelos; Por exemplo, um modelo para mensagens de alerta e um modelo para atualizações de bloco. Os aplicativos clientes também podem mesclar registros nativos (registros sem um modelo) e registros de modelo.

Olá Hub de notificação envia uma notificação para cada modelo sem considerar se eles pertencem toohello mesmo aplicativo de cliente. Esse comportamento pode ser usado tootranslate independente de plataforma notificações para notificações de mais. Por exemplo, Olá mesmo toohello mensagem independente de plataforma que hub de notificação podem ser convertido diretamente em um alerta de notificação do sistema e uma atualização de bloco, sem a necessidade de toobe de back-end Olá ciente dela. Observe que algumas plataformas (por exemplo, iOS) podem recolher várias toohello de notificações mesmo dispositivo, caso sejam enviadas em um curto período de tempo.

## <a name="using-templates-for-personalization"></a>Como usar modelos para personalização
Modelos de toousing outra vantagem é Olá capacidade toouse personalização de por registro tooperform Hubs de notificação de notificações. Por exemplo, considere um aplicativo de tempo que exibe um bloco com condições de tempo de saudação em um local específico. Um usuário pode escolher entre graus Celsius ou Fahrenheit e uma previsão única ou de cinco dias. Usando modelos, cada instalação do aplicativo cliente pode se registrar no formato Olá necessário (1 dia Celsius, 1 dia Fahrenheit, 5 dias Celsius, 5 dias Fahrenheit), e ter Olá back-end enviar uma mensagem única que contém todas as informações de saudação necessária toofill aqueles modelos (por exemplo, um cinco dias de previsão com graus Celsius e Fahrenheit).

modelo de Olá Olá um dia de previsão com Celsius temperaturas é o seguinte:

    <tile>
      <visual>
        <binding template="TileWideSmallImageAndText04">
          <image id="1" src="$(day1_image)" alt="alt text"/>
          <text id="1">Seattle, WA</text>
          <text id="2">$(day1_tempC)</text>
        </binding>  
      </visual>
    </tile>

Olá mensagem enviada toohello Hub de notificação contém Olá todas as propriedades a seguir:

<table border="1">

<tr><td>day1_image</td><td>day2_image</td><td>day3_image</td><td>day4_image</td><td>day5_image</td></tr>

<tr><td>day1_tempC</td><td>day2_tempC</td><td>day3_tempC</td><td>day4_tempC</td><td>day5_tempC</td></tr>

<tr><td>day1_tempF</td><td>day2_tempF</td><td>day3_tempF</td><td>day4_tempF</td><td>day5_tempF</td></tr>
</table><br/>

Usando esse padrão, Olá back-end apenas envia uma única mensagem sem ter que opções de personalização específicas de toostore para os usuários do aplicativo hello. Olá a imagem a seguir ilustra esse cenário:

![](./media/notification-hubs-templates/notification-hubs-registration-specific.png)

## <a name="how-tooregister-templates"></a>Como modelos de tooregister
tooregister com modelos usando o modelo de instalação de saudação (preferencial) ou Olá modelo de registro, consulte [Registration Management](notification-hubs-push-notification-registration-management.md).

## <a name="template-expression-language"></a>Linguagem de expressão do modelo
Os modelos são tooXML limitado ou formatos de documentos JSON. Além disso, só é possível usar expressões em determinados locais. Por exemplo, os atributos de nó ou valores para XML, cadeia de valores de propriedade para JSON.

Olá tabela a seguir mostra idioma Olá permitido em modelos:

| Expression | Descrição |
| --- | --- |
| $(prop) |Propriedade de evento de tooan de referência com hello determinado nome. Os nomes de propriedade não diferenciam maiúsculas de minúsculas. Essa expressão é resolvida no valor de texto da propriedade hello ou em uma cadeia de caracteres vazia se não houver propriedade Olá. |
| $(prop, n) |Como acima, mas hello texto é explicitamente recortado n caracteres, por exemplo $(título, 20) recorta conteúdo de saudação da propriedade de título de saudação em 20 caracteres. |
| .(prop, n) |Como acima, mas hello texto é com o sufixo três pontos conforme ele é anexado. tamanho total de saudação do hello recortado cadeia de caracteres e sufixo Olá não exceda n caracteres. . (título, 20) com uma propriedade de entrada de "Esta é a linha de título do hello" resulta em **este é o título de saudação...** |
| %(prop) |Too$(name) semelhante, exceto por essa saída Olá URI codificado. |
| #(prop) |Usada em modelos JSON (por exemplo, para modelos iOS e Android).<br><br>Essa função funciona exatamente iguais Olá como $(prop) especificado anteriormente, exceto quando usado em modelos JSON (por exemplo, modelos de Apple). Nesse caso, se essa função não é delimitada por "{','}" (por exemplo, 'myJsonProperty': '#(nome)'), e ele será avaliado tooa número no formato de Javascript, por exemplo, regexp: (0 &#124;) (&#91; 1-9 &#93; &#91; 0-9 & #93 ;*))(\. &#91; 0-9 &#93; +)? ((e &#124; E) (+ &#124;-)? &#91; 0-9 &#93; +)?, em seguida, Olá saída JSON é um número.<br><br>Por exemplo, ‘badge : ‘#(name)’se torna 'badge': 40 (e não ‘40‘). |
| 'texto' ou "texto" |Um literal. Literais contêm texto arbitrário entre aspas simples ou duplas. |
| expr1 + expr2 |operador de concatenação de saudação unindo duas expressões em uma única cadeia de caracteres. |

expressões de saudação podem ser qualquer Olá anterior formulários.

Ao usar a concatenação, toda a expressão Olá deve estar entre {}. Por exemplo, {$(prop) + “ - ” + $(prop2)}. |

Por exemplo, o seguinte Olá não é um modelo XML válido:

    <tile>
      <visual>
        <binding $(property)>
          <text id="1">Seattle, WA</text>
        </binding>  
      </visual>
    </tile>


Como explicado acima, ao usar concatenação, as expressões devem ser colocadas entre colchetes. Por exemplo:

    <tile>
      <visual>
        <binding template="ToastText01">
          <text id="1">{'Hi, ' + $(name)}</text>
        </binding>  
      </visual>
    </tile>

