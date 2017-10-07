---
title: "Portal do Azure - Gateway de aplicativo do Azure - investigação de aaaCreate um personalizado | Microsoft Docs"
description: "Saiba como toocreate um personalizado teste para o Application Gateway usando o portal de saudação"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 33fd5564-43a7-4c54-a9ec-b1235f661f97
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: 9e9309045ef33ba1010868783949b4fde31619ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-probe-for-application-gateway-by-using-hello-portal"></a>Criar uma investigação personalizada para o Application Gateway usando o portal de saudação

> [!div class="op_single_selector"]
> * [Portal do Azure](application-gateway-create-probe-portal.md)
> * [PowerShell do Azure Resource Manager](application-gateway-create-probe-ps.md)
> * [Azure Classic PowerShell](application-gateway-create-probe-classic-ps.md)

Neste artigo, adicionar um gateway de aplicativo existente do investigação personalizada tooan por meio de saudação portal do Azure. Testes personalizados são úteis para aplicativos que têm uma página de verificação de integridade específicas ou para aplicativos que não fornecem uma resposta bem-sucedida no aplicativo de web saudação padrão.

## <a name="before-you-begin"></a>Antes de começar

Se você não tiver um gateway de aplicativos, visite [criar um Application Gateway](application-gateway-create-gateway-portal.md) toocreate um toowork de gateway do aplicativo com.

## <a name="createprobe"></a>Criar a investigação de saudação

Testes são configurados em um processo de duas etapas por meio do portal hello. Olá primeira etapa é toocreate investigação de saudação. Na segunda etapa do hello, você deve adicionar configurações de http de back-end Olá investigação toohello do gateway de aplicativo hello.

1. Faça logon no toohello [portal do Azure](https://portal.azure.com). Caso você ainda não tenha uma conta, poderá se inscrever para obter uma [avaliação gratuita de um mês](https://azure.microsoft.com/free)

1. No hello portal do Azure painel Favoritos, clique em todos os recursos. Clique em Olá application gateway em Olá folha de todos os recursos. Se a assinatura de saudação selecionado já contiver vários recursos, você pode inserir partners.contoso.net Olá filtrar por nome... gateway de caixa tooeasily acesso Olá aplicativo.

1. Clique em **testes** e clique em Olá **adicionar** botão tooadd uma investigação.

  ![Folha Adicionar Investigação com as informações preenchidas][1]

1. Em Olá **investigação de integridade de adicionar** folha, preencha as informações para investigação Olá Olá necessário e quando concluir clique **Okey**.

  |**Configuração** | **Valor** | **Detalhes**|
  |---|---|---|
  |**Nome**|customProbe|Esse valor é um teste de toohello nome amigável que pode ser acessado no portal de saudação.|
  |**Protocolo**|HTTP ou HTTPS | usa o protocolo de Olá Olá investigação de integridade.|
  |**Host**|ou seja contoso.com|Esse valor é o nome de host de saudação que é usada para teste de saudação. Aplicável somente quando vários sites são configurados no Gateway de Aplicativo; do contrário, use '127.0.0.1'. Esse valor é diferente do nome de host VM hello.|
  |**Caminho**|/ ou outro caminho|Olá restante a url completa para investigação personalizada Olá Olá. Um caminho válido começa com "/". Para o caminho do saudação padrão de http://contoso.com apenas usar '/' |
  |**Intervalo (segundos)**|30|Frequência hello teste é executado toocheck de integridade. Não é recomendável tooset Olá menor do que 30 segundos.|
  |**Tempo limite (segundos)**|30|quantidade de saudação do teste de saudação do tempo espera antes do tempo limite. Olá timeout intervalo necessidades toobe alta o suficiente para que uma chamada http pode ser feita página de integridade tooensure Olá back-end está disponível.|
  |**Limite não íntegro**|3|Número de falhas toobe tentativas considerado não íntegro. Um limite de 0 significa que se uma verificação de integridade falhar Olá back-end é determinado Íntegro imediatamente.|

  > [!IMPORTANT]
  > nome do host Olá não é Olá igual ao nome do servidor. Esse valor é o nome de saudação do host virtual hello, em execução no servidor de aplicativo hello. teste de saudação é enviado toohttp: / /(host name):(port from httpsetting)/urlPath

## <a name="add-probe-toohello-gateway"></a>Adicionar teste toohello gateway

Agora que hello teste tiver sido criado, é hora tooadd-toohello gateway. Configurações de teste são definidas nas configurações de http de back-end saudação do gateway de aplicativo hello.

1. Clique em **configurações HTTP** no gateway do aplicativo hello, toobring a folha de configuração Olá clique em Olá atual back-end http configurações listadas na janela de saudação.

  ![janela de configurações de https][2]

1. Em hello **appGatewayBackEndHttpSettings** folha de configurações, Olá seleção **investigação personalizada Use** caixa de seleção e escolha investigação Olá criada no hello [criar investigação de saudação](#createprobe) seção em Olá **investigação personalizada** lista suspensa.
Ao concluir, clique em **salvar** e Olá configurações são aplicadas.

investigação de padrão de saudação verifica o aplicativo web do hello padrão acesso toohello. Agora que uma investigação personalizada tiver sido criada, o gateway de aplicativo hello usa Olá caminho personalizado definido toomonitor integridade para servidores de back-end de saudação. Com base em critérios de saudação que foi definida, gateway de aplicativo hello verifica caminho Olá especificado na investigação de saudação. Se Olá chamar toohost:Port / caminho não retorna um HTTP 200 399 resposta de status, servidor de saudação é retirada da rotação depois que o limite não íntegro Olá for atingido. Sondando continua no hello toodetermine de instância não íntegro quando ele se tornar Íntegro novamente. Depois que instância Olá for adicionada toohealthy back pool de servidores, tráfego começa a fluir tooit novamente e toohello probing instância continua no intervalo especificado de usuário normal.

## <a name="next-steps"></a>Próximas etapas

toolearn como tooconfigure descarregamento de SSL com o Gateway de aplicativo do Azure, consulte [configurar descarregamento de SSL](application-gateway-ssl-portal.md)

[1]: ./media/application-gateway-create-probe-portal/figure1.png
[2]: ./media/application-gateway-create-probe-portal/figure2.png

