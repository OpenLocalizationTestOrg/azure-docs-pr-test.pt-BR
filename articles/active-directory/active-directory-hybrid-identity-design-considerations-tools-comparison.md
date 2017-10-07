---
title: "Identidade Híbrida: comparação de ferramentas de integração de diretório | Microsoft Docs"
description: "Esta página fornece uma tabela abrangente que compara Olá várias ferramentas de integração de diretório que podem ser usadas para a integração de diretório."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 1e62a4bd-4d55-4609-895e-70131dedbf52
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 18ac0a0f58726eceb85510df516e8db71429b313
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-identity-directory-integration-tools-comparison"></a>Comparação de ferramentas de integração de diretório da Identidade Híbrida
Ao longo de anos de saudação ferramentas de integração de diretório Olá crescimento e à evolução.  Este documento é toohelp fornecem uma visão consolidada dessas ferramentas e uma comparação dos recursos de saudação que estão disponíveis em cada um.

<!-- hello hardcoded link is a workaround for campaign ids not working in acom links-->

> [!NOTE]
> Azure AD Connect incorpora componentes hello e funcionalidade lançada anteriormente como Dirsync e AAD Sync. Essas ferramentas não estão sendo lançadas individualmente, e todas as melhorias futuras serão incluídas em atualizações tooAzure AD conectar-se de que, para que você sempre saiba onde tooget Olá funcionalidade mais atual.
> 
> DirSync e Azure AD Sync foram preteridos. Mais informações podem ser encontradas [aqui](active-directory-aadconnect-dirsync-deprecated.md).
> 
> 

Use Olá chave a seguir para cada uma das tabelas de saudação.

● = Disponível Agora  
FR = Versão Futura  
PP = Versão prévia pública  

## <a name="on-premises-toocloud-synchronization"></a>TooCloud sincronização local
| Recurso | Conexão do Active Directory do Azure | Serviços de sincronização do Active Directory do Azure (sincronização do AAD) | Ferramenta de sincronização do Active Directory do Azure (DirSync) | O Forefront Identity Manager 2010 R2 (FIM) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|:---:|
| Conecte-se toosingle floresta do AD local |● |● |● |● |● |
| Conecte-se toomultiple florestas do AD local |● |● | |● |● |
| Conecte-se toomultiple organizações do Exchange local |● | | | | |
| Conecte-se o diretório LDAP toosingle local |FR | | |● |● |
| Conecte-se toomultiple em LDAP diretórios locais |FR | | |● |● |
| Conecte-se tooon local AD e diretórios LDAP locais |FR | | |● |● |
| Conectar sistemas toocustom (ou seja, SQL, Oracle, MySQL, etc.) |FR | | |● |● |
| Sincronize atributos definido pelo cliente (extensões de diretório) |● | | | | |
| Conecte-se HR tooon local (ou seja, SAP, Oracle eBusiness, PeopleSoft) |FR | | |● |● |
| Dá suporte a regras de sincronização do FIM e os conectores para o provisionamento de sistemas locais tooon. | | | |● |● |

## <a name="cloud-tooon-premises-synchronization"></a>Sincronização de tooOn local de nuvem
| Recurso | Conexão do Active Directory do Azure | Serviços de sincronização do Active Directory do Azure | Ferramenta de sincronização do Active Directory do Azure (DirSync) | O Forefront Identity Manager 2010 R2 (FIM) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|:---:|
| Write-back de dispositivos |● | |● | | |
| Write-back de atributo (para implantação híbrida do Exchange) |● |● |● |● |● |
| Write-back de objetos de grupos |● | | | | |
| Write-back de senhas (de redefinição de senha de autoatendimento (SSPR) e alteração de senha) |● |● | | | |

## <a name="authentication-feature-support"></a>Suporte ao recurso de autenticação
| Recurso | Conexão do Active Directory do Azure | Serviços de sincronização do Active Directory do Azure | Ferramenta de sincronização do Active Directory do Azure (DirSync) | O Forefront Identity Manager 2010 R2 (FIM) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|:---:|
| Sincronização de senha para a floresta única do AD local |● |● |● | | |
| Sincronização de senha para várias florestas do AD local |● |● | | | |
| Logon único com federação |● |● |● |● |● |
| Write-back de senhas (de alteração SSPR e senha) |● |● | | | |

## <a name="set-up-and-installation"></a>Instalação e configuração
| Recurso | Conexão do Active Directory do Azure | Serviços de sincronização do Active Directory do Azure | Ferramenta de sincronização do Active Directory do Azure (DirSync) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|
| Oferece suporte à instalação em um controlador de domínio |● |● |● | |
| Oferece suporte à instalação usando o SQL Express |● |● |● | |
| Atualização fácil de DirSync |● | | | |
| Localização de Admin UX tooWindows idiomas do servidor |● |● |● | |
| Localização do usuário final UX tooWindows idiomas do servidor | | | |● |
| Suporte para Windows Server 2008 e Windows Server 2008 R2 |● para sincronização, não para federação |● |● |● |
| Suporte para o Windows Server 2012 e Windows Server 2012 R2 |● |● |● |● |

## <a name="filtering-and-configuration"></a>Filtragem e configuração
| Recurso | Conexão do Active Directory do Azure | Serviços de sincronização do Active Directory do Azure | Ferramenta de sincronização do Active Directory do Azure (DirSync) | O Forefront Identity Manager 2010 R2 (FIM) | Microsoft Identity Manager 2016 (MIM) |
|:--- |:---:|:---:|:---:|:---:|:---:|
| Filtrar em domínios e unidades organizacionais |● |● |● |● |● |
| Filtrar os valores de atributo de objetos |● |● |● |● |● |
| Permitir que o conjunto mínimo de atributos toobe sincronizado (MinSync) |● |● | | | |
| Permitir toobe de modelos de serviço diferentes aplicado para fluxos de atributo |● |● | | | |
| Permite remover atributos que fluem do AD tooAzure AD |● |● | | | |
| Permitir a personalização avançada para fluxos de atributo |● |● | |● |● |

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre [Como integrar suas identidades locais ao Active Directory do Azure](active-directory-aadconnect.md).

