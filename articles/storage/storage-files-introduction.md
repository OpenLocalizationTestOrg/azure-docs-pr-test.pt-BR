---
title: aaaIntroduction tooAzure armazenamento de arquivo | Microsoft Docs
description: "Uma visão geral de armazenamento de arquivos do Azure, um serviço que permite que você toocreate e usar arquivo de rede compartilhamentos em Olá nuvem da Microsoft usando o padrão da indústria hello."
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
ms.openlocfilehash: a0a6a80a2ccd9742aa470bdd02ff375387a1629b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-file-storage"></a>Introdução tooAzure armazenamento de arquivo
Armazenamento de arquivo do Azure oferece a compartilhamentos de arquivos de rede em nuvem hello usando o padrão da indústria Olá [protocolo de bloco de mensagens de servidor (SMB)](https://msdn.microsoft.com/library/windows/desktop/aa365233.aspx) e [dinâmica de hosts (CIFS, Common Internet File System)](https://technet.microsoft.com/library/cc939973.aspx). Os compartilhamentos de Arquivos do Azure podem ser montados simultaneamente por clientes como implantações locais do Windows, macOS, Linux ou por Máquinas Virtuais do Azure. Um oferece de conta de armazenamento de uso geral acesso tooAzure armazenamento de arquivos e outros serviços, como Blobs, discos de máquina virtual do Azure, as filas em uma única conta.



## <a name="videos"></a>Vídeos
| Introdução ao armazenamento de Arquivos do Azure (27m) | Tutorial do armazenamento de Arquivos do Azure (5 minutos)  |
|-|-|
| [![Screencap de vídeo de armazenamento de arquivo do Azure apresentando Olá - clique tooplay!](media/storage-file-storage/azure-files-introduction-video-snapshot1.png)](https://www.youtube.com/watch?v=zlrpomv5RLs) | [![Screencap de armazenamento de arquivo do Azure Olá Tutorial - clique tooplay!](media/storage-file-storage/azure-files-introduction-video-snapshot2.png)](https://channel9.msdn.com/Blogs/Azure/Azure-File-storage-with-Windows/) |

## <a name="why-azure-file-storage-is-useful"></a>Por que o armazenamento de Arquivos do Azure é útil
Armazenamento de arquivo do Azure permite que você tooreplace Windows Server, Linux, ou servidores de arquivos com base NAS hospedado no local ou na nuvem Olá com um arquivo de nuvem sem sistema operacional compartilham. Isso tem Olá benefícios a seguir:

* **Acesso compartilhado:**. Protocolo SMB padrão, ou seja, você pode substituir perfeitamente seus compartilhamentos de arquivos local com compartilhamentos de arquivos do Azure sem se preocupar sobre compatibilidade de aplicativos do setor de Olá suporte de compartilhamentos de arquivos do Azure. Ser capaz de tooshare um sistema de arquivos em vários computadores, aplicativos/instâncias é uma vantagem significativa com o armazenamento de arquivo do Azure para aplicativos que precisam da capacidade de compartilhamento. 
* **Totalmente Gerenciado**. Compartilhamentos de arquivos do Azure podem ser criados sem um sistema operacional ou hardware de toomanage de necessidade de saudação. Isso significa que você não tem toodeal com patches do sistema operacional de servidor de saudação com as atualizações críticas de segurança ou substituir os discos rígidos com defeito.
* **Scripts e Ferramentas**. Cmdlets do PowerShell e a CLI do Azure podem ser usado toocreate, montar e gerenciar compartilhamentos de arquivos de armazenamento como parte da administração de saudação de aplicativos do Azure. Você pode criar e gerenciar compartilhamentos de arquivos do Azure usando o Portal do Azure e o Gerenciador de armazenamento do Azure. 
* **Resiliência**. Armazenamento de arquivo do Azure foi desenvolvido de saudação de plano de fundo se toobe sempre disponível. Armazenamento substituindo os compartilhamentos de arquivos local com o arquivo do Azure significa que você não tem mais toowake backup toodeal com quedas de energia locais ou problemas de rede. 
* **Programação Familiar**. Aplicativos em execução no Azure podem acessar dados no compartilhamento Olá por meio do arquivo [I/O APIs do sistema](https://msdn.microsoft.com/library/system.io.file.aspx). Os desenvolvedores podem aproveitar, portanto, seu código existente e os aplicativos existentes toomigrate habilidades. Além disso tooSystem APIs de e/s, você pode usar [bibliotecas de cliente de armazenamento do Azure](https://msdn.microsoft.com/library/azure/dn261237.aspx) ou hello [API de REST do armazenamento do Azure](/rest/api/storageservices/file-service-rest-api).

Os compartilhamentos de Arquivos do Azure podem ser usados para:

* **Substituir servidores de arquivos no local**:  
    Armazenamento de arquivo do Azure pode ser usado toocompletely substituir compartilhamentos de arquivos em servidores de arquivos tradicionais locais ou dispositivos NAS. Sistemas operacionais populares, como o Linux, Windows e macOS facilmente pode montar um compartilhamento de arquivos do Azure, onde quer que eles estejam em Olá, mundo.

* **Aplicativos de "Deslocamento e comparação"**:  
    Armazenamento de arquivo do Azure facilita muito "comparar e deslocar" nuvem toohello aplicativos que usam o arquivo local compartilha dados tooshare entre partes do aplicativo hello. toomake isso acontecer, cada VM conecta toohello compartilhamento de arquivos e, em seguida, ele pode ler e gravar arquivos exatamente como ele faria em relação a um arquivo local no compartilhamento.

* **Simplificar o Desenvolvimento na Nuvem**:  
    Armazenamento de arquivo do Azure pode ser usado em um número de diferentes maneiras toosimplify novos nuvem projetos de desenvolvimento.
    * **Configurações de Aplicativo Compartilhado**:  
        Um padrão comum para aplicativos distribuídos é toohave arquivos de configuração em um local centralizado onde eles podem ser acessados de várias VMs diferentes. Esses arquivos de configuração podem ser armazenados em um compartilhamento de Arquivos do Azure e lido por todas as instâncias de aplicativo. Essas configurações também podem ser gerenciadas por meio da interface REST hello, o que permite o acesso em todo o mundo toohello arquivos de configuração.

    * **Compartilhamento de Diagnóstico**:  
        Um compartilhamento de arquivos do Azure também pode ser usado toosave arquivos de diagnóstico como logs, métricas e despejos de memória. Essa disponibilidade por meio de saudação SMB e a interface REST permite que aplicativos toobuild ou utilizar uma variedade de ferramentas de análise para processamento e análise de dados de diagnóstico de saudação.

    * **Desenv/Teste/Depuração**:  
        Quando os desenvolvedores ou administradores estão trabalhando em máquinas virtuais na nuvem hello, muitas vezes eles precisam de um conjunto de ferramentas ou utilitários. A instalação e a distribuição desses utilitários em cada máquina virtual onde eles são necessários pode demorar muito. Com o armazenamento de arquivo do Azure, um desenvolvedor ou administrador pode armazenar suas ferramentas favoritas em um compartilhamento de arquivos, que pode ser conectado facilmente toofrom qualquer máquina virtual.
        
## <a name="how-does-it-work"></a>Como ele funciona?
Gerenciar compartilhamentos de Arquivos do Azure é muito mais simples do que gerenciar compartilhamentos de arquivos locais. Olá diagrama a seguir ilustra Olá construções de gerenciamento de armazenamento de arquivo do Azure:

![Estrutura do Arquivo](../../includes/media/storage-file-concepts-include/files-concepts.png)

* **Conta de armazenamento**: todos os acessos tooAzure armazenamento é feito por meio de uma conta de armazenamento. Confira Escalabilidade e Metas de Desempenho do Armazenamento do Azure para obter detalhes sobre a capacidade da conta de armazenamento.
* **Compartilhamento** : um compartilhamento do armazenamento de Arquivos é um compartilhamento de arquivos SMB no Azure. Todos os arquivos e diretórios devem ser criados em um compartilhamento pai. Uma conta pode conter um número ilimitado de compartilhamentos e um compartilhamento pode armazenar um número ilimitado de arquivos, a capacidade total de 5 TB de toohello saudação do compartilhamento de arquivos.
* **Diretório**: uma hierarquia opcional de diretórios.
* **Arquivo**: um arquivo no compartilhamento de saudação. Pode ser um arquivo de backup too1 TB de tamanho.
* **Formato de URL**: arquivos são acessados usando Olá formato de URL a seguir:  

    ```
    https://<storage account>.file.core.windows.net/<share>/<directory/directories>/<file>
    ```
## <a name="next-steps"></a>Próximas etapas
* [Criar um Compartilhamento de Arquivos do Azure](storage-file-how-to-create-file-share.md)
* [Conexão e Montagem no Windows](storage-file-how-to-use-files-windows.md)
* [Conexão e Montagem no Linux](storage-how-to-use-files-linux.md)
* [Conexão e Montagem no MacOS](storage-file-how-to-use-files-mac.md)
* [Perguntas frequentes](storage-files-faq.md)
* [Solução de problemas](storage-troubleshoot-file-connection-problems.md)

### <a name="conceptual-articles-and-videos"></a>Artigos e vídeos conceituais
* [Armazenamento de Arquivos do Azure: um sistema de arquivos SMB de nuvem ininterrupto para Windows e Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)

### <a name="tooling-support-for-azure-file-storage"></a>Suporte de ferramentas para o armazenamento de Arquivos do Azure
* [Usando o PowerShell do Azure com o Armazenamento do Azure](storage-powershell-guide-full.md)
* [Como toouse AzCopy com o armazenamento do Microsoft Azure](storage-use-azcopy.md)
* [Usando Olá CLI do Azure com o armazenamento do Azure](storage-azure-cli.md#create-and-manage-file-shares)

### <a name="blog-posts"></a>Postagens no blog
* [O Armazenamento de arquivos do Azure agora está disponível ao público geral](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [Por dentro do Armazenamento de Arquivos do Azure](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [Apresentando o serviço de arquivo do Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [Migrando dados tooAzure arquivo](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a>Referência
* [referência à Biblioteca de Cliente de armazenamento para .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [Referência à API REST do serviço de arquivos](http://msdn.microsoft.com/library/azure/dn167006.aspx)
