# 3 Tier AWS Project

This project is a full-stack web application built using React js for the frontend, Express js for the backend, and MySQL as the database. The application is designed to demonstrate the implementation of a 3-tier architecture, where the presentation layer (React js), application logic layer (Express js), and data layer (MySQL) are separated into distinct tiers.


## Application UI Screenshots 
#### Dashboard
![Dashboard](./frontend/public/ss/dashboard.png)

#### Books
![Dashboard](./frontend/public/ss/books.png)

#### Authors
![Dashboard](./frontend/public/ss/authors.png)

## STEP 1: Setting up Application Tier

## STEP 2: Setting up the Data Tier
#### Install MySQL

1. Create RDS MySQL Database by selecting the Free Tier option and set the password
   Ensure to store the password, to later configure in Application Tier
   
2. To Install MySQL mysql cli package:

```bash
sudo yum install -y mariadb
```

3. To verify the package is installed:

```bash
which mysql
```

4. Login to MySQL CLI, replace the RDS Host and username from the RDS Console, password will be asked on prompt

```bash
mysql -h <RDS Host> -P 3306 -u <username> -p
```

5. Once successfully logged in, you will see the below message

```bash
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 9738
Server version: 8.0.28 Source distribution

Type 'help;' or '\h' for help. Type '\c' to clear the buffer.

mysql>
```

3. Run each commands in the MQSQL:

```bash
CREATE DATABASE react_node_app; 
CREATE USER 'appuser'@'%' IDENTIFIED BY 'learnIT02#'; 
GRANT ALL PRIVILEGES ON react_node_app.* TO ' appuser'@'%'; 
FLUSH PRIVILEGES;

CREATE TABLE `author` ( 
  `id` int NOT NULL AUTO_INCREMENT, 
  `name` varchar(255) NOT NULL, 
  `birthday` date NOT NULL, 
  `bio` text NOT NULL, 
  `createdAt` date NOT NULL, 
  `updatedAt` date NOT NULL, 
  PRIMARY KEY (`id`) 
) ENGINE=InnoDB AUTO_INCREMENT=8 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;

CREATE TABLE `book` ( 
  `id` int NOT NULL AUTO_INCREMENT, 
  `title` varchar(255) NOT NULL, 
  `releaseDate` date NOT NULL, 
  `description` text NOT NULL, 
  `pages` int NOT NULL, 
  `createdAt` date NOT NULL, 
  `updatedAt` date NOT NULL, 
  `authorId` int DEFAULT NULL, 
  PRIMARY KEY (`id`), 
  KEY `FK_66a4f0f47943a0d99c16ecf90b2` (`authorId`), 
  CONSTRAINT `FK_66a4f0f47943a0d99c16ecf90b2` FOREIGN KEY (`authorId`) REFERENCES `author` (`id`) 
) ENGINE=InnoDB AUTO_INCREMENT=10 DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci; 
```

3. Switch to author table and add data:

```bash
USE author;

INSERT INTO `author` VALUES (1,'J.K. Rowling (Joanne Kathleen Rowling)','1965-07-31','J.K. Rowling is a British author best known for writing the Harry Potter fantasy series. The series has won multiple awards and sold over 500 million copies, becoming the best-selling book series in history. Rowling has also written other novels, including The Casual Vacancy and the Cormoran Strike crime series under the pen name Robert Galbraith.','2024-05-29','2024-05-29'),(3,'Jane Austen','1775-12-16','Jane Austen was an English novelist known for her wit, social commentary, and romantic stories. Her six major novels, which explore themes of love, marriage, and money, have earned her a place as one of the greatest writers in the English language.','2024-05-29','2024-05-29'),(4,'Harper Lee','1960-07-11','Harper Lee was an American novelist best known for her Pulitzer Prize-winning novel To Kill a Mockingbird. The novel explores themes of racial injustice and the importance of compassion. Lee published a sequel, Go Set a Watchman, in 2015.','2024-05-29','2024-05-29'),(5,'J.R.R. Tolkien','1954-07-29','J.R.R. Tolkien was a British philologist and writer best known for his fantasy novels The Hobbit and The Lord of the Rings. Tolkien\'s works have had a profound influence on the fantasy genre and popular culture.','2024-05-29','2024-05-29'),(6,'Mary Shelley','1818-03-03','Mary Shelley was a British novelist, playwright, and short story writer, the daughter of Mary Wollstonecraft Godwin and the wife of poet Percy Bysshe Shelley. Frankenstein, or, The Modern Prometheus (1818) is her most famous work.','2024-05-29','2024-05-29'),(7,'Douglas Adams','1979-10-12','Douglas Adams was an English science fiction writer, satirist, humorist, dramatist, screenwriter, and occasional actor. He is best known for the Hitchhiker\'s Guide to the Galaxy comedy series, which inspired a radio comedy, several books, stage shows, comic books, a 1981 TV series, a 1984 video game, a 2005 feature film, and a 2008 sequel film.','2024-05-29','2024-05-29'); 

```

3. Switch to books table and add data:

```bash
USE books;

INSERT INTO `book` VALUES (1,'Harry Potter and the Sorcerer\'s Stone','1997-07-26','On his birthday, Harry Potter discovers that he is the son of two well-known wizards, from whom he has inherited magical powers. He must attend a famous school of magic and sorcery, where he establishes a friendship with two young men who will become his companions on his adventure. During his first year at Hogwarts, he discovers that a malevolent and powerful wizard named Voldemort is in search of a philosopher\'s stone that prolongs the life of its owner.',223,'2024-05-29','2024-05-29',1),(3,'Harry Potter and the chamber of secrets','1998-07-02','Harry Potter and the sophomores investigate a malevolent threat to their Hogwarts classmates, a menacing beast that hides within the castle.',251,'2024-05-29','2024-05-29',1),(4,'Pride and Prejudice','1813-01-28','An English novel of manners by Jane Austen, first published in 1813. The story centres on the relationships among the Bennet sisters, in particular Elizabeth Bennet the middle daughter, and the wealthy Mr. Darcy. Austen satirizes the social classes of the English gentry through a witty and ironic narrative voice.',224,'2024-05-29','2024-05-29',3),(5,'Harry Potter and the Prisoner of Azkaban','1999-07-08','Harry\'s third year of studies at Hogwarts is threatened by Sirius Black\'s escape from Azkaban prison. Apparently, it is a dangerous wizard who was an accomplice of Lord Voldemort and who will try to take revenge on Harry Potter.',317,'2024-05-29','2024-05-29',1),(6,'Harry Potter and the Goblet of Fire','2000-07-08','Hogwarts prepares for the Triwizard Tournament, in which three schools of wizardry will compete. To everyone\'s surprise, Harry Potter is chosen to participate in the competition, in which he must fight dragons, enter the water and face his greatest fears.',636,'2024-05-29','2024-05-29',1),(7,'The Hitchhiker\'s Guide to the Galaxy','1979-10-12','A comic science fiction comedy series created by Douglas Adams. The story follows the comedic misadventures of Arthur Dent, a hapless Englishman, following the destruction of the Earth by the Vogons, a race of unpleasant bureaucratic aliens. Arthur escapes with his friend Ford Prefect, who reveals himself to be an undercover researcher for the titular Hitchhiker\'s Guide to the Galaxy, a galactic encyclopedia containing information about anything and everything.',184,'2024-05-29','2024-05-29',7),(8,'Frankenstein; or, The Modern Prometheus','1818-03-03','A Gothic novel by Mary Shelley that tells the story of Victor Frankenstein, a young scientist who creates a grotesque creature in an unorthodox scientific experiment. Frankenstein is horrified by his creation and abandons it, but the creature seeks revenge. The novel explores themes of scientific responsibility, creation versus destruction, and the nature of good and evil.',211,'2024-05-29','2024-05-29',6),(9,'The Lord of the Rings: The Fellowship of the Ring','1954-07-29','The first book in J.R.R. Tolkien\'s epic fantasy trilogy, The Lord of the Rings. The Fellowship of the Ring follows hobbit Frodo Baggins as he inherits the One Ring, an evil artifact of power created by the Dark Lord Sauron. Frodo embarks on a quest to destroy the Ring in the fires of Mount Doom, accompanied by a fellowship of eight companions.',482,'2024-05-29','2024-05-29',5); 
```

## STEP 3: Setting up the Presentation Tier

## Connecting to private EC2 instance via a bastion host
1. To change the ssh key permission:

```bash
chmod 400 your_key.pem
```

2. To start ssh agent:

```bash
eval "$(ssh-agent -s)"  
```

3. To add key to ssh agent:

```bash
ssh-add your_key.pem
```

4. To ssh into bastion host with agent forwarding:

```bash
ssh -A ec2-user@bastion_host_public_ip
```

5. To connect private instance from the bastion host:

```bash
ssh ec2-user@private_instance_private_ip 
```

## Setting up the Application Tier
#### Install GIT
```bash
sudo yum update -y

sudo yum install git -y

git — version
```

#### Clone repository
```bash
git clone https://github.com/learnItRightWay01/react-node-mysql-app.git
```

#### Install node.js
1. To install node version manager (nvm)
```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
```

2. To load nvm
```bash
source ~/.bashrc
```

3. To use nvm to install the latest LTS version of Node.js
```bash
nvm install --lts
```

4. To test that Node.js is installed and running
```bash
node -e "console.log('Running Node.js ' + process.version)"
```

## Setting up the Presentation Tier
#### Install GIT
```
PLEASE REFER ABOVE
```

#### Clone repository
```
PLEASE REFER ABOVE
```

#### Install node.js
```
PLEASE REFER ABOVE
```

#### Install NGINX
```bash
dnf search nginx

sudo dnf install nginx

sudo systemctl restart nginx 

nginx -v
```

#### Copy react.js build files
```bash
sudo cp -r dist /usr/share/nginx/html 
```

#### Update NGINX config
1. Server name and root
```
server_name    domain.com www.subdomain.com
root           /usr/share/nginx/html/dist
```

2. Setup reverse proxy
```
location /api { 
   proxy_pass http://application_tier_instance_private_ip:3200/api; 
}
```

3. Restart NGINX
```
sudo systemctl restart nginx
```

## User data scripts
#### Install NGINX
For [AWS solutions - 06](https://youtu.be/snQlL0fJI3Q) and  [AWS solutions - 07](https://youtu.be/eRX1FI2cFi8)

```bash
#!/bin/bash 
# Update package lists 
yum update -y 

# Install Nginx 
yum install -y nginx 

# Stop and disable default service (optional) 
systemctl stop nginx 
systemctl disable nginx 

# Create a custom welcome message file 
echo "Welcome to Presentation Tier EC2 instance in Availability Zone B." > /usr/share/nginx/html/index.html 

# Start and enable the Nginx service 
systemctl start nginx 
systemctl enable nginx
```
