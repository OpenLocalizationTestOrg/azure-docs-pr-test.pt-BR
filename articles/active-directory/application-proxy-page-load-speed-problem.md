---
title: aaaAn aplicativo Proxy de aplicativo usa muito tooload | Microsoft Docs
description: "Solucionar problemas de desempenho de carregamento de página com hello Proxy de aplicativo do Azure AD"
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
ms.openlocfilehash: 4c7a51f96840966a1d88933fa4e30f39479d8a5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="an-application-proxy-application-takes-too-long-tooload"></a>Um aplicativo de Proxy de aplicativo usa tooload muito longo

Este artigo ajuda toounderstand por que um aplicativo de Proxy de aplicativo do Azure AD pode levar um tooload muito tempo e o que você pode fazer tooresolve esse problema.

## <a name="overview"></a>Visão geral
Se os aplicativos estão funcionando, mas você verá uma longa latência, pode haver alguns ajustes secundários em sua topologia de rede que você pode considerar a velocidade de saudação tooimprove. Para uma avaliação das diferentes topologias, consulte Olá [documento de considerações de rede](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).

Se essas considerações não ajudarem, infelizmente nós não temos atualmente outras recomendações para ajuste de desempenho. Como Olá serviço Proxy de aplicativo expande toomore centros de dados que podem ser tooyou mais próximo, você pode iniciar toosee aprimorado latência diretamente. centros de lista completa de saudação de toosee de dados do Azure, você pode ver Olá [página de teste de latência](http://www.azurespeed.com/Azure/Latency). 

Olá centros de dados com o serviço de Proxy de aplicativo hello podem ser encontrados com hello [ferramenta de teste de portas do conector](https://aadap-portcheck.connectorporttest.msappproxy.net/). 

## <a name="feedback-on-application-proxy-data-center-locations"></a>Comentários sobre locais de data centers do Proxy de Aplicativo 
Pode haver data centers do Azure que ainda não incluam o Proxy de aplicativo, mas levam tooa aperfeiçoamento de latência excelentes para você. saudação de datacenter local < aadapfeedback@microsoft.com > para que possamos pode usar seu tooplan comentários como podemos expandir.

Estamos trabalhando em alguns recursos adicionais que ajudam a melhorar a latência de saudação para locatários que atualmente consulte latências de longo e ser documentação em tooshare-se de que quando estiver disponível.

## <a name="next-steps"></a>Próximas etapas
[Trabalhar com servidores proxy locais existentes](application-proxy-working-with-proxy-servers.md)
