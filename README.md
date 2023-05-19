# dio-aws-api
Passos realizados no projeto
  1-Barra de pesquisa "Search" -> API GateWay
    1.1 CreateAPI - > REST API "SEM VPC" ->
      Choose the protocol: REST
      Create new API: New API
        API Name = dio_live_api_new
        Description = 
        Endpoint Type = Regional
     1.2 Ir no botão Actions "Create Resources"
          Resource Name = Items
          Apertar no botão "Create Resources"
     
 2-Barra de pesquisa "Search" -> DynamoDB
  2.1 Ir no botão "Create table"
    Table name = DIOItems
    Partition key = id [String]
    Deixar o resto como padrão e clicar em -> "Create Table"
    
    
 3-Barra de pesquisa "Search" -> Lambda
  3.1 Ir no botão amarelo "Create function"
    Function name = dio_put_items_function
    Resto põe padrão e clica em "Create function"
  
  3.2 Editado o arquivo index.js (O mesmo esta no repositorio)
 
  3.3 Configuration -> Permissions -> Clicar em "dio_put_items_function-role-sdq15tez"
  
  4- Agora vamos para tela do IAM "Identity and Acess Managament"
    4.1 Vá no botão "Add permissions" -> "Create inline policy"
    4.2 Service = Clique em "Choose a service" -> pesquise e selecione "DynamoDB"
    4.3 Click em "add actions" -> Digite "putItem" e clique em "ADD"
    4.4 Vá em resources  -> ADD ARN
    4.5 vá no DynamoDB e pegue o ARN da tabela e digite na tela anterior
    4.6 
    
    
   
    
    
    
 


  
