<span data-ttu-id="7055d-101">Se você possui uma URL de SAS (assinatura de acesso compartilhado) que concede acesso a recursos em uma conta de armazenamento, pode usar a SAS em uma cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="7055d-101">If you possess a shared access signature (SAS) URL that grants you access to resources in a storage account, you can use the SAS in a connection string.</span></span> <span data-ttu-id="7055d-102">Como a SAS contém as informações necessárias para autenticar a solicitação, uma cadeia de conexão com uma SAS fornece o protocolo, o ponto de extremidade de serviço e as credenciais necessárias para acessar o recurso.</span><span class="sxs-lookup"><span data-stu-id="7055d-102">Because the SAS contains the information required to authenticate the request, a connection string with a SAS provides the protocol, the service endpoint, and the necessary credentials to access the resource.</span></span>

<span data-ttu-id="7055d-103">Para criar uma cadeia de conexão que inclui uma assinatura de acesso compartilhado, especifique a cadeia de caracteres no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="7055d-103">To create a connection string that includes a shared access signature, specify the string in the following format:</span></span>

```
BlobEndpoint=myBlobEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
FileEndpoint=myFileEndpoint;
SharedAccessSignature=sasToken
```

<span data-ttu-id="7055d-104">Cada ponto de extremidade de serviço é opcional, embora a cadeia de conexão deve conter pelo menos um.</span><span class="sxs-lookup"><span data-stu-id="7055d-104">Each service endpoint is optional, although the connection string must contain at least one.</span></span>

> [!NOTE]
> <span data-ttu-id="7055d-105">Usar HTTPS com uma SAS é uma prática recomendada.</span><span class="sxs-lookup"><span data-stu-id="7055d-105">Using HTTPS with a SAS is recommended as a best practice.</span></span>
>
> <span data-ttu-id="7055d-106">Se você estiver especificando uma SAS em uma cadeia de conexão em um arquivo de configuração, precisará codificar caracteres especiais na URL.</span><span class="sxs-lookup"><span data-stu-id="7055d-106">If you are specifying a SAS in a connection string in a configuration file, you may need to encode special characters in the URL.</span></span>
>
>

### <a name="service-sas-example"></a><span data-ttu-id="7055d-107">Exemplo de SAS de serviço</span><span class="sxs-lookup"><span data-stu-id="7055d-107">Service SAS example</span></span>
<span data-ttu-id="7055d-108">Aqui está um exemplo de uma cadeia de conexão que inclui um serviço SAS para o Armazenamento de Blobs:</span><span class="sxs-lookup"><span data-stu-id="7055d-108">Here's an example of a connection string that includes a service SAS for Blob storage:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
SharedAccessSignature=sv=2015-04-05&sr=b&si=tutorial-policy-635959936145100803&sig=9aCzs76n0E7y5BpEi2GvsSv433BZa22leDOZXX%2BXXIU%3D
```

<span data-ttu-id="7055d-109">E aqui está um exemplo da mesma cadeia de conexão com codificação de caracteres especiais:</span><span class="sxs-lookup"><span data-stu-id="7055d-109">And here's an example of the same connection string with encoding of special characters:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
SharedAccessSignature=sv=2015-04-05&amp;sr=b&amp;si=tutorial-policy-635959936145100803&amp;sig=9aCzs76n0E7y5BpEi2GvsSv433BZa22leDOZXX%2BXXIU%3D
```

### <a name="account-sas-example"></a><span data-ttu-id="7055d-110">Exemplo de SAS de conta</span><span class="sxs-lookup"><span data-stu-id="7055d-110">Account SAS example</span></span>
<span data-ttu-id="7055d-111">Aqui está um exemplo de uma cadeia de conexão que inclui uma conta SAS para o Armazenamento de Blobs e de Arquivos:</span><span class="sxs-lookup"><span data-stu-id="7055d-111">Here's an example of a connection string that includes an account SAS for Blob and File storage.</span></span> <span data-ttu-id="7055d-112">Observe que os pontos de extremidade para ambos os serviços são especificados:</span><span class="sxs-lookup"><span data-stu-id="7055d-112">Note that endpoints for both services are specified:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
FileEndpoint=https://storagesample.file.core.windows.net;
SharedAccessSignature=sv=2015-07-08&sig=iCvQmdZngZNW%2F4vw43j6%2BVz6fndHF5LI639QJba4r8o%3D&spr=https&st=2016-04-12T03%3A24%3A31Z&se=2016-04-13T03%3A29%3A31Z&srt=s&ss=bf&sp=rwl
```

<span data-ttu-id="7055d-113">E aqui está um exemplo da mesma cadeia de conexão com a codificação de URL:</span><span class="sxs-lookup"><span data-stu-id="7055d-113">And here's an example of the same connection string with URL encoding:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
FileEndpoint=https://storagesample.file.core.windows.net;
SharedAccessSignature=sv=2015-07-08&amp;sig=iCvQmdZngZNW%2F4vw43j6%2BVz6fndHF5LI639QJba4r8o%3D&amp;spr=https&amp;st=2016-04-12T03%3A24%3A31Z&amp;se=2016-04-13T03%3A29%3A31Z&amp;srt=s&amp;ss=bf&amp;sp=rwl
```

