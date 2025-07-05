# Use an official Python runtime as a parent image
FROM python:3.11-slim

# Set environment variables
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1
ENV UV_EXTRA_INDEX_URL="https://test.pypi.org/simple/"

# Set work directory
WORKDIR /app

# Install uv
RUN pip install uv

# Create a non-root user
RUN useradd -m appuser

# Copy necessary files for installation
COPY pyproject.toml README.md ./
COPY mcp_simple_streamablehttp_stateless/ ./mcp_simple_streamablehttp_stateless/

# Install the project and its dependencies
# This also makes the [project.scripts] entry available
# We use --index-strategy unsafe-best-match to allow uv to find the best package version across all indexes
RUN uv pip install . --system --index-strategy unsafe-best-match

# Expose the port the app runs on
EXPOSE 3000

# Switch to the non-root user
# USER appuser

# Run the application
# We only use the supported options (--port, but not --host)
CMD ["mcp-simple-streamablehttp-stateless", "--port", "3000"]
