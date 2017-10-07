---
title: "aaaAzure considerações de design do Active Directory híbrida identidade - determinar requisitos de identidade | Microsoft Docs"
description: "Identificar as necessidades de negócios da empresa Olá que levarão toodefine requisitos de saudação para design de identidade híbrida Olá."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: de690978-84ef-41ad-9dfe-785722d343a1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: b2f1cad923b0f08ededa0d8f9a4ea8e799956e54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="determine-identity-requirements-for-your-hybrid-identity-solution"></a>Determinar requisitos de identidade para sua solução de identidade híbrida
Olá primeira etapa na criação de uma solução de identidade híbrida é requisitos de saudação toodetermine da organização de negócios de saudação que será a utilização dessa solução.  Identidade híbrida começa como uma função de suporte (há suporte para todas as outras soluções de nuvem, fornecendo autenticação) e vai tooprovide funcionalidades novas e interessantes que desbloquear novas cargas de trabalho para os usuários.  Essas cargas de trabalho ou serviços que você deseja tooadopt para seus usuários ditará os requisitos de saudação para design de identidade híbrida hello.  Esses serviços e cargas de trabalho precisam de identidade híbridas de tooleverage locais e na nuvem hello.  

Você precisa toogo esses principais aspectos da saudação business toounderstand o que é um requisito agora e que empresa Olá planos para Olá futuras. Se você não tem visibilidade de saudação da estratégia de longo prazo Olá para design de identidade híbrida, a probabilidade é que sua solução não será escalonável conforme as necessidades de negócios de saudação aumenta e muda.   T ele diagrama abaixo mostra um exemplo de um híbrido identidade arquitetura e hello cargas de trabalho que estão sendo desbloqueada para usuários. Isso é apenas um exemplo de todos os Olá novas possibilidades que podem ser desbloqueadas e entregue com uma estratégia de identidade híbrida sólido. 

Alguns componentes que fazem parte da arquitetura de identidade híbrida Olá![](./media/hybrid-id-design-considerations/hybrid-identity-architechture.png)

## <a name="determine-business-needs"></a>Determinar as necessidades de negócios
Cada empresa terá requisitos diferentes, mesmo que essas empresas fizerem parte da saudação mesmo setor, os requisitos de negócios reais Olá podem variar. Você ainda pode aproveitar as práticas recomendadas do setor hello, mas, por fim, são necessidades de negócios da empresa Olá que levarão toodefine requisitos de saudação para design de identidade híbrida hello. 

Verifique se a seguir Olá tooanswer perguntas tooidentify sua empresa precisa de:

* Sua empresa está procurando toocut custos operacionais de TI?
* Sua empresa está procurando recursos de nuvem toosecure (aplicativos SaaS, infraestrutura)?
* Sua empresa procurando toomodernize sua equipe de TI?
  * São os usuários mais exigentes e móveis IT toocreate exceções em seu tipo diferente de tooallow DMZ recursos diferentes do tráfego tooaccess?
  * Sua empresa tem aplicativos herdados que necessários toobe publicado usuários modernos toothese mas não são fácil toorewrite?
  * Sua empresa precisa tooaccomplish todas essas tarefas e colocá-lo sob controle Olá simultaneamente?
* Sua empresa é procurando as identidades dos usuários toosecure e reduzir o risco colocando novas ferramentas que aproveitam a experiência de saudação do Azure segurança experiência local do Microsoft?
* É sua empresa tentar tooget rid da saudação temido contas "externas" no local e movê-los toohello nuvem em que eles não são mais uma ameaça inativa em seu ambiente local?

## <a name="analyze-on-premises-identity-infrastructure"></a>Analisar a infraestrutura de identidades no local
Agora que você tem uma ideia sobre os requisitos de negócios da empresa, é necessário tooevaluate sua infraestrutura de identidade local. Essa avaliação é importante para definir Olá requisitos técnicos toointegrate identidade solução toohello nuvem identidade sistema de gerenciamento atual. Certifique-se de saudação tooanswer perguntas a seguir:

* Que solução de autenticação e autorização sua empresa usa no local? 
* Sua empresa possui atualmente algum serviço de sincronização local?
* Sua empresa usa qualquer IdP (provedor de identidade de terceiros)?

Você também precisa toobe com reconhecimento de saudação serviços de nuvem que sua empresa pode ter. Executar uma avaliação toounderstand Olá atual a integração com o SaaS, IaaS ou PaaS modelos em seu ambiente é muito importante. Certifique-se de saudação tooanswer perguntas a seguir durante a avaliação:

* Sua empresa tem alguma integração com um provedor de serviços de nuvem?
* Em caso afirmativo, quais serviços estão sendo usados?
* Atualmente, essa integração está em produção ou é um piloto?

> [!NOTE]
> Se você não tiver um mapeamento de precisão de todos os seus aplicativos e serviços em nuvem, você pode usar a ferramenta do Cloud App Discovery Olá. Essa ferramenta pode fornecer a seu departamento de TI visibilidade de todos os negócios da organização e aplicativos de nuvem do consumidor. Que torna mais fácil do que nunca toodiscover shadow IT em sua organização, incluindo detalhes sobre os padrões de uso e de quaisquer usuários acessando seus aplicativos na nuvem. Consulte tooget iniciado [do Cloud app discovery](active-directory-cloudappdiscovery-whatis.md).
> 
> 

## <a name="evaluate-identity-integration-requirements"></a>Avaliar os requisitos de integração de identidade
Em seguida, você precisa tooevaluate requisitos de integração de identidade de saudação. Essa avaliação é importante toodefine requisitos técnicos do Olá para como fará a autenticação de usuários, como presença da organização Olá aparecerão na nuvem de saudação, como a organização Olá permitirá que a autorização e experiência do usuário que Olá é toobe contínuo. Certifique-se de saudação tooanswer perguntas a seguir:

* Sua organização usará federação, autenticação padrão ou ambos?
* A federação é um requisito?  Devido ao seguinte hello:
  * SSO baseada em Kerberos
  * Sua empresa tem um aplicativo local (seja criado internamente ou de terceiros) que usa SAML ou recursos de federação semelhantes.
  * MFA usando cartões inteligentes. RSA SecurID, etc.
  * Regras de acesso de cliente que aborde questões de saudação abaixo:
    1. Posso bloquear todos os tooOffice de acesso externo 365 com base no endereço IP de saudação do cliente Olá?
    2. Posso bloquear todos os tooOffice de acesso externo 365, exceto o Exchange ActiveSync?
    3. Posso bloquear todos os tooOffice de acesso externo 365, exceto aplicativos baseados em navegador (OWA, SPO)
    4. Pode bloquear todos os tooOffice de acesso externo 365 para membros de grupos do AD designados
* Preocupações de auditoria/segurança
* Investimento já existente na autenticação federada
* Qual nome de nossa organização usará para nosso domínio na nuvem Olá?
* Organização de saudação tem um domínio personalizado?
  1. Esse domínio é público e verificável facilmente usando DNS?
  2. Se não for, em seguida, você tem um domínio público que pode ser usado tooregister um UPN alternativo no AD?
* Identificadores de usuário Olá são consistentes para representação de nuvem? 
* Organização de saudação têm aplicativos que exigem integração com serviços de nuvem?
* Organização de saudação tem vários domínios e todos eles usará a autenticação federada ou padrão?

## <a name="evaluate-applications-that-run-in-your-environment"></a>Avaliar aplicativos executados em seu ambiente
Agora que você tem uma ideia sobre seus locais e infraestrutura de nuvem, você precisa de aplicativos de saudação tooevaluate que são executados nesses ambientes. Essa avaliação é importante toodefine Olá requisitos técnicos toointegrate sistema de gerenciamento de identidade de nuvem para toohello esses aplicativos. Certifique-se de saudação tooanswer perguntas a seguir:

* Onde nossos aplicativos residirão?
* Os usuários acessarão os aplicativos no local?  Na nuvem Olá? Ou ambos?
* Existem planos tootake Olá aplicativo cargas de trabalho existentes e movê-los toohello nuvem?
* Há planos toodevelop novos aplicativos que residem no local ou na saudação de nuvem que usará a autenticação de nuvem?

## <a name="evaluate-user-requirements"></a>Avaliar os requisitos do usuário
Você também tem requisitos de usuário tooevaluate hello. Essa avaliação é toodefine importantes etapas de saudação que serão necessário para a integração e ajudando os usuários como transição toohello nuvem. Certifique-se de saudação tooanswer perguntas a seguir:

* Os usuários acessarão aplicativos no local?
* Os usuários acessarão os aplicativos na nuvem Olá?
* Como fazer os usuários normalmente tootheir logon local ambiente?
* Como os usuários entrar toohello será nuvem?

> [!NOTE]
> Verifique se anotações tootake de cada resposta e entender Olá lógica por trás da resposta de saudação. [Determinar requisitos de resposta a incidentes](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) apresentará as opções de saudação disponíveis e profissionais/desvantagens de cada opção.  Ao responder essas perguntas, você selecionará a opção que melhor se ajusta às necessidades da sua empresa.
> 
> 

## <a name="next-steps"></a>Próximas etapas
[Determinar os requisitos de sincronização de diretório](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md)

## <a name="see-also"></a>Confira também
[Visão geral sobre as considerações de design](active-directory-hybrid-identity-design-considerations-overview.md)

