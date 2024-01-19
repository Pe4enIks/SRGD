FROM pytorch/pytorch:2.1.2-cuda12.1-cudnn8-runtime

ENV PYTHONUNBUFFERED=1 \
    PYTHONDONTWRITEBYTECODE=1 \
    PIP_NO_CACHE_DIR=off \
    PIP_DISABLE_PIP_VERSION_CHECK=on \
    PIP_DEFAULT_TIMEOUT=100 \
    POETRY_VERSION=1.6.1 \
    POETRY_NO_INTERACTION=1 \
    PATH="${PATH}:/root/.local/bin"

COPY api /backend/api
COPY configs /backend/configs
COPY dvc_data /backend/dvc_data
COPY model /backend/model
COPY submodules /backend/submodules
COPY utils /backend/utils
COPY pyproject.toml /backend/

WORKDIR /backend

RUN apt update && apt install -y curl
RUN curl -sSL https://install.python-poetry.org | python3 -
RUN poetry install --with api,ml

WORKDIR /backend/api
EXPOSE 8000

CMD poetry run uvicorn main:app --host 0.0.0.0 --port 8000