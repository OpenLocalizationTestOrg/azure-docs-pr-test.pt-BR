---
title: aaaAzure alta disponibilidade do Analysis Services | Microsoft Docs
description: Garantindo a alta disponibilidade do Azure Analysis Services.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 6e09536c5bd7dc7f88f9b662e1a9f42d2b8c969b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="analysis-services-high-availability"></a>Alta disponibilidade do Analysis Services
Este artigo descreve como garantir alta disponibilidade para servidores do Azure Analysis Services. 


## <a name="assuring-high-availability-during-a-service-disruption"></a>Garantindo alta disponibilidade durante uma interrupção do serviço
Embora seja raro, um data center do Azure pode sofrer uma interrupção. Quando uma interrupção ocorre, ela causa uma parada nos negócios que pode durar alguns minutos ou até mesmo horas. A alta disponibilidade geralmente é obtida com redundância do servidor. Com o Azure Analysis Services, você pode obter redundância criando servidores secundários adicionais em uma ou mais regiões. Ao criar servidores redundantes, dados de saudação tooassure e metadados nesses servidores está em sincronia com o servidor de saudação em uma região que ficou offline, você pode:

* Implante modelos tooredundant servidores em outras regiões. Esse método requer processamento de dados no servidor primário e servidores redundantes em paralelo, garantindo que todos os servidores estejam em sincronia.

* Faça backup dos bancos de dados do seu servidor primário e restaure em servidores redundantes. Por exemplo, você pode automatizar o armazenamento de tooAzure backups noturnos e restaurar os servidores redundantes tooother em outras regiões. 

Em ambos os casos, se o servidor primário sofrer uma interrupção, você deve alterar cadeias de caracteres de conexão de saudação em clientes tooconnect toohello servidor em um datacenter regional diferente de relatórios. Essa alteração deve ser considerada um último recurso e apenas caso ocorra uma interrupção catastrófica de data center regional. É mais provável que, após uma interrupção, o data center que hospeda o servidor primário fique online novamente antes de você poder atualizar conexões em todos os clientes. 



## <a name="related-information"></a>Informações relacionadas
[Fazer backup e restaurar](analysis-services-backup.md)   
[Gerenciar Azure Analysis Services](analysis-services-manage.md) 

