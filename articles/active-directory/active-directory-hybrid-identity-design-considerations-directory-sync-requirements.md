---
title: "aaaAzure considerações de design do Active Directory híbrida identidade - determinar requisitos de sincronização de diretório | Microsoft Docs"
description: "Identificar quais requisitos são necessários para a sincronização de todos os usuários de saudação entre = em locais e na nuvem para a empresa hello."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 593eaa71-17eb-4c16-8c98-43cc62987e65
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 6646e3792c65f37c3d62eecdb6c6f3bd257f04f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="determine-directory-synchronization-requirements"></a>Determinar os requisitos de sincronização de diretório
Sincronização é fornecer aos usuários uma identidade em nuvem Olá baseada na respectiva identidade local. Se eles usarão a conta sincronizada para autenticação ou autenticação federada, ou não usuários Olá ainda serão necessário toohave uma identidade em nuvem hello.  Essa identidade precisará toobe mantidos e atualizadas periodicamente.  Olá atualizações podem ter várias formas, de título alterações toopassword alterações.  

Comece a avaliar as organizações a saudação requisitos de usuário e solução de identidade no local. Essa avaliação é importante toodefine requisitos técnicos do Olá para como identidades de usuário serão criadas e mantidas na nuvem hello.  Para a maioria das organizações, o Active Directory é local e serão diretório local Olá que os usuários por sincronizados do, mas em alguns casos não será o caso de saudação.  

Certifique-se de saudação tooanswer perguntas a seguir:

* Você tem uma floresta do AD, várias ou nenhuma?
  
  * Quantos diretórios AD do Azure você vai sincronizar?
    
    1. Você está usando a filtragem?
    2. Você tem vários servidores do Azure AD Connect planejados?
* Atualmente, você tem uma ferramenta de sincronização local?
  
  * Em caso positivo, os usuários têm um diretório virtual/integração das identidades?
* Você tem qualquer outro diretório local que você deseja toosynchronize (por exemplo, diretório LDAP, banco de dados de RH, etc)?
  * Você vai toobe fazer qualquer GALSync?
  * O que é o estado atual de saudação do UPNs em sua organização? 
  * Você tem um diretório diferente que os usuários se autenticam?
  * Sua empresa usa o Microsoft Exchange?
    * Planeja de ter uma implantação híbrida de mudança?

Agora que você tem uma ideia sobre os requisitos de sincronização, é necessário toodetermine qual ferramenta é Olá toomeet correta de um esses requisitos.  A Microsoft fornece várias integração de diretório ferramentas tooaccomplish e sincronização.  Consulte Olá [tabela de comparação de ferramentas de integração do identidade híbrida diretório](active-directory-hybrid-identity-design-considerations-tools-comparison.md) para obter mais informações. 

Agora que você tem a seus requisitos de sincronização e a ferramenta Olá realizará essa operação para a sua empresa, você precisa de aplicativos de saudação tooevaluate que utilizem esses serviços de diretório. Essa avaliação é importante toodefine Olá requisitos técnicos toointegrate nuvem de toohello esses aplicativos. Certifique-se de saudação tooanswer perguntas a seguir:

* Esses aplicativos serão movido toohello de nuvem e usar o diretório Olá?
* Há atributos especiais que precisam toobe sincronizado toohello nuvem esses aplicativos podem usá-los com êxito?
* Esses aplicativos precisam de toobe reescrito tootake aproveitar autenticação de nuvem?
* Esses aplicativos continuará toolive local enquanto os usuários acessá-los usando a identidade de nuvem Olá?

Você também precisa toodetermine Olá segurança requisitos e restrições de sincronização de diretório. Essa avaliação é importante tooget uma lista de requisitos de saudação que será necessária em ordem toocreate e manter as identidades do usuário na nuvem hello. Certifique-se de saudação tooanswer perguntas a seguir:

* Onde o servidor de sincronização de saudação estarão localizado?
* Será integrado ao domínio?
* Servidor de saudação esteja localizado em uma rede restrita atrás de um firewall, como uma rede de Perímetro?
  * Você será a sincronização de toosupport tooopen capaz de saudação necessária firewall portas?
* Você tem um plano de recuperação de desastres para o servidor de sincronização de Olá?
* Você tem uma conta com as permissões corretas para todas as florestas que você deseja toosynch com Olá?
  * Se sua empresa não sabe a resposta Olá para essa pergunta, examine a seção de hello "Permissões para sincronização de senha" no artigo Olá [Olá instalar serviço de sincronização do Azure Active Directory](https://msdn.microsoft.com/library/azure/dn757602.aspx#BKMK_CreateAnADAccountForTheSyncService) e determine se você já tem um conta com essas permissões, ou se você precisa toocreate um.
* Se você tiver a sincronização de multi-floresta é floresta do hello sincronização servidor capaz de tooget tooeach?

> [!NOTE]
> Verifique se anotações tootake de cada resposta e entender Olá lógica por trás da resposta de saudação. [Determinar requisitos de resposta a incidentes](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) apresentará as opções de saudação disponíveis. Ao responder essas perguntas, você selecionará a opção que melhor se ajusta às necessidades da sua empresa.
> 
> 

## <a name="next-steps"></a>Próximas etapas
[Determinar os requisitos de autenticação multifator](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)

## <a name="see-also"></a>Confira também
[Visão geral sobre as considerações de design](active-directory-hybrid-identity-design-considerations-overview.md)

