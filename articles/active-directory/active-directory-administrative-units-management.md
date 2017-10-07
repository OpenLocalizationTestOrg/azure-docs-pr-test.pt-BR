---
title: "visualização de gerenciamento de unidades aaaAdministrative no Active Directory do Azure"
description: "Usando unidades administrativas para delegação mais granular de permissões no Active Directory do Azure"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 8464cd6b-1d1a-470d-a4fb-ee29b8eab4c4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/17/2017
ms.author: curtand
ms.reviewer: elkuzmen
ms.custom: oldportal;it-pro;
ms.openlocfilehash: ee2c7beb6f9f6292bbf3cdeab00801ac066ae0e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="administrative-units-management-in-azure-ad---public-preview"></a>Gerenciamento de unidades administrativas no Azure AD – visualização pública
Este artigo descreve as unidades administrativas – um novo contêiner do Active Directory do Azure de recursos que podem ser usados para delegar permissões administrativas em subconjuntos de usuários e aplicar subconjunto tooa de políticas de usuários. No Active Directory do Azure, unidades administrativas permitem que os administradores dos administradores centrais toodelegate permissões tooregional ou tooset política em um nível granular.

Isso é útil em organizações com divisões independentes, por exemplo, uma grande universidade que é composta de muitas escolas independentes (Faculdade de Administração, Faculdade de Engenharia e assim por diante) que são independentes umas das outras. Essas divisões têm seus próprios administradores de TI que controlam o acesso, gerenciam usuários e definem políticas especificamente para sua divisão. Os administradores centrais deseja conceder capaz de toobe essas permissões de administradores divisionais usuários Olá em suas divisões particulares. Mais especificamente, usando este exemplo, um administrador central pode, por exemplo, criar uma unidade administrativa para uma escola específica (escola de negócios) e preenchê-la com apenas Olá Business usuários da escola. Em seguida, um administrador central pode adicionar escola de negócios Olá equipe tooa escopo função, Olá de concessão em outras palavras, a equipe de TI de permissões administrativas de escola de negócios somente pela unidade administrativa da escola de negócios de saudação.

> [!IMPORTANT]
> Você poderá atribuir funções de administrador com escopo de unidade administrativa somente se você habilitar o Azure Active Directory Premium. Para saber mais, consulte [Introdução ao AD Premium do Azure](active-directory-get-started-premium.md).
>


Do ponto de vista do administrador central hello, uma unidade administrativa é um objeto de diretório que pode ser criado e populado com recursos. **Nesta versão de pré-visualização, esses recursos podem ser somente os usuários.** Depois de criada e preenchida, unidade administrativa Olá pode ser usada como uma saudação de toorestrict escopo permissão concedida somente sobre os recursos contidos na unidade administrativa hello.

## <a name="managing-administrative-units"></a>Gerenciando unidades administrativas
Nesta versão de visualização, você pode criar e gerenciar unidades administrativas usando cmdlets do hello Azure módulo Active Directory para Windows PowerShell. toolearn mais informações sobre como toodo que consulte [trabalhando com unidades administrativas](https://docs.microsoft.com/powershell/azure/active-directory/working-with-administrative-units?view=azureadps-2.0)

Para obter mais informações sobre requisitos de software e instalar módulo de saudação do AD do Azure e para obter informações sobre Olá cmdlets do módulo AD do Azure para gerenciar unidades administrativas, incluindo sintaxe, parâmetro descrições e exemplos, consulte [ativa do Azure PowerShell de diretório](https://docs.microsoft.com/powershell/azure/active-directory/overview?view=azureadps-2.0).

## <a name="next-steps"></a>Próximas etapas
[Edições do Active Directory do Azure](active-directory-editions.md)
