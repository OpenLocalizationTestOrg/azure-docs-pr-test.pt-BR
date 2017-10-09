>[!NOTE]
> Deixe comentários nesta página sobre mensagens de erro ou nos [comentários do Azure](https://feedback.azure.com/forums/216843-virtual-machines) com o rótulo #azerrormessage.

## <a name="error-response-format"></a>Formato da resposta de erro 
Máquinas virtuais do Azure usam Olá formato JSON para resposta de erro a seguir:

```json
{
  "status": "status code",
  "error": {
    "code":"Top level error code",
    "message":"Top level error message",
    "details":[
     {
      "code":"Inner evel error code",
      "message":"Inner level error message"
     }
    ]
   }
}
```

Uma resposta de erro sempre inclui um código de status e um objeto de erro. Cada objeto de erro sempre contém um código de erro e uma mensagem. Se hello VM é criada com um modelo de objeto de erro Olá também contém uma seção de detalhes que contém um nível interno de códigos de erro e a mensagem. Normalmente, hello mais nível interno de mensagem de erro é Olá raiz falha.


## <a name="common-virtual-machine-management-errors"></a>Erros comuns de gerenciamento da máquina virtual

Esta seção lista as mensagens de erro comuns Olá que você pode encontrar ao gerenciar máquinas virtuais:

|  Código do Erro  |  Mensagem de erro  |  
|  :------| :-------------|  
|  AcquireDiskLeaseFailed  |  Falha na tooacquire concessão ao criar o disco '{0}' usando blob com URI \\{1 \\}. O blob já está em utilização.  |  
|  AllocationFailed  |  Falha na alocação. Tente reduzir o tamanho da VM hello ou número de VMs, tente novamente mais tarde ou tente implantar tooa conjunto de disponibilidade diferente ou em outro local do Azure.  |  
|  AllocationFailed  |  Olá alocação de VM falhou devido a erro interno tooan. Verifique novamente mais tarde ou tente implantar tooa outro local.  |
|  ArtifactNotFound  |  Olá extensão VM com publicador '{0}' e tipo '\\{1 \\}' não pôde ser encontrado no local '2}'.  |
|  ArtifactNotFound  |  Tipo de extensão com editor '{0}', '\\{1 \\}' e versão do manipulador de tipo '2}' não foi encontrado no repositório de extensão hello.  |
|  ArtifactVersionNotFound  |  Nenhuma versão encontrada no repositório de artefato de saudação que satisfaça Olá solicitou versão '{0}'.  |
|  ArtifactVersionNotFound  |  Nenhuma versão encontrada no repositório de artefato de saudação que satisfaça Olá solicitado versão '{0}' para a extensão VM com publicador '\\{1 \\}' e tipo '2}'.  |
|  AttachDiskWhileBeingDetached  |  Não é possível anexar o disco '{0}' de dados tooVM '\\{1 \\}' porque o disco hello está sendo desanexado. Aguarde até que a saudação disco ser desanexado completamente e tente novamente.  |
|  BadRequest  |  Os Conjuntos de disponibilidade alinhados ainda não têm suporte nesta região.  |
|  BadRequest  |  Adição de uma VM com discos gerenciados conjunto de disponibilidade ou adição de uma VM com o blob com base em discos toomanaged conjunto de disponibilidade toonon gerenciado não tem suporte. Crie um conjunto de disponibilidade com a propriedade 'gerenciado' definida em ordem tooadd uma VM com discos gerenciado tooit.  |
|  BadRequest  |  Não há suporte para Managed Disks nesta região.  |
|  BadRequest  |  Não há suporte para vários VMExtensions por manipulador para o tipo de SO "{0}". A VMExtension "{1}" com o manipulador "{2}" já foi adicionada ou especificada na entrada.  |
|  BadRequest  |  Não há suporte para a operação "{0}" no recurso "{1}" com discos gerenciados.  |
|  CertificateImproperlyFormatted  |  representação de JSON do segredo recuperada de {0} Hello tem um campo de dados que não é um arquivo PFX formatado corretamente ou senha Olá fornecida não decodifica o arquivo PFX de saudação corretamente.  |
|  CertificateImproperlyFormatted  |  dados Olá recuperados do {0} não são desserializáveis em JSON.  |
|  Conflito  |  O redimensionamento de disco é permitido somente quando criar uma VM ou Olá VM é desalocada.  |
|  ConflictingUserInput  |  Disco '{0}' não pode ser anexado como disco Olá já pertence a VM '\\{1 \\}'.  |
|  ConflictingUserInput  |  Grupos de recursos de origem e destino são Olá mesmo.  |
|  ConflictingUserInput  |  As contas de armazenamento de origem e de destino do disco {0} são diferentes.  |
|  ContainerAlreadyOnLease  |  Já existe uma concessão no contêiner de armazenamento Olá mantendo blob Olá com URI {0}.  |
|  CrossSubscriptionMoveWithKeyVaultResources  |  solicitação de recursos de movimentação Olá contém recursos KeyVault que são referenciados por uma ou mais {0} s na solicitação de saudação. Não há suporte para isso no momento na Movimentação entre assinaturas. Verifique os detalhes de erro de saudação para Olá Ids de recurso KeyVault.  |
|  DiagnosticsOperationInternalError  |  Ocorreu um erro interno ao processar o perfil de diagnóstico da VM {0}.  |
|  DiskBlobAlreadyInUseByAnotherDisk  |  Blob {0} já está em uso por outro disco pertencente tooVM '\\{1 \\}'. Você pode examinar os metadados de blob Olá Olá disco informações de referência.  |
|  DiskBlobNotFound  |  Não é possível toofind VHD blob com URI {0} para o disco '\\{1 \\}'.  |
|  DiskBlobNotFound  |  Não é possível toofind VHD blob com URI {0}.  |
|  DiskEncryptionKeySecretMissingTags  |  segredo de {0} não tem marcas de \\{1 \\} hello. Atualizar a versão do segredo hello, adicionar marcas de saudação necessária e tente novamente.  |
|  DiskEncryptionKeySecretUnwrapFailed  |  A abertura do valor {0} secreto utilizando a chave {1} falhou.  |
|  DiskImageNotReady  |  A imagem do disco {0} está no estado de {1}. Tente novamente quando a imagem estiver pronta.  |
|  DiskPreparationError  |  Um ou mais erros ocorreram ao preparar discos de VM. Consulte a exibição de instância de disco para obter detalhes.  |
|  DiskProcessingError  |  Processamento de disco interrompido como Olá VM tem outros discos em discos com falha.  |
|  ImageBlobNotFound  |  Não é possível toofind VHD blob com URI {0} para o disco '\\{1 \\}'.  |
|  ImageBlobNotFound  |  Não é possível toofind VHD blob com URI {0}.  |
|  IncorrectDiskBlobType  |  Blobs de disco só podem ser do tipo blob de páginas. Blob {0} para o disco "{1}" é do tipo blob de blocos.  |
|  IncorrectDiskBlobType  |  Blobs de disco só podem ser do tipo blob de páginas. Blob {0} é do tipo "{1}".  |
|  IncorrectImageBlobType  |  Blobs de disco só podem ser do tipo blob de páginas. Blob {0} para o disco "{1}" é do tipo blob de blocos.  |
|  IncorrectImageBlobType  |  Blobs de disco só podem ser do tipo blob de páginas. Blob {0} é do tipo "{1}".  |
|  InternalOperationError  |  Não foi possível resolver a conta de armazenamento {0}. Verifique se ele foi criado por meio do provedor de recursos de armazenamento de saudação Olá mesmo local como saudação de recursos de computação.  |
|  InternalOperationError  |  Falha nas tarefas para atingir a meta {0}.  |
|  InternalOperationError  |  Erro ao validar o perfil de rede de saudação da VM '{0}'.  |
|  InvalidAccountType  |  Olá AccountType {0} é inválido.  |
|  InvalidParameter  |  valor de saudação do parâmetro {0} é inválido.  |
|  InvalidParameter  |  senha do administrador Olá especificada não é permitida.  |
|  InvalidParameter  |  "senha Olá fornecido deve estar entre {0}-\ {1 \} caracteres e deve satisfazer a pelo menos 2} de requisitos de complexidade de senha do seguinte hello: <ol><li> Contém um caractere maiúsculo</li><li>Contém um caractere minúsculo</li><li>Contém um dígito numérico</li><li>Contém um caractere especial.</li></ol>  |
|  InvalidParameter  |  Olá administrador de nome de usuário especificado não é permitido.  |
|  InvalidParameter  |  Não é possível anexar um disco do sistema operacional existente se hello VM é criada de uma imagem de plataforma ou de usuário.  |
|  InvalidParameter  |  O nome de contêiner {0} é inválido. Os nomes de contêiner devem ter de três a 63 caracteres e conter somente caracteres alfanuméricos minúsculos e hífen. O hífen deve ser precedido e seguido por um caractere alfanumérico.  |
|  InvalidParameter  |  O nome de contêiner {0} na URL {1} é inválido. Os nomes de contêiner devem ter de três a 63 caracteres e conter somente caracteres alfanuméricos minúsculos e hífen. O hífen deve ser precedido e seguido por um caractere alfanumérico.  |
|  InvalidParameter  |  nome do blob Olá na URL {0} contém uma barra. Atualmente, não há suporte para isso em discos.  |
|  InvalidParameter  |  Olá URI {0} não parecer toobe URI de blob correto.  |
|  InvalidParameter  |  Um disco chamado '{0}' já usa Olá mesmo LUN: \\{1 \\}.  |
|  InvalidParameter  |  Já existe um disco chamado "{0}".  |
|  InvalidParameter  |  Não é possível especificar substituições de imagem de usuário para um disco já definido no hello especificado a imagem de referência.  |
|  InvalidParameter  |  Um disco chamado '{0}' já usa Olá a mesma URL do VHD \\{1 \\}.  |
|  InvalidParameter  |  Hello {0} de contagem de domínio falha especificado deve estar no intervalo de saudação {1} too\ {2 \}.  |
|  InvalidParameter  |  tipo de licença Hello {0} é inválido. Os tipos de licenças válidos são: Windows_Client ou Windows_Server, sensíveis às maiúsculas e minúsculas.  |
|  InvalidParameter  |  Nome de host do Linux não pode exceder {0} caracteres nem conter Olá seguintes caracteres: \\{1 \\}.  |
|  InvalidParameter  |  Caminho de destino para as chaves públicas Ssh é atualmente limitada tooits padrão valor {0} devido tooa conhecido problema no agente de provisionamento do Linux.  |
|  InvalidParameter  |  Já existe um disco no LUN {0}.  |
|  InvalidParameter  |  {0} de assinatura da solicitação Olá deve corresponder Olá assinatura \\{1 \\} contida na id de disco gerenciado hello.  |
|  InvalidParameter  |  Os dados personalizados de OSProfile têm de ter uma codificação Base64 e um comprimento máximo de {0} caracteres.  |
|  InvalidParameter  |  O nome do blob do URL {0} tem de terminar com a extensão "{1}".  |
|  InvalidParameter  |  "{0}" não é um prefixo de nome de blob VHD capturado válido. Um prefixo válido deve corresponder à expressão "{1}".  |
|  InvalidParameter  |  Certificados não podem ser adicionados tooyour VM se o agente de VM Olá não está provisionado.  |
|  InvalidParameter  |  Já existe um disco no LUN {0}.  |
|  InvalidParameter  |  Não é possível toocreate Olá VM porque Olá solicitada {0} tamanho não está disponível no cluster Olá onde o conjunto de disponibilidade Olá alocado no momento. Olá os tamanhos disponíveis são: \\{1 \\}. Leia mais sobre estratégia de redimensionamento de VM em https://aka.ms/azure-resizevm.  |
|  InvalidParameter  |  Olá solicitada {0} de tamanho VM não está disponível na região atual da saudação. Olá tamanhos disponíveis na região atual da saudação são: \\{1 \\}. Saiba mais sobre os tamanhos VM disponíveis Olá em cada região no https://aka.ms/azure-regions.  |
|  InvalidParameter  |  Olá solicitada {0} de tamanho VM não está disponível na região atual da saudação. Saiba mais sobre os tamanhos VM disponíveis Olá em cada região no https://aka.ms/azure-regions.  |
|  InvalidParameter  |  Nome de usuário de administrador do Windows não pode ser mais do que {0} caracteres de comprimento, terminam com um ponto ou contenham Olá seguintes caracteres: \\{1 \\}.  |
|  InvalidParameter  |  Nome do computador Windows não pode ser mais do que {0} caracteres de comprimento, ser totalmente numérico ou contenham Olá seguintes caracteres: \\{1 \\}.  |
|  MissingMoveDependentResources  |  solicitação de recursos de movimentação de saudação não contém todos os recursos dependentes de saudação. Verifique nos detalhes do erro se há IDs de recursos que estão faltando.  |
|  MoveResourcesHaveInvalidState  |  solicitação para mover recursos Olá contém máquinas virtuais que estão associados a contas de armazenamento inválido. Verifique os detalhes dessas IDs de recurso e os nomes de conta de armazenamento referenciados.  |
|  MoveResourcesHavePendingOperations  |  Olá solicitação de recursos de movimentação contém recursos para o qual uma operação está pendente. Verifique os detalhes dessas IDs de recurso. Repita a operação depois de concluir a saudação operações pendentes.  |
|  MoveResourcesNotFound  |  Olá mover recursos solicitação contém recursos que não podem ser encontrados. Verifique os detalhes dessas IDs de recurso.  |
|  NetworkingInternalOperationError  |  Erro de alocação de rede desconhecido.  |
|  NetworkingInternalOperationError  |  Erro de alocação de rede desconhecido  |
|  NetworkingInternalOperationError  |  Ocorreu um erro interno no processamento de perfil de rede da saudação VM.  |
|  NotFound  |  Olá {0} de conjunto de disponibilidade não pode ser encontrado.  |
|  NotFound  |  Máquina Virtual de origem '{0}' especificado na solicitação de saudação não existe neste local do Azure.  |
|  NotFound  |  Locatário com ID {0} não encontrado.  |
|  NotFound  |  Olá imagem {0} não foi encontrado.  |
|  NotSupported  |  é o tipo de licença Olá {0}, mas não é \\{1 \\} blob de imagem de saudação do local.  |
|  OperationNotAllowed  |  Não é possível excluir o Conjunto de disponibilidade {0}. Antes de eliminar um Conjunto de disponibilidade, verifique se ele não contém nenhuma VM.  |
|  OperationNotAllowed  |  Alterando a disponibilidade do conjunto de SKU de 'Alinhado' too'Classic' não é permitido.  |
|  OperationNotAllowed  |  Não é possível modificar extensões na VM de saudação quando Olá VM não está em execução.  |
|  OperationNotAllowed  |  Olá ação de captura só tem suporte em uma máquina Virtual com discos de blob com base. Use Olá 'Imagem' recurso APIs toocreate uma imagem de uma máquina Virtual gerenciada.  |
|  OperationNotAllowed  |  Olá recurso {0} não é possível criar imagem \\{1 \\} até que a imagem foi criada com êxito.  |
|  OperationNotAllowed  |  Atualizações tooencryptionSettings não é permitido quando a VM for alocada tente novamente após a VM está desalocada  |
|  OperationNotAllowed  |  Não há suporte para a adição de um disco gerenciado de tooa VM com discos de blob com base.  |
|  OperationNotAllowed  |  Olá número máximo de discos de dados permitido tooa toobe anexado VMs desse tamanho é {0}.  |
|  OperationNotAllowed  |  Não há suporte para a adição de um tooVM de disco de blob com base em com discos gerenciados.  |
|  OperationNotAllowed  |  Operação '{0}' não é permitida na imagem '\\{1 \\}' desde Olá que imagem está marcada para exclusão. Você pode apenas Repita a operação de exclusão de saudação (ou aguardar um toocomplete em andamento de uma).  |
|  OperationNotAllowed  |  Operação '{0}' não é permitida na VM '\\{1 \\}' desde Olá que VM é generalizada.  |
|  OperationNotAllowed  |  Operação "{0}" não é permitida porque a coleção de Pontos de restauração "{1}" está marcada para exclusão.  |
|  OperationNotAllowed  |  A operação "{0}" não é permitida na extensão de VM "{1}" dado que está marcada para eliminação. Você pode apenas Repita a operação de exclusão de saudação (ou aguardar um toocomplete em andamento de uma).  |
|  OperationNotAllowed  |  Operação '{0}' não é permitida como máquinas virtuais Olá '\\{1 \\}' estão sendo provisionadas usando a imagem de saudação '2}'.  |
|  OperationNotAllowed  |  Operação '{0}' não é permitida porque Olá ScaleSet de máquina Virtual '\\{1 \\}' está usando atualmente Olá imagem '2}'.  |
|  OperationNotAllowed  |  Operação '{0}' não é permitida na VM '\\{1 \\}' desde Olá que VM está marcada para exclusão. Você pode apenas Repita a operação de exclusão de saudação (ou aguardar um toocomplete em andamento de uma).  |
|  OperationNotAllowed  |  Operação '{0}' não é permitida na VM '\\{1 \\}' como Olá VM é desalocada ou marcada toobe desalocada.  |
|  OperationNotAllowed  |  Operação '{0}' não é permitida na VM '\\{1 \\}' desde Olá que VM está em execução. . Desligue explicitamente caso você desligue Olá VM de dentro do sistema operacional hello.  |
|  OperationNotAllowed  |  Operação '{0}' não é permitida na VM '\\{1 \\}' desde Olá que VM não é desalocada.  |
|  OperationNotAllowed  |  Operação "{0}" não é permitida na VM "{1}" dado que a VM tem a extensão "{2}" no estado de falha.  |
|  OperationNotAllowed  |  A operação "{0}" não é permitida na VM "{1}" dado que outra operação está em curso.  |
|  OperationNotAllowed  |  operação de saudação '{0}' requer toobe '\\{1 \\}' da máquina Virtual Olá generalizado.  |
|  OperationNotAllowed  |  operação de saudação requer Olá toobe VM em execução (ou definir toorun).  |
|  OperationNotAllowed  |  Disco com tamanho de {0} GB, que é menor do que o hello {1}GB de disco correspondente na imagem de tamanho, não é permitida.  |
|  OperationNotAllowed  |  Extensões do conjunto de escala de VM do manipulador '{0}' podem ser adicionadas somente em tempo de saudação de criação de um conjunto de escala de VM.  |
|  OperationNotAllowed  |  Extensões do conjunto de escala de VM do manipulador '{0}' podem ser excluídas somente em tempo de saudação de exclusão do conjunto de escala de VM.  |
|  OperationNotAllowed  |  A VM "{0}" já está usando discos gerenciados.  |
|  OperationNotAllowed  |  VM '{0}' pertence too'Classic' '\\{1 \\}' do conjunto de disponibilidade. Atualização Olá disponibilidade defina toouse 'Alinhado' SKU e repita Olá conversão.  |
|  OperationNotAllowed  |  VM criada a partir da imagem não pode ter discos baseados em blob. Todos os discos têm discos toobe gerenciado.  |
|  OperationNotAllowed  |  Captura de operação não pode ser concluída porque o hello VM não é generalizada.  |
|  OperationNotAllowed  |  Não são permitidas operações de gerenciamento na máquina virtual '{0}' pois discos de VM estão sendo convertido toomanaged discos.  |
|  OperationNotAllowed  |  Uma operação em andamento é alterar o estado de energia de máquina Virtual {0} too\ {1 \}. Execute a operação {2} após algum tempo.  |
|  OperationNotAllowed  |  Não é possível tooadd ou atualização hello VM. Olá solicitada {0} de tamanho da VM pode não estar disponível na unidade de alocação existentes hello. Leia mais sobre estratégia de redimensionamento de VM em https://aka.ms/azure-resizevm.  |
|  OperationNotAllowed  |  Não é possível tooresize Olá VM porque Olá solicitada {0} tamanho não está disponível no cluster Olá onde o conjunto de disponibilidade Olá alocado no momento. Olá os tamanhos disponíveis são: \\{1 \\}. Leia mais sobre estratégia de redimensionamento de VM em https://aka.ms/azure-resizevm.  |
|  OperationNotAllowed  |  Não é possível tooresize Olá VM porque Olá solicitada {0} tamanho não está disponível no cluster Olá onde hello VM alocada no momento. tooresize too\ sua VM {1 \}. desalocar (Esta é a operação de parada em Olá portal do Azure) e tente a operação de redimensionamento Olá novamente. Leia mais sobre estratégia de redimensionamento de VM em https://aka.ms/azure-resizevm.  |
|  OSProvisioningClientError  |  Provisionamento de SO falhou para a máquina virtual '{0}' porque o sistema operacional convidado de saudação está atualmente sendo provisionado.  |
|  OSProvisioningClientError  |  Falha no provisionamento do SO para a VM "{0}". Detalhes do erro: \\{1 \\}, certifique-se de imagem de saudação foi adequadamente preparada (generalizada). <ul><li>Instruções para Windows: https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/  </li></ul> |
|  OSProvisioningClientError  |  Falha na geração da chave host de SSH. Detalhes do Erro: {0}. tooresolve esse problema, verifique se se o agente do Linux está configurado corretamente. <ul><li>Você pode verificar as instruções de saudação em: https://azure.microsoft.com/documentation/articles/virtual-machines-linux-agent-user-guide/ </li></ul> |
|  OSProvisioningClientError  |  Nome de usuário especificado para Olá que VM é inválida para a distribuição de Linux. Detalhes do Erro: {0}.  |
|  OSProvisioningInternalError  |  Provisionamento de SO falhou para a máquina virtual '{0}' devido a erro interno tooan.  |
|  OSProvisioningTimedOut  |  Provisionamento do sistema operacional para máquina virtual '{0}' não foi concluída no hello determinado tempo. Olá VM ainda pode concluir o provisionamento com êxito. Verifique mais tarde o estado do provisionamento.  |
|  OSProvisioningTimedOut  |  Provisionamento do sistema operacional para máquina virtual '{0}' não foi concluída no hello determinado tempo. Olá VM ainda pode concluir o provisionamento com êxito. Verifique mais tarde o estado do provisionamento. Além disso, certifique-se de imagem Olá foi adequadamente preparada (generalizada).   <ul><li>Instruções para Windows: https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/ </li><li> Instruções para Linux: https://azure.microsoft.com/documentation/articles/virtual-machines-linux-capture-image/</li></ul>  |
|  OSProvisioningTimedOut  |  Provisionamento do sistema operacional para máquina virtual '{0}' não foi concluída no hello determinado tempo. No entanto, agente de convidado da VM de saudação foi detectado em execução. Isso sugere convidado Olá SO não foi adequadamente preparada toobe usado como uma imagem de VM (com CreateOption = FromImage). tooresolve esse problema, Olá ou use VHD, sem CreateOption = anexar ou prepará-la corretamente para uso como uma imagem:   <ul><li>Instruções para Windows: https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/ </li><li> Instruções para Linux: https://azure.microsoft.com/documentation/articles/virtual-machines-linux-capture-image/</li></ul>  |
|  OverConstrainedAllocationRequest  |  Olá necessário tamanho da VM não está disponível atualmente no local de saudação selecionada.  |
|  ResourceUpdateBlockedOnPlatformUpdate  |  Recurso não pode ser atualizado no momento devido a atualização de plataforma tooongoing. Tente novamente mais tarde.  |
|  StorageAccountLimitation  |  Conta de armazenamento '{0}' não oferece suporte para blobs de página que são necessárias toocreate discos.  |
|  StorageAccountLimitation  |  A conta de armazenamento "{0}" excedeu a quota alocada.  |
|  StorageAccountLocationMismatch  |  Não foi possível resolver a conta de armazenamento {0}. Verifique se ele foi criado por meio do provedor de recursos de armazenamento de saudação Olá mesmo local como saudação de recursos de computação.  |
|  StorageAccountNotFound  |  Conta de armazenamento {0} não encontrada. Verifique se a conta de armazenamento não é excluída e pertence toohello mesmo local Olá VM do Azure.  |
|  StorageAccountNotRecognized  |  Utilize uma conta de armazenamento gerida pelo Provedor de Recursos de Armazenamento. Não há suporte para o uso de {0}.  |
|  StorageAccountOperationInternalError  |  Ocorreu um erro interno durante o acesso à conta de armazenamento {0}.  |
|  StorageAccountSubscriptionMismatch  |  Conta de armazenamento {0} não pertence a toosubscription \\{1 \\}.  |
|  StorageAccountTooBusy  |  Conta de armazenamento "{0}" está muito ocupada no momento. Considere usar outra conta.  |
|  StorageAccountTypeNotSupported  |  O disco {0} usa {1} que é uma conta de Armazenamento de Blobs. Tente novamente com uma conta de armazenamento de finalidade geral.  |
|  StorageAccountTypeNotSupported  |  A conta de armazenamento {0} é do tipo {1}. O Diagnóstico de inicialização oferece suporte a {2} tipos de conta de armazenamento.  |
|  SubscriptionNotAuthorizedForImage  |  Olá assinatura não está autorizada.  |
|  TargetDiskBlobAlreadyExists  |  O blob {0} já existe. Forneça um toocreate URI de blob diferente de um \\{'1 dados em branco disco \\} programa de implantação novo'.  |
|  TargetDiskBlobAlreadyExists  |  Captura de operação não pode continuar porque já existe uma imagem de destino blob {0} e blobs VHD Olá sinalizador toooverwrite não está definido. O excluir Olá blob ou defina o sinalizador de saudação toooverwrite blobs VHD e repita.  |
|  TargetDiskBlobAlreadyExists  |  Não é possível continuar com a operação dado que o blob de imagem de destino {0} tem uma concessão ativa.   |
|  TargetDiskBlobAlreadyExists  |  O blob {0} já existe. Forneça um URI de blob diferente como destino para o disco "{1}".  |
|  TooManyVMRedeploymentRequests  |  Foram recebidas muitas solicitações de reimplantação da VM '{0}' ou VMs Olá no hello excessivo mesmo com essa VM. Tente novamente mais tarde.  |
|  VHDSizeInvalid  |  Olá especificado valor de tamanho de disco de {0} para o disco '\\{1 \\}' com 2 blob} é inválido. O tamanho do disco deve ser de {3} a {4}.  |
|  VMAgentStatusCommunicationError  |  A VM "{0}" não reportou o status do agente de VM ou extensões. Verifique se a saudação VM tem um agente VM em execução e pode estabelecer o armazenamento de tooAzure de conexões de saída.  |
|  VMArtifactRepositoryInternalError  |  Ocorreu um erro durante a comunicação com detalhes de artefato VM de tooretrieve de repositório de artefato de Olá.  |
|  VMArtifactRepositoryInternalError  |  Ocorreu um erro interno ao recuperar dados de artefato VM de saudação do repositório de artefato de saudação.  |
|  VMExtensionHandlerNonTransientError  |  O processador "{0}" relatou uma falha para a Extensão de VM "{1}" com o código de erro terminal "{2}" e a mensagem de erro: "{3}"  |
|  VMExtensionManagementInternalError  |  Ocorreu um erro interno durante o processamento da extensão de VM "{0}".  |
|  VMExtensionManagementInternalError  |  Vários erros ao preparar as extensões de VM hello. Consulte a exibição de instância de extensão de VM para obter detalhes.  |
|  VMExtensionProvisioningError  |  A VM reportou uma falha durante o processamento da extensão "{0}". Mensagem de erro: "{1}".  |
|  VMExtensionProvisioningError  |  Várias extensões VM falha toobe provisionado no hello VM. Consulte a exibição de instância de extensão VM de saudação para obter detalhes.  |
|  VMExtensionProvisioningTimeout  |  Provisionamento de extensão da VM "{0}" expirou. A instalação da extensão pode estar demorando muito tempo, ou não foi possível obtê-la.  |
|  VMMarketplaceInvalidInput  |  Criar uma máquina virtual de uma imagem do Marketplace não precisa de informações do plano, remova Olá informações do plano na solicitação de saudação. O nome de disco do SO é {0}.  |
|  VMMarketplaceInvalidInput  |  informações de compra de saudação não coincide. Não é possível toodeploy Olá imagem do Marketplace. O nome de disco do SO é {0}.  |
|  VMMarketplaceInvalidInput  |  Criar uma máquina virtual da imagem do Marketplace exige informações do plano na solicitação de saudação. O nome de disco do SO é {0}.  |
|  VMNotFound  |  VM Hello '{0}' não pode ser encontrado.  |
|  VMRedeploymentFailed  |  Reimplantação da VM '{0}' falhou devido a erro interno tooan. Tente novamente mais tarde.  |
|  VMRedeploymentTimedOut  |  Reimplantação da máquina virtual '{0}' não foi concluída no hello determinado tempo. Ela pode ser concluída a qualquer momento. Caso contrário, você poderá repetir a solicitação de saudação.  |
|  VMStartTimedOut  |  VM '{0}' não foi iniciado no hello determinado tempo. Olá VM ainda pode ser iniciada com êxito. Verifique o estado de energia hello mais tarde.  |


## <a name="next-steps"></a>Próximas etapas
Se você precisar de mais ajuda, você pode contatar hello Azure especialistas em [Olá fóruns MSDN Azure e o estouro de pilha](https://azure.microsoft.com/support/forums/). Como alternativa, você pode registrar um incidente de suporte do Azure. Vá toohello [site de suporte do Azure](https://azure.microsoft.com/support/options/) e selecione **obter suporte**.
