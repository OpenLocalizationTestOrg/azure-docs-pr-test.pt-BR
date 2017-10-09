As Máquinas Virtuais do Azure têm suporte para a anexação de vários discos de dados. Para otimizar o desempenho, você desejará toolimit número de saudação de discos altamente utilizados anexado toohello máquina virtual tooavoid possíveis de limitação. Se todos os discos não estão sendo intensamente utilizados no hello mesmo tempo, conta de armazenamento Olá pode dar suporte a discos de um número maior.

* **Para discos gerenciado do Azure:** limite de contagem de discos gerenciado é regional e também depende de tipo de armazenamento de saudação. Olá padrão e também o limite máximo de saudação é 10.000 por assinatura, por região e por tipo de armazenamento. Por exemplo, você pode criar até too10, standard, 000 gerenciados discos e também 10.000 premium gerenciados discos em uma assinatura em uma região. 

    Instantâneos gerenciado e imagens são contadas em relação a saudação que limitar discos gerenciados.

* **Para contas de armazenamento padrão:** uma conta de armazenamento padrão tem uma taxa de solicitação total máxima de 20.000 IOPS. Olá IOPS total em todos os discos da máquina virtual em uma conta de armazenamento padrão não deve exceder esse limite.
  
    Você aproximadamente pode calcular o número de saudação de discos altamente utilizados suportado por uma conta de armazenamento único padrão com base no limite de taxa de solicitação de saudação. Por exemplo, para uma camada básica VM, Olá número máximo de altamente utilizados discos é aproximadamente 66 (20.000/300 IOPS por disco), e para uma VM de camada padrão, é cerca de 40 (IOPS de 20.000/500 por disco), conforme mostrado na tabela de saudação abaixo. 
* **Para contas de armazenamento premium:** uma conta de armazenamento premium tem uma taxa de transferência total máxima de 50 Gbps. taxa de transferência total em todos os discos VM saudação não deve exceder esse limite.

