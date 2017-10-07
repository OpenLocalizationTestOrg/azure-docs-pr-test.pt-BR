---
title: "Visão geral de aaaConceptual dos nomes de domínio personalizado no Active Directory do Azure | Microsoft Docs"
description: "Explica a estrutura conceitual Olá para o uso de nomes de domínio personalizados no Azure Active directory, incluindo federation para logon único"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: fd0c5def-0da2-43af-81bc-76f4cfe86afd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.openlocfilehash: 0a3454ae6b733a8a13a71925df3cc664063f388e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="conceptual-overview-of-custom-domain-names-in-azure-active-directory"></a>Visão geral conceitual dos nomes de domínio personalizados no Azure Active Directory
Um nome de domínio pode ser um identificador importante para muitos recursos de diretório, como parte de:

* Um nome de usuário ou endereço de email de um usuário
* Olá endereço de um grupo
* URI da ID do aplicativo Hello para um aplicativo

Um recurso no Azure Active Directory (AD do Azure) pode incluir um nome de domínio que já é verificado toobe pertencentes a directory Olá que contém o recurso de saudação. Somente um administrador global pode executar tarefas de gerenciamento de domínio no Azure AD.

> [!IMPORTANT]
> A Microsoft recomenda que você gerencie o AD do Azure usando Olá [Centro de administração do AD do Azure](https://aad.portal.azure.com) em Olá portal do Azure em vez de usar Olá portal clássico do Azure mencionado neste artigo. Para como toomanage seu nomes de domínio no Centro de administração de saudação do AD do Azure, consulte [gerenciar nomes de domínio personalizado no Active Directory do Azure](active-directory-domains-manage-azure-portal.md).

Nomes de domínio no Azure AD são globalmente exclusivos. Um nome de domínio personalizado pode ser usado apenas por um locatário do Azure AD por vez. Se um diretório do Azure AD verificar um nome de domínio, nenhum outro diretório do Azure AD poderá verificar ou usar o mesmo nome de domínio.

## <a name="initial-and-custom-domain-names"></a>Nomes de domínio iniciais e personalizados
Todo nome de domínio no Azure AD é um nome de domínio inicial ou um nome de domínio personalizado.

Cada AD do Azure vem com um nome de domínio inicial Olá formulário contoso.onmicrosoft.com. Esse nome de domínio de nível de terceiro, neste exemplo, "contoso.onmicrosoft.com", foi estabelecido quando Olá diretório foi criado, normalmente por Olá administrador que criou o diretório de saudação. nome de domínio inicial Olá para um diretório não pode ser alterada ou excluída. nome de domínio inicial Hello, enquanto totalmente funcional, destina-se principalmente toobe usado como um mecanismo de inicialização até que um nome de domínio personalizado é verificada.

Na maioria dos ambientes de produção, um diretório tem pelo menos um domínio personalizado verificado, como "contoso.com", e é esse domínio personalizado que é visível tooend usuários. Um nome de domínio personalizado é um nome de domínio que pertence à uma organização e é usado por ela, como "contoso.com" para ser usado para hospedar seu site da Web. Esse nome de domínio é familiar tooemployees porque ela é parte do nome de usuário de saudação que usam toosign na rede corporativa toohello ou toosend e recuperar o email.

Antes que ele pode ser usado pelo AD do Azure, o nome de domínio personalizado de saudação deve ser adicionado tooyour diretório e verificado.

## <a name="verified-and-unverified-domain-names"></a>Nomes de domínio verificados e não verificados
nome de domínio inicial Olá para um diretório implicitamente é avaliada como verificada pelo AD do Azure. Quando um administrador adiciona um nome de domínio personalizado tooan AD do Azure, é inicialmente em um estado não verificado. O AD do Azure não permitirá que qualquer toouse de recursos de diretório um nome de domínio não verificado. Isso garante que apenas um diretório pode usar um nome de domínio específico e, na verdade, organização Olá usa o nome de domínio Olá possui esse nome de domínio.

AD do Azure verifica a propriedade de nome de domínio procurando uma entrada específica no arquivo de zona do DNS (serviço) do hello domínio nome hello nome de domínio. tooverify a propriedade de nome de domínio, um administrador obtém entrada DNS de saudação do AD do Azure que o AD do Azure procurará e adiciona esse arquivo de zona do DNS de toohello entrada hello nome de domínio. arquivo de zona DNS Olá é mantido pela Olá registrador de nome de domínio. Olá etapas tooverify um domínio são mostrados no artigo Olá para [adicionando um diretório de tooyour do Azure AD de domínio personalizado](active-directory-add-domain.md).

Adicionar um arquivo de zona do DNS entrada toohello Olá nome de domínio não afeta os outros serviços de domínio, como email ou hospedagem na web.

## <a name="federated-and-managed-domain-names"></a>Nomes de domínio federados e gerenciados
Um nome de domínio personalizado no AD do Azure podem ser configurado toogive usuários uma experiência entre seu Active Directory no local e o Azure AD de entrada federada. Configurar um domínio para a federação exige atualizações tooprivileged recursos no AD do Azure e também tooyour do Active Directory do Windows Server. A configuração de um domínio federado deve ser realizada por meio do Azure AD Connect ou usando o PowerShell. Federar um domínio personalizado não pode ser iniciado do hello portal clássico do Azure. [Assista a este vídeo toolearn sobre como configurar o AD FS para o logon de usuário com o Azure AD Connect](http://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Configuring-AD-FS-for-user-sign-in-with-Azure-AD-Connect).

Domínios que não são federados algumas vezes são chamados de domínios gerenciados. domínio de saudação inicial para um diretório do AD do Azure implicitamente é avaliado como um domínio gerenciado.

## <a name="primary-domain-names"></a>Nomes de domínio primários
Olá, nome de domínio primário para um diretório é nome de domínio de saudação é pré-selecionada como valor padrão de saudação para parte do domínio' hello' hello do nome de usuário, quando um administrador cria um novo usuário em Olá [portal do Azure](https://portal.azure.com/), ou outro portal como o portal de administração do Office 365 de saudação ou no portal do Microsoft Intune Olá. Um diretório pode ter apenas um nome de domínio primário. Um administrador pode alterar toobe de nome de domínio primário Olá qualquer domínio personalizado verificado que não é federado ou o domínio inicial toohello.

## <a name="domain-names-in-azure-ad-and-other-microsoft-online-services"></a>Nomes de domínio no Azure AD e outros Microsoft Online Services
Um nome de domínio deve ser verificado no Azure AD antes que possa ser usado por outro Microsoft Online Service, como Exchange Online, SharePoint Online e Intune. Esses outros serviços geralmente exigem um administrador tooadd uma ou mais entradas DNS do serviço toohello específico.

Um aplicativo web do Azure usa a propriedade de tooverify seu próprio mecanismo de um domínio. Um domínio deve ser verificado para ser usado com o Azure AD, mesmo que tenha sido verificado anteriormente para ser usado por um aplicativo Web do Azure em uma assinatura que se baseia no Azure AD. Um aplicativo web do Azure pode usar um nome de domínio foi verificado em um diretório diferente do diretório de saudação que protege o aplicativo web de saudação.

## <a name="managing-domain-names"></a>Gerenciando nomes de domínio
Tarefas de gerenciamento de domínio podem ser concluídas do hello portal clássico do Azure e do PowerShell. Muitas tarefas podem ser concluídas usando hello Azure AD Graph API.

* [Adicionando e verificando um nome de domínio personalizado](active-directory-add-domain.md)
* [Gerenciar domínios no hello portal clássico do Azure](active-directory-add-manage-domain-names.md)
* [Usando nomes de domínio do PowerShell toomanage no AD do Azure](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [Usando nomes de domínio toomanage hello Azure AD Graph API no AD do Azure](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

