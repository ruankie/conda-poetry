# Args
# ARG CONDA_VER=4.12.0

# Base image
# FROM --platform=linux/amd64 continuumio/miniconda3:${CONDA_VER}
FROM --platform=linux/amd64 python:3.7.6-slim

# Switch to root
USER root:root

# Install common dependencies
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    build-essential \
    git \
    wget \
    curl && \
    apt-get clean -y && \
    rm -rf /var/lib/apt/lists/*

# Set working dir and copy all files to container
WORKDIR /app
COPY . .

# Create conda env with dependencies
# RUN conda env create -f /app/conda_env.yml

# Install poetry
ENV POETRY_VERSION=1.1.13
RUN curl -sSL https://raw.githubusercontent.com/python-poetry/poetry/master/get-poetry.py | python -
ENV PATH="${PATH}:/root/.poetry/bin"

# Install packages specified by poetry into conda env
# RUN conda run -n py376 --no-capture-output poetry install

# Install dependencies with poetry (without creating a virtual env)
RUN poetry config virtualenvs.create false
RUN poetry install

# Ensure new shells are opened inside the conda env
# RUN conda init bash
# RUN echo "conda activate py376" >> ~/.bashrc