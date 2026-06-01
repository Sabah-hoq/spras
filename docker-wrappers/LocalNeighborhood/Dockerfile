# Build stage using a modern Python Alpine image
FROM python:3.12-alpine AS builder

# Install build dependencies needed for certain Python packages
RUN apk add --no-cache build-base gcc musl-dev

WORKDIR /build

# Copy the configuration and source files from the root context
COPY pyproject.toml MANIFEST.in README.md LICENSE ./
COPY spras ./spras

# Install the local package securely to the user directory
RUN pip install --no-cache-dir --user -e .

# Runtime stage using a clean Python Alpine image
FROM python:3.12-alpine

WORKDIR /data

# Copy the installed dependencies from the builder stage
COPY --from=builder /root/.local /root/.local

# Update path environment variables
ENV PATH=/root/.local/bin:$PATH \
    PYTHONUNBUFFERED=1

ENTRYPOINT ["python"]
CMD ["-m", "spras.local_neighborhood"]# Create a Docker image for the Local Neighborhood algorithm here
