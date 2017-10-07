---
title: "aaaManage computação power no Azure SQL Data Warehouse (portal do Azure) | Microsoft Docs"
description: "Capacidade de computação toomanage tarefas do portal do Azure. Dimensionar recursos de computação ajustando as DWUs. Ou, pausar e retomar os custos de toosave de recursos de computação."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 233b0da5-4abd-4d1d-9586-4ccc5f50b071
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: b2e84b3763e97ce88c190eecfb64b2d06f727229
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-azure-portal"></a>Gerenciar poder de computação no SQL Data Warehouse do Azure (portal do Azure)
> [!div class="op_single_selector"]
> * [Visão geral](sql-data-warehouse-manage-compute-overview.md)
> * [Portal](sql-data-warehouse-manage-compute-portal.md)
> * [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
> * [REST](sql-data-warehouse-manage-compute-rest-api.md)
> * [TSQL](sql-data-warehouse-manage-compute-tsql.md)
>
>


## <a name="scale-compute-power"></a>Dimensionar poder de computação
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

recursos de computação toochange:

1. Olá abrir [portal do Azure][Azure portal], abra o banco de dados e clique em **escala**.

    ![Clique em Escala.][1]
2. Na folha de escala hello, mova o controle deslizante de saudação à esquerda ou direita toochange configuração de DWU de saudação.

    ![Mover o controle deslizante][2]
3. Clique em **Salvar**. Será exibida uma mensagem de confirmação. Clique em **Sim** tooconfirm ou **sem** toocancel.

    ![Clique em Salvar][3]

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a>Pausar computação
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

toopause um banco de dados:

1. Olá abrir [portal do Azure] [ Azure portal] e abra o banco de dados. Observe que Olá Status é **Online**.

    ![Status online][6]
2. Clique em recursos de computação e memória toosuspend, **pausar**, e, em seguida, será exibida uma mensagem de confirmação. Clique em **Sim** tooconfirm ou **sem** toocancel.

    ![Confirmar pausar][7]
3. Quando o SQL Data Warehouse é iniciar o banco de dados do hello, status de saudação é **pausar**.
4. Quando o status de saudação é **pausado**, Olá pausar operação seja concluída e você não está sendo cobradas DWUs.

    ![Status em pausa][4]

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a>Retomar a computação
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

tooresume um banco de dados:

1. Olá abrir [portal do Azure] [ Azure portal] e abra o banco de dados. Observe que Olá Status é **pausado**.

    ![Pausar banco de dados][4]
2. Clique em banco de dados de saudação tooresume **iniciar**, e, em seguida, será exibida uma mensagem de confirmação. Clique em **Sim** tooconfirm ou **sem** toocancel.

    ![Confirmar retomar][5]
3. Enquanto o SQL Data Warehouse é iniciar o banco de dados de saudação, o status de saudação é "Retomando".
4. Quando o status de saudação é **online**, Olá está pronto.

    ![Status online][6]

<a name="next-steps-bk"></a>

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações, confira [Visão geral de gerenciamento][Management overview].

<!--Image references-->
[1]: ./media/sql-data-warehouse-manage-compute-portal/click-scale.png
[2]: ./media/sql-data-warehouse-manage-compute-portal/move-slider.png
[3]: ./media/sql-data-warehouse-manage-compute-portal/click-save.png
[4]: ./media/sql-data-warehouse-manage-compute-portal/resume-database.png
[5]: ./media/sql-data-warehouse-manage-compute-portal/resume-confirm.png
[6]: ./media/sql-data-warehouse-manage-compute-portal/pause-database.png
[7]: ./media/sql-data-warehouse-manage-compute-portal/pause-confirm.png

<!--Article references-->
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
