🛵 MotoScan API
API RESTful para gerenciamento de frota de motos da Mottu, desenvolvida com ASP.NET Core 6.0.

📄 Descrição
O MotoScan é uma API que permite o controle completo de entrada e saída de motos, com funcionalidades de:

Check-in e check-out com imagem

CRUD completo das motos da frota

Armazenamento e rastreamento de dados via Oracle

⚙️ Tecnologias Utilizadas
ASP.NET Core 6.0

Entity Framework Core 6.0

Swagger/OpenAPI

Oracle Database

Docker

🚦 Rotas Disponíveis
🔧 Motos
Método	Endpoint	Descrição
GET	/api/Motos	Lista todas as motos
GET	/api/Motos/{id}	Busca moto por ID
GET	/api/Motos/placa/{placa}	Busca moto pela placa (ex: ABC1234)
POST	/api/Motos	Adiciona uma nova moto
PUT	/api/Motos/{id}	Atualiza informações de uma moto
DELETE	/api/Motos/{id}	Remove uma moto do sistema

🏁 Check-in e Check-out
Método	Endpoint	Descrição
POST	/api/Motos/checkin	Registra entrada de moto (com imagem)
POST	/api/Motos/checkout	Registra saída de moto (com imagem)

🧩 Modelo de Dados
A entidade Moto possui os seguintes atributos:

csharp
Copiar
Editar
Id (int)
Modelo (string)
Placa (string)
Estado (string)
Localizacao (string)
UltimoCheckIn (DateTime?)
UltimoCheckOut (DateTime?)
ImagemUrl (string)
🏍️ Modelos de Motos Suportados
Honda CG 160

Honda Pop 110i

Mottu Sport 110i (fabricado pela TVS)

Mottu-e (modelo elétrico)

Honda Biz 125

🚀 Como Instalar
bash
Copiar
Editar
# Clone o repositório
git clone https://github.com/LarissaMouraDev/MotoScan-api.git

# Navegue até o diretório do projeto
cd MotoScan-api

# Restaure os pacotes NuGet
dotnet restore
🔧 Configure a conexão com Oracle
No arquivo appsettings.json:

json
Copiar
Editar
"ConnectionStrings": {
  "OracleConnection": "User Id=seu_usuario;Password=sua_senha;Data Source=oracle.fiap.com.br"
}
🏗️ Execute as migrações
bash
Copiar
Editar
dotnet ef database update
▶️ Execute o projeto
bash
Copiar
Editar
dotnet run
Acesse a documentação Swagger em:
🔗 https://localhost:5001/swagger

🧪 Como Testar os Endpoints
🔍 Buscar motos
http
Copiar
Editar
GET /api/Motos
GET /api/Motos/1
GET /api/Motos/placa/ABC1234
➕ Adicionar nova moto
http
Copiar
Editar
POST /api/Motos
Content-Type: application/json

{
  "modelo": "Honda CG 160",
  "placa": "XYZ9876",
  "estado": "Excelente",
  "localizacao": "Entrada"
}
✏️ Atualizar moto
http
Copiar
Editar
PUT /api/Motos/1
Content-Type: application/json

{
  "id": 1,
  "modelo": "Honda CG 160",
  "placa": "XYZ9876",
  "estado": "Regular",
  "localizacao": "Pátio B"
}
📥 Check-in da moto
http
Copiar
Editar
POST /api/Motos/checkin?placa=XYZ9876
Content-Type: multipart/form-data
[Imagem como FormFile]
📤 Check-out da moto
http
Copiar
Editar
POST /api/Motos/checkout?placa=XYZ9876
Content-Type: multipart/form-data
[Imagem como FormFile]
🗂️ Estrutura do Projeto
bash
Copiar
Editar
MotoScan/
├── Controllers/        # Controladores da API
│   └── MotosController.cs
├── Data/               # Acesso a dados
│   ├── AppDbContext.cs
│   └── DbInitializer.cs
├── Models/             # Modelos de dados
│   └── Moto.cs
├── Services/           # Serviços auxiliares
│   └── ImagemService.cs
├── Properties/         # Configurações
├── wwwroot/            # Arquivos estáticos
│   └── Imagens/
│       ├── Checkin/
│       └── Checkout/
├── appsettings.json    # Configurações da aplicação
├── Program.cs          # Ponto de entrada
└── README.md           # Este arquivo
🐳 Executando com Docker
bash
Copiar
Editar
# Build da imagem
docker build -t motoscan .

# Executar o container
docker run -p 8080:80 \
-e "ConnectionStrings__OracleConnection=User Id=seu_usuario;Password=sua_senha;Data Source=oracle.fiap.com.br" \
motoscan
Acesse a API via:
🔗 http://localhost:8080/swagger

📄 Licença
Este projeto está licenciado sob a Licença MIT.
