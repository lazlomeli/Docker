app / db

docker run --name app --network=nw -v volumes:/var/www/html -p 8000:80 app_img
docker run --name db --network=nw --volumes-from datastore db_img
