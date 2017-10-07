---
title: "Azure Active Directory Domain Services: Habilitar a delegação restrita de kerberos | Microsoft Docs"
description: "Habilitar a delegação restrita de kerberos nos domínios gerenciados do Azure Active Directory Domain Services"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: d32547c8018dd1f99c992e95a01d2711d460a261
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-kerberos-constrained-delegation-kcd-on-a-managed-domain"></a>Configurar a KCD (delegação Restrita de Kerberos) em um domínio gerenciado
Muitos aplicativos precisam de recursos de tooaccess no contexto de saudação do usuário de saudação. O Active Directory oferece suporte a um mecanismo chamado delegação de Kerberos, que permite que esse caso de uso. Além disso, você pode restringir a delegação para que somente os recursos específicos podem ser acessados no contexto de saudação do usuário de saudação. Os domínios gerenciados do Azure AD Domain Services são diferentes dos domínios tradicionais do Active Directory, pois estão bloqueados com mais segurança.

Este artigo mostra como o kerberos tooconfigure restrita delegação em um domínio gerenciado do serviços de domínio do AD do Azure.

## <a name="kerberos-constrained-delegation-kcd"></a>KCD (delegação restrita de Kerberos)
Delegação Kerberos permite que uma conta tooimpersonate outro recursos de tooaccess principal (como um usuário) de segurança. Considere um aplicativo web que acessa uma API da web de back-end no contexto de saudação do usuário. Neste exemplo, hello aplicativo web (em execução no contexto de saudação de uma conta de serviço ou uma conta de computador ou da máquina) representa Olá usuário ao acessar o recurso de saudação (back-end da web API). A delegação Kerberos é insegura, pois não restringir Olá Olá recursos representando a conta pode acessar no contexto de saudação do usuário de saudação.

Delegação restringido de Kerberos (KCD) restringe Olá serviços/recursos toowhich Olá determinado servidor pode agir em nome de saudação de um usuário. Tradicional KCD exige tooconfigure de privilégios de administrador de domínio uma conta de domínio para um serviço e restringe o domínio único do hello conta tooa.

A KCD tradicional também tem alguns problemas associados. Em sistemas operacionais anteriores em que o administrador de domínio Olá configurado serviço hello, o administrador de serviços de saudação não tinha nenhum tooknow de maneira útil quais serviços front-end delegado toohello serviços de recurso que eles tinham. E qualquer serviço front-end que pudesse ser delegado tooa serviço de recurso representava um ponto de ataque potencial. Se um servidor que hospedasse um serviço front-end fosse comprometido, e ele foi configurado toodelegate tooresource services, serviços de recurso de saudação também poderiam ser comprometidos.

> [!NOTE]
> Em um domínio gerenciado do Azure AD Domain Services, você não tem privilégios de administrador de domínio. Portanto, **não é possível configurar uma KCD tradicional em um domínio gerenciado**. Use o KCD baseado em recursos conforme descrito neste artigo. Esse mecanismo também é mais seguro.
>
>

## <a name="resource-based-kerberos-constrained-delegation"></a>Delegação restrita de kerberos baseada em recursos
No Windows Server 2012 R2 e Windows Server 2012, a delegação Olá capacidade tooconfigure restringido para o serviço de saudação foi transferida do administrador de serviço toohello do administrador de domínio hello. Dessa forma, o administrador do serviço de back-end Olá pode permitir ou negar serviços front-end. Esse modelo é conhecido como **delegação restrita de kerberos baseada em recursos**.

A KCD Com base em recursos é configurado usando o PowerShell. Você usa Olá Set-ADComputer ou os cmdlets Set-ADUser, dependendo se o hello representando a conta é uma conta de computador ou uma conta de serviço/conta de usuário.

### <a name="configure-resource-based-kcd-for-a-computer-account-on-a-managed-domain"></a>Configurar a KCD baseada em recursos para uma conta de computador em um domínio gerenciado
Suponha que você tenha um aplicativo web em execução no computador de saudação ' contoso100-webapp.contoso100.com'. Precisa de recursos de saudação tooaccess (uma API da web em execução no ' contoso100-api.contoso100.com') no contexto de saudação de usuários do domínio. Veja como você pode configurar a KCD baseada em recursos para esse cenário.

```
$ImpersonatingAccount = Get-ADComputer -Identity contoso100-webapp.contoso100.com
Set-ADComputer contoso100-api.contoso100.com -PrincipalsAllowedToDelegateToAccount $ImpersonatingAccount
```

### <a name="configure-resource-based-kcd-for-a-user-account-on-a-managed-domain"></a>Configurar a KCD baseada em recursos para uma conta de usuário em um domínio gerenciado
Suponha que você tiver um aplicativo web em execução como uma conta de serviço 'appsvc' e ele precisa de recurso de saudação tooaccess (uma API da web em execução como uma conta de serviço - 'backendsvc') no contexto de saudação de usuários do domínio. Veja como você pode configurar a KCD baseada em recursos para esse cenário.

```
$ImpersonatingAccount = Get-ADUser -Identity appsvc
Set-ADUser backendsvc -PrincipalsAllowedToDelegateToAccount $ImpersonatingAccount
```

## <a name="related-content"></a>Conteúdo relacionado
* [Serviços de Domínio do Azure AD - guia de Introdução](active-directory-ds-getting-started.md)
* [Visão geral da Delegação Restrita de Kerberos](https://technet.microsoft.com/library/jj553400.aspx)
