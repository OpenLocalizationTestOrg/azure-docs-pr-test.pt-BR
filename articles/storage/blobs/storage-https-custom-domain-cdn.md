---
title: "blobs do aaaUsing hello Azure CDN tooaccess com domínios personalizados por HTTPS"
description: "Saiba como blobs toointegrate Olá CDN do Azure com tooaccess de armazenamento de blob com domínios personalizados HTTPS"
services: storage
documentationcenter: 
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: mihauss
ms.openlocfilehash: f6cee36ca5495983545f2f6a8ff140677cf6914b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cdn-tooaccess-blobs-with-custom-domains-over-https"></a>Usando blobs do hello Azure CDN tooaccess com domínios personalizados por HTTPS

A CDN (Rede de Distribuição de Conteúdo) do Azure agora dá suporte a HTTPS para nomes de domínio personalizados.
Você pode aproveitar os blobs de armazenamento de tooaccess esse recurso usando seu domínio personalizado sobre HTTPS. toodo assim, você precisará tooenable CDN do Azure no seu blob ponto de extremidade e mapear Olá CDN tooa nome de domínio personalizado. Depois que você seguir essas etapas, habilitar HTTPS para seu domínio personalizado foi simplificada por meio de um botão do mouse, gerenciamento de certificados completo e tudo com nenhum custo adicional toonormal CDN preços.

Essa capacidade é importante porque ela permite que você tooprotect Olá privacidade e integridade dos dados de seus dados de aplicativo web confidenciais em trânsito. Usar o tráfego de tooserve de protocolo hello SSL por HTTPS garante que os dados são criptografados quando ela é enviada pela Olá internet. O HTTPS fornece confiabilidade, autenticação e protege seus aplicativos Web contra ataques.

> [!NOTE]
> Além disso tooproviding suporte a SSL para nomes de domínio personalizado, Olá CDN do Azure pode ajudar a dimensionar seu conteúdo de alta largura de banda do aplicativo toodeliver em torno de Olá, mundo.
> toolearn mais, confira [visão geral de saudação do Azure CDN](../../cdn/cdn-overview.md).
>
>

## <a name="quick-start"></a>Início rápido

Estes são Olá etapas necessárias tooenable HTTPS para o ponto de extremidade de armazenamento de blob personalizado:

1.  [Integrar uma conta de armazenamento do Azure com a CDN do Azure](../../cdn/cdn-create-a-storage-account-with-cdn.md).
    Este artigo o orienta por meio de criar uma conta de armazenamento no hello Portal do Azure, se você ainda não fez isso.
2.  [Domínio personalizado do mapa do Azure CDN tooa conteúdo](../../cdn/cdn-map-content-to-custom-domain.md).
3.  [Habilite HTTPS em um domínio personalizado da CDN do Azure](../../cdn/cdn-custom-ssl.md).

## <a name="shared-access-signatures"></a>As Assinaturas de Acesso Compartilhado

Se o ponto de extremidade de armazenamento de blob é o acesso de leitura anônimo toodisallow configurado, você precisará tooprovide um [assinatura de acesso compartilhado (SAS)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) token em cada solicitação que domínio personalizado tooyour. Por padrão, os pontos de extremidade de Armazenamento de Blobs não permitem acesso de leitura anônimo. Para obter mais informações sobre assinaturas de acesso compartilhado, veja [Gerenciar acesso de leitura anônimo a contêineres e blobs](storage-manage-access-to-resources.md).

CDN do Azure não respeita qualquer token SAS restrições toohello adicionado. Por exemplo, todos os tokens SAS têm uma hora da expiração. Isso significa que o conteúdo ainda pode ser acessada com uma SAS expirada até que o conteúdo é limpo de nós de extremidade CDN hello. Você pode controlar quanto tempo os dados em cache em Olá CDN pelo cabeçalho de resposta de configuração de cache no hello. Veja [Gerenciar a expiração dos blobs de Armazenamento do Azure na CDN do Azure](../../cdn/cdn-manage-expiration-of-blob-content.md) para obter instruções.

Se você criar várias URLs da SAS para Olá mesmo ponto de extremidade de blob, é recomendável ativar o cache de cadeia de caracteres de consulta para o Azure CDN. Isso é tooensure que cada URL é tratado como uma entidade única. Para obter mais informações, confira [Controlar o comportamento de caching da CDN do Azure com cadeias de consulta](../../cdn/cdn-query-string.md).

## <a name="http-toohttps-redirection"></a>Redirecionamento de HTTP tooHTTPS

Você pode optar por tooredirect tooHTTPS de tráfego HTTP. Isso requer o uso de oferta de premium Olá CDN do Azure da Verizon. É necessário muito[comportamento substituir HTTP usando o mecanismo de regras do Azure CDN](../../cdn/cdn-rules-engine.md) com a seguinte regra:

![](./media/storage-https-custom-domain-cdn/redirect-to-https.png)

"Nome de ponto de extremidade Cdn" refere-se nome toohello que você configurou para seu ponto de extremidade CDN. Você pode selecionar esse valor na lista suspensa de saudação. "Caminho de origem" se refere ao caminho hello dentro de sua conta de armazenamento de origem onde reside o conteúdo estático.
Se você estiver hospedando todo o conteúdo estático em um único contêiner, substitua "caminho de origem" pelo nome de saudação do contêiner.

Para se aprofundar em regras, consulte Olá [recursos do mecanismo de regras do Azure CDN](../../cdn/cdn-rules-engine-reference-features.md).

## <a name="pricing-and-billing"></a>Preços e cobrança

Quando você acessar blobs por meio de uma CDN do Azure, você paga [os preços de armazenamento de Blob](https://azure.microsoft.com/pricing/details/storage/blobs/) para o tráfego entre nós de borda hello e da origem da saudação (armazenamento de Blob), e [preços CDN](https://azure.microsoft.com/pricing/details/cdn/) para dados acessados a partir de nós de borda hello.

Por exemplo, digamos que você tenha uma conta de armazenamento no Oeste dos EUA que está sendo acessada usando uma CDN do Azure. Se alguém de saudação do Reino Unido tenta tooaccess uma saudação blobs na conta de armazenamento por meio de saudação CDN, o Azure verifica primeiro nó de borda hello mais próximo à saudação do Reino Unido para esse blob. Se encontrado, ele acessa essa cópia de blob hello e usará CDN sobre preços, porque ele está sendo acessado no hello CDN. Se não for encontrado, o Azure copiará Olá blob toohello borda nó, o que resultará na saída e encargos de transação como especificado no hello preços de armazenamento de Blob e acessar o arquivo hello no nó de borda hello, que resultará na cobrança da CDN.

Ao examinar a saudação [CDN página de preços](https://azure.microsoft.com/pricing/details/cdn/), observe que dão suporte a HTTPS para nomes de domínio personalizado está disponível somente para CDN do Azure de produtos Verizon (Standard e Premium).

## <a name="next-steps"></a>Próximas etapas

[Configurar um nome de domínio personalizado para seu ponto de extremidade de Armazenamento de Blobs](storage-custom-domain-name.md)
