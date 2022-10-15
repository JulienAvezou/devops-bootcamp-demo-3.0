Demo project for Module 7 - Docker

Steps taken to complete demo:

1. Clone remote repo for the project and push to this repo (so we can have quick access to the code for reference)

2. Download Docker images for running mongoDB and mongo-express (UI)
docker pull mongo
docker pull mongo-express

3. Create new network for running mongoDB and mongo-express
create network -> docker network create mongo-network
check network was created -> docker network ls
<img width="396" alt="Capture d’écran 2022-10-15 à 18 42 30" src="https://user-images.githubusercontent.com/62488871/195998098-dc03d071-051f-4e9e-b801-c74b66509fc8.png">

4. Run mongoDB container
docker run -p 27017:27017 -d -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=password --name mongo --net mongo-network mongo

5. Run mongo-express container and connect it to mongoDB
docker run -d -p 8081:8081 -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin -e ME_CONFIG_MONGODB_ADMINPASSWORD=password --net mongo-network --name mongo-express -e ME_CONFIG_MONGODB_SERVER=mongo mongo-express

6. Connect node server with mongoDB container
<img width="554" alt="Capture d’écran 2022-10-15 à 19 07 59" src="https://user-images.githubusercontent.com/62488871/195999139-741587f7-8934-4381-b1d6-04d21811b0cb.png">
<img width="1175" alt="Capture d’écran 2022-10-15 à 19 08 16" src="https://user-images.githubusercontent.com/62488871/195999153-691ce01c-7553-4589-9462-a35cd0054e49.png">

7. Run containers this time using docker compose file, test it works, then stop containers using docker compose cmd
docker-compose -f docker-compose.yaml up
docker-compose -f docker-compose.yaml down

8. Build app using Docker image file
create the file
docker build -t my-app:1.0 .
<img width="454" alt="Capture d’écran 2022-10-15 à 20 11 32" src="https://user-images.githubusercontent.com/62488871/196001865-eaf64bed-7d4a-4a67-8e44-57e34d118be0.png">

9. Run newly built image above
<img width="470" alt="Capture d’écran 2022-10-15 à 20 18 12" src="https://user-images.githubusercontent.com/62488871/196002134-1d0446db-c74b-49ea-95fd-52b7f9ead8c0.png">

10. Create repository for Docker image with AWS ECR
<img width="1073" alt="Capture d’écran 2022-10-15 à 21 29 45" src="https://user-images.githubusercontent.com/62488871/196004605-c907651d-7073-43ea-899b-6f105e63dc0c.png">

11. Tag and push image to the repository on AWS
docker tag my-app:latest 395901524773.dkr.ecr.eu-central-1.amazonaws.com/my-app:latest
docker push 395901524773.dkr.ecr.eu-central-1.amazonaws.com/my-app:1.0
<img width="1094" alt="Capture d’écran 2022-10-15 à 21 37 49" src="https://user-images.githubusercontent.com/62488871/196004847-a04258c4-04d2-41f5-9523-1ea596199c87.png">

12. Make change in code, rebuild image and push that img version to repo
<img width="1125" alt="Capture d’écran 2022-10-15 à 21 43 37" src="https://user-images.githubusercontent.com/62488871/196005024-222554aa-c2fd-4a9f-8b2e-93bfd064e0b3.png">
