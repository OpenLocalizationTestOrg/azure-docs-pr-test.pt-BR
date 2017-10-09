---
title: "aaaConfigure proteger Azure Service Fabric conexões de cluster | Microsoft Docs"
description: "Saiba como toouse Visual Studio tooconfigure proteger conexões que são suportadas pelo cluster do Azure Service Fabric hello."
services: service-fabric
documentationcenter: na
author: cawaMS
manager: paulyuk
editor: tglee
ms.assetid: 80501867-dd7a-4648-8bd6-d4f26b68402d
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/04/2017
ms.author: cawa
ms.openlocfilehash: ed3e5043264cf026f74e24ca09b40ccc70086cf2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-connections-tooa-service-fabric-cluster-from-visual-studio"></a>Configurar conexões seguras tooa malha do serviço cluster do Visual Studio
Saiba como toouse Visual Studio toosecurely acessar um cluster do Azure Service Fabric com as políticas de controle de acesso configuradas.

## <a name="cluster-connection-types"></a>Tipos de conexão do cluster
Dois tipos de conexões são suportados pelo cluster do Azure Service Fabric Olá: **não seguro** conexões e **x509 baseada em certificado** conexões seguras. (Para clusters do Service Fabric hospedados localmente, também há suporte para autenticações do **Windows** e **dSTS**.) Você tem o tipo de conexão de cluster tooconfigure Olá quando cluster hello está sendo criado. Depois que ele é criado, o tipo de conexão de saudação não pode ser alterado.

ferramentas do Visual Studio Service Fabric Olá oferecem suporte a todos os tipos de autenticação para conexão cluster tooa para publicação. Consulte [Configurando um cluster do Service Fabric do portal do Azure de saudação](service-fabric-cluster-creation-via-portal.md) para obter instruções sobre como tooset um cluster do Service Fabric segura.

## <a name="configure-cluster-connections-in-publish-profiles"></a>Configurar conexões do cluster em perfis de publicação
Se você publicar um projeto de serviço de malha do Visual Studio, use Olá **publicar aplicativo do Service Fabric** toochoose caixa de diálogo um cluster do Azure Service Fabric. Em **Ponto de extremidade de conexão**, selecione um cluster existente em sua assinatura.

![Olá * * caixa de diálogo Publicar serviço Fabric Application * * é usado tooconfigure uma conexão do Service Fabric.][publishdialog]

Olá **publicar aplicativo do Service Fabric** caixa de diálogo valida automaticamente a conexão de cluster hello. Se solicitado, entre em tooyour conta do Azure. Se a validação é bem-sucedida, isso significa que o sistema tenha Olá correto certificados instalados tooconnect toohello cluster com segurança, ou o cluster é não segura. Falhas de validação podem ser causadas por problemas de rede ou por não ter o cluster do sistema configurado corretamente tooconnect tooa segura.

![Olá * * publicar serviço Fabric Application * * caixa de diálogo valida um existente, configurado corretamente conexão de cluster do Service Fabric.][selectsfcluster]

### <a name="tooconnect-tooa-secure-cluster"></a>tooconnect tooa segura cluster
1. Verifique se que você pode acessar um dos certificados de cliente Olá Olá relações de confiança de cluster de destino. certificado de saudação normalmente é compartilhado como um arquivo de troca de informações pessoais (. pfx). Consulte [Configurando um cluster do Service Fabric do portal do Azure de saudação](service-fabric-cluster-creation-via-portal.md) para como tooconfigure Olá server toogrant acessar tooa cliente.
2. Instale o certificado confiável de saudação. toodo isso, clique duas vezes no arquivo. pfx de saudação ou usar Olá PowerShell script Import-PfxCertificate tooimport Olá certificados. Instalar o certificado de saudação muito**Cert: \localmachine\my.**. É tooaccept Okey todas as configurações padrão ao importar o certificado de saudação.
3. Escolha Olá **publicar...**  comando no menu de atalho de saudação de saudação do hello projeto tooopen **publicar aplicativo do Azure** caixa de diálogo e o cluster de destino, em seguida, selecione hello. ferramenta Olá resolve conexão hello e salva perfil de conexão segura de saudação parâmetros em Olá publicar automaticamente.
4. Opcional: Você pode editar Olá publicar perfil toospecify uma conexão segura de cluster.
   
   Como editar manualmente informações de certificado do hello XML do perfil publicar arquivo toospecify Olá, ser se nome do repositório toonote Olá certificado, armazenar local e a impressão digital do certificado. Você precisará tooprovide esses valores para o repositório do certificado Olá nome e local do repositório. Consulte [como: recuperar Olá impressão digital de um certificado](https://msdn.microsoft.com/library/ms734695\(v=vs.110\).aspx) para obter mais informações.
   
   Você pode usar o hello *ClusterConnectionParameters* parâmetros toospecify Olá PowerShell parâmetros toouse ao conectar-se o cluster do Service Fabric toohello. Os parâmetros válidos são os que são aceitos pelo cmdlet do Connect-ServiceFabricCluster hello. Confira [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx) para obter uma lista dos parâmetros disponíveis.
   
   Se você estiver publicando um cluster remoto tooa, você precisa parâmetros apropriados do toospecify Olá para cluster específico. a seguir Olá é um exemplo de cluster de não seguro de tooa conexão:
   
   `<ClusterConnectionParameters ConnectionEndpoint="mycluster.westus.cloudapp.azure.com:19000" />`
   
   Aqui está um exemplo de conexão tooan x509 baseada em certificado seguro cluster:
   
   ```xml
   <ClusterConnectionParameters
   ConnectionEndpoint="mycluster.westus.cloudapp.azure.com:19000"
   X509Credential="true"
   ServerCertThumbprint="0123456789012345678901234567890123456789"
   FindType="FindByThumbprint"
   FindValue="9876543210987654321098765432109876543210"
   StoreLocation="CurrentUser"
   StoreName="My" />
   ```
5. Editar outras configurações necessárias, como parâmetros de atualização e o local do arquivo de parâmetro de aplicativo e, em seguida, publicar seu aplicativo do hello **publicar aplicativo do Service Fabric** caixa de diálogo no Visual Studio.

## <a name="next-steps"></a>Próximas etapas
Para saber mais sobre como acessar os clusters do Service Fabric, confira [Visualizando o cluster usando o Explorador do Service Fabric](service-fabric-visualizing-your-cluster.md).

<!--Image references-->
[publishdialog]:./media/service-fabric-visualstudio-configure-secure-connections/publishdialog.png
[selectsfcluster]:./media/service-fabric-visualstudio-configure-secure-connections/selectsfcluster.png
