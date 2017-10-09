---
title: "aaaHow toocreate uma coleção híbrida do RemoteApp do Azure | Microsoft Docs"
description: "Saiba como toocreate uma implantação do RemoteApp que se conecta a rede interna tooyour."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: 08ea0ce3-3a2c-4ddf-9394-6d75c8030cb1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 3fba29acc676e0af48e995da406f889c532c44c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-hybrid-collection-for-azure-remoteapp"></a>Como toocreate uma coleção híbrida do RemoteApp do Azure
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

Há dois tipos de coleções do Azure RemoteApp:

* Nuvem: reside completamente no Azure. Você pode escolher toosave todos os dados na nuvem hello (para uma coleção somente nuvem) ou tooconnect tooa sua coleção VNET e salvar dados.   
* Híbrido: inclui uma rede virtual para acesso local - isso requer o uso de saudação do AD do Azure e um ambiente do Active Directory local.

Não sabe o que precisa? Confira [Que tipo de coleção é necessária para o Azure RemoteApp](remoteapp-collections.md)

Este tutorial orienta você pelo processo de saudação de criação de uma coleção híbrida. Há oito etapas:

1. Decida qual [imagem](remoteapp-imageoptions.md) toouse para sua coleção. Você pode criar uma imagem personalizada ou usar uma das imagens do Microsoft hello incluídas com sua assinatura.
2. Configurar a sua rede virtual. Check-out Olá [planejamento de rede virtual](remoteapp-planvnet.md) e [dimensionamento](remoteapp-vnetsizing.md) informações.
3. Criar uma coleção.
4. Una seu domínio local do tooyour de coleção.
5. Adicione uma coleção de tooyour de imagem de modelo.
6. Configurar a sincronização do diretório. Azure RemoteApp requer que você integrar com o Active Directory do Azure pela ou 1) Configurar sincronização do Azure Active Directory com opção de sincronização de senha do hello, ou 2) Configurar sincronização Azure Active Directory sem a opção de sincronização de senha Olá mas usando um domínio que é tooAD federado FS. Check-out Olá [informações de configuração para o Active Directory com o RemoteApp](remoteapp-ad.md).
7. Publicar aplicativos do RemoteApp.
8. Configurar o acesso do usuário.

**Antes de começar**

Você precisa toodo Olá seguinte antes de criar a coleção de saudação:

* [Inscreva-se](https://azure.microsoft.com/services/remoteapp/) no Azure RemoteApp.
* Crie uma conta de usuário no Active Directory toouse como Olá conta de serviço do Azure RemoteApp. Restringir as permissões de saudação para essa conta para que ele só pode ingressar em domínio de toohello máquinas.
* Colete informações sobre a sua rede local: informações sobre endereço IP e detalhes do dispositivo VPN.
* Instalar Olá [Azure PowerShell](/powershell/azure/overview) módulo.
* Colete informações sobre usuários Olá que você deseja toogrant access. Será necessário Olá o nome principal de usuário do Active Directory do Azure (por exemplo, name@contoso.com) para cada usuário. Certifique-se de que Olá UPN faz a correspondência entre o AD do Azure e o Active Directory.
* Escolha sua imagem de modelo. Uma imagem de modelo do RemoteApp do Azure contém Olá aplicativos e programas que você deseja toopublish para seus usuários. Consulte [Opções de imagem do Azure RemoteApp](remoteapp-imageoptions.md) para saber mais.
* Deseja imagem Office 365 ProPlus do toouse Olá? Verifique as informações [aqui](remoteapp-officesubscription.md).
* [Configure o Active Directory para RemoteApp](remoteapp-ad.md).

## <a name="step-1-set-up-your-virtual-network"></a>Etapa 1: Configurar a sua rede virtual
Você pode implantar uma coleção híbrida que use uma rede virtual existente do Azure, ou pode criar uma nova rede virtual. Uma rede virtual permite que os seus usuários acessem os dados da sua rede local através dos recursos remotos do RemoteApp. Usar uma rede virtual do Azure fornece tooother de acesso de rede direta sua coleção serviços do Azure e máquinas virtuais implantadas rede virtual toothat.

Certifique-se de examinar Olá [planejamento de rede virtual](remoteapp-planvnet.md) e [tamanho da rede virtual](remoteapp-vnetsizing.md) informações antes de criar sua rede virtual.

### <a name="create-an-azure-vnet-and-join-it-tooyour-active-directory-deployment"></a>Criar uma rede virtual do Azure e associá-lo a implantação do Active Directory tooyour
Comece criando uma [rede virtual](../virtual-network/virtual-networks-create-vnet-arm-pportal.md). Isso é feito em Olá **rede** guia Olá portal do Azure. É necessário tooconnect toohello sua rede virtual implantação do Active Directory que é sincronizada tooyour locatário de Active Directory do Azure.

Consulte [criar uma rede virtual usando o portal do Azure de saudação](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) para obter mais informações.

### <a name="make-sure-your-virtual-network-is-ready-for-azure-remoteapp"></a>Verifique se sua rede virtual está pronta para o Azure RemoteApp
Antes de criar sua coleção, verifique se sua nova rede virtual está pronta. Você pode validar isso fazendo Olá seguinte:

1. Crie uma máquina virtual do Azure Olá sub-rede da rede virtual de saudação recém-criado para o RemoteApp.
2. Use a área de trabalho remota tooconnect toohello VM. (Clique em **Conectar**.)
3. Ingressar toohello mesma implantação do Active Directory que você deseja toouse do RemoteApp.

Funcionou? Sua rede virtual e sub-rede estão prontas para o Azure RemoteApp!

Você pode encontrar mais informações sobre como criar máquinas virtuais do Azure e conectando toothem com área de trabalho remota [aqui](https://msdn.microsoft.com/library/azure/jj156003.aspx).

## <a name="step-2-create-an-azure-remoteapp-collection"></a>Etapa 2: Criar uma coleção do Azure RemoteApp
1. Em Olá [portal do Azure](http://manage.windowsazure.com), vá toohello Azure RemoteApp página.
2. Clique em **Novo > Criar com VNET**.
3. Digite um nome para a sua coleção.
4. Escolha Olá plano que você deseja toouse - básico ou padrão.
5. Escolha sua rede virtual da saudação suspensa lista e, em seguida, sua sub-rede.
6. Escolha toojoin-tooyour domínio.
7. Clique em **Criar coleção de RemoteApp**.

Depois de sua coleção do RemoteApp foi criada, clique duas vezes em nome de saudação da coleção de saudação. Isso abrirá Olá **início rápido** página - isso é onde você terminar de configurar coleta de saudação.

Algo deu errado? Check-out Olá [coleção híbrida informações de solução de problemas](remoteapp-hybridtrouble.md).

## <a name="step-3-link-your-collection-toohello-local-domain"></a>Etapa 3: Vincular o domínio local do toohello de coleção
1. Em Olá **início rápido** , clique em **ingressar em um domínio local**.
2. Adicione hello Azure RemoteApp serviço conta tooyour local domínio do Active Directory. Será necessário o nome de domínio hello, unidade organizacional, nome de usuário da conta de serviço e senha.
   
    Essa é uma informação de saudação coletadas se você seguiu as etapas de saudação em [configurar o Active Directory do Azure RemoteApp](remoteapp-ad.md).

## <a name="step-4-link-tooan-azure-remoteapp-image"></a>Etapa 4: Imagem Link tooan Azure RemoteApp
Uma imagem de modelo do RemoteApp do Azure contém programas de saudação que você deseja tooshare com os usuários. Você pode criar um novo [imagem de modelo](remoteapp-imageoptions.md) ou link tooan imagem existente (um já importado ou carregado tooAzure RemoteApp). Também é possível vincular tooone de saudação do Azure RemoteApp [imagens de modelo](remoteapp-images.md) que contêm o Office 365 ou programas do Office 2013 (para uso de avaliação).

Se você estiver carregando a nova imagem de saudação, você precisa tooenter Olá nome e escolher local de saudação para imagem hello. Na próxima página do Assistente de Olá Olá, você ver um conjunto de cmdlets do PowerShell - copiar e executar esses cmdlets de uma imagem especificada com privilégios elevados do Windows PowerShell prompt tooupload hello.

Se você está vinculando tooan imagem de modelo existente, basta especifica nome da imagem hello, local e assinatura do Azure associada.

## <a name="step-5-configure-active-directory-directory-synchronization"></a>Etapa 5: Configurar a sincronização de diretório do Active Directory
Azure RemoteApp requer que você integrar com o Active Directory do Azure pela ou 1) Configurar sincronização do Azure Active Directory com opção de sincronização de senha do hello, ou 2) Configurar sincronização Azure Active Directory sem a opção de sincronização de senha Olá mas usando um domínio que é tooAD federado FS.

Confira [AD Connect](https://blogs.technet.microsoft.com/enterprisemobility/2014/08/04/connecting-ad-and-azure-ad-only-4-clicks-with-azure-ad-connect/) - este artigo ajuda você a configurar a integração de diretórios em quatro etapas.

Consulte o [Roteiro de sincronização do diretório](http://msdn.microsoft.com//library/azure/hh967642.aspx) para as informações de planejamento e etapas detalhadas.

## <a name="step-6-publish-apps"></a>Etapa 6: Publicar aplicativos
Um aplicativo do Azure RemoteApp é Olá aplicativo ou programa que você forneça tooyour usuários. Ele está localizado na imagem de modelo Olá carregado para a coleção de saudação. Quando um usuário acessa um aplicativo, ele aparece toorun no seu ambiente local, mas ele está em execução no Azure.

Antes dos usuários podem acessar aplicativos, você precisa toopublish-los – Isso permite que seus aplicativos de Olá de acesso de usuários por meio do cliente de área de trabalho remota de saudação.

Você pode publicar o conjunto de tooyour vários aplicativos. Na página de publicação Olá, clique em **publicar** tooadd um aplicativo. Você pode publicar de saudação **iniciar** menu Olá da imagem de modelo ou especificando o caminho de saudação na imagem de modelo Olá para o aplicativo hello. Se você escolher tooadd Olá **iniciar** menu, escolha Olá tooadd de programa. Se você escolher tooprovide Olá caminho toohello aplicativo, forneça um nome para o aplicativo hello e Olá caminho toowhere que ele é instalado na imagem de modelo hello.

## <a name="step-7-configure-user-access"></a>Etapa 7: Configurar o acesso do usuário
Agora que você criou sua coleção, é necessário tooadd usuários de saudação que você deseja toouse possível toobe seus recursos remotos. usuários de saudação que você forneça acesso tooneed tooexist no locatário do Active Directory Olá associados com a assinatura de saudação usaram toocreate desta coleção do RemoteApp do Azure.

1. Na página início rápido hello, clique em **configurar o acesso de usuário**.
2. Insira a conta de trabalho da saudação (a partir do Active Directory) ou a conta da Microsoft que você deseja acesso toogrant.
   
   **Observações:**
   
   Certifique-se de que você use Olá  *user@domain.com*  formato.
   
   Se você estiver usando o Office 365 ProPlus em sua coleção, você deve usar identidades do Active Directory Olá para seus usuários. Isso ajuda a validar o licenciamento.
3. Depois que os usuários de saudação forem validados, clique em **salvar**.

## <a name="next-steps"></a>Próximas etapas
É isso – sua coleção híbrida do Azure RemoteApp foi criada e implantada com sucesso. Olá próxima etapa é toohave aos usuários baixar e instalar o cliente de área de trabalho remota hello. Você pode encontrar o cliente Olá Olá URL na página de início rápido do Azure RemoteApp hello. Em seguida, tem os usuários façam logon em cliente hello e acessar Olá aplicativos publicados por você.

### <a name="help-us-help-you"></a>Ajude-nos a ajudar você
Você sabia que na adição toorating neste artigo e fazer comentários para baixo abaixo, você pode fazer alterações toohello artigo? Falta alguma coisa? Há algo errado? Escrevi algo que não ficou muito claro? Role para cima e clique em **Editar no GitHub** toomake alterações - aqueles virão toous para revisão e, em seguida, uma vez que saia neles, você verá suas alterações e aprimoramentos aqui.

