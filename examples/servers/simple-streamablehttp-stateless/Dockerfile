# Use an official Python runtime as a parent image
FROM python:3.11-slim

# Set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1
ENV UV_EXTRA_INDEX_URL="https://test.pypi.org/simple/"

# Set work directory
WORKDIR /app

# Install uv
RUN pip install uv

# Create a non-root user
RUN useradd -m appuser

# Copy the project definition file and install dependencies
COPY pyproject.toml .

# Install the project and its dependencies
# This also makes the [project.scripts] entry available
RUN uv pip install . --system

# Copy the rest of the application code
COPY mcp_simple_streamablehttp_stateless/ ./mcp_simple_streamablehttp_stateless/

# Expose the port the app runs on
EXPOSE 3000

# Switch to the non-root user
USER appuser

# Run the application
# We add --host 0.0.0.0 to make the server accessible from outside the container
CMD ["uv", "run", "mcp-simple-streamablehttp-stateless", "--host", "0.0.0.0", "--port", "3000"]
