---
title: aaaConnect tooSQL banco de dados usando o SQL Server Management Studio no Azure RemoteApp | Microsoft Docs
description: "Use este tutorial toolearn como toouse SQL Server Management Studio no Azure RemoteApp para segurança e desempenho ao se conectar tooSQL banco de dados"
services: sql-database
documentationcenter: 
author: adhurwit
manager: jhubbard
ms.assetid: 1052c83c-e7f5-4736-922f-216194d8874b
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: adhurwit
ms.openlocfilehash: 73994f9a1eb3e48efa5d7c4f976b00cfcbc88d75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-sql-server-management-studio-in-azure-remoteapp-tooconnect-toosql-database"></a>Use o SQL Server Management Studio no Azure RemoteApp tooconnect tooSQL banco de dados

> [!IMPORTANT]
> O RemoteApp do Azure está sendo descontinuado. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
>

## <a name="introduction"></a>Introdução
Este tutorial mostra como toouse SQL Server Management Studio (SSMS) no Azure RemoteApp tooconnect tooSQL banco de dados. Ele orienta você pelo processo de saudação de configurar o SQL Server Management Studio no Azure RemoteApp, explica os benefícios de saudação e mostra os recursos de segurança que você pode usar no Azure Active Directory.

**Estimado tempo toocomplete:** 45 minutos

## <a name="ssms-in-azure-remoteapp"></a>SSMS no Azure RemoteApp
O Azure RemoteApp é um serviço RDS no Azure que fornece aplicativos. Saiba mais sobre ele aqui: [O que é o RemoteApp?](../remoteapp/remoteapp-whatis.md)

SSMS em execução no Azure RemoteApp permite você Olá mesma experiência como executando o SSMS localmente.

![Captura de tela mostrando o SSMS em execução no Azure RemoteApp][1]

## <a name="benefits"></a>Benefícios
Há muitos benefícios toousing SSMS no Azure RemoteApp, incluindo:

* A porta 1433 no Azure SQL server não tem toobe exposta externamente (fora do Azure).
* Nenhum tookeep necessidade, adicionando e removendo endereços IP no firewall de servidor do SQL Azure hello.
* Todas as conexões do Azure RemoteApp ocorrem por HTTPS na porta 443 usando o protocolo de Área de Trabalho Remota
* Ele é multiusuário e pode ser dimensionado.
* Há um ganho de desempenho de se ter o SSMS em Olá mesma região Olá banco de dados SQL.
* Você pode auditar o uso do Azure RemoteApp com a edição Premium Olá do Active Directory do Azure que tem relatórios de atividade do usuário.
* Você pode habilitar a MFA (Multi-Factor Authentication).
* Acesso SSMS em qualquer lugar ao usar qualquer um dos Olá clientes com suporte do Azure RemoteApp que inclui o iOS, Android, Mac, Windows Phone e Windows PC.

## <a name="create-hello-azure-remoteapp-collection"></a>Criar coleção do Azure RemoteApp Olá
Aqui está Olá etapas toocreate sua coleção do RemoteApp do Azure com o SSMS:

### <a name="1-create-a-new-windows-vm-from-image"></a>1. Criar uma nova VM do Windows a partir da Imagem
Use hello "Windows Server Remote Desktop sessão hosts Windows Server 2012 R2" imagem da saudação Galeria toomake sua nova VM.

### <a name="2-install-ssms-from-sql-express"></a>2. Instalar o SSMS do SQL Express
Vá para Olá nova VM e navegar a página de download do toothis: [Microsoft® SQL Server® 2014 Express](https://www.microsoft.com/download/details.aspx?id=42299)

Há um download de tooonly opção SSMS. Após o download, vá para o diretório de instalação do hello e execute a instalação tooinstall SSMS.

Você também precisa tooinstall SQL Server 2014 Service Pack 1. Você pode baixá-lo aqui: [Microsoft SQL Server 2014 Service Pack 1 (SP1)](https://www.microsoft.com/download/details.aspx?id=46694)

O SQL Server 2014 Service Pack 1 inclui uma funcionalidade essencial para trabalhar com o Banco de Dados SQL.

### <a name="3-run-validate-script-and-sysprep"></a>3. Executar o script Validate e o Sysprep
Em Olá a área de trabalho do hello VM é um script PowerShell chamado validar. Execute-o clicando duas vezes nele. Ele verificará que Olá VM está pronto toobe usado para hospedar remoto de aplicativos. Quando a verificação for concluída, ela solicitará toorun sysprep - escolha toorun-lo.

Quando o sysprep for concluído, ele será encerrado Olá VM.

toolearn mais sobre como criar uma imagem do RemoteApp do Azure, consulte: [como toocreate um modelo do RemoteApp da imagem no Azure](http://blogs.msdn.com/b/rds/archive/2015/03/17/how-to-create-a-remoteapp-template-image-in-azure.aspx)

### <a name="4-capture-image"></a>4. Capturar a imagem
Quando a saudação VM parou de funcionar, encontrá-lo no portal atual do hello e capturá-lo.

toolearn mais sobre como capturar uma imagem, consulte [capturar uma imagem de uma máquina virtual do Windows Azure criada com o modelo de implantação clássico Olá](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

### <a name="5-add-tooazure-remoteapp-template-images"></a>5. Adicionar imagens de modelo do RemoteApp tooAzure
Em hello Azure RemoteApp seção portal atual do hello, vá toohello guia de imagens de modelo e clique em Adicionar. Na caixa de pop-up hello, selecione "Importar uma imagem de sua biblioteca de máquinas virtuais" e, em seguida, escolha Olá imagem que você acabou de criar.

### <a name="6-create-cloud-collection"></a>6. Criar uma coleção na nuvem
No portal atual do hello, crie uma nova coleção de nuvem do RemoteApp do Azure. Escolha Olá imagem de modelo que você acabou de importar com o SSMS instalado nele.

![Criar uma nova coleção na nuvem][2]

### <a name="7-publish-ssms"></a>7. Publicar o SSMS
Em Olá publicando guia da sua nova coleção de nuvem, selecione publicar um aplicativo do hello Menu Iniciar e escolha SSMS da lista de saudação.

![Publicar aplicativo][5]

### <a name="8-add-users"></a>8. Adicionar usuários
Na guia de acesso do usuário hello, você pode selecionar usuários Olá que terão acesso toothis Azure RemoteApp coleção que inclui apenas o SSMS.

![Adicionar usuário][6]

### <a name="9-install-hello-azure-remoteapp-client-application"></a>9. Instalar o aplicativo de cliente hello Azure RemoteApp
Você pode baixar e instalar um cliente do Azure RemoteApp aqui: [Baixar | Azure RemoteApp](https://www.remoteapp.windowsazure.com/en/clients.aspx)

## <a name="configure-azure-sql-server"></a>Configurar o Azure SQL Server
Olá somente a configuração necessária é tooensure serviços do Azure está habilitada para o firewall hello. Se você usar essa solução, em seguida, você não precisa tooadd qualquer firewall de saudação do tooopen de endereços IP. tráfego de rede de saudação é permitido toohello do SQL Server é de outros serviços do Azure.

![Permissão do Azure][4]

## <a name="multi-factor-authentication-mfa"></a>Multi-Factor Authentication (MFA)
A MFA pode ser habilitada especificamente para esse aplicativo. Vá toohello guia de aplicativos do Active Directory do Azure. Você encontrará uma entrada para o Microsoft Azure RemoteApp. Se você clicar nesse aplicativo e, em seguida, configurar, você verá a página de saudação abaixo onde você pode habilitar a MFA para este aplicativo.

![Habilitar MFA][3]

## <a name="audit-user-activity-with-azure-active-directory-premium"></a>Auditar a atividade do usuário com o Active Directory Premium do Azure
Se você não tiver Azure AD Premium, você terá que tooturn-lo no hello seção licenças do seu diretório. Com o Premium ativado, você pode atribuir usuários toohello nível de Premium.

Quando você for um usuário tooa no Active Directory do Azure, em seguida, você pode ir toohello atividade guia toosee logon informações tooAzure RemoteApp.

## <a name="next-steps"></a>Próximas etapas
Depois de concluir todas as Olá acima etapas, você será capaz de toorun hello Azure RemoteApp cliente e log com um usuário atribuído. Você verá SSMS como um de seus aplicativos e execute-o como você faria se estivesse instalado em seu computador com tooAzure acessar o SQL server.

Para obter mais informações sobre como toomake Olá conexão tooSQL banco de dados, consulte [conectar tooSQL banco de dados com o SQL Server Management Studio e executar um exemplo de consulta T-SQL](sql-database-connect-query-ssms.md).

Isso é tudo por enquanto. Aproveite!

<!--Image references-->
[1]: ./media/sql-database-ssms-remoteapp/ssms.png
[2]: ./media/sql-database-ssms-remoteapp/newcloudcollection.png
[3]: ./media/sql-database-ssms-remoteapp/mfa.png
[4]: ./media/sql-database-ssms-remoteapp/allowazure.png
[5]: ./media/sql-database-ssms-remoteapp/publish.png
[6]: ./media/sql-database-ssms-remoteapp/user.png