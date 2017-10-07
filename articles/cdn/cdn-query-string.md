---
title: comportamento do cache da CDN do Azure com cadeias de caracteres de consulta de aaaControl | Microsoft Docs
description: "Controla como os arquivos são toobe armazenado em cache quando eles contêm cadeias de caracteres de consulta o cache da cadeia de consulta do Azure CDN."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 17410e4f-130e-489c-834e-7ca6d6f9778d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: e7a138b2decec624a29eb703ad9a291d19c44ee8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings"></a>Controlando o comportamento de cache da CDN do Azure com cadeias de consulta
> [!div class="op_single_selector"]
> * [Standard](cdn-query-string.md)
> * [CDN Premium do Azure da Verizon](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a>Visão geral
Controla como os arquivos são toobe armazenado em cache quando eles contêm cadeias de caracteres de consulta o cache de cadeia de caracteres de consulta.

> [!IMPORTANT]
> Olá, Standard e Premium CDN produtos fornecem Olá mesma funcionalidade de cache de cadeia de caracteres de consulta, mas diferente de interface do usuário hello.  Este documento descreve a interface Olá para **padrão do Azure CDN do Akamai** e **Azure CDN padrão da Verizon**.  Para saber mais sobre o armazenamento em cache de cadeias de caracteres de consulta com a **CDN Premium do Azure da Verizon**, confira [Controlando o comportamento do cache de solicitações de CDN com cadeias de caracteres de consulta - Premium](cdn-query-string-premium.md).
> 
> 

Existem três modos disponíveis:

* **Ignorar as cadeias de caracteres de consulta**: Este é o modo padrão de saudação.  nó de extremidade CDN Olá passará a cadeia de caracteres de consulta de saudação da origem do hello solicitante toohello na primeira solicitação de saudação e ativos de saudação do cache.  Todas as solicitações subsequentes para esse ativo são atendidas do nó de borda Olá ignorará a cadeia de caracteres de consulta de saudação até expira ativo em cache hello.
* **Ignorar o cache para URL com cadeias de caracteres de consulta**: nesse modo, as solicitações com cadeias de caracteres de consulta não estão em cache no nó de extremidade CDN hello.  nó de borda Olá recupera ativo Olá diretamente origem hello e passa toohello solicitante com cada solicitação.
* **Armazenar em cache cada URL exclusiva**: esse modo trata cada solicitação com uma cadeia de consulta como um ativo exclusivo com seu próprio cache.  Por exemplo, Olá resposta origem Olá para uma solicitação para *foo.ashx?q=bar* seria armazenado em cache no nó de borda hello e retornado para caches subsequentes com essa mesma cadeia de caracteres de consulta.  Uma solicitação para *foo.ashx?q=somethingelse* deve ser armazenado em cache como um ativo separado com seu próprio tempo toolive.

## <a name="changing-query-string-caching-settings-for-standard-cdn-profiles"></a>Alterando configurações de cache de cadeia de consulta para perfis de CDN padrão
1. Na folha de perfil CDN hello, clique em ponto de extremidade CDN Olá desejar toomanage.
   
    ![Pontos de extremidade da folha Perfil CDN](./media/cdn-query-string/cdn-endpoints.png)
   
    Abre a folha de ponto de extremidade CDN Hello.
2. Clique em Olá **configurar** botão.
   
    ![botão gerenciar da folha Perfil CDN](./media/cdn-query-string/cdn-config-btn.png)
   
    Abre a folha de configuração de CDN Hello.
3. Selecione uma configuração de saudação **comportamento do cache de cadeia de consulta** lista suspensa.
   
    ![Opções de cache de cadeia de caracteres de consulta CDN](./media/cdn-query-string/cdn-query-string.png)
4. Depois de fazer sua escolha, clique em Olá **salvar** botão.

> [!IMPORTANT]
> alterações de configurações de saudação não podem ser imediatamente visíveis, como demora Olá toopropagate de registro por meio de saudação CDN.  Para <b>Azure CDN do Akamai</b> , a propagação geralmente é concluída em um minuto.  Para perfis da <b>CDN do Azure da Verizon</b>, a propagação geralmente é concluída em 90 minutos, mas em alguns casos pode levar mais tempo.
> 
> 

