🟦 1. Launch EC2 Instance
Recommended Configuration:

AMI: Amazon Linux 2023

Type: t2.micro (Free Tier)

Security Group Rules:

Type	Port	Source
SSH	22	0.0.0.0/0
HTTP	80	0.0.0.0/0
HTTPS	443	0.0.0.0/0
Custom TCP	8080	0.0.0.0/0
🟦 2. Connect to EC2

From AWS Console:

EC2 → Instances → Select → Connect → EC2 Instance Connect

Terminal will open as:

ec2-user@ip-xx-xx-xx-xx

🟦 3. Update EC2 Machine
sudo dnf update -y

🟦 4. Install Java 17
sudo dnf install java-17-amazon-corretto -y


Verify:

java -version

🟦 5. Install Maven
sudo dnf install maven -y


Verify:

mvn -version

🟦 6. Install Git
sudo dnf install git -y


Verify:

git --version

🟦 7. Clone Your Maven Project
git clone https://github.com/<your-username>/<your-repo>.git
cd <your-repo>


Example:

git clone https://github.com/shashank1369/maven.git
cd maven

🟦 8. Build the WAR File
mvn clean package


WAR output:

target/*.war


If BUILD SUCCESS appears → continue.

🟦 9. Install Docker (Amazon Linux 2023)
1️⃣ Install Docker
sudo dnf install docker -y

2️⃣ Start Docker
sudo systemctl start docker

3️⃣ Enable Docker on boot
sudo systemctl enable docker

4️⃣ Add ec2-user to docker group
sudo usermod -aG docker ec2-user

5️⃣ Refresh group permissions
newgrp docker

6️⃣ Verify Docker
docker --version

🟦 10. Build Docker Image

Make sure the Dockerfile exists in the project root.

docker build -t mywebapp .

🟦 11. Run Docker Container

Expose port 8080:

docker run -d -p 8080:8080 --name mycontainer mywebapp


Check if container is running:

docker ps


Expected:

mycontainer   Up X seconds

🟦 12. Access the Web Application

Open browser:

http://<YOUR-EC2-PUBLIC-IP>:8080/


Example:

http://13.220.90.161:8080/


Your app should now load successfully.

🟦 13. Common Commands
Stop container:
docker stop mycontainer

Start container:
docker start mycontainer

Remove container:
docker rm mycontainer

View logs:
docker logs mycontainer

🟦 14. Auto-Restart on Reboot

(Optional but useful)

docker update --restart unless-stopped mycontainer
