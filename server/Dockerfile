FROM python:3.12.0-slim-bookworm

ENV PYTHONBUFFERED 1
ENV PYTHONWRITEBYTECODE 1

ENV APP=/app

# Change the working directory
WORKDIR $APP

# Install the requirements
COPY requirements.txt $APP
RUN pip3 install -r requirements.txt

# Copy the rest of the files
COPY . $APP

# --- NEW LINES START HERE ---
# Create a non-root user and give them ownership of the files
RUN useradd -u 1001 appuser
RUN chown -R 1001 /app
USER 1001
# --- NEW LINES END HERE ---

# Expose port 8000
EXPOSE 8000

# Make the entrypoint script executable
RUN chmod +x /app/entrypoint.sh

# Define the entrypoint and command
ENTRYPOINT ["/bin/bash", "/app/entrypoint.sh"]
CMD ["gunicorn", "--bind", ":8000", "--workers", "3", "djangoproj.wsgi"]