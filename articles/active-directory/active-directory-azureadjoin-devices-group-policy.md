---
title: "passa por dispositivos que ingressaram no domínio de aaaConnect tooAzure AD para Windows 10 | Microsoft Docs"
description: "Explica como os administradores podem configurar a rede da empresa política de grupo tooenable dispositivos toobe toohello ingressado no domínio."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 2ff29f3e-5325-4f43-9baa-6ae8d6bad3e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 9766aa702352dea2ecad3a9a0bdf8d3286ee6d91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-domain-joined-devices-tooazure-ad-for-windows-10-experiences"></a>Conecte-se a dispositivos que ingressaram no domínio tooAzure AD para experiências do Windows 10
Ingresso no domínio é organizações de maneira tradicional de saudação conectou dispositivos para o trabalho para Olá últimos 15 anos e muito mais. Permitiu que usuários toosign tootheir dispositivos por meio de seu trabalho do Windows Server Active Directory (Active Directory) ou contas de estudante e toofully IT permitido gerenciam esses dispositivos. As organizações normalmente dependem de métodos tooprovision dispositivos toousers de geração de imagens e geralmente usam toomanage de diretiva de grupo ou System Center Configuration Manager (SCCM)-los.


Ingresso no domínio no Windows 10 fornece Olá benefícios a seguir depois de conectar dispositivos tooAzure do Active Directory (AD do Azure):

* Único sign-on (SSO) tooAzure AD recursos em qualquer lugar
* Acessar toohello empresa da Windows Store usando o trabalho ou escola contas (nenhuma conta da Microsoft necessários)
* Roaming de configurações de usuário entre dispositivos compatível com a empresa usando a conta corporativa ou de estudante (sem a exigência de conta da Microsoft)
* Autenticação forte e entrada conveniente para a conta corporativa ou de estudante com o Windows Hello for Business e o Windows Hello
* Capacidade toorestrict acessar apenas toodevices que estão em conformidade com as configurações de política de grupo do dispositivo organizacional

## <a name="prerequisites"></a>Pré-requisitos
Ingresso no domínio continua toobe útil. No entanto, tooget benefícios de saudação do AD do Azure do SSO, roaming de configurações com ou escolar contas e acessar o armazenamento de tooWindows com o trabalho ou de estudante contas, você precisará Olá a seguir:

* Assinatura do Azure AD
* Saudação de tooextend do Azure AD Connect tooAzure diretório AD local
* Diretiva que definiu tooconnect tooAzure de dispositivos que ingressaram no domínio AD
* Compilação do Windows 10 (compilação 10551 ou mais recente) para dispositivos

tooenable Windows Hello for Business e o Windows Hello, também será necessário seguir hello:

- **Infraestrutura de chave pública (PKI)** para a emissão de certificados de usuário.

- **Ramificação atual do System Center Configuration Manager** -você precisa tooinstall versão 1606 ou melhor.  
Para obter mais informações, consulte: 
    - [Documentação para o System Center Configuration Manager](https://technet.microsoft.com/library/mt346023.aspx)
    - [Blog da Equipe do System Center Configuration Manager](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx)
    - [Configurações do Windows Hello for Business no System Center Configuration Manager](https://docs.microsoft.com/sccm/protect/deploy-use/windows-hello-for-business-settings)

Como um requisito de implantação de PKI toohello alternativa, você pode fazer a seguir hello:

* Ter alguns controladores de domínio com os Serviços de Domínio do Active Directory do Windows Server 2016.

tooenable o acesso condicional, você pode criar configurações de diretiva de grupo que permitem que dispositivos que ingressaram no toodomain acesso com nenhuma implantações adicionais. toomanage controle de acesso com base na conformidade de dispositivo hello, você precisará seguir hello:

* Ramificação Atual do System Center Configuration Manager (1606 ou posterior) para cenários do Windows Hello for Business

## <a name="deployment-instructions"></a>Instruções de implantação

toodeploy, siga as etapas de Olá listadas na [como tooconfigure o registro automático do Windows ingressado no domínio dispositivos com o Active Directory do Azure](active-directory-conditional-access-automatic-device-registration-setup.md)

## <a name="next-step"></a>Próxima etapa
* [Windows 10 para a empresa Olá: dispositivos de toouse maneiras de trabalho](active-directory-azureadjoin-windows10-devices-overview.md)
* [Estendendo nuvem dispositivos de tooWindows 10 de recursos por meio de junção do Active Directory do Azure](active-directory-azureadjoin-user-upgrade.md)
* [Saiba mais sobre cenários de uso da Junção do Azure AD](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Conecte-se a dispositivos que ingressaram no domínio tooAzure AD para experiências do Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Configurar a Junção do Azure AD](active-directory-azureadjoin-setup.md)

