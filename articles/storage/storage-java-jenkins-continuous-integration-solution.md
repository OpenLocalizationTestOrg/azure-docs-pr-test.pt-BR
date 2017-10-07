---
title: "aaaUsing armazenamento do Azure com uma solução de integração contínua Jenkins | Microsoft Docs"
description: "Este tutorial mostra como toouse hello Azure serviço de blob como um repositório para criar artefatos criados por uma solução de integração contínua Jenkins."
services: storage
documentationcenter: java
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: f4e5ca75-f6cb-4f74-981b-2aa06bb8de45
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 02/28/2017
ms.author: seguler
ms.openlocfilehash: a8a8c6f3b03cf61d7ad98f0b38e9421dd0b47bfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-storage-with-a-jenkins-continuous-integration-solution"></a>Usando o Armazenamento do Azure com uma solução de Integração Contínua Jenkins
## <a name="overview"></a>Visão geral
Olá informações a seguir mostram como o armazenamento de Blob toouse como um repositório de artefatos de compilação criado por uma solução Jenkins CI (integração contínua) ou como uma fonte de arquivos para download toobe usados em um processo de compilação. Um dos cenários de saudação em que isso poderia ser útil é quando você estar codificando em um ambiente de desenvolvimento ágil (usando Java ou outras linguagens), compilações são executados com base em integração contínua e você precisa de um repositório para seus artefatos de compilação, para que você poderia , por exemplo, compartilhá-los com outros membros da organização, os clientes, ou mantenha um arquivamento. Outro cenário é quando o seu próprio trabalho de compilação requer outros arquivos, por exemplo, toodownload de dependências, como parte da saudação entrada de construção.

Neste tutorial você usará Olá plug-in do armazenamento do Azure para o IC Jenkins disponibilizados pela Microsoft.

## <a name="overview-of-jenkins"></a>Visão geral da Jenkins
Habilita a integração contínua Jenkins de um projeto de software, permitindo que os desenvolvedores tooeasily integrar as alterações de código e ter cria gerado automaticamente e com frequência, aumentando a produtividade Olá de desenvolvedores de saudação. Compilações têm controle de versão e artefatos de compilação podem ser carregado toovarious repositórios. Este tópico mostra como toouse Azure armazenamento de blob como repositório de saudação de artefatos de compilação de saudação. Mostra também como o armazenamento de blob dependências toodownload do Azure.

Mais informações sobre a Jenkins pode ser encontrada em [Conheça a Jenkins](https://wiki.jenkins-ci.org/display/JENKINS/Meet+Jenkins).

## <a name="benefits-of-using-hello-blob-service"></a>Benefícios do uso do serviço Blob Olá
Benefícios do uso de toohost de serviço Blob Olá seus artefatos de compilação de desenvolvimento ágil incluem:

* Alta disponibilidade de seus artefatos de compilação e/ou dependências baixáveis.
* Desempenho quando sua solução de CI Jenkins carrega seus artefatos de compilação.
* Desempenho quando seus clientes e parceiros baixam seus artefatos de compilação.
* O controle sobre as políticas de acesso do usuário, com uma opção entre acesso anônimo, acesso compartilhado com base em expiração, acesso de assinatura, acesso particular, etc.

## <a name="prerequisites"></a>Pré-requisitos
Você será necessário Olá seguintes toouse Olá serviço Blob com sua solução CI Jenkins:

* Uma solução de Integração Contínua Jenkins.
  
    Se você atualmente não tem uma solução CI Jenkins, você pode executar uma solução CI Jenkins usando Olá técnica a seguir:
  
  1. Em um computador habilitado para Java, baixe jenkins.war em <http://jenkins-ci.org>.
  2. No prompt de comando é aberto toohello pasta que contém jenkins.war, execute:
     
      `java -jar jenkins.war`

  3. No seu navegador, abra `http://localhost:8080/`. Isso abrirá o painel de Jenkins hello, que você irá usar tooinstall e configurar o plug-in do armazenamento do Azure hello.
     
      Enquanto uma solução típica de CI Jenkins será configurada toorun como um serviço, executar o war de Jenkins Olá na linha de comando Olá será suficiente para este tutorial.
* Uma conta do Azure. Você pode criar uma conta do Azure em <http://www.azure.com>.
* Uma conta de armazenamento do Azure. Se você ainda não tiver uma conta de armazenamento, você pode criar um usando as etapas de saudação em [criar uma conta de armazenamento](storage-create-storage-account.md#create-a-storage-account).
* Familiaridade com a solução de CI Jenkins Olá é recomendável, mas não é necessário, como hello conteúdo a seguir usará um tooshow exemplo básico Olá etapas necessárias ao usar o serviço de Blob hello como um repositório para o IC Jenkins compilar artefatos.

## <a name="how-toouse-hello-blob-service-with-jenkins-ci"></a>Como toouse Olá serviço Blob com Jenkins CI
serviço de Blob toouse Olá com Jenkins, você precisará tooinstall Olá plug-in do armazenamento do Azure, configurar Olá plug-in toouse sua conta de armazenamento e, em seguida, crie uma ação de pós-compilação que carrega sua conta de armazenamento de tooyour de artefatos de compilação. Essas etapas são descritas nas seções a seguir de saudação.

## <a name="how-tooinstall-hello-azure-storage-plugin"></a>Como tooinstall Olá plug-in do armazenamento do Azure
1. No painel do Jenkins hello, clique em **Jenkins gerenciar**.
2. Em Olá **Jenkins gerenciar** , clique em **gerenciar plug-ins**.
3. Clique em Olá **disponível** guia.
4. Em Olá **artefato Uploaders** seção, verifique **plug-in de armazenamento do Microsoft Azure**.
5. Clique em **Instalar sem reinicialização** ou **Baixar agora e instalar após a reinicialização**.
6. Reinicie o Jenkins.

## <a name="how-tooconfigure-hello-azure-storage-plugin-toouse-your-storage-account"></a>Como tooconfigure Olá toouse de plug-in do armazenamento do Azure sua conta de armazenamento
1. No painel do Jenkins hello, clique em **Jenkins gerenciar**.
2. Em Olá **Jenkins gerenciar** , clique em **Configurar sistema**.
3. Em Olá **configuração de conta de armazenamento do Microsoft Azure** seção:
   1. Insira seu nome de conta de armazenamento, você pode obter de saudação [Portal do Azure](https://portal.azure.com).
   2. Insira a chave de conta de armazenamento, também alcançável de saudação [Portal do Azure](https://portal.azure.com).
   3. Usar o valor padrão Olá **URL de ponto de extremidade de serviço Blob** se você estiver usando a nuvem do Azure públicos de saudação. Se você estiver usando uma nuvem do Azure diferente, use o ponto de extremidade de hello como especificado no hello [Portal do Azure](https://portal.azure.com) para sua conta de armazenamento. 
   4. Clique em **validar as credenciais de armazenamento** toovalidate sua conta de armazenamento. 
   5. [Opcional] Se você tiver contas de armazenamento adicional que você deseja tooyour feita disponível Jenkins CI, clique em **adicionar mais contas de armazenamento**.
   6. Clique em **salvar** toosave suas configurações.

## <a name="how-toocreate-a-post-build-action-that-uploads-your-build-artifacts-tooyour-storage-account"></a>Como toocreate uma ação de pós-compilação que carrega sua conta de armazenamento de tooyour de artefatos de compilação
Para fins de instrução, primeiro vamos precisar toocreate um trabalho que criará vários arquivos e, em seguida, adicionar conta de armazenamento Olá ação pós-compilação tooupload Olá arquivos tooyour.

1. No painel do Jenkins hello, clique em **Novo Item**.
2. Nome do trabalho Olá **MyJob**, clique em **compilar um projeto de software livre de estilo**e, em seguida, clique em **Okey**.
3. Em Olá **criar** seção de configuração de trabalho hello, clique em **adicionar a etapa de compilação** e escolha **Windows executar comando de lote**.
4. Em **comando**, use Olá comandos a seguir:

    ```   
    md text
    cd text
    echo Hello Azure Storage from Jenkins > hello.txt
    date /t > date.txt
    time /t >> date.txt
    ```

5. Em Olá **ações de pós-compilação** seção de configuração de trabalho hello, clique em **Adicionar ação de pós-compilação** e escolha **carregar o armazenamento de Blob artefatos tooAzure**.
6. Para **nome da conta de armazenamento**, selecione Olá toouse da conta de armazenamento.
7. Para **nome do contêiner**, especifique o nome do contêiner de saudação. (Olá contêiner será criado se ele ainda não existir quando são carregados artefatos de compilação hello.) Você pode usar variáveis de ambiente, então para este exemplo, digite **${JOB_NAME}** como nome do contêiner de saudação.
   
    **Dica**
   
    Abaixo Olá **comando** seção em que você inseriu um script para **Windows executar comando de lote** é um link de variáveis de ambiente toohello reconhecidas pelo Jenkins. Clique em que se vinculam a nomes de variável de ambiente toolearn hello e descrições. Observe que o ambiente de variáveis que contêm caracteres especiais, como Olá **BUILD_URL** variável de ambiente, não são permitidos como um nome de contêiner ou o caminho virtual comum.
8. Clique em **Tornar o novo contêiner público por padrão** para este exemplo. (Se você quiser toouse um contêiner privado, você precisará toocreate um acesso de tooallow de assinatura de acesso compartilhado. Que está além do escopo deste tópico hello. Você pode saber mais sobre assinaturas de acesso compartilhado em [Uso de SAS (Assinaturas de Acesso Compartilhado)](storage-dotnet-shared-access-signature-part-1.md).
9. [Opcional] Clique em **contêiner limpa antes de carregar** se você quiser Olá contêiner toobe apagados do conteúdo para artefatos de compilação são carregados (deixá-la desmarcada se você não quiser tooclean conteúdo de saudação do contêiner de saudação).
10. Para **tooupload de lista de artefatos**, digite  **texto /*. txt**.
11. Em **Caminho virtual comum para artefatos carregados**, para as finalidades deste tutorial, insira **${BUILD\_ID}/${BUILD\_NUMBER}**.
12. Clique em **salvar** toosave suas configurações.
13. No painel de Jenkins hello, clique em **criar agora** toorun **MyJob**. Examine a saída de console de saudação status. Mensagens de status para o armazenamento do Azure serão incluídas na saída do console Olá início da ação de pós-compilação Olá artefatos de compilação tooupload.
14. Após a conclusão bem-sucedida do trabalho hello, você pode examinar artefatos de compilação Olá abrindo blob público hello.
    1. Logon toohello [Portal do Azure](https://portal.azure.com).
    2. Clique em **Armazenamento**.
    3. Clique no nome de conta de armazenamento Olá que você usou para Jenkins.
    4. Clique em **Contêineres**.
    5. Clique em contêiner Olá denominado **myjob**, Olá a versão em minúsculas do nome do trabalho Olá que você atribuiu ao criar trabalho de Jenkins hello. Os nomes de contêineres e de blob são escritos em letra minúscula (e diferenciam maiúsculas de minúsculas) no armazenamento do Azure. Na lista de saudação de blobs para contêiner Olá denominado **myjob** , você verá **hello.txt** e **date.txt**. Copiar URL de saudação para qualquer um desses itens e abri-lo no seu navegador. Você verá o arquivo de texto de saudação que foi carregado como um artefato de compilação.

Somente uma ação de pós-compilação que carrega o armazenamento de blob tooAzure artefatos pode ser criada por trabalho. Observe que o armazenamento de blob Olá única ação de pós-compilação tooupload artefatos tooAzure pode especificar diferentes arquivos (incluindo caracteres curinga) e caminhos toofiles em **tooupload de lista de artefatos** usando um ponto e vírgula como separador. Por exemplo, se seu Jenkins compilar produz arquivos JAR e arquivos TXT no seu espaço de trabalho **criar** pasta e você deseja tooupload tanto tooAzure de armazenamento de blob, use o seguinte de saudação para Olá **tooupload de lista de artefatos** valor: **criar /\*. jar; compilação /\*. txt**. Você também pode usar a sintaxe de dois-pontos duplo toospecify toouse um caminho em nome do blob hello. Por exemplo, se você quiser Olá JARs tooget carregado usando **binários** no caminho de blob hello e Olá TXT arquivos tooget carregados usando **avisos** no caminho de blob Olá, use o seguinte de Olá para Olá  **Lista de tooupload artefatos** valor: **criar /\*. jar::binaries; compilação /\*. txt::notices**.

## <a name="how-toocreate-a-build-step-that-downloads-from-azure-blob-storage"></a>Como uma etapa de compilação de toocreate downloads do armazenamento de BLOBs do Azure
Olá, as etapas a seguir mostra como tooconfigure uma compilação etapa itens toodownload do armazenamento de BLOBs do Azure. Isso pode ser útil se você quiser tooinclude itens na criação, por exemplo, JARs manter no Azure armazenamento de blob.

1. Em Olá **criar** seção de configuração de trabalho hello, clique em **adicionar a etapa de compilação** e escolha **Download do armazenamento de BLOBs do Azure**.
2. Para **nome da conta de armazenamento**, selecione Olá toouse da conta de armazenamento.
3. Para **nome do contêiner**, especificar nome de saudação do contêiner de saudação que tem blobs Olá deseja toodownload. É possível usar variáveis de ambiente.
4. Para **nome do Blob**, especifique o nome do blob hello. É possível usar variáveis de ambiente. Além disso, você pode usar um asterisco como um caractere curinga depois que você especificar letras de saudação inicial do nome do blob hello. Por exemplo, **project\*** deve especificar todos os blobs cujos nomes começam com **project**.
5. [Opcional] Para **caminho de Download**, especifique o caminho de saudação na máquina de Jenkins Olá onde deseja toodownload arquivos do armazenamento de BLOBs do Azure. Também é possível usar variáveis de ambiente. (Se você não fornecer um valor para **caminho de Download**, arquivos de saudação do armazenamento de BLOBs do Azure será o espaço de trabalho do trabalho toohello baixado.)

Se você tiver itens adicionais que você deseja toodownload do armazenamento de BLOBs do Azure, você pode criar etapas de compilação adicionais.

Depois de executar uma compilação, você pode verificar Olá compilar saída do console de histórico ou examinar seu local de download, toosee se Olá blobs esperado foram baixados com êxito.  

## <a name="components-used-by-hello-blob-service"></a>Componentes usados pelo serviço Blob da saudação
a seguir Olá fornece uma visão geral dos componentes de serviço Blob hello.

* **Conta de armazenamento**: todos os acessos tooAzure armazenamento é feito por meio de uma conta de armazenamento. Este é o nível mais alto de saudação do namespace Olá para acessar blobs. Uma conta pode conter um número ilimitado de contêineres, desde que seu tamanho total esteja abaixo de 100 TB.
* **Contêiner**: o contêiner fornece um agrupamento de conjunto de blobs. Todos os blobs devem ter um contêiner. Uma conta pode conter um número ilimitado de contêineres. Um contêiner pode armazenar um número ilimitado de blobs.
* **Blob**: um arquivo de qualquer tipo e tamanho. Existem dois tipos de blobs que podem ser armazenados no Armazenamento do Azure: blobs de blocos e de páginas. A maioria dos arquivos são blobs de bloco. Um blob de bloco único pode ser o too200GB em tamanho. Este tutorial usa blobs de bloco. Blobs de página, outro tipo de blob, podem ser o too1TB no tamanho e são mais eficiente quando os intervalos de bytes em um arquivo são alterados com frequência. Para obter mais informações sobre os blobs, consulte [Compreendendo os Blobs de Bloco, Blobs de Anexo e Blobs de Página](http://msdn.microsoft.com/library/azure/ee691964.aspx).
* **Formato de URL**: Blobs são endereçados através de Olá formato de URL a seguir:
  
    `http://storageaccount.blob.core.windows.net/container_name/blob_name`
  
    (formato de saudação acima se aplica toohello nuvem pública do Azure. Se você estiver usando uma nuvem do Azure diferente, use pontos de extremidade Olá Olá [Portal do Azure](https://portal.azure.com) toodetermine seu ponto de extremidade de URL.)
  
    No formato de saudação acima, `storageaccount` representa Olá nome da sua conta de armazenamento, `container_name` representa Olá nome do seu contêiner e `blob_name` representa Olá nome de seu blob, respectivamente. Em nome do contêiner de saudação, você pode ter vários caminhos, separados por uma barra invertida,  **/** . nome do contêiner de exemplo Hello neste tutorial foi **MyJob**, e **${COMPILAR\_ID} / ${BUILD\_número}** foi usado para comuns caminho virtual hello, resultando em Olá blob tem um URL da saudação formulário a seguir:
  
    `http://example.blob.core.windows.net/myjob/2014-04-14_23-57-00/1/hello.txt`

## <a name="next-steps"></a>Próximas etapas
* [Conheça Jenkins](https://wiki.jenkins-ci.org/display/JENKINS/Meet+Jenkins)
* [SDK de Armazenamento do Azure para Java](https://github.com/azure/azure-storage-java)
* [Referência de SDK do Cliente de Armazenamento do Azure](http://dl.windowsazure.com/storage/javadoc/)
* [API REST de serviços de armazenamento do Azure](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Blog da equipe de Armazenamento do Azure](http://blogs.msdn.com/b/windowsazurestorage/)

Para obter mais informações, consulte também Olá [Central de desenvolvedores de Java](https://azure.microsoft.com/develop/java/).
