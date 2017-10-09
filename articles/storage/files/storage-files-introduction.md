---
title: aaaIntroduction tooAzure armazenamento de arquivo | Microsoft Docs
description: "Compartilhamentos de Introdução tooAzure armazenamento de arquivo, que fornece arquivos de rede em Olá Microsoft Cloud"
services: storage
documentationcenter: 
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
ms.openlocfilehash: fe6826e79c364a6956831d2e273c4342a5fd47f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-file-storage"></a>Introdução tooAzure armazenamento de arquivo

Armazenamento de arquivo do Azure oferece a compartilhamentos de arquivos de rede em nuvem hello usando o padrão da indústria Olá [protocolo de bloco de mensagens de servidor (SMB)](https://msdn.microsoft.com/library/windows/desktop/aa365233.aspx) e [dinâmica de hosts (CIFS, Common Internet File System)](https://technet.microsoft.com/library/cc939973.aspx). Os compartilhamentos de Arquivos do Azure podem ser montados simultaneamente por Máquinas Virtuais do Azure e implantações locais que executam Windows, macOS ou Linux. Um oferece de conta de armazenamento de uso geral acesso tooAzure o armazenamento de arquivos, armazenamento de BLOBs do Azure e armazenamento de fila do Azure.

## <a name="videos"></a>Vídeos
| Introdução ao armazenamento de Arquivos do Azure (27m) | Tutorial do armazenamento de Arquivos do Azure (5 minutos)  |
|-|-|
| [![Screencast de vídeo de armazenamento de arquivo do Azure apresentando Olá - clique tooplay!](./media/storage-files-introduction/azure-files-introduction-video-snapshot1.png)](https://www.youtube.com/watch?v=zlrpomv5RLs) | [![Screencast hello Azure de armazenamento de arquivos do Tutorial - clique tooplay!](./media/storage-files-introduction/azure-files-introduction-video-snapshot2.png)](https://channel9.msdn.com/Blogs/Azure/Azure-File-storage-with-Windows/) |

## <a name="why-azure-file-storage-is-useful"></a>Por que o armazenamento de Arquivos do Azure é útil

Armazenamento de arquivo do Azure permite que você tooreplace Windows Server, Linux, ou servidores de arquivos com base NAS hospedado no local ou na nuvem Olá com um arquivo de nuvem sem sistema operacional compartilham. Armazenamento de arquivo do Azure tem Olá benefícios a seguir:

* **Acesso compartilhado** setor de Olá suporte ao protocolo SMB padrão, ou seja, você pode substituir perfeitamente seus compartilhamentos de arquivos local com compartilhamentos de arquivos do Azure sem se preocupar sobre compatibilidade de aplicativos de compartilhamentos de arquivos do Azure. Sendo tooaccess capaz de um compartilhamento de arquivos de vários computadores e aplicativos/instâncias é uma vantagem significativa com o armazenamento de arquivo do Azure.

* **Totalmente gerenciado** compartilhamentos de arquivos do Azure podem ser criados sem hardware de toomanage necessidade hello ou um sistema operacional, o que significa que você não tem toodeal com patches do sistema operacional de servidor de saudação com as atualizações críticas de segurança ou substituir os discos rígidos com defeito.

* **Scripts e ferramentas** CLI do Azure e cmdlets do PowerShell podem ser usado toocreate, montar e gerenciar compartilhamentos de arquivos do Azure como parte da administração de saudação de aplicativos do Azure. Você pode criar e gerenciar compartilhamentos de arquivos do Azure usando Olá [portal do Azure](https://portal.azure.com) e hello [Azure Storage Explorer](https://storageexplorer.com). 

* **Resiliência** armazenamento de arquivo do Azure foi criado de saudação de plano de fundo se toobe sempre disponível. Armazenamento substituindo os compartilhamentos de arquivos local com o arquivo do Azure significa que você não tem mais toowake backup toodeal com quedas de energia locais ou problemas de rede. 

* **Programação familiar** aplicativos em execução no Azure podem acessar dados no compartilhamento de saudação via [I/O APIs do sistema de arquivos](https://msdn.microsoft.com/library/system.io.file.aspx). Os desenvolvedores podem aproveitar, portanto, seu código existente e os aplicativos existentes toomigrate habilidades. Além disso tooSystem APIs de e/s, você pode usar qualquer cliente de armazenamento do Azure Olá bibliotecas, como Olá um para [.NET](/dotnet/api/overview/azure/storage?view=azure-dotnet), ou hello [API de REST do armazenamento do Azure](/rest/api/storageservices/file-service-rest-api).

Os compartilhamentos de Arquivos do Azure podem ser usados para:

* **Substituição de servidores de arquivos no local** armazenamento de arquivo do Azure pode ser usado toocompletely substituir compartilhamentos de arquivos em servidores de arquivos tradicionais locais ou dispositivos NAS. Sistemas operacionais populares, como o Linux, Windows e macOS facilmente pode montar um compartilhamento de arquivos do Azure, onde quer que eles estejam em Olá, mundo.

* **Aplicativos de "Deslocamento e comparação"**

    Armazenamento de arquivo do Azure facilita muito "comparar e deslocar" nuvem toohello aplicativos que usam o arquivo local compartilha dados tooshare entre partes do aplicativo hello. tooimplement isso, cada VM conecta toohello compartilhamento de arquivos e, em seguida, ele pode ler e gravar arquivos exatamente como ele faria em relação a um arquivo local no compartilhamento.

* **Simplificar o Desenvolvimento na Nuvem**
    
    Armazenamento de arquivo do Azure pode ser usado em um número de diferentes maneiras toosimplify novos nuvem projetos de desenvolvimento.
    
    * **Configurações de Aplicativo Compartilhado**
    
        Um padrão comum para aplicativos distribuídos é toohave arquivos de configuração em um local centralizado onde eles podem ser acessados de várias VMs diferentes. Esses arquivos de configuração podem ser armazenados em um compartilhamento de Arquivos do Azure e lido por todas as instâncias de aplicativo. Essas configurações também podem ser gerenciadas por meio da interface REST hello, o que permite o acesso em todo o mundo toohello arquivos de configuração.

    * **Compartilhamento de Diagnóstico**
    
        Um compartilhamento de arquivos do Azure também pode ser usado toosave arquivos de diagnóstico como logs, métricas e despejos de memória. Ter compartilhamentos de arquivos disponíveis por meio de saudação SMB e a interface REST permite que aplicativos toobuild ou utilizar uma variedade de ferramentas de análise para processamento e análise de dados de diagnóstico de saudação.

    * **Desenv/Teste/Depuração**

        Quando os desenvolvedores ou administradores estão trabalhando em máquinas virtuais na nuvem hello, muitas vezes eles precisam de um conjunto de ferramentas ou utilitários. A instalação e a distribuição desses utilitários em cada máquina virtual onde eles são necessários pode demorar muito. Com o armazenamento de arquivo do Azure, um desenvolvedor ou administrador pode armazenar suas ferramentas favoritas em um compartilhamento de arquivos, que pode ser conectado facilmente toofrom qualquer máquina virtual.
        
## <a name="how-does-it-work"></a>Como ele funciona?

Gerenciar compartilhamentos de Arquivos do Azure é muito mais simples do que gerenciar compartilhamentos de arquivos locais. Olá diagrama a seguir ilustra Olá construções de gerenciamento de armazenamento de arquivo do Azure:

![Estrutura do Arquivo](./media/storage-files-introduction/files-concepts.png)

* **Conta de armazenamento** todos os acessos tooAzure armazenamento é feito por meio de uma conta de armazenamento. Consulte [Escalabilidade e Metas de Desempenho](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json) para obter detalhes sobre a capacidade da conta de armazenamento.

* **Compartilhamento** Um compartilhamento do Armazenamento de Arquivos é um compartilhamento de arquivos SMB no Azure. Todos os arquivos e diretórios devem ser criados em um compartilhamento pai. Uma conta pode conter um número ilimitado de compartilhamentos e um compartilhamento pode armazenar um número ilimitado de arquivos, a capacidade total de 5 TB de toohello saudação do compartilhamento de arquivos.

* **Diretório** Uma hierarquia opcional de diretórios.

* **Arquivo** um arquivo no compartilhamento de saudação. Pode ser um arquivo de backup too1 TB de tamanho.

* **Formato de URL** arquivos são acessados usando Olá formato de URL a seguir:  

    ```
    https://<storage account>.file.core.windows.net/<share>/<directory/directories>/<file>
    ```

## <a name="next-steps"></a>Próximas etapas

* [Criar um Compartilhamento de Arquivos do Azure](storage-how-to-create-file-share.md)
* [Conexão e Montagem no Windows](storage-how-to-use-files-windows.md)
* [Conexão e Montagem no Linux](storage-how-to-use-files-linux.md)
* [Conexão e Montagem no MacOS](storage-how-to-use-files-mac.md)
* [Perguntas frequentes](../storage-files-faq.md)
* [Solução de problemas no Windows](storage-troubleshoot-windows-file-connection-problems.md)   
* [Solução de problemas no Linux](storage-troubleshoot-linux-file-connection-problems.md)   

<!-- Rena I would remove any articles from here that are more than a year old. - Robin-->
### <a name="conceptual-articles-and-videos"></a>Artigos e vídeos conceituais
* [Armazenamento de Arquivos do Azure: um sistema de arquivos SMB de nuvem ininterrupto para Windows e Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)

### <a name="tooling-support-for-azure-file-storage"></a>Suporte de ferramentas para o armazenamento de Arquivos do Azure
* [Como toouse AzCopy com o armazenamento do Microsoft Azure](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [Usando Olá CLI do Azure com o armazenamento do Azure](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#create-and-manage-file-shares)

### <a name="blog-posts"></a>Postagens no blog
* [O Armazenamento de arquivos do Azure agora está disponível ao público geral](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [Por dentro do Armazenamento de Arquivos do Azure](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [Apresentando o serviço de arquivo do Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [Migrando dados tooAzure arquivo](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a>Referência
* [Referência à Biblioteca de Cliente de Armazenamento para .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [Referência à API REST do serviço de arquivos](http://msdn.microsoft.com/library/azure/dn167006.aspx)
