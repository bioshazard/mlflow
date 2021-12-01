ARG PYTHON_TAG="3.9.9-slim-buster"
ARG MLFLOW_PKG="mlflow[extras]"
ARG MLFLOW_PIP_EXTRA=""
FROM python:${PYTHON_TAG}

# Create non-root user
RUN useradd -m mlflow
WORKDIR /home/mlflow
USER mlflow

# Set defaults and add pip user install to PATH
ENV PATH="/home/mlflow/.local/bin:${PATH}"
ENV MLFLOW_HOST 0.0.0.0
ENV MLFLOW_BACKEND_STORE sqlite:///mlflow.db
ENV MLFLOW_ARTIFACT_ROOT ./artifacts
ENV MLFLOW_EXTRA_ARGS ""

# Install MLFlow
ARG MLFLOW_PKG
ARG MLFLOW_PIP_EXTRA
RUN pip install --user ${MLFLOW_PKG} ${MLFLOW_PIP_EXTRA}

# RUN pip install -U mlflow \
        # flask pandas gunicorn

# Run server with defaults
CMD mlflow server ${MLFLOW_EXTRA_ARGS} -h ${MLFLOW_HOST} \
        --backend-store-uri ${MLFLOW_BACKEND_STORE} \
        --default-artifact-root ${MLFLOW_ARTIFACT_ROOT}
