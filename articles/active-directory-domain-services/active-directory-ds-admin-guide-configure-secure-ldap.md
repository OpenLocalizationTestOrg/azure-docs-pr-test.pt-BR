---
title: "aaaConfigure seguro LDAP (LDAPS) nos serviços de domínio do AD do Azure | Microsoft Docs"
description: "Configurar o LDAP Seguro (LDAPS) para um domínio gerenciado dos Serviços de Domínio do Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: 99e44d917b115d7f7a67ff0a5e22c5c9165287e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a>Configurar o LDAPS (LDAP Seguro) para um domínio gerenciado do Azure AD Domain Services
Este artigo mostra como você pode habilitar o protocolo LDAPS para seu domínio gerenciado dos Serviços de Domínio do Azure AD. O LDAP Seguro também é conhecido como “LDAP sobre protocolo SSL/TLS”.

## <a name="before-you-begin"></a>Antes de começar
tarefas de saudação tooperform listadas neste artigo, você precisa:

1. Uma **assinatura do Azure**válida.
2. Um **diretório do AD do Azure** - seja sincronizado com um diretório local ou com um diretório somente na nuvem.
3. **Serviços de domínio do AD do Azure** devem estar habilitados para diretório de saudação do AD do Azure. Se você ainda não tiver feito isso, siga todas as tarefas de saudação descritas Olá [guia de Introdução](active-directory-ds-getting-started.md).
4. Um **LDAP seguro de certificados toobe usado tooenable**.

   * **Recomendado** - Obtenha um certificado da uma autoridade de certificação pública confiável. Essa opção de configuração é a mais segura.
   * Como alternativa, você também pode escolher muito[criar um certificado autoassinado](#task-1---obtain-a-certificate-for-secure-ldap) conforme mostrado neste artigo.

<br>

### <a name="requirements-for-hello-secure-ldap-certificate"></a>Requisitos de certificado LDAP seguro Olá
Adquira um certificado válido por Olá seguindo as diretrizes, antes de ativar o LDAP seguro. Você encontrar falhas, se você tentar tooenable LDAP seguro para seu domínio gerenciado com um certificado inválido/incorreto.

1. **Emissor confiável** -Olá certificado deve ser emitido por uma autoridade confiada por computadores que se conectam toohello domínio gerenciado usando o LDAP seguro. Essa autoridade pode ser uma autoridade de certificação pública de confiança nesses computadores.
2. **Tempo de vida** -certificado Olá deve ser válido para pelo menos Olá próximos 3 a 6 meses. Seguro LDAP acesso tooyour domínio gerenciado será interrompido quando Olá certificado expira.
3. **Nome da entidade** -nome de requerente Olá certificado Olá deve ser um caractere curinga para o domínio gerenciado. Por exemplo, se seu domínio é denominado 'contoso100.com', nome da entidade do certificado Olá deve ser ' *. contoso100.com'. Definir Olá DNS (nome alternativo da entidade) toothis curinga nome.
4. **Uso de chave** - certificado Olá deve ser configurado para Olá a seguir usa - assinaturas digitais e codificação de chave.
5. **Finalidade do certificado** -certificado Olá deve ser válido para autenticação de servidor SSL.

> [!NOTE]
> **Autoridades de Certificação Corporativas:** o Azure AD Domain Services não dá suporte ao uso de certificados LDAP seguros emitidos pela autoridade de certificação corporativa de sua organização. Essa restrição é porque o serviço de saudação não confia em sua autoridade de certificação como uma autoridade de certificação raiz. 
>
>

<br>

## <a name="task-1---obtain-a-certificate-for-secure-ldap"></a>Tarefa 1 – obter um certificado para LDAP seguro
tarefa de primeiro Olá envolve obtendo um certificado usado para proteger LDAP acesso toohello domínio gerenciado. Você tem duas opções:

* Obtenha um certificado de uma autoridade de certificação. autoridade Olá pode ser uma autoridade de certificação pública.
* Crie um certificado autoassinado.

### <a name="option-a-recommended---obtain-a-secure-ldap-certificate-from-a-certification-authority"></a>Opção A (recomendada) - obter um certificado LDAP seguro de uma autoridade de certificação
Se sua organização obtém seus certificados de uma autoridade de certificação pública, será necessário tooobtain Olá seguro LDAP de certificados de autoridade de certificação pública.

Ao solicitar um certificado, certifique-se de que você atenda a todos os requisitos de saudação descritos na [requisitos de certificado LDAP seguro Olá](#requirements-for-the-secure-ldap-certificate).

> [!NOTE]
> Computadores cliente que precisam tooconnect toohello domínio gerenciado usando o LDAP seguro devem confiar emissor de saudação do certificado LDAP seguro hello.
>
>

### <a name="option-b---create-a-self-signed-certificate-for-secure-ldap"></a>Opção B - criar um certificado autoassinado para LDAP seguro
Se você não espera toouse um certificado de uma autoridade de certificação pública, você pode escolher toocreate um certificado autoassinado para LDAP seguro.

**Criar um certificado autoassinado usando o PowerShell**

No seu computador Windows, abra uma nova janela do PowerShell como **administrador** e Olá tipo seguindo comandos, toocreate um novo certificado autoassinado.

    $lifetime=Get-Date

    New-SelfSignedCertificate -Subject *.contoso100.com -NotAfter $lifetime.AddDays(365) -KeyUsage DigitalSignature, KeyEncipherment -Type SSLServerAuthentication -DnsName *.contoso100.com

Olá anterior de exemplo, substitua '*. contoso100.com' com o nome de domínio DNS Olá do seu domínio gerenciado. Por exemplo, se você criou um domínio gerenciado chamado 'contoso100.onmicrosoft.com', substitua '*. contoso100.com' em Olá acima script com ' *. contoso100.onmicrosoft.com').

![Selecionar um diretório do AD do Azure](./media/active-directory-domain-services-admin-guide/secure-ldap-powershell-create-self-signed-cert.png)

certificado autoassinado Olá recém-criado é colocado no repositório de certificados do computador local hello.


## <a name="next-step"></a>Próxima etapa
[Tarefa 2: exportar Olá seguro LDAP certificado tooa. Arquivo PFX](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md)
