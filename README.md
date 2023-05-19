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
    
    
 


  
