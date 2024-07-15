# Notas App

Este proyecto es una aplicación básica de notas creada con Ruby on Rails. A continuación se describen los pasos para configurar el entorno de desarrollo en una máquina con Linux Mint.

## Instalación

1. **Actualizar el sistema**:
    ```bash
    sudo apt update && sudo apt upgrade -y
    ```

2. **Instalar dependencias**:
    ```bash
    sudo apt install -y curl gnupg2 build-essential libssl-dev libreadline-dev zlib1g-dev git
    ```

3. **Instalar rbenv y ruby-build**:
    ```bash
    git clone https://github.com/rbenv/rbenv.git ~/.rbenv
    echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
    echo 'eval "$(rbenv init -)"' >> ~/.bashrc
    exec $SHELL
    git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
    echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.bashrc
    exec $SHELL
    ```

4. **Instalar Ruby 3.0.1**:
    ```bash
    rbenv install 3.0.1
    rbenv global 3.0.1
    ```

5. **Instalar Node.js y Yarn**:
    ```bash
    curl -sL https://deb.nodesource.com/setup_20.x | sudo -E bash -
    sudo apt install -y nodejs
    npm install --global yarn
    ```

6. **Instalar Rails**:
    ```bash
    gem install rails -v 6.1.3.2
    rbenv rehash
    ```

7. **Clonar la aplicacion Rails**:
    ```bash
    git clone https://github.com/grupopetsa/notes-app
    cd notes-app
    bundle install
    rails webpacker:install
    ```

8. **Configurar Docker**:
    Crear un archivo `Dockerfile` con el siguiente contenido:
    ```dockerfile
    FROM ruby:3.0.1-buster

    WORKDIR /app

    RUN curl -sL https://deb.nodesource.com/setup_20.x | bash -

    RUN apt-get update -y && apt-get install -y nodejs

    RUN npm install --global yarn

    COPY Gemfile* ./

    RUN bundle install

    COPY . .

    RUN rails webpacker:install

    CMD ["rails", "db:setup"]
    ```

9. **Inicializar la base de datos**:
    ```bash
    rails db:setup
    ```

10. **Iniciar el servidor Rails**:
    ```bash
    rails server
    ```

## Solución de Problemas

- **Si el puerto 3000 ya está en uso**:
    ```bash
    lsof -i :3000
    kill -9 <PID>
    ```

Con estos pasos, deberías tener un entorno de desarrollo Ruby on Rails completamente funcional en tu máquina con Linux Mint.

---

Desarrollador Javier Ivan Valenzuela Esparza.
