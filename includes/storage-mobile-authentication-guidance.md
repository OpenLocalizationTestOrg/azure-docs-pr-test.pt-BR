## <a name="configure-your-application-tooaccess-azure-storage"></a>Configurar seu aplicativo tooaccess armazenamento do Azure
Há dois tooauthenticate de maneiras tooaccess seu aplicativo Serviços de armazenamento:

* Chave compartilhada: usar a chave compartilhada somente para fins de teste
* SAS (Assinatura de Acesso Compartilhado): use a SAS para aplicativos de produção

### <a name="shared-key"></a>Chave compartilhada
Autenticação de chave compartilhada significa que seu aplicativo usará o nome da conta e conta tooaccess chave serviços de armazenamento. Para fins de saudação do rapidamente mostrando como toouse nessa biblioteca, vamos usar a autenticação de chave compartilhada neste guia de Introdução.

> [!WARNING] 
> **Use autenticação de chave compartilhada somente para fins de teste!** O nome da conta e chave de conta, que concedem toohello de acesso de leitura/gravação completa conta de armazenamento associada, será distribuído tooevery pessoa que faz o download de seu aplicativo. Isso **não** é uma prática recomendada, pois você corre o risco de ter sua chave comprometida por clientes não confiáveis.
> 
> 

Ao usar a autenticação de Chave Compartilhada, você criará uma [cadeia de conexão](../articles/storage/common/storage-configure-connection-string.md). cadeia de caracteres de conexão de saudação é composta de:  

* Olá **DefaultEndpointsProtocol** -você pode escolher HTTP ou HTTPS. No entanto, é altamente recomendável usar HTTPS.
* Olá **nome da conta** - Olá nome da sua conta de armazenamento
* Olá **chave de conta** - nas Olá [Portal do Azure](https://portal.azure.com), navegue tooyour conta de armazenamento e clique em Olá **chaves** ícone toofind essas informações.
* (Opcional) **EndpointSuffix** - é usado para serviços de armazenamento em regiões com sufixos de ponto de extremidade diferentes, como o Azure China ou a Governança do Azure.

Veja um exemplo de cadeia de conexão usando a autenticação de Chave Compartilhada:

`"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here"`

### <a name="shared-access-signatures-sas"></a>SAS (Assinaturas de Acesso Compartilhado)
Para um aplicativo móvel, Olá recomendado método para autenticar uma solicitação por um cliente em relação a saudação serviço de armazenamento do Azure está usando uma assinatura de acesso compartilhado (SAS). SAS permite que você toogrant um recurso de tooa de acesso de cliente por um período especificado de tempo, com um conjunto de permissões especificado.
Como proprietário da conta de armazenamento hello, você precisará toogenerate um SAS para seu tooconsume clientes móveis. toogenerate Olá SAS, você provavelmente vai querer toowrite um serviço separado que gera Olá SAS toobe distribuída tooyour clientes. Para fins de teste, você pode usar o hello [Microsoft Azure Storage Explorer](http://storageexplorer.com) ou hello [Portal do Azure](https://portal.azure.com) toogenerate um SAS. Quando você cria Olá SAS, você pode especificar o intervalo de tempo de saudação sobre quais Olá SAS é válida e permissões de Olá Olá SAS concede toohello cliente.

saudação de exemplo a seguir mostra como toouse Olá toogenerate do Microsoft Azure Storage Explorer uma SAS.

1. Se você ainda não o fez, [Olá de instalação do Microsoft Azure Storage Explorer](http://storageexplorer.com)
2. Conecte-se a assinatura de tooyour.
3. Clique em sua conta de armazenamento e clique na guia Ações"hello" na parte inferior de saudação à esquerda. Clique em "Obter a assinatura de acesso compartilhado" toogenerate "cadeia de conexão" para o SAS.
4. Aqui está um exemplo de uma cadeia de caracteres de conexão de SAS que concede permissões leitura e gravação no serviço hello, contêiner e nível de objeto para o serviço de blob Olá Olá da conta de armazenamento.
   
   `"SharedAccessSignature=sv=2015-04-05&ss=b&srt=sco&sp=rw&se=2016-07-21T18%3A00%3A00Z&sig=3ABdLOJZosCp0o491T%2BqZGKIhafF1nlM3MzESDDD3Gg%3D;BlobEndpoint=https://youraccount.blob.core.windows.net"`

Como você pode ver, ao usar um SAS, você não expõe a chave de sua conta em seu aplicativo. Você pode aprender mais sobre SAS e práticas recomendadas para usar SAS fazendo check-out [assinaturas de acesso compartilhado: modelo SAS Olá Noções básicas sobre](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md).

