
# VARIÁVEIS DE AMBIENTE

#### **docker/.env:**

JWT\_SECRET=jzDTcS++yqI8BA28H+qLTaoZZk05XCrP+hKDtjhEEDw=  
MINIO\_ROOT\_USER=minioadmin   
MINIO\_ROOT\_PASSWORD=minioadmin123   
BUCKET\_NAME=upluxo-teste  
AWS\_ACCESS\_KEY\_ID=minioadmin  
AWS\_SECRET\_ACCESS\_KEY=minioadmin123  
AWS\_REGION="us-east-1"  
S3\_ENDPOINT=http://minio:9000/  
S3\_PUBLIC\_BASE\_URL=  
SMTP\_HOST=  
SMTP\_PORT=  
SMTP\_USERNAME=  
SMTP\_PASSWORD=  
SMTP\_FROM\_EMAIL=  
SMTP\_FROM\_NAME=  
SMTP\_USE\_SSL=true

**ui/web/.env:**  
\#Use apenas uma das opções  
VITE\_API\_URL="https://upluxo.digitalsysdev.com.br/" #Para usar api do servidor de dev  
\#VITE\_API\_URL="http://localhost:5000/api" #Para usar api rodando no servidor local