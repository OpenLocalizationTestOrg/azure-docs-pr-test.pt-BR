---
title: "práticas recomendadas de aaaBest para acesso condicional no Active Directory do Azure | Microsoft Docs"
description: "Saiba sobre o que você deve saber e o que você deve evitar fazer ao configurar políticas de acesso condicional."
services: active-directory
keywords: "tooapps de acesso condicional, o acesso condicional com o AD do Azure, proteger o acesso toocompany recursos, políticas de acesso condicional"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8c1d978f-e80b-420e-853a-8bbddc4bcdad
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 4952f8746a2e583380b3bb99cfe2fbdae1c07b08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-conditional-access-in-azure-active-directory"></a>Práticas recomendadas para o acesso condicional no Azure Active Directory

Este tópico fornece informações sobre o que você deve saber e o que você deve evitar fazer ao configurar políticas de acesso condicional. Antes de ler este tópico, você deve se familiarizar com os conceitos de saudação e terminologia Olá descritas em [acesso condicional no Active Directory do Azure](active-directory-conditional-access-azure-portal.md)

## <a name="what-you-should-know"></a>O que você deve saber

### <a name="whats-required-toomake-a-policy-work"></a>O que é necessário um trabalho de política de toomake?

Quando você cria uma nova política, não há nenhum usuário, grupo, aplicativo ou controle de acesso selecionado.

![Aplicativos na nuvem](./media/active-directory-conditional-access-best-practices/02.png)


toomake sua política de trabalho, você deve configurar a seguir hello:


|O que           | Como                                  | Porque|
|:--            | :--                                  | :-- |
|**Aplicativos na nuvem** |Você precisa de um ou mais aplicativos tooselect.  | meta de saudação de uma política de acesso condicional é tooenable toofine ajustar como os usuários autorizados podem acessar seus aplicativos.|
| **Usuários e grupos** | Você precisa tooselect pelo menos um usuário ou grupo que é autorizado tooaccess Olá aplicativos na nuvem selecionada. | Uma política de acesso condicional que não tenha usuários e grupos atribuídos nunca será disparada. |
| **Controles de acesso** | Você precisa tooselect pelo menos um controle de acesso. | O processador de diretiva precisa tooknow que toodo se as condições forem atendidas.|


Requisitos básicos de adição toothese, em muitos casos, você também deve configurar uma condição. Enquanto uma política também funcionaria sem uma condição configurada, as condições são um fator importante Olá para ajustar o acesso tooyour aplicativos.


![Aplicativos na nuvem](./media/active-directory-conditional-access-best-practices/04.png)



### <a name="how-are-assignments-evaluated"></a>Como as atribuições são avaliadas?

Todas as atribuições são avaliadas com **AND** lógicos. Se você tiver mais de uma atribuição configurada, tootrigger uma política, todas as atribuições devem ser atendidas.  

Se você precisar tooconfigure uma condição de local que se aplica a conexões tooall provenientes de fora da rede da sua organização, você pode fazer isso por:

- Incluindo **todos os locais**
- Excluindo **todos os IPs confiáveis**

### <a name="what-happens-if-you-have-policies-in-hello-azure-classic-portal-and-azure-portal-configured"></a>O que acontece se você tiver políticas no hello portal clássico do Azure e o portal do Azure configurado?  
Ambas as políticas são aplicadas pelo Active Directory do Azure e o usuário Olá obtém acesso somente quando todos os requisitos são atendidos.

### <a name="what-happens-if-you-have-policies-in-hello-intune-silverlight-portal-and-hello-azure-portal"></a>O que acontece se você tiver políticas no hello portal Intune Silverlight e hello Portal do Azure?
Ambas as políticas são aplicadas pelo Active Directory do Azure e o usuário Olá obtém acesso somente quando todos os requisitos são atendidos.

### <a name="what-happens-if-i-have-multiple-policies-for-hello-same-user-configured"></a>O que acontece se eu tiver várias políticas para Olá configurado pelo mesmo usuário?  
Para cada entrada, o Azure Active Directory avalia todas as políticas e garante que todos os requisitos são atendidos antes de usuário de toohello acesso concedido.


### <a name="does-conditional-access-work-with-exchange-activesync"></a>O acesso condicional funciona com o Exchange ActiveSync?

Sim, você não pode usar o Exchange ActiveSync em uma política de acesso condicional.


## <a name="what-you-should-avoid-doing"></a>O que você deve evitar

estrutura de acesso condicional Olá fornece uma excelente flexibilidade. No entanto, grande flexibilidade também significa que você deve rever cuidadosamente cada tooreleasing anterior de política de configuração-resultados indesejáveis tooavoid. Nesse contexto, você deve prestar atenção especial tooassignments afetar conjuntos como **todos os usuários / grupos / aplicativos de nuvem**.

Em seu ambiente, você deve evitar Olá configurações a seguir:


**Para todos os usuários, todos os aplicativos de nuvem:**

- **Bloquear o acesso** - Essa configuração bloqueia toda a organização, o que certamente não é uma boa ideia.

- **Requer dispositivo compatível** - para usuários que não tiverem registrado seus dispositivos ao mesmo tempo, essa política bloqueia o acesso de todos os incluindo acesso toohello Intune portal. Se você for um administrador sem um dispositivo registrado, esta política impede que você voltar para a diretiva de Olá Olá toochange portal do Azure.

- **Exigir o ingresso no domínio** - este bloco de diretiva acesso tem também Olá potencial tooblock acesso para todos os usuários em sua organização se você ainda não tiver um dispositivo ingressado no domínio.


**Para todos os usuários, todos os aplicativos de nuvem, todas as plataformas de dispositivo:**

- **Bloquear o acesso** - Essa configuração bloqueia toda a organização, o que certamente não é uma boa ideia.


## <a name="common-scenarios"></a>Cenários comuns

### <a name="requiring-multi-factor-authentication-for-apps"></a>Exibir a autenticação multifator para aplicativos

Muitos ambientes têm aplicativos que exigem um nível mais alto de proteção que Olá outras pessoas.
Isso acontece, por exemplo, Olá para aplicativos que têm acesso toosensitive dados.
Se você quiser tooadd outra camada de proteção toothese aplicativos, você pode configurar uma política de acesso condicional que requer autenticação multifator quando os usuários acessam esses aplicativos.


### <a name="requiring-multi-factor-authentication-for-access-from-networks-that-are-not-trusted"></a>Exigir autenticação multifator para acesso de redes que não são confiáveis

Esse cenário é semelhante cenário anterior de toohello porque ele adiciona um requisito para autenticação multifator.
No entanto, Olá principal diferença é a condição Olá para este requisito.  
Enquanto o foco de saudação do cenário anterior Olá estava em aplicativos com dados do access toosensitve, Olá foco deste cenário é locais confiáveis.  
Em outras palavras, você pode ter um requisito para autenticação multifator se um aplicativo for acessado por um usuário de uma rede em que você não confia.


### <a name="only-trusted-devices-can-access-office-365-services"></a>Somente os dispositivos confiáveis podem acessar os serviços do Office 365

Se você estiver usando o Intune em seu ambiente, você pode começar imediatamente usando a interface de política de acesso condicional Olá na Olá console do Azure.

Muitos clientes do Intune estão usando tooensure de acesso condicional que somente dispositivos confiáveis podem acessar os serviços do Office 365. Isso significa que os dispositivos móveis registrados com o Intune e atender aos requisitos da política de conformidade e PCs com Windows são tooan ingressado no domínio de local. Das principais melhorias é que você não tem tooset hello mesma política para cada um dos serviços de saudação Office 365.  Quando você cria uma nova política, configure Olá nuvem aplicativos tooinclude cada de saudação O365 aplicativos que você deseja tooprotect com acesso condicional.

## <a name="next-steps"></a>Próximas etapas

Se você quiser tooknow como tooconfigure uma política de acesso condicional, consulte [Introdução ao acesso condicional no Active Directory do Azure](active-directory-conditional-access-azure-portal-get-started.md).
