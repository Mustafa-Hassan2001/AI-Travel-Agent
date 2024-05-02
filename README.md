# AI Travel Agent with MariaDB, FastAPI, Next.js, & MindsDB

Transform a dataset into a predictive AI model that recommends the best flight based on the route selected.

Topics covered:
- Using AWS EC2, deploy Docker-based MariaDB Instance
- Aggregate Kaggle-based dataset via Python Pandas
- Load a dataset via Pandas and Jupyter to MariaDB
- Connect MariaDB to MindsDB
- Train two forecasting models within MindsDB
    - housing prices
    - flight prices
- Use SQL to run predictions in MindsDB Console
- Connect MariaDB with FastAPI, SQLAlchemy, and Pydantic
- Connect FastAPI to NextJS
- Build forms and routes with Next.js and App Router
- Craft UI elements with TailwindCSS and Flowbite
- Build Reusable Airport-select React/Next Client Component
- Connect FastAPI to MindsDB for SQL via Rest API
- Generate Synthetic Data with Gretel.ai

### Services used
⦿ MariaDB: https://mariadb.com/

⦿ MindsDB: https://mindsdb.com/

⦿ Gretel: https://gretel.ai

⦿ OpenAI: https://openai.com/

⦿ AWS EC2: https://aws.amazon.com/ec2/

### Software used
⦿ MariaDB Docker Image: https://hub.docker.com/_/mariadb

⦿ Docker Engine: https://docs.docker.com/engine/

⦿ Python: https://www.python.org/

⦿ Node.js: https://nodejs.org/en

⦿ FastAPI: https://fastapi.tiangolo.com/

⦿ Next.js: https://nextjs.org/

⦿ Pandas: https://pandas.pydata.org/

⦿ Jupyter Notebooks: https://jupyter.org/

⦿ Pydandtic: https://docs.pydantic.dev/latest/

## Lesson Reference
Each Git branch corresponds to the start and end of a section when it makes sense to do so. For example, section 33 starts at Branch `33-start` and ends with branch `33-end`. These branches exist for your reference where main branch has the latest code.

## Install Docker & Docker Compose

Enter you EC2 Instance
```
ssh -i your-private-key.pem ubuntu@<your-ec2-instance-public-ip>
```

Escalate to Root
```
sudo su
```

Install Docker
```
curl -fsSL https://get.docker.com | sudo sh
```


## Create secrets with Python

```bash
python3 -c "import secrets;print(secrets.token_urlsafe(32))"
```


## Five Steps to Launch a Docker-based MariaDB Instance on AWS EC2

### Step 1 Create an AWS EC2 Instance. 
Ensure the security groups are setup correctly to allow port 3306 access for MariaDB.

### Step 2: Install Docker Compose
SSH into EC2 Instance with your private key and the `ubuntu` user:

```bash
ssh -i your-private-key.pem ubuntu@<your-ec2-instance-public-ip>
```
Once complete, install Docker Compose as written above.

### Step 3: Setup MariaDB Root User Password

On the EC2 instance create the `.env` add the following line with your own password:

```bash
MARIADB_ROOT_PASSWORD=your-secret-password
```

Such as:

```bash
echo "MARIADB_ROOT_PASSWORD=$(python3 -c 'import secrets;print(secrets.token_urlsafe(32))')" >> .env
```

### Step 4: Run MariaDB with Docker Compose

Copy the contents of [config/compose.yaml](./config/compose.yaml) file to your EC2 instance to run MariaDB with:
```bash
curl https://raw.githubusercontent.com/codingforentrepreneurs/ai-travel-agent/main/config/compose.yaml -o compose.yaml
docker compose -f compose.yaml up -d
```

### Step 5: Connection String to MariaDB
Make note of the EC2 instance public IP address so you can re-use it anywhere with the following database connection string:
```bash
mariadb://root:your-secret-password@<your-ec2-instance-public-ip>:3306
```
