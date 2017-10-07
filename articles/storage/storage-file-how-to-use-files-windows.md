---
title: aaaMount um compartilhamento de arquivos do Azure e hello de acesso de compartilhamento no Windows | Microsoft Docs
description: "Monte um compartilhamento de saudação de acesso no Windows e o compartilhamento de arquivos do Azure."
services: storage
documentationcenter: na
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 15ac468d9d7b8e0a195b024926ed4dd9790360d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="mount-an-azure-file-share-and-access-hello-share-in-windows"></a>Montar um compartilhamento de saudação de acesso no Windows e o compartilhamento de arquivos do Azure
[Armazenamento de arquivo do Azure](storage-dotnet-how-to-use-files.md) é o sistema de arquivos de nuvem da Microsoft toouse fácil. Os compartilhamentos de arquivos do Azure podem ser montados no Windows e no Windows Server. Este artigo mostra três toomount de formas diferentes um compartilhamento de arquivos do Azure no Windows: com hello arquivo Explorer da interface do usuário, por meio do PowerShell e por meio de saudação de Prompt de comando. 

Ordem toomount de um arquivo do Azure compartilhar fora Olá região do Azure está hospedado no, como no local ou em uma região do Azure diferente, Olá SO deve oferecer suporte a SMB 3.0. 

O compartilhamento de Arquivos do Azure pode ser montado no computador Windows do local ou na VM do Azure, dependendo da versão do sistema operacional. Tabela abaixo ilustra Olá 

| Versão do Windows        | Versão do SMB |Montável na VM do Azure|Montável no local|
|------------------------|-------------|---------------------|---------------------|
| Windows 7              | SMB 2.1     | Sim                 | Não                  |
| Windows Server 2008 R2 | SMB 2.1     | Sim                 | Não                  |
| Windows 8              | SMB 3.0     | Sim                 | Sim                 |
| Windows Server 2012    | SMB 3.0     | Sim                 | Sim                 |
| Windows Server 2012 R2 | SMB 3.0     | Sim                 | Sim                 |
| Windows 10             | SMB 3.0     | Sim                 | Sim                 |

> [!Note]  
> É sempre recomendável fazer Olá KB mais recente para a sua versão do Windows.

## <a name="aprerequisites-for-mounting-azure-file-share-with-windows"></a></a>Pré-requisitos para montar o compartilhamento de arquivos do Azure com o Windows 
* **Nome da conta de armazenamento**: toomount de compartilhamento de um arquivo do Azure, será necessário Olá o nome da conta de armazenamento hello.

* **Chave de conta de armazenamento**: toomount de compartilhamento de um arquivo do Azure, será necessário Olá o chave de armazenamento primária (ou secundário). Atualmente, as chaves SAS não têm suporte para montagem.

* **Certifique-se de que a porta 445 esteja aberta**: o armazenamento de arquivos do Azure usa o protocolo SMB. SMB se comunica pela porta TCP 445 - Verifique toosee se o firewall não está bloqueando as portas TCP 445 do computador cliente.

## <a name="mount-hello-azure-file-share-with-file-explorer"></a>Montar o compartilhamento de arquivos do Azure Olá Explorador de arquivos
> [!Note]  
> Observe que Olá instruções a seguir são mostradas no Windows 10 e podem diferir ligeiramente em versões mais antigas. 

1. **Abra o Explorador de arquivos**: isso pode ser feito, a abertura da saudação Menu Iniciar, ou pressionando atalho Win + E.

2. **Navegue de item de "Este PC" toohello no lado esquerdo da saudação da janela de saudação. Isso alterará a menus de saudação disponíveis na faixa de opções de saudação. No menu de computador Olá, selecione "Mapear unidade de rede"**.
    
    ![Uma captura de tela de hello "Mapear unidade de rede" menu suspenso](media/storage-file-how-to-use-files-windows/1_MountOnWindows10.png)

3. **Caminho UNC de saudação de cópia de painel "Conectar-se" Olá Olá portal do Azure**: uma descrição detalhada de como toofind essas informações podem ser encontradas [aqui](storage-file-how-to-use-files-portal.md#connect-to-file-share).

    ![caminho UNC de saudação no painel de conectar-se de armazenamento de arquivo do Azure Olá](media/storage-file-how-to-use-files-windows/portal_netuse_connect.png)

4. **Selecione a letra da unidade hello e insira o caminho UNC hello.** 
    
    ![Uma captura de tela da caixa de diálogo hello "Mapear unidade de rede"](media/storage-file-how-to-use-files-windows/2_MountOnWindows10.png)

5. **Saudação de usar o nome de conta de armazenamento anexado com `Azure\` como saudação de nome de usuário e uma chave de conta de armazenamento como senha hello.**
    
    ![Uma captura de tela da caixa de diálogo de credenciais de rede Olá](media/storage-file-how-to-use-files-windows/3_MountOnWindows10.png)

6. **Use o compartilhamento de arquivos do Azure como quiser**.
    
    ![O compartilhamento de arquivos do Azure já está montado](media/storage-file-how-to-use-files-windows/4_MountOnWindows10.png)

7. **Quando você estiver pronto toodismount (ou desconecta) compartilhamento de arquivo do Azure hello, você pode fazer isso, clique com o botão direito na entrada Olá para compartilhamento de saudação em hello "locais de rede" no Explorador de arquivos e selecionando "Desconectar"**.

## <a name="mount-hello-azure-file-share-with-powershell"></a>Montar o compartilhamento de arquivo do Azure Olá com o PowerShell
1. **Compartilhamento de arquivo do Azure Olá toomount do comando de uso a seguir de saudação**: Lembre-se de tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` com informações apropriadas hello.

    ```PowerShell
    $acctKey = ConvertTo-SecureString -String "<storage-account-key>" -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential -ArgumentList "Azure\<storage-account-name>", $acctKey
    New-PSDrive -Name <desired-drive-letter> -PSProvider FileSystem -Root "\\<storage-account-name>.file.core.windows.net\<share-name>" -Credential $credential
    ```

2. **Compartilhamento de arquivo do Azure Use Olá conforme desejado**.

3. **Quando tiver terminado, desmontar o compartilhamento de arquivo do Azure hello usando o comando a seguir de saudação**.

    ```PowerShell
    Remove-PSDrive -Name <desired-drive-letter>
    ```

> [!Note]  
> Você pode usar o hello `-Persist` parâmetro `New-PSDrive` toomake Olá restante de toohello visíveis de compartilhamento de arquivo do Azure do hello SO enquanto montado.

## <a name="mount-hello-azure-file-share-with-command-prompt"></a>Montar o compartilhamento de arquivos do Azure Olá Prompt de comando
1. **Compartilhamento de arquivo do Azure Olá toomount do comando de uso a seguir de saudação**: Lembre-se de tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` com informações apropriadas hello.

    ```
    net use <desired-drive-letter>: \\<storage-account-name>.file.core.windows.net\<share-name> <storage-account-key> /user:Azure\<storage-account-name>
    ```

2. **Compartilhamento de arquivo do Azure Use Olá conforme desejado**.

3. **Quando tiver terminado, desmontar o compartilhamento de arquivo do Azure hello usando o comando a seguir de saudação**.

    ```
    net use <desired-drive-letter>: /delete
    ```

> [!Note]  
> Você pode configurar hello Azure arquivo compartilhamento tooautomatically reconectar-se na reinicialização pelas credenciais de saudação persistentes no Windows. saudação de comando a seguir será mantido credenciais hello:
>   ```
>   cmdkey /add:<storage-account-name>.file.core.windows.net /user:AZURE\<storage-account-name> /pass:<storage-account-key>
>   ```

## <a name="next-steps"></a>Próximas etapas
Consulte estes links para obter mais informações sobre o armazenamento de arquivo do Azure.

* [Perguntas frequentes](storage-files-faq.md)
* [Solução de problemas](storage-troubleshoot-file-connection-problems.md)

### <a name="conceptual-articles-and-videos"></a>Artigos e vídeos conceituais
* [Armazenamento de Arquivos do Azure: um sistema de arquivos SMB de nuvem ininterrupto para Windows e Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [Como toouse armazenamento de arquivo do Azure com Linux](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-azure-file-storage"></a>Suporte de ferramentas para o armazenamento de Arquivos do Azure
* [Usando o PowerShell do Azure com o Armazenamento do Azure](storage-powershell-guide-full.md)
* [Como toouse AzCopy com o armazenamento do Microsoft Azure](storage-use-azcopy.md)
* [Usando Olá CLI do Azure com o armazenamento do Azure](storage-azure-cli.md#create-and-manage-file-shares)
* [Solução de problemas do armazenamento de Arquivos do Azure](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="blog-posts"></a>Postagens no blog
* [O Armazenamento de arquivos do Azure agora está disponível ao público geral](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [Por dentro do Armazenamento de Arquivos do Azure](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [Apresentando o serviço de arquivo do Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [Migrando dados tooAzure arquivo](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a>Referência
* [Referência à Biblioteca de Cliente de Armazenamento para .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [Referência à API REST do serviço de arquivos](http://msdn.microsoft.com/library/azure/dn167006.aspx)
