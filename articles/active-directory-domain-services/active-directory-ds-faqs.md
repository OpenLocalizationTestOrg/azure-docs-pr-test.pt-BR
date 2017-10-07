---
title: aaaFAQs - Azure Active Directory Domain Services | Microsoft Docs
description: "Perguntas frequentes sobre os Serviços de Domínio do Active Directory do Azure"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 48731820-9e8c-4ec2-95e8-83dba1e58775
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: maheshu
ms.openlocfilehash: 42a6d659f6408bf694cb2aa6ec24bff7a76b0565
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-domain-services-frequently-asked-questions-faqs"></a>Azure Active Directory Domain Services: perguntas frequentes
Esta página respostas a perguntas frequentes sobre hello Azure Active Directory Domain Services. Continue verificando as atualizações.

### <a name="troubleshooting-guide"></a>Guia de Solução de Problemas
Consulte tooour [guia de solução de problemas](active-directory-ds-troubleshooting.md) para problemas de toocommon soluções encontrados quando configurar ou administrar os serviços de domínio do AD do Azure.

### <a name="configuration"></a>Configuração
#### <a name="can-i-create-multiple-domains-for-a-single-azure-ad-directory"></a>Posso criar vários domínios para um único diretório do AD do Azure?
Não. Você só pode criar um único domínio atendido pelos Serviços de Domínio do AD do Azure para um único diretório do AD do Azure.  

#### <a name="can-i-enable-azure-ad-domain-services-in-an-azure-resource-manager-virtual-network"></a>Posso habilitar os Serviços de Domínio do Azure AD em uma rede virtual do Azure Resource Manager?
Não. Os Serviços de Domínio do Azure AD só podem ser habilitados em uma rede virtual clássica do Azure. Você pode conectar Olá clássico de rede virtual tooa Gerenciador de recursos rede virtual usando o domínio gerenciado em uma rede virtual do Gerenciador de recursos de toouse emparelhamento de rede virtual.

#### <a name="can-i-enable-azure-ad-domain-services-in-a-federated-azure-ad-directory-i-use-adfs-tooauthenticate-users-for-access-toooffice-365-can-i-enable-azure-ad-domain-services-for-this-directory"></a>É possível habilitar o Azure AD Domain Services em um diretório federado do Azure AD? Eu uso a usuários do AD FS tooauthenticate para acesso tooOffice 365. É possível habilitar o Azure AD Domain Services nesse diretório?
Não. Serviços de domínio do AD do Azure precisam acessar toohello hashes de senha de contas de usuário, os usuários de tooauthenticate por NTLM ou Kerberos. Em um diretório federado, os hashes de senha não são armazenados no diretório do AD do Azure hello. Portanto, o Azure AD Domain Services não funciona nesses diretórios do Azure AD.

#### <a name="can-i-make-azure-ad-domain-services-available-in-multiple-virtual-networks-within-my-subscription"></a>Posso disponibilizar os Azure AD Domain Services em várias redes virtuais na minha assinatura?
serviço Olá em si não oferece suporte diretamente nesse cenário. Os Azure AD Domain Services só estão disponíveis em uma rede virtual de cada vez. No entanto, você pode configurar a conectividade entre várias redes virtuais tooexpose serviços de domínio do AD do Azure tooother redes virtuais. Este artigo descreve como você pode [conectar redes virtuais no Azure](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).

#### <a name="can-i-enable-azure-ad-domain-services-using-powershell"></a>Posso habilitar os Serviços de Domínio do AD do Azure usando o PowerShell?
A implantação do PowerShell/automatizada dos Serviços de Domínio do AD do Azure não está disponível no momento.

#### <a name="is-azure-ad-domain-services-available-in-hello-new-azure-portal"></a>Serviços de domínio do AD do Azure está disponível no novo portal do Azure de Olá?
Não. Serviços de domínio do AD do Azure podem ser definidos somente no hello [portal clássico do Azure](https://manage.windowsazure.com). Esperamos que o suporte a tooextend Olá [portal do Azure](https://portal.azure.com) em Olá futuras.

#### <a name="can-i-add-domain-controllers-tooan-azure-ad-domain-services-managed-domain"></a>É possível adicionar o domínio gerenciado por domínio controladores tooan serviços de domínio do AD do Azure?
Não. domínio Olá fornecido pelos serviços de domínio do AD do Azure é um domínio gerenciado. Você não precisa tooprovision, configurar ou gerenciar controladores de domínio para este domínio - essas atividades são fornecidas como um serviço pela Microsoft de gerenciamento. Portanto, você não pode adicionar mais controladores de domínio (leitura / gravação ou somente leitura) para o domínio gerenciado hello.

### <a name="administration-and-operations"></a>Administração e operações
#### <a name="can-i-connect-toohello-domain-controller-for-my-managed-domain-using-remote-desktop"></a>Pode conectar o controlador de domínio toohello para meu domínio gerenciado usando a área de trabalho remota?
Não. Você não tem permissões tooconnect toodomain controladores Olá gerenciados por meio da área de trabalho remota. Membros Olá ' AAD DC' do grupo de administradores podem administrar o domínio gerenciado hello, usando ferramentas de administração do AD como Olá Active Directory administração ADAC (centro) ou o PowerShell do AD. Essas ferramentas são instaladas usando Olá 'Ferramentas remotas do servidor de administração' recurso em um servidor Windows ingressados no domínio gerenciado toohello.

#### <a name="ive-enabled-azure-ad-domain-services-what-user-account-do-i-use-toodomain-join-machines-toothis-domain"></a>Habilitei os Serviços de Domínio do AD do Azure. Qual conta de usuário usar toodomain ingressar no domínio máquinas toothis?
Os membros do grupo administrativo de saudação 'AAD DC administradores' podem computadores ingressarem no domínio. Além disso, os membros deste grupo recebem toomachines de acesso remoto de área de trabalho que foram toohello ingressado no domínio.

#### <a name="do-i-have-domain-administrator-privileges-for-hello-managed-domain-provided-by-azure-ad-domain-services"></a>É necessário privilégios de administrador de domínio para o domínio gerenciado hello, fornecida pelos serviços de domínio do AD do Azure?
Não. Você não recebem privilégios administrativos no domínio gerenciado hello. Privilégios de administrador do domínio e o administrador da empresa '' não estão disponíveis para você toouse no domínio hello. Administrador de domínio existente ou grupos de administradores de empresa no diretório do AD do Azure também não recebem privilégios de administrador de domínio/enterprise no domínio hello.

#### <a name="can-i-modify-group-memberships-using-ldap-or-other-ad-administrative-tools-on-managed-domains"></a>Posso modificar associações de grupo usando o LDAP ou outras ferramentas administrativas do AD em domínios gerenciados?
Não. Associações de grupo não podem ser modificadas em domínios atendidos pelos Serviços de Domínio do AD do Azure. Olá que mesmo se aplica a atributos de usuário. No entanto, é possível alterar associações de grupo ou atributos de usuário no AD do Azure ou em seu domínio local. Essas alterações são sincronizada automaticamente tooAzure AD os serviços de domínio.

#### <a name="how-long-does-it-take-for-changes-i-make-toomy-azure-ad-directory-toobe-visible-in-my-managed-domain"></a>Quanto tempo leva para que as alterações tornar toomy do Azure AD directory toobe visível no meu domínio gerenciado?
As alterações feitas em seu diretório do AD do Azure usando a saudação da interface do AD do Azure ou o PowerShell são domínio gerenciado tooyour sincronizados. Esse processo de sincronização é executado no plano de fundo de saudação. Após a conclusão da saudação única a sincronização inicial de seu diretório, ele geralmente leva cerca de 20 minutos para que as alterações feitas no AD do Azure toobe refletidas no seu domínio gerenciado.

#### <a name="can-i-extend-hello-schema-of-hello-managed-domain-provided-by-azure-ad-domain-services"></a>Pode estender o esquema Olá Olá domínio gerenciado fornecida pelos serviços de domínio do AD do Azure?
Não. esquema de saudação é administrada pela Microsoft para o domínio gerenciado hello. As extensões de esquema não têm suporte dos Serviços de Domínio do AD do Azure.

#### <a name="can-i-modify-or-add-dns-records-in-my-managed-domain"></a>Posso modificar ou adicionar registros DNS em meu domínio gerenciado?
Sim. Os membros do hello ' AAD controlador de domínio do grupo 'Administradores têm privilégios de administrador do DNS, toomodify os registros DNS no domínio gerenciado hello. Eles podem usar o console do Gerenciador DNS Olá em um computador em execução do Windows Server toohello unidas gerenciado domínio toomanage DNS. Olá toouse console Gerenciador DNS, instale 'Ferramentas do servidor DNS', que faz parte do recurso opcional do hello 'Ferramentas de administração de servidor remoto' no servidor de saudação. Mais informações sobre os [utilitários para administrar, monitorar e solucionar problemas de DNS](https://technet.microsoft.com/library/cc753579.aspx) estão disponíveis no TechNet.

### <a name="billing-and-availability"></a>Disponibilidade e cobrança
#### <a name="is-azure-ad-domain-services-a-paid-service"></a>Os Azure AD Domain Services são um serviço pago?
Sim. Para obter mais informações, consulte Olá [página de preços](https://azure.microsoft.com/pricing/details/active-directory-ds/).

#### <a name="is-there-a-free-trial-for-hello-service"></a>Há uma avaliação gratuita para o serviço Olá?
Esse serviço está incluído na avaliação gratuita de saudação do Azure. Você pode se inscrever para uma [avaliação gratuita de um mês do Azure](https://azure.microsoft.com/pricing/free-trial/).

#### <a name="can-i-get-azure-ad-domain-services-as-part-of-enterprise-mobility-suite-ems-do-i-need-azure-ad-premium-toouse-azure-ad-domain-services"></a>Posso obter os Serviços de Domínio do AD do Azure como parte do EMS (Enterprise Mobility Suite)? Serviços de domínio do Azure AD Premium toouse AD do Azure é necessário?
Não. Os Serviços de Domínio do Azure AD é um serviço pré-pago do Azure e não faz parte do EMS. O Azure AD Domain Services pode ser usado em todas as edições do Azure AD (Free, Basic e Premium). Você será cobrado por hora, dependendo do uso.

#### <a name="what-azure-regions-is-hello-service-available-in"></a>Quais regiões do Azure Olá serviço está disponível em?
Consulte toohello [serviços do Azure por região](https://azure.microsoft.com/regions/#services/) toosee página uma lista de Olá regiões do Azure, onde os serviços de domínio do AD do Azure está disponível.
