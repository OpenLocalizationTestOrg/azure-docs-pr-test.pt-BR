---
title: aaaHow toouse sua assinatura do Office 365 com o Azure RemoteApp | Microsoft Docs
description: "Saiba como você pode usar sua assinatura do Office 365 em aplicativos do Office tooshare Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: piotrci
manager: mbaldwin
ms.assetid: f82b6e23-2b71-47be-846d-fd93f2652f3c
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 2648868dd28cbcd93e38461ae6dce25eaa5d5e99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-your-office-365-subscription-with-azure-remoteapp"></a>Como toouse sua assinatura do Office 365 com o Azure RemoteApp
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

Você sabia que você pode usar sua assinatura do Office 365 existente no Azure RemoteApp tooshare Office aplicativos da nuvem Olá? Continue lendo para obter informações sobre o Office 365 + opções RemoteApp do Azure, incluindo links tooarticles sobre o Office 365 que ajudarão a fazer hello mais da sua assinatura.

## <a name="how-do-i-use-office-365-accounts-for-azure-remoteapp"></a>Como usar contas do Office 365 para o Azure RemoteApp?
Check-out novo artigo de Peter para todas as informações de Olá: [como toouse Azure RemoteApp com contas de usuário do Office 365](remoteapp-o365user.md)

## <a name="can-i-use-my-office-365-subscription-toorun-office-applications-in-azure-remoteapp"></a>Pode usar meus aplicativos do Office 365 assinatura toorun Office no Azure RemoteApp?
Sim! Na verdade, usando a assinatura do Office 365 é Olá apenas de maneira toobring seu tooAzure de aplicativos do Office RemoteApp.

(Observação: se sua implantação do Azure RemoteApp é entregue por um parceiro de hospedagem, eles podem ser capaz de tooprovide com licenças do Office com base em um [contrato de licença de provedor de serviço](http://www.microsoft.com/en-us/Licensing/licensing-programs/spla-program.aspx))

Olá, BOM em sua assinatura do Office 365 é que ele permite que você use Olá mesmo licença de usuário em muitas plataformas diferentes e ambientes, incluindo Olá nuvem do Azure. Quando você usa os aplicativos do Office no Azure RemoteApp não precisar de toopurchase mais licenças ou configurar suas licenças existentes de qualquer maneira especial. Tudo o que você precisa é de uma assinatura do Office 365 que inclua o [Office 365 ProPlus](https://technet.microsoft.com/library/Gg702619.aspx).

O Office 365 ProPlus permite a [ativação de computador compartilhado](https://technet.microsoft.com/library/Dn782860.aspx) - esse recurso habilita a ativação temporária baseada no usuário para o Office em ambientes virtuais e de nuvem como o Azure RemoteApp (e os Serviços de Área de Trabalho Remota).

Quais planos do Office 365 incluem o Office 365 ProPlus? Check-out Olá [disponibilidade dentro de cada plano de serviço](https://technet.microsoft.com/library/office-365-plan-options.aspx) tabela. Observe que nem todos os planos incluem o Office 365 ProPlus (por exemplo, plano de negócios do Office 365 Olá). Se não tiver seu plano, considere atualizar plano tooa que faz (por exemplo, Office 365 Education E3).

## <a name="ok-so-how-are-my-office-365-proplus-licenses-used-with-azure-remoteapp"></a>OK. Como as minhas licenças do Office 365 ProPlus são usadas com o Azure RemoteApp?
Cada licença de usuário para o Office 365 ProPlus permite que um único usuário ativar aplicativos do Office em too5 computadores e tablets e telefones. Cada ativação está registrada com o usuário Olá até que eles desativar Office em dispositivo hello. (Os usuários podem gerenciar seus dispositivos no hello [portal do Office 365](https://portal.office365.com/).)

Com o Azure RemoteApp um único usuário pode fazer logon em vários computadores de saudação mesmo dia sem perceber. Isso ocorre porque o serviço Olá dimensiona os recursos na nuvem hello, enquanto o usuário Olá vê somente os aplicativos de saudação e programas que você compartilhou e gerencia automaticamente. Para este cenário Office 365 ProPlus oferece um modo de ativação do computador compartilhado – isso significa que o usuário não precisa toodo qualquer tooaccess de gerenciamento de licença desses recursos e que computadores individuais Olá não contam com relação ao limite de ativação de computador Olá 5.

Como você (Olá administrador) atribuir licenças do Office 365 ProPlus tooyour usuários, eles podem usar o Office em seus dispositivos pessoais, bem como por meio de sua coleção do RemoteApp.

## <a name="which-office-applications-can-i-use-with-office-365-and-azure-remoteapp"></a>Quais aplicativos do Office posso usar com o Office 365 e o Azure RemoteApp?
Você pode usar o tooactivate de assinatura do Office 365 e compartilhar o Office 2013 em implantações do Azure RemoteApp. Estamos atualmente não suportam uso de saudação de outras versões do Office com o Azure RemoteApp. Isso inclui o Office 2003, Office 2007, Office 2010 e Office 2016.

## <a name="what-about-visio-pro-or-project-pro"></a>E quanto ao Visio Pro ou o Project Pro?
imagem do Office 365 ProPlus Olá incluída na sua assinatura do RemoteApp inclui Visio Pro e Pro do projeto. Mas você não pode usar o Office 365 ProPlus tooactivate de assinatura desses programas - cada um deles tem sua própria licença. Você pode ativá-los no hello [portal do Office 365](https://portal.office365.com/). 

Você não tem toolicense esses programas se você não quiser toouse-los. Apenas ativar programas Olá você deseja toouse - e ignorar Olá outras pessoas. Você ainda poderá vê-los na imagem hello, mas você não pode usá-los. 

## <a name="how-do-i-get-started-with-office-365-and-azure-remoteapp"></a>Como posso começar a usar o Office 365 e o Azure RemoteApp?
Agora que você sabe os detalhes de saudação do licenciamento do Office 365, vamos começar a usá-lo no Azure RemoteApp - é muito fácil:

Quando você cria sua coleção do RemoteApp do Azure, use Olá **Office 365 ProPlus (assinatura necessária)** imagem.

![Imagem do Azure RemoteApp com o Office 365 Pro Plus](./media/remoteapp-officesubscription/remoteapp-officeimage.png)

Esta imagem contém a versão mais recente de saudação do Windows Server e o Office 365 ProPlus. Depois de configurar sua coleção (incluindo aplicativos de publicação), seus usuários apenas fazem logon no Azure RemoteApp (usando seu cliente do RemoteApp) e fornecem suas credenciais do Office 365 para todos os aplicativos do Office. As licenças serão entregues automaticamente sem que haja a necessidade de configuração ou gerenciamento.

## <a name="can-i-create-a-custom-image-with-office-365-proplus"></a>Posso criar uma imagem personalizada com o Office 365 ProPlus?
Você pode criar uma imagem personalizada para a sua coleção que contém o Office 365 ProPlus. Há 2 opções - imagem da Galeria do Azure use Olá que fornecemos ou você pode criar sua própria imagem personalizada e instalar o Office 365 ProPlus existe.

### <a name="use-hello-azure-gallery-image"></a>Usar imagem de galeria do Azure Olá
toodeploy de maneira mais fácil de saudação coleção do Office 365 ProPlus tooa é muito[iniciar com uma das imagens de galeria do Azure Olá](remoteapp-image-on-azurevm.md) incluído na sua assinatura do Azure RemoteApp. Verifique se você escolher Olá **Windows Server Desktop Host da sessão remota com o Office 365 ProPlus pré-instalado** imagem. Em seguida, instale quaisquer outros aplicativos que você deseja na imagem, e você está pronto toogo.

### <a name="use-a-custom-image"></a>Usar uma imagem personalizada
Você sempre pode criar uma imagem personalizada – você pode criar um [VM do Azure](remoteapp-image-on-azurevm.md) ou [criar imagem de saudação localmente](remoteapp-create-custom-image.md) e carregá-lo tooAzure. Em qualquer caso, verifique se que você instala o Office 365 ProPlus com o nó de ativação do computador compartilhado hello. Saudação de uso [ferramenta de implantação do Office](http://blogs.technet.com/b/odsupport/archive/2014/07/11/using-the-office-deployment-tool.aspx) e siga Olá [instruções](https://technet.microsoft.com/library/Dn782858.aspx) para instalação.  

### <a name="disable-automatic-updates-for-office-365-proplus-in-your-custom-image---important"></a>Desabilitar atualizações automáticas para o Office 365 ProPlus na imagem personalizada – IMPORTANTE
Sua imagem personalizada é usada pelo RemoteApp do Azure como um modelo para adicionar recursos adicionais como a demanda de saudação de seu usuários aumenta. problemas de conexão e atrasos tooprevent desabilitar as atualizações automáticas para o Office na imagem de saudação. Se você não fizer isso, cada recurso criado com esse modelo será atualizado automaticamente quando iniciado. Em vez disso, use processo padrão do Azure RemoteApp de saudação para atualizar sua imagem personalizada. Dessa forma você atualizar aplicativos do Office Olá uma vez na imagem de modelo de saudação e, em seguida, permitir que o Azure RemoteApp cuidar da obtenção de atualizações de saudação tooyour usuários.

as atualizações automáticas toodisable, adicionar Olá toohello arquivo de configuração de ferramenta de implantação do Office a seguir:

        <Updates Enabled="FALSE" />

Agora, o arquivo de configuração deve conter estas linhas:

        <Display Level="NONE" AcceptEULA="TRUE" />
        <Property Name="SharedComputerLicensing" Value="1" />
        <Updates Enabled="FALSE" />

## <a name="so-how-can-i-update-an-image-with-office-365-proplus"></a>Como é possível atualizar uma imagem com o Office 365 ProPlus?
Há imagem de saudação do muitos motivos tooupdate em sua coleção. Veja abaixo algumas delas:

* Obter as últimas atualizações do Windows hello 
* Obter as últimas atualizações do aplicativo Office 365 ProPlus Olá
* Atualizar seu aplicativo personalizado
* Alterar outras definições de configuração para a própria imagem Olá

Para etapas de ponta a ponta Olá para atualizar sua coleção toouse Olá imagem que você atualizou, vá [aqui](remoteapp-update.md). Mas, para obter informações sobre como tooupdate Olá imagem e o Office 365 ProPlus, check-out Olá informações a seguir.

Você tem duas opções para atualizar sua imagem: substituir a imagem por uma totalmente nova ou atualizar manualmente a imagem existente.

### <a name="replace-your-image-with-hello-latest-azure-gallery-image--add-customizations"></a>Substitua a imagem com a imagem da Galeria do Azure mais recente da saudação + adicionar personalizações
Com essa opção, você deixar a Microsoft cuidar de atualizações de servidor do Windows e o Office 365 ProPlus hello. Em vez de atualizar a imagem existente, você criará uma imagem completamente nova com base em imagem da Galeria de hello mais recente. Em seguida, repita as etapas que você fez antes da imagem de saudação toocustomize - instalar aplicativos personalizados, modifique a configuração de imagem hello, etc.

imagens da Galeria Olá são atualizadas regularmente, para que você possa ter fácil, sabendo que seus aplicativos do Windows Server e o Office 365 ProPlus estão backup toodate. Naturalmente, compensação de saudação é que você terá tooapply suas personalizações sempre que você tenha uma nova imagem. Você pode criar scripts tooautomate definindo suas personalizações.

### <a name="manually-update-your-existing-image"></a>Atualizar manualmente a imagem existente
Com essa opção, você usar a imagem padrão do Windows ferramentas tooapply atualizações toohello. Para o Office 365 ProPlus, use toodownload de ferramenta de implantação do Office de hello e instalar as atualizações mais recentes de saudação ou versões do Office 365 ProPlus.

> [!IMPORTANT]
> Lembre-se: Desativar atualizações automáticas do Office 365 ProPlus hello.
> 
> 

Precisar de mais informações sobre como usar Olá, ferramenta de implantação do Office para atualizações?

* [Implantar o clique em executar para produtos do Office 365 usando Olá, ferramenta de implantação do Office](https://technet.microsoft.com/library/JJ219423.aspx)
* [Olá Implantando e atualizando Office 365 ProPlus usando a ferramenta de implantação do Office](https://channel9.msdn.com/Events/Ignite/2015/BRK3168) (vídeo)
* [Definir configurações de atualização para o Office 365 ProPlus](https://technet.microsoft.com/library/dn761708.aspx)

