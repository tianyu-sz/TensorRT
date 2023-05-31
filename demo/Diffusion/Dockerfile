FROM nvcr.io/nvidia/tensorrt:22.10-py3

COPY requirements.txt .

RUN python3 -m pip install --upgrade pip

RUN pip3 install -r requirements.txt

RUN pip3 install accelerate

RUN pip install tensorrt==8.5.3.1

