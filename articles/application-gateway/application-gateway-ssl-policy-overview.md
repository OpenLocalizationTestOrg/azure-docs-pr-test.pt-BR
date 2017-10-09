---
title: "Visão geral da política aaaSSL para Gateway de aplicativo do Azure | Microsoft Docs"
description: "Saiba mais sobre Azure Application Gateway permite que você tooconfigure política de SSL"
services: application gateway
documentationcenter: na
author: amsriva
manager: 
editor: 
tags: azure resource manager
ms.service: application gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure services
ms.date: 08/03/2017
ms.author: amsriva
ms.openlocfilehash: 80dbc437da3dba8a558c518ecdbb5927a11a2ed9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-ssl-policy-overview"></a>Visão geral da política SSL do Gateway de Aplicativo

Aplicativo Gateway permite o gerenciamento de certificado SSL toocentralize e reduzir a sobrecarga de criptografia e descriptografia de um farm de servidores de back-end. Este SSL centralizado tratamento também permite que você toospecify um SSL central política adequada tooyour requisitos de segurança organizacional. Isso ajuda a atender aos requisitos de conformidade, bem como diretrizes de segurança e práticas recomendadas.

Política de SSL inclui controle de versão de protocolo SSL, bem como conjuntos de codificação e ordem de saudação codificações são usadas durante um handshake SSL. Para este aplicativo Gateway oferece dois mecanismos tooallow clientes toocontrol SSL diretiva, um modelo predefinido ou uma política personalizada.

## <a name="predefined-ssl-policy"></a>Política SSL predefinida

O Gateway de Aplicativo tem três políticas de segurança predefinidos. Você pode configurar o gateway com qualquer nível apropriado de saudação do tooget essas políticas de segurança. nomes de política de saudação são anotados pelo ano hello e o mês em que eles foram configurados. Cada política oferece diferentes versões protocolo SSL e conjuntos de codificação. É recomendável toouse hello mais recente SSL políticas tooensure Olá melhor segurança de SSL. Application Gateway hoje permite toochoose usuários de um dos seguintes Olá predefinido.

### <a name="appgwsslpolicy20150501"></a>AppGwSslPolicy20150501

|Propriedade  |Valor  |
|---|---|
|Nome     | AppGwSslPolicy20150501        |
|MinProtocolVersion     | TLSv1_0        |
|Padrão| True (se nenhuma política predefinida é especificada) |
|CipherSuites     |TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384<br>TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256<br>TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384<br>TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256<br>TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA<br>TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA<br>TLS_DHE_RSA_WITH_AES_256_GCM_SHA384<br>TLS_DHE_RSA_WITH_AES_128_GCM_SHA256<br>TLS_DHE_RSA_WITH_AES_256_CBC_SHA<br>TLS_DHE_RSA_WITH_AES_128_CBC_SHA<br>TLS_RSA_WITH_AES_256_GCM_SHA384<br>TLS_RSA_WITH_AES_128_GCM_SHA256<br>TLS_RSA_WITH_AES_256_CBC_SHA256<br>TLS_RSA_WITH_AES_128_CBC_SHA256<br>TLS_RSA_WITH_AES_256_CBC_SHA<br>TLS_RSA_WITH_AES_128_CBC_SHA<br>TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384<br>TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256<br>TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384<br>TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256<br>TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA<br>TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA<br>TLS_DHE_DSS_WITH_AES_256_CBC_SHA256<br>TLS_DHE_DSS_WITH_AES_128_CBC_SHA256<br>TLS_DHE_DSS_WITH_AES_256_CBC_SHA<br>TLS_DHE_DSS_WITH_AES_128_CBC_SHA<br>TLS_RSA_WITH_3DES_EDE_CBC_SHA<br>TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA |
  
  ### <a name="appgwsslpolicy20170401"></a>AppGwSslPolicy20170401
  
|Propriedade  |Valor  |
|   ---      |  ---       |
|Nome     | AppGwSslPolicy20170401        |
|MinProtocolVersion     | TLSv1_0        |
|Padrão| Falso |
|CipherSuites     |TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256<br>TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384<br>TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA<br>TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA<br>TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256<br>TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384<br>TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384<br>TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256<br>TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA<br>TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA<br>TLS_RSA_WITH_AES_256_GCM_SHA384<br>TLS_RSA_WITH_AES_128_GCM_SHA256<br>TLS_RSA_WITH_AES_256_CBC_SHA256<br>TLS_RSA_WITH_AES_128_CBC_SHA256<br>TLS_RSA_WITH_AES_256_CBC_SHA<br>TLS_RSA_WITH_AES_128_CBC_SHA |
  
### <a name="appgwsslpolicy20170401s"></a>AppGwSslPolicy20170401S

|Propriedade  |Valor  |
|---|---|
|Nome     | AppGwSslPolicy20170401        |
|MinProtocolVersion     | TLSv1_2        |
|Padrão| Falso |
|CipherSuites     |TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256 <br>    TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384 <br>    TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA <br>TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA <br>TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256<br>TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384<br>TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384<br>TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256<br>TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA<br>TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA<br>TLS_RSA_WITH_AES_256_GCM_SHA384<br>TLS_RSA_WITH_AES_128_GCM_SHA256<br>TLS_RSA_WITH_AES_256_CBC_SHA256<br>TLS_RSA_WITH_AES_128_CBC_SHA256<br>TLS_RSA_WITH_AES_256_CBC_SHA<br>TLS_RSA_WITH_AES_128_CBC_SHA<br> |

## <a name="custom-ssl-policy"></a>Política SSL personalizada

Se precisar de uma política SSL predefinida toobe configurado para suas necessidades, você tem deve definir sua própria política SSL personalizada. Nesse caso, você tem controle total sobre Olá mínimo SSL protocol versão toosupport bem como suporte para conjuntos de codificação e a ordem de prioridade.
 
Versões de protocolo SSL:

* SSL 2.0 e 3.0 desabilitados por padrão para todos os Gateways do Aplicativo. Essas versões de protocolo não são configuráveis.
* Personalizado SSL política definição dá a opção tooselect qualquer um de saudação após três protocolos como Olá mínimo SSL versão do protocolo do seu gateway TLSv1_0, TLSv1_1, TLSv1_2.
* Se nenhuma política SSL for definida, todas as três (TLSv1_0, TLSv1_1, TLSv1_2) deverão ser habilitadas.

Conjunto de Codificação:

Application Gateway oferece suporte a saudação seguintes conjuntos de codificação do qual a política personalizada pode ser escolhida. Olá ordenação dos conjuntos de codificação de saudação determina a ordem de prioridade de saudação durante a negociação SSL.

Conjuntos de codificação disponíveis:

- TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384
- TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
- TLS_DHE_RSA_WITH_AES_256_GCM_SHA384
- TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
- TLS_DHE_RSA_WITH_AES_256_CBC_SHA
- TLS_DHE_RSA_WITH_AES_128_CBC_SHA
- TLS_RSA_WITH_AES_256_GCM_SHA384
- TLS_RSA_WITH_AES_128_GCM_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA256
- TLS_RSA_WITH_AES_128_CBC_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA
- TLS_RSA_WITH_AES_128_CBC_SHA
- TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384
- TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256
- TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384
- TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256
- TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA
- TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA
- TLS_DHE_DSS_WITH_AES_256_CBC_SHA256
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA256
- TLS_DHE_DSS_WITH_AES_256_CBC_SHA
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA
- TLS_RSA_WITH_3DES_EDE_CBC_SHA
- TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA

## <a name="next-steps"></a>Próximas etapas

[Configurar política SSL em um gateway de aplicativo](application-gateway-configure-ssl-policy-powershell.md)
