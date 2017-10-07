---
title: "aaaConfigure autenticação com o Amazon Web Services | Microsoft Docs"
description: "Este artigo descreve como toocreate e validar uma credencial AWS para runbooks na automação do Azure gerenciar recursos AWS."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
keywords: "autenticação aws, configurar aws"
ms.assetid: b6dde4bb-26ac-4876-9aa9-e586bed30d6b
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 11/11/2016
ms.author: magoedte
ms.openlocfilehash: 6edaa000c1b206d80fe64b18c729dac124849070
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-runbooks-with-amazon-web-services"></a>Autenticar runbooks com o Amazon Web Services
A automação de tarefas comuns com recursos do AWS (Amazon Web Services) pode ser realizada com runbooks de Automação no Azure.  Você pode automatizar muitas tarefas no AWS usando runbooks de Automação, assim como faz com recursos no Azure.  Bastam duas coisas:

* Uma assinatura do AWS e um conjunto de credenciais.  Especificamente, sua Chave Secreta e sua Chave de Acesso do AWS.  Para obter mais informações, consulte o artigo Olá [usando as credenciais do AWS](http://docs.aws.amazon.com/powershell/latest/userguide/specifying-your-aws-credentials.html).
* Uma assinatura do Azure e uma conta de Automação.  Para obter mais informações sobre como configurar uma conta de automação do Azure, consulte o artigo Olá [configurar Azure conta executar como](automation-sec-configure-azure-runas-account.md).  

tooauthenticate com AWS, você deve especificar um conjunto de AWS credenciais tooauthenticate seus runbooks em execução de automação do Azure. Se você já tiver uma conta de automação criada e você desejar toouse que tooauthenticate com AWS, você pode seguir etapas Olá Olá seção a seguir.  Se você quiser toodedicated uma conta para recursos AWS direcionando runbooks, você deve primeiro criar um novo [conta executar como automação](automation-sec-configure-azure-runas-account.md) (ignorar Olá opção toocreate uma entidade de serviço) e, em seguida, siga as etapas de saudação abaixo.

## <a name="configure-automation-account"></a>Configurar conta de Automação
Para automação do Azure toocommunicate com AWS, você primeiro precisa tooretrieve suas credenciais AWS e armazená-los como ativos na automação do Azure.  Executar Olá seguindo as etapas documentadas no documento AWS Olá [gerenciar chaves de acesso para sua conta AWS](http://docs.aws.amazon.com/general/latest/gr/managing-aws-access-keys.html) toocreate uma chave de acesso e cópia Olá **ID da chave de acesso** e **chave de acesso do segredo** (opcionalmente baixar o arquivo de chave toostore-lo em um lugar seguro).

Depois de ter criado e copiado suas chaves de segurança AWS, será necessário toocreate um ativo de credencial com uma toosecurely de conta de automação do Azure armazená-los e referenciá-las com seus runbooks.  Siga as etapas de saudação na seção de saudação **criar um novo ativo de credencial** em Olá [credencial ativos na automação do Azure](automation-credentials.md) artigo e digite Olá informações a seguir:

1. Em Olá **nome** , digite **AWScred** ou um valor apropriado aos padrões de nomenclatura a seguir.  
2. Em Olá **nome de usuário** digite sua **ID de acesso** e seu **chave secreta do acesso** em hello **senha** e **confirmar senha** caixa.   

## <a name="next-steps"></a>Próximas etapas
* Artigo de solução de saudação Reivew [automatizar a implantação de uma VM no Amazon Web Services](automation-scenario-aws-deployment.md) toolearn como toocreate runbooks tooautomate as tarefas em AWS.

