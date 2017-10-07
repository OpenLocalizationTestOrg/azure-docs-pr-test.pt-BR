---
title: "aaaFrequently repositório Azure Data Lake perguntas frequentes | Microsoft Docs"
description: "Orientação sobre a solução de problemas ou a redução de problemas com o Azure Data Lake Store"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: bf7fd555-3e30-43ce-b28c-c3ad0a241fdb
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: eeabdeef18f3b72901bd1a14283f85dd9c0ead44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-azure-data-lake-store"></a>Perguntas frequentes sobre o Azure Data Lake Store
Neste artigo, você aprenderá sobre perguntas frequentes relacionada tooAzure repositório Data Lake.

## <a name="how-can-i-further-protect-my-data-from-region-wide-disasters-or-accidental-deletions"></a>Como proteger ainda mais os dados de desastres no âmbito da região ou exclusões acidentais?
dados de saudação em sua conta do repositório Azure Data Lake serão tootransient resiliente a falhas de hardware dentro de uma região por meio de réplicas automáticas. Isso assegura a durabilidade e alta disponibilidade, Olá reunião SLA de armazenamento do Azure Data Lake. Aqui estão algumas diretrizes sobre como o toofurther proteger seus dados contra falhas de toda a região raras ou exclusões acidentais.

### <a name="disaster-recovery-guidance"></a>Guia de recuperação de desastres
É essencial para cada cliente tooprepare seu próprio plano de recuperação de desastres. Consulte toohello documentação do Azure abaixo toobuild seu plano de recuperação de desastres. Aqui estão alguns recursos que podem ajudar você a criar seu próprio plano.

* [Recuperação de desastre e alta disponibilidade para aplicativos do Azure](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md)
* [Orientações técnicas de resiliência do Azure](../resiliency/resiliency-technical-guidance.md)

#### <a name="best-practices"></a>Práticas recomendadas
É recomendável que você copie seu dados críticos de tooanother conta do repositório Data Lake em outra região com necessidade de toohello de frequência alinhada de seu plano de recuperação de desastres. Há uma variedade de métodos toocopy dados incluindo [ADLCopy](data-lake-store-copy-data-azure-storage-blob.md), [Azure PowerShell](data-lake-store-get-started-powershell.md) ou [do Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md). O Azure Data Factory é um serviço útil para criar e implantar pipelines de movimentação de dados de forma recorrente.

Se ocorrer uma interrupção regional, em seguida, você pode acessar seus dados na região Olá onde dados saudação foi copiados. Você pode monitorar Olá [painel de integridade do serviço Azure](https://azure.microsoft.com/status/) toodetermine Olá status do serviço do Azure globo hello.

### <a name="data-corruption-or-accidental-deletion-recovery-guidance"></a>Orientação de recuperação contra corrupção de dados ou exclusão acidental
Enquanto o Azure Data Lake Store oferece resiliência de dados por meio de réplicas automáticas, isso não impede que seu aplicativo (ou desenvolvedores/usuários) corrompa dados ou os exclua acidentalmente.

#### <a name="best-practices"></a>Práticas recomendadas
a exclusão acidental tooprevent, recomendamos que você primeiro definir políticas de acesso corretas Olá para sua conta do repositório Data Lake.  Isso inclui a aplicação [bloqueios de recursos do Azure](../azure-resource-manager/resource-group-lock-resources.md) toolock para baixo recursos importantes, assim como o controle de acesso no nível de conta e o arquivo aplicando usando Olá disponível [recursos de segurança do repositório Data Lake](data-lake-store-security-overview.md). Também é recomendável que você crie cópias periódicas dos seus dados críticos usando o [ADLCopy](data-lake-store-copy-data-azure-storage-blob.md), o [Azure PowerShell](data-lake-store-get-started-powershell.md) ou o [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md) em outra conta ou pasta do Data Lake Store, ou assinatura do Azure.  Isso pode ser usado toorecover de um incidente de corrupção ou exclusão de dados. O Azure Data Factory é um serviço útil para criar e implantar pipelines de movimentação de dados de forma recorrente.

As organizações também podem habilitar [log de diagnóstico](data-lake-store-diagnostic-logs.md) para seu repositório Azure Data Lake conta toocollect trilhas de auditoria de acesso de dados que fornece informações sobre quem pode ter excluído ou um arquivo atualizado.

## <a name="next-steps"></a>Próximas etapas
* [Introdução ao Azure Data Lake Store](data-lake-store-get-started-portal.md)
* [Proteger dados no Repositório Data Lake](data-lake-store-secure-data.md)

