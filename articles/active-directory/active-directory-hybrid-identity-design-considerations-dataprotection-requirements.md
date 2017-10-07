---
title: "aaaAzure considerações de design do Active Directory híbrida identidade - determinar requisitos de proteção de dados | Microsoft Docs"
description: "Ao planejar sua solução de identidade híbrida, identificar os requisitos de proteção de dados de saudação para seu negócio e quais opções estão disponível toobest atenderem esses requisitos."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 40dc4baa-fe82-4ab6-a3e4-f36fa9dcd0df
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 189abf9affbc2894c322f362d84222d4e33d472e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="plan-for-enhancing-data-security-through-strong-identity-solution"></a>Planejar para aumentar a segurança de dados usando solução de identidade forte
Olá primeira etapa tooprotect Olá dados são identificar quem pode acessar os dados e como parte desse processo, você precisa toohave uma solução de identidade que pode se integra com os recursos de autenticação e autorização de tooprovide do sistema. Autenticação e autorização são frequentemente confundidos um com o outro e suas funções são mal compreendidas. Na realidade, são bastante diferentes, conforme mostrado na figura a saudação abaixo:

![](./media/hybrid-id-design-considerations/mobile-devicemgt-lifecycle.png)

**Estágios do ciclo de vida de gerenciamento de dispositivo móvel**

Ao planejar sua solução de identidade híbrida, você deve entender os requisitos de proteção de dados Olá para sua empresa e quais opções estão disponível toobest atenderem a esses requisitos.

> [!NOTE]
> Depois de concluir o planejamento de segurança de dados, examine [determinar os requisitos de autenticação multifator](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md) tooensure se suas seleções em relação aos requisitos de autenticação multifator não foram afetadas por decisões Olá Você fez nesta seção.
> 
> 

## <a name="determine-data-protection-requirements"></a>Determinar os requisitos para proteção de dados
Na era Olá de mobilidade, a maioria das empresas têm uma meta comum: habilitar seu toobe usuários produtivo em seus dispositivos móveis ao local ou remotamente em qualquer lugar na produtividade do tooincrease de ordem. Enquanto isso poderia ser um objetivo comum, as empresas que têm esse requisito também será preocupação, relativa à quantidade de saudação de ameaças que devem ser reduzidos em ordem tookeep dados da empresa seguros e manter a privacidade do usuário. Cada empresa terá requisitos diferentes em relação a isso; regras de conformidade diferente que variam de acordo empresa de saudação do setor toowhich está atuando vai levar toodifferent decisões de design. 

No entanto, há alguns aspectos de segurança que devem ser explorados e validados, independentemente do setor hello, que são explicados na próxima seção, Olá.

## <a name="data-protection-paths"></a>Caminhos de proteção de dados
![](./media/hybrid-id-design-considerations/data-protection-paths.png)

**Caminhos de proteção de dados**

Olá acima diagrama, o componente de identidade Olá será Olá primeiro um toobe verificado antes que os dados são acessados. No entanto, esses dados podem ser em diferentes estados durante o tempo de saudação que foi acessado. Cada número nesse diagrama representa um caminho no qual dados podem estar localizados em algum momento. Esses números são explicados abaixo:

1. Proteção de dados no nível do dispositivo de saudação.
2. Proteção de dados em trânsito.
3. Proteção de dados em repouso no local.
4. Proteção de dados em repouso na nuvem hello.

Embora os controles técnicos de saudação que permitirão IT tooprotect Olá próprios dados em cada um desses fases diretamente não são oferecidos pela solução de identidade híbrida Olá, é necessário que solução de identidade híbrida Olá é capaz de aproveitar locais e identidade gerenciamento usuário recursos de nuvem tooidentify Olá antes de conceder acessar toohello dados. Ao planejar sua solução de identidade híbrida Certifique-se de que Olá a seguir são responder perguntas de acordo com os requisitos da organização tooyour:

## <a name="data-protection-at-rest"></a>Proteção de dados em repouso
Independentemente de onde os dados de saudação estiverem em repouso (dispositivo, nuvem ou local), é importante tooperform uma organização de saudação avaliação toounderstand precisa nesse sentido. Para essa área, certifique-se de que Olá perguntas a seguir são frequentes:

* Sua empresa precisa tooprotect dados em repouso?
  * Em caso afirmativo, é toointegrate capaz de solução Olá de identidade híbrida com sua infraestrutura local atual?
  * Em caso afirmativo, é toointegrate capaz de solução Olá de identidade híbrida com suas cargas de trabalho localizadas na nuvem Olá?
* É Olá nuvem identity management tooprotect capaz de saudação credenciais do usuário e outros dados armazenados na nuvem Olá?

## <a name="data-protection-in-transit"></a>Proteção de dados em trânsito
Dados em trânsito entre dispositivo hello e Olá datacenter ou entre dispositivos hello e nuvem Olá devem ser protegidos. No entanto, estar em trânsito não significa necessariamente em um processo de comunicação com um componente fora do seu serviço de nuvem; ele também se move internamente, como entre duas redes virtuais. Para essa área, certifique-se de que Olá perguntas a seguir são frequentes:

* Sua empresa precisa tooprotect dados em trânsito?
  * Em caso afirmativo, é toointegrate capaz de solução Olá de identidade híbrida com controles de seguros, como SSL/TLS?
* Gerenciamento de identidades de nuvem Olá manter Olá tráfego tooand Olá repositório de diretório (dentro e entre data centers) assinado?

## <a name="compliance"></a>Conformidade
Normas, as leis e requisitos de conformidade normativa irão variar de acordo setor toohello que sua empresa pertence. As empresas em setores regulamentadas alta devem tratar problemas de toocompliance relacionados de preocupações de gerenciamento de identidades. Regulamentações como Sarbanes-Oxley (SOX), Olá Health Insurance Portability e Accountability Act (HIPAA), Olá Gramm-Leach-Bliley Act (GLBA) e Olá Payment Card Industry Data Security Standard (PCI DSS) são muito estrita sobre identidade e acesso. solução de identidade híbrida de saudação que sua empresa adotará deve ter Olá principais recursos que atenderá Olá necessidades de um ou mais essas normas. Para essa área, certifique-se de que Olá perguntas a seguir são frequentes:

* Solução de identidade híbrida Olá é compatível com os requisitos normativos Olá para sua empresa?
* Solução de identidade faz Olá híbrida desenvolveu nos recursos que habilitam toobe compatíveis normativa requisitos da sua empresa? 

> [!NOTE]
> Verifique se anotações tootake de cada resposta e entender Olá lógica por trás da resposta de saudação. [Definir a estratégia de proteção de dados](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) irá Olá opções disponíveis e as vantagens/desvantagens de cada opção.  Ao responder essas perguntas, você selecionará a opção que melhor se ajusta às necessidades da sua empresa.
> 
> 

## <a name="next-steps"></a>Próximas etapas
 [Determinar requisitos de gerenciamento de conteúdo](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md)

## <a name="see-also"></a>Consulte também
[Visão geral sobre as considerações de design](active-directory-hybrid-identity-design-considerations-overview.md)

