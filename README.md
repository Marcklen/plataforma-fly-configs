# 📦 plataforma-fly-configs

Repositório centralizado de **configurações externas (Spring Cloud Config)** para os microsserviços da aplicação **Plataforma FLY**.

Este repositório é consumido dinamicamente pelo serviço `config-server`, que distribui configurações específicas por ambiente e por serviço, garantindo **centralização, versionamento e flexibilidade de ambientes**.

---

## 📁 Estrutura

```bash
├── application.yml                 # Configurações globais para todos os serviços
├── gateway-api-dev.yml
├── auth-api-dev.yml
├── usuario-api-dev.yml
├── eureka-server-dev.yml
├── email-producer-dev.yml
├── email-consumer-dev.yml
```

---

## 🧩 Microsserviços e Suas Funções

| Serviço                  | Finalidade                                                                 |
|--------------------------|---------------------------------------------------------------------------|
| **config-server**        | Fornece configurações externas centralizadas para todos os microsserviços. |
| **eureka-server**        | Gerencia registro e descoberta de serviços (Service Discovery).           |
| **gateway-api**          | Gateway principal da aplicação. Encaminha as requisições para os serviços corretos. |
| **auth-api**             | Responsável pela autenticação e autorização via JWT.                      |
| **usuario-api**          | CRUD de usuários, controle de acesso por roles, envio de e-mails, cache via Redis. |
| **email-producer-api**   | Produz mensagens para a fila de e-mails (RabbitMQ/Kafka).                 |
| **email-consumer-api**   | Consome as mensagens da fila e envia os e-mails reais (ex: via Mailtrap). |

---

## 🌍 Ambientes da Plataforma

A arquitetura foi planejada para suportar **três ambientes distintos**, cada um com sua finalidade e configuração específica:

### 1. LOCAL

- ✅ Ideal para desenvolvimento com **debug ativo via IntelliJ ou IDE**.
- 🚫 Não usa Docker.
- 🔍 Permite uso de breakpoints e inspeção em tempo real.
- ⚙️ Configurações específicas em arquivos como `*-local.yml`.

### 2. DEV (Desenvolvimento)

- 🐳 Executado **100% via Docker Compose**.
- 🧠 Banco de dados **H2** (memória) para agilidade e simplicidade.
- 🔗 Integrado a Redis, RabbitMQ, Kafka e Prometheus/Grafana para observabilidade.
- 📄 Arquivos de configuração nomeados como `*-dev.yml`.

### 3. PROD (Produção)

- 🏦 Banco de dados **PostgreSQL**.
- 🔐 Foco em persistência real, segurança e confiabilidade.
- 🧩 Todos os serviços são executados em containers.
- 💡 Pronto para deploy em nuvem (ex: AWS, GCP, etc).
- 📄 Arquivos de configuração nomeados como `*-prod.yml`.

---

### 📝 Observações Importantes

- As configurações deste repositório são consumidas via HTTP pelo config-server, que utiliza o Spring Cloud Config Client nos microsserviços para carregar dinamicamente os arquivos YAML.

- É importante manter os arquivos bem organizados e separados por serviço e ambiente (-dev.yml, -prod.yml, -local.yml).

- Esse padrão permite escalar a aplicação com segurança e simplicidade, seja localmente, em ambientes de desenvolvimento, staging ou produção.
