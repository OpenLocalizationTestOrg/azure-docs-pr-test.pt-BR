---
title: "aaaAdvanced tópicos de atualização de aplicativo | Microsoft Docs"
description: "Este artigo aborda alguns tópicos avançados pertencente tooupgrading um aplicativo de malha do serviço."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: e29585ff-e96f-46f4-a07f-6682bbe63281
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar;chackdan
ms.openlocfilehash: bdaf3db6209c574d39f57e0bf9951fad5ad1cbec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade-advanced-topics"></a>Atualização do aplicativo Service Fabric: tópicos avançados
## <a name="adding-or-removing-services-during-an-application-upgrade"></a>Adicionando ou removendo serviços durante uma atualização de aplicativo
Se um novo serviço é adicionado aplicativo tooan que já está implantado e publicado como uma atualização, o novo serviço de saudação é aplicativo adicionado toohello implantado.  Essa atualização não afeta nenhum dos serviços de saudação que já fazem parte do aplicativo hello. No entanto, uma instância do serviço de saudação que foi adicionado deve ser iniciada para Olá novo serviço toobe active (usando Olá `New-ServiceFabricService` cmdlet).

Os serviços também podem ser removidos de um aplicativo como parte de uma atualização. No entanto, todas as instâncias do serviço de ser excluído Olá devem ser interrompidas antes de prosseguir com a atualização da saudação (usando Olá `Remove-ServiceFabricService` cmdlet).

## <a name="manual-upgrade-mode"></a>Modo de atualização manual
> [!NOTE]
> o modo manual não monitorado Olá deve ser considerado somente para uma atualização com falha ou suspensa. modo monitorado Olá é Olá recomendado o modo de atualização para aplicativos do Service Fabric.
>
>

Malha do serviço do Azure fornece vários modos de atualização toosupport clusters de desenvolvimento e produção. As opções de implantação escolhidas podem ser diferentes para ambientes diferentes.

atualização sem interrupção de aplicativo Hello monitorado é Olá toouse mais comuns de atualização no ambiente de produção de hello. Quando atualizar Olá política for especificada, o Service Fabric garante que o aplicativo hello esteja íntegro antes da atualização Olá continua.

 administrador do aplicativo Hello pode usar manual Olá sem interrupção aplicativo modo de atualização toohave total controle sobre o progresso da atualização por meio de Olá Olá vários domínios de atualização. Esse modo é útil quando uma política de avaliação de integridade personalizado ou complexa é necessária, ou um processo de atualização não convencional (por exemplo, aplicativo hello já está em perda de dados).

Por fim, hello automatizada atualização sem interrupção do aplicativo é útil para desenvolvimento ou tooprovide de ambientes de teste durante o desenvolvimento de serviços de ciclo de uma iteração rápida.

## <a name="change-toomanual-upgrade-mode"></a>Alterar o modo de atualização de toomanual
**Manual**-atualização do aplicativo de saudação parada no Olá atual UD e alteração Olá atualizar tooUnmonitored de modo Manual. Olá administrador precisa de chamada de toomanually **MoveNextApplicationUpgradeDomainAsync** tooproceed com hello atualizar ou disparar uma reversão, iniciando uma nova atualização. Depois que a atualização de saudação entra no modo Manual Olá, ela permanece no modo Manual Olá até que uma nova atualização é iniciada. Olá **GetApplicationUpgradeProgressAsync** comando retorna a MALHA\_aplicativo\_atualização\_estado\_sem interrupção\_FORWARD\_pendente.

## <a name="upgrade-with-a-diff-package"></a>Atualizar usando um pacote diff
Um aplicativo Malha do Serviço pode ser atualizado pelo provisionamento com um pacote de aplicativo completo e independente. Um aplicativo também pode ser atualizado usando um pacote de comparação que contém apenas arquivos de aplicativo hello atualizado, Olá atualizada manifesto de aplicativo e arquivos de manifesto de serviço hello.

Um pacote de aplicativo completo contém todos os toostart necessários arquivos de saudação e executa um aplicativo de malha do serviço. Um pacote de comparação contém apenas os arquivos de saudação alterado entre provisionar última hello e atualização atual hello, além de arquivos de manifesto do manifesto de aplicativo completo hello e serviço hello. Qualquer referência no manifesto do aplicativo hello ou manifesto de serviço que não pode ser encontrado no layout de compilação Olá é procurada no repositório de imagens de saudação.

Pacotes de aplicativo completo são necessários para a primeira instalação Olá de um cluster de toohello do aplicativo. Atualizações subsequentes podem ser um pacote de aplicativo completo ou um pacote diff.

Hipóteses em que usar um pacote diff seria uma boa opção:

* Será melhor usar um pacote diff quando você tiver um pacote de aplicativo grande que faça referência a vários arquivos de manifesto do serviço e/ou a vários pacotes de código, de configuração ou de dados.
* Um pacote de comparação é preferível quando você tiver um sistema de implantação que gera o layout de compilação Olá diretamente de seu processo de compilação do aplicativo. Nesse caso, mesmo que o código de saudação não for alterado, assemblies recém-criado obtém uma soma de verificação diferente. Usar um pacote de aplicativo completo exigiria que você tooupdate Olá versão de todos os pacotes de código. Usando um pacote de comparação, você fornece somente arquivos de Olá que foram alteradas e arquivos de manifesto Olá em que a versão de saudação foi alterada.

Quando um aplicativo é atualizado usando o Visual Studio, o pacote de comparação de saudação é publicado automaticamente. toocreate um pacote de comparação Olá manualmente, o manifesto de aplicativo e Olá manifestos do serviço devem ser atualizados, mas Olá alterado apenas os pacotes devem ser incluídos no pacote de aplicativo final hello.

Por exemplo, vamos começar com hello (números de versão fornecidos para facilitar a compreensão) do aplicativo a seguir:

```text
app1           1.0.0
  service1     1.0.0
    code       1.0.0
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

Agora, vamos supor que você desejava tooupdate somente Olá pacote de códigos de service1 usando um pacote de comparação usando o PowerShell. Agora, seu aplicativo atualizado tem Olá estrutura de pasta a seguir:

```text
app1           2.0.0      <-- new version
  service1     2.0.0      <-- new version
    code       2.0.0      <-- new version
    config     1.0.0
  service2     1.0.0
    code       1.0.0
    config     1.0.0
```

Nesse caso, você atualizar too2.0.0 de manifesto de aplicativo hello e Olá manifesto de serviço para atualização de pacote de código do service1 tooreflect hello. pasta de saudação para seu pacote de aplicativo teria Olá estrutura a seguir:

```text
app1/
  service1/
    code/
```

## <a name="next-steps"></a>Próximas etapas
[Atualização do aplicativo usando o Visual Studio](service-fabric-application-upgrade-tutorial.md) orienta você durante a atualização de aplicativo usando o Visual Studio.

[Atualização do aplicativo usando o PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) orienta você uma atualização de aplicativo usando o PowerShell.

Controle como seu aplicativo é atualizado usando [Parâmetros de Atualização](service-fabric-application-upgrade-parameters.md).

Verifique suas atualizações de aplicativo compatível aprendendo como toouse [serialização de dados](service-fabric-application-upgrade-data-serialization.md).

Corrigir problemas comuns em atualizações de aplicativo consultando etapas toohello [de solução de problemas de atualizações de aplicativo](service-fabric-application-upgrade-troubleshooting.md).
