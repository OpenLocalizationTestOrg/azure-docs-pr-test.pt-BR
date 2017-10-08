---
title: grupo de conector aaaNo trabalho encontrado para um aplicativo de Proxy de aplicativo | Microsoft Docs
description: "Solucionar problemas que podem ocorrer quando não há nenhum trabalho conector em um grupo de conector para seu aplicativo com hello Proxy de aplicativo do Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 4c4baf296b316db131929c9a7c618fb9960713e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="no-working-connector-group-found-for-an-application-proxy-application"></a>Nenhum grupo do conector de trabalho encontrado para um aplicativo de Application Proxy

Ajuda neste artigo você tooresolve Olá comuns dos problemas enfrentados quando não há um conector detectado para um aplicativo de Proxy de aplicativo integrado ao Active Directory do Azure.

## <a name="overview-of-steps"></a>Visão geral das etapas
Se não houver nenhum trabalho conector em um grupo de conector para seu aplicativo, há alguns problemas de saudação tooresolve de maneiras:

-   Se você tiver não conectores no grupo hello, você pode:

    -   Baixar um novo conector no servidor de local certo hello e atribua-toothis grupo

    -   Mover um conector para active para grupo de saudação

-   Se você não tiver nenhum conector ativo no grupo de saudação, você pode:

    -   Identificar o motivo Olá que seu conector está inativo e resolver

    -   Mover um conector para active para grupo de saudação

tooknow qual deles é problema hello, abra o menu de "Proxy de aplicativo" hello em seu aplicativo e examine a mensagem de aviso do grupo de saudação. Ele especifica esse grupo de saudação precisa de pelo menos um conector (necessário nenhum grupo Olá) ou se ele tem nenhum conector active (embora provavelmente tem conectores inativos).

   ![Seleção de grupo do conector no Portal do Azure](./media/application-proxy-connectivity-no-working-connector/no-active-connector.png)

Para obter detalhes sobre cada uma dessas opções, consulte Olá seção correspondente. Cada uma dessas pressupõe que você esteja iniciando na página de gerenciamento de conector hello. Se você estiver procurando na mensagem de erro de saudação acima, você pode ir toothis página clicando na mensagem de saudação do aviso. Caso contrário, isso pode ser encontrado indo muito**Active Directory do Azure**, clicando em **aplicativos empresariais**, em seguida, **Proxy de aplicativo.**

   ![Gerenciamento de grupo do conector no Portal do Azure](./media/application-proxy-connectivity-no-working-connector/app-proxy.png)

## <a name="download-a-new-connector"></a>Baixar um novo conector

toodownload um novo conector, use o botão de "Baixar conector" de saudação na parte superior de saudação da página de saudação.

necessidades de conector de saudação Observação toobe instalado em um computador com o aplicativo de back-end toohello linha direta de visão e geralmente é posicionado no hello mesmo servidor que o aplicativo hello. Depois de baixar, Olá conector deve aparecer no menu. Clique Olá conector e use hello "Grupo" suspensa toomake-se de que o grupo correto toohello pertence. Salve a alteração de saudação.

   ![Baixar o conector de saudação do hello Portal do Azure](./media/application-proxy-connectivity-no-working-connector/download-connector.png)
   
## <a name="move-an-active-connector"></a>Mova um conector ativo

Se você tiver um conector para active que deve pertencer toohello grupo e tem o aplicativo de back-end de destino de toohello de linha de visão, você pode mover Olá conector no grupo Olá atribuído. toodo, clique em Olá conector. No campo de "Grupo" Olá, usar grupo correto do Olá Olá tooselect da lista suspensa e clique em Salvar.

## <a name="resolve-an-inactive-connector"></a>Resolver um conector inativo

Se hello somente conectores no grupo Olá estejam inativos, é provável que eles em um computador que não tenham todas as portas necessárias de saudação desbloqueado.

Consulte portas Olá documento de solução de problemas para obter detalhes sobre como investigar o problema.

## <a name="next-steps"></a>Próximas etapas
[Noções básicas sobre conectores de Proxy de Aplicativo do Azure AD](application-proxy-understand-connectors.md)


