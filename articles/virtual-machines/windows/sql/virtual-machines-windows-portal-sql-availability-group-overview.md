---
title: "aaaSQL visão geral dos grupos de disponibilidade de servidor - máquinas virtuais do Azure - | Microsoft Docs"
description: "Este artigo apresenta os Grupos de Disponibilidade do SQL Server em máquinas virtuais do Azure."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 601eebb1-fc2c-4f5b-9c05-0e6ffd0e5334
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/13/2017
ms.author: mikeray
ms.openlocfilehash: ecac8b8c5073021af2aa22a05490bb8c4c20ed17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-sql-server-always-on-availability-groups-on-azure-virtual-machines"></a>Introdução aos grupos de disponibilidade do AlwaysOn do SQL Server em máquinas virtuais do Azure #

Este artigo apresenta os grupos de disponibilidade do SQL Server em máquinas virtuais do Azure. 

Sempre em grupos de disponibilidade em máquinas virtuais do Azure são semelhantes tooAlways grupos de disponibilidade no local. Para obter mais informações, confira [Grupos de disponibilidade Always On (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx). 

diagrama de saudação ilustra as partes de saudação de um grupo de disponibilidade de servidor do SQL de conclusão em máquinas virtuais do Azure.

![Grupo de Disponibilidade](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

Olá diferença chave para um grupo de disponibilidade em máquinas virtuais do Azure é que Olá máquinas virtuais do Azure, exigem um [balanceador de carga](../../../load-balancer/load-balancer-overview.md). o balanceador de carga Olá contém endereços IP Olá para o ouvinte do grupo de disponibilidade de saudação. Se você tiver mais de um grupo de disponibilidade cada grupo exige um ouvinte. Um balanceador de carga pode dar suporte a vários ouvintes.

Quando você estiver pronto toobuild um aroup de disponibilidade do SQL Server em máquinas virtuais do Azure, consulte os tutoriais de toothese.

## <a name="automatically-create-an-availability-group-from-a-template"></a>Criar automaticamente um grupo de disponibilidade de um modelo

[Configurar automaticamente o grupo de disponibilidade Always On na VM do Azure - Resource Manager](virtual-machines-windows-portal-sql-alwayson-availability-groups.md)

## <a name="manually-create-an-availability-group-in-azure-portal"></a>Criar manualmente um grupo de disponibilidade no portal do Azure

Você também pode criar máquinas virtuais de saudação sem modelo hello. Primeiro, complete os pré-requisitos de saudação e criar grupo de disponibilidade de saudação. Consulte Olá seguintes tópicos: 

- [Configurar os pré-requisitos para grupos de disponibilidade do SQL Server Always On nas máquinas virtuais do Azure](virtual-machines-windows-portal-sql-availability-group-prereq.md)

- [Criar grupo de disponibilidade AlwaysOn tooimprove disponibilidade e recuperação de desastres](virtual-machines-windows-portal-sql-availability-group-tutorial.md)

## <a name="next-steps"></a>Próximas etapas

[Configurar um SQL Server sempre no grupo de disponibilidade em máquinas virtuais do Azure em diferentes regiões](virtual-machines-windows-portal-sql-availability-group-dr.md).
