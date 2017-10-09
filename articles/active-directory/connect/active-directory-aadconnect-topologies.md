---
title: 'Azure AD Connect: Topologias com suporte | Microsoft Docs'
description: "Este tópico detalha as topologias com e sem suporte para o Azure AD Connect"
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 1034c000-59f2-4fc8-8137-2416fa5e4bfe
ms.service: active-directory
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: identity
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 41632a54e8e85492fbf1a751ef4e618c8870abe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="topologies-for-azure-ad-connect"></a>Topologias para o Azure AD Connect
Este artigo descreve várias topologias de Azure Active Directory (AD do Azure) que usam a sincronização do Azure AD Connect como solução de integração da chave hello e local. Este artigo inclui configurações com e sem suporte.

Aqui está a legenda Olá para imagens no artigo hello:

| Descrição | Símbolo |
| --- | --- |
| Floresta do Active Directory local |![Floresta do Active Directory local](./media/active-directory-aadconnect-topologies/LegendAD1.png) |
| Active Directory local com importação filtrada |![Active Directory com importação filtrada](./media/active-directory-aadconnect-topologies/LegendAD2.png) |
| Servidor do Azure AD Connect Sync |![Servidor do Azure AD Connect Sync](./media/active-directory-aadconnect-topologies/LegendSync1.png) |
| “Modo de preparo” do servidor de sincronização do Azure AD Connect |![“Modo de preparo” do servidor de sincronização do Azure AD Connect](./media/active-directory-aadconnect-topologies/LegendSync2.png) |
| GALSync com o Forefront Identity Manager (FIM) 2010 ou o Microsoft Identity Manager (MIM) 2016 |![GALSync com o FIM 2010 ou MIM 2016](./media/active-directory-aadconnect-topologies/LegendSync3.png) |
| Servidor do Azure AD Connect Sync detalhado |![Servidor do Azure AD Connect Sync detalhado](./media/active-directory-aadconnect-topologies/LegendSync4.png) |
| AD do Azure |![Azure Active Directory](./media/active-directory-aadconnect-topologies/LegendAAD.png) |
| Cenário sem suporte |![Cenário sem suporte](./media/active-directory-aadconnect-topologies/LegendUnsupported.png) |

## <a name="single-forest-single-azure-ad-tenant"></a>Floresta única, locatário único do Azure AD
![Topologia de uma única floresta e um único locatário](./media/active-directory-aadconnect-topologies/SingleForestSingleDirectory.png)

Olá a topologia mais comum é um único local de floresta, com um ou vários domínios e um único AD do Azure de locatário. Para a autenticação do Azure AD, é usada a sincronização de senha. a instalação expressa saudação do Azure AD Connect oferece suporte a apenas esta topologia.

### <a name="single-forest-multiple-sync-servers-tooone-azure-ad-tenant"></a>Floresta única, vários locatários de tooone AD do Azure de servidores de sincronização
![Topologia sem suporte, filtrada para uma floresta única](./media/active-directory-aadconnect-topologies/SingleForestFilteredUnsupported.png)

Tendo vários servidores de sincronização do Azure AD Connect não há suporte para o locatário conectado toohello mesmo Azure AD, exceto para uma [servidor de preparo](#staging-server). Ele não tem suporte mesmo que esses servidores são toosynchronize configurado com um conjunto de objetos de mutuamente exclusivo. Você pode considerado esta topologia se você não conseguir acessar todos os domínios na floresta de saudação de um único servidor, ou se você quiser toodistribute carga entre vários servidores.

## <a name="multiple-forests-single-azure-ad-tenant"></a>Várias florestas, locatário único do Azure AD
![Topologia de várias florestas e um único locatário](./media/active-directory-aadconnect-topologies/MultiForestSingleDirectory.png)

Muitas organizações têm ambientes com várias florestas do Active Directory local. Há vários motivos para ter mais de uma floresta do Active Directory local. Exemplos típicos são designs com florestas e Olá resultado de uma fusão ou aquisição conta-recurso.

Quando você tem várias florestas, todas elas devem ser acessíveis por um único servidor de sincronização do Azure AD Connect. Você não tem o domínio de tooa toojoin Olá server. Se necessário tooreach todas as florestas, você pode colocar o servidor de saudação em uma rede de perímetro (também conhecida como DMZ, zona desmilitarizada e sub-rede filtrada).

Assistente de instalação de conectar-se de saudação do AD do Azure oferece várias opções tooconsolidate que os usuários que são representados em várias florestas. meta de saudação é que um usuário é representado somente uma vez no AD do Azure. Há algumas topologias comuns que você pode configurar no caminho de instalação personalizada Olá no Assistente de instalação de saudação. Em Olá **identificando exclusivamente seus usuários** página, a opção correspondente do hello select que representa a sua topologia. consolidação de saudação está configurada apenas para os usuários. Grupos duplicados não são consolidados com a configuração padrão de saudação.

As topologias comuns são discutidas nas seções de saudação sobre [separar topologias](#multiple-forests-separate-topologies), [completo malha](#multiple-forests-full-mesh-with-optional-galsync), e [Olá topologia de conta-recurso](#multiple-forests-account-resource-forest).

assume a configuração padrão de saudação na sincronização do Azure AD Connect:

* Cada usuário tem apenas uma conta habilitada e floresta Olá onde esta conta está localizada é o usuário de saudação do tooauthenticate usado. Essa suposição serve para a sincronização de senha e para a federação. UserPrincipalName e sourceAnchor/immutableID vêm desta floresta.
* Cada usuário tem apenas uma caixa de correio.
* floresta de saudação que hospeda a caixa de correio Olá para um usuário tem a melhor qualidade de dados Olá para atributos visíveis na lista de endereços Global (GAL) Exchange de saudação. Se não houver nenhuma caixa de correio do usuário hello, qualquer floresta pode ser usado toocontribute esses valores de atributo.
* Caso tenha uma caixa de correio vinculada, há uma conta em outra floresta usada para entrada.

Se seu ambiente não corresponder a essas considerações, hello acontecem estas coisas:

* Se você tiver mais de uma conta ativa ou a mais de uma caixa de correio, o mecanismo de sincronização de saudação escolhe um e ignora Olá outros.
* Uma caixa de correio vinculada com nenhuma outra conta ativa não é exportado tooAzure AD. conta de usuário de saudação não é representada como um membro em qualquer grupo. Uma caixa de correio vinculada no DirSync é sempre representado como uma caixa de correio normal. Essa alteração é intencionalmente um cenários de várias florestas de suporte de toobetter um comportamento diferente.

Você pode encontrar mais detalhes em [Compreendendo a configuração padrão da saudação](active-directory-aadconnectsync-understanding-default-configuration.md).

### <a name="multiple-forests-multiple-sync-servers-tooone-azure-ad-tenant"></a>Várias florestas, vários locatários de tooone AD do Azure de servidores de sincronização
![Topologia sem suporte para vários servidores de sincronização e de várias florestas](./media/active-directory-aadconnect-topologies/MultiForestMultiSyncUnsupported.png)

Não há suporte para ter mais de uma conexão do AD do Azure sincronização servidor conectado tooa único locatário do AD do Azure. exceção Hello é uso de saudação de um [servidor de preparo](#staging-server).

### <a name="multiple-forests-separate-topologies"></a>Várias florestas, topologias separadas
![Opção para representar os usuários apenas uma vez em todos os diretórios](./media/active-directory-aadconnect-topologies/MultiForestUsersOnce.png)

![Representação de várias florestas e topologias separadas](./media/active-directory-aadconnect-topologies/MultiForestSeperateTopologies.png)

Nesse ambiente, todas as florestas locais são tratadas como entidades separadas. Não há usuários presentes em outras florestas. Cada floresta tem sua própria organização do Exchange, e não há nenhum GALSync entre florestas hello. Esta topologia pode ser situação Olá após uma fusão/aquisição ou em uma organização onde cada unidade de negócios opera de forma independente. Nessas florestas estão em Olá mesma organização no AD do Azure e aparecerá com um GAL unificado. Em Olá anterior imagem, cada objeto em cada floresta é representado uma vez no metaverso hello e agregado no locatário do AD do Azure de destino hello.

### <a name="multiple-forests-match-users"></a>Várias florestas: usuários correspondentes
Tooall comuns esses cenários são essa distribuição e grupos de segurança podem conter uma mistura de usuários, contatos e entidades de segurança externas (FSPs). FSPs são usadas em membros de toorepresent de serviços de domínio Active Directory (AD DS) de outras florestas em um grupo de segurança. Todos os FSPs são objeto real toohello resolvido no AD do Azure.

### <a name="multiple-forests-full-mesh-with-optional-galsync"></a>Várias florestas: malha completa com GALSync opcional
![Opção para usar o atributo de mensagem de saudação para correspondência quando existem identidades de usuários em vários diretórios](./media/active-directory-aadconnect-topologies/MultiForestUsersMail.png)

![Topologia de malha completa para várias florestas](./media/active-directory-aadconnect-topologies/MultiForestFullMesh.png)

Uma topologia de malha completa permite que os usuários e toobe recursos localizados em qualquer floresta. Normalmente, há relações de confiança bidirecionais entre florestas hello.

Se o Exchange estiver presente em mais de uma floresta, poderá haver uma solução GALSync local (opcional). Cada usuário é representado como um contato em todas as outras florestas. GALSync geralmente é implementado por meio do FIM 2010 ou MIM 2016. O Azure AD Connect não pode ser usado para GALSync local.

Nesse cenário, os objetos de identidade são unidos por meio do atributo de mensagem de saudação. Um usuário que tem uma caixa de correio em uma floresta é ingressado com contatos Olá Olá outras florestas.

### <a name="multiple-forests-account-resource-forest"></a>Várias florestas: floresta de recursos de conta
![Opção para usar os atributos de ObjectSID e msExchMasterAccountSID Olá para correspondência quando existem identidades em vários diretórios](./media/active-directory-aadconnect-topologies/MultiForestUsersObjectSID.png)

![Topologia de floresta de conta-recurso para várias florestas](./media/active-directory-aadconnect-topologies/MultiForestAccountResource.png)

Em uma topologia de floresta de conta-recurso, você tem uma ou mais florestas de *conta* com contas de usuário ativas. Você também tem uma ou mais florestas de *recursos* com contas desabilitadas.

Nesse cenário, uma (ou mais) floresta de recursos confia em todas as florestas de conta. floresta de recursos Olá geralmente tem um esquema do Active Directory estendido com o Exchange e Lync. Todos os serviços do Exchange e do Lync, bem como outros serviços compartilhados, estão localizados nessa floresta. Os usuários têm uma conta de usuário desabilitada nessa floresta e está vinculada a caixa de correio Olá toohello floresta de conta.

## <a name="office-365-and-topology-considerations"></a>Office 365 e considerações de topologia
Algumas cargas de trabalho do Office 365 têm certas restrições em topologias com suporte:

| Carga de trabalho | Restrições |
--------- | ---------
| Exchange Online | Se houver mais de uma organização do Exchange no local (ou seja, o Exchange foi implantado toomore de uma floresta), você deve usar o Exchange 2013 SP1 ou posterior. Para obter mais informações, confira [Implantações híbridas com várias florestas do Active Directory](https://technet.microsoft.com/library/jj873754.aspx). |
| Skype for Business | Quando você estiver usando várias florestas locais, topologia de floresta de conta-recurso Olá somente é suportada. Para obter mais informações, confira [Requisitos ambientais para Skype for Business Server 2015](https://technet.microsoft.com/library/dn933910.aspx). |


## <a name="staging-server"></a>Servidor de preparo
![Servidor de preparo em uma topologia](./media/active-directory-aadconnect-topologies/MultiForestStaging.png)

O Azure AD Connect dá suporte à instalação em um segundo servidor no *modo de preparo*. Um servidor nesse modo lê dados de todos os diretórios conectados, mas não grava nada tooconnected diretórios. Ele usa o ciclo de sincronização normal hello e, portanto, tem uma cópia atualizada dos dados de identidade de saudação.

Em um desastre em que o servidor primário Olá falha, você pode fazer failover toohello servidor de preparo. Você pode fazer isso no Assistente de conexão do AD do Azure hello. Esse segundo servidor pode estar localizado em um datacenter diferente porque nenhuma infraestrutura é compartilhada com o servidor primário hello. Você deve copiar manualmente qualquer alteração de configuração feita no segundo servidor de saudação servidor primário toohello.

Você pode usar um tootest de servidor de preparo um nova configuração e hello efeito personalizado que ele tem em seus dados. Você pode visualizar as alterações de saudação e ajustar a configuração de saudação. Quando estiver satisfeito com a nova configuração de hello, você pode fazer Olá servidor ativo de saudação de servidor de preparo e definir Olá antigo servidor ativo toostaging modo.

Você também pode usar este servidor de sincronização do active método tooreplace hello. Preparar o novo servidor de saudação e defina-o modo de toostaging. Verifique se ele está em bom estado, desabilitar (tornando ativo), de modo de preparo e desligar o servidor ativo atualmente hello.

É possível toohave mais de um servidor de preparo quando você quiser toohave vários backups em data centers diferentes.

## <a name="multiple-azure-ad-tenants"></a>Vários locatários do Azure AD
Recomendamos ter um único locatário no Azure AD para uma organização.
Antes de você planejar toouse vários locatários do AD do Azure, consulte o artigo Olá [gerenciamento de unidades administrativas no Azure AD](../active-directory-administrative-units-management.md). Ele aborda cenários comuns em que você pode usar um único locatário.

![Topologia de várias florestas e vários locatários](./media/active-directory-aadconnect-topologies/MultiForestMultiDirectory.png)

Há uma relação de 1:1 entre um servidor de sincronização do Azure AD Connect e um locatário do Azure AD. Para cada locatário do Azure AD, você precisará de uma instalação de servidor do Azure AD Connect Sync. instâncias de locatário do AD do Azure Olá são isoladas por design. Ou seja, os usuários em um locatário não podem ver usuários Olá outro locatário. Se você quiser que essa separação, essa é uma configuração com suporte. Caso contrário, você deve usar o hello único modelo de locatário do AD do Azure.

### <a name="each-object-only-once-in-an-azure-ad-tenant"></a>Cada objeto uma única vez em um locatário do Azure AD
![Topologia filtrada para uma floresta única](./media/active-directory-aadconnect-topologies/SingleForestFiltered.png)

Nessa topologia, um servidor de sincronização do Azure AD Connect é locatário tooeach conectada AD do Azure. servidores de sincronização do Azure AD Connect Olá devem ser configurados para filtragem para que cada um tenha um conjunto mutuamente exclusivo de objetos toooperate em. Você pode, por exemplo, definir o escopo cada domínio específico do servidor tooa ou unidade organizacional.

Um domínio DNS só pode ser registrado em um único locatário do Azure AD. Olá UPNs dos usuários Olá na instância de Active Directory local Olá também deve usar namespaces separados. Por exemplo, Olá anterior imagem, três sufixos UPN separados são registrados na instância de Active Directory local Olá: contoso.com e fabrikam.com brinquedos.com. os usuários de saudação em cada domínio do Active Directory local usem um namespace diferente.

Não há nenhum GALSync entre instâncias de locatário do AD do Azure hello. Olá catálogo de endereços no Exchange Online e Skype mostra Business somente usuários Olá mesmo locatário.

Essa topologia tem o seguinte Olá restrições em outro tipo de cenários com suporte:

* Somente um dos locatários de saudação do AD do Azure pode habilitar uma híbrida do Exchange com instância do hello local do Active Directory.
* Os dispositivos Windows 10 podem ser associados a um locatário do Azure AD.
* Olá único (SSO) opção de logon para autenticação de passagem e a sincronização de senha pode ser usada com apenas um locatário do AD do Azure.

requisito de saudação para um conjunto mutuamente exclusivo de objetos também se aplica a toowriteback. Alguns recursos de write-back não têm suporte com esta topologia pois eles supõem uma configuração única local. Esses recursos incluem:

* Write-back de grupo com configuração padrão.
* Write-back de dispositivo.

### <a name="each-object-multiple-times-in-an-azure-ad-tenant"></a>Cada objeto várias vezes em um locatário do Azure AD
![Topologia sem suporte para uma única floresta e vários locatários](./media/active-directory-aadconnect-topologies/SingleForestMultiDirectoryUnsupported.png) ![Topologia sem suporte para uma única floresta e vários conectores](./media/active-directory-aadconnect-topologies/SingleForestMultiConnectorsUnsupported.png)

Estas tarefas não têm suporte:

* Sincronização Olá mesmo locatários de toomultiple AD do Azure do usuário.
* Faça uma alteração de configuração para fazer os usuários de um locatário do Azure AD aparecerem como contatos em outro locatário do Azure AD.
* Modificar locatários do Azure AD Connect sincronização tooconnect toomultiple AD do Azure.

### <a name="galsync-by-using-writeback"></a>GALSync com o uso de write-back
![Topologia sem suporte para várias florestas e vários diretórios com GALSync concentrando-se no Azure AD](./media/active-directory-aadconnect-topologies/MultiForestMultiDirectoryGALSync1Unsupported.png) ![Topologia sem suporte para várias florestas e vários diretórios com GALSync concentrando-se no Active Directory local](./media/active-directory-aadconnect-topologies/MultiForestMultiDirectoryGALSync2Unsupported.png)

Os locatários do Azure AD são isolados por design. Estas tarefas não têm suporte:

* Alterar configuração de saudação do Azure AD Connect tooread de dados de sincronização de outro locatário do AD do Azure.
* Exporte usuários como instância do contatos tooanother local do Active Directory usando a sincronização do Azure AD Connect.

### <a name="galsync-with-on-premises-sync-server"></a>GALSync com o servidor de sincronização local
![GALSync em uma topologia para várias florestas e vários diretórios](./media/active-directory-aadconnect-topologies/MultiForestMultiDirectoryGALSync.png)

Você pode usar o FIM 2010 ou o MIM 2016 toosync usuários locais (via GALSync) entre duas organizações do Exchange. os usuários de saudação em uma organização aparecem como usuários/contatos externos em Olá outra organização. Essas instâncias locais diferentes do Active Directory poderão então ser sincronizadas para seus próprios locatários do Azure AD.

## <a name="next-steps"></a>Próximas etapas
toolearn como tooinstall do Azure AD Connect para esses cenários, consulte [instalação personalizada do Azure AD Connect](active-directory-aadconnect-get-started-custom.md).

Saiba mais sobre Olá [sincronização do Azure AD Connect](active-directory-aadconnectsync-whatis.md) configuração.

Saiba mais sobre [como integrar suas identidades locais ao Azure Active Directory](active-directory-aadconnect.md).
