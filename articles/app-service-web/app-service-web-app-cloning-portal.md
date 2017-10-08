---
title: aaaWeb clonagem de aplicativo usando o Portal do Azure
description: Saiba como tooclone toonew seus aplicativos Web aplicativos Web usando o Portal do Azure.
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 20b0ae4e-67e8-4bae-9d74-8a24dc445cce
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2016
ms.author: aelnably
ms.openlocfilehash: 605c4879f34d568e9981c34109f9496731c9ed18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-app-cloning-using-azure-portal"></a>Clonagem de aplicativo do Serviço de Aplicativo do Azure usando o Portal do Azure
Olá clonagem recurso no [aplicativos de Web do serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) permite que você facilmente clonar o aplicativo web existente aplicativos tooa recentemente criado em uma região diferente ou em Olá mesma região. Isso permitirá que os clientes toodeploy um número de aplicativos em regiões diferentes rapidamente e facilmente.

A clonagem de aplicativo atualmente só tem suporte para planos de serviço de aplicativos de camada Premium. novos usos de recurso Olá Olá mesmo limitações de recurso de Backup de aplicativos da Web, consulte [backup de um aplicativo web no serviço de aplicativo do Azure](web-sites-backup.md).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="cloning-an-existing-app"></a>Clonagem de um aplicativo existente
Olá web aplicativo deve estar em execução Olá **Premium** modo para que você toocreate um clone do aplicativo web de saudação.

1. Em Olá [Portal do Azure](https://portal.azure.com/), abra a folha do seu aplicativo web.
2. Clique em **Ferramentas**. Em seguida, no hello **ferramentas** folha, clique em **aplicativo Clone**.
   
    ![][1]
   
   > [!NOTE]
   > Se Olá web app não estiver no hello **Premium** modo, você receberá uma mensagem indicando modos Olá tem suportada para clonagem de aplicativo. Neste ponto, você tem Olá opção tooselect **atualizar**.
   > 
   > 
3. Em Olá **aplicativo Clone** folha forneça um nome do novo aplicativo de web hello, o grupo de recursos e o plano do serviço de aplicativo. Também Olá usuário será capaz de toochoose se tooclone um número de configurações do aplicativo de web de origem ou não.
   
    ![][2]
4. Depois de clicar em **criar** plataforma Olá começará a funcionar sobre como criar um clone do aplicativo de web de origem hello.

## <a name="cloning-an-existing-app-tooan-app-service-environment"></a>Clonagem de um tooan de aplicativo ambiente de serviço de aplicativo existente
Em Olá **aplicativo Clone** cliente de saudação de folha terá Olá opção toochoose um pool de aplicativos em um ambiente de serviço de aplicativo existente.

## <a name="current-restrictions"></a>Restrições atuais
Este recurso está atualmente em visualização, estamos trabalhando tooadd novos recursos ao longo do tempo, Olá lista a seguir são Olá restrições conhecidas na suporte atual Olá de clonagem de aplicativo no Portal do Azure:

* As configurações do Gerenciador de Tráfego do Azure não são clonadas
* As configurações de escala automática não são clonadas
* As configurações de agendamento de backup não são clonadas.
* As configurações da rede virtual não são clonadas
* Ideias de aplicativo não são automaticamente definidas no aplicativo de web de destino Olá
* As configurações de Autenticação Fácil não são clonadas
* A extensão Kudu não é clonada
* As regras de TiP não são clonadas
* O conteúdo do banco de dados não é clonado

### <a name="references"></a>Referências
* [Clonagem de Aplicativo Web usando o PowerShell](app-service-web-app-cloning.md)
* [Fazer backup de um aplicativo Web no Serviço de Aplicativo do Azure](web-sites-backup.md)
* [Como tooCreate um ambiente de serviço de aplicativo](app-service-web-how-to-create-an-app-service-environment.md)
* [Criar um aplicativo Web em um Ambiente de Serviço de Aplicativo](app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [Introdução tooApp ambiente de serviço](app-service-app-service-environment-intro.md)

<!--Image references-->
[1]: ./media/app-service-web-app-cloning-portal/CloningBlade.png
[2]: ./media/app-service-web-app-cloning-portal/CloneSettings.png
