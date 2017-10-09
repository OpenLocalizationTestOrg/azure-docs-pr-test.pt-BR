Se você possuir uma URL de SAS (assinatura) de acesso compartilhado que concede que acesso tooresources em uma conta de armazenamento, você pode usar o hello SAS em uma cadeia de caracteres de conexão. Como Olá SAS contém a solicitação de Olá Olá informações tooauthenticate necessária, uma cadeia de caracteres de conexão com uma SAS fornece protocolo hello, ponto de extremidade de serviço hello e recursos de Olá Olá credenciais necessárias tooaccess.

toocreate uma cadeia de caracteres de conexão que inclui uma assinatura de acesso compartilhado, especifique a cadeia de saudação em Olá formato a seguir:

```
BlobEndpoint=myBlobEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
FileEndpoint=myFileEndpoint;
SharedAccessSignature=sasToken
```

Cada ponto de extremidade de serviço é opcional, embora a cadeia de caracteres de conexão Olá deve conter pelo menos um.

> [!NOTE]
> Usar HTTPS com uma SAS é uma prática recomendada.
>
> Se você estiver especificando uma SAS em uma cadeia de conexão em um arquivo de configuração, talvez seja necessário tooencode de caracteres especiais na URL de saudação.
>
>

### <a name="service-sas-example"></a>Exemplo de SAS de serviço
Aqui está um exemplo de uma cadeia de conexão que inclui um serviço SAS para o Armazenamento de Blobs:

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
SharedAccessSignature=sv=2015-04-05&sr=b&si=tutorial-policy-635959936145100803&sig=9aCzs76n0E7y5BpEi2GvsSv433BZa22leDOZXX%2BXXIU%3D
```

E aqui está um exemplo de hello mesma cadeia de caracteres de conexão com a codificação de caracteres especiais:

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
SharedAccessSignature=sv=2015-04-05&amp;sr=b&amp;si=tutorial-policy-635959936145100803&amp;sig=9aCzs76n0E7y5BpEi2GvsSv433BZa22leDOZXX%2BXXIU%3D
```

### <a name="account-sas-example"></a>Exemplo de SAS de conta
Aqui está um exemplo de uma cadeia de conexão que inclui uma conta SAS para o Armazenamento de Blobs e de Arquivos: Observe que os pontos de extremidade para ambos os serviços são especificados:

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
FileEndpoint=https://storagesample.file.core.windows.net;
SharedAccessSignature=sv=2015-07-08&sig=iCvQmdZngZNW%2F4vw43j6%2BVz6fndHF5LI639QJba4r8o%3D&spr=https&st=2016-04-12T03%3A24%3A31Z&se=2016-04-13T03%3A29%3A31Z&srt=s&ss=bf&sp=rwl
```

E aqui está um exemplo de hello mesma cadeia de caracteres de conexão com a codificação de URL:

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
FileEndpoint=https://storagesample.file.core.windows.net;
SharedAccessSignature=sv=2015-07-08&amp;sig=iCvQmdZngZNW%2F4vw43j6%2BVz6fndHF5LI639QJba4r8o%3D&amp;spr=https&amp;st=2016-04-12T03%3A24%3A31Z&amp;se=2016-04-13T03%3A29%3A31Z&amp;srt=s&amp;ss=bf&amp;sp=rwl
```

