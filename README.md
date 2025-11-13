# GS-2 VR/AR Workspaces

API Java para integração de Ambientes de trabalho com Realidade Virtual ou Aumentada

## Criando .jar

```
mvn clean package
```

- Localizar o .jar em /target

```
java -jar target/app.jar
```

## Executar a API

-  *Executando* **Maven**

```
mvn spring-boot:run
```

-  *Executando* **Maven Wrapper**

```
./mvnw spring-boot:run
```

-  *Instruções* **Docker Compose**

    -  https://devhints.io/docker-compose

```
docker compose up
docker compose stop
```

### Documentação da API (Swagger)
- http://localhost:8081/

## Membros do Grupo

- **Rafael Bueno Villela**
  - RM: 550275

- **Cesar Iglesias**
  - RM: 98007

## Tema Escolhido

**Ambientes de trabalho com Realidade Virtual ou Aumentada**

**Cálculo do tema:**
- RM1: 550275
- RM2: 98007
- Soma: 550275 + 98007 = 648282
- Último dígito: 2
- Tema selecionado: Tema 2

## Descrição do Tema

Esta API foi desenvolvida para suportar ambientes de trabalho inovadores que utilizam tecnologias de Realidade Virtual (VR) e Realidade Aumentada (AR). O objetivo é criar plataformas que permitam colaboração remota imersiva, reuniões virtuais em espaços 3D, treinamentos interativos e ambientes de trabalho híbridos que combinam elementos físicos e digitais. A solução visa transformar a forma como as equipes trabalham, oferecendo experiências mais envolventes e produtivas através de tecnologias imersivas.

## Finalidade da API

A API de integração para Ambientes de trabalho com Realidade Virtual ou Aumentada foi projetada para:

- Facilitar a integração entre sistemas de VR/AR e plataformas de trabalho colaborativo
- Fornecer endpoints para gerenciamento de ambientes virtuais de trabalho
- Suportar sincronização de dados entre ambientes físicos e virtuais
- Permitir a criação e gerenciamento de espaços de trabalho imersivos
- Oferecer APIs para integração com dispositivos de realidade aumentada e virtual

## Endpoints Disponíveis

### GET /api/v1/tema/info

Retorna informações sobre o tema do projeto, membros do grupo e descrição.

**Resposta:**
```json
{
  "tema": "Ambientes de trabalho com Realidade Virtual ou Aumentada",
  "membro1": "Rafael Bueno Villela - RM550275",
  "membro2": "Cesar Iglesias - RM98007",
  "descricao": "Descrição detalhada do tema..."
}
```

### GET /api/v1/tema/ping

Endpoint de health check.

**Resposta:**
```
Pong
```

### GET /api/v1/tema/version

Retorna a versão da API.

## Docker Hub

**URL da Imagem no Docker Hub:**
```
https://hub.docker.com/r/villelar/gs-2-vr-ar-workspaces
```

**Comando para pull:**
```bash
docker pull villelar/gs-2-vr-ar-workspaces:latest
```

## Workflows CI/CD

O projeto possui três workflows GitHub Actions configurados:

### 1. Versionamento (release-please.yml)

**Trigger:** Push na branch `main`

**Funcionalidades:**
- Gera tags automáticas usando release-please
- Cria releases automaticamente

### 2. Continuous Integration (ci.yaml)

**Trigger:** Push nas branches `feature/**`, `release`, `hotfix`

**Funcionalidades:**
- Compila a aplicação
- Executa testes unitários
- Constrói a imagem Docker para verificação

### 3. Continuous Delivery (cd.yaml)

**Trigger:** Pull Request para a branch `develop`

**Funcionalidades:**
- Compila e empacota a aplicação
- Constrói a imagem Docker
- Envia automaticamente a imagem para o Docker Hub

### Configuração de Secrets

**Workflow de Versionamento:**
- Usa automaticamente o `GITHUB_TOKEN` fornecido pelo GitHub Actions
- Não requer configuração adicional

**Workflow de CD:**
- Executa apenas em Pull Requests para a branch `develop`
- Requer configuração de secrets para funcionar:
  1. Acesse: Settings → Secrets and variables → Actions
  2. Adicione:
     - **Variable**: `DOCKER_USER` (seu usuário do Docker Hub - ex: `villelar`)
     - **Secret**: `DOCKER_TOKEN` (seu token do Docker Hub)
- Faz push automático da imagem para: `${{ vars.DOCKER_USER }}/gs-2-vr-ar-workspaces:latest`

## Referencias

- https://springdoc.org/
