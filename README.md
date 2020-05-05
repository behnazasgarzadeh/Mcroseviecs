!cd && git clone https://github.com/callistaenterprise/blog-microservices.git
!cd && cd blog-microservices && git checkout -b B1 M1.1
!cd && wget https://www.dropbox.com/s/wbtq48x3fj9uuf2/install-java8.bash
!cd && chmod 755 install-java8.bash
!cd &&./install-java8.bash
!cd && cd blog-microservices && nohup ./build-all.sh>out 2>&1 &
!cd && cd blog-microservices/microservices && cd support/discovery-server; nohup ./gradlew bootRun >out 2>&1 &
!cd && cd blog-microservices/microservices && cd support/edge-server; nohup ./gradlew bootRun >out 2>&1 &
!cd && cd blog-microservices/microservices && cd core/product-service; nohup ./gradlew bootRun >out 2>&1 &
!cd && cd blog-microservices/microservices && cd core/recommendation-service; nohup ./gradlew bootRun >out 2>&1 &
!cd && cd blog-microservices/microservices && cd core/review-service; nohup ./gradlew bootRun >out 2>&1 &
!cd && cd blog-microservices/microservices && cd composite/product-composite-service; nohup ./gradlew bootRun >out 2>&1 &
#python code for run web application on google colap
#you should login in ngrok
!wget https://bin.equinox.io/c/4VmDzA7iaHb/ngrok-stable-linux-amd64.zip
!unzip ngrok-stable-linux-amd64.zip 
get_ipython().system_raw('./ngrok http 8761 &')
!curl -s http://localhost:4040/api/tunnels | python3 -c "import sys, json; print(json.load(sys.stdin)['tunnels'][0]['public_url'])"
