# 3days_Documentation
1)Docker installation.
  a)From docks.docker.com we have downloaded docker(https://docs.docker.com/docker-for-windows/install/).
  b)After downloaded we got error while installing (Docker desktop requires server services to be enabled)
  https://www.bing.com/videos/search?view=detail&mid=C12FF81E191DA0CA296AC12FF81E191DA0CA296A&q=docker from using this reference we rectified error.
   steps for error rectification->in serch type services.msc -> server -> automatic/Manual
  
 2)Creating ubuntu image(http://www.servermom.org/pull-docker-images-run-docker-containers/3225/#:~:text=To%20pull%20an%20image%2C%20use%20%E2%80%9C%20docker%20pull,your%20server%2C%20use%20%E2%80%9C%20docker%20images%20%E2%80%9D%20command)
  open cmd prompt-> docker pull ubuntu 
                 ->docker ps -l 
				 ->docker run -i -t ubuntu /bin/bash
 
 3)setup python notebook
   a)Installing python->https://www.datasciencelearner.com/install-and-run-python-in-docker-container/
     ->running ubuntu->docker run -ti -d ubuntu: latest
	 ->To get images ->docker ps 
	 ->Updating ubuntu to latest version ->apt-get update
	 ->Install python ->apt-get install python3
	 ->apt-get install python3
4)open ubuntu in docker and then clc there we have to give
     1.sudo ls
     2.su -
     3.apt-get update
     4.apt-get install sudo
     5.sudo ls
     6.sudo apt update
     7.sudo apt install python3-pip python3-dev
     8.it will asks do you want to continue [y/n] we should give y to install
     9.sudo -H pip3 install --upgrade pip
     10.sudo -H pip3 install virtualenv
     11.mkdir ~/myproject_dir
     12.cd ~/myproject_dir
     13.virtualenv myproject_env
     14.source myproject_env/bin/activate
     15.pip install jupyter
     ****jupyter notebook,--allow-root,jupyter notebook --no-browser --port=8888,local:8888****these r used but got errors
     16.jupyter notebook --allow-root then we got
7)ctrl+c
5)open cmd prompt
     1)ssh -L 8888:localhost:8888 root@97e384798831
     2)docker run -p 8888:8888 jupyter
     3)docker run -p 8888:8888 jupyter/minimal-notebook
After that will get localhost link then we have to copy and past that code in browser .

______________________________________________________________________________________________________________________________
--------TODAYTASK(4-8-21)--------------
1)Read a pdf in jupyter notebook
2)Do OCR
3)create a file

Read pdf in jupyter notebook
# importing required modules
import PyPDF2
 
# creating a pdf file object      =>we should give pdf name as File and have to upload that pdf in jupyter notebook
pdfFileObj = open('File.pdf', 'rb')
 
# creating a pdf reader object
pdfReader = PyPDF2.PdfFileReader(pdfFileObj)
 
# printing number of pages in pdf file
print(pdfReader.numPages)
 
# creating a page object
pageObj = pdfReader.getPage(0)
 
# extracting text from page
print(pageObj.extractText())
 
# closing the pdf file object
pdfFileObj.close()
refernce link:-https://www.geeksforgeeks.org/working-with-pdf-files-in-python/#:~:text=1%20Extracting%20text%20from%20PDF%20file%20Python%20Python,in%20...%205%20Adding%20watermark%20to%20PDF%20pages

# closing the pdf file object
pdfFileObj.close()
refernce link:-https://www.geeksforgeeks.org/working-with-pdf-files-in-python/#:~:text=1%20Extracting%20text%20from%20PDF%20file%20Python%20Python,in%20...%205%20Adding%20watermark%20to%20PDF%20pages

import os
os.getcmd() => to get know file directory path

Postgres:
1.docker pull postgres     //pulls latest image
2.docker run --name some-postgres -e POSTGRES_PASSWORD=mysecretpassword -d postgres     //run the image(it downloads if not present)
3.docker exec -it some-postgres bash     //connect to the container //opens in root
4.su postgres                //change user to postgres
5.psql                    //run sql
6.\conninfo
7.\q                    //to quit

 


 

1.docker network ls                               //displays all the network which is present
2.docker network create --driver driver_name network_name        //creates a new network
  ->docker network create --driver bridge new_network

 

Connect a new container:            //using bridge
3.docker run -it --network=new_network ubuntu:latest /bin/bash        //creates ubuntu in the network we created

 

4.docker run -it --network=new_network --name faz_postgres -e POSTGRES_PASSWORD=mysecretpassword -d postgres    //creates postgres in the network we created

 

5.docker inspect new_network             //inspect the network to check if containers are attached
                        // conatiners will be attached to network.
Connect a running container to a newwork:
docker network connect network-name container-name

 


Connecting jupyter to postgres (https://medium.com/analytics-vidhya/postgresql-integration-with-jupyter-notebook-deb97579a38d)

 

import psycopg2  
import pprint

 

conn = psycopg2.connect("postgres://postgres:mysecretpassword@172.17.0.3:5432/postgres")

 

ERROR:
//To find ip address -> docker inspect container_name   (Find ip)
//To find user name  -> \conninfo   

 


Working SQL commands:
!pip install ipython-sql
%load_ext sql
%sql sqlite://

 


CREATE TABLE AND INSERTING:(https://www.datacamp.com/community/tutorials/sql-interface-within-jupyterlab)
%%sql
CREATE TABLE EMP(firstname varchar(50),lastname varchar(50));
INSERT INTO EMP VALUES('tom','Mitchell');
INSERT INTO EMP VALUES('jack','ryan');
INSERT INTO EMP VALUES('kim','taehyung');
INSERT INTO EMP VALUES('kim','namjoon');

 

%sql SELECT * from EMP;
