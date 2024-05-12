# TNMT API Service

## Overview
The TNMT API Service is designed to provide various functionalities for classifying and summarizing Natural Resources and Environment news articles. It offers endpoints for classifying articles, summarizing content, and combining both classification and summarization.

## Installation and Usage
To use the TNMT API Service, you have two options:

### Option 1: Docker
1. Ensure you have Docker installed on your system.
    Or download at https://www.docker.com/products/docker-desktop/
2. Pull the TNMT API Docker image from Docker Hub:
    ```
    docker pull huongntt/tnmt-api-service-server:v1
    ```
3. Run the Docker container:
    ```
    docker run -p 5000:5000 huongntt/tnmt-api-service-server:v1
    ```
4. The API service will be accessible at `http://localhost:5000`.

### Option 2: Manual Setup
1. Install Python (version 3.11) and pip.
2. Clone this repository:
    ```
    git clone https://github.com/huongntt309/TNMT_NLP_API_service.git
    ```
3. Navigate to the project directory:
    ```
    cd TNMT_NLP_API_service
    ```
4. Install the required dependencies:
    ```
    pip install -r requirements.txt
    ```
5. Start the API service:
    ```
    python app/app.py
    ```
6. The API service will be accessible at `http://localhost:5000`.

## Configuration
The API service can be configured through environment variables. You can customize settings such as port number, logging level, and model paths by setting the corresponding environment variables.

## Example
Here is an example of how to use the API endpoints:
### API Endpoints
0. `GET /` - an endpoint to test the API with Website User Interface 
1. `POST /classify`
2. `POST /summarize`
3. `POST /sum-cls`


### API Input Format
3 POST requests has the same following format:
```bash
[
    {
        "id"        : "1",
        "title"     : "Trách nhiệm của ... cầm quân đội tuyển Việt Nam",
        "anchor"    : "Lãnh đạo VFF ... U23 Việt Nam",
        "content"   : "Lãnh đạo VFF cho biết, ... đấu trường khu vực đến châu lục."
    },
    {
        "id"        : "2",
        "title"     : "Hồ sơ Luật Địa chất và Khoáng sản cơ bản đáp ứng yêu cầu",
        "anchor"    : "(TN&MT) - Tại cuộc họp ... chiều 10/1",
        "content"   : "Chủ trì cuộc họp ... trình Chính phủ xem xét, quyết định."
    }
]
```

### API Output Format
```bash
[
    {
        "id"        : "1",                          
        "topic"     : "Không",                           
        "sub_topic" : [],                
        "aspect"    : [],         
        "sentiment" : "Không",                      
        "province"  : [],
    },
    {
        "id"        : "2",
        "summary"   : "Ngày 10/1 tại Hà Nội, ... những điểm nổi bật của dự thảo.",
        "topic"     : "Có",
        "sub_topic" : ["Địa chất - Khoáng sản"],
        "aspect"    : ["chính sách, quản lý", "Luật sửa đổi"],
        "sentiment" : "Trung tính",
        "province"  : ["Hà Nội"]
    }
]
```

### API Testing
We create a json test file in **app/bow_folder/21-test-cases.json**, you can use this data at Request Body, then test this at `http://localhost:5000/sum-cls`.

## Technology used
1. "VietAI/vit5-base": ViT5, Pre-trained Text-to-Text Transformer for Vietnamese Language Generation.
2. "vinai/bartpho-syllable": BARTpho, Pre-trained Sequence-to-Sequence Models for Vietnamese.
3. Flask API: A lightweight web framework for Python, offering simplicity and flexibility for building RESTful APIs.

## Contact
For any inquiries or support, please contact [huonguet8@gmail.com](mailto:huonguet8@gmail.com).
