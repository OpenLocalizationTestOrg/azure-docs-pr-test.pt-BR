---
title: carga aaaPre ativos em um ponto de extremidade CDN do Azure | Microsoft Docs
description: "Saiba como carga toopre armazenada em cache o conteúdo em um ponto de extremidade CDN do Azure."
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 5ea3eba5-1335-413e-9af3-3918ce608a83
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 08ac4b834f1ac8ce59d22e65fa8adea11bafcf17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="pre-load-assets-on-an-azure-cdn-endpoint"></a>Pré-carregar ativos em um ponto de extremidade da CDN do Azure
[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

Por padrão, os ativos são armazenados primeiro em cache à medida que são solicitados. Isso significa que a primeira solicitação saudação de cada região pode levar mais tempo, como servidores de borda de saudação não terá conteúdo Olá armazenadas em cache e será necessário um servidor de origem tooforward Olá solicitação toohello. O pré-carregamento de conteúdo evita essa latência de primeiro acesso.

Além disso tooproviding uma melhor experiência do cliente, pré-carregar seus ativos em cache também pode reduzir o tráfego de rede no servidor de origem de saudação.

> [!NOTE]
> Pré-carregar ativos é útil para eventos grandes ou conteúdo que se torna disponível simultaneamente tooa grande número de usuários, como uma nova versão de filme ou uma atualização de software.
> 
> 

Esse tutorial orienta você carregando previamente o conteúdo armazenado em cache em todos os nós de borda da CDN do Azure.

## <a name="walkthrough"></a>Passo a passo
1. Em Olá [Portal do Azure](https://portal.azure.com), procure o perfil CDN toohello que contém o ponto de extremidade de saudação desejar carregar toopre.  Abre a folha de perfil de saudação.
2. Clique em ponto de extremidade de saudação na lista de saudação.  Abre a folha de ponto de extremidade de saudação.
3. Na folha de ponto de extremidade CDN hello, clique botão de carga de saudação.
   
    ![Folha do ponto de extremidade da CDN](./media/cdn-preload-endpoint/cdn-endpoint-blade.png)
   
    Abre a folha de carga Hello.
   
    ![Folha de carregamento da CDN](./media/cdn-preload-endpoint/cdn-load-blade.png)
4. Digite o caminho completo da saudação de cada ativo desejar tooload (por exemplo, `/pictures/kitten.png`) no hello **caminho** caixa de texto.
   
   > [!TIP]
   > Mais **caminho** caixas de texto aparecerá depois que você inserir texto tooallow toobuild uma lista de vários ativos.  Você pode excluir ativos na lista de saudação clicando o botão de reticências (...) hello.
   > 
   > Caminhos devem ser uma URL relativa que atenda às seguintes Olá [expressão regular](https://msdn.microsoft.com/library/az24scfc.aspx):  
   > >Carregar um único caminho de arquivo `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`;  
   > >Carregar um único arquivo com a cadeia de caracteres de consulta `@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`  
   > 
   > Cada ativo deve ter seu próprio caminho.  Não há nenhuma funcionalidade de curinga para pré-carregar ativos.
   > 
   > 
   
    ![Botão Carregar](./media/cdn-preload-endpoint/cdn-load-paths.png)
5. Clique em Olá **carga** botão.
   
    ![Botão Carregar](./media/cdn-preload-endpoint/cdn-load-button.png)

> [!NOTE]
> Há uma limitação de 10 solicitações de carga por minuto para cada perfil CDN. São permitidos 50 caminhos por solicitação. Cada caminho tem um limite de comprimento de 1024 caracteres.
> 
> 

## <a name="see-also"></a>Consulte também
* [Limpar um ponto de extremidade da CDN do Azure](cdn-purge-endpoint.md)
* [Referência da API REST da CDN do Azure – limpar ou pré-carregar um ponto de extremidade](https://msdn.microsoft.com/library/mt634451.aspx)

