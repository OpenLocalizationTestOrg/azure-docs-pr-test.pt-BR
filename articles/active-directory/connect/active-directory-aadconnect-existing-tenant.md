---
title: "Azure AD Connect: Quando você já tiver o Azure AD | Microsoft Docs"
description: "Este tópico descreve como conectar toouse quando você tiver um locatário existente do AD do Azure."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: f7b166e9e85c1f03330e8e0074d4afa4036738c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-when-you-have-an-existent-tenant"></a>Azure AD Connect: quando você tem um locatário existente
A maioria dos tópicos de saudação para como toouse do Azure AD Connect pressupõe que você inicie com um novo Azure locatário do AD e o que há nenhum usuário ou outros objetos. Mas se você tiver começado com um locatário do AD do Azure, preencheu com usuários e outros objetos e agora deseja toouse conectar-se, em seguida, este tópico é para você.

## <a name="hello-basics"></a>Noções básicas de saudação
Um objeto no AD do Azure é controlado ou na nuvem de saudação (AD do Azure) ou no local. Em um único objeto, você não pode gerenciar alguns atributos locais e outros atributos no Azure AD. Cada objeto tem um sinalizador que indica onde o objeto de saudação é gerenciado.

Você pode gerenciar alguns usuários locais e outro na nuvem hello. Um cenário comum para essa configuração é uma organização com uma combinação de funcionários de contabilidade e vendedores. trabalhadores contabilização Hello tem um local conta do AD, mas os funcionários de vendas Olá não, eles têm uma conta no AD do Azure. Você deve gerenciar alguns usuários locais e outros no Azure AD.

Se você tiver iniciado toomanage usuários no AD do Azure que também estejam no AD local e mais tarde quiser toouse conectar, em seguida, existem alguns outros problemas que você precisa tooconsider.

## <a name="sync-with-existing-users-in-azure-ad"></a>Sincronia com usuários existentes no Azure AD
Quando você instalar o Azure AD Connect e iniciar a sincronização, hello serviço de sincronização do AD do Azure (no AD do Azure) faz uma verificação em todos os novos objetos e tente toofind um toomatch de objeto existente. Existem três atributos usados para esse processo: **userPrincipalName**, **proxyAddresses** e **sourceAnchor**/**immutableID**. Uma correspondência entre **userPrincipalName** e **proxyAddresses** é conhecida como uma **correspondência flexível**. Uma correspondência com **sourceAnchor** é conhecida como **correspondência rígida**. Para Olá **proxyAddresses** somente Olá valor com atributo **SMTP:**, que é o endereço de email principal Olá, é usado para avaliação de saudação.

correspondência de saudação é avaliada apenas para novos objetos provenientes do Connect. Se você alterar um objeto existente para que ele corresponda a um desses atributos, ocorrerá um erro.

Se o AD do Azure localiza um objeto em que os valores de atributo Olá são Olá mesmo para um objeto provenientes do Connect e que ele já está presente no AD do Azure, hello objeto no AD do Azure é controlado por conectar-se. Olá anteriormente objeto gerenciado de nuvem é sinalizado como gerenciado no local. Todos os atributos no AD do Azure com um valor no local AD são substituídos com valor de local de saudação. exceção de saudação é quando um atributo tem um **nulo** valor local. Nesse caso, valor Olá no AD do Azure continuará, mas você pode apenas alterá-la no local toosomething else.

> [!WARNING]
> Desde que todos os atributos no AD do Azure for toobe substituído pelo valor de local de saudação, verifique se que você tem dados no local. Por exemplo, se você só gerenciou emails no Office 365 e não manteve atualizado no AD DS local, você perderá os valores no Azure AD/Office 365 não presentes no AD DS.

> [!IMPORTANT]
> Se você usar a sincronização de senha, que é sempre usada pelas configurações expressas, em seguida, senha Olá no AD do Azure é substituída por senha Olá no local AD. Se os usuários forem usados toomanage de senhas diferentes, em seguida, você precisa tooinform que eles devem usar Olá senha local quando você instalou conectar.

aviso e Olá na seção anterior devem ser considerados no planejamento. Se você fez várias alterações no AD do Azure não serão refletido no local AD DS, e em seguida, você precisa tooplan para como toopopulate AD DS com hello atualizados valores antes de sincronizar seus objetos do Azure AD Connect.

Se você corresponde os objetos com uma correspondência de software, Olá **sourceAnchor** é adicionado toohello objeto no AD do Azure para uma correspondência de disco rígida pode ser usada mais tarde.

### <a name="hard-match-vs-soft-match"></a>Correspondência rígida x correspondência flexível
Para uma nova instalação do Connect, não há nenhuma diferença prática entre uma correspondência rígida e uma correspondência flexível. diferença de saudação é uma situação de recuperação de desastres. Se você tiver perdido o seu servidor com o Azure AD Connect, reinstale uma nova instância para não perder os dados. Um objeto com um sourceAnchor é enviado tooConnect durante a instalação inicial. Hello correspondência pode então ser avaliada pelo cliente de saudação (Azure AD Connect), que é muito mais rápido do que fazer Olá mesmo no AD do Azure. Uma correspondência rígida é avaliada pelo Connect e pelo Azure AD. Uma correspondência flexível é avaliada apenas pelo Azure AD.

### <a name="other-objects-than-users"></a>Outros objetos que não são usuários
Os usuários geralmente têm userPrincipalName e proxyAddresses, facilitando a correspondência de saudação. Mas outros objetos, como grupos de segurança, não. Nesse caso, você só pode corresponder em uma correspondência de disco rígida usando Olá sourceAnchor. Olá sourceAnchor é sempre Olá Base64 convertido **objectGUID** no local, portanto você deve atualizar o valor de saudação no AD do Azure, quando você precisa de dois toomatch de objetos. Olá sourceAnchor/immutableID só pode ser atualizada com o PowerShell e não por meio de portais de saudação.

## <a name="create-a-new-on-premises-active-directory-from-data-in-azure-ad"></a>Criação de um Active Directory local novo a partir dos dados no Azure AD
Alguns clientes começam com uma solução somente em nuvem com o Azure AD e não têm um AD local. Depois que eles tooconsume recursos de locais e toobuild um local AD com base nos dados do AD do Azure. O Azure AD Connect não pode ajudá-lo nesse cenário. Ele não cria os usuários locais e não tem nenhuma capacidade tooset Olá senha local toohello mesmo como o AD do Azure.

Se o único motivo de saudação por que você planejar tooadd local AD for toosupport LOBs (aplicativos de linha de negócios), talvez você considere toouse [dos serviços de domínio do AD do Azure](../../active-directory-domain-services/index.md) em vez disso.

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre [Como integrar suas identidades locais ao Active Directory do Azure](active-directory-aadconnect.md).
