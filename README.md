## 🧠 IBM watsonx Code Assistant – Lightspeed (L3) for Ansible

### 📘 Visão Geral

O **IBM watsonx Code Assistant – Lightspeed (L3)** é uma extensão de inteligência artificial generativa projetada para **acelerar o desenvolvimento de automações**, especialmente para **Ansible, Red Hat e infraestrutura em nuvem**.
Ele interpreta comentários em linguagem natural e gera automaticamente **playbooks, roles e tasks** com base nas melhores práticas da Red Hat e coleções oficiais Ansible.

> 💡 O nível **L3** (Lightspeed Tier 3) oferece suporte avançado a módulos específicos da Red Hat e AWS, contextualização de variáveis e integração com repositórios Git corporativos.

---

## ⚙️ Funcionalidades Principais

* 💬 **Geração de código com comentários** — basta escrever uma descrição natural (ex: *“criar um cluster ECS com Fargate”*) e o assistente gera o YAML pronto.
* 🧩 **Integração nativa com Ansible** — reconhece módulos das coleções `amazon.aws`, `community.general`, `ansible.builtin`, etc.
* 🔍 **Linting automático** — valida sintaxe e conformidade com as melhores práticas usando `ansible-lint`.
* 🧠 **Contexto de playbook** — entende variáveis e tasks anteriores para gerar código coerente.
* 🔒 **Segurança corporativa** — integração com IBM Cloud Identity e suporte a políticas de conformidade.

---

## 🖥️ Pré-requisitos

### 🔹 Sistema operacional

* **Linux** (recomendado) ou **Windows com WSL (Ubuntu)**
* macOS também é suportado para desenvolvimento local

### 🔹 Softwares necessários

| Dependência                | Versão mínima | Descrição                                         |
| -------------------------- | ------------- | ------------------------------------------------- |
| Python                     | 3.8+          | Necessário para executar o Ansible e dependências |
| Ansible                    | 2.15+         | Ferramenta principal de automação                 |
| ansible-lint               | 6.0+          | Analisador de boas práticas Ansible               |
| pip                        | 21.0+         | Gerenciador de pacotes Python                     |
| IBM watsonx Code Assistant | Última versão | Extensão IA (VS Code ou Red Hat Developer Hub)    |

---

## 🧰 Instalação (ambiente Linux/WSL recomendado)

### 1️⃣ Instalar Python e pip

```bash
sudo apt update
sudo apt install python3 python3-pip -y
```

### 2️⃣ Instalar Ansible e ansible-lint

```bash
pip3 install ansible ansible-lint
```

### 3️⃣ Instalar o Watsonx Code Assistant – Lightspeed

* Acesse: [https://cloud.ibm.com/watsonx/code-assistant](https://cloud.ibm.com/watsonx/code-assistant)
* Faça login com sua conta IBM Cloud
* Crie um espaço de implantação (**Deployment Space**)
* Ative o plano **Trial** ou **Enterprise L3**
* Gere uma **API Key IBM Cloud** (para autenticação no VS Code)

### 4️⃣ Configurar no VS Code

1. Instale a extensão **IBM watsonx Code Assistant – Lightspeed**

   * ID: `IBM.watsonx-code-assistant`
   * Permite gerar playbooks Ansible automaticamente com base em comentários.

2. Instale a extensão **Red Hat Ansible**

   * ID: `redhat.ansible`
   * Fornece suporte de sintaxe YAML, snippets e integração com o Lightspeed.

3. Configure sua **API Key IBM Cloud** nas configurações do Lightspeed.
   *(Command Palette → “Watsonx Code Assistant: Configure API Key”)*

4. Se estiver no **Windows**, abra o VS Code com **Remote WSL (Ubuntu)** para evitar erros de ambiente.

5. Crie um arquivo `.yml` e adicione comentários Ansible descritivos.
   Exemplo:

   ```yaml
   # Criar cluster ECS com Fargate e tags personalizadas
   ```

6. Clique em ⚡ **Generate with Lightspeed** para gerar o código automaticamente.

---

## 🧩 Estrutura típica de um playbook gerado

Exemplo:

```yaml
---
- name: ECS Cloud Operations
  hosts: localhost
  connection: local
  gather_facts: false

  vars:
    ecs_cluster:
      name: lightspeed-cluster
      capacity_providers: ["FARGATE", "FARGATE_SPOT"]

  tasks:
    # - name: Create ECS cluster using ecs_cluster var
```

O Lightspeed transforma esse comentário em:

```yaml
- name: Create ECS cluster using ecs_cluster var
  amazon.aws.ecs_cluster:
    name: "{{ ecs_cluster.name }}"
    capacity_providers: "{{ ecs_cluster.capacity_providers }}"
    state: present
```

---

## 🧠 Boas Práticas

* Sempre **defina variáveis em `vars:`** — o Lightspeed usa isso como contexto.
* Use **descrições específicas** (ex: “Provisionar serviço ECS com Fargate”).
* Mantenha o **ansible-lint instalado e no PATH** para validação automática.
* Se estiver no Windows, use o **WSL (Ubuntu)** para evitar erros como `No module named 'grp'` ou `Ansible not found`.
* Teste seus playbooks com:

  ```bash
  ansible-playbook seu_playbook.yml --check
  ```

---

## 🚑 Troubleshooting

| Erro                            | Causa                       | Solução                                                         |
| ------------------------------- | --------------------------- | --------------------------------------------------------------- |
| `No module named 'grp'`         | Execução no Windows sem WSL | Use o WSL Ubuntu                                                |
| `Ansible not found`             | PATH incorreto              | Adicione `/usr/local/bin` ao PATH                               |
| `Red Hat authentication failed` | Token expirado              | Gere novo token em [cloud.redhat.com](https://cloud.redhat.com) |
| `Invalid API key`               | Chave IBM incorreta         | Regere no portal IBM Cloud                                      |
| `Model_id`                      | Chave IBM model id incorreta         | Acessar o seu ambiente IBM e pegar o space guid dentro dos espaços de implementação|

---

## 🧾 Resumo

| Recurso        | Descrição                                                        |
| -------------- | ---------------------------------------------------------------- |
| **Produto**    | IBM watsonx Code Assistant – Lightspeed (L3)                     |
| **Finalidade** | Geração automatizada de código para Ansible e automação de nuvem |
| **Integração** | Red Hat Ansible, AWS, Kubernetes, IBM Cloud                      |
| **Nível L3**   | Recursos corporativos, modelos contextuais, sugestões avançadas  |
| **Benefício**  | Aumenta a produtividade, reduz erros e acelera o provisionamento |

---

📄 **By Diego Lins**
Engenheiro de Software | Especialista em Integrações AWS, .NET e Automação Ansible  
🔗 [IBM watsonx Code Assistant](https://cloud.ibm.com/watsonx/code-assistant)

