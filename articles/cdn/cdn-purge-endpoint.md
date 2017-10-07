---
title: aaaPurge um ponto de extremidade CDN do Azure | Microsoft Docs
description: "Saiba como toopurge todos armazenados em cache conteúdo de um ponto de extremidade CDN do Azure."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 0b50230b-fe82-4740-90aa-95d4dde8bd4f
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: a09f4a49aa1e2d7655ecae44b5126c11c28fd599
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="purge-an-azure-cdn-endpoint"></a>Limpar um ponto de extremidade da CDN do Azure
## <a name="overview"></a>Visão geral
Nós de borda do Azure CDN armazenará em cache ativos até a expiração time-to-live (TTL) do ativo Olá.  Depois TTL do ativo Olá expira, quando um cliente solicita o ativo de saudação do nó de borda hello, nó de borda hello serão recupere uma cópia atualizada de solicitação de cliente Olá ativo tooserve hello e armazenar Olá de atualização de cache.

Olá melhor prática toomake-se de que os usuários sempre obtêm cópia mais recente de saudação de seus ativos é tooversion seus ativos para cada atualização e publicação-los como novas URLs.  CDN recuperará imediatamente novos ativos Olá Olá Avançar solicitações do cliente.  Às vezes, talvez você queira toopurge armazenado em cache o conteúdo de todos os nós de borda e forçar todos os tooretrieve novos atualizado ativos.  Isso pode ser devido a aplicativo de web tooyour tooupdates ou tooquickly ativos de atualização que contenham informações incorretas.

> [!TIP]
> Observe que apenas limpeza limpa Olá armazenaram em cache o conteúdo nos servidores de borda CDN hello.  Qualquer cache downstream, como servidores proxy e caches do navegador local, ainda pode manter uma cópia armazenada em cache do arquivo hello.  É importante tooremember isso quando você define um arquivo de um tempo de vida.  Você pode forçar uma versão cliente downstream toorequest hello mais recente do arquivo, dando a ele um nome exclusivo sempre que você atualizá-lo ou aproveitando [cache de cadeia de caracteres de consulta](cdn-query-string.md).  
> 
> 

Este tutorial o orienta durante a limpeza de ativos de todos os nós de borda de um ponto de extremidade.

## <a name="walkthrough"></a>Passo a passo
1. Em Olá [Portal do Azure](https://portal.azure.com), procurar o perfil CDN toohello que contém o ponto de extremidade de saudação desejar toopurge.
2. Na folha de perfil CDN hello, clique botão de limpeza de saudação.
   
    ![Folha Perfil CDN](./media/cdn-purge-endpoint/cdn-profile-blade.png)
   
    Abre a folha de limpeza de saudação.
   
    ![Folha Limpeza da CDN](./media/cdn-purge-endpoint/cdn-purge-blade.png)
3. Em Olá Limpar folha, selecione o endereço do serviço Olá desejar toopurge na lista suspensa de URL hello.
   
    ![Formulário de limpeza](./media/cdn-purge-endpoint/cdn-purge-form.png)
   
   > [!NOTE]
   > Você também pode obter a folha de limpeza toohello clicando Olá **limpar** botão na folha de ponto de extremidade CDN hello.  Nesse caso, Olá **URL** campo será preenchido previamente com o endereço do serviço de saudação do ponto de extremidade específico.
   > 
   > 
4. Selecione quais recursos você deseja toopurge de saudação nós de borda.  Se você desejar tooclear todos os ativos, clique em Olá **Limpar tudo** caixa de seleção.  Caso contrário, caminho de saudação do tipo de cada ativo quiser toopurge Olá **caminho** caixa de texto. Abaixo formatos têm suporte no caminho de saudação.
    1. **Limpeza de URL única**: limpeza de ativos individuais, especificando a URL completa hello, com ou sem a extensão de arquivo hello, por exemplo,`/pictures/strasbourg.png`;`/pictures/strasbourg`
    2. **Limpeza de caractere curinga**: o asterisco (\*) pode ser usado como um caractere curinga. Limpar todas as pastas, subpastas e arquivos em um ponto de extremidade com `/*` Olá caminho ou limpar todas as subpastas e arquivos em uma pasta específica, especificando a pasta Olá seguida por `/*`, por exemplo,`/pictures/*`.  Observe que, no momento, a limpeza do caractere curinga não é compatível com a CDN do Azure do Akamai. 
    3. **Limpeza do domínio raiz**: limpeza de raiz de saudação do ponto de extremidade de saudação com "/" no caminho de saudação.
   
   > [!TIP]
   > Caminhos devem ser especificados para limpeza e deve ser uma URL relativa que se ajustam a seguir Olá [expressão regular](https://msdn.microsoft.com/library/az24scfc.aspx). Atualmente, **Limpar tudo** e **Limpeza de caractere curinga** não têm suporte na **CDN do Azure do Akamai**.
   > > Limpeza de URL única `@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`  
   > > Cadeia de consulta `@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`  
   > > Limpeza de caractere curinga `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`. 
   > 
   > Mais **caminho** caixas de texto aparecerá depois que você inserir texto tooallow toobuild uma lista de vários ativos.  Você pode excluir ativos na lista de saudação clicando o botão de reticências (...) hello.
   > 
5. Clique em Olá **limpar** botão.
   
    ![Botão Limpar](./media/cdn-purge-endpoint/cdn-purge-button.png)

> [!IMPORTANT]
> Limpar solicitações levar aproximadamente 2 a 3 minutos tooprocess com **CDN do Azure da Verizon** (Standard e Premium) e cerca de 7 minutos com **Azure CDN do Akamai**.  A CDN do Azure tem um limite de 50 solicitações de limpeza simultâneas por vez. 
> 
> 

## <a name="see-also"></a>Consulte também
* [Pré-carregar ativos em um ponto de extremidade da CDN do Azure](cdn-preload-endpoint.md)
* [Referência da API REST da CDN do Azure – limpar ou pré-carregar um ponto de extremidade](https://msdn.microsoft.com/library/mt634451.aspx)

