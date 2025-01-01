[![FrankenPHP Worker Mode](https://img.youtube.com/vi/VgQHVl2F2zE/0.jpg)](https://www.youtube.com/watch?v=VgQHVl2F2zE)

1.  Install Docker
    ```
    # Referensi: https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository

    sudo apt-get update
    sudo apt-get install ca-certificates curl
    sudo install -m 0755 -d /etc/apt/keyrings
    sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
    sudo chmod a+r /etc/apt/keyrings/docker.asc

    # Add the repository to Apt sources:
    echo \
        "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
        $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
        sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    sudo apt-get update
    sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
    ```

2.  Menjalankan FrankenPHP mode runtime biasa
    ```
    sudo docker run \
        -d --restart always \
        --name test \
        -e "SERVER_NAME=:80" \
        -v /home/ubuntu/test:/app/public \
        -p 80:80 \
        dunglas/frankenphp
    ```

3.  Menjalankan FrankenPHP mode worker
    ```
    sudo docker run -d \
        --restart always \
        --name worker \
        -e "SERVER_NAME=:80" \
        -v /home/ubuntu/worker:/app \
        -e "worker /home/ubuntu/worker/public/frankenphp-worker.php" \
        -p 81:80 \
        dunglas/frankenphp
    ```

4.  Menjalankan FrankenPHP dengan PHP versi sebelumnya
    ```
    sudo docker run \
        -d --restart always \
        --name lama \
        -e "SERVER_NAME=:80" \
        -v /home/ubuntu/test:/app/public \
        -p 82:80 \
        dunglas/frankenphp:php8.2-alpine
    ```

# Xenara Cafe and Coworking Space
Ruko Citra Grand, Blok LONDON C-08, Semarang, Jawa Tengah, Indonesia 50276
