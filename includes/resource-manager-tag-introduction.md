Você aplica marcas tooyour recursos do Azure toologically organizá-los por categorias. Cada marca consiste em um nome e em um valor. Por exemplo, você pode aplicar nome hello "Ambiente" e recursos do Olá Olá valor "Produção" tooall em produção. Sem essa marca, você pode ter dificuldade para identificar se um recurso é destinado para desenvolvimento, teste ou produção. No entanto, "Ambiente" e "Produção" são apenas exemplos. Você define nomes hello e valores que compõem hello mais sentido para a organização de sua assinatura.

Depois de aplicar marcas, você pode recuperar todos os recursos de saudação em sua assinatura com esse nome de marca e o valor. Marcas permitem que você tooretrieve relacionadas a recursos que residem em diferentes grupos de recursos. Essa abordagem é útil quando você precisa de recursos de tooorganize de cobrança ou gerenciamento.

Olá seguintes limitações se aplicam a tootags:

* Cada recurso ou grupo de recursos pode ter um máximo de 15 pares de nome/valor de marca. Essa limitação aplica-se apenas o grupo de recursos de toohello tootags aplicado diretamente ou recurso. Um grupo de recursos pode conter muitos recursos que possuem 15 pares de nome/valor de marca. 
* nome da marca da saudação é limitado too512 caracteres e o valor de marca Olá é limitado too256 caracteres. Para contas de armazenamento, o nome da marca Olá é limitado too128 caracteres e valor da marca de saudação é limitado too256 caracteres.
* Grupo de recursos de toohello marcas aplicadas não são herdadas pelos recursos de saudação desse grupo de recursos. 

Se você tiver mais de 15 valores que você precisa tooassociate com um recurso, use uma cadeia de caracteres JSON para o valor de marca hello. saudação de cadeia de caracteres JSON pode conter muitos valores que são aplicadas tooa o nome da marca única. Este artigo mostra um exemplo de atribuição de uma marca de toohello de cadeia de caracteres JSON.
