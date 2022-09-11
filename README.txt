Installing Docker on Amazon Linux 2

root-user = sudo -i
1. sudo yum update
2. sudo yum search docker
3. sudo yum info docker
4.sudo yum install docker
5.docker --version

Now we install docker-compose, run 
1. sudo curl -L https://github.com/docker/compose/releases/download/1.21.0/docker-compose-`uname -s`-`uname -m` | sudo tee /usr/local/bin/docker-compose > /dev/null
2. sudo chmod +x /usr/local/bin/docker-compose
3. ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
4. docker-compose --version

Running Jenkins With Docker Compose
You can run a Jenkins controller with a single Docker command:
docker run -it -p 8080:8080 jenkins/jenkins:lts
That will give you a running Jenkins controller. You can set it up,
log in, and start running jobs. But if you restart it, you will lose all your data.
You need to set up a volume to start the Jenkins instance data.

Create a directory named jenkins_compose and create a file named docker-compose.yaml with these contents.

version: '3.3'
services:
  jenkins:
    image: jenkins/jenkins:lts
    privileged: true
    user: root
    ports:
      - 8080:8080
      - 50000:50000
    container_name: jenkins
    volumes:
      - /ec2-user/jenkins_compose/jenkins_configuration



after this save it and run jenkins controller
1. docker-compose up -d

Now point a web browser at port 8080 on your host system. You’ll see the unlock page.
to Unlock Jenkins password
run this commend
1. docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword

now we creat our user.

for working with a GitHub repository we install github
1. sudo yum update -y
2. sudo yum install git -y
3. git version

now we make a ssh-key
1. cd ~/.ssh
2. ssh-keygen -o -t rsa -C "your@email.com"

and press enter
for show this key
1. cat ~/.ssh/id_rsa.pub

and put him in https://github.com/settings/keys

