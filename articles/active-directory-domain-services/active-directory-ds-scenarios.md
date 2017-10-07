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
ms.openlocfilehash: 8a64bd8f7c6eba8f6490e10fa62bef195b6b3d5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-scenarios-and-use-cases"></a>Cenários de implantação e casos de uso
Nesta seção, examinamos alguns cenários e casos de uso que podem aproveitar os Serviços de Domínio do AD (Azure Active Directory).

## <a name="secure-easy-administration-of-azure-virtual-machines"></a>Administração segura e fácil de máquinas virtuais do Azure
Você pode usar o Azure Active Directory Domain Services toomanage suas máquinas virtuais do Azure de forma simplificada. Máquinas virtuais do Azure pode ser o domínio gerenciado toohello unidas, permitindo que você toouse seu AD corporativa credenciais toolog no. Essa abordagem ajuda a evitar problemas de gerenciamento de credenciais, como manutenção de contas de administrador local em cada uma de suas máquinas virtuais do Azure.

Máquinas virtuais de servidor que toohello ingressado no domínio de gerenciado também possa ser gerenciadas e protegidas usando a diretiva de grupo. Você pode aplicar linhas de base de segurança necessário tooyour virtuais do Azure máquinas e bloqueie acordo com as diretrizes de segurança corporativa. Por exemplo, você pode usar o grupo gerenciamento recursos toorestrict Olá tipos de política de aplicativos que podem ser iniciados nessas máquinas virtuais.

![Administração simplificada de máquinas virtuais do Azure](./media/active-directory-domain-services-scenarios/streamlined-vm-administration.png)

Como servidores e outra infraestrutura atingir o fim da vida útil, a Contoso é mover muitos aplicativos atualmente hospedados na nuvem de toohello local. O padrão de TI atual exige que os servidores que hospedam aplicativos corporativos estejam ingressados no mesmo domínio e gerenciados usando a Política de Grupo. A Contoso administrador de TI prefere toodomain junção VMs implantadas no Azure, toomake administração mais fácil. Como resultado, os administradores e usuários podem fazer logon usando suas credenciais corporativas. Em Olá mesmo tempo, as máquinas podem estar toocomply configurado com linhas de base de segurança necessárias usando a diretiva de grupo. A Contoso prefere não toohave toodeploy, monitorar e gerenciar controladores de domínio no Azure toosecure máquinas virtuais do Azure. Portanto, os Serviços de Domínio do Azure AD são uma grande vantagem para esse caso de uso.

**Observações de implantação**

Considere Olá pontos importantes para este cenário de implantação a seguir:

* Domínios gerenciados fornecidos pelos Serviços de Domínio do Azure AD fornecem uma única estrutura de UO (unidade organizacional) simples por padrão. Todos os computadores que ingressaram no domínio residem em uma única UO simples. No entanto você pode escolher toocreate OUs personalizadas.
* Serviços de domínio do AD do Azure dá suporte à política de grupo simples na forma de saudação de um interno GPO cada Olá usuários e computadores contêineres. Você pode criar GPOs personalizados e de destino-los toocustom UOs.
* Serviços de domínio do AD do Azure dá suporte a esquema de objeto de computador do hello base AD. Você não pode estender o esquema do objeto de computador hello.

## <a name="lift-and-shift-an-on-premises-application-that-uses-ldap-bind-authentication-tooazure-infrastructure-services"></a>Comparação de precisão e shift um aplicativo local que usa LDAP bind autenticação tooAzure serviços de infraestrutura
![Associação LDAP](./media/active-directory-domain-services-scenarios/ldap-bind.png)

A Contoso tem um aplicativo local que foi comprado de um ISV há muitos anos. aplicativo Hello está atualmente em modo de manutenção Olá ISV e aplicativo solicitante de toohello de alterações é extremamente dispendioso para Contoso. Este aplicativo possui um front-end baseado na web que coleta credenciais de usuário usando um formulário da web e, em seguida, autentica usuários executando um toohello de ligação LDAP corporativo do Active Directory. A Contoso deseja toomigrate tooAzure esse aplicativo Serviços de infraestrutura. É recomendável que o aplicativo hello funciona como está, sem exigir nenhuma alteração. Além disso, os usuários devem ser capaz de tooauthenticate usando suas credenciais corporativas existentes e sem ter tooretrain coisas que os usuários toodo diferente. Em outras palavras, os usuários finais devem ser óbvia de onde o aplicativo hello está sendo executado e migração Olá deve ser toothem transparente.

**Observações de implantação**

Considere Olá pontos importantes para este cenário de implantação a seguir:

* Certifique-se de que o aplicativo hello não necessário toohello toomodify/gravar no diretório. Não há suporte para domínios de toomanaged de acesso de gravação LDAP fornecidos pelos serviços de domínio do AD do Azure.
* Você não pode alterar as senhas diretamente no domínio gerenciado hello. Os usuários finais podem alterar sua senha ou usando o mecanismo de alteração de senha de autoatendimento do AD do Azure ou em relação ao diretório de local de saudação. Essas alterações são automaticamente sincronizados e disponível no domínio gerenciado hello.

## <a name="lift-and-shift-an-on-premises-application-that-uses-ldap-read-tooaccess-hello-directory-tooazure-infrastructure-services"></a>Shift e comparação de precisão de um aplicativo local que usa LDAP leitura tooaccess Olá diretório tooAzure serviços de infraestrutura
A Contoso tem um aplicativo de LOB (linha de negócios) local desenvolvido quase uma década atrás. Esse aplicativo com reconhecimento de diretório e foi projetado toowork com o Windows Server AD. aplicativo Hello usa LDAP (Lightweight Directory Access Protocol) tooread/atributos de informação sobre os usuários do Active Directory. aplicativo Hello não modificar atributos ou caso contrário gravação toohello directory. A Contoso deseja toomigrate tooAzure esse aplicativo Serviços de infraestrutura e desativar o hardware de local de classificação por vencimento Olá hospedando este aplicativo. aplicativo Hello não pode ser regravada toouse modernos diretório APIs como Olá baseado em REST API do Azure AD Graph. Portanto, uma opção de comparação de precisão e shift é desejada pelo qual o aplicativo hello pode ser migrado toorun na nuvem hello, sem modificar o código ou reescrever o aplicativo hello.

**Observações de implantação**

Considere Olá pontos importantes para este cenário de implantação a seguir:

* Certifique-se de que o aplicativo hello não necessário toohello toomodify/gravar no diretório. Não há suporte para domínios de toomanaged de acesso de gravação LDAP fornecidos pelos serviços de domínio do AD do Azure.
* Certifique-se de que o aplicativo hello não é necessário um esquema do Active Directory estendido personalizado. As extensões de esquema não têm suporte nos Serviços de Domínio do AD do Azure.

## <a name="migrate-an-on-premises-service-or-daemon-application-tooazure-infrastructure-services"></a>Migrar um local daemon ou o serviço de aplicativo tooAzure serviços de infraestrutura
Alguns aplicativos consistem em várias camadas, onde uma das camadas de saudação precisa de camada de back-end do tooperform chamadas autenticadas tooa como uma camada de banco de dados. Contas de serviço do Active Directory são usadas para esses casos de uso. Possível comparação de precisão e shift tais aplicativos tooAzure serviços de infraestrutura e usar serviços de domínio do AD do Azure para necessidades de identidade Olá desses aplicativos. Você pode escolher toouse Olá a mesma conta de serviço que é sincronizada do seu diretório de local tooAzure AD. Como alternativa, você pode criar primeiro uma OU personalizada e, em seguida, criar uma conta de serviço separada daquela ou, toodeploy esses aplicativos.

![Conta de serviço usando WIA](./media/active-directory-domain-services-scenarios/wia-service-account.png)

A Contoso tem um aplicativo personalizado de cofre que inclui um front-end da Web, um SQL Server e um servidor FTP de back-end. Autenticação integrada do Windows de contas de serviço é servidor de toohello FTP tooauthenticate usado Olá web front-end. Olá web front-end está configurado toorun como uma conta de serviço. Olá servidor back-end está configurado tooauthorize acesso da conta de serviço Olá Olá web front-end. A Contoso prefere não toohave toodeploy uma máquina de virtual do controlador de domínio no hello nuvem toomove tooAzure esse aplicativo Serviços de infraestrutura. A Contoso administrador de TI pode implantar os servidores de Olá Olá web front-end, o SQL server e máquinas virtuais do hello FTP server tooAzure de hospedagem. Essas máquinas são unida tooan dos serviços de domínio do AD do Azure gerenciado domínio. Em seguida, eles podem usar Olá a mesma conta de serviço em seu diretório local para fins de autenticação do aplicativo hello. Essa conta de serviço é o domínio gerenciado do serviços de domínio do AD do Azure toohello sincronizada e está disponível para uso.

**Observações de implantação**

Considere Olá pontos importantes para este cenário de implantação a seguir:

* Certifique-se de que o aplicativo hello usa nome de usuário e senha para autenticação. A autenticação com certificado/cartão inteligente não tem suporte dos Serviços de Domínio do AD do Azure.
* Você não pode alterar as senhas diretamente no domínio gerenciado hello. Os usuários finais podem alterar sua senha ou usando o mecanismo de alteração de senha de autoatendimento do AD do Azure ou em relação ao diretório de local de saudação. Essas alterações são automaticamente sincronizados e disponível no domínio gerenciado hello.

## <a name="windows-server-remote-desktop-services-deployments-in-azure"></a>Implantações de serviços de área de trabalho remota do Windows Server
Você pode usar os serviços de domínio do AD do Azure tooprovide gerenciados AD tooyour servidores da área de trabalho remota implantados no Azure de serviços de domínio.

Para obter mais informações sobre esse cenário de implantação, consulte como muito[integrar serviços de domínio do AD do Azure com a implantação de RDS](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/rds-azure-adds).
