---
title: "dados de usuário aaaMigrate do Azure RemoteApp | Microsoft Docs"
description: "Saiba como toomigrate seus dados de usuário dentro e fora do Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: d7e4fbf1-cb42-4430-94a0-ed6d4676fc86
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: aefc6ccc2c6173754acf6cad06102f27c8cb1d26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-data-into-and-out-of-azure-remoteapp"></a>Como toomigrate dados dentro e fora do Azure RemoteApp
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

Você pode usar várias ferramentas diferentes e métodos tootransfer [dados de usuário](remoteapp-upd.md) dentro e fora do Azure RemoteApp. Veja alguns métodos:

* Copiar e colar usando o compartilhamento da área de transferência
* Copiar arquivos e dados do servidor de arquivos tooa
* Copiar arquivos tooOneDrive para os negócios por meio de um navegador
* Copiar os arquivos usando o redirecionamento

> [!NOTE]
> Não é possível habilitar Olá OneDrive para agentes de sincronização de consumidor ou de negócios - eles [não há suporte para](remoteapp-onedrive.md) no Azure RemoteApp.
> 
> 

## <a name="use-copy-and-paste-in-file-explorer"></a>Usar copiar e colar no Explorador de Arquivos
Copiar e colar usando a área de transferência hello está habilitado em implantações de RemoteApp [por padrão](remoteapp-redirection.md). Isso permite que os usuários copiem arquivos entre seus PCs locais e aplicativos do RemoteApp. Em geral, por meio de curso normal de saudação do uso de aplicativos no RemoteApp, os usuários salvou os arquivos tootheir UPDs - movendo que os dados do RemoteApp são fácil:

1. [Publicar o Explorador de Arquivos como um aplicativo](remoteapp-publish.md) em uma coleção de RemoteApp. (Observe que se trata de uma tarefa administrativa).
2. Direcione seus usuários toolaunch Olá Explorador de arquivos aplicativo publicado e toouse que toocopy e colar arquivos em sua UPD e fora dele.

## <a name="upload-files-and-data-tooa-file-server-by-using-standard-network-file-copy"></a>Upload de arquivos e o servidor de arquivos tooa dados usando a cópia de arquivos de rede padrão
As organizações usam dados gerais de toostore de servidores de arquivos. Se você souber o nome do servidor de saudação ou local, os usuários podem procurar na rede local para o servidor de saudação hello e copie seus arquivos, bem como acima. Novamente você deseja toopublish tooRemoteApp de Explorador de arquivos e compartilhá-lo com seus usuários.

> [!NOTE]
> servidor de arquivo Hello deve estar na rede roteável de saudação RemoteApp implantado em.
> 
> 

## <a name="copy-files-tooonedrive-for-business"></a>Copiar arquivos tooOneDrive para empresas
Embora você não pode habilitar hello OneDrive para o agente de sincronização de negócios no RemoteApp, você ainda pode copiar arquivos de seu tooOneDrive UDP para os negócios por meio de um navegador. 

1. Publicar tooRemoteApp Explorador de arquivos e, em seguida, informe a usuários tooaccess Olá arquivos por meio desse aplicativo. 
2. É mais fácil arquivos de tootransfer se eles são compactados, para que os usuários devem criar um arquivo. zip que contém todos os tooOneDrive de toomove arquivos hello para empresas.
3. Peça ao portal de toohello Office 365 toogo dos usuários e, em seguida, vá tooOneDrive e carregar o arquivo. zip de saudação.

## <a name="copy-files-by-using-drive-redirection"></a>Copiar arquivos usando o redirecionamento de unidade
Se tiver habilitado o [redirecionamento de unidade](remoteapp-redirection.md), você já terá criado uma unidade mapeada para seus usuários. Nesse caso, pode seus arquivos na unidade de saudação redirecionada zip e, em seguida, salvá-los tootheir PC local.

## <a name="how-administrators-can-export-data"></a>Como os administradores podem exportar dados

Administra para o Azure RemoteApp pode exportar todos os discos de perfil de usuário (UDP) para todas as coleções dentro de uma assinatura de tooAzure armazenamento usando o Azure PowerShell cmdlet Export-AzureRemoteAppUserDisk.  Não há nenhuma capacidade tooselect individuais UPD.  Quando Olá comando do PowerShell é executado, cada disco de usuário será um 50gb de tamanho de disco fixo e ser armazenamento tooAzure exportado.  Os custos de armazenamento do Azure incorrerão imediatamente para esse armazenamento.  Quando a execução desse comando Certifique-se de não existem sessões exportação de saudação caso contrário, falhará.

UPDs para implantações do Azure RemoteApp ingressadas no domínio só podem ser usados novamente em uma implantação do RDS; implantações ingressadas fora do domínio não podem ser usadas.  Se esses discos serão usados em uma implantação de RDS é recomendável toouse nosso [automatizada scripts](https://github.com/arcadiahlyy/aramigration) que será exportar, converter e importar saudação do UDP para uma implantação de RDS.

