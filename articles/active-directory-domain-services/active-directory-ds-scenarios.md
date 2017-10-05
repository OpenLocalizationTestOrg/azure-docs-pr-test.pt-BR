---
title: "Azure Active Directory Domain Services: cenários de implantação | Microsoft Docs"
description: "Cenários de implantação dos Serviços de Domínio do Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c5216ec9-4c4f-4b7e-830b-9d70cf176b20
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: maheshu
ms.openlocfilehash: 72514dabf3af0b282d1bb49c542c13f7095e03d8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="deployment-scenarios-and-use-cases"></a>Cenários de implantação e casos de uso
Nesta seção, examinamos alguns cenários e casos de uso que podem aproveitar os Serviços de Domínio do AD (Azure Active Directory).

## <a name="secure-easy-administration-of-azure-virtual-machines"></a>Administração segura e fácil de máquinas virtuais do Azure
Você pode usar os Serviços de Domínio do Azure Active Directory para gerenciar as máquinas virtuais do Azure de forma simplificada. As máquinas virtuais do Azure pode ser associadas ao domínio gerenciado, permitindo que você use suas credenciais corporativas do AD para fazer logon. Essa abordagem ajuda a evitar problemas de gerenciamento de credenciais, como manutenção de contas de administrador local em cada uma de suas máquinas virtuais do Azure.

Máquinas virtuais do servidor que ingressaram no domínio gerenciado também podem ser gerenciadas e protegidas usando a Política de Grupo. Você pode aplicar linhas de base de segurança necessária para as máquinas virtuais do Azure e bloquear de acordo com as diretrizes de segurança corporativa. Por exemplo, você pode usar os recursos de gerenciamento da Política de Grupo para restringir os tipos de aplicativos que podem ser iniciados nessas máquinas virtuais.

![Administração simplificada de máquinas virtuais do Azure](./media/active-directory-domain-services-scenarios/streamlined-vm-administration.png)

Conforme servidores e outras infraestruturas atingem o fim da vida útil, a Contoso está movendo muitos aplicativos atualmente hospedados no local para a nuvem. O padrão de TI atual exige que os servidores que hospedam aplicativos corporativos estejam ingressados no mesmo domínio e gerenciados usando a Política de Grupo. O administrador de TI da Contoso prefere associar máquinas virtuais ao domínio implantadas no Azure, para facilitar a administração. Como resultado, os administradores e usuários podem fazer logon usando suas credenciais corporativas. Ao mesmo tempo, as máquinas podem ser configuradas de acordo com as linhas de base de segurança necessárias usando a Política de Grupo. A Contoso prefere não ter que implantar, monitorar e gerenciar controladores de domínio no Azure para proteger máquinas virtuais do Azure. Portanto, os Serviços de Domínio do Azure AD são uma grande vantagem para esse caso de uso.

**Observações de implantação**

Considere os seguintes pontos importantes para este cenário de implantação:

* Domínios gerenciados fornecidos pelos Serviços de Domínio do Azure AD fornecem uma única estrutura de UO (unidade organizacional) simples por padrão. Todos os computadores que ingressaram no domínio residem em uma única UO simples. No entanto, você pode optar por criar UOs personalizadas.
* Os Serviços de Domínio do AD do Azure dão suporte à política de grupo simples na forma de um GPO interno para os usuários e um para os contêineres de computador. Você pode criar GPOs personalizados e direcioná-los às UOs personalizadas.
* Os Serviços de Domínio do AD do Azure dão suporte ao esquema do objeto de computador AD base. Você não pode estender o esquema do objeto de computador.

## <a name="lift-and-shift-an-on-premises-application-that-uses-ldap-bind-authentication-to-azure-infrastructure-services"></a>Fazer a mudança de aplicativos locais que usam autenticação de associação LDAP para os Serviços de Infraestrutura do Azure
![Associação LDAP](./media/active-directory-domain-services-scenarios/ldap-bind.png)

A Contoso tem um aplicativo local que foi comprado de um ISV há muitos anos. O aplicativo está atualmente no modo de manutenção pelo ISV e a solicitação de alterações no aplicativo é extremamente dispendioso para Contoso. Este aplicativo tem um front-end baseado na Web que coleta credenciais de usuário usando um formulário da Web e autentica usuários executando uma associação LDAP para o Active Directory corporativo. A Contoso deseja migrar esse aplicativo para os Serviços de Infraestrutura do Azure. É recomendável que o aplicativo funcione como está, sem exigir nenhuma alteração. Além disso, os usuários devem ser capazes de autenticar usando suas credenciais corporativas existentes e sem ter que ser treinados novamente para fazer coisas de forma diferente. Em outras palavras, os usuários finais não devem se lembrar de onde o aplicativo está sendo executado e a migração deve ser clara para eles.

**Observações de implantação**

Considere os seguintes pontos importantes para este cenário de implantação:

* Verifique se o aplicativo não precisa modificar/gravar no diretório. Não há suporte a acesso para gravação LDAP para domínios gerenciados fornecidos pelos Serviços de Domínio do Azure AD.
* Você não pode alterar senhas diretamente em relação ao domínio gerenciado. Os usuários finais podem alterar suas senhas ou usando o mecanismo de alteração de senha de autoatendimento do Azure AD ou no diretório local. Essas alterações são automaticamente sincronizadas e disponibilizadas no domínio gerenciado.

## <a name="lift-and-shift-an-on-premises-application-that-uses-ldap-read-to-access-the-directory-to-azure-infrastructure-services"></a>Fazer a mudança de aplicativos locais que usam leitura LDAP para acessar o diretório que leva aos Serviços de Infraestrutura do Azure
A Contoso tem um aplicativo de LOB (linha de negócios) local desenvolvido quase uma década atrás. Esse aplicativo percebe diretórios e foi projetado para funcionar com o AD do Windows Server. O aplicativo usa LDAP (Lightweight Directory Access Protocol) para ler informações/atributos sobre os usuários do Active Directory. O aplicativo não modifica atributos ou gravar no diretório de forma alguma. A Contoso deseja migrar esse aplicativo para os Serviços de Infraestrutura do Azure e desativar o hardware local antigo que atualmente hospeda esse aplicativo. O aplicativo não pode ser reescrito para usar APIs de diretório modernas, como a Graph API do Azure AD baseada em REST. Portanto, uma opção de mudança é desejada por meio da qual o aplicativo possa ser migrado para executar na nuvem sem modificar o código ou reescrever o aplicativo.

**Observações de implantação**

Considere os seguintes pontos importantes para este cenário de implantação:

* Verifique se o aplicativo não precisa modificar/gravar no diretório. Não há suporte a acesso para gravação LDAP para domínios gerenciados fornecidos pelos Serviços de Domínio do Azure AD.
* Verifique se o aplicativo não precisa de um esquema do Active Directory estendido/personalizado. As extensões de esquema não têm suporte nos Serviços de Domínio do AD do Azure.

## <a name="migrate-an-on-premises-service-or-daemon-application-to-azure-infrastructure-services"></a>Migrar um aplicativo de serviço ou daemon do local para os Serviços de Infraestrutura do Azure
Alguns aplicativos consistem em várias camadas, em que uma das camadas precisa realizar chamadas autenticadas para uma camada de back-end, como uma camada de banco de dados. Contas de serviço do Active Directory são usadas para esses casos de uso. Você pode arrastar e deslocar aplicativos para os Serviços de Infraestrutura do Azure e usar os Serviços de Domínio do Azure AD para as necessidades de identidade desses aplicativos. Você pode optar por usar a mesma conta de serviço que é sincronizada do seu diretório local para o Azure AD. Como alternativa, você pode criar primeiro uma UO personalizada e, em seguida, criar uma conta de serviço separada na UO para implantar esses aplicativos.

![Conta de serviço usando WIA](./media/active-directory-domain-services-scenarios/wia-service-account.png)

A Contoso tem um aplicativo personalizado de cofre que inclui um front-end da Web, um SQL Server e um servidor FTP de back-end. A autenticação integrada do Windows de contas de serviço é usada para autenticar o front-end da Web para o servidor FTP. O front-end da Web é configurado para execução como uma conta de serviço. O servidor back-end está configurado para autorizar o acesso da conta de serviço para o front-end da Web. A Contoso prefere não ter que implantar uma máquina virtual do controlador de domínio na nuvem para mover o aplicativo para os Serviços de Infraestrutura do Azure. O administrador de TI da Contoso pode implantar os servidores da Web front-end, o SQL Server e o servidor FTP para máquinas virtuais do Azure. Em seguida, esses computadores são adicionados a um domínio gerenciado do serviços de domínio do Azure AD. Em seguida, eles podem usar a mesma conta de serviço em seu diretório local para fins de autenticação do aplicativo. Essa conta de serviço é sincronizada com o domínio dos Serviços de Domínio do Azure AD e está disponível para uso.

**Observações de implantação**

Considere os seguintes pontos importantes para este cenário de implantação:

* Verifique se o aplicativo usa o nome de usuário e senha para autenticação. A autenticação com certificado/cartão inteligente não tem suporte dos Serviços de Domínio do AD do Azure.
* Você não pode alterar senhas diretamente em relação ao domínio gerenciado. Os usuários finais podem alterar suas senhas ou usando o mecanismo de alteração de senha de autoatendimento do Azure AD ou no diretório local. Essas alterações são automaticamente sincronizadas e disponibilizadas no domínio gerenciado.

## <a name="windows-server-remote-desktop-services-deployments-in-azure"></a>Implantações de serviços de área de trabalho remota do Windows Server
Você pode usar o Azure AD Domain Services para fornecer serviços de domínio do AD gerenciados aos servidores de área de trabalho remota implantados no Azure.

Para saber mais sobre esse cenário de implantação, confira [Integrate Azure AD Domain Services with your RDS deployment](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-azure-adds) (Integrar o Azure AD Domain Services à sua implantação do RDS).
