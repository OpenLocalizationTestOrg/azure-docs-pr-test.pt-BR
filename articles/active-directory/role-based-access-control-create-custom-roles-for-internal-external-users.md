---
title: "funções de controle de acesso baseado em função personalizadas aaaCreate e atribuir toointernal e usuários externos no Azure | Microsoft Docs"
description: "Atribuir funções RBAC personalizadas criadas usando o PowerShell e a CLI para usuários internos e externos"
services: active-directory
documentationcenter: 
author: andreicradu
manager: catadinu
editor: kgremban
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/10/2017
ms.author: a-crradu
ms.openlocfilehash: 26793a66d6ca2f771338eed87d10ce2b3b431841
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
## <a name="intro-on-role-based-access-control"></a>Introdução ao controle de acesso baseado em função do Azure

Controle de acesso baseado em função é um recurso de somente portal do Azure permitindo proprietários de saudação de uma assinatura tooassign funções granulares tooother que podem gerenciar escopos de recurso específico em seu ambiente.

RBAC permite melhor gerenciamento de segurança para organizações de grandes porte em SMBs trabalhando com parceiros externos, fornecedores ou freelancers que precisam acessar os recursos de toospecific em seu ambiente, mas não necessariamente toda a infraestrutura de toohello ou qualquer escopos relacionados à cobrança. RBAC permite flexibilidade de saudação do proprietário de uma assinatura do Azure gerenciada por conta de administrador da saudação (função de administrador de serviço em um nível de assinatura) e tem várias toowork usuários convidados em Olá mesma assinatura mas sem qualquer administrativas direitos para ele. De uma perspectiva de cobrança e gerenciamento, o recurso RBAC Olá prova toobe uma opção tempo e gerenciamento eficiente para o uso do Azure em vários cenários.

## <a name="prerequisites"></a>Pré-requisitos
Usando o RBAC no ambiente do Azure de saudação requer:

* Assinatura do Azure com um autônomo atribuído toohello usuário como o proprietário (função de assinatura)
* Ter função de proprietário de saudação do hello assinatura do Azure
* Ter acesso toohello [portal do Azure](https://portal.azure.com)
* Certifique-se Olá toohave seguintes provedores de recursos registrado para a assinatura de usuário Olá: **Microsoft**. Para obter mais informações sobre como tooregister Olá provedores de recursos, consulte [provedores do Gerenciador de recursos, regiões, as versões de API e esquemas](/azure-resource-manager/resource-manager-supported-services.md).

> [!NOTE]
> Assinaturas do Office 365 ou licenças do Active Directory do Azure (por exemplo: acessar tooAzure do Active Directory) provisionado de saudação O365 portal não qualidade usando o RBAC.

## <a name="how-can-rbac-be-used"></a>Como o RBAC pode ser usado
O RBAC pode ser aplicado em três escopos diferentes no Azure. De saudação maior escopo toohello um menor, eles são os seguintes:

* Assinatura (mais alto)
* Grupo de recursos
* Escopo do recurso (hello mais baixo nível de acesso oferta tooan escopo de recursos do Azure individuais de permissões de destino)

## <a name="assign-rbac-roles-at-hello-subscription-scope"></a>Atribuir funções RBAC no escopo de assinatura Olá
Há dois exemplos comuns de momentos em que o RBAC é usado (entre outros):

* Ter usuários externos de organizações de saudação (que não faz parte do Azure Active Directory do usuário do administrador de saudação) convidado toomanage certos recursos ou a assinatura inteira Olá
* Trabalhando com os usuários dentro da organização de saudação (elas fazem parte de locatário do Azure Active Directory do usuário Olá), mas parte de equipes diferentes ou grupos que precisam de acesso granular ou toohello assinatura inteira ou grupos de recursos toocertain ou recurso escopos em Olá ambiente

## <a name="grant-access-at-a-subscription-level-for-a-user-outside-of-azure-active-directory"></a>Conceder acesso no nível da assinatura para um usuário fora do Azure Active Directory
Funções RBAC podem ser concedidas somente pelo **proprietários** de assinatura de saudação, portanto, o usuário de administrador Olá deve estar conectado com um nome de usuário que tem essa função previamente atribuída ou criou Olá assinatura do Azure.

De Olá portal do Azure, depois que você entrar como administrador, selecione "Assinaturas" e escolha Olá desejado um.
![folha de assinatura no portal do Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) por padrão, se o usuário administrador Olá adquiriu Olá assinatura do Azure, usuário Olá aparecerão como **administrador da conta**, esta sendo a função de saudação de assinatura. Para obter mais detalhes sobre funções de assinatura do Azure hello, consulte [adicionar ou alterar funções de administrador do Azure que gerenciam a assinatura de saudação ou serviços](/billing/billing-add-change-azure-subscription-administrator.md).

Neste exemplo, Olá usuário "alflanigan@outlook.com" é hello **proprietário** de hello "Avaliação gratuita" assinatura no hello AAD locatário "Padrão de locatário do Azure". Como esse usuário é o criador de saudação do hello assinatura do Azure com a saudação inicial Account da Microsoft "Outlook" (Microsoft Account = Outlook, etc. ao vivo) Olá nome de domínio padrão para todos os outros usuários adicionados neste locatário será **"@alflaniganuoutlook.onmicrosoft.com"**. Por design, sintaxe de saudação do novo domínio de saudação é formado por reunir Olá nome de usuário e nome de domínio do usuário de saudação que criou o locatário hello e adicionar extensão de saudação **". c o m"**.
Além disso, os usuários podem entrar com um nome de domínio personalizado no locatário Olá depois de adicionar e verificando-lo para o novo locatário de saudação. Para obter mais detalhes sobre como tooverify um nome de domínio personalizado em um locatário do Active Directory do Azure, consulte [adicionar um diretório de tooyour de nome de domínio personalizado](/active-directory/active-directory-add-domain).

Neste exemplo, hello "padrão do Azure" diretório locatário contém somente os usuários com o nome de domínio hello "@alflanigan.onmicrosoft.com".

Depois de selecionar a assinatura hello, usuário de administrador Olá deve clicar em **controle de acesso (IAM)** e **adicionar uma nova função**.





![recurso IAM de controle de acesso no portal do Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/1.png)





![adicionar novo usuário no recurso IAM de controle de acesso no portal do Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/2.png)

Olá próxima etapa é tooselect Olá função toobe atribuído e usuário Olá quem será atribuída à função RBAC hello. Em Olá **função** usuário de administrador de saudação de menu suspenso vê apenas Olá RBAC funções internas que estão disponíveis no Azure. Para obter explicações mais detalhadas sobre cada função e seus escopos atribuíveis, consulte [Funções internas para o Controle de Acesso Baseado em Função do Azure](/active-directory/role-based-access-built-in-roles.md).

o usuário administrador Hello, deverá tooadd endereço de email de saudação do usuário externo hello. Olá esperado é de comportamento para Olá usuário externo toonot aparecem Olá existente de locatário. Depois que o usuário externo Olá foi convidado, ele ficará visível em **assinaturas > controle de acesso (IAM)** com todos os usuários atuais Olá que estão atualmente atribuídos a uma função de RBAC no escopo de assinatura de saudação.





![Adicionar função RBAC toonew permissões](./media/role-based-access-control-create-custom-roles-for-internal-external-users/3.png)





![lista de funções de RBAC no nível de assinatura](./media/role-based-access-control-create-custom-roles-for-internal-external-users/4.png)

usuário Hello "chessercarlton@gmail.com" foi convidado toobe um **proprietário** para Olá assinatura "Avaliação gratuita". Depois de enviar o convite hello, usuário externo Olá receberá um email de confirmação com um link de ativação.
![convite por email para a função RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)

Sendo organização toohello externo, Olá novo usuário não tem os atributos existentes no diretório de "Padrão de locatário do Azure" hello. Elas serão criadas depois que o usuário externo Olá tenha dado consentimento toobe registrada no diretório de saudação que é associado à assinatura Olá que ele foi atribuído uma função.





![mensagem de convite de email para a função de RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/6.png)

usuário externo Olá mostra no hello locatário do Active Directory do Azure de agora em diante como usuário externo e isso pode ser exibido em Olá portal do Azure e no portal clássico do hello.





![folha dos usuários no azure active-directory, portal do Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/7.png)





![folha dos usuários no azure active-directory, portal clássico do Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/8.png)

Em Olá **usuários** em ambos os usuários externos de saudação portais do modo de exibição pode ser reconhecido por:

* tipo de ícone diferentes Olá no hello portal do Azure
* Olá diferente de fornecimento de ponto no portal clássico Olá

No entanto, concedendo **proprietário** ou **Colaborador** acesso tooan usuário externo no hello **assinatura** escopo, não permite que o diretório do usuário do administrador toohello acesso Olá, a menos que Olá **Administrador Global** permite. Em Propriedades do usuário hello, Olá **usuário tipo** que tem dois parâmetros comuns, **membro** e **convidado** pode ser identificado. Um membro é um usuário que está registrado no diretório Olá enquanto um convidado é um diretório de toohello usuário convidado de uma fonte externa. Para obter mais informações, consulte [Como os administradores do Azure Active Directory adicionam usuários de colaboração B2B](/active-directory/active-directory-b2b-admin-add-users).

> [!NOTE]
> Certifique-se de que depois de inserir as credenciais de saudação no portal de hello, usuário externo Olá seleciona diretório correto de saudação toosign no. Olá mesmo usuário pode ter acesso toomultiple diretórios e pode selecionar qualquer uma delas clicando Olá nome de usuário no lado superior direito de saudação em Olá portal do Azure e escolha diretório apropriado Olá na lista suspensa hello.

Ao ser convidados no diretório Olá, usuário externo Olá pode gerenciar todos os recursos de saudação assinatura do Azure, mas não é possível acessar o diretório de saudação.





![acessar o portal do Azure do active directory tooazure restrito](./media/role-based-access-control-create-custom-roles-for-internal-external-users/9.png)

O Azure Active Directory e uma assinatura do Azure não têm uma relação de pai-filho como outros recursos do Azure (por exemplo: máquinas virtuais, redes virtuais, aplicativos Web, armazenamento etc.) têm com uma assinatura do Azure. Todos os hello último é criada, gerenciada e cobrado em uma assinatura do Azure, enquanto uma assinatura do Azure é usado toomanage Olá acesso tooan directory do Azure. Para obter mais detalhes, consulte [assinatura como um Azure está relacionada tooAzure AD](/active-directory/active-directory-how-subscriptions-associated-directory).

De todas as funções internas de RBAC de hello, **proprietário** e **Colaborador** oferecem acesso de gerenciamento completo tooall recursos ambiente hello, Olá diferença sendo que não é possível criar um colaborador e excluir novo Funções RBAC. Olá outras funções internas, como **colaborador da máquina Virtual** oferecem acesso de gerenciamento completo apenas os recursos de toohello indicados pelo nome do hello, independentemente de saudação **grupo de recursos** estão sendo criados em.

Atribuindo Olá RBAC função interna de **colaborador da máquina Virtual** em um nível de assinatura, significa que essa função de Olá Olá atribuídos pelo usuário:

* Pode exibir todas as máquinas virtuais independentemente suas implantação data e hello grupos de recursos fazem parte do
* Tem gerenciamento completo acessar toohello as máquinas virtuais na assinatura Olá
* Não é possível exibir outros tipos de recursos na assinatura Olá
* Não é possível operar nenhuma alteração de uma perspectiva de cobrança

> [!NOTE]
> RBAC sendo um recurso somente do portal do Azure, ele não concede o portal clássico do acesso toohello.

## <a name="assign-a-built-in-rbac-role-tooan-external-user"></a>Atribuir um usuário externo interno do RBAC função tooan
Para um cenário diferente nesse teste, Olá usuário externo "alflanigan@gmail.com" é adicionado como um **colaborador da máquina Virtual**.




![função interna de colaborador de máquina virtual](./media/role-based-access-control-create-custom-roles-for-internal-external-users/11.png)

comportamento de saudação normal para este usuário externo com essa função interna é toosee e gerenciar somente as máquinas virtuais e seu adjacentes Gerenciador de recursos somente recursos necessário durante a implantação. Por design, essas funções limitadas oferecem acesso apenas tootheir correspondente de recursos criados no hello portal do Azure, independentemente alguns ainda podem ser implantados no portal clássico Olá também (por exemplo: máquinas virtuais).





![visão geral da função de colaborador de máquina virtual no portal do azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/12.png)

## <a name="grant-access-at-a-subscription-level-for-a-user-in-hello-same-directory"></a>Conceda acesso em um nível de assinatura para um usuário no hello mesmo diretório
fluxo do processo de saudação é um usuário externo, da função RBAC do Olá administrador perspectiva concessão hello, bem como sendo concedida a função de toohello de acesso de usuário de saudação do tooadding idêntico. diferença de Olá aqui é que o usuário Olá convidado não receberão qualquer convites de email como todos os escopos de recurso Olá em assinatura Olá estarão disponíveis no painel de saudação depois de entrar.

## <a name="assign-rbac-roles-at-hello-resource-group-scope"></a>Atribuir funções RBAC no escopo do grupo de recursos de saudação
Atribuir uma função RBAC em um **grupo de recursos** escopo tem um processo idêntico para atribuição de função hello no nível de assinatura de saudação para ambos os tipos de usuários - externos ou internos (parte do hello mesmo diretório). Olá usuários que recebem a função RBAC Olá é toosee em seu ambiente somente o grupo de recursos de saudação eles tiverem recebido acesso de saudação **grupos de recursos** ícone Olá portal do Azure.

## <a name="assign-rbac-roles-at-hello-resource-scope"></a>Atribuir funções RBAC no escopo do recurso Olá
Atribuir uma função RBAC em um escopo de recursos no Azure tem um processo idêntico para atribuição de função hello no nível de assinatura de saudação ou no nível do grupo de recursos de hello, seguinte Olá mesmo fluxo de trabalho para os dois cenários. Novamente, usuários Olá que recebem a função RBAC Olá podem ver apenas os itens de saudação que eles tiverem recebido acesso para qualquer Olá em **todos os recursos** guia ou diretamente em seu painel.

É um aspecto importante para RBAC no escopo do grupo de recursos ou o escopo do recurso para o diretório correto do hello usuários toomake toohello se toosign-in.





![logon do diretório no portal do Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/13.png)

## <a name="assign-rbac-roles-for-an-azure-active-directory-group"></a>Atribuir funções de RBAC a um grupo do Azure Active Directory
Todos os cenários de saudação usando o RBAC em três escopos diferentes Olá na oferta do Azure privilégio de saudação de gerenciar, implantar e administrar vários recursos como um usuário atribuído sem Olá necessário do gerenciamento de uma assinatura pessoal. Função RBAC Olá independentemente é atribuída a uma assinatura, o grupo de recursos ou o escopo do recurso, todos os recursos de saudação criados mais adiante por usuários Olá atribuído são cobrados em Olá uma assinatura do Azure em que usuários de saudação têm acesso a. Dessa forma, hello usuários com permissões de administrador para essa assinatura do Azure inteira de cobrança tem uma visão geral completa consumo hello, independentemente de quem está gerenciando recursos de saudação.

Para organizações maiores, funções RBAC podem ser aplicadas no hello mesma forma para grupos do Active Directory do Azure considerando perspectiva Olá usuário Olá administrador quer acesso granular de saudação toogrant para equipes ou departamentos inteiros, não individualmente para cada usuário, assim considerá-lo como muito tempo e o gerenciamento eficiente opção. tooillustrate neste exemplo, a saudação **Colaborador** função foi adicionada tooone dos grupos de saudação locatário Olá no nível de assinatura de saudação.





![adicionar função de RBAC a grupos do AAD](./media/role-based-access-control-create-custom-roles-for-internal-external-users/14.png)

Esses grupos são grupos de segurança provisionados e gerenciados somente dentro do Azure Active Directory.

## <a name="create-a-custom-rbac-role-tooopen-support-requests-using-powershell"></a>Criar um suporte de tooopen função RBAC personalizado solicitações usando o PowerShell
funções RBAC internas Olá que estão disponíveis no Azure Verifique determinados níveis de permissão com base nos recursos disponíveis Olá ambiente hello. No entanto, se nenhuma dessas funções atenderem às necessidades do usuário do administrador Olá, há acesso toolimit de opção de saudação ainda mais com a criação de funções RBAC personalizadas.

Criar funções personalizadas de RBAC requer tootake uma função interna, editá-lo e, em seguida, importá-lo novamente no ambiente de saudação. download de saudação e o carregamento da função hello são gerenciados usando o PowerShell ou CLI.

É importante toounderstand Olá pré-requisitos de criação de uma função personalizada que podem conceder acesso granular no nível de assinatura hello e também permitir flexibilidade de Olá Olá convidado usuário de abrir solicitações de suporte.

Para essa função interna do exemplo hello **leitor** que permite aos usuários acesso tooview todos os recursos de saudação escopos mas não tooedit-los ou criar novos foi personalizada a opção de saudação de usuário tooallow Olá de abertura de solicitações de suporte.

Olá a primeira ação de exportação Olá **leitor** função necessidades toobe concluída no PowerShell é executado com permissões elevadas como administrador.

```
Login-AzureRMAccount

Get-AzureRMRoleDefinition -Name "Reader"

Get-AzureRMRoleDefinition -Name "Reader" | ConvertTo-Json | Out-File C:\rbacrole2.json

```





![Captura de tela do PowerShell para a função do RBAC de Leitor](./media/role-based-access-control-create-custom-roles-for-internal-external-users/15.png)

Você precisa tooextract modelo JSON Olá da função hello.





![Modelo JSON para a função do RBAC de Leitor personalizada](./media/role-based-access-control-create-custom-roles-for-internal-external-users/16.png)

Uma função RBAC típica é composta por três seções principais, **Actions**, **NotActions** e **AssignableScopes**.

Em Olá **ação** seção são listadas todas Olá operações permitidas para essa função. É importante toounderstand que cada ação é atribuída de um provedor de recursos. Nesse caso, para a criação de saudação de tíquetes de suporte **verificação** provedor de recursos deve ser listado.

toosee capaz de toobe todos Olá provedores de recursos disponíveis e registrados em sua assinatura, você pode usar o PowerShell.
```
Get-AzureRMResourceProvider

```
Além disso, você pode verificar Olá todos Olá disponível PowerShell cmdlets toomanage Olá provedores de recursos.
    ![Captura de tela do PowerShell para gerenciamento do provedor de recursos](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)

toorestrict todos Olá ações para uma função específica do RBAC, recurso provedores são listados na seção Olá **NotActions**.
Por último, é obrigatório para que essa função RBAC Olá contém assinatura explícita de saudação IDs onde ele é usado. Olá IDs de assinatura são listados na Olá **AssignableScopes**, caso contrário, você não poderá ser tooimport função de saudação em sua assinatura.

Depois de criar e personalizar a função RBAC hello, ele precisa toobe ambiente de saudação back importados.

```
New-AzureRMRoleDefinition -InputFile "C:\rbacrole2.json"

```

Neste exemplo, nome de saudação personalizado para essa função RBAC é "leitor suporte tíquetes nível de acesso" permitindo Olá usuário tooview tudo na assinatura hello e também tooopen solicitações de suporte.

> [!NOTE]
> Olá apenas duas funções RBAC internas, permitindo que a ação de saudação de abertura de solicitações de suporte são **proprietário** e **Colaborador**. Um toobe tooopen capaz de suporte para solicitações de usuário, ele deve receber uma função RBAC somente no escopo de assinatura de hello, porque todas as solicitações de suporte são criadas com base em uma assinatura do Azure.

Essa nova função personalizada foi atribuída a usuário tooan Olá mesmo diretório.





![captura de tela de função personalizada de RBAC importada Olá portal do Azure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/18.png)





![captura de tela da atribuição personalizado importado toouser função RBAC em Olá mesmo diretório](./media/role-based-access-control-create-custom-roles-for-internal-external-users/19.png)





![captura de tela de permissões para a função de RBAC personalizada importada](./media/role-based-access-control-create-custom-roles-for-internal-external-users/20.png)

exemplo Hello foi ainda mais detalhadas tooemphasize Olá limites dessa função RBAC personalizado da seguinte maneira:
* Pode criar novas solicitações de suporte
* Não pode criar novos escopos de recursos (por exemplo: máquina virtual)
* Não pode criar novos grupos de recursos





![captura de tela de função personalizada de RBAC criando solicitações de suporte](./media/role-based-access-control-create-custom-roles-for-internal-external-users/21.png)





![captura de tela de função RBAC personalizada não é possível toocreate VMs](./media/role-based-access-control-create-custom-roles-for-internal-external-users/22.png)





![captura de tela de função RBAC personalizada não é possível toocreate RGs novo](./media/role-based-access-control-create-custom-roles-for-internal-external-users/23.png)

## <a name="create-a-custom-rbac-role-tooopen-support-requests-using-azure-cli"></a>Criar um suporte de tooopen função RBAC personalizado solicitações usando a CLI do Azure
Em execução em um Mac e sem a necessidade de acesso tooPowerShell, CLI do Azure é Olá maneira toogo.

Olá etapas toocreate uma função personalizada são Olá iguais, com exceção de único Olá que usam a CLI função hello não pode ser baixada em um modelo JSON, mas podem ser exibidas no hello CLI.

Para este exemplo eu tiver selecionado a função interna de saudação do **Backup leitor**.

```

azure role show "backup reader" --json

```





![Captura de tela da CLI da função de leitor de backup mostrada](./media/role-based-access-control-create-custom-roles-for-internal-external-users/24.png)

Editar função hello no Visual Studio depois de copiar as propriedades de saudação em um modelo JSON, Olá **verificação** provedor de recursos foi adicionado no hello **ações** seções para que este usuário pode abrir solicitações de suporte enquanto continua toobe um leitor para o Cofre de backup hello. Novamente é ID de assinatura necessário tooadd Olá onde essa função será usada no hello **AssignableScopes** seção.

```

azure role create --inputfile <path>

```





![Captura de tela da CLI da importação da função de RBAC personalizada](./media/role-based-access-control-create-custom-roles-for-internal-external-users/25.png)

nova função de saudação agora está disponível no hello portal do Azure e o processo de atribuição de saudação é Olá mesmo como nos exemplos anteriores hello.





![Captura de tela do portal do Azure da função RBAC personalizada criada usando a CLI 1.0](./media/role-based-access-control-create-custom-roles-for-internal-external-users/26.png)

A partir de saudação 2017 de compilação mais recente, Olá Shell de nuvem do Azure está disponível. Shell de nuvem do Azure é um complemento tooIDE e hello Portal do Azure. Com esse serviço, você obtém um shell baseado em navegador que é autenticado e hospedado no Azure e pode ser usado no lugar da CLI instalada em seu computador.





![Azure Cloud Shell](./media/role-based-access-control-create-custom-roles-for-internal-external-users/27.png)
