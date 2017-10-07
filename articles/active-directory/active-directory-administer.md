---
title: "aaaHow toouse uma visão geral diretório de locatário do diretório de códigos ativa do Azure | Microsoft Docs"
description: "Explica o que é um locatário do AD do Azure e como toomanage Azure usando o Active Directory do Azure"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: it-pro;oldportal
ms.openlocfilehash: ddb16d89bf06a3753ed5106bd95162130ad51b08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-azure-ad-directory"></a>Gerenciar seu diretório do Azure AD

## <a name="what-is-an-azure-ad-tenant"></a>O que é um locatário AD Azure?
No Azure Active Directory (Azure AD), um locatário é uma instância dedicada de um diretório do Azure AD que sua organização recebe quando se inscreve em um serviço de nuvem da Microsoft, como o Azure ou Office 365. Cada diretório do Azure AD é distinto e separado de outros diretórios do Azure AD. Assim como uma construção de escritório corporativo é um tooonly de ativo seguro específico sua organização, um diretório do AD do Azure também foi projetado toobe um ativo seguro para uso unicamente de sua organização. Olá arquitetura do AD do Azure isola as informações de identidade e de dados do cliente para que os usuários e administradores de um diretório do AD do Azure não podem acidentalmente ou maliciosamente acessar dados em outro diretório.

![Gerenciar o Active Directory do Azure](./media/active-directory-administer/aad_portals.png)

## <a name="how-can-i-get-an-azure-ad-directory"></a>Como posso obter um diretório do Azure AD?
O AD do Azure fornece identidade e diretório de núcleo Olá atrás da maioria dos serviços de nuvem da Microsoft, incluindo os recursos de gerenciamento:

* As tabelas
* Microsoft Office 365
* Microsoft Dynamics CRM Online
* Microsoft Intune

Você obtém um diretório do Azure quando se inscreve para qualquer um desses serviços em nuvem da Microsoft. Você pode criar diretórios adicionais conforme necessário. Por exemplo, você pode manter seu primeiro diretório como um diretório de produção e, em seguida, criar um outro diretório para teste ou preparo.

### <a name="using-hello-azure-ad-directory-that-comes-with-a-new-azure-subscription"></a>Usando o diretório do AD do Azure Olá que vem com uma nova assinatura do Azure

É recomendável que você use a conta de administrador Olá usada para seu primeiro serviço quando você se inscrever para outros serviços da Microsoft. informações que você fornecer Olá Olá primeira vez que você se inscrever para um serviço da Microsoft é usado toocreate Azure um nova instância de diretório do AD para sua organização. Se você usar que diretório tooauthenticate tentativas de entrada quando você se inscreve tooother serviços da Microsoft, eles podem usar Olá contas de usuário existentes, políticas, configurações ou integração de diretórios locais configurados no seu diretório padrão.

Por exemplo, se você se inscreve para uma assinatura Microsoft Intune e, em seguida, sincronizar ainda mais o Active Directory no local com seu diretório do AD do Azure, você pode inscrever-se para outro serviço da Microsoft, como o Office 365 e facilmente obter Olá mesmo diretório benefícios de integração com o Microsoft Intune.

Para obter mais informações sobre como integrar seu diretório local ao Azure AD, consulte [Integração de diretório com o Azure AD Connect](active-directory-aadconnect.md).

### <a name="associate-an-existing-azure-ad-directory-with-a-new-azure-subscription"></a>Associar um diretório existente do Azure AD a uma nova assinatura do Azure
Você pode associar uma nova assinatura do Azure com hello mesmo diretório que autentica a entrada para uma assinatura existente do Office 365 ou Microsoft Intune. Para obter mais informações sobre esse cenário, consulte [transferir a propriedade de uma conta de tooanother de assinatura do Azure](../billing/billing-subscription-transfer.md)

### <a name="create-an-azure-ad-directory-by-signing-up-for-a-microsoft-cloud-service-as-an-organization"></a>Criar um diretório do Azure AD inscrevendo-se para um serviço de nuvem da Microsoft como uma organização
Se você ainda não tiver uma assinatura tooa serviço de nuvem da Microsoft, você pode usar uma saudação toosign links a seguir para cima. Ao inscrever-se no seu primeiro serviço um diretório do Azure AD automaticamente será criado automaticamente.

* [Microsoft Azure](https://account.azure.com/organization)
* [Office 365](http://products.office.com/business/compare-office-365-for-business-plans/)
* [Microsoft Intune](https://portal.office.com/Signup/Signup.aspx?OfferId=40BE278A-DFD1-470a-9EF7-9F2596EA7FF9&dl=INTUNE_A&ali=1#0%20)

### <a name="how-toochange-hello-default-directory-for-a-subscription"></a>Como toochange Olá diretório padrão para uma assinatura

1. Entrar toohello [Centro de contas Azure](https://account.windowsazure.com/Home/Index) com uma conta que seja Olá administrador da conta de propriedade de assinatura de tootransfer Olá assinatura.
2. Certifique-se de usuário Olá que você deseja o proprietário da assinatura Olá toobe está no diretório de saudação direcionada.
3. Clique em **Transferir assinatura**.
4. Especifique o destinatário hello. destinatário de saudação automaticamente recebe um email com um link de aceitação.
5. destinatário de saudação clica Olá link e segue as instruções hello, inclusive, inserir suas informações de pagamento. Quando o destinatário Olá for bem-sucedida, assinatura de saudação é transferida. 
6. Olá diretório padrão de assinatura de saudação é alterado diretório toohello Olá usuário é se a transferência de propriedade de assinatura Olá bem-sucedida.

### <a name="manage-hello-default-directory-in-azure"></a>Gerenciar o diretório padrão de saudação no Azure
Quando você se inscrever no Azure, um diretório do Azure AD padrão é associado à sua assinatura. Não há custos para usar o Azure AD e os diretórios são um recurso gratuito. Existem serviços do Azure AD pagos que são licenciados separadamente e fornecem funcionalidade adicional, como a identidade visual da empresa no momento do logon e redefinição de senha através de autoatendimento. Você também pode criar um domínio personalizado usando um nome DNS que você possui em vez do padrão de saudação *. c o m domínio.

## <a name="how-can-i-manage-directory-data"></a>Como posso gerenciar dados de diretório?
tooadminister uma ou mais assinaturas de serviço de nuvem Microsoft, você pode usar o hello [Centro de administração do AD do Azure](https://aad.portal.azure.com), Olá portal de conta Microsoft Intune ou Olá [Centro de administração do Office 365](https://portal.office.com/) toomanage seu dados de diretório da organização. Você também pode usar [cmdlets do PowerShell do Azure Active Directory](https://docs.microsoft.com/powershell/azure/active-directory) toohelp você gerenciar dados armazenados no AD do Azure.

A partir de qualquer um desses portais (ou cmdlets), você pode:

* Criar e gerenciar contas de usuário e de grupo
* Gerenciar serviços de nuvem relacionados das assinaturas da sua organização
* Configurar a integração local com os serviços de identidade e autenticação do Azure AD

Centro de administração do AD do Azure Hello, centro de administração do Office 365, portal de conta Microsoft Intune e Olá cmdlets do AD do Azure todos leem e gravam tooa única instância compartilhada do AD do Azure que está associado com o diretório da sua organização. Cada uma dessas ferramentas age como uma interface de front-end que recebe e/ou modifica seus dados de diretório.

Quando você altera os dados da sua organização usando quaisquer dos portais de saudação ou cmdlets enquanto conectado sob o contexto de saudação de um desses serviços, Olá alterações também são mostradas no hello outros portais Olá próxima vez que entrar no. Esses dados são compartilhados entre serviços de nuvem do hello Microsoft toowhich que assinar.

Por exemplo, se você usar Olá Centro de administração do Office 365 tooblock um usuário de entrar no, que bloqueia ação Olá usuário de entrar no tooany toowhich outros serviços sua organização é está inscrita. Se você exibir hello mesma conta de usuário no portal de conta do Microsoft Intune Olá, você também ver que o usuário hello está bloqueado.

## <a name="how-can-i-add-and-manage-multiple-directories"></a>Como posso adicionar e gerenciar vários diretórios?
Você pode [adicionar um diretório do AD do Azure no portal do Azure de saudação](https://portal.azure.com/#create/Microsoft.AzureActiveDirectory). Preencha as informações de saudação e selecione **criar**.

Você pode gerenciar cada diretório como um recurso completamente independente: cada diretório é um par, com recursos completos e logicamente independente de outros diretórios que você gerencia; não há nenhuma relação de pai-filho entre os diretórios. Essa independência entre diretórios inclui independência de recursos, independência administrativa e independência de sincronização.

* **Independência de recursos**. Se você cria ou excluir um recurso em um diretório, ele não tem impacto em qualquer recurso em outro diretório, com exceção de saudação parcial de usuários externos. Se você usar um domínio personalizado "contoso.com" com um diretório, ele não pode ser usado com nenhum outro diretório.
* **Independência administrativa**.  Se um usuário que não é administrador do diretório "Contoso" criar um diretório de teste chamado "Teste", então:
  
  * os administradores de saudação do diretório 'Contoso' têm toodirectory sem privilégios administrativos diretos 'Test' a menos que um administrador de "Teste" especificamente conceda a eles esses privilégios. Os administradores de 'Contoso' podem controlar o acesso toodirectory 'Test' por meio de seu controle Olá da conta de usuário que criou a 'Teste'.
    
  * Se você atribuir ou remover uma função de administrador para um usuário em um diretório, alteração de saudação não afeta nenhuma função de administrador que o usuário pode ter em outro diretório.
* **Independência de sincronização**. Você pode configurar cada Azure independentemente do AD locatário tooget dados sincronizados com a ferramenta de sincronização de diretórios de conectar uma única instância Olá AD do Azure.

Observe também que, ao contrário de outros recursos do Azure, seus diretórios não são recursos filho de uma assinatura do Azure. Então se você cancela ou permite tooexpire sua assinatura do Azure, você ainda pode acessar os dados de diretório usando o PowerShell do Azure AD, Olá API do Graph do Azure ou outras interfaces como Olá Office 365 Admin Center. Você também pode associar outra assinatura directory hello.

## <a name="how-tooprepare-toodelete-an-azure-ad-directory"></a>Como tooprepare toodelete um diretório do AD do Azure
Um administrador global pode excluir um diretório do AD do Azure do portal de saudação. Quando um diretório é excluído, todos os recursos que estão contidos no diretório Olá também são excluídos. Verifique se que você não precisa Olá diretório antes de excluí-lo.

> [!NOTE]
> Se o usuário Olá entrar com uma conta corporativa ou escolar, usuário Olá deve não estar tentando toodelete seu diretório inicial. Por exemplo, se hello usuário está conectado como joe@contoso.onmicrosoft.com, esse usuário não é possível excluir o diretório de saudação que tem contoso.onmicrosoft.com como seu domínio padrão.

O AD do Azure requer que certas condições sejam atendido toodelete um diretório. Isso reduz o risco de que a exclusão de um diretório negativamente afeta os usuários ou aplicativos, como a capacidade de saudação de usuários toosign em tooOffice 365 ou acessar os recursos no Azure. Por exemplo, se um diretório para uma assinatura for excluído acidentalmente, em seguida, os usuários não é possível acessar Olá recursos do Azure para essa assinatura.

Olá seguintes condições é atendida:

* Hello apenas o usuário no diretório Olá deve ser Olá administrador global que é toodelete Olá diretório. Quaisquer outros usuários devem ser excluídos antes de saudação diretório pode ser excluído. Se os usuários estiverem sincronizados no local, em seguida, sincronização deve ser desligada e usuários Olá devem ser excluídos no diretório de nuvem hello usando Olá portal do Azure ou os cmdlets do PowerShell do Azure. Não há nenhum grupo de toodelete de requisito ou contatos, tais como contatos adicionados do hello Office 365 Admin Center.
* Não pode haver nenhum aplicativo no diretório de saudação. Todos os aplicativos devem ser excluídos antes de saudação diretório pode ser excluído.
* Não há provedores de autenticação multifator podem ser vinculado toohello directory.
* Não pode haver nenhuma assinatura para o Microsoft Online Services, como o Microsoft Azure, Office 365 ou Azure AD Premium associada ao diretório de saudação. Por exemplo, se um diretório padrão tiver sido criado para você no Azure, você não poderá excluir esse diretório se sua assinatura do Azure ainda depender desse diretório para autenticação. Da mesma forma, você não pode excluir um diretório se outro usuário tiver associado uma assinatura a ele. 


## <a name="next-steps"></a>Próximas etapas
* [Fórum do Azure AD](https://social.msdn.microsoft.com/Forums/home?forum=WindowsAzureAD)
* [Fórum de autenticação multifator do Azure](https://social.msdn.microsoft.com/Forums/home?forum=windowsazureactiveauthentication)
* [Perguntas do Stack Overflow para Azure](http://stackoverflow.com/questions/tagged/azure)
* [Azure Active Directory PowerShell](https://docs.microsoft.com/powershell/azure/active-directory)
* [Atribuindo funções de administrador no Azure AD](active-directory-assign-admin-roles.md)
