# Projeto_Integrador_2SEM
Projeto 
Integração entre a máquina didática Planta Smart 4.0 com um sistema de E-commerce. A Planta Smart 4.0 é uma máquina que simula uma linha de produção de sucos. A máquina disponibiliza três opções de sucos, morango, laranja e maracujá, por limitações físicas só são possíveis selecionar três opções por vez, além de contar com um slot de estoque de dez itens. 
A solução de E-commerce se baseia em uma loja virtual, que faz requisições em HTTP para solicitar algum produto, realizar pagamentos, cadastrar usuários, visualizar estoque e recibo. Além de um sistema MES simplificado, que terá a responsabilidade de monitorar o estoque da máquina, existência de produtos fora dos padrões e os produtos entregues ao cliente.  

Tecnologias Utilizadas 
  1. Vue.Js/React - Framework responsável pelo Layout e interatividade do site. 
  
  2. Axios – Biblioteca Node.Js responsável pela integração entre FrontEnd e BackEnd, fazendo requisições em HTTP. 
  
  3. JavaScript – Linguagem de programação responsável pela interatividade do site. 
  
  4. Node.Js - Software JavaScript responsável por executar o código em JavaScript fora do navegador, processando o código de forma assíncrona e orientada a eventos, funcionando como uma espécie de servidor, recebendo e respondendo requisições dos clientes. 
  
  5. API’s - Aplicação que permite a troca de informações entre o MES, Loja Virtual e CLP. 
  
  6. Charts.Js – Biblioteca responsável pela geração de gráficos dos dados de entrada e saída. 
  
  7. MongoDB/Mongoose - Biblioteca responsável pela integração entre o Banco de Dados MongoDB com os dados do site.  
  
  8. Pinia - Biblioteca responsável por armazenar, gerenciar e acessar os estados em diversos componentes, sendo uma espécie de Variável Global. 
  
  9. Cors – Biblioteca responsável por restringir requisições HTTP de um domínio a outro diferente do qual foi gerado a solicitação, com o intuito de proteger os dados sensíveis contidos no na loja. 
  
  10. Node-opcua – Biblioteca responsável por implementar o protocolo OPC-UA, criando um servidor/cliente entre o MES e CLP. 

Dependências e configurações 

Node.js - Instalação através do site: https://nodejs.org/pt/download  

Vue.js/Vite - npm create vite@latest ProjetoIntegrador 

Dependências adicionais – npm install 

Pinia, axios, cors, vue-router, express e charts.js – npm install pinia axios vue-router cors express charts.js 

Protocolo OPCUA – npm install node-opcua 

Mongoose – npm install mongoose 

Arquitetura MVC (Model-View-Controller) 
A Arquitetura MVC se baseia em um software composto por três camadas, a camada Model, que realiza a lógica de negócios, ou seja, realiza a manipulação dos dados no software, View, parte responsável por exibir os dados para o usuário final, via textos ou gráficos e comunica o retorno dos dados ao Model e a camada Controller fica responsável por interpretar os inputs do sistema, mapeando as funções e enviando os dados ao Model e fazendo a comunicação com o View. 

Aplicação na Planta Smart 4.0 
Para aplicarmos o modelo de Arquitetura MVC no projeto, a camada Model será em torno do sistema MES e da Loja Virtual (Produto, Estoque, Pedido e Ordem de Produção). A View tem por finalidade a execução da Interface de Usuário do sistema, com as telas de catálogo de compras, status dos pedidos, pagamento e dashboard do MES. Já o Controller vai realizar a requisição e manter os dados atualizados entre o usuário e sistema. A Arquitetura MVC traz inúmeros benefícios ao projeto, como fácil manutenibilidade, escalabilidade, testabilidade (cada camada pode ser testada individualmente) e reutilização do código. 

