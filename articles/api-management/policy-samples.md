---
title: "Políticas do gerenciamento de API do Azure de exemplo | Microsoft Docs"
description: "Saiba mais sobre as políticas disponíveis para uso no Gerenciamento de API do Azure."
services: api-management
documentationcenter: 
author: Juliako
manager: cflower
editor: 
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: sample
ms.date: 10/31/2017
ms.author: apimpm
ms.custom: mvc
ms.openlocfilehash: e951eb47290a2d1b6f892f1ccf923f6ce0c1899c
ms.sourcegitcommit: 922687d91838b77c038c68b415ab87d94729555e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2017
---
# <a name="api-management-policy-samples"></a>Políticas de gerenciamento de API de exemplo

As [políticas](api-management-howto-policies.md) são funcionalidades poderosas do sistema que permitem que o editor altere o comportamento da API por meio de configuração. As políticas são um conjunto de instruções executadas em sequência, na solicitação ou na resposta de uma API. A tabela a seguir contém links para exemplos e fornece uma breve descrição de cada exemplo.

|||
|---|---|
|**Políticas de entrada**||
|[Adicionar um cabeçalho Forwarded para permitir que a API de back-end crie URLs adequadas](./policies/set-header-to-enable-backend-to-construct-urls.md?toc=api-management/toc.json) |Demonstra como adicionar um cabeçalho Forwarded na solicitação de entrada para permitir que a API de back-end crie URLs adequadas.|
|[Adicionar um cabeçalho que contém uma ID de correlação](./policies/add-correlation-id.md?toc=api-management/toc.json) |Demonstra como adicionar um cabeçalho que contém uma ID de correlação na solicitação de entrada.|
|[Adicionar recursos a um serviço de back-end e armazenar a resposta em cache](./policies/cache-response.md?toc=api-management/toc.json) |Mostra como adicionar recursos a um serviço de back-end. Por exemplo, aceitar um nome do local em vez de latitude e longitude em uma API de previsão do tempo.|
|[Autorizar o acesso com base em declarações JWT](./policies/authorize-request-based-on-jwt-claims.md?toc=api-management/toc.json) |Mostra como autorizar o acesso a métodos HTTP específicos em uma API com base em declarações de JWT.|
|[Autorizar o acesso usando o token OAuth do Google](./policies/use-google-as-oauth-token-provider.md?toc=api-management/toc.json) |Mostra como autorizar o acesso aos pontos de extremidade usando o Google como um provedor de token OAuth.|
|[Gerar Assinatura de Acesso Compartilhado e encaminhar solicitação para o armazenamento do Azure](./policies/generate-shared-access-signature.md?toc=api-management/toc.json) |Mostra como gerar uma [Assinatura de Acesso Compartilhado](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) usando expressões e encaminhar a solicitação para o armazenamento do Azure com a política rewrite-uri. |
|[Obter token de acesso OAuth2 do AAD e encaminhá-lo para o back-end](./policies/use-oauth2-for-authorization.md?toc=api-management/toc.json) |Fornece um exemplo de como usar o OAuth2 para autorização entre o gateway e um back-end. Ele mostra como obter um token de acesso do AAD e encaminhá-lo para o back-end.|
|[Obter token X-CSRF do SAP Gateway usando a política de solicitação de envio](./policies/get-x-csrf-token-from-sap-gateway.md?toc=api-management/toc.json) |Mostra como implementar o padrão X-CSRF usado por várias APIs. Este exemplo é específico do SAP Gateway. |
|[Rotear a solicitação com base no tamanho do corpo](./policies/route-requests-based-on-size.md?toc=api-management/toc.json) |Demonstra como rotear solicitações com base no tamanho do corpo.|
|[Enviar informações de contexto de solicitação para o serviço de back-end](./policies/send-request-context-info-to-backend-service.md?toc=api-management/toc.json) |Mostra como enviar algumas informações de contexto para o serviço de back-end para registro em log ou processamento.|
|[Definir duração do cache de resposta](./policies/set-cache-duration.md?toc=api-management/toc.json) |Demonstra como definir a duração do cache de resposta usando o valor de maxAge no cabeçalho Cache-Control enviado pelo back-end.|
|**Políticas de saída**||
|[Filtrar o conteúdo da resposta](./policies/filter-response-content.md?toc=api-management/toc.json) | Demonstra como filtrar os elementos de dados do conteúdo da resposta com base no produto associado à solicitação.|
|**Políticas em caso de erro**||
|[Registrar erros no Stackify](./policies/log-errors-to-stackify.md?toc=api-management/toc.json) |Mostra como adicionar uma política de registro de erro em log para enviar erros ao Stackify para que eles sejam registrados em log.|
