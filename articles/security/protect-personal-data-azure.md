---
title: Proteger dados pessoais no Microsoft Azure | Microsoft Docs
description: "Primeiro artigo de uma série de artigos para ajudá-lo a usar o Azure para proteger dados pessoais"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: dfb046374397c8a19672ce6b67741903fff6e178
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="protect-personal-data-in-microsoft-azure"></a>Proteger dados pessoais no Microsoft Azure

Este artigo apresenta uma série de artigos que ajuda a usar as tecnologias e os serviços de segurança do Azure para proteger dados pessoais. Este é um requisito fundamental para muitas iniciativas de governança e conformidade corporativas e do setor. O cenário, a declaração do problema e as metas da empresa são incluídos aqui.

## <a name="scenario-and-problem-statement"></a>Cenário e declaração do problema

Uma empresa de cruzeiro de grande porte, com sede nos Estados Unidos, está expandindo suas operações para oferecer roteiros nos mares Mediterrâneo, Adriático e Báltico, bem como nas Ilhas Britânicas. Para dar suporte a esses esforços, ela adquiriu várias linhas de cruzeiro menores localizadas na Itália, na Alemanha, na Dinamarca e no Reino Unido.

A empresa usa o Microsoft Azure para armazenar dados corporativos na nuvem. Isso pode incluir funcionário e/ou informações do cliente, como:

- endereços
- números de telefone
- números de identificação fiscal
- informações de médicas
- informações de cartão de crédito

A empresa deve proteger a privacidade dos dados de funcionário e o cliente ao fazer dados acessíveis para os departamentos que precisam dela. (como departamentos de folha de pagamento e reservas)

## <a name="company-goals"></a>Metas da empresa 

- As fontes de dados que contêm dados pessoais são criptografadas quando residem no armazenamento em nuvem.

- Os dados pessoais transferidos de um local para outro são criptografados enquanto estão em trânsito. Isso será verdadeiro se os dados estiverem viajando pela rede virtual ou na Internet entre os data centers corporativos e a nuvem do Azure.

- A confidencialidade e a integridade dos dados pessoais são protegidas contra o acesso não autorizado por tecnologias de controle de acesso e gerenciamento de identidade forte.

- Os dados pessoais são protegidos contra a exposição por meio da violação de dados com o monitoramento de ameaças e vulnerabilidades.

- O estado de segurança dos serviços do Azure que armazenam ou transmitem dados pessoais é avaliado para identificar oportunidades para proteger melhor os dados pessoais.

## <a name="data-protection-guidance"></a>Diretrizes de proteção de dados

Os seguintes artigos contêm diretrizes de instruções técnicas que ajudarão você a atingir as metas de proteção de dados pessoais listadas acima:

- [Tecnologias de criptografia do Azure](protect-personal-data-at-rest.md)

- [Tecnologias de criptografia do Azure](protect-personal-data-in-transit-encryption.md)

- [Tecnologias de acesso e identidade do Azure](protect-personal-data-identity-access-controls.md)

- [Tecnologias de segurança de rede do Azure](protect-personal-data-network-security.md)

- [Central de Segurança do Azure](protect-personal-data-azure-security-center.md)



## <a name="next-steps"></a>Próximas etapas

- [Site de Informações de Segurança do Azure](https://aka.ms/AzureSecInfo)

- [Central de Confiabilidade da Microsoft](https://www.microsoft.com/TrustCenter/default.aspx)

- [Central de Segurança do Azure](https://azure.microsoft.com/services/security-center/)

- [Blog da equipe de segurança do Azure](https://www.azuresecurityorg)

- [Blog do Azure.com – Segurança](https://azure.microsoft.com/blog/topics/security/)
