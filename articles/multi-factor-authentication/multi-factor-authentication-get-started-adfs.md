---
title: "verificação de aaaTwo etapa e o AD FS - Azure MFA | Microsoft Docs"
description: "Esta é hello Azure multi-Factor authentication página que descreve como tooget iniciada com o Azure MFA e AD FS."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 44fbba68-6cf9-46c1-a9df-736580b68ae3
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/23/2017
ms.author: kgremban
ms.openlocfilehash: 7c1c925039d3cb753ba60e286168e5869faeae4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-and-active-directory-federation-services"></a>Introdução ao Azure Multi-Factor Authentication e aos Serviços de Federação do Active Directory
<center>![Nuvem](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center>

Caso organização tenha federado seu Active Directory local com o Azure Active Directory usando o AD FS, existem duas opções para usar a Autenticação Multifator do Azure.

* Proteger os recursos de nuvem usando o Azure Multi-Factor Authentication ou os Serviços de Federação do Active Directory
* Proteger os recursos de nuvem e locais usando o Servidor Azure Multi-Factor Authentication

Olá a tabela a seguir resume a experiência de verificação de saudação entre a captação de recursos com autenticação multifator do Azure e o AD FS

| Experiência de verificação – Aplicativos baseados em navegador | Experiência de verificação – Aplicativos não baseados em navegador |
|:--- |:--- |:--- |
| Protegendo os recursos do AD do Azure usando o Azure Multi-Factor Authentication |<li>Olá a primeira etapa de verificação é realizada usando o AD FS no local.</li> <li>Olá segunda etapa é um método baseado em telefone realizado usando a autenticação de nuvem.</li> |
| Protegendo recursos do AD do Azure usando os Serviços de Federação do Active Directory |<li>Olá a primeira etapa de verificação é realizada usando o AD FS no local.</li><li>Olá segunda etapa é realizado no local, cumprindo a declaração de saudação.</li> |

Advertências sobre senhas de aplicativo para usuários federados:

* Senhas de aplicativo são verificadas usando a autenticação na nuvem e, portanto, ignora as federações. A federação só é usada ativamente ao configurar a senha de aplicativo.
* As configurações do Controle de Acesso do Cliente local não são consideradas pela Senha de aplicativo.
* Você perde a capacidade de registro de autenticação local para senha de aplicativo.
* Desabilitar/excluir a conta pode levar horas toothree para sincronização de diretórios, atrasando o desabilitar/excluir das senhas de aplicativo na identidade de nuvem hello.

## <a name="next-steps"></a>Próximas etapas
Para obter informações sobre como configurar a autenticação multifator do Azure ou Olá servidor Azure multi-Factor Authentication com o AD FS, consulte Olá artigos a seguir:

* [Proteger os recursos de nuvem usando o Azure Multi-Factor Authentication e o AD FS](multi-factor-authentication-get-started-adfs-cloud.md)
* [Proteger recursos de nuvem e locais usando o Servidor Azure Multi-Factor Authentication com o AD FS do Windows Server 2012 R2](multi-factor-authentication-get-started-adfs-w2k12.md)
* [Proteger recursos de nuvem e locais usando o Servidor Azure Multi-Factor Authentication com AD FS 2.0](multi-factor-authentication-get-started-adfs-adfs2.md)
