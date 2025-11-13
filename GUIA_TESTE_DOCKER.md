# Guia de Teste - Docker

## ✅ Checklist de Verificação Antes da Apresentação

### 1. Verificar se a imagem está no Docker Hub
```bash
# Verificar se consegue fazer pull da imagem
docker pull villelar/gs-2-vr-ar-workspaces:latest
```

### 2. Testar build local da imagem
```bash
# Build da imagem localmente
docker build -t gs-2-vr-ar-workspaces:local .

# Verificar se a imagem foi criada
docker images | grep gs-2-vr-ar-workspaces
```

### 3. Testar execução do container
```bash
# Executar o container
docker run -d -p 8081:8081 --name gs-2-test gs-2-vr-ar-workspaces:local

# Verificar se o container está rodando
docker ps | grep gs-2-test

# Ver logs (aguardar alguns segundos para a aplicação iniciar)
docker logs gs-2-test
```

### 4. Testar endpoints da API
```bash
# Testar endpoint /info
curl http://localhost:8081/info

# Testar endpoint /api/v1/tema/info
curl http://localhost:8081/api/v1/tema/info

# Testar endpoint /api/v1/tema/ping
curl http://localhost:8081/api/v1/tema/ping
```

### 5. Testar com Docker Compose
```bash
# Subir o container
docker compose up -d

# Verificar logs
docker compose logs -f

# Testar endpoints
curl http://localhost:8081/info

# Parar o container
docker compose down
```

### 6. Limpar containers de teste
```bash
# Parar e remover container de teste
docker stop gs-2-test
docker rm gs-2-test

# Limpar imagens de teste (opcional)
docker rmi gs-2-vr-ar-workspaces:local
```

## 🚀 Comandos para a Sala de Aula

### Opção 1: Usar imagem do Docker Hub
```bash
# Pull da imagem
docker pull villelar/gs-2-vr-ar-workspaces:latest

# Executar
docker run -d -p 8081:8081 --name gs-2-api villelar/gs-2-vr-ar-workspaces:latest

# Verificar
docker ps
curl http://localhost:8081/info
```

### Opção 2: Build local (se não tiver internet)
```bash
# Clonar repositório (se necessário)
git clone https://github.com/VillelaR/gs-2-vr-ar-workspaces.git
cd gs-2-vr-ar-workspaces

# Build
docker build -t gs-2-vr-ar-workspaces:local .

# Executar
docker run -d -p 8081:8081 --name gs-2-api gs-2-vr-ar-workspaces:local
```

### Opção 3: Docker Compose
```bash
# Clonar repositório (se necessário)
git clone https://github.com/VillelaR/gs-2-vr-ar-workspaces.git
cd gs-2-vr-ar-workspaces

# Executar
docker compose up -d

# Verificar
docker compose ps
curl http://localhost:8081/info
```

## 📋 Verificações Finais

- [ ] Imagem Docker builda sem erros
- [ ] Container inicia corretamente
- [ ] Endpoint `/info` retorna JSON com tema, membro1, membro2 e descricao
- [ ] Endpoint `/api/v1/tema/info` funciona
- [ ] Swagger acessível em `http://localhost:8081/`
- [ ] Porta 8081 está exposta corretamente
- [ ] Logs não mostram erros

## 🔍 Troubleshooting

### Container não inicia
```bash
# Ver logs detalhados
docker logs gs-2-api

# Verificar se a porta está em uso
netstat -an | grep 8081
# ou no Linux
lsof -i :8081
```

### Erro de porta já em uso
```bash
# Parar container que está usando a porta
docker stop $(docker ps -q --filter "publish=8081")

# Ou usar outra porta
docker run -d -p 8082:8081 --name gs-2-api villelar/gs-2-vr-ar-workspaces:latest
# Acessar em http://localhost:8082/info
```

### Erro ao fazer pull
```bash
# Verificar conexão com Docker Hub
docker login

# Tentar novamente
docker pull villelar/gs-2-vr-ar-workspaces:latest
```

