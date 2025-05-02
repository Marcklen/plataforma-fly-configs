# 📦 plataforma-fly-configs

Repositório de arquivos de configuração centralizada para os microserviços da plataforma FLY.

Este repositório é usado pelo **Config Server (Spring Cloud Config Server)** para distribuir configurações entre os microsserviços.

---

## 📁 Estrutura

```bash
├── application.yml                 # Configurações globais para todos os serviços
├── gateway-api-dev.yml
├── auth-api-dev.yml
├── usuario-api-dev.yml

## 🛠️ Banco de Dados: H2 (Desenvolvimento) e PostgreSQL (Produção)

Durante o desenvolvimento local, usei o banco de dados **H2 em memória** pela sua facilidade de uso e inicialização rápida — ideal para testes e desenvolvimento contínuo sem precisar de infraestrutura externa.

No ambiente de **produção**, estarei utilizado **PostgreSQL**, um banco robusto, confiável e com suporte a recursos avançados — essencial para aplicações reais e seguras.

> Todos os serviços em produção serão executados em containers **Docker** (via `docker-compose`), com exceção do banco H2, que permanece **somente no ambiente de desenvolvimento**.