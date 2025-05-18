Larissa de Freitas Moura -rm555136
João Victor Rebello -rm555287
Guilherme Francisco Silva -rm557648

MotoScan API
API RESTful para gerenciamento de uma frota de motos da Mottu, desenvolvida com ASP.NET Core.
Descrição
O MotoScan é uma API para controle de entrada e saída de motos, permitindo check-in, check-out e gerenciamento de informações das motos na frota. A API utiliza ASP.NET Core com Entity Framework Core para integração com banco de dados Oracle.
Tecnologias utilizadas

ASP.NET Core 6.0
Entity Framework Core 6.0
Swagger/OpenAPI para documentação
Banco de dados Oracle
Docker (configuração disponível)

Rotas disponíveis
Motos

GET /api/Motos - Lista todas as motos cadastradas no sistema
GET /api/Motos/{id} - Busca moto pelo ID numérico
GET /api/Motos/placa/{placa} - Busca moto pela placa (ex: ABC1234)
POST /api/Motos - Adiciona nova moto à frota
PUT /api/Motos/{id} - Atualiza informações de uma moto existente
DELETE /api/Motos/{id} - Remove uma moto do sistema

Check-in e Check-out

POST /api/Motos/checkin - Registra entrada de moto com imagem de documentação
POST /api/Motos/checkout - Registra saída de moto com imagem de documentação

Modelo de dados
A entidade Moto possui os seguintes atributos:

Id (int): Identificador único da moto
Modelo (string): Modelo da moto (ex: Honda CG 160)
Placa (string): Placa da moto (ex: ABC1234)
Estado (string): Estado de conservação da moto (ex: Bom, Regular, Excelente)
Localizacao (string): Localização atual da moto (ex: Pátio A, Saída, etc.)
UltimoCheckIn (DateTime?): Data e hora do último check-in
UltimoCheckOut (DateTime?): Data e hora do último check-out
ImagemUrl (string): URL para a imagem da moto (se disponível)

Modelos de motos suportados

Honda CG 160
Honda Pop 110i
Mottu Sport 110i (fabricado pela TVS)
Mottu-e (modelo elétrico)
Honda Biz 125

Instruções de instalação

Clone o repositório
git clone https://github.com/LarissaMouraDev/MotoScan-api.git

Navegue até a pasta do projeto
cd MotoScan-api

Restaure os pacotes NuGet
dotnet restore

Configure a string de conexão com o banco de dados Oracle no arquivo appsettings.json
json"ConnectionStrings": {
  "OracleConnection": "User Id=seu_usuario;Password=sua_senha;Data Source=oracle.fiap.com.br"
}

Execute as migrações do Entity Framework Core para criar as tabelas no banco de dados
dotnet ef database update

Execute o projeto
dotnet run

Acesse a documentação da API em https://localhost:5001/swagger

Como testar os endpoints
Listar todas as motos
httpGET /api/Motos
Buscar moto por ID
httpGET /api/Motos/1
Buscar moto pela placa
httpGET /api/Motos/placa/ABC1234
Adicionar nova moto
httpPOST /api/Motos
Content-Type: application/json

{
  "modelo": "Honda CG 160",
  "placa": "XYZ9876",
  "estado": "Excelente",
  "localizacao": "Entrada"
}
Atualizar moto existente
httpPUT /api/Motos/1
Content-Type: application/json

{
  "id": 1,
  "modelo": "Honda CG 160",
  "placa": "XYZ9876",
  "estado": "Regular",
  "localizacao": "Pátio B"
}
Registrar check-in de moto
httpPOST /api/Motos/checkin?placa=XYZ9876
Content-Type: multipart/form-data

[Imagem como FormFile]
Registrar check-out de moto
httpPOST /api/Motos/checkout?placa=XYZ9876
Content-Type: multipart/form-data

[Imagem como FormFile]
Estrutura do projeto
MotoScan/
├── Controllers/           # Controladores da API
│   └── MotosController.cs
├── Data/                  # Acesso a dados
│   ├── AppDbContext.cs
│   └── DbInitializer.cs
├── Models/                # Modelos de dados
│   └── Moto.cs
├── Services/              # Serviços
│   └── ImagemService.cs
├── Properties/            # Configurações de lançamento
├── wwwroot/               # Arquivos estáticos
│   └── Imagens/           # Armazenamento de imagens
│       ├── Checkin/
│       └── Checkout/
├── appsettings.json       # Configurações da aplicação
├── Program.cs             # Ponto de entrada da aplicação
└── README.md              # Este arquivo
Requisitos

.NET 6.0 ou superior
Acesso a um banco de dados Oracle
Espaço em disco para armazenar as imagens de check-in/check-out

Implementação
Esta API foi desenvolvida seguindo os requisitos do projeto:

API RESTful utilizando ASP.NET Core (Controllers ou Minimal API)
CRUD completo (GET, POST, PUT, DELETE)
Rotas parametrizadas corretamente (QueryParams e PathParams)
Retornos HTTP adequados (200 OK, 404 NotFound, 400 BadRequest, 201 Created)
Integração com Banco de Dados Oracle via Entity Framework Core
Documentação da API via Swagger/OpenAPI
Armazenamento de imagens para registro de entrada e saída de motos

Docker
Para executar o projeto usando Docker:

Construa a imagem
docker build -t motoscan .

Execute o contêiner
docker run -p 8080:80 -e "ConnectionStrings__OracleConnection=User Id=seu_usuario;Password=sua_senha;Data Source=oracle.fiap.com.br" motoscan

Acesse a API em http://localhost:8080/swagger

Contribuições
Contribuições são bem-vindas! Para contribuir:

Faça um fork do projeto
Crie uma branch para sua feature (git checkout -b feature/nova-feature)
Commit suas mudanças (git commit -am 'Adiciona nova feature')
Push para a branch (git push origin feature/nova-feature)
Crie um novo Pull Request

Licença
Este projeto está licenciado sob a licença MIT.
