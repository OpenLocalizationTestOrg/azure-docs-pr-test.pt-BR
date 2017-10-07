---
title: "aaaResources, funções e controle de acesso no Azure Application Insights | Microsoft Docs"
description: "Proprietários, colaboradores e leitores de percepções de sua organização."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 49f736a5-67fe-4cc6-b1ef-51b993fb39bd
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: bwren
ms.openlocfilehash: a6f6ca0443b5f60239f094606e124f856967d8ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="resources-roles-and-access-control-in-application-insights"></a>Recursos, funções e controle de acesso no Application Insights
Você pode controlar quem tem ler e atualizar dados do access tooyour no Azure [Application Insights][start], usando [controle de acesso baseado em função no Microsoft Azure](../active-directory/role-based-access-control-configure.md).

> [!IMPORTANT]
> Atribuir acesso toousers em Olá **grupo de recursos ou assinatura** toowhich pertence o recurso de aplicativo - não no próprio recurso de saudação. Atribuir Olá **Colaborador de componente do Application Insights** função. Isso garante uniforme controle de acesso tooweb testes e alertas juntamente com o recurso de aplicativo. [Saiba mais](#access).
> 
> 

## <a name="resources-groups-and-subscriptions"></a>Recursos, grupos e assinaturas
Primeiro, algumas definições:

* **Recurso** ‒ uma instância de um serviço do Microsoft Azure. O recurso do Application Insights coleta, analisa e exibe dados de telemetria saudação enviados do seu aplicativo.  Outros tipos de recursos do Azure incluem aplicativos Web, bancos de dados e VMs.
  
    toosee seus recursos, abra Olá [Portal do Azure][portal], entre e clique em todos os recursos. toofind um recurso, tipo de parte de seu nome no campo de filtro de saudação.
  
    ![Lista de recursos do Azure](./media/app-insights-resources-roles-access-control/10-browse.png)

<a name="resource-group"></a>

* [**Grupo de recursos** ] [ group] -cada recurso pertence tooone grupo. Um grupo é uma maneira toomanage relacionadas a recursos, particularmente para controle de acesso. Por exemplo, em um recurso de grupo, você pode colocar um aplicativo Web, um aplicativo de saudação do Application Insights recursos toomonitor e um tookeep de recursos de armazenamento dados exportados.

    ![Escolha Procurar e Grupos de recursos e, em seguida, escolha um grupo](./media/app-insights-resources-roles-access-control/11-group.png)

* [**Assinatura** ](https://manage.windowsazure.com) -toouse Application Insights ou outros recursos do Azure, você entrar tooan assinatura do Azure. Cada grupo de recursos pertence tooone assinatura do Azure, onde você escolha seu pacote de preços e, se for uma assinatura de organização, escolha Olá membros e suas permissões de acesso.
* [**Conta da Microsoft** ] [ account] -Olá, nome de usuário e senha que você use toosign em tooMicrosoft Azure assinaturas, XBox Live, Outlook.com e outros serviços da Microsoft.

## <a name="access"></a>Controlar o acesso no grupo de recursos de saudação
É importante toounderstand que o recurso de toohello adição que você criou para seu aplicativo, há também separar recursos ocultos para alertas e testes da web. Eles são anexado toohello mesmo [grupo de recursos](#resource-group) como seu aplicativo. Você também pode colocar outros serviços do Azure nele, como sites ou armazenamento.

![Recursos no Application Insights](./media/app-insights-resources-roles-access-control/00-resources.png)

toocontrol acessar recursos de toothese, portanto, é recomendável:

* Controlar o acesso no hello **grupo de recursos ou assinatura** nível.
* Atribuir Olá **Colaborador de componente do Application Insights** toousers de função. Isso permite que os testes de web tooedit, alertas e recursos do Application Insights, sem fornecer acesso tooany outros serviços no grupo de saudação.

## <a name="tooprovide-access-tooanother-user"></a>tooprovide tooanother usuário
Você deve ter a assinatura de toohello de direitos de proprietário ou grupo de recursos de saudação.

saudação de usuário deve ter uma [Account da Microsoft][account], ou acessar tootheir [organizacional Microsoft Account](../active-directory/sign-up-organization.md). Você pode fornecer acesso tooindividuals e toouser grupos definidos no Active Directory do Azure.

#### <a name="navigate-toohello-resource-group"></a>Navegue toohello grupo de recursos
Adicione usuário Olá aqui.

![Na folha de recursos do aplicativo, abra o Essentials, abra o grupo de recursos de saudação e nele, selecione configurações/usuários. Clique em Adicionar.](./media/app-insights-resources-roles-access-control/01-add-user.png)

Ou você pode ir para cima outro nível e adicionar Olá usuário toohello assinatura.

#### <a name="select-a-role"></a>Selecione uma função
![Selecione uma função de usuário nova Olá](./media/app-insights-resources-roles-access-control/03-role.png)

| Função | No grupo de recursos de saudação |
| --- | --- |
| Proprietário |Pode alterar qualquer item, incluindo o acesso do usuário |
| Colaborador |Pode editar qualquer item, incluindo todos os recursos |
| Colaborador de componente do Application Insights |Pode editar recursos do Application Insights, testes na Web e alertas |
| Leitor |Pode exibir, mas não pode alterar nada |

A 'edição' inclui a criação, a exclusão e a atualização:

* Recursos
* Testes da Web
* Alertas
* Exportação contínua

#### <a name="select-hello-user"></a>Selecione o usuário Olá

Se o usuário Olá desejado não estiver no diretório hello, você pode convidar qualquer pessoa com uma conta da Microsoft.
(Se ela usa serviços como Outlook.com, OneDrive, Windows Phone ou XBox Live, já tem uma conta da Microsoft.)

## <a name="related-content"></a>Conteúdo relacionado

* [Controle de acesso baseado em função no Azure](../active-directory/role-based-access-control-configure.md)

<!--Link references-->

[account]: https://account.microsoft.com
[group]: ../azure-resource-manager/resource-group-overview.md
[portal]: https://portal.azure.com/
[start]: app-insights-overview.md
