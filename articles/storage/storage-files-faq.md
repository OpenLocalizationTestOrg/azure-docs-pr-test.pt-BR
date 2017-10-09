---
title: aaaFrequently perguntas frequentes sobre o armazenamento de arquivo do Azure | Microsoft Docs
description: Encontre respostas toofrequently perguntas frequentes sobre o armazenamento de arquivo do Azure.
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
ms.date: 07/19/2017
ms.author: renash
ms.openlocfilehash: ecd685b3094f51e998bbf5dd0567a20732757015
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-about-azure-file-storage"></a>Perguntas frequentes sobre o armazenamento de Arquivos do Azure

## <a name="general"></a>Geral
* **P. O que é o armazenamento de Arquivos do Azure?**  
   
    O armazenamento de Arquivos do Azure é um sistema de arquivos distribuído no Azure. Ele fornece uma interface do protocolo SMB que possibilita o armazenamento de saudação do toomount de usuários como um compartilhamento nativo na máquina de Virtual do Azure com suporte ou máquina local.

* **P. Por que o armazenamento de Arquivos do Azure é útil?**  
   
    O armazenamento de Arquivos do Azure fornece o acesso a dados compartilhados em várias VMs e plataformas. Consulte também[o armazenamento de arquivo do Azure por que é útil](storage-files-introduction.md#why-azure-file-storage-is-useful).

* **P. Quando devo usar o Arquivo do Azure vs. Blob do Azure vs. Disco do Azure?**  
   
    Microsoft Azure fornece várias maneiras toostore e acessar dados na nuvem hello.  
   
    Armazenamento de arquivo do Azure - fornece uma interface SMB, bibliotecas de cliente e uma interface REST que permite o fácil acesso em qualquer lugar toostored arquivos.  
   
    Azure Blobs - fornece bibliotecas de cliente e uma interface REST que permite que os dados não estruturados toobe armazenados e acessados em grande escala em blobs de bloco.  
   
    Dados do Azure discos - fornece uma interface REST que permite que dados toobe persistentemente armazenados e acessados a partir de um disco rígido virtual conectado e bibliotecas de cliente.  
   
    Saiba mais em [Decidindo quando toouse Azure Blobs, arquivos do Azure ou discos de dados do Azure](storage-decide-blobs-files-disks.md)

* **P. Como fazer para começar a usar o armazenamento de Arquivos do Azure?**  
   
    Comece criando um compartilhamento de arquivos do Azure. Você pode criar compartilhamentos de arquivo do Azure usando o Portal do Azure, Olá cmdlets do PowerShell do armazenamento do Azure, bibliotecas de cliente de armazenamento do Azure hello ou Olá API de REST do armazenamento do Azure. Neste tutorial, você aprenderá:

    * [Saiba como toocreate arquivo Azure compartilhar usando Olá Portal](storage-file-how-to-create-file-share.md#create-file-share-through-the-portal)
    * [Saiba como toocreate arquivo Azure compartilhar usando o Powershell](storage-file-how-to-create-file-share.md#create-file-share-through-powershell)
    * [Saiba como toocreate arquivo Azure compartilhar usando a CLI](storage-file-how-to-create-file-share.md#create-file-share-through-command-line-interface-cli)

* **P. Para quais replicações há suporte no armazenamento de Arquivos do Azure?**  
   
    No momento, o armazenamento de Arquivos do Azure dá suporte apenas ao LRS ou GRS. Planejamos toosupport RA-GRS, mas ainda não houver nenhum tooshare de linha do tempo.

## <a name="security-authentication-and-access-control"></a>Segurança, autenticação e controle de acesso

* **P. Quais são arquivos de tooaccess de maneiras diferentes no armazenamento de arquivo do Azure?**
    
    Você pode montar Olá compartilhamento de arquivos em seu computador local usando o protocolo SMB 3.0 ou use ferramentas como o [Gerenciador de armazenamento](http://storageexplorer.com/) tooaccess arquivos em seu compartilhamento de arquivos. Do seu aplicativo, você pode usar bibliotecas de cliente de armazenamento, APIs REST ou Powershell tooaccess que compartilham seus arquivos no arquivo do Azure.

* **P. Como posso fornecer arquivo específico de tooa de acesso usando um navegador da web?**
    
    Com a SAS, você pode gerar tokens com permissões específicas que são válidas por um intervalo de tempo especificado. Por exemplo, você pode gerar um token com o arquivo específico do tooa acesso somente leitura para um período de tempo específico. Qualquer pessoa que possua essa url pode acessar o arquivo hello diretamente a partir de qualquer navegador da web enquanto ele é válido. Chaves SAS podem ser facilmente geradas na interface do usuário como o Gerenciador de armazenamento.

* **P. É possível toospecify permissões de somente leitura ou somente gravação em pastas no compartilhamento Olá?**
    
    Você não tem esse nível de controle sobre as permissões se montar o compartilhamento de arquivo hello via SMB. No entanto, você pode obter isso criando uma assinatura de acesso compartilhado (SAS) por meio de saudação API REST ou bibliotecas de cliente.  

* **P. Como posso habilitar a criptografia do Servidor no armazenamento de Arquivos do Azure?**

    A [Criptografia do Servidor](storage-service-encryption.md) do armazenamento de Arquivos do Azure está disponível em todas as regiões e nuvens públicas e nacionais. Habilite o SSE no armazenamento de Arquivos do Azure usando o [portal do Azure](https://portal.azure.com/), a [API do Provedor de Recursos do Armazenamento do Microsoft Azure](/rest/api/storagerp/storageaccounts), o [Azure PowerShell](https://msdn.microsoft.com/library/azure/mt607151.aspx) ou a [CLI do Azure](storage-azure-cli.md).
    
    Depois de habilitar SSE no armazenamento de arquivo do Azure, todos os novos dados gravados toohello o armazenamento de arquivos na conta de armazenamento serão criptografados automaticamente. Este recurso está disponível para todos os novos dados gravados tooexisting ou novos compartilhamentos em uma conta de armazenamento existente ou novo. Não há nenhum custo adicional para habilitar esse recurso. Saiba mais em [como tooenable SSE no armazenamento de arquivo do Azure](storage-service-encryption.md).

* **P. Há suporte para a autenticação baseada no Active Directory no armazenamento de Arquivos do Azure?**
   
    Atualmente não damos suporte a autenticação baseada no AD ou em ACLs, mas a temos em nossa lista de solicitações de recursos. Por enquanto, chaves de conta de armazenamento do Azure hello são usadas tooprovide compartilhamento de arquivos de toohello de autenticação. Oferecemos uma solução alternativa usando assinaturas de acesso compartilhado (SAS) por meio de bibliotecas de cliente de API REST ou Olá Olá. Com a SAS, você pode gerar tokens com permissões específicas que são válidas por um intervalo de tempo especificado. Por exemplo, você pode gerar um token com acesso somente leitura tooa dado arquivo com expiração de 10 minutos. Qualquer pessoa que possua esse token enquanto ele é válido tem o arquivo de toothat de acesso somente leitura para os 10 minutos.
   
    Somente há suporte para SAS por meio de bibliotecas de API REST ou cliente hello. Quando você monta Olá compartilhamento de arquivos por meio de saudação protocolo SMB, você não pode usar um conteúdo de tooits SAS toodelegate acesso. 
    
* **P. Quais são as políticas de conformidade do hello dados com suporte para armazenamento de arquivo do Azure?**

   Armazenamento de arquivo do Azure é executado na parte superior do hello mesma arquitetura de armazenamento, como outros tipos de armazenamento de serviços no armazenamento do Azure e aplicam Olá mesmas políticas de conformidade de dados. Mais informações sobre a conformidade de dados de armazenamento do Azure, você pode baixar e consulte muito[documento de proteção de dados do Microsoft Azure](http://go.microsoft.com/fwlink/?LinkID=398382&clcid=0x409).

## <a name="on-premises-access"></a>Acesso local

* **Q.Do tenho rota expressa do Azure toouse tooconnect armazenamento de arquivos tooAzure de uma VM local?**
   
    Não. Se você não tiver a rota expressa, você ainda pode acessar Olá compartilhamento de arquivos do local, desde que a porta 445 (TCP de saída) aberto para acesso à Internet. No entanto, se desejar, você pode usar o ExpressRoute com o armazenamento de Arquivos do Azure.

* **P. Como posso montar o compartilhamento de Arquivos do Azure no computador local?** 
    
    Você pode montar Olá compartilhamento de arquivos por meio do protocolo SMB da saudação desde que a porta 445 (TCP de saída) está aberta e o cliente oferece suporte a protocolo de saudação SMB 3.0 (por exemplo, você estiver usando o Windows 10 ou Windows Server 2012). Trabalhe com a porta de saudação do ISP provedor toounblock local. Em Olá provisório, você pode exibir os arquivos usando [Gerenciador de armazenamento](../vs-azure-tools-storage-explorer-files.md#view-a-file-shares-contents).


## <a name="billing-and-pricing"></a>Cobrança e preços
* **P. Olá o tráfego de rede entre uma VM do Azure e uma contagem de compartilhamento de arquivo como largura de banda externa que é cobrada toohello assinatura?**
   
    Se o compartilhamento de arquivo hello e VM estiverem em Olá mesma região do Azure, hello tráfego entre eles é gratuito. Se eles estiverem em regiões diferentes, tráfego de saudação entre elas será cobrado como largura de banda externa.

## <a name="backup"></a>Backup

* **P. Como fazer backup de meu Compartilhamento de Arquivos do Azure?**
    
    Use o AzCopy, o RoboCopy ou uma ferramenta de backup de terceiros que pode fazer backup de um compartilhamento de arquivos montado. Esperamos que instantâneos de tootake de capacidade toohave Olá de compartilhamentos de arquivos no hello futuro; próximo Você será capaz de toouse toobackup esse recurso de compartilhamento de arquivos o Azure.

## <a name="performance"></a>Desempenho

* **P. Quais são os limites de escala de saudação do armazenamento de arquivos do Azure?**
    Para obter informações sobre as metas de escalabilidade e desempenho do armazenamento de Arquivos do Azure, consulte [Metas de escalabilidade e desempenho do Armazenamento do Azure](storage-scalability-targets.md#scalability-targets-for-blobs-queues-tables-and-files).

* **P. O desempenho foi lento durante a tentativa de toounzip arquivos no armazenamento de arquivo do Azure. O que devo fazer?**
    
    tootransfer grande número de arquivos no armazenamento de arquivo do Azure, recomendamos que você use AzCopy (Windows, a visualização para Unix/Linux) ou o Azure Powershell como essas ferramentas foram otimizadas para transferência de rede.

* **P. O que patches foi lançada toofix problema de desempenho lento com armazenamento de arquivo do Azure?**
    
    a equipe do Windows Hello recentemente lançou um patch de toofix um problema de desempenho lento ao Prezado cliente acessa o armazenamento de arquivo do Azure do Windows 8.1 ou Windows Server 2012 R2. Para obter mais informações, entre check-out Olá associados artigo da KB [diminuir o desempenho quando você acessar o armazenamento de arquivo do Azure do Windows 8.1 ou Server 2012 R2](https://support.microsoft.com/kb/3114025).

## <a name="features-and-interoperability-with-other-services"></a>Recursos e interoperabilidade com outros serviços
* **P. É um "compartilhamento de arquivos" para um cluster de failover em uma saudação casos de uso para armazenamento de arquivo do Azure?**
   
    Atualmente, não há suporte para esse recurso.

* **P. Há uma operação de renomeação em Olá API REST?**
   
    Não no momento.

* **P. É possível ter compartilhamentos aninhados ou seja, um compartilhamento em outro compartilhamento?**
    
    Não. compartilhamento de arquivo Hello é driver de saudação virtual que você pode montar, portanto compartilhamentos aninhados não são suportados.

* **P. Como usar o armazenamento de Arquivos do Azure com o IBM MQ**
    
    IBM lançou clientes documento tooguide IBM MQ ao configurar o armazenamento de arquivo do Azure com seu serviço. Para obter mais informações, faça check-out [como toosetup IBM MQ várias instância Gerenciador de fila com o serviço de arquivo do Microsoft Azure](https://github.com/ibm-messaging/mq-azure/wiki/How-to-setup-IBM-MQ-Multi-instance-queue-manager-with-Microsoft-Azure-File-Service).


## <a name="troubleshooting"></a>Solucionar problemas
* **P. Como fazer para solucionar erros do armazenamento de Arquivos do Azure?**
    
    Você pode consultar muito[artigo de solução de problemas de armazenamento de arquivo do Azure](storage-troubleshoot-file-connection-problems.md) para obter diretrizes sobre solução de problemas de ponta a ponta. 


## <a name="see-also"></a>Consulte também
Consulte estes links para obter mais informações sobre o armazenamento de arquivo do Azure.

### <a name="conceptual-articles-and-videos"></a>Artigos e vídeos conceituais
* [Armazenamento de Arquivos do Azure: um sistema de arquivos SMB de nuvem ininterrupto para Windows e Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [Como toouse armazenamento de arquivo do Azure com Linux](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a>Suporte de ferramentas para o armazenamento de arquivos
* [Usando o PowerShell do Azure com o Armazenamento do Azure](storage-powershell-guide-full.md)
* [Como toouse AzCopy com o armazenamento do Microsoft Azure](storage-use-azcopy.md)
* [Usando Olá CLI do Azure com o armazenamento do Azure](storage-azure-cli.md)
* [Solução de problemas do armazenamento de Arquivos do Azure](storage-troubleshoot-file-connection-problems.md)

### <a name="blog-posts"></a>Postagens no blog
* [O Armazenamento de arquivos do Azure agora está disponível ao público geral](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [Por dentro do Armazenamento de Arquivos do Azure](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [Apresentando o serviço de arquivo do Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [Migrando dados tooAzure armazenamento de arquivo](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a>Referência
* [Referência à Biblioteca de Cliente de Armazenamento para .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [Referência à API REST do serviço de arquivos](http://msdn.microsoft.com/library/azure/dn167006.aspx)
