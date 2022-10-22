# Installation:

## Windows:

- Windows-Features: activate Windows-Subsystem for Linux
- Update auf WSL2 Download: https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi
- Check WSL Version in Terminal: wsl -l -v
- Set Default Version to 2: wsl --set-default-version 2
- Set Default Distribution: wsl --setdefault Ubuntu
- Set Distribution Version: wsl --set-version Ubuntu 2
- Install Ubuntu from MS-Store: https://apps.microsoft.com/store/detail/ubuntu-20045-lts/9MTTCL66CPXJ
- Install Docker-Desktop for Windows: https://docs.docker.com/desktop/install/windows-install/
- Install Docker-Compose for Windows: https://docs.docker.com/compose/install/

## Check Linux
- Explorer Path WSL: \\wsl$
- Explorer Path WSL Ubuntu: \\wsl$\Ubuntu
- Explorer Path WSL Ubuntu User: \\wsl$\Ubuntu\home\your_user_name

## Folder for Docker:
- Create a subfolder in the UserFolder: web_projects
- Create a subfolder in web_projects for Docker Setups: php_8_1_dev
- Copy this GIT-Zip in this folder

## Docker Prompts:
docker-compose -f apache.yml up --no-start

docker-compose -f apache.yml up --build --no-start

docker-compose -f apache.yml up --build --no-start --force-recreate

docker-compose -f apache.yml exec php bash