# Projeto dotProject# criado para visualização da comunidade 

Este repositório contém o código-fonte referente ao Trabalho de Conclusão de Curso (TCC) desenvolvido por **Bruno Coelho Ribas**. O projeto foca na modernização da ferramenta de gestão de projetos **dotProject**, com ênfase no aprimoramento do módulo de Recursos Humanos para alinhamento com as práticas do PMBOK v7. 

A aplicação foi migrada de sua arquitetura legada para um ambiente moderno e escalável, utilizando **PHP 8.4** e o framework **Laravel 12**, com interface atualizada via **Tailwind CSS**.

---

## Tecnologias Utilizadas

Para garantir a estabilidade e replicabilidade do ambiente, o projeto foi encapsulado em uma Máquina Virtual (VM) atuando como servidor web.

* **Sistema Operacional:** Debian 13 (Trixie)
* **Servidor Web:** Nginx
* **Linguagem:** PHP 8.4 (via PHP-FPM)
* **Framework:** Laravel 12
* **Banco de Dados:** MariaDB / MySQL
* **Frontend:** Tailwind CSS

---

## Acesso à Máquina Virtual (Appliance)

Para facilitar a avaliação e os testes, todo o ambiente já configurado (Servidor Web, Banco de Dados, Dependências e Código) está disponível em uma imagem de Máquina Virtual pré-configurada para o **VirtualBox**.

**Link para download da VM:** (https://ifcedubr-my.sharepoint.com/:u:/g/personal/bruno_ribas_estudantes_ifc_edu_br/IQBcA36q9bRLSLToaPpbP3TPAUdRSrv9gSuN7aHAeDIvi6I?e=M0Nh8B)

**Atenção:** Baixe o arquivo `.rar`, extraia o seu conteúdo e você encontrará o arquivo `.ova` (Appliance do VirtualBox).

---

## Como Rodar a Aplicação

Siga os passos abaixo para iniciar o sistema em qualquer computador:

1. **Instale o VirtualBox:** Certifique-se de ter o [VirtualBox](https://www.virtualbox.org/) instalado em sua máquina.
2. **Importe a VM:**
   * Abra o VirtualBox.
   * Vá em `Arquivo` > `Importar Appliance...` (ou pressione `Ctrl+I`).
   * Selecione o arquivo `.ova` que você extraiu.
   * Avance e clique em "Finalizar" para concluir a importação.
3. **Inicie o Servidor:**
   * Selecione a máquina virtual "debian13-server" na lista e clique em **Iniciar**.
   * Aguarde a tela preta de terminal do Debian carregar e pedir o login. *Você não precisa fazer login no terminal, o servidor web já inicia automaticamente em segundo plano.*
4. **Acesse o Sistema:**
   * A rede da VM está configurada em NAT com Redirecionamento de Portas.
   * Abra o navegador de sua preferência (no seu próprio computador) e acesse:
     **`http://localhost:8080`**

---

## Credenciais Padrão

Caso precise acessar os recursos internos, utilize as seguintes credenciais:

**Acesso ao Sistema (dotProject):**
* **Usuário:** `admin`
* **Senha:** `passwd`

**Acesso interno à VM Debian (Terminal):**
* **Usuário:** `root`
* **Senha:** ``

**Acesso ao Banco de Dados (MariaDB na VM):**
* **Banco:** `dotprojectplus_2025`
* **Usuário:** `root`
* **Senha:** ``

---

## Resolução de Problemas (Troubleshooting)

Caso encontre alguma dificuldade ao rodar a aplicação, verifique os pontos abaixo:

### 1. A página não carrega ("Não é possível acessar esse site")
* Verifique se a Máquina Virtual está ligada e rodando no VirtualBox.
* Certifique-se de estar acessando pela porta correta: `http://localhost:8080`.
* Se a porta `8080` já estiver sendo usada por outro programa no seu computador (como um Tomcat ou outro servidor local), você pode alterar o redirecionamento:
  * Vá nas configurações da VM no VirtualBox > `Rede` > `Avançado` > `Redirecionamento de Portas` e altere a "Porta do Hospedeiro" para `8081`, por exemplo (acessando via `http://localhost:8081`).

### 2. Erro 500 ou Tela Vermelha do Laravel (Base table or view not found)
* Isso geralmente indica que o Laravel não encontrou a tabela de sessões. Para rodar a aplicação sem precisar do banco de dados para sessões, os arquivos estão configurados para `SESSION_DRIVER=file` no arquivo `.env`. 
* Se o erro persistir, limpe o cache acessando a VM e rodando: 
  `sudo -u www-data php artisan config:clear` na pasta `/var/www/dotproject`.

### 3. A tela de login abriu, mas não consigo acessar (Usuário inválido)
* O banco de dados estrutural está presente, mas se for o primeiro acesso após a importação de uma estrutura limpa (Forward Engineering), pode não haver usuários. O usuário `admin` e a senha `123456` foram injetados para testes, verifique se foram importados corretamente.

### 4. Layout "quebrado" ou sem estilo
* O Laravel utiliza Tailwind CSS. Se os assets não estiverem compilados, acesse a pasta do projeto dentro da VM e rode o comando de build:
  `cd /var/www/dotproject && npm run build`
