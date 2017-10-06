---
title: "as portas de firewall Olá tooopen aaaHow necessárias para um aplicativo de Proxy de aplicativo | Microsoft Docs"
description: "Descubra quais tooopen portas para toowork de Proxy de aplicativo de saudação do AD do Azure corretamente"
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
ms.openlocfilehash: cdc7badb7c15591689a3bfd6bb26da182b00fb3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-hello-firewall-ports-required-for-an-application-proxy-application"></a>Como tooopen Olá portas de firewall necessárias para um aplicativo de Proxy de aplicativo

toosee uma lista completa de portas Olá necessários e a função de saudação de cada porta, consulte a seção pré-requisitos Olá Olá [documentação do Proxy de aplicativo](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable). observe que o Application Proxy usa apenas as portas de saída.

Você também pode verificar se há todas Olá necessárias portas abertas, abrindo Olá [ferramenta de teste de portas do conector](https://aadap-portcheck.connectorporttest.msappproxy.net/) da sua rede local. Mais marcas de seleção verde significa maior resiliência. 

## <a name="app-proxy-regions"></a>Regiões de Proxy de aplicativo

Estamos trabalhando em um modo toolet você sabe que essas regiões precisa toobe verde para você. Por enquanto, certifique-se de que todas estão verdes. EUA Central também é necessária, independentemente de qual região você está.

toomake se Olá ferramenta oferece Olá resultados à direita, ser-se:

-   Abra a ferramenta de saudação em um navegador do servidor de saudação onde você instalou Olá conector.

-   Certifique-se de que qualquer tooyour aplicável proxies ou firewalls conector também são aplicadas toothis página. Isso pode ser feito no Internet Explorer indo muito**configurações**  - &gt; **opções da Internet**  - &gt; **conexões**  - &gt; **Configurações da Lan**. Nessa página, você deve ver campo hello "Usar um Proxy do servidor para sua LAN". Marque esta caixa e coloque o endereço de proxy de saudação no campo de "Address" hello.

## <a name="next-steps"></a>Próximas etapas
[Noções básicas sobre conectores de Proxy de Aplicativo do Azure AD](application-proxy-understand-connectors.md)
