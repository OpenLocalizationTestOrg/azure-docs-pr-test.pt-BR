---
title: "aaaHow toocreate uma coleção de nuvem do Azure RemoteApp | Microsoft Docs"
description: "Saiba como toocreate uma implantação do Azure RemoteApp que salva dados em Olá nuvem do Azure."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: 4d7c6956-7e4a-4a41-b7f2-7e5832bf01e3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: a072ad19d8293016382831d48d0af8e0f5e0d458
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-cloud-collection-of-azure-remoteapp"></a>Como toocreate uma coleção de nuvem do Azure RemoteApp
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

Há dois tipos de coleções do [Azure RemoteApp](remoteapp-collections.md): 

* Nuvem: reside completamente no Azure. Você pode escolher toosave todos os dados na nuvem hello (para uma coleção somente nuvem) ou tooconnect tooa sua coleção VNET e salvar dados.   
* Híbrido: inclui uma rede virtual para acesso local - isso requer o uso de saudação do AD do Azure e um ambiente do Active Directory local.

Este tutorial orienta você pelo processo de saudação de criação de uma coleção de nuvem. Há quatro etapas: 

1. Criar uma coleção do Azure RemoteApp
2. Opcionalmente, configure a sincronização do diretório. Se você estiver usando o AD do Azure + Active Directory, você tem toosynchronize usuários, contatos e senhas do seu locatário de tooyour AD do Azure Active Directory local.
3. Publicar aplicativos.
4. Configurar o acesso do usuário.

**Antes de começar**

Você precisa toodo Olá seguinte antes de criar a coleção de saudação:

* [Inscreva-se](https://azure.microsoft.com/services/remoteapp/) no Azure RemoteApp. 
* Colete informações sobre usuários Olá que você deseja toogrant access. Podem ser informações da conta da Microsoft ou da conta corporativa do Active Directory para usuários ou grupos.
* Este procedimento pressupõe que são ambos toouse contínuo uma saudação de imagens de modelo fornecidos como parte da sua assinatura ou se você já tiver carregado imagem de modelo Olá deseja toouse. Se você precisar tooupload uma imagem de modelo diferente, você pode fazer isso na página de imagens de modelo de saudação. Basta clicar em **carregar uma imagem de modelo** e siga as etapas de saudação no Assistente de saudação. 
* Deseja imagem Office 365 ProPlus do toouse Olá? Verifique as informações [aqui](remoteapp-officesubscription.md).
* Deseja aplicativos personalizados tooprovide ou programas LOB? Crie uma nova [imagem](remoteapp-imageoptions.md) e use-a em sua coleção de nuvem.
* Descubra se você precisa de tooconnect tooa VNET. Se você escolher tooconnect tooa VNET, verifique se ele atende Olá [diretrizes de dimensionamento](remoteapp-vnetsizing.md) e que ele [pode se conectar a tooRemoteApp](remoteapp-vnet.md). Check-out Olá [artigo planejamento de rede virtual ](remoteapp-planvnet.md)para obter mais informações.
* Se você estiver usando uma rede virtual, decida se deseja toojoin-tooyour domínio de Active Directory local.

## <a name="step-1-create-a-cloud-collection---with-or-without-a-vnet"></a>Etapa 1: criar uma coleção na nuvem, com ou sem uma VNET
As etapas a seguir de saudação do uso muito**criar uma coleção somente nuvem**:

1. No portal de gerenciamento hello, vá toohello RemoteApp página.
2. Clique em **Novo > Criação Rápida**.
3. Digite um nome para a coleção e selecione sua região.
4. Escolha Olá plano que você deseja toouse - básico ou padrão.
5. Escolha Olá toouse de modelo para esta coleção. 
   
    **Dica:** sua assinatura do RemoteApp vem com [imagens de modelo](remoteapp-images.md) que contêm o Office 365 ou Office 2013 (para uso de avaliação) programas, alguns publicado (como Word) e outros pronto toopublish. Você também pode criar uma nova [imagem](remoteapp-imageoptions.md) e usá-la em sua coleção de nuvem.
6. Clique em **Criar coleção de RemoteApp**.
   
    **Importante:** pode levar até too30 minutos tooprovision sua coleção.

Depois de sua coleção do RemoteApp foi criada, clique duas vezes em nome de saudação da coleção de saudação. Isso abrirá Olá **início rápido** página - isso é onde você terminar de configurar coleta de saudação.

Toocreate as etapas a seguir do uso Olá um **coleção VNET + nuvem**:

1. No portal de gerenciamento hello, vá toohello Azure RemoteApp página.
2. Clique em **Novo** > **Criar com VNET**.
3. Digite um nome para a sua coleção.
4. Escolha Olá plano que você deseja toouse - básico ou padrão.
5. Escolha Olá VNET que você já tenha criado. Não sei como toodo que? Por enquanto, etapas Olá estão em Olá [híbrida](remoteapp-create-hybrid-deployment.md) tópico.
6. Decida se deseja toojoin seu domínio de tooyour da coleção. Em caso afirmativo, você precisará toouse AD Connect toointegrate AD do Azure e o ambiente do Active Directory. Isso será explicado abaixo na **Etapa 2**.
7. Clique em **Criar coleção de RemoteApp**.

## <a name="step-2-configure-active-directory-directory-synchronization-optional"></a>Etapa 2: Configurar a sincronização de diretório do Active Directory (opcional)
Se você quiser toouse do Active Directory, o Azure RemoteApp requer sincronização de diretórios entre o Active Directory do Azure e locais do Active Directory toosynchronize usuários, contatos e locatário de Active Directory do Azure tooyour senhas. Consulte [Configurando o Active Directory para o RemoteApp do Azure](remoteapp-ad.md) para obter informações de planejamento. Você também pode ir diretamente muito[AD Connect](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) para obter informações.

## <a name="step-3-publish-apps"></a>Etapa 3: Publicar aplicativos
Um aplicativo do Azure RemoteApp é Olá aplicativo ou programa que você forneça tooyour usuários. Ele está localizado na imagem de modelo Olá carregado para a coleção de saudação. Quando um usuário acessa um aplicativo, o aplicativo hello aparece toorun no seu ambiente local, mas ele está em execução em uma máquina virtual no Azure. 

Antes dos usuários podem acessar aplicativos, você precisa toopublish-los – permite que aplicativos que os usuários acessam aplicativos Olá por meio de publicação Olá cliente de área de trabalho remota.

Você pode publicar vários aplicativos tooyour coleção do RemoteApp do Azure. Na página de publicação Olá, clique em **publicar** tooadd um programa. Você pode publicar de saudação **iniciar** menu Olá da imagem de modelo ou especificando o caminho de saudação na imagem de modelo Olá para o aplicativo hello. Se você escolher tooadd Olá **iniciar** menu, escolha Olá toopublish de aplicativo. Se você escolher tooprovide Olá caminho toohello aplicativo, forneça um nome para o aplicativo hello e Olá caminho toowhere que ele é instalado na imagem de modelo hello.

## <a name="step-4-configure-user-access"></a>Etapa 4: Configurar o acesso do usuário
Agora que você criou sua coleção, é necessário tooadd usuários de saudação que você deseja toouse possível toobe seus recursos remotos. Se você estiver usando o Active Directory, usuários de saudação que você forneça acesso tooneed tooexist no locatário do Active Directory Olá associados com a assinatura de saudação usado toocreate nesta coleção.

1. Na página início rápido hello, clique em **configurar o acesso de usuário**. 
2. Insira a conta de trabalho da saudação (a partir do Active Directory) ou a conta da Microsoft que você deseja acesso toogrant.
   
   **Observações:** 
   
   Certifique-se de que você use Olá  *user@domain.com*  formato.
   
   Se você estiver usando o Office 365 ProPlus em sua coleção, você deve usar identidades do Active Directory Olá para seus usuários. Isso ajuda a validar o licenciamento. 
3. Depois que os usuários de saudação são validados, clique em **salvar**.

## <a name="next-steps"></a>Próximas etapas
É isso – sua implantação na nuvem do Azure RemoteApp foi criada e implantada com sucesso. Olá próxima etapa é toohave aos usuários baixar e instalar o cliente de área de trabalho remota hello. Você pode encontrar o cliente Olá Olá URL na página de início rápido do Azure RemoteApp hello. Em seguida, tem os usuários façam logon em cliente hello e acessar Olá aplicativos publicados por você.

### <a name="help-us-help-you"></a>Ajude-nos a ajudar você
Você sabia que na adição toorating neste artigo e fazer comentários para baixo abaixo, você pode fazer alterações toohello artigo? Falta alguma coisa? Há algo errado? Escrevi algo que não ficou muito claro? Role para cima e clique em **Editar no GitHub** toomake alterações - aqueles virão toous para revisão e, em seguida, uma vez que saia neles, você verá suas alterações e aprimoramentos aqui.

