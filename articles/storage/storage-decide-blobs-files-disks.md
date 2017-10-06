---
title: aaaDeciding quando toouse Azure Blobs, arquivos do Azure ou discos de dados do Azure
description: "Saiba sobre Olá diferentes maneiras toostore e acessar dados no Azure toohelp que decidir qual tecnologia toouse."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: robinsh
ms.openlocfilehash: 6109affe41e98ed459616a4f91064ded0c74428d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deciding-when-toouse-azure-blobs-azure-files-or-azure-data-disks"></a>Decidindo quando toouse Azure Blobs, arquivos do Azure ou discos de dados do Azure

Microsoft Azure fornece vários recursos no armazenamento do Azure para armazenar e acessar seus dados na nuvem hello. Este artigo aborda os arquivos do Azure, Blobs e discos de dados e é projetado toohelp escolher entre esses recursos.

## <a name="scenarios"></a>Cenários

Olá, a tabela a seguir compara os arquivos, Blobs e discos de dados e mostra cenários de exemplo apropriado para cada.

| Recurso | Descrição | Quando toouse |
|--------------|-------------|-------------|
| **Arquivos do Azure** | Fornece uma interface SMB, bibliotecas de cliente e um [interface REST](/rest/api/storageservices/file-service-rest-api) que permite o acesso em qualquer lugar toostored arquivos. | Você deseja muito "comparar e deslocar" uma nuvem de toohello de aplicativo que já usa dados saudação arquivos nativos sistema APIs tooshare entre ele e outros aplicativos em execução no Azure.<br/><br/>Você quer toostore desenvolvimento e ferramentas de depuração que precisam toobe acessado de várias máquinas virtuais. |
| **Blobs do Azure** | Fornece bibliotecas de cliente e um [interface REST](/rest/api/storageservices/blob-service-rest-api) que permite que os dados não estruturados muito ser armazenados e acessados em grande escala em blobs de bloco. | Você deseja que seu aplicativo toosupport streaming e cenários de acesso aleatório.<br/><br/>Você deseja toobe tooaccess capaz de dados de aplicativos de qualquer lugar. |
| **Discos de Dados do Azure** | Fornece bibliotecas de cliente e um [interface REST](/rest/api/compute/virtualmachines/virtualmachines-create-or-update) que permite que dados toobe persistentemente armazenados e acessados a partir de um disco rígido virtual conectado. | Você deseja toolift e deslocar aplicativos que usam tooread APIs do sistema de arquivos nativos e gravar toopersistent os discos de dados.<br/><br/>Você deseja toostore dados que não seja necessário toobe acessado a partir do disco de Olá Olá fora máquina virtual toowhich estão anexados. |

## <a name="comparison-files-and-blobs"></a>Comparação: Arquivos e Blobs

Olá a tabela a seguir compara os arquivos do Azure com Blobs do Azure.  
  
||||  
|-|-|-|  
|**Atributo**|**Blobs do Azure**|**Arquivos do Azure**|  
|Opções de durabilidade|LRS, ZRS, GRS (e RA-GRS para maior disponibilidade)|LRS, GRS|  
|Acessibilidade|APIs REST|APIs REST<br /><br /> SMB 2.1 e SMB 3.0 (APIs do sistema de arquivos padrão)|  
|Conectividade|APIs REST – No mundo todo|APIs REST – No mundo todo<br /><br /> SMB 2.1 – Na região<br /><br /> SMB 3.0 – No mundo todo|  
|Pontos de extremidade|`http://myaccount.blob.core.windows.net/mycontainer/myblob`|`\\myaccount.file.core.windows.net\myshare\myfile.txt`<br /><br /> `http://myaccount.file.core.windows.net/myshare/myfile.txt`|  
|Diretórios|Namespace simples|Objetos do diretório verdadeiros|  
|Diferenciação entre maiúsculas e minúsculas de nomes|Diferencia maiúsculas de minúsculas|Sem diferenciação entre maiúsculas e minúsculas, mas com preservação de maiúsculas e minúsculas|  
|Capacity|Backup de contêineres do too500 TB|Compartilhamentos de arquivos de 5 TB|  
|Taxa de transferência|O too60 MB/s por blob de bloco|Backup too60 MB/s por compartilhamento|  
|Tamanho do objeto|Backup too200 GB/blob de bloco|Too1TB/arquivo|  
|Capacidade cobrada|Com base nos bytes gravados|Com base no tamanho do arquivo|  
|Bibliotecas de cliente|Vários idiomas|Vários idiomas|  
  
## <a name="comparison-files-and-data-disks"></a>Comparação: Arquivos e Discos de Dados

Os Arquivos do Azure complementam os Discos de Dados do Azure. Um disco de dados só pode ser anexado tooone Máquina Virtual do Azure por vez. Discos de dados são armazenados como blobs de página no armazenamento do Azure de VHDs de formato fixo e são usados por dados duráveis do toostore Olá máquina virtual. Compartilhamentos de arquivos em arquivos do Azure podem ser acessados em Olá mesma maneira que o disco local Olá é acessado (por meio de APIs do sistema de arquivos nativo) e pode ser compartilhada entre várias máquinas virtuais.  
 
Olá, a tabela a seguir compara os arquivos do Azure com discos de dados do Azure.  
 
||||  
|-|-|-|  
|**Atributo**|**Discos de Dados do Azure**|**Arquivos do Azure**|  
|Escopo|Máquina virtual tooa exclusivo|Acesso compartilhado entre várias máquinas virtuais|  
|Instantâneos e cópia|Sim|Não|  
|Configuração|Conectado na inicialização da máquina virtual de saudação|Conectado após a inicialização da máquina virtual Olá|  
|Autenticação|Interno|Configurar com net use|  
|Limpeza|Automático|Manual|  
|Acesso com a REST|Não não possível acessar arquivos dentro de saudação VHD|É possível acessar os arquivos armazenados em um compartilhamento|  
|Tamanho máx.|Disco de 1 TB|Compartilhamento de Arquivos de 5 TB e arquivo de 1 TB no compartilhamento|  
|IOPS máximo de 8 KB|500 IOPS|1.000 IOPS|  
|Taxa de transferência|O too60 MB/s por disco|O too60 MB/s por compartilhamento de arquivos|  

## <a name="next-steps"></a>Próximas etapas

Ao tomar decisões sobre como os dados são armazenados e acessados, você também deve considerar os custos de saudação envolvidos. Para obter mais informações, consulte [Preços do Armazenamento do Azure](https://azure.microsoft.com/pricing/details/storage/).
  
Alguns recursos do SMB não são aplicáveis toohello nuvem. Para obter mais informações, consulte [recursos não suportados pelo Olá serviço arquivo do Azure](/rest/api/storageservices/features-not-supported-by-the-azure-file-service).
  
Para obter mais informações sobre discos de dados, consulte [gerenciar discos e imagens](storage-about-disks-and-vhds-linux.md) e [como tooAttach tooa um disco de dados Máquina Virtual do Windows](../virtual-machines/windows/classic/attach-disk.md).
