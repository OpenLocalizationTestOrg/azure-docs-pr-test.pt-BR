---
title: aaaControl o comportamento de cache do Azure CDN com cadeias de caracteres de consulta - Premium | Microsoft Docs
description: "Controla como os arquivos são toobe armazenado em cache quando eles contêm cadeias de caracteres de consulta o cache da cadeia de consulta do Azure CDN."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 99db4a85-4f5f-431f-ac3a-69e05518c997
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 5c97cf0230ae13fd378bfce49481f3135a5ef101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings---premium"></a>Controle o comportamento do caching da CDN do Azure com cadeias de consulta - Premium
> [!div class="op_single_selector"]
> * [Standard](cdn-query-string.md)
> * [CDN Premium do Azure da Verizon](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a>Visão geral
Controla como os arquivos são toobe armazenado em cache quando eles contêm cadeias de caracteres de consulta o cache de cadeia de caracteres de consulta.

> [!IMPORTANT]
> Olá, Standard e Premium CDN produtos fornecem Olá mesma funcionalidade de cache de cadeia de caracteres de consulta, mas diferente de interface do usuário hello.  Este documento descreve a interface Olá para **Premium do Azure CDN da Verizon**.  Para o cache da cadeia de consulta com a **CDN Standard do Azure da Akamai** e a **CDN Standard do Azure da Verizon**, consulte [Controlar o comportamento de cache das solicitações CDN com cadeias de consulta](cdn-query-string.md).
> 
> 

Existem três modos disponíveis:

* **Standard-cache**: Este é o modo padrão de saudação.  nó de extremidade CDN Olá passará a cadeia de caracteres de consulta de saudação da origem do hello solicitante toohello na primeira solicitação de saudação e ativos de saudação do cache.  Todas as solicitações subsequentes para esse ativo são atendidas do nó de borda Olá ignorará a cadeia de caracteres de consulta de saudação até expira ativo em cache hello.
* **sem cache**: nesse modo, as solicitações com cadeias de caracteres de consulta não estão em cache no nó de extremidade CDN hello.  nó de borda Olá recupera ativo Olá diretamente origem hello e passa toohello solicitante com cada solicitação.
* **unique-cache**: este modo trata cada solicitação com uma cadeia de consulta como um ativo exclusivo com seu próprio cache.  Por exemplo, Olá resposta origem Olá para uma solicitação para *foo.ashx?q=bar* seria armazenado em cache no nó de borda hello e retornado para caches subsequentes com essa mesma cadeia de caracteres de consulta.  Uma solicitação para *foo.ashx?q=somethingelse* deve ser armazenado em cache como um ativo separado com seu próprio tempo toolive.

## <a name="changing-query-string-caching-settings-for-premium-cdn-profiles"></a>Alterando as configurações de cache da cadeia de consulta para perfis de CDN Premium
1. Na folha de perfil CDN hello, clique em Olá **gerenciar** botão.
   
    ![botão gerenciar da folha Perfil CDN](./media/cdn-query-string-premium/cdn-manage-btn.png)
   
    portal de gerenciamento de CDN Olá é aberto.
2. Passe o mouse sobre Olá **HTTP grande** guia, em seguida, passe o mouse sobre Olá **as configurações de Cache** flutuante.  Clique em **Cache de Cadeia de Caracteres de Consulta**.
   
    As opções de cache de cadeia de caracteres de consulta são exibidas.
   
    ![Opções de cache de cadeia de caracteres de consulta CDN](./media/cdn-query-string-premium/cdn-query-string.png)
3. Depois de fazer sua escolha, clique em Olá **atualização** botão.

> [!IMPORTANT]
> alterações de configurações de saudação não podem ser imediatamente visíveis, como demora Olá toopropagate de registro por meio de saudação CDN.  Para perfis da <b>CDN do Azure da Verizon</b>, a propagação geralmente é concluída em 90 minutos, mas em alguns casos pode levar mais tempo.
> 
> 

