---
title: "aaaHow toouse armazenamento do Azure para SQL Server backup e restauração | Microsoft Docs"
description: "Saiba como tooback o SQL Server tooAzure armazenamento. Explica os benefícios de saudação do backup dos bancos de dados SQL tooAzure armazenamento."
services: virtual-machines-windows
documentationcenter: 
author: MikeRayMSFT
manager: jhubbard
tags: azure-service-management
ms.assetid: 0db7667d-ef63-4e2b-bd4d-574802090f8b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/31/2017
ms.author: mikeray
ms.openlocfilehash: 67ebe8377be97df1312f8c1345e23576aabe0c4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-for-sql-server-backup-and-restore"></a>Usar o armazenamento do Azure para o backup e restauração do SQL Server
## <a name="overview"></a>Visão geral
Começando com o SQL Server 2012 SP1 CU2, você pode agora gravar backups do SQL Server diretamente toohello serviço de armazenamento de BLOBs do Azure. Você pode usar este tooback funcionalidade tooand restauração do serviço de Blob do Azure Olá com um banco de dados do SQL Server no local ou um banco de dados do SQL Server em uma máquina virtual do Azure. Toocloud backup oferece benefícios de disponibilidade, armazenamento externo ilimitado replicado geograficamente e facilidade de migração de dados tooand da nuvem de saudação. Você pode emitir declarações de BACKUP ou RESTAURAÇÃO usando Transact-SQL ou o SMO.

SQL Server 2016 apresenta novos recursos; Você pode usar [backup de instantâneo de arquivo](http://msdn.microsoft.com/library/mt169363.aspx) tooperform backups quase imediatos e restaurações incrivelmente rápidas.

Este tópico explica por que você pode escolher toouse armazenamento do Azure para backups do SQL e descreve componentes de saudação envolvidos. Você pode usar os recursos de saudação fornecidos no final de saudação do hello artigo tooaccess orientações e informações adicionais toostart usando esse serviço com os backups do SQL Server.

## <a name="benefits-of-using-hello-azure-blob-service-for-sql-server-backups"></a>Benefícios do uso hello serviço Blob do Azure para Backups do SQL Server
Há vários desafios que enfrentamos ao fazer o backup do SQL Server. Esses desafios incluem gerenciamento de armazenamento, o risco de falha de armazenamento, acesso de armazenamento do site toooff e configuração de hardware. Muitos desses desafios são resolvidos usando o serviço de armazenamento de BLOBs do Azure Olá para backups do SQL Server. Considere Olá benefícios a seguir:

* **Facilidade de uso**: armazenar os backups em blobs do Azure pode ser uma opção externo tooaccess conveniente, flexível e fácil. Criar o armazenamento externo para backups do SQL Server podem ser tão fácil quanto modificar as existentes scripts/trabalhos Olá toouse **BACKUP tooURL** sintaxe. Armazenamento externo deve normalmente ser suficiente de tooprevent de local de banco de dados de produção de hello um único desastre que possa afetar Olá externamente e locais do banco de dados de produção. Escolhendo muito[replicar geograficamente os blobs do Azure](../../../storage/common/storage-redundancy.md), você tem uma camada extra de proteção no evento de saudação de um desastre que possa afetar a região inteira hello.
* **Arquivo de backup**: Olá serviço de armazenamento de Blob do Azure oferece uma fita toohello alternativo usado muitas vezes melhor backups de tooarchive de opção. Armazenamento em fita pode exigir o transporte físico tooan instalação e medidas tooprotect Olá mídia externa. Armazenar os backups em armazenamento de BLOBs do Azure fornece um instante e altamente disponível, e a opção de arquivamento de um duráveis.
* **Hardware gerenciado**: não há nenhuma sobrecarga de gerenciamento de hardware com os serviços do Azure. Os serviços do Azure gerenciam o hardware de saudação e fornecem replicação geográfica para redundância e proteção contra falhas de hardware.
* **Armazenamento ilimitado**: Habilitando um blobs tooAzure backup direto, você tem acesso toovirtually armazenamento ilimitado. Como alternativa, fazendo backup de disco de máquina virtual do Azure tooan tem limites com base no tamanho da máquina. Há um toohello limitar o número de discos, você pode anexar tooan máquina virtual do Azure para backups. Esse limite é de 16 discos para uma instância extra grande e menos para instâncias menores.
* **Disponibilidade de backup**: Backups armazenados em blobs do Azure estão disponíveis em qualquer lugar e a qualquer momento e podem ser facilmente acessados para restaurações tooeither um SQL Server no local ou em outro SQL Server em execução em uma máquina de Virtual do Azure, sem necessidade de saudação Para anexar/desanexar o banco de dados ou baixar e anexar Olá VHD.
* **Custo**: pague apenas pelo serviço de saudação que é usado. Pode ser econômico como uma opção de arquivamento externo e backup. Consulte Olá [Calculadora de preços do Azure](http://go.microsoft.com/fwlink/?LinkId=277060 "Calculadora de preços")e hello [artigo preços do Azure](http://go.microsoft.com/fwlink/?LinkId=277059 "preços artigo") para obter mais informações informações.
* **Instantâneos de armazenamento**: quando os arquivos de banco de dados são armazenados em um blob do Azure e você estiver usando o SQL Server 2016, você pode usar [backup de instantâneo de arquivo](http://msdn.microsoft.com/library/mt169363.aspx) tooperform backups quase imediatos e restaurações incrivelmente rápidas.

Para obter mais detalhes, consulte [SQL Server Backup e restauração com o serviço de armazenamento de Blob do Azure](http://go.microsoft.com/fwlink/?LinkId=271617).

Olá duas seções a seguir apresentam o serviço de armazenamento de BLOBs do Azure hello, incluindo componentes do SQL Server Olá necessário. É importante toounderstand componentes de saudação e os backup de uso toosuccessfully interação e restauração do serviço de armazenamento de BLOBs do Azure hello.

## <a name="azure-blob-storage-service-components"></a>Componentes do serviço de armazenamento de blobs do Azure
seguintes componentes do Azure Hello são usadas durante o backup toohello serviço de armazenamento de BLOBs do Azure.

| Componente | Descrição |
| --- | --- |
| **Conta de armazenamento** |conta de armazenamento Olá é hello ponto de partida para todos os serviços de armazenamento. tooaccess um serviço de armazenamento de BLOBs do Azure, primeiro crie uma conta de armazenamento do Azure. Para obter mais informações sobre o serviço de armazenamento de BLOBs do Azure, consulte [como toouse Olá serviço de armazenamento de BLOBs do Azure](https://azure.microsoft.com/develop/net/how-to-guides/blob-storage/) |
| **Contêiner** |Um contêiner fornece um agrupamento de um conjunto de blobs e pode armazenar um número ilimitado de blobs. toowrite um tooan de backup do SQL Server serviço Blob do Azure, você deve ter pelo menos contêiner raiz de saudação criado. |
| **Blob** |Um arquivo de qualquer tipo e tamanho. BLOBs são endereçados através de Olá formato de URL a seguir: **https://[storage account].blob.core.windows.net/[container]/[blob]**. Para obter mais informações sobre blobs de páginas, consulte [Noções gerais sobre blobs de blocos e blobs de páginas](http://msdn.microsoft.com/library/azure/ee691964.aspx) |

## <a name="sql-server-components"></a>Componentes do SQL Server
seguintes componentes do SQL Server Hello são usadas durante o backup toohello serviço de armazenamento de BLOBs do Azure.

| Componente | Descrição |
| --- | --- |
| **URL** |Uma URL especifica um arquivo de backup exclusivo do tooa identificador de recurso uniforme (URI). Olá URL é tooprovide usado Olá local e nome do arquivo de backup saudação do SQL Server. Olá URL deve apontar tooan blob real, e não apenas um contêiner. Se o blob Olá não existir, ele será criado. Se um blob existente for especificado, BACKUP falhar, a menos que hello > opção WITH FORMAT for especificada. Olá seguinte é um exemplo de URL Olá você especificará Olá comando BACKUP: **http[s]://[storageaccount].blob.core.windows.net/[container]/[FILENAME.bak]**. HTTPS é recomendável, mas não obrigatório. |
| **Credencial** |informações Olá tooconnect necessária e autenticar tooAzure serviço de armazenamento de Blob são armazenadas como uma credencial.  Em ordem para SQL Server toowrite backups tooan BLOBs do Azure ou restauração dele, uma credencial do SQL Server deve ser criada. Para obter mais informações, veja [Credencial do SQL Server](https://msdn.microsoft.com/library/ms189522.aspx). |

> [!NOTE]
> Se você escolher toocopy e carregar um arquivo de backup de toohello serviço de armazenamento de BLOBs do Azure, você deve usar um tipo de blob de página como opção de armazenamento, se você estiver planejando toouse esse arquivo para operações de restauração. RESTAURAÇÃO por meio de um tipo de blob de blocos falhará com um erro.
> 
> 

## <a name="next-steps"></a>Próximas etapas
1. Crie uma conta do Azure caso você ainda não tenha uma. Se você estiver avaliando o Azure, considere Olá [avaliação gratuita](https://azure.microsoft.com/free/).
2. Em seguida, passar por uma saudação tutoriais que o orientam você durante a criação de uma conta de armazenamento e executar uma restauração a seguir.
   
   * **SQL Server 2014**: [Tutorial: Backup do SQL Server 2014 e tooMicrosoft de restauração do serviço de armazenamento de BLOBs do Azure](https://msdn.microsoft.com/library/jj720558\(v=sql.120\).aspx).
   * **SQL Server 2016**: [Tutorial: usando o serviço de armazenamento de BLOBs do Microsoft Azure Olá com bancos de dados do SQL Server 2016](https://msdn.microsoft.com/library/dn466438.aspx)
3. Examine a documentação adicional começando com [Backup e Restauração do SQL Server com o Serviço de Armazenamento de Blobs do Microsoft Azure](https://msdn.microsoft.com/library/jj919148.aspx).

Se você tiver problemas, examine o tópico Olá [tooURL Backup do SQL Server Best Practices and Troubleshooting](https://msdn.microsoft.com/library/jj919149.aspx).

Para ver outras opções de backup e restauração do SQL Server, consulte [Backup e Restauração do SQL Server em Máquinas Virtuais do Azure](virtual-machines-windows-sql-backup-recovery.md).

