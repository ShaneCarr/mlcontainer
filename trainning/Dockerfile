# Use the NVIDIA CUDA base image
FROM nvcr.io/nvidia/cuda:11.4.2-cudnn8-devel-ubuntu20.04

# Set the working directory
WORKDIR /workspace

# Install necessary tools and dependencies
RUN apt-get update && \
    apt-get install -y python3 python3-pip git && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Install virtualenv
RUN pip3 install virtualenv

# Create a virtual environment
RUN virtualenv ml_env

# Activate the virtual environment and install required Python packages
RUN /bin/bash -c "source ml_env/bin/activate && \
    pip install --upgrade pip && \
    pip install jupyter numpy pandas scikit-learn tensorflow keras matplotlib seaborn torch torchvision torchaudio transformers"

# Expose Jupyter Notebook port
EXPOSE 8888

# Add a script to start Jupyter Notebook
RUN echo '#!/bin/bash\nsource ml_env/bin/activate\njupyter notebook --ip=0.0.0.0 --port=8888 --no-browser --allow-root' > /workspace/start_jupyter.sh
RUN chmod +x /workspace/start_jupyter.sh

# Set the default command to start Jupyter Notebook
CMD ["/workspace/start_jupyter.sh"]

